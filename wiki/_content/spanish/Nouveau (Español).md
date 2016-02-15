Este artículo describe la instalación y configuración del controlador de código abierto [Nouveau](http://nouveau.freedesktop.org/) para las tarjetas gráficas NVIDIA. Para obtener información sobre el controlador propietario, véase [NVIDIA](/index.php/NVIDIA_(Espa%C3%B1ol) "NVIDIA (Español)").

## Contents

*   [1 Con el controlador propietario NVIDIA instalado](#Con_el_controlador_propietario_NVIDIA_instalado)
*   [2 Instalación](#Instalaci.C3.B3n)
    *   [2.1 Activar Hardware Acceleration](#Activar_Hardware_Acceleration)
*   [3 Cargar el módulo](#Cargar_el_m.C3.B3dulo)
    *   [3.1 KMS](#KMS)
        *   [3.1.1 Inicio tardío](#Inicio_tard.C3.ADo)
        *   [3.1.2 Inicio temprano](#Inicio_temprano)
*   [4 Consejos y trucos](#Consejos_y_trucos)
    *   [4.1 Mantener el controlador NVIDIA instalado](#Mantener_el_controlador_NVIDIA_instalado)
    *   [4.2 Instalar los paquetes más recientes de desarrollo](#Instalar_los_paquetes_m.C3.A1s_recientes_de_desarrollo)
    *   [4.3 Problemas de lagrimeo con la composición](#Problemas_de_lagrimeo_con_la_composici.C3.B3n)
    *   [4.4 Dual Head](#Dual_Head)
    *   [4.5 Configuración de la resolución de la consola](#Configuraci.C3.B3n_de_la_resoluci.C3.B3n_de_la_consola)
    *   [4.6 Administración de energía](#Administraci.C3.B3n_de_energ.C3.ADa)
    *   [4.7 Activar MSI (Message Signaled Interrupts)](#Activar_MSI_.28Message_Signaled_Interrupts.29)
    *   [4.8 Optimus](#Optimus)
*   [5 Solución de problemas](#Soluci.C3.B3n_de_problemas)
    *   [5.1 Problema con salida fantasma](#Problema_con_salida_fantasma)

## Con el controlador propietario NVIDIA instalado

**Nota:** Esta sección está destinada únicamente para las personas que tienen instalado el controlador [NVIDIA](/index.php/NVIDIA_(Espa%C3%B1ol) "NVIDIA (Español)"). No es de utilidad para los demás usuarios.

**Sugerencia:** Si desea mantener instalado el controlador de Nvidia junto con Nouveau, ello [requierá alguna configuración adicional](#Mantener_el_controlador_NVIDIA_instalado) a fin de poder cargar el controlador Nouveau en lugar de Nvidia.

Si ya tiene instalado el controlador propietario de Nvidia, proceda primero a retirarlo:

```
# pacman -Rdds nvidia nvidia-utils nvidia-libgl

```

Asegúrese de eliminar también el archivo `/etc/X11/xorg.conf` que el controlador de Nvidia ha creado (o deshacer los cambios), o, de lo contrario X fallará y no cargará adecuadamente el controlador Nouveau.

## Instalación

Antes de continuar, eche un vistazo a [HardwareStatus](http://nouveau.freedesktop.org/wiki/HardwareStatus) para ver qué características son compatibles con una determinada arquitectura, y a la lista de [codenames](http://nouveau.freedesktop.org/wiki/CodeNames) de la propia tarjeta de vídeo. También puede consultar [Wikipedia](https://en.wikipedia.org/wiki/Comparison_of_Nvidia_Graphics_Processing_Units "wikipedia:Comparison of Nvidia Graphics Processing Units") para una lista más detallada. Asegúrese igualmente de que tiene instalado [Xorg](/index.php/Xorg_(Espa%C3%B1ol) "Xorg (Español)") correctamente.

[Instale](/index.php/Pacman_(Espa%C3%B1ol) "Pacman (Español)") el controlador DDX con el paquete [xf86-video-nouveau](https://www.archlinux.org/packages/?name=xf86-video-nouveau), el cual está disponible en los [repositorios oficiales](/index.php/Official_Repositories_(Espa%C3%B1ol) "Official Repositories (Español)"). Dicho paquete aporta [nouveau-dri](https://www.archlinux.org/packages/?name=nouveau-dri) como una dependencia, proporcionando el controlador DRI para una aceleración 3D.

Para utilizar aplicaciones de 32-bit con aceleración 3D en sistemas de x86_64, instale [lib32-nouveau-dri](https://www.archlinux.org/packages/?name=lib32-nouveau-dri) disponible en el repositorio [multilib](/index.php/Multilib "Multilib").

**Nota:** Consulte la [página de Nouveau MesaDrivers](http://nouveau.freedesktop.org/wiki/MesaDrivers) antes de informar de errores relativos al uso de los controladores para la aceleración 3D.

### Activar Hardware Acceleration

Para activar el acceso a la aceleración por hardware, el framebuffer, y los dispositivos de captura de vídeo, el usuario debe ser añadido al grupo `video`.

```
# gpasswd -a [user] video

```

## Cargar el módulo

El módulo del kernel Nouveau debe cargar bien de forma automática en el arranque del sistema.

Si esto no sucede, entonces:

*   Asegúrese de **no** tener `nomodeset` o `vga=` en los [parámetros del kernel](/index.php/Kernel_parameters_(Espa%C3%B1ol) "Kernel parameters (Español)"), de lo contrario el módulo Nouveau no será capaz de arrancar con éxito el kernel mode-setting (KMS) (véase más abajo).
*   Asimismo, compruebe que no ha desactivado el módulo de Nouveau mediante el uso del método blacklist en `/etc/modprobe.d/`.

### KMS

**Sugerencia:** Si tiene problemas con la resolución, compruebe [esta página](/index.php/Kernel_Mode_Setting_(Espa%C3%B1ol)#Forzar_modos "Kernel Mode Setting (Español)").

[Kernel Mode Setting](/index.php/Kernel_Mode_Setting_(Espa%C3%B1ol) "Kernel Mode Setting (Español)") (KMS) es requerido por el controlador Nouveau. Durante el arranque del sistema, la resolución es probable que cambie cuando KMS inicializa el controlador de vídeo. Simplemente instalando el controlador Nouveau debe ser suficiente para que el sistema reconozca y se inicialice en modo _«Late Start»_ (inicio tardío) (véase más abajo). Lectura adicional recomendada: [KernelModeSetting](http://nouveau.freedesktop.org/wiki/KernelModeSetting).

**Nota:** Algunos usuarios pueden preferir el método de inicio temprano, ya que no causa el cambio molesto de resolución durante el proceso de arranque

#### Inicio tardío

Con esta elección KMS se activa cuando los otros módulos del kernel se carguen. Usted verá el texto _«Loading modules»_ (Cargando los módulos) y el tamaño del texto puede cambiar, posiblemente con un parpadeo no deseado.

#### Inicio temprano

Este método iniciará KMS lo antes posible en el proceso de arranque, cuando [initramfs](/index.php/Mkinitcpio_(Espa%C3%B1ol) "Mkinitcpio (Español)") se carga. Aquí se indica cómo hacer esto con los paquetes oficiales:

Añadir `nouveau` a la matriz `MODULES` en `/etc/mkinitcpio.conf`:

```
MODULES="... nouveau ..."

```

Si está utilizando un archivo EDID personalizado, debe introducirlo en initramfs, así:

 `/etc/mkinitcpio.conf`  `FILES="/lib/firmware/edid/your_edid.bin"` 

Vuelva a generar la imagen ramdisk inicial:

```
# mkinitcpio -p <kernel preestablecido, por ejemplo linux>

```

Si experimenta problemas con nouveau y se ve obligado a reconstruir nouveau-drm varias veces para propósitos de prueba, no agregue `nouveau` a initramfs. Es fácil de obviar para reconstruir el initramfs y hacer alguna prueba más difícil. Solo tiene que utilizar _late start_ (inicio tardío) hasta que esté seguro de que el sistema es estable. Puede haber otros problemas con initramfs si necesita un firmware personalizado (por lo general no se recomienda).

## Consejos y trucos

### Mantener el controlador NVIDIA instalado

Si desea conservar el controlador propietario NVIDIA instalado, pero desea utilizar el controlador Nouveau, comente nouveau en blacklist en `etc/modprobe.d/nouveau_blacklist.conf` modificándolo de la siguiente manera:

```
**#**blacklist nouveau

```

Y ordene a Xorg cargar el controlador nouveau en vez del de nvidia, creando el archivo `/etc/X11/xorg.conf.d/20-nouveau.conf` con el siguiente contenido:

```
Section "Device"
    Identifier "Nvidia card"
    Driver     "nouveau"
EndSection

```

**Sugerencia:** Puede utilizar [estos scripts](/index.php/NVIDIA_(Espa%C3%B1ol)#Cambiar_entre_los_controladores_nvidia_y_nouveau "NVIDIA (Español)") si pretende cambiar entre los controladores propietario y libre muy a menudo.

Si ya ha utilizado el controlador de NVIDIA, y desea probar Nouveau sin reiniciar el sistema, asegúrese de que el módulo 'nvidia' ya no se carga:

```
# rmmod nvidia

```

A continuación, cargue el módulo 'nouveau':

```
# modprobe nouveau

```

Y compruebe que carga bien mirando los mensajes del kernel:

```
$ dmesg

```

### Instalar los paquetes más recientes de desarrollo

Se puede probar un controlador en su versión más reciente (-git), a través de AUR:

*   Puede usar [mesa-git](https://aur.archlinux.org/packages/mesa-git/), que permitirá la instalación del último controlador mesa (incluyendo la última versión del controlador DRI).
*   También puede usar [xf86-video-nouveau-git](https://aur.archlinux.org/packages/xf86-video-nouveau-git/), que permitirá la instalación de la última versión del controlador DDX.
*   Del mismo modo, se puede intentar instalar una versión del kernel más reciente, a través de paquetes de AUR como [linux-mainline](https://aur.archlinux.org/packages/linux-mainline/) en la que el código Nouveau DRM permitiría un mejor rendimiento.
*   Para obtener las últimas mejoras de nouveau, debe utilizar el paquete [linux-git](https://aur.archlinux.org/packages/linux-git/) de AUR, y editar el PKGBUILD para dirigirlo al repositorio propio del proyecto nouveau, que actualmente se encuentra en: [git://anongit.freedesktop.org/nouveau/linux-2.6](git://anongit.freedesktop.org/nouveau/linux-2.6).

La fuente de las versiones más recientes se puede encontrar aquí: [http://nouveau.freedesktop.org/wiki/Source](http://nouveau.freedesktop.org/wiki/Source).

### Problemas de lagrimeo con la composición

Edita tu `/etc/X11/xorg.conf.d/20-nouveau.conf`, y en la sección Device añadir:

```
Section "Device"
    Identifier "nvidia card"
    Driver     "nouveau"
    Option     "GLXVBlank" "true"
EndSection
```

### Dual Head

Nouveau soporta la extensión xrandr para modesetting y múltiples monitores. Consulte la página [RandR12](/index.php/RandR12 "RandR12") para el tutorial.

Aquí está una muestra completa `/etc/X11/xorg.conf.d/20-nouveau.conf` para la ejecución de 2 monitores en modo dual head. Es posible que prefiera utilizar una herramienta gráfica para configurar los monitores como el panel de GNOME Control Center's Display (`gnome-control-center display`).

```
# el del derecho
Section "Monitor"
          Identifier   "NEC"
          Option       "PreferredMode" "1280x1024_60.00"
EndSection

# el del izquierdo
Section "Monitor"
          Identifier   "FUS"
          Option       "PreferredMode" "1280x1024_60.00"
          Option       "LeftOf"        "NEC"
EndSection

Section "Device"
    Identifier "nvidia card"
    Driver     "nouveau"
    Option     "Monitor-DVI-I-1" "NEC"
    Option     "Monitor-DVI-I-2" "FUS"
EndSection

Section "Screen"
    Identifier   "screen1"
    DefaultDepth  24
      SubSection "Display"
       Depth      24
       Virtual    2560 2048
      EndSubSection
    Device       "nvidia card"
EndSection

Section "ServerLayout"
    Identifier "layout1"
    Screen     "screen1"
EndSection

```

### Configuración de la resolución de la consola

Use la herramienta [fbset](https://www.archlinux.org/packages/?name=fbset) para ajustar la resolución de la consola.

También puede pasar la resolución de nouveau con la opción **video=** a la línea del kernel (vea [KMS](/index.php/Kernel_Mode_Setting_(Espa%C3%B1ol) "Kernel Mode Setting (Español)")).

### Administración de energía

El escalado de la GPU para la gestión de la energía se encuentra en distintas etapas de desarrollo dependiendo de la GPU. Véase la página [Nouveau PowerManagement](http://nouveau.freedesktop.org/wiki/PowerManagement) para obtener más detalles.

### Activar MSI (Message Signaled Interrupts)

Esta opción puede proporcionar una ligera ventaja en términos de rendimiento. Es solo compatible con tarjetas NV50+ y está desactivada por defecto.

**Advertencia:** Este procedimiento puede causar inestabilidad con alguna combinación de la placa base / GPU

Inserte la siguiente línea en `/etc/modprobe.d/nouveau.conf`:

```
options nouveau msi=1

```

Si se utiliza el [inicio temprano](#Inicio_temprano), agregue la línea `FILES="/etc/modprobe.d/nouveau.conf"` al archivo `/etc/mkinitcpio.conf`, y, a continuación, vuelva a regenerar la imagen del kernel:

```
# mkinitcpio -p <kernel predefinido, por ejemplo linux>

```

Reinicie el sistema para hacer efectivos los cambios.

### Optimus

Tiene dos soluciones para utilizar Optimus en un ordenador portátil (también conocidos como gráficos híbridos, cuando tiene dos GPU en su portatil: [bumblebee](/index.php/Bumblebee "Bumblebee") y [PRIME](/index.php/PRIME "PRIME")

## Solución de problemas

Agregue lo siguiente a la línea de órdenes del kernel (si está utilizando GRUB presione `e` al mostrase el menú de inicio para poder editarlo) para activar la depuración del vídeo::

```
drm.debug=14 log_buf_len=16M

```

Cree un archivo que registre detalladamente el proceso de Xorg:

```
startx -- -logverbose 9 -verbose 9

```

Visualice los valores y parámetros cargados del módulo de vídeo:

```
modinfo -p video

```

#### Problema con salida fantasma

Es posible que el controlador nouveau detecte salidas «fantasma». Por ejemplo, cuando tanto VGA-1 como LVDS-1 aparecen como conectados pero solo LVDS-1 está presente.

Esto provoca problemas de visualización y una pantalla corrupta.

El problema se puede solucionar mediante la desactivación de la salida fantasma (VGA-1 en el ejemplo) en la línea de órdenes del kernel de su gestor de arranque. Esto se puede lograr añadiendo lo siguiente:

```
video=VGA-1:d

```

Donde **d** = desactivar.

La salida fantasma también se puede desactivar en X añadiendo lo siguiente a `/etc/X11/xorg.conf.d/20-nouveau.conf`:

```
Section "Monitor"
Identifier "VGA-1"
Option "Ignore" "1"
EndSection

```

**Fuente:** [http://gentoo-en.vfose.ru/wiki/Nouveau#Phantom_and_unpopulated_output_connector_issues](http://gentoo-en.vfose.ru/wiki/Nouveau#Phantom_and_unpopulated_output_connector_issues)