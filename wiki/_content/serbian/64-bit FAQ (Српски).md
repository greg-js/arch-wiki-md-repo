Below is a list of frequently asked questions about Arch64.

## Contents

*   [1 Kako da instalirate Arch64?](#Kako_da_instalirate_Arch64.3F)
*   [2 Koliko je potpun port?](#Koliko_je_potpun_port.3F)
*   [3 Hoću li imati sve pakete kao na 32-bitnom Archu koji sam imao?](#Ho.C4.87u_li_imati_sve_pakete_kao_na_32-bitnom_Archu_koji_sam_imao.3F)
*   [4 Da li 64-bita znače veliko brzinsko poboljšanje?](#Da_li_64-bita_zna.C4.8De_veliko_brzinsko_pobolj.C5.A1anje.3F)
*   [5 Kako mogu prijavit greške?](#Kako_mogu_prijavit_gre.C5.A1ke.3F)
*   [6 Koje riznice bi trebao koristit u pacmanu?](#Koje_riznice_bi_trebao_koristit_u_pacmanu.3F)
*   [7 Kako prepraviti postojeće PKGBUILDs da bi se koristili u Arch64?](#Kako_prepraviti_postoje.C4.87e_PKGBUILDs_da_bi_se_koristili_u_Arch64.3F)
*   [8 Šta ću propustiti u Arch64?](#.C5.A0ta_.C4.87u_propustiti_u_Arch64.3F)
*   [9 Mogu li graditi 32-bitne pakete za i686 unutar Arch64?](#Mogu_li_graditi_32-bitne_pakete_za_i686_unutar_Arch64.3F)
*   [10 Mogu li pokrenuti 32-bitne aplikacije unutar Arch64?](#Mogu_li_pokrenuti_32-bitne_aplikacije_unutar_Arch64.3F)
*   [11 Mogu li nadograditi / promeniti moj sistem od i686 bez ponovno instalirajte na x86_64?](#Mogu_li_nadograditi_.2F_promeniti_moj_sistem_od_i686_bez_ponovno_instalirajte_na_x86_64.3F)

## Kako da instalirate Arch64?

Dovoljno je koristiti naš [zvanični instalacioni ISO CD](https://www.archlinux.org/download/).

## Koliko je potpun port?

Port je spreman za svakodnevno korišćenje u desktop ili serverskom okruženju.

## Hoću li imati sve pakete kao na 32-bitnom Archu koji sam imao?

Osnovne i dodante riznice imaju gotovo sve pakete kao i na i686 i redovno se nadograđuju svaki dan samo je razlika par sati pri dolasku nove nadogradnje.

Najčešće paket u AUR će imat 'i686' , ali možete dodat u liniju PKGBUILD i 'x86_64' i najverovatnije da će vam paket radit.

## Da li 64-bita znače veliko brzinsko poboljšanje?

For applications using the 64-bit CPU registers (large databases and such) this is true in most cases. Some multimedia applications will also run noticeably faster. If you know an application which is known to be much faster when using SSE3 extensions you can rebuild the package yourself. We _only_ compile with SSE2 support (from march=x86_64) and -O2 optimizations. Za više informacija [http://forums.gentoo.org/viewtopic.php?t=221045](http://forums.gentoo.org/viewtopic.php?t=221045) ili [http://www.thejemreport.com/mambo/content/view/74/74/](http://www.thejemreport.com/mambo/content/view/74/74/) .

Za ostatak sistema: To ne čini bilo koji razlika ako se čeka na tastaturi.

For certain boot problems try these special kernel boot flags: [http://www.x86-64.org/lists/discuss/msg03747.html](http://www.x86-64.org/lists/discuss/msg03747.html) (dead link)

I have three 64-bit Archies running now, and they perform noticeably better under heavy load. It just seems to deliver more punch.

## Kako mogu prijavit greške?

Jednostavno korištenje Arch flyspray ali odaberite x86_64 arhitekturu u polje ako mislite da je u portu problem!

## Koje riznice bi trebao koristit u pacmanu?

Sve riznice su podržane za priključak koje su za x86_64 pakete.

## Kako prepraviti postojeće PKGBUILDs da bi se koristili u Arch64?

Dodati sledeću varijabilu:

```
arch=('i686' 'x86_64') 

```

Add small patches directly to the sources and md5sums area but use for complete different sources:

```
[ "$CARCH" = "x86_64" ] && source=(${source[@]} 'other source')
[ "$CARCH" = "x86_64" ] && md5sums=(${md5sums[@]} 'other md5sum')

```

For any small fix use this in the build area:

```
[ "$CARCH" = "x86_64" ] && (patch -Np0 -i ../foo_x86_64.patch || return 1)

```

Or when you need more changes:

```
if [ "$CARCH" = "x86_64" ]; then
    configure/patch/sed      # for x86_64
  else configure/patch/sed   # for i686
fi

```

## Šta ću propustiti u Arch64?

Ništa, stvarno. Gotovo svi programi podržavaju 64-bitne ili su do sada u tranziciji da postanu 64-bitni kompatibilni.

Ovi programi su prethodno bile problematični, ali sada su na raspolaganju [AUR](/index.php/AUR "AUR") i rada u redu:

*   [Skype](/index.php/Skype "Skype") as bin32-skype
*   [Wine](/index.php/Wine "Wine") as bin32-wine
*   [Zsnes](/index.php?title=Zsnes&action=edit&redlink=1 "Zsnes (page does not exist)") as bin32-zsnes

The biggest problem are packages that are either **closed source** or contains x86-specific assembly that is cumbersome to port to 64-bit (typical for emulators).

*   TeamSpeak will not support 64-bit until the next version is released.
*   Acrobat Reader plugin is not available in 64-bit, but you can run the 32-bit version in compatibility mode

Everything else should work perfectly fine. If you miss any Arch32 package in our port and you know that it will compile on x86_64 (perhaps you have found it as native packages in another 64-bit distribution), just contact the devs or request a new package in the forums.

## Mogu li graditi 32-bitne pakete za i686 unutar Arch64?

Da. Potreban vam je radni i686 chroot (installation with i686 iso "quickinstall" is recommended for the quick way to install it inside Arch64 or see [Arch64 Install bundled 32bit system](/index.php/Arch64_Install_bundled_32bit_system "Arch64 Install bundled 32bit system")). Install "linux32" wrapper pkg from current to make the chroot behave like a real i686 system. Then use this script to login into the chroot environment as root:

```
#!/bin/bash
mount --bind /dev /path-to-your-chroot/dev
mount --bind /dev/pts /path-to-your-chroot/dev/pts
mount --bind /dev/shm /path-to-your-chroot/dev/shm
mount -t proc none /path-to-your-chroot/proc
mount -t sysfs none /path-to-your-chroot/sys
linux32 chroot /path-to-your-chroot

```

If you keep the sources on the x86_64 host system you can add

```
"mount --bind /path-to-your-stored-sources /path-to-your-chroot/path-to-your-stored-sources" 

```

to share sources from host to chroot system for pkg building used in /etc/makepkg.conf.

## Mogu li pokrenuti 32-bitne aplikacije unutar Arch64?

Da!

1.  Možete instalirati lib32-* libs iz zajednice repozitorija za Multilib sistema.
2.  Ili možete stvoriti drugi chroot sa 32bit sistemom:

Bootujte u Arch64, startx, otvorite terminal.

```
$ xhost +local:
$ su
# mount /dev/sda1 /mnt/arch32
# mount --bind /proc /mnt/arch32/proc
# chroot /mnt/arch32
# su your32bitusername
$ /usr/bin/command-you want # or eg: /opt/mozilla/bin/firefox

```

Neke 32-bit programi (kao OpenOffice) zahteva sledeće dodatke. Sledeća linija se može stavitiu u rc.local kako bi se osiguralo da dobijete sve što vam treba za 32-bitne programe (assuming /mnt/arch32 is mounted in fstab):

```
mount --bind /dev /mnt/arch32/dev
mount --bind /dev/pts /mnt/arch32/dev/pts
mount --bind /dev/shm /mnt/arch32/dev/shm
mount --bind /proc /mnt/arch32/proc
mount --bind /proc/bus/usb /mnt/arch32/proc/bus/usb
mount --bind /sys /mnt/arch32/sys
mount --bind /tmp /mnt/arch32/tmp
#comment the following line if you do not use the same home folder
mount --bind /home /mnt/arch32/home

```

Nakon toga možete upisati u terminal:

```
$ xhost +localhost
$ sudo chroot /mnt/arch32 su your32bitusername /opt/openoffice/program/soffice

```

## Mogu li nadograditi / promeniti moj sistem od i686 bez ponovno instalirajte na x86_64?

- Ne, međutim, možete pokrenuti sistem s Arch64 instalirati CD, montirajte disk, backup sve Vaše podatke koje želite zadržati da nije 32-bitni binarni (npr: /home & /etc), i instalirajte.