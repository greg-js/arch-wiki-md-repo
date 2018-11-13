관련 항목

*   [FAQ (한국어)](/index.php/FAQ_(%ED%95%9C%EA%B5%AD%EC%96%B4) "FAQ (한국어)")
*   [설치 안내서](/index.php/%EC%84%A4%EC%B9%98_%EC%95%88%EB%82%B4%EC%84%9C "설치 안내서")
*   [초보자 안내서](/index.php/%EC%B4%88%EB%B3%B4%EC%9E%90_%EC%95%88%EB%82%B4%EC%84%9C "초보자 안내서")
*   [List of applications (한국어)](/index.php?title=List_of_applications_(%ED%95%9C%EA%B5%AD%EC%96%B4)&action=edit&redlink=1 "List of applications (한국어) (page does not exist)")

이 문서에서는 아치 리눅스 시스템을 향상시키고, 기능을 추가하는 데에 유용하거나 중요한 정보를 다룹니다. 이 문서는 여러분이 [초보자 안내서](/index.php/%EC%B4%88%EB%B3%B4%EC%9E%90_%EC%95%88%EB%82%B4%EC%84%9C "초보자 안내서")나 [설치 안내서](/index.php/%EC%84%A4%EC%B9%98_%EC%95%88%EB%82%B4%EC%84%9C "설치 안내서")를 통해 기본적인 아치 리눅스 설치를 끝낸 뒤라고 가정합니다. [#시스템 관리](#시스템_관리)와 [#패키지 관리](#패키지_관리) 섹션에서 다루는 기본적인 개념들을 *반드시* 이해하고 나서 나머지 항목들을 읽으십시오.

## Contents

*   [1 시스템 관리](#시스템_관리)
    *   [1.1 사용자와 그룹](#사용자와_그룹)
    *   [1.2 권한 상승](#권한_상승)
    *   [1.3 서비스 관리](#서비스_관리)
    *   [1.4 시스템 유지](#시스템_유지)
*   [2 패키지 관리](#패키지_관리)
    *   [2.1 pacman](#pacman)
    *   [2.2 저장소](#저장소)
    *   [2.3 아치 빌드 시스템(ABS)](#아치_빌드_시스템(ABS))
    *   [2.4 아치 사용자 저장소(Arch User Repository)](#아치_사용자_저장소(Arch_User_Repository))
    *   [2.5 미러](#미러)
*   [3 그래픽 사용자 인터페이스(GUI)](#그래픽_사용자_인터페이스(GUI))
    *   [3.1 디스플레이 드라이버](#디스플레이_드라이버)
    *   [3.2 디스플레이 서버](#디스플레이_서버)
    *   [3.3 창 관리자](#창_관리자)
    *   [3.4 디스플레이 관리자](#디스플레이_관리자)
    *   [3.5 데스크탑 환경](#데스크탑_환경)
*   [4 오디오 및 동영상](#오디오_및_동영상)
    *   [4.1 소리](#소리)
    *   [4.2 브라우저 플러그인](#브라우저_플러그인)
    *   [4.3 코덱](#코덱)
*   [5 네트워크](#네트워크)
    *   [5.1 시계 동기화](#시계_동기화)
    *   [5.2 DNS 성능](#DNS_성능)
    *   [5.3 DNS 보안](#DNS_보안)
    *   [5.4 방화벽 설정하기](#방화벽_설정하기)
    *   [5.5 윈도우 네트워크 사용하기](#윈도우_네트워크_사용하기)
*   [6 부팅](#부팅)
    *   [6.1 하드웨어 자동 감지](#하드웨어_자동_감지)
    *   [6.2 부팅시에 Num Lock 켜기](#부팅시에_Num_Lock_켜기)
    *   [6.3 부팅 메시지 유지하기](#부팅_메시지_유지하기)
    *   [6.4 부팅시에 자동으로 X 시작하기](#부팅시에_자동으로_X_시작하기)
*   [7 전원 관리](#전원_관리)
    *   [7.1 ACPI 이벤트](#ACPI_이벤트)
    *   [7.2 CPU 주파수 관리](#CPU_주파수_관리)
    *   [7.3 노트북](#노트북)
    *   [7.4 대기 모드와 최대 절전 모드](#대기_모드와_최대_절전_모드)
*   [8 입력 장치](#입력_장치)
    *   [8.1 키보드 레이아웃](#키보드_레이아웃)
    *   [8.2 마우스 버튼](#마우스_버튼)
    *   [8.3 노트북 터치패드](#노트북_터치패드)
    *   [8.4 TrackPoints](#TrackPoints)
*   [9 최적화](#최적화)
    *   [9.1 벤치마크](#벤치마크)
    *   [9.2 성능 극대화하기](#성능_극대화하기)
    *   [9.3 SSD](#SSD)
*   [10 시스템 서비스](#시스템_서비스)
    *   [10.1 파일 색인 및 검색](#파일_색인_및_검색)
    *   [10.2 로컬 메일 배달](#로컬_메일_배달)
    *   [10.3 프린터 설정](#프린터_설정)
*   [11 외관](#외관)
    *   [11.1 글꼴](#글꼴)
        *   [11.1.1 콘솔 글꼴](#콘솔_글꼴)
        *   [11.1.2 패치된 글꼴 패키지](#패치된_글꼴_패키지)
    *   [11.2 GTK 및 QT 테마](#GTK_및_QT_테마)
*   [12 콘솔 향상시키기](#콘솔_향상시키기)
    *   [12.1 Alias 설정하기](#Alias_설정하기)
    *   [12.2 다른 쉘 사용하기](#다른_쉘_사용하기)
    *   [12.3 Bash 추가기능](#Bash_추가기능)
    *   [12.4 컬러 출력](#컬러_출력)
        *   [12.4.1 핵심(Core) 유틸리티](#핵심(Core)_유틸리티)
        *   [12.4.2 Man 페이지](#Man_페이지)
    *   [12.5 압축파일](#압축파일)
    *   [12.6 콘솔 프롬프트](#콘솔_프롬프트)
    *   [12.7 이맥스 쉘](#이맥스_쉘)
    *   [12.8 마우스 지원](#마우스_지원)
    *   [12.9 스크롤백 버퍼](#스크롤백_버퍼)
    *   [12.10 세션 관리](#세션_관리)

## 시스템 관리

이 항목은 시스템 관리에 대한 기본적인 정보를 다룹니다. 더 자세한 정보를 얻으려면 [Category:System administration](/index.php/Category:System_administration "Category:System administration")와 [Core utilities](/index.php/Core_utilities "Core utilities")를 읽으십시오.

### 사용자와 그룹

새로 아치 리눅스를 설치했을 경우, 기본적으로 사용자 계정은 슈퍼유저 계정 하나 뿐입니다. 슈퍼유저 계정은 '루트(root)이라고도 부릅니다. 루트 사용자로 지속적으로 로그인하거나 [SSH](/index.php/SSH "SSH")로 루트 로그인을 허용하는 것은 보안 문제를 일으킬 수 있습니다. 그러므로 권한이 제한적인 사용자로 대부분의 작업을 진행하는 것이 권장됩니다. 루트 사용자는 시스템 관리 작업을 할 때에만 사용하십시오. [Users and groups#Example adding a user](/index.php/Users_and_groups#Example_adding_a_user "Users and groups") 항목에서 일반적인 데스크톱 시스템에서의 사용자 설정 예시를 볼 수 있습니다.

사용자와 그룹은 *접근 관리(access control)*에 사용됩니다. 시스템 관리자는 그룹 멤버십과 소유권 등을 세심하게 조정하여 사용자나 서비스들이 어느 시스템 리소스에 접근할 수 있는지 제어할 수 있습니다. [Users and groups](/index.php/Users_and_groups "Users and groups") 문서에서 사용자 및 그룹 관리에 대한 더 자세한 정보를 찾을 수 있습니다.

### 권한 상승

[su](/index.php/Su "Su") (substitute user) 명령어는 이미 로그인한 사용자가 시스템의 다른 사용자로 전환하여 작업을 진행할 수 있게 합니다. 주로 루트 사용자로 전환하는 데에 사용됩니다. 그에 비해 [sudo](/index.php/Sudo "Sudo") 명령어는 특정 명령어를 실행할 때에 일시적으로 더 높은 권한을 사용할 수 있게 합니다.

### 서비스 관리

아치리눅스는 [systemd](/index.php/Systemd "Systemd")를 init 시스템으로 사용합니다. init 시스템은 리눅스에서 시스템 및 서비스를 관리합니다. 그러므로 아치 리눅스 시스템을 관리하고 유지하기 위해서는 *systemd*의 기본을 알고 있는 것이 좋습니다. systemd와의 상호작용은 주로 *systemctl* 명령을 통해 이루어집니다. [systemd#Basic systemctl usage](/index.php/Systemd#Basic_systemctl_usage "Systemd") 항목을 참고하십시오.

### 시스템 유지

아치는 롤링 릴리스(Rolling Release) 시스템을 사용하는 배포판이며, 패키지의 업데이트 주기가 짧습니다. 사용자들은 아치 시스템을 관리하고 [유지](/index.php/System_maintenance "System maintenance")하기 위한 약간의 시간을 들여야 합니다. [Enhance system stability](/index.php/Enhance_system_stability "Enhance system stability") 문서에서 아치 리눅스 시스템을 가능한 한 안정적으로 만드는 데에 도움을 얻을 수 있습니다.

## 패키지 관리

이 부분은 패키지 관리에 관련된 유익한 정보를 다룹니다. [FAQ (한국어)#패키지 관리](/index.php/FAQ_(%ED%95%9C%EA%B5%AD%EC%96%B4)#패키지_관리 "FAQ (한국어)") 항목과 [Category:Package management](/index.php/Category:Package_management "Category:Package management")에 속하는 문서들에서 더 많은 정보를 얻을 수 있습니다.

**참고:** [편리성보다는 코드 정확성](/index.php/The_Arch_Way_(%ED%95%9C%EA%B5%AD%EC%96%B4)#편리성보다는_코드의_정확성 "The Arch Way (한국어)")을 추구하는 것은 아치 리눅스 철학의 핵심 중 하나입니다. 시스템을 업데이트**하기 전에** 사용자가 직접 개입해야 하는 부분을 분명히 이해하고 있어야 합니다. [arch-announce 메일링 리스트](https://mailman.archlinux.org/mailman/listinfo/arch-announce/)에 구독하거나 업데이트 전에 [아치리눅스 홈페이지](https://archlinux.org)의 첫 화면에 있는 뉴스 항목들을 확인하십시오. [이 rss 피드](https://www.archlinux.org/feeds/news/)에 구독하거나, 트위터에서 [@archlinux](https://twitter.com/archlinux)를 팔로우하는 것도 좋은 방법입니다.

### pacman

[pacman](/index.php/Pacman "Pacman")은 아치 리눅스의 패키지 관리자입니다(*pac*kage *man*ager에서 이름을 따왔습니다). 모든 사용자들은 이 위키의 다른 항목을 읽기 전에 반드시 pacman 사용에 익숙해져야 합니다.

[pacman tips](/index.php/Pacman_tips "Pacman tips")에서 *pacman*과의 상호작용을 향상시키는 방법과 패키지 관리 전반에 관한 팁을 얻을 수 있습니다.

### 저장소

공식 저장소에 있는 패키지들이 왜 공식적으로 유지되는지가 궁금하다면 [공식 저장소](/index.php/Official_repositories "Official repositories") 항목을 읽으십시오.

64비트(x86_64) 아치리눅스를 설치했으며, 32비트 애플리케이션을 사용하고자 한다면, [multilib](/index.php/Multilib "Multilib") 저장소를 활성화하십시오.

[Unofficial user repositories](/index.php/Unofficial_user_repositories "Unofficial user repositories") 항목에서 기타 지원되지 않는 저장소들의 목록을 찾을 수 있습니다.

### 아치 빌드 시스템(ABS)

**Ports**는 원래 BSD 배포판들이 사용하던 시스템으로, 수많은 port들을 로컬 시스템 상의 디렉토리 트리(directory tree)구조 안에 포함시키고 관리하는 시스템입니다. Ports 시스템 상에서 각 Port(포트)는 그 포트에 해당하는 서드파티 어플리케이션의 이름을 딴 폴더 안의 설치용 스크립트들을 포함합니다.

아치리눅스의 [ABS](/index.php/ABS "ABS") 트리는 Ports와 같은 기능을 제공합니다. [ABS](/index.php/ABS "ABS")는 [PKGBUILD](/index.php/PKGBUILD "PKGBUILD")라는 스크립트들을 사용합니다. 각 PKGBUILD는 파일 체크섬, 프로젝트 URL, 버전, 라이센스, 빌드 정보 등 해당 패키지에 대한 정보들로 채워집니다. [makepkg](/index.php/Makepkg "Makepkg")명령어가 PKGBUILD 스크립트를 해석하여 *pacman*이 관리할 수 있는 패키지를 만듭니다.

AUR에 들어있는 패키지들 뿐 아니라 아치 저장소에 포함되어 있는 모든 패키지들은 makepkg 명령을 이용하여 직접 재컴파일 할 수 있습니다.

### 아치 사용자 저장소(Arch User Repository)

[ABS](/index.php/ABS "ABS")트리를 통해서 공식 저장소에 들어있는 패키지들을 컴파일할 수 있다면, [아치 사용자 저장소(AUR)](/index.php/Arch_User_Repository "Arch User Repository")은 아치 사용자들이 만든 패키지에 대해 유사한 기능을 제공합니다. AUR은 빌드 스크립트들을 담고 있는 비공식 저장소입니다. [웹 인터페이스](https://aur.archlinux.org/index.php)나 AUR 도우미를 사용하여 접근할 수 있습니다.

[AUR 도우미](/index.php/AUR_helper "AUR helper")들은 AUR을 더욱 쉽게 사용할 수 있게 해줍니다. 도우미마다 조금씩 기능이 다를 수 있지만, 모두 AUR의 패키지를 검색하고, 가져오고, 빌드한 후 설치하는 것을 도와줍니다.

### 미러

[Mirrors](/index.php/Mirrors "Mirrors") 항목에서 빠르고 최신 상태의 팩맨 미러를 사용하는 방법을 알아보십시오. 해당 항목에서 설명한 대로, [Mirror status](https://www.archlinux.org/mirrors/status/) 페이지나 [Mirror-Status](http://www.archlinux.de/?page=MirrorStatus)페이지에서 최근에 동기화된 미러의 목록을 확인하는 것이 가장 좋습니다.

## 그래픽 사용자 인터페이스(GUI)

이 부분에서는 아치리눅스 상에서 GUI 어플리케이션을 사용하고자 하는 사용자들을 위한 기본적인 정보를 제공합니다. [Category:X server](/index.php/Category:X_server "Category:X server")에서 더 자세한 내용을 확인할 수 있습니다.

### 디스플레이 드라이버

기본으로 포함되어 있는 *vesa*드라이버는 대부분의 비디오 카드와 작동할 것입니다. 하지만 대개의 경우 각 비디오 카드에 맞는 드라이버를 설치하여 성능을 크게 향상시킬 수 있습니다. 사용하고 있는 비디오카드에 따라 [ATI](/index.php/ATI "ATI"), [Intel](/index.php/Intel_graphics "Intel graphics"), [NVIDIA](/index.php/NVIDIA "NVIDIA") 항목을 참고하십시오.

### 디스플레이 서버

[Xorg](/index.php/Xorg "Xorg")는 [X 윈도 시스템](https://ko.wikipedia.org/wiki/X_%EC%9C%88%EB%8F%84_%EC%8B%9C%EC%8A%A4%ED%85%9C)의 대표적인 오픈소스 구현판(implementation)입니다. GUI 어플리케이션을 사용하기 위하 필요하며, 대부분의 사용자들은 Xorg를 설치하는 것이 좋습니다.

[Wayland](/index.php/Wayland "Wayland")는 Xorg를 대체하기 위한 새로운 디스플레이 서버 프로토콜입니다. Wayland의 참조 구현판(reference implementation)으로 Weston이 있습니다. 아직 이른 개발 단계에 있어 어플리케션 지원이 거의 없는 상태입니다.

### 창 관리자

데스크탑 환경은 완전하고 일관된 GUI를 제공하지만, 상당한 시스템 자원을 사용합니다. 성능을 극대화하고 싶은 사용자나, 간단한 환경을 원하는 사용자라면 [창 관리자](/index.php/Window_manager "Window manager")를 설치한 후 필요한 부분만을 추가로 설치하여 사용할 수 있습니다. 또한, 대부분의 데스크탑 환경들에서도 창 관리자를 교체하여 사용할 수 있습니다. 창 관리자는 [Dynamic](/index.php/Category:Dynamic_WMs "Category:Dynamic WMs"), [stacking](/index.php/Category:Stacking_WMs "Category:Stacking WMs"), [tiling](/index.php/Category:Tiling_WMs "Category:Tiling WMs") 등의 종류로 구분되는데, 이 세 종류의 창 관리자들은 창 배열을 서로 다른 방식으로 처리합니다.

### 디스플레이 관리자

X를 수동으로 시작하기보다는 디스플레이 관리자를 이용하여 X 세션을 시작하고 싶다면 [Display manager](/index.php/Display_manager "Display manager") 항목을 참고하십시오. 디스플레이 관리자를 사용하고 싶지 않다면, [Start X at login](/index.php/Start_X_at_login "Start X at login") 문서에서 가상터미널에서 디스플레이 관리자와 유사한 기능을 사용하는 방법을 찾을 수 있습니다.

### 데스크탑 환경

Xorg가 GUI 환경 구현을 위한 기본적 프레임워크를 제공하지만, 온전한 GUI 환경을 사용하기 위해서는 몇 가지 추가 요소들이 필요합니다. [GNOME](/index.php/GNOME "GNOME"), [KDE](/index.php/KDE "KDE"), [LXDE](/index.php/LXDE "LXDE"), [Xfce](/index.php/Xfce "Xfce") 등의 [데스크탑 환경](/index.php/Desktop_environments "Desktop environments")들은 창 관리자, 패널, 파일관리자, 터미널 에뮬레이터, 텍스트 편집기, 아이콘 등 다양한 *X 클라이언트*를 포함합니다. 추가적인 정보는 [Category:Desktop environments](/index.php/Category:Desktop_environments "Category:Desktop environments")의 항목들에서 얻을 수 있습니다.

## 오디오 및 동영상

[Category:Multimedia](/index.php/Category:Multimedia "Category:Multimedia") 항목에서 멀티미디어에 관한 더 많은 정보를 얻을 수 있습니다.

### 소리

[소리](/index.php/Sound_system "Sound system")는 커널 사운드 드라이버에 의해 제공됩니다.

[ALSA](/index.php/ALSA "ALSA")는 커널에 포함되어 있으며, 음소거만 풀면 바로 사용할 수 있기 때문에 사용이 권장됩니다.

[OSS](/index.php/OSS "OSS")는 ALSA가 작동하지 않을 경우 사용할 수 있습니다.

추가로 [사운드 서버](/index.php/Sound#Sound_servers "Sound")를 설치하고 설정할 수 있습니다. 고급 오디오 설정이 필요하다면 [Pro Audio](/index.php/Pro_Audio "Pro Audio") 항목을 참조하십시오.

### 브라우저 플러그인

풍부하고 *완전한* 웹 브라우징을 위하여 아크로뱃 리더, 자바, 플래시 등 몇 가지 [브라우저 플러그인](/index.php/Browser_plugins "Browser plugins")들을 설치할 수 있습니다.

### 코덱

[코덱](/index.php/Codecs "Codecs")은 멀티미디어 어플리케이션들이 동영상과 오디오 스트림을 디코딩하고 인코딩하는 데에 사용됩니다. 동영상 및 음악 파일을 정상적으로 재생하기 위해서는 알맞는 코덱을 설치해야 합니다.

## 네트워크

이 섹션은 작은 네트워크 작업만을 다룹니다. [Network configuration](/index.php/Network_configuration "Network configuration")에서 더 자세한 설명을 읽을 수 있습니다. 더 많은 정보가 필요하다면 [Category:Networking](/index.php/Category:Networking "Category:Networking")의 문서들을 참조하십시오.

### 시계 동기화

[Network Time Protocol](https://en.wikipedia.org/wiki/Network_Time_Protocol "wikipedia:Network Time Protocol") (NTP)는 패킷 교환, 가변 레이턴시 데이터 네트워크를 통해 컴퓨터 시스템 간 시간 동기화를 위한 네트워크 프로토콜입니다. [Time synchronization](/index.php/Time_synchronization "Time synchronization") 항목에서 아치리눅스에서 어떻게 NTP를 사용할 수 있는지를 확인할 수 있습니다.

### DNS 성능

DNS 캐싱을 통해 웹페이지들을 더 빨리 로드되게 할 수 있습니다. 이를 위해서는 [pdnsd](/index.php/Pdnsd "Pdnsd")를 사용하십시오. [pdnsd](/index.php/Pdnsd "Pdnsd")는 매우 단순한 DNS 서버입니다. [dnsmasq](/index.php/Dnsmasq "Dnsmasq")를 설치하는 것도 좋습니다. dnsmasq는 pdnsd에 비해 시스템을 DHCP 서버로 전환하는 등의 다양한 기능들을 제공합니다.

### DNS 보안

웹 브라우징의 보안성을 높이고 싶거나, 온라인 결재, [SSH](/index.php/SSH "SSH") 연결 등 보안성이 중요한 작업을 해야 한다면 [DNSSEC](/index.php/DNSSEC "DNSSEC")을 사용할 수 있는 소프트웨어를 사용하는 것을 고려하십시오. DNSSEC을 사용하는 소프트웨어는 [DNS](https://en.wikipedia.org/wiki/Domain_Name_System "wikipedia:Domain Name System") 기록의 서명을 확인하여 보안성을 높여주며, [DNSCrypt](/index.php/DNSCrypt "DNSCrypt")를 이용하여 DNS 트래픽을 암호화할 수 있습니다.

### 방화벽 설정하기

[방화벽](/index.php/Firewalls "Firewalls")은 리눅스 네트워크 스택 위에 추가적인 보호 계층을 제공합니다. 리눅스는 [Netfilter](https://en.wikipedia.org/wiki/Netfilter "wikipedia:Netfilter")프로젝트의 일환으로 [stateful firewall](https://en.wikipedia.org/wiki/Stateful_firewall "wikipedia:Stateful firewall")인 iptables를 갖추고 있습니다. iptable 설정은 직접 할 수도 있으며, 자동화된 도구를 사용할 수도 있습니다. 아치리눅스는 아무 포트도 열리지 않은 상태로 제공되며, 네트워크 데몬은 직접 설정하지 않은 경우 자동으로 시작하지 않습니다. 따라서 보호해야 하는 서비스를 실행하고 있지 않다면 방화벽이 반드시 필요하지는 않습니다.

### 윈도우 네트워크 사용하기

윈도와 아치 리눅스 사이의 네트워크 커뮤니케이션을 위해서는 SMB/CIFS 네트워킹 프로토콜을 재구현(reimplement)한 [Samba](/index.php/Samba "Samba")를 사용하실 수 있습니다.

인증을 위해 Active Dictionary에 가입하고 사용하도록 아치 리눅스를 설정하기 위해서는[Active Directory Integration](/index.php/Active_Directory_Integration "Active Directory Integration") 문서를 읽으십시오.

## 부팅

이 섹션은 아치리눅스 부팅 과정에 관련된 정보를 다룹니다. 아치리눅스 부팅 과정에 대한 전반적인 정보는 [Arch boot process](/index.php/Arch_boot_process "Arch boot process")에서 찾을 수 있습니다. 더 자세히 알고 싶다면 [Category:Boot process](/index.php/Category:Boot_process "Category:Boot process")의 문서들을 확인하십시오.

### 하드웨어 자동 감지

[udev](/index.php/Udev "Udev")가 부팅시에 자동으로 하드웨어를 감지할 것입니다. 부팅 시간을 줄일 수 있습니다. [Kernel modules#Loading](/index.php/Kernel_modules#Loading "Kernel modules") 문서에 설명된 대로 모듈 자동 로딩을 해제하고 필요한 모듈을 수동으로 지정하면 부팅 속도가 향상될 수 있습니다. 덧붙여, [Xorg](/index.php/Xorg "Xorg")역시 기본으로는 udev를 통해 하드웨어를 자동 감지하도록 설정되어 있으나 수동으로 설정하는 것도 가능합니다.

### 부팅시에 Num Lock 켜기

Num Lock은 대부분 키보드에서 볼 수 있는 토글 키입니다. 부팅시에 Num Lock을 활성화시켜 Numpad의 숫자를 활성화시키는 방법은 [부팅시에 Numlock 활성화하기](/index.php/Activating_Numlock_on_Bootup "Activating Numlock on Bootup")를 보십시오.

### 부팅 메시지 유지하기

일단 부팅이 끝나고 나면 화면이 지워지고 로그인 프롬프트만 나타나서 사용자들이 부팅 과정에 대한 정보를 얻을 수 없게 만듭니다. 부팅 메시지가 지워지지 않도록 하기 위해서는 [Disable clearing of boot messages](/index.php/Disable_clearing_of_boot_messages "Disable clearing of boot messages")를 보십시오.

### 부팅시에 자동으로 X 시작하기

GUI를 사용하기 위하여 [X](/index.php/X "X")서버를 사용하고 있다면 로그인 한 후에 수동으로 X를 시작하는 것보다는 자동으로 X 세션이 시작되기를 원할 수 있습니다. [Display manager](/index.php/Display_manager "Display manager") 항목을 참조하여 GUI 로그인 화면을 사용할 수 있습니다. 디스플레이 관리자를 사용하고 싶지 않다면 [로그인시에 X 실행하기](/index.php/Start_X_at_login "Start X at login") 항목을 보십시오.

## 전원 관리

이 섹션은 노트북 사용자나 전원 관리를 원하는 사용자에게 유용할 것입니다. 더 자세한 내용은 [Category:Power management](/index.php/Category:Power_management "Category:Power management")의 문서들을 참고하십시오.

### ACPI 이벤트

전원 버튼을 눌렀거나 노트북의 덮개를 닫는 등의 ACPI 이벤트에 대해서 시스템이 어떻게 반응할지 설정할 수 있습니다. 권장되는 방법인 [systemd](/index.php/Systemd "Systemd")를 이용한 설정법을 사용하려면 [Power management with systemd](/index.php/Power_management#Power_management_with_systemd "Power management") 문서로 가십시오. 이전에 이용되던 설정법을 사용하기 위해서는 [acpid](/index.php/Acpid "Acpid")문서로 가십시오

### CPU 주파수 관리

최근의 프로세서들은 발열과 전력 사용을 줄이기 위해 주파수와 전압을 조절할 수 있습니다. 발열이 줄어들면 시스템을 조용하게 사용할 수 있으며, 하드웨어의 수명을 연장할 수 있습니다. [CPU frequency scaling](/index.php/CPU_frequency_scaling "CPU frequency scaling")문서를 참고하십시오.

### 노트북

노트북 모델별 설치 방법에 관련된 문서들을 보려면 [Category:Laptops](/index.php/Category:Laptops "Category:Laptops")를 보십시오. 일반적인 랩탑 관련 문서와 추천사항을 보시려면 [Laptop](/index.php/Laptop "Laptop") 페이지를 보십시오.

### 대기 모드와 최대 절전 모드

본문 [Suspend and hibernate](/index.php/Suspend_and_hibernate "Suspend and hibernate")를 보십시오.

## 입력 장치

이 섹션은 입력장치 설정을 위한 유용한 팁들을 다룹니다. 더 많은 정보는 [Category:Input devices](/index.php/Category:Input_devices "Category:Input devices")의 문서들에서 찾을 수 있습니다.

### 키보드 레이아웃

영어가 아니거나, 비표준적인 키보드 레이아웃을 사용할 경우, 직접 설정하지 않으면 키보드가 원하는대로 작동하지 않을 수 있습니다. 가상터미널과 Xorg에서 해당 키보드 레이아웃을 설정해야 합니다. [Keyboard configuration in console](/index.php/Keyboard_configuration_in_console "Keyboard configuration in console") 문서와 [Keyboard configuration in Xorg](/index.php/Keyboard_configuration_in_Xorg "Keyboard configuration in Xorg") 문서를 참고하세요.

### 마우스 버튼

일반적이지 않은 마우스를 사용한다면 모든 마우스 버튼이 인식되지 않거나, 각 버튼에 추가적으로 기능을 설정하고 싶을 수 있습니다. [All Mouse Buttons Working](/index.php/All_Mouse_Buttons_Working "All Mouse Buttons Working") 문서에서 그 방법을 알아보십시오.

### 노트북 터치패드

대부분의 노트북들은 [Synaptics](http://www.synaptics.com/)나 [ALPS](http://www.alps.com/) "터치패드" 지시 장치를 사용합니다. Synaptics 제품과 ALPS 제품을 비롯하여 몇가지 터치패드 모들을 사용하기 위해서는 Synaptics input 드라이버를 설치하세요. [Touchpad Synaptics](/index.php/Touchpad_Synaptics "Touchpad Synaptics")항목에서 터치패드 드라이버 설치 및 설정에 관한 자세한 정보를 얻을 수 있습니다.

### TrackPoints

Trackpoint 장치를 설정하려면 다음 [ThinkWiki](http://www.thinkwiki.org/wiki/How_to_configure_the_TrackPoint) 문서를 보십시오.

## 최적화

이 섹션은 시스템 및 어플리케이션 성능을 극대화할 때에 유용한 도구, 설정 및 트윅을 요약하여 제공합니다.

### 벤치마크

[벤치마킹](/index.php/Benchmarking "Benchmarking")이란 한 시스템의 성능을 측정하여 다른 시스템과 비교하는 것, 혹은 통일된 절차를 통하여 널리 인정되는 표준과 비교하는 것을 뜻합니다.

### 성능 극대화하기

[Improving performance](/index.php/Improving_performance "Improving performance") 문서는 아치 리눅스 성능에 대한 정보를 모으고, 성능 향상을 위하여 기본적으로 할 수 있는 일의 목록을 제시하는 문서입니다.

### SSD

[Solid State Drives](/index.php/Solid_State_Drives "Solid State Drives")문서는 SSD 수명을 연장하는 방법 등 SSD에 대한 여러 정보를 다룹니다.

## 시스템 서비스

이 섹션은 [daemons](/index.php/Daemons "Daemons")와 연관이 있습니다. 더 자세한 정보는 [Category:Daemons and system services](/index.php?title=Category:Daemons_and_system_services&action=edit&redlink=1 "Category:Daemons and system services (page does not exist)")의 항목들을 확인하십시오.

### 파일 색인 및 검색

대부분의 리눅스 배포판들에는 간편한 파일 검색을 위한 `locate` 명령어가 포함되어 있습니다. 이 기능을 사용하려면 [mlocate](https://www.archlinux.org/packages/?name=mlocate) 패키지를 설치하십시오. mlocate를 설치한 후에는 `updatedb` 명령을 통해 파일 색인을 시작하십시오.

### 로컬 메일 배달

기본적인 아치리눅스 시스템은 메일 동기화 기능을 포함하지 않습니다. *Postfix*를 이용하여 간단한 로컬 메일상자 기능을 사용할 수 있습니다. [Postfix](/index.php/Postfix "Postfix")문서를 참조하십시오. Postfix 대신 [SSMTP](/index.php/SSMTP "SSMTP"). [msmtp](/index.php/Msmtp "Msmtp"), [fdm](/index.php/Fdm "Fdm") 등을 사용하는 것도 가능합니다.

### 프린터 설정

[CUPS](/index.php/CUPS "CUPS")는 애플이 개발하는 표준에 기반한 오픈 소스 프린팅 시스템입니다. [Category:Printers](/index.php/Category:Printers "Category:Printers")의 문서들에서 프린터 모델별 설치 방법을 찾을 수 있습니다.

## 외관

이 섹션은 시스템의 외관을 꾸미기 위하여 자주 사용되는 트윅들을 담고 있습니다. 더 많은 내용은 [Category:Eye candy](/index.php/Category:Eye_candy "Category:Eye candy")의 문서들에서 찾을 수 있습니다.

### 글꼴

[글꼴](/index.php/Fonts "Fonts")과 [글꼴 설정](/index.php/Font_configuration "Font configuration")페이지에서 많은 정보를 얻을 수 있습니다.

#### 콘솔 글꼴

가상 콘솔에서(즉 X 서버 밖에서) 작업하며 많은 시간을 보낸다면 가독성을 높이기 위해 콘솔 글꼴을 변경할 수 있습니다. [Fonts#Console fonts](/index.php/Fonts#Console_fonts "Fonts")를 보세요.

#### 패치된 글꼴 패키지

보다 나은 글꼴 렌더링을 위하여 패치된 글꼴 라이브러리를 사용할 수 있습니다. [Font configuration#Patched packages](/index.php/Font_configuration#Patched_packages "Font configuration") 항목을 보세요.

### GTK 및 QT 테마

리눅스의 GUI 어플리케이션들은 [GTK+](/index.php/GTK%2B "GTK+")나 [Qt](/index.php/Qt "Qt")와 같은 툴킷을 사용하는 것이 많습니다. GTK+ 와 QT 문서 및 [Uniform look for Qt and GTK applications](/index.php/Uniform_look_for_Qt_and_GTK_applications "Uniform look for Qt and GTK applications") 항목을 참조하여 프로그램들의 외양을 향상시키세요.

## 콘솔 향상시키기

이 섹션에서는 콘솔 프로그램들을 더욱 실용적으로 만들기 위한 작은 설정값 변화들을 다룹니다. [[:Category:Command shells]의 문서들에 더 많은 내용이 들어 있습니다.

### Alias 설정하기

명령어 하나 혹은 여러개의 명령어를 단축 명령어(Alias)로 등록하는 것은 콘솔 사용 중에 시간을 절약하는 한 방법입니다. 특히 파라미터에 큰 변화 없이 반복되는 작업의 경우에 단축 명령어는 매우 유용할 수 있습니다. 흔한 단축 명령어들을 [Bash#Aliases](/index.php/Bash#Aliases "Bash") 항목에서 볼 수 있습니다. [Bash#Aliases](/index.php/Bash#Aliases "Bash") 항목에서 다루는 단축 명령어는 [zsh](/index.php/Zsh "Zsh")로도 쉽게 옮길 수 있습니다.

### 다른 쉘 사용하기

아치 리눅스에 기본으로 설치되는 쉘은 [Bash](/index.php/Bash "Bash") 입니다. 하지만 설치매체에서는 [grml-zsh-config](https://www.archlinux.org/packages/?name=grml-zsh-config) 추가 패키지를 통해 [zsh](/index.php/Zsh "Zsh")를 기본 쉘로 사용합니다. [Command-line shell#List of shells](/index.php/Command-line_shell#List_of_shells "Command-line shell") 항목에서 bash 대신 사용할 수 있는 쉘의 목록을 볼 수 있습니다.

### Bash 추가기능

자동완성 기능 개선, 기록 검색, readline 매크로 등 기타 Bash에서 설정할 수 있는 개선사항 목록은 [Bash#Tips and tricks](/index.php/Bash#Tips_and_tricks "Bash")에서 보실 수 있습니다.

### 컬러 출력

많은 어플리케이션이 기본적으로 컬러 기능을 가지고 있지만, `cope`과 같은 도구를 이용하여 컬러 기능을 사용하는 것도 가능합니다. [AUR](/index.php/AUR "AUR")에서 [cope-git](https://aur.archlinux.org/packages/cope-git/)나 더 자주 업데이트되는 [Git](/index.php/Git "Git")버전인 [cope-git](https://aur.archlinux.org/packages/cope-git/)를 설치하십시오. 유사한 소프트웨어인 [acoc](https://aur.archlinux.org/packages/acoc/)를 사용하실 수도 있습니다.

#### 핵심(Core) 유틸리티

**grep**나 **ls**와 같은 특정 핵심 유틸리티를 컬러로 출력하는 방법은 [핵심 유틸리티](/index.php/Core_utilities "Core utilities") 문서에서 다룹니다.

#### Man 페이지

Man 페이지 (혹은 매뉴얼 페이지)는 GNU/리눅스 유저에게 매우 유용한 자료입니다. 가독성을 향상시키기 위해 [man page#Colored man pages](/index.php/Man_page#Colored_man_pages "Man page")에 설명된 대로 컬러 텍스트를 보여주도록 man pager을 설정할 수 있습니다.

### 압축파일

아카이브라고도 불리는 압축파일들은 GNU/리눅스 시스템을 사용하다보면 자주 접하게 됩니다. [Tar](/index.php/Tar "Tar")은 가장 흔한 압축 파일 도구 중 하나이며, 사용자들은 Tar의 명령 형식에 익숙해지는 것이 좋습니다(예를 들어, 아치리눅스의 패키지 파일들도 xz으로 압축된 타르볼(tarball)입니다.)

### 콘솔 프롬프트

콘솔 프롬프트(PS1) 역시 많은 부분을 개인화할 수 있습니다. Bash를 사용한다면 [Color Bash Prompt](/index.php/Color_Bash_Prompt "Color Bash Prompt") 문서를, zsh를 사용한다면 [zsh#Prompts](/index.php/Zsh#Prompts "Zsh") 항목을 참고하십시오.

### 이맥스 쉘

이맥스는 텍스트 편집기 이상의 기능을 제공하는 것으로 유명합니다. 이맥스의 기능 중 하나는 이맥스를 쉘로 사용하는 것입니다. [Emacs#Colored output issues](/index.php/Emacs#Colored_output_issues "Emacs")에서 컬러 출력으로 인한 문자 깨짐에 대한 해결법을 알아보십시오.

### 마우스 지원

콘솔에서 마우스를 이용하여 복사와 붙여넣기를 하는 것은 [GNU Screen](/index.php/GNU_Screen "GNU Screen")의 전통적인 복사 모드보다 유용할 수 있습니다. [Console mouse support](/index.php/Console_mouse_support "Console mouse support")문서에서 콘솔에서 마우스를 사용하는 방법에 대한 자세한 정보를 찾을 수 있습니다.

### 스크롤백 버퍼

스크린 밖으로 밀려난 텍스트를 저장하고 보기 위해서는 [Scrollback buffer](/index.php/Scrollback_buffer "Scrollback buffer")를 보십시오.

### 세션 관리

[tmux](/index.php/Tmux "Tmux")나 [GNU Screen](/index.php/GNU_Screen "GNU Screen")과 같은 다중 터미널 장치를 사용하면 프로그램을 임의로 탈착할 수 있는 탭과 pane으로 이루어진 세션 속에서 실행할 수 있습니다. 이럴 경우, 터미널 에뮬레이터를 끄거나, [X](/index.php/X "X") 세션을 종료하거나 로그오프하더라도 다중 터미널 장치 서버가 작동하고 있는 한 세션들 안에서 실행되고 있는 프로그램들은 계속해서 백그라운드에서 실행될 것입니다. 세션을 다시 부착해야 세션 속의 프로그램들과 상호작용할 수 있습니다.