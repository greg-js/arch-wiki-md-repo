**Tip:** This is part of a multi-page article for The Beginners' Guide. **[Click here](/index.php/Beginners%27_Guide_(Indonesia) "Beginners' Guide (Indonesia)")** if you would rather read the guide in its entirety.

## Contents

*   [1 Persiapan](#Persiapan)
    *   [1.1 Dapatkan media instalasi terbaru Archlinux](#Dapatkan_media_instalasi_terbaru_Archlinux)
        *   [1.1.1 Memeriksa integritas dari file yang diunduh](#Memeriksa_integritas_dari_file_yang_diunduh)
        *   [1.1.2 Install melalui jaringan](#Install_melalui_jaringan)
*   [2 Menyiapkan File Installasi](#Menyiapkan_File_Installasi)
    *   [2.1 Installasi menggunakan CD](#Installasi_menggunakan_CD)
    *   [2.2 Installasi menggunakan Flashdisk atau USB drive lainnya](#Installasi_menggunakan_Flashdisk_atau_USB_drive_lainnya)
        *   [2.2.1 Menggunakan sistem operasi seperti *nix](#Menggunakan_sistem_operasi_seperti_.2Anix)
        *   [2.2.2 Menggunakan sistem operasi windows](#Menggunakan_sistem_operasi_windows)
*   [3 Memulai proses Installasi Archlinux](#Memulai_proses_Installasi_Archlinux)
    *   [3.1 Boot dari Media](#Boot_dari_Media)
    *   [3.2 Sistem Mulai OS](#Sistem_Mulai_OS)
    *   [3.3 Merubah keymap](#Merubah_keymap)
    *   [3.4 Dokumentasi](#Dokumentasi)

## Persiapan

**Note:** Jika Anda ingin menginstall Archlinux dipartisi lain karena sebelumnya sudah ada distro GNU/Linux yang terinstall atau Anda ingin membuat Archlinux LiveCD,silahkan lihat artikel berikut untuk mengetahui caranya.Lakukan hal tersebut jika Anda ingin menginstall Archlinux via VNC atau SSH.

Berikut adalah langkah-langkah installasi Archlinux :

### Dapatkan media instalasi terbaru Archlinux

Silahkan unduh Archlinux di [disini](https://archlinux.org/download/).Versi terbaru adalah **2015.11.01**.

*   File Archlinux baik yang "Core" maupun "Netinstall" hanyak menyediakan paket yang diperlukan saja guna membentuk **Sistem Dasar Archlinux**.Sebagai catatan,sistem dasar tidak mempunyai tampilan dengan grafis (GUI) dan hanya bersifat text-mode.Sistem dasar tersebut terdiri atas perangkat GNU (compiler, assembler, linker, libraries, shell, dan utilities), kernel linux, pacman (Manajer paket Arch) dan beberapa tambah file library dan modules.
*   "*Core images*" yang menyediakan penginstallan via CD dan jaringan.
*   Netinstall berukuran lebih kecil dan tidak mempunyai paket,karena semuanya akan diunduh via internet.
*   [Pertanyaan tentang Arch64](/index.php/Arch64_FAQ "Arch64 FAQ") akan membantu Anda dalam memilih antara versi 32bit dan 64bit.File installasi Archlinux sudah menyediakan versi 32bit dan 64bit sekaligus sehingga Anda dapat hemat kuota dan waktu.
*   Jangan lupa untuk mengunduh file checksum.txt bersamaan denan file ISO Archlinux yang sudah Anda unduh.

Versi pra-rilis dari Archlinux juga dapat Anda unduh [di sini](https://releng.archlinux.org/isos/).**Tapi yang itu tidaklah versi resmi dari Archlinux**."Versi tersebut hanya boleh digunakan jika Archlinux versi biasa tidak berkerja dengan perangkat Anda yang sekarang.

#### Memeriksa integritas dari file yang diunduh

Silahkan masuk kelokasi folder tempat Anda menyimpan file Archlinux dengan mengetik perintah `cd /lokasi/foldernya` dan ketikkan perintah `sha1sum`:

 `$ sha1sum --check file_checksum.txt nama_file_archlinux.iso` 

Perintah tersebut akan memunculkan pesan "Ok" jika berhasil,jika tidak maka Anda harus mengunduh ulang file ISO Archlinux. Cara tersebut juga dapat diterapkan untuk verifikasi md5sum.

#### Install melalui jaringan

Selain dengan cara menggunakan CD atau USB drive,Anda juga dapat boot ke file .iso Archlinux via jaringan.Cara ini akan bekerja maksimal jika Anda sudah menyiapkan server.Silahkan lihat [artikel ini](/index.php/Install_Arch_from_network_(via_PXE) "Install Arch from network (via PXE)") untuk info lebih lanjut,dan selanjutnya [instalasi booting ke Archlinux](#Boot_Arch_Linux_Installer).

## Menyiapkan File Installasi

### Installasi menggunakan CD

Silahkan "bakar/burn" file .iso Archlinux ke CD atau DVD dan lanjutkan dengan [booting ke instalasi Archlinux](#Boot_Arch_Linux_Installer).

**Note:** Optical drive mempunyai kualitas yang bervariasi.Umumnya,kecepatan "burn" yang lambat lebih baik.Beberapa pengguna menyarankan kecepatan "burn" sebesar "4x atau 2x".Jika terjadi hal yang tidak biasa,coba "burn" kembali dengan kecepatan yang lebih rendah.

### Installasi menggunakan Flashdisk atau USB drive lainnya

Lihat [cara menginstall Archlinux via USB drive](/index.php/Install_from_a_USB_flash_drive "Install from a USB flash drive") untuk info lebih lanjut.

Secara umum USB drive seperti flashdisk,card reader dll bisa digunakan dan dikenali oleh BIOS untuk keperluan booting.

**Perlu diingat,semua data yang ada di USB driver akan dihapus!**

#### Menggunakan sistem operasi seperti *nix

**Warning:** Berhati-hatilah saat memilih media USB yang akan digunakan,karena `dd` akan mengikuti semua perintah yang diketikkan meskipun hal tersebut akan merusak sistem Anda terutama hardisk.Jadi berhati-hatilah saat memilih lokasi USB yang akan digunakan.

Colokkan ke port USB flashdisk atau USB drive yang sudah diformat sebelumnya,tentukanan lokasinya seperti di "F:/" atau di "/dev/sdb1" dan pasang file .iso Archlinux kesana menggunakan `dd` dengan perintah :

 `# dd if=archlinux-2011.08.19-''{core|netinstall}''-''{i686|x86_64|dual}''.iso of=/dev/sd''x''` 

Keterangan : `if=` merupakan lokasi folder file ISO dan `of=` merupakan lokasi USB drive Anda.Pastikan untuk mengetik `/dev/sd**x**` dan tidak `/dev/sd**x1**`.Anda membutuhkan ruang kosong yang cukup banyak pada USB drive,

Untuk memastikan bahwa file ISO nya berhasil dipasang di USB drive,catat banyak record (blocks) yang dapat dibaca dan ditulis dengan mengetik perintah dibawah ini :

 ` # dd if=/dev/sd''x'' count=''number_of_records'' status=noxfer | md5sum` 

Md5sum akan menghasilkan angka yang sama dengan [isi file md5sums.txt](https://www.archlinux.org/iso/2011.08.19/md5sums.txt).Secara lebih spesifik,hasilnya adalah :

Write .iso to drive

 `$ [sudo] dd if=archlinux-2011.08.19-core-i686.iso of=/dev/sdc` 
```
 744973+0 records in
 744973+0 records out
 381426176 bytes (381 MB) copied, 106.611 s, 3.6 MB/s

```

Verify integrity:

 `$ [sudo] dd if=/dev/sdc count=744973 status=noxfer | md5sum` 
```
 4850d533ddd343b80507543536258229  -
 744973+0 records in
 744973+0 records out
```

Lanjutkan dengan [booting ke Arch installer](#Boot_Arch_Linux_Installer)

#### Menggunakan sistem operasi windows

Unduh Disk Imager dari [sini](https://launchpad.net/win32-image-writer/+download).Colokkan USB drive,jalankan Disk Imager dan pilih file ISO Archlinux (Disk Imager hanya mengenal file *.img,jadi Anda harus menggantinya dengan "*.iso" dikotak dialog yang muncul).Kemudian pilih lokasi USB drive kamu (seperti "F:/")dan klik "Write".

Ada juga solusi lain untuk [menulis file ISO untuk booting](/index.php/Install_from_a_USB_flash_drive#On_Windows "Install from a USB flash drive").Jika ada masalah,coba cabut dan pasang USB drive nya di port lain.

Kemudia lanjut dengan [booting ke Archlinux installer](#Boot_Arch_Linux_Installer).

## Memulai proses Installasi Archlinux

**Tip:** Pastikan Anda mempunyai minimal 64Mb RAM.

**Tip:** Selama proses tersebut,layar otomatis kosong bisa terjadi . Jika demikian, anda dapat menekan tombol Alt untuk mendapatkan tampilan normal dengan aman.

### Boot dari Media

Masukkan CD atau media flashdisk yang sudah anda siapkan , dan boot dari sana. Anda mungkin harus mengubah urutan boot pada BIOS komputer Anda. Untuk melakukan ini, Anda harus menekan tombol (biasanya DEL, F1, F2, F11 atau F12) selama fase POST BIOS (Power On Self-Test).

**Menu Utama:** Menu utama seharusnya ditampilkan pada saat ini. Pilih pilihan yang lebih disukai dengan menggunakan tombol panah untuk menyorot pilihan Anda, dan kemudian dengan menekan [Enter]. Menu sedikit berbeda di antara ISO yang berbeda.

### Sistem Mulai OS

Pilih "Boot Arch Linux" dari Main Menu dan tekan [Enter], untuk memulai dengan instalasi. Sistem sekarang akan memuat dan menyajikan sebuah shell prompt. Anda akan otomatis login sebagai root.

**Catatan:** Pengguna yang mencari untuk melakukan instalasi Arch Linux jarak jauh melalui koneksi ssh didorong untuk membuat beberapa tweak pada titik ini untuk mengaktifkan koneksi ssh langsung ke lingkungan live CD. Jika tertarik, lihat Artikel [Install dari SSH](/index.php?title=Install_dari_SSH&action=edit&redlink=1 "Install dari SSH (page does not exist)").

Jika menggunakan chipset Intel video dan layar menjadi kosong selama proses boot, masalahnya adalah kemungkinan besar masalah dengan pengaturan modus kernel. Sebuah solusi yang mungkin dapat dicapai dengan me-reboot dan menekan <Tab> di menu GRUB untuk memasukkan opsi kernel. Pada akhir baris kernel, tambahkan spasi dan kemudian:

```
i915.modeset=0

```

Atau, tambahkan:

```
video=SVIDEO-1:d

```

yang (jika bekerja) tidak akan menonaktifkan pengaturan modus kernel.

Setelah selesai membuat perubahan untuk setiap perintah menu, cukup tekan "Enter" untuk boot dengan pengaturan itu.

Lihat artikel [Intel](/index.php/Intel "Intel") untuk informasi lebih lanjut.

### Merubah keymap

Jika Anda memiliki tata letak keyboard non-US Anda dapat memilih keymap / font konsol Anda secara interaktif dengan perintah:

 `# km` 

atau menggunakan perintah loadkeys:

 `# loadkeys *layout*` 

dimana *layout* adalah layout keyboard Anda seperti `id` atau `be-latin1`

### Dokumentasi

Panduan penginstalan resmi yang nyaman tepat tersedia pada saat sistem hidup! Untuk mengaksesnya, ubah ke tty2 (konsol virtual # 2) dengan <ALT> + F2, login sebagai "root" dan kemudian jalankan `/usr/bin/less`dengan mengetikkan di bagian # berikut ini:

 `# less /usr/share/aif/docs/official_installation_guide_en` 

`less` akan memungkinkan Anda untuk membuka halaman demi halaman dokumen.

Ubah kembali ke tty1 dengan <ALT>+F1 untuk mengikuti sisa proses instalasi. (Ubah kembali ke tty2 setiap waktu jika Anda perlu referensi Panduan Resmi selagi Anda melalui proses instalasi.)

**Tip:** Harap dicatat bahwa panduan resmi hanya mencakup instalasi dan konfigurasi sistem dasar. Setelah itu terinstal, sangat disarankan agar Anda kembali ke sini ke wiki untuk mengetahui lebih lanjut tentang pasca-instalasi pertimbangan dan isu-isu terkait lainnya.

**[Panduan Pemula](/index.php/Beginners%27_Guide_(Indonesia) "Beginners' Guide (Indonesia)")**

* * *

[Preface](/index.php/Beginners%27_Guide/Preface_(Indonesia) "Beginners' Guide/Preface (Indonesia)") >> **Preparation** >> [Installation](/index.php?title=Beginners%27_Guide/Installation_(Indonesia)&action=edit&redlink=1 "Beginners' Guide/Installation (Indonesia) (page does not exist)") >> [Post-Installation](/index.php?title=Beginners%27_Guide/Post-Installation_(Indonesia)&action=edit&redlink=1 "Beginners' Guide/Post-Installation (Indonesia) (page does not exist)")