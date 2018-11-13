## Contents

*   [1 Úvod](#Úvod)
*   [2 Instalace balíčků](#Instalace_balíčků)
*   [3 Co je to balíček ?](#Co_je_to_balíček_?)
*   [4 Co je PKGBUILD a co obsahuje?](#Co_je_PKGBUILD_a_co_obsahuje?)
*   [5 Funkce build](#Funkce_build)
*   [6 Strom ABS](#Strom_ABS)
*   [7 První použití ABS : přizpůsobení balíčku](#První_použití_ABS_:_přizpůsobení_balíčku)
*   [8 Compiler Flags a úpravy makepkg](#Compiler_Flags_a_úpravy_makepkg)

#### Úvod

Arch Build System (ABS zkratkou) se používá pro

*   Tvorbu nových balíčků jenž ještě neexistují
*   Úpravu existujících balíčků pro vlastní potřeby (např. přidání parametru)
*   Re-build celého vašeho systému s použitím compiler flags, "ala freebsd" (a rozběhnutí modulů jádra s vaším vlastním kernelem!)

ABS není nezbytný pro používání Arch Linuxu ale je užitečný.

Toto how-to se vám pokusí dát přehled o ABS a baličcích Archu, není to kompletní referenční příručka! Pokud chcete víc, zkuste si přečíst manuálovou stránku.

#### Instalace balíčků

Pro použití abs, musíte nejprve nainstalovat **cvsup** a **wget**, to uděláte snadno příkazem:

 `pacman -S cvsup wget` 

Nebo, pokud máte stažené balíčky do adresáře pojmenovaného 'foo' (pro příklad):

```
cd foo
pacman -U  cvsup-*.pkg.tar.gz  wget-*.pkg.tar.gz
```

#### Co je to balíček ?

Typický soubor balíčku má tvar *balíček*.pkg.tar.gz

Ve skutečnosti to neni víc než gzipovaný tar archiv který obsahuje:

*   Soubory pro instalaci

*   .PKGBUILD : obsahuje všechna metadata potřebné pacmanem k výměně s balíčky, závislostmi, apod.

*   .FILELIST : seznam všech souborů obsažených v archivu. Je to vhodné pro zpětné odinstalování nebo konfliktu souborů.

*   .INSTALL : soubor pro provedení příkazů po instalaci/upgradu/odebrání.

#### Co je PKGBUILD a co obsahuje?

Vzhledem k vysvětlení výše, soubor [PKGBUILD](/index.php/PKGBUILD_(%C4%8Cesky) "PKGBUILD (Česky)") obsahuje metadata o balíčcích. Je to jednoduchý textový soubor. Zde je příklad:

```
# $Id: PKGBUILD,v 1.12 2003/11/06 08:26:13 dorphell Exp $
# Maintainer: judd <jvinet@zeroflux.org>
# Contributor: Judd Vinet <jvinet@zeroflux.org>
pkgname=foo
pkgver=0.99 # note: if the pkgver had been '0.99-10' then use an underscore. like '0.99_10'
pkgrel=1
pkgdesc="short description of foo"
arch=(i686 x86_64)
url="http://www.foo.org"
groups=
provides=
depends=('qt' 'python')
makedepends=('guile')
conflicts=('yafoo')
replaces=('mffoo')
backup=('etc/foo/foo.conf')
install=('foo.install')
source=(http://www.foo.org/download/$pkgname-$pkgver.tar.gz)
md5sums=('2c0cca3ef6330a187c6ef4fe41ecaa4d35175bee593a7cc7d6205584a94d8625')

build() {
  cd $srcdir/$pkgname-$pkgver
  ./configure --prefix=/usr
  make || return 1
  make prefix=$pkgdir/usr install
}

```

Zde si vysvětleme jednotlivé pojmy :

*   **# text** : komentář
*   **# $Id: PKGBUILD,v ...** : cvs-tag pro tento balíček (z archlinux-cvs system)
*   **# Maintainer** : vývojář zodpovědný za balíček v oficiálním repozitáři
*   **# Contributor** : osoba která napsala PKGBUILD pro tento balíček
*   **pkgname** : jméno balíčku
*   **pkgver** : verze balíčku
*   **pkgrel** : číslo vydání Arch balíčku. V základu je to číslo verze změněné pokud je PKGBUILD modifikován. To se může přihodit z mnoha důvodů pro příklad pokud povolíte compile-time pro něco.
*   **pkgdesc** : výstižný popis balíčku. Toto je co uvidíte pokud se podíváte na [databázi balíčků](https://archlinux.org/packages/)
*   **arch** : ukazuje na jakou architektutu je tvořen a odskoušen [Arch64 FAQ](/index.php/Arch64_FAQ "Arch64 FAQ") pro portování.
*   **url** : domovská stránka softwaru (objevíse pokud kliknete na balíček v databázi balíčků)
*   **groups** : je užívané ve skupinách balíčků: například když zkusíte nainstalovat kde, nainstalujete všechny balíčky obsažené ve skupině kde.
*   **provides** : pokud balíček poskytuje jiný balíček, pro příklad kernel-scsi poskytuje kernel
*   **depends** : seznam závislostí balíčku (co potřebuje k běhu)
*   **makedepends** : závislosti potřebné k tvorbě balíčku ale nepotřebné k samotnému spuštění
*   **conflicts** : balíčky které jsou v konfliktu. Např, *foo* má konflikt s *yafoo (yet another foo)*. Nemohou proto být nainstalovány společně.
*   **replaces** : nový balíček přepíše starý. Pokud *mffoo (my first foo)* je podporován, přepíše *foo*
*   **backup** : soubory pro zálohu (jako soubor.pacsave) pokud je balíček odstraněn
*   **install** : specifikuje speciální instalační script který může být obsažen v balíčku (ve stejném adresáři jako PKGBUILD)
*   **source** : specifikuje cestu odkud stáhnout zdrojový kód balíčku. Může to být např. "http" nebo "ftp".
*   **md5sums** : md5 součet pro ověření integrity

Tak pojdme si vysvětlit funkci :

*   build : všechny akce potřebné pro tvorbu balíčku (to bude vysvětleno v tomto dokumentu níže)

Dobře, podíváme se co PKGBUILD obsahuje za informace potřebné pro správce balíčků. To je srdce pacmana a abs.

Jsou tam také instalační soubory. Soubor PKGBUILD odkazuje na 'foo.install' jako na instalační soubor balíčku. Zde je příklad instalačního souboru:

```
post_install() {
/bin/true
}

post_upgrade() {
/bin/true
}

pre_remove() {
/bin/true
}

op=$1
shift

$op "$@"

```

Zde je vysvětlení funkcí :

*   post_install : tento script se spustí když jsou soubory nainstalovány, předává jeden argument :
    *   the package version
*   post_upgrade : tento script se spustí jsou-li soubory upgradovány *předává dva argumenty*  :
    *   the new package version
    *   the old package version
*   pre_remove : spustí se jsou-li soubory odstraněny (například zastaví daemona) a předá jeden argument :
    *   the package version

Ostatní jsou řádky potřebné pro každou instalaci.

#### Funkce build

Jestli nejste seznámen s tvorbou balíčku, měl by jste vědět že většina balíčků (ale ne všechny) jde vytvořit touto cestou :

*   rozbalit zdrojový soubor :

```
  tar -xzf foo-0.99.tar.gz
  tar -xjf foo-0.99.tar.bz2
```

*   otevřít adresář

 `cd foo-0.99` 

*   konfigurace balíčku : V adresáři je malý script zvaný `configure` který je použit ke konfiguraci balíčku a kontrole zda má váš pačítač všechen potřebný software. Můžete ho spustit pomocí :

 `./configure [[option]]` 

Klidně se můžete podívat na nápovědu jak to pracuje :

 `./configure --help` 

*   kompilace zdroje :

 `make` 

*   instalace

 `make install` 

Vždycky by jste měl číst soubor `INSTALL` pro informace jak program sestavit a nainstalovat ! **Všechny balíčky nepoužívají `configure; make; make install` systém!**

Podívejme se nyní na "standardní" build funkci :

```
build() {
  cd ${srcdir}/${pkgname}-${pkgver}
  ./configure --prefix=/usr
  make || return 1
  make prefix=${pkgdir}/usr install
}

```

Co děláme je to, že :

*   zadání adresáře kde máme zdrojové kódy :

 `cd ${srcdir}/${pkgname}-${pkgver}` 

Pokud zkoušíte sestavit balíček, pečlivě zkontrolujte, že je to správný adresář : někdy je adresář pojmenován :

 `tar -xzf foo-0.99.tar.gz` 

a `ls` může vypsat :

```
  .
  ..
  foo-0.99.tar.gz
  foo/
```

a ne :

```
  .
  ..
  foo-0.99.tar.gz
  foo-0.99/
```

*   konfigurace balíčku a provedení instalace v adresáři `/usr` :

 `  ./configure --prefix=/usr` 

*   kompilace

 `  make || return 1` 

*   instaluje software ale ne v adresáři `/usr`, ale v `${pkgdir}/usr`.

 `  make prefix=${pkgdir}/usr install` 

Co potřebujeme je vytvořit balíček ale neinstalovat ho do standartního adresáře (`/usr`), my chceme pomocí `make` nastavit náš speciální adresář : `${pkgdir}/usr`.

#### Strom ABS

Když spustíte poprvé abs :

 `# abs` 

provede se synchronizace věci zvané "strom ABS" což by se vlastně dalo nazvat jako cvs system Archlinuxu. Takže co je vlastně ABS strom ? Je uložen v /var/abs vypadá takto :

```
|-
| -- base/
|-
|     ||-- autoconf/
|-
|     ||-- automake/
|-
|     ||-- ...
|-
| -- devel/
|-
| -- ...
|-
| -- extra/
|-
|      || -- daemons/
|-
|      ||      || -- acpid/
|-
|      ||      ||      || -- PKGBUILD
...    ...    ...    ...

```

ABS strom má strukturu abs databáze :

*   první úroveň adresáře reprezentuje kategorii
*   první úroveň adresářů reprezentuje balíčky
*   PKGBUILD obsahují všechny informace vztahující se k balíčku

Existuje speciální adresář : **local**. Tento adresář je *váš*, Tohle je to pravé místo kam budete vše dávat : Nikdy nemodifikujte položky stromu !.

Takže nyní již víme co je ABS strom. Jak ho ale používat ?

#### První použití ABS : přizpůsobení balíčku

Tato situace nastane jistě víckrát než se domníváte : oficiální balíčky jsou kompilované s centrálním kódováním `--enable` nebo `--disable`.

Pro ilustraci uvedu příklad : *foo* Balíček *foo* je sestaven bez **arts** podpory. Představme si že chceme povolit **arts**. Zde je návod jak to udělat :

*   najděte kde je *foo* balíček umístěn. Můžete to udělat pomocí :

 `  find /var/abs -name "foo"` 

nebo použijte příkaz slocate :

 `  slocate foo | grep ^/var/abs` 

Zjistili jsme že foo patří do `extra` a `multimedia` (pro příklad)

*   kopírujte *foo* `PKGBUILD` do `/var/abs/local/foo`

```
  mkdir /var/abs/local/foo
  cp /var/abs/extra/multimedia/foo/* /var/abs/local/foo
  cd /var/abs/local/foo
```

*   modifikujte `PKGBUILD` : pro podporu **arts** :

```
  build() {
    cd ${srcdir}/${pkgname}-${pkgver}
    ./configure --prefix=/usr
    make || return 1
    make prefix=${pkgdir}/usr install
  }
```

becomes :

```
  build() {
    cd ${srcdir}/${pkgname}-${pkgver}
    ./configure --enable-arts --prefix=/usr
    make || return 1
    make prefix=${pkgdir}/usr install
  }
```

*   launch `makepkg` :

 `  makepkg` 

*   nainstalujte balíček (`-A` pro instalaci, `-U` pro upgrade):

```
  pacman -A foo-*.pkg.tar.gz
  pacman -U foo-*.pkg.tar.gz
```

#### Compiler Flags a úpravy makepkg

Konfigurační soubor `makepkg` je `/etc/makepkg.conf`. Zde můžeme nastavit parametry pro `gcc` a `make`, také nějaké pro `makepkg`. Následuje příklad `/etc/makepkg.conf`.

```
# FTP/HTTP download utilita kterou makepkg použije k získání zdrojových kódů
export FTPAGENT="/usr/bin/wget --continue --passive-ftp --tries=3 --waitretry=3"

# Informace pro gcc jaký typ počítače používáte.
export CARCH="i686"
export CHOST="i686-pc-linux-gnu"

# Flags pro gcc když balíček zkompiluje
export CFLAGS "-march athlon-tbird -O2 -pipe"
export CXXFLAGS "-march athlon-tbird -02 -pipe"

# Flags pro make když balíček zkompiluje
export MAKEFLAGS="-j 2"

# Povolí barevně odlišený výstup
export USE_COLOR="y"

# Povolte fakeroot pro sestavení balíčků bez nutnosti být root.
# Napište 'man fakeroot' pro více informací
export USE_FAKEROOT="y"

# Adresář kde jsou umístěny všechny balíčky (default is ./)
export PKGDEST=/home/packages

# ABS strom (default is /var/abs)
export ABSROOT=/var/abs

# Zde napište svoje jméno chcete-li
export PACKAGER="John Doe <nowhere@microsoft.com>"

```

Upozornění: Uživatel by si měl být jistý že změny `CFLAGS`, `CXXFLAGS` a `MAKEFLAGS` nezpůsobí problémy nebo nestabilitu. Většina uživatelů nemění hodnoty pro `CARCH`, `CHOST`, a `USE_FAKEROOT`.

References for gcc and make flags

*   [[1]](http://gcc.gnu.org/onlinedocs/gcc-3.4.3/gcc/Option-Summary.html#Option-Summary)
*   [*chapter/make*9.html#SEC102](http://www.gnu.org/software/make/manual/html)