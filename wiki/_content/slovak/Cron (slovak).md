Cron je plánovač úloh pre GNU/Linux a mnoho iných operačných systémov. Umožňuje automaticky opakovať úlohy spúšťaním daných príkazov v daný čas. Môže byť využitý pre široký rozsah aplikácii, od jednoduchých opakujúcich sa úloh až po zálohy systému.

## Contents

*   [1 Inštalácia](#In.C5.A1tal.C3.A1cia)
*   [2 Úvodná konfigurácia](#.C3.9Avodn.C3.A1_konfigur.C3.A1cia)
    *   [2.1 Používatelia a autoštart](#Pou.C5.BE.C3.ADvatelia_a_auto.C5.A1tart)
    *   [2.2 Chyby úloh](#Chyby_.C3.BAloh)
*   [3 Formát zápisu do crontab](#Form.C3.A1t_z.C3.A1pisu_do_crontab)
*   [4 Základné príkazy](#Z.C3.A1kladn.C3.A9_pr.C3.ADkazy)
*   [5 Príklady](#Pr.C3.ADklady)
*   [6 Viac informácií](#Viac_inform.C3.A1ci.C3.AD)
*   [7 Beh X aplikácií](#Beh_X_aplik.C3.A1ci.C3.AD)
*   [8 Asynchrónne spracovanie úloh](#Asynchr.C3.B3nne_spracovanie_.C3.BAloh)
*   [9 Zdroje](#Zdroje)

## Inštalácia

Existuje mnoho implementácií cron-u, ktoré sú prístupné a môžete si z nich vybrať. [dcron](https://aur.archlinux.org/packages/dcron/) (Dillon's Cron) je dostupný v [core] repozitáry a je inštalovaný ako súčasť **base** skupiny balíčkov.

```
# pacman -S dcron

```

Poprípade si môžete nainštalovať [fcron](https://www.archlinux.org/packages/?name=fcron) z [community] alebo [bcron](https://aur.archlinux.org/packages/bcron/) alebo [vixie-cron](https://aur.archlinux.org/packages/vixie-cron/) z [AUR](/index.php/AUR "AUR"); všetky poskytujú široký rozsah funkcií a možností konfigurácie.

Na [Gentoo Linux Cron Guide](http://www.gentoo.org/doc/en/cron-guide.xml) nájdete viacej porovnaní medzi spomenutými implementáciami.

## Úvodná konfigurácia

#### Používatelia a autoštart

Cron môže pre väčšinu užívateľov pracovať "out-of-box". Ak chcete používať crontab, používatelia musia byť členom určenej skupiny, ale v Arch-u je táto skupina *users*, ktorej členom by mali byť všetci používatelia. Ak by z nejakých dôvodov užívatelia neboli členmi danej skupiny, môžeme ich pridať nasledujúcim príkazom:

```
# gpasswd -a *username* users

```

a mali by bať schopný editácie svojich vlastných crontab-ov.

Aby ste sa uistili, že cron sa bude spúšťať pri štarte systému, pridajte *crond* do riadku DAEMONS v `/etc/rc.conf`.

#### Chyby úloh

Počas spúšťania daných úloh sa môžu vyskytnúť chyby. Keď sa to stane, cron zaregistruje **stderr** výstup úlohy a znaží sa ho poslať defaultne cez **sendmail**. Na log-ovanie týchto správ môžete použiť prepínač **-M** pre cornd a napísať si svoj vlastný skript alebo nainštalovať základný SMTP subsystém

```
# pacman -S esmtp procmail

```

Po inštalácii si vytvorte súbor `/etc/esmtprc` s týmto obsahom:

```
 mda "/usr/bin/procmail -d %T"

```

Otestujte pomocou:

```
$ sendmail user_name < message.txt
$ cat /var/spool/mail/user_name

```

Všetky chybové výstupy budú presmerované do `/var/spool/mail/$user_name` Thats all! All error output of jobs now will be redirected to `/var/spool/mail/$user_name`

## Formát zápisu do crontab

Základný formát je:

```
<minute> <hour> <day_of_month> <month> <day_of_week> <command>

```

*   *minute* nadobúda hodnoty od 0 do 59.
*   *hour* nadobúda hodnoty od 0 do 23.
*   *day_of_month* nadpbúda hodnoty od 1 do 31.
*   *month* nadobúda hodnoty od 1 do 12.
*   *day_of_week* nadobúda hodnoty od 0 do 6, kde 0 je nedeľa.

Viac časom môže byť určených pomocou pomocou čiarky, rozsah (od-do) môže byť určený pomocou pomlčky a hviezdička je použitá ako zástupný znak. Medzery sa používajú na oddelenie jednotlivých polí. Napríklad

```
*0,*5 9-16 * 1-5,9-12 1-5 /home/user/bin/i_love_cron.sh

```

spustí skript `i_love_cron.sh` v 5 minútových intervaloch od 9 do 16 každý pracovný deň v mesiaci okrem letných mesiacov (Jún, Júl, August)

## Základné príkazy

Crontab nemôže byť nikdy editovaný priamo. Používatelia by mali použiť program *crontab* na prácu s ich crontabmi.

Na zobrazenie crontab-ov, môžete použiť:

```
$ crontab -l

```

Na editovanie:

```
$ crontab -e

```

Na zmazanie:

```
$ crontab -d

```

Ak máte uložený crontab a chcete si prepísať svoj starý crontab:

```
$ crontab *uložený_crontab*

```

na prepísanie crontab-u z príkazového riadku ([Wikipedia:stdin](https://en.wikipedia.org/wiki/stdin "wikipedia:stdin")):

```
$ crontab - 

```

Na editovanie cudzieho crontab-u, spustite ako root:

```
# crontab -u *username* -e

```

Tento formát funguje aj na mazanie a pridávanie crontabov.

## Príklady

```
01 * * * * /bin/echo Hello, world!

```

spustí `/bin/echo Hello, world!` vždy prvú minútu každej hodiny, každý deň a každý meisac (12:01, 13:01, 14:01 ...)

Podobne

```
*/5 * * jan mon-fri /bin/echo Hello, world!

```

spustí ten istý príkaz každých 5 minút každý pracovný deň v Januári (12:00, 12:05, 12:10 ...)

```
*0,*5 9-16 * 1-5,9-12 1-5 /home/user/bin/i_love_cron.sh

```

spustí skript `i_love_cron.sh` v 5 minútových intervaloch od 9 do 16 každý pracovný deň v mesiaci okrem letných mesiacov (Jún, Júl, August)

## Viac informácií

Cron daemon využíva konfiguračný súbor známy ako *crontab*. Každý používateľ v systéme môže používať oddelený crontab na plánovanie svojich individuálnych úloh. ROOT-ov crontab je používaný na plánovanie úloh *system-wide*.

Medzi formátmi pre crontab jednotlivých daemonov sú rozdiely. Defaul root crontab pre dcron vyzerá asi takto:

```
/var/spool/cron/root

```

```
# root crontab
# DO NOT EDIT THIS FILE MANUALLY! USE crontab -e INSTEAD

# man 1 crontab for acceptable formats:
#    <minute> <hour> <day> <month> <dow> <tags and command>
#    <@freq> <tags and command>

# SYSTEM DAILY/WEEKLY/... FOLDERS
@hourly         ID=sys-hourly   /usr/sbin/run-cron /etc/cron.hourly
@daily          ID=sys-daily    /usr/sbin/run-cron /etc/cron.daily
@weekly         ID=sys-weekly   /usr/sbin/run-cron /etc/cron.weekly
@monthly        ID=sys-monthly  /usr/sbin/run-cron /etc/cron.monthly

```

Tieto riadky vysvetľujú jeden z možných formátov crontabu, kde:

1.  @perióda
2.  ID=meno úlohy
3.  príkaz

Ďaľším štandartným formátom je:

1.  minute
2.  hour
3.  day
4.  month
5.  day of week
6.  command

Súbory pre crontab sú zvyčajne uložené v `/var/spool/cron/username`. Napríklad crontab pre root nájdeme v `/var/spool/cron/root`.

Pre viac informácií si pozrite crontab [man page](/index.php/Man_page "Man page"), dcron man page [http://www.jimpryor.net/linux/dcron](http://www.jimpryor.net/linux/dcron) tu] a [tu](https://bbs.archlinux.org/viewtopic.php?id=78654&p=1) a príspevky na fóre.

## Beh X aplikácií

Ak by ste chceli spustiť X aplikáciu pomocou cronu, tak pred príkaz vložte:

```
export DISPLAY=:0.0 ;

```

To nastaví premennú DISPLAY na prvý displej, čo je zvyčajne správne, pokiaľ Vám nebeží viac xserverov.

Ak to stále nejde, potom potrebujete použiť xhost aby ste získali kontrolu nad X11:

```
# xhost +si:localuser:$(whoami)

```

Môžete si daný príkaz pridať do ponuky *Aplikácie spúšťané pri štarte* ako:

```
bash -c "xhost +si:localuser:$(whoami)"

```

## Asynchrónne spracovanie úloh

Ak ste vypli počítač, ale chcete, aby sa úloha potom spustila môžete použiť jedno z týchto riešení:

	Dcron 

	Vanilla dcron teraz podporuej asynchrónne spracovanie úloh. Stačí keď vložíte @hourly, @daily, @weekly alebo @monthy s menom úlohy asi takto:

```
@hourly         ID=greatest_ever_job      echo This job is very usefull.

```

	Cronwhip ([AUR](https://aur.archlinux.org/packages.php?ID=21079), [fórum](https://bbs.archlinux.org/viewtopic.php?id=57973))

	Skript na automatické spustenie zmeškaných úloh cronu, pracuje s default dcron-om.

	Anacron ([AUR](https://aur.archlinux.org/packages.php?ID=5196))

	Plná náhrada za dcron, úlohy spracováva asynchrónne.

## Zdroje

*   [Gentoo Linux Cron Guide](https://wiki.gentoo.org/wiki/Cron)