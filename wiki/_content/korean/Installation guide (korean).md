이 문서는 공식 설치 매체로 부팅된 라이브 시스템에서 [아치 리눅스](/index.php/Arch_Linux_(%ED%95%9C%EA%B5%AD%EC%96%B4) "Arch Linux (한국어)")를 설치하는 방법을 안내합니다. 설치하기 전에 [FAQ](/index.php/FAQ "FAQ")를 읽어 보십시오. 이 안내서가 어떤 원칙에 따라 작성되었는지는 [읽기 도움](/index.php/Help:Reading "Help:Reading")을 보십시오.

자세한 사항은 여기 안내서에서 링크로 제공하는 해당 [아치위키](/index.php/ArchWiki:About "ArchWiki:About") 항목이나 각 프로그램의 [man page](/index.php/Man_page "Man page")를 보십시오. 대화나 질문으로 다른 사용자에게서 도움을 받으려면 [IRC 채널](/index.php/IRC_channel "IRC channel")이나 [포럼](https://bbs.archlinux.org/)을 이용하십시오.

## Contents

*   [1 설치에 앞서 할 일](#.EC.84.A4.EC.B9.98.EC.97.90_.EC.95.9E.EC.84.9C_.ED.95.A0_.EC.9D.BC)
    *   [1.1 키보드 레이아웃 설정](#.ED.82.A4.EB.B3.B4.EB.93.9C_.EB.A0.88.EC.9D.B4.EC.95.84.EC.9B.83_.EC.84.A4.EC.A0.95)
    *   [1.2 부트 방식 확인](#.EB.B6.80.ED.8A.B8_.EB.B0.A9.EC.8B.9D_.ED.99.95.EC.9D.B8)
    *   [1.3 인터넷에 연결](#.EC.9D.B8.ED.84.B0.EB.84.B7.EC.97.90_.EC.97.B0.EA.B2.B0)
    *   [1.4 시스템 시간 설정](#.EC.8B.9C.EC.8A.A4.ED.85.9C_.EC.8B.9C.EA.B0.84_.EC.84.A4.EC.A0.95)
    *   [1.5 디스크 파티션 나누기](#.EB.94.94.EC.8A.A4.ED.81.AC_.ED.8C.8C.ED.8B.B0.EC.85.98_.EB.82.98.EB.88.84.EA.B8.B0)
    *   [1.6 파티션 포맷](#.ED.8C.8C.ED.8B.B0.EC.85.98_.ED.8F.AC.EB.A7.B7)
    *   [1.7 파티션 마운트](#.ED.8C.8C.ED.8B.B0.EC.85.98_.EB.A7.88.EC.9A.B4.ED.8A.B8)
*   [2 설치](#.EC.84.A4.EC.B9.98)
    *   [2.1 미러 선택하기](#.EB.AF.B8.EB.9F.AC_.EC.84.A0.ED.83.9D.ED.95.98.EA.B8.B0)
    *   [2.2 base 패키지 설치하기](#base_.ED.8C.A8.ED.82.A4.EC.A7.80_.EC.84.A4.EC.B9.98.ED.95.98.EA.B8.B0)
*   [3 시스템 설정하기](#.EC.8B.9C.EC.8A.A4.ED.85.9C_.EC.84.A4.EC.A0.95.ED.95.98.EA.B8.B0)
    *   [3.1 Fstab](#Fstab)
    *   [3.2 Chroot](#Chroot)
    *   [3.3 시간대](#.EC.8B.9C.EA.B0.84.EB.8C.80)
    *   [3.4 로캘](#.EB.A1.9C.EC.BA.98)
    *   [3.5 호스트이름](#.ED.98.B8.EC.8A.A4.ED.8A.B8.EC.9D.B4.EB.A6.84)
    *   [3.6 네트워크 설정](#.EB.84.A4.ED.8A.B8.EC.9B.8C.ED.81.AC_.EC.84.A4.EC.A0.95)
    *   [3.7 Initramfs](#Initramfs)
    *   [3.8 루트 비밀번호](#.EB.A3.A8.ED.8A.B8_.EB.B9.84.EB.B0.80.EB.B2.88.ED.98.B8)
    *   [3.9 부트로더](#.EB.B6.80.ED.8A.B8.EB.A1.9C.EB.8D.94)
*   [4 재부팅](#.EC.9E.AC.EB.B6.80.ED.8C.85)
*   [5 설치가 끝난 후](#.EC.84.A4.EC.B9.98.EA.B0.80_.EB.81.9D.EB.82.9C_.ED.9B.84)

## 설치에 앞서 할 일

아치 리눅스는 최소 메모리가 512MB인 [x86_64](https://en.wikipedia.org/wiki/X86-64 "w:X86-64") 호환 기계에서 실행되어야 합니다. [base](https://www.archlinux.org/groups/x86_64/base/) 그룹의 모든 패키지를 설치하는 기본 설치를 하면 800MB 미만의 디스크 공간을 차지합니다. 인터넷 연결이 되어 있어야 공식 패키지 저장소에서 패키지를 다운로드할 수 있습니다.

[아치 리눅스 다운로드 및 설치](/index.php/Category:Getting_and_installing_Arch "Category:Getting and installing Arch")에 설명된 대로 설치 매체를 다운로드하고 부팅하십시오. 첫번째 [가상 콘솔](https://en.wikipedia.org/wiki/Virtual_console "w:Virtual console")로 루트 사용자로 로그인한 [Zsh](/index.php/Zsh "Zsh") 쉘 프롬프트가 제공될 것입니다. [systemctl(1)](http://jlk.fjfi.cvut.cz/arch/manpages/man/systemctl.1)과 같은 일반적인 명령어는 명령어 일부를 입력한 후 탭 키를 누르면 명령어 전체가 자동으로 완성되는 [탭 완성](https://en.wikipedia.org/wiki/Command-line_completion "w:Command-line completion")으로 입력될 수 있습니다.

다른 콘솔로 이동하려면, 예를 들어 설치를 하고 있는 콘솔이 아닌 다른 콘솔로 이동해 [ELinks](/index.php/ELinks "ELinks")를 실행해 이 안내서를 보는 경우라면 `Alt+*화살표*` [바로가기](/index.php/Keyboard_shortcuts "Keyboard shortcuts")를 사용하십시오. 설정 파일을 [편집](/index.php/Textedit "Textedit")하려면 [nano](/index.php/Nano#Usage "Nano"), [vi](https://en.wikipedia.org/wiki/vi "w:vi"), [vim](/index.php/Vim#Usage "Vim") 등을 사용하십시오.

### 키보드 레이아웃 설정

기본 [콘솔 키맵](/index.php/Console_keymap "Console keymap")은 [US(미국)](https://en.wikipedia.org/wiki/File:KB_United_States-NoAltGr.svg "w:File:KB United States-NoAltGr.svg")입니다. `ls /usr/share/kbd/keymaps/**/*.map.gz`를 실행하면 사용할 수 있는 레이아웃을 보여줍니다. 레이아웃을 변경하려면 해당 파일 이름을 경로와 파일 확장자를 제외하고 [loadkeys(1)](http://jlk.fjfi.cvut.cz/arch/manpages/man/loadkeys.1)에 덧붙입니다. 가령, `loadkeys de-latin1`를 실행하면 [독일어](https://en.wikipedia.org/wiki/File:KB_Germany.svg "w:File:KB Germany.svg") 키보드 레이아웃을 설정합니다.

[콘솔 폰트](/index.php/Console_fonts "Console fonts")는 `/usr/share/kbd/consolefonts/`에 있으며 키맵처럼 [setfont(8)](http://jlk.fjfi.cvut.cz/arch/manpages/man/setfont.8)로 설정할 수 있습니다.

### 부트 방식 확인

UEFI모드가 [UEFI](/index.php/UEFI "UEFI") 마더보드에서 활성화되면 [Archiso](/index.php/Archiso "Archiso")는 [systemd-boot](/index.php/Systemd-boot "Systemd-boot")로 아치 리눅스를 [부팅](/index.php/Boot "Boot")할 것입니다. 이를 확인하려면 [efivars](/index.php/UEFI#UEFI_variables "UEFI") 디렉토리를 보기 위해 다음과 같이 실행합니다.

```
 # ls /sys/firmware/efi/efivars

```

이 디렉토리가 존재하지 않는다면 시스템은 [BIOS](https://en.wikipedia.org/wiki/BIOS "w:BIOS")나 CSM 모드로 부팅될 것입니다. 자세한 내용은 자신의 마더보드 설명서에서 보십시오.

### 인터넷에 연결

설치 이미지는 [유선](https://git.archlinux.org/archiso.git/tree/configs/releng/airootfs/etc/udev/rules.d/81-dhcpcd.rules) 네트워크 장치를 사용하도록 [dhcpcd](/index.php/Dhcpcd "Dhcpcd") 데몬을 부팅 시에 실행합니다. 연결 상태를 [확인](/index.php/Network_configuration#Check_the_connection "Network configuration")하기 위해 다음을 실행해보십시오.

```
# ping archlinux.org

```

연결이 안 된다면 `systemctl stop dhcpcd@` `Tab`키로 *dhcpcd* 서비스를 중지하고 [네트워크 설정](/index.php/Network_configuration#Device_driver "Network configuration")을 보십시오.

**무선**연결은 [iw(8)](http://jlk.fjfi.cvut.cz/arch/manpages/man/iw.8), [wpa_supplicant(8)](http://jlk.fjfi.cvut.cz/arch/manpages/man/wpa_supplicant.8), [netctl](/index.php/Netctl#Wireless_.28WPA-PSK.29 "Netctl")을 사용할 수 있습니다. [무선 네트워크 설정](/index.php/Wireless_network_configuration "Wireless network configuration")을 참고하십시오.

### 시스템 시간 설정

[timedatectl(1)](http://jlk.fjfi.cvut.cz/arch/manpages/man/timedatectl.1)을 사용해 시스템의 시간을 정확하게 설정하십시오.

```
# timedatectl set-ntp true

```

`timedatectl status`을 실행해 현재의 상태를 확인하십시오.

### 디스크 파티션 나누기

라이브 시스템은 디스크를 `/dev/sda`와 같은 *블록 장치*로 인식합니다. [lsblk](/index.php/Lsblk "Lsblk") 나 *fdisk*로 이러한 장치를 확인할 수 있습니다. 이때 `rom`, `loop`, `airoot`와 같은 장치는 무시하십시오.

```
# fdisk -l

```

다음의 *파티션*(숫자가 뒤에 붙어 있음)은 해당 장치에 필요합니다.

*   루트 디렉토리`/`용 파티션.
*   [UEFI](/index.php/UEFI "UEFI")가 활성화되었다면 [EFI 시스템 파티션](/index.php/EFI_System_Partition "EFI System Partition").

[스왑 공간](/index.php/Swap_space "Swap space")을 위한 독립된 파티션이나 [스왑 파일](/index.php/Swap_file "Swap file").

*파티션 테이블*을 수정하려면 [fdisk](/index.php/Fdisk "Fdisk")나 [parted](/index.php/Parted "Parted")를 사용하십시오. 자세한 내용은 [파티션 나누기](/index.php/Partitioning "Partitioning")를 참고하십시오.

[LVM](/index.php/LVM "LVM"), [디스크 암호화](/index.php/Disk_encryption "Disk encryption"), [RAID](/index.php/RAID "RAID")용 스택 블록 장치를 만들려면 지금 하십시오.

### 파티션 포맷

파티션을 나눈 후에 각 파티션을 알맞은 [파일 시스템](/index.php/File_system "File system")으로 포맷하십시오. 예를 들어, `/dev/*sda1*`의 루트 파티션을 `*ext4*`로 포맷하려면 다음을 실행하십시오.

```
# mkfs.*ext4* /dev/*sda1*

```

자세한 사항은 [파일 시스템](/index.php/File_systems#Create_a_file_system "File systems")문서를 참고하십시오.

### 파티션 마운트

`/mnt`에 루트 파티션의 파일 시스템을 [마운트](/index.php/Mount "Mount")해야 합니다.

예)

```
# mount /dev/*sda1* /mnt 

```

남아 있는 파티션의 마운트 포인트를 만들어서 파티션을 알맞게 마운트하십시오.

예)

```
# mkdir /mnt/*boot*
# mount /dev/*sda2* /mnt/*boot*

```

[genfstab](https://git.archlinux.org/arch-install-scripts.git/tree/genfstab.in)이 나중에 마운트된 파일 시스템과 스왑 공간을 인식할 것입니다.

## 설치

### 미러 선택하기

설치할 패키지는 [미러 서버](/index.php/Mirrors "Mirrors")에서 다운로드해야하는데 미러 서버는 `/etc/pacman.d/mirrorlist`에서 지정됩니다. 라이브 시스템에서는 모든 서버가 선택되어 있고 설치 이미지가 만들어진 시점에서 동기화 상태 및 속도에 따라 정렬되어 있습니다.

패키지를 다운로드할 때 미러 목록에서 위에 있는 미러 서버순으로 우선 순위가 주어집니다. 따라서 자신의 위치나 기타 조건에 맞게 이 미러 목록을 수정할 수 있습니다.

*pacstrap*이 이 미러 목록 파일을 새로운 시스템으로 복사하기 때문에 이 파일을 제대로 수정해 둘 필요가 있습니다.

### base 패키지 설치하기

[pacstrap](https://projects.archlinux.org/arch-install-scripts.git/tree/pacstrap.in) 스크립트를 사용해 [base](https://www.archlinux.org/groups/x86_64/base/) 패키지 그룹을 설치합니다.

```
# pacstrap /mnt base 

```

이 그룹은 [btrfs-progs](https://www.archlinux.org/packages/?name=btrfs-progs)나 특정 무선 펌웨어와 같은 라이브 설치에서의 모든 도구를 포함하고 있진 않습니다. [packages.both](https://projects.archlinux.org/archiso.git/tree/configs/releng/packages.both)에서 비교해 보십시오.

패키지와 [base-devel](https://www.archlinux.org/groups/x86_64/base-devel/)과 같은 그룹 등을 추가로 설치하려면 패키지 이름을 위의 명령 뒤에 덧붙이면 됩니다. 패키지 사이는 공백으로 구분해야 합니다. 또는 [chroot](#Chroot) 단계를 지나서 [pacman](/index.php/Pacman "Pacman") 명령으로 패키지를 설치할 수 있습니다.

## 시스템 설정하기

### Fstab

다음의 명령어를 사용해 [fstab](/index.php/Fstab "Fstab") 파일을 생성합니다. 이때 [UUID](/index.php/UUID "UUID")를 사용하려면 `-U`옵션을, 레이블을 사용하려면 `-L` 옵션을 사용할 수 있습니다.

```
# genfstab -U /mnt >> /mnt/etc/fstab

```

생선된 `/mnt/etc/fstab`파일을 확인해 오류가 있으면 수정하십시오.

### Chroot

새로운 시스템으로 [Change root](/index.php/Change_root "Change root")합니다.

```
# arch-chroot /mnt

```

### 시간대

[시간대](/index.php/Time_zone "Time zone")를 설정합니다.

```
# ln -sf /usr/share/zoneinfo/*지역*/*도시* /etc/localtime

```

[hwclock(8)](http://jlk.fjfi.cvut.cz/arch/manpages/man/hwclock.8)를 실행해 `/etc/adjtime`를 생성합니다.

```
# hwclock --systohc

```

위 명령은 하드웨어 클럭을 [UTC](https://en.wikipedia.org/wiki/UTC "w:UTC")로 설정합니다. 자세한 내용은 [시간 표준](/index.php/Time#Time_standard "Time")을 참고하십시오.

### 로캘

`/etc/locale.gen`에서 `en_US.UTF-8 UTF-8`과 필요한 [localization](/index.php/Localization "Localization")을 찾아 주석 표시를 제거하고 `locale-gen`을 실행해 로캘을 생성합니다.

```
# locale-gen

```

`LANG` [변수](/index.php/Variable "Variable")를 [locale.conf(5)](http://jlk.fjfi.cvut.cz/arch/manpages/man/locale.conf.5)에 설정합니다.

예)

 `/etc/locale.conf`  `LANG=*en_US.UTF-8*` 

[키보도 레이아웃을 설정](#.ED.82.A4.EB.B3.B4.EB.93.9C_.EB.A0.88.EC.9D.B4.EC.95.84.EC.9B.83_.EC.84.A4.EC.A0.95)한다면 [vconsole.conf(5)](http://jlk.fjfi.cvut.cz/arch/manpages/man/vconsole.conf.5)에 변경사항을 반영하십시오.

예)

 `/etc/vconsole.conf`  `KEYMAP=*de-latin1*` 

### 호스트이름

[hostname(5)](http://jlk.fjfi.cvut.cz/arch/manpages/man/hostname.5) 파일을 만드십시오.

 `/etc/hostname` 
```
*myhostname*

```

[hosts(5)](http://jlk.fjfi.cvut.cz/arch/manpages/man/hosts.5)에 항목을 추가할 수 있습니다.

 `/etc/hosts` 
```
127.0.0.1	localhost.localdomain	localhost
::1		localhost.localdomain	localhost
**127.0.1.1	*myhostname*.localdomain	*myhostname***

```

[호스트이름 설정](/index.php/Network_configuration#Set_the_hostname "Network configuration")을 참고하십시오.

### 네트워크 설정

새로 설치한 시스템에서는 기본적으로 네트워크 연결이 활성화되어 있지 않습니다. [네트워크 관리자](/index.php/Network_configuration#Network_managers "Network configuration")를 참고하십시오.

[무선 설정](/index.php/Wireless_configuration "Wireless configuration")을 하려면 [iw](https://www.archlinux.org/packages/?name=iw)와 [wpa_supplicant](https://www.archlinux.org/packages/?name=wpa_supplicant), 추가로 필요한 [펌웨어 패키지](/index.php/Wireless#Installing_driver.2Ffirmware "Wireless")를 [설치](/index.php/Install "Install")하십시오. *wifi-menu*를 사용하고 싶으면 [dialog](https://www.archlinux.org/packages/?name=dialog)를 설치하십시오.

### Initramfs

새로운 *initramfs*를 따로 생성할 필요는 없습니다. *pacstrap*으로 [linux](https://www.archlinux.org/packages/?name=linux) 패키지를 설치할 때 [mkinitcpio](/index.php/Mkinitcpio "Mkinitcpio")가 실행되었기 때문입니다.

특정한 설정 때문에 [mkinitcpio.conf(5)](http://jlk.fjfi.cvut.cz/arch/manpages/man/mkinitcpio.conf.5) 파일을 수정하면 다음을 실행해 initramfs 이미지를 다시 만드십시오.

```
# mkinitcpio -p linux

```

### 루트 비밀번호

루트 사용자의 [비밀번호](/index.php/Password "Password")를 설정하십시오.

```
# passwd

```

### 부트로더

리눅스를 인식할 수 있는 부트 로더를 설치해야 합니다. 설치할 [부트 로더](/index.php/Category:Boot_loaders "Category:Boot loaders")를 보십시오.

인텔 CPU인 시스템이라면 [intel-ucode](https://www.archlinux.org/packages/?name=intel-ucode) 패키지를 추가로 설치하고 [마이크로코드를 활성화](/index.php/Microcode#Enabling_Intel_microcode_updates "Microcode")하십시오.

## 재부팅

chroot 환경에서 `exit`를 입력하거나 `Ctrl+D`를 눌러서 그 환경을 종료하십시오.

원한다면 앞서 마운트했던 파티션들을 `umount -R /mnt`명령으로 직접 언마운트할 수도 있습니다. 이렇게 하면 "사용중"인 파티션을 알 수 있고 [fuser(1)](http://jlk.fjfi.cvut.cz/arch/manpages/man/fuser.1)로 그 원인을 찾아볼 수 있습니다.

마지막으로 `reboot` 명령으로 컴퓨터를 재부팅합니다. 마운트된 파티션이 남아있다면 *systemd*가 자동으로 언마운트할 것입니다. 설치 매체를 꼭 제거한 후에 새로운 시스템에 루트 계정으로 로그인하십시오.

## 설치가 끝난 후

시스템 관리에 대한 안내나 GUI 환경 설정, 소리, 터치패드 등 추가적으로 해야할 일은 [일반 추천 사항](/index.php/General_recommendations_(%ED%95%9C%EA%B5%AD%EC%96%B4) "General recommendations (한국어)")을 보십시오.

관심을 가질 만한 [프로그램 목록](/index.php/List_of_applications "List of applications")도 참고하십시오.