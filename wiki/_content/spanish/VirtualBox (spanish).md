**Estado de la traducción**
Este artículo es una traducción de [VirtualBox](/index.php/VirtualBox "VirtualBox"), revisada por última vez el **018-11-09**. Si advierte que la versión inglesa [ha cambiado](https://wiki.archlinux.org/index.php?title=VirtualBox&diff=0&oldid=550472) puede ayudar a actualizar la traducción, bien por [usted mismo](/index.php/ArchWiki:Translation_Team/Contributing_(Espa%C3%B1ol) "ArchWiki:Translation Team/Contributing (Español)") o bien avisando al [equipo de traducción](/index.php/ArchWiki:Translation_Team_(Espa%C3%B1ol) "ArchWiki:Translation Team (Español)").

Artículos relacionados

*   [VirtualBox/Tips and tricks (Español)](/index.php/VirtualBox/Tips_and_tricks_(Espa%C3%B1ol) "VirtualBox/Tips and tricks (Español)")
*   [Category:Hypervisors (Español)](/index.php/Category:Hypervisors_(Espa%C3%B1ol) "Category:Hypervisors (Español)")
*   [PhpVirtualBox](/index.php/PhpVirtualBox "PhpVirtualBox")
*   [RemoteBox](/index.php/RemoteBox "RemoteBox")
*   [Moving an existing install into (or out of) a virtual machine](/index.php/Moving_an_existing_install_into_(or_out_of)_a_virtual_machine "Moving an existing install into (or out of) a virtual machine")

[VirtualBox](https://www.virtualbox.org) es un [hipervisor](https://en.wikipedia.org/wiki/es:Hypervisor "wikipedia:es:Hypervisor") que se utiliza para ejecutar sistemas operativos en un entorno especial, llamado máquina virtual, corriendo sobre un sistema operativo ya existente. VirtualBox está en constante desarrollo y las nuevas características se implementan continuamente. Viene con una interfaz gráfica basada en [Qt](/index.php/Qt "Qt"), así como herramientas de línea de órdenes [SDL](https://en.wikipedia.org/wiki/Simple_DirectMedia_Layer "wikipedia:Simple DirectMedia Layer") y *headless* para la gestión y ejecución de máquinas virtuales.

Con el fin de integrar las funciones del sistema anfitrión en los sistemas huéspedes, incluyendo carpetas compartidas y portapapeles, aceleración de vídeo y un modo de integración de ventanas fluido, se proporcionan complementos huéspedes (*guest additions*) para algunos sistemas operativos huéspedes.

## Contents

*   [1 Pasos para preparar Arch Linux como sistema anfitrión](#Pasos_para_preparar_Arch_Linux_como_sistema_anfitri.C3.B3n)
    *   [1.1 Instalar los paquetes principales](#Instalar_los_paquetes_principales)
    *   [1.2 Firmar los módulos](#Firmar_los_m.C3.B3dulos)
    *   [1.3 Cargar los módulos del kernel de VirtualBox](#Cargar_los_m.C3.B3dulos_del_kernel_de_VirtualBox)
    *   [1.4 Acceder al dispositivos USB del anfitrión desde el huésped](#Acceder_al_dispositivos_USB_del_anfitri.C3.B3n_desde_el_hu.C3.A9sped)
    *   [1.5 Disco de «Guest Additions»](#Disco_de_.C2.ABGuest_Additions.C2.BB)
    *   [1.6 Paquete de extensiones](#Paquete_de_extensiones)
    *   [1.7 Utilizar el front-end adecuado](#Utilizar_el_front-end_adecuado)
*   [2 Pasos para instalar Arch Linux como sistema huésped](#Pasos_para_instalar_Arch_Linux_como_sistema_hu.C3.A9sped)
    *   [2.1 Instalación en modo EFI](#Instalaci.C3.B3n_en_modo_EFI)
    *   [2.2 Instalar los «Guest Additions»](#Instalar_los_.C2.ABGuest_Additions.C2.BB)
    *   [2.3 Establecer la resolución óptima de framebuffer](#Establecer_la_resoluci.C3.B3n_.C3.B3ptima_de_framebuffer)
    *   [2.4 Cargar los módulos del kernel de VirtualBox](#Cargar_los_m.C3.B3dulos_del_kernel_de_VirtualBox_2)
    *   [2.5 Lanzar los servicios de VirtualBox en el sistema huésped](#Lanzar_los_servicios_de_VirtualBox_en_el_sistema_hu.C3.A9sped)
    *   [2.6 Aceleracion de hardware](#Aceleracion_de_hardware)
    *   [2.7 Activar carpetas compartidas](#Activar_carpetas_compartidas)
        *   [2.7.1 Montaje manual](#Montaje_manual)
        *   [2.7.2 Montaje automático](#Montaje_autom.C3.A1tico)
        *   [2.7.3 Montaje durante el arranque](#Montaje_durante_el_arranque)
    *   [2.8 SSH de anfitrión a huésped](#SSH_de_anfitri.C3.B3n_a_hu.C3.A9sped)
        *   [2.8.1 SSHFS como alternativa a la carpeta compartida](#SSHFS_como_alternativa_a_la_carpeta_compartida)
*   [3 Gestionar discos virtuales](#Gestionar_discos_virtuales)
    *   [3.1 Formatos soportados por VirtualBox](#Formatos_soportados_por_VirtualBox)
    *   [3.2 Conversión de formatos de imagen de disco](#Conversi.C3.B3n_de_formatos_de_imagen_de_disco)
        *   [3.2.1 QCOW](#QCOW)
    *   [3.3 Montar discos virtuales](#Montar_discos_virtuales)
        *   [3.3.1 VDI](#VDI)
    *   [3.4 Discos virtuales compactos](#Discos_virtuales_compactos)
    *   [3.5 Aumentar discos virtuales](#Aumentar_discos_virtuales)
        *   [3.5.1 Procedimiento general](#Procedimiento_general)
        *   [3.5.2 Aumentar el tamaño de los discos VDI](#Aumentar_el_tama.C3.B1o_de_los_discos_VDI)
    *   [3.6 Reemplazar un disco virtual de forma manual desde el archivo .vbox](#Reemplazar_un_disco_virtual_de_forma_manual_desde_el_archivo_.vbox)
        *   [3.6.1 Transferencia entre el anfitrión de Linux y otro sistema operativo](#Transferencia_entre_el_anfitri.C3.B3n_de_Linux_y_otro_sistema_operativo)
    *   [3.7 Clonar un disco virtual y asignarle un UUID nuevo](#Clonar_un_disco_virtual_y_asignarle_un_UUID_nuevo)
*   [4 Consejos y trucos](#Consejos_y_trucos)
*   [5 Solución de problemas](#Soluci.C3.B3n_de_problemas)
    *   [5.1 Teclado y ratón bloqueados en la máquina virtual](#Teclado_y_rat.C3.B3n_bloqueados_en_la_m.C3.A1quina_virtual)
    *   [5.2 No hay opciones del sistema operativo de 64 bits para el cliente](#No_hay_opciones_del_sistema_operativo_de_64_bits_para_el_cliente)
    *   [5.3 La interfaz gráfica de VirtualBox no coincide con el tema GTK](#La_interfaz_gr.C3.A1fica_de_VirtualBox_no_coincide_con_el_tema_GTK)
    *   [5.4 No se pueden usar las teclas CTRL+ALT+Fn en la máquina virtual](#No_se_pueden_usar_las_teclas_CTRL.2BALT.2BFn_en_la_m.C3.A1quina_virtual)
    *   [5.5 El subsistema USB no funciona](#El_subsistema_USB_no_funciona)
    *   [5.6 El módem USB no funciona en el sistema anfitrión](#El_m.C3.B3dem_USB_no_funciona_en_el_sistema_anfitri.C3.B3n)
    *   [5.7 Acceder al puerto serie desde el sistema huésped](#Acceder_al_puerto_serie_desde_el_sistema_hu.C3.A9sped)
    *   [5.8 El sistema huésped se congela después de iniciar Xorg](#El_sistema_hu.C3.A9sped_se_congela_despu.C3.A9s_de_iniciar_Xorg)
    *   [5.9 El modo de pantalla completa muestra la pantalla en blanco](#El_modo_de_pantalla_completa_muestra_la_pantalla_en_blanco)
    *   [5.10 El sistema anfitrión se congela en el inicio de la máquina virtual](#El_sistema_anfitri.C3.B3n_se_congela_en_el_inicio_de_la_m.C3.A1quina_virtual)
    *   [5.11 El sistema huésped Linux tiene audio lento/distorsionado](#El_sistema_hu.C3.A9sped_Linux_tiene_audio_lento.2Fdistorsionado)
    *   [5.12 El micrófono analógico no funciona](#El_micr.C3.B3fono_anal.C3.B3gico_no_funciona)
    *   [5.13 El micrófono no funciona después de la actualización](#El_micr.C3.B3fono_no_funciona_despu.C3.A9s_de_la_actualizaci.C3.B3n)
    *   [5.14 Problemas con imágenes convertidas a ISO](#Problemas_con_im.C3.A1genes_convertidas_a_ISO)
    *   [5.15 Error al crear la interfaz de red única del anfitrión](#Error_al_crear_la_interfaz_de_red_.C3.BAnica_del_anfitri.C3.B3n)
    *   [5.16 Error al insertar el módulo](#Error_al_insertar_el_m.C3.B3dulo)
    *   [5.17 VBOX_E_INVALID_OBJECT_STATE (0x80BB0007)](#VBOX_E_INVALID_OBJECT_STATE_.280x80BB0007.29)
    *   [5.18 «NS_ERROR_FAILURE» y ausencia de elementos del menú](#.C2.ABNS_ERROR_FAILURE.C2.BB_y_ausencia_de_elementos_del_men.C3.BA)
    *   [5.19 Arch: el script pacstrap falla](#Arch:_el_script_pacstrap_falla)
    *   [5.20 OpenBSD queda inutilizable cuando las instrucciones de virtualización no están disponibles](#OpenBSD_queda_inutilizable_cuando_las_instrucciones_de_virtualizaci.C3.B3n_no_est.C3.A1n_disponibles)
    *   [5.21 Anfitrión Windows: VERR_ACCESS_DENIED](#Anfitri.C3.B3n_Windows:_VERR_ACCESS_DENIED)
    *   [5.22 Windows: «La ruta especificada no existe. Verifique la ruta y luego inténtelo nuevamente».](#Windows:_.C2.ABLa_ruta_especificada_no_existe._Verifique_la_ruta_y_luego_int.C3.A9ntelo_nuevamente.C2.BB.)
    *   [5.23 Código de error 0x000000C4 de Windows 8.x](#C.C3.B3digo_de_error_0x000000C4_de_Windows_8.x)
    *   [5.24 Windows 8, 8.1 o 10 no se instala, no se inicia o da el error «ERR_DISK_FULL»](#Windows_8.2C_8.1_o_10_no_se_instala.2C_no_se_inicia_o_da_el_error_.C2.ABERR_DISK_FULL.C2.BB)
    *   [5.25 WinXP: la profundidad de bits no puede ser mayor que 16](#WinXP:_la_profundidad_de_bits_no_puede_ser_mayor_que_16)
    *   [5.26 Windows: la pantalla parpadea si la aceleración 3D está activada](#Windows:_la_pantalla_parpadea_si_la_aceleraci.C3.B3n_3D_est.C3.A1_activada)
    *   [5.27 Sin aceleración 3D de hardware en Arch Linux huésped](#Sin_aceleraci.C3.B3n_3D_de_hardware_en_Arch_Linux_hu.C3.A9sped)
*   [6 Véase también](#V.C3.A9ase_tambi.C3.A9n)

## Pasos para preparar Arch Linux como sistema anfitrión

Para poner en marcha máquinas virtuales de VirtualBox emarcadas en su sistema Arch Linux, siga estos pasos de instalación.

### Instalar los paquetes principales

[Instale](/index.php/Install "Install") el paquete [virtualbox](https://www.archlinux.org/packages/?name=virtualbox). Deberá elegir un paquete para proporcionar módulos al sistema anfitrión:

*   para el kernel [linux](https://www.archlinux.org/packages/?name=linux) elija [virtualbox-host-modules-arch](https://www.archlinux.org/packages/?name=virtualbox-host-modules-arch)
*   para otros [kernels](/index.php/Kernels "Kernels") elija [virtualbox-host-dkms](https://www.archlinux.org/packages/?name=virtualbox-host-dkms)
    *   También es necesario instalar los paquetes de encabezados adecuados para su kernel(s) instalado(s): [linux-headers](https://www.archlinux.org/packages/?name=linux-headers) o [linux-lts-headers](https://www.archlinux.org/packages/?name=linux-lts-headers). [[1]](https://lists.archlinux.org/pipermail/arch-dev-public/2016-March/027808.html) Cuando se actualice VirtualBox o el kernel, los módulos del kernel se volverán a compilar automáticamente gracias al hook [DKMS](/index.php/DKMS "DKMS") de Pacman.

### Firmar los módulos

Cuando use un kernel personalizado con la opción `CONFIG_MODULE_SIG_FORCE` activada, debe firmar sus módulos con una clave generada durante la compilación del kernel.

Navegue a la carpeta del árbol del kernel y ejecute la siguiente orden:

```
# for module in `ls /lib/modules/$(uname -r)/kernel/misc/{vboxdrv.ko,vboxnetadp.ko,vboxnetflt.ko,vboxpci.ko}` ; do ./scripts/sign-file sha1 certs/signing_key.pem certs/signing_key.x509 $module ; done

```

**Nota:** el algoritmo de hash no tiene que coincidir con el configurado, pero debe estar integrado en el kernel.

### Cargar los módulos del kernel de VirtualBox

[virtualbox-host-modules-arch](https://www.archlinux.org/packages/?name=virtualbox-host-modules-arch) y [virtualbox-host-dkms](https://www.archlinux.org/packages/?name=virtualbox-host-dkms) usa `systemd-modules-load.service` para cargar los cuatro módulos de VirtualBox automáticamente en el momento del arranque. Para que los módulos se carguen después de la instalación, reinicie o cargue los módulos una vez manualmente.

**Nota:** si no desea que los módulos de VirtualBox se carguen automáticamente en el momento del arranque, debe [enmascarar](/index.php/Mask "Mask") el archivo predeterminado `/usr/lib/modules-load.d/virtualbox-host-modules-arch.conf` (o `/usr/lib/modules-load.d/virtualbox-host-dkms.conf`)creando un archivo vacío (o enlace simbólico a `/dev/null`) con el mismo nombre en `/etc/modules-load.d/`.

Entre los [módulos del kernel](/index.php/Kernel_modules_(Espa%C3%B1ol) "Kernel modules (Español)") de VirtualBo que puede utilizar, hay uno obligatorio llamado `vboxdrv`, que se debe cargar antes de que se pueda ejecutar cualquier máquina virtual.

Para cargar el módulo manualmente, ejecute:

```
# modprobe vboxdrv

```

Los siguientes módulos son opcionales, pero se recomiendan si no quiere que le den problebms con algunas configuraciones avanzadas (que son los que siguen): `vboxnetadp`, `vboxnetflt` y `vboxpci`.

*   `vboxnetadp` y `vboxnetflt` son necesarios cuando intenta usar la característica de [bridged](https://www.virtualbox.org/manual/ch06.html#network_bridged) o [conexión de red solo para el sistema anfitrión](https://www.virtualbox.org/manual/ch06.html#network_hostonly). Más precisamente, se necesita `vboxnetadp` para crear la interfaz del sistema anfitrión en las preferencias globales de VirtualBox, y `vboxnetflt` para iniciar una máquina virtual usando esa interfaz de red.

*   `vboxpci` es necesario cuando su máquina virtual necesita pasar a través de un dispositivo PCI del sistema anfitrión.

**Nota:** si los módulos del kernel de VirtualBox se cargaron en el kernel mientras actualizaba los módulos, debe volver a cargarlos manualmente para usar la nueva versión actualizada. Para hacerlo, ejecute `vboxreload` como root.

### Acceder al dispositivos USB del anfitrión desde el huésped

Para usar los puertos USB del equipo anfitrión en sus máquinas virtuales, agregue usuarios que estén autorizados para usar esta función a `vboxusers` del [grupo de usuarios](/index.php/User_group "User group").

### Disco de «Guest Additions»

También se recomienda instalar el paquete [virtualbox-guest-iso](https://www.archlinux.org/packages/?name=virtualbox-guest-iso) en el equipo que ejecuta VirtualBox. Este paquete actuará como una imagen de disco que se puede usar para instalar los complementos («*guest additions*») en sistemas huéspedes que no sean Arch Linux. El archivo *.iso* se ubicará en `/usr/lib/virtualbox/additions/VBoxGuestAdditions.iso`, y puede que tenga que ser montado manualmente dentro de la máquina virtual. Una vez montadao puede ejecutar el instalador de complementos adicionales dentro del huésped.

### Paquete de extensiones

El paquete *Oracle Extension* proporciona [additional features](https://www.virtualbox.org/manual/ch01.html#intro-installing) características adicionales] y se lanza bajo una licencia no gratuita **solo disponible para uso personal** . Para instalarlo, está disponible el paquete [virtualbox-ext-oracle](https://aur.archlinux.org/packages/virtualbox-ext-oracle/), y se puede encontrar una versión precompilada en el repositorio [seblu](/index.php/Unofficial_user_repositories#seblu "Unofficial user repositories").

Si prefiere usar la forma tradicional y manual: descargue la extensión manualmente e instálela a través de la interfaz gráfica (*Archivo > Preferencias > Extensiones*) o a través de `VBoxManage extpack install <.vbox-extpack>`, asegúrese de tener un conjunto de herramientas como [Polkit](/index.php/Polkit "Polkit") para otorgar acceso privilegiado a VirtualBox. La instalación de esta extensión [requiere acceso de root](https://www.virtualbox.org/ticket/8473).

### Utilizar el front-end adecuado

VirtualBox viene con tres [front-ends](https://en.wikipedia.org/wiki/es:Front-end_y_back-end "wikipedia:es:Front-end y back-end"):

*   Si desea usar VirtualBox con la interfaz gráfica normal, use `VirtualBox`.
*   Si desea iniciar y administrar sus máquinas virtuales desde la línea de órdenes, use la orden `VBoxSDL`,que solo proporciona una ventana simple para la máquina virtual sin superposiciones.
*   Si desea usar VirtualBox sin ejecutar ninguna interfaz gráfica (por ejemplo, en un servidor), use la orden `VBoxHeadless`. Con la extensión VRDP, aún puede acceder de forma remota a las pantallas de sus máquinas virtuales.

Por último, puede utilizar [PhpVirtualBox](/index.php/PhpVirtualBox "PhpVirtualBox") para administrar sus máquinas virtuales a través de una interfaz web.

Remítase al [manual de VirtualBox](https://www.virtualbox.org/manual) para aprender cómo crear máquinas virtuales.

**Advertencia:** si va a guardar imágenes de discos virtuales en un sistema de archivos [Btrfs](/index.php/Btrfs "Btrfs"), antes de crear cualquier imagen, debería considerar desactivar [Copy-on-Write](/index.php/Btrfs#Copy-on-Write_.28CoW.29 "Btrfs") para el directorio de destino de estas imágenes.

## Pasos para instalar Arch Linux como sistema huésped

Inicie el soporte de instalación de Arch a través de una de las unidades virtuales de la máquina virtual. Luego, complete la instalación de un sistema Arch básico como se explica en la [Installation guide (Español)](/index.php/Installation_guide_(Espa%C3%B1ol) "Installation guide (Español)").

#### Instalación en modo EFI

Si desea instalar Arch Linux en modo EFI en VirtualBox, en la configuración de la máquina virtual, choose *System* item from the panel on the left and *Motherboard* tab from the right panel, y marque la casilla *Enable EFI (special OSes only)*. Después seleccione el kernel desde el menú del soporte de instalación de Arch Linux, el soporte demorará por un minuto o dos y continuará con el arranque del kernel normalmente después. Sea paciente.

Una vez que el sistema y el cargador de arranque estén instalados, VirtualBox intentará ejecutar primero `/EFI/BOOT/BOOTX64.EFI` desde la partición [EFI system partition (Español)](/index.php/EFI_system_partition_(Espa%C3%B1ol) "EFI system partition (Español)"). Si esa primera opción falla, VirtualBox probará el script del intérprete de órdenes de EFI `startup.nsh` desde la raíz de la ESP. Esto significa que para iniciar el sistema tiene las siguientes opciones:

*   [Inicie el cargador de arranque manualmente](/index.php/Unified_Extensible_Firmware_Interface_(Espa%C3%B1ol)#Lanzar_el_int.C3.A9rprete_de_.C3.B3rdenes_UEFI "Unified Extensible Firmware Interface (Español)") desde el intérprete de órdenes de EFI cada vez;
*   Mueva el gestor de arranque a la ruta predeterminada `/EFI/BOOT/BOOTX64.EFI`;
*   Crea un script que se llame `startup.nsh` en la raíz de la partición ESP que contenga la ruta a la aplicación del cargador de arranque, por ejemplo `\EFI\grub\grubx64.efi`.
*   Arranque directamente desde la partición ESP usando un [script startup.nsh](/index.php/EFISTUB#Using_a_startup.nsh_script "EFISTUB").

No se moleste con el «*VirtualBox Boot Manager*» (accesible con `F2` en el inicio), ya que está defectuoso e incompleto. No almacena efivars establecidos de forma interactiva. Por lo tanto, las entradas EFI agregadas manualmente en el firmware (a las que se accede con `F12` en el momento del inicio) o con [efibootmgr](https://www.archlinux.org/packages/?name=efibootmgr) persistirán después de un reinicio [pero se pierden cuando la máquina virtual se apaga](https://www.virtualbox.org/ticket/11177).

Véase también [Problemas de arranque de la instalación de UEFI VirtualBox](https://bbs.archlinux.org/viewtopic.php?id=158003).

### Instalar los «Guest Additions»

Los [Guest Additions](https://www.virtualbox.org/manual/ch04.html) de VirtualBox proporcionan controladores y aplicaciones que optimizan el sistema operativo huésped, incluida una resolución de imagen mejorada y un mejor control del ratón. Dentro del sistema huésped instalado, instale:

*   [virtualbox-guest-utils](https://www.archlinux.org/packages/?name=virtualbox-guest-utils) para las utilidades de VirtualBox Guest con soporte para X;
*   [virtualbox-guest-utils-nox](https://www.archlinux.org/packages/?name=virtualbox-guest-utils-nox) para las utilidades de VirtualBox Guest sin soporte de X.

Ambos paquetes le darán a elegir un paquete para proporcionar módulos al huésped:

*   para el kernel [linux](https://www.archlinux.org/packages/?name=linux) predeterminado elija [virtualbox-guest-modules-arch](https://www.archlinux.org/packages/?name=virtualbox-guest-modules-arch);
*   para [kernels](/index.php/Kernels "Kernels") no predeterminados elija [virtualbox-guest-dkms](https://www.archlinux.org/packages/?name=virtualbox-guest-dkms).

Para compilar los módulos de virtualbox proporcionados por [virtualbox-guest-dkms](https://www.archlinux.org/packages/?name=virtualbox-guest-dkms), también será necesario instalar los paquetes de encabezados adecuados para su kernel instalado (por ejemplo, [linux-lts-headers](https://www.archlinux.org/packages/?name=linux-lts-headers) para [linux-lts](https://www.archlinux.org/packages/?name=linux-lts)). [[2]](https://lists.archlinux.org/pipermail/arch-dev-public/2016-March/027808.html) Cuando se actualice VirtualBox o el kernel, los módulos del kernel se volverán a compilar automáticamente gracias al hook [[DKMS] ] de Pacman.

**Nota:**

*   Alternativamente, puede instalar los «*Guest Additions*» con la ISO del paquete [virtualbox-guest-iso](https://www.archlinux.org/packages/?name=virtualbox-guest-iso), siempre que lo haya instalado en el sistema anfitrión. Para ello, vaya al menú del dispositivo y haga clic en Insertar imagen del CD de «*Guest Additions*».
*   Para recompilar los módulos del kernel de vbox, ejecuten `rcvboxdrv` como root.

Los complementos adicionales para el sistema huésped («*guest additions*») que se ejecutan en su sistema huésped y la aplicación VirtualBox que se ejecuta en su sistema anfitrión deben tener versiones coincidentes, de lo contrario los complementos adicionales (como el portapapeles compartido) pueden dejar de funcionar. Si actualiza su sistema huésped (por ejemplo, `pacman -Syu`), asegúrese de que su aplicación VirtualBox presente en el sistema anfitrión también sea la última versión. «Check for updates» en la interfaz gráfica de VirtualBox a veces no es suficiente; visite el sitio web [VirtualBox.org](https://www.virtualbox.org/).

### Establecer la resolución óptima de framebuffer

Normalmente, después de instalar Guest Additions, un huésped de Arch en pantalla completa que ejecuta X se configurará en la resolución óptima para su pantalla; sin embargo, el framebuffer de la consola virtual se configurará en una resolución estándar, a menudo más pequeña, detectada desde el controlador VESA personalizado de VirtualBox.

Para usar las consolas virtuales con una resolución óptima, Arch debe reconocer que la resolución es válida, lo que a su vez requiere que VirtualBox pase esta información al sistema operativo huésped.

Primero, verifique si su resolución deseada no está ya reconocida al ejecutar la orden:

```
hwinfo --framebuffer

```

Si la resolución óptima no se muestra, entonces deberá ejecutar la herramienta `VBoxManage` en el equipo anfitrión y agregue «resoluciones extras» a su máquina virtual (en un sistema anfitrión de Windows, vaya al directorio de instalación de VirtualBox para encontrar `VBoxManage.exe`). Por ejemplo:

```
$ VBoxManage setextradata "Arch Linux" "CustomVideoMode1" "1360x768x24"

```

Los parámetros "Arch Linux" y "1360x768x24" en el ejemplo anterior deben reemplazarse con el nombre de su máquina virtual y la resolución de framebuffer deseada. Por cierto, esta orden permite definir hasta 16 resoluciones adicionales ("CustomVideoMode1" hasta "CustomVideoMode16").

Luego, reinicie la máquina virtual y ejecute `hwinfo --framebuffer` una vez más para verificar que el sistema huésped ha reconocido las nuevas resoluciones (lo que no garantiza que funcionen, lo que dependerá de las limitaciones del hardware).

**Nota:** a partir de VirtualBox 5.2, `hwinfo --framebuffer` puede que no muestre ningún resultado, pero aún así debería poder establecer una resolución personalizada siguiendo este procedimiento.

Finalmente, agregue un [parámetro del kernel](/index.php/Kernel_parameters_(Espa%C3%B1ol) "Kernel parameters (Español)") `video=*resolution*` para configurar el framebuffer a la nueva resolución, por ejemplo::

```
video=1360x768

```

Además, es posible que desee configurar su [Arch boot process (Español)#Gestor de arranque](/index.php/Arch_boot_process_(Espa%C3%B1ol)#Gestor_de_arranque "Arch boot process (Español)") para usar la misma resolución. Si usa GRUB, consul [GRUB/Tips and tricks (Español)#Setting the framebuffer resolution](/index.php/GRUB/Tips_and_tricks_(Espa%C3%B1ol)#Setting_the_framebuffer_resolution "GRUB/Tips and tricks (Español)").

**Nota:** ni el parámetro del kernel `vga` ni la configuración de resolución del cargador de arranque (por ejemplo, `GRUB_GFXPAYLOAD_LINUX`) de GRUB, pueden arreglar el framebuffer, ya que están superados por la configuración de modo del kernel. La resolución del framebuffer debe ser establecida por el parámetro del kernel `video` como se describió anteriormente.

### Cargar los módulos del kernel de VirtualBox

Para cargar los módulos automáticamente, [active](/index.php/Enable "Enable") `vboxservice.service` que carga los módulos y sincroniza la hora del sistema del sistema huésped con el sistema anfitrión.

Para cargar los módulos manualmente, escriba:

```
# modprobe -a vboxguest vboxsf vboxvideo

```

[virtualbox-guest-dkms](https://www.archlinux.org/packages/?name=virtualbox-guest-dkms) utiliza `systemd-modules-load.service` para cargar los módulos en el momento del arranque.

**Nota:** si no desea que los módulos de VirtualBox se carguen en el momento del arranque, debe [enmascarar](/index.php/Mask "Mask") el archivo predeterminado `/usr/lib/modules-load.d/virtualbox-guest-dkms.conf` creando un archivo vacío (o enlace simbólico a `/dev/null`) con el mismo nombre en `/etc/modules-load.d/`.

### Lanzar los servicios de VirtualBox en el sistema huésped

Después de instalar los módulos del kernel, ahora se necesita iniciar los servicios en el sistema huésped. Los servicios de los huéspedes son en realidad un ejecutable binario llamado `VBoxClient` que interactuará con el sistema de ventanas X (X11) y que gestionará las siguientes funciones:

*   portapapeles compartido y función arrastrar y soltar entre el anfitrión y el huésped;
*   modo de ventanas integradas;
*   la pantalla del huésped se redimensiona automáticamente en función del tamaño de la ventana del sistema huésped;
*   y, finalmente, la comprobación de la versión del anfitrión de VirtualBox.

Todas estas características se pueden activar, separada y manualmente, con sus estiquetas dedicadas.

```
$ VBoxClient --clipboard --draganddrop --seamless --display --checkhostversion

```

Como método abreviado, el script de bash `VBoxClient-all` activa todas estas características.

[virtualbox-guest-utils](https://www.archlinux.org/packages/?name=virtualbox-guest-utils) instala `/etc/xdg/autostart/vboxclient.desktop` que lanza `VBoxClient-all` al iniciar sesión. Si su [entorno de escritorio](/index.php/Desktop_environment_(Espa%C3%B1ol) "Desktop environment (Español)") o [gestor de ventanas](/index.php/Window_manager_(Espa%C3%B1ol) "Window manager (Español)") no es compatible con [XDG Autostart](/index.php/XDG_Autostart "XDG Autostart"), deberá configurar el inicio automático usted mismo, consulte [Autostarting#On desktop environment startup](/index.php/Autostarting#On_desktop_environment_startup "Autostarting") y [Autostarting#On window manager startup](/index.php/Autostarting#On_window_manager_startup "Autostarting") para más detalles.

VirtualBox también puede sincronizar el tiempo entre el sistema anfitrión y el sistema huésped, para hacer esto,[inicie/active](/index.php/Start/enable "Start/enable") el servicio `vboxservice.service`.

Ahora, debería tener un sistema huésped de Arch Linux funcional. Tenga en cuenta que características como el uso compartido del portapapeles están desactivadas de manera predeterminada en VirtualBox, y tendrá que activarlas en la configuración para la máquina virtual si realmente quiere usarlas (por ejemplo, *Configuración > General > Avanzado > Portapapeles compartido*).

### Aceleracion de hardware

La aceleración de hardware se puede activar en las opciones de VirtualBox. Se sabe que el gestor de pantallas [GDMrompe](/index.php/GDM "GDM") el soporte de aceleración de hardware. [[3]](https://bugzilla.gnome.org/show_bug.cgi?id=749390) Si es el caso, y tiene problemas con la aceleración de hardware, pruebe con otro gestor de pantallas (lightdm parece funcionar bien). [[4]](https://bbs.archlinux.org/viewtopic.php?id=200025) [[5]](https://bbs.archlinux.org/viewtopic.php?pid=1607593#p1607593)

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
# mount -t vboxsf -o uid=1000,gid=1000 home /mnt

```

Donde *uid* y *gid* son los valores correspondientes a los usuarios que queremos dar acceso. Estos valores se obtienen de la orden `id` ejecutada respecto a dichos usuarios.

#### Montaje automático

**Nota:** El montaje automático requiere que el servicio `vboxservice.service` esté [activado](/index.php/Enabled "Enabled")/[iniciado](/index.php/Started "Started").

Para que la función de montaje automático funcione debe haber marcado la casilla de montaje automático en la interfaz gráica o usado la opción `--automount` en la orden `VBoxManage sharedfolder`.

La carpeta compartida debe aparecer ahora en `/media/sf_*shared_folder_name*`. If users in `media` cannot access the shared folders, check that `media` has permissions `755` or has group ownership `vboxsf` if using permission `750`. This is currently not the default if media is created by installing [virtualbox-guest-utils](https://www.archlinux.org/packages/?name=virtualbox-guest-utils).

Puede usar enlaces simbólicos si quiere tener un acceso más cómodo a dicha carpeta y ahorrarse tener que navegar hasta ese directorio, por ejemplo:

```
$ ln -s /media/sf_*shared_folder_name* ~/*my_documents*

```

#### Montaje durante el arranque

Puede montar su directorio con [fstab (Español)](/index.php/Fstab_(Espa%C3%B1ol) "Fstab (Español)"). Sin embargo, para evitar problemas de inicio con systemd, debe añadir `comment=systemd.automount` a `/etc/fstab`. De esta manera, las carpetas compartidas serán montadas bajo demanda, solo cuando se acceda a los puntos de montaje y no durante el inicio. Esto puede evitar algunos problemas, especialmente si las aplicaciones del sistema huésped no están aún cargadas mientras systemd lee fstab y monta las particiones.

```
*sharedFolderName*  */path/to/mntPtOnGuestMachine*  vboxsf  uid=*user*,gid=*group*,rw,dmode=700,fmode=600,noauto,x-systemd.automount

```

*   `*sharedFolderName*`: el valor del menú para la máquina virtual *Settings > SharedFolders > Edit > FolderName*. Este valor puede ser diferente del nombre de la carpeta real en equipo anfitrión. Para ver la *Configuración* para la máquina virtual vaya a la aplicación de VirtualBox del sistema operativo del sistema anfitrión, seleccione la máquina virtual correspondiente y haga clic en *Settings*.
*   `*/path/to/mntPtOnGuestMachine*`: si no existe, este directorio debe crearse manualmente (por ejemplo, utilizando [mkdir](/index.php/Core_utilities#Essentials "Core utilities")).
*   `dmode`/`fmode` son permisos de directorio/archivo para directorios/archivos dentro de `*/path/to/mntPtOnGuestMachine*`.

A partir de 2012-08-02, mount.vboxsf no admite la opción *nofail*:

```
desktop   /media/desktop    vboxsf  uid=user,gid=group,rw,dmode=700,fmode=600,nofail 0 0

```

### SSH de anfitrión a huésped

La pestaña network e la configuración de la máquina virtual contiene, en *Avanzado*, una herramienta para crear el reenvío de puertos. Es posible usarlo para reenviar el puerto ssh del sistema huésped `22` a un puerto del sistema anfitrión, por ejemplo `3022`:

```
user@host$ ssh -p 3022 $USER@localhost

```

establecerá una conexión del sistema anfitrión al sistema huésped.

#### SSHFS como alternativa a la carpeta compartida

Al usar este reenvío de puertos y sshfs, es sencillo montar el sistema de archivos del sistema huésped en el sistema anfitrión:

```
user@host$ sshfs -p 3022 $USER@localhost:$HOME ~/shared_folder

```

y luego transferir archivos entre ambos.

## Gestionar discos virtuales

Véase también [VirtualBox/Tips and tricks (Español)#Importar/exportar máquinas virtuales de VirtualBox a/desde otros hipervisores](/index.php/VirtualBox/Tips_and_tricks_(Espa%C3%B1ol)#Importar.2Fexportar_m.C3.A1quinas_virtuales_de_VirtualBox_a.2Fdesde_otros_hipervisores "VirtualBox/Tips and tricks (Español)").

### Formatos soportados por VirtualBox

VirtualBox es compatible con los siguientes formatos de disco virtual:

*   **VDI**: la «*Virtual Disk Image*» es el propio contenedor abierto de VirtualBox utilizado por defecto al crear una máquina virtual con VirtualBox.

*   **VMDK**: el «*Virtual Machine Disk*» fue desarrollado inicialmente por VMware para sus productos. La especificación fue inicialmente de código cerrado, pero ahora se ha convertido en un formato abierto que está totalmente respaldado por VirtualBox. Este formato ofrece la posibilidad de dividirse en varios archivos de 2 GB. Esta característica es especialmente útil si desea almacenar la máquina virtual en máquinas que no soportan archivos muy grandes. Otros formatos, excluyendo el formato HDD de Parallels, no proporcionan una característica equivalente.

*   **VHD**: el «*Virtual Hard Disk*» es el formato utilizado por Microsoft en Windows Virtual PC y Hyper-V. Si tiene intención de utilizar cualquiera de estos productos de Microsoft, tendrá que elegir este formato.

**Sugerencia:** desde Windows 7, este formato se puede montar directamente sin ninguna aplicación adicional.

*   **VHDX** (solo lectura): esta es la *versión extendida* del formato de «*Virtual Hard Disk*» desarrollada por Microsoft, que ha sido liberado el 2012-09-04 con Hyper-V 3.0 que viene con Windows Server 2012\. Esta nueva versión del formato de disco no ofrece un rendimiento mejorado (mejora, eso sí, la alineación de bloques), permite mayor tamaño de los bloques, y da soporte a journal que aporta resiliencia a los fallos de energía. VirtualBox [soporta este formato en solo lectura](https://www.virtualbox.org/manual/ch15.html#idp63002176).

*   **HDD** (versión 2): el formato HDD es desarrollado por Parallels Inc y utilizado en sus soluciones de hipervisor como Parallels Desktop para Mac. Las nuevas versiones de este formato (es decir, 3 y 4) no son compatibles debido a la falta de documentación de este formato propietario.
    **Nota:** en la actualidad existe una controversia con respecto al soporte de la versión 2 del formato. Si bien el manual oficial de VirtualBox [informa que solo la segunda versión del formato de archivo HDD está soportado](https://www.virtualbox.org/manual/ch05.html#vdidetails), los colaboradores de Wikipedia [informan que la primera versión puede funcionar también](https://en.wikipedia.org/wiki/Comparison_of_platform_virtual_machines#Image_type_compatibility "wikipedia:Comparison of platform virtual machines"). Si es posible realizar algunas pruebas con la primera versión del formato HDD, la ayuda será bienvenida.

*   **QED**: el formato «*QUEMU Enhanced Disk*» es un formato de archivo antiguo de QEMU, otro hipervisor de código libre y abierto. Este formato fue diseñado a partir de 2010 como una forma de ofrecer una alternativa superior a qcow2 y otros. Este formato cuenta con una trayectoria de E/S totalmente asíncrona, integridad de datos solida, respaldo de archivos y archivos dispersos. El formato QED solo se admite para la compatibilidad con máquinas virtuales creadas con versiones antiguas de QEMU.

*   **QCOW**: el formato «*QEMU Copy On Write*» es el formato actual de QEMU. El formato qcow soporta compresión transparente basada en zlib y cifrado (este último tiene defectos y no es recomendable). Qcow está disponible en dos versiones: QCOW y QCOW2\. El último tiende a reemplazar al primero. QCOW es [en la actualidad plenamente soportado por VirtualBox](https://www.virtualbox.org/manual/ch15.html#idp63002176). QCOW2 viene en dos revisiones: QCOW2 0.10 y QCOW2 1.1 (que es el valor por defecto cuando se crea un disco virtual con QEMU). VirtualBox no soporta este formato qcow2 (ambas revisiones se han probado).

*   **OVF**: El «*Open Virtualization Format*» es un formato abierto que ha sido diseñado para la interoperabilidad y la distribución de las máquinas virtuales entre diferentes hipervisores. VirtualBox es compatible con todas las revisiones de este formato a través de la [característica importar/exportar de VBoxManage](https://www.virtualbox.org/manual/ch08.html#idp55423424) pero con [limitaciones conocidas](https://www.virtualbox.org/manual/ch14.html#KnownProblems).

*   **RAW**: este es el modo cuando el disco virtual se expone directamente al disco sin ser contenida en un contenedor específico de formato de archivo. VirtualBox soporta esta característica de varias maneras: la conversión de disco RAW [a un formato específico](https://www.virtualbox.org/manual/ch08.html#idp59139136), o por [clonación de un disco a RAW](https://www.virtualbox.org/manual/ch08.html#vboxmanage-clonevdi), o utilizando directamente un archivo VMDK [que apunte a un disco físico o a un simple archivo](https://www.virtualbox.org/manual/ch09.html#idp57804112).

### Conversión de formatos de imagen de disco

[VBoxManage clonehd](https://www.virtualbox.org/manual/ch08.html#vboxmanage-clonevdi) se puede usar para convertir entre VDI, VMDK, VHD y RAW.

```
$ VBoxManage clonehd *inputfile* *outputfile* --format *outputformat*

```

Por ejemplo para convertir VDI a VMDK:

```
$ VBoxManage clonehd *source.vdi* *destination.vmdk* --format VMDK

```

#### QCOW

VirtualBox no admite el formato de imagen de disco QCOW2 de [QEMU](/index.php/QEMU "QEMU"). Para usar una imagen de disco QCOW2 con VirtualBox, por lo tanto, debe convertirla, lo que puede hacerse con la orden `qemu-img` del paquete [qemu](https://www.archlinux.org/packages/?name=qemu). `qemu-img` puede convertir QCOW a / desde VDI, VMDK, VHDX, RAW y varios otros formatos (que puede ver ejecutando

```
$ qemu-img convert -O *output_fmt* *inputfile* *outputfile*

```

Por ejemplo, para convertir QCOW2 a VDI:

```
$ qemu-img convert -O vdi *source.qcow2* *destination.vdi*

```

**Sugerencia:** el parámetro `-p` se usa para obtener la progresión de la tarea de conversión.

Hay dos revisiones de QCOW2: 0.10 y 1.1\. Puede especificar la revisión para usar con `-o compat=*revision*`.

### Montar discos virtuales

#### VDI

El montaje de imágenes VDI solo funciona con imágenes de tamaño fijo (también conocidas como imágenes estáticas); las imágenes dinámicas (asignación dinámica de tamaño) no son fáciles de montar.

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

**Nota:** este script se debe ejecutar en un entorno de PowerShell con privilegios de administrador. De forma predeterminada, los scripts no se pueden ejecutar, por lo que tendrá que asegurarse que la política de ejecución esté, al menos, en `RemoteSigned` y no en `Restricted`. Esto se puede comprobar con `Get-ExecutionPolicy` y la política requerida se puede establecer con `Set-ExecutionPolicy RemoteSigned`.

Una vez que el espacio libre en el disco ha sido anulado, apague su máquina virtual.

La próxima vez que arranque su máquina virtual, es recomendable hacer una verificación del sistema de archivos.

*   En los sistemas basados en UNIX, puede usar `fsck` manualmente;

*   En los sistemas GNU / Linux, y por lo tanto en Arch Linux, puede forzar una comprobación de disco en el arranque [gracias a un parámetro de arranque del kernel](/index.php/Fsck#Forcing_the_check "Fsck");

*   En los sistemas Windows, puede utilizar:

*   o bien, `chkdsk *c:* /F` donde `*c:*` necesita ser reemplazado por cada disco que necesita ser analizado y corregir errores;
*   o, `FsckDskAll` [desde aquí](http://therightstuff.de/2009/02/14/ChkDskAll-ChkDsk-For-All-Drives.aspx), que es básicamente el mismo software que `chkdsk`, pero sin la necesidad de repetir la orden para todas las unidades;

Ahora, hay que quitar los ceros del archivo *.|vdi* con [VBoxManage modifyhd](https://www.virtualbox.org/manual/ch08.html#vboxmanage-modifyvdi):

```
$ VBoxManage modifyhd *your_disk.vdi* --compact

```

**Nota:** si su máquina virtual dispone de instantáneas, es necesario aplicar la orden anterior en cada archivo `.vdi` que tenga.

### Aumentar discos virtuales

#### Procedimiento general

Si se está quedando sin espacio, debido al pequeño tamaño del disco duro que ha seleccionado al crear la máquina virtual, la solución aconsejada por el manual de VirtualBox es utilizar [VBoxManage modifyhd](https://www.virtualbox.org/manual/ch08.html#vboxmanage-modifyvdi). Sin embargo, esta orden solo funciona para los discos VDI y VHD, y solo para las variantes asignadas dinámicamente. Si desea cambiar el tamaño de un disco virtual que también es un disco de tamaño fijo, siga este arreglo que funciona bien para una máquina virtual Windows o UNIX.

En primer lugar, crear un nuevo disco virtual junto al que quiere aumentar:

```
$ VBoxManage createhd -filename *new.vdi* --size *10000*

```

donde el tamaño es en MiB, en este ejemplo 10000MiB ~= 10GiB, y *new.vdi* es el nombre del nuevo disco duro que se creará.

**Nota:** por defecto, esta orden utiliza el *estándar* de la variante de formato de archivo (correspondiente a la asignación dinámica) y, por lo tanto, no va a utilizar la misma variante de formato de archivo que la del disco virtual de origen. Si su archivo *old.vdi* tiene un tamaño fijo y desea mantener esta variante, agregue el parámetro `--variant Fixed`.

A continuación, el viejo disco virtual necesita ser clonado para el nuevo, lo cual puede tomar algún tiempo:

```
$ VBoxManage clonehd *old.vdi* *new.vdi* --existing

```

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

**Nota:** en discos GPT, al aumentar el tamaño del disco dará como resultado una copia de respaldo en la cabecera de GPT, pero dicho respaldo no se verá reflejado al final del dispositivo. GParted le preguntará si desea solucionar este problema, haga clic en *Fix* en ambas ocasiones. En los discos MBR, no se tiene un problema como este, ya que esta tabla de particiones no cuenta con respaldo al final del disco.

Por último, anule el registro del disco virtual de VirtualBox y elimine el archivo:

```
$ VBoxManage closemedium disk *old.vdi*
$ rm *old.vdi*

```

#### Aumentar el tamaño de los discos VDI

Si su disco es VDI, ejecute:

```
$ VBoxManage modifyhd *your_virtual_disk.vdi* --resize *the_new_size*

```

Luego salte de nuevo al paso Gparted, para aumentar el tamaño de la partición en el disco virtual.

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

**Nota:** si no sabe el GUID de la unidad que desea agregar, puede utilizar el archivo `VBoxManage showhdinfo *file*`. Si ha utilizado previamente `VBoxManage clonehd` para copiar/convertir su disco virtual, esta orden debería haber emitido el GUID justo después de la copia/conversión completada. El uso de un GUID aleatorio no funciona, ya que cada [UUID se almacena en el interior de cada imagen de disco](http://www.virtualbox.org/manual/ch05.html#cloningvdis).

#### Transferencia entre el anfitrión de Linux y otro sistema operativo

La información sobre la ruta a los discos duros y las instantáneas se almacena entre las etiquetas `<HardDisks> .... </HardDisks>` en el archivo con la extensión *.vbox*. Puede editarlos manualmente o usar este script donde necesitará cambiar solo la ruta o usar los valores predeterminados, asumiendo que *.vbo* está en el mismo directorio con un disco duro virtual y la carpeta de instantáneas. Se imprimirá nueva configuración a la salida estándar.

```
#!/bin/bash
NewPath="${PWD}/"
Snapshots="Snapshots/"
Filename="$1"

 awk -v SetPath="$NewPath" -v SnapPath="$Snapshots" '{if(index($0,"<HardDisk uuid=") != 0){A=$3;split(A,B,"=");
L=B[2];
 gsub(/\"/,"",L);
  sub(/^.*\//,"",L);
  sub(/^.*\\/,"",L);
 if(index($3,"{") != 0){SnapS=SnapPath}else{SnapS=""};
  print $1" "$2" location="\"SetPath SnapS L"\" "$4" "$5}
else print $0}' "$Filename"
```

**Nota:**

*   Si va a preparar una máquina virtual para su uso en un sistema Windows como anfitrión, en el final de la ruta debe usar la barra invertida \ en lugar de /.
*   El script detecta las instantáneas buscando `{` en el nombre del archivo.
*   Para hacer que se ejecute en un nuevo equipo, deberá agregarlo primero al registro haciendo clic en **Máquina -> Agregar...** o usar las teclas de acceso rápido Ctrl+A y luego ir al archivo *.vbox* que contiene la configuración o utilizar la línea de órdenes `VBoxManage registervm *filename*.vbox`

### Clonar un disco virtual y asignarle un UUID nuevo

Los UUID son ampliamente utilizados por VirtualBox. Cada máquina virtual y cada disco virtual de una máquina virtual deben tener un UUID diferente. Cuando se lanza una máquina virtual en VirtualBox, este último hace un seguimiento de todos los UUID de la instancia de la máquina virtual. Consulte la [`VBoxManage list`](http://www.virtualbox.org/manual/ch08.html#vboxmanage-list) para listar los elementos registrados por VirtualBox.

Si ha clonado un disco virtual de forma manual copiando el archivo del disco virtual, tendrá que asignar un nuevo UUID a la unidad virtual clonada, si quiere utilizar el disco en la misma máquina virtual o, incluso, en otra (si esta ya ha sido abierta y, por lo tanto, registrada, con VirtualBox).

Puede utilizar esta orden para asignar un nuevo UUID a su disco virtual:

```
$ VBoxManage internalcommands sethduuid */path/to/disk.vdi*

```

**Sugerencia:** en el futuro, para evitar la copia del disco virtual y la asignación de un nuevo UUID a su archivo de forma manual, use `[VBoxManage clonehd](http://www.virtualbox.org/manual/ch08.html#vboxmanage-clonevdi)` en su lugar.

**Nota:** las órdenes anteriores soportan [todos los formatos de disco virtual admitidos por VirtualBox](#Formatos_soportados_por_VirtualBox).

## Consejos y trucos

Para una configuración avanzada, vea [VirtualBox/Tips and tricks (Español)](/index.php/VirtualBox/Tips_and_tricks_(Espa%C3%B1ol) "VirtualBox/Tips and tricks (Español)").

## Solución de problemas

### Teclado y ratón bloqueados en la máquina virtual

Esto significa que su máquina virtual ha capturado la entrada de su teclado y del ratón. Basta con pulsar la tecla `Ctrl` derecho y su entrada debería volver al control de su sistema anfitrión de nuevo.

Para controlar de forma transparente su máquina virtual con el ratón de modo que este pueda pasear entre esta y el equipo anfitrión sin tener que pulsar ninguna tecla y con una integración perfecta, instale las *guest additions* dentro del sistema huésped. Lea los pasos para [#Instalar complementos para el sistema huésped](#Instalar_complementos_para_el_sistema_hu.C3.A9sped) si su sistema huésped es Arch Linux, en otro caso, lea la ayuda oficial de VirtualBox.

### No hay opciones del sistema operativo de 64 bits para el cliente

Cuando inicia un cliente VM, y no hay opciones de 64 bits disponibles, asegúrese de que las capacidades de virtualización de su CPU (generalmente llamadas `VT-x`) estén activadas en el BIOS.

Si está utilizando un sistema Windows como anfitrión, es posible que deba desactivar Hyper-V, ya que evita que VirtualBox use VT-x. [[6]](https://www.virtualbox.org/ticket/12350)

### La interfaz gráfica de VirtualBox no coincide con el tema GTK

Vea [Uniform look for Qt and GTK applications](/index.php/Uniform_look_for_Qt_and_GTK_applications "Uniform look for Qt and GTK applications") para obtener información sobre la tematización de aplicaciones basadas en Qt como VirtualBox.

### No se pueden usar las teclas CTRL+ALT+Fn en la máquina virtual

Si su sistema operativo huésped es una distribución de GNU/Linux puede abrir una nueva shell TTY con `Ctrl+Alt+F2` o salir de su sesión X actual con `Ctrl+Alt+Retroceso`. No obstante, si escribe estos atajos de teclado sin ninguna adaptación, el sistema huésped no recibirá ninguna entrada y el anfitrión (si se trata de una distribución GNU/Linux, tampoco) no interpretando estas teclas de acceso directo. Para enviar `Ctrl+Alt+F2` al sistema huésped, por ejemplo, basta con pulsar *«Host Key»*, (normalmente la tecla `Ctrl`) y `F2` simultáneamente.

### El subsistema USB no funciona

Su usuario debe estar en el grupo `vboxusers`, necesario para instalar el [paquete de extensiones](#Paquete_de_extensiones) si desea apoyo de USB 2\. Entonces será capaz de activar USB 2 en la configuración de la máquina virtual y añadir uno o varios filtros para los dispositivos a los que desee acceder desde el sistema operativo huésped.

If `VBoxManage list usbhost` does not show any USB devices even if run as root, make sure that there is no old udev rules (from VirtualBox 4.x) in `/etc/udev/rules.d/`. VirtualBox 5.0 installs udev rules to `/usr/lib/udev/rules.d/`. You can use command like `pacman -Qo /usr/lib/udev/rules.d/60-vboxdrv.rules` to determine if the udev rule file is outdated.

A veces, en equipos con Linux antiguo, el subsistema USB no se detecta automáticamente lo que da el error `Could not load the Host USB Proxy service: VERR_NOT_FOUND` o la unidad USB no es visible en el equipo, [incluso cuando el usuario está en el grupo **vboxusers**](https://bbs.archlinux.org/viewtopic.php?id=121377). Este problema es debido al hecho de que VirtualBox cambió de *usbfs* a *sysfs* en la versión 3.0.8\. Si el sistema anfitrión no entiende este cambio, puede revertir el comportamiento definiendo la siguiente variable de entorno en cualquier archivo fuente de la shell (por ejemplo, su `~/.bashrc` si usa *bash*):

 `~/.bashrc`  `VBOX_USB=usbfs` 

A continuación, asegúrese de que el entorno ha sido informado de este cambio (reconectar usb, recargar el archivo fuente manualmente, iniciar una instancia de shell o reiniciar equipo de nuevo).

También asegúrese de que su usuario es miembro del grupo `storage`.

### El módem USB no funciona en el sistema anfitrión

Si tiene un módem USB que está siendo utilizado por el sistema operativo huésped, eliminar el sistema operativo huésped, puede hacer que el sistema anfitrión no pueda utilizar el módem. Matar y reiniciar `VBoxSVC` debería solucionar este problema.

### Acceder al puerto serie desde el sistema huésped

Verifique su permiso para el puerto serie:

 `$ ls -l /dev/ttyS*` 
```
crw-rw---- 1 root uucp 4, 64 Feb  3 09:12 /dev/ttyS0
crw-rw---- 1 root uucp 4, 65 Feb  3 09:12 /dev/ttyS1
crw-rw---- 1 root uucp 4, 66 Feb  3 09:12 /dev/ttyS2
crw-rw---- 1 root uucp 4, 67 Feb  3 09:12 /dev/ttyS3

```

Agregue el usuario `uucp` al [grupo de usuarios](/index.php/User_group_(Espa%C3%B1ol) "User group (Español)").

### El sistema huésped se congela después de iniciar Xorg

Los controladores defectuosos o ausentes pueden provocar que el sistema huésped se congele después de iniciar Xorg, consulte por ejemplo [[7]](https://bbs.archlinux.org/viewtopic.php?pid=1167838) y [[8]](https://bbs.archlinux.org/viewtopic.php?id=156079). Intente desactivar la aceleración 3D en *Configuración > Pantalla*, y compruebe que todos los controladores de [Xorg (Español)](/index.php/Xorg_(Espa%C3%B1ol) "Xorg (Español)") están instalados.

### El modo de pantalla completa muestra la pantalla en blanco

En algunos gestores de ventanas ([i3](/index.php/I3 "I3"), [awesome](/index.php/Awesome "Awesome")), VirtualBox tiene problemas con el modo de pantalla completa debido a la barra de superposición. Para solucionar este problema, desactive la opción «Mostrar en pantalla completa/Sin márgenes» en «Configuración de invitado> Interfaz de usuario > Barra de herramientas mini». Consulte el [informe de errores de los desarrolladores](https://www.virtualbox.org/ticket/14323) para obtener más información.

### El sistema anfitrión se congela en el inicio de la máquina virtual

Posibles causas/soluciones:

*   SMAP

Esta es una incompatibilidad conocida con los kernels activados para SMAP que afectan (en su mayoría) a los conjuntos de chips Intel Broadwell. Una solución a este problema es desactivar el soporte SMAP en el kernel agregando la opción `nosmap` a sus [parámetros del kernel](/index.php/Kernel_parameters_(Espa%C3%B1ol) "Kernel parameters (Español)").

*   Virtualización de hardware

Desactivar la virtualización de hardware (VT-x/AMD-V) puede resolver el problema.

*   Varios errores de Kernel
    *   Particiones montadas fuse (como ntfs) [[9]](https://bbs.archlinux.org/viewtopic.php?id=185841), [[10]](https://bugzilla.kernel.org/show_bug.cgi?id=82951#c12)

En general, estos problemas se observan después de actualizar VirtualBox o el kernel de Linux. La degradación a las versiones anteriores de ellos podría resolver el problema.

### El sistema huésped Linux tiene audio lento/distorsionado

El controlador de audio AC97 dentro del kernel de Linux de vez en cuando define los ajustes del reloj de forma equivocada cuando se ejecuta dentro de Virtual Box, lo que lleva a que el audio sea demasiado lento o demasiado rápido. Para solucionar este problema, cree un archivo en `/etc/modprobe.d` con la siguiente línea:

```
options snd-intel8x0 ac97_clock=48000

```

### El micrófono analógico no funciona

Si la entrada de audio de un micrófono analógico funciona correctamente en el sistema anfitrión, pero no parece que el sonido llegue al sistema huésped, a pesar de que el dispositivo de micrófono se detecta normalmente, instalando un [servidor de sonido](/index.php/Sound_system#Sound_servers "Sound system") como [PulseAudio (Español)](/index.php/PulseAudio_(Espa%C3%B1ol) "PulseAudio (Español)") en el sistema anfitrión puede solucionar el problema.

Si después de instalar [PulseAudio (Español)](/index.php/PulseAudio_(Espa%C3%B1ol) "PulseAudio (Español)") el micrófono aún se niega a funcionar, la configuración de *Host Audio Driver* (en *VirtualBox > Machine > Settings > Audio*) para *ALSA Audio Driver* podría ayudar.

### El micrófono no funciona después de la actualización

Ha habido problemas informados sobre la entrada de sonido en las versiones 5.1.x [[11]](https://forums.virtualbox.org/viewtopic.php?f=7&t=78797)

[Degradar](/index.php/Downgrading "Downgrading") la versión puede resolver el problema. Puede usar [virtualbox-bin-5.0](https://aur.archlinux.org/packages/virtualbox-bin-5.0/) para facilitar la degradación.

### Problemas con imágenes convertidas a ISO

Algunos formatos de imagen no se pueden convertir de forma fiable a ISO. Por ejemplo, [ccd2iso](https://www.archlinux.org/packages/?name=ccd2iso) ignora los archivos .ccd y .sub, lo que puede resultar en imágenes de disco con archivos rotos.

En este caso, tendrá que usar [CDemu](/index.php/CDemu "CDemu") para Linux dentro de VirtualBox o cualquier otra utilidad utilizada para montar imágenes de disco.

### Error al crear la interfaz de red única del anfitrión

Asegúrese de que todos los módulos del kernel necesarios están cargados. Véase [#Cargar los módulos del kernel de VirtualBox](#Cargar_los_m.C3.B3dulos_del_kernel_de_VirtualBox).

### Error al insertar el módulo

Cuando obtiene el siguiente error al intentar cargar módulos:

```
Failed to insert 'vboxdrv': Required key not available

```

[Firme](#Sign_modules) los módulos o desactive `CONFIG_MODULE_SIG_FORCE` en la configuración de tu kernel.

### VBOX_E_INVALID_OBJECT_STATE (0x80BB0007)

Esto puede ocurrir si una máquina virtual se cierra de forma forzosa. Ejecute la siguiente orden:

```
$ VBoxManage controlvm *virtual_machine_name* poweroff

```

### «NS_ERROR_FAILURE» y ausencia de elementos del menú

Esto ocurre, a veces, cuando se selecciona el formato de disco *QCOW*/*QCOW2*/*QED* al crear un disco virtual nuevo.

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

### Arch: el script pacstrap falla

Si usó *pacstrap* en [#Pasos para instalar Arch Linux como sistema huésped](#Pasos_para_instalar_Arch_Linux_como_sistema_hu.C3.A9sped) también para [#Instalar los «Guest Additions»](#Instalar_los_.C2.ABGuest_Additions.C2.BB) **antes de** realizar un primer arranque en el nuevo sistema huésped, necesita `umount -l /mnt/dev` como root antes de usar *pacstrap* nuevamente; Si no lo hace, se volverá inutilizable.

### OpenBSD queda inutilizable cuando las instrucciones de virtualización no están disponibles

Aunque se informa que OpenBSD funciona bien en otros hipervisores sin instrucciones de virtualización (VT-x AMD-V) activadas, una máquina virtual OpenBSD que se ejecute en VirtualBox sin estas instrucciones será inutilizable, manifestándose con un montón de fallas de segmentación. Iniciar VirtualBox con el argumento *-noraw* [puede resolver el problema](https://www.virtualbox.org/ticket/3947). Puede hacerlo así:

```
$ VBoxSDL -norawr0 -vm *name_of_OpenBSD_VM*

```

### Anfitrión Windows: VERR_ACCESS_DENIED

Para acceder a la imagen VMDK en crudo en un sistema Windows que actúe de anfitrión, ejecute la interfaz gráfica de VirtualBox como administrador.

### Windows: «La ruta especificada no existe. Verifique la ruta y luego inténtelo nuevamente».

Este mensaje de error puede aparecer cuando se ejecuta un archivo `.exe` que requiere privilegios de administrador de una carpeta compartida en los sistemas huéspedes de Windows. [[12]](https://www.virtualbox.org/ticket/5732#comment:39)

Como solución alternativa, copie el archivo en la unidad virtual o use [Rutas UNC](https://en.wikipedia.org/wiki/es:Ruta_(inform%C3%A1tica)#Uniform_Naming_Convention (`\\vboxsvr`). Consulte [[13]](https://support.microsoft.com/de-de/help/2019185/copying-files-from-a-mapped-drive-to-a-local-directory-fails-with-erro) para obtener más información.

### Código de error 0x000000C4 de Windows 8.x

Si obtiene este código de error al iniciar, incluso si elige SO Type Win 8, pruebe activar la instrucción `CMPXCHG16B` de la CPU :

```
$ vboxmanage setextradata *virtual_machine_name* VBoxInternal/CPUM/CMPXCHG16B 1

```

### Windows 8, 8.1 o 10 no se instala, no se inicia o da el error «ERR_DISK_FULL»

Actualice la configuración de la máquina virtual navegando a *Settings > Storage > Controller:SATA* y marque «Use Host I/O Cache».

### WinXP: la profundidad de bits no puede ser mayor que 16

Si está ejecutando a una profundidad de color de 16 bits, entonces los iconos pueden aparecer borrosos / entrecortados. Sin embargo, al intentar cambiar la profundidad del color a un nivel superior, el sistema puede restringirlo a una resolución más baja o simplemente no permitirle cambiar la profundidad en absoluto. Para solucionar este problema, ejecute `regedit` en Windows y agregue la siguiente clave al registro de la máquina virtual de Windows XP:

```
[HKEY_LOCAL_MACHINE\SOFTWARE\Policies\Microsoft\Windows NT\Terminal Services]
"ColorDepth"=dword:00000004

```

Luego actualice la profundidad de color en la ventana «propiedades del escritorio». Si no sucede nada, fuerce la pantalla para redefinirse a través de algún método (esto es, `Host+f` para redefinir/ingresar a pantalla completa).

### Windows: la pantalla parpadea si la aceleración 3D está activada

VirtualBox > 4.3.14 tiene una regresión en la que los sistemas huéspedes de Windows parpadean si tienen activada la aceleración 3D. Desde r120678 se implementó un parche para reconocer una configuración de [variable de entorno](/index.php/Environment_variable_(Espa%C3%B1ol) "Environment variable (Español)"), inicie VirtualBox así:

```
$ CR_RENDER_FORCE_PRESENT_MAIN_THREAD=0 VirtualBox

```

Asegúrese de que no hay servicios de VirtualBox en ejecución. Consulte [VirtualBox bug 13653](https://www.virtualbox.org/ticket/13653).

### Sin aceleración 3D de hardware en Arch Linux huésped

El paquete [virtualbox-guest-utils](https://www.archlinux.org/packages/?name=virtualbox-guest-utils) a partir de la versión 5.2.16-2 no contiene el archivo `VBoxEGL.so`. Esto hace que el sistema huésped de Arch Linux no tenga la aceleración 3D adecuada. Vea [FS#49752](https://bugs.archlinux.org/task/49752).

Para resolver este problema, aplique el parche establecido en [FS#49752#comment152254](https://bugs.archlinux.org/task/49752#comment152254). Se requiere alguna solución al conjunto de parches para que funcione en la versión 5.2.16-2.

## Véase también

*   [VirtualBox User Manual](https://www.virtualbox.org/manual/UserManual.html)
*   [Wikipedia:VirtualBox](https://en.wikipedia.org/wiki/VirtualBox "wikipedia:VirtualBox")