Related articles

*   [Category:Hypervisors](/index.php/Category:Hypervisors "Category:Hypervisors")
*   [Libvirt](/index.php/Libvirt "Libvirt")

De acuerdo con [la wiki de QEMU](http://wiki.qemu.org/Main_Page), "QEMU es un emulador genérico y de código abierto de máquinas virtuales."

Cuando se utiliza como un emulador de máquina, QEMU pede correr sistemas operativos y programas hechos para una máquina en particular (por ej. una placa ARM) en una máquina diferente (e.j. tu PC x86). Usando la traducción dinámica, se consigue un rendimiento muy bueno.

QEMU puede usar hipervisores como [Xen](/index.php/Xen "Xen") o [KVM](/index.php/KVM "KVM") para utilizar las extensiones del procesador para la virtualización. Cuando se utiliza como virtualizador, QEMU alcanza un performance cercano a el rendimiento nativo ejecutando el código de invitado directamente en el CPU host.

## Contents

*   [1 Instalación](#Instalaci.C3.B3n)
*   [2 front-ends para QEMU](#front-ends_para_QEMU)
*   [3 Creando un nuevo sistema virtualizado](#Creando_un_nuevo_sistema_virtualizado)
    *   [3.1 Creando una imagen de disco duro](#Creando_una_imagen_de_disco_duro)
        *   [3.1.1 Superposición de imágenes de almacenamiento](#Superposici.C3.B3n_de_im.C3.A1genes_de_almacenamiento)
        *   [3.1.2 Cambiar el tamaño de una imagen](#Cambiar_el_tama.C3.B1o_de_una_imagen)
    *   [3.2 Preparando el medio de instalación](#Preparando_el_medio_de_instalaci.C3.B3n)
    *   [3.3 Instalando el sistema operativo](#Instalando_el_sistema_operativo)
*   [4 Ejecución del sistema virtualizado](#Ejecuci.C3.B3n_del_sistema_virtualizado)
    *   [4.1 Activar KVM](#Activar_KVM)
    *   [4.2 Habilitar soporte IOMMU (Intel VT-d/AMD-Vi)](#Habilitar_soporte_IOMMU_.28Intel_VT-d.2FAMD-Vi.29)
*   [5 Mover datos entre el host y el Sistema Operativo huésped](#Mover_datos_entre_el_host_y_el_Sistema_Operativo_hu.C3.A9sped)
    *   [5.1 Red](#Red)
    *   [5.2 Servidor SMB incorporado de QEMU](#Servidor_SMB_incorporado_de_QEMU)
    *   [5.3 Montaje de una partición dentro de una imagen de disco raw](#Montaje_de_una_partici.C3.B3n_dentro_de_una_imagen_de_disco_raw)
        *   [5.3.1 Con la especificación manual del desplazamiento de bytes](#Con_la_especificaci.C3.B3n_manual_del_desplazamiento_de_bytes)
        *   [5.3.2 Con las particiones autodetecting del módulo de bucle (loop)](#Con_las_particiones_autodetecting_del_m.C3.B3dulo_de_bucle_.28loop.29)
        *   [5.3.3 Con kpartx](#Con_kpartx)
    *   [5.4 Montar una partición dentro de una imagen qcow2](#Montar_una_partici.C3.B3n_dentro_de_una_imagen_qcow2)
    *   [5.5 Utilizar cualquier partición real como la única partición primaria de una imagen de disco duro](#Utilizar_cualquier_partici.C3.B3n_real_como_la_.C3.BAnica_partici.C3.B3n_primaria_de_una_imagen_de_disco_duro)
        *   [5.5.1 Especificar el kernel y el initrd manualmente](#Especificar_el_kernel_y_el_initrd_manualmente)
        *   [5.5.2 Simular disco virtual con MBR usando RAID lineal](#Simular_disco_virtual_con_MBR_usando_RAID_lineal)
*   [6 Redes](#Redes)
    *   [6.1 Advertencia de dirección a nivel de enlace](#Advertencia_de_direcci.C3.B3n_a_nivel_de_enlace)
    *   [6.2 Redes en modo de usuario](#Redes_en_modo_de_usuario)
    *   [6.3 Tap de red con QEMU](#Tap_de_red_con_QEMU)
        *   [6.3.1 Red de host solamente](#Red_de_host_solamente)
        *   [6.3.2 Red interna](#Red_interna)
        *   [6.3.3 Redes puenteadas usando qemu-bridge-helper](#Redes_puenteadas_usando_qemu-bridge-helper)
        *   [6.3.4 Creación manual del puente](#Creaci.C3.B3n_manual_del_puente)
        *   [6.3.5 Compartición de red entre dispositivo físico y un dispositivo de toque a través de iptables](#Compartici.C3.B3n_de_red_entre_dispositivo_f.C3.ADsico_y_un_dispositivo_de_toque_a_trav.C3.A9s_de_iptables)
    *   [6.4 Trabajo en red con VDE2](#Trabajo_en_red_con_VDE2)
        *   [6.4.1 ¿Qué es VDE?](#.C2.BFQu.C3.A9_es_VDE.3F)
        *   [6.4.2 Basics](#Basics)
        *   [6.4.3 Startup scripts](#Startup_scripts)
        *   [6.4.4 Método alternativo](#M.C3.A9todo_alternativo)
    *   [6.5 Puente VDE2](#Puente_VDE2)
        *   [6.5.1 Conceptos básicos](#Conceptos_b.C3.A1sicos)
        *   [6.5.2 Startup scripts](#Startup_scripts_2)
*   [7 Gráficos](#Gr.C3.A1ficos)
    *   [7.1 std](#std)
    *   [7.2 qxl](#qxl)
        *   [7.2.1 SPICE](#SPICE)
    *   [7.3 vmware](#vmware)
    *   [7.4 virtio](#virtio)
    *   [7.5 cirrus](#cirrus)
    *   [7.6 none](#none)
    *   [7.7 vnc](#vnc)
*   [8 Audio](#Audio)
    *   [8.1 Host](#Host)
    *   [8.2 Invitado](#Invitado)
*   [9 Instalación de controladores virtio](#Instalaci.C3.B3n_de_controladores_virtio)
    *   [9.1 Preparando a Arch Linux como invitado](#Preparando_a_Arch_Linux_como_invitado)
    *   [9.2 Preparar un invitado de Windows](#Preparar_un_invitado_de_Windows)
        *   [9.2.1 Bloquear controladores de dispositivo](#Bloquear_controladores_de_dispositivo)
            *   [9.2.1.1 Nueva instalación de Windows](#Nueva_instalaci.C3.B3n_de_Windows)
            *   [9.2.1.2 Cambiar la máquina virtual existente de Windows para utilizar virtio](#Cambiar_la_m.C3.A1quina_virtual_existente_de_Windows_para_utilizar_virtio)
        *   [9.2.2 Controladores de red](#Controladores_de_red)
    *   [9.3 Preparación de FreeBSD como invitado](#Preparaci.C3.B3n_de_FreeBSD_como_invitado)
*   [10 Consejos y trucos](#Consejos_y_trucos)
    *   [10.1 Inicio de las máquinas virtuales QEMU en el arranque](#Inicio_de_las_m.C3.A1quinas_virtuales_QEMU_en_el_arranque)
        *   [10.1.1 Con libvirt](#Con_libvirt)
        *   [10.1.2 Script personalizado](#Script_personalizado)
    *   [10.2 Integración del ratón](#Integraci.C3.B3n_del_rat.C3.B3n)
    *   [10.3 Dispositivo USB del host de paso](#Dispositivo_USB_del_host_de_paso)
    *   [10.4 Habilitar KSM](#Habilitar_KSM)
    *   [10.5 Multi-monitor support](#Multi-monitor_support)
    *   [10.6 Copiar y pegar](#Copiar_y_pegar)
    *   [10.7 Notas específicas de Windows](#Notas_espec.C3.ADficas_de_Windows)
        *   [10.7.1 Inicio rápido](#Inicio_r.C3.A1pido)
        *   [10.7.2 Protocolo de escritorio remoto](#Protocolo_de_escritorio_remoto)
*   [11 Solución de problemas](#Soluci.C3.B3n_de_problemas)
    *   [11.1 La máquina virtual virtual corre muy lento](#La_m.C3.A1quina_virtual_virtual_corre_muy_lento)
    *   [11.2 El cursor del ratón está nervioso o errático](#El_cursor_del_rat.C3.B3n_est.C3.A1_nervioso_o_err.C3.A1tico)
    *   [11.3 El cursor no es visible](#El_cursor_no_es_visible)
    *   [11.4 No se puede mover / adjuntar el cursor](#No_se_puede_mover_.2F_adjuntar_el_cursor)
    *   [11.5 El teclado parece roto ó las teclas de flecha no funcionan](#El_teclado_parece_roto_.C3.B3_las_teclas_de_flecha_no_funcionan)
    *   [11.6 Pantalla de invitado estirada en el tamaño de la ventana](#Pantalla_de_invitado_estirada_en_el_tama.C3.B1o_de_la_ventana)
    *   [11.7 ioctl(KVM_CREATE_VM) failed: 16 Device or resource busy](#ioctl.28KVM_CREATE_VM.29_failed:_16_Device_or_resource_busy)
    *   [11.8 Mensaje de error libgfapi](#Mensaje_de_error_libgfapi)
    *   [11.9 Kernel panic en entornos live](#Kernel_panic_en_entornos_live)
*   [12 Ver también](#Ver_tambi.C3.A9n)

## Instalación

Instala el paquete [qemu](https://www.archlinux.org/packages/?name=qemu) (ó [qemu-headless](https://www.archlinux.org/packages/?name=qemu-headless) para la versión sin GUI) y los paquetes opcionales para tus necesidades:

*   [qemu-arch-extra](https://www.archlinux.org/packages/?name=qemu-arch-extra) - Soporte extra para arquitecturas
*   [qemu-block-gluster](https://www.archlinux.org/packages/?name=qemu-block-gluster) - Soporte para bloque glusterfs
*   [qemu-block-iscsi](https://www.archlinux.org/packages/?name=qemu-block-iscsi) - Soporte para bloque iSCSI
*   [qemu-block-rbd](https://www.archlinux.org/packages/?name=qemu-block-rbd) - Soporte para bloque RBD
*   [samba](https://www.archlinux.org/packages/?name=samba) - SMB/ Soporte para servidor CIFS

## front-ends para QEMU

A diferencia de otros programas de virtualización como [VirtualBox](/index.php/VirtualBox "VirtualBox") y [VMware](/index.php/VMware "VMware"), QEMU no proporciona una interfaz gráfica de usuario para administrar máquinas virtuales (a parte de la ventana que aparece cuando se ejecuta una máquina virtual), tampoco proporciona una forma de crear una máquina virtual persistente con valores guardados. Todos los parámetros para ejecutar una máquina virtual deben especificarse en la línea de comandos en cada puesta en marcha, a menos que haga un script personalizadp para iniciar su máquina(s) virtual. Sin embargo, hay varios front-end GUI para QEMU:

*   [qemu-launcher](https://aur.archlinux.org/packages/qemu-launcher/)
*   [qtemu](https://aur.archlinux.org/packages/qtemu/)
*   [aqemu](https://aur.archlinux.org/packages/aqemu/)

front-ends con soporte para QEMU están disponibles por [libvirt](/index.php/Libvirt "Libvirt").

## Creando un nuevo sistema virtualizado

### Creando una imagen de disco duro

**Tip:** mira la wiki, [Wiki de QEMU](https://en.wikibooks.org/wiki/QEMU/Images) para más información sobre imagenes de QEMU.

Para ejecutar QMEU necesitarás una imagen de disco duro, a menos que estés cargando un sistema en vivo desde el CD-ROM ó la red (y no para instalar un sistema operativo en una imagen de disco duro). Una imagen de disco es un archivo que almacena los contenidos del disco duro emulado.

Una imagen de disco puede ser en "crudo", de manera que, literalemte, byte por byte es lo mismo que el cliente ve, y siempre utilizará toda la capacidad del disco duro del disco duro invitado en el host. Este método proporciona la menor sobrecarga de Entrada / Salida, pero puede desperdiciar una gran cantidad de espacio, ya que el espacio no utilizado por el invitado no se puede utilizar en el host.

Por otra parte, la imagen de disco duro puede estar en un formato tal como el de *qcow2* el cuál únicamente asigna espacio a el archivo de la imagen cuando el SO invitado está escribiendo en los sectores del disco virtual. La imagen aparece como el tamaño total del sistema operativo huésped, a pesar que puede tomar hasta una cantidad muy pequeña de espacio en el sistema host. El uso de este formato en lugar de el "crudo" probablemente afecte el rendimiento.

QEMU proporciona el `qemu-img` comando para crear imagenes de disco. Por ejemplo, para crear una imagen de 4GB en formato "crudo":

```
$ qemu-img create -f raw *image_file* 4G

```

Se puede uiltizar `-f qcow2` para crear un disco *qcow2* en su lugar.

También puedes simplemente crear una imagen "cruda" meidante la creación de un archivo del tamaño necesitado usando `dd` ó `fallocate`.}}

**Advertencia:** Si almacenas una imágen de disco en un sistema de archivos [Btrfs](/index.php/Btrfs "Btrfs"), deberías considerar deshabilitar [Copy-on-Write](/index.php/Btrfs#Copy-on-Write_.28CoW.29 "Btrfs") para el directorio antes de crear imágenes.

#### Superposición de imágenes de almacenamiento

Puede crear una imagen de almacenamiento una vez (la imagen de respaldo) y hacer que QEMU mantenga mutaciones a esta imagen en una imagen de superposición. Esto le permite volver a un estado anterior de esta imagen de almacenamiento. Puede volver a crear una nueva imagen de superposición en el momento en que desea revertir en función de la imagen de respaldo original.

Para crear una imagen de superposición, ingrese el comando:

 $ Qemu-img create -o backing_file = *img1.raw* , backing_fmt = *raw* -f *qcow2* *img1.cow*

Después de eso, puede ejecutar su máquina virtual como de costumbre (ver [#Ejecución del sistema virtualizado](#Ejecuci.C3.B3n_del_sistema_virtualizado)):

 $ Qemu-system-i386 *img1.cow*

La imagen de respaldo se dejará intacta y se registrarán mutaciones en este almacenamiento en el archivo de imagen de superposición.

Cuando cambia la ruta de acceso a la imagen de respaldo, se requiere reparación.

**Advertencia:** La ruta del sistema de archivos absoluto de la imagen de respaldo se almacena en el archivo de imagen de superposición (binario)). Cambiar el trayecto de la imagen de respaldo requiere un esfuerzo.

Asegúrese de que la ruta de la imagen de respaldo original sigue conduciendo a esta imagen. Si es necesario, haga un enlace simbólico en la ruta original a la nueva ruta. A continuación, emita un comando como:

 $ Qemu-img rebase -b */new/img1.raw* */new/img1.cow*

A su discreción, usted puede alternativamente realizar un rebase 'inseguro' donde no se comprueba la ruta anterior a la imagen de respaldo:

 $ Qemu-img rebase -u -b */new/img1.raw* */new/img1.cow*

#### Cambiar el tamaño de una imagen

**Advertencia:** Cambiar el tamaño de una imagen que contiene un sistema de arranque NTFS podría hacer el sistema operativo instalado **no arrancable**. Para una explicación completa y solucioón alternativa mira [[1]](http://tjworld.net/wiki/Howto/ResizeQemuDiskImages).

El ejecutable `qemu-img` tiene la opción `resize`, que permite redimensionar fácilmente una imagen de disco duro. Funciona tanto para *raw* como para *qcow2*. Por ejemplo, para aumentar el espacio de imagen en 10GB, ingresa:

```
$ qemu-img resize *disk_image* +10G

```

Después de ampliar la imagen de disco, debe utilizar el sistema de archivos y las herramientas de particionamiento dentro de la máquina virtual para comenzar a utilizar el nuevo espacio. Al reducir una imagen de disco, primero debe reducir los sistemas de archivos y los tamaños de partición asignados usando el sistema de archivos y las herramientas de partición dentro de la máquina virtual y luego reducir la imagen del disco en consecuencia, de lo contrario reducir la imagen del disco resultará en ¡pérdida de datos!

### Preparando el medio de instalación

Para instalar un sistema operativo en su imagen de disco, necesita el medio de instalación (por ejemplo, disco óptico, unidad USB o imagen ISO) para el sistema operativo. El soporte de instalación no debe montarse porque QEMU accede directamente al medio.

**Sugerencia:** Si utiliza un disco óptico, es una buena idea volcar primero los medios a un archivo porque esto mejora el rendimiento y no requiere que tenga acceso directo a los dispositivos (es decir, puede ejecutar QEMU como un usuario normal sin tener Para cambiar permisos de acceso en el archivo de dispositivo del medio). Por ejemplo, si el nodo de dispositivo de CD-ROM tiene el nombre `/dev/cdrom`, puede volcarlo a un archivo de comandos: `$ dd if=/dev/cdrom of=*Cd_image.iso*` 

### Instalando el sistema operativo

Esta es la primera vez que necesitará iniciar el emulador. Para instalar el sistema operativo en la imagen de disco, debe adjuntar la imagen de disco y el medio de instalación a la máquina virtual y hacer que arranque desde el soporte de instalación.

Por ejemplo, en invitados i386, para instalar desde un archivo ISO de arranque como CD-ROM y una imagen de disco sin formato:

 $ Qemu-system-i386 -cdrom *iso_image* - orden de arranque = d -drive file = *disk_image* , format = raw

Consulte `qemu (1)` para obtener más información sobre cómo cargar otros tipos de medios (como disquetes, imágenes de disco o unidades físicas) y [#Ejecución del sistema virtualizado](#Ejecuci.C3.B3n_del_sistema_virtualizado) para otras opciones útiles.

Una vez que el sistema operativo haya finalizado de instalar, la imagen de QEMU se puede iniciar directamente (ver [#Ejecución del sistema virtualizado](#Ejecuci.C3.B3n_del_sistema_virtualizado)).

**Advertencia:** De forma predeterminada, sólo se asignan 128 MB de memoria a la máquina. La cantidad de memoria se puede ajustar con el interruptor `-m`, por ejemplo `-m 512M` o `-m 2G`.

**Sugerencia:**

*   En lugar de especificar `-boot order = x`, algunos usuarios pueden sentirse más cómodos usando un menú de arranque: `-boot menu = on`, al menos durante la configuración y la experimentación.
*   Si necesita reemplazar disquetes o CD como parte del proceso de instalación, puede usar el monitor de la máquina QEMU (presione `Ctrl + Alt + 2` en la ventana de la máquina virtual) para quitar y conectar dispositivos de almacenamiento a un máquina virtual. Escriba `info block` para ver los dispositivos de bloque y use el comando `change` para intercambiar un dispositivo. Pulse `Ctrl + Alt + 1` para volver a la máquina virtual.

## Ejecución del sistema virtualizado

Los binarios `qemu-system-*` (por e.j. `qemu-system-i386` ó `qemu-system-x86_64`, dependiendo de la arquitectura del huésped) se usan para ejecutar el sistema virtualizado. El uso es:

```
$ qemu-system-i386 *options* *disk_image*

```

Las opciones son las mismas para todos los binarios `qemu-system-*`, mira `qemu(1)` para más información sobre todas las opciones.

Por defecto, QEMU mostrará la salida de video de la máquina virtual en una ventana. Una cosa a considerar: al hacer click dentro de la ventana de QMEU, el puntero del cursor será capturado. Para liberarlo presione `Ctrl+Alt+g`.

**Advertencia:** QEMU nunca debe ejecutarse como root. Si se debe iniciar en root, deberá usar la opción `-runas` para que QEMU utilice privilegios de root.

### Activar KVM

KVM debe ser soportado por su procesador y kernel, y necesariamente los [kernel modules](/index.php/Kernel_modules "Kernel modules") deben ser cargados. Mira [KVM](/index.php/KVM "KVM") para más información.

Para iniciar QEMU en modo KVM, adjunta `-enable-kvm` a las opciones de inicio adicionales. Para verificar si KVM está activado para ejecutar una máquina virtual, ingresa a la wiki de QEMU [Monitor](https://en.wikibooks.org/wiki/QEMU/Monitor), usando `Ctrl+Alt+Shift+2`, e ingresando `info kvm`.

**Nota:**

*   Si inicia su máquina virtual con una herramienta GUI y experimenta un rendimiento muy malo, debe verificar el soporte adecuado de KVM.
*   KVM necesita activarse en orden de iniciar adecuadamente Windows 7 y Windows 8 sin *pantallazo azul*.

### Habilitar soporte IOMMU (Intel VT-d/AMD-Vi)

Usando IOMMU (unidad de gestión de memoria de entrada y salida) se abre a las caraterísticas como el paso del PCI y la protección de la memoria de dispositivos defectuosos o maliciosos, mira [wikipedia:Input-output memory management unit#Advantages](https://en.wikipedia.org/wiki/Input-output_memory_management_unit#Advantages "wikipedia:Input-output memory management unit") y [Memory Management (computer programming): Could you explain IOMMU in plain English?](https://www.quora.com/Memory-Management-computer-programming/Could-you-explain-IOMMU-in-plain-English).

Para habilitar IOMMU:

1.  Asegure que AMD-Vi/Intel VT-d es soportado por el CPU y es habilitado en la configuración de BIOS.
2.  Agregue `intel_iommu=on` si tienes un procesador Intel ó `amd_iommu=on` si tienes un procesador AMD en los parámetros del kernel ([kernel parameters](/index.php/Kernel_parameters "Kernel parameters"))
3.  Reinicie y asegure que IOMMU está habilitado verificando `dmesg` para `DMAR`: `[0.000000] DMAR: IOMMU enabled`
4.  Añade `-device intel-iommu` para crear el dispositivo IOMMU:

```
$ qemu-system-i386 -enable-kvm -machine q35,accel=kvm -device intel-iommu ..

```

## Mover datos entre el host y el Sistema Operativo huésped

### Red

Los datos pueden compartirse entre el host y el sistema operativo huésped usando cualquier protocolo de red que pueda transferir archivos, como [NFS](/index.php/NFS "NFS"), [SMB](/index.php/SMB "SMB"), [NBD](https://en.wikipedia.org/wiki/Network_Block_Device "wikipedia:Network Block Device"), HTTP, [FTP](/index.php/Very_Secure_FTP_Daemon "Very Secure FTP Daemon"), ó [SSH](/index.php/SSH "SSH"), siempre que haya configurado la red apropiadamente y haya habilitado los servicios apropiados.

La red por defecto del modo de usuario permite al huésped acceder al sistema operativo host en la dirección IP 10.0.2.2\. Todos los servidores que se estén ejecutando en el sistema operativo anfitrión, como un servidor SSH o un servidor SMB, estarán accesibles en esta dirección IP. Así que en los invitados, puede montar los directorios exportados en el host a través de [SMB](/index.php/SMB "SMB") o [NFS](/index.php/NFS "NFS"), o puede acceder al servidor HTTP del host, etc. No será posible que el sistema operativo anfitrión acceda a los servidores que se ejecutan en el sistema operativo invitado, pero esto puede hacerse con otras configuraciones de red (consulte [#Tap de red con QEMU](#Tap_de_red_con_QEMU)).

### Servidor SMB incorporado de QEMU

La documentación de QEMU dice que tiene un servidor SMB "incorporado", pero en realidad acaba de iniciar [Samba](/index.php/Samba "Samba") con un archivo `smb.conf` generado automáticamente ubicado en `/tmp/qemu- Smb.*Pid*-0/smb.conf` y lo hace accesible para el invitado en una dirección IP diferente (10.0.2.4 por defecto). Esto sólo funciona para la red de usuarios, y esto no es necesariamente muy útil ya que el invitado también puede acceder al servicio normal [Samba](/index.php/Samba "Samba") en el host si ha configurado acciones en él.

Para habilitar esta característica, inicie QEMU con un comando como:

```
$ qemu-system-i386 *disk_image* -net nic -net user,smb=*shared_dir_path*

```

donde `*shared_dir_path*` es un directorio que quieres compartir entre huésped y el host.

Luego, en el invitado, podrá acceder al directorio compartido del host 10.0.2.4 con el nombre de recurso "qemu". Por ejemplo, en el Explorador de Windows iría a `\\ 10.0.2.4 \ qemu`.

**Nota:**

*   Si estás usando opciones de compartir varias veces como `-net user, smb= *shared_dir_path1* -net user, smb= *shared_dir_path2* `ó `-net user , Smb = *shared_dir_path1* , smb = *shared_dir_path2* `entonces solo compartirá el último definido.
*   Si no puede acceder a la carpeta compartida y el sistema invitado es Windows, compruebe que está habilitado el protocolo [NetBIOS](http://ecross.mvps.org/howto/enable-netbios-over-tcp-ip-with-windows.htm) Y que un cortafuegos no bloquea los puertos [[2]](http://technet.microsoft.com/en-us/library/cc940063.aspx) utilizados por el protocolo NetBIOS.

### Montaje de una partición dentro de una imagen de disco raw

Cuando la máquina virtual no se está ejecutando, es posible montar las particiones que están dentro de un archivo de imagen de disco sin formato configurándolas como dispositivos de bucle invertido. Esto no funciona con imágenes de disco en formatos especiales, como qcow2, aunque se pueden montar usando `qemu-nbd`.

**Advertencia:** Debe asegurarse de desmontar las particiones antes de ejecutar la máquina virtual de nuevo. De lo contrario, es muy probable que ocurra la corrupción de datos.

#### Con la especificación manual del desplazamiento de bytes

Una forma de montar una partición de imagen de disco es montar la imagen de disco en un cierto desplazamiento usando un comando como el siguiente:

```
$ mount -o loop, offset = 32256 *disk_image* *mountpoint*

```

La opción `offset = 32256` se pasa realmente al programa `losetup` para configurar un dispositivo de bucle invertido que empieza en el desplazamiento de byte 32256 del archivo y continúa hasta el final. A continuación, se monta este dispositivo de bucle invertido. También puede utilizar la opción `sizelimit` para especificar el tamaño exacto de la partición, pero esto normalmente no es necesario.

Dependiendo de la imagen del disco, la partición necesaria no se puede iniciar en el desplazamiento 32256\. Ejecute `fdisk -l *disk_image* `para ver las particiones de la imagen. Fdisk da las compensaciones de inicio y fin en sectores de 512 bytes, así que multiplique por 512 para obtener el desplazamiento correcto para pasar a `mount`.

#### Con las particiones autodetecting del módulo de bucle (loop)

El controlador de bucle de Linux realmente admite particiones en dispositivos de bucle invertido, pero está desactivado de forma predeterminada. Para habilitarlo, haga lo siguiente:

*   Deshacerse de todos los dispositivos de bucle invertido (desmontar todas las imágenes montadas, etc.).
*   [Unload](/index.php/Kernel_modules#_Manual_module_handling "Kernel modules") el módulo de kernel `loop` y cargarlo con el conjunto de parámetros `max_part = 15`. Además, el número máximo de dispositivos de bucle puede controlarse con el parámetro `max_loop`.

{{Sugerencia: puede poner una entrada en `/etc/modprobe.d` para cargar el módulo de bucle con `max_part=15` cada vez, o puede poner `loop.max_part = 15` en la línea de comandos del kernel, dependiendo de si tiene o no el módulo `loop.ko` integrado en su kernel.}}

Configure su imagen como un dispositivo de bucle invertido:

```
$ losetup -f -P *disk_image*

```

Entonces, si el dispositivo creado fue `/dev/loop0`, se habrán creado automáticamente dispositivos adicionales `/dev/loop0pX`, donde X es el número de la partición. Estos dispositivos de loopback de partición se pueden montar directamente. Por ejemplo:

```
$ mount /dev/loop0p1 *punto de montaje*

```

Para montar la imagen de disco con *udisksctl* , vea [Udisks#Mount loop devices](/index.php/Udisks#Mount_loop_devices "Udisks").

#### Con kpartx

*'Kpartx'* del paquete [multipath-tools](https://aur.archlinux.org/packages/multipath-tools/) puede leer una tabla de particiones en un dispositivo y crear un nuevo dispositivo para cada partición. Por ejemplo:  # Kpartx -a *disk_image*

Esto configurará el dispositivo de bucle invertido y creará los dispositivos de partición necesarios en `/dev/mapper/`.

### Montar una partición dentro de una imagen qcow2

Puede montar una partición dentro de una imagen qcow2 usando `qemu-nbd`. Mira [Wikibooks](http://en.wikibooks.org/wiki/QEMU/Images#Mounting_an_image_on_the_host).

### Utilizar cualquier partición real como la única partición primaria de una imagen de disco duro

A veces, puede que desee utilizar una de las particiones del sistema desde dentro de QEMU. El uso de una partición sin procesar para una máquina virtual mejorará el rendimiento, ya que las operaciones de lectura y escritura no pasan por la capa del sistema de archivos del host físico. Esta partición también proporciona una forma de compartir datos entre el host y el invitado.

En Arch Linux, los archivos de dispositivo para las particiones sin procesar son, por defecto, propiedad de *root* y del grupo *disk* . Si desea que un usuario no root pueda leer y escribir en una partición en bruto, debe cambiar el propietario del archivo de dispositivo de la partición para ese usuario.

**Advertencia:**

*   Aunque es posible, no se recomienda permitir que las máquinas virtuales alteren los datos críticos en el sistema host, como la partición raíz.
*   No debe montar un sistema de archivos en una partición de lectura-escritura en el host y el invitado al mismo tiempo. De lo contrario, se producirá corrupción de datos.

Después de hacerlo, puede adjuntar la partición a una máquina virtual QEMU como un disco virtual.

Sin embargo, las cosas son un poco más complicadas si desea tener la máquina virtual *completa* contenida en una partición. En ese caso, no habría ningún archivo de imagen de disco para arrancar realmente la máquina virtual, ya que no se puede instalar un cargador de arranque en una partición que está formateada como un sistema de archivos y no como un dispositivo particionado con un MBR. Una máquina virtual de este tipo se puede iniciar especificando el kernel y el initramfs manualmente o simulando un disco con un MBR usando RAID lineal.

#### Especificar el kernel y el initrd manualmente

QEMU es compatible con cargar [Linux kernels](/index.php/Kernels "Kernels") e [init ramdisks](/index.php/Initramfs "Initramfs") directamente, evitando así los cargadores de arranque como [GRUB](/index.php/GRUB "GRUB"). A continuación, se puede iniciar con la partición física que contiene el sistema de archivos raíz como el disco virtual, que no parecen ser particionados. Esto se hace emitiendo un comando similar al siguiente:

**Nota:** En este ejemplo, se trata de las imágenes del **host** que se están utilizando, no del invitado. Si desea utilizar las imágenes del huésped, monte `/dev/sda3` de sólo lectura (para proteger el sistema de archivos del host) y especifique `/full/path/to/images` ó usar algún truco kexec en el invitado para recargar el kernel del invitado (extiende el tiempo de arranque).

```
$ Qemu-system-i386 -kernel /boot/vmlinuz-linux -initrd /boot/initramfs-linux.img -append root=/dev/sda/dev/sda3

```

En el ejemplo anterior, la partición física que se utiliza para el sistema de archivos raíz del huésped es `/dev/sda3` en el host, pero aparece como `/dev/sda` en el invitado.

Por supuesto, puede especificar cualquier kernel e initrd que desee, y no sólo los que vienen con Arch Linux.

Cuando hay varios [kernel parameters](/index.php/Kernel_parameters "Kernel parameters") que se pasan a la opción `-append`, necesitan ser citados usando comillas simples o dobles. Por ejemplo:

```
$ ... -append 'root=/dev/sda1 console=ttyS0'

```

#### Simular disco virtual con MBR usando RAID lineal

Una forma más complicada de tener una máquina virtual usar una partición física, mientras que mantener esa partición formateada como un sistema de archivos y no sólo tener la partición invitado la partición como si fuera un disco, es simular un MBR para que pueda Arranque utilizando un gestor de arranque tal como GRUB.

Puede hacerlo utilizando el RAID del software en modo lineal (necesita el controlador de kernel `linear.ko`) y un dispositivo de loopback: el truco consiste en añadir previamente un registro maestro de arranque (MBR) Real que desea incrustar en una imagen de disco RAEM QEMU.

Suponga que tiene una partición simple `/` con algún sistema de archivos en la que desea formar parte de una imagen de disco QEMU. En primer lugar, crear un pequeño archivo para mantener el MBR:

```
$ dd if=/dev/zero of=*/path/to/mbr* count=32

```

Aquí, se crea un archivo de 16 KB (32 * 512 bytes). Es importante no hacerlo demasiado pequeño (incluso si el MBR sólo necesita un bloque de 512 bytes), ya que cuanto menor sea, menor será el tamaño del chasis del dispositivo RAID de software, lo que podría tener un impacto En el rendimiento. A continuación, configura un dispositivo de bucle invertido en el archivo MBR:

```
# losetup -f */path/to/mbr*

```

Supongamos que el dispositivo resultante es `/dev/loop0`, porque ya no habríamos estado usando otros bucle. El siguiente paso es crear la imagen de disco "fusionada" MBR + `/dev/hdaN` utilizando RAID de software:

```
# modprobe lineal

```

```
# mdadm --build --verbose /dev/md0 --chunk=16 --level=linear --raid-devices=2 /dev/loop0/dev/hda*N*

```

El resultante `/dev/md0` es lo que utilizará como una imagen de disco cruda QEMU (no olvide establecer los permisos para que el emulador pueda acceder a él). El último paso (y algo complicado) es configurar la configuración del disco (geometría del disco y tabla de particiones) para que el punto de inicio de la partición primaria en el MBR coincida con el de {{ic|/dev/hda*N*} Dentro `/dev/md0` (un desplazamiento de exactamente 16 * 512 = 16384 bytes en este ejemplo). Hacer esto usando `fdisk` en la máquina host, no en el emulador: la rutina de detección de disco crudo predeterminada de QEMU a menudo da lugar a offsets redondeados no kilobyte (como 31.5 KB, como en la sección anterior) que No puede ser administrado por el código RAID de software. Por lo tanto, desde el anfitrión:

```
$ fdisk /dev/md0

```

Pulse `X` para entrar en el menú de expertos. Establezca el número de sectores por pista para que el tamaño de un cilindro coincida con el tamaño de su archivo MBR. Para dos cabezas y un tamaño de sector de 512, el número de sectores por pista debe ser 16, por lo que obtenemos cilindros de tamaño 2x16x512 = 16k.

Ahora, presione `R` para regresar al menú principal.

Presione `P` y compruebe que el tamaño del cilindro es ahora 16k.

Ahora, cree una única partición primaria correspondiente a `/dev/hda*N*`. Debe comenzar en el cilindro 2 y terminar en el extremo del disco (tenga en cuenta que el número de cilindros ahora difiere de lo que era cuando se introdujo fdisk.

Finalmente, escribe el resultado al archivo: ya está. Ahora tiene una partición que puede montar directamente desde su host, así como parte de una imagen de disco QEMU:

```
$ Qemu-system-i386 -hdc /dev/md0 *[...]*

```

Por supuesto, puede configurar con seguridad cualquier cargador de arranque en esta imagen de disco utilizando QEMU, siempre que la partición original `/dev/hda*N*` contenga las herramientas necesarias.

## Redes

El rendimiento de la red virtual debería ser mejor con los dispositivos de derivación (tap) y puentes que con la red en modo de usuario o vde porque los dispositivos de derivación y los puentes se implementan en el kernel.

Además, el rendimiento de la red se puede mejorar asignando a las máquinas virtuales un dispositivo de red [virtio](http://wiki.libvirt.org/page/Virtio) en lugar de la emulación predeterminada de una NIC e1000\. Consulte [#Instalación de controladores virtio](#Instalaci.C3.B3n_de_controladores_virtio) para obtener más información.

### Advertencia de dirección a nivel de enlace

Al asignar el argumento `-net nic` a QEMU, asignará por defecto a una máquina virtual una interfaz de red con la dirección de enlace `52:54:00:12:34:56`. Sin embargo, cuando se utiliza la creación de redes puenteadas con varias máquinas virtuales, es esencial que cada máquina virtual tenga una dirección única de nivel de enlace (MAC) en el lado de la máquina virtual del dispositivo de derivación. De lo contrario, el puente no funcionará correctamente, ya que recibirá paquetes de varias fuentes que tienen la misma dirección de nivel de enlace. Este problema se produce incluso si los propios dispositivos de derivación tienen direcciones de nivel de enlace únicas porque la dirección de nivel de enlace de origen no se vuelve a escribir a medida que los paquetes pasan a través del dispositivo de derivación.

Asegúrese de que cada máquina virtual tiene una dirección única de nivel de enlace, pero siempre debe comenzar con `52:54:`. Utilice la opción siguiente, reemplazar *X* por un dígito hexadecimal arbitrario:

```
$ qemu-system-i386 -net nic,macaddr=52:54:*XX:XX:XX:XX* -net vde *disk_image*

```

Generar direcciones únicas de nivel de enlace se puede realizar de varias maneras:

1.  Especificar manualmente la dirección única de nivel de enlace para cada NIC. El beneficio es que el servidor DHCP asignará la misma dirección IP cada vez que se ejecute la máquina virtual, pero es inutilizable para un gran número de máquinas virtuales.
2.  Generar dirección de nivel de enlace aleatoria cada vez que se ejecuta la máquina virtual. Prácticamente cero probabilidad de colisiones, pero la desventaja es que el servidor DHCP asignará una dirección IP diferente cada vez. Puede utilizar el siguiente comando en una secuencia de comandos para generar una dirección de nivel de enlace aleatoria en una variable `macaddr`:
    ```
    printf -v macaddr "52:54:%02x:%02x:%02x:%02x" $(( $RANDOM & 0xff)) $(( $RANDOM & 0xff )) $(( $RANDOM & 0xff)) $(( $RANDOM & 0xff ))
    qemu-system-i386 -net nic,macaddr="$macaddr" -net vde *disk_image*
    ```

3.  Utilice el siguiente script `qemu-mac-hasher.py` para generar la dirección de nivel de enlace desde el nombre de la máquina virtual mediante una función de hash. Dado que los nombres de las máquinas virtuales son únicos, este método combina los beneficios de los métodos antes mencionados: genera la misma dirección de nivel de enlace cada vez que se ejecuta el script, aunque preserva la probabilidad prácticamente nula de colisiones. `qemu-mac-hasher.py` 
    ```
    #!/usr/bin/env python

    import sys
    import zlib

    if len(sys.argv) != 2:
        print("usage: %s <VM Name>" % sys.argv[0])
        sys.exit(1)

    crc = zlib.crc32(sys.argv[1].encode("utf-8")) & 0xffffffff
    crc = str(hex(crc))[2:]
    print("52:54:%s%s:%s%s:%s%s:%s%s" % tuple(crc))

    ```

    En un script, puede utilizar por ejemplo:

    ```
    vm_name="*VM Name*"
    qemu-system-i386 -name "$vm_name" -net nic,macaddr=$(qemu-mac-hasher.py "$vm_name") -net vde *disk_image*

    ```

### Redes en modo de usuario

De forma predeterminada, sin ningún argumento `-netdev`, QEMU utilizará la red en modo usuario con un servidor DHCP incorporado. A sus máquinas virtuales se les asignará una dirección IP cuando ejecuten su cliente DHCP, y podrán acceder a la red del host físico a través de la mascarada de IP realizada por QEMU.

**Advertencia:** Esto sólo funciona con los protocolos TCP y UDP, por lo que ICMP, incluido `ping`, no funcionará. No utilice `ping` para probar la conectividad de red.

Esta configuración predeterminada permite que sus máquinas virtuales accedan fácilmente a Internet, siempre que el host esté conectado a él, pero las máquinas virtuales no estarán directamente visibles en la red externa ni las máquinas virtuales podrán comunicarse entre sí si empieza Más de uno simultáneamente.

La red de usuario en modo QEMU puede ofrecer más capacidades, como servidores TFTP o SMB incorporados, redirigir los puertos del host al huésped (por ejemplo, para permitir conexiones SSH al invitado) o conectar invitados a las VLAN para que puedan hablar entre sí. Consulte la documentación de QEMU en el indicador `-net user` para obtener más detalles.

Sin embargo, la conexión en red en modo usuario tiene limitaciones tanto en la utilidad como en el rendimiento. Las configuraciones de red más avanzadas requieren el uso de dispositivos de derivación u otros métodos.

### Tap de red con QEMU

Los [dispositivos tap](https://en.wikipedia.org/wiki/TUN/TAP "wikipedia:TUN/TAP") Son una característica del kernel de Linux que le permite crear interfaces de red virtuales que aparecen como interfaces de red reales. Los paquetes enviados a una interfaz de derivación se entregan a un programa de espacio de usuario, tal como QEMU, que se ha enlazado a la interfaz.

QEMU puede utilizar la red de derivación para una máquina virtual de modo que los paquetes enviados a la interfaz de derivación se envíen a la máquina virtual y aparezcan como procedentes de una interfaz de red (normalmente una interfaz Ethernet) en la máquina virtual. Por el contrario, todo lo que la máquina virtual envía a través de su interfaz de red aparecerá en la interfaz de tap.

Los dispositivos de toque son soportados por los controladores de puente de Linux, por lo que es posible conectar entre sí los dispositivos entre sí y posiblemente con otras interfaces de host como `eth0`. Esto es deseable si desea que sus máquinas virtuales puedan hablar entre sí, o si desea que otras máquinas en su LAN puedan hablar con las máquinas virtuales.

{{Advertencia| Si conectas el dispositivo de toque y alguna interfaz de host, como `eth0`, las máquinas virtuales aparecerán directamente en la red externa, lo que los exponerá a posibles ataques. Dependiendo de los recursos a los que tengan acceso sus máquinas virtuales, es posible que tenga que tomar todas las [precauciones](/index.php/Firewalls "Firewalls") que normalmente tomaría al asegurar una computadora para proteger sus máquinas virtuales. Si el riesgo es demasiado grande, las máquinas virtuales tienen pocos recursos o se configuran varias máquinas virtuales, una solución mejor podría ser utilizar [[#Red de host solamente] y configurar NAT. En este caso sólo necesitará un firewall en el host en lugar de múltiples firewalls para cada huésped.}}

Como se indica en la sección de conexión en red de modo de usuario, los dispositivos de derivación ofrecen un rendimiento de red más alto que el modo de usuario. Si el OS invitado admite el controlador de red virtio, el rendimiento de la red se incrementará considerablemente también. Suponiendo el uso del dispositivo tap0, que el controlador virtio se utiliza en el invitado, y que no se utilizan scripts para ayudar a iniciar / detener la creación de redes, a continuación es parte del comando qemu se debe ver:

```
-net nic, model=virtio -net tap, ifname=tap0, script=no, downscript=no

```

Pero si ya está utilizando un dispositivo de tap con virtio controlador de red, uno puede incluso aumentar el rendimiento de la red mediante la activación de vhost, como:

```
-net nic, model=virtio -net tap, ifname=tap0, script=no, downscript=no, vhost=on

```

Ver [http://www.linux-kvm.com/content/how-maximize-virtio-net-performance-vhost-net](http://www.linux-kvm.com/content/how-maximize-virtio-net-performance-vhost-net) para obtener más información.

#### Red de host solamente

Si al puente se le da una dirección IP y se permite el tráfico destinado a ello, pero no hay una interfaz real (por ejemplo, `eth0`) conectada al puente, las máquinas virtuales podrán hablar entre sí y la Sistema anfitrión. Sin embargo, no podrán hablar con nada en la red externa, siempre y cuando no configure IP enmascarada en el host físico. Esta configuración se llama *red de host solamente* por otro software de virtualización como [VirtualBox](/index.php/VirtualBox "VirtualBox").

**Sugerencia:**

*   Si desea configurar IP masquerading, ej. NAT para máquinas virtuales, consulte la página [Internet sharing#Enable NAT](/index.php/Internet_sharing#Enable_NAT "Internet sharing").
*   Es posible que desee tener un servidor DHCP que se ejecute en la interfaz de puente para dar servicio a la red virtual. Por ejemplo, para usar la subred `172.20.0.1/16` con [dnsmasq](/index.php/Dnsmasq "Dnsmasq") como servidor DHCP:

```
# ip addr add 172.20.0.1/16 dev br0
# ip link set br0 up
# dnsmasq --interface=br0 --bind-interfaces --dhcp-range=172.20.0.2,172.20.255.254

```

#### Red interna

Si no le da al puente una dirección IP y agrega una regla [iptables](/index.php/Iptables "Iptables") para eliminar todo el tráfico al puente en la cadena INPUT, las máquinas virtuales podrán hablar entre sí, pero no con el host físico ó la red exterior. Esta configuración se llama "red interna" por otro software de virtualización como [VirtualBox](/index.php/VirtualBox "VirtualBox"). Deberá asignar direcciones IP estáticas a las máquinas virtuales o ejecutar un servidor DHCP en una de ellas.

De forma predeterminada, iptables eliminaría los paquetes de la red de bridge. Es posible que necesite utilizar dicha regla iptables para permitir paquetes en una red puenteada:

```
# iptables -I FORWARD -m physdev --physdev-is-bridged -j ACCEPT

```

#### Redes puenteadas usando qemu-bridge-helper

**Nota:** Este método está disponible desde QEMU 1.1, consulte [http://wiki.qemu.org/Features/HelperNetworking](http://wiki.qemu.org/Features/HelperNetworking).

Este método no requiere una secuencia de comandos de inicio y acepta fácilmente múltiples tomas y puentes múltiples. Utiliza el binario `/usr/lib/qemu/qemu-bridge-helper`, que permite crear dispositivos de derivación en un puente existente.

**Sugerencia:** Consulte [Network bridge](/index.php/Network_bridge "Network bridge") para obtener información sobre cómo crear un puente.

En primer lugar, cree un archivo de configuración que contenga los nombres de todos los puentes que QEMU utilizará:

 `/etc/qemu/bridge.conf` 
```
allow *bridge0*
allow *bridge1*
...
```

Ahora inicie la VM. El uso más básico sería:

```
$ qemu-system-i386 -net nic -net bridge,br=*bridge0* *[...]*

```

Con múltiples taps, el uso más básico requiere especificar la VLAN para todos los NIC adicionales:

```
$ qemu-system-i386 -net nic -net bridge,br=*bridge0* -net nic,vlan=1 -net bridge,vlan=1,br=*bridge1* *[...]*

```

#### Creación manual del puente

**Sugerencia:** Desde QEMU 1.1, el [puente de red ayudante](http://wiki.qemu.org/Features/HelperNetworking) puede establecer tun / tap up para usted sin necesidad de secuencias de comandos adicionales. Consulte [#Blocales de red utilizando qemu-bridge-helper](#Blocales_de_red_utilizando_qemu-bridge-helper).

A continuación se describe cómo conectar una máquina virtual con una interfaz de host como `eth0`, que es probablemente la configuración más común. Esta configuración hace que parezca que la máquina virtual está ubicada directamente en la red externa, en el mismo segmento Ethernet que la máquina host física.

Vamos a reemplazar el adaptador Ethernet normal con un adaptador de puente y enlazar el adaptador Ethernet normal a él.

*   Instale [bridge-utils](https://www.archlinux.org/packages/?name=bridge-utils), que proporciona `brctl` para manipular puentes.

*   Habilitar el reenvío IPv4:

```
# sysctl net.ipv4.ip_forward=1

```

Para hacer el cambio permanente, cambie `net.ipv4.ip_forward = 0` a `net.ipv4.ip_forward = 1` en `/etc/sysctl.d/99-sysctl.conf`.

*   Cargue el módulo `tun` y configurelo para cargarlo en el arranque. Ver [Kernel modules](/index.php/Kernel_modules "Kernel modules") para más detalles.

*   Ahora cree el puente. Ver [Bridge with netctl](/index.php/Bridge_with_netctl "Bridge with netctl") para más detalles. Recuerde nombrar su puente como `br0`, o modifique lo scripts a continuación del nombre del puente.

*   Cree el script que QEMU utiliza para abrir el adaptador de toma con los permisos `root:kvm` 750:

 `/etc/qemu-ifup` 
```
#!/bin/sh

echo "Executing /etc/qemu-ifup"
echo "Bringing up $1 for bridged mode..."
sudo /usr/bin/ip link set $1 up promisc on
echo "Adding $1 to br0..."
sudo /usr/bin/brctl addif br0 $1
sleep 2

```

*   Cree el guión que QEMU utiliza para derribar el adaptador de toma en `/etc/qemu-ifdown` con los permisos `root:kvm` 750:

 `/etc/qemu-ifdown` 
```
#!/bin/sh

echo "Executing /etc/qemu-ifdown"
sudo /usr/bin/ip link set $1 down
sudo /usr/bin/brctl delif br0 $1
sudo /usr/bin/ip link delete dev $1

```

*   Use `visudo` para añadir lo siguiente a el archivo `sudoers`:

```
Cmnd_Alias      QEMU=/usr/bin/ip,/usr/bin/modprobe,/usr/bin/brctl
%kvm     ALL=NOPASSWD: QEMU

```

*   Se inicia QEMU con el siguiente script `run-qemu`:

 `run-qemu` 
```
#!/bin/bash
USERID=$(whoami)

# Get name of newly created TAP device; see https://bbs.archlinux.org/viewtopic.php?pid=1285079#p1285079
precreationg=$(/usr/bin/ip tuntap list | /usr/bin/cut -d: -f1 | /usr/bin/sort)
sudo /usr/bin/ip tuntap add user $USERID mode tap
postcreation=$(/usr/bin/ip tuntap list | /usr/bin/cut -d: -f1 | /usr/bin/sort)
IFACE=$(comm -13 <(echo "$precreationg") <(echo "$postcreation"))

# This line creates a random MAC address. The downside is the DHCP server will assign a different IP address each time
printf -v macaddr "52:54:%02x:%02x:%02x:%02x" $(( $RANDOM & 0xff)) $(( $RANDOM & 0xff )) $(( $RANDOM & 0xff)) $(( $RANDOM & 0xff ))
# Instead, uncomment and edit this line to set a static MAC address. The benefit is that the DHCP server will assign the same IP address.
# macaddr='52:54:be:36:42:a9'

qemu-system-i386 -net nic,macaddr=$macaddr -net tap,ifname="$IFACE" $*

sudo ip link set dev $IFACE down &> /dev/null
sudo ip tuntap del $IFACE mode tap &> /dev/null

```

Para ejecutar una VM, haz algo como esto:

```
$ run-qemu -hda *myvm.img* -m 512 -vga std

```

*   Se recomienda, por motivos de rendimiento y seguridad, deshabilitar el firewall [en el puente](http://ebtables.netfilter.org/documentation/bridge-nf.html):

 `/etc/sysctl.d/10-disable-firewall-on-bridge.conf` 
```
net.bridge.bridge-nf-call-ip6tables = 0
net.bridge.bridge-nf-call-iptables = 0
net.bridge.bridge-nf-call-arptables = 0

```

Ejecute `sysctl -p /etc/sysctl.d/10-disable-firewall-on-bridge.conf` para aplicar los cambios inmediatamente.

Ver [libvirt wiki](http://wiki.libvirt.org/page/Networking#Creating_network_initscripts) y [Fedora bug 512206](https://bugzilla.redhat.com/show_bug.cgi?id=512206). Si obtiene errores de sysctl durante el inicio de archivos no existentes, haga que el módulo `bridge` se cargue al arrancar. Ver [Kernel modules#Automatic module handling](/index.php/Kernel_modules#Automatic_module_handling "Kernel modules").

Como alternativa, puede configurar [iptables](/index.php/Iptables "Iptables") para permitir que todo el tráfico se reenvíe a través del puente mediante la adición de una regla como esta:

```
-I FORWARD -m physdev --physdev-is-bridged -j ACCEPT

```

#### Compartición de red entre dispositivo físico y un dispositivo de toque a través de iptables

La conexión en puente funciona bien entre una interfaz cableada (por ejemplo, eth0), y es fácil de configurar. Sin embargo, si el host se conecta a la red a través de un dispositivo inalámbrico, el puente no es posible.

Consulte [Network bridge#Wireless interface on a bridge](/index.php/Network_bridge#Wireless_interface_on_a_bridge "Network bridge") como referencia.

Una forma de superar esto es configurar un dispositivo de derivación con una IP estática, haciendo que linux maneje automáticamente el enrutamiento para ella y, a continuación, reenvíe el tráfico entre la interfaz de derivación y el dispositivo conectado a la red a través de las reglas de iptables.

Consulte [Internet sharing](/index.php/Internet_sharing "Internet sharing") como referencia.

Allí puede encontrar lo que se necesita para compartir la red entre dispositivos, incluidos los de tap y tun. Lo siguiente sólo indica algunas de las configuraciones de host requeridas. Como se indica en la referencia anterior, el cliente debe configurarse para una IP estática, utilizando la IP asignada a la interfaz de derivación como puerta de enlace. La advertencia es que los servidores DNS del cliente pueden necesitar ser editados manualmente si cambian al cambiar de un dispositivo host conectado a la red a otro.

Para permitir el reenvío de IP en cada inicio, es necesario agregar las siguientes líneas al archivo de configuración de sysctl dentro de /etc/sysctl.d:

```
net.ipv4.ip_forward = 1
net.ipv6.conf.default.forwarding = 1
net.ipv6.conf.all.forwarding = 1

```

Las reglas de iptables pueden verse así:

```
# Forwarding from/to outside
iptables -A FORWARD -i ${INT} -o ${EXT_0} -j ACCEPT
iptables -A FORWARD -i ${INT} -o ${EXT_1} -j ACCEPT
iptables -A FORWARD -i ${INT} -o ${EXT_2} -j ACCEPT
iptables -A FORWARD -i ${EXT_0} -o ${INT} -j ACCEPT
iptables -A FORWARD -i ${EXT_1} -o ${INT} -j ACCEPT
iptables -A FORWARD -i ${EXT_2} -o ${INT} -j ACCEPT
# NAT/Masquerade (network address translation)
iptables -t nat -A POSTROUTING -o ${EXT_0} -j MASQUERADE
iptables -t nat -A POSTROUTING -o ${EXT_1} -j MASQUERADE
iptables -t nat -A POSTROUTING -o ${EXT_2} -j MASQUERADE

```

El anterior supone que hay 3 dispositivos conectados a la red compartiendo tráfico con un dispositivo interno, donde por ejemplo:

```
INT=tap0
EXT_0=eth0
EXT_1=wlan0
EXT_2=tun0

```

El anterior muestra un reenvío que permitiría compartir conexiones cableadas e inalámbricas con el dispositivo de derivación (tap).

Las reglas de reenvío que se muestran son apátridas y para el reenvío puro. Se podría pensar en restringir el tráfico específico, poniendo un cortafuegos en el lugar para proteger al huésped y otros. Sin embargo, esto reduciría el rendimiento de la red, mientras que un simple puente no incluye nada de eso.

Bonus: Si la conexión es cableada o inalámbrica, si se conecta a través de VPN a un sitio remoto con un dispositivo tun, suponiendo que el dispositivo tun abierto para esa conexión es tun0, y las reglas iptables anteriores se aplican, entonces la conexión remota se obtiene también Compartido con el huésped. Esto evita la necesidad de que el invitado también abra una conexión VPN. Una vez más, como la red de invitados debe ser estática, entonces si la conexión del host de forma remota de esta manera, uno probablemente tendrá que editar los servidores DNS en el invitado.

### Trabajo en red con VDE2

#### ¿Qué es VDE?

VDE significa Virtual Distributed Ethernet. Comenzó como una mejora del interruptor [uml](/index.php/User-mode_Linux "User-mode Linux") _. Es una caja de herramientas para administrar redes virtuales.

La idea es crear interruptores virtuales, que son básicamente sockets, y "conectar" tanto máquinas físicas como máquinas virtuales en ellas. La configuración que mostramos aquí es bastante simple; Sin embargo, VDE es mucho más potente que esto, puede conectar conmutadores virtuales juntos, ejecutarlos en diferentes hosts y supervisar el tráfico en los switches. Usted está invitado a leer [la documentación del proyecto](http://wiki.virtualsquare.org/wiki/index.php/Main_Page).

La ventaja de este método es que no tienes que agregar privilegios de sudo a tus usuarios. No se debe permitir que los usuarios regulares ejecuten modprobe.

#### Basics

El soporte de VDE puede ser [instalado](/index.php/Pacman "Pacman") a través del paquete [vde2](https://www.archlinux.org/packages/?name=vde2) en los [repositorios oficiales](/index.php?title=Repositorios_oficiales&action=edit&redlink=1 "Repositorios oficiales (page does not exist)").

En nuestra configuración, usamos tun/tap para crear una interfaz virtual en el host. Cargue el módulo `tun` (consulte [kernel modules](/index.php/Kernel_modules "Kernel modules") para obtener más detalles):

```
# modprobe tun

```

Ahora crea el conmutador virtual:

```
# vde_switch -tap tap0 -daemon -mod 660 -group users

```

Esta línea crea el switch, crea `tap0`, lo "enchufa" y permite a los usuarios del grupo `users` usarlo.

La interfaz está conectada pero no está configurada todavía. Para configurarlo, ejecute este comando:

```
# ip addr add 192.168.100.254/24 dev tap0

```

Ahora, sólo tiene que ejecutar KVM con estas opciones `-net` como usuario normal:

```
$ qemu-system-i386 -net nic -net vde -hda *[...]*

```

Configure la red para su invitado como lo haría en una red física.

**Sugerencia:** es posible que desee configurar NAT en dispositivo de toque para acceder a Internet desde la máquina virtual. Consulte [Internet sharing#Enable NAT](/index.php/Internet_sharing#Enable_NAT "Internet sharing") para obtener más información.

#### Startup scripts

Ejemplo de script principal que inicia VDE:

 `/etc/systemd/scripts/qemu-network-env` 
```
#!/bin/sh
# Preparación del entorno de red QEMU/VDE

# La configuración IP del dispositivo de derivación que se utilizará para
# La red de la máquina virtual:

TAP_DEV=tap0
TAP_IP=192.168.100.254
TAP_MASK=24
TAP_NETWORK=192.168.100.0

# Host interface
NIC=eth0

case "$1" in
  start)
        echo -n "Starting VDE network for QEMU: "

        # If you want tun kernel module to be loaded by script uncomment here
	#modprobe tun 2>/dev/null
	## Wait for the module to be loaded
 	#while ! lsmod | grep -q "^tun"; do echo "Waiting for tun device"; sleep 1; done

        # Start tap switch
        vde_switch -tap "$TAP_DEV" -daemon -mod 660 -group users

        # Bring tap interface up
        ip address add "$TAP_IP"/"$TAP_MASK" dev "$TAP_DEV"
        ip link set "$TAP_DEV" up

        # Start IP Forwarding
        echo "1" > /proc/sys/net/ipv4/ip_forward
        iptables -t nat -A POSTROUTING -s "$TAP_NETWORK"/"$TAP_MASK" -o "$NIC" -j MASQUERADE
        ;;
  stop)
        echo -n "Stopping VDE network for QEMU: "
        # Delete the NAT rules
        iptables -t nat -D POSTROUTING "$TAP_NETWORK"/"$TAP_MASK" -o "$NIC" -j MASQUERADE

        # Bring tap interface down
        ip link set "$TAP_DEV" down

        # Kill VDE switch
        pgrep -f vde_switch | xargs kill -TERM
        ;;
  restart|reload)
        $0 stop
        sleep 1
        $0 start
        ;;
  *)
        echo "Usage: $0 {start|stop|restart|reload}"
        exit 1
esac
exit 0

```

Ejemplo de servicio systemd utilizando el script anterior:

 `/etc/systemd/system/qemu-network-env.service` 
```
[Unit]
Description=Manage VDE Switch

[Service]
Type=oneshot
ExecStart=/etc/systemd/scripts/qemu-network-env start
ExecStop=/etc/systemd/scripts/qemu-network-env stop
RemainAfterExit=yes

[Install]
WantedBy=multi-user.target

```

Cambiar permisos de `qemu-network-env` para ser ejecutable

```
# chmod u+x /etc/systemd/scripts/qemu-network-env

```

Puede iniciar `qemu-network-env.service` como de costumbre.

#### Método alternativo

Si el método anterior no funciona o no quiere meterse con las configuraciones del kernel, TUN, dnsmasq e iptables, puede hacer lo siguiente para obtener el mismo resultado.

```
# vde_switch -daemon -mod 660 -group users
# slirpvde --dhcp --daemon

```

A continuación, para iniciar la VM con una conexión a la red del host:

```
$ qemu-system-i386 -net nic,macaddr=52:54:00:00:EE:03 -net vde *disk_image*

```

### Puente VDE2

Basado en [quickhowto: qemu networking using vde, tun/tap, and bridge](http://selamatpagicikgu.wordpress.com/2011/06/08/quickhowto-qemu-networking-using-vde-tuntap-and-bridge/) gráfico. Cualquier máquina virtual conectada a vde está expuesta externamente. Por ejemplo, cada máquina virtual puede recibir la configuración DHCP directamente desde su enrutador ADSL.

#### Conceptos básicos

Recuerde que necesita el módulo `tun` y el paquete [bridge-utils](https://www.archlinux.org/packages/?name=bridge-utils).

Cree el dispositivo vde2/tap:

```
# vde_switch -tap tap0 -daemon -mod 660 -group users
# ip link set tap0 up

```

Cree el puente:

```
# brctl addbr br0

```

Agregue dispositivos:

```
# brctl addif br0 eth0
# brctl addif br0 tap0

```

Y configure la interfaz del puente:

```
# dhcpcd br0

```

#### Startup scripts

Todos los dispositivos deben estar configurados. Y sólo el puente necesita una dirección IP. Para dispositivos físicos en el puente (por ejemplo, `eth0`), esto puede hacerse con [netctl](/index.php/Netctl "Netctl") utilizando un perfil Ethernet personalizado con:

 `/etc/netctl/ethernet-noip` 
```
Description='A more versatile static Ethernet connection'
Interface=eth0
Connection=ethernet
IP=no

```

El siguiente servicio systemd personalizado puede utilizarse para crear y activar una interfaz de toma VDE2 para su uso en el grupo de usuarios `users`.

 `/etc/systemd/system/vde2@.service` 
```
[Unit]
Description=Network Connectivity for %i
Wants=network.target
Before=network.target

[Service]
Type=oneshot
RemainAfterExit=yes
ExecStart=/usr/bin/vde_switch -tap %i -daemon -mod 660 -group users
ExecStart=/usr/bin/ip link set dev %i up
ExecStop=/usr/bin/ip addr flush dev %i
ExecStop=/usr/bin/ip link set dev %i down

[Install]
WantedBy=multi-user.target

```

Y, por último, puede crear el puente interfaz con netctl.

## Gráficos

QEMU puede utilizar las siguientes salidas gráficas diferentes: `std`, `qxl`, `vmware`, `virtio`, `cirrus` y `none`.

### std

Con `-vga std` puede obtener una resolución de hasta 2560 x 1600 píxeles sin necesidad de controladores invitados. Este es el valor predeterminado desde QEMU 2.2.

### qxl

QXL Es un controlador de gráficos paravirtual con soporte 2D. Para usarlo, pase la opción `-vga qxl` e instale los controladores en el invitado. Es posible que desee utilizar SPICE para mejorar el rendimiento gráfico al utilizar QXL.

En los invitados de Linux, los módulos del kernel `qxl` y `bochs_drm` deben ser inicializados para poder tener un rendimiento descente.

#### SPICE

El proyecto [SPICE](http://spice-space.org/) tiene como objetivo proporcionar una solución completa de código abierto para el acceso remoto a máquinas virtuales de una manera transparente.

SPICE sólo se puede utilizar cuando se utiliza QXL como la salida gráfica.

El siguiente es un ejemplo de arranque con SPICE como protocolo de escritorio remoto:

```
$ qemu-system-i386 -vga qxl -spice port=5930,disable-ticketing -chardev spicevm 

```

Conéctese al invitado utilizando un cliente SPICE. En este momento se recomienda [spice-gtk](https://www.archlinux.org/packages/?name=spice-gtk), sin embargo otros [clientes](http://www.spice-space.org/download.html), incluyendo otras plataformas, están disponibles:

```
$ spicy -h 127.0.0.1 -p 5930

```

El uso de [Unix sockets](https://en.wikipedia.org/wiki/Unix_socket "wikipedia:Unix socket") en lugar de los puertos TCP no implica el uso de pila de red en el sistema host, por lo que es [Sockets-vs-tcp-ports según se informa](https://unix.stackexchange.com/questions/91774/performance-of-unix-) mejor para el rendimiento. Ejemplo:

```
$ qemu-system-x86_64 -vga qxl -device virtio-serial-pci -device virtserialport,chardev=spicechannel0,name=com.redhat.spice.0 -chardev spicevmc,id=spicechannel0,name=vdagent -spice unix,addr=/tmp/vm_spice.socket,disable-ticketing
$ spicy --uri="spice+unix:///tmp/vm_spice.socket"

```

Para una mejor compatibilidad con varios monitores, compartir el portapapeles, etc., los paquetes siguientes deben estar instalados en el invitado:

*   [spice-vdagent](https://www.archlinux.org/packages/?name=spice-vdagent): Spice agent xorg cliente que permite copiar y pegar entre el cliente y X-session y más
*   [xf86-video-qxl](https://www.archlinux.org/packages/?name=xf86-video-qxl) [xf86-video-qxl-git](https://aur.archlinux.org/packages/xf86-video-qxl-git/): Xorg X11 qxl controlador de vídeo
*   Para otros sistemas operativos, mire la sección Guest de la página [SPICE-Space download](http://www.spice-space.org/download.html).

### vmware

Aunque tiene pocos errores, tiene mejor rendimiento que std y cirrus. Instale los controladores de VMware [xf86-video-vmware](https://www.archlinux.org/packages/?name=xf86-video-vmware) y [xf86-input-vmmouse](https://www.archlinux.org/packages/?name=xf86-input-vmmouse) para los invitados de Arch Linux.

### virtio

`virtio-vga` / `virtio-gpu` Es un controlador de gráficos 3D paravirtual basado en [virgl](https://virgil3d.github.io/). Actualmente un trabajo en curso, que sólo admite a invitados Linux (>= 4.4) con [mesa](https://www.archlinux.org/packages/?name=mesa) (>= 11.2) compilados con la opción `--with-gallium-drivers=virgl`.

Para activar la aceleración 3D en el sistema invitado, seleccione vga con `-vga virtio` y habilitar el contexto opengl en el dispositivo de visualización con `-display sdl,gl=on` ó `-display gtk,gl=on` Para la salida de pantalla sdl y gtk respectivamente. La configuración correcta se puede confirmar mirando el registro del kernel en el invitado:

 `$ dmesg | grep drm ` 
```
[drm] pci: virtio-vga detected
[drm] virgl 3d acceleration enabled

```

A partir de septiembre de 2016, el soporte para el protocolo de especias está en desarrollo y se puede probar la instalación de la versión de desarrollo de [spice](https://www.archlinux.org/packages/?name=spice) (>= 0.13.2) y la recompilación de qemu.

Para más información visite [blog de kraxel](https://www.kraxel.org/blog/tag/virgl/).

### cirrus

El adaptador gráfico cirrus fue el predeterminado [before 2.2](http://wiki.qemu.org/ChangeLog/2.2#VGA). [no debería](Https://www.kraxel.org/blog/2014/10/qemu-using-cirrus-considered-harmful/) utilizarse en sistemas modernos.

### none

Esto es como un PC que no tiene tarjeta VGA en absoluto. Ni siquiera podrías acceder a ella con la opción `-vnc`. Además, esto es diferente de la opción `-nographic` que permite a QEMU emular una tarjeta VGA, pero deshabilita la visualización SDL.

### vnc

Dado que usó la opción `-nographic`, puede agregar la opción `-vnc display` para que QEMU escuche en `display` y redirigir la pantalla VGA a la sesión VNC . Hay un ejemplo de esto en las configuraciones de ejemplo de la sección [#Starting QEMU virtual machines on boot](#Starting_QEMU_virtual_machines_on_boot).

```
$ qemu-system-i386 -vga std -nographic -vnc :0
$ gvncviewer :0

```

Al usar VNC, puede experimentar problemas de teclado descritos (en detalles gory) [Know-about-virtual-keyboard-handling / aquí](https://www.berrange.com/posts/2010/07/04/more-than-you-or-+-wanted-to-). La solución es "no" usar la opción `-k` en QEMU y usar `gvncviewer` de [gtk-vnc](https://www.archlinux.org/packages/?name=gtk-vnc). Ver también [este](http://www.mail-archive.com/libvir-list@redhat.com/msg13340.html) mensaje publicado en la lista de correo de libvirt.

## Audio

### Host

El controlador de audio utilizado por QEMU se establece con la variable de entorno `QEMU_AUDIO_DRV`:

```
$ export QEMU_AUDIO_DRV=pa

```

Ejecute el siguiente comando para obtener las opciones de configuración de QEMU relacionadas con PulseAudio:

```
$ qemu-system-x86_64 -audio-help | awk '/Name: pa/' RS=

```

Las opciones listadas se pueden exportar como variables de entorno, por ejemplo:

```
$ export QEMU_PA_SINK=alsa_output.pci-0000_04_01.0.analog-stereo.monitor
$ export QEMU_PA_SOURCE=input
```

### Invitado

Para obtener la lista de los controladores de audio de emulación compatibles:

```
$ qemu-system-x86_64 -soundhw help

```

Para usar (ej. `hda`) para el invitado utilice el comando `-soundhw hda` con QEMU.

**Nota:** Los controladores emulados con tarjeta gráfica de vídeo para la máquina invitada también pueden causar un problema con la calidad del sonido. Pruebe uno por uno para que funcione. Puede listar las opciones posibles con `qemu-system-x86_64 -h` .

## Instalación de controladores virtio

QEMU ofrece a los clientes la posibilidad de utilizar dispositivos bloqueados y de red paravirtualizados utilizando los controladores [virtio](http://wiki.libvirt.org/page/Virtio), que proporcionan un mejor rendimiento y menores gastos generales.

Un dispositivo virtio bloque requiere la opción `-drive` en lugar del simple `-hd *` más `if=virtio`:

```
$ qemu-system-i386 -boot order=c -drive file=*disk_image*,if=virtio

```

**Nota:** `-boot order=c` es absolutamente necesario cuando se desea arrancar desde él. No hay detección automática como con `-hd*`.

*   Casi de la misma manera para la red:

```
$ qemu-system-i386 -net nic,model=virtio

```

**Nota:** Esto sólo funcionará si la máquina invitada tiene controladores para dispositivos virtio. Linux lo hace, y los controladores necesarios están incluidos en Arch Linux, pero no hay garantía de que los dispositivos virtio funcionen con otros sistemas operativos.

### Preparando a Arch Linux como invitado

Para utilizar los dispositivos virtio después de instalar un invitado de Arch Linux, se deben cargar en el invitado los siguientes módulos: `virtio`, `virtio_pci`, `virtio_blk`, `Virtio_net`, y `virtio_ring`. Para los huéspedes de 32 bits, no es necesario el módulo "virtio" específico.

Si desea arrancar desde un disco virtio, el disco ramd inicial debe contener los módulos necesarios. De forma predeterminada, esto es manejado por el gancho `autodetect` de [mkinitcpio](/index.php/Mkinitcpio "Mkinitcpio"). De lo contrario, utilice la matriz `MODULES` en `/etc/mkinitcpio.conf` para incluir los módulos necesarios y reconstruir el disco ramd inicial.

 `/etc/mkinitcpio.conf`  `MODULES="virtio virtio_blk virtio_pci virtio_net"` 

Los discos Virtio se reconocen con el prefijo `**v**` (ej. `**v** da`, {{ic|**v** db} }, etc.); Por lo tanto, los cambios deben realizarse al menos en `/etc/fstab` y `/boot/grub/grub.cfg` al arrancar desde un disco virtio.

**Nota:** Cuando se hace referencia a discos por [UUID](/index.php/UUID "UUID") en `/etc/fstab` y bootloader, no hay nada que hacer.

Se puede encontrar más información sobre la paravirtualización con KVM [aquí](http://www.linux-kvm.org/page/Boot_from_virtio_block_device).

También puede instalar [qemu-guest-agent](https://www.archlinux.org/packages/?name=qemu-guest-agent) para implementar la compatibilidad con los comandos QMP que mejorarán las capacidades de administración del hipervisor. Después de instalar el paquete, puedes habilitar e iniciar el `qemu-ga.service`.

### Preparar un invitado de Windows

**Nota:** La única forma (fiable) de actualizar un cliente de Windows 8.1 a Windows 10 parece que es elegir temporalmente cpu core2duo, nx para la instalación [[3]](http://ubuntuforums.org/showthread.php?t=2289210). Después de la instalación, puede volver a otros ajustes de la CPU (8/8/2015).

#### Bloquear controladores de dispositivo

##### Nueva instalación de Windows

Windows no viene con los controladores virtio. Por lo tanto, tendrá que cargarlos durante la instalación. Hay básicamente dos maneras de hacer esto: vía disco blando o vía archivos de ISO. Ambas imágenes se pueden descargar desde el repositorio [Fedora](https://fedoraproject.org/wiki/Windows_Virtio_Drivers).

La opción del disquete es difícil porque necesitará presionar F6 (Shift-F6 en Windows más reciente) al inicio de la alimentación del QEMU. Esto es difícil ya que necesitas tiempo para conectar tu ventana de consola VNC. Puede intentar agregar un retardo a la secuencia de arranque. Consulte `man qemu-system` para obtener más detalles sobre la aplicación de un retardo en el arranque.

La opción ISO para cargar los controladores es la forma preferida, pero está disponible sólo en Windows Vista y Windows Server 2008 y versiones posteriores. El procedimiento consiste en cargar la imagen con controladores virtio en un dispositivo de cdrom adicional junto con el dispositivo de disco principal y el instalador de Windows:

```
$ qemu-system-i386 ... \
-drive file=*/path/to/primary/disk.img*,index=0,media=disk,if=virtio \
-drive file=*/path/to/installer.iso*,index=2,media=cdrom \
-drive file=*/path/to/virtio.iso*,index=3,media=cdrom \
...

```

Durante la instalación, el instalador de Windows le pedirá su clave de producto y realizará algunas comprobaciones adicionales. Cuando llegue a la "¿Dónde desea instalar Windows?" Pantalla, dará una advertencia de que no se encuentran discos. Siga las instrucciones de ejemplo siguientes (basadas en Windows Server 2012 R2 con Actualización).

*   Seleccione la opción `Load Drivers`.
*   Desactive la casilla de "Ocultar los controladores que no son compatibles con el hardware de este equipo".
*   Haga clic en el botón Examinar y abra el CDROM para la virtio iso, normalmente llamada "virtio-win-XX".
*   Ahora vaya a `E:\viostor\[your-os]\amd64`, seleccione y pulse OK.
*   Click Next

Ahora debería ver sus discos virtio listados aquí, listos para ser seleccionados, formateados e instalados.

##### Cambiar la máquina virtual existente de Windows para utilizar virtio

Modificar un invitado de Windows existente para arrancar desde disco virtio es un poco difícil.

Puede descargar el controlador de disco virtio desde el [repositorio de Fedora](https://fedoraproject.org/wiki/Windows_Virtio_Drivers).

Ahora necesita crear una nueva imagen de disco, que llene la fuerza de Windows para buscar el controlador. Por ejemplo:

```
$ qemu-img create -f qcow2 *fake.qcow2* 1G

```

Ejecute el invitado original de Windows (con el disco de inicio todavía en modo IDE) con el disco falso (en modo virtio) y un CD-ROM con el controlador.

```
$ qemu-system-i386 -m 512 -vga std -drive file=*windows_disk_image*,if=ide -drive file=*fake.qcow2*,if=virtio -cdrom virtio-win-0.1-81.iso

```

Windows detectará el disco falso y tratará de encontrar un controlador para ello. Si falla, vaya al *Administrador de dispositivos* , busque la unidad SCSI con un icono de signo de exclamación (debe estar abierto), haga clic en *Actualizar controlador* y seleccione el CD-ROM virtual. No olvide seleccionar la casilla de verificación que dice que debe buscar directorios recursivamente.

Cuando la instalación se realiza correctamente, puede apagar la máquina virtual y volver a iniciarla, ahora con el disco de arranque conectado en modo virtio:

```
$ qemu-system-i386 -m 512 -vga std -drive file=*windows_disk_image*,if=virtio

```

**Nota:** Si encuentra la pantalla azul de Death, asegúrese de no olvidar el parámetro `-m` y de que no arranca con virtio en lugar de ide para la unidad del sistema antes de instalar los controladores.

#### Controladores de red

La instalación de los controladores de red virtio es un poco más fácil, simplemente agregue el argumento `-net` como se explicó anteriormente.

```
$ qemu-system-i386 -m 512 -vga std -drive file=*windows_disk_image*,if=virtio -net nic,model=virtio -cdrom virtio-win-0.1-74.iso

```

Windows detectará el adaptador de red y tratará de encontrar un controlador para ello. Si falla, vaya al *Administrador de dispositivos*, localice el adaptador de red con un icono de signo de exclamación (debe estar abierto), haga clic en *Actualizar controlador* y seleccione el CD-ROM virtual. No olvide seleccionar la casilla de verificación que dice que debe buscar directorios recursivamente.

### Preparación de FreeBSD como invitado

Instale el puerto `emulators/virtio-kmod` si está utilizando FreeBSD 8.3 o posterior hasta 10.0-CURRENT donde están incluidos en el kernel. Después de la instalación, añada lo siguiente a su archivo `/boot/loader.conf`:

```
virtio_loader="YES"
virtio_pci_load="YES"
virtio_blk_load="YES"
if_vtnet_load="YES"
virtio_balloon_load="YES"

```

A continuación, modifique su `/etc/fstab` haciendo lo siguiente:

```
sed -i bak "s/ada/vtbd/g" /etc/fstab

```

Y verificar que `/etc/fstab` es consistente. Si algo sale mal, sólo arranque en un CD de rescate y copie `/etc/fstab.bak` de vuelta a `/etc/fstab`.

## Consejos y trucos

### Inicio de las máquinas virtuales QEMU en el arranque

#### Con libvirt

Si se configura una máquina virtual con [libvirt](/index.php/Libvirt "Libvirt"), se puede configurar a través de la interfaz gráfica de usuario de virt-manager para iniciar en el arranque de host, accediendo a las Opciones de arranque de la máquina virtual y seleccionando "Inicio de la máquina virtual en el arranque del host".

#### Script personalizado

Para ejecutar QEMU VMs al arrancar, puede usar las siguientes unidades systemd y config.

 `/etc/systemd/system/qemu@.service` 
```
[Unit]
Description=QEMU virtual machine

[Service]
Environment="type=system-x86_64" "haltcmd=kill -INT $MAINPID"
EnvironmentFile=/etc/conf.d/qemu.d/%i
ExecStart=/usr/bin/env qemu-${type} -name %i -nographic $args
ExecStop=/bin/sh -c ${haltcmd}
TimeoutStopSec=30
KillMode=none

[Install]
WantedBy=multi-user.target

```

{{Nota| De acuerdo con `systemd.service (5)` y `systemd.kill (5)` man, es necesario utilizar `KillMode=none` opción. De lo contrario, el proceso qemu principal se eliminará inmediatamente después de que se cierre el comando `ExecStop` (simplemente hace eco de una cadena) y su sistema de búsqueda no podrá apagarse correctamente.

A continuación, cree archivos de configuración por-VM, denominados `/etc/conf.d/qemu.d/*vm_name*`, con las siguientes variables establecidas:

	type

	QEMU binary to call. If specified, will be prepended with `/usr/bin/qemu-` and that binary will be used to start the VM. I.e. you can boot e.g. `qemu-system-arm` images with `type="system-arm"`.

	args

	QEMU command line to start with. Will always be prepended with `-name ${vm} -nographic`.

	haltcmd

	Command to shut down a VM safely. I am using `-monitor telnet:..` and power off my VMs via ACPI by sending `system_powerdown` to monitor. You can use SSH or some other ways.

Ejemplo de configuración:

 `/etc/conf.d/qemu.d/one` 
```
type="system-x86_64"

args="-enable-kvm -m 512 -hda /dev/mapper/vg0-vm1 -net nic,macaddr=DE:AD:BE:EF:E0:00 \
 -net tap,ifname=tap0 -serial telnet:localhost:7000,server,nowait,nodelay \
 -monitor telnet:localhost:7100,server,nowait,nodelay -vnc :0"

haltcmd="echo 'system_powerdown' | nc localhost 7100" # or netcat/ncat

# You can use other ways to shut down your VM correctly
#haltcmd="ssh powermanager@vm1 sudo poweroff"

```
 `/etc/conf.d/qemu.d/two` 
```
args="-enable-kvm -m 512 -hda /srv/kvm/vm2.img -net nic,macaddr=DE:AD:BE:EF:E0:01 \
 -net tap,ifname=tap1 -serial telnet:localhost:7001,server,nowait,nodelay \
 -monitor telnet:localhost:7101,server,nowait,nodelay -vnc :1"

haltcmd="echo 'system_powerdown' | nc localhost 7101"

```

Para establecer qué máquinas virtuales se iniciarán al arrancar, habilite la unidad de [systemd](/index.php/Systemd "Systemd") `qemu@*vm_name*.service`.

### Integración del ratón

Para evitar que el ratón sea agarrado al hacer clic en la ventana del sistema operativo invitado, agregue la opción `-usbdevice tablet`. Esto significa que QEMU puede reportar la posición del ratón sin tener que agarrar el ratón. Esto también anula la emulación de ratón PS/2 cuando se activa. Por ejemplo:

```
$ qemu-system-i386 -hda *disk_image* -m 512 -vga std -usbdevice tablet

```

If that does not work, try the tip at [#El cursor del ratón está nervioso o errático](#El_cursor_del_rat.C3.B3n_est.C3.A1_nervioso_o_err.C3.A1tico).

### Dispositivo USB del host de paso

Para acceder al dispositivo físico USB conectado al host desde la VM, puede utilizar la opción: `-usbdevice host:*vendor_id*:*product_id*`.

Puedes encontrar `vendor_id` y `product_id` de tu dispositivo con el comando `lsusb`.

Puesto que el chipset I440FX por defecto emulado por qemu cuentan con un solo controlador UHCI (USB 1), la opción `-usbdevice` intentará conectar su dispositivo físico a él. En algunos casos esto puede causar problemas con los dispositivos más nuevos. Una posible solución es emular el chipset [ICH9](http://wiki.qemu.org/Features/Q35), que ofrece un controlador EHCI que soporta hasta 12 dispositivos, usando la opción `-machine type=q35`.

Una solución menos invasiva es emular un controlador EHCI (USB 2) o XHCI (USB 3) con la opción `-device usb-ehci, id = ehci` o `-device nec -usb-xhci, id=xhci` respectivamente y luego adjuntar su dispositivo físico con la opción `-device usb-host,..` como sigue:

```
-device usb-host,bus=**controller_id**.0,vendorid=0x**vendor_id**,productid=0x**product_id**

```

También puede agregar la configuración `..., port =*<n>*` a la opción anterior para especificar en qué puerto físico del controlador virtual que desea conectar su dispositivo, útil en El caso que desea agregar varios dispositivos usb a la VM.

{{Nota|Si encuentra errores de permisos al ejecutar QEMU, consulte [Udev#Writing udev rules](/index.php/Udev#Writing_udev_rules "Udev") para obtener información sobre cómo establecer permisos del dispositivo.

### Habilitar KSM

Kernel Samepage Merging (KSM) es una característica del kernel de Linux que permite que una aplicación se registre con el kernel para que sus páginas se combinen con otros procesos que también se registren para que sus páginas se fusionen. El mecanismo KSM permite a las máquinas virtuales invitadas compartir páginas entre sí. En un entorno donde muchos de los sistemas operativos invitados son similares, esto puede resultar en ahorros significativos de memoria.

Para activar KSM, simplemente ejecute:

```
# echo 1 > /sys/kernel/mm/ksm/run

```

Para hacerlo permanente, puede utilizar [archivos temporales de systemd](/index.php/Systemd#Temporary_files "Systemd"):

 `/etc/tmpfiles.d/ksm.conf` 
```
w /sys/kernel/mm/ksm/run - - - - 1

```

Si KSM está en ejecución y hay páginas que se van a fusionar (es decir, al menos dos máquinas virtuales similares se están ejecutando), entonces `/sys/kernel/mm/ksm/pages_shared` debería ser distinto de cero. Consulte [https://www.kernel.org/doc/Documentation/vm/ksm.txt](https://www.kernel.org/doc/Documentation/vm/ksm.txt) para obtener más información.

**Sugerencia:** Una manera fácil de ver lo bien que KSM está realizando es simplemente imprimir el contenido de todos los archivos de ese directorio: `$ grep./Sys/kernel/mm/ksm/*` 

### Multi-monitor support

El controlador QXL de Linux soporta cuatro cabezas (pantallas virtuales) de forma predeterminada. Esto se puede cambiar a través del parámetro kernel `qxl.heads = N`.

El tamaño de memoria VGA predeterminado para los dispositivos QXL es de 16M (el tamaño de la VRAM es de 64M). Esto no es suficiente si desea habilitar dos monitores 1920x1200 ya que requiere 2 × 1920 × 4 (profundidad de color) × 1200 = 17.6 MiB memoria VGA. Esto se puede cambiar reemplazando `-vga qxl` por`
**Template error:** are you trying to use the = sign? Visit [Help:Template#Escape template-breaking characters](/index.php/Help:Template#Escape_template-breaking_characters "Help:Template") for workarounds.
`. Si alguna vez incrementas vgamem_mb más allá de 64M, también debes aumentar la opción `vram_size_mb`.

### Copiar y pegar

Para poder copiar y pegar entre el host y el invitado, debe habilitar el canal de comunicación del agente de especias. Requiere agregar un dispositivo virtio-serial al huésped, y abrir un puerto para el vdagent de la especia. También es necesario instalar el spice vdagent en invitado ([spice-vdagent](https://www.archlinux.org/packages/?name=spice-vdagent) para invitados de Arch, [Herramientas para invitados de Windows](http://www.spice-space.org/download.html) para invitados de Windows). Asegúrese de que el agente se está ejecutando (y para el futuro, se iniciará automáticamente).

Inicie QEMU con las siguientes opciones:

```
$ qemu-system-i386 -vga qxl -spice port=5930,disable-ticketing -device virtio-serial-pci -device virtserialport,chardev=spicechannel0,name=com.redhat.spice.0 -chardev spicevmc,id=spicechannel0,name=vdagent

```

La opción `-device virtio-serial-pci` añade el dispositivo virtio-serial, `-device virtserialport, chardev=spicechannel0, nombre=com.redhat.spice.0` abre un puerto Para spice vdagent en ese dispositivo y `-chardev spicevmc, id=spicechannel0, nombre=vdagent` añade un spicevmc chardev para ese puerto.

Es importante que la opción `chardev=` del dispositivo `virtserialport` coincida con la opción `id=` dada a la opción `chardev` (`spicechannel0` en este ejemplo). También es importante que el nombre del puerto sea `com.redhat.spice.0`, ya que es el espacio de nombres donde vdagent está buscando en el invitado. Y finalmente, especifique `name=vdagent` para que spice sepa para qué sirve este canal.

### Notas específicas de Windows

QEMU puede ejecutar cualquier versión de Windows desde Windows 95 a través de Windows 10.

Es posible ejecutar [Windows PE](/index.php/Windows_PE "Windows PE") en QEMU.

#### Inicio rápido

**Nota:** Se requiere una cuenta de administrador para cambiar la configuración de energía.

Para invitados de Windows 8 (o posteriores), es mejor desactivar "Activar inicio rápido (recomendado)" en Opciones de energía del Panel de control, ya que hace que el invitado se bloquee durante cada arranque.

El inicio rápido también puede necesitar deshabilitarse para que los cambios en la opción `-smp` se apliquen correctamente.

#### Protocolo de escritorio remoto

Si utiliza un invitado de MS Windows, puede utilizar RDP para conectarse a su VM invitada. Si está utilizando una VLAN o no está en la misma red que el invitado, utilice:

```
$ qemu-system-i386 -nographic -net user,hostfwd=tcp::5555-:3389

```

A continuación, conéctese con [rdesktop](https://www.archlinux.org/packages/?name=rdesktop) ó [freerdp](https://www.archlinux.org/packages/?name=freerdp) al invitado. Por ejemplo:

```
$ xfreerdp -g 2048x1152 localhost:5555 -z -x lan

```

## Solución de problemas

### La máquina virtual virtual corre muy lento

Hay algunas técnicas que se pueden usar para implementar rendimiento en la máquina virtual, por ejemplo:

*   Use la opción `-cpu host` para hacer que QEMU emule la CPU del host. Si no se hace esto, podría intentar emular un CPU más genérico.
*   Especialmente para los invitados de Windows, habilite [Iluminaciones de Hyper-V](http://blog.wikichoon.com/2014/07/enabling-hyper-v-enlightenments-with-kvm.html): `-Host de la CPU, hv_relaxed, hv_spinlocks=0x1fff, hv_vapic, hv_time`.
*   Si la máquina host tiene varias CPUs, asigne al invitado más CPUs usando la opción `-smp`.
*   Asegúrese de haber asignado a la máquina virtual suficiente memoria. De forma predeterminada, QEMU sólo asigna 128 MiB de memoria a cada máquina virtual. Utilice la opción `-m` para asignar más memoria. Por ejemplo, `-m 1024` ejecuta una máquina virtual con 1024 MiB de memoria.
*   Utilice KVM si es posible: agregue `-machine type=pc, accel=kvm` al comando de arranque QEMU que utilice.
*   Si es compatible con los controladores del sistema operativo invitado, utilice [virtio](http://wiki.libvirt.org/page/Virtio) para dispositivos de red y/o bloque. Por ejemplo:

```
$ qemu-system-i386 -net nic, model=virtio -net tap, if=tap0, script=no-drive file=*disk_image*,media=disco, if=virtio

```

*   Utilizar dispositivos TAP en lugar de redes en modo usuario. Consulte [#Tap de red con QEMU](#Tap_de_red_con_QEMU).
*   Si el sistema operativo invitado está haciendo escritura pesada en su disco, puede beneficiarse de ciertas opciones de montaje en el sistema de archivos del host. Por ejemplo, puede montar un [sistema de archivos ext4](/index.php/Ext4 "Ext4") con la opción `barrier=0`. Debe leer la documentación de las opciones que cambie porque a veces las opciones de mejora de rendimiento para los sistemas de archivos tienen el costo de integridad de los datos.
*   Si tiene una imagen de disco sin procesar, puede deshabilitar la caché:

```
$ qemu-system-i386 -drive file=*disk_image*, if=virtio, cache=none

```

*   Utilice el nativo Linux AIO:

```
$ qemu-system-i386 -drive file=*disk_image*, if=virtio, aio=native

```

*   Si utiliza una imagen de disco qcow2, el rendimiento de E/S se puede mejorar considerablemente al garantizar que el caché L2 es de tamaño suficiente. La fórmula [[4]](https://blogs.igalia.com/berto/2015/12/17/improving-disk-io-performance-in-qemu-2-5-with-the-qcow2-l2-cache/) para calcular La caché L2 es: l2_cache_size = disk_size * 8 / cluster_size. Suponiendo que la imagen qcow2 se creó con el tamaño de clúster predeterminado de 64 K, esto significa que para cada 8 GB de tamaño de la imagen qcow2, 1 MB de caché L2 es mejor para el rendimiento. QEMU utiliza sólo 1 MB por defecto; Especificar una caché más grande se hace en la línea de comandos QEMU. Por ejemplo, para especificar 4 MB de caché (adecuado para un disco de 32 GB con un tamaño de clúster de 64 KB):

```
$ qemu-system-i386 -drive file=*disk_image*,format=qcow2, l2-cache-size=4M

```

*   Si está ejecutando varias máquinas virtuales al mismo tiempo que todas tienen el mismo sistema operativo instalado, puede ahorrar memoria al habilitar [kernel de la misma página de fusión](https://en.wikipedia.org/wiki/Kernel_SamePage_Merging_(KSM) "wikipedia:Kernel SamePage Merging (KSM)"). Consulte [#Habilitar KSM](#Habilitar_KSM).
*   En algunos casos, la memoria se puede recuperar de correr máquinas virtuales ejecutando un controlador de globo de memoria en el sistema operativo invitado y lanzando QEMU con la opción `-balloon virtio`.
*   Es posible utilizar una capa de emulación para un controlador ICH-9 AHCI (aunque puede ser inestable). La emulación AHCI soporta [[Wikipedia: Native_Command_Queuing] NCQ], por lo que varias peticiones de lectura o escritura pueden estar pendientes al mismo tiempo:

```
$ qemu-system-i386 -drive id=disc, file=*disk_image*, if=none -device ich9-ahci, id=ahci -device ide-drive, drive=disk, bus=ahci.0

```

Mira [http://www.linux-kvm.org/page/Tuning_KVM](http://www.linux-kvm.org/page/Tuning_KVM) para más información.

### El cursor del ratón está nervioso o errático

Si el cursor "brinca" descontroladamente, podría ayudar ingresar este comando en la terminal antes de iniciar QEMU

```
$ export SDL_VIDEO_X11_DGAMOUSE=0

```

Si funciono, puedes agregarlo a tu `~/.bashrc` archivo.

### El cursor no es visible

Añade `-show-cursor` a las opciones de QEMU para poder ver el cursor.

Si persiste, asegurate de configurar la pantalla apropiadamente

Por ejemplo: `-vga qxl`

### No se puede mover / adjuntar el cursor

Reemplaza `-usbdevice tablet` con `-usb` como opción en QEMU.

### El teclado parece roto ó las teclas de flecha no funcionan

Probablemente notarás que algunas de tus teclas no funcionan ó "presionan" la tecla equivocada (en particular, las flechas), preferentemente, necesitas especificar la distribución de tu teclado como una opción. La distribución del teclado puede encontrarse en `/usr/share/qemu/keymaps`.

```
$ qemu-system-i386 -k *keymap* *disk_image*

```

### Pantalla de invitado estirada en el tamaño de la ventana

Para restarurar el tamaño por defecto de la ventanta, presiona `Ctrl+Alt+u`.

### ioctl(KVM_CREATE_VM) failed: 16 Device or resource busy

Si un mensaje de error como este es listado en el arranque de QUEMU con la opción `-enable-kvm`:

```
ioctl(KVM_CREATE_VM) failed: 16 Device or resource busy
failed to initialize KVM: Device or resource busy

```

Significa que otro [hypervisor](/index.php/Hypervisor "Hypervisor") está actualmente activo. No se recomienda ó no es poible correr varios hypervisores en paralelo.

### Mensaje de error libgfapi

El mensaje de error listado en el arranque:

```
Failed to open module: libgfapi.so.0: cannot open shared object file: No such file or directory

```

No es un problema, sólo significa que hace falta la dependencia opcional de GlusterFS

### Kernel panic en entornos live

Si inicia un sistema en vivo (ó bootea uno) podría encontrar esto:

```
end Kernel panic - not syncing: VFS: Unable to mount root fs on unknown block(0,0)

```

Ó algún otro proceso de arranque (ej. no se puede desempaquetar initramfs, no puede iniciar un servicio foo).

Intente iniciar la Máquina Virtual con el `-m VALOR` switch y un tamaño apropiado de RAM, si la RAM es muy poca probablemente encontrará problemas similares a los anteriores.

## Ver también

*   [Sitio web oficial de QEMU](http://qemu.org)
*   [Sitio web oficial de KVM](http://www.linux-kvm.org)
*   [Documentación para el usuario del emulador QEMU](http://qemu.weilnetz.de/qemu-doc.html) (en inglés)
*   [Wikilibro de QEMU](https://en.wikibooks.org/wiki/QEMU) (en inglés)
*   [[http://alien.slackbook.org/dokuwiki/doku.php?id=slackware:qemu](http://alien.slackbook.org/dokuwiki/doku.php?id=slackware:qemu) Virtualización de hardware con QEMU por AlienBOB (última actualización en 2008) (en inglés)
*   [Construyendo un ejército virtual](http://blog.falconindy.com/articles/build-a-virtual-army.html) por Falconindy (en inglés)
*   [Últimos documentos](http://git.qemu.org/?p=qemu.git;a=tree;f=docs)
*   [QEMU en Windows](http://qemu.weilnetz.de/)
*   [Wikipedia](https://en.wikipedia.org/wiki/Qemu "wikipedia:Qemu")
*   [QEMU - Wiki de Debian](https://wiki.debian.org/QEMU) (en inglés)
*   [QEMU Networking on gnome.org](https://people.gnome.org/~markmc/qemu-networking.html)
*   [Red virtual de QEMU en sistemas BSD](http://bsdwiki.reedmedia.net/wiki/networking_qemu_virtual_bsd_systems.html) (en inglés)
*   [QEMU on gnu.org](https://www.gnu.org/software/hurd/hurd/running/qemu.html)
*   [QEMU en FreeBSD como host](https://wiki.freebsd.org/qemu) (en inglés)