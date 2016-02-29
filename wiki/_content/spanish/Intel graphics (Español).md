Desde que Intel desarrolla y proporciona controladores de código abierto, las tarjetas de vídeo Intel son esencialmente plug-and-play.

Para obtener una lista completa de los modelos GPU-Intel, y los chipsets y CPUs correspondientes, consulte [esta comparación en la wikipedia](https://en.wikipedia.org/wiki/Comparison_of_Intel_graphics_processing_units "wikipedia:Comparison of Intel graphics processing units").

**Nota:** Las tarjetas gráficas basadas en el chip PowerVR (series [GMA 500](/index.php/GMA_500 "GMA 500") y [GMA 3600](/index.php/Intel_GMA3600 "Intel GMA3600")) no son compatibles con los controladores de código abierto.

## Contents

*   [1 Instalación](#Instalaci.C3.B3n)
*   [2 Configuración](#Configuraci.C3.B3n)
*   [3 KMS (Kernel Mode Setting)](#KMS_.28Kernel_Mode_Setting.29)
*   [4 Opciones de gestión de energía basadas en el módulo](#Opciones_de_gesti.C3.B3n_de_energ.C3.ADa_basadas_en_el_m.C3.B3dulo)
*   [5 Consejos y trucos](#Consejos_y_trucos)
    *   [5.1 Elegir el método de aceleración](#Elegir_el_m.C3.A9todo_de_aceleraci.C3.B3n)
    *   [5.2 Desactivar Vertical Synchronization (VSYNC)](#Desactivar_Vertical_Synchronization_.28VSYNC.29)
    *   [5.3 Ajustar la modalidad de escalado](#Ajustar_la_modalidad_de_escalado)
    *   [5.4 Problema KMS: la consola está limitada a una pequeña porción de la pantalla](#Problema_KMS:_la_consola_est.C3.A1_limitada_a_una_peque.C3.B1a_porci.C3.B3n_de_la_pantalla)
    *   [5.5 Decodificación H.264 en el chip GMA 4500](#Decodificaci.C3.B3n_H.264_en_el_chip_GMA_4500)
    *   [5.6 Establecer el valor gamma y el brillo](#Establecer_el_valor_gamma_y_el_brillo)
*   [6 Solución de problemas](#Soluci.C3.B3n_de_problemas)
    *   [6.1 Pantalla vacía durante el inicio, en la fase «Loading modules»](#Pantalla_vac.C3.ADa_durante_el_inicio.2C_en_la_fase_.C2.ABLoading_modules.C2.BB)
    *   [6.2 Vídeo rasgado](#V.C3.ADdeo_rasgado)
    *   [6.3 Congelación/bloqueo del servidor X con el controlador intel](#Congelaci.C3.B3n.2Fbloqueo_del_servidor_X_con_el_controlador_intel)
    *   [6.4 Añadir resoluciones no detectadas](#A.C3.B1adir_resoluciones_no_detectadas)
    *   [6.5 Lentitud tras una actualización de libGL 9 e Intel-DRI 9](#Lentitud_tras_una_actualizaci.C3.B3n_de_libGL_9_e_Intel-DRI_9)
    *   [6.6 Texturas en negro en videojuegos](#Texturas_en_negro_en_videojuegos)
    *   [6.7 Colores alterados (problema con el espacio de color)](#Colores_alterados_.28problema_con_el_espacio_de_color.29)
    *   [6.8 Retroiluminación no ajustable completamente, o no regulable del todo después de la reanudación](#Retroiluminaci.C3.B3n_no_ajustable_completamente.2C_o_no_regulable_del_todo_despu.C3.A9s_de_la_reanudaci.C3.B3n)
    *   [6.9 Desactivar la compresión del frame buffer](#Desactivar_la_compresi.C3.B3n_del_frame_buffer)
    *   [6.10 Alteraciones en Chrome/Chromium](#Alteraciones_en_Chrome.2FChromium)
*   [7 Véase también](#V.C3.A9ase_tambi.C3.A9n)

## Instalación

Prerrequisito: [Xorg](/index.php/Xorg_(Espa%C3%B1ol) "Xorg (Español)").

[Instale](/index.php/Pacman_(Espa%C3%B1ol) "Pacman (Español)") el paquete [xf86-video-intel](https://www.archlinux.org/packages/?name=xf86-video-intel) desde los [repositorios oficiales](/index.php/Official_repositories_(Espa%C3%B1ol) "Official repositories (Español)"). Este paquete proporciona el controlador DDX para la aceleración 2D y tira de [intel-dri](https://www.archlinux.org/packages/?name=intel-dri) como una dependencia, proporcionando el controlador DRI para la aceleración 3D.

Para soporte 3D de programas de 32 bits que corran en sistemas de x86_64, instale [lib32-intel-dri](https://www.archlinux.org/packages/?name=lib32-intel-dri) desde el repositorio [multilib](/index.php/Multilib "Multilib").

La aceleración de vídeo por hardware para codificar/decodificar en las GPU más antiguas es proporcionado por el controlador [XvMC](/index.php/XvMC "XvMC"), incluido en el controlador DDX. Para GPU más antiguas instale el controlador [VA-API](/index.php/VA-API "VA-API") proporcionado por el paquete [libva-intel-driver](https://www.archlinux.org/packages/?name=libva-intel-driver).

## Configuración

No necesita ningún tipo de configuración para hacer funcionar Xorg (el archivo `xorg.conf` no es necessario, pero tiene que estar configurado correctamente si está presente).

Para ver la lista de opciones, escriba `man intel`

## KMS (Kernel Mode Setting)

**Sugerencia:** Si tiene problemas con la resolución, compruebe [esta página](/index.php/Kernel_mode_setting_(Espa%C3%B1ol)#Forzar_modos "Kernel mode setting (Español)").

[KMS](/index.php/Kernel_mode_setting_(Espa%C3%B1ol) "Kernel mode setting (Español)") es necesario para ejecutar X y el entorno de escritorio, tales como [GNOME](/index.php/GNOME "GNOME"), [KDE](/index.php/KDE "KDE"), [Xfce](/index.php/Xfce "Xfce"), [LXDE](/index.php/LXDE "LXDE"), etc. KMS es compatible con el chipset Intel cuando usa el driver i915 DRM, el cual ahora está activado por defecto en el kernel v2.6.32\. Las versiones 2.10 del kernel y las más recientes del driver [xf86-video-intel](https://www.archlinux.org/packages/?name=xf86-video-intel) ya no dan soporte a UMS (excepto para la antigua familia de chipsets 810), que requieran el uso de KMS obligatoriamente. KMS se suele inicializar normalmente una vez arrancado el kernel. Es posible, sin embargo, habilitar KMS durante la fase de arranque el kernel, permitiendo que todo el proceso de arranque funcione en la resolución nativa.

**Nota:** Al utilizar KMS, **es necesario** quitar todas las referencias al obsoleto `vga` o `nomodeset` de la configuración de arranque.

Para proceder, añada el módulo `i915` a la matriz `MODULES` en `/etc/mkinitcpio.conf`:

```
MODULES="**i915**"

```

Si utiliza un archivo EDID personalizado, debe incorporarlo en initramfs de esta manera:

 `/etc/mkinitcpio.conf`  `FILES="/lib/firmware/edid/su_edid.bin"` 

A continuación, vuelva a crear el initramfs:

 `# mkinitcpio -p linux` 

y reinicie el sistema. Ahora todo debería funcionar.

## Opciones de gestión de energía basadas en el módulo

El módulo del kernel **i915** permite configurarlo a través de `/etc/modprobe.d/i915.conf`, donde se pueden establecer las opciones de gestión de energía. Existe un lista de opciones disponible a través de la orden:

```
$ modinfo i915 | grep power

```

He aquí un ejemplo de `/etc/modprobe.d/i915.conf`:

```
options i915 i915_enable_rc6=7 i915_enable_fbc=1 lvds_downclock=1

```

## Consejos y trucos

### Elegir el método de aceleración

*   UXA - (Unified Acceleration Architecture) es el backend maduro que se introdujo para apoyar el modelo de controlador GEM.
*   SNA - (Sandybridge's New Acceleration) es el sucesor más rápido para hardware compatible.

El método predeterminado es SNA (a partir de 2013-08-05[[2]](https://projects.archlinux.org/svntogit/packages.git/commit/trunk?h=packages/xf86-video-intel&id=d03f5fb77df413017821f492aa81e5d68def7e48)), el cual es menos estable, pero más rápido. Revisa los benchmarks realizados por Phoronix [[3]](http://www.phoronix.com/scan.php?page=news_item&px=MTEzOTE). Esto puede ser encontrado [aquí para Sandy Bridge](http://www.phoronix.com/scan.php?page=article&item=intel_glamor_first&num=1) y [aquí para Ivy Bridge](http://www.phoronix.com/scan.php?page=article&item=intel_ivy_glamor&num=1). UXA es aún una sólida opción, si experimenta problemas con SNA.

Para usar el antiguo método de aceleración UXA, se debe crear el archivo `/etc/X11/xorg.conf.d/20-intel.conf` con el siguiente contenido:

 `/etc/X11/xorg.conf.d/20-intel.conf` 
```
Section "Device"
   Identifier  "Intel Graphics"
   Driver      "intel"
   Option      "AccelMethod"  "uxa"
EndSection
```

### Desactivar Vertical Synchronization (VSYNC)

El controlador de intel utiliza [Triple Buffering](http://www.intel.com/support/graphics/sb/CS-004527.htm) para la sincronización vertical, lo que permite un rendimiento completo y evita la ruptura. Para poner la sincronización vertical en apagado (por ejemplo, para benchmarking) utilice este archivo .drirc en su carpeta «home»:

 `~/.drirc` 
```
<device screen="0" driver="dri2">
	<application name="Default">
		<option name="vblank_mode" value="0"/>
	</application>
</device>
```

No utilice [driconf](https://www.archlinux.org/packages/?name=driconf) para crear este archivo, producirá un error y establecerá el controlador incorrecto.

### Ajustar la modalidad de escalado

Este procedimiento puede ser útil para algunas aplicaciones a pantalla completa:

```
$ xrandr --output LVDS1 --set PANEL_FITTING param

```

donde `param` puede asumir los valores:

*   `center`: la resolución se mantendrá exactamente como está definida, no se aplicará ningún redimensionamiento.
*   `full`: Redimensiona el tamaño de la resolución para ocupar toda la pantalla.
*   `full_aspect`: Redimensiona el tamaño de la resolución al máximo permitido, manteniendo la relación de aspecto de la imagen.

Si esto no funciona, pruebe con:

```
$ xrandr --output LVDS1 --set "scaling mode" param

```

donde `param` puede tomar el valor de `"Full"`, `"Center"` o `"Full aspect"`.

### Problema KMS: la consola está limitada a una pequeña porción de la pantalla

Un puerto de vídeo de baja resolución puede ser activado en el inicio, causando el uso de solo una pequeña zona de la pantalla. Para solucionar esto, deshabilite explícitamente el puerto infractor proporcionando un reajuste del módulo i915 con `video=SVIDEO-1:d` como un parámetro a la línea de comandos del kernel en el gestor de arranque. Consulte los [parámetros del kernel](/index.php/Kernel_parameters_(Espa%C3%B1ol) "Kernel parameters (Español)") para más información.

Si esto no funciona, pruebe a sustituir TV1 o VGA1 en el lugar de SVIDEO-1.

### Decodificación H.264 en el chip GMA 4500

El paquete [libva-intel-driver](https://www.archlinux.org/packages/?name=libva-intel-driver) proporciona descodificación MPEG-2 solo para las GPUs de la serie GMA 4500\. El soporte para la decodificación de H.264 se mantiene en un rama separada, g45-h264, que se puede utilizar al instalar el paquete [libva-driver-intel-g45-h264](https://aur.archlinux.org/packages/libva-driver-intel-g45-h264/), disponible en el repositorio [AUR](/index.php/Arch_User_Repository_(Espa%C3%B1ol) "Arch User Repository (Español)"). Sin embargo, tenga en cuenta que este soporte es experimental y no está actualmente en desarrollo activo. El uso de VA-API en una tarjeta de la serie GMA 4500 descarga la GPU, pero no hace una reproducción más ágil, ya que la reproducción se hace sin aceleración. Las pruebas usando mplayer mostraton que el uso de VAAPI para reproducir un video H.264 codificado a 1080p redujo a la mitad la carga de la CPU (en comparación con la superposición XV), pero dió lugar a una reproducción muy agitada, mientras que codificado a 720p funcionó razonablemente bien [[4]](https://bbs.archlinux.org/viewtopic.php?id=150550). Esto se ha hecho eco de otras experiencias [[5]](http://www.emmolution.org/?p=192&cpage=1#comment-12292).

### Establecer el valor gamma y el brillo

Intel no proporciona un método para establecer estos parámetros en el controlador. Afortunadamente, se pueden establecer a través de `xgamma` y `xrandr`.

El rango de valores Gamma se puede ajustar con:

```
$ xgamma -gamma 1.0

```

o

```
$ xrandr --output VGA1 --gamma 1.0:1.0:1.0

```

El brillo se puede ajustar con:

```
$ xrandr --output VGA1 --brightness 1.0

```

## Solución de problemas

### Pantalla vacía durante el inicio, en la fase «Loading modules»

Si está utilizando el inicio tardío de KMS (*«late start»*), y la pantalla se queda sin mostrar nada durante la fase «Loading modules», puede ser útil agregar `i915` y `intel_agp` al initramfs. Consulte la [sección](#KMS_.28Kernel_Mode_Setting.29) anterior.

Como alternativa, puede intentar resolverlo añadiendo a la línea de comandos del kernel lo que sigue:

```
video=SVIDEO-1:d

```

### Vídeo rasgado

Si se utiliza el método de aceleración SNA, es posible resolver el problema activando la opción `"TearFree"` en el controlador:

 `/etc/X11/xorg.conf.d/20-intel.conf` 
```
Section "Device"
   Identifier  "Intel Graphics"
   Driver      "intel"
   Option      "TearFree"    "true"
EndSection
```

**Nota:**

*   Esta opción puede no funcionar cuando `SwapbuffersWait` es `false`.
*   Esta opción es problemática para las aplicaciones que son muy exigentes con la cadencia vsync, como [Super Meat Boy](https://en.wikipedia.org/wiki/Super_Meat_Boy "wikipedia:Super Meat Boy").
*   Con esta opción activada, algunas animaciones de Gnome Shell son sensiblemente lentas.

### Congelación/bloqueo del servidor X con el controlador intel

Si tiene un problema con le servidor X que termina inesperadamente, o que parece bloquearse, o la GPU no responde correctamente, puede que la solución sea desactivar el uso de la GPU con la opción `NoAccel`:

 `/etc/X11/xorg.conf.d/20-intel.conf` 
```
Section "Device"
   Identifier "Intel Graphics"
   Driver "intel"
   Option "NoAccel" "True"
EndSection
```

Como alternativa, pruebe a desactivar únicamente la aceleración 3D con la opción `DRI`:

 `/etc/X11/xorg.conf.d/20-intel.conf` 
```
Section "Device"
   Identifier "Intel Graphics"
   Driver "intel"
   Option "DRI" "False"
EndSection
```

Si el equipo falla y tiene

```
Option "TearFree" "true"
Option "AccelMethod" "sna"

```

en el archivo de configuración, en la mayoría de los casos se puede solucionar añadiendo

```
i915.semaphores=1

```

en los parámetros del arranque.

### Añadir resoluciones no detectadas

Esta cuestión se aborda en el artículo [Xrandr](/index.php/Xrandr#Adding_undetected_resolutions "Xrandr").

### Lentitud tras una actualización de libGL 9 e Intel-DRI 9

Efectuar un [Downgrade](/index.php/Downgrading_packages#ARM "Downgrading packages") para Intel-DRI 8 y libGL 8.

### Texturas en negro en videojuegos

Si está experimentando texturas negras en los juegos de vídeo, la solución puede ser habilitar el soporte S3TC que permite la compresión de texturas. Se puede activar a través de [driconf](https://www.archlinux.org/packages/?name=driconf) o instalando [libtxc_dxtn](https://www.archlinux.org/packages/?name=libtxc_dxtn) desde AUR.

Este «problema» se solucionará muy pronto en los [nuevos controladores](http://www.phoronix.com/scan.php?page=news_item&px=MTIwOTg)

Puede leer más sobre la compresión S3TC en: [http://dri.freedesktop.org/wiki/S3TC](http://dri.freedesktop.org/wiki/S3TC) [wikipedia:S3_Texture_Compression](https://en.wikipedia.org/wiki/S3_Texture_Compression "wikipedia:S3 Texture Compression")

Uno de los juegos que se ve afectado por este problema es [Oil Rush](http://www.phoronix.com/scan.php?page=article&item=unigine_oilrush_gold&num=2) y World of Warcraft usando Wine.

### Colores alterados (problema con el espacio de color)

**Nota:** Este problema está relacionado con los cambios en el kernel 3.9.

El Kernel 3.9 contiene las modificaciones del controlador Intel que permite un fácil ajuste de los rangos de RGB Limited, que puede causar la alteración de los colores en algunos casos. Esto se relaciona con el nuevo modo "Automatic" para la propiedad "Broadcast RGB". Se puede forzar la modalidad, por ejemplo con `xrandr --output HDMI1 --set "Broadcast RGB" "Full"` usando la salida del dispositivo apropiada distinta de HDMI1.

**Nota:** Algunos televisores solo pueden mostrar colores desde el rango 16-255, de modo que al ajustar a la modalidad *Full* causará un recorte de los colores en el rango de 0-15, por lo que es mejor dejarlo en *Automatic*, ya que de este modo detectará automáticamente si es necesario comprimir el espacio de color para el televisor.

También hay otros problemas relacionados que pueden ser resueltos modificado los registros de la GPU. Información adicional se puede encontrar en estas páginas: [[6]](http://lists.freedesktop.org/archives/intel-gfx/2012-April/016217.html) y [[7]](http://github.com/OpenELEC/OpenELEC.tv/commit/09109e9259eb051f34f771929b6a02635806404c).

### Retroiluminación no ajustable completamente, o no regulable del todo después de la reanudación

Si utiliza una tarjeta gráfica de Intel y no tiene control mediante las teclas de acceso rápido para modificar el brillo de la pantalla, pruebe iniciando el sistema con estos parámetros del kermel:

```
acpi_backlight=vendor

```

Si eso no resuelve el problema, algunos usuarios han conseguido resolverlo añadiendo, o bien:

```
acpi_osi=Linux

```

o

```
acpi_osi="!Windows 2012"

```

además del parámetro mencionado anteriormente.

Si ninguna de estas propuestas resuelve el problema, se debe editar/crear el archivo `/etc/X11/xorg.conf.d/20-intel.conf` con el contenido siguiente:

 `/etc/X11/xorg.conf.d/20-intel.conf` 
```
Section "Device"
        Identifier  "card0"
        Driver      "intel"
        Option      "Backlight"  "intel_backlight"
        BusID       "PCI:0:2:0"

EndSection
```

Si utiliza la aceleración SNA como se mencionó anteriormente, cree el archivo como sigue:

 `/etc/X11/xorg.conf.d/20-intel.conf` 
```
Section "Device"
        Identifier  "card0"
        Driver      "intel"
        Option      "AccelMethod"  "sna"
        Option      "Backlight"    "intel_backlight"
        BusID       "PCI:0:2:0"

EndSection
```

### Desactivar la compresión del frame buffer

En algunas tarjetas, como la Intel Corporation Mobile 4 Series Chipsets, la compresión del frame buffer está activada y forzada, lo que da como resultado mensajes de error sin fin:

```
$ dmesg |tail 
[ 2360.475430] [drm] not enough stolen space for compressed buffer (need 4325376 bytes), disabling
[ 2360.475437] [drm] hint: you may be able to increase stolen memory size in the BIOS to avoid this

```

La solución es desactivar la compresión del frame buffer, lo cual aumentará ligeramente el consumo de energía. En este sentido, para desactivarla hay que añadir `i915.i915_enable_fbc=0` a la línea de parámetros del kernel. Más información sobre los resultados de la desactivación de la compresión se puede encontrar [aquí](http://zinc.canonical.com/~cking/power-benchmarking/background-colour-and-framebuffer-compression/results.txt).

### Alteraciones en Chrome/Chromium

Si experimenta alteraciones en Chrome/Chromium establezca AccelMethod a "UXA" [#Elegir el método de aceleración](#Elegir_el_m.C3.A9todo_de_aceleraci.C3.B3n)

## Véase también

*   [http://intellinuxgraphics.org/documentation.html](http://intellinuxgraphics.org/documentation.html) (incluye una lista de hardware compatible)
*   [KMS](/index.php/Kernel_mode_setting_(Espa%C3%B1ol) "Kernel mode setting (Español)") — Artículo de Arch wiki sobre kernel mode setting
*   [Xrandr](/index.php/Xrandr "Xrandr") — Si tiene problemas con la configuración de la resolución
*   Arch Linux forums: [Intel 945GM, Xorg, Kernel - performance](https://bbs.archlinux.org/viewtopic.php?pid=522665#p522665)