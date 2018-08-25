Смотрите основную статью: [Steam](/index.php/Steam_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Steam (Русский)")

**Совет:** Скрипт `/usr/bin/steam` перенаправляет стандартный вывод из stdout и stderr Steam в файл `/tmp/dumps/${USER}_stdout.txt`. Это означает, что вам не обязательно запускать Steam в терминале для ознакомления с данным выводом.

**Примечание:** В дополнение к описанию здесь, любой баг/исправление/ошибка должны быть (если ещё не) сообщены в баг-трекер компании Valve на их [странице GitHub](https://github.com/ValveSoftware/steam-for-linux).

## Contents

*   [1 Проблемы с драйверами nvidia версии 361.28](#.D0.9F.D1.80.D0.BE.D0.B1.D0.BB.D0.B5.D0.BC.D1.8B_.D1.81_.D0.B4.D1.80.D0.B0.D0.B9.D0.B2.D0.B5.D1.80.D0.B0.D0.BC.D0.B8_nvidia_.D0.B2.D0.B5.D1.80.D1.81.D0.B8.D0.B8_361.28)
*   [2 Проблемы среды выполнения Steam](#.D0.9F.D1.80.D0.BE.D0.B1.D0.BB.D0.B5.D0.BC.D1.8B_.D1.81.D1.80.D0.B5.D0.B4.D1.8B_.D0.B2.D1.8B.D0.BF.D0.BE.D0.BB.D0.BD.D0.B5.D0.BD.D0.B8.D1.8F_Steam)
    *   [2.1 Возможные симптомы](#.D0.92.D0.BE.D0.B7.D0.BC.D0.BE.D0.B6.D0.BD.D1.8B.D0.B5_.D1.81.D0.B8.D0.BC.D0.BF.D1.82.D0.BE.D0.BC.D1.8B)
    *   [2.2 Временные решения](#.D0.92.D1.80.D0.B5.D0.BC.D0.B5.D0.BD.D0.BD.D1.8B.D0.B5_.D1.80.D0.B5.D1.88.D0.B5.D0.BD.D0.B8.D1.8F)
        *   [2.2.1 Использование динамического компоновщика](#.D0.98.D1.81.D0.BF.D0.BE.D0.BB.D1.8C.D0.B7.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D0.B5_.D0.B4.D0.B8.D0.BD.D0.B0.D0.BC.D0.B8.D1.87.D0.B5.D1.81.D0.BA.D0.BE.D0.B3.D0.BE_.D0.BA.D0.BE.D0.BC.D0.BF.D0.BE.D0.BD.D0.BE.D0.B2.D1.89.D0.B8.D0.BA.D0.B0)
        *   [2.2.2 Удаление библиотек среды выполнения Steam](#.D0.A3.D0.B4.D0.B0.D0.BB.D0.B5.D0.BD.D0.B8.D0.B5_.D0.B1.D0.B8.D0.B1.D0.BB.D0.B8.D0.BE.D1.82.D0.B5.D0.BA_.D1.81.D1.80.D0.B5.D0.B4.D1.8B_.D0.B2.D1.8B.D0.BF.D0.BE.D0.BB.D0.BD.D0.B5.D0.BD.D0.B8.D1.8F_Steam)
*   [3 Проблема при использовании нескольких мониторов](#.D0.9F.D1.80.D0.BE.D0.B1.D0.BB.D0.B5.D0.BC.D0.B0_.D0.BF.D1.80.D0.B8_.D0.B8.D1.81.D0.BF.D0.BE.D0.BB.D1.8C.D0.B7.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D0.B8_.D0.BD.D0.B5.D1.81.D0.BA.D0.BE.D0.BB.D1.8C.D0.BA.D0.B8.D1.85_.D0.BC.D0.BE.D0.BD.D0.B8.D1.82.D0.BE.D1.80.D0.BE.D0.B2)
*   [4 Родная среда выполнения: steam.sh line 756 ошибка сегментации](#.D0.A0.D0.BE.D0.B4.D0.BD.D0.B0.D1.8F_.D1.81.D1.80.D0.B5.D0.B4.D0.B0_.D0.B2.D1.8B.D0.BF.D0.BE.D0.BB.D0.BD.D0.B5.D0.BD.D0.B8.D1.8F:_steam.sh_line_756_.D0.BE.D1.88.D0.B8.D0.B1.D0.BA.D0.B0_.D1.81.D0.B5.D0.B3.D0.BC.D0.B5.D0.BD.D1.82.D0.B0.D1.86.D0.B8.D0.B8)
*   [5 Кнопка закрытия только сворачивает окно](#.D0.9A.D0.BD.D0.BE.D0.BF.D0.BA.D0.B0_.D0.B7.D0.B0.D0.BA.D1.80.D1.8B.D1.82.D0.B8.D1.8F_.D1.82.D0.BE.D0.BB.D1.8C.D0.BA.D0.BE_.D1.81.D0.B2.D0.BE.D1.80.D0.B0.D1.87.D0.B8.D0.B2.D0.B0.D0.B5.D1.82_.D0.BE.D0.BA.D0.BD.D0.BE)
*   [6 Flash не работает на 64-битных системах](#Flash_.D0.BD.D0.B5_.D1.80.D0.B0.D0.B1.D0.BE.D1.82.D0.B0.D0.B5.D1.82_.D0.BD.D0.B0_64-.D0.B1.D0.B8.D1.82.D0.BD.D1.8B.D1.85_.D1.81.D0.B8.D1.81.D1.82.D0.B5.D0.BC.D0.B0.D1.85)
*   [7 Текст повреждён или не отображается](#.D0.A2.D0.B5.D0.BA.D1.81.D1.82_.D0.BF.D0.BE.D0.B2.D1.80.D0.B5.D0.B6.D0.B4.D1.91.D0.BD_.D0.B8.D0.BB.D0.B8_.D0.BD.D0.B5_.D0.BE.D1.82.D0.BE.D0.B1.D1.80.D0.B0.D0.B6.D0.B0.D0.B5.D1.82.D1.81.D1.8F)
*   [8 SetLocale('en_US.UTF-8') не срабатывает при запуске игры](#SetLocale.28.27en_US.UTF-8.27.29_.D0.BD.D0.B5_.D1.81.D1.80.D0.B0.D0.B1.D0.B0.D1.82.D1.8B.D0.B2.D0.B0.D0.B5.D1.82_.D0.BF.D1.80.D0.B8_.D0.B7.D0.B0.D0.BF.D1.83.D1.81.D0.BA.D0.B5_.D0.B8.D0.B3.D1.80.D1.8B)
*   [9 Игра вылетает немедленно после запуска](#.D0.98.D0.B3.D1.80.D0.B0_.D0.B2.D1.8B.D0.BB.D0.B5.D1.82.D0.B0.D0.B5.D1.82_.D0.BD.D0.B5.D0.BC.D0.B5.D0.B4.D0.BB.D0.B5.D0.BD.D0.BD.D0.BE_.D0.BF.D0.BE.D1.81.D0.BB.D0.B5_.D0.B7.D0.B0.D0.BF.D1.83.D1.81.D0.BA.D0.B0)
*   [10 OpenGL не использует прямой рендеринг](#OpenGL_.D0.BD.D0.B5_.D0.B8.D1.81.D0.BF.D0.BE.D0.BB.D1.8C.D0.B7.D1.83.D0.B5.D1.82_.D0.BF.D1.80.D1.8F.D0.BC.D0.BE.D0.B9_.D1.80.D0.B5.D0.BD.D0.B4.D0.B5.D1.80.D0.B8.D0.BD.D0.B3)
*   [11 Ошибка libGL при запуске некоторых игр](#.D0.9E.D1.88.D0.B8.D0.B1.D0.BA.D0.B0_libGL_.D0.BF.D1.80.D0.B8_.D0.B7.D0.B0.D0.BF.D1.83.D1.81.D0.BA.D0.B5_.D0.BD.D0.B5.D0.BA.D0.BE.D1.82.D0.BE.D1.80.D1.8B.D1.85_.D0.B8.D0.B3.D1.80)
*   [12 OpenGL не использует прямой рендеринг / Steam вешает Xorg](#OpenGL_.D0.BD.D0.B5_.D0.B8.D1.81.D0.BF.D0.BE.D0.BB.D1.8C.D0.B7.D1.83.D0.B5.D1.82_.D0.BF.D1.80.D1.8F.D0.BC.D0.BE.D0.B9_.D1.80.D0.B5.D0.BD.D0.B4.D0.B5.D1.80.D0.B8.D0.BD.D0.B3_.2F_Steam_.D0.B2.D0.B5.D1.88.D0.B0.D0.B5.D1.82_Xorg)
*   [13 Проблемы с 64-битными играми, таких как XCOM](#.D0.9F.D1.80.D0.BE.D0.B1.D0.BB.D0.B5.D0.BC.D1.8B_.D1.81_64-.D0.B1.D0.B8.D1.82.D0.BD.D1.8B.D0.BC.D0.B8_.D0.B8.D0.B3.D1.80.D0.B0.D0.BC.D0.B8.2C_.D1.82.D0.B0.D0.BA.D0.B8.D1.85_.D0.BA.D0.B0.D0.BA_XCOM)
*   [14 Нет звука в некоторых играх](#.D0.9D.D0.B5.D1.82_.D0.B7.D0.B2.D1.83.D0.BA.D0.B0_.D0.B2_.D0.BD.D0.B5.D0.BA.D0.BE.D1.82.D0.BE.D1.80.D1.8B.D1.85_.D0.B8.D0.B3.D1.80.D0.B0.D1.85)
*   [15 Missing libGL](#Missing_libGL)
*   [16 Игры не запускаются на старом оборудовании Intel](#.D0.98.D0.B3.D1.80.D1.8B_.D0.BD.D0.B5_.D0.B7.D0.B0.D0.BF.D1.83.D1.81.D0.BA.D0.B0.D1.8E.D1.82.D1.81.D1.8F_.D0.BD.D0.B0_.D1.81.D1.82.D0.B0.D1.80.D0.BE.D0.BC_.D0.BE.D0.B1.D0.BE.D1.80.D1.83.D0.B4.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D0.B8_Intel)
*   [17 Некоторые игры не запускаются](#.D0.9D.D0.B5.D0.BA.D0.BE.D1.82.D0.BE.D1.80.D1.8B.D0.B5_.D0.B8.D0.B3.D1.80.D1.8B_.D0.BD.D0.B5_.D0.B7.D0.B0.D0.BF.D1.83.D1.81.D0.BA.D0.B0.D1.8E.D1.82.D1.81.D1.8F)

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

**Примечание:** Неправильно настроенный firewall (брандмауэр) также может вызывать проблемы в работе Steam, которые схожи с симптомами проблем среды выполнения, вследствие того, что у Steam происходит сбой всякий раз, когда клиент не может установить соединение со стимовскими серверами, а также большинство игр просто не запускаются из-за того, что Steam API не загружается.

#### Временные решения

Вы можете решить данную проблему заставив Steam принудительно использовать актуальные версии библиотек (установленные с помощью [pacman](/index.php/Pacman_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Pacman (Русский)")) следующими двумя способами.

##### Использование динамического компоновщика

Динамический компоновщик ([ld.so(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/ld.so.8)) может загружать определённые библиотеки с помощью [переменной окружения](/index.php/Environment_variables_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Environment variables (Русский)") `LD_PRELOAD`.

```
LD_PRELOAD='/usr/$LIB/libstdc++.so.6 /usr/$LIB/libgcc_s.so.1 /usr/$LIB/libxcb.so.1' steam

```

При использовании .desktop файла вы можете использовать команду в строке **Exec=**

```
env LD_PRELOAD='/usr/$LIB/libstdc++.so.6 /usr/$LIB/libgcc_s.so.1 /usr/$LIB/libxcb.so.1' /usr/bin/steam %U

```

**Примечание:** Указанное выше значение '$LIB' не является переменной, а выступает как указание компоновщику использовать соответствующую архитектуру для библиотеки. Одиночные кавычки необходимы для предотвращения определения командной оболочки значения $LIB как переменной.

##### Удаление библиотек среды выполнения Steam

Запустите следующую команду для удаления конфликтных библиотек среды выполнения Steam, вызывающих проблемы в Arch Linux:

```
find ~/.steam/root/ \( -name "libgcc_s.so*" -o -name "libstdc++.so*" -o -name "libxcb.so*" \) -print -delete

```

Если указанная выше команда не сработала, то запустите её ещё раз, а затем запустите следующую команду.

```
find ~/.local/share/Steam/ \( -name "libgcc_s.so*" -o -name "libstdc++.so*" -o -name "libxcb.so*" \) -print -delete

```

**Примечание:** Во время обновления Steam часто восстанавливает собственные библиотеки среды выполнения, поэтому до окончательного решения проблемы вам следует после окончания обновления Steam закрыть клиент, удалить библиотеки и запустить Steam опять.

Если вы хотите восстановить файлы, которые были удалены указанной выше командой, то вы можете воспользоваться встроенной функцией сброса Steam.

**Важно:** `--reset` также удалит игры (каталог по умолчанию SteamApps).

```
bc|steam --reset

```

### Проблема при использовании нескольких мониторов

Использование нескольких мониторов может вызвать следующую ошибку: `ERROR: ld.so: object '~/.local/share/Steam/ubuntu12_32/gameoverlayrenderer.so' from LD_PRELOAD cannot be preloaded (wrong ELF class: ELFCLASS32): ignored.` которая приводит к сбою при запуске игры. При возникновении данной ошибки вы можете отключить дополнительные экраны и затем запустить игру. В случае успешного запуска игры вы можете включить экраны снова.

Также вы можете попробовать выполнить данную команду:

```
export LD_LIBRARY_PATH=/usr/lib32/nvidia:/usr/lib/nvidia:$LD_LIBRARY_PATH

```

и затем запустить steam.

### Родная среда выполнения: steam.sh line 756 ошибка сегментации

	Valve GitHub [issue 3863](https://github.com/ValveSoftware/steam-for-linux/issues/3863)

Согласно вышеупомянутому отчёту в Steam происходит сбой с ошибкой `/home/<username>/.local/share/Steam/steam.sh: line 756: <различный числовой код> Segmentation fault (core dumped)` при запуске с параметром `STEAM_RUNTIME=0`.

Единственное предложенное решение - это копирование собственных 32-битных библиотек Steam libusb и libgudev в /usr/lib32:

```
# cp $HOME/.local/share/Steam/ubuntu12_32/steam-runtime/i386/usr/lib/i386-linux-gnu/libgudev* /usr/lib32
# cp $HOME/.local/share/Steam/ubuntu12_32/steam-runtime/i386/lib/i386-linux-gnu/libusb* /usr/lib32
```

Следует отметить, что данный способ необходимо применять в тех системах, где установлены lib32-libgudev и lib32-libusb

### Кнопка закрытия только сворачивает окно

	Valve GitHub [issue 1025](https://github.com/ValveSoftware/steam-for-linux/issues/1025)

Чтобы окно Steam закрывалось (и убиралось из панели задач) при нажатии **крестика**, но сам Steam продолжал работать в трее, установите переменную окружения `STEAM_FRAME_FORCE_CLOSE` в значение `1`. (См. [Переменные окружения#Графические приложения](/index.php/Environment_variables_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#.D0.93.D1.80.D0.B0.D1.84.D0.B8.D1.87.D0.B5.D1.81.D0.BA.D0.B8.D0.B5_.D0.BF.D1.80.D0.B8.D0.BB.D0.BE.D0.B6.D0.B5.D0.BD.D0.B8.D1.8F "Environment variables (Русский)")). Это можно сделать, запустив Steam следующей командой:

```
$ STEAM_FRAME_FORCE_CLOSE=1 steam

```

Если вы запускаете Steam через .desktop файл, вы должны изменить строку с `Exec` следующим образом:

```
 Exec=sh -c 'STEAM_FRAME_FORCE_CLOSE=1 steam' %U. 

```

Для использования данной переменной окружения при запуске Steam вы можете добавить `export STEAM_FRAME_FORCE_CLOSE=1` в скрипт `/usr/bin/steam`

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

### OpenGL не использует прямой рендеринг / Steam вешает Xorg

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

### Missing libGL

You may encounter this error when you launch Steam at first time.

```
You are missing the following 32-bit libraries, and Steam may not run: libGL.so.1

```

Make sure you have installed the `lib32` version of all your video drivers as described in [Xorg#Driver installation](/index.php/Xorg#Driver_installation "Xorg").

If you get this error after reinstalling your Nvidia proprietary drivers, or switching from a version to another, [reinstall](/index.php/Reinstall "Reinstall") [lib32-nvidia-utils](https://www.archlinux.org/packages/?name=lib32-nvidia-utils) and [lib32-nvidia-libgl](https://www.archlinux.org/packages/?name=lib32-nvidia-libgl).

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