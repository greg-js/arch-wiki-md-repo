[Arch Build System](/index.php/Arch_Build_System "Arch Build System") позволит вам собрать собственное ядро на основе официального пакета Linux. Этот метод предлагает автоматизировать весь процесс компиляции и основан на тщательно протестированном пакете. Вы можете отредактировать PKGBUILD для использования собственных настроек ядра или для добавления дополнительных патчей.

## Contents

*   [1 Получение необходимых пакетов](#.D0.9F.D0.BE.D0.BB.D1.83.D1.87.D0.B5.D0.BD.D0.B8.D0.B5_.D0.BD.D0.B5.D0.BE.D0.B1.D1.85.D0.BE.D0.B4.D0.B8.D0.BC.D1.8B.D1.85_.D0.BF.D0.B0.D0.BA.D0.B5.D1.82.D0.BE.D0.B2)
*   [2 Редактирование PKGBUILD](#.D0.A0.D0.B5.D0.B4.D0.B0.D0.BA.D1.82.D0.B8.D1.80.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D0.B5_PKGBUILD)
    *   [2.1 Изменение prepare()](#.D0.98.D0.B7.D0.BC.D0.B5.D0.BD.D0.B5.D0.BD.D0.B8.D0.B5_prepare.28.29)
        *   [2.1.1 Load existing .config](#Load_existing_.config)
    *   [2.2 Пересоздание контрольных сумм](#.D0.9F.D0.B5.D1.80.D0.B5.D1.81.D0.BE.D0.B7.D0.B4.D0.B0.D0.BD.D0.B8.D0.B5_.D0.BA.D0.BE.D0.BD.D1.82.D1.80.D0.BE.D0.BB.D1.8C.D0.BD.D1.8B.D1.85_.D1.81.D1.83.D0.BC.D0.BC)
*   [3 Компиляция](#.D0.9A.D0.BE.D0.BC.D0.BF.D0.B8.D0.BB.D1.8F.D1.86.D0.B8.D1.8F)
*   [4 Установка](#.D0.A3.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B0)
*   [5 Загрузчик](#.D0.97.D0.B0.D0.B3.D1.80.D1.83.D0.B7.D1.87.D0.B8.D0.BA)

## Получение необходимых пакетов

Поскольку сборка осуществляется при помощи [makepkg](/index.php/Makepkg "Makepkg"), необходимо следовать рекомендациям ниже. К примеру, вы не сможете запустить makepkg от имени root/sudo, поэтому для начала создадим папку `build` в домашней директории пользователя.

```
 $ cd ~/
 $ mkdir build
 $ cd build/

```

[Установите](/index.php/%D0%A3%D1%81%D1%82%D0%B0%D0%BD%D0%BE%D0%B2%D0%B8%D1%82%D0%B5 "Установите") пакет [asp](https://www.archlinux.org/packages/?name=asp) и группу [base-devel](https://www.archlinux.org/groups/x86_64/base-devel/)

```
# pacman -S asp base-devel

```

Перед кастомизацией потребуется чистое ядро. Получите из ABS файлы пакета в рабочую папку командой:

 `$ ASPROOT=. asp checkout linux` 

Затем получите все остальные файлы, которые вам потребуются (например, пользовательские файлы конфигурации, патчи и т.д.) из соответствующих источников.

## Редактирование PKGBUILD

Отредактируйте `PKGBUILD` обратите внимание на параметр `pkgbase`. Укажите в нем имя вашего пакета, например:

```
 pkgbase=linux-custom

```

В зависимости от PKGBUILD также может потребоваться переименовать `linux.install` для соответствия измененному `pkgbase`.

### Изменение prepare()

Внутри этой функции вы можете применить патчи или изменить конфигурацию сборки ядра.

Если вам нужно изменить несколько опций можно использовать `config.x86_64` для 64-битной системы и `config` для 32-битной по умолчанию и добавить в него необходимые вам опции :

```
$ echo '
CONFIG_DEBUG_INFO=y
CONFIG_FOO=n
' >> config.x86_64

```

Также вы можете использовать утилиту с графическим интерфейсом для настройки параметров. Для этого раскомментируйте одну из возможных, указанных в prepare() функций в PKGBUILD, например:

 `PKGBUILD` 
```
...
  # load configuration
  # Configure the kernel. Replace the line below with one of your choice.
  #make menuconfig # CLI menu for configuration
  make nconfig # new CLI menu for configuration
  #make xconfig # X-based configuration
  #make oldconfig # using old config from previous kernel version
  # ... or manually edit .config
...

```

**Важно:** У systemd есть несколько требований к конфигурации ядра для работы, некоторых вариантов использования (напр., UEFI) и для специфичной функциональности (напр., bootchart). Несоблюдение этих требований может привести к нестабильной работе или отказу системы. Список необходимых и рекомендуемых параметров вы можете найти в файле `/usr/share/doc/systemd/README`. Сверьтесь с ним перед компиляцией. Сами требования время от времени меняются, а изменения не анонсируются, так как Arch предполагает, что вы используете официальное ядро. Перед установкой новой версии systemd обратитесь к примечанию к релизу и убедитесь, что ваша конфигурация ядра соответствует требованиям.

#### Load existing .config

If you have already a kernel `.config` file, uncommenting one of the interactive config tools, such as `nconfig`, and loading your `.config` from there avoids any problems with kernel naming that may otherwise occur - except in the case of at least make menuconfig. See note.

**Note:** If you uncomment and use 'make menuconfig' in prepare(), then use the menuconfig gui to load your existing config, you will run into problems with conflicting files in the end package. This is because you will overwrite the default config that PKGBUILD has modified to provide a unique install path, specifically the LOCALVERSION and LOCALVERSION_AUTO config options. To fix this, simply re-set LOCALVERSION to your custom kernel naming and LOCALVERSION_AUTO=n while still in menuconfig. For details, see [BBS#173504](https://bbs.archlinux.org/viewtopic.php?id=173504)

### Пересоздание контрольных сумм

Т.к. файл настройки был изменен, необходимо сгенерировать новые контрольные суммы, запустив:

```
$ updpkgsums

```

## Компиляция

Теперь можно приступить к компиляции ядра обычной командой `makepkg`. Если вы выбрали интерактивную программу для настройки параметров ядра (напр. menuconfig), вы должны присутствовать во время компиляции.

```
 $ makepkg -s

```

Параметр `-s` загрузит все необходимые зависимости, используемые последними ядрами, такие как xml и docs.

**Примечание:**

*   [Одновременный запуск нескольких процессов компиляции](/index.php/Makepkg#MAKEFLAGS "Makepkg") может значительно сократить время компиляции на многоядерных системах.
*   Ядру нужно время на компиляцию, 1 час - это вполне нормально. На современных системах с SSD обычно это занимает менее десяти минут.
*   Исходные коды ядра [подписаны PGP](https://www.kernel.org/signature.html#kernel-org-web-of-trust), и makepkg проверит это. Смотрите [Makepkg#Signature checking](/index.php/Makepkg#Signature_checking "Makepkg") для получения подробностей.

## Установка

После makepkg, вы можете посмотреть файл linux.install. Можно заметить, что некоторые переменные изменились. Теперь пакет можно установить, как обычно, с помощью pacman (или эквивалентной программы):

```
# pacman -U <kernel-headers_package>
# pacman -U <kernel_package>

```

**Примечание:** Желательно так же установить kernel headers. Он может понадобится, если, к примеру, понадобится установить драйвера NVIDIA с [nvidia-hook](/index.php/NVIDIA#Alternate_install:_custom_kernel "NVIDIA")

## Загрузчик

К этому времени файлы и каталоги для собранного вами ядра должны быть созданы, например, `/boot/vmlinuz-linux-test`. Для проверки вашего ядра нужно обновить загрузчик (/boot/grub/menu.lst для GRUB), добавив новые записи ('default' and 'fallback') для вашего свежесозданного ядра. Таким образом, вы можете паралельно хранить и основное и собранное вами ядра.