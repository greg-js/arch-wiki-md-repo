Bu belge, Arch Linux'u yüklemek için kullanılan canlı sistem kılavuzudur. Kurulumdan önce, [Sıkça sorulan sorulara](/index.php/Frequently_asked_questions_(T%C3%BCrk%C3%A7e) "Frequently asked questions (Türkçe)") bakmanız önerilmektedir. Bu belgede kullanılan düzen için, bakınız [Yardım:Okuma](/index.php/Help:Reading "Help:Reading"). Örneğin, kod örneklerinde (*italik* formatında) yer tutucular bulunabilir ve bunları uygun değerle değiştirmeniz gerekmektedir.

Daha ayrıntılı talimatlar için, bu kılavuzdan karşılık gelen [ArchWiki](/index.php/ArchWiki:About "ArchWiki:About") makalelerine ya da çeşitli programların [man sayfalarına](/index.php/Man_page "Man page") bakınız. İnteraktif yardım için, [IRC kanalını](/index.php/IRC_channel "IRC channel") ve [forumu](https://bbs.archlinux.org/) kullanabilirsiniz.

Arch Linux en az 512 MB RAM'e sahip olan herhangi bir [x86_64](https://en.wikipedia.org/wiki/X86-64 "w:X86-64") uyumlu makinede çalışır. [base](https://www.archlinux.org/groups/x86_64/base/) grubundaki tüm paketleri içeren basit bir kurulum 800 megabyte'tan az bir disk alanı kaplar. Kurulum esnasında paketlerin veri havuzundan indirilmesi gerektiğinden, çalışan bir internet bağlantısı gereklidir.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Kurulum Öncesi](#Kurulum_Öncesi)
    *   [1.1 İmzayı Doğrula](#İmzayı_Doğrula)
    *   [1.2 Canlı ortamı önyükle](#Canlı_ortamı_önyükle)
    *   [1.3 Klavye düzenini ayarla](#Klavye_düzenini_ayarla)
    *   [1.4 Önyükleme modunu doğrula](#Önyükleme_modunu_doğrula)
    *   [1.5 İnternete bağlan](#İnternete_bağlan)
    *   [1.6 Sistem saatini güncelle](#Sistem_saatini_güncelle)
    *   [1.7 Diskleri bölümlendir](#Diskleri_bölümlendir)
    *   [1.8 Bölümleri biçimlendir](#Bölümleri_biçimlendir)
    *   [1.9 Dosya sistemerini bağla](#Dosya_sistemerini_bağla)
*   [2 Kurulum](#Kurulum)
    *   [2.1 Yansıları(Mirrors) seç](#Yansıları(Mirrors)_seç)
    *   [2.2 Temel paketleri kurun](#Temel_paketleri_kurun)
*   [3 Sistemi yapılandır](#Sistemi_yapılandır)
    *   [3.1 Fstab](#Fstab)
    *   [3.2 Chroot](#Chroot)
    *   [3.3 Zaman dilimi](#Zaman_dilimi)
    *   [3.4 Yerelleştirme(locale)](#Yerelleştirme(locale))
    *   [3.5 Sistem adı(Hostname)](#Sistem_adı(Hostname))
    *   [3.6 Ağ yapılandırma](#Ağ_yapılandırma)
    *   [3.7 Initramfs](#Initramfs)
    *   [3.8 Root parolası](#Root_parolası)
    *   [3.9 Önyükleme yükleyicisi(Boot Loader)](#Önyükleme_yükleyicisi(Boot_Loader))
*   [4 Yeniden Başlat](#Yeniden_Başlat)
*   [5 Yükleme sonrası](#Yükleme_sonrası)

## Kurulum Öncesi

Yükleme medyasını [Arch'ı İndirmek ve Kurmak](/index.php/Getting_and_installing_Arch "Getting and installing Arch") sayfasında açıklandığı gibi indiriniz ve aynı zamanda [GnuPG](/index.php/GnuPG "GnuPG") imzasını da edininiz.

### İmzayı Doğrula

İmaj imzasını kullanmadan önce kontrol etmeniz önerilmektedir, özellikle eğer *HTTP yansımasından* indiriyorsanız, ki buradan indirmeler [zararlı imajlar sunabilir](https://www2.cs.arizona.edu/stork/packagemanagersecurity/attacks-on-package-managers.html) eğer saldırıya uğramışsa.

[GnuPG](/index.php/GnuPG "GnuPG") yüklü olan bir sistemde, şu şekilde *PGP* imzasını (*Checksum* ın altında) ISO klasörüne indirip [doğrulayın:](/index.php/GnuPG#Verify_a_signature "GnuPG")

```
 $ gpg --keyserver-options auto-key-retrieve --verify archlinux-version-x86_64.iso.sig

```

Veya alternatif olarak, zaten kurulu olan bir Arch Linux sisteminden şunu çalıştırın:

```
 $ pacman-key -v archlinux-version-x86_64.iso.sig

```

**Note:**

*   Eğer [https://archlinux.org](https://archlinux.org) dışında başka bir siteden indirilmişse, imza manipüle edilmiş olabilir. Bu durumda, imzayı çözme görevinde kullanılan kamu anahtarının (public key) bir başka güvenilir bir anahtar tarafından imzalandığına emin olun. `gpg` komudu kamu anahtarının parmak izini çıktılayacaktır.

*   İmzanın yetkinliğini onaylamanın başka bir yöntemi ise, kamu anahtarının (public key) parmak izinin, ISO dosyasını imzalayan [Arch Linux Geliştiricisi](https://www.archlinux.org/people/developers/) 'nin anahtar parmak iziyle aynı olduğunundan emin olmaktır. Kamu anahtarı işleminin nasıl olduğuyla ilgili ayrıntılı bilgi için [Wikipedia:Public-key cryptography](https://en.wikipedia.org/wiki/Public-key_cryptography "wikipedia:Public-key cryptography") sayfasına göz atın.

### Canlı ortamı önyükle

Canlı ortam bir [USB sürücüden](/index.php/USB_flash_installation_media "USB flash installation media") [optik diskten](/index.php/Optical_disc_drive#Burning "Optical disc drive") veya da [PXE](/index.php/PXE "PXE") kullanarak ağ üzerinden önyüklenebilir. Alternatif kuruluş yolları için gözatınız [Category:Installation process](/index.php/Category:Installation_process "Category:Installation process").

*   Önyüklemeyi Arch kurulum ortamına yönlendirmek için genel kullanılan yöntem [Ön safhada](https://en.wikipedia.org/wiki/Power-on_self_test "wikipedia:Power-on self test") bir tuşa basmaktır. Detaylar için kendi anakartınızın kılavuzuna başvurun.
*   Arch menüsü göründüğünde, *Arch'ı Önyükle* (*Boot Arch*) seçeneğini seçin ve `Enter` tuşuna basarak kurulum ortamına girin.
*   [Önyükleme parametreleri](/index.php/Kernel_parameters#Configuration "Kernel parameters") için gözatınız [README.bootparams](https://projects.archlinux.org/archiso.git/tree/docs/README.bootparams). Ayrıca dahil edilmiş paket listesi için şuraya göz atınız [packages.x86_64](https://git.archlinux.org/archiso.git/tree/configs/releng/packages.x86_64).

İlk sanal konsola root kullanıcısı olarak giriş yapacaksınız ve [Zsh](/index.php/Zsh "Zsh") komut istemiyle karşılaşacaksınız. [systemctl(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/systemctl.1) gibi yaygın komutlar [Tab tuşuyla tamamlanabilir.](https://en.wikipedia.org/wiki/Command-line_completion "w:Command-line completion")

Farklı bir konsola geçmek için, örneğin kurulum esnasında bu rehberi [ELinks](/index.php/ELinks "ELinks") ile görüntülemek için, `Alt+*ok tuşu*` [kısayolunu](/index.php/Keyboard_shortcuts "Keyboard shortcuts") kullanabilirsiniz. Yapılandırma dosyalarını [düzenlemek](/index.php/Textedit "Textedit") için, [nano](/index.php/Nano#Usage "Nano"), [vi](https://en.wikipedia.org/wiki/vi "w:vi") veya [vim](/index.php/Vim#Usage "Vim") kullanılabilir.

### Klavye düzenini ayarla

Varsayılan [konsol klavye düzeni](/index.php/Console_keymap "Console keymap") [US](https://en.wikipedia.org/wiki/File:KB_United_States-NoAltGr.svg "w:File:KB United States-NoAltGr.svg")'tır. Mevcut klavye düzenlerini görüntülemek için, `ls /usr/share/kbd/keymaps/**/*.map.gz` komudunu çalıştırın. Klavye düzenini değiştirmek için, [loadkeys(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/loadkeys.1) komutuna yolunu ve uzantısını atlayarak, eşdeğer dosya adını ekleyin. Örneğin, [Türkçe q](https://en.wikipedia.org/wiki/File:KB_Turkey.svg "w:File:KB Turkey.svg") klavye düzeni için `loadkeys trq` komudunu çalıştırın.

[Konsol fontları](/index.php/Console_fonts "Console fonts") `/usr/share/kbd/consolefonts/` dizisinde yer almaktadır ve aynı şekilde [setfont(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/setfont.8) komudu ile ayarlanabilir.

### Önyükleme modunu doğrula

Bir [UEFI](/index.php/UEFI "UEFI") ankartta UEFI sistemi etkinleştirilmişse, [Archiso](/index.php/Archiso "Archiso"), Arch Linux'u [systemd-boot](/index.php/Systemd-boot "Systemd-boot")'una göre [önyükleyecektir](/index.php/Boot "Boot"). Bunu doğrulamak için, [efivars](/index.php/UEFI#UEFI_variables "UEFI") dizinini listeleyin.

```
# ls /sys/firmware/efi/efivars

```

Eğer böyle bir dizin yoksa, sistem [BIOS](https://en.wikipedia.org/wiki/BIOS "w:BIOS") ya da CSM modunda önyüklenmiş olabilir. Ayrıntılar için anakartınızın kullanım kılavuzuna bakın.

### İnternete bağlan

İso dosyayı [dhcpcd](/index.php/Dhcpcd "Dhcpcd") sunucusunu(daemon) [kablolu](https://git.archlinux.org/archiso.git/tree/configs/releng/airootfs/etc/udev/rules.d/81-dhcpcd.rules) cihazlar için önyüklemede aktifleştirir. Bağlantı şununla [kontrol](/index.php/Network_configuration#Check_the_connection "Network configuration") edilebilir:

```
# ping archlinux.org

```

Eğer hiçbir bağlantı yoksa, *dhcpcd* servisini `systemctl stop dhcpcd@` komutuyla [durdurup](/index.php/Stop "Stop"), `Tab` tuşuna basın. **Kablolu** bağlantılar için [Ağ yapılandırması](/index.php/Network_configuration#Device_driver "Network configuration") ile devam edin ya da **Kablosuz** bağlantılar için [Kablosuz ağ yapılandırması](/index.php/Wireless_network_configuration "Wireless network configuration") ile devam edin.

### Sistem saatini güncelle

Sistem saatinin doğruluğundan emin olmak için [timedatectl(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/timedatectl.1) komutunu kullanın.

```
# timedatectl set-ntp true

```

Servis durumunu kontrol etmek için, `timedatectl status` komutunu kullanın.

### Diskleri bölümlendir

Diskler, canlı bir sistem tarafından tanındığında, `/dev/sda` ya da `/dev/nvme0n1` gibi [blok cihazlara](https://en.wikipedia.org/wiki/Device_file#Naming_conventions "wikipedia:Device file") atanmış olurlar. Bu cihazları görüntülemek için, [lsblk](/index.php/Lsblk "Lsblk") komutunu ya da *fdisk* komutunu kullanın.

```
# fdisk -l

```

`rom`, `loop` ya da `airoot` ile biten sonuçlar göz ardı edilebilir.

Aşağıdaki *Bölümler*, seçilen cihazlar için **gereklidir**:

*   Bir bölüm root dizini için. `/`.
*   [UEFI](/index.php/UEFI "UEFI") aktif ise, bir [EFI Sistem Bölümü](/index.php/EFI_system_partition "EFI system partition")(EFI System Partition).

**Note:** [Swap alanı](/index.php/Swap_space "Swap space"), ayrı bölümlere veya bir [swap dosyasına](/index.php/Swap_file "Swap file") kurulabilir.

*Bölüm tablolarını(partition tables*) değiştirmek için, [fdisk](/index.php/Fdisk "Fdisk") ya da [parted](/index.php/Parted "Parted") komutunu kullanın.

```
# fdisk /dev/sda

```

Daha fazla bilgi için [Bölümleme](/index.php/Partitioning "Partitioning") bölümüne bakınız.

**Note:** [LVM](/index.php/LVM "LVM"), [disk şifreleme](/index.php/Disk_encryption "Disk encryption") veya [RAID](/index.php/RAID "RAID") için istiflenmiş blok cihazları(stacked block devices) yapmak istiyorsanız, şimdi yapın.

### Bölümleri biçimlendir

Bölümler oluşturulduktan sonra, her biri uygun bir [dosya sistemi](/index.php/File_system "File system") ile biçimlendirilmelidir. Örneğin, root bölümünü `/dev/*sda1*` üzerine `*ext4*` ile biçimlendirmek için şunu çalıştırın:

```
# mkfs.*ext4* /dev/*sda1*

```

Daha fazla bilgi için bakınız: [Dosya sistemi#Dosya sistemi oluşturmak](/index.php/File_systems#Create_a_file_system "File systems").

### Dosya sistemerini bağla

Root bölümündeki dosya sistemini `/mnt`'ye [bağlayın](/index.php/Mount "Mount"), örneğin:

```
# mount /dev/*sda1* /mnt

```

Kalan bölümler için bağlama noktaları oluşturun ve uygun şekilde bağlayın, örneğin:

```
# mkdir /mnt/*boot*
# mount /dev/*sda2* /mnt/*boot*

```

[genfstab](https://git.archlinux.org/arch-install-scripts.git/tree/genfstab.in) daha sonra bağlanmış dosya sistemlerini ve swap alanını algılayacaktır.

## Kurulum

### Yansıları(Mirrors) seç

Yüklenecek paketler `/etc/pacman.d/mirrorlist` dizisinde tanımlanmış olan, [yansı sunucularından](/index.php/Mirrors "Mirrors")(mirror servers) indirilmelidir. Canlı bir sistemde, bütün yansılar etkinleştirilir ve yükleme disk görüntüsü(iso) oluşturulduğunda, senkronizasyon durumuna ve hızına göre sıralanır.

Bir yansı listede ne kadar yüksek sırada olursa, bir paket indirilirken daha fazla öncelik verilir. Dosyayı buna göre düzenlemek ve coğrafi olarak en yakın yansıları listenin en üstüne taşımak isteyebilirsiniz, ancak diğer kriterler dikkate alınmalıdır.

Bu dosya *pacstrap* tarafından yeni sisteme kopyalanacak, yani hata yapmamaya değer.

### Temel paketleri kurun

[base](https://www.archlinux.org/groups/x86_64/base/) paket grupunu kurmak için, [pacstrap](https://projects.archlinux.org/arch-install-scripts.git/tree/pacstrap.in) yazılımını kullanın:

```
# pacstrap /mnt base

```

Bu grup, canlı sistem kurlumundaki [btrfs-progs](https://www.archlinux.org/packages/?name=btrfs-progs) ya da belirli bir kablosuz yazılımı gibi bütün araçları içermiyor; karşılaştırma için [packages.both](https://projects.archlinux.org/archiso.git/tree/configs/releng/packages.both) sayfasına bakınız.

Paketleri ve [base-devel](https://www.archlinux.org/groups/x86_64/base-devel/) gibi diğer grubları [kurmak](/index.php/Install "Install") için, [#Chroot](#Chroot) adımından sonra isimleri *pacstrap* ya da [pacman](/index.php/Pacman "Pacman") komutlarına boşluk bırakarak ekleyin.

## Sistemi yapılandır

### Fstab

Bir [fstab](/index.php/Fstab "Fstab") dosyası oluştur ( [UUID](/index.php/UUID "UUID") ya da etiketler(labels) olarak tanımlamak içn, sırasıyla `-U` ya da `-L` komutlarını kullanın):

```
# genfstab -U /mnt >> /mnt/etc/fstab

```

Sonra, `/mnt/etc/fstab` dizininde oluşan dosyayı kontol edin ve hata durumunda düzenleyin.

### Chroot

Yeni sistemin içine [root'u değiştir](/index.php/Change_root "Change root")([Change root](/index.php/Change_root "Change root")):

```
# arch-chroot /mnt

```

### Zaman dilimi

[Zaman dilimini](/index.php/Time_zone "Time zone") ayarla:

```
# ln -sf /usr/share/zoneinfo/*Bölge*/*Şehir* /etc/localtime

```

`/etc/adjtime` dizinini oluşturmak için [hwclock(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/hwclock.8) komutunu çalıştırın:

```
# hwclock --systohc

```

Bu komut sistem donanımının [UTC](https://en.wikipedia.org/wiki/UTC "w:UTC") biçiminde olduğunu varsayar. Detaylar için [Zaman#Zaman standartları](/index.php/System_time#Time_standard "System time") bölümüne bakınız.

### Yerelleştirme(locale)

`/etc/locale.gen` dizinindeki `en_US.UTF-8 UTF-8` satırını ve gerekli [yerelleştirmelerin](/index.php/Localization "Localization") önündeki *#*(Hash tag) işaretini kaldırın, ve şununla oluşturun:

```
# locale-gen

```

`LANG` [değişkenini](/index.php/Variable "Variable") [locale.conf(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/locale.conf.5) dizinine ayarlayın, öreneğin:

 `/etc/locale.conf`  `LANG=*tr_TR.UTF-8*` 

[klavye düzenini ayarladıysanız](#Set_the_keyboard_layout), değişiklikleri [vconsole.conf(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/vconsole.conf.5) dizininde kalıcı hale getirin:

 `/etc/vconsole.conf`  `KEYMAP=*trq*` 

### Sistem adı(Hostname)

[hostname(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/hostname.5) dosyası oluştur:

 `/etc/hostname` 
```
*bilgisayar_adim*

```

Uygun girdileri [hosts(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/hosts.5)'a ekleyin:

 `/etc/hosts` 
```
127.0.0.1	localhost.localdomain	localhost
::1		localhost.localdomain	localhost
**127.0.1.1	*bilgisayar_adim*.localdomain	*bilgisayar_adim***

```

Ayrıca bakınız [Ağ yapılandırması#Sistem adını ayarla](/index.php/Network_configuration#Set_the_hostname "Network configuration").

### Ağ yapılandırma

Yeni kurulan ortamda varsayılan olarak ağ bağlantısı yoktur. Bakınız [Ağ yapılandırması#Ağ yönetimi](/index.php/Network_configuration#Network_management "Network configuration").

[Kablosuz yapılandırma](/index.php/Wireless_configuration "Wireless configuration") için, [iw](https://www.archlinux.org/packages/?name=iw) ve [wpa_supplicant](https://www.archlinux.org/packages/?name=wpa_supplicant) paketlerinin yanı sıra gerekli [ürün yazılımı paketlerini](/index.php/Wireless#Installing_driver/firmware "Wireless") de kurun. İsteğe bağlı olarak *wifi-menu* kullanımı için(kendisi kablosuz ağa bağlanmanızı sağlar) [dialog](https://www.archlinux.org/packages/?name=dialog) paketini de kurun.

### Initramfs

Yeni bir *initramfs* dosyası oluşturmak genellikle gerekli değildir, çünkü [mkinitcpio](/index.php/Mkinitcpio "Mkinitcpio"), [linux](https://www.archlinux.org/packages/?name=linux) paketinin kurulumu sırasında *pacstrap* ile çalıştırılır.

Özel ayarlar için, [mkinitcpio.conf(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/mkinitcpio.conf.5) dosyasını değiştirin ve initramfs görüntüsünü yeniden oluşturun:

```
# mkinitcpio -p linux

```

### Root parolası

Root [parolası](/index.php/Password "Password") ayarla:

```
# passwd

```

### Önyükleme yükleyicisi(Boot Loader)

Arch Linux'u önyüklemek için Linux özellikli bir önyükleyici kurulmalıdır. Mevcut seçenekler için bakınız [Katagöri:Önyükleme yükleyicileri(Boot loaders)](/index.php/Category:Boot_loaders "Category:Boot loaders").

Eğer bir Intel işlemciniz varsa, ek olarak [intel-ucode](https://www.archlinux.org/packages/?name=intel-ucode) paketini yükleyin ve [microcode güncellemelerini etkinleştirin](/index.php/Microcode#Enabling_Intel_microcode_updates "Microcode").

## Yeniden Başlat

`exit` yazarak, ya da `Ctrl+D` tuş kombinasyonlarını kullanarak, chroot ortamından çıkın.

İsteğe bağlı olarak tüm bölümleri `umount -R /mnt` ile manuel olarak ayırın: bu, [fuser(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/fuser.1) ile "meşgul" bölümleri fark etmenizi ve nedenini bulmanızı sağlar.

Son olarak, `reboot` yazarak, makinenizi yeniden başatın: Hâlâ bağlı olan tüm bölümler otomatik olarak *systemd* tarafından ayrılacaktır. Kurulum medyasını çıkarmayın unutmayı ve ardından root hesabıyla yeni sisteme giriş yapın.

## Yükleme sonrası

Sistem yönetimi yönergeleri ve yükleme sonrası dersleri(bir grafiksel kullanıcı arayüzü, ses ya da bir touchpad sürücüleri gibi) için bakınız [Genel öneriler](/index.php/General_recommendations "General recommendations").

İlgi çekici olabilecek uygulamaların listesi için, bakınız [Uygulamalar listesi](/index.php/List_of_applications "List of applications").