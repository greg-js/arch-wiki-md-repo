# Makepkg (Ελληνικά)

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

Η εντολή `makepkg` χρησιμοποιείται για να μεταγλωττίσετε τα δικά σας πακέτα καταλλήλως, έτσι ώστε να μπορεί να τα διαχειριστεί ο Pacman. Χρησιμοποιεί ένα σύστημα χτισίματος βασισμένο σε script το οποίο μπορεί να κατεβάζει και να ελέγχει την ακεραιότητα των πηγαίων αρχείων, να ελέγχει για εξαρτήσεις, να ρυθμίζει τις επιλογές για το χτίσιμο, να χτίζει/μεταγλωττίζει το πακέτο, να το εγκαθιστά σε ένα προσωρινό root περιβάλλον, να κάνει τροποποιήσεις, να δημιουργεί μετα-πληροφορίες και να πακετάρει το αποτέλεσμα. Όπως μπορείτε να δείτε η εντολή `makepkg` έχει πολλά χαρακτηριστικά, τα βασικά από τα οποία περιγράφονται παρακάτω.

## Contents

*   [1 Ξεκινώντας με τα απαραίτητα](#.CE.9E.CE.B5.CE.BA.CE.B9.CE.BD.CF.8E.CE.BD.CF.84.CE.B1.CF.82_.CE.BC.CE.B5_.CF.84.CE.B1_.CE.B1.CF.80.CE.B1.CF.81.CE.B1.CE.AF.CF.84.CE.B7.CF.84.CE.B1)
    *   [1.1 Arch Build System](#Arch_Build_System)
    *   [1.2 Makepkg](#Makepkg)
*   [2 Χτίζοντας ένα πακέτο](#.CE.A7.CF.84.CE.AF.CE.B6.CE.BF.CE.BD.CF.84.CE.B1.CF.82_.CE.AD.CE.BD.CE.B1_.CF.80.CE.B1.CE.BA.CE.AD.CF.84.CE.BF)
*   [3 Εγκαθιστώντας από buildscripts](#.CE.95.CE.B3.CE.BA.CE.B1.CE.B8.CE.B9.CF.83.CF.84.CF.8E.CE.BD.CF.84.CE.B1.CF.82_.CE.B1.CF.80.CF.8C_buildscripts)
*   [4 Χρήσιμοι Σύνδεσμοι](#.CE.A7.CF.81.CE.AE.CF.83.CE.B9.CE.BC.CE.BF.CE.B9_.CE.A3.CF.8D.CE.BD.CE.B4.CE.B5.CF.83.CE.BC.CE.BF.CE.B9)

## Ξεκινώντας με τα απαραίτητα

### Arch Build System

Καταρχήν σιγουρευτείτε ότι έχετε εγκατεστημένα όλα τα απαραίτητα εργαλεία έτσι ώστε να μπορείτε να τρέξετε τις εντολές [Arch Build System](/index.php/Arch_Build_System "Arch Build System")/makepkg και να μπορείτε να μεταγλωττίζετε software από τα πηγαία αρχεία:

```
pacman -S base-devel
pacman -S abs

```

Απαντήστε 'Y' ή απλά πατήστε Enter.

Τώρα μπορείτε να τρέξετε την εντολή `abs` για να κατεβάσετε στον υπολογιστή σας όλα τα PKGBUILDs και τα σχετικά αρχεία από τα οποία έχουν χτιστεί τα επίσημα πακέτα του Arch:

```
abs

```

Αυτό θα δημιουργήσει μια SVN ιεραρχία των αποθετηρίων κάτω από τον φάκελο /var/abs στον σκληρό σας δίσκο. Από προεπιλογή ορισμένα αποθετήρια είναι απενεργοποιημένα και θα χρειαστεί να επεξεργαστείτε πρώτα το αρχείο /etc/abs.conf και να αφαιρέσετε τα θαυμαστικά.

Επειδή ο φάκελος /var/abs έχει ιδιοκτήτη τον χρήστη root (είναι μέρος του πακέτου 'filesystem') και οι περισσότεροι άνθρωποι και οδηγοί υποθέτουν ότι χτίζετε τα πακέτα σας μέσα στον φάκελο /var/abs/local, χρειάζεται να επιτρέψετε στον χρήστη σας να έχει τα σωστά δικαιώματα στον φάκελο:

```
groupadd abs
gpasswd -a $USER abs
chown root:abs /var/abs/local
chmod 775 /var/abs/local

```

### Makepkg

Εάν θέλετε να είστε ικανοί να εγκαθιστάτε εξαρτήσεις με την εντολή makepkg ως χρήστης (με την makepkg -s, δείτε παρακάτω) θα χρειαστεί να εγκαταστήσετε το πακέτο [sudo](/index.php/Sudo "Sudo") και να προσθέσετε τον χρήστη σας στο /etc/sudoers

```
USER_NAME    ALL=(ALL)    NOPASSWD: /usr/bin/pacman

```

To παραπάνω θα εξαλείψει την ανάγκη να εισάγετε password με τον pacman. Δείτε το άρθρο στο wiki για το [Sudo](/index.php/Sudo "Sudo") για λεπτομερείς πληροφορίες.

Το επόμενο βήμα είναι να αποφασίσετε που θέλετε να τοποθετούνται τα χτισμένα σας πακέτα, για παράδειγμα μπορείτε να τα έχετε κάτω από το /home σας σε ένα ξεχωριστό φάκελο. Μπορείτε να παραλείψετε αυτό το βήμα κ τα πακέτα σας θα δημιουργούνται στον ίδιο φάκελο όπου αρχίσατε την makepkg.

Δημιουργείστε τον φάκελο

```
mkdir /home/$USER/packages

```

Μετά τροποποιήστε τον μεταβλητή PKGDEST στο αρχείο /etc/makepkg.conf ανάλογα.

Όσο βρίσκεστε εδώ, μπορείτε να ρίξετε μια ματιά και στις άλλες μεταβλητές στο makepkg.conf. Για παράδειγμα, μπορείτε να επεξεργαστείτε την PACKAGER, ή να αφαιρέσετε τα ! από το docs στην προκαθορισμένη σειρά OPTIONS, σε περίπτωση που δεν θέλετε ο φάκελος /usr/share/doc/<onoma_paketou> να διαγράφεται από την makepkg. ΔΕίτε το [Makepkg.conf](/index.php/Makepkg.conf "Makepkg.conf") για περισσότερες πληροφορίες.

## Χτίζοντας ένα πακέτο

Για να χτίσετε ένα πακέτο χρειάζεται είτε να δημιουργήσετε ένα όπως περιγράφετε στο [Creating packages](/index.php/Creating_packages "Creating packages"), ή να πάρετε ένα από το [AUR](https://aur.archlinux.org) ή το [ABS](/index.php/ABS "ABS") (δείτε παραπάνω) ή από κάποια άλλη πηγή. Θα πρέπει να είστε προσεκτικοί στο από που παίρνετε τα πακέτα σας, και να εγκαθιστάτε μόνο εκείνα τις πηγές των οποίων εμπιστεύεστε.

Ας πούμε ότι βρήκατε ένα εξαιρετικό πακέτο στο AUR που θέλετε να χτίσετε και να εγκαταστήσετε (σε αυτό το παράδειγμα θα χρησιμοποιήσουμε το "rufus", ένα torrent client βασισμένο σε Python). Μπορείτε να πάρετε το `PKGBUILD` του και όσα αρχεία χρειάζονται από [την σελίδα του στο AUR](https://aur.archlinux.org/packages.php?do_Details=1&ID=3394), κάντε κλικ στο link του "Tarball"

```
cd /path/to/file
tar -zxf rufus.tar.gz
cd rufus

```

Θα παρατηρήσετε ότι υπάρχουν κάποια αρχεία κάτω από αυτόν τον φάκελο, συμπεριλαμβανομένου του `PKGBUILD` script που χρησιμοποιείται για να χτιστεί το πακέτο. Για να χτίσετε το πακέτο, δώστε απλά την εντολή (σαν απλός χρήστης):

```
makepkg

```

αυτή τότε θα ετοιμάσει, θα κατεβάσει και θα προσπαθήσει να χτίσει το πακέτο σας. Εάν δεν έχετε όλες τις απαραίτητες εξαρτήσεις εγκατεστημένες, η `makepkg` θα σας προειδοποιήσει πριν να αποτύχει. Για να χτίσετε το πακέτο σας και να εγκαταστήσετε αυτές τις εξαρτήσεις, απλά χρησιμοποιείστε την εντολή:

```
makepkg -s

```

Πρέπει να σημειωθεί ότι αυτές οι εξαρτήσεις πρέπει να υπάρχουν στα αποθετήρια που έχετε ρυθμίσει να χρησιμοποιούνται από το σύστημα σας. Εναλλακτικά μπορείτε από χειροκίνητα να κατεβάσετε πρώτα τα πακέτα χρησιμοποιώντας την: `pacman -S dep1 dep2 klp`

Όταν όλες οι εξαρτήσεις έχουν ικανοποιηθεί και το πακέτο σας χτιστεί επιτυχώς θα πρέπει να έχετε το αρχείο rufus-0.7.0-1.pkg.tar.gz στο φάκελο απ' τον οποίο τρέξατε το `makepkg`. Για να το εγκαταστήσετε (σαν υπερχρήστης -- root), δώστε την εντολή:

```
pacman -U rufus-0.7.0-1.pkg.tar.gz

```

## Εγκαθιστώντας από buildscripts

Μερικές φορές παίρνουμε από τα αποθετήρια τρίτων μόνο τα αρχεία *.pkgbuild. Σε αυτήν την περίπτωση χρησιμοποιούμε:-

**makepkg -p**

Συγχαρητήρια! Τώρα έχετε εγκαταστήσει επιτυχώς το δικό σας πακέτο!

## Χρήσιμοι Σύνδεσμοι

*   [A helpful guide to makepkg/ABS](https://bbs.archlinux.org/viewtopic.php?t=1590)
*   [Creating packages](/index.php/Creating_packages "Creating packages")
*   [AUR](https://aur.archlinux.org)
*   [the Makepkg man page](https://www.archlinux.org/pacman/makepkg.8.html)
*   [Arch CVS & SVN PKGBUILD guidelines](/index.php/Arch_CVS_%26_SVN_PKGBUILD_guidelines "Arch CVS & SVN PKGBUILD guidelines")
*   [Makepkg.conf](/index.php/Makepkg.conf "Makepkg.conf")

Retrieved from "[https://wiki.archlinux.org/index.php?title=Makepkg_(Ελληνικά)&oldid=411592](https://wiki.archlinux.org/index.php?title=Makepkg_(Ελληνικά)&oldid=411592)"

[Categories](/index.php/Special:Categories "Special:Categories"):

*   [Package management (Ελληνικά)](/index.php/Category:Package_management_(%CE%95%CE%BB%CE%BB%CE%B7%CE%BD%CE%B9%CE%BA%CE%AC) "Category:Package management (Ελληνικά)")
*   [Package development (Ελληνικά)](/index.php/Category:Package_development_(%CE%95%CE%BB%CE%BB%CE%B7%CE%BD%CE%B9%CE%BA%CE%AC) "Category:Package development (Ελληνικά)")