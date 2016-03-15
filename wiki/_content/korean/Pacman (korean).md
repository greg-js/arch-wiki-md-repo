## Contents

*   [1 개요](#.EA.B0.9C.EC.9A.94)
*   [2 사용법](#.EC.82.AC.EC.9A.A9.EB.B2.95)
    *   [2.1 설치 및 삭제](#.EC.84.A4.EC.B9.98_.EB.B0.8F_.EC.82.AD.EC.A0.9C)
    *   [2.2 시스템 갱신](#.EC.8B.9C.EC.8A.A4.ED.85.9C_.EA.B0.B1.EC.8B.A0)
    *   [2.3 꾸러미 질의](#.EA.BE.B8.EB.9F.AC.EB.AF.B8_.EC.A7.88.EC.9D.98)
    *   [2.4 다른 사용법](#.EB.8B.A4.EB.A5.B8_.EC.82.AC.EC.9A.A9.EB.B2.95)
*   [3 설정](#.EC.84.A4.EC.A0.95)
    *   [3.1 기본 옵션](#.EA.B8.B0.EB.B3.B8_.EC.98.B5.EC.85.98)
    *   [3.2 저장소](#.EC.A0.80.EC.9E.A5.EC.86.8C)
*   [4 연관 고리](#.EC.97.B0.EA.B4.80_.EA.B3.A0.EB.A6.AC)

## 개요

**pacman** [꾸러미 관리자](https://en.wikipedia.org/wiki/Package_manager "wikipedia:Package manager")(패키지 매니저)는 아치 리눅스만의 개성있는 주 기능 중 하나입니다. 이진 꾸러미(바이너리 패키지) 형식과 사용하기 쉬운 [빌드 시스템](/index.php/Arch_Build_System_(%ED%95%9C%EA%B5%AD%EC%96%B4) "Arch Build System (한국어)")으로 이루어져 있습니다. *pacman*은 [아치 공식 저장소](/index.php/Official_repositories "Official repositories")나 사용자가 직접 만든 꾸러미 등을 쉽게 관리하도록 해줍니다.

*pacman*은 꾸러미 목록과 마스터 서버를 동기화해 가장 최신의 시스템을 유지합니다. 게다가 이 서버 및 클라이언트 모델은 간단한 명령으로 사용자에게 꾸러미와 필요한 의존성 꾸러미까지 같이 내려받고 설치도 해줍니다!

*pacman*은 C로 짜여졌으며 *.pkg.tar.xz* 형식의 패키지를 씁니다.

**Tip:** 아치 공식 [pacman](https://www.archlinux.org/packages/?name=pacman) 꾸러미에는 **makepkg**, **pactree**, **vercmp**, [checkupdates](#Partial_upgrades_are_unsupported) 같이 자주 쓰는 도구들도 포함되어 있어요. `pacman -Ql pacman | grep bin`를 실행하면 모든 도구들을 목록으로 볼 수 있습니다.

## 사용법

모르는 것이 있다면 `man pacman`를 읽어보도록 하자.

### 설치 및 삭제

설치와 삭제에 앞서 로컬 꾸러미 DB와 원격 저장소를 동기화 시킬 필요성이 있다.

```
pacman -Sy

```

또는

```
pacman --sync --refresh

```

하나의 꾸러미 또는 그 이상의 리스트 (여기에는 의존성에 의한 딸림-꾸러미 포함) 에 대한 설치 또는 판올림 명령은 다음과 같다.

```
pacman -S 꾸러미_이름1 꾸러미_이름2

```

다른 저장소에 있는 꾸러미를 원한다면 (예를들어 extra나 testing), 다음 처럼 기술한다.

```
pacman -S extra/꾸러미_이름
pacman -S testing/꾸러미_이름

```

꾸러미 설치 전 로컬 꾸러미 DB에 대한 새로 고침:

```
pacman -S 꾸러미_이름

```

찌꺼기를 남기는, 꾸러미 하나에 대한 삭제

```
pacman -R 꾸러미_이름

```

설치된 다른 꾸러미가 사용하지 않는 의존적인 꾸러미들의 모든 삭제:

```
pacman -Rs 꾸러미_이름

```

의존성 검사 없이 꾸러미 삭제

```
pacman -Rd 꾸러미_이름

```

### 시스템 갱신

**Pacman**은 단 하나의 명령으로 모든 꾸러미들의 판올림이 가능하다. (완전 자동)

```
pacman -Su

```

다음은, 저장소에 대한 동기화와 동시에 시스템에 대한 판올림을 해준다:

```
pacman -Syu

```

### 꾸러미 질의

**Pacman**은 꾸러미 목록에 대한 꾸러미 DB 검색이 가능하며, 꾸러미 이름의 일부분이라도 일치되는 글자열을 가진 모든 꾸러미들을 검색할 수 있다.

```
pacman -Ss 꾸러미

```

설치된 꾸러미 찾기:

```
pacman -Qs 꾸러미

```

꾸러미 이름을 알고 있다면, 꾸러미에 대한 정보를 찾아 볼 수 있다. 첨언하자면, *query info* (-Qi) 는 *sync info* (-Si) 보다 설치된 꾸러미에 한해서 조금 더 많은 정보를 보여주며, 미설치된 꾸러미 정보는 볼 수 없다.

```
pacman -Si 꾸러미
pacman -Qi 꾸러미

```

꾸러미에 적재된 파일리스트:

```
pacman -Ql 꾸러미

```

현재 설치된 꾸러미 가운데 사용되지 않는 파일 리스트:

```
pacman -Qe 

```

또, 시스템에 존재하는 꾸러미 파일을 찾을 수 있다.

```
pacman -Qo /패스/경로/파일

```

### 다른 사용법

*   설치 없이 꾸러미 내려받기:

```
pacman -Sw 꾸러미_이름

```

*   로컬 꾸러미 설치 (저장소 아님):

```
pacman -U /패스/경로/꾸러미/꾸러미_이름-버젼.pkg.tar.gz

```

*   꾸러미 캐쉬를 몽땅 버리기 (/var/cache/pacman/pkg):

```
pacman -Scc

```

보다 상세한 스위치들에 대해서는 `pacman --help`나 `man pacman`를 조회해보자.

## 설정

*pacman'*의 설정 파일은 `/etc/pacman.conf`에 있습니다. 이건 pacman에게 사용자가 원하는 방식으로 작업하도록 프로그램을 설정하는 스크립트 입니다. 설정 파일에 관한 자세한 정보는 [man pacman.conf](https://www.archlinux.org/pacman/pacman.conf.5.html)에서 볼 수 있습니다.

### 기본 옵션

기본 옵션들은 설정 파일의 `[options]` 부분에 있습니다. [man page](/index.php/Man_page "Man page")를 읽어보시거나 or 기본 `pacman.conf`를 보시면 여기에다가 무엇을 해야하는지 알 수 있습니다.

### 저장소

`/etc/pacman.conf` 설정 파일에 써져있는 바와 같이, 이 부분에서는 어떤 [공식 저장소](/index.php/Official_repositories "Official repositories")를 사용할 것인지 정합니다. 여러 저장소들은 `/etc/pacman.d/mirrorlist`처럼 다른 파일에 포함되어 있거나 직접 설정 파일에서 정할 수 있습니다. 그래서 딱 하나의 목록을 유지보수 함을 필요로 합니다.

 `/etc/pacman.conf` 
```
#[testing]
#SigLevel = PackageRequired
#Include = /etc/pacman.d/mirrorlist

[core]
SigLevel = PackageRequired
Include = /etc/pacman.d/mirrorlist

[extra]
SigLevel = PackageRequired
Include = /etc/pacman.d/mirrorlist

#[community-testing]
#SigLevel = PackageRequired
#Include = /etc/pacman.d/mirrorlist

[community]
SigLevel = PackageRequired
Include = /etc/pacman.d/mirrorlist

# If you want to run 32 bit applications on your x86_64 system,
# enable the multilib repositories as required here.

#[multilib-testing]
#SigLevel = PackageRequired
#Include = /etc/pacman.d/mirrorlist

#[multilib]
#SigLevel = PackageRequired
#Include = /etc/pacman.d/mirrorlist

# An example of a custom package repository.  See the pacman manpage for
# tips on creating your own repositories.
#[custom]
#SigLevel = Optional TrustAll
#Server = file:///home/custompkgs
```

**Warning:** Care should be taken when using the *testing* repository. It is in active development and updating may cause some packages to stop working. People who use the *testing* repository are encouraged to subscribe to the [arch-dev-public mailing list](https://mailman.archlinux.org/mailman/listinfo/arch-dev-public) for current information.

## 연관 고리

[Improve pacman performance](/index.php/Improve_pacman_performance "Improve pacman performance")
[Colored Pacman output](/index.php/Colored_Pacman_output "Colored Pacman output")
[Downgrade packages](/index.php/Downgrade_packages "Downgrade packages")
[Redownloading all installed packages](/index.php/Redownloading_all_installed_packages "Redownloading all installed packages")
[Arch User Repository](/index.php/Arch_User_Repository "Arch User Repository")
[Local repository HOW-TO](/index.php/Local_repository_HOW-TO "Local repository HOW-TO")
[Custom local repository with ABS and gensync](/index.php/Custom_local_repository_with_ABS_and_gensync "Custom local repository with ABS and gensync")
[Howto Upgrade via Home Network](/index.php/Howto_Upgrade_via_Home_Network "Howto Upgrade via Home Network") (Network Shared Pacman Cache)
[Pacman GUI Frontends](/index.php/Pacman_GUI_Frontends "Pacman GUI Frontends")
[Pacman Aliases (for bash)](/index.php/Pacman_Aliases "Pacman Aliases")