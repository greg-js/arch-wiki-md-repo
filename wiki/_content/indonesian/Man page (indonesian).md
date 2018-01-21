**man pages**—singkatan untuk "halaman panduan" -adalah dokumentasi ekstensif yang telah terpasang dengan hampir semua substansial sistem operasi mirip-UNIX, termasuk Arch Linux. Perintah yang digunakan untuk menampilkannya adalah `man`.

Terlepas dari ruang lingkupnya, halaman panduan dirancang untuk menjadi dokumen serba lengkap,secara konsekuen membatasi dirinya untuk mengacu ke halaman panduan yang lain ketika membahas subjek terkait. Hal ini sangat kontras dengan info berkas *hyperlink-aware*, upaya GNU menggantikan format tradisional pada halaman panduan.

[less](/index.php/Core_utilities#less "Core utilities") adalah halaman bawaan yang digunakan dengan *man*.

## Contents

*   [1 Mengakses halaman panduan](#Mengakses_halaman_panduan)
*   [2 Format](#Format)
*   [3 Mencari panduan](#Mencari_panduan)
*   [4 Halaman panduan berwarna](#Halaman_panduan_berwarna)
*   [5 Lebar halaman dinamis](#Lebar_halaman_dinamis)
*   [6 Membaca halaman panduan lokal](#Membaca_halaman_panduan_lokal)
    *   [6.1 Mengonversi ke mode halaman HTML peramban](#Mengonversi_ke_mode_halaman_HTML_peramban)
        *   [6.1.1 mandoc](#mandoc)
        *   [6.1.2 man2html](#man2html)
        *   [6.1.3 man -H](#man_-H)
        *   [6.1.4 roffit](#roffit)
    *   [6.2 Mengonversi ke PDF](#Mengonversi_ke_PDF)
*   [7 Halaman Panduan berbasis Online](#Halaman_Panduan_berbasis_Online)
*   [8 Halaman panduan penting](#Halaman_panduan_penting)
*   [9 Lihat juga](#Lihat_juga)

## Mengakses halaman panduan

Untuk membaca halaman panduan, secara sederhana ketikkan:

```
$ man *nama_halaman*

```

Panduan-panduan diurutkan menjadi beberapa bagian. Untuk daftar lengkapnya, lihat bagian berjudul "Sections of the manual pages" in [man-pages(7)](https://jlk.fjfi.cvut.cz/arch/manpages/man/man-pages.7).

Halaman panduan biasanya dirujuk berdasarkan namanya, diikuti dengan jumlah bagiannya dalam tanda kurung. Sering kali ada beberapa halaman panduan dengan nama yang sama, seperti man(1) dan man(7). Dalam hal ini, memberikan nomor bagian pada man yang diikuti dengan nama halaman panduan, misalnya:

```
$ man 5 passwd

```

untuk membaca halaman manual pada `/etc/passwd`, darpiada utilitas `passwd`.

Deskripsi satu-baris (*one-line*) dari halaman panduan dapat ditampilkan dengan menggunakan perintah `whatis`. Misalnya, untuk penjelasan singkat dari bagian halaman panduan mengenai `ls`, ketik:

 `$ whatis ls` 
```
ls (1p)              - list directory contents
ls (1)               - list directory contents
```

## Format

Semua halaman panduan mengikuti format yang cukup standar, yang membantu dalam melakukan navigasi pada halaman panduan. Lihat bagian yang berjudul "Sections within a manual page" dalam [man-pages(7)](https://jlk.fjfi.cvut.cz/arch/manpages/man/man-pages.7).

## Mencari panduan

Walaupun utilitas `man` memungkinkan pengguna untuk menampilkan halaman panduan, dan mencari isinya melalui *less*, masalah muncul ketika pengguna mengetahui bahwa bukan nama yang tepat dari halaman panduan yang diinginkan! Untungnya, opsi `-k` atau opsi `--apropos` dapat digunakan untuk mencari deskripsi halaman panduan pada kasus kata kunci tertentu.

Fitur penelitian disediakan oleh *cache* yang didedikasikan. Secara bawaan, Anda mungkin tidak memiliki *cache* apapun yang dibangun dan semua pencarian Anda, akan memberi Anda hasil *nothing appropriate* (yang tidak tepat). Anda dapat membuat atau memperbarui *cache* dengan menjalankan perintah

```
# mandb

```

Anda harus menjalankan perintah tersebut, setiap kali halaman panduan baru terpasang.

Sekarang Anda dapat memulai pencarian Anda. Misal, untuk mencari halaman panduan yang berkaitan dengan "password":

```
$ man -k password

```

atau:

```
$ man --apropos password

```

Hal ini sama dengan memanggil perintah `apropos`:

```
$ apropos password

```

Kata kunci yang diberikan diinterpretasikan sebagai ekspresi reguler secara bawaan.

Jika Anda ingin melakukan pencarian yang lebih mendalam dengan menyesuaikan kata kunci yang ditemukan di seluruh artikel, Anda dapat menggunakan opsi `-K`:

```
$ man -K password

```

## Halaman panduan berwarna

Lihat [Color output in console#man](/index.php/Color_output_in_console#man "Color output in console").

## Lebar halaman dinamis

Lebar halaman panduan dikendalikan oleh variable konfigurasi `MANWIDTH`.

Jika jumlah kolom pada *terminal* terlalu kecil (misal lebar layarnya sempit), jeda baris akan tidak akurat. Hal ini dapat sangat mengganggu ketika dibaca. Anda dapat memperbaiki hal ini dengan mengatur MANWIDTH pada invokasi `man`. Dengan `Bash`, akan menjadi seperti berikut:

 `~/.bashrc` 
```
man() {
    local width=$(tput cols)
    [ $width -gt $MANWIDTH ] && width=$MANWIDTH
    env MANWIDTH=$width \
    man "$@"
}

```

Jangan ragu untuk mengombinasikan fungsi ini dengan [color settings](#Colored_man_pages).

## Membaca halaman panduan lokal

Sebagai ganti antarmuka yang standar, menggunakan peramban seperti [lynx](https://www.archlinux.org/packages/?name=lynx) dan [Firefox](/index.php/Firefox "Firefox") untuk melihat halaman panduan yang memungkinkan pengguna mendapatkan manfaat utama halaman informasi dari teks *hyperlink*. Alternatifnya meliputi sebagai berikut:

*   Para pengguna [KDE](/index.php/KDE "KDE") dapat membaca halaman panduan di Konqueror menggunakan `man:<name>`.
*   [xorg-xman](https://www.archlinux.org/packages/?name=xorg-xman) menyajikan tampilan halaman panduan yang terkategorikan pada [X](/index.php/X "X").
*   Bantuan Peramban (*Help Browseer*) [GNOME](/index.php/GNOME "GNOME") [yelp](https://www.archlinux.org/packages/?name=yelp) dapat digunakan melalui `yelp man:<name>`.

### Mengonversi ke mode halaman HTML peramban

#### mandoc

Pasang [mandoc](https://aur.archlinux.org/packages/mandoc/) dari [AUR](/index.php/AUR "AUR"). Untuk mengonversikan sebuah halaman, misalnya `free(1)`:

```
$ gunzip -c /usr/share/man/man1/free.1.gz | mandoc -Thtml -Ostyle=style.css 1> free.html

```

Buka berkas yang bernama `free.html` pada peramban Anda.

#### man2html

Pertama, pasang [man2html](https://www.archlinux.org/packages/?name=man2html) dari repositori resmi.

Lalu, konversikan halaman panduan:

```
$ man free | man2html -compress -cgiurl man$section/$title.$section$subsection.html > ~/man/free.html

```

Penggunaan lain dari `man2html` adalah mengonversi ke berkas *raw*, teks yang kompatibel dengan mesin cetak:

```
$ man free | man2html -bare > ~/free.txt

```

#### man -H

Implementasi GNU pada pandual di dalam repositori Archjuga juga memiliki kemampuan untuk melakukan hal tersebut dengan cara:

```
$ man -H free

```

Hal ini akan membaca `BROWSER` [environment variable](/index.php/Environment_variable "Environment variable") Anda untuk menentukan peramban. Anda dapat mengganti ini dengan cara melewati biner ke opsi `-H`.

#### roffit

Pertama-tama pasang [roffit](https://aur.archlinux.org/packages/roffit/) dari[AUR](/index.php/AUR "AUR").

Untuk mengonversi halaman panduan:

```
$ gunzip -c /usr/share/man/man1/free.1.gz | roffit > free.html

```

### Mengonversi ke PDF

Halaman panduan selalu bisa dicetak: ditulis dalam troff, yang pada dasarnya merupakan suatu bahasa penyusunan huruf (*typesetting*). Jika Anda telah memasang *ghostscript*, mengonversi sebuah halaman panduan ke PDF sangatlah mudah: `man -t <manpage> | ps2pdf - <pdf>`. [Berikut hasil dari pencarian gambar google](https://www.google.com/search?q=manpage+pdf+troff&num=100&hl=en&prmd=imvns&source=lnms&tbm=isch&sa=X&ei=5BZpUI3oH6rI2AXvx4CoAw&ved=0CAoQ_AUoAQ&biw=1321&bih=1100) memberikan Anda gambaran akan terlihat seperti apa hasilnya; mungkin bukan kesukaan semua orang.

Caveats: Huruf-huruf umumnya terbatas pada Times dengan ukuran *hardcoded*. Tidak ada *hyperlink*. Beberapa halaman panduan didesain khusus untuk tampilan *terminal*, dan tidak akan terlihat baik pada format PS atau PDF.

Berikut skrip dalam bahasa perl untuk mengonversi halaman panduan ke PDF, penyimpanan sementara PDF di dalam direktori `$HOME/.manpdf/`, dan secara khusus gunakan penampil PDF, seperti [mupdf](https://www.archlinux.org/packages/?name=mupdf).

 `Usage: manpdf [<section>] <manpage>` 
```
#!/usr/bin/perl
use File::stat;

$pdfdir = $ENV{"HOME"}."/.manpdf";
-d $pdfdir || mkdir $pdfdir || die "can't create $pdfdir";
$manpage = $ARGV[0];
chop($manpath = `man -w $manpage`);
die if $?;

$maninfo = stat($manpath) or die;
$manpath =~ s@.*/man./(.*)(\.(gz|bz2))?$@$1@;
$pdfpath = "$pdfdir/$manpath.pdf";
$pdftime = 0;
if (-f $pdfpath) {
    $pdfinfo = stat($pdfpath) or die;
    $pdftime = $pdfinfo->mtime;
}
if (!-f $pdfpath || $maninfo->mtime > $pdftime) {
    system "man -t $manpage | ps2pdf -dPDFSETTINGS=/screen - $pdfpath";
}
die if !-f $pdfpath;
if (!fork) {
    open(STDOUT, "/dev/null");
    open(STDERR, "/dev/null");
    exec "mupdf", "-r", "96", $pdfpath;
    #exec "acroread", $pdfpath;
}

```

## Halaman Panduan berbasis Online

Ada beberapa basis datas halaman panduan yang berbasis *online*, termasuk:

*   [Man7.org.](http://man7.org/linux/man-pages/index.html) Upstream for Arch Linux's [man-pages](https://www.archlinux.org/packages/?name=man-pages).
*   [*Arch Linux man pages*](https://manned.org/pkg/arch)
*   [*Debian GNU/Linux man pages*](http://manpages.debian.net/)
*   [*DragonFlyBSD manual pages*](http://leaf.dragonflybsd.org/cgi/web-man)
*   [*FreeBSD Hypertext Man Pages*](http://www.freebsd.org/cgi/man.cgi)
*   [*Linux and Solaris 10 Man Pages*](http://www.manpages.spotlynx.com/)
*   [*Linux man pages at die.net*](http://linux.die.net/man/)
*   [The Linux man-pages project at kernel.org](http://www.kernel.org/doc/man-pages/)
*   [*NetBSD manual pages*](http://netbsd.gw.com/cgi-bin/man-cgi)
*   [*Mac OS X Manual Pages*](http://developer.apple.com/documentation/Darwin/Reference/ManPages/index.html)
*   [*On-line UNIX manual pages*](http://unixhelp.ed.ac.uk/alphabetical/index.html)
*   [*OpenBSD manual pages*](http://www.openbsd.org/cgi-bin/man.cgi)
*   [*Plan 9 Manual — Volume 1*](http://man.cat-v.org/plan_9/)
*   [*Inferno Manual — Volume 1*](http://man.cat-v.org/inferno/)
*   [*Storage Foundation Man Pages*](http://sfdoccentral.symantec.com/sf/5.0MP3/linux/manpages/index.html)
*   [*The UNIX and Linux Forums Man Page Repository*](http://www.unix.com/man-page/OpenSolaris/1/man/)
*   [*Ubuntu Manpage Repository*](http://manpages.ubuntu.com/)

**Warning:** Beberapa distribusi menyediakan halaman panduan yang telah di-*patch* atau sudah usang yang berbeda dari yang disediakan oleh Arch. Hati-hati saat menggunakan panduan secara *online*.

## Halaman panduan penting

Berikut daftar non-komplit dari halaman penting yang dapat membantu Anda memahami banyak hal secara lebih mendalam. Beberapa dari daftar di bawah ini dapat menjadi referensi yang bagus (seperti tabel ASCII).

*   [ascii(7)](https://jlk.fjfi.cvut.cz/arch/manpages/man/ascii.7)
*   [boot(7)](https://jlk.fjfi.cvut.cz/arch/manpages/man/boot.7)
*   [charsets(7)](https://jlk.fjfi.cvut.cz/arch/manpages/man/charsets.7)
*   [chmod(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/chmod.1)
*   [credentials(7)](https://jlk.fjfi.cvut.cz/arch/manpages/man/credentials.7)
*   [fstab(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/fstab.5)
*   [hier(7)](https://jlk.fjfi.cvut.cz/arch/manpages/man/hier.7)
*   [systemd(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/systemd.1)
*   [locale(1p)](https://jlk.fjfi.cvut.cz/arch/manpages/man/locale.1p), [locale(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/locale.5), [locale(7)](https://jlk.fjfi.cvut.cz/arch/manpages/man/locale.7)
*   [printf(3)](https://jlk.fjfi.cvut.cz/arch/manpages/man/printf.3)
*   [proc(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/proc.5)
*   [regex(7)](https://jlk.fjfi.cvut.cz/arch/manpages/man/regex.7)
*   [signal(7)](https://jlk.fjfi.cvut.cz/arch/manpages/man/signal.7)
*   [term(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/term.5), [term(7)](https://jlk.fjfi.cvut.cz/arch/manpages/man/term.7)
*   [termcap(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/termcap.5)
*   [terminfo(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/terminfo.5)
*   [utf-8(7)](https://jlk.fjfi.cvut.cz/arch/manpages/man/utf-8.7)

Secara lebih umum, lihatlah kategori 7 pada halaman panduan:

```
$ man -s 7 -k ".*" 

```

Halaman khusus Arch Linux:

*   [archlinux(7)](https://jlk.fjfi.cvut.cz/arch/manpages/man/archlinux.7)
*   [mkinitcpio(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/mkinitcpio.8)
*   [pacman(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/pacman.8)
*   [pacman-key(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/pacman-key.8)
*   [pacman.conf(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/pacman.conf.5)

## Lihat juga

*   [man page - Gentoo wiki article](https://wiki.gentoo.org/wiki/Man_page)
*   [Setting colors for less](http://unix.stackexchange.com/a/147) dan [solving related problems](http://unix.stackexchange.com/a/6357) (*thread* di StackExchange)
*   [Write The Fine Manual with pod2man](https://linuxtidbits.wordpress.com/2013/08/21/wtfm-write-the-fine-manual-with-pod2man-text-converter/)