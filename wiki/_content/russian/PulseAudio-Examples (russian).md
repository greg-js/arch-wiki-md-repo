**Состояние перевода:** На этой странице представлен перевод статьи [PulseAudio/Examples](/index.php/PulseAudio/Examples "PulseAudio/Examples"). Дата последней синхронизации: 18 ноября 2017\. Вы можете [помочь](/index.php/ArchWiki_Translation_Team_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "ArchWiki Translation Team (Русский)") синхронизировать перевод, если в английской версии произошли [изменения](https://wiki.archlinux.org/index.php?title=PulseAudio/Examples&diff=0&oldid=497074).

## Contents

*   [1 Настройка стандартных устройств ввода](#.D0.9D.D0.B0.D1.81.D1.82.D1.80.D0.BE.D0.B9.D0.BA.D0.B0_.D1.81.D1.82.D0.B0.D0.BD.D0.B4.D0.B0.D1.80.D1.82.D0.BD.D1.8B.D1.85_.D1.83.D1.81.D1.82.D1.80.D0.BE.D0.B9.D1.81.D1.82.D0.B2_.D0.B2.D0.B2.D0.BE.D0.B4.D0.B0)
*   [2 Установка стандартного устройства вывода](#.D0.A3.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B0_.D1.81.D1.82.D0.B0.D0.BD.D0.B4.D0.B0.D1.80.D1.82.D0.BD.D0.BE.D0.B3.D0.BE_.D1.83.D1.81.D1.82.D1.80.D0.BE.D0.B9.D1.81.D1.82.D0.B2.D0.B0_.D0.B2.D1.8B.D0.B2.D0.BE.D0.B4.D0.B0)
*   [3 Одновременный HDMI и аналоговый вывод](#.D0.9E.D0.B4.D0.BD.D0.BE.D0.B2.D1.80.D0.B5.D0.BC.D0.B5.D0.BD.D0.BD.D1.8B.D0.B9_HDMI_.D0.B8_.D0.B0.D0.BD.D0.B0.D0.BB.D0.BE.D0.B3.D0.BE.D0.B2.D1.8B.D0.B9_.D0.B2.D1.8B.D0.B2.D0.BE.D0.B4)
*   [4 Настройка HDMI вывода](#.D0.9D.D0.B0.D1.81.D1.82.D1.80.D0.BE.D0.B9.D0.BA.D0.B0_HDMI_.D0.B2.D1.8B.D0.B2.D0.BE.D0.B4.D0.B0)
    *   [4.1 Поиск HDMI вывода](#.D0.9F.D0.BE.D0.B8.D1.81.D0.BA_HDMI_.D0.B2.D1.8B.D0.B2.D0.BE.D0.B4.D0.B0)
    *   [4.2 Проверка на правильную карту](#.D0.9F.D1.80.D0.BE.D0.B2.D0.B5.D1.80.D0.BA.D0.B0_.D0.BD.D0.B0_.D0.BF.D1.80.D0.B0.D0.B2.D0.B8.D0.BB.D1.8C.D0.BD.D1.83.D1.8E_.D0.BA.D0.B0.D1.80.D1.82.D1.83)
    *   [4.3 Ручная настройка PulseAudio, чтобы он находил HDMI Nvidia](#.D0.A0.D1.83.D1.87.D0.BD.D0.B0.D1.8F_.D0.BD.D0.B0.D1.81.D1.82.D1.80.D0.BE.D0.B9.D0.BA.D0.B0_PulseAudio.2C_.D1.87.D1.82.D0.BE.D0.B1.D1.8B_.D0.BE.D0.BD_.D0.BD.D0.B0.D1.85.D0.BE.D0.B4.D0.B8.D0.BB_HDMI_Nvidia)
    *   [4.4 Автоматическое переключение звука на HDMI](#.D0.90.D0.B2.D1.82.D0.BE.D0.BC.D0.B0.D1.82.D0.B8.D1.87.D0.B5.D1.81.D0.BA.D0.BE.D0.B5_.D0.BF.D0.B5.D1.80.D0.B5.D0.BA.D0.BB.D1.8E.D1.87.D0.B5.D0.BD.D0.B8.D0.B5_.D0.B7.D0.B2.D1.83.D0.BA.D0.B0_.D0.BD.D0.B0_HDMI)
*   [5 Настройка объёмного звука](#.D0.9D.D0.B0.D1.81.D1.82.D1.80.D0.BE.D0.B9.D0.BA.D0.B0_.D0.BE.D0.B1.D1.8A.D1.91.D0.BC.D0.BD.D0.BE.D0.B3.D0.BE_.D0.B7.D0.B2.D1.83.D0.BA.D0.B0)
    *   [5.1 Разделение передний/задний](#.D0.A0.D0.B0.D0.B7.D0.B4.D0.B5.D0.BB.D0.B5.D0.BD.D0.B8.D0.B5_.D0.BF.D0.B5.D1.80.D0.B5.D0.B4.D0.BD.D0.B8.D0.B9.2F.D0.B7.D0.B0.D0.B4.D0.BD.D0.B8.D0.B9)
    *   [5.2 Разделение 7.1 на 5.1+2.0](#.D0.A0.D0.B0.D0.B7.D0.B4.D0.B5.D0.BB.D0.B5.D0.BD.D0.B8.D0.B5_7.1_.D0.BD.D0.B0_5.1.2B2.0)
    *   [5.3 Отключение ремиксинга LFE](#.D0.9E.D1.82.D0.BA.D0.BB.D1.8E.D1.87.D0.B5.D0.BD.D0.B8.D0.B5_.D1.80.D0.B5.D0.BC.D0.B8.D0.BA.D1.81.D0.B8.D0.BD.D0.B3.D0.B0_LFE)
    *   [5.4 Бинауральные наушники](#.D0.91.D0.B8.D0.BD.D0.B0.D1.83.D1.80.D0.B0.D0.BB.D1.8C.D0.BD.D1.8B.D0.B5_.D0.BD.D0.B0.D1.83.D1.88.D0.BD.D0.B8.D0.BA.D0.B8)
*   [6 PulseAudio через сеть](#PulseAudio_.D1.87.D0.B5.D1.80.D0.B5.D0.B7_.D1.81.D0.B5.D1.82.D1.8C)
    *   [6.1 Поддержка TCP (звук через сеть)](#.D0.9F.D0.BE.D0.B4.D0.B4.D0.B5.D1.80.D0.B6.D0.BA.D0.B0_TCP_.28.D0.B7.D0.B2.D1.83.D0.BA_.D1.87.D0.B5.D1.80.D0.B5.D0.B7_.D1.81.D0.B5.D1.82.D1.8C.29)
    *   [6.2 Поддержка TCP с анонимными клиентами](#.D0.9F.D0.BE.D0.B4.D0.B4.D0.B5.D1.80.D0.B6.D0.BA.D0.B0_TCP_.D1.81_.D0.B0.D0.BD.D0.BE.D0.BD.D0.B8.D0.BC.D0.BD.D1.8B.D0.BC.D0.B8_.D0.BA.D0.BB.D0.B8.D0.B5.D0.BD.D1.82.D0.B0.D0.BC.D0.B8)
    *   [6.3 Zeroconf (Avahi)](#Zeroconf_.28Avahi.29)
    *   [6.4 Переключение PulseAudio сервера используя локальные клиенты Х](#.D0.9F.D0.B5.D1.80.D0.B5.D0.BA.D0.BB.D1.8E.D1.87.D0.B5.D0.BD.D0.B8.D0.B5_PulseAudio_.D1.81.D0.B5.D1.80.D0.B2.D0.B5.D1.80.D0.B0_.D0.B8.D1.81.D0.BF.D0.BE.D0.BB.D1.8C.D0.B7.D1.83.D1.8F_.D0.BB.D0.BE.D0.BA.D0.B0.D0.BB.D1.8C.D0.BD.D1.8B.D0.B5_.D0.BA.D0.BB.D0.B8.D0.B5.D0.BD.D1.82.D1.8B_.D0.A5)
    *   [6.5 Выбор сервера](#.D0.92.D1.8B.D0.B1.D0.BE.D1.80_.D1.81.D0.B5.D1.80.D0.B2.D0.B5.D1.80.D0.B0)
    *   [6.6 Если всё остальное не работает](#.D0.95.D1.81.D0.BB.D0.B8_.D0.B2.D1.81.D1.91_.D0.BE.D1.81.D1.82.D0.B0.D0.BB.D1.8C.D0.BD.D0.BE.D0.B5_.D0.BD.D0.B5_.D1.80.D0.B0.D0.B1.D0.BE.D1.82.D0.B0.D0.B5.D1.82)
*   [7 ALSA monitor source](#ALSA_monitor_source)
*   [8 Наблюдение конкретного вывода](#.D0.9D.D0.B0.D0.B1.D0.BB.D1.8E.D0.B4.D0.B5.D0.BD.D0.B8.D0.B5_.D0.BA.D0.BE.D0.BD.D0.BA.D1.80.D0.B5.D1.82.D0.BD.D0.BE.D0.B3.D0.BE_.D0.B2.D1.8B.D0.B2.D0.BE.D0.B4.D0.B0)
*   [9 PulseAudio через JACK](#PulseAudio_.D1.87.D0.B5.D1.80.D0.B5.D0.B7_JACK)
    *   [9.1 Метод KXStudio](#.D0.9C.D0.B5.D1.82.D0.BE.D0.B4_KXStudio)
    *   [9.2 Ручная настройка устройств вывода](#.D0.A0.D1.83.D1.87.D0.BD.D0.B0.D1.8F_.D0.BD.D0.B0.D1.81.D1.82.D1.80.D0.BE.D0.B9.D0.BA.D0.B0_.D1.83.D1.81.D1.82.D1.80.D0.BE.D0.B9.D1.81.D1.82.D0.B2_.D0.B2.D1.8B.D0.B2.D0.BE.D0.B4.D0.B0)
    *   [9.3 Настройка с помощью скриптов](#.D0.9D.D0.B0.D1.81.D1.82.D1.80.D0.BE.D0.B9.D0.BA.D0.B0_.D1.81_.D0.BF.D0.BE.D0.BC.D0.BE.D1.89.D1.8C.D1.8E_.D1.81.D0.BA.D1.80.D0.B8.D0.BF.D1.82.D0.BE.D0.B2)
    *   [9.4 Путем остановки PulseAudio](#.D0.9F.D1.83.D1.82.D0.B5.D0.BC_.D0.BE.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B8_PulseAudio)
*   [10 PulseAudio через OSS](#PulseAudio_.D1.87.D0.B5.D1.80.D0.B5.D0.B7_OSS)
*   [11 Запуск PulseAudio из chroot (напр. 32-бит chroot в 64-битной истеме)](#.D0.97.D0.B0.D0.BF.D1.83.D1.81.D0.BA_PulseAudio_.D0.B8.D0.B7_chroot_.28.D0.BD.D0.B0.D0.BF.D1.80._32-.D0.B1.D0.B8.D1.82_chroot_.D0.B2_64-.D0.B1.D0.B8.D1.82.D0.BD.D0.BE.D0.B9_.D0.B8.D1.81.D1.82.D0.B5.D0.BC.D0.B5.29)
*   [12 Отключение автоматического запуска сервера PulseAudio](#.D0.9E.D1.82.D0.BA.D0.BB.D1.8E.D1.87.D0.B5.D0.BD.D0.B8.D0.B5_.D0.B0.D0.B2.D1.82.D0.BE.D0.BC.D0.B0.D1.82.D0.B8.D1.87.D0.B5.D1.81.D0.BA.D0.BE.D0.B3.D0.BE_.D0.B7.D0.B0.D0.BF.D1.83.D1.81.D0.BA.D0.B0_.D1.81.D0.B5.D1.80.D0.B2.D0.B5.D1.80.D0.B0_PulseAudio)
*   [13 Отключение демона pulseaudio полностью](#.D0.9E.D1.82.D0.BA.D0.BB.D1.8E.D1.87.D0.B5.D0.BD.D0.B8.D0.B5_.D0.B4.D0.B5.D0.BC.D0.BE.D0.BD.D0.B0_pulseaudio_.D0.BF.D0.BE.D0.BB.D0.BD.D0.BE.D1.81.D1.82.D1.8C.D1.8E)
*   [14 Изменить стерео на моно](#.D0.98.D0.B7.D0.BC.D0.B5.D0.BD.D0.B8.D1.82.D1.8C_.D1.81.D1.82.D0.B5.D1.80.D0.B5.D0.BE_.D0.BD.D0.B0_.D0.BC.D0.BE.D0.BD.D0.BE)
*   [15 Поменять левый/правый каналы](#.D0.9F.D0.BE.D0.BC.D0.B5.D0.BD.D1.8F.D1.82.D1.8C_.D0.BB.D0.B5.D0.B2.D1.8B.D0.B9.2F.D0.BF.D1.80.D0.B0.D0.B2.D1.8B.D0.B9_.D0.BA.D0.B0.D0.BD.D0.B0.D0.BB.D1.8B)
*   [16 PulseAudio в качестве ненавязчивого проводника ALSA](#PulseAudio_.D0.B2_.D0.BA.D0.B0.D1.87.D0.B5.D1.81.D1.82.D0.B2.D0.B5_.D0.BD.D0.B5.D0.BD.D0.B0.D0.B2.D1.8F.D0.B7.D1.87.D0.B8.D0.B2.D0.BE.D0.B3.D0.BE_.D0.BF.D1.80.D0.BE.D0.B2.D0.BE.D0.B4.D0.BD.D0.B8.D0.BA.D0.B0_ALSA)
*   [17 Наушники и колонки подключены одновременно и переключаются приложением на лету](#.D0.9D.D0.B0.D1.83.D1.88.D0.BD.D0.B8.D0.BA.D0.B8_.D0.B8_.D0.BA.D0.BE.D0.BB.D0.BE.D0.BD.D0.BA.D0.B8_.D0.BF.D0.BE.D0.B4.D0.BA.D0.BB.D1.8E.D1.87.D0.B5.D0.BD.D1.8B_.D0.BE.D0.B4.D0.BD.D0.BE.D0.B2.D1.80.D0.B5.D0.BC.D0.B5.D0.BD.D0.BD.D0.BE_.D0.B8_.D0.BF.D0.B5.D1.80.D0.B5.D0.BA.D0.BB.D1.8E.D1.87.D0.B0.D1.8E.D1.82.D1.81.D1.8F_.D0.BF.D1.80.D0.B8.D0.BB.D0.BE.D0.B6.D0.B5.D0.BD.D0.B8.D0.B5.D0.BC_.D0.BD.D0.B0_.D0.BB.D0.B5.D1.82.D1.83)
*   [18 Одновременное использование PulseAudio несколькими пользователями](#.D0.9E.D0.B4.D0.BD.D0.BE.D0.B2.D1.80.D0.B5.D0.BC.D0.B5.D0.BD.D0.BD.D0.BE.D0.B5_.D0.B8.D1.81.D0.BF.D0.BE.D0.BB.D1.8C.D0.B7.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D0.B5_PulseAudio_.D0.BD.D0.B5.D1.81.D0.BA.D0.BE.D0.BB.D1.8C.D0.BA.D0.B8.D0.BC.D0.B8_.D0.BF.D0.BE.D0.BB.D1.8C.D0.B7.D0.BE.D0.B2.D0.B0.D1.82.D0.B5.D0.BB.D1.8F.D0.BC.D0.B8)

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

Чтобы установить их как устройства по умолчанию для всей системы, добавьте названия источников в файл /etc/pulse/default.pa

```
set-default-source alsa_output.pci-0000_04_01.0.analog-stereo.monitor

```

Для временного использования

```
$ pacmd "set-default-source alsa_output.pci-0000_04_01.0.analog-stereo.monitor"

```

**Tip:** При использовании в командах, имя устройства по умолчанию может быть заменено как `@DEFAULT_SOURCE@`, например: `$ pactl set-source-mute @DEFAULT_SOURCE@ toggle`.

## Установка стандартного устройства вывода

Определите правильное имя нового источника, который содержит * в начале индекса:

 `$ pacmd list-sinks | grep -e 'name:' -e 'index'` 
```
  * index: 0
	name: <alsa_output.pci-0000_04_01.0.analog-stereo>
    index: 1
	name: <combined>

```

Для установки его как устройства по умолчанию для всей системы, добавьте следующее в /etc/pulse/default.pa

```
set-default-sink alsa_output.pci-0000_04_01.0.analog-stereo

```

Когда вы закончите, можете выйти/войти в систему или перезапустить PulseAudio вручную, чтобы изменения вступили в силу.

**Примечание:**

*   Устройства вывода, которые установлены по умолчанию отмечены `*` в начале индекса.
*   Нумерация устройств вывода не гарантируется быть постоянной, поэтому все устройства вывода в файле `default.pa` должны быть идентифицированы по имени.
*   Для быстрой идентификации во время выполнения (например, для управления громкости звука), вы можете использовать индекс устройства вывода вместо имени устройства вывода:
    ```
    $ pactl set-sink-volume 0 +3%
    $ pactl set-sink-volume 0 -- -3%
    $ pactl set-sink-mute 0 toggle

    ```

*   Чтобы избежать ненужных изменений в 100% нормальном звуке, лучше использовать альтернативные утилиты менеджмента звука. См. [тему на форуме (Англ.)](https://bbs.archlinux.org/viewtopic.php?id=124513) для доп. информации

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

Или используя команду `pacmd`:

 `$ pacmd list-sinks  | grep -e 'name:'  -e 'alsa.device ' -e 'alsa.subdevice '` 
```
	name: <alsa_output.pci-0000_00_1b.0.analog-stereo>
		alsa.subdevice = "0"
		alsa.device = "0"
```

Главное в файле конфигурации вроде этого - понять, что устройство, выбранное в pavucontrol в *Configuration > Internal Audio* - стандартное. Используйте *pavucontrol > Configuration* и выберите HDMI в качестве профиля.

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

Теперь запустите программу, которая будет использовать PulseAudio, такую как MPlayer, VLC, mpd, и т.д. и переключитесь во вкладку "Воспроизведение". Выпадающий список должен предоставить выбор из трёх устройств.

Так же см. [этот пост](https://bbs.archlinux.org/viewtopic.php?id=118026) и [PulseAudio FAQ](http://www.freedesktop.org/wiki/Software/PulseAudio/FAQ#Can_I_use_PulseAudio_to_playback_music_on_two_sound_cards_simultaneously.3F) для вариаций по этой теме.

## Настройка HDMI вывода

Как выделено в [ftp://download.nvidia.com/XFree86/gpu-hdmi-audio-document/gpu-hdmi-audio.html#_issues_in_pulseaudio](ftp://download.nvidia.com/XFree86/gpu-hdmi-audio-document/gpu-hdmi-audio.html#_issues_in_pulseaudio), пока HDMI порт - первое устройство вывода, PulseAudio не сможет использовать любое другое аудио при использовании некоторых видеокарт с поддержкой HDMI. Это происходит из-за бага PulseAudio, из-за которого он может выбрать только первый HDMI, как устройство вывода. Обход этой проблемы, написан ниже - найти, какой HDMI вывод работает с помощью aplay из ALSA.

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

### Ручная настройка PulseAudio, чтобы он находил HDMI Nvidia

Чтобы заставить PulseAudio находить HDMI, нужно отредактировать `/etc/pulse/default.pa`:

```
# load-module module-alsa-sink device=hw:1,7

```

где 1 - карта, а 7 - устройство,найденное в предыдущем разделе перезапустите pulse audio

```
 $ pulseaudio -k
 $ pulseaudio --start

```

откройте менеджер настройки аудио, убедитесь в том, что во вкладке "hardware" - графическая карта с HDMI установлена как "Digital Stereo (HDMI) Output" (Моя карта называлась "GF100 High Definition Audio Controller")

Далее, откройте вкладку вывода. Теперь там должно быть два выхода HDMI для графической карты. Проверьте, какой работает, выбрав один из них, а затем воспроизведите любое аудио. Например, запустите фильм с помощью VLC, и если выход не работает, выберите следующий.

### Автоматическое переключение звука на HDMI

Создайте скрипт для переключения на желаемый профиль при присоединении кабеля HDMI:

 `/usr/local/bin/hdmi_sound_toggle.sh` 
```
#!/bin/bash
USER_NAME=$(w -hs | awk -v vt=tty$(fgconsole) '$0 ~ vt {print $1}')
USER_ID=$(id -u "$USER_NAME")
HDMI_STATUS=$(</sys/class/drm/card0/*HDMI*/status)

export PULSE_SERVER="unix:/run/user/"$USER_ID"/pulse/native"

if [[ $HDMI_STATUS == connected ]]
then
   sudo -u "$USER_NAME" pactl --server "$PULSE_SERVER" set-card-profile 0 output:hdmi-stereo+input:analog-stereo
else
   sudo -u "$USER_NAME" pactl --server "$PULSE_SERVER" set-card-profile 0 output:analog-stereo+input:analog-stereo
fi

```

Сделайте скрипт исполняемым:

```
chmod +x /usr/local/bin/hdmi_sound_toggle.sh

```

Создайте правило [udev](/index.php/Udev_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Udev (Русский)") для запуска этого сценария, когда статус HDMI изменится:

**Примечание:** правило udev не может напрямую запустить скрипт, обойдите это воспользовавшись .service для запуска скрипта
 `/etc/udev/rules.d/99-hdmi_sound.rules`  `KERNEL=="card0", SUBSYSTEM=="drm", ACTION=="change", RUN+="/usr/bin/systemctl start hdmi_sound_toggle.service"` 

И, наконец, создайте файл .service требуемый правилом udev:

 `/etc/systemd/system/hdmi_sound_toggle.service` 
```
[Unit]
Description=hdmi sound hotplug

[Service]
Type=simple
RemainAfterExit=no
ExecStart=/usr/local/bin/hdmi_sound_toggle.sh

[Install]
WantedBy=multi-user.target
```

Для того чтобы внесённые изменения вступили в силу, не забудьте перезагрузить правила udev:

```
udevadm control --reload-rules

```

Также, вам необходимо перезагрузить компоненты systemd.

```
systemctl daemon-reload

```

Может потребоваться перезагрузка.

## Настройка объёмного звука

У многих людей есть звуковая карта с поддержкой объёмного звука, но устройства воспроизведения поддерживают только 2 канала. PulseAudio не может выставить звуковую настройку для объёмного звука по умолчанию. Чтобы включить все каналы, измените `/etc/pulse/daemon.conf`: раскомментируйте строку default-sample-channels и выставьте значение **6** для *5.1* или **8** для *7.1* и т.д.

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

Обратите внимание, что это пример для настройки 5.1.

После этого перезапустите PulseAudio

### Разделение передний/задний

Подключите устройство к переднему аналоговому выходу и наушники - к заднему. Будет полезно разделить передний/задний устройства вывода. Добавьте следующее в `/etc/pulse/default.pa`:

```
 load-module module-remap-sink sink_name=speakers remix=no master=alsa_output.pci-0000_05_00.0.analog-surround-40 channels=2 master_channel_map=front-left,front-right channel_map=front-left,front-right
 load-module module-remap-sink sink_name=headphones remix=no master=alsa_output.pci-0000_05_00.0.analog-surround-40 channels=2 master_channel_map=rear-left,rear-right channel_map=front-left,front-right

```

Убедитесь, что заменили alsa_output.pci-0000_05_00.0.analog-surround-40 названием своей звуковой картой, которое можно увидеть в 'pacmd list-sinks'. Теперь у вас есть 2 дополнительных устройства вывода, которые можно использовать раздельно. Вы можете подобрать название 'sink_name' сами, важно, чтобы оно не совпадало с существующими именами. Параметр 'remix' контролирует, в каком из устройств стоит поднять/опустить стандартный звук для совпадением с каналами устройств вывода.

**Совет:** Если pulseaudio выдаёт ошибку `master sink not found` - закомментируйте строку переназначения, запустите PulseAudio и проверьте, что выход вашей звуковой карты установлен на тот, что вы указали выше (напр. analog surround 4.0). Вы также можете попробовать [номер устройства вывода](#Set_the_default_output_source) вместо имени.

### Разделение 7.1 на 5.1+2.0

По примеру выше, вы также можете поделить 7.1 на 5.1 и стерео. Установите режим карты на 7.1, затем добавьте эти строки в `/etc/pulse/default.pa`:

```
 load-module module-remap-sink sink_name=Surround remix=no master=alsa_output.pci-0000_00_14.2.analog-surround-71 channels=6 master_channel_map=front-left,front-right,rear-left,rear-right,front-center,lfe channel_map=front-left,front-right,rear-left,rear-right,front-center,lfe
 load-module module-remap-sink sink_name=Stereo remix=yes master=alsa_output.pci-0000_00_14.2.analog-surround-71 channels=2 master_channel_map=front-left,front-right channel_map=front-left,front-right

```

Убедитесь, что заменили alsa_output.pci-0000_00_14.2 именем своей звуковой карты, которое можно получить, запустив 'pacmd list-sinks'. Эта конфигурация будет использовать передние/задние/центральные+lfe(зелёный/черный/оранжевый) разъемы для 5.1 и боковой (серый) разъем для стерео. Это также уменьшит любое аудио до стерео для стерео выхода, но не затронет 5.1.

**Совет:** Если pulseaudio выдаёт ошибку `master sink not found` - закомментируйте строку переназначения, запустите PulseAudio и проверьте, что выход вашей звуковой карты установлен на тот, что вы указали выше (напр. analog surround 4.0). Вы также можете попробовать [номер устройства вывода](#Set_the_default_output_source) вместо имени.

### Отключение ремиксинга LFE

По умолчанию, PusleAudio преобразует число каналов в соответствии с default-sample-channels и, начиная с версии 7, также преобразует канал LFE. Если вы хотите отключить преобразование LFE, раскомментируйте строку:

```
; enable-lfe-remixing = yes

```

и замените yes на no :

```
enable-lfe-remixing = no

```

затем перезапустите PulseAudio.

### Бинауральные наушники

[ladspa-bs2b](https://aur.archlinux.org/packages/ladspa-bs2b/) предоставляет плагин для симуляции объемного стереозвучания в наушниках. Для его использования найдите свои наушники с помощью команды:

 `$ pacmd list-sinks | grep -e 'name:'` 
```
	name: <alsa_output.pci-0000_00_1b.0.iec958-ac3-surround-51>
	name: <alsa_output.pci-0000_00_1b.0.iec958-ac3-surround-51.equalizer>
	name: <bluez_sink.00_1F_82_28_93_51>

```

Загрузите плагин (*новое* sink_name задается произвольно, master=*название устройства вывода (наушников)*):

```
pacmd load-module module-ladspa-sink sink_name=binaural master=bluez_sink.00_1F_82_28_93_51 plugin=bs2b label=bs2b control=700,4.5

```

Используйте [pavucontrol](https://www.archlinux.org/packages/?name=pavucontrol) для передачи потока на новое устройство вывода или:

```
pactl move-sink-input $INPUTID $BINAURALSINKNAME

```

## PulseAudio через сеть

Одна из уникальных функций PulseAudio - возможность передачи аудио от клиентов через TCP к серверу, запущенному PulseAudio демоном в локальной сети. Убедитесь, что серверная и клиентская системы синхронизированы по времени (например, посредством NTP), в противном случае аудио поток будет 'заикаться' или вовсе не работать.

Чтобы сделать это доступным, нужно включить module-native-protocol-tcp.

### Поддержка TCP (звук через сеть)

Чтобы включить TCP модуль, добавьте это (или раскомментируйте, если уже есть) в `/etc/pulse/default.pa` на клиенте и сервере:

```
load-module module-native-protocol-tcp

```

Чтобы это работало, клиент и сервер должны разделять общий cookie. Убедитесь, что клиент и сервер разделяют один cookie файл в `~/.config/pulse/cookie`. Не важно, чей файл они используют (клиента/сервера), просто удостоверьтесь, что это один и тот же файл.

Обратите внимание, если с подключением возникают проблемы, используйте (на сервере)

```
pacmd list-modules

```

### Поддержка TCP с анонимными клиентами

Если отсутствует возможность копировать cookie файл с клиентских машин, анонимные клиенты могут получить доступ к серверу, если добавить следующий параметр в module-native-protocol-tcp на сервере(снова в `/etc/pulse/default.pa`):

```
 load-module module-native-protocol-tcp auth-ip-acl=127.0.0.1;192.168.0.0/24 auth-anonymous=1

```

Измените LAN IP подсети для клиентов, которым вы желаете предоставить доступ.

### Zeroconf (Avahi)

Чтобы удалённый PulseAudio сервер появился в списке устройств PulseAudio Device Chooser (`pasystray`), загрузите нужные модули zeroconf и включите [Avahi](/index.php/Avahi "Avahi") [daemon](/index.php/Daemons_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Daemons (Русский)").

Установите на клиенте и сервере `pulseaudio-zeroconf`.

На обеих машинах [запустите](/index.php/Systemd_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#.D0.98.D1.81.D0.BF.D0.BE.D0.BB.D1.8C.D0.B7.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D0.B5_.D1.8E.D0.BD.D0.B8.D1.82.D0.BE.D0.B2 "Systemd (Русский)") и [включите](/index.php/Systemd_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#.D0.98.D1.81.D0.BF.D0.BE.D0.BB.D1.8C.D0.B7.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D0.B5_.D1.8E.D0.BD.D0.B8.D1.82.D0.BE.D0.B2 "Systemd (Русский)") systemd юнит `avahi-daemon`.

На сервере добавьте `load-module module-zeroconf-publish` в файл `/etc/pulse/default.pa`, на клиенте - `load-module module-zeroconf-discover` в `/etc/pulse/default.pa`. Теперь перенаправьте любой поток или весь аудио выход на удаленный сервер PulseAudio, выбрав соответствующее устройство вывода.

Если вы испытываете проблемы с удаленной синхронизацией на клиентской машине, попробуйте перезапустить демон Avahi на сервере, чтобы переотправить доступные интерфейсы.

### Переключение PulseAudio сервера используя локальные клиенты Х

Чтобы переключатся между серверами на клиенте в пределах X, можно использовать команду `pax11publish`. Например, чтобы переключится со стандартного сервера на хост foo:

```
$ pax11publish -e -S foo

```

И чтобы вернутся обратно:

```
$ pax11publish -e -r

```

Это отредактирует переменные PulseAudio в корневом окне X11, что сообщит клиентским библиотекам PulseAudio о том, что нужно соединяться с сервером PulseAudio, а не с `localhost`, вместо того чтобы заставлять сервер PulseAudio вещать аудио (как описано выше). Таким образом, программы больше не будут взаимодействовать с локальным процессом `pulseaudio`, который затем может быть [остановлен](/index.php/Systemd_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#.D0.98.D1.81.D0.BF.D0.BE.D0.BB.D1.8C.D0.B7.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D0.B5_.D1.8E.D0.BD.D0.B8.D1.82.D0.BE.D0.B2 "Systemd (Русский)"). Такие программы, как `pactl`, `pacmd` или `pavucontrol` также необходимо будет запустить с соответствующим `PULSE_SERVER` окружением/переменным X, для управления удалённым сервером PulseAudio.

Обратите внимание, что переключение станет заметным, когда программы использующие Pulse будут перезапущены, или их клиентская библиотека PulseAudio переинициализирована (может быть достаточно полной остановки и перезапуска воспроизведения). Для того чтобы эти изменения оставались постоянными, отредактируйте `default-server` в `~/.config/pulse/client.conf` или `/etc/pulse/client.conf`.

### Выбор сервера

Запустите программу PulseAudio Volume Control `pavucontrol`. Во вкладке **Устройства вывода** вы должны увидеть список локальных и удаленных устройств вывода. На вкладке **Проигрывание**, слева от кнопки "X" Заглушить звук (Mute Audio), вы должны увидеть выпадающий список устройств вывода. Список содержит доступные устройства вывода, и в нем выделено текущее устройство. Переключение устройства вывода позволит аудиопотоку сменить сервер PulseAudio, связанный с этим устройством. Данное управление остается неясным до самого момента его использования, и является особенно полезным при работы с удаленным автономным звуковым сервером.

Аналогично, на вкладке **Устройства ввода** отображены локальные и удаленные устройства ввода. И на вкладке **Запись** расположен выпадающий список, содержащий доступные устройства ввода.

Для направления аудиопотока, запускайте `pavucontrol` локально или на удаленной машине, в зависимости от его связей. Например, запускайте `pavucontrol` на удаленной машине для направления аудио вывода на локальную. И запускайте `pavucontrol` локально для направления аудио вывода на удаленную машину.

С настройкой одновременных выводов или вводов дело обстоит иначе. Для этого ознакомьтесь с информацией о "monitor" и "module-combine-sink".

### Если всё остальное не работает

Это НЕ постоянное решение, лишь временное исправление проблемы

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

Есть возможность наблюдать конкретный вывод, например, чтобы передавать аудио из плеера в VOIP-приложение. Просто создайте пустое устройство вывода:

```
pactl load-module module-null-sink sink_name=<имя>

```

В Настройках Звука Pulseaudio (pavucontrol), во вкладе "Playback", измените устройство вывода приложния на <имя>, и во вкладке записи измените устройство ввода приложения на "Monitor of <имя>". Теперь аудио будет поступать из одного приложения в другое.

## PulseAudio через JACK

[JACK Audio Connection Kit](/index.php/JACK_Audio_Connection_Kit "JACK Audio Connection Kit") популярен для работы со звуком и широко поддерживается аудиоприложениями Linux. Он занимает совместную с PulseAudio нишу, но с акцентом в сторону профессиональной работы со звуком. Он может предложить аудиомониторинг с низкой временной задержкой вместе с большим контролем за вводом и выводом множественных звуковых устройств ввода-вывода.

### Метод KXStudio

Это рекомендуемый способ, так как он был [официально одобрен разработчиками JACK](https://github.com/jackaudio/jackaudio.github.com/wiki/WalkThrough_User_PulseOnJack)

Эта настройка работает с обоими пакетами [jack2-dbus](https://www.archlinux.org/packages/?name=jack2-dbus) и [jack2](https://www.archlinux.org/packages/?name=jack2).

В текущий момент JACK обладает способностью переключаться между ALSA, PulseAudio и JACK. Это дает вам возможность одновременно запускать JACK и PulseAudio и получать их вывод без каких-либо дополнительных настроек или команд терминала.

Перед началом последующих действий рекомендуется удалить пакет [qjackctl](https://www.archlinux.org/packages/?name=qjackctl), если вы его используете.

Начните с установки [cadence](https://aur.archlinux.org/packages/cadence/) из AUR. Как только вы установите и запустите его, в нижнем правом углу экрана должен появиться JACK bridge configuration. ALSA audio bridge следует настроить как ALSA -> PulseAudio -> JACK и включить PulseAudio bridge. Убедитесь с помощью `pavucontrol`, что все устройства ввода и вывода, не относящиеся к JACK, выключены (muted). Воспользуйтесь кнопкой Force Restart для запуска JACK, и, если все запустилось успешно, вывод программ PulseAudio будет перенаправлен через JACK.

### Ручная настройка устройств вывода

Этот способ позволяет обеспечить одновременную работу JACK и PulseAudio и обмен выводом между собой. В этом случае используется ручная настройка систем, которая обеспечивает связь между JACK и PulseAudio. Эта конфигурация не опирается на скрипты или команды, и полностью основана на работе с настройками.

Рассматриваемый метод работает только с jackdbus (JACK2 скомпилированный с поддержкой D-Bus). Вам также потребуется пакет [pulseaudio-jack](https://www.archlinux.org/packages/?name=pulseaudio-jack). Убедитесь, что файл `/etc/pulse/default.pa` содержит строку:

```
load-module module-jackdbus-detect *options*

```

Где `*options*` может быть любой опцией, поддерживаемой этим модулем, обычно `channels=2`.

Как описано на странице [Jack-DBUS Packaging](https://github.com/jackaudio/jackaudio.github.com/wiki/JackDbusPackaging):

*Автозапуск сервера реализован в качестве вызова D-Bus, который автоматически активирует сервис JACK D-Bus, если он еще не был запущен, и запускает сервер JACK. Правильное взаимодействие с PulseAudio обеспечивается механизмом "получения/отдачи" ("acquire/release") звуковой карты, основанным на D-Bus. Когда запускается сервер JACK, он запрашивает получение звуковой карты у данного D-Bus сервиса, и PulseAudio безоговорочно отдает управление над ней. В тот момент, когда сервер JACK заканчивает свою работу, он освобождает звуковую карту, которая вновь может быть занята PulseAudio.*

`module-jackdbus-detect.so` динамически загружает и выгружает модули module-jack-sink и module-jack-source, когда jackdbus запускается и останавливается.

Если PulseAudio не работает, проверьте с помощью `pavucontrol`, появились ли соответствующие программы на вкладке воспроизведения. Если нет, то добавьте следующее в файл `~/.asoundrc` или `/etc/asound.conf` для перенаправления ALSA на PulseAudio:

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

В случае, если он все также не работает, проверьте с помощью `pavucontrol` вкладку воспроизведения и убедитесь, что соответствующие программы осуществляют вывод через PulseAudio JACK Sink, а не через звуковую карту (которую в текущий момент контролирует JACK, и это не сработает). Также убедитесь, что на графике JACK PulseAudio JACK Source соединен с системным аудио выходом.

### Настройка с помощью скриптов

Этот способ позволяет JACK и PulseAudio осуществлять вывод одновременно. Основной упор здесь делается на использование скриптов, автоматически запускаемых QJackCTL, для управления особенностями поведения устройств вывода JACK и PulseAudio.

Идея данного подхода строится на том, что прерывание PulseAudio - это плохо, так как может повлечь за собой аварийную остановку приложений, которые используют PulseAudio, и сломать весь вывод звука в целом.

Пошагово наши действия можно расписать так:

1.  PulseAudio освобождает звуковую карту
2.  запускается JACK и принимает управление звуковой картой на себя
3.  скрипт перенаправляет PulseAudio на JACK
4.  приложения PulseAudio вручную направляются на вывод JACK (pavucontrol может помочь справится с данной задачей)
5.  используются требуемые приложения JACK
6.  скриптом происходит остановка перенаправления PulseAudio на JACK
7.  останавливается JACK и освобождается звуковая карта
8.  PulseAudio возвращает управление звуковой картой и перенаправляет звук на нее напрямую

С помощью QJackCTL настройте следующие скрипты:

`pulse-jack-pre-start.sh` скрипт должен быть настроен как исполняемый и выполняться из скрипта запуска системы

```
#!/bin/bash
pacmd suspend true

```

`pulse-jack-post-start.sh` также нужно сделать исполняемым и выполнять после запуска системы

```
#!/bin/bash
pactl load-module module-jack-sink channels=2
pactl load-module module-jack-source channels=2
pacmd set-default-sink jack_out
pacmd set-default-source jack_in

```

`pulse-jack-pre-stop.sh` "должен выполняться при выключении системы"

```
#!/bin/bash
SINKID=$(pactl list | grep -B 1 "Name: module-jack-sink" | grep Module | sed 's/[^0-9]//g')
SOURCEID=$(pactl list | grep -B 1 "Name: module-jack-source" | grep Module | sed 's/[^0-9]//g')
pactl unload-module $SINKID
pactl unload-module $SOURCEID
sleep 5

```

`pulse-jack-post-stop.sh` "должен выполняться после выключения системы"

```
#!/bin/bash
pacmd suspend false

```

### Путем остановки PulseAudio

Этот способ основывается на скрипте, который автоматически прерывает выполнение PulseAudio, когда запускается JACK, и автоматически запускает PulseAudio, когда JACK завершает работу. Такой подход дает выигрыш в производительности за счет меньшей нагрузки на ЦПУ, в отличии от вариантов, в которых запущены обе программы. Но он может приводить к ошибкам в запущенных приложениях, использующих PulseAudio, и не позволяет осуществлять одновременный вывод (с JACK и PulseAudio).

При использовании предыдущего метода, применяется QjackCtl для выполнения скриптов загрузки/выгрузки PulseAudio во время запуска и остановки системы. Это приводит к выключению модулей PulseAudio, которые отвечают за автоматическое распознавание аппаратных устройств, и может стать одной из причин, по которой пользователи могут захотеть воспользоваться текущим вариантом. Рассматриваемая настройка подготовлена для связки PulseAudio и JACK, хотя и может быть изменена для загрузки/выгрузки иных не-JACK конфигураций, но корректный запуск/остановка PulseAudio при использовании его программами может стать проблемой.

**Примечание:** padevchooser в следующем примере устарел. Он был заменен pasystray

Следующий пример можно использовать и изменять, при необходимости, как стартовый скрипт, запускающий демон PulseAudio и загружающий программу *padevchooser* (при необходимости, требуется сборка из AUR). Назовем его `jack_startup`:

```
#!/bin/bash	
#Load PulseAudio and PulseAudio Device Chooser
pulseaudio -D
padevchooser&

```

Аналогичный скрипт для остановки PulseAudio и Pulse Audio Device Chooser, который назовем `jack_shutdown` и также разместим в домашней директории:

```
#!/bin/bash	
#Kill PulseAudio and PulseAudio Device Chooser		
pulseaudio --kill	
killall padevchooser	

```

Оба скрипта сделаем исполняемыми:

```
chmod +x jack_startup jack_shutdown

```

затем запустим QjackCtl, нажмем на кнопку *Setup* и перейдем на вкладку *Options*, где отметим обе опции "Execute Script after Startup:" и "Execute Script on Shutdown:", в которые добавим адреса до наших скриптов (с помощью кнопки ... или вписав путь до файлов) `~/jack_startup` и `~/jack_shutdown`, при условии, что они располагаются в домашней директории. Сохраним изменения.

## PulseAudio через OSS

Добавьте следующее в `/etc/pulse/default.pa`:

```
load-module module-oss

```

Затем запустите PulseAudio как обычно, убедитесь что все источники объявлены для OSS усройств.

## Запуск PulseAudio из chroot (напр. 32-бит chroot в 64-битной истеме)

Так как chroot представляет собственный root для запуска/остановки приложений, PulseAudio должен быть установлен из самого chroot (`pacman -S pulseaudio` в окружении chroot).

PulseAudio, если не настроен на подключения к конкретному серверу (это можно сделать в `/etc/pulse/client.conf`, через переменную окружения PULSE_SERVER, или через локальные настройки X11, используя module-x11-publish), будет пытаться подключится к локальному pulse серверу, если у него не получится - он создаст новый. Каждый pulse сервер имеет уникальный ID, основанный на машинном id значении в `/var/lib/dbus`. Чтобы дать приложениям из chroot доступ к pulse серверу, следующие директории должны быть смонтированный в chroot:-

```
/run
/var/lib/dbus
/tmp
~/config/.pulse

```

`/dev/shm` также должен быть смонтирован для эффективного использования. Заметьте, что монтирование /home также обычно означает общий доступ к каталогу `~/.pulse`.

PulseAduio выберет путь к сокету через XDG_RUNTIME_DIR, так что удостовертесь что перенесли его тоже с помощью sudo, когда используете chroot (см. [Sudo#Environment variables](/index.php/Sudo_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#.D0.9F.D0.B5.D1.80.D0.B5.D0.BC.D0.B5.D0.BD.D0.BD.D1.8B.D0.B5_.D0.BE.D0.BA.D1.80.D1.83.D0.B6.D0.B5.D0.BD.D0.B8.D1.8F "Sudo (Русский)")).

Для особых случаев, пожалуйста, обратитесь к статьям по установке сборок 32-битных систем, особенно к [дополнительной секции](/index.php/Install_bundled_32-bit_system_in_Arch64#Allow_32-bit_applications_access_to_64-bit_PulseAudio "Install bundled 32-bit system in Arch64"), относящейся к PulseAudio.

## Отключение автоматического запуска сервера PulseAudio

Некоторые пользователи предпочитают вручную запускать сервер PulseAudio, перед запуском определенных программ, а затем останавливать сервер PulseAudio, когда они завершены. Для достижения такого результата, отредактируйте `~/.config/pulse/client.conf` или `/etc/pulse/client.conf` и измените `autospawn = yes` на `autospawn = no`. Убедитесь что строка не закомментирована.

 `/etc/pulse/client.conf` 
```
autospawn = no

```

Теперь вы можете вручную запустить PulseAudio сервер командой

```
$ pulseaudio --start

```

И остановить его

```
$ pulseaudio --kill

```

Этот параметр также учитывается стандартным скриптом pulseaudio при запуске сеанса рабочего стола `start-pulseaudio-x11` который выполняется из `/etc/xdg/autostart/pulseaudio.desktop`.

## Отключение демона pulseaudio полностью

Чтобы отключить демон PulseAudio полностью, и тем самым предотвратить его запуск, добавьте `daemon-binary=/bin/true` в файл настроек.

 `~/.config/pulse/client.conf #or /etc/pulse/client.conf` 
```
daemon-binary=/bin/true

```

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

Это тоже самое, что инвертировать стерео, когда левый и правый канал меняются местами.

Во-первых, определите звуковую карту, в которой вы хотите произвести изменение:

```
$ cat /proc/asound/cards

```

и запомните строку с именем для устройства, которое вы хотите использовать (оно заключено в квадратные скобки, например [Intel]).

Отредактируйте `/etc/pulse/default.pa` и закомментируйте строки, которые содержат module-hal-detect и module-detect.

Найдите закомментированную строку, которая начинается с "#load-module module-alsa-sink", раскомментируйте ее и измените на

```
load-module module-alsa-sink device=hw:[device name] channel_map=right,left

```

Перезапустите демон PulseAudio

```
pulseaudio -k; pulseaudio -D

```

[Документация переназначения модуля устройства](http://www.freedesktop.org/wiki/Software/PulseAudio/Documentation/User/Modules/#index12h3)

## PulseAudio в качестве ненавязчивого проводника ALSA

Некоторые пользователи по различным причинам не хотят всё время запускать PulseAudio. Этот пример превратит полноценный звуковой сервер в ненавязчивый проводник к устройствам ALSA, который автоматически запускает **и** останавливает себя, когда дело сделано, позволяя приложениям требующим PulseAudio, полностью функционировать, не трогая настройки ALSA, не устанавливая себя по умолчанию как устройства ALSA.

Эта настройка позволит клиентам, использующим PA, производить автозапуск демона в тот момент, когда он им понадобится, а также завершать его работу как только все клиенты отсоединяться.

Сам демон использует простую статическую настройку, которая использует только настроенные вами `pcm.!default` устройства ALSA. Никаких замен ALSA, никаких игр с уровнями микшера, ничего, кроме записи/воспроизведения. Также убедитесь, что [pulseaudio-alsa](https://www.archlinux.org/packages/?name=pulseaudio-alsa) **не** установлен, так как стандартные клиенты ALSA по умолчанию не привязаны к Pulse. Функции `alsamixer` продолжают работать должным образом, как и любые другие клиенты ALSA . Также убедитесь, что общие фрэймворки, как Xine, Gstreamer и Phonon настроены на использование ALSA: по умолчанию, если они обнаружат установленный PulseAudio, они будут пытаться использовать его перед ALSA.

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

## Наушники и колонки подключены одновременно и переключаются приложением на лету

Pulseaudio устроен так, что он автоматически отключает Line Out, когда подключены наушники и начинает использовать их ползунок для управления. Подобное поведение вы можете наблюдать в `alsamixer`. Мы же хотим разделить управление наушников и Line Out, и заставить их работать одновременно. Это очень полезно в том случае, если вы хотите переназначить гнезда Realtek, например, зеленое использовать для наушников, а голубое - для динамиков (при помощи `hdajackretask` из [alsa-tools](https://www.archlinux.org/packages/?name=alsa-tools)).

Для этого вам потребуется отредактировать непосредственно конфигурацию Pulseaudio mixer:

1\. Мы сообщаем pulseaudio, что наушники всегда подключены. Редактируем:

`/usr/share/pulseaudio/alsa-mixer/paths/analog-output-lineout.conf`

Находим:

```
[Jack Headphone]
state.plugged = no
state.unplugged = unknown

```

Изменяем `no` на `yes`

2\. По умолчанию, громкость Line Out управляется только через Master, а не через ползунок Line Out. Мы хотим соединить Line Out с Master.

Добавьте этот блок в конец файла:

```
[Element Line Out]
switch = mute
volume = merge

```

3\. Нам нужно полностью отключать Line Out, когда мы используем наушники. Редактируем:

`/usr/share/pulseaudio/alsa-mixer/paths/analog-output-headphones.conf`

Добавляем блок в конец файла:

```
[Element Line Out]
switch = off
volume = off

```

4\. Как и Pulseaudio, Alsa самостоятельно отключает динамики, когда подключаются наушники. Откройте `alsamixer` (для Realtek HDA `alsamixer -c0`) и измените `Auto-Mute mode` на `disabled`.

5\. Перезапустите Pulseaudio

```
$ pulseaudio -k
$ pulseaudio --start

```

Теперь у вас есть два порта на одно устройство вывода в pulseaudio. Они заглушают друг друга, таким образом вы можете переключиться на наушники, и это отключит звук в динамиках и наоборот. Для переключения между портами вы можете использовать звуковой микшер Gnome или Plasma, или установить подходящее расширение рабочего стола.

## Одновременное использование PulseAudio несколькими пользователями

Иногда желательно запускать программы как другой пользователь, находясь в системе как основной пользователь, например, для изоляции программы. Тем не менее, PulseAudio по умолчанию не будет поддерживать соединения второго пользователя, поскольку демон PulseAudio уже запущен для основного. Но может быть создан сокет PulseAudio UNIX для поддержки соединений других пользователей демоном PulseAudio, запущенным основным пользователем.

Во-первых, отредактируйте файл `/etc/pulse/default.pa` или `~/.config/pulse/default.pa` и добавьте указание для создания unix сокета:

 `~/.config/pulse/default.pa`  `load-module module-native-protocol-unix auth-anonymous=1 socket=/tmp/pulse-socket` 

Затем, укажите PulseAudio в качестве клиента для сокета UNIX, только что созданного вторым пользователем:

 `/home/*secondaryuser*/.config/pulse/client.conf`  `default-server = unix:/tmp/pulse-socket` 

Теперь, после перезапуска демона PulseAudio, приложения, запущенные от имени второго пользователя, должны без проблем проигрывать звук через демон PulseAudio, запущенный основным пользователем.