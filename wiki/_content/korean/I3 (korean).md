[i3](http://i3wm.org/) 는 동적 [타일링 창 관리자](https://en.wikipedia.org/wiki/Tiling_window_manager "wikipedia:Tiling window manager")로 [wmii](/index.php/Wmii "Wmii")에서 영감을 받았으며 주로 개발자와 상급 사용자를 대상으로 한다.

클라이언트(창)는 컨테이너 내에서 나무 자료 구조로 구성된다. 나무는 수평이나 수직 분할로 가지를 치며 컨테이너는 스택이나 탭 배열로 설정할 수도 있다. 기존에 익숙한 플로팅 창도 타일링 창과 잘 맞지 않는 경우를 대비해 사용할 수 있으며 이 플로팅 창은 모든 타일링 창보다 위에 나타난다.

## Contents

*   [1 설치](#설치)
*   [2 설정](#설정)
    *   [2.1 시작](#시작)
    *   [2.2 설정 파일 및 키 조합](#설정_파일_및_키_조합)
    *   [2.3 상태 표시 줄](#상태_표시_줄)
    *   [2.4 새로운 방법: i3bar](#새로운_방법:_i3bar)
    *   [2.5 i3bar와 dzen2 비교](#i3bar와_dzen2_비교)
*   [3 i3lock이 시스템 절전 모드와 작동하도록 하기](#i3lock이_시스템_절전_모드와_작동하도록_하기)
*   [4 기타 도구](#기타_도구)
*   [5 추가 자료](#추가_자료)

## 설치

i3는 [community](/index.php/Community_repository "Community repository") 저장소에 있다. [i3](https://www.archlinux.org/groups/x86_64/i3/) 그룹을 설치하면 그에 속하는 [i3lock](https://www.archlinux.org/packages/?name=i3lock), [i3status](https://www.archlinux.org/packages/?name=i3status) 와 [i3-wm](https://www.archlinux.org/packages/?name=i3-wm)이 설치된다. 또 다른 방법으로 그룹 내 각 꾸러미를 따로 설치할 수도 있다. 창 관리자는 [i3-wm](https://www.archlinux.org/packages/?name=i3-wm), 상태 표시 줄은 [i3status](https://www.archlinux.org/packages/?name=i3status), 화면 잠금기는 [i3lock](https://www.archlinux.org/packages/?name=i3lock)이다.

개발 버전을 설치하려면 [i3-git](https://aur.archlinux.org/packages/i3-git/)를 [AUR](/index.php/AUR "AUR")에서 설치하라. 그놈 세션을 추가하려면 [i3-gnome](https://aur.archlinux.org/packages/i3-gnome/)를 설치하라.

## 설정

### 시작

`~/.xinitrc`를 편집해 다음을 추가하라.

```
exec i3 

```

i3가 그 출력을 기록(디버깅 시 유용)하게 하려면 다음 줄을 `~/.xinitrc`에 추가하라.

```
exec i3 -V >> ~/.i3/i3log 2>&1 

```

Nvidia 드라이버 **302.17** 이전 버전을 사용하려면 --force-xinerama 플래그를 `~/.xinitrc`에 추가하라. 자세한 설명은 [i3wm.org](http://i3wm.org/docs/multi-monitor.html)를 보라.

```
exec i3 --force-xinerama 

```

### 설정 파일 및 키 조합

i3는 단순한 텍스트 파일을 사용해 설정한다. i3는 `~/.i3/config` 파일을 먼저 찾아 보고 없으면 기본 설정 파일인 `/etc/i3/config`를 읽어 들인다. 설정을 변경하기 위해 다음과 같이 자신의 홈 디렉토리로 파일을 복사하라.

```
cp /etc/i3/config ~/.i3/config 

```

이 파일에서 다음과 같은 것을 설정할 수 있다.

*   터미널 (see [i3-sensible-terminal](http://buildbot.i3wm.org/docs/i3-sensible-terminal.html))
*   테두리 색
*   글꼴
*   키 연결
*   작업공간 이름
*   기본 컨테이너 배치
*   프로그램을 특정 작업공간에 할당

i3 [사용자 설명서](http://i3wm.org/docs/userguide.html)에서 이 파일 설정에 대해 일목요연하게 설명한다. 기본 키 연결을 설정할 때 기본 키로 Mod1 (보통 Alt 키)나 Mod3/Mod4 (윈도 키)를 사용하며, 때로는 이 키와 Ctrl이나 Shift와 조합한다. 자신의 시스템의 모든 종류의 Mod# 키를 확인하려면 `xmodmap` 명령어를 인수 없이 실행하라.

기본 키 조합은 키 코드에 따르며 키보드 상의 실제 문자와는 무관하다! 이에 익숙하지 않다면 설정 파일에서 `bind` 지시자를 `bindsym` 지시자로 대체할 수 있다. 키 조합에 대해 더 알고 싶으면 다음 부분을 보라.

다음은 가장 중요한 키 조합 가운데 일부이다.

*   프로그램 실행하기: Mod 키+d
*   새 터미널 열기: Mod 키+Enter
*   창 전환하기: Mod 키+ "jkl;" 중에 하나(Vim과 비슷한 키 설정) 또는 화살표 키
*   창 이동하기: Mod 키+Shift+ "jkl;" 중에 하나 또는 화살표 키
*   작업 공간 전환하기: Mod 키+ 숫자
*   다른 작업 공간으로 이동하기: Mod 키+Shift+ 숫자

i3는 창 관리를 위해 컨테이너를 사용한다는 점을 명심하라. [Wmii](/index.php/Wmii "Wmii")와 대조적으로 창을 수평으로 나눌 수 있다. 단순하게 창을 Mod1+Shift+방향 키로 아래나 위로 화면 가장자리 너머로 이동하라. 새로운 가로 줄이 나타날 것이다. Mod4+Ctrl+방향키로 창을 선택한 방향으로 확대할 수 있다. 방향키는 "jkl;"와 화살표 키를 말한다.

다음 세 가지의 컨테이너 모드가 있다.

*   보통(타일): Mod 키+e
*   탭: Mod 키+w
*   스택: Mod 키+s

추가로 전체 화면: Mod 키+f

[i3 키 조합 일람표 (pdf)](http://i3wm.org/docs/refcard.pdf)

### 상태 표시 줄

내부 상태 표시 줄 i3-wsbar는 지원 중단되었으며 i3 v4.0부터 i3bar가 사용된다.

### 새로운 방법: i3bar

dzen2를 사용하는 i3-wsbar와 달리, i3bar는 [i3-wm](https://www.archlinux.org/packages/?name=i3-wm) 외에는 어떤 의존성도 없다. [conky](/index.php/Conky "Conky")나 i3status가 생성하는 정보를 i3bar에서 볼 수 있다. 보기(4.1버전 기준):

 `~/.i3/config` 
```

bar { 
    output            LVDS1 
    status_command    i3status 
    position          top 
    mode              hide 
    workspace_buttons yes 
    tray_output       none 

    font -misc-fixed-medium-r-normal--13-120-75-75-C-70-iso10646-1 

    colors { 
        background #000000 
        statusline #ffffff 

        focused_workspace  #ffffff #285577 
        active_workspace   #ffffff #333333 
        inactive_workspace #888888 #222222 
        urgent_workspace   #ffffff #900000 
    } 
} 

```

더 자세한 내용은 공식 사용자 설명서 [i3bar 설정하기](http://i4wm.org/docs/userguide.html#_configuring_i3bar) 부분을 보라.

### i3bar와 dzen2 비교

i3bar와 dzen2를 여기서 비교한 점은 conky나 i3status의 입력을 두 프로그램이 얼마나 잘 처리할 수 있는지만 고려한 것이다.

| 프로그램 | 색상 코드 | 서식 | 특수 글꼴 | 독 | 시스템 트레이 |
| i3bar | 지원 | 미지원, 우측 정렬 | 미지원 (UTF8만 지원) | 지원 | 지원 |
| dzen2 | 지원 | 미지원, 좌측 정렬 | 지원 | 지원 (svn 버전) | 미지원 |

i3bar가 매우 활발하게 개발되고 포맷을 설정할 수 있고, 글꼴을 지정할 수 있지만, dzen2-svn이 i3bar보다 8월 7일 기준으로 낫다.

## i3lock이 시스템 절전 모드와 작동하도록 하기

아래의 유닛 파일을 추가해서 `# systemctl enable suspend@<user>.service`로 활성화하라.

 `/etc/systemd/system/suspend@.service` 
```
[Unit]
Description=Starts i3lock at suspend time
Before=sleep.target

[Service]
User=%I
Type=forking
Environment=DISPLAY=:0
ExecStartPre= 
ExecStart=/usr/bin/i3lock}}

[Install]
WantedBy=sleep.target
```

## 기타 도구

i3는 프로그램 실행기로 [dmenu](/index.php/Dmenu "Dmenu")를 사용하며 기본적으로 설정된 `Mod 키`+`d`를 눌러 이를 실행할 수 있다.

## 추가 자료

*   [타일링 창 관리자 비교](/index.php/Comparison_of_tiling_window_managers "Comparison of tiling window managers")
*   [공식 웹사이트](http://i3wm.org)
*   [소스 코드](http://code.stapelberg.de/git/i3)
*   [서비스 파일 시작/중단하기](/index.php/Systemd#Suspend.2Fresume_service_files "Systemd")

**아치 리눅스 포럼**

*   [*i3 게시글*](https://bbs.archlinux.org/viewtopic.php?id=99064) - 전반적인 i3 토론
*   [*i3 데스크톱 스크린샷 및 설정 공유*](https://bbs.archlinux.org/viewtopic.php?pid=1229978)