Related articles

*   [Internationalization](/index.php/Internationalization "Internationalization")
*   [Dasom](/index.php/Dasom "Dasom")
*   [IBus](/index.php/IBus "IBus")
*   [SCIM](/index.php/SCIM "SCIM")
*   [UIM](/index.php/UIM "UIM")
*   [Fcitx](/index.php/Fcitx "Fcitx")

[님프(Nimf)](https://nimf-i18n.gitlab.io/)는 다국어 [입력기](https://en.wikipedia.org/wiki/Input_method "wikipedia:Input method") 프레임워크 이며, [다솜](/index.php/Dasom "Dasom")의 후속 프로젝트 입니다.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 설치](#설치)
    *   [1.1 입력기 엔진](#입력기_엔진)
    *   [1.2 초기 설정](#초기_설정)
*   [2 설정 변경](#설정_변경)
*   [3 더 보기](#더_보기)

## 설치

[nimf](https://aur.archlinux.org/packages/nimf/) 패키지 하나만 [설치](/index.php/Install "Install") 하면 됩니다.

### 입력기 엔진

*   nimf-libhangul, [libhangul](https://www.archlinux.org/packages/?name=libhangul) 기반의 한국어 입력 엔진 ([nimf](https://aur.archlinux.org/packages/nimf/)에 내장되어 있음).
*   nimf-anthy, [anthy](https://www.archlinux.org/packages/?name=anthy) 기반의 일본어 입력 엔진 ([nimf](https://aur.archlinux.org/packages/nimf/)에 내장되어 있음).
*   nimf-chewing, [libchewing](https://www.archlinux.org/packages/?name=libchewing) 기반의 중국어 주음 입력 엔진 ([nimf](https://aur.archlinux.org/packages/nimf/)에 내장되어 있음).
*   nimf-rime, [librime](https://www.archlinux.org/packages/?name=librime) 기반의 중국어 입력 엔진 ([nimf](https://aur.archlinux.org/packages/nimf/)에 내장되어 있음).

### 초기 설정

아래와 같은 내용을 데스크톱 시작 스크립트에 추가합니다.

*   KDM, GDM, LightDM 또는 SDDM 사용시, `.xprofile` 를 사용하세요.
*   startx 또는 Slim 사용시, `.xinitrc` 를 사용하세요.

```
export GTK_IM_MODULE=nimf
export QT4_IM_MODULE="nimf"
export QT_IM_MODULE=nimf
export XMODIFIERS="@im=nimf"
nimf

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

*   [님프 깃랩](https://gitlab.com/nimf-i18n/nimf)