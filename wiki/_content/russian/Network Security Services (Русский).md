**Network Security Services (NSS)** — набор библиотек, нацеленный на поддержку разработки кроссплатформенных клиентских и серверных приложений, для которых важна безопасность.

Приложения, встроенные в NSS, поддерживают [SSL](https://en.wikipedia.org/wiki/ru:SSL "wikipedia:ru:SSL") v2/v3, [TLS](https://en.wikipedia.org/wiki/ru:TLS "wikipedia:ru:TLS"), [PKCS](https://en.wikipedia.org/wiki/ru:PKCS "wikipedia:ru:PKCS") #5/#7/#11/#12, [S/MIME](https://en.wikipedia.org/wiki/ru:S/MIME "wikipedia:ru:S/MIME"), [X.509](https://en.wikipedia.org/wiki/ru:X.509 "wikipedia:ru:X.509") v3, а также прочие стандарты безопасности.

## Contents

*   [1 Установка](#.D0.A3.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B0)
*   [2 Управление сертификатами](#.D0.A3.D0.BF.D1.80.D0.B0.D0.B2.D0.BB.D0.B5.D0.BD.D0.B8.D0.B5_.D1.81.D0.B5.D1.80.D1.82.D0.B8.D1.84.D0.B8.D0.BA.D0.B0.D1.82.D0.B0.D0.BC.D0.B8)
    *   [2.1 Список сертификатов](#.D0.A1.D0.BF.D0.B8.D1.81.D0.BE.D0.BA_.D1.81.D0.B5.D1.80.D1.82.D0.B8.D1.84.D0.B8.D0.BA.D0.B0.D1.82.D0.BE.D0.B2)
    *   [2.2 Импортирование сертификата](#.D0.98.D0.BC.D0.BF.D0.BE.D1.80.D1.82.D0.B8.D1.80.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D0.B5_.D1.81.D0.B5.D1.80.D1.82.D0.B8.D1.84.D0.B8.D0.BA.D0.B0.D1.82.D0.B0)
    *   [2.3 Изменение сертификата](#.D0.98.D0.B7.D0.BC.D0.B5.D0.BD.D0.B5.D0.BD.D0.B8.D0.B5_.D1.81.D0.B5.D1.80.D1.82.D0.B8.D1.84.D0.B8.D0.BA.D0.B0.D1.82.D0.B0)
    *   [2.4 Удаление сертификата](#.D0.A3.D0.B4.D0.B0.D0.BB.D0.B5.D0.BD.D0.B8.D0.B5_.D1.81.D0.B5.D1.80.D1.82.D0.B8.D1.84.D0.B8.D0.BA.D0.B0.D1.82.D0.B0)
*   [3 Добавление сертификатов WebMoney](#.D0.94.D0.BE.D0.B1.D0.B0.D0.B2.D0.BB.D0.B5.D0.BD.D0.B8.D0.B5_.D1.81.D0.B5.D1.80.D1.82.D0.B8.D1.84.D0.B8.D0.BA.D0.B0.D1.82.D0.BE.D0.B2_WebMoney)
*   [4 Смотрите также](#.D0.A1.D0.BC.D0.BE.D1.82.D1.80.D0.B8.D1.82.D0.B5_.D1.82.D0.B0.D0.BA.D0.B6.D0.B5)

## Установка

[Установите](/index.php/Pacman_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#.D0.A3.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B0_.D0.BE.D0.BF.D1.80.D0.B5.D0.B4.D0.B5.D0.BB.D0.B5.D0.BD.D0.BD.D1.8B.D1.85_.D0.BF.D0.B0.D0.BA.D0.B5.D1.82.D0.BE.D0.B2 "Pacman (Русский)") пакет [nss](https://www.archlinux.org/packages/?name=nss), доступный в [официальных репозиториях](/index.php/Official_repositories_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Official repositories (Русский)").

## Управление сертификатами

Для управления сертификатами используйте утилиту *certutil*, входящую в состав пакета NSS.

### Список сертификатов

Показать список установленных сертификатов:

```
$ certutil -d sql:$HOME/.pki/nssdb -L

```

Показать подробную информацию о сертификате:

```
$ certutil -d sql:$HOME/.pki/nssdb -L -n *имя_сертификата*

```

### Импортирование сертификата

Для добавления сертификата используйте опцию `-A`:

```
$ certutil -d sql:$HOME/.pki/nssdb -A -t "*TRUSTARGS*" -n *имя_сертификата* -i */путь/к/файлу/сертификата*

```

Аргумент `TRUSTARGS` состоит из трех групп, разделенных запятыми. Каждая группа представляет собой набор букв (флагов), которые определяют доверие сертификата для SSL, электронной почты и подписи объектов, например `"TCu,Cu,Tuw"`. Их описание вы можете найти в [документации certutil](http://www.mozilla.org/projects/security/pki/nss/tools/certutil.html#1034193) или [в этой статье от Meena](https://blogs.oracle.com/meena/entry/notes_about_trust_flags).

Для добавления персонального сертификата и личного ключа для SSL авторизации используйте:

```
$ pk12util -d sql:$HOME/.pki/nssdb -i */путь/к/файлу/сертификата/PKCS12.p12*

```

Данная команда импортирует персональный сертификат и личный ключ в файле PKCS #12\. Аргумент `TRUSTARGS` персонального сертификата будет установлен как `"u,u,u"`.

### Изменение сертификата

Вызовите *certutil* с опцией `-M` для редактирования параметров сертификата. Например, для редактирования списка `TRUSTARGS`:

```
$ certutil -d sql:$HOME/.pki/nssdb -M -t "*TRUSTARGS*" -n *имя_сертификата*

```

### Удаление сертификата

Используйте опцию `-D` для удаления сертификата:

```
$ certutil -d sql:$HOME/.pki/nssdb -D -n *имя_сертификата*

```

## Добавление сертификатов WebMoney

**Обратите внимание:** В последних версиях Chromium добавление сертификата в NSS можно также произвести в настройках `chrome://settings/certificates`.

Как известно, [Chromium](/index.php/Chromium_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Chromium (Русский)") не имеет собственного хранилища сертификатов, поэтому, для работы с WebMoney Keeper Light, необходимо добавить корневой и личный сертификаты в хранилище NSS.

Проверяем, что хранилище сертификатов работает и доступ к нему есть:

```
$ certutil -d sql:$HOME/.pki/nssdb -L

```

Устанавливаем корневой сертификат (вместо *WebMoneyTransferRootCA.crt* введите путь к файлу корневого сертификата):

```
$ certutil -d sql:$HOME/.pki/nssdb -A -t "C,," -n "WebmoneyCA" -i *WebMoneyTransferRootCA.crt*

```

Устанавливаем личный сертификат (вместо *PersonalCert.p12* введите путь к файлу личного сертификата):

```
$ pk12util -d sql:$HOME/.pki/nssdb -i *PersonalCert.p12*

```

Если всё прошло успешно, после перезапуска Chromium вы сможете авторизоваться в WebMoney Keeper Light используя личный сертификат.

## Смотрите также

*   [Network Security Services](http://www.mozilla.org/projects/security/pki/nss/) на mozilla.org.
*   [Using the Certificate Database Tool](http://www.mozilla.org/projects/security/pki/nss/tools/certutil.html#1034193) на mozilla.org.
*   [Certificate management](http://code.google.com/p/chromium/wiki/LinuxCertManagement) в Chromium Wiki.
*   [Managing Certificate Trust flags in NSS Database](http://blogs.oracle.com/meena/entry/notes_about_trust_flags) в блоге Meena.