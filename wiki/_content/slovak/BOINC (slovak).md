## Contents

*   [1 Čo je BOINC](#.C4.8Co_je_BOINC)
*   [2 Inštalácia BOINC](#In.C5.A1tal.C3.A1cia_BOINC)
    *   [2.1 Súhrn](#S.C3.BAhrn)
    *   [2.2 Inštrukcie](#In.C5.A1trukcie)
*   [3 Používanie BOINC](#Pou.C5.BE.C3.ADvanie_BOINC)
    *   [3.1 BOINC via GUI](#BOINC_via_GUI)
*   [4 Log](#Log)
*   [5 Ako si vybrať správny projekt](#Ako_si_vybra.C5.A5_spr.C3.A1vny_projekt)
    *   [5.1 BOINC na Arch64](#BOINC_na_Arch64)
*   [6 Linky](#Linky)

## Čo je BOINC

Citácia zo stránky BOINC: *"Využíva čas nečinnosti Vášho počítača (Linux, Mac, Windows) na liečenie chorôb, štúdium globálneho otepľovania, objavovanie pulsarov a na veľa iných typov vedeckých výskumov. Je to bezpečné a ľahké."*

Citácia z Wikipédie: *"Berkeley Open Infrastructure for Network Computing (BOINC) je infraštruktúra pre distribuované výpočty. BOINC je založený na myšlienke, že na svete beží väčšina počítačov ako nevyužitých. Moderné operačné systémy dokážu tento nevyužitý výkon spotrebovať, bez toho aby došlo k výraznému spomaleniu aplikácií, ktoré používateľ používa."*

## Inštalácia BOINC

### Súhrn

BOINC je nainštalovaný ako daemon a z bezpečnostných dôvodov bude bežať pod novovytvoreným užívateľom *boinc*. Pridáme sa do skupinu *boinc* a vytvoríme si link na súbor s heslom, a tak budeme môcť využívať GUI na jeho ovládanie.

### Inštrukcie

Inštalácia BOINC cez pacman:

```
# pacman -S boinc

```

BOINC beži ako daemon, aby sa spúšťal pri štarte pridajte ho do riadku DAEMONS v `/etc/rc.conf`

```
DAEMONS=(... **boinc** ...)

```

Pridajte Vášho užívateľa do skupiny *boinc*. Pre dosiahnutie zmien je potrebné sa odhlásiť a prihlásiť.

```
# gpasswd -a username boinc

```

Ak chcete, môžete si jednoducho skontrolovať, či ste v skupine *boinc* nasledujúcim príkazom.

```
$ groups

```

Spustenie damona BOINC

```
# /etc/rc.d/boinc start

```

Sontrolovanie či beží:

```
$ pgrep boinc

```

## Používanie BOINC

### BOINC via GUI

Deafultne je heslo pre pripojenie GUI k daemonovi vytvorené v `/var/lib/boinc/gui_rpc_auth.cfg`. Na zjednodušenie, využite nasledovný postup, v ktorom sa presuniete do svojho domovského priečinku, vytvoríte link na daný súbor a pridelíte mu práva na čítanie pre užívateľov skupiny *boinc*.

```
$ cd
$ ln -s /var/lib/boinc/gui_rpc_auth.cfg gui_rpc_auth.cfg
# chmod 640 gui_rpc_auth.cfg

```

**Tip:** Ak chcete iné heslo, alebo heslo nechcete, môžete editovať `/var/lib/boinc/gui_rpc_auth.cfg`. Potom nezabudnite reštartovať daemona BOINC.
```
# /etc/rc.d/boinc restart

```

Ak sa vám nepáči idea, že tento súbor máte v svojom home adresáry, je tu aj alternatívne riešenie. Boinc Manager bude hľadať čitateľnž súbor `gui_rpc_auth.cfg` v aktuálnom pracovnom adresáry. Ak spravíte súbor čitateľný pre skupinu *boinc* a uistíte sa, že Boinc Manager beží s pracovným adresárom **var/lib/boinc**, client sa bude pripájať k daemon-ovi automaticky.

GUI spustíte príkazom:

```
$ boincmgr

```

BOINC Vás prevedie procesom pripojenia k projektu. Väčšina projektov Vás nechá vytvoriť si konto priamo cez GUI, pri iných si musíte vytvoriť konto na ich webovej stránke (napr. projekt World Community Grid). Samozrejme sa môžete pripojiť k viacerým projektom cez menu *Nástroje -> Attach to project or account manager*.

Ak sa BOINC nespýta na pripojenie k projektu, skontrolujte či ste pripojený k daemon-ovi. Cez menu *Pokročilý -> Vybrať počítač*, zvoľte meno vašeho počítača (zvyčajne localhost) a zadajte heslo. {{Tip|Aby ste sa tomu vyhli, uistite sa, že ste vykonali vyššie spomenuté kroky týkajúce sa `gui_rpc_auth.cfg`.

## Log

Boinc ukladá logy do `/var/lib/boinc/`:

```
/var/lib/boinc/stderrdae.txt
/var/lib/boinc/stdoutdae.txt

```

## Ako si vybrať správny projekt

Projekty majú odlišné minimálne hardware-ové požiadavky a rozličné časy potrebné na výpočet každej WU (work unit). Ak nestihnete dokončiť WU pred deadlinom, bude poslaná niekomu inému. Preto je lepšie pozrieť sa po projekte, ktorý Váš PC bezproblémov zvládne.

Taktiež, ak to je pre Vás dôležité, zistite si, či projekt poskytuje dáta a výsledky ako verejne dostupné.

### BOINC na Arch64

Niektoré projekty majú iba 32bitové aplikácie a niektoré potrebujú pre svoj beh alebo zobrazenie grafiky 32bitové knižnice.

	Na beh WU (napr. Climateprediction)

```
# pacman -S lib32-glibc lib32-glib2

```

	Na zobrazenie grafiky (napr. niektoré projekty WCG, Climateprediction)

```
# pacman -S lib32-pango lib32-libxdamage lib32-libxi lib32-libgl lib32-libjpeg6 lib32-libxmu

```

**Note:** Aby ste mohli inštalovať 32-bitové knižnice, musíte odkomentovať repozitár **multilib** v `/etc/pacman.conf`

## Linky

*   [BOINC homepage](http://boinc.berkeley.edu/)
*   [List of BOINC projects](http://boinc.berkeley.edu/projects.php)
*   [Wikipedia entry](https://en.wikipedia.org/wiki/BOINC "wikipedia:BOINC")
*   [BOINC.sk](http://boinc.sk)