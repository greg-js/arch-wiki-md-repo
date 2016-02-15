PekWM은 Claes Nästen이 만들었다. 코드는 [aewm++](/index.php?title=Aewm%2B%2B&action=edit&redlink=1 "Aewm++ (page does not exist)") 창 관리자에 기초하지만 거듭 발전하면서 더 이상 [aewm++](/index.php?title=Aewm%2B%2B&action=edit&redlink=1 "Aewm++ (page does not exist)")와 비슷하지 않다. 또한 기능도 확장해서 [ion3](/index.php/Ion3 "Ion3"), [pwm](/index.php?title=Pwm&action=edit&redlink=1 "Pwm (page does not exist)"), [fluxbox](/index.php/Fluxbox "Fluxbox")와 비슷한 창 그룹화, 자동 속성, xinerama, 키 조합을 지원하는 keygrabber 등 훨씬 다양한 기능을 갖추었다.

## Contents

*   [1 설치](#.EC.84.A4.EC.B9.98)
*   [2 시작하기](#.EC.8B.9C.EC.9E.91.ED.95.98.EA.B8.B0)
    *   [2.1 방법 1: kdm/gdm](#.EB.B0.A9.EB.B2.95_1:_kdm.2Fgdm)
    *   [2.2 방법 2: xinitrc](#.EB.B0.A9.EB.B2.95_2:_xinitrc)
*   [3 PekWM 설정하기](#PekWM_.EC.84.A4.EC.A0.95.ED.95.98.EA.B8.B0)
    *   [3.1 메뉴](#.EB.A9.94.EB.89.B4)
        *   [3.1.1 MenuMaker](#MenuMaker)
        *   [3.1.2 수동으로 편집하기](#.EC.88.98.EB.8F.99.EC.9C.BC.EB.A1.9C_.ED.8E.B8.EC.A7.91.ED.95.98.EA.B8.B0)
    *   [3.2 단축키](#.EB.8B.A8.EC.B6.95.ED.82.A4)
    *   [3.3 마우스](#.EB.A7.88.EC.9A.B0.EC.8A.A4)
    *   [3.4 프로그램 자동 시작](#.ED.94.84.EB.A1.9C.EA.B7.B8.EB.9E.A8_.EC.9E.90.EB.8F.99_.EC.8B.9C.EC.9E.91)
    *   [3.5 변수](#.EB.B3.80.EC.88.98)
    *   [3.6 자동 속성](#.EC.9E.90.EB.8F.99_.EC.86.8D.EC.84.B1)
*   [4 테마](#.ED.85.8C.EB.A7.88)
    *   [4.1 GTK 테마](#GTK_.ED.85.8C.EB.A7.88)
*   [5 바탕화면 설정](#.EB.B0.94.ED.83.95.ED.99.94.EB.A9.B4_.EC.84.A4.EC.A0.95)
*   [6 문제점](#.EB.AC.B8.EC.A0.9C.EC.A0.90)
    *   [6.1 Nvidia TwinView를 사용할 때, 창이 두 화면 모두에 걸쳐 최대화되는 경우](#Nvidia_TwinView.EB.A5.BC_.EC.82.AC.EC.9A.A9.ED.95.A0_.EB.95.8C.2C_.EC.B0.BD.EC.9D.B4_.EB.91.90_.ED.99.94.EB.A9.B4_.EB.AA.A8.EB.91.90.EC.97.90_.EA.B1.B8.EC.B3.90_.EC.B5.9C.EB.8C.80.ED.99.94.EB.90.98.EB.8A.94_.EA.B2.BD.EC.9A.B0)
    *   [6.2 컴포지팅/투명 효과가 문제가 되는 경우](#.EC.BB.B4.ED.8F.AC.EC.A7.80.ED.8C.85.2F.ED.88.AC.EB.AA.85_.ED.9A.A8.EA.B3.BC.EA.B0.80_.EB.AC.B8.EC.A0.9C.EA.B0.80_.EB.90.98.EB.8A.94_.EA.B2.BD.EC.9A.B0)
*   [7 바깥 고리](#.EB.B0.94.EA.B9.A5_.EA.B3.A0.EB.A6.AC)

## 설치

저장소에서 PekWM을 설치하라.

```
pacman -S pekwm

```

## 시작하기

### 방법 1: kdm/gdm

먼저 kdm이나 gdm을 설치하여 활성화하라. **로그인 관리자**를 활성화하는 방법은 [여기](/index.php/Display_manager "Display manager")를 보라. PekWM이 세션 목록에 추가되어 있을 것이다. 로그인하기에 앞서 세션 목록에서 PekWM을 선택하라.

### 방법 2: xinitrc

자신의 홈 폴더에 있는 .xinitrc 파일(~/.xinitrc)에 다음을 추가하라.

```
exec pekwm

```

## PekWM 설정하기

~/.pekwm/config 파일이 주 설정 파일이다. 작업공간, 뷰포트, 메뉴, 화면 가장 자리 설정 등을 제어한다. [여기](http://www.pekwm.org/files/pekwm/doc/git/html/config/configfile.html) PekWM 문서에 자세한 설명과 함께 보기 파일이 있다.

### 메뉴

PekWM는 기본적으로 아치 저장소에서 설치될 때 미리 정의된 메뉴도 함께 온다. 이는 자신의 시스템을 반영하는 것이 아니며 따라서 실제로 설치된 것과 매우 다를 가능성이 높다. 보기로서 제공되는 것으로 그것을 수정하지 않고 사용해야할 필요는 없다.

자신의 메뉴는 ~/.pekwm/menu에 저장된다.

#### MenuMaker

자신의 시스템에 설치된 프로그램용 메뉴를 자동으로 생성하는 방법 가운데 하나는 Menumaker를 사용하는 것이다. 다음과 같이 실행하여 자신의 메뉴를 만들어라.

```
mmaker --no-desktop pekwm

```

**참고:** 위의 명령은 기존의 메뉴 파일을 덮어 쓰지 않을 것이다. 덮어쓰기를 원하면 -f 플래그를 위의 명령에 추가하라.

**mmaker –help**를 실행해 전체 옵션을 보라.

위의 명령으로 꽤 상세한 메뉴를 만들 수 있다. 이제 그 메뉴 파일을 수동으로 수정하거나 새로운 소프트웨어를 설치할 때마다 단순히 재생성하라.

#### 수동으로 편집하기

이미 말했듯이 ~/.pekwm/menu가 메뉴 파일이다. 이 파일의 문법은 이해하기 쉽다. 간단한 항목은 다음과 같은 구조이다.

```
Entry = "NAME" { Actions = "Exec COMMAND &" }

```

서브메뉴는 다음과 같이 구성된다.

```
Submenu = "NAME" {
     Entry = "NAME" { Actions = "Exec COMMAND &" }
     Entry = "NAME" { Actions = "Exec COMMAND &" }
}

```

(중괄호는 반드시 짝을 이루도록 해라. 그렇지 않으면 오류가 생겨 메뉴가 나타나지 않을 것이다.)

메뉴에 구분선을 추가하려면 다음을 사용하라.

```
Separator {}

```

PekWM은 동적 메뉴도 지원한다. 이는 기본적으로 메뉴 항목이나 서브메뉴로 그 항목이나 서브메뉴가 접근될 때마다 실행되는 스크립트의 결과를 출력하는 것이다.

온라인에서 동적 메뉴를 구할 수 있다. 메뉴에 맞는 문법을 반드시 확인하라. 이는 문법이 변하기 때문이다. 불행하게도 동적 메뉴가 온라인에 많지 않다. [여기](http://www.hewphoria.com/?p=submission&type=config)에서 Gmail과 네트워크 연결용 동적 메뉴를, [여기](http://urukrama.wordpress.com/2008/01/02/show-the-date-and-time-in-pekwms-menu/)에서는 시간과 날짜를 표시하는 동적 메뉴를 구할 수 있다. [pekwm_menu_tools](http://www.pekwm.org/projects/11)라는 프로젝트도 있는데 PekWM용 동적 메뉴를 생성하는 일련의 유용한 프로그램을 만들고자 한다.

### 단축키

~/.pekwm/keys에 단축키 설정이 저장된다. 이 파일에서 PekWM용 키보드 연결과 키연쇄를 제어한다. 키보드 연결로 프로그램을 실행하거나 PekWM 작동을 수행할 수 있다. 작동의 예를 들면, 메뉴 보기, 창 이동, 데스크톱 전환 등을 들 수 있다. 전체 PekWM 작동 목록은 [작동 문서](http://www.pekwm.org/files/pekwm/doc/git/html/config/keys_mouse.html#config-keys_mouse-actions)에 있다.

하나 이상의 작동을 키 조합에 할당할 수 있다. 그 방법은 작동을 쌍반점으로 구분하면 된다. 보기:

```
KeyPress = "Ctrl Mod1 R" { Actions = "Exec osdctl -s 'Reconfiguring'; Reload" }

```

Ctrl+Alt+R을 누르면 Pekwm은 화면에 'Reconfiguring'라는 글자를 나타내고(osdctl -s 'Reconfiguring') 재설정(Reload)한다. (참고로 이를 위해서는 osdsh를 설치해야 한다.)

키 "연쇄"도 다음과 같이 할 수 있다.

```
Chain = "Ctrl Mod1 C" {
     KeyPress = "Q" { Actions = "MoveToEdge TopLeft" }
     KeyPress = "W" { Actions = "MoveToEdge TopCenterEdge" }
}

```

곧, Ctrl+Alt+C를 누르고 나서 Q를 치면 활성 창을 화면 좌측 상단으로 이동하고 Ctrl+Alt+C를 누르고 나서 W를 치면 창을 상단 중앙으로 이동한다.

### 마우스

~/.pekwm/mouse 파일에 마우스 설정이 저장된다. 이 파일도 이해하기 쉽다. 보기:

```
FrameTitle {
     ButtonRelease = "1" { Actions = "Raise; Focus" }
}

```

위의 의미는 마우스 버튼 1(보통 왼쪽 버튼)을 창 프레임 제목 위에서 누르면 창이 최상위로 올라오면서 활성화된다는 말이다.

PekWM은 기본적으로 마우스를 창 위로 가져가면 창이 활성화되는데 이는 전통적인 방식인 클릭해서 창을 활성화하는 방식에 비해 불편해 하는 사람이 있다. 다음과 같은 줄을 찾아서 설명대로 하라.

```
# Remove the following line if you want to use click to focus.
# Uncomment the following line if windows should raise when clicked.

```

### 프로그램 자동 시작

시작 프로그램은 ~/.pekwm/start 파일에 있다. Pekwm을 시작할 때 바탕화면을 표시하거나 패널을 실행하려면 이 파일에 해당 프로그램을 추가하면 된다. 이 프로그램은 Pekwm이 시작될 때마다 실행되며 루트 메뉴에서 'Restart'를 해도 역시 실행됨을 유의하라.

다음과 같이 프로그램을 추가하라.

```
프로그램이름 &

```

이름 뒤에 &가 있어야 하며 그렇지 않으면 그 뒤에 어떤 것이라도 실행되지 않을 것이다. 다음의 보기를 참고하라.

```
xfce4-panel &
conky &
hsetroot -fill ~/images/darkwood.jpg &

```

이 파일을 사용하기에 앞서 다음 명령어로 실행 가능하도록 해야 한다.

```
chmod +x ~/.pekwm/start

```

### 변수

PekWM에서 사용되는 일반 변수는 ~/.pekwm/vars에 있다. 기본 항목 자체로 이해하기 쉽다.

```
$TERM="xterm -fn fixed +sb -bg white -fg black"

```

$TERM 변수가 PekWM 설정 파일에서 사용될 때마다 xterm -fn fixed +sb -bg white -fg black이 실행될 것이다. 다음과 같이 변경하면

```
$TERM="urxvt"

```

터미널 명령으로 urxvt가 실행될 것이다.

### 자동 속성

특정 프로그램이 특정한 작업공간에서 열리거나 특정 제목을 나타내거나 창 메뉴를 없애거나 자동으로 함께 탭으로 묶이기를 바란다면 여기에서 모두 지정할 수 있다. PekWM에서 가장 혼동되는 설정 파일이지만 가장 강력한 파일이기도 하다. 이 파일에서 설정될 수 있는 것이 너무 많아서 여기에서 다룰 수 없으나 [자동 속성 문서](http://www.pekwm.org/files/pekwm/doc/git/html/config/autoprops.html)에서 상세하게 설명된다. 기본 ~/.pekwm/autoproperties 파일 또한 자동 속성을 빠르게 이해할 수 있는 설명을 포함하고 있다.

## 테마

몇 곳의 테마 사이트 링크가 문서 하단에 있다. 테마를 설치하려면 테마 압축 파일을 테마 디렉토리에 풀어야 한다. 다음은 기본 테마 디렉토리이다.

*   시스템 전체 - /usr/share/pekwm/themes
*   사용자 - ~/.pekwm/themes

### GTK 테마

GTK 프로그램 테마를 변경하기 위해 [LXAppearance](http://www.gnomefiles.org/app.php/LXAppearance)를 사용할 수 있다.

## 바탕화면 설정

PekWM은 단순한 창 관리자이므로 별도의 프로그램을 사용해 바탕화면을 설정해야 한다. 다음 프로그램이 많이 쓰인다.

*   [feh](/index.php/Feh "Feh")
*   [Nitrogen](/index.php/Nitrogen "Nitrogen")
*   [xli](/index.php?title=Xli&action=edit&redlink=1 "Xli (page does not exist)")
*   [esetroot](/index.php?title=Esetroot&action=edit&redlink=1 "Esetroot (page does not exist)")
*   [hsetroot](/index.php?title=Hsetroot&action=edit&redlink=1 "Hsetroot (page does not exist)")

## 문제점

### Nvidia TwinView를 사용할 때, 창이 두 화면 모두에 걸쳐 최대화되는 경우

`~/.pekwm/config`를 열어 다음 줄을 찾아서

 `HonourRandr = "True"` 

아래 줄처럼 변경한다.

 `HonourRandr = "False"` 

[Source](https://projects.pekdon.net/projects/pekwm/tasks/124)

### 컴포지팅/투명 효과가 문제가 되는 경우

v0.1.11 기준, PekWM은 컴포지팅을 원할하게 지원하지 못하는 것 같다. 기본 xcompmgr은 작동하지만 투명 독과 패널은 그렇지 못하다. 또 창을 숨기면 그래픽 결함이 나타나는데 이를 해결하려면 모든 창의 투명도를 .999나 기타 다른 값으로 devilspie와 transset-df를 사용해 설정할 수 있다.

transset-df로 모든 창의 투명도를 .999로 설정하는 devilspie 스크립트 보기:

```
(spawn_async (str "transset-df -i " (window_xid) " .999" ))

```

## 바깥 고리

*   [Pekwm 홈페이지](http://pekwm.org/)
*   [젠투 위키 PekWM 문서](http://en.gentoo-wiki.com/wiki/PekWM)
*   [Box-Look PekWM 테마](http://box-look.org/index.php?xcontentmode=7403)
*   [Hewphoria PekWM 테마](http://hewphoria.com/?p=submission&type=theme&cat=1)
*   [Freshmeat PekWM 테마](http://themes.freshmeat.net/search/?q=pekwm&section=projects)