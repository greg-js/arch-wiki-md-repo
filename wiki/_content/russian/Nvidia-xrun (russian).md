**Состояние перевода:** На этой странице представлен перевод статьи [Nvidia-xrun](/index.php/Nvidia-xrun "Nvidia-xrun"). Дата последней синхронизации: 25 мая 2019\. Вы можете [помочь](/index.php/ArchWiki_Translation_Team_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "ArchWiki Translation Team (Русский)") синхронизировать перевод, если в английской версии произошли [изменения](https://wiki.archlinux.org/index.php?title=Nvidia-xrun&diff=0&oldid=573979).

[Nvidia-xrun](https://github.com/Witko/nvidia-xrun) — утилита, запускающая [X сервер](/index.php/Xorg_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Xorg (Русский)"), используя дискретный графический процессор NVIDIA, на ноутбуках с поддержкой NVIDIA Optimus. Это решение предлагает полное использование GPU, а также повышенные совместимость и производительность.

X сервер работает либо с интегрированным, либо с дискретным графическим процессором, но не с обоими сразу. Для использования другой видеокарты переключитесь на отдельную [виртуальную консоль](/index.php/Linux_console_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#Виртуальная_консоль "Linux console (Русский)") и запустите еще один X сервер.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Установка](#Установка)
*   [2 Настройка](#Настройка)
    *   [2.1 Установка корректного идентификатора шины](#Установка_корректного_идентификатора_шины)
    *   [2.2 Автоматический запуск оконного менеджер](#Автоматический_запуск_оконного_менеджер)
    *   [2.3 Использование bbswitch для управления картой NVIDIA](#Использование_bbswitch_для_управления_картой_NVIDIA)
*   [3 Использование](#Использование)
*   [4 Решение проблем](#Решение_проблем)
    *   [4.1 Графический процессор NVIDIA не отключается или устанавливается по умолчанию](#Графический_процессор_NVIDIA_не_отключается_или_устанавливается_по_умолчанию)

## Установка

[Установите](/index.php/%D0%A3%D1%81%D1%82%D0%B0%D0%BD%D0%BE%D0%B2%D0%B8%D1%82%D0%B5 "Установите"):

*   [nvidia](https://www.archlinux.org/packages/?name=nvidia)
*   [bbswitch](https://www.archlinux.org/packages/?name=bbswitch)
*   [nvidia-xrun](https://aur.archlinux.org/packages/nvidia-xrun/), [nvidia-xrun-git](https://aur.archlinux.org/packages/nvidia-xrun-git/)
    *   или [nvidia-xrun-pm](https://aur.archlinux.org/packages/nvidia-xrun-pm/) если `bbswitch` не поддерживает ваше оборудование [[1]](https://bbs.archlinux.org/viewtopic.php?id=238389)
*   [Оконный менеджер](/index.php/Window_manager_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Window manager (Русский)"), например, [openbox](https://www.archlinux.org/packages/?name=openbox) или [xfce4-session](https://www.archlinux.org/packages/?name=xfce4-session), так как запуск приложений напрямую c помощью `nvidia-xrun` работает некорректно.

## Настройка

### Установка корректного идентификатора шины

**Note:** Пользователи, которые установили `nvidia-xrun` из [AUR](/index.php/AUR "AUR"), могут пропустить этот шаг, потому что идентификатор шины устанавливается автоматически в `/etc/X11/nvidia-xorg.conf`.

Найдите ID шины вашего дисплея:

```
 $ lspci | grep -i nvidia | awk '{print $1}'

```

Выход будет аналогичен этому примеру: **`01:00.0`**.

После чего создайте файл, например, `/etc/X11/nvidia-xorg.conf.d/30-nvidia.conf`, для установки правильного ID шины:

 `/etc/X11/nvidia-xorg.conf.d/30-nvidia.conf` 
```
Section "Device"
    Identifier "nvidia"
    Driver "nvidia"
    BusID "PCI:**1:0:0**"
EndSection
```

Также можете изменить настройки NVIDIA, если возникли проблемы:

 `/etc/X11/nvidia-xorg.conf.d/30-nvidia.conf` 
```
Section "Screen"
    Identifier "nvidia"
    Device "nvidia"
    #  Option "AllowEmptyInitialConfiguration" "Yes"
    #  Option "UseDisplayDevice" "none"
EndSection
```

### Автоматический запуск оконного менеджер

Для удобства можете создать файл `~/.nvidia-xinitrc` для запуска `openbox`:

```
if [ $# -gt 0 ]; then
  $*
else
  openbox-session
  # Alternatively, you can also use xfce4:
  # xfce4-session
fi

```

Тогда не придется указывать приложение, просто выполните команду:

```
$ nvidia-xrun

```

### Использование bbswitch для управления картой NVIDIA

Когда карта NVIDIA не нужна, для отключения используется `bbswitch`. Скрипт `nvidia-xrun` автоматически позаботится о запуске оконного менеджера и включения карты NVIDIA. Для этого следует:

*   Загрузить модуль `bbswitch` при включении:

```
 # echo 'bbswitch ' > /etc/modules-load.d/bbswitch.conf

```

*   Отключить модуль `nvidia` при включении:

```
 # echo 'options bbswitch load_state=0 unload_state=1' > /etc/modprobe.d/bbswitch.conf 

```

После перезагрузки видеокарта NVIDIA будет отключена. Чтобы это увидеть, проверьте статус `bbswitch`:

```
 $ cat /proc/acpi/bbswitch  

```

Для принудительно включения или выключения видеокарты, выполните:

```
 # tee /proc/acpi/bbswitch <<<ON
 # tee /proc/acpi/bbswitch <<<OFF

```

Подробнее о `bbswitch` смотрите в [Bumblebee-Project/bbswitch](https://github.com/Bumblebee-Project/bbswitch).

## Использование

После загрузки войдите в систему с виртуальной консоли и выполните команду `nvidia-xrun`.

## Решение проблем

### Графический процессор NVIDIA не отключается или устанавливается по умолчанию

Если графический процессор NVIDIA по-прежнему не отключается или устанавливается по умолчанию, то придется занести в черный список модули, приведенные ниже. Создайте этот файл и перезапустите систему:

 `/usr/lib/modprobe.d/nvidia-xrun.conf` 
```
blacklist nvidia
blacklist nvidia-drm
blacklist nvidia-modeset
blacklist nvidia-uvm
blacklist nouveau

```

Убедитесь, что DRM Kernel Mode Setting отключен. См. [NVIDIA_(Русский)#DRM_kernel_mode_setting](/index.php/NVIDIA_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#DRM_kernel_mode_setting "NVIDIA (Русский)") и [Kernel_mode_setting_(Русский)](/index.php/Kernel_mode_setting_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Kernel mode setting (Русский)") для получения более подробной информации.