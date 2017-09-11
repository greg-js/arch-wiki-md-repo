**Состояние перевода:** На этой странице представлен перевод статьи [Diskless system](/index.php/Diskless_system "Diskless system"). Дата последней синхронизации: 16 июля 2017\. Вы можете [помочь](/index.php/ArchWiki_Translation_Team_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "ArchWiki Translation Team (Русский)") синхронизировать перевод, если в английской версии произошли [изменения](https://wiki.archlinux.org/index.php?title=Diskless_system&diff=0&oldid=482033).

Ссылки по теме

*   [NFS (Русский)](/index.php/NFS_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "NFS (Русский)")
*   [NFS Troubleshooting](/index.php/NFS_Troubleshooting "NFS Troubleshooting")
*   [PXE (Русский)](/index.php/PXE_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "PXE (Русский)")
*   [Mkinitcpio (Русский)#Использование net](/index.php/Mkinitcpio_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#.D0.98.D1.81.D0.BF.D0.BE.D0.BB.D1.8C.D0.B7.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D0.B5_net "Mkinitcpio (Русский)")
*   [iSCSI Boot](/index.php/ISCSI_Boot "ISCSI Boot")

Из [Википедии:Бездисковая рабочая станция](https://en.wikipedia.org/wiki/ru:%D0%91%D0%B5%D0%B7%D0%B4%D0%B8%D1%81%D0%BA%D0%BE%D0%B2%D0%B0%D1%8F_%D1%80%D0%B0%D0%B1%D0%BE%D1%87%D0%B0%D1%8F_%D1%81%D1%82%D0%B0%D0%BD%D1%86%D0%B8%D1%8F "w:ru:Бездисковая рабочая станция")

	*Бездисковая рабочая станция (или бездисковый узел) — это персональный компьютер, лишённый несъёмных средств для долговременного хранения данных и который использует для загрузки своей операционной системы с сервера.*

## Contents

*   [1 Настройка сервера](#.D0.9D.D0.B0.D1.81.D1.82.D1.80.D0.BE.D0.B9.D0.BA.D0.B0_.D1.81.D0.B5.D1.80.D0.B2.D0.B5.D1.80.D0.B0)
    *   [1.1 DHCP](#DHCP)
    *   [1.2 TFTP](#TFTP)
    *   [1.3 Сетевое хранилище](#.D0.A1.D0.B5.D1.82.D0.B5.D0.B2.D0.BE.D0.B5_.D1.85.D1.80.D0.B0.D0.BD.D0.B8.D0.BB.D0.B8.D1.89.D0.B5)
        *   [1.3.1 NFS](#NFS)
        *   [1.3.2 NBD](#NBD)
*   [2 Установка клиента](#.D0.A3.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B0_.D0.BA.D0.BB.D0.B8.D0.B5.D0.BD.D1.82.D0.B0)
    *   [2.1 Настройка каталога](#.D0.9D.D0.B0.D1.81.D1.82.D1.80.D0.BE.D0.B9.D0.BA.D0.B0_.D0.BA.D0.B0.D1.82.D0.B0.D0.BB.D0.BE.D0.B3.D0.B0)
    *   [2.2 Загрузчик установки](#.D0.97.D0.B0.D0.B3.D1.80.D1.83.D0.B7.D1.87.D0.B8.D0.BA_.D1.83.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B8)
        *   [2.2.1 NFS](#NFS_2)
        *   [2.2.2 NBD](#NBD_2)
*   [3 Настройка клиента](#.D0.9D.D0.B0.D1.81.D1.82.D1.80.D0.BE.D0.B9.D0.BA.D0.B0_.D0.BA.D0.BB.D0.B8.D0.B5.D0.BD.D1.82.D0.B0)
    *   [3.1 Загрузчик](#.D0.97.D0.B0.D0.B3.D1.80.D1.83.D0.B7.D1.87.D0.B8.D0.BA)
        *   [3.1.1 GRUB](#GRUB)
        *   [3.1.2 Pxelinux](#Pxelinux)
    *   [3.2 Дополнительные точки монтирования](#.D0.94.D0.BE.D0.BF.D0.BE.D0.BB.D0.BD.D0.B8.D1.82.D0.B5.D0.BB.D1.8C.D0.BD.D1.8B.D0.B5_.D1.82.D0.BE.D1.87.D0.BA.D0.B8_.D0.BC.D0.BE.D0.BD.D1.82.D0.B8.D1.80.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D1.8F)
        *   [3.2.1 Корень NBD](#.D0.9A.D0.BE.D1.80.D0.B5.D0.BD.D1.8C_NBD)
        *   [3.2.2 Состояние каталогов программ](#.D0.A1.D0.BE.D1.81.D1.82.D0.BE.D1.8F.D0.BD.D0.B8.D0.B5_.D0.BA.D0.B0.D1.82.D0.B0.D0.BB.D0.BE.D0.B3.D0.BE.D0.B2_.D0.BF.D1.80.D0.BE.D0.B3.D1.80.D0.B0.D0.BC.D0.BC)
*   [4 Загрузка клиента](#.D0.97.D0.B0.D0.B3.D1.80.D1.83.D0.B7.D0.BA.D0.B0_.D0.BA.D0.BB.D0.B8.D0.B5.D0.BD.D1.82.D0.B0)
    *   [4.1 NBD](#NBD_3)
*   [5 Смотрите также](#.D0.A1.D0.BC.D0.BE.D1.82.D1.80.D0.B8.D1.82.D0.B5_.D1.82.D0.B0.D0.BA.D0.B6.D0.B5)

## Настройка сервера

Прежде всего, мы должны установить следующие компоненты:

*   Сервер [DHCP](/index.php/Dhcpd_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Dhcpd (Русский)") для назначения IP-адресов нашим бездисковым узлам.
*   Сервер [TFTP](/index.php/TFTP "TFTP") для передачи загрузочного образа (требование всех опций roms PXE).
*   Форма сетевого хранилища ([NFS](/index.php/NFS_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "NFS (Русский)") или NBD) для экспорта установки Arch на бездисковый узел.

**Примечание:** [dnsmasq](https://www.archlinux.org/packages/?name=dnsmasq) способен одновременно действовать как сервер DHCP и TFTP. Для получения дополнительной информации смотрите статью [dnsmasq](/index.php/Dnsmasq_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Dnsmasq (Русский)").

### DHCP

Установите ISC [dhcp](https://www.archlinux.org/packages/?name=dhcp) и настройте его:

 `/etc/dhcpd.conf` 
```
allow booting;
allow bootp;

authoritative;

option domain-name-servers 10.0.0.1;

option architecture code 93 = unsigned integer 16;

group {
    next-server 10.0.0.1;

    if option architecture = 00:07 {
        filename "/grub/x86_64-efi/core.efi";
    } else {
        filename "/grub/i386-pc/core.0";
    }

    subnet 10.0.0.0 netmask 255.255.255.0 {
        option routers 10.0.0.1;
        range 10.0.0.128 10.0.0.254;
    }
}
```

**Примечание:** `next-server` должен быть адресом сервера TFTP; все остальное должно быть изменено в соответствии с вашей сетью

RFC 4578 определяет параметр dhcp "Client System Architecture Type". В приведенной выше конфигурации, если клиент PXE запрашивает двоичный файл x86_64-efi (тип 0x7), мы соответствующим образом предоставляем его, в противном случае возвращаемся к устаревшему двоичному файлу. Это позволяет одновременно загружать UEFI и устаревшие клиенты BIOS в один и тот же сегмент сети.

Запустите службу [systemd](/index.php/Systemd_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Systemd (Русский)") ISC DHCP.

### TFTP

TFTP-сервер будет использоваться для передачи загрузчика, ядра и initramfs клиенту.

Установите корень TFTP в `/srv/arch/boot`. Смотрите [[Tftpd server|]сервер Tftpd] для установки и настройки.

### Сетевое хранилище

Основное различие между использованием NFS и NBD заключается в том, что с обоими вы можете иметь несколько клиентов, использующих одну и ту же установку, с NBD (по характеру манипулирования файловой системой напрямую) вам нужно будет использовать режим `copyonwrite` для этого, который в конечном итоге отбрасывает все записи на отключении клиента. Однако в некоторых ситуациях это может быть очень полезно.

#### NFS

Установите [nfs-utils](https://www.archlinux.org/packages/?name=nfs-utils) на сервере.

Вам нужно будет добавить корень вашей установки Arch в ваш экспорт [NFS](/index.php/NFS_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "NFS (Русский)"):

 `/etc/exports` 
```
/srv       *(rw,fsid=0,no_root_squash,no_subtree_check)
/srv/arch  *(rw,no_root_squash,no_subtree_check)
```

Затем запустите службы NFS: `rpc-idmapd` `rpc-mountd`.

#### NBD

Установите [nbd](https://www.archlinux.org/packages/?name=nbd) и настройте его.

 `# vim /etc/nbd-server/config` 
```
[generic]
    user = nbd
    group = nbd
[arch]
    exportname = /srv/arch.img
    copyonwrite = false
```

**Примечание:** Установите `copyonwrite` в true, если вы хотите одновременно использовать несколько клиентов, использующих один и тот же ресурс NBD; для получения дополнительной информации смотрите [nbd-server(5)](http://jlk.fjfi.cvut.cz/arch/manpages/man/nbd-server.5).

Запустите `nbd` службу systemd.

## Установка клиента

Затем мы создадим полную установку Arch Linux в подкаталоге на сервере. Во время загрузки бездисковый клиент получает IP-адрес от DHCP-сервера, а затем загружается с хоста с помощью PXE и монтирует эту установку в качестве своего корня.

### Настройка каталога

Создайте [разрежённый файл](https://en.wikipedia.org/wiki/ru:%D0%A0%D0%B0%D0%B7%D1%80%D0%B5%D0%B6%D1%91%D0%BD%D0%BD%D1%8B%D0%B9_%D1%84%D0%B0%D0%B9%D0%BB "w:ru:Разрежённый файл") размером не менее 1 гигабайта и создайте на нем файловую систему btrfs (вы также можете использовать реальное блочное устройство или [LVM](/index.php/LVM_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "LVM (Русский)"), если вы так желаете).

```
# truncate -s 1G /srv/arch.img
# mkfs.btrfs /srv/arch.img
# export root=/srv/arch
# mkdir -p "$root"
# mount -o loop,discard,compress=lzo /srv/arch.img "$root"

```

**Примечание:** Создание отдельной файловой системы требуется для NBD, но необязательно для NFS и может быть пропущено/проигнорировано.

### Загрузчик установки

Установите [devtools](https://www.archlinux.org/packages/?name=devtools) и [arch-install-scripts](https://www.archlinux.org/packages/?name=arch-install-scripts), а затем запустите `mkarchroot`.

```
# pacstrap -d "$root" base mkinitcpio-nfs-utils nfs-utils

```

**Примечание:** Во всех случаях [mkinitcpio-nfs-utils](https://www.archlinux.org/packages/?name=mkinitcpio-nfs-utils) по-прежнему требуется. `ipconfig`, используемый на ранних этапах процесса загрузки, предоставляется только последним.

Теперь необходимо создать initramfs.

#### NFS

Для того, чтобы монтирование NFSv4 работало (не поддерживается `nfsmount` - по умолчанию для хука `net`), необходимы тривиальные модификации хука `net`.

```
# sed s/nfsmount/mount.nfs4/ "$root/usr/lib/initcpio/hooks/net" > "$root/usr/lib/initcpio/hooks/net_nfs4"
# cp $root/usr/lib/initcpio/install/net{,_nfs4}

```

Копия `net`, к сожалению, необходима, чтобы он не перезаписывался при обновлении [mkinitcpio-nfs-utils](https://www.archlinux.org/packages/?name=mkinitcpio-nfs-utils) во время установки клиента.

Отредактируйте `$root/etc/mkinitcpio.conf` и добавьте `nfsv4` в `MODULES`, `net_nfs4` в `HOOKS` и `/usr/bin/mount.nfs4` в `BINARIES`.

Затем мы выполним [chroot](/index.php/Change_root_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Change root (Русский)") для нашей установки и запустим *mkinitcpio*:

```
# arch-chroot "$root" mkinitcpio -p linux

```

#### NBD

Пакет [mkinitcpio-nbd](https://aur.archlinux.org/packages/mkinitcpio-nbd/) должен быть установлен на клиенте. Соберите его с помощью *[makepkg](/index.php/Makepkg_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Makepkg (Русский)")* и установите его:

```
# pacman --root "$root" --dbpath "$root/var/lib/pacman" -U mkinitcpio-nbd-0.4-1-any.pkg.tar.xz

```

Затем вам нужно добавить `nbd` в ваш массив `HOOKS` после `net`; `net` настроит вашу сеть для вас, но не пытайтесь монтировать NFS, если `nfsroot не указан в строке ядра.`.

## Настройка клиента

В дополнение к настройке, упомянутой здесь, вы также должны установить свои [имя хоста](/index.php/Network_configuration_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#.D0.A3.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B0_.D0.B8.D0.BC.D0.B5.D0.BD.D0.B8_.D1.83.D0.B7.D0.BB.D0.B0 "Network configuration (Русский)"), [часовой пояс](/index.php/Time_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#.D0.A7.D0.B0.D1.81.D0.BE.D0.B2.D0.BE.D0.B9_.D0.BF.D0.BE.D1.8F.D1.81 "Time (Русский)"), [локаль](/index.php/Locale_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#.D0.A3.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B0_.D1.81.D0.B8.D1.81.D1.82.D0.B5.D0.BC.D0.BD.D0.BE.D0.B9_.D0.BB.D0.BE.D0.BA.D0.B0.D0.BB.D0.B8 "Locale (Русский)") и [раскладку клавиатуры](/index.php/Keyboard_configuration_in_console_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Keyboard configuration in console (Русский)"), а затем следуйте любым другим соответствующим разделам [руководства по установке](/index.php/Installation_guide_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Installation guide (Русский)").

### Загрузчик

#### GRUB

Несмотря на то, что GRUB плохо документирован, он загружается через PXE.

```
# pacman --root "$root" --dbpath "$root/var/lib/pacman" -S grub

```

Создайте префикс grub для целевой установки для обеих архитектур, используя `grub-mknetdir`.

```
# arch-chroot "$root" grub-mknetdir --net-directory=/boot --subdir=grub

```

К счастью для нас, grub-mknetdir создает префиксы для всех компилированных/установленных целей, а сопровождающие [grub](https://www.archlinux.org/packages/?name=grub) были достаточно хороши, чтобы предоставить нам обоих в одном пакете, поэтому grub-mknetdir нужно запускать только один раз.

Теперь мы создаем тривиальную конфигурацию GRUB:

 `# vim "$root/boot/grub/grub.cfg"` 
```
menuentry "Arch Linux" {
    linux /vmlinuz-linux quiet add_efi_memmap ip=:::::eth0:dhcp nfsroot=10.0.0.1:/arch
    initrd /initramfs-linux.img
}
```

[GRUB](/index.php/GRUB_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "GRUB (Русский)") dark-magic будет `set root=(tftp,10.0.0.1)` автоматически, так что ядро и initramfs будут переданы через TFTP без какой-либо дополнительной настройки, хотя вы можете явно установить его, если у вас есть другие non-tftp menuentries.

**Примечание:** Измените нужную строку ядра как надо, обратитесь к параметрам [Pxelinux](/index.php/Syslinux_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#Pxelinux "Syslinux (Русский)") для NBD.

#### Pxelinux

[Pxelinux](/index.php/Syslinux_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Syslinux (Русский)") предоставляется пакетом [syslinux](https://www.archlinux.org/packages/?name=syslinux), для получения допольнительной информации смотрите [здесь](/index.php/Syslinux_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#Pxelinux "Syslinux (Русский)").

### Дополнительные точки монтирования

#### Корень NBD

В конце загрузки вы захотите переключить монтирование корневой файловой системы на `rw` и включить `compress=lzo`, что значительно улучшит производительность диска по сравнению с [NFS](/index.php/NFS_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "NFS (Русский)").

 `# vim "$root/etc/fstab"`  `/dev/nbd0  /  btrfs  rw,noatime,discard,compress=lzo  0 0` 

#### Состояние каталогов программ

Вы можете смонтировать `/var/log`, например, как tmpfs, чтобы журналы с нескольких хостов не смешивались непредсказуемо и делали то же самое с `/var/spool/cups`, поэтому 20 экземпляров cups, использующих один и тот же spool, не сражаются друг с другом и делают 1 498 заданий на печать и едят целую бумагу (или, что еще хуже: тонер-картридж) в одночасье.

 `# vim "$root/etc/fstab"` 
```
tmpfs   /var/log        tmpfs     nodev,nosuid    0 0
tmpfs   /var/spool/cups tmpfs     nodev,nosuid    0 0
```

Было бы лучше настроить программное обеспечение, которое имеет какое-то состояние/базу данных для использования уникальных каталогов для хранения состояния/баз данных для каждого хоста. Например, если вы хотите запустить [puppet](http://puppetlabs.com/), вы можете просто использовать спецификатор `%H` в файле юнита puppet:

 `# vim "$root/etc/systemd/system/puppetagent.service"` 
```
[Unit]
Description=Puppet agent
Wants=basic.target
After=basic.target network.target

[Service]
Type=forking
PIDFile=/run/puppet/agent.pid
ExecStartPre=/usr/bin/install -d -o puppet -m 755 /run/puppet
ExecStart=/usr/bin/puppet agent --vardir=/var/lib/puppet-%H --ssldir=/etc/puppet/ssl-%H

[Install]
WantedBy=multi-user.target
```

Puppet-агент создает vardir и ssldir, если они не существуют.

Если ни один из этих подходов не подходит, последним разумным вариантом будет создание [генератора systemd](http://www.freedesktop.org/wiki/Software/systemd/Generators), который создает узел монтирования, специфичный для текущего хоста (к сожалению, спецификаторы не разрешены в юнитах монтирования).

## Загрузка клиента

### NBD

Если вы используете NBD, вам нужно будет размонтировать `arch.img` до/во время загрузки вашего клиента.

Это особенно интересно, когда дело доходит до обновлений ядра. У вас не может быть смонтирована ваша файловая система клиента при загрузке клиента, но это также означает, что вам нужно использовать ядро отдельно от вашей файловой системы клиента, чтобы его собрать.

Вам нужно сначала скопировать `$root/boot` с установки клиента на ваш корень tftp (то есть в `/srv/boot`).

```
# cp -r "$root/boot" /srv/boot

```

Затем вам нужно будет размонтировать `$root` перед запуском клиента.

```
# umount "$root"

```

**Примечание:** Чтобы обновить ядро на этом этапе, вам нужно либо смонтировать `/srv/boot` с помощью [NFS](/index.php/NFS_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "NFS (Русский)") в [fstab](/index.php/Fstab_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Fstab (Русский)") на клиенте (до обновления ядра) или смонтировать вашу клиентскую файловую систему после того, как клиент отключился от NBD

## Смотрите также

*   [kernel.org: Монтирование корневой файловой системы через NFS (nfsroot)](https://www.kernel.org/doc/Documentation/filesystems/nfs/nfsroot.txt)
*   [syslinux.org: pxelinux FAQ](http://www.syslinux.org/wiki/index.php/PXELINUX)