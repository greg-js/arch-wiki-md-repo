## Contents

*   [1 소개](#.EC.86.8C.EA.B0.9C)
*   [2 시스템](#.EC.8B.9C.EC.8A.A4.ED.85.9C)
*   [3 부분 적용](#.EB.B6.80.EB.B6.84_.EC.A0.81.EC.9A.A9)
    *   [3.1 X 환경](#X_.ED.99.98.EA.B2.BD)
    *   [3.2 콘솔 환경](#.EC.BD.98.EC.86.94_.ED.99.98.EA.B2.BD)
    *   [3.3 ALSA 이용](#ALSA_.EC.9D.B4.EC.9A.A9)
    *   [3.4 그놈/Metacity 환경](#.EA.B7.B8.EB.86.88.2FMetacity_.ED.99.98.EA.B2.BD)
*   [4 같이 보기](#.EA.B0.99.EC.9D.B4_.EB.B3.B4.EA.B8.B0)

## 소개

컴퓨터는 비프음이나 기타 소리를 우리가 원하든 원하지 않든 다양한 때에 낸다. 소리의 원인은 여러 가지이며 그 특성에 따라 소리가 날지 언제 날지를 설정할 수도 있다. 게다가 컴퓨터 소리는 내장 스피커나 사운드 카드에 연결된 스피커로 들을 수 있다. 이 문서는 주로 전자의 경우를 다룬다.

소리는 바이오스(기본 입출력 시스템), OS (운영체제), DE (데스트탑 환경) 또는 여러 소프트웨어에서 난다. 바이오스는 마더보드의 EPROM 칩에 저장되어 있기 때문에 특히 문제가 되며 사용자가 그것을 제어하는 유일한 방법은 시스템을 켜거나 끄는 것이다. 바이오스 설정에서 조정할 수 없거나 적당한 광원으로 그 칩용 프로그램을 다시 짜지 않는다면 바이오스를 바꾸기가 불가능하다. 바이오스가 내는 비프음은 여기서 다루지 않는다. 다만, 내장 스피커를 분리하면 그러한 소리는 안 들리지만 위험을 각오하고 그렇게 하라.

그러나 내장 스피커에서 나는 그 밖의 모든 소리는 다음의 방법을 사용해 제어할 수 있다.

특정한 소리를 끄고 나머지는 켜 둔 상태에서 어떤 소리가 나면 그 소리가 어디서 나는지 확인할 수 있음을 명심해야 한다. 이렇게 하면 주의를 끄는 소리를 선택할 수 있다. 다른 사용자에게 유용한 설정 조합을 발견하면 여기 문서에 자유롭게 추가하라.

## 시스템

PC speaker는 `pcspkr` 모듈을 [제거](/index.php/Kernel_modules#Removal "Kernel modules")하여 끌 수 있다.

```
# rmmod pcspkr

```

`pcspkr` 모듈을 [블랙리스팅](/index.php/Kernel_modules#Blacklisting "Kernel modules")하여 부팅 시에 [udev](/index.php/Udev "Udev")가 그것을 불러들이지 못하게 한다.

## 부분 적용

### X 환경

```
$ xset -b

```

이 명령을 [xprofile](/index.php/Xprofile "Xprofile")와 같은 시작 파일에 추가하여 이 설정을 유지할 수 있다.

### 콘솔 환경

다음의 명령을 `/etc/profile` 또는 `/etc/profile.d/disable-beep.sh`와 같은 전용 파일 (반드시 실행 가능해야 함)에 추가할 수 있다:

```
setterm -blength 0

```

또 다른 방법은 다음을 `/etc/inputrc`나 `~/.inputrc`에 추가하거나 주석 표시를 제거하는 것이다:

```
set bell-style none

```

### ALSA 이용

PC 스피커 소리 끄기:

```
$ amixer set 'PC Speaker' 0% mute

```

일부 사운드 카드에서는 PC 비프음을 사용:

```
$ amixer set 'PC Beep' 0% mute

```

또는 그냥 비프음:

```
$ amixer set 'Beep' 0% mute

```

콘솔 GUI용 alsamixer를 사용할 수 있다.

```
$ alsamixer

```

PC 비프음을 선택해 'M'을 눌러 소리를 끄고 설정을 저장한다:

```
# alsactl store

```

이 방법이 작동하려면 `alsa`가 `/etc/rc.conf`의 [`DAEMONS` 배열](/index.php/Rc.conf#Daemons "Rc.conf")에 있어야 한다.

**참고:** 모든 사운드 카드가 alsamixer에 PC 스피커나 PC 비프음 슬라이더 제어기를 제공하지는 않는다.

### 그놈/Metacity 환경

Gconf에서 **`/apps/metacity/general/audible_bell`**를 **`false`**로 설정한다.

```
$ gconftool-2 -s -t string /apps/metacity/general/audible_bell false

```

## 같이 보기

*   더 자세한 사항은 다음의 `man` 문서를 참고하라: `xset(1)`, `setterm(1)`, `readline(3)`
*   [Kernel modules](/index.php/Kernel_modules "Kernel modules")