Související články

*   [AUR User Guidelines (Česky)](/index.php/AUR_User_Guidelines_(%C4%8Cesky) "AUR User Guidelines (Česky)")
*   [AUR Trusted User Guidelines](/index.php/AUR_Trusted_User_Guidelines "AUR Trusted User Guidelines")

## Contents

*   [1 Souhrnně](#Souhrnně)
    *   [1.1 Důležité dokumenty](#Důležité_dokumenty)
*   [2 Začínáme](#Začínáme)
*   [3 Historie](#Historie)
    *   [3.1 Incoming](#Incoming)
    *   [3.2 Trusted User repozitáře](#Trusted_User_repozitáře)
*   [4 Viz též](#Viz_též)
*   [5 FAQ](#FAQ)
    *   [5.1 Běžné otázky](#Běžné_otázky)
        *   [5.1.1 Co je AUR?](#Co_je_AUR?)
        *   [5.1.2 Co je TU?](#Co_je_TU?)
        *   [5.1.3 Jaký je rozdíl mezi Unsupported a Community?](#Jaký_je_rozdíl_mezi_Unsupported_a_Community?)
        *   [5.1.4 Kolik potřebuje PKGBUILD hlasů, aby se dostal do Community?](#Kolik_potřebuje_PKGBUILD_hlasů,_aby_se_dostal_do_Community?)
        *   [5.1.5 Kam se mám podívat, abych zjistil, jak udělat PKGBUILD?](#Kam_se_mám_podívat,_abych_zjistil,_jak_udělat_PKGBUILD?)
    *   [5.2 Běžné problémy](#Běžné_problémy)
        *   [5.2.1 Zkouším udělat pacman -S něco a nejde to, ale vím, že je v Community](#Zkouším_udělat_pacman_-S_něco_a_nejde_to,_ale_vím,_že_je_v_Community)
        *   [5.2.2 Něco je v AUR zastaralé, co mám dělat?](#Něco_je_v_AUR_zastaralé,_co_mám_dělat?)
        *   [5.2.3 Mám PKGBUILD, který bych rád odeslal, může se někdo podívat, jestli v něm nejsou žádné chyby?](#Mám_PKGBUILD,_který_bych_rád_odeslal,_může_se_někdo_podívat,_jestli_v_něm_nejsou_žádné_chyby?)
        *   [5.2.4 Něco se v AUR nezkompiluje, když dám makepkg. Co mám dělat?](#Něco_se_v_AUR_nezkompiluje,_když_dám_makepkg._Co_mám_dělat?)
        *   [5.2.5 Jak zpřístupním balíčky z Unsupported?](#Jak_zpřístupním_balíčky_z_Unsupported?)
        *   [5.2.6 Jak můžu posílat balíčky do AUR bez použití webového rozhraní?](#Jak_můžu_posílat_balíčky_do_AUR_bez_použití_webového_rozhraní?)
*   [6 Externí odkazy](#Externí_odkazy)

## Souhrnně

**Arch Linux User-Community Repository (AUR)** je repozitář pro uživatele Arch Linuxu řízený komunitou. AUR byl od počátku vytvořen k tomu, aby organizoval sdílení PKGBUILDů v širší komunitě a usnadnil začleňování oblíbených balíčků, kterými přispěli uživatelé, do repozitáře [community](#.5Bcommunity.5D).

Je přezdíván rodiště nových balíčků Arch Linuxu -- v AUR uživatelé přispívají svými vlastními balíčky. Komunita AUR hlasuje pro ně nebo proti nim, a jakmile bylo pro balíček dostatečně hlasováno, AUR Trusted User (Důvěryhodný Uživatel) ho přesune do repozitáře [community], odkud je přístupný přes [pacmana](/index.php/Pacman_(%C4%8Cesky) "Pacman (Česky)") a [ABS](/index.php/ABS_-_The_Arch_Build_System_(%C4%8Cesky) "ABS - The Arch Build System (Česky)").

### Důležité dokumenty

Kromě tohoto článku si nezapomeňte přečíst [uživatelského průvodce AUR](/index.php/AUR_-_u%C5%BEivatelsk%C3%BD_pr%C5%AFvodce_(%C4%8Cesky) "AUR - uživatelský průvodce (Česky)"), pokud chcete být uživatel AUR, a [AUR Trusted User Guidelines](/index.php/AUR_Trusted_User_Guidelines "AUR Trusted User Guidelines"), pokud plánujete být Trusted User.

## Začínáme

*   Krátký návod pro instalování balíčků z AUR můžete nalézt [zde](#Jak_na_bal.C3.AD.C4.8Dek_z_UNSUPPORTED). Pro detailní informace o sestavování balíčků z AUR se prosím podívejte na článek o [makepkg](/index.php/Makepkg "Makepkg").
*   [Uživatelský průvodce AUR](/index.php/AUR_-_u%C5%BEivatelsk%C3%BD_pr%C5%AFvodce_(%C4%8Cesky) "AUR - uživatelský průvodce (Česky)") vysvětluje a ukazuje, jak zpřístupnit repozitář [community] v [pacmanu](/index.php/Pacman_(%C4%8Cesky) "Pacman (Česky)") a [ABS](/index.php/ABS_-_The_Arch_Build_System_(%C4%8Cesky) "ABS - The Arch Build System (Česky)").
*   Navštivte [webové rozhraní AUR](https://aur.archlinux.org), abyste se informovali o aktualizacích a událostech. Najdete tam také statistiky a aktualizovaný seznam nejnovějších balíčků dostupných v AUR.
*   Také se podívejte na [otázky a odpovědi](/index.php/AUR_Q_%26_A "AUR Q & A").

## Historie

Následující položky jsou uvedeny jen pro historické účely. Od té doby byly nahrazeny AURem a dále již nejsou dostupné.

### Incoming

Na počátku bylo:

```
[ftp://ftp.archlinux.org/incoming](ftp://ftp.archlinux.org/incoming)

```

a lidé přispívali jednoduše tak, že nahráli [PKGBUILD](/index.php/PKGBUILD "PKGBUILD"), potřebné doplňující soubory a samotný sestavený balíček na server. Balíček zde zůstal tak dlouho, než ho uviděl [správce balíčků](/index.php/Package_Maintainer "Package Maintainer") a adoptoval ho.

### Trusted User repozitáře

Poté se zrodily Trusted User repozitáře. Určitým jednotlivcům v komunitě bylo dovoleno hostovat své vlastní repozitáře, které pak mohl kdokoliv využívat. AUR vznikl na tomto základě s cílem toto učinit jak flexibilnější tak použitelnější. Správcům AUR se ve skutečnosti stále říká TU (Trusted Users).

## Viz též

*   [AUR helpers](/index.php/AUR_helpers "AUR helpers") vám mohou pomoci najít, stáhnout a nainstalovat balíčky z AUR.

## FAQ

### Běžné otázky

#### Co je AUR?

AUR (Arch User Repository) je místo, kam může komunita Arch Linuxu nahrávat [PKGBUILDy](/index.php/Arch_Build_System_(%C4%8Cesky)#Co_je_PKGBUILD_a_co_obsahuje.3F "Arch Build System (Česky)") aplikací, knihoven atd. a sdílet je s celou komunitou. Další uživatelé pak pro své oblíbené balíčky mohou volit, aby se dostaly do repozitáře Community a mohly tak být sdíleny s uživateli Arch Linuxu v binární formě.

#### Co je TU?

[TU (Trusted User)](/index.php/AUR_Trusted_User_Guidelines "AUR Trusted User Guidelines") je osoba, která je zvolena pro to, aby dohlížela na AUR a repozitář Community. Oni jsou ti, kdo dávají PKGBUILDy, které dostanou nejvíce hlasů, do Community, označují PKGBUILDy jako bezpečné a obecně udržují AUR v chodu.

#### Jaký je rozdíl mezi Unsupported a Community?

Unsupported je místo, kam posílají všechny PKGBUILDy uživatelé. Z nich pak musíte sestavit balíčky ručně pomocí <tt>makepkg</tt>. Když PKBUILDy dostanou dostatečné množství hlasů, jdou do repozitáře Community, kde je spravují TU a jelikož jsou to nyní binární balíčky, může být pro jejich instalaci použit pacman.

#### Kolik potřebuje PKGBUILD hlasů, aby se dostal do Community?

Obvykle to dá kolem 25 hlasů, než se něco dostane do Community. Výjimkou je, když je aplikace vyvíjena pro Arch Linux a TU ji chce dát do Community; pak vstoupí do repozitáře dříve.

#### Kam se mám podívat, abych zjistil, jak udělat PKGBUILD?

Nejlepší místo je [zde (anglicky)](/index.php/Creating_packages "Creating packages"). Před vytvářením PKGBUILDu se nezapomeňte podívat do AUR, abyste zbytečně nevytvářeli něco, co již existuje.

### Běžné problémy

#### Zkouším udělat <tt>pacman -S něco</tt> a nejde to, ale vím, že je v Community

Pravděpodobně jste nepovolili Community ve svém souboru /etc/pacman.conf. Jednoduše odkomentujte příslušné řádky.

#### Něco je v AUR zastaralé, co mám dělat?

Začátečníci mohou balíček označit jako "out-of-date" (zastaralý). Pokud zůstane takto označený délší dobu, nejlepší věc je poslat e-mail jeho správci. V případě, že ho chcete udržovat sami a nedostanete od správce žádnou odpověď, můžete poslat e-mail do mailing listu aur-general, aby nějaký TU balíček osiřel.

#### Mám PKGBUILD, který bych rád odeslal, může se někdo podívat, jestli v něm nejsou žádné chyby?

Pokud chcete nechat okomentovat svůj PKGBUILD, pošlete ho na mailing list AUR, kde získáte zpětnou vazbu od TU a ostatních členů AUR. Též můžete získat pomoc od gangu na [IRC kanálu](/index.php/ArchChannel "ArchChannel"), irc.freenode.net #archlinux. Pro zkontrolování svého PKGBUILDu a pkg.tar.gz můžete také použít **namcap**.

#### Něco se v AUR nezkompiluje, když dám makepkg. Co mám dělat?

Nejdříve před kompilací čehokoliv s <tt>makepkg</tt> udělejte <tt>pacman -Syu</tt>, jelikož problém může být v tom, že váš systém není aktuální. Pokud to není ten případ, ohlašte to správci balíčku.

#### Jak zpřístupním balíčky z Unsupported?

[Viz zde.](#Jak_na_bal.C3.AD.C4.8Dek_z_UNSUPPORTED)

#### Jak můžu posílat balíčky do AUR bez použití webového rozhraní?

Můžete použít [aurup](https://aur.archlinux.org/packages.php?ID=5848), což je rozhraní do příkazové řádky.

## Externí odkazy

*   Webové rozhraní AUR: [https://aur.archlinux.org](https://aur.archlinux.org)
*   Mailing list AUR: [https://www.archlinux.org/mailman/listinfo/aur-general](https://www.archlinux.org/mailman/listinfo/aur-general)