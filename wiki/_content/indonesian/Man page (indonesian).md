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
    *   [6.1 Mengkonversi ke mode halaman HTML peramban](#Mengkonversi_ke_mode_halaman_HTML_peramban)
        *   [6.1.1 mdocml](#mdocml)
        *   [6.1.2 man2html](#man2html)
        *   [6.1.3 man -H](#man_-H)
        *   [6.1.4 roffit](#roffit)
    *   [6.2 Mengkonversi ke PDF](#Mengkonversi_ke_PDF)
*   [7 Halaman Panduan berbasis Online](#Halaman_Panduan_berbasis_Online)
*   [8 Halaman panduan penting](#Halaman_panduan_penting)
*   [9 Lihat juga](#Lihat_juga)

## Mengakses halaman panduan

Untuk membaca halaman panduan, secara sederhana ketikkan:

```
$ man *nama_halaman*

```

Panduan-panduan diurutkan menjadi beberapa bagian. Untuk daftar lengkapnya, lihat bagian berjudul "Sections of the manual pages" in `man man-pages`.

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

Semua halaman panduan mengikuti format yang cukup standar, yang membantu dalam melakukan navigasi pada halaman panduan. Lihat bagian yang berjudul "Sections within a manual page" dalam `man man-pages`.

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

See [Color output in console#man](/index.php/Color_output_in_console#man "Color output in console").

## Lebar halaman dinamis

The man page width is controlled by the `MANWIDTH` environment variable.

If the number of columns in the terminal is too small (e.g. the window width is narrow), the line breaks will be wrong. This can be very disturbing for reading. You can fix this by setting the MANWIDTH on `man` invocation. With `Bash`, that would be:

 `~/.bashrc` 
```
man() {
    local width=$(tput cols)
    [ $width -gt $MANWIDTH ] && width=$MANWIDTH
    env MANWIDTH=$width \
    man "$@"
}

```

Feel free to combine this function with the [color settings](#Colored_man_pages).

## Membaca halaman panduan lokal

Instead of the standard interface, using browsers such as [lynx](https://www.archlinux.org/packages/?name=lynx) and [Firefox](/index.php/Firefox "Firefox") to view man pages allows users to reap info pages' main benefit of hyperlinked text. Alternatives include the following:

*   [KDE](/index.php/KDE "KDE") users can read man pages in Konqueror using `man:<name>`.
*   [xorg-xman](https://www.archlinux.org/packages/?name=xorg-xman) provides a categorized look at man pages in [X](/index.php/X "X").
*   The [GNOME](/index.php/GNOME "GNOME") Help Browser [yelp](https://www.archlinux.org/packages/?name=yelp) can be used via `yelp man:<name>`.

### Mengkonversi ke mode halaman HTML peramban

#### mdocml

Install [mdocml](https://aur.archlinux.org/packages/mdocml/) from [AUR](/index.php/AUR "AUR"). To convert a page, for example `free(1)`:

```
$ gunzip -c /usr/share/man/man1/free.1.gz | mandoc -Thtml -Ostyle=style.css 1> free.html

```

Now open the file called `free.html` in your favourite browser.

#### man2html

First, install [man2html](https://www.archlinux.org/packages/?name=man2html) from the official repositories.

Now, convert a man page:

```
$ man free | man2html -compress -cgiurl man$section/$title.$section$subsection.html > ~/man/free.html

```

Another use for `man2html` is exporting to raw, printer-friendly text:

```
$ man free | man2html -bare > ~/free.txt

```

#### man -H

The GNU implementation of man in the Arch repositories also has the ability to do this on its own:

```
$ man -H free

```

This will read your `BROWSER` [environment variable](/index.php/Environment_variable "Environment variable") to determine the browser. You can override this by passing the binary to the `-H` option.

#### roffit

First install [roffit](https://aur.archlinux.org/packages/roffit/) from [AUR](/index.php/AUR "AUR").

To convert a man page:

```
$ gunzip -c /usr/share/man/man1/free.1.gz | roffit > free.html

```

### Mengkonversi ke PDF

man pages have always been printable: they are written in troff, which is fundamentally a typesetting language. If you have ghostscript installed, converting a man page to PDF is actually very easy: `man -t <manpage> | ps2pdf - <pdf>`. [This google image search](https://www.google.com/search?q=manpage+pdf+troff&num=100&hl=en&prmd=imvns&source=lnms&tbm=isch&sa=X&ei=5BZpUI3oH6rI2AXvx4CoAw&ved=0CAoQ_AUoAQ&biw=1321&bih=1100) should give you an idea of what the result looks like; it may not be to everybody's liking.

Caveats: Fonts are generally limited to Times at hardcoded sizes. There are no hyperlinks. Some man pages were specifically designed for terminal viewing, and won't look right in PS or PDF form.

The following perl script converts man pages to PDFs, caches the PDFs in the `$HOME/.manpdf/` directory, and calls a PDF viewer, specifically [mupdf](https://www.archlinux.org/packages/?name=mupdf).

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

There are several online databases of man pages, including:

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

**Warning:** Some distributions provide patched or outdated man pages that differ from those provided by Arch. Exercise caution when using online man pages.

## Halaman panduan penting

Here follows a non-exhaustive list of noteworthy pages that might help you understand a lot of things more in-depth. Some of them might serve as a good reference (like the ASCII table).

*   [ascii(7)](http://man7.org/linux/man-pages/man7/ascii.7.html)
*   [boot(7)](http://man7.org/linux/man-pages/man7/boot.7.html)
*   [charsets(7)](http://man7.org/linux/man-pages/man7/charsets.7.html)
*   [chmod(1)](http://man7.org/linux/man-pages/man1/chmod.1.html)
*   [credentials(7)](http://man7.org/linux/man-pages/man7/credentials.7.html)
*   [fstab(5)](http://man7.org/linux/man-pages/man5/fstab.5.html)
*   [hier(7)](http://man7.org/linux/man-pages/man7/hier.7.html)
*   [systemd(1)](http://man7.org/linux/man-pages/man1/systemd.1.html)
*   [locale(1p)](http://man7.org/linux/man-pages/man1/locale.1p.html), [locale(5)](http://man7.org/linux/man-pages/man5/locale.5.html), [locale(7)](http://man7.org/linux/man-pages/man7/locale.7.html)
*   [printf(3)](http://man7.org/linux/man-pages/man3/printf.3.html)
*   [proc(5)](http://man7.org/linux/man-pages/man5/proc.5.html)
*   [regex(7)](http://man7.org/linux/man-pages/man7/regex.7.html)
*   [signal(7)](http://man7.org/linux/man-pages/man7/signal.7.html)
*   [term(5)](http://man7.org/linux/man-pages/man5/term.5.html), [term(7)](http://man7.org/linux/man-pages/man7/term.7.html)
*   [termcap(5)](http://man7.org/linux/man-pages/man5/termcap.5.html)
*   [terminfo(5)](http://man7.org/linux/man-pages/man5/terminfo.5.html)
*   [utf-8(7)](http://man7.org/linux/man-pages/man7/utf-8.7.html)

More generally, have a look at category 7 pages:

```
$ man -s 7 -k ".*" 

```

Arch Linux specific pages:

*   archlinux(7)
*   mkinitcpio(8)
*   [pacman(8)](https://www.archlinux.org/pacman/pacman.8.html)
*   [pacman-key(8)](https://www.archlinux.org/pacman/pacman-key.8.html)
*   [pacman.conf(5)](https://www.archlinux.org/pacman/pacman.conf.5.html)

## Lihat juga

*   [man page - Gentoo wiki article](https://wiki.gentoo.org/wiki/Man_page)
*   [Setting colors for less](http://unix.stackexchange.com/a/147) and [solving related problems](http://unix.stackexchange.com/a/6357) (threads on StackExchange)
*   [Write The Fine Manual with pod2man](https://linuxtidbits.wordpress.com/2013/08/21/wtfm-write-the-fine-manual-with-pod2man-text-converter/)