관련 항목

*   [Browser Plugins](/index.php/Browser_Plugins "Browser Plugins")
*   [Firefox Tweaks](/index.php/Firefox_Tweaks "Firefox Tweaks")

[파이어폭스](http://www.firefox.com)는 [모질라](http://www.mozilla.com)에서 만든 인기 오픈 소스 그래픽 웹브라우저이다.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 설치](#설치)
*   [2 애드온](#애드온)
*   [3 플러그인](#플러그인)
    *   [3.1 GNOME 연결](#GNOME_연결)
    *   [3.2 철자 검사용 사전](#철자_검사용_사전)
    *   [3.3 파이어폭스 검색 엔진 추가](#파이어폭스_검색_엔진_추가)
        *   [3.3.1 아치 파이어폭스 검색](#아치_파이어폭스_검색)
*   [4 파이어폭스 관련 프로젝트](#파이어폭스_관련_프로젝트)
    *   [4.1 파이어폭스 파생 브라우저](#파이어폭스_파생_브라우저)
    *   [4.2 KDE 통합을 강화한 파이어폭스](#KDE_통합을_강화한_파이어폭스)
*   [5 문제 해결](#문제_해결)
    *   [5.1 Firefox 4 메뉴 단추](#Firefox_4_메뉴_단추)
    *   [5.2 폴더 열기 문제(KDE)](#폴더_열기_문제(KDE))
    *   [5.3 ~/Desktop를 계속해서 만들 때](#~/Desktop를_계속해서_만들_때)
    *   [5.4 플러그인이 팝업을 허용하지 못하게 하기](#플러그인이_팝업을_허용하지_못하게_하기)
    *   [5.5 마우스 가운데 클릭 오류](#마우스_가운데_클릭_오류)
    *   [5.6 백스페이스로 '뒤로가기' 단추 기능이 안 될 때](#백스페이스로_'뒤로가기'_단추_기능이_안_될_때)
    *   [5.7 로그인 정보를 기억하지 못할 때](#로그인_정보를_기억하지_못할_때)
    *   [5.8 어두운 Gtk 테마를 사용할 때 웹사이트나 입력 필드 문제](#어두운_Gtk_테마를_사용할_때_웹사이트나_입력_필드_문제)
    *   [5.9 파일 연결 문제](#파일_연결_문제)
    *   [5.10 "I'm Feeling Lucky" 모드](#"I'm_Feeling_Lucky"_모드)
    *   [5.11 "Do you want Firefox to save your tabs for the next time it starts?" 대화 상자가 나타나지 않을 때](#"Do_you_want_Firefox_to_save_your_tabs_for_the_next_time_it_starts?"_대화_상자가_나타나지_않을_때)
    *   [5.12 엔비디아 GPU 시스템에서 스크롤링 시에 CPU 사용률이 높아지고 느려질 때](#엔비디아_GPU_시스템에서_스크롤링_시에_CPU_사용률이_높아지고_느려질_때)
    *   [5.13 일부 웹페이지에서 글자가 보기 싫게 나타날 때](#일부_웹페이지에서_글자가_보기_싫게_나타날_때)
    *   [5.14 파이어폭스 13으로 업그레이드한 후 메뉴가 뜨지 않을 때](#파이어폭스_13으로_업그레이드한_후_메뉴가_뜨지_않을_때)
*   [6 같이 보기](#같이_보기)

## 설치

[firefox](https://www.archlinux.org/packages/?name=firefox) 꾸러미는 [공식 저장소](/index.php/Official_repositories "Official repositories")에 있으며 [pacman](/index.php/Pacman "Pacman")으로 설치할 수 있다.

영어가 선호하는 언어가 아니라면 그 밖의 많은 언어팩이 있다. 그 목록을 보려면 다음을 실행하라.

 `$ pacman -Ss firefox-i18n` 

파이어폭스에서 글꼴 안티앨리어스나 힌팅이 제대로 작동하지 않으면 [ttf-win7-fonts](https://aur.archlinux.org/packages/ttf-win7-fonts/)(추천)나 [ttf-ms-fonts](https://aur.archlinux.org/packages/ttf-ms-fonts/)를 설치해보고 [Font configuration](/index.php/Font_configuration "Font configuration")를 보라.

## 애드온

파이어폭스는 그 기능을 확장할 수 있는 수많은 애드온으로 아주 잘 알려져 있다. 파이어폭스 "애드온 관리자"에서 애드온을 설치하거나 관리할 수 있다.

인기 애드온 목록을 보려면 [인기순으로 정렬한 모질라 애드온 목록](https://addons.mozilla.org/en-US/firefox/extensions/?sort=popular)을 보라.

## 플러그인

*[브라우저 플러그인](/index.php/Browser_plugins "Browser plugins")을 보라*

어떤 플러그인이 설치되어 있고 활성화되었는지 다음을 브라우저 주소 입력줄에 입력하여 확인하라.

```
about:plugins

```

또는 메뉴 바에서 *애드온*을 선택한 후 좌측에서 “플러그인”을 선택하라.

### GNOME 연결

[AUR](/index.php/Arch_User_Repository "Arch User Repository")에서 [firefox-extension-gnome-keyring-git](https://aur.archlinux.org/packages/firefox-extension-gnome-keyring-git/)를 설치하여 파이어폭스 3.6.x를 그놈 키링에 연결하라.

[firefox-extension-firefoxnotify-git](https://aur.archlinux.org/packages/firefox-extension-firefoxnotify-git/)를 설치해 libnotify/notifyOSD를 통합할 수도 있다.

### 철자 검사용 사전

텍스트 입력 필드에서 마우스 오른 클릭하여 원하는 언어용 사전을 추가하라. 파이어폭스를 재시작하여 텍스트 입력 필드를 다시 클릭해 철자 검사 기능을 활성화하라.

또는 팩맨으로 다음을 실행하라.

```
pacman -Ss hunspell

```

### 파이어폭스 검색 엔진 추가

[https://addons.mozilla.org/en-US/firefox/browse/type:4/](https://addons.mozilla.org/en-US/firefox/browse/type:4/) 로 가서 설치하라.

자신의 검색 엔진을 추가하려면 `~/.mozilla/firefox/xxx.default/searchplugins/`(xxx는 자신의 프로파일 ID)를 보라.

또 다른 검색바 엔진 저장소: [http://mycroft.mozdev.org/](http://mycroft.mozdev.org/)

또는 [add-to-searchbar](https://firefox.maltekraus.de/extensions/add-to-search-bar) 확장 기능을 사용해 오페라 브라우저처럼 검색을 어떤 웹사이트에서도 자신의 검색바에 추가할 수 있다.

#### 아치 파이어폭스 검색

아치 전용 검색 (AUR, 위키, 포럼 등)을 파이어폭스 검색 도구바에 다음을 설치해 추가할 수 있다.

```
# pacman -S arch-firefox-search

```

## 파이어폭스 관련 프로젝트

### 파이어폭스 파생 브라우저

두 가지가 있다.

*   데비안 Iceweasel ([Wikipedia:Iceweasel](https://en.wikipedia.org/wiki/Iceweasel "wikipedia:Iceweasel"); [http://wiki.debian.org/Iceweasel](http://wiki.debian.org/Iceweasel)): 데비안에서 개발하며 2.0 기반이다.
*   GNU/IceCat ([Wikipedia:GNU IceCat](https://en.wikipedia.org/wiki/GNU_IceCat "wikipedia:GNU IceCat"); AUR: [icecat](https://aur.archlinux.org/packages/icecat/)): GNU IceWeasel로 이전에 불렸으며, GNU 프로젝트에서 베포하는 웹 브라우저이다. IceCat은 완전히 자유 소프트웨어로 만들어졌다. 운영 체제와 거의 모든 파이어폭스 애드온과 호환되며 파이어폭스를 완전히 대체할 수 있다.

### KDE 통합을 강화한 파이어폭스

*   [firefox-kde-opensuse](https://aur.archlinux.org/packages/firefox-kde-opensuse/)

	OpenSUSE 패치로 KDE통합을 하는 것이 최고라고 여겨진다.

*   [kpartsplugin](https://www.archlinux.org/packages/?name=kpartsplugin)

	이 플러그인은 KDE KParts를 사용하여 비KDE 브라우저에 파일 뷰어를 내장한다.

*   [Oxygen KDE](http://kde-look.org/content/show.php/?content=117962)

	이 애드온은 KDE Oxygen 테마, 색상 조합 검색, Faenza 아이콘 및 많은 수정을 추가하여 KDE 통합을 더욱 개선합니다.

## 문제 해결

### Firefox 4 메뉴 단추

기본적으로 아치 리눅스는 메뉴바의 고전 레이아웃을 나타낸다. Firefox 4부터 메뉴바를 대체하는 새로운 메뉴 단추를 나타내려면 보기->도구바->메뉴바를 체크 해제한다.

GNU/Linux에서는 윈도의 오렌지색 단추와는 달리 밋밋한 회색 단추만 볼 것이다. 하지만 이것을 파이어폭스 아이콘이나 아이콘과 그 옆에 "Firefox"글자가 있는 단추로 바꿀 수 있다.

`~/.mozilla/firefox/userprofile/chrome/userChrome.css` 파일에 추가하면 파이어폭스 아이콘과 그 옆에 "Firefox"글자가 있는 단추로 바뀔 것이다.

```
#appmenu-toolbar-button {
  list-style-image: url("chrome://branding/content/icon16.png");
}

```

이 파일에 다음을 추가하면 "Firefox" 글자만 제거하고 아이콘만 있는 단추가 될 것이다.

```
#appmenu-toolbar-button > .toolbarbutton-text,
#appmenu-toolbar-button > .toolbarbutton-menu-dropmarker {
  display: none !important;
}

```

**참고:** `chrome` 디렉토리와 `userChrome.css` 파일은 없다면 만들어야 한다.

### 폴더 열기 문제(KDE)

파이어폭스 다운로드 관리자에서 “폴더 열기”를 선택했을 때 자신이 선호하는 파일 관리자가 아닌 다른 파일 관리자가 실행된다면 KDE 시스템 설정에서 자신이 원하는 파일 관리자(돌핀 등)를 지정했는지 확인하라.

	**System Settings -> Default Applications -> File Manager**

이미 자신이 선호하는 파일 관리자를 지정했으나 Cervisia( 자신이 지정한 파일 관리자가 아닌 관리자)가 열리면 `~/.local/share/applications/defaults.list`에 다음 두 줄을 추가하라.

```
x-directory/normal=kde4-dolphin.desktop;kde4-kfmclient_dir.desktop;
inode/directory=kde4-dolphin.desktop;kde4-kfmclient_dir.desktop;kde4-gwenview.desktop;kde4-filelight.desktop;kde4-cervisia.desktop;

```

### ~/Desktop를 계속해서 만들 때

파이어폭스는 `~/Desktop`을 내려받은 파일이나 올린 파일을 저장하는 기본 장소로 사용한다. 다른 폴더로 지정하려면 `~/.config/user-dirs.dirs`를 만들어 다음을 추가하라.

```
XDG_DESKTOP_DIR="/home/<user>/"
XDG_DOWNLOAD_DIR="/home/<user>/<dir>"
XDG_TEMPLATES_DIR="/home/<user>/<dir>"
XDG_PUBLICSHARE_DIR="/home/<user>/<dir>"
XDG_DOCUMENTS_DIR="/home/<user>/<dir>"
XDG_MUSIC_DIR="/home/<user>/<dir>"
XDG_PICTURES_DIR="/home/<user>/<dir>"
XDG_VIDEOS_DIR="/home/<user>/<dir>"

```

`<user>`와 `<dir>`을 실제 이름으로 바꾸어라.

### 플러그인이 팝업을 허용하지 못하게 하기

팝업을 차단했는데도 팝업이 나타나는지 궁금했는가? 플래시 플러그인이 기본 설정을 무시하고 성가신 팝업을 허용하는 것 같다. 두려워마라. 그것도 차단할 수 있다.

해결 방법:

1.  about:config를 주소줄에 입력한다.
2.  그 페이지에서 오른 클릭 후 New -> Integer를 선택한다.
3.  privacy.popups.disable_from_plugins이라고 이름을 붙인다.
4.  값으로 2를 입력한다.

입력할 수 있는 값:

*   0: 플러그인에서 모든 팝업 허용
*   1: 팝업 허용하되 dom.popup_maximum이 최대 허용 한도
*   2: 플러그인에서 모든 팝업 차단
*   3: 플러그인에서 허용된 사이트를 포함한 모든 팝업 차단

### 마우스 가운데 클릭 오류

```
! The URL is not valid and cannot be loaded.

```

또 다른 증상은 가운데 클릭하면 예기치 못한 작동을 하여 임의의 웹페이지를 여는 경우가 있다 .

이는 유닉스 계열 운영 체제에서 마우스 가운데 단추의 쓰임새 때문이다. 그 단추는 선택된 텍스트나 클립보드에 복사된 텍스트를 붙여넣기하기 위해 사용된다. 그런데 파이어폭스에서는 그 단추를 누를 때 일치하는 텍스트가 있는 URL을 불러오는 기능을 하기 때문에 기능 충돌이 발생할 수 있다. 다음과 같은 방법으로 이 기능을 비활성화할 수 있다.

브라우저를 열고 주소줄에 다음을 입력한다.

```
about:config

```

**middlemouse.contentLoadURL**를 찾아서 false로 지정한다.

또 다른 방법으로 전통적인 방식(윈도 브라우저의 기본 방식)인 가운데 클릭 시 스크롤 커서로 변하게 하는 것이다. **general.autoScroll**을 찾아서 true로 지정한다.

### 백스페이스로 '뒤로가기' 단추 기능이 안 될 때

[이 기사](http://ubuntu.wordpress.com/2006/12/21/fix-firefox-backspace-to-take-you-to-the-previous-page/)에 따르면, 이 기능은 버그 수정을 위해 제거되었다. 다음과 같이 하면 원래 기능을 살릴 수 있다..

브라우저를 열고 다음을 주소줄에 입력한다.

```
about:config

```

**browser.backspace_action**를 찾아서 0(영)을 지정한다.

### 로그인 정보를 기억하지 못할 때

[파이어폭스 프로파일](http://support.mozilla.com/en-US/kb/Profiles#How_to_find_your_profile) 폴더에 있는 `cookies.sqlite`이 손상되었을 수 있다. 이를 수정하려면 파이어폭스를 종료하고 cookie.sqlite를 단순히 지우거나 이름을 변경한다.

터미널을 열어서 다음을 입력한다.

```
$ cd ~/.mozilla/firefox/xxxxxxxx.default/
$ rm -f cookies.sqlite

```

**참고:** xxxxxxxx는 임의의 8자리 문자열을 나타낸다.

파이어폭스를 재시작해서 문제가 해결되었는지 확인하다.

### 어두운 Gtk 테마를 사용할 때 웹사이트나 입력 필드 문제

어두운 [GTK](/index.php/GTK "GTK") 테마를 사용할 때, 입력 텍스트 필드(p.e. Amazon – 흰 배경색에 흰 글자)를 읽을 수 없는 웹사이트를 볼 수도 있다. 이는 그 사이트가 배경색이나 글자 색 가운데 하나만을 설정하여 파이어폭스가 나머지 하나를 테마에서 지정된 값을 사용하기 때문이다.

`~/.mozilla/firefox/.../chrome/userContent.css`에서 모든 웹페이지용 표준 색상을 명시적으로 설정하여 이 문제를 해결할 수 있다.

다음은 입력 필드를 표준 검정 글자/흰 배경색으로 설정한다. 이 설정보다 표시되는 사이트에서 지정한 값이 우선하므로 사이트가 원하는 색상은 나타난다.

```
input {
    -moz-appearance: none !important;
    background-color: white;
    color: black;
}

textarea {
    -moz-appearance: none !important;
    background-color: white;
    color: black;
}

```

이것은 색상을 강제로 지정한다.(**Preferences > Content > Color** 대화 상자에서 "Allow pages to choose their own colors [..]" 설정)

```
input {
    -moz-appearance: none !important;
    background-color: pink !important;
    color: green !important;
}

textarea {
    -moz-appearance: none !important;
    background-color: pink !important;
    color: green !important;
}

```

색상 값을 적절하게 바꾸거나 [Stylish](https://addons.mozilla.org/en-US/firefox/addon/2108)와 같은 애드온을 사용하라.

### 파일 연결 문제

[GNOME](/index.php/GNOME "GNOME") 사용자가 아닌 경우, 파이어폭스가 파일 형식(내려받기 대화 상자에서 "Open With" 부분)을 연결하지 못할 수도 있다. [libgnome](https://aur.archlinux.org/packages/libgnome/)를 설치하여 그 문제를 해결한다.

```
pacman -S libgnome

```

KDE를 사용한다면 다음을 할 수도 있다.

```
ln -s ~/.local/share/applications/mimeapps.list ~/.local/share/applications/mimeinfo.cache

```

당분간 파이어폭스는 KDE에서 명시한 프로그램을 사용해야 한다.

### "I'm Feeling Lucky" 모드

일부 검색 엔진은 운 좋은 예감이라는 기능이 있다. 구글의 "I'm Feeling Lucky"와 DuckDuckGo의 "I'm Feeling Ducky"가 그 예이다.

이 기능을 활성화하기.

1.  주소줄에 "**about:config**"를 입력
2.  **keyword.url**이라는 문자열을 찾음
3.  그 값이 있다면 검색 엔진의 URL로 변경

	구글의 경우 다음과 같이 설정:

	 `http://www.google.com/search?btnI=I%27m+Feeling+Lucky&q=` 

	DuckDuckGo의 경우 다음과 같이 설정:

	 `https://duckduckgo.com/?q=\` 

### "Do you want Firefox to save your tabs for the next time it starts?" 대화 상자가 나타나지 않을 때

[모질라 지원](http://support.mozilla.com/en-US/questions/767751) 사이트 인용

1.  주소줄에 "**about:config**"를 입력
2.  **browser.warnOnQuit**을 **true**로 설정
3.  **browser.showQuitWarning**을 **true**로 설정

### 엔비디아 GPU 시스템에서 스크롤링 시에 CPU 사용률이 높아지고 느려질 때

어떤 경우에 nVidia 소유 드라이버가 pixmap을 시스템 메모리 대신에 비디오 메모리에 저장하게 하면 파이어폭스와 같이 pixmap을 많이 사용하는 프로그램에서 체감 성능이 엄청나게 향상될 수 있다. 다음을 터미널에서 실행하라.

```
$ nvidia-settings -a InitialPixmapPlacement=2

```

결과가 만족스러우면 이것을 스크립트에 추가하고 자신의 데스크톱 환경 자동실행 프로그램에 넣어 시스템이 시작할 때마다 실행하라. 또 다른 방법으로 `~/.nvidia-settings-rc`에 추가하고 다음을 시스템을 시작할 때 실행하라.

```
$ nvidia-settings --load-config-only

```

이 설정은 [nvidia-settings 소스 코드](http://cgit.freedesktop.org/~aplattner/nvidia-settings/tree/src/libXNVCtrl/NVCtrl.h?id=b27db3d10d58b821e87fbe3f46166e02dc589855#n2797)에 나와 있다. 기타 성능 향상 설정도 추가했는지 확인하라([NVIDIA](/index.php/NVIDIA "NVIDIA")참고).

### 일부 웹페이지에서 글자가 보기 싫게 나타날 때

파이어폭스가 비트맵 글꼴을 사용하면, 일부 웹사이트에서 글꼴이 매우 보기 싫게 나타날 수 있다.(구글 크롬과 비교해 볼 경우)

[http://i.imgur.com/SMVdi.png](http://i.imgur.com/SMVdi.png) vs [http://i.imgur.com/jNmxU.png](http://i.imgur.com/jNmxU.png)

이 문제를 해결하기 위해 X용 비트맵 글꼴을 비활성화 시켜라.

```
$ sudo ln -s /etc/fonts/conf.avail/70-no-bitmaps.conf /etc/fonts/conf.d/

```

### 파이어폭스 13으로 업그레이드한 후 메뉴가 뜨지 않을 때

이 문제는 [fcitx](https://www.archlinux.org/packages/?name=fcitx) 입력 방법을 사용하는 중국어 사용자에게 발생할 수 있다. fcitx 환경 변수 설정을 확인해 보라. 또는 [fcitx-gtk2](https://www.archlinux.org/packages/?name=fcitx-gtk2), [fcitx-gtk3](https://www.archlinux.org/packages/?name=fcitx-gtk3), [fcitx-qt](https://www.archlinux.org/packages/?name=fcitx-qt)를 설치하여 해결할 수 있다.

## 같이 보기

*   [데비안과 모질라 파이어폭스에 관한 사실](http://web.glandium.org/blog/?p=97)

	데비안 파이어폭스 꾸러미 관리자가 상표 문제에 대해 설명

*   [Gnuzilla와 IceWeasel](http://www.gnu.org/software/gnuzilla/)

	GNU 모질라 파생 프로젝트 공식 웹사이트