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
    *   [3.4 테마](#.ED.85.8C.EB.A7.88)
    *   [3.5 사운드](#.EC.82.AC.EC.9A.B4.EB.93.9C)
        *   [3.5.1 Xfce4 mixer](#Xfce4_mixer)
            *   [3.5.1.1 Xfce4 mixer의 기본 사운드카드 변경](#Xfce4_mixer.EC.9D.98_.EA.B8.B0.EB.B3.B8_.EC.82.AC.EC.9A.B4.EB.93.9C.EC.B9.B4.EB.93.9C_.EB.B3.80.EA.B2.BD)
        *   [3.5.2 키보드의 볼륨 조절 버튼](#.ED.82.A4.EB.B3.B4.EB.93.9C.EC.9D.98_.EB.B3.BC.EB.A5.A8_.EC.A1.B0.EC.A0.88_.EB.B2.84.ED.8A.BC)
            *   [3.5.2.1 단축키](#.EB.8B.A8.EC.B6.95.ED.82.A4)
    *   [3.6 키보드 단축키](#.ED.82.A4.EB.B3.B4.EB.93.9C_.EB.8B.A8.EC.B6.95.ED.82.A4)
    *   [3.7 Polkit Authentication Agent](#Polkit_Authentication_Agent)
    *   [3.8 화면에 아무것도 나오지 않을 경우](#.ED.99.94.EB.A9.B4.EC.97.90_.EC.95.84.EB.AC.B4.EA.B2.83.EB.8F.84_.EB.82.98.EC.98.A4.EC.A7.80_.EC.95.8A.EC.9D.84_.EA.B2.BD.EC.9A.B0)
*   [4 사용관련 도움말](#.EC.82.AC.EC.9A.A9.EA.B4.80.EB.A0.A8_.EB.8F.84.EC.9B.80.EB.A7.90)
    *   [4.1 thunar와 xfdesktop에서 파티션 숨기기](#thunar.EC.99.80_xfdesktop.EC.97.90.EC.84.9C_.ED.8C.8C.ED.8B.B0.EC.85.98_.EC.88.A8.EA.B8.B0.EA.B8.B0)
    *   [4.2 스크린샷(화면 갈무리)](#.EC.8A.A4.ED.81.AC.EB.A6.B0.EC.83.B7.28.ED.99.94.EB.A9.B4_.EA.B0.88.EB.AC.B4.EB.A6.AC.29)
    *   [4.3 터미널 상에서 F1 and F11 단축키 비활성화](#.ED.84.B0.EB.AF.B8.EB.84.90_.EC.83.81.EC.97.90.EC.84.9C_F1_and_F11_.EB.8B.A8.EC.B6.95.ED.82.A4_.EB.B9.84.ED.99.9C.EC.84.B1.ED.99.94)
    *   [4.4 터미널 색 테마, 팔레트](#.ED.84.B0.EB.AF.B8.EB.84.90_.EC.83.89_.ED.85.8C.EB.A7.88.2C_.ED.8C.94.EB.A0.88.ED.8A.B8)
        *   [4.4.1 기본 색 테마 변경하기](#.EA.B8.B0.EB.B3.B8_.EC.83.89_.ED.85.8C.EB.A7.88_.EB.B3.80.EA.B2.BD.ED.95.98.EA.B8.B0)
        *   [4.4.2 터미널 tango 색 테마](#.ED.84.B0.EB.AF.B8.EB.84.90_tango_.EC.83.89_.ED.85.8C.EB.A7.88)
    *   [4.5 색 관리](#.EC.83.89_.EA.B4.80.EB.A6.AC)
    *   [4.6 다중 모니터 사용](#.EB.8B.A4.EC.A4.91_.EB.AA.A8.EB.8B.88.ED.84.B0_.EC.82.AC.EC.9A.A9)
    *   [4.7 SSH agents](#SSH_agents)
    *   [4.8 포커스 변경 없이 다른 창 스크롤하기](#.ED.8F.AC.EC.BB.A4.EC.8A.A4_.EB.B3.80.EA.B2.BD_.EC.97.86.EC.9D.B4_.EB.8B.A4.EB.A5.B8_.EC.B0.BD_.EC.8A.A4.ED.81.AC.EB.A1.A4.ED.95.98.EA.B8.B0)
    *   [4.9 마우스 버튼 modifier키](#.EB.A7.88.EC.9A.B0.EC.8A.A4_.EB.B2.84.ED.8A.BC_modifier.ED.82.A4)
*   [5 기타 문제 해결](#.EA.B8.B0.ED.83.80_.EB.AC.B8.EC.A0.9C_.ED.95.B4.EA.B2.B0)
    *   [5.1 Action 버튼에 아이콘이 없는 경우](#Action_.EB.B2.84.ED.8A.BC.EC.97.90_.EC.95.84.EC.9D.B4.EC.BD.98.EC.9D.B4_.EC.97.86.EB.8A.94_.EA.B2.BD.EC.9A.B0)
    *   [5.2 데스크탑 아이콘 재정렬 문제](#.EB.8D.B0.EC.8A.A4.ED.81.AC.ED.83.91_.EC.95.84.EC.9D.B4.EC.BD.98_.EC.9E.AC.EC.A0.95.EB.A0.AC_.EB.AC.B8.EC.A0.9C)
    *   [5.3 다중 모니터에서 GTK 테마가 정상적으로 작동하지 않는 문제](#.EB.8B.A4.EC.A4.91_.EB.AA.A8.EB.8B.88.ED.84.B0.EC.97.90.EC.84.9C_GTK_.ED.85.8C.EB.A7.88.EA.B0.80_.EC.A0.95.EC.83.81.EC.A0.81.EC.9C.BC.EB.A1.9C_.EC.9E.91.EB.8F.99.ED.95.98.EC.A7.80_.EC.95.8A.EB.8A.94_.EB.AC.B8.EC.A0.9C)
    *   [5.4 오른쪽 마우스 클릭 메뉴에서 아이콘이 나타나지 않을 때](#.EC.98.A4.EB.A5.B8.EC.AA.BD_.EB.A7.88.EC.9A.B0.EC.8A.A4_.ED.81.B4.EB.A6.AD_.EB.A9.94.EB.89.B4.EC.97.90.EC.84.9C_.EC.95.84.EC.9D.B4.EC.BD.98.EC.9D.B4_.EB.82.98.ED.83.80.EB.82.98.EC.A7.80_.EC.95.8A.EC.9D.84_.EB.95.8C)
    *   [5.5 xkb-plugin에서 키보드 설정이 저장되지 않는 문제](#xkb-plugin.EC.97.90.EC.84.9C_.ED.82.A4.EB.B3.B4.EB.93.9C_.EC.84.A4.EC.A0.95.EC.9D.B4_.EC.A0.80.EC.9E.A5.EB.90.98.EC.A7.80_.EC.95.8A.EB.8A.94_.EB.AC.B8.EC.A0.9C)
    *   [5.6 NVIDIA와 xfce4-sensors-plugin](#NVIDIA.EC.99.80_xfce4-sensors-plugin)
    *   [5.7 패널이 항상 왼쪽으로 정렬되어 있는 문제](#.ED.8C.A8.EB.84.90.EC.9D.B4_.ED.95.AD.EC.83.81_.EC.99.BC.EC.AA.BD.EC.9C.BC.EB.A1.9C_.EC.A0.95.EB.A0.AC.EB.90.98.EC.96.B4_.EC.9E.88.EB.8A.94_.EB.AC.B8.EC.A0.9C)
    *   [5.8 Preferred Applications 설정 문제](#Preferred_Applications_.EC.84.A4.EC.A0.95_.EB.AC.B8.EC.A0.9C)
    *   [5.9 기본 설정 복구](#.EA.B8.B0.EB.B3.B8_.EC.84.A4.EC.A0.95_.EB.B3.B5.EA.B5.AC)
    *   [5.10 세션 실패](#.EC.84.B8.EC.85.98_.EC.8B.A4.ED.8C.A8)
    *   [5.11 창 제목의 폰트로 xfce4-title가 깨지는 문제](#.EC.B0.BD_.EC.A0.9C.EB.AA.A9.EC.9D.98_.ED.8F.B0.ED.8A.B8.EB.A1.9C_xfce4-title.EA.B0.80_.EA.B9.A8.EC.A7.80.EB.8A.94_.EB.AC.B8.EC.A0.9C)
    *   [5.12 노트북 덮개 설정 문제](#.EB.85.B8.ED.8A.B8.EB.B6.81_.EB.8D.AE.EA.B0.9C_.EC.84.A4.EC.A0.95_.EB.AC.B8.EC.A0.9C)
    *   [5.13 Adwaita 테마에서의 렌더링 문제](#Adwaita_.ED.85.8C.EB.A7.88.EC.97.90.EC.84.9C.EC.9D.98_.EB.A0.8C.EB.8D.94.EB.A7.81_.EB.AC.B8.EC.A0.9C)
*   [6 참고](#.EC.B0.B8.EA.B3.A0)

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

### 테마

XFCE 테마들은 [xfce-look.org](http://www.xfce-look.org)에서 구할 수 있다. *Xfwm* 테마들은 `/usr/share/themes/xfce4`에 저장되며 *Settings > Window Manager*의 설정 탭을 통하여 설정할 수 있다. [GTK+](/index.php/GTK%2B "GTK+") 테마는 *Settings > Appearance*에서 설정할 수 있다.

모든 어플리케이션에서 동일한 모양새를 얻고 싶다면, [Uniform look for Qt and GTK applications](/index.php/Uniform_look_for_Qt_and_GTK_applications "Uniform look for Qt and GTK applications")을 참고한다.

참고: [Cursor themes](/index.php/Cursor_themes "Cursor themes"), [Icons](/index.php/Icons "Icons"), [Font configuration](/index.php/Font_configuration "Font configuration")

### 사운드

#### Xfce4 mixer

**Note:** ᅟᅡXfce4 mixer와 Xfce4 volumed는 Streamer 1.0으로 포팅이 되지 않기 때문에 더이상 유지보수 되는 업스트림(upstream)으로 취급되지 않는다. 더 자세한 사항은 다음 링크(4.12)를 참고한다. [news post](http://www.xfce.org/about/news/?post=1425081600).

[xfce4-mixer](https://www.archlinux.org/packages/?name=xfce4-mixer)로 제공되는 Xfce4 mixer는 Xfce 팀에서 개발된 GUI 믹서 어플리케이션과 패널 플러그인이다. 해당 패키지는 xfce4 패키지 그룹의 일부분으로 포함되어 있다. [PulseAudio](/index.php/PulseAudio "PulseAudio")와 [OSS](/index.php/OSS "OSS") 지원을 원한다면 [gstreamer0.10-good-plugins](https://www.archlinux.org/packages/?name=gstreamer0.10-good-plugins) 설치가 필요하다.

Xfce4 mixer가 제대로 동작하도록 하기 위해 기본으로 설정되어 있는 사운드 카드를 변경해야할지도 모른다. 기본 사운드 카드 변경과 관련하여 자세한 사항을 알고 싶다면 [Advanced Linux Sound Architecture#Set the default sound card](/index.php/Advanced_Linux_Sound_Architecture#Set_the_default_sound_card "Advanced Linux Sound Architecture")를 참고한다. 또 다른 방법으로 [PulseAudio](/index.php/PulseAudio "PulseAudio")와 [pavucontrol](https://www.archlinux.org/packages/?name=pavucontrol) 또는 [PulseAudio](/index.php/PulseAudio "PulseAudio")와 [OSS](/index.php/OSS "OSS")를 함께 사용하는 방법이 있다. OSS 사용 부분이 궁금하다면 [OSS#Applications that use GStreamer](/index.php/OSS#Applications_that_use_GStreamer "OSS")을 참고한다.

변경된 기본 사운드카드 사항을 적용하기 위해서는 로그아웃을 해주어야 한다.

##### Xfce4 mixer의 기본 사운드카드 변경

[PulseAudio](/index.php/PulseAudio "PulseAudio") 또는 [xfce4-volumed](https://aur.archlinux.org/packages/xfce4-volumed/)와 같이 몇몇 경우에 Xfce4 Mixer의 볼륨 조절이 제대로 동작하게 하기 위해서 Xfce4 Mixer의 기본 사운드카드를 변경해야할 필요가 있다. [[2]](http://grumbel.blogspot.co.uk/2011/10/fixing-volume-control-in-xfce4.html)

기본 사운드카드를 변경하기 위해서는 *xfce4-settings-editor*를 연 뒤에 **xfce4-mixer** 부분을 들어간다. 그 뒤에 **sound-cards**항목들을 확인한다. 현재 사용하고 있는 사운드카드가 제대로 표시되어있는지 확인하고 **sound-card**와 **active-card** 항목의 값을 대체한다. PulseAudio를 사용하고 있는 경우에는 다음과 같은 내용과 비슷한 항목이 나타날 것이다: **PlaybackInternalAudioAnalogStereoPulseAudioMixer**. 변경이 완료된 후에는 변경사항을 적용하기 위해 로그아웃을 해준다.

#### 키보드의 볼륨 조절 버튼

[xfce4-mixer](https://www.archlinux.org/packages/?name=xfce4-mixer) 패키지의 버전이 `4.10.0-3` 이거나 더 높은 경우 mixer 패널 애플릿이 키보드를 이용한 볼륨조절 기능을 제공한다. 하지만 볼륨조절 관련 알림창은 보이지 않는다. 다른 방법으로는, [xfce4-volumed](https://aur.archlinux.org/packages/xfce4-volumed/)를 사용할 수 있다. 해당 프로그램은 Xfce4 mixer로 볼륨키를 매핑시키고 Xfce4-notifyd를 통해 관련 알림창을 화면에 표시해준다. 만약 PulseAudio를 사용하고 있고 Xfce4 Mixer 프로그램 사용을 원하지 않는 경우라면, [xfce4-pulseaudio-plugin](https://aur.archlinux.org/packages/xfce4-pulseaudio-plugin/)을 설치한다. 이 플러그인 또한 패널 애플릿으로서 키보드 버튼을 통한 볼륨조절과 관련 알림창을 띄워주는 기능을 가지고 있다.

**Warning:** [xfce4-pulseaudio-plugin](https://aur.archlinux.org/packages/xfce4-pulseaudio-plugin/) 의 경우 높은 CPU 사용량을 가질 수 있다. (~5% on i7 Intel CPU).

데스크탑 환경(Xfce, 그놈, KDE, etc.)이 아닌 경우는 다음을 참고한다. [List of applications#Volume managers](/index.php/List_of_applications#Volume_managers "List of applications").

##### 단축키

볼륨조절 키 관련 기능을 제공해주는 애플릿(applet)이나 데몬(daemon)을 사용하지 않는 경우, Xfce의 키보드 설정을 통해 사용자가 직접 볼륨조절 키를 매핑할 수 있다. 사용하고 있는 사운드 시스템에 따라 아래 항목을 참고한다.

*   ALSA: [Advanced Linux Sound Architecture#Keyboard volume control](/index.php/Advanced_Linux_Sound_Architecture#Keyboard_volume_control "Advanced Linux Sound Architecture")
*   PulseAudio: [PulseAudio#Keyboard volume control](/index.php/PulseAudio#Keyboard_volume_control "PulseAudio")
*   OSS: [OSS#Using multimedia keys with OSS](/index.php/OSS#Using_multimedia_keys_with_OSS "OSS")

### 키보드 단축키

키보드 단축키는 두 군데서 설정이 가능하다.

*   *Settings > Window Manager > Keyboard*
*   *Settings > Keyboard > Shortcuts*.

### Polkit Authentication Agent

[polkit-gnome](https://www.archlinux.org/packages/?name=polkit-gnome) 패키지는 xfce4-session을 따라서 자동으로 설치되며 Xfce실행 시 자동으로 실행된다. 사용자의 때문에 사용자의 설정이 특별하게 요구되지 않는다. 자세한 사항은 [Polkit#Authentication agents](/index.php/Polkit#Authentication_agents "Polkit")ᅟ을 참고한다.

Xfce를 위한 서드 파티 polkit 인증 관리자 또한 사용가능하다: [xfce-polkit-git](https://aur.archlinux.org/packages/xfce-polkit-git/) 참고.

### 화면에 아무것도 나오지 않을 경우

**Note:** 화면에 아무 것도 나오지 않거나 몇몇 설정에서 검은 화면으로 되었다가 화면이 복구되지 않고 아무 것도 나타나지 않는 문제들이 있다. 관련 문제는 다음 링크를 참고한다. [[3]](https://bbs.archlinux.org/viewtopic.php?id=194313&p=2)[[4]](https://bugzilla.xfce.org/show_bug.cgi?id=11107)

Xfce에서 흔히 사용되는 몇몇 프로그램들은 모니터 초기화와 [DPMS](/index.php/DPMS "DPMS") (모니터 전력관리)을 제어한다. 해당 문제들에 대한 온라인 상에서의 토론을 위 링크에서 참고할 수 있다.

	Xfce Power Manager

Xfce Power Manager는 모니터 초기화와 DPMS 설정을 관리한다. 이러한 설정들은 *xfce4-power-manager-settings*의 *Display*탭을 통해서 확인할 수 있다. *Handle display power management* 옵션을 해제하면 DPMS 기능이 비활성화 된다는 점에 유의한다(전원관리자가 DPMS 기능을 관리하지 않는다는 뜻이 아니다). 또 하나 유의해야 하는 점은 해당 옵션을 비활성화해도 스크린 초기화기능을 비활성화 하지 않는다는 점이다. 스크린 초기화 기능과 DPMS 기능 모두를 비활성화하기 위해서는 패널의 전원관리자 트레이 아이콘을 대고 오른쪽 마우스를 클릭하거나 패널 애플릿에서 왼쪽 마우스를 클릭하여 *Presentation mode*라고 표시되어 있는 옵션을 체크한다.

	XScreenSaver

[XScreenSaver#DPMS and blanking settings](/index.php/XScreenSaver#DPMS_and_blanking_settings "XScreenSaver")을 참고한다. 유의해야할 점은 만약 XScreenSaver와 Xfce Power Manager가 동시에 실행되는 경우 둘 중에 어떤 어플리케이션이 화면 초기화와 DPMS를 제어하는지 불분명해진다는 점이다. 이러한 문제 때문에 화면이 꺼져서는 안되는 상황이라면(예. 영화감상) 두 개의 어플리케이션 모두에서 blanking과 DPMS기능을 해제해주어야 한다.

	xset

만약 위에서 언급된 어플리케이션이 하나도 실행되고 있지 않다면 스크린 초기화와 DPMS 설정은 xset 명령어를 통해서 제어될 수 있다. 이와 관련된 부분은 [DPMS#Modifying DPMS and screensaver settings using xset](/index.php/DPMS#Modifying_DPMS_and_screensaver_settings_using_xset "DPMS")을 참고한다.

## 사용관련 도움말

### thunar와 xfdesktop에서 파티션 숨기기

[Udisks#Hide selected partitions](/index.php/Udisks#Hide_selected_partitions "Udisks") 참고.

### 스크린샷(화면 갈무리)

Xfce는 자체 스크린샷 도구를 제공한다([xfce4-screenshooter](https://www.archlinux.org/packages/?name=xfce4-screenshooter)). [xfce4-goodies](https://www.archlinux.org/groups/x86_64/xfce4-goodies/) 패키지 그룹으로 설치된다.

*Applications > Settings > Keyboard*에서 *Application Shortcuts*을 클릭한다. `xfce4-screenshooter -f` (현재창을 갈무리하려면 `-w`) 명령어를 추가하여 `Print` 키로 전체화면 크기의 화면을 갈무리 하기 위해 등록한다. 추가적인 정보를 확인하기 위해서는 screenshooter의 man page를 참고한다.

또 다른 방법으로, [scrot](/index.php/Taking_a_screenshot#scrot "Taking a screenshot")과 같이 화면 갈무리를 위한 독립된 프로그램이 있다.

### 터미널 상에서 F1 and F11 단축키 비활성화

Xfce 터미널은 기본으로 F1 and F11 키를 각각 도움말과 전체 화면 키로 매핑되었다. 이 때문에 htop과 같은 프로그램 사용에 있어 불편한 점이 있기 때문에, 해당 단축키들을 비활성화하기 위해서는 xfce 터미널을 위한 설정 파일을 만든 뒤에 로그아웃 한 뒤 다시 로그인 한다. F10 키의 경우에는 터미널의 설정창에서 비활성화될 수 있다.

 `~/.config/xfce4/terminal/accels.scm` 
```
(gtk_accel_path "<Actions>/terminal-window/fullscreen" "")
(gtk_accel_path "<Actions>/terminal-window/contents" "")

```

### 터미널 색 테마, 팔레트

터미널 색 테마와 팔레트는 터미널의 설정의 Appearance 탭을 통해서 변경할 수 있다. 제공되는 칼라들은 [Emacs](/index.php/Emacs "Emacs")와 [Vi](/index.php/Vi "Vi")와 같은 콘솔 어플리케이션의 대부분에서 사용가능한 것들이다. 각각의 설정들은 개별적으로 `~/.config/xfce4/terminal/terminalrc` 파일에 저장된다. 또한 다양한 선택 가능한 다른 색 테마들도 있다. 아치 리눅스의 다음 쓰레드를 확인하면 사용 가능한 수백가지의 테마들을 확인할 수 있다. [Terminal Colour Scheme Screenshots](https://bbs.archlinux.org/viewtopic.php?id=51818)

#### 기본 색 테마 변경하기

XFCE의 `extra/terminal` 패키지는 어두운 색 팔레트가 기본으로 되어 있다. 좀 더 밝은 색 테마를 위해서 이를 변경하기 위해서ᅟ는 다음 내용을 사용자의 terminalrc 파일 뒤에 삽입한다.

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

#### 터미널 tango 색 테마

tango 색 테마로 변경하기 위해서는 다음 파일을 연다.

```
~/.config/xfce4/terminal/terminalrc

```

다음 내용을 추가한다.

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

### 색 관리

Xfce는 색 관리를 위한 지원이 없다. 다른 방법을 위해 다음 링크를 참조한다. [[5]](https://bugzilla.xfce.org/show_bug.cgi?id=8559) See [ICC profiles](/index.php/ICC_profiles "ICC profiles")

### 다중 모니터 사용

[xfce4-settings](https://www.archlinux.org/packages/?name=xfce4-settings) 버전 4.11.4 이후로, Xfce는 다중 모니터에 대한 지원을 제공한다. *Applications* -> *Settings* -> *Display* 을 통해 설정할 수 있다. 더 자세한 내용은 다음 링크를 참고한다. [display](http://docs.xfce.org/xfce/xfce4-settings/display)

### SSH agents

기본적으로 Xfce 4.10은 세션 초기화 동안에 gpg-agent와 ssh-agent를 로드하려고 한다. 이를 비활성화 하려면 다음과 같이 xfconf 키를 생성한다:

```
xfconf-query -c xfce4-session -p /startup/ssh-agent/enabled -n -t bool -s false

```

gpg-agent가 설치된 환경에서 ssh-agent 사용을 강제하려면 다음 명령어를 실행한다:

```
xfconf-query -c xfce4-session -p /startup/ssh-agent/type -n -t string -s ssh-agent

```

[GNOME Keyring](/index.php/GNOME_Keyring "GNOME Keyring")를 사용하기 위해서, Xfce 설정의 *Session Manager* > *Advanced* 탭에서 *Launch GNOME services on startup* 체크박스를 해제한다. 해당 옵션은 gpg-agent와 ssh-agent 모두를 비활성화한다.

출처: [http://docs.xfce.org/xfce/xfce4-session/advanced](http://docs.xfce.org/xfce/xfce4-session/advanced)

### 포커스 변경 없이 다른 창 스크롤하기

*Main Menu > Settings > Window Manager Tweaks > Accessibility* 탭에서 *Raise windows when any mouse button is pressed* 체크를 해제한다.

### 마우스 버튼 modifier키

기본으로 Xfce는 modifier 키가 `Alt`로 설정되어 있다. modifier키는 *xfconf-query*에서 변경될 수 있다. 예를 들어, 다음 명령어는 modifier키를 `Super`로 바꾼다.

```
$ xfconf-query -c xfwm4 -p /general/easy_click -n -t string -s "Super"

```

임밀히 따지면 복수의 키를 modifier 키로 사용하는 것은 제공되지 않는다. 하지만 `><`로 구분된 키 조합을 사용하여 modifier 키를 설정할 수 있다. 예를 들면, `Ctrl+Alt`키를 마우스 버튼 modifier 키로 사용하기 위해 다음 명령어를 사용할 수 있다.

```
$ xfconf-query -c xfwm4 -p /general/easy_click -n -t string -s "Ctrl><Alt"

```

## 기타 문제 해결

### Action 버튼에 아이콘이 없는 경우

아이콘 테마에 몇몇 Action(Suspend, Hibernate)과 관련된 아이콘이 없는 경우 혹은 예상되는 이름을 갖고 있지 않는 경우에 발견되는 문제다. 이러ᅟ한 문제를 해결하기 위해서는 필요한 아이콘들이 추가된 아이콘 테마를 설치해야 한다. [Icons#Xfce icons](/index.php/Icons#Xfce_icons "Icons") 참고.

아이콘 테마 설치 후에는, Applications -> Settings -> Appearance -> Icons 탭에서 아이콘 테마를 변경한다.

다른 대안으로서, 필요한 아이콘을 이미 설치된 아이콘 테마로 변경할 수 있다. 이를 위해서는 먼저 사용되고 있는 아이콘 테마의 이름을 알아야 한다. 이는 다음 명령어를 통해 알 수 있다:

```
$ xfconf-query -c xsettings -p /Net/IconThemeName

```

이후, 다음과 같이 변수 이름을 설정한다.

```
$ icontheme=/usr/share/icons/*theme-name*

```

*theme-name*에는 현재 아이콘 테마의 이름을 적는다.

이 후, 누락된 아이콘에 대한 심볼릭 링크를 만든다. 밑의 예제에서는 [elementary-xfce-icons](https://aur.archlinux.org/packages/elementary-xfce-icons/) 테마의 아이콘을 이용해서 ${icontheme}에서 누락된 아이콘들의 심볼릭 링크를 만들어주는 과정이다.

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

로그아웃 뒤에 다시 재로그인하면 아이콘이 제대로 표시되는 것을 확인할 수 있다.

### 데스크탑 아이콘 재정렬 문제

패널 설정 다이얼로그를 여는 것과 같이 어떤 특정 이벤트가 발생했을 때 데스크탑의 아이콘들은 재정렬된다. 이러한 것은 아이콘들의 위치가 `~/.config/xfce4/desktop/` 디렉토리 안에 정의되어 있기 때문이다. 매번 변경될 때마다 데스크탑에서의 아이콘들에 관한 새로ᅟ운 파일이 생성되어 해당 파일들끼리 충돌하게 된다.

이 문제를 해결하기 위해서는 해당 디렉토리로 이동하여 정상적으로 위치가 정의되어 있는 파일을 제외한 모든 파일을 삭제한다. 행렬은 모두 숫자 0부터 시작하여 가장 위쪽 행은 `row 0`로, 가장 왼쪽 열은 `col 0`로서 정의된다. 때문에 다음 내용은

```
[Firefox]
row=3
col=0

```

Firefox 아이콘이 4번째 행에서 가장 왼쪽 열에 위치하게 된다는 것을 의미한다.

### 다중 모니터에서 GTK 테마가 정상적으로 작동하지 않는 문제

몇몇 설정 프로그램들은 displays.xml 파일을 망가뜨릴 수 있고 이 때문에 *Applications Menu > Settings > Appearance* 설정 탭의 동작을 제대로 작동되지 않게 할 수 있다. 문제를 해결하기 위해서는 `~/.config/xfce4/xfconf/xfce-perchannel-xml/displays.xml` 파일을 삭제하고 사용자의 화면을 재설정한다.and reconfigure your screens.

### 오른쪽 마우스 클릭 메뉴에서 아이콘이 나타나지 않을 때

**Note:** 현재 GConf가 deprecation상태이지만 아래 방법은 여전히 잘 작동함

사용자들은 [Qt](/index.php/Qt "Qt")로 제작된 몇몇 어플리케이션에서 오른쪽 마우스 클릭시에 아이콘들이 나타나지 않는 것을 볼 수 있다. 이는 오직 Xfce에서만 나타나는 문제로서, 다음 명령어를 실행한다:

```
$ gconftool-2 --type boolean --set /desktop/gnome/interface/buttons_have_icons true
$ gconftool-2 --type boolean --set /desktop/gnome/interface/menus_have_icons true

```

### xkb-plugin에서 키보드 설정이 저장되지 않는 문제

[xfce4-xkb-plugin](https://www.archlinux.org/packages/?name=xfce4-xkb-plugin) *0.5.4.1-1* 에서 키보드, 레이아웃 변경과 키 조합 설정과 관련해 저장되지 않는 버그가 있다.[[6]](https://bugzilla.xfce.org/show_bug.cgi?id=10226) 해결 방법으는 `xfce4-keyboard-settings`에서 *Use system defaults*를 클릭한 뒤에 *xfce4-xkb-plugin*를 재설정한다.

### NVIDIA와 xfce4-sensors-plugin

nvidia gpu 센서를 사용하기 위해서는 [libxnvctrl](https://www.archlinux.org/packages/?name=libxnvctrl) 패키지를 설치한 뒤에 [xfce4-sensors-plugin](https://www.archlinux.org/packages/?name=xfce4-sensors-plugin)를 [ABS](/index.php/ABS "ABS") 옵션과 함께 재빌드 해야한다. 또 다른 방법으로는 [xfce4-sensors-plugin](https://www.archlinux.org/packages/?name=xfce4-sensors-plugin) 대신 [xfce4-sensors-plugin-nvidia](https://aur.archlinux.org/packages/xfce4-sensors-plugin-nvidia/)을 사용하는 방법도 있다.

### 패널이 항상 왼쪽으로 정렬되어 있는 문제

패널에 "expand" 속성을 활성화하여 separator를 추가한다. [[7]](https://forums.linuxmint.com/viewtopic.php?f=110&t=155602}) 참고.

### Preferred Applications 설정 문제

대부분의 어플리케이션은 주어진 파일이나 URL을 열기 위해서 [xdg-open](/index.php/Xdg-open "Xdg-open")에 의존성이 있다.

xdg-open와 xdg-settings 이 Xfce 데스크탑 환경과 제대로 통합되어 작동되게 하기 위해서는 [xorg-xprop](https://www.archlinux.org/packages/?name=xorg-xprop) 패키지를 설치해야 한다.

만약 해당 패키지를 설치하지 않는 경우에는 preferred applications 설정이 제대로 반영되지 않는다.

ᅟᅵᆨxdg-open이 제대로 동작하고 있는지 확이하려면 *xdg-settings*를 이용해서 다음과 같이 명령어로 알아볼 수 있다.

```
# xdg-settings get default-web-browser

```

만약 다음과 같은 메세지가 출력된다면,

```
xdg-settings: unknown desktop environment

```

xdg-open이 Xfce 데스크탑 환경을 감지하지 못했다는 뜻이다([xorg-xprop](https://www.archlinux.org/packages/?name=xorg-xprop)패키지의 미설치가 원인).

### 기본 설정 복구

기본 설정으로 복구하기 위해서는 `~/.config/xfce4-session/`과 `~/.config/xfce4/`의 이름을 변경한다.

```
$ mv ~/.config/xfce4-session/ ~/.config/xfce4-session-bak
$ mv ~/.config/xfce4/ ~/.config/xfce4-bak

```

그 후에 다시 로그인하면 기본설정으로 복구된 것을 확인할 수 있다. 만약에 로그인 도중 `Unable to load a failsafe session` 메세지가 출력되었다면 [#세션 실패](#.EC.84.B8.EC.85.98_.EC.8B.A4.ED.8C.A8)를 참고한다.

### 세션 실패

포함되는 증상:

*   마우스 커서가 X 이거나 아예 나타나지 않는 경우
*   창 테두리가 나타나지 않고 창이 닫히지 않는 경우
*   (`xfwm4-settings`)가 시작되지 않고 `These settings cannot work with your current window manager (unknown)`라는 메세지가 나타나는 경우
*   [display manager](/index.php/Display_manager "Display manager") `No window manager registered on screen 0`와 같은 에러가 [display manager](/index.php/Display_manager "Display manager")에 나타나는 경우
*   failsafe 세션을 로드하지 못하는 경우

```
Unable to load a failsafe session.
Unable to determine failsafe session name.  Possible causes: xfconfd isn't running (D-Bus setup problem); environment variable $XDG_CONFIG_DIRS is set incorrectly (must include "/etc"), or xfce4-session is installed incorrectly. 

```

xfce를 재시작하거나 시스템 재부팅이 문제를 해결할 수 있지만 이전의 손상된 세션이 문제의 원인일 수 있기 때문에 해당 세션을 지운다.

```
$ rm -r ~/.cache/sessions/

```

또한 `$HOME` 내의 관련 폴더의 권한을 확인하여 `xfce4`를 실행하는 사용자의 권한으로 제대로 설정이 되어있는지 확인한다.. See [Chown](/index.php/Chown "Chown").

### 창 제목의 폰트로 xfce4-title가 깨지는 문제

[ttf-droid](https://www.archlinux.org/packages/?name=ttf-droid), [ttf-dejavu](https://www.archlinux.org/packages/?name=ttf-dejavu)를 설치한다. 관련 문제는 [FS#44382](https://bugs.archlinux.org/task/44382)를 참고한다.

### 노트북 덮개 설정 문제

Xfce4 전원 관리자에서 설정한 노트북 덮개 관련 설정이 제대로 작동하지 않는 문제가 있다. 때문에 사용자가 전원 관리자 내에서 어떤 설정을 했던간에 덮개를 덮으면 항상 suspend가 되어버리는 경우다. 이러한 문제는 전원관리자가 덮개가 덮히는 이벤트를 기본으로 관리하지 않기 때문이다. 대신에 logind가 전원관리자 대신 덮개가 닫히는 이벤트를 처리한다. 이러한 문제를 해결하기 위해서는 다음 명령어를 실행한다.

```
$ xfconf-query -c xfce4-power-manager -p /xfce4-power-manager/logind-handle-lid-switch -s false

```

전원관리자에서 노트북 덮개 관련 설정이 변경될 때마다 해당 설정은 초기화된다는 점에 유의한다.

### Adwaita 테마에서의 렌더링 문제

gnome-themes-standard가 3.18.0-1 버전에서 3.20.0-1로 업그레이드 된 이후로 Xfce 내에서 Adwaita 테마 사용시, 몇가지 이슈들이 나타난다. 해당 이슈에는 알림창 영역의 주변 프레임영역과 이클립스에서의 어두운 배경의 tooltip과 같은 문제들이 있다.

무식한 해결 방법으로는 [gnome-themes-standard](https://www.archlinux.org/packages/?name=gnome-themes-standard)패키지를 구버전 3.18.0-1으로 다운그레이드 하는 것이다. 해당 패키지는 다음 링크에서 다운로드 가능하다:

```
$ wget https://archive.archlinux.org/repos/2016/04/08/extra/os/$(uname -m)/gnome-themes-standard-3.18.0-1-$(uname -m).pkg.tar.xz

```

다운로드 후에는 pacman의 -U옵션을 통해서 설치될 수 있다.

## 참고

*   [Xfce - About](http://www.xfce.org/about/)
*   [http://docs.xfce.org/](http://docs.xfce.org/) - The complete documentation.
*   [Xfce-Look](http://www.xfce-look.org/) - Themes, wallpapers, and more.
*   [Xfce Wikia](http://xfce.wikia.com/wiki/Frequently_Asked_Questions) - How to edit the auto generated menu with the menu editor
*   [Xfce Wiki](http://wiki.xfce.org)