## Contents

*   [1 Настройка стандартных устройств ввода](#.D0.9D.D0.B0.D1.81.D1.82.D1.80.D0.BE.D0.B9.D0.BA.D0.B0_.D1.81.D1.82.D0.B0.D0.BD.D0.B4.D0.B0.D1.80.D1.82.D0.BD.D1.8B.D1.85_.D1.83.D1.81.D1.82.D1.80.D0.BE.D0.B9.D1.81.D1.82.D0.B2_.D0.B2.D0.B2.D0.BE.D0.B4.D0.B0)
*   [2 Установка стандартного устройтва ввода](#.D0.A3.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B0_.D1.81.D1.82.D0.B0.D0.BD.D0.B4.D0.B0.D1.80.D1.82.D0.BD.D0.BE.D0.B3.D0.BE_.D1.83.D1.81.D1.82.D1.80.D0.BE.D0.B9.D1.82.D0.B2.D0.B0_.D0.B2.D0.B2.D0.BE.D0.B4.D0.B0)
*   [3 Одновременный HDMI и аналоговый вывод](#.D0.9E.D0.B4.D0.BD.D0.BE.D0.B2.D1.80.D0.B5.D0.BC.D0.B5.D0.BD.D0.BD.D1.8B.D0.B9_HDMI_.D0.B8_.D0.B0.D0.BD.D0.B0.D0.BB.D0.BE.D0.B3.D0.BE.D0.B2.D1.8B.D0.B9_.D0.B2.D1.8B.D0.B2.D0.BE.D0.B4)
*   [4 Настройка HDMI вывода](#.D0.9D.D0.B0.D1.81.D1.82.D1.80.D0.BE.D0.B9.D0.BA.D0.B0_HDMI_.D0.B2.D1.8B.D0.B2.D0.BE.D0.B4.D0.B0)
    *   [4.1 Поиск HDMI вывода](#.D0.9F.D0.BE.D0.B8.D1.81.D0.BA_HDMI_.D0.B2.D1.8B.D0.B2.D0.BE.D0.B4.D0.B0)
    *   [4.2 Проверка на правильную карту](#.D0.9F.D1.80.D0.BE.D0.B2.D0.B5.D1.80.D0.BA.D0.B0_.D0.BD.D0.B0_.D0.BF.D1.80.D0.B0.D0.B2.D0.B8.D0.BB.D1.8C.D0.BD.D1.83.D1.8E_.D0.BA.D0.B0.D1.80.D1.82.D1.83)
    *   [4.3 Ручная настройка PulseAudio,чтобы он находил HDMI Nvidia](#.D0.A0.D1.83.D1.87.D0.BD.D0.B0.D1.8F_.D0.BD.D0.B0.D1.81.D1.82.D1.80.D0.BE.D0.B9.D0.BA.D0.B0_PulseAudio.2C.D1.87.D1.82.D0.BE.D0.B1.D1.8B_.D0.BE.D0.BD_.D0.BD.D0.B0.D1.85.D0.BE.D0.B4.D0.B8.D0.BB_HDMI_Nvidia)
*   [5 Настройка объёмного звука](#.D0.9D.D0.B0.D1.81.D1.82.D1.80.D0.BE.D0.B9.D0.BA.D0.B0_.D0.BE.D0.B1.D1.8A.D1.91.D0.BC.D0.BD.D0.BE.D0.B3.D0.BE_.D0.B7.D0.B2.D1.83.D0.BA.D0.B0)
    *   [5.1 Разделение передний/задний](#.D0.A0.D0.B0.D0.B7.D0.B4.D0.B5.D0.BB.D0.B5.D0.BD.D0.B8.D0.B5_.D0.BF.D0.B5.D1.80.D0.B5.D0.B4.D0.BD.D0.B8.D0.B9.2F.D0.B7.D0.B0.D0.B4.D0.BD.D0.B8.D0.B9)
    *   [5.2 Разделение 7.1 на 5.1 + 2.0](#.D0.A0.D0.B0.D0.B7.D0.B4.D0.B5.D0.BB.D0.B5.D0.BD.D0.B8.D0.B5_7.1_.D0.BD.D0.B0_5.1_.2B_2.0)
    *   [5.3 LFE ремиксинг](#LFE_.D1.80.D0.B5.D0.BC.D0.B8.D0.BA.D1.81.D0.B8.D0.BD.D0.B3)
*   [6 PulseAudio через сеть](#PulseAudio_.D1.87.D0.B5.D1.80.D0.B5.D0.B7_.D1.81.D0.B5.D1.82.D1.8C)
    *   [6.1 Поддержка TCP (звук через сеть)](#.D0.9F.D0.BE.D0.B4.D0.B4.D0.B5.D1.80.D0.B6.D0.BA.D0.B0_TCP_.28.D0.B7.D0.B2.D1.83.D0.BA_.D1.87.D0.B5.D1.80.D0.B5.D0.B7_.D1.81.D0.B5.D1.82.D1.8C.29)
    *   [6.2 Поддержка TCP с анонимными клиентами](#.D0.9F.D0.BE.D0.B4.D0.B4.D0.B5.D1.80.D0.B6.D0.BA.D0.B0_TCP_.D1.81_.D0.B0.D0.BD.D0.BE.D0.BD.D0.B8.D0.BC.D0.BD.D1.8B.D0.BC.D0.B8_.D0.BA.D0.BB.D0.B8.D0.B5.D0.BD.D1.82.D0.B0.D0.BC.D0.B8)
    *   [6.3 Zeroconf (Avahi)](#Zeroconf_.28Avahi.29)
    *   [6.4 Переключение PulseAudio сервера ипользуется локальными X клиентами](#.D0.9F.D0.B5.D1.80.D0.B5.D0.BA.D0.BB.D1.8E.D1.87.D0.B5.D0.BD.D0.B8.D0.B5_PulseAudio_.D1.81.D0.B5.D1.80.D0.B2.D0.B5.D1.80.D0.B0_.D0.B8.D0.BF.D0.BE.D0.BB.D1.8C.D0.B7.D1.83.D0.B5.D1.82.D1.81.D1.8F_.D0.BB.D0.BE.D0.BA.D0.B0.D0.BB.D1.8C.D0.BD.D1.8B.D0.BC.D0.B8_X_.D0.BA.D0.BB.D0.B8.D0.B5.D0.BD.D1.82.D0.B0.D0.BC.D0.B8)
    *   [6.5 Если всё остальное не работает](#.D0.95.D1.81.D0.BB.D0.B8_.D0.B2.D1.81.D1.91_.D0.BE.D1.81.D1.82.D0.B0.D0.BB.D1.8C.D0.BD.D0.BE.D0.B5_.D0.BD.D0.B5_.D1.80.D0.B0.D0.B1.D0.BE.D1.82.D0.B0.D0.B5.D1.82)
*   [7 ALSA monitor source](#ALSA_monitor_source)
*   [8 Наблюдение конкретного вывода](#.D0.9D.D0.B0.D0.B1.D0.BB.D1.8E.D0.B4.D0.B5.D0.BD.D0.B8.D0.B5_.D0.BA.D0.BE.D0.BD.D0.BA.D1.80.D0.B5.D1.82.D0.BD.D0.BE.D0.B3.D0.BE_.D0.B2.D1.8B.D0.B2.D0.BE.D0.B4.D0.B0)
*   [9 PulseAudio через JACK](#PulseAudio_.D1.87.D0.B5.D1.80.D0.B5.D0.B7_JACK)
    *   [9.1 Новый новый способ](#.D0.9D.D0.BE.D0.B2.D1.8B.D0.B9_.D0.BD.D0.BE.D0.B2.D1.8B.D0.B9_.D1.81.D0.BF.D0.BE.D1.81.D0.BE.D0.B1)
    *   [9.2 Новый способ](#.D0.9D.D0.BE.D0.B2.D1.8B.D0.B9_.D1.81.D0.BF.D0.BE.D1.81.D0.BE.D0.B1)
    *   [9.3 Старый способ](#.D0.A1.D1.82.D0.B0.D1.80.D1.8B.D0.B9_.D1.81.D0.BF.D0.BE.D1.81.D0.BE.D0.B1)
        *   [9.3.1 QjackCtl с скриптами загрузки/выключения](#QjackCtl_.D1.81_.D1.81.D0.BA.D1.80.D0.B8.D0.BF.D1.82.D0.B0.D0.BC.D0.B8_.D0.B7.D0.B0.D0.B3.D1.80.D1.83.D0.B7.D0.BA.D0.B8.2F.D0.B2.D1.8B.D0.BA.D0.BB.D1.8E.D1.87.D0.B5.D0.BD.D0.B8.D1.8F)
*   [10 PulseAudio через OSS](#PulseAudio_.D1.87.D0.B5.D1.80.D0.B5.D0.B7_OSS)
*   [11 Запуск PulseAudio из chroot (напр. 32-бит chroot в 64-битной истеме)](#.D0.97.D0.B0.D0.BF.D1.83.D1.81.D0.BA_PulseAudio_.D0.B8.D0.B7_chroot_.28.D0.BD.D0.B0.D0.BF.D1.80._32-.D0.B1.D0.B8.D1.82_chroot_.D0.B2_64-.D0.B1.D0.B8.D1.82.D0.BD.D0.BE.D0.B9_.D0.B8.D1.81.D1.82.D0.B5.D0.BC.D0.B5.29)
*   [12 Отключение автоматического запуска сервера PulseAudio](#.D0.9E.D1.82.D0.BA.D0.BB.D1.8E.D1.87.D0.B5.D0.BD.D0.B8.D0.B5_.D0.B0.D0.B2.D1.82.D0.BE.D0.BC.D0.B0.D1.82.D0.B8.D1.87.D0.B5.D1.81.D0.BA.D0.BE.D0.B3.D0.BE_.D0.B7.D0.B0.D0.BF.D1.83.D1.81.D0.BA.D0.B0_.D1.81.D0.B5.D1.80.D0.B2.D0.B5.D1.80.D0.B0_PulseAudio)
*   [13 Изменить стерео на моно](#.D0.98.D0.B7.D0.BC.D0.B5.D0.BD.D0.B8.D1.82.D1.8C_.D1.81.D1.82.D0.B5.D1.80.D0.B5.D0.BE_.D0.BD.D0.B0_.D0.BC.D0.BE.D0.BD.D0.BE)
*   [14 Поменять левый/правый каналы](#.D0.9F.D0.BE.D0.BC.D0.B5.D0.BD.D1.8F.D1.82.D1.8C_.D0.BB.D0.B5.D0.B2.D1.8B.D0.B9.2F.D0.BF.D1.80.D0.B0.D0.B2.D1.8B.D0.B9_.D0.BA.D0.B0.D0.BD.D0.B0.D0.BB.D1.8B)
*   [15 PulseAudio as a minimal unintrusive dumb pipe to ALSA](#PulseAudio_as_a_minimal_unintrusive_dumb_pipe_to_ALSA)

## Настройка стандартных устройств ввода

Показать доступные устройства ввода:

 `$ pacmd list-sources | grep -e device.string -e 'name:'` 
```
name: <input>
 device.string = "hw:2"
name: <oss_input.dsp>
 device.string = "/dev/dsp"
name: <alsa_output.pci-0000_04_01.0.analog-stereo.monitor>
name: <combined.monitor>
```

Для постоянного хранения в файле *default.pa*

Выбор OSS как устройство ввода

```
load-module module-oss device=/dev/dsp sink_name=alsa_output.pci-0000_04_01.0.analog-stereo mmap=1

```

Сделать его стандартным

```
set-default-source alsa_output.pci-0000_04_01.0.analog-stereo.monitor

```

Выбор ALSA как устройств ввода

```
load-module module-alsa-source source_name=input device=hw:2

```

Сделать его стандартным

```
set-default-source input

```

Для временного использования

```
$ pacmd "load-module module-alsa-source source_name=input device=hw:2"
$ pacmd "set-default-source input"

```

## Установка стандартного устройтва ввода

**Note:** Используйте 'aplay' чтобы увидеть список всех устройств, которые являются частью пакета [alsa-utils](https://www.archlinux.org/packages/?name=alsa-utils) и не требуют множественного вывода. Это требуется чтобы увидеть список устройств воспоизведения и,следовательно, он может быть удалён,когда вы закончите с этим.

Чтобы выбрать альтернативынй источник звука как стандартный, вы можете получить список всех источников:

 `$ aplay -l | grep card` 
```
card 0: CMI8768 [C-Media CMI8768], device 0: CMI8738-MC8 [C-Media PCI DAC/ADC]
card 0: CMI8768 [C-Media CMI8768], device 1: CMI8738-MC8 [C-Media PCI 2nd DAC]
card 0: CMI8768 [C-Media CMI8768], device 2: CMI8738-MC8 [C-Media PCI IEC958]
card 1: HDMI [HDA Intel HDMI], device 3: HDMI 0 [HDMI 0]
card 1: HDMI [HDA Intel HDMI], device 7: HDMI 1 [HDMI 1]
card 1: HDMI [HDA Intel HDMI], device 8: HDMI 2 [HDMI 2]
```

Чтобы выбрать *card 0, device 0*, измените `/etc/pulse/default.pa`, добавьте load-module module-alsa-sink device=hw:0,0

Определите правильный индекс нового источника:

 `$ pacmd list-sinks | grep -e 'name:' -e 'index'` 
```
  * index: 0
	name: <alsa_output.pci-0000_04_01.0.analog-stereo>
    index: 1
	name: <combined>

```

Для установки его как стандартного в `/etc/pulse/default.pa` вы можете использовть

```
set-default-sink 0

```

Когда вы закончите, можете выйти/войти или перезапустить PulseAudip вручную,чтобы изменения вступили в силу.

**Note:** .

*   Индекс соответствует 'alsa_output.hw_0_0'.
*   Стандартные sink`и помечаются ***** перед индесом .
*   Вы можете использовать индекс для изменения громкости источников:

```
 $ pactl set-sink-volume **0** +3%
 $ pactl set-sink-volume **0** -- -3%
 $ pactl set-sink-mute **0** toggle
```

*   Чтобы избежать ненужных изменений в 100% нормальном звуке, лучше использовать альтернативные утилиты менеджмента звука. См. [arch forum](https://bbs.archlinux.org/viewtopic.php?id=124513) для доп. информации

## Одновременный HDMI и аналоговый вывод

PulseAudio позволяет одновременный вывод в множество источников. В этом примере, некоторые приложения настроены использовать HDMI, в то время как некоторые настроены использовать аналоговый вывод. Отправлять звук можно в несколько приложений сразу.

```
$ aplay -l
**** List of PLAYBACK Hardware Devices ****
card 0: Intel [HDA Intel], device 0: ALC889A Analog [ALC889A Analog]
  Subdevices: 0/1
  Subdevice #0: subdevice #0
card 0: Intel [HDA Intel], device 1: ALC889A Digital [ALC889A Digital]
  Subdevices: 1/1
  Subdevice #0: subdevice #0
card 0: Intel [HDA Intel], device 3: HDMI 0 [HDMI 0]
  Subdevices: 0/1
  Subdevice #0: subdevice #0
```

Или использую команду `pacmd`:

 `$ pacmd list-sinks  | grep -e 'name:'  -e 'alsa.device ' -e 'alsa.subdevice '` 
```
	name: <alsa_output.pci-0000_00_1b.0.analog-stereo>
		alsa.subdevice = "0"
		alsa.device = "0"
```

Главное в файле конфигурации вроде этого - понять, что устройство, выбранное в 'pavucontrol' в *Configuration > Internal Audio* - стандартное. Используйте *pavucontrol > Configuration* и выберите HDMI в качестве профиля.

Чтобы установить аналоговое утройство как вторичное устройство вывода, добавьте следующее в начало конфигурационного фала `/etc/pulse/default.pa`, перед тем, как начнётся загрузка модулей:

```
### Загрузите аналогое устройство
load-module module-alsa-sink device=hw:0,0
load-module module-combine-sink sink_name=combined
set-default-sink combined

```

Перезапустите PulseAudio, запустите *pavucontrol* и выберите пункт "Output Devices". Вы должны увидеть следующие настройки:

1.  Internal Audio Digital Stereo (HDMI)
2.  Internal Audio
3.  Simultaneous output to Internal Audio Digital Stereo (HDMI), Internal Audio

Теперь запустите программу,которая будет использовать PulseAudio, такую как MPlayer, VLC, mpd, и т.д. и переключитесь во вкладку "Воспроизведение". Выпадающий список должен предоставить выбор из трёх устройств.

Так же см. [этот пост](https://bbs.archlinux.org/viewtopic.php?id=118026) и [PulseAudio FAQ](http://www.freedesktop.org/wiki/Software/PulseAudio/FAQ#Can_I_use_PulseAudio_to_playback_music_on_two_sound_cards_simultaneously.3F) для вариаций по этой теме.

## Настройка HDMI вывода

Как выделено в [ftp://download.nvidia.com/XFree86/gpu-hdmi-audio-document/gpu-hdmi-audio.html#_issues_in_pulseaudio](ftp://download.nvidia.com/XFree86/gpu-hdmi-audio-document/gpu-hdmi-audio.html#_issues_in_pulseaudio), пока HDMI порт - первое устройство вывода,PulseAudio не сможет использовать любое другое аудио при использрвании некоторых видеокарт с поддержкой HDMI. Это происходит из-за бага PulseAudio, из-за которого он может выбрать только первый HDMI как устройство вывода. Обход этой проблемы, написан ниже - найти,какой HDMI вывод работает с помощью aply из ALSA.1

Проблема в основном возникает с некоторыми картами от nVidia и некоторыми другими, см. [эту тему на форуме](https://bbs.archlinux.org/viewtopic.php?id=133222)

### Поиск HDMI вывода

Далее найдите рабочий вывод из списка доступных карт

```
# aplay -l

```

```
примерный вывод:
 **** List of PLAYBACK Hardware Devices ****
 card 0: NVidia [HDA NVidia], device 0: ALC1200 Analog [ALC1200 Analog]
   Subdevices: 1/1
   Subdevice #0: subdevice #0
 card 0: NVidia [HDA NVidia], device 3: ALC1200 Digital [ALC1200 Digital]
   Subdevices: 1/1
   Subdevice #0: subdevice #0
 card 1: NVidia_1 [HDA NVidia], device 3: HDMI 0 [HDMI 0]
   Subdevices: 1/1
   Subdevice #0: subdevice #0
 card 1: NVidia_1 [HDA NVidia], device 7: HDMI 0 [HDMI 0]
   Subdevices: 0/1
   Subdevice #0: subdevice #0
 card 1: NVidia_1 [HDA NVidia], device 8: HDMI 0 [HDMI 0]
   Subdevices: 1/1
   Subdevice #0: subdevice #0
 card 1: NVidia_1 [HDA NVidia], device 9: HDMI 0 [HDMI 0]
   Subdevices: 1/1
   Subdevice #0: subdevice #0

```

### Проверка на правильную карту

Теперь, когда у вас есть список карт, пользователям нужно проверить, какая из них выводит на ТВ/Монитор

```
# aplay -D plughw:1,3 /usr/share/sounds/alsa/Front_Right.wav

```

Где 1 - карта, а 3 - устройство-замена в предыдущих разделах. Если звука нет, попробуйте другое устройство-замену (на моей карте пришлось использовать карту 1 устройство 7)

### Ручная настройка PulseAudio,чтобы он находил HDMI Nvidia

Чтобы заставить PulseAudio находить HDMI, нужно отредактировать `/etc/pulse/default.pa`:

```
# load-module module-alsa-sink device=hw:1,7

```

где 1 - карта, а 7 - утсройство,найденное в предыдущем разделе перезапустите pulse audio

```
 $ pulseaudio -k
 $ pulseaudio --start

```

откройте менеджер настройки аудио, убедитесь в том,что во вкладке "hardware" - графическая карта с HDMI установлена как "Digital Stereo (HDMI) Output" (Моя карта также называлась "GF100 High Definition Audio Controller")

Далее, откройте вкладку вывода. Там теперь должно быть вдва выхода HDMI для граф. карты. Проверьте,какая из них работает,выбрав одну,а затем воспроизведите любое аудио,и,если оно не работает,попробуйте другое.

## Настройка объёмного звука

У многих людей есть звукокавая карта с поддержкой объёмного зука, но спикеры у них всего на 2 канала, так что PulseAudio не может выставить звуковую настройку для объёмного звука по умолчанию.Чтобы включить все каналы, измените `/etc/pulse/daemon.conf`: раскомментируйте строку *default-sample-channels* и выставьте значение **6** для **5.1** или **8** для **7.1**и т.д.

```
# Стандартное
default-sample-channels=2
# Для 5.1
default-sample-channels=6
# Для 7.1
default-sample-channels=8

```

Если каналы неправлено назначены или регуляция звука для отдельных каналов в pavucontrol работает неправильно, и у вас есть HDMI и аналоговая звуковая карта, попробуйте добавить эту строку в `/etc/pulse/default.pa`

```
load-module module-combine channels=6 channel_map=front-left,front-right,rear-left,rear-right,front-center,lfe

```

Заметьте,что это пример для 5.1.

После этого перезапустить PulseAudio

### Разделение передний/задний

Подключите устройство к переднему аналоговому выходу и наушники - к заднему. Будет полезно разделить передний/задний порты. Добавьте следующее в {ic|/etc/pulse/default.pa}}:

```
 load-module module-remap-sink sink_name=speakers remix=no master=alsa_output.pci-0000_05_00.0.analog-surround-40 channels=2 master_channel_map=front-left,front-right channel_map=front-left,front-right
 load-module module-remap-sink sink_name=headphones remix=no master=alsa_output.pci-0000_05_00.0.analog-surround-40 channels=2 master_channel_map=rear-left,rear-right channel_map=front-left,front-right

```

Замените alsa_output.pci-0000_05_00.0.analog-surround-40 своей звуковой картой, как показано в 'pacmd list-sinks'. Теперь вы можете испоьзовать их раздельно. Вы можете выбрать 'sink_name' сами, если такого же уже не существует. Параметр 'remix' контролирует, в каком из устройств стоит поднять/опустить стандартный звук.

**Tip:** Если pulseaudio выдаёт ошибку `master sink not found` - закомментируйте строку переназначения, запустите PulseAudio и проверьте, что выход вашей звуковой карты установлен на тот,что вы указали выше (напр. analog surround 4.0). Вы также можете попробовать [sink index](#Set_the_defaulting_output_source) вместо имени.

### Разделение 7.1 на 5.1 + 2.0

По примеру выше,вы также можете поделить 7.1 на 5.1 и стерео. Усановите режим карты на 7.1, затем добавьте эти строки в `/etc/pulse/default.pa`:

```
 load-module module-remap-sink sink_name=Surround remix=no master=alsa_output.pci-0000_00_14.2.analog-surround-71 channels=6 master_channel_map=front-left,front-right,rear-left,rear-right,front-center,lfe channel_map=front-left,front-right,rear-left,rear-right,front-center,lfe
 load-module module-remap-sink sink_name=Stereo remix=yes master=alsa_output.pci-0000_00_14.2.analog-surround-71 channels=2 master_channel_map=front-left,front-right channel_map=front-left,front-right

```

Замените alsa_output.pci-0000_00_14.2 именем своей звуковой карты('pacmd list-sinks'). Эта конфигурация будет использовать передние/задние/центральные+lfe(зелёный/черный/оранжевый) джеки для 5.1 и боковой (серый) джек для стерео. Это также уменьшит любое аудио до стерео для стерео выхода, но не затронет 5.1.

**Tip:** Если pulseaudio выдаёт ошибку `master sink not found` - закомментируйте строку переназначения, запустите PulseAudio и проверьте, что выход вашей звуковой карты установлен на тот,что вы указали выше (напр. analog surround 4.0). Вы также можете попробовать [sink index](#Set_the_defaulting_output_source) вместо имени.

**Note:** `remix=yes` будет работать только если у вас включен `enable-remixing = yes` в `/etc/pulse/daemon.conf` (стандартно).

### LFE ремиксинг

Стандартно, PusleAudio ремиксит каналы default-sample-channels; тем не менее,этого не происходит с LFE каналом. Чтобы включить LFE ремиксинг,раскоментируйте эту строку

```
; enable-lfe-remixing = no

```

и замените no на yes:

```
enable-lfe-remixing = yes

```

затем перезапустите PulseAudio

## PulseAudio через сеть

Одна из уникальных функций PulseAudio - возможность передачи аудио клиентам через TCP к серверу, запущенному PulseAudio демоном в сети.

Чтобы достичь этого, нужно включить module-native-protocol-tcp.

### Поддержка TCP (звук через сеть)

Чтобы включить TCP модуль, добавьте это (или ракомментируйте, если уже есть) в `/etc/pulse/default.pa` на клиенте и сервере:

```
load-module module-native-protocol-tcp

```

Чтобы это работало, клиент и сервер должны разделять общий cookie. Убедитесь, что клиент и сервер разделяют один cookie файл в `~/.config/pulse/cookie`. Не важно, чей файл они используют (клиента/сервера), просто удоствоверьтесь, что это один и тот же файл.

`**Заметка:** Если возникают проблемы с подключением, выполните на сервере *pacmd list-modules*`

### Поддержка TCP с анонимными клиентами

Если копировать каждый cookie файл клиентам слишком долго, анонимные клиенты пошут получать доступ к серверу, если добавить следующий параметр в module-native-protocol-tcp на сервере(в `/etc/pulse/default.pa`):

```
 load-module module-native-protocol-tcp auth-ip-acl=127.0.0.1;192.168.0.0/24 auth-anonymous=1

```

Измените дрес подсети клиента, чтобы они могли подключится.

### Zeroconf (Avahi)

Чтобы удалённый PulseAudio сервер появился в списке устройст PulseAudio (`pasystray`), загрузите нужные подули zeroconf и вкючите [Avahi](/index.php/Avahi "Avahi") [daemon](/index.php/Daemon "Daemon").

На обоих машинах выполните:

```
$ systemctl start avahi-daemon
$ systemctl enable avahi-daemon

```

на сервере, добавьте `load-module module-zeroconf-publish` в `/etc/pulse/default.pa`, на клиенте - `load-module module-zeroconf-discover` в `/etc/pulse/default.pa`. Теперь перенаправляйте любой звук на удалённый PulseAudio сервер,выбрав нужное устройство.

Если вы испытываете проблемы с удалёнными устройствами на клинте, попробуйте перезапустить демона Avahi на сервере и переотправить доступные интерфейсы.

### Переключение PulseAudio сервера ипользуется локальными X клиентами

Чтобы переключатся между серверами на клиенте в пределах X, можно использовать команду `pax11publish`. Например, чтобы переключится со стандартного сервера на хоста foo:

```
$ pax11publish -e -S foo

```

И чтобы вернутся обратно:

```
$ pax11publish -e -r

```

Чтобы это заработало, нужно перезапустить программы использующие Pulse.

### Если всё остальное не работает

`**Внимание:** это не постоянное решение, а временный фикс`

На сервере:

```
 $ paprefs 

```

В Network Access -> Включите доступ к локальным устройствам звука (Также включите 'Allow discover' и 'Don't require authentication').

На клиенте:

```
 $ export PULSE_SERVER=server.ip && mplayer test.mp3

```

## ALSA monitor source

Чтобы иметь возможность записывать из monitor source (a.k.a. "What-U-Hear", "Stereo Mix"), используйте `pactl list` чтобы найти имя источника в PulseAudio (напр.`alsa_output.pci-0000_00_1b.0.analog-stereo.monitor`). Затем добавьте следующие строки в `/etc/asound.conf` или `~/.asoundrc`:

```
pcm.pulse_monitor {
  type pulse
  device alsa_output.pci-0000_00_1b.0.analog-stereo.monitor
}

ctl.pulse_monitor {
  type pulse
  device alsa_output.pci-0000_00_1b.0.analog-stereo.monitor
}

```

Теперь вы можете выбрать `pulse_monitor` как устройство записи.

Как альтернативу, вы можете использовать **pavucontrol**.Чтобы сделать это: убедитесь, что он настроен показывать ВСЕ устройства ввода, затем выберите "Monitor of [ваша звуковая карта]" как устройство записи.

## Наблюдение конкретного вывода

Есть аозможность наблюдать конкретный вывод, например, чтобы стримить аудио из плеера в VOIP-приложение. Просто создайте пустое устройство вывода:

```
pactl load-module module-null-sink sink_name=<имя>

```

В Настройках Звука Pulseaudio (pavucontrol), во вкладе "Playback", измените устройство вывода приложния на <имя>, и во вкладке записи измените устройство ввода приложения на "Monitor of <имя>". Теперь аудио будет поступать из одного приложения в другое.

## PulseAudio через JACK

### Новый новый способ

Эта конфигурация работает только с jackdbus(JACK2 совмещённый с D-Bus пожжержкой). Он также тербует пакет [pulseaudio-jack](https://www.archlinux.org/packages/?name=pulseaudio-jack).Добавьте следующее в `/etc/pulse/default.pa`:

```
load-module module-jackdbus-detect

```

Как описано на странице [Jack-DBUS Packaging](http://trac.jackaudio.org/wiki/JackDbusPackaging):

*Автозапуск сервера реализован как вызов D-Bus, который автоматически запускает JACK D-Bus службу, в случае, если она уже запущена, он запускает JACK сервер.* Правильная воздействие с PulseAudio происходит, используя чере аудио карту,основаннуй на D-Bus механизме "acquire/release".Когда JACK сервер стартует, он просит D-Bus службу получить аудио карту и PulseAudio безоговорочно "отпустит" её. Когда JACK сервер останавливается, он "отпускает" аудио карту и она снова может быть подхвачена PulseAduio.

`module-jackdbus-detect.so` динамически загружает и выгружает module-jack-sink и module-jack-source когда jackdbus стартует/останавливается.

Если звук в PulseAudio не работает, проверьте `pavucontrol` чтобы проверить, появляются ли нужные программы во вкладку playback. Если нет - добавьте следующее в `~/.asound.conf` или `/etc/asound.conf`, чтобы перенаправлять ALSA в PulseAudio:

```
pcm.pulse {
    type pulse
}

ctl.pulse {
    type pulse
}

pcm.!default {
    type pulse
}
ctl.!default {
    type pulse
}

```

Если всё ещё не работает, проверьте `pavucontrol`, во вкладке playback, и удостоверьтесь,что нужные программы выводят звук в PulseAduio JACK вместо вашей звуковой карты.

### Новый способ

Основная идея: аварийно останавливать PulseAduio - плохая идея, это может крашнуть приложения, испльзвующие PulseAudio.

Как работает эта настройка:

1.  PulseAudio отпускает звуковую карту
2.  JACK подзватывает звуковую карту и запускается
3.  Скрипт перенаправляет PulseAudio в JACK
4.  вручную отправлять PulseAudio приложения в JACK вывод (pavucontrol может быть полезным)
5.  использовать JACK программы и т.д.
6.  через скрипт, перестать перенаправлять PulseAudio в JACK
7.  остановить JACK и отпустить звуковую карту
8.  PulseAudio подхватывает звуковую карту и всё работает как обычно

Через QJackCTL, настройте эти скрипты:

`pulse-jack-pre-start.sh` установливает скрипт при загрузке

```
#!/bin/bash
pacmd suspend true

```

`pulse-jack-post-start.sh` устанавливает скрипт после загрузки

```
#!/bin/bash
pactl load-module module-jack-sink channels=2
pactl load-module module-jack-source channels=2
pacmd set-default-sink jack_out
pacmd set-default-source jack_in

```

`pulse-jack-pre-stop.sh` "выполнять при выключении"

```
#!/bin/bash
SINKID=$(pactl list | grep -B 1 "Name: module-jack-sink" | grep Module | sed 's/[^0-9]//g')
SOURCEID=$(pactl list | grep -B 1 "Name: module-jack-source" | grep Module | sed 's/[^0-9]//g')
pactl unload-module $SINKID
pactl unload-module $SOURCEID
sleep 5

```

`pulse-jack-post-stop.sh` "исполнять послы выключения"

```
#!/bin/bash
pacmd suspend false

```

### Старый способ

JACK-Audio-Connection-Kit популярен для аудио работы и широко распростаранён в аудио приложениях для Linux. По функционалу он похож на PulseAudip, но с упором на профессиональную работу с аудио. Ardour and Audacity, например, хорошо работают с Jack.

В PulseAudio есть module-jack-source и module-jack-sink допускает PulseAudio запускаться как звуковой сервер поверх демона JACK. Это позволяет использовать настраивать приложения отдельно, позволяя воспроизводить в приложениях, при этом позволяя приложенияем для работы со звуком подключаться к JACK. Тем не менее, это не даёт PulseAudio записывать напрямую в буфер звуковой карты, увеличивая нагрузку на процессор.

Просто попробуйте запустить PA поверх JACK, пусть PA загрузить нужные модули при старте:

```
pulseaudio -L module-jack-sink -L module-jack-source

```

Чтобы использовать PA с JACK, JACK должен быть запущен перед PulseAUdio, использую метод, который вы предпочтёте. PulseAudio нужно запуститься при этом загрузиа два нужным модулей. Измените `/etc/pulse/default.pa`,и измените следующую область:

```
### Load audio drivers statically (it is probably better to not load
### these drivers manually, but instead use module-hal-detect --
### see below -- for doing this automatically)
#load-module module-alsa-sink
#load-module module-alsa-source device=hw:1,0
#load-module module-oss device="/dev/dsp" sink_name=output source_name=input
#load-module module-oss-mmap device="/dev/dsp" sink_name=output source_name=input
#load-module module-null-sink
#load-module module-pipe-sink

### Automatically load driver modules depending on the hardware available
.ifexists module-udev-detect.so
load-module module-udev-detect
.else
### Alternatively use the static hardware detection module (for systems that
### lack udev support)
load-module module-detect
.endif

```

на следующее:

```
### Load audio drivers statically (it is probably better to not load
### these drivers manually, but instead use module-hal-detect --
### see below -- for doing this automatically)
#load-module module-alsa-sink
#load-module module-alsa-source device=hw:1,0
#load-module module-oss device="/dev/dsp" sink_name=output source_name=input
#load-module module-oss-mmap device="/dev/dsp" sink_name=output source_name=input
#load-module module-null-sink
#load-module module-pipe-sink
load-module module-jack-source
load-module module-jack-sink

### Automatically load driver modules depending on the hardware available
#.ifexists module-udev-detect.so
#load-module module-udev-detect
#.else
### Alternatively use the static hardware detection module (for systems that
### lack udev support)
#load-module module-detect
#.endif

```

Вообще, это предотвращает загрузку module-udev-detect. module-udev-detect будет пытатся захватить звкуовую карту (JACK уже сделал это, так что это приведёт к ошибке). Кстати, источники JACK должны быть явно загружены.

#### QjackCtl с скриптами загрузки/выключения

Использоуя настроки описанные выше, используйте QjackCtl чтобы выполнять скрипты во вреся запуска и выключения PulseAudio. Одной из причин, почему пользователи хотят это использовать - оно выключает автоопределение аппаратуры. Именна эта настройка - для использования PulseAudio с JACK, хотя скрипты и могут быть изменены для загрузки других скриптов кроме JACK.

**Note:** padevchooser в следующем примере устарел. Он заменён pasystray

Следующий пример может быть использован и измененён как скрипт загрузки, который делает PulseAudio демона и загружает *padevchooser* программу (опционално, его можно взять в AUR), которая называется `jack_startup`:

```
#!/bin/bash
#Load PulseAudio and PulseAudio Device Chooser

pulseaudio -D
padevchooser&

```

также как и скрипт выключения останавливает PulseAudio и "Выбор Устройств Pulse Audio", он также вызывает `jack_shutdown` в домашней директории:

```
#!/bin/bash
#Kill PulseAudio and PulseAudio Device Chooser

pulseaudio --kill
killall padevchooser

```

Оба скрипта должны быть сделаны исполняемыми:

```
chmod +x jack_startup jack_shutdown

```

затем, с загруженным QjackCtl, нажмите на кнопку *Setup* и затем вкладку *Options* и поставьте голочки: "Execute Script after Startup:" и "Execute Script on Shutdown:" и установите "use the ... button" или введите путь до скриптов (предпологается, что скрипты находятся в домашней директории) `~/jack_startup` и `~/jack_shutdown`, убедитесь что сохранили всё.

## PulseAudio через OSS

Добавьте следующее в `/etc/pulse/default.pa`:

```
load-module module-oss

```

Затем запустите PulseAudio как обычно, убедитесь что все источники объявлены для OSS усройств.

## Запуск PulseAudio из chroot (напр. 32-бит chroot в 64-битной истеме)

Так как chroot представляет собственный root для запуска приложений, PulseAudio должен быть установлен из самого chroot (`pacman -S pulseaudio` в окружении chroot).

PulseAudio, если не натсроен на подключения к конкретному серверу (это можно сделать в `/etc/pulse/client.conf`, через переменную PULSE_SERVER, или через локальные настройки X11, используя module-x11-publish), будет пытаться подключится к локальному pulse серверу, если у него не получится - он создаст новый. Каждый pulse сервер имеет уникальный ID, основанный на машинно id в `/var/lib/dbus`. Чтобы дать приложениям из chroot доступ к pulse серверу. следующие директории должны быть смонтированный в chroot:-

```
/run
/var/lib/dbus
/tmp
~/config/.pulse

```

`/dev/shm` также должен быть смонтирован для эффективного использования. Заметьте, что монтирования /home также обычно означает разделение `~/.pulse`.

PulseAduio выбирет путь к сокету через XDG_RUNTIME_DIR, так что удостовертесь перенести его тоже, когда используете chroot из-под sudo (см. [Sudo#Environment variables](/index.php/Sudo#Environment_variables "Sudo")).

Также обратите внимание на [additional section](/index.php/Install_bundled_32-bit_system_in_Arch64#Allow_32-bit_applications_access_to_64-bit_PulseAudio "Install bundled 32-bit system in Arch64")

## Отключение автоматического запуска сервера PulseAudio

Некоторые пользователи предпочитают вручную запускать сервер PulseAudio, перед запуском определенных программ, а затем останавливать сервер PulseAudio, когда они завершены. Для достижения такого результата, отредактируйте `/etc/pulse/client.conf` и измените `autospawn = yes` на `autospawn = no`, и установите `daemon-binary = /bin/true`. Убедитесь что обе строки не закомментированы.

 `/etc/pulse/client.conf` 
```
autospawn = no
daemon-binary = /bin/true 

```

Теперь вы можете вручную запустить PulseAudio сервер командой

```
$ pulseaudio --start

```

И остановить его

```
$ pulseaudio --kill

```

Также можете переместить или удалить файл .desktop в `/etc/xdg/autostart` если он существует.

## Изменить стерео на моно

Изменить стерео устройство вывода на моно устройство вывода можно путём создания виртуального устройства вывода. Это будет полезно если у вас только один динамик. Добавьте в `/etc/pulse/default.pa`:

```
load-module module-remap-sink master=alsa_output.pci-0000_00_1f.5.analog-stereo sink_name=mono channels=2 channel_map=mono,mono
# Optional: Select new remap as default
set-default-sink mono

```

(замените имя звуковой карты alsa_output.pci-0000_00_1f.5.analog-stereo показанным в `pacmd list-sinks`)

Переключайтесь между виртуальным моно устройством и настоящим стерео устройством.

## Поменять левый/правый каналы

Поменять местами стерео каналы путём создания виртуального устройства. Добавьте в `/etc/pulse/default.pa`:

```
load-module module-remap-sink sink_name=reverse-stereo master=alsa_output.pci-0000_00_1f.5.analog-stereo channels=2 master_channel_map=front-right,front-left channel_map=front-left,front-right
set-default-sink reverse-stereo

```

(замените alsa_output.pci-0000_00_1f.5.analog-stereo на имя звуковой карты показанной из `pacmd list-sinks`)

[Документация переназначения модуля устройства](http://www.freedesktop.org/wiki/Software/PulseAudio/Documentation/User/Modules/#index12h3)

## PulseAudio as a minimal unintrusive dumb pipe to ALSA

Some people do not want to run PulseAudio all the time for various reasons. This example will turn the full fledged audio server into an unobstrusive dumb pipe to ALSA devices that automatically starts **and** stops itself when done, allowing applications that requires PulseAudio to fully function while not touching any ALSA setting nor setting itself as the default ALSA device.

This configuration tells native PA clients to autospawn the daemon when they need it, then the daemon is configured to autoexit as soon as all clients have disconnected. The daemon itself uses a plain simple static configuration that uses your configured `pcm.!default` ALSA devices and nothing more. No replacement of ALSA's default, no playing with mixer levels, nothing but record/playback. Also make sure [pulseaudio-alsa](https://www.archlinux.org/packages/?name=pulseaudio-alsa) is **not** installed so standard ALSA clients don't default to pulse. `alsamixer` functions properly as well as any other ALSA clients. Also make sure common frameworks like Xine, Gstreamer and Phonon are configured to use ALSA: by default if they detect PulseAudio is installed they will try to use it before ALSA.

 `/etc/pulse/daemon.conf` 
```
# Replace these with the proper values
exit-idle-time = 0 # Exit as soon as unneeded
flat-volumes = yes # Prevent messing with the master volume

```
 `/etc/pulse/client.conf` 
```
# Replace these with the proper values

# Applications that uses PulseAudio *directly* will spawn it,
# use it, and pulse will exit itself when done because of the
# exit-idle-time setting in daemon.conf
autospawn = yes

```
 `/etc/pulse/default.pa` 
```
# Replace the *entire* content of this file with these few lines and
# read the comments

.fail
    # Set tsched=0 here if you experience glitchy playback. This will
    # revert back to interrupt-based scheduling and should fix it.
    #
    # Replace the device= part if you want pulse to use a specific device
    # such as "dmix" and "dsnoop" so it doesn't lock an hw: device.

    # INPUT/RECORD
    load-module module-alsa-source device="default" tsched=1

    # OUTPUT/PLAYBACK
    load-module module-alsa-sink device="default" tsched=1 

    # Accept clients -- very important
    load-module module-native-protocol-unix

.nofail
.ifexists module-x11-publish.so
    # Publish to X11 so the clients know how to connect to Pulse. Will
    # clear itself on unload.
    load-module module-x11-publish
.endif

```