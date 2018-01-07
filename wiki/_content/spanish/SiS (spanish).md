Esta página describe cómo hacer funcionar los adaptadores gráficos [Silicon Integrated Systems (SiS)](http://dri.freedesktop.org/wiki/SiS) en Arch Linux:

## Contents

*   [1 Paquetes](#Paquetes)
*   [2 lspci](#lspci)
*   [3 Módulos y rc.conf](#M.C3.B3dulos_y_rc.conf)
*   [4 xorg.conf](#xorg.conf)
    *   [4.1 Activar SSE](#Activar_SSE)
    *   [4.2 Tarjeta SiS 671](#Tarjeta_SiS_671)
    *   [4.3 Configuración para Monitor extendido](#Configuraci.C3.B3n_para_Monitor_extendido)

## Paquetes

Necesitará instalar el paquete [xf86-video-sis](https://aur.archlinux.org/packages/xf86-video-sis/), también es buena idea instalar [sisctrl](https://aur.archlinux.org/packages/sisctrl/) (herramienta gráfica para editar los modos de vídeo). Algunas tarjetas que no son soportadas por el controlador **sis** pueden funcionar instalando los paquetes [xf86-video-sisusb](https://www.archlinux.org/packages/?name=xf86-video-sisusb) y [xf86-video-sisimedia](https://aur.archlinux.org/packages/xf86-video-sisimedia/). También puede probar con [xf86-video-sis671](https://aur.archlinux.org/packages/xf86-video-sis671/) desde [AUR](/index.php/AUR "AUR").

## lspci

El resultado de `lspci` debe lucir algo así (varia según el modelo):

```
01:00.0 VGA compatible controller: Silicon Integrated Systems [SiS] 661/741/760 PCI/AGP or 662/761Gx PCIE VGA Display Adapter

```

## Módulos y rc.conf

Hay algunos módulos relacionados con las tarjesas de vídeo SiS:

```
$ lsmod | grep sis | sed -re 's#^([a-zA-Z0-9_-]*) *.*#\1#g' | xargs modinfo | grep 'filename:'
...
filename:       /usr/lib/modules/*{kernel-version}*/kernel/drivers/char/agp/sis-agp.ko.gz
filename:       /usr/lib/modules/*{kernel-version}*/kernel/drivers/char/agp/agpgart.ko.gz
...

```

*donde **{kernel-version}** es la versión del kernel instalado actualmente en el sistema. Por ejemplo kernel 3.7.1.1*.

Probablemente solo necesitará cargar **sis-agp** (este cargará los otros posibles módulos SIS que sean requeridos por tu hardware) colóquelo antes que los otros módulos, de modo que el orden del apartado MODULES en `/etc/rc.conf` debería lucir algo así:

```
MODULES=( **sis-agp** ... )

```

## xorg.conf

Aqui están algunas de las secciones mas importantes en `/etc/X11/xorg.conf`

*   Carga algunos módulos:

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

*   Especificaciones del dispositivo:

```
Section "Device"
  Identifier "Card0"
  Driver "sis"
  Card        "** SiS (generic)     [sis]"
  BusID "PCI:1:0:0"

  Option "UseFBDev"              "true"
  Option "EnableSisCtrl"         "yes"
  Option "ForceCRT1Type"         "LCD"
  Option "ForceCRT2Type"         "NONE"
  #Option "CRT2Detection"        "true" #Si utiliza esta opción, comente las dos líneas *Force* de arriba.
  Option "CRT1Gamma"             "on"
  Option "CRT2Gamma"             "on"
  Option "Brightness"            "0.000 0.000 0.000"
  Option "Contrast"              "0.000 0.000 0.000"
  Option "CRT1Saturation"        "0"
  Option "XvOnCRT2"              "yes"
  Option "XvDefaultContrast"     "2"
  Option "XvDefaultBrightness"   "10"
  Option "XvDefaultHue"          "0"
  Option "XvDefaultSaturation"   "0"
  Option "XvDefaultDisableGfxLR" "no"
  Option "XvGamma"               "off"
EndSection

```

*   Activar renderizado directo:

```
Section "DRI"
  Mode         0666
EndSection

```

#### Activar SSE

Activar o forzar el uso de SSE en la tarjeta SiS.

Añada

```
 Option "UseSSE" "yes"

```

a la sección `Device`.

#### Tarjeta SiS 671

Añada

```
Option          "UseTiming1366"      "yes"

```

a la sección `Device`.

### Configuración para Monitor extendido

Necesita 2 secciones «device» para activar la función monitor extendido. Algunas de las opciones específicas deberían ser colocadas en la sección de la pantalla principal.

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