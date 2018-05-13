Bu doküman, Arch Linux'u yüklemek için kullanılan canlı sistem kılavuzudur. Kurulumdan önce, [Sıkça sorulan sorulara](/index.php/Frequently_asked_questions_(T%C3%BCrk%C3%A7e) "Frequently asked questions (Türkçe)") bakmanız önerilmektedir. Bu belgede kullanılan lisanslar için, bakınız [Help:Reading](/index.php/Help:Reading "Help:Reading").

Daha ayrıntılı talimatlar için, bu kılavuzdan sırasıyla [ArchWiki](/index.php/ArchWiki:About "ArchWiki:About") makalelerine ya da çeşitli programların olduğu linklere' [man pages](/index.php/Man_page "Man page"), bakınız. İnteraktif yardım için, [IRC kanalını](/index.php/IRC_channel "IRC channel") ve [forumu](https://bbs.archlinux.org/) kullanabilirsiniz.

## Contents

*   [1 Kurulum Öncesi](#Kurulum_.C3.96ncesi)
    *   [1.1 Klavye düzenini ayarla](#Klavye_d.C3.BCzenini_ayarla)
    *   [1.2 Önyükleme modunu doğrula](#.C3.96ny.C3.BCkleme_modunu_do.C4.9Frula)
    *   [1.3 İnternete bağlan](#.C4.B0nternete_ba.C4.9Flan)
    *   [1.4 Sistem saatini güncelle](#Sistem_saatini_g.C3.BCncelle)
    *   [1.5 Diskleri bölümlendir](#Diskleri_b.C3.B6l.C3.BCmlendir)
    *   [1.6 Bölümleri biçimlendir](#B.C3.B6l.C3.BCmleri_bi.C3.A7imlendir)
    *   [1.7 Dosya sistemerini bağla](#Dosya_sistemerini_ba.C4.9Fla)
*   [2 Kurulum](#Kurulum)
    *   [2.1 Mirror'ları seç](#Mirror.27lar.C4.B1_se.C3.A7)
    *   [2.2 Temel paketleri kurun](#Temel_paketleri_kurun)
*   [3 Sistemi yapılandır](#Sistemi_yap.C4.B1land.C4.B1r)
    *   [3.1 Fstab](#Fstab)
    *   [3.2 Chroot](#Chroot)
    *   [3.3 Zaman dilimi](#Zaman_dilimi)
    *   [3.4 Locale](#Locale)
    *   [3.5 Hostname](#Hostname)
    *   [3.6 Network configuration](#Network_configuration)
    *   [3.7 Initramfs](#Initramfs)
    *   [3.8 Root password](#Root_password)
    *   [3.9 Boot loader](#Boot_loader)
*   [4 Reboot](#Reboot)
*   [5 Post-installation](#Post-installation)

## Kurulum Öncesi

Arch Linux en az 512 MB RAM'e sahip olan herhangi bir [x86_64](https://en.wikipedia.org/wiki/X86-64 "w:X86-64") uyumlu makinede çalışır. [base](https://www.archlinux.org/groups/x86_64/base/) grubundaki tüm paketleri içeren basit bir kurulum 800 megabyte'tan az bir disk alanı kaplar. Kurulum esnasında paketlerin veri havuzundan indirilmesi gerektiğinden, çalışan bir internet bağlantısı gereklidir.

Yükleme medyasını [Category:Getting and installing Arch](/index.php/Category:Getting_and_installing_Arch "Category:Getting and installing Arch") sayfasında açıklandığı gibi indiriniz ve önyükleyiniz. İlk sanal konsola root kullanıcısı olarak giriş yapacaksınız ve [Zsh](/index.php/Zsh "Zsh") komut istemiyle karşılaşacaksınız. [systemctl(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/systemctl.1) gibi yaygın komutlar [Tab tuşuyla tamamlanabilir.](https://en.wikipedia.org/wiki/Command-line_completion "w:Command-line completion")

Farklı bir konsola geçmek için, örneğin kurulum esnasında bu rehberi [ELinks](/index.php/ELinks "ELinks") ile görüntülemek için, `Alt+*ok tuşu*` [kısayolunu](/index.php/Keyboard_shortcuts "Keyboard shortcuts") kullanabilirsiniz. Yapılandırma dosyalarını [düzenlemek](/index.php/Textedit "Textedit") için, [nano](/index.php/Nano#Usage "Nano"), [vi](https://en.wikipedia.org/wiki/vi "w:vi") veya [vim](/index.php/Vim#Usage "Vim") kullanılabilir.

### Klavye düzenini ayarla

Varsayılan [konsol klavye düzeni](/index.php/Console_keymap "Console keymap") [US](https://en.wikipedia.org/wiki/File:KB_United_States-NoAltGr.svg "w:File:KB United States-NoAltGr.svg")'tır. Mevcut klavye düznlerini görüntülemek için, `ls /usr/share/kbd/keymaps/**/*.map.gz` komudunu çalıştırın. Klavye düzenini değiştirmek için, [loadkeys(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/loadkeys.1) komutuna yolunu ve uzantısını atlayarak, eşdeğer dosya adını yekleyin. Örneğin,[Türkçe q](https://en.wikipedia.org/wiki/File:KB_Turkey.svg "w:File:KB Turkey.svg") klavye düzeni için `loadkeys trq` komudunu çalıştırın.

[Konsol fontları](/index.php/Console_fonts "Console fonts") `/usr/share/kbd/consolefonts/` dizisinde yer almaktadır ve aynı şekilde [setfont(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/setfont.8) komudu ile ayarlanabilir.

### Önyükleme modunu doğrula

Bir [UEFI](/index.php/UEFI "UEFI") ankartta UEFI sistemi etkinleştirilmiş ise, [Archiso](/index.php/Archiso "Archiso") Arch Linux'u [systemd-boot](/index.php/Systemd-boot "Systemd-boot")'una göre [önyükleyecektir](/index.php/Boot "Boot"). Bunu doğrulamak için, [efivars](/index.php/UEFI#UEFI_variables "UEFI") dizisini listeleyin:

```
# ls /sys/firmware/efi/efivars

```

Eğer böyle bir dizin yoksa, sistem [BIOS](https://en.wikipedia.org/wiki/BIOS "w:BIOS") ya da CSM modunda önyüklenmiş olabilir. Ayrıntılar için anakartınızın kullanım klavuzuna bakın.

### İnternete bağlan

İso dosyayı [dhcpcd](/index.php/Dhcpcd "Dhcpcd") daemon'unu [kablolu](https://git.archlinux.org/archiso.git/tree/configs/releng/airootfs/etc/udev/rules.d/81-dhcpcd.rules) cihazlar için önyüklemede aktifleştirir. Bağlantı  ile [kontrol](/index.php/Network_configuration#Check_the_connection "Network configuration") edilebilir:

```
# ping archlinux.org

```

Eğer hiçbir bağlantı yoksa, *dhcpcd* servisini `systemctl stop dhcpcd@` komutuyla [durdurup](/index.php/Stop "Stop") `Tab`'a basın. **Kablolu** bağlantılar için [Ağ yapılandırmasına](/index.php/Network_configuration#Device_driver "Network configuration") bakın ya da **Kablosuz** bağlantılar için, [Kablosuz ağ yapılandırması](/index.php/Wireless_network_configuration "Wireless network configuration")'a bakın.

### Sistem saatini güncelle

Sistem saatinin doğruluğunu sağlamak için [timedatectl(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/timedatectl.1) komutunu kullanın:

```
# timedatectl set-ntp true

```

Servis durumunu kontrol etmek için, `timedatectl status` komutunu kullanın.

### Diskleri bölümlendir

Diskler canlı bir sistem tarafından tanındığında, `/dev/sda` gibi *block cihaz*lara atanmış olurlar. Bu cihazları görüntülemek için, [lsblk](/index.php/Lsblk "Lsblk") komutunu ya da *fdisk* komutunu kullanın.

```
# fdisk -l

```

`rom`, `loop` ya da `airoot` ile biten sonuçlar göz ardı edilebilir.

Aşağıdaki *Bölümler* (Sayısal sonek ile gösterilenler) seçilen cihazlar için gereklidir:

*   Bir bölüm root dizini için. `/`.
*   [UEFI](/index.php/UEFI "UEFI") aktif ise, bir [EFI System Partition](/index.php/EFI_System_Partition "EFI System Partition")'ı.

**Not:** [Swap bölümün](/index.php/Swap_space "Swap space")ü ayrı bölümlere veya bir [swap dosyası](/index.php/Swap_file "Swap file")'na kurulabilir.

*Bölüm tabloları*nı değiştirmek için, [fdisk](/index.php/Fdisk "Fdisk") ya da [parted](/index.php/Parted "Parted") komutunu kullanın.

```
# fdisk /dev/sda

```

Daha fazla bilgi için [Bölümleme](/index.php/Partitioning "Partitioning")'ye bakınız.

**Not:** [LVM](/index.php/LVM "LVM"), [disk encryption](/index.php/Disk_encryption "Disk encryption") veya [RAID](/index.php/RAID "RAID") için toplu blok cihazları yapmak istiyorsanız, şimdi yapın.

### Bölümleri biçimlendir

Bölümler oluşturulduktan sonra, her biri uygun bir [dosya sistemi](/index.php/File_system "File system") ile biçimlendirilmelidir. Örneğin, root bölümünü `/dev/*sda1*` üzerine `*ext4*` biçiminde biçimlendirmek için, komudunu:

```
# mkfs.*ext4* /dev/*sda1*

```

çalıştırın.

Daha fazla bilgi için bakınız [Dosya sistemi#Dosya sistemi oluşturmak](/index.php/File_systems#Create_a_file_system "File systems").

### Dosya sistemerini bağla

Dosya sistemini root bölümüne `/mnt` olarak [bağlayın](/index.php/Mount "Mount"), örneğin:

```
# mount /dev/*sda1* /mnt

```

Kalan bölümler için bağlama noktaları oluşturun ve buna göre bağlayın, örneğin:

```
# mkdir /mnt/*boot*
# mount /dev/*sda2* /mnt/*boot*

```

[genfstab](https://git.archlinux.org/arch-install-scripts.git/tree/genfstab.in) daha sonra swap bölümünü ve bağlanmış dosya sistemlerini algılayacaktır.

## Kurulum

### Mirror'ları seç

Yüklenecek paketler `/etc/pacman.d/mirrorlist`'de tanımlanmış olan, [mirror sunucular](/index.php/Mirrors "Mirrors")ından indirilmeli. Canlı bir sistemde, bütün mirror'lar etkinleştirilir ve yükleme iso'su oluşturulduğunda, senkronizasyon durumuna ve hızına göre sıralanır.

Bir mirror listede ne kadar yüksek olursa, bir paket indirilirken daha fazla öncelik verilir. Dosyayı buna göre düzenlemek ve coğrafi olarak en yakın mirror'ları listenin en üstüne taşımak isteyebilirsiniz, ancak diğer kriterler dikkate alınmalıdır.

Bu dosya *pacstrap* tarafından yeni sisteme kopyalanacak, yani hata yapmamaya değer.

### Temel paketleri kurun

[base](https://www.archlinux.org/groups/x86_64/base/) paket grupunu kurmak için, [pacstrap](https://projects.archlinux.org/arch-install-scripts.git/tree/pacstrap.in) yazılımını kullanın:

```
# pacstrap /mnt base

```

Bu grup, canlı sistem kurlumundaki [btrfs-progs](https://www.archlinux.org/packages/?name=btrfs-progs) ya da belirli bir kablosuz yazılımı gibi bütün araçları içermiyor; karşılaştırma için [packages.both](https://projects.archlinux.org/archiso.git/tree/configs/releng/packages.both) sayfasına bakınız bakınız.

Paketleri ve [base-devel](https://www.archlinux.org/groups/x86_64/base-devel/) gibi diğer grubları [kurmak](/index.php/Install "Install") için, [#Chroot](#Chroot) adımından sonra isimleri *pacstrap* ya da [pacman](/index.php/Pacman "Pacman") komutlarına ekleyin.

## Sistemi yapılandır

### Fstab

Bir [fstab](/index.php/Fstab "Fstab") dosyası oluştur ( [UUID](/index.php/UUID "UUID") ya da label'lar olarak tanımlamak içn, `-U` ya da `-L` komutunu kullanın):

```
# genfstab -U /mnt >> /mnt/etc/fstab

```

Sonra, `/mnt/etc/fstab`'ta oluşan dosyayı kontol edin ve hata durumunda düzenleyin.

### Chroot

Yeni sistemdeki [root'u değiştir](/index.php/Change_root "Change root"):

```
# arch-chroot /mnt

```

### Zaman dilimi

[Zaman dilimini](/index.php/Time_zone "Time zone") ayarlayın:

```
# ln -sf /usr/share/zoneinfo/*Bölge*/*Şehir* /etc/localtime

```

`/etc/adjtime` dizinini oluşturmak için, [hwclock(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/hwclock.8) komutunu çalıştırın:

```
# hwclock --systohc

```

Bu komut sistem donanımının [UTC](https://en.wikipedia.org/wiki/UTC "w:UTC") biçiminde olduğunu varsayar. Detaylar için [Zaman#Zaman standartları](/index.php/Time#Time_standard "Time") bölümüne bakınız.

### Locale

Uncomment `en_US.UTF-8 UTF-8` and other needed [localizations](/index.php/Localization "Localization") in `/etc/locale.gen`, and generate them with:

```
# locale-gen

```

Set the `LANG` [variable](/index.php/Variable "Variable") in [locale.conf(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/locale.conf.5) accordingly, for example:

 `/etc/locale.conf`  `LANG=*en_US.UTF-8*` 

If you [set the keyboard layout](#Set_the_keyboard_layout), make the changes persistent in [vconsole.conf(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/vconsole.conf.5):

 `/etc/vconsole.conf`  `KEYMAP=*de-latin1*` 

### Hostname

Create the [hostname(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/hostname.5) file:

 `/etc/hostname` 
```
*myhostname*

```

Consider adding a matching entry to [hosts(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/hosts.5):

 `/etc/hosts` 
```
127.0.0.1	localhost.localdomain	localhost
::1		localhost.localdomain	localhost
**127.0.1.1	*myhostname*.localdomain	*myhostname***

```

See also [Network configuration#Set the hostname](/index.php/Network_configuration#Set_the_hostname "Network configuration").

### Network configuration

The newly installed environment has no network connection activated by default. See [Network configuration#Network management](/index.php/Network_configuration#Network_management "Network configuration").

For [Wireless configuration](/index.php/Wireless_configuration "Wireless configuration"), [install](/index.php/Install "Install") the [iw](https://www.archlinux.org/packages/?name=iw) and [wpa_supplicant](https://www.archlinux.org/packages/?name=wpa_supplicant) packages, as well as needed [firmware packages](/index.php/Wireless#Installing_driver.2Ffirmware "Wireless"). Optionally install [dialog](https://www.archlinux.org/packages/?name=dialog) for usage of *wifi-menu*.

### Initramfs

Creating a new *initramfs* is usually not required, because [mkinitcpio](/index.php/Mkinitcpio "Mkinitcpio") was run on installation of the [linux](https://www.archlinux.org/packages/?name=linux) package with *pacstrap*.

For special configurations, modify the [mkinitcpio.conf(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/mkinitcpio.conf.5) file and recreate the initramfs image:

```
# mkinitcpio -p linux

```

### Root password

Set the root [password](/index.php/Password "Password"):

```
# passwd

```

### Boot loader

A Linux-capable boot loader must be installed in order to boot Arch Linux. See [Category:Boot loaders](/index.php/Category:Boot_loaders "Category:Boot loaders") for available choices.

If you have an Intel CPU, install the [intel-ucode](https://www.archlinux.org/packages/?name=intel-ucode) package in addition, and [enable microcode updates](/index.php/Microcode#Enabling_Intel_microcode_updates "Microcode").

## Reboot

Exit the chroot environment by typing `exit` or pressing `Ctrl+D`.

Optionally manually unmount all the partitions with `umount -R /mnt`: this allows noticing any "busy" partitions, and finding the cause with [fuser(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/fuser.1).

Finally, restart the machine by typing `reboot`: any partitions still mounted will be automatically unmounted by *systemd*. Remember to remove the installation media and then login into the new system with the root account.

## Post-installation

See [General recommendations](/index.php/General_recommendations "General recommendations") for system management directions and post-installation tutorials (like setting up a graphical user interface, sound or a touchpad).

For a list of applications that may be of interest, see [List of applications](/index.php/List_of_applications "List of applications").