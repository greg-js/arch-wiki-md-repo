Artículos relacionados

*   [AMD Catalyst (Español)](/index.php/AMD_Catalyst_(Espa%C3%B1ol) "AMD Catalyst (Español)")
*   [Xorg (Español)](/index.php/Xorg_(Espa%C3%B1ol) "Xorg (Español)")

Los poseedores de tarjetas gráficas **ATI/AMD** pueden elegir entre el [controlador privativo](/index.php/ATI_Catalyst_(Espa%C3%B1ol) "ATI Catalyst (Español)") de AMD ([catalyst](https://aur.archlinux.org/packages/catalyst/)) y el controlador de código abierto ([xf86-video-ati](https://www.archlinux.org/packages/?name=xf86-video-ati)). Este artículo trata sobre el controlador de código abierto.

El controlador libre no está *a la par* con el controlador propietario en términos de rendimiento 3D en las nuevas tarjetas ni tiene soporte tan fiable para la salida de TV. Sin embargo, ofrece un mejor apoyo dual-head, aceleración 2D excelente, y proporciona suficiente aceleración 3D necesaria para algunos [gestores de ventanas](/index.php/Window_manager_(Espa%C3%B1ol) "Window manager (Español)") que aprovechan la aceleración OpenGl, tal como [Compiz](/index.php/Compiz "Compiz") o KWin.

Si tiene dudas sobre cuál elegir, pruebe primero el controlador de código abierto, dado que, por regla general, se adaptará perfectamente a la mayoría de sus necesidades y es menos problemático (consulte la [tabla de características](http://www.x.org/wiki/RadeonFeature) para más detalles).

## Contents

*   [1 Convenciones sobre nombres](#Convenciones_sobre_nombres)
*   [2 Descripción](#Descripci.C3.B3n)
*   [3 Instalación](#Instalaci.C3.B3n)
*   [4 Configuración](#Configuraci.C3.B3n)
*   [5 Kernel mode-setting (KMS)](#Kernel_mode-setting_.28KMS.29)
    *   [5.1 Inicio temprano de KMS](#Inicio_temprano_de_KMS)
    *   [5.2 Inicio tardío](#Inicio_tard.C3.ADo)
*   [6 Optimizar prestaciones](#Optimizar_prestaciones)
    *   [6.1 Desactivar PCI-E 2.0](#Desactivar_PCI-E_2.0)
    *   [6.2 Glamor](#Glamor)
*   [7 Tarjetas gráficas intercambiables Hybrid graphics/AMD Dynamic](#Tarjetas_gr.C3.A1ficas_intercambiables_Hybrid_graphics.2FAMD_Dynamic)
*   [8 Gestionar el ahorro de energía (Powersaving)](#Gestionar_el_ahorro_de_energ.C3.ADa_.28Powersaving.29)
    *   [8.1 Métodos antiguos](#M.C3.A9todos_antiguos)
        *   [8.1.1 Variación dinámica de la frecuencia](#Variaci.C3.B3n_din.C3.A1mica_de_la_frecuencia)
        *   [8.1.2 Variación de la frecuencia, basada en perfiles](#Variaci.C3.B3n_de_la_frecuencia.2C_basada_en_perfiles)
        *   [8.1.3 Configuración permanente](#Configuraci.C3.B3n_permanente)
        *   [8.1.4 Herramientas gráficas](#Herramientas_gr.C3.A1ficas)
        *   [8.1.5 Otras notas](#Otras_notas)
    *   [8.2 Gestión dinámica de la energía](#Gesti.C3.B3n_din.C3.A1mica_de_la_energ.C3.ADa)
*   [9 Salida de TV](#Salida_de_TV)
    *   [9.1 Forzar la salida de TV con KMS](#Forzar_la_salida_de_TV_con_KMS)
*   [10 Audio por HDMI](#Audio_por_HDMI)
*   [11 Configuración Dual Head](#Configuraci.C3.B3n_Dual_Head)
    *   [11.1 Pantallas X independientes](#Pantallas_X_independientes)
*   [12 Activar la aceleración de vídeo](#Activar_la_aceleraci.C3.B3n_de_v.C3.ADdeo)
*   [13 Cambiar vsync a off](#Cambiar_vsync_a_off)
*   [14 Solución de problemas](#Soluci.C3.B3n_de_problemas)
    *   [14.1 Fallos al iniciar sesión en el DE o WM](#Fallos_al_iniciar_sesi.C3.B3n_en_el_DE_o_WM)
    *   [14.2 Añadir resoluciones no detectadas](#A.C3.B1adir_resoluciones_no_detectadas)
    *   [14.3 AGP está desactivado (con KMS)](#AGP_est.C3.A1_desactivado_.28con_KMS.29)
    *   [14.4 TV mostrando un borde negro alrededor de la pantalla](#TV_mostrando_un_borde_negro_alrededor_de_la_pantalla)
    *   [14.5 Pantalla en negro mostrando el cursor del ratón en X al reanudar desde la suspensión](#Pantalla_en_negro_mostrando_el_cursor_del_rat.C3.B3n_en_X_al_reanudar_desde_la_suspensi.C3.B3n)
    *   [14.6 Sin efectos de escritorio de KDE4 con X1300 y el controlador Radeon](#Sin_efectos_de_escritorio_de_KDE4_con_X1300_y_el_controlador_Radeon)
    *   [14.7 Pantalla negra y sin consola visualizada, pero X funcionando en KMS](#Pantalla_negra_y_sin_consola_visualizada.2C_pero_X_funcionando_en_KMS)
    *   [14.8 Algunas aplicaciones 3D fallan o muestran texturas completamente negras](#Algunas_aplicaciones_3D_fallan_o_muestran_texturas_completamente_negras)
    *   [14.9 Prestaciones 2D (por ejemplo, el desplazamiento) lentas](#Prestaciones_2D_.28por_ejemplo.2C_el_desplazamiento.29_lentas)
    *   [14.10 ATI X1600 (series RV530) con aplicaciones 3D muestra ventanas negras](#ATI_X1600_.28series_RV530.29_con_aplicaciones_3D_muestra_ventanas_negras)

## Convenciones sobre nombres

La marca ATI [Radeon](https://en.wikipedia.org/wiki/es:Radeon "wikipedia:es:Radeon") sigue un esquema de nombres que relaciona cada producto para un segmento del mercado. En este artículo, se utilizará la nomenclatura tanto en base al nombre del *producto* (por ejemplo, HD 4850, X1900) como en base al nombre del *código* o del *núcleo* (*core*) (por ejemplo, RV770, R580). Tradicionalmente, una *serie del producto* se correspondería a una *serie del núcleo* (por ejemplo, la serie del producto «X1000» incluye todos los productos X1300, X1600, X1800, X1900 y del mismo modo cuando utilizan el núcleo de la serie «R500» - que incluiría los núcleos RV515, RV530, R520, y R580).

Para una tabla completa de comparación entre el nombre de los productos y los correlativos núcleos, consulte la [comparación de las unidades de procesamiento gráfico AMD](https://en.wikipedia.org/wiki/Comparison_of_AMD_graphics_processing_units "wikipedia:Comparison of AMD graphics processing units")

## Descripción

El controlador `xf86-video-ati` (radeon):

*   Funciona con chipsets Radeon HD hasta 6xxx y 7xxxM (últimos chipsets Northern Islands).
    *   Las tarjetas Radeon de la serie HD 77xx (Southern Islands) son parcialmente compatibles. Compruebe [feature matrix](http://www.x.org/wiki/RadeonFeature) para determinar las características no compatibles.
    *   Las tarjetas Radeon hasta la serie X1xxx son totalmente compatibles, estables y proporcionan una completa aceleración 2D y 3D.
    *   Las tarjetas Radeon HD de las series 2xxx a 6xxx tienen pleno soporte para una aceleración 2D y una aceleración 3D funcional, pero no son compatibles con todas las características que ofrece el controlador propietario.
*   Soporta DRI1, RandR 1.2/1.3, aceleración EXA y [kernel mode-setting](/index.php/Kernel_mode_setting_(Espa%C3%B1ol) "Kernel mode setting (Español)")/DRI2.

Generalmente, **xf86-video-ati** debe ser su primera opción, independientemente de la tarjeta ATI que se posea. En caso de que sea necesario utilizar un controlador para las nuevas tarjetas ATI, es preferible el controlador privativo **catalyst**.

**Nota:** **xf86-video-ati** es reconocido como *radeon* por el kernel y en `xorg.conf`.

## Instalación

**Nota:** Si Catalyst/`fglrx` ha sido instalado previamente, véase [ATI Catalyst (Español)#Desinstalación](/index.php/ATI_Catalyst_(Espa%C3%B1ol)#Desinstalaci.C3.B3n "ATI Catalyst (Español)").

[Instale](/index.php/Help:Reading_(Espa%C3%B1ol)#Instalaci.C3.B3n_de_paquetes "Help:Reading (Español)") [xf86-video-ati](https://www.archlinux.org/packages/?name=xf86-video-ati), disponible en los [Repositorios Oficiales](/index.php/Repositorios_Oficiales "Repositorios Oficiales").

## Configuración

Xorg cargará automáticamente el controlador y utilizará el EDID del monitor para ajustar la resolución nativa. La configuración solo es necesaria para optimizar el controlador.

Si desea hacer una configuración manualmente, cree el archivo `/etc/X11/xorg.conf.d/**20-radeon.conf**`, y añada lo siguiente:

```
 Section "Device"
    Identifier "Radeon"
    Driver     "radeon"
 EndSection

```

Con esta sección, puede habilitar posteriormente algunas características y ajustar la configuración del controlador.

## Kernel mode-setting (KMS)

**Sugerencia:** Si tiene problemas con la resolución, compruebe [esta página](/index.php/Kernel_mode_setting_(Espa%C3%B1ol)#Forzar_modos_y_EDID "Kernel mode setting (Español)").

[KMS](/index.php/Kernel_mode_setting_(Espa%C3%B1ol) "Kernel mode setting (Español)") permite la resolución nativa en el framebuffer y permite la conmutación instantánea de la consola (tty). KMS permite también nuevas tecnologías (como DRI2) que ayudarán a reducir eventuales anomalías y aumentará el rendimiento 3D, incluyendo el ahorro de enegía en el kernel-space.

KMS para tarjetas de vídeo ATI exige el controlador de código abierto de [Xorg](/index.php/Xorg_(Espa%C3%B1ol) "Xorg (Español)") [xf86-video-ati](https://www.archlinux.org/packages/?name=xf86-video-ati) versión 6.12.4 o posterior.

**Nota:**

*   KMS está **activado** por defecto para detectar automáticamente las tarjetas ATI/AMD. Esta sección se mantiene para configuraciones fuera de stock.
*   A partir de Linux 3.9, el controlador `radeon` **requiere** kernel mode-setting (el antiguo uso de mode-setting todavía se puede activar como opción en la compilación del kernel, sin embargo, algunas características como audio HDMI dependerán de KMS). Si se tiene `radeon.modeset=0` o `nomodeset` entre los [parámetros del kernel](/index.php/Kernel_parameters_(Espa%C3%B1ol) "Kernel parameters (Español)"), elimínelos. Si tiene `options radeon modeset=0` en cualquier archivo de `/etc/modprobe.d/`, elimínelo.

#### Inicio temprano de KMS

*Este método iniciará KMS tan pronto como sea posible en el [proceso de arranque](/index.php/Systemd_(Espa%C3%B1ol) "Systemd (Español)").*

1\. Retiraremos todos los controladores UMS en conflicto de la línea de órdenes del kernel:

*   Eliminaremos todas las opciones `vga=` de la línea del *kernel* en el [archivo de configuración](/index.php/Boot_Loader#Configuration_files "Boot Loader") del gestor de arranque. El uso de otros controladores framebuffer (como `[uvesafb](/index.php/Uvesafb "Uvesafb")` o `radeonfb`) entrarán en conflicto con KMS.
*   La velocidad del bus AGP la podemos ajustar con la opción `radeon.agpmode=x` en la línea del kernel, donde x puede tener los valores 1, 2, 4, 8 (velocidad AGP) o -1 (modo PCI).

2\. De otro modo, cuando [initramfs](/index.php/Mkinitcpio_(Espa%C3%B1ol) "Mkinitcpio (Español)") se cargue:

*   Si tiene un kernel especial fuera del stock de `-ARCH` (por ejemplo, linux-zen), recuerde utilizar el archivo de configuración apropiado de mkinitcpio, por ejemplo, `/etc/mkinitcpio-zen.conf` y no `/etc/mkinitcpio.conf`.
*   Eliminaremos cualquier módulo relacionado con el framebuffer del archivo *mkinitcpio*.
*   Añadiremos `radeon` a la matriz `MODULES` del archivo *mkinitcpio* . Para dar soporte técnico a AGP, es necesario añadir `intel_agp` (o `ali_agp`, `ati_agp`, `amd_agp`, `amd64_agp` etc.) antes del módulo `radeon`.
*   Regeneraremos [initramfs](/index.php/Mkinitcpio_(Espa%C3%B1ol)#Creaci.C3.B3n_de_la_imagen_y_activaci.C3.B3n "Mkinitcpio (Español)").

Por último, **reinicie** el sistema.

#### Inicio tardío

*Con esta elección, KMS se activará cuando los módulos se carguen durante el [proceso de arranque](/index.php/Boot_process "Boot process")*.

Si tiene un kernel especial (por ejemplo, linux-zen), recuerde utilizar el archivo de configuración apropiado mkinitcpio, por ejemplo, `/ etc/mkinitcpio-zen.conf`. Estas instrucciones están escritas para el kernel por defecto ([linux](https://www.archlinux.org/packages/?name=linux)).

**Nota:** Para soporte AGP, puede ser necesario añadir `intel_agp`, `ali_agp`, `ati_agp`, `amd_agp`, o `amd64_agp`) a los archivos .conf apropiados en `/etc/modules-load.d`.

1.  Elimine todas las opciones `vga=` de la línea del *kernel* en el [archivo de configuración](/index.php/Boot_Loader#Configuration_files "Boot Loader") del gestor de arranque. El uso de otros controladores framebuffer (como `[uvesafb](/index.php/Uvesafb "Uvesafb")` o `radeonfb`) entrarán en conflicto con KMS. Retire cualquier otro módulo relacionado con framebuffer de `/etc/mkinitcpio.conf`. La opción `video=` puede ahora ser utilizada en conjunción con KMS.
2.  **Reiniciar** el sistema.

## Optimizar prestaciones

Las siguientes opciones se aplican en el archivo `/etc/X11/xorg.conf.d/**20-radeon conf**`.

**ColorTiling**, es completamente seguro activarla y supuestamente está habilitada de forma predeterminada. La mayoría de los usuarios notarán un mayor rendimiento, pero todavía no está soportado en tarjetas R200 y anteriores. Puede ser activado en las tarjetas anteriores, pero la carga de trabajo se transfiere a la CPU

```
 Option "ColorTiling" "1"

```

**Acceleration architecture**; esta opción solo funcionará en las tarjetas **nuevas**. Si la habilita y luego no puede volver a X, retírela.

```
 Option "AccelMethod" "EXA"

```

**PageFlip**, es generalmente segura su activación. Esto principalmente se utiliza en las tarjetas más antiguas, que desactivará EXA. Con los controladores más modernos se puede habilitar junto con EXA.

```
 Option "EnablePageFlip" "1"

```

**EXAVSync**, se trata de una opción que evita que se rompa la imagen del monitor al detener el motor hasta que el controlador de pantalla ha pasado a la región de destino. Reduce el desgarro a costa de una disminución de las prestaciones y es sabido que causa inestabilidad en algunos chips. Muy útil cuando se habilita la superposición Xv en los vídeos en un escritorio con aceleración 3D. No es necesario cuando KMS (continuando la aceleración DRI2) está habilitado.

```
 Option "EXAVSync" "1"

```

A continuación un ejemplo de archivo de configuración `/etc/X11/xorg.conf.d /**20-radeon.conf**`:

```
Section "Device"
       Identifier  "Mi Tarjeta Gráfica"
       Driver	"radeon"
       Option	"SWcursor"              "off" #software del cursor necesario en raras ocasiones, por lo tanto desactivado de forma predeterminada
       Option	"EnablePageFlip"        "on"  #soportado en todas las tarjetas R/RV/RS4xx y hardware antiguo, y desactivado de forma predeterminada
       Option	"AccelMethod"           "EXA" #opciones válidas XAA y EXA. EXA es el método más reciente para la aceleración y es la opción predeterminada
       Option	"RenderAccel"           "on"  #activado por defecto en todos los hardware radeon
       Option	"ColorTiling"           "on"  #habilitados de forma predeterminada en RV300 y últimas tarjetas Radeon
       Option	"EXAVSync"              "off" #por defecto está desactivada
       Option	"EXAPixmaps"            "on"  #afecta positivamente en el rendimiento de 2D, pero también puede causar fallos en algunas tarjetas antiguas
       Option	"AccelDFS"              "on"  #está apagado por defecto, lea la página de manual radeon para más información
EndSection

```

La definición del **gartsize**, si no es detectada automáticamente, puede ser realizada mediante la adición de `radeon.gartsize=32` en los [parámetros del kernel](/index.php/Kernel_parameters_(Espa%C3%B1ol) "Kernel parameters (Español)"). El tamaño es en megabytes y 32 es para tarjetas RV280.

Por otra parte, también se puede hacer con una opción modprobe en `/etc/modprobe.d/radeon.conf`:

```
 options radeon gartsize=32

```

**Para más información y otras opciones, lea la página de manual radeon y la página de módulos info**: [radeon(4)](https://jlk.fjfi.cvut.cz/arch/manpages/man/radeon.4), `modinfo radeon`.

Un buena herramienta para probar es [driconf](https://www.archlinux.org/packages/?name=driconf). Esto le permitirá modificar varias configuraciones, como vsync, filtrado anisotrópico, compresión de texturas, etc. Con esta herramienta es posible deshabilitar «Low Impact fallback», necesario para algunos programas (por ejemplo, Google Earth).

### Desactivar PCI-E 2.0

A partir del kernel 3.6, PCI-E v2.0 en **radeon** parece estar activada de forma predeterminada.

Puede ser inestable con algunas placas base, por lo que se puede desactivar mediante la adición de `radeon.pcie_gen2=0` en la [línea de órdenes del kernel](/index.php/Kernel_parameters_(Espa%C3%B1ol) "Kernel parameters (Español)").

Más información en este [artículo de Phoronix](http://www.phoronix.com/scan.php?page=article&item=amd_pcie_gen2&num=1)

### Glamor

Con las nuevas versiones de los controladores abiertos de ATI, ahora se puede utilizar un novedoso AccelMethod llamado «glamor»: es un método de aceleración 2D implementado a través de OpenGL que debería funcionar con tarjetas gráficas cuyo controlador sea igual o superior a R300.

```
 Option	"AccelMethod"           "glamor"

```

Sin embargo, es necesario agregar la siguiente sección antes:

```
Section "Module"
	Load "dri2"
	Load "glamoregl" 
EndSection

```

## Tarjetas gráficas intercambiables Hybrid graphics/AMD Dynamic

Es la tecnología que se utiliza en los recientes ordenadores portátiles equipados con GPU, una para energía convencional (normalmente una tarjeta Intel integrada) y otra que demanda más energía (por lo general, Radeon o Nvidia). Hay tres maneras de conseguir que funcione::

*   Si no necesita ejecutar ninguna aplicación que demande mucha energía de la GPU, basta con desactivar la tarjeta dedicada: `echo OFF > /sys/kernel/debug/vgaswitcheroo/switch`. Se pueden hacer más cosas con vgaswitcheroo (véase [Ubuntu wiki](https://help.ubuntu.com/community/HybridGraphics#Using_vga_switcheroo) para más información) pero hay que tener en cuenta que las características de una de las tarjetas esán vinculadas a una sesión gráfica, no se pueden utilizar ambas tarjetas en dicha sesión.
*   Puede usar [PRIME](/index.php/PRIME "PRIME"). Es la forma correcta de usar las tarjetas gráficas híbridas en Linux, pero todavía requiere un poco de intervención manual por parte del usuario.
*   También puede utilizar [bumblebee](/index.php/Bumblebee "Bumblebee") con radeon, para lo cual tiene el paquete [bumblebee-amd-git](https://aur.archlinux.org/packages/bumblebee-amd-git/) disponible en [AUR](/index.php/AUR_(Espa%C3%B1ol) "AUR (Español)").

## Gestionar el ahorro de energía (Powersaving)

Con el controlador radeon, el ahorro de energía está desactivado por defecto y tiene que ser activado manualmente, si se desea.

Se puede elegir entre tres métodos diferentes:

1.  [dynpm](#Dynamic_frequency_switching)
2.  [profile](#Profile-based_frequency_switching)
3.  [dpm](#Dynamic_power_management) (disponible desde el kernel 3.11)

**Es difícil decir cuál es el mejor en general, así que se tiene que decidir por cada cual.**

La administración de energía es compatible con todos los chips que incluyen las tablas de estado de energía adecuadas en el vbios (R1xx y posteriores). «dpm» solo se admite en R6xx y nuevos chips.

Véase [http://www.x.org/wiki/RadeonFeature/#index3h2](http://www.x.org/wiki/RadeonFeature/#index3h2) para obtener más detalles.

### Métodos antiguos

#### Variación dinámica de la frecuencia

Este método cambia dinámicamente la frecuencia de los relojes en base a la carga de la gpu, por lo que el rendimiento es incrementado cuando se ejecutan aplicaciones intensivas para la GPU, y disminuye cuando la GPU está inactiva. La modificación de la frecuencia del reloj se intenta realizar durante los periodos de barrido vertical, pero debido a la temporalización de las funciones de resincronización, no siempre se completa en el período de barrido, lo que puede conducir a un parpadeo en la pantalla. Debido a esto, el perfil dynpm solo funciona cuando está conectado un único monitor.

Se puede activar simplemente ejecutando la siguiente orden:

```
# echo dynpm > /sys/class/drm/card0/device/power_method

```

#### Variación de la frecuencia, basada en perfiles

Este método le permite seleccionar uno de los cinco perfiles (descritos abajo). Los diferentes perfiles, en su mayor parte, terminan cambiando la frecuencia/voltaje de la tarjeta. Este método no es tan agresivo, pero es más estable y libre de parpadeo, y trabaja con múltiples cabezales activos.

Se puede activar simplemente ejecutando la siguiente orden:

```
# echo profile > /sys/class/drm/card0/device/power_method

```

Seleccione uno de los perfiles disponibles:

*   `default` utiliza los relojes por defecto y no cambia el estado de energía. Este es el comportamiento predeterminado.
*   `auto` selecciona el perfil entre los estados de energía `mid` y `high` («medio» y «alto») basado en si la energía del sistema procede de la batería o de la red electrica, respectivamente. Selecciona el estado de energía `low` cuando los monitores se encuentran en estado apagado ([DPMS](/index.php/DPMS "DPMS")-off).
*   `low` fuerza a la GPU a funcionar en estado de energía `low` en todo momento. El perfil `low` puede causar problemas de visualización en algunos ordenadores portátiles, de ahí que el perfil `auto` solo utiliza el modo `low` cuando el monitor está apagado.
*   `mid` fuerza a la gpu a funcionar en estado de energía `mid`(«medio») en todo momento. El perfil `low` se selecciona cuando el monitor se encuentra en estado [DPMS](/index.php/DPMS "DPMS")-off.
*   `high` fuerza a la gpu a funcionar en estado de energía `high` en todo momento. El perfil `low` se selecciona cuando el monitor se encuentra [DPMS](/index.php/DPMS "DPMS")-off (apagado).

Así, por ejemplo, digamos que queremos activar el perfil `low` (sustituya `low` con cualquiera de los perfiles anteriormente mencionados, según sus necesidades):

```
# echo low > /sys/class/drm/card0/device/power_profile

```

#### Configuración permanente

La activación que se ha descrito anteriormente no es persistente, esto es, no va a durar después de reiniciar el equipo. Para que permanezca, puede utilizar [systemd-tmpfiles](/index.php/Systemd#Temporary_files "Systemd") (ejemplo para [#Variación dinámica de la frecuencia](#Variaci.C3.B3n_din.C3.A1mica_de_la_frecuencia)):

 `/etc/tmpfiles.d/radeon-pm.conf` 
```
w /sys/class/drm/card0/device/power_method - - - - dynpm

```

Como alternativa, puede usar esta regla [udev](/index.php/Udev "Udev") en su lugar (ejemplo para [#Variación de la frecuencia, basada en perfiles](#Variaci.C3.B3n_de_la_frecuencia.2C_basada_en_perfiles)):

 `/etc/udev/rules.d/30-radeon-pm.rules` 
```
KERNEL=="dri/card0", SUBSYSTEM=="drm", DRIVERS=="radeon", ATTR{device/power_method}="profile", ATTR{device/power_profile}="low"

```

**Nota:** Si la regla anterior falla, pruebe eliminando el prefijo `dri/`.

#### Herramientas gráficas

*   **Radeon-tray** — Un pequeño programa para controlar los perfiles de energía de la tarjeta Radeon mediante un icono en la bandeja del sistema. Está escrito en PyQt4 y es adecuado para usuarios que no usan Gnome.

	[https://github.com/StuntsPT/Radeon-tray](https://github.com/StuntsPT/Radeon-tray) ||

*   **power-play-switcher** — Una interfaz gráfica de usuario para cambiar la configuración de powerplay y el controlador de código abierto para las tarjetas ATI Radeon .

	[https://code.google.com/p/power-play-switcher/](https://code.google.com/p/power-play-switcher/) || [power-play-switcher](https://aur.archlinux.org/packages/power-play-switcher/)

*   **Gnome-shell-extension-Radeon-Power-Profile-Manager** — Una pequeña extensión para Gnome-shell que le permitirá cambiar el perfil de la potencia de la tarjeta radeon cuando se utiliza el controlador de código abierto.

	[https://github.com/StuntsPT/shell-extension-radeon-power-profile-manager](https://github.com/StuntsPT/shell-extension-radeon-power-profile-manager) || [gnome-shell-extension-radeon-ppm](https://aur.archlinux.org/packages/gnome-shell-extension-radeon-ppm/) [gnome-shell-extension-radeon-power-profile-manager-git](https://aur.archlinux.org/packages/gnome-shell-extension-radeon-power-profile-manager-git/)

#### Otras notas

Para obtener información sobre la velocidad con que la GPU funciona, ejecute la orden siguiente y obtendrá algo parecido a esto:

 `$ cat /sys/kernel/debug/dri/0/radeon_pm_info` 
```
  state: PM_STATE_ENABLED
  default engine clock: 300000 kHz
  current engine clock: 300720 kHz
  default memory clock: 200000 kHz

```

Todo depende de qué línea GPU sea la suya. Junto con la versión del controlador radeon, de la versión del kernel, etc. Por lo tanto, puede que no tenga muchas opciones de regulación de voltaje disponibles.

Los sensores térmicos se realizan a través de los chips i2c externos o a través del sensor térmico interno (rv6xx-evergreen solamente). Para conseguir la temperatura en tarjetas que usan chips i2c, es necesario cargar el controlador hwmon apropiado para el sensor utilizado en su placa (lm63, lm64, etc.) El drm intentará cargar el controlador hwmon apropiado. En las tarjetas que utilizan el sensor térmico interno, el drm configurará el interfaz hwmon automáticamente. Cuando el controlador adecuado se carga, la temperatura puede ser vista a través de las herramientas [lm_sensors](/index.php/Lm_sensors "Lm sensors") o a través de sysfs en `/sys/class/hwmon`.

### Gestión dinámica de la energía

Con el kernel 3.11, ASPM está activado por defecto, pero DPM no. Para activarlo, agregue el parámetro `radeon.dpm=1` en los [parámetros del kernel](/index.php/Kernel_parameters_(Espa%C3%B1ol) "Kernel parameters (Español)").

A diferencia de [dynpm](#Dynamic_frequency_switching), el método «dpm» utiliza el hardware de la GPU para cambiar dinámicamente los relojes y el voltaje según la carga de la GPU.

Hay 3 modos de funcionamiento para elegir:

*   `battery` menor consumo de energía
*   `balanced` estado predeterminado
*   `performance` rendimiento más alto

Se pueden cambiar a través de sysfs:

```
# echo battery > /sys/class/drm/card0/device/power_dpm_state

```

Para probar o depurar propósitos, puede forzar a la tarjeta a funcionar en un modo de rendimiento determinado:

*   `auto` predeterminado; utiliza todos los niveles del estado de energía
*   `low` fuerza el nivel de rendimiento más bajo
*   `high` fuerza el nivel de rendimiento más alto

```
# echo low > /sys/class/drm/card0/device/power_dpm_force_performance_level

```

## Salida de TV

Desde agosto de 2007, hay soporte para salida de TV para todas las tarjetas Radeon con salida de TV integrada.

Por el momento esto está un poco limitado, dado que no siempre detectará automáticamente la salida correctamente y solo funciona el modo NTSC.

En primer lugar, compruebe que dispone de una salida de S-video: `xrandr` que debería darle algo como

```
 Screen 0: minimum 320x200, current 1024x768, maximum 1280x1200
 ...
 S-video disconnected (normal left inverted right x axis y axis)

```

Configure la tv estándar a usar:

```
 xrandr --output S-video --set "tv standard" ntsc

```

Añada una modalidad para ella (actualmente solo es compatible con 800x600):

```
 xrandr - addmode S-video 800x600

```

Puede apoyarse en un modo clon:

```
 xrandr --output S-video --same-as VGA-0

```

Hasta aquí todo bien. Ahora vamos a tratar de ver lo que tenemos:

```
 xrandr --output S-video --mode 800x600

```

En este punto, se debe ver una versión 800x600 de su escritorio en su televisor.

Para desactivar la salida, haga

```
 xrandr --output S-video --off

```

También se puede observar que el vídeo se está reproduciendo en el monitor y no en el televisor. Donde la superposición Xv se envía y se controla mediante el atributo XV_CRTC.

Para enviar la señal de salida a la TV, haga

```
 xvattr -a XV_CRTC -v 1

```

**Nota:** Necesita instalar **xvattr** desde [AUR](/index.php/Arch_User_Repository_(Espa%C3%B1ol) "Arch User Repository (Español)") para ejecutar esta orden

Para volver al propio monitor, cambie el valor a `0`. El valor `-1` se utiliza para el intercambio automático en configuraciones dualhead.

Por favor, consulte [Habilitación de Salida de TV Estática](http://www.x.org/wiki/radeonTV) para saber cómo activar la salida de TV en su archivo de configuración xorg.

### Forzar la salida de TV con KMS

El kernel puede reconocer el parámetro `video=` con el siguiente formato:

```
  video=<conn>:<xres>x<yres>[M][R][-<bpp>][@<refresh>][i][m][eDd]

```

(Consulte [KMS](/index.php/Kernel_mode_setting_(Espa%C3%B1ol) "Kernel mode setting (Español)"))

Por ejemplo:

```
 video=DVI-I-1:1280x1024-24@60e

```

o

```
 "video=9-pin DIN-1:1024x768-24@60e"

```

Los parámetros que contengan espacios en blanco deben encerrarse entre comillas dobles. La implementación actual de mkinitcpio también requiere que un signo `#` se coloque al principio de la línea. Por ejemplo:

```
 root=/dev/disk/by-uuid/d950a14f-fc0c-451d-b0d4-f95c2adefee3 ro quiet radeon.modeset=1 security=none # video=DVI-I-1:1280x1024-24@60e "video=9-pin DIN-1:1024x768-24@60e"

```

*   Grub puede pasar la línea de órdenes tal como se ofrecen.
*   Lilo necesita la utilización de barras invertidas para reconocer los caracteres entre «dobles comillas» (append `# \"video=9-pin DIN-1:1024x768-24@60e\"`)
*   Grub2: TODO

Se puede obtener la lista de salidas de vídeo con la siguiente orden:

 `ls -1 /sys/class/drm/ | grep -E '^card[[:digit:]]+-' | cut -d- -f2-` 

## Audio por HDMI

El Audio HDMI es compatible con el controlador de vídeo [xf86-video-ati](https://www.archlinux.org/packages/?name=xf86-video-ati). Por defecto, el módulo del kernel necesario está desactivado en las versiones del kerne >=3.0\. Sin embargo, si su tarjeta Radeon aparece en el listado de [Radeon Feature Matrix](http://www.x.org/wiki/RadeonFeature), puede añadir `radeon.audio=1` a los [parámetros del kernel](/index.php/Kernel_parameters_(Espa%C3%B1ol) "Kernel parameters (Español)"). Por ejemplo:

 `/boot/syslinux/syslinux.cfg` 
```
LABEL arch
    MENU LABEL Arch Linux
    LINUX ../vmlinuz-linux
    APPEND root=/dev/sda1 ro radeon.audio=1
    INITRD ../initramfs-linux.img

```

Si el audio HDMI no funciona después de instalar el controlador, compruebe la configuración con el procedimiento [Advanced Linux Sound Architecture/Troubleshooting#HDMI Output does not work](/index.php/Advanced_Linux_Sound_Architecture/Troubleshooting#HDMI_Output_does_not_work "Advanced Linux Sound Architecture/Troubleshooting").

**Nota:** Al escribir estas líneas (2013-05-20), los controladores de las tarjetas [Southern Islands](http://www.x.org/wiki/RadeonFeature#Decoder_ring_for_engineering_vs_marketing_names) no son compatibles con el audio HDMI.

*   El módulo del kernel `radeon.audio` solo funciona si [KMS](#Kernel_mode-setting_.28KMS.29) está activado. Por defecto, **xf86-video-ati** permite KMS.
*   Si el sonido se distorsiona pruebe [ajustando `tsched=0`](/index.php/PulseAudio#Glitches.2C_skips_or_crackling "PulseAudio") y asegúrese que el demonio `rtkit` está ejecutándose.

## Configuración Dual Head

### Pantallas X independientes

Una configuración independiente para el doble-cabezal puede ser ajustada de la manera habitual. Sin embargo, es posible que desee saber que el controlador radeon tiene la opción `"ZaphodHeads"` que le permite enlazar una sección específica del dispositivo a una salida de su elección, por ejemplo utilizando:

```
       Section "Device"
         Identifier     "Device0"
         Driver         "radeon"
         Option         "ZaphodHeads"   "VGA-0"
         VendorName     "ATI"
         BusID          "PCI:1:0:0"
         Screen          0
       EndSection

```

Esto puede ser un salvavidas, ya que algunas tarjetas que tienen más de dos salidas (por ejemplo, una salida HDMI, otra DVI, otra VGA), solo seleccionará y utilizará las salidas HDMI + DVI para la configuración del dual-head, a menos que explícitamente especifique `"ZaphodHeads" "VGA-0"`.

Por otra parte, esta opción le permite seleccionar fácilmente la pantalla que desea marcar como primaria.

## Activar la aceleración de vídeo

La última versión del paquete [mesa](https://www.archlinux.org/packages/?name=mesa) ha añadido compatibilidad para decodificar MPEG1/2 al controlador libre, expontándola mediante [libvdpau](https://www.archlinux.org/packages/?name=libvdpau). Después de haberlo instalado, asigne el valor `vdpau` a la variable de entorno `LIBVA_DRIVER_NAME` y el nombre del núcleo del controlador a `VDPAU_DRIVER`, por ejemplo:

 `~/.bashrc` 
```
export LIBVA_DRIVER_NAME=vdpau
export VDPAU_DRIVER=r600
```

para tarjetas basadas en r600 (todos los controladores disponibles para el varlor VDPAU están en `/usr/lib/vdpau/`).

## Cambiar vsync a off

El controlador radeon activa vsync por defecto, lo cual es perfectamente correcto, excepto para el [benchmarking](https://es.wikipedia.org/wiki/Benchmarking). Para desactivarlo, cree el archivo `~/.drirc` (o modifíquelo si ya existe) y añada la siguiente sección:

 `~/.drirc` 
```
<driconf>
    <device screen="0" driver="dri2">
        <application name="Default">
            <option name="vblank_mode" value="0" />
        </application>
    </device>
    <!-- Other devices ... -->
</driconf>

```

Esto es eficaz con **dri2**, no con el código de su tarjeta de vídeo (como r600).

## Solución de problemas

### Fallos al iniciar sesión en el DE o WM

Si encuentra fallos gráficos cuando efectúa el login en su Entorno de Escritorio o Gestor de Ventanas, primero intente iniciar X sin `/etc/X11/xorg.conf`. Las versiones recientes de Xorg son capaces de auto-detección fiable y auto-configuración para la mayoría de los casos al uso. Archivos `xorg.conf` obsoletos o mal configurados suelen ser la causa de estos problemas.

Con el fin de funcionar sin un archivo de configuración, se recomienda que el grupo de paquetes `xorg-input-drivers` esté instalado.

Los fallos también pueden estar relacionados con el [Kernel Mode Setting](/index.php/Kernel_mode_setting_(Espa%C3%B1ol) "Kernel mode setting (Español)"). Considere la posibilidad de [deshabilitar KMS.](#Desactivar_KMS)

Se puede también intentar desactivar la opción `EXAPixmaps` en el archivo `/etc/X11/xorg.conf.d/20-radeon.conf`:

```
 Section "Device"
    Identifier "Radeon"
    Driver "radeon"
    Opción "EXAPixmaps" "off"
 EndSection

```

El fallo también podría tener su causa en la opción `AccelDFS`, por lo que pruebe desactivarla mediante:

```
 Option "AccelDFS" "off"

```

### Añadir resoluciones no detectadas

Por ejemplo, cuando EDID falla en una conexión a un DisplayPort.

Este tema se trata en [Xrandr page](/index.php/Xrandr#Adding_undetected_resolutions "Xrandr").

### AGP está desactivado (con KMS)

Si experimenta un rendimiento deficiente y dmesg muestra algo como esto

```
 [drm:radeon_agp_init] *ERROR* Unable to acquire AGP: -19

```

compruebe si el controlador AGP de la placa base (por ejemplo, `via_agp`, `intel_agp`, etc.) se carga antes que el módulo `radeon`. Consulte [activación de KMS.](#Activar_KMS)

### TV mostrando un borde negro alrededor de la pantalla

Si al conectar la TV y una Radeon HD 5770 a través del puerto HDMI, la TV muestra una imagen borrosa con un borde de 2-3 cm alrededor, se debe a la protección de [Overscan](https://en.wikipedia.org/wiki/Overscan "wikipedia:Overscan"), que se puede desactivar mediante xrandr:

```
 xrandr --output HDMI-0 --set underscan off

```

Este problema no se da cuando se utiliza el controlador propietario.

### Pantalla en negro mostrando el cursor del ratón en X al reanudar desde la suspensión

Al reanudar desde la suspensión con tarjetas de 32MB o menos puede encontrarse con una pantalla en negro con un cursor del ratón en X. Algunas partes de la pantalla pueden ser rediseñadas cuando están bajo el cursor del ratón. Obligando a `EXAPixmaps` a `"activarse"` en `/etc/X11/xorg.conf.d/20-radeon.conf` puede solucionar el problema. Véase [performance tuning](#Performance_tuning) para obtener más información.

### Sin efectos de escritorio de KDE4 con X1300 y el controlador Radeon

Un error en KDE4 puede impedir un control exacto del hardware de vídeo, con la desactivación de los efectos de escritorio a pesar de que la X1300 tiene potencia más que suficiente para la GPU. Una solución puede ser la de anular manualmente dicho control en los archivos de configuración KDE4 `/usr/share/kde-settings/kde-profile/default/share/config/kwinrc` y/o `.kde/share/config/kwinrc`. Añada:

```
 DisableChecks=true

```

Para la sección [Compositing]. Asegúrese de que la composición se activa con:

```
 Enabled=true

```

### Pantalla negra y sin consola visualizada, pero X funcionando en KMS

Esta es una solución para problemas de no visualizar ninguna consola que pueden presentarse cuando se utilizan dos o más tarjetas de ATI en el mismo PC. El portatil Fujitsu Siemens Amilo PA 3553, por ejemplo, tiene este problema. Esto se debe al controlador de consola fbcon que lleva a cabo su propia asignación en el dispositivo framebuffer respecto a la tarjeta incorrecta. Esto se puede solucionar mediante la adición de un argumento a la línea de arranque del kernel:

```
 fbcon=map:1

```

Esto le indicará al controlador fbcon que realice el mapeado sobre el disposibito framebuffer `/dev/fb1` y no sobre `/dev/fb0`, que en el caso examinado es la tarjeta gráfica incorrecta.

### Algunas aplicaciones 3D fallan o muestran texturas completamente negras

Es posible que necesite apoyo de compresión de textura, que no está incluido en el controlador de código abierto. Instale [libtxc_dxtn](https://www.archlinux.org/packages/?name=libtxc_dxtn) (y [lib32-libtxc_dxtn](https://www.archlinux.org/packages/?name=lib32-libtxc_dxtn) para los sistemas multilib).

### Prestaciones 2D (por ejemplo, el desplazamiento) lentas

Si tiene problemas con el rendimiento 2D, como el desplazamiento en el terminal o el navegador, puede que tenga que añadir `Option "MigrationHeuristic" "greedy"` en la sección `"Device"` de su archivo `xorg.conf`.

A continuación un archivo de configuración de ejemplo `/etc/X11/xorg.conf.d/**20-radeon.conf**`:

```
Section "Device"
        Identifier  "Mi Tarjeta Gráfica"
        Driver      "radeon"
        Option      "MigrationHeuristic"  "greedy"
EndSection

```

### ATI X1600 (series RV530) con aplicaciones 3D muestra ventanas negras

Hay tres posibles soluciones:

*   Trate de añadir `pci=nomsi` a su gestor de arranque en los [parámetros del Kernel.](/index.php/Kernel_parameters_(Espa%C3%B1ol) "Kernel parameters (Español)")
*   Si esto no funciona, pruebe añadiendo `noapic` en lugar de `pci=nomsi`.
*   Si ninguna de las propuestas anteriores funciona, entonces pruebe ejecutando `vblank_mode=0 glxgears` o `vblank_mode=1 glxgears` para ver cuál de ellas soluciona el problema, y entonces instale `driconf` a través de pacman y configure esa opción en `~/.drirc`.