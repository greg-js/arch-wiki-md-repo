Záznam zprovoznění Arch Linuxu na notebooku HP nx7400.

## Contents

*   [1 Konfigurace](#Konfigurace)
*   [2 Instalace:](#Instalace:)
*   [3 Nastavení xorg.conf:](#Nastaven.C3.AD_xorg.conf:)
    *   [3.1 Poznámky:](#Pozn.C3.A1mky:)
*   [4 Procesor](#Procesor)
*   [5 Wi-fi](#Wi-fi)
*   [6 Multimediální klávesy](#Multimedi.C3.A1ln.C3.AD_kl.C3.A1vesy)
*   [7 Firewire](#Firewire)
*   [8 USB](#USB)
*   [9 Eth](#Eth)
*   [10 Modem](#Modem)
*   [11 VGA výstup](#VGA_v.C3.BDstup)
*   [12 Dokovací stanice](#Dokovac.C3.AD_stanice)
*   [13 Výpis bežných teplot](#V.C3.BDpis_be.C5.BEn.C3.BDch_teplot)
*   [14 Poznámky](#Pozn.C3.A1mky)

## Konfigurace

Výrobce: HP
Model: Compaq nx7400
CPU: Intel Celeron M430 1.73 GHz
Video: Intel Corporation Mobile 945GM/GMS/940GML
Audio: Intel Corporation 82801G (ICH7 Family)
Eth: Broadcom Corporation BCM4401-B0 100Base-TX
Wlan: Broadcom Corporation Dell Wireless 1390 WLAN Mini-PCI Card

## Instalace:

Instalace Arch Linux 0.7.2 proběhla bez problémů. Po instalaci nefunkční wi-fi.

## Nastavení xorg.conf:

```
Section "Files"
        FontPath        "/usr/share/fonts/misc"
        FontPath        "/usr/share/fonts/cyrillic"
        FontPath        "/usr/share/fonts/100dpi/:unscaled"
        FontPath        "/usr/share/fonts/75dpi/:unscaled"
        FontPath        "/usr/share/fonts/Type1"
        FontPath        "/usr/share/fonts/100dpi"
        FontPath        "/usr/share/fonts/75dpi"
        FontPath        "/var/lib/defoma/x-ttcidfont-conf.d/dirs/TrueType"
EndSection

Section "Module"
        Load    "i2c"
        Load    "bitmap"
        Load    "ddc"
        Load    "dri"
        Load    "extmod"
        Load    "freetype"
        Load    "glx"
        Load    "int10"
        Load    "type1"
        Load    "vbe"
EndSection

Section "InputDevice"
        Identifier      "Keyboard"
        Driver          "kbd"
        Option          "CoreKeyboard"
        Option          "XkbRules"      "xorg"
        Option          "XkbModel"      "pc104"
        Option          "XkbLayout"     "cz"
EndSection

Section "InputDevice"
        Identifier      "Mouse"
        Driver          "mouse"
        Option          "CorePointer"
        Option          "Device"                "/dev/input/mice"
        Option          "Protocol"              "ExplorerPS/2"
        Option          "ZAxisMapping"          "4 5"
        Option          "Emulate3Buttons"       "true"
EndSection

Section "InputDevice"
        Identifier      "Touchpad"
        Driver          "synaptics"
        Option          "CorePointer"
        Option          "SendCoreEvents"        "true"
        Option          "Device"                "/dev/psaux"
        Option          "Protocol"              "auto-dev"
        Option          "HorizScrollDelta"      "0"
EndSection

Section "Device"
        Identifier      "Video"
        Driver          "i810"
EndSection

Section "Monitor"
        Identifier      "Monitor"
        Option          "DPMS"
EndSection

Section "Screen"
        Identifier      "Screen"
        Device          "Video"
        Monitor         "Monitor"
        DefaultDepth    24
        SubSection "Display"
                Depth           24
                Modes           "1280x800"
        EndSubSection
EndSection

Section "ServerLayout"
        Identifier      "MyXorg"
        Screen          "Screen"
        InputDevice     "Keyboard"
        InputDevice     "Mouse"
        InputDevice     "Touchpad"
EndSection

Section "DRI"
        Mode    0666
EndSection

```

### Poznámky:

*   Pro zprovoznění touchpadu je potřeba naistalovat synaptics drivery. (`balíček synaptics`)

*   Pro zprovoznění grafiky je potřeba naistalovat i810 drivery. (See [Intel graphics](/index.php/Intel_graphics "Intel graphics"))

*   Pokud nefunguje externí myš, zkontrolujte zda její umístění odpravdu odpovídá - více informací poskytne udevmonitor

*   Pro použití tohoto xorg.conf je potřeba také doinstalovat všechny možné xorg fonty.

## Procesor

See [Cpufreq](/index.php/Cpufreq "Cpufreq").

## Wi-fi

Je potřeba naistalovat ndiswrapper a ndiswrapper-utils a vlastnit správný ovladač pro danou wifi z windows (bcmwl5). Pozor! Velké množství driverů nefunguje. Mě fungovala tato verze (nejnovější, kterou jsem nalezl.)

[http://martin.kopta.eu/bcmwl5/](http://martin.kopta.eu/bcmwl5/) download inf and sys and save them in /root/drivers (for backup)

```
cd /root/drivers
ndiswrapper -i bcmwl5.inf
ndiswrapper -m
ndiswrapper -d 14e4:4311 bcmwl5

```

and edit /etc/rc.conf and write in to MODULES=(ndiswrapper)
after reboot (not needed but required) print iwconfig some like this

```
> iwconfig
lo        no wireless extensions.

wlan0     IEEE 802.11g  ESSID:off/any  
          Mode:Managed  Frequency:2.462 GHz  Access Point: Not-Associated   
          Bit Rate:54 Mb/s   Tx-Power:32 dBm   
          RTS thr:2347 B   Fragment thr:2346 B   
          Power Management:off
          Link Quality:0  Signal level:0  Noise level:0
          Rx invalid nwid:0  Rx invalid crypt:0  Rx invalid frag:0
          Tx excessive retries:0  Invalid misc:0   Missed beacon:0

eth0      no wireless extensions.

> 

```

## Multimediální klávesy

Gnome si s nimi bezproblémů poradí. `xev` je identifikuje a dají se bezproblému nastavit pomocí `xmodmap` i pro různé window manažery.
Zvláštně se chová tlačíko pro wi-fi. Po zadání příkazu `sudo iwlist wlan0 scan` se dioda rozsvítí a tlačítko začne normálně zapínat a vypínat diodku.

## Firewire

Nezkoušel jsem

## USB

Zcela funkční

## Eth

Zcela funkční

## Modem

Nezkoušel jsem

## VGA výstup

Nezkoušel jsem.

## Dokovací stanice

Nezkoušel jsem.

## Výpis bežných teplot

```
> acpi -V
     Thermal 1: active[3], 50.0 degrees C
     Thermal 2: ok, 46.0 degrees C
     Thermal 3: ok, 44.0 degrees C
     Thermal 4: ok, 16.0 degrees C
     Thermal 5: ok, 35.0 degrees C
  AC Adapter 1: on-line

```

*   Thermal 4 je baterie - v zobrazeném připadě baterie není přtomna v notebooku.

## Poznámky

*   wifi-radar mi dělal problémy - sice rozsvítil diodku, ale nenalezl žádnou síť a po pár vteřinách vytuhl celý počítač.

*   Výdrž na baterii -- 2.5 hod při čtení pdf