[cpufrequtils](https://www.archlinux.org/packages/?q=cpufrequtils) je set utilít navrhnutý pre _CPU frequency scaling_, technológiu využívanú primárne na notebook-och. Táto technológia umožňuje operačnému systému meniť frekvenciu CPU v závislosti na aktuálnom vyťažení systému.

V spojení s [pm-utils](/index.php/Pm-utils "Pm-utils") poskytuje kompletný power managment.

Tento článok pokrýva inštaláciu a základnú konfiguráciu balíčka `cpufrequtils`.

## Contents

*   [1 Inštalácia](#In.C5.A1tal.C3.A1cia)
*   [2 Konfigurácia](#Konfigur.C3.A1cia)
    *   [2.1 Ovládač frekvencie CPU](#Ovl.C3.A1da.C4.8D_frekvencie_CPU)
        *   [2.1.1 Intel](#Intel)
        *   [2.1.2 AMD](#AMD)
    *   [2.2 Načítanie pri boot-e](#Na.C4.8D.C3.ADtanie_pri_boot-e)
    *   [2.3 Pridelenie práv v Gnome](#Pridelenie_pr.C3.A1v_v_Gnome)
    *   [2.4 Cpufrequtils a Laptop Mode Tools](#Cpufrequtils_a_Laptop_Mode_Tools)
    *   [2.5 Governors](#Governors)
        *   [2.5.1 Zmena prahu ondemand režimu](#Zmena_prahu_ondemand_re.C5.BEimu)
        *   [2.5.2 Interakcia s ACPI](#Interakcia_s_ACPI)
    *   [2.6 Daemon](#Daemon)
*   [3 Možné problémy](#Mo.C5.BEn.C3.A9_probl.C3.A9my)

## Inštalácia

Balíček [cpufrequtils](https://www.archlinux.org/packages/?name=cpufrequtils) je dostupný v repozitáry [extra]:

```
# pacman -S cpufrequtils

```

## Konfigurácia

Konfigurácia zmeny frekvencie CPU pozostáva z 3 častí:

1.  Načítanie správneho ovládača
2.  Načítanie požadovaných tzv. _governors_
3.  Konfigurácia a načítanie daemona.

### Ovládač frekvencie CPU

Aby Vám zmena frekvencie pracovala správne, operačný systém musí poznať limity CPU. Na splnenie tejto požiadavky sa načítavá modul kernelu, ktorý dokáže čítať a riadiť špecifikácie CPU.

Väčšina dnešných notebook-ov a PC môže používať ovládač **`acpi-cpufreq`**. Ďaľšími možnosťami sú ovládače `p4-clockmod`, `powernow-k8` a `speedstep-centrino`. Aby ste videlikompletný zoznam dostupných ovládačov, spustite nasledovný príkaz:

```
$ ls /lib/modules/2.6.??-ARCH/kernel/drivers/cpufreq

```

**Tip:** Pre AMD "K10" CPU ako napr. Phenom X4, použite ovládač `powernow-k8`.

#### Intel

Manuálne načítanie ovládača:

```
# modprobe acpi-cpufreq

```

Ak máte starší procesor Intel, vyššie uvedený príkaz môže vrátiť:

```
FATAL: Error inserting acpi_cpufreq ([...]/acpi-cpufreq.ko): No such device

```

V tomto prípade nahraďte kernel modul `acpi-cpufreq` s `speedstep-centrino`, `p4-clockmod` alebo `speedstep-ich`.

Modul `speedstep-centrino` je ale zastaraný.

V AUR-e sa náchdaza kernel s modulom speedstep-centrino. Je to balíček **`kernel26-pentium-m`**, ktorý nájdete [tu](https://aur.archlinux.org/packages.php?ID=33104).

#### AMD

```
# modprobe powernow-k8

```

### Načítanie pri boot-e

Aby sa driver načítal automaticky pri štarte pridajte vhodný ovládač do riadku MODULES `/etc/rc.conf`. Príklad:

```
MODULES=( **acpi-cpufreq** vboxdrv fuse fglrx iwl3945 ... )

```

Keď je ovládač načítaný, detailné informácie o CPU môžete zobraziť príkazom:

```
$ cpufreq-info

```

Výstup príkazu by mal byť podobný tomuto:

```
$ cpufreq-info

```

```
 analyzing CPU 0:
  driver: acpi-cpufreq
  CPUs which need to switch frequency at the same time: 0 1
  hardware limits: 1000 MHz - 2.00 GHz
  available frequency steps: 2.00 GHz, 1.67 GHz, 1.33 GHz, 1000 MHz
  available cpufreq governors: ondemand, performance
  current policy: frequency should be within 1000 MHz and 2.00 GHz.
                  The governor "performance" may decide which speed to use
                  within this range.
  current CPU frequency is 2.00 GHz.
 analyzing CPU 1:
  driver: acpi-cpufreq
  CPUs which need to switch frequency at the same time: 0 1
  hardware limits: 1000 MHz - 2.00 GHz
  available frequency steps: 2.00 GHz, 1.67 GHz, 1.33 GHz, 1000 MHz
  available cpufreq governors: ondemand, performance
  current policy: frequency should be within 1000 MHz and 2.00 GHz.
                  The governor "performance" may decide which speed to use
                  within this range.
  current CPU frequency is 2.00 GHz.

```

Pre zobrazenie dostupných _governors_ použijeme:

```
cat /sys/devices/system/cpu/cpu0/cpufreq/scaling_available_governors

```

Monitorovanie frekvenice CPU v reálnom čase si zabezpečíme pomocou:

```
watch grep \"cpu MHz\" /proc/cpuinfo

```

### Pridelenie práv v Gnome

Gnome má pekný applet umožňujúci zmenu _governor_ počas behu. Pre jeho použitie bez potreby zadávanie hesla pre root jednoducho vytvorte `/var/lib/polkit-1/localauthority/50-local.d/org.gnome.cpufreqselector.pkla`a vložte do neho nasledújúci text:

```
[org.gnome.cpufreqselector]
Identity=unix-user:USER
Action=org.gnome.cpufreqselector
ResultAny=no
ResultInactive=no
ResultActive=yes
```

Kde slovo USER nahradíte vašim používateľským menom.

### Cpufrequtils a Laptop Mode Tools

Ak používate alebo plánujete používať [Laptop Mode Tools](/index.php/Laptop_Mode_Tools "Laptop Mode Tools") možno ho budete chcieť nechať riadiť aj zmeny frekvencie CPU. V tomto prípade vložte `acpi-cpufreq` do riadku MODULES v `/etc/rc.conf`:

```
MODULES=(**acpi-cpufreq**)

```

A potom v `/etc/laptop-mode/conf.d/cpufreq.conf` definujte _governors_, frekvencie a politiky.

Ak používate `laptop-mode-tools` na riadenie `cpufrequtils`, potom nepotrebujete načítavať iné moduly a daemonov alebo nastavovať _governors_ a interakcie s ACPI. Prosím prečítajte si [Laptop Mode Tools](/index.php/Laptop_Mode_Tools "Laptop Mode Tools"), aby ste sa dozvedeli ako nainštalova a nakonfigurovať `laptop-mode-tools`.

### Governors

Governors môžu byť myslené ako predkonfigurované schémy pre CPU. Tieto _governors_ musia byť načítavané ako moduly kernelu, aby ich programy ako _kpowersave_ alebo _gnome-power-manager_ mohli využívať.

Dostupné _governors_:

	`cpufreq_performance` _(default)_

	CPU beží na maximálnej frekvencii. Režím je zabudovaný do kernelu.

	`cpufreq_ondemand` _(odporúčané)_

	Dynamicky mení frekvencie CPU na základe zaťaženia systému.

	`cpufreq_conservative`

	Podobné `ondemand`, ale viac konzervatívne.

	`cpufreq_powersave`

	CPU beží na minimálnej frekvencii.

	`cpufreq_userspace`

	Manuálne nastavené frekvencie užívateľom.

Načítanie požadovaného režimu sa robí pomocou `modprobe`. Napríklad:

```
# modprobe cpufreq_ondemand
# modprobe cpufreq_userspace

```

Alebo pridajte požadované režimy do riadku MODULES v `/etc/rc.conf` a reštartujte.

```
MODULES=(acpi-cpufreq **cpufreq_ondemand** **cpufreq_powersave**)

```

Manuálne môžete režim zmeniť pomocou príkazu `cpufreq-set` (ako root), ale toto nastavenie nebude uložené po reštarte alebo vypnutí. Napríklad:

```
# cpufreq-set -g ondemand

```

Tento príkaz nastaví režim iba pre prvý procesor. Ak máte viacjadrový alebo viacprocesorový systém, použite prepínač -c. Napr. pre nastavenie režimu pre štvrté jadro (jadrá sa číslujú od nuly):

```
# cpufreq-set -c 3 -g ondemand

```

Pre viac informácii spustite príkaz `cpufreq-set --help` alebo `man cpufreq-set`.

Pre tých, ktorý chcú GUI na zmenu _governors_ alebo frekvencií môžu použiť [trayfreq](/index.php/Trayfreq "Trayfreq").

#### Zmena prahu `ondemand` režimu

Na zmenu toho, kedy sa režim `ondemand`prepne na vyšší stupeň môžete zmeniť `/sys/devices/system/cpu/cpufreq/ondemand/up_threshold`. Na zistenie aktuálnej hodnoty nastavenia zadajte nasledujúci príkaz ako root:

```
# cat /sys/devices/system/cpu/cpufreq/ondemand/up_threshold

```

Navrátená hodnota môže byť napr. `80` (default pri kerneli 2.6.31). To znamený, že režim `ondemand` zvýšši frelvenciu keď jadro CPU dosiahne 80% využitia. Môžeme to zmeniť napr. nasledovne:

```
echo "15" > /sys/devices/system/cpu/cpufreq/ondemand/up_threshold

```

**Note:** Minimálna hodnota musí byť aspoň o 1 vyššia ako je v down_treshold. Zadanie hodnoty pod túto hodnotu vyhodí chybovú hlášku "bash: echo: write error: Invalid argument"

#### Interakcia s ACPI

Používatelia si môžu nastaviť režimy tak, aby sa automaticky prepínali v závislosti na rozličných ACPI eventoch (napr. pripojenie AC adaptéra alebo zatvorenie krytu laptopu). Eventy sú definované v `/etc/acpi/handler.sh`. Ak je balíček [acpid](https://www.archlinux.org/packages/?name=acpid)nainštalovaný, súbor pravdepodobne existuje a je spustiteľný. Napríklad, ak chcete zmeniť režim z `performance` na `conservative` pri odpojení AC adaptéra a zmeniť naspäť pri jeho zapojení zadáte do súboru:

```
/etc/acpi/handler.sh

```

```
[...]

 ac_adapter)
     case "$2" in
         AC*)
             case "$4" in
                 00000000)
                     echo "conservative" >/sys/devices/system/cpu/cpu0/cpufreq/scaling_governor    
                     echo -n $minspeed >$setspeed
                     #/etc/laptop-mode/laptop-mode start
                 ;;
                 00000001)
                     echo "performance" >/sys/devices/system/cpu/cpu0/cpufreq/scaling_governor
                     echo -n $maxspeed >$setspeed
                     #/etc/laptop-mode/laptop-mode stop
                 ;;
             esac
         ;;
         *) logger "ACPI action undefined: $2" ;;
     esac
 ;;

[...]

```

### Daemon

`cpufrequtils` obsahuje daemona, kotrý dovoľuje užívateľom nastaviť požadované režimy a min/max frekvencie pre všetky jadrá počas boot-u a bez potreby ďaľších nástrojov ako napr. _kpowersave_.

Pred spustením daemona editujte ako root `/etc/conf.d/cpufreq` a nastavte požadované hodnoty, napr:

```
/etc/conf.d/cpufreq

```

```
#configuration for cpufreq control

# valid governors:
#  ondemand, performance, powersave,
#  conservative, userspace
governor="ondemand"

# valid suffixes: Hz, kHz (default), MHz, GHz, THz
min_freq="1GHz"
max_freq="2GHz"

```

**Note:** Presné min/max hodnoty môžete zistiť pomocou `cpufreq-info` po načítaní ovládaču (napr. `modprobe acpi-cpufreq`). Tieto hodnoty sú _voliteľné_. Môžete ich vynechať vymazaním alebo zakomentovaním riadkov min/max. Zmeny budú potom automatické.

S požadovanou konfiguráciou následne spustíme daemona ako root pomocu:

```
# /etc/rc.d/cpufreq start

```

Pre automatické spúštanie daemona pri štarte pridajte `cpufreq` do riadku DAEMONS v `/etc/rc.conf`, napríklad:

```
DAEMONS=(syslog-ng networkmanager @alsa @crond @cupsd **@cpufreq**)

```

## Možné problémy

*   Niektoré aplikácie ako napr. [ntop](/index.php/Ntop "Ntop") neodpovedajú dobre na automatické zmeny frekvencie. V tomto prípade to môže viesť k segmentation fault.

*   Niektoré CPU môžu trpieť nízkym výkonom pri režime `ondemand`. Riešením je vypnutie zmien frekvencie alebo zvýšenie alebo zníženie _up_treshold_.

*   Niektoré CPU/BIOS konfigurácie môžu mať problém pri zmenách frekvencie na maximum alebo vo všeobecnosti pri zmenách frekvencie. nanešťastie momentálne existuje iba workaround. Pridajte processor.ignore_ppc=1" do kernel boot a/alebo zmente hodnotu v /sys/module/processor/parameters/ignore_ppc z 0 na 1.