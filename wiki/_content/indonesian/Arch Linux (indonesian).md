## Contents

*   [1 Apakah Arch Linux?](#Apakah_Arch_Linux.3F)
*   [2 Kelebihan](#Kelebihan)
*   [3 Manajemen Paket yang Unik](#Manajemen_Paket_yang_Unik)
*   [4 Modernitas](#Modernitas)
*   [5 Simple](#Simple)
*   [6 Lebih Jauh](#Lebih_Jauh)

## Apakah Arch Linux?

Arch Linux (atau Arch) adalah sebuah distro i686/x86-64 yang dikembangkan secara independen berdasarkan model paket rolling-release. Pendekatan desain pengembang distro ini berfokus pada minimalisme, keanggunan kode, kebenaran program dan modernitas. Versi 0.1 (Homer) telah dirilis pada 11 Maret 2002.

## Kelebihan

Arch menyajikan lingkungan instalasi yang sederhana (tanpa GUI), dikompilasi untuk arsitektur i686/x86-64\. Arch itu ringan, fleksibel, dan simpel. Filosofi desain dan implementasinya membuatnya mudah untuk dikembangkan dan dibentuk menjadi sistem apapun yang Anda buat--dari konsol minimalis hingga desktop mewah yang kaya fitur. Daripada nantinya harus membuang paket-paket yang tidak diinginkan. Arch menyediakan *power user* kemampuan untuk membangun sistem dari dasar tanpa konfigurasi apapun.

## Manajemen Paket yang Unik

Arch menggunakan sistem paket binary yang mudah digunakan ([pacman](/index.php/Pacman "Pacman")) yang mengizinkan anda untuk mengupgrade sistem dengan satu perintah. Pacman dibangun dengan bahasa **C** dan didesain untuk ringan dari bawah hingga ke ujung atas untuk menjadi ringan, simple, dan sangat cepat. Arch juga menyediakan sistem pemaketan yang ports-like ([Arch Build System](/index.php/Arch_Build_System "Arch Build System")) untuk memudahkan membuat paket dan menginstal paket dari kode sumber, dan bisa disinkronisasikan dengan satu perintah. Bahkan anda juga dapat membangun kembali sistem anda dengan satu perintah. Semuanya dilakukan dengan sangat mudah dan transparan. Model rolling release memungkinkan satu kali instalasi kemudian upgrade berkesinambungan, tanpa pernah harus melakukan instalasi ulang atau upgrade besar-besaran dari satu versi ke berikutnya.

## Modernitas

Arch Linux berusaha untuk menyediakan versi stabil terbaru dari perangkat lunak berdasarkan sistem rolling-release. Saat ini kami mendukung set paket *core* untuk sistem dasar i686 dan x86-64, ribuan tambahan, paket binary berkualitas tinggi dari pengembang dan repositori pengguna, serta ribuan *script* PKGBUILD untuk membangun dan memaketkan dari kode sumber. Arch menyediakan software vanilla, *non-patched*; paket-paket yang ditawarkan adalah murni dari *upstream*, sebagaimana awalnya itu ditujukan untuk didistribusikan. *Patch* hanya terjadi dalam beberapa kasus, untuk mencegah kerusakan parah. Contohnya ketidakcocokan versi yang mungkin terjadi dalam model rolling release. Arch juga menyediakan fitur-fitur baru yang tersedia untuk pengguna GNU/Linux, termasuk *filesystem* modern (Ext2/3/4, Reiser, XFS, JFS), LVM2/EVMS, software RAID, dukungan udev dan initcpio, serta kernel terbaru.

## Simple

[The Arch Way](/index.php/The_Arch_Way "The Arch Way") adalah filosofi yang bertujuan untuk tetap *simple*. Sistem dasar Arch Linux sangatlah minimal, lingkungan GNU/Linux yang fungsional; kernel Linux, GNU *toolchain*, dan berberapa *utility* seperti **links** dan **Vi**. Titik awal yang bersih dan *simple* ini adalah dasar yang baik untuk selanjutnya dikembangkan sesuai kemauan pengguna.

Sistem *init* milik Arch terinspirasi dari BSD yang mengatur *init* dari sebuah berkas/file, (`/etc/rc.conf`), dibandingkan struktur direktori rumit yang berisi banyak *symlink* untuk setiap *runlevel*.

Konfigurasi sistem dapat dilakukan dengan mengubah *file-file* teks sederhana.

## Lebih Jauh

Homepage Arch berada di [https://www.archlinux.org/](https://www.archlinux.org/) dimana anda bia menemukan tautan ke forum pengguna, dokumentasi resmi, dan segalanya tentang Arch. Anda juga dapat membaca [The Arch Way](/index.php/The_Arch_Way "The Arch Way") untuk lebih dalamnya tentang Arch.