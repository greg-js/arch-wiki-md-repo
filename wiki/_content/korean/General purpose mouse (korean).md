관련 항목

*   [Daemon](/index.php/Daemon "Daemon")

GPM(General Purpose Mouse)은 리눅스 가상 콘솔에서 마우스를 지원하는 데몬이다.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 설치하기](#설치하기)
    *   [1.1 데스코톱](#데스코톱)
    *   [1.2 노트북](#노트북)
*   [2 설정하기](#설정하기)

## 설치하기

### 데스코톱

[pacman](/index.php/Pacman "Pacman")으로 [gpm](https://www.archlinux.org/packages/?name=gpm)을 설치하라 .

### 노트북

[pacman](/index.php/Pacman "Pacman")으로 [gpm](https://www.archlinux.org/packages/?name=gpm)과 [xf86-input-synaptics](https://www.archlinux.org/packages/?name=xf86-input-synaptics)를 설치하라.

## 설정하기

The `-m` 매개변수는 사용할 마우스를 선언할 때 그 앞에 붙인다. `-t` 매개변수는 마우스 타입 앞에 붙인다. `-t` 옵션에서 사용할 마우스 타입 목록을 보려면 `gpm`을 `-t help`와 함께 실행하라.

```
$ gpm -m /dev/input/mice -t help

```

마우스 버튼이 두 개뿐이라면 `GPM_ARGS`에 `-2`를 지정해야 버튼 2가 붙여넣기 기능을 수행할 수 있다.

[gpm](https://www.archlinux.org/packages/?name=gpm) 꾸러미에는 필수 매개변수가 있다. 그 매개변수는 `/etc/conf.d/gpm`에 지정하거나 직접 `gpm`을 실행할 때 사용할 수 있다.

*   PS/2 마우스일 경우, 기존의 줄을 다음으로 변경하라.

```
GPM_ARGS="-m /dev/psaux -t ps2"

```

*   USB 마우스일 경우, 다음을 사용하라.

```
GPM_ARGS="-m /dev/input/mice -t imps2"

```

*   IBM 트랙포인트일 경우, 다음을 사용하라.

```
GPM_ARGS="-m /dev/input/mice -t ps2"

```

설정이 제대로 끝나면 `/etc/rc.conf`의 `DAEMONS` 배열에 `gpm`을 추가해야 부팅 시에 로드할 수 있다. 보기)

```
DAEMONS=(syslog-ng **gpm** network netfs crond)

```

더 자세한 사상은 [gpm(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/gpm.8)을 보라.