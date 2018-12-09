Tareas en GNU/Linux

**Estado de la traducción**
Este artículo es una traducción de [VirtualBox/Tips and tricks](/index.php/VirtualBox/Tips_and_tricks "VirtualBox/Tips and tricks"), revisada por última vez el **018-11-09**. Si advierte que la versión inglesa [ha cambiado](https://wiki.archlinux.org/index.php?title=VirtualBox/Tips_and_tricks&diff=0&oldid=553747) puede ayudar a actualizar la traducción, bien por [usted mismo](/index.php/ArchWiki:Translation_Team/Contributing_(Espa%C3%B1ol) "ArchWiki:Translation Team/Contributing (Español)") o bien avisando al [equipo de traducción](/index.php/ArchWiki:Translation_Team_(Espa%C3%B1ol) "ArchWiki:Translation Team (Español)").

Véase [VirtualBox (Español)](/index.php/VirtualBox_(Espa%C3%B1ol) "VirtualBox (Español)") para el artículo principal.

## Contents

*   [1 Importar/exportar máquinas virtuales de VirtualBox a/desde otros hipervisores](#Importar/exportar_máquinas_virtuales_de_VirtualBox_a/desde_otros_hipervisores)
    *   [1.1 Eliminar complementos](#Eliminar_complementos)
    *   [1.2 Utilizar el formato adecuado de disco virtual](#Utilizar_el_formato_adecuado_de_disco_virtual)
        *   [1.2.1 Herramientas de automatización](#Herramientas_de_automatización)
        *   [1.2.2 Conversión manual](#Conversión_manual)
    *   [1.3 Crear la configuración de la maquina virtual para su hipervisor](#Crear_la_configuración_de_la_maquina_virtual_para_su_hipervisor)
*   [2 Gestionar el lanzamiento de la máquina virtual](#Gestionar_el_lanzamiento_de_la_máquina_virtual)
    *   [2.1 Iniciar máquinas virtuales con un servicio](#Iniciar_máquinas_virtuales_con_un_servicio)
    *   [2.2 Iniciar máquinas virtuales con un atajo del teclado](#Iniciar_máquinas_virtuales_con_un_atajo_del_teclado)
*   [3 Utilizar dispositivos específicos en la máquina virtual](#Utilizar_dispositivos_específicos_en_la_máquina_virtual)
    *   [3.1 Utilizar webcam / micrófono USB](#Utilizar_webcam_/_micrófono_USB)
    *   [3.2 Detectar cámaras web y otros dispositivos USB](#Detectar_cámaras_web_y_otros_dispositivos_USB)
*   [4 Acceder a un servidor huésped](#Acceder_a_un_servidor_huésped)
*   [5 Aceleración D3D en huéspedes Windows](#Aceleración_D3D_en_huéspedes_Windows)
*   [6 VirtualBox en una llave USB](#VirtualBox_en_una_llave_USB)
*   [7 Ejecutar una instalación nativa de Arch Linux dentro de VirtualBox](#Ejecutar_una_instalación_nativa_de_Arch_Linux_dentro_de_VirtualBox)
    *   [7.1 Asegurarse de que se tiene un esquema de nombres persistentes](#Asegurarse_de_que_se_tiene_un_esquema_de_nombres_persistentes)
    *   [7.2 Asegurarse de que su imagen mkinitcpio es correcta](#Asegurarse_de_que_su_imagen_mkinitcpio_es_correcta)
    *   [7.3 Crear una configuración de máquina virtual para arrancar desde la unidad física](#Crear_una_configuración_de_máquina_virtual_para_arrancar_desde_la_unidad_física)
        *   [7.3.1 Crear una imagen .vmdk de disco raw](#Crear_una_imagen_.vmdk_de_disco_raw)
        *   [7.3.2 Crear el archivo de configuración de la máquina virtual](#Crear_el_archivo_de_configuración_de_la_máquina_virtual)
*   [8 Instalar un sistema nativo de Arch Linux desde VirtualBox](#Instalar_un_sistema_nativo_de_Arch_Linux_desde_VirtualBox)
*   [9 Mover una instalación nativa de Windows a una máquina virtual](#Mover_una_instalación_nativa_de_Windows_a_una_máquina_virtual)
    *   [9.1 Tareas en Windows](#Tareas_en_Windows)
    *   [9.2 Using Disk2vhd to clone Windows partition](#Using_Disk2vhd_to_clone_Windows_partition)
    *   [9.3 Tareas en GNU/Linux](#Tareas_en_GNU/Linux)
    *   [9.4 Arreglar el MBR y el gestor de arranque de Microsoft](#Arreglar_el_MBR_y_el_gestor_de_arranque_de_Microsoft)
    *   [9.5 Limitaciones conocidas](#Limitaciones_conocidas)
*   [10 Ejecutar una partición de Windows en VirtualBox](#Ejecutar_una_partición_de_Windows_en_VirtualBox)
    *   [10.1 Configurar udev para dar acceso sin formato a VirtualBox a las particiones de Windows](#Configurar_udev_para_dar_acceso_sin_formato_a_VirtualBox_a_las_particiones_de_Windows)
    *   [10.2 Configuración de VirtualBox](#Configuración_de_VirtualBox)
        *   [10.2.1 Crear archivos de imagen de disco virtual](#Crear_archivos_de_imagen_de_disco_virtual)
        *   [10.2.2 Adjuntar imágenes de disco virtual a la máquina virtual](#Adjuntar_imágenes_de_disco_virtual_a_la_máquina_virtual)
    *   [10.3 Configurar una ESP por separado en VirtualBox](#Configurar_una_ESP_por_separado_en_VirtualBox)
    *   [10.4 Configurar el firmware UEFI virtual para usar el cargador de arranque de Windows](#Configurar_el_firmware_UEFI_virtual_para_usar_el_cargador_de_arranque_de_Windows)

## Importar/exportar máquinas virtuales de VirtualBox a/desde otros hipervisores

Si planea utilizar su máquina virtual en otro [hipervisor](https://en.wikipedia.org/wiki/es:Hipervisor "wikipedia:es:Hipervisor") o quiere importar en VirtualBox una máquina virtual creada con otro hipervisor, quizás podría estar interesado en la lectura de los siguientes pasos.

### Eliminar complementos

Los complementos para el sistema huésped están disponibles en la mayoría de las soluciones de los hipervisores: VirtualBox cuenta con Guest Additions, VMware con VMware Tools, Parallels con Parallels Tools, etc. Estos componentes adicionales están diseñados para ser instalados en una máquina virtual después de que el sistema operativo huésped haya sido instalado. Se componen de controladores de dispositivos y aplicaciones del sistema que optimizan el sistema operativo invitado para un mejor rendimiento y usabilidad [proporcionando estas características](https://www.virtualbox.org/manual/ch04.html).

Si ha instalado los complementos en su máquina virtual, desinstálelos primero. Su huésped, especialmente si está usando un sistema operativo de la familia Windows, podría comportarse extrañamente, romperse o, incluso, puede que no arranque en absoluto si todavía se están utilizando los controladores específicos de otro hipervisor.

### Utilizar el formato adecuado de disco virtual

Este paso dependerá de la capacidad de convertir la imagen de disco virtual directamente o no.

#### Herramientas de automatización

Algunos proveedores ofrecen herramientas que dan la posibilidad de crear máquinas virtuales desde un sistema operativo Windows o GNU/Linux ya se encuentre en una máquina virtual o, incluso, en una instalación nativa. Con este tipo de producto, no es necesario aplicar este y los siguientes pasos y puede dejar de leer aquí.

*   *[Parallels Transporter](http://www.parallels.com/products/transporter)* no es gratis, es un producto de Parallels Inc. Esta solución consiste, básicamente, en una pieza de software llamada *agent* que será instalado en el sistema huésped que desee importar/convertir. A continuación, Parallels Transporter, <u>que solo funciona en OS X</u>, creará una máquina virtual conectada a través de *agent* bien por USB o por conexión de red cableada.
*   *[VMware vCenter Converter](https://www.vmware.com/products/converter/)* es gratuita, previa inscripción en el sitio web de VMware, funciona casi de la misma manera que Parallels Transporter, con la particularidad de que la pieza de software que hará recopilar los datos para crear la máquina virtual solo funciona en una plataforma Windows.

#### Conversión manual

En primer lugar, familiarícese con [los formatos soportados por VirtualBox](/index.php/VirtualBox_(Espa%C3%B1ol)#Formatos_soportados_por_VirtualBox "VirtualBox (Español)") y [los formatos soportados por otros hipervisores](https://en.wikipedia.org/wiki/Comparison_of_platform_virtual_machines#Image_type_compatibility "wikipedia:Comparison of platform virtual machines").

*   La importación o exportación de una máquina virtual a/desde VMware no es un problema en absoluto si utiliza el formato de disco VMDK o OVF, convirtiendo [VirtualBox (Español)#VMDK a VDI y VDI a VMDK](/index.php/VirtualBox_(Espa%C3%B1ol)#VMDK_a_VDI_y_VDI_a_VMDK "VirtualBox (Español)") si es posible y tiene disponible la mencionada herramienta VMware vCenter de conversión.

*   La importación o exportación de una máquina virtual a/desde QEMU no es ningún problema: algunos formatos de QEMU tienen soporte directamente en VirtualBox y la conversión entre [VirtualBox (Español)#QCOW2 a VDI y VDI a QCOW2](/index.php/VirtualBox_(Espa%C3%B1ol)#QCOW2_a_VDI_y_VDI_a_QCOW2 "VirtualBox (Español)") la tenemos disponible si es necesario.

*   La importación o exportación de una máquina virtual a/desde Parallels es el camino más difícil: solo soporta su propio formato HDD (incluso el formato estándar y portable OVF no está soportado).

*   Para exportar la máquina virtual Parallels, tendrá que utilizar la herramienta de Parallels Transporter descrita anteriormente.
*   Para importar a VirtualBox, tendrá que usar VMware vCenter Converter descrito anteriormente para convertir la máquina virtual al formato VMware primero. Luego, tendrá que aplicar la solución para migrar desde VMware.

### Crear la configuración de la maquina virtual para su hipervisor

Cada hipervisor tiene su propio archivo de configuración de máquina virtual: `.vbox` para VirtualBox, `.vmx` para VMware, un archivo `config.pvs` ubicado en el paquete de la máquina virtual (archivo `.pvm`), etc. De este modo, tendrá que recrear una nueva máquina virtual en su nuevo hipervisor de destino y especificar su configuración de hardware tan precisa como sea posible, de modo similar a como se hizo en su máquina virtual inicial.

Preste especial atención a la interfaz del firmware (BIOS o UEFI) utilizado para instalar el sistema operativo huésped. Mientras que existe una opción disponible para elegir entre estas 2 interfaces en VirtualBox y Parallels, en VMware, en cambio, tendrá que añadir manualmente la siguiente línea a su archivo *.vmx*.

 `ArchLinux_vm.vmx`  `firmware = "efi"` 

Por último, indique a su hipervisor el disco virtual a utilizar que ha convertido y lance la máquina virtual.

**Sugerencia:**

*   En VirtualBox, si no desea navegar por la interfaz gráfica de usuario para encontrar la ubicación adecuada para agregar el nuevo dispositivo de disco virtual, puede [VirtualBox (Español)#Reemplazar un disco virtual de forma manual desde el archivo .vbox](/index.php/VirtualBox_(Espa%C3%B1ol)#Reemplazar_un_disco_virtual_de_forma_manual_desde_el_archivo_.vbox "VirtualBox (Español)"), o utilizar `VBoxManage storageattach` descrito en [#Aumentar discos virtuales](#Aumentar_discos_virtuales) o en la [página del manual de VirtualBox](https://www.virtualbox.org/manual/ch08.html#vboxmanage-storageattach).
*   Del mismo modo, en los productos de VMware, puede reemplazar el lugar de la ubicación actual del disco virtual adaptando la ubicación del archivo *.vmdk* en su archivo de configuración *.vmx*

## Gestionar el lanzamiento de la máquina virtual

### Iniciar máquinas virtuales con un servicio

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
ExecStart=/usr/bin/VBoxManage startvm %i --type *startmode*
ExecStop=/usr/bin/VBoxManage controlvm %i *stopmode*
RemainAfterExit=yes

[Install]
WantedBy=multi-user.target
```

**Nota:**

*   Reemplace `*username*` con un usuario que sea miembro del grupo `vboxusers`. Asegúrese de que el usuario elegido es el mismo usuario que creará/importará las máquinas virtuales, de lo contrario el usuario no verá las aplicaciones de la máquina virtual.
*   Reemplace `*startmode*` con un tipo de frontend de máquina virtual, generalmente `gui`, `headless` o `separate`
*   Reemplace `*stopmode*` con el alternador de estado deseado, generalmente `savestate` or `acpipowerbutton`

**Nota:** si tiene varias máquinas virtuales gestionadas por systemd y las mismas no se detienen correctamente, pruebe añadiendo `RemainAfterExit=true` y `KillMode=none` al final de la sección `[Service]`.

[Active](/index.php/Enable "Enable") la unidad `vboxvmservice@*your_virtual_machine_name*` para lanzar la máquina virtual en el próximo reinicio. Para lanzar directamente la máquina virtual, basta con [iniciar](/index.php/Start "Start") la unidad de systemd.

VirtualBox 4.2 introduce [una nueva forma](http://lifeofageekadmin.com/how-to-set-your-virtualbox-vm-to-automatically-startup/) para que sistemas tipo UNIX tengan máquinas virtuales que se inicien automáticamente, distinto al uso de un servicio systemd.

### Iniciar máquinas virtuales con un atajo del teclado

Puede ser útil comenzar máquinas virtuales directamente con un atajo de teclado en lugar de utilizar la interfaz de VirtualBox (GUI o CLI). Para ello, solo tiene que definir combinaciones de teclas en `.xbindkeysrc`. Remítase a [Xbindkeys](/index.php/Xbindkeys "Xbindkeys") para más detalles.

He aquí un ejemplo, usando la tecla `Fn` del portatil con una tecla no utilizada (`F3` utilizada en este ejemplo):

```
"VBoxManage startvm 'Windows 7'"
m:0x0 + c:244
XF86Battery

```

**Nota:** Si se tiene un espacio en el nombre de la máquina virtual, entonces se encierra entre comillas simples, como se ha hecho en el ejemplo que acabamos de poner.

## Utilizar dispositivos específicos en la máquina virtual

### Utilizar webcam / micrófono USB

**Nota:** Necesita tener el paquete de extensiones de VirtualBox instalado antes de seguir los pasos de abajo. Vea la sección [VirtualBox (Español)#Paquete de extensiones](/index.php/VirtualBox_(Espa%C3%B1ol)#Paquete_de_extensiones "VirtualBox (Español)") para más detalles.

1.  Asegúrese de que la máquina virtual no está en funcionamiento y no se está utilizando la webcam / micrófono.
2.  Haga que aparezca la ventana principal de VirtualBox y vaya a la configuración de la máquina de Arch. Navegue hasta la sección USB.
3.  Asegúrese de que está seleccionado «Enable USB Controller». Asegúrese también de que está seleccionado «Enable USB 2.0 (EHCI) Controller».
4.  Haga clic en el botón «Add filter from device» (el cable con el icono '+').
5.  Seleccione el dispositivo de cámara web/micrófono USB de la lista.
6.  Ahora, haga clic en Aceptar e inicie su máquina virtual.

**Nota:** si su micrófono no aparece en el menú «Agregar filtro desde dispositivo», pruebe las opciones USB 3.0 y 1.1 en su lugar (en el Paso 3.

### Detectar cámaras web y otros dispositivos USB

**Note:** Esto no servirá de mucho si está ejecutando un sistema operativo *NIX dentro de su máquina virtual, ya que la mayoría no tiene funciones de detección automática.

Si el dispositivo que está buscando no aparece en ninguno de los menús en la sección anterior y ha probado las tres opciones de controlador USB, arranque su máquina virtual tres veces separadamente. Una vez usando el controlador USB 1.1, otro usando el controlador USB 2.0, etc. Deje que la máquina virtual se ejecute durante al menos 5 minutos después del inicio. A veces Windows detectará automáticamente el dispositivo. Asegúrese de filtrar cualquier dispositivo que no sea un teclado o un mouse para que no se inicien en el arranque. Esto asegura que Windows detectará el dispositivo en el inicio.

## Acceder a un servidor huésped

Para acceder a un [servidor Apache](https://en.wikipedia.org/wiki/es:Servidor_HTTP_Apache "wikipedia:es:Servidor HTTP Apache") en una máquina virtual de un **solo** equipo anfitrión, basta con ejecutar la siguientes líneas en el equipo anfitrión:

```
$ VBoxManage setextradata GuestName "VBoxInternal/Devices/*pcnet*/0/LUN#0/Config/Apache/HostPort" *8888*
$ VBoxManage setextradata GuestName "VBoxInternal/Devices/*pcnet*/0/LUN#0/Config/Apache/GuestPort" *80*
$ VBoxManage setextradata GuestName "VBoxInternal/Devices/*pcnet*/0/LUN#0/Config/Apache/Protocol" TCP

```

Donde 8888 es el puerto por el que el equipo anfitrión debe escuchar y el 80 es el puerto por el que la máquina virtual enviará la señal al servidor Apache.

Para utilizar un puerto inferior a 1024 en el equipo anfitrión, los cambios tienen que ser reflejados en el cortafuegos de la máquina anfitriona. Esto también puede ser configurado para trabajar con SSH o con cualquier otro servicio cambiando «Apache» para los servicios y puertos correspondientes.

**Nota:** `pcnet` se refiere a la tarjeta de red de la máquina virtual. Si utiliza una tarjeta de Intel en la configuración de la máquina virtual, cambie `pcnet` a `e1000`.

To communicate between the VirtualBox guest and host using ssh, the server port must be forwarded under Settings > Network. When connecting from the client/host, connect to the IP address of the client/host machine, as opposed to the connection of the other machine. This is because the connection will be made over a virtual adapter.

## Aceleración D3D en huéspedes Windows

Las versiones recientes de Virtualbox tienen soporte para la aceleración OpenGL dentro de los sistemas huéspedes. Esto se puede activar marcando una simple casilla en la configuración del equipo, justo debajo de donde se establece la memoria RAM de vídeo y la instalación de las aplicaciones del sistema huésped en VirtualBox. Sin embargo, la mayoría de los juegos de Windows utilizan Direct3D (parte de DirectX), no OpenGL, y, por lo tanto, no son ayudados por este método. No obstante, es posible obtener la aceleración Direct3D en los sistemas huéspedes Windows mediante préstamos de las bibliotecas D3D de wine, que traducen d3d a OpenGL, permitiendo la aceleración. Estas bibliotecas son ahora parte del software *guest additions* de Virtualbox.

Después de activar la aceleración OpenGL como se describió anteriormente, reinicie el sistema huésped en modo seguro (presione F8 antes de que aparezca la pantalla de Windows, pero después de que desaparezca la pantalla de Virtualbox), e instale las *guest additions* de Virtualbox, durante la instalación active la casilla «Direct3D support». Reinicie en modo normal y ya debería tener aceleración Direct3D.

**Nota:** este truco puede o no funcionar para algunos juegos en función de las comprobaciones que se haga del hardware y qué partes de D3D se utilice.

**Nota:** esto fue probado en Windows XP, 7 y 8,1\. Si el método no funciona en su versión de Windows, por favor agregue los datos aquí.

## VirtualBox en una llave USB

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

## Ejecutar una instalación nativa de Arch Linux dentro de VirtualBox

Si tiene un sistema de arranque dual entre Arch Linux y otro sistema operativo, puede resultar sumamente tedioso tener que alternar entre uno y otro para trabajar. Por otro lado, mediante el uso de máquinas virtuales, solo se dispone de un pequeño fragmento de energía del equipo, que puede causar problemas cuando se trabaja en proyectos de cierta envergadura.

Esta guía le permitirá utilizar, en una máquina virtual, la instalación nativa de Arch Linux cuando se está ejecutando el segundo sistema operativo. De esta forma, mantendrá la capacidad de ejecutar cada sistema operativo de forma nativa, pero con la opción de ejecutar la instalación de Arch Linux en una máquina virtual.

### Asegurarse de que se tiene un esquema de nombres persistentes

Dependiendo de la configuración del disco duro, la representación de los archivos de los dispositivos del disco duro pueden aparecer de forma diferente cuando se ejecuta la instalación de Arch Linux de forma nativa o en la máquina virtual. Este problema se produce cuando se utiliza [FakeRAID](/index.php/RAID_(Espa%C3%B1ol)#Implementación "RAID (Español)") por ejemplo. El dispositivo FakeRAID vendrá asignado como `/dev/mapper/` al ejecutar la distribución GNU/Linux de forma nativa, al tiempo que los demás dispositivos siguen siendo accesibles por separado. Sin embargo, en su máquina virtual, puede aparecer sin ningún mapeo como `/dev/sdaX` por ejemplo, porque los controladores que controlan el FakeRAID en su sistema operativo anfitrión (por ejemplo, Windows) se abstraerán del dispositivo FakeRAID.

Para evitar este problema, tendremos que utilizar un esquema de direccionamiento que sea persistente en ambos sistemas. Esto se puede lograr usando [UUID](/index.php/Fstab_(Espa%C3%B1ol)#UUID "Fstab (Español)") en su archivo `/etc/fstab`. Asegúrese de que su archivo [fstab (Español)](/index.php/Fstab_(Espa%C3%B1ol) "Fstab (Español)") utiliza UUID para solucionar este problema. Lea [fstab (Español)](/index.php/Fstab_(Espa%C3%B1ol) "Fstab (Español)") y [Persistent block device naming (Español)](/index.php/Persistent_block_device_naming_(Espa%C3%B1ol) "Persistent block device naming (Español)").

**Advertencia:**

*   Asegúrese de que su partición anfitriona solo es accesible en modo solo lectura desde su máquina virtual Arch Linux, esto evitará el riesgo de corrupción si estando en la partición anfitriona escribe en ella por descuido.
*   NUNCA debe permitir que VirtualBox arranque desde la entrada de su segundo sistema operativo, que, a modo de recordatorio, es usado como anfitrión de esta máquina virtual. Preste especial cuidado en colocar la entrada de su otro sistema operativo por defecto en su gestor de arranque. De un mayor margen de espera o póngalo debajo en el orden de preferencias.

### Asegurarse de que su imagen mkinitcpio es correcta

Asegúrese de que la configuración de su [mkinitcpio](/index.php/Mkinitcpio_(Espa%C3%B1ol) "Mkinitcpio (Español)") utiliza el [HOOK](/index.php/Mkinitcpio_(Espa%C3%B1ol)#HOOKS "Mkinitcpio (Español)") `block`:

 `/etc/mkinitcpio.conf` 
```
[...]
HOOKS="base udev autodetect modconf *block* filesystems keyboard fsck"
[...]
```

Si no está presente, añádalo y regenere su initramfs con la orden `# mkinitcpio -p linux`, cuyo [uso se describe aquí con detalle](/index.php/Mkinitcpio_(Espa%C3%B1ol)#Creación_de_la_imagen_y_activación "Mkinitcpio (Español)").

### Crear una configuración de máquina virtual para arrancar desde la unidad física

#### Crear una imagen .vmdk de disco raw

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

#### Crear el archivo de configuración de la máquina virtual

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

Por último, es posible que desee una integración perfecta entre su sistema Arch Linux y su sistema operativo anfitrión, permitiendo la función de pegar y copiar entre ambos sistemas operativos. Por favor, consulte [VirtualBox (Español)#Instalar complementos para el sistema huésped](/index.php/VirtualBox_(Espa%C3%B1ol)#Instalar_complementos_para_el_sistema_huésped "VirtualBox (Español)") ya que, no debemos olvidar que esta máquina virtual de Arch Linux no deja de ser un sistema huésped cuando se ejecuta sobre el otro sistema operativo.

**Advertencia:** Para que [Xorg](/index.php/Xorg_(Espa%C3%B1ol) "Xorg (Español)") pueda funcionar tanto en forma nativa como en la máquina virtual, dado que va a utilizar diferentes controladores en uno u otro entorno, la mejor opción es que no exista un archivo `/etc/X11/xorg.conf`, de modo que se deje a Xorg que recoja todo lo que necesita sobre la marcha. Sin embargo, si realmente necesita su propia configuración Xorg, tal vez valga la pena establecer su target predefinido de systemd a `multi-user.target` con `# systemctl isolate graphical.target` (más detalles en [Systemd (Español)#Tabla de targets](/index.php/Systemd_(Espa%C3%B1ol)#Tabla_de_targets "Systemd (Español)")y [Systemd (Español)#Cambiar el target vigente](/index.php/Systemd_(Espa%C3%B1ol)#Cambiar_el_target_vigente "Systemd (Español)"). De este modo, la interfaz gráfica estará desactivada (es decir Xorg no se pondrá en marcha) y, después de iniciar sesión, podrá ejecutar `startx` manualmente con un archivo `xorg.conf` personalizado.

## Instalar un sistema nativo de Arch Linux desde VirtualBox

En algunos casos, puede ser útil instalar un sistema nativo de Linux Arch mientras se ejecuta otro sistema operativo: una forma de lograr esto es realizar la instalación a través de VirtualBox en un [disco raw](http://www.virtualbox.org/manual/ch09.html#rawdisk). Si el sistema operativo existente está basado en Linux, es posible que desee considerar el siguiente artículo [Install from existing Linux (Español)](/index.php/Install_from_existing_Linux_(Espa%C3%B1ol) "Install from existing Linux (Español)") en su lugar.

Este escenario es muy similar a la [#Ejecutar una instalación nativa de Arch Linux dentro de VirtualBox](#Ejecutar_una_instalación_nativa_de_Arch_Linux_dentro_de_VirtualBox), pero seguirá los pasos en un orden diferente: empiece por [#Crear una imagen .vmdk de disco raw](#Crear_una_imagen_.vmdk_de_disco_raw), y luego [#Crear el archivo de configuración de la máquina virtual](#Crear_el_archivo_de_configuración_de_la_máquina_virtual).

Ahora, debe tener una configuración de máquina virtual funcional cuyos discos virtuales VMDK están ligados a un disco real. El proceso de instalación es exactamente lo mismo que el descrito en [VirtualBox (Español)#Pasos para preparar Arch Linux como sistema anfitrión](/index.php/VirtualBox_(Espa%C3%B1ol)#Pasos_para_preparar_Arch_Linux_como_sistema_anfitrión "VirtualBox (Español)"), pero [asegurándose de que tiene un esquema de nombres persistentes](/index.php/VirtualBox_(Espa%C3%B1ol)#Asegurarse_de_que_se_tiene_un_esquema_de_nombres_persistentes "VirtualBox (Español)") y [que su imagen mkinitcpio es correcta](#Asegurarse_de_que_su_imagen_mkinitcpio_es_correcta).

**Advertencia:**

*   Para los sistemas BIOS con un esquema de particionado MBR, no instale un gestor de arranque en su máquina virtual, esto no funcionará ya que el MBR no está vinculado con el MBR de su máquina real y su disco virtual solo se asignaŕa como una partición real sin MBR.
*   Para los sistemas UEFI sin [Compatibility Support Module (CSM)](https://en.wikipedia.org/wiki/Compatibility_Support_Module#CSM "wikipedia:Compatibility Support Module") y con esquema de particionado GPT, la instalación no funcionará en absoluto, dado que:

*   la partición [EFI System partition (ESP)](https://en.wikipedia.org/wiki/EFI_System_partition para más detalles);
*   y las variables efivars, si va a instalar Arch Linux usando el modo EFI por intermediación de VirtualBox, no se corresponden con la de su sistema real: por lo tanto, las entradas de su gestor de arranque no serán registradas.

*   Esta razones hacen recomendable crear, primero, las particiones en una instalación nativa, de lo contrario las particiones no serán tomadas en consideración en su tabla de particiones MBR/GPT.

Después de completar la instalación, arranque el ordenador con un soporte de instalación de GNU/Linux (ya se trate de Arch Linux o no), entre en entorno [chroot](/index.php/Installation_guide_(Espa%C3%B1ol)#Chroot "Installation guide (Español)") en su recién instalado Arch Linux e instale y configure un [gestor de arranque](/index.php/Arch_boot_process_(Espa%C3%B1ol)#Gestor_de_arranque "Arch boot process (Español)").

## Mover una instalación nativa de Windows a una máquina virtual

Si desea migrar una instalación de Windows nativa existente a una máquina virtual que se utilizará con VirtualBox en GNU/Linux, siga leyendo. Esta sección solo trata la instalación nativa de Windows utilizando el esquema de particiones MS-DOS/Intel. Su instalación de Windows debe residir en la primera partición del MBR para que esta operación tenga éxito. La operación también es posible en otras particiones, pero no ha sido probada (Consulte [#Limitaciones conocidas](#Limitaciones_conocidas) para conocer detalles).

**Advertencia:** Si está utilizando una versión OEM de Windows, este proceso no está autorizado por la licencia de usuario final. De hecho, la licencia OEM normalmente establece las instalación de Windows ligada al hardware específico del equipo donde se instala. Al transferir una instalación de Windows a una máquina virtual se elimina esa vinculación. Asegúrese de que tiene una instalación completa de Windows o un modelo de licencia por volumen antes de continuar. Si tiene una licencia completa de Windows, pero este último no viene en volumen, ni como una licencia especial para varios PC, esto significa que tendrá que quitar la instalación nativa después de que se haya logrado la operación de transferencia.

Se requiere un par de tareas a realizar en el interior de la instalación original de Windows primero, y luego en su sistema GNU/Linux anfitrión.

### Tareas en Windows

Los primeros tres siguientes puntos vienen de [esta página desactualizada de la wiki de VirtualBox](https://www.virtualbox.org/wiki/Migrate_Windows#HAL), pero se actualizan aquí.

*   Elimine los chequeos de las controladoras de IDE/ATA (solo en Windows XP): Windows memoriza las controladoras de disco IDE/ATA cuando se ha instalado y no arrancará si detecta que estos han cambiado. La solución propuesta por Microsoft es volver a utilizar la misma controladora o utilizar una de la misma serie, lo cual es imposible de lograr ya que estamos utilizando una máquina virtual. Se puede utilizar [MergeIDE](https://www.virtualbox.org/wiki/Migrate_Windows#HardDiskSupport), una herramienta alemana, desarrollada sobre la base de una solución propuesta por Microsoft. Esta solución consiste básicamente en tomar todos los controladores de la controladora ATA/IDE compatibles con Windows XP desde el archivo del controlador inicial (la ubicación está codificada, o especificada como el primer argumento del script `.bat`), instalándolos y registrándolos con la base de datos regedit.

*   Utilice el tipo Hardware Abstraction Layer (versiones de Windows de 32 bits viejas): Microsoft incluye 3 versiones por defecto: `Hal.dll` (Standard PC), `Halacpi.dll` (ACPI HAL) y `Halaacpi.dll` (ACPI HAL con IO APIC). Su instalación de Windows podría venir instalado con la primera o la segunda versión. Si es así [desactive la característica extendida *Enable IO/APIC* de VirtualBox](https://www.virtualbox.org/manual/ch08.html#idp56927888).

*   Desactive cualquier controlador del dispositivo AGP (solo versiones obsoletas de Windows): si tiene los archivos `agp440.sys` o `intelppm.sys` dentro de la carpeta `C:\Windows\SYSTEM32\drivers\` retírelos. Como VirtualBox utiliza una tarjeta gráfica PCI virtual, esto puede causar problemas cuando se utiliza este controlador AGP.

*   Crear un disco de recuperación de Windows: en los siguientes pasos, si la operación sale mal, tendrá que reparar la instalación de Windows. Asegúrese de tener un soporte de instalación a mano, o cree uno con la utilidad *Crear un disco de recuperación* de Windows.

### Using Disk2vhd to clone Windows partition

Boot into Windows, clean up the installation (with [CCleaner](http://www.piriform.com/ccleaner) for example), use [disk2vhd](https://technet.microsoft.com/en-us/library/ee656415.aspx) tool to create a VHD image. Include a reserved system partition (if present) and the actual Windows partition (usually disk C:). The size of Disk2vhd-created image will be the sum of the actual files on the partition (used space), not the size of a whole partition. If all goes well, the image should just boot in a VM and you will not have to go through the hassle with MBR and Windows bootloader, as in the case of cloning an entire partition.

### Tareas en GNU/Linux

**Tip:** Skip the partition-related parts if you created VHD image with [Disk2vhd](#Using_Disk2vhd_to_clone_Windows_partition).

*   Reduzca el tamaño de la partición donde tenga instalado Windows nativo al tamaño que Windows necesita realmente con `ntfsresize`, disponible en el paquete [ntfs-3g](https://www.archlinux.org/packages/?name=ntfs-3g). El tamaño que especifique será el mismo tamaño de la VDI que se creará en el siguiente paso. Si este tamaño es demasiado bajo, es posible romper su instalación de Windows y este último podría provocar que no arranque en absoluto.

	Utilice la opción `--no-action` primero para realizar una prueba:

	 `# ntfsresize --no-action --size *52Gi* */dev/sda1*` 

	Si la prueba anterior tuvo éxito, ejecute la orden de nuevo, pero esta vez sin la opción antes mencionada.

*   Instale VirtualBox en su sistema anfitrión GNU/Linux (vea [#Pasos para preparar Arch Linux como sistema anfitrión](#Pasos_para_preparar_Arch_Linux_como_sistema_anfitrión) si su sistema anfitrión es Arch Linux).

*   Cree la imagen de disco de Windows desde el principio de la unidad hasta el final de la primera partición donde se encuentra la instalación de Windows. Es necesario copiar desde el principio del disco porque el espacio del MBR del principio de la unidad tiene que estar en la unidad virtual junto con la partición de Windows. En este ejemplo las dos siguientes particiones `sda2` y `sda3` serán eliminadas de la tabla de particiones y el gestor de arranque MBR será actualizado.

	 `# sectnum=$(( $(cat /sys/block/''sda/sda1''/start) + $(cat /sys/block/''sda/sda1''/size) ))` 

	El uso de `cat /sys/block/*sda/sda1*/size` mostrará el número de sectores totales de la primera partición del disco `sda`. Adaptar cuando sea necesario.

	 `# dd if=''/dev/sda'' bs=512 count=$sectnum | VBoxManage convertfromraw stdin ''windows.vdi'' $(( $sectnum * 512 ))` 

	Tenemos que obtener el tamaño en bytes, `$(( $sectnum * 512 ))` convertirá los números de sector a bytes.

*   Cree el archivo de configuración de la máquina virtual y utilice el disco virtual creado anteriormente como disco duro virtual principal. `# chown $USER:users windows.vdi`.

*   Trate de arrancar su maquina virtual de Windows, Debería funcionar sin más. Primero, sin embargo, retire y repare los discos desde el proceso de arranque, ya que pueden interferir (y probablemente lo hagan) arrancar en modo seguro.

*   Intente arrancar su máquina virtual Windows en modo seguro (pulse la tecla F8 antes de que el logotipo de Windows aparezca)... si se dan problemas de arranque, lea [#Arreglar el MBR y el gestor de arranque de Microsoft](#Arreglar_el_MBR_y_el_gestor_de_arranque_de_Microsoft). En modo seguro, los controladores se instalarán probablemente por el mecanismo de detección plug-and-play de Windows ([vistas](http://i.imgur.com/hh1RrSp.png)). Adicionalmente, instale los Guest Additions de VirtualBox a través del menú *Devices* > *Insert Guest Additions CD image...*. Si no aparece un nuevo diálogo para el disco, vaya a la unidad del CD e inicie el instalador manualmente.

*   Finalmente, debe tener una máquina virtual de Windows funcional. No se olvide de leer las [#Limitaciones conocidas](#Limitaciones_conocidas).

*   Performance tip: according to [VirtualBox manual](http://www.virtualbox.org/manual/ch05.html#harddiskcontrollers), SATA controller has a better performance than IDE. If you cannot boot Windows off virtual SATA controller right away, it is probably due to the lack of SATA drivers. Attach virtual disk to IDE controller, create an empty SATA controller and boot the VM - Windows should automatically install SATA drivers for the controller. You can then shutdown VM, detach virtual disk from IDE controller and attach it to SATA controller instead.

### Arreglar el MBR y el gestor de arranque de Microsoft

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

### Limitaciones conocidas

*   Su máquina virtual, a veces, puede colgarse y desbordar la memoria RAM, lo cual puede ser causado por controladores en conflicto todavía instalados en su máquina virtual Windows. ¡Buena suerte en encontrarlos!
*   El software adicional que espera un controlador dado puede, o bien estar el controlador desactivado/desinstalado, o bien el software necesita ser desinstalado primero respecto de los controladores que ya no están disponibles.
*   Su instalación de Windows debe residir en la primera partición para que el proceso anterior pueda funcionar. Si no se cumple este requisito, el proceso podría lograrse también, pero esto no ha sido probado. Para ello será necesario copiar el MBR y editarlo en formato hexadecimal (vea [VirtualBox: arrancar disco clonado](http://superuser.com/questions/237782/virtualbox-booting-cloned-disk/253417#253417)) lo cual requerirá arreglar la tabla de particiones, bien [manualmente](http://gparted.org/h2-fix-msdos-pt.php), o bien mediante la reparación de Windows con el disco de recuperación que creó en el paso anterior. Consideremos que nuestra instalación de Windows está en la segunda partición; vamos a copiar el MBR y, a continuación, la segunda partición en la que reside la imagen del disco. `VBoxManage convertfromraw` necesita saber el número total de bytes que se escribirán: calculados gracias al tamaño del MBR (el comienzo de la primera partición) más el tamaño de la segunda partición (Windows). `{ dd if=/dev/sda bs=512 count=$(cat /sys/block/sda/sda1/start) ; dd if=/dev/sda2 bs=512 count=$(cat /sys/block/sda/sda2/size) ; } | VBoxManage convertfromraw stdin windows.vdi $(( ($(cat /sys/block/sda/sda1/start) + $(cat /sys/block/sda/sda2/size)) * 512 ))`.

## Ejecutar una partición de Windows en VirtualBox

**Nota:** la técnica descrita en esta sección solo se aplica a los sistemas [UEFI](/index.php/UEFI "UEFI").

En algunos casos, es útil poder tener un [arranque dual con Windows](/index.php/Dual_boot_with_Windows "Dual boot with Windows") *y* acceder a la partición en una máquina virtual. Este proceso es significativamente diferente a la operación de [#Mover una instalación nativa de Windows a una máquina virtual](#Mover_una_instalación_nativa_de_Windows_a_una_máquina_virtual) en varios puntos

*   La partición de Windows no se copia a una imagen de disco virtual. En su lugar, se crea un archivo VMDK en bruto
*   Los cambios en la máquina virtual se reflejarán en la partición, y viceversa
*   Las licencias OEM aún deben estar satisfechas, ya que la partición de Windows se arranca directamente en el hardware

**Advertencia:** algunas de las órdenes utilizadas aquí pueden dañar la partición de Windows, la partición de Arch Linux o ambas. Tenga mucho cuidado al ejecutar órdenes y verifique que se estén ejecutando en el intérprete de órdenes correcto. Sería una buena idea tener preparada una copia de seguridad de todo el disco antes de comenzar este proceso.

**Sugerencia:** será útil tener disponible [Arch install ISO](https://www.archlinux.org/download/), ya que se usará para configurar la [EFI system partition (Español)](/index.php/EFI_system_partition_(Espa%C3%B1ol) "EFI system partition (Español)") en la máquina virtual. También vale la pena tener acceso a los soportes de instalación de Windows (como la [ISO de Windows 10](https://www.microsoft.com/en-us/software-download/windows10ISO)) en caso de que la partición de Windows esté dañada.

### Configurar udev para dar acceso sin formato a VirtualBox a las particiones de Windows

VirtualBox debe tener [acceso a disco sin formato](https://www.virtualbox.org/manual/ch09.html#rawdisk) para ejecutar una partición de Windows. Normalmente, esto requeriría que VirtualBox se ejecutara con privilegios de root completos, pero [udev (Español)](/index.php/Udev_(Espa%C3%B1ol) "Udev (Español)") se puede configurar para restringir el acceso a ciertas particiones. Una forma conveniente de hacer esto es asignar todas las particiones relacionadas con Windows al grupo *vboxusers*, lo que se puede hacer con las siguientes reglas de udev:

**Nota:** los UUID en estas reglas corresponden a [tipos de partición GPT](https://en.wikipedia.org/wiki/GUID_Partition_Table#Partition_type_GUIDs "wikipedia:GUID Partition Table") particulares. En este caso, los UUID corresponden a todas las particiones [Microsoft Reserved](https://en.wikipedia.org/wiki/Microsoft_Reserved_Partition "wikipedia:Microsoft Reserved Partition") (*msftres*) y [|Microsoft basic data](https://en.wikipedia.org/wiki/Microsoft_basic_data_partition "wikipedia:Microsoft basic data partition") (*msftdata*).
 `/etc/udev/rules.d/99-vbox.rules` 
```
# Rules to give VirtualBox users raw access to Windows partitions

# Microsoft Reserved partitions (msftres)
SUBSYSTEM=="block", ENV{ID_PART_ENTRY_TYPE}=="e3c9e316-0b5c-4db8-817d-f92df00215ae", GROUP="vboxusers"

# Windows partitions (msftdata)
SUBSYSTEM=="block", ENV{ID_PART_ENTRY_TYPE}=="ebd0a0a2-b9e5-4433-87c0-68b6b72699c7", GROUP="vboxusers"

```

**Sugerencia:** se pueden encontrar variables y atributos útiles del entorno udev correspondientes a una partición en particular ejecutando `udevadm info /dev/*sdXX*`.

### Configuración de VirtualBox

Una máquina virtual de VirtualBox se puede crear manualmente con una configuración personalizada.

**Nota:** no agregue un disco virtual durante la creación inicial de la máquina virtual.

Configure la máquina virtual con la siguiente configuración:

*   Sistema
    *   Placa base
        *   *Activar E/S APIC*
        *   *Activar EFI*
        *   *Reloj de hardware en hora UTC*
    *   Aceleración
        *   Interfaz de Paravirtualización: *Hyper-V*
        *   *Activar VT-x / AMD-V*
        *   *Activar paginación anidada*
*   Pantalla > Screen > Aceleración
    *   *Activar aceleración 3D*
    *   *Activar aceleración 2D*
*   USB > *Activar controlador USB*

**Nota:** la configuración *Hyper-V* no es necesaria para que el sistema funcione correctamente, pero puede ayudar a evitar problemas de licencia.

#### Crear archivos de imagen de disco virtual

Para acceder a las particiones de Windows, cree un [archivo VMDK en bruto](https://www.virtualbox.org/manual/ch09.html#rawdisk) que apunte a las particiones de Windows relevantes y establezca la propiedad:

```
# vboxmanage internalcommands createrawvmdk -filename */path/to/vm/folder/windows.vmdk* -rawdisk /dev/*sdx* -partitions *res*,*data* -relative
# chown *user*:*group* */path/to/vm/folder/windows.vmdk*
```

**Nota:** al crear el archivo VMDK en bruto...

*   Acceda como root porque VirtualBox debe leer la tabla de particiones.
*   El parámetro `-rawdisk` debe apuntar a un dispositivo de bloque, no a una partición.
*   *res* es el número de partición de la partición reservada de Microsoft.
*   *data* es el número de partición de la partición de datos básicos de Microsoft (es decir, la instalación de Windows).
*   También se creará un archivo adicional (*windows-pt.vmdk*).
*   *windows.vmdk* tendrá que volver a crearse si se cambia la tabla de particiones.

Después de crear la imagen, cambie la propiedad para que el usuario/grupo deseado tenga acceso:

Para iniciar la máquina virtual en modo UEFI, se debe crear un disco virtual dedicado para la partición [EFI system partition (Español)](/index.php/EFI_system_partition_(Espa%C3%B1ol) "EFI system partition (Español)"):

 `$ vboxmanage createmedium disk --filename */path/to/vm/folder/esp.vmdk* --size 512 --format VMDK` 

#### Adjuntar imágenes de disco virtual a la máquina virtual

### Configurar una ESP por separado en VirtualBox

### Configurar el firmware UEFI virtual para usar el cargador de arranque de Windows