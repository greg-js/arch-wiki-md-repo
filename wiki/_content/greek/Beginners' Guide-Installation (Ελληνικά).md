**Συμβουλή:** Αυτό το έγγραφο είναι μέρος του άρθρου πολλαπλών σελίδων για τον Οδηγό για Αρχάριους (Beginners Guide). Κάντε κλίκ [εδώ](/index.php/Beginners%27_guide_(%CE%95%CE%BB%CE%BB%CE%B7%CE%BD%CE%B9%CE%BA%CE%AC) "Beginners' guide (Ελληνικά)") αν θέλετε να τον διαβάσετε σε μια σελίδα.

Αυτό το έγγραφο θα σας οδηγήσει κατά την διαδικασία της εγκατάστασης του [Arch Linux](/index.php/Arch_Linux_(%CE%95%CE%BB%CE%BB%CE%B7%CE%BD%CE%B9%CE%BA%CE%AC) "Arch Linux (Ελληνικά)") χρησιμοποιώντας τα [Installation guide](/index.php/Installation_guide "Installation guide"). Πριν εγκαταστήσετε σας προτείνουμε να διαβάσετε πολύ καλά το [FAQ](/index.php/FAQ "FAQ").

Το [ArchWiki](/index.php/Main_page_(%CE%95%CE%BB%CE%BB%CE%B7%CE%BD%CE%B9%CE%BA%CE%AC) "Main page (Ελληνικά)") που συντηρείται από την κοινότητα είναι η βασική πηγή που συμβουλεύει όταν παρουσιάζονται διάφορα προβλήματα. Το [κανάλι irc](/index.php/IRC_channel "IRC channel") ([irc://irc.freenode.net/#archlinux-greece](irc://irc.freenode.net/#archlinux-greece)) και τα [forums](https://bbs.archlinux.org/) είναι επίσης εξαιρετικές πηγές αν δεν μπορεί να βρεθεί αλλού απάντηση. Σύμφωνα με το [Arch Way](/index.php/The_Arch_Way_(%CE%95%CE%BB%CE%BB%CE%B7%CE%BD%CE%B9%CE%BA%CE%AC) "The Arch Way (Ελληνικά)") σας ενθαρρύνουμε να πληκτρολογείτε την `man command` ώστε να διαβάζετε την σελίδα `man` οποιασδήποτε εντολής που δεν είστε εξοικειωμένοι.

## Contents

*   [1 Εγκατάσταση](#.CE.95.CE.B3.CE.BA.CE.B1.CF.84.CE.AC.CF.83.CF.84.CE.B1.CF.83.CE.B7)
    *   [1.1 Αλλαγή γλώσσας](#.CE.91.CE.BB.CE.BB.CE.B1.CE.B3.CE.AE_.CE.B3.CE.BB.CF.8E.CF.83.CF.83.CE.B1.CF.82)
    *   [1.2 Δημιουργία σύνδεσης με το διαδίκτυο](#.CE.94.CE.B7.CE.BC.CE.B9.CE.BF.CF.85.CF.81.CE.B3.CE.AF.CE.B1_.CF.83.CF.8D.CE.BD.CE.B4.CE.B5.CF.83.CE.B7.CF.82_.CE.BC.CE.B5_.CF.84.CE.BF_.CE.B4.CE.B9.CE.B1.CE.B4.CE.AF.CE.BA.CF.84.CF.85.CE.BF)
    *   [1.3 Ενσύρματη σύνδεση](#.CE.95.CE.BD.CF.83.CF.8D.CF.81.CE.BC.CE.B1.CF.84.CE.B7_.CF.83.CF.8D.CE.BD.CE.B4.CE.B5.CF.83.CE.B7)
    *   [1.4 Ασύρματη σύνδεση](#.CE.91.CF.83.CF.8D.CF.81.CE.BC.CE.B1.CF.84.CE.B7_.CF.83.CF.8D.CE.BD.CE.B4.CE.B5.CF.83.CE.B7)
        *   [1.4.1 Χωρίς την χρήση της wifi-menu](#.CE.A7.CF.89.CF.81.CE.AF.CF.82_.CF.84.CE.B7.CE.BD_.CF.87.CF.81.CE.AE.CF.83.CE.B7_.CF.84.CE.B7.CF.82_wifi-menu)
    *   [1.5 Αναλογικό modem, ISDN ή PPPoE DSL](#.CE.91.CE.BD.CE.B1.CE.BB.CE.BF.CE.B3.CE.B9.CE.BA.CF.8C_modem.2C_ISDN_.CE.AE_PPPoE_DSL)
    *   [1.6 Μέσω διακομιστή μεσολάβησης (proxy server)](#.CE.9C.CE.AD.CF.83.CF.89_.CE.B4.CE.B9.CE.B1.CE.BA.CE.BF.CE.BC.CE.B9.CF.83.CF.84.CE.AE_.CE.BC.CE.B5.CF.83.CE.BF.CE.BB.CE.AC.CE.B2.CE.B7.CF.83.CE.B7.CF.82_.28proxy_server.29)
    *   [1.7 Προετοιμασία του μέσου αποθήκευσης](#.CE.A0.CF.81.CE.BF.CE.B5.CF.84.CE.BF.CE.B9.CE.BC.CE.B1.CF.83.CE.AF.CE.B1_.CF.84.CE.BF.CF.85_.CE.BC.CE.AD.CF.83.CE.BF.CF.85_.CE.B1.CF.80.CE.BF.CE.B8.CE.AE.CE.BA.CE.B5.CF.85.CF.83.CE.B7.CF.82)
        *   [1.7.1 Επιλέξτε έναν τύπο πίνακα κατάτμησης](#.CE.95.CF.80.CE.B9.CE.BB.CE.AD.CE.BE.CF.84.CE.B5_.CE.AD.CE.BD.CE.B1.CE.BD_.CF.84.CF.8D.CF.80.CE.BF_.CF.80.CE.AF.CE.BD.CE.B1.CE.BA.CE.B1_.CE.BA.CE.B1.CF.84.CE.AC.CF.84.CE.BC.CE.B7.CF.83.CE.B7.CF.82)
        *   [1.7.2 Εργαλείο κατατμήσεων](#.CE.95.CF.81.CE.B3.CE.B1.CE.BB.CE.B5.CE.AF.CE.BF_.CE.BA.CE.B1.CF.84.CE.B1.CF.84.CE.BC.CE.AE.CF.83.CE.B5.CF.89.CE.BD)
        *   [1.7.3 Οργανόγραμμα κατατμήσεων](#.CE.9F.CF.81.CE.B3.CE.B1.CE.BD.CF.8C.CE.B3.CF.81.CE.B1.CE.BC.CE.BC.CE.B1_.CE.BA.CE.B1.CF.84.CE.B1.CF.84.CE.BC.CE.AE.CF.83.CE.B5.CF.89.CE.BD)
        *   [1.7.4 Εκτιμήσεις για διπλή εκκίνηση με Windows](#.CE.95.CE.BA.CF.84.CE.B9.CE.BC.CE.AE.CF.83.CE.B5.CE.B9.CF.82_.CE.B3.CE.B9.CE.B1_.CE.B4.CE.B9.CF.80.CE.BB.CE.AE_.CE.B5.CE.BA.CE.BA.CE.AF.CE.BD.CE.B7.CF.83.CE.B7_.CE.BC.CE.B5_Windows)
        *   [1.7.5 Παράδειγμα](#.CE.A0.CE.B1.CF.81.CE.AC.CE.B4.CE.B5.CE.B9.CE.B3.CE.BC.CE.B1)
            *   [1.7.5.1 Χρησιμοποιώντας το cgdisk για τη δημιουργία κατατμήσεων τύπου GPT](#.CE.A7.CF.81.CE.B7.CF.83.CE.B9.CE.BC.CE.BF.CF.80.CE.BF.CE.B9.CF.8E.CE.BD.CF.84.CE.B1.CF.82_.CF.84.CE.BF_cgdisk_.CE.B3.CE.B9.CE.B1_.CF.84.CE.B7_.CE.B4.CE.B7.CE.BC.CE.B9.CE.BF.CF.85.CF.81.CE.B3.CE.AF.CE.B1_.CE.BA.CE.B1.CF.84.CE.B1.CF.84.CE.BC.CE.AE.CF.83.CE.B5.CF.89.CE.BD_.CF.84.CF.8D.CF.80.CE.BF.CF.85_GPT)
            *   [1.7.5.2 Χρησιμοποιώντας το fdisk για τη δημιουργία κατατμήσεων τύπου MBR](#.CE.A7.CF.81.CE.B7.CF.83.CE.B9.CE.BC.CE.BF.CF.80.CE.BF.CE.B9.CF.8E.CE.BD.CF.84.CE.B1.CF.82_.CF.84.CE.BF_fdisk_.CE.B3.CE.B9.CE.B1_.CF.84.CE.B7_.CE.B4.CE.B7.CE.BC.CE.B9.CE.BF.CF.85.CF.81.CE.B3.CE.AF.CE.B1_.CE.BA.CE.B1.CF.84.CE.B1.CF.84.CE.BC.CE.AE.CF.83.CE.B5.CF.89.CE.BD_.CF.84.CF.8D.CF.80.CE.BF.CF.85_MBR)
        *   [1.7.6 Δημιουργία συστήματος αρχείων](#.CE.94.CE.B7.CE.BC.CE.B9.CE.BF.CF.85.CF.81.CE.B3.CE.AF.CE.B1_.CF.83.CF.85.CF.83.CF.84.CE.AE.CE.BC.CE.B1.CF.84.CE.BF.CF.82_.CE.B1.CF.81.CF.87.CE.B5.CE.AF.CF.89.CE.BD)
    *   [1.8 Προσαρτήστε τις κατατμήσεις](#.CE.A0.CF.81.CE.BF.CF.83.CE.B1.CF.81.CF.84.CE.AE.CF.83.CF.84.CE.B5_.CF.84.CE.B9.CF.82_.CE.BA.CE.B1.CF.84.CE.B1.CF.84.CE.BC.CE.AE.CF.83.CE.B5.CE.B9.CF.82)
    *   [1.9 Επιλέξτε ένα mirror](#.CE.95.CF.80.CE.B9.CE.BB.CE.AD.CE.BE.CF.84.CE.B5_.CE.AD.CE.BD.CE.B1_mirror)
    *   [1.10 Εγκαταστήστε το βασικό σύστημα](#.CE.95.CE.B3.CE.BA.CE.B1.CF.84.CE.B1.CF.83.CF.84.CE.AE.CF.83.CF.84.CE.B5_.CF.84.CE.BF_.CE.B2.CE.B1.CF.83.CE.B9.CE.BA.CF.8C_.CF.83.CF.8D.CF.83.CF.84.CE.B7.CE.BC.CE.B1)
    *   [1.11 Δημιουργία του fstab](#.CE.94.CE.B7.CE.BC.CE.B9.CE.BF.CF.85.CF.81.CE.B3.CE.AF.CE.B1_.CF.84.CE.BF.CF.85_fstab)
    *   [1.12 Κάντε chroot και ρυθμίστε το βασικό σύστημα](#.CE.9A.CE.AC.CE.BD.CF.84.CE.B5_chroot_.CE.BA.CE.B1.CE.B9_.CF.81.CF.85.CE.B8.CE.BC.CE.AF.CF.83.CF.84.CE.B5_.CF.84.CE.BF_.CE.B2.CE.B1.CF.83.CE.B9.CE.BA.CF.8C_.CF.83.CF.8D.CF.83.CF.84.CE.B7.CE.BC.CE.B1)
        *   [1.12.1 Locale (τοπική ρύθμιση)](#Locale_.28.CF.84.CE.BF.CF.80.CE.B9.CE.BA.CE.AE_.CF.81.CF.8D.CE.B8.CE.BC.CE.B9.CF.83.CE.B7.29)
        *   [1.12.2 Γραμματοσειρά κονσόλας και διάταξη πληκτρολογίου](#.CE.93.CF.81.CE.B1.CE.BC.CE.BC.CE.B1.CF.84.CE.BF.CF.83.CE.B5.CE.B9.CF.81.CE.AC_.CE.BA.CE.BF.CE.BD.CF.83.CF.8C.CE.BB.CE.B1.CF.82_.CE.BA.CE.B1.CE.B9_.CE.B4.CE.B9.CE.AC.CF.84.CE.B1.CE.BE.CE.B7_.CF.80.CE.BB.CE.B7.CE.BA.CF.84.CF.81.CE.BF.CE.BB.CE.BF.CE.B3.CE.AF.CE.BF.CF.85)
        *   [1.12.3 Ζώνη ώρας](#.CE.96.CF.8E.CE.BD.CE.B7_.CF.8E.CF.81.CE.B1.CF.82)
        *   [1.12.4 Hardware clock (ρολόι υπολογιστή)](#Hardware_clock_.28.CF.81.CE.BF.CE.BB.CF.8C.CE.B9_.CF.85.CF.80.CE.BF.CE.BB.CE.BF.CE.B3.CE.B9.CF.83.CF.84.CE.AE.29)
        *   [1.12.5 Kernel modules (αρθρώματα του πυρήνα)](#Kernel_modules_.28.CE.B1.CF.81.CE.B8.CF.81.CF.8E.CE.BC.CE.B1.CF.84.CE.B1_.CF.84.CE.BF.CF.85_.CF.80.CF.85.CF.81.CE.AE.CE.BD.CE.B1.29)
        *   [1.12.6 Hostname (όνομα συστήματος)](#Hostname_.28.CF.8C.CE.BD.CE.BF.CE.BC.CE.B1_.CF.83.CF.85.CF.83.CF.84.CE.AE.CE.BC.CE.B1.CF.84.CE.BF.CF.82.29)
    *   [1.13 Ρυθμίστε το δίκτυο](#.CE.A1.CF.85.CE.B8.CE.BC.CE.AF.CF.83.CF.84.CE.B5_.CF.84.CE.BF_.CE.B4.CE.AF.CE.BA.CF.84.CF.85.CE.BF)
        *   [1.13.1 Ενσύρματη σύνδεση](#.CE.95.CE.BD.CF.83.CF.8D.CF.81.CE.BC.CE.B1.CF.84.CE.B7_.CF.83.CF.8D.CE.BD.CE.B4.CE.B5.CF.83.CE.B7_2)
            *   [1.13.1.1 Δυναμική IP](#.CE.94.CF.85.CE.BD.CE.B1.CE.BC.CE.B9.CE.BA.CE.AE_IP)
            *   [1.13.1.2 Στατική IP](#.CE.A3.CF.84.CE.B1.CF.84.CE.B9.CE.BA.CE.AE_IP)
        *   [1.13.2 Ασύρματη σύνδεση](#.CE.91.CF.83.CF.8D.CF.81.CE.BC.CE.B1.CF.84.CE.B7_.CF.83.CF.8D.CE.BD.CE.B4.CE.B5.CF.83.CE.B7_2)
            *   [1.13.2.1 Προσθήκη ασύρματων δικτύων](#.CE.A0.CF.81.CE.BF.CF.83.CE.B8.CE.AE.CE.BA.CE.B7_.CE.B1.CF.83.CF.8D.CF.81.CE.BC.CE.B1.CF.84.CF.89.CE.BD_.CE.B4.CE.B9.CE.BA.CF.84.CF.8D.CF.89.CE.BD)
            *   [1.13.2.2 Αυτόματη σύνδεση σε γνωστά δίκτυα](#.CE.91.CF.85.CF.84.CF.8C.CE.BC.CE.B1.CF.84.CE.B7_.CF.83.CF.8D.CE.BD.CE.B4.CE.B5.CF.83.CE.B7_.CF.83.CE.B5_.CE.B3.CE.BD.CF.89.CF.83.CF.84.CE.AC_.CE.B4.CE.AF.CE.BA.CF.84.CF.85.CE.B1)
        *   [1.13.3 Αναλογικό modem, ISDN ή PPPoE DSL](#.CE.91.CE.BD.CE.B1.CE.BB.CE.BF.CE.B3.CE.B9.CE.BA.CF.8C_modem.2C_ISDN_.CE.AE_PPPoE_DSL_2)
    *   [1.14 Δημιουργείστε ένα αρχικό περιβάλλον ramdisk](#.CE.94.CE.B7.CE.BC.CE.B9.CE.BF.CF.85.CF.81.CE.B3.CE.B5.CE.AF.CF.83.CF.84.CE.B5_.CE.AD.CE.BD.CE.B1_.CE.B1.CF.81.CF.87.CE.B9.CE.BA.CF.8C_.CF.80.CE.B5.CF.81.CE.B9.CE.B2.CE.AC.CE.BB.CE.BB.CE.BF.CE.BD_ramdisk)
    *   [1.15 Θέστε τον κωδικό του root](#.CE.98.CE.AD.CF.83.CF.84.CE.B5_.CF.84.CE.BF.CE.BD_.CE.BA.CF.89.CE.B4.CE.B9.CE.BA.CF.8C_.CF.84.CE.BF.CF.85_root)
    *   [1.16 Εγκαταστήστε και ρυθμίστε τον bootloader](#.CE.95.CE.B3.CE.BA.CE.B1.CF.84.CE.B1.CF.83.CF.84.CE.AE.CF.83.CF.84.CE.B5_.CE.BA.CE.B1.CE.B9_.CF.81.CF.85.CE.B8.CE.BC.CE.AF.CF.83.CF.84.CE.B5_.CF.84.CE.BF.CE.BD_bootloader)
        *   [1.16.1 Για μητρικές με BIOS](#.CE.93.CE.B9.CE.B1_.CE.BC.CE.B7.CF.84.CF.81.CE.B9.CE.BA.CE.AD.CF.82_.CE.BC.CE.B5_BIOS)
            *   [1.16.1.1 Syslinux](#Syslinux)
            *   [1.16.1.2 GRUB](#GRUB)
        *   [1.16.2 Για μητρικές με UEFI](#.CE.93.CE.B9.CE.B1_.CE.BC.CE.B7.CF.84.CF.81.CE.B9.CE.BA.CE.AD.CF.82_.CE.BC.CE.B5_UEFI)
            *   [1.16.2.1 Gummiboot](#Gummiboot)
            *   [1.16.2.2 GRUB](#GRUB_2)
    *   [1.17 Αποπροσαρτήστε τις κατατμήσεις και κάντε επανεκκίνηση](#.CE.91.CF.80.CE.BF.CF.80.CF.81.CE.BF.CF.83.CE.B1.CF.81.CF.84.CE.AE.CF.83.CF.84.CE.B5_.CF.84.CE.B9.CF.82_.CE.BA.CE.B1.CF.84.CE.B1.CF.84.CE.BC.CE.AE.CF.83.CE.B5.CE.B9.CF.82_.CE.BA.CE.B1.CE.B9_.CE.BA.CE.AC.CE.BD.CF.84.CE.B5_.CE.B5.CF.80.CE.B1.CE.BD.CE.B5.CE.BA.CE.BA.CE.AF.CE.BD.CE.B7.CF.83.CE.B7)

## Εγκατάσταση

Βρίσκεστε τώρα μπροστά σε μια οθόνη τερματικού με τον λογαριασμό του χρήστη root. Αυτή η διαδικασία είναι αυτόματη.

### Αλλαγή γλώσσας

**Συμβουλή:** Αυτή η διαδικασία είναι προαιρετική για την πλειονότητα των χρηστών. Έχει νόημα μόνο αν σκοπεύεται να γράψετε στην γλώσσα σας σε οποιοδήποτε από τα αρχεία διαμόρφωσης, αν χρησιμοποιείτε σημεία της γλώσσας σας στον κωδικό πρόσβασης του ασύρματου δικτύου σας ή αν τα μηνύματα λάθους του συστήματος να είναι στην γλώσσα σας. Οποιαδήποτε αλλαγή εδώ, επηρεάζει μόνο την διαδικασία της εγκατάστασης.

Από προεπιλογή, η διάταξη του πληκτρολογίου είναι ρυθμισμένη κατά `us`. Αν έχετε ένα μη-[US](https://en.wikipedia.org/wiki/File:KB_United_States-NoAltGr.svg "wikipedia:File:KB United States-NoAltGr.svg") διάταξης πληκτρολόγιο, τρέξτε

`# loadkeys *layout*`

όπου *layout* μπορεί να είναι `fr`, `uk`, `dvorak`, `be-latin1` κ.λ.π.

Δείτε [εδώ](https://en.wikipedia.org/wiki/ISO_3166-1_alpha-2#Officially_assigned_code_elements "wikipedia:ISO 3166-1 alpha-2") για τον κώδικα 2-χαρακτήρων για κάθε χώρα.

Η γραμματοσειρά θα πρέπει επίσης να αλλάξει, διότι οι περισσότερες χώρες χρησιμοποιούν περισσότερους από τους 26 χαρακτήρες [Αγγλικού αλφάβητου](https://en.wikipedia.org/wiki/English_alphabet "wikipedia:English alphabet"). Διαφορετικά μερικοί χαρακτήρες θα εμφανίζονται ως άσπρα τετράγωνα ή ως άλλα σύμβολα. Σημειώστε πως η γραφή κάνει διάκριση πεζών-κεφαλαίων. Θα πρέπει να την πληκτρολογήσετε **ακριβώς** όπως την βλέπετε.

`# setfont Lat2-Terminus16`

Από προεπιλογή η γλώσσα είναι ρυθμισμένη σε English (US). Αν θέλετε να αλλάξετε την γλώσσα για την διαδικασία της εγκατάστασης (*Γερμανικά* σε αυτό το παράδειγμα) αφαιρέστε το σύμβολο `#` μπροστά από [locale](http://www.greendesktiny.com/support/knowledgebase_detail.php?ref=EUH-483) που θέλετε, στο αρχείο `/etc/locale.gen` καθώς και μπροστά από το English (US). Επιλέξτε `UTF-8.`

Για να το επεξεργαστείτε με τον επεξεργαστή κειμένου {{|ic|nano}}, τρέξτε την

`nano /etc/locale.gen` και κάντε τις αλλαγές που επιθυμείτε. Κατόπιν πατήστε `ctrl+x` για έξοδο από τον επεξεργαστή, και όταν ερωτηθείτε αν θέλετε να σώσετε τις αλλαγές πιέστε `Y` & `Enter` για να χρησιμοποιήσετε το ίδιο όνομα αρχείου.

 `# nano /etc/locale.gen` 
```
en_US.UTF-8 UTF-8
de_DE.UTF-8 UTF-8
```

```
# locale-gen
# export LANG=de_DE.UTF-8

```

### Δημιουργία σύνδεσης με το διαδίκτυο

**Προσοχή:** Μετά την έκδοση v197, το πακέτο udev δεν δίνει ονόματα στα interfaces (διεπαφές) σας σύμφωνα με τον κανόνα wlanX & ethX. Αν έρχεστε από άλλη διανομή ή κάνετε επανεγκατάσταση του Arch και δεν είστε γνώστες των νέων ονομάτων των intefaces σας, μην υποθέσετε πως το ασύρματό σας θα έχει όνομα wlan0 και το ενσύρματό σας eth0\. Χρησιμοποιείστε την εντολή `ip link` ώστε να δείτε τα νέα ονόματα των interfaces σας.

Ο δαίμονας `dhcpcd` φορτώνεται αυτόματα κατά την διαδικασία εκκίνησης του συστήματος και θα προσπαθήσει να εκκινήσει την ενσύρματη σύνδεση. Δοκιμάστε να κάνετε ping έναν server (εξυπηρετητή) ώστε να διαπιστώσετε αν έχει επιτευχθεί η σύνδεση με το διαδίκτυο. Για παράδειγμα τους servers της Google:

 `# ping -c 3 www.google.com` 
```
PING www.l.google.com (74.125.132.105) 56(84) bytes of data.
64 bytes from wb-in-f105.1e100.net (74.125.132.105): icmp_req=1 ttl=50 time=17.0 ms
64 bytes from wb-in-f105.1e100.net (74.125.132.105): icmp_req=2 ttl=50 time=18.2 ms
64 bytes from wb-in-f105.1e100.net (74.125.132.105): icmp_req=3 ttl=50 time=16.6 ms

--- www.l.google.com ping statistics ---
3 packets transmitted, 3 received, 0% packet loss, time 2003ms
rtt min/avg/max/mdev = 16.660/17.320/18.254/0.678 ms
```

Αν λάβετε το σφάλμα `ping: unknown host` πρώτα δείτε αν έχει πρόβλημα το καλώδιο σύνδεσης ή το σήμα του ασύρματου είναι πολύ ασθενές. Εάν τίποτα από αυτά δεν ισχύει, τότε θα πρέπει να δημιουργήσετε χειροκίνητα την σύνδεση με το διαδίκτυο με την μέθοδο που περιγράφεται παρακάτω. Μόλις η σύνδεση επιτευχθεί, μετακινηθείτε στο [Προετοιμασία του μέσου αποθήκευσης](#.CE.A0.CF.81.CE.BF.CE.B5.CF.84.CE.BF.CE.B9.CE.BC.CE.B1.CF.83.CE.AF.CE.B1_.CF.84.CE.BF.CF.85_.CE.BC.CE.AD.CF.83.CE.BF.CF.85_.CE.B1.CF.80.CE.BF.CE.B8.CE.AE.CE.BA.CE.B5.CF.85.CF.83.CE.B7.CF.82)

### Ενσύρματη σύνδεση

Ακολουθήστε αυτή την διαδικασία αν θέλετε να επιτύχετε ενσύρματη σύνδεση με το διαδίκτυο μέσω μια στατικής διεύθυνσης ip (static ip).

Πρώτα απενεργοποιείστε το dhcpcd που ξεκίνησε αυτόματα κατά την εκκίνηση του συστήματος.

`# systemctl stop dhcpcd.service`

Βρείτε το όνομα που έχει πάρει το ενσύρματο interface σας

 `# ip link` 
```
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN mode DEFAULT
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
2: enp2s0f0: <BROADCAST,MULTICAST> mtu 1500 qdisc noop state DOWN mode DEFAULT qlen 1000
    link/ether 00:11:25:31:69:20 brd ff:ff:ff:ff:ff:ff
3: wlp3s0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc mq state UP mode DORMANT qlen 1000
    link/ether 01:02:03:04:05:06 brd ff:ff:ff:ff:ff:ff
```

Σε αυτό το παράδειγμα το Ενσύρματο interface είναι η `enp2s0f0`. Αν δεν είστε σίγουροι, το όνομα του ενσύρματου interface είναι πιο πιθανό ξεκινά με τον χαρακτήρα `e` παρά με τους χαρακτήρες `lo` & `w`. Επίσης μπορείτε να το διαπιστώσετε με την `iwconfig` ώστε να δείτε ποια interfaces δεν είναι ασύρματα.

 `# iwconfig` 
```
enp2s0f0  no wireless extensions.
wlp3s0    IEEE 802.11bgn  ESSID:"NETGEAR97"
          Mode:Managed  Frequency:2.427 GHz  Access Point: 2C:B0:5D:9C:72:BF
          Bit Rate=65 Mb/s   Tx-Power=16 dBm
          Retry  long limit:7   RTS thr:off   Fragment thr:off
          Power Management:on
          Link Quality=61/70  Signal level=-49 dBm
          Rx invalid nwid:0  Rx invalid crypt:0  Rx invalid frag:0
          Tx excessive retries:0  Invalid misc:430   Missed beacn:0
lo        no wireless extensions.
```

Σε αυτό το παράδειγμα, τα interfaces `enp2s0f0 & lo` δεν έχουν ασύρματη δυνατότητα, το οποίο μας οδηγεί στο συμπέρασμα πως η `enp2s0f0` είναι το ενσύρματο interface μας.

Επίσης θα πρέπει να γνωρίζετε:

*   Την στατική διεύθυνση ip (static ip address).
*   Την μάσκα του υποδικτύου (subnet mask).
*   Την διεύθυνση ip εξόδου προς το διαδίκτυο (Gateway ip).
*   Τις διευθύνσεις ip για τους DNS (εξυπηρετητές ονομάτων).
*   Το όνομα του δικτύου που θα συνδεθείτε (εκτός και αν είστε σε τοπικό δίκτυο το οποίο σε αυτή την περίπτωση μπορείτε να δημιουργήσετε εσείς) (Domain name).

Ενεργοποιείστε το ενσύρματο interface σας (π.χ. `enp2s0f0`)

`# ip link set enp2s0f0 up`

Δώστε την διεύθυνση ip

`# ip addr add ip_address/mask_bits dev interface_name`

Για παράδειγμα

`# ip addr add 192.168.1.2/24 dev enp2s0f0`

Για περισσότερες πληροφορίες, τρέξτε `man ip`.

Προσθέστε την διεύθυνση ip της πύλη εξόδου στο διαδίκτυο με την παρακάτω εντολή, αντικαθιστώντας την με την διεύθυνση ip της δικής σας πύλης εξόδου.

`# ip route add default via ip_address`

Επεξεργαστείτε το αρχείο `resolv.conf` αντικαθιστώντας τις διευθύνσεις ip των εξυπηρετητών ονομάτων (DNS) με αυτών που επιθυμείτε και προσθέτοντας το όνομα δικτύου σας.

 `# nano /etc/resolv.conf` 
```
nameserver 61.23.173.5
nameserver 61.95.849.8
search example.com
```

**Σημείωση:** Μέχρι στιγμής μπορείτε να συμπεριλάβετε έως τρεις γραμμές με `nameservers`. Εάν χρειαστεί να ξεπεράσετε αυτόν τον περιορισμό μπορείτε να χρησιμοποιήσετε έναν τοπικό εξυπηρετητή ονομάτων προσωρινής μνήμης (locally caching nameserver) όπως τον [Dnsmasq](/index.php/Dnsmasq "Dnsmasq").

Θα πρέπει να έχετε μια ενεργή ενσύρματη σύνδεση με το διαδίκτυο. Αν όχι, δείτε [Διαμόρφωση δικτύου](/index.php/Configuring_Network_(%CE%95%CE%BB%CE%BB%CE%B7%CE%BD%CE%B9%CE%BA%CE%AC) "Configuring Network (Ελληνικά)").

### Ασύρματη σύνδεση

Ακολουθήστε την παρακάτω διαδικασία αν επιθυμείτε ασύρματη σύνδεση (wifi) κατά την εγκατάσταση.

Πρώτα, βρείτε το όνομα του ασύρματου interface σας.

 `# iw dev` 
```
phy#0
        Interface wlp3s0
                ifindex 3
                wdev 0x1
                addr 00:21:6a:5e:52:bc
                type managed
```

Σε αυτό το παράδειγμα, το όνομα του ασύρματου interface σας είναι το `wlp3s0`. Αν δεν είστε σίγουροι, το όνομα του ασύρματου interface, είναι πιθανότερο να ξεκινά με τον χαρακτήρα `w` παρά με τους χαρακτήρες `lo` ή `e`.

**Σημείωση:** Αν δείτε έξοδο της εντολής παραπλήσια με την παραπάνω, τότε είναι πιθανό να μην έχει φορτωθεί ο οδηγός (driver) του ασύρματου interface σας. Σε αυτή την περίπτωση θα πρέπει να τον φορτώσετε εσείς. Δείτε [Ρύθμιση ασύρματου δικτύου](/index.php/Wireless_Setup_(%CE%95%CE%BB%CE%BB%CE%B7%CE%BD%CE%B9%CE%BA%CE%AC) "Wireless Setup (Ελληνικά)") για περισσότερες πληροφορίες.

Ενεργοποιείστε το interface.

`# ip link set wlp3s0 up`

Οι περισσότερες ασύρματες συσκευές απαιτούν υλικό λογισμικού (firmware) ώστε να υποστηρίξουν τον κατάλληλο οδηγό (driver). Ο πυρήνας (kernel) προσπαθεί να τις αναγνωρίσει και να φορτώσει το κατάλληλο λογισμικό και για τα δύο αυτόματα. Αν η έξοδος της παραπάνω εντολής είναι κάπως έτσι `SIOCSIFFLAGS: No such file or directory`, σημαίνει πως θα πρέπει να φορτώσετε και τα δύο λογισμικά χειροκίνητα. Αν δεν είστε σίγουροι, δώστε την εντολή `dmseg` ώστε να δείτε τα σχετικά μετο ασύρματο interface σας μηνύματα λάθους του πυρήνα (kernel). Για παράδειγμα, αν έχετε μια ασύρματη κάρτα Intel δώστε σε τερματικό την παρακάτω εντολή ώστε να εμφανιστούν τα σχετικά με το firmware μηνύματα λάθους.

 `# dmesg | grep firmware`  `firmware: requesting iwlwifi-5000-1.ucode` 

Αν δεν υπάρχει έξοδος, μπορούμε να συμπεράνουμε πως η ασύρματη κάρτα σας δεν απαιτεί την ύπαρξη λογισμικού υλικού (firmware).

**Προσοχή:** Τα πακέτα που αφορούν λογισμικό υλικού (firmware) για όποιες ασύρματες συσκευές το απαιτούν είναι ήδη εγκατεστημένα στο περιβάλλον του δίσκου εκκίνησης (live cd) στην διαδρομή `/usr/lib/firmware`, **αλλά πρέπει να εγκατασταθούν ξεχωριστά στο πραγματικό δικό σας σύστημα ώστε να σας παρέχουν ασύρματη δικτύωση μετά την επανεκκίνηση και την πρώτη σας είσοδο σε αυτό**. Η εγκατάσταση πακέτων καλύπτεται αργότερα σε αυτόν τον οδηγό. Βεβαιωθείτε πως έχετε εγκαταστήσει την λειτουργική μονάδα (module) και το ανάλογο λογισμικό υλικού (firmware) πριν την επανεκκίνηση. Δείτε [Ρύθμιση ασύρματου δικτύου](/index.php/Wireless_Setup_(%CE%95%CE%BB%CE%BB%CE%B7%CE%BD%CE%B9%CE%BA%CE%AC) "Wireless Setup (Ελληνικά)") αν δεν είστε σίγουροι για την ανάγκη εγκατάστασης του απαιτούμενου αντίστοιχου λογισμικού υλικού (firmware) για την συγκεκριμένη συσκευή σας.

Στην συνέχεια, χρησιμοποιείστε την εντολή `wifi-menu` που παρέχει το πακέτο [netctl](https://www.archlinux.org/packages/?name=netctl) ώστε να συνδεθείτε στο δίκτυο

`# wifi-menu wlp3s0`

**Σημείωση:** Το πακέτο netctl περιέχεται στο live-cd.

#### Χωρίς την χρήση της wifi-menu

Εναλλακτικά μπορείτε να χρησιμοποιήσετε την εντολή `iw dev wlp3s0 scan` ώστε να δείτε τα διαθέσιμα δίκτυα με το χαρακτηριστικό τους όνομα (SSID), κατόπιν μπορείτε να συνδεθείτε δίνοντας την παρακάτω

`# wpa_supplicant -B -i wlp3s0 -c <(wpa_passphrase "ssid" "psk")`

Πρέπει να αντικαταστήσετε το *ssid* με το όνομα του δικούς σας δικτύου (π.χ. linksys...) και το *psk* με τον δικό σας κρυφό κωδικό σύνδεσης, **διατηρώντας τα εισαγωγικά στίγματα (" ") γύρω από το όνομα και τον κωδικό σας**.

Τέλος θα πρέπει να δώσετε στην σύνδεσή σας μια διεύθυνση ip. Αυτό το επιτυγχάνουμε με την εντολή

`# dhcpcd wlp3s0`

Εάν αυτό δεν έχει αποτέλεσμα, δώστε τις παρακάτω εντολές

```
# echo 'ctrl_interface=DIR=/run/wpa_supplicant' > /etc/wpa_supplicant.conf
# wpa_passphrase <ssid> <passphrase> >> /etc/wpa_supplicant.conf
# ip link set <interface> up # May not be needed, but does no harm in any case
# wpa_supplicant -B -D nl80211 -c /foobar.conf -i <interface name>
# dhcpcd -A <interface name>

```

### Αναλογικό modem, ISDN ή PPPoE DSL

Για αναλογική σύνδεση pstn, isdn ή xDSL, δείτε [Σύνδεση με αναλογικό modem](/index.php?title=Direct_Modem_Connection_(%CE%95%CE%BB%CE%BB%CE%B7%CE%BD%CE%B9%CE%BA%CE%AC)&action=edit&redlink=1 "Direct Modem Connection (Ελληνικά) (page does not exist)")

### Μέσω διακομιστή μεσολάβησης (proxy server)

Αν συνδέεστε μέσω Διακομιστή μεσολάβησης (proxy server) δείτε [Ρύθμιση διακομιστή μεσολάβησης](/index.php?title=Proxy_settings_(%CE%95%CE%BB%CE%BB%CE%B7%CE%BD%CE%B9%CE%BA%CE%AC)&action=edit&redlink=1 "Proxy settings (Ελληνικά) (page does not exist)").

### Προετοιμασία του μέσου αποθήκευσης

**Προσοχή:** Η διαμέριση του δίσκου μπορεί να καταστρέψει τα δεδομένα σας. Σας **συμβουλεύουμε να πάρετε αντίγραφα ασφαλείας** όλων των σημαντικών δεδομένων σας πριν προχωρήσετε

#### Επιλέξτε έναν τύπο πίνακα κατάτμησης

Πρέπει να επιλέξετε μεταξύ [GUID Partition Table](/index.php/GUID_Partition_Table_(%CE%95%CE%BB%CE%BB%CE%B7%CE%BD%CE%B9%CE%BA%CE%AC) "GUID Partition Table (Ελληνικά)") (GPT) και [Master Boot Record](/index.php/Master_Boot_Record "Master Boot Record") (MBR). To GPT είναι πιο σύγχρονο και συνίσταται για νέες εγκαταστάσεις.

*   Αν θέλετε να στήσετε ένα σύστημα το οποίο θα είναι διπλής εκκίνησης με windows, τότε πρέπει να δείξετε ιδιαίτερη προσοχή σε αυτό. Δείτε στο [Partitioning#Choosing between GPT and MBR](/index.php/Partitioning#Choosing_between_GPT_and_MBR "Partitioning") για τις «φρικιαστικές» λεπτομέρειες.
*   Προτείνεται να χρησιμοποιείτε πάντα το GPT για UEFI boot, καθώς μερικά UEFI firmwares δεν επιτρέπουν τον συνδυασμό UEFI-MBR boot.
*   Μερικά συστήματα BIOS μπορεί να έχουν προβλήματα με το GPT. Δείτε στο [http://mjg59.dreamwidth.org/8035.html](http://mjg59.dreamwidth.org/8035.html) και στο [http://rodsbooks.com/gdisk/bios.html](http://rodsbooks.com/gdisk/bios.html) για περισσότερες πληροφορίες και λύσεις.

**Σημείωση:** Αν κάνετε εγκατάσταση σε ένα USB stick, δείτε στο [Installing Arch Linux on a USB key](/index.php/Installing_Arch_Linux_on_a_USB_key "Installing Arch Linux on a USB key")

#### Εργαλείο κατατμήσεων

Για τους εντελώς αρχάριους προτείνεται να χρησιμοποιήσουν ένα εργαλείο κατατμήσεων με γραφικό περιβάλλον. Το [GParted](http://gparted.sourceforge.net/download.php) είναι ένα καλό παράδειγμα τέτοιου εργαλείου και [παρέχεται με ένα "live" CD](http://gparted.sourceforge.net/livecd.php). Συμπεριλαμβάνεται επίσης στα περισσότερα CDs γνωστών διανομών Linux όπως το [Ubuntu](https://en.wikipedia.org/wiki/Ubuntu_(operating_system) και το [Linux Mint](https://en.wikipedia.org/wiki/Linux_Mint "wikipedia:Linux Mint"). Ένας δίσκος πρέπει πρώτα να [διαμεριστεί](/index.php/Partitioning "Partitioning") και τα διαμερίσματα πρέπει να τροποποιηθούν (format) με το κατάλληλο [σύστημα αρχείων](/index.php/File_systems "File systems") πριν την επανεκκίνηση.

**Συμβουλή:** Όταν χρησιμοποιείτε το Gparted και επιλέξετε να δημιουργήσετε ένα νέο διαμέρισμα, ο πίνακας του διαμερίσματος από προεπιλογή είναι το "msdos". Αν θέλετε να δημιουργήσετε ένα διαμέρισμα με GPT πίνακα, πρέπει να επιλέξετε το μενού "Advanced" και μετά να επιλέξτε "gpt" από την αναπτυσσόμενη λίστα.

Αν και το gparted είναι ευκολότερο στην χρήση, αν απλά θέλετε να δημιουργήσετε μερικά διαμερίσματα σε έναν καινούριο δίσκο, μπορείτε να το κάνετε χρησιμοποιώντας ένα εργαλείο από τις [παραλλαγές της fdisk](/index.php/Partitioning#Partitioning_tools "Partitioning") τα οποία συμπεριλαμβάνονται στο μέσον εγκατάστασης. Υπάρχουν σύντομες οδηγίες χρήσης και για την [gdisk](/index.php/Partitioning#Gdisk_usage_summary "Partitioning"), αλλά και για την [fdisk](/index.php/Partitioning#Fdisk_usage_summary "Partitioning").

#### Οργανόγραμμα κατατμήσεων

Μπορείτε να αποφασίσετε σε πόσες κατατμήσεις πρέπει να χωριστεί ο δίσκος και για ποιον κατάλογο θα χρησιμοποιηθεί η κάθε κατάτμηση. Η αντιστοίχηση των κατατμήσεων με τους καταλόγους (συνήθως τα αποκαλούμε 'σημεία προσάρτησης') είναι το λεγόμενο [Partition scheme](/index.php/Partitioning#Partition_scheme "Partitioning"). Η πιο απλή μέθοδος και όχι απαραίτητα κακή, είναι να δημιουργήσετε μια μεγάλη κατάτμηση για το `/`. Μια άλλη δημοφιλής επιλογή είναι να έχετε μια κατάτμηση `/` και μια `/home`.

**Επιπρόσθετες απαιτούμενες κατατμήσεις:**

*   Αν έχετε μια μητρική με [UEFI](/index.php/UEFI "UEFI"), θα χρειαστεί να δημιουργήσετε μια έξτρα κατάτμηση [EFI System Partition](/index.php/Unified_Extensible_Firmware_Interface#EFI_System_Partition "Unified Extensible Firmware Interface") (συνίσταται περίπου 1GB σε μέγεθος).
*   Αν έχετε μια μητρική κάρτα με BIOS (ή σχεδιάζετε να εκκινείτε σε συμβατότητα BIOS) και θέλετε να στήσετε τον GRUB σε ένα δίσκο με GPT πίνακα κατατμήσεων, θα χρειαστεί να δημιουργήσετε ένα έξτρα [BIOS Boot Partition](/index.php/GRUB#GUID_Partition_Table_.28GPT.29_specific_instructions "GRUB") μεγέθους 1 ή 2MB και τύπου `EF02`. Ο Syslinux δεν χρειάζεται κάτι τέτοιο.
*   Αν θέλετε να κρυπτογραφήσετε ([Disk encryption](/index.php/Disk_encryption "Disk encryption")) το σύστημα αρχείων, αυτό πρέπει να αντικατοπτρίζει το οργανόγραμμα των κατατμήσεων σας. Δεν υπάρχει πρόβλημα αν θέλετε να προσθέσετε κρυπτογραφημένους φακέλους ή να κρυπτογραφήσετε όλο τον προσωπικό σας κατάλογο (home) αφού εγκαταστήσετε το σύστημα.
*   Αν σκοπεύετε να χρησιμοποιήσετε ένα διαφορετικό σύστημα αρχείων από το ext4 (όπως [F2fs](/index.php/F2fs "F2fs")), πρέπει πρώτα να τσεκάρετε αν ο GRUB υποστηρίζει αυτό το σύστημα αρχείων. Διαφορετικά θα πρέπει να δημιουργήσετε μια ξεχωριστή κατάτμηση σε σύστημα αρχείων ext4 για το `/boot`.

Δείτε το κεφάλαιο [Swap](/index.php/Swap "Swap") για λεπτομέρειες, αν θέλετε να δημιουργήσετε μια κατάτμηση swap ή ένα αρχείο swap. Ένα αρχείο swap είναι ευκολότερο να αλλάξει μέγεθος απ' ότι μια κατάτμηση, αλλά δεν μπορεί να χρησιμοποιηθεί με ένα σύστημα αρχείων Btrfs.

#### Εκτιμήσεις για διπλή εκκίνηση με Windows

Αν έχετε ήδη μια εγκατάσταση λειτουργικού, να ξέρετε πως αν μετατρέψετε τον πίνακα κατατμήσεων στον δίσκο τότε θα χάσετε όλα σας τα δεδομένα.

Ο προτεινόμενος τρόπος για να στήσετε ένα σύστημα διπλής εκκίνηση Linux/Windows, είναι να εγκαταστήστε πρώτα τα Windows, χρησιμοποιώντας ένα κομμάτι του δίσκου για τις κατατμήσεις. Όταν τελειώσετε με την εγκατάσταση των Windows, τότε εκκινήστε στο περιβάλλον εγκατάστασης του Linux και εκεί μπορείτε να προσθέσετε επιπλέον κατατμήσεις ενώ θα αφήσετε τις κατατμήσεις των Windows απείραχτες.

Κάποιοι νεότεροι υπολογιστές έρχονται με Windows 8 προ-εγκατεστημένα, καθώς χρησιμοποιούν και το sercure boot. Το Arch Linux αυτή τη στιγμή δεν υποστηρίζει το secure boot. Επίσης κάποιες εγκαταστάσεις των Windows 8 έχει παρατηρηθεί πως δεν εκκινούν όταν το secure boot είναι κλειστό. Σε μερικές περιπτώσεις είναι απαραίτητο να κλείσετε και το secure boot, καθώς και το fastboot από το BIOS, για να επιτρέψετε στα Windows 8 να εκκινήσουν με το secure boot κλειστό. Όμως υπάρχουν κάποιοι κίνδυνοι ασφαλείας κλείνοντας το secure boot και εκκινώντας τα Windows 8\. Γι' αυτό τον λόγο ίσως είναι καλύτερο να αφήσετε τα Windows 8 απείραχτα και να εγκαταστήσετε το Linux σε έναν ξεχωριστό σκληρό δίσκο - ο οποίος μπορεί να κατατμηθεί από την αρχή, χρησιμοποιώντας έναν πίνακα κατατμήσεων GPT. Αυτή η διαδικασία δεν είναι συνήθως εύκολη για μικρά laptop. Αυτή τη στιγμή το Secure Boot δεν βρίσκεται σε μια σταθερή έκδοση για αξιόπιστες εργασίες, ακόμη και για εκδόσεις Linux που το υποστηρίζουν.

**Προσοχή:** Τα Windows 8 συμπεριλαμβάνουν ένα νέο χαρακτηριστικό που ονομάζεται Fast Startup, το οποίο μετατρέπει το shutdown(κλείσιμο) σε suspend-to-disk(αδρανοποίηση). Το αποτέλεσμα αυτού είναι ότι, όλα τα συστήματα αρχείων που είναι κοινά ανάμεσα σε Windows 8 και οποιοδήποτε άλλο Λ.Σ. είναι σχεδόν σίγουρο πως θα πάθουν ζημιά όταν εκκινείτε μεταξύ των δύο Λ.Σ. Ακόμη και αν δεν έχετε σκοπό να μοιραστείτε τα συστήματα αρχείων, το EFI System Partition είναι πιθανό να πάθει ζημιά σε ένα σύστημα με EFI. Γι' αυτό τον λόγο είναι καλό να απενεργοποιήσετε το Fast Startup , όπως περιγράφεται [εδώ,](http://www.eightforums.com/tutorials/6320-fast-startup-turn-off-windows-8-a.html) πριν εγκαταστήσετε Linux σε οποιονδήποτε υπολογιστή χρησιμοποιεί Windows 8.

Αν έχετε ήδη δημιουργήσει τις κατατμήσεις, προχωρήστε στο [#Δημιουργία_συστήματος_αρχείων](#.CE.94.CE.B7.CE.BC.CE.B9.CE.BF.CF.85.CF.81.CE.B3.CE.AF.CE.B1_.CF.83.CF.85.CF.83.CF.84.CE.AE.CE.BC.CE.B1.CF.84.CE.BF.CF.82_.CE.B1.CF.81.CF.87.CE.B5.CE.AF.CF.89.CE.BD)

Διαφορετικά, δείτε το παρακάτω παράδειγμα.

#### Παράδειγμα

Το μέσο εγκατάστασης του Arch Linux περιλαμβάνει τα ακόλουθα εργαλεία κατάτμησης: `fdisk`, `gdisk`, `cfdisk`, `cgdisk`, `parted`.

**Συμβουλή:** Χρησιμοποιήστε την εντολή `lsblk` για να δείτε τη λίστα των σκληρών δίσκων που είναι συνδεδεμένοι στο σύστημα σας, καθώς επίσης και τα μεγέθη των υπάρχοντων κατατμήσεων τους. Αυτό θα σας βοηθήσει στο να είστε σίγουροι ότι δημιουργείτε κατατμήσεις στο σωστό δίσκο.

Το σύστημα του παραδείγματος περιλαμβάνει μία κατάτμηση root 15 GB, και μία κατάτμηση [home](/index.php/Partitioning#.2Fhome "Partitioning") για τον υπόλοιπο χώρο. Επιλέξτε είτε [MBR](/index.php/MBR "MBR") είτε [GPT](/index.php/GPT "GPT"). Μην επιλέξετε και τα δύο!

Πρέπει να τονίσουμε ότι η δημιουργία κατατμήσεων είναι μια προσωπική επιλογή και ότι αυτό το παράδειγμα χρησιμοποιείται μόνο για επεξηγηματικούς λόγους. Βλέπε [Partitioning](/index.php/Partitioning "Partitioning").

##### Χρησιμοποιώντας το cgdisk για τη δημιουργία κατατμήσεων τύπου GPT

```
# cgdisk /dev/sda

```

	Root

*   Επιλέξτε *New* (ή πατήστε `N`) – `Enter` για τον πρώτο τομέα (2048) – πληκτρολογήστε `15G` – `Enter` για τον προκαθορισμένο κώδικα hex (8300) – `Enter` για ένα κενό όνομα κατάτμησης.

	Home

*   Πιέστε το κάτω βελάκι μερικές φορές για να μετακινηθείτε στην περιοχή μεγαλύτερου ελεύθερου χώρου.
*   Επιλέξτε *New* (ή πατήστε `N`) – `Enter` για τον πρώτο τομέα – `Enter` για να χρησιμοποιήσετε τον υπόλοιπο δίσκο (ή θα μπορούσατε να πληκτρολογήσετε το επιθυμητό μέγεθος, για παράδειγμα `30G`) – `Enter` για τον προκαθορισμένο κώδικα hex (8300) – `Enter` για ένα κενό όνομα κατάτμησης.

Θα πρέπει να δείχνει κάπως έτσι:

```
Part. #     Size        Partition Type            Partition Name
----------------------------------------------------------------
            1007.0 KiB  free space
   1        15.0 GiB    Linux filesystem
   2        123.45 GiB  Linux filesystem

```

Ελένξτε διπλά και σιγουρευτείτε ότι είστε ικανοποιημένοι από τα μεγέθη των κατατμήσεων καθώς επίσης και από τον πίνακα κατατμήσεων πριν συνεχίσετε.

Εάν επιθυμείτε να ξεκινήσετε την διαδικασία από την αρχή, μπορείτε απλά να επιλέξετε *Quit* (ή να πατήσετε `Q`) για έξοδο χωρίς αποθήκευση αλλαγών και μετά να ξαναξεκινήσετε το *cgdisk*.

Εάν είστε ικανοποιημένοι, επιλέξτε *Write* (ή πατήστε `Shift+W`) για να ολοκληρώσετε και να γράψετε τον πίνακα κατατμήσεων στον δίσκο. Πληκτρολογήστε `yes` και επιλέξτε *Quit* (ή πατήστε `Q`) για έξοδο χωρίς περαιτέρω αλλαγές.

##### Χρησιμοποιώντας το fdisk για τη δημιουργία κατατμήσεων τύπου MBR

**Σημείωση:** Υπάρχει επίσης το *cfdisk*, που έχει παρόμοιο περιβάλλον με το *cgdisk*, αλλά προς το παρόν δεν βρίσκει αυτόματα την πρώτη κατάτμηση. Αυτός είναι ο λόγος που χρησιμοποιούμε εδώ το κλασσικό εργαλείο *fdisk*.

Εκκινείστε το *fdisk* με:

```
# fdisk /dev/sda

```

Δημιουργείστε τον πίνακα κατατμήσεων:

*   `Command (Εντολή) (m για βοήθεια):` πληκτρολογήστε `o` και πατήστε `Enter`

Έπειτα δημιουργήστε την πρώτη κατάτμηση:

1.  `Command (Εντολή) (m για βοήθεια):` πληκτρολογήστε `n` και πατήστε `Enter`
2.  Partition type (Είδος κατάτμησης): `Επιλέξτε (προκαθορισμένο το p (πρωτεύων)):` πατήστε `Enter`
3.  `Partition number (αριθμός κατάτμησης) (1-4, προκαθορισμένο το 1):` πατήστε `Enter`
4.  `First sector (Πρώτος τομέας) (2048-209715199, προκαθορισμένος ο 2048):` πατήστε `Enter`
5.  `Last sector, +sectors or +size{K,M,G} (Τελευταίος τομέας, +τομείς ή +μέγεθος{K,M,G}) (2048-209715199....., προκαθορισμένος ο 209715199):` πληκτρολογήστε `+15G` και πατήστε `Enter`

Έπειτα δημιουργήστε την δεύτερη κατάτμηση:

1.  `Command (Εντολή) (m για βοήθεια):` πληκτρολογήστε `n` και πατήστε `Enter`
2.  Partition type (Είδος κατάτμησης): `Επιλέξτε (προκαθορισμένο το p (πρωτεύων)):` πατήστε `Enter`
3.  `Partition number (αριθμός κατάτμησης) (1-4, προκαθορισμένο το 2):` πατήστε `Enter`
4.  `First sector (Πρώτος τομέας) (31459328-209715199, προκαθορισμένος ο 31459328):` πατήστε `Enter`
5.  `Last sector, +sectors or +size{K,M,G} (Τελευταίος τομέας, +τομείς ή +μέγεθος{K,M,G}) (31459328-209715199....., προκαθορισμένος ο 209715199):` πατήστε `Enter`

Τώρα κάντε προεσκόπιση του νέου πίνακα κατατμήσεων:

*   `Command (Εντολή) (m για βοήθεια):` πληκτρολογήστε `p` και πατήστε `Enter`

```
Disk /dev/sda: 107.4 GB, 107374182400 bytes, 209715200 sectors
Units = sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 512 bytes
I/O size (minimum/optimal): 512 bytes / 512 bytes
Disk identifier: 0x5698d902

   Device Boot     Start         End     Blocks   Id  System
/dev/sda1           2048    31459327   15728640   83   Linux
/dev/sda2       31459328   209715199   89127936   83   Linux

```

Και γράψτε τις αλλαγές στον δίσκο:

*   `Command (Εντολή) (m για βοήθεια):` πληκτρολογήστε `w` και πατήστε `Enter`

Εάν όλα πήγαν καλά το fdisk θα τερματιστεί τώρα με το ακόλουθο μύνημα:

```
The partition table has been altered!

Calling ioctl() to re-read partition table.
Syncing disks. 

```

Στην περίπτωση που αυτό δεν δουλέψει επειδή το *fdisk* παρουσίασε κάποιο σφάλμα, μπορείτε να χρησιμοποιήσετε την εντολή `q` για να τερματίσετε.

#### Δημιουργία συστήματος αρχείων

Η δημιουργία και μόνο κατατμήσεων δεν είναι αρκετή, οι κατατμήσεις χρειάζονται επίσης ένα [σύστημα αρχείων](/index.php/File_systems "File systems"). Για να κάνετε format τις κατατμήσεις με το σύστημα αρχείων ext4:

**Προσοχή:** Ελένξτε διπλά και τριπλά ότι θέλετε να κάνετε format στα `/dev/sda1` και `/dev/sda2`. Για βοήθεια μπορείτε να χρησιμοποιήσετε το `lsblk`.

```
# mkfs.ext4 /dev/sda1
# mkfs.ext4 /dev/sda2

```

Εάν έχετε δημιουργήσει κάποια κατάτμηση για χρήση ως swap (κωδικός 82), μην ξεχάσετε να του κάνετε format και να το ενεργοποιήσετε με:

```
# mkswap /dev/sda*X*
# swapon /dev/sda*X*

```

Για UEFI, θα πρέπει να κάνετε format την Κατάτμηση Συστήματος EFI (για παράδειγμα /dev/sd*XY*) με:

```
# mkfs.fat -F32 /dev/sd*XY*

```

### Προσαρτήστε τις κατατμήσεις

Κάθε κατάτμηση αναγνωρίζεται με έναν αριθμό στο τέλος. Για παράδειγμα το `sda1`, δείχνει την πρώτη κατάτμηση στον πρώτο δίσκο, όταν το `sda` είναι ολόκληρος ο (πρώτος) δίσκος.

Για να δείτε την τρέχουσα διάταξη κατατμήσεων:

```
# lsblk /dev/sda

```

**Σημείωση:** Μην προσαρτείτε περισσότερες από μια κατατμήσεις στον ίδιο κατάλογο. Και δώστε σημασία γιατί η σειρά προσάρτησης είναι σημαντική.

Πρώτα, προσαρτείστε την κατάτμηση root στο `/mnt`. Ακολουθώντας το παραπάνω παράδειγμα (στην δική σας περίπτωση μπορεί να διαφέρει), θα είναι:

```
# mount /dev/sda1 /mnt

```

Μετά προσαρτείστε την κατάτμηση home και όποια άλλη ξεχωριστή κατάτμηση έχετε πιθανόν φτιάξει, (`/boot`, `/var`...κλπ.)

```
# mkdir /mnt/home
# mount /dev/sda2 /mnt/home

```

Σε περίπτωση που έχετε UEFI μητρική κάρτα, προσαρτείστε το σύστημα κατάτμηση EFI στο σημείο προσάρτησης που θέλετε. Στο παρακάτω παράδειγμα χρησιμοποιείται το `/boot`:

```
# mkdir -p /mnt/boot
# mount /dev/sd*XY* /mnt/boot

```

### Επιλέξτε ένα mirror

**Σημείωση:** Ως mirror εκλάβετε έναν server ο οποίος φιλοξενεί τα πακέτα του Arch Linux. Όσο πιο κοντά σας βρίσκεται, τόσο το καλύτερο. Για την Ελλάδα υπάρχουν τρεις τέτοιοι servers (mirrors) διαθέσιμοι. Μπορείτε να τους δείτε μέσα στο αρχείο `mirrorlist`.

Πριν προχωρήσετε στην εγκατάσταση, μπορεί να θέλετε να επεξεργαστείτε το αρχείο `mirrorlist` και να τοποθετήσετε το mirror που σας ενδιαφέρει πρώτο. Ένα αντίγραφο αυτού του αρχείου θα εγκατασταθεί στο σύστημά σας μέσω του `pacstrap`, οπότε αξίζει να το κάνετε σωστά.

 `# nano /etc/pacman.d/mirrorlist` 
```
##
## Arch Linux repository mirrorlist
## Sorted by mirror score from mirror status page
## Generated on 2012-MM-DD
##

Server = http://mirror.example.xyz/archlinux/$repo/os/$arch
...
```

*   `Alt+6` για να αντιγράψετε μια γραμμή `Server`.
*   `PageUp` για να πλοηγηθείτε προς τα πάνω.
*   `Ctrl+U` για να την επικολλήσετε στην αρχή της λίστας.
*   `Ctrl+X` για έξοδο. Μόλις σας ζητηθεί να σώσετε τις αλλαγές πατήστε `Y` και `Enter` για να σωθούν οι αλλαγές στο ίδιο αρχείο.

Αν θέλετε μπορείτε να κάνετε το mirror σας ως το **μοναδικό** διαθέσιμο και να απαλλαγείτε από όλα τα υπόλοιπα χρησιμοποιώντας το `Ctrl+K`. Είναι όμως καλή ιδέα να έχετε και μερικά mirrors ακόμη διαθέσιμα σε περίπτωση που κάποιο δεν λειτουργεί.

**Συμβουλή:**

*   Χρησιμοποιείστε το [Mirrorlist Generator](https://www.archlinux.org/mirrorlist/) για να δείτε μια ενημερωμένη λίστα για την χώρα σας. Τα HTTP mirrors είναι ταχύτερα από τα FTP, λόγω κάποιου χαρακτηριστικού που λέγεται [keepalive](https://en.wikipedia.org/wiki/Keepalive "wikipedia:Keepalive"). Με το FTP ο pacman πρέπει να στείλει ένα σήμα κάθε φορά που κατεβάζει ένα πακέτο, αυτό έχει ως αποτέλεσμα μια σύντομη παύση. Για άλλους τρόπους δημιουργίας μιας λίστας mirror δείτε στα [Sorting mirrors](/index.php/Mirrors#Sorting_mirrors "Mirrors") και [Reflector](/index.php/Reflector "Reflector").
*   Στο [Arch Linux MirrorStatus](https://archlinux.org/mirrors/status/) μπορείτε να δείτε αναφορές για διάφορα θέματα που αφορούν τα mirrors, όπως προβλήματα δικτύου, προβλήματα συλλογής δεδομένων καθώς και την τελευταία ώρα που συγχρονισμού των mirrors.

**Σημείωση:**

*   Όποτε στο μέλλον θελήσετε να αλλάξετε την λίστα με τα mirrors σας, να θυμάστε να επιβάλετε στον pacman να ανανεώσει όλες τις λίστες πακέτων με την `pacman -Syy`. Αυτή θεωρείται καλή πρακτική και θα σας γλιτώσει από πιθανούς «πονοκεφάλους». Δείτε στο [Mirrors](/index.php/Mirrors "Mirrors") για περισσότερες πληροφορίες.
*   Αν χρησιμοποιείστε ένα παλιό μέσον εγκατάστασης, τότε η mirrorlist πιθανών να είναι παρωχημένη, το οποίο θα οδηγήσει σε προβλήματα όταν κάνετε ενημέρωση το Arch Linux (δείτε το [FS#22510](https://bugs.archlinux.org/task/22510)). Γι' αυτό τον λόγο είναι καλό να εξασφαλίσετε την τελευταία διαθέσιμη λίστα mirror, όπως αναφέρθηκε παραπάνω.
*   Κάποια προβλήματα έχουν αναφερθεί στα [Arch Linux forums](https://bbs.archlinux.org/) σχετικά με προβλήματα δικτύου που εμποδίζουν τον pacman από το να ενημερώσει/συγχρονίσει τα αποθετήρια (δείτε [[1]](https://bbs.archlinux.org/viewtopic.php?id=68944) και [[2]](https://bbs.archlinux.org/viewtopic.php?id=65728)). Όταν εγκαθιστάτε το Arch Linux στον υπολογιστή σας αυτά τα προβλήματα μπορούν να επιλυθούν αντικαθιστώντας τον προεπιλεγμένο file downloader του pacman με έναν εναλλακτικό (δείτε το [Improve pacman performance](/index.php/Improve_pacman_performance "Improve pacman performance") για περισσότερες λεπτομέρειες). Όταν εγκαθιστάτε το Arch Linux ως φιλοξενούμενο Λ.Σ σε [VirtualBox](/index.php/VirtualBox_(%CE%95%CE%BB%CE%BB%CE%B7%CE%BD%CE%B9%CE%BA%CE%AC) "VirtualBox (Ελληνικά)"), αυτό το θέμα μπορεί επίσης να επιλυθεί χρησιμοποιώντας "Host interface" αντί για "NAT" στις ρυθμίσεις της εικονικής μηχανής.

### Εγκαταστήστε το βασικό σύστημα

Το βασικό σύστημα εγκαθίσταται χρησιμοποιώντας το script [pacstrap](https://github.com/falconindy/arch-install-scripts/blob/master/pacstrap.in).

Ο διακόπτης (επιλογή) `-i` μπορεί να χρησιμοποιηθεί εάν επιθυμείτε να εγκαταστήσετε όλα τα πακέτα από το group *base* χωρίς να ερωτηθείτε.

```
# pacstrap -i /mnt base

```

**Σημείωση:**

*   Εάν ο pacman αποτύχει να ταυτοποιήσει τα πακέτα, ελένξτε την ώρα του συστήματος με το `cal`. Εάν η ημερομηνία του συστήματος δεν είναι έγκυρη (για παράδειγμα λέει ότι το έτος είναι το 2010), τα κλειδιά των υπογραφών θα θεωρηθούν ληγμένα (ή μη έγκυρα), ο έλεγχος των υπογραφών στα πακέτα θα αποτύχει και η εγκατάσταση θα διακοπεί. Βεβαιωθείτε ότι έχετε βάλει έγκυρη ώρα συστήματος, είτε χειροκίνητα είτε μέσω του client [ntp](https://www.archlinux.org/packages/?name=ntp), και τρέξτε ξανά την εντολή pacstrap. Δείτε την σελίδα [Time](/index.php/Time "Time") για περισσότερες πληροφορίες σχετικά με την διόρθωση της ώρας συστήματος.
*   Εάν ο pacman παραπονεθεί με το μήνυμα `error: failed to commit transaction (invalid or corrupted package)`, τρέξτε την ακόλουθη εντολή:

```
# pacman-key --init && pacman-key --populate archlinux

```

Έτσι θά 'χετε ένα βασικό σύστημα Arch. Πρόσθετα πακέτα μπορούν να εγκατασταθούν αργότερα κάνοντας χρήση του [pacman](/index.php/Pacman_(%CE%95%CE%BB%CE%BB%CE%B7%CE%BD%CE%B9%CE%BA%CE%AC) "Pacman (Ελληνικά)").

### Δημιουργία του fstab

Δημιουργείστε ένα αρχείο [fstab](/index.php/Fstab "Fstab") με την παρακάτω εντολή. Θα χρησιμοποιηθούν UUIDs, διότι έχουν συγκεκριμένα πλεονεκτήματα (δείτε στο [fstab#Identifying filesystems](/index.php/Fstab#Identifying_filesystems "Fstab")). Αν θέλετε να χρησιμοποιήσετε labels , τότε αντικαταστήστε την επιλογή `-U` με την `-L`.

```
# genfstab -U -p /mnt >> /mnt/etc/fstab
# nano /mnt/etc/fstab

```

**Προσοχή:** Το αρχείο fstab πρέπει πάντα να ελέγχεται αφού δημιουργηθεί. Αν αντιμετωπίσετε προβλήματα τρέχοντας την genfstab ή αργότερα κατά την διάρκεια της εγκατάστασης, **μην** τρέξετε ξανά την εντολή genfstab. Απλά επεξεργαστείτε το αρχείο fstab.

Μερικές θεωρήσεις:

*   Το τελευταίο πεδίο καθορίζει την σειρά με την οποία ελέγχονται οι κατατμήσεις κατά τη διάρκεια της εκκίνησης: Χρησιμοποιείστε το `1` για τις (μη-`btrfs`) κατατμήσεις, που πρέπει να ελεγχθούν πρώτες. Το `2` για όλες τις υπόλοιπες κατατμήσεις που θέλετε να ελεγχθούν κατά τη διάρκεια της εκκίνησης. Το `0` σημαίνει 'μην κάνεις έλεγχο' (δείτε στο [fstab#Field definitions](/index.php/Fstab#Field_definitions "Fstab")).
*   Όλες οι [btrfs](/index.php/Btrfs "Btrfs") κατατμήσεις πρέπει να έχουν `0` σε αυτό το πεδίο. Επίσης θέλετε και η κατάτμηση *swap* να έχει `0`.

### Κάντε chroot και ρυθμίστε το βασικό σύστημα

**Σημείωση:** Αν σχεδιάζετε να κάνετε επανεκκίνηση σε UEFI mode, διαβάστε το [#Για μητρικές με UEFI](#.CE.93.CE.B9.CE.B1_.CE.BC.CE.B7.CF.84.CF.81.CE.B9.CE.BA.CE.AD.CF.82_.CE.BC.CE.B5_UEFI), καθώς υπάρχουν κάποια πράγματα που πρέπει να κάνετε **πριν** μπείτε σε chroot. Αυτό είναι απαραίτητο για να σιγουρέψετε ότι ο boot loader ή manager μπορεί να ρυθμιστεί σωστά μέσα στο περιβάλλον chroot.

Μετά, κάνουμε [chroot](/index.php/Chroot "Chroot") στο νέο εγκατεστημένο σύστημα:

```
# arch-chroot /mnt

```

**Σημείωση:** Χρησιμοποιείστε την `arch-chroot /mnt /bin/bash` για να κάνετε chroot σε ένα bash shell.

Σε αυτό το στάδιο της εγκατάστασης θα ρυθμίσετε τα κύρια αρχεία ρυθμίσεων του βασικού συστήματος Arch Linux. Αυτά μπορούν είτε να δημιουργηθούν αν δεν υπάρχουν, ή να τα επεξεργαστείτε (αν θέλετε) αλλάζοντας τα προεπιλεγμένα.

Το να παρακολουθήσετε και να καταλάβετε αυτά τα βήματα, είναι σημαντικό για να ρυθμίσετε σωστά το σύστημα.

#### Locale (τοπική ρύθμιση)

Οι τοπικές ρυθμίσεις (locales) χρησιμοποιούνται από την **glibc** και άλλα προγράμματα ή βιβλιοθήκες για να αποδίδουν κείμενα, όπως και να δείχνουν σωστά περιφερειακές νομισματικές αξίες, την ώρα και ημερομηνία και άλλα τοπικά-ειδικά πρότυπα.

Υπάρχουν δυο αρχεία που χρειάζονται επεξεργασία: `locale.gen` και `locale.conf`.

*   Το αρχείο `locale.gen` είναι άδειο από προεπιλογή (τα πάντα είναι σχόλια) και χρειάζεται να αφαιρέσετε την δίεση `#` μπροστά από κάποια γραμμή(ή γραμμές) που θέλετε. Μπορείτε να αποσχολιάσετε περισσότερες γραμμές εκτός του English (US), αρκεί να επιλέξετε την κωδικοποίηση `UTF-8`:

 `# nano /etc/locale.gen` 
```
en_US.UTF-8 UTF-8
el_GR.UTF-8 UTF-8

```

```
# locale-gen

```

Αυτό θα τρέξει σε κάθε αναβάθμιση της **glibc** , παράγοντας όλα τα locales που υπάρχουν στο `/etc/locale.gen`.

*   Το αρχείο `locale.conf` δεν υπάρχει από προεπιλογή. Το να θέσετε μόνο την παράμετρο `LANG`, πρέπει να είναι αρκετό. Θα ενεργήσει ως η προεπιλεγμένη παράμετρος για όλες τις υπόλοιπες. Φυσικά προσαρμόστε τις παρακάτω εντολές αναλόγως με το δικό σας locale, π.χ `el_GR.UTF-8`. Το locale που υπάρχει στην παράμετρο `LANG` πρέπει να είναι αποσχολιασμένο στο αρχείο `/etc/locale.gen`.

```
# echo LANG=en_US.UTF-8 > /etc/locale.conf
# export LANG=en_US.UTF-8

```

Για να χρησιμοποιήσετε άλλες παραμέτρους τοπικών ρυθμίσεων(locales) `LC_*`, τρέξτε `locale` για να δείτε τις διαθέσιμες επιλογές και προσθέστε τις στο `locale.conf`. Δεν συνίσταται να θέτετε την παράμετρο `LC_ALL`. Δείτε στο [Locale#Setting system-wide locale](/index.php/Locale#Setting_system-wide_locale "Locale") για λεπτομέρειες.

#### Γραμματοσειρά κονσόλας και διάταξη πληκτρολογίου

Αν θέσατε κάποια διάταξη πληκτρολογίου [στην αρχή](#.CE.91.CE.BB.CE.BB.CE.B1.CE.B3.CE.AE_.CE.B3.CE.BB.CF.8E.CF.83.CF.83.CE.B1.CF.82) της εγκατάστασης, φορτώστε την ξανά τώρα διότι το περιβάλλον έχει αλλάξει. Για παράδειγμα:

```
# loadkeys *de-latin1*
# setfont Lat2-Terminus16

```

Για να τις κάνετε διαθέσιμες μετά την επανεκκίνηση, επεξεργαστείτε το `vconsole.conf` (δημιουργήστε το αν δεν υπάρχει):

 `# nano /etc/vconsole.conf` 
```
KEYMAP=de-latin1
FONT=Lat2-Terminus16
```

*   `KEYMAP` – Λάβετε υπόψιν σας πως αυτή η ρύθμιση είναι σωστή μόνον για τα TTYs και όχι για κάποιο γραφικό διαχειριστή παραθύρων ή τον Xorg.

*   `FONT` – Εναλλακτικά διαθέσιμες γραμματοσειρές βρίσκονται στο `/usr/share/kbd/consolefonts/`. Το προεπιλεγμένο (κενό) είναι ασφαλές, αλλά ορισμένοι ξένοι χαρακτήρες ίσως εμφανίζονται ως άσπρα τετράγωνα ή άλλα σύμβολα. Προτείνεται να το αλλάξετε σε `Lat2-Terminus16`, διότι σύμφωνα με το `/usr/share/kbd/consolefonts/README.Lat2-Terminus16`, ισχυρίζεται πως υποστηρίζει "περίπου 110 γλωσσικά σετ".

*   Πιθανές επιλογές `FONT_MAP` – Καθορίζει τον χάρτη της κονσόλας που θα φορτωθεί στην εκκίνηση. Διαβάστε το `man setfont`. Είτε το διαγράψετε, είτε το αφήσετε κενό, είναι ασφαλές.

Δείτε το [Fonts#Console fonts](/index.php/Fonts#Console_fonts "Fonts") και το `man vconsole.conf` για περισσότερες πληροφορίες.

#### Ζώνη ώρας

Οι διαθέσιμες ζώνες (και υποζώνες) ώρας μπορούν να βρεθούν στους καταλόγους `/usr/share/zoneinfo/<Zone>/<SubZone>`.

Για να δείτε τις διαθέσιμες ζώνες (<Zone>), ελέγξτε τον κατάλογο `/usr/share/zoneinfo/`:

```
# ls /usr/share/zoneinfo/

```

Παρομοίως, μπορείτε να ελέγξετε τα περιεχόμενα των καταλόγων που ανήκουν σε μια υποζώνη <SubZone>:

```
# ls /usr/share/zoneinfo/Europe

```

Δημιουργείστε έναν συμβολικό σύνδεσμο `/etc/localtime` στο αρχείο ζώνης σας `/usr/share/zoneinfo/<Zone>/<SubZone>` χρησιμοποιώντας αυτή την εντολή:

```
# ln -s /usr/share/zoneinfo/<Zone>/<SubZone> /etc/localtime

```

**Παράδειγμα:**

```
# ln -s /usr/share/zoneinfo/Europe/Athens /etc/localtime

```

#### Hardware clock (ρολόι υπολογιστή)

Θέστε το ρολόι του υπολογιστή ομοιόμορφα μεταξύ των λειτουργικών συστημάτων. Διαφορετικά, ίσως αντικαταστήσουν το ρολόι του υπολογιστή και προκαλέσουν χρονικές μετατοπίσεις.

Μπορείτε να δημιουργήσετε το `/etc/adjtime` αυτόματα, χρησιμοποιώντας τις παρακάτω εντολές:

*   **UTC** (προτείνεται)

**Σημείωση:** Χρησιμοποιώντας το [UTC](https://en.wikipedia.org/wiki/Coordinated_Universal_Time "wikipedia:Coordinated Universal Time") για το ρολόι του υπολογιστή δεν σημαίνει πως το λογισμικό θα δείχνει την ώρα σε UTC.

	 `# hwclock --systohc --utc` 

Για να συγχρονίσετε την "UTC" ώρα σας μέσω του διαδικτύου, δείτε το [NTPd](/index.php/Network_Time_Protocol_daemon "Network Time Protocol daemon").

*   **localtime** (δεν προτείνεται, χρησιμοποιείτε από προεπιλογή στα Windows)

**Προσοχή:** Χρησιμοποιώντας το *localtime* μπορεί να οδηγήσει σε γνωστά σφάλματα. Ωστόσο δεν υπάρχουν σχέδια για να σταματήσει η υποστήριξη του *localtime*.

	 `# hwclock --systohc --localtime` 

Αν έχετε (ή σχεδιάζετε να έχετε) διπλή εκκίνηση με Windows:

*   Συνιστώμενο: Θέστε και τα δύο λειτουργικά (Arch Linux & Windows) να χρησιμοποιούν UTC. Ένα σύντομο [registry fix](/index.php/Time#UTC_in_Windows "Time") χρειάζεται. Επίσης

βεβαιωθείτε πως τα Windows δεν συγχρονίζουν την ώρα με το διαδίκτυο, διότι το ρολόι του υπολογιστή θα τεθεί πίσω στο *localtime*.

*   Δεν συνίσταται: Θέστε το Arch Linux στο *localtime* και απενεργοποιήστε οποιαδήποτε υπηρεσία σχετική με την ώρα, όπως το [NTPd](/index.php/Network_Time_Protocol_daemon "Network Time Protocol daemon"). Αυτό θα αφήσει τα Windows να έχουν τον έλεγχο του ρολογιού του υπολογιστή και πρέπει να θυμάστε αν κάνετε εκκίνηση σε Windows τουλάχιστον δυο φορές τον χρόνο (Άνοιξη και Φθινόπωρο) όταν αλλάζει η ώρα. Σας παρακαλούμε να μην ρωτήστε στα forums γιατί το ρολόι είναι μια ώρα μπροστά ή πίσω αν έχετε να κάνετε μέρες ή και βδομάδες εκκίνηση σε Windows.

#### Kernel modules (αρθρώματα του πυρήνα)

**Συμβουλή:** Αυτό είναι απλά ένα παράδειγμα, δεν χρειάζεται να θέστε κάτι τέτοιο. Όλα τα αρθρώματα που χρειάζονται φορτώνονται αυτόματα από το udev, οπότε σπάνια θα χρειαστεί να προσθέσετε κάτι. Προσθέστε αρθρώματα μόνον όταν ξέρετε ότι λείπουν.

Για αρθρώματα του πυρήνα που χρειάζεται να φορτωθούν κατά την εκκίνηση, δημιουργείστε ένα αρχείο με κατάληξη `*.conf`, μέσα στο `/etc/modules-load.d/`, με το όνομά του να βασίζεται στο πρόγραμμα που το χρησιμοποιεί.

 `# nano /etc/modules-load.d/virtio-net.conf` 
```
# Load 'virtio-net.ko' at boot.

virtio-net
```

Αν υπάρχουν περισσότερα αρθρώματα για κάθε `*.conf`, τα ονόματα τους μπορούν να διαχωριστούν από νέες γραμμές. Ένα καλό παράδειγμα είναι τα [VirtualBox Guest Additions](/index.php/VirtualBox_(%CE%95%CE%BB%CE%BB%CE%B7%CE%BD%CE%B9%CE%BA%CE%AC)#.CE.95.CE.B3.CE.BA.CE.B1.CF.84.CE.AC.CF.83.CF.84.CE.B1.CF.83.CE.B7_.CF.84.CF.89.CE.BD_Guest_Additions "VirtualBox (Ελληνικά)").

Οι άδειες γραμμές και οι γραμμές που ξεκινούν με `#` ή `;`, δεν λαμβάνονται υπόψιν.

#### Hostname (όνομα συστήματος)

Θέστε το [hostname](https://en.wikipedia.org/wiki/hostname "wikipedia:hostname") αναλόγως με το τι σας αρέσει (π.χ. *arch*):

```
# echo *myhostname* > /etc/hostname

```

**Σημείωση:** Δεν χρειάζεται να επεξεργαστείτε το `/etc/hosts`.

### Ρυθμίστε το δίκτυο

Χρειάζεται να ρυθμίσετε πάλι το δίκτυο, αλλά αυτή τη φορά για το φρεσκοεγκατεστημένο σύστημα. Η διαδικασία και οι απαιτούμενες ενέργειες είναι αρκετά παρόμοιες με αυτές που περιγράφονται [πιο πάνω](#Establish_an_internet_connection_.28.CE.95.CE.BB.CE.BB.CE.B7.CE.BD.CE.B9.CE.BA.CE.AC.29), εκτός απ' ότι θα τις κάνουμε μόνιμες και να τρέχουν αυτόματα κατά την εκκίνηση.

**Σημείωση:**

*   Για μεγαλύτερη ανάλυση εις βάθος σχετικά με τη ρύθμιση δικτύου, δείτε τις παραγράφους [Configuring Network](/index.php/Configuring_Network_(%CE%95%CE%BB%CE%BB%CE%B7%CE%BD%CE%B9%CE%BA%CE%AC) "Configuring Network (Ελληνικά)") και [Wireless Setup](/index.php/Wireless_Setup_(%CE%95%CE%BB%CE%BB%CE%B7%CE%BD%CE%B9%CE%BA%CE%AC) "Wireless Setup (Ελληνικά)").
*   Εάν επιθυμείτε να χρησιμοποιείτε την παλιά μέθοδο ονοματολογίας (για παράδειγμα eth* και wlan*) μπορείτε να το πετύχετε δημιουργώντας ένα κενό αρχείο `/etc/udev/rules.d/80-net-name-slot.rules` το οποίο θα «κρύψει» το αρχείο ίδιου ονόματος που βρίσκεται στο `/usr/lib/udev/rules.d` (εναλλακτικά, αντί για ένα κενό αρχείο, μία άλλη αποδεκτή μέθοδος «κρυψίματος» είναι να δημιουργήσετε μια συντόμευση προς το `/dev/null`).

#### Ενσύρματη σύνδεση

##### Δυναμική IP

	Χρησιμοποιώντας το dhcpcd

Εάν χρησιμοποιείτε μόνο μία οριστική ενσύρματη σύνδεση για το δίκτυο, δεν χρειάζεστε κάποια υπηρεσία (service) διαχείρισης δικτύου και μπορείτε απλά να ενεργοποιήσετε την υπηρεσία `dhcpcd`:

```
# systemctl enable dhcpcd.service

```

**Σημείωση:** Εάν δεν δουλέψει, χρησιμοποιείστε την εντολή: `# systemctl enable dhcpcd@*όνομα_του_interface*.service`

	Χρησιμοποιώντας το netctl

Αντιγράψτε ένα προφίλ-δείγμα από το `/etc/netctl/examples` στο `/etc/netctl`:

```
# cd /etc/netctl
# cp examples/ethernet-dhcp το_δίκτυο_μου

```

Τροποποιήστε το προφίλ όπως είναι αναγκαίο (ενημερώστε το `Interface` ώστε αντί του `eth0` να δείχνει το ID του αντάπτορα όπως φαίνεται από το τρέξιμο της εντολής `ip link`):

```
# nano το_δίκτυο_μου

```

Ενεργοποιείστε το προφίλ `το_δίκτυο_μου`:

```
# netctl enable το_δίκτυο_μου

```

	Χρησιμοποιώντας το netctl-ifplugd

**Προσοχή:** Δεν μπορείτε να χρησιμοποιήσετε αυτή τη μέθοδο σε συνδυασμό με μια σαφή ενεργοποίηση των προφίλ, όπως γίνεται στην περίπτωση της εντολής `netctl enable <profile>`.

Εναλλακτικά, μπορείτε να χρησιμοποιήσετε το `netctl-ifplugd`, το οποίο διαχειρίζεται υποδειγματικά δυναμικές συνδέσεις σε καινούργια δίκτυα:

Εγκαταστήστε το [ifplugd](https://www.archlinux.org/packages/?name=ifplugd), που απαιτείται από το `netctl-ifplugd`:

```
# pacman -S ifplugd

```

Κατόπιν ενεργοποιήστε το για το interface που θέλετε:

```
# systemctl enable netctl-ifplugd@<interface>.service

```

**Συμβουλή:** Το [Netctl](/index.php/Netctl "Netctl") παρέχει επίσης το `netctl-auto`, το οποίο μπορεί να χρησιμοποιηθεί για το χειρισμό ενσύρματων προφίλ σε συνδυασμό με το `netctl-ifplugd`.

##### Στατική IP

	Χρησιμοποιώντας το netctl

Αντιγράψτε ένα προφίλ-δείγμα από το `/etc/netctl/examples` στο `/etc/netctl`:

```
# cd /etc/netctl
# cp examples/ethernet-static το_δίκτυο_μου

```

Τροποποιήστε το προφίλ όπως είναι αναγκαίο (αλλάξτε τα `Interface`, `Address`, `Gateway` και `DNS`):

```
# nano το_δίκτυο_μου

```

*   Παρατηρείστε τον αριθμό `/24` στην `Address` ο οποίος είναι η [ένδειξη του CIDR](https://en.wikipedia.org/wiki/Classless_Inter-Domain_Routing#CIDR_notation "wikipedia:Classless Inter-Domain Routing") μιας μάσκας υποδικτύου `255.255.255.0`

Ενεργοποιήστε το προφίλ που δημιουργήσατε παραπάνω, ώστε να ξεκινάει σε κάθε εκκίνηση:

```
# netctl enable το_δίκτυο_μου

```

#### Ασύρματη σύνδεση

**Σημείωση:** Εάν ο αντάπτορας της ασύρματης σύνδεσης σας απαιτεί κάποιο firmware (όπως αναλύεται στις παραπάνω παραγράφους [Δημιουργία σύνδεσης με το διαδίκτυο](#Wireless_.28.CE.95.CE.BB.CE.BB.CE.B7.CE.BD.CE.B9.CE.BA.CE.AC.29) και επίσης [εδώ](/index.php/Wireless_network_configuration#Device_driver_.28.CE.95.CE.BB.CE.BB.CE.B7.CE.BD.CE.B9.CE.BA.CE.AC.29 "Wireless network configuration")), εγκαταστήστε το πακέτο που περιέχει το απαιτούμενο firmware. Τις περισσότερες φορές, το πακέτο [linux-firmware](https://www.archlinux.org/packages/?name=linux-firmware) θα περιέχει ήδη το απαιτούμενο firmware. Αν και για κάποιες συσκευές, το απαιτούμενο firmware μπορεί να περιέχεται στο δικό του πακέτο. Για παράδειγμα: `# pacman -S zd1211-firmware` Δείτε το [Wireless network configuration#Installing driver/firmware (Ελληνικά)](/index.php/Wireless_network_configuration#Installing_driver.2Ffirmware_.28.CE.95.CE.BB.CE.BB.CE.B7.CE.BD.CE.B9.CE.BA.CE.AC.29 "Wireless network configuration") για περισσότερες πληροφορίες.

Εγκαταστήστε τα πακέτα [iw](https://www.archlinux.org/packages/?name=iw) και [wpa_supplicant](https://www.archlinux.org/packages/?name=wpa_supplicant) που θα χρειαστείτε για να συνδεθείτε σε κάποιο δίκτυο:

```
# pacman -S iw wpa_supplicant

```

##### Προσθήκη ασύρματων δικτύων

	Χρησιμοποιώντας το wifi-menu

Εγκαταστήστε το πακέτο [dialog](https://www.archlinux.org/packages/?name=dialog), που απαιτείται από το `wifi-menu`:

```
# pacman -S dialog

```

Μετά το τέλος αυτής της εγκατάστασης και μετά από επανεκκίνηση, μπορείτε να συνδεθείτε στο δίκτυο με χρήση της εντολής `wifi-menu *όνομα_του_interface*` (όπου `*όνομα_του_interface*` είναι το interface του ασύρματου chipset της συσκευής).

```
# wifi-menu *όνομα_του_interface*

```

**Προσοχή:** Αυτό πρέπει να γίνει *μετά* την επανεκκίνηση όταν θά 'χετε τελειώσει με το chroot. Η διεργασία που θα προκύψει από αυτήν την εντολή θα έρθει σε σύγκρουση με την εντολή που τρέχετε έξω από το περιβάλλον chroot. Εναλλακτικά, θα μπορούσατε να ρυθμίσετε χειροκίνητα κάποιο προφίλ δικτύου χρησιμοποιώντας τα ακόλουθα templates ούτως ώστε να μην ανησυχείτε καθόλου για την χρήση του `wifi-menu`.

Χρησιμοποιώντας αυτοσχέδια προφίλ του netctl

Αντιγράψτε κάποιο προφίλ δικτύου από το `/etc/netctl/examples` στο `/etc/netctl`:

```
# cd /etc/netctl
# cp examples/wireless-wpa το-δίκτυο-μου

```

Τροποποιήστε το προφίλ όπως είναι αναγκαίο (αλλάξτε τα `Interface`, `ESSID` και `Key`):

```
# nano το-δίκτυο-μου

```

Ενεργοποιήστε το προφίλ που δημιουργήσατε πιο πάνω ούτως ώστε να ξεκινάει σε κάθε εκκίνηση:

```
# netctl enable το-δίκτυο-μου

```

##### Αυτόματη σύνδεση σε γνωστά δίκτυα

**Προσοχή:** Δεν μπορείτε να χρησιμοποιήσετε αυτήν την μέθοδο σε συνδυασμό με μια σαφή ενεργοποίηση των προφίλ, όπως γίνεται στην περίπτωση της εντολής `netctl enable <profile>`.

Εγκαταστήστε το πακέτο [wpa_actiond](https://www.archlinux.org/packages/?name=wpa_actiond), που απαιτείται από το `netctl-auto`:

```
# pacman -S wpa_actiond

```

Ενεργοποιήστε την υπηρεσία `netctl-auto`, το οποίο θα συνδεθεί σε γνωστά δίκτυα και υποδειγματικά θα διαχειριστεί την περιαγωγή και τις αποσυνδέσεις:

```
# systemctl enable netctl-auto@*όνομα_του_interface*.service

```

**Συμβουλή:** Το [Netctl](/index.php/Netctl "Netctl") παρέχει επίσης το `netctl-ifplugd`, το οποίο μπορεί να χρησιμοποιηθεί για τη διαχείριση ενσύρματων προφίλ σε συνδυασμό με το `netctl-auto`.

#### Αναλογικό modem, ISDN ή PPPoE DSL

Για συνδέσεις xDSL, dial-up και ISDN, βλέπε [Direct Modem Connection](/index.php/Direct_Modem_Connection "Direct Modem Connection").

### Δημιουργείστε ένα αρχικό περιβάλλον ramdisk

**Συμβουλή:** Οι περισσότεροι χρήστες μπορούν να παραλείψουν αυτό το βήμα και να χρησιμοποιήσουν τις προεπιλεγμένες ρυθμίσεις στο `mkinitcpio.conf`. Η εικόνα initramfs (από τον φάκελο `/boot`) έχει ήδη δημιουργηθεί όταν εγκαταστήσαμε νωρίτερα το πακέτο [linux](https://www.archlinux.org/packages/?name=linux) (πυρήνας Linux) με την `pacstrap`.

Εδώ χρειάζεται να θέσετε τα σωστά [hooks](/index.php/Mkinitcpio#HOOKS "Mkinitcpio") αν το σύστημα root βρίσκεται σε ένα USB δίσκο, αν χρησιμοποιείτε RAID, LVM ή αν το `/usr` βρίσκεται σε ξεχωριστή κατάτμηση.

Επεξεργαστείτε το `/etc/mkinitcpio.conf` αναλόγως και αναδημιουργείστε την εικόνα initramfs με:

```
# mkinitcpio -p linux

```

**Σημείωση:** Οι εγκαταστάσεις του Arch σε VPS στο QEMU (π.χ όταν χρησιμοποιείται ο `virt-manager`) ίσως να χρειαστούν τα αρθρώματα `virtio` μέσα στο `mkinitcpio.conf` για να εκκινήσουν σωστά.
 `# nano /etc/mkinitcpio.conf`  `MODULES="virtio virtio_blk virtio_pci virtio_net"` 

### Θέστε τον κωδικό του root

*Ως root αναφερόμαστε στον υπέρ-χρήστη που έχει πλήρη δικαιώματα στο Arch Linux.*

Θέστε τον κωδικό του root με:

```
# passwd

```

### Εγκαταστήστε και ρυθμίστε τον bootloader

#### Για μητρικές με BIOS

Για μητρικές με BIOS, διάφοροι boot loaders είναι διαθέσιμοι, δείτε στο [Boot Loaders](/index.php/Boot_Loaders "Boot Loaders") για μια πλήρη λίστα. Διαλέξτε έναν που σας ταιριάζει. Εδώ θα δώσουμε δυο πιθανά παραδείγματα:

*   Ο Syslinux μπορεί (για τώρα) να φορτώσει αρχεία από κατατμήσεις στις οποίες έχει εγκατασταθεί. Το αρχείο επεξεργασίας του θεωρείται ευκολότερο στο να το καταλάβετε. Ένα παράδειγμα επεξεργασία μπορείτε να δείτε [εδώ](https://bbs.archlinux.org/viewtopic.php?pid=1109328#p1109328).

*   Ο GRUB είναι πλούσιος σε χαρακτηριστικά και υποστηρίζει πολυπλοκότερα σενάρια. Τα αρχεία επεξεργασίας του είναι παρόμοια με την 'sh' γλώσσα προγραμματισμού και γι' αυτό μπορεί να φανούν δύσκολα στους αρχάριους χρήστες που θέλουν να τα επεξεργαστούν. Προτείνεται να δημιουργούν τα αρχεία αυτά, αυτόματα.

##### Syslinux

**Σημείωση:** Αν δημιουργήσατε ένα GUID πίνακα κατατμήσεων (GPT) για τον δίσκο σας νωρίτερα, χρειάζεται να εγκαταστήστε το πακέτο [gptfdisk](https://www.archlinux.org/packages/?name=gptfdisk) τώρα, για να δουλέψει το επόμενο βήμα. Υποθέτοντας βέβαια πως δεν το έχετε εγκαταστήσει ήδη.

Εγκαταστήστε το πακέτο [syslinux](https://www.archlinux.org/packages/?name=syslinux) και μετά χρησιμοποιείστε το `syslinux-install_update` script για να *εγκαταστήσετε* αυτόματα τον bootloader (`-i`), σημειώστε την κατάτμηση ως *ενεργή(active)* θέτοντας την σημαία εκκίνησης (`-a`), και εγκαταστήστε τον κώδικα εκκίνησης MBR (`-m`):

```
# pacman -S syslinux
# syslinux-install_update -i -a -m

```

Επεξεργαστείτε το `syslinux.cfg` έτσι ώστε να δείχνει στη σωστή root κατάτμηση. Αυτό το βήμα είναι πολύ σημαντικό. Αν δείχνει σε λάθος κατάτμηση, το Arch Linux δεν θα εκκινεί. Αλλάξτε το `/dev/sda3` έτσι ώστε να αντικατοπτρίζει τη δική σας root κατάτμηση. *(αν διαμερίσατε τον δίσκο όπως στο [παράδειγμα](#.CE.A0.CF.81.CE.BF.CE.B5.CF.84.CE.BF.CE.B9.CE.BC.CE.B1.CF.83.CE.AF.CE.B1_.CF.84.CE.BF.CF.85_.CE.BC.CE.AD.CF.83.CE.BF.CF.85_.CE.B1.CF.80.CE.BF.CE.B8.CE.AE.CE.BA.CE.B5.CF.85.CF.83.CE.B7.CF.82), τότε η root κατάτμησή σας είναι η `/dev/sda1`)*. Κάντε το ίδιο για την εισαγωγή fallback.

 `# nano /boot/syslinux/syslinux.cfg` 
```
...
LABEL arch
        ...
        APPEND root=**/dev/sda3** rw
        ...
```

Για περισσότερες πληροφορίες σε ότι αφορά την επεξεργασία και την χρήση του Syslinux, δείτε στο [Syslinux](/index.php/Syslinux "Syslinux").

##### GRUB

Εγκαταστήστε το πακέτο [grub](https://www.archlinux.org/packages/?name=grub) και μετά τρέξτε `grub-install` για να εγκαταστήσετε τον bootloader:

**Σημείωση:**

*   Αλλάξτε το `/dev/sda` έτσι ώστε να αντικατοπτρίζει τον δίσκο όπου έχετε εγκαταστήσει το Arch. Μην προσθέσετε αριθμό κατάτμησης (μην χρησιμοποιείσετε `sda*X*`).
*   Για δίσκους που έχουν διαμεριστεί με GPT σε μητρικές με BIOS, θα χρειαστείτε επίσης ένα "BIOS Boot Partition". Δείτε στο [GPT-specific instructions](/index.php/GRUB#GUID_Partition_Table_.28GPT.29_specific_instructions "GRUB") στην σελίδα του GRUB.

```
# pacman -S grub
# grub-install --target=i386-pc --recheck **/dev/sda**

```

Αν και το να χρησιμοποιήσετε ένα χειροκίνητα δημιουργημένο `grub.cfg` είναι εντάξει, ωστόσο για τους αρχάριους συνίσταται να δημιουργήσουν ένα, αυτόματα:

**Συμβουλή:** Για να γίνει σάρωση αυτόματα, για άλλα λειτουργικά συστήματα στον υπολογιστή σας, εγκαταστήστε το [os-prober](https://www.archlinux.org/packages/?name=os-prober) (`pacman -S os-prober`), πριν τρέξετε την εντολή.

```
# grub-mkconfig -o /boot/grub/grub.cfg

```

Για περισσότερες πληροφορίες σχετικά με την επεξεργασία και χρήστη του GRUB, δείτε στο [GRUB](/index.php/GRUB "GRUB").

#### Για μητρικές με UEFI

Για συστήματα με UEFI, διάφοροι boot loaders είναι διαθέσιμοι, δείτε στο [Boot Loaders](/index.php/Boot_Loaders "Boot Loaders") για μια πλήρη λίστα. Διαλέξετε έναν, ο όποιος σας διευκολύνει. Εδώ, δίνουμε δυο πιθανούς, ως παράδειγμα:

*   Ο [gummiboot](/index.php/Gummiboot "Gummiboot") είναι ένας μινιμαλιστικός UEFI boot Manager που βασικά παρέχει ένα μενού για [EFISTUB](/index.php/EFISTUB "EFISTUB") πυρήνες και άλλες UEFI εφαρμογές.

Αυτή είναι μια προτεινόμενη μέθοδος εκκίνησης UEFI.

*   Ο GRUB είναι ένας πιο ολοκληρωμένος bootloader, χρήσιμος αν αντιμετωπίσετε προβλήματα με τον Gummiboot.

**Σημείωση:** Για μια εκκίνηση σε UEFI, ο δίσκος πρέπει να έχει διαμεριστεί με GPT και μία κατάτμηση [EFI](/index.php/Unified_Extensible_Firmware_Interface#EFI_System_Partition "Unified Extensible Firmware Interface") (512ΜΒ ή μεγαλύτερη, με τύπο gdisk `EF00` και διαμορφωμένη σε FAT32) πρέπει να υπάρχει. Στα παρακάτω παραδείγματα αυτή η κατάτμηση υποτίθεται πως είναι προσαρτημένη στο `/boot`. Αν ακολουθήσατε αυτόν τον οδηγό από την αρχή, όλα αυτά τα έχετε ήδη κάνει.

##### Gummiboot

Πρώτα εγκαταστήστε το πακέτο [gummiboot](https://www.archlinux.org/packages/?name=gummiboot) και μετά τρέξτε `gummiboot install` για να εγκαταστήσετε τον bootloader στην EFI κατάτμηση του συστήματος:

**Σημείωση:** Όλες οι εντολές θα πρέπει να εκτελεστούν ΜΕΣΑ στο περιβάλλον chroot, αν υπάρχει.

```
# mount -t efivarfs efivarfs /sys/firmware/efi/efivars              # αγνοείστε το αν είναι ήδη προσαρτημένη
# pacman -S gummiboot
# gummiboot install

```

Θα χρειαστεί να δημιουργήσετε χειροκίνητα ένα αρχείο ρυθμίσεων για να προσθέσετε μια εισαγωγή για το Arch Linux στον gumiboot manager. Δημιουργείστε το `/boot/loader/entries/arch.conf` και προσθέσετε τα παρακάτω περιεχόμενα, αντικαθιστώντας το `/dev/sdaX` με την κυρίως κατάρτηση root, συνήθως είναι το `/dev/sda2`:

 `# nano /boot/loader/entries/arch.conf` 
```
title          Arch Linux
linux          /vmlinuz-linux
initrd         /initramfs-linux.img
options        root=**/dev/sdaX** rw
```

Για περισσότερες πληροφορίες σχετικά με την επεξεργασία και χρήση του gummiboot, δείτε στο [gummiboot](/index.php/Gummiboot "Gummiboot").

##### GRUB

Πρώτα εγκαταστήστε τα πακέτα [grub](https://www.archlinux.org/packages/?name=grub) και [efibootmgr](https://www.archlinux.org/packages/?name=efibootmgr) και μετά τρέξτε `grub-install` για να εγκαταστήσετε τον bootloader στην EFI κατάρτηση του συστήματος:

**Σημείωση:** Όλες οι εντολές θα πρέπει να εκτελεστούν ΜΕΣΑ στο περιβάλλον chroot, αν υπάρχει.

```
# mount -t efivarfs efivarfs /sys/firmware/efi/efivars              # αγνοείστε το αν είναι ήδη προσαρτημένη
# pacman -S grub efibootmgr
# grub-install --target=x86_64-efi --efi-directory=/boot --bootloader-id=arch_grub --recheck

```

Μετά, αν και το να χρησιμοποιήσετε ένα χειροκίνητα δημιουργημένο `grub.cfg` είναι εντάξει, ωστόσο για τους αρχάριους συνίσταται να δημιουργήσουν ένα, αυτόματα:

**Συμβουλή:** Για να γίνει σάρωση αυτόματα, για άλλα λειτουργικά συστήματα στον υπολογιστή σας, εγκαταστήστε το [os-prober](https://www.archlinux.org/packages/?name=os-prober) , πριν τρέξετε την εντολή. Αν και το os-prober δεν γνωρίζει πως να εντοπίζει σωστά άλλα UEFI λειτουργικά συστήματα.

```
# grub-mkconfig -o /boot/grub/grub.cfg

```

Για περισσότερες πληροφορίες σχετικά με την επεξεργασία και χρήστη του GRUB, δείτε στο [GRUB](/index.php/GRUB "GRUB").

### Αποπροσαρτήστε τις κατατμήσεις και κάντε επανεκκίνηση

Πραγματοποιήστε έξοδο από το περιβάλλον chroot:

```
# exit

```

Αφού οι κατατμήσεις είναι προσαρτημένες στο `/mnt`, χρησιμοποιούμε την παρακάτω εντολή για να τις αποπροσαρτήσουμε:

```
# umount -R /mnt

```

Κάντε επανεκκίνηση:

```
# reboot

```

**Συμβουλή:** Σιγουρευτείτε πως έχετε αφαιρέσει το μέσον εγκατάστασης, διαφορετικά θα γίνει επανεκκίνηση ξανά σε αυτό.

**[Beginners' Guide (Ελληνικά)](/index.php/Beginners%27_Guide_(%CE%95%CE%BB%CE%BB%CE%B7%CE%BD%CE%B9%CE%BA%CE%AC) "Beginners' Guide (Ελληνικά)")**

* * *

[Προετοιμασία](/index.php/Beginners%27_Guide/Preparation_(%CE%95%CE%BB%CE%BB%CE%B7%CE%BD%CE%B9%CE%BA%CE%AC) "Beginners' Guide/Preparation (Ελληνικά)") >> **Εγκατάσταση** >> [Μετά την εγκατάσταση](/index.php/Beginners%27_Guide/Post-Installation_(%CE%95%CE%BB%CE%BB%CE%B7%CE%BD%CE%B9%CE%BA%CE%AC) "Beginners' Guide/Post-Installation (Ελληνικά)")