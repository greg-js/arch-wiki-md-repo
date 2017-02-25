[SLiM](http://slim.berlios.de/)은 간단한 로그인 관리자입니다. SLiM은 간단합니다. SLiM은 가벼우며 쉽게 설정할 수 있습니다. SLiM은 [GNOME](/index.php/GNOME "GNOME") 또는 [KDE](/index.php/KDE "KDE")에 의존되지 않으며 단독으로 사용할 수 있습니다. [Xfce](/index.php/Xfce "Xfce"), [Openbox](/index.php/Openbox "Openbox"), [Fluxbox](/index.php/Fluxbox "Fluxbox") 등 가벼운 데스크톱을 좋아하는 분들은 시스템을 가볍게 할 수 있습니다.

## Contents

*   [1 설치](#.EC.84.A4.EC.B9.98)
*   [2 설정](#.EC.84.A4.EC.A0.95)
    *   [2.1 SLiM 활성화](#SLiM_.ED.99.9C.EC.84.B1.ED.99.94)
        *   [2.1.1 /etc/rc.conf 파일에서 활성화 방법](#.2Fetc.2Frc.conf_.ED.8C.8C.EC.9D.BC.EC.97.90.EC.84.9C_.ED.99.9C.EC.84.B1.ED.99.94_.EB.B0.A9.EB.B2.95)
        *   [2.1.2 /etc/inittab 파일에서 활성화 방법](#.2Fetc.2Finittab_.ED.8C.8C.EC.9D.BC.EC.97.90.EC.84.9C_.ED.99.9C.EC.84.B1.ED.99.94_.EB.B0.A9.EB.B2.95)
    *   [2.2 단일 데스크톱 환경](#.EB.8B.A8.EC.9D.BC_.EB.8D.B0.EC.8A.A4.ED.81.AC.ED.86.B1_.ED.99.98.EA.B2.BD)
    *   [2.3 다중 데스크톱 환경](#.EB.8B.A4.EC.A4.91_.EB.8D.B0.EC.8A.A4.ED.81.AC.ED.86.B1_.ED.99.98.EA.B2.BD)
    *   [2.4 테마](#.ED.85.8C.EB.A7.88)
        *   [2.4.1 다중 화면 설정](#.EB.8B.A4.EC.A4.91_.ED.99.94.EB.A9.B4_.EC.84.A4.EC.A0.95)
*   [3 기타 옵션](#.EA.B8.B0.ED.83.80_.EC.98.B5.EC.85.98)
    *   [3.1 커서 바꾸기](#.EC.BB.A4.EC.84.9C_.EB.B0.94.EA.BE.B8.EA.B8.B0)
    *   [3.2 테마 배경화면과 데스크톱 배경화면 통일 시키기](#.ED.85.8C.EB.A7.88_.EB.B0.B0.EA.B2.BD.ED.99.94.EB.A9.B4.EA.B3.BC_.EB.8D.B0.EC.8A.A4.ED.81.AC.ED.86.B1_.EB.B0.B0.EA.B2.BD.ED.99.94.EB.A9.B4_.ED.86.B5.EC.9D.BC_.EC.8B.9C.ED.82.A4.EA.B8.B0)
    *   [3.3 SLiM에서 컴퓨터 끄기, 재부팅, 절전모드, 나가기, 터미널 실행](#SLiM.EC.97.90.EC.84.9C_.EC.BB.B4.ED.93.A8.ED.84.B0_.EB.81.84.EA.B8.B0.2C_.EC.9E.AC.EB.B6.80.ED.8C.85.2C_.EC.A0.88.EC.A0.84.EB.AA.A8.EB.93.9C.2C_.EB.82.98.EA.B0.80.EA.B8.B0.2C_.ED.84.B0.EB.AF.B8.EB.84.90_.EC.8B.A4.ED.96.89)
    *   [3.4 Splashy 쓸 때 컴퓨터 끄기 에러](#Splashy_.EC.93.B8_.EB.95.8C_.EC.BB.B4.ED.93.A8.ED.84.B0_.EB.81.84.EA.B8.B0_.EC.97.90.EB.9F.AC)
    *   [3.5 SLiM의 로그인 정보](#SLiM.EC.9D.98_.EB.A1.9C.EA.B7.B8.EC.9D.B8_.EC.A0.95.EB.B3.B4)
    *   [3.6 SLiM에서 DPI 설정](#SLiM.EC.97.90.EC.84.9C_DPI_.EC.84.A4.EC.A0.95)
    *   [3.7 무작위로 테마 선택하기](#.EB.AC.B4.EC.9E.91.EC.9C.84.EB.A1.9C_.ED.85.8C.EB.A7.88_.EC.84.A0.ED.83.9D.ED.95.98.EA.B8.B0)
*   [4 자료](#.EC.9E.90.EB.A3.8C)

## 설치

```
# pacman -S slim

```

## 설정

부팅 시 활성화 설정, 사용하는 데스크톱 환경을 구동하기 위한 설정, 테마 설정

### SLiM 활성화

SLiM을 부팅 시 활성화 시키기 위해 `/etc/rc.conf`파일에서 데몬으로 추가해도 되며 `/etc/inittab` 파일에서 활성화 시켜도 됩니다. SLiM 이외에 [다른 방법](/index.php/Display_manager "Display manager")도 있습니다.

#### /etc/rc.conf 파일에서 활성화 방법

`/etc/rc.conf` 파일을 수정합니다.

```
# vim /etc/rc.conf

```

DAEMONS 항목에 slim을 추가합니다.

```
# DAEMONS=(... slim ...)

```

#### /etc/inittab 파일에서 활성화 방법

[`/etc/inittab` 파일을 수정합니다.](/index.php/Display_manager "Display manager")

```
# vim /etc/inittab

```

실행 레벨을 3에서 5로 수정합니다.

```
id:5:initdefault:

```

로그인 관리자로 SLiM을 선택합니다.

```
x:5:respawn:/usr/bin/slim >& /dev/null

```

### 단일 데스크톱 환경

단일 데스크톱 환경에서는 홈 디렉터리에 있는 `~/.xinitrc` 파일을 설정하여 데스크톱을 실행시킵니다.

```
#!/bin/sh

#
# ~/.xinitrc
#
# Executed by startx (run your window manager from here)
#

exec [session-command] # 해당 데스크탑 세션 실행

```

다른 데스크톱으로 바꾸고 싶을 때는 `[session-command]`를 입력하면 됩니다. 아래는 몇 가지 예시입니다.

```
exec openbox-session
exec fluxbox (or exec startfluxbox)
exec startxfce4
exec gnome-session
exec startkde
exec fvwm2
exec awesome

```

위 목록에 없는 데스크톱 환경이 있으면 해당 위키 페이지에서 확인하면 됩니다.

### 다중 데스크톱 환경

여러 데스크톱 환경을 선택할 수 있도록 하려면, SLiM으로 로그인할 선택할 수 있게 합니다. `~/.xinitrc` 파일과 `/etc/slim.conf`파일을 수정하여 세션 변수가 일치하도록 합니다. 로그인 화면에서 F1키를 눌러 고를 수 있습니다.

```
# The following variable defines the session which is started if the user doesn't explicitly select a session
# Source: http://svn.berlios.de/svnroot/repos/slim/trunk/xinitrc.sample

DEFAULT_SESSION=twm

case $1 in
kde)
	exec startkde
	;;
xfce4)
	exec startxfce4
	;;
icewm)
	icewmbg &
	icewmtray &
	exec icewm
	;;
wmaker)
	exec wmaker
	;;
blackbox)
	exec blackbox
	;;
*)
	exec $DEFAULT_SESSION
	;;
esac

```

### 테마

[slim-themes](https://www.archlinux.org/packages/?name=slim-themes) 패키지를 설치합니다.

```
# pacman -S slim-themes archlinux-themes-slim

```

[archlinux-themes-slim](https://www.archlinux.org/packages/?name=archlinux-themes-slim) 패키지는 여러 가지 테마가 포함되어 있습니다. 테마를 확인하려면 `/usr/share/slim/themes` 디렉터리에서 확인하면 됩니다. `/etc/slim.conf` 파일의 'current_theme' 설정 부분에서 원하는 테마 이름을 입력하면 설정됩니다.

```
#current_theme       default
current_theme       archlinux-simplyblack

```

미리 보기를 하려면 다음 명령어를 사용합니다.

```
$ slim -p /usr/share/slim/themes/<theme name>

```

종료를 하려면 로그인 입력창에 'exit'을 입력합니다.

#### 다중 화면 설정

`/usr/share/slim/themes/해당 테마/slim.theme` 파일에서 퍼센트 값을 조정

```
input_panel_x           50%
input_panel_y           50%

```

아니면 픽셀 값을 조정

```
# These settings set the "archlinux-simplyblack" panel in the center of my 1440x900 left screen
input_panel_x           495
input_panel_y           325

```

해당 파일에서 배경화면('stretch', 'tile', 'center' 또는 'color')을 설정할 수 있습니다. 자세한 내용은 [SLiM 홈페이지 공식 문서](http://slim.berlios.de/themes_howto.php)를 확인하십시오.

## 기타 옵션

### 커서 바꾸기

기본 X 마우스 커서를 새로운 디자인으로 바꾸고 싶다면 [slim-cursor](https://aur.archlinux.org/packages/slim-cursor/)패키지를 사용할 수 있습니다.

설치 후, `/etc/slim.conf` 파일 안의 아래의 부분을 지우세요:

```
cursor   left_ptr

```

이렇게 하시면 보통 화살표가 나옵니다. 이 설정은 `xsetroot -cursor_name`로 전달됩니다. 쓸 수 있는 커서의 이름을 [여기](http://cvsweb.xfree86.org/cvsweb/*checkout*/xc/lib/X11/cursorfont.h?rev=HEAD&content-type=text/plain)나 `/usr/share/icons/<your-cursor-theme>/cursors/` 에서 찾아 보실 수 있습니다.

로그인 화면에서 쓰이는 커서의 테마를 바꾸기 위해 `/usr/share/icons/default/index.theme` 파일을 만드시고 아래의 내용을 넣으세요:

```
[Icon Theme]
Inherits=<your-cursor-theme>

```

<your-cursor-theme> 부분을 쓰고 싶은 커서 테마 이름으로 바꾸세요. (예: whiteglass)

### 테마 배경화면과 데스크톱 배경화면 통일 시키기

SLiM 또는 데스크톱 배경화면 파일을 연결시켜 통일할 수 있습니다.

```
# mv /usr/share/slim/themes/default/background.jpg{,.bck}
# ln -s /path/to/mywallpaper.jpg /usr/share/slim/themes/default/background.jpg

```

### SLiM에서 컴퓨터 끄기, 재부팅, 절전모드, 나가기, 터미널 실행

컴퓨터 끄기나 재부팅, 대기모드, 로그아웃, 터미널 실행을 SLiM 로그인 화면에서 할 수 있습니다. 그러려면 유저네임 입력칸에 값과 루트 암호를 암호 입력칸에 넣으세요:

*   터미널을 실행하려면, 유저네임에 **console**을 넣으세요. (기본값은 따로 설치되어 있을 xterm 입니다... 사용할 터미널을 바꾸려면 `/etc/slim.conf`를 수정하세요.
*   컴퓨터 끄기를 하려면 유저네임에 **halt**를 넣으세요.
*   재부팅을 하려면 유저네임에 **reboot**를 넣으세요.
*   bash로 나가려면 유저네임에 **exit**를 넣으세요.
*   절전모드로 전환하려면, 유저네임에 **suspend**를 넣으세요. (절전모드는 기본값에서 비활성화 되어있습니다. 활성화 하려면 루트로 로그인해서 `/etc/slim.conf` 파일의 `suspend_cmd` 부분을 지우고, 필요한 경우에는 대기모드 명령을 수정하세요. (예: `/usr/sbin/suspend`를 `sudo /usr/sbin/pm-suspend`로 바꾸기)

### Splashy 쓸 때 컴퓨터 끄기 에러

Splashy와 SLiM을 같이 사용한다면 가끔씩 GNOME이나, Xfce, LXDE 등의 메뉴에서 컴퓨터를 끄거나 리부팅 할 때 안 되기도 합니다. `/etc/slim.conf`과 `/etc/splash.conf` 파일을 확인하고 DEFAULT_TTY=7 부분을 xserver_arguments vt07로 설정하세요.

### SLiM의 로그인 정보

utmp와 wtmp는 누가, 언제 가장 마지막에 로그인 했는지 같은 로그인 정보의 잘못된 기록을 발생시킵니다. 기본값에서 SLiM은 utmp와 wtmp로 로그인 하는 걸 로그하는 것을 실패합니다. 이것을 고치려면 `slim.conf` 파일에 아래와 같이 넣으세요:

```
 sessionstart_cmd    /usr/bin/sessreg -a -l $DISPLAY %user
 sessionstop_cmd     /usr/bin/sessreg -d -l $DISPLAY %user

```

### SLiM에서 DPI 설정

Xorg 서버는 보통 DPI를 잡아냅니다. 그러나 못 잡아낸다면 SLiM이 문제일 수 있습니다. `/etc/X11/xinit/xserverrc`에 DPI를 argument -dpi 96 으로 설정한다면 SLiM에선 동작하지 않을 것입니다. 해결하기 위해 `slim.conf`의 아래의 부분을:

```
 xserver_arguments   -nolisten tcp vt07 

```

아래와 같이 바꾸세요:

```
 xserver_arguments   -nolisten tcp vt07 -dpi 96

```

### 무작위로 테마 선택하기

`/etc/slim.conf` 파일의 'current_theme' 설정에 콤마(,)를 추가하여 무작위로 선택할 테마를 지정하면 됩니다.

## 자료

*   [SLiM 홈페이지](http://slim.berlios.de/)
*   [SLiM 문서](http://slim.berlios.de/manual.php)