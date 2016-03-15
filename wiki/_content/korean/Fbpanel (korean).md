fbpanel은 가벼운 NETWM 호환 데스크톱 패널이다. 이 문서에서는 fbpanel을 설치하고 설정하는 방법을 설명한다.

## Contents

*   [1 설치하기](#.EC.84.A4.EC.B9.98.ED.95.98.EA.B8.B0)
*   [2 시작하기](#.EC.8B.9C.EC.9E.91.ED.95.98.EA.B8.B0)
*   [3 설정하기](#.EC.84.A4.EC.A0.95.ED.95.98.EA.B8.B0)
*   [4 문제해결](#.EB.AC.B8.EC.A0.9C.ED.95.B4.EA.B2.B0)
    *   [4.1 wincmd 플러그인 (데스크톱 보기 버튼)](#wincmd_.ED.94.8C.EB.9F.AC.EA.B7.B8.EC.9D.B8_.28.EB.8D.B0.EC.8A.A4.ED.81.AC.ED.86.B1_.EB.B3.B4.EA.B8.B0_.EB.B2.84.ED.8A.BC.29)
    *   [4.2 fbpanel이 트레이에 나타나지 않을 경우](#fbpanel.EC.9D.B4_.ED.8A.B8.EB.A0.88.EC.9D.B4.EC.97.90_.EB.82.98.ED.83.80.EB.82.98.EC.A7.80_.EC.95.8A.EC.9D.84_.EA.B2.BD.EC.9A.B0)
*   [5 같이 보기](#.EA.B0.99.EC.9D.B4_.EB.B3.B4.EA.B8.B0)

## 설치하기

[공식 저장소](/index.php/Official_repositories "Official repositories")에서 [fbpanel](https://www.archlinux.org/packages/?name=fbpanel) 꾸러미를 [설치](/index.php/Pacman "Pacman")하라.

## 시작하기

fbpanel을 X 세션 시작 시에 실행하려면 .xinitrc 파일에 다음을 창 관리자 실행 줄 이전에 추가하라.

```
fbpanel &

```

## 설정하기

`~/.config/fbpanel`에 설정 파일이 있다.

없다면 기본 설정 파일을 다음과 같이 복사하라

```
# mkdir ~/.config/fbpanel
# cp /usr/share/fbpanel/default ~/.config/fbpanel

```

## 문제해결

### wincmd 플러그인 (데스크톱 보기 버튼)

이 플러그인은 기본적으로 활성화되지만 기본 아이콘을 찾지 못하면 나타나지 않을 것이다. 그런 경우에는 시스템에 있는 아이콘을 가리키도록 아이콘 경로를 수정하라. 또한 아이콘 대신에 이미지를 사용할 수도 있다. 이 때에는 다음처럼 "icon"을 "image"로 대체하라.

```
Plugin {
   type = wincmd
   config {
       image = ~/images/my_image.png
       tooltip = 왼쪽 클릭하면 모든 창을 아이콘화한다. 가운데 클릭하면 모든 창을 숨긴다.
   }
}

```

### fbpanel이 트레이에 나타나지 않을 경우

플러그인이 없을 경우로 fbpanel을 터미널에서 실행해 해당 플러그인을 확인하여 그 플러그인을 주석 처리하라.

## 같이 보기

*   [공식 웹사이트](http://fbpanel.sourceforge.net/)