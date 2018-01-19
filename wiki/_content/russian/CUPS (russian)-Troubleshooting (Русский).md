Ссылки по теме

*   [CUPS (Русский)](/index.php/CUPS_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "CUPS (Русский)")
*   [CUPS/Принтероспецифичные проблемы](/index.php/CUPS/%D0%9F%D1%80%D0%B8%D0%BD%D1%82%D0%B5%D1%80%D0%BE%D1%81%D0%BF%D0%B5%D1%86%D0%B8%D1%84%D0%B8%D1%87%D0%BD%D1%8B%D0%B5_%D0%BF%D1%80%D0%BE%D0%B1%D0%BB%D0%B5%D0%BC%D1%8B "CUPS/Принтероспецифичные проблемы")

**Состояние перевода:** На этой странице представлен перевод статьи [CUPS/Troubleshooting](/index.php/CUPS/Troubleshooting "CUPS/Troubleshooting"). Дата последней синхронизации: 9 января 2018\. Вы можете [помочь](/index.php/ArchWiki_Translation_Team_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "ArchWiki Translation Team (Русский)") синхронизировать перевод, если в английской версии произошли [изменения](https://wiki.archlinux.org/index.php?title=CUPS/Troubleshooting&diff=0&oldid=506747).

В этой статье рассматриваются все неспецифические (то есть не связанные с каким-либо одним принтером) проблемы CUPS и драйверов принтеров (но не проблемы, связанные с совместным использованием принтеров), включая методы определения точной природы проблемы и решения выявленной проблемы.

## Contents

*   [1 Введение](#.D0.92.D0.B2.D0.B5.D0.B4.D0.B5.D0.BD.D0.B8.D0.B5)
*   [2 Проблемы, возникающие в результате обновлений](#.D0.9F.D1.80.D0.BE.D0.B1.D0.BB.D0.B5.D0.BC.D1.8B.2C_.D0.B2.D0.BE.D0.B7.D0.BD.D0.B8.D0.BA.D0.B0.D1.8E.D1.89.D0.B8.D0.B5_.D0.B2_.D1.80.D0.B5.D0.B7.D1.83.D0.BB.D1.8C.D1.82.D0.B0.D1.82.D0.B5_.D0.BE.D0.B1.D0.BD.D0.BE.D0.B2.D0.BB.D0.B5.D0.BD.D0.B8.D0.B9)
    *   [2.1 CUPS останавливается](#CUPS_.D0.BE.D1.81.D1.82.D0.B0.D0.BD.D0.B0.D0.B2.D0.BB.D0.B8.D0.B2.D0.B0.D0.B5.D1.82.D1.81.D1.8F)
    *   [2.2 Для всех заданий - "остановлено"](#.D0.94.D0.BB.D1.8F_.D0.B2.D1.81.D0.B5.D1.85_.D0.B7.D0.B0.D0.B4.D0.B0.D0.BD.D0.B8.D0.B9_-_.22.D0.BE.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BB.D0.B5.D0.BD.D0.BE.22)
    *   [2.3 Для всех заданий - "Принтер не отвечает"](#.D0.94.D0.BB.D1.8F_.D0.B2.D1.81.D0.B5.D1.85_.D0.B7.D0.B0.D0.B4.D0.B0.D0.BD.D0.B8.D0.B9_-_.22.D0.9F.D1.80.D0.B8.D0.BD.D1.82.D0.B5.D1.80_.D0.BD.D0.B5_.D0.BE.D1.82.D0.B2.D0.B5.D1.87.D0.B0.D0.B5.D1.82.22)
    *   [2.4 Версия PPD не совместима с gutenprint](#.D0.92.D0.B5.D1.80.D1.81.D0.B8.D1.8F_PPD_.D0.BD.D0.B5_.D1.81.D0.BE.D0.B2.D0.BC.D0.B5.D1.81.D1.82.D0.B8.D0.BC.D0.B0_.D1.81_gutenprint)
    *   [2.5 Принтеры отсутствуют в диалоговом окне печати для приложений GTK3](#.D0.9F.D1.80.D0.B8.D0.BD.D1.82.D0.B5.D1.80.D1.8B_.D0.BE.D1.82.D1.81.D1.83.D1.82.D1.81.D1.82.D0.B2.D1.83.D1.8E.D1.82_.D0.B2_.D0.B4.D0.B8.D0.B0.D0.BB.D0.BE.D0.B3.D0.BE.D0.B2.D0.BE.D0.BC_.D0.BE.D0.BA.D0.BD.D0.B5_.D0.BF.D0.B5.D1.87.D0.B0.D1.82.D0.B8_.D0.B4.D0.BB.D1.8F_.D0.BF.D1.80.D0.B8.D0.BB.D0.BE.D0.B6.D0.B5.D0.BD.D0.B8.D0.B9_GTK3)
*   [3 Networking issues](#Networking_issues)
    *   [3.1 Unable to locate printer](#Unable_to_locate_printer)
    *   [3.2 Old CUPS server](#Old_CUPS_server)
    *   [3.3 Shared printer works locally but remote machine fails to print](#Shared_printer_works_locally_but_remote_machine_fails_to_print)
*   [4 USB printers](#USB_printers)
    *   [4.1 Conflict with SANE](#Conflict_with_SANE)
    *   [4.2 Conflict with usblp](#Conflict_with_usblp)
*   [5 HP issues](#HP_issues)
    *   [5.1 CUPS: "/usr/lib/cups/backend/hp failed"](#CUPS:_.22.2Fusr.2Flib.2Fcups.2Fbackend.2Fhp_failed.22)
    *   [5.2 CUPS: Job is shown as complete but the printer does nothing](#CUPS:_Job_is_shown_as_complete_but_the_printer_does_nothing)
    *   [5.3 CUPS: '"foomatic-rip" not available/stopped with status 3'](#CUPS:_.27.22foomatic-rip.22_not_available.2Fstopped_with_status_3.27)
    *   [5.4 CUPS: "Filter failed"](#CUPS:_.22Filter_failed.22)
        *   [5.4.1 Missing ghostscript](#Missing_ghostscript)
        *   [5.4.2 Missing foomatic-db](#Missing_foomatic-db)
        *   [5.4.3 Bad permissions](#Bad_permissions)
        *   [5.4.4 Avahi not enabled](#Avahi_not_enabled)
        *   [5.4.5 Out-of-date plugin](#Out-of-date_plugin)
        *   [5.4.6 Outdated printer configuration](#Outdated_printer_configuration)
    *   [5.5 CUPS: prints only an empty and an error-message page on HP LaserJet](#CUPS:_prints_only_an_empty_and_an_error-message_page_on_HP_LaserJet)
    *   [5.6 HPLIP 3.13: Plugin is installed, but HP Device Manager complains it is not](#HPLIP_3.13:_Plugin_is_installed.2C_but_HP_Device_Manager_complains_it_is_not)
    *   [5.7 hp-toolbox: "Unable to communicate with device"](#hp-toolbox:_.22Unable_to_communicate_with_device.22)
        *   [5.7.1 Permission problem](#Permission_problem)
        *   [5.7.2 Virtual CDROM printers](#Virtual_CDROM_printers)
        *   [5.7.3 Networked printers](#Networked_printers)
    *   [5.8 hp-setup asks to specify the PPD file for the discovered printer](#hp-setup_asks_to_specify_the_PPD_file_for_the_discovered_printer)
    *   [5.9 hp-setup: "Qt/PyQt 4 initialization failed"](#hp-setup:_.22Qt.2FPyQt_4_initialization_failed.22)
    *   [5.10 hp-setup: finds the printer automatically but reports "Unable to communicate with device" when printing test page immediately afterwards](#hp-setup:_finds_the_printer_automatically_but_reports_.22Unable_to_communicate_with_device.22_when_printing_test_page_immediately_afterwards)
*   [6 Other](#Other)
    *   [6.1 Printer "Paused" or "Stopped" with Status "Rendering completed"](#Printer_.22Paused.22_or_.22Stopped.22_with_Status_.22Rendering_completed.22)
        *   [6.1.1 Low ink](#Low_ink)
        *   [6.1.2 Permission issue](#Permission_issue)
    *   [6.2 Printing fails with unauthorised error](#Printing_fails_with_unauthorised_error)
    *   [6.3 Unknown supported format: application/postscript](#Unknown_supported_format:_application.2Fpostscript)
    *   [6.4 Print-Job client-error-document-format-not-supported](#Print-Job_client-error-document-format-not-supported)
    *   [6.5 Unable to get list of printer drivers](#Unable_to_get_list_of_printer_drivers)
    *   [6.6 lp: Error - Scheduler Not Responding](#lp:_Error_-_Scheduler_Not_Responding)
    *   [6.7 "Using invalid Host" error message](#.22Using_invalid_Host.22_error_message)
    *   [6.8 Cannot print from LibreOffice](#Cannot_print_from_LibreOffice)
    *   [6.9 Printer output shifted](#Printer_output_shifted)
    *   [6.10 Printer becomes stuck after a problem](#Printer_becomes_stuck_after_a_problem)
    *   [6.11 Samsung: URF ERROR - Incomplete Session by time out](#Samsung:_URF_ERROR_-_Incomplete_Session_by_time_out)
    *   [6.12 Brother: Printer prints multiple copies](#Brother:_Printer_prints_multiple_copies)
    *   [6.13 Regular user cannot change properties of the printer or remove certain jobs](#Regular_user_cannot_change_properties_of_the_printer_or_remove_certain_jobs)

## Введение

Наилучший способ борьбы с неисправностями - это выставить 'LogLevel' в файле `/etc/cups/cupsd.conf` на:

```
LogLevel debug

```

А потом посмотреть вывод из файла `/var/log/cups/error_log` например так:

```
# tail -n 100 -f /var/log/cups/error_log

```

Символы слева от вывода означают следующее:

*   D=Debug(отладка)
*   E=Error(ошибка)
*   I=Information(информация)
*   И так далее

Следующие файлы также могут быть полезны:

*   `/var/log/cups/page_log` - каждый раз при успешной печати, пишет новую запись
*   `/var/log/cups/access_log` - записывает всю активность на cupsd http1.1 сервере

Также, если вы хотите решить свои проблемы, важно понимать, как вообще работает CUPS. Вот краткая информация об этом:

1.  Когда вы жмёте 'печать' приложение отправляет .ps-файл (PostScript, язык-скрипт, который описывает, как выглядит страница) в систему CUPS (так происходит в большинстве программ).
2.  CUPS смотрит на PPD-файл (файл описания принтера) и находит, фильтры которые ему нужно использовать для преобразования .ps-файла в файл, который понимает ваш принтер (например, PJL,PCL). Обычно для этого ему требуется ghostscript.
3.  GhostScript принимает ввод и решает, какие фильтры ему использовать, потом применяет их и преобразовывает .ps-файл в формат, который понимает принтер.
4.  Затем файл передается бэкенду. Например, если у вас принтер подключен к usb порту, то используется usb бэкенд

Распечатайте документ и посмотрите `error_log`, чтобы получить более подробное и правильное представление об процессе печати.

## Проблемы, возникающие в результате обновлений

*Проблемы возникшие после обновления CUPS и сопутствующего ему набора программ*

### CUPS останавливается

Существует вероятность, что для правильной работы в обновленной версии понадобится новый файл конфигурации. Например, получение сообщения "404 - page not found" при попытке входа в панель управления CUPS через localhost:631.

Для того, чтобы воспользоваться новым конфигом, скопируйте `/etc/cups/cupsd.conf.default` в `/etc/cups/cupsd.conf` (при необходимости сделайте резервную копию старого конфига) и, чтобы новые настройки вступили в силу, перезапустите CUPS.

### Для всех заданий - "остановлено"

Если для всех отправленных на печать заданий установился статус "остановлено" ("stopped"), - удалите принтер и установите его заново. Для этого войдите в [веб-интерфейс CUPS](http://localhost:631), перейдите Принтеры > Удалить Принтер.

Для проверки настроек принтера перейдите во вкладку *Принтеры*, затем скопируйте отображаемую информацию. Далее нажмите на *Администрирование*. В выпадающем списке кликните *Изменить принтер*, перейдите к следующей странице(ам), и так далее.

### Для всех заданий - "Принтер не отвечает"

Для сетевых принтеров, поскольку CUPS подключается через URI, необходимо убедиться, что в DNS настроен доступ к принтерам по IP. Например, если принтер подключен следующим образом:

```
lpd://BRN_020554/BINARY_P1

```

то имя хоста 'BRN_020554' должно соответствовать IP принтера, управляемого сервером CUPS. Если используется [Avahi](/index.php/Avahi "Avahi"), убедитесь, что [разрешение имени хоста Avahi](/index.php/Avahi#Hostname_resolution "Avahi") работает.

Альтернативно, замените имя хоста, используемое в URI, IP-адресом принтера.

### Версия PPD не совместима с gutenprint

Запустите:

```
# /usr/bin/cups-genppdupdate

```

И перезагрузите CUPS (будет выведено соответствующее сообщение после установки gutenprint).

### Принтеры отсутствуют в диалоговом окне печати для приложений GTK3

Начиная с версии GTK3 3.22 требовался пакет gtk3-print-backends, но сейчас он снова объединен с gtk3.

(**Устаревшее**) Признаки и симптомы: принтеры не отображаются в диалоговом окне печати GTK3, что делает невозможным отправить на печать непосредственно из таких приложений, как [gedit](/index.php/Gedit "Gedit"), [Chromium](/index.php/Chromium_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Chromium (Русский)") и [Firefox](/index.php/Firefox_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Firefox (Русский)"); но принтеры все еще отображаются в веб-интерфейсе CUPS и lpstat, и отправка на печать из интерфейса командной строки или приложений GTK2 (например, GIMP) работает.

## Networking issues

### Unable to locate printer

Even if CUPS can detect networked printers, you may still end up with an "Unable to locate printer" error when trying to print something. The solution to this problem is to enable Avahi's [.local hostname resolution](/index.php/Avahi#Hostname_resolution "Avahi"). See [CUPS#Network](/index.php/CUPS#Network "CUPS") for details.

### Old CUPS server

As of CUPS version 1.6, the client defaults to IPP 2.0\. If the server uses CUPS <= 1.5 / IPP <= 1.1, the client does not downgrade the protocol automatically and thus cannot communicate with the server. A workaround is to append the `version=1.1` option documented at [[1]](https://www.cups.org/doc/network.html#TABLE2) to the URI.

### Shared printer works locally but remote machine fails to print

This is caused by a print job being sent through a filter twice, once on the local machine and once on the remote. See also the warning on the main [CUPS](/index.php/CUPS#Network_2 "CUPS") page.

## USB printers

### Conflict with SANE

If you are also running [SANE](/index.php/SANE "SANE"), it's possible that it is conflicting with CUPS. To fix this create a [Udev](/index.php/Udev "Udev") rule marking the device as matched by libsane:

 `/etc/udev/rules.d/99-printer.rules`  `ATTRS{idVendor}=="*vendor id*", ATTRS{idProduct}=="*product id*", MODE="0664", GROUP="lp", ENV{libsane_matched}="yes"` 

### Conflict with usblp

USB printers can be accessed using two methods: The usblp kernel module and libusb. The former is the classic way. It is simple: data is sent to the printer by writing it to a device file as a simple serial data stream. Reading the same device file allows bi-di access, at least for things like reading out ink levels, status, or printer capability information (PJL). It works very well for simple printers, but for multi-function devices (printer/scanner) it is not suitable and manufacturers like HP supply their own backends. Source: [here](http://lists.linuxfoundation.org/pipermail/printing-architecture/2012/002412.html).

**Warning:** As of [cups](https://www.archlinux.org/packages/?name=cups) version 1.6.0, it should no longer be necessary to blacklist the `usblp` kernel module. If you find out this is the only way to fix a remaining issue please report this upstream to the CUPS bug tracker and maybe also get in contact with Till Kamppeter (Debian CUPS maintainer). See [upstream bug](http://cups.org/str.php?L4128) for more info.

If you have problems getting your USB printer to work, you can try [blacklisting](/index.php/Blacklisting "Blacklisting") the `usblp` [kernel module](/index.php/Kernel_module "Kernel module"):

 `/etc/modprobe.d/blacklistusblp.conf` 
```
blacklist usblp

```

Custom kernel users may need to manually load the `usbcore` [kernel module](/index.php/Kernel_module "Kernel module") before proceeding.

Once the modules are installed, plug in the printer and check if the kernel detected it by running the following:

```
# journalctl -e

```

or

```
# dmesg

```

If you are using `usblp`, the output should indicate that the printer has been detected like so:

```
Feb 19 20:17:11 kernel: printer.c: usblp0: USB Bidirectional
printer dev 2 if 0 alt 0 proto 2 vid 0x04E8 pid 0x300E
Feb 19 20:17:11 kernel: usb.c: usblp driver claimed interface cfef3920
Feb 19 20:17:11 kernel: printer.c: v0.13: USB Printer Device Class driver

```

If you blacklisted `usblp`, you will see something like:

```
usb 3-2: new full speed USB device using uhci_hcd and address 3
usb 3-2: configuration #1 chosen from 1 choice

```

## HP issues

See also [CUPS/Printer-specific problems#HP](/index.php/CUPS/Printer-specific_problems#HP "CUPS/Printer-specific problems").

### CUPS: "/usr/lib/cups/backend/hp failed"

Make sure dbus is installed and running. If the error persists, try starting avahi-daemon.

Try adding the printer as a Network Printer using the http:// protocol.

**Note:** There might need to set permissions issues right.

### CUPS: Job is shown as complete but the printer does nothing

This happens on HP printers when you select the (old) hpijs driver (e.g. the Deskjet D1600 series). Use the hpcups driver instead.

Some HP printers require their firmware to be downloaded from the computer every time the printer is switched on. If there is an issue with udev (or equivalent) and the firmware download rule is never fired, you may experience this issue. As a workaround, you can manually download the firmware to the printer. Ensure the printer is plugged in and switched on, then run

```
hp-firmware -n

```

### CUPS: '"foomatic-rip" not available/stopped with status 3'

If receiving any of the following error messages in `/var/log/cups/error_log` while using a HP printer, with jobs appearing to be processed while they all end up not being completed with their status set to 'stopped':

```
Filter "foomatic-rip" for printer *printer_name* not available: No such file or director

```

or:

```
PID *pid* (/usr/lib/cups/filter/foomatic-rip) stopped with status 3!

```

make sure [hplip](https://www.archlinux.org/packages/?name=hplip) has been [installed](/index.php/Installed "Installed").

### CUPS: "Filter failed"

A "filter failed" error can be caused by any number of issues. The CUPS error log (by default `/var/log/cups/error_log`) should record which filter failed and why.

#### Missing ghostscript

Install [ghostscript](https://www.archlinux.org/packages/?name=ghostscript) (`/usr/lib/cups/filter/gstoraster` needs it to run).

#### Missing foomatic-db

Install [foomatic-db](https://www.archlinux.org/packages/?name=foomatic-db) and [foomatic-db-ppds](https://www.archlinux.org/packages/?name=foomatic-db-ppds). This fixes it in some cases.

#### Bad permissions

Change the permissions of the printer USB port. Get the bus and device number from `lsusb`, then set the permission using:

 ` lsusb `  ` Bus <BUSID> Device <DEVID>: ID <PRINTERID>:<VENDOR> Hewlett-Packard DeskJet D1360` 

Then substitute the provided device information to the

```
# chmod 0666 /dev/bus/usb/<BUSID>/<DEVID>

```

To make the persistent permission change that will be triggered automatically each time the computer is rebooted, add the following line.

 `/etc/udev/rules.d/10-local.rules`  `SUBSYSTEM=="usb", ATTRS{idVendor}=="<VENDOR>", ATTRS{idProduct}=="<PRINTERID>", GROUP="lp", MODE:="666"` 

Each system may vary, so consult [udev#List attributes of a device](/index.php/Udev#List_attributes_of_a_device "Udev") wiki page.

#### Avahi not enabled

[Start](/index.php/Start "Start"), and [enable](/index.php/Enable "Enable") the `avahi-daemon` service.

#### Out-of-date plugin

This error can also indicate that the plugin is out of date (version is mismatched). If you have installed [hplip-plugin](https://aur.archlinux.org/packages/hplip-plugin/), you will need to update the package.

#### Outdated printer configuration

As of [hplip-plugin](https://aur.archlinux.org/packages/hplip-plugin/) v3.17.11 hpijs is not longer available. If you have printers using hpijs they will fail to print. You must modify them and select the new hpcups driver instead.

You can check if this is your case looking at cups error_log:

 ` $ cat /var/log/cups/error_log | grep hpijs ` 
```
 ...
 D [09/Jan/2018:14:32:58 +0000] [Job 97] **sh: hpijs: command not found**
 ...
```

### CUPS: prints only an empty and an error-message page on HP LaserJet

There is a bug that causes CUPS to fail when printing images on HP LaserJet (in my case 3380). The bug has been reported and fixed by [Ubuntu](https://bugs.launchpad.net/ubuntu/+source/cups-filters/+bug/998087). The first page is empty, the second page contains the following error message:

```
 ERROR:
 invalidaccess
 OFFENDING COMMAND:
 filter
 STACK:
 /SubFileDecode
 endstream
 ...

```

In order to fix the issue, run the following command as root:

```
# lpadmin -p *printer* -o pdftops-renderer-default=pdftops

```

### HPLIP 3.13: Plugin is installed, but HP Device Manager complains it is not

The issue might have to do with the file permission change that had been made to `/var/lib/hp/hplip.state`. To correct the issue, a simple `chmod 644 /var/lib/hp/hplip.state` and `chmod 755 /var/lib/hp` should be sufficient. For further information, please read this [link](https://bugs.launchpad.net/hplip/+bug/1131596).

### hp-toolbox: "Unable to communicate with device"

```
# hp-toolbox
# error: Unable to communicate with device (code=12): hp:/usb/*printer id*

```

#### Permission problem

It may be needed to add the user to the `lp` and `sys` [groups](/index.php/Group "Group").

#### Virtual CDROM printers

This can also be caused by printers such as the P1102 that provide a virtual CD-ROM drive for MS Windows drivers. The lp dev appears and then disappears. In that case, try the **usb-modeswitch** and **usb-modeswitch-data** packages, that lets one switch off the "Smart Drive" (udev rules included in said packages).

#### Networked printers

This can also occur with network attached printers using dynamic hostnames if the [avahi-daemon](/index.php/Avahi "Avahi") is not running. Another possibility is that *hp-setup* failed to locate the printer because the IP address of the the printer changed due to DHCP. If this is the case, consider adding a DHCP reservation for the printer in the DHCP server's configuration.

### hp-setup asks to specify the PPD file for the discovered printer

Install and start CUPS before running hp-setup.

### hp-setup: "Qt/PyQt 4 initialization failed"

[Install](/index.php/Install "Install") [python-pyqt4](https://www.archlinux.org/packages/?name=python-pyqt4), which is an optdepend of [hplip](https://www.archlinux.org/packages/?name=hplip). Alternatively, to run hp-setup with the command line interface, use the `-i` flag.

### hp-setup: finds the printer automatically but reports "Unable to communicate with device" when printing test page immediately afterwards

This at least happens to hplip 3.13.5-2 for HP Officejet 6500A through local network connection. To solve the problem, specify the IP address of the HP printer for hp-setup to locate the printer.

## Other

### Printer "Paused" or "Stopped" with Status "Rendering completed"

#### Low ink

When low on ink, some printers will get stuck in "Rendering completed" status and, if it is a network printer, the printer may even become unreachable from CUPS' perspective despite being properly connected to the network. Replacing the low/depleted ink cartridge(s) in this setting will return the printer to "Ready" status and, if it is a network printer, will make the printer available to CUPS again.

**Note:** If you use third-party ink cartridges, the ink levels reported by the printer may be inaccurate. If you use third-party ink and your printer used to work fine but is now getting stuck on "Rendering completed" status, replace the ink cartridges regardless of the reported ink levels before trying other fixes.

#### Permission issue

Prior to [cups](https://www.archlinux.org/packages/?name=cups) 2.0.0-2, if the group set in the `Group` directive is also listed in the `SystemGroup` directive in `/etc/cups/cups-files.conf`, `cupsd` will instead run any helper programs with a group of `nobody`. However, the helpers may need to write to printer devices, which are created with user `root` and group `lp`, and will be unable to if they are run with a group of `nobody`, causing the print queue to become "Paused" or "Stopped".

To fix this, ensure that the the `Group` directive is set to `lp`, and the `SystemGroup` directive does not include `lp`.

Fixed in Arch with [[2]](https://git.archlinux.org/svntogit/packages.git/commit/trunk?h=packages/cups&id=c20b22f4f996cb08b1aa856d4c8991e869459eb2).

### Printing fails with unauthorised error

If a remote printer requests authentication CUPS will automatically add an `AuthInfoRequired` directive to the printer in `/etc/cups/printers.conf`. However, some graphical applications (for instance, some versions of [LibreOffice](/index.php/LibreOffice "LibreOffice") [[3]](https://bugs.documentfoundation.org/show_bug.cgi?id=53029)) have no way to prompt for credentials, so printing fails. To fix this include the required username and password in the URI. See [[4]](https://bugs.launchpad.net/ubuntu/+source/cups/+bug/283811), [[5]](https://bbs.archlinux.org/viewtopic.php?id=61826).

### Unknown supported format: application/postscript

Comment the lines:

```
application/octet-stream        application/vnd.cups-raw        0      -

```

from `/etc/cups/mime.convs`, and:

```
application/octet-stream

```

in `/etc/cups/mime.types`.

### Print-Job client-error-document-format-not-supported

Try installing the foomatic packages and use a foomatic driver.

### Unable to get list of printer drivers

(Also applicable to error "-1 not supported!")

Try to remove Foomatic drivers or refer to [CUPS/Printer-specific problems#HPLIP Driver](/index.php/CUPS/Printer-specific_problems#HPLIP_Driver "CUPS/Printer-specific problems") for a workaround.

### lp: Error - Scheduler Not Responding

If you get this error, ensure [CUPS](/index.php/CUPS "CUPS") is running, the environmental variable `CUPS_SERVER` is unset, and that `/etc/cups/client.conf` is correct.

### "Using invalid Host" error message

Try adding `ServerAlias *` into `/etc/cups/cupsd.conf`.

### Cannot print from LibreOffice

If you can print a test page from the [CUPS](/index.php/CUPS "CUPS") web interface, but not from [LibreOffice](/index.php/LibreOffice "LibreOffice"), try to [install](/index.php/Install "Install") the [a2ps](https://www.archlinux.org/packages/?name=a2ps) package.

### Printer output shifted

This seems to be caused by the wrong page size being set in [CUPS](/index.php/CUPS "CUPS").

### Printer becomes stuck after a problem

When an issue arises during printing, the printer in CUPS may become unresponsive. `lpq` reports that the printer `is not ready`, and it can be reactivated using `cupsenable`. In the CUPS web interface, the printer is shown as *Paused*, and can be reactivated by *resuming* the printer.

To automatically have CUPS reactivate the printer, change [ErrorPolicy](https://www.cups.org/doc/man-cupsd.conf.html?TOPIC=Man+Pages#ErrorPolicy) from the default `stop-printer` to `retry-this-job`.

### Samsung: URF ERROR - Incomplete Session by time out

This error is usually encountered when printing files over the network through IPP to a Samsung printer, and is solved by using the [samsung-unified-driver](https://aur.archlinux.org/packages/samsung-unified-driver/) package.

**Note:** The corresponding error code 11-1112 corresponds to an internal wiring problem with the printer, so contacting Samsung's tech support is futile.

### Brother: Printer prints multiple copies

Sometimes the printer will print multiple copies of a document (for instance a MFC-9330CDW printed 10 copies). The solution is to [update the printer firmware](/index.php/CUPS/Printer-specific_problems#Updating_the_firmware "CUPS/Printer-specific problems").

### Regular user cannot change properties of the printer or remove certain jobs

If a regular user needs to be able to change the printers properties or manage the printer queue, the user may need to be added to the `sys` group.