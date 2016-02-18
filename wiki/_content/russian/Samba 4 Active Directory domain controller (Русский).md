Эта статья объясняет, как настроить новый контроллер домена Active Directory. Предполагается, что после установки все файлы настроек находятся в неизменённом состоянии. Эта статья была написана и протестирована на свежей установке, без каких-либо других установок (сетевое соединение статического IPv4, назначение имени хоста, добавление [OpenSSH](/index.php/Secure_Shell_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Secure Shell (Русский)") и [Vim](/index.php/Vim_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Vim (Русский)")), которые не должны иметь никакого влияния на настройки [Samba](/index.php/Samba_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Samba (Русский)"). Большинство приведенных ниже команд потребует повышенных привелегий (прав суперпользователя). Несмотря на здравый смысл, проще запустить несколько этих коротких команд из сессии root, чем получать права по мере необходимости.

## Contents

*   [1 Установка](#.D0.A3.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B0)
*   [2 Резервирование](#.D0.A0.D0.B5.D0.B7.D0.B5.D1.80.D0.B2.D0.B8.D1.80.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D0.B5)
    *   [2.1 Объяснение параметров (аргументов)](#.D0.9E.D0.B1.D1.8A.D1.8F.D1.81.D0.BD.D0.B5.D0.BD.D0.B8.D0.B5_.D0.BF.D0.B0.D1.80.D0.B0.D0.BC.D0.B5.D1.82.D1.80.D0.BE.D0.B2_.28.D0.B0.D1.80.D0.B3.D1.83.D0.BC.D0.B5.D0.BD.D1.82.D0.BE.D0.B2.29)
    *   [2.2 Interactive provision explanations](#Interactive_provision_explanations)
*   [3 Настройка демонов](#.D0.9D.D0.B0.D1.81.D1.82.D1.80.D0.BE.D0.B9.D0.BA.D0.B0_.D0.B4.D0.B5.D0.BC.D0.BE.D0.BD.D0.BE.D0.B2)
    *   [3.1 NTPD](#NTPD)
    *   [3.2 BIND](#BIND)
    *   [3.3 Клиентские утилиты Kerberos](#.D0.9A.D0.BB.D0.B8.D0.B5.D0.BD.D1.82.D1.81.D0.BA.D0.B8.D0.B5_.D1.83.D1.82.D0.B8.D0.BB.D0.B8.D1.82.D1.8B_Kerberos)
    *   [3.4 DNS](#DNS)
    *   [3.5 Samba](#Samba)
*   [4 Тестирование установки](#.D0.A2.D0.B5.D1.81.D1.82.D0.B8.D1.80.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D0.B5_.D1.83.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B8)
    *   [4.1 DNS](#DNS_2)
    *   [4.2 Аутентификация NT](#.D0.90.D1.83.D1.82.D0.B5.D0.BD.D1.82.D0.B8.D1.84.D0.B8.D0.BA.D0.B0.D1.86.D0.B8.D1.8F_NT)
    *   [4.3 Kerberos](#Kerberos)
*   [5 Расширенная настройка](#.D0.A0.D0.B0.D1.81.D1.88.D0.B8.D1.80.D0.B5.D0.BD.D0.BD.D0.B0.D1.8F_.D0.BD.D0.B0.D1.81.D1.82.D1.80.D0.BE.D0.B9.D0.BA.D0.B0)
    *   [5.1 DNS](#DNS_3)
    *   [5.2 SSL](#SSL)
    *   [5.3 DHCP](#DHCP)
*   [6 Что делать дальше](#.D0.A7.D1.82.D0.BE_.D0.B4.D0.B5.D0.BB.D0.B0.D1.82.D1.8C_.D0.B4.D0.B0.D0.BB.D1.8C.D1.88.D0.B5)

## Установка

Полностью функциональный Samba 4 DC требует несколько программ, помимо тех, которые включенны в дистрибутив Samba. [Установите](/index.php/Install "Install") пакеты [bind-tools](https://www.archlinux.org/packages/?name=bind-tools), [krb5](https://www.archlinux.org/packages/?name=krb5), [ntp](https://www.archlinux.org/packages/?name=ntp), [openldap](https://www.archlinux.org/packages/?name=openldap), и [samba](https://www.archlinux.org/packages/?name=samba).

Кроме того, Самба содержит свой собственный полнофункциональный DNS-сервер, но многие администраторы предпочитают использовать пакет ISC BIND. Если вам нужна поддержка DNS зон для внешних доменов, вам настоятельно рекомендуется использовать [bind](https://www.archlinux.org/packages/?name=bind). Для совместного использования принтеров, воспользуйтесь [cups](https://www.archlinux.org/packages/?name=cups). При необходимости, поставьте пакет(ы) [bind](https://www.archlinux.org/packages/?name=bind) и/или [cups](https://www.archlinux.org/packages/?name=cups).

## Резервирование

Первый шаг к созданию домена Active Directory является создание резервов. Если это первый контроллер домена в новом домене (как предполагает это руководство), это подразумевает создание внутреннего LDAP, Kerberos и DNS-серверов и выполнение всех базовых настроек, необходимых для каталога. Вы должны быть в курсе потенциальных ошибок, созданных этими индивидуальными компонентами и работающих, как единое целое. Причина этой трудности в том, что разработчики Samba решили не использовать сервер MIT Kerberos или Heimdal или сервер OpenLDAP в пользу выбора внутренних версих этих программ. Выше были установлены пакеты сервера только для клиентских программ. С Samba 4 резервирование проще. Выполните следующую команду:

```
# samba-tool domain provision --use-rfc2307 --use-xattrs=yes --interactive

```

### Объяснение параметров (аргументов)

	--use-rfc2307

	этот параметр добавляет POSIX атрибуты (UID / GID) на схеме AD. Это понадобится при аутендификации клиентов Linux, BSD, or OS X (в том числе на локальной машине) в дополнение к Microsoft Windows.

	--use-xattrs=yes

	этот параметр включает расширенное использование атрибутов unix (ACLs) для файлов, размещенных на этом сервере. Если вы не будете открывать доступ файлов на контроллере домена, пропустите этот аргумент (но это не рекомендуется). Вы также должны убедиться, что все файловые системы, которые будут принимать открыт доступ Samba, установлены с поддержкой ACL's.

	--interactive

	этот параметр заставляет сценарий резерва запускаться в интерактивном режиме. Alternately, you can review the help for the provision step by running `samba-tool domain provision --help`.

### Interactive provision explanations

	Realm

	**INTERNAL.DOMAIN.COM** - должен быть таким же, как и домен DNS в верхнем регистре. Является общим для использования внутреннего только суб-домена, чтобы отделить внутреннюю область от ваших внешних доменов DNS, но это не обязательно.

	Domain

	**INTERNAL** - тут указывается доменное имя NetBIOS, как правило, leftmost DNS-суб-домен, но может быть все что угодно. Внутреннее имя, например, будет не наглядным. Возможно, будет уместно название компании или инициалы. Это должно вводится во всех шапках, и содержать максимум 15 символов, для совместимости со старыми клиентами.

	Server Role

	**dc** - Этот пункт предполагает, что в новом домене установлен первый DC. Если вы выберите что-то другое, то остальная часть статьи, вероятно, будет бесполезна для вас.

	DNS Backend

	**BIND9_DLZ** или **SAMBA_INTERNAL** - This is down to personal preference of the server admin. Again, if you are hosting DNS for external domains, you are strongly encouraged to use the **BIND9_DLZ** backend so that flat zone files can continue to be used and existing transfer rules can co-exist with the internal DNS server. Если вы не уверены, используйте бакэнд **SAMBA_INTERNAL**.

	Administrator password

	**xxxxxxxx** - Вы должны задать *сложный* пароль для аккаунта администратора. Минимальным требованием являются: одна буква в верхнем регистре, одна цифра, и не менее восьми символов. Если вы попытаетесь использовать пароль, который не отвечает требованиям сложности, инициализации не удастся.

## Настройка демонов

### NTPD

Создайте подходящую настройку сервера времени NTP. Для пояснения и настройки дополнительных опций смотрите [Ntpd](/index.php/Network_Time_Protocol_daemon_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Network Time Protocol daemon (Русский)"). Создать резервную копию файла по умолчанию:

```
# mv /etc/ntp.conf{,.default}

```

Создайте файл `/etc/ntp.conf` со следующим содержимым:

```
# Начало /etc/ntp.conf

# Ассоцииация с публичным пулом серверов NTP
server 0.pool.ntp.org
server 1.pool.ntp.org
server 2.pool.ntp.org

# Расположение drift file
driftfile /var/lib/ntp/ntpd.drift

# Расположение файла log'ов
logfile /var/log/ntpd

# Расположение каталога обновлений
ntpsigndsocket /var/lib/samba/ntp_signd/

# Ограничения
restrict default kod limited nomodify notrap nopeer mssntp
restrict 127.0.0.1
restrict ::1
restrict 0.pool.ntp.org mask 255.255.255.255 nomodify notrap nopeer noquery
restrict 1.pool.ntp.org mask 255.255.255.255 nomodify notrap nopeer noquery
restrict 2.pool.ntp.org mask 255.255.255.255 nomodify notrap nopeer noquery

# Конец /etc/ntp.conf

```

Создайте каталог и установите права:

```
# install -d /var/lib/samba/ntp_signd
# chown root:ntp /var/lib/samba/ntp_signd
# chmod 0750 /var/lib/samba/ntp_signd

```

Включите и запустите службу `ntpd`.

### BIND

Если вы решили использовать **BIND9_DLZ** DNS бэкенд, [установите](/index.php/Install "Install") пакет [bind](https://www.archlinux.org/packages/?name=bind) и создайте следующую конфигурацию BIND. Смотрите [BIND](/index.php/BIND "BIND") для объяснения, и дополнительных опций настройки. Замените символы **x** на верные, подходящие значения: Для начала, создайте резервную копию файла настроек по умолчанию:

```
# mv /etc/named.conf{,.default}

```

Создайте файл `/etc/named.conf`:

```
//Begin /etc/named.conf

// Global options
options {
    auth-nxdomain yes;
    datasize default;
    directory "/var/named";
    empty-zones-enable no;
    pid-file "/run/named/named.pid";
    tkey-gssapi-keytab "/var/lib/samba/private/dns.keytab";
    forwarders { **xxx.xxx.xxx.xxx**; **xxx.xxx.xxx.xxx**; };
//  Uncomment the next line to enable IPv6
//    listen-on-v6 { any; };
//  Add this for no IPv4:
//    listen-on { none; };
    notify no;
//  Add any subnets or hosts you want to allow to use this DNS server (use "; " delimiter)
    allow-query     { **xxx.xxx.xxx.xxx/xx**; 127.0.0.0/8; };
//  Add any subnets or hosts you want to allow to use recursive queries
    allow-recursion { **xxx.xxx.xxx.xxx/xx**; 127.0.0.0/8; };
//  Add any subnets or hosts you want to allow dynamic updates from
    allow-update    { **xxx.xxx.xxx.xxx/xx**; 127.0.0.0/8; };
    version none;
    hostname none;
    server-id none;
};

//Root servers (required zone for recursive queries)
zone "." IN {
    type hint;
    file "root.hint";
};

//Required localhost forward-/reverse zones
zone "localhost" IN {
    type master;
    file "localhost.zone";
//  allow-transfer { any; };
};
zone "0.0.127.in-addr.arpa" IN {
    type master;
    file "127.0.0.zone";
//  allow-transfer { any; };
};
// Uncomment the following zone for IPv6 support
//zone "1.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.ip6.arpa" IN {
//    type master;
//    file "localhost.ip6.zone";
//    allow-transfer { any; };
//};

//Load AD integrated zones
dlz "AD DNS Zones" {
    database "dlopen /usr/lib/samba/bind9/dlz_bind9_10.so";
};

//Log settings
logging {
   channel xfer-log {
       file "/var/log/named.log";
       print-category yes;
       print-severity yes;
       print-time yes;
       severity info;
    };
    category xfer-in { xfer-log; };
    category xfer-out { xfer-log; };
    category notify { xfer-log; };
};

//End /etc/named.conf

```

Установка разрешений:

```
# chgrp named /var/lib/samba/private/dns.keytab
# chmod g+r /var/lib/samba/private/dns.keytab
# touch /var/log/named.log
# chown root:named /var/log/named.log
# chmod 664 /var/log/named.log

```

Включите и запустите службу `named`.

Good values for forwarders are your ISP's DNS servers. Google (8.8.8.8, 8.8.4.4, 2001:4860:4860::8888, и 2001:4860:4860::8844) и OpenDNS (208.67.222.222, 208.67.220.220, 2620:0:ccc::2 and 2620:0:ccd::2) provide suitable public DNS servers free of charge. Соответствующие значения для подсетей характерны для вашей сети.

### Клиентские утилиты Kerberos

Шаг инициализации выше, создал совершенно правильный файл krb5.conf для использования с Samba 4 DC. Установите его с помощью следующих команд:

```
# mv /etc/krb5.conf{,.default}
# cp /var/lib/samba/private/krb5.conf /etc

```

### DNS

Сейчас вам нужно будет начать использовать локальный сервер DNS. Если ваши файлы настройки интерфейса используют Resolvconf, перенастройте их соответствующим образом. Создайте `/etc/resolv.conf.tail` (не забудьте заменить **internal.domain.tld** с внутреннего домена):

```
# Samba configuration
search **internal.domain.tld**
# If using IPv6, uncomment the following line
#nameserver ::1
nameserver 127.0.0.1

```

Установите права и пересоздайте новый файл `/etc/resolv.conf`

```
# chmod 644 /etc/resolv.conf.tail
# resolvconf -u

```

### Samba

Включите и запустите службу `samba`. Если вы намерены использовать утилиты LDB utilities, вам также понадобится создать файл `/etc/profile.d/sambaldb.sh` чтобы задать **LDB_MODULES_PATH**:

```
export LDB_MODULES_PATH="${LDB_MODULES_PATH}:/usr/lib/samba/ldb"

```

Установка разрешения и выполнения на файл:

```
# chmod 0755 /etc/profile.d/sambaldb.sh
# . /etc/profile.d/sambaldb.sh

```

## Тестирование установки

### DNS

Во-первых, убедитесь, что DNS-работает, как и ожидалось. Выполните следующие команды, заменяя соответствующие значения для **internal.domain.com** и **server**:

```
# host -t SRV _ldap._tcp.**internal.domain.com**.
# host -t SRV _kerberos._udp.**internal.domain.com**.
# host -t A **server**.**internal.domain.com**.

```

Вы должны получить результат, похожий на следующий:

```
_ldap._tcp.internal.domain.com has SRV record 0 100 389 server.internal.domain.com.
_kerberos._udp.internal.domain.com has SRV record 0 100 88 server.internal.domain.com.
server.internal.domain.com has address xxx.xxx.xxx.xxx
```

### Аутентификация NT

Убедитесь, что проверка подлинности пароля работает, как и ожидалось:

```
# smbclient //localhost/netlogon -U Administrator -c 'ls'

```

Вам будет предложено ввести пароль (тот, который вы выбрали ранее), и после получите список каталогов:

```
Domain=[INTERNAL] OS=[Unix] Server=[Samba 4.1.2]
  .                                   D        0  Wed Nov 27 23:59:07 2013
  ..                                  D        0  Wed Nov 27 23:59:12 2013

		50332 blocks of size 2097152\. 47185 blocks available
```

### Kerberos

Проверьте раоту KDC. Замените **INTERNAL.DOMAIN.COM** используя заглавные буквы:

```
# kinit administrator@**INTERNAL.DOMAIN.COM**

```

Вам будет предложено ввести пароль и вы получите результат, похожий на следующий:

 `Warning: Your password will expire in 41 days on Wed 08 Jan 2014 11:59:11 PM CST` 

Убедитесь, что вы на самом деле получил тикет:

```
# klist

```

Вы должны получить результат, похожий на:

```
Ticket cache: FILE:/tmp/krb5cc_0
Default principal: administrator@INTERNAL.DOMAIN.COM

Valid starting       Expires              Service principal
11/28/2013 00:22:17  11/28/2013 10:22:17  krbtgt/INTERNAL.DOMAIN.COM@INTERNAL.DOMAIN.COM
	renew until 11/29/2013 00:22:14
```

В качестве последнего испытания, используйте smbclient с недавно приобретенным тикетом. Замените **server** на правильное имя сервера:

```
# smbclient //**server**/netlogon -k -c 'ls'

```

Вывод должен быть такой же, как при тестировании парольной аутентификации выше.

## Расширенная настройка

### DNS

Вы также должны создать зону обратного просмотра для каждой подсети в вашей среде DNS. Важно, что это хранится в DNS Samba как противоположность BIND для обеспечения динамического обновления клиентов. Для каждой подсети, создайте зону обратного просмотра с помощью следующих команд. Замените **server**.**internal**.**domain**.**tld** и **xxx**.**xxx**.**xxx** с соответствующими значениями. Для **xxx**.**xxx**.**xxx**, используйте первые три байта подсети в обратном порядке (например: 192.168.0.0/24 станет 0.168.192):

```
# samba-tool dns zonecreate **server**.**internal**.**domain**.**tld** **xxx**.**xxx**.**xxx**.in-addr.arpa

```

Теперь добавьте запись для вашего сервера (если ваш сервер multi-homed, добавьте для каждой подсети) снова заменяя соответствующие значения, как указано выше. **zzz** будет замененён четвёртым октетом IP для сервера:

```
# samba-tool dns add **server**.**internal**.**domain**.**tld** **xxx**.**xxx**.**xxx**.in-addr.arpa **zzz** PTR **server**.**internal**.**domain**.**tld**

```

Перезапустите службу `samba`. При использовании BIND для DNS, перезапустите также сервис `named`.

Наконец, проверьте поиск. Замените **xxx**.**xxx**.**xxx**.**xxx** с IP вашего сервера:

```
# host -t PTR **xxx**.**xxx**.**xxx**.**xxx**

```

Вы должны получить результат, похожий на следующий:

```
xxx.xxx.xxx.xxx.in-addr.arpa domain name pointer server.internal.domain.tld.

```

### SSL

По умолчанию, поддержка SSL не включена, однако, сертификат по умолчанию был создан когда поднимался DC. Для использования ключей по умолчанию, добавьте следующие строки в секцию "**[global]**" файла `/etc/samba/smb.conf`:

```
        tls enabled  = yes
        tls keyfile  = tls/key.pem
        tls certfile = tls/cert.pem
        tls cafile   = tls/ca.pem

```

Если необходим доверенный сертификат, создайте ключ подписи и запрос на сертификат с помощью следующих команд (убедитесь, что общее имя совпадает с полным доменным именем сервера и не вводите пароль):

```
# cd /var/lib/samba/private/tls
# openssl genpkey -algorithm RSA -pkeyopt rsa_keygen_bits:2048 -out **NETBIOS**_KEY.pem
# openssl req -new -key **NETBIOS**_KEY.pem -out **NETBIOS**_CSR.pem

```

Получите выбранной сертификации подписанный CSR, имя соответствующее (**NETBIOS**_CERT.pem для этого примера), и положите в этуже папку.

Если вашему сертификату авторизации также нужен сертификат интермедиа, положите его тамже, и используйте **tls cafile** Parmeter (иначе оставьте **tls cafile** пустым).

Чтобы изменения вступили в силу, перезапустите `samba`.

### DHCP

Следует отметить, что с помощью этого метода, повлиеяем на функциональность windows клиентов, так как они будут по-прежнему пытаться обновить DNS самостоятельно и будет отказано в разрешении сделать так, как запись будет принадлежать пользователю DHCP. Вы должны создать объект групповой политики (GPO), чтобы преодолеть это, но, к сожалению, Samba 4 еще не имеют утилиту командной строки для изменения объектов GPO, так что вам будет нужен установленный в Windows PC RSAT. Просто создайте выделенный GPO с помощью редактора групповой политики (Group Policy Editor), применяются только к подразделениям, которые содержат рабочие станции (так, что серверы можно по-прежнему обновлять с помощью 'ipconfig /registerdns') и настройте следующие параметры:

```
Computer Configuration
  Policies
    Administrative Templates
      Network
        DNS Client
          Dynamic Update = Disabled
          Register PTR Records = Disabled
```

[Установите](/index.php/Install "Install") пакет [dhcp](https://www.archlinux.org/packages/?name=dhcp).

Создайте непривилегированного пользователя в AD для выполнения обновления. При запросе пароля, используйте безопасный пароль. Достаточно 63 случайных, смешанных, буквенно-циферных символов. По желанию samba-tool также берет случайный аргумент:

```
# samba-tool user create dhcp --description="Unprivileged user for DNS updates via DHCP server"

```

Since this is a service account, disabling password expiration on the user account is recommended, but not required:

```
# samba-tool user setexpiry dhcp --noexpiry

```

Дайте пользователю привелегии администратора DNS:

```
# samba-tool group addmembers DnsAdmins dhcp

```

Экспорт учетных данных пользователей private keytab:

```
# samba-tool domain exportkeytab --principal=dhcp@**INTERNAL**.**DOMAIN**.**TLD** dhcpd.keytab
# install -vdm 755 /etc/dhcpd
# mv dhcpd.keytab /etc/dhcpd
# chown root:root /etc/dhcpd/dhcpd.keytab
# chmod 400 /etc/dhcpd/dhcpd.keytab

```

Теперь, когда пользователь будет создан, создайте сценарий для выполнения обновления `/usr/local/sbin/samba-dnsupdate.sh`:

```
#!/bin/bash
# Begin samba-dnsupdate.sh
# Author: DJ Lucas <dj_AT_linuxfromscratch_DOT_org>
# kerberos_creds() courtesy of Sergey Urushkin
# http://www.kuron-germany.de/michael/blog/wp-content/uploads/2012/03/dhcpdns-sergey2.txt

# DHCP server should be authoritative for its own records, sleep for 5 seconds
# to allow unconfigured Windows hosts to create their own DNS records
# In order to use this script you should disable dynamic updates by hosts that
# will receive addresses from this DHCP server. Instructions are found here:
# https://wiki.archlinux.org/index.php/Samba_4_Active_Directory_Domain_Controller#DHCP
sleep 5

checkvalues()
{
        [ -z "${2}" ] && echo "Error: argument '${1}' requires a parameter." && exit 1

        case ${2} in

                -*)
                        echo "Error: Invalid parameter '${2}' passed to ${1}."
                        exit 1
                ;;

                *)
                        return 0
                ;;
        esac
}

showhelp()
{
echo -e "
"`basename ${0}` "uses samba-tool to update DNS records in Samba 4's DNS"
echo "server when using INTERNAL DNS or BIND9 DLZ plugin."
echo ""
echo "    Command line options (and variables):"
echo ""
echo "      -a | --action      Action for this script to perform"
echo "                         ACTION={add|delete}"
echo "      -c | --krb5cc      Path of the krb5 credential cache (optional)"
echo "                         Default: KRB5CC=/run/dhcpd.krb5cc"
echo "      -d | --domain      The DNS domain/zone to be updated"
echo "                         DOMAIN={domain.tld}"
echo "      -h | --help        Show this help message and exit"
echo "      -H | --hostname    Hostname of the record to be updated"
echo "                         HNAME={hostname}"
echo "      -i | --ip          IP address of the host to be updated"
echo "                         IP={0.0.0.0}"
echo "      -k | --keytab      Krb5 keytab to be used for authorization (optional)"
echo "                         Default: KEYTAB=/etc/dhcp/dhcpd.keytab"
echo "      -m | --mitkrb5     Use MIT krb5 client utilities"
echo "                         MITKRB5={YES|NO}"
echo "      -n | --nameserver  DNS server to be updated (must use FQDN, not IP)"
echo "                         NAMESERVER={server.internal.domain.tld}"
echo "      -p | --principal   Principal used for DNS updates"
echo "                         PRINCIPAL={user@domain.tld}"
echo "      -r | --realm       Authentication realm"
echo "                         REALM={DOMAIN.TLD}"
echo "      -z | --zone        Then name of the zone to be updated in AD.
echo "                         ZONE={zonename}
echo ""
echo "Example: $(basename $0) -d domain.tld -i 192.168.0.x -n 192.168.0.x \\"
echo "             -r DOMAIN.TLD -p user@domain.tld -H HOSTNAME -m"
echo ""
}

# Process arguments
[ -z "$1" ] && showhelp && exit 1
while [ -n "$1" ]; do
        case $1 in

                -a | --action)
                        checkvalues ${1} ${2}
                        ACTION=${2}
                        shift 2
                ;;

                -c | --krb5cc)
                        checkvalues ${1} ${2}
                        KRB5CC=${2}
                        shift 2
                ;;

                -d | --domain)
                        checkvalues ${1} ${2}
                        DOMAIN=${2}
                        shift 2
                ;;

                -h | --help)
                        showhelp
                        exit 0
                ;;

                -H | --hostname)
                        checkvalues ${1} ${2}
                        HNAME=${2%%.*}
                        shift 2
                ;;

                -i | --ip)
                        checkvalues ${1} ${2}
                        IP=${2}
                        shift 2
                ;;

                -k | --keytab)
                        checkvalues ${1} ${2}
                        KEYTAB=${2}
                        shift 2
                ;;

                -m | --mitkrb5)
                        KRB5MIT=YES
                        shift 1
                ;;

                -n | --nameserver)
                        checkvalues ${1} ${2}
                        NAMESERVER=${2}
                        shift 2
                ;;

                -p | --principal)
                        checkvalues ${1} ${2}
                        PRINCIPAL=${2}
                        shift 2
                ;;

                -r | --realm)
                        checkvalues ${1} ${2}
                        REALM=${2}
                        shift 2
                ;;

                -z | --zone)
                        checkvalues ${1} ${2}
                        ZONE=${2}
                        shift 2
                ;;

                *)
                        echo "Error!!! Unknown command line opion!"
                        echo "Try" `basename $0` "--help."
                        exit 1
                ;;
        esac
done

# Sanity checking
[ -z "$ACTION" ] && echo "Error: action not set." && exit 2
case "$ACTION" in
        add | Add | ADD)
                ACTION=ADD
        ;;
        del | delete | Delete | DEL | DELETE)
                ACTION=DEL
        ;;
        *)
                echo "Error: invalid action \"$ACTION\"." && exit 3
        ;;
esac
[ -z "$KRB5CC" ] && KRB5CC=/run/dhcpd.krb5cc
[ -z "$DOMAIN" ] && echo "Error: invalid domain." && exit 4
[ -z "$HNAME" ] && [ "$ACTION" == "ADD" ] && \
     echo "Error: hostname not set." && exit 5
[ -z "$IP" ] && echo "Error: IP address not set." && exit 6
[ -z "$KEYTAB" ] && KEYTAB=/etc/dhcp/dhcpd.keytab
[ -z "$NAMESERVER" ] && echo "Error: nameservers not set." && exit 7
[ -z "$PRINCIPAL" ] && echo "Error: principal not set." && exit 8
[ -z "$REALM" ] && echo "Error: realm not set." && exit 9
[ -z "$ZONE" ] && echo "Error: zone not set." && exit 10

# Disassemble IP for reverse lookups
OCT1=$(echo $IP | cut -d . -f 1)
OCT2=$(echo $IP | cut -d . -f 2)
OCT3=$(echo $IP | cut -d . -f 3)
OCT4=$(echo $IP | cut -d . -f 4)
RZONE="$OCT3.$OCT2.$OCT1.in-addr.arpa"

kerberos_creds() {
export KRB5_KTNAME="$KEYTAB"
export KRB5CCNAME="$KRB5CC"

if [ "$KRB5MIT" = "YES" ]; then
    KLISTARG="-s"
else
    KLISTARG="-t"
fi

klist $KLISTARG || kinit -k -t "$KEYTAB" -c "$KRB5CC" "$PRINCIPAL" || { logger -s -p daemon.error -t dhcpd kinit for dynamic DNS failed; exit 11; }
}

add_host(){
    logger -s -p daemon.info -t dhcpd Adding A record for host $HNAME with IP $IP to zone $ZONE on server $NAMESERVER
    samba-tool dns add $NAMESERVER $ZONE $HNAME A $IP -k yes
}

delete_host(){
    logger -s -p daemon.info -t dhcpd Removing A record for host $HNAME with IP $IP from zone $ZONE on server $NAMESERVER
    samba-tool dns delete $NAMESERVER $ZONE $HNAME A $IP -k yes
}

update_host(){
    logger -s -p daemon.info -t dhcpd Removing A record for host $HNAME with IP $CURIP from zone $ZONE on server $NAMESERVER
    samba-tool dns delete $NAMESERVER $ZONE $HNAME A $CURIP -k yes
    add_host
}

add_ptr(){
    logger -s -p daemon.info -t dhcpd Adding PTR record $OCT4 with hostname $HNAME to zone $RZONE on server $NAMESERVER
    samba-tool dns add $NAMESERVER $RZONE $OCT4 PTR $HNAME.$DOMAIN -k yes
}

delete_ptr(){
    logger -s -p daemon.info -t dhcpd Removing PTR record $OCT4 with hostname $HNAME from zone $RZONE on server $NAMESERVER
    samba-tool dns delete $NAMESERVER $RZONE $OCT4 PTR $HNAME.$DOMAIN -k yes
}

update_ptr(){
    logger -s -p daemon.info -t dhcpd Removing PTR record $OCT4 with hostname $CURHNAME from zone $RZONE on server $NAMESERVER
    samba-tool dns delete $NAMESERVER $RZONE $OCT4 PTR $CURHNAME -k yes
    add_ptr
}

case "$ACTION" in
    ADD)
        kerberos_creds
        host -t A $HNAME.$DOMAIN > /dev/null
        if [ "${?}" == 0 ]; then
          CURIP=$(host -t A $HNAME.$DOMAIN | cut -d " " -f 4 )
          if [[ "$CURIP" != "$IP" ]]; then
             update_host
          fi
        else
           add_host
        fi

        host -t PTR $IP > /dev/null
        if [ "${?}" == 0 ]; then
           CURHNAME=$(host -t PTR $IP | cut -d " " -f 5 | rev | cut -c 2- | rev)
           if [[ "$CURHNAME" != "$HNAME.$DOMAIN" ]]; then 
              update_ptr
           fi
        else
           add_ptr
        fi
    ;;

    DEL)
        kerberos_creds
        host -t A $HNAME.$DOMAIN > /dev/null
        if [ "${?}" == 0 ]; then
            delete_host
        fi

        host -t PTR $IP > /dev/null
        if [ "${?}" == 0 ]; then
            delete_ptr
        fi
    ;;

    *)
        echo "Error: Invalid action '$ACTION'!" && exit 12
    ;;

esac

# End samba-dnsupdate.sh

```

Службе dhcpd нужно будет использовать быстрый выход сценария оболочки, чтобы избежать блокировки запросов и задержек. Создайте скрипт `/etc/dhcpd/update.sh` со следующими командами (подставляя правильные значения для **server**, **internal**.**domain**.**tld**, и **INTERNAL**.**DOMAIN**.**TLD**):

```
#!/bin/bash
# Begin /etc/dhcpd/update.sh

# Variables
KRB5CC="/run/dhcpd4.krb5cc"
KEYTAB="/etc/dhcpd/dhcpd.keytab"
DOMAIN="**internal**.**domain**.**tld**"
REALM="**INTERNAL**.**DOMAIN**.**TLD**"
PRINCIPAL="dhcp@${REALM}"
NAMESERVER="**server**.${DOMAIN}"
ZONE="${DOMAIN}"

ACTION=$1
IP=$2
HNAME=$3

export KRB5CC KEYTAB DOMAIN REALM PRINCIPAL NAMESERVER ZONE ACTION IP HNAME

/usr/local/sbin/samba-dnsupdate.sh -m &

# End /etc/dhcpd/update.sh

```

Настройте сервер dhcpd после статьи [DHCPD](/index.php?title=DHCPD&action=edit&redlink=1 "DHCPD (page does not exist)"), и добавьте все следующие декларации подсети в файл `/etc/dhcpd.conf`, который обеспечит службу DHCP:

```
  on commit {
    set ClientIP = binary-to-ascii(10, 8, ".", leased-address);
    set ClientName = pick-first-value(option host-name, host-decl-name);
    execute("/etc/dhcpd/update.sh", "add", ClientIP, ClientName);
  }

  on release {
    set ClientIP = binary-to-ascii(10, 8, ".", leased-address);
    set ClientName = pick-first-value(option host-name, host-decl-name);
    execute("/etc/dhcpd/update.sh", "delete", ClientIP, ClientName);
  }

    on expiry {
    set ClientIP = binary-to-ascii(10, 8, ".", leased-address);
    set ClientName = pick-first-value(option host-name, host-decl-name);
    execute("/etc/dhcpd/update.sh", "delete", ClientIP, ClientName);

```

Вот полный пример файла `/etc/dhcpd.conf` для образца:

```
# Begin /etc/dhcpd.conf

# No DHCP service in the DMZ.
subnet 192.168.2.0 netmask 255.255.255.0 {
}

# Internal subnet
subnet 192.168.1.0 netmask 255.255.255.0 {
  range 192.168.1.100 192.168.1.199;
  option subnet-mask 255.255.255.0;
  option routers 192.168.1.254;
  option domain-name "internal.domain.tld";
  option domain-name-servers 192.168.1.1;
  option broadcast-address 192.168.1.255;
  default-lease-time 28800;
  max-lease-time 43200;
  authoritative;

  on commit {
    set ClientIP = binary-to-ascii(10, 8, ".", leased-address);
    set ClientName = pick-first-value(option host-name, host-decl-name);
    execute("/etc/dhcpd/update.sh", "add", ClientIP, ClientName);
  }

  on release {
    set ClientIP = binary-to-ascii(10, 8, ".", leased-address);
    set ClientName = pick-first-value(option host-name, host-decl-name);
    execute("/etc/dhcpd/update.sh", "delete", ClientIP, ClientName);
  }

    on expiry {
    set ClientIP = binary-to-ascii(10, 8, ".", leased-address);
    set ClientName = pick-first-value(option host-name, host-decl-name);
    execute("/etc/dhcpd/update.sh", "delete", ClientIP, ClientName);
  }
}

# End /etc/dhcpd.conf

```

Установите права:

```
# chmod 750 /usr/local/sbin/samba-dnsupdate.sh
# chmod 750 /etc/dhcpd/update.sh

```

Наконец, включите и запустите (или перезапустите) службу `dhcpd4`.

## Что делать дальше

Если вы зашли настолько далеко, что не покинули указанных выше испытаний, - вы на верном пути. Поздравляем! Вот некоторые темы, по расширению вашего сервера AD:

[Active Directory Integration](/index.php/Active_Directory_Integration "Active Directory Integration") - This article explains how to attach Linux clients to an Active Directory domain.

[OpenChange server](/index.php/OpenChange_server "OpenChange server") - The OpenChange project provides a Microsoft Exchange compatible mail server using only open source software.