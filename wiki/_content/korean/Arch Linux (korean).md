<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 아치 리눅스가 무엇입니까?](#아치_리눅스가_무엇입니까?)
*   [2 장점](#장점)
*   [3 독특한 패키지 관리](#독특한_패키지_관리)
*   [4 최신](#최신)
*   [5 간결함](#간결함)
*   [6 더 읽을거리](#더_읽을거리)

## 아치 리눅스가 무엇입니까?

아치 리눅스는 롤링-릴리즈 패키지 모델에 기반하고 GNU/리눅스 사용자들의 요구를 충족시키는데 목표를 둔 독립적으로 개발되는 i686/x86-64 최적화된 커뮤니티 배포판입니다. 개발은 최소주의, 우아함, 코드의 확실함과 최신의 균형에 촛점을 맞춥니다. 버전 0.1 (호머)는 2002년 3월 11일 출시되었습니다.

## 장점

아치는 설치시 i686/x86-64 아키텍처용으로 이미 컴파일 및 최적화된 최소의 환경(GUI 없음)을 제공합니다. 아치는 가볍고 유연하며 간결합니다. 이 설계 철학과 구현은 쉽게 확장할 수 있게 하고 당신이 만들고 있는 어떤 종류의 시스템-최소한의 콘솔 기계부터 가장 장대하고 기능이 풍부한 데스크탑 환경-으로든 녹아듭니다. 아치는 필요없고 원하지 않는 패키지를 제거하는 것보다, 기본값으로 선택되지 않은 최소한의 기초부터 구축할 수 있는 능력을 지닌 강력한 사용자를 원합니다. 아치 리눅스가 무엇이 될 것인지는 *사용자*가 결정하는 것입니다.

## 독특한 패키지 관리

아치는 당신의 전체 시스템을 한 명령으로 업그레이드할 수 있게 해주는 - [pacman (한국어)](/index.php/Pacman_(%ED%95%9C%EA%B5%AD%EC%96%B4) "Pacman (한국어)") - 사용하기 쉬운 바이너리 패키지 시스템에 의해 뒷받침됩니다. pacman은 **C**로 작성되었고 밑바닥부터 가볍고 간결하며 매우 빠르게 설계되었습니다. 아치는 한 명령으로 동기화할 수 있는, 소스로부터 패키지를 빌드하고 설치하는 것을 쉽게 해주는 ports 같은 패키지 빌드 시스템 ([Arch Build System](/index.php/Arch_Build_System "Arch Build System"))도 사용합니다. 심지어 하나의 명령으로 전체 시스템을 다시 만들 수도 있습니다. 모든 것이 매우 간결하고 투명하게 이루어집니다. 롤링 릴리즈 모델은 재설치 또는 한 버전에서 다음 버전으로 복잡한 시스템 업그레이드를 수행하지 않고, 설치와 지속적으로 원활한 업데이트를 한번에 할 수 있도록 허용합니다.

## 최신

아치 리눅스는 롤링 릴리즈 시스템에 기반하여 소프트웨어의 최신 안정 버전을 유지하기 위해 분투하고 있습니다. 우리는 현재 최소한의 i686과 x86-64 기반 시스템를 위한 능률적인 핵심 패키지, 개발자와 사용자 모두에 의해 유지되는 저장소의 수천개의 추가적인 고품질 바이너리 패키지, 그리고 소스로부터 빌드와 패키지를 위한 수천개의 PKGBUILD 스크립트를 지원합니다. 아치는 패치가 없는 순수한 소프트웨어를 제공합니다; 패키지는 저작자가 배포하려고 의도한 순수한 원시 소스가 제공됩니다. 패치 작업은 극도로 희귀한 경우로 롤링 릴리즈 모델 하의 버전 불일치의 인스턴스에서 일어날 수 있는 심각한 파손을 방지하기 위해 발생합니다. 아치는 GNU/리눅스 사용자에게 최신 파일시스템 (Ext2/3, Reiser, XFS, JFS), LVM2/EVMS, 소프트웨어 RAID, udev 지원 및 initcpio 를 포함하는 많은 새로운 기능을 부여합니다.

## 간결함

[아치의 도(道)](/index.php/The_Arch_Way_(%ED%95%9C%EA%B5%AD%EC%96%B4) "The Arch Way (한국어)")는 간결함을 유지하려는 철학입니다. 아치 리눅스 기반 시스템은 GNU/리눅스 환경으로서 최소한으로 매우 간결합니다. 리눅스 커널, GNU 툴체인, 그리고 links와 Vi같은 명령행 유틸리티는 선택적입니다. 이 깔끔하고 간결한 출발점은 사용자가 필요한 무엇이든 시스템을 확장하는 단단한 기반을 제공합니다.

아치의 간결한 init 시스템은 각 실행수준에 대한 수십 개의 심볼릭 링크를 포함하는 뒤얽힌 디렉토리 구조보다 단일 파일(etc/rc.conf)으로부터 통합 호출하는 *BSD 방식에 큰 영감을 받았습니다.

시스템 설정은 간단한 텍스트 파일 편집을 통해 이뤄집니다.

## 더 읽을거리

사용자 게시판, 공식 문서, 그리고 아치에 대한 모든 것에 대한 링크를 찾을 수 있는 아치의 홈페이지는 [https://www.archlinux.org/](https://www.archlinux.org/) 입니다. 여기서 잃어버린 약간의 통찰력을 위해 [아치의 도(道)](/index.php/The_Arch_Way_(%ED%95%9C%EA%B5%AD%EC%96%B4) "The Arch Way (한국어)") 또한 읽을 수 있습니다.