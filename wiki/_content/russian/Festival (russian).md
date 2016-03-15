[Festival](http://www.cstr.ed.ac.uk/projects/festival/) - это многоязычная система синтеза речи, разработанная CSTR ([Centre for Speech Technology Research](http://www.cstr.ed.ac.uk/)).

## Contents

*   [1 Установка](#.D0.A3.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B0)
*   [2 Настройка](#.D0.9D.D0.B0.D1.81.D1.82.D1.80.D0.BE.D0.B9.D0.BA.D0.B0)
    *   [2.1 Использование со звуковым сервером](#.D0.98.D1.81.D0.BF.D0.BE.D0.BB.D1.8C.D0.B7.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D0.B5_.D1.81.D0.BE_.D0.B7.D0.B2.D1.83.D0.BA.D0.BE.D0.B2.D1.8B.D0.BC_.D1.81.D0.B5.D1.80.D0.B2.D0.B5.D1.80.D0.BE.D0.BC)
    *   [2.2 Голоса](#.D0.93.D0.BE.D0.BB.D0.BE.D1.81.D0.B0)
    *   [2.3 Установка голоса по умолчанию](#.D0.A3.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B0_.D0.B3.D0.BE.D0.BB.D0.BE.D1.81.D0.B0_.D0.BF.D0.BE_.D1.83.D0.BC.D0.BE.D0.BB.D1.87.D0.B0.D0.BD.D0.B8.D1.8E)
        *   [2.3.1 Ручная установка голосов](#.D0.A0.D1.83.D1.87.D0.BD.D0.B0.D1.8F_.D1.83.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B0_.D0.B3.D0.BE.D0.BB.D0.BE.D1.81.D0.BE.D0.B2)
    *   [2.4 Поддержка русского языка](#.D0.9F.D0.BE.D0.B4.D0.B4.D0.B5.D1.80.D0.B6.D0.BA.D0.B0_.D1.80.D1.83.D1.81.D1.81.D0.BA.D0.BE.D0.B3.D0.BE_.D1.8F.D0.B7.D1.8B.D0.BA.D0.B0)
*   [3 Использование](#.D0.98.D1.81.D0.BF.D0.BE.D0.BB.D1.8C.D0.B7.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D0.B5)
    *   [3.1 Интерактивный режим (тестирование голосов и пр.)](#.D0.98.D0.BD.D1.82.D0.B5.D1.80.D0.B0.D0.BA.D1.82.D0.B8.D0.B2.D0.BD.D1.8B.D0.B9_.D1.80.D0.B5.D0.B6.D0.B8.D0.BC_.28.D1.82.D0.B5.D1.81.D1.82.D0.B8.D1.80.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D0.B5_.D0.B3.D0.BE.D0.BB.D0.BE.D1.81.D0.BE.D0.B2_.D0.B8_.D0.BF.D1.80..29)
    *   [3.2 Чтение текстового файла](#.D0.A7.D1.82.D0.B5.D0.BD.D0.B8.D0.B5_.D1.82.D0.B5.D0.BA.D1.81.D1.82.D0.BE.D0.B2.D0.BE.D0.B3.D0.BE_.D1.84.D0.B0.D0.B9.D0.BB.D0.B0)
    *   [3.3 Чтение текстового файла и сохранение в wav](#.D0.A7.D1.82.D0.B5.D0.BD.D0.B8.D0.B5_.D1.82.D0.B5.D0.BA.D1.81.D1.82.D0.BE.D0.B2.D0.BE.D0.B3.D0.BE_.D1.84.D0.B0.D0.B9.D0.BB.D0.B0_.D0.B8_.D1.81.D0.BE.D1.85.D1.80.D0.B0.D0.BD.D0.B5.D0.BD.D0.B8.D0.B5_.D0.B2_wav)
    *   [3.4 Пример скрипта для festival](#.D0.9F.D1.80.D0.B8.D0.BC.D0.B5.D1.80_.D1.81.D0.BA.D1.80.D0.B8.D0.BF.D1.82.D0.B0_.D0.B4.D0.BB.D1.8F_festival)
*   [4 Решение проблем](#.D0.A0.D0.B5.D1.88.D0.B5.D0.BD.D0.B8.D0.B5_.D0.BF.D1.80.D0.BE.D0.B1.D0.BB.D0.B5.D0.BC)
    *   [4.1 Cannot open /dev/dsp](#Cannot_open_.2Fdev.2Fdsp)
    *   [4.2 Alsa playing @ wrong speed](#Alsa_playing_.40_wrong_speed)
*   [5 Смотрите также](#.D0.A1.D0.BC.D0.BE.D1.82.D1.80.D0.B8.D1.82.D0.B5_.D1.82.D0.B0.D0.BA.D0.B6.D0.B5)

## Установка

[Установите](/index.php/%D0%A3%D1%81%D1%82%D0%B0%D0%BD%D0%BE%D0%B2%D0%B8%D1%82%D0%B5 "Установите") [festival](https://www.archlinux.org/packages/?name=festival) из [официальных репозиториев](/index.php/Official_repositories_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Official repositories (Русский)"). Кроме того, необходимо установить один или несколько голосовых пакетов [festival-english](https://www.archlinux.org/packages/?name=festival-english), [festival-us](https://www.archlinux.org/packages/?name=festival-us). Также для Festival доступны и другие голоса; некоторые из них вы можете найти в [AUR](/index.php/AUR_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "AUR (Русский)").

Для проверки выполните команду:

```
$ echo "This is an example. Arch is the best." | festival --tts

```

Если вы слышите то, что написано в примере, вы успешно установили TTS-систему. Если вы ничего не слышите, слышите какой-то странный звук или только начало предложения, смотрите раздел [#Решение проблем](#.D0.A0.D0.B5.D1.88.D0.B5.D0.BD.D0.B8.D0.B5_.D0.BF.D1.80.D0.BE.D0.B1.D0.BB.D0.B5.D0.BC).

## Настройка

Основной конфигурационный файл расположен в /etc, но рекомендуется создать пользовательский файл `~/.festivalrc`, или редактировать непосредственно `/usr/share/festival/festival.scm`.

### Использование со звуковым сервером

Для PulseAudio, добавить эти строки в конец файла `~/.festivalrc` или `/usr/share/festival/festival.scm`:

```
(Parameter.set 'Audio_Required_Format 'aiff)
(Parameter.set 'Audio_Method 'Audio_Command)
(Parameter.set 'Audio_Command "paplay $FILE --client-name=Festival --stream-name=Speech")

```

Для ALSA, использовать эти строки вместо ([source](http://ubuntuforums.org/showpost.php?p=4058268&postcount=16)):

```
(Parameter.set 'Audio_Method 'Audio_Command)
(Parameter.set 'Audio_Command "aplay -q -c 1 -t raw -f s16 -r $SR $FILE")

```

### Голоса

Чтобы узнать, какие голоса в настоящее время установлены и какой из них используется по умолчанию, перейдите в оболочку фестиваля (представляющую схему REPL):

```
   $ festival

   Festival Speech Synthesis System 2.1:release November 2010
   Copyright (C) University of Edinburgh, 1996-2010\. All rights reserved.

   clunits: Copyright (C) University of Edinburgh and CMU 1997-2010
   clustergen_engine: Copyright (C) CMU 2005-2010
   hts_engine: 
   The HMM-based speech synthesis system (HTS)
   hts_engine API version 1.04 ([http://hts-engine.sourceforge.net/](http://hts-engine.sourceforge.net/))
   Copyright (C) 2001-2010  Nagoya Institute of Technology
                 2001-2008  Tokyo Institute of Technology
   All rights reserved.
   For details type `(festival_warranty)'
   festival> voice_default 
   voice_cmu_us_slt_arctic_hts          ;;<-- THIS IS THE VOICE FESTIVAL SPEAKS WITH
   festival> default-voice-priority-list 

```

```
   (kal_diphone                         ;;<-- THIS IS THE HARD-CODED LIST OF VOICES FESTIVAL CAME PRE-AWARE OF
    cmu_us_bdl_arctic_hts
    cmu_us_jmk_arctic_hts
    cmu_us_slt_arctic_hts
    cmu_us_awb_arctic_hts
    ked_diphone
    don_diphone
    rab_diphone
    en1_mbrola
    us1_mbrola
    us2_mbrola
    us3_mbrola
    gsw_diphone
    el_diphone)

   festival> (voice_                    ;;<-- PRESS TAB HERE TO SEE WHAT VOICES FESTIVAL HAS AVAILABLE
   voice_cmu_us_slt_arctic_hts     voice_kal_diphone               voice_nitech_us_slt_arctic_hts  voice_reset
   voice_default                   voice_nitech_us_clb_arctic_hts  voice_rab_diphone
   festival> (voice_cmu_us_slt_arctic_hts) 
   cmu_us_slt_arctic_hts
   festival> (SayText "Arch makes me happy")
   #<Utterance 0x7fb5b8c423b0>
   festival> 

```

### Установка голоса по умолчанию

Чтобы установить голос по умолчанию, добавьте следующую строку в конец вашего `~/.festivalrc`

```
(set! voice_default voice_msu_ru_nsh_clunits)

```

You cannot set the voice with festival.scm; to set voices globally, set order of searched voices in `/usr/share/festival/voices.scm`.

#### Ручная установка голосов

Вы также можете получить голоса прямо из [festvox.org](http://festvox.org/festival/downloads.html). Файлы для загрузки различных голосов имеют вид "festvox_*.tgz". Чтобы их задействовать, необходимо распакованный архив переместить в каталог, содержащий голос. На данный момент для Arch подходящей директорией является `/usr/share/festival/voices/` с соответствующей подкаталогом для голоса из 'festvox'.

### Поддержка русского языка

В файл /usr/share/festival/languages.scm дописать вначале:

```
(define (language_russian)
 "(language_russian)
  Set up language parameters for Russian."
  (set! male1 voice_msu_ru_nsh_clunits)
  (male1)
  (Parameter.set 'Language 'russian)
)

```

и в этом же файле в define(select_language language) добавить:

```
((equal? language 'russian)
(language_russian))

```

Для проверки выполните команду:

```
$ echo "Арч самый лучший. Я гарантирую!" | festival --tts --language russian

```

## Использование

### Интерактивный режим (тестирование голосов и пр.)

festival имеет командную строку, которая вы можете использовать для тестов. Несколько примеров (с примерами выводов)

```
$ festival 
[...]
festival> 

```

Список доступных голосов:

```
festival> (voice.list)
(cstr_us_awb_arctic_multisyn kal_diphone don_diphone)

```

Установить голос:

```
festival> (voice_cstr_us_awb_arctic_multisyn)
#<voice 0x1545b90>

```

Произнести:

```
festival> (SayText '"test this is a test oh no a test bla test")
inserting pause after: t.
Inserting pause
[...]
id _63 ; name t ; 
id _65 ; name # ; 
#<Utterance 0x7f7c0c144810>

```

Помощь:

```
festival> help 
"The Festival Speech Synthesizer System: Help

```

Выход - ctrl+d или набрать:

```
festival> (quit)

```

### Чтение текстового файла

```
festival --tts /path/to/letter.txt

```

### Чтение текстового файла и сохранение в wav

```
cat letter.txt | text2wave -o letter.wav

```

### Пример скрипта для festival

Одним из классических приложений, для которых удобно использовать festival, является ping. Используйте этот скрипт при пинге хоста, который будет возвращать успешный или неудачный результат:

```
#!/bin/bash
while [ 1 = 1 ]; do
     ping -c $1 && (echo "Ping" | festival --tts) || (echo "Fail" | festival --tts)
done

```

Заметьте, что синтезатор речи работает не в реальном времени, т.к. ему нужно некоторое время перед воспроизведением.

## Решение проблем

### Cannot open /dev/dsp

Если festival возвращает следующую ошибку:

```
Linux: cannot open /dev/dsp

```

В зависимости от установленной аудиосистемы (можно проверить, набрав aplay или paplay в терминале), добавьте эти строки в ваш .festivalrc, или в usr/share/festival/festival.scm ([source](http://ubuntuforums.org/showpost.php?p=4058268&postcount=16), [source](http://snipt.net/alifity/make-festival-work-with-pulseaudio)):

Для ALSA:

```
(Parameter.set 'Audio_Method 'Audio_Command)
(Parameter.set 'Audio_Command "aplay -q -c 1 -t raw -f s16 -r $SR $FILE")

```

Для PulseAudio:

```
(Parameter.set 'Audio_Command "paplay $FILE")
(Parameter.set 'Audio_Method 'Audio_Command)
(Parameter.set 'Audio_Required_Format 'snd)

```

### Alsa playing @ wrong speed

Если решение выше даёт скрипучий (писклявый) голос, можно попробовать следующее:

```
(Parameter.set 'Audio_Method 'Audio_Command)
(Parameter.set 'Audio_Command "aplay -Dplug:default -f S16_LE -r $SR $FILE")

```

## Смотрите также

[Банк скриптов для голосового движка Festival](http://ru.festivalspeaker.wikia.com/wiki/%D0%91%D0%B0%D0%BD%D0%BA_%D1%81%D0%BA%D1%80%D0%B8%D0%BF%D1%82%D0%BE%D0%B2_%D0%B4%D0%BB%D1%8F_%D0%B3%D0%BE%D0%BB%D0%BE%D1%81%D0%BE%D0%B2%D0%BE%D0%B3%D0%BE_%D0%B4%D0%B2%D0%B8%D0%B6%D0%BA%D0%B0_Festival)

[Учим компьютер говорить по-русски / Festival скрипты](http://forum.ubuntu.ru/index.php?topic=92123.0)

[Говорящий пингвин. Учим Linux говорить и слушать](http://xakep.ru/magazine/xa/133/082/1.asp)