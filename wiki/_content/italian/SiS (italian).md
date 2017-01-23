Questa pagina descrive come far funzionare [Silicon Integrated Systems (SiS)](http://dri.freedesktop.org/wiki/SiS) su Arch Linux:

## Contents

*   [1 Pacchetti](#Pacchetti)
*   [2 lspci](#lspci)
*   [3 Moduli & rc.conf](#Moduli_.26_rc.conf)
*   [4 xorg.conf](#xorg.conf)
    *   [4.1 Scheda SiS 671](#Scheda_SiS_671)
    *   [4.2 Configurazione doppio monitor](#Configurazione_doppio_monitor)

## Pacchetti

Servirà installare il pacchetto [xf86-video-sis](https://aur.archlinux.org/packages/xf86-video-sis/), ed è una buona idea installare anche [sisctrl](https://www.archlinux.org/packages/?name=sisctrl) (GUI per impostare le risoluzioni):

Alcune schede non supportate da **sis** driver package possono funzionare installando i pacchetti [xf86-video-sisusb](https://www.archlinux.org/packages/?name=xf86-video-sisusb) e [xf86-video-sisimedia](https://aur.archlinux.org/packages/xf86-video-sisimedia/). Puoi anche provare [xf86-video-sis671](https://aur.archlinux.org/packages/xf86-video-sis671/) da [AUR](/index.php/AUR "AUR").

## lspci

L'output di lspci dovrebbe essere simile a questo (dipende dal modello in uso):

```
01:00.0 VGA compatible controller: Silicon Integrated Systems [SiS] 661/741/760 PCI/AGP or 662/761Gx PCIE VGA Display Adapter

```

## Moduli & rc.conf

Qui ci sono alcuni moduli inerenti alle schede grafiche SiS:

```
$ modprobe -l | grep -i sis
/lib/modules/2.6.28-ARCH/kernel/drivers/usb/misc/sisusbvga/**sisusbvga**.ko
/lib/modules/2.6.28-ARCH/kernel/drivers/video/sis/**sisfb**.ko
/lib/modules/2.6.28-ARCH/kernel/drivers/char/agp/**sis-agp**.ko
/lib/modules/2.6.28-ARCH/kernel/drivers/gpu/drm/sis/**sis**.ko

```

Probabilmente servirà solo caricare **sisfb** (esso dovrebbe caricare gli altri moduli SiS richiesti dall'hardware) per primo e poi gli altri moduli. Quindi l'inizio di MODULES nel file `/etc/rc.conf` dovrebbe essere simile a questo:

```
MODULES=( **sisfb** ... )

```

## xorg.conf

Qui ci sono alcune importanti sezioni di /etc/X11/xorg.conf

1.  Caricamento dei moduli:

```
Section "Module"
  Load  "dbe"
  Load  "i2c"
  Load  "bitmap"
  Load  "ddc"
  Load  "dri"
  Load  "extmod"
  Load  "freetype"
  Load  "glx"
  Load  "int10"
  Load  "vbe"
EndSection

```

1.  Specificazione del dispositivo:

```
Section "Device"
  Identifier "Card0"
  Driver "sis"
  Card        "** SiS (generic)     [sis]"
  BusID "PCI:1:0:0"

  Option "UseFBDev" "true"
  Option "EnableSisCtrl" "yes"
  Option "ForceCRT1Type" "LCD"
  Option "ForceCRT2Type" "NONE"
  #Option "CRT2Detection" "true" #For me this worked better than forceing the detection. If you use this comment out the two Force lines above this.
  Option "CRT1Gamma" "on"
  Option "CRT2Gamma" "on"
  Option "Brightness" "0.000 0.000 0.000"
  Option "Contrast" "0.000 0.000 0.000"
  Option "CRT1Saturation" "0"
  Option "XvOnCRT2" "yes"
  Option "XvDefaultContrast" "2"
  Option "XvDefaultBrightness" "10"
  Option "XvDefaultHue" "0"
  Option "XvDefaultSaturation" "0"
  Option "XvDefaultDisableGfxLR" "no"
  Option "XvGamma" "off"
EndSection

```

1.  Abilita il Direct Rendering:

```
Section "DRI"
  Mode         0666
EndSection

```

#### Scheda SiS 671

Aggiungere

```
Option          "UseTiming1366"      "yes"

```

nella sezione `Device`.

### Configurazione doppio monitor

Servono 2 sezioni Device per abilitare il doppio monitor. Le impostazioni specifiche di SiS dovrebbero essere messe nella sezione Device del monitor principale.

```
Section "Monitor"
  Identifier   "CRT1"
  ModelName    "PANEL"
  Option       "DPMS"
  VendorName   "LCD"
  HorizSync    31-60
  VertRefresh  40-60
EndSection

Section "Monitor"
  Identifier   "CRT2"
  ModelName    "tv"
  Option       "DPMS"
  VendorName   "tv"
EndSection

Section "Screen"
  DefaultDepth 24
  SubSection "Display"
    Depth      24
    Modes      "1024x768".
  EndSubSection
  Device       "Device[0]"
  Identifier   "Screen[0]"
  Monitor      "CRT2"
EndSection

Section "Screen"
  DefaultDepth 24
  SubSection "Display"
    Depth      24
    Modes      "1024x768".
  EndSubSection
  Device       "Device[1]"
  Identifier   "Screen[1]"
  Monitor      "CRT1"
EndSection

Section "Device"
  BoardName    "630"
  BusID        "PCI:1:0:0"
  Driver       "sis"
  Identifier   "Device[1]"
  Screen       1
  VendorName   "SiS"
EndSection

Section "Device"
  BoardName    "630"
  BusID        "PCI:1:0:0"
  Driver       "sis"
  Identifier   "Device[0]"
  Screen       0
  VendorName   "SiS"
  Option "EnableSisCtrl" "true"
EndSection

Section "ServerLayout"
  Identifier   "Layout[dual]"
  ...
  Option       "Clone" "off"
  Screen       "Screen[0]"
  Screen       "Screen[1]" RightOf "Screen[0]"
  Option       "Xinerama" "off"
EndSection

```