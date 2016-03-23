**Состояние перевода:** На этой странице представлен перевод статьи [NVIDIA/Tips and tricks](/index.php/NVIDIA/Tips_and_tricks "NVIDIA/Tips and tricks"). Дата последней синхронизации: 23 марта 2016\. Вы можете [помочь](/index.php/ArchWiki_Translation_Team_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "ArchWiki Translation Team (Русский)") синхронизировать перевод, если в английской версии произошли [изменения](https://wiki.archlinux.org/index.php?title=NVIDIA/Tips_and_tricks&diff=0&oldid=427264).

Смотрите главную статью [NVIDIA](/index.php/NVIDIA_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "NVIDIA (Русский)").

## Contents

*   [1 Исправление разрешения терминала](#.D0.98.D1.81.D0.BF.D1.80.D0.B0.D0.B2.D0.BB.D0.B5.D0.BD.D0.B8.D0.B5_.D1.80.D0.B0.D0.B7.D1.80.D0.B5.D1.88.D0.B5.D0.BD.D0.B8.D1.8F_.D1.82.D0.B5.D1.80.D0.BC.D0.B8.D0.BD.D0.B0.D0.BB.D0.B0)
*   [2 Использование ТВ-выхода](#.D0.98.D1.81.D0.BF.D0.BE.D0.BB.D1.8C.D0.B7.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D0.B5_.D0.A2.D0.92-.D0.B2.D1.8B.D1.85.D0.BE.D0.B4.D0.B0)
*   [3 X with a TV (DFP) as the only display](#X_with_a_TV_.28DFP.29_as_the_only_display)
*   [4 Проверьте источник питания](#.D0.9F.D1.80.D0.BE.D0.B2.D0.B5.D1.80.D1.8C.D1.82.D0.B5_.D0.B8.D1.81.D1.82.D0.BE.D1.87.D0.BD.D0.B8.D0.BA_.D0.BF.D0.B8.D1.82.D0.B0.D0.BD.D0.B8.D1.8F)
*   [5 Listening to ACPI events](#Listening_to_ACPI_events)
*   [6 Отображение температуры графического процессора в оболочке](#.D0.9E.D1.82.D0.BE.D0.B1.D1.80.D0.B0.D0.B6.D0.B5.D0.BD.D0.B8.D0.B5_.D1.82.D0.B5.D0.BC.D0.BF.D0.B5.D1.80.D0.B0.D1.82.D1.83.D1.80.D1.8B_.D0.B3.D1.80.D0.B0.D1.84.D0.B8.D1.87.D0.B5.D1.81.D0.BA.D0.BE.D0.B3.D0.BE_.D0.BF.D1.80.D0.BE.D1.86.D0.B5.D1.81.D1.81.D0.BE.D1.80.D0.B0_.D0.B2_.D0.BE.D0.B1.D0.BE.D0.BB.D0.BE.D1.87.D0.BA.D0.B5)
    *   [6.1 Method 1 - nvidia-settings](#Method_1_-_nvidia-settings)
    *   [6.2 Method 2 - nvidia-smi](#Method_2_-_nvidia-smi)
    *   [6.3 Method 3 - nvclock](#Method_3_-_nvclock)
*   [7 Установка скорости вентилятора при входе](#.D0.A3.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B0_.D1.81.D0.BA.D0.BE.D1.80.D0.BE.D1.81.D1.82.D0.B8_.D0.B2.D0.B5.D0.BD.D1.82.D0.B8.D0.BB.D1.8F.D1.82.D0.BE.D1.80.D0.B0_.D0.BF.D1.80.D0.B8_.D0.B2.D1.85.D0.BE.D0.B4.D0.B5)
*   [8 Switching between NVIDIA and nouveau drivers](#Switching_between_NVIDIA_and_nouveau_drivers)
*   [9 Как избежать разрывов/тиринга на картах GeForce серий 500/600/700/900](#.D0.9A.D0.B0.D0.BA_.D0.B8.D0.B7.D0.B1.D0.B5.D0.B6.D0.B0.D1.82.D1.8C_.D1.80.D0.B0.D0.B7.D1.80.D1.8B.D0.B2.D0.BE.D0.B2.2F.D1.82.D0.B8.D1.80.D0.B8.D0.BD.D0.B3.D0.B0_.D0.BD.D0.B0_.D0.BA.D0.B0.D1.80.D1.82.D0.B0.D1.85_GeForce_.D1.81.D0.B5.D1.80.D0.B8.D0.B9_500.2F600.2F700.2F900)
*   [10 Manual configuration](#Manual_configuration)
    *   [10.1 Отключение логотипа при загрузке](#.D0.9E.D1.82.D0.BA.D0.BB.D1.8E.D1.87.D0.B5.D0.BD.D0.B8.D0.B5_.D0.BB.D0.BE.D0.B3.D0.BE.D1.82.D0.B8.D0.BF.D0.B0_.D0.BF.D1.80.D0.B8_.D0.B7.D0.B0.D0.B3.D1.80.D1.83.D0.B7.D0.BA.D0.B5)
    *   [10.2 Overriding monitor detection](#Overriding_monitor_detection)
    *   [10.3 Включение контроля яркости](#.D0.92.D0.BA.D0.BB.D1.8E.D1.87.D0.B5.D0.BD.D0.B8.D0.B5_.D0.BA.D0.BE.D0.BD.D1.82.D1.80.D0.BE.D0.BB.D1.8F_.D1.8F.D1.80.D0.BA.D0.BE.D1.81.D1.82.D0.B8)
    *   [10.4 Включение SLI](#.D0.92.D0.BA.D0.BB.D1.8E.D1.87.D0.B5.D0.BD.D0.B8.D0.B5_SLI)
    *   [10.5 Включение разгона](#.D0.92.D0.BA.D0.BB.D1.8E.D1.87.D0.B5.D0.BD.D0.B8.D0.B5_.D1.80.D0.B0.D0.B7.D0.B3.D0.BE.D0.BD.D0.B0)
        *   [10.5.1 Настройка статического 2D/3D разгона](#.D0.9D.D0.B0.D1.81.D1.82.D1.80.D0.BE.D0.B9.D0.BA.D0.B0_.D1.81.D1.82.D0.B0.D1.82.D0.B8.D1.87.D0.B5.D1.81.D0.BA.D0.BE.D0.B3.D0.BE_2D.2F3D_.D1.80.D0.B0.D0.B7.D0.B3.D0.BE.D0.BD.D0.B0)

## Исправление разрешения терминала

Переход с драйвера nouveau будет сопровождаться низким разрешением экрана терминала при загрузке. Для загрузчика GRUB, обратитесь к [GRUB/Tips and tricks#Setting the framebuffer resolution](/index.php/GRUB/Tips_and_tricks#Setting_the_framebuffer_resolution "GRUB/Tips and tricks"), чтобы увеличить разрешение.

## Использование ТВ-выхода

Хорошая статья об этом есть [тут](http://en.wikibooks.org/wiki/NVidia/TV-OUT).

## X with a TV (DFP) as the only display

Сервер X откатывается к CRT-0, если нет автоматически определённого монитора. Это может стать проблемой при использовании подключения ТВ через DVI как основной монитор, и сервер X был запущен при выключенном ТВ или он был не подключен.

Для принудительного использования DFP драйвером NVIDIA, сохраните копию EDID в файловой системе там, где его сможет прочитать сервер X, вместо чтения EDID с ТВ/DFP.

Для получения EDID запустите nvidia-settings. Появится различная информация в древовидном формате, игнорируя все настройки выберите графический процессор (соответствующее поле должно называться "GPU-0" или быть похожим на него), щелкните по `DFP` секции (также возможно `DFP-0` или что-то похожее), нажмите на кнопку `Acquire Edid` и сохраните куда-нибудь, например в `/etc/X11/dfp0.edid`.

Если у вас не подключена мышь и клавиатура, EDID может быть получен из командной строки. Запустите сервер X с нужным логированием для вывода блока EDID:

```
$ startx -- -logverbose 6

```

После окончания иницализации сервера X закройте его, ваш лог файл сохранится в `/var/log/Xorg.0.log`. Извлеките блок EDID используя nvidia-xconfig:

```
$ nvidia-xconfig --extract-edids-from-file=/var/log/Xorg.0.log --extract-edids-output-file=/etc/X11/dfp0.bin

```

Отредактируйте `xorg.conf` добавив в секцию `Device` строки:

```
Option "ConnectedMonitor" "DFP"
Option "CustomEDID" "DFP-0:/etc/X11/dfp0.edid"

```

Опция `ConnectedMonitor` принуждает драйвер распознавать DFP так, как буд-то он подключен. `CustomEDID` предоставляет данные EDID для устройства и говорит, что при загрузке ТВ/DFP как бы был подключен во время процесса запуска X.

Таким образом, можно автоматически запускать менеджер экрана при загрузке, иметь рабочий и настроенный экран для X до включения питания ТВ.

Если вышеуказанные изменения не работают, в `xorg.conf` в секции `Device` вы можете попробовать удалить строку `Option "ConnectedMonitor" "DFP"` и добавить следующие строки:

```
Option "ModeValidation" "NoDFPNativeResolutionCheck"
Option "ConnectedMonitor" "DFP-0"

```

Опция драйвера NVIDIA `NoDFPNativeResolutionCheck` предотвращает отключение всех режимов, которые не подходят к основному разрешению.

## Проверьте источник питания

The NVIDIA X.org driver can also be used to detect the GPU's current source of power. To see the current power source, check the 'GPUPowerSource' read-only parameter (0 - AC, 1 - battery):

 `$ nvidia-settings -q GPUPowerSource -t`  `1` 

## Listening to ACPI events

NVIDIA drivers automatically try to connect to the [acpid](/index.php/Acpid "Acpid") daemon and listen to ACPI events such as battery power, docking, some hotkeys, etc. If connection fails, X.org will output the following warning:

 `~/.local/share/xorg/Xorg.0.log` 
```
NVIDIA(0): ACPI: failed to connect to the ACPI event daemon; the daemon
NVIDIA(0):     may not be running or the "AcpidSocketPath" X
NVIDIA(0):     configuration option may not be set correctly.  When the
NVIDIA(0):     ACPI event daemon is available, the NVIDIA X driver will
NVIDIA(0):     try to use it to receive ACPI event notifications.  For
NVIDIA(0):     details, please see the "ConnectToAcpid" and
NVIDIA(0):     "AcpidSocketPath" X configuration options in Appendix B: X
NVIDIA(0):     Config Options in the README.

```

While completely harmless, you may get rid of this message by disabling the `ConnectToAcpid` option in your `/etc/X11/xorg.conf.d/20-nvidia.conf`:

```
Section "Device"
  ...
  Driver "nvidia"
  Option "ConnectToAcpid" "0"
  ...
EndSection

```

If you are on laptop, it might be a good idea to install and enable the [acpid](/index.php/Acpid "Acpid") daemon instead.

## Отображение температуры графического процессора в оболочке

### Method 1 - nvidia-settings

**Примечание:** Данный метод требует наличия сервера X. Используйте второй или третий метод если X сервер вам не нужен. Также, третий метод не работает с новыми картами NVIDIA, такими как GeForce 200 series, и с интегрированными графическими решениями, такими как Zotac IONITX's 8800GS.

Для отображения температуры графического ядра в оболочке используйте `nvidia-settings` как указано ниже:

```
$ nvidia-settings -q gpucoretemp

```

Вывод должен быть примерно такой:

```
Attribute 'GPUCoreTemp' (hostname:0.0): 41.
'GPUCoreTemp' is an integer attribute.
'GPUCoreTemp' is a read-only attribute.
'GPUCoreTemp' can use the following target types: X Screen, GPU.

```

Температура графического процессора этой платы 41 °C.

Пример того, как получить значение температуры для использования в утилитах `rrdtool` или `conky` и др.:

 `$ nvidia-settings -q gpucoretemp -t`  `41` 

### Method 2 - nvidia-smi

`nvidia-smi` может читать температуру прямо с графического процессора без использования сервера X. Это важно для небольшой группы пользователей, которые не имеют запущенного сервера X, те, кто используют ОС для серверных приложений. Отображение температуры графического процессора с использованием nvidia-smi:

```
$ nvidia-smi

```

Пример вывода результата работы программы:

 `$ nvidia-smi` 
```
Fri Jan  6 18:53:54 2012       
+------------------------------------------------------+                       
| NVIDIA-SMI 2.290.10   Driver Version: 290.10         |                       
|-------------------------------+----------------------+----------------------+
| Nb.  Name                     | Bus Id        Disp.  | Volatile ECC SB / DB |
| Fan   Temp   Power Usage /Cap | Memory Usage         | GPU Util. Compute M. |
|===============================+======================+======================|
| 0\.  GeForce 8500 GT           | 0000:01:00.0  N/A    |       N/A        N/A |
|  30%   62 C  N/A   N/A /  N/A |  17%   42MB /  255MB |  N/A      Default    |
|-------------------------------+----------------------+----------------------|
| Compute processes:                                               GPU Memory |
|  GPU  PID     Process name                                       Usage      |
|=============================================================================|
|  0\.           ERROR: Not Supported                                          |
+-----------------------------------------------------------------------------+

```

Только температура:

 `$ nvidia-smi -q -d TEMPERATURE` 
```

==============NVSMI LOG==============

Timestamp                           : Sun Apr 12 08:49:10 2015
Driver Version                      : 346.59

Attached GPUs                       : 1
GPU 0000:01:00.0
    Temperature
        GPU Current Temp            : 52 C
        GPU Shutdown Temp           : N/A
        GPU Slowdown Temp           : N/A

```

Пример того, как получить значение температуры для использования в утилитах `rrdtool` или `conky` и др.:

 `$ nvidia-smi -q -d TEMPERATURE | awk '/GPU Current Temp/ {print $5}'`  `52` 

Ссылка на руководство: [http://www.question-defense.com/2010/03/22/gpu-linux-shell-temp-get-nvidia-gpu-temperatures-via-linux-cli](http://www.question-defense.com/2010/03/22/gpu-linux-shell-temp-get-nvidia-gpu-temperatures-via-linux-cli).

### Method 3 - nvclock

Используйте [nvclock](https://aur.archlinux.org/packages/nvclock/), который доступен в [AUR](/index.php/AUR "AUR").

**Примечание:** `nvclock` не может получить доступ к тепловому сенсору на картах NVIDIA новее Geforce 200 series.

Могут быть расхождения значений температуры между nvclock и nvidia-settings/nv-control. В соответствии с [этим сообщением](http://sourceforge.net/projects/nvclock/forums/forum/67426/topic/1906899) от автора (thunderbird) nvclock, значения выдаваемые nvclock более точные.

## Установка скорости вентилятора при входе

Вы можете выставить скорость вентилятора вашей графической карты с помощью консольного интерфейса *nvidia-settings*. Сначала убедитесь в том, что в вашем конфигурационом файле Xorg значения опции Coolbits установлены в `4`, `5` или `12` для архитектуры Ферми и выше в секции `Device` для включения управления скоростью вентилятора.

```
Option "Coolbits" "4"

```

**Примечание:** Для карт GeForce 400/500 series, на текущий момент, этот метод при входе не устанавливает скорость вентилятора. Также, этот метод только позволяет настраивать скорость вентилятора только для текущей сессии X через nvidia-settings.

Поместите следующую строку в ваш файл [xinitrc](/index.php/Xinitrc "Xinitrc") для управления вентилятором при запуске Xorg. Замените `*n*` на значение скорости вентилятора нужное вам в процентах.

```
nvidia-settings -a "[gpu:0]/GPUFanControlState=1" -a "[fan:0]/GPUCurrentFanSpeed=*n*"

```

Также вы можете указать и второй графический процессор, путем увеличения счетчика графического процесора и вентилятора.

```
nvidia-settings -a "[gpu:0]/GPUFanControlState=1" -a "[fan:0]/GPUCurrentFanSpeed=*n*" \
                -a "[gpu:1]/GPUFanControlState=1" -a  [fan:1]/GPUCurrentFanSpeed=*n*" &

```

Если вы ипользуете менеджер входа такой как GDM или KDM, вы можете создать файл настроек. Создайте `~/.config/autostart/nvidia-fan-speed.desktop` и вставьте следующий текст.Снова измените `*n*` на значение скорости вентилятора нужное вам в процентах.

```
[Desktop Entry]
Type=Application
Exec=nvidia-settings -a "[gpu:0]/GPUFanControlState=1" -a "[fan:0]/GPUCurrentFanSpeed=*n*"
X-GNOME-Autostart-enabled=true
Name=nvidia-fan-speed

```

**Примечание:** С версии драйвера 349.16, опция `GPUCurrentFanSpeed` заменена на `GPUTargetFanSpeed`. [[1]](https://devtalk.nvidia.com/default/topic/821563/linux/can-t-control-fan-speed-with-beta-driver-349-12/post/4526208/#4526208)

## Switching between NVIDIA and nouveau drivers

If you need to switch between drivers, you may use the following script, run as root (say yes to all confirmations):

```
#!/bin/bash
BRANCH= # Enter a branch if needed, i.e. -340xx or -304xx
NVIDIA=nvidia${BRANCH} # If no branch entered above this would be "nvidia"
NOUVEAU=xf86-video-nouveau

# Replace -R with -Rs to if you want to remove the unneeded dependencies
if [ $(pacman -Qqs ^mesa-libgl$) ]; then
    pacman -S $NVIDIA ${NVIDIA}-libgl # Add lib32-${NVIDIA}-libgl and ${NVIDIA}-lts if needed
    # pacman -R $NOUVEAU
elif [ $(pacman -Qqs ^${NVIDIA}$) ]; then
    pacman -S --needed $NOUVEAU mesa-libgl # Add lib32-mesa-libgl if needed
    pacman -R $NVIDIA # Add ${NVIDIA}-lts if needed
fi

```

## Как избежать разрывов/тиринга на картах GeForce серий 500/600/700/900

Разрывов можно избежать принудительным включением цепочки полного композитинга, независимо от используего вами композитора. Для проверки работоспособности опции, выполните

```
nvidia-settings --assign CurrentMetaMode="nvidia-auto-select +0+0 { ForceFullCompositionPipeline = On }"

```

Вам будет сообщено, что производительность некоторых приложений OpenGL может быть снижена.

Для постоянного использования сделанных изменений, вам необходимо добавить следующую строку в секцию `"Screen"` вашего конфигурационного файла Xorg, например `/etc/X11/xorg.conf.d/20-nvidia.conf`:

```
Option  "metamodes" "nvidia-auto-select +0+0 { ForceFullCompositionPipeline = On }"

```

Если у вас нет конфигурационного файла Xorg, вы можете создать его для текущей видеокарты исполльзуя `nvidia-xconfig` (смотрите [#Автоматическая настройка](#.D0.90.D0.B2.D1.82.D0.BE.D0.BC.D0.B0.D1.82.D0.B8.D1.87.D0.B5.D1.81.D0.BA.D0.B0.D1.8F_.D0.BD.D0.B0.D1.81.D1.82.D1.80.D0.BE.D0.B9.D0.BA.D0.B0)) и переместить его из `/etc/X11/xorg.conf` в более удобное место `/etc/X11/xorg.conf.d/20-nvidia.conf`.

## Manual configuration

Several tweaks (which cannot be enabled [automatically](#Automatic_configuration) or with the [GUI](#NVIDIA_Settings)) can be performed by editing your [config](#Configuring) file. The Xorg server will need to be restarted before any changes are applied.

See [NVIDIA Accelerated Linux Graphics Driver README and Installation Guide](ftp://download.nvidia.com/XFree86/Linux-x86/355.11/README/README.txt) for additional details and options.

### Отключение логотипа при загрузке

Добавьте опцию `"NoLogo"` внутри секции `Device`:

```
Option "NoLogo" "1"

```

### Overriding monitor detection

The `"ConnectedMonitor"` option under section `Device` allows to override monitor detection when X server starts, which may save a significant amount of time at start up. The available options are: `"CRT"` for analog connections, `"DFP"` for digital monitors and `"TV"` for televisions.

The following statement forces the NVIDIA driver to bypass startup checks and recognize the monitor as DFP:

```
Option "ConnectedMonitor" "DFP"

```

**Note:** Use "CRT" for all analog 15 pin VGA connections, even if the display is a flat panel. "DFP" is intended for DVI, HDMI, or DisplayPort digital connections only.

### Включение контроля яркости

Добавьте в секцию `Device` строку:

```
Option "RegistryDwords" "EnableBrightnessControl=1"

```

Если контроль яркости не заработает после применения данной опции, попробуйте установить [nvidia-bl](https://aur.archlinux.org/packages/nvidia-bl/) или [nvidiabl](https://aur.archlinux.org/packages/nvidiabl/).

### Включение SLI

**Важно:** По состоянию на Май 7, 2011, вы можете испытывать проблемы с производительностью видео в GNOME 3, после включения SLI.

Выдержка из [README](ftp://download.nvidia.com/XFree86/Linux-x86/355.11/README/xconfigoptions.html) драйвера NVIDIA Приложение B: *Данная опция контролирует рендеринг SLI в поддерживаемых конфигурациях.* Другими словами, в "поддерживаемых конфигурациях" обозначены компьютеры оборудованные материнской платой c сертифицированной поддержкой SLI и 2 или 3 графических процессора GeForce, также с сертифицированной поддержкой SLI. Смотрите [Зона SLI (англ.)](http://www.slizone.com/page/home.html) для получения подробной информации.

Найдем первый PCI Bus ID графического процессора, используя `lspci`:

 `$ lspci | grep VGA` 
```
03:00.0 VGA compatible controller: nVidia Corporation G92 [GeForce 8800 GTS 512] (rev a2)
05:00.0 VGA compatible controller: nVidia Corporation G92 [GeForce 8800 GTS 512] (rev a2)

```

Добавим BusID (3 в нашем случае) в секцию `Device`:

```
BusID "PCI:3:0:0"

```

**Примечание:** Формат написания очень важен. Значение BusID должно быть указано в таком формате `"PCI:<BusID>:0:0"`

Добавьте желаемое значение режима рендеринга SLI в секцию `Screen`:

```
Option "SLI" "AA"

```

Следущая таблица описывает доступные режимы рендеринга.

| Значение | Описание |
| 0, no, off, false, Single | Использовать только один графический процессор для рендеринга. |
| 1, yes, on, true, Auto | Включить SLI и позволить драйверу автоматически выбрать режим рендеринга. |
| AFR | Включить SLI и использовать режим поочередного рендеринга кадров. |
| SFR | Включить SLI и использовать режим разделённого рендеринга кадров. |
| AA | Включить SLI и использовать сглаживание SLI. Используйте в сочетании с полным сглаживанием сцены, для улучшения качества визуализации. |

Другой вариант, вы можете использовать утилиту `nvidia-xconfig` для вставки изменений в `xorg.conf` одной командой:

```
# nvidia-xconfig --busid=PCI:3:0:0 --sli=AA

```

Для проверки работы режима SLI в консольном режиме:

 `$ nvidia-settings -q all | grep SLIMode` 
```
  Attribute 'SLIMode' (arch:0.0): AA 
    'SLIMode' is a string attribute.
    'SLIMode' is a read-only attribute.
    'SLIMode' can use the following target types: X Screen.

```

**Важно:** После включения SLI ваша система может зависать/не отвечать после запуска Xorg. Желательно отключить менеджер входа до перезагрузки.

### Включение разгона

**Важно:** Помните, что разгон может привести к повреждению оборудования и авторы этой страницы снимают с себя любую ответственность за повреждение оборудования, вся информация, в том числе и возможность разгона, указывается изготовителем в спецификации к оборудованию.

Разгон контролируется через опцию *Coolbits* в секции `Device`, позволяя использовать различные неподдерживаемые свойства:

```
Option "Coolbits" "*value*"

```

**Совет:** Опция *Coolbits* легко контролируется через *nvidia-xconfig*, которая может управлять файлами конфигурации Xorg: `# nvidia-xconfig --cool-bits=*value*` 

Значение *Coolbits* - сумма его составляющих битов в двоичной системе исчисления. Типы битов:

*   `1` (bit 0) - Включает возможность разгона для старых (до архитектуры Fermi) ядер, вкладка *Clock Frequencies* в *nvidia-settings*.
*   `2` (bit 1) - Когда бит установлен, драйвер "будет пытаться инициализировать режим SLI, когда используются два графических процессора с разным количеством видеопамяти".
*   `4` (bit 2) - Включает ручное управление охлаждением графического процессора вкладка *Thermal Monitor* в *nvidia-settings*.
*   `8` (bit 3) - Включает возможность разгона на вкладке *PowerMizer* в *nvidia-settings*. Доступна с версии 337.12 для архитектур Fermi и новее. [[2]](http://www.phoronix.com/scan.php?px=MTY1OTM&page=news_item)
*   `16` (bit 4) - Включает возможность повышения напряжения через параметры командной строки *nvidia-settings*. Доступна с версии 337.12 для архитектур Fermi и новее.[[3]](http://www.phoronix.com/scan.php?page=news_item&px=MTg0MDI)

Чтобы включить несколько свойств, сложите значения *Coolbits*. Например, чтобы включить возможности разгона и повышения напряжения для архитектуры Fermi, установите значение `Option "Coolbits" "24"`.

Документация по *Coolbits* находится в `/usr/share/doc/nvidia/html/xconfigoptions.html`. Последния онлайн-версия документации по *Coolbits* (версия драйвера 355.11) находится [тут (англ.)](ftp://download.nvidia.com/XFree86/Linux-x86/355.11/README/xconfigoptions.html).

**Примечание:** Также, возможно отредактировать и переписать BIOS графического процессора, используя DOS (предпочтительнее) или с использованием Win32 окружения с помощью [nvflash](http://www.mvktech.net/component/option,com_remository/Itemid,26/func,select/id,127/orderby,2/page,1/) и [NiBiTor 6.0](http://www.mvktech.net/component/option,com_remository/Itemid,26/func,select/id,135/orderby,2/page,1/). Преимущество данного способа в том, что вы можете поднять не только напряжение, но и повысить стабильность программных методов разгона, такие как Coolbits. [Руководство по модификации BIOS архитектуры Fermi (англ.)](http://ivanvojtko.blogspot.sk/2014/03/how-to-overclock-geforce-460gtx-fermi.html)

#### Настройка статического 2D/3D разгона

Установите следующую строку в секции `Device` для включения PowerMizer на максимальную производительность (VSync не будет работать без этой строки):

```
Option "RegistryDwords" "PerfLevelSrc=0x2222"

```