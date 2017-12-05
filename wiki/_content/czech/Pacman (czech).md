Související články

*   [Downgrading Packages (Česky)](/index.php/Downgrading_Packages_(%C4%8Cesky) "Downgrading Packages (Česky)")
*   [Pacnew and Pacsave Files (Česky)](/index.php/Pacnew_and_Pacsave_Files_(%C4%8Cesky) "Pacnew and Pacsave Files (Česky)")
*   [pacman GUI Frontends (Česky)](/index.php/Pacman_GUI_Frontends_(%C4%8Cesky) "Pacman GUI Frontends (Česky)")

Správce balíčků **[pacman](https://archlinux.org/pacman/)** je jedním z hlavních rysů Arch Linuxu. Kombinuje jednoduchý binární formát balíčků se sestavovacím systémem jednoduchým na použití (viz [makepkg](/index.php?title=Makepkg_(%C4%8Cesky)&action=edit&redlink=1 "Makepkg (Česky) (page does not exist)") a [Arch Build System](/index.php/Arch_Build_System_(%C4%8Cesky) "Arch Build System (Česky)")). Cílem pacmana je umožnit jednoduchou správu balíčků, ať už pocházejí z oficiálních repozitářů Archu nebo jsou sestaveny samotnými uživateli.

pacman udržuje systém aktuální pomocí synchronizace seznamů balíčků s hlavním serverem. Tento model server/klient též umožňuje stáhnutí/instalaci balíčků jedním jednoduchým příkazem, a to včetně všech vynucených závislostí.

Narozdíl od většiny ostatních správců balíčků je pacman napsán v programovacím jazyku C. Používá formát balíčků .tar.gz a v současnosti migruje k používání formátu .tar.xz (komprese LZMA2).

**Tip:** Balíček [pacman](https://www.archlinux.org/packages/?name=pacman) obsahuje další užitečné nástroje jako [makepkg](/index.php/Makepkg "Makepkg"), **pactree**, **vercmp**, a [checkupdates](/index.php/Checkupdates "Checkupdates"). Pro zobrazení úplného seznamu spusťe `pacman -Qlq pacman | grep bin`

## Contents

*   [1 Konfigurace](#Konfigurace)
    *   [1.1 Hlavní volby](#Hlavn.C3.AD_volby)
        *   [1.1.1 Zamezení upgradu balíčku](#Zamezen.C3.AD_upgradu_bal.C3.AD.C4.8Dku)
        *   [1.1.2 Zamezení upgradu skupiny balíčků](#Zamezen.C3.AD_upgradu_skupiny_bal.C3.AD.C4.8Dk.C5.AF)
    *   [1.2 Repozitáře](#Repozit.C3.A1.C5.99e)
*   [2 Použití](#Pou.C5.BEit.C3.AD)
    *   [2.1 Instalace balíčků](#Instalace_bal.C3.AD.C4.8Dk.C5.AF)
    *   [2.2 Odstraňování balíčků](#Odstra.C5.88ov.C3.A1n.C3.AD_bal.C3.AD.C4.8Dk.C5.AF)
    *   [2.3 Upgrade balíčků](#Upgrade_bal.C3.AD.C4.8Dk.C5.AF)
    *   [2.4 Dotazování databází balíčků](#Dotazov.C3.A1n.C3.AD_datab.C3.A1z.C3.AD_bal.C3.AD.C4.8Dk.C5.AF)
    *   [2.5 Další příkazy](#Dal.C5.A1.C3.AD_p.C5.99.C3.ADkazy)
*   [3 Řešení problémů](#.C5.98e.C5.A1en.C3.AD_probl.C3.A9m.C5.AF)
    *   [3.1 Aktualizace balíčku XYZ mi rozbila systém!](#Aktualizace_bal.C3.AD.C4.8Dku_XYZ_mi_rozbila_syst.C3.A9m.21)
    *   [3.2 Vím o tom, že byl vydán update balíčku ABC, ale pacman mi stále říká, že je můj systém aktuální!](#V.C3.ADm_o_tom.2C_.C5.BEe_byl_vyd.C3.A1n_update_bal.C3.AD.C4.8Dku_ABC.2C_ale_pacman_mi_st.C3.A1le_.C5.99.C3.ADk.C3.A1.2C_.C5.BEe_je_m.C5.AFj_syst.C3.A9m_aktu.C3.A1ln.C3.AD.21)
    *   [3.3 Při aktualizaci dostávám chybu: "file exists in filesystem"!](#P.C5.99i_aktualizaci_dost.C3.A1v.C3.A1m_chybu:_.22file_exists_in_filesystem.22.21)
    *   [3.4 Při instalaci balíčku dostávám chybu: "not found in sync db"](#P.C5.99i_instalaci_bal.C3.AD.C4.8Dku_dost.C3.A1v.C3.A1m_chybu:_.22not_found_in_sync_db.22)
    *   [3.5 pacman opakovaně upgraduje ten samý balíček!](#pacman_opakovan.C4.9B_upgraduje_ten_sam.C3.BD_bal.C3.AD.C4.8Dek.21)
    *   [3.6 pacman během upgradu sletěl!](#pacman_b.C4.9Bhem_upgradu_slet.C4.9Bl.21)
    *   [3.7 Nainstaloval jsem software pomocí make install; tyto soubory nepatří žádnému balíčku!](#Nainstaloval_jsem_software_pomoc.C3.AD_make_install.3B_tyto_soubory_nepat.C5.99.C3.AD_.C5.BE.C3.A1dn.C3.A9mu_bal.C3.AD.C4.8Dku.21)
*   [4 Externí odkazy](#Extern.C3.AD_odkazy)

## Konfigurace

Konfigurace pacmana se nachází v souboru `/etc/pacman.conf`. Ten je místem, kde si uživatel nakonfiguruje program tak, aby pracoval požadovaným způsobem. Zevrubné informace o konfiguračním souboru můžete nalézt v [manuálové stránce pacman.conf (anglicky)](https://www.archlinux.org/pacman/pacman.conf.5.html).

### Hlavní volby

Hlavní volby jsou v sekci `[options]`. Pro informace týkající se toho, co zde můžete udělat, si přečtěte si manuálovou stránku nebo si prohlédněte výchozí `pacman.conf`.

Český překlad bohužel v současnosti neexistuje.

#### Zamezení upgradu balíčku

Abyste zamezili upgradu některého specifického balíčku, uveďte ho v souboru tímto způsobem:

```
IgnorePkg=kernel26

```

Pokud zde potřebujete uvést vícero balíčků, oddělte je mezerami.

#### Zamezení upgradu skupiny balíčků

Stejně jako u jednotlivých balíčků je možné zamezit i upgradu celé skupiny balíčků:

```
IgnoreGroup=gnome

```

### Repozitáře

Tato sekce definuje, které repozitáře mají být použity. Mohou zde být uvedeny přímo nebo zahrnuty z jiného souboru.

Všechny oficiální repozitáře používají shodný soubor se seznamem zrcadel `/etc/pacman.d/mirrorlist`, jenž pro umožnění udržování takovéhoto jednotného seznamu využívá proměnnou "`$repo`". Ta se při každém zahrnutí seznamu zrcadel v určitém repozitáři nahradí za jméno onoho repozitáře.

Následuje příklad pro [oficiální repozitáře](/index.php/Official_repositories_(%C4%8Cesky) "Official repositories (Česky)"), jenž využívá [zrcadla](/index.php?title=Mirrors_(%C4%8Cesky)&action=edit&redlink=1 "Mirrors (Česky) (page does not exist)") ze zmíněného souboru.

```
[core]
# Sem přidejte své upřednostňované servery, budou použity jako první
Include=/etc/pacman.d/mirrorlist

```

```
[extra]
# Sem přidejte své upřednostňované servery, budou použity jako první
Include=/etc/pacman.d/mirrorlist

```

```
[community]
# Sem přidejte své upřednostňované servery, budou použity jako první
Include=/etc/pacman.d/mirrorlist

```

**Note:** Při využívání repozitáře `[testing]` byste si měli dávat pozor. Je v aktivním vývoji a aktualizace mohou způsobit nefunkčnost některých balíčků. Lidem užívající repozitář `[testing]` je doporučeno se přihlásit na anglický mailing list [arch-dev-public](https://mailman.archlinux.org/mailman/listinfo/arch-dev-public), aby měli k dispozici aktuální informace.

## Použití

Pro další ukázky schopností pacmana vizte anglickou [manuálovou stránku pacmana](https://archlinux.org/pacman/pacman.8.html). Ukázky uvedené níže jsou pouze malým vzorkem operací, jež mohou být provedeny.

### Instalace balíčků

Abyste nainstalovali buď jeden balíček nebo seznam balíčků (včetně závislostí), použijte následující příkaz:

```
# pacman -S jméno_prvního_balíčku jméno_druhého_balíčku

```

Někdy je od jednoho balíčku vícero verzí v různých repozitářích (např. extra a testing). Můžete určit, který z nich má být nainstalován:

```
# pacman -S extra/jméno_balíčku
# pacman -S testing/jméno_balíčku

```

**Note:** **Neměňte** během instalace balíčků jejich seznam (např. pomocí `pacman -Sy jméno_balíčku`); může to vést k problémům se závislostmi [[1]](https://bbs.archlinux.org/viewtopic.php?id=89328). Namísto toho proveďte onen [upgrade](#Upgrade_bal.C3.AD.C4.8Dk.C5.AF) **před** instalací jakýchkoliv nových balíčků.

### Odstraňování balíčků

Pro odstranění konkrétního balíčku, ponechávaje všechny jeho závislosti i nadále nainstalované:

```
# pacman -R jméno_balíčku

```

Pro odstranění balíčku a všech jeho závislostí, jež nejsou vyžadovány žádným jiným nainstalovaným balíčkem:

```
# pacman -Rs jméno_balíčku

```

Při odstraňování jistých aplikací pacman ukládá důležité konfigurační soubory s koncovkou `.pacsave`. Abyste smazali i tyto záložní soubory, použijte volbu -n:

```
# pacman -Rn jméno_balíčku
# pacman -Rns jméno_balíčku

```

**Note:** pacman neodstraňuje konfigurační soubory vytvořené samotnou aplikací (například `.tečkové` soubory v domovském adresáři).

### Upgrade balíčků

pacman dokáže zaktualizovat všechny nainstalované balíčky pomocí jednoho jediného příkazu. V závislosti na tom, jak je váš systém aktuální, to může chvíli trvat. Tento příkaz sesynchronizuje databáze repozitářů *a zároveň* zaktualizuje balíčky v systému:

```
# pacman -Syu

```

**Note:** Jsouc distribucí používající postupné aktualizace, nebude vždy aktualizace vašeho Arch Linux systému tak přímočará jako u distribucí s pevnými vydáními. Navíc pacman není balíčkovačem s principem "udělat a zapomenout". Údržba systému s Arch Linuxem má proto sklon mást nováčky (vycházeje ze stále se opakujících diskuzí na fóru). Před pokračováním si, prosím, *pečlivě* pročtěte následující sekci.

pacman je mocný nástroj pro správu balíčků, ale nepokouší se "udělat všechno možné". Pokud vás to mate, přečtěte si článek [o principech Arch Linuxu](/index.php/The_Arch_Way_(%C4%8Cesky) "The Arch Way (Česky)"). Místo toho by měli být uživatelé ostražití a za údržbu vlastního systému brát odpovědnost. Například, když vykonováte aktualizaci systému (`pacman -Syu`), **je nezbytné, abyste si přečetli veškerý výstup z pacmana a používali zdravý rozum.**

Namísto okamžitého aktualizování, jakmile jsou balíčky dostupné, by měli uživatelé mít na paměti, že aktualizace *kritického* balíčku může mít nedozírné následky. To ku příkladu znamená, že není moudré aktualizovat `xorg-server`, máte-li za chvíli předvádět důležitou prezentaci. Raději aktualizujte ve volném čase a buďte připraveni se popást s jakýmkoliv problémem, který kvůli aktualizaci může nastat.

Dále je zárukou navštívení [domovské stránky Arch Linuxu](https://archlinux.org/). Když aktualizace vyžadují zásah uživatele, často se na [https://archlinux.org](https://archlinux.org) objeví příslušné oznámení, které o tom pojednává. Krátce po tom, co se stanou aktualizace dostupné na zrcadlech, se na též fóru obvykle objeví příspěvky popisující ten samý problém a případně poskytující jeho řešení.

Když je prováděna samotná aktualizace, nezapomeňte si pročíst zprávy vypsané pacmanem. Balíčkovači často popisují změny a očekávané problémy, a vedou uživatele k příslušnému zdroji nebo stránce na této wiki. **Vždy si pročtěte veškeré informace ve výstupu pacmana!**

**Tip:** Nezapomeňte, že výstup pacmana je logován do souboru `/var/log/pacman.log`.

### Dotazování databází balíčků

Je-li uvedena volba -Q, pacman se dotazuje lokální databáze balíčků, viz:

```
$ pacman -Q --help

```

Je-li uvedena volba -S, dotazuje se databáze synchronizované se servery, viz:

```
$ pacman -S --help

```

pacman může v databázi vyhledávat určité balíčky, a to jak podle jmen tak podle popisů balíčků:

```
$ pacman -Ss balíček

```

Pro prohledání již nainstalovaných balíčků:

```
$ pacman -Qs balíček

```

Pokud chcete širší informace o některém balíčku:

```
$ pacman -Si balíček

```

A opět pro lokálně nainstalované balíčky:

```
$ pacman -Qi balíček

```

Pro zobrazení seznamu souborů nainstalovaných některým balíčkem:

```
$ pacman -Ql balíček

```

Též se můžete dotázat databáze, zda-li neví, k jakému balíčku patří určitý soubor v souborovém systému.

```
$ pacman -Qo /cesta/k/souboru

```

Pro vypsání všech balíčků, které již nadále nejsou potřebné jako závislosti pro jiné balíčky (sirotci):

```
$ pacman -Qdt

```

### Další příkazy

Stáhnout balíček, ale neinstalovat ho:

```
# pacman -Sw balíček

```

Instalace "lokálního" balíčku, který nepochází z repozitáře:

```
# pacman -U /cesta/k/balíčku/jméno_balíčku-verze.pkg.tar.gz

```

Instalace "vzdáleného" balíčku (taktéž nepocházejícího z repozitáře):

```
# pacman -U [http://www.ukázkovýbalíček/repo/ukázkovýbal.tar.gz](http://www.ukázkovýbalíček/repo/ukázkovýbal.tar.gz)

```

Vyčištění cache balíčků od balíčků, jenž nejsou momentálně nainstalovány (`/var/cache/pacman/pkg`):

```
# pacman -Sc

```

Smazání kompletně celé cache balíčků:

**Warning:** Toto provádějte pouze tehdy, jste-li si jistí, že nebude třeba [downgrade některého balíčku](/index.php/Downgrading_packages_(%C4%8Cesky) "Downgrading packages (Česky)"), protože `pacman -Scc` z cache odstraní skutečně *všechny* balíčky.

```
# pacman -Scc

```

## Řešení problémů

### Aktualizace balíčku XYZ mi rozbila systém!

Arch Linux je distribuce s postupnými aktualizacemi a nejnovějším dostupným softwarem. Aktualizace balíčků jsou dostupné, jakmile jsou považovány za dostatečně stabilní pro obecné použití. Aktualizace nicméně někdy vyžadují zásah uživatele: konfigurační soubory mohou potřebovat aktualizovat, volitelné závislosti se mohou změnit atp.

Nejdůležitější rada pro zapamatování je neaktualizovat systém "naslepo". Vždy si přečtěte seznam balíčků, které mají být zaktualizovány. Všímejte si případů, kdy mají být aktualizovány "kritické" balíčky (`linux`, `xorg-server`, a tak dále). Pokud ano, je obvykle dobrý nápad podívat se na [https://www.archlinux.org](https://www.archlinux.org) po jakýchkoliv novinkách a projít si poslední příspěvky na fóru, abyste předem věděli, zda lidé nemají v důsledku některé aktualizace problémy.

Pokud je očekáváno/známo, že aktualizace balíčku způsobí problémy, balíčkovači (lidé, kteří se starají o balíčky) nezapomenou přidat příslušnou zprávu, kterou pacman zobrazí při aktualizaci daného balíčku. Pokud po aktualizaci máte nějaké potíže, dvakrát si projděte výstup pacmana, jenž naleznete v logu (`/var/log/pacman.log`).

V tomto momentě, **pouze poté, co jste se ujistili, že pacman neposkytuje žádné informace, že nejsou žádné související novinky na [https://www.archlinux.org](https://www.archlinux.org), a že nejsou na fóru žádné příspěvky ohledně dané aktualizace**, byste měli zvážit vyhledání pomoci na fóru, [IRC](/index.php?title=IRC_Channel_(%C4%8Cesky)&action=edit&redlink=1 "IRC Channel (Česky) (page does not exist)") nebo zkuste [downgradovat problematický balíček](/index.php/Downgrading_packages_(%C4%8Cesky) "Downgrading packages (Česky)").

Přečtěte si poslední odstavec znova.

### Vím o tom, že byl vydán update balíčku ABC, ale pacman mi stále říká, že je můj systém aktuální!

Zrcadla pro pacmana nejsou sesynchronizována okamžitě. Může trvat i déle než 24 hodin, než bude aktualizace pro vás dostupná.

Jediné možnosti jsou zde být trpělivý nebo použít jiné zrcadlo.

### Při aktualizaci dostávám chybu: "file exists in filesystem"!

Pozn. stranou: *Převzato z [https://bbs.archlinux.org/viewtopic.php?id=56373](https://bbs.archlinux.org/viewtopic.php?id=56373) od Misfit138.*

```
error: could not prepare transaction
error: failed to commit transaction (conflicting files)
package: /cesta/k/souboru exists in filesystem
Errors occurred, no packages were upgraded.

```

Proč se to stává: pacman zjistil konflikt souborů a shodně s jeho návrhem tyto soubory pro vás nepřepíše. Je to vlastnost návrhu, nikoliv nedostatek.

Je odpovědností uživatele udržovat svůj systém, ne správce balíčků. (Pro dotázání, který balíček, pokud vůbec nějaký, vlastní daný soubor, můžete zavolat `pacman -Qo`.)

Tato záležitost má obvykle triviální řešení. Bezpečný způsob je nejdříve si ověřit, zda-li tento soubor nevlastní jiný balíček (`pacman -Qo /cesta/k/souboru`). Pokud je soubor vlastněn jiným balíčkem, [vyplňte zprávu o bugu](/index.php?title=Reporting_Bug_Guidelines_(%C4%8Cesky)&action=edit&redlink=1 "Reporting Bug Guidelines (Česky) (page does not exist)"). Pokud onen soubor *není* vlastněn jiným balíčkem, přejmenujte soubor, který "existuje v souborovém systému" a vyvolejte příkaz pro aktualizaci znovu. Pokud všechno půjde dobře, ten soubor budete moci odstranit.

### Při instalaci balíčku dostávám chybu: "not found in sync db"

Nejdříve se ujistěte, že balíček skutečně existuje (a pozor na překlepy!). Pokud daný balíček existuje, buď může být váš seznam balíčků zastaralý nebo můžete mít špatně nakonfigurované repozitáře. Zkuste spustit `pacman -Syy` pro vynucenou obnovu všech seznamů balíčků.

### pacman opakovaně upgraduje ten samý balíček!

Toto nastává kvůli duplikovaným záznamům ve `/var/lib/pacman/local/`, např. dvoum instancím `kernel26`. `pacman -Qi` vypíše správnou verzi, ale `pacman -Qu` rozpozná tu starou verzi a proto se pokusí balíček upgradovat.

Řešení: smažte problematický záznam ve `/var/lib/pacman/local/`.

**Note:** pacman verze 3.4 by již měl v případě duplikovaných záznamů vyhlásit chybu. Tato poznámka by tedy měla být zastaralá.

### pacman během upgradu sletěl!

V případě, že pacman během odstraňování balíčků spadne spolu s chybovou hláškou ohledně zápisu do databáze a další pokusy o reinstalaci nebo upgrade balíčků selhávají:

1.  Nabootujte pomocí Live CD Arch Linuxu
2.  Připojte svůj kořenový souborový systém (root)
3.  Aktualizujte databázi balíčků pomocí `pacman -Syy`
4.  Nainstalujte poškozený balíček pomocí `pacman -r /cesta/k/rootu -S balíček`

### Nainstaloval jsem software pomocí `make install`; tyto soubory nepatří žádnému balíčku!

Pokud předáte pacmanovi při instalaci přepínač `-S --force`, přepíše ručně nainstalovaný software. Pokud byl software nainstalován do `/usr/local`, můžete nechat vyhledat soubory, o kterých pacman *má* přehled:

```
# find /usr/local -exec bash -c 'file={}; pacman -Qo "$file" 2>/dev/null' \;

```

Pro vyhledání všech souborů, které *nejsou* sledovány pacmanem:

```
# find / -xdev -exec bash -c 'file={}; [[ "$file" =~ ^/root || \
> "$file" =~ ^/boot/(grub|kernel) || "$file" =~ ^/usr/(include|lib) ]] || \
> pacman -Qo "$file" &>/dev/null || echo "$file"' \;

```

## Externí odkazy

**Manuálové stránky (anglicky)**

*   [libalpm(3)](https://www.archlinux.org/pacman/libalpm.3.html)
*   [makepkg(8)](https://www.archlinux.org/pacman/makepkg.8.html)
*   [makepkg.conf(5)](https://www.archlinux.org/pacman/makepkg.conf.5.html)
*   [pacman(8)](https://www.archlinux.org/pacman/pacman.8.html)
*   [pacman.conf(5)](https://www.archlinux.org/pacman/pacman.conf.5.html)
*   [PKGBUILD(5)](https://www.archlinux.org/pacman/PKGBUILD.5.html)
*   [repo-add(8)](https://www.archlinux.org/pacman/repo-add.8.html)