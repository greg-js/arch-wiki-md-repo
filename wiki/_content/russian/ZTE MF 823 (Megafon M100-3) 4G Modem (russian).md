## Contents

*   [1 Определение устройства](#.D0.9E.D0.BF.D1.80.D0.B5.D0.B4.D0.B5.D0.BB.D0.B5.D0.BD.D0.B8.D0.B5_.D1.83.D1.81.D1.82.D1.80.D0.BE.D0.B9.D1.81.D1.82.D0.B2.D0.B0)
*   [2 Соединение](#.D0.A1.D0.BE.D0.B5.D0.B4.D0.B8.D0.BD.D0.B5.D0.BD.D0.B8.D0.B5)
*   [3 Команды](#.D0.9A.D0.BE.D0.BC.D0.B0.D0.BD.D0.B4.D1.8B)
*   [4 Telnet соединение](#Telnet_.D1.81.D0.BE.D0.B5.D0.B4.D0.B8.D0.BD.D0.B5.D0.BD.D0.B8.D0.B5)
*   [5 Внешние ссылки](#.D0.92.D0.BD.D0.B5.D1.88.D0.BD.D0.B8.D0.B5_.D1.81.D1.81.D1.8B.D0.BB.D0.BA.D0.B8)

## Определение устройства

Проверьте вывод lsusb. Должно получиться:

```
$ Bus 002 Device 018: ID 19d2:1405 ZTE WCDMA Technologies MSM 

```

В России модем поставляется Мегафоном (модель М100-3, без веб-интерфеса, устанавливается дополнительный софт) и Билайном (имеется веб-интерфейс).

Возможные режимы модема:

1225 - режим "по умолчанию". Доступен USB Mass Storage Device с CD-ROM и кардридером

1403 - рабочий режим. Доступны адаптер RNDIS и Mass Storage Device.

1405 - рабочий режим для линукс - CDC ethernet mode, то, что нам необходимо.

0016 - диагностический режим (download mode)

Если модем не определяется как 19d2:1405 (или 1403), обратитесь к этой статье: [USB 3G Modem#Mode switching](/index.php/USB_3G_Modem#Mode_switching "USB 3G Modem")

## Соединение

Модем определяется как интерфейс Ethernet (проводное соединение). Для работы с ним нет необходимости устанавливать специальные программы. Для установки соединения используйте NetworkManager или dhcpcd.

Лампочка на модеме (синяя при 2G/3G режиме или зеленая при 4G) не мигает. Для подключения к сети необходимо вставить ссылку (CGI команду) в браузер.

[http://192.168.0.1/goform/goform_set_cmd_process?goformId=CONNECT_NETWORK](http://192.168.0.1/goform/goform_set_cmd_process?goformId=CONNECT_NETWORK)

Чтобы не вводить эту команду каждый раз после выключения модема, переключите модем в режим "автодозвона"

[http://192.168.0.1/goform/goform_set_cmd_process?goformId=SET_CONNECTION_MODE&ConnectionMode=auto_dial](http://192.168.0.1/goform/goform_set_cmd_process?goformId=SET_CONNECTION_MODE&ConnectionMode=auto_dial)

## Команды

CGI команда для выбора режимов 2G/3G/4G:

 `http://192.168.0.1/goform/goform_set_cmd_process?goformId=SET_BEARER_PREFERENCE&BearerPreference=` 

Добавьте необходимый параметр после знака "=" (чувствительны к регистру)

```
NETWORK_auto (автоматический режим)
WCDMA_preferred (предпочитать 3G)
GSM_preferred (предпочитать 2G)
Only_GSM (только 2G)
Only_WCDMA (только 3G)
Only_LTE (только 4G)
WCDMA_AND_GSM (3G+2G)
WCDMA_AND_LTE (3G+4G)
GSM_AND_LTE (2G+4G)

```

После выбора режима необходимо вновь набрать команду **NETWORK CONNECT** для подключения к сети.

Для перевода модема в **диагностический режим** (**ВНИМАНИЕ! Прием дальнейших CGI команд будет невозможен, соединение прервано!**), используйте следующую ссылку:

 `http://192.168.0.1/goform/goform_process?goformId=MODE_SWITCH&switchCmd=FACTORY` 

После перевода модема в **диагностический режим** можно посылать команды через PuTTY:

```
putty /dev/ttyUSB0
AT+ZCDRUN=8 - установить режим 1403 (RNDIS)
AT+ZCDRUN=9 - установить режим 1225 (по-умолчанию)
AT+ZCDRUN=F - выйти из диагностического режима и перейти в выбранный режим (RNDIS или по-умолчанию)

```

## Telnet соединение

К модему можно подключиться по telnet

```
telnet 192.168.0.1
login: root
password: zte9x15

```

Как видите, внутри модема установлен Линукс. Вы можете установить дополнительные программы для ARM-машин (например mc, nano...) или изменить что-то в веб-интерфейсе. Исследуйте модем с осторожностью!

## Внешние ссылки

[Gsmforum.ru - Обсуждение ZTE MF823, в №7 посте инструкция по разлочке](http://www.gsmforum.ru/threads/188925-ZTE-MF823-%D0%B8-%D0%B2%D1%81%D1%91-%D1%87%D1%82%D0%BE-%D1%81-%D0%BD%D0%B8%D0%BC-%D1%81%D0%B2%D1%8F%D0%B7%D0%B0%D0%BD%D0%BE)