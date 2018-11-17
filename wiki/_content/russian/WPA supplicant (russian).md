Ссылки по теме

*   [Network configuration (Русский)](/index.php/Network_configuration_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Network configuration (Русский)")
*   [Wireless network configuration (Русский)](/index.php/Wireless_network_configuration_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Wireless network configuration (Русский)")

[wpa_supplicant](http://hostap.epitest.fi/wpa_supplicant/) — кроссплатформенный [суппликант](https://en.wikipedia.org/wiki/Supplicant_(computer) с поддержкой WEP, WPA и WPA2 ([IEEE 802.11i](https://en.wikipedia.org/wiki/IEEE_802.11i "wikipedia:IEEE 802.11i") / RSN (*Robust Secure Network*, надежная защищенная сеть)). Он подходит для настольных компьютеров, ноутбуков и встраиваемых систем.

*wpa_supplicant* является реализацией компонента IEEE 802.1X/WPA Supplicant, который используется на клиентских машинах. Он реализует согласование ключей шифрования с аутентификатором WPA (WPA Authenticator), аутентификацию EAP с сервером аутентификации (Authentication Server), а также управляет роумингом и выполняет сопряжение адаптера с беспроводной сетью.

## Contents

*   [1 Установка](#Установка)
*   [2 Обзор](#Обзор)
*   [3 Подключение при помощи wpa_cli](#Подключение_при_помощи_wpa_cli)
    *   [3.1 Подключение при помощи wpa_passphrase](#Подключение_при_помощи_wpa_passphrase)
*   [4 Расширенное использование](#Расширенное_использование)
    *   [4.1 Настройка](#Настройка)
    *   [4.2 Установка соединения](#Установка_соединения)
        *   [4.2.1 Вручную](#Вручную)
        *   [4.2.2 При загрузке (systemd)](#При_загрузке_(systemd))
    *   [4.3 Скрипт обработки событий на основе wpa_cli](#Скрипт_обработки_событий_на_основе_wpa_cli)
*   [5 Смотрите также](#Смотрите_также)

## Установка

[Установите](/index.php/%D0%A3%D1%81%D1%82%D0%B0%D0%BD%D0%BE%D0%B2%D0%B8%D1%82%D0%B5 "Установите") пакет [wpa_supplicant](https://www.archlinux.org/packages/?name=wpa_supplicant), доступный в [официальных репозиториях](/index.php/Official_repositories_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Official repositories (Русский)").

Также вы можете установить [wpa_supplicant_gui](https://aur.archlinux.org/packages/wpa_supplicant_gui/), который предоставляет *wpa_gui* – графическую оболочку для *wpa_supplicant*.

## Обзор

При установке соединения с зашифрованной беспроводной сетью *wpa_supplicant* проходит аутентификацию у аутентификатора WPA. Для успешного завершения этого процесса *wpa_supplicant* должен быть настроен так, чтобы иметь возможность передать правильный закрытый ключ сети аутентификатору.

После успешного завершения процесса аутентификации необходимо установить IP-адрес сетевого интерфейса вручную с помощью утилит [iproute2](/index.php/%D0%91%D0%B0%D0%B7%D0%BE%D0%B2%D1%8B%D0%B5_%D1%83%D1%82%D0%B8%D0%BB%D0%B8%D1%82%D1%8B#ip "Базовые утилиты"), либо автоматически, например с [systemd-networkd](/index.php/Systemd-networkd_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Systemd-networkd (Русский)") или [dhcpcd (Русский)](/index.php/Dhcpcd_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Dhcpcd (Русский)") для настройки автоматического получения IP через DHCP. Как только сетевому интерфейсу будет присвоен IP-адрес, станет возможо получить доступ к сети через беспроводное соединение.

Методы и примеры вы также сможете найти на страницах по [беспроводной](/index.php/Wireless_network_configuration_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#Systemd_с_wpa_supplicant_и_статическим_IP "Wireless network configuration (Русский)") и [проводной](/index.php/Network_configuration_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#Настройка_IP-адреса "Network configuration (Русский)") настройке сети.

## Подключение при помощи wpa_cli

Этот метод позволяет выполнить сканирование для поиска окружающих сетей, используя *wpa_cli* – утилиту командной строки, которая может быть использована для интерактивной настройки запущенного *wpa_supplicant*. Смотрите [wpa_cli(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/wpa_cli.8) для получения дополнительной информации.

Чтобы использовать *wpa_cli*, для *wpa_supplicant* должен быть указан контрольный интерфейс (файл сокета), и ему должны быть даны права на обновление файла настроек. Сделать это можно создав минимальный файл настроек:

 `/etc/wpa_supplicant/example.conf` 
```
ctrl_interface=/run/wpa_supplicant
update_config=1
```

Теперь запустите *wpa_supplicant* командой:

```
# wpa_supplicant -B -i *имя_интерфейса* -c /etc/wpa_supplicant/example.conf

```

где *имя_интерфейса* – имя вашего беспроводного сетевого интерфейса.

**Совет:** Чтобы определить имя беспроводного сетевого интерфейса, используйте команду `ip link`.

Теперь запустите *wpa_cli*:

```
# wpa_cli

```

Будет отображено приглашение для ввода команд (`>`), где вы можете использовать автодополнение по `Tab` и получать описание для дополняемых команд.

**Совет:** Расположение сокета может быть указано вручную с помощью опции `-p`; с помощью `-i` можно также указать имя сетевого интерфейса. Если имя не указано явно, будет использоваться первый найденный беспроводной интерфейс, управляемый *wpa_supplicant*.

Используйте команды `scan` и `scan_results` для сканирования доступных беспроводных сетей:

```
> scan
OK
<3>CTRL-EVENT-SCAN-RESULTS
> scan_results
bssid / frequency / signal level / flags / ssid
00:00:00:00:00:00 2462 -49 [WPA2-PSK-CCMP][ESS] MYSSID
11:11:11:11:11:11 2437 -64 [WPA2-PSK-CCMP][ESS] ANOTHERSSID

```

Чтобы подключиться к сети `MYSSID`, добавьте новую сеть (`add_network`), укажите ее идентификатор (*ssid*) и пароль для доступа к сети (`set_network`), затем включите ее (`enable_network`):

```
> add_network
0
> set_network 0 ssid "MYSSID"
> set_network 0 psk "passphrase"
> enable_network 0
<2>CTRL-EVENT-CONNECTED – Connection to 00:00:00:00:00:00 completed (reauth) [id=0 id_str=]

```

**Примечание:**

*   Каждая сеть нумеруется с нуля, поэтому первая сеть имеет индекс 0.
*   [Закрытый ключ (PSK)](https://en.wikipedia.org/wiki/Pre-shared_key "wikipedia:Pre-shared key") сети вычисляется на основе парольной фразы, заключенной в кавычки, что вы также можете заметить, прочитав раздел [wpa_passphrase](#Подключение_при_помощи_wpa_passphrase). Тем не менее, вы можете ввести закрытый ключ напрямую, введя его в команде `set_network *id* psk` *без* кавычек.

Теперь сохраните внесенные изменения в файл настроек:

```
> save_config
OK

```

Как только сопряжение с сетью будет выполнено, все, что останется сделать – получить IP адрес, как было указано в разделе [#Обзор](#Обзор), например:

```
# dhcpcd *имя_интерфейса*

```

### Подключение при помощи wpa_passphrase

Этот метод позволяет быстро соединиться с сетью, SSID которой известен, используя *wpa_passphrase* – утилиту командной строки, которая генерирует текст минимальной необходимой конфигурации для *wpa_supplicant*. Пример:

 `$ wpa_passphrase MYSSID passphrase` 
```
network={
    ssid="MYSSID"
    #psk="passphrase"
    psk=59e0d07fa4c7741797a4e394f38a5c321e3bed51d54ad5fcbd3f84bc7415d73d
}
```

Так как текст попадает в стандартный вывод, вы можете сразу вызвать *wpa_supplicant*, передавая ему настройки:

```
# wpa_supplicant -B -i *имя_интерфейса* -c <(wpa_passphrase MYSSID passphrase)

```

**Note:** Из-за подстановки процесса, вы **не можете** запускать эту команду из [sudo](/index.php/Sudo "Sudo"): вам нужен постоянный сеанс суперпользователя. Смотрите также [Help:Reading#Regular user or root](/index.php/Help:Reading#Regular_user_or_root "Help:Reading").

**Совет:**

*   Используйте кавычки, если строка содержит пробелы, например: `"secret passphrase"`.
*   Чтобы определить имя беспроводного сетевого интерфейса, используйте команду `ip link`.
*   Парольные фразы с некоторыми нестандартными символами могут потребовать ввода из файла: `wpa_passphrase MYSSID < passphrase.txt`.

Как только сопряжение с сетью будет выполнено, вам останется получить IP адрес, как было указано в разделе [#Обзор](#Обзор), например:

```
# dhcpcd *имя_интерфейса*

```

## Расширенное использование

Для более сложных сетей, например, широко практикующих использование [EAP](https://en.wikipedia.org/wiki/Extensible_Authentication_Protocol "wikipedia:Extensible Authentication Protocol"), будет необходимо вручную настроить *wpa_supplicant*. На странице [wpa_supplicant.conf(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/wpa_supplicant.conf.5) вы можете найти описание структуры и содержимого файла настроек и примеры файлов; более детальное описание всех опций вы можете найти в файле `/etc/wpa_supplicant/wpa_supplicant.conf`.

### Настройка

Как уже было сказано в разделе [#Подключение при помощи wpa_passphrase](#Подключение_при_помощи_wpa_passphrase), минимальная конфигурация может быть создана при помощи команды:

```
# wpa_passphrase *SSID_сети* *парольная_фраза* > /etc/wpa_supplicant/example.conf

```

Команда создает только блок опций `network`. Файл настроек с наиболее общими опциями может выглядеть примерно так:

 `/etc/wpa_supplicant/example.conf` 
```
ctrl_interface=DIR=/run/wpa_supplicant GROUP=wheel
update_config=1
fast_reauth=1
ap_scan=1
network={
    ssid="''SSID_сети''"
    #psk="''парольная_фраза''"
    psk=59e0d07fa4c7741797a4e394f38a5c321e3bed51d54ad5fcbd3f84bc7415d73d
}
```

В дальнейшем блоки `network` могут быть добавлены вручную либо с использованием *wpa_cli*, как показано в разделе [#Подключение при помощи wpa_cli](#Подключение_при_помощи_wpa_cli). Чтобы использовать *wpa_cli*, должен быть указан контрольный интерфейс при помощи опции `ctrl_interface`. Установка `GROUP=wheel` позволяет пользователям этой группы использовать *wpa_cli*. Также добавьте `update_config=1`, чтобы изменения, сделанные в *wpa_cli* могли сохраняться в файл.

Опции `fast_reauth=1` и `ap_scan=1` установлены глобально. Нужны они вам или нет зависит от того, к какому типу сети вы хотите подключиться. Если вам нужны прочие глобальные опции, просто скопируйте их из `/etc/wpa_supplicant/wpa_supplicant.conf`.

Также вы можете использовать команду `wpa_cli set` для отображения текущего состояния опций и установки их значений. Несколько блоков `network` можно добавить в файл настроек: *wpa_supplicant* сможет работать с каждой из них. По умолчанию, производится подключение к сети с наиболее сильным сигналом; если это поведение нежелательно, вы можете использовать опцию `priority` для установки числового значения приоритета.

Преимущество размещения настроек в `/etc/wpa_supplicant/wpa_supplicant.conf` в том, что [dhcpcd](/index.php/Dhcpcd "Dhcpcd") использует этот файл по умолчанию. Обратите внимание, что, кроме подробного описания опций в комментариях, некоторые опции добавлены в файл незакомментированными, в том числе и набор блоков `network`, приведенный там в качестве примера, которые однажды могут привести к незапланированному подключению к чужой сети с совпавшим SSID. Возможно, вы захотите сохранить резервную копию этого файла для примера, и создать новый файл для своих настроек на этом месте. В любом случае, при наличии изменений в новых версиях стандартного файла конфигурации должно произойти безопасное [слияние](/index.php/Pacnew_and_Pacsave_files "Pacnew and Pacsave files").

**Примечание:** Начиная с версии dhcpcd-6.10.0-1 поведение демона по умолчанию изменено: теперь хук 10-wpa_supplicant не запускается по умолчанию! Подробнее: [[1]](https://bbs.archlinux.org/viewtopic.php?id=207416), [[2]](https://gentoo.org/support/news-items/2016-01-08-some-dhcpcd-hooks-are-now-examples.html)

**Совет:** Чтобы настроить блок `network` для соединения с беспроводной сетью со скрытым SSID, добавьте в него опцию `scan_ssid=1`.

### Установка соединения

#### Вручную

Запустите *wpa_supplicant*. Наиболее распространенные опции команды:

*   `-B` – запуск в фоновом режиме.
*   `-c *filename*` – путь до файла настроек.
*   `-i *interface*` – сетевой интерфейс.
*   `-D *driver*` – опционально позволяет указать драйвер адаптера. Для получения списка поддерживаемых драйверов наберите `wpa_supplicant -h`.
    *   `nl80211` в данный момент является стандартным, но не все модули беспроводных контроллеров поддерживают его.
    *   `wext` устарел, однако, все еще широко поддерживается.

Полный список поддерживаемых опций ищите в руководстве [wpa_supplicant(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/wpa_supplicant.8).

Пример вызова *wpa_supplicant*:

```
# wpa_supplicant -B -i *имя_интерфейса* -c /etc/wpa_supplicant/example.conf

```

Когда будет произведено успешное сопряжение с беспроводной сетью, вы сможете получить IP-адрес, как было указано в разделе [#Обзор](#Обзор), например:

```
# systemctl enable dhcpcd@*interface*

```

**Совет:** *dhcpcd* имеет хук, который может неявно запускать *wpa_supplicant*, подробнее смотрите на странице [dhcpcd (Русский)#10-wpa_supplicant](/index.php/Dhcpcd_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#10-wpa_supplicant "Dhcpcd (Русский)").

#### При загрузке (systemd)

Пакет *wpa_supplicant* предоставляет множество файлов служб [systemd](/index.php/Systemd_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Systemd (Русский)"):

*   `wpa_supplicant.service` – использует [D-Bus](/index.php/D-Bus "D-Bus"), рекомендуется для пользователей [NetworkManager](/index.php/NetworkManager "NetworkManager").
*   `wpa_supplicant@.service` – принимает имя интерфейса в качестве аргумента и запускает на нем демон *wpa_supplicant*, который прочитывает настройки из файла `/etc/wpa_supplicant/wpa_supplicant-*имя_интерфейса*.conf`.
*   `wpa_supplicant-nl80211@.service` – также позволяет указать интерфейс, кроме того указывает *wpa_supplicant* использовать драйвер `nl80211`. Используется файл настроек `/etc/wpa_supplicant/wpa_supplicant-nl80211-*имя_интерфейса*.conf`.
*   `wpa_supplicant-wired@.service` – также позволяет указать интерфейс, кроме того указывает *wpa_supplicant* использовать драйвер `wired`. Используется файл настроек `/etc/wpa_supplicant/wpa_supplicant-wired-*имя_интерфейса*.conf`.

Чтобы соединение автоматически выполнялось при старте системы, включите одну из предоставленных служб, например:

```
# systemctl enable wpa_supplicant@*имя_интерфейса*

```

Когда будет произведено успешное сопряжение с беспроводной сетью, вы сможете получить IP-адрес, как было указано в разделе [#Обзор](#Обзор), например:

```
# systemctl enable dhcpcd@*interface*

```

**Совет:** *dhcpcd* имеет хук, который может неявно запускать *wpa_supplicant*, подробнее смотрите на странице [dhcpcd (Русский)#10-wpa_supplicant](/index.php/Dhcpcd_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#10-wpa_supplicant "Dhcpcd (Русский)").

### Скрипт обработки событий на основе wpa_cli

*wpa_cli* может выполняться как демон и запускать указанный скрипт для событий, генерируемых *wpa_supplicant*. Поддерживаются два события: `CONNECTED` и `DISCONNECTED`. Некоторые [переменные окружения](/index.php/Environment_variables_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Environment variables (Русский)") доступны для использовании в скрипте, смотрите [wpa_cli(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/wpa_cli.8) для получения подробной информации.

Следующий пример использует [уведомления рабочего стола](/index.php/Desktop_notifications "Desktop notifications") для уведомления пользователя о событиях:

```
#!/bin/bash

case "$2" in
    CONNECTED)
        notify-send "WPA supplicant: connection established";
        ;;
    DISCONNECTED)
        notify-send "WPA supplicant: connection lost";
        ;;
esac

```

Не забудьте сделать файл скрипта исполняемым, затем укажите его при запуске *wpa_cli* с помощью опции `-a`:

```
$ wpa_cli -a */путь/до/скрипта*

```

## Смотрите также

*   [домашняя страница WPA Supplicant](http://hostap.epitest.fi/wpa_supplicant/)
*   [примеры использования wpa_cli](https://gist.github.com/buhman/7162560)
*   [wpa_supplicant(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/wpa_supplicant.8)
*   [wpa_supplicant.conf(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/wpa_supplicant.conf.5)
*   [wpa_cli(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/wpa_cli.8)
*   [документация wpa_supplicant на Kernel.org](http://wireless.kernel.org/en/users/Documentation/wpa_supplicant)