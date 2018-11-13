Med ABS kan en Arch Linux-bruger let kompilere en kilde til en pkg.tar.gz-**pakke**.

## Contents

*   [1 Hvad er en pakkefil?](#Hvad_er_en_pakkefil?)
*   [2 Hvad er en PKGBUILD? Og hvad indeholder det?](#Hvad_er_en_PKGBUILD?_Og_hvad_indeholder_det?)
*   [3 Byggefunktionen forklaret](#Byggefunktionen_forklaret)
*   [4 Mere ABS-information](#Mere_ABS-information)

#### Hvad er en pakkefil?

Husk at ABS downloader automatisk kildekoden for netop det software, du kompilerer. Derefter pakker det ud, kompilerer kilderne og klemmer det hele ind i en installerbar pakke. Typisk er resultatet en pakkefil ved navn foo.pkg.tar.gz.

Faktisk er det blot en g-zippet tar-arkiv eller 'tarball', der indeholder:

*   De filer der skal installeres.
*   Filen .PKGINFO: indeholder alle metadata, der er nødvendige, for at Pacman kan håndtere pakker, afhængigheder osv.
*   Filen .FILELIST: viser en liste over alle filer i arkivet. Det benyttes i forbindelse med afinstallation , eller for at tjekke for filkonflikter.
*   Filen .INSTALL: bruges til at eksekvere kommandoer efter installér-/opgradér-/fjern-trinet (Denne fil findes kun, hvis den er specificeret i PKGBUILD.)

Eftersom Pacman håndterer 'tar.gz'-pakker, kan 'foo.pkg.tar.gz' nu let installeres/fjernes.

#### Hvad er en PKGBUILD? Og hvad indeholder det?

Som forklaret før indeholder filen PKGBUILD metadata om en pakke. Det er en simpel tekstfil. Her er et eksempel:

```
 # $Id: PKGBUILD,v 1.12 2003/11/06 08:26:13 dorphell Exp $
 # Maintainer: judd <jvinet@zeroflux.org>
 # Contributor: Judd Vinet <jvinet@zeroflux.org>
 pkgname=foo
 pkgver=0.99 # BEMÆRK: Hvis pakkeversionen havde været '0.99-10', så benyt en bundstreg som f.eks. '0.99_10'.
 pkgrel=1
 pkgdesc="en kort beskrivelse af 'foo'"
 arch=(i686 x86_64)
 url="http://www.foo.org"
 license=('GPL')
 groups=
 provides=
 depends=('qt' 'python')
 makedepends=('guile')
 conflicts=('yafoo')
 replaces=('mffoo')
 backup=('etc/foo/foo.conf')
 install=foo.install
 source=(http://www.foo.org/download/$pkgname-$pkgver.tar.gz)
 md5sums=('2c0cca3ef6330a187c6ef4fe41ecaa4d35175bee593a7cc7d6205584a94d8625')

 build() {
 cd $startdir/src/$pkgname-$pkgver
 ./configure --prefix=/usr
 make || return 1
 make prefix=$startdir/pkg/usr install
 }

```

Så lad os forklare hvert felt:

*   **# text**: kommentarer
*   **# $Id: PKGBUILD,v** ...: Er cvs-flaget for denne pakke (oprettet fra systemet 'archlinux-cvs').
*   **# Maintainer**: Den ansvarlige vedligeholder for denne pakke i de officielle software-kilder.
*   **# Contributor**: Personen der skrev den første PKGBUILD for denne pakke.
*   **pkgname**: Pakkens navn.
*   **pkgver**: Pakkens version.
*   **pkgrel**: Arch-pakkens udgivelsesnummer. Dette er forskelligt fra pakkeversionen, og ændres når PKGBUILD ændres. Der kan være mange årsager til dette, f.eks hvis du aktiverer understøttelse af kompileringstid for noget.
*   **pkgdesc**: En kort beskrivelse af pakken. Dette er hvad du sernår du browser pakkedatabasen
*   **arch**: Viser på hvilke arkitekturer, det er kendt for at bygge og virke - se Arch64_FAQ for detaljer om portering.
*   **url**: Hjemmesiden for softwaren (som kommer frem, når du klikker på en pakke i pakkedatabasen).
*   **license**: Licensen under hvilken dette software distribueres.
*   **groups**: Dette anvendes til at gruppere pakker. Hvis du f.eks. installerer KDE, installeres alle pakker, der tilhører gruppen KDE.
*   **provides**: Dette anvendes, hvis pakken leverer en anden pakke, som f.eks. 'kernel-scsi' leverer 'kernel'.
*   **depends**: Dette viser en lisgte over kørselstids-afhængigheder (hvad den skal bruge for at fungere).
*   **makedepends**: Afhængigheder der er kræves for at bygge pakken, men ikke er nødvendige, når pakken er bygget.
*   **conflicts**: Disse pakker kan ikke installeres på samme tid. Her konflikter foo med yafoo (yet another foo).
*   **replaces**: Den nye pakke erstatter den gamle. Her understøttes mffoo (min første foo) ikke længere og erstattes af foo
*   **backup**: Hvilke filer der skal tages backup af (som fil.pacsave), når pakken fjernes.
*   **install**: Angiver et specielt installations-script, som skal inkluderes i pakken (det skal forefindes i samme mappe som PKGBUILD).
*   **source**: Dette angiver, hvorfra pakkens kildekode skal downloades. Dette kan være en lokal pakke, en 'http' eller en 'ftp'. Dette navngives med pkgver for at undga at ændre kilden, hver gang der skiftes version.
*   **md5sums**: Kildens md5-sum for at tjekke integriteten.

Så lad os nu forklare funktionen:

*   build: alle krævede aktioner for at bygge pakken (dette forklares nærmere senere i denne artikel).

Du kan se, at filen PKGBUILD indeholder alt det information, der kan kræves af pakkehåndteringen. Dette er hjertet af Pacman og ABS.

Der er også installationsfiler. Denne PKGBUILD specificerer 'foo.install' som pakkens installationsfil. Her er et eksempel på en installationsfil:

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

Her er en forklaring på funktionerne:

*   post_install: Dette script køres lige efter filerne er installerede. Det kræver ét argument:
    *   Pakkeversionen
*   post_upgrade: Dette script køres efter alle filer er opgraderede. Det kræver to argumenter:
    *   Den nye pakkeversion
    *   Den gamle pakkeversion
*   pre_remove: Dette script køres umiddelbart før filer fjernes (til f.eks at stoppe en dæmon). Det kræver ét argument:
    *   Pakkeversionen

De tre linjer i bunden kræves af alle installationsfiler, for at de kan køres ordentligt.

#### Byggefunktionen forklaret

Lad os kigge på en byggefunktion, som den dikteres af PKGBUILD-eksemplet ovenfor. Bemærk byggesektionen:

```
build() {
cd $startdir/src/$pkgname-$pkgver
./configure --prefix=/usr
make || return 1
make prefix=$startdir/pkg/usr install
}

```

Der sker følgende:

*   går ind i mappen, hvor kilderne blev pakket ud:

```
cd $startdir/src/$pkgname-$pkgver

```

*   konfigurerer pakken og fortæller at den skal installeres i mappen /usr:

```
./configure --prefix=/usr

```

*   kompilerer

```
make || return 1

```

*   installerer softwaren - ikke i /usr men i stedet i $startdir/pkg/usr så Pacman har kontrol over filerne.

```
make prefix=$startdir/pkg/usr install

```

Det, vi vil gøre, er at bygge pakken - ikke at installere den. Så i stedet for at installere den i standardmappen (/usr), siger vi til make, at den skal lægge alle filer ind i vores specielle mappe: $startdir/pkg/usr. På denne måde kan 'makepkg' se, hvilke filer pakken installerer, og derefter komprimere dem ind i Arch-pakken.

BEMÆRK: Det sker, at prefix ikke anvendes i Makefile, hvor DESTDIR bruges i stedet for. Hvis pakken bygges med autoconf/automake benyttes DESTDIR. Det er, hvad der beskrives i manualerne. Tjek om den genererede filelist er meget kortere ned den burde være, i så fald prøv at bygge den med make DESTDIR=$startdir/pkg install. Hvis dette ikke virker, skal du prøve at kigge dybere ind i de installationskommandoer, der eksekveres af "make <...> install=".

#### Mere ABS-information

*   [ABS](/index.php/ABS "ABS") The Arch Build System
*   [Creating packages](/index.php/Creating_packages "Creating packages")
*   [Makepkg](/index.php/Makepkg "Makepkg")
*   [Safe Cflags](/index.php/Safe_Cflags "Safe Cflags")
*   [Kernel Compilation with ABS](/index.php/Kernel_Compilation_with_ABS "Kernel Compilation with ABS")
*   [Arch User Repository](/index.php/Arch_User_Repository "Arch User Repository")
*   [Custom local repository with ABS and gensync](/index.php/Custom_local_repository_with_ABS_and_gensync "Custom local repository with ABS and gensync")