Το **VirtualBox** είναι ένας [υπερεπόπτης](https://en.wikipedia.org/wiki/Hypervisor "wikipedia:Hypervisor") (hypervisor) που χρησιμοποιείται για να τρέχουμε λειτουργικά συστήματα σε ένα ιδιαίτερο περιβάλλον, που λέγεται εικονική μηχανή (virtual machine) και που τρέχει πάνω από το υπάρχον λειτουργικό σύστημα. Βρίσκεται υπό συνεχή εξέλιξη και διαρκώς του προστίθενται νέα χαρακτηριστικά. Είναι εφοδιασμένο με διεπαφή γραφικού περιβάλλοντος (GUI) που έχει αναπτυχθεί σε [Qt](/index.php/Qt "Qt"), καθώς και με εργαλεία γραμμής εντολών (command line tools) είτε χωρίς κεφαλίδες (headless) είτε σε [SDL](https://en.wikipedia.org/wiki/SDL "wikipedia:SDL"), για τη διαχείριση και τη λειτουργία εικονικών μηχανών.

Για να μπορεί να ενσωματώνει λειτουργίες του συστήματος βάσης (host) στο φιλοξενούμενο σύστημα (guest), στις οποίες συμπεριλαμβάνονται κοινοί φάκελοι και κοινό πρόχειρο (clipboard), επιτάχυνση γραφικών (video acceleration) και αδιάλειπτη λειτουργία ενσωμάτωσης παραθύρων (seamless window integration mode), διατίθεται το πακέτο guest additions για κάποια εικονικά λειτουργικά συστήματα.

## Contents

*   [1 Εγκατάσταση στον υπολογιστή βάσης](#.CE.95.CE.B3.CE.BA.CE.B1.CF.84.CE.AC.CF.83.CF.84.CE.B1.CF.83.CE.B7_.CF.83.CF.84.CE.BF.CE.BD_.CF.85.CF.80.CE.BF.CE.BB.CE.BF.CE.B3.CE.B9.CF.83.CF.84.CE.AE_.CE.B2.CE.AC.CF.83.CE.B7.CF.82)
    *   [1.1 Host με επεξεργασμένο (custom) πυρήνα](#Host_.CE.BC.CE.B5_.CE.B5.CF.80.CE.B5.CE.BE.CE.B5.CF.81.CE.B3.CE.B1.CF.83.CE.BC.CE.AD.CE.BD.CE.BF_.28custom.29_.CF.80.CF.85.CF.81.CE.AE.CE.BD.CE.B1)
*   [2 Στήσιμο](#.CE.A3.CF.84.CE.AE.CF.83.CE.B9.CE.BC.CE.BF)
    *   [2.1 Προσθήκη ονομάτων χρηστών στην ομάδα (group) vboxusers](#.CE.A0.CF.81.CE.BF.CF.83.CE.B8.CE.AE.CE.BA.CE.B7_.CE.BF.CE.BD.CE.BF.CE.BC.CE.AC.CF.84.CF.89.CE.BD_.CF.87.CF.81.CE.B7.CF.83.CF.84.CF.8E.CE.BD_.CF.83.CF.84.CE.B7.CE.BD_.CE.BF.CE.BC.CE.AC.CE.B4.CE.B1_.28group.29_vboxusers)
    *   [2.2 Φόρτωση αρθρωμάτων πυρήνα](#.CE.A6.CF.8C.CF.81.CF.84.CF.89.CF.83.CE.B7_.CE.B1.CF.81.CE.B8.CF.81.CF.89.CE.BC.CE.AC.CF.84.CF.89.CE.BD_.CF.80.CF.85.CF.81.CE.AE.CE.BD.CE.B1)
    *   [2.3 Ο δίσκος Guest additions](#.CE.9F_.CE.B4.CE.AF.CF.83.CE.BA.CE.BF.CF.82_Guest_additions)
    *   [2.4 Εκκίνηση εικόνας live δίσκου](#.CE.95.CE.BA.CE.BA.CE.AF.CE.BD.CE.B7.CF.83.CE.B7_.CE.B5.CE.B9.CE.BA.CF.8C.CE.BD.CE.B1.CF.82_live_.CE.B4.CE.AF.CF.83.CE.BA.CE.BF.CF.85)
    *   [2.5 Εκκίνηση εικονικών μηχανών με ενεργή μια υπηρεσία](#.CE.95.CE.BA.CE.BA.CE.AF.CE.BD.CE.B7.CF.83.CE.B7_.CE.B5.CE.B9.CE.BA.CE.BF.CE.BD.CE.B9.CE.BA.CF.8E.CE.BD_.CE.BC.CE.B7.CF.87.CE.B1.CE.BD.CF.8E.CE.BD_.CE.BC.CE.B5_.CE.B5.CE.BD.CE.B5.CF.81.CE.B3.CE.AE_.CE.BC.CE.B9.CE.B1_.CF.85.CF.80.CE.B7.CF.81.CE.B5.CF.83.CE.AF.CE.B1)
*   [3 Το Arch Linux ως guest σύστημα σε εικονική μηχανή](#.CE.A4.CE.BF_Arch_Linux_.CF.89.CF.82_guest_.CF.83.CF.8D.CF.83.CF.84.CE.B7.CE.BC.CE.B1_.CF.83.CE.B5_.CE.B5.CE.B9.CE.BA.CE.BF.CE.BD.CE.B9.CE.BA.CE.AE_.CE.BC.CE.B7.CF.87.CE.B1.CE.BD.CE.AE)
    *   [3.1 Εγκατάσταση των Guest Additions](#.CE.95.CE.B3.CE.BA.CE.B1.CF.84.CE.AC.CF.83.CF.84.CE.B1.CF.83.CE.B7_.CF.84.CF.89.CE.BD_Guest_Additions)
    *   [3.2 Αυτόματη αναμεταγλώττιση (re-compilation) των αρθρωμάτων guest του VirtualBox σε κάθε ενημέρωση οποιουδήποτε πυρήνα](#.CE.91.CF.85.CF.84.CF.8C.CE.BC.CE.B1.CF.84.CE.B7_.CE.B1.CE.BD.CE.B1.CE.BC.CE.B5.CF.84.CE.B1.CE.B3.CE.BB.CF.8E.CF.84.CF.84.CE.B9.CF.83.CE.B7_.28re-compilation.29_.CF.84.CF.89.CE.BD_.CE.B1.CF.81.CE.B8.CF.81.CF.89.CE.BC.CE.AC.CF.84.CF.89.CE.BD_guest_.CF.84.CE.BF.CF.85_VirtualBox_.CF.83.CE.B5_.CE.BA.CE.AC.CE.B8.CE.B5_.CE.B5.CE.BD.CE.B7.CE.BC.CE.AD.CF.81.CF.89.CF.83.CE.B7_.CE.BF.CF.80.CE.BF.CE.B9.CE.BF.CF.85.CE.B4.CE.AE.CF.80.CE.BF.CF.84.CE.B5_.CF.80.CF.85.CF.81.CE.AE.CE.BD.CE.B1)
    *   [3.3 Εκκίνηση των διαμοιραζόμενων υπηρεσιών](#.CE.95.CE.BA.CE.BA.CE.AF.CE.BD.CE.B7.CF.83.CE.B7_.CF.84.CF.89.CE.BD_.CE.B4.CE.B9.CE.B1.CE.BC.CE.BF.CE.B9.CF.81.CE.B1.CE.B6.CF.8C.CE.BC.CE.B5.CE.BD.CF.89.CE.BD_.CF.85.CF.80.CE.B7.CF.81.CE.B5.CF.83.CE.B9.CF.8E.CE.BD)
    *   [3.4 Χρήση USB webcam / μικροφώνου](#.CE.A7.CF.81.CE.AE.CF.83.CE.B7_USB_webcam_.2F_.CE.BC.CE.B9.CE.BA.CF.81.CE.BF.CF.86.CF.8E.CE.BD.CE.BF.CF.85)
    *   [3.5 Χρήση του Arch σε περιβάλλον VirtualBox με εκκίνηση EFI](#.CE.A7.CF.81.CE.AE.CF.83.CE.B7_.CF.84.CE.BF.CF.85_Arch_.CF.83.CE.B5_.CF.80.CE.B5.CF.81.CE.B9.CE.B2.CE.AC.CE.BB.CE.BB.CE.BF.CE.BD_VirtualBox_.CE.BC.CE.B5_.CE.B5.CE.BA.CE.BA.CE.AF.CE.BD.CE.B7.CF.83.CE.B7_EFI)
    *   [3.6 Συγχρονισμός ημερομηνίας/ώρας μεταξύ guest και host](#.CE.A3.CF.85.CE.B3.CF.87.CF.81.CE.BF.CE.BD.CE.B9.CF.83.CE.BC.CF.8C.CF.82_.CE.B7.CE.BC.CE.B5.CF.81.CE.BF.CE.BC.CE.B7.CE.BD.CE.AF.CE.B1.CF.82.2F.CF.8E.CF.81.CE.B1.CF.82_.CE.BC.CE.B5.CF.84.CE.B1.CE.BE.CF.8D_guest_.CE.BA.CE.B1.CE.B9_host)
    *   [3.7 Ενεργοποίηση κοινόχρηστων φακέλων](#.CE.95.CE.BD.CE.B5.CF.81.CE.B3.CE.BF.CF.80.CE.BF.CE.AF.CE.B7.CF.83.CE.B7_.CE.BA.CE.BF.CE.B9.CE.BD.CF.8C.CF.87.CF.81.CE.B7.CF.83.CF.84.CF.89.CE.BD_.CF.86.CE.B1.CE.BA.CE.AD.CE.BB.CF.89.CE.BD)
*   [4 Εξαγωγή των εικονικών μηχανών του VB για χρήση από άλλους hypervisors](#.CE.95.CE.BE.CE.B1.CE.B3.CF.89.CE.B3.CE.AE_.CF.84.CF.89.CE.BD_.CE.B5.CE.B9.CE.BA.CE.BF.CE.BD.CE.B9.CE.BA.CF.8E.CE.BD_.CE.BC.CE.B7.CF.87.CE.B1.CE.BD.CF.8E.CE.BD_.CF.84.CE.BF.CF.85_VB_.CE.B3.CE.B9.CE.B1_.CF.87.CF.81.CE.AE.CF.83.CE.B7_.CE.B1.CF.80.CF.8C_.CE.AC.CE.BB.CE.BB.CE.BF.CF.85.CF.82_hypervisors)
    *   [4.1 Αφαιρέστε τα πρόσθετα (additions)](#.CE.91.CF.86.CE.B1.CE.B9.CF.81.CE.AD.CF.83.CF.84.CE.B5_.CF.84.CE.B1_.CF.80.CF.81.CF.8C.CF.83.CE.B8.CE.B5.CF.84.CE.B1_.28additions.29)
    *   [4.2 Χρήση του σωστού format για τον εικονικό δίσκο](#.CE.A7.CF.81.CE.AE.CF.83.CE.B7_.CF.84.CE.BF.CF.85_.CF.83.CF.89.CF.83.CF.84.CE.BF.CF.8D_format_.CE.B3.CE.B9.CE.B1_.CF.84.CE.BF.CE.BD_.CE.B5.CE.B9.CE.BA.CE.BF.CE.BD.CE.B9.CE.BA.CF.8C_.CE.B4.CE.AF.CF.83.CE.BA.CE.BF)
        *   [4.2.1 Formats που χρησιμοποιεί το VirtualBox](#Formats_.CF.80.CE.BF.CF.85_.CF.87.CF.81.CE.B7.CF.83.CE.B9.CE.BC.CE.BF.CF.80.CE.BF.CE.B9.CE.B5.CE.AF_.CF.84.CE.BF_VirtualBox)
        *   [4.2.2 Διαφορές συγκεκριμένων format εικονικών δίσκων](#.CE.94.CE.B9.CE.B1.CF.86.CE.BF.CF.81.CE.AD.CF.82_.CF.83.CF.85.CE.B3.CE.BA.CE.B5.CE.BA.CF.81.CE.B9.CE.BC.CE.AD.CE.BD.CF.89.CE.BD_format_.CE.B5.CE.B9.CE.BA.CE.BF.CE.BD.CE.B9.CE.BA.CF.8E.CE.BD_.CE.B4.CE.AF.CF.83.CE.BA.CF.89.CE.BD)
        *   [4.2.3 Μετατροπή του format του εικονικού δίσκου](#.CE.9C.CE.B5.CF.84.CE.B1.CF.84.CF.81.CE.BF.CF.80.CE.AE_.CF.84.CE.BF.CF.85_format_.CF.84.CE.BF.CF.85_.CE.B5.CE.B9.CE.BA.CE.BF.CE.BD.CE.B9.CE.BA.CE.BF.CF.8D_.CE.B4.CE.AF.CF.83.CE.BA.CE.BF.CF.85)
    *   [4.3 Δημιουργήστε τη διαμόρφωση της εικονικής μηχανής για τον υπερεπόπτη σας](#.CE.94.CE.B7.CE.BC.CE.B9.CE.BF.CF.85.CF.81.CE.B3.CE.AE.CF.83.CF.84.CE.B5_.CF.84.CE.B7_.CE.B4.CE.B9.CE.B1.CE.BC.CF.8C.CF.81.CF.86.CF.89.CF.83.CE.B7_.CF.84.CE.B7.CF.82_.CE.B5.CE.B9.CE.BA.CE.BF.CE.BD.CE.B9.CE.BA.CE.AE.CF.82_.CE.BC.CE.B7.CF.87.CE.B1.CE.BD.CE.AE.CF.82_.CE.B3.CE.B9.CE.B1_.CF.84.CE.BF.CE.BD_.CF.85.CF.80.CE.B5.CF.81.CE.B5.CF.80.CF.8C.CF.80.CF.84.CE.B7_.CF.83.CE.B1.CF.82)
*   [5 Προχωρημένη διαμόρφωση](#.CE.A0.CF.81.CE.BF.CF.87.CF.89.CF.81.CE.B7.CE.BC.CE.AD.CE.BD.CE.B7_.CE.B4.CE.B9.CE.B1.CE.BC.CF.8C.CF.81.CF.86.CF.89.CF.83.CE.B7)
    *   [5.1 Αντικατάσταση του εικονικού δίσκου «με το χέρι» από το αρχείο _.vbox_](#.CE.91.CE.BD.CF.84.CE.B9.CE.BA.CE.B1.CF.84.CE.AC.CF.83.CF.84.CE.B1.CF.83.CE.B7_.CF.84.CE.BF.CF.85_.CE.B5.CE.B9.CE.BA.CE.BF.CE.BD.CE.B9.CE.BA.CE.BF.CF.8D_.CE.B4.CE.AF.CF.83.CE.BA.CE.BF.CF.85_.C2.AB.CE.BC.CE.B5_.CF.84.CE.BF_.CF.87.CE.AD.CF.81.CE.B9.C2.BB_.CE.B1.CF.80.CF.8C_.CF.84.CE.BF_.CE.B1.CF.81.CF.87.CE.B5.CE.AF.CE.BF_.vbox)
*   [6 Αντιμετώπιση προβλημάτων](#.CE.91.CE.BD.CF.84.CE.B9.CE.BC.CE.B5.CF.84.CF.8E.CF.80.CE.B9.CF.83.CE.B7_.CF.80.CF.81.CE.BF.CE.B2.CE.BB.CE.B7.CE.BC.CE.AC.CF.84.CF.89.CE.BD)
    *   [6.1 VBOX_E_INVALID_OBJECT_STATE (0x80BB0007)](#VBOX_E_INVALID_OBJECT_STATE_.280x80BB0007.29)
    *   [6.2 Το υποσύστημα USB δεν λειτουργεί στο host ή στο guest σύστημα](#.CE.A4.CE.BF_.CF.85.CF.80.CE.BF.CF.83.CF.8D.CF.83.CF.84.CE.B7.CE.BC.CE.B1_USB_.CE.B4.CE.B5.CE.BD_.CE.BB.CE.B5.CE.B9.CF.84.CE.BF.CF.85.CF.81.CE.B3.CE.B5.CE.AF_.CF.83.CF.84.CE.BF_host_.CE.AE_.CF.83.CF.84.CE.BF_guest_.CF.83.CF.8D.CF.83.CF.84.CE.B7.CE.BC.CE.B1)
    *   [6.3 Αποτυχία δημιουργίας της μόνο-host-διεπαφής δικτύου](#.CE.91.CF.80.CE.BF.CF.84.CF.85.CF.87.CE.AF.CE.B1_.CE.B4.CE.B7.CE.BC.CE.B9.CE.BF.CF.85.CF.81.CE.B3.CE.AF.CE.B1.CF.82_.CF.84.CE.B7.CF.82_.CE.BC.CF.8C.CE.BD.CE.BF-host-.CE.B4.CE.B9.CE.B5.CF.80.CE.B1.CF.86.CE.AE.CF.82_.CE.B4.CE.B9.CE.BA.CF.84.CF.8D.CE.BF.CF.85)
    *   [6.4 WinXP: Το βάθος χρώματος δεν μπορεί να είναι μεγαλύτερο από 16 bits](#WinXP:_.CE.A4.CE.BF_.CE.B2.CE.AC.CE.B8.CE.BF.CF.82_.CF.87.CF.81.CF.8E.CE.BC.CE.B1.CF.84.CE.BF.CF.82_.CE.B4.CE.B5.CE.BD_.CE.BC.CF.80.CE.BF.CF.81.CE.B5.CE.AF_.CE.BD.CE.B1_.CE.B5.CE.AF.CE.BD.CE.B1.CE.B9_.CE.BC.CE.B5.CE.B3.CE.B1.CE.BB.CF.8D.CF.84.CE.B5.CF.81.CE.BF_.CE.B1.CF.80.CF.8C_16_bits)
    *   [6.5 Φόρτωση εικόνων .vdi](#.CE.A6.CF.8C.CF.81.CF.84.CF.89.CF.83.CE.B7_.CE.B5.CE.B9.CE.BA.CF.8C.CE.BD.CF.89.CE.BD_.vdi)
    *   [6.6 Δεν δουλεύει η Αντιγραφή/Επικόλληση (Copy/Paste) στον guest με Arch Linux](#.CE.94.CE.B5.CE.BD_.CE.B4.CE.BF.CF.85.CE.BB.CE.B5.CF.8D.CE.B5.CE.B9_.CE.B7_.CE.91.CE.BD.CF.84.CE.B9.CE.B3.CF.81.CE.B1.CF.86.CE.AE.2F.CE.95.CF.80.CE.B9.CE.BA.CF.8C.CE.BB.CE.BB.CE.B7.CF.83.CE.B7_.28Copy.2FPaste.29_.CF.83.CF.84.CE.BF.CE.BD_guest_.CE.BC.CE.B5_Arch_Linux)
    *   [6.7 Χρήση σειριακής θύρας στο φιλοξενούμενο (guest) λειτουργικό σύστημα](#.CE.A7.CF.81.CE.AE.CF.83.CE.B7_.CF.83.CE.B5.CE.B9.CF.81.CE.B9.CE.B1.CE.BA.CE.AE.CF.82_.CE.B8.CF.8D.CF.81.CE.B1.CF.82_.CF.83.CF.84.CE.BF_.CF.86.CE.B9.CE.BB.CE.BF.CE.BE.CE.B5.CE.BD.CE.BF.CF.8D.CE.BC.CE.B5.CE.BD.CE.BF_.28guest.29_.CE.BB.CE.B5.CE.B9.CF.84.CE.BF.CF.85.CF.81.CE.B3.CE.B9.CE.BA.CF.8C_.CF.83.CF.8D.CF.83.CF.84.CE.B7.CE.BC.CE.B1)
    *   [6.8 Το σύστημα κλείνει κατά την επαναφορά](#.CE.A4.CE.BF_.CF.83.CF.8D.CF.83.CF.84.CE.B7.CE.BC.CE.B1_.CE.BA.CE.BB.CE.B5.CE.AF.CE.BD.CE.B5.CE.B9_.CE.BA.CE.B1.CF.84.CE.AC_.CF.84.CE.B7.CE.BD_.CE.B5.CF.80.CE.B1.CE.BD.CE.B1.CF.86.CE.BF.CF.81.CE.AC)
    *   [6.9 Εικόνες συστημάτων σε Btrfs](#.CE.95.CE.B9.CE.BA.CF.8C.CE.BD.CE.B5.CF.82_.CF.83.CF.85.CF.83.CF.84.CE.B7.CE.BC.CE.AC.CF.84.CF.89.CE.BD_.CF.83.CE.B5_Btrfs)
    *   [6.10 Windows 8.x Error Code 0x000000C4](#Windows_8.x_Error_Code_0x000000C4)
    *   [6.11 Η εικονική μηχανή με τα Windows 8 δεν εκκινεί και δίνει σφάλμα "ERR_DISK_FULL"](#.CE.97_.CE.B5.CE.B9.CE.BA.CE.BF.CE.BD.CE.B9.CE.BA.CE.AE_.CE.BC.CE.B7.CF.87.CE.B1.CE.BD.CE.AE_.CE.BC.CE.B5_.CF.84.CE.B1_Windows_8_.CE.B4.CE.B5.CE.BD_.CE.B5.CE.BA.CE.BA.CE.B9.CE.BD.CE.B5.CE.AF_.CE.BA.CE.B1.CE.B9_.CE.B4.CE.AF.CE.BD.CE.B5.CE.B9_.CF.83.CF.86.CE.AC.CE.BB.CE.BC.CE.B1_.22ERR_DISK_FULL.22)
*   [7 Ἐξωτερικοί σύνδεσμοι](#.E1.BC.98.CE.BE.CF.89.CF.84.CE.B5.CF.81.CE.B9.CE.BA.CE.BF.CE.AF_.CF.83.CF.8D.CE.BD.CE.B4.CE.B5.CF.83.CE.BC.CE.BF.CE.B9)

## Εγκατάσταση στον υπολογιστή βάσης

Η βασική σουίτα του VirtualBox, που καλύπτεται από την άδεια GPL, μπορεί να [εγκατασταθεί](/index.php/Pacman "Pacman") από τα [επίσημα αποθετήρια](/index.php/Official_repositories "Official repositories") με το πακέτο [virtualbox](https://www.archlinux.org/packages/?name=virtualbox).

Το πακέτο [virtualbox-host-modules](https://www.archlinux.org/packages/?name=virtualbox-host-modules), που περιέχει τα προ-μεταγλωττισμένα αρθρώματα για τον κοινό πυρήνα του archlinux, θα πρέπει να έχει εγκατασταθεί μαζί με τη σουίτα. Αν χρησιμοποιείτε τον πυρήνα [linux-lts](https://www.archlinux.org/packages/?name=linux-lts), θα πρέπει να εγκαταστήσετε μόνοι σας το πακέτο [virtualbox-host-modules-lts](https://www.archlinux.org/packages/?name=virtualbox-host-modules-lts). Για επεξεργασμένους (custom) πυρήνες, διαβάστε [παρακάτω](#Hosts_running_a_custom_kernel).

Προκειμένου να χρησιμοποιήσετε την διεπαφή γραφικού περιβάλλοντος, που βασίζεται στην πλατφόρμα [Qt](/index.php/Qt "Qt") (εντολή `VirtualBox`), θα χρειαστεί να εγκαταστήσετε επίσης το πακέτο [qt4](https://www.archlinux.org/packages/?name=qt4). Κάτι τέτοιο δεν χρειάζεται για το απλούστερο γραφικό περιβάλλον SDL (εντολή `VBoxSDL`) ούτε για την εντολή `VBoxHeadless`.

### Host με επεξεργασμένο (custom) πυρήνα

Το VirtualBox συνεργάζεται πολύ καλά με custom πυρήνες, όπως ο πυρήνας [Linux-ck](/index.php/Linux-ck "Linux-ck"), _χωρίς_ να χρειάζεται να διατηρηθεί κάποιο από τα πακέτα του επίσημου πυρήνα ArchLinux στο σύστημα. Δεδομένου ότι αυτά τα επίσημα πακέτα είναι εξαρτήσεις του πακέτου `virtualbox-host-modules`, αν θέλετε να αποτρέψετε τον pacman να εγκαταστήσει αυτά τα περιττά πακέτα, προτείνεται να εγκαταστήσετε το πακέτο [virtualbox-host-dkms](https://www.archlinux.org/packages/?name=virtualbox-host-dkms). Αυτό το τελευταίο έρχεται μαζί με τον πηγαίο κώδικα των αρθρωμάτων πυρήνα του VirtualBox που θα χρησιμοποιηθεί για τη δημιουργία τους έτσι, ώστε να ταιριάζουν με τον πυρήνα σας.

Από τη στιγμή που θα εγκατασταθεί το [virtualbox-host-dkms](https://www.archlinux.org/packages/?name=virtualbox-host-dkms), απλώς δημιουργήστε τα αρθρώματα πυρήνα για τον custom πυρήνα σας, τρέχοντας την εξής δομή εντολών:

```
# dkms install vboxhost/**<αριθμός έκδοσης του virtualbox-host-source>** -k **<όνομα του custom πυρήνα σας>**/**<αρχιτεκτονική του συστήματός σας>**

```

ή με την όλα-σε-ένα εντολή:

```
# dkms install vboxhost/$(pacman -Q virtualbox|awk {'print $2'}|sed 's/\-.\+//') -k $(uname -rm|sed 's/\ /\//')

```

**Σημείωση:** Αν πάρετε μήνυμα λάθους του τύπου:

`Your kernel headers for kernel **<το όνομα του custom πυρήνα σας>** cannot be found at /usr/lib/modules/<το όνομα του custom πυρήνα σας>/build or /usr/lib/modules/**<το όνομα του custom πυρήνα σας>**/source`

πιθανότατα δεν θα έχετε στο σύστημά σας τις κεφαλίδες (headers) πυρήνα που αντιστοιχούν στην έκδοση του custom πυρήνα σας

.

Αφού δημιουργήσετε το άρθρωμα του VirtualBox, το φορτώνετε με την:

```
# modprobe vboxdrv

```

Για να ξαναμεταγλωττίσετε/ξαναφορτώσετε το άρθρωμα VirtualBox στον πυρήνα σας, μετά από αναβάθμισή του, μπορείτε να ενεργοποιήσετε την υπηρεσία `dkms` με την εντολή:

```
# systemctl enable dkms

```

Αν δεν έχετε ενεργή την υπηρεσία `dkms` την ώρα που ενημερώνεται ο πυρήνας σας (επίσημος ή custom), το άρθρωμα VirtualBox δεν θα ενημερωθεί και ίσως να μη δουλεύει με τη νέα έκδοση του πυρήνα σας πλέον. Αν θέλετε να ξαναμεταγλωττίσετε/ενημερώσετε το άρθρωμα VirtualBox κατά την επανεκκίνηση του συστήματός σας μετά την εγκατάσταση νέας έκδοσης του πυρήνα, μπορείτε να χρησιμοποιήσετε ένα [άγκιστρο](/index.php/Mkinitcpio "Mkinitcpio") (hook) στο initramfs, το οποίο θα καλεί αυτόματα την εντολή `dkms` που προαναφέρθηκε.

Για να ενεργοποιήσετε αυτό το χαρακτηριστικό, εγκαθιστάτε το πακέτο [vboxhost-hook](https://aur.archlinux.org/packages/vboxhost-hook/) από το [AUR](/index.php/Arch_User_Repository "Arch User Repository") και προσθέτετε το `vboxhost` στο πεδίο HOOKS του αρχείου `/etc/mkinitcpio.conf`. Στη συνέχεια πρέπει να εξασφαλίσετε ότι ενημερώνεται πρώτα το πακέτο [linux-headers](https://www.archlinux.org/packages/?name=linux-headers) του συστήματός σας, με:

```
# pacman -Sy linux-headers && pacman -Su

```

**Σημείωση:** Όπως και το `dkms`, το άγκιστρο (hook) `vboxhost` θα σας ενημερώσει αν κάτι δεν πάει καλά κατά την επαναμεταγλώττιση του αρθρώματος του VirtualBox.

## Στήσιμο

### Προσθήκη ονομάτων χρηστών στην ομάδα (group) vboxusers

Προσθέστε τα ονόματα χρηστών που θέλετε στην [ομάδα](/index.php/Group "Group") `vboxusers`. Ενδέχεται όλα να δουλεύουν ρολόι και χωρίς αυτό το βήμα, αλλά οι κοινόχρηστοι φάκελοι - και πιθανώς κάποια άλλα προαιρετικά χαρακτηριστικά - τα χρειάζονται για να λειτουργήσουν. Η νέα ομάδα δεν εντάσσεται αυτόματα σε ενεργές συνεδρίες· ο χρήστης πρέπει να κάνει επανασύνδεση (log out / log in) ή να ξεκινήσει ένα νέο περιβάλλον με μία εντολή όπως `newgrp` ή `sudo -u $USER -s`. Η προσθήκη γίνεται με την:

```
# gpasswd -a $USER vboxusers

```

### Φόρτωση αρθρωμάτων πυρήνα

Τὸ VirtualBox σε host με Linux χρησιμοποιεί τα δικά του [αρθρώματα πυρήνα](/index.php/Kernel_modules "Kernel modules"), στα οποία περιλαμβάνεται ένα υποχρεωτικό άρθρωμα, το `vboxdrv`, που πρέπει να φορτωθεί πριν μπορέσουν να τρέξουν οι εικονικές μηχανές. Αυτό το άρθρωμα μπορεί να φορτώνεται αυτόματα με την εκκίνηση του ArchLinux ή μπορεί να φορτώνεται «με το χέρι» όποτε χρειάζεται.

Για να φορτώσετε το άρθρωμα με το χέρι:

```
# modprobe vboxdrv

```

Για νά φορτώσετε τη μονάδα δίσκου VirtualBox driver από την αρχή, ανατρέξτε στο [Kernel_modules#Loading](/index.php/Kernel_modules#Loading "Kernel modules") και χρησιμοποιήστε το όνομα αρχείου `virtualbox.conf`

**Σημείωση:** Προκειμένου να αποφύγετε μηνύματα λάθους του είδους `no such file or directory` κατά τη φόρτωση του `vboxdrv`, ίσως χρειαστεί να ενημερώσετε τη βάση δεδομένων με τα αρθρώματα του πυρήνα, μέσω της `depmod -a`.

Για να ξεκινήσετε τον γραφικό διαχειριστή του VirtualBox:

```
$ VirtualBox

```

Για να εξασφαλίσετε πλήρη λειτουργικότητα στις δικτυώσεις γέφυρας (bridged networking), βεβαιωθείτε ότι έχουν φορτωθεί προηγουμένως τα [αρθρώματα πυρήνα](/index.php/Kernel_modules "Kernel modules") `vboxnetadp`, `vboxnetflt` και `vboxpci` και ότι το πακέτο [net-tools](https://www.archlinux.org/packages/?name=net-tools) είναι ήδη εγκατεστημένο.

### Ο δίσκος Guest additions

Το πακέτο [virtualbox](https://www.archlinux.org/packages/?name=virtualbox) προτείνει επίσης την εγκατάσταση του [virtualbox-guest-iso](https://www.archlinux.org/packages/?name=virtualbox-guest-iso) στον υπολογιστή βάσης (host) που τρέχει το VirtualBox. Πρόκειται για μια εικόνα δίσκου που μπορεί να χρησιμοποιηθεί για την εγκατάσταση πρόσθετων δυνατοτήτων στα φιλοξενούμενα (guest) συστήματα. Μπορείτε να τον κάνετε διαθέσιμο σε κάποιο εν λειτουργία εικονικό σύστημα, πηγαίνοντας στο μενού Συσκευές (Devices) και δίνοντας _Install Guest Additions... Host+D_, για να τρέξετε την εγκατάσταση των πρόσθετων μέσα από το εικονικό σύστημα.

### Εκκίνηση εικόνας live δίσκου

Κάντε κλίκ στο κουμπί _Νέο_ (New) για να δημιουργήστε ένα νέο εικονικό περιβάλλον. Δώστε του ένα κατάλληλο όνομα και επιλέξτε τύπο και έκδοση λειτουργικού συστήματος. Επιλέξτε μέγεθος βασικής μνήμης (σημείωση: τα περισσότερα λειτουργικά συστήματα θα χρειαστούν τουλάχιστον 512 MiB για να λειτουργήσουν απρόσκοπτα). Δημιουργήστε μια καινούργια εικόνα σκληρού δίσκου (εικόνα σκληρού δίσκου είναι ένα αρχείο που θα περιέχει το σύστημα αρχείων και τα αρχεία του λειτουργικού συστήματος).

Όταν θα έχει δημιουργηθεί η νέα εικόνα, κάντε κλικ στο _Ιδιότητες_ (Settings), έπειτα στο _CD/DVD-ROM_, επιλέξτε με τικ στο κουτάκι του το _Mount CD/DVD Drive_ και μετά επιλέξτε μια εικόνα ISO.

### Εκκίνηση εικονικών μηχανών με ενεργή μια υπηρεσία

Παρακάτω θα βρείτε πώς μπορείτε να εγκαταστήσετε μια υπηρεσία systemd που θα χρησιμοποιηθεί για να αντιμετωπίσει το σύστημα την εικονική μηχανή ως υπηρεσία.

 `/etc/systemd/system/vboxvmservice@.service` 

```
[Unit]
Description=VBox Virtual Machine %i Service
Requires=systemd-modules-load.service
After=systemd-modules-load.service

[Service]
User=`**<user>**`
Group=vboxusers
ExecStart=/usr/bin/VBoxHeadless -s %i
ExecStop=/usr/bin/VBoxManage controlvm %i savestate

[Install]
WantedBy=multi-user.target
```

**Σημείωση:** Αντικαταστήστε το `**<user>**` με το όνομα ενός χρήστη-μέλους της ομάδας `vboxusers`. Βεβαιωθείτε ότι ο χρήστης που επιλέξατε είναι ο ίδιος χρήστης που θα δημιουργεί και θα εκκινεί τις εικονικές μηχανές, ειδάλλως δεν θα μπορεί να βλέπει τις εγκατεστημένες εικονικές μηχανές.

Για να ενεργοποιήσετε την υπηρεσία που θα ξεκινά την εικονική μηχανή στην επόμενη εκκίνηση συστήματος, δώστε:

```
# systemctl enable vboxvmservice@**your virtual machine name**

```

Για να ξεκινήσετε την υπηρεσία που θα ξεκινά απευθείας την εικονική μηχανή, δώστε:

```
# systemctl start vboxvmservice@**το όνομα της εικονικής μηχανής σας**

```

Από την έκδοση 4.2 του VirtualBox εισάγεται μια [νέα μέθοδος](http://lifeofageekadmin.com/how-to-set-your-virtualbox-vm-to-automatically-startup/) ώστε συστήματα τύπου UNIX να μπορούν να ξεκινούν αυτομάτως εικονικές μηχανές, σε αντικατάσταση της μεθόδου που καλεί υπηρεσία του systemd.

## Το Arch Linux ως guest σύστημα σε εικονική μηχανή

Η εγκατάσταση του Arch Linux σε εικονική μηχανή του VirtualBox γίνεται ακριβώς όπως και μια κανονική εγκατάσταση. Όμως οι προσθήκες (guest additions) θα πρέπει να εγκατασταθούν μέσω pacman (σύμφωνα με τις οδηγίες που ακολουθούν) και όχι μέσω της επιλογής Install Guest Additions από το μενού του VirtualBox στο σύστημα του υπολογιστή βάσης, ούτε με φόρτωση εικόνας ISO.

### Εγκατάσταση των Guest Additions

Εγκαταστήστε το πακέτο [virtualbox-guest-utils](https://www.archlinux.org/packages/?name=virtualbox-guest-utils). Τα αρθρώματα φορτώστε τα «με το χέρι», δίνοντας:

```
# modprobe -a vboxguest vboxsf vboxvideo

```

Φτιάξτε ένα αρχείο `*.conf` (π.χ. `virtualbox.conf`) στη διαδρομή `/etc/modules-load.d/`, το οποίο θα έχει αυτές τις γραμμές:

 `/etc/modules-load.d/virtualbox.conf` 

```
vboxguest
vboxsf
vboxvideo
```

Προσθέστε την ακόλουθη γραμμή στην κορυφή του `~/.xinitrc`, πάνω από όποια επιλογή `exec`. (Αν δεν υπάρχει το αρχείο, φτιάξτε ένα καινούργιο):

 `~/.xinitrc`  `/usr/bin/VBoxClient-all` 
**Σημείωση:** Αν φτιάξατε καινούργιο αρχείο `~/.xinitrc`, θα _πρέπει_ να συμπεριλάβετε και έναν [διαχειριστή παραθύρων](/index.php/Window_manager "Window manager") ή ένα [desktop environment](/index.php/Desktop_environment "Desktop environment").

### Αυτόματη αναμεταγλώττιση (re-compilation) των αρθρωμάτων guest του VirtualBox σε κάθε ενημέρωση οποιουδήποτε πυρήνα

Αυτό είναι εφικτό χάρη στο πακέτο [vboxguest-hook](https://aur.archlinux.org/packages/vboxguest-hook/) από τα αποθετήρια [AUR](/index.php/Arch_User_Repository "Arch User Repository"). Στο **vboxguest-hook** η 'αυτόματη αναμεταγλώττιση' εξασφαλίζεται μέσω ενός **άγκιστρου vboxguest** στο [mkinitcpio](/index.php/Mkinitcpio "Mkinitcpio") μετά την αναγκαστική ενημέρωση του πακέτου [linux-headers](https://www.archlinux.org/packages/?name=linux-headers). Θα χρειαστεί να προσθέσετε το `vboxguest` στο πεδίο των HOOKS στο αρχείο `/etc/mkinitcpio.conf`. Ίσως χρειαστεί να ξαναδημιουργήσετε μόνοι σας το initramfs μετά από αναβάθμιση του πακέτου [linux-headers](https://www.archlinux.org/packages/?name=linux-headers).

Το εν λόγω άγκιστρο θα καλέσει την εντολή `dkms` για να ενημερωθούν τα αρθρώματα VirtualBox guest modules για κάθε έκδοση του νέου πυρήνα σας.

**Σημείωση:** Αν χρησιμοποιείτε αυτή τη μέθοδο, είναι **σημαντικό** να παρακολουθείτε την πορεία της εγκατάστασης του [linux](https://www.archlinux.org/packages/?name=linux) (ή οποιουδήποτε άλλου πυρήνα. Το άγκιστρο vboxguest-hook θα σας ενημερώσει, αν κάτι δεν πάει καλά.

### Εκκίνηση των διαμοιραζόμενων υπηρεσιών

Μετά την εγκατάσταση του πακέτου [virtualbox-guest-utils](https://www.archlinux.org/packages/?name=virtualbox-guest-utils) που είδαμε πιο πάνω, θα πρέπει να ξεκινήσετε την εντολή `VBoxClient-all` για να ξεκινήσουν οι υπηρεσίες διαμοιρασμού του προχείρου (clipboard), του επανακαθορισμού μεγέθους της οθόνης κ.λπ.

*   Αν τρέχετε κάτι που ενεργοποιεί το `/etc/xdg/autostart/vboxclient.desktop`, όπως π.χ. το GNOME ή το KDE, δεν χρειάζετε να κάνετε τίποτε.
*   Αν, αντίθετα, χρησιμοποιείτε το `.xinitrc` για να ενεργοποιήσετε λειτουργίες, θα πρέπει να προσθέσετε στο αρχείο σας `.xinitrc` την εξής εντολή, πριν εκκινήσετε τον διαχειριστή παραθύρων σας:

```
# VBoxClient-all &

```

### Χρήση USB webcam / μικροφώνου

**Σημείωση:** Απαιτείται να έχετε εγκατεστημένο το πακέτο επεκτάσεων του VirtualBox πριν ακολουθήσετε τα βήματα που περιγράφονται παρακάτω. Δείτε το [VirtualBox_Extras#Extension_pack](/index.php/VirtualBox_Extras#Extension_pack "VirtualBox Extras") για περισσότερες λεπτομέρειες.

1.  Βεβαιωθείτε ότι δεν τρέχει η εικονική μηχανή σας και ότι δεν είναι σε χρήση η webcam και/ή το μικρόφωνό σας.
2.  Ανοίξτε το κεντρικό παράθυρο του VirtualBox και πηγαίνετε στις ρυθμίσεις για τη μηχανή του Arch. Πηγαίνετε στο πεδίο USB.
3.  Βεβαιωθείτε ότι έχει επιλεγεί το «Ενεργοποίηση ελεγκτή USB» (Enable USB controller). Επίσης βεβαιωθείτε ότι είναι επιλεγμένο το "Enable USB 2.0 (EHCI) Controller".
4.  Επιλέξτε το κουμπί «Προσθήκη φίλτρου από συσκευή» (Add filter from device) - είναι το καλώδιο με το +.
5.  Επιλέξτε τη USB συσκευή σας (webcam/μικρόφωνο) από τη λίστα
6.  Δώστε OK και ξεκινήστε την εικονική μηχανή σας.

### Χρήση του Arch σε περιβάλλον VirtualBox με εκκίνηση EFI

Η προσωπική μου εμπειρία με αυτές τις συνθήκες ήταν τρομακτική, αλλά το θέμα είναι ότι δουλεύει.

_UPD. Η χρήση του efibootmgr έχει το ίδιο αποτέλεσμα όπως και η χρήση του μενού εκκίνησης του VirtualBox (βλ. σημείωση παρακάτω): Οι ρυθμίσεις [χάνονται](https://www.virtualbox.org/ticket/11177) μετά το κλείσιμο της εικονικής μηχανής._ Εν πρώτοις, ο `efibootmgr` ΔΕΝ δουλεύει. Θα φαίνεται ότι δουλεύει, αλλά όλες οι αλλαγές που θα κάνει φαίνεται ότι ξαναγυρίζουν στις αρχικές ρυθμίσες μετά από επανεκκίνηση. Αφού κάνετε μία τυπική εγκατάσταση UEFI/GPT, δοκιμάστε να επανεκκινήσετε το σύστημα και θα βρεθείτε στο περιβάλλον με το κέλυφος του EFI. Δώστε exit και θα βρεθείτε σε ένα μενού. Εκεί επιλέξτε: Boot Management Manager, Boot Options, Add Boot Option. Με τον περιηγητή αρχείων σας (file browser) βρείτε το αρχείο του grub efi και επιλέξτε το. Αν θέλετε, προσθέστε του και μια ετικέτα (label). Έπειτα επιλέξτε Change Boot Order από το μενού, με τα βελάκια επιλέξτε το Arch και δώστε `+` για να το μετακινήσετε στην κορυφή της λίστας. Τώρα πια ο GRUB θα πρέπει να είναι η κατ' αρχήν επιλογή εκκίνησης.

Άλλες εναλλακτικές είναι: 1) πηγαίνετε την επιλογή φόρτωσης στο `\EFI\boot\bootx64.efi`, 2) δημιουργήστε ένα σκριπτάκι `\startup.nsh` που θα τρέχει το επιθυμητή πρόγραμμα φόρτωσης, κάπως έτσι:

 `\startup.nsh`  `HD16a0a1:\EFI\refind\refindx64.efi` 

Εδώ έδωσα ένα συμβατό όνομα για την απεικόνιση (mapping). Σαν ιδέα είναι μάλλον καλή, αφού επιβιώνει σε τυχόν αλλαγές προδιαγραφών.

**Σημείωση:** Ένας άλλος χρήσιμος τρόπος να ξαναγυρίσετε πίσω στο μενού EFI μετὰ από αυτόματη εκκίνηση είναι να πιέσετε το `c` μέσα στο περιβάλλον του GRUB και να πληκτρολογήσετε `exit`. Προφανώς αυτός ο τρόπος θα δουλέψει μόνο με το `grub-efi`, όχι με το `grub-bios.`

Μπορεί ακόμη να χρειάζεται αναδημιουργία του αρχείου `grub.cfg` προκειμένου να επιδιορθωθούν κατεστραμμένοι σύνδεσμοι UUID. Ελέγξτε την ορθότητά τους με την εντολή `lsblk -f`.

Τέλος, άλλος ένας χρήσιμος τρόπος να φτάσουμε στο μενού εκκίνησης του VirtualBox είναι να πατήσουμε `F12` αμέσως μόλις εκκινήσουμε την εικονική μηχανή. Είναι κάτι που βολεύει, όταν χρησιμοποιούμε, για παράδειγμα, rEFInd + EFISTUB.

### Συγχρονισμός ημερομηνίας/ώρας μεταξύ guest και host

Για να διατηρήσετε σε συγχρονισμό την ημερομηνία και την ώρα, βεβαιωθείτε ότι έχετε εγκατεστημένο το πακέτο [virtualbox-guest-utils](https://www.archlinux.org/packages/?name=virtualbox-guest-utils) στον υπολογιστή βάσης (host - δείτε [παραπάνω](#Install_the_Guest_Additions)). Για να έχετε ενεργή την υπηρεσία και σε επόμενες εκκινήσεις, τρέξτε την εντολή:

```
# systemctl enable vboxservice

```

Για να την ενεργοποιήσετε αμέσως, δώστε

```
# systemctl start vboxservice

```

Θα χρειαστεί να τρέξετε αυτόν τον «δαίμονα» και για να χρησιμοποιήσετε το χαρακτηριστικό της αυτόματης φόρτωσης (auto-mount) των κοινόχρηστων φακέλων, που προαναφέρθηκε.

### Ενεργοποίηση κοινόχρηστων φακέλων

Τους κοινόχρηστους φακέλους τους διαχειρίζεται το πρόγραμμα του VirtualBox στον host υπολογιστή. Από εκεί μπορούν να προστεθούν, να φορτώνονται αυτόματα και να χαρακτηρίζονται ως μόνον-ανάγνωσης (read-only).

Αν έχει ενεργοποιηθεί η αυτόματη φόρτωση (auto-mount) και είναι ενεργή και η υπηρεσία `vboxservice`, δημιουργώντας έναν κοινόχρηστο φάκελο μέσα από το πρόγραμμα VirtualBox του host υπολογιστή, θα φορτώσουμε αυτόν τον φάκελο και στον guest, στη διαδρομή `/media/sf__ΟΝΟΜΑ_ΚΟΙΝΟΧΡΗΣΤΟΥ-ΦΑΚΕΛΟΥ_`. Για να έχετε αυτόν τον φάκελο και στον Arch Guest, αφού έχετε εγκαταστήσει το Guest Additions, θα χρειαστεί να προσθέσετε το όνομα χρήστη σας στην ομάδα `vboxsf`:

```
# groupadd vboxsf
# gpasswd -a $USER vboxsf

```

**Σημείωση:** Για να λειτουργήσει η **αυτόματη φόρτωση**, θα πρέπει να ενεργοποιήσετε την υπηρεσία **vboxservice**.

Αν θέλετε να δημιουργήσετε έναν συμβολικό δεσμό (symlink) ανάμεσα σε έναν κοινόχρηστο φάκελο και κάποιον άλλο φάκελο του home καταλόγου σας, για ευκολότερη πρόσβαση, μπορείτε να δώσετε στο guest σύστημα:

```
$ ln -s /media/sf_Dropbox/* ~/dropbox

```

Το σκριπτ `VBoxLinuxAdditions.run` που περιέχεται στον εικονικό δίσκο (iso) των Guest Additions το κάνει αυτό από μόνο του. Ωστόσο στο Arch δεν συνιστάται να το χρησιμοποιήσετε. iso does this for you, however, Arch does not recommend using it.

Αν δεν φορτώνονται αυτόματα οι κοινόχρηστοι φάκελοί σας, δοκιμάστε αυτό: [manually mount](https://bbs.archlinux.org/viewtopic.php?id=70780).

Για να αποτρέψετε προβλήματα στην εκκίνηση κατά τη χρήση του [systemd](/index.php/Systemd "Systemd"), θα πρέπει να προσθέσετε το `comment=systemd.automount` στο αρχείο σας `/etc/fstab`. Κατ' αυτό τον τρόπο, θα γίνεται αυτόματη φόρτωση μόνο κατά την πρόσβαση στα αντίστοιχα σημεία πρόσβασης (mount points) και όχι κατά την εκκίνηση. Ειδάλλως, το σύστημα σας ενδέχεται να γίνει ασταθές μετά από μία αναβάθμιση πυρήνα (αν εγκαθιστάτε τα guest additions «με το χέρι»).

```
desktop   /media/desktop    vboxsf  uid=user,gid=group,rw,dmode=700,fmode=600,comment=systemd.automount 0 0

```

Μη χάνετε το χρόνο σας δοκιμάζοντας την επιλογή `nofail`. Το `mount.vboxsf` δεν είναι σε θέση να την χειριστεί (2012-08-20).

```
desktop   /media/desktop    vboxsf  uid=user,gid=group,rw,dmode=700,fmode=600,nofail 0 0

```

## Εξαγωγή των εικονικών μηχανών του VB για χρήση από άλλους hypervisors

Αν σκοπεύετε να χρησιμοποιήσετε την εικονική μηχανή που δημιουργήσατε με το VirtualBox σε άλλον υπολογιστή, που δεν έχει κατ' ανάγκην εγκατεστημένο VirtualBox, ίσως να ενδιαφέρεστε να ακολουθήσετε τα παρακάτω βήματα:

### Αφαιρέστε τα πρόσθετα (additions)

Αν έχετε εγκαταστήσει τα πρόσθετα (VirtualBox additions) του VirtualBox στην εικονική μηχανή σας, καλό είναι να τα απεγκαταστήσετε. Το guest μηχάνημά σας, ιδίως αν χρησιμοποιεί λειτουργικό σύστημα από την οικογένεια των Windows, ενδέχεται να αρχίσει να συμπεριφέρεται παράξενα, να «σπάσει» (crash) ή ακόμη και να μην εκκινεί καθόλου, αν χρησιμοποιήσετε τους ειδικούς οδηγούς (drivers) του VirtualBox σε άλλον υπερεπόπτη (hypervisor).

**Συμβουλή:** Αν σκοπεύετε να χρησιμοποιήσετε κάποια λύση εικονικοποίησης από την Parallels Inc για τον Mac σας, μπορείτε να χρησιμοποιήσετε το προϊόν της _Parallels Transporter_ για να φτιάξετε μια εικονική μηχανή από μιαν άλλη εικονική μηχανή Windows ή GNU/Linux (ή ακόμη κι από μια πραγματική εγκατάσταση). Με ένα τέτοιο προϊόν δεν υπάρχει λόγος να προχωρήσετε στο επόμενο βήμα και μπορείτε να σταματήσετε εδώ το διάβασμα.

### Χρήση του σωστού format για τον εικονικό δίσκο

#### Formats που χρησιμοποιεί το VirtualBox

Το VirtualBox εμπεριέχει δικό του τύπο εικονικών σκληρών δίσκων: Πρόκειται για αρχεία με format Virtual Disk Image (VDI). Όμως, ακόμα κι αν αυτό το format είναι προεπιλογή κατά τη δημιουργία εικονικής μηχανής μέσω του VirtualBox, μπορείτε να ορίσετε άλλο. Πράγματι, το VirtualBox υποστηρίζει άμεμπτα και άλλα format:

*   Το VMDK: Αυτό το format αναπτύχθηκε αρχικά από την VMware για τα προϊόντα της, αλλά σήμερα είναι πλέον ανοιχτό (open) format. Αν σκοπεύετε να χρησιμοποιήσετε κάποιο προϊόν της VMware, θα χρειαστεί να βαδίσετε με αυτό το format, αφού είναι το μόνο που υποστηρίζει η VMware.

*   Το VHD: Αυτό είναι το format που χρησιμοποιεί η Microsoft στα Windows Virtual PC και Hyper-V. Αν λογαριάζετε να χρησιμοποιήσετε οποιοδήποτε από αυτά τα προϊόντα της Microsoft, θα πρέπει να διαλέξετε αυτό το format.

**Συμβουλή:** Από τα Windows 7 και μετά, αυτό το format μπορεί να φορτωθεί απευθείας, χωρίς κάποια επιπρόσθετη εφαρμογή.

*   Η Version 2 του HDD format που χρησιμοποιεί η Parallels (Desktop for Mac).

*   Τα QED and QCOW που χρησιμοποιεί το QEMU.

Το ποιο format θα χρειαστεί να επιλέξετε εξαρτάται από τον υπερεπόπτη που θα χρησιμοποιήσετε.

#### Διαφορές συγκεκριμένων format εικονικών δίσκων

Πριν μετατρέψετε τον εικονικό δίσκο σας, καλό θα ήταν να λάβετε υπόψιν σας τις παρακάτω διαφορές συγκεκριμένων format εικονικών δίσκων:

*   Το VMDK προσφέρει τη δυνατότητα να «σπάσει» σε περισσότερα του ενός αρχεία μεγέθους μέχρι 2GB. Αυτό το χαρακτηριστικό είναι ιδιαίτερα χρήσιμο, αν θέλετε να αποθηκεύσετε την εικονική μηχανή σας σε υπολογιστές που δεν υποστηρίζουν πολύ μεγάλα αρχεία. Τα άλλα format δεν παρέχουν κάποιο αντίστοιχο χαρακτηριστικό.

*   Η αλλαγή στη λογική χωρητικότητα ενός ήδη υπάρχοντος εικονικού δίσκου μέσω της εντολής `VBoxManage` του VirtualBox υποστηρίζεται μόνο για τα format VDI και VHD που χρησιμοποιούνται στη λειτουργία δυναμικής εκχώρησης (dynamic allocation mode) για να μεγαλώσουν (και όχι για να μικρύνουν) τη χωρητικότητά τους.

#### Μετατροπή του format του εικονικού δίσκου

Το VirtualBox υποστηρίζει μόνο μετατροπές εικονικών δίσκων από και προς VDI, VMDK και VHD formats. Ακολουθεί ένα παράδειγμα μετατροπής εικονικού δίσκου VDI σε VMDK:

```
$ VBoxManage clonehd _ArchLinux_VM.vdi_ _ArchLinux_VM.vmdk_ --format _VMDK_

```

Αν θέλετε να αντικαταστήσετε τον εικονικό δίσκο που καθορίσατε όταν δημιουργήσατε την εικονική μηχανή σας με αυτόν που μόλις μετατρέψατε, χρησιμοποιήστε την εντολή `VBoxManage storagectl` (συμβουλευτείτε το εγχειρίδιο χρήσης [VirtualBox manual](https://www.virtualbox.org/manual)), ή χρησιμοποιήστε το γραφικό περιβάλλον, ή [τροποποιήστε το _.vbox_ configuration file](#Replace_the_virtual_disk_manually_from_the_.vbox_file).

### Δημιουργήστε τη διαμόρφωση της εικονικής μηχανής για τον υπερεπόπτη σας

Αν ο υπερεπόπτης σας (όπως π.χ. το VMware) δεν υποστηρίζει την εισαγωγή αρχείων διαμόρφωσης του VirtualBox (_.vbox_), θα χρειαστεί να φτιάξετε μια νέα εικονική μηχανή και να καθορίσετε τις προδιαγραφές της για προσομοίωση του hardware όσο γίνεται πιο παραπλήσιες προς εκείνες της αρχικής εικονικής μηχανής σας (του VirtualBox).

```
a new virtual machine and specify its hardware configuration as close as possible as your initial VirtualBox virtual machine.

```

**Σημείωση:** Δώστε ιδιαίτερη προσοχή στον τρόπο εγκατάστασης (BIOS ή UEFI) του guest λειτουργικού συστήματος. Ενώ στο VirtualBox υπάρχει διαθέσιμη επιλογή για να διαλέξετε ανάμεσα στους δύο αυτούς τρόπους, στο VMware θα πρέπει να προσθέσετε το εξής στο _.vmx_ αρχείο σας: `ArchLinux_vm.vmx`  `firmware = "efi"` 

Τέλος ζητήστε από τον υπερεπόπτη σας να χρησιμοποιήσει τον υπάρχοντα εικονικό δίσκο που μετατρέψατε και ξεκινήστε την εικονική μηχανή σας.

**Συμβουλή:** Αν χρησιμοποιείτε προϊόντα VMware και δεν θέλετε να διατρέξετε σε όλο το γραφικό περιβάλλον για να βρείτε την ακριβή τοποθεσία για τον νέο εικονικό δίσκο σας, μπορείτε να αντικαταστήσετε την τοποθεσία του τρέχοντος αρχείου _.vmdk_ επεμβαίνοντας «με το χέρι» στο αρχείο διαμόρφωσης _.vmx_.

## Προχωρημένη διαμόρφωση

### Αντικατάσταση του εικονικού δίσκου «με το χέρι» από το αρχείο _.vbox_

Αν θεωρείτε ότι η επεξεργασία ενός απλού _XML_ αρχείου σας βολεύει περισσότερο από το γραφικό περιβάλλον ή το `VBoxManage` και θέλετε να αντικαταστήσετε (ή να προσθέσετε) έναν εικονικό δίσκο στην εικονική μηχανή σας, τότε στο αρχείο διαμόρφωσης _.vbox_ που αντιστοιχεί στην εικονική μηχανή σας απλώς αντικαταστήστε το GUID, τη θέση του αρχείου και το φορμάτ του σύμφωνα με τις ανάγκες σας:

 `ArchLinux_vm.vbox`  `<HardDisk uuid="_{670157e5-8bd4-4f7b-8b96-9ee412a712b5}_" location="_ArchLinux_vm.vdi_" format="_VDI_" type="Normal"/>` 

και στη συνέχεια στην εγγραφή `<AttachedDevice>` του πεδίου `<StorageController>`, αντικαταστήστε το GUID με το καινούργιο.

 `ArchLinux_vm.vbox` 

```
<AttachedDevice type="HardDisk" port="0" device="0">
  <Image uuid="_{670157e5-8bd4-4f7b-8b96-9ee412a712b5}_"/>
</AttachedDevice>
```

**Σημείωση:** Αν δεν ξέρετε το GUID του δίσκου που θέλετε να προσθέσετε, αλλά έχετε μόλις χρησιμοποιήσει για τη μετατροπή το `VBoxManage`, αυτή η εντολή θα εμφανίσει το GUID αμέσως μετά από τη μετατροπή. Η χρήση τυχαίου GUID δεν λειτουργεί.

## Αντιμετώπιση προβλημάτων

### VBOX_E_INVALID_OBJECT_STATE (0x80BB0007)

Αυτό το μήνυμα σφάλματος μπορεί να προκύψει αν μια εικονική μηχανή τερμάτισε ανώμαλα. Η λύση για το «ξεκλείδωμα» της εικονικής μηχανής είναι τετριμμένη:

```
$ VBoxManage controlvm <your virtual machine name> poweroff

```

### Το υποσύστημα USB δεν λειτουργεί στο host ή στο guest σύστημα

Κάποιες φορές, σε παλιότερα μηχανήματα host με Linux, το υποσύστημα USB δεν ανιχνεύεται αυτόματα και έτσι προκύπτει μήνυμα λάθους του τύπου `Could not load the Host USB Proxy service: VERR_NOT_FOUND` ή δεν εμφανίζεται καν οδηγός USB στο host σύστημα, [ακόμα και αν ο χρήστης είναι μέλος της ομάδας **vboxusers**](https://bbs.archlinux.org/viewtopic.php?id=121377). Αυτό τοπρόβλημα οφείλεται στο γεγονός ότι το VirtualBox πέρασε από το _usbfs_ στο _sysfs_ από την έκδοση 3.0.8\. Αν το host σύστημα δεν αντιλαμβάνεται την αλλαγή, μπορείτε να επαναφέρετε την παλιά συμπεριφορά ορίζοντας την ακόλουθη μεταβλητή περιβάλλοντος που «πατάει» στο κέλυφός σας (π.χ.το αρχείο σας `~/.bashrc`, αν χρησιμοποιείτε _bash_):

 `~/.bashrc`  `VBOX_USB=usbfs` 

Έπειτα βεβαιωθείτε ότι το περιβάλλον έλαβε γνώση αυτής της αλλαγής (με επανασύνδεση, με πρόσβαση του αρχείου με το χέρι, με την εκκίνηση ενός νέου στιγμιότυπου του κελύφους ή με επανεκκίνηση).

Επίσης βεβαιωθείτε ότι ο χρήστης σας είναι μέλος της ομάδας `storage`.

### Αποτυχία δημιουργίας της μόνο-host-διεπαφής δικτύου

Για να μπορέσετε να δημιουργήσετε έναν προσαρμογέα μόνο-host-δικτύου (Host-Only Network Adapter) ή έναν προσαρμογέα δικτύωσης γέφυρας (Bridged Network Adapter), πρέπει να φορτωθούν τα αρθρώματα πυρήνα `vboxnetadp` και `vboxnetflt`, ενώ θα χρειαστεί επίσης να βεβαιωθείτε ότι έχει εγκατασταθεί το πακέτο [net-tools](https://www.archlinux.org/packages/?name=net-tools).Μπορείτε να φορτώσετε και με το χέρι αυτά τα αρθρώματα, με την:

```
# modprobe -a vboxdrv vboxnetadp vboxnetflt

```

Για να φορτώνονται αυτά τα αρθρώματα αυτόματα κατά την εκκίνηση, δείτε το άρθρο [Kernel_modules#Loading](/index.php/Kernel_modules#Loading "Kernel modules") και χρησιμοποιήστε ένα όνομα προγράμματος του `virtualbox`.

### WinXP: Το βάθος χρώματος δεν μπορεί να είναι μεγαλύτερο από 16 bits

Αν τρέχετε την εικονική μηχανή σας σε βάθος χρώματος 16 bits, τα εικονίδια μπορεί να εμφανίζονται θολά ή «πριονωτά». Ωστόσο στην προσπάθειά σας να αυξήσετε το βάθος χρώματος, το σύστημα μπορεί να σας περιορίσει σε χαμηλότερη ανάλυση ή απλώς να μη σας επιτρέπει καμία αλλαγή βάθους χρώματος. Για να το διορθώσετε αυτό, τρέξτε στα Windows το `regedit` και προσθέστε το ακόλουθο κλειδί στη registry της εικονικής μηχανής με τα Windows XP:

```
[HKEY_LOCAL_MACHINE\SOFTWARE\Policies\Microsoft\Windows NT\Terminal Services]
"ColorDepth"=dword:00000004

```

Στη συνέχεια αλλάξτε το βάθος χρώματος από το παράθυρο των ιδιοτήτων της επιφάνειας εργασίας. Αν και πάλι δεν συμβεί τίποτε, εξαναγκάστε τον επανασχεδιασμό της οθονης μέ καποια μέθοδο (π.χ. με `Host+f` για τον επανασχεδιασμό/είσοδο σε λειτουργία πλήρους οθόνης).

### Φόρτωση εικόνων .vdi

Η φόρτωση εικόνων vdi εφαρμόζεται μόνο σε εικόνες δίσκου σταθερού μεγέθους (_static_). Οι εικόνες _δυναμικού μεγέθους_ δεν είναι εύκολο να φορτωθούν.

Κατ' αρχήν χρειαζόμαστε μία πληροφορία από το αρχείο εικόνας .vdi:

```
$ VBoxManage internalcommands dumphdinfo <διαδρομή του .vdi αρχείου σας> | grep offData
Header: offBlocks=4096 offData=69632

```

Έπειτα προσθέστε 32256 στο `offData` που πήρατε (π.χ. 32256 + 69632 = 101888)

Τώρα μπορείτε να φορτώσετε την εικόνα vdi που θέλετε με την εξής εντολή:

```
# mount -t ext4 -o rw,noatime,noexec,loop,offset=101888 <διαδρομή του .vdi αρχείου σας> /mnt/

```

### Δεν δουλεύει η Αντιγραφή/Επικόλληση (Copy/Paste) στον guest με Arch Linux

Μετά την ενημέρωση των `virtualbox-guest-additions` στην έκδοση `4.2.0-2`, το χαρακτηριστικό της αντιγραφής και επικόλλησης από τον host στον εικονικό υπολογιστή που τρέχει Arch Linux δεν λειτουργεί πια. Εμφανίζεται σαν να οφείλεται στο ότι το `VBoxClient-all` απαιτεί πρόσβαση με δικαιώματα διαχειριστή (root). Σε προηγούμενες εκδόσεις αρκούσε να προσθέσουμε το `VBoxClient-all &` στο αρχείο `~/.xinitrc` για να ξαναλειτουργήσει το copy/paste. Τώρα, για να λύσουμε το πρόβλημα, θα πρέπει να ενημερώσουμε το `~/.xinitrc` κατάλληλα (`sudo VBoxClient-all &`) και να προσθέσουμε τη γραμμή `, NOPASSWD: /usr/bin/VBoxClient-all` δίπλα στο όνομα χρήστη σας στο αρχείο `/etc/sudoers` και να επανεκκινήσουμε το σύστημα γραφικών Χ. Αυτό θα πρέπει να κάνει το σύστημα να ξαναδουλεύει κανονικά. Η γραμμή στο αρχείο sudoers θα πρέπει να μοιάζει κάπως έτσι:

```
# Δώστε άδεια χρήσης του sudo στον χρήστη 'you' και επιτρέψτε του να τρέχει το VBoxClient-all χωρίς password
you ALL = PASSWD: ALL, NOPASSWD: /usr/bin/VBoxClient-all

```

**Σημείωση:** Χρησιμοποιήστε το `visudo` για την επέμβαση στο αρχείο `/etc/sudoers`. Αυτό θα ελέγξει για τυχόν λάθη σύνταξης καθώς θα αποθηκεύει τις αλλαγές.

### Χρήση σειριακής θύρας στο φιλοξενούμενο (guest) λειτουργικό σύστημα

Ελέγξτε τα δικαιώματά σας (permissions) επί της σειριακής θύρας:

```
$ /bin/ls -l /dev/ttyS*
crw-rw---- 1 root uucp 4, 64 Feb  3 09:12 /dev/ttyS0
crw-rw---- 1 root uucp 4, 65 Feb  3 09:12 /dev/ttyS1
crw-rw---- 1 root uucp 4, 66 Feb  3 09:12 /dev/ttyS2
crw-rw---- 1 root uucp 4, 67 Feb  3 09:12 /dev/ttyS3

```

Προσθέστε τον χρήστη σας στην ομάδα `uucp`

```
# gpasswd -a $USER uucp 

```

και κάντε log out και ξανά login.

### Το σύστημα κλείνει κατά την επαναφορά

Αυτό είναι ένα [γνωστό σφάλμα](https://www.virtualbox.org/ticket/11289) που προκαλεί κλείσιμο της εικονικής μηχανής όταν ο χρήστης προσπαθεί να την επαναφέρει. Μία μέθοδος για την παράκαμψη του προβλήματος είναι απλώς να κλείνετε πάντοτε την εικονική μηχανή σας με τον συνδυασμό πλήκτρων `Host+q` η με τη σχετική εντολή από το μενού.

### Εικόνες συστημάτων σε Btrfs

Πίσω στο 2010 είχαν εμφανιστεί αναφορές ότι τέτοιες εικόνες δίσκων με λειτουργικά συστήματα δεν εκκινούσαν, αν ήταν προσαρτημένες στο σύστημα μέσω εικονικής συσκευής SATA. Αυτό αναφέρθηκε ότι διορθώθηκε και πράγματι έτσι έδειχναν τα πράγματα. Όμως κάπου γύρω στο Μάρτιο του 2013 η συγκεκριμένη αναφορά σφάλματος [ξανάνοιξε](https://www.virtualbox.org/ticket/6905). Το σφάλμα μπορεί να διορθωθεί, αν ενεργοποιήσουμε τη χρήση της μνήμης cache της εισόδου/εξόδου του host (host I/O cache), που είναι εξ ορισμού ανενεργή για διεπαφές εικονικών SATA.

### Windows 8.x Error Code 0x000000C4

Αν δείτε αυτό το μήνυμα σφάλματος κατά την εκκίνηση, ακόμη κι αν επιλέξετε τύπο λειτουργικού συστήματος Win 8, προσπαθήστε να ενεργοποιήσετε την `CMPXCHG16B` εντολή της CPU

```
$ vboxmanage setextradata <όνομα της εικονικής μηχανής σας> VBoxInternal/CPUM/CMPXCHG16B 1

```

### Η εικονική μηχανή με τα Windows 8 δεν εκκινεί και δίνει σφάλμα "ERR_DISK_FULL"

Κατάσταση: Η εικονική μηχανή σας με τα Windows 8 αρνείται να εκκινήσει. Το VirtualBox εμφανίζει ως σφάλμα ότι ο εικονικός δίσκος είναι πλήρης. Όμως εσείς είστε σίγουροι ότι ο δίσκος έχει χώρο. Πηγαίνετε στις ρυθμίσεις της εικονικής μηχανής σας, στο _Settings > Storage > Controller:SATA_ και επιλέξτε "Use Host I/O Cache".

## Ἐξωτερικοί σύνδεσμοι

*   [VirtualBox User Manual](https://www.virtualbox.org/manual/UserManual.html)
*   [Wikipedia:VirtualBox](https://en.wikipedia.org/wiki/VirtualBox "wikipedia:VirtualBox")