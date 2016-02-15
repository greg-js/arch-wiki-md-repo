**Σημείωση:** Αυτό το έγγραφο είναι μέρος του άρθρου πολλαπλών σελίδων για τον Οδηγό για Αρχάριους (Beginners Guide). Κάντε κλίκ [εδώ](/index.php/Beginners%27_Guide_(%CE%95%CE%BB%CE%BB%CE%B7%CE%BD%CE%B9%CE%BA%CE%AC) "Beginners' Guide (Ελληνικά)") αν θέλετε να τον διαβάσετε σε μια σελίδα.

## Contents

*   [1 Post-installation (μετά την εγκατάσταση)](#Post-installation_.28.CE.BC.CE.B5.CF.84.CE.AC_.CF.84.CE.B7.CE.BD_.CE.B5.CE.B3.CE.BA.CE.B1.CF.84.CE.AC.CF.83.CF.84.CE.B1.CF.83.CE.B7.29)
    *   [1.1 Διαχείριση χρηστών](#.CE.94.CE.B9.CE.B1.CF.87.CE.B5.CE.AF.CF.81.CE.B9.CF.83.CE.B7_.CF.87.CF.81.CE.B7.CF.83.CF.84.CF.8E.CE.BD)
    *   [1.2 Διαχείριση πακέτων](#.CE.94.CE.B9.CE.B1.CF.87.CE.B5.CE.AF.CF.81.CE.B9.CF.83.CE.B7_.CF.80.CE.B1.CE.BA.CE.AD.CF.84.CF.89.CE.BD)
    *   [1.3 Διαχείριση υπηρεσιών](#.CE.94.CE.B9.CE.B1.CF.87.CE.B5.CE.AF.CF.81.CE.B9.CF.83.CE.B7_.CF.85.CF.80.CE.B7.CF.81.CE.B5.CF.83.CE.B9.CF.8E.CE.BD)
    *   [1.4 Ήχος](#.CE.89.CF.87.CE.BF.CF.82)
    *   [1.5 Περιβάλλον εργασίας χρήστη](#.CE.A0.CE.B5.CF.81.CE.B9.CE.B2.CE.AC.CE.BB.CE.BB.CE.BF.CE.BD_.CE.B5.CF.81.CE.B3.CE.B1.CF.83.CE.AF.CE.B1.CF.82_.CF.87.CF.81.CE.AE.CF.83.CF.84.CE.B7)
        *   [1.5.1 Εγκατάσταση του X](#.CE.95.CE.B3.CE.BA.CE.B1.CF.84.CE.AC.CF.83.CF.84.CE.B1.CF.83.CE.B7_.CF.84.CE.BF.CF.85_X)
        *   [1.5.2 Εγκατάσταση ενός οδηγού γραφικών](#.CE.95.CE.B3.CE.BA.CE.B1.CF.84.CE.AC.CF.83.CF.84.CE.B1.CF.83.CE.B7_.CE.B5.CE.BD.CF.8C.CF.82_.CE.BF.CE.B4.CE.B7.CE.B3.CE.BF.CF.8D_.CE.B3.CF.81.CE.B1.CF.86.CE.B9.CE.BA.CF.8E.CE.BD)
        *   [1.5.3 Εγκατάσταση οδηγών εισόδου](#.CE.95.CE.B3.CE.BA.CE.B1.CF.84.CE.AC.CF.83.CF.84.CE.B1.CF.83.CE.B7_.CE.BF.CE.B4.CE.B7.CE.B3.CF.8E.CE.BD_.CE.B5.CE.B9.CF.83.CF.8C.CE.B4.CE.BF.CF.85)
        *   [1.5.4 Ρυθμίστε τον X](#.CE.A1.CF.85.CE.B8.CE.BC.CE.AF.CF.83.CF.84.CE.B5_.CF.84.CE.BF.CE.BD_X)
        *   [1.5.5 Δοκιμάστε τον X](#.CE.94.CE.BF.CE.BA.CE.B9.CE.BC.CE.AC.CF.83.CF.84.CE.B5_.CF.84.CE.BF.CE.BD_X)
            *   [1.5.5.1 Επίλυση προβλημάτων](#.CE.95.CF.80.CE.AF.CE.BB.CF.85.CF.83.CE.B7_.CF.80.CF.81.CE.BF.CE.B2.CE.BB.CE.B7.CE.BC.CE.AC.CF.84.CF.89.CE.BD)
        *   [1.5.6 Γραμματοσειρές](#.CE.93.CF.81.CE.B1.CE.BC.CE.BC.CE.B1.CF.84.CE.BF.CF.83.CE.B5.CE.B9.CF.81.CE.AD.CF.82)
        *   [1.5.7 Διαλέξτε και εγκαταστήστε ένα γραφικό περιβάλλον](#.CE.94.CE.B9.CE.B1.CE.BB.CE.AD.CE.BE.CF.84.CE.B5_.CE.BA.CE.B1.CE.B9_.CE.B5.CE.B3.CE.BA.CE.B1.CF.84.CE.B1.CF.83.CF.84.CE.AE.CF.83.CF.84.CE.B5_.CE.AD.CE.BD.CE.B1_.CE.B3.CF.81.CE.B1.CF.86.CE.B9.CE.BA.CF.8C_.CF.80.CE.B5.CF.81.CE.B9.CE.B2.CE.AC.CE.BB.CE.BB.CE.BF.CE.BD)
*   [2 Παράρτημα](#.CE.A0.CE.B1.CF.81.CE.AC.CF.81.CF.84.CE.B7.CE.BC.CE.B1)

## Post-installation (μετά την εγκατάσταση)

Το νέο σας βασικό σύστημα Arch Linux είναι τώρα ένα λειτουργικό GNU/Linux περιβάλλον, έτοιμο να χτιστεί σε οτιδήποτε επιθυμείτε ή απαιτείται για τους στόχους σας.

### Διαχείριση χρηστών

Προσθέστε λογαριασμούς οποιονδήποτε χρηστών που χρειάζεστε εκτός από τον υπερ-χρήστη root, όπως περιγράφεται στο [User management](/index.php/Users_and_groups#User_management "Users and groups"). Δεν είναι καλή πρακτική να χρησιμοποιείτε τον χρήστη root για καθημερινή χρήση, ή να εκθέτετε τον λογαριασμό μέσω [SSH](/index.php/SSH "SSH") σε έναν server. Ο λογαριασμός του χρήστη root πρέπει να χρησιμοποιείται μόνον για διαχειριστικές εργασίες.

### Διαχείριση πακέτων

Ο Pacman είναι ο διαχειριστής πακέτων (**pac**kage **man**ager) του Arch Linux. Δείτε στο [pacman](/index.php/Pacman_(%CE%95%CE%BB%CE%BB%CE%B7%CE%BD%CE%B9%CE%BA%CE%AC) "Pacman (Ελληνικά)") για απαντήσεις σχετικά με την εγκατάσταση, ενημέρωση και διαχείριση των πακέτων.

Εξαιτίας του ["Ορθότητα κώδικα σε σύγκριση με την άνεση"](/index.php/The_Arch_Way_(%CE%95%CE%BB%CE%BB%CE%B7%CE%BD%CE%B9%CE%BA%CE%AC)#.CE.9F.CF.81.CE.B8.CF.8C.CF.84.CE.B7.CF.84.CE.B1_.CE.BA.CF.8E.CE.B4.CE.B9.CE.BA.CE.B1_.CF.83.CE.B5_.CF.83.CF.8D.CE.B3.CE.BA.CF.81.CE.B9.CF.83.CE.B7_.CE.BC.CE.B5_.CF.84.CE.B7.CE.BD_.CE.AC.CE.BD.CE.B5.CF.83.CE.B7 "The Arch Way (Ελληνικά)"), είναι απαραίτητο να είστε ενημερωμένοι για τυχών αλλαγές που χρειάζονται χειροκίνητη παρέμβαση **πριν** κάνετε αναβάθμιση του συστήματος. Γραφτείτε στην λίστα ηλεκτρονικού ταχυδρομείου [arch-announce mailing list](https://mailman.archlinux.org/mailman/listinfo/arch-announce/) ή ελέγχετε την αρχική σελίδα [Arch news](https://www.archlinux.org/) πριν κάνετε αναβάθμιση. Εναλλακτικά, μπορεί να είναι χρήσιμο να γραφτείτε συνδρομητές [σε αυτό το RSS](https://www.archlinux.org/feeds/news/) ή να ακολουθείτε το [@archlinux](https://twitter.com/archlinux) στο Twitter.

Αν έχετε εγκαταστήσει το Arch Linux 64bit, ίσως θα θέλατε να ενεργοποιήσετε το [[multilib] αποθετήριο](/index.php/Multilib "Multilib") αν σχεδιάζετε να εγκαταστήσετε 32bit εφαρμογές.

Δείτε στο [Official repositories](/index.php/Official_repositories "Official repositories") για λεπτομέρειες σχετικά με τον σκοπό του κάθε αποθετηρίου.

### Διαχείριση υπηρεσιών

Το Arch Linux χρησιμοποιεί το [systemd](/index.php/Systemd "Systemd") ως init, το οποίο είναι ένα σύστημα και μια υπηρεσία διαχείρισης για το Linux. Για να συντηρείτε την εγκατάσταση Arch Linux που έχετε, είναι καλή ιδέα αν μάθετε τα βασικά. Η αλληλεπίδραση με το systemd γίνεται μέσω της εντολής `systemctl`. Διαβάστε το [systemd#Basic systemctl usage](/index.php/Systemd#Basic_systemctl_usage "Systemd") για περισσότερες πληροφορίες.

### Ήχος

Η [ALSA](/index.php/ALSA "ALSA") συνήθως δουλεύει χωρίς προβλήματα. Απλά, μερικές φορές χρειάζεται να είναι μην είναι σε σίγαση. Εγκαταστήστε το [alsa-utils](https://www.archlinux.org/packages/?name=alsa-utils) (το οποίο περιέχει το `alsamixer`) και ακολουθείστε [αυτές](/index.php/Advanced_Linux_Sound_Architecture#Unmuting_the_channels "Advanced Linux Sound Architecture") τις οδηγίες.

Η ALSA συμπεριλαμβάνεται στον πυρήνα και συνίσταται. Αν δεν λειτουργεί, το [OSS](/index.php/OSS "OSS") είναι μια διαθέσιμη εναλλακτική λύση. Αν έχετε προχωρημένες απαιτήσεις για τον ήχο, ρίξτε μια ματιά στο [Sound system](/index.php/Sound_system "Sound system") για μια περίληψη από διάφορα άρθρα.

### Περιβάλλον εργασίας χρήστη

#### Εγκατάσταση του X

Το [X Window System](https://en.wikipedia.org/wiki/X_Window_System "wikipedia:X Window System") (συνήθως **X11**, ή **X**) είναι ένα δικτυακό πρωτόκολο απεικόνισης το οποίο σχεδιάζει παράθυρα σε απεικονίσεις τύπου bitmap. Παρέχει την στάνταρντ εργαλειοθήκη και το πρωτόκολο για την δημιουργία γραφικών περιβάλλοντων (GUIs).

Για να εγκαταστήσετε τα βασικά πακέτα του [Xorg](/index.php/Xorg "Xorg"):

```
# pacman -S xorg-server xorg-server-utils xorg-xinit

```

Εγκαταστήστε το πακέτο [mesa](https://en.wikipedia.org/wiki/Mesa_(computer_graphics) "wikipedia:Mesa (computer graphics)") για 3D υποστήριξη:

```
# pacman -S mesa

```

#### Εγκατάσταση ενός οδηγού γραφικών

**Σημείωση:** Αν έχετε εγκαταστήσει το Arch σε εικονική μηχανή ως guest, δεν χρειάζεται να εγκαταστήσετε κάποιον οδηγό (video driver). Δείτε στο [Το Arch Linux ως guest σύστημα σε εικονική μηχανή](/index.php/VirtualBox_(%CE%95%CE%BB%CE%BB%CE%B7%CE%BD%CE%B9%CE%BA%CE%AC)#.CE.A4.CE.BF_Arch_Linux_.CF.89.CF.82_guest_.CF.83.CF.8D.CF.83.CF.84.CE.B7.CE.BC.CE.B1_.CF.83.CE.B5_.CE.B5.CE.B9.CE.BA.CE.BF.CE.BD.CE.B9.CE.BA.CE.AE_.CE.BC.CE.B7.CF.87.CE.B1.CE.BD.CE.AE "VirtualBox (Ελληνικά)") για να εγκαταστήσετε και να στήσετε τα Guest Additions και μεταπηδήστε στο [παρακάτω άρθρο](#.CE.A1.CF.85.CE.B8.CE.BC.CE.AF.CF.83.CF.84.CE.B5_.CF.84.CE.BF.CE.BD_X).

Ο πυρήνας Linux εμπεριέχει ανοιχτού-κώδικα οδηγούς κάρτας γραφικών και παρέχει υποστήριξη για επιτάχυνση υλικού. Ωστόσο, χρειάζεται υποστήριξη και από την πλευρά του χρήστη για το OpenGL και την 2D επιτάχυνση στον X11.

Αν δεν γνωρίζετε ποιο chipset είναι διαθέσιμο στο μηχανημά σας, τρέξτε:

```
$ lspci | grep VGA

```

Για μια πλήρη λίστα των ανοιχτών-οδηγών για κάρτες γραφικών, ψάξτε την βάση δεδομένων των πακέτων:

```
$ pacman -Ss xf86-video | less

```

Ο οδηγός `vesa` είναι ένας γενικός οδηγός ο οποίος θα δουλέψει με σχεδόν όλες τις GPU, αλλά δεν παρέχει κάποια 2D ή 3D επιτάχυνση. Αν δεν μπορεί να βρεθεί κάποιος καλύτερος οδηγός ή αποτύχει να φορτωθεί, τότε ο Xorg θα φορτώσει τον vesa. Για να τον εγκαταστήσετε τρέξτε:

```
# pacman -S xf86-video-vesa

```

Για να λειτουργήσει σωστά η επιτάχυνση υλικού και να γίνουν διαθέσιμες όλες οι επιλογές (modes) που μπορεί να υποστηρίζει μια GPU, ένας κατάλληλος οδηγός γραφικών είναι απαραίτητος. Δείτε στο [εγκατάσταση οδηγού(αγγλικά)](/index.php/Xorg#Driver_installation "Xorg") για έναν πίνακα με τους συχνότερα χρησιμοποιούμενους οδηγούς.

#### Εγκατάσταση οδηγών εισόδου

Ο udev θα πρέπει να είναι ικανός να εντοπίσει το υλικό σας χωρίς προβλήματα. Ο οδηγός `evdev` ([xf86-input-evdev](https://www.archlinux.org/packages/?name=xf86-input-evdev)) είνια ο καινούριος (hot-plugging) οδηγός εισόδου για σχεδόν όλες τις συσκευές. Οπότε στις περισσότερες περιπτώσεις η εγκατάσταση ενός οδηγού εισόδου δεν χρειάζεται. Σε αυτό το σημείο ο `evdev` έχει ήδη εγκατασταθεί ως εξάρτηση του πακέτου [xorg-server](https://www.archlinux.org/packages/?name=xorg-server).

Οι χρήστες Laptop (ή οι χρήστες με οθόνη αφής) θα χρειαστούν το πακέτο [xf86-input-synaptics](https://www.archlinux.org/packages/?name=xf86-input-synaptics) για να λειτουργήσουν σωστά τα touchpad/touchscreen.

```
# pacman -S xf86-input-synaptics

```

Για πληροφορίες σχετικά με την ρύθμιση και την αντιμετώπιση προβλημάτνω στο touchpad, δείτε το άρθρο [Touchpad Synaptics(αγγλικά)](/index.php/Touchpad_Synaptics "Touchpad Synaptics").

#### Ρυθμίστε τον X

**Προσοχή:** Για τους κλειστού-κώδικα οδηγούς συνήθως χρειάζεται επαννεκίνηση μετά την εγκατάσταση για να λειτουργήσουν σωστά. Δείτε στο [NVIDIA(αγγλικά)](/index.php/NVIDIA "NVIDIA") ή [AMD Catalyst(αγγλικά)](/index.php/AMD_Catalyst "AMD Catalyst") για λεπτομέρειες

Τα χαρακτηριστικά του Xorg συνήθως εντοπίζονται αυτόματα, γι' αυτό το λόγο μπορεί να λειτουργήσει απροβλημάτιστα και χωρίς αρχείο `xorg.conf`. Αν επιθυμείτε να ρυθμίσετε χειροκίνητα τον X Server, δείτε στην σελίδα [Xorg(αγγλικά)](/index.php/Xorg "Xorg").

Ίσως χρειαστεί να ρυθμίσετε χειροκίνητα την [αλλαγή γλώσσας πληκτορλογίου στον Xorg(αγγλικά)](/index.php/Keyboard_configuration_in_Xorg "Keyboard configuration in Xorg") αν δεν χρησιμοποιείτε ένα στάνταρτ [US](https://en.wikipedia.org/wiki/File:KB_United_States-NoAltGr.svg "wikipedia:File:KB United States-NoAltGr.svg") πληκτρολόγιο.

**Σημείωση:** Το `XkbLayout` ίσως είναι διαφορετικό από τον κώδικα keymap που χρησιμοποιείσατε με την εντολή `loadkeys`. Μια λίστα με πολλά keyboard layouts και παραλλαγές αυτών μπορούν να βρεθούν στο `/usr/share/X11/xkb/rules/base.lst` (μετά από την γραμμή που ξεκινά με `! layout`). Για παράδειγμα, το `gb` layout αντιστοιχεί στο "English (UK)", αν και για την κονσόλα ήταν `loadkeys uk`.

#### Δοκιμάστε τον X

**Συμβουλή:** Αυτά τα βήματα είναι προαιρετικά. Δοκιμάστε τα αν εγκαθιστάτε το Arch Linux για πρώτη φορά, ή αν κάνετε εγκατάσταση σε ένα νέο και μη συνηθισμένο υλικό(hardware).

**Σημείωση:** Αν οι συσκευές εισόδου δεν δουλεύουν κατά την διάρκεια αυτής της δοκιμής, εγκαταστήστε τον απαραίτητο οδηγό από το γκρουπ [xorg-drivers](https://www.archlinux.org/groups/x86_64/xorg-drivers/) και δοκιμάστε ξανά. Για μια πλήρη λίστα των οδηγών για συσκευές εισόδου(input devices) επικαλεστείτε την αναζήτηση του pacman (πατήστε `Q` για έξοδο):

```
$ pacman -Ss xf86-input | less

```

Το μόνο που χρειάζεστε είναι το [xf86-input-keyboard](https://www.archlinux.org/packages/?name=xf86-input-keyboard) ή το [xf86-input-mouse](https://www.archlinux.org/packages/?name=xf86-input-mouse) αν σχεδιάζετε να απενεργοποιήσετε το [hot-plugging(αγγλικά)](https://en.wikipedia.org/wiki/Hot-plugging "wikipedia:Hot-plugging"), διαφορετικά ο `evdev` θα λειτουργεί ως ο οδηγός συσκευής εισόδου (προτείνεται).

Εγκαταστήστε το προ-επιλεγμένο περιβάλλον εργασίας:

```
# pacman -S xorg-twm xorg-xclock xterm

```

Αν ο Xorg εγκαταστάθηκε πριν δημιουργήσετε τον απλό χρήστη (non-root user), θα υπάρχει ένα πρότυπο(template) `.xinitrc` αρχείο στο κατάλογο home που πρέπει είτε να το διαγράψετε ή να το μετατρέψετε σε comment(σχόλιο). Αν απλά το διαγράψετε ο **X** θα τρέχει με το προ-επιλεγμένο περιβάλλον που εγκαταστήσαμε παραπάνω.

```
$ rm ~/.xinitrc

```

**Σημείωση:** Ο X πρέπει πάντα τρέχει στο ίδιο TTY που έγινε η είσοδος(login), για να διατηρεί την logind συνεδρία. Ο χειρισμός από προ-επιλογή γίνεται μέσω του `/etc/X11/xinit/xserverrc`.

Για να εκκινήσετε την συνεδρία του Xorg, τρέξτε:

```
$ startx

```

Μερικά μετακινούμενα παράθυρα πρέπει να εμφανιστούν και το ποντίκι πρέπει να λειτουργεί. Όταν θεωρήσετε πως η εγκατάσταση του **X** ήταν επιτυχημένη, μπορείτε να βγείτε(έξοδος) από την συνεδρία τρέχοντας την εντολή `exit` μέχρι να επιστρέψετε στην κονσόλα.

```
$ exit

```

Αν η οθόνη παραμείνει μαύρη, μπορείτε να προσπαθήσετε να αλλάξετε σε μια διαφορετική εικονική κονσόλα (π.χ. `Ctrl+Alt+F2`), και να συνδεθείτε (στα τυφλά) ως υπερ-χρήστης (root). Μπορείτε να το κάνετε πληκτρολογώντας "root" (πατήστε `Enter` αφού το πληκτρολογήσετε) και εισάγοντας τον κωδικό (ξανά, πατήστε `Enter` μετά την εισαγωγή του κωδικού).

Επίσης μπορείτε να προσπαθήστε να σκοτώσετε τον **X** με:

```
# pkill X

```

Αν ούτε αυτό δουλέψει, κάντε επανεκκίνηση(στα τυφλά) πληκτρολογώντας:

```
# reboot

```

##### Επίλυση προβλημάτων

Αν παρουσιαστεί κάποιο πρόβλημα, κοιτάξτε για λάθη στο αρχείο `Xorg.0.log`. Παρατηρείστε οποιεσδήποτε γραμμές ξεκινούν με `(EE)`, που δείχνουν ότι υπάρχει λάθος(Error) ή και `(WW)` που δείχνουν ότι υπάρχει προειδοποίηση(Warning).

```
$ grep EE /var/log/Xorg.0.log

```

Αν εξακολουθείτε να αντιμετωπίζετε πρόβλημα, αφού συμβουλευτείτε το άρθρο [Xorg(αγγλικά)](/index.php/Xorg "Xorg") και ακόμη χρειάζεστε βοήθεια από το Arch Linux Forum ή το IRC κανάλι, εγκαταστήστε και χρησιμοποιείστε το [wgetpaste](https://www.archlinux.org/packages/?name=wgetpaste) και παραθέστε τα links από:

```
# pacman -S wgetpaste
$ wgetpaste ~/.xinitrc
$ wgetpaste /etc/X11/xorg.conf
$ wgetpaste /var/log/Xorg.0.log

```

**Σημείωση:** Παρακαλούμε να παρέχετε όλες τις σχετικές πληροφορίες (υλικό(hardware), πληροφορίες οδηγών(driver)...κλπ) όταν ζητάτε βοήθεια.

#### Γραμματοσειρές

Ίσως θέλετε να εγκαταστήσετε ένα σετ από TrueType γραμματοσειρές, διότι μόνον οι bitmap γραμματοσειρές συμπεριλαμβάνονται από προ-επιλογή. Ωστόσο αν χρησιμοποιήσετε ένα πλήρες [γραφικό περιβάλλον(αγγλικά)](/index.php/Desktop_environment "Desktop environment") όπως για παράδειγμα το [KDE|KDE(αγγλικά)]], τότε αυτό το βήμα μάλλον δεν χρειάζεται. Οι DejaVu είναι ένα σετ υψηλής ποιότητας και γενικής χρήσεως γραμματοσειρές με καλή υποστήριξη [Unicode](http://el.wikipedia.org/wiki/Unicode):

```
# pacman -S ttf-dejavu

```

Κοιτάξτε το [Font Configuration(αγγλικά)](/index.php/Font_configuration "Font configuration") για το πως να ρυθμίσετε το font rendering και το [Fonts(αγγλικά)](/index.php/Fonts "Fonts") για συμβουλές και οδηγίες σχετικά με την εγκατάσταση.

```
# pacman -S ttf-dejavu

```

#### Διαλέξτε και εγκαταστήστε ένα γραφικό περιβάλλον

Στο X Window System παρέχει το βασικό framework για να χτίσετε ένα γραφικό περιβάλλον χρήστη (GUI).

**Σημείωση:** Η επιλογή του DE ή WM είναι καθαρά θέμα προσωπικής απόφασης. Διαλέξτε το περιβάλλον που ταιριάζει καλύτερα στις δικές σας ανάγκες. Επίσης μπορείτε να χτίσετε το δικό σας DE με μόνο έναν WM και τις εφαρμογές της επιλογής σας.

*   Οι [Window Managers](/index.php/Window_manager "Window manager") (WM) ελέγχουν και καθορίζουν την εμφάνιση των παραθύρων των εφαρμογών σε συνδυασμό με το X Window System.

*   Τα [Desktop Environments](/index.php/Desktop_environment "Desktop environment") (DE) λειτουργούν πάνω και σε συνδυασμό με τον X, για να παρέχουν ένα πλήρως λειτουργικό και δυναμικό GUI. Ένα DE τυπικά παρέχει έναν διαχειριστή παραθύρων(window manager), εικονίδια, εφαρμογές, παράθυρα, καταλόγους, ταπετσαρίες, μια σουίτα από εφαρμογές και λειτουργίες όπως το drag and drop.

Αντί να εκκινήσετε τον X χειροκίνητα με την `startx` από το [xorg-xinit](https://www.archlinux.org/packages/?name=xorg-xinit), δείτε το [Display manager(αγγλικά)](/index.php/Display_manager "Display manager") για οδηγίες χρήσης ενός Display Manager, ή δείτε το [Start X at Login(αγγλικά)](/index.php/Start_X_at_login "Start X at login") για να χρησιμοποιήσετε ένα εικονικό τερματικό ως το αντίστοιχο του display manager.

## Παράρτημα

Για μια λίστα από εφαρμογές που μπορεί να σας ενδιαφέρουν, δείτε στο [List of Applications(αγγλικά)](/index.php/List_of_applications "List of applications").

Δείτε στο [Γενικές Συμβουλές](/index.php/General_Recommendations_(%CE%95%CE%BB%CE%BB%CE%B7%CE%BD%CE%B9%CE%BA%CE%AC) "General Recommendations (Ελληνικά)") για μετά-την-εγκατάσταση tutorials όπως, πως να ρυθμίσετε το touchpad ή το font rendering.

**[Beginners' Guide (Ελληνικά)](/index.php/Beginners%27_Guide_(%CE%95%CE%BB%CE%BB%CE%B7%CE%BD%CE%B9%CE%BA%CE%AC) "Beginners' Guide (Ελληνικά)")**

* * *

[Προετοιμασία](/index.php/Beginners%27_Guide/Preparation_(%CE%95%CE%BB%CE%BB%CE%B7%CE%BD%CE%B9%CE%BA%CE%AC) "Beginners' Guide/Preparation (Ελληνικά)") >> [Εγκατάσταση](/index.php/Beginners%27_Guide/Installation_(%CE%95%CE%BB%CE%BB%CE%B7%CE%BD%CE%B9%CE%BA%CE%AC) "Beginners' Guide/Installation (Ελληνικά)") >> **Μετά την εγκατάσταση**