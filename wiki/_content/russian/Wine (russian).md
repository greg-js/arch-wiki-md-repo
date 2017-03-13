[Wine](https://en.wikipedia.org/wiki/ru:Wine "wikipedia:ru:Wine") — свободная реализация программного интерфейса Microsoft Windows (WinAPI), позволяющая запускать приложения Windows в среде Unix-подобных операционных систем. Программы, запущенные в Wine, работают точно так же, как и в своей родной среде без снижения производительности, в отличие от запуска в эмуляторе. Более подробное описание Wine смотрите на [домашней странице проекта](http://www.winehq.org/) и на [вики-страницах Wine](http://wiki.winehq.org/).

## Contents

*   [1 Установка](#.D0.A3.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B0)
*   [2 Настройка](#.D0.9D.D0.B0.D1.81.D1.82.D1.80.D0.BE.D0.B9.D0.BA.D0.B0)
    *   [2.1 WINEPREFIX](#WINEPREFIX)
    *   [2.2 WINEARCH](#WINEARCH)
    *   [2.3 Графические драйверы](#.D0.93.D1.80.D0.B0.D1.84.D0.B8.D1.87.D0.B5.D1.81.D0.BA.D0.B8.D0.B5_.D0.B4.D1.80.D0.B0.D0.B9.D0.B2.D0.B5.D1.80.D1.8B)
    *   [2.4 Звук](#.D0.97.D0.B2.D1.83.D0.BA)
        *   [2.4.1 Поддержка MIDI](#.D0.9F.D0.BE.D0.B4.D0.B4.D0.B5.D1.80.D0.B6.D0.BA.D0.B0_MIDI)
    *   [2.5 Другие библиотеки](#.D0.94.D1.80.D1.83.D0.B3.D0.B8.D0.B5_.D0.B1.D0.B8.D0.B1.D0.BB.D0.B8.D0.BE.D1.82.D0.B5.D0.BA.D0.B8)
    *   [2.6 Шрифты](#.D0.A8.D1.80.D0.B8.D1.84.D1.82.D1.8B)
    *   [2.7 Значки запуска программ](#.D0.97.D0.BD.D0.B0.D1.87.D0.BA.D0.B8_.D0.B7.D0.B0.D0.BF.D1.83.D1.81.D0.BA.D0.B0_.D0.BF.D1.80.D0.BE.D0.B3.D1.80.D0.B0.D0.BC.D0.BC)
        *   [2.7.1 Создание пунктов меню для утилит Wine](#.D0.A1.D0.BE.D0.B7.D0.B4.D0.B0.D0.BD.D0.B8.D0.B5_.D0.BF.D1.83.D0.BD.D0.BA.D1.82.D0.BE.D0.B2_.D0.BC.D0.B5.D0.BD.D1.8E_.D0.B4.D0.BB.D1.8F_.D1.83.D1.82.D0.B8.D0.BB.D0.B8.D1.82_Wine)
        *   [2.7.2 Удаление пунктов меню](#.D0.A3.D0.B4.D0.B0.D0.BB.D0.B5.D0.BD.D0.B8.D0.B5_.D0.BF.D1.83.D0.BD.D0.BA.D1.82.D0.BE.D0.B2_.D0.BC.D0.B5.D0.BD.D1.8E)
        *   [2.7.3 Неверный раздел в меню KDE 4](#.D0.9D.D0.B5.D0.B2.D0.B5.D1.80.D0.BD.D1.8B.D0.B9_.D1.80.D0.B0.D0.B7.D0.B4.D0.B5.D0.BB_.D0.B2_.D0.BC.D0.B5.D0.BD.D1.8E_KDE_4)
*   [3 Запуск приложений Windows](#.D0.97.D0.B0.D0.BF.D1.83.D1.81.D0.BA_.D0.BF.D1.80.D0.B8.D0.BB.D0.BE.D0.B6.D0.B5.D0.BD.D0.B8.D0.B9_Windows)
*   [4 Советы и рекомендации](#.D0.A1.D0.BE.D0.B2.D0.B5.D1.82.D1.8B_.D0.B8_.D1.80.D0.B5.D0.BA.D0.BE.D0.BC.D0.B5.D0.BD.D0.B4.D0.B0.D1.86.D0.B8.D0.B8)
    *   [4.1 Сброс ассоциаций файлов Wine](#.D0.A1.D0.B1.D1.80.D0.BE.D1.81_.D0.B0.D1.81.D1.81.D0.BE.D1.86.D0.B8.D0.B0.D1.86.D0.B8.D0.B9_.D1.84.D0.B0.D0.B9.D0.BB.D0.BE.D0.B2_Wine)
    *   [4.2 Два монитора с разными разрешениями](#.D0.94.D0.B2.D0.B0_.D0.BC.D0.BE.D0.BD.D0.B8.D1.82.D0.BE.D1.80.D0.B0_.D1.81_.D1.80.D0.B0.D0.B7.D0.BD.D1.8B.D0.BC.D0.B8_.D1.80.D0.B0.D0.B7.D1.80.D0.B5.D1.88.D0.B5.D0.BD.D0.B8.D1.8F.D0.BC.D0.B8)
    *   [4.3 exe-thumbnailer](#exe-thumbnailer)
    *   [4.4 Патч CSMT](#.D0.9F.D0.B0.D1.82.D1.87_CSMT)
        *   [4.4.1 Дополнительная информация о CSMT](#.D0.94.D0.BE.D0.BF.D0.BE.D0.BB.D0.BD.D0.B8.D1.82.D0.B5.D0.BB.D1.8C.D0.BD.D0.B0.D1.8F_.D0.B8.D0.BD.D1.84.D0.BE.D1.80.D0.BC.D0.B0.D1.86.D0.B8.D1.8F_.D0.BE_CSMT)
    *   [4.5 Изменение языка](#.D0.98.D0.B7.D0.BC.D0.B5.D0.BD.D0.B5.D0.BD.D0.B8.D0.B5_.D1.8F.D0.B7.D1.8B.D0.BA.D0.B0)
    *   [4.6 Установка Microsoft Office 2010](#.D0.A3.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B0_Microsoft_Office_2010)
    *   [4.7 Правильное монтирование образов компакт-дисков](#.D0.9F.D1.80.D0.B0.D0.B2.D0.B8.D0.BB.D1.8C.D0.BD.D0.BE.D0.B5_.D0.BC.D0.BE.D0.BD.D1.82.D0.B8.D1.80.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D0.B5_.D0.BE.D0.B1.D1.80.D0.B0.D0.B7.D0.BE.D0.B2_.D0.BA.D0.BE.D0.BC.D0.BF.D0.B0.D0.BA.D1.82-.D0.B4.D0.B8.D1.81.D0.BA.D0.BE.D0.B2)
    *   [4.8 Запись на компакт-диски](#.D0.97.D0.B0.D0.BF.D0.B8.D1.81.D1.8C_.D0.BD.D0.B0_.D0.BA.D0.BE.D0.BC.D0.BF.D0.B0.D0.BA.D1.82-.D0.B4.D0.B8.D1.81.D0.BA.D0.B8)
    *   [4.9 OpenGL](#OpenGL)
    *   [4.10 Использование Wine как интерпретатор для исполняемых файлов Win16/Win32](#.D0.98.D1.81.D0.BF.D0.BE.D0.BB.D1.8C.D0.B7.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D0.B5_Wine_.D0.BA.D0.B0.D0.BA_.D0.B8.D0.BD.D1.82.D0.B5.D1.80.D0.BF.D1.80.D0.B5.D1.82.D0.B0.D1.82.D0.BE.D1.80_.D0.B4.D0.BB.D1.8F_.D0.B8.D1.81.D0.BF.D0.BE.D0.BB.D0.BD.D1.8F.D0.B5.D0.BC.D1.8B.D1.85_.D1.84.D0.B0.D0.B9.D0.BB.D0.BE.D0.B2_Win16.2FWin32)
    *   [4.11 Wineconsole](#Wineconsole)
    *   [4.12 Winetricks](#Winetricks)
    *   [4.13 Установка .NET framework 4.0](#.D0.A3.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B0_.NET_framework_4.0)
    *   [4.14 Треск из колонок при использовании PulseAudio](#.D0.A2.D1.80.D0.B5.D1.81.D0.BA_.D0.B8.D0.B7_.D0.BA.D0.BE.D0.BB.D0.BE.D0.BD.D0.BE.D0.BA_.D0.BF.D1.80.D0.B8_.D0.B8.D1.81.D0.BF.D0.BE.D0.BB.D1.8C.D0.B7.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D0.B8_PulseAudio)
    *   [4.15 16-битные программы](#16-.D0.B1.D0.B8.D1.82.D0.BD.D1.8B.D0.B5_.D0.BF.D1.80.D0.BE.D0.B3.D1.80.D0.B0.D0.BC.D0.BC.D1.8B)
*   [5 Сторонние оболочки](#.D0.A1.D1.82.D0.BE.D1.80.D0.BE.D0.BD.D0.BD.D0.B8.D0.B5_.D0.BE.D0.B1.D0.BE.D0.BB.D0.BE.D1.87.D0.BA.D0.B8)
    *   [5.1 CrossOver](#CrossOver)
    *   [5.2 PlayOnLinux/PlayOnMac](#PlayOnLinux.2FPlayOnMac)
    *   [5.3 PyWinery](#PyWinery)
    *   [5.4 Q4wine](#Q4wine)
*   [6 Смотрите также](#.D0.A1.D0.BC.D0.BE.D1.82.D1.80.D0.B8.D1.82.D0.B5_.D1.82.D0.B0.D0.BA.D0.B6.D0.B5)

## Установка

**Важно:** Если у вас есть права для доступа к какому-либо файлу или ресурсу, то и запущенная вами программа в префиксе Wine тоже их получит. Префиксы Wine **не** являются так называемыми [песочницами](https://en.wikipedia.org/wiki/ru:%D0%9F%D0%B5%D1%81%D0%BE%D1%87%D0%BD%D0%B8%D1%86%D0%B0_(%D0%B1%D0%B5%D0%B7%D0%BE%D0%BF%D0%B0%D1%81%D0%BD%D0%BE%D1%81%D1%82%D1%8C) "wikipedia:ru:Песочница (безопасность)"). Если важно обеспечение безопасности, используйте средства [виртуализации](https://en.wikipedia.org/wiki/ru:%D0%92%D0%B8%D1%80%D1%82%D1%83%D0%B0%D0%BB%D0%B8%D0%B7%D0%B0%D1%86%D0%B8%D1%8F "wikipedia:ru:Виртуализация").

Wine может быть [установлен](/index.php/Pacman_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#.D0.A3.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B0_.D0.BE.D0.BF.D1.80.D0.B5.D0.B4.D0.B5.D0.BB.D0.B5.D0.BD.D0.BD.D1.8B.D1.85_.D0.BF.D0.B0.D0.BA.D0.B5.D1.82.D0.BE.D0.B2 "Pacman (Русский)") с пакетом [wine](https://www.archlinux.org/packages/?name=wine), доступном в [официальных репозиториях](/index.php/Official_repositories_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Official repositories (Русский)"). Если вы используете 64-битную систему, первым делом не забудьте включить репозиторий [Multilib](/index.php/Multilib_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Multilib (Русский)").

Также вы можете установить пакеты [wine_gecko](https://www.archlinux.org/packages/?name=wine_gecko) и [wine-mono](https://www.archlinux.org/packages/?name=wine-mono) для приложений, которые нуждаются в поддержке Internet Explorer и .NET, соответственно. Строго говоря, эти пакеты не обязательно устанавливать, так как Wine может загружать необходимые файлы самостоятельно по мере необходимости. Однако, если установить их сразу, это позволит затем работать без доступа к сети, так как Wine больше не будет загружать файлы для каждого префикса.

**Архитектурные различия**

Версия пакета Arch i686, используемая по умолчанию, содержит 32-битную сборку Wine, поэтому вы не сможете запускать в нем 64-битные приложения. Пакет Arch x86_64, однако, содержит сборку с флагом `--enable-win64`, которая включает в Wine подсистему [WoW64](https://en.wikipedia.org/wiki/ru:WoW64 "wikipedia:ru:WoW64").

*   В Windows эта сложная подсистема позволяет пользователям запускать 32-битные и 64-битные программы одновременно и даже в одном и том же каталоге.
*   В Wine пользователь должен создать отдельные префиксы или каталоги. Более подробную информацию смотрите в [Wine64](http://wiki.winehq.org/Wine64).

Если вы испытываете проблемы с *winetricks* или программами в 64-битном окружении, попробуйте создать новый 32-битный префикс. Смотрите раздел [#WINEARCH](#WINEARCH). Использование пакета x86_64 с `WINEARCH=win32` должно иметь тот же эффект, что и просто использование сборки из пакета i686.

## Настройка

Настройка Wine обычно выполняется с помощью следующих инструментов:

*   [winecfg](http://wiki.winehq.org/winecfg) — инструмент для настройки Wine с графическим интерфейсом. Вы можете запустить его из терминала, набрав `$ winecfg`, или, с указанием префикса: `$ WINEPREFIX=~/.some_prefix winecfg`.
*   [control.exe](http://wiki.winehq.org/control) — реализация Панели управления Windows в Wine, которую можно вызвать, выполнив `$ wine control`.
*   [regedit](http://wiki.winehq.org/regedit) — инструмент для редактирования реестра. Если *winecfg* или Панели управления недостаточно, смотрите [эту статью на WineHQ](http://wiki.winehq.org/UsefulRegistryKeys), в которой перечислены полезные ключи реестра.

### WINEPREFIX

По умолчанию, Wine хранит файлы настроек и установленные приложения Windows в каталоге `~/.wine`. Этот каталог называется *префиксом* Wine (Wine prefix). Он создается и обновляется автоматически по необходимости при запуске программ Windows и программ настройки Wine, например *winecfg*. Каталог префикса также содержит стандартную структуру корневого раздела каталогов Windows, которая представляется программам Windows как диск `C:`.

Вы можете изменить место расположения префикса, создав переменную окружения `WINEPREFIX` с указанием нового пути. Это полезно, когда вам необходимо использовать различное окружение для разных приложений Windows. При запуске приложения Windows новый префикс будет автоматически создан на указанном в `WINEPREFIX` месте, если его до этого не существовало.

Для примера, если вы запускаете одно приложение с `$ env WINEPREFIX=~/.win-a wine program-a.exe`, а другое с `$ env WINEPREFIX=~/.win-b wine program-b.exe`, у каждой программы будет свой раздел `C:`, соответственно, своя копия всех настроек и реестра. Таким образом, обе программы будут запущены в полностью изолированных друг от друга средах.

**Примечание:** Тем не менее, префиксы Wine не являются [песочницами](https://en.wikipedia.org/wiki/ru:%D0%9F%D0%B5%D1%81%D0%BE%D1%87%D0%BD%D0%B8%D1%86%D0%B0_(%D0%B1%D0%B5%D0%B7%D0%BE%D0%BF%D0%B0%D1%81%D0%BD%D0%BE%D1%81%D1%82%D1%8C) "wikipedia:ru:Песочница (безопасность)"). Программы, запущенные в Wine могут также получать доступ к оставшейся части системы (например, раздел `Z:` обычно соответствует корню файловой системы `/`).

Для создания префикса без запуска каких-либо средств настройки Wine или приложений Windows вы можете использовать команду:

```
$ env WINEPREFIX=~/.customprefix wineboot -u

```

### WINEARCH

Информация в данном разделе применима только если вы используете 64-битную сборку Wine, поставляемую с версией пакета `x86_64`.

Если у вас 64-битная операционная система, по умолчанию будет запускаться 64-битная среда Wine. Вы можете изменить это поведение используя переменную окружения `WINEARCH`. При создании префикса передайте программе переменную окружения `$ WINEARCH=win32`. Например, чтобы создать новый 32-битный префикс на стандартном месте, переименуйте старый каталог `~/.wine` и выполните `$ WINEARCH=win32 winecfg`. Будет создан новый 32-битный префикс Wine. Без указания `$ WINEARCH=win32` на 64-битных системах создается 64-битный префикс.

Вы можете объединить эту переменную с `WINEPREFIX` для создания отдельных 32-битной и 64-битной сред:

```
$ WINEARCH=win32 WINEPREFIX=~/win32 winecfg
$ WINEPREFIX=~/win64 winecfg

```

Также вы можете использовать `WINEARCH` вместе с другими программами Wine, например с *winetricks* (Steam использован в качестве примера):

```
WINEARCH=win32 WINEPREFIX=~/.local/share/wineprefixes/steam winetricks steam

```

Вы можете добавить переменные окружения `WINEPREFIX` и `WINEARCH` в файл инициализации вашей командной оболочки, например `~/.bashrc` или `~/.zshrc`, чтобы не указывать их каждый раз при использовании Wine:

```
export WINEPREFIX=$HOME/.config/wine/
export WINEARCH=win32

```

### Графические драйверы

Для большинства игр потребуются драйверы для графического ускорителя. Обычно это значит, что вам следует использовать проприетарные драйверы, такие как [NVIDIA](/index.php/NVIDIA "NVIDIA") или [AMD Catalyst](/index.php/AMD_Catalyst "AMD Catalyst"). Открытые реализации драйверов, например [ATI](/index.php/ATI "ATI") также все чаще используются c Wine. Драйверы [Intel](/index.php/Intel "Intel") также должны в большинстве случаев нормально заработать "из коробки".

Смотрите статью [Играем на Wine: хорошие и плохие графические драйверы](http://www.phoronix.com/scan.php?page=news_item&px=MTI5NjU) для получения дополнительной информации.

Признаком того, что с вашими драйвером что-то не так, или они не настроен правильно, может служить такое сообщение Wine в окне терминала:

```
Direct rendering is disabled, most likely your OpenGL drivers have not been installed correctly

```

Для 64-разрядных систем потребуются дополнительные пакеты из репозитория [multilib](/index.php/Multilib_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Multilib (Русский)"). Перечень необходимых пакетов вы можете найти в таблице на странице [Xorg#Driver installation](/index.php/Xorg#Driver_installation "Xorg").

**Примечание:** Возможно, потребуется перезапустить X после установки пакетов.

### Звук

Если возникли проблемы со звуком, первым делом убедитесь, что только одно звуковое устройство выбрано в `winecfg`. На данный момент драйвер [Alsa](/index.php/Alsa "Alsa") наиболее предпочтителен.

Если вы хотите использовать драйвер Alsa в Wine на 64-битной системе, вам необходимо установить пакеты [lib32-alsa-lib](https://www.archlinux.org/packages/?name=lib32-alsa-lib) и [lib32-alsa-plugins](https://www.archlinux.org/packages/?name=lib32-alsa-plugins). Если вы используете [PulseAudio](/index.php/PulseAudio "PulseAudio"), установите также [lib32-libpulse](https://www.archlinux.org/packages/?name=lib32-libpulse).

Если вы хотите использовать драйвер [OSS](/index.php/OSS "OSS") в Wine, вам нужно установить пакет [lib32-alsa-oss](https://www.archlinux.org/packages/?name=lib32-alsa-oss). Драйвера OSS в ядре недостаточно для работы в Wine.

Если `winecfg` **все еще** не может обнаружить звуковой драйвер, [выберите его вручную в реестре](http://wiki.jswindle.com/index.php/Wine_Registry#Configuring_Sound).

Игры, которые используют расширенные звуковые системы могут также потребовать установки [lib32-openal](https://www.archlinux.org/packages/?name=lib32-openal).

#### Поддержка MIDI

[MIDI](/index.php/MIDI "MIDI") была довольно популярной системой в видеоиграх 90-х годов. Если вы запускаете старые игры, скорее всего звук сразу не заработает как надо. Wine имеет отличную поддержку MIDI. Однако, первым делом вам необходимо заставить ее работать на основой системе. Смотрите страницу [MIDI](/index.php/MIDI "MIDI") для получения дополнительной информации. В конечном итоге убедитесь, что Wine использует правильный звуковой выход MIDI. Подробнее об установке смотрите на странице [MIDI на Wine wiki](http://wiki.winehq.org/MIDI).

### Другие библиотеки

*   Некоторые приложения (например, Office 2003/2007) требуют библиотеки MSXML для декодирования HTML и XML, в таких случаях установите [lib32-libxml2](https://www.archlinux.org/packages/?name=lib32-libxml2).

*   Некоторые приложения, которые воспроизводят музыку нуждаются в [lib32-mpg123](https://www.archlinux.org/packages/?name=lib32-mpg123).

*   Некоторые приложения, которые используют родные библиотеки преобразования изображений могут потребовать [lib32-giflib](https://www.archlinux.org/packages/?name=lib32-giflib) и [lib32-libpng](https://www.archlinux.org/packages/?name=lib32-libpng).

*   Некоторые приложения, требующие поддержки средств шифрования потребуют установки [lib32-gnutls](https://www.archlinux.org/packages/?name=lib32-gnutls).

### Шрифты

Если в приложениях Wine плохие шрифты, вероятно, у вас не установлены шрифты TrueType от Microsoft. В этом случае обратитесь к статье [Шрифты Microsoft](/index.php/%D0%A8%D1%80%D0%B8%D1%84%D1%82%D1%8B_Microsoft "Шрифты Microsoft"). Если это не помогло, попробуйте выполнить `winetricks allfonts`.

После установки выйдите из всех приложений Wine и запустите `winecfg`. Шрифты должны стать лучше.

Если шрифты выглядят размыто, импортируйте следующий файл в реестр Wine с помощью [regedit](http://wiki.winehq.org/regedit):

```
[HKEY_CURRENT_USER\Software\Wine\X11 Driver]
"ClientSideWithRender"="N"

```

Смотрите также раздел [Настройка шрифтов#Приложения без поддержки fontconfig](/index.php/%D0%9D%D0%B0%D1%81%D1%82%D1%80%D0%BE%D0%B9%D0%BA%D0%B0_%D1%88%D1%80%D0%B8%D1%84%D1%82%D0%BE%D0%B2#.D0.9F.D1.80.D0.B8.D0.BB.D0.BE.D0.B6.D0.B5.D0.BD.D0.B8.D1.8F_.D0.B1.D0.B5.D0.B7_.D0.BF.D0.BE.D0.B4.D0.B4.D0.B5.D1.80.D0.B6.D0.BA.D0.B8_fontconfig "Настройка шрифтов").

Если у шрифтов приложений Wine отсутствует сглаживание, то самый простой способ его включить через winetricks:

```
$ winetricks fontsmooth-rgb
$ winetricks settings fontsmooth=rgb

```

### Значки запуска программ

При установке приложений Windows в Wine должны создаваться соответствующие значки запуска программ в меню и на рабочем столе. Например, если программа установки (напр. *setup.exe*) создает обычные ярлыки Windows на рабочем столе и в меню "Пуск", то при их создании будут автоматически созданы соответствующие стандартные файлы *.desktop* для запуска программ в Wine.

**Совет:** Если знаки запуска не появляются при установке программ или куда-то пропали, вам сможет помочь утилита [winemenubuilder](http://wiki.winehq.org/winemenubuilder).

#### Создание пунктов меню для утилит Wine

По умолчанию при установке Wine значки для запуска для программ, поставляемых с Wine (например для *winecfg*, *winebrowser* и пр.) не создаются на рабочем столе и в меню. В этом разделе описано, как создать их самостоятельно.

Первым делом, установите какое-нибудь приложение Windows для создания основного меню. После того, как основное меню создано, создайте следующие файлы в `~/.local/share/applications/wine/`:

 `wine-browsedrive.desktop` 
```
[Desktop Entry]
Name=Диск C:
Comment=Запуск обозревателя в диске С:
Exec=wine winebrowser c:
Terminal=false
Type=Application
Icon=folder-wine
Categories=Wine;
```
 `wine-uninstaller.desktop` 
```
[Desktop Entry]
Name=Удаление приложений
Comment=Удаление приложений Windows, установленных в Wine
Exec=wine uninstaller
Terminal=false
Type=Application
Icon=wine-uninstaller
Categories=Wine;
```
 `wine-winecfg.desktop` 
```
[Desktop Entry]
Name=Настройка Wine
Comment=Изменение настроек Wine и отдельных приложений
Exec=winecfg
Terminal=false
Icon=wine-winecfg
Type=Application
Categories=Wine;
```

Также создайте следующий файл в `~/.config/menus/applications-merged/`:

 `wine.menu` 
```
<!DOCTYPE Menu PUBLIC "-//freedesktop//DTD Menu 1.0//EN"
"[http://www.freedesktop.org/standards/menu-spec/menu-1.0.dtd](http://www.freedesktop.org/standards/menu-spec/menu-1.0.dtd)">
<Menu>
  <Name>Приложения</Name>
  <Menu>
    <Name>wine-wine</Name>
    <Directory>wine-wine.directory</Directory>
    <Include>
      <Category>Wine</Category>
    </Include>
  </Menu>
</Menu>
```

Если значки пунктов меню не отображаются или отображаются некорректно, вероятно, что они отсутствуют в текущем наборе значков. В таком случае, следует явно указать полный путь к желаемому значку в системе. Это можно сделать в панели настроек меню. Также вам может понравиться отличный набор иконок, который поддерживает используемые здесь значки, доступный на странице [GNOME-colors](http://www.gnome-look.org/content/show.php/GNOME-colors?content=82562).

#### Удаление пунктов меню

Пункты меню, создаваемые Wine располагаются в `~/.local/share/applications/wine/Programs/`. Для удаления пункта меню просто удалите соответствующий файл *.desktop*.

Кстати, вы также можете удалить все нежелательные сопоставления расширений файлов, созданные Wine, удалив файлы по следующим путям (взято с сайта Wine):

```
$ rm ~/.local/share/mime/packages/x-wine*
$ rm ~/.local/share/applications/wine-extension*
$ rm ~/.local/share/icons/hicolor/*/*/application-x-wine-extension*
$ rm ~/.local/share/mime/application/x-wine-extension*

```

#### Неверный раздел в меню KDE 4

В KDE4 пункты меню Wine [могут появляться](https://bugs.launchpad.net/ubuntu/+source/wine/+bug/263041) в разделе меню "Lost & Found" вместо стандартного раздела Wine. Это происходит потому, что в `kde-applications.menu` отсутствует опция `MergeDir`.

Отредактируйте файл `/etc/xdg/menus/kde-applications.menu`, добавив в конец файла `<MergeDir>applications-merged</MergeDir>` после `<DefaultMergeDirs/>`:

```
<Menu>
        <Include>
                <And>
                        <Category>KDE</Category>
                        <Category>Core</Category>
                </And>
        </Include>
        <DefaultMergeDirs/>
        **<MergeDir>applications-merged</MergeDir>**
        <MergeFile>applications-kmenuedit.menu</MergeFile>
</Menu>

```

Также вы можете просто создать символическую ссылку на каталог, в который смотрит KDE:

```
$ ln -s ~/.config/menus/applications-merged ~/.config/menus/kde-applications-merged

```

## Запуск приложений Windows

**Важно:** Не запускайте и не устанавливайте приложения в Wine с правами суперпользователя! На странице [Running Wine as root](http://wiki.winehq.org/FAQ#run_as_root) вы можете найти официальное предупреждение.

Для запуска приложения Windows наберите:

```
$ wine *путь_до_exe*

```

Чтобы установить приложение с помощью установщика MSI, используйте встроенную утилиту *msiexec*:

```
$ msiexec /i *путь_до_msi*

```

## Советы и рекомендации

**Совет:** В дополнение к ссылкам, предоставленным вначале статьи, следующие материалы могут также быть вам интересны:

*   [The Wine Application Database (AppDB)](http://appdb.winehq.org/) — информация о запуске отдельных приложений Windows (известные неполадки, рейтинги, руководства и т. п.)
*   [The WineHQ Forums](http://forum.winehq.org/) — здесь вы можете получить помощь, если вы не смогли с чем-либо разобраться даже после прочтения FAQ и AppDB.

### Сброс ассоциаций файлов Wine

Wine берет на себя роль приложения по умолчанию для многих форматов файлов. Некоторые (к примеру, `vbs` или `chm`) относятся только к Windows, однако более распространенные форматы (`gif`, `jpeg`, `txt`, `js` и т.д.) Wine пытается открыть в своих реализациях Internet Explorer или Notepad, что может реально надоедать.

Ассоциации файлов Wine задаются в файле `~/.local/share/applications/`, а команда `rm ~/.local/share/applications/mimeinfo.cache` позволяет быстро восстановить предыдущие настройки. Также вы можете выборочно удалить отдельные файлы *.desktop* из этого каталога. Имейте ввиду, что обновления Wine могут восстановить любые удаленные файлы и все придется делать по новой.

### Два монитора с разными разрешениями

Если у вас появились проблемы при использовании нескольких мониторов с разными разрешениями, вероятно дело в недостающем пакете [lib32-libxrandr](https://www.archlinux.org/packages/?name=lib32-libxrandr).

### exe-thumbnailer

Эта небольшая надстройка будет отображать встроенные в исполняемые файлы *.exe* значки, когда они доступны, а также подскажет, что запуск программы будет осуществлен в Wine. Подробности вы можете найти на [Wine wiki](http://wiki.winehq.org/exe-thumbnailer). Пакет [gnome-exe-thumbnailer](https://aur.archlinux.org/packages/gnome-exe-thumbnailer/) доступен в [AUR](/index.php/AUR_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "AUR (Русский)").

### Патч CSMT

В настоящий момент [разработчики Wine](http://www.winehq.org/pipermail/wine-devel/2013-September/101106.html) экспериментируют с оптимизацией потоков ввода-вывода и потоков выполнения. Вы можете наблюдать значительное улучшение производительности, используя экспериментальную версию Wine. Множество игр могут запускаться также быстро, как на Windows или даже быстрее. Этот патч известен как CSMT и работает с графическими ускорителями NVidia и AMD.

**Примечание:** Так как это экспериментальная версия, не все может работать, как ожидается. Пожалуйста, сообщайте о своем удачном и неудачном опыте разработчикам для помощи в разработке новых версий.

Простой путь состоит в использовании [playonlinux](https://www.archlinux.org/packages/?name=playonlinux). После установки игры активируйте версию Wine *1.7.4-CSMT* в меню Tools → Manage Wine Versions.

Скопируйте следующие настройки в секцию `Miscellaneous/Command to exec before running the program` файла конфигурации вашей игры:

```
export WINEDEBUG=-all
export LD_PRELOAD="libpthread.so.0 libGL.so.1"
export __GL_THREADED_OPTIMIZATIONS=0
export __GL_SYNC_TO_VBLANK=1
export __GL_YIELD="NOTHING"
export CSMT=enabled

```

Убедитесь, что опция `StrictDrawOrdering` выключена в `Tools` → `General`.

#### Дополнительная информация о CSMT

[обсуждение на форуме Phoronix](http://www.phoronix.com/forums/showthread.php?93967-Wine-s-Big-Command-Stream-D3D-Patch-Set-Updated/page3&s=7775d7c3d4fa698089d5492bb7b1a435) с участием разработчика CSMT Стефана Дёсингера

[презентация CSMT](http://wiki.winehq.org/FOSDEM2014?action=AttachFile&do=get&target=d3d-drivers.odp) с бенчмарками

[Здесь](https://www.youtube.com/playlist?list=PL0P2a_sII2eTd8uq-azTNpQjiFLqBhDjg) вы найдете игровые видео с демонстрацией возможностей CSMT.

### Изменение языка

Некоторые программы могут не позволять выбирать язык, полагаясь на настройку системной локали. Wine передает параметры окружения (включая настройки локалей) приложению, поэтому все должно работать "из коробки". Если вы хотите принудительно заставить программу использовать другую локаль, вызовите Wine с переменной `LC_ALL`:

```
LC_ALL=*xx_XX.encoding* wine *путь/к/программе*

```

Например,

```
LC_ALL=it_IT.UTF-8 wine *путь/к/программе*

```

### Установка Microsoft Office 2010

**Примечание:** К сожалению, Microsoft Office 2013 пока не запускается.

Microsoft Office 2010 работает без каких-либо проблем (проверено на Microsoft Office Home и Student 2010, Wine 1.5.27 и 1.7.5). Активация через Интернет также работает.

Начните с установки [wine-mono](https://www.archlinux.org/packages/?name=wine-mono), [wine_gecko](https://www.archlinux.org/packages/?name=wine_gecko), [samba](https://www.archlinux.org/packages/?name=samba), и [lib32-libxml2](https://www.archlinux.org/packages/?name=lib32-libxml2).

```
$ export WINEPREFIX=~/.wine # Wine prefix to use
$ export WINEARCH=win32
$ wine /path/to/office_cd/setup.exe

```

Если вы не хотите устанавливать Office в стандартный префикс (`~/.wine`), создайте новый, как указано в разделе [#WINEPREFIX](#WINEPREFIX). Вы также можете поместить указанные переменные окружения в файл инициализации вашей командной оболочки, о чем также написано в разделе.

Как только установка завершится, откройте Word или Excel для активации через Интернет. После активации закройте программу, запустите *winecfg* и установите `riched20` (на вкладке Libraries) to `(native,builtin)`. Это позволит работать PowerPoint.

Дополнительную информацию смотрите в [этой статье на WineHQ](http://appdb.winehq.org/appview.php?iVersionId=4992).

**Примечание:** Чтобы заработал OneNote, запустите `winetricks wininet` и убедитесь, что для библиотеки `wininet` в *winecfg* установлено значение `(native,builtin)`.

**Примечание:** Если активация через Интернет не заработала и вы хотите выполнить ее по телефону, убедитесь, что для библиотеки `riched20` в *winecfg* установлено `(native,builtin)`, иначе вы не сможете выбрать страну из списка.

**Примечание:** [playonlinux](https://www.archlinux.org/packages/?name=playonlinux) дает возможность полностью установить Office 2003, 2007 и 2010 без каких-либо дополнительных действий. Вам будет необходимо лишь указать путь до *setup.exe* или установочного образа диска и процесс установки будет выполнен автоматически. Кроме того, установка Office 2010 из playonlinux исправляет некоторые проблемы, приводившие к появлению ошибок наподобие "Word cannot open the doument".

### Правильное монтирование образов компакт-дисков

Некоторые приложения проверяют, что компакт-диск находится в дисководе. Они могут только лишь проверять данные, в таком случае может быть достаточно указать соответствующий путь в системе как привод CD-ROM в *winecfg*.

Однако, другие приложения могут проверять также метаданные, такие как имя диска или серийный номер, и в этом случае образ должен быть монтирован с указанием этих специальных параметров.

Инструменты создания виртуальных приводов CD-ROM, основанные на fuse не работают с метаданными (например, Acetoneiso). Программа CDEmu, в свою очередь, обрабатывает их правильно.

### Запись на компакт-диски

Чтобы записать данные на CD и DVD, вам необходимо загрузить [модуль ядра](/index.php/Kernel_modules_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Kernel modules (Русский)") `sg`.

### OpenGL

Множество игр и приложений имеют поддержку режима OpenGL, который *может* работать лучше чем стандартный режим DirectX. В то время, как способы включения рендеринга через OpenGL могут различаться от случая к случаю, многие игры просто принимают опцию `-opengl`:

```
$ wine /path/to/3d_game.exe -opengl

```

В общем случае, вам следует посмотреть документацию на ваше приложение, а также искать дополнительную информацию в базе приложений [AppDB](http://appdb.winehq.org).

### Использование Wine как интерпретатор для исполняемых файлов Win16/Win32

Чтобы указать ядру использовать Wine как интерпретатор для всех исполняемых файлов Win16/Win32, наберите:

```
echo ':DOSWin:M::MZ::/usr/bin/wine:' > /proc/sys/fs/binfmt_misc/register

```

Чтобы изменения сохранились после перезагрузки, создайте файл `/etc/binfmt.d/wine.conf` со следующим содержимым:

```
# start Wine for Windows executables
:DOSWin:M::MZ::/usr/bin/wine:

```

[systemd](/index.php/Systemd_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Systemd (Русский)") автоматически монтирует файловую систему `/proc/sys/fs/binfmt_misc` используя `proc-sys-fs-binfmt_misc.mount` (и automount) и запускает файл службы `systemd-binfmt.service` чтобы загружать ваши настройки при старте системы.

Теперь попробуйте запустить программу Windows:

```
$ chmod +x *exefile.exe*
$ ./*exefile.exe*

```

Если все настроено правильно, программа *exefile.exe* будет запущена.

If all went well, *exefile.exe* should run.

### Wineconsole

Бывает необходимо запускать файлы *.exe* для того, чтобы пропатчить файлы какую-либо игру. Например, мод для поддержки широкоэкранного формата изображения для какой-нибудь старой игры. Иногда при запуске файла *.exe* ничего не происходит. В этом случае, попробуйте запускать программу из консоли Wine:

```
$ wineconsole cmd

```

Теперь перейдите к каталогу с *.exe* файлом и запустите его оттуда.

### Winetricks

[Winetricks](http://wiki.winehq.org/winetricks) — скрипт, который позволяет быстро устанавливать в префикс компоненты, необходимые для запуска приложений Windows. Такие компоненты включают библиотеки DirectX 9, MSXML (который необходим Microsoft Office 2007 и Internet Explorer), пакеты Visual C++ Redistributable и многое другое.

Последнюю версию Winetricks вы можете установить с пакетом [winetricks](https://www.archlinux.org/packages/?name=winetricks). Пакет [winetricks-svn](https://aur.archlinux.org/packages/winetricks-svn/) предоставляет наиболее свежую версию, находящуюся в разработке.

После установки запустите Winetricks:

```
$ winetricks

```

### Установка .NET framework 4.0

Первым делом создайте новый 32-битный префикс, если вы используете 64-разрядную систему:

```
$ WINEARCH=win32 WINEPREFIX=~/win32 winecfg

```

Теперь используйте Winetricks для установки необходимых пакетов:

```
$ WINEARCH=win32 WINEPREFIX=~/win32 winetricks -q msxml3 dotnet40 corefonts

```

### Треск из колонок при использовании PulseAudio

Если вы слышите треск в приложениях Wine при использовании PulseAudio, попробуйте раскомментировать строку `; default-fragment-size-msec = 25` в файле `/etc/pulse/daemon.conf` и установить значение `5` для этой опции:

```
default-fragment-size-msec = 5

```

Смотрите [здесь](http://wiki.winehq.org/FAQ#head-58290651b9f85c059a8bfc98118a0262e2cca84b) для получения дополнительной информации.

### 16-битные программы

При запуске старых программ для Windows 9x programs, может возникнуть следующая ошибка:

```
modify_ldt: Invalid argument
err:winediag:build_module Failed to create module for "krnl386.exe",
16-bit LDT support may be missing.
err:module:attach_process_dlls "krnl386.exe16" failed to initialize,
aborting

```

В этом случае, следующая команда может помочь решить проблему:

```
echo 1 > /proc/sys/abi/ldt16

```

Смотрите также [список рассылки Fedora](http://www.spinics.net/linux/fedora/fedora-users/msg450821.html).

## Сторонние оболочки

Оболочки для запуска Wine *не поддерживаются* официально, однако могут быть полезны.

### CrossOver

[CrossOver](http://www.codeweavers.com/about/) имеет собственную [страницу](/index.php/CrossOver "CrossOver").

### PlayOnLinux/PlayOnMac

[PlayOnLinux](http://www.playonlinux.com/) является графической программой для управления приложениями Windows и DOS. Он использует специально создаваемые скрипты для настройки и запуска программ в раздельных префиксах и даже умеет использовать отдельные версий Wine для запуска каждого конкретного исполняемого файла (это вызвано проблемами с обратной совместимостью версий). Если вам нужно знать, какая версия Wine работает лучше всего для конкретной игры, обратитесь к [Wine Application Database](http://appdb.winehq.org/). Пакет [playonlinux](https://www.archlinux.org/packages/?name=playonlinux) доступен в официальных репозиториях.

### PyWinery

[PyWinery](http://code.google.com/p/pywinery/) — простая графическая утилита для управления префиксами, которая позволяет вам настраивать отдельные префиксы и запускать в них приложения. Вы можете установить PyWinery с пакетом [pywinery](https://aur.archlinux.org/packages/pywinery/) из [AUR](/index.php/AUR_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "AUR (Русский)").

### Q4wine

[Q4Wine](http://sourceforge.net/projects/q4wine/) — графический менеджер префиксов Wine, который также позволяет настраивать префиксы. Из достоинств следует отметить возможность экспорта тем Qt в конфигурацию Wine. Пакет [q4wine](https://www.archlinux.org/packages/?name=q4wine) доступен в официальных репозиториях.

## Смотрите также

*   [Официальный сайт Wine](http://www.winehq.com/)
*   [Wine AppDB](http://appdb.winehq.org/)
*   [Настройка графического адаптера и OpenGl в Wine и ускорение его работы](http://linuxgamingtoday.wordpress.com/2008/02/16/quick-tips-to-speed-up-your-gaming-in-wine/)
*   [FileInfo](http://wiki.gotux.net/code:perl:fileinfo) — поиск заголовков PE/COFF в файлах exe/dll/ocx в Linux.
*   [Wine на Gentoo's Wiki](https://wiki.gentoo.org/wiki/Wine)