`PKGBUILD` je textový soubor, ve kterém je přesně určeno, jak se bude vytvářet určitý binární balíček. Více [zde](/index.php/Creating_packages "Creating packages"). Tento článek pouze popisuje proměnné, které lze při vytváření tohoto souboru použít.

## Sestavování balíčků

Balíčky jsou v ArchLinuxu sestavovány programem [makepkg](/index.php/Makepkg "Makepkg"). Při jeho spuštění se program pokouší najít `PKGBUILD` ve vašem pracovním adresáři. Pokud ho najde, přečte si ho a podle jednotlivých instrukcí v něm obsažených začne sestavovat balíček. Pokud je vše provedeno bez chyb, vznikne soubor (`pkgname.pkg.tar.xz`). Tento balíček obsahuje binární soubory a instrukce pro instalaci. Takto vytvořený balíček lze nainstalovat pomocí správce balíčků [pacman](/index.php/Pacman_(%C4%8Cesky) "Pacman (Česky)").

Pro více informací běžte na [vytváření balíčků](/index.php/Creating_packages "Creating packages").

## Proměnné

Následující proměnné mohou být použity v souboru `PKGBUILD`:

	`pkgname` 

	Obsahuje jméno balíčku. Mělo by se skládat z **alfanumerických znaků a pomlčky ('-')**. Všechna písmena by měla být malá (**lowercase**). V zájmu soudržnosti by se měla proměnná `pkgname` shodovat s názvem zdrojového archivu programu, pro který balíček vytváříte. Například, pokud je jméno tarballu `foobar-2.5.tar.gz`, měla by hodnota `pkgname` být *foobar*.

	`pkgver` 

	Verze balíčku. Hodnota proměnné by měla být stejná jako verze sestavovaného programu. Může obsahovat písmena, čísla a tečky ale **NEMĚL BY** obsahovat pomlčku. Pokud autor programu používá ve verzi pomlčku, nahraďte ji podtržítkem. Například, pokud je verze programu *0.99-10*, měla by být změněna na *0.99_10*. Pokud je pak proměnná použita dále ve skriptu, lze jednoduše podtržítko nahradit pomlčkou následovně:

