Ссылки по теме

*   [Mirroring](/index.php/Mirroring "Mirroring")
*   [pacman (Русский)](/index.php/Pacman_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Pacman (Русский)")
*   [Reflector (Русский)](/index.php/Reflector_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Reflector (Русский)")

На этой странице представлено руководство по выбору и настройке зеркал, а также список зеркал, доступных в настоящее время.

## Contents

*   [1 Включение зеркал](#.D0.92.D0.BA.D0.BB.D1.8E.D1.87.D0.B5.D0.BD.D0.B8.D0.B5_.D0.B7.D0.B5.D1.80.D0.BA.D0.B0.D0.BB)
    *   [1.1 Обновление базы данных pacman после изменения зеркал](#.D0.9E.D0.B1.D0.BD.D0.BE.D0.B2.D0.BB.D0.B5.D0.BD.D0.B8.D0.B5_.D0.B1.D0.B0.D0.B7.D1.8B_.D0.B4.D0.B0.D0.BD.D0.BD.D1.8B.D1.85_pacman_.D0.BF.D0.BE.D1.81.D0.BB.D0.B5_.D0.B8.D0.B7.D0.BC.D0.B5.D0.BD.D0.B5.D0.BD.D0.B8.D1.8F_.D0.B7.D0.B5.D1.80.D0.BA.D0.B0.D0.BB)
*   [2 Статус зеркала](#.D0.A1.D1.82.D0.B0.D1.82.D1.83.D1.81_.D0.B7.D0.B5.D1.80.D0.BA.D0.B0.D0.BB.D0.B0)
*   [3 Приоритет зеркал](#.D0.9F.D1.80.D0.B8.D0.BE.D1.80.D0.B8.D1.82.D0.B5.D1.82_.D0.B7.D0.B5.D1.80.D0.BA.D0.B0.D0.BB)
    *   [3.1 Список по скорости](#.D0.A1.D0.BF.D0.B8.D1.81.D0.BE.D0.BA_.D0.BF.D0.BE_.D1.81.D0.BA.D0.BE.D1.80.D0.BE.D1.81.D1.82.D0.B8)
    *   [3.2 Список одновременно по скорости и статусу](#.D0.A1.D0.BF.D0.B8.D1.81.D0.BE.D0.BA_.D0.BE.D0.B4.D0.BD.D0.BE.D0.B2.D1.80.D0.B5.D0.BC.D0.B5.D0.BD.D0.BD.D0.BE_.D0.BF.D0.BE_.D1.81.D0.BA.D0.BE.D1.80.D0.BE.D1.81.D1.82.D0.B8_.D0.B8_.D1.81.D1.82.D0.B0.D1.82.D1.83.D1.81.D1.83)
    *   [3.3 Скрипт для получения списка зеркал из Pacman Mirrorlist Generator](#.D0.A1.D0.BA.D1.80.D0.B8.D0.BF.D1.82_.D0.B4.D0.BB.D1.8F_.D0.BF.D0.BE.D0.BB.D1.83.D1.87.D0.B5.D0.BD.D0.B8.D1.8F_.D1.81.D0.BF.D0.B8.D1.81.D0.BA.D0.B0_.D0.B7.D0.B5.D1.80.D0.BA.D0.B0.D0.BB_.D0.B8.D0.B7_Pacman_Mirrorlist_Generator)
    *   [3.4 Используя Reflector](#.D0.98.D1.81.D0.BF.D0.BE.D0.BB.D1.8C.D0.B7.D1.83.D1.8F_Reflector)
    *   [3.5 Выбор местного зеркала](#.D0.92.D1.8B.D0.B1.D0.BE.D1.80_.D0.BC.D0.B5.D1.81.D1.82.D0.BD.D0.BE.D0.B3.D0.BE_.D0.B7.D0.B5.D1.80.D0.BA.D0.B0.D0.BB.D0.B0)
    *   [3.6 Список зеркал только для конкретной страны](#.D0.A1.D0.BF.D0.B8.D1.81.D0.BE.D0.BA_.D0.B7.D0.B5.D1.80.D0.BA.D0.B0.D0.BB_.D1.82.D0.BE.D0.BB.D1.8C.D0.BA.D0.BE_.D0.B4.D0.BB.D1.8F_.D0.BA.D0.BE.D0.BD.D0.BA.D1.80.D0.B5.D1.82.D0.BD.D0.BE.D0.B9_.D1.81.D1.82.D1.80.D0.B0.D0.BD.D1.8B)
*   [4 Официальные зеркала](#.D0.9E.D1.84.D0.B8.D1.86.D0.B8.D0.B0.D0.BB.D1.8C.D0.BD.D1.8B.D0.B5_.D0.B7.D0.B5.D1.80.D0.BA.D0.B0.D0.BB.D0.B0)
    *   [4.1 Зеркала IPv6](#.D0.97.D0.B5.D1.80.D0.BA.D0.B0.D0.BB.D0.B0_IPv6)
*   [5 Неофициальные зеркала](#.D0.9D.D0.B5.D0.BE.D1.84.D0.B8.D1.86.D0.B8.D0.B0.D0.BB.D1.8C.D0.BD.D1.8B.D0.B5_.D0.B7.D0.B5.D1.80.D0.BA.D0.B0.D0.BB.D0.B0)
    *   [5.1 Старые образы](#.D0.A1.D1.82.D0.B0.D1.80.D1.8B.D0.B5_.D0.BE.D0.B1.D1.80.D0.B0.D0.B7.D1.8B)
    *   [5.2 Сеть TOR](#.D0.A1.D0.B5.D1.82.D1.8C_TOR)
    *   [5.3 Австрия](#.D0.90.D0.B2.D1.81.D1.82.D1.80.D0.B8.D1.8F)
    *   [5.4 Болгария](#.D0.91.D0.BE.D0.BB.D0.B3.D0.B0.D1.80.D0.B8.D1.8F)
    *   [5.5 Китай](#.D0.9A.D0.B8.D1.82.D0.B0.D0.B9)
    *   [5.6 Франция](#.D0.A4.D1.80.D0.B0.D0.BD.D1.86.D0.B8.D1.8F)
    *   [5.7 Германия](#.D0.93.D0.B5.D1.80.D0.BC.D0.B0.D0.BD.D0.B8.D1.8F)
    *   [5.8 Гонконг](#.D0.93.D0.BE.D0.BD.D0.BA.D0.BE.D0.BD.D0.B3)
    *   [5.9 Индия](#.D0.98.D0.BD.D0.B4.D0.B8.D1.8F)
    *   [5.10 Индонезия](#.D0.98.D0.BD.D0.B4.D0.BE.D0.BD.D0.B5.D0.B7.D0.B8.D1.8F)
    *   [5.11 Иран](#.D0.98.D1.80.D0.B0.D0.BD)
    *   [5.12 Италия](#.D0.98.D1.82.D0.B0.D0.BB.D0.B8.D1.8F)
    *   [5.13 Япония](#.D0.AF.D0.BF.D0.BE.D0.BD.D0.B8.D1.8F)
    *   [5.14 Казахстан](#.D0.9A.D0.B0.D0.B7.D0.B0.D1.85.D1.81.D1.82.D0.B0.D0.BD)
    *   [5.15 Малайзия](#.D0.9C.D0.B0.D0.BB.D0.B0.D0.B9.D0.B7.D0.B8.D1.8F)
    *   [5.16 Новая Зеландия](#.D0.9D.D0.BE.D0.B2.D0.B0.D1.8F_.D0.97.D0.B5.D0.BB.D0.B0.D0.BD.D0.B4.D0.B8.D1.8F)
    *   [5.17 Польша](#.D0.9F.D0.BE.D0.BB.D1.8C.D1.88.D0.B0)
    *   [5.18 Россия](#.D0.A0.D0.BE.D1.81.D1.81.D0.B8.D1.8F)
    *   [5.19 Сингапур](#.D0.A1.D0.B8.D0.BD.D0.B3.D0.B0.D0.BF.D1.83.D1.80)
    *   [5.20 Южно-Африканская Республика](#.D0.AE.D0.B6.D0.BD.D0.BE-.D0.90.D1.84.D1.80.D0.B8.D0.BA.D0.B0.D0.BD.D1.81.D0.BA.D0.B0.D1.8F_.D0.A0.D0.B5.D1.81.D0.BF.D1.83.D0.B1.D0.BB.D0.B8.D0.BA.D0.B0)
    *   [5.21 Южная Корея](#.D0.AE.D0.B6.D0.BD.D0.B0.D1.8F_.D0.9A.D0.BE.D1.80.D0.B5.D1.8F)
    *   [5.22 Соединенные Штаты Америки](#.D0.A1.D0.BE.D0.B5.D0.B4.D0.B8.D0.BD.D0.B5.D0.BD.D0.BD.D1.8B.D0.B5_.D0.A8.D1.82.D0.B0.D1.82.D1.8B_.D0.90.D0.BC.D0.B5.D1.80.D0.B8.D0.BA.D0.B8)
    *   [5.23 Вьетнам](#.D0.92.D1.8C.D0.B5.D1.82.D0.BD.D0.B0.D0.BC)
*   [6 Смотрите также](#.D0.A1.D0.BC.D0.BE.D1.82.D1.80.D0.B8.D1.82.D0.B5_.D1.82.D0.B0.D0.BA.D0.B6.D0.B5)

## Включение зеркал

Чтобы включить зеркала, откройте файл `/etc/pacman.d/mirrorlist` и найдите подходящие зеркала, основываясь на вашем географическом местоположении. Раскомментируйте наиболее близкие к вам зеркала.

**Примечание:** На ftp.archlinux.org установлено ограничение пропускной способности в 50 КБайт/с [[1]](https://www.archlinux.org/news/throttling-ftparchlinuxorg-rsyncarchlinuxorg/).

Пример:

```
# Any
# Server = ftp://mirrors.kernel.org/archlinux/$repo/os/$arch
**Server = http://mirrors.kernel.org/archlinux/$repo/os/$arch**

```

Разделы [#Статус зеркала](#.D0.A1.D1.82.D0.B0.D1.82.D1.83.D1.81_.D0.B7.D0.B5.D1.80.D0.BA.D0.B0.D0.BB.D0.B0) и [#Список по скорости](#.D0.A1.D0.BF.D0.B8.D1.81.D0.BE.D0.BA_.D0.BF.D0.BE_.D1.81.D0.BA.D0.BE.D1.80.D0.BE.D1.81.D1.82.D0.B8) также помогут вам выбрать зеркало.

**Совет:** Раскомментируйте 5 наиболее подходящих вам зеркал и поместите их наверху файла mirrorlist. Таким образом, будет легко потом устанавливать приоритет, меняя их местами, если у первого зеркала в списке начнутся какие-нибудь проблемы. Это также упрощает слияние файлов mirrorlist при обновлениях списка зеркал.

Также вы можете указать зеркала в `/etc/pacman.conf`. Для репозитория *core* стандартная установка выглядит следующим образом:

```
[core]
Include = /etc/pacman.d/mirrorlist

```

Например, вы хотите использовать зеркало "HostEurope" для *core*. Тогда добавьте его перед `Include`:

```
[core]
**Server = ftp://ftp.hosteurope.de/mirror/ftp.archlinux.org/core/os/$arch**
Include = /etc/pacman.d/mirrorlist

```

Теперь pacman будет первым делом пытаться соединиться с этим зеркалом. Аналогично следует сделать и для других репозиториев: *testing*, *extra*, и *community*.

**Примечание:** Если вы указываете зеркала напрямую в `pacman.conf`, вам следует использовать одно и то же зеркало для всех репозиториев. В противном случае вы можете столкнуться с тем, что будут поставлены несовместимые версии пакетов из разных зеркал (так как зеркала синхронизируются не мгновенно).

### Обновление базы данных pacman после изменения зеркал

После внесения изменений в `/etc/pacman.d/mirrorlist` (неважно, вручную или с *rankmirrors*) выполните синхронизацию базы данных пакетов pacman:

```
# pacman -Syyu

```

**Совет:** Указание сразу двух опций `--refresh` или `-y` заставляет pacman обновлять списки пакетов, даже если pacman уже считает их обновленными. Запуск `pacman -Syyu` *при любой смене зеркала* является хорошей практикой и позволяет избежать возможных проблем.

## Статус зеркала

Проверить текущий статус любого зеркала вы можете на странице [https://www.archlinux.org/mirrors/status/](https://www.archlinux.org/mirrors/status/).

Вы можете использовать [Pacman Mirrorlist Generator](https://www.archlinux.org/mirrorlist/) для того, чтобы сгенерировать список подходящих зеркал. Для автоматизации этого процесса существует [#Скрипт для получения списка зеркал из Pacman Mirrorlist Generator](#.D0.A1.D0.BA.D1.80.D0.B8.D0.BF.D1.82_.D0.B4.D0.BB.D1.8F_.D0.BF.D0.BE.D0.BB.D1.83.D1.87.D0.B5.D0.BD.D0.B8.D1.8F_.D1.81.D0.BF.D0.B8.D1.81.D0.BA.D0.B0_.D0.B7.D0.B5.D1.80.D0.BA.D0.B0.D0.BB_.D0.B8.D0.B7_Pacman_Mirrorlist_Generator). Кроме того, вы можете установить [Reflector](/index.php/Reflector_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Reflector (Русский)") — утилиту, которая генерирует список зеркал на основе данных со страницы [Mirror Status](https://www.archlinux.org/mirrors/status/).

## Приоритет зеркал

При загрузке пакетов pacman использует зеркала в том порядке, в котором они перечислены в `/etc/pacman.d/mirrorlist`. Если вы не используете [Reflector](/index.php/Reflector_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Reflector (Русский)"), который может упорядочить зеркала и по степени обновления, и по скорости отдачи, вам поможет небольшая инструкция в этом разделе по ручной сортировке зеркал.

**Примечание:** Это не относится к [powerpill-light](/index.php/Improve_pacman_performance#Using_powerpill-light "Improve pacman performance"), который соединяется с несколькими серверами сразу для ускорения скорости загрузки. При этом скорость каждого соединения становится не так важна, и в powerpill-light можно настроить ограничение скорости на каждое соединение.

### Список по скорости

Самое быстрое зеркало можно определить при помощи скрипта `/usr/bin/rankmirrors`.

Сохраните текущий файл `/etc/pacman.d/mirrorlist`:

```
# cp /etc/pacman.d/mirrorlist /etc/pacman.d/mirrorlist.backup

```

Отредактируйте `/etc/pacman.d/mirrorlist.backup`, раскомментировав зеркала для проверки скриптом `rankmirrors`.

Если вы хотите попробовать все зеркала, используйте *sed* для раскомментирования всех зеркал:

```
# sed -i 's/^#Server/Server/' /etc/pacman.d/mirrorlist.backup

```

Теперь запустите скрипт. Опция `-n 6` ограничивает вывод шестью наиболее быстрыми зеркалами:

```
# rankmirrors -n 6 /etc/pacman.d/mirrorlist.backup > /etc/pacman.d/mirrorlist

```

Список всех доступных опций вы можете просмотреть, набрав `rankmirrors -h`.

### Список одновременно по скорости и статусу

Не самая лучшая идея просто использовать наиболее быстрые зеркала, так как они могут при этом обновляться с большим опозданием и содержать старые пакеты. Предпочтительнее сначала создать [#Список по скорости](#.D0.A1.D0.BF.D0.B8.D1.81.D0.BE.D0.BA_.D0.BF.D0.BE_.D1.81.D0.BA.D0.BE.D1.80.D0.BE.D1.81.D1.82.D0.B8), а затем отсортировать этот список, проверяя [#Статус зеркала](#.D0.A1.D1.82.D0.B0.D1.82.D1.83.D1.81_.D0.B7.D0.B5.D1.80.D0.BA.D0.B0.D0.BB.D0.B0).

Просто просмотрите статус каждого из зеркал, как это написано в разделе [#Статус зеркала](#.D0.A1.D1.82.D0.B0.D1.82.D1.83.D1.81_.D0.B7.D0.B5.D1.80.D0.BA.D0.B0.D0.BB.D0.B0), и вручную расположите их в порядке от наиболее к наименее обновленному.

Сохраните полученный список в `/etc/pacman.d/mirrorlist`.

### Скрипт для получения списка зеркал из Pacman Mirrorlist Generator

[Pacman Mirrorlist Generator](https://www.archlinux.org/mirrorlist/) располагает зеркала на основе географического расположения, доступности и уровне. Вы можете использовать удобный скрипт *armrr* либо из пакета ([armrr-git](https://aur.archlinux.org/packages/armrr-git/), либо загрузив его напрямую командой `curl -O [https://raw.githubusercontent.com/Gen2ly/armrr/master/armrr](https://raw.githubusercontent.com/Gen2ly/armrr/master/armrr)`), который позволяет на основе данных этого ресурса сгенерировать новый файл `mirrorlist`, создав резервную копию старого. Запустите скрипт без аргументов и введите код страны. Вы можете просмотреть список опций командной строки, набрав `armrr -h`.

### Используя Reflector

Вы можете использовать [Reflector](/index.php/Reflector_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Reflector (Русский)") для того, чтобы получить свежий список зеркал со страницы [Mirror Status](https://www.archlinux.org/mirrors/status/), отсеять из них устаревшие, отсортировать по скорости и сгенерировать новый файл `/etc/pacman.d/mirrorlist`.

### Выбор местного зеркала

Простым способом настроить зеркала является просто найти местное зеркало в mirrorlist и поместить его на самый верх. Таким образом, pacman будет предпочитать именно это зеркало.

Как вариант, вы можете добавить это зеркало перед строкой, где выполняется запуск файла mirrorlist, то есть, где сказано "add your preferred servers here". Безопаснее использовать один и тот же сервер для каждого из репозиториев.

### Список зеркал только для конкретной страны

Может быть также полезно получать список зеркал только для какой-то конкретной страны вместо того, чтобы выполнять замер скорости загрузки для каждого.

```
Cnt="Russia";
awk -v GG=$Cnt '{if(match($0,GG) != "0")AA="1";if(AA == "1"){if( length($0) != "0"  )print $3 ;else AA="0"} }' \
/etc/pacman.d/mirrorlist.pacnew | grep ':' 
```

## Официальные зеркала

Список официальных зеркал доступен с пакетом [pacman-mirrorlist](https://www.archlinux.org/packages/?name=pacman-mirrorlist). Наиболее свежий список зеркал доступен на странице [Pacman Mirror List Generator](https://www.archlinux.org/mirrorlist/).

Если случилось так, что у вас нет настроенных зеркал и `pacman-mirrorlist` не установлен, загрузите его напрямую:

```
# wget -O /etc/pacman.d/mirrorlist https://www.archlinux.org/mirrorlist/all/

```

Не забудьте раскомментировать подходящее зеркало, как было указано выше, и выполнить синхронизацию списка пакетов:

```
# pacman -Syyu pacman-mirrorlist

```

Если вы имеете собственное зеркало и хотите, чтобы оно было добавлено в список официальных, присылайте feature request и добавьте свое зеркало в список [#Неофициальные зеркала](#.D0.9D.D0.B5.D0.BE.D1.84.D0.B8.D1.86.D0.B8.D0.B0.D0.BB.D1.8C.D0.BD.D1.8B.D0.B5_.D0.B7.D0.B5.D1.80.D0.BA.D0.B0.D0.BB.D0.B0) в конце страницы.

Если вы получаете ошибку о том, что переменная `$arch` не определена, добавьте следующую строку в ваш `/etc/pacman.conf`:

```
Architecture = *x86_64*

```

**Примечание:** Здесь же вы можете использовать значения `auto` и `i686`.

### Зеркала IPv6

Используйте [Pacman Mirror List Generator](https://www.archlinux.org/mirrorlist/?country=all&protocol=http&ip_version=6) для запроса списка доступных зеркал IPv6.

## Неофициальные зеркала

Эти зеркала не перечислены в `/etc/pacman.d/mirrorlist`.

### Старые образы

*   [http://sourceforge.net/projects/archlinux/files/](http://sourceforge.net/projects/archlinux/files/) — *ISO files only; Does not have any releases since 2006\. Use it only if for getting older ISOs.*

### Сеть TOR

*   [http://cz2jqg7pj2hqanw7.onion/archlinux](http://cz2jqg7pj2hqanw7.onion/archlinux)
*   [ftp://mirror:mirror@cz2jqg7pj2hqanw7.onion/archlinux](ftp://mirror:mirror@cz2jqg7pj2hqanw7.onion/archlinux)
*   [http://rstpevyo7zx47bld.onion/archlinux](http://rstpevyo7zx47bld.onion/archlinux)

### Австрия

*   [http://gd.tuwien.ac.at/opsys/linux/archlinux/](http://gd.tuwien.ac.at/opsys/linux/archlinux/) — *Vienna University of Technology*
*   [ftp://gd.tuwien.ac.at/opsys/linux/archlinux/](ftp://gd.tuwien.ac.at/opsys/linux/archlinux/)

### Болгария

*   [http://mirror.telepoint.bg/archlinux/](http://mirror.telepoint.bg/archlinux/)
*   [ftp://mirror.telepoint.bg/archlinux/](ftp://mirror.telepoint.bg/archlinux/)

### Китай

**CHINA TELECOM**

*   [http://mirror.lupaworld.com/archlinux/](http://mirror.lupaworld.com/archlinux/)

**CHINA UNICOM**

*   [http://mirrors.sohu.com/archlinux/](http://mirrors.sohu.com/archlinux/)
*   [http://mirrors.yun-idc.com/archlinux/](http://mirrors.yun-idc.com/archlinux/)

**Cernet**

*   [http://mirrors.zju.edu.cn/archlinux/](http://mirrors.zju.edu.cn/archlinux/) — *Zhejian University*
*   [http://ftp.sjtu.edu.cn/archlinux/](http://ftp.sjtu.edu.cn/archlinux/) — *Shanghai Jiaotong University*
*   [ftp://ftp.sjtu.edu.cn/archlinux/](ftp://ftp.sjtu.edu.cn/archlinux/)
*   [http://mirrors.ustc.edu.cn/archlinux/](http://mirrors.ustc.edu.cn/archlinux/) — *University of Science and Technology of China*
*   [ftp://mirrors.ustc.edu.cn/archlinux/](ftp://mirrors.ustc.edu.cn/archlinux/)
*   [http://mirrors.tuna.tsinghua.edu.cn/archlinux/](http://mirrors.tuna.tsinghua.edu.cn/archlinux/) — *Tsinghua University*
*   [http://mirrors.4.tuna.tsinghua.edu.cn/archlinux/](http://mirrors.4.tuna.tsinghua.edu.cn/archlinux/) *(ipv4 only)*
*   [http://mirrors.6.tuna.tsinghua.edu.cn/archlinux/](http://mirrors.6.tuna.tsinghua.edu.cn/archlinux/) *(ipv6 only)*
*   [http://mirror.lzu.edu.cn/archlinux/](http://mirror.lzu.edu.cn/archlinux/) — *Lanzhou University*
*   [http://mirrors.huste.du.cn/archlinux](http://mirrors.huste.du.cn/archlinux) — *Huazhong University of Science and Technology*

### Франция

*   [http://delta.archlinux.fr/](http://delta.archlinux.fr/) — *With Delta package support. Needs xdelta3 package from extra to run.*
*   [http://mirror.soa1.org/archlinux](http://mirror.soa1.org/archlinux)
*   [ftp://mirror:mirror@mirror.soa1.org/archlinux](ftp://mirror:mirror@mirror.soa1.org/archlinux)

### Германия

*   [http://ftp.uni-erlangen.de/mirrors/archlinux/](http://ftp.uni-erlangen.de/mirrors/archlinux/)
*   [ftp://ftp.uni-erlangen.de/mirrors/archlinux/](ftp://ftp.uni-erlangen.de/mirrors/archlinux/)
*   [http://ftp.u-tx.net/archlinux/](http://ftp.u-tx.net/archlinux/)
*   [ftp://ftp.u-tx.net/archlinux/](ftp://ftp.u-tx.net/archlinux/)
*   [http://mirror.michael-eckert.net/archlinux/](http://mirror.michael-eckert.net/archlinux/)
*   [http://linux.rz.rub.de/archlinux/](http://linux.rz.rub.de/archlinux/)
*   [http://mirror.k42.ch/archlinux/](http://mirror.k42.ch/archlinux/)

### Гонконг

*   [http://hk.mirrors.linaxe.net/archlinux/](http://hk.mirrors.linaxe.net/archlinux/)

### Индия

*   [http://ftp.iitm.ac.in/archlinux/](http://ftp.iitm.ac.in/archlinux/)
*   [ftp://ftp.iitm.ac.in/archlinux/](ftp://ftp.iitm.ac.in/archlinux/)

### Индонезия

*   [http://mirror.kavalinux.com/archlinux/](http://mirror.kavalinux.com/archlinux/) — *only from Indonesia*
*   [http://kambing.ui.ac.id/archlinux/](http://kambing.ui.ac.id/archlinux/)
*   [http://repo.ukdw.ac.id/archlinux/](http://repo.ukdw.ac.id/archlinux/)

### Иран

*   [http://mirror.yazd.ac.ir/arch/](http://mirror.yazd.ac.ir/arch/)

### Италия

*   [http://mi.mirror.garr.it/mirrors/archlinux/](http://mi.mirror.garr.it/mirrors/archlinux/)

### Япония

*   [http://ftp.nara.wide.ad.jp/pub/Linux/archlinux/](http://ftp.nara.wide.ad.jp/pub/Linux/archlinux/) — *NAra Institute of Science and Technology*
*   [http://ftp.kddilabs.jp/Linux/packages/archlinux/](http://ftp.kddilabs.jp/Linux/packages/archlinux/)
*   [http://srv2.ftp.ne.jp/Linux/packages/archlinux/](http://srv2.ftp.ne.jp/Linux/packages/archlinux/)

### Казахстан

*   [http://archlinux.kz/](http://archlinux.kz/)
*   [http://mirror.neolabs.kz/archlinux/](http://mirror.neolabs.kz/archlinux/)
*   [http://mirror-kt.neolabs.kz/archlinux/](http://mirror-kt.neolabs.kz/archlinux/)

### Малайзия

*   [http://mirror.oscc.org.my/archlinux/](http://mirror.oscc.org.my/archlinux/)
*   [http://mirrors.inetutils.net/archlinux/](http://mirrors.inetutils.net/archlinux/) — *ISO and Core*

### Новая Зеландия

*   [http://mirror.ihug.co.nz/archlinux/](http://mirror.ihug.co.nz/archlinux/)
*   [http://mirror.ece.auckland.ac.nz/archlinux/](http://mirror.ece.auckland.ac.nz/archlinux/) *NZ only*

### Польша

*   [ftp://ftp.icm.edu.pl/pub/Linux/dist/archlinux/](ftp://ftp.icm.edu.pl/pub/Linux/dist/archlinux/) — ICM UW
*   [http://ftp.icm.edu.pl/pub/Linux/dist/archlinux/](http://ftp.icm.edu.pl/pub/Linux/dist/archlinux/) — ICM UW
*   rsync://ftp.icm.edu.pl/pub/Linux/dist/archlinux/ — ICM UW

### Россия

*   [http://hatred.homelinux.net/archlinux/](http://hatred.homelinux.net/archlinux/) — *Vladivostok, without iso, with <sub>[3SPY](http://hatred.homelinux.net/wiki/proekty:3spy:start)</sub> project repos and [**mingw32**](http://hatred.homelinux.net/archlinux/mingw32/os/i686) repo*
*   [http://mirrors.krasinfo.ru/archlinux/](http://mirrors.krasinfo.ru/archlinux/) — *Krasnoyarsk, Classica-Service Ltd*
*   [http://mirror.yandex.ru/archlinux/](http://mirror.yandex.ru/archlinux/) — *Moscow, [Yandex](http://www.yandex.ru/) LLC*

### Сингапур

*   [http://mirror.nus.edu.sg/archlinux/](http://mirror.nus.edu.sg/archlinux/)

### Южно-Африканская Республика

*   [http://ftp.leg.uct.ac.za/pub/linux/arch/](http://ftp.leg.uct.ac.za/pub/linux/arch/) — *University of Cape Town*
*   [ftp://ftp.leg.uct.ac.za/pub/linux/arch/](ftp://ftp.leg.uct.ac.za/pub/linux/arch/)
*   [http://mirror.ufs.ac.za/archlinux/](http://mirror.ufs.ac.za/archlinux/) — *University of the Free State*
*   [ftp://mirror.ufs.ac.za/os/linux/distros/archlinux/](ftp://mirror.ufs.ac.za/os/linux/distros/archlinux/)
*   [http://ftp.wa.co.za/pub/archlinux/](http://ftp.wa.co.za/pub/archlinux/) — *Web Africa Networks*
*   [ftp://ftp.wa.co.za/pub/archlinux/](ftp://ftp.wa.co.za/pub/archlinux/)
*   [http://archlinux.mirror.ac.za](http://archlinux.mirror.ac.za) — *TENET — Tertiary Education and Research Network of South Africa*
*   [ftp://archlinux.mirror.ac.za](ftp://archlinux.mirror.ac.za)

### Южная Корея

*   [http://mirror.star4u.org/archlinux/](http://mirror.star4u.org/archlinux/)
*   [http://ftp2.lecl.net/pub/archlinux](http://ftp2.lecl.net/pub/archlinux)

### Соединенные Штаты Америки

*   [http://archlinux.linuxfreedom.com](http://archlinux.linuxfreedom.com) — *Contains numerous ISO images but does not contain the ISO dated 2011.08.19*
*   [http://mirror.clarkson.edu/archlinux/](http://mirror.clarkson.edu/archlinux/)
*   [http://mirror.pointysoftware.net/archlinux/](http://mirror.pointysoftware.net/archlinux/)
*   [http://il.mirrors.linaxe.net/archlinux/](http://il.mirrors.linaxe.net/archlinux/) — *Server location — Chicago, IL*

### Вьетнам

**FPT TELECOM**

*   [http://mirror-fpt-telecom.fpt.net/archlinux/](http://mirror-fpt-telecom.fpt.net/archlinux/)

## Смотрите также

*   [MirUp](http://wiki.gotux.net/code/bash/mirup) — pacman mirrorlist downloader/checker