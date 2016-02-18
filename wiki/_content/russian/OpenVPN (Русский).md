Эта статья описывает базовую установку и настройку [OpenVPN](http://openvpn.net), чего достаточно для частного использования или малой офисной сети. Больше информации можно найти на странице [OpenVPN 2.3 man page](https://community.openvpn.net/openvpn/wiki/Openvpn23ManPage) и на странице [OpenVPN документации](http://openvpn.net/index.php/open-source/documentation).

OpenVPN -- мощный и гибкий кроссплатформенный [VPN](https://en.wikipedia.org/wiki/ru:VPN через [прокси](https://en.wikipedia.org/wiki/ru:%D0%9F%D1%80%D0%BE%D0%BA%D1%81%D0%B8-%D1%81%D0%B5%D1%80%D0%B2%D0%B5%D1%80 "wikipedia:ru:Прокси-сервер") или [NAT](https://en.wikipedia.org/wiki/ru:NAT "wikipedia:ru:NAT"), поддерживает [DHCP](https://en.wikipedia.org/wiki/ru:DHCP "wikipedia:ru:DHCP"), масштабируется на сотни и тысячи пользователей.

OpenVPN тесно связан с [OpenSSL](http://www.openssl.org) библиотеками и механизмы шифрования основаны в основном на нем.

OpenVPN поддерживает простое шифрование с [pre-shared secret key](https://en.wikipedia.org/wiki/Pre-shared_key "wikipedia:Pre-shared key") (режим статического ключа) или [SSL/TLS](https://en.wikipedia.org/wiki/ru:TLS "wikipedia:ru:TLS") (режим [открытого ключа безопасности)](https://en.wikipedia.org/wiki/ru:%D0%9A%D1%80%D0%B8%D0%BF%D1%82%D0%BE%D1%81%D0%B8%D1%81%D1%82%D0%B5%D0%BC%D0%B0_%D1%81_%D0%BE%D1%82%D0%BA%D1%80%D1%8B%D1%82%D1%8B%D0%BC_%D0%BA%D0%BB%D1%8E%D1%87%D0%BE%D0%BC "wikipedia:ru:Криптосистема с открытым ключом") с использованием клиентских и серверных сертификатов. OpenVPN так же поддерживает незашифрованные TCP/UDP туннели.

OpenVPN использует [TUN/TAP](https://en.wikipedia.org/wiki/ru:TUN/TAP "wikipedia:ru:TUN/TAP") виртуальные сетевые интерфейсы, поддерживаемые на множестве платформ. В целом, OpenVPN предлагает многие из основных особенностей [IPSec](https://en.wikipedia.org/wiki/ru:Ipsec "wikipedia:ru:Ipsec")

OpenVPN была написана James Yonan и распространяется под лицензией [GNU General Public License (GPL)](https://en.wikipedia.org/wiki/GNU_General_Public_License "wikipedia:GNU General Public License").

## Contents

*   [1 Установка OpenVPN](#.D0.A3.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B0_OpenVPN)
*   [2 Настройка поддержки TUN/TAP](#.D0.9D.D0.B0.D1.81.D1.82.D1.80.D0.BE.D0.B9.D0.BA.D0.B0_.D0.BF.D0.BE.D0.B4.D0.B4.D0.B5.D1.80.D0.B6.D0.BA.D0.B8_TUN.2FTAP)
*   [3 Подключение к VPN, предоставляемой третьей стороной](#.D0.9F.D0.BE.D0.B4.D0.BA.D0.BB.D1.8E.D1.87.D0.B5.D0.BD.D0.B8.D0.B5_.D0.BA_VPN.2C_.D0.BF.D1.80.D0.B5.D0.B4.D0.BE.D1.81.D1.82.D0.B0.D0.B2.D0.BB.D1.8F.D0.B5.D0.BC.D0.BE.D0.B9_.D1.82.D1.80.D0.B5.D1.82.D1.8C.D0.B5.D0.B9_.D1.81.D1.82.D0.BE.D1.80.D0.BE.D0.BD.D0.BE.D0.B9)
*   [4 Инфраструктура открытых ключей](#.D0.98.D0.BD.D1.84.D1.80.D0.B0.D1.81.D1.82.D1.80.D1.83.D0.BA.D1.82.D1.83.D1.80.D0.B0_.D0.BE.D1.82.D0.BA.D1.80.D1.8B.D1.82.D1.8B.D1.85_.D0.BA.D0.BB.D1.8E.D1.87.D0.B5.D0.B9)
*   [5 Основная конфигурация L3 IP маршрутизации](#.D0.9E.D1.81.D0.BD.D0.BE.D0.B2.D0.BD.D0.B0.D1.8F_.D0.BA.D0.BE.D0.BD.D1.84.D0.B8.D0.B3.D1.83.D1.80.D0.B0.D1.86.D0.B8.D1.8F_L3_IP_.D0.BC.D0.B0.D1.80.D1.88.D1.80.D1.83.D1.82.D0.B8.D0.B7.D0.B0.D1.86.D0.B8.D0.B8)
    *   [5.1 Конфигурация сервера](#.D0.9A.D0.BE.D0.BD.D1.84.D0.B8.D0.B3.D1.83.D1.80.D0.B0.D1.86.D0.B8.D1.8F_.D1.81.D0.B5.D1.80.D0.B2.D0.B5.D1.80.D0.B0)
    *   [5.2 Конфигурация клиента](#.D0.9A.D0.BE.D0.BD.D1.84.D0.B8.D0.B3.D1.83.D1.80.D0.B0.D1.86.D0.B8.D1.8F_.D0.BA.D0.BB.D0.B8.D0.B5.D0.BD.D1.82.D0.B0)
    *   [5.3 Проверка настроек OpenVPN](#.D0.9F.D1.80.D0.BE.D0.B2.D0.B5.D1.80.D0.BA.D0.B0_.D0.BD.D0.B0.D1.81.D1.82.D1.80.D0.BE.D0.B5.D0.BA_OpenVPN)
    *   [5.4 Настройка размеров MTU и MSS](#.D0.9D.D0.B0.D1.81.D1.82.D1.80.D0.BE.D0.B9.D0.BA.D0.B0_.D1.80.D0.B0.D0.B7.D0.BC.D0.B5.D1.80.D0.BE.D0.B2_MTU_.D0.B8_MSS)
*   [6 Запуск OpenVPN](#.D0.97.D0.B0.D0.BF.D1.83.D1.81.D0.BA_OpenVPN)
    *   [6.1 Ручной старт](#.D0.A0.D1.83.D1.87.D0.BD.D0.BE.D0.B9_.D1.81.D1.82.D0.B0.D1.80.D1.82)
    *   [6.2 Настройка запуска через systemd](#.D0.9D.D0.B0.D1.81.D1.82.D1.80.D0.BE.D0.B9.D0.BA.D0.B0_.D0.B7.D0.B0.D0.BF.D1.83.D1.81.D0.BA.D0.B0_.D1.87.D0.B5.D1.80.D0.B5.D0.B7_systemd)
        *   [6.2.1 OpenVPN не поднимается после выхода из сна](#OpenVPN_.D0.BD.D0.B5_.D0.BF.D0.BE.D0.B4.D0.BD.D0.B8.D0.BC.D0.B0.D0.B5.D1.82.D1.81.D1.8F_.D0.BF.D0.BE.D1.81.D0.BB.D0.B5_.D0.B2.D1.8B.D1.85.D0.BE.D0.B4.D0.B0_.D0.B8.D0.B7_.D1.81.D0.BD.D0.B0)
*   [7 Развертывание L3 IP маршрутизации](#.D0.A0.D0.B0.D0.B7.D0.B2.D0.B5.D1.80.D1.82.D1.8B.D0.B2.D0.B0.D0.BD.D0.B8.D0.B5_L3_IP_.D0.BC.D0.B0.D1.80.D1.88.D1.80.D1.83.D1.82.D0.B8.D0.B7.D0.B0.D1.86.D0.B8.D0.B8)
    *   [7.1 Необходимые условия для маршрутизации локальной сети](#.D0.9D.D0.B5.D0.BE.D0.B1.D1.85.D0.BE.D0.B4.D0.B8.D0.BC.D1.8B.D0.B5_.D1.83.D1.81.D0.BB.D0.BE.D0.B2.D0.B8.D1.8F_.D0.B4.D0.BB.D1.8F_.D0.BC.D0.B0.D1.80.D1.88.D1.80.D1.83.D1.82.D0.B8.D0.B7.D0.B0.D1.86.D0.B8.D0.B8_.D0.BB.D0.BE.D0.BA.D0.B0.D0.BB.D1.8C.D0.BD.D0.BE.D0.B9_.D1.81.D0.B5.D1.82.D0.B8)
        *   [7.1.1 IPv4 переадресация](#IPv4_.D0.BF.D0.B5.D1.80.D0.B5.D0.B0.D0.B4.D1.80.D0.B5.D1.81.D0.B0.D1.86.D0.B8.D1.8F)
        *   [7.1.2 Неразборчивый режим LAN интерфейса](#.D0.9D.D0.B5.D1.80.D0.B0.D0.B7.D0.B1.D0.BE.D1.80.D1.87.D0.B8.D0.B2.D1.8B.D0.B9_.D1.80.D0.B5.D0.B6.D0.B8.D0.BC_LAN_.D0.B8.D0.BD.D1.82.D0.B5.D1.80.D1.84.D0.B5.D0.B9.D1.81.D0.B0)
        *   [7.1.3 Маршрутизация](#.D0.9C.D0.B0.D1.80.D1.88.D1.80.D1.83.D1.82.D0.B8.D0.B7.D0.B0.D1.86.D0.B8.D1.8F)
    *   [7.2 Связь локальной сети сервера с клиентом](#.D0.A1.D0.B2.D1.8F.D0.B7.D1.8C_.D0.BB.D0.BE.D0.BA.D0.B0.D0.BB.D1.8C.D0.BD.D0.BE.D0.B9_.D1.81.D0.B5.D1.82.D0.B8_.D1.81.D0.B5.D1.80.D0.B2.D0.B5.D1.80.D0.B0_.D1.81_.D0.BA.D0.BB.D0.B8.D0.B5.D0.BD.D1.82.D0.BE.D0.BC)
    *   [7.3 Связь локальной сети клиента с сервером](#.D0.A1.D0.B2.D1.8F.D0.B7.D1.8C_.D0.BB.D0.BE.D0.BA.D0.B0.D0.BB.D1.8C.D0.BD.D0.BE.D0.B9_.D1.81.D0.B5.D1.82.D0.B8_.D0.BA.D0.BB.D0.B8.D0.B5.D0.BD.D1.82.D0.B0_.D1.81_.D1.81.D0.B5.D1.80.D0.B2.D0.B5.D1.80.D0.BE.D0.BC)
    *   [7.4 Связь клиента и сервера с их локальными сетями](#.D0.A1.D0.B2.D1.8F.D0.B7.D1.8C_.D0.BA.D0.BB.D0.B8.D0.B5.D0.BD.D1.82.D0.B0_.D0.B8_.D1.81.D0.B5.D1.80.D0.B2.D0.B5.D1.80.D0.B0_.D1.81_.D0.B8.D1.85_.D0.BB.D0.BE.D0.BA.D0.B0.D0.BB.D1.8C.D0.BD.D1.8B.D0.BC.D0.B8_.D1.81.D0.B5.D1.82.D1.8F.D0.BC.D0.B8)
    *   [7.5 Связь клиентов с другими локальными сетями](#.D0.A1.D0.B2.D1.8F.D0.B7.D1.8C_.D0.BA.D0.BB.D0.B8.D0.B5.D0.BD.D1.82.D0.BE.D0.B2_.D1.81_.D0.B4.D1.80.D1.83.D0.B3.D0.B8.D0.BC.D0.B8_.D0.BB.D0.BE.D0.BA.D0.B0.D0.BB.D1.8C.D0.BD.D1.8B.D0.BC.D0.B8_.D1.81.D0.B5.D1.82.D1.8F.D0.BC.D0.B8)
*   [8 L2 Ethernet мосты](#L2_Ethernet_.D0.BC.D0.BE.D1.81.D1.82.D1.8B)
*   [9 Contributions that do not yet fit into the main article](#Contributions_that_do_not_yet_fit_into_the_main_article)
    *   [9.1 Routing client traffic through the server](#Routing_client_traffic_through_the_server)
        *   [9.1.1 Configure ufw for routing](#Configure_ufw_for_routing)
        *   [9.1.2 Использование iptables](#.D0.98.D1.81.D0.BF.D0.BE.D0.BB.D1.8C.D0.B7.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D0.B5_iptables)
    *   [9.2 Deprecated older wiki content](#Deprecated_older_wiki_content)
        *   [9.2.1 Using PAM and passwords to authenticate](#Using_PAM_and_passwords_to_authenticate)
        *   [9.2.2 Аутентификация по сертификатам](#.D0.90.D1.83.D1.82.D0.B5.D0.BD.D1.82.D0.B8.D1.84.D0.B8.D0.BA.D0.B0.D1.86.D0.B8.D1.8F_.D0.BF.D0.BE_.D1.81.D0.B5.D1.80.D1.82.D0.B8.D1.84.D0.B8.D0.BA.D0.B0.D1.82.D0.B0.D0.BC)
        *   [9.2.3 Routing traffic through the server](#Routing_traffic_through_the_server)
        *   [9.2.4 Setting up the client](#Setting_up_the_client)
            *   [9.2.4.1 With password authentication](#With_password_authentication)
            *   [9.2.4.2 Certificates authentication](#Certificates_authentication)
            *   [9.2.4.3 DNS](#DNS)
            *   [9.2.4.4 Webmin](#Webmin)
        *   [9.2.5 Connecting to the server](#Connecting_to_the_server)
*   [10 Troubleshooting](#Troubleshooting)
    *   [10.1 Resolve issues](#Resolve_issues)
*   [11 Ссылки](#.D0.A1.D1.81.D1.8B.D0.BB.D0.BA.D0.B8)

## Установка OpenVPN

[Установите](/index.php/%D0%A3%D1%81%D1%82%D0%B0%D0%BD%D0%BE%D0%B2%D0%B8%D1%82%D0%B5 "Установите") [openvpn](https://www.archlinux.org/packages/?name=openvpn) из [официального репозитория](/index.php/Official_repositories_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Official repositories (Русский)").

**Обратите внимание:** Пакет OpenVPN поддерживает режим как сервера, так и клиента, поэтому установите его на всех машинах, которые должны создать VPN-соединение.

## Настройка поддержки TUN/TAP

OpenVPN требует поддержки TUN/TAP. Удостоверьтесь в загрузке `tun` модуля.

Прочтите [Kernel modules (Русский)](/index.php/Kernel_modules_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Kernel modules (Русский)").

По умолчанию ядро уже настроено, но если Вы используете другое ядро, тогда проверьте что модуль TUN/TAP загружен. Если `$ zgrep CONFIG_TUN /proc/config.gz` возвратит `CONFIG_TUN=n`, тогда перенастройте конфигурационный файл ядра и пересоберите ядро.

 `Kernel config file` 
```
 Device Drivers
  --> Network device support
    [M] Universal TUN/TAP device driver support
```

## Подключение к VPN, предоставляемой третьей стороной

Для подключения к VPN, предоставленной третьей стороной, большинство текста ниже скорее всего может не пригодиться. Используйте сертификаты и инструкции, предоставленные поставщиком, например см.: [Airvpn](/index.php/Airvpn "Airvpn").

**Note:** To connect to servers of the most VPN providers that offer free service, one can plainly use [PPTP Server](/index.php/PPTP_Server_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "PPTP Server (Русский)") since most offers only this protocol.

## Инфраструктура открытых ключей

При настройке OpenVPN с нуля нужно создать [инфраструктуру открытых ключей (PKI)](https://en.wikipedia.org/wiki/ru:%D0%98%D0%BD%D1%84%D1%80%D0%B0%D1%81%D1%82%D1%80%D1%83%D0%BA%D1%82%D1%83%D1%80%D0%B0_%D0%BE%D1%82%D0%BA%D1%80%D1%8B%D1%82%D1%8B%D1%85_%D0%BA%D0%BB%D1%8E%D1%87%D0%B5%D0%B9 "wikipedia:ru:Инфраструктура открытых ключей")

Создайте необходимые сертификаты и ключи следуя [Create a Public Key Infrastructure Using the easy-rsa Scripts](/index.php/Create_a_Public_Key_Infrastructure_Using_the_easy-rsa_Scripts "Create a Public Key Infrastructure Using the easy-rsa Scripts").

Передайте эти файлы по защищенному каналу машинам, которые будут использовать OpenVPN.

**Обратите внимание:** Далее будет предполагаться, что ключи и сертификаты будут расположены в `/etc/openvpn`.

Публичный сертификат *ca.crt* нужен как серверу так и клиенту. Ключ *ca.key* секретный используется только машиной, генерируемой ключи и сертификаты.

Для сервера необходимы server.crt, dh2048.pem server.key и *ta.key*.

Для клиента нужны *client.crt*, *client.key*, и *ta.key*.

## Основная конфигурация L3 IP маршрутизации

**Обратите внимание:** Если иное не оговорено, остальная часть этой статьи предполагает эту базовую конфигурацию.

OpenVPN является чрезвычайно универсальным программным обеспечением, позволяющим настроить конфигурацию на любой вкус, где одна машина может одновременно являться сервером и клиентом, делая их между собой неразличимыми.

То, что действительно отличает сервер от клиента (помимо используемого типа сертификата) является сам конфигурационный файл.OpenVPN демон при запуске считывает все файлы конфигурации *.conf* в `/etc/openvpn` и запускается в соответсвии с ними . Если он находит более одного файла конфигурации, он запустит один процесс OpenVPN на каждый файл конфигурации.

Эта статья объясняет, как настроить сервер с именем elmer и клиент, который подключается к ней по имени bugs. Серверы и клиенты могут быть легко добавлены путем создания новых пар ключ/сертификат и файлов конфигурации сервера и клиента.

Пакет OpenVPN поставляется с набором файлов-примеров конфигураций для различных целей. Эти файлы будут идеальной отправной точкой для базовой настройки OpenVPN со следующими характеристиками:

*   Использует [инфраструктуру открытых ключей (PKI)](https://en.wikipedia.org/wiki/ru:%D0%98%D0%BD%D1%84%D1%80%D0%B0%D1%81%D1%82%D1%80%D1%83%D0%BA%D1%82%D1%83%D1%80%D0%B0_%D0%BE%D1%82%D0%BA%D1%80%D1%8B%D1%82%D1%8B%D1%85_%D0%BA%D0%BB%D1%8E%D1%87%D0%B5%D0%B9 "wikipedia:ru:Инфраструктура открытых ключей") для аутентификации.
*   Созданет VPN, используя виртуальный TUN сетевой интерфейс (OSI L3 IP маршрутизации).
*   Слушает 1194 UDP порт для клиентских подключений (OpenVPN [официальный зарегистрированный IANA порт](https://en.wikipedia.org/wiki/%D0%9F%D0%BE%D1%80%D1%82_(%D0%BA%D0%BE%D0%BC%D0%BF%D1%8C%D1%8E%D1%82%D0%B5%D1%80%D0%BD%D1%8B%D0%B5_%D1%81%D0%B5%D1%82%D0%B8) "wikipedia:Порт (компьютерные сети)")).
*   Раздает виртуальные адреса подключенным клиентам из 10.8.0.0/24 подсети

Для более продвинутых конфигураций смотрите официальную [OpenVPN 2.2 справочную страницу](http://openvpn.net/index.php/manuals/427-openvpn-22.html) и [документацию OpenVPN](http://openvpn.net/index.php/open-source/documentation).

### Конфигурация сервера

Скопируйте пример конфигурационного файла сервера в `/etc/openvpn/server.conf`:

```
# cp /usr/share/openvpn/examples/server.conf /etc/openvpn/server.conf

```

Отредактируйте следующее:

*   Параметры `ca`, `cert`, `key`, и `dh`, указав путь, имена ключей и сертификатов. Указанные абсолютные пути позволят вам запустить OpenVPN из любого каталога для проверки.
*   Включите HMAC защиту SSL/TLS . **Обратите внимание на использование параметра 0 для сервера**.
*   В целях безопасности рекомендуется запускать OpenVPN с пониженными правами. Раскомментируйте строки `user` и `group`.

 `/etc/openvpn/server.conf` 
```
ca /etc/openvpn/ca.crt
cert /etc/openvpn/elmer.crt
key /etc/openvpn/elmer.key

dh /etc/openvpn/dh2048.pem

tls-auth /etc/openvpn/ta.key **0**

user nobody
group nobody

```

**Обратите внимание:** Обратите внимание, что если сервер находится за брандмауэром или за NAT маршрутизатора, вам придется пробросить порт OpenVPN UDP (1194) на сервер

### Конфигурация клиента

Скопируйте пример конфигурационного файла клиента в `/etc/openvpn/client.conf`:

```
# cp /usr/share/openvpn/examples/client.conf /etc/openvpn/client.conf

```

Отредактируйте следующее:

*   В `remote` строке укажите подключаемый сервер [Полное имя домена](https://en.wikipedia.org/wiki/ru:FQDN "wikipedia:ru:FQDN"), hostname (as known to the client), либо IP адрес.
*   Раскоментируйте `user` и `group` строки для понижения привилегий.
*   Параметры `ca`, `cert`, and `key` указав путь, имена ключей и сертификатов.
*   Включите HMAC защиту SSL/TLS . **Обратите внимание на использование параметра 1 для клиента**.

 `/etc/openvpn/client.conf` 
```
remote elmer.acmecorp.org 1194
.
.
user nobody
group nobody
.
.
ca /etc/openvpn/ca.crt
cert /etc/openvpn/bugs.crt
key /etc/openvpn/bugs.key
.
.
tls-auth /etc/openvpn/ta.key **1**

```

### Проверка настроек OpenVPN

Запустите `# openvpn /etc/openvpn/server.conf` на сервере, и `# openvpn /etc/openvpn/client.conf` на клиенте. Вы должны увидеть следующее:

 `# openvpn /etc/openvpn/server.conf` 
```
Wed Dec 28 14:41:26 2011 OpenVPN 2.2.1 x86_64-unknown-linux-gnu [SSL] [LZO2] [EPOLL] [eurephia] built on Aug 13 2011
Wed Dec 28 14:41:26 2011 NOTE: OpenVPN 2.1 requires '--script-security 2' or higher to call user-defined scripts or executables
Wed Dec 28 14:41:26 2011 Diffie-Hellman initialized with 2048 bit key
.
.
Wed Dec 28 14:41:54 2011 bugs/95.126.136.73:48904 MULTI: primary virtual IP for bugs/95.126.136.73:48904: 10.8.0.6
Wed Dec 28 14:41:57 2011 bugs/95.126.136.73:48904 PUSH: Received control message: 'PUSH_REQUEST'
Wed Dec 28 14:41:57 2011 bugs/95.126.136.73:48904 SENT CONTROL [bugs]: 'PUSH_REPLY,route 10.8.0.1,topology net30,ping 10,ping-restart 120,ifconfig 10.8.0.6 10.8.0.5' (status=1)
```
 `# openvpn /etc/openvpn/client.conf` 
```
Wed Dec 28 14:41:50 2011 OpenVPN 2.2.1 i686-pc-linux-gnu [SSL] [LZO2] [EPOLL] [eurephia] built on Aug 13 2011
Wed Dec 28 14:41:50 2011 NOTE: OpenVPN 2.1 requires '--script-security 2' or higher to call user-defined scripts or executables
Wed Dec 28 14:41:50 2011 LZO compression initialized
.
.
Wed Dec 28 14:41:57 2011 GID set to nobody
Wed Dec 28 14:41:57 2011 UID set to nobody
Wed Dec 28 14:41:57 2011 Initialization Sequence Completed
```

На сервере найдите IP адрес назначенный интерфейсу tunX:

 `# ip addr show` 
```
.
.
40: tun0: <POINTOPOINT,MULTICAST,NOARP,UP,LOWER_UP> mtu 1500 qdisc pfifo_fast state UNKNOWN qlen 100
    link/none
    inet 10.8.0.1 peer 10.8.0.2/32 scope global tun0
```

Here we see that the server end of the tunnel has been given the IP address 10.8.0.1. Здесь мы видим, что серверу туннеля был выдан IP-адрес 10.8.0.1.

Сделайте то же самое на клиенте:

 `# ip addr show` 
```
.
.
37: tun0: <POINTOPOINT,MULTICAST,NOARP,UP,LOWER_UP> mtu 1500 qdisc pfifo_fast state UNKNOWN qlen 100
    link/none
    inet 10.8.0.6 peer 10.8.0.5/32 scope global tun0
```

И на стороне клиента был выдан IP-адрес 10.8.0.6.

Теперь попробуйте пропинговать интерфейсы

На сервере:

 `# ping -c3 10.8.0.6` 
```
PING 10.8.0.6 (10.8.0.6) 56(84) bytes of data.
64 bytes from 10.8.0.6: icmp_req=1 ttl=64 time=238 ms
64 bytes from 10.8.0.6: icmp_req=2 ttl=64 time=237 ms
64 bytes from 10.8.0.6: icmp_req=3 ttl=64 time=205 ms

--- 10.8.0.6 ping statistics ---
3 packets transmitted, 3 received, 0% packet loss, time 2002ms
rtt min/avg/max/mdev = 205.862/227.266/238.788/15.160 ms
```

На клиенте:

 `# ping -c3 10.8.0.1` 
```
PING 10.8.0.1 (10.8.0.1) 56(84) bytes of data.
64 bytes from 10.8.0.1: icmp_req=1 ttl=64 time=158 ms
64 bytes from 10.8.0.1: icmp_req=2 ttl=64 time=158 ms
64 bytes from 10.8.0.1: icmp_req=3 ttl=64 time=157 ms

--- 10.8.0.1 ping statistics ---
3 packets transmitted, 3 received, 0% packet loss, time 2001ms
rtt min/avg/max/mdev = 157.426/158.278/158.940/0.711 ms
```

Теперь Вы имеете рабочую OpenVPN, и ваш клиент (bugs) может пользоваться сервисами сервера (Elmer) и наоборот.

**Обратите внимание:** Если используется брандмауэр, убедитесь, что IP-пакеты на TUN устройстве не блокируются.

### Настройка размеров MTU и MSS

**Обратите внимание:** Если Вы не настроите MTU, тогда будут передаваться маленькие пакеты, такие как пинг и DNS будут работать, но просмотр веб страниц работать не будет.

Теперь необходимо настроить максимальный размер сегмента (MSS). Для того чтобы сделать это, мы должны выяснить, какой MTU является наименьши между клиентом и сервером. Для этого проверьте связь с сервером и отключите фрагментацию. Укажите максимальный размер пакета.

 `# ping -c5 -M do -s 1500 elmer.acmecorp.org` 
```
PING elmer.acmecorp.org (99.88.77.66) 1500(1528) bytes of data.
From 1.2.3.4 (99.88.77.66) icmp_seq=1 Frag needed and DF set (mtu = 576)
From 1.2.3.4 (99.88.77.66) icmp_seq=1 Frag needed and DF set (mtu = 576)
From 1.2.3.4 (99.88.77.66) icmp_seq=1 Frag needed and DF set (mtu = 576)
From 1.2.3.4 (99.88.77.66) icmp_seq=1 Frag needed and DF set (mtu = 576)
From 1.2.3.4 (99.88.77.66) icmp_seq=1 Frag needed and DF set (mtu = 576)

--- core.myrelay.net ping statistics ---
0 packets transmitted, 0 received, +5 errors
```

We received an ICMP message telling us the MTU is 576 bytes. The means we need to fragment the UDP packets smaller then 576 bytes to allow for some UDP overhead.

 `# ping -c5 -M do -s 548 elmer.acmecorp.org` 
```
PING elmer.acmecorp.org (99.88.77.66) 548(576) bytes of data.
556 bytes from 99.88.77.66: icmp_seq=1 ttl=48 time=206 ms
556 bytes from 99.88.77.66: icmp_seq=2 ttl=48 time=224 ms
556 bytes from 99.88.77.66: icmp_seq=3 ttl=48 time=206 ms
556 bytes from 99.88.77.66: icmp_seq=4 ttl=48 time=207 ms
556 bytes from 99.88.77.66: icmp_seq=5 ttl=48 time=208 ms

--- myrelay.net ping statistics ---
5 packets transmitted, 5 received, 0% packet loss, time 4001ms
rtt min/avg/max/mdev = 206.027/210.603/224.158/6.832 ms
```

After some trial and error..., we discover that we need to fragment packets on 548 bytes. In order to do this we specify this fragment size in the configuration and instruct OpenVPN to fix the Maximum Segment Size (MSS).

 `/etc/openvpn/client.conf` 
```
remote elmer.acmecorp.org 1194
.
.
fragment 548
mssfix
.
.
user nobody
group nobody
.
.
ca /etc/openvpn/ca.crt
cert /etc/openvpn/bugs.crt
key /etc/openvpn/bugs.key
.
.
tls-auth /etc/openvpn/ta.key **1**

```

**Обратите внимание:** Это добавит около 3 минут к запуску OpenVPN. Желательно настроить размер фрагмента, если только ваш клиент не является ноутбуком, который будет подключен через множество различных сетей и будет горлышком бутылки на стороне клиента.

Вы также можете позволить OpenVPN делать проверку пинга каждый раз, когда клиент подключается к VPN.

 `/etc/openvpn/client.conf` 
```
remote elmer.acmecorp.org 1194
.
.
mtu-test
.
.
user nobody
group nobody
.
.
ca /etc/openvpn/ca.crt
cert /etc/openvpn/bugs.crt
key /etc/openvpn/bugs.key
.
.
tls-auth /etc/openvpn/ta.key **1**

```

## Запуск OpenVPN

### Ручной старт

Для отладки VPN подключений, запускайте демон вручную: `# openvpn /etc/openvpn/client.conf`.

### Настройка запуска через systemd

Синтаксис автозапуска OpenVPN : `systemctl [enable](/index.php/Daemon "Daemon") openvpn@*<configuration>*`.

Например, если файл конфигурации `/etc/openvpn/client.conf`, то название сервиса будет `openvpn@client.service`.

#### OpenVPN не поднимается после выхода из сна

На случай, если при возобновлении работы из спящего режима OpenVPN не перезапускается, что приводит к битому подключению:

 `/usr/lib/systemd/system-sleep/vpn.sh` 
```
#!/bin/sh
if [ "$1" == "pre" ]
then
  killall openvpn
fi
```

Дайте файлу права на исполнение `chmod a+x /usr/lib/systemd/system-sleep/vpn.sh`

Добавьте `Restart=always` в `/usr/lib/systemd/system/openvpn@.service`

## Развертывание L3 IP маршрутизации

### Необходимые условия для маршрутизации локальной сети

#### IPv4 переадресация

Чтобы хост мог пересылать IPv4 пакеты между локальной сетью и VPN, он должен уметь перенаправлять пакеты между его NIC и tun/tap устройствами.

Отредактируйте или создайте `etc/sysctl.d/99-sysctl.conf` чтобы включить постоянную пересылку пакетов IPv4 (изменения вступят в силу при следующей загрузке):

 `/etc/sysctl.d/99-sysctl.conf` 
```
# Enable packet forwarding
net.ipv4.ip_forward=1
```

**Совет:** Для временного включения без необходимости перезагрузки: `# echo 1 > /proc/sys/net/ipv4/ip_forward`

#### Неразборчивый режим LAN интерфейса

Для переадресации хост NIC (к примеру enp1s0) должен быть установлен в таком состоянии, чтобы он мог принимать пакеты с отличных от настроенного IP-адреса, называемом [неразборчивый режим](https://en.wikipedia.org/wiki/ru:Promiscuous_mode и задействуйте его, выполнив:

```
 # systemctl enable promiscuous@enp1s0

```

**Совет:** Чтобы временно включить без перезагрузки, выполните: `# ip link set dev enp1s0 promisc on`.

**Обратите внимание:** Хорошим тоном будет отдать эту работу правилу MASQUERADE.

#### Маршрутизация

По умолчанию все IP пакеты из LAN направляются на шлюз по умолчанию. Если LAN/VPN шлюз является шлюзом по умолчанию, то проблем нет. Однако в противном случае шлюз не будет знать куда направлять пакеты. Решается это следующим образом.

*   Добавлением статических маршрутов через VPN шлюз на подсеть LAN/VPN.
*   Добавлением статических маршрутов на каждый хост в сети для отправки IP пакетов обратно на VPN.
*   Использование [iptables](/index.php/Iptables_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Iptables (Русский)")' NAT на LAN/VPN шлюзе для маскарадинга входящих с VPN IP пакетов.

### Связь локальной сети сервера с клиентом

Пусть на стороне сервера используется подсеть 10.66.0.0/24\. Чтобы эта подсеть была доступна клиенту, добавьте параметр push в файл конфигурации сервера: `/etc/openvpn/server.conf`  `push "route 10.66.0.0 255.255.255.0"` 
**Обратите внимание:**

*   Не забудьте включить IPv4 переадресацию и перевести LAN интерфейс сервера в неразборчивый режим. Убедитесь, что локальная сеть на стороне сервера знает, как связаться с клиентом VPN.
*   Для маршрутизации других локальных сетей со стороны сервера к клиенту, укажите их в параметре ***push*** файла конфигурации сервера. Однако имейте в виду, что эти сети также должны знать, как установить связь с клиентом VPN.

### Связь локальной сети клиента с сервером

Необходимые условия:

*   Любая подсеть, используемая на стороне клиента, должна быть уникальной и не используемой на сервере или любом другом клиенте. Например пусть локальная подсеть клиента будет 192.168.4.0/24.
*   Сертификат каждого клиента должен иметь уникальное имя, в данном примере bugs.
*   The server may not use the duplicate-cn directive in its config file.

Создайте каталог настройки клиентов на сервере (например ccd - client config dir). Сервер в нем будет искать файлы с именем, идетничным названию клиента, и указанные в нем параметры будут применяться к клиенту при подключении.

```
# mkdir -p /etc/openvpn/ccd

```

Создайте в этом каталоге файл, назвав его *bugs*, содержащий `iroute 192.168.4.0 255.255.255.0` параметр. Это укажет серверу направлять пакеты с подсети к клиенту

 `/etc/openvpn/ccd/bugs`  `iroute 192.168.4.0 255.255.255.0` 

Добавьте в конфиг. сервера строку с параметром каталога настройки клиентов . Укажите серверу направлять пакеты подсети туннеля на сервер локальной сети `route 192.168.4.0 255.255.255.0`

 `/etc/openvpn/server.conf` 
```
client-config-dir ccd
route 192.168.4.0 255.255.255.0

```

**Обратите внимание:**

*   Не забудьте включить IPv4 переадресацию и перевести LAN интерфейс клиента в неразборчивый режим. Убедитесь, что локальная сеть на стороне клиента знает, как связаться с сервером VPN.
*   Для маршрутизации других LAN от клиента к серверу,укажите их в параметрах ***iroute*** и ***route*** в соответствующих файлах конфигурации. Однако имейте в виду, что эти подсети также должны знать, как установить связь с сервером VPN

### Связь клиента и сервера с их локальными сетями

Совмещает два предыдущих раздела:

 `/etc/openvpn/server.conf` 
```
push "route 10.66.0.0 255.255.255.0"
client-config-dir ccd
route 192.168.4.0 255.255.255.0

```
 `/etc/openvpn/ccd/bugs`  `iroute 192.168.4.0 255.255.255.0` 
**Обратите внимание:** Не забудьте включить IPv4 переадресацию и перевести в неразборчивый режим интерфейсы LAN как на клиенте и на сервере. Убедитесь в том, что все хосты локальной сети могут установить маршрут ко всем адресатам.

### Связь клиентов с другими локальными сетями

По умолчанию клиенты не видят друг друга. Чтобы разрешить обмениваться пакетами между клиентами и клиентскими сетями, добавьте *client-to-client* в файл конфигурации сервера: `/etc/openvpn/server.conf`  `client-to-client` 

Чтобы клиенты сервера и другие сети были доступны друг для друга, пропишите маршруты для каждой подсети в файл конфигурации сервера

 `/etc/openvpn/server.conf` 
```
client-to-client
push "route 192.168.4.0 255.255.255.0"
push "route 192.168.5.0 255.255.255.0"

```

**Обратите внимание:** Убедитесь, что маршрутизация настроена правильно.

## L2 Ethernet мосты

For now see: [OpenVPN Bridge](/index.php/OpenVPN_Bridge "OpenVPN Bridge")

## Contributions that do not yet fit into the main article

### Routing client traffic through the server

Append the following to your server's openvpn.conf configuration file:

```
push "redirect-gateway def1"
push "dhcp-option DNS 192.168.1.1"

```

Change "192.168.1.1" to your preferred DNS IP address.

If you have problems with non responsive DNS after connecting to server, install [BIND](/index.php/BIND "BIND") as simple DNS forwarder and push the IP address of the OpenVPN server as DNS to clients.

#### Configure ufw for routing

Configure your ufw settings to enable routing traffic from clients through server.

You must change default forward policy as in [#IPv4 forwarding](#IPv4_forwarding).

And then configure ufw in `/etc/default/ufw`:

 `/etc/default/ufw`  `DEFAULT_FORWARD_POLICY="ACCEPT"` 

Now change `/etc/ufw/before.rules`, and add the following code after the header and before the "*filter" line. Don't forget to change the IP/subnet mask to match the one in `/etc/openvpn/server.conf`.

 `/etc/ufw/before.rules` 
```
# NAT (Network Address Translation) table rules
*nat
:POSTROUTING ACCEPT [0:0]

# Allow traffic from clients to enp1s0
-A POSTROUTING -s 10.8.0.0/8 -o enp1s0 -j MASQUERADE

# don't delete the "COMMIT" line or the NAT table rules above won't be processed
COMMIT
```

Open OpenVPN port 1194:

```
ufw allow 1194

```

#### Использование iptables

Use an iptable for NAT forwarding:

```
echo 1 > /proc/sys/net/ipv4/ip_forward
iptables -t nat -A POSTROUTING -s 10.8.0.0/24 -o enp1s0 -j MASQUERADE

```

If running Arch Linux in a OpenVZ VPS environment [[1]](http://thecodeninja.net/linux/openvpn-archlinux-openvz-vps/):

```
iptables -t nat -A POSTROUTING -s 10.8.0.0/24 -o venet0 -j SNAT --to (venet0 ip)

```

If all is well, make the changes permanent:

Edit `/etc/conf.d/iptables` and change IPTABLES_FORWARD=1

```
# iptables-save > /etc/iptables/iptables.rules

```

### Deprecated older wiki content

#### Using PAM and passwords to authenticate

```
port 1194
proto udp
mtu-test
dev tap
ca /etc/openvpn/easy-rsa/keys/ca.crt
cert /etc/openvpn/easy-rsa/keys/<MYSERVER>.crt
key /etc/openvpn/easy-rsa/keys/<MYSERVER>.key
dh /etc/openvpn/easy-rsa/keys/dh2048.pem
server 192.168.56.0 255.255.255.0
ifconfig-pool-persist ipp.txt
;learn-address ./script
client-to-client
;duplicate-cn
keepalive 10 120
;tls-auth ta.key 0
comp-lzo
;max-clients 100
;user nobody
;group nobody
persist-key
persist-tun
status /var/log/openvpn-status.log
verb 3
client-cert-not-required
username-as-common-name
plugin /usr/lib/openvpn/plugins/openvpn-plugin-auth-pam.so login

```

#### Аутентификация по сертификатам

```
port 1194
proto tcp
dev tun0

ca /etc/openvpn/easy-rsa/keys/ca.crt
cert /etc/openvpn/easy-rsa/keys/<MYSERVER>.crt
key /etc/openvpn/easy-rsa/keys/<MYSERVER>.key
dh /etc/openvpn/easy-rsa/keys/dh2048.pem

server 10.8.0.0 255.255.255.0
ifconfig-pool-persist ipp.txt
keepalive 10 120
comp-lzo
user nobody
group nobody
persist-key
persist-tun
status /var/log/openvpn-status.log
verb 3

log-append /var/log/openvpn
status /tmp/vpn.status 10

```

#### Routing traffic through the server

Append the following to your server's openvpn.conf configuration file:

```
push "dhcp-option DNS 192.168.1.1"
push "redirect-gateway def1"

```

Change "192.168.1.1" to your external DNS IP address.

Use an iptable for NAT forwarding:

```
echo 1 > /proc/sys/net/ipv4/ip_forward
iptables -t nat -A POSTROUTING -s 10.8.0.0/24 -o enp1s0 -j MASQUERADE

```

If running Arch Linux in a OpenVZ VPS environment [[2]](http://thecodeninja.net/linux/openvpn-archlinux-openvz-vps/):

```
iptables -t nat -A POSTROUTING -s 10.8.0.0/24 -o venet0 -j SNAT --to (venet0 ip)

```

If all is well, make the changes permanent:

Edit `/etc/conf.d/iptables` and change IPTABLES_FORWARD=1

```
# iptables-save > /etc/iptables/iptables.rules

```

#### Setting up the client

The client-side .conf file

##### With password authentication

```
client
dev tap
proto udp
mtu-test
remote <address> 1194
resolv-retry infinite
nobind
persist-tun
comp-lzo
verb 3
auth-user-pass passwd
ca ca.crt

```

passwd file (referenced by auth-user-pass) must contain two lines:

*   first line - username
*   second - password

##### Certificates authentication

```
client
remote <MYSERVER> 1194
dev tun0
proto tcp
resolv-retry infinite
nobind
persist-key
persist-tun
verb 2
ca ca.crt
cert client1.crt
key client1.key
comp-lzo

```

Copy three files from server to remote computer.

```
ca.crt
client1.crt
client1.key

```

Install the tunnel/tap module:

```
# modprobe tun

```

To have the **tun** module loaded automatically at boot, read [Kernel modules (Русский)](/index.php/Kernel_modules_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Kernel modules (Русский)").

##### DNS

The DNS servers used by the system are defined in `/etc/resolv.conf`. Traditionally, this file is the responsibility of whichever program deals with connecting the system to the network (e.g. Wicd, NetworkManager, etc...) However, OpenVPN will need to modify this file if you want to be able to resolve names on the remote side. To achieve this in a sensible way, install [openresolv](https://www.archlinux.org/packages/?name=openresolv), which makes it possible for more than one program to modify resolv.conf without stepping on each-other's toes. Before continuing, test openresolv by restarting your network connection and ensuring that resolv.conf states that it was generated by "resolvconf", and that your DNS resolution still works as before. You should not need to configure openresolv; it should be automatically detected and used by your network system.

Next, save the following script at `/usr/share/openvpn/update-resolv-conf`:

```
#!/bin/bash
#
# Parses DHCP options from openvpn to update resolv.conf
# To use set as 'up' and 'down' script in your openvpn *.conf:
# up /etc/openvpn/update-resolv-conf
# down /etc/openvpn/update-resolv-conf
#
# Used snippets of resolvconf script by Thomas Hood <jdthood@yahoo.co.uk>
# and Chris Hanson
# Licensed under the GNU GPL.  See /usr/share/common-licenses/GPL.
# 07/2013 colin@daedrum.net Fixed intet name
# 05/2006 chlauber@bnc.ch
#
# Example envs set from openvpn:
# foreign_option_1='dhcp-option DNS 193.43.27.132'
# foreign_option_2='dhcp-option DNS 193.43.27.133'
# foreign_option_3='dhcp-option DOMAIN be.bnc.ch'
# foreign_option_4='dhcp-option DOMAIN-SEARCH bnc.local'

set -e

## You might need to set the path manually here, i.e.
# RESOLVCONF=/usr/bin/resolvconf
RESOLVCONF=$(which resolvconf)
[ -x $RESOLVCONF ] || exit 0

case $script_type in

up)
   for optionname in ${!foreign_option_*} ; do
      option="${!optionname}"
      echo $option
      part1=$(echo "$option" | cut -d " " -f 1)
      if [ "$part1" == "dhcp-option" ] ; then
         part2=$(echo "$option" | cut -d " " -f 2)
         part3=$(echo "$option" | cut -d " " -f 3)
         if [ "$part2" == "DNS" ] ; then
            IF_DNS_NAMESERVERS="$IF_DNS_NAMESERVERS $part3"
         fi
         if [[ "$part2" == "DOMAIN" || "$part2" == "DOMAIN-SEARCH" ]] ; then
            IF_DNS_SEARCH="$IF_DNS_SEARCH $part3"
         fi
      fi
   done
   R=""
   for DS in $IF_DNS_SEARCH ; do
           R="${R}search $DS
"
   done
   for NS in $IF_DNS_NAMESERVERS ; do
           R="${R}nameserver $NS
"
   done
   #echo -n "$R" | $RESOLVCONF -p -a "${dev}"
   echo -n "$R" | $RESOLVCONF -a "${dev}.inet"
   ;;
down)
   $RESOLVCONF -d "${dev}.inet"
   ;;
esac

```

Remember to make the file executable with:

```
 $ chmod +x /usr/share/openvpn/update-resolv-conf

```

Next, add the following lines to your OpenVPN client configuration file:

```
script-security 2
up /usr/share/openvpn/update-resolv-conf
down /usr/share/openvpn/update-resolv-conf

```

Now, when your launch your OpenVPN connection, you should find that your resolv.conf file is updated accordingly, and also returns to normal when your close the connection.

*Caveat: The script will fail to restore the original DNS settings if your OpenVPN client.conf is set-up to drop root privileges after connection.*

##### Webmin

[webmin-plugin-openvpn](https://aur.archlinux.org/packages/webmin-plugin-openvpn/) is available in the [AUR](/index.php/AUR "AUR").

**Обратите внимание:** You must add "openvpn" to the end of `/etc/webmin/webmin.acl`

#### Connecting to the server

You need to start the service on the server

```
systemctl start openvpn@server

```

To make it permanent:

```
systemctl enable openvpn@server

```

On the client, in the home directory create a folder that will hold your OpenVPN client config files along with the **.crt**/**.key** files. Assuming your OpenVPN config folder is called **.openvpn** and your client config file is **vpn1.conf**, to connect to the server issue the following command:

```
# cd ~/.openvpn && openvpn vpn1.conf

```

## Troubleshooting

### Resolve issues

If you are having resolve issues when starting your profile:

 `# journalctl _SYSTEMD_UNIT=openvpn@*profile*.service` 
```
RESOLVE: Cannot resolve host address: example.com: Name or service not known

```

Then, **only if your network setup can be started before OpenVPN**, you should force OpenVPN to wait for the network by adding `Requires=network.target` and `After=network.target` to the OpenVPN systemd service file:

 `/usr/lib/systemd/system/openvpn@.service` 
```
[Unit]
Description=OpenVPN connection to %i
Requires=network.target
After=network.target
...

```

Don't forget to restart OpenVPN:

```
# systemctl daemon-reload
# systemctl restart openvpn@*profile*

```

## Ссылки

*   [VPNBook Ruby Script (Free OpenVPN)](http://blog.gotux.net/code/ruby/vpnbook/)
*   [Перевод официального HOWTO](http://lithium.opennet.ru/articles/openvpn/openvpn-howto.html)