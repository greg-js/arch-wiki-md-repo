이 문서는 공식 설치 매체를 이용한 [아치 리눅스](/index.php/Arch_Linux_(%ED%95%9C%EA%B5%AD%EC%96%B4) "Arch Linux (한국어)") 설치 방법을 안내합니다. 설치를 시작하기 전에 [FAQ](/index.php/FAQ "FAQ") 문서를 확인하는 것이 좋습니다. 더 자세하고 긴 설치 안내서를 원한다면 [초보자 안내서](/index.php/Beginners%27_guide_(%ED%95%9C%EA%B5%AD%EC%96%B4) "Beginners' guide (한국어)")로 이동하십시오. 특수한 설치를 원하는 경우 [Category:Getting and installing Arch](/index.php/Category:Getting_and_installing_Arch "Category:Getting and installing Arch")의 문서들을 확인하십시오.

대개의 경우, 커뮤니티가 관리하는 이 위키나 각 프로그램의 [man page](/index.php/Man_page "Man page")를 통해 정보와 도움을 얻을 수 있습니다. 다른 사람들과 대화하며 도움을 얻고 싶다면, [IRC 채널](/index.php/IRC_channel "IRC channel")이나 [포럼](https://bbs.archlinux.org/)을 사용하십시오.

## Contents

*   [1 내려받기](#.EB.82.B4.EB.A0.A4.EB.B0.9B.EA.B8.B0)
*   [2 설치 준비하기](#.EC.84.A4.EC.B9.98_.EC.A4.80.EB.B9.84.ED.95.98.EA.B8.B0)
    *   [2.1 키보드 레이아웃 설정](#.ED.82.A4.EB.B3.B4.EB.93.9C_.EB.A0.88.EC.9D.B4.EC.95.84.EC.9B.83_.EC.84.A4.EC.A0.95)
    *   [2.2 디스크 파티션 설정](#.EB.94.94.EC.8A.A4.ED.81.AC_.ED.8C.8C.ED.8B.B0.EC.85.98_.EC.84.A4.EC.A0.95)
    *   [2.3 파티션 포맷](#.ED.8C.8C.ED.8B.B0.EC.85.98_.ED.8F.AC.EB.A7.B7)
    *   [2.4 파티션 마운트](#.ED.8C.8C.ED.8B.B0.EC.85.98_.EB.A7.88.EC.9A.B4.ED.8A.B8)
    *   [2.5 인터넷에 연결](#.EC.9D.B8.ED.84.B0.EB.84.B7.EC.97.90_.EC.97.B0.EA.B2.B0)
*   [3 설치하기](#.EC.84.A4.EC.B9.98.ED.95.98.EA.B8.B0)
    *   [3.1 미러 선택](#.EB.AF.B8.EB.9F.AC_.EC.84.A0.ED.83.9D)
    *   [3.2 base 패키지 설치하기](#base_.ED.8C.A8.ED.82.A4.EC.A7.80_.EC.84.A4.EC.B9.98.ED.95.98.EA.B8.B0)
    *   [3.3 시스템 설정](#.EC.8B.9C.EC.8A.A4.ED.85.9C_.EC.84.A4.EC.A0.95)
    *   [3.4 부트로더 설치](#.EB.B6.80.ED.8A.B8.EB.A1.9C.EB.8D.94_.EC.84.A4.EC.B9.98)
    *   [3.5 언마운트와 재부팅](#.EC.96.B8.EB.A7.88.EC.9A.B4.ED.8A.B8.EC.99.80_.EC.9E.AC.EB.B6.80.ED.8C.85)
*   [4 설치 후](#.EC.84.A4.EC.B9.98_.ED.9B.84)

## 내려받기

[아치 리눅스 내려받기](https://www.archlinux.org/download/)에서 아치 리눅스 ISO를 내려받습니다. 이 ISO 이미지는 x86_64와 i686 아키텍처를 둘 다 지원하는 하이브리드 이미지입니다. 어느 라이브 환경으로 부팅할지는 해당 시스템의 CPU 아키텍처 및 사용자의 선택에 의해 결정됩니다.

설치 매체 이미지에는 패키지가 포함되어 있지 않습니다. 아치 리눅스를 설치하기 위해서는 네트워크에 연결하여 원격 저장소에서 패키지를 내려받아 설치해야 합니다. 따라서 반드시 인터넷에 연결되어 있어야 합니다.

ISO 이미지를 다운로드받은 후에는 반드시 전자서명 키를 이용하여 파일 무결성 검사를 실행하십시오(`pacman-key -v *설치매체_이미지.iso.sig*`. 혹은 체크섬 파일을 이용하여 파일 무결성을 검사할 수 있습니다`md5sum *설치매체_이미지.iso*`). 체크섬 파일들은 내려받기 페이지에서 설치 매체 이미지와 함께 내려받을 수 있습니다.

마지막으로, 설치 매체 이미지는 CD에 굽거나, ISO 파일로서 마운트하거나, [USB 드라이브](/index.php/USB_Installation_Media "USB Installation Media")에 기록할 수 있습니다.

## 설치 준비하기

설치 매체 이미지를 부팅한 후에, 다음 단계들을 통해 설치를 위한 준비를 해야 합니다.

### 키보드 레이아웃 설정

기본 키보드 레이아웃은 US(미국)입니다. `loadkeys *keymap_file*` 명령으로 다른 키보드 레이아웃을 로드할 수 있습니다. 키맵 파일들은 `/usr/share/kbd/keymaps/`에 있습니다. (파일 경로와 파일 확장자는 생략할 수 있습니다.)

### 디스크 파티션 설정

자세한 사항은 [partitioning](/index.php/Partitioning "Partitioning")을 보십시오. 몇가지 특수한 파티션을 만들어야 할 수 있습니다. [UEFI#EFI System Partition](/index.php/UEFI#EFI_System_Partition "UEFI")문서와 [GRUB BIOS 부트 파티션](/index.php/GRUB#GUID_Partition_Table_.28GPT.29_specific_instructions "GRUB") 문서를 참고하십시오. [LVM](/index.php/LVM "LVM"), [드라이브 암호화](/index.php/Disk_encryption "Disk encryption"), [RAID](/index.php/RAID "RAID")를 위하여 스택 블록 장치를 만들고자 한다면, 이 단계에서 만들도록 하십시오.

### 파티션 포맷

자세한 사항은 [File systems](/index.php/File_systems#Create_a_filesystem "File systems")문서를 참고하십시오. 스왑을 사용하고 싶다면 [Swap](/index.php/Swap "Swap")문서를 보십시오.

### 파티션 마운트

`/mnt`에 루트 파티션을 마운트해야 합니다. 그 다음, 필요한 디렉토리를(`/mnt/boot`, `/mnt/home`등)를 만들어 추가적인 파티션들을 마운트합니다. 이렇게 해야 나중에 `genfstab` 명령을 실행했을 때 추가 파티션들이 자동으로 인식되어 fstab 파일에 추가됩니다.

### 인터넷에 연결

유선 연결을 사용할 경우, DHCP Discovery를 이용하여 자동으로 인터넷에 연결될 것입니다. [Network configuration](/index.php/Network_configuration "Network configuration")문서에서 더 자세한 내용을 읽으십시오. 지원되는 무선 네트워크 장치를 사용하고 있다면, `wifi-menu` 명령을 내려 네트워크에 연결하십시오. [Wireless network configuration](/index.php/Wireless_network_configuration "Wireless network configuration")문서에 더 자세한 내용이 있습니다. 고정 IP나 네트워크 관리 도구를 사용해야 한다면, `systemctl stop dhcpcd.service` 명령으로 DHCP Discovery 서비스를 종료하고, [Netctl](/index.php/Netctl "Netctl")문서를 읽으십시오.

## 설치하기

### 미러 선택

설치하기에 앞서 `/etc/pacman.d/mirrorlist`를 편집해서 자신이 선호하는 미러를 처음에 배치합니다. 나중에 `pacstrap`을 실행하여 이 파일을 새로운 시스템에 복사하기 때문에 지금 제대로 편집하면 다시 편집할 필요가 없습니다.

### base 패키지 설치하기

[pacstrap](https://github.com/falconindy/arch-install-scripts/blob/master/pacstrap.in)스크립트를 사용하여 기본 시스템을 설치합니다. [AUR](/index.php/AUR "AUR") 또는 [ABS](/index.php/ABS "ABS")에서 소프트웨어를 컴파일하려면 ‘’base-devel'’ 패키지(꾸러미)도 설치해야 합니다.

```
# pacstrap /mnt base base-devel

```

부트로더 등 추가로 설치하고 싶은 패키지나 패키지 그룹이 있다면 패키지 이름을 위의 명령 뒤에 덧붙이면 됩니다. 패키지 사이는 공백으로 구분해야 합니다.

### 시스템 설정

다음의 명령어를 사용해 [fstab](/index.php/Fstab "Fstab")를 생성합니다. 이때 UUID를 사용하려면 `-U`, 레이블을 사용하려면 `-L` 옵션을 사용할 수 있습니다.

```
# genfstab -p /mnt >> /mnt/etc/fstab

```

다음으로 새로 설치할 시스템에 [chroot](/index.php/Chroot "Chroot")하여 들어갑니다.

```
# arch-chroot /mnt

```

`/etc/hostname`에 자신의 [호스트 이름](/index.php/Hostname "Hostname")을 적습니다.

```
# echo *computer_name* > /etc/hostname

```

시간대를 설정합니다.

```
# ln -sf /usr/share/zoneinfo/*zone*/*subzone* /etc/localtime

```

`/etc/locale.gen`에서 원하는 로캘을 찾아 주석 표시를 제거하고 `locale-gen`을 실행해 로캘을 생성합니다.

로캘 설정을 `/etc/locale.conf`에 밝힙니다. 선택적으로 `$HOME/.config/locale.conf`에도 밝힐 수 있습니다.

```
# echo LANG=*선택한_로캘* > /etc/locale.conf

```

콘솔 [키맵](/index.php/Keymap "Keymap") 및 [글꼴](/index.php/Fonts#Console_fonts "Fonts") 설정을 `/etc/vconsole.conf`에 추가합니다.

새로 설치한 시스템에 다시 한번 네트워크를 설정합니다. [네트워크 설정](/index.php/Network_configuration "Network configuration")과 [Wireless network configuration](/index.php/Wireless_network_configuration "Wireless network configuration")문서를 보십시오.

자신의 필요에 따라 `/etc/mkinitcpio.conf`([mkinitcpio](/index.php/Mkinitcpio "Mkinitcpio") 참조)를 편집하고 다음의 명령어로 초기 램 디스크를 만듭니다.

```
# mkinitcpio -p linux

```

`passwd` 명령으로 루트 비밀번호를 설정하세요.

### 부트로더 설치

[부트로더](/index.php/Boot_loaders "Boot loaders") 항목에서 설치 가능한 부트로더와 설정 방법을 읽으십시오.

### 언마운트와 재부팅

아직 chroot 환경 안에 있다면 `exit`를 입력하거나 `Ctrl+D`를 눌러서 그 환경을 종료하세요.

`umount -R /mnt` 명령으로 선택적으로 앞서 마운트했던 파티션들을 언마운트할 수 있습니다. 이렇게 하면 "바쁜(busy)" 파티션들을 찾아내고, [여기에서](https://en.wikipedia.org/wiki/fuser_(Unix) 그 원인을 찾아볼 수 있습니다.

`reboot` 명령을 통해 컴퓨터를 재부팅합니다. 마운트된 파티션이 남아있다면 *systemd*가 자동으로 언마운트시킬 것입니다. 이제 재부팅하여 루트 계정으로 새 시스템에 로그인합니다. 컴퓨터가 꺼진 후에 반드시 설치 매체를 꺼내십시오.

## 설치 후

시스템 관리에 대한 안내나 GUI 환경 설정, 소리, 터치패드 등 설치 완료 후 할 일에 대한 안내가 필요하다면 [General recommendations (한국어)](/index.php/General_recommendations_(%ED%95%9C%EA%B5%AD%EC%96%B4) "General recommendations (한국어)") 문서를 참고하십시오.

[Common Applications](/index.php/Common_Applications "Common Applications")는 여러분이 관심을 가질 만한 프로그램 목록을 다룹니다.