**Состояние перевода:** На этой странице представлен перевод статьи [ProtonVPN](/index.php/ProtonVPN "ProtonVPN"). Дата последней синхронизации: 14 июня 2019\. Вы можете [помочь](/index.php/ArchWiki_Translation_Team_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "ArchWiki Translation Team (Русский)") синхронизировать перевод, если в английской версии произошли [изменения](https://wiki.archlinux.org/index.php?title=ProtonVPN&diff=0&oldid=575507).

Ссылки по теме

*   [OpenVPN (Русский)](/index.php/OpenVPN_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "OpenVPN (Русский)")

[ProtonVPN](https://www.protonvpn.com) — VPN провайдер, использующий протокол OpenVPN.

Для использования необходим аккаунт ProtonVPN.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Установка](#Установка)
*   [2 Использование](#Использование)
*   [3 Советы и рекомендации](#Советы_и_рекомендации)
    *   [3.1 Сохранение аутентификации OpenVPN](#Сохранение_аутентификации_OpenVPN)
    *   [3.2 Включение VPN при загрузке](#Включение_VPN_при_загрузке)
*   [4 protonvpn-cli](#protonvpn-cli)
    *   [4.1 Установка](#Установка_2)
    *   [4.2 Использование](#Использование_2)

## Установка

[Установите](/index.php/%D0%A3%D1%81%D1%82%D0%B0%D0%BD%D0%BE%D0%B2%D0%B8%D1%82%D0%B5 "Установите") пакет [openvpn](https://www.archlinux.org/packages/?name=openvpn).

## Использование

Войдите в ProtonVPN и загрузите один или несколько файлов конфигурации OpenVPN.

Скопируйте конфигурационные файлы клиента (*.ovpn) в `/etc/openvpn/client/` и сделайте резервную копию оригинала.

Выполните [следующие действия](/index.php/OpenVPN#Update_systemd-resolved_script "OpenVPN"), чтобы убедиться, что весь сетевой трафик использует VPN. Если используется systemd старше версии 229, выполните [следующие действия](/index.php/OpenVPN#Update_resolv-conf_script "OpenVPN").

Подключитесь к VPN:

```
# openvpn /etc/openvpn/client/client_config_file.ovpn

```

Нажмите `Ctrl+C`, чтобы закрыть VPN-соединение.

## Советы и рекомендации

### Сохранение аутентификации OpenVPN

Если надоело вводить имя пользователя и пароль, сохраните учётные данные OpenVPN в отдельном файле для их автоматического использования при аутентификации.

 `/etc/openvpn/client/client_config_file.ovpn` 
```
auth-user-pass /etc/openvpn/client/login.conf

```
 `/etc/openvpn/client/login.conf` 
```
имя_пользователя_openvpn
пароль_пользователя_openvpn

```

### Включение VPN при загрузке

См. раздел [OpenVPN#systemd service configuration](/index.php/OpenVPN#systemd_service_configuration "OpenVPN") для получения информации о настройке службы systemd.

## protonvpn-cli

ProtonVPN предоставляет утилиту для доступа к VPN. Подробности доступны на [официальном сайте](https://protonvpn.com/support/linux-vpn-tool/) и в [GitHub-репозитории](https://github.com/ProtonVPN/protonvpn-cli).

### Установка

[Установите](/index.php/%D0%A3%D1%81%D1%82%D0%B0%D0%BD%D0%BE%D0%B2%D0%B8%D1%82%D0%B5 "Установите") пакет [protonvpn-cli](https://aur.archlinux.org/packages/protonvpn-cli/).

### Использование

Инициализируйте клиент:

```
# protonvpn-cli -init

```

Введите имя пользователя и пароль OpenVPN, которые необходимо настроить на странице [настроек ProtonVPN](https://account.protonvpn.com/settings). Например:

```
Enter OpenVPN username: ProtonVPN.user
Enter OpenVPN password:

```

После ввода учётных данных необходимо выбрать ваш план подписки. Например, выберите бесплатный (Free) план:

```
[.]ProtonVPN Plans:
1) Free
2) Basic
3) Plus
4) Visionary
Enter Your ProtonVPN plan ID: 1

```

Теперь можно подключиться к VPN:

```
# protonvpn-cli -connect

```

Должен отобразиться подробный список стран с доступными серверами. Выберите предпочитаемый сервер и нажмите ОК.

Далее выберите протокол UDP или TCP и снова нажмите OK.

При успешном подключении отобразится следующий вывод:

```
Connecting...
Connected!
New IP: X.X.X.X

```