#### DeltUp - Экономия трафика

Экономим трафик — delta обновления в ArchLinux для платформ i686 и x86_64

1\. Устанавливаем [xdelta3](https://www.archlinux.org/packages/?name=xdelta3)

```
# pacman -S xdelta3 

```

2\. Добавляем в `/etc/pacman.d/mirrorlist`

 `/etc/pacman.d/mirrorlist` 
```
##
## Arch Linux repository mirrorlist
## Generated on 2011-03-24
##

## Dela Archlinux.fr
Server = [http://delta.archlinux.fr/$repo/os/$arch](http://delta.archlinux.fr/$repo/os/$arch)
.....
```

3\. Проверяем перед включением опции UseDelta каков размер скачиваемых файлов.

```
#  pacman -Syu

 ...
 Размер загружаемых файлов:   416,89 МБ
 Размер устанавливаемых файлов:   1933,56 МБ

 Приступить к установке? [Y/n]
```

Нажимаем N Обращаем внимание на размер: Размер загружаемых файлов: 416,89 МБ

4\. В `/etc/pacman.conf` убираем `#` перед параметром `UseDelta`

 `/etc/pacman.conf` 
```
.....
# Misc options (all disabled by default)
#UseSyslog
ShowSize
UseDelta
TotalDownload
.....
```

5\. Повторяем запрос на обновление системы с включенной опцией `UseDelta`:

```
# pacman -Syu

 ...
 Размер загружаемых файлов:   343,15 МБ
 Размер устанавливаемых файлов:   1933,56 МБ

 Приступить к установке? [Y/n]

```

Обращаем внимание на: Размер загружаемых файлов: 343,15 МБ

6\. Выводы

Таким образом мы экономим 416,89 МБ - 343,15 МБ ~ порядка 100 МБ, а также время.

7\. Недостатки данного метода:

К сожалению данный метод еще не очень сильно развит в дистрибутиве Archlinux в отличие к примеру от [OpenSuSE](http://www.opensuse.org) или [Gentoo](http://www.gentoo.org). Поэтому репозиториев для deltup обновлений пока очень мало. Результаты могут быть намного лучше если в репозиториях deltup появится больше delta пакетов между предыдущими версиями. К примеру в используемом автором репозитории испольуется всего -1 версия каждого пакета.

```
kdeartwork-kscreensaver-4.6.2-1_to_4.6.3-1-x86_64.delta	2011-May-06 22:35:41	301.8K	 application/octet-stream 
kdeartwork-kscreensaver-4.6.3-1-x86_64.pkg.tar.xz	2011-May-06 08:57:57	589.2K	 application/octet-stream

```