**도움말:** 이 문서는 초보자 안내서 전체 문서의 일부입니다. 초보자 안내서 전체를 보려면 **[여기](/index.php/Beginners%27_Guide_(%ED%95%9C%EA%B5%AD%EC%96%B4) "Beginners' Guide (한국어)")**를 클릭하십시오.

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

**[초보자 안내서](/index.php/Beginners%27_Guide_(%ED%95%9C%EA%B5%AD%EC%96%B4) "Beginners' Guide (한국어)")**

* * *

**준비하기** >> [설치하기](/index.php/Beginners%27_Guide/Installation_(%ED%95%9C%EA%B5%AD%EC%96%B4) "Beginners' Guide/Installation (한국어)") >> [기타](/index.php/Beginners%27_Guide/Extra_(%ED%95%9C%EA%B5%AD%EC%96%B4) "Beginners' Guide/Extra (한국어)")