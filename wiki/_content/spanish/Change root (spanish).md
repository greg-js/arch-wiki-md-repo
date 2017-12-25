Artículos relacionados

*   [Install bundled 32-bit system in Arch64](/index.php/Install_bundled_32-bit_system_in_Arch64 "Install bundled 32-bit system in Arch64")
*   [PRoot](/index.php/PRoot "PRoot")
*   [systemd-nspawn](/index.php/Systemd-nspawn "Systemd-nspawn")

[Chroot](https://en.wikipedia.org/wiki/Chroot "wikipedia:Chroot") es el proceso por el que se cambia el directorio root del disco aparente (y el actual proceso en marcha y sus descendientes) a otro directorio root. Al cambiar a otro directorio root no se puede acceder a los archivos y órdenes fuera de ese directorio. Este directorio se llama *jaula chroot*. El cambio de root se hace comúnmente para el mantenimiento del sistema, como puede ser volver a instalar el gestor de arranque o restablecer una contraseña olvidada.

## Contents

*   [1 Requisitos](#Requisitos)
*   [2 Montar las particiones](#Montar_las_particiones)
*   [3 Cambiar root](#Cambiar_root)
    *   [3.1 Usando arch-chroot](#Usando_arch-chroot)
    *   [3.2 Usando chroot](#Usando_chroot)
    *   [3.3 Usando systemd-nspawn](#Usando_systemd-nspawn)
*   [4 Ejecutar aplicaciones gráficas en entornos chroot](#Ejecutar_aplicaciones_gr.C3.A1ficas_en_entornos_chroot)
*   [5 Realizar el mantenimiento del sistema](#Realizar_el_mantenimiento_del_sistema)
*   [6 Salir del entorno chroot](#Salir_del_entorno_chroot)
*   [7 Ejemplo](#Ejemplo)
*   [8 Véase también](#V.C3.A9ase_tambi.C3.A9n)

## Requisitos

*   Tendrá que arrancar desde otro entorno Linux para funcionar (por ejemplo, desde un LiveCD o un medio flash USB, o desde otra distribución Linux instalada).

*   Se requieren privilegios de root con el fin de efectuar chroot.

*   Asegúrese de que la arquitectura del entorno de Linux que haya arrancado coincide con la arquitectura del directorio root que desea introducir (es decir, i686, x86_64). Puede encontrar la arquitectura de su entorno actual con la orden:

	 `# uname -m` 

*   Si necesita algún módulo del kernel cargado en el entorno chroot, cárguelos antes de efectuar el cambio de root. Dichos módulos pueden ser útiles para inicializar la partición de intercambio (`swapon /dev/sdxY`) y para establecer una conexión a Internet antes de efectuar chroot.

## Montar las particiones

La partición root del sistema Linux, donde se está tratando de efectuar chroot, necesita estar montada previamente. Para saber el nombre asignado por el kernel a dicha partición, ejecute:

```
# lsblk /dev/sda

```

También puede ejecutar la siguiente orden para tener una idea de la distribución de las particiones.

```
# fdisk -l

```

Ahora cree un directorio (por ejemplo, arch) en el que desee montar la partición root (por ejemplo, la partición sda3) y móntela:

```
# mkdir /mnt/arch                 # crea el directorio
# mount /dev/sda3 /mnt/arch       # monta la partición root

```

A continuación, si tiene particiones separadas para otras partes del sistema (por ejemplo, `/boot`, `/home`, `/var`, etc.), debe montarlas, de este modo:

```
# mount /dev/sda1 /mnt/arch/boot/
# mount /dev/sdb5 /mnt/arch/home/
# mount ...

```

Si bien es posible montar sistemas de archivos después de efectuar chroot, es más conveniente hacerlo antes. La razón de esto es que se tendrán que desmontar los sistemas de archivos creados temporalmente después de salir de la jaula, así que este procedimiento le permite desmontar todos los sistemas de archivos con una sola orden. Por otro lado, esto también permite un cierre más seguro. Debido a que el entorno de Linux externo conoce todas las particiones montadas, puede desmontarlas con seguridad durante el apagado.

## Cambiar root

### Usando arch-chroot

El script `arch-chroot` es parte del paquete [arch-install-scripts](https://www.archlinux.org/packages/?name=arch-install-scripts) de los [[Official repositories (Español)]|repositorios oficiales]. El script monta los sistemas de archivos de la API como `/proc` y pone disponible al chroot `/etc/resolv.conf` antes de ejecutar `/usr/bin/chroot`.

Ejecute arch-chroot con el nuevo directorio raíz como primer argumento:

```
# arch-chroot /mnt/arch

```

Para usar la shell bash en vez de sh usado por defecto:

```
# arch-chroot /mnt/arch /bin/bash

```

Para ejecutar `mkinitcpio -p linux` desde el chroot y salir inmediatamente:

```
# arch-chroot /mnt/arch /usr/bin/mkinitcpio -p linux

```

### Usando chroot

Monte los sistemas de archivos temporales:

```
# cd /mnt/arch
# mount -t proc proc proc/
# mount -t sysfs sys sys/
# mount -o bind /dev dev/
# mount -t devpts pts dev/pts/

```

Si se establece una conexión a Internet y desea utilizarla en el entorno chroot, puede que tenga que copiar sus servidores DNS para que se conecten a la red:

```
# cp -L /etc/resolv.conf etc/resolv.conf

```

Ahora efectúe chroot en el sistema instalado y defina la shell:

```
# chroot /mnt/arch /usr/bin/bash

```

**Nota:**

*   Si ve el error `chroot: cannot run command '/bin/bash': Exec format error`, es probable que las dos arquitecturas no coincidan.
*   Si ve el error `chroot: '/usr/bin/bash': permission denied`, vuelva a montar con el permiso exec: `mount -o remount,exec /mnt/arch`.

De manera opcional, para suministrar una configuración propia a Bash (`~/.bashrc` y `/etc/bash.bashrc`), ejecute:

```
# source ~/.bashrc
# source /etc/profile

```

**Tip:** Opcionalmente también, cree un prompt único capaz de diferenciar el entorno chroot: `# export PS1="(chroot) $PS1"` 

### Usando systemd-nspawn

Como alternativa, puede usar `systemd-nspawn` para lograr lo mismo, con beneficios adicionales (ver la página del manual de «systemd-nspawn»).

Los pasos son muy similares:

*   Primero monte la partición `root`:

```
# mkdir /mnt/arch
# mount /dev/sdx3 /mnt/arch

```

*   A continuación, monte las particiones `boot` y `home` en la partición root:

```
# mount /dev/sdx1 /mnt/arch/boot
# mount /dev/sdx4 /mnt/arch/home

```

*   Luego, basta con hacer `cd` en la partición root y ejecutar systemd-nspawn:

```
# cd /mnt/arch
# systemd-nspawn

```

Como puede ver, no hay necesidad de preocuparse por montar `proc`, `sys`, `dev` o `dev/pts`. `systemd-nspawn` inicia un proceso init nuevo en el entorno creado, que se encarga de todo. Es como arrancar un segundo sistema operativo Linux en la misma máquina, pero que no se comporta como una máquina virtual.

Para salir, simplemente cierre la sesión o ejecute la orden `poweroff`. A continuación, puede desmontar las particiones como se ha descrito anteriormente (sin tener que preocuparse de proc, sys, etc).

## Ejecutar aplicaciones gráficas en entornos chroot

Si tiene [X](/index.php/Xorg_(Espa%C3%B1ol) "Xorg (Español)") ejecutándose en el sistema, puede iniciar aplicaciones gráficas desde el entorno chroot.

Para permitir la conexión a un servidor X en un entorno chroot, abra un terminal dentro del servidor X (es decir, dentro del escritorio del usuario donde se ha iniciado actualmente sesión), y, a continuación, ejecute la siguiente orden que concede permisos a cualquiera para conectarse al servidor X del usuario:

```
$ xhost +

```

Después, para dirigir las aplicaciones al servidor X desde el entorno chroot, establezca la variable de entorno del DISPLAY dentro del entorno chroot, para que coincida con la variable del DISPLAY del usuario al que pertenece el servidor X. Así, por ejemplo, ejecute:

```
$ echo $DISPLAY

```

como el usuario que es propietario del servidor X para ver el valor de DISPLAY. Si el valor es Y. If the value is ":0" (por ejemplo), entonces en el entorno chroot ejecute:

```
# export DISPLAY=:0

```

Ahora puede iniciar aplicaciones gráficas desde la línea de órdenes del entorno chroot.

## Realizar el mantenimiento del sistema

En este punto puede realizar cualquier mantenimiento del sistema que necesite dentro del entorno chroot. Algunos ejemplos comunes son:

*   Volver a instalar el gestor de arranque.
*   Reconstruir la imagen [initramfs](/index.php/Mkinitcpio_(Espa%C3%B1ol) "Mkinitcpio (Español)").
*   Actualizar o realizar [downgrade](/index.php/Downgrading_packages "Downgrading packages") de paquetes.
*   Restablecer una [contraseña olvidada](/index.php/Password_recovery "Password recovery").

## Salir del entorno chroot

Cuando haya terminado con el mantenimiento del sistema, salga de chroot:

```
# exit

```

A continuación, desmonte los sistemas de archivos temporales y los dispositivos montados:

```
# umount {proc,sys,dev,boot,[...],}

```

Por último, desmonte la partición root:

```
# cd ..
# umount arch/

```

**Nota:** Si obtiene un error diciendo que `/mnt` (o cualquier otra partición) está ocupada, esto puede significar una de estas dos cosas:

*   Que un programa ha quedado ejecutándose dentro del entorno chroot.

*   O, más normalmente, que un submontaje todavía existe (por ejemplo, `/mnt/arch/boot` en `/mnt/arch`). Compruebe, con la orden `lsblk`, si hay puntos de montaje pendientes:

	 `lsblk /dev/sda` 

	Si aún sigue sin poder desmontar una partición, use la opción `--force`:

	 `# umount -f /mnt` 

Después de esto, será capaz de reiniciar el sistema de forma segura.

## Ejemplo

Esto puede proteger su sistema contra ataques desde Internet durante la navegación:

```
# # as root: 
# cd /home/*user*
# mkdir myroot
# pacman -S arch-install-scripts
# # pacstrap must see myroot as mounted: 
# mount --bind myroot myroot
# pacstrap -i myroot base base-devel
# mount -t proc proc myroot/proc/
# mount -t sysfs sys myroot/sys/
# mount -o bind /dev myroot/dev/
# mount -t devpts pts myroot/dev/pts/
# cp -i /etc/resolv.conf myroot/etc/
# chroot myroot
# # inside chroot: 
# passwd # set a password 
# useradd -m -s /bin/bash *user*
# passwd *user* # set a password
# # in a shell outside the chroot: 
# pacman -S xorg-server-xnest
# # in a shell outside the chroot you can run this as *user*: 
$ Xnest -ac -geometry 1024x716+0+0 :1
# # continue inside the chroot: 
# pacman -S xterm
# DISPLAY=:1
# xterm
# # xterm is now running in Xnest 
# pacman -S xorg-server xorg-xinit xorg-server-utils
# pacman -S openbox
# # for java we need icedtea-web which requires some fonts: 
# nano /etc/locale.gen
# # uncomment en_US.UTF-8 UTF-8, save and exit 
# locale-gen
# echo LANG=en_US.UTF-8 > /etc/locale.conf
# export LANG=en_US.UTF-8
# pacman -S ttf-dejavu
# pacman -S icedtea-web
# pacman -S firefox
# firefox
# # firefox is now running in Xnest 
# exit
# # outside chroot: 
# chroot --userspec=*user* myroot
# # inside chroot as *user*: 
$ DISPLAY=:1
$ openbox &
$ HOME="/home/*user*"
$ firefox
```

## Véase también

*   [systemd-nspawn](/index.php/Systemd-nspawn "Systemd-nspawn")
*   [Basic Chroot](https://help.ubuntu.com/community/BasicChroot)