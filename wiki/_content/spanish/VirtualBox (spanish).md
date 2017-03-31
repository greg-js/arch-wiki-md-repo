[VirtualBox](https://www.virtualbox.org) es un [hipervisor](https://en.wikipedia.org/wiki/es:Hypervisor "wikipedia:es:Hypervisor") que se utiliza para ejecutar sistemas operativos en un entorno especial, llamado máquina virtual, corriendo sobre un sistema operativo ya existente. VirtualBox está en constante desarrollo y las nuevas características se implementan continuamente. Viene con una interfaz gráfica basada en [Qt](/index.php/Qt "Qt"), así como herramientas de línea de órdenes [SDL](https://en.wikipedia.org/wiki/Simple_DirectMedia_Layer "wikipedia:Simple DirectMedia Layer") y *headless* para la gestión y ejecución de máquinas virtuales.

Con el fin de integrar las funciones del sistema anfitrión en los sistemas huéspedes, incluyendo carpetas compartidas y portapapeles, aceleración de vídeo y un modo de integración de ventanas fluido, se proporcionan complementos huéspedes (*guest additions*) para algunos sistemas operativos invitados.

## Contents

*   [1 Pasos para preparar Arch Linux como sistema anfitrión](#Pasos_para_preparar_Arch_Linux_como_sistema_anfitri.C3.B3n)
    *   [1.1 Instalar los paquetes principales](#Instalar_los_paquetes_principales)
    *   [1.2 Instalar los módulos del kernel de VirtualBox](#Instalar_los_m.C3.B3dulos_del_kernel_de_VirtualBox)
        *   [1.2.1 Sistema anfitrión corriendo sobre un kernel oficial](#Sistema_anfitri.C3.B3n_corriendo_sobre_un_kernel_oficial)
        *   [1.2.2 Sistema anfitrión corriendo sobre un kernel personalizado](#Sistema_anfitri.C3.B3n_corriendo_sobre_un_kernel_personalizado)
    *   [1.3 Cargar los módulos del kernel de VirtualBox](#Cargar_los_m.C3.B3dulos_del_kernel_de_VirtualBox)
    *   [1.4 Añadir nombres de usuario al grupo vboxusers](#A.C3.B1adir_nombres_de_usuario_al_grupo_vboxusers)
    *   [1.5 Discos con complementos para el sistema huésped (*guest additions*)](#Discos_con_complementos_para_el_sistema_hu.C3.A9sped_.28guest_additions.29)
    *   [1.6 Paquete de extensiones](#Paquete_de_extensiones)
    *   [1.7 Utilizar el front-end adecuado](#Utilizar_el_front-end_adecuado)
*   [2 Pasos para instalar Arch Linux como sistema huésped](#Pasos_para_instalar_Arch_Linux_como_sistema_hu.C3.A9sped)
    *   [2.1 Instalar Arch Linux dentro de la máquina virtual](#Instalar_Arch_Linux_dentro_de_la_m.C3.A1quina_virtual)
        *   [2.1.1 Instalación en modo EFI](#Instalaci.C3.B3n_en_modo_EFI)
    *   [2.2 Instalar complementos para el sistema huésped](#Instalar_complementos_para_el_sistema_hu.C3.A9sped)
    *   [2.3 Instalar los módulos del kernel de VirtualBox en el sistema huésped](#Instalar_los_m.C3.B3dulos_del_kernel_de_VirtualBox_en_el_sistema_hu.C3.A9sped)
        *   [2.3.1 Sistemas huéspedes que ejecutan un kernel oficial](#Sistemas_hu.C3.A9spedes_que_ejecutan_un_kernel_oficial)
        *   [2.3.2 Sistemas huéspedes que ejecutan un kernel personalizado](#Sistemas_hu.C3.A9spedes_que_ejecutan_un_kernel_personalizado)
    *   [2.4 Cargar los módulos del kernel de VirtualBox](#Cargar_los_m.C3.B3dulos_del_kernel_de_VirtualBox_2)
    *   [2.5 Lanzar los servicios de VirtualBox en el sistema huésped](#Lanzar_los_servicios_de_VirtualBox_en_el_sistema_hu.C3.A9sped)
    *   [2.6 Activar carpetas compartidas](#Activar_carpetas_compartidas)
        *   [2.6.1 Montaje manual](#Montaje_manual)
        *   [2.6.2 Montaje automático](#Montaje_autom.C3.A1tico)
        *   [2.6.3 Montaje durante el arranque](#Montaje_durante_el_arranque)
*   [3 Importar/exportar máquinas virtuales de VirtualBox a/desde otros hipervisores](#Importar.2Fexportar_m.C3.A1quinas_virtuales_de_VirtualBox_a.2Fdesde_otros_hipervisores)
    *   [3.1 Eliminar complementos](#Eliminar_complementos)
    *   [3.2 Utilizar el formato de disco virtual adecuado](#Utilizar_el_formato_de_disco_virtual_adecuado)
        *   [3.2.1 Herramientas de automatización](#Herramientas_de_automatizaci.C3.B3n)
        *   [3.2.2 Conversión manual](#Conversi.C3.B3n_manual)
    *   [3.3 Crear la configuración de la maquina virtual para su hipervisor](#Crear_la_configuraci.C3.B3n_de_la_maquina_virtual_para_su_hipervisor)
*   [4 Gestionar discos virtuales](#Gestionar_discos_virtuales)
    *   [4.1 Formatos soportados por VirtualBox](#Formatos_soportados_por_VirtualBox)
    *   [4.2 Conversión de formatos de imagen de disco](#Conversi.C3.B3n_de_formatos_de_imagen_de_disco)
        *   [4.2.1 VMDK a VDI y VDI a VMDK](#VMDK_a_VDI_y_VDI_a_VMDK)
        *   [4.2.2 VHD a VDI y VDI a VDH](#VHD_a_VDI_y_VDI_a_VDH)
        *   [4.2.3 QCOW2 a VDI y VDI a QCOW2](#QCOW2_a_VDI_y_VDI_a_QCOW2)
    *   [4.3 Montar discos virtuales](#Montar_discos_virtuales)
        *   [4.3.1 VDI](#VDI)
    *   [4.4 Discos virtuales compactos](#Discos_virtuales_compactos)
    *   [4.5 Aumentar discos virtuales](#Aumentar_discos_virtuales)
    *   [4.6 Reemplazar un disco virtual de forma manual desde el archivo .vbox](#Reemplazar_un_disco_virtual_de_forma_manual_desde_el_archivo_.vbox)
    *   [4.7 Clonar un disco virtual y asignarle un UUID nuevo](#Clonar_un_disco_virtual_y_asignarle_un_UUID_nuevo)
*   [5 Configuración avanzada](#Configuraci.C3.B3n_avanzada)
    *   [5.1 Gestionar el lanzamiento de la máquina virtual](#Gestionar_el_lanzamiento_de_la_m.C3.A1quina_virtual)
        *   [5.1.1 Iniciar máquinas virtuales con un servicio](#Iniciar_m.C3.A1quinas_virtuales_con_un_servicio)
        *   [5.1.2 Iniciar máquinas virtuales con un atajo del teclado](#Iniciar_m.C3.A1quinas_virtuales_con_un_atajo_del_teclado)
    *   [5.2 Utilizar dispositivos específicos en la máquina virtual](#Utilizar_dispositivos_espec.C3.ADficos_en_la_m.C3.A1quina_virtual)
        *   [5.2.1 Utilizar webcam / micrófono USB](#Utilizar_webcam_.2F_micr.C3.B3fono_USB)
        *   [5.2.2 Detectar cámaras web y otros dispositivos USB](#Detectar_c.C3.A1maras_web_y_otros_dispositivos_USB)
    *   [5.3 Acceder a un servidor huésped](#Acceder_a_un_servidor_hu.C3.A9sped)
    *   [5.4 Aceleración D3D en huéspedes Windows](#Aceleraci.C3.B3n_D3D_en_hu.C3.A9spedes_Windows)
    *   [5.5 VirtualBox en una llave USB](#VirtualBox_en_una_llave_USB)
    *   [5.6 Ejecutar una instalación nativa de Arch Linux dentro de VirtualBox](#Ejecutar_una_instalaci.C3.B3n_nativa_de_Arch_Linux_dentro_de_VirtualBox)
        *   [5.6.1 Asegurarse de que se tiene un esquema de nombres persistentes](#Asegurarse_de_que_se_tiene_un_esquema_de_nombres_persistentes)
        *   [5.6.2 Asegurarse de que su imagen mkinitcpio es correcta](#Asegurarse_de_que_su_imagen_mkinitcpio_es_correcta)
        *   [5.6.3 Crear una configuración de máquina virtual para arrancar desde la unidad física](#Crear_una_configuraci.C3.B3n_de_m.C3.A1quina_virtual_para_arrancar_desde_la_unidad_f.C3.ADsica)
            *   [5.6.3.1 Crear una imagen .vmdk de disco raw](#Crear_una_imagen_.vmdk_de_disco_raw)
            *   [5.6.3.2 Crear el archivo de configuración de la máquina virtual](#Crear_el_archivo_de_configuraci.C3.B3n_de_la_m.C3.A1quina_virtual)
        *   [5.6.4 Instalar Guest Additions](#Instalar_Guest_Additions)
    *   [5.7 Instalar un sistema nativo de Arch Linux desde VirtualBox](#Instalar_un_sistema_nativo_de_Arch_Linux_desde_VirtualBox)
    *   [5.8 Mover una instalación nativa de Windows a una máquina virtual](#Mover_una_instalaci.C3.B3n_nativa_de_Windows_a_una_m.C3.A1quina_virtual)
        *   [5.8.1 Tareas en Windows](#Tareas_en_Windows)
        *   [5.8.2 Tareas en GNU/Linux](#Tareas_en_GNU.2FLinux)
        *   [5.8.3 Arreglar el MBR y el gestor de arranque de Microsoft](#Arreglar_el_MBR_y_el_gestor_de_arranque_de_Microsoft)
        *   [5.8.4 Limitaciones conocidas](#Limitaciones_conocidas)
*   [6 Solución de problemas](#Soluci.C3.B3n_de_problemas)
    *   [6.1 Teclado y ratón bloqueados en la máquina virtual](#Teclado_y_rat.C3.B3n_bloqueados_en_la_m.C3.A1quina_virtual)
    *   [6.2 No se pueden usar las teclas CTRL+ALT+Fn en la máquina virtual](#No_se_pueden_usar_las_teclas_CTRL.2BALT.2BFn_en_la_m.C3.A1quina_virtual)
    *   [6.3 Arreglar problemas de imágenes ISO](#Arreglar_problemas_de_im.C3.A1genes_ISO)
    *   [6.4 La interfaz gráfica de VirtualBox no coincide con mi tema GTK](#La_interfaz_gr.C3.A1fica_de_VirtualBox_no_coincide_con_mi_tema_GTK)
    *   [6.5 OpenBSD inutilizable cuando las instrucciones de virtualización no están disponibles](#OpenBSD_inutilizable_cuando_las_instrucciones_de_virtualizaci.C3.B3n_no_est.C3.A1n_disponibles)
    *   [6.6 VBOX_E_INVALID_OBJECT_STATE (0x80BB0007)](#VBOX_E_INVALID_OBJECT_STATE_.280x80BB0007.29)
    *   [6.7 Subsistema USB no funciona en el sistema anfitrión o huésped](#Subsistema_USB_no_funciona_en_el_sistema_anfitri.C3.B3n_o_hu.C3.A9sped)
    *   [6.8 Error al crear la interfaz de red única del anfitrión](#Error_al_crear_la_interfaz_de_red_.C3.BAnica_del_anfitri.C3.B3n)
    *   [6.9 WinXP: Bit-depth no puede ser mayor que 16](#WinXP:_Bit-depth_no_puede_ser_mayor_que_16)
    *   [6.10 Utilizar puerto de serie en el sistema operativo huésped](#Utilizar_puerto_de_serie_en_el_sistema_operativo_hu.C3.A9sped)
    *   [6.11 Windows 8.x Error Code 0x000000C4](#Windows_8.x_Error_Code_0x000000C4)
    *   [6.12 Fallos de la máquina vitual de Windows 8 al arrancar con el error «ERR_DISK_FULL»](#Fallos_de_la_m.C3.A1quina_vitual_de_Windows_8_al_arrancar_con_el_error_.C2.ABERR_DISK_FULL.C2.BB)
    *   [6.13 El sistema huésped Linux tiene audio lento/distorsionado](#El_sistema_hu.C3.A9sped_Linux_tiene_audio_lento.2Fdistorsionado)
    *   [6.14 El huésped se congela después de iniciar Xorg](#El_hu.C3.A9sped_se_congela_despu.C3.A9s_de_iniciar_Xorg)
    *   [6.15 «NS_ERROR_FAILURE» y ausencia de elementos del menú](#.C2.ABNS_ERROR_FAILURE.C2.BB_y_ausencia_de_elementos_del_men.C3.BA)
    *   [6.16 Error en Windows huésped «The specified path does not exist. Check the path and then try again.»](#Error_en_Windows_hu.C3.A9sped_.C2.ABThe_specified_path_does_not_exist._Check_the_path_and_then_try_again..C2.BB)
*   [7 Véase también](#V.C3.A9ase_tambi.C3.A9n)

## Pasos para preparar Arch Linux como sistema anfitrión

Para poner en marcha máquinas virtuales de VirtualBox emarcadas en su sistema Arch Linux, siga estos pasos de instalación.

### Instalar los paquetes principales

El primer paso es instalar el paquete [virtualbox](https://www.archlinux.org/packages/?name=virtualbox) disponible en los [repositorios oficiales](/index.php/Official_repositories_(Espa%C3%B1ol) "Official repositories (Español)"), que contiene la suite de VirtualBox bajo licencia GPL con las herramientas de línea de órdenes SDL y headless incluidas. El paquete [virtualbox](https://www.archlinux.org/packages/?name=virtualbox) viene con [virtualbox-host-dkms](https://www.archlinux.org/packages/?name=virtualbox-host-dkms) como una dependencia necesaria.

Puede instalar la dependencia opcional [qt4](https://www.archlinux.org/packages/?name=qt4) con el fin de utilizar la interfaz gráfica del usuario basada en [Qt](/index.php/Qt "Qt"). Esto no es necesario si va a utilizar VirtualBox solamente desde la línea de órdenes. [Ver abajo para conocer las diferencias](#Utilizar_el_front-end_adecuado).

### Instalar los módulos del kernel de VirtualBox

A continuación, para virtualizar totalmente la instalación del sistema huésped, VirtualBox ofrece los siguientes [módulos del kernel](/index.php/Kernel_modules_(Espa%C3%B1ol) "Kernel modules (Español)"): `vboxdrv`, `vboxnetadp`, `vboxnetflt`, y `vboxpci`. Estos módulos deben ser añadidos al kernel del sistema anfitrión.

La compatibilidad binaria de los módulos del kernel depende de la API del kernel sobre al que va a ser compilado. El problema con el kernel de Linux es que estas interfaces podrían no ser las mismas entre una y otra versión del kernel. Con el fin de evitar problemas de compatibilidad y errores sutiles, cada vez que el kernel de Linux se actualiza, se aconseja volver a compilar los módulos del kernel respecto de la versión del kernel de Linux que acaba de ser instalada. Esto es lo que los empaquetadores de Arch Linux realmente hacen con los paquetes de los módulos del kernel de VirtualBox: cada vez que un nuevo kernel de Linux del Arch se libera, los módulos de Virtualbox se actualizan también.

Por lo tanto, hay que distinguir si se está usando un kernel de los [repositorios oficiales](/index.php/Official_repositories_(Espa%C3%B1ol) "Official repositories (Español)") o uno personalizado (autocompilado o instalado desde [AUR](/index.php/AUR_(Espa%C3%B1ol) "AUR (Español)")), ya que el paquete de los módulos del kernel a instalar puede variar de uno a otro.

#### Sistema anfitrión corriendo sobre un kernel oficial

*   Si está utilizando el kernel de [linux](https://www.archlinux.org/packages/?name=linux), asegúrese de que el paquete [virtualbox-host-dkms](https://www.archlinux.org/packages/?name=virtualbox-host-dkms) está instalado. Este último se ha debido instalar con el paquete [virtualbox](https://www.archlinux.org/packages/?name=virtualbox).
*   Si está utilizando la versión LTS del kernel ([linux-lts](https://www.archlinux.org/packages/?name=linux-lts)), es necesario instalar el paquete [virtualbox-host-dkms](https://www.archlinux.org/packages/?name=virtualbox-host-dkms). El paquete [virtualbox-host-dkms](https://www.archlinux.org/packages/?name=virtualbox-host-dkms) ya no será necesario y puede ser eliminado, si quiere.
*   Si está utilizando el kernel [linux-ck](https://aur.archlinux.org/packages/linux-ck/), construya el paquete [virtualbox-ck-host-modules](https://aur.archlinux.org/packages/virtualbox-ck-host-modules/).

#### Sistema anfitrión corriendo sobre un kernel personalizado

Si utiliza o pretende utilizar un kernel autocompilado desde las fuentes, tiene que saber que VirtualBox no requiere ningún módulo de virtualización (por ejemplo Virtuo, kvm, ...). Los módulos del kernel de VirtualBox proporcionan todo lo necesario para que VirtualBox funcione correctamente. De este modo se pueden desactivar los archivos *.config* de virtualización del kernel, siempre que no use otros hipervisores como Xen, KVM o QEMU.

El paquete `virtualbox-host-modules` funciona bien con kernels personalizados de la misma versión que el kernel de Arch Linux como [linux-ck](https://aur.archlinux.org/packages/linux-ck/). Dado que `virtualbox-host-modules` viene con el kernel oficial de Arch Linux ([linux](https://www.archlinux.org/packages/?name=linux)) como una dependencia, si no usa ese kernel, instale [virtualbox-host-dkms](https://www.archlinux.org/packages/?name=virtualbox-host-dkms) en su lugar.

Si utiliza un kernel personalizado que no es de la misma versión que el común de Arch Linux, tendrá que instalar el paquete [virtualbox-host-dkms](https://www.archlinux.org/packages/?name=virtualbox-host-dkms) igualmente. Este último viene con la fuente de los módulos del kernel de VirtualBox que se compila para generar estos módulos para el kernel.

En la medida en que el paquete [virtualbox-host-dkms](https://www.archlinux.org/packages/?name=virtualbox-host-dkms) necesita compilación, asegúrese de que tiene las cabeceras del kernel correspondientes a su versión del kernel personalizado para evitar que ocurra este error `Your kernel headers for kernel *your custom kernel version* cannot be found at /usr/lib/modules/*your custom kernel version*/build or /usr/lib/modules/*your custom kernel version*/source`

*   Si utiliza un kernel autocompilado y ha utilizado `make modules_install` para instalar los módulos, las carpetas `/usr/lib/modules/*your custom kernel version*/build` y `(...)/source` serán un enlace simbólico a las fuentes del kernel. Estos enlaces actuarán como las cabeceras del kernel que necesita. Si no ha eliminado estas fuentes del kernel, sin embargo, no tiene nada que hacer.
*   Si utiliza un kernel personalizado desde [AUR](/index.php/AUR "AUR"), asegúrese de que el paquete [linux-headers](https://www.archlinux.org/packages/?name=linux-headers) está instalado.

Una vez que [virtualbox-host-dkms](https://www.archlinux.org/packages/?name=virtualbox-host-dkms) está instalado, simplemente genere los módulos del kernel para su kernel personalizado mediante la ejecución de la siguiente orden que tiene la siguiente estructura:

```
# dkms install vboxhost/*virtualbox-host-source version* -k *your custom kernel version*/*your architecture*

```

**Sugerencia:** Utilice esta orden única en su lugar, si no necesita personalizar la orden anterior: `# dkms install vboxhost/$(pacman -Q virtualbox|awk '{print $2}'|sed 's/\-.\+//') -k $(uname -rm|sed 's/\ /\//')` 

Para volver a compilar automáticamente los módulos del kernel de VirtualBox cuando sus fuentes se actualicen (es decir, cuando el paquete [virtualbox-host-dkms](https://www.archlinux.org/packages/?name=virtualbox-host-dkms) se actualiza) y evitar tener que escribir de nuevo la orden anterior `dkms install` manualmente, active el servicio `dkms` con:

```
# systemctl enable dkms.service

```

Si este servicio no está activado mientras el paquete [virtualbox-host-dkms](https://www.archlinux.org/packages/?name=virtualbox-host-dkms) está siendo actualizado, no se actualizarán los módulos de VirtualBox y tendrá que escribir manualmente la orden `dkms install` como se ha descrito antes, para compilar la última versión de los módulos del kernel de VirtualBox. Si no desea escribir manualmente esta orden, si el servicio `dkms` se carga automáticamente al arranque, solo tiene que reiniciar el sistema para que sus módulos de VirtualBox se vuelvan a compilar en silencio.

Sin embargo, si desea mantener este demonio desactivado, puede utilizar un [hook de initramfs](/index.php/Mkinitcpio_(Espa%C3%B1ol) "Mkinitcpio (Español)") que activará automáticamente la orden `dkms install` antes descrita en el arranque. Para ello será necesario un reinicio para volver a compilar los módulos de VirtualBox. Para activar este hook, instale el [vboxhost-hook](https://aur.archlinux.org/packages/vboxhost-hook/) disponible en [AUR](/index.php/Arch_User_Repository_(Espa%C3%B1ol) "Arch User Repository (Español)") y añada `vboxhost` a la matriz HOOKS en `/etc/mkinitcpio.conf`. Una vez más, asegúrese de que las cabeceras de Linux correctas están disponibles para el nuevo kernel, de lo contrario la compilación fallará.

**Sugerencia:** Al igual que la orden `dkms`, el hook `vboxhost` le dirá si algo sale mal durante la reconstrucción de los módulos de VirtualBox.

### Cargar los módulos del kernel de VirtualBox

Entre los [módulos del kernel](/index.php/Kernel_modules_(Espa%C3%B1ol) "Kernel modules (Español)") que utiliza VirtualBox, hay uno necesario llamado `vboxdrv`, que se debe cargar antes de que las máquinas virtuales pueden ejecutarse. Se puede cargar automáticamente cuando Arch Linux se inicia, o se puede cargar manualmente cuando sea necesario.

Para cargar el módulo manualmente:

```
# modprobe vboxdrv

```

Para cargar el módulo de VirtualBox en el arranque, remítase a [Kernel modules (Español)#Cargar módulos](/index.php/Kernel_modules_(Espa%C3%B1ol)#Cargar_m.C3.B3dulos "Kernel modules (Español)") y cree un archivo `*.conf` (por ejemplo, `virtualbox.conf`) en `/etc/modules-load.d/` con la línea:

 `/etc/modules-load.d/virtualbox.conf`  `vboxdrv` 

Los siguientes módulos son opcionales, pero son recomendables si no quiere molestarse en realizar algunas configuraciones avanzadas (necesarias después): `vboxnetadp`, `vboxnetflt` y `vboxpci`.

*   `vboxnetadp` y `vboxnetflt` son necesarios cuando se va a utilizar la característica [«Host-only networking»](https://www.virtualbox.org/manual/ch06.html#network_hostonly). Más concretamente, `vboxnetadp` es necesario para crear la interfaz del sistema anfitrión en las preferencias globales de VirtualBox y `vboxnetflt` se necesita para poner en marcha una máquina virtual usando la interfaz de red.

*   `vboxpci` es necesario cuando su máquina virtual tiene que pasar a través de un dispositivo PCI en su sistema anfitrión.

**Nota:** Si los módulos del kernel de VirtualBox fueron cargados en el kernel durante la actualización de los módulos, necesita recargarlos manualmente para utilizar la nueva versión actualizada. Para hacerlo, ejecute como root `vboxreload`.

Por último, si se utiliza la característica «Host-only networking», asegúrese de que el paquete [net-tools](https://www.archlinux.org/packages/?name=net-tools) está instalado. VirtualBox utiliza realmente `ifconfig` y `route` para asignar la IP y la ruta a la interfaz del sitema anfitrión configurados con `VBoxManage hostonlyif` o mediante la interfaz grática del usuario en *Settings > Network > Host-only Networks > Edit host-only network (space) > Adapter*.

### Añadir nombres de usuario al grupo vboxusers

Para utilizar los puertos USB de la máquina anfitriona en sus máquinas virtuales, cree el [grupo](/index.php/Users_and_groups "Users and groups") `vboxusers`, cuyos usuarios estarán autorizados a utilizar esta función. El nuevo grupo no se aplica automáticamente a las sesiones existentes; el usuario tiene que salir y entrar de nuevo, o iniciar un nuevo entorno con la orden `newgrp` o con `sudo -u $USER -s`. Para agregar el usuario vigente al grupo `vboxusers`, escriba:

```
# gpasswd -a $USER vboxusers

```

### Discos con complementos para el sistema huésped (*guest additions*)

También se recomienda instalar el paquete [virtualbox-guest-iso](https://www.archlinux.org/packages/?name=virtualbox-guest-iso) en el sistema anfitrión donde se ejecuta VirtualBox. Este paquete actuará como una imagen de disco que se puede utilizar para instalar las aplicaciones huéspedes (guest additions) que no sean de Arch Linux en el sistema invitado. La imagen *.iso* se encuentra en `/usr/lib/virtualbox/additions/VBoxGuestAdditions.iso`.

### Paquete de extensiones

Desde VirtualBox 4.0, los componentes no-GPL se han separado del resto de la aplicación. A pesar de que «Oracle Extension Pack» ha sido liberado bajo una licencia no libre y **está disponible solo para uso personal**, podría estar interesado en instalar dicho paquete el cual proporciona [características adicionales](https://www.virtualbox.org/manual/ch01.html#intro-installing). Para evitar que tenga que manipularlo manualmente, el paquete [virtualbox-ext-oracle](https://aur.archlinux.org/packages/virtualbox-ext-oracle/) está disponible en [AUR](/index.php/AUR_(Espa%C3%B1ol) "AUR (Español)") y una versión precompilada se puede encontrar en el repositorio [seblu](/index.php/Unofficial_user_repositories#seblu "Unofficial user repositories").

Si prefiere utilizar la forma tradicional y manual: descargue las extensiones e instálelas manualmente a través de la interfaz gráfica de usuario (*Settings > Extensions*) o mediante `VBoxManage extpack install <.vbox-extpack>`, asegurándose de que tiene el conjunto de herramientas adecuadas (como [Polkit](/index.php/Polkit "Polkit"), gksu, etc.) para permitirle el acceso a VirtualBox con privilegios de root. La instalación de esta extensión [requiere acceder como root](https://www.virtualbox.org/ticket/8473).

### Utilizar el front-end adecuado

¡Enhorabuena! Ahora, está listo para utilizar VirtualBox.

Hay varios front-ends disponibles, de los cuales, dos por defecto:

*   Si desea utilizar VirtualBox únicamente desde la línea de órdenes (solo lanzarlo y cambiar la configuración de las máquinas virtuales existentes), puede utilizar la orden `VBoxSDL`. VBoxSDL solo proporciona una ventana simple que contiene únicamente la máquina virtual *pura*, sin menús ni controles.
*   Si desea utilizar VirtualBox desde la línea de órdenes sin ninguna interfaz gráfica de usuario ejecutándose (por ejemplo, en un servidor) para crear, lanzar y configurar máquinas virtuales, utilice `VBoxHeadless` que no produce ninguna salida visible en el equipo anfitrión, enviando solo los datos VRDP.

Si ha instalado el paquete [qt4](https://www.archlinux.org/packages/?name=qt4) como dependencia opcional, tendrá disponible una bonita interfaz gráfica de usuario con menús que le permitirán usar el ratón.

Por último, puede utilizar [PhpVirtualBox](/index.php/PhpVirtualBox "PhpVirtualBox") para administrar sus máquinas virtuales a través de una interfaz web.

Remítase al [manual de VirtualBox](https://www.virtualbox.org/manual) para aprender cómo crear máquinas virtuales.

**Advertencia:** Si va a guardar imágenes de discos virtuales en un sistema de archivos [Btrfs](/index.php/Btrfs "Btrfs"), antes de crear cualquier imagen, debería considerar desactivar [Copy-on-Write](/index.php/Btrfs#Copy-On-Write_.28CoW.29 "Btrfs") para el directorio de destino de estas imágenes.

## Pasos para instalar Arch Linux como sistema huésped

### Instalar Arch Linux dentro de la máquina virtual

**Nota:** En Windows como sistema anfitrión, puede que tenga que desactivar Hyper-V con el fin de utilizar las funciones de virtualización del hardware y poder crear máquinas virtuales de 64 bits en VirtualBox. Para aprender a desactivar/reactivar Hyper-V [vea este post de stackoverflow](http://superuser.com/questions/684966/switch-off-hyper-v-without-disable-functionality-in-windows-8-1).

Arranque el soporte de instalación de Arch a través de una de las unidades virtuales de la máquina virtual. A continuacion, complete la instalación de un sistema básico de Arch como se explica en la [Guía para principiantes](/index.php/Beginners%27_guide_(Espa%C3%B1ol) "Beginners' guide (Español)") o en la [Guía de instalación](/index.php/Installation_guide_(Espa%C3%B1ol) "Installation guide (Español)") sin instalar ningún controlador gráfico: vamos a instalar uno proporcionado por VirtualBox justo en el paso siguiente.

#### Instalación en modo EFI

Si desea instalar Arch Linux en modo EFI en VirtualBox, en la configuración de la máquina virtual, vaya a la pestaña *Settings*, y marque la casilla *Enable EFI (special OSes only)*. Después seleccione el kernel desde el menú del soporte de instalación de Arch Linux, el soporte demorará por un minuto o dos y continuará con el arranque del kernel normalmente después. Sea paciente.

Al arrancar en modo EFI, VirtualBox primero intentará ejecutar `/EFI/BOOT/BOOTX64.EFI` desde la ESP y después el script de la shell de EFI `startup.nsh` desde la raíz de la ESP si la primera opción falla. A menos que desee iniciar manualmente su gestor de arranque desde la shell EFI cada vez, tendrá que mover su gestor de arranque a la ruta predeterminada. No se moleste con el gestor de arranque de VirtualBox (accesible con `F2` en el arranque): añada entradas EFI al mismo manualmente al arrancar o con [efibootmgr](https://www.archlinux.org/packages/?name=efibootmgr), las cuales persistirán después de cada reinicio, [sin embargo, se pierden cuando la máquina virtual se apaga](https://www.virtualbox.org/ticket/11177).

### Instalar complementos para el sistema huésped

Después de completar la instalación del sistema huésped, instale los [Guest Additions](https://www.virtualbox.org/manual/ch04.html) de VirtualBox que incluyen controladores y aplicaciones que optimizan el sistema operativo invitado.

En los sistemas huéspedes que no son Arch, estos pueden ser instalados de dos formas:

*   Ya sea a través del proceso de instalación normal descrito en el manual de VirtualBox (en el sistema anfitrión, haga clic en «Install Guest Additions» en el menú VirtualBox, luego en el sistema huésped, monte el cdrom manualmente en `/mnt` y, después, ejecute `/mnt/VBoxLinuxAdditions.run`);
    **Nota:** Si ha probado este primer método, el segundo fallará con un [file conflict](/index.php/Pacman#I_get_an_error_when_updating:_.22file_exists_in_filesystem.22.21 "Pacman"): `/usr/bin/VBox*` y `/usr/lib/VBox* exists in filesystem`. Quite los archivos afectados (que son enlaces simbólicos a `/opt`), y repita la operación.

*   O bien, mediante un paquete que se puede instalar desde los repositorios oficiales de la distribución.

Cuando el sistema huésped es Arch Linux, el primer método no funciona y da como resultado el error `Unable to determine your Linux distribution`. Por lo tanto, utilice el segundo camino e instale [virtualbox-guest-utils](https://www.archlinux.org/packages/?name=virtualbox-guest-utils), que proporciona [virtualbox-guest-modules](https://www.archlinux.org/packages/?name=virtualbox-guest-modules) como una dependencia necesaria.

### Instalar los módulos del kernel de VirtualBox en el sistema huésped

#### Sistemas huéspedes que ejecutan un kernel oficial

*   Si está utilizando el kernel [linux](https://www.archlinux.org/packages/?name=linux), asegúrese de que el paquete [virtualbox-guest-modules](https://www.archlinux.org/packages/?name=virtualbox-guest-modules) ha sido instalado. Este último se ha debido ser instalado con el paquete [virtualbox-guest-utils](https://www.archlinux.org/packages/?name=virtualbox-guest-utils).
*   Si está utilizando la versión LTS del kernel ([linux-lts](https://www.archlinux.org/packages/?name=linux-lts)), es necesario instalar el paquete [virtualbox-guest-modules-lts](https://www.archlinux.org/packages/?name=virtualbox-guest-modules-lts). [virtualbox-guest-modules](https://www.archlinux.org/packages/?name=virtualbox-guest-modules) puede ser ahora eliminado.
*   Si está utilizando el kernel [linux-ck](https://aur.archlinux.org/packages/linux-ck/), compile el paquete [virtualbox-ck-guest-modules](https://aur.archlinux.org/packages/virtualbox-ck-guest-modules/). [virtualbox-guest-modules](https://www.archlinux.org/packages/?name=virtualbox-guest-modules) puede ser ahora eliminado en este caso también, si lo desea.

#### Sistemas huéspedes que ejecutan un kernel personalizado

Como este paso de la instalación es bastante similar a la sección de la instalación de los módulos del kernel de Vitualbox para el anfitrión que se ha descrito anteriormente, por favor consulte [esta sección](#Instalar_los_m.C3.B3dulos_del_kernel_de_VirtualBox) para más información y sustituya todos los paquetes [virtualbox-host-modules](https://www.archlinux.org/packages/?name=virtualbox-host-modules), [virtualbox-host-dkms](https://www.archlinux.org/packages/?name=virtualbox-host-dkms) y [vboxhost-hook](https://aur.archlinux.org/packages/vboxhost-hook/) para [virtualbox-guest-modules](https://www.archlinux.org/packages/?name=virtualbox-guest-modules), [virtualbox-guest-dkms](https://www.archlinux.org/packages/?name=virtualbox-guest-dkms) y [vboxguest-hook](https://aur.archlinux.org/packages/vboxguest-hook/) respectivamente.

### Cargar los módulos del kernel de VirtualBox

Para cargar los módulos manualmente, escriba:

```
# modprobe -a vboxguest vboxsf vboxvideo

```

Si al ejecutar modprobe se muestra `Module not found` (vea [[1]](http://unix.stackexchange.com/questions/131792/virtualbox-modprobe-cant-find-vboxguest-vboxsf-vboxvideo), [[2]](https://bbs.archlinux.org/viewtopic.php?id=181938) y [FS#40495](https://bugs.archlinux.org/task/40495)), ejecute la siguiente orden:

```
# depmod $(uname -r)

```

Para cargar el módulo de VirtualBox en el arranque, consulte [Kernel modules (Español)#Cargar módulos](/index.php/Kernel_modules_(Espa%C3%B1ol)#Cargar_m.C3.B3dulos "Kernel modules (Español)") y cree un archivo `*.conf` (por ejemplo, `virtualbox.conf`) en `/etc/modules-load.d/` con estas líneas:

 `/etc/modules-load.d/virtualbox.conf` 
```
vboxguest
vboxsf
vboxvideo
```

### Lanzar los servicios de VirtualBox en el sistema huésped

Después de instalar los módulos del kernel, ahora se necesita iniciar los servicios en el sistema huésped. Los servicios de los huéspedes son en realidad un ejecutable binario llamado `VBoxClient` que interactuará con el sistema de ventanas X (X11) y que gestionará las siguientes funciones:

*   portapapeles compartido y función arrastrar y soltar entre el anfitrión y el huésped;
*   modo de ventanas integradas;
*   la pantalla del huésped se redimensiona automáticamente en función del tamaño de la ventana huésped;
*   y, finalmente, la comprobación de la versión del anfitrión de VirtualBox.

Todas estas características se pueden activar, separada y manualmente, con sus estiquetas dedicadas.

```
# VBoxClient --clipboard --draganddrop --seamless --display --checkhostversion

```

Otras características que también son proporcionados por los servicios de sistemas huéspedes:

*   sincronización en tiempo real entre el anfitrión y el huésped;
*   carpetas compartidas con funciones de solo lectura y montaje automático entre el anfitrión y el huésped.

Pero VirtualBox ofrece una característica actualmente indocumentada, un script de Bash `VBoxClient-all` que activa todas estas características de forma automática y comprueba si un servidor X11 está realmente funcionando antes de activar algunas de ellas.

```
# VBoxClient-all

```

Para iniciar el script de forma automática cuando se inicia el sistema, ejecute la siguiente orden como root:

```
# systemctl enable vboxservice

```

Si no desea utilizar este servicio systemd, hay dos soluciones alternativas disponibles:

*   si se está usando un [Desktop environment (Español)](/index.php/Desktop_environment_(Espa%C3%B1ol) "Desktop environment (Español)"), solo necesita marcar una casilla o añadir la ruta del script `/usr/sbin/VBoxClient-all` en la sección autostart en la configuración del entorno de escritorio (en los entornos de escritorios esto se suele establecer en un archivo *.desktop* en `~/.config/autostart` —[vea la sección de inicio automático para más detalles](/index.php/Autostarting_(Espa%C3%B1ol)#Entradas_de_Desktop "Autostarting (Español)")—);
*   si no tiene ningún [entorno de escritorio](/index.php/Desktop_environment_(Espa%C3%B1ol) "Desktop environment (Español)"), agregue la línea siguiente en la parte superior de [~/.xinitrc](/index.php/Xinitrc "Xinitrc") por encima de cualquier opción `exec`:

 `~/.xinitrc`  `/usr/bin/VBoxClient-all` 

¡Enhorabuena! Ahora, debe tener un sistema Arch Linux huésped operativo.

Si quiere compartir carpetas entre el sistema anfitrión y su huésped Arch Linux, siga leyendo.

### Activar carpetas compartidas

Las carpetas compartidas se gestionan en el sistema anfitrión, en la configuración de la máquina virtual, accesible a través de la interfaz gráfica del usuario de VirtualBox, en la pestaña *Shared Folders*. Ahí se pueden especificar, la *Ruta de la carpeta*, el nombre del punto de montaje identificado por el *Nombre de la carpeta* , y opciones como *Solo lectura*, *Montaje automático* y *Hacer permanente*. Estos parámetros se pueden definir con la utilidad de línea de órdenes `VBoxManage`. Vea [esto](https://www.virtualbox.org/manual/ch04.html#sharedfolders) para más detalles.

Independientemente del método que utilice para montar su carpeta, todos los métodos requieren algunos pasos previos.

Para evitar este problema `/sbin/mount.vboxsf: mounting failed with the error: No such device`, asegúrese de que el módulo del kernel `vboxsf` se ha cargado adecuadamente. Esto ya ha debido ser así, ya que se activaron todos los módulos del kernel del sistema huésped previamente.

Se necesitan dos pasos adicionales para que el punto de montaje sea accesible a los usuarios sin privilegios de root:

*   el paquete [virtualbox-guest-utils](https://www.archlinux.org/packages/?name=virtualbox-guest-utils) habrá creado un grupo `vboxsf` (hecho en un paso anterior);
*   su nombre de usuario debe estar en este grupo. Utilice esta orden `gpasswd -a $USER vboxsf` para añadir su nombre de usuario y esta otra `newgrp` para aplicar los cambios inmediatamente;

#### Montaje manual

Utilice la siguiente orden para montar su carpeta en el sistema huésped Arch Linux:

```
# mount -t vboxsf *shared_folder_name* *mount_point_on_guest_system*

```

El sistema de archivos vboxsf ofrece otras opciones que se pueden visualizar con esta orden:

```
# mount.vboxsf

```

Por ejemplo, si el usuario no estaba en el grupo *vboxsf*, podríamos utilizar esta orden para darle acceso a nuestro punto de montaje:

```
# mount -t vboxsf -o uid=1000,gid=1000 home /mnt/

```

Donde *uid* y *gid* son los valores correspondientes a los usuarios que queremos dar acceso. Estos valores se obtienen de la orden `id` ejecutada respecto a dichos usuarios.

#### Montaje automático

Para que la función de montaje automático funcione, se deben cumplir las siguientes condiciones:

*   vboxservice debe estar cargado en el sistema huésped (hecho en un paso anterior);
*   debe haber marcado la casilla de montaje automático en la interfaz gráica o usado la opción `--automount` en la orden `VBoxManage sharedfolder`.

La carpeta compartida debe aparecer ahora en `/media/sf_*shared_folder_name*`.

Puede usar enlaces simbólicos si quiere tener un acceso más cómodo a dicha carpeta y ahorrarse tener que navegar hasta ese directorio, por ejemplo:

```
$ ln -s /media/sf_*shared_folder_name* ~/*my_documents*

```

#### Montaje durante el arranque

Puede montar su directorio con [fstab (Español)](/index.php/Fstab_(Espa%C3%B1ol) "Fstab (Español)"). Sin embargo, para evitar problemas de inicio con systemd, debe añadir `comment=systemd.automount` a `/etc/fstab`. De esta manera, las carpetas compartidas serán montadas bajo demanda, solo cuando se acceda a los puntos de montaje y no durante el inicio. Esto puede evitar algunos problemas, especialmente si las aplicaciones del sistema huésped no están aún cargadas mientras systemd lee fstab y monta las particiones.

```
desktop   /media/desktop    vboxsf  uid=user,gid=group,rw,dmode=700,fmode=600,comment=systemd.automount 0 0

```

A partir de 2012-08-02, mount.vboxsf no admite la opción *nofail*:

```
desktop   /media/desktop    vboxsf  uid=user,gid=group,rw,dmode=700,fmode=600,nofail 0 0

```

## Importar/exportar máquinas virtuales de VirtualBox a/desde otros hipervisores

Si planea utilizar su máquina virtual en otro hipervisor o quiere importar en VirtualBox una máquina virtual creada con otro hipervisor, quizás podría estar interesado en la lectura de los siguientes pasos.

### Eliminar complementos

Los complementos para el sistema huésped están disponibles en la mayoría de las soluciones de los hipervisores: VirtualBox cuenta con Guest Additions, VMware con VMware Tools, Parallels con Parallels Tools, etc. Estos componentes adicionales están diseñados para ser instalados en una máquina virtual después de que el sistema operativo huésped haya sido instalado. Se componen de controladores de dispositivos y aplicaciones del sistema que optimizan el sistema operativo invitado para un mejor rendimiento y usabilidad [proporcionando estas características](https://www.virtualbox.org/manual/ch04.html).

Si ha instalado los complementos en su máquina virtual, desinstalelos primero. Su huésped, especialmente si está usando un sistema operativo de la familia Windows, podría comportarse extrañamente, romperse o, incluso, puede que no arranque en absoluto si todavía se están utilizando los controladores específicos de otro hipervisor.

### Utilizar el formato de disco virtual adecuado

Este paso dependerá de la capacidad de convertir la imagen de disco virtual directamente o no.

#### Herramientas de automatización

Algunos proveedores ofrecen herramientas que dan la posibilidad de crear máquinas virtuales desde un sistema operativo Windows o GNU/Linux ya se encuentre en una máquina virtual o, incluso, en una instalación nativa. Con este tipo de producto, no es necesario aplicar este y los siguientes pasos y puede dejar de leer aquí.

*   *[Parallels Transporter](http://www.parallels.com/products/transporter)* no es gratis, es un producto de Parallels Inc. Esta solución consiste, básicamente, en una pieza de software llamada *agent* que será instalado en el sistema huésped que desee importar/convertir. A continuación, Parallels Transporter, <u>que solo funciona en OS X</u>, creará una máquina virtual conectada a través de *agent* bien por USB o por conexión de red cableada.
*   *[VMware vCenter Converter](https://www.vmware.com/products/converter/)* es gratuita, previa inscripción en el sitio web de VMware, funciona casi de la misma manera que Parallels Transporter, con la particularidad de que la pieza de software que hará recopilar los datos para crear la máquina virtual solo funciona en una plataforma Windows.

#### Conversión manual

En primer lugar, familiarícese con [los formatos soportados por VirtualBox](#Formatos_soportados_por_VirtualBox) y [los formatos soportados por otros hipervisores](https://en.wikipedia.org/wiki/Comparison_of_platform_virtual_machines#Image_type_compatibility "wikipedia:Comparison of platform virtual machines").

*   La importación o exportación de una máquina virtual a/desde VMware no es un problema en absoluto si utiliza el formato de disco VMDK o OVF, convirtiendo [#VMDK a VDI y VDI a VMDK](#VMDK_a_VDI_y_VDI_a_VMDK) si es posible y tiene disponible la mencionada herramienta VMware vCenter de conversión.

*   La importación o exportación de una máquina virtual a/desde QEMU no es ningún problema: algunos formatos de QEMU tienen soporte directamente en VirtualBox y la conversión entre [#QCOW2 a VDI y VDI a QCOW2](#QCOW2_a_VDI_y_VDI_a_QCOW2) la tenemos disponible si es necesario.

*   La importación o exportación de una máquina virtual a/desde Parallels es el camino más difícil: solo soporta su propio formato HDD (incluso el formato estándar y portable OVF no está soportado).

*   Para exportar la máquina virtual Parallels, tendrá que utilizar la herramienta de Parallels Transporter descrita anteriormente.
*   Para importar a VirtualBox, tendrá que usar VMware vCenter Converter descrito anteriormente para convertir la máquina virtual al formato VMware primero. Luego, tendrá que aplicar la solución para migrar desde VMware.

### Crear la configuración de la maquina virtual para su hipervisor

Cada hipervisor tiene su propio archivo de configuración de máquina virtual: `.vbox` para VirtualBox, `.vmx` para VMware, un archivo `config.pvs` ubicado en el paquete de la máquina virtual (archivo `.pvm`), etc. De este modo, tendrá que recrear una nueva máquina virtual en su nuevo hipervisor de destino y especificar su configuración de hardware tan precisa como sea posible, de modo similar a como se hizo en su máquina virtual inicial.

Preste especial atención a la interfaz del firmware (BIOS o UEFI) utilizado para instalar el sistema operativo huésped. Mientras que existe una opción disponible para elegir entre estas 2 interfaces en VirtualBox y Parallels, en VMware, en cambio, tendrá que añadir manualmente la siguiente línea a su archivo *.vmx*.

 `ArchLinux_vm.vmx`  `firmware = "efi"` 

Por último, indique a su hipervisor el disco virtual a utilizar que ha convertido y lance la máquina virtual.

**Sugerencia:**

*   En VirtualBox, si no desea navegar por la interfaz gráfica de usuario para encontrar la ubicación adecuada para agregar el nuevo dispositivo de disco virtual, puede [#Reemplazar un disco virtual de forma manual desde el archivo .vbox](#Reemplazar_un_disco_virtual_de_forma_manual_desde_el_archivo_.vbox), o utilizar `VBoxManage storageattach` descrito en [#Aumentar discos virtuales](#Aumentar_discos_virtuales) o en la [página del manual de VirtualBox](https://www.virtualbox.org/manual/ch08.html#vboxmanage-storageattach).
*   Del mismo modo, en los productos de VMware, puede reemplazar el lugar de la ubicación actual del disco virtual adaptando la ubicación del archivo *.vmdk* en su archivo de configuración *.vmx*

## Gestionar discos virtuales

### Formatos soportados por VirtualBox

VirtualBox es compatible con los siguientes formatos de disco virtual:

*   VDI: La Virtual Disk Image es el propio contenedor abierto de VirtualBox utilizado por defecto al crear una máquina virtual con VirtualBox.

*   VMDK: El Virtual Machine Disk fue desarrollado inicialmente por VMware para sus productos. La especificación fue inicialmente de código cerrado, pero ahora se ha convertido en un formato abierto que está totalmente respaldado por VirtualBox. Este formato ofrece la posibilidad de dividirse en varios archivos de 2 GB. Esta característica es especialmente útil si desea almacenar la máquina virtual en máquinas que no soportan archivos muy grandes. Otros formatos, excluyendo el formato HDD de Parallels, no proporcionan una característica equivalente.

*   VHD: El Virtual Hard Disk es el formato utilizado por Microsoft en Windows Virtual PC y Hyper-V. Si tiene intención de utilizar cualquiera de estos productos de Microsoft, tendrá que elegir este formato.

**Sugerencia:** Desde Windows 7, este formato se puede montar directamente sin ninguna aplicación adicional.

*   VHDX (solo lectura): Esta es la versión extendida del formato de Virtual Hard Disk desarrollada por Microsoft, que ha sido liberado el 2012-09-04 con Hyper-V 3.0 que viene con Windows Server 2012\. Esta nueva versión del formato de disco no ofrece un rendimiento mejorado (mejora, eso sí, la alineación de bloques), permite mayor tamaño de los bloques, y da soporte a journal que aporta resiliencia a los fallos de energía. VirtualBox [soporta este formato en solo lectura](https://www.virtualbox.org/manual/ch15.html#idp63002176).

*   La versión 2 de HDD: El formato HDD es desarrollado por Parallels Inc y utilizado en sus soluciones de hipervisor como Parallels Desktop para Mac. Las nuevas versiones de este formato (es decir, 3 y 4) no son compatibles debido a la falta de documentación de este formato propietario.
    **Nota:** En la actualidad existe una controversia con respecto al soporte de la versión 2 del formato. Si bien el manual oficial de VirtualBox [informa que solo la segunda versión del formato de archivo HDD está soportado](https://www.virtualbox.org/manual/ch05.html#vdidetails), los colaboradores de Wikipedia [informan que la primera versión puede funcionar también](https://en.wikipedia.org/wiki/Comparison_of_platform_virtual_machines#Image_type_compatibility "wikipedia:Comparison of platform virtual machines"). Si es posible realizar algunas pruebas con la primera versión del formato HDD, la ayuda será bienvenida.

*   QED: El formato Enhanced Disk de QUEMU es un formato de archivo antiguo de QEMU, otro hipervisor de código libre y abierto. Este formato fue diseñado a partir de 2010 como una forma de ofrecer una alternativa superior a qcow2 y otros. Este formato cuenta con una trayectoria de E/S totalmente asíncrona, integridad de datos solida, respaldo de archivos y archivos dispersos. El formato QED solo se admite para la compatibilidad con máquinas virtuales creadas con versiones antiguas de QEMU.

*   QCOW: El formato QEMU Copy On Write es el formato actual de QEMU. El formato qcow soporta compresión transparente basada en zlib y cifrado (este último tiene defectos y no es recomendable). Qcow está disponible en dos versiones: QCOW y QCOW2\. El último tiende a reemplazar al primero. QCOW es [en la actualidad plenamente soportado por VirtualBox](https://www.virtualbox.org/manual/ch15.html#idp63002176). QCOW2 viene en dos revisiones: QCOW2 0.10 y QCOW2 1.1 (que es el valor por defecto cuando se crea un disco virtual con QEMU). VirtualBox no soporta este formato qcow2 (ambas revisiones se han probado).

*   OVF: El Open Virtualization Format es un formato abierto que ha sido diseñado para la interoperabilidad y la distribución de las máquinas virtuales entre diferentes hipervisores. VirtualBox es compatible con todas las revisiones de este formato a través de la [característica importar/exportar de `VBoxManage`](https://www.virtualbox.org/manual/ch08.html#idp55423424) pero con [limitaciones conocidas](https://www.virtualbox.org/manual/ch14.html#KnownProblems).

*   RAW: Este es el modo cuando el disco virtual se expone directamente al disco sin ser contenida en un contenedor específico de formato de archivo. VirtualBox soporta esta característica de varias maneras: la conversión de disco RAW [a un formato específico](https://www.virtualbox.org/manual/ch08.html#idp59139136), o por [clonación de un disco a RAW](https://www.virtualbox.org/manual/ch08.html#vboxmanage-clonevdi), o utilizando directamente un archivo VMDK [que apunte a un disco físico o a un simple archivo](https://www.virtualbox.org/manual/ch09.html#idp57804112).

### Conversión de formatos de imagen de disco

#### VMDK a VDI y VDI a VMDK

VirtualBox puede manejar la conversión de VDI a VMDK (y viceversa) por sí mismo con [`VBoxManage clonehd`](https://www.virtualbox.org/manual/ch08.html#vboxmanage-clonevdi).

VMDK a VDI:

```
$ VBoxManage clonehd *source.vmdk* *destination.vdi* --format VDI

```

VDI a VMDK:

```
$ VBoxManage clonehd *source.vdi* *destination.vmdk* --format VMDK

```

#### VHD a VDI y VDI a VDH

VirtualBox puede manejar la conversión de VHD a VDI (y viceversa) con [`VBoxManage clonehd`](https://www.virtualbox.org/manual/ch08.html#vboxmanage-clonevdi) también.

VHD a VDI:

```
$ VBoxManage clonehd *source.vhd* *destination.vdi* --format VDI

```

VDI a VHD:

```
$ VBoxManage clonehd *source.vdi* *destination.vhd* --format VHD

```

#### QCOW2 a VDI y VDI a QCOW2

[`VBoxManage clonehd`](https://www.virtualbox.org/manual/ch08.html#vboxmanage-clonevdi) no puede manejar la conversión del formato de QEMU; por lo tanto, vamos a confiar en otra herramienta. La orden `qemu-img` de [qemu](https://www.archlinux.org/packages/?name=qemu) se puede utilizar para convertir imágenes de VDI a QCOW2 (y viceversa).
**Nota:** `qemu-img` puede manejar otros formatos también. De acuerdo con `qemu-img --help`, estos son los formatos soportados que admite: «*vvfat vpc vmdk vhdx vdi ssh sheepdog sheepdog sheepdog raw host_cdrom host_floppy host_device file qed qcow2 qcow parallels nbd nbd nbd iscsi dmg tftp ftps ftp https http cow cloop bochs blkverify blkdebug'».*

QCOW2 a VDI:

```
$ qemu-img convert -pO vdi *source.qcow2* *destination.vdi*

```

VDI a QCOW2:

```
$ qemu-img convert -pO qcow2 *source.vdi* *destination.qcow2*

```

Como qcow2 viene en dos revisiones (vea [#Formatos soportados por VirtualBox](#Formatos_soportados_por_VirtualBox), utilice la etiqueta `-o compat=` para especificar la revisión.

```
$ qemu-img convert -pO qcow2 *source.vdi* *destination.qcow2* -o compat=0.10

```

o

```
$ qemu-img convert -pO qcow2 *source.vdi* *destination.qcow2* -o compat=1.1

```

**Sugerencia:** El parámetro `-p` se usa para mostrar el progreso de la tarea de conversión.

### Montar discos virtuales

#### VDI

El montaje de imágenes vdi solo funciona con imágenes de tamaño fijo (también conocidas como imágenes estáticas); las imágenes dinámicas (asignación dinámica de tamaño) no son fáciles de montar.

El desplazamiento de la partición (en el VDI) es necesario, luego hay que agregar el valor `offData` a `32256` (por ejemplo, 69632 + 32256 = 101888):

```
$ VBoxManage internalcommands dumphdinfo <storage.vdi> | grep "offData"

```

Ahora se puede montar con:

```
# mount -t ext4 -o rw,noatime,noexec,loop,offset=101888 <storage.vdi> /mntpoint/

```

También puede utilizar el script [mount.vdi](https://github.com/pld-linux/VirtualBox/blob/master/mount.vdi) script that, which you can use as (install script itself to `/usr/bin/`):

```
# mount -t vdi -o fstype=ext4,rw,noatime,noexec *vdi_file_location* */mnt/*

```

Alternativamente, puede usar el módulo del kernel [qemu](https://www.archlinux.org/packages/?name=qemu) que puede hacer este [attrib](http://bethesignal.org/blog/2011/01/05/how-to-mount-virtualbox-vdi-image/):

```
# modprobe nbd max_part=16
# qemu-nbd -c /dev/nbd0 <storage.vdi>
# mount /dev/nbd0p1 /mnt/dir/
# # to unmount:
# umount /mnt/dir/
# qemu-nbd -d /dev/nbd0

```

Si los nodos de partición no se desplazan, pruebe usando `partprobe /dev/nbd0`; en otro caso, una partición vdi se puede asignar directamente a un nodo con: `qemu-nbd -P 1 -c /dev/nbd0 <storage.vdi>`.

### Discos virtuales compactos

La compactación de discos virtuales solo funciona con archivos `.vdi` y, básicamente, consiste en los siguientes pasos.

Arranque su máquina virtual y quite todo el espacio sobrante manualmente o mediante el uso de una herramienta de limpieza como [bleachbit](https://www.archlinux.org/packages/?name=bleachbit) disponible [para sistemas windows también](http://bleachbit.sourceforge.net/download/windows).

Limpie el espacio libre con ceros que puede lograrse con varias herramientas:

*   Si se estaba utilizando BleachBit, puede seguir usando esta utilidad para esta función, marcando la casilla *System > Free disk space* de la interfaz, o, en otro caso, utilizando `bleachbit -c system.free_disk_space` en la línea de intérprete de órdenes (CLI);
*   En los sistemas basados en UNIX, usando `dd` o, preferiblemente [dcfldd](https://www.archlinux.org/packages/?name=dcfldd) (vea [esto](http://superuser.com/a/355322) para conocer las diferencias):

	 `# dcfldd if=/dev/zero of=*/fillfile* bs=4M` 

	Cuando `fillfile` haya alcanzado el límite de la partición, se recibirá un mensaje como `1280 blocks (5120Mb) written.dcfldd:: No space left on device`. Esto significa que todos los bloques del espacio de usuario y no reservados de la partición se llenarán con ceros. Utilice esta orden como root ya que es importante asegurarse de que todos los bloques libres han sido sobrescritos. De hecho, por defecto, al utilizar particiones con sistema de archivos ext, un porcentaje específico de bloques del sistema de archivos está reservada para el superusuario (vea el argumento `-m` en la página del manual de `mkfs.ext4` o utilice `tune2fs -l` para ver cuánto espacio está reservado para aplicaciones de root).

	Cuando el proceso antes mencionado se ha completado, puede eliminar el archivo `*fillfile*` creado.

*   En Windows, hay dos herramientas disponibles:

*   `sdelete` de la [suite Sysinternals](http://technet.microsoft.com/en-us/sysinternals/bb842062.aspx), escriba `sdelete -s *c:*`, necesitará repetir la orden para cada unidad que tenga en su máquina virtual;
*   o, si se prefiere los scripts, hay una [solución PowerShell](http://blog.whatsupduck.net/2012/03/powershell-alternative-to-sdelete.html), pero que aún así necesita ser repetido para todas las unidades.

	 `PS> ./Write-ZeroesToFreeSpace.ps1 -Root *c:\* -PercentFree 0` 

**Nota:** Este script se debe ejecutar en un entorno de PowerShell con privilegios de administrador. De forma predeterminada, los scripts no se pueden ejecutar, por lo que tendrá que asegurarse que la política de ejecución esté, al menos, en `RemoteSigned` y no en `Restricted`. Esto se puede comprobar con `Get-ExecutionPolicy` y la política requerida se puede establecer con `Set-ExecutionPolicy RemoteSigned`.

Una vez que el espacio libre en el disco ha sido anulado, apague su máquina virtual.

La próxima vez que arranque su máquina virtual, es recomendable hacer una verificación del sistema de archivos.

*   En los sistemas basados en UNIX, puede usar `fsck` manualmente;

*   En los sistemas GNU / Linux, y por lo tanto en Arch Linux, puede forzar una comprobación de disco en el arranque [gracias a un parámetro de arranque del kernel](/index.php/Fsck#Forcing_the_check "Fsck");

*   En los sistemas Windows, puede utilizar:

*   o bien, `chkdsk *c:* /F` donde `*c:*` necesita ser reemplazado por cada disco que necesita ser analizado y corregir errores;
*   o, `FsckDskAll` [desde aquí](http://therightstuff.de/2009/02/14/ChkDskAll-ChkDsk-For-All-Drives.aspx), que es básicamente el mismo software que `chkdsk`, pero sin la necesidad de repetir la orden para todas las unidades;

Ahora, hay que quitar los ceros del archivo `vdi` con `[VBoxManage modifyhd](https://www.virtualbox.org/manual/ch08.html#vboxmanage-modifyvdi)`:

```
$ VBoxManage modifyhd *your_disk.vdi* --compact

```

**Nota:** Si su máquina virtual dispone de instantáneas, es necesario aplicar la orden anterior en cada archivo `.vdi` que tenga.

### Aumentar discos virtuales

Si se está quedando sin espacio, debido al pequeño tamaño del disco duro que ha seleccionado al crear la máquina virtual, la solución aconsejada por el manual de VirtualBox es utilizar [`VBoxManage modifyhd`](https://www.virtualbox.org/manual/ch08.html#vboxmanage-modifyvdi). Sin embargo, esta orden solo funciona para los discos VDI y VHD, y solo para las variantes asignadas dinámicamente. Si desea cambiar el tamaño de un disco virtual que también es un disco de tamaño fijo, siga este arreglo que funciona bien para una máquina virtual Windows o UNIX.

En primer lugar, crear un nuevo disco virtual junto al que quiere aumentar:

```
$ VBoxManage createhd -filename
$ VBoxManage createhd -filename *new.vdi* --size *10000*

```

donde el tamaño es en MiB, en este ejemplo 10000MiB ~= 10GiB, y *new.vdi* es el nombre del nuevo disco duro que se creará.

A continuación, el viejo disco virtual necesita ser clonado para el nuevo, lo cual puede tomar algún tiempo:

```
$ VBoxManage clonehd *old.vdi* *new.vdi* --existing

```

**Nota:** Por defecto, esta orden utiliza el *estándard* de la variante de formato de archivo (correspondiente a la asignación dinámica) y, por lo tanto, no va a utilizar la misma variante de formato de archivo que la del disco virtual de origen. Si su archivo *old.vdi* tiene un tamaño fijo y desea mantener esta variante, agregue el parámetro `--variant Fixed`.

Separe el viejo disco duro y adjunte uno nuevo, sustituyendo todos los argumentos en cursiva obligatoriamente, según sus características:

```
$ VBoxManage storageattach *VM_name* --storagectl *SATA* --port *0* --medium none
$ VBoxManage storageattach *VM_name* --storagectl *SATA* --port *0* --medium *new.vdi* --type hdd

```

Para obtener el nombre del controlador del almacenamiento y el número del puerto, puede utilizar la orden `VBoxManage showvminfo *VM_name*`. De la salida obtendrá tal resultado (lo que busca está en cursiva):

```
[...]
Storage Controller Name (0):            IDE
Storage Controller Type (0):            PIIX4
Storage Controller Instance Number (0): 0
Storage Controller Max Port Count (0):  2
Storage Controller Port Count (0):      2
Storage Controller Bootable (0):        on
Storage Controller Name (1):            SATA
Storage Controller Type (1):            IntelAhci
Storage Controller Instance Number (1): 0
Storage Controller Max Port Count (1):  30
Storage Controller Port Count (1):      1
Storage Controller Bootable (1):        on
IDE (1, 0): Empty
*SATA* (*0*, 0): /home/wget/IT/Virtual_machines/GNU_Linux_distributions/ArchLinux_x64_EFI/Snapshots/{6bb17af7-e8a2-4bbf-baac-fbba05ebd704}.vdi (UUID: 6bb17af7-e8a2-4bbf-baac-fbba05ebd704)
[...]
```

Descargue la [imagen de GParted live](http://gparted.org/download.php) y móntela como un archivo de disco CD/DVD virtual, arranque su máquina virtual, aumente/mueva las particiones, desmonte GParted live y reinicie el sistema.

**Nota:** En discos GPT, al aumentar el tamaño del disco dará como resultado una copia de respaldo en la cabecera de GPT, pero dicho respaldo no se verá reflejado al final del dispositivo. GParted le preguntará si desea solucionar este problema, haga clic en *Fix* en ambas ocasiones. En los discos MBR, no se tiene un problema como este, ya que esta tabla de particiones no cuenta con respaldo al final del disco.

Por último, anule el registro del disco virtual de VirtualBox y elimine el archivo:

```
$ VBoxManage closemedium disk *old.vdi*
$ rm *old.vdi*

```

### Reemplazar un disco virtual de forma manual desde el archivo .vbox

Si piensa que la edición de un simple archivo *XML* es más eficaz que jugar con la interfaz gráfica del usuario o con `VBoxManage` y desea reemplazar (o añadir) un disco virtual a la máquina virtual, basta con reemplazar la GUID en el archivo de configuración *.vbox* correspondiente a su máquina virtual, con el archivo de ubicación y el formato que necesite:

 `ArchLinux_vm.vbox`  `<HardDisk uuid="*{670157e5-8bd4-4f7b-8b96-9ee412a712b5}*" location="*ArchLinux_vm.vdi*" format="*VDI*" type="Normal"/>` 

a continuación, en la subetiqueta `<AttachedDevice>` de `<StorageController>`, sustituya la GUID por la nueva.

 `ArchLinux_vm.vbox` 
```
<AttachedDevice type="HardDisk" port="0" device="0">
  <Image uuid="*{670157e5-8bd4-4f7b-8b96-9ee412a712b5}*"/>
</AttachedDevice>
```

**Nota:** Si no sabe el GUID de la unidad que desea agregar, puede utilizar el archivo `VBoxManage showhdinfo *file*`. Si ha utilizado previamente `VBoxManage clonehd` para copiar/convertir su disco virtual, esta orden debería haber emitido el GUID justo después de la copia/conversión completada. El uso de un GUID aleatorio no funciona, ya que cada [UUID se almacena en el interior de cada imagen de disco](http://www.virtualbox.org/manual/ch05.html#cloningvdis).

### Clonar un disco virtual y asignarle un UUID nuevo

Los UUID son ampliamente utilizados por VirtualBox. Cada máquina virtual y cada disco virtual de una máquina virtual deben tener un UUID diferente. Cuando se lanza una máquina virtual en VirtualBox, este último hace un seguimiento de todos los UUID de la instancia de la máquina virtual. Consulte la [`VBoxManage list`](http://www.virtualbox.org/manual/ch08.html#vboxmanage-list) para listar los elementos registrados por VirtualBox.

Si ha clonado un disco virtual de forma manual copiando el archivo del disco virtual, tendrá que asignar un nuevo UUID a la unidad virtual clonada, si quiere utilizar el disco en la misma máquina virtual o, incluso, en otra (si esta ya ha sido abierta y, por lo tanto, registrada, con VirtualBox).

Puede utilizar esta orden para asignar un nuevo UUID a su disco virtual:

```
$ VBoxManage internalcommands sethduuid */path/to/disk.vdi*

```

**Sugerencia:** En el futuro, para evitar la copia del disco virtual y la asignación de un nuevo UUID a su archivo de forma manual, use `[VBoxManage clonehd](http://www.virtualbox.org/manual/ch08.html#vboxmanage-clonevdi)` en su lugar.

**Nota:** Las órdenes anteriores soportan [todos los formatos de disco virtual admitidos por VirtualBox](#Formatos_soportados_por_VirtualBox).

## Configuración avanzada

### Gestionar el lanzamiento de la máquina virtual

#### Iniciar máquinas virtuales con un servicio

He aquí los detalles de la implementación de un servicio de systemd que se utilizará para considerar una máquina virtual como un servicio.

 `/etc/systemd/system/vboxvmservice@.service` 
```
[Unit]
Description=VBox Virtual Machine %i Service
Requires=systemd-modules-load.service
After=systemd-modules-load.service

[Service]
User=*username*
Group=vboxusers
ExecStart=/usr/bin/VBoxHeadless -s %i
ExecStop=/usr/bin/VBoxManage controlvm %i savestate

[Install]
WantedBy=multi-user.target
```

**Nota:**

*   Reemplace `*username*` con un usuario que sea miembro del grupo `vboxusers`. Asegúrese de que el usuario elegido es el mismo usuario que creará/importará las máquinas virtuales, de lo contrario el usuario no verá las aplicaciones de la máquina virtual.
*   Si tiene varias máquinas virtuales gestionadas por systemd y las mismas no se detienen correctamente, pruebe añadiendo `RemainAfterExit=true` y `KillMode=none` al final de la sección `[Service]`.

Para activar el servicio que pondrá en marcha la máquina virtual en el siguiente inicio, utilice:

```
# systemctl enable vboxvmservice@*your_virtual_machine_name*

```

Para iniciar el servicio que lance directamente la máquina virtual, utilice:

```
# systemctl start vboxvmservice@*your_virtual_machine_name*

```

VirtualBox 4.2 introduce [una nueva forma](http://lifeofageekadmin.com/how-to-set-your-virtualbox-vm-to-automatically-startup/) para que sistemas tipo UNIX tengan máquinas virtuales que se inicien automáticamente, distinto al uso de un servicio systemd.

#### Iniciar máquinas virtuales con un atajo del teclado

Puede ser útil comenzar máquinas virtuales directamente con un atajo de teclado en lugar de utilizar la interfaz de VirtualBox (GUI o CLI). Para ello, solo tiene que definir combinaciones de teclas en `.xbindkeysrc`. Remítase a [Xbindkeys](/index.php/Xbindkeys "Xbindkeys") para más detalles.

He aquí un ejemplo, usando la tecla `Fn` del portatil con una tecla no utilizada (`F3` utilizada en este ejemplo):

```
"VBoxManage startvm 'Windows 7'"
m:0x0 + c:244
XF86Battery

```

**Nota:** Si se tiene un espacio en el nombre de la máquina virtual, entonces se encierra entre comillas simples, como se ha hecho en el ejemplo que acabamos de poner.

### Utilizar dispositivos específicos en la máquina virtual

#### Utilizar webcam / micrófono USB

**Nota:** Necesita tener el paquete de extensiones de VirtualBox instalado antes de seguir los pasos de abajo. Vea la sección [#Paquete de extensiones](#Paquete_de_extensiones) para más detalles.

1.  Asegúrese de que la máquina virtual no está en funcionamiento y no se está utilizando la webcam / micrófono.
2.  Haga que aparezca la ventana principal de VirtualBox y vaya a la configuración de la máquina de Arch. Navegue hasta la sección USB.
3.  Asegúrese de que está seleccionado «Enable USB Controller». Asegúrese también de que está seleccionado «Enable USB 2.0 (EHCI) Controller».
4.  Haga clic en el botón «Add filter from device» (el cable con el icono '+').
5.  Seleccione el dispositivo de cámara web/micrófono USB de la lista.
6.  Ahora, haga clic en Aceptar e inicie su máquina virtual.

#### Detectar cámaras web y otros dispositivos USB

Asegúrese de filtrar todos los dispositivos que no sean un teclado o un ratón para que no se inicien en el arranque y garantizar, de este modo, que Windows detecte el dispositivo en el arranque.

### Acceder a un servidor huésped

Para acceder a un [servidor Apache](https://en.wikipedia.org/wiki/es:Servidor_HTTP_Apache "wikipedia:es:Servidor HTTP Apache") en una máquina virtual de un **solo** equipo anfitrión, basta con ejecutar la siguientes líneas en el equipo anfitrión:

```
$ VBoxManage setextradata GuestName "VBoxInternal/Devices/*pcnet*/0/LUN#0/Config/Apache/HostPort" *8888*
$ VBoxManage setextradata GuestName "VBoxInternal/Devices/*pcnet*/0/LUN#0/Config/Apache/GuestPort" *80*
$ VBoxManage setextradata GuestName "VBoxInternal/Devices/*pcnet*/0/LUN#0/Config/Apache/Protocol" TCP

```

Donde 8888 es el puerto por el que el equipo anfitrión debe escuchar y el 80 es el puerto por el que la máquina virtual enviará la señal al servidor Apache.

Para utilizar un puerto inferior a 1024 en el equipo anfitrión, los cambios tienen que ser reflejados en el cortafuegos de la máquina anfitriona. Esto también puede ser configurado para trabajar con SSH o con cualquier otro servicio cambiando «Apache» para los servicios y puertos correspondientes.

**Nota:** `pcnet` se refiere a la tarjeta de red de la máquina virtual. Si utiliza una tarjeta de Intel en la configuración de la máquina virtual, cambie `pcnet` a `e1000`.

### Aceleración D3D en huéspedes Windows

Las versiones recientes de Virtualbox tienen soporte para la aceleración OpenGL dentro de los sistemas huéspedes. Esto se puede activar marcando una simple casilla en la configuración del equipo, justo debajo de donde se establece la memoria RAM de vídeo y la instalación de las aplicaciones del sistema huésped en VirtualBox. Sin embargo, la mayoría de los juegos de Windows utilizan Direct3D (parte de DirectX), no OpenGL, y, por lo tanto, no son ayudados por este método. No obstante, es posible obtener la aceleración Direct3D en los sistemas huéspedes Windows mediante préstamos de las bibliotecas D3D de wine, que traducen d3d a OpenGL, permitiendo la aceleración. Estas bibliotecas son ahora parte del software *guest additions* de Virtualbox.

Después de activar la aceleración OpenGL como se describió anteriormente, reinicie el sistema huésped en modo seguro (presione F8 antes de que aparezca la pantalla de Windows, pero después de que desaparezca la pantalla de Virtualbox), e instale las *guest additions* de Virtualbox, durante la instalación active la casilla «Direct3D support». Reinicie en modo normal y ya debería tener aceleración Direct3D.

**Nota:**

*   Este truco puede o no funcionar para algunos juegos en función de las comprobaciones que se haga del hardware y qué partes de D3D se utilice.
*   Esto fue probado en Windows XP, 7 y 8,1\. Si el método no funciona en su versión de Windows, por favor agregue los datos aquí.

### VirtualBox en una llave USB

Al usar VirtualBox en una llave USB, por ejemplo, para iniciar una máquina instalada una imagen ISO, tendrá que crear de forma manual VDMKs desde las unidades existentes. Sin embargo, una vez que los nuevos VMDK se guardan y se mueve a otra máquina, puede experimentar problemas al iniciar una máquina de forma apropiada de nuevo. Para deshacerse de este problema, puede utilizar el siguiente script para iniciar VirtualBox. Este script va a limpiar y eliminar el registro de archivos VMDK viejos y creará nuevos VMDK adecuados:

```
#!/bin/bash

# Borrar entradas viejas VMDK
rm ~/.VirtualBox/*.vmdk

# Limpiar registro VBox
sed -i '/sd/d' ~/.VirtualBox/VirtualBox.xml

# Eliminar discos duros antiguos de las máquinas existentes
find ~/.VirtualBox/Machines -name \*.xml | while read file; do
  line=`grep -e "type\=\"HardDisk\"" -n $file | cut -d ':' -f 1`
  if [ -n "$line" ]; then
    sed -i ${line}d $file
    sed -i ${line}d $file
    sed -i ${line}d $file
  fi
  sed -i "/rg/d" $file
done

# Eliminar archivos previos creados por VirtualBox
find  ~/.VirtualBox/Machines -name \*-prev -exec rm '{}' \;

# Recrear VMDKs
ls -l /dev/disk/by-uuid | cut -d ' ' -f 9,11 | while read ln; do
  if [ -n "$ln" ]; then
    uuid=`echo "$ln" | cut -d ' ' -f 1`
    device=`echo "$ln" | cut -d ' ' -f 2 | cut -d '/' -f 3 | cut -b 1-3`

    # Determinar si la unidad está ya montada
    checkstr1=`mount | grep $uuid`
    checkstr2=`mount | grep $device`
    checkstr3=`ls ~/.VirtualBox/*.vmdk | grep $device`
    if [[ -z "$checkstr1" && -z "$checkstr2" && -z "$checkstr3" ]]; then
      VBoxManage internalcommands createrawvmdk -filename ~/.VirtualBox/$device.vmdk -rawdisk /dev/$device -register
    fi
  fi
done

# Iniciar VirtualBox
VirtualBox

```

Tenga en cuenta que su usuario tiene que ser añadido al grupo «disk» para poder crear VMDK fuera de las unidades existentes.

### Ejecutar una instalación nativa de Arch Linux dentro de VirtualBox

Si tiene un sistema de arranque dual entre Arch Linux y otro sistema operativo, puede resultar sumamente tedioso tener que alternar entre uno y otro para trabajar. Por otro lado, mediante el uso de máquinas virtuales, solo se dispone de un pequeño fragmento de energía del equipo, que puede causar problemas cuando se trabaja en proyectos de cierta envergadura.

Esta guía le permitirá utilizar, en una máquina virtual, la instalación nativa de Arch Linux cuando se está ejecutando el segundo sistema operativo. De esta forma, mantendrá la capacidad de ejecutar cada sistema operativo de forma nativa, pero con la opción de ejecutar la instalación de Arch Linux en una máquina virtual.

#### Asegurarse de que se tiene un esquema de nombres persistentes

Dependiendo de la configuración del disco duro, la representación de los archivos de los dispositivos del disco duro pueden aparecer de forma diferente cuando se ejecuta la instalación de Arch Linux de forma nativa o en la máquina virtual. Este problema se produce cuando se utiliza [FakeRAID](/index.php/RAID#Implementation "RAID") por ejemplo. El dispositivo FakeRAID vendrá asignado como `/dev/mapper/` al ejecutar la distribución GNU/Linux de forma nativa, al tiempo que los demás dispositivos siguen siendo accesibles por separado. Sin embargo, en su máquina virtual, puede aparecer sin ningún mapeo como `/dev/sdaX` por ejemplo, porque los controladores que controlan el FakeRAID en su sistema operativo anfitrión (por ejemplo, Windows) se abstraerán del dispositivo FakeRAID.

Para evitar este problema, tendremos que utilizar un esquema de direccionamiento que sea persistente en ambos sistemas. Esto se puede lograr usando [UUID](/index.php/Fstab_(Espa%C3%B1ol)#UUID "Fstab (Español)") en su archivo `/etc/fstab`. Asegúrese de que su archivo [fstab](/index.php/Fstab "Fstab") utiliza UUID para solucionar este problema. Lea [fstab](/index.php/Fstab "Fstab") y [Persistent block device naming](/index.php/Persistent_block_device_naming "Persistent block device naming").

`/etc/fstab` no es el único lugar en el que se utilizan los UUID. Administradores y gestores de arranque hacen uso de ellos también. Por tanto, asegúrese de que estos realmente usan UUID.

	[GRUB Legacy](/index.php/GRUB_Legacy "GRUB Legacy")

Si todavía está utilizando el antiguo [GRUB Legacy](/index.php/GRUB_Legacy "GRUB Legacy"), lo mejor es que [actualice a GRUB2](/index.php/GRUB_Legacy#Upgrading_to_GRUB2 "GRUB Legacy"), ya que este paquete está ahora desatendido desde los repositorios oficiales de Arch Linux. Si desea mantenerlo, edite `/boot/grub/menu.lst` y sustituya la declaración `root=/dev/sdXX` en su entrada de arranque de Arch Linux por el mapeo UUID `/dev/disk/by-uuid/` correspondiente a su partición root.

```
title  Arch Linux
root
kernel /vmlinuz-linux root=*/dev/disk/by-uuid/0a3407de-014b-458b-b5c1-848e92a327a3* ro vga=773
initrd /initramfs-linux-vbox.img

```

Repita el proceso para la entrada fallback.

	[GRUB](/index.php/GRUB_(Espa%C3%B1ol) "GRUB (Español)")

Si está ejecutando la versión más reciente de [GRUB](/index.php/GRUB_(Espa%C3%B1ol) "GRUB (Español)") no tiene nada que hacer. Sin embargo, es una razón más para actualizar a GRUB2.

**Advertencia:**

*   Asegúrese de que su partición anfitriona solo es accesible en modo solo lectura desde su máquina virtual Arch Linux, esto evitará el riesgo de corrupción si estando en la partición anfitriona escribe en ella por descuido.
*   NUNCA debe permitir que VirtualBox arranque desde la entrada de su segundo sistema operativo, que, a modo de recordatorio, es usado como anfitrión de esta máquina virtual. Preste especial cuidado en colocar la entrada de su otro sistema operativo por defecto en su gestor de arranque. De un mayor margen de espera o póngalo debajo en el orden de preferencias.

#### Asegurarse de que su imagen mkinitcpio es correcta

Asegúrese de que la configuración de su [mkinitcpio](/index.php/Mkinitcpio_(Espa%C3%B1ol) "Mkinitcpio (Español)") utiliza el [HOOK](/index.php/Mkinitcpio_(Espa%C3%B1ol)#HOOKS "Mkinitcpio (Español)") `block`:

 `/etc/mkinitcpio.conf` 
```
[...]
HOOKS="base udev autodetect modconf *block* filesystems keyboard fsck"
[...]
```

Si no está presente, añádalo y regenere su initramfs con la orden `# mkinitcpio -p linux`, cuyo [uso se describe aquí con detalle](/index.php/Mkinitcpio#Image_creation_and_activation "Mkinitcpio").

#### Crear una configuración de máquina virtual para arrancar desde la unidad física

##### Crear una imagen .vmdk de disco raw

Ahora, tenemos que crear una nueva máquina virtual que utilizará un [disco RAW](https://www.virtualbox.org/manual/ch09.html#rawdisk) como unidad virtual, para lo cual vamos a utilizar un archivoVMDK de ~ 1Kio que será asignado a un disco físico. Desafortunadamente, VirtualBox no tiene esta opción en la interfaz gráfica de usuario, por lo que tendrá que utilizar la consola y utilizar una orden interna de `VBoxManage`.

Arranque el sistema anfitrión que utilizará la máquina virtual de Arch Linux. La orden tendrá que ser adaptada al sistema anfitrión que tenga.

	En un sistema anfitrión GNU/Linux

Hay 3 maneras de lograr esto: iniciando sesión como root, cambiando los derechos de acceso al dispositivo con `chmod` o añadiendo su usuario al grupo `disk`. Esta última forma es la más elegante, así que vamos a proceder de esa manera:

```
# gpasswd -a *your_user* disk

```

Aplicar la nueva configuración de grupo con:

```
$ newgrp

```

Ahora, puede utilizar la orden:

```
$ VBoxManage internalcommands createrawvmdk -filename */path/to/file.vmdk* -rawdisk */dev/sdb* -register 

```

Adaptar la orden anterior a sus características, especialmente la ruta, el nombre de la ubicación VMDK y la ubicación del disco raw para el mapeo que contiene la instalación de Arch Linux.

	En un sistema anfitrión Windows

Abra un símbolo del sistema como administrador.
**Sugerencia:** En Windows, abra la pantalla menú/inicio, escriba `cmd`, y pulse `Ctrl+Mayús+Intro`, esto es un acceso directo para ejecutar el programa seleccionado con derechos de administrador.
En Windows, como la convención de nombres de archivos del disco es diferente de UNIX, utilice esta orden para determinar qué unidades tiene en su sistema Windows y cuál es su ubicación: `# wmic diskdrive get name,size,model` 
```
Model                               Name                Size
WDC WD40EZRX-00SPEB0 ATA Device     \\.\PHYSICALDRIVE1  4000783933440
KINGSTON SVP100S296G ATA Device     \\.\PHYSICALDRIVE0  96024821760
Hitachi HDT721010SLA360 ATA Device  \\.\PHYSICALDRIVE2  1000202273280
Innostor Ext. HDD USB Device        \\.\PHYSICALDRIVE3  1000202273280
```

En este ejemplo, como la convención de Windows es `\\.\PhysicalDriveX` donde X es un número, `\\.\PHYSICALDRIVE1` podría ser análogo a `/dev/sdb` en la terminología de los discos en Linux.

Para usar la orden `VBoxManage` en Windows, puede, o bien moverse del directorio actual a la carpeta de instalación de VirtualBox primero con `cd C:\Program Files\Oracle\VirtualBox\`

```
# .\VBoxManage.exe internalcommands createrawvmdk -filename C:\file.vmdk -rawdisk \\.\PHYSICALDRIVE1

```

o bien, usar la ruta absoluta:

```
# «C:\Program Files\Oracle\VirtualBox\VBoxManage.exe» internalcommands createrawvmdk -filename C:\file.vmdk -rawdisk \\.\PHYSICALDRIVE1

```

	En un sistema anfitrión de otro sistema operativo

Hay otras limitaciones en cuanto a la orden antes mencionada cuando se utiliza en otros sistemas operativos como OS X, por favor [lea atentamente la página del manual](https://www.virtualbox.org/manual/ch09.html#rawdisk), si le concierne.

##### Crear el archivo de configuración de la máquina virtual

**Nota:**

*   Para hacer uso de la orden VBoxManage en Windows, es necesario primero moverse del directorio actual a la carpeta de instalación de VirtualBox: cd C:\Program Files\Oracle\VirtualBox\.
*   Windows hace uso de las barras invertidas en lugar de barras normales, de modo que no olvide cambiar las barras normales / a las barras invertidas \ cuando aparezcan en las órdenes que siguen.

Después, tenemos que crear una nueva máquina (sustituir el *VM_NAME* a su conveniencia) y registrarla en VirtualBox.

```
$ VBoxManage createvm -name *VM_name* -register

```

A continuación, el disco recién creado necesita ser asociado a la máquina. Esto dependerá si el equipo o raiz vigente de la instalación nativa de Arch Linux tiene una controladora IDE o SATA.

Si necesita una controladora IDE:

```
$ VBoxManage storagectl *VM_name* --name "IDE Controller" --add ide
$ VBoxManage storageattach machineA --storagectl "IDE Controller" --port 0 --device 0 --type hdd --medium /path/to/file.vmdk

```

de otro modo:

```
$ VBoxManage storagectl *VM_name* --name "SATA Controller" --add sata
$ VBoxManage storageattach machineA --storagectl "SATA Controller" --port 0 --device 0 --type hdd --medium /path/to/file.vmdk

```

Aunque utilice la CLI, es recomendable utilizar la interfaz gráfica de VirtualBox para personalizar la configuración de la máquina virtual. De hecho, debe especificar su configuración de hardware tan precisa como le sea posible, como si lo hiciese en una máquina nativa: conectar la aceleración 3D, aumentar la memoria de vídeo, ajustar la interfaz de red, etc.

#### Instalar Guest Additions

Por último, es posible que desee una integración perfecta entre su sistema Arch Linux y su sistema operativo anfitrión, permitiendo la función de pegar y copiar entre ambos sistemas operativos. Por favor, consulte [#Instalar complementos para el sistema huésped](#Instalar_complementos_para_el_sistema_hu.C3.A9sped) ya que, no debemos olvidar que esta máquina virtual de Arch Linux no deja de ser un sistema huésped cuando se ejecuta sobre el otro sistema operativo.

**Advertencia:** Para que [Xorg](/index.php/Xorg_(Espa%C3%B1ol) "Xorg (Español)") pueda funcionar tanto en forma nativa como en la máquina virtual, dado que va a utilizar diferentes controladores en uno u otro entorno, la mejor opción es que no exista un archivo `/etc/X11/xorg.conf`, de modo que se deje a Xorg que recoja todo lo que necesita sobre la marcha. Sin embargo, si realmente necesita su propia configuración Xorg, tal vez valga la pena establecer su target predefinido de systemd a `multi-user.target` con `# systemctl isolate graphical.target` (más detalles en [Systemd (Español)#Tabla de targetsy](/index.php/Systemd_(Espa%C3%B1ol)#Tabla_de_targets "Systemd (Español)") [Systemd (Español)#Cambiar el target vigente](/index.php/Systemd_(Espa%C3%B1ol)#Cambiar_el_target_vigente "Systemd (Español)"). De este modo, la interfaz gráfica estará desactivada (es decir Xorg no se pondrá en marcha) y, después de iniciar sesión, podrá ejecutar `startx` manualmente con un archivo `xorg.conf` personalizado.

### Instalar un sistema nativo de Arch Linux desde VirtualBox

En algunos casos, puede ser útil instalar un sistema nativo de Linux Arch mientras se ejecuta otro sistema operativo: una forma de lograr esto es realizar la instalación a través de VirtualBox en un [disco raw](http://www.virtualbox.org/manual/ch09.html#rawdisk). Si el sistema operativo existente está basado en Linux, es posible que desee considerar el siguiente artículo [Install from existing Linux](/index.php/Install_from_existing_Linux "Install from existing Linux") en su lugar.

Este escenario es muy similar a la [#Ejecutar una instalación nativa de Arch Linux dentro de VirtualBox](#Ejecutar_una_instalaci.C3.B3n_nativa_de_Arch_Linux_dentro_de_VirtualBox), pero seguirá los pasos en un orden diferente: empiece por [#Crear una imagen .vmdk de disco raw](#Crear_una_imagen_.vmdk_de_disco_raw), y luego [#Crear el archivo de configuración de la máquina virtual](#Crear_el_archivo_de_configuraci.C3.B3n_de_la_m.C3.A1quina_virtual).

Ahora, debe tener una configuración de máquina virtual funcional cuyos discos virtuales VMDK están ligados a un disco real. El proceso de instalación es exactamente lo mismo que el descrito en [#Pasos para preparar Arch Linux como sistema anfitrión](#Pasos_para_preparar_Arch_Linux_como_sistema_anfitri.C3.B3n), pero [asegurándose de que tiene un esquema de nombres persistentes](#Asegurarse_de_que_se_tiene_un_esquema_de_nombres_persistentes) y [que su imagen mkinitcpio es correcta](#Asegurarse_de_que_su_imagen_mkinitcpio_es_correcta).

**Advertencia:**

*   Para los sistemas BIOS con un esquema de particionado MBR, no instale un gestor de arranque en su máquina virtual, esto no funcionará ya que el MBR no está vinculado con el MBR de su máquina real y su disco virtual solo se asignaŕa como una partición real sin MBR.
*   Para los sistemas UEFI sin [Compatibility Support Module (CSM)](https://en.wikipedia.org/wiki/Compatibility_Support_Module#CSM "wikipedia:Compatibility Support Module") y con esquema de particionado GPT, la instalación no funcionará en absoluto, dado que:

*   la partición [EFI System partition (ESP)](https://en.wikipedia.org/wiki/EFI_System_partition para más detalles);
*   y las variables efivars, si va a instalar Arch Linux usando el modo EFI por intermediación de VirtualBox, no se corresponden con la de su sistema real: por lo tanto, las entradas de su gestor de arranque no serán registradas.

*   Esta razones hacen recomendable crear, primero, las particiones en una instalación nativa, de lo contrario las particiones no serán tomadas en consideración en su tabla de particiones MBR/GPT.

Después de completar la instalación, arranque el ordenador con un soporte de instalación de GNU/Linux (ya se trate de Arch Linux o no), entre en entorno [chroot](/index.php/Beginners%27_guide_(Espa%C3%B1ol)#Efectuar_chroot_y_configurar_el_sistema_base "Beginners' guide (Español)") en su recién instalado Arch Linux e [#instale y configure un gestor de arranque](/index.php/Beginners%27_guide_(Espa%C3%B1ol)#Instalar_un_gestor_de_arranque "Beginners' guide (Español)").

### Mover una instalación nativa de Windows a una máquina virtual

Si desea migrar una instalación de Windows nativa existente a una máquina virtual que se utilizará con VirtualBox en GNU/Linux, siga leyendo. Esta sección solo trata la instalación nativa de Windows utilizando el esquema de particiones MS-DOS/Intel. Su instalación de Windows debe residir en la primera partición del MBR para que esta operación tenga éxito. La operación también es posible en otras particiones, pero no ha sido probada (vea [#Known limitations](#Known_limitations) para conocer detalles).

**Advertencia:** Si está utilizando una versión OEM de Windows, este proceso no está autorizado por la licencia de usuario final. De hecho, la licencia OEM normalmente establece las instalación de Windows ligada al hardware específico del equipo donde se instala. Al transferir una instalación de Windows a una máquina virtual se elimina esa vinculación. Asegúrese de que tiene una instalación completa de Windows o un modelo de licencia por volumen antes de continuar. Si tiene una licencia completa de Windows, pero este último no viene en volumen, ni como una licencia especial para varios PC, esto significa que tendrá que quitar la instalación nativa después de que se haya logrado la operación de transferencia.

Se requiere un par de tareas a realizar en el interior de la instalación original de Windows primero, y luego en su sistema GNU/Linux anfitrión.

#### Tareas en Windows

Los primeros tres siguientes puntos vienen de [esta página desactualizada de la wiki de VirtualBox](https://www.virtualbox.org/wiki/Migrate_Windows#HAL), pero se actualizan aquí.

*   Elimine los chequeos de las controladoras de IDE/ATA (solo en Windows XP): Windows memoriza las controladoras de disco IDE/ATA cuando se ha instalado y no arrancará si detecta que estos han cambiado. La solución propuesta por Microsoft es volver a utilizar la misma controladora o utilizar una de la misma serie, lo cual es imposible de lograr ya que estamos utilizando una máquina virtual. Se puede utilizar [MergeIDE](https://www.virtualbox.org/wiki/Migrate_Windows#HardDiskSupport), una herramienta alemana, desarrollada sobre la base de una solución propuesta por Microsoft. Esta solución consiste básicamente en tomar todos los controladores de la controladora ATA/IDE compatibles con Windows XP desde el archivo del controlador inicial (la ubicación está codificada, o especificada como el primer argumento del script `.bat`), instalándolos y registrándolos con la base de datos regedit.

*   Utilice el tipo Hardware Abstraction Layer (versiones de Windows de 32 bits viejas): Microsoft incluye 3 versiones por defecto: `Hal.dll` (Standard PC), `Halacpi.dll` (ACPI HAL) y `Halaacpi.dll` (ACPI HAL con IO APIC). Su instalación de Windows podría venir instalado con la primera o la segunda versión. Si es así [desactive la característica extendida *Enable IO/APIC* de VirtualBox](https://www.virtualbox.org/manual/ch08.html#idp56927888).

*   Desactive cualquier controlador del dispositivo AGP (solo versiones obsoletas de Windows): si tiene los archivos `agp440.sys` o `intelppm.sys` dentro de la carpeta `C:\Windows\SYSTEM32\drivers\` retírelos. Como VirtualBox utiliza una tarjeta gráfica PCI virtual, esto puede causar problemas cuando se utiliza este controlador AGP.

*   Crear un disco de recuperación de Windows: en los siguientes pasos, si la operación sale mal, tendrá que reparar la instalación de Windows. Asegúrese de tener un soporte de instalación a mano, o cree uno con la utilidad *Crear un disco de recuperación* de Windows.

#### Tareas en GNU/Linux

*   Reduzca el tamaño de la partición donde tenga instalado Windows nativo al tamaño que Windows necesita realmente con `ntfsresize`, disponible en el paquete [ntfs-3g](https://www.archlinux.org/packages/?name=ntfs-3g). El tamaño que especifique será el mismo tamaño de la VDI que se creará en el siguiente paso. Si este tamaño es demasiado bajo, es posible romper su instalación de Windows y este último podría provocar que no arranque en absoluto.

	Utilice la opción `--no-action` primero para realizar una prueba:

	 `# ntfsresize --no-action --size *52Gi* */dev/sda1*` 

	Si la prueba anterior tuvo éxito, ejecute la orden de nuevo, pero esta vez sin la opción antes mencionada.

*   Instale VirtualBox en su sistema anfitrión GNU/Linux (vea [#Pasos para preparar Arch Linux como sistema anfitrión](#Pasos_para_preparar_Arch_Linux_como_sistema_anfitri.C3.B3n) si su sistema anfitrión es Arch Linux).

*   Cree la imagen de disco de Windows desde el principio de la unidad hasta el final de la primera partición donde se encuentra la instalación de Windows. Es necesario copiar desde el principio del disco porque el espacio del MBR del principio de la unidad tiene que estar en la unidad virtual junto con la partición de Windows. En este ejemplo las dos siguientes particiones `sda2` y `sda3` serán eliminadas de la tabla de particiones y el gestor de arranque MBR será actualizado.

	 `# sectnum=$(( $(cat /sys/block/''sda/sda1''/start) + $(cat /sys/block/''sda/sda1''/size) ))` 

	El uso de `cat /sys/block/*sda/sda1*/size` mostrará el número de sectores totales de la primera partición del disco `sda`. Adaptar cuando sea necesario.

	 `# dd if=''/dev/sda'' bs=512 count=$sectnum | VBoxManage convertfromraw stdin ''windows.vdi'' $(( $sectnum * 512 ))` 

	Tenemos que obtener el tamaño en bytes, `$(( $sectnum * 512 ))` convertirá los números de sector a bytes.

*   Cree el archivo de configuración de la máquina virtual y utilice el disco virtual creado anteriormente como disco duro virtual principal. `# chown $USER:users windows.vdi`.

*   Trate de arrancar su maquina virtual de Windows, Debería funcionar sin más. Primero, sin embargo, retire y repare los discos desde el proceso de arranque, ya que pueden interferir (y probablemente lo hagan) arrancar en modo seguro.

*   Intente arrancar su máquina virtual Windows en modo seguro (pulse la tecla F8 antes de que el logotipo de Windows aparezca)... si se dan problemas de arranque, lea [#Arreglar el MBR y el gestor de arranque de Microsoft](#Arreglar_el_MBR_y_el_gestor_de_arranque_de_Microsoft). En modo seguro, los controladores se instalarán probablemente por el mecanismo de detección plug-and-play de Windows ([vistas](http://i.imgur.com/hh1RrSp.png)). Adicionalmente, instale los Guest Additions de VirtualBox a través del menú *Devices* > *Insert Guest Additions CD image...*. Si no aparece un nuevo diálogo para el disco, vaya a la unidad del CD e inicie el instalador manualmente.

*   Finalmente, debe tener una máquina virtual de Windows funcional. No se olvide de leer las [#Limitaciones conocidas](#Limitaciones_conocidas).

#### Arreglar el MBR y el gestor de arranque de Microsoft

Si su máquina virtual Windows se niega a arrancar, puede que tenga que aplicar las siguientes modificaciones a su máquina virtual.

*   Arranque una distribución GNU/Linux en su máquina virtual antes de que Windows se inicie.

*   Retire las otras entradas de las particiones del MBR del disco virtual. De hecho, ya hemos copiado el MBR y dejado únicamente la partición de Windows, las entradas de las otras particiones están todavía presentes en el MBR, pero las particiones ya no están disponibles. Use `fdisk` para lograr esto, por ejemplo.

```
fdisk ''/dev/sda''
Command (m for help): a
Partition number (''1-3'', default ''3''): ''1''
```

*   Escriba la tabla de partición actualizada en el disco (esto volverá a crear el MBR) utilizando la orden `m` con `fdisk`.

*   Utilice [testdisk](https://www.archlinux.org/packages/?name=testdisk) (vea [esto](http://www.cgsecurity.org/index.html?testdisk.html) para más detalles) para añadir un MBR genérico:

	 `# testdisk > *Disk /dev/sda...'* > [Proceed] >  [Intel] Intel/PC partition > [MBR Code] Write TestDisk MBR to first sector > Write a new copy of MBR code to first sector? (Y/n) > Y > Write a new copy of MBR code, confirm? (Y/N) > A new copy of MBR code has been written. You have to reboot for the change to take effect. > [OK]` 

*   Con el nuevo MBR y la tabla de particiones actualizada, su máquina virtual Windows debería ser capaz de arrancar. Si todavía encuentra problemas, arranque su disco de recuperación de Windows aconsejado realizar en la etapa anterior y, dentro de su entorno de Windows de recuperación, ejecute las órdenes [descritas aquí](http://support.microsoft.com/kb/927392).

#### Limitaciones conocidas

*   Su máquina virtual, a veces, puede colgarse y desbordar la memoria RAM, lo cual puede ser causado por controladores en conflicto todavía instalados en su máquina virtual Windows. ¡Buena suerte en encontrarlos!
*   El software adicional que espera un controlador dado puede, o bien estar el controlador desactivado/desinstalado, o bien el software necesita ser desinstalado primero respecto de los controladores que ya no están disponibles.
*   Su instalación de Windows debe residir en la primera partición para que el proceso anterior pueda funcionar. Si no se cumple este requisito, el proceso podría lograrse también, pero esto no ha sido probado. Para ello será necesario copiar el MBR y editarlo en formato hexadecimal (vea [VirtualBox: arrancar disco clonado](http://superuser.com/questions/237782/virtualbox-booting-cloned-disk/253417#253417)) lo cual requerirá arreglar la tabla de particiones, bien [manualmente](http://gparted.org/h2-fix-msdos-pt.php), o bien mediante la reparación de Windows con el disco de recuperación que creó en el paso anterior. Consideremos que nuestra instalación de Windows está en la segunda partición; vamos a copiar el MBR y, a continuación, la segunda partición en la que reside la imagen del disco. `VBoxManage convertfromraw` necesita saber el número total de bytes que se escribirán: calculados gracias al tamaño del MBR (el comienzo de la primera partición) más el tamaño de la segunda partición (Windows). `{ dd if=/dev/sda bs=512 count=$(cat /sys/block/sda/sda1/start) ; dd if=/dev/sda2 bs=512 count=$(cat /sys/block/sda/sda2/size) ; } | VBoxManage convertfromraw stdin windows.vdi $(( ($(cat /sys/block/sda/sda1/start) + $(cat /sys/block/sda/sda2/size)) * 512 ))`.

## Solución de problemas

### Teclado y ratón bloqueados en la máquina virtual

Esto significa que su máquina virtual ha capturado la entrada de su teclado y del ratón. Basta con pulsar la tecla `Ctrl` derecho y su entrada debería volver al control de su sistema anfitrión de nuevo.

Para controlar de forma transparente su máquina virtual con el ratón de modo que pueda pasear entre esta y el equipo anfitrión sin tener que pulsar ninguna tecla y con una integración perfecta, instale las *guest additions* dentro del sistema huésped. Lea los pasos para [#Instalar complementos para el sistema huésped](#Instalar_complementos_para_el_sistema_hu.C3.A9sped) si su sistema huésped es Arch Linux, en otro caso, lea la ayuda oficial de VirtualBox.

### No se pueden usar las teclas CTRL+ALT+Fn en la máquina virtual

Si su sistema operativo huésped es una distribución de GNU/Linux puede abrir una nueva shell TTY con `Ctrl+Alt+F2` o salir de su sesión X actual con `Ctrl+Alt+Retroceso`. No obstante, si escribe estos atajos de teclado sin ninguna adaptación, el sistema huésped no recibirá ninguna entrada y el anfitrión (si se trata de una distribución GNU/Linux, tampoco) no interpretando estas teclas de acceso directo. Para enviar `Ctrl+Alt+F2` al sistema huésped, por ejemplo, basta con pulsar *«Host Key»*, (normalmente la tecla `Ctrl`) y `F2` simultáneamente.

### Arreglar problemas de imágenes ISO

Mientras que VirtualBox puede montar imágenes ISO sin problema, hay algunos formatos de imagen que no se pueden convertir a ISO de forma fiable. Por ejemplo, ccd2iso ignora archivos .ccd y .sub, lo que puede dar como resultado imágenes de disco con archivos dañados.

En estos casos, tendrá que usar [CDemu](/index.php/CDemu "CDemu") para Linux dentro de VirtualBox o cualquier otra herramienta que se utiliza para montar imágenes de disco.

### La interfaz gráfica de VirtualBox no coincide con mi tema GTK

Vea [Uniform look for Qt and GTK applications](/index.php/Uniform_look_for_Qt_and_GTK_applications "Uniform look for Qt and GTK applications") para obtener información sobre la tematización de aplicaciones basadas en Qt como VirtualBox.

### OpenBSD inutilizable cuando las instrucciones de virtualización no están disponibles

Mientras que es sabido que OpenBSD puede funcionar bien en otros hipervisores sin las instrucciones (VT-x AMD-V) de virtualización activadas, una máquina virtual OpenBSD que se ejecuta en VirtualBox sin estas instrucciones no se podrá utilizar, dando lugar a fallos de segmentación. Iniciando VirtualBox con el argumento *-norawr0* [se puede resolver este problema](https://www.virtualbox.org/ticket/3947). Puede hacerlo de esta manera:

```
$ VBoxSDL -norawr0 -vm *name_of_OpenBSD_VM*

```

### VBOX_E_INVALID_OBJECT_STATE (0x80BB0007)

Esto puede ocurrir si una máquina virtual se apaga mal. La solución para desbloquear la máquina virtual es trivial:

```
$ VBoxManage controlvm *virtual_machine_name* poweroff

```

### Subsistema USB no funciona en el sistema anfitrión o huésped

Su usuario debe estar en el grupo `vboxusers`, necesario para instalar el [paquete de extensiones](#Paquete_de_extensiones) si desea apoyo de USB 2\. Entonces será capaz de activar USB 2 en la configuración de la máquina virtual y añadir uno o varios filtros para los dispositivos a los que desee acceder desde el sistema operativo huésped.

A veces, en equipos con Linux antiguo, el subsistema USB no se detecta automáticamente lo que da el error `Could not load the Host USB Proxy service: VERR_NOT_FOUND` o la unidad USB no es visible en el equipo, [incluso cuando el usuario está en el grupo **vboxusers**](https://bbs.archlinux.org/viewtopic.php?id=121377). Este problema es debido al hecho de que VirtualBox cambió de *usbfs* a *sysfs* en la versión 3.0.8\. Si el sistema anfitrión no entiende este cambio, puede revertir el comportamiento definiendo la siguiente variable de entorno en cualquier archivo fuente de la shell (por ejemplo, su `~/.bashrc` si usa *bash*):

 `~/.bashrc`  `VBOX_USB=usbfs` 

A continuación, asegúrese de que el entorno ha sido informado de este cambio (reconectar usb, recargar el archivo fuente manualmente, iniciar una instancia de shell o reiniciar equipo de nuevo).

También asegúrese de que su usuario es miembro del grupo `storage`.

### Error al crear la interfaz de red única del anfitrión

Asegúrese de que todos los módulos del kernel necesarios están cargados. Véase [#Cargar los módulos del kernel de VirtualBox](#Cargar_los_m.C3.B3dulos_del_kernel_de_VirtualBox).

### WinXP: Bit-depth no puede ser mayor que 16

Si está ejecutando una profundidad de color de 16 bits, entonces los iconos pueden aparecer borrosos/entrecortados. Sin embargo, al intentar cambiar la profundidad de color a un nivel más alto, el sistema puede estar restringido a una resolución inferior o simplemente no le permita cambiar la profundidad en absoluto. Para solucionar este problema, ejecute `regedit` en Windows y agregue la siguiente clave del registro para la máquina virtual Windows:

```
[HKEY_LOCAL_MACHINE\SOFTWARE\Policies\Microsoft\Windows NT\Terminal Services]
"ColorDepth"=dword:00000004

```

A continuación, actualice la profundidad de color en la ventana «desktop properties». Si no ocurre nada, fuerce la pantalla a redibujarse a través de algún método (es decir, `Host+f` para redibujar/introducir la pantalla completa).

### Utilizar puerto de serie en el sistema operativo huésped

Compruebe su permiso para el puerto de serie:

```
$ /bin/ls -l /dev/ttyS*
crw-rw---- 1 root uucp 4, 64 Feb  3 09:12 /dev/ttyS0
crw-rw---- 1 root uucp 4, 65 Feb  3 09:12 /dev/ttyS1
crw-rw---- 1 root uucp 4, 66 Feb  3 09:12 /dev/ttyS2
crw-rw---- 1 root uucp 4, 67 Feb  3 09:12 /dev/ttyS3

```

Añade su usuario al grupo `uucp`.

```
# gpasswd -a $USER uucp 

```

y, cierre y abra sesión de nuevo.

### Windows 8.x Error Code 0x000000C4

Si recibe este código de error durante el arranque, incluso si elige sistema operativo Tipo Win 8, pruebe a activar la instrucción `CMPXCHG16B` de la CPU:

```
$ vboxmanage setextradata *virtual_machine_name* VBoxInternal/CPUM/CMPXCHG16B 1

```

### Fallos de la máquina vitual de Windows 8 al arrancar con el error «ERR_DISK_FULL»

Situación: su máquina virtual Windows 8 se niega a iniciar. VirtualBox lanza un error que indica que el disco virtual está lleno. Sin embargo, está seguro de que el disco no está lleno. Abra la configuración de su máquina virtual en *Settings > Storage > Controller:SATA* y seleccione «Use Host I/O Cache».

### El sistema huésped Linux tiene audio lento/distorsionado

El controlador de audio AC97 dentro del kernel de Linux de vez en cuando define los ajustes del reloj de forma equivocada cuando se ejecuta dentro de Virtual Box, lo que lleva a que el audio sea demasiado lento o demasiado rápido. Para solucionar este problema, cree un archivo en `/etc/modprobe.d` con la siguiente línea:

```
options snd-intel8x0 ac97_clock=48000

```

### El huésped se congela después de iniciar Xorg

Controladores defectuosos o ausentes pueden causar que el sistema huésped se congele después de comenzar Xorg, vea, por ejemplo, [[3]](https://bbs.archlinux.org/viewtopic.php?pid=1167838) y [[4]](https://bbs.archlinux.org/viewtopic.php?id=156079). Pruebe a desactivar la aceleración 3D en *Settings > Display*, y comprobar si se han instalado todos los controladores [Xorg](/index.php/Xorg "Xorg").

### «NS_ERROR_FAILURE» y ausencia de elementos del menú

Si encuentra este mensaje cada vez que inicia la máquina virtual:

```
Failed to open a session for the virtual machine debian.
Could not open the medium '/home/.../VirtualBox VMs/debian/debian.qcow'.
QCow: Reading the L1 table for image '/home/.../VirtualBox VMs/debian/debian.qcow' failed (VERR_EOF).
VD: error VERR_EOF opening image file '/home/.../VirtualBox VMs/debian/debian.qcow' (VERR_EOF).

Result Code: 
NS_ERROR_FAILURE (0x80004005)
Component: 
Medium

```

Salga de VirtualBox, elimine todos los archivos de la nueva máquina y del archivo de configuración de VirtualBox elimine la última línea del menú `MachineRegistry` (o la máquina hostil que lo está creando):

 `~/.config/VirtualBox/VirtualBox.xml` 
```
...
<MachineRegistry>
  <MachineEntry uuid="{00000000-0000-0000-0000-000000000000}" src="/home/void/VirtualBox VMs/debian/debian.vbox"/>
  <MachineEntry uuid="{00000000-0000-0000-0000-000000000000}" src="/home/void/VirtualBox VMs/ubuntu/ubuntu.vbox"/>
  ~~<MachineEntry uuid="{00000000-0000-0000-0000-000000000000}" src="/home/void/VirtualBox VMs/lastvmcausingproblems/lastvmcausingproblems.qcow"/>~~
</MachineRegistry>
...
```

Esto ocurre, a veces, cuando se selecciona el formato de disco *QCOW*/*QCOW2*/*QED* al crear un disco virtual nuevo.

### Error en Windows huésped «The specified path does not exist. Check the path and then try again.»

Este mensaje de error aparece a menudo cuando se ejecuta un archivo .exe que requiere privilegios de administrador de una carpeta compartida en un sistema huésped Windows. Vea [este informe de error](https://www.virtualbox.org/ticket/5732) para más detalles.

Hay varias soluciones:

1.  Desactive UAC en el Panel de Control -> Action Center -> «Change User Account Control settings» del panel lateral izquierdo -> ajustar slider a «Never notify» -> OK y reiniciar.
2.  Copie el archivo de la carpeta compartida para el sistema huésped y ejecute desde allí
3.  Control Panel -> Network and Internet -> Internet Options -> Security -> Trusted Sites -> Sites -> Añada «VBOXSVR» como un sitio web
4.  Menú/Inicio -> escriba «gpedit.msc» y pulse Intro -> Computer Configuration -> Administrative Templates -> Windows Components -> Internet Explorer -> Internet Control Panel -> Security Page -> Size to Zone Assignment List -> Ajuste «VBOXSVR» a «2» y reinicie.

## Véase también

*   [VirtualBox User Manual](https://www.virtualbox.org/manual/UserManual.html)
*   [Wikipedia:VirtualBox](https://en.wikipedia.org/wiki/VirtualBox "wikipedia:VirtualBox")