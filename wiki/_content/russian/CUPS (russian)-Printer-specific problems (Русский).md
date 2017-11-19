Ссылки по теме

*   [CUPS (Русский)](/index.php/CUPS_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "CUPS (Русский)")
*   [CUPS/Troubleshooting](/index.php/CUPS/Troubleshooting "CUPS/Troubleshooting")

**Состояние перевода:** На этой странице представлен перевод статьи [CUPS/Printer-specific problems](/index.php/CUPS/Printer-specific_problems "CUPS/Printer-specific problems"). Дата последней синхронизации: 17 ноября 2017\. Вы можете [помочь](/index.php/ArchWiki_Translation_Team_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "ArchWiki Translation Team (Русский)") синхронизировать перевод, если в английской версии произошли [изменения](https://wiki.archlinux.org/index.php?title=CUPS/Printer-specific_problems&diff=0&oldid=497004).

Эта статья содержит инструкции по настройки [CUPS](/index.php/CUPS_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "CUPS (Русский)") для конкретных моделей принтеров. Если ваш принтер не упомянается здесь, или если ни один из перечисленных драйверов не работает, посмотрите на сайте [OpenPrinting](http://www.openprinting.org/printers).

**Примечание:** Если вы добавите принтер в этот список, подумайте о том, чтобы внести свой вклад в [OpenPrinting](https://wiki.linuxfoundation.org/openprinting/database/databaseintro) - таким образом и для пользователей других дистрибутивов эта информация будет полезна!

## Contents

*   [1 Brother](#Brother)
    *   [1.1 Сетевые принтеры](#.D0.A1.D0.B5.D1.82.D0.B5.D0.B2.D1.8B.D0.B5_.D0.BF.D1.80.D0.B8.D0.BD.D1.82.D0.B5.D1.80.D1.8B)
    *   [1.2 Пользовательские драйверы](#.D0.9F.D0.BE.D0.BB.D1.8C.D0.B7.D0.BE.D0.B2.D0.B0.D1.82.D0.B5.D0.BB.D1.8C.D1.81.D0.BA.D0.B8.D0.B5_.D0.B4.D1.80.D0.B0.D0.B9.D0.B2.D0.B5.D1.80.D1.8B)
        *   [1.2.1 Установка вручную из пакетов RPM](#.D0.A3.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B0_.D0.B2.D1.80.D1.83.D1.87.D0.BD.D1.83.D1.8E_.D0.B8.D0.B7_.D0.BF.D0.B0.D0.BA.D0.B5.D1.82.D0.BE.D0.B2_RPM)
    *   [1.3 Обновление прошивки](#.D0.9E.D0.B1.D0.BD.D0.BE.D0.B2.D0.BB.D0.B5.D0.BD.D0.B8.D0.B5_.D0.BF.D1.80.D0.BE.D1.88.D0.B8.D0.B2.D0.BA.D0.B8)
*   [2 Canon](#Canon)
    *   [2.1 CARPS](#CARPS)
    *   [2.2 USB over IP (BJNP)](#USB_over_IP_.28BJNP.29)
*   [3 Dell](#Dell)
*   [4 Epson](#Epson)
    *   [4.1 Utilities](#Utilities)
        *   [4.1.1 escputil](#escputil)
        *   [4.1.2 mtink](#mtink)
        *   [4.1.3 Stylus-toolbox](#Stylus-toolbox)
    *   [4.2 Custom drivers](#Custom_drivers)
        *   [4.2.1 Avasys](#Avasys)
*   [5 HP](#HP)
    *   [5.1 HPLIP Driver](#HPLIP_Driver)
*   [6 Konica](#Konica)
*   [7 Lexmark](#Lexmark)
    *   [7.1 Utilities](#Utilities_2)
    *   [7.2 Custom drivers](#Custom_drivers_2)
*   [8 Oki](#Oki)
*   [9 Ricoh](#Ricoh)
*   [10 Samsung](#Samsung)
*   [11 Xerox or FujiXerox](#Xerox_or_FujiXerox)
    *   [11.1 Custom drivers](#Custom_drivers_3)
        *   [11.1.1 Phaser 3100MFP](#Phaser_3100MFP)
        *   [11.1.2 Phaser 6000B](#Phaser_6000B)
        *   [11.1.3 Phaser 6125N](#Phaser_6125N)

## Brother

| Принтер | Драйвер/фильтр | Примечание |
| DCP-135C | [brother-dcp135c](https://aur.archlinux.org/packages/brother-dcp135c/) |
| DCP-150C | [brother-dcp150c](https://aur.archlinux.org/packages/brother-dcp150c/) |
| DCP-7020 | [foomatic](/index.php/CUPS_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#Foomatic "CUPS (Русский)") | Или драйвер Brother. |
| DCP-7030 | [brother-dcp7030](https://aur.archlinux.org/packages/brother-dcp7030/) |
| DCP-7065DN | [brother-dcp7065dn](https://aur.archlinux.org/packages/brother-dcp7065dn/) |
| FAX-2820 | [brother-cups-wrapper-laser](https://aur.archlinux.org/packages/brother-cups-wrapper-laser/) |
| FAX-2840 | [brother-fax2840](https://aur.archlinux.org/packages/brother-fax2840/) | Или [foomatic](/index.php/CUPS_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#Foomatic "CUPS (Русский)") - работает в основном с `hpijs-pcl5e.ppd`. То же, что и HL-2170W. |
| FAX-2940 | [brother-fax2940](https://aur.archlinux.org/packages/brother-fax2940/) |
| HL-2030 | [foomatic](/index.php/CUPS_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#Foomatic "CUPS (Русский)") | Или [brother-hl2030](https://aur.archlinux.org/packages/brother-hl2030/) |
| HL-2035 | [foomatic](/index.php/CUPS_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#Foomatic "CUPS (Русский)") | Должен быть совместим с любыми драйверами для HL-2030. |
| HL-2040 | [foomatic](/index.php/CUPS_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#Foomatic "CUPS (Русский)") | Или [brother-hl2040](https://aur.archlinux.org/packages/brother-hl2040/) |
| HL-2130 | [foomatic](/index.php/CUPS_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#Foomatic "CUPS (Русский)") (с использованием драйвера HL-2140) | Или [hplip](https://www.archlinux.org/packages/?name=hplip) |
| HL-2140 | [foomatic](/index.php/CUPS_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#Foomatic "CUPS (Русский)") | Или [brother-hl2140](https://aur.archlinux.org/packages/brother-hl2140/) |
| HL-2170W | [foomatic](/index.php/CUPS_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#Foomatic "CUPS (Русский)") | Или драйвер Brother. |
| HL-2230 | [foomatic](/index.php/CUPS_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#Foomatic "CUPS (Русский)") | То же, что и HL-2170W. Выберите HL-2170W в качестве драйвера в администраторе CUPS при добавлении принтера. |
| HL-2250DN | [brother-hl2250dn](https://aur.archlinux.org/packages/brother-hl2250dn/) |
| HL-2270DW | [brother-hl2270dw](https://aur.archlinux.org/packages/brother-hl2270dw/) |
| HL-2280DW | [brother-hl2280dw](https://aur.archlinux.org/packages/brother-hl2280dw/) |
| HL-2340DW | [brother-hll2340dw](https://aur.archlinux.org/packages/brother-hll2340dw/) |
| HL-3045CN | Установите драйвер Brother. |
| HL-3140CW | [brother-hl3140cw](https://aur.archlinux.org/packages/brother-hl3140cw/) | Используйте драйвер IPP и Brother, чтобы избежать сокращения страниц и бесконечных распечаток |
| HL-3150CDW | [brother-hl3150cdw](https://aur.archlinux.org/packages/brother-hl3150cdw/) |
| HL-3170CDW | [brother-hl3170cdw](https://aur.archlinux.org/packages/brother-hl3170cdw/) |
| HL-5140 | [foomatic](/index.php/CUPS_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#Foomatic "CUPS (Русский)") | Или драйвер Brother. |
| HL-5340 | [foomatic](/index.php/CUPS_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#Foomatic "CUPS (Русский)") | Используйте *Generic PCL 6/PCL XL Printer - CUPS+Gutenprint* ([gutenprint](https://www.archlinux.org/packages/?name=gutenprint) и [foomatic-db-gutenprint-ppds](https://www.archlinux.org/packages/?name=foomatic-db-gutenprint-ppds)). Или драйвер Brother, который может привести к сбою печати с ошибками postscript. |
| HL-L2300D | [brother-hll2300d](https://aur.archlinux.org/packages/brother-hll2300d/) |
| HL-L2380DW | [brother-hll2380dw](https://aur.archlinux.org/packages/brother-hll2380dw/) |
| MFC-420CN | [brother-mfc-420cn](https://aur.archlinux.org/packages/brother-mfc-420cn/) |
| MFC-440CN | [brother-mfc-440cn](https://aur.archlinux.org/packages/brother-mfc-440cn/) |
| MFC-465CN | [brother-mfc-465cn](https://aur.archlinux.org/packages/brother-mfc-465cn/) |
| MFC-7360N | [brother-mfc7360n](https://aur.archlinux.org/packages/brother-mfc7360n/) |
| MFC-9320CW | Установите драйвер Brother. |
| MFC-9332CDW | [brother-mfc-9332cdw](https://aur.archlinux.org/packages/brother-mfc-9332cdw/) |
| MFC-9840CDW | [foomatic](/index.php/CUPS_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#Foomatic "CUPS (Русский)") | Или драйвер Brother. Этот принтер также работает с универсальным драйвером PCL-6 из пакета [gutenprint](https://www.archlinux.org/packages/?name=gutenprint). Используйте **pcl_p1**, как адрес принтера при использовании драйвера PCL-6. |
| MFC-J470DW | [brother-mfc-j470dw](https://aur.archlinux.org/packages/brother-mfc-j470dw/) |
| MFC-J5520DW | [brother-mfc-j5520dw](https://aur.archlinux.org/packages/brother-mfc-j5520dw/) |
| MFC-J5910DW | [brother-mfc-j5910dw](https://aur.archlinux.org/packages/brother-mfc-j5910dw/) |
| MFC-J650DW | Установите драйвер Brother. |
| MFC-J885DW | [brother-mfc-j885dw](https://aur.archlinux.org/packages/brother-mfc-j885dw/) |
| MFC-J985DW | [brother-mfc-j985dw](https://aur.archlinux.org/packages/brother-mfc-j985dw/) |
| MFC-L2700DW | [brother-mfc-l2700dw](https://aur.archlinux.org/packages/brother-mfc-l2700dw/) | Пожалуйста, посмотрите также комментарии на странице пакета в aur. |
| QL-500 | [brother-ql500](https://aur.archlinux.org/packages/brother-ql500/) |
| QL-570 | [brother-ql570](https://aur.archlinux.org/packages/brother-ql570/) |
| QL-580N | [brother-ql580n](https://aur.archlinux.org/packages/brother-ql580n/) |
| QL-650TD | [brother-ql650td](https://aur.archlinux.org/packages/brother-ql650td/) |
| QL-700 | [brother-ql700](https://aur.archlinux.org/packages/brother-ql700/) |
| QL-710W | [brother-ql710w](https://aur.archlinux.org/packages/brother-ql710w/) |
| QL-720NW | [brother-ql720nw](https://aur.archlinux.org/packages/brother-ql720nw/) |
| QL-1050 | [brother-ql1050](https://aur.archlinux.org/packages/brother-ql1050/) |
| QL-1050N | [brother-ql1050n](https://aur.archlinux.org/packages/brother-ql1050n/) |
| QL-1060 | [brother-ql1060n](https://aur.archlinux.org/packages/brother-ql1060n/) |
| TD-2020 | [brother-td2020](https://aur.archlinux.org/packages/brother-td2020/) |
| TD-2120N | [brother-td2120n](https://aur.archlinux.org/packages/brother-td2120n/) |
| TD-2130N | [brother-td2130n](https://aur.archlinux.org/packages/brother-td2130n/) |
| TD-4000 | [brother-td4000](https://aur.archlinux.org/packages/brother-td4000/) |
| TD-4100N | [brother-td4100n](https://aur.archlinux.org/packages/brother-td4100n/) |
| Принтер | Драйвер/фильтр | Примечание |

### Сетевые принтеры

Для сетевых принтеров используйте `ipp://**printer_ip**/ipp/port1` в качестве адреса принтера. Для некоторых старых принтеров это может не сработать. Если не сработало, попробуйте `lpd://**printer_ip**/BINARY_P1`.

Некоторые принтеры используют протокол сокета. Для этих принтеров используйте `socket://**printer_ip**:9100`. Для http используйте `http://**printer_ip**/POSTSCRIPT_P1`.

### Пользовательские драйверы

Brother предоставляет пользовательские драйверы на своем веб-сайте либо в исходном архиве, так и в формате rpm или deb. [Сборка драйверов принтера Brother](/index.php/Packaging_Brother_printer_drivers "Packaging Brother printer drivers") охватывает создание [PKGBUILD](/index.php/PKGBUILD_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "PKGBUILD (Русский)") из существующих пакетов RPM.

**Примечание:** Исходные пакеты могут быть лучшей альтернативой пакетам rpm, если они содержат все необходимые файлы.

#### Установка вручную из пакетов RPM

**Важно:** В идеале это должно быть автоматизировано в [PKGBUILD](/index.php/PKGBUILD_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "PKGBUILD (Русский)")

[Установите](/index.php/%D0%A3%D1%81%D1%82%D0%B0%D0%BD%D0%BE%D0%B2%D0%B8%D1%82%D0%B5 "Установите") пакет [rpmextract](https://www.archlinux.org/packages/?name=rpmextract) и извлеките оба пакета rpm с помощью `rpmextract.sh`. Извлечение обоих файлов создаст каталог var и usr - переместите содержимое обоих каталогов в соответствующие корневые каталоги.

Запустите файл оболочки CUPS в `/usr/local/Brother/cupswrapper`. Это должно автоматически установить и настроить ваш принтер brother.

### Обновление прошивки

[Установите](/index.php/%D0%A3%D1%81%D1%82%D0%B0%D0%BD%D0%BE%D0%B2%D0%B8%D1%82%D0%B5 "Установите") [net-snmp](https://www.archlinux.org/packages/?name=net-snmp) и запустите:

```
snmpwalk -c public $PRINTER_IP | grep -A 1 3.6.1.4.1.2435.2.4.3.99.3.1.6.1.2

```

На этом этапе у вас будут соответствующие данные, чтобы получить ссылку на прошивку от Brother. Файл должен выглядеть примерно так:

 `request.xml` 
```
 <REQUESTINFO>
    <FIRMUPDATETOOLINFO>
        <FIRMCATEGORY>MAIN</FIRMCATEGORY>
        <OS>LINUX</OS>
        <INSPECTMODE>1</INSPECTMODE>
    </FIRMUPDATETOOLINFO>

    <FIRMUPDATEINFO>
        <MODELINFO>
            <SELIALNO></SELIALNO>
            <NAME>MFC-9330CDW</NAME>
            <SPEC>0401</SPEC>
            <DRIVER></DRIVER>
            <FIRMINFO>
                <FIRM>
                    <ID>MAIN</ID>
                    <VERSION>R1506121801:4504</VERSION>
                </FIRM>
                <FIRM>
                    <ID>SUB1</ID>
                    <VERSION>1.07</VERSION>
                </FIRM>
                <FIRM>
                    <ID>SUB2</ID>
                    <VERSION>L1505291600</VERSION>
                </FIRM>
            </FIRMINFO>
        </MODELINFO>
        <DRIVERCNT>1</DRIVERCNT>
        <LOGNO>2</LOGNO>
        <ERRBIT></ERRBIT>
        <NEEDRESPONSE>1</NEEDRESPONSE>
    </FIRMUPDATEINFO>
 </REQUESTINFO>

```

Отправьте этот файл Brother:

```
curl -X POST -d @request.xml [https://firmverup.brother.co.jp/kne_bh7_update_nt_ssl/ifax2.asmx/fileUpdate](https://firmverup.brother.co.jp/kne_bh7_update_nt_ssl/ifax2.asmx/fileUpdate) -H "Content-Type:text/xml" > response.xml

```

В `response.xml` вы найдете тег `<PATH>`, содержащий URL-адрес загрузки прошивки. Затем загрузите прошивку, нажмите ее на принтер и дайте принтеру обработать ее. Прежде чем это сделать, измените пароль администратора на что-то известное, он будет использоваться как пользователь для входа на сайт FTP (ОЧЕНЬ плохая практика, не делайте этого).

```
wget [http://update-akamai.brother.co.jp/CS/LZ4266_W.djf](http://update-akamai.brother.co.jp/CS/LZ4266_W.djf)
ftp $PRINTER_IP
 bin
 hash
 send LZ4266_W.djf
 bye

```

При этом принтер перезагрузится, и последняя версия прошивки будет установлена и (надеюсь) проблемы с печатью будут решены.

## Canon

Существует много возможных драйверов для принтеров Canon. [Многие принтеры Canon](http://gimp-print.sourceforge.net/p_Supported_Printers.php) поддерживаются [gutenprint](https://www.archlinux.org/packages/?name=gutenprint). Некоторые из принтеров Canon LBP, iR и MF используют драйвер, поддерживающий протоколы UFR II/UFR II LT/LIPSLX, который доступен как [cndrvcups-lb](https://aur.archlinux.org/packages/cndrvcups-lb/) или [cndrvcups-lb-bin](https://aur.archlinux.org/packages/cndrvcups-lb-bin/). Другие используют драйверы [#CARPS](#CARPS) или [Canon CAPT](/index.php/Canon_CAPT "Canon CAPT").

| Принтер | Драйвер/фильтр | Примечание |
| iP4300 | [gutenprint](https://www.archlinux.org/packages/?name=gutenprint) | Или используйте драйвер Canon [cnijfilter-ip4300](https://aur.archlinux.org/packages/cnijfilter-ip4300/) или драйвер [TurboPrint](http://www.turboprint.info/). |
| LBP810 | [Canon CAPT](/index.php/Canon_CAPT "Canon CAPT") |
| LBP1120 |
| LBP1210 |
| LBP2900 |
| LBP3000 |
| LBP3010 |
| LBP3018 |
| LBP3050 |
| LBP3100 |
| LBP3108 |
| LBP3150 |
| LBP3200 |
| LBP3210 |
| LBP3250 |
| LBP3300 |
| LBP3310 |
| LBP3500 |
| LBP5000 |
| LBP5050 series |
| LBP5100 |
| LBP5300 |
| LBP6000 |
| LBP6018 |
| LBP6020 |
| LBP6200 |
| LBP6300 |
| LBP6300n |
| LBP6310dn |
| LBP7010C |
| LBP7018C |
| LBP7200Cdn (сетевой режим) |
| LBP7200C series |
| LBP7210Cdn |
| LBP9100C |
| MF4720w | [cndrvcups-lb-bin](https://aur.archlinux.org/packages/cndrvcups-lb-bin/) |
| MG4200 series | [cnijfilter-mg4200](https://aur.archlinux.org/packages/cnijfilter-mg4200/) |
| TS8050 | [cnijfilter2](https://aur.archlinux.org/packages/cnijfilter2/) | Без [cnijfilter2](https://aur.archlinux.org/packages/cnijfilter2/) печать завершится ошибкой фильтра или вы можете получить "рендеринг завершен", а принтер ничего не напечатает |
| TS9020 | [canon-ts9020](https://aur.archlinux.org/packages/canon-ts9020/) |
| Принтер | Драйвер/фильтр | Примечание |

Некоторые принтеры Canon будут использовать аналогичную настройку для iP4500, поэтому рассмотрите возможность изменения пакета [cnijfilter-ip4500](https://aur.archlinux.org/packages/cnijfilter-ip4500/) для других аналогичных принтеров.

### CARPS

Some of Canon's printers use Canon's proprietary Canon Advanced Raster Printing System (CARPS) driver. [Rainbow Software](http://www.rainbow-software.org/2014/01/23/cups-driver-for-canon-carps-printers/) have managed to reverse engineer the CARPS data format and have successfully created a CARPS CUPS driver, which is available as [carps-cups](https://aur.archlinux.org/packages/carps-cups/). The project's [GitHub](https://github.com/ondrej-zary/carps-cups) page includes a list of working printers.

### USB over IP (BJNP)

Some Canon printers use Canon's proprietary USB over IP BJNP protocol to communicate over the network. There is a CUPS backend for this, which is available as [cups-bjnp](https://aur.archlinux.org/packages/cups-bjnp/).

## Dell

| Printer | Driver/filter | Notes |
| 1250C | [foo2zjs-nightly](https://aur.archlinux.org/packages/foo2zjs-nightly/) | See [http://cybercom.net/~dcoffin/hbpl](http://cybercom.net/~dcoffin/hbpl), the patch has been merged into upstream. The printer may also work with the [Xerox Phaser 6000B driver](#Phaser_6000B). |
| E515,

E515dw

 | Install [Dell's driver](http://downloads.dell.com/FOLDER03040853M/1/Printer_E515dw_Driver_Dell_A00_LINUX.zip). | Both *e515dwcupswrapper-3.2.0-1.i386.deb* and *e515dwlpr-3.2.0-1.i386.deb* need to be installed. You could either write a [PKGBUILD](/index.php/PKGBUILD "PKGBUILD"), use [debtap](https://aur.archlinux.org/packages/debtap/), or use [dpkg](https://aur.archlinux.org/packages/dpkg/) (using dpkg is not recommended as the files will not be managed by [pacman](/index.php/Pacman "Pacman")). The driver works on both the x86_64 and i386 platforms, but may require [multilib](/index.php/Multilib "Multilib"). |
| Printer | Driver/filter | Notes |

## Epson

[epson-inkjet-printer-escpr](https://aur.archlinux.org/packages/epson-inkjet-printer-escpr/) is a driver for the Epson Inkjet Printer Driver (ESC/P-R) for Linux.

There is a large selection of printer drivers/filters available in the [AUR](/index.php/AUR "AUR").

| Printer | Driver/filter | Notes |
| AcuLaser CX11(NF) | [epson-alcx11-filter](https://aur.archlinux.org/packages/epson-alcx11-filter/) |
| AcuLaser C900 | This printer uses Epson's driver, with a device URI of '**usb://EPSON/AL-C900'**, and may need the pipsplus service to be running. |
| TX125 | [epson-inkjet-printer-n10-nx127](https://aur.archlinux.org/packages/epson-inkjet-printer-n10-nx127/) |
| LP-S5000 | This printer requires a [custom driver from Avasys](#Avasys). |
| Printer | Driver/filter | Notes |

### Utilities

#### escputil

escputil is part of the [gutenprint](https://www.archlinux.org/packages/?name=gutenprint) package, and performs some utility functions on Epson printers such as nozzle cleaning.

#### mtink

This is a printer status monitor which enables to get the remaining ink quantity, to print test patterns, to reset printer and to clean nozzle. It use an intuitive graphical user interface.

#### Stylus-toolbox

This is a GUI using escputil and cups drivers. It supports nearly all USB printer of Epson and displays ink quantity, can clean and align print heads and print test patterns.

### Custom drivers

#### Avasys

**Warning:** This section involves installing packages without [pacman](/index.php/Pacman "Pacman"). These directions should ideally be automated with a [PKGBUILD](/index.php/PKGBUILD "PKGBUILD").

"Source" code of the driver is available on the [avasys website](http://www.avasys.jp), in Japanese, however it includes a 32 bit binary which will cause problem on 64 bit system.

*   [Install](/index.php/Install "Install") the [psutils](https://www.archlinux.org/packages/?name=psutils), [bc](https://www.archlinux.org/packages/?name=bc), [libstdc++5](https://www.archlinux.org/packages/?name=libstdc%2B%2B5) packages ([lib32-libstdc++5](https://www.archlinux.org/packages/?name=lib32-libstdc%2B%2B5) on 64bit).

*   Download the source code of the driver.
*   Compile and install the driver.

```
$ ./configure --prefix=/usr
$ make
# make install

```

If you have any problems on a 64 system, some other lib32 libraries may be required. Please adjust this page if that is the case.

## HP

See also [CUPS/Troubleshooting#HP issues](/index.php/CUPS/Troubleshooting#HP_issues "CUPS/Troubleshooting").

Most HP printers will use [hplip](https://www.archlinux.org/packages/?name=hplip), but some may use [hpoj](https://aur.archlinux.org/packages/hpoj/).

| Printer | Driver/filter | Notes |
| DeskJet 710C | [pnm2ppa](https://aur.archlinux.org/packages/pnm2ppa/) |
| DeskJet 712C |
| DeskJet 720C |
| DeskJet 722C |
| DeskJet 820se |
| DeskJet 820Cxi |
| DeskJet 1000Cse |
| DeskJet 1000Cxi |
| LaserJet P1606dn | [hplip](https://www.archlinux.org/packages/?name=hplip) + [hplip-plugin](https://aur.archlinux.org/packages/hplip-plugin/) | Or [foo2zjs-nightly](https://aur.archlinux.org/packages/foo2zjs-nightly/), or [AirPrint](/index.php/CUPS#CUPS "CUPS"). |
| Photosmart 2575 | [hplip](https://www.archlinux.org/packages/?name=hplip) | Or use the hpijs driver in [foomatic](/index.php/CUPS#Foomatic "CUPS"). |
| Printer | Driver/filter | Notes |

###### HPLIP Driver

[hplip](https://www.archlinux.org/packages/?name=hplip) provides drivers for HP DeskJet, OfficeJet, Photosmart, Business Inkjet, and some LaserJet printers, and also provides an easy to use setup tool.

To run the setup tool with the GUI qt frontend:

```
# hp-setup -u

```

To run the setup tool with the command line frontend:

```
# hp-setup -i

```

To set up directly the configuration of a network connected HP printer:

```
# hp-setup -i *<ip address>*

```

To run systray spool manager:

```
$ hp-systray

```

To generate a URI for a given ip address:

```
# hp-makeuri *<ip address>*

```

PPD files are in `/usr/share/ppd/HP/`.

For printers that require the proprietary HP plugin (like the Laserjet Pro P1102w or 1020), install the [hplip-plugin](https://aur.archlinux.org/packages/hplip-plugin/) package from [AUR](/index.php/AUR "AUR").

**Note:**

[hplip](https://www.archlinux.org/packages/?name=hplip) depends on [foomatic-db-engine](https://www.archlinux.org/packages/?name=foomatic-db-engine) which prevents the drivers list from appearing when a printer is added to CUPS via the web user interface (following error : "Unable to get list of printer drivers"). Possible workarounds:

*   **Either:** Install [hplip](https://www.archlinux.org/packages/?name=hplip) first, then retrieve the PPD file that matches your printer from `/usr/share/ppd/HP/`. Next, remove [hplip](https://www.archlinux.org/packages/?name=hplip) entirely as well as any unnecessary dependencies. Finally, install the printer manually using the CUPS web UI, selecting the PPD file you retrieved, and then re-install [hplip](https://www.archlinux.org/packages/?name=hplip). After a reboot, you should have a fully working printer.
*   **Or:** Remove [hplip](https://www.archlinux.org/packages/?name=hplip), [foomatic-db](https://www.archlinux.org/packages/?name=foomatic-db) and [foomatic-db-engine](https://www.archlinux.org/packages/?name=foomatic-db-engine) along with any unnecessary dependencies. Reinstall [hplip](https://www.archlinux.org/packages/?name=hplip) and restart CUPS. Install your printer using the CUPS web UI, which should now be able to find the drivers automatically. No reboot needed.

## Konica

| Printer | Driver/filter | Notes |
| Minolta Magicolor 1600W | [foomatic](/index.php/CUPS#Foomatic "CUPS") |
| Minolta Magicolor 1680MF |
| Minolta Magicolor 1690MF |
| Minolta Magicolor 2480MF |
| Minolta Magicolor 2490MF |
| Minolta Magicolor 2530DL |
| Minolta Magicolor 4690MF |
| Printer | Driver/filter | Notes |

## Lexmark

### Utilities

Lexmark provides a utility called lexijtools with the drivers.

### Custom drivers

Lexmark does provide Linux drivers for all their hardware. The following packages are required:

*   [cups](https://www.archlinux.org/packages/?name=cups)
*   [sane](https://www.archlinux.org/packages/?name=sane)
*   [ncurses](https://www.archlinux.org/packages/?name=ncurses)
*   [libusb](https://www.archlinux.org/packages/?name=libusb)
*   [libxext](https://www.archlinux.org/packages/?name=libxext)
*   [libxtst](https://www.archlinux.org/packages/?name=libxtst)
*   [libxi](https://www.archlinux.org/packages/?name=libxi)
*   [libstdc++5](https://www.archlinux.org/packages/?name=libstdc%2B%2B5)
*   [krb5](https://www.archlinux.org/packages/?name=krb5)
*   [lua](https://www.archlinux.org/packages/?name=lua) (for the automated installer)
*   [Java](/index.php/Java "Java") (for the automated installer, and some of the Lexmark tools)

The drivers will need to be [downloaded](http://support.lexmark.com/index?page=driversdownloads) from Lexmark's website. Preferably, create a package (see [Creating packages](/index.php/Creating_packages "Creating packages")) and install it. Here is a basic [PKGBUILD](/index.php/PKGBUILD "PKGBUILD") that still needs work but will give an idea of what is required.

 `PKGBUILD` 
```
# Contributor: Todd Partridge (Gen2ly) toddrpartridge (at) yahoo

pkgname=cups-lexmark-Z2300-2600
pkgver=1
pkgrel=1
pkgdesc="Lexmark Z2300 and 2600 Series printer driver for cups"
arch=('i686')
url="http://www.lexmark.com/"
license=('custom')
depends=('cups' 'glibc' 'ncurses' 'libusb' 'libxext' 'libxtst' 'libxi' 'libstdc++5' 'krb5' 'lua' 'java-runtime')
conflicts=('z600' 'cjlz35le-cups' 'cups-lexmark-700')
source=(lexmark-inkjet-08-driver-1.0-1.i386.tar.gz.sh)
md5sums=(3c37eb87e3dad4853bf29344f9695134)

package() {
  # Extract installer
  sh lexmark-inkjet-08-driver-1.0-1.i386.tar.gz.sh --target Installer-Files
  cd Installer-Files
  mkdir Driver
  tar xvvf instarchive_all --lzma -C Driver/
  cd Driver
  tar xv lexmark-inkjet-08-driver-1.0-1.i386.tar.gz -C $pkgdir
}

```

Keep in mind you can use the automated installer but doing so will leave the resulting changes untracked. The PPD will be installed into `/usr/local/lexmark/lxk08/etc/` or similar, depending on the printer model.

## Oki

| Printer | Driver/filter | Notes |
| C110 | [foomatic](/index.php/CUPS#Foomatic "CUPS") |
| MC561 | [foomatic-db-nonfree](/index.php/CUPS#Foomatic "CUPS") |
| Printer | Driver/filter | Notes |

## Ricoh

Install [openprinting-ppds-pxlmono-ricoh](https://aur.archlinux.org/packages/openprinting-ppds-pxlmono-ricoh/) if your device is black and white, or [openprinting-ppds-pxlcolor-ricoh](https://aur.archlinux.org/packages/openprinting-ppds-pxlcolor-ricoh/) if it's color. Note that Ricoh copiers are sometimes branded as Savin, Gestetner, Lanier, Rex-Rotary, Nashuatec, and/or IKON. So, if you have a device bearing one of these brands, it may be supported by these drivers as well.

*   [List of supported black and white models](https://www.openprinting.org/driver/pxlmono-Ricoh)
*   [List of supported color models](https://www.openprinting.org/driver/pxlcolor-Ricoh)

## Samsung

For printers requiring the *cnijfilter* drivers, search for the correct driver [in the AUR](https://aur.archlinux.org/packages.php?K=cnijfilter)

| Printer | Driver/filter | Notes |
| ML-2010 | [splix](https://www.archlinux.org/packages/?name=splix) |
| SCX-4200 | [splix](https://www.archlinux.org/packages/?name=splix) |
| Newer printers? | [samsung-unified-driver](https://aur.archlinux.org/packages/samsung-unified-driver/) |
| Printer | Driver/filter | Notes |

## Xerox or FujiXerox

| Printer | Driver/filter | Notes |
| DocuPrint 203A | [hplip](https://www.archlinux.org/packages/?name=hplip) | Using the **DocuPrint P8e(hpijs)** driver, or the Brother driver on FujiXerox's website (see [#Brother](#Brother) for more information on how to install custom Brother drivers). |
| Phaser 3100MFP | Install Xerox's driver | See [#Phaser 3100MFP](#Phaser_3100MFP) for more instructions. |
| Phaser 6115MFP | [foomatic](/index.php/CUPS#Foomatic "CUPS") |
| Phaser 6121MFP | [foomatic](/index.php/CUPS#Foomatic "CUPS") |
|  ? | [fxlinuxprint](https://aur.archlinux.org/packages/fxlinuxprint/) |
| Printer | Driver/filter | Notes |

### Custom drivers

#### Phaser 3100MFP

**Warning:** This section involves installing packages without [pacman](/index.php/Pacman "Pacman"). These directions should ideally be automated with a [PKGBUILD](/index.php/PKGBUILD "PKGBUILD").

Once you have downloaded the drivers, execute the driver installer and accept the licence:

```
# cd printer
# ./XeroxPhaser3100.install

```

Note that the driver is 32 bit, so some 32 bit libraries will be required on an x86_64 system.

For the scanner, create an /etc/sane.d directory if it doesn't already exist, because it's need by the installer:

```
# mkdir -p /etc/sane.d

```

Now install the driver:

```
# cd scanner/
# ./XeroxPhaser3100sc.install

```

Again, on an x86_64 install, 32 bit libraries will be needed.

#### Phaser 6000B

[Install](/index.php/Install "Install") the [xerox-phaser-6010](https://github.com/aur-archive/xerox-phaser-6010) package (archived from the AUR). The driver may require older versions of [nettle](https://www.archlinux.org/packages/?name=nettle) and [gnutls](https://www.archlinux.org/packages/?name=gnutls) to be installed, since the binary blob linked against older versions of the shared libraries provided by those packages. The oldest known-good versions are `nettle-2.7.1-1` and `gnutls-3.3.13-1`.

#### Phaser 6125N

**Warning:** This section involves installing packages without [pacman](/index.php/Pacman "Pacman"). These directions should ideally be automated with a [PKGBUILD](/index.php/PKGBUILD "PKGBUILD").

FujiXerox does not support Linux on this model. An old rpm [is available](http://onlinesupport.fujixerox.com/tiles/common/hc_drivers_download.jsp?system=%27Linux%27&shortdesc=null&xcrealpath=http://www.fujixeroxprinters.com/downloads/uploaded/dpc525a_linux_.0.0.tar_81c2.zip) but does not seem to work.

A slightly adapted [custom driver](https://rickvanderzwet.nl/trac/personal/wiki/XeroxPhaser6125N) has been found to work out of the box.

To install the tarball, run

```
# tar -C / --keep-newer-files -xvzf cups-xerox-phaser-6125n-1.0.0.tar.gz

```