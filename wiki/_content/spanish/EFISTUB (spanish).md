Artículos relacionados

*   [Arch boot process (Español)](/index.php/Arch_boot_process_(Espa%C3%B1ol) "Arch boot process (Español)")
*   [Boot loaders (Español)](/index.php/Boot_loaders_(Espa%C3%B1ol) "Boot loaders (Español)")
*   [Unified Extensible Firmware Interface (Español)](/index.php/Unified_Extensible_Firmware_Interface_(Espa%C3%B1ol) "Unified Extensible Firmware Interface (Español)")

**Advertencia:** Se ha notificado un error según el cual el arranque con EFISTUB puede fallar dependiendo de la versión del kernel y del modelo de placa base. Vea [[1]](https://bugs.archlinux.org/task/33745) y [[2]](https://bbs.archlinux.org/viewtopic.php?id=156670) para más información.

El kernel de Linux ([linux](https://www.archlinux.org/packages/?name=linux)>=3.3) admite arrancar con EFISTUB (EFI BOOT STUB). Esta característica permite que el firmware EFI cargue el kernel como un ejecutable EFI. La opción está activada de forma predeterminada en los kernels de Arch Linux o se puede activar mediante el establecimiento de la variable `CONFIG_EFI_STUB=y` en la configuración del kernel (vea [The EFI Boot Stub](https://www.kernel.org/doc/Documentation/efi-stub.txt) para más información).

Un kernel EFISTUB se puede arrancar directamente por una placa base UEFI o indirectamente usando un [gestor de arranque UEFI](/index.php/Boot_loaders_(Espa%C3%B1ol)#Gestores_de_arranque_solo_para_UEFI "Boot loaders (Español)"). Este último es recomendado si se tienen múltiples pares de kernel/initramfs y el menú de inicio UEFI de su placa base no es fácil de usar.

## Contents

*   [1 Configurar EFISTUB](#Configurar_EFISTUB)
    *   [1.1 Puntos de montajes de ESP alternativos](#Puntos_de_montajes_de_ESP_alternativos)
        *   [1.1.1 Utilizar systemd](#Utilizar_systemd)
        *   [1.1.2 Incron](#Incron)
        *   [1.1.3 Hook de mkinitcpio](#Hook_de_mkinitcpio)
        *   [1.1.4 Montar en bind](#Montar_en_bind)
*   [2 Arrancar EFISTUB](#Arrancar_EFISTUB)
    *   [2.1 Utilizar un gestor de arranque](#Utilizar_un_gestor_de_arranque)
    *   [2.2 Utilizar la shell de UEFI](#Utilizar_la_shell_de_UEFI)
    *   [2.3 Utilizar directamente UEFI (efibootmgr)](#Utilizar_directamente_UEFI_(efibootmgr))

## Configurar EFISTUB

Después de crear la [EFI System Partition](/index.php/Unified_Extensible_Firmware_Interface#EFI_System_Partition "Unified Extensible Firmware Interface"), debe elegir la forma en que se va a montar. La opción más sencilla es montarlo en `/boot`, ya que esto permite a pacman actualizar directamente el kernel que el firmware EFI leerá. Si opta por esta opción, continúe en [#Arrancar EFISTUB](#Arrancar_EFISTUB).

### Puntos de montajes de ESP alternativos

Si monta la partición del sistema EFI (ESP) en otro lugar (como `/boot/efi`), tendrá que copiar los archivos de /boot a esa ubicación (en adelante `$esp`).

```
# mkdir $esp/EFI/arch
# cp /boot/vmlinuz-linux $esp/EFI/arch/vmlinuz-arch.efi
# cp /boot/initramfs-linux.img $esp/EFI/arch/initramfs-arch.img
# cp /boot/initramfs-linux-fallback.img $esp/EFI/arch/initramfs-arch-fallback.img

```

Además, tendrá que mantener los archivos de ESP al día con las actualizaciones posteriores del kernel. De no hacerlo podría dar como resultado un sistema que no arranca. Las siguientes secciones ofrecen varios mecanismos para hacerlo.

#### Utilizar systemd

[Systemd (Español)](/index.php/Systemd_(Espa%C3%B1ol) "Systemd (Español)") tiene la facultad de realizar tareas tras desencadenarse un evento. En este caso particular, la capacidad de detectar un cambio en la ruta de acceso se puede utilizar para sincronizar el kernel EFISTUB y los archivos initramfs cuando se actualizan en `/boot`.

 `/etc/systemd/system/efistub-update.path` 
```
[Unit]
Description=Copiar Kernel EFISTUB a partición UEFISYS

[Path]
PathChanged=/boot/initramfs-linux-fallback.img

[Install]
WantedBy=multi-user.target

```

**Nota:** Este servicio observa a la imagen initramfs-linux-fallback.img para realizar los cambios, ya que dicha imagen es el último archivo compilado por mkinitcpio. Esto actúa como una condición para evitar una carrera potencial donde systemd podría copiar archivos antiguos antes de que se hayan compilado todos los archivos.
 `/etc/systemd/system/efistub-update.service` 
```
[Unit]
Description=Copiar Kernel EFISTUB a partición UEFISYS

[Service]
Type=oneshot
ExecStart=/usr/bin/cp -f /boot/vmlinuz-linux $esp/EFI/arch/vmlinuz-arch.efi
ExecStart=/usr/bin/cp -f /boot/initramfs-linux.img $esp/EFI/arch/initramfs-arch.img
ExecStart=/usr/bin/cp -f /boot/initramfs-linux-fallback.img $esp/EFI/arch/initramfs-arch-fallback.img

```

Activar estos servicios con:

```
# systemctl enable efistub-update.path

```

#### Incron

[incron](https://www.archlinux.org/packages/?name=incron) se puede utilizar para ejecutar un script de sincronización del Kernel EFISTUB después de las actualizaciones del kernel.

 `/usr/local/bin/efistub-update.sh` 
```
#!/usr/bin/env bash
/usr/bin/cp -f /boot/vmlinuz-linux $esp/EFI/arch/vmlinuz-arch.efi
/usr/bin/cp -f /boot/initramfs-linux.img $esp/EFI/arch/initramfs-arch.img
/usr/bin/cp -f /boot/initramfs-linux-fallback.img $esp/EFI/arch/initramfs-arch-fallback.img
```

**Nota:** El primer parámetro `/boot/initramfs-linux-fallback.img` es el archivo que debe tener en cuenta. El segundo parámetro `IN_CLOSE_WRITE` es la acción que debe observar. El tercer parámetro `/usr/local/bin/efistub-update.sh` es el script que debe ejecutar.
 `/etc/incron.d/efistub-update.conf`  `/boot/initramfs-linux-fallback.img IN_CLOSE_WRITE /usr/local/bin/efistub-update.sh` 

Para utilizar este método, active el servicio incrond:

```
# systemctl enable incrond.service

```

#### Hook de mkinitcpio

Mkinitcpio puede generar un hook que no necesita un demonio de nivel de sistema para funcionar. Se generará un proceso en segundo plano que espera a que se genere `vm-Linuz`, `initramfs-linux.img` y `initramfs-linux-fallback.img` antes de copiar los archivos.

Añada `efistub-update` a la lista de hooks en `/etc/mkinitcpio.conf`.

 `/usr/lib/initcpio/install/efistub-update` 
```
#!/usr/bin/env bash
build() {
	/root/watch.sh &
}

help() {
	cat <<HELPEOF
Este hook espera a que mkinitcpio termine y copia la imagen ramdiks y el kernel terminados a la ESP
HELPEOF
}
```
 `/root/watch.sh` 
```
#!/usr/bin/env bash

while [[ -d "/proc/$PPID" ]]; do
	sleep 1
done

/usr/bin/cp -f /boot/vmlinuz-linux $esp/EFI/arch/vmlinuz-arch.efi
/usr/bin/cp -f /boot/initramfs-linux.img $esp/EFI/arch/initramfs-arch.img
/usr/bin/cp -f /boot/initramfs-linux-fallback.img $esp/EFI/arch/initramfs-arch-fallback.img

echo "Kernel sincronizado con ESP"
```

#### Montar en bind

En lugar de montar la propia ESP en `/boot`, se puede montar un directorio de ESP en `/boot` usando un montaje con bind (véase `mount(8)`). Esto permite a pacman actualizar el kernel directamente, manteniendo la ESP organizada a su gusto. Si funciona en su caso, este método es mucho más simple que los otros enfoques que necesitan copiar los archivos.

**Nota:** Esto requiere un kernel y un gestor de arranque compatibles con FAT32\. Esto no es un problema para una instalación normal de Arch, pero podría ser problemático para otras distribuciones (a saber, las que requieren enlaces simbólicos en `/boot`). Post del foro [aquí](https://bbs.archlinux.org/viewtopic.php?pid=1331867#p1331867).

Como se hizo [anteriormente](#Alternative_ESP_Mount_Points), copie todos los archivos de /boot a un directorio en la ESP, pero monte ESP **fuera** de `/boot` (por ejemplo, `/esp`). A continuación, monte en bind el directorio:

```
# mount --bind /esp/EFI/arch/ /boot

```

Si sus archivos se muestran en `/boot` como desea, edite [Fstab (Español)](/index.php/Fstab_(Espa%C3%B1ol) "Fstab (Español)") para que esta operación sea permanente:

 `/etc/fstab` 
```
/esp/EFI/arch /boot none defaults,bind 0 0

```

**Advertencia:** *Debe* usar el [parámetro del kernel](/index.php/Kernel_parameters#Parameter_list "Kernel parameters") `root=*system_root*` para poder arrancar utilizando este método.

## Arrancar EFISTUB

**Advertencia:** La ruta a initramfs para EFISTUB debe ser relativa con respecto a la raiz de EFI System Partition. Por ejemplo, si initramfs se encuentra en `$esp/EFI/arch/initramfs-linux.img`, la línea correspondiente a UEFI debe ser `initrd=/EFI/arch/initramfs-linux.img` o `initrd=\EFI\arch\initramfs-linux.img`.

### Utilizar un gestor de arranque

Existen varios gestores de arranque UEFI que pueden proporcionar opciones adicionales o simplificar el proceso de arranque UEFI —especialmente si tiene múltiples kernels/sistemas operativos—. Vea [Boot loaders (Español)](/index.php/Boot_loaders_(Espa%C3%B1ol) "Boot loaders (Español)") para más información.

### Utilizar la shell de UEFI

Es posible lanzar un kernel EFISTUB desde la shell de UEFI como si fuera una aplicación normal UEFI. En este caso, los parámetros del kernel se pasan como parámetros normales al archivo del kernel EFISTUB lanzado.

```
> fs0:
> \EFI\arch\vmlinuz-linux root=PARTUUID=3518bb68-d01e-45c9-b973-0b5d918aae96 rootfstype=ext4 rw add_efi_memmap initrd=EFI/arch/initramfs-linux.img

```

Para evitar tener que recordar todos los parámetros del kernel una y otra vez, puede guardar la orden ejecutable como un script de shell (por ejemplo, como `archlinux.nsh`) en la partición del sistema UEFI, luego ejecútelo con:

```
> fs0:
> archlinux

```

### Utilizar directamente UEFI (efibootmgr)

UEFI está [diseñado para eliminar la necesidad](/index.php/UEFI#Multibooting_in_UEFI "UEFI") de tener un gestor de arranque intermedio como, por ejemplo, [GRUB (Español)](/index.php/GRUB_(Espa%C3%B1ol) "GRUB (Español)"). Si su placa base tiene una buena implementación UEFI, es posible incluir los parámetros del kernel dentro de una entrada de arranque UEFI para que la placa base arranque Arch directamente. Puede utilizar `efibootmgr` para modificar las entradas de arranque de su placa base para que incluya a Arch.

```
# efibootmgr -d /dev/sd**X** -p **Y** -c -L "Arch Linux" -l /vmlinuz-linux -u "root=**/dev/sda2** rw initrd=/initramfs-linux.img"

```

Donde `X` e `Y` se deben cambiar para reflejar el disco y la partición donde se encuentra la ESP. Cambie el parámetro `root=` para reflejar la raiz de Linux (la UUID del disco también puede ser utilizada). Es una buena idea ejecutar:

```
# efibootmgr -v

```

para verificar que la entrada resultante es correcta.

**Advertencia:** Algunas combinaciones de kernel y `efibootmgr` podrían negarse a crear nuevas entradas de inicio. Esto podría ser debido a la falta de espacio libre en la memoria NVRAM. Podría tratar de eliminar cualquier archivo de volcado de EFI:
```
# rm /sys/firmware/efi/efivars/dump-*

```
O, como último recurso, arrancar con el parámetro del kermel `efi_no_storage_paranoia`. Véase bug discussion [[3]](https://bugs.archlinux.org/task/34641) para más información.

Para establecer el orden de arranque, ejecute:

```
# efibootmgr -o XXXX,XXXX

```

donde XXXX es el número que aparece en la salida de la orden `efibootmgr` de cada entrada.

**Sugerencia:** Guarde la orden para crear su entrada de arranque en un script de shell en algún lugar, lo que hará que sea más fácil de modificar (al cambiar los parámetros del kernel, por ejemplo)
.

Más información sobre efibootmgr en [Unified Extensible Firmware Interface (Español)#efibootmgr](/index.php/Unified_Extensible_Firmware_Interface_(Espa%C3%B1ol)#efibootmgr "Unified Extensible Firmware Interface (Español)"). Post del foro: [https://bbs.archlinux.org/viewtopic.php?pid=1090040#p1090040](https://bbs.archlinux.org/viewtopic.php?pid=1090040#p1090040) .