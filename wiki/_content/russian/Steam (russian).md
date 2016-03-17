Из [Wikipedia](https://en.wikipedia.org/wiki/Steam_(software) "wikipedia:Steam (software)"):

[Steam](http://store.steampowered.com/about/) — сервис цифрового распространения компьютерных игр и программ, принадлежащий компании Valve, известному разработчику компьютерных игр. Steam выполняет функции службы активации, загрузки через интернет, автоматических обновлений и новостей для игр как самой Valve, так и сторонних разработчиков по соглашению с Valve, таких как Epic Games, THQ, 2K Games, Activision, Capcom, Codemasters, Eidos Interactive, 1С, GSC Game World, id Software, SEGA, Atari, Rockstar Games, Telltale Games, Ubisoft, Bethesda Softworks и многих других фирм, оформивших контракт на дистрибьюцию.

## Contents

*   [1 Установка](#.D0.A3.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B0)
*   [2 Запуск Steam](#.D0.97.D0.B0.D0.BF.D1.83.D1.81.D0.BA_Steam)
    *   [2.1 Режим Big Picture (из Display Manager)](#.D0.A0.D0.B5.D0.B6.D0.B8.D0.BC_Big_Picture_.28.D0.B8.D0.B7_Display_Manager.29)
    *   [2.2 Запуск Steam свернутым в области уведомлений (silent mode)](#.D0.97.D0.B0.D0.BF.D1.83.D1.81.D0.BA_Steam_.D1.81.D0.B2.D0.B5.D1.80.D0.BD.D1.83.D1.82.D1.8B.D0.BC_.D0.B2_.D0.BE.D0.B1.D0.BB.D0.B0.D1.81.D1.82.D0.B8_.D1.83.D0.B2.D0.B5.D0.B4.D0.BE.D0.BC.D0.BB.D0.B5.D0.BD.D0.B8.D0.B9_.28silent_mode.29)
*   [3 Советы и приёмы](#.D0.A1.D0.BE.D0.B2.D0.B5.D1.82.D1.8B_.D0.B8_.D0.BF.D1.80.D0.B8.D1.91.D0.BC.D1.8B)
    *   [3.1 Запуск игр с дополнительными параметрами, такими как Bumblebee/Primus](#.D0.97.D0.B0.D0.BF.D1.83.D1.81.D0.BA_.D0.B8.D0.B3.D1.80_.D1.81_.D0.B4.D0.BE.D0.BF.D0.BE.D0.BB.D0.BD.D0.B8.D1.82.D0.B5.D0.BB.D1.8C.D0.BD.D1.8B.D0.BC.D0.B8_.D0.BF.D0.B0.D1.80.D0.B0.D0.BC.D0.B5.D1.82.D1.80.D0.B0.D0.BC.D0.B8.2C_.D1.82.D0.B0.D0.BA.D0.B8.D0.BC.D0.B8_.D0.BA.D0.B0.D0.BA_Bumblebee.2FPrimus)
    *   [3.2 Отключение отдельных композиторов при запуске игр](#.D0.9E.D1.82.D0.BA.D0.BB.D1.8E.D1.87.D0.B5.D0.BD.D0.B8.D0.B5_.D0.BE.D1.82.D0.B4.D0.B5.D0.BB.D1.8C.D0.BD.D1.8B.D1.85_.D0.BA.D0.BE.D0.BC.D0.BF.D0.BE.D0.B7.D0.B8.D1.82.D0.BE.D1.80.D0.BE.D0.B2_.D0.BF.D1.80.D0.B8_.D0.B7.D0.B0.D0.BF.D1.83.D1.81.D0.BA.D0.B5_.D0.B8.D0.B3.D1.80)
    *   [3.3 Using native runtime](#Using_native_runtime)
    *   [3.4 Skins for Steam](#Skins_for_Steam)
        *   [3.4.1 Steam skin manager](#Steam_skin_manager)
    *   [3.5 Changing the Steam friends notification placement](#Changing_the_Steam_friends_notification_placement)
        *   [3.5.1 Use a skin](#Use_a_skin)
        *   [3.5.2 On The fly patch](#On_The_fly_patch)
*   [4 Устранение неполадок](#.D0.A3.D1.81.D1.82.D1.80.D0.B0.D0.BD.D0.B5.D0.BD.D0.B8.D0.B5_.D0.BD.D0.B5.D0.BF.D0.BE.D0.BB.D0.B0.D0.B4.D0.BE.D0.BA)
*   [5 Смотрите также](#.D0.A1.D0.BC.D0.BE.D1.82.D1.80.D0.B8.D1.82.D0.B5_.D1.82.D0.B0.D0.BA.D0.B6.D0.B5)

## Установка

**Примечание:**

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

## Советы и приёмы

### Запуск игр с дополнительными параметрами, такими как Bumblebee/Primus

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

### Using native runtime

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

### Skins for Steam

**Note:** Using skins that are not up-to-date with the version of the Steam client may cause visual errors.

The Steam interface can be fully customized by copying its various interface files in its skins directory and modifying them.

An extensive list of skins can be found on [Steam's forums](http://forums.steampowered.com/forums/showthread.php?t=1161035).

#### Steam skin manager

The process of applying a skin to Steam can be greatly simplified using [steam-skin-manager](https://aur.archlinux.org/packages/steam-skin-manager/). The package also comes with a hacked version of the Steam launcher which allows the window manager to draw its borders on the Steam window.

As a result, skins for Steam will come in two flavors, one with and one without window buttons. The skin manager will prompt you whether you use the hacked version or not, and will automatically apply the theme corresponding to your GTK+ theme if it is found. You can of course still apply another skin if you want.

The package ships with two themes for the default Ubuntu themes, Ambiance and Radiance.

### Changing the Steam friends notification placement

**Note:** A handful of games do not support this, for example this can not work with XCOM: Enemy Unknown.

#### Use a skin

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

#### On The fly patch

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

## Устранение неполадок

Смотрите [Steam/Устранение неполадок](/index.php/Steam/Troubleshooting_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Steam/Troubleshooting (Русский)").

## Смотрите также

*   [https://wiki.gentoo.org/wiki/Steam](https://wiki.gentoo.org/wiki/Steam)