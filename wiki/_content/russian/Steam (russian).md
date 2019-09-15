Related articles

*   [Steam/Wine](/index.php/Steam/Wine "Steam/Wine")
*   [Steam/Устранение_неполадок](/index.php/Steam/%D0%A3%D1%81%D1%82%D1%80%D0%B0%D0%BD%D0%B5%D0%BD%D0%B8%D0%B5_%D0%BD%D0%B5%D0%BF%D0%BE%D0%BB%D0%B0%D0%B4%D0%BE%D0%BA "Steam/Устранение неполадок")
*   [Steam/Game-specific troubleshooting](/index.php/Steam/Game-specific_troubleshooting "Steam/Game-specific troubleshooting")

Из [Wikipedia](https://en.wikipedia.org/wiki/Steam_(software) "wikipedia:Steam (software)"):

[Steam](http://store.steampowered.com/about/) — сервис цифрового распространения компьютерных игр и программ, принадлежащий компании Valve, известному разработчику компьютерных игр. Steam выполняет функции службы активации, загрузки через интернет, автоматических обновлений и новостей для игр как самой Valve, так и сторонних разработчиков по соглашению с Valve, таких как Epic Games, THQ, 2K Games, Activision, Capcom, Codemasters, Eidos Interactive, 1С, GSC Game World, id Software, SEGA, Atari, Rockstar Games, Telltale Games, Ubisoft, Bethesda Softworks и многих других фирм, оформивших контракт на дистрибьюцию.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Установка](#Установка)
*   [2 Запуск Steam](#Запуск_Steam)
    *   [2.1 Режим Big Picture (из Display Manager)](#Режим_Big_Picture_(из_Display_Manager))
    *   [2.2 Запуск Steam свернутым в области уведомлений (silent mode)](#Запуск_Steam_свернутым_в_области_уведомлений_(silent_mode))
    *   [2.3 Headless In-Home Streaming Server](#Headless_In-Home_Streaming_Server)
*   [3 Советы и приёмы](#Советы_и_приёмы)
    *   [3.1 Запуск игр с дополнительными параметрами](#Запуск_игр_с_дополнительными_параметрами)
    *   [3.2 Отключение отдельных композиторов при запуске игр](#Отключение_отдельных_композиторов_при_запуске_игр)
    *   [3.3 Using native runtime](#Using_native_runtime)
    *   [3.4 Оформление для Steam](#Оформление_для_Steam)
        *   [3.4.1 Менеджер тем Steam](#Менеджер_тем_Steam)
    *   [3.5 Changing the Steam friends notification placement](#Changing_the_Steam_friends_notification_placement)
        *   [3.5.1 Use a skin](#Use_a_skin)
        *   [3.5.2 On-the-fly patch](#On-the-fly_patch)
    *   [3.6 Предотвращение дампов памяти потребляющих RAM](#Предотвращение_дампов_памяти_потребляющих_RAM)
*   [4 Устранение неполадок](#Устранение_неполадок)
*   [5 Смотрите также](#Смотрите_также)

## Установка

**Примечание:**

*   Arch Linux **не** имеет [официальной поддержки](https://support.steampowered.com/kb_article.php?ref=1504-QHXN-8366).
*   Поскольку клиент Steam является 32-битным приложением, вам необходимо включить [multilib](/index.php/Multilib_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Multilib (Русский)") репозиторий, если у вас 64-битная система. Также может понадобиться установить [multilib-devel](https://www.archlinux.org/groups/x86_64/multilib-devel/), чтобы предоставить некоторые важные multilib библиотеки.

Steam можно установить с помощью пакета [steam](https://www.archlinux.org/packages/?name=steam), доступного в [официальных репозиториях](/index.php/Official_repositories_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Official repositories (Русский)"). Если у вас 64-битная система, сначала включите репозиторий [multilib](/index.php/Multilib_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Multilib (Русский)").

Steam не сопровождается для этого дистрибутива. Поэтому пользователям придётся самим исправить некоторые недочёты в работе:

*   Steam интенсивно использует шрифт Arial. Для замены шрифта Arial воспользуйтесьпакетом [ttf-liberation](https://www.archlinux.org/packages/?name=ttf-liberation) или [шрифтами, предоставленными Steam'ом](#Текст_повреждён_или_не_отображается). Чтобы корректно отображались азиатские языки, установите [wqy-zenhei](https://www.archlinux.org/packages/?name=wqy-zenhei).

*   Если у вас 64-битная система, вы должны установить [32-битную версию графического драйвера](/index.php/Xorg_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#Установка "Xorg (Русский)") (пакет из столбца *Multilib* в таблице), чтобы запускать 32-битные игры.

*   Если у вас 64-битная система, вам нужно установить [lib32-alsa-plugins](https://www.archlinux.org/packages/?name=lib32-alsa-plugins), чтобы работал звук в 32-битных играх.

*   Если у вас 64-битная система, вам нужно установить [lib32-curl](https://www.archlinux.org/packages/?name=lib32-curl), чтобы обновится при первом запуске.

*   Некоторые игры имеют зависимости, которые не установлены в вашей системе. Если игра вылетает при запуске, (часто даже без сообщения об ошибке), тогда убедитесь, что вы установили все библиотеки, перечисленные в [Steam/Game-specific troubleshooting](/index.php/Steam/Game-specific_troubleshooting "Steam/Game-specific troubleshooting").

## Запуск Steam

### Режим Big Picture (из Display Manager)

Чтобы запустить Steam в режиме Big Picture из менеджера дисплеев (таких как LightDM), создайте файл `/usr/share/xsessions/steam-big-picture.desktop` со следующим содержимым:

 `/usr/share/xsessions/steam-big-picture.desktop` 
```
[Desktop Entry]
Name=Steam Big Picture Mode
Comment=Start Steam in Big Picture Mode
Exec=/usr/bin/steam -bigpicture
TryExec=/usr/bin/steam
Icon=
Type=Application
```

Также это можно сделать из Steam > Настройки > Интерфейс, отметьте галочкой 'Запускать Steam в режиме Big Picture' и запускайте Steam обычным образом. С некоторыми оконными менеджерами такой способ работает лучше, чем вариант с командной строкой.

### Запуск Steam свернутым в области уведомлений (silent mode)

Если при старте появляется главное окно Steam, вы можете добавить параметр `-silent` к команде запуска, чтобы окно не отображалось:

```
/usr/bin/steam -silent %U

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

### Headless In-Home Streaming Server

To setup a Headless In-Home Streaming Server follow the Guide at: [https://steamcommunity.com/sharedfiles/filedetails/?id=680514371](https://steamcommunity.com/sharedfiles/filedetails/?id=680514371)

## Советы и приёмы

### Запуск игр с дополнительными параметрами

Steam может запускать игры, используя ваши собственные команды. Чтобы это сделать, перейдите в вашу Библиотеку игр, щёлкните правой кнопкой мыши по нужной игре, выбирете Свойства, Установить параметры запуска. Steam заменит тег `%command%` на команду, на ту, которую он выполнит по факту. Например, чтобы запустить Team Fortress 2 с primusrun и разрешением 1920x1080, вы должны ввести:

```
primusrun %command% -w 1920 -h 1080

```

В некоторых случаях optirun даёт большую производительность, чем primusrun, однако, некоторые игры могут крашиться сразу после запуска. Это можно исправить предзагрузкой правильной версии libGL. Используйте:

```
locate libGL

```

что-бы узнать доступные варианты. Для 64-битных игр вы, возможно, захотите предзагрузить 64-битную версию libGL, для этого используйте команду запуска:

```
LD_PRELOAD=/usr/lib/nvidia/libGL.so optirun %command%

```

Если вы используете ядро [Linux-ck](/index.php/Linux-ck "Linux-ck"), вы можете уменьшить задержки и увеличить производительность, запустив игру в SCHED_ISO (низкие задержки, избежание перегрузки CPU) с помощью [schedtool](https://www.archlinux.org/packages/?name=schedtool)

```
# schedtool -I -e %command% *other arguments*

```

Также, стоит помнить, что Steam [на самом деле не волнует](http://i.imgur.com/oJcLDBi.png), что именно вы хотите запустить. Изменяя `%command%` на переменную окружения, вы можете заставить Steam запускать то, что вы хотите. К примеру, вот опции запуска, которые использовались на картинке выше:

```
IGNORE_ME=%command% glxgears

```

### Отключение отдельных композиторов при запуске игр

В дополнение к этому, используйте `%command%` для того, чтобы убивать отдельные композиторы, (такие как Xcompmgr или [Compton](/index.php/Compton_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Compton (Русский)")), из-за которых игра может глючить и тормозить на некоторых системах, и запускать их снова после выхода из игры, добавив в опции запуска игры следующее:

```
 killall compton && %command%; nohup compton &

```

Замените `compton` в приведённой выше команде на ваш композитор. Вы также можете добавить -options к `%command%` или `compton`.

Steam будет родительским процессом для любой команды, написанной после `%command%` и ваш Steam статус будет отображаться как "в игре". Поэтому, в этом примере мы используем композитор через `nohup`, таким образом он не будет привязан к процессу Steam (и будет продолжать работать после закрытия Steam), а завершение команды амперсандом сбросит ваш статус Steam.

### Using native runtime

Steam, by default, ships with a copy of every library it uses, packaged within itself, so that games can launch without issue. This can be a resource hog, and the slightly out-of-date libraries they package may be missing important features (Notably, the OpenAL version they ship lacks [HRTF](/index.php/Gaming#Binaural_Audio_with_OpenAL "Gaming") and surround71 support). To use your own system libraries, you can run Steam with:

```
$ STEAM_RUNTIME=0 steam

```

However, if you are missing any libraries Steam makes use of, this will fail to launch properly. An easy way to find the missing libraries is to run the following commands:

```
$ cd ~/.local/share/Steam/ubuntu12_32
$ LD_LIBRARY_PATH=".:${LD_LIBRARY_PATH}" ldd $(file *|sed '/ELF/!d;s/:.*//g')|grep 'not found'|sort|uniq

```

**Note:** The libraries will have to be 32-bit, which means you may have to download some from the AUR if on x86_64, such as NetworkManager.

Once you have done this, run steam again with `STEAM_RUNTIME=0 steam` and verify it is not loading anything outside of the handful of steam support libraries:

```
$ for i in $(pgrep steam); do sed '/\.local/!d;s/.*  //g' /proc/$i/maps; done | sort | uniq

```

To launch Steam using native runtime in a graphical user environment you can add the [environment variable](/index.php/Environment_variable "Environment variable") to your [xprofile](/index.php/Xprofile "Xprofile") file:

 `~/.xprofile` 
```
export STEAM_RUNTIME=0

```

If you create or edit this file while in a desktop session you will need to log out and then back into your [desktop environment](/index.php/Desktop_environment "Desktop environment") to enable the change to take effect.

**Backing out the using native runtime in a graphical environment change**

To reverse this change remove or comment out the export line in your [xprofile](/index.php/Xprofile "Xprofile") file. Log out and then in again to refresh your desktop session. When launched, Steam will use the old bundled Ubuntu libraries.

**Convenience repository**

The unofficial [alucryd-multilib](/index.php/Unofficial_user_repositories#alucryd-multilib "Unofficial user repositories") repository contains all libraries needed to run native steam on x86_64\. Please note that, for some reason, steam does not pick up sdl2 or libav* even if you have them installed. It will still use the ones it ships with.

All you need to install is the meta-package [steam-libs](https://aur.archlinux.org/packages/steam-libs/), it will pull all the libs for you. Please report if there is any missing library, the maintainer already had some lib32 packages installed so a library may have been overlooked.

**Satisfying dependencies without using the convenience repository or steam-libs meta-package (For x86_64)**

If you do not like the approach of installing all the libraries known for Steam and various game-compatibility libraries and want to install the minimum required libraries to launch Steam and most games install the following libraries:

Steam on x86_64 requires the following libraries from [AUR](/index.php/AUR "AUR") to be installed [lib32-gconf](https://www.archlinux.org/packages/?name=lib32-gconf) [lib32-dbus-glib](https://www.archlinux.org/packages/?name=lib32-dbus-glib) [lib32-libnm-glib](https://www.archlinux.org/packages/?name=lib32-libnm-glib) and [lib32-libudev0](https://aur.archlinux.org/packages/lib32-libudev0/).

It will also require the following libraries from the [multilib](/index.php/Multilib "Multilib") repository [lib32-openal](https://www.archlinux.org/packages/?name=lib32-openal) [lib32-nss](https://www.archlinux.org/packages/?name=lib32-nss) [lib32-gtk2](https://www.archlinux.org/packages/?name=lib32-gtk2) and [lib32-gtk3](https://www.archlinux.org/packages/?name=lib32-gtk3).

If Steam displays errors related to libcanberra-gtk3 install [lib32-libcanberra](https://www.archlinux.org/packages/?name=lib32-libcanberra).

While most games will run with the minimal set of libraries listed here some games will require additional libraries to run. For a list of known game-compatibility libraries consult the [game-specific troubleshooting](/index.php/Steam/Game-specific_troubleshooting "Steam/Game-specific troubleshooting") page.

### Оформление для Steam

**Note:** Использование устаревших скинов Steam может привести к визуальными/графическим ошибкам.

Графический интерфейс Steam может быть полностью кастомизирован, достаточно скопировать файлы тем в их директорию и изменить.

Большой список тем можно найти на [форуме Steam](http://forums.steampowered.com/forums/showthread.php?t=1161035).

#### Менеджер тем Steam

Смена различных тем может быть упрощена установкой пакета [steam-skin-manager](https://aur.archlinux.org/packages/steam-skin-manager/). Пакет идёт вместе с изменённым Steam-лаунчером, позволяющим оконным менеджерам отрисовывать границы окна на клиенте Steam.

Как результат, темы для Steam идут двух видов - с кнопками окна и без них. Менеджер тем предупредит вас, используете ли вы изменённую версию клиента и автоматически применит соответствующую тему GTK+. Вы так же можете использовать другую тему, если захотите.

Пакет распространяется с двумя Ubuntu-темами по умолчанию - Ambiance и Radiance.

### Changing the Steam friends notification placement

**Note:** A handful of games do not support this, for example this can not work with XCOM: Enemy Unknown.

#### Use a skin

You can create a skin that does nothing but change the notification corner. First you need to create the directories:

```
 $ mkdir -p $HOME/Top-Right/resource
 $ cp -R $HOME/.steam/steam/resource/styles $HOME/Top-Right/resource/
 $ mv $HOME/Top-Right $HOME/.local/share/Steam/skins/
 $ cd .local/share/Steam/skins/
 $ cp -R Top-Right Top-Left && cp -R Top-Right Bottom-Right

```

Then modify the correct files. `Top-Right/resource/styles/gameoverlay.style` will change the corner for the in-game overlay whereas `steam.style` will change it for your desktop.

Now find the entry: `Notifications.PanelPosition` in whichever file you opened and change it to the appropriate value, for example for Top-Right:

```
 Notifications.PanelPosition     "TopRight"

```

This line will look the same in both files. Repeat the process for all the 3 variants (`Top-Right`, `Top-Left` and `Bottom-Left`) and adjust the corners for the desktop and in-game overlay to your satisfaction for each skin, then save the files.

To finish you will have to select the skin in Steam: *Settings > Interface* and *<default skin>* in the drop-down menu.

You can use these files across distributions and even between Windows and Linux (OS X has its own entry for the desktop notification placement)

#### On-the-fly patch

This method is more compatible with future updates of Steams since the files in the skins above are updated as part of steam and as such if the original files change, the skin will not follow the graphics update to steam and will have to be re-created every time something like that happens. Doing things this way will also give you the ability to use per-game notification locations as you can run a patch changing the location of the notifications by specifying it in the launch options for games.

Steam updates the files we need to edit everytime it updates (which is everytime it is launched) so the most effective way to do this is patching the file after Steam has already been launched.

First you will need a patch:

 `$HOME/.steam/topright.patch` 
```
--- A/steam/resource/styles/gameoverlay.styles	2013-06-14 23:49:36.000000000 +0000
+++ B/steam/resource/styles/gameoverlay.styles	2014-07-08 23:13:15.255806000 +0000
@@ -7,7 +7,7 @@
 		mostly_black "0 0 0 240"
 		semi_black "0 0 0 128"
 		semi_gray "32 32 32 220"
-		Notifications.PanelPosition     "BottomRight"
+		Notifications.PanelPosition     "TopRight"
 	}

 	styles

```

**Note:** The patch file should have all above lines, including the newline at the end.

You can edit the entry and change it between "BottomRight"(default), "TopRight" "TopLeft" and "BottomLeft": the following will assume you used "TopRight" as in the original file.

Next create an alias in `$HOME/.bashrc`:

```
 alias steam_topright='pushd $HOME/.steam/ && patch -p1 -f -r - --no-backup-if-mismatch < topright.patch && popd'

```

Log out and back in to refresh the aliases. Launch Steam and wait for it to fully load, then run the alias

```
 $ steam_topright

```

And most games you launch after this will have their notification in the upper right corner.

You can also duplicate the patch and make more aliases for the other corners if you do not want all games to use the same corner so you can switch back.

To automate the process you will need a script file as steam launch options cannot read your aliases. The location and name of the file could for example be **$HOME/.scripts/steam_topright.sh**, and assuming that is the path you used, it needs to be executable:

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
 $HOME/.scripts/steam_topright.sh && %command%

```

There is another file in the same folder as **gameoverlay.style** folder called **steam.style** which has an entry with the exact same function as the file we patched and will change the notification corner for the desktop only (not in-game), but for editing this file to actually work it has to be set before steam is launched and the folder set to read-only so steam cannot re-write the file. Therefore the only two ways to modify that file is to make the directory read only so steam cannot change it when it is launched (can break updates) or making a skin like in method 1.

### Предотвращение дампов памяти потребляющих RAM

Каждый раз, когда steam крашится, он записывает дамп памяти в **/tmp/dumps/**. Если Steam часто падает в циклическую ошибку, то дамп-файлы могут потреблять значительное количество места. Поскольку **/tmp** в Arch примонтирован как tmpfs, память и swap файл будут потребляться без необходимости. Что-бы предотвратить это, вы можете создать символическую ссылку в **/dev/null** или создать и изменить права доступа **/tmp/dumps**. После этого Steam не сможет записывать дампы в эту директорию. Это также заставит Steam не выгружать дампы на сервера Valve.

```
# ln -s /dev/null /tmp/dumps

```

или

```
# mkdir /tmp/dumps
# chmod 600 /tmp/dumps

```

## Устранение неполадок

Смотрите [Steam/Устранение неполадок](/index.php/Steam/Troubleshooting_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Steam/Troubleshooting (Русский)").

## Смотрите также

*   [https://wiki.gentoo.org/wiki/Steam](https://wiki.gentoo.org/wiki/Steam)