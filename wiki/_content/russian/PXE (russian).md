**Состояние перевода:** На этой странице представлен перевод статьи [PXE](/index.php/PXE "PXE"). Дата последней синхронизации: 14 января 2018\. Вы можете [помочь](/index.php/ArchWiki_Translation_Team_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "ArchWiki Translation Team (Русский)") синхронизировать перевод, если в английской версии произошли [изменения](https://wiki.archlinux.org/index.php?title=PXE&diff=0&oldid=507511).

Ссылки по теме

*   [Бездисковая система](/index.php/%D0%91%D0%B5%D0%B7%D0%B4%D0%B8%D1%81%D0%BA%D0%BE%D0%B2%D0%B0%D1%8F_%D1%81%D0%B8%D1%81%D1%82%D0%B5%D0%BC%D0%B0 "Бездисковая система")

Ваш ноутбук поставляется без дисковода, и не позволяет загружаться с USB-накопителя? Не бойтесь, вы можете загрузиться с помощью PXE.

Из [Википедии:Preboot Execution Environment](https://en.wikipedia.org/wiki/ru:PXE "w:ru:PXE"):

	***PXE** (англ.**P**reboot e**X**ecution **E**nvironment произносится* пикси*) — среда для загрузки компьютеров с помощью сетевой карты без использования жёстких дисков, компакт-дисков и других устройств, применяемых при загрузке операционной системы.*

В этом руководстве PXE используется для загрузки установочного носителя с соответствующей опцией-rom, которая поддерживает PXE в целевом объекте. Это хорошо работает, когда у вас уже установлен сервер.

## Contents

*   [1 Как это работает](#.D0.9A.D0.B0.D0.BA_.D1.8D.D1.82.D0.BE_.D1.80.D0.B0.D0.B1.D0.BE.D1.82.D0.B0.D0.B5.D1.82)
*   [2 Подготовка](#.D0.9F.D0.BE.D0.B4.D0.B3.D0.BE.D1.82.D0.BE.D0.B2.D0.BA.D0.B0)
*   [3 Настройка сервера](#.D0.9D.D0.B0.D1.81.D1.82.D1.80.D0.BE.D0.B9.D0.BA.D0.B0_.D1.81.D0.B5.D1.80.D0.B2.D0.B5.D1.80.D0.B0)
    *   [3.1 Сеть](#.D0.A1.D0.B5.D1.82.D1.8C)
    *   [3.2 DHCP + TFTP](#DHCP_.2B_TFTP)
    *   [3.3 HTTP](#HTTP)
*   [4 Установка](#.D0.A3.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B0)
    *   [4.1 Загрузка](#.D0.97.D0.B0.D0.B3.D1.80.D1.83.D0.B7.D0.BA.D0.B0)
    *   [4.2 После загрузки](#.D0.9F.D0.BE.D1.81.D0.BB.D0.B5_.D0.B7.D0.B0.D0.B3.D1.80.D1.83.D0.B7.D0.BA.D0.B8)
*   [5 Альтернативные способы](#.D0.90.D0.BB.D1.8C.D1.82.D0.B5.D1.80.D0.BD.D0.B0.D1.82.D0.B8.D0.B2.D0.BD.D1.8B.D0.B5_.D1.81.D0.BF.D0.BE.D1.81.D0.BE.D0.B1.D1.8B)
    *   [5.1 NFS](#NFS)
    *   [5.2 NBD](#NBD)
    *   [5.3 Существующий сервер PXE](#.D0.A1.D1.83.D1.89.D0.B5.D1.81.D1.82.D0.B2.D1.83.D1.8E.D1.89.D0.B8.D0.B9_.D1.81.D0.B5.D1.80.D0.B2.D0.B5.D1.80_PXE)
    *   [5.4 Ошибка переименования интерфейса DHCP](#.D0.9E.D1.88.D0.B8.D0.B1.D0.BA.D0.B0_.D0.BF.D0.B5.D1.80.D0.B5.D0.B8.D0.BC.D0.B5.D0.BD.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D1.8F_.D0.B8.D0.BD.D1.82.D0.B5.D1.80.D1.84.D0.B5.D0.B9.D1.81.D0.B0_DHCP)
    *   [5.5 Системы с небольшим объемом памяти](#.D0.A1.D0.B8.D1.81.D1.82.D0.B5.D0.BC.D1.8B_.D1.81_.D0.BD.D0.B5.D0.B1.D0.BE.D0.BB.D1.8C.D1.88.D0.B8.D0.BC_.D0.BE.D0.B1.D1.8A.D0.B5.D0.BC.D0.BE.D0.BC_.D0.BF.D0.B0.D0.BC.D1.8F.D1.82.D0.B8)
*   [6 Смотрите также](#.D0.A1.D0.BC.D0.BE.D1.82.D1.80.D0.B8.D1.82.D0.B5_.D1.82.D0.B0.D0.BA.D0.B6.D0.B5)

## Как это работает

Грубое описание процесса загрузки с помощью PXE:

*   клиент (тот компьютер на который вы хотите установить) подключается к сети и опрашивает DHCP-сервера для аренды IP.
*   DHCP-сервер передает клиенту IP и другую, необходимую для сетевой загрузки, информацию.
*   затем клиент, на основе полученной информации, подключается TFTP-серверу по протоколу TFTP (который очень похож на регулярный FTP) и загружает файлы.

после этого клиент загружает систему со скаченных файлов. После загрузки системы можно отключить сетевое соединение (образ полностью загружается в память).

## Подготовка

Загрузите последний официальный установочный образ со [страницы загрузки](https://www.archlinux.org/download/).

Затем смонтируйте образ:

```
# mkdir -p /mnt/archiso
# mount -o loop,ro archlinux-2017.12.01-x86_64.iso /mnt/archiso

```

## Настройка сервера

Вам необходимо установить DHCP, [TFTP](/index.php/TFTP "TFTP") и [HTTP-сервер](/index.php/List_of_applications/Internet_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#Web_servers "List of applications/Internet (Русский)") для настройки сети, загрузки pxelinux/kernel/initramfs, и, наконец, загрузки корневой файловой системы (соответственно).

На данный момент Arch поддерживает загрузку PXE только в стиле BIOS. Для получения дополнительной информации смотрите [FS#50188](https://bugs.archlinux.org/task/50188).

### Сеть

Подключите проводную сетевую карту и назначьте ее соответствующим образом.

```
# ip link set eth0 up
# ip addr add 192.168.0.1/24 dev eth0

```

### DHCP + TFTP

Для настройки сети на устройстве вам потребуется как DHCP, так и TFTP-сервер, чтобы облегчить передачу файлов между сервером PXE и клиентом; [dnsmasq](/index.php/Dnsmasq "Dnsmasq") делает и то, и другое, и очень прост в настройке.

[Установите](/index.php/%D0%A3%D1%81%D1%82%D0%B0%D0%BD%D0%BE%D0%B2%D0%B8%D1%82%D0%B5 "Установите") пакет [dnsmasq](https://www.archlinux.org/packages/?name=dnsmasq).

Настройте *dnsmasq*:

 `# /etc/dnsmasq.conf` 
```
port=0
interface=eth0
bind-interfaces
dhcp-range=192.168.0.50,192.168.0.150,12h
dhcp-boot=/arch/boot/syslinux/lpxelinux.0
dhcp-option-force=209,boot/syslinux/archiso.cfg
dhcp-option-force=210,/arch/
dhcp-option-force=66,192.168.0.1
enable-tftp
tftp-root=/mnt/archiso
```

[Запустите](/index.php/%D0%97%D0%B0%D0%BF%D1%83%D1%81%D1%82%D0%B8%D1%82%D0%B5 "Запустите") `dnsmasq.service`.

### HTTP

Благодаря недавним изменениям в [archiso](/index.php/Archiso_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Archiso (Русский)"), теперь можно загрузиться с HTTP (`archiso_pxe_http` initcpio hook) или NFS (`archiso_pxe_nfs` initcpio hook); среди всех альтернатив, darkhttpd на сегодняшний день является самым тривиальным (и самым легким) для настройки.

Сначала, [установите](/index.php/%D0%A3%D1%81%D1%82%D0%B0%D0%BD%D0%BE%D0%B2%D0%B8%D1%82%D0%B5 "Установите") пакет [darkhttpd](https://www.archlinux.org/packages/?name=darkhttpd).

Затем запустите *darkhttpd*, используя наш `/mnt/archiso` в качестве корневого документа:

 `# darkhttpd /mnt/archiso` 
```
darkhttpd/1.8, copyright (c) 2003-2011 Emil Mikulic.
listening on: http://0.0.0.0:80/

```

Обратите внимание, что важно, чтобы сервер работал на `80` порту. Если вы запустите *darkhttpd* без доступа суперпользователя, по умолчанию он будет `8080`. Клиент попытается получить доступ к 80 порту, и загрузка завершится неудачно.

## Установка

Для этой части вам нужно выяснить, как сообщить клиенту выбрать загрузку PXE; в углу экрана вместе с обычными сообщениями обычно появляется подсказка о том, какую клавишу нажать, чтобы сначала запустить загрузку PXE. На IBM x3650 при нажатии `F12` появляется меню загрузки, первым вариантом которого является *Network*; на Dell PE 1950/2950 нажатие `F12` инициирует загрузку PXE напрямую.

### Загрузка

Просмотр [journald](/index.php/Systemd_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#.D0.96.D1.83.D1.80.D0.BD.D0.B0.D0.BB "Systemd (Русский)") на сервере PXE даст дополнительную информацию о том, что именно происходит на ранних этапах процесса загрузки PXE:

 `# journalctl -u dnsmasq.service -f` 
```
dnsmasq-dhcp[2544]: DHCPDISCOVER(eth1) 00:1a:64:6a:a2:4d 
dnsmasq-dhcp[2544]: DHCPOFFER(eth1) 192.168.0.110 00:1a:64:6a:a2:4d 
dnsmasq-dhcp[2544]: DHCPREQUEST(eth1) 192.168.0.110 00:1a:64:6a:a2:4d 
dnsmasq-dhcp[2544]: DHCPACK(eth1) 192.168.0.110 00:1a:64:6a:a2:4d 
dnsmasq-tftp[2544]: sent /mnt/archiso/arch/boot/syslinux/pxelinux.0 to 192.168.0.110
dnsmasq-tftp[2544]: sent /mnt/archiso/arch/boot/syslinux/archiso.cfg to 192.168.0.110
dnsmasq-tftp[2544]: sent /mnt/archiso/arch/boot/syslinux/whichsys.c32 to 192.168.0.110
dnsmasq-tftp[2544]: sent /mnt/archiso/arch/boot/syslinux/archiso_pxe_choose.cfg to 192.168.0.110
dnsmasq-tftp[2544]: sent /mnt/archiso/arch/boot/syslinux/ifcpu64.c32 to 192.168.0.110
dnsmasq-tftp[2544]: sent /mnt/archiso/arch/boot/syslinux/archiso_pxe_both_inc.cfg to 192.168.0.110
dnsmasq-tftp[2544]: sent /mnt/archiso/arch/boot/syslinux/archiso_head.cfg to 192.168.0.110
dnsmasq-tftp[2544]: sent /mnt/archiso/arch/boot/syslinux/archiso_pxe32.cfg to 192.168.0.110
dnsmasq-tftp[2544]: sent /mnt/archiso/arch/boot/syslinux/archiso_pxe64.cfg to 192.168.0.110
dnsmasq-tftp[2544]: sent /mnt/archiso/arch/boot/syslinux/archiso_tail.cfg to 192.168.0.110
dnsmasq-tftp[2544]: sent /mnt/archiso/arch/boot/syslinux/vesamenu.c32 to 192.168.0.110
dnsmasq-tftp[2544]: sent /mnt/archiso/arch/boot/syslinux/splash.png to 192.168.0.110

```

После загрузки `pxelinux.0` и `archiso.cfg` через TFTP вам (надеюсь) будет представлено меню загрузки [syslinux](/index.php/Syslinux_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Syslinux (Русский)") с несколькими параметрами, в которых вы можете выбрать *Boot Arch Linux (x86_64) (HTTP)*.

Затем ядро и initramfs (подходящие для выбранной вами архитектуры) будут переданы снова через TFTP:

```
dnsmasq-tftp[2544]: sent /mnt/archiso/arch/boot/x86_64/vmlinuz to 192.168.0.110
dnsmasq-tftp[2544]: sent /mnt/archiso/arch/boot/x86_64/archiso.img to 192.168.0.110
```

Если все пойдет хорошо, вы должны увидеть активность на darkhttpd исходящую от PXE-target; на этом этапе ядро будет загружено на PXE-target и инициализировано:

```
1348347586 192.168.0.110 "GET /arch/aitab" 200 678 "" "curl/7.27.0"
1348347587 192.168.0.110 "GET /arch/x86_64/root-image.fs.sfs" 200 107860206 "" "curl/7.27.0"
1348347588 192.168.0.110 "GET /arch/x86_64/usr-lib-modules.fs.sfs" 200 36819181 "" "curl/7.27.0"
1348347588 192.168.0.110 "GET /arch/any/usr-share.fs.sfs" 200 63693037 "" "curl/7.27.0"
```

После того, как корневая файловая система загружается через HTTP, вы в конечном итоге окажетесь в обычном запросе суперпользователя [zsh](/index.php/Zsh_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Zsh (Русский)").

### После загрузки

Если вы не хотите, чтобы весь трафик маршрутизировался через ваш PXE-сервер (который не будет работать в любом случае, если вы [не настроите его правильно](/index.php/Simple_stateful_firewall#Setting_up_a_NAT_gateway "Simple stateful firewall")), вы захотите [остановить](/index.php/%D0%9E%D1%81%D1%82%D0%B0%D0%BD%D0%BE%D0%B2%D0%B8%D1%82%D1%8C "Остановить") `dnsmasq.service` и получить новую аренду на цели установки, в зависимости от вашего сетевого расположения.

Вы также можете убить *darkhttpd*; объект уже загрузил корневую файловую систему, поэтому он больше не нужен. Пока он активен, вы также можете размонтировать установочный образ:

```
# umount /mnt/archiso

```

На этом этапе вы можете следовать [Руководство по установке](/index.php/%D0%A0%D1%83%D0%BA%D0%BE%D0%B2%D0%BE%D0%B4%D1%81%D1%82%D0%B2%D0%BE_%D0%BF%D0%BE_%D1%83%D1%81%D1%82%D0%B0%D0%BD%D0%BE%D0%B2%D0%BA%D0%B5 "Руководство по установке").

## Альтернативные способы

Как видно из меню syslinux, существует несколько других альтернатив:

### NFS

Вам нужно будет настроить [сервер NFS](/index.php/NFS_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "NFS (Русский)") с экспортом в корне вашего смонтированного установочного носителя, который будет `/mnt/archiso`, если вы следовали за разделом [#Подготовка](#.D0.9F.D0.BE.D0.B4.D0.B3.D0.BE.D1.82.D0.BE.D0.B2.D0.BA.D0.B0). После настройки сервера добавьте следующую строку в файл `/etc/exports`:

 `/etc/exports` 
```
mnt/archiso 192.168.0.0/24(ro,no_subtree_check)

```

Если сервер уже запущен, повторно экспортируйте файловые системы с помощью `exportfs -r -a -v`.

Настройки по умолчанию в установщике ожидают найти NFS в `/run/archiso/bootmnt`, поэтому вам нужно будет отредактировать параметры загрузки. Для этого нажмите вкладку в соответствующем выборе меню загрузки и отредактируйте параметр `archiso_nfs_srv` соответственно:

```
archiso_nfs_srv=${pxeserver}:/mnt/archiso

```

Кроме того, вы можете использовать `/run/archiso/bootmnt` для всего процесса.

После загрузки образа ядра начальной загрузки Arch скопирует корневую файловую систему через NFS на загрузочный хост. Это может занять некоторое время. Как только это завершится, у вас появится работающая система.

### NBD

[Установите](/index.php/%D0%A3%D1%81%D1%82%D0%B0%D0%BD%D0%BE%D0%B2%D0%B8%D1%82%D0%B5 "Установите") пакет [nbd](https://www.archlinux.org/packages/?name=nbd) и настройте его:

 `/etc/nbd-server/config` 
```
[generic]
[archiso]
    readonly = true
    exportname = /srv/archlinux-2017.12.01-x86_64.iso
```

[Запустите](/index.php/%D0%97%D0%B0%D0%BF%D1%83%D1%81%D1%82%D0%B8%D1%82%D0%B5 "Запустите") `nbd.service`.

### Существующий сервер PXE

Если у вас есть PXE-сервер с настроенной системой [PXELINUX](/index.php/PXELINUX_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "PXELINUX (Русский)") (например, комбинация DHCP и [TFTP](/index.php/TFTP "TFTP")), вы можете добавить в файл `pxelinux.cfg` следующие пункты меню, чтобы загрузить Arch предпочтительным для вас способом:

```
LABEL 2
        MENU LABEL Arch Linux x86_64
        LINUX */path/to/extracted/Arch/ISO*/arch/boot/x86_64/vmlinuz
        NITRD */path/to/extracted/Arch/ISO*/arch/boot/intel_ucode.img,*/path/to/extracted/Arch/ISO*/arch/boot/x86_64/archiso.img
        APPEND archisobasedir=arch archiso_http_srv=*http://httpserver/path/to/extracted/Arch/ISO*/ ip=::
        SYSAPPEND 2
        TEXT HELP
        Arch Linux 2017.12.01 x86_64
        ENDTEXT
```

Вы можете заменить `archiso_http_srv` на `archiso_nfs_srv` для NFS или `archiso_nbd_srv` для NBD. Добавление инструкции `ip=` необходимо, чтобы дать указание ядру вызвать сетевой интерфейс, прежде чем попытаться смонтировать установочный носитель по сети. Смотрите [README.bootparams](https://git.archlinux.org/archiso.git/plain/docs/README.bootparams), чтобы узнать доступные параметры загрузки.

### Ошибка переименования интерфейса DHCP

[FS#36749](https://bugs.archlinux.org/task/36749) вызывает [предсказуемое переименование сетевого интерфейса](http://www.freedesktop.org/wiki/Software/systemd/PredictableNetworkInterfaceNames/) по умолчанию, а затем отказ клиента dhcp из-за него. Обходным путем является добавление параметра загрузки ядра `net.ifnames=0`, чтобы отключить предсказуемые имена интерфейсов.

### Системы с небольшим объемом памяти

Опция `copytoram` [initramfs](/index.php/Initramfs "Initramfs") может использоваться для контроля того, должна ли корневая файловая система полностью копироваться в оперативную память в полном объеме в начале загрузки.

Настоятельно рекомендуется оставить этот параметр в покое, и его следует отключать только в случае необходимости (системы с физической памятью размером менее 256 МБ). Если вы хотите это сделать, добавьте `copytoram=n` в строку ядра.

**Примечание:** Поскольку для этого требуются loop-mounting squashfs из смонтированной удаленной файловой системе, `copytoram=n` и `[archiso_pxe_http](#HTTP)` являются взаимоисключающими.

## Смотрите также

*   [PXE](http://xgu.ru/wiki/PXE)