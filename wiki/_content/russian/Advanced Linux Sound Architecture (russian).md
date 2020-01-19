Ссылки по теме

*   [ALSA configuration examples](/index.php/ALSA_configuration_examples "ALSA configuration examples")
*   [ALSA troubleshooting](/index.php/ALSA_troubleshooting "ALSA troubleshooting")
*   [Звуковая система](/index.php/%D0%97%D0%B2%D1%83%D0%BA%D0%BE%D0%B2%D0%B0%D1%8F_%D1%81%D0%B8%D1%81%D1%82%D0%B5%D0%BC%D0%B0 "Звуковая система")
*   [Динамик ПК](/index.php/%D0%94%D0%B8%D0%BD%D0%B0%D0%BC%D0%B8%D0%BA_%D0%9F%D0%9A "Динамик ПК")
*   [PulseAudio (Русский)](/index.php/PulseAudio_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "PulseAudio (Русский)")
*   [Open Sound System](/index.php/Open_Sound_System "Open Sound System")

[Advanced Linux Sound Architecture](https://en.wikipedia.org/wiki/Advanced_Linux_Sound_Architecture "wikipedia:Advanced Linux Sound Architecture") (**ALSA**) — компонент ядра Linux, который заменил оригинальную Open Sound System (OSSv3) в обеспечении драверов для звуковых карт. В отличие от драйверов звуковых карт, **ALSA** также содержит пользовательские библиотеки для разработчиков приложений, которые хотят использовать возможности драйвера для высокоуровневых API, что напрямую связаны с драйверами ядра.

**Примечание:** Для альтернативного звукового окружения, обратитесь к статье [Open Sound System](/index.php/Open_Sound_System "Open Sound System").

Этот документ описывает процесс **настройки ALSA**, в частности, для ядра версии 2.6.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Установка](#Установка)
    *   [1.1 Пользовательские утилиты](#Пользовательские_утилиты)
*   [2 Включить звук каналов](#Включить_звук_каналов)
*   [3 Настройка](#Настройка)
    *   [3.1 Основы синтаксиса](#Основы_синтаксиса)
        *   [3.1.1 Назначения и Разделители](#Назначения_и_Разделители)
        *   [3.1.2 Типы данных](#Типы_данных)
        *   [3.1.3 Режимы работы](#Режимы_работы)
            *   [3.1.3.1 Пример установок основного устройства использующего узел "defaults"](#Пример_установок_основного_устройства_использующего_узел_"defaults")
        *   [3.1.4 Гнездование](#Гнездование)
        *   [3.1.5 Including configuration files](#Including_configuration_files)
    *   [3.2 Установка звуковой карты по умолчанию](#Установка_звуковой_карты_по_умолчанию)
        *   [3.2.1 Выбор стандартной PCM с помощью переменной окружения](#Выбор_стандартной_PCM_с_помощью_переменной_окружения)
        *   [3.2.2 Другой способ](#Другой_способ)
    *   [3.3 Проверка на правильность загруженных модулей](#Проверка_на_правильность_загруженных_модулей)
    *   [3.4 Getting S/PDIF output](#Getting_S/PDIF_output)
    *   [3.5 System-wide equalizer](#System-wide_equalizer)
        *   [3.5.1 Using ALSAEqual (provides UI)](#Using_ALSAEqual_(provides_UI))
            *   [3.5.1.1 Managing ALSAEqual states](#Managing_ALSAEqual_states)
        *   [3.5.2 Using mbeq](#Using_mbeq)
*   [4 Старые методы настройки](#Старые_методы_настройки)
    *   [4.1 Проверка загруженных модулей](#Проверка_загруженных_модулей)
    *   [4.2 Выставление звука на каналах и проверка звуковой карты](#Выставление_звука_на_каналах_и_проверка_звуковой_карты)
    *   [4.3 Настройка прав](#Настройка_прав)
    *   [4.4 Восстановление звуковых настроек при загрузке](#Восстановление_звуковых_настроек_при_загрузке)
    *   [4.5 Настройка вывода через SPDIF](#Настройка_вывода_через_SPDIF)
    *   [4.6 KDE](#KDE)
*   [5 Высокое качество передискретизации](#Высокое_качество_передискретизации)
*   [6 Разложение/сведение каналов](#Разложение/сведение_каналов)
    *   [6.1 Разложение каналов](#Разложение_каналов)
    *   [6.2 Сведение каналов](#Сведение_каналов)
*   [7 Проблемы](#Проблемы)
    *   [7.1 Эмуляция работы OSS драйвера для ALSA](#Эмуляция_работы_OSS_драйвера_для_ALSA)
    *   [7.2 Если у вас всё ещё нет звука](#Если_у_вас_всё_ещё_нет_звука)
    *   [7.3 Плохое качество звука](#Плохое_качество_звука)
    *   [7.4 Нет звука на установленной S/PDIF видеокарте](#Нет_звука_на_установленной_S/PDIF_видеокарте)

## Установка

ALSA включена в стандартную сборку ядра Arch Linux ([linux](https://www.archlinux.org/packages/?name=linux)) в качестве набора модулей, поэтому ручная установка не требуется. Если вы компилируете ядро самостоятельно, не забудьте включить ALSA модуль, который вам нужен.

[udev](/index.php/Udev "Udev") автоматически определит ваше железо при загрузке, загрузив соответсвующий модуль ядра для вашей звуковой карты. Никакой особой настройки не требуется, если вы не используете ISA карты. Итак, ваш звук уже работает, но заглушён (по умолчанию).

Пользователи вошедшие в систему (в виртуальном терминале или менеджере рабочего стола) имеют права на проигрывание звука и изменение уровней микшера. Для разрешения таких прав удалённому пользователю, оный должен быть [заключён](/index.php/Users_and_groups#Group_management "Users and groups") в группу `audio`. Членство в группе `audio` также дает непосредственный доступ к устройствам и позволяет исключительный захват устройства вывода. Это может вывести из строя програмное микширование или быстрое переключение пользователей на многопользовательских системах. Поэтому добавление пользователя в группу `audio` строго **не** рекомендуется, если на то нет особых причин [[1]](https://wiki.ubuntu.com/Audio/TheAudioGroup).

Никогда не используйте *alsaconf*, если у вас PCI или ISAPNP звуковая карта: строчки, добавленные в `modprobe.conf`, могут сломать автоопределение [udev](/index.php/Udev_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Udev (Русский)").

### Пользовательские утилиты

[Установите](/index.php/%D0%A3%D1%81%D1%82%D0%B0%D0%BD%D0%BE%D0%B2%D0%B8%D1%82%D0%B5 "Установите") пакет [alsa-utils](https://www.archlinux.org/packages/?name=alsa-utils) из [официального репозитория](/index.php/Official_repositories_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Official repositories (Русский)"), который (помимо других утилит) содержит программу `alsamixer` и `amixer`.

```
 # pacman -S alsa-lib alsa-utils

```

*alsamixer* предлагает основанный на [ncurses](https://en.wikipedia.org/wiki/Ncurses "wikipedia:Ncurses") интерфейс для консольной настройки звуковых устройств. Так же установите пакет [alsa-plugins](https://www.archlinux.org/packages/?name=alsa-plugins) если желаете [высокое качество передискретизации](#Высокое_качество_передискретизации), возможность [разложения/сведения каналов](#Разложение/сведение_каналов) и другие возможности.

Если вы желаете что бы приложения [OSS](/index.php/OSS "OSS") работали с [dmix](#Dmix) установите так же пакет [alsa-oss](https://www.archlinux.org/packages/?name=alsa-oss).

```
 # pacman -S alsa-oss

```

Загрузите [модули ядра](/index.php/Kernel_modules_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Kernel modules (Русский)") `snd_seq_oss`, `snd_pcm_oss` и `snd_mixer_oss` для эмуляции OSS.

**Примечание:** Начиная с udev>=171, OSS-модули, по-умолчанию, автоматически не загружаются. При необходимости загрузите вручную: sudo modprobe snd-mixer-oss и добавьте в /etc/rc.conf, в секцию модулей: MODULES=(... snd-mixer-oss). Например, TVtime использует snd-mixer-oss для программного управления звуком

У всех alsa программ в качестве зависимости есть alsa-lib.

## Включить звук каналов

В ALSA по умолчанию отключены все каналы, и они все должны быть включены вручную. Этого можно добиться при помощи *amixer*:

```
$ amixer sset Master unmute

```

Так же есть возможность сделать то же самое с *alsamixer*:

```
$ alsamixer

```

Знак `MM` снизу канала показывает что канал отключён (*muted*), а `00` показывает что открыт (*open*).

Пролистайте до каналов `Master` и `PCM`при помощи клавиш `←` и `→` и включите звук на них, нажав клавишу `m`. Используйте клавишу `↑` для увеличения звука и достижения уровня в `0` dB (Децибел). Уровень может быть найден в верхнем левом поле, следующим за `Item:`.

**Примечание:** Если уровень выставить более 0 dB может быть слышен хрип из колонок.

Что бы получить полноценный 5.1 или 7.1 *surround sound* вам скорее всего понадобится включить каналы `Front`, `Surround`, `Center`, `LFE` (сабвуфер) и `Side` (это названия каналов, характерные для Intel HD Audio, они могут отличатся на различных устройствах). Стоит отметить, что это не даёт автоматического разложения на каналы стерео звука (каким является большинство музыки). Что бы задействовать такие возможности, смотрите [Разложение/сведение каналов](#Разложение/сведение_каналов).

Для включения микрофона, переключитесь на вкладку Capture (Устройства захвата) нажав `F4` и включите канал, нажав `Пробел`.

Для выхода из *alsamixer*, нажмите `Esc`.

**Примечание:**

*   На некоторых картах нужно заглушить цифровой выход, что бы слышать аналоговый звук. Для Soundblaster Audigy LS заглушите канал, подписанный `IEC958`.
*   На некоторых машинах, (как Thinkpad T61), есть канал `Speaker`, который должен быть включён и на нём поднят уровень.
*   На некоторых машинах, (как Dell E6400) так же потребуется включить и настроить каналы `Front` и `Headphone`.
*   Если ваши настройки звука пропадают после перезагрузки, попробуйте запустить alsamixer от суперпользователя.

Далее, проверим работу звука:

```
$ speaker-test -c 2

```

Измените `-c` по количеству колонок. Используйте `-c 8` для 7.1, например:

```
$ speaker-test -c 8

```

Если звук выходит через не то устройство, попробуйте в ручную указать их с аргументом `-D`.

```
$ speaker-test -D default -c 8

```

`-D` принимает названия каналов PCM, которые могут быть получены при запуске:

 `$ aplay -L | grep :CARD` 
```
default:CARD=PCH  # 'default' это название канала PCM
sysdefault:CARD=PCH
front:CARD=PCH,DEV=0
surround21:CARD=PCH,DEV=0
surround40:CARD=PCH,DEV=0
surround41:CARD=PCH,DEV=0
surround50:CARD=PCH,DEV=0
surround51:CARD=PCH,DEV=0
surround71:CARD=PCH,DEV=0
```

Если это не сработало, посмотрите разделы [Настройка](#Настройка) и [Проблемы](#Проблемы).

Пакет [alsa-utils](https://www.archlinux.org/packages/?name=alsa-utils) включает конфигурационные файлы [systemd](/index.php/Systemd_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Systemd (Русский)") `alsa-restore.service` и `alsa-store.service`, которые запускаются при старте системы и перед выключением, соответственно. Их не нужно вручную активировать через `systemctl`. Напоминаем, ALSA хранит свои настройки в `/var/lib/alsa/asound.state`.

## Настройка

### Основы синтаксиса

Файлы настройки ALSA следуют простому синтаксису, из иерархично расположенных значений для назначенных параметров (ключей). Ниже приведены (изменённые) отрывки из asoundrc.txt, который обычно находится в пакете `alsa-lib`, но может быть взят и [тут](http://www.alsa-project.org/alsa-doc/alsa-lib/conf.html).

#### Назначения и Разделители

Назначения определяют значение данного ключа. Достуаны различные стили и типы назначений.

 `Simple assignment` 
```
# Это комментарий. Всё после символа '#' до конца строки игнорируется ALSA.
key = value # Знак равно, как правило, опускают, поскольку пробел также может быть использован в качестве разделителя.

key value # Эквивалентно примеру выше.
```

Разделители используются для определения начала и конца назначений, использование запятых и пробелов также возможно.

 `Seperators` 
```
# Следующие три назначения одинаковы.
key value0; key valueN;
key value0, key valueN,
key value0 key valueN

key
value0
	key
valueN
```

Сложные назначения используют фигурные скобки в качестве разделителя.

 `Compound assignment` 
```
key {	subkey0 value0;
	subkeyN valueN;	}

key.subkey0 value0; # Эквивалентно примеру выше.
key.subkeyN valueN;
```

Для лёгкого понимания, рекомендуется использовать первый стиль в определениях, содержащих более трех значений.

Массив определений использует квадратные скобки в качестве разделителя.

 `Single array` 
```
key [	"value0";
	"valueN";	]

key.0 "value0"; # Эквивалентно примеру выше.
key.N "valueN";
```

Зависит от предпочтений пользователя,как оформлять настройки в различных стилях, главное не смешивать различные способы. Более полная информация базовых настроек можно найти [тут](http://www.volkerschatz.com/noise/alsa.html#basicconf).

#### Типы данных

ALSA использует различные типы данных для значений параметров, которые устанавливаются в пользовательских файлах настроек. Некоторые ключи принимают множественные типы данных, но многие - нет. Список опций настроек и их соответствующих аргументов для плагина PCM можно найти [тут](http://www.alsa-project.org/alsa-doc/alsa-lib/pcm_plugins.html)

#### Режимы работы

Есть несколько различных режимов работы для парсинга узлов, основные режимы соеденить и создать. Если режим работы один из соединить/создать или соединить делается проверка типов. Только данные одного типа могут быть соединены, так что строки не могут быть соединены с числовыми значениями. Попытка определить простое значение в основном режиме работы с соединением (и наоборот) также не работает.

Префиксы для режимов работы:

*   "+" -- соединить и создать
*   "-" -- соединить
*   "?" -- не замещать
*   "!" -- заместить

 `Operation modes` 
```
# Соединить/создать - Если узел не существует, он будет создан. Если он создан и типы совпадают,
# subkeyN присоединится в ключ.
key.subkeyN valueN;

# Соединить/создать - эквивалентно примеру выше
key.+subkeyN valueN;

# Соединить - Узел key.subkeyN должен уже существовать и быть того же типа данных
key.-subkeyN valueN;

# Не замещать - Игнорировать новое присвоение, если узел key.subkeyN уже существует
key.?subkeyN valueN;

# Замещение - Удаляет subkeyN и все ключи ниже, затем создаёт узел key.subkeyN
key.!subkeyN valueN;
```

Использование режима замещения, если все сделано правильно, как правило, безопасно, однако следует иметь в виду, возможно, для правильного функционирования, следует указать и другие необходимые ключи в узле.

**Важно:** Замещение узла pcm само по себе делает работу alsa нестабильной, поскольку определения всех плагинов будут удалены. Так что **не используйте !pcm.key** пока создаёте настройки на боевой машине.

##### Пример установок основного устройства использующего узел "defaults"

Подразумевая что узел "defaults" прописан в /usr/share/alsa/alsa.conf, где defaults.pcm.card и его ctl дубликат имеет прописанные значения "0" (тип integer), пользователь желает прописать основным pcm и управляющим устройством карту "2" или "SB" на звуковой карте Azalia.

 `Defaults node` 
```
defaults.ctl.card 2; # Установит основное устройство и отдаст контроль третьей карте (счёт начинается с 0).
defaults.pcm.card 2; # Это не меняет тип данных.

defaults.ctl.+card 2; # Эквивалентно написанному выше.
defaults.pcm.+card 2;

defaults.ctl.-card 2; # Такой же эффект, как от настроек по умолчанию, но если узел defaults был удалён или
defaults.pcm.-card 2; # тип был изменён через операцию слияния не получить результата.

defaults.pcm.?card 2; # Это не сделает ничего, поскольку данное назначение уже существует.
defaults.ctl.?card 2;

defaults.pcm.!card "SB"; # Операция перезаписи нужна, поскольку тут
defaults.ctl.!card "SB"; # различные типы значений.
```

Использование двойных кавычек тут автоматически устанавливает значения данных в "строку (string)", так в примере выше установка defaults.pcm.!card "2" приведёт к результату удерживания последнего устройства по умолчанию, в данном случае карты 0\. Использование двойных кавычек для строк не обязательно, пока не используются спецсимволы,что в идеале никогда не должно произойти. Это может быть недействительным для других назначений.

**Примечание:** С точки зрения настройки, не равнозначна установка связи устройства "default" pcm, поскольку большинство пользователей так же указывают тип адресации тут, что почти тоже самое, но назначение само по себе отличается. Так же defaults.pcm.card упоминается много раз в файлах настройки alsa, обычно как резервное назначение, где различные переменные окружения имеют приоритет.

#### Гнездование

Иногда полезно и даже легче прочитать об использовании гнездования в настройках.

 `Гнездование плагинов PCM` 
```
pcm.azalia {	type hw; card 0	}
pcm.!default {	type plug; slave.pcm "azalia"	}

# что равнозначно

pcm.!default {	type plug; slave.pcm {	type hw; card 0;	}	}

# что так же равнозначно

pcm.!default.type plug;
pcm.default.slave.pcm.type hw;
pcm.default.slave.pcm.card 0;
```

#### Including configuration files

 `Include other configuration files` 
```
</path/to/configuration-file> # Include a configuration file
<confdir:/path/to/configuration-file> # Reference to a global configuration directory
```

### Установка звуковой карты по умолчанию

Если ваша звуковая карта меняет порядок при загрузке, вы можете указать их порядок в любом файле, который заканчивается на `.conf` в `/etc/modprobe.d` (`/etc/modprobe.d/alsa-base.conf` предложенный). Например, если вы хотите, чтобы ваша звуковая карта Mia была #0:

 `/etc/modprobe.d/alsa-base.conf` 
```
options snd_mia index=0
options snd_hda_intel index=1
```

Используйте `$ cat /proc/asound/modules` чтобы получить загруженные звуковые модули и их порядок. Этот список, в большинсте случев, все, что вам нужно для загрузки порядка. Используйте `$ lsmod | grep snd` чтобы получить список устройств и модулей. Эта конфигурация предполагает, что у вас есть одна звуковая карта Mia, которая использует `snd_mia` и одна (напр. встроенная) карта использующая `snd_hda_intel`.

Вы также можете задать индекс `-2`, чтобы заставить ALSA никогда не использовать звуковую карту, как первичную. Дистрибутивы, такие как Linux Mint и Ubuntu используют следующие настройки, чтобы USB и другие "неправильные" драйвера не получили индекс `0`:

 `/etc/modprobe.d/alsa-base.conf` 
```
options bt87x index=-2
options cx88_alsa index=-2
options saa7134-alsa index=-2
options snd-atiixp-modem index=-2
options snd-intel8x0m index=-2
options snd-via82xx-modem index=-2
options snd-usb-audio index=-2
options snd-usb-caiaq index=-2
options snd-usb-ua101 index=-2
options snd-usb-us122l index=-2
options snd-usb-usx2y index=-2
options snd-pcsp index=-2
options snd-usb-audio index=-2
```

Эти изменения требуют перезагрузки системы.

Смотрите также [[2]](https://bbs.archlinux.org/viewtopic.php?pid=1446773#p1446773)

#### Выбор стандартной PCM с помощью переменной окружения

В вашем файле конфигурации, предпочитается общий, добавьте:

```
pcm.!default {
    type plug
    slave.pcm {
        @func getenv
        vars [ ALSAPCM ]
        default "hw:Audigy2"
    }
}
```

Вам необходимо заменить линию по умолчанию с именем вашей карты (в примере `Audigy2`). Вы можете получить имена, используя `aplay -l` или вы можете также использовать PCM. Но если вам нужно использовать микрофон, будет хорошей идеей выбрать полный дуплекс PCM по умолчанию.

Теперь вы можете запускать программы с выбором звуковой карты, изменяя только переменную окружения `ALSAPCM`. Это работает для всех програм, которые не позволяют выбрать карту, для других убедитесь, что вы используете карту по умолчанию. Например, при условии, что вы напишете понижающее микширование PCM, которе будет иметь название `mix51to20` вы можете использовать его с [mplayer](https://www.archlinux.org/packages/?name=mplayer) используя командную строку `ALSAPCM=mix51to20 mplayer example_6_channel.wav`

Вместо использования новых переменных, вы можете установить одну из упомянутых в общей конфигурации по умолчанию.

 `/usr/share/alsa/alsa.conf` 
```
Variable name # Definition
ALSA_CARD # pcm.default pcm.hw pcm.plughw ctl.sysdefault ctl.hw rawmidi.default rawmidi.hw hwdep.hw
ALSA_CTL_CARD # ctl.sysdefault ctl.hw
ALSA_HWDEP_CARD # hwdep.default hwdep.hw
ALSA_HWDEP_DEVICE # hwdep.default hwdep.hw
ALSA_PCM_CARD # pcm.default pcm.hw pcm.plughw
ALSA_PCM_DEVICE # pcm.hw pcm.plughw
ALSA_RAWMIDI_CARD # rawmidi.default rawmidi.hw
ALSA_RAWMIDI_DEVICE # rawmidi.default rawmidi.hw
```

**Примечание:** Обратите внимание на тип адресации по умолчанию.

#### Другой способ

**Совет:** Этот процесс может быть частично автоматизирован с использованием [asoundconf](https://www.archlinux.org/packages/?name=asoundconf) из [Arch User Repository](/index.php/AUR_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "AUR (Русский)").

Сперва Вам нужно найти карту и id устройства, которое Вы хотите установить по-умолчанию:

 `$ aplay -l` 
```
**** List of PLAYBACK Hardware Devices ****
card 0: Intel [HDA Intel], device 0: CONEXANT Analog [CONEXANT Analog]
  Subdevices: 1/1
  Subdevice #0: subdevice #0
card 0: Intel [HDA Intel], device 1: Conexant Digital [Conexant Digital]
  Subdevices: 1/1
  Subdevice #0: subdevice #0
card 1: JamLab [JamLab], device 0: USB Audio [USB Audio]
  Subdevices: 1/1
  Subdevice #0: subdevice #0
card 2: Audio [Altec Lansing XT1 - USB Audio], device 0: USB Audio [USB Audio]
  Subdevices: 1/1
  Subdevice #0: subdevice #0
```

**Важно:** Simply setting a `type hw` as default card is equivalent to addressing hardware directly, which leaves the device unavailable to other applications. This method is only recommended if it is a part of a more sophisticated setup `~/.asoundrc` or if user deliberately wants to address sound card directly (digital output through `eic958` or dedicated music server for example).

For example, the last entry in this list has the card ID 2 and the device ID 0\. To set this card as the default, you can either use the system-wide file `/etc/asound.conf` or the user-specific file `~/.asoundrc`. You may have to create the file if it does not exist. Then insert the following options with the corresponding card.

```
pcm.!default {
    type hw
    card 2
}

ctl.!default {
    type hw
    card 2
}

```

**Примечание:** For the Asus U32U serie it seems that card should be set to 1 for both pcm and ctl.

In most cases it is recommended to use sound card names instead of number references, which also solves boot order problem. Therefore the following would be correct for the above example.

```
pcm.!default {
    type hw
    card Audio
}

ctl.!default {
    type hw
    card Audio
}

```

To get valid ALSA card names, use *aplay*:

 `$ aplay -l | awk -F \: '/,/{print $2}' | awk '{print $1}' | uniq` 
```
PCH

```

Alternatively use *cat*, which might return unused devices:

 `$ cat /proc/asound/card*/id` 
```
PCH
ThinkPadEC

```

**Примечание:** This method could be problematic if your system has several cards of the same (ALSA)name.

The 'pcm' options affect which card and device will be used for audio playback while the 'ctl' option affects which card is used by control utilities like alsamixer .

The changes should take effect as soon as you (re-)start an application (MPlayer etc.). You can also test with a command like *aplay*.

```
$ aplay -D default *your_favourite_sound.wav*

```

If you receive an error regarding your asound configuration, check the [upstream documentation](http://www.alsa-project.org/main/index.php/Asoundrc#The_default_plugin) for possible changes to the config file format.

### Проверка на правильность загруженных модулей

Вы можете предполагать, что udev определил ваш звук правильно. Проверить это можно, используя командную строку.

 `$ lsmod | grep '^snd' | column -t` 
```
snd_hda_codec_hdmi     22378   4
snd_hda_codec_realtek  294191  1
snd_hda_intel          21738   1
snd_hda_codec          73739   3  snd_hda_codec_hdmi,snd_hda_codec_realtek,snd_hda_intel
snd_hwdep              6134    1  snd_hda_codec
snd_pcm                71032   3  snd_hda_codec_hdmi,snd_hda_intel,snd_hda_codec
snd_timer              18992   1  snd_pcm
snd                    55132   9  snd_hda_codec_hdmi,snd_hda_codec_realtek,snd_hda_intel,snd_hda_codec,snd_hwdep,snd_pcm,snd_timer
snd_page_alloc         7017    2  snd_hda_intel,snd_pcm
```

Если вывод выглядит похожим, ваш звуковой драйвер был успешно автоопределен.

**Примечание:** Начиная с `udev>=171`, модули эмуляции OSS (`snd_seq_oss, snd_pcm_oss, snd_mixer_oss`) не загружаются по умолчанию: [Загрузите их вручную](/index.php/Kernel_modules_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#Loading "Kernel modules (Русский)") если это требуется.

Вы также можете проверить директорию `/dev/snd/` на правильность файлов устройств:

 `$ ls -l /dev/snd` 
```
total 0
crw-rw----  1 root audio 116,  0 Apr  8 14:17 controlC0
crw-rw----  1 root audio 116, 32 Apr  8 14:17 controlC1
crw-rw----  1 root audio 116, 24 Apr  8 14:17 pcmC0D0c
crw-rw----  1 root audio 116, 16 Apr  8 14:17 pcmC0D0p
crw-rw----  1 root audio 116, 25 Apr  8 14:17 pcmC0D1c
crw-rw----  1 root audio 116, 56 Apr  8 14:17 pcmC1D0c
crw-rw----  1 root audio 116, 48 Apr  8 14:17 pcmC1D0p
crw-rw----  1 root audio 116,  1 Apr  8 14:17 seq
crw-rw----  1 root audio 116, 33 Apr  8 14:17 timer
```

**Примечание:** Если нужна помощь в IRC или на форуме, пожалуйста отправляйте вывод выше указанных команд, если попросят.

Если вы имеете устройства **controlC0** и **pcmC0D0p** или аналогичные, тогда ваш звуковой модуль был обнаружен и загружен правильно.

Если этого не случилось, ваш звуковой модуль был обнаружен не правильно. Чтобы это исправить, вы можете попытаться загрузить модуль самостоятельно:

*   Найдите модуль вашей звуковой карты: [ALSA Soundcard Matrix](http://www.alsa-project.org/main/index.php/Matrix:Main) Модуль будет с префиксом 'snd-' (например: `snd-via82xx`).
*   [Загрузите модуль](/index.php/Kernel_modules_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#Loading "Kernel modules (Русский)").
*   Проверьте файлы устройства в `/dev/snd` (см. выше) и/или проверьте имеет ли `alsamixer` или `amixer` допустимый вывод.
*   Настройте `snd-NAME-OF-MODULE` и `snd-pcm-oss` на [загрузку при старте](/index.php/Kernel_modules#Loading "Kernel modules").

### Getting S/PDIF output

[S/PDIF](https://en.wikipedia.org/wiki/S/PDIF "wikipedia:S/PDIF") is a digital audio interface often used to connect a computer to a digital amplifier (such as a home theatre with 5.1/7.1 surround sound).

**Примечание:** With some soundcards this disables analog sound output (eg. Audigy2).

Depending on what [shell](/index.php/Shell "Shell") you use, add the following line to your shell's configuration file:

```
amixer -c 0 cset name='IEC958 Playback Switch' on

```

You can see the name of your card's digital output with:

```
$ amixer scontrols

```

### System-wide equalizer

#### Using ALSAEqual (provides UI)

Install the [alsaequal](https://aur.archlinux.org/packages/alsaequal/) package from the [Arch User Repository](/index.php/Arch_User_Repository "Arch User Repository").

**Примечание:** If you have a x86_64-system and are using a 32bit-flashplugin the sound in flash will not work. You have to disable alsaequal or build alsaequal for 32bit.

After installing the package, add the following to your ALSA configuration file:

 `/etc/asound.conf` 
```
ctl.equal {
    type equal;
}

pcm.plugequal {
    type equal;
    # Modify the line below if you do not
    # want to use sound card 0.
    #slave.pcm "plughw:0,0";
    # by default we want to play from more sources at time:
    slave.pcm "plug:dmix";
}

# pcm.equal {
# If you do not want the equalizer to be your
# default soundcard comment the following
# line and uncomment the above line. (You can
# choose it as the output device by addressing
# it with specific apps,eg mpg123 -a equal 06.Back_In_Black.mp3)
pcm.!default {
    type plug;
    slave.pcm plugequal;
}
```

And you are ready to change your equalizer using command

```
$ alsamixer -D equal

```

Note that configuration file is different for each user (until not specified else) it is saved in `~/.alsaequal.bin`. so if you want to use ALSAEqual with [mpd](/index.php/Mpd "Mpd") or another software running under different user, you can configure it using

```
$ su mpd -c 'alsamixer -D equal'

```

or for example, you can make a symlink to your `.alsaequal.bin` in his home...

##### Managing ALSAEqual states

Install [alsaequal-mgr](https://aur.archlinux.org/packages/alsaequal-mgr/) from the [Arch User Repository](/index.php/Arch_User_Repository "Arch User Repository").

Configure the equalizer as usual with

```
$ alsamixer -D equal

```

When you are satisfied with the state, you may give it a name ("foo" in this example) and save it:

```
$ alsaequal-mgr save foo

```

The state "foo" can then be restored at a later time with

```
$ alsaequal-mgr load foo

```

You can thus create different equalizer states for games, movies, music genres, VoIP apps, etc. and reload them as necessary.

See the [project page](http://xyne.archlinux.ca/projects/alsaequal-mgr/) and the help message for more options.

#### Using mbeq

**Примечание:** This method requires the use of a [LADSPA](https://en.wikipedia.org/wiki/LADSPA "wikipedia:LADSPA") plugin which might be CPU intensive during playback. In addition, this was made with stereophonic sound (e.g. headphones) in mind.

Install the [alsa-plugins](https://www.archlinux.org/packages/?name=alsa-plugins), [ladspa](https://www.archlinux.org/packages/?name=ladspa) and [swh-plugins](https://www.archlinux.org/packages/?name=swh-plugins) packages if you do not already have them.

If you have not already created either an `~/.asoundrc` or a `/etc/asound.conf` file, then create either one and insert the following:

 `/etc/asound.conf` 
```
pcm.eq {
    type ladspa

    # The output from the EQ can either go direct to a hardware device
    # (if you have a hardware mixer, e.g. SBLive/Audigy) or it can go
    # to the software mixer shown here.
    #slave.pcm "plughw:0,0"
    slave.pcm "plug:dmix"

    # Sometimes you may need to specify the path to the plugins,
    # especially if you have just installed them.  Once you have logged
    # out/restarted this should not be necessary, but if you get errors
    # about being unable to find plugins, try uncommenting this.
    #path "/usr/lib/ladspa"

    plugins [
    {
        label mbeq
        id 1197
        input {
            # The following setting is just an example, edit to your own taste:
            # bands: 50hz, 100hz, 156hz, 220hz, 311hz, 440hz, 622hz, 880hz, 1250hz, 1750hz, 25000hz,
            # 50000hz, 10000hz, 20000hz
            controls [ -5 -5 -5 -5 -5 -10 -20 -15 -10 -10 -10 -10 -10 -3 -2 ]
            }
        }
    ]
}

# Redirect the default device to go via the EQ - you may want to do
# this last, once you are sure everything is working.  Otherwise all
# your audio programs will break/crash if something has gone wrong.
pcm.!default {
    type plug
    slave.pcm "eq"
}

# Redirect the OSS emulation through the EQ too (when programs are running through "aoss")
pcm.dsp0 {
    type plug
    slave.pcm "eq"
}
```

## Старые методы настройки

### Проверка загруженных модулей

Вы можете рассчитывать, что udev автоматически найдёт вашу звуковую карту, включая модули совместимости OSS. Вы можете проверить это с помощью следующей команды:

```
$ lsmod|grep 'snd'
snd_usb_audio          69696  0 
snd_usb_lib            13504  1 snd_usb_audio
snd_rawmidi            20064  1 snd_usb_lib
snd_hwdep               7044  1 snd_usb_audio
snd_seq_oss            29412  0 
snd_seq_midi_event      6080  1 snd_seq_oss
snd_seq                46220  4 snd_seq_oss,snd_seq_midi_event
snd_seq_device          6796  3 snd_rawmidi,snd_seq_oss,snd_seq
snd_pcm_oss            45216  0 
snd_mixer_oss          15232  1 snd_pcm_oss
snd_intel8x0           27932  0 
snd_ac97_codec         87648  1 snd_intel8x0
snd_ac97_bus            1792  1 snd_ac97_codec
snd_pcm                76296  4 snd_usb_audio,snd_pcm_oss,snd_intel8x0,snd_ac97_codec
snd_timer              19780  2 snd_seq,snd_pcm
snd                    43776  12 snd_usb_audio,snd_rawmidi,snd_hwdep,snd_seq_oss,snd_seq,snd_seq_device,snd_pcm_oss,snd_mixer_oss,snd_intel8x0,snd_ac97_codec,snd_pcm,snd_timer
snd_page_alloc          7944  2 snd_intel8x0,snd_pcm

```

Если вывод имеет похожий вид, то ваши звуковые модули успешно обнаружились (обратите внимание, что в этом случае, snd_intel8x0 и snd_usb_audio являются драйверами для устройств). Вы также можете проверить каталог **/dev/snd** на правильные права:

```
$ ls -l /dev/snd/
total 0
crw-rw----  1 root audio 116,  0 Apr  8 14:17 controlC0
crw-rw----  1 root audio 116, 32 Apr  8 14:17 controlC1
crw-rw----  1 root audio 116, 24 Apr  8 14:17 pcmC0D0c
crw-rw----  1 root audio 116, 16 Apr  8 14:17 pcmC0D0p
crw-rw----  1 root audio 116, 25 Apr  8 14:17 pcmC0D1c
crw-rw----  1 root audio 116, 56 Apr  8 14:17 pcmC1D0c
crw-rw----  1 root audio 116, 48 Apr  8 14:17 pcmC1D0p
crw-rw----  1 root audio 116,  1 Apr  8 14:17 seq
crw-rw----  1 root audio 116, 33 Apr  8 14:17 timer

```

Если у вас есть хотя бы **controlC0** и **pcmC0D0p** или что-то похожее, то ваши звуковые модули обнаружились и загрузились правильно.

Если это не так, то ваши модули не были обнаружены. **Если вы хотите получить помощь на форумах или IRC, пожалуйста, введите вывод команд, использовавшихся выше.** Для решения этой ситуации вы можете попробовать загрузить модули вручную:

*   Узнайте имя модуля для вашей звуковой карты: [http://www.alsa-project.org/alsa-doc/](http://www.alsa-project.org/alsa-doc/) Модуль будет иметь префикс 'snd-' (например, 'snd-via82xx').
*   Загрузите модули:

```
 # modprobe snd-NAME-OF-MODULE
 # modprobe snd-pcm-oss

```

*   Проверьте файлы в **/dev/snd** (смотрите выше) и/или что **alsamixer** или **amixer** достаточный уровень звука.
*   Добавьте **snd-NAME-OF-MODULE** и **snd-pcm-oss** в список MODULES в **/etc/rc.conf**, чтобы они загрузились в следующий раз (удостоверьтесь, что **snd-NAME-OF-MODULE** находится перед **snd-pcm-oss**).

### Выставление звука на каналах и проверка звуковой карты

В этом разделе мы подразумеваем, что вы выполняете команды от суперпользователя. Если вы хотите выполнять эти шаги от пользователя, то перейдите сначала к следующей секции, *Настройка прав доступа*.

*   Включение звука

Рекомендуется использовать 'alsamixer' для настройки вашего микшера и включения звука на каналах.
**ОБРАТИТЕ ВНИМАНИЕ:** когда вы используете **alsamixer**, включите звук нажатием **M**, а не только повысьте уровень звука. **ОБРАТИТЕ ВНИМАНИЕ:** при использовании amixer для выставления уровня громкости следует использовать знак процента %. **amixer** понимает знак процента (%), а не числа.

```
 # amixer set Master 90% unmute
 # amixer set PCM 85% unmute

```

*   Попробуйте проиграть wav-файл:

```
 # aplay mywav.wav

```

**Примечание:** на некоторых карточках (как минимум, на Soundblaster Audigy LS) требуется отключить или заглушить цифровой выход, чтобы слушать аналоговый звук.

### Настройка прав

Для того чтобы можно было пользоваться звуковой картой пользователем, проделайте следующие шаги:

*   Добавьте пользователя в группу audio:

```
# gpasswd -a USERNAME audio

```

*   Выйдите пользователем из системы и войдите заново.

### Восстановление звуковых настроек при загрузке

*   Запустите 'alsactl' один раз, чтобы создать '/etc/asound.state':

```
alsactl store

```

*   Отредактируйте '/etc/rc.conf' и добавьте 'alsa' в список демонов, загружающихся при старте системы. Это позволит сохранять настройки микшера при каждом выключении системы и восстанавливать их при загрузке.

### Настройка вывода через SPDIF

(от **gralves** с форумов *Gentoo*)

*   В GNOME Volume Control, во вкладке Options, измените IEC958 на PCM. Эта опция может быть включена в настройках.
*   Если у вас не установлен GNOME Volume Control:
    *   Отредактируйте файл /etc/asound.state. В нём хранятся alsasound хранит настройки вашего микшера.
    *   Найдите строчку вида: 'IEC958 Playback Switch'. Рядом с ней вы найдёте строчку типа `value:false`. Измените её на `value:true`.
    *   Теперь найдите строчку 'IEC958 Playback AC97-SPSA' и измените её значение на 0.
    *   Перезапустите alsa.

Есть другой способ включить вывод через SPDIF автоматически при загрузке системы (проверено на SoundBlaster Audigy):

*   добавьте следующие строчки в /etc/rc.local:

```
 # Use COAX-digital output
 amixer set 'IEC958 Optical' 100 unmute
 amixer set 'Audigy Analog/Digital Output Jack' on

```

Вы можете увидеть имя цифрового выхода вашей карты с помощью:

```
 amixer scontrols

```

### KDE

*   Запустите KDE:

```
$ startx

```

*   Установите предпочитаемый уровень звука (у каждого пользователя сои настройки):

```
$ alsamixer

```

*   **KDE 3.5**. Зайдите в K Menu -> Multimedia -> KMix
    *   Выберите Settings > Configure KMix...
    *   Выключите опцию "Restore volumes on login"
    *   Нажмите OK. Теперь ваш уровень звука будет одинаковым как в командной строке, так и в KDE.

## Высокое качество передискретизации

Когда включено програмное микширование, ALSA вынуждена предесритезировать всё на единой частоте (48 kHz по умолчанию, если поддерживается). По умолчанию, она попытается использовать для этого конвертер *speexrate*, и откатится к низкому качеству линейной интерполяции, если не получится[[3]](http://git.alsa-project.org/?p=alsa-lib.git;a=blob;f=src/pcm/pcm_rate.c;h=2eb4b1b33933dec878d0f25ad118869adac95767;hb=HEAD#l1278). Таким образом, если вы получили некачественный звук из-за плохой передискретизации, проблема может быть решена путем простой установки [alsa-plugins](https://www.archlinux.org/packages/?name=alsa-plugins). Для еще более высокого качества передискретизации, вы можете изменить преобразователь частот по умолчанию на `speexrate_medium` или `speexrate_best`. Оба работают достаточно хорошо, что не имеет практического значения, какой вы выберите, и использование лучшего конвертера не стоит тех циклов процессора, которые он тратит.

Для смены преобразователя частот по умолчанию введите следующие строки в ваши `~/.asoundrc` или `/etc/asound.conf`:

 `/etc/asound.conf` 
```
defaults.pcm.rate_converter "speexrate_medium"

```

**Примечание:** Так же возможно использовать конвертер [libsamplerate](https://www.archlinux.org/packages/?name=libsamplerate), который в два раза медленее конвертеров *speexrate*, но даёт небольшой прирост в качестве. Смотрите [обсуждение](/index.php/Talk:Advanced_Linux_Sound_Architecture#On_high_quality_resampling "Talk:Advanced Linux Sound Architecture").

**Примечание:** Некоторые приложения (как MPlayer и его ответвления) настроены по умолчанию на собственную передискретизацию. Поскольку некоторые драйвера ALSA неправильно сообщают задержки, когда передискретизация включена (что ведет к рассинхронизации AV), изменение данных настроек не возымеет эффекта, пока вы не настроете их использовать передискретизацию от ALSA.

## Разложение/сведение каналов

### Разложение каналов

В случае, если вы желаете выпустить стерео звуки, например музыку, через 5.1 или 7.1 системы, вам нужно использовать разложение каналов. В стародавние времена это было сложно, баговано и крючкотворно, но в нашем светлом настоящем достаточно установить плагин, который позаботится об этом. Мы используем плагин `upmix`, входящий в сотав [alsa-plugins](https://www.archlinux.org/packages/?name=alsa-plugins).

Затем добавим следующие строки в ваши настройки ALSA (на выбор: `/etc/asound.conf` или `~/.asoundrc`):

```
pcm.upmix71 {
    type upmix
    slave.pcm "surround71"
    delay 15
    channels 8
}

```

Вы можете легко менять данный пример разложения на 7.1 для 5.1 (surround51) или 4.0 (surround40).

В данном примере добавляется новый канал PCM, который можно использовать для разложения. Если вы желаете направлять все источники звуков через данный канал, добавьте его в качестве основного, указав ниже предыдущего примера:

```
pcm.!default "plug:upmix71"

```

Плагин автоматически дозволяет множественным ресурсам проигрывать посредством себя без лишних проблем, так что установка его в качестве основного безопасна. Если данная настройка не работает, вам нужно установить собственный dmixer для разложения каналов PCM, как указано далее:

```
pcm.dmix6 {
    type asym
    playback.pcm {
        type dmix
        ipc_key 567829
        slave {
            pcm "hw:0,0"
            channels 6
        }
    }
}
```

и использовать "dmix6" вместо "surround71". Если вы слышите проглатывание или искажение звуков, попробуйте увеличить размер буфера buffer_size (до 32768, например) или использовать [высококачественную передискретизацию](#Высокое_качество_передискретизации).

### Сведение каналов

Если вы желаете сводить каналы в стерео звук, потому что вам, например, захотелось смотреть фильм со звуком 5.1 на стерео-системе: используйте плагин `vdownmix`, входящий в [alsa-plugins](https://www.archlinux.org/packages/?name=alsa-plugins).

И далее, в ваши файлы настроек добавьте:

```
pcm.!surround51 {
    type vdownmix
    slave.pcm "default"
}
pcm.!surround40 {
    type vdownmix
    slave.pcm "default"
}
```

**Примечание:** Этого может быть не достаточно для работы сведения каналов, смотри [баг](http://bugs.debian.org/cgi-bin/bugreport.cgi?bug=541786). Так что, вам может потребоваться добавить `pcm.!default "plug:surround51"` или `pcm.!default "plug:surround40"`. Только одно подключение `vdownmix` может быть использовано; если у вас 7.1-канальная система, вам потребуется использовать `surround71` вместо настроек, указанных выше. Хороший пример, показывающий работающие настройки для `vdownmix` и `dmix`, может быть найден [тут](https://bbs.archlinux.org/viewtopic.php?id=167275).

Пример конфига взятого [отсюда](https://bbs.archlinux.org/viewtopic.php?id=167275), но с включенным сведением и поддержкой внутрисистемного микшера alsaequal.

```
defaults.pcm.rate_converter "samplerate_best"

pcm.snd_card {
        type hw
        card 0
}

pcm.aout {
        type dmix
        ipc_key 1
        ipc_key_add_uid false
        ipc_perm 0660
        slave {
                pcm "snd_card"
                channels 2
        }
}

# Audio in
pcm.ain {
        type dsnoop
        ipc_key 2
        ipc_key_add_uid false
        ipc_perm 0660
        slave {
                pcm "snd_card"
                channels 2
        }
}

pcm.!surround71 {
        type vdownmix
        slave.pcm "aout"
}

pcm.asymed {
        type asym
        playback.pcm "surround71"
        capture.pcm  "ain"
        slave.pcm "equal"
}

ctl.equal {
    type equal;
}

pcm.plugequal {
    type equal;
    slave.pcm "plug:dmix";
}

pcm.!default {
        type plug
        slave.pcm "plugequal"
}
```

## Проблемы

### Эмуляция работы OSS драйвера для ALSA

Скачайте и распакуйте [архив с этой страницы](http://www.kote.ninja/news@1/2015-05-10/gorky18/). Установите его командами

```
make

```

затем

```
sudo make install

```

Затем запустите демон

```
sudo /usr/local/sbin/osspd

```

и дайте права появившимся устройствам. Затем запускайте любое OSS приложение.

### Если у вас всё ещё нет звука

Даже если ваши драйвера установлены корректно, выставлен правильный уровень звука, ничего не выключено, вы можете ничего не слышать! Добавление следующей строчки к `/etc/modprobe.d/modprobe.conf` решает эту проблемы (по крайней мере для модуля `via82xx`):

```
options snd-NAME-OF-MODULE ac97_quirk=0

```

### Плохое качество звука

Если качество звука у вас плохое, можете попробовать выставить такой уровень PCM (в alsamixer), чтобы gain был равен 0.

### Нет звука на установленной S/PDIF видеокарте

Посмотрите доступные модули и их порядок:

 `$ cat /proc/asound/modules` 
```
 0 snd_hda_intel
 1 snd_ca0106

```

Отключите нежелательный аудиокодек видеокарты в `/etc/modprobe.d/modprobe.conf`:

 `/etc/modprobe.d/modprobe.conf` 
```
install snd_hda_intel /bin/false

```

Если оба устройства используют одинаковый модуль, можно включить параметр `enable` в модуле snd_hda_intel; это массив логических значений что разрешают/запрещают работу желаемой звуковой карты.

```
options snd_hda_intel enable=1,0

```

Будьте внимательны к названию вашего устройства *snd**_**hda**_**intel* (подчеркивание) или *snd**-**hda**-**intel* (тире).