Esto cubre la instalación de un segundo disco después de tener un sistema que ya esté corriendo con uno solo. Antes cerciórate de tener a salvo toda tu información (backup).

## Contents

*   [1 Disco primario: déjalo para conseguir la info y grabarlo. Utilicé cfdisk.](#Disco_primario:_déjalo_para_conseguir_la_info_y_grabarlo._Utilicé_cfdisk.)
*   [2 Disco secundario: instalación usando cfdisk.](#Disco_secundario:_instalación_usando_cfdisk.)
*   [3 Creamos los nodos md para los dispositivos:](#Creamos_los_nodos_md_para_los_dispositivos:)
*   [4 Creamos los dispositivos RAID](#Creamos_los_dispositivos_RAID)
*   [5 Chequea /proc/mdstat](#Chequea_/proc/mdstat)
*   [6 Creamos los sistemas de archivos que necesitemos utilizando las herramientas de creación.](#Creamos_los_sistemas_de_archivos_que_necesitemos_utilizando_las_herramientas_de_creación.)
*   [7 Montamos y copiamos la información.](#Montamos_y_copiamos_la_información.)
*   [8 Nota: PASO CRUCIAL](#Nota:_PASO_CRUCIAL)
*   [9 Instalar: vi /mnt/etc/fstab para el nuevo dispositivo md.](#Instalar:_vi_/mnt/etc/fstab_para_el_nuevo_dispositivo_md.)
*   [10 Ejecutamos chroot dentro del nuevo sistema RAID y reconstruimos initrd.](#Ejecutamos_chroot_dentro_del_nuevo_sistema_RAID_y_reconstruimos_initrd.)
*   [11 Instalamos GRUB en el nuevo RAID de discos, cambiando los números de acuerdo a la instalación.](#Instalamos_GRUB_en_el_nuevo_RAID_de_discos,_cambiando_los_números_de_acuerdo_a_la_instalación.)
*   [12 Chequeamos con mdstat](#Chequeamos_con_mdstat)
*   [13 Finalizamos la configuración de grub](#Finalizamos_la_configuración_de_grub)
*   [14 Finalizamos initrd.](#Finalizamos_initrd.)
*   [15 Cambiamos el orden de arranque en la BIOS nuevamente.](#Cambiamos_el_orden_de_arranque_en_la_BIOS_nuevamente.)

## Disco primario: déjalo para conseguir la info y grabarlo. Utilicé cfdisk.

Nota: no cambies cualquier cosa, solo presiona TAB para salir.

```
cfdisk /dev/<tu_antiguo_dispositivo>

```

```
disc1       Boot, NC    Primary   Linux ext2                          41.13 
disc2                   Primary   Linux swap / Solaris               271.44
disc3                   Primary   Linux ext3                       82030.72

```

## Disco secundario: instalación usando cfdisk.

```
cfdisk /dev/<tu_nuevo_dispositivo>

```

```
disc1       Boot        Primary   Linux raid autodetect               41.13 
disc2                   Primary   Linux raid autodetect              271.44
disc3                   Primary   Linux raid autodetect            82030.72
Hint --> Linux raid autodetect is type: FD

```

## Creamos los nodos md para los dispositivos:

```
mknod /dev/md0 b 9 0
mknod /dev/md1 b 9 1
mknod /dev/md2 b 9 2
mknod /dev/md3 b 9 3
...

```

## Creamos los dispositivos RAID

```
[root@svn ~]# mdadm --create /dev/md0 --level=1 --raid-devices=2 missing /dev/<yournewdevice-partitionA>
mdadm: array /dev/md0 started.
[root@svn ~]# mdadm --create /dev/md1 --level 1 --raid-devices=2 missing /dev/<yournewdevice-partitionB>
mdadm: array /dev/md1 started.
[root@svn ~]# mdadm --create /dev/md2 --level 1 --raid-devices=2 missing /dev/<yournewdevice-partitionC>
mdadm: array /dev/md2 started.
...
You may be asked: 'Continue creating array? y' if the disk was already formated.
[root@svn ~]#

```

## Chequea /proc/mdstat

Todos los dispositivos están intactos pero se degradan:

```
[root@svn ~]# cat /proc/mdstat 
Personalities : [linear] [raid0] [raid1] [raid5] [multipath] [raid6] [raid10] 
md2 : active raid1 sdb3[1]
     80108032 blocks [2/1] [_U]

md1 : active raid1 sdb2[1]
     264960 blocks [2/1] [_U]

md0 : active raid1 sdb1[1]
     40064 blocks [2/1] [_U]

unused devices: <none>
[root@svn ~]#

```

## Creamos los sistemas de archivos que necesitemos utilizando las herramientas de creación.

Nota: nuestro /boot es ext2, / es ext3.

```
[root@svn ~]# mke2fs -j /dev/md0
mke2fs 1.38 (30-Jun-2005)
Filesystem label=
OS type: Linux
Block size=1024 (log=0)
Fragment size=1024 (log=0)
10040 inodes, 40064 blocks
2003 blocks (5.00%) reserved for the super user
First data block=1
5 block groups
8192 blocks per group, 8192 fragments per group
2008 inodes per group
Superblock backups stored on blocks: 
       8193, 24577

```

```
Writing inode tables: done                            
Creating journal (4096 blocks): done
Writing superblocks and filesystem accounting information: done
This filesystem will be automatically checked every 35 mounts or
180 days, whichever comes first.  Use tune2fs -c or -i to override.

```

```
* mkswap
[root@svn ~]# mkswap /dev/md1   
Setting up swapspace version 1, size = 271314 kB
no label, UUID=9d746813-2d6b-4706-a56a-ecfd108f3fe9

```

```
* mkfs.ext3 for /
[root@svn ~]# mkfs.ext3 -j /dev/md2
mke2fs 1.38 (30-Jun-2005)
Filesystem label=
OS type: Linux
Block size=4096 (log=2)
Fragment size=4096 (log=2)
10027008 inodes, 20027008 blocks
1001350 blocks (5.00%) reserved for the super user
First data block=0
612 block groups
32768 blocks per group, 32768 fragments per group
16384 inodes per group
Superblock backups stored on blocks:
       32768, 98304, 163840, 229376, 294912, 819200, 884736, 1605632, 2654208, 
       4096000, 7962624, 11239424

```

```
Writing inode tables: done                            
Creating journal (32768 blocks): done
Writing superblocks and filesystem accounting information: done

```

```
This filesystem will be automatically checked every 25 mounts or
180 days, whichever comes first.  Use tune2fs -c or -i to override.
[root@svn ~]#

```

## Montamos y copiamos la información.

```
# mount new raid /
[root@svn ~]# mount /dev/md<where you assigned-/-number> /mnt/
# mount new raid /boot
[root@svn ~]# mkdir /mnt/boot
[root@svn ~]# mount /dev/md<where you assigned-/boot-number> /mnt/boot/
# add dirs and mount all other partitions
You need to do this for every partition you had on old disk, to create the new raid device exactly the same.
...
# copy / to new /raid/
[root@svn ~]# cd /mnt
[root@svn mnt]# tar -C / -clspf - . | tar -xlspvf - 
# copy /boot to new /raid/boot
cd /mnt/boot

```

[root@svn boot]# tar -C /boot -clspf - . | tar -xlspvf -

```
# copy other partitions
You need to do this for every partition you had on old disk, to create the new raid device exactly the same.
...

```

## Nota: PASO CRUCIAL

Editar /mnt/boot/grub/menu.lst Nota: debe parecerse a: Añadir "fallback 1" a menú.lst

```
----- snip -----
default   0
color light-blue/black light-cyan/blue

```

```
## fallback disc1
fallback 1

```

```
# (0) Arch Linux
title  Arch Linux  [Disc0: /boot/vmlinuz26]
root   (hd0,0)
#kernel /vmlinuz26 root=/dev/discs/disc0/part3 ro
kernel /vmlinuz26 root=/dev/md<where you assigned-/-number> 
md=<all your md devices, 
please refer mkinitcpio howto for correct syntax, 
but don't add the old disk partitions at this point> ro

```

```
# (1) Arch Linux
title  Arch Linux  [Disc1: /boot/vmlinuz26]
root   (hd1,0)
#kernel /vmlinuz26 root=/dev/discs/disc1/part3 ro
kernel /vmlinuz26 root=/dev/md<where you assigned-/-number> 
md=<all your md devices, 
please refer mkinitcpio howto for correct syntax,
but don't add the old disk partitions at this point> ro
----- snip -----

```

## Instalar: vi /mnt/etc/fstab para el nuevo dispositivo md.

Acabo de comentar las líneas hacia fuera.

```
#/dev/discs/disc0/part3 / ext3 defaults 0 1
/dev/md2 / ext3 defaults 0 1
#/dev/discs/disc0/part1 /boot ext2 defaults 0 1
/dev/md0 /boot ext2 defaults 0 1
#/dev/discs/disc0/part2 swap swap defaults 0 0
/dev/md1 swap swap defaults 0 0 

```

Montar /proc y /sys para el nuevo raid.

```
mount --bind /sys /mnt/sys
mound --bind /proc /mnt/proc

```

## Ejecutamos chroot dentro del nuevo sistema RAID y reconstruimos initrd.

```
chroot /mnt
# edit /etc/mkinitcpio.conf to include 'raid' in HOOKS and place it before 'autodetect'
mkinitcpio -g /boot/kernel26.img
pacman -Rd udev
pacman -S udev
exit

```

## Instalamos GRUB en el nuevo RAID de discos, cambiando los números de acuerdo a la instalación.

```
[root@svn /]#grub
grub> root (hd1,0)
Filesystem type is ext2fs, partition type 0xfd

```

```
grub> setup (hd1)
Checking if "/boot/grub/stage1" exists... yes
Checking if "/boot/grub/stage2" exists... yes
Checking if "/boot/grub/e2fs_stage1_5" exists... yes
Running "embed /boot/grub/e2fs_stage1_5 (hd1)"...  16 sectors are embedded.
succeeded
Running "install /boot/grub/stage1 (hd1) (hd1)1+16 p

```

(hd1,0)/boot/grub/stage2 /boot/grub/grub.conf"... succeeded

```
Done
grub>quit
[root@svn /]#

```

Reiniciamos con el nuevo disco RAID y no, dentro del disco viejo podríamos necesitar hacer algunos ajustes en el BIOS.

```
/sbin/reboot

```

Cruzamos los dedos ;) Si el sistema bootea bien, agrega los dispositivos md que faltan al RAID.

```
[root@svn ~]# mdadm /dev/md0 -a /dev/<old-disk-partitionA>
mdadm: hot added /dev/<old-disk-partitionA>
[root@svn ~]# mdadm /dev/md1 -a /dev/<old-disk-partitionB>
mdadm: hot added /dev/<old-disk-partitionB>
[root@svn ~]# mdadm /dev/md2 -a /dev/<old-disk-partitionC>
mdadm: hot added /dev/<old-disk-partitionC>
...
[root@svn ~]

```

## Chequeamos con mdstat

Verificamos que el RAID se haya construído:

```
[root@svn ~]# cat /proc/mdstat 
Personalities : [linear] [raid0] [raid1] [raid5] [multipath] [raid6] [raid10] 
md1 : active raid1 sda2[0] sdb2[1]
     264960 blocks [2/2] [UU]

md2 : active raid1 sda3[2] sdb3[1]
     80108032 blocks [2/1] [_U]
     [>....................]  recovery =  1.2% (1002176/80108032) finish=42.0min speed=31318K/sec
md0 : active raid1 sda1[0] sdb1[1]
     40064 blocks [2/2] [UU]

unused devices: <none>
[root@svn ~]#

```

## Finalizamos la configuración de grub

```
----- snip -----
# (0) Arch Linux
title  Arch Linux  [Disc0: /boot/vmlinuz26]
root   (hd0,0)
#kernel /vmlinuz26 root=/dev/discs/disc0/part3 ro
kernel /vmlinuz26 root=/dev/md<where you assigned-/-number> 
md=<all your md devices, 
please refer mkinitcpio howto for correct syntax, 
add the old disk partitions at this point> ro

```

```
# (1) Arch Linux
title  Arch Linux  [Disc1: /boot/vmlinuz26]
root   (hd1,0)
#kernel /vmlinuz26 root=/dev/discs/disc1/part3 ro
kernel /vmlinuz26 root=/dev/md<where you assigned-/-number> 
md=<all your md devices, 
please refer mkinitcpio howto for correct syntax, 
add the old disk partitions at this point> ro
----- snip -----

```

## Finalizamos initrd.

```
edit /etc/mkinitcpio.conf
you can now place 'raid' hook behind autodetect and rebuild initrd
mkinitpcio -g /boot/kernel26.img

```

## Cambiamos el orden de arranque en la BIOS nuevamente.

Terminamos, disfruta de tu nueva configuración RAID.