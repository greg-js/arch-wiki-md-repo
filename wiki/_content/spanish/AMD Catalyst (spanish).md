Los poseedores de tarjetas de video **ATI/AMD** tienen la opción de elegir entre el controlador propietario de ATI ([catalyst](https://aur.archlinux.org/packages/catalyst/)) y el [controlador de código abierto](/index.php/ATI_(Espa%C3%B1ol) "ATI (Español)") ([xf86-video-ati](https://www.archlinux.org/packages/?name=xf86-video-ati)). Este artículo trata sobre el driver propietario.

El paquete del controlador catalyst de AMD para linux , era conocido anteriormente como *fglrx* (**F**ire**GL** y **R**adeon **X**). Solo el nombre del paquete ha cambiado, mientras que el módulo del kernel conserva su nombre original *fglrx.ko*. Por lo tanto, cualquier mención de fglrx en este artículo se refiere específicamente al *módulo del kernel*, **no al paquete**.

Desde el 26 de abril de 2013, los paquetes de Catalyst ya no se ofrecen en los repositorios oficiales. En el pasado, Catalyst [dejó de tener](https://www.archlinux.org/news/ati-catalyst-support-dropped/) el apoyo oficial de Arch debido a la insatisfacción con la calidad y la velocidad de su desarrollo. Esta vez, ha sido su incompatibilidad con Xorg 1.14.

En comparación con el controlador de código abierto, Catalyst tiene peor rendimiento en gráficos 2D, pero tiene un mejor soporte para la representación 3D. Los dispositivos soportados son las tarjetas de vídeo [ATI/AMD Radeon](https://en.wikipedia.org/wiki/Radeon "wikipedia:Radeon") con chipset R600 y más recientes (Radeon HD 2xxx y posteriores). Consulte [esta tabla](https://en.wikipedia.org/wiki/Comparison_of_AMD_graphics_processing_units "wikipedia:Comparison of AMD graphics processing units"), o Xorg [Decoder ring](http://www.x.org/wiki/RadeonFeature#Decoder_ring_for_engineering_vs_marketing_names) para relacionar nombres de *modelo* (X1900, HD4850) desde/con nombres de *chips* (R580, RV770, respectivamente).

## Contents

*   [1 Instalación](#Instalaci.C3.B3n)
    *   [1.1 Instalar el controlador](#Instalar_el_controlador)
        *   [1.1.1 Instalar desde el repositorio no oficial](#Instalar_desde_el_repositorio_no_oficial)
        *   [1.1.2 Instalar desde AUR](#Instalar_desde_AUR)
    *   [1.2 Configurar el controlador](#Configurar_el_controlador)
        *   [1.2.1 Configurar X](#Configurar_X)
        *   [1.2.2 Cargar los módulos al arrancar](#Cargar_los_m.C3.B3dulos_al_arrancar)
        *   [1.2.3 Desactivar kernel mode setting](#Desactivar_kernel_mode_setting)
        *   [1.2.4 Comprobación del funcionamiento](#Comprobaci.C3.B3n_del_funcionamiento)
    *   [1.3 Kernels personalizados](#Kernels_personalizados)
    *   [1.4 Apoyo a PowerXpress](#Apoyo_a_PowerXpress)
        *   [1.4.1 Ejecutar dos servidores X (uno usando el controlador Intel, el otro usando fglrx) simultáneamente](#Ejecutar_dos_servidores_X_.28uno_usando_el_controlador_Intel.2C_el_otro_usando_fglrx.29_simult.C3.A1neamente)
        *   [1.4.2 Problemas con PowerXpress en portátiles ejecutándose en modalidad AMD (pxp_switch_catalyst amd) con monitor externo / secundario](#Problemas_con_PowerXpress_en_port.C3.A1tiles_ejecut.C3.A1ndose_en_modalidad_AMD_.28pxp_switch_catalyst_amd.29_con_monitor_externo_.2F_secundario)
*   [2 Repositorios Xorg](#Repositorios_Xorg)
    *   [2.1 [xorg114]](#.5Bxorg114.5D)
    *   [2.2 [xorg113]](#.5Bxorg113.5D)
    *   [2.3 [xorg112]](#.5Bxorg112.5D)
*   [3 Herramientas](#Herramientas)
    *   [3.1 Catalyst-hook](#Catalyst-hook)
    *   [3.2 Catalyst-generator](#Catalyst-generator)
*   [4 Características](#Caracter.C3.ADsticas)
    *   [4.1 Prestación «Tear Free»](#Prestaci.C3.B3n_.C2.ABTear_Free.C2.BB)
    *   [4.2 Aceleración de vídeo](#Aceleraci.C3.B3n_de_v.C3.ADdeo)
    *   [4.3 Frecuencia GPU/Mem, Temperatura, Velocidad del ventilador, utilidades Overclocking](#Frecuencia_GPU.2FMem.2C_Temperatura.2C_Velocidad_del_ventilador.2C_utilidades_Overclocking)
    *   [4.4 Doble Pantalla (Dual Head / Dual Screen / Xinerama)](#Doble_Pantalla_.28Dual_Head_.2F_Dual_Screen_.2F_Xinerama.29)
        *   [4.4.1 Introducción](#Introducci.C3.B3n)
        *   [4.4.2 ATI Catalyst Control Center](#ATI_Catalyst_Control_Center)
        *   [4.4.3 Instalación](#Instalaci.C3.B3n_2)
        *   [4.4.4 Configuración](#Configuraci.C3.B3n)
*   [5 Desinstalación](#Desinstalaci.C3.B3n)
*   [6 Solución de problemas](#Soluci.C3.B3n_de_problemas)
    *   [6.1 Aplicaciones 3D en Wine congeladas](#Aplicaciones_3D_en_Wine_congeladas)
    *   [6.2 Problemas con los colores de vídeo](#Problemas_con_los_colores_de_v.C3.ADdeo)
    *   [6.3 KWin y composite](#KWin_y_composite)
    *   [6.4 Pantalla en negro con bloqueos completos al reiniciar el sistema o startx](#Pantalla_en_negro_con_bloqueos_completos_al_reiniciar_el_sistema_o_startx)
        *   [6.4.1 Llamadas hardware ACPI defectuosa](#Llamadas_hardware_ACPI_defectuosa)
    *   [6.5 KDM desaparece después de cerrar la sesión](#KDM_desaparece_despu.C3.A9s_de_cerrar_la_sesi.C3.B3n)
    *   [6.6 Direct Rendering no funciona](#Direct_Rendering_no_funciona)
    *   [6.7 Problemas con la hibernación y la suspensión](#Problemas_con_la_hibernaci.C3.B3n_y_la_suspensi.C3.B3n)
        *   [6.7.1 Vídeo no reanuda desde suspend2ram](#V.C3.ADdeo_no_reanuda_desde_suspend2ram)
    *   [6.8 Bloqueo del sistema/Hard lock](#Bloqueo_del_sistema.2FHard_lock)
    *   [6.9 Conflictos con el hardware](#Conflictos_con_el_hardware)
    *   [6.10 Bloqueos temporales durante la reproducción de vídeo](#Bloqueos_temporales_durante_la_reproducci.C3.B3n_de_v.C3.ADdeo)
    *   [6.11 «aticonfig: No supported adaptaters detected»](#.C2.ABaticonfig:_No_supported_adaptaters_detected.C2.BB)
    *   [6.12 Soporte WebGL en Chromium](#Soporte_WebGL_en_Chromium)
    *   [6.13 Retardos y bloqueos en vídeos flash con el flashplugin de Adobe](#Retardos_y_bloqueos_en_v.C3.ADdeos_flash_con_el_flashplugin_de_Adobe)
    *   [6.14 Retardos en el movimiento de ventanas en GNOME3](#Retardos_en_el_movimiento_de_ventanas_en_GNOME3)
    *   [6.15 Imposible utilizar pantalla completa con resolución 1920x1080](#Imposible_utilizar_pantalla_completa_con_resoluci.C3.B3n_1920x1080)
    *   [6.16 Configuración de pantalla dual: problemas generales con aceleración, OpenGL, composición, funcionamiento](#Configuraci.C3.B3n_de_pantalla_dual:_problemas_generales_con_aceleraci.C3.B3n.2C_OpenGL.2C_composici.C3.B3n.2C_funcionamiento)
    *   [6.17 Desactivar características VariBright](#Desactivar_caracter.C3.ADsticas_VariBright)
    *   [6.18 Hybrid/PowerXpress: apagar la GPU dedicada](#Hybrid.2FPowerXpress:_apagar_la_GPU_dedicada)
    *   [6.19 Al intercambiar desde una sesión X a TTY nos da una pantalla en blanco](#Al_intercambiar_desde_una_sesi.C3.B3n_X_a_TTY_nos_da_una_pantalla_en_blanco)
    *   [6.20 Error: 30 FPS / Tear-Free / V-Sync](#Error:_30_FPS_.2F_Tear-Free_.2F_V-Sync)
*   [7 Véase también](#V.C3.A9ase_tambi.C3.A9n)

## Instalación

Hay tres formas de instalar Catalyst en el sistema:

*   Una forma es utilizar el repositorio [Vi0L0](https://aur.archlinux.org/account/Vi0l0/) (mantenedor Catalyst no oficial de Arch). Este repositorio contiene todos los paquetes necesarios.
*   El segundo método que puede utilizar es desde AUR; los PKGBUILD ofrecen aquí los mismos paquetes que Vi0L0 y son los que utiliza para compilar paquetes para su repositorio.
*   Por último, se puede instalar el controlador directamente desde AMD.

Antes de elegir el método que prefiera, tendrá que ver el controlador que necesita. A partir de Catalyst 12.4, AMD ha decidido seguir de modo diferente el desarrollo para las tarjetas Radeon HD 5xxx y Radeon HD 2xxx, 3xxx y 4xxx. Para las tarjetas Radeon HD 2xxx, 3xxx y 4xxx, existe el controlador Catalyst **legacy**, siendo el controlador actual el proporcionado para Radeon HD 5xxx (y posteriores). Al margen del controlador adecuado, se necesitarán las utilidades Catalyst.

**Nota:** Después de las instrucciones dadas para cada método de instalación, encontrará instrucciones generales que **todos** deben realizar, independientemente del método utilizado.

### Instalar el controlador

#### Instalar desde el repositorio no oficial

Si no pretende o no se siente a gusto compilando los paquetes de [AUR](/index.php/AUR "AUR"), este es el método a seguir. El repositorio es mantenido por nuestro mantenedor Catalyst no oficial, Vi0L0\. Todos los paquetes están firmados y es seguro usarlos. Como se verá más adelante en este artículo, Vi0L0 también es responsable de muchos otros paquetes que le ayudarán a conseguir que su sistema trabaje con sus tarjetas gráficas ATI.

Vi0L0 tiene tres repositorios Catalyst diferentes, cada uno de los cuales tiene controladores diferentes:

*   [catalyst]; para el controlador Catalyst actual que necesitan las tarjetas Radeon HD 5xxx y superiores, el cual contiene las últimas versiones (estable o beta) de Catalyst.
*   [catalyst-stable]; para el controlador normal de Catalyst requerido por las tarjetas Radeon HD 5xxx y posteriores, con la última versión estable del controlador;
*   [catalyst-hd234k]; para el controlador Catalyst legacy que necesitan las tarjetas Radeon HD 2xxx, 3xxx y 4xxx.

**Advertencia:** El controlador legacy Catalyst no es compatible con Xorg 1.13\. Si desea utilizar este controlador, consulte [#Repositorios Xorg](#Repositorios_Xorg) para obtener instrucciones sobre cómo volver a utilizar o mantener Xorg 1.12.

**Advertencia:** Catalyst no es compatible con el servidor Xorg 1.15, consulte [#Repositorios de Xorg](#Repositorios_de_Xorg) y elija el repositorio xorg que desea utilizar.

Para activar uno de estos, tendrá que editar `/etc/pacman.conf` y añadir el repositorio de su elección **por encima de todos los demás repositorios** en `/etc/pacman.conf`:

*   Para [catalyst], es este:

```
[catalyst]
Server = http://catalyst.wirephire.com/repo/catalyst/$arch

```

*   Para [catalyst-stable] se obtiene con el siguiente:

```
[catalyst-stable]
Server = http://catalyst.wirephire.com/repo/catalyst/$arch

```

*   Para [catalyst-hd234k], hay que añadir el siguiente:

```
[catalyst-hd234k]
Server = http://catalyst.wirephire.com/repo/catalyst-hd234k/$arch

```

También debe [añadir clave GPG para Vi0L0](/index.php/User:Vi0L0 "User:Vi0L0") de modo que pacman confíe en los repositorios:

```
# pacman-key --keyserver pgp.mit.edu --recv-keys 0xabed422d653c3094
# pacman-key --lsign-key 0xabed422d653c3094

```

**Sugerencia:** Dado que catalyst.wirephire.com se caerá si se excede un cierto límite de ancho de banda (esto ha venido pasando) o puede ser demasiado lento desde su ubicación, los mirrors de los repositorios son proporcionados por yanom en [[1]](http://70.239.162.206/catalyst-mirror) (EE.UU.) y por rtsinformatique en [[2]](http://mirror.rts-informatique.fr/archlinux-catalyst/) (Francia). Estos mirrors, sin embargo, vienen sin ninguna garantía y no es seguro que estén siempre operativos:
```
[catalyst]
#Server = http://70.239.162.206/catalyst-mirror/repo/catalyst/$arch
#Server = http://mirror.rts-informatique.fr/archlinux-catalyst/repo/catalyst/$arch

```

```
[catalyst-stable]
#Server = http://70.239.162.206/catalyst-mirror/repo/catalyst/$arch
#Server = http://mirror.rts-informatique.fr/archlinux-catalyst/repo/catalyst/$arch

```

```
[catalyst-hd234k]
#Server = http://70.239.162.206/catalyst-mirror/repo/catalyst-hd234k/$arch
#Server = http://mirror.rts-informatique.fr/archlinux-catalyst/repo/catalyst-hd234k/$arch

```

(descomente la línea para el mirror más cercano a su ubicación; es una buena idea tener alternativas para el caso de inactividad de un mirror)

La creación de la imagen del repositorio se puede lograr fácilmente usando rsync://mirror.rts-informatique.fr::archlinux-catalyst

Una vez que los haya agregado, actualice la base de datos de pacman e [instale](/index.php/Pacman_(Espa%C3%B1ol) "Pacman (Español)") los paquetes:

*   *catalyst*
*   *catalyst-utils*
*   *lib32-catalyst-utils* - opcional, si necesita soporte para OpenGL de 32 bit en sistemas de 64-bit.

Si utiliza un portátil con tarjeta gráfica híbrida Intel/AMD, el conjunto de paquetes será un poco diferente:

*   *catalyst*
*   *catalyst-utils-pxp*
*   *lib32-catalyst-utils-pxp* - opcional, si necesita soporte para OpenGL de 32 bit en sistemas de 64-bit.

**Nota:** Si pacman le pregunta acerca de la eliminación de **libgl** puede responder con segurida que si: «Y»

**Advertencia:** Catalyst, desde el repositorio de Vi0L0, se compila con un kernel y solo uno. Para Vi0L0, se está haciendo cada vez más difícil mantenerse al día con el ritmo de actualización de los kernels y, como consecuencia, hemos visto una gran cantidad de usuarios que piden saber qué hacer sobre esto en los foros. A menudo, la solución es a) esperar a que Vi0L0 recompile el paquete Catalyst con aquellas versiones más recientes, b) hacerlo usted mismo o c) contener la actualización del kernel de Linux. La solución más fácil es hacerlo usted mismo, no de forma manual, sino mediante el uso del excelente [#Catalyst-hook](#Catalyst-hook) de Vi0L0.

Dichos repositorios también contienen algunos paquetes adicionales que pueden ser útiles, los que se pueden sustituir el paquete catalyst-hook:

*   *catalyst-generator* - este paquete es capaz de generar módulos `fglrx` empaquetados para ser accesibles por pacman -paquete más seguro y compatible, aunque tiene que ser realizado manualmente-. Se describe en [#Catalyst-generator](#Catalyst-generator)
*   *catalyst-hook* - un servicio de systemd que actualizará automáticamente el módulo `fglrx`, mientras que el sistema se apaga o se reinicia. Se describe en [#Catalyst-hook](#Catalyst-hook)

Encontrará más detalles acerca de estos paquetes en la sección [Herramientas](#Herramientas). Por último, ambos repositorios también contienen el paquete [xvba-video](https://aur.archlinux.org/packages/xvba-video/), que permiten la aceleración de vídeo descrita [aquí](#Aceleraci.C3.B3n_de_v.C3.ADdeo) y el paquete **AMDOverdriveCtrl**, que es una GUI para controlar over- y underclocking. Consulte [esta sección](#Frecuencia_GPU.2FMem.2C_Temperatura.2C_Velocidad_del_ventilador.2C_utilidades_Overclocking).

#### Instalar desde AUR

La última forma de instalar Catalyst es desde [AUR](/index.php/AUR "AUR"). Si quiere compilar los paquetes específicamente para su equipo, esta es tu mejor opción. Tenga en cuenta que también es la manera más tediosa para instalar Catalyst, por el trabajo que conlleva y por que requiere actualizaciones manuales sobre cada actualización del kernel.

**Advertencia:** Si instala el paquete Catalyst desde AUR, tendrá que reconstruir Catalyst cada vez que se actualiza el kernel. De lo contrario X **fallará** al iniciar.

Todos los paquetes mencionados anteriormente en el repositorio no oficial Vi0L0 también están disponibles en [AUR](/index.php/AUR "AUR"):

*   [catalyst](https://aur.archlinux.org/packages/catalyst/);
*   [catalyst-generator](https://aur.archlinux.org/packages/catalyst-generator/);
*   [catalyst-hook](https://aur.archlinux.org/packages/catalyst-hook/);
*   [catalyst-utils](https://aur.archlinux.org/packages/catalyst-utils/);
*   [lib32-catalyst-utils](https://aur.archlinux.org/packages/lib32-catalyst-utils/);

AUR además contiene algunos paquetes que **no** están en ninguno de los repositorios. Este contienen el paquete denominado *Catalyst-total* y las versiones beta:

*   [catalyst-total](https://aur.archlinux.org/packages/catalyst-total/);
*   [catalyst-total-pxp](https://aur.archlinux.org/packages/catalyst-total-pxp/);
*   [catalyst-total-hd234k](https://aur.archlinux.org/packages/catalyst-total-hd234k/);
*   [catalyst-test](https://aur.archlinux.org/packages/catalyst-test/);

El paquete [catalyst-total](https://aur.archlinux.org/packages/catalyst-total/) hace más fácil el trabajo de los usuarios de AUR. Compila el controlador, las utilidades del kernel y las utilidades del kernel de 32 bit. También compila el paquete [catalyst-hook](https://aur.archlinux.org/packages/catalyst-hook/), explicado más arriba.

[catalyst-total-pxp](https://aur.archlinux.org/packages/catalyst-total-pxp/) construye Catalyst con el soporte experimental powerXpress.

### Configurar el controlador

Una vez que haya instalado el controlador mediante alguno de los métodos anteriores, tendrá que configurar X para que funcione con Catalyst. También, tendrá que asegurarse de que el módulo se carga en el arranque. Además, se debe desactivar [kernel mode setting](/index.php/Kernel_mode_setting "Kernel mode setting").

#### Configurar X

Para configurar X, tendrá que crear un archivo xorg.conf. Catalyst proporciona la herramienta `aticonfig` para crear/modificar el archivo `xorg.conf`. También puede configurar prácticamente todos los aspectos de la tarjeta accediendo al archivo `/etc/ati/amdpcsdb`. Para obtener una lista completa de las opciones de `aticonfig`, ejecute:

```
# aticonfig --help | less

```

**Advertencia:** Utilice la opción `--output` para generar un archivo de prueba antes de comprometerse a crear un archivo definitivo `xorg.conf` en el directorio `/etc/X11/`, en cuanto que la presencia de este último anulará cualquier ajuste presente en los archivos ubicados en la carpeta `/etc/X11/xorg.conf.d/`.

**Nota:** Para adherirse a la nueva localización de configuración use `# aticonfig [...] --output` para que pueda adaptarse a la sección `Device` en `/etc/X11/xorg.conf.d/20-radeon.conf`. El inconveniente de esto es que muchas opciones de `aticonfig` se basan en un archivo `xorg.conf`, y, por lo tanto, no estarán disponible para el nuevo.

Ahora, hay que configurar Catalyst.

*   Si solo tiene un monitor, ejecute lo siguiente:

	 `# aticonfig --initial` 

**Nota:** Si tiene problemas con PowerXpress quizás debería probar instalando [catalyst-total-pxp](https://aur.archlinux.org/packages/catalyst-total-pxp/).

*   Sin embargo, si tiene dos monitores y desea utilizar los dos, puede ejecutar la orden indicada a continuación. Tenga en cuenta que esto generará una configuración de *«dual head»* con la segunda pantalla situada encima de la primera pantalla.

	 `# aticonfig --initial=dual-head --screen-layout=above` 

**Nota:** Consulte [esta sección](#Doble_Pantalla_.28Dual_Head_.2F_Dual_Screen_.2F_Xinerama.29) para obtener más información sobre la configuración de dos monitores.

Puede comparar el archivo generado con uno de los [ejemplos Xorg.conf](/index.php/Xorg#Sample_xorg.conf_Files "Xorg") (listado de ejemplos que figuran en la página de Xorg).

Aunque las versiones actuales de Xorg detectan automáticamente la mayoría de las opciones cuando se inicia, es posible que desee especificar, en algún caso, otras opciones respecto a las dadas en las versiones por defecto.

Aquí hay un ejemplo (con notas) **para referencias**. Las entradas con `#` son necesarias, agregue entradas después de `##` según su conveniencia:

```
Section "ServerLayout"
        Identifier     "Arch"
        Screen      0  "Screen0" 0 0                # Los 0 son necesarios.
EndSection
Section "Module"
        Load ...
        ...
EndSection
Section "Monitor"
        Identifier   "Monitor0"
        ...
EndSection
Section "Device"
        Identifier  "Card0"
        Driver      "fglrx"                         # Esencial.
        BusID       "PCI:1:0:0"                     # Recomendado si falla la autodetección.
        Option      "OpenGLOverlay" "0"             ##
        Option      "XAANoOffscreenPixmaps" "false" ##
EndSection
Section "Screen"
        Identifier "Screen0"
        Device     "Card0"
        Monitor    "Monitor0"
        DefaultDepth    24
        SubSection "Display"
                Viewport   0 0
                Depth     24                        # No debe cambiar de '24'
                Modes "1280x1024" "2048x1536"       ## 1er valor=resolución predeterminada, segundo=máxima.
                Virtual 1664 1200                   ## (x+64, y) to workaround potential OGL rect. artifacts/
        EndSubSection                               ## fijado en Catalyst 9.8
EndSection
Section "DRI"
        Mode 0666                                   # Puede ayudar a habilitar direct rendering.
EndSection
```

**Nota:** En **toda** actualización de Catalyst debería eliminar el archivo `amdcccle` de la siguiente forma: detener X, eliminar `/etc/ati/amdpcsdb`, iniciar X, y a continuación, ejecutar `amdcccle`, de lo contrario puede experimentar una mala detección de la versión de Catalyst en `amdcccle`.

*Si necesita más información sobre Catalyst, visite [este hilo](https://bbs.archlinux.org/viewtopic.php?id=57084).*

#### Cargar los módulos al arrancar

Tenemos que colocar en blacklist el módulo `radeon` para evitar la carga automática. Para ello, pondremos *radeon* en la lista negra en `/etc/modprobe.d/modprobe.conf`. Además, nos aseguraremos que no se carga ningún archivo en `/etc/modules-load.d/`. Para obtener más información, podemos consultar [blacklisting en este artículo](/index.php/Kernel_modules_(Espa%C3%B1ol)#Blacklisting "Kernel modules (Español)").

A continuación, vamos a tener que asegurarnos que el módulo `fglrx` se carga automáticamente. Bien añadiendo `fglrx` en una nueva línea de un archivo de módulo existente ubicado en `/etc/modules-load.d/`, o bien creando un nuevo archivo y agregando `fglrx` .

#### Desactivar kernel mode setting

**Nota:** No haga esto si está usando `catalyst-utils-pxp` or `catalyst-total-pxp` porque controlador intel lo necesita.

Desactivar el mode setting del kernel es importante, ya que el controlador no parece compatible con [KMS](/index.php/KMS "KMS") todavía. Si no desactiva KMS, el sistema puede congelarse cuando se trata de cambiar a un tty o, incluso, cuando apague el equipo a través de su DE.

Para desactivar kernel mode setting, añada `nomodeset` a los [parámetros del kernel](/index.php/Kernel_parameters_(Espa%C3%B1ol) "Kernel parameters (Español)").

#### Comprobación del funcionamiento

Suponiendo que ha reiniciado el sistema y el inicio de sesión se ha realizado correctamente, se puede comprobar si fglrx está funcionando correctamente con las siguientes órdenes:

```
$ lsmod | grep fglrx
$ fglrxinfo

```

Si tiene salida, funciona. Por último, ejecute Xorg con `$ startx` o usando GDM/KDM y verifique que el *direct rendering* está activado ejecutando la siguiente orden en una terminal:

```
$ glxinfo | grep "direct rendering"

```

Si la salida es `"direct rendering: yes"`, entonces ¡todo ha funcionado!. Si la orden `$ glxinfo` no se encuentra, puede que tenga que instalar el paquete [mesa-demos](https://www.archlinux.org/packages/?name=mesa-demos) también.

**Nota:** También puede utilizar:
```
$ fgl_glxgears

```

como test alternativo de fglrx para `glxgears`.

**Advertencia:** En las últimas versiones de Xorg, las rutas de las bibliotecas han cambiado. De modo que, a veces `libGL.so` no se puede cargar correctamente incluso si está instalado. No descarte esta opción si su GL no está funcionando. Por favor, lea [#Solución de problema](#Soluci.C3.B3n_de_problema) para obtener más detalles.

### Kernels personalizados

**Nota:** Si no se siente cómodo o no tiene experiencia en la creación de empaquetados, lea primero la página [ABS](/index.php/Arch_Build_System_(Espa%C3%B1ol) "Arch Build System (Español)") dela wiki para que las cosas salgan bien.

Para instalar catalyst de un kernel personalizado, tendrá que crear su propio paquete `catalyst-$kernel` .

Si usted no tiene experiencia o confianza en compilar paquetes, consulte la sección de [ABS](/index.php/ABS "ABS") de la wiki para un tutorial completo sobre el método a utilizar.

1.  Obtenga, en primer lugar, los archivos `PKGBUILD` y `catalyst.install` desde [Catalyst](/index.php/AUR "AUR").
2.  Edite PKGBUILD. Dos cambios son necesarios aquí:
    1.  Cambie `pkgname=catalyst` en `pkgname=catalyst-$kernel_name`, donde $kernel_name es el nombre que desee (por ejemplo, custom, mm...).
    2.  Cambie la dependencia `linux` a `$kernel_name`.
3.  Compile e instale el paquete: ejecute (`makepkg -i` o `makepkg` seguido de `# pacman -U pkgname.pkg.tar.gz`)

**Nota:**

*   Teniendo instalados varios kernels, a continuación, necesitará instalar los controladores de [catalyst-utils](https://aur.archlinux.org/packages/catalyst-utils/) para todos los kernels. No entrarán en conflictos unos con otros.
*   [catalyst-generator](https://aur.archlinux.org/packages/catalyst-generator/) es capaz de compilar el paquete `catalyst-{kernver}` por sí solo, por lo que no se necesita realmente llevar a cabo ningún paso manual. Para obtener más información, consulte [esta sección](#Herramientas).

### Apoyo a PowerXpress

La tegnología PowerXpress permite intercambiar desde las tarjetas gráficas integradas (IGP) a gráficas distintas en los portátiles, ya sea para aumentar la duración de la batería o para lograr una mejor capacidad de renderizado 3D.

Para utilizar esta funcionalidad en Arch tendrá que:

*   Obtener y compilar el paquete [catalyst-total-pxp](https://aur.archlinux.org/packages/catalyst-total-pxp/) desde [AUR](/index.php/AUR "AUR"), o
*   Instalar el paquete **catalyst-utils-pxp** desde el repositorio [catalyst] (además de lib32-catalyst-utils-pxp, si es necesario).

Para habilitar el intercambio en la IGP de Intel también tendrá que instalar el paquete [mesa-libgl](https://www.archlinux.org/packages/?name=mesa-libgl) y los controladores: [xf86-video-intel](https://www.archlinux.org/packages/?name=xf86-video-intel) y [intel-dri](https://www.archlinux.org/packages/?name=intel-dri).

**Nota:** **La última versión de Catalyst, versión 13.1 (no Catalyst legacy) es compatible con [xorg-server](https://www.archlinux.org/packages/?name=xorg-server) (version 1.13.1), [mesa](https://www.archlinux.org/packages/?name=mesa) 9.0.1 y [xf86-video-intel](https://www.archlinux.org/packages/?name=xf86-video-intel) 2.20.18**.

En las versiones de Catalyst anteriores a la 13.1 (y todas las versiones de Catalyst legacy) tienen algunos problemas con los nuevos controladores de Intel, **siendo la última versión funcional de la que se tiene constancia la 2.20.2-2 de [xf86-video-intel](https://www.archlinux.org/packages/?name=xf86-video-intel)**, por lo que quizás se vea obligado a hacer downgrade si se está utilizando los últimos lanzamientos de los repositorios de Arch (aunque es recomendable probar el controlador más nuevo antes de hacer downgrade, por si funciona).

Tenga en cuenta que [xf86-video-intel](https://www.archlinux.org/packages/?name=xf86-video-intel) 2.20.2-2 funciona con **xorg-server 1.12**, por lo que si desea utilizarlo, tendrá que hacer downgrade de xorg-server también. Para más información sobre esto, véase [#Repositorios Xorg](#Repositorios_Xorg).

Ahora se puede intercambiar entre la tarjeta integrada y la dedicada de la GPU, usando las siguientes órdenes:

```
# aticonfig --px-igpu    #para GPU integrada
# aticonfig --px-dgpu    #para GPU dedicada
```

Recordarle únicamente que necesita `/etc/X11/xorg.conf` configurado para la tarjeta AMD con `fglrx` incorporado.

También puede utilizar el script de intercabio `pxp_switch_catalyst` que llevará a cabo algunas operaciones utiles adicionales:

*   Intercambiar `xorg.conf` - se cambiará el nombre de `xorg.conf` en `xorg.conf.cat` (si está fglrx en su interior) o `xorg.conf.oth` (si está intel incorporado) y se creará un enlace simbólico a `xorg.conf`, en función de lo que se eligió.
*   Ejecutar `aticonfig --px-Xgpu`.
*   Ejecutar `switchlibGL`.
*   Añadir/eliminar `fglrx` en/desde `/etc/modules-load.d/catalyst.conf`.

Utilización:

```
# pxp_switch_catalyst amd
# pxp_switch_catalyst intel
```

Si se tienen problemas cuando se intenta ejecutar X con el controlador de Intel, es posible que sea porque está tratando de forzar la aceleración "UXA" ; asegúrese de que `xorg.conf` para la GPU de Intel tiene `Option "AccelMethod" "uxa"`, como sigue:

 `/etc/X11/xorg.conf` 
```
Section "Device"
        Identifier  "Intel Graphics"
        Driver      "intel"
        #Option      "AccelMethod"  "sna"
        **Option      "AccelMethod"  "uxa"**
        #Option      "AccelMethod"  "xaa"
EndSection
```

#### Ejecutar dos servidores X (uno usando el controlador Intel, el otro usando fglrx) simultáneamente

Dado que fglrx es propenso a romperse (con respecto a PowerXpress), podría ser una buena idea utilizar el controlador Intel en el servidor X principal y disponer de un servidor X secundario usando fglrx cuando la aceleración 3D sea necesaria. No obstante, si intercambiamos sin más a la GPU dedicada desde la GPU integrada usando `aticonfig` o `amdcccle`, causará toda suerte de errores extraños cuando se inicie la segunda X.

Para ejecutar dos servidores X al mismo tiempo (cada uno con un controlador diferente), primero debemos configurar una X plenamente funcional con el controlador Catalyst y luego mover su configuración `xorg.conf` a un lugar temporal (por ejemplo, `/etc/X11/xorg.conf.fglrx`. La próxima vez que iniciemos X, se utilizará el controlador Intel por defecto en lugar de fglrx.

Para iniciar un servidor X secundario usando fglrx, simplemente movemos `xorg.conf` de nuevo al lugar que le corresponde (`/etc/X11/xorg.conf`) antes de iniciar X. Este método permite incluso intercambiarlo entre las sesiones de X. Cuando hayamos terminado de usar fglrx, moveremos `xorg.conf` a otro lugar de nuevo.

La única desventaja de este método es no tener aceleración 3D usando el controlador de Intel. La aceleración 2D, sin embargo, es completamente funcional. Aparte de ello, esto nos dará un escritorio completamente estable.

#### Problemas con PowerXpress en portátiles ejecutándose en modalidad AMD (pxp_switch_catalyst amd) con monitor externo / secundario

Cuando se utiliza PowerXpress en un portatil en modalidad AMD únicamente (es decir, configurada la tarjeta dedicada para hacerlo todo) se obtienen a veces problemas con el artifacting/duplicating entre pantallas. Este es un problema conocido, y parece afectar a tarjetas de la serie 7xxxM.

El artifacting desaparece cuando se pasa uno de los monitores bien sea a rotating o a scaling. Así que se puede usar xrandr para solucionar este problema:

 `xrandr --output HDMI1 --left-of LVDS1 --primary --scale 1x1 --output LVDS1 --scale 1.0001x1.0001` 

## Repositorios Xorg

Es notoria la lentitud del proceso de actualización de Catalyst. En consecuencia, es normal que una versión nueva de Xorg rompa la compatibilidad para el controlador Catalyst. Esto significa que los usuarios de Catalyst o bien deben retener la actualización de los paquetes de Xorg, o usar un repositorio backports que solo contenga los paquetes Xorg compatibles. Vi0L0 ha permitido realizar esta tarea y proporciona varios repositorios backports.

Si desea utilizar los repositorios backports, tiene que editar `/etc/pacman.conf` y añadir la información del repositorio **por encima de todos los demás repositorios**, incluso por encima de su repositorio Catalyst, y debería añadir solo uno.

### [xorg114]

Catalyst no soporta xorg-server 1.15.

```
[xorg114]
Server = http://catalyst.wirephire.com/repo/xorg114/$arch

```

### [xorg113]

Catalyst < 13.6 no soporta xorg-server 1.14.

```
[xorg113]
Server = http://catalyst.wirephire.com/repo/xorg113/$arch

```

### [xorg112]

La versión < 12.10 de Catalyst no soporta xorg-server 1.13.

```
[xorg112]
Server = http://catalyst.apocalypsus.net/repo/xorg112/$arch

```

## Herramientas

### Catalyst-hook

[Catalyst-hook](https://aur.archlinux.org/packages/Catalyst-hook/) es un servicio de [systemd](/index.php/Systemd_(Espa%C3%B1ol) "Systemd (Español)") que recompilará automáticamente los módulos fglrx mientras el sistema se apaga o se reinicia, pero solo si es necesario (por ejemplo, después de una actualización).

Antes de utilizar este paquete debe asegurarse de que tanto el grupo [base-devel](https://www.archlinux.org/groups/x86_64/base-devel/), como el paquete [linux-headers](https://www.archlinux.org/packages/?name=linux-headers) (el específico al kernel que usa) están instalados.

Para habilitar la actualización automática, active el servicio `catalyst-hook.service`:

```
# systemctl enable catalyst-hook
# systemctl start catalyst-hook

```

También puede utilizar este paquete para compilar el módulo `fglrx` manualmente. Basta con ejecutar el script `catalyst_build_module` después de que el kernel ha sido actualizado:

```
# catalyst_build_module all

```

**Algunos detalles técnicos adicionales:**

El servicio `catalyst-hook.service` detiene el «flujo» de systemd y le obliga a esperar hasta que catalyst-hook termine su trabajo.

El servicio `catalyst-hook.service` llama a la función `catalyst_build_module check` que comprueba si la reconstrucción de `fglrx` es realmente necesaria.

La función `check` comprueba si existe el módulo `fglrx`, de modo que:

*   Si no existe, lo construirá;

*   Si existe, comparará los dos valores para asegurarse de que la reconstrucción es necesaria.

Estos valores son los md5sums del archivo `/usr/lib/modules/<kernel_version>/build/Module.symvers` (porque, Vi0L0, advirtió que este archivo es único y diferente para cada versión del kernel). El primer valor es la suma md5 del archivo `Module.symvers` existente. El segundo valor es la suma md5 del archivo `Module.symvers` que existe en el momento de creación del módulo `fglrx`. Este valor fue compilado en el módulo `fglrx` por un script `catalyst_build_module`.

Si los valores son diferentes, se compila el módulo `fglrx` nuevo.

La verificación es comprobar el conjunto de directorios de `/usr/lib/modules/` y los módulos de compilación para todos los kernels instalados, si es necesario. Si la compilación o reconstrucción no es necesaria, todo el proceso no lleva más de unos milisegundos para completarse, antes de que sea terminado por systemd.

### Catalyst-generator

[catalyst-generator](https://aur.archlinux.org/packages/catalyst-generator/) es un paquete capaz de construir e instalar los módulos `fglrx` generando un paquete `catalyst-${kernver}` accesible por pacman. La diferencia de Catalyst-hook es que se tendrá que activar esta orden manualmente, mientras Catalyst-generator lo hará automáticamente en el arranque cuando advierta un nuevo kernel instalado.

Cree el paquete `catalyst-${kernver}` usando [makepkg](/index.php/Makepkg "Makepkg") e instálelo con el auxilio de [pacman](/index.php/Pacman "Pacman"). `${kernver`} es la versión del kernel con el cual se compiló el paquete (por ejemplo, el paquete catalyst-2.6.35-ARCH fue compilado para el kernel 6.2.35-ARCH).

Para compilar e instalar el paquete `catalyst-${kernver}` para el kernel actualmente en ejecución, como usuario sin privilegios (no como root, método más seguro), escriba: `catalyst_build_module` . Se le pedirá la contraseña de root para continuar con la instalación del paquete.

Un breve resumen de cómo usar este paquete:

1.  Como root: `catalyst_build_module remove`. Esto eliminará todos los paquetes `catalyst-{kernver}` no utilizados.
2.  Como usuario sin privilegios: `catalyst_build_module ${kernver}`, donde `${kernver}` es una versión del kernel que acaba de actualizar. Por ejemplo: `catalyst_build_module 2.6.36-ARCH`. También es posible compilar `catalyst-{kernver}` para todos los kernels instalados usando `catalyst_build_module all`.
3.  Si desea eliminar `catalyst-generator`, lo mejor es ejecutar, antes de quitar catalyst-generator, como root: `catalyst_build_module remove_all`. **Esto eliminará todos los paquetes `catalyst-{kernver}` del sistema.**

`Catalyst-generator` no es capaz de eliminar todos esos paquetes `catalyst-{kernver}` automáticamente mientras es eliminado porque no puede haber más de una instancia de pacman ejecutándose simultáneamente. Si se ha olvidado de ejecutar `# catalyst_build_module remove_all` antes de ejecutar `# pacman -R catalyst-generator`, catalyst-generator le dirá qué paquetes `catalyst-{kernver}` tiene que eliminar manualmente después de la eliminación de catalyst-generator.

Catalyst-generator es la solución más segura y amistosa, porque:

1.  se puede utilizar el usuario normal para compilar el paquete;
2.  los módulos se compilan en un entorno fakeroot;
3.  los archivos no están esparcidos en cualquier lugar; el gestor de paquetes siempre sabe donde están;
4.  lo único que hay que hacer es recordar usarlo.

**Nota:** Si ve estas advertencias:
```
**WARNING:** Package contains reference to $srcdir

```

```
**WARNING:** '.pkg' is not a valid archive extension.

```
mientras compila el paquete `catalyst-{kernver}`, no se preocupe, es normal.

## Características

### Prestación «Tear Free»

Presentado en **Catalyst 11.1**, la función *Tear Free Desktop* reduce el desgarro en aplicaciones 2D, 3D y de vídeo. Es probable que a esto se sume el triple-buffering y v-sync. Tenga en cuenta que requiere un suplemento adicional de recursos de la GPU.

Para activar 'Tear Free Desktop' ejecute `amdcccle` y vaya a: `Display Options` → `Tear Free`.

O ejecute como root:

```
# aticonfig --set-pcs-u32=DDX,EnableTearFreeDesktop,1

```

Para desactivarlo, use también `amdcccle`, o ejecute como root:

```
# aticonfig --del-pcs-key=DDX,EnableTearFreeDesktop

```

### Aceleración de vídeo

**[Aceleración de Vídeo API](https://en.wikipedia.org/wiki/Video_Acceleration_API "wikipedia:Video Acceleration API") (VA API)** es una biblioteca de software de código abierto (libVA) adherida a la especificación API que proporciona una aceleración de la GPU para el procesamiento del contenido de vídeo en sistemas operativos basados en Linux/UNIX. El proceso funciona al permitir la decodificación de video acelerada mediante hardware en varios puntos de entrada (VLD, IDCT, Compensación de movimiento, desbloqueo) para los estándares de codificación comunes (MPEG-2, MPEG-4 ASP/H.263, MPEG-4 AVC/H.264 , y VC-1/WMV3).

VA-API ha ganado una nueva patente propietaria (en noviembre 2009) llamada [xvba-video](https://aur.archlinux.org/packages/xvba-video/), que permite a las aplicaciones habilitar el uso de VA-API para aprovechar el chipset AMD Radeon chipsets UVD2 mediante la biblioteca [XvBA (X-Video Bitstream Acceleration API) de AMD)](https://en.wikipedia.org/wiki/XvBA "wikipedia:XvBA").

El soporte a XvBA y a xvba-video está todavía en desarrollo, sin embargo, **está funcionando muy bien en la mayoría de los casos**. Compile (o instale desde el repositorio de Vi0L0) el paquete privativo [xvba-video](https://aur.archlinux.org/packages/xvba-video/), o, si tiene problemas con esta versión, instale [libva-xvba-driver](https://aur.archlinux.org/packages/libva-xvba-driver/); y también instale [mplayer-vaapi](https://aur.archlinux.org/packages/mplayer-vaapi/) y [libva](https://www.archlinux.org/packages/?name=libva). A continuación, ajuste el reproductor de vídeo para utilizar el parámetro vaapi:gl como salida de vídeo:

```
$ mplayer -vo vaapi:gl movie.avi

```

Estas opciones se pueden añadir al archivo de configuración mplayer, consulte [MPlayer](/index.php/MPlayer "MPlayer").

Para **smplayer**:

```
Opciones → Preferencias → General → Video (pestaña) → Controlador de salida: Definido por el usuario : vaapi:gl
Opciones → Preferencias → General → Video (pestaña) → Doble buffering **on**
Opciones → Preferencias → General → General → Imágenes → Rotar imágenes screenshots **off**
Opciones → Preferencias → Rendimiento → Temas para decodificar **1** (para desactivar el parámetro -lavdopts)

```

**Nota:** Si Tear Free Desktop está activada, es mejor utilizar:
```
Opciones → Preferencias → General → Video (pestaña) → Controlador de salida: vaapi

```

Si la salida de vídeo **vaapi:gl** no funciona, por favor, compruebe:

```
**vaapi**, **vaapi:gl2** o simplemente **xv(0 - AMD Radeon [AVIVO Video](https://en.wikipedia.org/wiki/Avivo "wikipedia:Avivo"))**.

```

Para **VLC**:

```
Herramientas → Preferencias → Input & Codecs → Use decodificar aceleración GPU

```

Podría ayudar a activar v-sync en **amdcccle**:

```
3D → Otras configuraciones → Wait for vertical refresh = Always On

```

**Note:** Si utiliza **Compiz/KWin**, la única forma de **evitar el parpadeo de vídeo** es ver vídeos en **pantalla completa**, y solo cuando **Unredirect Fullscreen está desactivada**. En **compiz** es necesario establecer **Redirected Direct Rendering** en las Opciones Generales de ccsm. Si todavía parpadea, trate desactivando esta opción en CCSM. Viene desactivada de forma predeterminada en **KWin**, pero si sigue viendo parpadeos pruebe alternando la opción on/off del parámetro «Suspender los efectos de escritorio de las ventanas a pantalla completa» o desactivarlo en `Configuración del sistema` → `Efectos de escritorio` → `Avanzado`.

### Frecuencia GPU/Mem, Temperatura, Velocidad del ventilador, utilidades Overclocking

Se pueden obtener los relojes de la GPU/Mem con: `$ aticonfig --od-getclocks`.

Se puede obtener la velocidad del ventilador con: `$ aticonfig --pplib-cmd "get fanspeed 0"`

Se puede obtener la temperatura con: `$ aticonfig --odgt`

Para establecer la velocidad del ventilador con: `$ aticonfig --pplib-cmd "set fanspeed 0 50"` Índice de Consulta: 50, velocidad en porcentaje

Para operaciones de overclock y/o underclock es más fácil utilizar algún GUI, como **ATi Overclocking Utility**, que es muy simple de usar pero requiere la biblioteca qt para funcionar. Podría estar desactualizado/anticuado, pero se puede conseguir [aquí](http://kde-apps.org/content/show.php/ATI+Overclock?content=47796).

Otra utilidad, más compleja, para llevar a cabo este tipo de operaciones es **AMDOverdriveCtrl**. Su página web es [esta](http://sourceforge.net/projects/amdovdrvctrl) y se puede obtener un paquete compilado para Arch desde [AUR](https://aur.archlinux.org/packages.php?ID=45298) o desde los repositorios no oficiales de Vi0L0.

### Doble Pantalla (Dual Head / Dual Screen / Xinerama)

#### Introducción

**Advertencia:** Tiene que saber que no existe una solución única, las configuraciones son diferentes para adaptarse a diversas necesidades. Es por eso que tiene que adaptar los siguientes pasos a sus propias necesidades. Es posible que se tenga que probar más de una vez. **Por lo tanto, debe guardar la configuración realizada al archivo `/etc/X11/xorg.conf` antes de realizar cualquier nuevo cambio y debe ser capaz de recuperar dicha configuración desde un entorno de línea de órdenes.**

*   En esta parte, vamos a describir la instalación de dos pantallas de tamaño diferentes en una sola tarjeta gráfica con dos puertos de salida diferentes (DVI + HDMI) con la configuración "Big desktop".

*   La solución Xinerama tiene algunos inconvenientes, sobre todo porque no es compatible con XrandR. Por esa misma razón, no se debe utilizar ahora, porque XrandR es solo un recurso que utilizaremos más tarde en nuestra configuración.

*   La solución "Dual Head" le permitiría tener dos sesiones distintas (una para cada pantalla). Podría ser esto preferible, pero no será capaz de mover ventanas de una pantalla a otra. Si solo dispone de una pantalla, tendrá que definir el ratón dentro de Xorg para las 2 sesiones dentro de la sección Server Layout.

[Documentación ATI](http://support.amd.com/us/kbarticles/Pages/1105-HowCanIConfigureMultip.aspx)

#### ATI Catalyst Control Center

La herramienta GUI proporcionada por ATI es muy útil y vamos a tratar de usarla tanto como nos sea posible. Para iniciarla, abra un terminal y utilice la siguiente línea de órdenes:

```
$ {kdesu/gksu} amdcccle

```

**Advertencia:** **No** utilice sudo directamente con la interfaz gráfica de usuario amdcccle. Sudo le da derechos de administrador pero con la información de la cuenta de usuario. En su lugar, utilice gksu (GNOME) o kdesu (KDE).

#### Instalación

Este paso es fácil, pero importante: asegúrese de que el hardware está conectado correctamente y que usted conoce sus caracteristicas fundamentales (dimensiones de la pantalla, tamaños, tasa de refresco, etc.). Normalmente, las dos pantallas se reconocen en el momento del arranque pero no siempre su configuración resulta ser correcta, especialmente si se está usando un archivo de configuración base de Xorg (`/etc/X11/xorg.conf`) pero se cuenta con la función hot-plugging.

El primer paso es asegurarse de que las pantallas serán reconocidas por su DE y por X. Para ello, es necesario generar un archivo de configuración Xorg básico para sus dos pantallas:

```
# aticonfig --initial --desktop-setup=horizontal --overlay-on=1

```

o

```
# aticonfig --initial=dual-head --screen-layout=left

```

**Nota:** `overlay` es importante porque le permite tener un pixel (o más) compartido entre las dos pantallas.

**Sugerencia:** Para las diferentes opciones posibles y disponibles, no dude en escribir `aticonfig --help` en un terminal para mostrar todas las líneas de órdenes disponibles.

Normalmente, ahora tendrá un archivo básico que podrá editar para añadir las resoluciones de pantalla deseadas. Es importante utilizar la resolución precisa, especialmente si tiene pantallas de diferentes tamaños. Estas resoluciones tienen que ser añadidas en la sección "Screen":

```
SubSection "Display"
   Depth 24
   Modes "X-resolution screen 1xY-resolution screen 1" "Xresolution screen 2xY-resolution screen 2"
EndSubSection

```

A partir de ahora, en lugar de editar el archivo `xorg.conf` manualmente, vamos a utilizar la herramienta GUI de ATI. Reinicie X para asegurarse de que sus dos pantallas están bien soportados y que la resolución es correcta. (Las pantallas deben ser independientes).

#### Configuración

En este caso, es suficiente lanzar el ATI Control Center con privilegios de root, entrar en el menú de pantalla y elegir la configuración que se prefiera para su sistema (flecha pequeña en el menú desplegable). Terminado, reinicie X y ¡todo debería funcionar!

Antes de reiniciar X, compruebe su nuevo archivo `xorg.conf`. En este punto, dentro de la subsección "Display" de la sección "Screen", debería ver la línea de órdenes "Virtual", en la que la resolución debería ser la suma de las dos pantallas. La sección "Server Layout" contiene el resto.

## Desinstalación

Si desea instalar el driver de código abierto y previamente estaba usando y, por lo tanto, tenía instalado, el driver propietario (catalyst), lo primero que es necesario hacer es remover catalyst. Básicamente, necesita quitar los paquetes `catalyst` y `catalyst-utils`. También debe eliminar los paquetes [catalyst-generator](https://aur.archlinux.org/packages/catalyst-generator/), [catalyst-hook](https://aur.archlinux.org/packages/catalyst-hook/) y [lib32-catalyst-utils](https://aur.archlinux.org/packages/lib32-catalyst-utils/) si han sido instalado en el sistema.

**Advertencia:**

*   Es posible que necesite usar `# pacman -Rdd` para eliminar [catalyst-utils](https://aur.archlinux.org/packages/catalyst-utils/) (y​​/o [lib32-catalyst-utils](https://aur.archlinux.org/packages/lib32-catalyst-utils/)) porque esos paquetes contienen archivos relacionados con *gl* y muchos de los paquetes presentes en su sistema dependen de ellos. Estas dependencias serán satisfechas nuevamente al instalar [xf86-video-ati](https://www.archlinux.org/packages/?name=xf86-video-ati).
*   Es posible que tenga que quitar `/etc/profile.d/ati-flgrx.sh` y `/etc/profile.d/lib32-catalyst` (si existe en su sistema), de lo contrario `r600_dri.so` no se cargará y no tendrá soporte 3D.

**Nota:** Debe eliminar los reporitorios no oficiales que se mencionan en la página wiki [ATI Catalyst](/index.php/ATI_Catalyst_(Espa%C3%B1ol) "ATI Catalyst (Español)") del archivo `/etc/pacman.conf` y ejecutar `pacman-Syu`, porque esos depósitos contienen paquetes Xorg obsoletos para el uso de `catalyst` y el paquete [xf86-video-ati](https://www.archlinux.org/packages/?name=xf86-video-ati) necesita los paquetes de Xorg más actualizados presentes en los [Repositorios Oficiales](/index.php/Repositorios_Oficiales "Repositorios Oficiales")

También puede seguir estos pasos:

*   Si tiene un archivo `/etc/modprobe.d/blacklist-radeon.conf`, elimine o comente la línea `blacklist radeon` contenida en ese archivo.
*   Si tiene un archivo en `/etc/modules-load.d` para cargar el módulo `fglrx` en el arranque, elimine o comente la línea que contiene `fglrx`.
*   Asegúrese de quitar el antiguo `/etc/X11/xorg.conf`
*   Si ha instalado el paquete [catalyst-hook](https://aur.archlinux.org/packages/catalyst-hook/), asegúrese de desactivar el servicio de systemd.

*   Si utiliza la opción `nomodese` en su [archivo de configuración](/index.php/Boot_Loader#Configuration_files "Boot Loader") en la línea de parámetros del kernel y va a utilizar [KMS](#Kernel_mode-setting_.28KMS.29), retírelo.
*   **Reinicie** antes de instalar el otro controlador.

## Solución de problemas

Si todavía puede arrancar desde la línea de órdenes, entonces el problema, probablemente, se encuentra en `/etc/X11/xorg.conf`

Se puede analizar el conjunto `/var/log/Xorg.0.log` o, buscar pistas con:

```
$ grep '(EE)' /var/log/Xorg.0.log
$ grep '(WW)' /var/log/Xorg.0.log

```

Si no sabe qué hacer, puede publicar un mensaje en la sede de [support de los foros](https://bbs.archlinux.org/viewtopic.php?pid=1166052#p1166052/). Cuando lo haga, por favor proporcione la información que se obtiene de ambas órdenes mencionados anteriormente.

### Aplicaciones 3D en Wine congeladas

Si utiliza una aplicación 3D con wine y se bloquea, hay que desactivar TLS. Para ello utilice, o bien `aticonfig` o modifique `/etc/X11/xorg.conf`. Para usar `aticonfig`:

```
# aticonfig --tls=off

```

O, para modificar `/etc/X11/xorg.conf`: en primer lugar, con privilegios de root, abra el archivo y añada `Option "UseFastTLS" "off"` para la sección *Device* de este archivo.

Después de aplicar cualquiera de las dos soluciones, reinicie X para que surta efecto.

### Problemas con los colores de vídeo

Se puede usar todavía `vaapi:gl` para evitar el parpadeo de vídeo, pero sin aceleración de vídeo:

*   Ejecute **mplayer** sin la opción `-vo vaapi`.

*   Ejecute **smplayer** y remueva `-vo vaapi` de las Opciones → Preferencias → Avanzado → Opciones de MPlayer → Opciones: -vo vaapi

Además, para **smplayer** ahora puede convertir imágenes en forma segura.

### KWin y composite

Se puede utilizar XRender si la prestación con OpenGL es lenta. Sin embargo, XRender también podría ser más lento que OpenGL dependiendo de su tarjeta. XRender también resuelve los problemas aparatos gráficos en algunos casos.

### Pantalla en negro con bloqueos completos al reiniciar el sistema o startx

Asegúrese de que ha añadido la opción **nomodeset** a la línea de opciones del kernel en el gestor de arranque (consulte [esta sección](#Desactivar_kernel_mode_setting)).

Si se está utilizando el controlador legacy (`catalyst-hd234k`) y obtener una pantalla en negro, pruebe haciendo downgrading de xorg-server a 1.11 usando el repositorio [#xorg111](/index.php/AMD_Catalyst_(Espa%C3%B1ol)#.5Bxorg111.5D "AMD Catalyst (Español)").

#### Llamadas hardware ACPI defectuosa

Es posible que fglrx no coopere bien con las llamadas hardware ACPI del sistema, por lo que se deshabilita él mismo y no hay salida de pantalla.

Así que trate de ejecutar esto:

```
$ aticonfig --acpi-services=off

```

### KDM desaparece después de cerrar la sesión

Si está ejecutando el controlador propietario Catalyst y se obtiene una consola (tty1) en lugar de la pantalla de KDM cuando se cierra la sesión, debe indicar a KDM que reinicie el servidor X después de cada cierre de sesión. Descomente la línea siguiente en la sección titulada `[X-:*-Core]`:

 `/usr/share/config/kdm/kdmrc`  `TerminateServer=True` 

KDM debe aparecer al cerrar la sesión de KDE.

### Direct Rendering no funciona

El problema puede producirse cuando se utiliza el controlador propietario **Catalyst**.

**Advertencia:** Este error también aparece si no **reinicia** el sistema después de la instalación o actualización de catalyst. El sistema tiene que cargar el módulo fglrx.ko con el fin de hacer funcionar al controlador.

Si se tiene un problema con direct rendering, ejecute en un terminal:

```
$ LIBGL_DEBUG=verbose glxinfo > /dev/null

```

Se obtendrá una salida en cuyo inicio, por lo general, se va a mostrar un mensaje de error diciendo que no se tiene direct rendering.

Los errores más comunes y sus soluciones, son los siguientes:

```
libGL error: XF86DRIQueryDirectRenderingCapable returned false

```

*   Asegúrese de que está cargando los módulos correctos agp para su chipset AGP antes de cargar el módulo del kernel `fglrx`. Para determinar qué módulos agp necesita, ejecute `hwdetect --show-agp`. A continuación, abra el archivo `/etc/modules-load.d/fglrx.conf` y añada el módulo agp en una línea **previa** a `fglrx`.

```
libGL error: failed to open DRM: Operation not permitted
libGL error: reverting to (slow) indirect rendering

```

```
libGL: OpenDriver: trying /usr/lib/xorg/modules/dri//fglrx_dri.so
libGL error: dlopen /usr/lib/xorg/modules/dri//fglrx_dri.so failed
(/usr/lib/xorg/modules/dri//fglrx_dri.so: cannot open shared object file: No such file or directory)
libGL error: unable to find driver: fglrx_dri.so

```

*   Asegúrese de que todo ha sido instalado correctamente. Si la salida en el mensaje de error es `/usr/X11R6/lib/modules/dri/fglrx_dri.so`, ahora, asegúrese de salir completamente del sistema y entre de nuevo. Si está utilizando un gestor de pantalla (gdm, kdm, xdm), asegúrese de que `/etc/profile` se vuelva cada vez que inicie sesión. Esto generalmente se logra mediante la adición de `source /etc/profile` en `~/.xsession` o `~/.xinitrc`, no obstante lo cual esto puede variar entre los distintos administradores de inicio de sesión.

*   Si entre las rutas anteriores de su mensaje de error *está* `/usr/lib/xorg/modules/dri/fglrx_dri.so`, entonces algo no está bien instalado. Pruebe volviendo a instalar el paquete [catalyst](https://aur.archlinux.org/packages/catalyst/).

Errores tales como:

```
fglrx: libGL version undetermined - OpenGL module is using glapi fallback

```

podría ser causado por tener múltiples versiones de `libGL.so` en su sistema. La siguiente orden debería devolver la siguiente salida:

 `$ locate libGL.s` 
```
 /usr/lib/libGL.so
 /usr/lib/libGL.so.1
 /usr/lib/libGL.so.1.2

```

Estos son los tres únicos archivos libGL.so que debe tener en su sistema. Si tiene alguno más (por ejemplo `/usr/X11R6/lib/libGL.so.1.2`), entonces elimínelos. Esto debería solucionar el problema.

Hay casos que no se muestran errores que indiquen la presencia de un problema. Si se está usando X11R7, asegúrese de **no** tener estos archivos en su sistema:

```
/usr/X11R6/lib/libGL.so.1.2
/usr/X11R6/lib/libGL.so.1

```

### Problemas con la hibernación y la suspensión

#### Vídeo no reanuda desde suspend2ram

El controlador propietario ATI Catalyst no se puede reanudar desde la suspensión si el framebuffer está habilitado. Para desactivar el framebuffer, añada `vga=0` a las opciones de los [parámetros del kernel](/index.php/Kernel_parameters_(Espa%C3%B1ol) "Kernel parameters (Español)").

Para ver dónde es necesario agregar esto con otros gestores de arranque, consulte [#Desactivar kernel mode setting](#Desactivar_kernel_mode_setting).

### Bloqueo del sistema/Hard lock

*   El driver del framebuffer `radeonfb` es conocido por causar problemas de esta naturaleza. Si el kernel está compilado con el soporte radeonfb, puede ser útil probar un kernel diferente y ver si esto resuelve el problema.

*   Si se experimenta bloqueos del sistema al salir de su DE (apagar, suspender, cambiar a tty, etc.) probablemente se olvidó de desactivar KMS. (Consulte [#Desactivar kernel mode setting](#Desactivar_kernel_mode_setting)).

### Conflictos con el hardware

La tarjeta radeon usada conjuntamente con alguna versión del chipset nForce3 (por ejemplo, nForce 3 250Gb) no proporciona aceleración 3D. Actualmente la causa de este problema es desconocida, pero algunas fuentes indican que puede ser posible obtener la aceleración con esta combinación de hardware mediante el arranque de Windows con los controladores de NVIDIA y luego reiniciar el sistema. Si obtiene algo similar a esto (usando un sistema basado en nForce3):

 `$ dmesg | grep agp` 
```
agpgart: Detected AGP bridge 0
agpgart: Setting up Nforce3 AGP.
agpgart: aperture base > 4G

```

y también si la emisión de la siguiente orden muestra el siguiente resultado:

 `$ tail -n 100 /var/log/Xorg.0.log | grep agp`  ` (EE) fglrx(0): [agp] unable to acquire AGP, error "xf86_ENODEV"` 

Entonces efectivamente tiene este error.

Algunas fuentes indican que, en algunas situaciones, es útil hacer un downgrade de la BIOS de la placa base, pero esto no se ha podido comprobar en todos los casos. Además, **un mal downgrade de la BIOS puede hacer inutilizable su hardware, así que preste atención.**

Consulte [este bugreport](http://bugzilla.kernel.org/show_bug.cgi?id=6350/) para más información y posibles soluciones.

### Bloqueos temporales durante la reproducción de vídeo

Este problema puede producirse cuando se utiliza el driver Catalyst propietario.

Si usted experimenta cuelgues temporales de unos segundos a varios minutos de duración que ocurren al azar durante la reproducción de mplayer, compruebe /var/log/messages.log buscando una salida como:

```
Nov 28 18:31:56 pandemonium [<c01c64a6>] ? proc_get_sb+0xc6/0x160
Nov 28 18:31:56 pandemonium [<c01c64a6>] ? proc_get_sb+0xc6/0x160
Nov 28 18:31:56 pandemonium [<f8bc628c>] ? ip_firegl_ioctl+0x1c/0x30 [fglrx]
Nov 28 18:31:56 pandemonium [<c01c64a6>] ? proc_get_sb+0xc6/0x160
Nov 28 18:31:56 pandemonium [<c0197038>] ? vfs_ioctl+0x78/0x90
Nov 28 18:31:56 pandemonium [<c01970b7>] ? do_vfs_ioctl+0x67/0x2f0
Nov 28 18:31:56 pandemonium [<c01973a6>] ? sys_ioctl+0x66/0x70
Nov 28 18:31:56 pandemonium [<c0103ef3>] ? sysenter_do_call+0x12/0x33
Nov 28 18:31:56 pandemonium [<c01c64a6>] ? proc_get_sb+0xc6/0x160
Nov 28 18:31:56 pandemonium =======================

```

Añada la opción nopat kernel a las opciones del kernel en el gestor de arranque y reinicie. Para ver cómo hacer esto para gestores de arranque diferente, consulte [#Desactivar kernel mode setting](#Desactivar_kernel_mode_setting).

### «aticonfig: No supported adaptaters detected»

Si se obtiene lo siguiente:

 `# aticonfig --initial` 
```
aticonfig: No supported adapters detected

```

Pero tiene una AMD GPU (o APU), todavía es posible hacer funcionar Catalyst estableciendo manualmente el dispositivo en el propio archivo `etc/X11/xorg.conf` o copiando un archivo `/etc/ati/control` para que funcione posteriormente (preferible -esto también corrige el problema de la marca de agua-).

Para obtener un archivo de control ulterior, descargue desde AMD una versión anterior de fglrx y ejecútelo con el parámetro `--extract driver`. Encontrará el archivo de control en `driver/common/etc/ati/control`. Copie el archivo extraído en el archivo del sistema y reinicie Xorg. Se pueden probar diferentes versiones del archivo.

Para establecer el propio modelo en `xorg.conf`, modifique la sección «device» de `/etc/X11/xorg.conf` a:

 `/etc/X11/xorg.conf` 
```
Section "Device"
        Identifier "ATI radeon ********"
        Driver     "fglrx"
EndSection

```

Donde `****` debería sustituirse por el número de comercialización de su dispositivo (por ejemplo, 6870 para la HD 6870 y 6310 para la APU E-350).

Xorg ahora se iniciará y será posible utilizar `amdcccle` en lugar de `aticonfig`. Puede mostrar el siguiente aviso: «AMD Unsupported hardware».

Es posible quitar el aviso utilizando el siguiente script:

```
#!/bin/sh
DRIVER=/usr/lib/xorg/modules/drivers/fglrx_drv.so
for x in $(objdump -d $DRIVER|awk '/call/&&/EnableLogo/{print "\\x"$2"\\x"$3"\\x"$4"\\x"$5"\\x"$6}'); do
 sed -i "s/$x/\x90\x90\x90\x90\x90/g" $DRIVER
done

```

y reiniciando.

### Soporte WebGL en Chromium

Google introduce en blacklist el controlador Catalyst para Linux con el fin de dar apoyo a la aceleración webGL en los navegadores Chromium/Chrome.

Puede obviar esto editando y añadiendo el parámetro `--ignore-gpu-blacklist` en la línea `Exec`, de modo que se vea así:

 `/usr/share/applications/chromium.desktop`  `Exec=chromium %U **--ignore-gpu-blacklist**` 

También puede ejecutar chromium desde consola con el mismo parámetro `--ignore-gpu-blacklist`:

```
$ chromium **--ignore-gpu-blacklist**

```

**Advertencia:** Catalyst no es compatible con la extensión `GL_ARB_robustness`, así que es posible que un sitio malicioso podría utilizar WebGL para realizar un ataque DoS en la tarjeta gráfica.

### Retardos y bloqueos en vídeos flash con el flashplugin de Adobe

Edite:

 `/etc/adobe/mms.cfg` 
```
#EnableLinuxHWVideoDecode=1
OverrideGPUValidation=true
```

Si está usando KDE, asegúrese de que la opción «suspender los efectos del escritorio para la pantalla completa de las ventanas» no está marcada en `Preferencias del sistema` → `Efectos del escritorio` → `Avanzado`.

### Retardos en el movimiento de ventanas en GNOME3

Puede probar esta solución, funciona para muchos usuarios.

Añada esta línea en `~/.profile` o en `/etc/profile`:

```
export CLUTTER_VBLANK=none

```

Reinicie el servidor X o reinicie el sistema.

### Imposible utilizar pantalla completa con resolución 1920x1080

Usando la interfaz amdcccle es posible seleccionar la pantalla, vaya a ajustes, y configure Underscan a 0% (por defecto está en 15%).

Como alternativa, puede desactivar underscanning usando `aticonfig`:

```
aticonfig --set-pcs-val=MCIL,DigitalHDTVDefaultUnderscan,0

```

Para la versión más reciente (por ejemplo, 12.11), si Catalyst control center falla repetidamente al guardar la configuración de overscan, modifique `/etc/ati/amdpcsdb`:

 `/etc/ati/amdpcsdb`  `TVEnableOverscan=V0` 

Después salga y reinicie sesión.

### Configuración de pantalla dual: problemas generales con aceleración, OpenGL, composición, funcionamiento

Trate de desactivar xinerama y xrandr12\. Eche un vistazo al siguiente ejemplo y proceda de la misma manera:

Como usuario root, escriba las siguientes órdenes:

```
aticonfig --initial
aticonfig --set-pcs-str="DDX,EnableRandR12,FALSE"

```

A continuación, reinicie el sistema. En el archivo `/etc/X11/xorg.conf` compruebe que xinerama está desactivado, si no es así desactívelo y reinicie el sistema.

Posteriormente, ejecute `amdcccle` y configúrelo: amdcccle → gestor de pantalla → multipantalla → escritorio multipantalla con 2 pantalla(s).

Reinicie de nuevo y proceda a configurar el diseño de pantalla como desee.

### Desactivar características VariBright

Como usuario root escriba la orden:

```
aticonfig --set-pcs-u32=MCIL,PP_UserVariBrightEnable,0

```

### Hybrid/PowerXpress: apagar la GPU dedicada

Cuando se utiliza [catalyst-total-pxp](https://aur.archlinux.org/packages/catalyst-total-pxp/) o catalyst-utils-pxp y se cambia a la GPU integrada es posible que observe que la GPU dedicada sigue trabajando, consumiendo energía y aumentando la temperatura del equipo.

A veces, esto es, cuando la GPU integrada es una Intel, puede usar `vgaswitcheroo` para apagar la GPU dedicada. Por desgracia, esto no siempre funciona.

En este caso, puede comprobar [acpi_call](https://aur.archlinux.org/packages/?O=0&K=acpi_call). MrDeepPurple ha preparado el script para llevar a cabo esta tarea de 'apagado', este script es llamado a través de un servicio systemd durante el arranque y la reanudación del sistema. He aquí este script:

```
#!/bin/sh
libglx=$(/usr/lib/fglrx/switchlibglx query)
modprobe acpi_call
if [ "$libglx" = "intel" ]; then
echo '\_SB.PCI0.PEG0.PEGP._OFF' > /proc/acpi/call
fi

```

### Al intercambiar desde una sesión X a TTY nos da una pantalla en blanco

Una solución para esta «característica», que apareció en catalyst 13.2 betas, es utilizar la opción `vga=` del kernel, como `vga=792`. Se puede obtener la lista de las resoluciones soportadas con la orden:

```
hwinfo --framebuffer

```

Recoja una de las resoluciones más bajas, y cópiela y péguela en la línea del kernel del gestor de arranque, de modo que podría quedar como sigue: `vga=0x03d4`.

### Error: 30 FPS / Tear-Free / V-Sync

Error introducido en Catalyst 13.6 beta, no arreglado por el momento (13.9).

Después de activar la característica «Tear-Free» todas las aplicaciones OpenGL recién iniciadas se ralentizan, a menudo generando solo 30 FPS, que también afecta la composición del escritorio.

La solución del problema es bastante simple y se encontró por M132\. Aquí están los pasos, con la aplicación «AMD Catalyst Control Center» (amdcccle):

```
1\. Activar Tear-Free, estableciendo la opción 3D V-Sync en  «Always on».
2\. Ajustar 3D V-Sync en «Always Off».
3\. Asegúrese de que Tear-Free está encendido.
4\. Reiniciar X o reiniciar sesión.

```

Está trabajando bien en KDE 4.11.x, pero, en caso de problemas, M132 sugiere: "Pruebe a desactivar «Detect refresh rate» y especifique la frecuencia de actualización del monitor en el complemento Composite".

## Véase también

*   [Unofficial Wiki for the ATI Linux Driver](http://wiki.cchtml.com/index.php/Main_Page)
*   [Unofficial ATI Linux Driver Bugzilla](http://ati.cchtml.com/query.cgi)