```
 source=($pkgname-${pkgver//_/-}.tar.gz)

```

	`pkgrel` 

	Tato proměnná zastupuje číslo release. Umožňuje uživatelům rozlišit mezi jednotlivými verzemi `PKGBUILD`u. Když je vydána první verze balíčku, začíná proměnná `pkgrel` **na hodnotě 1**. Pokud později nastanou ruzné optimalizace souboru `PKGBUILD`, balíček bude **vydán znovu** a **release číslo** se zvýší o 1\. Pokud pak vyjde nová verze sestavovaného programu, release číslo verze se nastaví opět na 1.

	`epoch` 

	Je to číselná hodnota, která umožňuje rozdíl verzí. Defaultně se do této proměnné vloží nula. Nepoužívejte ji, pokud nevíte co děláte.

	`pkgdesc` 

	Krátký popis balíčku. Popis by měl být dlouhý okolo 80 znaků nebo méně a neměl by v sobě obsahovat znovu jméno programu. Například, místo "Nedit is a text editor for X11" by mělo spíše být "A text editor for X11."

	`arch` 

	Pole architektur na kterých je možné balíček správně zkompilovat a spustit. V současné době většinou obsahuje **i686** a/nebo **x86_64**, `arch=('i686' 'x86_64')`. Hodnota **any** může být použita také, pokud sestavujete na platformě nezávislý balíček. Při samotném průběhu sestavování balíčku pak k této hodnotě můžete přistupovat pomocí proměnné `$CARCH`.

	`url` 

	V této proměnné je obsažena oficiální stránka programu, který sestavujete.

	`license` 

	Toto pole obsahuje licenci pod kterou je program distribuován. V repozitáři `[core]` byl vytvořen balíček [licenses](https://www.archlinux.org/packages/?name=licenses), který obsahuje nejběžnější licence. Soubory licencí jsou pak uloženy v adresáři `/usr/share/licenses/common`, například známou `/usr/share/licenses/common/GPL`. Pokud je balíček licencován pod některou z těchto licencí, měla by být proměnná nastavena na jméno adresáře tzn. `license=('GPL')`. Jestliže se licence, pod kterou je program vydáván v adresáři nenachází, musíte ještě udělat pár věcí:

1.  Pokud archiv se zdrojovými kódy programu **neobsahuje** žádný soubor s licencí, budete pravděpodobně muset licenci odněkud zkopírovat, například z oficiálních stránek programu. Následně ji uložit do souboru a zajistit to, aby se licence nainstalovala spolu s balíčkem, který vytváříte.
2.  Nastavte pole `license` na **custom**. Případně ještě můžete nahradit **custom** za **custom:jméno neoficiální licence**. Pokud je daná licence použita u dvou a více programů z oficiálního repozitáře (včetně `[community]`), stává se součástí balíčku [licenses](https://www.archlinux.org/packages/?name=licenses).

*   Licence [BSD](https://en.wikipedia.org/wiki/BSD_License "wikipedia:BSD License"), [MIT](https://en.wikipedia.org/wiki/MIT_License "wikipedia:MIT License"), [zlib/png](https://en.wikipedia.org/wiki/ZLIB_license "wikipedia:ZLIB license") a [Python](https://en.wikipedia.org/wiki/Python_License "wikipedia:Python License") jsou speciální případy, které nemohou být obsažené v balíčku [licenses](https://www.archlinux.org/packages/?name=licenses). Pokud je program vydáván pod některou z těchto licencí vložte ji do pole `license` takto (`license=('BSD')`, `license=('MIT')`, `license=('ZLIB')` nebo `license=('Python')`). Každý z těchto balíčků by měl mít svou vlastní unikátní licenci uloženou v `/usr/share/licenses/**pkgname**`. Některé balíčky nemusejí být vždy vydávány pouze pod jednou licencí, proto lze do pole vložit licencí více. Například takto `license=('GPL' 'custom:jméno licence')`.
*   Kromě toho například (L)GPL má plno různých podob, proto je pro (L)GPL software dodržována tato konvence:
    *   (L)GPL - (L)GPLv2 nebo kterákoliv pozdější verze
    *   (L)GPL2 - (L)GPL2 pouze
    *   (L)GPL3 - (L)GPL3 nebo kterákoliv pozdější verze

	`groups` 

	Jméno skupiny do které balíček patří. Například když nainstalujete balíče [kdebase](https://www.archlinux.org/groups/x86_64/kdebase/), nainstalují se zároveň i ostatní balíčky, které patří do skupiny *kde*.

	`depends` 

	Pole jmen balíčků, které musí být pro spuštění sestavovaného programu nainstalovány. Pokud program vyžaduje nějakou určitou verzi balíčku, lze ji definovat použitím operátoru **>=**, například takto: `depends=('foobar>=1.8.0')`.

	`makedepends` 

	Je pole jmen balíčků, které musí být nainstalovány, aby šel daný program zkompilovat, ale nejsou už potom potřeba pro samotný běh programu. Můžete také specifikovat minimální verzi závislého balíčku. To se nastavuje úplně stejně jako u pole `depends`.

**Warning:** Skupina balíčků "base-devel" je už nainstalovaná automaticky, pokud vše sestavujete pomocí programu makepkg. Takže by balíčky z této skupiny **neměly** být obsaženy v tomto poli.

	`optdepends` 

	Je pole balíčků, které obsahuje jména programů, které nejsou nutně potřeba pro běh programu, ale pouze poskytují nějaké nadstandartní funkce. U každého zmíněného balíčku by měla být obsažena krátká informace o tom, co poskytuje. Pole `optdepends` by mohlo vypadat například následovně:

```
optdepends=('cups: printing support'
'sane: scanners support'
'libgphoto2: digital cameras support'
'alsa-lib: sound support'
'giflib: GIF images support'
'libjpeg: JPEG images support'
'libpng: PNG images support')

```

	`provides` 

	Pole jmen balíčků, které tento balíček funkčně zastupuje. Pokud toto pole použijete, měli byste ještě definovat proměnnou (`pkgver`, případně i `pkgrel`). Například pokud poskytujete upravenou verzi *qt* v balíčku pojmenovaném *qt-foobar* verze 3.3.8, mělo by pole `provides` vypadat nějak takto: `provides=('qt=3.3.8')`. Proměnnou `pkgname` do tohoto pole nepřidávejte - *makepkg* to udělá za vás.

	`conflicts` 

	Pole jmen balíčků, které mohou způsobovat problémy, když bude tento program nainstalován. Mužete zde také specifikovat konfliktní verzi balíčku - stejně jako u pole `depends`.

	`replaces` 

	Pole jmen balíčků, které mají být nahrazeny tímto balíčkem. Například `replaces=('ethereal')`. Pokud poskytujete alternativní verzi nějakého existujícího balíčku, použijte pole `conflicts`.

	`backup` 

	Toto pole obsahuje jména souborů, které se mají zálohovat a tím pádem uložit jako `soubor.pacsave` když je balíček odinstalován ze systému. Toto se většinou používá u balíčků, které svou konfiguraci ukládají do adresáře `/etc`. Cesty definované v tomto poli by měly být relativní. Takže například `etc/pacman.conf`. Nepoužívejte absolutní cesty! (`/etc/pacman.conf`).

	`options` 

	Toto pole vám umožňuje změnit základní chování programu `makepkg`. Pro nastavení vložte jméno určité volby do pole. Pro změnu defaultní volby na opačnou hodnotu vložte **!** na začátek jména. V poli lze použít následující:

*   ***strip*** - Odstranění symbolů z binárních souborů a knihoven.
*   ***docs*** - Uložení adresářů `/doc`.
*   ***libtool*** - Odstranění souborů programu *libtool* (`.la`).
*   ***emptydirs*** - Odstranění prázdných adresářů z výsledného balíčku.
*   ***zipman*** - Komprese *man* a *info* stránek programem *gzip*.
*   ***ccache*** - Povoluje použití `ccache` v průběhu sestavování balíčku. Více se užívá obrácená varianta této volby `!ccache` - většinou pro balíčky, které mají problém při sestavování s `ccache`.
*   ***distcc*** - Povoluje užítí `distcc` v průběhu sestavování balíčku. Více se užívá obrácená varianta této volby `!distcc`. Tuto volbu většinou používájí balíčky, které mají problémy při sestavování s `distcc`.
*   ***makeflags*** - Umožňuje definovat proměnné pro kompilaci. Více se užívá její znegovaná forma `!makeflags`.
*   ***force*** - Donutí balíček k aktualizaci, a to i v případě, že by to verze balíčku neměla umožňovat. Tato volba se například užívá při změně číslování verzí balíčku nebo když je nutný tzv. downgrade balíčku z důvodu bezpečnosti.

	`install` 

	Představuje jméno skriptu `.install`, který může a nemusí být součástí balíčku. *pacman* pak tento skript spouští při instalaci, odstranění nebo aktualizaci balíčku. Skript pak může obsahovat následující funkce. Každá z funkcí se spouští v jinou dobu.

*   ***pre_install*** - Tato funkce je volána *předtím*, než jsou soubory rozbaleny. Funkci je argumentem předávána nová verze balíčku.
*   ***post_install*** - Tato funkce je volána *po* rozbalení balíčku. V argumentu ji je předáváno číslo nové verze balíčku.
*   ***pre_upgrade*** - Tato funkce je volána *předtím*, než jsou soubory rozbaleny. Jsou ji předávány dva argumenty v tomto pořadí: nová verze balíčku, stará verze balíčku.
*   ***post_upgrade*** - Tato funkce je volána *po* rozbalení balíčku. Jsou ji předávány dva argumenty v tomto pořadí: nová verze balíčku, stará verze balíčku.
*   ***pre_remove*** - Funkce, která je volána předtím, než jsou všechny soubory odstraněny. Je jí předáván jeden parametr - stará verze balíčku.
*   ***post_remove*** - Funkce, která je volána po odstranění souborů. Je jí předáván jeden argument - stará verze balíčku.

**Tip:** Prototyp souboru `.install` můžete naleznout zde: `/usr/share/pacman/proto.install`.

	`source` 

	Je pole souborů, které jsou potřeba pro sestavení balíčku. Musí obsahovat umístění zdrojových kódů programu. Umístění tedy představuje adresa URL na HTTP nebo FTP. Můžete zde využít již definované proměnné `pkgname` a `pkgver`. Například takto: `source=(http://example.com/$pkgname-$pkgver.tar.gz)`.

**Note:** Pokud k balíčku potřebujete přidat nějaké soubory, které není možno stáhnout přímo z internetu (například patche apod.), stačí je jednoduše přidat do stejného adresáře jako váš `PKGBUILD` a název souboru přidat do tohoto pole. Předtím, než začne samotný proces sestavování balíčku, jsou všechny odkazované soubory staženy a zkontrolovány. Pokud nastane nějaká chyba, `makepkg` nebude dál pokračovat a skončí s chybou.

**Note:** Můžete také specifikovat jiné jméno stahovaného souboru. Například pokud má stahovaný soubor nehodící se jméno (například obsahuje parametry GET). Vše uděláte následovně: <jmeno_souboru>::<uri_souboru>, vše bez znaků '<' a '>'.

	`noextract` 

	Pole souborů, které jsou obsaženy v poli `source`, ale nemají být extraktovány. Toto pole se většinou používá pro archívy typu zip, které nemohou být rozbaleny programem *bsdtar*. V těchto situacích by se měl přidat program *unzip* do pole `makedepends` a první řádka funkce `build()` by měla obsahovat:

```
cd $srcdir/$pkgname-$pkgver
unzip [source].zip

```

	`md5sums` 

	Je pole kontrolních součtů typu MD5\. Jedná se o kontrolní součty souborů obsažených v poli `source`. Při sestavování balíčku se pak automaticky spočítá kontrolní součet souborů obsažených v poli `source` a porovná se se součtama z tohoto pole. Toto pole lze jednoduše vygenerovat pomocí příkazu `makepkg -g` spuštěném v adresáři, který obsahuje daný soubor `PKGBUILD`.

	`sha1sums` 

	Je pole SHA-1 160-bitových kontrolních součtů. Je to alternativa k md5 součtům, které jsou zmíněny výše. Pro to, aby jste je mohli používat musíte mít zaplou volbu INTEGRITY_CHECK ve vašem `makepkg.conf`. Pro více informací koukněte do man makepkg.conf.

	`sha256sums, sha384sums, sha512sums` 

	Pole kontrolních součtů typu SHA-2 o šířce 256, 384 a 512 bitů. Jsou alternativou pro kontrolní součty typu md5, které jsou popsané výše. Pro zapnutí generování těchto kontrolních součtů se ujistěte, že máte správně nastavenou volbu INTEGRITY_CHECK ve vašem `makepkg.conf`. Mrkněte také do man makepkg.conf.

Běžně se ve skriptu `PKGBUILD` zachovává stejné pořádí proměnných jako výše. Nicméně to není povinné. Jediným požadavkem je dodržení přesné [Bash](https://en.wikipedia.org/wiki/Bash "wikipedia:Bash") syntaxe.

## Externí odkazy

*   [PKGBUILD(5) Manuálová stránka](https://www.archlinux.org/pacman/PKGBUILD.5.html)
*   [Balíčkovací systém Archlinuxu na Root.cz](http://www.root.cz/clanky/arch-linux-balickovaci-system/)
*   [Příklad skriptu PKGBUILD](http://seberm.pastebin.com/r7q5VuYM)
*   [Příklad skriptu .install](http://seberm.pastebin.com/gP0tBqvs)