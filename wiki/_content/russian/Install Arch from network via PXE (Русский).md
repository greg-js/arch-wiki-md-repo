## Contents

*   [1 Загрузка по сети](#.D0.97.D0.B0.D0.B3.D1.80.D1.83.D0.B7.D0.BA.D0.B0_.D0.BF.D0.BE_.D1.81.D0.B5.D1.82.D0.B8)
    *   [1.1 Как это работает](#.D0.9A.D0.B0.D0.BA_.D1.8D.D1.82.D0.BE_.D1.80.D0.B0.D0.B1.D0.BE.D1.82.D0.B0.D0.B5.D1.82)
    *   [1.2 Подготовка](#.D0.9F.D0.BE.D0.B4.D0.B3.D0.BE.D1.82.D0.BE.D0.B2.D0.BA.D0.B0)
*   [2 Подготовка tftpd](#.D0.9F.D0.BE.D0.B4.D0.B3.D0.BE.D1.82.D0.BE.D0.B2.D0.BA.D0.B0_tftpd)
*   [3 Способ 1 - Использование DNSMASQ](#.D0.A1.D0.BF.D0.BE.D1.81.D0.BE.D0.B1_1_-_.D0.98.D1.81.D0.BF.D0.BE.D0.BB.D1.8C.D0.B7.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D0.B5_DNSMASQ)
*   [4 Способ 2 - использование DHCPD](#.D0.A1.D0.BF.D0.BE.D1.81.D0.BE.D0.B1_2_-_.D0.B8.D1.81.D0.BF.D0.BE.D0.BB.D1.8C.D0.B7.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D0.B5_DHCPD)

## Загрузка по сети

Ваш ноутбук поставляется без дисковода, и не позволяет загружаться с USB-накопителя? Не бойтесь, вы можете загрузиться с помощью PXE.

**PXE** сокращение от **P**reboot e**X**ecution **E**nvironment (произносится _пикси_) - это часть BIOS для загрузки компьютера с помощью сетевой карты. Для того, чтобы загрузиться через PXE, проверьте опции загрузки в BIOS. Обычно используется Ethernet порт.

### Как это работает

Грубое описание процесса загрузки с помощью PXE:

*   клиент (тот компьютер на который вы хотите установить) подключается к сети и опрашивает DHCP-сервера для аренды IP.
*   DHCP-сервер передает клиенту IP и другую, необходимую для сетевой загрузки, информацию.
*   затем клиент, на основе полученной информации, подключается TFTP-серверу по протоколу TFTP (который очень похож на регулярный FTP) и загружает файлы.

после этого клиент загружает систему со скаченных файлов. После загрузки системы можно отключить сетевое соединение (образ полностью загружается в память).

### Подготовка

Минимальный набор:

*   Сервер DHCPD
*   Сервер tftpd
*   Дистрибутив Arch Linux [Выбрать из списка серверов для ближайший для России можно здесь](https://www.archlinux.org/mirrorlist/?country=RU&protocol=http&ip_version=4)

DHCP-сервер и TFTP может быть один и тот же компьютер, если у вас есть только один.

Убедитесь, что межсетевой экран не блокирует порты.

Запустите сетевой интерфейс или убедитесь, что он запущен.

```
ifconfig eth0 up
ifconfig eth0 192.168.0.2

```

При необходимости настройте маршрутизацию.

```
ip route add default via 192.168.0.1

```

А также добавьте DNS сервера.

```
echo nameserver 192.168.0.1 >> /etc/resolv.conf

```

If a router is between the server and the client disabling DHCP on the router might be necessary, else you should be able to ignore these steps.

Alternatively, if your router has dnsmasq installed (like the *WRT family) you can configure it in the router with the following option:

```
dhcp-boot=pxelinux.0,_<hostname-of-the-tftd-server>_,_<ip-of-the-tftd-server>_

```

[Here](http://www.dd-wrt.com/wiki/index.php/PXE) is an example for DD-WRT.

## Подготовка tftpd

Примонтируйте archboot.iso и скопируйте содержимое в каталог загрузки /var/tftpboot/:

```
mount -o loop,ro archboot.iso /mnt/iso
cp -a /mnt/iso/boot/ /var/tftpboot

```

Переместите содержимое каталога isolinux (или syslinux) в корень tftpboot:

```
mv /var/tftpboot/boot/syslinux/* /var/tftpboot/
rmdir /var/tftpboot/boot/syslinux

```

Настройте pxelinux:

```
mkdir /var/tftpboot/pxelinux.cfg
mv /var/tftpboot/syslinux.cfg /var/tftpboot/pxelinux.cfg/default

```

Ваш сетевой инсталлятор Arch Linux готов.

## Способ 1 - Использование DNSMASQ

This one is a bit easier since dnsmasq already has a tftp server builtin. Install dnsmasq on your server:

```
pacman -S dnsmasq

```

Edit the configuration file for dnsmasq in:

```
/etc/dnsmasq.conf

```

The configuration file comments are rather verbose and should be self-explanatory. You should at least enable the following settings:

```
dhcp-range=192.168.0.50,192.168.0.150,12h
dhcp-boot=pxelinux.0
enable-tftp
tftp-root=/var/tftpboot

```

As for the necessary files to be able to boot follow the instructions as given at "Preparing tfptd". Now run dnsmasq.

```
rc.d start dnsmasq

```

## Способ 2 - использование DHCPD

Установите необходимое программное обеспечение на существующий компьютер под управлением Arch Linux. Этот компьютер будет выступать в роли сервера для установки на другой клиентский компьютер:

```
pacman -S tftp-hpa dhcp

```

Replace the default /etc/dhcpd.conf with the following (adjust to your network environment):

```
# /etc/dhcpd.conf
option domain-name-servers 208.67.222.222, 208.67.220.220;
default-lease-time 86400;
max-lease-time 604800;
authoritative;
subnet 192.168.0.0 netmask 255.255.255.0 {
 range 192.168.0.10 192.168.0.49;
 filename "pxelinux.0";        # the PXELinux boot agent
 option subnet-mask 255.255.255.0;
 option broadcast-address 192.168.0.255;
 option routers 192.168.0.1;
}

```

Dhcpd will not run without ipv6\. If you have disabled ipv6, reload the module:

```
modprobe ipv6

```

Be sure to static the LAN IP to the same subnet as **option routers** IP to get the DHCP server to start: ifconfig eth0 192.168.0.1 255.255.255.0

Now make sure the dhcpd and tftpd daemons are running on the server.

```
# /etc/rc.d/tftpd start
# /etc/rc.d/dhcpd start

```

Boot your destination machine over PXE (usually something like F12 (on Dells) or F11 (on Supermicro's), or enable it in the BIOS).

When you get the PXEBoot prompt, type 'arch' or hit return to start the installer. The install should now progress the same as if you booted from CD. You can continue installation by following the [Руководство для начинающих](/index.php/Beginners%27_guide_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Beginners' guide (Русский)") or the [Руководство по установке](/index.php/Installation_guide_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Installation guide (Русский)").