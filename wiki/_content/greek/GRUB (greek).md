Ο [GRUB](https://www.gnu.org/software/grub/) — να μην συγχέεται με το [GRUB Legacy](/index.php/GRUB_Legacy "GRUB Legacy") — είναι η νέα γενιά του GRand Unified Bootloader. Ο GRUB προέρχεται από το [PUPA](http://www.nongnu.org/pupa/) που ήταν ένα ερευνητικό σχήμα για την ανάπτυξη της νέας γενιάς αυτού που σήμερα λέμε GRUB Legacy. Ο GRUB ξανα-γράφτηκε από την αρχή για να ανασυγκροτηθεί και να παρέχει δομοστοιχειωτό σχεδιασμό και φορητότητα.[[1]](https://www.gnu.org/software/grub/grub-faq.html#q1).

## Contents

*   [1 Πρόλογος](#.CE.A0.CF.81.CF.8C.CE.BB.CE.BF.CE.B3.CE.BF.CF.82)
*   [2 Σήστημα BIOS](#.CE.A3.CE.AE.CF.83.CF.84.CE.B7.CE.BC.CE.B1_BIOS)
    *   [2.1 Ειδικές οδηγίες για τον πίνακα κατατμήσεων GUID (GPT)](#.CE.95.CE.B9.CE.B4.CE.B9.CE.BA.CE.AD.CF.82_.CE.BF.CE.B4.CE.B7.CE.B3.CE.AF.CE.B5.CF.82_.CE.B3.CE.B9.CE.B1_.CF.84.CE.BF.CE.BD_.CF.80.CE.AF.CE.BD.CE.B1.CE.BA.CE.B1_.CE.BA.CE.B1.CF.84.CE.B1.CF.84.CE.BC.CE.AE.CF.83.CE.B5.CF.89.CE.BD_GUID_.28GPT.29)
    *   [2.2 Ειδικές οδηγίες για τον 'Master Boot Record (MBR)'](#.CE.95.CE.B9.CE.B4.CE.B9.CE.BA.CE.AD.CF.82_.CE.BF.CE.B4.CE.B7.CE.B3.CE.AF.CE.B5.CF.82_.CE.B3.CE.B9.CE.B1_.CF.84.CE.BF.CE.BD_.27Master_Boot_Record_.28MBR.29.27)
    *   [2.3 Εγκατάσταση](#.CE.95.CE.B3.CE.BA.CE.B1.CF.84.CE.AC.CF.83.CF.84.CE.B1.CF.83.CE.B7)
        *   [2.3.1 Εγκατάσταση αρχείων boot](#.CE.95.CE.B3.CE.BA.CE.B1.CF.84.CE.AC.CF.83.CF.84.CE.B1.CF.83.CE.B7_.CE.B1.CF.81.CF.87.CE.B5.CE.AF.CF.89.CE.BD_boot)

## Πρόλογος

*   Ο *bootloader* είναι το πρώτο πρόγραμμα που τρέχει ο υπολογιστής κατά την εκκίνησή του. Είναι υπεύθυνος στο να διαβαστεί και να μεταφερθεί ο πυρήνας (kernel) του Linux.
*   Το όνομα GRUB ουσιαστικά απευθύνετε στην *δεύτερη* έκδοση της εφαρμογής αυτής, [δες](https://www.gnu.org/software/grub/). Αν θέλετε να μάθετε περισσότερο για την παλαιότερη έκδοσή του, διαβάστε στο [GRUB Legacy](/index.php/GRUB_Legacy "GRUB Legacy").
*   Ο GRUB υποστηρίζει το σύστημα αρχείων [Btrfs](/index.php/Btrfs "Btrfs") σαν διαχειριστής *root* είτε είναι συμπιεσμένο σαν *zlib* είτε *LZO* χωρίς ξεχωριστό `/boot`.
*   Ο GRUB δεν υποστηρίζει στο σύστημα αρχείων [F2FS](/index.php/F2FS "F2FS") σαν διαχειριστής *root*. Έτσι θα χρειαστείτε ένα ξεχωριστό `/boot` με υποστηριζόμενο σύστημα αρχείων.

## Σήστημα BIOS

### Ειδικές οδηγίες για τον πίνακα κατατμήσεων GUID (GPT)

Για την ρύθμιση του BIOS/[GUID Partition Table (Ελληνικά)](/index.php/GUID_Partition_Table_(%CE%95%CE%BB%CE%BB%CE%B7%CE%BD%CE%B9%CE%BA%CE%AC) "GUID Partition Table (Ελληνικά)") χρειάζεται ο [BIOS boot partition](http://www.gnu.org/software/grub/manual/html_node/BIOS-installation.html). Ο GRUB ενσωματώνει σε αυτόν το `core.img` του.

**Σημείωση:**

*   Πριν κάνετε αυτήν την μέθοδο, να έχετε υπόψιν πως όλα τα συστήματα δεν υποστηρίζουν αυτήν την μέθοδο διαμόρφωσης. Περισσότερες πληροφορίες στο [Σύστημα BIOS](/index.php/GUID_Partition_Table_(%CE%95%CE%BB%CE%BB%CE%B7%CE%BD%CE%B9%CE%BA%CE%AC)#.CE.A3.CF.85.CF.83.CF.84.CE.AE.CE.BC.CE.B1.CF.84.CE.B1_BIOS "GUID Partition Table (Ελληνικά)").
*   Ο GRUB χρειάζεται αυτό το έξτρα τμήμα σκληρού μόνο για την μέθοδο διαμόρφωσης BIOS/GPT. Παλιότερα στην μέθοδο BIOS/MBR ο GRUB χρησιμοποιούσε το Post-MBR για να ενσωματώσει το `core.img` του. Ο GRUB για το BIOS/GPT δεν χρησιμοποιεί το Post-GPT για να συμμορφωθεί με τις απαιτήσεις που χρειάζεται 1_μεγκαμπάιτ/2048_τομείς σκληρού δίσκου.
*   Στα συστήματα [UEFI](/index.php/UEFI "UEFI") δεν χρειάζεται αυτό το έξτρα τμήμα σκληρού μιας και δεν ενσωματώνετε στο boot sector.

Δημιουργήστε ένα τμήμα σκληρού 1 mebibyte (`+1M` με το `fdisk` ή με το `gdisk`) σε δίσκο που δεν έχει σύστημα αρχείων και επιλέξτε BIOS boot (*BIOS boot* για το fdisk, `ef02` για το gdisk, `bios_grub` για το `parted`). Αυτό το τμήμα σκληρού μπορεί να βρίσκεται σε οποιαδήποτε θέση αλλά πριν τα πρώτα 2 TiB του σκληρού. Αυτό το τμήμα πρέπει να δημιουργηθεί πριν την εγκατάσταση του GRUB. Όταν δημιουργηθεί αυτό το τμήμα, εγκαταστήστε τον GRUB όπως αναφέρετε πιο κάτω.

Το Post-GPT μπορεί επίσης να χρησιμοποιηθεί και σαν τμήμα σκληρού 'BIOS boot' παρά που δεν θα χρησιμοποιεί τις προδιαγραφές του GPT. Μιας και αυτό το τμήμα σκληρού δεν θα χρησιμοποιείται τακτικά, τυχόν αναφορές σφαλμάτων (από κάποια προγράμματα διαχείρισης δίσκων) μπορούν να αγνοηθούν. Με το `fdisk` ή με το `gdisk` δημιουργήστε ένα τμήμα σκληρού που να αρχίζει από τον 34ο τομέα μέχρι τον 2047ο και ρυθμίστε τον τύπο του. Για να μπορείτε να βλέπετε τις πρώτες κατατμήσεις του σκληρού, να φτιάξετε αυτό το τμήμα τελευταίο.

### Ειδικές οδηγίες για τον 'Master Boot Record (MBR)'

Ο post-[MBR](/index.php/MBR "MBR") ξεκινάει μετά από τα πρώτα 512 byte της περιοχής του MBR και πριν το πρώτο διαμέρισμα σκληρού. Σε πολλά MBR (ή με την ετικέτα 'msdos') διαχωρισμένα συστήματα ο χώρος του MBR είναι 31 KiB όπου ήταν ικανοποιητικός για το σύστημα DOS. Ωστόσο για τον GRUB συνιστάται ο χώρος αυτός να είναι 1-2 MiB για να υπάρχει αρκετός χώρος για να ενσωματωθεί ο `core.img` του GRUB ([FS#24103](https://bugs.archlinux.org/task/24103)). Καλό είναι να χρησιμοποιείται εργαλεία διαμόρφωσης σκληρών που υποστηρίζουν 1 MiB για να επιτευχθεί αυτός ο χώρος όπως και να ικανοποιηθούν άλλα μή-512 byte προβλήματα (που είναι άσχετα με την ενσωμάτωση του `core.img`).

### Εγκατάσταση

Ο GRUB μπορεί να [εγκατασταθεί](/index.php/Pacman_(%CE%95%CE%BB%CE%BB%CE%B7%CE%BD%CE%B9%CE%BA%CE%AC) "Pacman (Ελληνικά)") με το πακέτο [grub](https://www.archlinux.org/packages/?name=grub) από τα [official repositories](/index.php/Official_repositories "Official repositories"). Θα αντικαταστήσει το [grub-legacy](https://aur.archlinux.org/packages/grub-legacy/), αν είναι ήδη εγκατεστημένο.

**Note:** Εγκαταστόντας απλά το πακέτο δεν θα ανανεώνει το αρχείο `/boot/grub/i386-pc/core.img` και τις ενότητες στο `/boot/grub/i386-pc`. Θα πρέπει να τις ανανεώνετε χειροκίνητα με την χρήση του `grub-install` όπως αναφέρεται πιο κάτω.

#### Εγκατάσταση αρχείων boot

Υπάρχουν 4 τρόποι για να εγκατασταθούν τα αρχεία του GRUB boot για τον BIOS:

*   [Εγκατάσταση στον δίσκο](#.CE.95.CE.B3.CE.BA.CE.B1.CF.84.CE.AC.CF.83.CF.84.CE.B1.CF.83.CE.B7_.CE.B1.CF.81.CF.87.CE.B5.CE.AF.CF.89.CE.BD_boot) (συνιστάται)
*   [Εγκατάσταση σε εξωτερική USB μονάδα](#.CE.95.CE.B3.CE.BA.CE.B1.CF.84.CE.AC.CF.83.CF.84.CE.B1.CF.83.CE.B7_.CF.83.CE.B5_.CE.B5.CE.BE.CF.89.CF.84.CE.B5.CF.81.CE.B9.CE.BA.CE.AE_USB_.CE.BC.CE.BF.CE.BD.CE.AC.CE.B4.CE.B1) (για ανάκτηση)
*   Εγκατάσταση σε τμήμα, μη-τμήμα σκληρού δίσκου (δεν συνιστάται)
*   [Δημιουργία μόνο του core.img](#.CE.94.CE.B7.CE.BC.CE.B9.CE.BF.CF.85.CF.81.CE.B3.CE.AF.CE.B1_.CE.BC.CF.8C.CE.BD.CE.BF_.CF.84.CE.BF.CF.85_core.img) (ασφαλέστερη μέθοδος, αλλά απαιτεί άλλον έναν BIOS bootloader σαν το [Syslinux](/index.php/Syslinux "Syslinux") να είναι ήδη εγκατεστημένο για να συνδέσει το `/boot/grub/i386-pc/core.img`)

**Note:** Δείτε το [https://www.gnu.org/software/grub/manual/html_node/BIOS-installation.html](https://www.gnu.org/software/grub/manual/html_node/BIOS-installation.html) για περισσότερες πληροφορίες.