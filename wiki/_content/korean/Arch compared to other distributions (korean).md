이 페이지는 아치와 타 GNU/리눅스 배포본/`유닉스`-류 운영체제간 유사점과 차이점에 대한 요약입니다. 아치와 타 배포본을 비교하는 최선의 방법은 직접 설치하고 써보는 것입니다. 아치는 항상 새로운 사용자를 도우려는 놀라운 사용자 커뮤니티를 갖고 있습니다. 아래의 요약은 아치가 당신에게 정말로 필요하다고 판단하기에 충분한 정보를 제공할 뿐입니다.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 소스-기반](#소스-기반)
    *   [1.1 젠투](#젠투)
    *   [1.2 소서러/루나-리눅스/소스메이지](#소서러/루나-리눅스/소스메이지)
    *   [1.3 Rock](#Rock)
*   [2 최소주의](#최소주의)
    *   [2.1 LFS](#LFS)
    *   [2.2 CRUX](#CRUX)
    *   [2.3 Slackware](#Slackware)
*   [3 Graphical](#Graphical)
    *   [3.1 Ubuntu](#Ubuntu)
    *   [3.2 Fedora](#Fedora)
    *   [3.3 Mandriva](#Mandriva)
    *   [3.4 SUSE](#SUSE)
    *   [3.5 PCLinuxOS](#PCLinuxOS)
*   [4 The *BSDs](#The_*BSDs)
    *   [4.1 FreeBSD](#FreeBSD)
    *   [4.2 NetBSD](#NetBSD)
    *   [4.3 OpenBSD](#OpenBSD)
*   [5 Other](#Other)
    *   [5.1 Debian GNU/Linux](#Debian_GNU/Linux)
    *   [5.2 Frugalware](#Frugalware)

## 소스-기반

소스-기반 배포본들은 이식성 높고, 특정 기계 아키텍처로 전체 운영체제와 패키지를 컴파일하는 장점과 자연적으로 소스-컴파일의 시간-소모하는 단점을 가져옵니다. 아치 기본과 모든 패키지는 i686과 x86-64 아키텍처에 최적화되었고 편리한 설치의 장점과 함께 i386/i486/i586 바이너리 배포본에 비해 잠재적인 성능 향상을 제공합니다.

### 젠투

아치 설치는 바이너리이기 때문에, 소스-기반 젠투 설치에 비해 시간-소모가 훨씬 적습니다. 젠투와 아치 모두 makeworld 기능이 가능한 바이너리와 소스-기반 패키징을 허용합니다; 하지만, 아치가 바이너리인 반면 젠투 기본 시스템은 소스-기반입니다. 둘다 롤링-릴리즈 시스템입니다. 아치 PKGBUILD는 젠투 ebuild보다 간결하고 더욱 편리하게 널리 인식됩니다. 젠투는 x86, ppc, sparc, alpha, amd64, mips, hppa, itanium을 지원하는 반면, 아치는 i686과 x86-64 뿐입니다. 아치 설계 방식은 간결함과 최소주의에 촛점을 두는 반면, 젠투는 소스 컴파일의 모든 측면을 전체적으로 제어하는 능력에 촛점을 맞춥니다. 두 배포본 모두 초)고수 수준의 커스텀을 허용하는 반면 젠투 사용자들은 아치의 많은 부분에서 훨씬 편리하다고 느끼고 있습니다.

### 소서러/루나-리눅스/소스메이지

소서러/루나-리눅스/소스메이지 (SLS) 는 젠투처럼 모두 소스-기반 배포본이지만 원래는 아치와 관련이 있습니다. SLS 배포본은 패키지 설명을 만드는 간단한 스크립트 파일 모음과 컴파일 과정을 설정하는 전역 설정 파일을 사용하기 보다는 아치의 ABS 시스템류를 사용합니다. SLS 도구는 완전한 의존성 검사(추가적인 기능 처리 포함)와 패키지 추적(및 제거/업그레이드)을 합니다. SLS 계열 위한 바이너리 패키지가 없기는 하지만 이전 설치된 패키지로 쉽게 돌아갈 수 있습니다.

설치는 기본 시스템 설치(아치와 매우 닮은점: i686-최적화, CLI와 ncurses 메뉴, 핵심 도구)를 수반하고, 나중에 (선택적) 기본 시스템을 다시 컴파일할 수 있게 합니다. 여기에는 "표준" WM/DE/DM 이 전혀 없고 기본 설치동안 X 서버를 설치하지 않습니다. 그러나 X 서버 대체품 (X.Org 6,8 or 7, XFree86)을 설치하는 쉬운 방법을 제공합니다.

SLS는 매우 복잡한 역사를 지녔습니다. 이에 대해 가장 잘 씌여진 글: [http://wiki.sourcemage.org/SourceMage/History](http://wiki.sourcemage.org/SourceMage/History)

루나 리눅스: [http://lunar-linux.org/](http://lunar-linux.org/)
소스메이지: [http://www.sourcemage.org/](http://www.sourcemage.org/)
소서러: [http://sorcerer.berlios.de/](http://sorcerer.berlios.de/)

### Rock

*소개 [http://www.rocklinux.org/wiki/About](http://www.rocklinux.org/wiki/About)*

ROCK 리눅스는 유연한 리눅스 배포 빌드 키트입니다, 예를 들어 당신 자신만의 리눅스 배포본을 만들기 위한 툴체인/프레임워크. 만약 당신 자신만의 배포본을 빌드하기 원하지 않지만 단순히 좋은 범용 배포본으로 흥미가 있다면 크리스탈 ROCK을 원할 것입니다. [http://www.rocklinux.org/wiki/Crystal_ROCK](http://www.rocklinux.org/wiki/Crystal_ROCK)

빌드 도구에 의존하는 배포본 VS 아치; 컴파일에 시간이 걸리는 소스 기반으로서 똑같은 문제점, 기타. SPARC, ARM 등 많은 프로세서에서 작동하는 것으로 보입니다.

## 최소주의

최소주의 배포본들은 아치와 비교될만한 몇가지 유사점을 공유합니다.

### LFS

LFS, 또는 Linux From Scratch는 GNU/리눅스 시스템을 위해 손수 컴파일하고 설정한 최소한의 기본 패키지 모음입니다. LFS는 기본 시스템을 구축하는 교육 과정을 훌륭히 제공할 수 있도록 최소한으로 구성됩니다. 아치는 이와 매우 동일한 패키지에 BSD-스타일 init, 약간의 추가적인 도구와 기본 시스템으로써 i686/x86-64로 컴파일된 강력한 pacman 패키지 매니저를 제공합니다. LFS는 온라인 저장소가 없습니다; 수동으로 취득한 소스는 **make**로 컴파일 및 설치됩니다. (패키지 관리의 일부 수동 방식이 존재하고, LFS 힌트에 언급되어 있습니다.) 최소한의 아치 기본 시스템과 함께, 아치 커뮤니티와 개발자들은 pacman을 통해 설치 가능한 많은 수 천개의 바이너리 패키지뿐만 아니라 ABS - 아치 (소스) 빌드 시스템과 함께 사용되는 PKGBUIL 빌드 스크립트를 제공하고 유지합니다. 아치는 또한 편법 빌드 또는 pacman이 손쉽게 설치할 수 있는 .pkg.tar.gz 패키지를 커스터마이징하는 makepkg 도구를 포함합니다. Judd Vinet은 아치를 밑바닥부터 만들고, pacman을 C로 작성했습니다. 아치는 가끔, 한 마디로 "멋진 패키지 관리자를 곁들인 리눅스"라고 익살스럽게 설명됩니다.

### CRUX

아치는 독립적으로 개발되고, 아무런 기반 없이 만들어지며, 다른 GNU/Linux 배포판에 기초하지 않습니다. 아치를 만들기 전에, Judd Vinet가 Per Liden에 의해 만들어진 최소주의 배포판인 CRUX를 칭찬했고, 사용했습니다. 본래 CRUX와 공통으로 가지는 아이디어에 영감을 얻어, 아치는 scratch로부터 제작되고, [pacman](/index.php/Pacman "Pacman")은 그 후 C언어로 작성되었습니다. 그 둘은 그 둘을 지도하는 몇몇 원칙을 공유합니다: 예를며 들면, 둘 모두 아키텍처 최적화되어 있고, 최소주의이며 K.I.S.S.를 지향합니다. 둘 모두 ports 식의 시스템이 제공되며, BSD 스타일의 init 시스템과, BSD처럼 기반이 되는 최소한의 환경을 제공합니다. 아치는 바이너리 시스템 패키지 관리를 다루고 [Arch Build System](/index.php/Arch_Build_System "Arch Build System")과 균일하게 작동하는 pacman을 특징으로 합니다. CRUX는 커뮤니티의 공헌을 기반으로하는 시스템인 prt-get을 사용하고, 이는 CRUX 자체의 ports 시스템과 결합하여 의존성 해결을 다루지만, 모든 패키지를 소스로부터 빌드합니다(CRUX 기반 설치는 i686 바이너리이지만요.). 아치는 공식적으로 x86_64와 i686을 지원하는 반면, CRUX는 i686만을 지원합니다.

아치는 롤링 릴리즈 시스템을 사용하며 많은 열의 바이너리 패키지 저장소뿐만 아니라 [Arch User Repository](/index.php/Arch_User_Repository "Arch User Repository")까지 특징으로 삼습니다. ᅟCRUX는 더 규모가 축소된, 공식적으로 지원되는 포트 시스템에 더해 보통의 커뮤니티 저장소를 제공합니다.

### Slackware

The mighty Slackware and Arch are quite similar in that both are simple distributions focused on elegance and minimalism. Slackware is famous for its lack of branding and completely vanilla packages, from the kernel up. Arch typically applies patching only to avoid severe breakage and preserve functionality, if absolutely necessary. Both use BSD-style init scripts. Arch supplies a package management system in [pacman](/index.php/Pacman "Pacman") which, unlike Slackware's standard tools, offers automatic dependency resolution and allows for more automated system upgrades. Slackware users typically prefer their method of manual dependency resolution, citing the level of system control it grants them. Arch is a rolling-release system. Slackware is seen as more conservative in its release cycle, preferring proven stable packages. Arch is more 'bleeding-edge' in this respect. Arch offers the [Arch Build System](/index.php/Arch_Build_System "Arch Build System"), an actual ports-like system. The (unofficial) Slackbuild system is very similar to the [Arch User Repository](/index.php/Arch_User_Repository "Arch User Repository") concept. Slackware users will generally be quite comfortable with most aspects of Arch.

## Graphical

때때로 "초심자(newbie)"를 위한 배포판이라 불리는, 그래픽 형식의 배포판은 아치와 많은 유사성을 지니지만, 그들과는 꽤 다른 점이 있습니다. 아치는 만약 여러분이 최소한의 기초로부터 GNU/Linux를 직접 구성하며 배우고 싶다면 더 나은 선택일 것입니다. 왜냐하면 아치의 설치 과정은 그들과 비교해서 매우 적은 수의 패키지만을 설치하기 때문입니다. 그래픽 형식의 배포판은 페도라의 아나콘다(Anaconda)와 같은 GUI 설치 프로그램과 수세의 YaST와 같은 GUI 시스템 설정 도구와 함께 딸려오는 경향이 있습니다. 각 배포판 간의 구체적인 차이점은 아래에서 자세히 설명하겠습니다.

### Ubuntu

우분투는 캐노니컬 유한회사(Canonical Ltd.)에 의해 상업적으로 지원되는 굉장히 유명한 데비안 기반의 배포판입니다. 반면 아치는 아무런 기반 없이 설계되는, 독립적으로 개발되는 시스템입니다. 만약 여러분이 여러분만의 커널을 컴파일하고 싶으시다면, 최첨단의 CVS-only 프로젝트를 시도해 보시거나, 때로는 프로그램을 소스로부터 빌드하고 싶으시다면, 아치가 더 알맞습니다. 하지만 만약 여러분이 컴퓨터를 빠르게 켜서 사용하고, 시스템에 대한 것을 그다지 건드리고 싶지 않으시다면, 우분투가 더 알맞습니다. 아치는 기초 설치에서부터 좀 더 최소주의 형태로 제공되며, 사용자 각자가 그들의 필요에 맞게 개인화 하는 것에 의존합니다. 일반적으로, 개발자나 스스로 이것저것 만지기 좋아하는 사람들은 아마도 우분투보다 아치를 더 좋아할 것이지만, 몆몆 아치 유저는 우분투에서 시작해서 아치로 이전했다고 말합니다. 우분투는 개별 릴리즈를 6개월마다 시행하지만, 아치는 롤링 릴리즈 시스템입니다. 아치는 ports 식의 패키지 빌드 시스템인 [Arch Build System](/index.php/Arch_Build_System "Arch Build System")을 제공하지만, 우분투는 그렇지 않습니다. 두 배포판의 커뮤니티 또한 다른 면이 있습니다. 아치의 커뮤니티는 더 작으며, 그런 점에서 더 적극적이기를 독려합니다; 높은 비율의 이용자가 배포판에 기여합니다. 반면, 우분투 커뮤니티는 꽤 크고, 따라서 배포판 개발이나 패키지 또는 저장소 유지에 기여하지 않는 더 높은 비율의 유저를 수용해야 합니다.

### Fedora

페도라는 래드햇 베포판에서 파생된 것이며, 현재까지 꾸준하게 가장 유명한 배포판입니다. 그렇기에, 거대한 커뮤니티와 다수의 미리 빌드된 패키지, 그리고 지원이 있습니다. 페도라의 패키지는 RPM 기반이고, YUM을 패키지 매니저로 사용합니다 (Fedora 22부터는 DNF가 기본 패키지 매니저입니다). 아치는 [pacman](/index.php/Pacman "Pacman")을 패키지 관리자로 사용합니다. 페도라가 특허 문제로 MP3 미디어 포맷을 지원하려 하지 않는 것은 유명합니다. 아치는 MP3나 다른 미디어 포맷의 지원에 좀 더 관대합니다. 페도라는 GUI 설치 프로그램을 기본으로 사용합니다. 아치는 GUI 설치 프로그램을 지원하지 않고, ncurses 기반의 설치 프로그램을 사용하여, 사용자의 수동 설정에 의존합니다. 페도라는 정해진 출시 사이클을 가지고 있습니다. 아치는 반면 롤링 릴리즈 시스템입니다. 아치의 디자인 접근은 자동화/자동 설정이 아닌 가벼움과 미려함, 그리고 최소주의에 맞게 설겨되었습니다. 페도라는 혁신적이고 SELinux와 선(Sun)의 JRE의 필요성을 제거하기 위해 GCJ compiled 패키지를 통합한 것으로 많은 커뮤니티의 인정을 받았습니다. 페도라는 JFS와 ReiserFS 모두 훌륭하게 지원하지 않습니다.

### Mandriva

맨드리바 리눅스(이전에는 맨드레이크 리눅스)는 GNU/Linux를 누구나 쉽게 사용하게 하고자 하는 목적으로 1998년에 만들어졌습니다. 이것은 RPM 기반이며, urpmi를 패키지 매니저로 사용합니다. 다시 한 번 강조하자면, 아치는 좀 더 간단한 접근법을 취하며, 문자 기반이며, 수동 설정에 의존합니다. 또한 아치는 중급 또는 고급 사용자에 약간 더 알맞습니다.

### SUSE

수세는 높이 평가 받는 YaST 설정 도구를 중심으로 유명하며, 이 도구는 대부분 사용자가 필요한 설청을 모두 갖추고 있습니다. 아치는 [The Arch Way](/index.php/The_Arch_Way "The Arch Way"), 즉 아치 방식을 추구하기 때문에 그러한 도구를 제공하지 않습니다. 수세는 그러므로 리눅스에 경험이 부족한 사용자, GUI 위주의 환경을 원하는 사용자, 자동 설정과 기대하는 기능이 훌륭하게 작동하길 원하는 사용자에게 더 적합하다고 널리 여겨집니다.

### PCLinuxOS

PCLinuxOS is a popular Mandriva-based distro providing a complete DE, designed for user-friendliness and is described as "simple", though its definition of simple is quite different than the Arch definition. Arch is designed as a simple base system to be customized from the ground up and is aimed more toward advanced users. PCLOS uses the apt package manager as a wrapper for RPM packages. Arch uses its own independently-developed [pacman](/index.php/Pacman "Pacman") package manager with `.pkg.tar.gz` packages. PCLOS is very GUI-driven, provides GUI hardware configuration tools and the Synaptic package management front-end, and claims to have little or no reliance on the shell. Arch is command-line oriented and designed for more simple approaches to system configuration, management and maintenance. PCLOS recommends 256MB RAM as part of its minimum system requirements. Being more lightweight, Arch can run on systems with much less system memory, requiring only 64MB of RAM for a base i686 install, and will run flawlessly on more modern systems.

## The *BSDs

Both Arch and *BSD offer a tightly-integrated base and ports system combined with available binary packages. The BSDs derive from Berkeley <tt>UNIX</tt>. Therefore, *BSDs are not GNU/Linux distros, but rather, <tt>UNIX</tt>-like OS's.

### FreeBSD

Both Arch and [FreeBSD](http://www.freebsd.org/about.html) offer software which can be obtained using binaries or compiled using 'ports' systems. Both share a very similar init system. FreeBSD boasts that it is more of a system designed as a whole, compared to GNU/Linux distros, with each application 'ported' over to FreeBSD and made sure to work in the process. Both use `/etc/rc.conf` as a main configuration file. The FreeBSD license is generally more protective of the *coder*, compared to the GPL, which in contrast favors protection of the *code* itself. Arch is released under the GPL. In FreeBSD, like Arch, decisions are delegated to you, the power user. This may be the most interesting comparison to Arch since it goes head-to-head in package modernity and has a somewhat sizable, smart, active, no-nonsense community. Both systems share many similarities and FreeBSD users will generally feel quite comfortable with most aspects of Arch.

### NetBSD

NetBSD is a free, secure, and highly portable <tt>UNIX</tt>-like open-source operating system available for over 50 platforms, from 64-bit Opteron machines and desktop systems to hand-held and embedded devices. Its clean design and advanced features make it excellent in both production and research environments, and it is user-supported with complete source. Many applications are easily available through pkgsrc, the NetBSD Packages Collection. Arch may not operate on the vast number of devices NetBSD operates on, but for an i686 system it may offer more applications. Also, the default installation method in pkgsrc is to pull and compile sources whereas Arch offers binary packages. Arch does share many similarities with NetBSD; both use `/etc/rc.conf` as the primary configuration file, they are very minimalist and lightweight, they both offer ports systems as well as binaries and both have active, no-nonsense developers and communities. Arch also borrows from *BSD for its init system concepts.

### OpenBSD

The OpenBSD project produces a free, multi-platform 4.4BSD-based <tt>UNIX</tt>-like operating system. Efforts focus on portability, standardization, code correctness, proactive security, and integrated cryptography. In contrast, Arch focuses more on simplicity, elegance, minimalism and bleeding edge software. OpenBSD supports binary emulation of most programs from SVR4 (Solaris), FreeBSD, GNU/Linux, BSD/OS, SunOS and HP-UX. OpenBSD is self-described as 'perhaps the #1 security OS'.

In common with Arch, OpenBSD offers a small, elegant, base install and uses a ports system and packaging systems to allow for easy installation and management of programs which are not part of the base operating system. In contrast to a GNU/Linux system like Arch, but in common with most other BSD-based operating systems, the OpenBSD kernel and userland programs, such as the shell and common tools (like ls, cp, cat and ps), are developed together in a single source repository.

## Other

These OS's fall into the 'other' category.

### Debian GNU/Linux

데비안은 더 큰 프로젝트이자 커뮤니티이며, 20000개 이상의 바이너리 패키지를 제공하는 stable, testing, unstable 저장소를 특징으로 삼습니다. 아치는 그들 패키지를 데비안처럼 "-dev"와 "-common"으로 '분리'하지 않기 때문에, 아치의 저장소는 훨씬 작아보일 것입니다. 데비안은 더 열렬하게 자유 소프트웨어의 자세를 가지고 있습니다. 아치는 GNU에 의해 'non-free(비자유)'로 정의된 패키지에 대해 좀 더 관대합니다. 데비안의 디자인 접근법은 안정성과 엄격한 테스트에 초점을 맞춥니다. 아치는 간결함, 최소주의 철학과, 최첨단 소프트웨어를 제공하는 것에 더욱 초점을 맞추고 있습니다. 아치의 패키지는 데비안 Stable과 Testing의 패키지보다 더 최신이며, 데비안 unstable하고 일반적으로 같은 버전을 지닙니다. 데비안과 아치 모두 양질의 패키지 관리 시스템을 제공합니다. 아치는 롤링 릴리즈 방식인 반면, 데비안 Stable은 "frozen" 패키지와 함께 출시됩니다. 데비안은 alpha, arm, hppa, i386, x86_64, ia64, m68k, mips, mipse, powerpc, s390과 sparc를 포함한 다양한 아키텍처에서 사용 가능하지만, 아치는 i686과 x86_64만을 제공합니다. 아치는 ports 식의 패키지 빌드 시스템과 함께 외부 소스로부터 자체의, 설치가능한 패키지를 빌드하는 더 편리한 지원을 제공합니다. 데비안은 ports 시스템을 제공하지 않고, 대신 그것의 거대한 바이너리 저장소에 의존합니다. 아치 설치 시스템은 오직 최소한의 기반만 제공하며, 이는 시스템 설정을 하는 동안에 투명하게 노출되지만, 데비안의 방법은 더 자동화된 설정뿐만 아니라 여러 대체 설치 방식도 제공합니다. 데비안은 SysVinit을 활용하는 반면, 아치는 더 간단한 BSD 스타일의 init을 사용합니다.

### Frugalware

Arch is text-based and command-line oriented. Frugalware has adopted Arch's [pacman](/index.php/Pacman "Pacman") as its package manager, but uses bzipped tarballs. In contrast, Arch uses gzipped tarballs, for the purpose of expedience of installation. Frugalware doesn't support the JFS filesystem by default. Frugalware is no longer based on Slackware but is rather a distro of its own, and is promoted as an i686 distro. Arch is a fundamentally different system, being installed as a minimal base environment and expanded with pacman according to the user's choices and needs. Frugalware is installed from a DVD, with default software choices and desktop environment chosen for the user already. Frugalware has a scheduled release cycle. Again, Arch is more focused on simplicity, minimalism, code-correctness and bleeding edge packages within a rolling-release model.