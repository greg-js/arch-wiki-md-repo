Este artículo trata sobre la instalación y configuración de los controladores *propietarios* para la tarjeta gráfica [NVIDIA](http://www.nvidia.com). Si, por el contrario, desea obtener información acerca de los controladores de código abierto, consulte [Nouveau](/index.php/Nouveau_(Espa%C3%B1ol) "Nouveau (Español)").

## Contents

*   [1 Instalación](#Instalaci.C3.B3n)
    *   [1.1 Instalación alternativa: kernel personalizado](#Instalaci.C3.B3n_alternativa:_kernel_personalizado)
    *   [1.2 Recompilación automatica del modulo NVIDIA para cada actualización en cualquier kernel](#Recompilaci.C3.B3n_automatica_del_modulo_NVIDIA_para_cada_actualizaci.C3.B3n_en_cualquier_kernel)
*   [2 Configuración](#Configuraci.C3.B3n)
    *   [2.1 Configuración mínima](#Configuraci.C3.B3n_m.C3.ADnima)
    *   [2.2 Configuración automática](#Configuraci.C3.B3n_autom.C3.A1tica)
    *   [2.3 Varios monitores](#Varios_monitores)
        *   [2.3.1 TwinView](#TwinView)
            *   [2.3.1.1 Configuración manual de CLI con xrandr](#Configuraci.C3.B3n_manual_de_CLI_con_xrandr)
        *   [2.3.2 Utilizar NVIDIA Settings](#Utilizar_NVIDIA_Settings)
        *   [2.3.3 ConnectedMonitor](#ConnectedMonitor)
        *   [2.3.4 Modo mosaic](#Modo_mosaic)
            *   [2.3.4.1 Mosaic básico](#Mosaic_b.C3.A1sico)
            *   [2.3.4.2 Mosaic SLI](#Mosaic_SLI)
*   [3 Optimización](#Optimizaci.C3.B3n)
    *   [3.1 GUI: nvidia-settings](#GUI:_nvidia-settings)
    *   [3.2 Activar MSI (Message Signaled Interrupts)](#Activar_MSI_.28Message_Signaled_Interrupts.29)
    *   [3.3 Avanzado: 20-nvidia.conf](#Avanzado:_20-nvidia.conf)
        *   [3.3.1 Activar desktop composition](#Activar_desktop_composition)
        *   [3.3.2 Desactivar la aparición del logo al iniciar](#Desactivar_la_aparici.C3.B3n_del_logo_al_iniciar)
        *   [3.3.3 Activar aceleración por hardware](#Activar_aceleraci.C3.B3n_por_hardware)
        *   [3.3.4 Omitir la detección de monitor](#Omitir_la_detecci.C3.B3n_de_monitor)
        *   [3.3.5 Activar el triple buffering](#Activar_el_triple_buffering)
        *   [3.3.6 Usar los eventos del sistema](#Usar_los_eventos_del_sistema)
        *   [3.3.7 Activar el ahorro de energía](#Activar_el_ahorro_de_energ.C3.ADa)
        *   [3.3.8 Activar el control del brillo](#Activar_el_control_del_brillo)
        *   [3.3.9 Activar la modalidad SLI](#Activar_la_modalidad_SLI)
        *   [3.3.10 Forzar el nivel de rendimiento Powermizer (para portátiles)](#Forzar_el_nivel_de_rendimiento_Powermizer_.28para_port.C3.A1tiles.29)
            *   [3.3.10.1 Dejar que la GPU establezca su propio nivel de rendimiento basado en la temperatura](#Dejar_que_la_GPU_establezca_su_propio_nivel_de_rendimiento_basado_en_la_temperatura)
        *   [3.3.11 Desactivar vblank interrupts (para portátiles)](#Desactivar_vblank_interrupts_.28para_port.C3.A1tiles.29)
        *   [3.3.12 Activar overclocking](#Activar_overclocking)
            *   [3.3.12.1 Configurar un marcador estático 2D/3D](#Configurar_un_marcador_est.C3.A1tico_2D.2F3D)
*   [4 Consejos y trucos](#Consejos_y_trucos)
    *   [4.1 Ajustar la resolución del terminal de inicio](#Ajustar_la_resoluci.C3.B3n_del_terminal_de_inicio)
    *   [4.2 Activar Vídeo HD (VDPAU/VAAPI)](#Activar_V.C3.ADdeo_HD_.28VDPAU.2FVAAPI.29)
    *   [4.3 Decodificar aceleración de vídeo por hardware con XvMC](#Decodificar_aceleraci.C3.B3n_de_v.C3.ADdeo_por_hardware_con_XvMC)
    *   [4.4 Usar la salida de TV](#Usar_la_salida_de_TV)
    *   [4.5 X con un televisor (DFP) como única pantalla](#X_con_un_televisor_.28DFP.29_como_.C3.BAnica_pantalla)
    *   [4.6 Comprobar el estado de energía](#Comprobar_el_estado_de_energ.C3.ADa)
    *   [4.7 Visualizar la temperatura de la GPU en la shell](#Visualizar_la_temperatura_de_la_GPU_en_la_shell)
        *   [4.7.1 Método 1 - nvidia-settings](#M.C3.A9todo_1_-_nvidia-settings)
        *   [4.7.2 Método 2 - nvidia-smi](#M.C3.A9todo_2_-_nvidia-smi)
        *   [4.7.3 Método 3 - nvclock](#M.C3.A9todo_3_-_nvclock)
    *   [4.8 Ajustar la velocidad del ventilador en la sesión](#Ajustar_la_velocidad_del_ventilador_en_la_sesi.C3.B3n)
    *   [4.9 Orden de instalación/desinstalación para cambiar los controladores](#Orden_de_instalaci.C3.B3n.2Fdesinstalaci.C3.B3n_para_cambiar_los_controladores)
    *   [4.10 Cambiar entre los controladores NVIDIA y nouveau](#Cambiar_entre_los_controladores_NVIDIA_y_nouveau)
*   [5 Solución de problemas](#Soluci.C3.B3n_de_problemas)
    *   [5.1 Rendimiento bajo, por ejemplo, rediseño lento al cambiar las pestañas en Chrome](#Rendimiento_bajo.2C_por_ejemplo.2C_redise.C3.B1o_lento_al_cambiar_las_pesta.C3.B1as_en_Chrome)
    *   [5.2 Jugar usando Twinview](#Jugar_usando_Twinview)
    *   [5.3 Sincronización vertical usando TwinView](#Sincronizaci.C3.B3n_vertical_usando_TwinView)
    *   [5.4 Antigua configuración de Xorg](#Antigua_configuraci.C3.B3n_de_Xorg)
    *   [5.5 Pantalla corrupta: el problema de las «seis pantallas»](#Pantalla_corrupta:_el_problema_de_las_.C2.ABseis_pantallas.C2.BB)
    *   [5.6 Error '/dev/nvidia0' Input/Output](#Error_.27.2Fdev.2Fnvidia0.27_Input.2FOutput)
    *   [5.7 Errores '/dev/nvidiactl'](#Errores_.27.2Fdev.2Fnvidiactl.27)
    *   [5.8 Las aplicaciones de 32 bits no se inician](#Las_aplicaciones_de_32_bits_no_se_inician)
    *   [5.9 Errores después de actualizar el kernel](#Errores_despu.C3.A9s_de_actualizar_el_kernel)
    *   [5.10 Fallo general](#Fallo_general)
    *   [5.11 Inadecuado rendimiento después de instalar una nueva versión del controlador](#Inadecuado_rendimiento_despu.C3.A9s_de_instalar_una_nueva_versi.C3.B3n_del_controlador)
    *   [5.12 Picos altos de la CPU con tarjetas de la serie 400](#Picos_altos_de_la_CPU_con_tarjetas_de_la_serie_400)
    *   [5.13 Portátiles: X se bloquea al iniciar/cerrar sesión, obviado con Ctrl+Alt+Backspace](#Port.C3.A1tiles:_X_se_bloquea_al_iniciar.2Fcerrar_sesi.C3.B3n.2C_obviado_con_Ctrl.2BAlt.2BBackspace)
    *   [5.14 Frecuencia de refresco no detectada correctamente por los servicios dependientes de XRandR](#Frecuencia_de_refresco_no_detectada_correctamente_por_los_servicios_dependientes_de_XRandR)
    *   [5.15 No se encuentran pantallas en un ordenador portátil/NVIDIA Optimus](#No_se_encuentran_pantallas_en_un_ordenador_port.C3.A1til.2FNVIDIA_Optimus)
        *   [5.15.1 Posible Solución](#Posible_Soluci.C3.B3n)
    *   [5.16 Pantalla(s) encontrada, pero ninguna configuración utilizable](#Pantalla.28s.29_encontrada.2C_pero_ninguna_configuraci.C3.B3n_utilizable)
    *   [5.17 Sin control de brillo en los portátiles](#Sin_control_de_brillo_en_los_port.C3.A1tiles)
    *   [5.18 Barras negras durante la reproducción a pantalla completa de videos flash con la configuración TwinView](#Barras_negras_durante_la_reproducci.C3.B3n_a_pantalla_completa_de_videos_flash_con_la_configuraci.C3.B3n_TwinView)
    *   [5.19 La retroiluminación no se apaga en algunas ocasiones](#La_retroiluminaci.C3.B3n_no_se_apaga_en_algunas_ocasiones)
    *   [5.20 Tinte azul en vídeos con Flash](#Tinte_azul_en_v.C3.ADdeos_con_Flash)
    *   [5.21 Bleeding Overlay con Flash](#Bleeding_Overlay_con_Flash)
    *   [5.22 Congelación completa del sistema utilizando Flash](#Congelaci.C3.B3n_completa_del_sistema_utilizando_Flash)
    *   [5.23 Xorg falla al cargarse o aparece una pantalla roja](#Xorg_falla_al_cargarse_o_aparece_una_pantalla_roja)
    *   [5.24 Pantalla en negro en sistemas con GPU integrada de Intel](#Pantalla_en_negro_en_sistemas_con_GPU_integrada_de_Intel)
    *   [5.25 Pantalla en negro en sistemas con GPU VIA integrada](#Pantalla_en_negro_en_sistemas_con_GPU_VIA_integrada)
    *   [5.26 X falla lanzando «no screens found» con una Intel iGPU](#X_falla_lanzando_.C2.ABno_screens_found.C2.BB_con_una_Intel_iGPU)
*   [6 Véase también](#V.C3.A9ase_tambi.C3.A9n)

## Instalación

Estas instrucciones son para aquellos que utilizan el paquete stock [linux](https://www.archlinux.org/packages/?name=linux). Para la configuración de kernel personalizado, vaya a la [sección correspondiente](#Instalaci.C3.B3n_alternativa:_kernel_personalizado).

**Sugerencia:** Por lo general es ventajoso instalar el controlador NVIDIA a través de [pacman](/index.php/Pacman_(Espa%C3%B1ol) "Pacman (Español)") en lugar del paquete proporcionado por el sitio web de NVIDIA, dado que permite asegurarse que el controlador se actualice conforme se vaya actualizando el sistema.

1\. Si no sabe qué tarjeta gráfica tiene, puede conocerla mediante la emisión de la siguiente orden:

	 `# lspci -k | grep -A 2 -i "VGA"` 

2\. Instale el controlador apropiado para su tarjeta:

*   Para las tarjetas de la serie GeForce 8 y posteriores [NVC0 y posteriores], instale el paquete [nvidia](https://www.archlinux.org/packages/?name=nvidia), disponible en los [repositorios oficiales](/index.php/Official_repositories_(Espa%C3%B1ol) "Official repositories (Español)").
*   Para las tarjetas de las series GeForce 6/7 [NV40-FANV], instale el paquete [nvidia-304xx](https://www.archlinux.org/packages/?name=nvidia-304xx), disponible en los [repositorios oficiales](/index.php/Official_repositories_(Espa%C3%B1ol) "Official repositories (Español)").
*   Para las tarjetas de la serie GeForce 5 FX [NV30-NV38], instale el paquete [nvidia-173xx](https://aur.archlinux.org/packages/nvidia-173xx/), disponible en [AUR](/index.php/Arch_User_Repository_(Espa%C3%B1ol) "Arch User Repository (Español)").
*   Para las tarjetas de las series 2/3/4 MX/Ti [NV11 y NV17-NV28], instale el paquete [nvidia-96xx](https://aur.archlinux.org/packages/nvidia-96xx/), disponible en [AUR](/index.php/Arch_User_Repository_(Espa%C3%B1ol) "Arch User Repository (Español)").

**Sugerencia:** Si no está seguro, consulte [driver download site](http://www.nvidia.com/Download/index.aspx) de NVIDIA para conocer el controlador apropiado para una tarjeta determinada. También puede comprobar la [lista de tarjetas legacy](http://www.nvidia.com/object/IO_32667.html) y la página [nouveau wiki's code names](http://nouveau.freedesktop.org/wiki/CodeNames).

	Para los modelos más recientes de GPU, puede ser necesario instalar [nvidia-beta](https://aur.archlinux.org/packages/nvidia-beta/) desde [AUR](/index.php/Arch_User_Repository_(Espa%C3%B1ol) "Arch User Repository (Español)"), ya que los controladores estables pueden no admitir las funciones mas recientemente introducidas.

	Si está en un sistema 64 bits y necesita soporte OpenGL de 32 bits, también puede instalar el paquete *lib32* equivalente disponible en el repositorio [multilib](/index.php/Multilib "Multilib") (por ejemplo [lib32-nvidia-libgl](https://www.archlinux.org/packages/?name=lib32-nvidia-libgl) o *lib32-nvidia-{304xx,173xx}-utils*).

**Sugerencia:** Los controladores nvidia-96xx y nvidia-173xx antiguos también pueden ser instalados desde el [repositorio [city]](http://pkgbuild.com/~bgyorgy/city.html) no oficial.

3\. Reinicie. El paquete [nvidia](https://www.archlinux.org/packages/?name=nvidia) contiene un archivo que introduce en blacklist al módulo *nouveau*, por lo que es necesario reiniciar.

Una vez que el controlador ha sido instalado, proceda a su [configuración](#Configuraci.C3.B3n).

### Instalación alternativa: kernel personalizado

En primer lugar, es bueno saber cómo funciona el sistema ABS mediante la lectura de algunos de los artículos acerca de él:

*   Artículo principal de [ABS](/index.php/Arch_Build_System_(Espa%C3%B1ol) "Arch Build System (Español)")
*   Artículo sobre [makepkg](/index.php/Makepkg "Makepkg")
*   Artículo sobre [creación de paquetes](/index.php/Creating_packages "Creating packages")

**Nota:** Usted también puede encontrar el paquete [nvidia-all](https://aur.archlinux.org/packages/nvidia-all/) en [AUR](/index.php/Arch_User_Repository_(Espa%C3%B1ol) "Arch User Repository (Español)"), que hace que sea más fácil de usar con kernels personalizados y/o múltiples

Lo que sigue es un breve tutorial para crear un paquete personalizado de controladores NVIDIA usando [ABS](/index.php/Arch_Build_System_(Espa%C3%B1ol) "Arch Build System (Español)"):

[Instale](/index.php/Pacman_(Espa%C3%B1ol) "Pacman (Español)") el paquete [abs](https://www.archlinux.org/packages/?name=abs) desde los [repositorios oficiales](/index.php/Official_repositories_(Espa%C3%B1ol) "Official repositories (Español)") y genere el árbol con:

```
# abs

```

Como usuario normal (sin privilegios), cree un directorio temporal para crear el nuevo paquete:

```
$ mkdir -p ~/abs

```

Haga una copia del paquete `nvidia` al directorio:

```
$ cp -r /var/abs/extra/nvidia/ ~/abs/

```

Entre en el directorio de compilación temporal `nvidia` :

```
$ cd ~/abs/nvidia

```

Ahora es necesario modificar los archivos `nvidia.install` y `PKGBUILD` de modo que contengan las variables correctas de la versión del kernel.

Ejecutando el kernel personalizado, se obtine el kernel apropiado y los nombres de la versión local:

```
$ uname -r

```

1.  Edite el archivo `nvidia.install` y reemplace la variable `EXTRAMODULES='extramodules-3.4-ARCH'` con la versión de kernel personalizado, como `EXTRAMODULES='extramodules-3.4.4'` o `EXTRAMODULES='extramodules-3.4.4-custom'` dependiendo de la versión del kernel y el texto/número de la versión local. Repita esta operación en todas las apariciones del número de versión en este archivo.
2.  En el archivo `PKGBUILD` cambie la variable `_extramodules=extramodules-3.4-ARCH` para que coincida con la versión adecuada, como antes.
3.  Si hay más de un kernel en el sistema instalado en paralelo (como un kernel personalizado junto con el kernel por defecto de ARCH), cambie la variable `pkgname=nvidia` en el archivo PKGBUILD a un nuevo identificador único, como nvidia-344 ó nvidia-custom. Esto permitirá que los dos kernels puedan utilizar el módulo nvidia, ya que el paquete del módulo personalizado tendrá un nombre diferente y no sobreescribirá el original. Usted también tendrá que comentar la línea en `package()` que introduce en blacklist el módulo nvidia en `/usr/lib/modprobe.d/nvidia.conf` (no es necesario volver a hacerlo) .

Luego haga:

```
$ makepkg -ci

```

La variable `-c` ordena a makepkg que limpie los archivos sobrantes del proceso de empaquetado después de la creación del paquete, mientras que `-i` especifica a makepkg que ejecute automáticamente pacman para instalar el paquete resultante.

### Recompilación automatica del modulo NVIDIA para cada actualización en cualquier kernel

Esto es posible gracias al paquete [nvidia-hook](https://aur.archlinux.org/packages/nvidia-hook/) de [AUR](/index.php/Arch_User_Repository_(Espa%C3%B1ol) "Arch User Repository (Español)"). Será necesario instalar las fuentes del modulo: [nvidia-source](https://aur.archlinux.org/packages/nvidia-source/). Con **nvidia-hook**, la funcionalidad para la «recompilación automática» se consigue mediante un **hook de nvidia** en [mkinitcpio](/index.php/Mkinitcpio_(Espa%C3%B1ol) "Mkinitcpio (Español)") después de haber forzado la actualización del paquete **linux-headers**. Será necesario añadir `nvidia` a la matriz HOOK en `/etc/mkinitcpio.conf`.

El hook invocará la orden **dkms** para actualizar el módulo NVIDIA a la versión del nuevo kernel .

**Nota:**

*   Si se utiliza esta funcionalidad es **importante** comprobar la salida del proceso de instalación del paquete de linux (o cualquier otro kernel). El hook nvidia señalará cualquier cosa que ande mal.
*   Si desea hacer esto manualmente, consulte [esta sección](/index.php/Dynamic_Kernel_Module_Support#Usage "Dynamic Kernel Module Support") de la wiki de arch sobre dkms.

## Configuración

Es posible que después de instalar el controlador no sea necesario crear un archivo de configuración para el servidor Xorg. Puede realizar [una prueba](/index.php/Xorg#Running "Xorg") para ver si el servidor Xorg funcionará correctamente sin un archivo de configuración. Sin embargo, aún funcionando correctamente, todavía puede ser útil crear un archivo de configuración `/etc/X11/xorg.conf` con el fin de realizar diversos ajustes. Esta configuración puede ser generada por la herramienta de configuración Xorg NVIDIA, o puede ser creado manualmente. Si la crea manualmente, puede consistir en una configuración mínima (en el sentido de que solo suministrarán las opciones básicas para el servidor [Xorg](/index.php/Xorg_(Espa%C3%B1ol) "Xorg (Español)")), o puede incluir una [serie de ajustes](/index.php/Xorg_(Espa%C3%B1ol)#Configuraci.C3.B3n_manual "Xorg (Español)") más detallados que pueden puentear las opciones preconfiguradas del controlador o las propias de Xorg.

**Nota:** Desde la versión 1.8.x Xorg utiliza archivos de configuración separados ubicados en `/etc/X11/xorg.conf.d /` - consulte la sección [configuración avanzada](#Avanzado:_20-nvidia.conf).

### Configuración mínima

Un archivo de configuración `20-nvidia.conf` básico (o en el desusado `xorg.conf`) podría ser similar a este:

 `/etc/X11/xorg.conf.d/20-nvidia.conf` 
```
Section "Device"
        Identifier "Nvidia Card"
        Driver "nvidia"
        VendorName "NVIDIA Corporation"
        Option "NoLogo" "true"
        #Option "UseEDID" "false"
        #Option "ConnectedMonitor" "DFP"
        # ...
EndSection

```

**Sugerencia:** Si está actualizando a nvidia después de haber utilizado el controlador nouveau, asegúrese de eliminar «`nouveau`» del archivo `/etc/mkinitcpio.conf`. Consulte cómo [cambiar entre los controladores nvidia y nouveau](#Cambiar_entre_los_controladores_NVIDIA_y_nouveau), si desea cambiar entre los controladores abiertos y propietarios.

### Configuración automática

El paquete NVIDIA incluye una herramienta de configuración automática para crear un archivo de configuración (`xorg.conf`) para el servidor Xorg y se puede ejecutar a través de:

```
 # nvidia-xconfig

```

Esta orden buscará automáticamente y creará (o modificará, si ya existe) la configuración de `/etc/X11/xorg.conf` de acuerdo con el hardware instalado.

Si está presente la instancia de DRI, asegúrese de que está comentada:

```
 #    Load        "dri"

```

Revise su archivo `/etc/X11/xorg.conf` para asegurarse de que los valores predefinidos sobre **depth** (profundidad), **horizontal sync** (sincronización horizontal), **vertical refresh** (refresco vertical), y las **resoluciones del monitor** son aceptables por su hardware.

**Advertencia:** Este procedimiento puede no funcionar correctamente con Xorg-server 1.8

### Varios monitores

	*Consulte el artículo [Multihead](/index.php/Multihead "Multihead") para obtener información más general*

**Advertencia:** Desde agosto de 2013, Xinerama se rompe cuando se utiliza el controlador propietario de NVIDIA con las versiones superiores a 319\. Los usuarios que deseen utilizar Xinerama con el controlador de NVIDIA deben utilizar la versión 313 del controlador, que solo funciona con los kernels de Linux anteriores a la 3.10\. Véase [this thread](https://bbs.archlinux.org/viewtopic.php?id=163319) para obtener más información.

Para activar el soporte de pantalla dual, solo tiene que editar el archivo `/etc/X11/xorg.conf.d/10-monitor.conf` que se habrá creado previamente.

Por cada monitor físico, añadir una sección Monitor, Device y Screen, y luego una sección ServerLayout para su gestión. Tenga en cuenta que cuando Xinerama está activada, el controlador de NVIDIA desactiva automáticamente la propiedad de composición (compositing). Si usted desea disfrutar de esta propiedad, debe comentar la línea `Xinerama` en «`ServerLayout`» y utilizar, en su lugar, TwinView (ver más abajo).

 `/etc/X11/xorg.conf.d/10-monitor.conf` 
```
Section "ServerLayout"
    Identifier     "DualSreen"
    Screen       0 "Screen0"
    Screen       1 "Screen1" RightOf "Screen0" #Screen1 a la derecha de Screen0
    Option         "Xinerama" "1" #Para mover ventanas entre pantallas
EndSection

Section "Monitor"
    Identifier     "Monitor0"
    Option         "Enable"   "1"
EndSection

Section "Monitor"
    Identifier     "Monitor1"
    Option         "Enable"   "1"
EndSection

Section "Device"
    Identifier     "Device0"
    Driver         "nvidia"
    Screen         0
EndSection

Section "Device"
    Identifier     "Device1"
    Driver         "nvidia"
    Screen         1
EndSection

Section "Screen"
    Identifier     "Screen0"
    Device         "Device0"
    Monitor        "Monitor0"
    DefaultDepth    24
    Option         "TwinView"  "0"
    SubSection "Display"
        Depth       24
        Modes       "1280x800_75.00"
    EndSubSection
EndSection

Section "Screen"
    Identifier     "Screen1"
    Device         "Device1"
    Monitor        "Monitor1"
    DefaultDepth   24
    Option         "TwinView"  "0"
    SubSection "Display"
        Depth      24
    EndSubSection
EndSection

```

#### TwinView

Si usted quiere solo una pantalla grande en vez de dos. Ajuste la opción `TwinView` a `1`. Esta opción debe ser utilizada en lugar de Xinerama (ver arriba), si desea la composición (compositing).

```
Option "TwinView" "1"

```

TwinView solo funciona sobre una tarjeta de base: Si tiene varias tarjetas (¿y no SLI?), usted tendrá que usar xinerama o la modalidad zaphod (múltiples pantallas en X). Se pueden combinar TwinView con el modo zaphod, por ejemplo, con dos pantallas X que cubren dos monitores cada uno. La mayoría de los gestores de ventanas fallan miserablemente en modo zaphod. La excepción brillante es Awesome. En algunos casos, también funciona con KDE.

Ejemplo de configuración:

 `/etc/X11/xorg.conf.d/10-monitor.conf` 
```
Section "ServerLayout"
    Identifier     "TwinLayout"
    Screen         0 "metaScreen" 0 0
EndSection

Section "Monitor"
    Identifier     "Monitor0"
    Option         "Enable"   "1"
EndSection

Section "Monitor"
    Identifier     "Monitor1"
    Option         "Enable"   "1"
EndSection

Section "Device"
    Identifier     "Card0"
    Driver         "nvidia"
    VendorName     "NVIDIA Corporation"

    #consulte el enlace de abajo para obtener más información sobre cada una de las siguientes opciones.
    Option         "HorizSync"           "DFP-0: 28-33; DFP-1 28-33"
    Option         "VertRefresh"         "DFP-0: 43-73; DFP-1 43-73"
    Option         "MetaModes"           "1920x1080, 1920x1080"
    Option         "ConnectedMonitor"    "DFP-0, DFP-1"
    Option         "MetaModeOrientation" "DFP-1 LeftOf DFP-0"
EndSection

Section "Screen"
    Identifier     "metaScreen"
    Device         "Card0"
    Monitor        "Monitor0"
    DefaultDepth    24
    Option         "TwinView"   "1"
    SubSection "Display"
        Modes      "1920x1080"
    EndSubSection
EndSection

```

[Información sobre las opciones para usar en Device](http://us.download.nvidia.com/XFree86/Linux-x86/304.22/README/configtwinview.html)

Si tiene varias tarjetas con capacidad SLI, es posible ejecutar más de un monitor conectado a las tarjetas separadas (por ejemplo: dos tarjetas en SLI con un monitor conectado a cada una). La opción «MetaModes» junto con el modo mosaico SLI permite esto. A continuación se muestra una configuración que funciona para el ejemplo anterior y corre con [GNOME](/index.php/GNOME_(Espa%C3%B1ol) "GNOME (Español)") sin problemas.

 `/etc/X11/xorg.conf.d/10-monitor.conf` 
```
Section "Device"
        Identifier      "Card A"
        Driver          "nvidia"
        BusID           "PCI:1:00:0"
EndSection

Section "Device"
        Identifier      "Card B"
        Driver          "nvidia"
        BusID           "PCI:2:00:0"
EndSection

Section "Monitor"
        Identifier      "Right Monitor"
EndSection

Section "Monitor"
        Identifier      "Left Monitor"
EndSection

Section "Screen"
        Identifier      "Right Screen"
        Device          "Card A"
        Monitor         "Right Monitor"
        DefaultDepth    24
        Option          "SLI" "Mosaic"
        Option          "Stereo" "0"
        Option          "BaseMosaic" "True"
        Option          "MetaModes" "GPU-0.DFP-0: 1920x1200+4480+0, GPU-1.DFP-0:1920x1200+0+0"
        SubSection      "Display"
                        Depth           24
        EndSubSection
EndSection

Section "Screen"
        Identifier      "Left Screen"
        Device          "Card B"
        Monitor         "Left Monitor"
        DefaultDepth    24
        Option          "SLI" "Mosaic"
        Option          "Stereo" "0"
        Option          "BaseMosaic" "True"
        Option          "MetaModes" "GPU-0.DFP-0: 1920x1200+4480+0, GPU-1.DFP-0:1920x1200+0+0"
        SubSection      "Display"
                        Depth           24
        EndSubSection
EndSection

Section "ServerLayout"
        Identifier      "Default"
        Screen 0        "Right Screen" 0 0
        Option          "Xinerama" "0"
EndSection
```

##### Configuración manual de CLI con xrandr

Si las últimas soluciones no funcionan para usted, puede usar la baza *autostart* de su gestor de ventanas para ejecutar una orden:

```
xrandr --output DVI-I-0 --auto --primary --left-of DVI-I-1

```

o

```
xrandr --output DVI-I-1 --pos 1440x0 --mode 1440x900 --rate 75.0

```

donde:

*   `--output` sirve para indicar a cuál «monitor» establecer las opciones.
*   `DVI-I-1` es el nombre del segundo monitor.
*   `--pos` es la posición del segundo monitor respecto al primero.
*   `--mode` es la resolución del segundo monitor.
*   `--rate` establece la frecuencia de refresco en Hz.

Es necesario adaptar esta cadena con opciones de `xrandr` con la ayuda de la salida generada por la orden `xrandr` ejecutado en un terminal.

#### Utilizar NVIDIA Settings

También puede utilizar la herramienta `nvidia-settings` proporcionada por [nvidia-utils](https://www.archlinux.org/packages/?name=nvidia-utils). Con este método, se utiliza el software propietario NVIDIA puesto a diposición de sus controladores. Basta con ejecutar `nvidia-settings` como root, a continuación, configurar como se desee, y luego guardar la configuración en `/etc/X11/xorg.conf.d/10-monitor.conf`.

#### ConnectedMonitor

Si el controlador no detecta correctamente un segundo monitor, se puede forzar a que lo haga con ConnectedMonitor.

 `/etc/X11/xorg.conf` 
```

Section "Monitor"
    Identifier     "Monitor1"
    VendorName     "Panasonic"
    ModelName      "Panasonic MICRON 2100Ex"
    HorizSync       30.0 - 121.0 # este monitor dispone de EDID incorrecto, por lo tanto, se usa Option "UseEdidFreqs" "false"
    VertRefresh     50.0 - 160.0
    Option         "DPMS"
EndSection

Section "Monitor"
    Identifier     "Monitor2"
    VendorName     "Gateway"
    ModelName      "GatewayVX1120"
    HorizSync       30.0 - 121.0
    VertRefresh     50.0 - 160.0
    Option         "DPMS"
EndSection

Section "Device"
    Identifier     "Device1"
    Driver         "nvidia"
    Option         "NoLogo"
    Option         "UseEDIDFreqs" "false"
    Option         "ConnectedMonitor" "CRT,CRT"
    VendorName     "NVIDIA Corporation"
    BoardName      "GeForce 6200 LE"
    BusID          "PCI:3:0:0"
    Screen          0
EndSection

Section "Device"
    Identifier     "Device2"
    Driver         "nvidia"
    Option         "NoLogo"
    Option         "UseEDIDFreqs" "false"
    Option         "ConnectedMonitor" "CRT,CRT"
    VendorName     "NVIDIA Corporation"
    BoardName      "GeForce 6200 LE"
    BusID          "PCI:3:0:0"
    Screen          1
EndSection

```

La sección duplicada de "Device" con `Screen` es la forma de obtener X para usar dos monitores en una sola tarjeta sin utilizar `TwinView`. Tenga en cuenta que `nvidia-settings` elimina todas las opciones `ConnectedMonitor` que haya añadido.

#### Modo mosaic

El modo mosaic es la única forma de utilizar más de 2 monitores a través de varias tarjetas gráficas con la composición. Su gestor de ventanas puede o no reconocer la diferencia entre cada monitor.

##### Mosaic básico

El modo básico mosaic funciona en cualquier configuración de GPU de la serie GeForce 8000 o superior. No se puede activar desde la GUI nvidia-setting. Se debe utilizar el programa nvidia-xconfig en línea de órdenes o editar xorg.conf manualmente. MetaModes debe ser especificado. El siguiente es un ejemplo para cuatro DFP en una configuración de 2x2, cada uno funcionando a 1920x1024, con dos pantallas digitales planas conectadas a dos tarjetas:

```
$ nvidia-xconfig --base-mosaic --metamodes="GPU-0.DFP-0: 1920x1024+0+0, GPU-0.DFP-1: 1920x1024+1920+0, GPU-1.DFP-0: 1920x1024+0+1024, GPU-1.DFP-1: 1920x1024+1920+1024"

```

##### Mosaic SLI

Si tiene una configuración SLI en combinación con una GPU Quadro FX 5800, Quadro Fermi o posterior, puede utilizar el modo Mosaic SLI. Se puede activar desde dentro de la interfaz gráfica nvidia-settings o desde la línea de órdenes con:

```
$ nvidia-xconfig --sli=Mosaic --metamodes="GPU-0.DFP-0: 1920x1024+0+0, GPU-0.DFP-1: 1920x1024+1920+0, GPU-1.DFP-0: 1920x1024+0+1024, GPU-1.DFP-1: 1920x1024+1920+1024"

```

## Optimización

### GUI: nvidia-settings

El paquete NVIDIA incluye el programa `nvidia-settings` con el que se permite ajustar varias opciones adicionales.

Para cargar los ajustes al iniciar sesión, ejecute esta orden en el terminal:

```
$ nvidia-settings --load-config-only

```

O lo añade al método de auto arranque del propio entorno de escritorio.

Para un aumento considerable de rendimiento de los gráficos 2D en aplicaciones que explotan en modo intensivo el pixmap, por ejemplo, Firefox, establezca el parámetro `InitialPixmapPlacement` a `2`:

```
 $ nvidia-settings -a InitialPixmapPlacement=2

```

Esto está documentado en el [código fuente de nvidia-settings](http://cgit.freedesktop.org/~aplattner/nvidia-settings/tree/src/libXNVCtrl/NVCtrl.h?id=b27db3d10d58b821e87fbe3f46166e02dc589855#n2797). Para que este ajuste permanezca, la anterior orden debe ser lanzada en cada arranque. Puede añadirlo al archivo ~/.xinitrc para iniciarlo automáticamente con X.

**Sugerencia:** Es raro, pero en ocasiones el archivo `~/.nvidia-settings-rc` puede resultar corrupto. Si esto ocurre, el servidor Xorg puede bloquearse y el archivo tendrá que ser eliminado para solucionar el problema.

### Activar MSI (Message Signaled Interrupts)

Por defecto, la tarjeta gráfica utiliza un sistema de interrupción compartida. Para dar un pequeño aumento de rendimiento, edite `/etc/modprobe.d/modprobe.conf` y añada:

```
options nvidia NVreg_EnableMSI=1

```

¡Tenga cuidado, ya que esto se ha reportado como dañoso para algunos sistemas con hardware antiguo!

Para confirmarlo, ejecute:

```
# cat /proc/interrupts | grep nvidia
  43:          0         49       4199      86318   PCI-MSI-edge      nvidia

```

### Avanzado: 20-nvidia.conf

Edite el archivo `/etc/X11/xorg.conf.d/20-nvidia.conf`, y añada las opciones a la sección correcta. El servidor Xorg tendrá que ser reiniciado para que los cambios se apliquen.

*   Consulte [NVIDIA Accelerated Linux Graphics Driver README y la Guía de Instalación](http://us.download.nvidia.com/XFree86/Linux-x86_64/256.53/README/index.html) para más detalles y opciones de configuración.

#### Activar desktop composition

A partir de la versión 180.44 del controlador NVIDIA, el apoyo a GLX con Damage y las extensiones Composite X están habilitadas de forma predeterminada. Consulte [Composite](/index.php/Composite "Composite") para obtener instrucciones detalladas.

#### Desactivar la aparición del logo al iniciar

Agregue la opción `"NoLogo"` en la sección `Device`:

```
Option "NoLogo" "1"

```

#### Activar aceleración por hardware

**Nota:** RenderAccel está activado por defecto desde la versión 97.46.xx del controlador

Agregue la opción `"RenderAccel"` en la sección `Device`:

```
Option "RenderAccel" "1"

```

#### Omitir la detección de monitor

La opciónn `"ConnectedMonitor"` en la sección `Device` permite anular la detección del monitor cuando el servidor X se inicia, lo que puede ahorrar una cantidad significativa de tiempo en el arranque. Las opciones disponibles son: `"CRT"` para las conexiones analógicas, `"DFP"` para monitores digitales y `"TV"` para televisores.

La siguiente declaración fuerza al controlador NVIDIA a omitir las comprobaciones del arranque y a reconocer el monitor como DFP:

```
Option "ConnectedMonitor" "DFP"

```

**Nota:** Se usa "CRT" para todas las conexiones analógicas de 15 pin VGA, aunque el monitor sea una pantalla plana. "DFP" está diseñado para conexiones DVI digitales.

#### Activar el triple buffering

Para activar el uso de triple buffering se añade la opción`"TripleBuffer"` en la sección `Device`:

```
Option "TripleBuffer" "1"

```

Utilice esta opción si la tarjeta gráfica tiene suficiente memoria RAM (igual o superior a 128 MB). El ajuste solo tiene efecto cuando la sincronización para VBLANK, una de las opciones que aparecen en nvidia-settings (`syncing to vblank`), está habilitada.

**Nota:** Esta opción puede producir problemas de visualización en pantalla completa. A partir de los controladores R300, VBLANK está activado por defecto.

#### Usar los eventos del sistema

Tomado del archivo [LÉAME](http://http.download.nvidia.com/XFree86/Linux-x86/1.0-7182/README/readme.txt) del controlador de NVIDIA: *«[...] el uso de los eventos del sistema permite notificar eficientemente a X cuando un cliente ha realizado el direct rendering sobre una ventana que tiene que ser compuesta».* Cualquier cosa identificada, puede ayudar a mejorar el rendimiento, pero esta opción, por el momento, es incompatible con la tecnología SLI y multi-GPU.

Añadir en la sección `Device`:

```
Option "DamageEvents" "1"

```

**Nota:** Esta opción está activada por defecto en las versiones más recientes del controlador.

#### Activar el ahorro de energía

Añadir en la sección `Monitor`:

```
 Option "DPMS" "1"

```

#### Activar el control del brillo

Añadir en la sección `Device`:

```
Option "RegistryDwords" "EnableBrightnessControl=1"

```

**Nota:** Si ya tiene activada esta opción y el control de brillo no funciona pruebe comentandola.

#### Activar la modalidad SLI

**Advertencia:** Desde el 7 de mayo del 2011, se puede experimentar un rendimiento de vídeo lento en GNOME 3 después de activar SLI.

Tomado del apendice de [README](http://http.download.nvidia.com/XFree86/Linux-x86/1.0-8774/README/appendix-d.html) del controlador de Nvidia: *Esta opción controla la configuración SLI del renderizado en configuraciones compatibles.* Una *configuración compatible* es un ordenador equipado con un placa base SLI-Certified y 2 ó 3 tarjetas de video SLI-Certified GeForce GPUs. Consulte NVIDIA [Zona SLI](http://www.slizone.com/page/home.html) para obtener más información.

En primer lugar identifique el PCI Bus ID de la GPU utilizando `lspci`:

 `$ lspci | grep VGA` 
```
03:00.0 VGA compatible controller: nVidia Corporation G92 [GeForce 8800 GTS 512] (rev a2)
05:00.0 VGA compatible controller: nVidia Corporation G92 [GeForce 8800 GTS 512] (rev a2)

```

Agregue el BusID (3 en el ejemplo anterior) en la sección `Device`:

```
BusID "PCI:3:0:0"

```

**Nota:** El formato es importante. El valor BusID debe especificarse como `"PCI:*BusID*:0:0"`

Añadir el valor deseado para la modalidad de renderizado SLI a utilizar en la sección `Screen`:

```
Option "SLI" "SLIAA"

```

En la siguiente tabla se presentan los modos de renderizados disponibles.

| Valor | Comportamiento |
| 0, no, off, false, Single | Usa únicamente una sola GPU para el renderizado. |
| 1, yes, on, true, Auto | Habilita SLI y permite al controlador seleccionar automáticamente el modo de renderizado adecuado. |
| AFR | Habilita SLI y utiliza un modo de renderizado con fotograma alternativo. |
| SFR | Habilita SLI y utiliza un modo de renderizado con fotograma "dividido". |
| SLIAA | Habilita SLI y utiliza también SLI antialiasing. Utilice esta función junto con la modalidad anti-aliasing para mejorar la calidad visual. |

Como alternativa, puede usar la utilidad `nvidia-xconfig` para insertar estos cambios directamente en el archivo `xorg.conf` con una sola orden:

```
# nvidia-xconfig --busid=PCI:3:0:0 --sli=SLIAA

```

Para comprobar que el modo SLI está habilitado, escriba en un terminal:

 `$ nvidia-settings -q all | grep SLIMode` 
```
  Attribute 'SLIMode' (arch:0.0): AA 
    'SLIMode' is a string attribute.
    'SLIMode' is a read-only attribute.
    'SLIMode' can use the following target types: X Screen.

```

**Advertencia:** Después de activar SLI el sistema puede quedar congelado/no responder al arrancar xorg. Es recomendable que desactive el gestor de pantalla antes de reiniciar.

#### Forzar el nivel de rendimiento Powermizer (para portátiles)

Añada en la sección `Device`:

```
# Forzar Powermizer a un cierto nivel en todo momento:
# level 0x1=highest
# level 0x2=med
# level 0x3=lowest

# Ajustes de AC (corriente alterna):
Option "RegistryDwords" "PowerMizerLevelAC=0x3"
# Ajustes de batería:
Option	"RegistryDwords" "PowerMizerLevel=0x3"

```

##### Dejar que la GPU establezca su propio nivel de rendimiento basado en la temperatura

Añada en la sección `Device`:

```
 Option "RegistryDwords" "PerfLevelSrc=0x3333"

```

#### Desactivar vblank interrupts (para portátiles)

Cuando la utilidad de reconocimiento de interrupciones [powertop](/index.php/Powertop "Powertop") está activa, se puede observar que el controlador de Nvidia va a generar una interrupción por cada VBLANK. Para evitar este inconveniente, añada la siguiente línea en la sección `Device`:

```
 Option    "OnDemandVBlankInterrupts" "1"

```

Esto reducirá las interrupciones a aproximadamente una o dos por segundo.

#### Activar overclocking

**Advertencia:** Tenga en cuenta que el overclocking puede dañar el hardware y que ninguna responsabilidad puede ser trasladada a los autores de esta página por los posibles daños reportados por la instrumentalización del hardware modificado para funcionar de manera diferente de las especificaciones técnicas de fábrica.

Para activar overclocking (aceleración de la GPU y la memoria), coloque la línea siguiente en la sección `Device`:

```
 Option         "Coolbits" "1"

```

Esta modificación permitirá la gestión de overclocking en una sesión de X ejecutando:

```
  $ nvidia-settings

```

**Nota:** Las tarjetas nvidia de la serie GTX 4xx/5xx que utilizan el núcleo "Fermi" no soportan actualmente el método 'Coolbits' para overclocking. Una alternativa es flashear y modificar la BIOS de la GPU ya sea bajo DOS (preferido), o dentro de un entorno Win32 mediante [nvflash](http://www.mvktech.net/component/option,com_remository/Itemid,26/func,select/id,127/orderby,2/page,1/) y [NiBiTor 6.0](http://www.mvktech.net/component/option,com_remository/Itemid,26/func,select/id,135/orderby,2/page,1/). La ventaja de hacer un flash de la BIOS es que no solo puede verse aumentado el límite de voltaje, sino que la estabilidad se mejora generalmente en comparación con los métodos de overclocking software tales como Coolbits.

##### Configurar un marcador estático 2D/3D

Establezca la siguiente línea en la sección `Device` para ajustar el sistema PowerMizer en su máximo nivel de rendimiento:

```
  Option "RegistryDwords" "PerfLevelSrc=0x2222"

```

Establezca una de las dos líneas siguientes en la sección `Device` para permitir el control manual del ventilador de la GPU a través de `nvidia-settings`:

```
  Option "Coolbits" "4"

```

```
  Option "Coolbits" "5"

```

## Consejos y trucos

### Ajustar la resolución del terminal de inicio

La transición de nouveau puede causar al inicio una visualización del terminal en una resolución más baja. Una posible solución (si se está utilizando GRUB) consiste en editar la línea `GRUB_GFXMODE` en `/etc/default/grub` con la resolución de pantalla deseada. Es posible especificar varias resoluciones, incluyendo el parámetro por defecto `auto`, por lo que se recomienda que se modifique la línea para asemejarse a este ejemplo: `GRUB_GFXMODE=<resolución deseada>,<fallback como 1024x768>,auto`. Véase [http://www.gnu.org/software/grub/manual/html_node/gfxmode.html#gfxmode](http://www.gnu.org/software/grub/manual/html_node/gfxmode.html#gfxmode) para obtener más información.

### Activar Vídeo HD (VDPAU/VAAPI)

**Hardware requerido:**

Tener una tarjeta de vídeo que soporte, al menos, la segunda generación de PureVideo HD [wikipedia:PureVideo_HD#Table_of_PureVideo_.28HD.29_GPUs](https://en.wikipedia.org/wiki/PureVideo_HD#Table_of_PureVideo_.28HD.29_GPUs "wikipedia:PureVideo HD")

**Software requerido:**

Tarjetas de video NVIDIA con el controlador propietario instalado proporcionarán las capacidades de descodificación de vídeo con la interfaz VDPAU a niveles diferentes de acuerdo con la generación PureVideo.

También puede añadir soporte para la interfaz VA-API con [libva-vdpau-driver](https://www.archlinux.org/packages/?name=libva-vdpau-driver).

Compruebe la compatibilidad VA-API con:

```
 $ vainfo

```

Para aprovechar al máximo la capacidad de decodificación de hardware de la tarjeta de vídeo se necesita utilizar un reproductor multimedia que soporte VDPAU o VA-API.

Para activar la aceleración de hardware en [MPlayer](/index.php/MPlayer "MPlayer") edite `~/.mplayer/config`

```
 vo=vdpau
 vc=ffmpeg12vdpau, ffwmv3vdpau, ffvc1vdpau, ffh264vdpau, ffodivxvdpau,

```

**Advertencia:** El códec `ffodivxvdpau` solo es compatible con las series más reciente de hardware NVIDIA. Considere la posibilidad de omitirlo en función de su hardware específico.

Para activar la aceleración de hardware en [VLC](/index.php/VLC "VLC") ir a:

`**Tools** (**Herramientas**)` -> `**Preferences** (**Preferencias**)` -> `**Input & Codecs**` -> active `**Use GPU accelerated decoding**`

Para activar la aceleración de hardware en **smplayer** ir a:

`**Options** (**Opciones**)` -> `**Preferences** (**Preferencias**)` -> `**General**` -> `**Video Tab** (**Tarjeta Vídeo**)` -> seleccionar `vdpau` como `**output driver** (**salida del controlador**)`

Para activar la aceleración de hardware en **gnome-mplayer** ir a:

`**Edit** (**Editar**)` -> `**Preferences** (**Preferencias**)` -> ajustar `**video output**(**salida de video**)` en `vdpau`

**Reproducción de películas HD en tarjetas con poca memoria:**

Si su tarjeta gráfica no tiene mucha memoria (> 521MB?), puede experimentar problemas técnicos cuando se ven películas con una resolución de 1080p o 720p, incluso. Puede evitar esto con un administrador de inicio de sesión simple como TWM o MWM.

Además, el aumento de tamaño de la memoria caché de MPlayer editando el archivo `~/.mplayer /config` puede ayudar, cuando al visionar una película en HD decae la velocidad del disco duro.

### Decodificar aceleración de vídeo por hardware con XvMC

La codificación de la aceleración de vídeos MPEG-1 y MPEG-2 mediante [XvMC](/index.php/XvMC "XvMC") es compatible con las tarjetas series GeForce4, GeForce 5 FX, GeForce 6 y GeForce 7\. Para utilizarla, cree un nuevo archivo `/etc/X11/XvMCConfig` con el contenido siguiente:

```
libXvMCNVIDIA_dynamic.so.1

```

Consulte cómo configurar [software compatible](/index.php/XvMC#Supported_software "XvMC").

### Usar la salida de TV

Un buen artículo sobre el tema se puede encontrar [aquí](http://en.wikibooks.org/wiki/NVidia/TV-OUT)

### X con un televisor (DFP) como única pantalla

El servidor X se cambia a CRT-0 si no hay ningún monitor reconocido automáticamente. Esto puede ser un problema cuando se utiliza una TV conectada vía DVI como la pantalla principal, y el servidor X se inicia mientras el TV está apagada o desconectada de otra manera.

Para forzar al controlador nvidia a utilizar DFP, guarde una copia de la EDID en algún lugar del sistema de archivos para que X puede analizar el archivo en lugar de leer la EDID de la TV/DFP.

Para adquirir el EDID, inicie nvidia-settings. Se mostrará algo de información en estructura de árbol, ignore el resto de los ajustes por ahora y seleccione la GPU (la entrada correspondiente debería titularse "GPU-0" o similar), haga clic en la sección `DFP` (de nuevo, `DFP-0` o similar), haga clic sobre el botón `Adquirir Edid` y guárdelo en alguna parte, por ejemplo, `/etc/X11/dfp0.edid`.

Editar `xorg.conf` añadiendo a la sección `Device`:

```
 Option "ConnectedMonitor" "DFP"
 Option "CustomEDID" "DFP-0:/etc/X11/dfp0.edid"

```

La opción `ConnectedMonitor` obliga al controlador a reconocer el DFP como si estuviera conectado. La opción `CustomEDID` proporciona los datos EDID del dispositivo, lo que significa que se comportará como si el TV/DFP estuviese conectado durante el proceso de arranque de X.

De esta manera, uno puede comenzar automáticamente un administrador de sesión en el arranque y entonces tendrá una pantalla de X funcionando y configurada correctamente para el momento en que encienda el televisor.

### Comprobar el estado de energía

El controlador NVIDIA X.org puede detectar la fuente de alimentación. Para ver el estado actual, compruebe el parámetro de solo lectura 'GPUPowerSource' (0 - AC, 1 - battery):

 `$ nvidia-settings -q GPUPowerSource -t`  `1` 

Si aparece un mensaje de error similar al de abajo, entonces necesita tener instalado [acpid](/index.php/Acpid "Acpid") o iniciar el servicio systemd mediante `systemctl start acpid.service`

```
 ACPI: failed to connect to the ACPI event daemon; the daemon
 may not be running or the "AcpidSocketPath" X
 configuration option may not be set correctly. When the
 ACPI event daemon is available, the NVIDIA X driver will
 try to use it to receive ACPI event notifications. For
 details, please see the "ConnectToAcpid" and
 "AcpidSocketPath" X configuration options in Appendix B: X
 Config Options in the README.

```

(Si no está viendo este error, no es necesario instalar/ejecutar acpid únicamente para este propósito. Eso querrá decir que la fuente de alimentación actual estará correctamente informada sin acpid aún instalado.)

### Visualizar la temperatura de la GPU en la shell

#### Método 1 - nvidia-settings

**Nota:** Este método requiere el uso de una sesión X. No se requiere si, alternativamente, se usa el método 2 ó el método 3\. También tenga en cuenta que el método 3, de momento, no funciona con las nuevas tarjetas de NVIDIA como la G210/220 así como las integradas en la GPU como la Zotac IONITX's 8800GS.

Para mostrar la temperatura de la GPU en el shell, utilice `nvidia-settings` de la siguiente manera:

```
 $ nvidia-settings -q gpucoretemp

```

Lo que daría algo similar a lo siguiente:

```
 Attribute 'GPUCoreTemp' (hostname:0.0): 41.
 'GPUCoreTemp' is an integer attribute.
 'GPUCoreTemp' is a read-only attribute.
 'GPUCoreTemp' can use the following target types: X Screen, GPU.

```

Las temperaturas de la GPU de esta placa es de 41ºC.

Para conseguir solamente la temperatura para su uso en programas como `rrdtool` o `conky`, entre otros, usar la orden:

 `$ nvidia-settings -q gpucoretemp -t`  `41` 

#### Método 2 - nvidia-smi

Use nvidia-smi que puede leer directamente la temperatura de la GPU sin necesidad de utilizar X en absoluto. Esto es importante para un pequeño grupo de usuarios que no disponen de X, bien por que se trata de un servidor, bien por que no utilizan aplicaciones con interfaz gráficas. Para mostrar la temperatura de la GPU en el shell, utilice nvidia-smi como sigue:

```
 $ nvidia-smi

```

La orden debe generar una salida similar a lo siguiente:

 `$ nvidia-smi` 
```
Fri Jan  6 18:53:54 2012       
+------------------------------------------------------+                       
| NVIDIA-SMI 2.290.10   Driver Version: 290.10         |                       
|-------------------------------+----------------------+----------------------+
| Nb.  Name                     | Bus Id        Disp.  | Volatile ECC SB / DB |
| Fan   Temp   Power Usage /Cap | Memory Usage         | GPU Util. Compute M. |
|===============================+======================+======================|
| 0\.  GeForce 8500 GT           | 0000:01:00.0  N/A    |       N/A        N/A |
|  30%   62 C  N/A   N/A /  N/A |  17%   42MB /  255MB |  N/A      Default    |
|-------------------------------+----------------------+----------------------|
| Compute processes:                                               GPU Memory |
|  GPU  PID     Process name                                       Usage      |
|=============================================================================|
|  0\.           ERROR: Not Supported                                          |
+-----------------------------------------------------------------------------+

```

Para mostrar solo la temperatura:

 `$ nvidia-smi -q -d TEMPERATURE` 
```

==============NVSMI LOG==============

Timestamp                       : Fri Jan  6 18:50:57 2012

Driver Version                  : 290.10

Attached GPUs                   : 1

GPU 0000:01:00.0
    Temperature
        Gpu                     : 62 C

```

Con el fin de obtener tan solo el valor de la temperatura para su uso en programas como rrdtool o conky, entre otros, usar la orden:

 `$ nvidia-smi -q -d TEMPERATURE | grep Gpu | cut -c35-36`  `62` 

Referencia: [http://www.question-defense.com/2010/03/22/gpu-linux-shell-temp-get-nvidia-gpu-temperatures-via-linux-cli](http://www.question-defense.com/2010/03/22/gpu-linux-shell-temp-get-nvidia-gpu-temperatures-via-linux-cli)

#### Método 3 - nvclock

Utilice nvclock que está disponible en el repositorio [extra].

**Nota:** `nvclock` no puede acceder a los sensores térmicos en las nuevas tarjetas de NVIDIA como la G210/220

Puede haber diferencias significativas entre las temperaturas reportadas por nvclock y nvidia-settings/nv-control. Según [este post](http://sourceforge.net/projects/nvclock/forums/forum/67426/topic/1906899) del autor (thunderbird) de nvclock, los valores nvclock deberían ser más precisos.

### Ajustar la velocidad del ventilador en la sesión

Se puede ajustar la velocidad del ventilador de la tarjeta gráfica con la interfaz de usuario `nvidia-settings`. Primero, asegúrese de que la configuración Xorg establece la opción Coolbits a `4` ó `5` en la sección `Device` para permitir el control del ventilador.

```
 Option "Coolbits" "4"

```

**Nota:** Las tarjetas de la serie GTX 4xx/5xx actualmente no pueden establecer la velocidad del ventilador al iniciar la sesión utilizando este método. Este método solo permite el ajuste de la velocidad del ventilador dentro de la sesión X actual a través de nvidia-settings.

Coloque la línea siguiente en el archivo `~/.xinitrc` para ajustar la velocidad del ventilador al iniciar Xorg. Sustituya `*n*` con un valor porcentual relativo a la velocidad del ventilador que desea configurar.

```
 nvidia-settings -a "[gpu:0]/GPUFanControlState=1" -a "[fan:0]/GPUCurrentFanSpeed=*n*"

```

También puede configurar una segunda GPU mediante el incremento del número de la GPU y el número de ventiladores.

```
 nvidia-settings -a "[gpu:0]/GPUFanControlState=1" \ 
 -a "[gpu:1]/GPUFanControlState=1" \
 -a "[fan:0]/GPUCurrentFanSpeed=*n*" \
 -a  [fan:1]/GPUCurrentFanSpeed=*n*" &

```

Si utiliza un gestor de inicio de sesión, como GDM o KDM, puede crear un archivo .desktop para procesar este ajuste. Cree el archivo `~/.config/autostart/nvidia-fan-speed.desktop` y coloque el texto que sigue en su interior. Una vez más, sustituya `*n*` por el valor porcentual en base a su exigencia.

```
 [Desktop Entry]
 Type=Application
 Exec=nvidia-settings -a "[gpu:0]/GPUFanControlState=1" -a "[fan:0]/GPUCurrentFanSpeed=*n*"
 X-GNOME-Autostart-enabled=true
 Name=nvidia-fan-speed

```

### Orden de instalación/desinstalación para cambiar los controladores

Cuando el controlador antiguo de nvidia es nvidiaO y el nuevo es nvidiaN, el orden a seguir para sustituir uno por otro sería:

```
Eliminar nvidiaO
Instalar nvidia-utilsN
Instalar nvidiaN
Instalar lib32-nvidia-utils-N (si es necesario)

```

### Cambiar entre los controladores NVIDIA y nouveau

Si va a cambiar entre el controlador nvidia y el controlador nouveau con frecuencia, puede utilizar estos dos scripts para que sea más fácil (ambos tienen que ser lanzados como root):

```
 #!/bin/bash
 # nouveau -> nvidia

 set -e

 # check if root
 if [[ $EUID -ne 0 ]]; then
    echo "You must be root to run this script. Aborting...";
    exit 1;
 fi

 sed -i 's/MODULES="nouveau"/#MODULES="nouveau"/' /etc/mkinitcpio.conf

 pacman -Rdds --noconfirm nouveau-dri xf86-video-nouveau mesa-libgl #lib32-nouveau-dri lib32-mesa-libgl
 pacman -S --noconfirm nvidia #lib32-nvidia-libgl

 mkinitcpio -p linux

```

```
 #!/bin/bash
 # nvidia -> nouveau

 set -e

 # check if root
 if [[ $EUID -ne 0 ]]; then
    echo "You must be root to run this script. Aborting...";
    exit 1;
 fi

 sed -i 's/#*MODULES="nouveau"/MODULES="nouveau"/' /etc/mkinitcpio.conf

 pacman -Rdds --noconfirm nvidia #lib32-nvidia-libgl
 pacman -S --noconfirm nouveau-dri xf86-video-nouveau #lib32-nouveau-dri

 mkinitcpio -p linux

```

Es necesario reiniciar para completar los cambios.

Ajuste los scripts a sus propias necesidades, en el caso de que use otros controladores de NVIDIA (por ejemplo, nvidia-173xx).

Descomente los paquetes de lib32 si corre sobre un sistema de 64-bit y necesita las bibliotecas de 32-bit (por ejemplo juegos/Steam de 32-bit ).

## Solución de problemas

### Rendimiento bajo, por ejemplo, rediseño lento al cambiar las pestañas en Chrome

En algunas máquinas, los últimos controladores de nvidia introducen un bug (?) que provoca un reajuste del mapa de píxeles muy lento en X11\. El cambio de pestañas en Chrome/Chromium (si se mantienen abiertas más de 2 pestañas) toma 1-2 segundos, en lugar de unos pocos milisegundos.

Parece que la modificación de la variable **InitialPixmapPlacement** a **0** soluciona ese problema, aunque (como se describe en algunos párrafos más arriba) **InitialPixmapPlacement=2** en realidad debería ser el método más rápido.

La variable puede ser creada (temporalmente) con la orden:

```
 nvidia-settings -a InitialPixmapPlacement=0

```

Para hacerlo permanente, esta orden puede ser colocada en un script de arranque.

### Jugar usando Twinview

En caso de que quiera jugar a pantalla completa cuando se utiliza la opción TwinView, se dará cuenta de que los juegos reconocen las dos pantallas como si fuera una gran pantalla. Si bien esto es técnicamente correcto (la pantalla virtual de X es realmente el tamaño de sus dos pantallas combinadas), es probable que no quieren jugar en ambas pantallas al mismo tiempo.

Para corregir este comportamiento para SDL, intente:

```
 export SDL_VIDEO_FULLSCREEN_HEAD=1

```

Para OpenGL, añada las Metamodes apropiadas para su xorg.conf en la sección `Device` y reinicie X:

```
 Option "Metamodes" "1680x1050,1680x1050; 1280x1024,1280x1024; 1680x1050,NULL;  1280x1024,NULL;""

```

Otro método que puede funcionar ya sea solo o en combinación con los mencionados anteriormente consiste en el [starting games in a separate X server](/index.php/Gaming#Starting_games_in_a_separate_X_server "Gaming").

### Sincronización vertical usando TwinView

Si utiliza vertical sync (sincronización vertical) en combinación con TwinView (la opción "Sync to Vblank" en **nvidia-settings**), se dará cuenta de que solo una pantalla se sincroniza correctamente, a menos que tenga dos monitores idénticos. Aunque **nvidia-settings** ofrece una opción para permitir la sincronización al cambiar la pantalla (la opción "Sync to this display device"), esto no siempre funciona. Una solución es añadir las siguientes variables de entorno en la fase de arranque, por ejemplo anexarlo en `/etc/profile`:

```
  export __GL_SYNC_TO_VBLANK=1
  export __GL_SYNC_DISPLAY_DEVICE=DFP-0
  export __VDPAU_NVIDIA_SYNC_DISPLAY_DEVICE=DFP-0

```

Puede cambiar `DFP-0` con su pantalla preferida; (`DFP-0` indica el puerto DVI, mientras `CRT-0` es el puerto VGA).

### Antigua configuración de Xorg

Si está actualizando desde una instalación antigua, por favor, elimine las antiguas rutas `/usr/X11R6/`, ya que puede causar problemas durante la instalación.

### Pantalla corrupta: el problema de las «seis pantallas»

Para algunos usuarios que utilizan la tarjeta de vídeo Geforce GT 100M, la pantalla se vuelve corrupta después del inicio de X, dividida en 6 secciones con una resolución limitada a 640x480.

Para resolver este problema, habilite el Validation Mode `NoTotalSizeCheck` en la sección `Device`:

```
Section "Device"
 ...
 Option "ModeValidation" "NoTotalSizeCheck"
 ...
EndSection

```

### Error '/dev/nvidia0' Input/Output

Este error puede ocurrir por varias razones diferentes, y la solución más común para este error es comprobar los permisos del grupo/archivo, aunque en casi todos los casos *no* es la solución del problema. La documentación de NVIDIA no aborda en detalle sobre lo que debe hacerse para corregir este problema, pero hay algunas cosas que han funcionado para algunos usuarios. El problema puede ser un conflicto con el IRQ de otro dispositivo o enrutamiento mal asignado ya sea por el kernel o por la BIOS.

La primera cosa a intentar es quitar otros dispositivos de vídeo tales como tarjetas de captura de vídeo y ver si el problema desaparece. Si hay demasiados procesadores de video en el mismo sistema puede hacer que el kernel sea incapaz de arrancar, debido a problemas de asignación de memoria con el controlador de vídeo. En particular, en los sistemas con baja memoria de vídeo, esto puede suceder incluso si solo hay un procesador de vídeo. En tal caso, debe saber la cantidad de memoria de vídeo de su sistema (por ejemplo con la orden `lspci-v`) y pasar los parámetros de asignación al kernel, por ejemplo:

```
 vmalloc = 64M
 o
 vmalloc = 256M

```

Si se ejecuta un kernel de 64 bits, un defecto del controlador puede hacer que el módulo nvidia aborte la inicialización [IOMMU](https://en.wikipedia.org/wiki/IOMMU "wikipedia:IOMMU") cuando está encendido. Algunos usuarios han reportado que apagarlo en la BIOS puede ser la solución. [[1]](http://www.nvnews.net/vbulletin/showthread.php?s=68bb2fabadcb53b10b286aa42d13c5bc&t=159335)[User:Clickthem#nvidia module](/index.php/User:Clickthem#nvidia_module "User:Clickthem")

Otra cosa que puede probar es cambiar su BIOS IRQ routing de `Operating system controlled` en `BIOS controlled` o al revés. El primero de ellos se puede pasar como un parámetro del kernel:

```
 PCI=biosirq

```

El parámetro `noacpi` del kernel también se ha sugerido como una posible solución, pero, dado que desactiva ACPI por completo, debe utilizarse con precaución. Algunos dispositivos pueden ser fácilmente dañados por sobrecalentamiento.

**Nota:** Las opciones del kernel se pueden pasar a través de la línea de comandos del kernel o al archivo de configuración del gestor de arranque. Consulte la página Wiki sobre su gestor de arranque para más información.

### Errores '/dev/nvidiactl'

Al intentar iniciar una aplicación OpenGL podría dar lugar a errores tales como:

```
 Error: Could not open /dev/nvidiactl because the permissions are too
 restrictive. Please see the FREQUENTLY ASKED QUESTIONS 
 section of /usr/share/doc/NVIDIA_GLX-1.0/README 
 for steps to correct.

```

Se resuelve añadiendo el usuario apropiado al grupo `video` e iniciando de nuevo la sesión:

```
 # gpasswd -a username video

```

### Las aplicaciones de 32 bits no se inician

En sistemas de 64 bits, la instalación de `lib32-nvidia-utils`, que corresponde a la misma versión instalada para el controlador de 64 bits, soluciona el problema.

### Errores después de actualizar el kernel

Si se utiliza un módulo NVIDIA compilado en lugar del paquete proporcionado en [extra], se requiere una recompilación cada vez que se actualiza el kernel. Se recomienda reiniciar el sistema después de actualizar los controladores del kernel y el driver.

### Fallo general

*   Intente desactivando `RenderAccel` en `xorg.conf`.
*   Si Xorg genera un error de "conflicting memory type" o "failed to allocate primary buffer: out of memory", agregue `nopat` al final de la línea del `kernel` en `/boot/grub/menu.lst`.
*   Si el compilador NVIDIA se queja de las diferentes versiones de GCC entre el actual y el que se utiliza para compilar el kernel, añada en `/etc/profile`:

```
 export IGNORE_CC_MISMATCH=1

```

*   Si Xorg está fallando con un "Signal 11" al usar los controladores nvidia-96xx, intente desactivar PAT. Pase el argumento `nopat` a la línea del `kernel` en `menu.lst`.

Más información sobre solución de problemas del controlador se puede encontrar en los [NVIDIA forums.](http://www.nvnews.net/vbulletin/forumdisplay.php?s=&forumid=14)

### Inadecuado rendimiento después de instalar una nueva versión del controlador

Si FPS ha disminuido en comparación con los controladores anteriores, compruebe primero si el direct rendering está activado:

```
 $ glxinfo | grep direct

```

Si la orden reporta:

```
 direct rendering: No

```

esto, podría ser una indicación de la caída repentina del FPS.

Una posible solución podría ser la de volver a la versión del controlador instalado anteriormente y reiniciar después.

### Picos altos de la CPU con tarjetas de la serie 400

Si usted está experimentando picos intermitentes de CPU con una tarjeta de la serie 400, esto puede ser causado por PowerMizer que cambia constantemente la frecuencia del reloj de la GPU. Cambie la configuración de PowerMizer de **Adaptive** a **Performance**, agregando lo siguiente a la sección `Device` de la configuración de Xorg:

```
  Option "RegistryDwords" "PowerMizerEnable=0x1; PerfLevelSrc=0x3322; PowerMizerDefaultAC=0x1"

```

### Portátiles: X se bloquea al iniciar/cerrar sesión, obviado con Ctrl+Alt+Backspace

Si durante el uso de los controladores NVIDIA, Xorg se cuelga al inicio o cierre de sesión (en particular, con una pantalla extraña dividida en dos piezas en blanco y negro/gris), pero sigue siendo posible efectuar el registro o login a través de Ctrl-Alt-Backspace (o cualquiera que sea la nueva combinación de teclas para "kill X"), pruebe a añadir lo siguiente en `/etc/modprobe.d/modprobe.conf`:

```
 options nvidia NVreg_Mobile=1

```

Un usuario ha reportado solucionarlo con la orden descrita, pero hace que el rendimiento disminuya significativamente, por lo que se podría intentar lo siguiente:

```
 options nvidia NVreg_DeviceFileUID=0 NVreg_DeviceFileGID=33 NVreg_DeviceFileMode=0660 NVreg_SoftEDIDs=0 NVreg_Mobile=1

```

Tenga en cuenta que `NVreg_Mobile` necesita ser cambiado de acuerdo con el tipo de portátil:

*   1 para portátiles Dell.
*   2 para portátiles no Compal Toshiba.
*   3 para otros portátiles.
*   4 para portátiles Compal Toshiba.
*   5 para portátiles Gateway.

Consulte [Léame del controlador de NVIDIA:Apéndice K](http://http.download.nvidia.com/XFree86/Linux-x86/1.0-7182/README/readme.txt) para más información.

### Frecuencia de refresco no detectada correctamente por los servicios dependientes de XRandR

La extensión XRandR X no es capaz actualmente de gestionar múltiples dispositivos de visualización en una única pantalla de X, sino que solo ve el box delimitador de `MetaMode`, que puede contener uno o más modos reales. Esto significa que si múltiples MetaModes tienen la misma box de delimitación, XRandR no será capaz de distinguir entre ellos.

Con el fin de apoyar `DynamicTwinView`, el controlador de NVIDIA debe hacer que aparezca cada MetaMode como único para XRandR. Actualmente, el controlador de NVIDIA logra esto mediante el uso de la frecuencia de refresco como un identificador único.

Use `nvidia-settings-q RefreshRate` para consultar la actual frecuencia de actualización en cada dispositivo de visualización.

La extensión XRandR está siendo rediseñada por la comunidad de X.Org, por lo que el problema de la frecuencia de actualización puede ser resuelto en poco tiempo.

Esta solución también se puede desactivar mediante el establecimiento de la opción de configuración de X `DynamicTwinView` en `false`, la cual deshabilita el apoyo a NV-CONTROL para la manipulación de MetaModes, pero hará, para ser precisa, que la tasa de refresco de XRandR y XF86VidMode sea visible.

### No se encuentran pantallas en un ordenador portátil/NVIDIA Optimus

Si en un portátil, el controlador de NVIDIA no puede encontrar la pantalla (no screen found), es posible que esté en presencia de una configuración que utiliza Nvidia Optimus: un chipset Intel conectado a la pantalla y las salidas de vídeo, y una tarjeta NVIDIA que hace todo el trabajo duro y escribe para el chipset de la memoria de video.

Compruebe si `$ lspci | grep VGA` obtiene una salida similar a esta:

```
 00:02.0 VGA compatible controlador: Intel Corporation Core Processor Integrated Graphics Controller (rev 02)
 01:00.0 VGA compatible controlador: nVidia Corporation Device 0df4 (rev a1)

```

NVIDIA ha [anunciado planes](http://www.phoronix.com/scan.php?page=news_item&px=MTE3MzY) para apoyar Optimus en sus controladores para Linux en un futuro próximo.

Por tanto, en el estado actual, es necesario instalar el controlador [Intel](/index.php/Intel "Intel") para manejar las pantallas, y luego, si quiere que funcione también el software 3D, puede utilizar [Bumblebee](/index.php/Bumblebee_(Espa%C3%B1ol) "Bumblebee (Español)") para que, a través de dicho programa, pueda hacer uso de la tarjeta NVIDIA.

#### Posible Solución

Un usuario ha reportado una posible solución en un portatil Lenovo W520 con una Quadro 1000M y Nvidia Optimus, consistente en entrar en la BIOS y cambiar en gráficos por defecto de "Optimus" a "discreta" y, de este modo, el controlador de Nvidia (versión 295.20-1 y posteriores) reconoce las pantallas.

Pasos:

1.  Entre en la BIOS
2.  Busque 'Graphics Settings' (pruebe en la pestaña 'Config', y luego en el submenú 'Display')
3.  Cambie 'Graphics Device' a 'Discrete Graphics" (Desactive los gráficos integrados de Intel)
4.  Cambie 'OS Detection for Nvidia Optimus' a 'Desactivado'
5.  Guarde y salga

Comprobado en un Lenovo W520 con un Quadro 1000M y Nvidia Optimus.

### Pantalla(s) encontrada, pero ninguna configuración utilizable

En un portátil, a veces el controlador NVIDIA no puede encontrar la pantalla activa. Puede ser causada porque se posee una tarjeta gráfica con salida VGA/TV. Debe examinar Xorg.0.log para ver lo que está mal.

Otra cosa que puede probar consiste en usar una opción que invalide `"ConnectedMonitor" Option` en la seción `"Device"` para obligar a Xorg a lanzar un error y mostar cómo corregirlo. [Aquí](http://http.download.nvidia.com/XFree86/Linux-x86/1.0-8178/README/appendix-d.html) más información sobre ajustes de ConnectedMonitor.

Después de reiniciar X, supervise Xorg.0.log para obtener el valor correcto de CRT-x, DFP-x, TV-x.

La orden `nvidia-xconfig --query-gpu-info` también podría ser útil.

### Sin control de brillo en los portátiles

Pruebe añadiendo la siguiente línea en el archivo `20-nvidia.conf`

```
 Option "RegistryDwords" "EnableBrightnessControl=1"

```

Si todavía no funciona, puede intentarlo instalando [nvidia-bl](https://aur.archlinux.org/packages/nvidia-bl/) o [nvidiabl](https://aur.archlinux.org/packages.php?ID=50749).

### Barras negras durante la reproducción a pantalla completa de videos flash con la configuración TwinView

Siga las instrucciones que aparecen en este artículo: [Enlace](http://al.robotfuzz.com/content/workaround-fullscreen-flash-linux-multiheaded-desktops)

### La retroiluminación no se apaga en algunas ocasiones

De forma predeterminada, DPMS debe apagar la luz de fondo con el ajuste de tiempo de espera dado o ejecutando xset. Sin embargo, probablemente debido a un error de los controladores propietarios de Nvidia, a veces el resultado es una pantalla en blanco, sin el consiguiente ahorro de energía. Para solucionar esto, hasta tanto el error haya sido corregido, puede utilizar el `vbetool` como usuario root.

Instale el paquete [vbetool](https://www.archlinux.org/packages/?name=vbetool).

Para apagar la pantalla a la vista cuando se desee y luego, pulsando una tecla cualquiera, encender de nuevo la retroiluminación:

```
 vbetool dpms off && read -n1; vbetool dpms on

```

Alternativamente, xrandr es capaz de desactivar y reactivar salidas de monitor sin necesidad de actuar como root.

```
 xrandr --output DP-1 --off; read -n1; xrandr --output DP-1 --auto

```

### Tinte azul en vídeos con Flash

Un problema con las versiones 11.2.202.228-1 y 11.2.202.233-1 de [flashplugin](https://www.archlinux.org/packages/?name=flashplugin) causan que envíen a los paneles de U/V una orden incorrecta, que da como resultado una coloración azul en la visualizanción de algunos vídeos. Hay algunos arreglos posibles para este error:

1.  Instale el paquete [libvdpau](https://www.archlinux.org/packages/?name=libvdpau) más reciente.
2.  Parchee `vdpau_trace.so`_trace.so con [este makepkg](https://bbs.archlinux.org/viewtopic.php?pid=1078368#p1078368).
3.  Haga clic con el botón derecho del mouse sobre un vídeo, seleccione 'Ajustes... (Settings ...)', y desmarque "Activar aceleración de hardware (Enable hardware acceleration)". Vuelva a cargar la página para que los ajustes surtan efecto. Tenga en cuenta que esto desactiva la aceleración GPU.
4.  Efectúe un [Downgrade](/index.php/Downgrading_packages "Downgrading packages") del paquete [flashplugin](https://www.archlinux.org/packages/?name=flashplugin) a la versión 11.1.102.63-1 o anterior.
5.  Utilice [google-chrome](https://aur.archlinux.org/packages/google-chrome/) que incorpora la nueva API Pepper [chromium-pepper-flash](https://aur.archlinux.org/packages/chromium-pepper-flash/).
6.  Pruebe una de las pocas alternativas de Flash.

Los méritos de cada uno de estos posibles arreglos se discuten en [este hilo](https://bbs.archlinux.org/viewtopic.php?id=137877).

### Bleeding Overlay con Flash

Este error se debe a una clave de color incorrecta que utiliza la versión 11.2.202.228-1 de [flashplugin](https://www.archlinux.org/packages/?name=flashplugin), y hace que el contenido flash se "filtre" a otras páginas o fondos negros sólidos. Para evitar este problema basta con instalar la última versión de [libvdpau](https://www.archlinux.org/packages/?name=libvdpau) o exportar la variable `VDPAU_NVIDIA_NO_OVERLAY=1` al perfil de la shell (por ejemplo a `~/.bash_profile` o `~/.zprofile`) o `~/.xinitrc`

### Congelación completa del sistema utilizando Flash

Si usted experimenta ocasionales congelamientos/bloqueos completos del sistema (solo el ratón se mueve) durante la utilización de flashplugin y obtiene del registro:

 `/var/log/errors.log` 
```
NVRM: Xid (0000:01:00): 31, Ch 00000007, engmask 00000120, intr 10000000

```
0000:01:00): 31, Ch 00000007, engmask 00000120, intr 10000000

una posible solución es desactivar la aceleración hardware del flash, estableciendo

 `/etc/adobe/mms.cfg`  `EnableLinuxHWVideoDecode=0` 

O, si desea mantener la aceleración por hardware activada, puede intentar:

```
export VDPAU_NVIDIA_NO_OVERLAY=1

```

...antes de iniciar el navegador. Tenga en cuenta que esto puede provocar lagrimeo.

### Xorg falla al cargarse o aparece una pantalla roja

Si se obtine una pantalla roja y utiliza grub2, deshabilite el framebuffer de grub2 editando `/etc/defaults/grub`, y descomentando la cadena GRUB_TERMINAL_OUTPUT. Para obtener más información consulte [Deshabilitar el framebuffer](/index.php/GRUB2_(Espa%C3%B1ol)#Desactivar_el_framebuffer "GRUB2 (Español)").

### Pantalla en negro en sistemas con GPU integrada de Intel

Si se dispone de una CPU Intel con una GPU integrada (por ejemplo, Intel HD 4000) y se obtiene una pantalla en negro en el arranque después de instalar el paquete [nvidia](https://www.archlinux.org/packages/?name=nvidia), ello se puede deber a un conflicto entre los módulos gráficos. Esto se soluciona con la introducción de algunos módulos en blacklisting para la GPU de Intel. Cree un archivo `/etc/modprobe.d/blacklist.conf` con los módulos *i915* y *intel_agp* para impedir que estos se carguen en el arranque:

 `/etc/modprobe.d/blacklist.conf` 
```
install i915 /bin/false
install intel_agp /bin/false

```

### Pantalla en negro en sistemas con GPU VIA integrada

Como antes, poner en blacklisting el módulo *viafb* puede resolver los conflictos con los controladores de NVIDIA:

 `/etc/modprobe.d/blacklist.conf` 
```
install viafb /usr/bin/false

```

### X falla lanzando «no screens found» con una Intel iGPU

Al igual que anteriormente, si se tiene una CPU Intel con una GPU integrada y X no arranca con mensajes de:

```
[ 76.633] (EE) No devices detected.
[ 76.633] Fatal server error:
[ 76.633] no screens found

```

entonces será necesario añadir el BusID de la tarjeta nvidia a la propia configuración de X. Puede encontrar dicho parámetro con la siguiente orden:

 `# lspci | grep VGA` 
```
00:02.0 VGA compatible controller: Intel Corporation Xeon E3-1200 v2/3rd Gen Core processor Graphics Controller (rev 09)
01:00.0 VGA compatible controller: NVIDIA Corporation GK107 [GeForce GTX 650] (rev a1)

```

para resolver el problema se añade la propia tarjeta en la sección Device en el archivo de configuración de X. En este caso:

 `/etc/X11/xorg.conf.d/10-nvidia.conf` 
```
Section "Device"
    Identifier     "Device0"
    Driver         "nvidia"
    VendorName     "NVIDIA Corporation"
    BusID          "PCI:1:0:0"
EndSection

```

Advierta como la salida `01:00.0` se escribe con el formato `1:0:0`.

## Véase también

*   [Foros de NVIDIA](http://www.nvnews.net/vbulletin/forumdisplay.php?s=&forumid=14)
*   [Archivo léame oficial para los controladores de NVIDIA](http://http.download.nvidia.com/XFree86/Linux-x86/1.0-7182/README/readme.txt)