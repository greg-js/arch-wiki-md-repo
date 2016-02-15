[Subtle 프로젝트 사이트](http://subforge.org/projects/subtle) 인용:

	_Subtle은 기존 타일링 창 관리자와 달리 수동 타일링 창 관리자이다. 그러므로 사전에 정의된 배치를 사용하는 대신에 화면을 그래버티라고 하는 사용자 정의 구역으로 나눈다._

Subtle은 [Xorg](/index.php/Xorg "Xorg")용 [Ruby](/index.php/Ruby "Ruby")를 사용해서 설정한다.

**참고:** 여기서는 Subtle의 기본적인 부분만 설명한다. 더 상세한 정보와 설명서는 [Subtle 프로젝트 사이트](http://subforge.org/projects/subtle)에서 볼 수 있다.

## Contents

*   [1 설치하기](#.EC.84.A4.EC.B9.98.ED.95.98.EA.B8.B0)
*   [2 Subtle 실행하기](#Subtle_.EC.8B.A4.ED.96.89.ED.95.98.EA.B8.B0)
*   [3 기본 기능](#.EA.B8.B0.EB.B3.B8_.EA.B8.B0.EB.8A.A5)
*   [4 설정](#.EC.84.A4.EC.A0.95)
*   [5 Sublet](#Sublet)
    *   [5.1 sublet 설치하기](#sublet_.EC.84.A4.EC.B9.98.ED.95.98.EA.B8.B0)
    *   [5.2 sublets 활성화하기](#sublets_.ED.99.9C.EC.84.B1.ED.99.94.ED.95.98.EA.B8.B0)
*   [6 같이 보기](#.EA.B0.99.EC.9D.B4_.EB.B3.B4.EA.B8.B0)

## 설치하기

[공식 저장소](/index.php/Official_repositories "Official repositories")에서 [subtle](https://aur.archlinux.org/packages/subtle/) 꾸러미를 다음과 같이 설치한다.

```
# pacman -S subtle

```

개발자 버전을 설치하려면 [AUR](/index.php/AUR "AUR")에서 [subtle-hg](https://aur.archlinux.org/packages/subtle-hg/)를 설치하라.

## Subtle 실행하기

Subtle을 실행하려면 `exec subtle`을 `.xinitrc`에 추가하고 Xorg를 실행하라. 단, 다음을 명심하라. Subtle은 어떤 아이콘이나 메뉴를 제공하지 않고 단지 터미널을 실행하는 키 연결 `Super+Enter`만 제공하여 [Urxvt](/index.php/Urxvt "Urxvt")를 열 수 있다. 따라서 Urxvt가 없다면 설치하거나 시작하기에 앞서 설정 파일을 수정하라. Subtle을 종료하려면 `Super+Ctrl+q`를 눌러라.

## 기본 기능

창이 열릴 때 사전 정의된 규칙에 따라 알맞은 위치와 크기가 정해진다. 이 규칙을 적용할 때 다음의 세 가지 부분을 고려한다.

*   View
*   Gravity
*   Tag

_Views_란 창이 놓이는 환경을 말한다. 상당 부분 일반적인 데스크톱 화면과 유사하다. _tag_에서 실제 규칙을 정의한다. 사용할 _gravity_ 또한 태그에서 결정된다. 그래버티는 창의 크기와 위치를 제어한다.

**참고:** Subtle을 설정할 때 실제로 이 요소를 역순으로 정의해야 한다. 곧, Gravity, tag, view 순이다.

## 설정

Subtle은 $XDG_CONFIG_HOME 경로에서 `subtle.rb`를 찾는다. 그 파일이 없다면 $XDG_CONFIG_DIRS에서 기본 파일을 로드할 것이다. 기본 설정 파일을 사용하기 보다는 이 파일을 `$XDG_CONFIG_HOME/subtle` 디렉토리에 복사해서 사용하는 게 바람직하다.

기본 파일엣는 많은 gravities, tags, views가 있다. 이 파일은 자신의 환경을 처음 구축할 때 사용하기에 아주 좋다. 일치하는 태그가 없는 프로그램은 기본 태그가 있는 뷰에 나타난다. 어떤 뷰에도 기본 태그가 없다면 자동적으로 첫 번째 뷰에 나타날 것이다.

자신의 설정 파일에서 잠재적 오류를 검사하려면 다음 명령어를 실행하라.

```
$ subtle -k

```

## Sublet

Sublet은 Subtle 패널에 나타나는 작은 프로그램으로 다양한 프로그램을 제어하고 시스템 정보를 표시한다.

### sublet 설치하기

sublet을 설치하려면 터미널에서 다음을 실행하라.

```
$ sur install <name of sublet>

```

sublet 목록을 보려면 [sur 웹사이트](http://sur.subforge.org)를 보라.

**참고:** 루트 사용자로 sublet을 설치하면 일반 사용자는 그 sublet을 실행할 수 없다. 일반 사용자가 사용할 sublet은 일반사용자로 설치해야 한다.

### sublets 활성화하기

sublet을 설치한 후에 `subtle.rb`에서 그것을 활성화해야 한다. 다음과 유사한 줄을 찾아라.

```
screen 1 do
 top [ :title, :spacer, :views ]
 bottom [ :mpd, :wifi, :battery ]
end

```

그리고 다음과 같이 다른 sublet과 같은 방식으로 sublet을 추가하라.

```
 bottom [ :mpd,  :<name of sublet>, :wifi, :battery ]

```

물론, 위치는 자신이 고를 수 있다.

## 같이 보기

*   [Subtle 프로젝트 사이트](http://subforge.org/projects/subtle)
*   [Sublets archive](http://sur.subforge.org)
*   [subtle 게시글](https://bbs.archlinux.org/viewtopic.php?id=71783)
*   [Subtle 환경 공유하기!](https://bbs.archlinux.org/viewtopic.php?id=112486)
*   [xinitrc](/index.php/Xinitrc "Xinitrc")
*   [Start X at login](/index.php/Start_X_at_login "Start X at login")
*   [Window manager](/index.php/Window_manager "Window manager")