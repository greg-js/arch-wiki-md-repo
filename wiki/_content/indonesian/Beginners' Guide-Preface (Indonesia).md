## Contents

*   [1 Pendahuluan](#Pendahuluan)
    *   [1.1 Pendahuluan](#Pendahuluan_2)
    *   [1.2 Lisensi](#Lisensi)
    *   [1.3 Cara Arch](#Cara_Arch)
    *   [1.4 Tentang Panduan Ini](#Tentang_Panduan_Ini)

## Pendahuluan

### Pendahuluan

Selamat Datang. Dokumen ini akan memandu Anda melalui proses instalasi [Arch Linux](/index.php/Arch_Linux "Arch Linux"): sederhana, distribusi [GNU](/index.php/GNU_Project "GNU Project")/ Linux ringan yang ditargetkan kepada para pengguna berkompeten. Panduan ini ditujukan kepada para pengguna baru Arch, tetapi tidak menutup kemungkinan untuk dijadikan sebagai referensi yang kuat dan berbasis informatif untuk semua.

Sebelum menginstal, Anda disarankan untuk menuju ke [FAQ](/index.php/FAQ "FAQ").

**Garis Besar Distribusi Arch Linux:**

*   [Sederhana](/index.php/The_Arch_Way "The Arch Way") secara desain dan filosofi
*   [Semua paket](https://www.archlinux.org/packages/?q=) dikompilasi untuk arsitektur [i686](https://en.wikipedia.org/wiki/P6_(microarchitecture) "wikipedia:P6 (microarchitecture)") dan [x86_64](https://en.wikipedia.org/wiki/x86-64 "wikipedia:x86-64")
*   [Rolling-release](https://en.wikipedia.org/wiki/Rolling_release "wikipedia:Rolling release") model, memungkinkan instalasi satu kali dan upgrade tanpa batas ke versi stabil yg terbaru dari perangkat lunak yang diinstal
*   Init script [Gaya BSD](/index.php/Arch_boot_process "Arch boot process"), menampilkan satu file konfigurasi terpusat
*   [mkinitcpio](/index.php/Mkinitcpio "Mkinitcpio") yang sederhana dan dinamis sebagai pembuat [initramfs](https://en.wikipedia.org/wiki/initrd "wikipedia:initrd")
*   [manajer paket](https://en.wikipedia.org/wiki/Package_manager "wikipedia:Package manager") [Pacman](/index.php/Pacman "Pacman") yang ringan dan cerdas, dengan jejak memori yang sangat sederhana
*   [Arch Build System](/index.php/Arch_Build_System "Arch Build System"): sistem pembuat paket yang ports-like, menyediakan framework sederhana untuk membuat paket Arch yang mudah diinstal dari source
*   [Arch User Repository](/index.php/Arch_User_Repository "Arch User Repository"): menawarkan ribuan build scripts hasil kontribusi pengguna dan kesempatan untuk berbagi hasil kreasi Anda

### Lisensi

Arch Linux, pacman, dokumentasi, dan skrip adalah Hak Cipta © 2002-2007 oleh Judd Vinet, Copyright © 2007-2011 oleh Aaron Griffin dan berlisensi di bawah [GNU General Public License Version 2](http://www.gnu.org/licenses/old-licenses/gpl-2.0.html).

### Cara Arch

_**Prinsip-prinsip desain di balik Arch bertujuan menjaganya tetap [sederhana](/index.php/The_Arch_Way "The Arch Way").**_

'Sederhana', dalam konteks ini, berarti 'tanpa tambahan yang tidak perlu, modifikasi, atau komplikasi'. Singkatnya, pendekatan yg elegan dan minimalis.

**Beberapa pemikiran yang perlu diingat ketika Anda mempertimbangkan kesederhanaan:**

*   _" 'Sederhana' didefinisikan dari sudut pandang teknis, bukan sudut pandang kegunaan. Lebih baik secara teknis elegan dengan kurva belajar yang lebih tinggi, daripada menjadi mudah digunakan dan [inferior] secara teknis ." —**Aaron Griffin**_
*   _Entia non sunt multiplicanda praeter necessitatem_ atau "Entities should not be multiplied unnecessarily." —**Occam's razor**. Dalam hal ini Razor merujuk pada tindakan pemangkasan komplikasi hal yang tak diperlukan demi mencapai penjelasan yang sederhana, baik teori maupun metoda.
*   _"Bagian luar biasa [metode saya] terletak pada kesederhanaan .. Ketinggian budidaya selalu berarah pada kesederhanaan."_ — **Bruce Lee**

### Tentang Panduan Ini

[Arch wiki](/index.php/Main_page "Main page") yang diasuh oleh komunitas ini adalah sumber pertama yang tepat untuk konsultasi masalah. Kanal [IRC](https://en.wikipedia.org/wiki/IRC "wikipedia:IRC") ([irc://irc.freenode.net/#archlinux](irc://irc.freenode.net/#archlinux)), dan [forum](https://bbs.archlinux.org/) juga tersedia bila belum menemukan jawaban. Dan jangan lupa untuk merujuk pada halaman `man` untuk setiap perintah yang belum familiar; ini biasanya dapat diakses dengan `man _command_`.

**Catatan:** Panduan berikut merupakan hal penting dalam rangka konfigurasi dan penginstalan sistem Arch Linux yang baik dan benar, jadi _tolong_ baca ini dengan seksama. Sangat disarankan untuk membaca secara menyeluruh <u>sebelum</u> mengeksekusi perintah-perintah yang tertera.

Panduan ini terbagi menjadi tiga komponen utama:

*   [Part I: Persiapan](/index.php/Beginners%27_Guide/Preparation#Preparation "Beginners' Guide/Preparation")
*   [Part II: Instalasi](/index.php/Beginners%27_Guide/Installation#Installation "Beginners' Guide/Installation")

**[Panduan Pemula](/index.php/Beginners%27_Guide_(Indonesia) "Beginners' Guide (Indonesia)")**

* * *

**Preface** >> [Preparation](/index.php/Beginners%27_Guide/Preparation_(Indonesia) "Beginners' Guide/Preparation (Indonesia)") >> [Installation](/index.php?title=Beginners%27_Guide/Installation_(Indonesia)&action=edit&redlink=1 "Beginners' Guide/Installation (Indonesia) (page does not exist)") >> [Post-Installation](/index.php?title=Beginners%27_Guide/Post-Installation_(Indonesia)&action=edit&redlink=1 "Beginners' Guide/Post-Installation (Indonesia) (page does not exist)")