## Contents

*   [1 Предисловие](#.D0.9F.D1.80.D0.B5.D0.B4.D0.B8.D1.81.D0.BB.D0.BE.D0.B2.D0.B8.D0.B5)
*   [2 Установка vmware-player-modules](#.D0.A3.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B0_vmware-player-modules)
*   [3 Установка vmware-player](#.D0.A3.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B0_vmware-player)
*   [4 Конфигурация](#.D0.9A.D0.BE.D0.BD.D1.84.D0.B8.D0.B3.D1.83.D1.80.D0.B0.D1.86.D0.B8.D1.8F)
*   [5 Обновления ядра](#.D0.9E.D0.B1.D0.BD.D0.BE.D0.B2.D0.BB.D0.B5.D0.BD.D0.B8.D1.8F_.D1.8F.D0.B4.D1.80.D0.B0)

## Предисловие

Ниже представлен, возможно, самый быстрый способ установки vmware player на Arch Linux.

Данное руководство было написано для версий vmware player 1.03 и ядра 2.6.20\. Однако, актуально и для более поздних версий.

Названия и версии пакетов в данном руководстве могут отличаться от актуальных.

Вам потребуется скачать нужные для сборки файлы и поместить их в директорию ~/pkgbuild или в другую на ваше усмотрение.

Нет необходимости скачивать vmware-player и его модули для ядра самостоятельно, это будет сделано автоматически при вызове makepkg.

Замечание: если у вас уже имеются один или оба этих больших файла, просто поместите их в соответствующие директории. Например:

~/pkgbuild/vmware-player-modules/ и ~/pkgbuild/vmware-player/

## Установка vmware-player-modules

Необходимо скачать архив vmware-player-modules.tar.gz со страницы vmware-player-modules в AUR. Данный архив содержит инструкции для сборки и нужные патчи. Ссылка:

[https://aur.archlinux.org/packages/vmware-player-modules/vmware-player-modules.tar.gz](https://aur.archlinux.org/packages/vmware-player-modules/vmware-player-modules.tar.gz)

Далее распакуйте архив сюда:

~/pkgbuild/vmware-player-modules/

и выполните:

```
cd ~/pkgbuild/vmware-player-modules/

makepkg

```

таким образом, все нужные для сборки файлы скачаются и создастся пакет с, например, таким именем:

~/pkgbuild/vmware-player-modules/vmware-player-modules-1.0.3_34682-2.pkg.tar.gz

Этот пакет следует установить с помощью pacman:

```
pacman -A ~/pkgbuild/vmware-player-modules/vmware-player-modules-1.0.3_34682-2.pkg.tar.gz

```

Если все прошло хорошо, значит пакет vmware-player-modules установлен.

## Установка vmware-player

Как и в предыдущий раз, нужно скачать архив (vmware-player.tar.gz) со страницы AUR:

[https://aur.archlinux.org/packages/vmware-player/vmware-player.tar.gz](https://aur.archlinux.org/packages/vmware-player/vmware-player.tar.gz)

И распаковать сюда: ~/pkgbuild/vmware-player

Далее:

```
cd ~/pkgbuild/vmware-player/

makepkg

```

В результате появится пакет:

~/pkgbuild/vmware-player/vmware-player-1.0.3_34682-1.pkg.tar.gz

Устанавливаем:

```
pacman -A ~/pkgbuild/vmware-player/vmware-player-1.0.3_34682-1.pkg.tar.gz

```

## Конфигурация

Для конфигурации VMware Player нужно запустить скрипт по адресу /usr/bin/vmware-config.pl

Также следует добавить vmware в строку загружаемых демонов (DAEMONS) в файле /etc/rc.conf

**->** _для пользователей arch64:_ Если при попытке загрузить файл .vmx возникает следующая ошибка:

```
/usr/lib/vmware/bin/vmware-vmx: error while loading shared libraries: libXtst.so.6: wrong ELF class: ELFCLASS64

```

убедитесь, что пакет lib32-libxtst (находится в community) установлен.

## Обновления ядра

В случае установки новой версии ядра системы, vmware может перестать загружаться.

В этом случае нужно пересобрать vmware-player-modules