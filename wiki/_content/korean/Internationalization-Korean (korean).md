관련 항목

*   [Internationalization](/index.php/Internationalization "Internationalization")

이 문서는 아치리눅스 설치 후 한국어 입력을 설정하는 방법을 다룹니다.

이 문서를 읽기 전에 [X11](/index.php/X11 "X11") 환경을 미리 설치하고 설정하십시오. 이 문서는 콘솔에서 한국어를 입력하는 방법을 다루지 않습니다.

## Contents

*   [1 글꼴](#.EA.B8.80.EA.BC.B4)
*   [2 한글 입력기 고르기](#.ED.95.9C.EA.B8.80_.EC.9E.85.EB.A0.A5.EA.B8.B0_.EA.B3.A0.EB.A5.B4.EA.B8.B0)
    *   [2.1 입력기별 문제](#.EC.9E.85.EB.A0.A5.EA.B8.B0.EB.B3.84_.EB.AC.B8.EC.A0.9C)
*   [3 입력기 설정](#.EC.9E.85.EB.A0.A5.EA.B8.B0_.EC.84.A4.EC.A0.95)
    *   [3.1 ibus-hangul](#ibus-hangul)
    *   [3.2 uim-byeoru](#uim-byeoru)
    *   [3.3 scim-hangul](#scim-hangul)
    *   [3.4 fcitx-hangul](#fcitx-hangul)
    *   [3.5 nabi](#nabi)
    *   [3.6 dasom](#dasom)
*   [4 팁과 트릭](#.ED.8C.81.EA.B3.BC_.ED.8A.B8.EB.A6.AD)
    *   [4.1 한영키 사용하기](#.ED.95.9C.EC.98.81.ED.82.A4_.EC.82.AC.EC.9A.A9.ED.95.98.EA.B8.B0)
    *   [4.2 리브레오피스](#.EB.A6.AC.EB.B8.8C.EB.A0.88.EC.98.A4.ED.94.BC.EC.8A.A4)

## 글꼴

한글 입력을 사용하기 위해서는 한글 글꼴이 설치되어 있어야 합니다. [ttf-nanum](https://aur.archlinux.org/packages/ttf-nanum/)이나 [ttf-unfonts-core](https://aur.archlinux.org/packages/ttf-unfonts-core/) 패키지를 [AUR](/index.php/AUR "AUR")에서 설치하십시오. 터미널 등에서 사용할 수 있는 고정폭 글꼴이 필요하다면 AUR에서 [ttf-nanumgothic_coding](https://aur.archlinux.org/packages/ttf-nanumgothic_coding/) 패키지를 설치하십시오. 만약 향상된 글꼴 렌더링을 제공하는 [Infinality](/index.php/Infinality "Infinality") 패치를 사용하며, [Infinality 글꼴 저장소(Infinality-bundle-fonts)](/index.php/Unofficial_user_repositories#infinality-bundle-fonts "Unofficial user repositories")를 추가했다면, `ttf-nanum-fonts-ibx`, `ttf-nanumgothic-coding-ibx`, `ttf-unfonts-core-ibx` 등을 대신 설치하십시오. 옛한글을 읽고 입력하기 원한다면, 은 글꼴이나 [ttf-hamchorom-lvt](https://aur.archlinux.org/packages/ttf-hamchorom-lvt/) 패키지를 사용하십시오.

## 한글 입력기 고르기

입력기 프레임워크들은 여러가지 입력기와 입력 라이브러리를 포함하여 사용중인 입력기를 쉽게 전환할 수 있도록 해줍니다. [IBus](/index.php/IBus "IBus"), [uim](/index.php/UIM "UIM"), [fcitx](/index.php/Fcitx "Fcitx"), [scim](/index.php/Scim "Scim") 등의 입력기 프레임워크들이 한국어 입력을 지원합니다. 덧붙여, [nabi](https://aur.archlinux.org/packages/nabi/)는 독립적인 한글 입력기로서, 다른 프레임워크를 사용하지 않습니다. 이 항목에서는 한글 입력기 선택을 돕기 위한 정보를 제공합니다.

**참고:** 각 입력기나 입력기 프레임워크에서 나타나는 문제들을 반드시 확인한 후에 입력기를 고르십시오.

### 입력기별 문제

	ibus

	[IBus](/index.php/IBus "IBus")는 [GNOME](/index.php/GNOME "GNOME")과 우분투의 기본 입력기 프레임워크입니다. 가장 널리 지원을 받으며, 대부분의 어플리케이션에서 문제 없이 한글 입력을 할 수 있습니다.

	uim

	[uim](/index.php/UIM "UIM")은 여러 언어를 지원하는 크로스 플랫폼 입력기입니다. 아치리눅스 공식 저장소의 [uim](https://www.archlinux.org/packages/?name=uim) 패키지에는 한국어 입력기인 uim-byeoru가 포함되어 있습니다. uim-byeoru는 구글 크롬과 크로미움을 포함한 대부분의 어플리케이션에서 문제 없이 한글 입력을 할 수 있습니다. 하지만 [opera](https://www.archlinux.org/packages/?name=opera) 사용자라면 opera에서 uim-byeoru를 사용하려고 할 때 opera가 충돌하는 현상이 나타날 수 있습니다.

	scim

	scim 혹은 [Smart Common Input Method platform](/index.php/Smart_Common_Input_Method_platform "Smart Common Input Method platform")는 posix와 호환되는 운영체제를 위한 입력기 프레임워크입니다. 2014년 11월 현재, scim-hangul는 Google Chrome과 Chromium에서 문제를 일으킵니다. 기본 환경 변수를 사용할 경우, scim-hangul은 Google Chrome이나 Chromium에서 한글 입력을 할 수 없습니다. 2014년 현재, scim-hangul은 gedit과도 문제를 일으킵니다. 기본 환경 변수를 사용할 경우, 한글 입력기를 선택한 상태에서는 gedit에서 백스페이스가 정상적으로 작동하지 않습니다. 이 두 문제에 대한 해결 방법은 아래에서 다룹니다. 단, 아래의 해결 방법을 사용한 후에도 Google Chrome이나 Chromium에서는 입력기 버퍼 안의 글자가 사라지는 현상이 발생합니다. 즉 한글 입력 중에 스페이스바를 누르면 입력 중이던 마지막 한 글자가 사라집니다. *현재 이 문제에 대한 해결책은 없습니다.*

	fcitx

	[Fcitx](/index.php/Fcitx "Fcitx") 역시 POSIX 호환 운영체제들을 위한 입력기 프레임워크입니다. 사용하는데 문제는 없지만, GNOME을 사용한다면 탭 메뉴에서 몇 가지의 메뉴가 열리지 않습니다. 또한, Slack을 사용한다면, Electron이 입력을 무시해서 입력은 영어로밖에 입력이 되지 않습니다.

	nabi

	[nabi](https://aur.archlinux.org/packages/nabi/)는 최환진 씨가 개발하는 독립적 한글 입력기입니다. 옛한글 입력 등 한글 입력에 특화된 여러 기능을 제공합니다. 한글과 영어만을 사용한다면, 나비 입력기를 설치해보십시오. 2014년 11월 현재 나비는 Google Chrome과 Chromium에서 문제를 일으킵니다. 스페이스바를 누를 경우, 입력 중이던 글자가 공백 뒤에 놓이는 현상이 나타납니다. 즉 Google Chrome에서 `한글 입력에 문제가 있습니다`를 쳤다면, `한 글입력 에문제 가있습니다`와 같이 입력이 됩니다. 현재 나비는 아치 리눅스에서 제공되고 있지 않습니다.

	dasom

	다솜 입력기([dasom-git](https://aur.archlinux.org/packages/dasom-git/))는 다국어 입력기 프레임워크 입니다. 타 입력기에서 나타나는 끝글자 버그가 다솜에서는 발생하지 않습니다. 한글 및 영문 엔진, qt4, qt5, gtk2, gtk3, XIM 모듈을 지원하며, 세벌씩 자판과 드보락 자판도 지원합니다.

자신이 사용할 입력기를 골랐다면, 입력기 설정 섹션으로 넘어가십시오.

## 입력기 설정

### ibus-hangul

[IBus](/index.php/IBus "IBus") 문서를 보십시오.

### uim-byeoru

[User:Isaac914/uim](/index.php/User:Isaac914/uim "User:Isaac914/uim")의 설명을 따라 uim을 기본 입력기로 설정하십시오. uim을 기본 입력기로 설정한 후에 이 항목으로 돌아오십시오.

```
$ uim-pref-gtk (혹은 uim-pref-gtk3/uim-pref-qt4)

```

명령으로 uim의 설정창을 여십시오.

"Global settings"에서 *specify default IM*(기본 입력기 설정)에 체크 표시를 하십시오. 그리고 "Byeoru"를 기본 입력기로 설정하십시오.

또한, 'Edit'버튼을 눌러 사용하지 않을 입력기들을 비활성화할 수 있습니다.

한글과 영어 외에 다른 언어의 입력기도 사용하며, 여러 입력 방법 사이를 빠르게 전환하고 싶다면, *enable IM switching by hotkey* 에 체크표시를 하고, 원하는 단축키를 설정하십시오.

uim의 전역 설정을 마쳤다면, uim 설정창 왼쪽의 트리 메뉴에서 *Byeoru*를 찾아 클릭하십시오. 여기에서 세벌식 등으로 키보드 레이아웃을 변경할 수 있습니다. Byeoru가 사용할 한자 사전 등의 기타 설정 역시 조정할 수 있습니다.

이제 트리 메뉴에서 *Byeoru* 바로 아래에 있는 *Byeoru Keybinding 1*에 클릭하십시오. 여기에서 한영 전환에 사용할 단축키를 설정하십시오. 위에서 입력기 전환을 위한 단축키를 선택했다면, 여기에서는 반드시 다른 단축키를 사용해야 합니다. 대부분의 한국 사용자들은 한영 전환에 `Ctrl+space`나 `shift+space`를 사용합니다.

**참고:** 오른쪽 alt키(한/영키)로 한영 전환을 하고 싶다면, [#한영키 사용하기](#.ED.95.9C.EC.98.81.ED.82.A4_.EC.82.AC.EC.9A.A9.ED.95.98.EA.B8.B0) 섹션으로 가십시오.

이제 uim-byeoru를 이용하여 한글 입력을 할 수 있을 것입니다.

### scim-hangul

[scim-hangul](https://www.archlinux.org/packages/?name=scim-hangul) 패키지를 설치하십시오.

다음을 `.xintrc`, `.xprofile`, `.xsession` 파일에 추가하십시오.

```
export XMODIFIERS=@im=SCIM
export GTK_IM_MODULE="xim"
export QT_IM_MODULE="scim"
scim -d

```

**참고:** 이 문서에서 추천하는 환경변수와 [scim](/index.php/Scim "Scim") 항목에서 추천하는 환경변수 사이에 약간의 차이가 있습니다. [scim](/index.php/Scim "Scim")문서에서 추천하는 `GTK_IM_MODULE=”scim"` 대신 `export GTK_IM_MODULE="xim"`를 추가하였습니다. 이렇게 해야 Google Chrome과 Chromium에서 한글 입력이 가능해지며, gedit 등 gtk+ 3 어플리케이션에서 백스페이스를 정상적으로 사용할 수 있습니다.

### fcitx-hangul

[fcitx-hangul](https://www.archlinux.org/packages/?name=fcitx-hangul)과 자신이 사용하는 GUI 툴킷에 알맞은 fcitx 프론트엔드 패키지를 [설치](/index.php/Install "Install")합니다. [fcitx-gtk2](https://www.archlinux.org/packages/?name=fcitx-gtk2), [fcitx-gtk3](https://www.archlinux.org/packages/?name=fcitx-gtk3), [fcitx-qt4](https://www.archlinux.org/packages/?name=fcitx-qt4), [fcitx-qt5](https://www.archlinux.org/packages/?name=fcitx-qt5) 등에서 필요한 패키지를 선택하여 설치하십시오..

KDE 사용자라면 [kcm-fcitx](https://www.archlinux.org/packages/?name=kcm-fcitx)를 설치하십시오. KDE 시스템 설정 안에서 fcitx를 설정할 수 있습니다.

fcitx를 설치했다면, 다음을 `.xinitrc`, `.xprofile`, 혹은 `.xsession`에 추가하십시오.

```
export GTK_IM_MODULE=fcitx
export QT_IM_MODULE=fcitx
export XMODIFIERS=@im=fcitx

```

### nabi

[nabi](https://aur.archlinux.org/packages/nabi/) 패키지를 [AUR](/index.php/AUR "AUR")에서 설치하십시오.

나비의 최신 버전을 사용하고 싶다면, `git clone [https://github.com/choehwanjin/nabi.git](https://github.com/choehwanjin/nabi.git)` 명령을 내린 후, 터미널을 열어 복제된 git 저장소 안으로 들어갑니다. `./configure` 스크립트를 실행하여 필요한 라이브러리가 모두 설치되었는지 확인한 후, `make` 명령으로 나비를 컴파일하십시오. 컴파일이 끝났다면, 루트 권한으로`make install` 명령을 내리십시오.

나비를 설치했다면, `.xprofile`, `.xinitrc`, 혹은 `xsession` 파일에 다음을 추가하십시오.

```
export XIM=nabi
export XIM_ARGS=
export XIM_PROGRAM="nabi"
export XMODIFIERS="@im=nabi"
export GTK_IM_MODULE=xim
export QT_IM_MODULE=xim

```

X 세션을 재시작하십시오. 나비는 자동으로 시작될 것입니다. 기본 한글 키보드 레이아웃은 두벌식입니다. 세벌식, 두벌식 옛글 등 다른 키보드 레이아웃을 사용하고 싶다면 나비의 시스템 트레이 아이콘을 클릭하여 원하는 키보드 레아이웃을 선택하십시오.

### dasom

[dasom-git](https://aur.archlinux.org/packages/dasom-git/),[dasom-gtk-git](https://aur.archlinux.org/packages/dasom-gtk-git/) ,[dasom-qt-git](https://aur.archlinux.org/packages/dasom-qt-git/) 패키지와 [dasom-jeongeum-git](https://aur.archlinux.org/packages/dasom-jeongeum-git/) 패키지를 [AUR](/index.php/AUR "AUR")에서 설치하십시오.

설치 후, `.xprofile` 파일에 다음을 추가하십시오.

```
export GTK_IM_MODULE=dasom
export QT_IM_MODULE=dasom
export XMODIFIERS="@im=dasom"
dasom-daemon
dasom-indicator

```

만약, [GNOME](/index.php/GNOME "GNOME") 데스크탑을 사용한다면, 다음을 추가적으로 실행하십시오.

```
gsettings set org.gnome.settings-daemon.plugins.keyboard active false
gsettings set org.gnome.settings-daemon.plugins.xsettings overrides "{'Gtk/IMModule':<'dasom'>}"

```

X 세션을 재시작하십시오. 다솜입력기는 자동으로 시작될 것입니다.

## 팁과 트릭

### 한영키 사용하기

scim, nabi, uim 중 하나를 선택했다면 한영키를 이용하여 한영전환을 할 수 있습니다. 입력기를 시작하는 환경 변수 **뒤에** 다음 환경 변수들을 추가하십시오.

 `nano .xprofile` 
```
xmodmap -e 'remove mod1 = Alt_R'
xmodmap -e 'keycode 108 = Hangul'
xmodmap -e 'remove control = Control_R'
xmodmap -e 'keycode 105 = Hangul_Hanja'

```

이제 오른쪽 alt키가 "Hangul"이라는 키로, 오른쪽 Ctrl키가 "Hangul_Hanja"라는 키로 매핑되었을 것입니다. 이제 선택한 입력기의 설정창에서 한영키를 한영 전환을 위한 단축키로, 한자키를 한자 입력을 위한 단축키로 설정하십시오. 만약 .xinitrc, .xprofile, .xsession 파일에 위의 환경변수를 추가하는 것으로 한영키나 한자키를 사용할 수 없다면, 위의 변수들을 포함한 쉘 스크립트를 작성하여 X 세션을 시작할 때마다 실행되도록 설정하십시오.

### 리브레오피스

리브레오피스에서 한글 입력을 할 수 없다면, `.xinitrc`, `.xprofile` 혹은 `.xsession`에 다음을 추가해보십시오. `export OOO_FORCE_DESKTOP="gnome"`