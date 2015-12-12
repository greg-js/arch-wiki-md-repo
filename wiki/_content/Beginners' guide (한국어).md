# Beginners' guide (한국어)

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

**도움말:** 이 안내서는 전체를 한 문서에서 보는 방법 외에도 여러 문서로 나누어서 볼 수도 있습니다. 나누어진 문서를 보려면 **[여기](/index.php/Beginners%27_Guide/Preface_(%ED%95%9C%EA%B5%AD%EC%96%B4) "Beginners' Guide/Preface (한국어)")**에서부터 시작하십시오.

관련 항목

*   [Category:Accessibility](/index.php/Category:Accessibility "Category:Accessibility")
*   [Installation Guide (한국어)](/index.php/Installation_Guide_(%ED%95%9C%EA%B5%AD%EC%96%B4) "Installation Guide (한국어)")
*   [Install from SSH](/index.php/Install_from_SSH "Install from SSH")
*   [General Recommendations (한국어)](/index.php/General_Recommendations_(%ED%95%9C%EA%B5%AD%EC%96%B4) "General Recommendations (한국어)")
*   [General Troubleshooting](/index.php/General_Troubleshooting "General Troubleshooting")

이 문서는 [아치 설치 스크립트](https://github.com/falconindy/arch-install-scripts)를 사용하여 [Arch Linux](/index.php/Arch_Linux "Arch Linux")를 설치하는 과정을 안내합니다. 설치하기에 앞서 [FAQ](/index.php/FAQ "FAQ")를 읽어 보세요.

아치리눅스 커뮤니티가 관리하는 [Arch wiki](/index.php/Main_page "Main page")는 아주 좋은 자료로 문제가 생기면 가장 먼저 찾아봐야 합니다. [IRC](https://en.wikipedia.org/wiki/IRC "wikipedia:IRC") 채널([irc://irc.freenode.net/#archlinux](irc://irc.freenode.net/#archlinux), [irc://irc.freenode.net/#archlinux-ko](irc://irc.freenode.net/#archlinux-ko) )과 [포럼](https://bbs.archlinux.org/) 또한 문제를 해결할 때 이용할 수 있습니다. 특정 명령어에 대한 도움말을 원하신다면 `man` 항목을 읽어보십시오. `man` 항목은 보통 `man _명령어_`로 볼 수 있습니다.

## Contents

*   [1 준비하기](#.EC.A4.80.EB.B9.84.ED.95.98.EA.B8.B0)
    *   [1.1 시스템 요구사항](#.EC.8B.9C.EC.8A.A4.ED.85.9C_.EC.9A.94.EA.B5.AC.EC.82.AC.ED.95.AD)
    *   [1.2 최신 설치매체 준비하기](#.EC.B5.9C.EC.8B.A0_.EC.84.A4.EC.B9.98.EB.A7.A4.EC.B2.B4_.EC.A4.80.EB.B9.84.ED.95.98.EA.B8.B0)
        *   [1.2.1 네트워크를 통해 설치하기](#.EB.84.A4.ED.8A.B8.EC.9B.8C.ED.81.AC.EB.A5.BC_.ED.86.B5.ED.95.B4_.EC.84.A4.EC.B9.98.ED.95.98.EA.B8.B0)
        *   [1.2.2 기존에 설치한 리눅스 시스템에서 아치리눅스 설치하기](#.EA.B8.B0.EC.A1.B4.EC.97.90_.EC.84.A4.EC.B9.98.ED.95.9C_.EB.A6.AC.EB.88.85.EC.8A.A4_.EC.8B.9C.EC.8A.A4.ED.85.9C.EC.97.90.EC.84.9C_.EC.95.84.EC.B9.98.EB.A6.AC.EB.88.85.EC.8A.A4_.EC.84.A4.EC.B9.98.ED.95.98.EA.B8.B0)
        *   [1.2.3 가상 머신에 설치하기](#.EA.B0.80.EC.83.81_.EB.A8.B8.EC.8B.A0.EC.97.90_.EC.84.A4.EC.B9.98.ED.95.98.EA.B8.B0)
        *   [1.2.4 아치리눅스 설치매체로 부팅하기](#.EC.95.84.EC.B9.98.EB.A6.AC.EB.88.85.EC.8A.A4_.EC.84.A4.EC.B9.98.EB.A7.A4.EC.B2.B4.EB.A1.9C_.EB.B6.80.ED.8C.85.ED.95.98.EA.B8.B0)
            *   [1.2.4.1 UEFI 모드로 부팅했는지 확인하기](#UEFI_.EB.AA.A8.EB.93.9C.EB.A1.9C_.EB.B6.80.ED.8C.85.ED.96.88.EB.8A.94.EC.A7.80_.ED.99.95.EC.9D.B8.ED.95.98.EA.B8.B0)
        *   [1.2.5 부팅 문제 해결](#.EB.B6.80.ED.8C.85_.EB.AC.B8.EC.A0.9C_.ED.95.B4.EA.B2.B0)
*   [2 설치하기](#.EC.84.A4.EC.B9.98.ED.95.98.EA.B8.B0)
    *   [2.1 언어 변경하기](#.EC.96.B8.EC.96.B4_.EB.B3.80.EA.B2.BD.ED.95.98.EA.B8.B0)
    *   [2.2 인터넷 연결 설정하기](#.EC.9D.B8.ED.84.B0.EB.84.B7_.EC.97.B0.EA.B2.B0_.EC.84.A4.EC.A0.95.ED.95.98.EA.B8.B0)
        *   [2.2.1 유선 네트워크](#.EC.9C.A0.EC.84.A0_.EB.84.A4.ED.8A.B8.EC.9B.8C.ED.81.AC)
        *   [2.2.2 무선 네트워크](#.EB.AC.B4.EC.84.A0_.EB.84.A4.ED.8A.B8.EC.9B.8C.ED.81.AC)
            *   [2.2.2.1 wifi-menu를 사용하지 않고 와이파이에 연결하기](#wifi-menu.EB.A5.BC_.EC.82.AC.EC.9A.A9.ED.95.98.EC.A7.80_.EC.95.8A.EA.B3.A0_.EC.99.80.EC.9D.B4.ED.8C.8C.EC.9D.B4.EC.97.90_.EC.97.B0.EA.B2.B0.ED.95.98.EA.B8.B0)
        *   [2.2.3 xDSL (PPPoE), 아날로그 모뎀 혹은 ISDN](#xDSL_.28PPPoE.29.2C_.EC.95.84.EB.82.A0.EB.A1.9C.EA.B7.B8_.EB.AA.A8.EB.8E.80_.ED.98.B9.EC.9D.80_ISDN)
        *   [2.2.4 프록시 서버를 경유할 경우](#.ED.94.84.EB.A1.9D.EC.8B.9C_.EC.84.9C.EB.B2.84.EB.A5.BC_.EA.B2.BD.EC.9C.A0.ED.95.A0_.EA.B2.BD.EC.9A.B0)
    *   [2.3 하드디스크 준비하기](#.ED.95.98.EB.93.9C.EB.94.94.EC.8A.A4.ED.81.AC_.EC.A4.80.EB.B9.84.ED.95.98.EA.B8.B0)
        *   [2.3.1 파티션 테이블 종류 선택](#.ED.8C.8C.ED.8B.B0.EC.85.98_.ED.85.8C.EC.9D.B4.EB.B8.94_.EC.A2.85.EB.A5.98_.EC.84.A0.ED.83.9D)
        *   [2.3.2 파티션 도구](#.ED.8C.8C.ED.8B.B0.EC.85.98_.EB.8F.84.EA.B5.AC)
        *   [2.3.3 파티션 테이블 지우기](#.ED.8C.8C.ED.8B.B0.EC.85.98_.ED.85.8C.EC.9D.B4.EB.B8.94_.EC.A7.80.EC.9A.B0.EA.B8.B0)
        *   [2.3.4 파티션 구성하기](#.ED.8C.8C.ED.8B.B0.EC.85.98_.EA.B5.AC.EC.84.B1.ED.95.98.EA.B8.B0)
        *   [2.3.5 예시](#.EC.98.88.EC.8B.9C)
            *   [2.3.5.1 cgdisk로 GPT 파티션 만들기](#cgdisk.EB.A1.9C_GPT_.ED.8C.8C.ED.8B.B0.EC.85.98_.EB.A7.8C.EB.93.A4.EA.B8.B0)
            *   [2.3.5.2 fdisk로 MBR 파티션 만들기](#fdisk.EB.A1.9C_MBR_.ED.8C.8C.ED.8B.B0.EC.85.98_.EB.A7.8C.EB.93.A4.EA.B8.B0)
        *   [2.3.6 파일시스템 만들기](#.ED.8C.8C.EC.9D.BC.EC.8B.9C.EC.8A.A4.ED.85.9C_.EB.A7.8C.EB.93.A4.EA.B8.B0)
    *   [2.4 파티션 마운트하기](#.ED.8C.8C.ED.8B.B0.EC.85.98_.EB.A7.88.EC.9A.B4.ED.8A.B8.ED.95.98.EA.B8.B0)
    *   [2.5 미러 사이트 선택하기](#.EB.AF.B8.EB.9F.AC_.EC.82.AC.EC.9D.B4.ED.8A.B8_.EC.84.A0.ED.83.9D.ED.95.98.EA.B8.B0)
    *   [2.6 기반 시스템 설치하기](#.EA.B8.B0.EB.B0.98_.EC.8B.9C.EC.8A.A4.ED.85.9C_.EC.84.A4.EC.B9.98.ED.95.98.EA.B8.B0)
    *   [2.7 fstab 생성하기](#fstab_.EC.83.9D.EC.84.B1.ED.95.98.EA.B8.B0)
    *   [2.8 시스템에 chroot로 들어가기](#.EC.8B.9C.EC.8A.A4.ED.85.9C.EC.97.90_chroot.EB.A1.9C_.EB.93.A4.EC.96.B4.EA.B0.80.EA.B8.B0)
        *   [2.8.1 로케일](#.EB.A1.9C.EC.BC.80.EC.9D.BC)
            *   [2.8.1.1 영어가 아닌 언어에 대한 예시](#.EC.98.81.EC.96.B4.EA.B0.80_.EC.95.84.EB.8B.8C_.EC.96.B8.EC.96.B4.EC.97.90_.EB.8C.80.ED.95.9C_.EC.98.88.EC.8B.9C)
        *   [2.8.2 콘솔 폰트와 키맵](#.EC.BD.98.EC.86.94_.ED.8F.B0.ED.8A.B8.EC.99.80_.ED.82.A4.EB.A7.B5)
        *   [2.8.3 시간대](#.EC.8B.9C.EA.B0.84.EB.8C.80)
        *   [2.8.4 하드웨어 시계](#.ED.95.98.EB.93.9C.EC.9B.A8.EC.96.B4_.EC.8B.9C.EA.B3.84)
        *   [2.8.5 커널 모듈](#.EC.BB.A4.EB.84.90_.EB.AA.A8.EB.93.88)
        *   [2.8.6 호스트 네임](#.ED.98.B8.EC.8A.A4.ED.8A.B8_.EB.84.A4.EC.9E.84)
    *   [2.9 네트워크 설정하기](#.EB.84.A4.ED.8A.B8.EC.9B.8C.ED.81.AC_.EC.84.A4.EC.A0.95.ED.95.98.EA.B8.B0)
        *   [2.9.1 유선 네트워크](#.EC.9C.A0.EC.84.A0_.EB.84.A4.ED.8A.B8.EC.9B.8C.ED.81.AC_2)
            *   [2.9.1.1 유동 IP](#.EC.9C.A0.EB.8F.99_IP)
            *   [2.9.1.2 고정 IP](#.EA.B3.A0.EC.A0.95_IP)
        *   [2.9.2 무선 네트워크](#.EB.AC.B4.EC.84.A0_.EB.84.A4.ED.8A.B8.EC.9B.8C.ED.81.AC_2)
            *   [2.9.2.1 무선 네트워크 추가하기](#.EB.AC.B4.EC.84.A0_.EB.84.A4.ED.8A.B8.EC.9B.8C.ED.81.AC_.EC.B6.94.EA.B0.80.ED.95.98.EA.B8.B0)
            *   [2.9.2.2 알고 있는 네트워크에 자동으로 연결](#.EC.95.8C.EA.B3.A0_.EC.9E.88.EB.8A.94_.EB.84.A4.ED.8A.B8.EC.9B.8C.ED.81.AC.EC.97.90_.EC.9E.90.EB.8F.99.EC.9C.BC.EB.A1.9C_.EC.97.B0.EA.B2.B0)
            *   [2.9.2.3 GRUB](#GRUB)
    *   [2.10 파티션을 언마운트 시키고 재부팅하기](#.ED.8C.8C.ED.8B.B0.EC.85.98.EC.9D.84_.EC.96.B8.EB.A7.88.EC.9A.B4.ED.8A.B8_.EC.8B.9C.ED.82.A4.EA.B3.A0_.EC.9E.AC.EB.B6.80.ED.8C.85.ED.95.98.EA.B8.B0)
*   [3 설치 후](#.EC.84.A4.EC.B9.98_.ED.9B.84)

## 준비하기

**참고:** 만약 여러분이 다른 GNU/리눅스 배포판 또는 라이브CD를 이용해서 다른 파티션에 설치하길 원한다면, [이 wiki 문서](/index.php/Install_from_Existing_Linux "Install from Existing Linux")를 봐주세요. 만약 여러분이 원격으로 [VNC](/index.php/VNC "VNC")나 [SSH](/index.php/SSH "SSH")를 통해 아치리눅스를 설치하려고 한다면 특히 유용할 것입니다.

### 시스템 요구사항

아치리눅스는 64MB 이상의 메모리와 [i686](https://en.wikipedia.org/wiki/P6_(microarchitecture) "wikipedia:P6 (microarchitecture)")와 호환되는 CPU가 탑재된 모든 컴퓨터에서 작동합니다. [base](https://www.archlinux.org/groups/x86_64/base/) 그룹의 모든 패키지만을 설치할 경우, 800MB 이하의 디스크 공간을 차지합니다. 만일 디스크 용량이 제한적이라면, 그 이하로도 줄일 수 있습니다. 다만 이를 위해서는 무엇을 설치해야 하는지 정확히 이해해고 있어야 합니다.

### 최신 설치매체 준비하기

[여기](https://archlinux.org/download/)에서 아치리눅스의 공식 설치 매체를 얻을 수 있습니다. 이 설치 매체는 32 비트와 64비트 아키텍처를 동시에 지원합니다. 항상 가장 최근의 설치 매체를 사용하는 것이 좋습니다.

**도움말:** [archboot](https://downloads.archlinux.de/iso/archboot/latest) 설치 매체를 사용할 경우, 이 가이드에서 설명하는 몇 가지 단계를 [대화형으로 진행](/index.php/Archboot#Interactive_setup_features "Archboot")할 수 있습니다. [Archboot](/index.php/Archboot "Archboot") 문서에서 더 자세한 내용을 읽으실 수 있습니다.

*   아치리눅스 설치 매체는 전자 서명이 되어 있으며, 설치하기 전에 서명을 확인하는 것이 좋습니다. 다운로드 페이지나 사용하신 미러에서 _.sig_ 파일을 같이 다운로드하십시오. 아치리눅스 환경에서는 루트 권한으로 `pacman-key -v _설치매체_파일_.sig` 를 실행하면 됩니다. 다른 환경에서는 루트 권한으로 gpg2를 이용하여 서명을 확인할 수 있습니다. 루트 권한으로 `gpg2 --verify _설치매체_파일_.sig`을 실행하십시오. 파일 무결성 확인을 위한 md5, sha1 체크섬 역시 제공되고 있습니다.

    **참고:** 서명에 사용된 RSA 키에 해당하는 공개키를 다운로드하지 않고 gpg2를 이용할 경우, 확인 절차가 실패합니다. [http://sparewotw.wordpress.com/2012/10/31/how-to-verify-signature-using-sig-file/](http://sparewotw.wordpress.com/2012/10/31/how-to-verify-signature-using-sig-file/) 에서 더 상세한 설명을 읽을 수 있습니다

*   적절한 소프트웨어를 이용해서 .iso 파일을 CD나 DVD에 구우십시오. 아치리눅스 환경에서 구울 경우 [Optical disc drive#Burning](/index.php/Optical_disc_drive#Burning "Optical disc drive") 문서를 참고하십시오.

**참고:** CD 미디어나 광학 드라이브의 질은 매우 편차가 큽니다. 일반적으로 오류를 최대한 줄이기 위해 느리게 기록하는 것을 추천합니다. 몇몇 사용자들은 _**2배속 또는 4배속 정도까지 느린**_ 속도를 추천합니다. 만약 CD로부터 오류가 발생한다면, 가능한 한 가장 느린 속도로 기록하시기 바랍니다.

*   혹은 .iso이미지를 USB 드라이브에 기록하실수도 있습니다. [USB Installation Media](/index.php/USB_Installation_Media "USB Installation Media")에서 상세한 설명을 보십시오.

**참고:** 만약 [UEFI](/index.php/UEFI "UEFI") 마더보드를 사용한다면 [여기](/index.php/UEFI#Create_UEFI_bootable_USB_from_ISO "UEFI")와 [여기](/index.php/USB_Installation_Media#Without_overwriting_the_USB_drive "USB Installation Media")를 보십시오.

#### 네트워크를 통해 설치하기

디스크나 USB 드라이브에 설치 매체를 기록하는 대신에, 네트워크를 통해 ISO 이미지로 부팅할 수 있습니다. 이미 작동하고 있는 서버가 있을 경우에 네트워크 설치가 좋을 수 있습니다. 네트워크 설치를 원하실 경우 반드시 [PXE](/index.php/PXE "PXE") 문서를 읽은 후, [아치리눅스 설치도구로 부팅하기](#.EC.95.84.EC.B9.98.EB.A6.AC.EB.88.85.EC.8A.A4_.EC.84.A4.EC.B9.98.EB.8F.84.EA.B5.AC.EB.A1.9C_.EB.B6.80.ED.8C.85.ED.95.98.EA.B8.B0_2) 섹션으로 넘어가십시오.

#### 기존에 설치한 리눅스 시스템에서 아치리눅스 설치하기

이미 작동하고 있는 리눅스 시스템이 있다면 그 리눅스 시스템을 이용하여 아치리눅스를 설치하는 것도 가능합니다. [Install from Existing Linux](/index.php/Install_from_Existing_Linux "Install from Existing Linux") 문서를 참고하십시오. 이 방법은 아치를 [VNC](/index.php/VNC "VNC")나 [SSH](/index.php/SSH "SSH")를 통해 원격으로 설치할 경우 특히 유용합니다. 아치를 [SSH](/index.php/SSH "SSH")를 통해 원격 설치하려는 사용자는 [Install from SSH](/index.php/Install_from_SSH "Install from SSH")문서를 참고하십시오.

#### 가상 머신에 설치하기

[가상 머신](https://en.wikipedia.org/wiki/Virtual_machine "wikipedia:Virtual machine")에 아치리눅스를 설치하는 것은 현재 사용하고 있는 운영체제에서 나오거나 새로운 파티션을 만들 필요 없이 아치리눅스에 익숙해지기에 좋은 방법입니다. 또한 이 방법을 사용하면 설치하는 동안 웹 브라우저로 이 초보자 안내서를 읽을 수 있습니다. 아치리눅스를 테스트 목적으로 설치하는 사용자라면 가상 드라이브에 독립적인 아치리눅스 시스템을 설치하는 것이 바람직할 수 있습니다.

가상 소프트웨어의 대표적인 예로는 [VirtualBox](/index.php/VirtualBox "VirtualBox"), [VMware](/index.php/VMware "VMware"), [QEMU](/index.php/QEMU "QEMU"), [Xen](/index.php/Xen "Xen"), [Parallels](/index.php/Parallels "Parallels")가 있습니다.

가상 머신을 준비하는 과정은 소프트웨어에 따라 조금씩 다르지만, 일반적으로 다음의 과정을 따릅니다:

1.  OS가 설치될 가상의 디스크 이미지를 만듭니다.
2.  버추얼 머신의 환경을 적절하게 구성합니다.
3.  다운로드받은 .iso 이미지를 가상 CD 드라이브에 넣어 가상 머신을 부팅합니다.
4.  [아치리눅스 설치도구로 부팅하기](#.EC.95.84.EC.B9.98.EB.A6.AC.EB.88.85.EC.8A.A4_.EC.84.A4.EC.B9.98.EB.8F.84.EA.B5.AC.EB.A1.9C_.EB.B6.80.ED.8C.85.ED.95.98.EA.B8.B0)로 넘어가 설명을 따릅니다.

다음의 문서들이 도움이 될 수 있습니다:

*   [Arch Linux as VirtualBox guest](/index.php/VirtualBox#Installation_steps_for_Arch_Linux_guests "VirtualBox")
*   [Installing Arch Linux from VirtualBox](/index.php/Installing_Arch_Linux_from_VirtualBox "Installing Arch Linux from VirtualBox")
*   [Arch Linux as VirtualBox guest on a physical drive](/index.php/VirtualBox_Arch_Linux_Guest_On_Physical_Drive "VirtualBox Arch Linux Guest On Physical Drive")
*   [Arch Linux as VMware guest](/index.php/Installing_Arch_Linux_in_VMware "Installing Arch Linux in VMware")
*   [Moving an existing install into (or out of) a virtual machine](/index.php/Moving_an_existing_install_into_(or_out_of)_a_virtual_machine "Moving an existing install into (or out of) a virtual machine")

#### 아치리눅스 설치매체로 부팅하기

대부분의 컴퓨터에서는 [POST](https://en.wikipedia.org/wiki/Power-on_self_test "wikipedia:Power-on self test") 단계에서 부트 장치를 선택할 수 있습니다. 일반적으로 바이오스 화면이 나타날 때 `F12` 키를 누르면 됩니다. 아치리눅스 설치매체를 기록한 장치를 선택합니다. 어떤 컴퓨터들에서는 바이오스에서 부팅 순서를 바꿔야 할 수 있습니다.

[POST](https://en.wikipedia.org/wiki/Power-on_self_test "wikipedia:Power-on self test") 단계에서 특정 키(일반적으로 `Delete`, `F1`, `F2`, `F11`, `F12` 등)를 눌러 바이오스 메뉴로 진입하십시오. 바이오스 메뉴에서 부팅 장치의 순서를 조정하여 아치리눅스 iso가 기록된 장치에서 가장 먼저 부팅을 시도하도록 설정하십시오. 그리고 "save & exit(저장하고 나가기)" (혹은 자신의 바이오스에서 save & exit에 해당하는 것) 을 선택하십시오. 컴퓨터가 부팅을 시작할 것입니다.

아치 메뉴가 나타나면 메뉴에서 "Boot Arch Linux"를 선택하고 `Enter`를 누르십시오. 설치 과정 동안 사용할 라이브 환경이 로드됩니다. (UEFI 시동 디스크로 부팅했을 경우, 메뉴가 "Arch Linux archiso x86_64 UEFI" 와 같이 나타날 수 있습니다)

##### UEFI 모드로 부팅했는지 확인하기

[UEFI](/index.php/Unified_Extensible_Firmware_Interface "Unified Extensible Firmware Interface") 마더보드를 사용하고 UEFI 부팅 모드가 활성화되었을 경우(그리고 UEFI를 BIOS/Legacy 모드보다 선호하도록 설정되었을 경우), CD나 USB가 자동으로 [Gummiboot](/index.php/Gummiboot "Gummiboot")을 이용하여 아치리눅스를 부팅할 것입니다. 이 경우, 검은 바탕에 흰 글씨로 다음과 같은 메뉴가 나타납니다.

```
Arch Linux archiso x86_64 UEFI USB
UEFI Shell x86_64 v1
UEFI Shell x86_64 v2
EFI Default Loader
```

만일 부팅시에 어느 메뉴를 사용했는지 기억이 나지 않거나, UEFI 모드로 부팅했다는 것을 확인하기 위해서는

```
# efivar -l

```

명령을 내리십시오. _efivar_이 UEFI 변수들을 정확하게 나열했다면, UEFI 모드로 부팅한 것입니다. 만일 _efivar_이 UEFI 변수들을 정확히 나열하지 않았다면, [Unified Extensible Firmware Interface](/index.php/Unified_Extensible_Firmware_Interface#Requirements_for_UEFI_Variables_support_to_work_properly "Unified Extensible Firmware Interface")에 나와있는 요구 사항을 만족시켰는지 확인하십시오.

#### 부팅 문제 해결

*   인텔 비디오 칩셋을 사용하며, 부팅 과정에서 화면에 아무것도 나오지 않는다면, 아마 커널 모드 세팅([KMS](/index.php/Kernel_Mode_Setting "Kernel Mode Setting"))의 문제일 것입니다. 해결을 위해서는 재부팅을 하고, 메뉴에서 부팅하기를 원하는 항목(i686이나 x86_64)을 선택하고 `Tab`을 누릅니다. 화면에 나오는 문자열의 끝에 `nomodset`을 추가하고 `Enter`를 누릅니다. `nomodset` 대신 `video=SVIDEO-1:d`를 추가하셔도 됩니다. `video=SVIDEO-1:d`는 커널 모드 세팅을 비활성화하지 않습니다. `i915.modeset=0`를 추가하는 것도 가능합니다. 관련 내용은 [Intel](/index.php/Intel "Intel")항목을 참고하십시오.

*   만약 화면이 공백 상태로 가지 _않고_ 커널을 로딩하는 중에 부팅이 멈춘다면, 메뉴 항목을 선택한 상테에서 `Tab`키를 눌러 다음 내용을 추가해 준 다음 `Enter`키를 눌러주십시오.

```
`acpi=off`

```

## 설치하기

이제 자동으로 루트 사용자로 로그인 된 쉘 프롬프트가 제공됩니다. [Zsh](/index.php/Zsh "Zsh")가 기본 쉘입니다. [Zsh](/index.php/Zsh "Zsh")는 편리한 탭 자동완성 기능을 비롯하여 [grml config](http://grml.org/zsh/)에 나와있는 다양한 기능들을 제공합니다. 텍스트 파일 편집을 위해서는 터미널 내에서 사용할 수 있는 _nano_를 추천합니다. nano에 익숙하지 않다면, [nano#nano usage](/index.php/Nano#nano_usage "Nano")를 참고하십시오. 윈도우와 듀얼부팅을 할 것이라면, [Windows and Arch Dual Boot](/index.php/Windows_and_Arch_Dual_Boot "Windows and Arch Dual Boot")항목을 참고하십시오.

### 언어 변경하기

**도움말:** 이 설정은 대부분 사용자에게 선택사항일 뿐이며 지금이 아니라도 설치 도중 언제든지 실행하실 수 있습니다. 와이파이 비밀번호에 특수문자가 들어가는 등 설정 파일에 영어및 숫자가 아닌 다른 문자를 넣어야 한다거나, 시스템 메시지(오류 메시지 등)을 한글로 받고자 하는 경우가 아니라면 설정을 변경할 필요가 없습니다. 시스템 메시지는 영어로 두는 편이 포럼 등에서 도움을 받을 때에 편리하며, 한글 키보드의 경우 영문 키보드와는 한/영키와 한자키 정도의 차이밖에 없고 설치 미디어의 콘솔 상태에서는 한글을 입력하거나 인식할 방법이 없으므로 설정할 필요가 없습니다.

기본적으로, 키보드 레이아웃은 `us`로 설정되어 있습니다. [US](https://en.wikipedia.org/wiki/File:KB_United_States-NoAltGr.svg "wikipedia:File:KB United States-NoAltGr.svg")가 아닌 키보드 레이아웃을 사용할 경우 다음 명령어를 실행하십시오.

 `# loadkeys _layout_` 

_layout_ 대신 `fr`, `uk` 혹은 `be-latin1`등을 넣으시면 됩니다. [여기](/index.php/KEYMAP#Keyboard_layouts "KEYMAP")에서 사용 가능한 국가 코드 목록을 보십시오.

몇몇 글자가 이상하게 표시되거나 아예 나오지 않더라도 걱정하지 마십시오. 폰트에 해당 글자가 존재하지 않기 때문일 것입니다. 해당 글자는 정상적으로 입력되는것이며 나중에 그래픽 환경을 설치한 뒤에 제대로 표시될 것입니다. 콘솔에서 사용되는 폰트를 바꾸고 싶다면 `/usr/share/kbd/consolefonts/`에 들어있는 글꼴들 중에서 선택할 수 있습니다. 폰트 변경을 위해서는

```
# setfont lat9w-16

```

과 같은 명령을 사용하면 됩니다. 선택된 폰트에 포함된 글자들을 모두 보고 싶다면, `showconsolefont` 명령을 실행하십시오. 폰트 이름에는 대소문자가 구분된다는 점에 유의하십시오. [Fonts#Console Fonts](/index.php/Fonts#Console_Fonts "Fonts")에서 더 자세한 정보를 찾을 수 있습니다.

기본 언어는 미국 영어로 설정되어 있습니다. 언어를 바꾸고 싶으면 `/etc/locale.gen`에서 en_US와 함께 사용할 언어인 한국어 ko_KR 앞의 `#`을 제거하세요. 그리고 `Ctrl+X`를 누른 후 `Y`를 누르고 `Enter`를 눌러 같은 파일이름으로 저장하세요. (ko_KR.EUC_KR 보다는 ko_KR.UTF-8을 선택하는 것이 좋습니다)

 `# nano /etc/locale.gen` 

```
en_US.UTF-8 UTF-8
ko_KR.UTF-8 UTF-8
```

```
# locale-gen
# export LANG=ko_KR.UTF-8

```

`LAlt+LShift`로 키맵을 활성화하거나 비활성화할 수 있습니다.

### 인터넷 연결 설정하기

**경고:** udev는 더 이상 wlanX와 ethX 명명 방식으로 네트워크 인터페이스 이름을 할당하지 않습니다. 다른 배포판에서 아치리눅스로 넘어왔거나, 아치를 재설치하고 있다면, 네트워크 인터페이스의 명칭이 낯설 수 있습니다. 무선인터페이스가 wlan0, 유선 인터페이스가 eth0일 것이라고 가정하지 마십시오. 네트워크 인터페이스의 명칭은 `ip link` 명령을 이용하여 확인할 수 있습니다.

**참고:** 2014.04 이후의 설치매체에는 "Fritzbox!" 시리즈의 일부 라우터에서 dhcp를 통하여 ip 주소를 받는 데에 문제가 있습니다. 현재 7390[[1]](http://unix.stackexchange.com/questions/126526/archlinux-2014-04-64bit-and-connectivity-problem-during-instalation), 7112[[2]](https://unix.stackexchange.com/questions/126694/enabling-wired-internet-connection-with-dhcp-during-arch-linux-installation/126709) 두 모델에서 문제가 발생한다는 것이 확인되었지만, 다른 모델에서도 비슷한 문제가 있을 수 있습니다. [dhcpcd](/index.php/Dhcpcd "Dhcpcd")와 Fritzbox! 라우터들이 ip 주소를 할당하는 방식 사이에서 문제가 나타나는 것으로 보입니다. 이 문제를 해결하기 위해서는 Fritzbox! 설정 창에서 아치를 설치하려는 컴퓨터의 ip 주소를 삭제하십시오. 그 후, "Assign always the same IP address to this machine(이 컴퓨터에 항상 같은 IP 주소 부여하기)" 옵션을 비활성화하십시오. 그런 다음 dhcpcd 프로세스를 다시 시작하거나 컴퓨터를 재부팅하면 정상적으로 IP 주소를 부여받을 수 있습니다. 만일 그래도 문제가 생간다면, Fritzbox! 라우터를 재부팅해보십시오. 일단 컴퓨터에게 정상적으로 IP 주소가 할당된 후에는 아까 비활성화했던 옵션을 다시 활성화시킬 수 있습니다.

systemd-197부터 udev는 안정적으로 예층 가능한 인터페이스 이름을 부여합니다. 부여된 인터페이스 명칭은 재부팅한 후에도 유지됩니다. 이것이 왜 필요한지에 대해 더 자세히 알고 싶다면 [여기](http://www.freedesktop.org/wiki/Software/systemd/PredictableNetworkInterfaceNames)를 보세요.

`dhcpcd` 네트워크 데몬이 부팅시에 자동적으로 시작될 것이며 유선 인터넷에 연결하려고 시도할 것입니다. 제대로 연결되었는지 확인을 위해서는 다음과 같이 `ping`를 이용해서 시험해 보십시오.

 `# ping -c 3 www.google.com` 

```
PING www.l.google.com (74.125.132.105) 56(84) bytes of data.
64 bytes from wb-in-f105.1e100.net (74.125.132.105): icmp_req=1 ttl=50 time=17.0 ms
64 bytes from wb-in-f105.1e100.net (74.125.132.105): icmp_req=2 ttl=50 time=18.2 ms
64 bytes from wb-in-f105.1e100.net (74.125.132.105): icmp_req=3 ttl=50 time=16.6 ms

--- www.l.google.com ping statistics ---
3 packets transmitted, 3 received, 0% packet loss, time 2003ms
rtt min/avg/max/mdev = 16.660/17.320/18.254/0.678 ms
```

만약 `ping: unknown host` 오류가 발생한다면 아래와 같이 네트워크를 직접 설정해야 합니다. 오류가 발생하지 않았다면, [#하드디스크 준비하기](#.ED.95.98.EB.93.9C.EB.94.94.EC.8A.A4.ED.81.AC_.EC.A4.80.EB.B9.84.ED.95.98.EA.B8.B0)로 넘어가시면 됩니다.

#### 유선 네트워크

고정 ip를 사용해 유선 연결을 하려면 이 절차를 따르세요.

우선 `dhcpcd` 서비스를 비활성화합니다. 아래 명령을 실행하세요.

**참고:** dhcpcd가 다른 이름의 서비스로 실행되고 있을 수 있습니다. `dhcpcd@이더넷_인터페이스_명칭.service`와 같은 이름을 가진 서비스로 실행되고 있을 수 있습니다. 비활성화해야하는 dhcpcd를 고르기 위해서는 `systemctl stop dhcpcd`를 친 후에 `Tab`키를 두번 누르면 됩니다.

```
# systemctl stop dhcpcd.service

```

이더넷 인터페이스의 이름을 확인합니다.

 `# ip link` 

```
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN mode DEFAULT
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
2: enp2s0f0: <BROADCAST,MULTICAST> mtu 1500 qdisc noop state DOWN mode DEFAULT qlen 1000
    link/ether 00:11:25:31:69:20 brd ff:ff:ff:ff:ff:ff
3: wlp3s0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc mq state UP mode DORMANT qlen 1000
    link/ether 01:02:03:04:05:06 brd ff:ff:ff:ff:ff:ff

```

이 경우에 이더넷 인터페이스는 enp2s0f0입니다. 잘 모르겠으면 이더넷 인터페이스는 보통 "e"로 시작하며 "lo"나 "w"로 시작할 가능성은 매우 낮습니다. 또한 iwconfig를 사용해 어떤 인터페이스가 이더넷 인터페이스인지 확인할 수 있습니다.

 `# iwconfig` 

```
enp2s0f0  no wireless extensions.
wlp3s0    IEEE 802.11bgn  ESSID:"NETGEAR97"  
          Mode:Managed  Frequency:2.427 GHz  Access Point: 2C:B0:5D:9C:72:BF   
          Bit Rate=65 Mb/s   Tx-Power=16 dBm   
          Retry  long limit:7   RTS thr:off   Fragment thr:off
          Power Management:on
          Link Quality=61/70  Signal level=-49 dBm  
          Rx invalid nwid:0  Rx invalid crypt:0  Rx invalid frag:0
          Tx excessive retries:0  Invalid misc:430   Missed beacon:0
lo        no wireless extensions.
```

이 예에서는 enp2s0f0도 loopback 장치도 무선 확장이 없습니다. 이는 enp2s0f0이 이더넷 인터페이스라는 의미입니다.

다음 설정값들도 알아야 합니다.

*   고정 IP 주소
*   서브넷 마스크
*   게이트웨이 IP 주소
*   네임서버(DNS)의 IP 주소
*   도메인 이름(랜 환경이 아닌 경우에 해당됩니다. 로컬 랜이라면 도메인명을 자유롭게 지어낼 수 있습니다)

연결된 이더넷 인터페이스를 활성화합니다. (위의 예에서는 `enp2s0f0`)

1.  ip link set enp2s0f0 up

다음과 같이 주소를 추가하십시오.

```
# ip addr add _IP 주소_/_서브넷 마스크_ dev _인터페이스_명칭_

```

예시:

```
# ip addr add 192.168.1.2/24 dev enp2s0f0

```

더 많은 옵션을 보려면, `man ip`를 실행하십시오.

다음과 같이 게이트웨이를 추가하십시오.

```
# ip route add default via _IP 주소_

```

예시:

```
# ip route add default via 192.168.1.1

```

사용하고 있는 네임 서버의 IP 주소와 로컬 도메인 이름을 다음과 같이 `resolv.conf`에 추가하십시오.

 `# nano /etc/resolv.conf` 

```
nameserver 61.23.173.5
nameserver 61.95.849.8
search example.com

```

**참고:** 현재, 최대 3개의 `nameserver`줄을 넣을 수 있습니다. 3개 이상을 추가하고자 한다면, [dnsmasq](/index.php/Dnsmasq "Dnsmasq")와 같은 로컬 캐싱 네임서버를 사용하십시오.

**도움말:** 이제 네트워크에 연결되었을 것입니다. 연결이 되지 않았다면 [Configuring Network](/index.php/Configuring_Network "Configuring Network")를 확인하십시오.

#### 무선 네트워크

설치 과정에서 무선 연결(와이파이)이 필요하다면 다음 절차를 따르십시오.

다른 배포판을 사용하다 왔거나 명명 방식이 바뀐 후에 처음으로 아치를 설치한다면 첫 번째 무선 인터페이스 가 "wlan0"아니라서 놀랐을 것입니다. 겁먹지 마세요. 간단하게 `iwconfig`를 실행해 무선 인터페이스 이름을 확인하세요.

무선 드라이버와 유틸리티는 설치 미디어의 라이브 환경에서 사용하실 수 있습니다. 무선 하드웨어에 대해 잘 알고 있을수록 설정을 쉽게 끝낼 수 있을 것입니다. _지금 시점에서 실행하는_ 간단 설정 내용은 무선 장치를 _설치 매체의 라이브 환경에서만_ 사용할 수 있게 만들 것입니다. 이 단계(혹은 다른 형태의 무선 관리)는 **설치가 끝난 뒤 다시 한번 설정해 주어야 합니다**.

또한 이 시점에서의 무선 연결은 꼭 필요하지만은 않다는 것을 알아두십시오; 무선 네트워크는 나중에라도 언제든지 연결할 수 있습니다.

**참고:** 다음 예시는 `wlp3s0`를 인터페이스로, `linksys`를 ESSID로 가정합니다. 환경에 따라 이 값들을 변경해서 사용하십시오.

기본 단계는 다음과 같습니다.

*   무선 인터페이스를 알아냅니다.

 `# iw dev` 

```
phy#0
        Interface wlp3s0
                ifindex 3
                wdev 0x1
                addr 00:11:22:33:44:55
                type managed
```

이 예시에서는 `wlp3s0` 가 사용할 수 있는 무선 인터페이스입니다. 확신이 들지 않는다면 인터페이스 명칭이 어떤 글자로 시작하는지 확인하십시오. 무선 인터페이스는 보통 'w'로 시작하며, 'lo', 'e'로 시작할 가능성은 낮습니다.

**참고:** 이런 내용이 출력되지 않는다면, 무선 드라이버가 로드되지 않은 것입니다. 이런 경우, 직접 드라이버를 로드해야 합니다. [무선 네트워크 설정](/index.php/Wireless_Setup "Wireless Setup") 항목으로 이동해 자세한 정보를 얻으십시오.

이제 [netctl](/index.php/Netctl "Netctl")이 제공하는 `wifi-menu`를 이용하여 네트워크에 연결합니다.

```
# wifi-menu wlp3s0

```

이제 와이파이에 연결될 것입니다. 그렇지 않다면, [Wireless network configuration](/index.php/Wireless_network_configuration "Wireless network configuration")에서 자세한 사항을 보십시오. 네트워크에 연결하기 위해 사용자명과 비밀번호가 모두 필요할 경우, [WPA2 Enterprise](/index.php/WPA2_Enterprise "WPA2 Enterprise") 항목을 참고하십시오.

##### wifi-menu를 사용하지 않고 와이파이에 연결하기

해당 인터페이스를 다음 명령어로 작동시킵니다.

```
# ip link set wlp3s0 up

```

인터페이스가 작동하고 있는지 확인하려면, 다음 명령의 출력을 검사하면 됩니다.

 `# ip link show wlp3s0` 

```
3: wlp3s0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc mq state DOWN mode DORMANT group default qlen 1000
    link/ether 00:11:22:33:44:55 brd ff:ff:ff:ff:ff:ff

```

`<BROADCAST,MULTICAST,UP,LOWER_UP>`의 `UP`이 인터페이스가 작동하고 있음을 나타냅니다. 그 뒤의 `state DOWN`은 무시하셔도 됩니다.

대부분의 무선 칩셋은 드라이버 뿐 아니라 알맞는 펌웨어를 필요로 합니다. 커널은 자동으로 알맞는 드라이버와 펌웨어를 로드하려 할 것입니다. 만일 `SIOCSIFFLAGS: No such file or directory`과 같은 오류가 출력되었다면, 펌웨어를 수동으로 로드해야 합니다. 잘 모르겠다면 `dmesg` 명령어로 커널 로그를 보면서 해당 칩셋에 대한 펌웨어 요청이 있는지 확인하십시오. 예를 들어, 펌웨어 가 필요한 인텔 칩셋을 사용하고 있다면,

 `# dmesg | grep firmware` 

```
firmware: requesting iwlwifi-5000-1.ucode

```

과 같은 내용이 있을 것입니다. 만일 출력이 없다면, 이는 현재 시스템의 무선 칩셋이 펌웨어를 필요로 하지 않는다는 뜻입니다.

**경고:** (CD나 USB 스틱의) 라이브 환경 하에서는 (필요한 카드에 대해) 무선 칩셋 펌웨어 패키지가 `/usr/lib/firmware`에 미리 설치되어 있지만, 아치리눅스를 설치할 때 따로 해당 펌웨어를 설치해주어야 합니다. 그렇지 않으면 설치 완료 후 설치된 시스템으로 재부팅 했을 때에 무선 기능을 사용할 수 없을 수 있습니다. 패키지 설치는 이 가이드 내에서 나중에 다뤄집니다. 재부팅 하기 전에 무선 모듈과 펌웨어를 꼭 설치하도록 하세요! 특정 칩셋용 펌웨어를 필요로 하는지 잘 모르겠다면 [무선 네트워크 설정](/index.php/Wireless_Setup "Wireless Setup") 페이지를 보세요.

그 다음, `iw dev wlp3s0 scan | grep SSID` 명령으로 사용할 수 있는 와이파이 네트워크를 검색합니다. 네트워크에 연결하려면 다음과 같은 명령을 이용합니다.

```
# wpa_supplicant -B -i wlp3s0 -c <(wpa_passphrase "_ssid_" "_psk_")

```

_ssid_에 원하는 네트워크의 이름을 넣고, _psk_에 비밀번호를 넣으면 됩니다. 단, 명령을 내릴 때 **네트워크 이름과 비밀번호에 각각 따옴표 표시를 해야 합니다.**

마지막으로, 무선 인터페이스에 IP 주소를 부여해야 합니다. 수동으로 하거나 dhcp를 이용하여 자동으로 부여받을 수 있습니다. dhcp를 이용하려면 다음 명령을 내립니다.

```
# dhcpcd wlp3s0

```

이 명령으로 연결이 되지 않았다면, 다음 명령들을 시도해보십시오.

```
# echo 'ctrl_interface=DIR=/run/wpa_supplicant' > /etc/wpa_supplicant.conf
# wpa_passphrase _ssid_ _passphrase_ >> /etc/wpa_supplicant.conf
# ip link set _interface_ up
# wpa_supplicant -B -D nl80211 -c /etc/wpa_supplicant.conf -i _interface_
# dhcpcd -A _interface_

```

3단계에서 ip link set _interface_ up 명령은 불필요할 수도 있으나, 확인 차원에서 실행하는 것이 좋습니다.

4단계에서 _wpa_supplicant_가 unsupported driver(지원되지 않는 드라이버) 등의 오류를 출력한다면, `-D nl80211` 파라미터를 빼고 다시 명령을 내리십시오.

```
# wpa_supplicant -B -c /etc/wpa_supplicant.conf -i _interface_

```

#### xDSL (PPPoE), 아날로그 모뎀 혹은 ISDN

XDSL, 전화선 인터넷, ISDL 등을 사용하려면 [Direct Modem Connection](/index.php/Direct_Modem_Connection "Direct Modem Connection") 문서를 보십시오.

#### 프록시 서버를 경유할 경우

프록시 서버를 경유해야 할 경우, `http_proxy`및 `ftp_proxy` 환경 변수를 설정해야 합니다. 더 많은 정보를 위해서는 **[여기](/index.php/Proxy "Proxy")**를 클릭하십시오.

### 하드디스크 준비하기

**경고:** 파티션을 편집하다가 데이터가 소실될 수 있습니다. 이 점을 **반드시** 숙지하고 계속하기 전에 중요한 데이터는 백업해 두시기를 권합니다.

**참고:** USB Flash Key에 아치를 설치하고자 한다면, [Installing Arch Linux on a USB key](/index.php/Installing_Arch_Linux_on_a_USB_key "Installing Arch Linux on a USB key")문서를 참고하십시오.

**도움말:** [LVM](/index.php/LVM "LVM"), [디스크 암호화](/index.php/Disk_encryption "Disk encryption"), [RAID](/index.php/RAID "RAID")를 위해 stacked block device를 만들고자 한다면, 지금 만드십시오.

#### 파티션 테이블 종류 선택

**참고:** 아치리눅스와 윈도우가 같은 디스크에서 듀얼부팅되고 있다면, **대개의 경우** 아치는 미리 설치된 윈도우가 사용하는 펌웨어 부팅 모드와 파티션 조합을 사용할 것입니다. 그렇지 않은 경우, 윈도우 부팅이 실패할 것입니다. [Windows and Arch Dual Boot#Important Information](/index.php/Windows_and_Arch_Dual_Boot#Important_Information "Windows and Arch Dual Boot")을 참고하십시오.

[GPT](/index.php/GUID_Partition_Table "GUID Partition Table")와 [MBR](/index.php/Master_Boot_Record "Master Boot Record") 중 하나를 선택해야 합니다. [Partitioning#Choosing between GPT and MBR](/index.php/Partitioning#Choosing_between_GPT_and_MBR "Partitioning")을 참고하십시오.

*   UEFI를 사용할 경우, 항상 GPT를 사용하는 것이 좋습니다. 특정 UEFI 펌웨어들은 UEFI-MBR 부팅을 허용하지 않습니다.

*   어떤 BIOS 시스템들은 GPT를 사용할 경우 문제를 일으킵니다. [http://mjg59.dreamwidth.org/8035.html](http://mjg59.dreamwidth.org/8035.html) 과 [http://rodsbooks.com/gdisk/bios.html](http://rodsbooks.com/gdisk/bios.html) 에서 더 자세한 내용과 가능한 해결법들을 찾을 수 있습니다.

#### 파티션 도구

완전 초보자들은 그래픽 파티션 도구를 사용하시기를 권합니다. [GParted](/index.php/GParted "GParted")가 좋은 예입니다. Gparted는 [라이브 CD](http://gparted.sourceforge.net/livecd.php)로도 제공되고 있습니다. 먼저 드라이브에 [파티션을 만들고](/index.php/Partitioning "Partitioning"), 파티션을 [파일 시스템](/index.php/File_Systems "File Systems")으로 포맷해야 합니다.

GParted는 사용하기 쉽지만, 그냥 새로운 디스크에 파티션 몇 개를 만들고 싶다면 설치 매체에 포함되어 있는 [fdisk 계열의 파티션 도구](/index.php/Partitioning#Partitioning_tools "Partitioning")를 이용하여 간편하게 작업을 할 수 있습니다. 다음 섹션에서는 [gdisk](/index.php/Partitioning#Gdisk_usage_summary "Partitioning")와 [fdisk](/index.php/Partitioning#Fdisk_usage_summary "Partitioning")를 사용하는 방법을 간단히 다룰 것입니다.

#### 파티션 테이블 지우기

컴퓨터에 존재하는 기존의 파티션을 다 지우고 새로 시작하고 싶다면, 파티션 테이블을 지우는 것이 좋습니다. 이렇게 하면 새로 파티션을 만드는 것이 쉬워질 뿐 아니라 디스크를 MBR에서 GPT로 바꾸거나, GTP에서 MBR로 바꿀 때에 문제를 피할 수 있습니다.

```
# sgdisk --zap-all /dev/sda

```

#### 파티션 구성하기

파티션을 몇 개나 만들지, 그리고 어느 파티션을 어느 디렉토리로 사용할지를 스스로 결정할 수 있습니다. 어느 파티션이 시스템의 어느 디렉토리로(Mount Point라고도 부릅니다) 사용될 것인지 매핑한 것을 [파티션 구성(partition scheme)](/index.php/Partitioning#Partition_scheme "Partitioning")이라고 합니다. 가장 단순한 파티션 구성은 하나의 큰 `/` 파티션을 만드는 것입니다. 단순하지만 나쁜 선택은 아닙니다. 역시 흔히 사용되는 구성은 `/`와 `/home` 파티션을 만드는 것입니다.

**추가적으로 필요한 파티션**

*   [UEFI](/index.php/Unified_Extensible_Firmware_Interface "Unified Extensible Firmware Interface") 마더보드를 사용하고 있을 경우, [EFI 시스템 파티션](/index.php/Unified_Extensible_Firmware_Interface#EFI_System_Partition "Unified Extensible Firmware Interface")을 추가적으로 만들어야 합니다.
*   BIOS 마더보드를 사용하고 있거나 BIOS 호환성 모드를 사용하고자 하며, GRUB 부트로더를 GPT 디스크에서 사용하려고 할 경우, 1 혹은 2 MiB 크기의 [Bios 부트 파티션](/index.php/GRUB#GUID_Partition_Table_.28GPT.29_specific_instructions "GRUB")을 `EF02` 타입 코드를 적용하여 추가로 만들어야 합니다. Syslinux를 사용할 경우 이 파티션은 필요 없습니다.
*   시스템 자체에 [디스크 암호화](/index.php/Disk_encryption "Disk encryption")를 적용하려 할 경우, 파티션 구성에도 이를 반영해야 합니다. 시스템 설치 이후에 암호화된 폴더, 컨테이너, 홈 디렉토리를 추가하는 것이 더 문제를 덜 일으킵니다.

스왑 파티션이나 스왑 파일을 사용하고자 한다면 [Swap](/index.php/Swap "Swap") 문서를 읽으십시오. 스왑 파일은 스왑 파티션에 비해 설치 완료 후에 크기를 조정하기 쉽지만, Btffs 파티션과 같이 사용할 수 없습니다.

이미 파티션 작업을 해 두었다면 [파티션 마운트하기](#.ED.8C.8C.ED.8B.B0.EC.85.98_.EB.A7.88.EC.9A.B4.ED.8A.B8.ED.95.98.EA.B8.B0)로 넘어가십시오. 새로 파티션을 잡고자 한다면, 다음의 예시를 참고하십시오.

#### 예시

아치 리눅스 설치 미디어에는 다음 파티션 도구가 들어 있습니다.

*   [cfdisk](https://en.wikipedia.org/wiki/cfdisk "wikipedia:cfdisk") – [MBR](/index.php/MBR "MBR") 파티션 테이블만을 지원합니다.
*   [gdisk](https://en.wikipedia.org/wiki/gdisk "wikipedia:gdisk") – [GPT](/index.php/GPT "GPT") 파티션 테이블만을 지원합니다.
*   [parted](https://en.wikipedia.org/wiki/parted "wikipedia:parted") – 양쪽 모두 지원합니다.

**도움말:** `lsblk`명령으로 시스템에 들어있는 하드디스크들의 리스트를 볼 수 있습니다. 파티션 작업을 시작하기 전, 원하는 디스크를 확인하는 데에 도움을 줄 수 있습니다.`lsblk -f`는 추가적인 정보를 제공합니다. 각 디스크와 파티션의 라벨, UUID, 파일시스템 종류 등을 확인할 수 있습니다.

이 예시에서는 15GB 크기의 루트 파티션과 남는 공간을 차지하는 [홈](/index.php/Partitioning#.2Fhome "Partitioning") 파티션으로 시스템을 구성할 것입니다. MBR과 GPT 중 하나를 선택하십시오. 둘 다 선택해서는 안됩니다!

파티션 잡기는 개인적인 선택이며, 이 예시는 단지 파티션 구성법을 보여주기 위한 것일 뿐임을 유의하십시오. [파티션](/index.php/Partitioning "Partitioning") 문서를 참고하십시오.

##### cgdisk로 GPT 파티션 만들기

다음 명령으로 _cgdisk_를 실행하십시오.

```
# cgdisk /dev/sda

```

**도움말:** cgdisk가 디스크를 GPT로 변환할 수 없다면, [parted](https://www.archlinux.org/packages/?name=parted)를 사용하십시오.

**root:**

**참고:** 이 파티션은 `/root` 이 아니라 `/` 로 마운트 될 파티션입니다.

*   _New_를 선택(`N`을 눌러도 됩니다)하고 `Enter`를 누릅니다. 첫 섹터 (2048)에는 `15G`를 입력하고 `Enter`를 누릅니다. 기본 hex 코드는 (8300)을 입력하고 `Enter`를 누르면 빈 이름을 가진 파티션이 만들어집니다.

**Home:**

*   아래 방향키를 몇 번 눌러 더 큰 빈 공간으로 이동합니다.
*   _New_를 선택하거나 `N`을 누르고 `Enter`를 칩니다. 빈 공간을 모두 이용하려면 다시 `Enter`를 누릅니다. 만일 다른 크기로 파티션을 만들고 싶다면 원하는 크기를 입력하고(예: 30G) `Enter`를 누릅니다. 기본 hex 코드는 (8300)을 넣고 `Enter`를 눌러 빈 이름을 가진 파티션을 만듭니다.

이렇게 했다면 아래와 같은 출력을 볼 수 있을 것입니다.

```
Part. #     Size        Partition Type            Partition Name
----------------------------------------------------------------
            1007.0 KiB  free space
   1        15.0 GiB    Linux filesystem
   2        123.45 GiB  Linux filesystem

```

파티션이 원하는 크기로 만들어졌는지, 파티션 테이블 레이아웃이 마음에 드는지 다시 한번 확인하십시오.

만일 중간에 다시 시작하고 싶다면 그냥 _Quit_ 을 선택하거나 `Q`를 누르면 저장하지 않고 나올 수 있습니다. 다시 _cgdisk_를 실행해서 새로 파티션 구성을 하면 됩니다.

파티션 구성이 마음에 든다면, "Write"를 선택하거나 `Shift+W`를 눌러 파티션 구성을 디스크에 기록합니다. `yes`를 입력해 최종 확인을 한 후, "Quit"을 선택하거나 `Q`를 눌러 _cgdisk_에서 빠져나옵니다.

##### fdisk로 MBR 파티션 만들기

**참고:** MBR 파티션을 만들 때에는 _cfdisk_역시 사용할 수 있습니다. _cfdisk_는 _cgdisk_와 비슷한 인터페이스를 가지고 있습니다. 하지만 현재에는 _cfdisk_에 첫 파티션을 자동으로 정확하게 정렬하지 않는 버그가 존재하기 때문에, 여기에서는 _fdisk_를 사용하였습니다.

_fdisk_를 실행시킵니다:

```
# fdisk /dev/sda 

```

파티션 테이블을 만듭니다:

*   `Command (m for help):` 에서 `o`를 치고 `Enter`를 누릅니다.

첫 파티션을 만듭니다:

1.  `Command (m for help):` `n` 를 치고 `Enter`를 누릅니다.
2.  Partition type: `Select (default p):` `Enter`를 누릅니다.
3.  `Partition number (1-4, default 2):` `Enter`를 누릅니다.
4.  `First sector (31459328-209715199, default 31459328):` `Enter`를 누릅니다.
5.  `Last sector, +sectors or +size{K,M,G,T,P} (31459328-209715199....., default 209715199):` `Enter`를 누릅니다.

두번째 파티션을 만듭니다:

1.  `Command (m for help):` `n`을 치고 `Enter`를 누릅니다.
2.  Partition type: `Select (default p):` `Enter`를 누릅니다.
3.  `Partition number (1-4, default 2):` `Enter`를 누릅니다.
4.  `First sector (31459328-209715199, default 31459328):` `Enter`를 누릅니다.
5.  `Last sector, +sectors or +size{K,M,G,T,P} (31459328-209715199....., default 209715199):` `Enter`를 누릅니다.

디스크에 새 파티션 테이블을 기록하기 전에 확인을 합니다:

*   `Command (m for help):` `p`를 치고 `Enter`를 누릅니다.

```
Disk /dev/sda: 107.4 GB, 107374182400 bytes, 209715200 sectors
Units = sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 512 bytes
I/O size (minimum/optimal): 512 bytes / 512 bytes
Disk identifier: 0x5698d902

   Device Boot     Start         End     Blocks   Id  System
/dev/sda1           2048    31459327   15728640   83   Linux
/dev/sda2       31459328   209715199   89127936   83   Linux

```

변경 사항을 디스크에 기록합니다.

*   `Command (m for help):` `w`를 치고 `Enter`를 누릅니다.

모든 단계가 정상적으로 진행되었다면 fdisk가 다음 메시지를 출력하고 종료할 것입니다.

```
The partition table has been altered!

Calling ioctl() to re-read partition table.
Syncing disks. 

```

만일 에러 메시지를 출력하며 이 과정이 실패한다면, `q` 키를 눌러 _fdisk_를 종료할 수 있습니다.

#### 파일시스템 만들기

파티션을 다 만들었다고 해도 디스크 준비 과정이 끝난 것은 아닙니다. 파티션들을 [파일 시스템](/index.php/File_Systems "File Systems")으로 포맷을 해주어야 합니다. 리눅스의 기본 파일 시스템은 ext4로 파티션들을 포맷해주려면 다음 명령을 사용하세요.

**경고:** 포맷되는 파티션들이 정말로 `/dev/sda1` 과 `/dev/sda2`인지 반드시 다시 확인하세요. `lsblk` 명령이 여기에 도움을 줍니다.

```
# mkfs.ext4 /dev/sda1
# mkfs.ext4 /dev/sda2

```

스왑 파티션을 만들고 싶다면 (코드 82), 다음과 같이 그 파티션을 활성화하십시오.

```
# mkswap /dev/sda_X_
# swapon /dev/sda_X_

```

UEFI를 사용하고 있다면, EFI 시스템 파티션을 다음과 같이 포맷해주십시오. (아래의 예시에서는 /dev/sd_xy_입니다)

```
# mkfs.fat -F32 /dev/sd_XY_

```

**참고:** BIOS 시스템을 사용하고 있으며, [GPT](/index.php/GUID_Partition_Table "GUID Partition Table") 디스크에 GRUB를 설치할 계획이라면, [BIOS 부트 파티션](/index.php/GRUB#GUID_Partition_Table_.28GPT.29_specific_instructions "GRUB")은 `/boot` 마운트 포인트와 무관하다는 사실에 유의하십시오. GRUB가 직접 BIOS 부트 파티션을 사용할 것입니다. 해당 파티션에 파일 시스템을 만들거나, 다음 단계들에서 그 파티션을 마운트하지 마십시오.

### 파티션 마운트하기

각각의 파티션은 끝의 번호로 구별됩니다. 예를 들어, `sda1`은 첫 드라이브의 첫 파티션을 가리키며, `sda`는 드라이브 전체를 가리킵니다.

다음 명령어로 파티션 레이아웃을 보십시오.

```
# lsblk /dev/sda

```

**참고:** 한 디렉토리에 두개 이상의 파티션을 마운트하려 하지 마십시오. 마운트 순서는 매우 중요하므로 신경을 써야 합니다.

먼저, 루트 파티션을 `/mnt`에 마운트합니다. 설정에 따라 다를 수 있지만 예시를 따르면 다음과 같습니다.

```
# mount /dev/sda1 /mnt

```

별개의 파티션(`/home`, `/boot`, `/var` 등)을 지정했다면 다음과 같이 마운트하십시오.

```
# mkdir /mnt/home
# mount /dev/sda3 /mnt/home
# mkdir /mnt/boot
# mount /dev/sda_x_ /mnt/boot

```

UEFI 마더보드를 사용하고 있다면, EFI 시스템 파티션을 `/boot`에 마운트하십시오. 다른 마운트 포인트를 사용하는 것도 가능하지만, `/boot`를 사용하는 것이 추천됩니다. 그 이유는 [EFISTUB](/index.php/EFISTUB "EFISTUB")문서에서 설명하고 있습니다.

### 미러 사이트 선택하기

설치하기 전에, 선호하는 미러 사이트가 먼저 오도록 `mirrorlist`를 편집하는 것이 좋습니다. mirrorlist의 사본이 pacstrap에 의해서 새 시스템에도 복사될 것이므로 지금 설정해 두는 것이 좋습니다.

**참고:** ftp.archlinux.org의 속도는 50KB/s로 낮춰져 있습니다.

 `# nano /etc/pacman.d/mirrorlist` 

```
##
## Arch Linux repository mirrorlist
## Sorted by mirror score from mirror status page
## Generated on YYYY-MM-DD
##

Server = http://mirror.example.xyz/archlinux/$repo/os/$arch
...
```

*   `Alt+6`를 눌러 `Server` 줄을 복사하십시오.
*   `PageUp`를 눌러 위로 되돌아가십시오.
*   `Ctrl+U`를 눌러 목록 맨 위에 넣으십시오.

원한다면 `Ctrl+K`를 눌러서 나머지를 모두 지워 버리고 해당 미러를 유일한 미러로 만들어도 됩니다. 하지만 그 미러가 오프라인 상태일 때를 대비하여 미러 몇 개를 더 활성화해놓는 것이 좋습니다.

**도움말:** [Mirrorlist Generator](https://www.archlinux.org/mirrorlist/)를 사용해서 여러분 국가의 업데이트된 목록을 받으십시오. HTTP 미러는 FTP보다 빠른데, 왜냐하면 [keepalive](https://en.wikipedia.org/wiki/Keepalive "wikipedia:Keepalive")라는 것 때문입니다. FTP를 이용하면 팩맨은 매번 패키지를 받을 때 마다 신호를 보내기 때문에 약간의 끊김이 발생합니다.

**참고:** 한국에서 아치리눅스를 설치하고 있다면 대체로 한국과 지리적으로 가까운 국가들에 있는 미러들의 속도가 빠릅니다. 일본, 대만, 한국의 미러들을 사용하여 속도를 높일 수 있습니다.

**참고:**

*   `mirrorlist`에 변화를 가할 때마다 `pacman -Syyu` 커맨드를 이용하여 패치키 리스트와 mirrorlist가 일치하도록 하는 것이 좋습니다. [Mirrors](/index.php/Mirrors "Mirrors")를 참고하십시오.
*   최신 버전이 아닌 설치 매체를 사용하고 있을 경우, mirrorlist가 오래되어 업데이트시 문제가 생길 수 있습니다([FS#22510](https://bugs.archlinux.org/task/22510)를 참고하십시오). 그러므로 항상 최신 버전의 미러 정보를 사용하는 것이 좋습니다.
*   [아치리눅스 포럼](https://bbs.archlinux.org/)에서 _pacman_이 저장소를 업데이트하거나 동기화하는 데에 문제를 일으키는 몇가지 네트워크 문제들이 발견되었습니다([[3]](https://bbs.archlinux.org/viewtopic.php?id=68944)와 [[4]](https://bbs.archlinux.org/viewtopic.php?id=65728)를 참고하십시오). 아치 리눅스를 실제 하드웨어에 설치하고 있다면, _pacman_의 파일 다운로더를 다른 다운로더로 대체하여 문제를 해결할 수 있습니다([Improve pacman performance](/index.php/Improve_pacman_performance "Improve pacman performance")문서를 확인하십시오). 만약 [VirtualBox](/index.php/VirtualBox "VirtualBox") 등을 이용하여 가상 머신에 아치리눅스를 설치하고 있다면, 네트워크 인터페이스를 "NAT"에서 "호스트 인터페이스(Host interface)로 바꾸어 문제를 해결할 수 있습니다.

### 기반 시스템 설치하기

기반 시스템은 [pacstrap](https://github.com/falconindy/arch-install-scripts/blob/master/pacstrap.in) 스크립트에 의해 설치됩니다. [base](https://www.archlinux.org/groups/x86_64/base/)의 모든 패키지를 설치하고자 한다면 `-i`를 사용하지 않아도 됩니다. `-i`를 사용하지 않을 경우 pacstrap은 사용자 확인을 요청하지 않고 모든 패키지를 설치합니다. [base-devel](https://www.archlinux.org/groups/x86_64/base-devel/)의 패치지들 역시 설치하는 것을 권장합니다.

```
# pacstrap /mnt base base-devel

```

*   [base](https://www.archlinux.org/groups/x86_64/base/): 최소한의 기반 환경을 제공하기 위한 [core] 저장소의 소프트웨어 패키지들
*   [base-devel](https://www.archlinux.org/groups/x86_64/base-devel/): `make`나 `automake`와 같은 [core]의 기타 도구들. 이 도구들은 시스템을 확장하는데 필요할 가능성이 높기 때문에 대부분의 초보자들은 설치하도록 선택해야 합니다. 이 도구들은 [Arch User Repository](/index.php/Arch_User_Repository "Arch User Repository")의 소프트웨어를 설치하는 데 필요합니다.

**참고:**

*   미러를 정확하게 설정했음에도 _pacstrap_이 `error: failed retrieving file 'core.db' from mirror... : Connection time-out`라는 오류를 출력하며 멈춘다면, [네임 서버](/index.php/Resolv.conf "Resolv.conf")를 바꾸어 보십시오.
*   base 패키지를 설치하다가 pgp키를 import해야 한다는 메시지가 출력되면, 동의하고 계속하십시오. 이 문제는 사용하고 있는 아치 설치 매체가 최신 버전이 아닌 경우 발생할 수 있습니다. pgp 키를 추가하는 데에 실패한다면, [archlinux-keyring](https://www.archlinux.org/packages/?name=archlinux-keyring)을 `pacman -S archlinux-keyring`명령을 통해 업그레이드하십시오.
*   만약 pacman이 패키지의 무결성을 검사하는 데 실패하면, 시스템의 시계를 확인해 보십시오. 만약 시스템 날짜가 2010년으로 설정돼 있는 등 잘못 설정되어 있다면 서명 키를 만료된 것으로(혹은 무효인 것으로) 판단하게 되어 서명 체크가 실패하고, 설치가 중단될 것입니다. 시스템의 시간을 `ntpd -qg`명령을 사용하거나 수동으로 맞춘 후에 pacstrap 명령을 다시 실행해 보십시오. [Time](/index.php/Time "Time") 페이지에서 시스템 시간을 맞추는 데 더 많은 정보를 볼 수 있습니다.
*   _pacman_이 `error: failed to commit transaction (invalid or corrupted package)`라는 오류를 출력하면, 다음 명령을 내린 후에 다시 pacstrap 명령을 실행하십시오.

```
# pacman-key --init && pacman-key --populate archlinux

```

이렇게 해서 아치의 기본적인 시스템이 만들어집니다. 다른 패키지들은 [pacman](/index.php/Pacman "Pacman")을 이용해서 설치할 수 있습니다.

### fstab 생성하기

다음 명령어를 이용해 [fstab](/index.php/Fstab "Fstab")파일을 생성합니다. 아치에서는 기본으로 UUID를 이용하여 fstab을 설정합니다. 그 이유는 [fstab#Identifying filesystems](/index.php/Fstab#Identifying_filesystems "Fstab")를 참고하십시오. UUID 대신 라벨을 사용하고 싶다면, `-U` 옵션 대신 `-L`을 사용하십시오.

**참고:** genfstab을 실행하는 중이나 나중에 설치 과정에서 문제가 발생하면, genfstab을 **다시 실행하지 마십시오**. 그냥 fstab을 직접 편집하십시오.

```
# genfstab -p /mnt >> /mnt/etc/fstab
# nano /mnt/etc/fstab

```

고려할 사항이 몇가지 있습니다:

*   fstab의 각 파티션에 해당하는 줄에서 마지막 칸은 부팅시 파티션을 확인하는 순서를 결정합니다. 루트 파티션에 Btrfs를 사용하지 않는다면, 루트 파티션에는 `1`를 사용하십시오. 확인되기를 바라는 다른 파티션들에는 `2`를 사용하십시오. `0`는 그 파티션을 확인하지 않는다는 뜻입니다. ([fstab#Field definitions](/index.php/Fstab#Field_definitions "Fstab")에서 더 자세한 정보를 얻으실 수 있습니다.)
*   모든 [Btrfs](/index.php/Btrfs "Btrfs")파일 시스템으로 포맷된 파티션은 `0`를 사용해야 합니다. _스왑(swap)_ 파티션에도 `0`을 적용하는 것이 일반적입니다.

### 시스템에 chroot로 들어가기

이제 [chroot](/index.php/Change_root "Change root")을 이용해서 새로 설치한 시스템에 들어갈 것입니다.

```
# arch-chroot /mnt /bin/bash

```

**참고:** `/bin/bash`를 사용하지 않을 경우, 매우 기본적인 sh를 쉘로 사용하게 됩니다.

이 단계에서는 설치된 아치 리눅스 시스템의 주요 설정 파일들을 설정할 것입니다. 해당 파일이 존재하지 않는다면 만들어서 편집할 수 있고, 기본값과 다른 설정을 원한다면 이미 존재하는 파일들을 수정할 수 있습니다.

다음 단계들을 정확하게 이해하고 설명을 정확하게 따르는 것은 정상적으로 동작하는 시스템을 설치하는 데에 매우 중요합니다.

#### 로케일

로케일은 [glibc](https://www.archlinux.org/packages/?name=glibc)를 비롯하여 로케일을 감지할 수 있는 프로그램과 라이브러리들이 지역별 화폐 단위, 날짜 형식, 문자의 특성 등 지역별 표준에 맞게 텍스트를 표현할 때에 사용됩니다. 로케일 설정값은 `locale.gen`과 `locale.conf`에서 정의됩니다.

기본적으로 `locale.gen`파일은 모든 로케일이 주석처리되어 있습니다. 주석처리를 해제하고 로케일을 활성화하려면 해당 로케일 앞의 `#`을 지우세요. 항상 `ISO-8859` 대신 `UTF-8`을 사용하는 것이 추천됩니다.

`en_US.UTF-8`를 활성화시키세요. 다른 로케일이 필요하다면 필요한 로케일 앞의 `#`표시를 지우세요.

 `# nano /etc/locale.gen` 

```
...
#en_SG ISO-8859-1
en_US.UTF-8 UTF-8
#en_US ISO-8859-1
...

```

`locale.gen`에서 설정한 로케일들을 생성합니다.

```
# locale-gen

```

**참고:** 이 명령은 [glibc](https://www.archlinux.org/packages/?name=glibc)가 업데이트될 때마다 자동으로 실행됩니다.

원하는 기본 로케일을 선택하여 `/etc/locale.conf` 파일을 만듭니다.

**참고:** 기본 시스템 로케일로 `en_US.UTF-8`를 설정하면 시스템 로그가 영어로 출력되게 됩니다. 시스템 로그를 영어로 두는 것이 문제 해결을 더 쉽게 합니다. 시스템 로케일에 관계 없이 각 사용자는 자신의 환경을 위해 자신의 로케일을 설정할 수 있습니다. [Locale#Per user](/index.php/Locale#Per_user "Locale")를 참고하십시오.

```
# echo LANG=en_US.UTF-8 > /etc/locale.conf

```

**참고:**

*   `LANG` 환경변수에서 설정된 로케일은 반드시 `/etc/locale.gen` 파일에서 활성화되어 있어야 합니다.
*   `locale.conf`파일은 기본적으로 존재하지 않습니다. `LANG`을 설정하는 것만으로도 해당 로케일이 다른 변수에 대한 기본값으로 작용합니다.

```
# export LANG=en_US.UTF-8

```

**참고:** 다른 `LC_*`환경 변수들에 다른 로케일을 적용하고 싶다면, `locale` 명령어를 사용하여 사용할 수 있는 옵션들을 확인하고 `locale.conf` 파일에 그 옵션들을 추가할 수 있습니다. `LC_ALL` 환경변수를 사용하는 것은 권장되지 않습니다. [Locale](/index.php/Locale "Locale")문서를 참고하십시오.

##### 영어가 아닌 언어에 대한 예시

만약 설치 과정 및 재부팅 이후에 영어가 아닌 언어_(이 예제에서는 한국어)_를 보고 싶으시다면, 다음과 같이 진행하시면 됩니다.

 `# nano /etc/locale.gen` 

```
en_US.UTF-8 UTF-8
ko_KR.UTF-8 UTF-8
```

```
# locale-gen

```

```
# echo "LANG=ko_KR.UTF-8" > /etc/locale.conf
# export LANG=ko_KR.UTF-8

```

#### 콘솔 폰트와 키맵

[#언어 변경하기](#.EC.96.B8.EC.96.B4_.EB.B3.80.EA.B2.BD.ED.95.98.EA.B8.B0)에서 콘솔 키맵과 폰트를 변경했다면, 변경했던 설정값과 동일하게 `/etc/vconsole.conf`를 편집해야 합니다. 그렇게 해야 설치된 시스템으로 재부팅했을 때에도 변경된 설정값이 유지됩니다. 예를 들어,

 `# nano /etc/vconsole.conf` 

```
KEYMAP=de-latin1
FONT=lat9w-16
```

**경고:** `KEYMAP` 변수와 처음에 _loadkeys_를 이용하여 설정한 키맵이 다를 경우, 비밀번호 설정 후에 설치된 시스템을 재부팅 한 후 로그인하는 데에 문제가 생길 수 있습니다. 키들이 다르게 매핑되었을 수 있기 때문입니다.

이 설정값들은 콘솔에서만 유효하다는 사실에 유의하십시오. [Xorg](/index.php/Xorg "Xorg")에는 이 설정값들이 적용되지 않습니다. [Fonts#Console fonts](/index.php/Fonts#Console_fonts "Fonts") 문서에서 더 자세한 내용을 찾을 수 있습니다.

#### 시간대

zone과 subzone은 `/usr/share/zoneinfo/<Zone>/<SubZone>` 디렉토리 내에 있습니다.

사용 가능한 <Zone>을 보려면, 다음과 같이 `/usr/share/zoneinfo/` 디렉토리를 확인하십시오.

```
# ls /usr/share/zoneinfo/

```

마찬가지로, <SubZone>을 보려면 다음과 같이 해당 디렉토리의 내용을 보십시오.

```
# ls /usr/share/zoneinfo/Asia

```

다음 명령어를 이용해서 `/etc/localtime`을 해당 `/usr/share/zoneinfo/<Zone>/<SubZone>`에 심볼릭 링크를 걸도록 하십시오.

```
# ln -s `/usr/share/zoneinfo/<Zone>/<SubZone>` /etc/localtime

```

**예시:**

```
# ln -s /usr/share/zoneinfo/Asia/Seoul /etc/localtime

```

**참고:** `ln: failed to create symbolic link '/etc/localtime': File exists`라는 오류가 출력된다면, 이미 존재하는 파일을 `ls -l /etc/localtime` 명령으로 확인한 후에, `ln` 명령에 `-f`옵션을 더해 존재하는 파일을 덮어쓰십시오.

#### 하드웨어 시계

사용하는 운영체제 간에 하드웨어 시계를 일관되게 설정하십시오. 그렇지 않을 경우 각 운영체제가 하드웨어 시계를 덮어쓰면서 시간에 오차가 생길 수 있습니다.

다음 명령으로 `/etc/adjtime`파일을 자동으로 생성할 수 있습니다.

*   **UTC** (권장):

    **참고:** [UTC](https://en.wikipedia.org/wiki/Coordinated_Universal_Time "wikipedia:Coordinated Universal Time")를 하드웨어 시계로 사용한다고 해서 소프트웨어 시계가 UTC에 맞춰지는 것은 아닙니다.

     `# hwclock --systohc --utc` 
*   **localtime** (비추천, Windows의 기본값):

    **Warning:** _localtime_을 사용하는 것은 몇가지 고칠 수 없는 버그를 일으킵니다. 그러나 _localtime_은 계속해서 지원될 것입니다.

     `# hwclock --systohc --localtime` 

#### 커널 모듈

**도움말:** 이 부분은 단지 예시일 뿐입니다. 대개의 경우, 커널 모듈을 따로 설정할 필요는 없습니다. udev가 자동으로 필요한 커널 모듈을 로드할 것입니다. 자동으로 로드되지 않지만 필요한 커널 모듈이 있으며, 그 커널 모듈이 무엇인지 정확히 아는 경우에만 추가하십시오.

특정 커널 모듈을 부팅시에 로드하려면 `/etc/modules-load.d` 안에 `*.conf` 파일을 넣으십시오. .conf 파일의 이름은 그 모듈의 이름을 사용하는 것이 좋습니다.

 `# nano /etc/modules-load.d/virtio-net.conf` 

```
# Load 'virtio-net.ko' at boot.

virtio-net

```

한 `*.conf`파일로 여러개의 커널 모듈을 로드하고 싶다면, 모듈 이름을 줄바꿈하여 구분하면 됩니다. `#`이나 `;`로 시작하는 줄은 무시될 것입니다.

#### 호스트 네임

원하는 [호스트 네임](/index.php/Network_configuration#Set_the_hostname "Network configuration")((예:_arch_)을 다음과 같이 설정하십시오.

```
# echo _원하는_호스트_네임_ > /etc/hostname

```

`/etc/hosts`파일에도 같은 호스트네임을 추가하십시오.

 `# nano /etc/hosts` 

```
#
# /etc/hosts: static lookup table for host names
#

#<ip-address>	<hostname.domain.org>	<hostname>
127.0.0.1	localhost.localdomain	localhost _원하는_호스트_네임_	
::1		localhost.localdomain	localhost _원하는_호스트_네임_

# End of file

```

### 네트워크 설정하기

이제 네트워크를 다시 한 번 설정해야 합니다. 이번에 하는 설정은 라이브 환경이 아니라 새로 설치한 시스템에 적용될 것입니다. 부팅시에 자동으로 적용되게 한다는 점과, 디스크에 설정 내용을 저장하여 지속적으로 사용할 수 있다는 점 외에는 [위](#.EC.9D.B8.ED.84.B0.EB.84.B7_.EC.97.B0.EA.B2.B0_.EC.84.A4.EC.A0.95.ED.95.98.EA.B8.B0)에서 설명한 바와 비슷합니다.

우선, `ip link` 명령으로 사용하고자 하는 네트워크 인터페이스의 이름을 다시 확인합니다.

**참고:**

*   네트워크 설정에 대해 더 자세히 알아보고 싶다면 [Network Configuration](/index.php/Network_Configuration "Network Configuration")와 [Wireless network configuration](/index.php/Wireless_network_configuration "Wireless network configuration") 문서를 읽으십시오.
*   이전에 사용되던 인터페이스 이름(wlan*, eth* 등)을 사용하고 싶다면 `/etc/udev/rules.d/80-net-setup-link.rules`라는 빈 파일을 만드십시오. 이 파일은 `/usr/lib/udev/rules.d/`에 있는 동명의 파일에 대한 마스크로 작용할 것입니다.

#### 유선 네트워크

##### 유동 IP

dhcpcd 사용하기

하나의 유선 네트워크 연결만을 사용한다면, 네트워크 관리 서비스가 필요하지 않습니다. `dhcpcd` 서비스를 해당 인터페이스에 대해 활성화하기만 하면 됩니다.

```
# systemctl enable dhcpcd@_인터페이스_이름_.service

```

netctl 사용하기

`/etc/netctl/examples`에 있는 예시 프로파일 중 하나를 `/etc/netctl`로 복사합니다.

```
# cd /etc/netctl
# cp examples/ethernet-dhcp my_network

```

적절하게 프로파일을 편집합니다(ic|Interface}}를 `eth0`에서 실제 인터페이스 이름으로 바꿉니다)

```
# nano my_network

```

`my_network`프로파일을 활성화합니다.

```
# netctl enable my_network

```

**참고:** "Running in chroot, ignoring request."라는 메시지가 출력될 것입니다. 현재로서는 이 메시지를 무시해도 됩니다.

netctl-ifplugd 사용하기

**경고:** 이 방법은 `netctl enable 'profile'`과 같은 명령으로 프로파일을 직접 설정하는 방법과 같이 사용할 수 없습니다.

`netctl-ifplugd`를 사용할 수도 있습니다. `netctl-ifplugd`는 새로운 네트워크에 유동적으로 연결하는 것을 잘 처리합니다.

`netctl-ifplugd`를 사용하기 위해 [ifplugd](https://www.archlinux.org/packages/?name=ifplugd)를 설치합니다.

```
# pacman -S ifplugd

```

이제 원하는 인터페이스에 대하여 활성화시킵니다.

```
# systemctl enable netctl-ifplugd@_인터페이스_이름_.service

```

**도움말:** [netctl](/index.php/Netctl "Netctl")은 `netctl-auto`역시 제공합니다. `netctl-auto`는 `netctl-ifplugd`과 함께 작동하며 유선 프로파일을 관리합니다.

##### 고정 IP

netctl 사용하기

`/etc/netctl/examples`에 있는 예시 프로파일 중 하나를 `/etc/netctl`로 복사합니다.

```
# cd /etc/netctl
# cp examples/ethernet-static my_network

```

필요에 따라 복사해 온 프로파일을 편집합니다(`Interface`, `Address`, `Gateway`, `DNS` 등을 변경합니다.)

```
# nano my_network

```

`Address`가 알맞는 넷마스크를 포함하도록 유의합니다(예시 프로파일에 포함되어 있는 넷마스크 `/24`는 `255.255.255.0`에 해당합니다.}} 넷마스크가 맞지 않으면 프로파일이 작동하지 않습니다. [CIDR notation](https://en.wikipedia.org/wiki/Classless_Inter-Domain_Routing#CIDR_notation "wikipedia:Classless Inter-Domain Routing")를 참고하십시오.

만들어진 프로파일을 활성화하여 부팅시에 자동으로 연결되도록 합니다.

```
# netctl enable my_network

```

systemd-networkd 사용하기

[systemd-networkd](/index.php/Systemd-networkd "Systemd-networkd")항목을 참고하십시오.

#### 무선 네트워크

**참고:** [#무선 네트워크](#.EB.AC.B4.EC.84.A0_.EB.84.A4.ED.8A.B8.EC.9B.8C.ED.81.AC)에서 무선 어댑터의 펌웨어가 필요했다면 ([Wireless network configuration#Device driver](/index.php/Wireless_network_configuration#Device_driver "Wireless network configuration") 참고), 지금 필요한 펌웨어가 포함된 패키지를 설치하세요. 대개의 경우, [linux-firmware](https://www.archlinux.org/packages/?name=linux-firmware) 패키지에 필요한 펌웨어가 포함되어 있을 것입니다. 어떤 기기들의 펌웨어는 독립된 패키지로 들어있기도 합니다. 이 경우 해당 패키지를 설치하세요. 다음 명령은 펌웨어 패키지를 설치하는 한 예입니다. `# pacman -S zd1211-firmware` [Wireless network configuration#Installing driver/firmware](/index.php/Wireless_network_configuration#Installing_driver.2Ffirmware "Wireless network configuration") 항목을 참고하세요.

네트워크에 연결하기 위해 필요한 패키지 [iw](https://www.archlinux.org/packages/?name=iw)와 [wpa_supplicant](https://www.archlinux.org/packages/?name=wpa_supplicant)를 설치합니다.

```
# pacman -S iw wpa_supplicant

```

##### 무선 네트워크 추가하기

wifi-menu 사용

`wifi-menu`를 사용하기 위해 필요한 패키지 [dialog](https://www.archlinux.org/packages/?name=dialog)를 설치합니다.

```
# pacman -S dialog

```

시스템 설치가 끝난 후, 설치한 시스템으로 재부팅을 한 후에 다음 명령으로 무선 네트워크에 연결할 수 있습니다. (_인터페이스_이름_을 실제 무선 인터페이스 이름으로 바꾸세요)

```
# wifi-menu _인터페이스_이름_

```

**경고:** 저 명령은 시스템 설치를 마치고 재부팅을 하여 chroot 환경에서 빠져나온 **후**에 실행해야 합니다. chroot 되어있는 상태에서 저 명령을 내릴 경우, chroot 밖에서 이미 실행되고 있는 명령과 충돌합니다. `wifi-menu` 대신 다음 템플릿을 이용하여 네트워크 프로파일을 만들어 사용할 수 있습니다.

수동으로 netctl 프로파일 사용하기

`/etc/netctl/examples`에 있는 예시 프로파일 중 하나를 `/etc/netctl`에 복사합니다.

```
# cd /etc/netctl
# cp examples/wireless-wpa my-network

```

복사한 프로파일을 필요에 따라 편집합니다. (`Interface`, `ESSID`, `Key`를 수정합니다.)

```
# nano my-network

```

이렇게 해서 만든 프로파일을 활성화하여 부팅시 자동으로 연결되도록 합니다.

```
# netctl enable my-network

```

##### 알고 있는 네트워크에 자동으로 연결

**경고:** 이 방법은 `netctl enable _profile_`과 같은 명령으로 직접 프로파일을 설정하는 방법과 같이 사용될 수 없습니다.

`netctl-auto`를 사용하기 위해 필요한 패키지[wpa_actiond](https://www.archlinux.org/packages/?name=wpa_actiond)를 설치합니다.

```
# pacman -S wpa_actiond

```

`netctl-auto`서비스를 활성화합니다. `netctl-auto`는 자동으로 알려진 네트워크에 연결하고, 연결이 끊기는 상황이나 로밍 등을 처리합니다.

```
# systemctl enable netctl-auto@_인터페이스_이름_.service

```

**도움말:**

**Template error:** are you trying to use the = sign? Visit [Help:Template#Escape template-breaking characters](/index.php/Help:Template#Escape_template-breaking_characters "Help:Template") for workarounds.

[gummiboot](https://www.archlinux.org/packages/?name=gummiboot) 패키지를 설치하고 자동 설치 스크립트를 실행합니다. `**$esp**`를 자신의 EFI 시스템 파티션의 위치로 대체합니다. 대개의 경우 `/boot`입니다.

```
# pacman -S gummiboot
# gummiboot --path=**$esp** install

```

UEFI 펌웨어는 `**$esp**/EFI/boot`에 생성된 Gummiboot의 `bootx64.efi` stub을 인식할 것입니다. Gummiboot은 `.efi` stub을 사용하는 다른 운영체제들을 자동으로 인식합니다. 그러나 Gummiboot을 사용하기 위해서는 직접 설정 파일을 만들어야 합니다.

우선, `**$esp**/loader/entries/arch.conf` 파일을 만듭니다. `/dev/sdaX`를 새로 설치한 아치리눅스 시스템의 **루트** 파티션으로 바꾸어 아래의 내용을 arch.conf 안에 추가합니다.

 `# nano **$esp**/loader/entries/arch.conf` 

```
title          Arch Linux
linux          /vmlinuz-linux
initrd         /initramfs-linux.img
options        root=**/dev/sdaX** rw
```

그 다음, `**$esp**/loader/loader.conf` 파일을 만들고 아래 내용을 추가합니다. 단, timeout(gummiboot 메뉴가 보이는 시간) 값은 초 단위로 자신이 원하는 시간을 넣어주세요.

 `# nano **$esp**/loader/loader.conf` 

```
default  arch
timeout  5
```

더욱 자세한 내용은 [gummiboot](/index.php/Gummiboot "Gummiboot")문서를 참고하십시오.

##### GRUB

[grub](https://www.archlinux.org/packages/?name=grub) 패키지를 설치하고, grub 설치 스크립트를 실행하십시오. 아래 예시에서 `**$esp**`를 EFI 시스템 파티션의 위치로 바꾸어 실행시키면 됩니다.

```
# pacman -S grub
# grub-install --target=x86_64-efi --efi-directory=**$esp** --bootloader-id=arch_grub --recheck

```

직접 만든 grub.cfg파일을 사용하는 것에 문제는 없지만, 초보자들은 자동으로 만들어진 grub.cfg파일을 사용하는 것을 권장합니다. 아래의 명령으로 grub.cfg 파일을 자동 생성합니다.

```
# grub-mkconfig -o /boot/grub/grub.cfg

```

만일 시스템을 부팅할 수 없다면, [GRUB#UEFI firmware workaround](/index.php/GRUB#UEFI_firmware_workaround "GRUB") 항목을 참고하십시오. [GRUB](/index.php/GRUB "GRUB")문서에서 더 자세한 정보를 얻을 수 있습니다.

### 파티션을 언마운트 시키고 재부팅하기

chroot 환경에서 빠져나오십시오.

```
# exit

```

**참고:** 컴퓨터를 끌 때에 _systemd_가 자동으로 파티션을 언마운트하지만, 안전을 위해 `umount -R /mnt` 명령으로 파티션을 직접 언마운트해도 됩니다. 만약 `umount`가 partition is busy와 같은 오류 메시지를 출력하며 실패한다면, [fuser](https://en.wikipedia.org/wiki/fuser_(Unix) "wikipedia:fuser (Unix)")에서 그 이유를 찾아보십시오.

컴퓨터를 재부팅합니다.

```
# reboot

```

**도움말:** 컴퓨터가 꺼진 후에 반드시 설치 매체를 꺼내십시오. 그렇지 않으면 다시 설치 매체로 재부팅할 것입니다. 재부팅이 완료되고 나면, 위에서 설정했던 비밀번호로 "root" 사용자로 로그인할 수 있습니다. 만일 비밀번호를 설정하지 않았다면, 기본 비밀번호는 "root" 입니다.

## 설치 후

**축하합니다. 새로운 아치 리눅스 시스템에 오신 것을 환영합니다**

새로운 아치 리눅스 시스템이 이제 작동하는 리눅스 환경이 되었으며 입맛에 따라 설정을 변경할 준비가 되어 있습니다. 이제 기본적인 아치 리눅스 시스템이 설치되었습니다 여기에서부터 이 멋진 도구의 집합체를 당신이 원하거나 목적에 부합하는 어떤 것으로도 만들 수 있습니다.

[일반 추천 사항](/index.php/General_Recommendations_(%ED%95%9C%EA%B5%AD%EC%96%B4) "General Recommendations (한국어)") 문서를 읽는 것을 **강력히** 권장합니다. 특히 첫 두 섹션은 반드시 읽는 것이 좋습니다. 나머지 섹션들에서는 터치패드 설정, 사운드 설정, 그래픽 설정 등 여러가지 튜토리얼로 가는 링크들이 제공됩니다.

[Common Applications](/index.php/Common_Applications "Common Applications")는 여러분이 관심을 가질 만한 프로그램 목록을 다룹니다.

Retrieved from "[https://wiki.archlinux.org/index.php?title=Beginners%27_guide_(한국어)&oldid=411542](https://wiki.archlinux.org/index.php?title=Beginners%27_guide_(한국어)&oldid=411542)"

[Categories](/index.php/Special:Categories "Special:Categories"):

*   [About Arch (한국어)](/index.php/Category:About_Arch_(%ED%95%9C%EA%B5%AD%EC%96%B4) "Category:About Arch (한국어)")
*   [Getting and installing Arch (한국어)](/index.php/Category:Getting_and_installing_Arch_(%ED%95%9C%EA%B5%AD%EC%96%B4) "Category:Getting and installing Arch (한국어)")