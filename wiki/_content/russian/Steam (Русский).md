Из [Wikipedia](https://en.wikipedia.org/wiki/Steam_(software) "wikipedia:Steam (software)"):

[Steam](http://store.steampowered.com/about/) — сервис цифрового распространения компьютерных игр и программ, принадлежащий компании Valve, известному разработчику компьютерных игр. Steam выполняет функции службы активации, загрузки через интернет, автоматических обновлений и новостей для игр как самой Valve, так и сторонних разработчиков по соглашению с Valve, таких как Epic Games, THQ, 2K Games, Activision, Capcom, Codemasters, Eidos Interactive, 1С, GSC Game World, id Software, SEGA, Atari, Rockstar Games, Telltale Games, Ubisoft, Bethesda Softworks и многих других фирм, оформивших контракт на дистрибьюцию.

## Contents

*   [1 Установка](#.D0.A3.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B0)
*   [2 Запуск Steam](#.D0.97.D0.B0.D0.BF.D1.83.D1.81.D0.BA_Steam)
    *   [2.1 Режим Big Picture (из Display Manager)](#.D0.A0.D0.B5.D0.B6.D0.B8.D0.BC_Big_Picture_.28.D0.B8.D0.B7_Display_Manager.29)
    *   [2.2 Запуск Steam свернутым в области уведомлений (silent mode)](#.D0.97.D0.B0.D0.BF.D1.83.D1.81.D0.BA_Steam_.D1.81.D0.B2.D0.B5.D1.80.D0.BD.D1.83.D1.82.D1.8B.D0.BC_.D0.B2_.D0.BE.D0.B1.D0.BB.D0.B0.D1.81.D1.82.D0.B8_.D1.83.D0.B2.D0.B5.D0.B4.D0.BE.D0.BC.D0.BB.D0.B5.D0.BD.D0.B8.D0.B9_.28silent_mode.29)
*   [3 Решение проблем](#.D0.A0.D0.B5.D1.88.D0.B5.D0.BD.D0.B8.D0.B5_.D0.BF.D1.80.D0.BE.D0.B1.D0.BB.D0.B5.D0.BC)
    *   [3.1 Проблемы с драйверами nvidia версии 361.28](#.D0.9F.D1.80.D0.BE.D0.B1.D0.BB.D0.B5.D0.BC.D1.8B_.D1.81_.D0.B4.D1.80.D0.B0.D0.B9.D0.B2.D0.B5.D1.80.D0.B0.D0.BC.D0.B8_nvidia_.D0.B2.D0.B5.D1.80.D1.81.D0.B8.D0.B8_361.28)
    *   [3.2 Проблемы среды выполнения Steam](#.D0.9F.D1.80.D0.BE.D0.B1.D0.BB.D0.B5.D0.BC.D1.8B_.D1.81.D1.80.D0.B5.D0.B4.D1.8B_.D0.B2.D1.8B.D0.BF.D0.BE.D0.BB.D0.BD.D0.B5.D0.BD.D0.B8.D1.8F_Steam)
        *   [3.2.1 Возможные симптомы](#.D0.92.D0.BE.D0.B7.D0.BC.D0.BE.D0.B6.D0.BD.D1.8B.D0.B5_.D1.81.D0.B8.D0.BC.D0.BF.D1.82.D0.BE.D0.BC.D1.8B)
        *   [3.2.2 Временные решения](#.D0.92.D1.80.D0.B5.D0.BC.D0.B5.D0.BD.D0.BD.D1.8B.D0.B5_.D1.80.D0.B5.D1.88.D0.B5.D0.BD.D0.B8.D1.8F)
            *   [3.2.2.1 Использование динамического компоновщика](#.D0.98.D1.81.D0.BF.D0.BE.D0.BB.D1.8C.D0.B7.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D0.B5_.D0.B4.D0.B8.D0.BD.D0.B0.D0.BC.D0.B8.D1.87.D0.B5.D1.81.D0.BA.D0.BE.D0.B3.D0.BE_.D0.BA.D0.BE.D0.BC.D0.BF.D0.BE.D0.BD.D0.BE.D0.B2.D1.89.D0.B8.D0.BA.D0.B0)
            *   [3.2.2.2 Удаление библиотек среды выполнения Steam](#.D0.A3.D0.B4.D0.B0.D0.BB.D0.B5.D0.BD.D0.B8.D0.B5_.D0.B1.D0.B8.D0.B1.D0.BB.D0.B8.D0.BE.D1.82.D0.B5.D0.BA_.D1.81.D1.80.D0.B5.D0.B4.D1.8B_.D0.B2.D1.8B.D0.BF.D0.BE.D0.BB.D0.BD.D0.B5.D0.BD.D0.B8.D1.8F_Steam)
    *   [3.3 Кнопка закрытия только сворачивает окно](#.D0.9A.D0.BD.D0.BE.D0.BF.D0.BA.D0.B0_.D0.B7.D0.B0.D0.BA.D1.80.D1.8B.D1.82.D0.B8.D1.8F_.D1.82.D0.BE.D0.BB.D1.8C.D0.BA.D0.BE_.D1.81.D0.B2.D0.BE.D1.80.D0.B0.D1.87.D0.B8.D0.B2.D0.B0.D0.B5.D1.82_.D0.BE.D0.BA.D0.BD.D0.BE)
    *   [3.4 Flash не работает на 64-битных системах](#Flash_.D0.BD.D0.B5_.D1.80.D0.B0.D0.B1.D0.BE.D1.82.D0.B0.D0.B5.D1.82_.D0.BD.D0.B0_64-.D0.B1.D0.B8.D1.82.D0.BD.D1.8B.D1.85_.D1.81.D0.B8.D1.81.D1.82.D0.B5.D0.BC.D0.B0.D1.85)
    *   [3.5 Текст повреждён или не отображается](#.D0.A2.D0.B5.D0.BA.D1.81.D1.82_.D0.BF.D0.BE.D0.B2.D1.80.D0.B5.D0.B6.D0.B4.D1.91.D0.BD_.D0.B8.D0.BB.D0.B8_.D0.BD.D0.B5_.D0.BE.D1.82.D0.BE.D0.B1.D1.80.D0.B0.D0.B6.D0.B0.D0.B5.D1.82.D1.81.D1.8F)
    *   [3.6 SetLocale('en_US.UTF-8') не срабатывает при запуске игры](#SetLocale.28.27en_US.UTF-8.27.29_.D0.BD.D0.B5_.D1.81.D1.80.D0.B0.D0.B1.D0.B0.D1.82.D1.8B.D0.B2.D0.B0.D0.B5.D1.82_.D0.BF.D1.80.D0.B8_.D0.B7.D0.B0.D0.BF.D1.83.D1.81.D0.BA.D0.B5_.D0.B8.D0.B3.D1.80.D1.8B)
    *   [3.7 Игра вылетает немедленно после запуска](#.D0.98.D0.B3.D1.80.D0.B0_.D0.B2.D1.8B.D0.BB.D0.B5.D1.82.D0.B0.D0.B5.D1.82_.D0.BD.D0.B5.D0.BC.D0.B5.D0.B4.D0.BB.D0.B5.D0.BD.D0.BD.D0.BE_.D0.BF.D0.BE.D1.81.D0.BB.D0.B5_.D0.B7.D0.B0.D0.BF.D1.83.D1.81.D0.BA.D0.B0)
    *   [3.8 OpenGL не использует прямой рендеринг](#OpenGL_.D0.BD.D0.B5_.D0.B8.D1.81.D0.BF.D0.BE.D0.BB.D1.8C.D0.B7.D1.83.D0.B5.D1.82_.D0.BF.D1.80.D1.8F.D0.BC.D0.BE.D0.B9_.D1.80.D0.B5.D0.BD.D0.B4.D0.B5.D1.80.D0.B8.D0.BD.D0.B3)
    *   [3.9 Ошибка libGL при запуске некоторых игр](#.D0.9E.D1.88.D0.B8.D0.B1.D0.BA.D0.B0_libGL_.D0.BF.D1.80.D0.B8_.D0.B7.D0.B0.D0.BF.D1.83.D1.81.D0.BA.D0.B5_.D0.BD.D0.B5.D0.BA.D0.BE.D1.82.D0.BE.D1.80.D1.8B.D1.85_.D0.B8.D0.B3.D1.80)
    *   [3.10 OpenGL GLX context не использует прямой рендеринг, из-за чего происходят проблемы с производительностью или Steam вешает Xorg](#OpenGL_GLX_context_.D0.BD.D0.B5_.D0.B8.D1.81.D0.BF.D0.BE.D0.BB.D1.8C.D0.B7.D1.83.D0.B5.D1.82_.D0.BF.D1.80.D1.8F.D0.BC.D0.BE.D0.B9_.D1.80.D0.B5.D0.BD.D0.B4.D0.B5.D1.80.D0.B8.D0.BD.D0.B3.2C_.D0.B8.D0.B7-.D0.B7.D0.B0_.D1.87.D0.B5.D0.B3.D0.BE_.D0.BF.D1.80.D0.BE.D0.B8.D1.81.D1.85.D0.BE.D0.B4.D1.8F.D1.82_.D0.BF.D1.80.D0.BE.D0.B1.D0.BB.D0.B5.D0.BC.D1.8B_.D1.81_.D0.BF.D1.80.D0.BE.D0.B8.D0.B7.D0.B2.D0.BE.D0.B4.D0.B8.D1.82.D0.B5.D0.BB.D1.8C.D0.BD.D0.BE.D1.81.D1.82.D1.8C.D1.8E_.D0.B8.D0.BB.D0.B8_Steam_.D0.B2.D0.B5.D1.88.D0.B0.D0.B5.D1.82_Xorg)
    *   [3.11 Проблемы с 64-битными играми, таких как XCOM](#.D0.9F.D1.80.D0.BE.D0.B1.D0.BB.D0.B5.D0.BC.D1.8B_.D1.81_64-.D0.B1.D0.B8.D1.82.D0.BD.D1.8B.D0.BC.D0.B8_.D0.B8.D0.B3.D1.80.D0.B0.D0.BC.D0.B8.2C_.D1.82.D0.B0.D0.BA.D0.B8.D1.85_.D0.BA.D0.B0.D0.BA_XCOM)
    *   [3.12 Нет звука в некоторых играх](#.D0.9D.D0.B5.D1.82_.D0.B7.D0.B2.D1.83.D0.BA.D0.B0_.D0.B2_.D0.BD.D0.B5.D0.BA.D0.BE.D1.82.D0.BE.D1.80.D1.8B.D1.85_.D0.B8.D0.B3.D1.80.D0.B0.D1.85)
    *   [3.13 Ошибка "You are missing the following 32-bit libraries, and Steam may not run: libGL.so.1"](#.D0.9E.D1.88.D0.B8.D0.B1.D0.BA.D0.B0_.22You_are_missing_the_following_32-bit_libraries.2C_and_Steam_may_not_run:_libGL.so.1.22)
    *   [3.14 Игры не запускаются на старом оборудовании Intel](#.D0.98.D0.B3.D1.80.D1.8B_.D0.BD.D0.B5_.D0.B7.D0.B0.D0.BF.D1.83.D1.81.D0.BA.D0.B0.D1.8E.D1.82.D1.81.D1.8F_.D0.BD.D0.B0_.D1.81.D1.82.D0.B0.D1.80.D0.BE.D0.BC_.D0.BE.D0.B1.D0.BE.D1.80.D1.83.D0.B4.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D0.B8_Intel)
    *   [3.15 Некоторые игры не запускаются](#.D0.9D.D0.B5.D0.BA.D0.BE.D1.82.D0.BE.D1.80.D1.8B.D0.B5_.D0.B8.D0.B3.D1.80.D1.8B_.D0.BD.D0.B5_.D0.B7.D0.B0.D0.BF.D1.83.D1.81.D0.BA.D0.B0.D1.8E.D1.82.D1.81.D1.8F)
*   [4 Запуск игр с дополнительными параметрами, такими как Bumblebee/Primus](#.D0.97.D0.B0.D0.BF.D1.83.D1.81.D0.BA_.D0.B8.D0.B3.D1.80_.D1.81_.D0.B4.D0.BE.D0.BF.D0.BE.D0.BB.D0.BD.D0.B8.D1.82.D0.B5.D0.BB.D1.8C.D0.BD.D1.8B.D0.BC.D0.B8_.D0.BF.D0.B0.D1.80.D0.B0.D0.BC.D0.B5.D1.82.D1.80.D0.B0.D0.BC.D0.B8.2C_.D1.82.D0.B0.D0.BA.D0.B8.D0.BC.D0.B8_.D0.BA.D0.B0.D0.BA_Bumblebee.2FPrimus)
    *   [4.1 Отключение отдельных композиторов при запуске игр](#.D0.9E.D1.82.D0.BA.D0.BB.D1.8E.D1.87.D0.B5.D0.BD.D0.B8.D0.B5_.D0.BE.D1.82.D0.B4.D0.B5.D0.BB.D1.8C.D0.BD.D1.8B.D1.85_.D0.BA.D0.BE.D0.BC.D0.BF.D0.BE.D0.B7.D0.B8.D1.82.D0.BE.D1.80.D0.BE.D0.B2_.D0.BF.D1.80.D0.B8_.D0.B7.D0.B0.D0.BF.D1.83.D1.81.D0.BA.D0.B5_.D0.B8.D0.B3.D1.80)
*   [5 Using native runtime](#Using_native_runtime)
*   [6 Skins for Steam](#Skins_for_Steam)
    *   [6.1 Steam skin manager](#Steam_skin_manager)
*   [7 Changing the Steam friends notification placement](#Changing_the_Steam_friends_notification_placement)
    *   [7.1 Use a skin](#Use_a_skin)
    *   [7.2 On The fly patch](#On_The_fly_patch)
*   [8 Смотрите также](#.D0.A1.D0.BC.D0.BE.D1.82.D1.80.D0.B8.D1.82.D0.B5_.D1.82.D0.B0.D0.BA.D0.B6.D0.B5)

## Установка

**Обратите внимание:**

*   Arch Linux **не** имеет [официальной поддержки](https://support.steampowered.com/kb_article.php?ref=1504-QHXN-8366).
*   Поскольку клиент Steam является 32-битным приложением, вам необходимо включить [multilib](/index.php/Multilib_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Multilib (Русский)") репозиторий, если у вас 64-битная система. Также может понадобиться установить [multilib-devel](https://www.archlinux.org/groups/x86_64/multilib-devel/), чтобы предоставить некоторые важные multilib библиотеки.

Steam можно установить с помощью пакета [steam](https://www.archlinux.org/packages/?name=steam), доступного в [официальных репозиториях](/index.php/Official_repositories_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Official repositories (Русский)"). Если у вас 64-битная система, сначала включите репозиторий [multilib](/index.php/Multilib_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Multilib (Русский)").

Steam не сопровождается для этого дистрибутива. Поэтому пользователям придётся самим исправить некоторые недочёты в работе:

*   Steam интенсивно использует шрифт Arial. Для замены шрифта Arial воспользуйтесьпакетом [ttf-liberation](https://www.archlinux.org/packages/?name=ttf-liberation) или [шрифтами, предоставленными Steam'ом](#.D0.A2.D0.B5.D0.BA.D1.81.D1.82_.D0.BF.D0.BE.D0.B2.D1.80.D0.B5.D0.B6.D0.B4.D1.91.D0.BD_.D0.B8.D0.BB.D0.B8_.D0.BD.D0.B5_.D0.BE.D1.82.D0.BE.D0.B1.D1.80.D0.B0.D0.B6.D0.B0.D0.B5.D1.82.D1.81.D1.8F). Чтобы корректно отображались азиатские языки, установите [wqy-zenhei](https://www.archlinux.org/packages/?name=wqy-zenhei).

*   Если у вас 64-битная система, вы должны установить [32-битную версию графического драйвера](/index.php/Xorg_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#.D0.A3.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B0 "Xorg (Русский)") (пакет из столбца *Multilib* в таблице), чтобы запускать 32-битные игры.

*   Если у вас 64-битная система, вам нужно установить [lib32-alsa-plugins](https://www.archlinux.org/packages/?name=lib32-alsa-plugins), чтобы работал звук в 32-битных играх.

*   Некоторые игры имеют зависимости, которые не установлены в вашей системе. Если игра вылетает при запуске, (часто даже без сообщения об ошибке), тогда убедитесь, что вы установили все библиотеки, перечисленные в [Steam/Game-specific troubleshooting](/index.php/Steam/Game-specific_troubleshooting "Steam/Game-specific troubleshooting").

## Запуск Steam

### Режим Big Picture (из Display Manager)

Чтобы запустить Steam в режиме Big Picture из менеджера дисплеев (таких как LightDM), создайте файл `/usr/share/xsessions/steam-big-picture.desktop` со следующим содержимым:

 `/usr/share/xsessions/steam-big-picture.desktop` 
```
[Desktop Entry]
Name=Steam Big Picture Mode
Comment=Start Steam in Big Picture Mode
Exec='/usr/bin/steam -bigpicture'
TryExec='/usr/bin/steam -bigpicture'
Icon=
Type=Application
```

Также это можно сделать из Steam > Настройки > Интерфейс, отметьте галочкой 'Запускать Steam в режиме Big Picture' и запускайте Steam обычным образом. С некоторыми оконными менеджерами такой способ работает лучше, чем вариант с командной строкой.

### Запуск Steam свернутым в области уведомлений (silent mode)

Если при старте появляется главное окно Steam, вы можете добавить параметр `-silent` к команде запуска, чтобы окно не отображалось:

```
/usr/bin/steam -silent %U

```

либо же вы можете отредактировать следующий [.desktop файл](/index.php/Desktop_entries "Desktop entries"), добавив этот параметр вручную:

 `~/.config/autostart/steam.desktop` 
```
[Desktop Entry]
Name=Steam
Comment=Application for managing and playing games on Steam
Exec=/usr/bin/steam -silent %U
Icon=steam
Terminal=false
Type=Application
Categories=Network;FileTransfer;Game;
MimeType=x-scheme-handler/steam;
Actions=Store;Community;Library;Servers;Screenshots;News;Settings;BigPicture;Friends;
...
```

## Решение проблем

**Совет:** Скрипт `/usr/bin/steam` перенаправляет стандартный вывод из stdout и stderr Steam в файл `/tmp/dumps/${USER}_stdout.txt`. Это означает, что вам не обязательно запускать Steam в терминале для ознакомления с данным выводом.

**Обратите внимание:** В дополнение к описанию здесь, любой баг/исправление/ошибка должны быть (если ещё не) сообщены в баг-трекер компании Valve на их [странице GitHub](https://github.com/ValveSoftware/steam-for-linux).

### Проблемы с драйверами nvidia версии 361.28

При запуске некоторых игр возникает ошибка, появившаяся в драйверах nvidia версии 361.28

 `"Missing basic OpenGL v1.0 -> v2.0 required OpenGL functionality."` 

До исправления NVIDIA данной ошибки вы можете использовать следующий параметр для запуска для проблемной игры:

 `__GLVND_DISALLOW_PATCHING=1 %command%` 

либо же вы можете откатить версию драйверов nvidia до 361.16

### Проблемы среды выполнения Steam

Steam устанавливает собственные, часто устаревшие версии библиотек, также называемые "Steam Runtime" (среда выполнения Steam). Данные библиотеки, вероятно, будут часто конфликтовать с теми, которые включены в Arch Linux.

#### Возможные симптомы

Некоторые из возможных симптомов данных проблем проявляются в зависании или сбоях при запуске клиента Steam, а также в виде следующих ошибок:

```
libGL error: unable to load driver: some_driver_dri.so
libGL error: driver pointer missing
libGL error: failed to load driver: some_driver
libGL error: unable to load driver: swrast_dri.so
libGL error: failed to load driver: swrast
```

```
Failed to load libGL: undefined symbol: xcb_send_fd

```

```
ERROR: ld.so: object '~/.local/share/Steam/ubuntu12_32/gameoverlayrenderer.so' from LD_PRELOAD cannot be preloaded (wrong ELF class: ELFCLASS32): ignored.

```

```
OpenGL GLX context is not using direct rendering, which may cause performance problems. [(смотри ниже)](#OpenGL_.D0.BD.D0.B5_.D0.B8.D1.81.D0.BF.D0.BE.D0.BB.D1.8C.D0.B7.D1.83.D0.B5.D1.82_.D0.BF.D1.80.D1.8F.D0.BC.D0.BE.D0.B9_.D1.80.D0.B5.D0.BD.D0.B4.D0.B5.D1.80.D0.B8.D0.BD.D0.B3)

```

```
Could not find required OpenGL entry point 'glGetError'! Either your video card is unsupported or your OpenGL driver needs to be updated.

```

**Обратите внимание:** Неправильно настроенный firewall (брандмауэр) также может вызывать проблемы в работе Steam, которые схожи с симптомами проблем среды выполнения, вследствие того, что у Steam происходит сбой всякий раз, когда клиент не может установить соединение со стимовскими серверами, а также большинство игр просто не запускаются из-за того, что Steam API не загружается.

#### Временные решения

Вы можете решить данную проблему заставив Steam принудительно использовать актуальные версии библиотек (установленные с помощью [pacman](/index.php/Pacman_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Pacman (Русский)")) следующими двумя способами.

##### Использование динамического компоновщика

Динамический компоновщик (`man 8 ld.so`) может загружать определённые библиотеки с помощью [переменной окружения](/index.php/Environment_variables_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Environment variables (Русский)") `LD_PRELOAD`.

```
LD_PRELOAD='/usr/$LIB/libstdc++.so.6 /usr/$LIB/libgcc_s.so.1 /usr/$LIB/libxcb.so.1' steam

```

При использовании .desktop файла вы можете использовать команду в строке **Exec=**

```
env LD_PRELOAD='/usr/$LIB/libstdc++.so.6 /usr/$LIB/libgcc_s.so.1 /usr/$LIB/libxcb.so.1' /usr/bin/steam %U

```

**Обратите внимание:** Указанное выше значение '$LIB' не является переменной, а выступает как указание компоновщику использовать соответствующую архитектуру для библиотеки. Одиночные кавычки необходимы для предотвращения определения командной оболочки значения $LIB как переменной.

##### Удаление библиотек среды выполнения Steam

Запустите следующую команду для удаления конфликтных библиотек среды выполнения Steam, вызывающих проблемы в Arch Linux:

```
find ~/.steam/root/ \( -name "libgcc_s.so*" -o -name "libstdc++.so*" -o -name "libxcb.so*" \) -print -delete

```

Если указанная выше команда не сработала, то запустите её ещё раз, а затем запустите следующую команду.

```
find ~/.local/share/Steam/ \( -name "libgcc_s.so*" -o -name "libstdc++.so*" -o -name "libxcb.so*" \) -print -delete

```

**Обратите внимание:** Во время обновления Steam часто восстанавливает собственные библиотеки среды выполнения, поэтому до окончательного решения проблемы вам следует после окончания обновления Steam закрыть клиент, удалить библиотеки и запустить Steam опять.

Если вы хотите восстановить файлы, которые были удалены указанной выше командой, то вы можете воспользоваться встроенной функцией сброса Steam.

**Важно:** `--reset` также удалит игры (каталог по умолчанию SteamApps).

```
bc|steam --reset

```

### Кнопка закрытия только сворачивает окно

	Valve GitHub [issue 1025](https://github.com/ValveSoftware/steam-for-linux/issues/1025)

Чтобы окно Steam закрывалось (и убиралось из панели задач) при нажатии **крестика**, но сам Steam продолжал работать в трее, установите переменную окружения `STEAM_FRAME_FORCE_CLOSE` в значение `1`. Это можно сделать, запустив Steam следующей командой:

```
$ STEAM_FRAME_FORCE_CLOSE=1 steam

```

Если вы запускаете Steam через .desktop файл, вы должны изменить строку с `Exec` следующим образом:

```
 Exec=sh -c 'STEAM_FRAME_FORCE_CLOSE=1 steam' %U

```

### Flash не работает на 64-битных системах

	[Статья](https://support.steampowered.com/kb_article.php?ref=1493-GHZB-7612) на сайте поддержки Steam

Сначала убедитесь, что пакет [lib32-flashplugin](https://www.archlinux.org/packages/?name=lib32-flashplugin) установлен. Теперь должно заработать. Если это не так, создайте папку локальной версии Flash плагина для Steam:

```
$ mkdir ~/.steam/bin32/plugins/

```

и создайте символьную ссылку на глобальный файл lib32 flash plugin в этой папке:

```
$ ln -s /usr/lib32/mozilla/plugins/libflashplayer.so ~/.steam/bin32/plugins/

```

### Текст повреждён или не отображается

[Инструкция](https://support.steampowered.com/kb_article.php?ref=1974-YFKL-4947) для Windows от поддержки Steam также работает и на Linux.

Вы можете установить их пакетом [steam-fonts](https://aur.archlinux.org/packages/steam-fonts/) из [AUR (Русский)](/index.php/AUR_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "AUR (Русский)"), или вручную, скачав и [установив](/index.php/Fonts#Manual_installation "Fonts") [SteamFonts.zip](https://support.steampowered.com/downloads/1974-YFKL-4947/SteamFonts.zip).

### SetLocale('en_US.UTF-8') не срабатывает при запуске игры

Раскомментируйте `en_US.UTF-8 UTF-8` в файле `/etc/locale.gen`, затем выполните `locale-gen` от имени суперпользователя.

### Игра вылетает немедленно после запуска

Если игра сразу же вылетает, попробуйте отключить: *"Enable the Steam Overlay while in-game"* в *Properties* игры.

### OpenGL не использует прямой рендеринг

	[Статья](https://support.steampowered.com/kb_article.php?ref=9938-EYZB-7457) на сайте поддержки Steam

Возможно, вы не установили 32-битный графический драйвер. Узнайте из статьи [Xorg](/index.php/Xorg#Driver_installation "Xorg") какой пакет вам нужно установить.

Вы можете проверить/протестировать, установлен ли он правильно, установив [lib32-mesa-demos](https://www.archlinux.org/packages/?name=lib32-mesa-demos) и запустив следующую команду:

```
$ glxinfo32 | grep OpenGL.

```

### Ошибка libGL при запуске некоторых игр

Если у вас возникает ошибка вида `Failed to load libGL: undefined symbol: xcb_send_fd`, это может происходить из-за устаревших библиотек среды выполнения Steam. Удаление `~/.local/share/Steam/ubuntu12_32/steam-runtime/i386/usr/lib/i386-linux-gnu/libxcb.so.1` заставит Steam загружать версии библиотек, установленных pacman'ом.

### OpenGL GLX context не использует прямой рендеринг, из-за чего происходят проблемы с производительностью или Steam вешает Xorg

Steam распространяется со своими собственными версиями некоторых библиотек, и они иногда настолько устаревают, что не могут работать с системными библиотеками Arch Linux. Удаление библиотек, распространяющихся со Steam приведёт к тому, что Steam будет вынужден использовать новые версии из Arch Linux. [Обсуждение на форуме](https://bbs.archlinux.org/viewtopic.php?pid=1416098#p1416098).

```
rm ~/.local/share/Steam/ubuntu12_32/steam-runtime/i386/usr/lib/i386-linux-gnu/libstdc++.so.6
rm ~/.local/share/Steam/ubuntu12_32/steam-runtime/i386/lib/i386-linux-gnu/libgcc_s.so.1
rm ~/.local/share/Steam/ubuntu12_32/steam-runtime/amd64/lib/x86_64-linux-gnu/libgcc_s.so.1
rm ~/.local/share/Steam/ubuntu12_32/steam-runtime/amd64/usr/lib/x86_64-linux-gnu/libstdc++.so.6

```

### Проблемы с 64-битными играми, таких как XCOM

Steam распространяется со своими собственными версиями некоторых библиотек, и они иногда настолько устаревают, что не могут работать с системными библиотеками Arch Linux. Удаление библиотек, распространяющихся со Steam приведёт к тому, что Steam будет вынужден использовать новые версии из Arch Linux. [[1]](https://bbs.archlinux.org/viewtopic.php?pid=1428375#p1428375).

```
rm ~/.local/share/Steam/ubuntu12_32/steam-runtime/amd64/lib/x86_64-linux-gnu/libgcc_s.so.1
rm ~/.local/share/Steam/ubuntu12_32/steam-runtime/amd64/usr/lib/x86_64-linux-gnu/libstdc++.so.6
```

### Нет звука в некоторых играх

Если в некоторых играх нет звука, и инструкции из статьи [Steam/Game-specific troubleshooting](/index.php/Steam/Game-specific_troubleshooting "Steam/Game-specific troubleshooting") не решили проблему, то [использование родной среды выполнения](#Using_native_runtime) может дать положительный результат.

### Ошибка "You are missing the following 32-bit libraries, and Steam may not run: libGL.so.1"

У вас может возникнуть такая ошибка при первом запуска Steam. Убедитесь, что вы установили lib32-версии всех ваших графических драйверов. Например, если вы установили [catalyst-utils-pxp](https://www.archlinux.org/packages/?name=catalyst-utils-pxp), [xf86-video-dri](https://www.archlinux.org/packages/?name=xf86-video-dri), [intel-dri](https://www.archlinux.org/packages/?name=intel-dri), [mesa-libgl](https://www.archlinux.org/packages/?name=mesa-libgl) для AMD и Intel двойных карт, то вам следует установить [lib32-catalyst-utils-pxp](https://www.archlinux.org/packages/?name=lib32-catalyst-utils-pxp), [lib32-intel-dri](https://www.archlinux.org/packages/?name=lib32-intel-dri), [lib32-mesa-libgl](https://www.archlinux.org/packages/?name=lib32-mesa-libgl).

### Игры не запускаются на старом оборудовании Intel

На старом оборудовании Intel, если игра при запуске немедленно вылетает, это может происходить из-за того, что оборудование не поддерживает последний OpenGL. Это проявляется как ошибка gameoverlayrenderer.so в /tmp/dumps/mobile_stdout.txt, но читая /tmp/gameoverlayrenderer.log вы видите ошибку GLXBadFBConfig.

Однако, это можно исправить, заставив игру использовать более позднюю версию OpenGL, чем она требует. Нажмите правой кнопкой мыши по игре, выберите Свойства. Затем нажмите "Установить параметры запуска" во вкладке "Основное" и вставьте следующее:

```
MESA_GL_VERSION_OVERRIDE=3.1 MESA_GLSL_VERSION_OVERRIDE=140 %command%

```

Это заставит игру использовать последнюю версию OpenGL.

### Некоторые игры не запускаются

Некоторые игры не запускаются и выводят что-то вроде:

 `ERROR: ld.so: object '~/.local/share/Steam/ubuntu12_32/gameoverlayrenderer.so' from LD_PRELOAD cannot be preloaded (wrong ELF class: ELFCLASS32): ignored.` Это значит, что прилагающаяся libstdc++.so конфликтует с чем-то [описанным здесь](https://bbs.archlinux.org/viewtopic.php?id=181171). Решением является установка переменной окружения STEAM_RUNTIME в значение 0 и выполнение следующей команды: `rm ~/.local/share/Steam/ubuntu12_32/steam-runtime/i386/usr/lib/i386-linux-gnu/libstdc++.so.6` 

## Запуск игр с дополнительными параметрами, такими как Bumblebee/Primus

Steam может запускать игры, используя ваши собственные команды. Чтобы это сделать, перейдите в вашу Библиотеку игр, щёлкните правой кнопкой мыши по нужной игре, выбирете Свойства, Установить параметры запуска. Steam заменит тег `%command%` на команду, на ту, которую он выполнит по факту. Например, чтобы запустить Team Fortress 2 с primusrun и разрешением 1920x1080, вы должны ввести:

```
primusrun %command% -w 1920 -h 1080

```

Если вы используете ядро [Linux-ck](/index.php/Linux-ck "Linux-ck"), вы можете уменьшить задержки и увеличить производительность, запустив игру в SCHED_ISO (низкие задержки, избежание перегрузки CPU) с помощью [schedtool](https://www.archlinux.org/packages/?name=schedtool)

```
# schedtool -I -e %command% *other arguments*

```

### Отключение отдельных композиторов при запуске игр

В дополнение к этому, используйте `%command%` для того, чтобы убивать отдельные композиторы, (такие как Xcompmgr или [Compton](/index.php/Compton_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Compton (Русский)")), из-за которых игра может глючить и тормозить на некоторых системах, и запускать их снова после выхода из игры, добавив в опции запуска игры следующее:

```
 killall compton && %command%; nohup compton &

```

Замените `compton` в приведённой выше команде на ваш композитор. Вы также можете добавить -options к `%command%` или `compton`.

Steam будет родительским процессом для любой команды, написанной после `%command%` и ваш Steam статус будет отображаться как "в игре". Поэтому, в этом примере мы используем композитор через `nohup`, таким образом он не будет привязан к процессу Steam (и будет продолжать работать после закрытия Steam), а завершение команды амперсандом сбросит ваш статус Steam.

## Using native runtime

Steam, by default, ships with a copy of every library it uses, packaged within itself, so that games can launch without issue. This can be a resource hog, and the slightly out-of-date libraries they package may be missing important features (Notably, the OpenAL version they ship lacks HRTF and surround71 support). To use your own system libraries, you can run Steam with:

```
$ STEAM_RUNTIME=0 steam

```

However, if you're missing any libraries Steam makes use of, this will fail to launch properly. An easy way to find the missing libraries is to run the following commands:

```
$ cd ~/.local/share/Steam/ubuntu12_32
$ LD_LIBRARY_PATH=".:${LD_LIBRARY_PATH}" ldd $(file *|sed '/ELF/!d;s/:.*//g')|grep 'not found'|sort|uniq

```

**Note:** The libraries will have to be 32-bit, which means you may have to download some from the AUR if on x86_64, such as NetworkManager.

Once you've done this, run steam again with `STEAM_RUNTIME=0 steam` and verify it's not loading anything outside of the handful of steam support libraries:

```
$ cat /proc/$(pidof steam)/maps|sed '/\.local/!d;s/.*  //g'|sort|uniq

```

One easy way to gather and install all of those libraries is a package in the AUR that's really way harder to find than it should be, called steam-native.

## Skins for Steam

**Note:** Using skins that are not up-to-date with the version of the Steam client may cause visual errors.

The Steam interface can be fully customized by copying its various interface files in its skins directory and modifying them.

An extensive list of skins can be found on [Steam's forums](http://forums.steampowered.com/forums/showthread.php?t=1161035).

### Steam skin manager

The process of applying a skin to Steam can be greatly simplified using [steam-skin-manager](https://aur.archlinux.org/packages/steam-skin-manager/). The package also comes with a hacked version of the Steam launcher which allows the window manager to draw its borders on the Steam window.

As a result, skins for Steam will come in two flavors, one with and one without window buttons. The skin manager will prompt you whether you use the hacked version or not, and will automatically apply the theme corresponding to your GTK+ theme if it is found. You can of course still apply another skin if you want.

The package ships with two themes for the default Ubuntu themes, Ambiance and Radiance.

## Changing the Steam friends notification placement

**Note:** A handful of games do not support this, for example this can not work with XCOM: Enemy Unknown.

### Use a skin

You can create a skin that does nothing but change the notification corner. To save yourself from creating these manually I have uploaded them to mediafire. You can [download them here](http://www.mediafire.com/download/lnt2cjlbcdccm11/Steam-Notifications.zip) and then extract them into your home folder (make sure it is not extracted into a subdirectory, i.e. the .local folder in the zip needs to go into your home directory) after that you will have to open Steam, go to it's Settings, and enter the Interface tab. Then in the drop-down list where it says **< default skin >** you can select the desired skin and finally move that notification out of your way!

If you would like to manually create the files, here is how you can do it. First you need to create the directories:

```
 mkdir -p $HOME/Top-Right/resource
 cp -R $HOME/.steam/steam/resource/styles $HOME/Top-Right/resource/
 mv $HOME/Top-Right $HOME/.local/share/Steam/skins/
 cd .local/share/Steam/skins/
 cp -R Top-Right Top-Left && cp -R Top-Right Bottom-Right

```

Then with a text editor of your choosing open the file you wish to modify, the **gameoverlay.style** will change the corner for the in-game overlay whereas the **steam.style** will change it for your desktop. In this example I will use nano and the in-game overlay file.

```
 nano Top-Right/resource/styles/gameoverlay.style

```

Now find the entry: **Notifications.PanelPosition** in whichever file you opened and change it to the appropriate value, for example for Top-Right:

```
 Notifications.PanelPosition     "TopRight"

```

This line will look the same in both files. Repeat the process for all the 3 variants (Top-Right, Top-Left and Bottom-Left) and adjust the corners for the desktop and in-game overlay to your satisfaction for each skin, then save the files.

To finish you will have to select the skin in Steam as explained above. You can use these files across distributions and even between Windows and Linux (OS X has it's own entry for the desktop notification placement)

### On The fly patch

This method is more compatible with future updates of Steams since the files in the skins above are updated as part of steam and as such if the original files change, the skin will not follow the graphics update to steam and will have to be re-created every time something like that happens. Doing things this way will also give you the ability to use per-game notification locations as you can run a patch changing the location of the notifications by specifying it in the launch options for games.

Steam updates the files we need to edit everytime it updates (which is everytime it is launched) so the most effective way to do this is patching the file after Steam has already been launched.

First you will need [this patch](http://www.mediafire.com/download/ao3dhpdg9omj94r/topright.patch)[(pastebin ver)](http://pastebin.com/FWHZNdUU). you can edit the entry and change it between "BottomRight"(default), "TopRight" "TopLeft" and "BottomLeft" but I will assume you used "TopRight" as in the original file. Save that file as **$HOME/.steam/topright.patch**.

**Note:** For pastebin to work you need to copy the raw data from line 1 through line 12 (line 12 is whitespace, but the patch will fail without it, this is why I provided a mediafire version too) you basically need to start copying behind the "-" sign at the bottom of the raw paste data and go up from there.

Next create an alias in your **$HOME/.bashrc**

```
 alias steam_topright='pushd $HOME/.steam/ && patch -p1 -f -r - --no-backup-if-mismatch < topright.patch && popd'

```

Log out and back in to refresh the aliases. Launch Steam and wait for it to fully load, then run the alias

```
 $ steam_topright

```

And most games you launch after this will have their notification in the upper right corner.

You can also duplicate the patch and make more aliases for the other corners if you don't want all games to use the same corner so you can switch back.

To automate the process you will need a script file as steam launch options cannot read your aliases. The location and name of the file could for example be **$HOME/.scripts/steam_topright.sh**, and assuming that's the path you used, it needs to be executable:

```
 $ chmod +755 $HOME/.scripts/steam_topright.sh

```

The contents of the file should be the following:

```
 #!/bin/sh
 pushd $HOME/.steam/ && patch -p1 -f -r - --no-backup-if-mismatch < topright.patch && popd

```

And the launch options should be something like the following.

```
 $HOME/.scripts/steam_topright.sh && %command%

```

There is another file in the same folder as **gameoverlay.style** folder called **steam.style** which has an entry with the exact same function as the file we patched and will change the notification corner for the desktop only (not in-game), but for editing this file to actually work it has to be set before steam is launched and the folder set to read-only so steam cannot re-write the file. Therefore the only two ways to modify that file is to make the directory read only so steam cannot change it when it is launched (can break updates) or making a skin like in method 1.

## Смотрите также

*   [https://wiki.gentoo.org/wiki/Steam](https://wiki.gentoo.org/wiki/Steam)