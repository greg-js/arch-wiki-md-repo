**Состояние перевода:** На этой странице представлен перевод статьи [Sound system](/index.php/Sound_system "Sound system"). Дата последней синхронизации: 8 октября 2019\. Вы можете [помочь](/index.php/ArchWiki_Translation_Team_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "ArchWiki Translation Team (Русский)") синхронизировать перевод, если в английской версии произошли [изменения](https://wiki.archlinux.org/index.php?title=Sound_system&diff=0&oldid=584791).

Эта статья рассказывает о базовом управлении звуком. Для получения информации о более сложных темах см. статью [Профессиональное аудио](/index.php/%D0%9F%D1%80%D0%BE%D1%84%D0%B5%D1%81%D1%81%D0%B8%D0%BE%D0%BD%D0%B0%D0%BB%D1%8C%D0%BD%D0%BE%D0%B5_%D0%B0%D1%83%D0%B4%D0%B8%D0%BE "Профессиональное аудио").

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Общие сведения](#Общие_сведения)
*   [2 Драйверы и интерфейс](#Драйверы_и_интерфейс)
*   [3 Звуковые серверы](#Звуковые_серверы)
*   [4 Смотрите также](#Смотрите_также)

## Общие сведения

Звуковая система Arch Linux состоит из нескольких уровней:

*   Драйверы и интерфейс — поддержка и взаимодействие с аппаратным обеспечением
*   Usermode API (библиотеки) — требуются и используются приложениями
*   **(опционально)** Звуковые серверы в пользовательском режиме — находят лучшее применение в сложных системах, требующих одновременной работы нескольких аудиоприложений и незаменимы для более продвинутых возможностей, например, [профессионального аудио](/index.php/Pro_Audio_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Pro Audio (Русский)").
*   **(опционально)** Звуковые фреймворки — более высокоуровневые программные окружения, не связанные с серверными процессами

Базовая установка Arch Linux включает в себя звуковую систему ядра ([ALSA](/index.php/Advanced_Linux_Sound_Architecture_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Advanced Linux Sound Architecture (Русский)")), также можно установить множество утилит для управления ALSA из [официальных репозиториев](/index.php/Official_repositories_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Official repositories (Русский)"). Если требуются дополнительные возможности, вы можете сменить его на [OSS](/index.php/OSS "OSS") или выбрать другой [звуковой сервер](https://en.wikipedia.org/wiki/sound_server "wikipedia:sound server").

## Драйверы и интерфейс

*   **[ALSA](/index.php/ALSA_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "ALSA (Русский)")** — компонент ядра Linux, содержащий драйверы устройств и обеспечивающий наиболее низкоуровневую поддержку звукового аппаратного обеспечения.

	[https://www.alsa-project.org/wiki/Main_Page](https://www.alsa-project.org/wiki/Main_Page) || входит в состав ядра по умолчанию

*   **[Open Sound System](/index.php/Open_Sound_System "Open Sound System") (OSS)** — альтернативная звуковая архитектура для Unix- и POSIX-совместимых систем. OSS 3-ей версии была основной звуковой системой Linux и включалась в ядро, но была заменена на ALSA в 2002 году, когда 4-ая версия OSS стала проприетарным ПО. OSSv4 вновь стала свободным ПО в 2007, когда 4Front Technologies опубликовали её исходные коды и разместили их под лицензией GPL. OSS не поддерживает такое же множество устройств как ALSA, но в некоторых случаях работает лучше.

	[http://www.opensound.com/](http://www.opensound.com/) || [oss](https://aur.archlinux.org/packages/oss/)

## Звуковые серверы

*   **[PulseAudio](/index.php/PulseAudio_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "PulseAudio (Русский)")** — очень популярный звуковой сервер, использующийся большинством современных приложений для Linux. Очень хорошо работает с несколькими одновременными потоками аудио и может использоваться по сети. Также PulseAudio легко настраивается — зачастую достаточно только установить пакет.

	[https://www.freedesktop.org/wiki/Software/PulseAudio/](https://www.freedesktop.org/wiki/Software/PulseAudio/) || [pulseaudio](https://www.archlinux.org/packages/?name=pulseaudio)

*   **[JACK Audio Connection Kit](/index.php/JACK_Audio_Connection_Kit "JACK Audio Connection Kit")** — более старая редакция звукового сервера, используемая в профессиональной работе со звуком, особенно когда требуется быстрый отклик при работе с записью, эффектами, синтезом в реальном времени и так далее. Хотя эта редакция и является старой, она сохраняет группу активных и преданных разработчиков, а многие проблемы удаётся решить путём проб и ошибок.

	[https://jackaudio.org/](https://jackaudio.org/) || [jack](https://www.archlinux.org/packages/?name=jack)

*   **JACK2** — новая версия JACK, разработанная непосредственно для работы в мультипроцессорных системах и также включающая передачу данных по сети.

	[https://github.com/jackaudio/jackaudio.github.com/wiki/Q_difference_jack1_jack2](https://github.com/jackaudio/jackaudio.github.com/wiki/Q_difference_jack1_jack2) || [jack2](https://www.archlinux.org/packages/?name=jack2)

*   **[NAS](https://en.wikipedia.org/wiki/ru:Network_Audio_System "wikipedia:ru:Network Audio System")** — звуковой сервер, поддерживаемый некоторыми крупными приложениями.

	[https://www.radscan.com/nas/nas-links.html](https://www.radscan.com/nas/nas-links.html) || [nas](https://aur.archlinux.org/packages/nas/)

## Смотрите также

*   [MIDI](/index.php/MIDI "MIDI")
*   [Кодеки](/index.php/%D0%9A%D0%BE%D0%B4%D0%B5%D0%BA%D0%B8 "Кодеки")
*   [Профессиональное аудио](/index.php/%D0%9F%D1%80%D0%BE%D1%84%D0%B5%D1%81%D1%81%D0%B8%D0%BE%D0%BD%D0%B0%D0%BB%D1%8C%D0%BD%D0%BE%D0%B5_%D0%B0%D1%83%D0%B4%D0%B8%D0%BE "Профессиональное аудио")
*   [Динамик ПК](/index.php/%D0%94%D0%B8%D0%BD%D0%B0%D0%BC%D0%B8%D0%BA_%D0%9F%D0%9A "Динамик ПК")