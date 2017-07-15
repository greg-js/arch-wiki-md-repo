**Состояние перевода:** На этой странице представлен перевод статьи [Install on WSL](/index.php/Install_on_WSL "Install on WSL"). Дата последней синхронизации: 11 июля 2017\. Вы можете [помочь](/index.php/ArchWiki_Translation_Team_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "ArchWiki Translation Team (Русский)") синхронизировать перевод, если в английской версии произошли [изменения](https://wiki.archlinux.org/index.php?title=Install_on_WSL&diff=0&oldid=481707).

В Windows 10 есть подсистема, которая эмулирует интерфейс ядра Linux, позволяя запускать обычные приложения Linux. Это похоже на противоположность [Wine](/index.php/Wine_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Wine (Русский)"), но на более низком уровне. По умолчанию она поставляется с пользовательским пространством Ubuntu, но ее можно заменить на Arch. Чтобы она работала исправно, для создания некоторых пакетов вам потребуется доступ к существующей установке Arch. Эти инструкции основаны на [этом руководстве](https://www.reddit.com/r/bashonubuntuonwindows/comments/5vnne8/howto_installing_arch_on_wsl_manually/).

## Подготовка

Вы должны запустить Windows 10 creator's update. Если вы еще не используюте подсистему Linux в Windows, следуйте инструкциям [здесь](https://msdn.microsoft.com/en-gb/commandline/wsl/install_guide), чтобы включить ее. В основном она включается так:

*   Режим разработчика в *Настройки > Обновление и безопасность > Для разработчиков* и
*   Подсистема Linux в Windows (бета) в разделе *"Включить или отключить функции Windows"*.

Если вы уже установили ее, используйте:

```
> lxrun /uninstall /full /y

```

чтобы полностью удалить существующую установку (сначала вы можете сохранить некоторые данные).

## Установка

**Примечание:** Вы также можете установить Ubuntu из [Windows Store](https://www.microsoft.com/en-us/store/p/ubuntu/9nblggh4msv6), хотя вам необходимо иметь Windows Insider (или запустите предстоящее обновление Fall Creators Update). Смотрите для получения [дополнительной информации](https://blogs.msdn.microsoft.com/commandline/2017/07/10/ubuntu-now-available-from-the-windows-store/).

Откройте командную строку и установите официальную версию Ubuntu:

```
> lxrun /install /y

```

Запустите bash:

```
> bash ~

```

Скачайте Arch bootstrap .tar.gz с [Arch Linux загрузок](https://www.archlinux.org/download/) и распакуйте его:

```
$ tar -zxvf /mnt/c/Users/*имя пользователя*/Downloads/archlinux-bootstrap-2017.06.01-x86_64.tar.gz

```

Раскомментируйте сервер в `~/root.x86_64/etc/pacman.d/mirrorlist`.

Сделайте WSL autogenerate `/etc/resolv.conf`:

```
$ echo "# Этот файл автоматически генерируется WSL. Чтобы остановить автоматическое создание этого файла, удалите эту строку." > ~/root.x86_64/etc/resolv.conf

```

Выйдите из всех приглашений bash, которые вы открыли.

В проводнике Windows перейдите к `C:\Users\*имя пользователя*\AppData\Local\lxss\rootfs` и удалите `bin`, `etc`, `lib`, `lib64`, `sbin`, `usr` и `var`.

Теперь переместите (не копируйте) те же папки из `C:\Users\*имя пользователя*\AppData\Local\lxss\root\root.x86_64` в `C:\Users\*имя пользователя*\AppData\Local\lxss\rootfs`

Используя компьютерную сборку Linux [fakeroot-tcp](https://aur.archlinux.org/packages/fakeroot-tcp/) и [glibc-wsl](https://aur.archlinux.org/packages/glibc-wsl/) скопируйте пакеты на ваш ПК с ОС Windows. *glibc-wsl* имеет обходное решение для [этой ошибки](https://github.com/Microsoft/BashOnWindows/issues/1878), а *fakeroot-tcp* необходим, пока не будет полностью реализована System V IPC [(смотрите здесь)](https://github.com/Microsoft/BashOnWindows/issues/1016). Этот шаг будет лишним, если эти ошибки будут исправлены.

Откройте снова bash и установите Arch:

```
# pacman-key --init
# pacman-key --populate archlinux
# pacman -U /mnt/c/Users/*имя пользователя*/Downloads/glibc-wsl-2.25-2-x86_64.pkg.tar.xz
# pacman -U /mnt/c/Users/*имя пользователя*/Downloads/fakeroot-tcp-1.21-2-x86_64.pkg.tar.xz
# pacman -Syyu base base-devel

```

Настройте пользователя (имя не обязательно должно совпадать с именем пользователя Windows):

```
# useradd -m -G wheel -s /bin/bash *имя пользователя*
# passwd root
# passwd *имя пользователя*

```

Задайте пользователю по умолчанию, выполнив следующее в командной строке Windows:

```
> lxrun /setdefaultuser *имя пользователя*

```