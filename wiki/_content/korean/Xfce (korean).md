[Xfce](http://www.xfce.org)는 현재 GTK+ 2를 기반으로 하는 모듈식의 저용량 [데스크탑 환경](/index.php/Desktop_environment "Desktop environment")이다. 완벽한 사용자 경험을 제공하기 위해 Xfce는 창 관리자, 파일 관리자, 데스크탑과 패널을 포함한다.

## Contents

*   [1 설치하기](#.EC.84.A4.EC.B9.98.ED.95.98.EA.B8.B0)
*   [2 Xfce 시작하기](#Xfce_.EC.8B.9C.EC.9E.91.ED.95.98.EA.B8.B0)
*   [3 설정하기](#.EC.84.A4.EC.A0.95.ED.95.98.EA.B8.B0)
    *   [3.1 메뉴](#.EB.A9.94.EB.89.B4)
        *   [3.1.1 Whisker 메뉴](#Whisker_.EB.A9.94.EB.89.B4)
        *   [3.1.2 메뉴 편집](#.EB.A9.94.EB.89.B4_.ED.8E.B8.EC.A7.91)
    *   [3.2 바탕화면](#.EB.B0.94.ED.83.95.ED.99.94.EB.A9.B4)
        *   [3.2.1 투명한 아이콘 제목 배경색](#.ED.88.AC.EB.AA.85.ED.95.9C_.EC.95.84.EC.9D.B4.EC.BD.98_.EC.A0.9C.EB.AA.A9_.EB.B0.B0.EA.B2.BD.EC.83.89)
        *   [3.2.2 오른쪽 마우스 클릭 메뉴에서 Thunar 옵션 제거](#.EC.98.A4.EB.A5.B8.EC.AA.BD_.EB.A7.88.EC.9A.B0.EC.8A.A4_.ED.81.B4.EB.A6.AD_.EB.A9.94.EB.89.B4.EC.97.90.EC.84.9C_Thunar_.EC.98.B5.EC.85.98_.EC.A0.9C.EA.B1.B0)
        *   [3.2.3 프로그램 강제 종료 단축키](#.ED.94.84.EB.A1.9C.EA.B7.B8.EB.9E.A8_.EA.B0.95.EC.A0.9C_.EC.A2.85.EB.A3.8C_.EB.8B.A8.EC.B6.95.ED.82.A4)
    *   [3.3 세션](#.EC.84.B8.EC.85.98)
        *   [3.3.1 시작 프로그램](#.EC.8B.9C.EC.9E.91_.ED.94.84.EB.A1.9C.EA.B7.B8.EB.9E.A8)
            *   [3.3.1.1 시작 프로그램 지연 설정](#.EC.8B.9C.EC.9E.91_.ED.94.84.EB.A1.9C.EA.B7.B8.EB.9E.A8_.EC.A7.80.EC.97.B0_.EC.84.A4.EC.A0.95)
        *   [3.3.2 화면 잠금](#.ED.99.94.EB.A9.B4_.EC.9E.A0.EA.B8.88)
        *   [3.3.3 사용자 전환 버튼](#.EC.82.AC.EC.9A.A9.EC.9E.90_.EC.A0.84.ED.99.98_.EB.B2.84.ED.8A.BC)
        *   [3.3.4 저장된 세션 비활성화하기](#.EC.A0.80.EC.9E.A5.EB.90.9C_.EC.84.B8.EC.85.98_.EB.B9.84.ED.99.9C.EC.84.B1.ED.99.94.ED.95.98.EA.B8.B0)
        *   [3.3.5 기본 창 관리자](#.EA.B8.B0.EB.B3.B8_.EC.B0.BD_.EA.B4.80.EB.A6.AC.EC.9E.90)
    *   [3.4 Theming](#Theming)
    *   [3.5 Sound](#Sound)
        *   [3.5.1 Xfce4 mixer](#Xfce4_mixer)
            *   [3.5.1.1 Change default sound card in Xfce4 mixer](#Change_default_sound_card_in_Xfce4_mixer)
        *   [3.5.2 Keyboard volume buttons](#Keyboard_volume_buttons)
            *   [3.5.2.1 Shortcuts](#Shortcuts)
    *   [3.6 Keyboard Shortcuts](#Keyboard_Shortcuts)
    *   [3.7 Polkit Authentication Agent](#Polkit_Authentication_Agent)
    *   [3.8 Display blanking](#Display_blanking)
*   [4 Tips and tricks](#Tips_and_tricks)
    *   [4.1 Hide partitions from thunar and xfdesktop](#Hide_partitions_from_thunar_and_xfdesktop)
    *   [4.2 Screenshots](#Screenshots)
    *   [4.3 Disable Terminal F1 and F11 shortcuts](#Disable_Terminal_F1_and_F11_shortcuts)
    *   [4.4 Terminal color themes or palettes](#Terminal_color_themes_or_palettes)
        *   [4.4.1 Changing default color theme](#Changing_default_color_theme)
        *   [4.4.2 Terminal tango color theme](#Terminal_tango_color_theme)
    *   [4.5 Colour management](#Colour_management)
    *   [4.6 Multiple monitors](#Multiple_monitors)
    *   [4.7 SSH agents](#SSH_agents)
    *   [4.8 Scroll a background window without shifting focus on it](#Scroll_a_background_window_without_shifting_focus_on_it)
    *   [4.9 Mouse button modifier](#Mouse_button_modifier)
*   [5 Troubleshooting](#Troubleshooting)
    *   [5.1 Action buttons are missing icons](#Action_buttons_are_missing_icons)
    *   [5.2 Desktop icons rearrange themselves](#Desktop_icons_rearrange_themselves)
    *   [5.3 GTK themes not working with multiple monitors](#GTK_themes_not_working_with_multiple_monitors)
    *   [5.4 Icons do not appear in right-click menus](#Icons_do_not_appear_in_right-click_menus)
    *   [5.5 Keyboard settings are not saved in xkb-plugin](#Keyboard_settings_are_not_saved_in_xkb-plugin)
    *   [5.6 NVIDIA and xfce4-sensors-plugin](#NVIDIA_and_xfce4-sensors-plugin)
    *   [5.7 Panel applets keep being aligned on the left](#Panel_applets_keep_being_aligned_on_the_left)
    *   [5.8 Preferred Applications preferences have no effect](#Preferred_Applications_preferences_have_no_effect)
    *   [5.9 Restore default settings](#Restore_default_settings)
    *   [5.10 Session failure](#Session_failure)
    *   [5.11 Fonts in window title crashing xfce4-title](#Fonts_in_window_title_crashing_xfce4-title)
    *   [5.12 Laptop lid settings ignored](#Laptop_lid_settings_ignored)
    *   [5.13 Rendering issues with Adwaita theme](#Rendering_issues_with_Adwaita_theme)
*   [6 See also](#See_also)

## 설치하기

[xfce4](https://www.archlinux.org/groups/x86_64/xfce4/) 그룹을 [설치](/index.php/Install "Install")한다. 추가 플러그인과 [mousepad](https://www.archlinux.org/packages/?name=mousepad) 편집기와 같은 유용한 유틸리티를 설치하고자 하는 경우 [xfce4-goodies](https://www.archlinux.org/groups/x86_64/xfce4-goodies/) 그룹으로 설치할 수 있다. Xfce는 [Xfwm](/index.php/Xfwm "Xfwm")을 기본 창 관리자로 사용한다.

## Xfce 시작하기

[display manager](/index.php/Display_manager "Display manager")의 선택 메뉴에서 *Xfce Session* 을 선택하거나 [Xinitrc](/index.php/Xinitrc "Xinitrc")에 `exec startxfce4`를 추가한다.

**참고:** `xfce4-session`을 직접 실행하지 않는다. `startxfce4`의 호출이 올바른 실행법이며 해당 명령어에서 단계적으로 `xfce4-session`을 적절한 시기에 호출한다.

## 설정하기

Xfce는 설정 옵션들을 [Xfconf](http://docs.xfce.org/xfce/xfconf/start)에 저장한다. 해당 옵션들을 설정하는 방법에는 다음과 같은 몇 가지 방법들이 있다.

*   메인 메뉴에서 설정([Settings](http://docs.xfce.org/xfce/xfce4-settings/start))을 클릭하고 설정하고자 하는 카테고리를 클릭한다. 카테고리들은 대부분 `/usr/bin/xfce4-*`와 `/usr/bin/xfdesktop-settings`에 위치한 프로그램들이다.
*   `xfce4-settings-editor`을 통해 수정가능한 설정을 확인할 수 있다. 여기서 수정된 사항들은 곧바로 적용된다. `xfconf-query`를 사용하여 커맨드라인에서 설정을 변경할 수도 있다. 자세한 사항은 [the documentation](http://docs.xfce.org/xfce/xfconf/xfconf-query)을 참고하기 바란다.
*   설정은 `~/.config/xfce4/xfconf/xfce-perchannel-xml/` 에 XML 파일로 저장되며 해당 파일은 직접적으로 수정될 수 있다. 하지만 변경된 사항은 *곧바로 적용되지 않는다*.

### 메뉴

#### Whisker 메뉴

[xfce4-whiskermenu-plugin](https://www.archlinux.org/packages/?name=xfce4-whiskermenu-plugin) is an alternate application launcher. It shows a list of favorites, browses through all installed applications through category buttons, and supports fuzzy searching. [xfce4-whiskermenu-plugin](https://www.archlinux.org/packages/?name=xfce4-whiskermenu-plugin) 는 xfce의 또다른 어플리케이션 런처이다. 즐겨찾기 목록을 보여주고, 카테고리 버튼을 통해 설치된 프로그램을 탐색할 수 있으며 퍼지 검색을 지원한다.

#### 메뉴 편집

메뉴를 편집하기 위해서 다음과 같은 그래픽 인터페이스 기반의 툴들을 사용할 수 있다:

*   **XAME** — Xfce 메뉴 편집용으로 디자인 된 Gambas 기반의 GUI 툴. 오직 Xfce에서만 사용가능하며 다른 Desktop Environment에서는 작동하지 않는다.

	[http://www.redsquirrel87.com/XAME.html](http://www.redsquirrel87.com/XAME.html) || [xame](https://aur.archlinux.org/packages/xame/)

*   **MenuLibre** — 깔끔하고 사용하기 쉬운 인터페이스로 최신 기능을 제공하는 고급 메뉴 편집기

	[https://launchpad.net/menulibre](https://launchpad.net/menulibre) || [menulibre](https://aur.archlinux.org/packages/menulibre/).

*   **Alacarte** — GNOME용 메뉴 편집기

	[http://www.gnome.org/](http://www.gnome.org/) || [alacarte](https://www.archlinux.org/packages/?name=alacarte)

다른 방법으로, `~/.config/menus/xfce-applications.menu` 파일을 직접 만들어 메뉴를 관리할 수 있다. 다음의 예제를 참고한다.

```
<!DOCTYPE Menu PUBLIC "-//freedesktop//DTD Menu 1.0//EN"
  "[http://www.freedesktop.org/standards/menu-spec/1.0/menu.dtd](http://www.freedesktop.org/standards/menu-spec/1.0/menu.dtd)">

```

```
<Menu>
    <Name>Xfce</Name>
    <MergeFile type="parent">/etc/xdg/menus/xfce-applications.menu</MergeFile>

```

```
    <Exclude>
        <Filename>xfce4-run.desktop</Filename>
        <Filename>exo-terminal-emulator.desktop</Filename>
        <Filename>exo-file-manager.desktop</Filename>
        <Filename>exo-mail-reader.desktop</Filename>
        <Filename>exo-web-browser.desktop</Filename>
        <Filename>xfce4-about.desktop</Filename>
        <Filename>xfhelp4.desktop</Filename>
    </Exclude>

```

```
    <Layout>
        <Merge type="all"/>
        <Separator/>
        <Menuname>Settings</Menuname>
        <Separator/>
        <Filename>xfce4-session-logout.desktop</Filename>
    </Layout>
</Menu>

```

`<MergeFile>` 태그는 기본 Xfce 메뉴를 포함한다.

`<Exclude>` 태그는 메뉴로부터 태그 안의 어플리케이션을 제외시킨다. 예제에서는 Xfce의 기본 바로가기만을 제외시켰지만 `firefox.desktop` 혹은 다른 어플리케이션도 제외시킬 수 있다.

`<Layout>` 태그는 메뉴의 레이아웃을 정의한다. 어플리케이션들은 폴더 내 혹은 사용자가 원하는 곳에 배치될 수 있다. 자세한 정보는 [Xfce wiki](http://wiki.xfce.org/howto/customize-menu)를 참고한다.

추가적으로 `.desktop` 파일들을 수정하여 Xfce 메뉴를 변경할 수도 있다. 메뉴 엔트리를 숨기기 위해서는 [Desktop entries#Hide desktop entries](/index.php/Desktop_entries#Hide_desktop_entries "Desktop entries")를 참고한다. `Categories=` desktop entry를 수정하여 어플리케이션의 카테고리도 변경이 가능하다. 관련 내용은 [Desktop entries#File example](/index.php/Desktop_entries#File_example "Desktop entries")을 참고한다.

### 바탕화면

#### 투명한 아이콘 제목 배경색

바탕화면에 있는 아이콘 이름 부분의 기본 하얀색 배경을 좀 더 배경과 어울리게 바꾸기 위해서, `~/.gtkrc-2.0` 파일을 생성하거나 편집한다:

```
style "xfdesktop-icon-view" {
    XfdesktopIconView::label-alpha = 10
    base[NORMAL] = "#000000"
    base[SELECTED] = "#71B9FF"
    base[ACTIVE] = "#71B9FF"
    fg[NORMAL] = "#fcfcfc"
    fg[SELECTED] = "#ffffff"
    fg[ACTIVE] = "#ffffff"
}
widget_class "*XfdesktopIconView*" style "xfdesktop-icon-view"

```

#### 오른쪽 마우스 클릭 메뉴에서 Thunar 옵션 제거

다음 명령어를 실행한다.

```
$ xfconf-query -c xfce4-desktop -v --create -p /desktop-icons/style -t int -s 0

```

#### 프로그램 강제 종료 단축키

Xfce에서는 프로그램이 멈추었을 때 강제 종료하기 위한 기본 단축키가 없다. 하지만 [xorg-xkill](https://www.archlinux.org/packages/?name=xorg-xkill) 패키지의 `xkill` 명령어를 사용하여 열려있는 창을 강제로 닫을 수 있다. 현재 활성화 상태의 창이라면(현재 창이 열려 있고 포커스를 가지고 있는 경우), [xdotool](https://www.archlinux.org/packages/?name=xdotool)를 사용하여 활성화 상태의 창을 강제종료할 수 있다.

```
$ xdotool getwindowfocus windowkill

```

또 다른 방법으로, 다음 명령어을 사용할 수 있다.

```
$ xkill -id "$(xprop -root -notype | sed -n '/^_NET_ACTIVE_WINDOW/ s/^.*# *\|\,.*$//g p')"

```

단축키를 추가하기 위해서는 *Settings > Keyboard* 혹은 [xbindkeys](https://www.archlinux.org/packages/?name=xbindkeys) 어플리케이션을 사용한다.

### 세션

#### 시작 프로그램

사용자정의 프로그램을 Xfce 시작시에 실행되도록 하기 위해서는 *Applications Menu > Settings > Settings Manager*의 *Session and Startup > Application Autostart* 탭을 확인한다. 해당 탭을 통해 시작 시에 실행되는 프로그램 리스트를 확인할 수 있다. 시작프로그램을 추가하기 위해서는 *Add* 버튼을 클릭하고 등록하고자 하는 실행파일의 경로를 정의한다.

또 다른 방법으로, [xinitrc](/index.php/Xinitrc "Xinitrc") ([display manager](/index.php/Display_manager "Display manager")가 사용되고 있는 경우에는 [xprofile](/index.php/Xprofile "Xprofile"))에 명령어를 추가하여 시작 프로그램을 등록할 수 있다.

##### 시작 프로그램 지연 설정

가끔, 시작프로그램의 시작을 늦추는 것이 유용할 때가 있다. 이러한 경우, *Application Autostart* 에서 `sleep 3 && command`와 같이 등록한 것은 동작하지 않기 때문에 다음 명령어를 대신 사용한다.

```
sh -c "sleep 3 && command"

```

#### 화면 잠금

*xflock4*ᅟ을 통해 Xfce4 세션을 잠그기 위해서는 [xscreensaver](https://www.archlinux.org/packages/?name=xscreensaver), [gnome-screensaver](https://www.archlinux.org/packages/?name=gnome-screensaver), [slock](https://www.archlinux.org/packages/?name=slock), [xlockmore](https://www.archlinux.org/packages/?name=xlockmore) 중 하나는 설치되어 있어야 한다. 또는, 다음 명령어를 통해 잠금 명령어를 설정할 수도 있다.

```
$ xfconf-query -c xfce4-session -p /general/LockCommand -s "light-locker-command -l" --create -t string

```

만약 명령어를 업데이트하고 싶다면 다음과 같이 명령어를 새로 업데이트할 수 있다.

```
$ xfconf-query -c xfce4-session -p /general/LockCommand -s "light-locker-command -l"

```

화면 잠금 관련 프로그램은 [List of applications/Security#Screen lockers](/index.php/List_of_applications/Security#Screen_lockers "List of applications/Security")에서 확인할 수 있다.

**Tip:** [light-locker](https://www.archlinux.org/packages/?name=light-locker) 세션 잠금은 [xfce4-power-manager](https://www.archlinux.org/packages/?name=xfce4-power-manager)와 통합된다. 만약 light-locker가 설치되어 있다면, 전원관리설정(power manager settings)에 추가된 *Security* 탭과 *Security* 탭에 *Lock screen when system is going for sleep* 설정이 있는 것을 확인할 수 있다.

**Note:** The *xflock4* 스크립트는 포스팅[[1]](https://bbs.archlinux.org/viewtopic.php?id=189484)에서 언급된 것처럼 직접적으로 수정될 수 있다. 다만, 패키지 업그레이드로 수정된 사항이 덮어쓰기되는 것을 방지하기 위해서 xflock4를 `/usr/local/bin`에 복사하고 해당 경로가 `/usr/bin`보다 우선적으로 실행될 수 있도록 설정해야 한다. (환경변수 PATH에서 /usr/local/bin:/usr/bin 과 같은 순서로 될 수 있도록 한다.)

#### 사용자 전환 버튼

**Note:** GDM 없이 사용자 전환 버튼을 사용하기 위해서는 다음의 해결 방법이 필요하다:

*   LXDM - [LXDM#Simultaneous users and switching users](/index.php/LXDM#Simultaneous_users_and_switching_users "LXDM").
*   LightDM - [LightDM#User switching under Xfce4](/index.php/LightDM#User_switching_under_Xfce4 "LightDM").

Xfce4는 [LightDM](/index.php/LightDM "LightDM")과 [GDM](/index.php/GDM "GDM")과 같이 사용자 전환 기능을 가지고 있는 [Display manager](/index.php/Display_manager "Display manager")가 사용되고 있는 경우에 사용자 전환을 지원한다. 더 자세한 정보는 Display manager 관련 위키페이지를 참조하도록 한다. display manager가 설치되어 있고 올바르게 설정이 되어있다면 Xfce 패널의 사용자 전환 버튼을 통해 사용자 전환이 가능하다.

#### 저장된 세션 비활성화하기

유저마다 저장된 세션은 다음 명령어를 실행하여 비활성화될 수 있다.

```
$ xfconf-query -t bool -c xfce4-session -p /general/SaveOnExit -s false

```

명령어 실행 이후, *Applications* -> *Settings* -> *Session and Startup* -> *Sessions* 안의 *Clear saved sessions* 버튼을 클릭한다.

**Tip:** 만약 위의 명령어가 설정을 영구적으로 변경하지 않는다면 다음 명령어를 대신 사용한다: `xfconf-query -c xfce4-session -p /general/SaveOnExit -n -t bool -s false`

또 다른 방법으로, Xfce [kiosk mode](https://wiki.xfce.org/howto/kiosk_mode)가 사용될 수 있다. 세션을 비활성화하기 위해, `/etc/xdg/xfce4/kiosk/kioskrc` 을 만들거나 수정하고 다음을 추가한다.

```
[xfce4-session]
SaveSession=NONE

```

만일 kiosk 모드가 작동하지 않는다면 현재 사용자가 세션관련 디렉토리에 대해 read 권한만 갖고 있기 때문이다.

```
$ rm ~/.cache/sessions/* && chmod 500 ~/.cache/sessions

```

위의 명령어가 Xfce가 모든 관련 설정에 상관없이 세션이 저장되는 것을 방지할 것이다.

#### 기본 창 관리자

**Note:** 변경 사항을 적용하기 위해서는 저장된 세션을 지우고 처음 로그아웃시에 세션 저장 기능을 반드시 비활성화해야 한다. 창 관리자가 실행되면 세션 저장기능은 다시 활성화된다.

기본 창관리자를 명시하는 파일은 다음 위치에서 찾을 수 있다.

*   `~/.config/xfce4/xfconf/xfce-perchannel-xml/xfce4-session.xml` - 각 사용자 영역
*   `/etc/xdg/xfce4/xfconf/xfce-perchannel-xml/xfce4-session.xml` - 시스템 전역

기본 창 관리자는 *xfconf-query*를 사용하여 간단하게 설정될 수 있다.

```
$ xfconf-query -c xfce4-session -p /sessions/Failsafe/Client0_Command -t string -sa **wm_name**

```

만약 커맨드라인 옵션을 사용하여 창 관리자를 실행하고 싶을 경우, 다음 명령어들을 참고한다:

```
$ xfconf-query -c xfce4-session -p /sessions/Failsafe/Client0_Command -t string -t string -s **wm_name** -s **--wm-option**

```

더 많은 커맨드라인 옵션이 필요하다면, 간단하게 `-t string`와 `-s **--wm-option**` 인자들을 명령어에 추가한다.

시스템 전역적으로 기본 창 관리자를 변경하고 싶다면 위에서 명시된 파일을 직접 수정하여 *xfwm4*를 선호하는 창 관리자로 바꾸고 필요시에는 `<value type="string" value="**--wm-option**"/>` 라인을 extra command line 옵션으로 추가한다.

또한 `**wm_name** --replace` 를 자동시작되도록 하거나 `**wm_name** --replace &`가 터미널에서 시작되도록 하고 해당 세션이 저장되도록 하여 창 관리자를 변경할 수 있다. 하지만 이 방법은 실제로 기본 창관리자를 변경하지 않는다는 점에 주의하자. 만약 자동시작 기능을 사용한다면 저장된 세션 때문에 해당 창 관리자가 두 번 중복되어 실행될 수 있으므로 저장된 세션을 비활성화한다.

### Theming

XFCE themes are available at [xfce-look.org](http://www.xfce-look.org). *Xfwm* themes are stored in `/usr/share/themes/xfce4`, and set in *Settings > Window Manager*. [GTK+](/index.php/GTK%2B "GTK+") themes are set in *Settings > Appearance*.

To achieve a uniform look for all applications, see [Uniform look for Qt and GTK applications](/index.php/Uniform_look_for_Qt_and_GTK_applications "Uniform look for Qt and GTK applications").

See also [Cursor themes](/index.php/Cursor_themes "Cursor themes"), [Icons](/index.php/Icons "Icons"), and [Font configuration](/index.php/Font_configuration "Font configuration").

### Sound

#### Xfce4 mixer

**Note:** Xfce4 mixer and Xfce4 volumed are no longer being maintained upstream as they cannot be ported to GStreamer 1.0\. For more information, see the 4.12 [news post](http://www.xfce.org/about/news/?post=1425081600).

Xfce4 mixer, provided by [xfce4-mixer](https://www.archlinux.org/packages/?name=xfce4-mixer), is the GUI mixer app and panel plugin from the Xfce team. It is part of the xfce4 group. For [PulseAudio](/index.php/PulseAudio "PulseAudio") and [OSS](/index.php/OSS "OSS") support, you will need to install [gstreamer0.10-good-plugins](https://www.archlinux.org/packages/?name=gstreamer0.10-good-plugins) if it is not installed already.

You might need to change the default sound card for Xfce4 mixer to function correctly. For further details, such as how to set the default sound card, see [Advanced Linux Sound Architecture#Set the default sound card](/index.php/Advanced_Linux_Sound_Architecture#Set_the_default_sound_card "Advanced Linux Sound Architecture"). Alternatively you can use [PulseAudio](/index.php/PulseAudio "PulseAudio") together with [pavucontrol](https://www.archlinux.org/packages/?name=pavucontrol) or [OSS](/index.php/OSS "OSS"). For OSS, see [OSS#Applications that use GStreamer](/index.php/OSS#Applications_that_use_GStreamer "OSS").

If you did need to change the default soundcard, logout to ensure that the changes take effect.

##### Change default sound card in Xfce4 mixer

In some cases (when using [PulseAudio](/index.php/PulseAudio "PulseAudio") or [xfce4-volumed](https://aur.archlinux.org/packages/xfce4-volumed/) for instance) it might be necessary to change the default sound card in Xfce4 Mixer in order for volume control to work as expected. [[2]](http://grumbel.blogspot.co.uk/2011/10/fixing-volume-control-in-xfce4.html)

To change the default sound card, open *xfce4-settings-editor* and navigate to **xfce4-mixer** and check the entries under **sound-cards**. Locate the correct entry for the card you are using and then replace the values of **sound-card** and **active-card** with the entry. If you are using PulseAudio then the entry will likely be similar to the following: **PlaybackInternalAudioAnalogStereoPulseAudioMixer**. Then logout for the changes to take effect.

#### Keyboard volume buttons

If the [xfce4-mixer](https://www.archlinux.org/packages/?name=xfce4-mixer) package is version `4.10.0-3` or greater, then the mixer panel applet provides the ability to control the volume using the keyboard. However, volume notifications will not be shown. Alternatively, [xfce4-volumed](https://aur.archlinux.org/packages/xfce4-volumed/) maps volume keys to Xfce4 mixer, and displays notifications through Xfce4-notifyd. If you are using PulseAudio and you do not wish to use Xfce4 Mixer at all, install [xfce4-pulseaudio-plugin](https://aur.archlinux.org/packages/xfce4-pulseaudio-plugin/). This provides a panel applet which has support for keyboard volume control and volume notifications.

**Warning:** [xfce4-pulseaudio-plugin](https://aur.archlinux.org/packages/xfce4-pulseaudio-plugin/) might have high CPU usage (~5% on i7 Intel CPU).

For non desktop environment specific alternatives, see [List of applications#Volume managers](/index.php/List_of_applications#Volume_managers "List of applications").

##### Shortcuts

If you are not using an applet or daemon that controls the volume keys, you can map volume control commands to your volume keys manually using Xfce's keyboard settings. For the sound system you are using, see the sections linked to below for the appropriate commands.

*   ALSA: see [Advanced Linux Sound Architecture#Keyboard volume control](/index.php/Advanced_Linux_Sound_Architecture#Keyboard_volume_control "Advanced Linux Sound Architecture").
*   PulseAudio: see [PulseAudio#Keyboard volume control](/index.php/PulseAudio#Keyboard_volume_control "PulseAudio")
*   OSS: see [OSS#Using multimedia keys with OSS](/index.php/OSS#Using_multimedia_keys_with_OSS "OSS").

### Keyboard Shortcuts

Keyboard shortcuts are defined in two places: *Settings > Window Manager > Keyboard*, and *Settings > Keyboard > Shortcuts*.

### Polkit Authentication Agent

The [polkit-gnome](https://www.archlinux.org/packages/?name=polkit-gnome) agent will be installed along with [xfce4-session](https://www.archlinux.org/packages/?name=xfce4-session) and autostarted automatically; no user intervention is required. For more information, see [Polkit#Authentication agents](/index.php/Polkit#Authentication_agents "Polkit").

A third party polkit authentication agent for Xfce is also available, see [xfce-polkit-git](https://aur.archlinux.org/packages/xfce-polkit-git/).

### Display blanking

**Note:** There are some issues associated with blanking and resuming from blanking in some configurations. See [[3]](https://bbs.archlinux.org/viewtopic.php?id=194313&p=2)[[4]](https://bugzilla.xfce.org/show_bug.cgi?id=11107).

Some programs that are commonly used with Xfce will control monitor blanking and [DPMS](/index.php/DPMS "DPMS") (monitor powersaving) settings. They are discussed below.

	Xfce Power Manager

Xfce Power Manager will control blanking and DPMS settings. These settings can be configured by running *xfce4-power-manager-settings* and clicking the *Display* tab. Note that unticking the *Handle display power management* option means that the Power Manager will disable DPMS - it does not mean that the Power Manager will relinquish control of DPMS. Also note that it will not disable screen blanking. To disable both blanking and DPMS, right click on the power manager system tray icon or left click on the panel applet and make sure that the option labelled *Presentation mode* is ticked.

	XScreenSaver

See [XScreenSaver#DPMS and blanking settings](/index.php/XScreenSaver#DPMS_and_blanking_settings "XScreenSaver"). Note that if XScreenSaver is running alongside Xfce Power Manager, it may not be entirely clear which application is in control of blanking and DPMS as both applications are competing for control of the same settings. Therefore, in a situation where it is important that the monitor not be blanked (when watching a film for instance), it is advisable to disable blanking and DPMS through both applications.

	xset

If neither of the above applications are running, then blanking and DPMS settings can be controlled using the *xset* command, see [DPMS#Modifying DPMS and screensaver settings using xset](/index.php/DPMS#Modifying_DPMS_and_screensaver_settings_using_xset "DPMS").

## Tips and tricks

### Hide partitions from thunar and xfdesktop

See [Udisks#Hide selected partitions](/index.php/Udisks#Hide_selected_partitions "Udisks").

### Screenshots

Xfce has its own screenshot tool, [xfce4-screenshooter](https://www.archlinux.org/packages/?name=xfce4-screenshooter). It is part of the [xfce4-goodies](https://www.archlinux.org/groups/x86_64/xfce4-goodies/) group.

Go to *Applications > Settings > Keyboard*, *Application Shortcuts*. Add the `xfce4-screenshooter -f` (or `-w` for the active window) command to use the `Print` key in order to take fullscreen screenshots. See screenshooter's man page for other optional arguments.

Alternatively, an independent screenshot program like [scrot](/index.php/Taking_a_screenshot#scrot "Taking a screenshot") can be used.

### Disable Terminal F1 and F11 shortcuts

The xfce terminal binds F1 and F11 to help and fullscreen, respectively, which can make using programs like htop difficult. To disable those shortcuts, create or edit its configuration file, then log out and log back in. F10 can disabled in the Preferences menu.

 `~/.config/xfce4/terminal/accels.scm` 
```
(gtk_accel_path "<Actions>/terminal-window/fullscreen" "")
(gtk_accel_path "<Actions>/terminal-window/contents" "")

```

### Terminal color themes or palettes

Terminal color themes or palettes can be changed in GUI under Appearance tab in Preferences. These are the colors that are available to most console applications like [Emacs](/index.php/Emacs "Emacs"), [Vi](/index.php/Vi "Vi") and so on. Their settings are stored individually for each system user in `~/.config/xfce4/terminal/terminalrc` file. There are also so many other themes to choose from. Check forum thread [Terminal Colour Scheme Screenshots](https://bbs.archlinux.org/viewtopic.php?id=51818) for hundreds of available choices and themes.

#### Changing default color theme

XFCE's `extra/terminal` package comes with a darker color palette. To change this, append the following in your terminalrc file for a lighter color theme, that is always visible in darker Terminal backgrounds.

```
~/.config/xfce4/terminal/terminalrc

```

```
ColorPalette5=#38d0fcaaf3a9
ColorPalette4=#e013a0a1612f
ColorPalette2=#d456a81b7b42
ColorPalette6=#ffff7062ffff
ColorPalette3=#7ffff7bd7fff
ColorPalette13=#82108210ffff

```

#### Terminal tango color theme

To switch to tango color theme, open with your favorite editor

```
~/.config/xfce4/terminal/terminalrc

```

And add(replace) these lines:

```
ColorForeground=White
ColorBackground=#323232323232
ColorPalette1=#2e2e34343636
ColorPalette2=#cccc00000000
ColorPalette3=#4e4e9a9a0606
ColorPalette4=#c4c4a0a00000
ColorPalette5=#34346565a4a4
ColorPalette6=#757550507b7b
ColorPalette7=#060698989a9a
ColorPalette8=#d3d3d7d7cfcf
ColorPalette9=#555557575353
ColorPalette10=#efef29292929
ColorPalette11=#8a8ae2e23434
ColorPalette12=#fcfce9e94f4f
ColorPalette13=#72729f9fcfcf
ColorPalette14=#adad7f7fa8a8
ColorPalette15=#3434e2e2e2e2
ColorPalette16=#eeeeeeeeecec

```

### Colour management

Xfce has no native support for colour management. [[5]](https://bugzilla.xfce.org/show_bug.cgi?id=8559) See [ICC profiles](/index.php/ICC_profiles "ICC profiles") for alternatives.

### Multiple monitors

As of [xfce4-settings](https://www.archlinux.org/packages/?name=xfce4-settings) version 4.11.4, Xfce has support for multiple monitors. Settings can be configured in the *Applications* -> *Settings* -> *Display* dialog. For more information, see the [display](http://docs.xfce.org/xfce/xfce4-settings/display) article from the Xfce documentation.

### SSH agents

By default Xfce 4.10 will try to load gpg-agent or ssh-agent in that order during session initialization. To disable this, create an xfconf key using the following command:

```
xfconf-query -c xfce4-session -p /startup/ssh-agent/enabled -n -t bool -s false

```

To force using ssh-agent even if gpg-agent is installed, run the following instead:

```
xfconf-query -c xfce4-session -p /startup/ssh-agent/type -n -t string -s ssh-agent

```

To use [GNOME Keyring](/index.php/GNOME_Keyring "GNOME Keyring"), simply tick the checkbox *Launch GNOME services on startup* in the *Advanced* tab of *Session Manager* in Xfce's settings. This will also disable gpg-agent and ssh-agent.

Source: [http://docs.xfce.org/xfce/xfce4-session/advanced](http://docs.xfce.org/xfce/xfce4-session/advanced)

### Scroll a background window without shifting focus on it

Go to *Main Menu > Settings > Window Manager Tweaks > Accessibility* tab. Uncheck *Raise windows when any mouse button is pressed*.

### Mouse button modifier

By default, the mouse button modifier in Xfce is set to `Alt`. This can be changed with *xfconf-query*. For instance, the following command will set the `Super` key as the mouse button modifier:

```
$ xfconf-query -c xfwm4 -p /general/easy_click -n -t string -s "Super"

```

Strictly speaking, using multiple modifiers is not supported. However, as a workaround, multiple modifiers can be specified if the key names are separated with `><`. For instance, to set `Ctrl+Alt` as the mouse button modifier, you can use the following command:

```
$ xfconf-query -c xfwm4 -p /general/easy_click -n -t string -s "Ctrl><Alt"

```

## Troubleshooting

### Action buttons are missing icons

This happens if icons for some actions (Suspend, Hibernate) are missing from the icon theme, or do not have the expected names. To fix this, install an icon theme which has the necessary icons already added; see [Icons#Xfce icons](/index.php/Icons#Xfce_icons "Icons").

Then, you can switch to that icon theme using Applications -> Settings -> Appearance -> Icons.

Alternatively you can use the required icons provided by the icon theme you installed in your current icon theme. To do so, you first need to find out what the currently used icon theme is called. You can do so by using the command below:

```
$ xfconf-query -c xsettings -p /Net/IconThemeName

```

Then set the following variable:

```
$ icontheme=/usr/share/icons/*theme-name*

```

where *theme-name* is the name of the current icon theme.

Then create symbolic links from the current icon theme into the icon theme providing the icons (this example assumes the icons are being provided by the [elementary-xfce-icons](https://aur.archlinux.org/packages/elementary-xfce-icons/) theme.)

```
ln -s /usr/share/icons/elementary-xfce/apps/16/system-suspend.svg           ${icontheme}/16x16/actions/system-suspend.svg
ln -s /usr/share/icons/elementary-xfce/apps/16/system-suspend-hibernate.svg ${icontheme}/16x16/actions/system-hibernate.svg
ln -s /usr/share/icons/elementary-xfce/apps/22/system-suspend.svg           ${icontheme}/22x22/actions/system-suspend.svg
ln -s /usr/share/icons/elementary-xfce/apps/22/system-suspend-hibernate.svg ${icontheme}/22x22/actions/system-hibernate.svg
ln -s /usr/share/icons/elementary-xfce/apps/24/system-suspend.svg           ${icontheme}/24x24/actions/system-suspend.svg
ln -s /usr/share/icons/elementary-xfce/apps/24/system-suspend-hibernate.svg ${icontheme}/24x24/actions/system-hibernate.svg
ln -s /usr/share/icons/elementary-xfce/apps/48/system-suspend.svg           ${icontheme}/48x48/actions/system-suspend.svg
ln -s /usr/share/icons/elementary-xfce/apps/48/system-suspend-hibernate.svg ${icontheme}/48x48/actions/system-hibernate.svg

```

Log out and in again, and you should see icons for all actions.

### Desktop icons rearrange themselves

At certain events (such as opening the panel settings dialog) icons on the desktop rearrange themselves. This is because icon positions are determined by files in the `~/.config/xfce4/desktop/` directory. Each time a change is made to the desktop (icons are added or removed or change position) a new file is generated in this directory and these files can conflict.

To solve the problem, navigate to the directory and delete all the files other than the one which correctly defines the icon positions. You can determine which file defines the correct icon positions by opening it and examining the locations of the icons. The topmost row is defined as `row 0` and the leftmost column is defined by `col 0`. Therefore an entry of:

```
[Firefox]
row=3
col=0

```

means that the Firefox icon will be located on the 4th row of the leftmost column.

### GTK themes not working with multiple monitors

Some configuration tools may corrupt displays.xml, which results in GTK themes under *Applications Menu > Settings > Appearance* ceasing to work. To fix the issue, delete `~/.config/xfce4/xfconf/xfce-perchannel-xml/displays.xml` and reconfigure your screens.

### Icons do not appear in right-click menus

**Note:** Despite the deprecation of GConf, this method does still work.

Users may find that icons do not appear when right-clicking options within some applications, including those made with [Qt](/index.php/Qt "Qt"). This problem only appears to happen within Xfce. Run these two commands:

```
$ gconftool-2 --type boolean --set /desktop/gnome/interface/buttons_have_icons true
$ gconftool-2 --type boolean --set /desktop/gnome/interface/menus_have_icons true

```

### Keyboard settings are not saved in xkb-plugin

There is a bug in [xfce4-xkb-plugin](https://www.archlinux.org/packages/?name=xfce4-xkb-plugin) *0.5.4.1-1* which causes it to lose keyboard, layout switching and compose key settings. [[6]](https://bugzilla.xfce.org/show_bug.cgi?id=10226) As a workaround, enable *Use system defaults* in `xfce4-keyboard-settings`, then reconfigure *xfce4-xkb-plugin*.

### NVIDIA and xfce4-sensors-plugin

To detect and use sensors of nvidia gpu you need to install [libxnvctrl](https://www.archlinux.org/packages/?name=libxnvctrl) and then rebuild [xfce4-sensors-plugin](https://www.archlinux.org/packages/?name=xfce4-sensors-plugin) with [ABS](/index.php/ABS "ABS"). You also have the option of using [xfce4-sensors-plugin-nvidia](https://aur.archlinux.org/packages/xfce4-sensors-plugin-nvidia/) which replaces [xfce4-sensors-plugin](https://www.archlinux.org/packages/?name=xfce4-sensors-plugin).

### Panel applets keep being aligned on the left

Add a separator someplace before the right end and set its "expand" property. [[7]](https://forums.linuxmint.com/viewtopic.php?f=110&t=155602})

### Preferred Applications preferences have no effect

Most applications rely on [xdg-open](/index.php/Xdg-open "Xdg-open") for opening a preferred application for a given file or URL.

In order for xdg-open and xdg-settings to detect and integrate with the Xfce desktop environment correctly, you need to [install](/index.php/Install "Install") the [xorg-xprop](https://www.archlinux.org/packages/?name=xorg-xprop) package.

If you do not do that, your preferred applications preferences (set by exo-preferred-applications) will not be obeyed. Installing the package and allowing *xdg-open* to detect that you are running Xfce makes it forward all calls to *exo-open* instead, which correctly uses all your preferred applications preferences.

To make sure xdg-open integration is working correctly, ask *xdg-settings* for the default web browser and see what the result is:

```
# xdg-settings get default-web-browser

```

If it replies with:

```
xdg-settings: unknown desktop environment

```

it means that it has failed to detect Xfce as your desktop environment, which is likely due to a missing [xorg-xprop](https://www.archlinux.org/packages/?name=xorg-xprop) package.

### Restore default settings

If for any reason you need to revert back: to the default settings, rename `~/.config/xfce4-session/` and `~/.config/xfce4/`

```
$ mv ~/.config/xfce4-session/ ~/.config/xfce4-session-bak
$ mv ~/.config/xfce4/ ~/.config/xfce4-bak

```

Relogin for changes to take effect. If you get `Unable to load a failsafe session` upon login, see the [#Session failure](#Session_failure) section.

### Session failure

Symptoms include:

*   The mouse is an X and/or does not appear at all;
*   Window decorations have disappeared and windows cannot be closed;
*   (`xfwm4-settings`) will not start, reporting `These settings cannot work with your current window manager (unknown)`;
*   Errors reported by a [display manager](/index.php/Display_manager "Display manager") such as `No window manager registered on screen 0`.
*   Unable to load a failsafe session:

```
Unable to load a failsafe session.
Unable to determine failsafe session name.  Possible causes: xfconfd isn't running (D-Bus setup problem); environment variable $XDG_CONFIG_DIRS is set incorrectly (must include "/etc"), or xfce4-session is installed incorrectly. 

```

Restarting xfce or rebooting your system may solve the problem, but a corrupt session is the likely cause. Delete the session folder:

```
$ rm -r ~/.cache/sessions/

```

Also make sure that the relevant folders in `$HOME` are owned by the user starting `xfce4`. See [Chown](/index.php/Chown "Chown").

### Fonts in window title crashing xfce4-title

[Install](/index.php/Install "Install") [ttf-droid](https://www.archlinux.org/packages/?name=ttf-droid) and [ttf-dejavu](https://www.archlinux.org/packages/?name=ttf-dejavu). See also [FS#44382](https://bugs.archlinux.org/task/44382).

### Laptop lid settings ignored

You may find that the lid close settings in Xfce4 Power Manager are ignored, meaning that the laptop will always suspend on lid close, no matter what settings are chosen in the power manager. This is because the power manager is not set to handle lid close events by default. Instead, logind handles the lid close event. To change this behavior so that the the power manager handles lid close events, execute the following command:

```
$ xfconf-query -c xfce4-power-manager -p /xfce4-power-manager/logind-handle-lid-switch -s false

```

Note that each time the laptop lid settings are changed in the power manager, this setting will be reset.

### Rendering issues with Adwaita theme

Since the upgrade of gnome-themes-standard from 3.18.0-1 version to 3.20.0-1 the Adwaita theme exhibits several issues when being used in Xfce, like a frame around the notification area and dark background of the tooltip in eclipse.

A ugly solution is to downgrade the [gnome-themes-standard](https://www.archlinux.org/packages/?name=gnome-themes-standard) to the old 3.18.0-1 meanwhile. The package can be downloaded at:

```
$ wget https://archive.archlinux.org/repos/2016/04/08/extra/os/$(uname -m)/gnome-themes-standard-3.18.0-1-$(uname -m).pkg.tar.xz

```

and installed via pacman's `-U` option.

## See also

*   [Xfce - About](http://www.xfce.org/about/)
*   [http://docs.xfce.org/](http://docs.xfce.org/) - The complete documentation.
*   [Xfce-Look](http://www.xfce-look.org/) - Themes, wallpapers, and more.
*   [Xfce Wikia](http://xfce.wikia.com/wiki/Frequently_Asked_Questions) - How to edit the auto generated menu with the menu editor
*   [Xfce Wiki](http://wiki.xfce.org)