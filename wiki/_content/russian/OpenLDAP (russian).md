OpenLDAP, LDAP являются очень большой темой для описания, поэтому конфигурация довольно сложна. В этой статье описываются лишь основы установки и настройки Openldap на Archlinux.

Если вам совершенно неизвестно что такое ldap, то можете [почитать (англ)](http://www.brennan.id.au/20-Shared_Address_Book_LDAP.html) хорошую инструкцию-введение, которая легка в понимании и поможет вам разобраться в основах, даже если вы только знакомитесь с LDAP.

## Contents

*   [1 Установка](#.D0.A3.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B0)
*   [2 Настройка](#.D0.9D.D0.B0.D1.81.D1.82.D1.80.D0.BE.D0.B9.D0.BA.D0.B0)
    *   [2.1 Сервер (slapd)](#.D0.A1.D0.B5.D1.80.D0.B2.D0.B5.D1.80_.28slapd.29)
        *   [2.1.1 /etc/openldap/slapd.conf](#.2Fetc.2Fopenldap.2Fslapd.conf)
        *   [2.1.2 /etc/conf.d/slapd](#.2Fetc.2Fconf.d.2Fslapd)
    *   [2.2 Клиент](#.D0.9A.D0.BB.D0.B8.D0.B5.D0.BD.D1.82)
    *   [2.3 Тестирование установки](#.D0.A2.D0.B5.D1.81.D1.82.D0.B8.D1.80.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D0.B5_.D1.83.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B8)
    *   [2.4 OpenLDAP и SSL](#OpenLDAP_.D0.B8_SSL)
        *   [2.4.1 Создание само-подписанного сертификата](#.D0.A1.D0.BE.D0.B7.D0.B4.D0.B0.D0.BD.D0.B8.D0.B5_.D1.81.D0.B0.D0.BC.D0.BE-.D0.BF.D0.BE.D0.B4.D0.BF.D0.B8.D1.81.D0.B0.D0.BD.D0.BD.D0.BE.D0.B3.D0.BE_.D1.81.D0.B5.D1.80.D1.82.D0.B8.D1.84.D0.B8.D0.BA.D0.B0.D1.82.D0.B0)
        *   [2.4.2 Настройка slapd для использования SSL](#.D0.9D.D0.B0.D1.81.D1.82.D1.80.D0.BE.D0.B9.D0.BA.D0.B0_slapd_.D0.B4.D0.BB.D1.8F_.D0.B8.D1.81.D0.BF.D0.BE.D0.BB.D1.8C.D0.B7.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D1.8F_SSL)
        *   [2.4.3 Запуск slapd с SSL](#.D0.97.D0.B0.D0.BF.D1.83.D1.81.D0.BA_slapd_.D1.81_SSL)
*   [3 Следующие шаги](#.D0.A1.D0.BB.D0.B5.D0.B4.D1.83.D1.8E.D1.89.D0.B8.D0.B5_.D1.88.D0.B0.D0.B3.D0.B8)
*   [4 Решение проблем](#.D0.A0.D0.B5.D1.88.D0.B5.D0.BD.D0.B8.D0.B5_.D0.BF.D1.80.D0.BE.D0.B1.D0.BB.D0.B5.D0.BC)
*   [5 Внешние ссылки](#.D0.92.D0.BD.D0.B5.D1.88.D0.BD.D0.B8.D0.B5_.D1.81.D1.81.D1.8B.D0.BB.D0.BA.D0.B8)

## Установка

Установите пакет:

```
pacman -S openldap 

```

Пакет openldap обычно включает две части: серверную (slapd) и клиентскую. Возможно, вы захотите запустить сервер на своем компьютере. После того, как вы настроете его, сервер будет готов предоставить сервисы аутентификации для клиентов. It is quite likely that you will run services requiring the LDAP authentication on that very computer, in which case the LDAP client will query the LDAP server from the same package.

## Настройка

### Сервер (slapd)

Для начала необходимо подготовить каталог с базой данных. Вам необходимо скопировать дефолтный конфигурационный файл и выставить нужные права владения.

**Важно:** Приведенный пример удалит существующую базу

```
rm -rf /var/lib/openldap/openldap-data/*
cp /etc/openldap/DB_CONFIG.example /var/lib/openldap/openldap-data/DB_CONFIG
chown ldap:ldap /var/lib/openldap/openldap-data/DB_CONFIG

```

#### /etc/openldap/slapd.conf

Далее необходимо подготовить slap.conf. Добавим несколько типичных схем:

```
include         /etc/openldap/schema/cosine.schema
include         /etc/openldap/schema/nis.schema
include         /etc/openldap/schema/inetorgperson.schema

```

Измените suffix. Обычно это ваше доменное имя, но не обязательно. Это зависит от того, как вы собираетесь использовать каталог. В этом примере будет использоваться 'example' в качестве доменного имении и 'com' для TLD. Также установите имя администратора.

```
suffix     "dc=example,dc=com"
rootdn     "cn=root,dc=example,dc=com"

```

Теперь удалим стандартный пароль администратора и создадим новый, более защищенный:

```
#find the line with rootpw and delete it
sed -i "/rootpw/ d" slapd.conf
#add a line which includes the hashed password output from slappasswd
echo "rootpw    $(slappasswd)" >> slapd.conf

```

Для ускорения обработки поисковых запросов можно использовать индексацию. Смотрите [документацию](http://www.zytrax.com/books/ldap/ch6/#index) для более подробного описания

```
index   uid             pres,eq
index   mail            pres,sub,eq
index   cn              pres,sub,eq
index   sn              pres,sub,eq
index   dc              eq

```

Не забудьте запустить `slapindex` после того, как заполните директорию (перед этим необходимо остановить slapd). Затем измените владельцев всех созданных файлов:

```
chown ldap.ldap /var/lib/openldap/openldap-data/*

```

Если вы хотите использовать SSL, здесь необходимо указать путь к вашим сертификатам. См. [OpenLDAP Authentication](/index.php/OpenLDAP_Authentication "OpenLDAP Authentication")

Теперь можно запустить демон:

```
#systemctl start slapd

```

Может получиться так, что /run/openldap не существует и запуск демона не представляется возможным. Для исправления ситуации просто создайте директорию:

```
#mkdir /run/openldap

```

#### /etc/conf.d/slapd

В этом файле крайне важно определить, какой порт сервер будет прослушивать и, если вы хотите использовать SSL, вы должны использовать ldaps:// URI вместо обычного ldap:// Также здесь можно указать дополнительные опции для slapd.

### Клиент

Работа с клиентом обычно довольно просто, всего лишь необходимо знать, что ваши приложения требуют LDAP аутентификацию. Следовательно, если что-то идет не так с LDAP, не тратьте ваше время на приложение, а обратите внимание на LDAP клиент.

Конфигурационный файл клиента находится в /etc/openldap/ldap.conf Обычно он довольно прост

Если вы решите использовать SSL:

*   The protocol (ldap or ldaps) in the URI entry has to conform with the slapd configuration
*   If you decide to use self-signed certificates, you have to add them to TLS_CACERT

### Тестирование установки

Для проверки работоспособности ваших настроек запустите команду:

```
ldapsearch -x -b * -s base '(objectclass=*)' namingContexts*

```

Если все настроено правильно, вы должны увидеть информацию о вашей базе данных.

### OpenLDAP и SSL

**Примечание:** [здесь](http://www.openldap.org/pub/ksoper/OpenLDAP_TLS.html#4.0) находится более полезная и полная информация, чем то что вы увидите ниже

Если вы подключаетесь к OpenLdap серверу по сети, и особенно если у вас есть важные данные, хранящиеся на сервере, вы рискуете что кто-то может перехватить их в открытом виде. Как вариант, LDAP можно использовать на основе SSL.

Перед началом использования SSL необходимо создать сертификат. Возможно, у вас есть подписанный сертификат, или можете создать собственный Certificate Authority (CA), однако для нашей цели само-подписанного сертификата будет достаточно.

**Важно:** OpenLDAP не может использовать сертификат, который имеет пароль, связанный с ним

#### Создание само-подписанного сертификата

Для создания *само-подписанного* сертификата, используйте команду:

 `openssl req -new -x509 -nodes -out slapdcert.pem -keyout slapdkey.pem -days 365` 

Вам будет предложено ввести информацию о вашем LDAP сервере. Большая часть информации может остаться незаполненной. Самая важная часть - это common name. Это значение должно соответствовать доменному имени LDAP сервера. If your LDAP server's IP address resolves to example.org but its server certificate shows a CN of bad.example.org, LDAP clients will reject the certificate and will be unable to negotiate TLS connections (apparently the results are wholly unpredictable).

Теперь, когда файлы сертификатов созданы, скопируйте их в `/etc/openldap/ssl/` (создайте эту директорию, если необходимо) и защитите их.
**Важно** slapdcert.pem должен быть доступен всем, т.к. он содержит открытый ключ. slapdkey.pem же наоборот, должен читаться только LDAP-пользователями для лучшей безопасности

```
cp slapdcert.pem slapdkey.pem /etc/openldap/ssl/
chown ldap slapdkey.pem
chmod 400 slapdkey.pem
chmod 444 slapdcert.pem

```

#### Настройка slapd для использования SSL

Отредактируйте конфигурационный файл (`/etc/openldap/slapd.conf`) для того, чтобы сообщить LDAP, где находятся файлы сертификатов, добавив эти строки:

```
# Certificate/SSL Section
TLSCipherSuite HIGH:MEDIUM:+SSLv2
TLSCertificateFile /etc/openldap/ssl/slapdcert.pem
TLSCertificateKeyFile /etc/openldap/ssl/slapdkey.pem

```

The TLSCipherSuite specifies a list of OpenSSL ciphers from which slapd will choose when negotiating TLS connections, in decreasing order of preference. In addition to those specific ciphers, you can use any of the wildcards supported by OpenSSL. **NOTE:** HIGH, MEDIUM, and +SSLv2 are all wildcards.

**Примечание:** To see which ciphers are supported by your local OpenSSL installation, type the following: `openssl ciphers -v ALL`

#### Запуск slapd с SSL

Чтобы сообщить OpenLDAP серверу, что необходимо запуститься, используя шифрование, измените /etc/conf.d/slapd, раскомментировав строку SLAPD_SERVICES и установив значение:

 `SLAPD_SERVICES="ldaps:///"` 

Соединения localhost не нуждаются в SSL, поэтому можно использовать так:

 `SLAPD_SERVICES="ldap://127.0.0.1 ldaps:///:` 

**ВАЖНО:** Если вы создали само-подписанный сертификат, добавьте следующую строку в /etc/openldap/ldap.conf, иначе вы не сможете подключиться.

```
TLS_REQCERT allow

```

После всего этого перезапустите сервер.

## Следующие шаги

Теперь у вас есть базовая установка ldap. Далее необходимо спроектировать вашу директорию. Проектирование сильно зависит от ваших целей. If you are new to ldap, consider starting with a directory design recommended by the specific client services that will use the directory (PAM, Postfix, etc).

A directory for system authentication is the [LDAP authentication](/index.php/LDAP_authentication "LDAP authentication") article.

## Решение проблем

Если вы заметили, что slapd запускается, но затем останавливается, возможно вам поможет смена владельца этого каталога:

```
# chown ldap:ldap /var/lib/openldap/openldap-data/*

```

Этим вы добьетесь того, что slapd будет записывать данные в директорию от имени пользователя ldap.

## Внешние ссылки

*   [http://www.openldap.org/doc/admin24/](http://www.openldap.org/doc/admin24/)
*   [phpLDAPadmin](http://phpldapadmin.sourceforge.net/) - web-инструментарий в стиле phpmyadmin
*   [apachedirectorystudio2](https://aur.archlinux.org/packages/apachedirectorystudio2/) - основанная на [Eclipse](/index.php/Eclipse_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Eclipse (Русский)") программа просмотра LDAP. Идеально работает с OpenLDAP