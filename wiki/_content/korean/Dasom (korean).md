[다솜(Dasom)](http://dasom-im.github.io)은 다국어 [입력기](https://en.wikipedia.org/wiki/Input_method "wikipedia:Input method") 프레임워크 입니다.

## Contents

*   [1 설치](#.EC.84.A4.EC.B9.98)
    *   [1.1 입력기 엔진](#.EC.9E.85.EB.A0.A5.EA.B8.B0_.EC.97.94.EC.A7.84)
    *   [1.2 초기 설정](#.EC.B4.88.EA.B8.B0_.EC.84.A4.EC.A0.95)
*   [2 더 보기](#.EB.8D.94_.EB.B3.B4.EA.B8.B0)

## 설치

[dasom-git](https://aur.archlinux.org/packages/dasom-git/)패키지를 [설치](/index.php/Install "Install") 하세요. 필요한 경우, 입력기 모듈 패키지를 추가적으로 설치하세요. GTK+ 응용프로그램에 대해서는 [dasom-gtk-git](https://aur.archlinux.org/packages/dasom-gtk-git/)를, Qt 응용프로그램에 대해서는 [dasom-gtk-git](https://aur.archlinux.org/packages/dasom-gtk-git/)를 설치합니다.

### 입력기 엔진

*   [dasom-jeongeum-git](https://aur.archlinux.org/packages/dasom-jeongeum-git/), [libhangul](https://www.archlinux.org/packages/?name=libhangul) 기반의 한국어 입력 엔진.

### 초기 설정

아래와 같은 내용을 데스크톱 시작 스크립트에 추가합니다.

*   KDM, GDM, LightDM 또는 SDDM 사용시, `.xprofile` 를 사용하세요.
*   startx 또는 Slim 사용시, `.xinitrc` 를 사용하세요.

```
export GTK_IM_MODULE=dasom
export QT_IM_MODULE=dasom
export XMODIFIERS="@im=dasom"
dasom-daemon
dasom-indicator

```

변경한 것이 적용되도록 하기 위해, 다시 로그인 합니다.

**참고:** GNOME 사용시, 다솜을 사용하려면 아래와 같은 명령어를 실행해 주셔야 합니다.:
```
$ gsettings set org.gnome.settings-daemon.plugins.keyboard active false
$ gsettings set org.gnome.settings-daemon.plugins.xsettings overrides "{'Gtk/IMModule':<'dasom'>}"

```

## 더 보기

*   [다솜 깃허브](https://github.com/dasom-im/dasom/)
*   [다솜 홈페이지](http://dasom-im.github.io)