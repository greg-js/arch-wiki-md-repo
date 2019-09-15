1.  Preuzeti ISO image i kopirati na instalacijski medij

    *   Posljednja verzija se može skinuti sa [Download](https://www.archlinux.org/download/); odraditi hash nad ISO image-om sa md5sum ili SHA-1 i vidjeti da li se slaže sa hashom sa *Download* page-a.
    *   Spržiti na CD ili USB koristeći **dd**. Potrebno je navesti tačan naziv uredjaja, u našem slučaju **/dev/sda2** `# dd if=archlinux-*-x86_64.iso of=/dev/sda2 status=progress`

2.  Bootati sa instalacijskog medija
3.  Podesiti particije

    *   Sa jednim od sljedećih alata: fdisk, parted, cfdisk, [gdisk](/index.php/Gdisk "Gdisk") itd.
    *   Podesiti [LVM](/index.php/LVM "LVM"),[LUKS](/index.php/LUKS "LUKS"),[RAID](/index.php/RAID "RAID"). [LVM](/index.php/LVM "LVM") olakšava upravljanje particijama izmedju ostalih stvari. Npr. Ako želimo da dodamo još jedan hard disk na / particiju, sa LVM-om možemo to odraditi bez gašenja, dok bez LVM morali bismo izgasiti i uci u *rescue* mode.
    *   Poželjno je napraviti [swap](/index.php/Swap "Swap") particiju u ovome koraku.

4.  Kreirati fajl sistem

    *   `mkfs` željenog sistema([ext2](/index.php?title=Ext2&action=edit&redlink=1 "Ext2 (page does not exist)"),[ext3](/index.php/Ext3 "Ext3"),[ext4](/index.php/Ext4 "Ext4"),[xfs](/index.php/Xfs "Xfs"))

5.  Mountati particije

    *   Root particiju u `# mount /dev/sdX /mnt`
    *   Swap particiju `# mkswap /dev/sdX; swapon /dev/sdX`

6.  Instalirati [base](/index.php/Base "Base") pakete sa [pacstrap](https://projects.archlinux.org/arch-install-scripts.git/tree/pacstrap.in)-om

    *   `# pacstrap /mnt base`

7.  Sistemska podešavanja

    *   [fstab](/index.php/Fstab "Fstab") generisati: `# genfstab -p /mnt >> /mnt/etc/fstab`
    *   `# arch-chroot /mnt`
        *   Sistemska konfiguracija
            *   Podesiti hostname unutar `/etc/hostname`
            *   Podesiti podešavanja jezika unutar `/etc/locale.conf`
            *   Napraviti symbolic link `# ln -sf /usr/share/zoneinfo/Europe/Sarajevo /etc/localtime`
            *   Odkomentarisati željene jezike unutar `/etc/locale.gen`, te generisati sa `# locale-gen`
        *   [mkinitcpio](/index.php/Mkinitcpio "Mkinitcpio") nad `/etc/mkinitcpio.conf`
        *   Kreirati kernel image: `# mkinitcpio -p linux`
        *   Podesiti password za root usera `# passwd`
        *   Urediti keyboard layour unutar `/etc/vconsole.conf`

8.  Konfigurisati [bootloader](/index.php/Bootloader "Bootloader")

    *   [syslinux](/index.php/Syslinux "Syslinux")
        *   Instalirati syslinux: `# pacman -S syslinux`
        *   Instalirati syslinux na MBR sda diska `# syslinux-install_update -i -a -m`
        *   Provjeriti postavke unutar `/boot/syslinux/syslinux.cfg`, pogotovo liniju **APPEND root=...** da li je dobra boot particija odabrana
    *   [grub](/index.php/Grub "Grub")

9.  Izaci iz chroot-a(`# exit`)
10.  Umountati particije (`# umount /dev/sdX`)
11.  Izgasiti računar, otkloniti instalacijski medij te pokrenuti računar.