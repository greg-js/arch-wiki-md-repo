Related articles

*   [Sound system (Русский)](/index.php/Sound_system_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Sound system (Русский)")
*   [envy24control](/index.php/Envy24control "Envy24control")

Современные Linux системы способны удовлетворить любые ваши (полу-)профессиональные аудио потребности. При использовании хорошего аппаратного обеспечения и надлежащей конфигурации можно добиться временной задержки от 5 мс до 1 мс.

## Contents

*   [1 Начало работы](#.D0.9D.D0.B0.D1.87.D0.B0.D0.BB.D0.BE_.D1.80.D0.B0.D0.B1.D0.BE.D1.82.D1.8B)
    *   [1.1 Настройка системы](#.D0.9D.D0.B0.D1.81.D1.82.D1.80.D0.BE.D0.B9.D0.BA.D0.B0_.D1.81.D0.B8.D1.81.D1.82.D0.B5.D0.BC.D1.8B)
        *   [1.1.1 Контрольный перечень](#.D0.9A.D0.BE.D0.BD.D1.82.D1.80.D0.BE.D0.BB.D1.8C.D0.BD.D1.8B.D0.B9_.D0.BF.D0.B5.D1.80.D0.B5.D1.87.D0.B5.D0.BD.D1.8C)
    *   [1.2 JACK](#JACK)
        *   [1.2.1 FireWire](#FireWire)
        *   [1.2.2 Jack Flash](#Jack_Flash)
        *   [1.2.3 Quickscan JACK script](#Quickscan_JACK_script)
        *   [1.2.4 Desktop Effects vs JACK](#Desktop_Effects_vs_JACK)
        *   [1.2.5 Общий пример](#.D0.9E.D0.B1.D1.89.D0.B8.D0.B9_.D0.BF.D1.80.D0.B8.D0.BC.D0.B5.D1.80)
*   [2 Realtime Kernel](#Realtime_Kernel)
    *   [2.1 AUR](#AUR)
*   [3 MIDI](#MIDI)
*   [4 Переменные окружения](#.D0.9F.D0.B5.D1.80.D0.B5.D0.BC.D0.B5.D0.BD.D0.BD.D1.8B.D0.B5_.D0.BE.D0.BA.D1.80.D1.83.D0.B6.D0.B5.D0.BD.D0.B8.D1.8F)
*   [5 Советы и хитрости](#.D0.A1.D0.BE.D0.B2.D0.B5.D1.82.D1.8B_.D0.B8_.D1.85.D0.B8.D1.82.D1.80.D0.BE.D1.81.D1.82.D0.B8)
*   [6 Аппаратное обеспечение](#.D0.90.D0.BF.D0.BF.D0.B0.D1.80.D0.B0.D1.82.D0.BD.D0.BE.D0.B5_.D0.BE.D0.B1.D0.B5.D1.81.D0.BF.D0.B5.D1.87.D0.B5.D0.BD.D0.B8.D0.B5)
    *   [6.1 M-Audio Delta 1010](#M-Audio_Delta_1010)
    *   [6.2 M-Audio Fast Track Pro](#M-Audio_Fast_Track_Pro)
    *   [6.3 PreSonus Firepod](#PreSonus_Firepod)
    *   [6.4 PreSonus AudioBox USB](#PreSonus_AudioBox_USB)
    *   [6.5 Tascam US-122](#Tascam_US-122)
    *   [6.6 RME Babyface](#RME_Babyface)
*   [7 Restricted Software](#Restricted_Software)
    *   [7.1 Steinberg's SDKs](#Steinberg.27s_SDKs)
*   [8 Arch Linux Pro Audio Project](#Arch_Linux_Pro_Audio_Project)
*   [9 Linux и Arch Linux Pro Audio в новостях](#Linux_.D0.B8_Arch_Linux_Pro_Audio_.D0.B2_.D0.BD.D0.BE.D0.B2.D0.BE.D1.81.D1.82.D1.8F.D1.85)
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

*   [qsampler](https://aur.archlinux.org/packages/qsampler/) (also see [LinuxSampler](/index.php/LinuxSampler "LinuxSampler"))
*   [mhwaveedit](https://aur.archlinux.org/packages/mhwaveedit/)
*   [carla](https://aur.archlinux.org/packages/carla/)
*   [rakarrack-git](https://aur.archlinux.org/packages/rakarrack-git/)
*   [XCFA](https://aur.archlinux.org/packages/XCFA/)
*   [yoshimi](https://aur.archlinux.org/packages/yoshimi/)
*   [wineasio](https://aur.archlinux.org/packages/wineasio/)
*   [vst-bridge](https://github.com/abique/vst-bridge)

Смотрите также [List of applications (Русский)#Аудиосистемы](/index.php/List_of_applications_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#.D0.90.D1.83.D0.B4.D0.B8.D0.BE.D1.81.D0.B8.D1.81.D1.82.D0.B5.D0.BC.D1.8B "List of applications (Русский)"), [List of applications (Русский)#Редакторы аудио](/index.php/List_of_applications_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#.D0.A0.D0.B5.D0.B4.D0.B0.D0.BA.D1.82.D0.BE.D1.80.D1.8B_.D0.B0.D1.83.D0.B4.D0.B8.D0.BE "List of applications (Русский)"), и [awesome-linuxaudio](https://github.com/nodiscc/awesome-linuxaudio).

### Настройка системы

Могут оказаться полезными следующие часто используемые настройки системы:

*   Добавление себя в [группу](/index.php/Users_and_groups_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#.D0.93.D1.80.D1.83.D0.BF.D0.BF.D1.8B "Users and groups (Русский)") *audio*.
*   Добавление [параметра ядра](/index.php/Kernel_parameters_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Kernel parameters (Русский)") `threadirqs`.
*   Установка ядра [linux-rt](https://aur.archlinux.org/packages/linux-rt/).
*   Настройка регулятора [cpufreq](/index.php/CPU_frequency_scaling_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "CPU frequency scaling (Русский)") на *performance* (производительность).
*   Добавление параметра *noatime* в [fstab](/index.php/Fstab_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Fstab (Русский)") (смотрите [Improving performance#Mount options](/index.php/Improving_performance#Mount_options "Improving performance")).

Настройка в реальном времени в основном автоматизирована. Нет больше необходимости вносить правки в файлы вроде `/etc/security/limits.conf` для получения доступа реального времени. Тем не менее, если вам необходимо изменить настройки, смотрите `/etc/security/limits.d/99-audio.conf` и `/usr/lib/udev/rules.d/40-hpet-permissions.rules` (эти файлы поставляются с пакетами [jack](https://www.archlinux.org/packages/?name=jack) или [jack2](https://www.archlinux.org/packages/?name=jack2)). Дополнительно, вы можете захотеть увеличить максимально запрашиваемую частоту прерывания RTC (по умолчанию 64 Hz), запустив [следующее при загрузке системы](/index.php/Systemd_FAQ#How_can_I_make_a_script_start_during_the_boot_process.3F "Systemd FAQ"):

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

[qjackctl](https://www.archlinux.org/packages/?name=qjackctl), [cadence](https://aur.archlinux.org/packages/cadence/) и [patchage](https://www.archlinux.org/packages/?name=patchage) могут быть использованы как графическая оболочка для контроля за статусом JACK и упрощением его настройки.

**Примечание:** Как только вы закончите конфигурацию JACK, проверьте ваши настройки, запустив различные аудио приложения. Я потратил целый день, разбираясь с проблемой работы JACK xrun с LMMS, что в конце концов оказалось проблемой с последним.

*Дополнительная информация: [Linux Magazine article](http://www.linux-magazine.com/content/download/63041/486886/version/1/file/JACK_Audio_Server.pdf)*

#### FireWire

**Note:** Nothing much is needed to be done as most things have been automated, especially with the introduction of the [new FireWire stack](https://ieee1394.wiki.kernel.org/articles/j/u/j/Juju_Migration_e8a6.html), deprecation of HAL and more focus on [udev](/index.php/Udev "Udev"). You should not need to edit device permissions, but if you suspect that your device may not be working due to such issues, see `/lib/udev/rules.d/60-ffado.rules` and if needed, create and put your changes into `/etc/udev/rules.d/60-ffado.rules`.

JACK(2) is built against FFADO, you only need to install it with the [libffado](https://www.archlinux.org/packages/?name=libffado) package.

To test whether you have any chances of getting FireWire devices to work:

*   Ensure the proper kernel modules are loaded:

```
# modprobe firewire-core firewire-ohci

```

*   Is my chipset sane enough to initiate a device?

[http://www.ffado.org/?q=node/622](http://www.ffado.org/?q=node/622)

*   Is my chipset sane enough to make a device work to its capacity?

We cannot say for sure, particularly for those based on Ricoh (cross-platform issue). Most of the time, your device will run fine, but on occasion you will be faced with funny quirks. For unlucky ones, you will be facing hell.

**Note:** As stated by Takashi Sakamoto [on the alsa-devel mailing list](http://mailman.alsa-project.org/pipermail/alsa-devel/2014-September/081731.html), if you use the FireWire backend with jackd, the DICE module is incompatible. If you see a line like this :
```
Warning (dice_eap.cpp)[1811] read: No routes found. Base 0x7, offset 0x4000

```
you need to disable the "snd_dice" module.

#### Jack Flash

If after getting jack setup you will find that Flash has no audio.

In order to get flash to work with jack you will need to [install](/index.php/Install "Install") the [libflashsupport-jack](https://aur.archlinux.org/packages/libflashsupport-jack/) package.

You can also use more flexible method to allow Alsa programs (including Flash) play sound while jack is running:

First you must install the jack plugin for Alsa by [installing](/index.php/Installing "Installing") the [alsa-plugins](https://www.archlinux.org/packages/?name=alsa-plugins) package. Enable it by editing (or creating) `/etc/asound.conf` (system wide settings) to have these lines:

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

You do not need to restart your computer or anything. Just edit the alsa config files, start up jack.

#### Quickscan JACK script

Most people will probably want to run JACK in realtime mode, there are however a lot of knobs and buttons to press in order for that to happen.

A great way to quickly diagnose your system and find out what it is missing in order to have JACK work properly in real time mode is to run the Quickscan script.

[https://github.com/raboof/realtimeconfigquickscan/blob/master/realTimeConfigQuickScan.pl](https://github.com/raboof/realtimeconfigquickscan/blob/master/realTimeConfigQuickScan.pl)

The output should tell you where your system is lacking and will point you to places to find more information.

#### Desktop Effects vs JACK

In addition to the factors listed under the System Configuration section above as well as the settings checked by realTimeConfigQuickScan.pl, it is also worth noting that desktop environments can cause xruns and hence JACK audio glitches, especially memory/process intensive ones and those desktops that utilize composited desktop effects. It is recommended you disable desktop effects when using JACK. You are likely to get the least xruns and best performance by running a lightweight desktop or just a window manager instead.

#### Общий пример

Общий пример настройки доступен по ссылке [JACK Audio Connection Kit#A shell-based example setup](/index.php/JACK_Audio_Connection_Kit#A_shell-based_example_setup "JACK Audio Connection Kit").

## Realtime Kernel

Since a while ago, the stock Linux kernel has proven to be adequate for realtime uses. The stock kernel (with `CONFIG_PREEMPT=y`, default in Arch) can operate with a worst case latency of [upto 10ms](https://rt.wiki.kernel.org/index.php/Frequently_Asked_Questions#What_are_real-time_capabilities_of_the_stock_2.6_linux_kernel.3F) (time between the moment an interrupt occurs in hardware, and the moment the corresponding interrupt-thread gets running), although some device drivers can introduce latency much worse than that. So depending on your hardware and driver (and requirement), you might want a kernel with hard realtime capabilities.

The [RT_PREEPMT](https://rt.wiki.kernel.org/index.php/RT_PREEMPT_HOWTO) patch by Ingo Molnar and Thomas Gleixner is an interesting option for hard and firm realtime applications, reaching from professional audio to industrial control. Most audio-specific distro Linux ships with this patch applied. A realtime-preemptible kernel will also make it possible to tweak priorities of IRQ handling threads and help ensure smooth audio almost regardless of the load.

If you are going to compile your own kernel, remember that removing modules/options does not equate to a "leaner and meaner" kernel. It is true that the size of the kernel image is reduced, but in today's systems it is not as much of an issue as it was back in **1995**.

In any way, you should also ensure that:

*   **Timer Frequency** is set to **1000Hz** (CONFIG_HZ_1000=y; if you do not do *MIDI* you can ignore this)
*   **APM** is **DISABLED** (CONFIG_APM=n; Troublesome with some hardware - default in x86_64)

If you truly want a slim system, we suggest you go your own way and deploy one with *static /devs*. You should, however, set your CPU architecture. Selecting "Core 2 Duo" for appropriate hardware will allow for a good deal of optimisation, but not so much as you go down the scale.

General issue(s) with (realtime) kernels:

*   Hyperthreading (if you suspect, disable in BIOS)

There are ready-to-run/compile patched kernels available in the ABS and AUR.

**Note:** Before you decide to use a patched kernel, see [http://jackaudio.org/faq/realtime_vs_realtime_kernel.html](http://jackaudio.org/faq/realtime_vs_realtime_kernel.html).

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

*   Известно, что некоторое USB аудио аппаратное обеспечение не работает с портами USB 3, попробуйте вместо этого использовать порты USB 2/1\.

*   Могут случаться ошибки IRQ, что создаёт проблемы. Пример, видео аппаратное обеспечение, резервирующее шину, приводящее к ненужным прерываниям в системном пути ввода-вывода. Смотрите обсуждение в [FFADO IRQ Priorities How-To](http://subversion.ffado.org/wiki/IrqPriorities). Если вы используете ядро реального времени или свежее ядро, вы можете использовать [rtirq](https://aur.archlinux.org/packages/rtirq/) для настройки приоритетов обработки потоков IRQ.

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

The M-Audio Fast Track Pro is an USB 4x4 audio interface, working at 24bit/96kHz. Due to limitation of USB 1, this device requires additional setup to get access to all its features. Device works in one of two configuration:

*   Configuration 1, or "Class compliant mode" - with reduced functionality, only 16bit, 48kHz, analogue input (2 channels) and digital/analogue output (4 channels).
*   Configuration 2 - with access to all features of interface.

Currently with stock kernel it runs in configuration 2, but if you want to make sure in what mode you are, you can check kernel log for entries:

```
usb-audio: Fast Track Pro switching to config #2
usb-audio: Fast Track Pro config OK

```

The interface also needs extra step of cofiguration to switch modes. It is done using option `device_setup` during module loading. The recommended way to setup the interface is using file in `modprobe.d`:

 `/etc/modprobe.d/ftp.conf` 
```
options snd_usb_audio vid=0x763 pid=0x2012 device_setup=XXX index=YYY enable=1

```

where `vid` and `pid` are vendor and product id for M-Audio Fast Track Pro, `index` is desired device number and `device_setup` is desired device setup. Possible values for `device_setup` are:

<caption>device modes</caption>
| device_setup value | bit depth | frequency | analog output | digital output | analog input | digital input | IO mode |
| 0x0 | 16 bit | 48kHz | + | + | + | + | 4x4 |
| 0x9 | 24 bit | 48kHz | + | + | + | - | 2x4 |
| 0x13 | 24 bit | 48kHz | + | + | - | + | 2x4 |
| 0x5 | 24 bit | 96kHz | * | * | * | * | 2x0 or 0x2 |

The 24 bit/96kHz mode is special: it provides all input/output, but you can open only one of 4 interfaces at a time. If you for example open output interface and then try to open second output or input interface, you will see error in kernel log:

```
cannot submit datapipe for urb 0, error -28: not enough bandwidth

```

which is perfectly normal, because this is USB 1 device and cannot provide enough bandwidth to support more than single (2 channel) destination/source of that quality at a time.

Depending on the value of `index` it will setup two devices: `hwYYY:0` and `hwYYY:1`, which will contain available inputs and outputs. First device is most likely to contain analog output and digital input, while second one will contain analog input and digital output. To find out which devices are linked where and if they are setup correctly, you can check `/proc/asound/cardYYY/stream{0,1}` . Below is list of important endpoints that will help in correctly identifying card connections (it easy to mistake analog and digital input or output connections before you get used to the device):

```
EP 3 (analgoue output = TRS on back, mirrored on RCA outputs 1 and 2 on back)
EP 4 (digital output = S/PDIF output on back, mirrored on RCA outputs 3 and 4 on back)
EP 5 (analogue input = balanced TRS or XLR microphone, unbalanced TS line on front)
EP 6 (digital input = S/PDIF input on back)

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

1.  Startup: Either from command line or QjackCtl, the driver is called firewire.
2.  Specs: The card contains 8/8 preamp'ed XLR plus a stereo pair, in total 10 channels.
3.  Linking: Cards can be linked together without any problems.
4.  Hardware Settings: Nothing particular, tweak the settings in QjackCtl to your likings.

Volume levels are hardware and routing can be done through QjackCtl, even with more cards linked together, this is not a problem. The ffadomixer does not work with this card yet, hopefully in the future we can control more aspects of the card through a software interface like that.

### PreSonus AudioBox USB

1.  Startup: ALSA именует устройство как "USB".
2.  Specs: Два моно входа TRS+XLR, два моно выхода TRS, MIDI вход и выход, плюс отдельный стерео канал для наушников. Присутствуют регуляторы для управления обоими входами, основным выходом, и для наушников, всего четыре.
3.  Hardware: Работает очень хорошо, и аудио и MIDI. Не управляется программным микшером.

### Tascam US-122

***This does not apply to the US-122L***

1.  Required packages: [alsa-tools](https://www.archlinux.org/packages/?name=alsa-tools) [alsa-firmware](https://www.archlinux.org/packages/?name=alsa-firmware) [fxload](https://aur.archlinux.org/packages/fxload/)
2.  udev rules: create the following rules file, then reload udev rules, [Udev#Loading new rules](/index.php/Udev#Loading_new_rules "Udev")

 `/etc/udev/rules.d/51-tascam-us-122.rules` 
```
SUBSYSTEMS=="usb", ACTION=="add", ATTRS{idProduct}=="8006", ATTRS{idVendor}=="1604", RUN+="/bin/sh -c '/sbin/fxload -D %N -s /usr/share/alsa/firmware/usx2yloader/tascam_loader.ihx -I /usr/share/alsa/firmware/usx2yloader/us122fw.ihx'"
SUBSYSTEMS=="usb", ACTION=="add", ATTRS{idProduct}=="8007", ATTRS{idVendor}=="1604", RUN+="/bin/sh -c '/usr/bin/usx2yloader'"

```

Plug in the unit The device should now be working, there are no software mixer controls

### RME Babyface

It works very well at low latencies (~5ms) with [alsa-utils](https://www.archlinux.org/packages/?name=alsa-utils), [jack2](https://www.archlinux.org/packages/?name=jack2) and [linux-rt](https://aur.archlinux.org/packages/linux-rt/). Running on ALSA only with the standard kernel may cause crackling at lower latencies.

To be recognized and work, the firmware version of the Babyface needs to be >= 200, which introduces the Class Compliant Mode. To enter Class Compliant Mode hold the "Select" and "Recall" buttons while connecting the Babyface to the computer via USB. It should now be recognized.

To check if it is recognized:

```
grep -i baby /proc/asound/cards

```

For more info about the Class Compliant Mode visit RME's website, they have PDF which covers all the functionality.

The Babyface does not need any special Jack Settings. But if you want to use the built in MIDI In/Out then you need to set the "MIDI Driver" to "seq" and optionally disable "Enable Alsa Sequencer Support" to use it in combination with other MIDI Devices (a USB Midi Keyboard for example).

## Restricted Software

### Steinberg's SDKs

It is very clear - we can distribute neither the VST nor the ASIO headers in **binary package form**. However, whenever you are building a program which would host Windows *.dll* VST plug-ins, check for the following hints (that do not require use of any SDK):

*   dssi-vst
*   fst
*   vestige

With that said, if you are building a program which would host native *.so* VST plug-ins, then there is no escape. For such cases, Arch yet again allows us to maintain a uniform local software database. We can "install" the SDK *system-wide* - you simply have to download it yourself and place it in the packaging directory.

[Get them from AUR](https://aur.archlinux.org/packages.php?O=0&K=steinberg-&do_Search=Go)

*Note: Steinberg does not forbid redistribution of resulting products, nor dictate what license they can be under. There are many GPL-licensed VST plug-ins. As such, distributing binary packages of software built with these restricted headers is **not** a problem, because the headers are simply **buildtime dependencies**.*

## Arch Linux Pro Audio Project

Yes, we have one. Think of "Planet CCRMA" or "Pro Audio Overlay", less the academic connotations of the former: [ArchAudio](http://archaudio.org).

What this means is that the repositories are add-ons, i.e you need to have a running, sane Arch Linux installation.

It is a relatively new effort although the initiative has been around since 2006/2007\.

History: [https://bbs.archlinux.org/viewtopic.php?id=30547](https://bbs.archlinux.org/viewtopic.php?id=30547)

For all your Arch- and ArchAudio-related audio issues hop on to **IRC**: #archaudio @ Freenode

## Linux и Arch Linux Pro Audio в новостях

*   [Построй систему для производства серьёзной мультимедиа продукции с Arch](https://www.linux.com/learn/tutorials/607117-build-a-serious-multimedia-production-workstation-with-arch-linux) - Linux.com статья, июль 2012

*   [Практика использования Arch](http://www.linuxjournal.com/content/arch-tale) - Статья от музыканта и писателя Dave Phillips, октябрь 2011

*   [С Windows на Linux: разумное решение](http://www.itwire.com/opinion-and-analysis/open-sauce/36698-from-windows-to-linux-a-sound-decision) - интервью с Geoff "songshop" Beasley, февраль 2010

## Mailing list

*   [Linux-audio-user -- A list for linux audio users](http://lists.linuxaudio.org/listinfo/linux-audio-user) The Linux pro-audio related mailing list with much traffic and a huge subscriber community of users and developers.