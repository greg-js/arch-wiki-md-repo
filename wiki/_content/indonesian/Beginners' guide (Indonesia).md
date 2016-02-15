**Tip:** This guide is also available in multiple pages, rather than one large copy. If you would rather follow it that way, please start **[here](/index.php/Beginners%27_Guide/Preface_(Indonesia) "Beginners' Guide/Preface (Indonesia)")**.

## Contents

*   [1 Pendahuluan](#Pendahuluan)
    *   [1.1 Perkenalan](#Perkenalan)
    *   [1.2 Lisensi](#Lisensi)
    *   [1.3 The Arch Way](#The_Arch_Way)
    *   [1.4 Tentang _Arch wiki_](#Tentang_Arch_wiki)
*   [2 Dapatkan file ISO Archlinux terbaru](#Dapatkan_file_ISO_Archlinux_terbaru)
*   [3 Instalasi sistem dasar](#Instalasi_sistem_dasar)
    *   [3.1 Boot CD Archlinux](#Boot_CD_Archlinux)
    *   [3.2 Mengganti keymap](#Mengganti_keymap)
    *   [3.3 Memulai instalasi](#Memulai_instalasi)
        *   [3.3.1 Pilih sumber instalasi](#Pilih_sumber_instalasi)
        *   [3.3.2 Menyiapkan Hard Drive](#Menyiapkan_Hard_Drive)
            *   [3.3.2.1 Partisi](#Partisi)
            *   [3.3.2.2 Swap Partition](#Swap_Partition)
        *   [3.3.3 Set File system Mountpoints](#Set_File_system_Mountpoints)
            *   [3.3.3.1 Penjelasan singkat mengenai **filesystems** dan _file systems_:](#Penjelasan_singkat_mengenai_filesystems_dan_file_systems:)
    *   [3.4 Memilih Packages](#Memilih_Packages)
    *   [3.5 Instalasi Packages](#Instalasi_Packages)
    *   [3.6 Konfigurasi Sistem](#Konfigurasi_Sistem)
        *   [3.6.1 /etc/rc.conf](#.2Fetc.2Frc.conf)
        *   [3.6.2 Mengenai DAEMONS](#Mengenai_DAEMONS)
        *   [3.6.3 /etc/hosts](#.2Fetc.2Fhosts)
        *   [3.6.4 /etc/fstab, mkinitcpio.conf and modprobe.conf](#.2Fetc.2Ffstab.2C_mkinitcpio.conf_and_modprobe.conf)
        *   [3.6.5 /etc/resolv.conf (for Static IP)](#.2Fetc.2Fresolv.conf_.28for_Static_IP.29)
        *   [3.6.6 /etc/locale.gen](#.2Fetc.2Flocale.gen)
        *   [3.6.7 Root password](#Root_password)
    *   [3.7 Instalasi Kernel](#Instalasi_Kernel)
    *   [3.8 Menginstall dan mengatur bootloader](#Menginstall_dan_mengatur_bootloader)
        *   [3.8.1 Untuk motherboards BIOS](#Untuk_motherboards_BIOS)
            *   [3.8.1.1 Syslinux](#Syslinux)
            *   [3.8.1.2 GRUB](#GRUB)
        *   [3.8.2 Untuk motherboards UEFI](#Untuk_motherboards_UEFI)
            *   [3.8.2.1 Gummiboot](#Gummiboot)
            *   [3.8.2.2 GRUB](#GRUB_2)
*   [4 Konfigurasi lebih lanjut sistem dasar Arch Linux](#Konfigurasi_lebih_lanjut_sistem_dasar_Arch_Linux)
    *   [4.1 Konfigurasi pacman](#Konfigurasi_pacman)
    *   [4.2 Konfigurasi jaringan jika dibutuhkan](#Konfigurasi_jaringan_jika_dibutuhkan)
        *   [4.2.1 Jaringan kabel LAN](#Jaringan_kabel_LAN)
        *   [4.2.2 Jaringan nirkabel (seperti wifi)](#Jaringan_nirkabel_.28seperti_wifi.29)
        *   [4.2.3 Modem Analog](#Modem_Analog)
        *   [4.2.4 ISDN](#ISDN)
        *   [4.2.5 DSL (PPPoE)](#DSL_.28PPPoE.29)
*   [5 Update, Sync dan Upgrade sistem dengan pacman](#Update.2C_Sync_dan_Upgrade_sistem_dengan_pacman)
    *   [5.1 _Perhatikan pesan yang muncul ketika terjadi proses_ upgrading _kernel!_](#Perhatikan_pesan_yang_muncul_ketika_terjadi_proses_upgrading_kernel.21)
    *   [5.2 Mantapnya _Rolling Release_](#Mantapnya_Rolling_Release)
    *   [5.3 Mengenal Pacman lebih dalam](#Mengenal_Pacman_lebih_dalam)
    *   [5.4 Menambahkan pengguna dan atur grup](#Menambahkan_pengguna_dan_atur_grup)
*   [6 Instalasi dan konfigurasi perangkat keras](#Instalasi_dan_konfigurasi_perangkat_keras)
    *   [6.1 Konfigurasi Kartu Audio](#Konfigurasi_Kartu_Audio)
    *   [6.2 Konfigurasi _kecepatan frekuensi CPU_](#Konfigurasi_kecepatan_frekuensi_CPU)
    *   [6.3 _Tweak_ tambahan untuk laptop](#Tweak_tambahan_untuk_laptop)
*   [7 Instalasi dan Konfigurasi X](#Instalasi_dan_Konfigurasi_X)
*   [8 Membuat /etc/X11/xorg.conf](#Membuat_.2Fetc.2FX11.2Fxorg.conf)
    *   [8.1 Apa itu /etc/X11/xorg.conf?](#Apa_itu_.2Fetc.2FX11.2Fxorg.conf.3F)
    *   [8.2 Simple baseline X test](#Simple_baseline_X_test)
    *   [8.3 Mengatur _Layout Keyboard_](#Mengatur_Layout_Keyboard)
    *   [8.4 Mengatur _scroll wheel_ Tetikus/_Mouse_](#Mengatur_scroll_wheel_Tetikus.2FMouse)
    *   [8.5 evdev](#evdev)
    *   [8.6 Memakai _Driver_ Grafis Proprietari (nVIDIA, ATI)](#Memakai_Driver_Grafis_Proprietari_.28nVIDIA.2C_ATI.29)
        *   [8.6.1 Kartu Grafis nVIDIA](#Kartu_Grafis_nVIDIA)
        *   [8.6.2 Kartu Grafis ATI](#Kartu_Grafis_ATI)
*   [9 Menginstal dan mengonfigurasikan sebuah Desktop Environment](#Menginstal_dan_mengonfigurasikan_sebuah_Desktop_Environment)
    *   [9.1 Instalasi Huruf/Font](#Instalasi_Huruf.2FFont)
    *   [9.2 GNOME](#GNOME)
        *   [9.2.1 Tentang GNOME](#Tentang_GNOME)
        *   [9.2.2 Instalasi](#Instalasi)
            *   [9.2.2.1 DAEMON yang berguna untuk GNOME](#DAEMON_yang_berguna_untuk_GNOME)
        *   [9.2.3 ~/.xinitrc](#.7E.2F.xinitrc)
        *   [9.2.4 Eye Candy](#Eye_Candy)
    *   [9.3 KDE](#KDE)
        *   [9.3.1 Tentang KDE](#Tentang_KDE)
        *   [9.3.2 Installation](#Installation)
        *   [9.3.3 Useful KDE DAEMONS](#Useful_KDE_DAEMONS)
            *   [9.3.3.1 ~/.xinitrc](#.7E.2F.xinitrc_2)
    *   [9.4 Xfce](#Xfce)
        *   [9.4.1 Tentang Xfce](#Tentang_Xfce)
        *   [9.4.2 Instalasi](#Instalasi_2)
    *   [9.5 *box](#.2Abox)
        *   [9.5.1 Fluxbox](#Fluxbox)
        *   [9.5.2 Openbox](#Openbox)
    *   [9.6 fvwm2](#fvwm2)
*   [10 HAL](#HAL)
*   [11 Aplikasi-aplikasi yang Bermanfaat](#Aplikasi-aplikasi_yang_Bermanfaat)
    *   [11.1 Internet](#Internet)
        *   [11.1.1 Firefox](#Firefox)
    *   [11.2 Perkantoran (_Office_)](#Perkantoran_.28Office.29)
*   [12 Multimedia](#Multimedia)
    *   [12.1 Pemutar Video](#Pemutar_Video)
        *   [12.1.1 VLC](#VLC)
        *   [12.1.2 Mplayer](#Mplayer)
        *   [12.1.3 GNOME](#GNOME_2)
            *   [12.1.3.1 Totem](#Totem)
        *   [12.1.4 KDE](#KDE_2)
            *   [12.1.4.1 Kaffeine](#Kaffeine)
    *   [12.2 Pemutar Audio](#Pemutar_Audio)
        *   [12.2.1 GNOME/Xfce](#GNOME.2FXfce)
            *   [12.2.1.1 Exaile](#Exaile)
            *   [12.2.1.2 Rhythmbox](#Rhythmbox)
        *   [12.2.2 KDE](#KDE_3)
            *   [12.2.2.1 Amarok](#Amarok)
        *   [12.2.3 Console](#Console)
        *   [12.2.4 Yang berbasis X lainnya](#Yang_berbasis_X_lainnya)
    *   [12.3 Codec dan tipe konten multimedia](#Codec_dan_tipe_konten_multimedia)
        *   [12.3.1 DVD](#DVD)
        *   [12.3.2 Flash](#Flash)
        *   [12.3.3 Quicktime](#Quicktime)
        *   [12.3.4 Realplayer](#Realplayer)
    *   [12.4 Membakar (_Burning_) CD dan DVD](#Membakar_.28Burning.29_CD_dan_DVD)
        *   [12.4.1 GNOME](#GNOME_3)
            *   [12.4.1.1 Brasero](#Brasero)
        *   [12.4.2 KDE](#KDE_4)
            *   [12.4.2.1 K3b](#K3b)
    *   [12.5 TV-Cards](#TV-Cards)
    *   [12.6 Kamera Digital](#Kamera_Digital)
    *   [12.7 USB Memory Sticks / Hard Disks](#USB_Memory_Sticks_.2F_Hard_Disks)
*   [13 Memelihara sistem](#Memelihara_sistem)
    *   [13.1 Pacman](#Pacman)
        *   [13.1.1 Perintah yang bermanfaat](#Perintah_yang_bermanfaat)
*   [14 Informasi Lebih Lanjut](#Informasi_Lebih_Lanjut)

## Pendahuluan

##### Perkenalan

Selamat datang...

Disini,Anda akan menemukan petunjuk tentang cara menginstall dan mengkonfigurasi Archlinux,distro GNU/Linux sederhana,elegan dan minimalis untuk pengguna kompeten.Panduan ini diperuntukkan bagi pengguna baru Archlinux,dan juga dapat digunakan sebagai sumber referensi bagi semua orang.

**Kelebihan Archlinux yang harus Anda ketahui :**

*   Archlinux merupakan distro yang simpel,elegan,minimalis dan selalu _up to date_.Baca juga tentang [Prinsip Archlinux](/index.php/The_Arch_Way "The Arch Way").
*   Archlinux serta paket/aplikasinya mendukung arsitektur mesin i686 dan x86_64.
*   Skrip _Init_ [bergaya BSD](/index.php/Arch_boot_process "Arch boot process"), menyajikan konfigurasi berkas yang terpusat.
*   _mkinitcpio_: sebuah kreator _initramfs_ yang sederhana dan dinamis.
*   [Pacman](/index.php/Pacman "Pacman") _Manajemen Paket_ yang sangat ringan dan cepat serta hemat memori.
*   _The [Arch Build System](/index.php/Arch_Build_System "Arch Build System")_: sebuah sistem pembentukan paket menyerupai sistem _ports_, menyediakan _framework_ sederhana untuk membuat paket Arch yang bisa di-_install_ dari kode sumber.
*   _The [Arch User Repository](/index.php/Arch_User_Repository "Arch User Repository")_ (AUR): menawarkan lebih dari ribuan kontribusi _build scripts_ dari penggunanya dan memberikan kesempatan bagi Anda untuk ikut berkontribusi.

##### Lisensi

Arch Linux, pacman, dokumentasi, dan _scripts_ adalah hak cipta ©2002-2007 oleh Judd Vinet, ©2007-2011 oleh Aaron Griffin dan dilisensikan di bawah [Lisensi Umum GNU Versi 2](http://www.gnu.org/licenses/old-licenses/gpl-2.0.html).

### The Arch Way

_**Prinsip desain di balik Arch ditujukan untuk menjaganya agar tetap [sederhana](/index.php/The_Arch_Way "The Arch Way").**_

'Sederhana', dalam konteks ini, berarti 'tanpa tambahan yang tidak perlu, modifikasi, atau komplikasi'. Singkatnya, sebuah pendekatan yang elegan, minimalis.

**Beberapa pemikiran yang perlu diingat ketika Anda mempertimbangkan kesederhanaan:**

*   _" 'sederhana' didefinisikan dari sudut pandang teknis, bukan sudut pandang kegunaan Lebih baik secara teknis elegan dengan kurva belajar yang lebih tinggi, daripada menjadi mudah digunakan dan teknis [rendah]." -Aaron Griffin_

*   _Entia sunt non multiplicanda praeter necessitatem_ atau "Entitas tidak boleh dikalikan tidak perlu." -s Occam 'pisau cukur. _Pisau cukur_ merujuk pada tindakan memangkas semua hal yang tidak perlu untuk sampai pada metode, penjeleasan, metode ataupun teori yang paling sederhana.

*   _" Bagian yang luar biasa [metode saya] terletak pada kesederhanaannya .. Budidaya yang tinggi selalu berjalan untuk kesederhanaan."_ - Bruce Lee

### Tentang _Arch wiki_

Arch Wiki adalah sumber yang bagus dan dapat menjadi referensi untuk permasalahan yang Anda temui [pertama](/index.php/Main_page "Main page"). Ruang IRC (di irc.freenode.net #archlinux), dan [forum](https://bbs.archlinux.org) juga tersedia apabila Anda tidak menemui jawaban untuk permasalahan Anda. Juga selalu biasakan untuk membaca `Man / Petunjuk Penggunaan` untuk semua perintah yang terdengar asing bagi Anda.Ini biasanya dapat dipanggil dengan cara `man _command_`.

**Note:** Mengikuti panduan ini dengan sangat detil adalah suatu keharusan agar berhasil menginstall ArchLinux dengan benar, jadi _harap_ perhatikan dengan seksama. Di rekomendasikan untuk membaca tiap bagian sampai selesai <u>sebelum</u> melaksanakan tugas-tugas yang ada.

Panduan ini terbagi atas 4 bagian utama :

*   [Bagian I: Mempersiapkan Instalasi](/index.php/Beginners%27_guide/Preparation#Prepare_the_Installation "Beginners' guide/Preparation")
*   [Bagian II: Instalasi Sistem Dasar](/index.php/Beginners%27_guide/Installation#Install_the_Base_System "Beginners' guide/Installation")
*   [Bagian III: Post instalasi](/index.php/Beginners%27_guide/Post-installation#Post_Install "Beginners' guide/Post-installation")
*   [Bagian IV: Extra](/index.php/Beginners%27_guide/Post-installation#Extras "Beginners' guide/Post-installation")

## Dapatkan file ISO Archlinux terbaru

Silahkan unduh file ISO terbaru Archlinux di [www.archlinux.org/download/](https://www.archlinux.org/download/).

Sangat direkomendasikan untuk memilih **base-CD**,dengan alasan :

1.  Mempunyai ukuran file yang lebih kecil sehingga bisa menghemat kuota dan waktu.
2.  Paket di versi full mungkin nantinya akan ada yang konflik ketika melakukan update.
3.  Base system lebih mudah dan cepat untuk diperbarui dan
4.  Petunjuk ini lebih ditujukan untuk installasi dari base-CD.

## Instalasi sistem dasar

Selain petunjuk ini, kamu juga dapat menggunakan petunjuk resmi ini [Official Arch Linux Install Guide](/index.php/Official_Arch_Linux_Install_Guide "Official Arch Linux Install Guide") atau [versi yang dapat di print](https://www.archlinux.org/static/docs/arch-install-guide.html) juga tersedia.

### Boot CD Archlinux

Masukkan CD dan boot dari CD-ROM, kamu mungkin perlu mengganti urutan boot pada bios komputer kamu (biasanya dengan menekan F11 atau F12).

Beberapa pilihan pada saat booting Arch Linux CD yang dapat kamu gunakan:

*   ide-legacy jika IDE drive kamu bermasalah.
*   noapic acpi=off pci=routeirq nosmp jika sistem kamu hangs ketika boot.
*   memtest86+ if jika kamu ingin memeriksa memorimu.

Pilih "Arch Linux Installation / Rescue System". Jika kamu ingin merubah opsi boot tekan e.

### Mengganti keymap

Tekan enter di welcome screen. Jika keyboard kamu non-US tekan

```
km

```

pada prompt dan pilih keymap yang sesuai.

_Contoh_(untuk keymap norwegia) :

Pada console keymap screen pilih

```
no-latin1

```

Pada console font screen pilih

```
lat0-16

```

Memilih "default8x16.psfu.gz" sebagai font console adalah pilihan aman.

### Memulai instalasi

Pada console ketikkan

```
/arch/setup 

```

lalu tekan enter untuk memulai instalasi.

#### Pilih sumber instalasi

Pilih CD jika kamu menggunakan base atau full (current) ISO, atau pilih FTP jika kamu menggunakan FTP ISO.

#### Menyiapkan Hard Drive

Pada menu pilihan,pilih **Prepare Hard Drive**. Hati-hati, jika memilih **Auto-prepare**, **seluruh isi hard drive mu akan dihapus**. Pada contoh ini,kita memilih opsi mengatur partisi hard drive secara manual. Pilih **2\. Partition Hard Drives**, pilih hard drive yang kamu inginkan (/dev/sdx), dan buatlah beberapa partisi.

##### Partisi

Sebuah partisi adalah bagian dari hard disk yang tampil sebagai ruang yang terpisah, dan dapat ditambahkan ke dalam sistem Arch Linuxmu. Partisi hard disk terbagi ke dalam "Primary", "Extended", dan "Logical". Sebuah partisi "primary" dapat diboot. Jumlah maksimalnya 4\. Jadi, jika kamu menggunakan sebuah PC dengan drive SATA, partisi "primary" pertama dikenal sebagai sda1\. Partisi "primary" kedua dreferensikan sebagai sda2, kemudian sda3 dan sda4\. Jika terdapat lebih dari 4 partisi "primary", maka yang terpaksa digunakan untuk partisi ini adalah "extended", yang dimana partisi ini menampung partisi "logical".

Partisi _extended_ bersifat sebagai "penampung" untuk partisi logical. Partisi logical harus berada dalam partisi extended. Contohnya, ketika mempartisi, kita dapat melihat penomoran partisi dengan memberi nomor sda1-3 pada partisi primary, diikuti dengan nomor sda4 pada partisi extended, kemudian membuat partisi logical dengan penomoran sda5,sda6 dst.

Banyak user memiliki pendapat yang berbeda-beda mengenai bagaimana cara terbaik untuk mempartisi hard disk. Yang perlu diketahui adalah bahwa syarat minimal adalah adanya satu partisi primary yang dijadikan sebagai root [Filesystem](https://en.wikipedia.org/wiki/File_system "wikipedia:File system") ( / ) dan satu partisi lagi sebagai swap. Beberapa pilihan lain untuk dipasang pada partisi yang berbeda adalah /boot (yang secara garis besar menampung kernel) dan /home (menampung data user). Adalah ide yang bagus untuk memisahkan root (/) dan /home pada partisi yang berbeda. Ini memungkinkan untuk melakukan instlasi kembali sistem Arch Linux mu, atau distro lainnya, sementara itu data-data dan konfigurasi _desktop environment_ tetap terjaga.

Pada contoh ini, kita akan meletakkan root (/), /home dan swap pada partisi yang berbeda.

##### Swap Partition

Sebuah partisi swap adalah tempat dalam hard disk yang dapat menampung _virtual_ RAM_. Partisi swap digunakan ketika jumlah RAM yang dibutuhkan melebihi daya_ tampung dari memori RAM yang dimiliki mesin anda.

Mengenai ukuran dari partisi swap ini, terdapat beberapa pendapat. Jika kapasitas memory RAM anda besar (lebih besar dari 1024 MB), anda bisa saja tidak menggunakan partisi swap sama sekali. Namun ada pula yang mengusulkan menyediakan ruang bagi partisi swap sebesar 2 kali kapasitas memory RAM mesin anda. Sementara itu ada yang mengusulkan ruang yang dialokasikan tidak lebih dari 1024 MB.

Mari kita mulai dari membuat sebuah **primary partition**. Partisi ini akan menjadi tempat bagi **root**. Pilih New -> Primary, kemudian tentukan ukuran yang anda inginkan (ukuran yang umum adalah 4 hingga 8 GB). Letakkan partisi ini pada bagian pertama disk anda. Pilih partisi baru ini dan jadikan partisi ini "Bootable".

Tambahkan **partition for your home directory**. Untuk partisi ini, pilihlah partisi primary lainnya dan tentukan ukurannya sesuai dengan kebutuhan anda. Ukuran ini tergantung dengan apa yang akan anda simpan dalam partisi tersebut.

Terakhir, ciptakan partisi ketiga yaitu **partition for swap**. Pilihlah ukuran antara 512 MB dan 1 GB (sebagai contoh dalam tutorial ini), dan ganti tipenya menjadi 82 (Linux swap / Solaris).

Inilah hasil dari pengaturan partisi (ukuran akan tergantung pilihan anda).

```
Name    Flags  Part Type   FS Type         [Label]         Size (MB)
-------------------------------------------------------------------------
sda1    Boot   Primary     Linux                           (4096 - 8192)
sda2           Primary     Linux                           (> 100)
sda3           Primary     Linux swap / Solaris            (512 - 1024)

```

Pilih write dan ketikkan yes. Hati-hati, langkah ini akan menghapus data dari hard disk anda jika sebelumnya anda menindih atau menghapus partisi yang ada. Pilih Quit untuk meninggalkan bagian konfigurasi partisi.

Pilih Done untuk keluar dari menu ini dan kita lanjutkan pada "Set Filesystem Mountpoints".

#### Set File system Mountpoints

##### Penjelasan singkat mengenai **filesystems** dan _file systems_:

Secara teknis, sebuah **filesystem** adalah format data untuk _data throughput_, sementara itu _file system_ (dengan spasi), adalah istilah yang menunjukkan tata letak dari seluruh file dan direktori pada sebuah sistem. Jadi, ketika ada pertanyaan apakah anda mau membuat sebuah **filesystem**, ini berarti anda ditanya untuk **memformat** sebuah partisi. Sedangkan jika anda ditanya mengenai lokasi _mounting_ sebuah partisi, anda diminta untuk menentukan di lokasi mana pada _file system_ partisi ini akan diletakkan. Mari kita mulai.

Pertama, anda akan ditanya mengenai partisi swap. Pilih lokasi yang sesuai (dalam contoh ini adalah sda3). Anda akan ditanya apakah anda ingin menciptakan sebuah _filesystem_, pilih _yes_. Kemudian, tentukan lokasi _mounting_ direktori / (root) (dalam contoh ini adalah sda1). Anda akan ditanya tipe _filesystem_ yang anda inginkan.

Dalam menentukan tipe _filesystem_, terdapat pula perbedaan pendapat. Masing-masing ada kelebihan dan kekurangannya. Di bawah ini adalah sebuah ringkasan sederhana.

1\. **ext2** - Lebih tua, _filesystem_ yang dapat dihandalkan. Cepat dan sangat stabil, namun tidak memiliki kemampuan _journaling_.

2\. **ext3** - Sama seperti _ext2_, namun dengan tambahan kemampuan _journaling_. Agak lambat bila dibandingkan dengan _ext2_. Sangat stabil, lebih banyak digunakan dan dikembangkan.

3\. **ReiserFS** - _Hans Reiser's high-performance journaling FS_ menggunakan metode yang menarik terkait _data throughput_. _ReiserFS_ sangat cepat, terutama ketika menangani file-file kecil.

4\. **JFS** - _IBM's Journaling FS_. JFS cukup dikenal, cepat dan stabil.

5\. **XFS** - adalah _journaling filesystem_ yang cepat dan lebih cocok untuk file dengan ukuran yang besar(lebih besar dari 1 GB). Lebih lambat untuk file berukuran kecil. Cukup stabil.

Perbedaan utamanya dapat dilihat di [wikipedia:Journaling_file_system](https://en.wikipedia.org/wiki/Journaling_file_system "wikipedia:Journaling file system").

Semua _filesystem_ menggunakan journaling, kecuali ext2\. ext3 kompatibel dengan ext2\. Pilihan yang aman untuk sebuah partisi root adalah ext3.

Kemudian buatlah partisi ini denga memilih yes. Anda akan ditanya apakah akan membuat partisi baru.

Pada contoh ini, hanya ada partisi sda2 yang tersisa. Pilih sebuah tipe _filesystem_, dan _mount_ sebagai /home. Kemudian ciptakan partisi ini dan pilih Done. Kembalilah ke menu utama.

### Memilih Packages

Sekarang kita akan memilih packages untuk diinstalasi pada sistem. Pilih CD sebagai sumber. Jika anda memiliki lebih dari satu drive CD, pilih yang memuat CD Archlinux.

Karena tutorial ini ditujukan sebagai instalasi dasar, pilihlah katagori **base**. Adalah pilihan yang aman untuk mencentang semua package dalam **base**.

### Instalasi Packages

Ini adalah tahapan termudah, karena semua proses berjalan secara otomatis. Buatlah secangkir kopi dan tunggu sampai proses instalasi selesai (tekan tombol "Continue" jika diperlukan). Minumnya jangan kelamaan, karena instalasi sistem dasar Arch Linux hanya berberapa menit saja :P .

### Konfigurasi Sistem

Anda akan ditanyakan apakah ingin agar _hwdetect_ mengumpulkan informasi untuk konfigurasi anda. Opsi ini sangat direkomendasikan untuk dipilih. Sekarang anda akan ditanyakan apakah anda butuh support untuk booting dari perangkat USB, perangkat FireWire, perangkat PCMCIA, jaringan NFS, software RAID arrays, LVM2 volumes, and encrypted volumes. Pilih Yes jika anda mebutuhkannya; dalam contoh ini, tidak ada yang diperlukan. Sekarang anda akan ditanya penyunting teks mana yang ingin anda pilih, [nano](https://en.wikipedia.org/wiki/Nano_(text_editor) "wikipedia:Nano (text editor)") atau [vi/vim](https://en.wikipedia.org/wiki/Vim_(text_editor) "wikipedia:Vim (text editor)"). Sekarang Anda akan menemukan menu yang penting untuk mengkonfigurasi sistem anda. Kami hanya melakukan perubahan kecil disini. Jika anda ingin tahu opsi apa saja yang terdapat di rc.conf, tekanlah Alt+F2 untuk masuk shell, dan kembali ke installer dengan Alt+F1\.

##### /etc/rc.conf

*   Ubah LOCALE anda jika diperlukan (Misalnya: "de_DE.utf8") (Lokal ini harus

sesuai pada /etc/locale.gen. **Lihat di bawah ini**.)

*   Ubah zona waktu anda jika diperlukan pada TIMEZONE (e.g. "Asia/Jakarta")
*   Ubah KEYMAP anda jika diperlukan (e.g. "de-latin1-nodeadkeys")

*   Tambahkan bagian MODULES jika anda modul penting yang tidak otomatis

diaktifkan oleh hwdetect

*   Ubah HOSTNAME anda
*   Ubah pengaturan jaringan anda:
    *   Jangan ubah lo line
    *   Atur _IP address_, _netmask_ dan _broadcast address_ jika anda menggunakan _static IP_.
    *   Tetapkan eth0="dhcp" jika anda menggunakan metode DHCP dalam menentukan alamat IP anda.
    *   Jika anda memiliki _static IP_, tetapkan _gateway address_ sesuai dengan router anda dan hapuskan ! dari baris ROUTES.

##### Mengenai DAEMONS

Anda tak perlu mengubah baris [daemons](/index.php/Daemons "Daemons") saat ini, tapi penting untuk menjelaskan ini, karena kita membutuhkannya di bagian lain panduan ini. mirip dengan service pada Windows, daemon adalah program yang berjalan background untuk melayani program. Salah satu contoh adalah webserver yang menunggu request untuk mengirimkan halaman atau server SSH yang menunggu orang untuk masuk. Selain daemon yang berupa aplikasi yang terlihat nyata layanannya, ada berberapa daemon yang bekerja tanpa terlihat. Contohnya ada daemon yang menulis pesan pada file log (misalnya: syslog, metalog), ada daemon yang menurunkan frekuensi CPU anda jika tak ada yang perlu dilakukan, dan daemon yang menyajikan anda login grafis (misalnya: gdm, kdm). Semua program ini dapat ditambahkan ke baris daemons dan akan dijalankan saat sistem mulai. Daemon-daemon penting akan disajikan dalam panduan ini.

Gunakan Ctrl+X untuk keluar dari editor.

##### /etc/hosts

Tambahkan _hostname_ yang Anda tambahkan pada rc.conf sebelumnya:

```
127.0.0.1   localhost.localdomain   localhost _yourhostname_

```

Format ini, **termasuk entri 'localhost'** , diperlukan untuk kompatibilitas. Biasanya menambahkan _hostname_ di akhir baris ini terbilang cukup. Namun, sebagian pengguna merekomendasikan:

```
127.0.0.1  _yourhostname_.domain.org localhost.localdomain   localhost 

```

_yourhostname_ Jika anda menggunakan IP statik, tambahkan baris lain menggunakan sintaks: <ip-statik> hostname.domainname.org hostname, e.g.:

```
192.168.1.100 yourhostname.domain.org  yourhostname

```

##### /etc/fstab, mkinitcpio.conf and modprobe.conf

Kita tidak perlu mengubah mkinitcpio.conf, or modprobe.conf saat ini. mkinitcpio mengatur ramdisk (misalnya: booting dari RAID, partisi terenkripsi), dan modprobe dapat digunakan untuk mengatur berberapa konfigurasi khusus pada modul-modul).

Jika anda berencana menggunakan HAL daemon untuk mengautomatisasi pengaitan partisi-partisi, perangkat optik, perangkat USB, dll, Anda mungkin berkeinginan untuk mengubah /etc/fstab dengan menghilangkan tanda pagar (#) pada entri untuk cdrom, floppy, and dvd.

##### /etc/resolv.conf (for Static IP)

If you use a static IP, set your DNS servers in /etc/[resolv.conf](/index.php/Resolv.conf "Resolv.conf") (nameserver <ip-address>). You may have as many as you wish.

Jika anda menggunakan router, Anda mungkin ingin mengarahkan server DNS ke router anda (dimana juga merupakan gateway anda di /etc/rc.conf), misalnya:

```
nameserver 192.168.1.1

```

Selanjutnya, tambahkan server-server yang anda inginkan satu-per-satu. Misalnya:

```
nameserver 4.2.2.1
nameserver 4.2.2.2

```

##### /etc/locale.gen

Pilih locale sesuai yang anda butuhkan (dengan menghapus # dari baris locale yang anda pilih) contoh:

```
en_US ISO-8859-1
en_US.UTF-8	

```

(**Locale yang anda pilih harus sama dengan yang anda tentukan pada file /etc/rc.conf**)

##### Root password

Tetapkan password bagi user root. Kemudian kembali ke menu utama dan lanjutkan dengan proses instalasi kernel.

### Instalasi Kernel

Tidak banyak pilihan disini. Pilih saja v2.6 dan lanjutkan.

### Menginstall dan mengatur bootloader

#### Untuk motherboards BIOS

Untuk sistem BIOS,tersedia beberapa pilihan bootloader,cek di [Boot loaders](/index.php/Boot_loaders "Boot loaders") untuk lebih jelasnya.Berikut adalah 2 contoh umum bootloader yang sering digunakan oleh pengguna BIOS :

*   [Syslinux](/index.php/Syslinux "Syslinux") is (currently) limited to loading only files from the partition where it was installed. Its configuration file is considered to be easier to understand. An example configuration can be found in the [syslinux](/index.php/Syslinux#Examples "Syslinux") article.
*   [GRUB](/index.php/GRUB "GRUB") is more feature-rich and supports more complex scenarios. Its configuration file(s) is more similar to 'sh' scripting language, which may be difficult for beginners to manually write. It is recommended that they automatically generate one.

##### Syslinux

If you opted for a GUID partition table (GPT) for your hard drive earlier, you need to install the [gptfdisk](https://www.archlinux.org/packages/?name=gptfdisk) package now for the installation of _syslinux_ to work:

```
# pacman -S gptfdisk

```

Install the [syslinux](https://www.archlinux.org/packages/?name=syslinux) package and then use the `syslinux-install_update` script to automatically _install_ the bootloader (`-i`), mark the partition _active_ by setting the boot flag (`-a`), and install the _MBR_ boot code (`-m`):

```
# pacman -S syslinux
# syslinux-install_update -iam

```

After installing Syslinux, configure `syslinux.cfg` to point to the right root partition. This step is vital. If it points to the wrong partition, Arch Linux will not boot. Change `/dev/sda3` to reflect your root partition (if you partitioned your drive as in [the example](#Prepare_the_storage_drive), your root partition is `/dev/sda1`).

 `# nano /boot/syslinux/syslinux.cfg` 

```
...
LABEL arch
        ...
        APPEND root=**/dev/sda3** rw
        ...
```

If adding [UUID](/index.php/UUID "UUID") rather than partition number the syntax is `APPEND root=UUID=_partition_uuid_ rw`.

Do the same for the fallback entry.

For more information on configuring and using Syslinux, see [Syslinux](/index.php/Syslinux "Syslinux").

##### GRUB

Instal paket [grub](https://www.archlinux.org/packages/?name=grub) dan jalankan perintah `grub-install` untuk menginstall bootloader :

```
# pacman -S grub
# grub-install --target=i386-pc --recheck **/dev/sda**

```

**Catatan:**

*   Change `/dev/sda` to reflect the drive you installed Arch on. Do not append a partition number (do not use `sda_X_`).
*   For GPT-partitioned drives on BIOS motherboards, you also need a "BIOS Boot Partition". See [GPT-specific instructions](/index.php/GRUB#GUID_Partition_Table_.28GPT.29_specific_instructions "GRUB") in the GRUB page.
*   A sample `/boot/grub/grub.cfg` gets installed as part of the [grub](https://www.archlinux.org/packages/?name=grub) package, and subsequent `grub-*` commands may not over-write it. Ensure that your intended changes are in `grub.cfg`, rather than in `grub.cfg.new` or some such file.

Selanjutnya,menggunakan konfigurasi difile `grub.cfg` yang terbuat secara manual adalah hal yang aman,direkomendasikan untuk pengguna pemula membuat file serupa secara otomatis :

**Tip:** Jika kamu ingin menambahkan daftar sistem operasi lainnya didalam bootloader (dual boot),instal paket [os-prober](https://www.archlinux.org/packages/?name=os-prober) sebelum menjalankan perintah dibawah ini.

```
# grub-mkconfig -o /boot/grub/grub.cfg

```

**Note:** It is possible that multiple redundant menu entries will be generated. See [GRUB#Redundant_menu_entries](/index.php/GRUB#Redundant_menu_entries "GRUB").

Silahkan lihat halaman [GRUB](/index.php/GRUB "GRUB") untuk informasi lebih mendalam.

#### Untuk motherboards UEFI

Untuk sistem UEFI,tersedia beberapa pilihan bootloader,cek di [Boot loaders](/index.php/Boot_loaders "Boot loaders") untuk lebih jelasnya.Berikut adalah 2 contoh umum bootloader yang sering digunakan oleh pengguna UEFI :

*   [gummiboot](/index.php/Gummiboot "Gummiboot") is a minimal UEFI Boot Manager which provides a menu for [EFISTUB](/index.php/EFISTUB "EFISTUB") kernels and other UEFI applications.
*   [GRUB](/index.php/GRUB "GRUB") is a more complete bootloader, useful if you run into problems with Gummiboot.

Setelah menentukan pilihan,pertama install [dosfstools](https://www.archlinux.org/packages/?name=dosfstools) package, sehingga sistem partisi EFI dapat dimanipulasi :

```
# pacman -S dosfstools

```

**Note:** For UEFI boot, the drive needs to be GPT-partitioned and an [EFI System Partition](/index.php/Unified_Extensible_Firmware_Interface#EFI_System_Partition "Unified Extensible Firmware Interface") (512 MiB or larger, gdisk type `EF00`, formatted with FAT32) must be present. In the following examples, this partition is assumed to be mounted at `/boot`. If you have followed this guide from the beginning, you have already done all of these.

##### Gummiboot

Instal paket [gummiboot](https://www.archlinux.org/packages/?name=gummiboot) dan jalankan `gummiboot install` untuk menginstall bootloader ke sistem EFI :

```
# pacman -S gummiboot
# gummiboot install

```

**Warning:** Gummibot dan Kernel Linux tidak akan terupdate otomatis jika sistem partisi EFI kamu tidak di mount ke `/boot`.

Kamu harus menambahkan konfigurasi secara manual untuk memasukkan Archlinux kedalam gummiboot manager.Buat file `/boot/loader/entries/arch.conf` dan tambahkan teks dibawah ini,ganti `/dev/sdaX` dengan partisi **root** kamu.Contoh : `/dev/sda2` :

 `# nano /boot/loader/entries/arch.conf` 

```
title          Arch Linux
linux          /vmlinuz-linux
initrd         /initramfs-linux.img
options        root=**/dev/sdaX** rw
```

Silahkan cek halaman wiki [gummiboot](/index.php/Gummiboot "Gummiboot") untuk info lebih lanjut mengenai cara konfigurasinya.

##### GRUB

Instal paket [grub](https://www.archlinux.org/packages/?name=grub) dan [efibootmgr](https://www.archlinux.org/packages/?name=efibootmgr) kemudian jalankan perintah `grub-install` untuk menginstall bootloader :

```
# pacman -S grub efibootmgr
# grub-install --target=x86_64-efi --efi-directory=/boot --bootloader-id=arch_grub --recheck

```

Selanjutnya,menggunakan konfigurasi difile `grub.cfg` yang terbuat secara manual adalah hal yang aman,direkomendasikan untuk pengguna pemula membuat file serupa secara otomatis :

**Tip:** Jika kamu ingin menambahkan daftar sistem operasi lainnya didalam bootloader (dual boot),instal paket [os-prober](https://www.archlinux.org/packages/?name=os-prober) sebelum menjalankan perintah dibawah ini.Meskipun _os-prober_ tidak mampu mendeteksi sistem operasi secara baik lainnya di sistem UEFI.

```
# grub-mkconfig -o /boot/grub/grub.cfg

```

Silahkan lihat halaman [GRUB](/index.php/GRUB "GRUB") untuk informasi lebih mendalam.

## Konfigurasi lebih lanjut sistem dasar Arch Linux

Dari titik ini, anda dapat mengatur lebih lanjut sistem dasar Arch Linux anda.

* * *

Login sebagai root. Kita akan mengatur pacman dan memperbaharui sistem.

### Konfigurasi pacman

Edit /etc/pacman.conf:

```
nano -w /etc/pacman.conf

```

dan hilangkan # dari baris "Include = /etc/pacman.d/community" dan "[community]". Pada repositori ini terdapat banyak aplikasi yang bermanfaat.

Sekarang bukalah /etc/pacman.d/mirrorlist:

```
 nano /etc/pacman.d/mirrorlist

```

dan pilihlah lokasi mirror terdekat dengan anda.

### Konfigurasi jaringan jika dibutuhkan

Jika semua berjalan lancar, maka sekarang seharusnya anda memiliki jaringan yang bekerja. Cobalah mem_ping_ www.google.com untuk memastikan ini.

```
ping -c 3 www.google.com

```

Jika jaringan anda sudah berjalan, lanjutkan ke proses "Update, Sync dan Upgrade dengan pacman".

Namun jika setelah melakukan _ping_ di atas anda mendapatkan pesan "unknown host", dapat disimpulkan bahwa jaringan belum berjalan. Anda dapat melihat berkas berikut dan atur konfigurasinya:

**/etc/rc.conf** # terutama periksa bagian HOSTNAME= dan NETWORKING

**/etc/hosts** # Lihat format penulisannya.

**/etc/resolv.conf** # Jika anda menggunakan static IP. Jika menggunakan DHCP, berkas ini akan dibuat dan dihapus secara otomatis,tapi hal ini dapat diubah sesuai dengan keinginan anda. (Lihat [Network](/index.php/Network "Network").)

Petunjuk pengaturan lebih terperinci dapat dilihat pada artikel [Network](/index.php/Network "Network").

#### Jaringan kabel LAN

Periksa Ethernet anda menggunakan perintah:

```
ifconfig

```

Anda akan melihat baris untuk eth0\. Jika diperlukan, anda dapat mengatur konfigurasi _static IP_:

```
ifconfig eth0 <ip address> netmask <netmask> up 

```

dan _default gateway_

```
ip route add default via <ip address gateway>

```

periksa apakah /etc/resolv.conf memuat DNS server anda. Tambahkan jika tidak ada.

Periksa kembali jaringan anda dengan:

```
ping -c 3 www.google.com

```

Jika semua berjalan lancar, atur kembali /etc/rc.conf sesuai dengan pada bagian 2.6 (static IP). Jika anda memiliki server/router DHCP, cobalah:

```
dhcpcd eth0

```

Jika perintah ini berjalan, aturlah /etc/rc.conf seperti yang dijelaskan pada bagian 2.6 (dynamic IP).

#### Jaringan nirkabel (seperti wifi)

Silahkan cek halaman [Wireless network configuration](/index.php/Wireless_network_configuration "Wireless network configuration") untuk mengetahui cara mengkonfigurasinya lebih lanjut.

#### Modem Analog

Untuk bisa menggunakan modem analog, eksternal, _Hayes-compatible_, kamu perlu memiliki setidaknya paket `ppp` terpasang. Modifikasi berkas `/etc/ppp/options` untuk menyesuaikan dengan kebutuhan kamu dan mengacu pada `man pppd`. Kamu mungkin perlu mengatur skrip `chat` untuk memasukkan _username_ dan _password_ dari ISP setelah koneksi berhasil. Halaman manual `pppd` dan `chat` memiliki contoh yang baik agar koneksi berhasil jika kamu merasa kurang berpengalaman. Dengan `udev`, _serial ports_ kamu biasanya diidentifikasi sebagai `/dev/tts/0` dan `/dev/tts/1`. Tips: Baca [Dialup without a dialer HOWTO](/index.php/Dialup_without_a_dialer_HOWTO "Dialup without a dialer HOWTO").

Daripada repot dengan _plain pppd_, kamu memiliki pilihan untuk memasang `wvdial` atau perangkat sejenis untuk memudahkan penyetelan. Jika kamu memakai WinModem, yang mana dasarnya berupa _PCI plugin card_ yang berfungsi sebagai modem analog internal, kamu sebaiknya mengacu pada informasi di laman (_homepage_) [LinModem](http://www.linmodems.org/).

#### ISDN

Penyetelan ISDN dapat dilakukan dalam 3 langkah:

1.  Instal dan konfigurasi perangkat keras/_hardware_
2.  Instal dan konfigurasi perlengkapan ISDN
3.  Menambah setelan untuk ISP kamu

Kernel terkini Arch telah memasukkan modul ISDN, berarti kamu tidak perlu untuk mengompilasi ulang kernel meskipun kamu berniat akan memakai perangkat keras ISDN lawas. Setelang memasang kartu ISDN secara fisik di mesin kamu atau mencolokkannya di kotak USB ISDN kamu, kamu dapat mencoba mengaktifkan modul dengan `modprobe`. Hampir semua kartu PCI ISDN pasif ditangani oleh modul hisax, yang membutuhkan 2 parameter: tipe dan protokol. Kamu harus mengeset protokol ke '1' jika negara kamu memakai standar 1TR6, '2' jika memakai EuroISDN (EDSS1), '3' jika memakai _hooked_ ke _leased-line_ tanpa _D-channel_, dan '4' untuk US NI1.

Detail tentang semua setelan dan bagaimana mengaturnya sudah ada di dokumentasi kernel, lebih spesifik lagi ada di subdirektori isdn, dan tersedia daring (dalam jaringan; _online_). Tipe parameter tergantung kartu kamu; sebuah daftar yang menyajikan semua kemungkinan tipe dapat ditemukan di dokumentasi kernel `README.HiSax`. Pilih kartu kamu dan aktifkan modul dengan pilihan yang tepat seperti ini:

```
# modprobe hisax type=18 protocol=2

```

Ini akan mengaktifkan modul hisax untuk ELSA Quickstep 1000PCI saya, digunakan di Jerman dengan protokol EDSS1\. Kamu akan menemukan keluaran _debugging_ yang bermanfaat di berkas `/var/log/everything.log`, yang mana kamu akan melihat bahwa kartu kamu sedang dipersiapkan untuk bisa dipakai. Tolong dicatat bahwa kamu mungkin perlu mengaktifkan beberapa modul USB sebelum kamu dapat bekerja dengan Adapter USB ISDN eksternal.

Sekali kamu memperoleh konfirmasi bahwa kartu kamu sudah bekerja dengan setelan yang ada, kamu dapat menambahkan opsi modul berikut ke berkas `/etc/modprobe.d/modprobe.conf`:

```
alias ippp0 hisax
options hisax type=18 protocol=2

```

Alternatifnya, kamu dapat menambahkan baris opsi di sini, dan menambahkan hisax ke MODULES array di berkas `rc.conf`. Ini pilihan anda, sebenarnya, tetapi contoh ini memiliki keuntungan bahwa modul tidak akan aktif hingga benar-benar dibutuhkan.

Selesai, kamu seharusnya sudah bisa bekerja, perangkat keras sudah didukung. Kini kamu butuh perlengkapan dasar untuk benar-benar bisa memakainya.

Instal paket `isdn4k-utils`,dan baca `manpage` terkait `isdnctrl`; kamu bisa memulainya dari sana. Di bagian bawah manpage akan kamu temukan penjelasan tentang bagaimana membuat sebuah konfigurasi berkas yang dapat dipahami oleh isdnctrl, beserta beberapa contohnya. Tolong dicatat bahwa kamu harus menambahkan SPID kamu ke setelan MSN kamu dipisahkan dengan titik koma jika kamu memakai US NI1.

Setelah kamu mengonfigurasikan kartu ISDN dengan perlengkapan isdnctrl, kamu harusnya bisa melakukan dial via mesin dengan parameter PHONE_OUT, tetapi gagal otentifikasi username dan password. Untuk bisa berfungsi, tambahkan username dan password kamu ke berkas `/etc/ppp/pap-secrets` atau `/etc/ppp/chap-secrets` sebagaimana kamu mengonfigurasikan koneksi PPP analog, tergantung protokol ISP yang kamu gunakan. Jika ragu, letakkan data kamu di kedua berkas.

Jika kamu telah menyetel semuanya dengan benar, kamu harusnya sudah bisa memperoleh koneksi dial-up yang stabil saat ini dengan

```
# isdnctrl dial ippp0

```

sebagai root. Jika kamu memperoleh masalah, ingat untuk mengecek berkas log!

#### DSL (PPPoE)

Instruksi berikut relevan bagi kamu jika PC kamu ditujukan untuk pengelolaan koneksi ke ISP kamu. Kamu tidak perlu melakukan apapun tetapi cukup menentukan _default gateway_ yang tepat jika kamu memakai _router_ terpisah untuk melakukan _grunt work_.

Sebelum kamu bisa menggunakan koneksi daring (_online_) DSL kamu, kamu harus memasang (_install_) kartu jaringan (_network card_) yang dipakai untuk menghubungkan Modem-DSL ke komputer. Setelah menambahkan kartu jaringan yang baru ke `modules.conf/modprobe.conf` atau _MODULES array_, kamu harus memasang paket `rp-pppoe` dan menjalankan perintah atau skrip `pppoe-setup` untuk mengonfigurasikan koneksi kamu. Setelah kamu memasukkan semua data, kamu bisa _connect_ dan _disconnect_ dengan perintah:

 `/etc/rc.d/adsl start` 

dan

 `/etc/rc.d/adsl stop` 

Penyetelan biasanya mudah, tetapi silakan membaca halaman manual untuk petunjuk lebih lanjut. Jika kamu ingin _dial_ otomatis saat _boot-up_, tambahkan `adsl` ke _DAEMONS array_.

## Update, Sync dan Upgrade sistem dengan [pacman](/index.php/Pacman "Pacman")

Sekarang kita akan memperbarui sistem menggunakan [pacman](/index.php/Pacman "Pacman"). Pacman adalah _**pac**kage **man**ager_ bagi Linux Arch. Pacman adalah _Package Manager_ yang cepat, simpel, dan tangguh. Dia mengelola seluruh sistem _package_ kamu, dan memungkinkan adanya proses instalasi, _downgrade_ (melalui tembolok/_cache_), kompilasi _package custom_, pengaturan dependensi secara otomatis, dan banyak kemampuan lainnya.

_Update_, _sync_, dan **upgrade** sistem anda dengan:

 `pacman -Syu` 

pacman akan mengunduh informasi terbaru yang tersedia terkait semua _package_ dan melakukan proses _upgrade_ jika ada. Kamu kemungkinan akan mendapatkan permintaan untuk meng-_upgrade_ pacman, ketikkan "y" dan jalankan pacman -Syu jika sudah selesai.

##### _Perhatikan pesan yang muncul ketika terjadi proses_ upgrading _kernel!_

Jika kernel di-_upgrade_, modul-modul seperti `nvidia` mungkin tidak berfungsi, karena modul yang baru, versi yang baru bertentangan dengan kernel yang baru, dan sistem kamu masih memakai yang lama. _Reboot_ mungkin diperlukan.

##### Mantapnya _Rolling Release_

Ingatlah bahwa Linux Arch adalah sebuah distro yang bersifat **Rolling Release**. Ini berarti bahwa tidak perlu ada instal ulang ataupun pembaruan sistem secara bersamaan untuk mendapatkan versi yang terbaru. Hanya dengan menjalankan **pacman -Syu** secara rutin menjadikan sistemmu selalu terbarui dan berada pada _bleeding edge_.

##### Mengenal Pacman lebih dalam

Pacman adalah sahabat para pengguna Linux Arch. Sangat dianjurkan bagi pengguna untuk mempelajarinya dan menggunakan peralatan pacman. Coba jalankan:

 `man pacman` 

Lihatlah pada bagian akhir artikel ini, dan lihatlah bagian [pacman](/index.php/Pacman "Pacman") ketika anda sengggang.

### Menambahkan pengguna dan atur grup

Kamu seharusnya tidak menjalankan kegiatan-kegiatan normal sebagai seorang root. Hal tersebut bukan saja sebuah praktik yang buruk, tapi merupakan kegiatan yang berbahaya. Root adalah tipe pengguna/_user_ administrasi. Oleh karena itu, tambahkanlah sebuah pengguna baru:

 `adduser` 

Meskipun pengaturan standar sudah aman untuk digunakan, tetapi anda dapat menambahkan pengguna sebagai anggota dari kelompok _audio_ dan _wheel_.

_Audio_ memungkinkan kamu untuk menggunakan kartu audio, sementara itu _wheel_ mengizinkan kamu untuk menjadi pengguna root menggunakan perintah `su`. Kelompok lain yang dapat ditambahkan adalah:

*   disk - untuk mengelola disk, seperti _USB flash drive_ dan sejenisnya.

*   storage - untuk mengelola disk penyimpanan.

*   video - untuk mengelola tugas-tugas video.

*   optical - untuk mengelola tugas-tugas terkait _drive_ optik.

*   floppy - untuk mengakses floppy jika dibutuhkan.

*   lp - untuk mengelola tugas mencetak.

Kamu juga dapat menambahkan _user_ kamu ke dalam kelompok _optical_ untuk mengaktifkan perekaman CD/DVD.

Lihat artikel [Groups](/index.php/Groups "Groups") untuk mengetahui kelompok mana saja yang perlu kamu masukkan untuk _user_ kamu. Kamu juga bisa menambahkan _user_ kamu ke dalam kelompok berikut (sebagai root):

 `usermod -aG audio,video,floppy,lp,optical,network,storage,wheel USERNAME` 

## Instalasi dan konfigurasi perangkat keras

### Konfigurasi Kartu Audio

Kartu suara anda seharusnya sudah bekerja, tetapi anda tidak dapat mendengarkan suara apapun karena di awal ia berada dalam status diam. Instal alsa-utils

```
 pacman -S alsa-utils

```

dan gunakan alsamixer untuk mengatur chanel:

```
 alsamixer

```

aktifkan chanel Master dan PCM dengan bergerak ke posisi chanel masing-masing dan tekan **M**. Naikkan volume dengan tombol atas. Keluar dari alsamixer dengan menggunakan tombol ESC, dan simpan konfigurasi menggunakan perintah:

```
 alsactl store

```

Jika anda merencanakan untuk menggunakan sebuah _desktop environment_ seperti GNOME dan KDE, dan menginginkan alsa untuk mengingat konfigurasi ketika anda sudah mengganti konfigurasinya, jangan jalankan perintah diatas--pengaturan volume anda akan diingat secara otomatis.

Jangan lupa untuk menambahkan alsa pada entri DAEMON pada `/etc/rc.conf` untuk memuat kembali mixernya secara otomatis saat boot-up. Jalankan perintah berikut sebagai root:

```
 DAEMONS=(syslog-ng network crond **alsa**)

```

### Konfigurasi _kecepatan frekuensi CPU_

Prosesor modern mampu menurunkan frekuensi dan voltasenya untuk mengurangi panas dan konsumsi daya. Berkurangnya panas mendukung sistem menjadi lebih tenang; sistem desktop pun akan mendapat manfaat dari hal ini. Instalasi: [cpufrequtils](https://www.archlinux.org/packages/?name=cpufrequtils):

 `pacman -S cpufrequtils` 

dan tambahkan `cpufrequtils` ke _daemons_ kamu di `/etc/rc.conf`. Edit berkas `/etc/conf.d/cpufreq` dan ubah

 `governor="conservative"` 

yang mana akan meningkatkan frekuensi CPU secara dinamis jika diperlukan (aman juga digunakan di sistem desktop). Sesuaikan `min_freq` dan `max_freq` dengan spesifikasi CPU kamu. Jika kamu tidak mengetahui frekuensinya, jalankan `cpufreq-info` setelah mengaktifkan salah satu modul _frequency scaling_-nya. Tambahkan modul _frequency scaling_ ke berkas `/etc/rc.conf`. Kebanyakan desktop dan komputer jinjing (_notebook_) dapat dengan mudah memakai _driver_ `acpi-cpufreq`, sedangkan opsi lain diantaranya `p4-clockmod, powernow-k6, powernow-k7, powernow-k8`, dan `speedstep-centrino`. _Load_ modul

 `modprobe <namamodul>` 

dan start `cpufreq` dengan

 `/etc/rc.d/cpufreq start` 

Untuk lebih detailnya, lihat [Cpufrequtils](/index.php/Cpufrequtils "Cpufrequtils").

### _Tweak_ tambahan untuk laptop

Dukungan ACPI dibutuhkan jika kamu ingin memakai beberapa fungsi spesial komputer jinjing/_notebook_/_laptop_ (misalnya _sleep_, _sleep_ ketika _lid_ ditutup, _special keys_...). Pasang `acpid`

 `pacman -S acpid` 

dan tambahkan ke _daemons_ di `/etc/rc.conf` (acpid). Start dengan

 `/etc/rc.d/acpid start` 

Informasi lebih spesifik tentang Linux Arch di pelbagai komputer jinjing (_laptop_/_notebook_) dapat ditemukan di [Category:Laptops](/index.php/Category:Laptops "Category:Laptops").

## Instalasi dan Konfigurasi X

See [Xorg](/index.php/Xorg "Xorg").

## Membuat /etc/X11/xorg.conf

##### Apa itu /etc/X11/xorg.conf?

/etc/X11/xorg.conf adalah **berkas konfigurasi utama** untuk **X** Window System, fondasi dari **G**raphical **U**ser **I**nterface. Berkas ini berisi konfigurasi berupa teks yang terbagi kedalam bagian dan subbagian. Bagian yang penting adalah _Files, InputDevice, Monitor, Modes, Screen, Device dan ServerLayout_. Bagian-bagian ini dapat muncul dalam urutan yang beragam. Bagian-bagian tadi juga dapat muncul lebih dari sekali.

Secara default, kamu tidak akan memiliki berkas ini. Bahkan dengan Xorg versi terbaru, kamu tidak membutuhkan berkas ini _jika_ proses pengenalan sistem secara otomatis _berjalan dengan baik_, dan jika kamu tidak perlu mengaktifkan fitur seperti aiglx dan sebagainya. _Tetapi kebanyakan orang tetap membutuhkan berkas ini_.

Ada beberapa cara untuk membuat berkas /etc/X11/xorg.conf:

*   Menggunakan The Xorg way untuk membuat berkas ini:

```
Xorg -configure

```

dan proses ini akan membuat berkas /root/xorg.conf. Pindahkan berkas ini ke lokasi yang benar:

```
mv /root/xorg.conf.new /etc/X11/xorg.conf

```

*   Cara lain untuk membuat berkas xorg.conf tanpa mengotori tangan anda adalah menggunakan alat khusus dari Arch:

```
hwd -xa
hwd (to see the various options)

```

*   Driver video propietary juga memiliki alat untuk mengatur xorg.conf. Alat-alat ini yaitu:

```
aticonfig

```

dan

```
nvidia-xconfig

```

Tetapi, kamu seharusnya tidak merasa asing dengan mengatur konfigurasi xorg.conf secara manual. Karena kamu akan butuh untuk mengatur konfigurasi ini secara manual nantinya untuk menyelesaikan beberapa isu.

Misalnya untuk mengatur konfigurasi driver video:

```
nano /etc/X11/xorg.conf

```

Kemudian:

```
Section "Device"
Driver  "i810"

```

##### Simple baseline X test

Pada titik ini, seharusnya kamu sudah memiliki xorg terinstalasi. Jika kamu ingin mencoba konfigurasi ini sebelum menginstal sebuah desktop environment yang lengkap, instal terlebih dahulu **xterm**. Xterm adalah sebuah terminal yang berjalan pada X Server environment. Xterm memungkinkan kamu untuk menguji coba konfigurasi /etc/X11/xorg.conf secara efektif.

Sebagai alternatif, jika kamu ingin menguji coba apakah proses pendeteksian secara otomatis berjalan secara otomatis (berarti belum ada berkas /etc/X11/xorg.conf, maka lakukanlah:

```
pacman -S xterm

```

Ubah berkas /home/username/.xinitrc, **sebagai user biasa**, untuk mengatur X Server mana yang akan dipanggil ketika menjalankan perintah 'startx':

```
su yourusername

```

```
nano ~/.xinitrc

```

dan tambahkan (atau buang tanda #)

```
exec xterm

```

Sehingga berkas ini terlihat seperti:

```
#!/bin/sh
#
# ~/.xinitrc
#
# Executed by startx (run your window manager from here)
#
exec xterm
# exec wmaker
# exec startkde
# exec icewm
# exec blackbox
# exec fluxbox

```

Pastikan hanya ada satu baris saja pada berkas ~/.xinitrc yang tidak diberi tanda comment (#).

Jika kamu tidak memiliki berkas ~/.xinitrc, buatlah berkas ini secara manual dan isilah berkas ini dengan konfigurasi seperti di atas.

Jalankan X Server sebagai user biasa, dengan perintah:

```
startx

```

Seharusnya kamu memiliki sebuah session xterm sampingan yang berjalan. Kamu dapat keluar dari X Server ini dengan Ctrl+Alt+Backspace, atau dengan mengetikkan "exit". Jika kamu memiliki permasalahan menjalankan X Server, kamu dapat melihat pesan kesalahan pada berkas /var/log/Xorg.0.log.

Sekarang, kamu mungkin mau menginstal sebuah login manager seperti [GDM](/index.php/GDM "GDM") atau [KDM](/index.php/KDM "KDM"), tetapi ini _dapat_ ditunda dulu. Untuk konfigurasi yang lebih terinci mengenai xorg, dapat dilihat pada artikel [Xorg](/index.php/Xorg "Xorg").

### Mengatur _Layout Keyboard_

Kamu mungkin ingin mengubah _layout_ papan ketik (_keyboard_) kamu. Untuk melakukannya, edit berkas `/etc/X11/xorg.conf` kamu dan tambahkan baris berikut di _Input Section (keyboard0)_ (contoh berikut menunjukkan _layout_ papan ketik Jerman tanpa _dead keys_; sesuaikan dengan kebutuhan kamu).

```
Option          "XkbLayout"     "de"
Option          "XkbVariant"    "nodeadkeys"
```

### Mengatur _scroll wheel_ Tetikus/_Mouse_

Ketika tetikus (_mouse_) kamu seharusnya berfungsi otomatis, kamu mungkin ingin memakai _scroll wheel_-nya. Tambahkan baris berikut di _Input Section (mouse0)_:

 `Option      "ZAxisMapping" "4 5 6 7"` 

### evdev

Jika kamu memiliki tetikus (_mouse_) USB modern dengan beberapa tombol dan/atau fungsi, kamu mungkin perlu memasang _driver_ tetikus _evdev_, yang akan memungkinkan kamu mengembangkan fungsi tetikus kamu:

 `pacman -S xf86-input-evdev` 

_Load driver_-nya:

 `modprobe evdev` 

Temukan nama tetikus kamu:

 `cat /proc/bus/input/devices | egrep "Nama"` 

Gunakan nama tetikus, konfigurasikan berkas `/etc/X11/xorg.conf` di seksi _InputDevice_, misalnya:

```
Section "InputDevice"
  Identifier      "Evdev Mouse"
  Driver          "evdev"
  Option          "Name" "Logitech USB-PS/2 Optical Mouse"
  Option          "CorePointer"
 EndSection
```

Kamu boleh memiliki hanya **satu** deklarasi perangkat _CorePointer_ di `/etc/X11/xorg.conf`, jadi pastikan untuk meng-_comment out_ entri tetikus lain sampai kamu merasa aman untuk menghapus entri yang lama.

Juda edit bagian _ServerLayout_ untuk memasukkan _Evdev Mouse_ sebagai _CorePointer_, misalnya:

```
Section "ServerLayout"
    Identifier     "Layout0"
    Screen      0  "Screen0"
    InputDevice    "Keyboard0" "CoreKeyboard"
    InputDevice    "Evdev Mouse" "CorePointer"
```

### Memakai _Driver_ Grafis Proprietari (nVIDIA, ATI)

Anda dapat memilih untuk menggunakan driver video kepemilikan dari nVIDIA atau ATI.

#### Kartu Grafis nVIDIA

Driver hak milik nVIDIA umumnya dianggap sangat baik kualitasnya, dan menawarkan performa 3D yang unggul.

Sebelum Anda mengkonfigurasi Graphics Card Anda, Anda akan harus mengetahui driver mana yang cocok. Arch saat ini memiliki 3 driver yang berbeda yang sama dengan subset tertentu dari kartu:

**1\. nvidia-71xx** _untuk Kartu yang sangat lama seperti TNT dan TNT2_

**2\. nvidia-96xx** _kartu yang sedikit lebih baru hingga GF 4_

**3\. nvidia** _GPU terbaru setelah GF 4_

Konsultasikan Situs nVIDIA untuk melihat mana yang tepat untuk Anda. Perbedaannya hanya pada instalasi, konfigurasi bekerja sama dengan setiap driver.

Instal driver nvidia yang sesuai, cth.:

```
pacman -S nvidia 

```

Pada tahap ini, Anda memiliki 3 pilihan tentang cara untuk melanjutkan.

*   **1.** Jika Anda tidak memiliki xorg.conf sama sekali, atau jika Anda memiliki xorg.conf yang ada

dan ingin **menghasilkan sesuatu yang sama sekali baru** dengan utilitas nVIDIA, buat cadangan untuk yang lama:

```
mv /etc/X11/xorg.conf /etc/X11/xorg.old

```

Lalu buat baru /etc/X11/xorg.conf dengan

```
nvidia-xconfig

```

Utilitas nvidia-xconfig biasanya akan membuat sangat singkat, efisien, xorg.conf yang mudah dibaca

Ia juga memiliki beberapa pilihan yang selanjutnya akan menentukan isi dan pilihan dari file xorg.conf yang. Sebagai contoh,

```
nvidia-xconfig --composite --add-argb-glx-visuals

```

Untuk informasi lebih lanjut, lihat nvidia-xconfig(1).

*   **2.** **Pilihan para ahli:** Jika Anda memiliki xorg.conf yang yang ada dan ingin

menyimpannya, sunting xorg Anda secara manual sesuai yang diperlukan, dan setidaknya, sesuaikan bagian **Device** dengan mengubah driver "<namadriverlama>" ke Driver "nvidia".

```
Section "Device"

Driver  "nvidia" 

```

*   **3.** Atau, Anda dapat memilih untuk tetap menggunakan

/etc/X11/xorg.conf yang ada, dan jalankan:

```
nvidia-xconfig

```

yang secara otomatis akan meng-**update** /etc/X11/xorg.conf anda untuk digunakan dengan driver milik nVIDIA.

Beberapa pilihan tweak yang berguna di bagian device (berhati-hatilah bahwa ini mungkin tidak bekerja pada sistem Anda):

```
       Option          "RenderAccel" "true"
       Option          "NoLogo" "true"
       Option          "AGPFastWrite" "true"
       Option          "EnablePageFlip" "true"

```

Utilitas nvidia-xconfig secara otomatis akan menempatkan pilihan glx di xorg Anda. Jika Anda tidak menggunakan nvidia-xconfig, maka Anda harus menambahkan ini ke bagian modul Anda:

```
Load "glx"

```

Periksa kembali /etc/X11/xorg.conf Anda untuk memastikan kedalaman standar Anda, horisontal refresh, vertikal refresh, dan resolusi dapat diterima.

Logout dan login.

Mulai X server sebagai pengguna normal, untuk mencoba konfigurasi anda:

```
startx

```

Instruksi lanjutan untuk konfigurasi nvidia dapat ditemukan di artikel [NVIDIA](/index.php/NVIDIA "NVIDIA").

#### Kartu Grafis ATI

Pemilik ATI memiliki dua pilihan untuk driver. Jika Anda tidak yakin driver mana yang digunakan, silakan coba yang open source terlebih dahulu. Driver open source akan sesuai dengan yang paling dibutuhan karena pada umumnya tidak bermasalah.

Instal Driver **hak milik/proprietary** ATI dengan

```
pacman -S fglrx

```

Gunakan alat aticonfig untuk menyunting xorg.conf. Catatan: Driver proprietary tidak mendukung AIGLX. Untuk menggunakan [Compiz](/index.php/Compiz "Compiz") atau Beryl dengan driver ini anda perlu menggunakan XGL.

Instal Driver **open-source** ATI dengan

```
pacman -S xf86-video-ati

```

Saat ini, kinerja dari driver open source ini tidak setara dengan yang berpemilik/proprietary . Juga tidak memiliki dukungan TV-out, dual-link DVI, dan mungkin fitur lainnya. Di sisi lain, mendukung AIGLX dan memiliki dukungan dual-head yang lebih baik.

Instruksi lanjutan untuk konfigurasi ATI dapat ditemukan di [ATI wiki](/index.php/ATI "ATI").

## Menginstal dan mengonfigurasikan sebuah Desktop Environment

Jika kamu menanyakan 2 orang apa itu Desktop Environment atau Window Manager, kamu akan memperoleh 5 jawaban berbeda.

*   Jika kamu ingin sesuatu yang kaya fitur dan nampak serupa dengan Windows dan Mac OSX, **KDE** adalah pilihan yang baik
*   Jika kamu ingin sesuatu yang minimalis, mengikuti prinsip yang mendekati K.I.S.S., **GNOME** adalah pilihan yangg baik
*   Jika kamu punya mesin tua atau ingin sesuatu yang lebih ringan, **xfce4** adalah pilihan yang baik, tetap mampu memberi _desktop environment_ yang lengkap
*   Jika kamu butuh sesuatu yang lebih ringan lagi, **openbox, fluxbox atau fvwm2** mungkin pilihan yang tepat (tidak menyebut semua window managers ringan lain seperti **windowmaker dan twm**).
*   Jika kamu membutuhkan sesuatu yang sama sekali berbeda, coba **ion, wmii, atau dwm**.

### Instalasi Huruf/Font

Pada poin ini, kamu mungkin ingin memasang beberapa huruf yang berpenampilan menarik, **sebelum** memasang _desktop environment_/_window manager_. _Dejavu_ dan _bitstream-vera_ adalah set huruf yang baik. Untuk situs Web, kamu mungkin membutuhkan huruf dari Microsoft juga. Pasang dengan cara:

 `pacman -S ttf-ms-fonts ttf-dejavu ttf-bitstream-vera` 

### GNOME

#### Tentang GNOME

**G**NU **N**etwork **O**bject **M**odel **E**nvironment. Proyek GNOME menyediakan 2 hal: _The GNOME desktop environment_, sebuah desktop yang intuitif dan atraktif bagi pengguna, dan platform pengembangan berbasis GNOME, suatu _extensive framework_ untuk membangun aplikasi yang terintegrasi ke desktop.

#### Instalasi

Pasang GNOME dengan

```
pacman -S gnome

```

Jika kamu menginginkan suatu distribusi GNOME yang lebih komplit dengan banyak fitur ekstra, lakukan:

```
pacman -S gnome-extra

```

Aman untuk memilih semua paket yang ada.

##### DAEMON yang berguna untuk GNOME

Mengingat kembali dari keterangan di atas bahwa _daemon_ adalah program yang berjalan di _background_, menunggu suatu _events_ terjadi dan menawarkan layanannya. _Daemon_ **hal**, melebihi yang lain, akan otomatis me-_mounting disks_, _optical drives_, dan _USB drives_/_thumbdrives_ untuk digunakan di GUI. _Daemon_ **fam** memungkinkan representasi _real-time_ alterasi berkas di GUI, mengijinkan akses instan ke program yang terpasang, atau perubahan di sistem berkas (_file system_). Keduanya, **hal** dan **fam**, memudahkan pengguna GNOME.

Kamu mungkin ingin memasang _graphical login manager_. Untuk GNOME, _daemon_ **gdm** adalah pilihan yang tepat. Pasang _gdm_ dengan

 `pacman -S gdm` 

Kamu akan memerlukan _daemon_ **hal** dan **fam**.

Start _hal_ dan _fam_:

 `/etc/rc.d/hal start`  `/etc/rc.d/fam start` 

Tambahkan ke berkas `/etc/rc.conf` di bagian _DAEMONS_, sehingga keduanya akan dipanggil saat _boot-up_:

 `nano /etc/rc.conf`  `DAEMONS=(syslog-ng network crond alsa hal fam gdm)` 

(Jika kamu lebih memilih log masuk ke _console_ dan memulai X secara manual sesuai tradisi Slackware, jangan ikutkan _gdm_).

#### ~/.xinitrc

Berkas ini mengontrol apa yang akan terjadi setelah kamu mengetikkan `startx`.

Edit berkas `/home/username/.xinitrc` untuk mengaktifkan sesi GNOME:

 `nano ~/.xinitrc` 

_Uncomment_ baris `exec gnome-session` sehingga nampak seperti di bawah:

```
 #!/bin/sh
 #
 # ~/.xinitrc
 #
 # Executed by startx (run your window manager from here)
 #
 #exec xterm
 #exec wmaker
 # exec startkde
 exec gnome-session
 # exec icewm
 # exec blackbox
 # exec fluxbox
```

Jika kamu tidak memiliki berkas `~/.xinitrc`, buatlah sesuai informasi di atas. Ingat, kamu hanya bisa memiliki satu baris yang aktif di `~/.xinitrc`.

Beralih sebagai pengguna normal (sesuaikan nama kamu):

```
su - username

```

Dan tes dengan:

```
startx

```

Kamu mungkin ingin memasang sebuah _terminal_ dan _editor_. Saya menyarankan `geany` dan `gnome-terminal` (bagian dari kelompok `gnome-extra`):

```
pacman -S geany gnome-terminal

```

Instruksi lebih lanjut untuk memasang dan mengonfigurasikan GNOME dapat ditemukan di artikel [GNOME](/index.php/GNOME "GNOME").

#### Eye Candy

Kamu mungkin merasa ikon dan tema bawaan GNOME kurang atraktif. Sebuah tema gtk yang menarik yaitu murrine. Pasang dengan

```
pacman -S gtk-engine-murrine

```

dan pilih di System→Preferences→Theme. Kamu akan menemukan lebih banyak tema, ikon, dan _wallpaper_ di [GNOME Look](http://www.gnome-look.org).

### KDE

#### Tentang KDE

The **K** **D**esktop **E**nvironment. KDE adalah sebuah graphical desktop environment yang lengkap dan kuat untuk Linux dan Unix. KDE menggambungkan kemudahan penggunaan, fitur mutakhir, dan desain yang menawan.

#### Installation

Arch offers several versions of kde: **kde, kdebase, and KDEmod**. Choose **one** of the following, and continue below with **"Useful KDE DAEMONS"**:

**1.)** Package **kde** is the complete, vanilla KDE, ~300MB.

```
pacman -S kde

```

**2.)** Package **kdebase** is a slimmed-down version with less applications, ~80MB.

```
pacman -S kdebase

```

**3.)** Lastly, **KDEmod** is an Arch Linux exclusive, community-driven system which is modified for extreme performance and modularity. The KDEmod project website can be found at [http://kdemod.ath.cx/](http://kdemod.ath.cx/). KDEmod is extremely fast, lightweight and responsive, with a pleasing, customized theme.

To install KDEmod in 5 easy steps, just follow these installation instructions... Note: Before you start, please remember to read all of the install messages. They are fairly comprehensive and should solve any upcoming questions after the installation. If you cant scroll back to see all messages, just take a look into /var/log/pacman.log

*   1\. Add the kdemod repo to your /etc/pacman.conf:

```
nano /etc/pacman.conf

```

Add one of these entries at the top of your server list:

```
       [kdemod]
       Server = [http://kdemod.ath.cx/repo/current/i686](http://kdemod.ath.cx/repo/current/i686)

```

for 32 bit Arch, or

```
       [kdemod]
       Server = [http://kdemod.ath.cx/repo/current/x86_64](http://kdemod.ath.cx/repo/current/x86_64)

```

for 64 bit Arch.

*   2\. You must also activate the [community] repository in /etc/pacman.conf

because KDEmod needs some packages from this repository. Make sure the following lines are uncommented:

```
[community]
Include = /etc/pacman.d/community

```

*   3\. Update your package database with pacman -Syu. Now you can choose between

two installations:

```
       pacman -S kdemod  _- installs a light base system_
       pacman -S kdemod-complete  _- installs the full KDE desktop_

```

If you encounter any errors or conflicts at this step, check pacmans output, and if there are some unsolvable problems, tell us about them at the forums.

*   4\. Install your localization. Take a look at the list of packages or simply do

a pacman -Ss kdemod-kde-i18n to see which of them are already included.

*   5\. Install all the extra apps you want. You can check out all available KDEmod

packages by entering pacman -Sl kdemod

#### Useful KDE DAEMONS

KDE will require the **hal** (**H**ardware **A**bstraction **L**ayer) and **fam** (**F**ile **A**lteration **M**onitor) daemons. The **kdm** daemon is the **K** **D**isplay **M**anager, which provides a **graphical** login**, if desired.**

Recall from above that a daemon is a program that runs in the background, waiting for events to occur and offering services. The hal daemon, among other things, will automate the mounting of disks, optical drives, and USB drives/thumbdrives for use in the GUI. The fam daemon will allow real-time representation of file alterations in the GUI, allowing instant access to recently installed programs, or changes in the file system.. Both **hal** and **fam** make life easier for the KDE user, and are installed when you install KDE.

Start hal and fam:

```
/etc/rc.d/hal start

```

```
/etc/rc.d/fam start

```

Edit your DAEMONS section in /etc/rc.conf:

```
nano /etc/rc.conf

```

Add **hal** and **fam** to your DAEMONS section, to start them on bootup. If you prefer a graphical login, add **kdm** as well:

```
DAEMONS=(syslog-ng network crond alsa **hal fam kdm**)

```

(If you prefer to log into the **console** and manually start X in the 'Slackware tradition', leave out kdm.)

##### ~/.xinitrc

This file controls what occurs when you type 'startx'.

Edit your /home/username/.xinitrc to utilize KDE:

```
nano ~/.xinitrc

```

Uncomment the 'exec startkde' line so that it looks like this:

```
#!/bin/sh
#
# ~/.xinitrc
#
# Executed by startx (run your window manager from here)
#
#exec xterm
#exec wmaker
exec startkde
# exec gnome-session
# exec icewm
# exec blackbox
# exec fluxbox

```

If you do not have a ~/.xinitrc file, simply create it with the above information. Remember, you must have only **one** uncommented line in your ~/.xinitrc.

Switch to your normal user:

```
su username

```

Now try starting your X Server:

```
startx

```

Congratulations! Welcome to your KDE desktop environment on your new Arch Linux system! You may wish to continue by viewing [Post Installation Tips](/index.php/Post_Installation_Tips "Post Installation Tips"), or the rest of the information below. Advanced instructions for installing and configuring KDE can be found in the [KDE](/index.php/KDE "KDE") article.

### Xfce

#### Tentang Xfce

Xfce adalah sebuah _Desktop Environment_ (DE), seperti GNOME atau KDE. Xfce terdiri dari suatu kumpulan aplikasi seperti aplikasi _root window_, _window manager_, _file manager_, panel, dan sebagainya. Xfce ditulis menggunakan GTK2 _toolkit_ dan mengandung lingkungan pengembangannya sendiri (pustaka/_libraries_, _daemons_, dan lain-lain) serupa dengan DE besar lain. Tidak seperti GNOME atau KDE, Xfce lebih ringan (_lightweight_) dan dirancang dalam CDE dibanding Windows atau Mac. Siklus pengembangannya lebih lambat, tetapi sangat stabil dan cepat. Xfce baik digunakan di perangkat keras (_hardware_) yang lawas.

#### Instalasi

Pasang xfce dengan cara:

 `pacman -S xfce4 xfce4-goodies` 

Jika kamu menggunakan kdm atau gdm, sebuah sesi baru xfce akan terlihat. Jika belum, tambahkan:

 `startxfce4` 

Instruksi lebih lanjut untuk memasang dan mengonfigurasikan Xfce dapat ditemukan di artikel [Xfce](/index.php/Xfce "Xfce").

### *box

#### Fluxbox

Fluxbox © adalah windowmanager lainnya untuk X. Berbasis kode Blackbox 0.61.1\. Fluxbox terlihat menyerupai blackbox dan mampu menangani styles, colors, window placement dan sesuatu yang serupa dengan blackbox (theme/style kompatibel 100%).

Instal Fluxbox dengan cara

```
pacman -S fluxbox fluxconf

```

Jika kamu memakai gdm/kdm, sebuah sesi fluxbox akan otomatis ditambahkan. Jika tidak, kamu sebaiknya memodifikasi berkas `.xinitrc` dan tambahkan baris berikut:

```
exec startfluxbox 

```

Informasi lebih lanjut ada di artikel [Fluxbox](/index.php/Fluxbox "Fluxbox").

#### Openbox

Openbox adalah _window manager extensible_ yang memenuhi standar, cepat, dan ringan.

Openbox dapat berfungsi dengan aplikasi-aplikasi kamu, dan membuat desktop kamu lebih mudah dikelola. Ini karena pendekatan pengembangannya berlawanan dengan _window manager_ umumnya. Openbox awalnya dibuat untuk memenuhi standar dan berfungsi sebagaimana mestinya. Setelah itu tim mengembangkan antarmuka visualnya.

Openbox berfungsi penuh sebagai lingkungan yang mandiri, atau dapat digunakan sebagai opsi pengganti _window manager_ bawaan di _desktop environment_ GNOME atau KDE.

Pasang `openbox` dengan cara:

 `pacman -S openbox obconf obmenu` 

Saat `openbox` terpasang, kamu akan mendapat pesan untuk memindahkan berkas `menu.xml` & `rc.xml` ke `~/.config/openbox/` di direktori `home` kamu:

```
mkdir -p ~/.config/openbox/
 cp /etc/xdg/openbox/rc.xml ~/.config/openbox/
 cp /etc/xdg/openbox/menu.xml ~/.config/openbox/
```

Dalam berkas `rc.xml`, kamu dapat mengubah pelbagai setelan Openbox (atau gunakan `obconf`). Dalam berkas `menu.xml` kamu bisa mengubah menu klik kanan kamu.

Supaya bisa log masuk ke Openbox, kamu bisa melakukannya via _graphical login_ memakai KDM/GDM atau `startx`, atau edit berkas `~/.xinitrc` (sebagai pengguna biasa) dan tambahkan baris berikut:

 `exec openbox` 

Untuk KDM, tidak perlu repot; Openbox sudah ada di pilihan menu sesi KDM.

Beberapa program yang bermanfaat untuk Openbox:

*   PyPanel atau LXpanel jika kamu butuh panel.
*   feh jika kamu ingin mengatur latar/_background_.
*   ROX jika kamu ingin _file manager_ dan ikon desktop sederhana.

Informasi lebih lanjut tersedia di artikel [Openbox](/index.php/Openbox "Openbox").

### fvwm2

FVWM adalah _window manager_ desktop virtual yang multipel sesuai standar ICCCM, sangat _powerful_, untuk sistem _X Window_.

Instal fvwm2:

 `pacman -S fvwm` 

fvwm akan muncul otomatis di sesi menu kdm/gdm. Jika belum, tambahkan:

 `exec fvwm` 

di berkas `.xinitrc` pengguna.

Catatan: versi stabil fvwm cukup lawas. Jika kamu ingin versi fvwm yang lebih terkini, paket fvwm-devel ada di repo _unstable_.

## HAL

Karena kamu akan memasang sebuah _desktop environment_, sebaiknya pasang juga HAL. HAL memungkinkan fungsi _plug-and-play_ untuk ponsel, iPod,_hard disk_ eksternal kamu, dll. HAL akan me-_mount_ perangkat tersebut dan menampilkan ikonnya di desktop dan/atau di _My Computer_, memungkinkan kamu mengakses perangkat setelah menancapkannya dibandng mengaturnya manual di berkas `/etc/fstab` atau _udev rules_ untuk tiap perangkat baru.

KDE, GNOME dan XFCE memakai HAL.

Rujuk artikel berikut untuk memasangnya: [HAL](/index.php/HAL "HAL") Wikipedia: [1](https://en.wikipedia.org/wiki/HAL_(software) "wikipedia:HAL (software)")

## Aplikasi-aplikasi yang Bermanfaat

Bagian ini tidak akan pernah lengkap. Hanya akan ditampilkan beberapa aplikasi yang baik untuk pengguna sehari-hari.

### Internet

##### Firefox

Peramban Web (_browser_) populer Firefox (Fx atau fx) tersedia via `pacman`. Pasang dengan cara:

 `pacman -S firefox` 

Untuk fungsi Web yang komplit, pastikan paket `flashplugin`, `mplayer`, `mplayer-plugin`, dan `codecs` telah terpasang:

 `pacman -S flashplugin mplayer mplayer-plugin codecs` 

(Paket `codecs` mengandung pustaka untuk konten Quicktime dan Realplayer.)

Thunderbird berguna untuk mengelola surat elektronik (surel)/email kamu. Jika kamu memakai GNOME, kamu bisa juga memakai Epiphany dan Evolution; jika kamu memakai KDE, Konqueror dan KMail bisa menjadi pilihan kamu. Jika kamu ingin sesuatu yang komplit berbeda, coba Opera. Akhir kata, jika kamu bekerja di lingkungan _console_ - atau sesi _terminal_ - kamu bisa memakai pelbagai peramban Web berbasis teks seperti ELinks, Links & Lynx, dan mengelola surel dengan [Mutt](/index.php/Mutt "Mutt"). Pidgin (sebelumnya bernama Gaim) dan Kopete adalah aplikasi _instant messengers_ yang baik untuk GNOME dan KDE. PSI dan Gajim juga baik jika kamu hanya memakai Jabber atau Google Talk.

### Perkantoran (_Office_)

OpenOffice adalah suatu perangkat _office suite_ yang komplit (serupa dengan Microsoft Office). Abiword bagus, pengolah kata alternatif yang ringan, dan Gnumeric adalah sebuah pengganti Excel untuk desktop GNOME. KOffice adalah _office suite_ komplit untuk desktop KDE. GIMP (atau GIMPShop) adalah program grafis berbasis piksel (serupa dengan Adobe Photoshop), dimana Inkscape adalah program grafis berbasis vektor (seperti Adobe Illustrator). Dan, tentu saja, Arch hadir dengan satu set penuh program LaTeX.

## Multimedia

### Pemutar Video

#### VLC

VLC Player adalah pemutar multimedia untuk Linux. Untuk memasangnya, ketik kode di bawah:

 `pacman -S vlc` 

(TODO) Instruksi untuk plug-in VLC-mozilla.

#### Mplayer

MPlayer adalah pemutar multimedia untuk Linux. Untuk memasangnya, ketik kode di bawah:

 `pacman -S mplayer` 

Ada juga _plug-in_ Mozilla untuk video dan _streams embedded_ di halaman Web. Untuk memasangnya, ketik kode di bawah:

 `pacman -S mplayer-plugin` 

Jika kamu memakai KDE, KMplayer adalah pilihan yang baik. Tersedia _plug-in_ untuk video dan _streams embedded_ di halaman Web, yang berfungsi dengan Konqueror. Untuk memasangnya, ketik kode di bawah:

 `pacman -S kmplayer` 

(TODO) Instruksi GMPlayer.

#### GNOME

##### Totem

[Totem](http://www.gnome.org/projects/totem/) adalah pemutar film resmi _desktop environment_ (DE) GNOME berbasis `xine-lib` atau GStreamer (`gstreamer` otomatis terpasang saat memilih paket arch `totem`). Fiturnya meliputi _playlist_, _full-screen mode_, _seek_, kontrol volume, dan navigasi _keyboard_. Fungsi tambahannya antara lain:

*   _Video thumbnailer_ untuk _file manager_.
*   GNOME Files properties tab.
*   _Plugin_ Epiphany / Mozilla (Firefox) untuk menampilkan film di peramban Web.
*   Perangkat Webcam (sedang dalam pengembangan).

Totem-xine masih menjadi pilihan terbaik untuk menonton DVD.

Totem bagian dari kelompok `gnome-extra`; sedangkan Plugin Totem webbrowser bukan bagian kelompok tersebut.

Untuk memasangnya secara terpisah:

 `pacman -S totem` 

Untuk memasang _plugin_ Totem webbrowser:

 `pacman -S totem-plugin` 

#### KDE

##### Kaffeine

Kaffeine adalah pilihan yang baik untuk pengguna KDE. Untuk memasangnya, ketikkan:

```
pacman -S kaffeine

```

### Pemutar Audio

#### GNOME/Xfce

##### Exaile

[Exaile](/index.php/Exaile "Exaile") adalah pemutar musik yang ditulis dengan Python dan membutuhkan GTK+ toolkit.

##### Rhythmbox

[Rhythmbox](http://www.gnome.org/projects/rhythmbox/) adalah aplikasi pengelola musik yang terintegrasi, aslinya diinspirasi oleh iTunes milik Apple. Perangkat ini bebas/gratis, didesain untuk befungsi di desktop GNOME, dan berbasis GStreamer.

Rhythmbox memiliki beberapa fitur, diantaranya:

*   _Music browser_ yang mudah digunakan.
*   _Searching_ dan _sorting_.
*   Dukungan format audio yang komprehensif melalui GStreamer.
*   Dukungan radio Internet.
*   Playlists.

Untuk memasang `rhythmbox`:

 `pacman -S rhythmbox` 

Pemutar audio yang baik lainnya: Banshee, Quodlibet, dan Listen. Lihat [Gnomefiles](http://gnomefiles.org/) untuk membandingkannya.

#### KDE

##### Amarok

[Amarok](http://amarok.kde.org/) adalah salah satu sistem pustaka pemutar audio dan musik terbaik untuk KDE. Untuk memasangnya, ketikkan kode di bawah:

 `pacman -S amarok-base` 

#### Console

Moc adalah pemutar audio berbasis _ncurses_ untuk _console_; opsi lain yang cukup baik ada mpd.

Pilihan menarik lainnya [cmus](http://freshmeat.net/projects/cmus/).

#### Yang berbasis X lainnya

(TODO) Xmms, audacious, bmpx.

### Codec dan tipe konten multimedia

#### DVD

Kamu dapat menggunakan `totem-xine`, `mplayer` atau `kaffeine` (3 terbaik) untuk menonton DVD. Yang masih kurang hanya `libdvdcss`. Perhatikan bahwa paket ini mungkin ilegal di beberapa negara.

#### Flash

Pasang `flashplugin` dengan

 `pacman -S flashplugin` 

untuk mengaktifkan fitur Macromedia (sekarang Adobe) Flash di peramban Web kamu.

#### Quicktime

_Codec_ Quicktime sudah termasuk di paket `codec`. Cukup ketikkan

 `pacman -S codecs` 

untuk memasangnya.

#### Realplayer

_Codec_ untuk Realplayer 9 ada di dalam paket `codec`. Cukup ketikkan

 `pacman -S codecs` 

untuk memasangnya. Realplayer 10 tersedia dalam bentuk paket binari untuk Linux. Kamu bisa memperolehnya dari AUR [di sini](https://aur.archlinux.org/packages.php?do_Details=1&ID=1590&O=0&L=0&C=0&K=realplay&SB=&SO=&PP=25&do_MyPackages=0&do_Orphans=0&SeB=nd).

### Membakar (_Burning_) CD dan DVD

#### GNOME

##### Brasero

[Brasero](http://www.gnome.org/projects/brasero/) adalah sebuah aplikasi untuk membakar (_burn_) CD/DVD di desktop GNOME. Didesain sesederhana mungkin dan memiliki fitur unik yang memungkinkan pengguna untuk membuat cakram/disk dengan mudah dan cepat.

Untuk memasangnya, ketikkan:

 `pacman -S brasero` 

#### KDE

##### K3b

K3b - **B**urn, **B**aby, **B**urn in **K**DE

* * *

[K3B](http://k3b.plainblack.com/) - aplikasi pembakar CD/DVD untuk Linux - dioptimalkan untuk KDE - di bawah lisensi GPL. Untuk memasangnya, ketikkan:

 `pacman -S k3b` 

(Todo) cdrecord, graveman...

Kebanyakan pembakar CD tersedia dalam `cdrecord`:

 `pacman -S cdrkit` 

Jika kamu memasang aplikasi pembakar CD/DVD seperti Brasero atau K3B, pustakanya, seperti `libburn` atau `cdrkit`, akan terpasang pula.

Perangkat pembakar DVD yang baik adalah `growisofs`:

 `pacman -S dvd+rw-tools` 

### TV-Cards

Masih banyak yang harus dilakukan jika kamu ingin menonton TV di Linux (Arch). Tugas yang paling penting adalah menemukan chip mana yang tuner kamu gunakan. Bagaimanapun, dukungan tetap diberikan. Pastikan mengecek Basisdata Perangkat Keras (_Hardware Database_) (misal [TV Cards](http://en.opensuse.org/HCL/TV_Cards) di openSUSE). Setelah kamu mengetahui modelnya, tinggal sedikit lagi langkah yang dibutuhkan.

Pada kebanyakan kasus, kamu akan membutuhkan _bttv-drivers_ (_driver_ lain tersedia, lihat [drivers](http://linux.bytesex.org/v4l2/drivers.html)) beserta module I2C. Konfigurasikan perangkat di atas sesuai petunjuk masing-masing. Jika kamu beruntung, coba lakukan

 `modprobe bttv` 

akan mendeteksi otomatis perangkat kamu (cek `dmesg` untuk melihat hasilnya). Pada kasus tersebut, kamu tinggal memasang aplikasi untuk menonton TV. Kita akan meninjaunya belakangan. Jika deteksi otomatis tidak berhasil, cek berkas CARDLIST, yang ada di _tarball_ dari [bttv](http://dl.bytesex.org/releases/video4linux/) untuk menemukan parameter yang tepat bagimu. PV951 tanpa dukungan radio akan membutuhkan pemanggilan fungsi berikut:

 `modprobe bttv card=42 radio=0` 

Beberapa kartu memerlukan baris berikut untuk memunculkan suaranya:

 `modprobe tvaudio` 

Semua itu bervariasi. Jadi, cobalah. Beberapa kartu yang lain membutuhkan:

 `modprobe tuner` 

_Trial-and-error_ memang.

TODO: klarifikasi prosedur instalasi.

Untuk benar-benar menonton TV, pasang paket `xawtv`

 `pacman -S xawtv` 

baca halaman manualnya.

TODO: klarifikasi beberapa masalah dan prosedur. Introduksi XAWTV di halaman yang lain?

### Kamera Digital

Kebanyakan kamera digital terbaru didukung oleh perangkat _USB mass storage_, sehingga cukup menancapkannya lalu kopi/salin berkas gambar/foto yang ada. Kamera yang lebih lawas mungkin membutuhkan PTP (_Picture Transfer Protocol_) yang memerlukan _special driver_. gPhoto2 menyediakan _driver_ ini dan memungkinkan transfer gambar berbasis shell; `digikam` (untuk KDE) dan `gthumb` (untuk GNOME, `gtkam` opsi lainnya) menggunakan _driver_ ini dan memiliki antarmuka yang menarik.

### USB Memory Sticks / Hard Disks

_USB Memory Sticks_ dan _hard disks_ didukung langsung oleh _USB mass storage_ dan akan muncul sebagai _SCSI device_ (`/dev/sdX`). Jika kamu menggunakan KDE atau GNOME, kamu sebaiknya memakai `dbus` dan `hal` (tambahkan fungsi itu ke _daemons_ di berkas `/etc/rc.conf`), dan perangkat tersebut akan di-_mount_ otomatis. Jika kamu memakai DE yang berbeda, coba gunakan `ivman`.

## Memelihara sistem

### Pacman

[Pacman](/index.php/Pacman "Pacman") adalah pengelola kedua jenis paket--binari dan kode sumber--yang mampu mengunduh, memasang, dan _upgrade_ paket dari _remote_ dan repositori lokal dengan penanganan dependensi otomatis, dan peranti yang mudah dipahami untuk membuat paket kamu sendiri.

Deskripsi lebih detail tentang Pacman dapat ditemukan di [artikel ini](/index.php/Pacman "Pacman").

#### Perintah yang bermanfaat

Untuk sinkronisasi dan _update_ basisdata paket lokal dengan _remote_ repositories _(hal ini sebaiknya dilakukan sebelum memasang (_installing_) dan_ upgrading _paket):_

 `pacman -Sy` 

Untuk **upgrade** semua paket di sistem:

 `pacman -Su` 

Untuk sinkronisasi, _update_, dan **upgrade** semua paket di sistem dengan satu perintah:

 `pacman -Syu` 

Untuk memasang atau **upgrade** sebuah paket tunggal atau sejumlah paket (termasuk dependensinya):

 `pacman -S paketA paketB` 

Untuk menghapus sebuah paket tunggal, tapi membiarkan dependensinya terpasang:

 `pacman -R package` 

Untuk menghapus sebuah paket dan semua dependensinya yang tidak dipakai oleh tiap paket yang masih terpasang:

 `pacman -Rs package` 

Untuk menghapus semua dependensi paket yang tidak dibutuhkan dan tidak perlu membuat salinan setelannya:

 `pacman -Rsn package` 

Untuk menelusuri daftar basisdata paket di _remote (repo)_ berdasar kata kunci tertentu:

 `pacman -Ss keyword` 

Untuk mengurutkan (_query_) semua paket di sistem kamu:

 `pacman -Q` 

Untuk menelusuri paket basisdata lokal (di mesin kamu) untuk kata kunci tertentu:

 `pacman -Q package` 

Untuk menelusuri basisdata paket lokal (di mesin kamu) untuk kata kunci tertentu dan mengurutkan semua informasi terkait:

 `pacman -Qi package` 

Untuk _defragment_ _cache_ basisdata `pacman` dan mengoptimalkan kecepatannya:

 `pacman-optimize` 

Untuk menghitung jumlah paket yang ada di sistem kamu saat ini:

 `pacman -Q | wc -l` 

Untuk memasang paket yang dikompilasi dari kode sumber memakai ABS dan `makepkg`:

 `pacman -U packagename.pkg.tar.gz` 

Catatan: Terdapat banyak fungsi dan perintah tambahan yang tak terhitung jumlahnya bagi `pacman`. Coba `man pacman` dan masukan wiki [pacman](/index.php/Pacman "Pacman").

## Informasi Lebih Lanjut

Jika setelah membaca ini kamu ingin sedikit memolesnya lagi, silakan menuju [Post Installation Tips](/index.php/Post_Installation_Tips "Post Installation Tips"). Untuk bantuan dan informasi lebih lanjut, kamu bisa menuju ke [Halaman utama Linux Arch](https://www.archlinux.org), menelusuri [wiki](https://wiki.archlinux.org/index.php/), [forum](https://bbs.archlinux.org), [IRC channel](/index.php/ArchChannel "ArchChannel"), dan [_mailing lists_](https://www.archlinux.org/mailman/listinfo/).