# Wvdial (Русский)

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

[![Tango-preferences-desktop-locale.png](/images/d/dc/Tango-preferences-desktop-locale.png)](/index.php/File:Tango-preferences-desktop-locale.png)

[![Tango-preferences-desktop-locale.png](/images/d/dc/Tango-preferences-desktop-locale.png)](/index.php/File:Tango-preferences-desktop-locale.png)

**Эта страница нуждается в сопроводителе**

Статья не гарантирует актуальность информации. Помогите русскоязычному сообществу поддержкой подобных страниц. См. [Команда переводчиков ArchWiki](/index.php/%D0%9A%D0%BE%D0%BC%D0%B0%D0%BD%D0%B4%D0%B0_%D0%BF%D0%B5%D1%80%D0%B5%D0%B2%D0%BE%D0%B4%D1%87%D0%B8%D0%BA%D0%BE%D0%B2_ArchWiki "Команда переводчиков ArchWiki")

Существует несколько различных способов дать пользователям возможность использовать wvdial для создания ppp-соединение. Этот документ описывает три различных способа, отличающиеся друг от друга сложностью использования и степенями безопасности. Подразумевается, что вы должным образом сконфигурировали wvdial. Все настройки, представленные ниже, должны быть сделаны под root’ом.

## Используя suid

Это, несомненно, самый простой способ настроить, но и сильная угроза системе безопасности, поскольку любой пользователь может запустить wvdial в качестве привилегированного пользователя. По возможности, используйте одно из других решений. Так как обычные пользователи не могут по умолчанию использовать wvdial для дозвона, то необходимо поменять права:

```
chmod u+s /usr/bin/wvdial

```

Вы должны увидеть следующие разрешения:

```
ls -l /usr/bin/wvdial
-rwsr-xr-x 1 root root 114368 2005-12-07 19:21 /usr/bin/wvdial

```

## Используя группу dialout

Другой, немного более безопасный способ - создать группу dialout (вы можете, впрочем, назвать ее как вам угодно) и дать членам этой группы права на запуск wvdial как root. Во-первых, необходимо создать группу и добавить туда пользователей:

```
groupadd dialout
gpasswd -a myuser dialout

```

Затем установить группу и дать разрешение на использование wvdial:

```
chgrp dialout /usr/bin/wvdial
chmod u+s,o= /usr/bin/wvdial

```

Теперь можно посмотреть права:

```
ls -l /usr/bin/wvdial
-rwsr-x— 1 root dialout 114368 2005-12-07 19:21 /usr/bin/wvdial

```

## Используя sudo

sudo предлагает, вероятно, самый безопасный способ позволить пользователям устанавливать dial-up соединения с помощью wvdial. sudo может использоваться для того, чтобы дать права для как пользователю, так и определённой группе пользователей. Другая выгода от использования sudo состоит в том, что достаточно однажды установить права, и при установке нового пакета wvdial не будет необходимости заново давать разрешения, в отличие от двух предыдущих способов. Здесь мы не будет вдаваться в подробности использования sudo. За дополнительной информацией обращайтесь к man-страницам (sudo, sudoers, visudo). Используйте visudo для редактирования файла /etc/sudoers:

```
visudo

```

Чтобы предоставить разрешение конкретному пользователю использовать wvdial с правами суперпользователя, необходимо добавить следующую строку (конечно, заменив имя пользователя на нужное):

```
myuser localhost = /usr/bin/wvdial

```

Чтобы предоставить права всем членам группы (dialout):

```
%dialout localhost = /usr/bin/wvdial

```

Retrieved from "[https://wiki.archlinux.org/index.php?title=Wvdial_(Русский)&oldid=415147](https://wiki.archlinux.org/index.php?title=Wvdial_(Русский)&oldid=415147)"

[Categories](/index.php/Special:Categories "Special:Categories"):

*   [Русский](/index.php/Category:%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9 "Category:Русский")
*   [Networking (Русский)](/index.php/Category:Networking_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Category:Networking (Русский)")