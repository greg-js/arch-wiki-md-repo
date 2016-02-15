| **Dispositivo** | **Estado** | **Módulos** |
| Intel 945GME | **OK** | _xf86-video-intel_ |
| Red Cableada (ethernet) | **OK** |
| Red Inalámbrica (wireless) | **OK** |
| Audio | **OK** | _snd_hda_intel_ |
| Camara Web | **OK** | _uvcvideo_ |
| Tarjeta SD | **OK** |
| Teclas de función | **OK** |

La versión de este articulo está principalmente adaptado de la versión en ingles de la [Eee PC 1000HE](/index.php/ASUS_Eee_PC_1000HE "ASUS Eee PC 1000HE"), siéntase libre de expandirlo!

El kernel por defecto (actualmente 2.6.34) soporta todo el hardware de la 1005HA, así que se supone que todo debería funcionar luego de la instalación.

## Contents

*   [1 Instalación](#Instalaci.C3.B3n)
*   [2 Pantalla y dispositivos de ingreso](#Pantalla_y_dispositivos_de_ingreso)
    *   [2.1 Puntos Por Pulgada (DPI)](#Puntos_Por_Pulgada_.28DPI.29)
    *   [2.2 Rendimiento Gráfico](#Rendimiento_Gr.C3.A1fico)
    *   [2.3 Teclado](#Teclado)
    *   [2.4 Touchpad](#Touchpad)
        *   [2.4.1 Desplazamiento con dos dedos (manera simple)](#Desplazamiento_con_dos_dedos_.28manera_simple.29)
        *   [2.4.2 Desplazamiento con dos dedos (forma alternativa)](#Desplazamiento_con_dos_dedos_.28forma_alternativa.29)
    *   [2.5 xrandr (Extensión para cambiar de tamaño y rotar de X.org)](#xrandr_.28Extensi.C3.B3n_para_cambiar_de_tama.C3.B1o_y_rotar_de_X.org.29)
*   [3 Ahorro de energía y ACPI (Interfaz de Energía Avanzada)](#Ahorro_de_energ.C3.ADa_y_ACPI_.28Interfaz_de_Energ.C3.ADa_Avanzada.29)
    *   [3.1 Instalación y configuración de laptop-mode-tools](#Instalaci.C3.B3n_y_configuraci.C3.B3n_de_laptop-mode-tools)
        *   [3.1.1 Brillo del LCD](#Brillo_del_LCD)
        *   [3.1.2 Ahorro de energía en el CPU](#Ahorro_de_energ.C3.ADa_en_el_CPU)
        *   [3.1.3 Suspender USB](#Suspender_USB)
    *   [3.2 Instalación y configuración de cpufrequtils](#Instalaci.C3.B3n_y_configuraci.C3.B3n_de_cpufrequtils)
    *   [3.3 Teclas de Función (Hotkeys)](#Teclas_de_Funci.C3.B3n_.28Hotkeys.29)
        *   [3.3.1 Activar / Desactivar WiFi](#Activar_.2F_Desactivar_WiFi)
        *   [3.3.2 Teclas de Volumen](#Teclas_de_Volumen)
        *   [3.3.3 Suspender](#Suspender)
    *   [3.4 Configuración de Pantalla](#Configuraci.C3.B3n_de_Pantalla)
*   [4 Hardware](#Hardware)
    *   [4.1 Red Cableada (Ethernet)](#Red_Cableada_.28Ethernet.29)
    *   [4.2 Conexión Inalámbrica (WiFi)](#Conexi.C3.B3n_Inal.C3.A1mbrica_.28WiFi.29)
    *   [4.3 Cámara Web](#C.C3.A1mara_Web)
    *   [4.4 Micrófono](#Micr.C3.B3fono)
*   [5 Hardware Info](#Hardware_Info)
    *   [5.1 Información de Hardware (lspci)](#Informaci.C3.B3n_de_Hardware_.28lspci.29)
*   [6 Problemas](#Problemas)

# Instalación

Para una guía completa de instalación de Arch, vea la [Guía de Principiantes](/index.php/Beginners%27_Guide_(Espa%C3%B1ol) "Beginners' Guide (Español)").

# Pantalla y dispositivos de ingreso

Si todavía no lo ha instalado, necesita **[xorg-server](/index.php/Xorg_(Espa%C3%B1ol) "Xorg (Español)")** y **xf86-video-intel** para hacer funcionar X.org:

```
pacman -S xorg-server x86-video-intel

```

Este ejemplo usa hotplugging (conexiones sin apagar el sistema). Este seguro de que tenga instalado e iniciado hal. Ademas, no se olvide de agregar hal al array de DAEMONS=() en **[rc.conf](/index.php/Rc.conf_(Espa%C3%B1ol) "Rc.conf (Español)")** ([en ingles](/index.php/Rc.conf "Rc.conf"))! (/etc/rc.conf por defecto).

Nota: La 1005HA funciona correctamente sin utilizar xorg.conf! No hay necesidad de crear un archivo xorg.conf.

## Puntos Por Pulgada (DPI)

En general la resolución auto-detectada no se ajusta correctamente a la resolución mas pequeña. Una configuración cómoda seria 96dpi o 75dpi si le gusta ver fuentes realmente pequeñas. Una forma sencilla de configurar el DPI seria agregar esto al final del archivo **xserverrc** (/etc/X11/xinit/xserverrc por defecto).

```
 exec /usr/bin/X -nolisten tcp -dpi 96

```

## Rendimiento Gráfico

Con la nueva arquitectura de aceleración 2D de X.org (EXA), los usuarios de controladores (drivers) Intel podrán experimentar des-aceleración con los desplazamientos y re-trazados de las ventanas. Una posible solución a esto es reemplazar el controlador 2D por defecto de Intel (XXA), con el nuevo controlador de X.org. Añadir esto a la sección de controladores del archivo **xorg.conf** (/etc/X11/xorg.conf por defecto).

```
Option "AccelMethod" "exa" 
Option "MigrationHeuristic" "greedy"

```

Ademas para mejorar el rendimiento 2D, el rendimiento 3D de la tarjeta de video puede ser extremadamente mejorado agregando esta linea en el archivo /etc/profile. [[1]](https://bugs.launchpad.net/xserver-xorg-video-intel/+bug/195843)

```
export INTEL_BATCH=1

```

Ver [Intel](/index.php/Intel_(Espa%C3%B1ol) "Intel (Español)") ([en Ingles](/index.php/Intel "Intel")) para mas información.

De acuerdo con la documentación del controlador (driver) Intel, “X-Video Motion Compensation” o "XvMC" no está habilitado de forma predeterminada. Al habilitar esta opción puede reducir considerablemente el uso de CPU al reproducir vídeo MPEG-2\. Para habilitar esta opción, se deben hacer dos cosas; en primer lugar, agregar esta linea a la sección del dispositivo de tu **xorg.conf** (/etc/X11/xorg.conf por defecto):

```
Option "XvMC" "true"

```

Por último, crear un archivo de configuración para decirle al servidor X donde se encuentra la biblioteca XvMC:

```
echo /usr/lib/libIntelXvMC.so > /etc/X11/XvMCConfig

```

## Teclado

1.  Copiar **/usr/share/hal/fdi/policy/10osvendor/10-keymap.fdi** en **/etc/hal/fdi/policy**. ` cp /usr/share/hal/fdi/policy/10osvendor/10-keymap.fdi /etc/hal/fdi/policy/` 
2.  Editar **/etc/hal/fdi/policy/10-keymap.fdi** y cambiar **<merge key="input.xkb.layout" type="string">us</merge>** por **<merge key="input.xkb.layout" type="string">es</merge>**. ` nano /etc/hal/fdi/policy/10-keymap.fdi` 

## Touchpad

1.  Instalar el paquete **xf86-input-synaptics** con: ` pacman -S xf86-input-synaptics` 
2.  Crea un archivo de normas hal: ` cp /usr/share/hal/fdi/policy/10osvendor/11-x11-synaptics.fdi /etc/hal/fdi/policy/` 

He aquí un ejemplo de configuración:

```
<?xml version="1.0" encoding="ISO-8859-1"?>
<deviceinfo version="0.2">
  <device>
    <match key="info.product" contains="ETPS/2 Elantech Touchpad">
        <append key="info.capabilities" type="strlist">input.touchpad</append>
    </match> 
    <match key="info.capabilities" contains="input.touchpad">
        <merge key="input.x11_driver" type="string">synaptics</merge>
        <merge key="input.x11_options.SHMConfig" type="string">on</merge>
        <merge key="input.x11_options.MaxSpeed" type="string">1.00</merge>
        <merge key="input.x11_options.MinSpeed" type="string">0.75</merge>
        <merge key="input.x11_options.Emulate3Buttons" type="string">on</merge>
        <merge key="input.x11_options.TapButton1" type="string">1</merge>
        <merge key="input.x11_options.TapButton2" type="string">2</merge>
        <merge key="input.x11_options.TapButton3" type="string">3</merge>
        <merge key="input.x11_options.LockedDrags" type="string">1</merge>
    </match>
  </device>
</deviceinfo>

```

Para obtener mas información, vea [Touchpad Synaptics](/index.php/Touchpad_Synaptics_(Espa%C3%B1ol) "Touchpad Synaptics (Español)") ([en ingles](/index.php/Touchpad_Synaptics "Touchpad Synaptics")).

### Desplazamiento con dos dedos (manera simple)

Añadirlo siguiente al archivo **11-x11-synaptics.fdi**:

```
<merge key="input.x11_options.VertTwoFingerScroll" type="string">true</merge>
<merge key="input.x11_options.HorizTwoFingerScroll" type="string">true</merge>
<merge key="input.x11_options.EmulateTwoFingerMinZ" type="string">10</merge>
<merge key="input.x11_options.EmulateTwoFingerMinW" type="string">7</merge>

```

### Desplazamiento con dos dedos (forma alternativa)

Cree este script:

```
#!/bin/sh 
# 
# Use xinput --list-props "SynPS/2 Synaptics TouchPad" para extraer datos
# 

# Establece los parámetros de emulación multi-touch
xinput set-int-prop "SynPS/2 Synaptics TouchPad" "Synaptics Two-Finger Pressure" 32 10 
xinput set-int-prop "SynPS/2 Synaptics TouchPad" "Synaptics Two-Finger Width" 32 8 
xinput set-int-prop "SynPS/2 Synaptics TouchPad" "Two-Finger Scrolling" 8 1 
xinput set-int-prop "SynPS/2 Synaptics TouchPad" "Synaptics Two-Finger Scrolling" 8 1 1 

# Deshabilitar desplazamiento lateral
xinput set-int-prop "SynPS/2 Synaptics TouchPad" "Synaptics Edge Scrolling" 8 0 0 0 

# Esto hará que el cursor no salte si tiene dos dedos sobre el touchpad y levanta uno
# (Que se suele hacer después de desplazarse con dos dedos)
xinput set-int-prop "SynPS/2 Synaptics TouchPad" "Synaptics Jumpy Cursor Threshold" 32 110 

```

Hágalo ejecutable con:

```
chmod +x _<script-name>_

```

y por ultimo, agreguelo a **[~/.xinitrc](/index.php/Xinitrc_(Espa%C3%B1ol) "Xinitrc (Español)")** para que se ejecute al inicio. [[2]](http://blog.twinapex.fi/2009/10/11/setting-up-multi-touch-scrolling-for-ubuntu-9-10-karmic-koala-linux-on-asus-eee-1005ha-netbook/)

## xrandr (Extensión para cambiar de tamaño y rotar de X.org)

Para una utilidad interesante de GUI, intente **lxrandr**; es muy fácil de usar!

Cambiar a monitor externo:

```
xrandr --output LVDS --off --output VGA --auto

```

Volver al LCD de la EeePC:

```
xrandr --output LVDS --auto --output VGA --off

```

# Ahorro de energía y ACPI (Interfaz de Energía Avanzada)

Inicie su aventura de ahorro de energía instalando Powertop. Básicamente es un programa para ver cuanta energía se esta utilizando, pero también proporciona algunos consejos para mejorar el rendimiento.

```
pacman -S powertop

```

Un buen punto de partida, es deshabilitar el hardware que no va a utilizar. Reinicie el sistema e ingrese a la configuración del BIOS pulsando F2\. Deshabilitar por ejemplo, el lector de tarjetas, la cámara web, la red cableada (ethernet), pero sólo si no los necesita, por supuesto.

De acuerdo con Powertop, la 1005HA utiliza alrededor de 7-10 Watts en un nivel de máximo ahorro (utilizando **laptop-mode-tools** y **[cpufreq](/index.php/Cpufreq "Cpufreq")**, y habiendo deshabilitado el hardware previamente mencionado). En estado de inactividad, el consumo es de entre 5-6 Watts. Por favor informe como reducirlo aun mas!

## Instalación y configuración de laptop-mode-tools

**laptop-mode-tools** es una manera fácil y agradable de configurar la mayor parte de las opciones de ahorro de energía en la 1005HA. Estos incluyen varias opciones, desde bajar la frecuencia de giro del disco duro y el consumo del CPU, como también la auto-suspensión de los puertos USB, el control del brillo de la pantalla y mucho mas. Provee una gran centralización de los archivos de configuración, como también, archivos separados para cada uno de los módulos controlados por las opciones de ahorro.

Instalar el paquete con:

```
pacman -S laptop-mode-tools

```

El archivo de configuración principal se encuentra por defecto en **/etc/laptop-mode/laptop-mode.conf**, pero hay mas archivos de configuración en el directorio **/etc/laptop-mode/conf.d/**. Asegúrese de leerlos por completo y configurarlos correctamente.

Note la opción en el archivo laptop-mode.conf que permite iniciar automáticamente los demás módulos.

Algunas opciones especificas para algunos modulos de la 1005HA (hay muchos mas):

### Brillo del LCD

Para configurar el brillo del LCD, edite el archivo /etc/laptop-mode/conf.d/lcd-brightness.conf y ajuste lo como mas le convenga. El valor mínimo (mas oscuro) es 0 y el valor máximo (mas claro) es 15, esta es la configuración sugerida:

```
BATT_BRIGHTNESS_COMMAND="echo 1"
LM_AC_BRIGHTNESS_COMMAND="echo 15"
NOLM_AC_BRIGHTNESS_COMMAND="echo 15"
BRIGHTNESS_OUTPUT="/proc/acpi/video/VGA/LCDD/brightness"

```

### Ahorro de energía en el CPU

El “Super Hybrid Engine” de la EeePC (como se lo conoce en Windows), tiene un efecto significativo en el ahorro de energía. Esto reduce la frecuencia de reloj (underclock) del FSB (front-side bus) para ahorrar energía, o la aumenta para mejorar el rendimiento; es controlado mediante **/sys/devices/platform/eeepc/cpufv**, que es provisto por el modulo eeepc_laptop. Esta incluido en el packete laptop-mode-tools y es activado y configurado mediante el archivo **/etc/laptop-mode/conf.d/eee-superhe.conf**. [[3]](https://bbs.archlinux.org/viewtopic.php?id=74951)

A partir de la versión 2.6.32 del kernel, el modulo eeepc_laptop no funciona; para hacerlo funcionar nuevamente, se debe agregar esta linea en el archivo de configuración de [GRUB](/index.php/GRUB "GRUB") (/boot/grub/menu.lst por defecto):

```
acpi_osi=Linux

```

_Ejemplo:_

```
# (0) Arch Linux
title  Arch Linux
root   (hd0,0)
kernel /vmlinuz26 root=/dev/disk/by-uuid/62db43c3-8321-479d-a2a0-0608fc566bc9 ro acpi_osi=Linux
initrd /kernel26.img

```

La frecuencia del CPU puede ser controlada a través del archivo **/etc/laptop-mode/conf.d/cpufreq.conf**, provisto por el laptop-mode-tools. Un buen valor es “T2” (75% de la velocidad normal) cuando esta utilizando la batería y el rendimiento es el mínimo; y velocidad máxima cuando esta conectado a el cargador. De todas maneras, utilizando el paquete **[cpufrequtils](/index.php/Cpufrequtils "Cpufrequtils")** (vea a continuación), es por lo general una mejor opción, ya que cambia automáticamente el uso del CPU de acuerdo a la configuración establecida.

### Suspender USB

Sugerencia: use la opción para desactivar el uso de algunos dispositivos USB (por ejemplo: modems 3G) usando el ID que muestra el comando **lsusb**, y luego insertándolo en el archivo de configuración.

## Instalación y configuración de cpufrequtils

Para reducir el uso de energía del CPU, seguramente este interesado en **[cpufrequtils](/index.php/Cpufrequtils "Cpufrequtils")**. El “[daemon](/index.php/Daemon "Daemon")” (proceso secundario o servidor) provisto por este script, se encarga de automatizar su uso. Usted puede elegir un valor de frecuencia mínima (min_freq) mayor (por ejemplo: 1000MHz) si prefiere que el sistema responda con mayor fluidez, mientras ahorra algo de energía. Note que esto también puede ser manejado por laptop-mode-tools si así lo prefiere.

1.  Instalar el paquete: ` pacman -S cpufrequtils` 
2.  Editar **/etc/conf.d/cpufreq** ` min_freq="800MHz" max_freq="1.60GHz"` 
3.  Agregar los módulos: ` modprobe acpi-cpufreq cpufreq_ondemand cpufreq_powersave` 
4.  Agregar los módulos anteriores al array MODULES=() en el archivo **rc.conf** (/etc/rc.conf por defecto).
5.  Iniciar el daemon: ` /etc/rc.d/cpufreq start` 
6.  Agregar **cpufreq** al array DAEMONS=() en el archivo **rc.conf**.

## Teclas de Función (Hotkeys)

Para activar las teclas de función (Fn+F1, Bloqueo del Touchpad, Tecla de encendido y apagado, SuperHybridEngine, etc.), instale el paquete **acpi-eeepc-generic** [[4]](https://aur.archlinux.org/packages.php?ID=23318) de AUR. La configuración se encuentra en el archivo **/etc/conf.d/acpi-eeepc-generic.conf**.

### Activar / Desactivar WiFi

Para activar la tecla de activar/desactivar Wifi (Fn+F2), edite el archivo de configuración de **acpi-eeepc-generic** y cambie: [[5]](http://code.google.com/p/acpi-eeepc-generic/wiki/Wireless)

```
COMMANDS_WIFI_TOGGLE=("/etc/acpi/eeepc/acpi-generic-toggle-wifi.sh")

```

por

```
COMMANDS_WIFI_TOGGLE=()

```

### Teclas de Volumen

Para hacer funcionar las teclas de _Mudo_, _Aumentar_ y _Disminuir_ el volumen, edite el archivo **/etc/conf.d/acpi-eeepc-generic.conf** y reemplace las lineas:

```
COMMANDS_MUTE=("alsa_toggle_mute")
COMMANDS_VOLUME_DOWN=("alsa_set_volume 5%-")
COMMANDS_VOLUME_UP=("alsa_set_volume 5%+")

```

por

```
COMMANDS_MUTE=("amixer set Master toggle")
COMMANDS_VOLUME_DOWN=("amixer set Master 10%-")
COMMANDS_VOLUME_UP=("amixer set Master 10%+")

```

Note que el valor 10% puede ser reemplazado por cualquiera que usted prefiera, vea la pagina de manual del [amixer](/index.php/ALSA_(Espa%C3%B1ol) "ALSA (Español)") (_man amixer_).

### Suspender

Si tiene problemas con el script proporcionado por acpi-eeepc-generic, entonces pruebe **pm-suspend**.

Para sustituir el script de acpi-eeepc-generic por **pm-suspend**, edite **/etc/conf.d/acpi-eeepc-generic.conf** y comente las siguientes lineas (agregando # al principio):

```
COMMANDS_SLEEP=("/etc/acpi/eeepc/acpi-eeepc-generic-suspend2ram.sh")

```

reemplacelo por:

```
COMMANDS_SLEEP=("/usr/sbin/pm-suspend")

```

## Configuración de Pantalla

Cree el archivo **/etc/X11/xorg.conf** y agregue las siguientes lineas en el, para activar la compresion del framebuffer de Intel, la cual, de acuerdo a [Lesswats.org](http://www.lesswatts.org/projects/display-and-graphics/faq.php), supone un pequeño ahorro de energía.

```
Section "Device"
	Identifier	"Builtin Default intel Device 0"
	Driver		"intel"
	Option		"FramebufferCompression" "on"
	Option		"AccelMethod" "EXA"
	Option		"Tiling" "on"
EndSection

```

# Hardware

## Red Cableada (Ethernet)

Funciona por defecto con el kernel 2.6.32, si tienes alguna version anterior, posiblemente necesite instalar los drivers de AUR. [[6]](https://aur.archlinux.org/packages.php?ID=30159)

## Conexión Inalámbrica (WiFi)

El WiFi funciona por defecto con el kernel de Arch (probado con 2.6.30, 2.6.32 y 2.6.34).

## Cámara Web

Para activar y desactivar la cámara:

1.  Activar ` echo 1 > /sys/devices/platform/eeepc/camera` 
2.  Desactivar ` echo 0 > /sys/devices/platform/eeepc/camera` 

Si realmente desea desactivar la cámara, se recomienda que mire en la parte de dispositivos del BIOS.

Asegúrese de que el modulo **uvcvideo** este cargado.

Para grabar videos y sacar fotos, se recomienda usar [cheese](https://www.archlinux.org/packages/?name=cheese) o [wxcam](https://www.archlinux.org/packages/?name=wxcam).

Para simplemente probar la cámara, se puede utilizar **mplayer**:

```
mplayer -fps 15 tv://

```

La cámara web funciona con Skype.

## Micrófono

El micrófono funciona por defecto, solo se debe configurar en alsamixer; ingrese a la configuración:

```
alsamixer

```

Presione <F4> para ir a la sección 'Capture' (Capturar). Navegue hasta el item 'Capture' (Capturar) utilizando las flechas de la derecha y la izquierda y revise que aparezca 'LR Capture'. De no ser así, presione la barra espaciadora. Los valores de 'Capturar' y 'Digital' son un balanceo entre la estática y el incremento. Se recomienda fijar el valor entre 70 y 75 (usando las flechas de arriba y abajo) respectivamente, aunque esto puede ser configurado a su gusto. Salga de _alsamixer_ presionando <ESC> y pruebelo:

```
arecord /tmp/record.wav

```

Diga algo cerca del micrófono y luego presione <Ctrl+C> para terminar la grabación. Ahora pruebelo con:

```
aplay /tmp/record.wav 

```

Si todo funciona correctamente, guarde los cambios (como root):

```
alsactl store

```

[[7]](https://bbs.archlinux.org/viewtopic.php?pid=495168#p495168)

# Hardware Info

## Información de Hardware (lspci)

```
[ ~]$ lspci
00:00.0 Host bridge: Intel Corporation Mobile 945GME Express Memory Controller Hub (rev 03)
00:02.0 VGA compatible controller: Intel Corporation Mobile 945GME Express Integrated Graphics Controller
(rev 03)
00:02.1 Display controller: Intel Corporation Mobile 945GM/GMS/GME, 943/940GML Express Integrated Graphics
Controller (rev 03)
00:1b.0 Audio device: Intel Corporation 82801G (ICH7 Family) High Definition Audio Controller (rev 02)
00:1c.0 PCI bridge: Intel Corporation 82801G (ICH7 Family) PCI Express Port 1 (rev 02)
00:1c.1 PCI bridge: Intel Corporation 82801G (ICH7 Family) PCI Express Port 2 (rev 02)
00:1c.3 PCI bridge: Intel Corporation 82801G (ICH7 Family) PCI Express Port 4 (rev 02)
00:1d.0 USB Controller: Intel Corporation 82801G (ICH7 Family) USB UHCI Controller #1 (rev 02)
00:1d.1 USB Controller: Intel Corporation 82801G (ICH7 Family) USB UHCI Controller #2 (rev 02)
00:1d.2 USB Controller: Intel Corporation 82801G (ICH7 Family) USB UHCI Controller #3 (rev 02)
00:1d.3 USB Controller: Intel Corporation 82801G (ICH7 Family) USB UHCI Controller #4 (rev 02)
00:1d.7 USB Controller: Intel Corporation 82801G (ICH7 Family) USB2 EHCI Controller (rev 02)
00:1e.0 PCI bridge: Intel Corporation 82801 Mobile PCI Bridge (rev e2)
00:1f.0 ISA bridge: Intel Corporation 82801GBM (ICH7-M) LPC Interface Bridge (rev 02)
00:1f.2 SATA controller: Intel Corporation 82801GBM/GHM (ICH7 Family) SATA AHCI Controller (rev 02)
01:00.0 Ethernet controller: Atheros Communications Atheros AR8132 / L1c Gigabit Ethernet Adapter (rev c0)
02:00.0 Network controller: Atheros Communications Inc. AR9285 Wireless Network Adapter (PCI-Express) (rev 01)

```

# Problemas

Ninguno por el momento.