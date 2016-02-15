## Contents

*   [1 Účel](#.C3.9A.C4.8Del)
*   [2 Uživatel a AUR](#U.C5.BEivatel_a_AUR)
    *   [2.1 Sdílení PKGBUILDů v Unsupported](#Sd.C3.ADlen.C3.AD_PKGBUILD.C5.AF_v_Unsupported)
    *   [2.2 [community]](#.5Bcommunity.5D)
    *   [2.3 Hlasování](#Hlasov.C3.A1n.C3.AD)
*   [3 Jak používat AUR](#Jak_pou.C5.BE.C3.ADvat_AUR)
    *   [3.1 Jak na balíček z UNSUPPORTED](#Jak_na_bal.C3.AD.C4.8Dek_z_UNSUPPORTED)
    *   [3.2 Použití fakeroot](#Pou.C5.BEit.C3.AD_fakeroot)
    *   [3.3 Odeslání balíčku do Unsupported](#Odesl.C3.A1n.C3.AD_bal.C3.AD.C4.8Dku_do_Unsupported)
    *   [3.4 Údržba balíčků v Unsupported](#.C3.9Adr.C5.BEba_bal.C3.AD.C4.8Dk.C5.AF_v_Unsupported)
*   [4 AUR-DMS (skripty pro stahování a správu)](#AUR-DMS_.28skripty_pro_stahov.C3.A1n.C3.AD_a_spr.C3.A1vu.29)
    *   [4.1 Seznam AUR-DMS](#Seznam_AUR-DMS)

## Účel

[Arch User Repository (AUR)](/index.php/Arch_User_Repository_(%C4%8Cesky) "Arch User Repository (Česky)") je komunitou spravovaný repozitář pro uživatele Arch Linuxu. Tato stránka ukazuje jak se může normální uživatel k AURu dostat a pracovat s ním.

## Uživatel a AUR

Běžní uživatelé hrají v AURu podstatnou a nezbytnou roli, bez podpory, angažovanosti a přispívání širší komunity uživatelů by AUR nemohl plnit svůj účel. Život balíčku v AURu začíná i končí u uživatele a potřebuje přispívání uživatelů v několika směrech.

### Sdílení PKGBUILDů v Unsupported

Uživatelé mohou sdílet PKGBUILDy přes "Unsupported" oblast AURu. Unsupported neobsahuje žádné binární balíčky, ale umožňuje nahrát PKGBUILD, který si mohou stáhnout ostatní a pomocí něj vytvořit balíček který si nainstalují. Možnost komentování uživately umožňuje "zpětnou vazbu" formou návrhů pro správce PKGBUILDu, na úpravy/vylepšení. Nový "flagging" systém, který bude uveden, dovoluje TU uživatelům označit balíčky, které obsahují nebezpečný kód. Nicméně PKGBUILDy jsou neoficiální, měly by se používat s opatrností a vše je na vlastní nebezpečí.

### [community]

[community] repozitář doplňuje k [extra] a [current] repozitářům nejpopulárnější balíčky z Unsupported, je udržován důvěryhodnými uživateli ( Trusted users). [community], narozdíl od Unsupported, obsahuje binární balíčky, které se dají instalovat přímo přes pacmana, "build" soubory jsou dostupné pomocí [ABS](/index.php/ABS "ABS"). Některé z těchto balíčků mohou přejít do [current] nebo [extra] repozitáře, pokud vývojáři usoudí, že jsou zásadní pro distribuci.

Uživatelé se do AUR [community] repo dostanou přidáním/odkomentováním toho řádku v /etc/pacman.conf:

```
Include = /etc/pacman.d/community

```

Pokud soubor `/etc/pacman.d/community` neexistuje, vytvořte jej, a vložte do něj následující:

```
[community]
Server = ftp://ftp.archlinux.org/community/os/i686/
```

Pro přístup k [community] build souborům editujte `/etc/abs.conf` do této podoby:

 `REPOS=(core extra community)` 

### Hlasování

Jedna z nejsnažších aktivit pro všechny uživatele Archu je brouzdání po AURu, pomocí webového rozhraní a hlasování pro jejich oblíbené balíčky. Kterýkoli balíček může být převzat Trusted userem - důvěryhodným uživatelem pro zahrnutí do [community], a počet hlasů je jedna z věcí, která se při tomto posuzuje - takže hlasujte pro své oblíbence!

## Jak používat AUR

### Jak na balíček z UNSUPPORTED

Instalace balíčku z Unsupported sestává z těchto kroků :

*   vyhledání aplikace v AURu pomocí [vyhledávače](https://aur.archlinux.org/packages.php) (v našem příkladě budeme chtít nainstalovat balíček "foo") a kliknutí na jméno balíčku ve výsledku vyhledávání. Tímto se dostaneme na stránku s informacemi o balíčku. Na levé straně vidíme vedle sebe dva odkazy:

 ` Tarball :: Files ` 

*   Kliknutím na `Tarball` stáhneme nezbytné build soubory na disk. V našem vzorovém případě se soubor jmenuje `foo.tar.gz`.
*   Zkopírujeme `foo.tar.gz` tarball do "build" adresáře, například `/var/abs/local` a rozbalíme jej. Tímto se vytvoří nový adresář, `/var/abs/local/foo` ve kterém jsou všechny soubory, potřebné k vytvoření požadovaného balíčku.
*   **DŮLEŽITÉ**: otevřete nově vytvořený adresář a pečlivě zkontrolujte PKGBUILD a ostatní .install soubory, zda neobsahují nebezpečný kód - pokud máte jakékoli pochybnosti, **nevytvářejte** balíček a pošlete oznámení o problému na fórum nebo mailing list.
*   Pro vytváření balíčků je vhodné využít `fakeroot` (čtěte níže), zdrojový soubor by měl být stažen, zkontrolován a vytvořen pomocí normálního uživatele, to umožní fakeroot.
*   makepkg vytvoří tarball pojmenovaný foo.pkg.tar.gz který se dá normálně instalovat pomocí pacmana, například:

```
 # pacman -U foo.pkg.tar.gz

```

### Použití `fakeroot`

`fakeroot` dává běžnému uživateli nezbytná oprávnení roota, pro vytvoření balíčku, avšak nedovolí modifikaci jiných souborů systému. Pokud se build proces pokusí o modifikaci souborů mimo build rozhraní, dojde k chybě a build selže - to je velmi užitečné pro ověřování kvality/bezpečnosti/integrity PKGBUILDů. Standardně `export USE_FAKEROOT="y"` najdete v /etc/makepkg.conf takže pokud jste nenastavili jinak, je fakeroot již povolený.

### Odeslání balíčku do Unsupported

Po příhlášení do webového rozhraní AURu, může uživatel [odeslat](https://aur.archlinux.org/pkgsubmit.php) tarball (tar.gz) adresáře, se soubory pro vytvoření balíčku. Adresář by tedy měl obsahovat PKGBUILD, nebo nějaký .install soubor, patche, atd. **Rozhodně ne binárky!** Příklad jak takovýto adresář může vypadat najdete v /var/abs.

Když odesíláte balíček, dodržujte následující pravidla:

*   Zkontrolujte [extra], [current], Unsupported, a [community] zda-li už tam balíček není. Pokud ho v jakékoli formě v některých z repozitářů najdete, **neodesílejte jej!** (pokud je stávající balíček poškozen, nebo chybí nějaká vlastnost, zašlete bug-report do [FlySpray](https://bugs.archlinux.org/)).
*   Zkontrolujte pečlivě, zda to co posíláte je správně. Všichni přispívající si musí přečíst a dodržovat [Arch packaging standards](/index.php/Arch_packaging_standards "Arch packaging standards") když píší PKGBUILDy. To je podstatné pro hladký běh a celkovou úspěšnost AURu. Vytvářením špatných PKGBUILDů plýtváte časem uživatelů a žádnou slávu či respekt si takto neuděláte.
*   Balíčky obsahující binárky nebo jsou velice mizerně napsány, jsou mazány bez varování.
*   Pokud jste si balíčkem jakkoli nejistí, odešlete nejdříve PKGBUILD do AUR Mailing List nebo AUR fóra, kde se na něj podívají ostatní, opraví se chyby a může se přidat do AURu.

### Údržba balíčků v Unsupported

*   Kontrolujte komentáře ostatních uživatelů,snažte se zabudovat vylepšení které vám navrhují; učíte se tím nové věci!
*   Prosím po odeslání **nezapomínejte** na váš balíček! Pokud je v Unsupported, je uživatelova práce kontrolovat updaty balíčku a provádět následné úpravy PKGBUILDu.
*   Pokud nechcete pokračovat v udržování balíčku, zřekněte se (disown) balíčku použitím webového rozhraní AURu a/nebo odešlete zprávu do AUR Mailing List.

## AUR-DMS (skripty pro stahování a správu)

### Seznam AUR-DMS

*   [aurbuild](/index.php/Aurbuild "Aurbuild") (Python)
*   aur-install (bash)
*   aur-sync (Perl) - pro stáhnutí všech AUR tarballs
*   aurup (bash) - pro upload balíčku do AURu
*   aurscripts (bash):
    1.  aurcreate - vytvoří čístý balík připravený pro upload do AURu
    2.  aurdownload - stáhnutí a rozbalení balíčku z AURu
    3.  aurupdate - updatování balíčku a md5sum
*   autoaur (bash, závisí na aurscripts, automaticky updatuje všechny vaše balíčky instalované z AURu)
*   qpkg (Python, pracuje taky s ne-AUR-aplikacemi, druhý nejhlasovanější)
*   [yaourt](/index.php/Yaourt "Yaourt") (bash, wrapper pro srcpac s podporou AURu)

Všechny z těchto skriptů najdete v Unsupported.