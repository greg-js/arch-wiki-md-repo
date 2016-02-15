## Contents

*   [1 Введение](#.D0.92.D0.B2.D0.B5.D0.B4.D0.B5.D0.BD.D0.B8.D0.B5)
*   [2 Установка](#.D0.A3.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B0)
*   [3 Настройка](#.D0.9D.D0.B0.D1.81.D1.82.D1.80.D0.BE.D0.B9.D0.BA.D0.B0)
    *   [3.1 Включение ACL](#.D0.92.D0.BA.D0.BB.D1.8E.D1.87.D0.B5.D0.BD.D0.B8.D0.B5_ACL)
    *   [3.2 Установка прав ACL](#.D0.A3.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B0_.D0.BF.D1.80.D0.B0.D0.B2_ACL)
*   [4 Примеры](#.D0.9F.D1.80.D0.B8.D0.BC.D0.B5.D1.80.D1.8B)
    *   [4.1 Вывод команды ls](#.D0.92.D1.8B.D0.B2.D0.BE.D0.B4_.D0.BA.D0.BE.D0.BC.D0.B0.D0.BD.D0.B4.D1.8B_ls)
*   [5 Повышение безопасности веб-сервера](#.D0.9F.D0.BE.D0.B2.D1.8B.D1.88.D0.B5.D0.BD.D0.B8.D0.B5_.D0.B1.D0.B5.D0.B7.D0.BE.D0.BF.D0.B0.D1.81.D0.BD.D0.BE.D1.81.D1.82.D0.B8_.D0.B2.D0.B5.D0.B1-.D1.81.D0.B5.D1.80.D0.B2.D0.B5.D1.80.D0.B0)
*   [6 Дополнительные ресурсы](#.D0.94.D0.BE.D0.BF.D0.BE.D0.BB.D0.BD.D0.B8.D1.82.D0.B5.D0.BB.D1.8C.D0.BD.D1.8B.D0.B5_.D1.80.D0.B5.D1.81.D1.83.D1.80.D1.81.D1.8B)

## Введение

**A**ccess **C**ontrol **L**ist предоставляет расширенный и более гибкий механизм распределения прав файловых систем. Он предназначен для расширения прав доступа к файлам `UNIX`. ACL позволяет устанавливать разрешения любым пользователям или группам для различных файловых ресурсов.

## Установка

ACL доступно из /core хранилища пакетов:

```
# pacman -S acl

```

## Настройка

### Включение ACL

Для включения ACL - отредактируйте файл **/etc/fstab** и добавьте атрибут **acl** к опциям раздела, где полагается использование ACL:

```
# 
# /etc/fstab: static file system information
#
# <file system>        <dir>         <type>    <options>          <dump> <pass>
none                   /dev/pts      devpts    defaults            0      0
none                   /dev/shm      tmpfs     defaults            0      0

UUID=5de01fca-7c63-49b0-9b2b-8b1790f8428e swap swap defaults 0 0

UUID=8e5259dd-26fc-411a-88e2-f38d4dc36724 /home reiserfs defaults,acl 0 1

UUID=c18f753e-0039-49bd-930f-587d48b7e083 / reiserfs defaults 0 1

```

Сохраните файл. Переподключите раздел:

```
# mount -o remount /home

```

### Установка прав ACL

Для изменения ACL используйте команду **setfacl**. Для добавления прав используйте **setfacl -m**.

Добавление прав какому-нибудь пользователю:

```
# setfacl -m "u:username:permissions"

```

или

```
# setfacl -m "u:uid:permissions"

```

Для добавления прав какой-нибудь группе:

```
# setfacl -m "g:groupname:permissions"

```

или

```
# setfacl -m "g:gid:permissions"

```

Удаление всех расширений ACL:

```
# setfacl -b

```

Удаление всех записей:

```
# setfacl -x "entry"

```

Проверка установленных разрешений:

```
# getfacl filename

```

## Примеры

Установить все разрешения на файл "abc" для пользователя johny:

```
# setfacl -m "u:johny:rwx" abc

```

Проверить разрешения:

```
# getfacl abc

```

```
# file: abc
# owner: someone
# group: someone
user::rw-
user:johny:rwx
group::r--
mask::rwx
other::r--

```

Изменение разрешений для пользователя johny:

```
# setfacl -m "u:johny:r-x" abc

```

Проверка разрешений:

```
# getfacl abc

```

```
# file: abc
# owner: someone
# group: someone
user::rw-
user:johny:r-x
group::r--
mask::r-x
other::r--

```

Удаление всех записей расширения ACL:

```
# setfacl -b abc

```

Проверка разрешений:

```
# getfacl abc

```

```
# file: abc
# owner: someone
# group: someone
user::rw-
group::r--
other::r--

```

### Вывод команды ls

При использовании команды **ls -l** можно заметить **+**(знак плюс) следующий за правами unix, предупреждающий об использовании расширений ACL для файла.

```
$ ls -l /dev/audio 
crw-rw----+ 1 root audio 14, 4 nov.   9 12:49 /dev/audio

$ getfacl /dev/audio
getfacl: Removing leading '/' from absolute path names
# file: dev/audio
# owner: root
# group: audio
user::rw-
user:solstice:rw-
group::rw-
mask::rw-
other::---

```

## Повышение безопасности веб-сервера

Для повышения безопасности веб-сервера добавьте расширенные права на домашнюю директорию и/или директорию сайта только для пользователя **http**.

Перейдите в домашнюю директорию:

```
# cd /home

```

Добавьте разрешение **+x** для пользователя http с помощью ACL:

```
# setfacl -m "u:http:--x" homeusername/

```

Теперь удалите права rx разрешающие использование директории другим пользователям:

```
# chmod o-rx homeusername/

```

Проверьте изменения:

```
# file: username/
# owner: username
# group: users
user::rwx
user:http:--x
group::r-x
mask::r-x
other::---

```

Как мы можем видеть, другие пользователи не имеют доступа, но для пользователя http установлен атрибут "x", что разрешает ему просмотр пользовательской директории и дает доступ к веб-страницам пользователя. Это справедливо, если веб-сервер работает от имени пользователя http. По умолчанию пользователь http не наделён такими полномочиями.

## Дополнительные ресурсы

*   Страница руководства - **man getfacl**
*   Страница руководства - **man setfacl**