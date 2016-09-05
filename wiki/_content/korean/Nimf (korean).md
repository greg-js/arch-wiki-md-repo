[님프(Nimf)](https://github.com/cogniti/nimf)는 다국어 [입력기](https://en.wikipedia.org/wiki/Input_method "wikipedia:Input method") 프레임워크 이며, [다솜](/index.php/Dasom "Dasom")의 후속 프로젝트 입니다.

## Contents

*   [1 설치](#.EC.84.A4.EC.B9.98)
    *   [1.1 입력기 엔진](#.EC.9E.85.EB.A0.A5.EA.B8.B0_.EC.97.94.EC.A7.84)
    *   [1.2 초기 설정](#.EC.B4.88.EA.B8.B0_.EC.84.A4.EC.A0.95)
*   [2 설정 변경](#.EC.84.A4.EC.A0.95_.EB.B3.80.EA.B2.BD)
*   [3 더 보기](#.EB.8D.94_.EB.B3.B4.EA.B8.B0)

## 설치

[nimf-git](https://aur.archlinux.org/packages/nimf-git/) 패키지 하나만 [설치](/index.php/Install "Install") 하면 됩니다.

### 입력기 엔진

*   nimf-libhangul, [libhangul](https://www.archlinux.org/packages/?name=libhangul) 기반의 한국어 입력 엔진 ([nimf-git](https://aur.archlinux.org/packages/nimf-git/)에 내장되어 있음).
*   nimf-sunpinyin, [sunpinyin](https://www.archlinux.org/packages/?name=sunpinyin) 기반의 중국어 병음 입력 엔진 ([nimf-git](https://aur.archlinux.org/packages/nimf-git/)에 내장되어 있음).
*   nimf-anthy, [anthy](https://www.archlinux.org/packages/?name=anthy) 기반의 일본어 입력 엔진(개발중) ([nimf-git](https://aur.archlinux.org/packages/nimf-git/)에 내장되어 있음).
*   nimf-chewing, [libchewing](https://www.archlinux.org/packages/?name=libchewing) 기반의 중국어 주음 입력 엔진(개발중) ([nimf-git](https://aur.archlinux.org/packages/nimf-git/)에 내장되어 있음).
*   nimf-rime, [librime](https://www.archlinux.org/packages/?name=librime) 기반의 중국어 입력 엔진(개발중) ([nimf-git](https://aur.archlinux.org/packages/nimf-git/)에 내장되어 있음).

### 초기 설정

아래와 같은 내용을 데스크톱 시작 스크립트에 추가합니다.

*   KDM, GDM, LightDM 또는 SDDM 사용시, `.xprofile` 를 사용하세요.
*   startx 또는 Slim 사용시, `.xinitrc` 를 사용하세요.

```
export GTK_IM_MODULE=nimf
export QT4_IM_MODULE="nimf"
export QT_IM_MODULE=nimf
export XMODIFIERS="@im=nimf"
nimf-daemon
nimf-indicator

```

변경한 것이 적용되도록 하기 위해, 다시 로그인 합니다.

**참고:** GNOME 사용시, 님프를 사용하려면 아래와 같은 명령어를 실행해 주셔야 합니다.:
```
$ gsettings set org.gnome.settings-daemon.plugins.keyboard active false
$ gsettings set org.gnome.settings-daemon.plugins.xsettings overrides "{'Gtk/IMModule':<'nimf'>}"

```

## 설정 변경

님프 설정을 변경하려면, `nimf-settings` 를 사용하세요. 터미널에서 `nimf-settings` 를 실행 하거나, 시스템 트레이에 표시되는 님프 표시기를 클릭하면 나타나는 표시기 메뉴에서 `설정` 을 선택하여 실행하실 수 있습니다.

## 더 보기

*   [님프 깃허브](https://github.com/cogniti/nimf)