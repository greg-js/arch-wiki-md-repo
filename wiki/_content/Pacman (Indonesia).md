# Pacman (Indonesia)

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

<table style="margin-left: 5px; padding: 5px; border-spacing: 0px 4px; float: right; clear: right; width: 25%;" cellpadding="0">

<tbody>

<tr style="text-align: center; border-bottom: 5px #08c solid;">

<th style="background: #333; color: white; padding: 3px;">**Summary** <sup>[help replacing me](/index.php/Help_talk:Style/Article_summary_templates#Replacing_Article_summaries_with_Related_articles "Help talk:Style/Article summary templates")</sup></th>

</tr>

<tr>

<td style="text-align: left; padding: 3px">pacman adalah manajer paket Arch Linux. Manajer paket digunakan untuk memasang, mengupgrade, dan menghapus perangkat lunak. Artikel ini mencakup penggunaan dasar dan tips untuk mengatasi masalah.</td>

</tr>

<tr style="text-align: center; height: 1.5em; border-bottom: 5px #08c solid;">

<th style="background: #333; color: white; padding: 2px;">**Overview**</th>

</tr>

<tr>

<td style="text-align: left; padding: 3px">Packages in Arch Linux are built using [makepkg](/index.php/Makepkg "Makepkg") and a custom build script for each package (known as a [PKGBUILD](/index.php/PKGBUILD "PKGBUILD")). Once packaged, software can be installed and managed with [pacman](/index.php/Pacman "Pacman"). PKGBUILDs for software in the [official repositories](/index.php/Official_repositories "Official repositories") are available from the [ABS](/index.php/Arch_Build_System "Arch Build System") tree; thousands more are available from the (unsupported) [Arch User Repository](/index.php/Arch_User_Repository "Arch User Repository").</td>

</tr>

<tr style="text-align: center; height: 1.5em; border-bottom: 5px #08c solid;">

<th style="background: #333; color: white; padding: 2px;">**Related**</th>

</tr>

<tr>

<td style="text-align: left; padding: 3px">[Downgrading Packages](/index.php/Downgrading_Packages "Downgrading Packages")</td>

</tr>

<tr>

<td style="text-align: left; padding: 3px">[Improve Pacman Performance](/index.php/Improve_Pacman_Performance "Improve Pacman Performance")</td>

</tr>

<tr>

<td style="text-align: left; padding: 3px">[pacman GUI Frontends](/index.php/Pacman_GUI_Frontends "Pacman GUI Frontends")</td>

</tr>

<tr>

<td style="text-align: left; padding: 3px">[pacman Rosetta](/index.php/Pacman_Rosetta "Pacman Rosetta")</td>

</tr>

<tr>

<td style="text-align: left; padding: 3px">[pacman Tips](/index.php/Pacman_Tips "Pacman Tips")</td>

</tr>

<tr style="text-align: center; height: 1.5em; border-bottom: 5px #08c solid;">

<th style="background: #333; color: white; padding: 2px;">**Resources**</th>

</tr>

<tr>

<td style="text-align: left; padding: 3px">[libalpm(3) Manual Page](https://www.archlinux.org/pacman/libalpm.3.html)</td>

</tr>

<tr>

<td style="text-align: left; padding: 3px">[pacman(8) Manual Page](https://www.archlinux.org/pacman/pacman.8.html)</td>

</tr>

<tr>

<td style="text-align: left; padding: 3px">[pacman.conf(5) Manual Page](https://www.archlinux.org/pacman/pacman.conf.5.html)</td>

</tr>

<tr>

<td style="text-align: left; padding: 3px">[repo-add(8) Manual Page](https://www.archlinux.org/pacman/repo-add.8.html)</td>

</tr>

</tbody>

</table>

Manajer paket **[pacman](https://archlinux.org/pacman/)** adalah salah satu fitur utama dari Arch Linux. Menggabungkan sebuah format paket biner sederhana dengan sebuah sistem pembangunan yang mudah digunakan (lihat [makepkg](/index.php/Makepkg "Makepkg") dan [Arch Build System](/index.php/Arch_Build_System "Arch Build System")). Tujuan dari pacman adalah memungkinkan pengaturan paket-paket dengan mudah, baik yang berasal dari repositori resmi Arch maupun yang dibangun sendiri oleh para pengguna.

pacman menjaga sistem tetap up to date dengan sinkronisasi daftar paket dengan server master. Model server/klien juga memungkinkan Anda untuk mengunduh/memasang paket dengan perintah sederhana, lengkap dengan semua dependensi yang diperlukan.

pacman ditulis dalam bahasa pemrograman C dan menggunakan format paket `.pkg.tar.xz`.

## Konfigurasi

Konfigurasi pacman terletak di `/etc/pacman.conf`. Di sinilah pengguna mengkonfigurasi program tersebut agar berjalan sesuai dengan yang diinginkan. Informasi mendalam tentang file konfigurasi dapat ditemukan di [man pacman.conf](https://www.archlinux.org/pacman/pacman.conf.5.html).

### Opsi Umum

Opsi-opsi umum terdapat di bagian `[options]`. Baca man page atau lihat di `pacman.conf` untuk informasi apa yang dapat dilakukan di sini.

Retrieved from "[https://wiki.archlinux.org/index.php?title=Pacman_(Indonesia)&oldid=413289](https://wiki.archlinux.org/index.php?title=Pacman_(Indonesia)&oldid=413289)"

[Categories](/index.php/Special:Categories "Special:Categories"):

*   [Package management (Indonesia)](/index.php/Category:Package_management_(Indonesia) "Category:Package management (Indonesia)")
*   [Utilities (Indonesia)](/index.php/Category:Utilities_(Indonesia) "Category:Utilities (Indonesia)")