## Contents

*   [1 Zavaděč](#Zavad.C4.9B.C4.8D)
*   [2 Jádro](#J.C3.A1dro)
*   [3 Initframs](#Initframs)
*   [4 Init proces](#Init_proces)
*   [5 Viz také](#Viz_tak.C3.A9)

## Zavaděč

Poté, co je sytém zapnut a [POST](https://en.wikipedia.org/wiki/Power-on_self_test "wikipedia:Power-on self test") dokončen, nalezne BIOS preferované bootovací médium a předá kontrolu programu v [Master Boot Record](/index.php/Master_Boot_Record "Master Boot Record") na tomto médiu. Na GNU/Linux počítači se často v MBR nalézá zavaděč jako je např. [GRUB](/index.php/GRUB_(%C4%8Cesky) "GRUB (Česky)") nebo [LILO](/index.php/LILO_(%C4%8Cesky) "LILO (Česky)"). Zavaděč pak uživateli nabídne možné operační systémy pro bootování, např. Arch Linux a Windows v tzv. [dual-boot sestavě](/index.php/Windows_and_Arch_Dual_Boot "Windows and Arch Dual Boot"). Jakmile je Arch zvolen, zavaděč nahraje obraz jádra (`vmlinuz-linux`) a prvotní obraz root filesystému (`initramfs-linux.img`) do paměti a spustí jádro, kterému předá adresu umístění obrazů v paměti.

## Jádro

Jádro je základ operačního systému. Operuje v nízké úrovni systému (_kernelspace_) a zprostředkovává interakce mezi hardwarem a programy. K dosažení efektivního využití CPU používá jádro plánovač, který na základě priority střídavě přiděluje jednotlivým procesům procesorový čas, čímž se docílí iluze, že je více programů prováděno zároveň.

## Initframs

Po zavedení jádra se rozbalí [initramfs](/index.php?title=Mkinitcpio_(%C4%8Cesky)&action=edit&redlink=1 "Mkinitcpio (Česky) (page does not exist)") (initial RAM filesystem), který se stane prvotním kořenovým souborovým systémem. Jádro poté spustí `/init` jako první proces, čímž začíná _early userspace_.

Účelem initramfs je zavést systém do stavu, kdy už má přístup ke kořenovému souborovému systému (viz [FHS](/index.php/FHS "FHS")). To znamená, že moduly potřebné k přístupu k zařízením, jako jsou např. IDE, SCSI, SATA nebo USB/FW, musí být možno zavést do jádra přímo z initramfs (pokud dané moduly nejsou zkompilovány přímo v jádře); jakmile se z initramfs naloadují správné moduly (buď explicitně nějakým programem či skriptem, nebo prostřednictvím [udev](/index.php/Udev_(%C4%8Cesky) "Udev (Česky)")), bootovací proces pokračuje. Díky tomu může initramfs obsahovat pouze moduly potřebné k přístupu ke kořenovému souborovému systému; nemusí tedy obsahovat všechny moduly, které by mohly být kdy použity. Většina modulů bude zavedena později během init procesu prostřednictvím udev.

## Init proces

Během poslední fáze _early userspace_ je připojen skutečný kořenový souborový systém, který následně nahradí prvotní kořenový souborový systém. Nakonec je spuštěn `/sbin/init`, který nahradí proces `/init`.

Dříve Arch Linux využíval [SysVinit](/index.php/SysVinit "SysVinit") jako init proces. Nyní při nové instalaci již je jako výchozí [systemd](/index.php/Systemd "Systemd"). Uživatelům, kteří nadále používají [SysVinit](/index.php/SysVinit "SysVinit"), je doporučeno přejít k [systemd](/index.php/Systemd "Systemd").

## Viz také

*   [Early Userspace in Arch Linux](http://archlinux.me/brain0/2010/02/13/early-userspace-in-arch-linux/)
*   [Inside the Linux boot process](http://www.ibm.com/developerworks/linux/library/l-linuxboot/)
*   [Boot with GRUB](http://www.linuxjournal.com/article/4622)
*   [Wikipedia:Linux startup process](https://en.wikipedia.org/wiki/Linux_startup_process "wikipedia:Linux startup process")
*   [Wikipedia:initrd](https://en.wikipedia.org/wiki/initrd "wikipedia:initrd")
*   [Boot Linux Grub Into Single User Mode](http://www.cyberciti.biz/faq/grub-boot-into-single-user-mode/)