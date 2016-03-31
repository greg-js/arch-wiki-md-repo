Для подключения к Интернету с помощью 3G или GPRS модема не обязательно использовать [Wvdial](/index.php/Wvdial_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Wvdial (Русский)") или подобные программы. Использовать их удобно, но они создают лишний "слой". Более простое, очевидно, является более надёжным, не так ли?

## Contents

*   [1 Требования](#.D0.A2.D1.80.D0.B5.D0.B1.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D1.8F)
*   [2 Настройка](#.D0.9D.D0.B0.D1.81.D1.82.D1.80.D0.BE.D0.B9.D0.BA.D0.B0)
    *   [2.1 Настройки модема](#.D0.9D.D0.B0.D1.81.D1.82.D1.80.D0.BE.D0.B9.D0.BA.D0.B8_.D0.BC.D0.BE.D0.B4.D0.B5.D0.BC.D0.B0)
    *   [2.2 Настройки оператора](#.D0.9D.D0.B0.D1.81.D1.82.D1.80.D0.BE.D0.B9.D0.BA.D0.B8_.D0.BE.D0.BF.D0.B5.D1.80.D0.B0.D1.82.D0.BE.D1.80.D0.B0)
    *   [2.3 Сценарии диалога](#.D0.A1.D1.86.D0.B5.D0.BD.D0.B0.D1.80.D0.B8.D0.B8_.D0.B4.D0.B8.D0.B0.D0.BB.D0.BE.D0.B3.D0.B0)
*   [3 Запуск](#.D0.97.D0.B0.D0.BF.D1.83.D1.81.D0.BA)
    *   [3.1 Патч на доступность модема](#.D0.9F.D0.B0.D1.82.D1.87_.D0.BD.D0.B0_.D0.B4.D0.BE.D1.81.D1.82.D1.83.D0.BF.D0.BD.D0.BE.D1.81.D1.82.D1.8C_.D0.BC.D0.BE.D0.B4.D0.B5.D0.BC.D0.B0)
*   [4 Устранение неполадок](#.D0.A3.D1.81.D1.82.D1.80.D0.B0.D0.BD.D0.B5.D0.BD.D0.B8.D0.B5_.D0.BD.D0.B5.D0.BF.D0.BE.D0.BB.D0.B0.D0.B4.D0.BE.D0.BA)
    *   [4.1 Проблема с PIN кодом](#.D0.9F.D1.80.D0.BE.D0.B1.D0.BB.D0.B5.D0.BC.D0.B0_.D1.81_PIN_.D0.BA.D0.BE.D0.B4.D0.BE.D0.BC)
    *   [4.2 Модем EM770](#.D0.9C.D0.BE.D0.B4.D0.B5.D0.BC_EM770)
*   [5 Справочник команд AT^SYSCFG для Huawei](#.D0.A1.D0.BF.D1.80.D0.B0.D0.B2.D0.BE.D1.87.D0.BD.D0.B8.D0.BA_.D0.BA.D0.BE.D0.BC.D0.B0.D0.BD.D0.B4_AT.5ESYSCFG_.D0.B4.D0.BB.D1.8F_Huawei)
*   [6 Связанные статьи](#.D0.A1.D0.B2.D1.8F.D0.B7.D0.B0.D0.BD.D0.BD.D1.8B.D0.B5_.D1.81.D1.82.D0.B0.D1.82.D1.8C.D0.B8)

## Требования

Единственное требование к программной части - установленный [ppp](https://www.archlinux.org/packages/?name=ppp).

Способ настройки и подключения, изложенный ниже, был проверен на нескольких модемах:

*   Huawey EM770 MiniPCIe (внутренний модем Asus Eee PC 1000H Go);
*   внешний модем Huawey E220;
*   Nokia N73 (подключение по USB; в телефоне выбрано "PC Suite").

## Настройка

**Примечание:** Описание настройки pppd в [оригинальной статье](/index.php/3G_and_GPRS_modems_with_pppd_alone "3G and GPRS modems with pppd alone") содержит подробные листинги конфигурационных файлов. Здесь же описывается краткий вариант для настройки на единственного оператора.

**Важно:** Дальнейшие действия предполагают, что ваш модем установлен и успешно опознан. Более подробную информацию по установке и настройке 3G/GPRS модема вы можете получить в статье [USB 3G Модем](/index.php/USB_3G_%D0%9C%D0%BE%D0%B4%D0%B5%D0%BC "USB 3G Модем").

**Tip:** Вам нужно будет создать несоклько файлов в `/etc/ppp`, и для этого понадобятся права root.

### Настройки модема

Первым делом, создайте файл `/etc/ppp/options-mobile`. Pppd, следуя указанным настройкам, постарается удержать соединение активным, а в случае обрыва попытается восстановить его.

 `/etc/ppp/options-mobile` 
```
**/dev/ttyUSBn**
921600
defaultroute
usepeerdns
crtscts
lock
noauth
local
persist
modem
nopcomp
novjccomp
nobsdcomp
nodeflate
noaccomp
ipcp-accept-local
ipcp-accept-remote
noipdefault

```

Обратите внимание на первую строчку: здесь должно быть имя вашего модема в `/dev`. Подставьте вместо *n* номер устройства модема.

**Примечание:** Обычно, для USB модемов, оно имеет вид `ttyUSBn`, где n - номер модема, или же `ttyACMn`.

### Настройки оператора

Если ваш оператор требует авторизации при установлении соединения с Интернетом, создайте файл `/etc/ppp/peers/*название-оператора*` следующего содержания:

 `/etc/ppp/peers/*название-оператора*` 
```
file /etc/ppp/options-mobile
user "*логин*"
password "*пароль*"
connect "/usr/sbin/chat -v -t15 -f /etc/ppp/chatscripts/*название-оператора*.chat"

```

Замените *логин* и *пароль* на предоставленные вашим оператором.

**Tip:** Вы можете создать несколько таких файлов для разных операторов

Если же авторизация **не** требуется, опустите строчки `user...` и `password...`

### Сценарии диалога

Чтобы подключиться к Интернету, вашему компьютеру необходимо отправить на модем команды, которые бы задали режим работы, номер телефона и прочие настройки, необходимые для установления соедиинения. Такие команды называются AT-командами, и pppd для "общения" с модемом использует программу `/usr/sbin/chat`. Сейчас мы создадим "сценарий диалога", которые будет использовать `chat` для общения с нашим модемом.

Создайте папку `/etc/ppp/chatscripts`.

```
mkdir /etc/ppp/chatscripts

```
 `/etc/ppp/chatscripts/*название-оператора*.chat` 
```
ABORT 'BUSY'
ABORT 'NO CARRIER'
ABORT 'VOICE'
ABORT 'NO DIALTONE'
ABORT 'NO DIAL TONE'
ABORT 'NO ANSWER'
ABORT 'DELAYED'
REPORT CONNECT
TIMEOUT 6
'' 'ATQ0'
'OK-AT-OK' 'ATZ'
TIMEOUT 3
**'OK' 'AT+CPIN=0000'**
'OK-AT-OK' 'ATI'
'OK' 'ATZ'
'OK' 'ATQ0 V1 E1 S0=0 &C1 &D2 +FCLASS=0'
**'OK' 'AT\^SYSCFG=2,2,3fffffff,0,1'**
**'OK-AT-OK' 'AT+CGDCONT=1,"IP","internet.apn"'**
'OK' 'ATDT*99***1#'
TIMEOUT 30
CONNECT 
```

Если вы используете проверку PIN кода, замените нули в первой выделенной строке (`'OK' 'AT+CPIN=0000'`) на ваш PIN-код. В противном случае просто удалите строчку целиком.

3G модем может работать в четырёх режимах. Для задания того или иного режима вам нужно внести изменения во вторую выделенную строчку:

*   Только 3G - `AT\^SYSCFG=14,2,3fffffff,0,1`
*   Предпочтительно 3G - `AT\^SYSCFG=2,2,3fffffff,0,1`
*   Только GPRS - `AT\^SYSCFG=13,1,3fffffff,0,0`
*   Предпочтительно GPRS - `AT\^SYSCFG=2,1,3fffffff,0,0`

Задайте точку доступа в последней выделенной строке: замените `internet.apn` на точку доступа, указанную вашим оператором.

**Важно:** Будьте внимательны при указании точки доступа. Ошибка может привести к списанию значительной суммы с вашего виртуального счёта.

## Запуск

Чтобы подключиться к Интернету, наберите:

```
/etc/rc.d/ppp start

```

Для отключения выполните:

```
/etc/rc.d/ppp stop

```

Вы можете добавить pppd в список демонов файла `/etc/rc.conf`, если хотите, чтобы pppd запускался автоматически.

### Патч на доступность модема

Если вы запускаете pppd автоматически, может возникнуть такая проблема: к моменту запуска pppd модем ещё не существует. Pppd честно пытается запуститься, не находит нужного устройства и завершается с ошибкой.

Для того чтобы pppd немного подождал, пока появится модем, измените файл `/etc/rc.d/ppp`:

```
case "$1" in
  start)
    stat_busy "Starting PPP daemon"
 **/etc/ppp/wait-dialup-hardware**
    [ -z "$PID" ] && /usr/bin/pon

```

Теперь, создайте файл `/etc/ppp/wait-dialup-hardware`:

 `/etc/ppp/wait-dialup-hardware` 
```
#!/bin/bash
INTERFACE="/dev/$(/usr/bin/head -1 /etc/ppp/options-mobile)"
for ((retry=0; retry < 40; retry++))
do
    if [ -c ${INTERFACE} ]; then
        /usr/bin/logger "$0: OK existing required device ${INTERFACE} (in $((retry / 4)).$((100 * (retry % 4) / 4)) seconds)"
        break
    else
        /bin/sleep 0.25
    fi
done
if [ ! -c ${INTERFACE} ]; then
    /usr/bin/logger "$0: ERROR timeout waiting for required device ${INTERFACE}"
fi
exit 0
```

Этот сценарий добавит в `/var/log/messages` строчку:

```
Jun  1 22:52:08 parsec logger: /etc/ppp/wait-dialup-hardware: OK existing required device /dev/ttyUSB0 (in 1.25 seconds)

```

## Устранение неполадок

### Проблема с PIN кодом

Если PIN код задан неверно, модем может игнорировать строчку, задающую точку доступа. В `/var/log/messages` это выглядит примерно так:

```
Jun 20 00:17:30 quark chat[3348]: send (AT+CGDCONT=1,"IP","ac.vodafone.es"^M)
Jun 20 00:17:31 quark chat[3348]: expect (OK)
Jun 20 00:17:31 quark chat[3348]: ^M
Jun 20 00:17:31 quark chat[3348]: AT+CGDCONT=1,"IP","ac.vodafone.es"^M^M
Jun 20 00:17:31 quark chat[3348]: ERROR^M
Jun 20 00:17:34 quark chat[3348]: alarm
Jun 20 00:17:34 quark chat[3348]: Failed

```

Если вы только что установили или изменили PIN код, перезагрузите телефон и первый раз пройдите проверку PIN кода **на телефоне**, и лишь затем переставляйте SIM карту в модем.

Возможно, подходящим решением будет отключить проверку PIN кода, это можно сделать в настройках безопасности вашего телефона.

### Модем EM770

Если pppd часто перезапускается вручную, например, при проверке настроек, EM770 (прошивка 11.104.16.12.00) иногда зависает после ответа `NO CARIER` (хотя исправно отвечал на `AT` а соединение с сотовой сетью в порядке). Этой ошибки не происходит, если при потере соединения с интернетом, сценарий будет ждать некоторое время, прежде чем попытаться ещё раз установить соединение. Если же модем всё-таки "залип", включите и выключите компьютер, это помогает. Вероятно, это ошибка программного обеспечения модема.

Кроме того, если используется проверка PIN кода, этот модем отвечает `NO CARRIER` при первой попытке соединения. В этом случае помогает большой интервал ожидания после отправки `AT+CPIN`.

## Справочник команд AT^SYSCFG для Huawei

Чтобы увидеть поддерживаемые значения, вы можете опросить свой модем, отправив на него команду `AT^SYSCFG=?`.

```
AT^SYSCFG=$mode,$acqOrder,$band,$roam,$srvDomain

$mode
2=Auto-Select
13=GSM only
14=WCDMA only
16=no Change

$acqOrder
0=Automatic
1=GSM prefered
2=WCDMA prefered
3=no Change

$band
3fffffff = All
other (query list with "AT^SYSCFG=?")

$roam
0=Not Supported
1=Supported
2=no Change

$srvDomain
0=Circuit-Switched only
1=Packet-Switched only
2=Circuit- & Packet-Switched
3=Any
4=no Change

```

## Связанные статьи

*   [Dialup without a dialer HOWTO (Русский)](/index.php/Dialup_without_a_dialer_HOWTO_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Dialup without a dialer HOWTO (Русский)")
*   [Huawei E220](/index.php/Huawei_E220 "Huawei E220")
*   [USB 3G Modem (Русский)](/index.php/USB_3G_Modem_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "USB 3G Modem (Русский)")