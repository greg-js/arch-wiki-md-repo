**Συμβουλή:** Αυτό το έγγραφο είναι μέρος του άρθρου πολλαπλών σελίδων για τον Οδηγό για Αρχάριους (Beginners Guide). Κάντε κλίκ [εδώ](/index.php/Beginners%27_guide_(%CE%95%CE%BB%CE%BB%CE%B7%CE%BD%CE%B9%CE%BA%CE%AC) "Beginners' guide (Ελληνικά)") αν θέλετε να τον διαβάσετε σε μια σελίδα.

## Contents

*   [1 Προετοιμασία](#.CE.A0.CF.81.CE.BF.CE.B5.CF.84.CE.BF.CE.B9.CE.BC.CE.B1.CF.83.CE.AF.CE.B1)
    *   [1.1 Απαιτήσεις συστήματος](#.CE.91.CF.80.CE.B1.CE.B9.CF.84.CE.AE.CF.83.CE.B5.CE.B9.CF.82_.CF.83.CF.85.CF.83.CF.84.CE.AE.CE.BC.CE.B1.CF.84.CE.BF.CF.82)
    *   [1.2 Κάψτε ή γράψτε το τελευταίο μέσον εγκατάστασης](#.CE.9A.CE.AC.CF.88.CF.84.CE.B5_.CE.AE_.CE.B3.CF.81.CE.AC.CF.88.CF.84.CE.B5_.CF.84.CE.BF_.CF.84.CE.B5.CE.BB.CE.B5.CF.85.CF.84.CE.B1.CE.AF.CE.BF_.CE.BC.CE.AD.CF.83.CE.BF.CE.BD_.CE.B5.CE.B3.CE.BA.CE.B1.CF.84.CE.AC.CF.83.CF.84.CE.B1.CF.83.CE.B7.CF.82)
        *   [1.2.1 Εγκατάσταση μέσω δικτύου](#.CE.95.CE.B3.CE.BA.CE.B1.CF.84.CE.AC.CF.83.CF.84.CE.B1.CF.83.CE.B7_.CE.BC.CE.AD.CF.83.CF.89_.CE.B4.CE.B9.CE.BA.CF.84.CF.8D.CE.BF.CF.85)
        *   [1.2.2 Εγκατάσταση σε εικονική μηχανή](#.CE.95.CE.B3.CE.BA.CE.B1.CF.84.CE.AC.CF.83.CF.84.CE.B1.CF.83.CE.B7_.CF.83.CE.B5_.CE.B5.CE.B9.CE.BA.CE.BF.CE.BD.CE.B9.CE.BA.CE.AE_.CE.BC.CE.B7.CF.87.CE.B1.CE.BD.CE.AE)
    *   [1.3 Εκκίνηση του μέσου εγκατάστασης](#.CE.95.CE.BA.CE.BA.CE.AF.CE.BD.CE.B7.CF.83.CE.B7_.CF.84.CE.BF.CF.85_.CE.BC.CE.AD.CF.83.CE.BF.CF.85_.CE.B5.CE.B3.CE.BA.CE.B1.CF.84.CE.AC.CF.83.CF.84.CE.B1.CF.83.CE.B7.CF.82)
        *   [1.3.1 Ελέγξτε αν έχετε κάνει εκκίνηση σε UEFI mode](#.CE.95.CE.BB.CE.AD.CE.B3.CE.BE.CF.84.CE.B5_.CE.B1.CE.BD_.CE.AD.CF.87.CE.B5.CF.84.CE.B5_.CE.BA.CE.AC.CE.BD.CE.B5.CE.B9_.CE.B5.CE.BA.CE.BA.CE.AF.CE.BD.CE.B7.CF.83.CE.B7_.CF.83.CE.B5_UEFI_mode)
        *   [1.3.2 Αποσφαλμάτωση προβλημάτων εκκίνησης](#.CE.91.CF.80.CE.BF.CF.83.CF.86.CE.B1.CE.BB.CE.BC.CE.AC.CF.84.CF.89.CF.83.CE.B7_.CF.80.CF.81.CE.BF.CE.B2.CE.BB.CE.B7.CE.BC.CE.AC.CF.84.CF.89.CE.BD_.CE.B5.CE.BA.CE.BA.CE.AF.CE.BD.CE.B7.CF.83.CE.B7.CF.82)

## Προετοιμασία

**Σημείωση:** Αν επιθυμείτε να κάνετε εγκατάσταση από μια υπάρχουσα διανομή GNU/Linux, δείτε [αυτό το άρθρο](/index.php/Install_from_existing_Linux "Install from existing Linux"). Αυτό μπορεί να σας φανεί χρήσιμο, ιδιαίτερα αν σχεδιάζετε να εγκαταστήσετε το Arch μέσω [VNC](/index.php/VNC "VNC") ή [SSH](/index.php/SSH "SSH") απομακρυσμένα. Οι χρήστες που επιθυμούν να εγκαταστήσουν το Arch Linux απομακρυσμένα μέσω [SSH](/index.php/SSH "SSH"), πρέπει να διαβάσουν το [Install from SSH](/index.php/Install_from_SSH "Install from SSH") για έξτρα πληροφορίες

### Απαιτήσεις συστήματος

Το Arch Linux πρέπει να τρέχει σε οποιονδήποτε συμβατό με i686 υπολογιστή και με ελάχιστη μνήμη 256MB RAM. Μια βασική εγκατάσταση με όλα τα πακέτα από το γκρουπ της βάσης [[base](https://www.archlinux.org/groups/x86_64/base/)], πρέπει να δεσμεύσει περί τα 800ΜΒ χώρο στον δίσκο. Αν δεν διαθέτετε τόσο χώρο στον δίσκο σας, τότε μπορείτε να μειώσετε το μέγεθος των πακέτων, αλλά πρέπει να γνωρίζετε τι κάνετε και πως να το κάνετε.

### Κάψτε ή γράψτε το τελευταίο μέσον εγκατάστασης

Την τελευταία έκδοση του Arch Linux μπορείτε να την βρείτε και να την κατεβάσετε από την σελίδα [Download](https://archlinux.org/download/). Σημειώστε πως η τελευταία .iso εικόνα υποστηρίζει και τις δύο αρχιτεκτονικές 32bit & 64bit. Συνίσταται να χρησιμοποιείτε πάντα την τελευταία διαθέσιμη εικόνα .iso.

*   Οι εικόνες εγκατάστασης είναι υπογεγραμμένες και συνίσταται να επαληθεύετε την υπογραφή τους πριν την χρήση: αυτό μπορεί να γίνει κατεβάζοντας το αρχείο **sig** από την σελίδα λήψης (ή από έναν mirror που υπάρχει εκεί) στον ίδιο κατάλογο με το **iso** αρχείο και μετά να χρησιμοποιήσετε την εντολή `pacman-key -v *iso-file*.sig`.

*   Κάψτε την εικόνα ISO σε ένα CD ή DVD με το πρόγραμμα που προτιμάτε.

**Σημείωση:** Η ποιότητα των οπτικών δίσκων και των δίσκων αυτών καθεαυτών, ποικίλλει σε μεγάλο βαθμό. Γενικά, προτείνεται να χρησιμοποιείτε μια χαμηλή ταχύτητα εγγραφής για ένα αξιόπιστο αποτέλεσμα. Αν αντιμετωπίσετε προβλήματα με τον δίσκο, δοκιμάστε να τον κάψετε στην χαμηλότερη δυνατή ταχύτητα που υποστηρίζει ο εγγραφέας

*   Εναλλακτικά μπορείτε να κάψετε την εικόνα ISO σε ένα USB stick. Για λεπτομερείς οδηγίες δείτε στο [USB Installation Media](/index.php/USB_Installation_Media "USB Installation Media").

#### Εγκατάσταση μέσω δικτύου

Αντί να γράψετε το μέσον εκκίνησης σε έναν δίσκο ή USB stick, εναλλακτικά μπορείτε να κάνετε εκκίνηση την εικόνα .iso μέσω δικτύου. Αυτή η μέθοδος δουλεύει καλά αν έχετε ήδη στημένο έναν server. Για περισσότερες πληροφορίες δείτε σε αυτό το [άρθρο](/index.php/Install_Arch_from_network_(via_PXE) "Install Arch from network (via PXE)") και μετά συνεχίστε με το [Εκκίνηση του μέσου εγκατάστασης](#.CE.95.CE.BA.CE.BA.CE.AF.CE.BD.CE.B7.CF.83.CE.B7_.CF.84.CE.BF.CF.85_.CE.BC.CE.AD.CF.83.CE.BF.CF.85_.CE.B5.CE.B3.CE.BA.CE.B1.CF.84.CE.AC.CF.83.CF.84.CE.B1.CF.83.CE.B7.CF.82).

#### Εγκατάσταση σε εικονική μηχανή

Η εγκατάσταση σε μια [εικονική μηχανή](https://el.wikipedia.org/wiki/%CE%95%CE%B9%CE%BA%CE%BF%CE%BD%CE%B9%CE%BA%CE%BF%CF%80%CE%BF%CE%AF%CE%B7%CF%83%CE%B7) είναι ένας καλός τρόπος για να εξοικειωθείτε με το Arch Linux και την διαδικασία εγκατάστασης, χωρίς να χρειάζεται να αφήσετε το τρέχων λειτουργικό σας σύστημα και να δημιουργήσετε διαμερίσματα στον δίσκο. Θα σας επιτρέψει επίσης, να έχετε αυτόν τον οδηγό για αρχάριους ανοιχτό σε έναν περιηγητή(browser) καθ' όλη την διαδικασία της εγκατάστασης. Μερικοί χρήστες θα το βρουν αρκετά ωφέλιμο να έχουν ένα ανεξάρτητο λειτουργικό σύστημα Arch Linux σε μια εικονική μηχανή, για δοκιμαστικούς σκοπούς. Παραδείγματα λογισμικού εικονικοποίησης είναι [VirtualBox](/index.php/VirtualBox "VirtualBox"), [VMware](/index.php/VMware "VMware"), [QEMU](/index.php/QEMU "QEMU"), [Xen](/index.php/Xen "Xen"), [Parallels](/index.php/Parallels "Parallels").

Η ακριβής διαδικασία προετοιμασίας μιας εικονικής μηχανής εξαρτάται από το λογισμικό. Γενικά όμως ακολουθούμε τα παρακάτω βήματα:

1.  Δημιουργούμε τον εικονικό δίσκο που θα φιλοξενήσει το λειτουργικό σύστημα.
2.  Ρυθμίζουμε κατάλληλα τις παραμέτρους της εικονικής μηχανής.
3.  Εκκινούμε το ISO που έχουμε κατεβάσει μέσω του εικονικού CD drive.
4.  Συνεχίζουμε με το [Εκκίνηση του μέσου εγκατάστασης](#.CE.95.CE.BA.CE.BA.CE.AF.CE.BD.CE.B7.CF.83.CE.B7_.CF.84.CE.BF.CF.85_.CE.BC.CE.AD.CF.83.CE.BF.CF.85_.CE.B5.CE.B3.CE.BA.CE.B1.CF.84.CE.AC.CF.83.CF.84.CE.B1.CF.83.CE.B7.CF.82).

Τα παρακάτω άρθρα μπορεί να σας φανούν χρήσιμα:

*   [Arch Linux as VirtualBox guest](/index.php/VirtualBox#Arch_Linux_as_a_guest_in_a_Virtual_Machine "VirtualBox")
*   [Arch Linux as VirtualBox guest on a physical drive](/index.php/VirtualBox_Arch_Linux_Guest_On_Physical_Drive "VirtualBox Arch Linux Guest On Physical Drive")
*   [Arch Linux as VMware guest](/index.php/Installing_Arch_Linux_in_VMware "Installing Arch Linux in VMware")
*   [Moving an existing install into (or out of) a virtual machine](/index.php/Moving_an_existing_install_into_(or_out_of)_a_virtual_machine "Moving an existing install into (or out of) a virtual machine")

### Εκκίνηση του μέσου εγκατάστασης

Πρώτα, ίσως θα πρέπει να αλλάξετε την σειρά εκκίνησης από το BIOS. Για να το κάνετε αυτό, πιέστε ένα πλήκτρο (συνήθως είναι το `Delete`, `F1`, `F2`, `F11` ή `F12`) κατά τη διάρκεια της εκκίνησης του υπολογιστή, [φάση POST](https://en.wikipedia.org/wiki/Power-on_self_test "wikipedia:Power-on self test"). Αυτό θα σας πάει στις ρυθμίσεις του BIOS, απ' όπου μπορείτε να θέσετε την σειρά με την οποία θα ψάξει ο υπολογιστής για συσκευές να εκκινήσει. Επιλέξτε "Save & Exit" (ή το αντίστοιχο μενού στο δικό σας BIOS) και μετά ο υπολογιστής σας θα πρέπει να ολοκληρώσει κανονικά την διαδικασία εκκίνησης. (αν κάνετε εκκίνηση από ένα UEFI μέσον εκκίνησης, τότε η επιλογή μπορεί να μοιάζει ως "Arch Linux archiso x86_64 UEFI") Όταν το μενού του Arch εμφανιστεί, επιλέξτε "Boot Arch Linux" και πατήστε `Enter` για να μπείτε στο «ζωντανό» (live) περιβάλλον του Arch Linux, απ' όπου θα κάνετε και την εγκατάσταση.

Αφού έχετε εκκινήσει στο «ζωντανό» (live) περιβάλλον, το κέλυφος (shell) είναι το [Zsh](/index.php/Zsh "Zsh")· αυτό θα σας παρέχει ένα προχωρημένο Tab Completion(σύστημα αυτόματης συμπλήρωσης εντολών) και άλλα χαρακτηριστικά ως μέρος του [grml config](http://grml.org/zsh/).

#### Ελέγξτε αν έχετε κάνει εκκίνηση σε UEFI mode

Στην περίπτωση που έχετε μητρική κάρτα με [UEFI](/index.php/UEFI "UEFI") και είναι ενεργοποιημένο (και προτιμάται από το BIOS/Legacy), το CD/USB θα κάνει εκκίνηση αυτόματα τον πυρήνα(kernel) του Arch Linux (Kernel [EFISTUB](/index.php/EFISTUB "EFISTUB") μέσω του [Gummiboot](/index.php/Gummiboot "Gummiboot")). Για να ελέγξετε αν είστε σε UEFI mode τρέξτε:

```
# mount -t efivarfs efivarfs /sys/firmware/efi/efivars              # αγνοήστε το αν είναι ήδη προσαρτημένο
# efivar -l

```

Αν τα αποτελέσματα της εντολής efivar έχουν ως έξοδο τις παραμέτρους σωστά, τότε έχετε κάνει εκκίνηση σε UEFI mode. Αν όχι, ελέγξτε αν όλες οι απαιτήσεις που γράφονται εδώ: [Unified Extensible Firmware Interface#Requirements for UEFI Variables support to work properly](/index.php/Unified_Extensible_Firmware_Interface#Requirements_for_UEFI_Variables_support_to_work_properly "Unified Extensible Firmware Interface") ικανοποιούνται.

#### Αποσφαλμάτωση προβλημάτων εκκίνησης

*   Αν χρησιμοποιείτε κάποια κάρτα γραφικών Intel και η οθόνη μένει κενή κατά την διάρκεια της εκκίνησης, πιθανότατα το πρόβλημα είναι σχετικό με το [Kernel mode setting](/index.php/Kernel_mode_setting "Kernel mode setting"). Μια πιθανή λύση μπορεί να είναι να κάνετε μια επανεκκίνηση και πατήστε το πλήκτρο `e` επάνω στην ένδειξη που θέλετε να κάνετε εκκίνηση (i686 ή x86_64). Στο τέλος της σειράς της γραμμής γράψτε `nomodeset` και πατήστε το `Enter`. Εναλλακτικά, δοκιμάσετε `video=SVIDEO-1:d` και αν δουλέψει δεν θα απενεργοποιήσει την ρύθμιση λειτουργίας του πυρήνα (kernel mode setting). Επίσης μπορείτε να δοκιμάσετε `i915.modeset=0`. Δείτε το άρθρο της [Intel](/index.php/Intel "Intel") για περισσότερες πληροφορίες.

*   Αν η οθόνη **δεν** μένει κενή και η διαδικασία εκκίνησης κολλάει καθώς φορτώνει ο πυρήνας, πατήστε το πλήκτρο `Tab` καθώς βρίσκεστε επάνω στο μενού και γράψτε στο τέλος της σειράς της γραμμής, `acpi=off` και πατήστε `Enter`.

**[Beginners' Guide (Ελληνικά)](/index.php/Beginners%27_Guide_(%CE%95%CE%BB%CE%BB%CE%B7%CE%BD%CE%B9%CE%BA%CE%AC) "Beginners' Guide (Ελληνικά)")**

* * *

**Προετοιμασία** >> [Εγκατάσταση](/index.php/Beginners%27_Guide/Installation_(%CE%95%CE%BB%CE%BB%CE%B7%CE%BD%CE%B9%CE%BA%CE%AC) "Beginners' Guide/Installation (Ελληνικά)") >> [Μετά την εγκατάσταση](/index.php/Beginners%27_Guide/Post-Installation_(%CE%95%CE%BB%CE%BB%CE%B7%CE%BD%CE%B9%CE%BA%CE%AC) "Beginners' Guide/Post-Installation (Ελληνικά)")