Εδώ συχνές ερωτήσεις-απαντήσεις για την αρχιτεκτονική x86_64 στο Arch Linux

## Contents

*   [1 Πώς μπορώ να εγκαταστήσω το Arch64;](#.CE.A0.CF.8E.CF.82_.CE.BC.CF.80.CE.BF.CF.81.CF.8E_.CE.BD.CE.B1_.CE.B5.CE.B3.CE.BA.CE.B1.CF.84.CE.B1.CF.83.CF.84.CE.AE.CF.83.CF.89_.CF.84.CE.BF_Arch64.3B)
*   [2 Πόσο πλήρης είναι η μεταφορά στην 64bit αρχιτεκτονική; Θα έχω όλα τα πακέτα απο το αντίστοιχο 32bit περιβάλλον ;](#.CE.A0.CF.8C.CF.83.CE.BF_.CF.80.CE.BB.CE.AE.CF.81.CE.B7.CF.82_.CE.B5.CE.AF.CE.BD.CE.B1.CE.B9_.CE.B7_.CE.BC.CE.B5.CF.84.CE.B1.CF.86.CE.BF.CF.81.CE.AC_.CF.83.CF.84.CE.B7.CE.BD_64bit_.CE.B1.CF.81.CF.87.CE.B9.CF.84.CE.B5.CE.BA.CF.84.CE.BF.CE.BD.CE.B9.CE.BA.CE.AE.3B_.CE.98.CE.B1_.CE.AD.CF.87.CF.89_.CF.8C.CE.BB.CE.B1_.CF.84.CE.B1_.CF.80.CE.B1.CE.BA.CE.AD.CF.84.CE.B1_.CE.B1.CF.80.CE.BF_.CF.84.CE.BF_.CE.B1.CE.BD.CF.84.CE.AF.CF.83.CF.84.CE.BF.CE.B9.CF.87.CE.BF_32bit_.CF.80.CE.B5.CF.81.CE.B9.CE.B2.CE.AC.CE.BB.CE.BB.CE.BF.CE.BD_.3B)
*   [3 Το 64bit σημαίνει μεγάλη αύξηση σε ταχύτητα ;](#.CE.A4.CE.BF_64bit_.CF.83.CE.B7.CE.BC.CE.B1.CE.AF.CE.BD.CE.B5.CE.B9_.CE.BC.CE.B5.CE.B3.CE.AC.CE.BB.CE.B7_.CE.B1.CF.8D.CE.BE.CE.B7.CF.83.CE.B7_.CF.83.CE.B5_.CF.84.CE.B1.CF.87.CF.8D.CF.84.CE.B7.CF.84.CE.B1_.3B)
*   [4 Προσοχή όταν αναβαθμίζετε το πακετο glibc από την έκδοση <2.4 !](#.CE.A0.CF.81.CE.BF.CF.83.CE.BF.CF.87.CE.AE_.CF.8C.CF.84.CE.B1.CE.BD_.CE.B1.CE.BD.CE.B1.CE.B2.CE.B1.CE.B8.CE.BC.CE.AF.CE.B6.CE.B5.CF.84.CE.B5_.CF.84.CE.BF_.CF.80.CE.B1.CE.BA.CE.B5.CF.84.CE.BF_glibc_.CE.B1.CF.80.CF.8C_.CF.84.CE.B7.CE.BD_.CE.AD.CE.BA.CE.B4.CE.BF.CF.83.CE.B7_.3C2.4_.21)
*   [5 Πώς ενημερώνω για πιθανά bugs;](#.CE.A0.CF.8E.CF.82_.CE.B5.CE.BD.CE.B7.CE.BC.CE.B5.CF.81.CF.8E.CE.BD.CF.89_.CE.B3.CE.B9.CE.B1_.CF.80.CE.B9.CE.B8.CE.B1.CE.BD.CE.AC_bugs.3B)
*   [6 Υπάρχει mailing list;](#.CE.A5.CF.80.CE.AC.CF.81.CF.87.CE.B5.CE.B9_mailing_list.3B)
*   [7 Τί repos πρέπει να χρησιμοποιήσω;](#.CE.A4.CE.AF_repos_.CF.80.CF.81.CE.AD.CF.80.CE.B5.CE.B9_.CE.BD.CE.B1_.CF.87.CF.81.CE.B7.CF.83.CE.B9.CE.BC.CE.BF.CF.80.CE.BF.CE.B9.CE.AE.CF.83.CF.89.3B)
*   [8 Πώς μπορώ να βρω PKGBUILDS για το χτίσιμο πακέτων για την αρχιτεκτονική 64bit ;](#.CE.A0.CF.8E.CF.82_.CE.BC.CF.80.CE.BF.CF.81.CF.8E_.CE.BD.CE.B1_.CE.B2.CF.81.CF.89_PKGBUILDS_.CE.B3.CE.B9.CE.B1_.CF.84.CE.BF_.CF.87.CF.84.CE.AF.CF.83.CE.B9.CE.BC.CE.BF_.CF.80.CE.B1.CE.BA.CE.AD.CF.84.CF.89.CE.BD_.CE.B3.CE.B9.CE.B1_.CF.84.CE.B7.CE.BD_.CE.B1.CF.81.CF.87.CE.B9.CF.84.CE.B5.CE.BA.CF.84.CE.BF.CE.BD.CE.B9.CE.BA.CE.AE_64bit_.3B)
*   [9 Πώς μπορώ να χτίσω 64bit πακέτα απο έτοιμα 32bit PKGBUILDs;](#.CE.A0.CF.8E.CF.82_.CE.BC.CF.80.CE.BF.CF.81.CF.8E_.CE.BD.CE.B1_.CF.87.CF.84.CE.AF.CF.83.CF.89_64bit_.CF.80.CE.B1.CE.BA.CE.AD.CF.84.CE.B1_.CE.B1.CF.80.CE.BF_.CE.AD.CF.84.CE.BF.CE.B9.CE.BC.CE.B1_32bit_PKGBUILDs.3B)
*   [10 Πώς μπορώ να προσθέσω patches σε ήδη υπάρχοντα PKGBUILDs για χρήση με το Arch64;](#.CE.A0.CF.8E.CF.82_.CE.BC.CF.80.CE.BF.CF.81.CF.8E_.CE.BD.CE.B1_.CF.80.CF.81.CE.BF.CF.83.CE.B8.CE.AD.CF.83.CF.89_patches_.CF.83.CE.B5_.CE.AE.CE.B4.CE.B7_.CF.85.CF.80.CE.AC.CF.81.CF.87.CE.BF.CE.BD.CF.84.CE.B1_PKGBUILDs_.CE.B3.CE.B9.CE.B1_.CF.87.CF.81.CE.AE.CF.83.CE.B7_.CE.BC.CE.B5_.CF.84.CE.BF_Arch64.3B)
*   [11 Τί χάνω στο Arch64;](#.CE.A4.CE.AF_.CF.87.CE.AC.CE.BD.CF.89_.CF.83.CF.84.CE.BF_Arch64.3B)
*   [12 Μπορώ να χτίσω πακέτα για την αρχιτεκτονική 32bit (i686) μεσα σε περιβάλλον 64bit (x86_64) ;](#.CE.9C.CF.80.CE.BF.CF.81.CF.8E_.CE.BD.CE.B1_.CF.87.CF.84.CE.AF.CF.83.CF.89_.CF.80.CE.B1.CE.BA.CE.AD.CF.84.CE.B1_.CE.B3.CE.B9.CE.B1_.CF.84.CE.B7.CE.BD_.CE.B1.CF.81.CF.87.CE.B9.CF.84.CE.B5.CE.BA.CF.84.CE.BF.CE.BD.CE.B9.CE.BA.CE.AE_32bit_.28i686.29_.CE.BC.CE.B5.CF.83.CE.B1_.CF.83.CE.B5_.CF.80.CE.B5.CF.81.CE.B9.CE.B2.CE.AC.CE.BB.CE.BB.CE.BF.CE.BD_64bit_.28x86_64.29_.3B)
*   [13 Μπορώ να τρέξω 32bit εφαρμογές μεσα στο 64bit Arch σύστημα μου;](#.CE.9C.CF.80.CE.BF.CF.81.CF.8E_.CE.BD.CE.B1_.CF.84.CF.81.CE.AD.CE.BE.CF.89_32bit_.CE.B5.CF.86.CE.B1.CF.81.CE.BC.CE.BF.CE.B3.CE.AD.CF.82_.CE.BC.CE.B5.CF.83.CE.B1_.CF.83.CF.84.CE.BF_64bit_Arch_.CF.83.CF.8D.CF.83.CF.84.CE.B7.CE.BC.CE.B1_.CE.BC.CE.BF.CF.85.3B)
*   [14 Μπορώ να "αναβαθμίσω" το σύστημα μου σε 64bit, από ένα σύστημα 32bit, χωρίς επανεγκατάσταση ;](#.CE.9C.CF.80.CE.BF.CF.81.CF.8E_.CE.BD.CE.B1_.22.CE.B1.CE.BD.CE.B1.CE.B2.CE.B1.CE.B8.CE.BC.CE.AF.CF.83.CF.89.22_.CF.84.CE.BF_.CF.83.CF.8D.CF.83.CF.84.CE.B7.CE.BC.CE.B1_.CE.BC.CE.BF.CF.85_.CF.83.CE.B5_64bit.2C_.CE.B1.CF.80.CF.8C_.CE.AD.CE.BD.CE.B1_.CF.83.CF.8D.CF.83.CF.84.CE.B7.CE.BC.CE.B1_32bit.2C_.CF.87.CF.89.CF.81.CE.AF.CF.82_.CE.B5.CF.80.CE.B1.CE.BD.CE.B5.CE.B3.CE.BA.CE.B1.CF.84.CE.AC.CF.83.CF.84.CE.B1.CF.83.CE.B7_.3B)

## Πώς μπορώ να εγκαταστήσω το Arch64;

Απλά χρησιμοποιείστε το [επίσημο CD εγκατάστασης για το Arch64](https://www.archlinux.org/download/).

## Πόσο πλήρης είναι η μεταφορά στην 64bit αρχιτεκτονική; Θα έχω όλα τα πακέτα απο το αντίστοιχο 32bit περιβάλλον ;

Τα αποθετήρια (repositories) [extra] και [core] είναι πλήρως μεταγλωττισμένα στην 64bit αρχιτεκτονική και σχεδόν up-to-date, δηλαδή μόλις λίγες ώρες ή μερες πίσω σε ανανεωση απο το Arch i686\. Οι TUs προσπαθούν να μεταφέρουν και το [community] αποθετήριο πλήρως και στην 64bit αρχιτεκτονική.

Το port στην 64bit αρχιτεκτονική είναι πλήρες για καθημερινή desktop και server χρήση.

## Το 64bit σημαίνει μεγάλη αύξηση σε ταχύτητα ;

Για εφαρμογές που χρησιμοποιούν αμειγώς 64bit μητρώα (όπως μεγάλες βάσεις δεδομένων κλπ) αυτό είναι αλήθεια, στις περισσότερες περιπτώσεις. Ορισμένες μάλιστα εφαρμογές multimedia θα εκτελούνται εμφανώς γρηγορότερα. Εάν γνωρίζετε μία εφαρμογή που να εκτελείται γρηγορότερα όταν χρησιμοποιούνται οι CPU επεκτάσεις SSE3, μπορείτε να ξαναχτίσετε το πακέτο μόνοι σας. Εμείς κάνουμε compilation σε προγράμματα μόνο με SSE2 support (με march=x86_64) and -O2 βελτιστοποιήσεις. Για περισσότερα διαβάστε [http://forums.gentoo.org/viewtopic.php?t=221045](http://forums.gentoo.org/viewtopic.php?t=221045) ή [http://www.thejemreport.com/mambo/content/view/74/74/](http://www.thejemreport.com/mambo/content/view/74/74/) .

Για το υπόλοιπο σύστημα: Δεν κάνει και καμιά ιδιαίτερη διαφορά.

Ως γνωστόν, τα 64bit συστήματα, καταφέρνουν να φέρουν υψηλότερες επιδόσεις, ιδίως σε υψηλό φόρτο, με οποιοδήποτε 64bit capable επεξεργαστή (Core2Duo ή νεότερο επεξεργαστή Intel με Intel64, Athlon64 ή νεότερο επεξεργαστή AMD με AMD64)

## Προσοχή όταν αναβαθμίζετε το πακετο glibc από την έκδοση <2.4 !

Είναι σημαντικό να αναβαθμίσετε το glibc απο έκδοση <2.4 και πρέπει να γίνει ξεχωριστά απο το υπόλοιπο σύστημα. Γι'αυτό κάνετε μόνο

```
  pacman -Syy glibc 

```

και εάν είναι επιτυχής η αναβάθμιση κάνετε

```
 pacman -Su 

```

Μπορεί να μην πετύχει η προσθαφαίρεση βιβλιοθηκών και πρέπει να χρησιμοποιήσετε το pacman.static για να το διορθώσετε.

## Πώς ενημερώνω για πιθανά bugs;

Απλά να χρησιμοποιήσετε το Arch Flyspray αλλά επισημάνετε ότι χρησιμοποιείτε x86_64 εάν πιστεύετε ότι είναι πρόβλημα μεταφοράς πακέτων στα 64bit.

## Υπάρχει mailing list;

Ναι, δείτε εδώ μία[mailing list για τα Arch ports σε αλλη αρχιτεκτονική](https://archlinux.org/mailman/listinfo/arch-ports).

## Τί repos πρέπει να χρησιμοποιήσω;

Όλα τα επίσημα repos λειτουργούν σωστά για την 64bit αρχιτεκτονική.

## Πώς μπορώ να βρω PKGBUILDS για το χτίσιμο πακέτων για την αρχιτεκτονική 64bit ;

Χρησιμοποιείται το _**ABS**_ όπως στο 32bit Arch. Προτεινόμενο μέρος για τοποθέτηση των PKGBUILDs είναι το _/var/abs_. Το _abs_ κατεβάζει όλες τις καταχωρήσεις στο Arch CVS από το archlinux.org που έχουν ως tag CURRENT-64.

## Πώς μπορώ να χτίσω 64bit πακέτα απο έτοιμα 32bit PKGBUILDs;

Τα PKGBUILDs του Arch 32bit είναι κοινά με του Arch 64bit. Μπορείτε να βρείτε 32-bit PKGBUILDs που δεν έχουν ακόμη μεταφερθεί ως ports στην 64bit αρχιτεκτονική απο το CVS: [https://www.archlinux.org/cvs/](https://www.archlinux.org/cvs/)

## Πώς μπορώ να προσθέσω patches σε ήδη υπάρχοντα PKGBUILDs για χρήση με το Arch64;

Προστίθεται αυτή η μεταβλητή:

```
arch=('i686' 'x86_64') 

```

Προσθέστε μικρά patches κατευθείαν στο source πακέτο και στο τμήμα για τα MD5SUMs για χρήση σε τελειως διαφορετικά sources:

```
[ "$CARCH" = "x86_64" ] && source=(${source[@]} 'other source')
[ "$CARCH" = "x86_64" ] && md5sums=(${md5sums[@]} 'other md5sum')

```

Προσθέστε αυτό στο τμήμα για το χτίσιμο του πακέτου (build area):

```
[ "$CARCH" = "x86_64" ] && (patch -Np0 -i ../foo_x86_64.patch || return 1)

```

Ή όταν κάνετε μεγαλύτερες αλλαγές:

```
if [ "$CARCH" = "x86_64" ]; then
    configure/patch/sed      # for x86_64
  else configure/patch/sed   # for i686
fi

```

Για τους developers:

```
cvs commit -m "x86_64 updated/fixed or whatever"
cvs tag -cFR CURRENT-64 foo-package-directory (ακόμη και για τα extra, community, unstable and testing repositories)

```

## Τί χάνω στο Arch64;

Οι ακόλουθες εφαρμογές δεν είναι ακόμη 64bit συμβατές:

*   πραγματικό x86_64 Flash support, μόνο κατά τμήματα με το GPL gnash or swfdec package από το extra repo
*   όχι native (εγγενές) Flash plugin από την Adobe (R) - μόνο το nspluginwrapper από το community repo επιτρέπει την χρήση 32bit plugins και εγκαθιστά lib32 packages για συμβατότητα - ακολουθείστε αυτόν τον οδηγό για περισσότερα [Install Flash on Arch64](/index.php?title=Install_Flash_on_Arch64&action=edit&redlink=1 "Install Flash on Arch64 (page does not exist)")
*   Εφαρμογές κλειστού κώδικα όπως το Skype, TeamSpeak, games και άλλα ...
*   win32 codecs (... που δεν χρειαζόμαστε σχεδόν ποτέ)
*   πακέτα που χρησιμοποιούν x86 32-bit assembler κώδικα (ορισμένοι emulators όπως το zsnes και το syslinux)

Όλα τα υπόλοιπα σχεδόν πακέτα και προγράμματα μπορούν να μεταφερθούν στην 64bit αρχιτεκτονική. Εάν σας λείπει κάποιο 32bit πακέτο και ξέρετε ότι χτίζεται και για την 64bit αρχιτεκτονική (e.g. το βρήκατε και σε άλλη 64bit Linux διανομή χωρίς την χρήση πρόσθετων βιβλιοθηκών συμβατότητας), ενημερώστε τους developers.

## Μπορώ να χτίσω πακέτα για την αρχιτεκτονική 32bit (i686) μεσα σε περιβάλλον 64bit (x86_64) ;

Ναι. Χρειάζεται να φτιάξετε ενα i686 chroot περιβάλλον (για χρήση και του i686 CD δειτε περισσότερα εδώ [Arch64 Install bundled 32bit system](/index.php/Arch64_Install_bundled_32bit_system "Arch64 Install bundled 32bit system")). Εγκαταστήστε το linux32 πακέτο για να κάνετε το chrooted περιβάλλον να συμπεριφέρεται σαν πραγματικό i686 περιβάλλον. Μετά χρησιμοποιείστε το script που ακολουθεί για να κάνετε login στο chrooted περιβάλλον σαν root

**Προσοχή ! Να βάλετε τα δικά σας mountpoints απαραιτήτως**:

```
#!/bin/bash
mount --bind /dev /path-to-your-chroot/dev
mount --bind /dev/pts /path-to-your-chroot/dev/pts
mount --bind /dev/shm /path-to-your-chroot/dev/shm
mount -t proc none /path-to-your-chroot/proc
mount -t sysfs none /path-to-your-chroot/sys
linux32 chroot /path-to-your-chroot

```

Εάν τα πακέτα με το source βρίσκονται στο x86_64 σύστημα προσθέστε

```
 "mount --bind /path-to-your-stored-sources /path-to-your-chroot/path-to-your-stored-sources" 

```

για να μοιράζετε sources από το μητρικό στο chrooted σύστημα για το χτίσιμο των δικών σας πακέτων μέσω του /etc/makepkg.conf.

## Μπορώ να τρέξω 32bit εφαρμογές μεσα στο 64bit Arch σύστημα μου;

Ναι.

1) Εγκαταστήστε τις lib32-* βιβλιοθήκες από το community repo..

2) Ή να φτιάξετε ένα chrooted περιβάλλον με 32bit σύστημα:

Εκκινείστε το Arch64, εκκινείστε τον X (π.χ. startx), ανοίξτε terminal (π.χ. xterm)

**Προσοχή, χρησιμοποιείστε τα δικά σας mountpoints.**

```
xhost +local:
su
mount /dev/sda1 /mnt/arch32
mount --bind /proc /mnt/arch32/proc
chroot /mnt/arch32
su your32bitusername
/usr/bin/command-που-θέλετε-να-τρέξετε # ή π.χ.: /opt/mozilla/bin/firefox

```

Ορισμένες 32bit εφαρμογές (όπως το OpenOffice) χρειάζονται οπωσδήποτε πρόσθετα πακέτα για το χτίσιμο τους. Οι εξής γραμμές πρέπει να προσθεθούν στο rc.local για να επιβεβαιώσετε ότι θα τρέξουν 32-bit εφαρμογές χωρίς πρόβλημα (υποθέτωντας ότι το /mnt/arch32 είναι mounted στο /etc/fstab):

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

Μετά πατήστε στο terminal

```
xhost +localhost
sudo chroot /mnt/arch32 su your32bitusername /opt/openoffice/program/soffice

```

## Μπορώ να "αναβαθμίσω" το σύστημα μου σε 64bit, από ένα σύστημα 32bit, χωρίς επανεγκατάσταση ;

Όχι. Όμως, μπορείτε να εγκαταστήσετε το Arch64 CD, κάνετε mount τον δίσκο , κάνετε backup ό,τι χρειάζεστε και εγκαταστήστε κρατώντας ό,τι δεν είναι 32bit compiled, όπως και mountpoints που δεν θα έχουν πρόβλημα συμβατότητας (π.χ.: /home & /etc) και εγκαταστήστε.