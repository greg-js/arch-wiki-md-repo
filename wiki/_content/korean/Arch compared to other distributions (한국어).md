이 페이지는 아치와 타 GNU/리눅스 배포본/`유닉스`-류 운영체제간 유사점과 차이점에 대한 요약입니다. 아치와 타 배포본을 비교하는 최선의 방법은 직접 설치하고 써보는 것입니다. 아치는 항상 새로운 사용자를 도우려는 놀라운 사용자 커뮤니티를 갖고 있습니다. 아래의 요약은 아치가 당신에게 정말로 필요하다고 판단하기에 충분한 정보를 제공할 뿐입니다.

## Contents

*   [1 소스-기반](#.EC.86.8C.EC.8A.A4-.EA.B8.B0.EB.B0.98)
    *   [1.1 젠투](#.EC.A0.A0.ED.88.AC)
    *   [1.2 소서러/루나-리눅스/소스메이지](#.EC.86.8C.EC.84.9C.EB.9F.AC.2F.EB.A3.A8.EB.82.98-.EB.A6.AC.EB.88.85.EC.8A.A4.2F.EC.86.8C.EC.8A.A4.EB.A9.94.EC.9D.B4.EC.A7.80)
    *   [1.3 Rock](#Rock)
*   [2 최소주의](#.EC.B5.9C.EC.86.8C.EC.A3.BC.EC.9D.98)
    *   [2.1 LFS](#LFS)
    *   [2.2 CRUX](#CRUX)
    *   [2.3 Slackware](#Slackware)
*   [3 Graphical](#Graphical)
    *   [3.1 Ubuntu](#Ubuntu)
    *   [3.2 Fedora](#Fedora)
    *   [3.3 Mandriva](#Mandriva)
    *   [3.4 SUSE](#SUSE)
    *   [3.5 PCLinuxOS](#PCLinuxOS)
*   [4 The *BSDs](#The_.2ABSDs)
    *   [4.1 FreeBSD](#FreeBSD)
    *   [4.2 NetBSD](#NetBSD)
    *   [4.3 OpenBSD](#OpenBSD)
*   [5 Other](#Other)
    *   [5.1 Debian GNU/Linux](#Debian_GNU.2FLinux)
    *   [5.2 Frugalware](#Frugalware)

## 소스-기반

소스-기반 배포본들은 이식성 높고, 특정 기계 아키텍처로 전체 운영체제와 패키지를 컴파일하는 장점과 자연적으로 소스-컴파일의 시간-소모하는 단점을 가져옵니다. 아치 기본과 모든 패키지는 i686과 x86-64 아키텍처에 최적화되었고 편리한 설치의 장점과 함께 i386/i486/i586 바이너리 배포본에 비해 잠재적인 성능 향상을 제공합니다.

### 젠투

아치 설치는 바이너리이기 때문에, 소스-기반 젠투 설치에 비해 시간-소모가 훨씬 적습니다. 젠투와 아치 모두 makeworld 기능이 가능한한 바이너리와 소스-기반 패키징을 허용합니다; 하지만, 아치가 바이너리인 반면 젠투 기본 시스템은 소스-기반입니다. 둘다 롤링-릴리즈 시스템입니다. 아치 PKGBUILD는 젠투 ebuild보다 간결하고 더욱 편리하게 널리 인식됩니다. 젠투는 x86, ppc, sparc, alpha, amd64, mips, hppa, itanium을 지원하는 반면, 아치는 i686과 x86-64 뿐입니다. 아치 설계 방식은 간결함과 최소주의에 촛점을 두는 반면, 젠투는 소스 컴파일의 모든 측면을 전체적으로 제어하는 능력에 촛점을 맞춥니다. 두 배포본 모두 초고수준의 커스텀을 허용하는 반면 젠투 사용자들은 아치의 많은 부분에서 훨씬 편리하다고 느끼고 있습니다.

### 소서러/루나-리눅스/소스메이지

소서러/루나-리눅스/소스메이지 (SLS) 는 젠투처럼 모두 소스-기반 배포본이지만 원래는 아치와 관련이 있습니다. SLS 배포본은 패키지 설명을 만드는 간단한 스크립트 파일 모음과 컴파일 과정을 설정하는 전역 설정 파일을 사용하기 보다는 아치의 ABS 시스템류를 사용합니다. SLS 도구는 완전한 의존성 검사(추가적인 기능 처리 포함)와 패키지 추적(및 제거/업그레이드)을 합니다. SLS 계열 위한 바이너리 패키지가 없기는 하지만 이전 설치된 패키지로 쉽게 돌아갈 수 있습니다.

설치는 기본 시스템 설치(아치와 매우 닮은점: i686-최적화, CLI와 ncurses 메뉴, 핵심 도구)를 수반하고, 나중에 (선택적) 기본 시스템을 다시 컴파일할 수 있게 합니다. 여기에는 "표준" WM/DE/DM 이 전혀 없고 기본 설치동안 X 서버를 설치하지 않습니다. 그러나 X 서버 대체품 (X.Org 6,8 or 7, XFree86)을 설치하는 쉬운 방법을 제공합니다.

SLS는 매우 복잡한 역사를 지녔습니다. 이에 대해 가장 잘 씌여진 글: [http://wiki.sourcemage.org/SourceMage/History](http://wiki.sourcemage.org/SourceMage/History)

루나 리눅스: [http://lunar-linux.org/](http://lunar-linux.org/)
소스메이지: [http://www.sourcemage.org/](http://www.sourcemage.org/)
소서러: [http://sorcerer.berlios.de/](http://sorcerer.berlios.de/)

### Rock

_소개 [http://www.rocklinux.org/wiki/About](http://www.rocklinux.org/wiki/About)_

ROCK 리눅스는 유연한 리눅스 배포 빌드 키트입니다, 예를 들어 당신 자신만의 리눅스 배포본을 만들기 위한 툴체인/프레임워크. 만약 당신 자신만의 배포본을 빌드하기 원하지 않지만 단순히 좋은 범용 배포본으로 흥미가 있다면 크리스탈 ROCK을 원할 것입니다. [http://www.rocklinux.org/wiki/Crystal_ROCK](http://www.rocklinux.org/wiki/Crystal_ROCK)

빌드 도구에 의존하는 배포본 VS 아치; 컴파일에 시간이 걸리는 소스 기반으로서 똑같은 문제점, 기타. SPARC, ARM 등 많은 프로세서에서 작동하는 것으로 보입니다.

## 최소주의

최소주의 배포본들은 아치와 비교될만한 몇가지 유사점을 공유합니다.

### LFS

LFS, 또는 Linux From Scratch는 GNU/리눅스 시스템을 위해 손수 컴파일하고 설정한 최소한의 기본 패키지 모음입니다. LFS는 기본 시스템을 구축하는 교육 과정을 훌륭히 제공할 수 있도록 최소한으로 구성됩니다. 아치는 이와 매우 동일한 패키지에 BSD-스타일 init, 약간의 추가적인 도구와 기본 시스템으로써 i686/x86-64로 컴파일된 강력한 pacman 패키지 매니저를 제공합니다. LFS는 온라인 저장소가 없습니다; 수동으로 취득한 소스는 **make**로 컴파일 및 설치됩니다. (패키지 관리의 일부 수동 방식이 존재하고, LFS 힌트에 언급되어 있습니다.) 최소한의 아치 기본 시스템과 함께, 아치 커뮤니티와 개발자들은 pacman을 통해 설치 가능한 많은 수 천개의 바이너리 패키지뿐만 아니라 ABS - 아치 (소스) 빌드 시스템과 함께 사용되는 PKGBUIL 빌드 스크립트를 제공하고 유지합니다. 아치는 또한 편법 빌드 또는 pacman이 손쉽게 설치할 수 있는 .pkg.tar.gz 패키지를 커스터마이징하는 makepkg 도구를 포함합니다. Judd Vinet은 아치를 밑바닥부터 만들고, pacman을 C로 작성했습니다. 아치는 가끔, 한 마디로 "멋진 패키지 관리자를 곁들인 리눅스"라고 익살스럽게 설명됩니다.

### CRUX

Arch is independently developed, was built from scratch and is not based on any other GNU/Linux distribution. Before creating Arch, Judd Vinet admired and used CRUX, a minimalist distro created by Per Liden. Originally inspired by ideas in common with CRUX, Arch was built from scratch, and [pacman](/index.php/Pacman "Pacman") was then coded in C. The two share some guiding principles: for instance, both are architecture-optimized, minimalist and K.I.S.S.-oriented. Both ship with ports-like systems, use *BSD-style init systems and, like *BSD, both provide a minimal base environment to build upon. Arch features pacman, which handles binary system package management and works seamlessly with the [Arch Build System](/index.php/Arch_Build_System "Arch Build System"). CRUX uses a community contributed system called prt-get, which, in combination with its own ports system, handles dependency resolution, but builds all packages from source (though the CRUX base installation is i686 binary). Arch officially supports x86-64 and i686, whereas CRUX is i686-only.

Arch uses a rolling-release system and features a large array of binary package repositories as well as the [Arch User Repository](/index.php/Arch_User_Repository "Arch User Repository"). CRUX provides a more slimmed-down officially supported ports system in addition to a modest community repository.

### Slackware

The mighty Slackware and Arch are quite similar in that both are simple distributions focused on elegance and minimalism. Slackware is famous for its lack of branding and completely vanilla packages, from the kernel up. Arch typically applies patching only to avoid severe breakage and preserve functionality, if absolutely necessary. Both use BSD-style init scripts. Arch supplies a package management system in [pacman](/index.php/Pacman "Pacman") which, unlike Slackware's standard tools, offers automatic dependency resolution and allows for more automated system upgrades. Slackware users typically prefer their method of manual dependency resolution, citing the level of system control it grants them. Arch is a rolling-release system. Slackware is seen as more conservative in its release cycle, preferring proven stable packages. Arch is more 'bleeding-edge' in this respect. Arch offers the [Arch Build System](/index.php/Arch_Build_System "Arch Build System"), an actual ports-like system. The (unofficial) Slackbuild system is very similar to the [Arch User Repository](/index.php/Arch_User_Repository "Arch User Repository") concept. Slackware users will generally be quite comfortable with most aspects of Arch.

## Graphical

Sometimes called "newbie" distros, the graphical distros share a lot of similarities, though Arch is quite different from them. Arch may be a better choice if you want to learn about GNU/Linux by building up from a very minimal base, as an installation of Arch installs very few packages in comparison. Graphical distros tend to ship with GUI installers (like Fedora's Anaconda) and GUI system-configuration tools (like SUSE's YaST). Specific differences between distros are described below.

### Ubuntu

Ubuntu is an immensely popular Debian-based distro commercially sponsored by Canonical Ltd., while Arch is an indepedently developed system built from scratch. If you like to compile your own kernels, try out bleeding-edge CVS-only projects, or build a program from source every once in a while, Arch is better suited. If you want to get up and running quickly and not fiddle around with the guts of the system as much, Ubuntu is better suited. Arch is presented as a much more minimalist design from the base installation onward, relying on the user to customize it to their own specific needs. In general, developers and tinkerers will probably like Arch better than Ubuntu, though some Arch users claim to have started on Ubuntu and eventually migrated to Arch. Ubuntu moves between discrete releases every 6 months, whereas Arch is a rolling-release system. Arch offers a ports-like package build system, the [Arch Build System](/index.php/Arch_Build_System "Arch Build System"), while Ubuntu does not. The two communities differ in some ways as well. The Arch community is much smaller and is strongly encouraged to be proactive; a large percentage contribute to the distro. In contrast, the Ubuntu community is quite large and can therefore tolerate a much larger percentage of users who do not contribute to development, package or repo maintenance.

### Fedora

Fedora is a spin-off from the Red Hat distribution and has continually been one of the most popular distributions to date. As such, there is a massive community and lots of pre-built packages and support available. Fedora packages are RPM-based, using YUM as its package manager. Arch uses [pacman](/index.php/Pacman "Pacman") to manage `.pkg.tar.gz` packages. Fedora famously doesn't attempt to support the MP3 media format due to perceived patent issues. Arch is more lenient in its disposition toward MP3 and other media. Fedora uses a graphical install by default. Arch does not offer a graphical installer, but rather, uses an ncurses-based installer, relying more on the user for manual configuration. Fedora has a scheduled release cycle. Arch is a rolling-release system. The Arch design approach is geared more toward lightweight elegance and minimalism rather than automation/auto-configuration. Fedora does innovate and recently earned much community recognition for integration of SELinux and GCJ compiled packages to remove the need for Sun's JRE. Fedora supports neither JFS nor ReiserFS out of the box.

### Mandriva

Mandriva Linux (formerly Mandrake Linux) was created in 1998 with the goal of making GNU/Linux easy to use for everyone. It is RPM-based and uses the urpmi package manager. Again, Arch takes a simpler approach, being text-based and relying on more manual configuration and is aimed a bit more toward intermediate to advanced users.

### SUSE

SUSE is centered around its well-regarded YaST configuration tool, which is a one-stop shop for most users' configuration needs. Arch doesn't offer such a facility as it goes against [The Arch Way](/index.php/The_Arch_Way "The Arch Way"). SUSE, therefore, is widely regarded as more appropriate for less-experienced users, or those who want a more GUI-driven environment, auto-configuration and expected functionality out of the box.

### PCLinuxOS

PCLinuxOS is a popular Mandriva-based distro providing a complete DE, designed for user-friendliness and is described as "simple", though its definition of simple is quite different than the Arch definition. Arch is designed as a simple base system to be customized from the ground up and is aimed more toward advanced users. PCLOS uses the apt package manager as a wrapper for RPM packages. Arch uses its own independently-developed [pacman](/index.php/Pacman "Pacman") package manager with `.pkg.tar.gz` packages. PCLOS is very GUI-driven, provides GUI hardware configuration tools and the Synaptic package management front-end, and claims to have little or no reliance on the shell. Arch is command-line oriented and designed for more simple approaches to system configuration, management and maintenance. PCLOS recommends 256MB RAM as part of its minimum system requirements. Being more lightweight, Arch can run on systems with much less system memory, requiring only 64MB of RAM for a base i686 install, and will run flawlessly on more modern systems.

## The *BSDs

Both Arch and *BSD offer a tightly-integrated base and ports system combined with available binary packages. The BSDs derive from Berkeley <tt>UNIX</tt>. Therefore, *BSDs are not GNU/Linux distros, but rather, <tt>UNIX</tt>-like OS's.

### FreeBSD

Both Arch and [FreeBSD](http://www.freebsd.org/about.html) offer software which can be obtained using binaries or compiled using 'ports' systems. Both share a very similar init system. FreeBSD boasts that it is more of a system designed as a whole, compared to GNU/Linux distros, with each application 'ported' over to FreeBSD and made sure to work in the process. Both use `/etc/rc.conf` as a main configuration file. The FreeBSD license is generally more protective of the _coder_, compared to the GPL, which in contrast favors protection of the _code_ itself. Arch is released under the GPL. In FreeBSD, like Arch, decisions are delegated to you, the power user. This may be the most interesting comparison to Arch since it goes head-to-head in package modernity and has a somewhat sizable, smart, active, no-nonsense community. Both systems share many similarities and FreeBSD users will generally feel quite comfortable with most aspects of Arch.

### NetBSD

NetBSD is a free, secure, and highly portable <tt>UNIX</tt>-like open-source operating system available for over 50 platforms, from 64-bit Opteron machines and desktop systems to hand-held and embedded devices. Its clean design and advanced features make it excellent in both production and research environments, and it is user-supported with complete source. Many applications are easily available through pkgsrc, the NetBSD Packages Collection. Arch may not operate on the vast number of devices NetBSD operates on, but for an i686 system it may offer more applications. Also, the default installation method in pkgsrc is to pull and compile sources whereas Arch offers binary packages. Arch does share many similarities with NetBSD; both use `/etc/rc.conf` as the primary configuration file, they are very minimalist and lightweight, they both offer ports systems as well as binaries and both have active, no-nonsense developers and communities. Arch also borrows from *BSD for its init system concepts.

### OpenBSD

The OpenBSD project produces a free, multi-platform 4.4BSD-based <tt>UNIX</tt>-like operating system. Efforts focus on portability, standardization, code correctness, proactive security, and integrated cryptography. In contrast, Arch focuses more on simplicity, elegance, minimalism and bleeding edge software. OpenBSD supports binary emulation of most programs from SVR4 (Solaris), FreeBSD, GNU/Linux, BSD/OS, SunOS and HP-UX. OpenBSD is self-described as 'perhaps the #1 security OS'.

In common with Arch, OpenBSD offers a small, elegant, base install and uses a ports system and packaging systems to allow for easy installation and management of programs which are not part of the base operating system. In contrast to a GNU/Linux system like Arch, but in common with most other BSD-based operating systems, the OpenBSD kernel and userland programs, such as the shell and common tools (like ls, cp, cat and ps), are developed together in a single source repository.

## Other

These OS's fall into the 'other' category.

### Debian GNU/Linux

Debian is a much larger project and community and features stable, testing, and unstable branches, offering over 20,000 binary packages. Arch does not 'split' their packages into "-dev" and "-common" as Debian does, therefore, Arch repositories will seem much smaller. Debian has a more vehement stance on free software. Arch is more lenient when it comes to 'non-free' packages as defined by GNU. Debian's design approach focuses more on stability and stringent testing. Arch is focused more on the philosophy of simplicity, minimalism, and offering bleeding edge software. Arch packages are more current than Debian Stable and Testing, typically being about equal with Debian unstable. Both Debian and Arch offer well-regarded package management systems. Arch is a rolling release, whereas Debian Stable is released with "frozen" packages. Debian is available for many architectures, including alpha, arm, hppa, i386, x86_64, ia64, m68k, mips, mipsel, powerpc, s390, and sparc, whereas Arch is i686 and x86_64 only. Arch provides more expedient support for building custom, installable packages from outside sources, with a ports-like package build system. Debian does not offer a ports system, relying instead on its huge binary repositories. The Arch installation system only offers a minimal base, transparently exposed during system configuration, whereas Debian's methods offer a more automatically configured approach as well as several alternative methods of installation. Debian utilizes the SysVinit, whereas Arch uses a simpler *BSD-style init.

### Frugalware

Arch is text-based and command-line oriented. Frugalware has adopted Arch's [pacman](/index.php/Pacman "Pacman") as its package manager, but uses bzipped tarballs. In contrast, Arch uses gzipped tarballs, for the purpose of expedience of installation. Frugalware doesn't support the JFS filesystem by default. Frugalware is no longer based on Slackware but is rather a distro of its own, and is promoted as an i686 distro. Arch is a fundamentally different system, being installed as a minimal base environment and expanded with pacman according to the user's choices and needs. Frugalware is installed from a DVD, with default software choices and desktop environment chosen for the user already. Frugalware has a scheduled release cycle. Again, Arch is more focused on simplicity, minimalism, code-correctness and bleeding edge packages within a rolling-release model.