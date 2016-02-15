오픈박스는 가볍고 설정을 자유롭게 할 수 있으며 광범위한 표준을 지원하는 [윈도 매니저](/index.php/Window_manager "Window manager")이다. 오픈박스 [공식 웹사이트](http://openbox.org/)에 그 기능들이 설명되어 있다. 이 문서는 아치 리눅스에서 오픈박스를 설치하는 것에 대한 것이다.

## Contents

*   [1 설치](#.EC.84.A4.EC.B9.98)
*   [2 오픈박스 3.5 버전으로 업그레이드하기](#.EC.98.A4.ED.94.88.EB.B0.95.EC.8A.A4_3.5_.EB.B2.84.EC.A0.84.EC.9C.BC.EB.A1.9C_.EC.97.85.EA.B7.B8.EB.A0.88.EC.9D.B4.EB.93.9C.ED.95.98.EA.B8.B0)
*   [3 단독 WM로 오픈박스 사용](#.EB.8B.A8.EB.8F.85_WM.EB.A1.9C_.EC.98.A4.ED.94.88.EB.B0.95.EC.8A.A4_.EC.82.AC.EC.9A.A9)
*   [4 데스크톱 환경용 윈도매니저로 오픈박스 사용하기](#.EB.8D.B0.EC.8A.A4.ED.81.AC.ED.86.B1_.ED.99.98.EA.B2.BD.EC.9A.A9_.EC.9C.88.EB.8F.84.EB.A7.A4.EB.8B.88.EC.A0.80.EB.A1.9C_.EC.98.A4.ED.94.88.EB.B0.95.EC.8A.A4_.EC.82.AC.EC.9A.A9.ED.95.98.EA.B8.B0)
    *   [4.1 GNOME 2.24와 2.26](#GNOME_2.24.EC.99.80_2.26)
    *   [4.2 GNOME 2.26 redux](#GNOME_2.26_redux)
    *   [4.3 GNOME 2.22와 그 이전](#GNOME_2.22.EC.99.80_.EA.B7.B8_.EC.9D.B4.EC.A0.84)
    *   [4.4 KDE](#KDE)
    *   [4.5 Xfce4](#Xfce4)
*   [5 Openbox for multihead users](#Openbox_for_multihead_users)
*   [6 Configuration](#Configuration)
    *   [6.1 Manual configuration](#Manual_configuration)
    *   [6.2 ObConf](#ObConf)
    *   [6.3 Application customization](#Application_customization)
*   [7 Menus](#Menus)
    *   [7.1 Manual configuration of menus](#Manual_configuration_of_menus)
    *   [7.2 Icons in menu](#Icons_in_menu)
    *   [7.3 MenuMaker](#MenuMaker)
    *   [7.4 Obmenu](#Obmenu)
        *   [7.4.1 Obm-xdg](#Obm-xdg)
    *   [7.5 XDG-menu](#XDG-menu)
    *   [7.6 openbox-menu](#openbox-menu)
    *   [7.7 Python-based xdg menu script](#Python-based_xdg_menu_script)
    *   [7.8 Openbox menu generator](#Openbox_menu_generator)
    *   [7.9 Pipe menus](#Pipe_menus)
*   [8 Startup programs](#Startup_programs)
    *   [8.1 Enabling autostart](#Enabling_autostart)
    *   [8.2 Autostart script](#Autostart_script)
    *   [8.3 Autostart directory](#Autostart_directory)
*   [9 Themes and appearance](#Themes_and_appearance)
    *   [9.1 Openbox themes](#Openbox_themes)
    *   [9.2 Cursors, icons, wallpaper](#Cursors.2C_icons.2C_wallpaper)
*   [10 Recommended programs](#Recommended_programs)
*   [11 Tips and tricks](#Tips_and_tricks)
    *   [11.1 Aero snap behaviour](#Aero_snap_behaviour)
    *   [11.2 File associations](#File_associations)
    *   [11.3 Copy and paste](#Copy_and_paste)
    *   [11.4 Window transparency](#Window_transparency)
    *   [11.5 Xprop values for applications](#Xprop_values_for_applications)
        *   [11.5.1 Xprop for Firefox](#Xprop_for_Firefox)
    *   [11.6 Linking the menu to a button](#Linking_the_menu_to_a_button)
    *   [11.7 Urxvt in the background](#Urxvt_in_the_background)
        *   [11.7.1 ToggleShowDesktop exception](#ToggleShowDesktop_exception)
    *   [11.8 Keyboard volume control](#Keyboard_volume_control)
        *   [11.8.1 ALSA](#ALSA)
        *   [11.8.2 Pulseaudio](#Pulseaudio)
*   [12 Troubleshooting Openbox 3.5](#Troubleshooting_Openbox_3.5)
    *   [12.1 X server crashes](#X_server_crashes)
    *   [12.2 Autostarting unwanted applications in 3.5](#Autostarting_unwanted_applications_in_3.5)
    *   [12.3 SSH agent no longer starting](#SSH_agent_no_longer_starting)
*   [13 See also](#See_also)

## 설치

[공식 저장소](/index.php/Official_repositories "Official repositories")에 있는 [오픈박스](https://www.archlinux.org/packages/?name=%EC%98%A4%ED%94%88%EB%B0%95%EC%8A%A4)를 설치한다. 그 다음에 기본 설정 파일인 `rc.xml`, `menu.xml`, `autostart` 및 `environment`를 `~/.config/openbox`로 복사한다.

**참고:** 루트 권한이 없는 일반 사용자로 이것을 실행한다.

```
$ mkdir -p ~/.config/openbox
$ cp /etc/xdg/openbox/{rc.xml,menu.xml,autostart,environment} ~/.config/openbox

```

다음 파일 네 개가 오픈박스를 기본적으로 설정한다. 각 파일은 특정한 부분을 설정하는데 각 파일에 대한 설명은 다음과 같다.

	`rc.xml`

	이 파일이 기본 설정 파일이다. 키보드 단축키, 테마, 가상 데스크톱 등을 설정한다.

	`menu.xml`

	이 파일은 마우스 오르쪽 클릭 메뉴를 설정한다. 프로그램 실행기와 기타 빠른 실행을 설정한다. [#Menus](#Menus) 부분을 참고하라.

	`autostart`

	오픈박스 실행 시에 openbox-session이 읽어 들인다. 오픈박스 실행 시에 시작하는 프로그램을 포함한다. 보통 환경 변수를 설정하거나 패널/독을 실행하거나 바탕화면을 설정하거나 시작 스크립트를 실행하는 데에 사용된다. [오픈박스 위키](http://openbox.org/wiki/Help:Autostart)를 참고하라.

	`environment`

	오픈박스 실행 시에 openbox-session이 읽어 들인다. 오픈박스에서 설정될 환경 변수를 포함한다. 여기에 설정된 어떤 변수라도 오픈박스와 오픈박스 메뉴에서 실행하는 모두에 적용될 것이다.

## 오픈박스 3.5 버전으로 업그레이드하기

오픈박스 3.5이상으로 업그레이드하려면 다음을 유의하세요.

*   `environment`라는 새로운 설정 파일이 있는데 `/etc/xdg/openbox`에서 `~/.config/openbox`로 복사해야 합니다.
*   이전에 `autostart.sh`라는 설정 파일은 지금 `autostart`이다. 이전 파일이 있다면 파일 이름 뒤에 `.sh`를 제거하라.
*   `rc.xml` 파일에서 설정 구문 일부가 바뀌었다. 오픈박스가 옛 설정을 인식하는 것처럼 보일지라도 `/etc/xdg/openbox`에 있는 파일과 비교해서 영향을 받을 수 있는 변경 사항을 검토하는 것이 좋다. 

## 단독 WM로 오픈박스 사용

오픈박스는 단독으로 사용할 수 있는 윈도 매니저(WM)이다. 이는 데스크톱 환경과 함께 사용할 때보다 설치하고 설정하기가 더 간단하다. 오픈박스를 단독으로 사용하기 때문에 CPU와 메모리 부하를 줄일 수 있다. 오픈박스를 단독으로 실행하려면 다음을 `~/.xinitrc`에 추가하라.

```
exec openbox-session

```

명령 쉘(텍스트 프롬프트)에서 `xinit`를 사용해 실행할 수도 있다.

```
$ xinit /usr/bin/openbox-session

```

Xfwm과 같은 윈도 매니저를 이전에 사용했고 지금 로그아웃해서 오픈박스를 시작할 수 없다면 autostart 폴더를 삭제해보라.

```
mv ~/.config/autostart ~/.config/autostart.bak

```

**참고:** 오픈박스 xdg-autostart를 사용하려면 [python2-xdg](https://www.archlinux.org/packages/?name=python2-xdg)가 필요하다.

## 데스크톱 환경용 윈도매니저로 오픈박스 사용하기

오픈박스는 완전한 데스크톱 환경용 윈도 매니저로 사용할 수 있다. 오픈박스를 사용하는 방법은 데스크톱 환경에 따라 다르다.

### GNOME 2.24와 2.26

다음의 내용으로 `/usr/share/applications/openbox.desktop` 파일을 생성하라.

```
[Desktop Entry]
Type=Application
Encoding=UTF-8
Name=OpenBox
Exec=openbox
NoDisplay=true
# 로드할 수 있는 컨트롤 센터 모듈 이름
X-GNOME-WMSettingsModule=openbox
#  WM 확인 창 이름
X-GNOME-WMName=OpenBox

```

gconf에서 `/desktop/gnome/session/required_components/windowmanager`를 `openbox`로 설정하라.

```
$ gconftool-2 -s -t string /desktop/gnome/session/required_components/windowmanager openbox

```

마지막으로 GDM 세션 선택 메뉴에서 `GNOME` 세션을 선택하라.

### GNOME 2.26 redux

_**앞의 GNOME 2.24 용 안내가 효과가 없을 경우**_

"Gnome/Openbox" 세션으로 로그인하려하지만 계속해서 시작하지 못하면 다음을 시도해보라. 이 방법은 Gnome 세션을 시작할 때 WM로 오픈박스를 사용하는 한 가지 방법이다.

1.  Gnome-only 세션(윈도 매니저로 메타시티를 사용할 경우)으로 로그인하라.
2.  오픈박스를 아직 설치하지 않았다면 설치하라.
3.  메뉴에서 _System → Preferences → Startup Applications_ ( Gnome 옛 버전에서는 'Session'이라고 함) 순으로 찾아 가라.
4.  Startup Application을 열어서 '+ Add'를 선택한 후에 다음의 글을 입력하라. # 뒤의 글은 생략하라.
5.  'Add' 버튼을 클릭해 데이터 입력 창을 연다. 새로 입력하는 항목 옆의 체크박스를 선택했는지 확인하라.
6.  Gnome 세션에서 로그아웃하고 다시 로그인하라.
7.  지금 오픈박스를 윈도 매니저로 실행하고 있어야 한다.

```
Name:    Openbox Windox Manager          # 변경 가능
Command: openbox --replace               # 이 줄은 필수 입력 사항이며 뒤에 덧붙일 수 있음
Comment: Replaces metacity with openbox  # 변경 가능

```

이는 시작 항목을 생성하며 사용자 세션이 시작할 때마다 Gnome이 실행한다.

### GNOME 2.22와 그 이전

1.  GDM을 사용한다면 "GNOME/Openbox" 로그인 옵션을 선택하라.
2.  `startx`를 사용한다면 `exec openbox-gnome-session`를 `~/.xinitrc`에 추가하라.
3.  쉘에서 다음을 실행할 수도 있다.

```
$ xinit /usr/bin/openbox-gnome-session

```

### KDE

1.  KDM을 사용한다면 "KDE/Openbox" 로그인 옵션을 선택하라.
2.  System Settings > Default Applications (Workspace Appearance and Behaviour 부분)을 열어서 디폴트 윈도 매니저를 오픈박스(다시 로그인할 필요가 없음)로 변경하라.
3.  startx를 사용한다면 `exec openbox-kde-session`을 `~/.xinitrc`에 추가하라.
4.  쉘에서 다음을 실행할 수도 있다.

```
$ xinit /usr/bin/openbox-kde-session

```

### Xfce4

Log into a normal Xfce4 session. From your terminal, type:

```
$ killall xfwm4 ; openbox & exit

```

This kills xfwm4, runs Openbox, and closes the terminal. Log out, being sure to check the _"Save session for future logins"_ box. On your next login, Xfce4 should use **Openbox** as its window manager.

Alternatively, you can chooose _Settings_ -> _Session and Startup_ from menu, go to the _Application Autostart_ tab and add `openbox --replace` to the list of automatically started applications.

To enable exiting from a session using _xfce4-session_, edit `~/.config/openbox/menu.xml`. If the file is not there, copy it from `/etc/xdg/openbox/`. Look for the following entry:

```
 <item label="Exit Openbox">
   <action name="Exit">
     <prompt>yes</prompt>
   </action>
 </item>

```

Change it to:

```
 <item label="Exit Openbox">
   <action name="Execute">
     <prompt>yes</prompt>
    <command>xfce4-session-logout</command>
   </action>
 </item>

```

Otherwise, choosing "Exit" from the root-menu causes Openbox to terminate its execution, leaving you with no window manager.

If you have a problem changing virtual desktops with the mouse wheel skipping over desktops, edit `~/.config/openbox/rc.xml`. Move the _mouse binds with..._ actions "DesktopPrevious" and "DesktopNext" from context _Desktop_ to the context _Root_. Note that you may need to create a definition for the _Root_ context as well.

When using the Openbox root-menu instead of Xfce's menu, you may exit the Xfdesktop with this terminal command:

```
$ xfdesktop --quit

```

Xfdesktop manages the wallpaper and desktop icons, requiring you to use other utilities such as ROX for these functions.

(When terminating Xfdesktop, the above issue with the virtual desktops is no longer a problem.)

## Openbox for multihead users

While Openbox provides better than average multihead support on its own, a branch called [Openbox Multihead](https://aur.archlinux.org/packages.php?ID=51460) is now available in the AUR that gives multihead users per-monitor desktops. This model is not commonly found in floating window managers, but exists mainly in tiling window managers. It is explained well on the [Xmonad web site](http://xmonad.org/tour.html#workspace). Also, please see [README.MULTIHEAD](https://github.com/BurntSushi/openbox-multihead/blob/multihead/README.MULTIHEAD) for a more comprehensive description of the new features and configuration options found in Openbox Multihead.

Openbox Multihead will function like normal Openbox when only a single head is available.

A downside to using Openbox Multihead is that it breaks the EWMH assumption that one and only one desktop is visible at any time. Thus, existing pagers will not work well with it. To remedy this, [pager-multihead](https://aur.archlinux.org/packages.php?ID=51536) can be found in the AUR that is compatible with Openbox Multihead. [Screenshots](http://imgur.com/a/cnZeq#y04nk).

Finally, a new version of [pytyle](https://aur.archlinux.org/packages.php?ID=51626) can also be found in the AUR that will work with Openbox Multihead.

Both pytyle3 and pager-multihead will work without Openbox Multihead if only one monitor is active.

## Configuration

There are several options for configuring Openbox settings:

### Manual configuration

To configure Openbox manually, edit the `~/.config/openbox/rc.xml` file with a text editor. The file has explanatory comments throughout. See the [Help:Configuration openbox wiki](http://openbox.org/wiki/Help:Configuration) for more documentation on editing this file.

### ObConf

[ObConf](http://openbox.org/wiki/ObConf:About) is an Openbox configuration tool. It is used to set most common preferences such as themes, virtual desktops, window properties, and desktop margins. It can be installed with pacman:

```
# pacman -S obconf

```

ObConf cannot configure keyboard shortcuts and certain other features. For these features edit `rc.xml` manually. Alternatively, you can try [obkey](https://aur.archlinux.org/packages/obkey/) from the [AUR](/index.php/AUR "AUR").

### Application customization

Openbox allows per-application customizations. This lets you define rules for a given program. For example:

*   Start your web browser on a specific virtual desktop.
*   Open your terminal program with no window decorations (window chrome).
*   Make your bit-torrent client open at a given screen position.

Per-application settings are defined in `~/.config/openbox/rc.xml`. Instructions are in the file's comments. More details are found in the [Help:Applications openbox wiki](http://openbox.org/wiki/Help:Applications).

## Menus

The default Openbox menu includes a variety of menu items to get you started. Many of these items launch applications you do not want, have not installed yet, or never intend to install. You will surely want to customize **`menu.xml`** at some point. There are a number of ways to do so.

### Manual configuration of menus

You can edit `~/.config/openbox/menu.xml` with a text editor. Many of the settings are self-explanatory. The article [Help:Menus](http://openbox.org/wiki/Help:Menus) has extensive details.

### Icons in menu

Since version 3.5.0 you can have icons next to your menu entries. To do that :

1.  add <showIcons>yes</showIcons> in the <menu> section of the `rc.xml` file
2.  edit the menu entries in `menu.xml` and add icons="<path>" like this :

```
<menu id="apps-menu" label="SomeApp" icon="/home/user/.icons/application.png">

```

then openbox --reconfigure or openbox --restart if you have troubles updating the menu :)

### MenuMaker

[MenuMaker](http://menumaker.sourceforge.net/) creates XML menus for several window managers including Openbox. MenuMaker searchs your computer for executable programs and creates a menu file from the result. It can be configured to exclude certain application types (GNOME, KDE, etc) if you desire.

```
# pacman -S menumaker    #  Install MenuMaker from the repository

```

Once installed, generate a menu file (named `menu.xml`) by running the program.

```
$ mmaker -v OpenBox3     #  Will not overwrite an existing menu file.
$ mmaker -vf OpenBox3    #  Force option permits overwriting the menu file.
$ mmaker --help          #  See the full set of options for MenuMaker.

```

MenuMaker creates a comprehensive `menu.xml`. You may edit this file by hand or regenerate it after installing software.

### Obmenu

Obmenu is a menu editor for Openbox. This GUI application is the best choice for those who dislike editing XML code. Obmenu is available in the community repository:

```
# pacman -S obmenu

```

Once installed, run `obmenu` then add and remove applications as desired.

#### Obm-xdg

`obm-xdg` is a command-line tool that comes with Obmenu. It generates a categorized sub-menu of installed GTK/GNOME applications.

To use obm-xdg with other menus, add the following line to `~/.config/openbox/menu.xml`:

```
<menu execute="obm-xdg" id="xdg-menu" label="xdg"/>

```

Then add the following line under your 'root-menu' entry where you want to have the menu appear:

```
<menu id="xdg-menu"/>

```

Then run `openbox --reconfigure` to refresh the Openbox menu. You should now see a sub-menu labeled **xdg** in your menu.

To use obm-xdg by itself, create `~/.config/openbox/menu.xml` and add these lines:

```
<openbox_menu>
 <menu execute="obm-xdg" id="root-menu" label="apps"/>
</openbox_menu>

```

**Note:** If you do not have GNOME installed, you need to install the package [gnome-menus](https://www.archlinux.org/packages/?name=gnome-menus) for obm-xdg.

### XDG-menu

[community] 저장소에 있는 [archlinux-xdg-menu](https://www.archlinux.org/packages/?name=archlinux-xdg-menu) 꾸러미는 XDG 파일을 사용해 오픈박스용 메뉴를 자동으로 생성한다. 사용 방법은 [여기](/index.php/Xdg-menu#OpenBox "Xdg-menu")를 참고하라.

### openbox-menu

Openbox-menu는 LXDE 프로젝트에서 만든 [menu-cache](http://sourceforge.net/projects/lxde/files/menu-cache/)를 사용해 오픈박스용 동적 메뉴를 만든다.

프로젝트 홈페이지: [http://mimasgpc.free.fr/openbox-menu_en.html](http://mimasgpc.free.fr/openbox-menu_en.html)

AUR 꾸러미: [[1]](https://aur.archlinux.org/packages.php?ID=31605)

### Python-based xdg menu script

This script is found in Fedora's Openbox package. You have only to put the script somewhere and create a menu entry.

Here is the head: [latest script](http://pkgs.fedoraproject.org/gitweb/?p=openbox.git;f=xdg-menu;hb=HEAD)

Download from the above repository. Place the file into the directory you want.

Open `menu.xml` with your text editor and add the following entry. Of course, you can modify the label as you see fit.

```
<menu id="apps-menu" label="xdg-menu" execute="python2 <path>/xdg-menu"/>

```

Save the file and run `openbox --reconfigure`.

**Note:** If you do not have GNOME installed, you need to install the package [gnome-menus](https://www.archlinux.org/packages/?name=gnome-menus) for xdg-menu.

### Openbox menu generator

Residing in the AUR as [obmenugen-bin,](https://aur.archlinux.org/packages.php?ID=27300) Openbox menu generator creates the menu file from *.desktop files. Obmenugen provides a text file which filters (hides) menu items using basic regex.

```
$ obmenugen               # Create a menu file
$ openbox --reconfigure   # To see the menu you generated

```

### Pipe menus

Like other window managers, Openbox allows for scripts to dynamically build menus (menus on-the-fly). Examples are system monitors, media player controls, or weather monitors. Pipe menu script examples are found in the [Openbox:Pipemenus](http://openbox.org/wiki/Openbox:Pipemenus) page at Openbox's site.

User _Xyne_ created a pipe menu file browser and user _brisbin33_ created a pipe menu for scanning and connecting to wireless hot spots (using netcfg). Forum posts for these utilities are here: [file browser](https://bbs.archlinux.org/viewtopic.php?id=77197&p=1) and here: [wifi](https://bbs.archlinux.org/viewtopic.php?id=78290).

User _jnguyen_ created a pipe menu for managing removable devices using Udisks. The forum post is here: [obdevicemenu](https://bbs.archlinux.org/viewtopic.php?id=114702).

## Startup programs

Openbox supports running programs at startup. This is provided by command **openbox-session**.

### Enabling autostart

There are two ways to enable autostart:

1.  When using startx or xinit to begin a session, edit `~/.xinitrc`. Change the line that executes _**openbox**_ to **openbox-session**.
2.  When using GDM or KDM, selecting an _Openbox_ session automatically runs the autostart script.

### Autostart script

Openbox provides a system-wide startup script which applies to all users and is located at `/etc/xdg/openbox/autostart`. A user may also create his own startup script to be executed after the system-wide script by creating the file `~/.config/openbox/autostart`. This file is not provided by default and must be created by the user.

Further instructions are available in the [Help:Autostart](http://openbox.org/wiki/Help:Autostart) article at the official Openbox site.

**Note:** The autostart files used to be named autostart.sh prior to OpenBox 3.5.0\. While these scripts will presently still work, users who are upgrading are advised to drop the .sh extension.

### Autostart directory

Openbox also starts any *.desktop files in `/etc/xdg/autostart` - this happens regardless of whether a user startup script is present. `nm-applet`, for example, installs a file at this location, and may cause it to run twice for users with the usual `(sleep 3 && /usr/bin/nm-applet --sm-disable) &` in their startup script. There is a discussion on managing the effects of this at [[2]](https://bbs.archlinux.org/viewtopic.php?pid=993738).

## Themes and appearance

The supplemental article **[Openbox Themes and Apps](/index.php/Openbox_Themes_and_Apps "Openbox Themes and Apps")** has detailed information about changing Openbox's GUI.

### Openbox themes

Themes control the appearance of windows, titlebars, and buttons. They also control menu appearance and on-screen display (OSD). Additional themes are available from the standard repositories.

```
# pacman -S openbox-themes

```

### Cursors, icons, wallpaper

Please see [Openbox Themes and Apps](/index.php/Openbox_Themes_and_Apps#X11_Mouse_cursors "Openbox Themes and Apps") for information on these GUI customizations.

## Recommended programs

The supplemental wiki article **[Openbox Themes and Apps](/index.php/Openbox_Themes_and_Apps#Recommended_programs "Openbox Themes and Apps")** has information on applications you may use with Openbox. The article gives details about panels, trays, mixer controls, and other widgets used on a desktop interface.

There is a list of [Lightweight Applications](/index.php/Lightweight_Applications "Lightweight Applications") in the wiki. Most of these work nicely with Openbox.

## Tips and tricks

### Aero snap behaviour

Windows 7 supports a unique window behaviour to snap windows when they are moved to the edge of the screen. This effect can also be achieved through an Openbox keybinding. More information [here](http://ubuntuforums.org/showthread.php?t=1796793).

### File associations

Because Openbox and the applications you use with it are not well-integrated you might run into the issues with your browser. Your browser may not know which program it is supposed to use for certain types of files.

A package in the AUR called [gnome-defaults-list](https://aur.archlinux.org/packages.php?ID=23170) contains a list of file-types and programs specific to the Gnome desktop. The list is installed to `/etc/gnome/defaults.list.`

Open this file with your text-editor. Now you can replace a given application with the name of the program of your choosing. For example, totem <=> vlc or eog <=> mirage. Save the file to `~/.local/share/applications/defaults.list`.

Another way of setting file associations is to install package _perl-file-mimeinfo_ from the repository and invoke **mimeopen** like this:

```
mimeopen -d /path/to/file

```

You are asked which application to use when opening /path/to/file:

```
Please choose a default application for files of type text/plain
       1) notepad  (wine-extension-txt)
       2) Leafpad  (leafpad)
       3) OpenOffice.org Writer  (writer)
       4) gVim  (gvim)
       5) Other...

```

Your answer becomes the default handler for that type of file. Mimeopen is installed as `/usr/bin/perlbin/vendor/mimetype`.

### Copy and paste

From a terminal `Ctrl+Insert` for copy and `Shift+Insert` for paste.

Also `Ctrl+Shift+c` for copy and **mouse middle-click** for paste (in terminals).

Other applications most likely use the conventional keyboard shortcuts for copy and paste.

### Window transparency

The program transset-df (virtually the same as _transset_) is installed with pacman -S transset-df. With transset-df you can enable window-transparency on-the-fly.

For instance by placing the following in `~/.config/openbox/rc.xml` you can have your mouse adjust window transparency by scrolling while hovering over the title bar (it is in the <mouse> section):

```
    <context name="Titlebar">
     . . .
     <mousebind button="Up" action="Click">
       <action name= "Execute" >
       <execute>transset-df -p .2 --inc  </execute>
       </action>
     </mousebind>
     <mousebind button="Down" action="Click">
       <action name= "Execute" >
       <execute>transset-df -p .2 --dec </execute>
       </action>
     </mousebind>
     . . .
   </context>

```

It appears to work only when no additional actions are defined within the action group.

### Xprop values for applications

If you use per-application settings frequently, you might find this bash alias handy:

```
alias xp='xprop | grep "WM_WINDOW_ROLE\|WM_CLASS" && echo "WM_CLASS(STRING) = \"NAME\", \"CLASS\""'

```

To use, run **`xp`** and click on the running program that you would like to define with per-app settings. The result displays only the info that Openbox requires, namely the WM_WINDOW_ROLE and WM_CLASS (name and class) values:

```
[thayer@dublin:~] $ xp
WM_WINDOW_ROLE(STRING) = "roster"
WM_CLASS(STRING) = "gajim.py", "Gajim.py"
WM_CLASS(STRING) = "NAME", "CLASS"

```

#### Xprop for Firefox

For whatever reason, Firefox and like-minded equivalents ignore application rules (e.g. <desktop>) unless `class="Firefox*"` is used. This applies irrespective of whatever values xprop may report for the program's WM_CLASS.

### Linking the menu to a button

Some people want to link the Openbox menu (or any menu) to an object. This is useful for creating a panel button to pop up a menu. Although Openbox does not provide this, a program called **xdotool** (available in community repo) simulates a keypress. Openbox can be configured to bind that keypress to the _ShowMenu_ action.

After installing _xdotool_, add the following to the <keyboard> section of your **`rc.xml`**:

```
 <keybind key="A-C-q">
   <action name="ShowMenu">
     <menu>root-menu</menu>
   </action>
 </keybind>

```

Restart/reconfigure Openbox. The following command summons a menu at your cursor position. The command may given as-is, linked to an object, or placed in a script.

```
$ xdotool key ctrl+alt+q

```

Of course, change the key shortcut to your liking. Here is a snippet from a **tint2** (a taskbar-like panel) configuration file which pops up a menu when the clock area is clicked. Each key combination is set to open a menu within openbox's **`rc.xml`** configuration file. The right‑click menu is different from the left‑click menu:

```
clock_rclick_command = xdotool key --clearmodifiers "ctrl+XF86PowerOff"
clock_lclick_command = xdotool key --clearmodifiers "alt+XF86PowerOff"

```

### Urxvt in the background

With Openbox, running a terminal as desktop background is easy. You will not need **devilspie** here.

First you must enable transparency, open your `.Xdefaults` file (if it does not exist yet, create it in your home folder).

```
URxvt*transparent:true
URxvt*scrollBar:false
URxvt*geometry:124x24    #I do not use the whole screen, if you want a full screen term do not bother with this and see below.
URxvt*borderLess:true
URxvt*foreground:Black   #Font color. My wallpaper is White, you may wish to change this to White.

```

Then edit your `.config/openbox/rc.xml` file:

```
<application name="urxvt">
  <decor>no</decor>
  <focus>yes</focus>
  <position>
    <x>center</x>
    <y>20</y>
  </position>
  <layer>below</layer>
  <desktop>all</desktop>
  <maximized>true</maximized> #Only if you want a full size terminal.
</application>

```

The _magic_ comes from the `<layer>below</layer>` line, which place the application under all others. Here Urxvt is displayed on all desktops, change it to your convenience.

Note: Instead of using <application name="URxvt">, you can use another name ("URxvt-bg" for example), and use the -name option when starting uxrvt. That way, only the urxvt terminals which you choose to name URxvt-bg would be captured and modified by the application rule in rc.xml. For example: urxvt -name URxvt-bg (case sensitive)

#### ToggleShowDesktop exception

~~Above method still minimizes Urxvt when using the ToggleShowDesktop command. A method for avoiding this is explained in this [forum post](https://bbs.archlinux.org/viewtopic.php?pid=865844#p865844). This involves editing Urxvt's source code.~~

**Note:** This method seems to have been broken in a recent update, now leading to a memory leak when the patched Urxvt is run.

The only working method at the moment seems to be the one outlined [here](https://bbs.archlinux.org/viewtopic.php?pid=929792#p929792). This makes ToggleShowDesktop a one-way action, not restoring the other desktop applications when ToggleShowDesktop is run for a second time. It also creates the opportunity to use a different terminal emulator than Urxvt, however.

### Keyboard volume control

#### ALSA

If you use ALSA for sound, you can use the amixer program to adjust the volume of sound. You can use Openbox's keybindings to act like multimedia keys. (Alternatively, you can probably find out the names of your real multimedia keys and map them.) For example, in the <keyboard> section of rc.xml:

```
   <keybind key="W-Up">
     <action name="Execute">
       <command>amixer set Master 5%+</command>
     </action>
   </keybind>

```

This binds Windows key + Up arrow to increase your master ALSA volume by 5%. Corresponding binding for volume down:

```
   <keybind key="W-Down">
     <action name="Execute">
       <command>amixer set Master 5%-</command>
     </action>
   </keybind>

```

As another example you can also use the XF86Audio keybindings:

```
   <keybind key="XF86AudioRaiseVolume">
     <action name="Execute">
       <command>amixer set Master 5%+ unmute</command>
     </action>
   </keybind>
   <keybind key="XF86AudioLowerVolume">
     <action name="Execute">
       <command>amixer set Master 5%- unmute</command>
     </action>
   </keybind>
   <keybind key="XF86AudioMute">
     <action name="Execute">
       <command>amixer set Master toggle</command>
     </action>
   </keybind>

```

The above example should work for the majority of multimedia keyboards. It should enable to raise, lower and mute the Master control of your audio device by using the respective multimedia keyboard keys. Notice also that in this example:

*   The "Mute" key should unmute the Master control if it is already in mute mode.
*   The "Raise" and "Lower" keys should unmute the Master control if it is in mute mode.

#### Pulseaudio

If you are using pulseaudio with ALSA as a backend the above keybinding are slightly different as amixer must be told to use pulse.

```
  <keybind key="XF86AudioRaiseVolume">
     <action name="Execute">
       <command>amixer -D pulse set Master 5%+ unmute</command>
     </action>
   </keybind>
   <keybind key="XF86AudioLowerVolume">
     <action name="Execute">
       <command>amixer -D pulse set Master 5%- unmute</command>
     </action>
   </keybind>
   <keybind key="XF86AudioMute">
     <action name="Execute">
       <command>amixer set Master toggle</command>
     </action>
   </keybind>

```

This keybindings should work for most of the systems. Other examples can be found [here](http://ubuntuforums.org/showthread.php?t=987149).

## Troubleshooting Openbox 3.5

### X server crashes

Problems have been detected after upgrade to ver. 3.5, that the X server might crash in attempt to start openbox, ending with similar error message:

```
(metacity:25137): GLib-WARNING **: In call to g_spawn_sync(), exit status of a child process \
                   was requested but SIGCHLD action was set to SIG_IGN and ECHILD was received by waitpid(), so exit \
                   status can't be returned. This is a bug in the program calling g_spawn_sync(); either do not request \
                   the exit status, or do not set the SIGCHLD action.
xinit: connection to X server lost
waiting for X server to shut down

```

In this particular case, some problem with metacity package has been identified as the cause of the X server crash issue. Removal of metacity & compiz-decorator-gtk packages solved the problem. Though, later was found, that even a simple reinstall of packages might have helped, as there is no problem after new installation of previously removed packages.

Also, plenty of similar cases have been found on the Internet, that not only metacity package might be causing the X server to crash. Thus, whatever else instead of metacity you get in the error output message, try to reinstall it (or remove if necessary) in an attempt to get rid of this X server crash.

### Autostarting unwanted applications in 3.5

Unwanted applications do start with your Openbox session, though they are not listed in your `~/.config/openbox/autostart` script?

Check the `~/.config/autostart/` directory, it might contain the residues from your previously used desktop environment (GNOME, KDE, etc.), and remove unwanted files.

### SSH agent no longer starting

Whereas Openbox 3.4.x allowed launching an SSH agent from `$XDG_CONFIG_HOME/openbox/autostart{,.sh}`, with 3.5 that no longer seems to work. You need to put your code in `$XDG_CONFIG_HOME/openbox/environment`, e.g.:

```
SSHAGENT="/usr/bin/ssh-agent"
SSHAGENTARGS="-s"
if [ -z "$SSH_AUTH_SOCK" -a -x "$SSHAGENT" ]; then
        eval `$SSHAGENT $SSHAGENTARGS`
        trap "kill $SSH_AGENT_PID" 0
fi

```

## See also

*   [Openbox Website](http://openbox.org/) — The official website
*   [Planet Openbox](http://planetob.openmonkey.com/) – Openbox news portal
*   [Box-Look.org](http://www.box-look.org/) – A good resource for themes and related artwork
*   [Openbox Hacks and Configs Thread](https://bbs.archlinux.org/viewtopic.php?id=93126) @ Arch Linux Forums
*   [Openbox Screenshots Thread](https://bbs.archlinux.org/viewtopic.php?id=45692) @ Arch Linux Forums
*   [Installation and configuration tutorial](http://snott.net/linux/using-gnome3-with-openbox/) Using gnome3 with Openbox