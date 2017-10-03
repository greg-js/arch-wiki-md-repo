## Contents

*   [1 Введение](#.D0.92.D0.B2.D0.B5.D0.B4.D0.B5.D0.BD.D0.B8.D0.B5)
*   [2 Установка](#.D0.A3.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B0)
*   [3 Настройка](#.D0.9D.D0.B0.D1.81.D1.82.D1.80.D0.BE.D0.B9.D0.BA.D0.B0)
    *   [3.1 Включение ACL](#.D0.92.D0.BA.D0.BB.D1.8E.D1.87.D0.B5.D0.BD.D0.B8.D0.B5_ACL)
    *   [3.2 Изменение прав ACL](#.D0.98.D0.B7.D0.BC.D0.B5.D0.BD.D0.B5.D0.BD.D0.B8.D0.B5_.D0.BF.D1.80.D0.B0.D0.B2_ACL)
    *   [3.3 Просмотр прав ACL](#.D0.9F.D1.80.D0.BE.D1.81.D0.BC.D0.BE.D1.82.D1.80_.D0.BF.D1.80.D0.B0.D0.B2_ACL)
*   [4 Примеры](#.D0.9F.D1.80.D0.B8.D0.BC.D0.B5.D1.80.D1.8B)
    *   [4.1 Вывод команды ls](#.D0.92.D1.8B.D0.B2.D0.BE.D0.B4_.D0.BA.D0.BE.D0.BC.D0.B0.D0.BD.D0.B4.D1.8B_ls)
    *   [4.2 Поиск файлов с правами ACL](#.D0.9F.D0.BE.D0.B8.D1.81.D0.BA_.D1.84.D0.B0.D0.B9.D0.BB.D0.BE.D0.B2_.D1.81_.D0.BF.D1.80.D0.B0.D0.B2.D0.B0.D0.BC.D0.B8_ACL)
    *   [4.3 Предоставление разрешений на выполнение личных файлов веб-сервером](#.D0.9F.D1.80.D0.B5.D0.B4.D0.BE.D1.81.D1.82.D0.B0.D0.B2.D0.BB.D0.B5.D0.BD.D0.B8.D0.B5_.D1.80.D0.B0.D0.B7.D1.80.D0.B5.D1.88.D0.B5.D0.BD.D0.B8.D0.B9_.D0.BD.D0.B0_.D0.B2.D1.8B.D0.BF.D0.BE.D0.BB.D0.BD.D0.B5.D0.BD.D0.B8.D0.B5_.D0.BB.D0.B8.D1.87.D0.BD.D1.8B.D1.85_.D1.84.D0.B0.D0.B9.D0.BB.D0.BE.D0.B2_.D0.B2.D0.B5.D0.B1-.D1.81.D0.B5.D1.80.D0.B2.D0.B5.D1.80.D0.BE.D0.BC)
*   [5 Дополнительные ресурсы](#.D0.94.D0.BE.D0.BF.D0.BE.D0.BB.D0.BD.D0.B8.D1.82.D0.B5.D0.BB.D1.8C.D0.BD.D1.8B.D0.B5_.D1.80.D0.B5.D1.81.D1.83.D1.80.D1.81.D1.8B)

## Введение

**ACL** (**A**ccess **C**ontrol **L**ist - Список Контроля Доступа) предоставляет расширенный и более гибкий механизм распределения прав файловых систем. Он предназначен для расширения прав доступа к файлам `UNIX`. ACL позволяет устанавливать разрешения любым пользователям или группам для различных файловых ресурсов.

## Установка

Пакет [acl](https://www.archlinux.org/packages/?name=acl) уже установлен так как является зависимостью для [systemd](/index.php/Systemd "Systemd").

## Настройка

### Включение ACL

Чтобы включить ACL, файловая система должна быть смонтирована с опцией `acl`. Используйте [fstab](/index.php/Fstab "Fstab") для постоянного монтирование с данной опцией.

Вероятно параметр `acl` уже активен как параметр установки файловой системы по умолчанию. Это справедливо для [Btrfs](/index.php/Btrfs "Btrfs") и ext{2,3,4} файловых систем. Команда для проверки разделов ext* на предмет включенного параметра `acl` :

 `# tune2fs -l /dev/sd*XY* | grep "Default mount options:"` 
```
Default mount options:    user_xattr acl

```

Также убедитесь, что опция монтирования по умолчанию не переопределена, об этом будет свидетельствовать присутствие параметра `noacl` в выводе `/proc/mounts` для соответствующего раздела.

Вы также можете установить параметры монтирования по умолчанию для файловой системы, используя команду `tune2fs -o *option* *partition*`, например:

```
# tune2fs -o acl /dev/sd*XY*

```

Это очень удобно, так как избавляет от необходимости править `/etc/fstab`, а также установки опции `acl` при монтировании внешних дисков.

**Примечание:**

*   `acl` указывается как опция установки по умолчанию при создании файловой системы ext{2,3,4}. Это настроено в файле `/etc/mke2fs.conf`.
*   Параметры монтирования по умолчанию не указаны в `/proc/mounts`.
*   При архивации с помощью `tar` используйте ключ **--acls** чтобы включить поддержку атрибутов `acl`.

### Изменение прав ACL

Для изменения прав ACL используйте команду *setfacl*.

Добавить разрешения для пользователя (`*user*` здесь имя пользователя или его ID):

```
# setfacl -m "u:*user:permissions*" <file/dir>

```

Добавить разрешения для группы (`*group*` здесь имя группы или её ID):

```
# setfacl -m "g:*group:permissions*" <file/dir>

```

Все файлы и каталоги при создании будут наследовать записи ACL родительского каталога:

```
# setfacl -dm "*entry*" <dir>

```

Удалить определённую ACL запись:

```
# setfacl -x "*entry*" <file/dir>

```

Удалить все ACL записи:

```
# setfacl -b <file/dir>

```

### Просмотр прав ACL

Посмотреть права ACL:

```
# getfacl <file/dir>

```

## Примеры

Установить все разрешения на файл "abc" для пользователя johny:

```
# setfacl -m "u:johny:rwx" abc

```

Проверить разрешения:

 `# getfacl abc` 
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

 `# getfacl abc` 
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

 `# getfacl abc` 
```
# file: abc
# owner: someone
# group: someone
user::rw-
group::r--
other::r--

```

### Вывод команды ls

Знак `**+**`(плюс) в выводе команды `ls -l` который следует за правами Unix, указывает на использование ACL.

 `$ ls -l /dev/audio` 
```
crw-rw----+ 1 root audio 14, 4 nov.   9 12:49 /dev/audio

```
 `$ getfacl /dev/audio` 
```
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

### Поиск файлов с правами ACL

```
getfacl -R -s -p <dir> | sed -n 's/^# file: //p'

```

данная команда ищет в указанном каталоге и его подкаталогах все файлы и директории которые имеют права ACL

### Предоставление разрешений на выполнение личных файлов веб-сервером

Следующий метод описывает то, как процесс веб-сервера может получить доступ к файлам находящихся в домашней папке пользователя, без ущерба для безопасности.

Будем считать что веб-сервер работает от пользователя `webserver` и предоставляет доступ к домашнему каталогу `/home/geoffrey` пользователя `geoffrey`.

Для начала разрешим `webserver` доступ к домашней папке пользователя `geoffrey` :

```
# setfacl -m "u:webserver:--x" /home/geoffrey

```

**Примечание:** Права доступа к *каталогу* дают возможность процессу читать содержимое данного каталога.

Поскольку `webserver` теперь имеет доступ к файлам в `/home/geoffrey` то безопаснее будет удалить доступ `other` пользователей:

```
# chmod o-rx /home/geoffrey

```

Проверим изменения с помощью `getfacl`:

```
$ getfacl /home/geoffrey
getfacl: Removing leading '/' from absolute path names
# file: home/geoffrey
# owner: geoffrey
# group: geoffrey
user::rwx
user:webserver:--x
group::r-x
mask::r-x
other::---

```

Как видно из вывода, `other` больше не имеют никаких разрешений, но `webserver` все еще может обращаться к файлам.

## Дополнительные ресурсы

*   [getfacl(1)](http://jlk.fjfi.cvut.cz/arch/manpages/man/getfacl.1)
*   [setfacl(1)](http://jlk.fjfi.cvut.cz/arch/manpages/man/setfacl.1)