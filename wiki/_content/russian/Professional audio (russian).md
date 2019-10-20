Related articles

*   [Sound system (Русский)](/index.php/Sound_system_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Sound system (Русский)")
*   [envy24control](/index.php/Envy24control "Envy24control")

Современные Linux системы способны удовлетворить любые ваши (полу-)профессиональные аудио потребности. При использовании хорошего аппаратного обеспечения и надлежащей конфигурации можно добиться временной задержки от 5 мс до 1 мс.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Начало работы](#Начало_работы)
    *   [1.1 Настройка системы](#Настройка_системы)
        *   [1.1.1 Контрольный перечень](#Контрольный_перечень)
    *   [1.2 JACK](#JACK)
        *   [1.2.1 FireWire](#FireWire)
        *   [1.2.2 Jack Flash](#Jack_Flash)
        *   [1.2.3 Quickscan JACK script](#Quickscan_JACK_script)
        *   [1.2.4 Desktop Effects vs JACK](#Desktop_Effects_vs_JACK)
        *   [1.2.5 Общий пример](#Общий_пример)
*   [2 Режим реального времени ядра](#Режим_реального_времени_ядра)
    *   [2.1 AUR](#AUR)
*   [3 MIDI](#MIDI)
*   [4 Переменные окружения](#Переменные_окружения)
*   [5 Советы и хитрости](#Советы_и_хитрости)
*   [6 Аппаратное обеспечение](#Аппаратное_обеспечение)
    *   [6.1 M-Audio Delta 1010](#M-Audio_Delta_1010)
    *   [6.2 M-Audio Fast Track Pro](#M-Audio_Fast_Track_Pro)
    *   [6.3 PreSonus Firepod](#PreSonus_Firepod)
    *   [6.4 PreSonus AudioBox USB](#PreSonus_AudioBox_USB)
    *   [6.5 Tascam US-122](#Tascam_US-122)
    *   [6.6 RME Babyface](#RME_Babyface)
*   [7 Несвободные приложения](#Несвободные_приложения)
    *   [7.1 Steinberg'овые SDK](#Steinberg'овые_SDK)
*   [8 Проект Arch Linux Pro Audio](#Проект_Arch_Linux_Pro_Audio)
*   [9 Linux и Arch Linux Pro Audio в новостях](#Linux_и_Arch_Linux_Pro_Audio_в_новостях)
*   [10 Mailing list](#Mailing_list)

## Начало работы

Некоторые основные профессиональные аудио приложения уже доступны из официального репозитория или репозитория сообщества Arch Linux. Для всего остального вы можете либо добавить бинарный репозиторий (смотрите ниже) либо, если вы предпочитаете компиляцию, поискать приложение в AUR. Никто не останавливает вас от непосредственной сборки новых выпусков, но, с тем же успехом, вы могли бы пользоваться LFS.

Начните с установки [JACK](/index.php/JACK "JACK").

Следующие пакеты являются хорошим базисом для построения полнофункциональной профессиональной аудио системы:

*   [qjackctl](https://www.archlinux.org/packages/?name=qjackctl)
*   [patchage](https://www.archlinux.org/packages/?name=patchage)
*   [ardour](https://www.archlinux.org/packages/?name=ardour)
*   [qtractor](https://www.archlinux.org/packages/?name=qtractor)
*   [hydrogen](https://www.archlinux.org/packages/?name=hydrogen)
*   [musescore](https://www.archlinux.org/packages/?name=musescore)
*   [rosegarden](https://www.archlinux.org/packages/?name=rosegarden)
*   [qsynth](https://www.archlinux.org/packages/?name=qsynth)
*   [jsampler](https://www.archlinux.org/packages/?name=jsampler)
*   [lmms](https://www.archlinux.org/packages/?name=lmms)
*   [calf](https://www.archlinux.org/packages/?name=calf)
*   [dssi](https://www.archlinux.org/packages/?name=dssi)
*   [guitarix2](https://www.archlinux.org/packages/?name=guitarix2)

Другие пакеты, которые могут вам понадобиться, доступны через [AUR](/index.php/Arch_User_Repository_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Arch User Repository (Русский)"):

*   [qsampler](https://www.archlinux.org/packages/?name=qsampler) (also see [LinuxSampler](/index.php/LinuxSampler "LinuxSampler"))
*   [mhwaveedit](https://aur.archlinux.org/packages/mhwaveedit/)
*   [carla](https://www.archlinux.org/packages/?name=carla)
*   [rakarrack-git](https://aur.archlinux.org/packages/rakarrack-git/)
*   [XCFA](https://aur.archlinux.org/packages/XCFA/)
*   [yoshimi](https://www.archlinux.org/packages/?name=yoshimi)
*   [wineasio](https://aur.archlinux.org/packages/wineasio/)
*   [vst-bridge](https://github.com/abique/vst-bridge)

Смотрите также [List of applications (Русский)#Аудиосистемы](/index.php/List_of_applications_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#Аудиосистемы "List of applications (Русский)"), [List of applications (Русский)#Редакторы аудио](/index.php/List_of_applications_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#Редакторы_аудио "List of applications (Русский)"), и [awesome-linuxaudio](https://github.com/nodiscc/awesome-linuxaudio).

### Настройка системы

Могут оказаться полезными следующие часто используемые настройки системы:

*   Добавление себя в [группу](/index.php/Users_and_groups_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#Группы "Users and groups (Русский)") *audio*.
*   Добавление [параметра ядра](/index.php/Kernel_parameters_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Kernel parameters (Русский)") `threadirqs`.
*   Установка ядра [linux-rt](https://aur.archlinux.org/packages/linux-rt/).
*   Настройка регулятора [cpufreq](/index.php/CPU_frequency_scaling_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "CPU frequency scaling (Русский)") на *performance* (производительность).
*   Добавление параметра *noatime* в [fstab](/index.php/Fstab_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Fstab (Русский)") (смотрите [Improving performance#Mount options](/index.php/Improving_performance#Mount_options "Improving performance")).

Настройка в реальном времени в основном автоматизирована. Нет больше необходимости вносить правки в файлы вроде `/etc/security/limits.conf` для получения доступа реального времени. Тем не менее, если вам необходимо изменить настройки, смотрите `/etc/security/limits.d/99-audio.conf` и `/usr/lib/udev/rules.d/40-hpet-permissions.rules` (эти файлы поставляются с пакетами [jack](https://www.archlinux.org/packages/?name=jack) или [jack2](https://www.archlinux.org/packages/?name=jack2)). Дополнительно, вы можете захотеть увеличить максимально запрашиваемую частоту прерывания RTC (по умолчанию 64 Hz), запустив [следующее при загрузке системы](/index.php/Systemd_FAQ#How_can_I_make_a_script_start_during_the_boot_process? "Systemd FAQ"):

```
echo 2048 > /sys/class/rtc/rtc0/max_user_freq
echo 2048 > /proc/sys/dev/hpet/max-user-freq

```

По умолчанию, частота обращения к swap определяется параметром "swappiness" и имеет значение 60\. При уменьшении этого числа до 10, система будет ждать гораздо дольше перед тем, как попытается начать запись на диск. Далее, параметр *inotify* следит за изменениями, вносимыми в файлы, и сообщает о них приложениям при соответствующих запросах. Когда ведётся работа с большим объёмом аудио данных, требуется множество контролёров, поэтому необходимо увеличить их число. Две этих настройки можно произвести в файле `/etc/sysctl.d/99-sysctl.conf`.

```
vm.swappiness = 10
fs.inotify.max_user_watches = 524288

```

Вы также можете захотеть увеличить таймер задержки PCI для звуковой карты формата PCI и повысить значение таймера задержки всех остальных PCI устройств (по умолчанию 64).

```
$ setpci -v -d *:* latency_timer=**b0**
$ setpci -v -s *$SOUND_CARD_PCI_ID* latency_timer=**ff** # eg. SOUND_CARD_PCI_ID=03:00.0 (see below)

```

Значение SOUND_CARD_PCI_ID может быть получено таким образом:

 `$ lspci ¦ grep -i audio` 
```
**03:00.0** Multimedia audio controller: Creative Labs SB Audigy (rev 03)
**03:01.0** Multimedia audio controller: VIA Technologies Inc. VT1720/24 [Envy24PT/HT] PCI Multi-Channel Audio Controller (rev 01)
```

#### Контрольный перечень

Представленные ниже пункты по большей части приведены для того, чтобы вы могли удостовериться, что у вас работающая мультимедиа система:

*   Тщательно ли я настроил звук? Смотрите [ALSA](/index.php/Advanced_Linux_Sound_Architecture_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Advanced Linux Sound Architecture (Русский)") или [OSS](/index.php/OSS "OSS").

```
$ speaker-test

```

*   Включен ли я в группу audio? Смотрите [ALSA](/index.php/Advanced_Linux_Sound_Architecture_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Advanced Linux Sound Architecture (Русский)") или [OSS](/index.php/OSS "OSS").

```
$ groups | grep audio

```

*   Захвачено ли устройство с помощью PulseAudio, OSS или чего-то иного?

```
$ lsof +c 0 /dev/snd/pcm* /dev/dsp*

```

-ИЛИ-

```
$ fuser -fv /dev/snd/pcm* /dev/dsp*  

```

*   Работают ли PAM-security (подключаемые модули аутентификации) и режим реального времени?

Смотрите: [Realtime for Users#PAM-enabled login](/index.php/Realtime_for_Users#PAM-enabled_login "Realtime for Users") (Обратите особое внимание, особенно если вы не запускали KDM, GDM или Slim.)

*   Перезагрузился ли я после всех проделанных изменений?

### JACK

Главная задача здесь заключена в поиске лучшего соотношения размера буффера (buffer size) и частот (periods), которое может обеспечить ваше программное обеспечение. Разумнее всего начинать со значения **Frames/Period = 256**. Попробуйте использовать **Periods/Buffer = 3** для встроенных и USB устройств. Наиболее распространённые значения: 256/3, 256/2, 128/3.

Кроме того, частота семплирования должна совпадать с частотой семплирования аппаратного обеспечения. Для проверки возможности поддержки вашим устройством частоты семплирования и битрейта:

```
$ cat /proc/asound/card0/codec#0

```

Измените *card0* и *codec#0* на ваши значения. Следует обратить внимание на **rates** или *VRA* в **Extended ID**. Современные устройства чаще всего обладают частотой семплирования **48000 Hz**. Чуть менее распространены значения 44100 Hz и 96000 Hz.

Почти всегда при записи или сведении с использованием внешних устройств требуется работа в режиме реального времени (**realtime**). Также, вам, возможно, захочется установить максимальный приоритет (как минимум в 10 раз меньше чем ограничения системы, определённые в файле `/etc/security/limits.d/99-audio.conf`; наивысший для самого устройства).

Запустите jack с опциями, которые вы получили ранее:

```
$ /usr/bin/jackd -R -P89 -dalsa -dhw:0 -r48000 -p256 -n3

```

[qjackctl](https://www.archlinux.org/packages/?name=qjackctl), [cadence](https://www.archlinux.org/packages/?name=cadence) и [patchage](https://www.archlinux.org/packages/?name=patchage) могут быть использованы как графическая оболочка для контроля за статусом JACK и упрощением его настройки.

**Примечание:** Как только вы закончите конфигурацию JACK, проверьте ваши настройки, запустив различные аудио приложения. Я потратил целый день, разбираясь с проблемой работы JACK xrun с LMMS, что в конце концов оказалось проблемой с последним.

*Дополнительная информация: [Linux Magazine article](http://www.linux-magazine.com/content/download/63041/486886/version/1/file/JACK_Audio_Server.pdf)*

#### FireWire

**Примечание:** Дополнительные действия не требуются, так как большинство вещей было автоматизировано, особенно с введением [нового стека FireWire](https://ieee1394.wiki.kernel.org/articles/j/u/j/Juju_Migration_e8a6.html), отказом от HAL и большей концентрации на [udev](/index.php/Udev "Udev"). Вам не требуется редактировать права устройств, но если вы столкнулись с проблемами и подозреваете, что причина кроется в этом, ознакомьтесь с `/lib/udev/rules.d/60-ffado.rules` и, если необходимо, создайте и разместите свои правки в `/etc/udev/rules.d/60-ffado.rules`.

JACK(2) построен против FFADO, вам только нужно установить его с пакетом [libffado](https://www.archlinux.org/packages/?name=libffado).

Для проверки возможности запустить FireWire вам следует:

*   Убедиться, что загружены необходимые модули ядра:

```
# modprobe firewire-core firewire-ohci

```

*   Сможет ли ваш чипсет инициировать устройство?

[http://www.ffado.org/?q=node/622](http://www.ffado.org/?q=node/622)

*   Сможет ли ваш чипсет позволить устройству работать на полную мощность?

Мы не можем сказать это наверняка, особенно для устройств, построенных на базе Ricoh (проблема кроссплатформенности). В большинстве случаев устройство работает хорошо, но иногда можно столкнуться с забавными причудами. Если это случилось с вами, то вам можно только посочувствовать.

**Примечание:** Как указано Takashi Sakamoto [в списке рассылки alsa-devel](http://mailman.alsa-project.org/pipermail/alsa-devel/2014-September/081731.html), если вы используете бэкенд FireWire с jackd, модуль DICE будет несовместим. Если вы увидели строку как эта:
```
Warning (dice_eap.cpp)[1811] read: No routes found. Base 0x7, offset 0x4000

```
вам необходимо отключить модуль "snd_dice".

#### Jack Flash

Если после настройки jack вы обнаружили, что Flash больше не воспроизводит звук.

Чтобы дать возможность flash работать с jack, вам нужно [установить](/index.php/%D0%A3%D1%81%D1%82%D0%B0%D0%BD%D0%BE%D0%B2%D0%B8%D1%82%D1%8C "Установить") пакет [libflashsupport-jack](https://aur.archlinux.org/packages/libflashsupport-jack/).

Вы также можете использовать более гибкий способ для настройки возможности программам Alsa (включая Flash) проигрывать звук при запущенном jack:

Во-первых, вы должны установить плагин jack для Alsa, [установив](/index.php/%D0%A3%D1%81%D1%82%D0%B0%D0%BD%D0%BE%D0%B2%D0%B8%D1%82%D1%8C "Установить") пакет [alsa-plugins](https://www.archlinux.org/packages/?name=alsa-plugins). Активируйте его отредактировав (или создав) `/etc/asound.conf` (настройка для всей системы), чтобы в нём были следующие строки:

```
# convert alsa API over jack API
# use it with
# % aplay foo.wav

# use this as default
pcm.!default {
    type plug
    slave { pcm "jack" }
}

ctl.mixer0 {
    type hw
    card 1
}

# pcm type jack
pcm.jack {
    type jack
    playback_ports {
        0 system:playback_1
        1 system:playback_2
    }
    capture_ports {
        0 system:capture_1
        1 system:capture_2
    }
}

```

Перезагрузка или иные действия не требуются. Просто отредактируйте конфигурационные файлы alsa, запустите jack.

#### Quickscan JACK script

Вероятно, большинство людей захотят работать с JACK в режиме реального времени; однако, для этого требуется крутить слишком много ручек и настроек.

Отличный способ проверить системную конфигурацию после настройки JACK'а — это запустить скрипт Quickscan.

[https://github.com/raboof/realtimeconfigquickscan/blob/master/realTimeConfigQuickScan.pl](https://github.com/raboof/realtimeconfigquickscan/blob/master/realTimeConfigQuickScan.pl)

Вывод данного скрипта покажет вам узкие места(бутылочное горло) в системе и/или железе, и укажет места, где можно найти более подробную информацию по этому поводу.

#### Desktop Effects vs JACK

In addition to the factors listed under the System Configuration section above as well as the settings checked by realTimeConfigQuickScan.pl, it is also worth noting that desktop environments can cause xruns and hence JACK audio glitches, especially memory/process intensive ones and those desktops that utilize composited desktop effects. It is recommended you disable desktop effects when using JACK. You are likely to get the least xruns and best performance by running a lightweight desktop or just a window manager instead.

#### Общий пример

Общий пример настройки доступен по ссылке [JACK Audio Connection Kit#A shell-based example setup](/index.php/JACK_Audio_Connection_Kit#A_shell-based_example_setup "JACK Audio Connection Kit").

## Режим реального времени ядра

С недавнего времени основное ядро Linux предоставляет хорошие возможности для использования его в режиме реального времени. Основное ядро (с параметром `CONFIG_PREEMPT=y`, используемое в Арч по умолчанию) в худшем случае может работать с задержкой [до 10мс](https://rt.wiki.kernel.org/index.php/Frequently_Asked_Questions#What_are_real-time_capabilities_of_the_stock_2.6_linux_kernel.3F) (время между моментом аппаратного прерывания и моментом, соответствующим получению прерывания выполняющимся потоком), хотя, конечно же, некоторые драйверы устройств могут внести задержки намного бо́льшие, чем системные. В зависимости от вашего аппаратного обеспечения и драйверов (и требований), вы, возможно, захотите ядро с возможностями жёсткого режима реального времени.

Патч [RT_PREEPMT](https://rt.wiki.kernel.org/index.php/RT_PREEMPT_HOWTO) от Инго Молнара (Ingo Molnar) и Томаса Глейкснера (Thomas Gleixner) является интересным вариантом для жёстких задержек и приложений режима реального времени, достигаемых в профессиональном аудио промышленного масштаба. Большинство аудио специфичных дистрибутивов Linux поставляются с применением данного патча. Режим вытесняющей многозадачности реального времени ядра также позволяет настроить приоритеты прерываний (IRQ) обработки потоков и помогает обеспечить плавный звук почти независимо от нагрузки.

Если вы собираетесь компилировать собственное ядро, помните, что удаление модулей/опций не следует приравнивать к «лёгкости и простоте» ядра. Образ ядра, конечно же, уменьшится, но в современных системах это не такая проблема, какая она была в 1995-м.

В любом случае, вы должны обеспечить следующие параметры:

*   **Timer Frequency** установить в значение **1000Hz** (CONFIG_HZ_1000=y; если вы не задаёте *MIDI*, вы можете это игнорировать)
*   **APM** в значение **DISABLED** (CONFIG_APM=n; Могут быть трудности с некоторым оборудованием - по умолчанию в x86_64)

Если вы хотите действительно лёгкую систему, мы предлагаем вам пойти своим путём и развернуть систему один раз с статической аппаратной поддержкой. Однако, вам понадобится выбрать архитектуру процессора. Выбор «Core 2 Duo» с подбором соответствующего аппаратного обеспечения может послужить хорошим подспорьем для оптимизации; но тем меньше будет выигрыш, чем ниже архитектура.

Основные проблемы с режимом реального времени ядра:

*   Гиперпоточность (hyperthreading) (если имеются подозрения, отключите в BIOS)

Также имеются готовые скомпилированные с патчами ядра, доступные в ABS и AUR.

**Примечание:** Прежде чем вы решите использовать патченное ядро, загляните по ссылке: [http://jackaudio.org/faq/realtime_vs_realtime_kernel.html (англ.)](http://jackaudio.org/faq/realtime_vs_realtime_kernel.html).

### AUR

Из репозитория [AUR](/index.php/AUR "AUR") вам доступны следующие варианты:

*   [linux-rt](https://aur.archlinux.org/packages/linux-rt/)
*   [linux-rt-lts](https://aur.archlinux.org/packages/linux-rt-lts/) (долгосрочная поддержка, стабильный выпуск)

Два первых - это стандартные ядра с патчем CONFIG_PREEMPT_RT, в то время как -ice включают некоторые патчи, которые работают не на всех конфигурациях.

	*Смотрите: [Real-Time Linux Wiki](https://rt.wiki.kernel.org/)*

## MIDI

Для уменьшения дрожания MIDI при использовании внешнего MIDI оснащения jack2, должна быть использована опция Xalsarawmidi. При этом вам также потребуется использовать a2jmidid.

Вы можете проверить насколько сильно дрожание с помощью [alsa-midi-latency-test](https://github.com/koppi/alsa-midi-latency-test). PCI и PCIe карты зачастую показывают лучшие результаты по сравнению с устройствами USB MIDI.

При работе с MIDI настоятельно рекомендуется установить a2j ([a2jmidid](https://www.archlinux.org/packages/?name=a2jmidid)) - связующее звено между alsa midi и jack midi. Это позволит вам соединить приложения, которые связаны только с alsa midi, с приложениями, которые связаны только с jack midi. Laditray также может запускать/останавливать a2j.

	*Смотрите: [JACK#MIDI](/index.php/JACK#MIDI "JACK")*

## Переменные окружения

Если вы что-то устанавливаете в нестандартный каталог, зачастую необходимо настроить переменные путей окружения, чтобы приложения знали где искать (для плагинов и других библиотек). Обычно это относится к VST, так как пользователи могут иметь Wine или внешние пути Windows.

Как правило, плагины Linux (LADSPA, LV2, DSSI, LXVST) располагаются по стандартным путям, поэтому не требуется их экспортировать. Но если это не так, убедитесь, что добавили эти стандартные пути, так как Arch ничего не будет делать для *dssi* или *ladspa*, и приложений вроде *dssi-vst*, и не будет смотреть где-то ещё, если найдет предустановленные пути.

 `~/.bashrc` 
```
...
export VST_PATH=/usr/lib/vst:/usr/local/lib/vst:~/.vst:/someother/custom/dir
export LXVST_PATH=/usr/lib/lxvst:/usr/local/lib/lxvst:~/.lxvst:/someother/custom/dir
export LADSPA_PATH=/usr/lib/ladspa:/usr/local/lib/ladspa:~/.ladspa:/someother/custom/dir
export LV2_PATH=/usr/lib/lv2:/usr/local/lib/lv2:~/.lv2:/someother/custom/dir
export DSSI_PATH=/usr/lib/dssi:/usr/local/lib/dssi:~/.dssi:/someother/custom/dir
```

## Советы и хитрости

*   Отключите WiFi и закройте все приложения, нетребующиеся для записи, такие как браузер. Многие отмечали, что отключение WiFi сказывается на производительности JACK.

*   Известно, что некоторое USB аудио аппаратное обеспечение не работает с портами USB 3, попробуйте вместо этого использовать порты USB 2/1.

*   Могут случаться ошибки IRQ, что создаёт проблемы. Пример, видео аппаратное обеспечение, резервирующее шину, приводящее к ненужным прерываниям в системном пути ввода-вывода. Смотрите обсуждение в [FFADO IRQ Priorities How-To](http://subversion.ffado.org/wiki/IrqPriorities). Если вы используете ядро реального времени или свежее ядро, вы можете использовать [rtirq](https://www.archlinux.org/packages/?name=rtirq) для настройки приоритетов обработки потоков IRQ.

*   Не используйте службу **irqbalance**, или будьте с ней очень осторожны [[1]](http://docs.redhat.com/docs/en-US/Red_Hat_Enterprise_MRG/1.3/html/Realtime_Tuning_Guide/sect-Realtime_Tuning_Guide-General_System_Tuning-Interrupt_and_Process_Binding.html).

*   Если вам необходимо использовать несколько аудио устройств с JACK2, можно воспользоваться вспомогательными программами **alsa_in** и **alsa_out** для скрытия лишних устройств и показывать их как вывод в JACK patchbay.

*   Некоторые службы/процессы могут неожиданно вызывать **xruns**. Если вам это не нужно, отключите их. Без вопросов.

```
$ ls /var/run/daemons
$ top # or htop, ps aux, whatever you are comfortable with
$ killall -9 $processname
# systemctl stop $daemonname

```

*   Если *xruns* было запущено много раз, особенно с [nvidia](https://www.archlinux.org/packages/?name=nvidia), отключите дросселирование GPU. Сделать это можно с помощью апплета управления картой и для nvidia это "prefer maximum performance" (спасибо за письмо в LAU от Frank Kober).

*   Если вы хотите узнать больше о ALSA: [http://www.volkerschatz.com/noise/alsa.html](http://www.volkerschatz.com/noise/alsa.html)

## Аппаратное обеспечение

Подавляющее большинство звуковых карт и аудио устройств не потребуют дополнительных настроек или пакетов для работы. Просто укажите используемое гнездо звуковой карты и перезагрузите систему.

Но это справедливо не для всех устройств, в частности для тех что перечислены ниже.

### M-Audio Delta 1010

Серия звуковых карт M-Audio Delta основана на аудио чипсете VIA Ice1712. Карты, основанные на этом чипе, требуют установки пакета alsa-tools, так как в нём содержится приложение [envy24control](/index.php/Envy24control "Envy24control"). [Envy24control](/index.php/Envy24control "Envy24control") - это микшер/контроллер аппаратного уровня. Вы *можете* использовать alsa-mixer, но, поверьте, вы сохраните кучу нервов, если не будете пробовать этого. Обратите внимание, в этом разделе отсутствует информация о настройке или использовании MIDI.

Запустите приложение-микшер:

```
$ envy24control

```

Это приложение может показаться очень запутанным; смотрите [envy24control](/index.php/Envy24control "Envy24control") для объяснения по работе с ним. Тем не менее, ниже приведёна очень простая работающая конфигурация для мультитрекинга с Ardour.

1.  На вкладках "Monitor Inputs" и "Monitor PCMs" установите значение 20 для всех контролируемых входов и PCM's.
2.  На вкладке "Patchbay / Router" для всех значений выберите выход PCM.
3.  На вкладке "Hardware Settings" убедитесь, что настройки Master Clock совпадают с настройками Qjackctl. Если это не так, то ваш xruns не контролируется!

### M-Audio Fast Track Pro

The M-Audio Fast Track Pro - это аудио интерфейс USB 4x4, работающий с характеристиками 24 бит/96 кГц. Из-за ограничений USB 1, это устройство требует дополнительной настройки для получения доступа ко всем его функциям. Устройство может работать в одном из двух режимов:

*   Конфигурация 1, или "Режим совместимости классов" ("Class compliant mode") - с усечённой функциональностью, только 16 бит, 48 кГц, аналоговый вход (2 канала) и цифровой/аналоговый выход (4 канала).
*   Конфигурация 2 - с доступом ко всем функциям интерфейса.

В настоящий момент, с обычным ядром оно запускается в конфигурации 2, но если вы хотите дополнительно проверить, так ли это, вы можете обратиться к логам ядра в поисках записей вида:

```
usb-audio: Fast Track Pro switching to config #2
usb-audio: Fast Track Pro config OK

```

С интерфейсом потребуется проделать несколько дополнительных операций для переключения режима. Это производится с помощью опции `device_setup` в процессе загрузке модуля. Рекомендуемый способ настройки интерфейса осуществляется с использованием файла в `modprobe.d`:

 `/etc/modprobe.d/ftp.conf` 
```
options snd_usb_audio vid=0x763 pid=0x2012 device_setup=XXX index=YYY enable=1

```

где `vid` и `pid` - идентификаторы поставщика и продукта для M-Audio Fast Track Pro, `index` - это требуемый номер устройства и `device_setup` - требуемая настройка устройства. Возможные значения для `device_setup`:

<caption>device modes</caption>
| device_setup value | bit depth | frequency | analog output | digital output | analog input | digital input | IO mode |
| 0x0 | 16 bit | 48kHz | + | + | + | + | 4x4 |
| 0x9 | 24 bit | 48kHz | + | + | + | - | 2x4 |
| 0x13 | 24 bit | 48kHz | + | + | - | + | 2x4 |
| 0x5 | 24 bit | 96kHz | * | * | * | * | 2x0 or 0x2 |

Режим 24 бита/96 кГц является особенным: он предоставляет все входы/выходы, но вы можете открыть только 4 интерфейса одновременно. Если вы, например, откроете выходной интерфейс и следом попытаетесь открыть второй такой же или входной интерфейс, то увидите запись об ошибке в логах ядра:

```
cannot submit datapipe for urb 0, error -28: not enough bandwidth

```

что является нормальным, потому что это устройство USB 1 и не может обеспечить достаточную пропускную способность такого качества для более чем одного (2-канального) источника/получателя одновременно.

В зависимости от значения `index` будет установлено два устройства: `hwYYY:0` и `hwYYY:1`, которые будут содержать доступные входы и выходы. Первое устройство, скорее всего, будет содержать в себе аналоговый выход и цифровой вход, в то время как второй — аналоговый вход и цифровой выход. Чтобы узнать, где и как устройства соединены, — если они настроены правильно, — вы можете проверить `/proc/asound/cardYYY/stream{0,1}` . Ниже приведён список наиболее важных конечных точек (endpoints), которые помогут правильно определить соединения карты (легко перепутать аналоговые и цифровые входные или выходные соединения, прежде чем привыкаешь к устройству):

```
EP 3 (аналоговый выход (analogue output) = разъём TRS задней панели зеркально отображается на выходах RCA 1 и 2 задней панели)
EP 4 (цифровой выход (digital output) = выход S/PDIF задней панели зеркально отображается на выходах RCA 3 и 4 задней панели)
EP 5 (аналоговый вход (analogue input) = балансный разъём TRS или XLR микрофона, небалансная линия TS на передней панели)
EP 6 (цифровой вход (digital input) = вход S/PDIF задней панели)

```

This .asoundrc file enables 24-bit IO on the fast-track pro (and I'm sure it could be modified to work with other 3-byte usb devices) within the context of jack's 32-bit interface while routing default alsa traffic to jack outputs on the audio interface. Alsa will be in S24_3BE mode but jack can plug S32_LE data in and out of the interface and other alsa programs will be able to plug almost anything into jack.

```
### ~/.asoundrc
### default alsa config file, for a fast-track pro configured in 24-bit mode as so:
### options snd_usb_audio device_setup=0x9
### invoke jack with: (if you use -r48000, change the rate in the plugs as well)
### $jackd -dalsa -P"hw:Pro" -C"hw:Pro,1" -r44100

## setup input and output plugs so jack can write S24_3BE data to the audio interface

pcm.maud0 {
	type hw
	card Pro
	 }

#jack_out plug makes sure that S32_LE data can be written to hw:Pro
pcm.jack_out{
	type plug
	format S32_LE
	channels 2
	rate 44100
	slave pcm.maud0
}

pcm.maud1 {
	type hw
	card Pro
	device 1
}
## jack_in plug makes sure that hw:Pro,1 can read S32_LE data
pcm.jack_in {
	type plug
	format S32_LE
	channels 2
	rate 44100
	slave pcm.maud1
}
#####
# route default alsa traffic through jack system io

pcm.jack {
    type jack
    playback_ports {
        0 system:playback_1
        1 system:playback_2
    }
    capture_ports {
        0 system:capture_1
        1 system:capture_2
    }
} 
pcm.amix {
	type asym
	playback.pcm "jack"
	capture.pcm "jack"
	}
pcm.!default {
	type plug
	slave.pcm amix
}

```

### PreSonus Firepod

1.  Запуск: либо из командной строки, либо Qjackctl; драйвер называется firewire.
2.  Характеристики: карта содержит 8/8 XLR предусилителей плюс стереопара, итого получается 10 каналов.
3.  Сопряжение: карты могут соединяться вместе без каких-либо проблем.
4.  Настройка оборудования: ничего особенного; меняйте настройки в Qjackctl по своему усмотрению.

Уровни громкости аппаратные, а маршрутизация может быть выполнена в Qjackctl, даже если между собой сопряжено множество карт, — это не проблема. Ffadomixer пока ещё не работает с данной картой; надеемся, в будущем мы сможем контролировать больше аспектов карты через программный интерфейс как этот.

### PreSonus AudioBox USB

1.  Startup: ALSA именует устройство как "USB".
2.  Specs: Два моно входа TRS+XLR, два моно выхода TRS, MIDI вход и выход, плюс отдельный стерео канал для наушников. Присутствуют регуляторы для управления обоими входами, основным выходом, и для наушников, всего четыре.
3.  Hardware: Работает очень хорошо, и аудио и MIDI. Не управляется программным микшером.

### Tascam US-122

***Данные настройки неприменимы для US-122L***

1.  Требуемые пакеты: [alsa-tools](https://www.archlinux.org/packages/?name=alsa-tools) [alsa-firmware](https://www.archlinux.org/packages/?name=alsa-firmware) [fxload](https://aur.archlinux.org/packages/fxload/)
2.  Правила udev: создайте следующий файл правил, затем перезагрузите правила udev, [Udev (Русский)#Загрузка новых правил](/index.php/Udev_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#Загрузка_новых_правил "Udev (Русский)")

 `/etc/udev/rules.d/51-tascam-us-122.rules` 
```
SUBSYSTEMS=="usb", ACTION=="add", ATTRS{idProduct}=="8006", ATTRS{idVendor}=="1604", RUN+="/bin/sh -c '/sbin/fxload -D %N -s /usr/share/alsa/firmware/usx2yloader/tascam_loader.ihx -I /usr/share/alsa/firmware/usx2yloader/us122fw.ihx'"
SUBSYSTEMS=="usb", ACTION=="add", ATTRS{idProduct}=="8007", ATTRS{idVendor}=="1604", RUN+="/bin/sh -c '/usr/bin/usx2yloader'"

```

Подключите устройство. После этого устройство должно начать работать. Программного управления микшером нет.

### RME Babyface

Хорошо работает при малых задержках (~5мс) с [alsa-utils](https://www.archlinux.org/packages/?name=alsa-utils), [jack2](https://www.archlinux.org/packages/?name=jack2) и [linux-rt](https://aur.archlinux.org/packages/linux-rt/). Запуск ALSA только со стандартным ядром может привести к появлению треска при меньших задержках.

Для распознавания устройства и его работы, версия прошивки должна быть >= 200, который обладает режимом класса совместимости (Class Compliant Mode). Для перехода в режим совместимости классов (Class Compliant Mode) зажмите кнопки "Select" и "Recall" при подсоединении Babyface к компьютеру через USB. После этого оно должно быть распознано.

Для проверки распознавания устройства смотрите:

```
grep -i baby /proc/asound/cards

```

Для получения большей информации о режиме совместимости классов (Class Compliant Mode), посетите сайт RME. На нём имеется PDF, который рассказывает обо всех функциях.

Для Babyface не требуется особых настроек Jack. Но если вы захотите воспользоваться встроенным входом/выходом MIDI, вам нужно установить "MIDI Driver" в положение "seq" и, при необходимости, отключить "Enable Alsa Sequencer Support" для использования его в комбинации с другими устройствами MIDI (например, USB Midi клавиатура).

## Несвободные приложения

### Steinberg'овые SDK

Естественно, мы не можем распространять заголовки ни VST, ни ASIO в форме бинарных пакетов. Тем не менее, всякий раз, когда вы собираете программу, которая будет работать с плагинами VST в виде Windows-библиотек *.dll*, проверьте следующие пакеты (которые не требуют использования какого-либо SDK):

*   dssi-vst
*   fst
*   vestige

С учётом вышесказанного, если вы собираете программу, которая будет работать с нативными *.so* VST плагинами, то в этом случае выхода нет. Для таких случаев Арч позволяет нам поддерживать единую локальную базу данных приложений. Мы можем «установить» общесистемную SDK — достаточно лишь скачать и поместить файл в директорию установленного пакета.

[Получить их можно в AUR](https://aur.archlinux.org/packages.php?O=0&K=steinberg-&do_Search=)

**Примечание:** *Steinberg не запрещает распространять конечные продукты и не диктует лицензию, под которой они должны распространяться. Существует много плагинов с лицензией GPL. Таким образом, распространение бинарных пакетов или программного обеспечения, собранного с данными несвободными заголовками не проблема, потому что заголовки являются лишь временными зависимостями для сборки.*

## Проект Arch Linux Pro Audio

Да, у нас есть и такое. Задумайтесь над "Planet CCRMA" или "Pro Audio Overlay", меньше научной коннотации: [ArchAudio](http://archaudio.org).

Что значит, что сие является репозиторием дополнений, т.е. вы должны поработать над разумной установкой и настройкой Archlinux.

Это относительно новое течение, хотя инициатива была проявлена ещё примерно в 2006/2007г.

История: [https://bbs.archlinux.org/viewtopic.php?id=30547](https://bbs.archlinux.org/viewtopic.php?id=30547)

По всем вопросам, связанными с Arch- и ArchAudio- проблемами можно обратиться в наш **IRC**: #archaudio @ Freenode

## Linux и Arch Linux Pro Audio в новостях

*   [Построй систему для производства серьёзной мультимедиа продукции с Arch](https://www.linux.com/learn/tutorials/607117-build-a-serious-multimedia-production-workstation-with-arch-linux) - Linux.com статья, июль 2012

*   [Практика использования Arch](http://www.linuxjournal.com/content/arch-tale) - Статья от музыканта и писателя Dave Phillips, октябрь 2011

*   [С Windows на Linux: разумное решение](http://www.itwire.com/opinion-and-analysis/open-sauce/36698-from-windows-to-linux-a-sound-decision) - интервью с Geoff "songshop" Beasley, февраль 2010

## Mailing list

*   [Linux-audio-user -- A list for linux audio users](http://lists.linuxaudio.org/listinfo/linux-audio-user) The Linux pro-audio related mailing list with much traffic and a huge subscriber community of users and developers.