## Contents

*   [1 Informace od vývojáře tpowa](#Informace_od_v.C3.BDvoj.C3.A1.C5.99e_tpowa)
*   [2 Upgrade balíčků](#Upgrade_bal.C3.AD.C4.8Dk.C5.AF)
    *   [2.1 Nabídky:](#Nab.C3.ADdky:)
    *   [2.2 Update z kde3.4 beta1 na kde 3.4:](#Update_z_kde3.4_beta1_na_kde_3.4:)
    *   [2.3 Kde vzít KDE 3.5:](#Kde_vz.C3.ADt_KDE_3.5:)
*   [3 Známé problémy](#Zn.C3.A1m.C3.A9_probl.C3.A9my)
*   [4 KDEBASE](#KDEBASE)
    *   [4.1 Podpora pro Samba/Windows:](#Podpora_pro_Samba.2FWindows:)
    *   [4.2 Podpora Javy:](#Podpora_Javy:)
    *   [4.3 Podpora tisku:](#Podpora_tisku:)
    *   [4.4 Základní fonty:](#Z.C3.A1kladn.C3.AD_fonty:)
    *   [4.5 Soubor KDM Xserver:](#Soubor_KDM_Xserver:)
    *   [4.6 D-Bus/udev Stuff:](#D-Bus.2Fudev_Stuff:)
    *   [4.7 GPG/SSH Stuff:](#GPG.2FSSH_Stuff:)
    *   [4.8 Kdebindings:](#Kdebindings:)
    *   [4.9 Kdesdk:](#Kdesdk:)
    *   [4.10 Změna nastavení DPI pro KDM:](#Zm.C4.9Bna_nastaven.C3.AD_DPI_pro_KDM:)
*   [5 Chyby](#Chyby)
*   [6 Zajímavé odkazy](#Zaj.C3.ADmav.C3.A9_odkazy)
*   [7 Rozdělování KDE balíčků](#Rozd.C4.9Blov.C3.A1n.C3.AD_KDE_bal.C3.AD.C4.8Dk.C5.AF)
    *   [7.1 Proč balíčky vycházejí před oficiálním vydáním?:](#Pro.C4.8D_bal.C3.AD.C4.8Dky_vych.C3.A1zej.C3.AD_p.C5.99ed_ofici.C3.A1ln.C3.ADm_vyd.C3.A1n.C3.ADm.3F:)

## Informace od vývojáře tpowa

Prosím neměnte dokument aniž by jste mě neinformovali, pošlete mi krátký email ohledně vašich změn. Tento dokument je založen na KDE 3.5.0!

## Upgrade balíčků

Prosím skočte do konzolového módu před upgradem KDE, jelikož by se mohli ztratit ikony ve vašem panelu.

#### Nabídky:

Pokud máte problém s nabídkou, nejprve odinstalujte KDE a teprve poté nainstalujte aktuální.

#### Update z kde3.4 beta1 na kde 3.4:

Prosím neinstalujte kdebase-config. Je nahrazen kde-common.

#### Kde vzít KDE 3.5:

Jsou umístěny v extra repozitáři. Díky za vaši odezvu. Užijte si nové vydání KDE. Přeji příjemnou zábavu a prosím hlašte případné chyby.

Odkaz na diskuzi: [[1]](https://bbs.archlinux.org/viewtopic.php?t=15257)

## Známé problémy

Jesliže máte stále problémy po upgradu, promyslete zda .kde/ nemůže mít vnitřní konflikty, kompatibilita s KDE 3.5 není. Prosím přesunte soubory na bezpečné místo a spusťte s novým .kde/ adresářem ve svém /home.

Pokud máte instalované rozšíření nebo další software pro kde (ne z našich repozitářů), může to být také příčina pádů kde 3.5\. Prosím sestavte je znovu pro kde 3.5 nebo je odinstalujte.

zařízení:/ kioslave je uzpůsobeno pro získání nového sidebaru: prosím smažte svůj /home/$user/.kde/share/apps/konqsidebartng/

kde 3.5 poskytuje nové možnosti pro kcompmgr (kompozitní rozšíření pro xorg), pokud ho povolíte, může vás spadnout X-Server, vemte to na vědomí.

Applet úschovny může způsobit velké logování, buďte si vědomi tohoto problému a zkontrolujte velikost /var/log/. Může to znamenat že vaše usb zařízení má nějakou závadu.

KSim applet padá jednou za čas. Link na KSim chybu: [[2]](http://bugs.kde.org/show_bug.cgi?id=101261)

## KDEBASE

#### Podpora pro Samba/Windows:

```
# pacman -S samba

```

#### Podpora Javy:

```
# pacman -S j2re

```

#### Podpora tisku:

```
# pacman -S <oblibeny_tiskovy_system>

```

Je to překonfigurované pro cups v kcontrol

#### Základní fonty:

Pokud máte problém se základním nastavení fontů, např. se speciálními znaky pro váš jazyk, zkuste nastavit fonty v 'kcontrol' pro podporu vašich znaků.

#### Soubor KDM Xserver:

KDM nepoužívá soubor /opt/kde/share/config/kdm/Xserver, všechno je nyní v /opt/kde/share/config/kdm/kdmrc zkontrolujte soubor kdmrc.default pro nastavení všech parametrů (např. -dpi 100).

#### D-Bus/udev Stuff:

Prosím přidejte 'dbus' do rc.conf seznamu démonů pro plnout podporu medií:/ kioslave.

#### GPG/SSH Stuff:

Pro vypnutí gpg-agent a/nebo ssh-agent v sezeních KDE, editujte '/opt/kde/env/agent-startup.sh' a '/opt/kde/shutdown/agent-shutdown.sh'.

#### Kdebindings:

Kdebindings bylo sestaveno s podporou pro Javu a GTK. Pokud chcete obojí používat proveďte v pacmanu následující příkazy:

```
# pacman -S j2sdk
# pacman -S gtk

```

#### Kdesdk:

Kdesdk bylo sestaveno s podporou pro Subversion. Pokud ho chcete používat proveďte následující příkaz:

```
# pacman -S subversion

```

#### Změna nastavení DPI pro KDM:

Změna nastavení DPI pro KDE může být trochu skličující ale podíváme se, jak to udělat. Hned po bootu musíme otevřít soubor /opt/kde/share/config/kdm/kdmrc a přidat ServerArgsLocal=-dpi 96 do [X-:*-Core] sekce (nebo jaké DPI chcete). Poté ukončíme editaci a restartujeme X (CTRL+ALT+BACKSPACE).

*Pozn.: Pokud nepoužíváte KDE, pak musíte editovat /usr/X11/bin/startx. Najděte řádku pro defaultserverargs. Přidejte "-dpi 96" (nebo jaké chcete) a restartujte X.*

## Chyby

Pokud si myslíte, že jste našli chybu, ověřte jestli to není náhodná chyba nově vytvořeným uživatelem, který vyčistí setup. Pokud to pod novým uživatelem běží bez potíží zkuste přesunou konfigurační soubory do vašeho uživatele.

kde konfigurační soubory jsou často umístěny v: /home/$user/.kde/share/config a app specifikace v: /home/$user/.kde/share/apps

## Zajímavé odkazy

*   [Arch Linux Bug Tracker](https://bugs.archlinux.org)
*   [KDE Homepage](http://www.kde.org)
*   [KDE Bug Tracker](http://bugs.kde.org)
*   [KDE WebSVN](http://websvn.kde.org)
*   [Control X Font DPI](http://process-of-elimination.net/index.php?title=Control_Font_DPI_in_X)

## Rozdělování KDE balíčků

Pacman není navržen pro tvorbu multiple balíčků do jednoho tarballu. A nezapomeňme na spravovatelnost. Neplánuji si rozdělovat balíčky.

Tvorba samostatných KDE balíčků : [zde](/index.php?title=Making_separate_KDE_packages&action=edit&redlink=1 "Making separate KDE packages (page does not exist)")

#### Proč balíčky vycházejí před oficiálním vydáním?:

Lidé vydávají tarbally i týden před oficiálním vydáním aby měli čas provést patřičné změny a úpravy.