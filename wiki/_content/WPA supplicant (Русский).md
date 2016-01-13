# WPA supplicant (Русский)

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

Ссылки по теме

*   [Network configuration (Русский)](/index.php/Network_configuration_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Network configuration (Русский)")
*   [Wireless network configuration (Русский)](/index.php/Wireless_network_configuration_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Wireless network configuration (Русский)")

[![Tango-preferences-desktop-locale.png](/images/d/dc/Tango-preferences-desktop-locale.png)](/index.php/File:Tango-preferences-desktop-locale.png)

[![Tango-preferences-desktop-locale.png](/images/d/dc/Tango-preferences-desktop-locale.png)](/index.php/File:Tango-preferences-desktop-locale.png)

**Эта страница нуждается в сопроводителе**

Статья не гарантирует актуальность информации. Помогите русскоязычному сообществу поддержкой подобных страниц. См. [Команда переводчиков ArchWiki](/index.php/%D0%9A%D0%BE%D0%BC%D0%B0%D0%BD%D0%B4%D0%B0_%D0%BF%D0%B5%D1%80%D0%B5%D0%B2%D0%BE%D0%B4%D1%87%D0%B8%D0%BA%D0%BE%D0%B2_ArchWiki "Команда переводчиков ArchWiki")

[wpa_supplicant](http://hostap.epitest.fi/wpa_supplicant/) — кроссплатформенный [суппликант](https://en.wikipedia.org/wiki/Supplicant_(computer) "wikipedia:Supplicant (computer)") с поддержкой WEP, WPA и WPA2 ([IEEE 802.11i](https://en.wikipedia.org/wiki/IEEE_802.11i "wikipedia:IEEE 802.11i") / RSN (_Robust Secure Network_, надежная защищенная сеть)). Он подходит для настольных компьютеров, ноутбуков и встраиваемых систем.

_wpa_supplicant_ является реализацией компонента IEEE 802.1X/WPA Supplicant, который используется на клиентских машинах. Он реализует согласование ключей шифрования с аутентификатором WPA (WPA Authenticator), аутентификацию EAP с сервером аутентификации (Authentication Server), а также управляет роумингом и выполняет сопряжение адаптера с беспроводной сетью.

## Contents

*   [1 Установка](#.D0.A3.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B0)
*   [2 Обзор](#.D0.9E.D0.B1.D0.B7.D0.BE.D1.80)
*   [3 Подключение при помощи wpa_cli](#.D0.9F.D0.BE.D0.B4.D0.BA.D0.BB.D1.8E.D1.87.D0.B5.D0.BD.D0.B8.D0.B5_.D0.BF.D1.80.D0.B8_.D0.BF.D0.BE.D0.BC.D0.BE.D1.89.D0.B8_wpa_cli)
    *   [3.1 Подключение при помощи wpa_passphrase](#.D0.9F.D0.BE.D0.B4.D0.BA.D0.BB.D1.8E.D1.87.D0.B5.D0.BD.D0.B8.D0.B5_.D0.BF.D1.80.D0.B8_.D0.BF.D0.BE.D0.BC.D0.BE.D1.89.D0.B8_wpa_passphrase)
*   [4 Расширенное использование](#.D0.A0.D0.B0.D1.81.D1.88.D0.B8.D1.80.D0.B5.D0.BD.D0.BD.D0.BE.D0.B5_.D0.B8.D1.81.D0.BF.D0.BE.D0.BB.D1.8C.D0.B7.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D0.B5)
    *   [4.1 Настройка](#.D0.9D.D0.B0.D1.81.D1.82.D1.80.D0.BE.D0.B9.D0.BA.D0.B0)
    *   [4.2 Установка соединения](#.D0.A3.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B0_.D1.81.D0.BE.D0.B5.D0.B4.D0.B8.D0.BD.D0.B5.D0.BD.D0.B8.D1.8F)
        *   [4.2.1 Вручную](#.D0.92.D1.80.D1.83.D1.87.D0.BD.D1.83.D1.8E)
        *   [4.2.2 При загрузке (systemd)](#.D0.9F.D1.80.D0.B8_.D0.B7.D0.B0.D0.B3.D1.80.D1.83.D0.B7.D0.BA.D0.B5_.28systemd.29)
    *   [4.3 Скрипт обработки событий на основе wpa_cli](#.D0.A1.D0.BA.D1.80.D0.B8.D0.BF.D1.82_.D0.BE.D0.B1.D1.80.D0.B0.D0.B1.D0.BE.D1.82.D0.BA.D0.B8_.D1.81.D0.BE.D0.B1.D1.8B.D1.82.D0.B8.D0.B9_.D0.BD.D0.B0_.D0.BE.D1.81.D0.BD.D0.BE.D0.B2.D0.B5_wpa_cli)
*   [5 Смотрите также](#.D0.A1.D0.BC.D0.BE.D1.82.D1.80.D0.B8.D1.82.D0.B5_.D1.82.D0.B0.D0.BA.D0.B6.D0.B5)

## Установка

[Установите](/index.php/Pacman_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#.D0.A3.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B0_.D0.BE.D0.BF.D1.80.D0.B5.D0.B4.D0.B5.D0.BB.D0.B5.D0.BD.D0.BD.D1.8B.D1.85_.D0.BF.D0.B0.D0.BA.D0.B5.D1.82.D0.BE.D0.B2 "Pacman (Русский)") пакет [wpa_supplicant](https://www.archlinux.org/packages/?name=wpa_supplicant), доступный в [официальных репозиториях](/index.php/Official_repositories_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Official repositories (Русский)").

Также вы можете установить [wpa_supplicant_gui](https://www.archlinux.org/packages/?name=wpa_supplicant_gui), который предоставляет _wpa_gui_ – графическую оболочку для _wpa_supplicant_.

## Обзор

При установке соединения с зашифрованной беспроводной сетью _wpa_supplicant_ проходит аутентификацию у аутентификатора WPA. Для успешного завершения этого процесса _wpa_supplicant_ должен быть настроен так, чтобы иметь возможность передать правильный закрытый ключ сети аутентификатору.

После успешного завершения процесса аутентификации необходимо установить IP-адрес сетевого интерфейса вручную с помощью утилит [iproute2](/index.php/%D0%91%D0%B0%D0%B7%D0%BE%D0%B2%D1%8B%D0%B5_%D1%83%D1%82%D0%B8%D0%BB%D0%B8%D1%82%D1%8B#ip "Базовые утилиты"), либо автоматически, например с [systemd-networkd](/index.php/Systemd-networkd_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Systemd-networkd (Русский)") или [dhcpcd (Русский)](/index.php/Dhcpcd_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Dhcpcd (Русский)") для настройки автоматического получения IP через DHCP. Как только будет сетевому интерфейсу будет присвоен IP-адрес, станет возможо получить доступ к сети через беспроводное соединение.

Методы и примеры вы также сможете найти на страницах по [беспроводной](/index.php/Wireless_network_configuration_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#Systemd_.D1.81_wpa_supplicant_.D0.B8_.D1.81.D1.82.D0.B0.D1.82.D0.B8.D1.87.D0.B5.D1.81.D0.BA.D0.B8.D0.BC_IP "Wireless network configuration (Русский)") и [проводной](/index.php/Network_configuration_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#.D0.9D.D0.B0.D1.81.D1.82.D1.80.D0.BE.D0.B9.D0.BA.D0.B0_IP-.D0.B0.D0.B4.D1.80.D0.B5.D1.81.D0.B0 "Network configuration (Русский)") настройке сети.

## Подключение при помощи wpa_cli

Этот метод позволяет выполнить сканирование для поиска окружающих сетей, используя _wpa_cli_ – утилиту командной строки, которая может быть использована для интерактивной настройки запущенного _wpa_supplicant_. Смотрите [wpa_cli(8)](http://linux.die.net/man/8/wpa_cli) для получения дополнительной информации.

Чтобы использовать _wpa_cli_, для _wpa_supplicant_ должен быть указан контрольный интерфейс (файл сокета), и ему должны быть даны права на обновление файла настроек. Сделать это можно создав минимальный файл настроек:

 `/etc/wpa_supplicant/example.conf` 

```
ctrl_interface=/run/wpa_supplicant
update_config=1
```

Теперь запустите _wpa_supplicant_ командой:

```
# wpa_supplicant -B -i _имя_интерфейса_ -c /etc/wpa_supplicant/example.conf

```

где _имя_интерфейса_ – имя вашего беспроводного сетевого интерфейса.

**Совет:** Чтобы определить имя беспроводного сетевого интерфейса, используйте команду `ip link`.

Теперь запустите _wpa_cli_:

```
# wpa_cli

```

Будет отображено приглашение для ввода команд (`>`), где вы можете использовать автодополнение по `Tab` и получать описание для дополняемых команд.

**Совет:** Расположение сокета может быть указано вручную с помощью опции `-p`; с помощью `-i` можно также указать имя сетевого интерфейса. Если имя не указано явно, будет использоваться первый найденный беспроводной интерфейс, управляемый _wpa_supplicant_.

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

Чтобы подключиться к сети `MYSSID`, добавьте новую сеть (`add_network`), укажите ее идентификатор (_ssid_) и пароль для доступа к сети (`set_network`), затем включите ее (`enable_network`):

```
> add_network
0
> set_network 0 ssid "MYSSID"
> set_network 0 psk "passphrase"
> enable_network 0
<2>CTRL-EVENT-CONNECTED – Connection to 00:00:00:00:00:00 completed (reauth) [id=0 id_str=]

```

**Обратите внимание:**

*   Каждая сеть нумеруется с нуля, поэтому первая сеть имеет индекс 0.
*   [Закрытый ключ (PSK)](https://en.wikipedia.org/wiki/Pre-shared_key "wikipedia:Pre-shared key") сети вычисляется на основе парольной фразы, заключенной в кавычки, что вы также можете заметить, прочитав раздел [wpa_passphrase](#.D0.9F.D0.BE.D0.B4.D0.BA.D0.BB.D1.8E.D1.87.D0.B5.D0.BD.D0.B8.D0.B5_.D0.BF.D1.80.D0.B8_.D0.BF.D0.BE.D0.BC.D0.BE.D1.89.D0.B8_wpa_passphrase). Тем не менее, вы можете ввести закрытый ключ напрямую, введя его в команде `set_network _id_ psk` _без_ кавычек.

Теперь сохраните внесенные изменения в файл настроек:

```
> save_config
OK

```

Как только сопряжение с сетью будет выполнено, все, что останется сделать – получить IP адрес, как было указано в разделе [#Обзор](#.D0.9E.D0.B1.D0.B7.D0.BE.D1.80), например:

```
# dhcpcd _имя_интерфейса_

```

### Подключение при помощи wpa_passphrase

Этот метод позволяет быстро соединиться с сетью, SSID которой известен, используя _wpa_passphrase_ – утилиту командной строки, которая генерирует текст минимальной необходимой конфигурации для _wpa_supplicant_. Пример:

 `$ wpa_passphrase MYSSID passphrase` 

```
network={
    ssid="MYSSID"
    #psk="passphrase"
    psk=59e0d07fa4c7741797a4e394f38a5c321e3bed51d54ad5fcbd3f84bc7415d73d
}
```

Так как текст попадает в стандартный вывод, вы можете сразу вызвать _wpa_supplicant_, передавая ему настройки:

```
# wpa_supplicant -B -i _имя_интерфейса_ -c <(wpa_passphrase MYSSID passphrase)

```

**Note:** Из-за подстановки процесса, вы **не можете** запускать эту команду из [sudo](/index.php/Sudo "Sudo"): вам нужен постоянный сеанс суперпользователя. Смотрите также [Help:Reading#Regular user or root](/index.php/Help:Reading#Regular_user_or_root "Help:Reading").

**Совет:**

*   Используйте кавычки, если строка содержит пробелы, например: `"secret passphrase"`.
*   Чтобы определить имя беспроводного сетевого интерфейса, используйте команду `ip link`.
*   Парольные фразы с некоторыми нестандартными символами могут потребовать ввода из файла: `wpa_passphrase MYSSID < passphrase.txt`.

Как только сопряжение с сетью будет выполнено, вам останется получить IP адрес, как было указано в разделе [#Обзор](#.D0.9E.D0.B1.D0.B7.D0.BE.D1.80), например:

```
# dhcpcd _имя_интерфейса_

```

## Расширенное использование

Для более сложных сетей, например, широко практикующих использование [EAP](https://en.wikipedia.org/wiki/Extensible_Authentication_Protocol "wikipedia:Extensible Authentication Protocol"), будет необходимо вручную настроить _wpa_supplicant_. На странице [wpa_supplicant.conf(5)](http://linux.die.net/man/5/wpa_supplicant.conf) вы можете найти описание структуры и содержимого файла настроек и примеры файлов; более детальное описание всех опций вы можете найти в файле `/etc/wpa_supplicant/wpa_supplicant.conf`.

### Настройка

Как уже было сказано в разделе [#Сопряжение при помощи wpa_passphrase](#.D0.A1.D0.BE.D0.BF.D1.80.D1.8F.D0.B6.D0.B5.D0.BD.D0.B8.D0.B5_.D0.BF.D1.80.D0.B8_.D0.BF.D0.BE.D0.BC.D0.BE.D1.89.D0.B8_wpa_passphrase), минимальная конфигурация может быть создана при помощи команды:

```
# wpa_passphrase _SSID_сети_ _парольная_фраза_ > /etc/wpa_supplicant/example.conf

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

В дальнейшем блоки `network` могут быть добавлены вручную либо с использованием _wpa_cli_, как показано в разделе [#Подключение при помощи wpa_cli](#.D0.9F.D0.BE.D0.B4.D0.BA.D0.BB.D1.8E.D1.87.D0.B5.D0.BD.D0.B8.D0.B5_.D0.BF.D1.80.D0.B8_.D0.BF.D0.BE.D0.BC.D0.BE.D1.89.D0.B8_wpa_cli). Чтобы использовать _wpa_cli_, должен быть указан контрольный интерфейс при помощи опции `ctrl_interface`. Установка `GROUP=wheel` позволяет пользователям этой группы использовать _wpa_cli_. Также добавьте `update_config=1`, чтобы изменения, сделанные в _wpa_cli_ могли сохраняться в файл.

Опции `fast_reauth=1` и `ap_scan=1` установлены глобально. Нужны они вам или нет зависит от того, к какому типу сети вы хотите подключиться. Если вам нужны прочие глобальные опции, просто скопируйте их из `/etc/wpa_supplicant/wpa_supplicant.conf`.

Также вы можете использовать команду `wpa_cli set` для отображения текущего состояния опций и установки их значений. Несколько блоков `network` можно добавить в файл настроек: _wpa_supplicant_ сможет работать с каждой из них. По умолчанию, производится подключение к сети с наиболее сильным сигналом; если это поведение нежелательно, вы можете использовать опцию `priority` для установки числового значения приоритета.

Преимущество размещения настроек в `/etc/wpa_supplicant/wpa_supplicant.conf` в том, что этот файл по умолчанию использует [dhcpcd](/index.php/Dhcpcd "Dhcpcd"). Обратите внимание, что, кроме подробного описания опций в комментариях, некоторые опции добавлены в файл незакомментированными, в том числе и набор блоков `network`, приведенный там в качестве примера, которые однажды могут привести к незапланированному подключению к чужой сети с совпавшим SSID. Возможно, вы захотите сохранить резервную копию этого файла для примера, и создать новый файл для своих настроек на этом месте. В любом случае, при наличии изменений в новых версиях стандартного файла конфигурации должно произойти безопасное [слияние](/index.php/Pacnew_and_Pacsave_files "Pacnew and Pacsave files").

**Обратите внимание:** Начиная с версии dhcpcd-6.10.0-1 поведение демона по умолчанию изменено: теперь хук 10-wpa_supplicant не запускается по умолчанию! Подробнее: [[1]](https://bbs.archlinux.org/viewtopic.php?id=207416), [[2]](https://gentoo.org/support/news-items/2016-01-08-some-dhcpcd-hooks-are-now-examples.html)

**Совет:** Чтобы настроить блок `network` для соединения с беспроводной сетью со скрытым SSID, добавьте в него опцию `scan_ssid=1`.

### Установка соединения

#### Вручную

Запустите _wpa_supplicant_. Наиболее распространенные опции команды:

*   `-B` – запуск в фоновом режиме.
*   `-c _filename_` – путь до файла настроек.
*   `-i _interface_` – сетевой интерфейс.
*   `-D _driver_` – опционально позволяет указать драйвер адаптера. Для получения списка поддерживаемых драйверов наберите `wpa_supplicant -h`.
    *   `nl80211` в данный момент является стандартным, но не все модули беспроводных контроллеров поддерживают его.
    *   `wext` устарел, однако, все еще широко поддерживается.

Полный список поддерживаемых опций ищите в руководстве [wpa_supplicant(8)](http://linux.die.net/man/8/wpa_supplicant).

Пример вызова _wpa_supplicant_:

```
# wpa_supplicant -B -i _имя_интерфейса_ -c /etc/wpa_supplicant/example.conf

```

Когда будет произведено успешное сопряжение с беспроводной сетью, вы сможете получить IP-адрес, как было указано в разделе [#Обзор](#.D0.9E.D0.B1.D0.B7.D0.BE.D1.80), например:

```
# systemctl enable dhcpcd@_interface_

```

**Совет:** _dhcpcd_ имеет хук, который может неявно запускать _wpa_supplicant_, подробнее смотрите на странице [dhcpcd (Русский)#10-wpa_supplicant](/index.php/Dhcpcd_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#10-wpa_supplicant "Dhcpcd (Русский)").

#### При загрузке (systemd)

Пакет _wpa_supplicant_ предоставляет множество файлов служб [systemd](/index.php/Systemd_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Systemd (Русский)"):

*   `wpa_supplicant.service` – использует [D-Bus](/index.php/D-Bus "D-Bus"), рекомендуется для пользователей [NetworkManager](/index.php/NetworkManager "NetworkManager").
*   `wpa_supplicant@.service` – принимает имя интерфейса в качестве аргумента и запускает на нем демон _wpa_supplicant_, который прочитывает настройки из файла `/etc/wpa_supplicant/wpa_supplicant-_имя_интерфейса_.conf`.
*   `wpa_supplicant-nl80211@.service` – также позволяет указать интерфейс, кроме того указывает _wpa_supplicant_ использовать драйвер `nl80211`. Используется файл настроек `/etc/wpa_supplicant/wpa_supplicant-nl80211-_имя_интерфейса_.conf`.
*   `wpa_supplicant-wired@.service` – также позволяет указать интерфейс, кроме того указывает _wpa_supplicant_ использовать драйвер `wired`. Используется файл настроек `/etc/wpa_supplicant/wpa_supplicant-wired-_имя_интерфейса_.conf`.

Чтобы соединение автоматически выполнялось при старте системы, включите одну из предоставленных служб, например:

```
# systemctl enable wpa_supplicant@_имя_интерфейса_

```

Когда будет произведено успешное сопряжение с беспроводной сетью, вы сможете получить IP-адрес, как было указано в разделе [#Обзор](#.D0.9E.D0.B1.D0.B7.D0.BE.D1.80), например:

```
# systemctl enable dhcpcd@_interface_

```

**Совет:** _dhcpcd_ имеет хук, который может неявно запускать _wpa_supplicant_, подробнее смотрите на странице [dhcpcd (Русский)#10-wpa_supplicant](/index.php/Dhcpcd_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#10-wpa_supplicant "Dhcpcd (Русский)").

### Скрипт обработки событий на основе wpa_cli

_wpa_cli_ может выполняться как демон и запускать указанный скрипт для событий, генерируемых _wpa_supplicant_. Поддерживаются два события: `CONNECTED` и `DISCONNECTED`. Некоторые [переменные окружения](/index.php/Environment_variables_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Environment variables (Русский)") доступны для использовании в скрипте, смотрите [wpa_cli(8)](http://linux.die.net/man/8/wpa_cli) для получения подробной информации.

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

Не забудьте сделать файл скрипта исполняемым, затем укажите его при запуске _wpa_cli_ с помощью опции `-a`:

```
$ wpa_cli -a _/путь/до/скрипта_

```

## Смотрите также

*   [домашняя страница WPA Supplicant](http://hostap.epitest.fi/wpa_supplicant/)
*   [примеры использования wpa_cli](https://gist.github.com/buhman/7162560)
*   [wpa_supplicant(8)](http://linux.die.net/man/8/wpa_supplicant)
*   [wpa_supplicant.conf(5)](http://linux.die.net/man/5/wpa_supplicant.conf)
*   [wpa_cli(8)](http://linux.die.net/man/8/wpa_cli)
*   [документация wpa_supplicant на Kernel.org](http://wireless.kernel.org/en/users/Documentation/wpa_supplicant)

Retrieved from "[https://wiki.archlinux.org/index.php?title=WPA_supplicant_(Русский)&oldid=415072](https://wiki.archlinux.org/index.php?title=WPA_supplicant_(Русский)&oldid=415072)"

[Categories](/index.php/Special:Categories "Special:Categories"):

*   [Wireless networking (Русский)](/index.php/Category:Wireless_networking_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Category:Wireless networking (Русский)")
*   [Русский](/index.php/Category:%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9 "Category:Русский")