Tato stránka srovnává Arch Linux s ostatními populárními distribucemi GNU/Linuxu a UNIX-like operačními systémy. Následující přehled obsahuje stručné popisy, které vám mohou pomoci rozhodnout, jestli Arch Linux bude vyhovovat vašim potřebám. Mějte prosím na paměti, že nejlepším způsobem jak porovnat Arch s ostatními distribucemi je, že si ho nainstalujete a vyzkoušíte sami.

## Contents

*   [1 Source-based distribuce](#Source-based_distribuce)
    *   [1.1 Gentoo Linux](#Gentoo_Linux)
    *   [1.2 Sorcerer/Lunar-Linux/Source Mage](#Sorcerer.2FLunar-Linux.2FSource_Mage)
*   [2 Minimalistické distribuce](#Minimalistick.C3.A9_distribuce)
    *   [2.1 LFS](#LFS)
    *   [2.2 CRUX](#CRUX)
    *   [2.3 Slackware](#Slackware)
*   [3 Všeobecné distribuce](#V.C5.A1eobecn.C3.A9_distribuce)
    *   [3.1 Debian GNU/Linux](#Debian_GNU.2FLinux)
    *   [3.2 Fedora](#Fedora)
    *   [3.3 Frugalware](#Frugalware)
*   [4 Distribuce pro začátečníky](#Distribuce_pro_za.C4.8D.C3.A1te.C4.8Dn.C3.ADky)
    *   [4.1 Ubuntu](#Ubuntu)
    *   [4.2 Mandriva](#Mandriva)
    *   [4.3 openSUSE](#openSUSE)
    *   [4.4 PCLinuxOS](#PCLinuxOS)
*   [5 BSD systémy](#BSD_syst.C3.A9my)
    *   [5.1 FreeBSD](#FreeBSD)
    *   [5.2 NetBSD](#NetBSD)
    *   [5.3 OpenBSD](#OpenBSD)
*   [6 Externí odkazy](#Extern.C3.AD_odkazy)

## Source-based distribuce

*Source-based* distribuce jsou velmi přizpůsobitelné, dávají uživatelům možnost kontroly a kompilace kompletního operačního systému i aplikací pro konkrétní architekturu a způsob použití, nevýhodou je však časová náročnost kompilace. Arch kompiluje všechny balíčky pro architektury i686 a x86-64, čímž poskytuje potenciálně vyšší výkon oproti distribucím poskytujícím binární balíčky pro architektury i386/i486/i586.

### Gentoo Linux

Arch Linux i Gentoo Linux používají rolling-release aktualizační model, čímž poskytují aktuální balíčky krátce po jejich oficiálním vydání. V Gentoo jsou balíčky a základní systém kompilovány přímo ze zdrojového kódu podle uživatelských 'USE flags'. Arch poskytuje *ports-like* systém pro kompilaci balíčků ze zdrojového kódu, ačkoli základní systém Archu je navržen pro instalaci z předkompilovaných balíčků pro architektury i686/x86-64\. Z tohoto důvodu je všeobecně konfigurace a aktualizace Archu rychlejší, zatímco Gentoo je systematičtěji přizpůsobitelný. Arch podporuje architektury i686 a x86-64, Gentoo oficiálně podporuje architektury x86, PPC, SPARC, Alpha, AMD64, ARM, MIPS, HP/PA, S/390, sh, a Itanium. Protože Gentoo i Arch poskytují v základu pouze holý systém, oba systémy jsou považovány za velmi přizpůsobitelné. Uživatelé Gentoo se v Archu v mnoha ohledech cítí pohodlně.

### Sorcerer/Lunar-Linux/Source Mage

Sorcerer/Lunar-Linux/Source Mage (SLS) jsou *source-based* distribuce, původně úzce spjaté. SLS distribuce používají na kompilaci balíčků poměrně jednoduché skripty a používají globální konfigurační soubor na konfiguraci kompilačního procesu, což se velmi podobá [Arch Build System](/index.php/Arch_Build_System_(%C4%8Cesky) "Arch Build System (Česky)"). Nástroje SLS provádí úplnou kontrolu závislostí, včetně správy volitelných funkcí, sledování balíčků, jejich odebírání a aktualizování. Pro SLS nejsou žádné binární balíčky, ačkoli je zde možnost jednoduše se vrátit k dříve nainstalovaným balíčkům.

Instalační proces zahrnuje konfiguraci jednoduchého základního systému z příkazové řádky a ncurses menu a poté volitelnou rekompilaci základního systému. Stejně jako v Archu zde není žádné výchozí desktopové prostředí a Xorg není v základní instalaci. Je dostupných několik alternativ X serveru (X.Org 6.8 nebo 7, XFree86).

SLS má velmi komplikovanou historii. Asi nejlepší shrnutí naleznete na [SourceMage wiki](http://wiki.sourcemage.org/SourceMage/History).

## Minimalistické distribuce

Minimalistické distribuce jsou v několika ohledech srovnatelné s Archem. Všechny jsou z technického hlediska považovány za *jednoduché*.

### LFS

LFS (Linux From Scratch) existuje jednoduše jako dokumentace, která obsahuje informace o tom, jak získat zdrojový kód minimálního množství základních balíčků pro funční GNU/Linux systém a jak je manuálně od nuly kompilovat, záplatovat a konfigurovat. LFS je tak minimalistický, jak to jen jde, a nabízí excelentní vzdělávací proces výstavby a přizpůsobování základního systému. Arch poskytuje v základu přesně tyto balíčky, plus [systemd](/index.php/Systemd "Systemd"), několik extra nástrojů a mocného správce balíčků [pacman](/index.php/Pacman_(%C4%8Cesky) "Pacman (Česky)"), už v podobě předkompilovaných balíčků pro architektury i686/x86-64\. LFS neposkytuje žádné online repozitáře; zdrojový kód je třeba manuálně stáhnout, zkompilovat a nainstalovat pomocí `make`. (Existuje několik manuálních metod správy balíčků, jsou zmíněny v [LFS Hints](http://www.linuxfromscratch.org/hints/)). Kromě minimálního systému poskytují vývojáři a uživatelé Archu několik tisíc binárních balíčků, které je možno jednoduše nainstalovat pacmanem, a [PKGBUILD](/index.php/PKGBUILD_(%C4%8Cesky) "PKGBUILD (Česky)") skripty pro [Arch Build System](/index.php/Arch_Build_System_(%C4%8Cesky) "Arch Build System (Česky)"). Arch také poskytuje nástroj [makepkg](/index.php/Makepkg "Makepkg") pro jednoduché sestavení `.pkg.tar.xz` balíčků. Judd Vinet postavil Arch od nuly (*from scratch*), a potom napsal pacmana v jazyce C. Archu se někdy vtipně říkalo "Linux s pěkným správcem balíčků".

### CRUX

Před tím než Judd Vinet vytvořil Arch, používal právě CRUX. Jedná se o minimalistickou distribuci, kterou vytvořil Per Lidén. Původně inspirován myšlenkami společnými pro CRUX a BSD, Arch byl postaven od nuly a potom byl v jazyce C napsán [pacman](/index.php/Pacman_(%C4%8Cesky) "Pacman (Česky)"). Arch a CRUX sdílí několik vůdčích principů, např. oba systémy jsou optimalizovány pro konkrétní architektury, jsou minimalistické a drží se KISS principu. Oba mají *ports-like* systém a stejně jako BSD systémy poskytují minimální základní prostředí, které uživatel dále rozšiřuje. Arch má pacmana, který se stará o správu binárních balíčků a elegantně spolupracuje s [Arch Build System](/index.php/Arch_Build_System_(%C4%8Cesky) "Arch Build System (Česky)"). CRUX používá komunitní systém zvaný prt-get, který v kombinaci s vlastním *ports-like* systémem zvládá správu závislostí, ale sestavuje balíčky ze zdrojového kódu (ačkoli základní instalace CRUXu je binární). Arch oficiálně podporuje architektury i686 a x86-64, kdežto CRUX oficiálně nabízí pouze x86-64.

Arch používá *rolling-release* model, nabízí množství binárních balíčků v oficiálních repozitářích a ještě více v [Arch User Repository](/index.php/Arch_User_Repository_(%C4%8Cesky) "Arch User Repository (Česky)"). CRUX má štíhlejší *ports-like* systém a poměrně chudší komunitní repozitář.

### Slackware

*   Slackware i Arch jsou jednoduché distribuce zaměřující se na eleganci a minimalismus.
*   Slackware je známý tím, že poskytuje naprosto čisté *vanilla* balíčky včetně kernelu. Arch typicky záplatuje pouze aby se vyhnul závažnému rozbití balíčků, nebo aby kompilace proběhla v pořádku.
*   Slackware používá init skripty ve stylu BSD, Arch používá [systemd](/index.php/Systemd "Systemd").
*   Arch poskytuje správce balíčků [pacman](/index.php/Pacman_(%C4%8Cesky) "Pacman (Česky)"), který na rozdíl od standardních nástrojů Slackware poskytuje automatickou správu závislostí a umožňuje automatizovanější aktualizace systému. Slackware typicky preferuje svou metodu manuální správy závislostí.
*   Arch je *rolling-release*. Slackware je považován za konzervativnější, preferuje otestované stabilní balíčky. Arch je v tomto ohledu více *bleeding-edge*.
*   Arch poskytuje v oficiálních repozitářích tisíce binárních balíčků, repozitáře Slackware jsou chudší.
*   Arch nabízí *ports-like* systém [Arch Build System](/index.php/Arch_Build_System_(%C4%8Cesky) "Arch Build System (Česky)") a [Arch User Repository](/index.php/Arch_User_Repository_(%C4%8Cesky) "Arch User Repository (Česky)"), velmi rozsáhlou kolekci [PKGBUILD](/index.php/PKGBUILD_(%C4%8Cesky) "PKGBUILD (Česky)") skriptů, do které přispívají uživatelé. Slackware nabízí podobný, avšak štíhlejší systém na [slackbuilds.org](http://www.slackbuilds.org), který je polooficiálním repozitářem skriptů Slackbuilds, které jsou analogií skriptů PKGBUILD. Uživatelé Slackware se v Archu v mnoha ohledech cítí pohodlně.

## Všeobecné distribuce

Tyto distribuce mají mnoho výhod a silných stránek, mohou být použity pro mnoho účelů.

### Debian GNU/Linux

*   Debian je největší linuxovou distribucí s větší komunitou, nabízí stabilní, testovací a nestabilní větve, repozitáře obsahují přes 30000 velmi kvalitních binárních balíčků. Množství dostupných binárních balíčků Archu je menší, ale pokud započítáme AUR, množství už jsou srovnatelná.
*   Debian má silně podporuje svobodný software, ale jeho repozitáře stále obsahují také nesvobodný software. Arch je shovívavější a přístupnější ohledně nesvobodných balíčků podle definice GNU, čímž nechává volbu na uživateli.
*   Debian se soustředí více na stabilitu a přísné testování. Arch se drží filozofie jednoduchosti, minimalismu a nabízení *bleeding-edge* software. Balíčky Archu jsou aktuálnější než stabilní a testovací balíčky Debianu, jsou srovnatelné s balíčky z nestabilní větve Debianu.
*   Debian i Arch nabízí kvalitní systémy správy balíčků.
*   Arch je *rolling-release*, kdežto stabilní větev Debianu je uvolňována se zmraženými (*frozen*) balíčky. Nestabilní větev Debianu je také *rolling-release*.
*   Debian je dostupný pro mnoho architektur, včetně alpha, arm, hppa, i386, x86_64, ia64, m68k, mips, mipsel, powerpc, s390 a sparc, kdežto Arch oficiálně podporuje pouze i686 a x86-64 (komunita podporuje i arm, např. pro Raspberry Pi).
*   Arch nabízí *ports-like* systém, který poskytuje vhodnější podporu pro sestavování vlastních balíčků z vnějších zdrojů. Debian nenabízí *ports-like* systém, spoléhá na své obrovské binární repozitáře.
*   Instalace Archu nabízí pouze minimální základní systém, který lze dále transparentně konfigurovat, kdežto metody Debianu volí přístup automatizovanější konfigurace a několik alternativních metod instalace.
*   Debian používá v základu SysVinit, ačkoli systemd a upstart jsou uživatelům také dostupné. Arch používá primárně [systemd](/index.php/Systemd "Systemd") kvůli celkově lepšímu výkonu.
*   Arch udržuje záplatování na minimu, čímž se vyhýbá problémům o kterých vývojáři aplikací nemohou vědět, kdežto Debian své balíčky záplatuje rozsáhleji pro širší uživatelskou základnu.

### Fedora

*   Fedora je vyvíjena komunitou, ale je zajištěna firmou Red Hat; často je prezentována jako jeho *bleeding-edge* testovací prostředí; balíčky a projekty Fedory migrují do Red Hat Enterprise Linuxu a některé jsou později přijaty i ostatními distribucemi. Arch je také všeobecně pokládán za *bleeding-edge*, ale na rozdíl od Fedory však používá *rolling-release* model aktualizací a není testovacím prostředím pro jinou distribuci.
*   Fedora používá RPM formát balíčků a jejich správce YUM, také jsou dostupné oficiální grafické front-endy. Arch používá správce balíčků [pacman](/index.php/Pacman_(%C4%8Cesky) "Pacman (Česky)"), balíčky jsou v `.tar.xz` formátu, neposkytuje oficiální grafické front-endy.
*   Fedora kvůli své oddanosti svobodnému software odmítá do svých repozitářů přidat podporu pro MP3 a další nesvobodný software, ale repozitáře třetích stran pro takové balíčky existují. Arch je shovívavější a přístupnější ohledně nesvobodných balíčků podle definice GNU, čímž nechává volbu na uživateli.
*   Fedora nabízí mnoho instalačních voleb včetně grafického instalátoru a možnosti nainstalovat pouze minimální systém. Alternativní verze Fedory nabízí různá desktopová prostředí, každé se skromnou kolekcí výchozích aplikací. Naproti tomu Arch nabízí pouze několik skriptů, které mají usnadnit proces instalace minimálního systému.
*   Fedora má plánovaný vývojový cyklus, ale oficiálně pomocí nástroje FedUp podporuje aktualizace z jedné verze Fedory na druhou. Arch má *rolling-release* model.
*   **The Arch Way** se zaměřuje na jednoduchost, eleganci, odlehčenost a silnou roli uživatele, kdežto základními hodnotami Fedory jsou svobodný software, komunitní vývoj a *bleeding-edge* systémová inovace.
*   Arch poskytuje *ports-like* systém, kdežto Fedora ne.
*   **Arch i Fedora se zaměřují na zkušené uživatele a vývojáře.** Obě distribuce silně podporují své uživatele k přispívání do vývoje projektu.
*   Fedora si získala respekt komunity integrací SELinux, balíčků kompilovaných pomocí GCJ (aby se zbavila závislosti na JRE firmy Sun) a podílením se na vývojí aplikací; vývojáři Red Hatu a Fedory přispívají k vývoji linuxového jádra procentuálně více než jakýkoliv jiný projekt.
*   Arch poskytuje wiki, která je běžně označována za nejpodrobnější a nejvšeobecnější dokumentaci mezi všemi linuxovými distribucemi. Wiki Fedory je používána hlavně pro rychlou výměnu informací mezi vývojáři, testery a uživateli. Na rozdíl od ArchWiki není míněna jako zdroj informací pro koncové uživatele. Wiki Fedory se podobá shromaždišti chyb a problémů.

### Frugalware

*   Arch je orientovaný na příkazový řádek.
*   Frugalware ve výchozím stavu nepodporuje souborový systém JFS.
*   Arch i Frugalware jsou optimalizovány pro architekturu i686.
*   Arch může být nainstalován nejprve jako minimální prostředí, které je poté rozšiřováno podle přání a potřeb uživatele. Frugalware je instalován z DVD, které obsahuje výchozí sadu aplikací a desktopových prostředí.
*   Frugalware má plánovaný vývojový cyklus. Arch je zaměřen na jednoduchost, minimalismus, správnost kódu a *bleeding-edge* balíčky s *rolling-release* modelem.

## Distribuce pro začátečníky

Tyto distribuce jsou někdy označovány jako *pro nováčky*, mají mnoho společného, ale Arch je dost odlišný. Arch může být lepší volbou, pokud se chcete naučit něco o GNU/Linuxu tím, že si z minimálního základu sestavíte systém přesně podle svých přání a potřeb. Konkrétní rozdíly jsou popsány níže.

### Ubuntu

*   Ubuntu je velmi populární distribuce založená na Debianu a komerčně podporovaná firmou Canonical, kdežto Arch je nezávisle vyvíjená distribuce postavená od nuly.
*   Oba projekty mají jiné cíle a jinou cílovou skupinu uživatelů. Arch je navržen pro uživatele toužící po *udělej si sám* přístupu, Ubuntu poskytuje automaticky konfigurovaný systém, který se snaží být více uživatelsky přívětivý. Arch je prezentován jako od základů mnohom minimalističtější systém, který silně spoléhá na schopnosti uživatele. Všeobecně vývojáři a šťouralové budou mít pravděpodobně Arch raději než Ubuntu, ačkoli mnoho Archistů začínalo s Ubuntu a později přešli k Archu.
*   Současný vývoj Ubuntu se silně soustředí na trh se zařízeními s dotykovým displejem, kdežto vývoj Archu se všeobecně soustředí na uživatele (z ang. *user-centric*) a podporuje komunitu ke spolupráci na vytváření vlastních řešení.
*   Ubuntu vydává nové verze každých 6 měsícu, kdežto arch má *rolling-release* model aktualizací a každý měsíc vydává nový snapshot instalačního média.
*   Arch nabízí *ports-like* balíčkovací systém, kdežto Ubuntu ne.
*   Komunity obou distribucí se také liší. Komunita Archu je mnohem menší a je silně povzbuzována k přispívání do distribuce. Naopak komunita Ubuntu je relativně velká a proto může tolerovat mnohem menší procento nepřispívajících uživatelů.

### Mandriva

Mandriva Linux (dříve Mandrake Linux) byla vytvořena v roce 1998 s cílem udělat GNU/Linux jednoduše použitelným pro každého. Je založena na RPM balíčcích a používá správce balíčků urpmi. Arch se drží mnohem jednoduššího přístupu, spoléhá na manuální konfiguraci a cílenou skupinou jsou pokročilí uživatelé.

### openSUSE

openSUSE je vystaveno kolem formátu balíčků RPM a oblíbeného grafického konfiguračního nástroje YaST2, který vyhovuje potřebám naprosté většiny uživatelů, zvládá taky správu balíčků. Arch nenabízí podobný konfigurační systém, protože si podobná myšlenka protiřečí s [The Arch Way](/index.php/The_Arch_Way_(%C4%8Cesky) "The Arch Way (Česky)"). openSUSE je proto považován za vhodnější pro méně zkušené uživatele nebo pro ty, kteří chtějí grafické prostředí, automatickou konfiguraci a očekávanou funkčnost přímo po instalaci aplikace.

### PCLinuxOS

*   PCLinuxOS je populární distribuce vycházející z Mandrivy a poskytující kompletní desktopové prostředí, které se snaží být uživatelsky přívětivé a je popisováno jako *jednoduché*, ačkoli definice jednoduchosti je zde dost odlišná od definice v [The Arch Way](/index.php/The_Arch_Way_(%C4%8Cesky) "The Arch Way (Česky)"). Arch je navržen jako jednoduchý základní systém, který je dále přizpůsobován a je cílen na zkušené uživatele.
*   PCLOS používá správce balíčků apt a RPM formát balíčků. Arch používá vlastního nezávisle vyvíjeného správce [pacman](/index.php/Pacman_(%C4%8Cesky) "Pacman (Česky)") a `.pkg.tar.xz` balíčky.
*   PCLOS je zaměřen na grafické prostředí, poskytuje grafické konfigurační nástroje a front-end pro správce balíčků Synaptic, a tvrdí, že velmi málo závisí na příkazovém řádku. Arch je orientován na příkazový řádek a navrhnul jednodušší přístupy ke konfiguraci, správě a údržbě systému.
*   PCLOS doporučuje 256MB RAM jako součást svých minimálních systémových požadavků. Arch je více odlehčený, může běžet na systémech s mnohem menší pamětí, vyžaduje pouze 64MB RAM pro základní instalaci pro i686 architekturu a na modernějších systémech poběží perfektně.

## BSD systémy

BSD systémy mají společný původ na Kalifornské univerzitě v Berkely, jsou produktem snahy vytvořit svobodný `UNIX` systém. Nejedná se o distribuce GNU/Linuxu, ale o `UNIX`-like operační systémy. Proto ačkoli Arch a BSD systémy sdílí koncepty pevného základu a *ports-like* systému, není zde žádná souvislost z hlediska zdrojového kódu, možná s vyjímkou `vi`, protože `vi` v Archu je originální BSD `vi` (většina BSD systémů už nepoužívá originální BSD `vi`). BSD systémy byly odvozeny z originálního `UNIX` kódu firmy AT&T a mají tedy pravé `UNIX` dědictví. Pokud se chcete dozvědět více informací o variantách BSD, navštivte jejich stránky.

### FreeBSD

*   Arch i [FreeBSD](http://www.freebsd.org/about.html) nabízí software, který lze získat ve formě binárního balíčku nebo pomocí *ports-like* systémů.
*   Stejně jako ostatní BSD systémy je i FreeBSD vyvíjen jako systém navržený jako celek, každá aplikace je portována na FreeBSD a je testováno, jestli v systému funguje správně. Naproti tomu distribuce GNU/Linuxu, kterou je i Arch, existují jako slepeniny sestavené z mnoha různých zdrojů.
*   Licence FreeBSD všeobecně více ochraňuje *autora* kódu, naproti tomu licence GPL ochraňuje samotný *kód*. Arch je uvolněn pod GPL licencí.
*   Ve FreeBSD jsou stejně jako v Archu ponechána rozhodnutí na uživateli. Tohle je asi nejzajímavější srovnání s Archem, protože jde ruku v ruce s moderností balíčků je to důkaz existence poměrně velké, chytré, aktivní a seriózní komunity.
*   Oba systémy jsou si v mnohém podobné a uživatelé FreeBSD se v Archu budou všeobecně cítit pohodlně.

### NetBSD

*   NetBSD je svobodný, bezpečný a velmi přenosný `UNIX`-like *open-source* operační systém dostupný pro více než 50 platforem, od 64-bit Opteronů a desktopových systémů až po zařízení do ruky a *embedded* systémy. Má čistý návrh a pokročilé funkce z něj dělají výborné produkční i vývojové prostředí, a je podporováno uživateli s kompletním zdrojovým kódem. Mnoho aplikací je lehce dostupných v NetBSD Packages Collection, `pkgsrc`.
*   Arch sice nepodporuje takové množství architektur, ale na i686 poskytuje více aplikací.
*   `pkgsrc` poskytuje NetBSD metodu instalace ze zdrojového kódu podobnou [Arch Build System](/index.php/Arch_Build_System_(%C4%8Cesky) "Arch Build System (Česky)"), ale binární balíčky pro NetBSD jsou také k dispozici prostřednictvím pkg_tools.
*   Arch má mnoho společného s NetBSD: vyžaduje manuální konfiguraci, je minimalistický a odlehčený, poskytuje *ports-like* systém i binární balíčky a má aktivní a seriózní vývojáře a komunitu.

### OpenBSD

Projekt OpenBSD poskytuje svobodný multiplatformní `UNIX`-like operační systém založený na BSD 4.4.

*   OpenBSD se soustředí na přenosnost, standardizaci, správnost kódu, proaktivní bezpečnost a integrovanou kryptografii. Naproti tomu Arch se soustředí více na jednoduchost, eleganci, minimalismus a *bleeding-edge* software. OpenBSD se sám popisuje jako *"snad nejzabezpečenější OS"*.
*   Arch i OpenBSD nabízí v základu malý elegantní systém.
*   Arch i OpenBSD nabízí *ports-like* a balíčkovací systém umožňující snadnou instalaci a správu balíčků, které nejsou součástí základního systému.
*   Na rozdíl od systémů GNU/Linux, jakým je i Arch, většina BSD systémů včetně OpenBSD vyvíjí jádro a uživatelské programy (jako např. `ls`, `cp`, `cat` a `ps`) společně v jednom repozitáři zdrojového kódu.

## Externí odkazy

*   [DistroWatch.com](http://distrowatch.com/)