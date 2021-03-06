Related articles

*   [Arch packaging standards](/index.php/Arch_packaging_standards "Arch packaging standards")
*   [Arch User Repository](/index.php/Arch_User_Repository "Arch User Repository")
*   [Creating packages](/index.php/Creating_packages "Creating packages")
*   [Kernel Compilation with ABS](/index.php/Kernel_Compilation_with_ABS "Kernel Compilation with ABS")
*   [makepkg](/index.php/Makepkg "Makepkg")
*   [makepkg.conf](/index.php/Makepkg.conf "Makepkg.conf")
*   [pacman](/index.php/Pacman "Pacman")
*   [pacman Tips](/index.php/Pacman_Tips "Pacman Tips")
*   [PKGBUILD](/index.php/PKGBUILD "PKGBUILD")

이 문서는 초보자를 위한 빠른 설명과 함께 아치 빌드 시스템의 개요를 제공합니다. 이 문서의 내용은 완벽한 안내서가 아닙니다! 더 많은 정보가 필요하면, 맨 페이지를 참조 해주세요.

## Contents

*   [1 아치 빌드 시스템이란?](#아치_빌드_시스템이란?)
    *   [1.1 포트와 유사한(ports-like) 시스템이란?](#포트와_유사한(ports-like)_시스템이란?)
    *   [1.2 **ABS** 는 같은 개념입니다.](#ABS_는_같은_개념입니다.)
    *   [1.3 ABS 개요](#ABS_개요)
*   [2 ABS를 왜 사용하나요?](#ABS를_왜_사용하나요?)
*   [3 구성하기](#구성하기)
    *   [3.1 간략 내용](#간략_내용)
    *   [3.2 세부사항](#세부사항)
    *   [3.3 /etc/abs.conf](#/etc/abs.conf)
    *   [3.4 ABS 트리 다운로드](#ABS_트리_다운로드)
    *   [3.5 /etc/makepkg.conf](#/etc/makepkg.conf)
    *   [3.6 ABS 트리 구조](#ABS_트리_구조)
    *   [3.7 빌드 디렉토리 만들기](#빌드_디렉토리_만들기)
    *   [3.8 전통적인 빌드 방법](#전통적인_빌드_방법)
    *   [3.9 ABS를 이용한 패키지 빌드](#ABS를_이용한_패키지_빌드)

## 아치 빌드 시스템이란?

아치 빌드 시스템은 BSD의 포트와 유사한 소스코드로 부터 패키지를 만드는 시스템입니다. ABS (`.pkg.tar.gz` 패키지를 만들기 위한 전문적인 도구)를 통해 소스를 컴파일 후 [팩맨](/index.php/Pacman "Pacman")을 통해 바이너리 패키지를 관리(설치/삭제/업그레이드등)을 도와줍니다.

### 포트와 유사한(ports-like) 시스템이란?

'포트'시스템은 BSD*에서 소스 패키지를 다운로드 압축 해제, 패치, 컴파일하여 설치하는 사용됩니다. '포트'는 사용자의 컴퓨터에 디렉토리로 존재합니다. 이 작은 디렉토리는 해당 소프트웨어의 이름이 같으며, 일반적으로 디렉토리 안에는 소스와 응용 프로그램을 설치하기 위한 지침을 몇 가지 파일이 포함되어 있습니다. 이 시스템은 보다 쉽게 소스를 컴파일하고 원하는 소프트웨어 설치를 도와줍니다.

### **ABS** 는 같은 개념입니다.

ABS 는 `/var/abs` 아래에 ABS 라는 디렉토리 구조를 만듭니다. 이 구조에는 많은 하부 디렉토리와 각각의 패키들에 의해 명명되고 분류되어 있습니다. 이 구조는 SVN 시스템에 의해 복구되는 모든 *공식 아치 소프트웨어*를 표현 합니다.(내용을 담고 있지는 않습니다.) 'ABS'에서 각각의 패키지 명명화된 하부 디렉토리를 참조 할것이며, '포트'에서 참조하는것 보다 많은 방법을 사용 할것입니다. 이들 ABS (또는 하부 디렉토리들)은 소프트웨어 패키지 또는 소스를 포함하지 않지만 [PKGBUILD](/index.php/PKGBUILD "PKGBUILD") 화일(그리고 때로는 다른 화일들)을 포함합니다. PKGBUILD는 간결한 BASH 빌더 스크립터 입니다. -- 다운로드 할 수 있는 tar 묶음된 **소스**의 가장 적절한 URL로 구성된 컴파일 하기와 패키징 하기 정보를 담고 있는 텍스트 화일입니다. (ABS에서 가장 중요한 요소는 PKGBUILD입니다.) ABS [makepkg](/index.php/Makepkg "Makepkg")에 의해서 야기된 소프트웨어는 인스톨되기전에 빌더 디렉토리에서 먼저 컴파일되고 *패키지화* 됩니다. 이제 여러분은 아치 리눅스 패키지 매니저인 [pacman](/index.php/Pacman "Pacman")을 사용하여 새로운 패키지를 설치, 업데이트, 삭제 할 수 있습니다.

### ABS 개요

'ABS' 는 ABS를 포함해서 그 외 의존하는 여러가지 구성 요소를 총칭하는 용어로 사용할 수 있습니다. 따라서, 'ABS'는 다음과 같은 구조와 도구를 지칭 할 때도 사용 됩니다 :

	ABS 트리

	ABS 디렉토리 구조; 여러분의 (로컬) 머신에 SVN 계층구조와 같이 `/var/abs/` . 그것은 여러 하위 디렉토리의 지정된 저장소에 사용 가능한 모든 공식 아치 리눅스 소프트웨어가 포함되어 있습니다. `/etc/abs.conf`, 하지만 패키지 자체는 저장 되어 있지 않습니다.

	ABS 

	**공식**아치 리눅스의 PKGBUILDs 내용을 읽어서, 빌드. PKGBUILDs 예제도 포함되어있습니다.

	[PKGBUILDs](/index.php/PKGBUILD "PKGBUILD")

	ABS 디렉토리 아래에 존재하는 텍스트 파일로 만들어진 스크립트, 혹은 사용자가 정의한 스크립트, 필요한 파일이나 url, 빌드방법을 적어둔 지침

	[makepkg](/index.php/Makepkg "Makepkg")

	ABS 쉘 명령어 도구로 PKGBUILDs 읽고 소스를 자동으로 다운로드, 컴파일 및 `.pkg.tar.gz` 파일 생성

	[pacman](/index.php/Pacman "Pacman")

	pacman은 직접적인 연관은 없지만 makepkg나 수동으로 필요한 패키지를 설치, 제거, 의존성 해결을 위해서 필요 합니다.

	[AUR](/index.php/AUR "AUR")

	아치 사용자 저장소를 ABS에서 [AUR](/index.php/AUR "AUR") ([비공식]) 직접적으로 지원하지는 않지만 makepkg 도구를 통해서 PKGBUILDs 파일을 컴파일 및 패키지로 만들수 있습니다. AUR에는 16,000 이상의 아치 패키지로 만들수 있는 PKGBUILDs가 포함되어있습니다. 만약 공식적인 아치 트리에 포함되지 않은 패키지를 빌드해야 한다면 [AUR](/index.php/AUR "AUR") 을 이용하시면 됩니다.

## ABS를 왜 사용하나요?

아래와 같은 경우 아치 빌드 시스템을 사용합니다 :

*   어떤 이유로 인해서 패키지를 재컴파일 해야하는 경우
*   패키지가 없는 새로운 소프트웨어를 소스로부터 패키지를 생성 /설치시([Creating packages](/index.php/Creating_packages "Creating packages") 참고)
*   사용자 정의 패키지 (기존 패키지의 옵션을 활성화하거나 비활성화, 패치)
*   컴파일러 플래그를 지정하여 여러분의 전체 시스템을 재빌드 "a la FreeBSD"([pacbuilder](/index.php/Pacbuilder "Pacbuilder"))참고)
*   자신만의 사용자 정의 커널 설치 ([Custom Kernel Compilation with ABS](/index.php/Custom_Kernel_Compilation_with_ABS "Custom Kernel Compilation with ABS")와 [Kernel Compilation](/index.php/Kernel_Compilation "Kernel Compilation") 참고)
*   사용자 정의 커널과 커널 모듈 작업
*   새버전을 쉽게 컴파일하고, 베타 또는 아치 패키지의 개발 버전을 수정하여 원하는 버전 번호를 PKGBUILD에 적용 설치

ABS를 사용하기 위해서 아치리눅스를 사용할 필요는 없지만 소스를 컴파일하여 특정 작업을 자동화하는데 좀 더 편리하게 이용 가능합니다.

## 구성하기

pacman으로 설치 가능한 공식 저장소의 바이너리 패키지들은 **ABS 트리** 안에 PKGBUILD 이 제공되며 이를 이용해서 사용자 직접 소스를 컴파일, `.pkg.tar.gz` 파일 생성, 설치 가능합니다.

### 간략 내용

먼저 ABS 패키지를 설치합니다. `pacman -S abs`. `abs`를 루트 권한으로 실행하여서 아치 리눅스 서버로 부터 ABS 트리를 생성 및 동기화 시켜 줍니다. 만약 당신이 파일의 복사본을 만들어서 소스 패키지를 빌드하고 싶었다면 ( `/var/abs/<repo>/<pkgname>`) 와 같은 빌드 디렉토리의 PKGBUILD 을 편집(필요시), *makepkg **명령을 실행.** ***makepkg**은 PKGBUILD 지침에 따라 소스 tarball을 다운로드합니다. 그리고 압축 해제, 필요 시 패치, CFLAGS`makepkg.conf`에 따로 컴파일, 그리고 컴파일 된 패키지 파일은 `.pkg.tar.gz`으로 생성 됩니다. PKGBUILDs는 고유한 구성을 요구하거나, 사용자 정의 패치를 정의할 수있습니다. 설치는 단지 `pacman -U <.pkg.tar.gz file>`를 입력해주면 됩니다. 패키지 제거도 팩맨에 의해 처리됩니다.

또한 makepkg는 [AUR](/index.php/AUR "AUR") 이나 써드파티 소스로 자신만의 패키지를 만들 수 있습니다 . ([Creating packages](/index.php/Creating_packages "Creating packages") 위키 문서 참고.)

### 세부사항

abs를 사용하기 위해서는 먼저 [core] 저장소에 있는 **abs** 패키지를 설치 해야합니다.단지 아래 명령을 실행하면 설치 됩니다:

```
# pacman -S abs

```

이것은 abs-sync 스크립트, 기타 다양한 스크립트, [rsync](/index.php/Rsync "Rsync") 를 구성 해줍니다. (필요 패키지가 없을시 의존성으로 추가 설치 필요).

또한 실제 패키지 빌드를 위해서는 기본적인 컴파일 도구가 필요 합니다. 이러한 패키지는 **base-devel** 그룹 패키지에 모여 있습니다. 이 그룹 패키지는 아래와 같이 설치 할 수 있습니다 :

```
# pacman -S base-devel

```

**Warning:** (make)의존성이 누락되었다고 불평하기전에 기억하세요. 이 내용은 "base"와 "base-devel" 그룹 패키지가 설치되어 있는 시스템을 가정으로 설명하고 있습니다.

### `/etc/abs.conf`

`/etc/abs.conf`을 root 계정으로 원하는 저장소를 포함하게 수정:

```
# vim /etc/abs.conf

```

or:

```
# nano /etc/abs.conf

```

원하는 저장소 앞에 붙어있는 ! 를 제거 해주세요 :

```
REPOS=(core extra community !testing)

```

### ABS 트리 다운로드

root 로 실행:

```
# abs

```

당신의 ABS 트리는 `/var/abs` 아래 생성 됩니다. ABS 트리에 대한 세부설정은 `/etc/abs.conf` 파일 안에 존재합니다.

만약 당신이 활발한 개발자라면, 주기적으로 abs 명령을 통해서 공식 저장소와 동기화 시켜야합니다. 보통의 개발자라면 특정 ABS 패키지만 다운로드 할 수 있습니다 :

```
# abs 저장소/패키지명

```

### `/etc/makepkg.conf`

`/etc/makepkg.conf` 특정한 글로벌 설정 값과 컴파일러 플래그를 지정합니다.SMP 시스템 또는 기타 원하는 최적화를 지정할 수있습니다. 기본 설정은 싱글의 i686와 x86_64 CPU 시스템에서 잘 작동합니다. (SMP 시스템에서도 문제 없이 작동하지만 컴파일 시 하나의 코어/CPU만 사용합니다.자세한 내용은 [makepkg.conf](/index.php/Makepkg.conf "Makepkg.conf") 참고하세요.)

### ABS 트리 구조

처음으로 `abs` 를 실행하면 아치리눅스 서버로 부터 ABS 트리를 동기화 합니다. ABS 트리는 SVN 디렉토리 구조와 같이 로컬 시스템 `/var/abs` 에 아래처럼 생성 됩니다 :

```
| -- core/
|     || -- base/
|     ||     || -- acl/
|     ||     ||     || -- PKGBUILD
|     ||     || -- attr/
|     ||     ||     || -- PKGBUILD
|     ||     || -- ...
|     || -- devel/
|     ||     || -- abs/
|     ||     ||     || -- PKGBUILD
|     ||     || -- autoconf/
|     ||     ||     || -- PKGBUILD
|     ||     || -- ...
|     || -- ...
| -- extra/
|     || -- daemons/
|     ||     || -- acpid/
|     ||     ||     || -- PKGBUILD
|     ||     ||     || -- ...
|     ||     || -- apache/
|     ||     ||     || -- ...
|     ||     || -- ...
|     || -- ...
| -- community/
|     || -- ...

```

ABS 트리는 패키지 데이터베이스 구조와 동일한 구조를 하고 있습니다 :

*   레벨 1 : 카탈로그 디렉토리
*   레벨 2 : 패키지 이름 디렉토리
*   레벨 3 : PKGBUILD (패키지를 만드는데 필요한 정보) 및 기타 관련 파일 (패치, 기타 패키지 빌드 시 필요 파일)

ABS 디렉토리에는 패키지의 소스 코드는 존재 하지 않습니다. 대신, **PKGBUILD**파일에 포함된 URL주소의 소스 코드 를 다운로드합니다.

### 빌드 디렉토리 만들기

당신이 실제 컴파일에 사용될 디렉토리를 만들어야합니다. 이 디렉토리에서 모든것을 할 수 있습니다; ABS 트리에서 내용을 수정정/빌드 하면, ABS 업데이트 시 수정내용을 잃어버리게(덮어쓰기) 됩니다. 좋은 방법은 일반 사용자 계정 홈 디렉토리 밑에 `/var/abs/` 디렉토리를 생성하는 것입니다. ABS 트리 (`/var/abs/branch/category-/pkgname`) 에서 빌드 디렉토리 `/path/to/build/dir`로 복사합니다.

개인 빌드 디렉토리 만들기 e.g.:

```
$ mkdir -p $HOME/abs

```

**Note:** 처음 abs 다운로드 시 많은 시간이 필요하지만, 이 후에는 변화된 부분만 다운로드 될 것입니다. 당신의 유일한 인터넷 연결방법이 56k 모뎀이라도 겁내지 마세요; 단지 압축된 텍스트 파일입니다. 예를 들면, 2009년 11월 24일의 core, extra, community 저장소 abs 트리의 용량은 ~16MB 입니다. (압축 해제시 ~56MB 디스크 용량.)

### 전통적인 빌드 방법

만약 당신이 패키지 빌드에 익숙하지 않다면, **일반적인** 소스 컴파일 방법을 사용 가능합니다 :

*   원격 서버로 부터 소스 tar 파일을 웹브라우저, ftp, wget 등으로 다운로드 합니다.

*   소스 파일 압축 해제:

```
$ tar -xzf foo-0.99.tar.gz

```

나

```
$ tar -xjf foo-0.99.tar.bz2

```

*   디렉토리 이동:

```
$ cd foo-0.99

```

*   패키지 구성. 일반적으로 `configure` 스크립트 파일을 실행하여 구성합니다. 이 파일은 소스 디렉토리 안에 포함 되어있습니다. 옵션(여러가지 지원 옵션을 추가 나 삭제, 설치 디렉토리, 기타) 과 빌드시 필요한 패키지가 시스템에 설치 되어있는지 검사 해줍니다. 아래와 같이 실행 해주세요:

```
$ ./configure [옵션]

```

옵션이나 사용법을 알고 싶으면 아래와 같이 명령을 실행합니다:

```
$ ./configure --help

```

만약 `--prefix` 옵션을 스크립트 실행 시 추가 하지 않으면, *대부분* 스크립트는 `/usr/local` 을 설치 패스로 사용하며, 그외에는 `/usr`를 사용합니다. 일관성을 위해서 일반적으로 `--prefix=/usr/local` 옵션을 사용합니다. 좋은 설치 습관은 개인적은 프로그램은 `/usr/local`에 설치하며, 배포판에서 관리되는 프로그램은 `/usr`에 설치합니다. 이렇게 개인화된 프로그램 버전도 배포판 패키지 매니저로 같이 관리 할수 있습니다. -- 아치리눅스의 경우에는 *pacman*.

```
$ ./configure --prefix=/usr/local

```

*   소스 컴파일:

```
$ make

```

*   인스톨:

```
# make install

```

*   설치된 파일을 삭제 시 소스 디렉토리로 이동 후 실행:

```
# make uninstall

```

하지만 당신은 항상 `INSTALL` 파일의 패키지 빌드와 설치 방법을 읽어야합니다! **모든 패키지가 `configure; make; make install`를 사용해서 패키지를 생성하지는 않기 때문이죠**

**Note:** 위와 같이 소스를 간단히 tar 압축해제, 컴파일하는 전통적인 방법은 물론, 아치 리눅스에서 사용할 수있습니다. 하지만, 설치된 파일이 파일 시스템 전역에 흩어져 설치 될수 있고, 팩맨(혹은 기타 패키지 매니저)으로 관리가 불가능합니다. 만약, 패키지 관리자를 이용한 설치가 아치 리눅스에 문제를 발생 시키거나 설치된 파일들을 모두 파악하고 있을경우에만 사용 해야합니다.

### ABS를 이용한 패키지 빌드

ABS는 강력한 지원 및 사용자 지정 프로세스를 구축하고 *pacman-trackable*(팩맨이 추적가능한) 패키지 파일을 생성하기 위한 우아한 빌드 도구입니다. ABS를 이용한 방법에는 ABS트리에서 파일을 복사, makepkg를 이용한 패키징하는 것을 포함합니다. 예를 들면 *slim* 디스플레이 매니저 패키지 방법을 보겠습니다.

먼저 ABS로 부터 ABS 트리를 빌드 디렉토리로 복사합니다:

```
$ cp -r /var/abs/extra/slim/ ~/abs

```

빌드 디렉토리로 이동:

```
$ cd ~/abs/slim

```

PKGBUILD 파일을 수정, 추가, 삭제, 패치등 구성요소를 조정합니다 (패키지 버전등 기타, 공식 패키지와 같이 사용시 수정 안해도 됩니다):

```
$ nano PKGBUILD

```

일반 사용자로 makepkg 을 실행 (`-s` 옵션을 같이 사용시 의존성을 자동으로 처리합니다):

```
$ makepkg -s

```

root 사용자로 패키지 설치:

```
# pacman -U slim-1.3.0-2-i686.pkg.tar.gz

```

어때요 참 쉽죠? 팩맨을 이용해서 빌드한 패키지를 설치, 삭제가 가능합니다. 패키지를 삭제할 때에는 {{Ic|pacman -R slim} 명령을 이용합니다.

기본적으로, 빌드과정(일반적으로 `./configure, make, make install` 과정)은 *fake root* 환경에서 실행 됩니다. (페이크 루트는 가상의 루트 디렉토리 내에 하위 디렉토리를 구축하고 가상 루트 디렉토리를 실제 루트 디렉토리 처럼 인식, 작동하게 합니다. ) ***fakeroot** *프로그램과 함께, makepkg 가 fake root 디렉토리를 생성하고 그곳에 컴파일된 바이너리 및 관련 파일을 **root** 권한으로 생성 합니다.) 컴파일된 소프트웨어 패키지는 `.pkg.tar.gz` 확장자를 가지거나 *package*로 생성 됩니다. 생성된 패키지 파일을 팩맨을 이용해서 설치를 하면 실제 루트 디렉토리에 설치됩니다. (`/`).

*ABS를 이용하면 편의성, 자동화, 컴파일된 패키지의 투명성, 기타 설치 과정을 PKGBUILD파일을 통해 사용 가능합니다.*