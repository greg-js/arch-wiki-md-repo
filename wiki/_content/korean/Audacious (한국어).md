**오데이셔스**(Audacious)는 GTK+에 기초한 고급 오디오 재생기이다. 오디오 품질에 중점을 두며 다양한 오디오 코덱을 지원하고 외부 플러그인으로 쉽게 기능을 확장할 수 있다.

## Contents

*   [1 설치](#.EC.84.A4.EC.B9.98)
*   [2 환경 설정](#.ED.99.98.EA.B2.BD_.EC.84.A4.EC.A0.95)
    *   [2.1 인터페이스](#.EC.9D.B8.ED.84.B0.ED.8E.98.EC.9D.B4.EC.8A.A4)
        *   [2.1.1 윈앰프(winamp) 스킨 추가하기](#.EC.9C.88.EC.95.B0.ED.94.84.28winamp.29_.EC.8A.A4.ED.82.A8_.EC.B6.94.EA.B0.80.ED.95.98.EA.B8.B0)
    *   [2.2 오디오 CD 재생하기](#.EC.98.A4.EB.94.94.EC.98.A4_CD_.EC.9E.AC.EC.83.9D.ED.95.98.EA.B8.B0)
*   [3 유용한 정보](#.EC.9C.A0.EC.9A.A9.ED.95.9C_.EC.A0.95.EB.B3.B4)
    *   [3.1 Audtool](#Audtool)
    *   [3.2 MP3 문제](#MP3_.EB.AC.B8.EC.A0.9C)
*   [4 바깥 고리](#.EB.B0.94.EA.B9.A5_.EA.B3.A0.EB.A6.AC)

## 설치

[audacious](https://www.archlinux.org/packages/?name=audacious)는 공식 저장소에 있으므로 [pacman](/index.php/Pacman "Pacman")으로 설치한다.

```
# pacman -S audacious

```

## 환경 설정

### 인터페이스

**참고:** GTK+가 오데이셔스 2.4 이상에서 기본 인터페이스이다.

오데이셔스는 현재 두 가지 인터페이스를 제공한다.

*   윈앰프 고전 인터페이스
*   GTK 인터페이스

두 인터페이스를 서로 전환할 수 있다.

#### 윈앰프(winamp) 스킨 추가하기

방법은 아주 쉽다. 스킨 파일(.zip, .wsz, .tgz, .tar.gz, .tar.bz2)을 `~/.local/share/audacious/Skins`(자신에게만 적용할 경우)이나 `/usr/share/audacious/Skins`(전체 사용자에게 적용할 경우)에 복사한다. 그러고 나서 **Preferences**의 **Skinned Interface**탭에서 그것을 찾아서 선택한다.

### 오디오 CD 재생하기

먼저 "libcdio"를 설치한다.

```
# pacman -S libcdio

```

이제 audacious에서 오디오 CD를 재생할 수 있다.

## 유용한 정보

### Audtool

오데이셔스에는 Audtool이라는 강력한 관리 도구가 있다. Audtool은 정보를 가져오거나 재생기를 제어하는 데 사용한다.

예를 들면, 듣고 있는 노래 제목이나 음악가를 알고 싶으면 다음 명령어를 실행한다.

```
$ audtool current-song
$ audtool current-song-tuple-data artist

```

또한 재생기를 제어하고 재생 목록, 이퀄라이저 및 프로그램 창을 조작하는 기능도 있다. 더 자세한 정보를 보려면 다음을 실행한다.

```
$ audtool --help

```

### MP3 문제

"mpg123"를 설치해 본다.

```
# pacman -S mpg123

```

## 바깥 고리

*   [Audacious 공식 웹사이트](http://audacious-media-player.org/)