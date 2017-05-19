Από την [ιστοσελίδα του project](http://freedesktop.org/wiki/Software/systemd):

*Ο* **systemd** είναι ένας διαχειριστής συστήματος και υπηρεσιών για το Linux, συμβατός με τα script εκκίνησης SysV και LSB. O systemd είναι ικανός για παραλληλισμό εργασιών, χρησιμοποιεί socket και τον [D-Bus(*αγγλικά*)](/index.php/D-Bus "D-Bus") για να εκκινήσει τις υπηρεσίες. Προσφέρει εκκίνηση daemons σύφωνα με τις επιθυμίες του χρήστη, παρακολουθεί τις υπηρεσίες που χρησιμοποιούν τα Linux [control groups(*αγγλικά*)](/index.php/Cgroups "Cgroups"), υποστηρίζει snapshooting και επαναφορά του συστήματος σε προηγούμενη κατάσταση, συντηρεί τα σημεία προσάρτησης (και αυτόματης προσάρτησης) και υλοποιεί μια επιμελημένη, βασισμένη σε εξαρτήσεις, κεντρική λογική υπηρεσίων.

**Σημείωση:** Για μια λεπτομερή εξήγηση σχετικά με το γιατί το Arch μετακινήθηκε στο *systemd*, δείτε [αυτήν την ανάρτηση στο forum](https://bbs.archlinux.org/viewtopic.php?pid=1149530#p1149530).

## Contents

*   [1 Βασική χρήση της εντολής systemctl](#.CE.92.CE.B1.CF.83.CE.B9.CE.BA.CE.AE_.CF.87.CF.81.CE.AE.CF.83.CE.B7_.CF.84.CE.B7.CF.82_.CE.B5.CE.BD.CF.84.CE.BF.CE.BB.CE.AE.CF.82_systemctl)
    *   [1.1 Αναλύοντας την κατάσταση του συστήματος](#.CE.91.CE.BD.CE.B1.CE.BB.CF.8D.CE.BF.CE.BD.CF.84.CE.B1.CF.82_.CF.84.CE.B7.CE.BD_.CE.BA.CE.B1.CF.84.CE.AC.CF.83.CF.84.CE.B1.CF.83.CE.B7_.CF.84.CE.BF.CF.85_.CF.83.CF.85.CF.83.CF.84.CE.AE.CE.BC.CE.B1.CF.84.CE.BF.CF.82)
    *   [1.2 Χρησιμοποιώντας τις μονάδες (units)](#.CE.A7.CF.81.CE.B7.CF.83.CE.B9.CE.BC.CE.BF.CF.80.CE.BF.CE.B9.CF.8E.CE.BD.CF.84.CE.B1.CF.82_.CF.84.CE.B9.CF.82_.CE.BC.CE.BF.CE.BD.CE.AC.CE.B4.CE.B5.CF.82_.28units.29)
    *   [1.3 Διαχείριση ενέργειας](#.CE.94.CE.B9.CE.B1.CF.87.CE.B5.CE.AF.CF.81.CE.B9.CF.83.CE.B7_.CE.B5.CE.BD.CE.AD.CF.81.CE.B3.CE.B5.CE.B9.CE.B1.CF.82)
*   [2 Γράφοντας προσαρμοσμένα .service files](#.CE.93.CF.81.CE.AC.CF.86.CE.BF.CE.BD.CF.84.CE.B1.CF.82_.CF.80.CF.81.CE.BF.CF.83.CE.B1.CF.81.CE.BC.CE.BF.CF.83.CE.BC.CE.AD.CE.BD.CE.B1_.service_files)
    *   [2.1 Χειρισμός εξαρτήσεων](#.CE.A7.CE.B5.CE.B9.CF.81.CE.B9.CF.83.CE.BC.CF.8C.CF.82_.CE.B5.CE.BE.CE.B1.CF.81.CF.84.CE.AE.CF.83.CE.B5.CF.89.CE.BD)
    *   [2.2 Είδος](#.CE.95.CE.AF.CE.B4.CE.BF.CF.82)
    *   [2.3 Επεξεργασία σε παρεχόμενα αρχεία μονάδων](#.CE.95.CF.80.CE.B5.CE.BE.CE.B5.CF.81.CE.B3.CE.B1.CF.83.CE.AF.CE.B1_.CF.83.CE.B5_.CF.80.CE.B1.CF.81.CE.B5.CF.87.CF.8C.CE.BC.CE.B5.CE.BD.CE.B1_.CE.B1.CF.81.CF.87.CE.B5.CE.AF.CE.B1_.CE.BC.CE.BF.CE.BD.CE.AC.CE.B4.CF.89.CE.BD)
    *   [2.4 Επισήμανση σύνταξης για μονάδες με τον Vim](#.CE.95.CF.80.CE.B9.CF.83.CE.AE.CE.BC.CE.B1.CE.BD.CF.83.CE.B7_.CF.83.CF.8D.CE.BD.CF.84.CE.B1.CE.BE.CE.B7.CF.82_.CE.B3.CE.B9.CE.B1_.CE.BC.CE.BF.CE.BD.CE.AC.CE.B4.CE.B5.CF.82_.CE.BC.CE.B5_.CF.84.CE.BF.CE.BD_Vim)
*   [3 Targets](#Targets)
    *   [3.1 Δείτε τα τρέχοντα targets](#.CE.94.CE.B5.CE.AF.CF.84.CE.B5_.CF.84.CE.B1_.CF.84.CF.81.CE.AD.CF.87.CE.BF.CE.BD.CF.84.CE.B1_targets)
    *   [3.2 Δημιουργία προσαρμοσμένου target](#.CE.94.CE.B7.CE.BC.CE.B9.CE.BF.CF.85.CF.81.CE.B3.CE.AF.CE.B1_.CF.80.CF.81.CE.BF.CF.83.CE.B1.CF.81.CE.BC.CE.BF.CF.83.CE.BC.CE.AD.CE.BD.CE.BF.CF.85_target)
    *   [3.3 Πίνακας Targets](#.CE.A0.CE.AF.CE.BD.CE.B1.CE.BA.CE.B1.CF.82_Targets)
    *   [3.4 Αλλαγή τρέχοντος target](#.CE.91.CE.BB.CE.BB.CE.B1.CE.B3.CE.AE_.CF.84.CF.81.CE.AD.CF.87.CE.BF.CE.BD.CF.84.CE.BF.CF.82_target)
    *   [3.5 Αλλαγή προεπιλεγμένου target εκκίνησης συστήματος](#.CE.91.CE.BB.CE.BB.CE.B1.CE.B3.CE.AE_.CF.80.CF.81.CE.BF.CE.B5.CF.80.CE.B9.CE.BB.CE.B5.CE.B3.CE.BC.CE.AD.CE.BD.CE.BF.CF.85_target_.CE.B5.CE.BA.CE.BA.CE.AF.CE.BD.CE.B7.CF.83.CE.B7.CF.82_.CF.83.CF.85.CF.83.CF.84.CE.AE.CE.BC.CE.B1.CF.84.CE.BF.CF.82)
*   [4 Temporary files](#Temporary_files)
*   [5 Timers](#Timers)
*   [6 Journal](#Journal)
    *   [6.1 Filtering output](#Filtering_output)
    *   [6.2 Journal size limit](#Journal_size_limit)
    *   [6.3 Journald in conjunction with syslog](#Journald_in_conjunction_with_syslog)
    *   [6.4 Forward journald to /dev/tty12](#Forward_journald_to_.2Fdev.2Ftty12)
*   [7 Troubleshooting](#Troubleshooting)
    *   [7.1 Investigating systemd errors](#Investigating_systemd_errors)
    *   [7.2 Diagnosing boot problems](#Diagnosing_boot_problems)
    *   [7.3 Shutdown/reboot takes terribly long](#Shutdown.2Freboot_takes_terribly_long)
    *   [7.4 Short lived processes do not seem to log any output](#Short_lived_processes_do_not_seem_to_log_any_output)
    *   [7.5 Disabling application crash dumps journaling](#Disabling_application_crash_dumps_journaling)
    *   [7.6 Error message on reboot or shutdown](#Error_message_on_reboot_or_shutdown)
        *   [7.6.1 cgroup : option or name mismatch, new: 0x0 "", old: 0x4 "systemd"](#cgroup_:_option_or_name_mismatch.2C_new:_0x0_.22.22.2C_old:_0x4_.22systemd.22)
        *   [7.6.2 watchdog watchdog0: watchdog did not stop!](#watchdog_watchdog0:_watchdog_did_not_stop.21)
*   [8 See also](#See_also)

## Βασική χρήση της εντολής systemctl

Η βασική εντολή που χρησιμοποιείται για τον έλεγχο του *systemd* είναι η **systemctl**. Μερικές από τις χρήσεις της εντολής εξετάζουν την κατάσταση του συστήματος και διαχειρίζονται το σύστημα και τις υπηρεσίες (services). Δες το `man 1 systemctl` για περισσότερες λεπτομέρειες.

**Συμβουλή:** Μπορείτε να χρησιμοποιήσετε όλες τις ακόλουθες εντολές του systemctl μαζί με το `-H *user*@*host*` switch για να ελέγξετε το *systemd* σε μια απομακρυσμένη μηχανή. Αυτό θα χρησιμοποιήσει το δικτυακό πρωτόκολλο [SSH(*αγγλικά*)](/index.php/SSH "SSH") για να συνδεθεί στο απομακρυσμένο *systemd* σύστημα.

**Σημείωση:** Το *systemadm* είναι το επίσημο γραφικό frontend για το *systemctl*. Παρέχεται από το πακέτο [systemd-ui-git](https://aur.archlinux.org/packages/systemd-ui-git/) από το [AUR](/index.php/Arch_User_Repository_(%CE%95%CE%BB%CE%BB%CE%B7%CE%BD%CE%B9%CE%BA%CE%AC) "Arch User Repository (Ελληνικά)").

### Αναλύοντας την κατάσταση του συστήματος

Παρέχει λίστα των μονάδων (units) που εκτελούνται:

```
$ systemctl

```

ή

```
$ systemctl list-units

```

Παρέχει λίστα των μονάδων που απέτυχαν:

```
$ systemctl --failed

```

Οι διαθέσιμες μονάδες φαίνονται στο `/usr/lib/systemd/system/` και στο `/etc/systemd/system/` (το τελευταίο έχει προτεραιότητα). Μπορείτε να δείτε μια λίστα των εγκατεστημένων αρχείων των μονάδων με την εντολή:

```
$ systemctl list-unit-files

```

### Χρησιμοποιώντας τις μονάδες (units)

Οι μονάδες μπορούν να είναι, για παράδειγμα, υπηρεσίες (*.service*), σημεία προσάρτησης (*.mount*), συσκευές (*.device*) ή υποδοχές (*.socket*)

Όταν χρησιμοποιούμε το *systemctl*, γενικά πρέπει να προσδιορίσουμε το πλήρες όνομα του αρχείου της μονάδας, συμπεριλαμβανομένης της κατάληξης του, για παράδειγμα *sshd.socket*. Υπάρχουν ωστόσο μερικές σύντομες μορφές για τον προσδιορισμό των μονάδων στις ακόλουθες εντολές του *systemctl* :

*   Αν δεν προσδιορίσουμε την κατάληξη το systemctl θα υποθέσει πως πρόκειται για υπηρεσία *.service*. Για παράδειγμα, το `netcfg` και το `netcfg.service` είναι ισοδύναμα.
*   Τα σημεία προσάρτησης θα μεταφράζονται αυτόματα σε κατάλληλη μονάδα*.mount*. Για παράδειγμα, το να προσδιορίσουμε το `/home` είναι ισοδύναμο με το `home.mount`.
*   Ομοίως με τα σημεία προσάρτησης, οι συσκευές θα μεταφράζονται αυτόματα σε κατάλληλη μονάδα *.device* και ως εκ τούτου το να προσδιορίζουμε το `/dev/sda2` είναι ισοδύναμο με το `dev-sda2.device`.

Δείτε στο `man systemd.unit` για λεπτομέρειες.

**Συμβουλή:** Οι περισσότερες από τις παρακάτω εντολές λειτουργούν επίσης όταν πολλαπλές μονάδες προσδιοριστούν, δείτε το `man systemctl` για περισσότερες πληροφορίες.

Για να ενεργοποιήσετε μια μονάδα αμέσως:

```
# systemctl start *unit*

```

Απενεργοποιήστε μια μονάδα αμέσως:

```
# systemctl stop *unit*

```

Επανεκκίνηση μια μονάδας:

```
# systemctl restart *unit*

```

Για να φορτώσει ξανά τις ρυθμίσεις:

```
# systemctl reload *unit*

```

Δείτε την κατάσταση μιας μονάδας, συμπεριλαμβανομένου του αν τρέχει ή όχι:

```
$ systemctl status *unit*

```

Δείτε αν μια μονάδα είναι ενεργοποιημένη ή όχι:

```
$ systemctl is-enabled *unit*

```

Ενεργοποιείστε μια μονάδα έτσι ώστε να εκκινεί κατά το boot:

```
# systemctl enable *unit*

```

**Σημείωση:** Οι υπηρεσίες χωρίς `[Install]` τμήμα, συνήθως καλούνται αυτόματα από άλλες υπηρεσίες. Αν χρειάζεστε να τις εγκαταστήσετε χειροκίνητα, χρησιμοποιείστε την επόμενη εντολή, αντικαθιστώντας το *foo* με το όνομα της υπηρεσίας.
```
 # ln -s /usr/lib/systemd/system/*foo*.service /etc/systemd/system/graphical.target.wants/

```

Απενεργοποίηση μιας υπηρεσίας έτσι ώστε να μην εκκινεί κατά το boot:

```
# systemctl disable *unit*

```

Δείτε την σελίδα τεκμηρίωσης που σχετίζεται με μια μονάδα (πρέπει να υποστηρίζεται από το αρχείο (unit file)):

```
$ systemctl help *unit*

```

Φορτώστε ξανά το *systemd* σαρώνοντας και εντοπίζοντας νέες μονάδες ή μονάδες που έχουν αλλάξει:

```
# systemctl daemon-reload

```

### Διαχείριση ενέργειας

Το [polkit(*αγγλικά*)](/index.php/Polkit "Polkit") είναι απαραίτητο για να διαχειριστείτε την ενέργεια ως απλός χρήστης (non-root user). Αν βρίσκεστε σε μια τοπική *systemd-logind* συνεδρία χρήστη και καμία άλλη συνεδρία δεν είναι ενεργή, οι παρακάτω εντολές θα λειτουργήσουν χωρίς δικαιώματα υπερ-χρήστη(root). Αν όχι, (επειδή για παράδειγμα ένας άλλος χρήστης είναι συνδεδεμένος σε ένα TTY), το *systemd* αυτόματα θα σας ζητήσει τον κωδικό του υπερ-χρήστη (root).

Επανεκκίνηση του συστήματος:

```
$ systemctl reboot

```

Διακοπή λειτουργίας του συστήματος:

```
$ systemctl poweroff

```

Θέστε το σύστημα σε κατάσταση αναστολής λειτουργίας:

```
$ systemctl suspend

```

Θέστε το σύστημα σε κατάσταση αδρανοποίησης:

```
$ systemctl hibernate

```

Θέστε το σύστημα σε κατάσταση υβριδικού-ύπνου:

```
$ systemctl hybrid-sleep

```

## Γράφοντας προσαρμοσμένα .service files

Η σύνταξη του systemd [(χρησιμοποιώντας τις μονάδες)](#.CE.A7.CF.81.CE.B7.CF.83.CE.B9.CE.BC.CE.BF.CF.80.CE.BF.CE.B9.CF.8E.CE.BD.CF.84.CE.B1.CF.82_.CF.84.CE.B9.CF.82_.CE.BC.CE.BF.CE.BD.CE.AC.CE.B4.CE.B5.CF.82_.28units.29) είναι εμπνευσμένη από τα *.desktop* files του XDG Desktop Entry, τα οποία είναι εμπνευσμένα από τα *.ini* files της Microsoft.

### Χειρισμός εξαρτήσεων

Με τον *systemd* οι εξαρτήσεις μπορούν να επιλυθούν σχεδιάζοντας ένα αρχείο μονάδας(unit file) σωστά. Η πιο συνήθης περίπτωση είναι πως η μονάδα *A* απαιτεί την μονάδα *B* να τρέχει ήδη, πριν η μονάδα *A* ξεκινήσει. Σε αυτή την περίπτωση προσθέτουμε `Requires=*B*` και `After=*B*` στο τμήμα `[Unit]` της μονάδας *A*. Αν η εξάρτηση είναι προαιρετική, προσθέτουμε `Wants=*B*` και `After=*B*`. Σημειώστε ότι τα `Wants=` και `Requires=` δεν συνεπάγονται το `After=`, που σημαίνει πως αν το `After=` δεν καθοριστεί, οι δύο μονάδες θα εκκινήσουν παράλληλα.

Οι εξαρτήσεις, συνήθως, τοποθετούνται στις υπηρεσίες (services) και όχι στα targets. Για παράδειγμα, το *network.target* «τραβιέται» από οποιαδήποτε υπηρεσία εκκινεί και ρυθμίζει τις διασυνδέσεις του δικτύου σας και ως εκ τούτου διατάσσοντας την προσαρμοσμένη μονάδα μετά(after), είναι αρκετό αφού το *netwrok.target* εκκινεί ούτως ή άλλως.

### Είδος

Υπάρχουν πολλά διαφορετικά είδη start-up που πρέπει να σκεφτούμε όταν γράφουμε ένα προσαρμοσμένο αρχείο service. Αυτό το καθορίζουμε με την παράμετρο `Type=` στο τμήμα `[Service]`. Δείτε στο `man systemd.service` για πιο λεπτομερή εξήγηση.

*   `Type=simple` (προεπιλογή): Ο *systemd* θεωρεί ότι η υπηρεσία πρέπει να εκκινήσει αμέσως. Η διεργασία δεν πρέπει να γίνεται fork. Μην χρησιμοποιείτε αυτόν τον τύπο αν άλλες υπηρεσίες πρέπει να τακτοποιηθούν βάση της συγκεκριμένης υπηρεσίας, εκτός και αν ενεργοποιείται μέσω socket.
*   `Type=forking`: O *systemd* θεωρεί πως η υπηρεσία έχει εκκινηθεί όταν η διεργασία έχει γίνει fork και η parent έχει τερματιστεί. Για κλασικές διεργασίες deamon χρησιμοποιείστε αυτόν τον τύπο, εκτός αν γνωρίζετε πως δεν είναι απαραίτητο. Πρέπει να προσδιορίσετε και το `PIDFile=`, έτσι ώστε ο *systemd* να μπορεί να παρακολουθεί την βασική διεργασία.
*   `Type=oneshot`: αυτός ο τύπος είναι εύχρηστος για scripts που κάνουν μια συγκεκριμένη «δουλειά» και μετά τερματίζονται. Μπορείτε να θέσετε και το `RemainAfterExit=yes` έτσι ώστε ο *systemd* να θεωρεί την διεργασία ως ενεργή, ακόμη και μετά τον τερματισμό της.
*   `Type=notify`: πανομοιότυπο με το `Type=simple`, με την προϋπόθεση ότι o daemon θα στείλει ένα σήμα στον *systemd* για το πότε είναι έτοιμος. Η υλοποίηση της αναφοράς για την εν λόγω ειδοποίηση παρέχεται από το *libsystemd-daemon.so*.
*   `Type=dbus`: η υπηρεσία θεωρείται έτοιμη όταν το προσδιορισμένο `BusName` εμφανίζεται στο system bus του Dbus.

### Επεξεργασία σε παρεχόμενα αρχεία μονάδων

Για να επεξεργαστείτε ένα αρχείο μονάδας(unit) που παρέχεται από κάποιο πακέτο, μπορείτε να δημιουργήσετε έναν κατάλογο που να ονομάζεται `/etc/systemd/system/*unit*.d/`, για παράδειγμα `/etc/systemd/system/httpd.service.d/` και να τοποθετήσετε τα αρχεία **.conf* εκεί μέσα έτσι ώστε να παρακάμψετε ή να προσθέσετε νέες επιλογές. Ο *systemd* θα αναλύσει τα αρχεία **.conf* και θα τα "περάσει" στην κορυφή της πρωτότυπης μονάδας(unit). Για παράδειγμα, αν απλά θέλετε να προσθέσετε μια επιπρόσθετη εξάρτηση σε μια μονάδα, μπορείτε να δημιουργήσετε το παρακάτω αρχείο:

 `/etc/systemd/system/*unit*.d/customdependency.conf` 
```
[Unit]
Requires=*new dependency*
After=*new dependency*
```

Ως άλλο ένα παράδειγμα, για να αντικαταστήσετε την οδηγία του `ExecStart` για μια μονάδα, που δεν είναι του τύπου `oneshot`, δημιουργήστε το παρακάτω αρχείο:

 `/etc/systemd/system/*unit*.d/customexec.conf` 
```
[Service]
ExecStart=
ExecStart=*new command*
```

Άλλο ένα παράδειγμα για την αυτόματη επανεκκίνηση μιας υπηρεσίας:

 `/etc/systemd/system/*unit*.d/restart.conf` 
```
[Service]
Restart=always
RestartSec=30
```

Έπειτα τρέξτε το παρακάτω για να τεθούν σε ισχύ οι αλλαγές σας:

```
# systemctl daemon-reload
# systemctl restart *unit*

```

Εναλλακτικά μπορείτε να αντιγράψετε το παλιό αρχείο μονάδας από το `/usr/lib/systemd/system/` στο `/etc/systemd/system/` και να κάνετε τις αλλαγές σας εκεί. Ένα αρχείο μονάδας στο `/etc/systemd/system/` πάντα παρακάμπτει/αντικαθιστά την ίδια μονάδα που βρίσκεται στο `/usr/lib/systemd/system/`. Σημειώστε πως όταν η πρωτότυπη μονάδα στο `/usr/lib/` αλλάξει, πιθανών λόγω αναβάθμισης του πακέτου, αυτές οι αλλαγές δεν θα περαστούν αυτόματα στο προσαρμοσμένο αρχείο σας στο `/etc/`. Επιπροσθέτως θα πρέπει να ενεργοποιήσετε πάλι την μονάδα χειροκίνητα με `systemctl reenable *unit*`. Γι' αυτό το λόγο προτείνεται να χρησιμοποιείτε την μέθοδο με τα αρχεία **.conf* που περιγράφεται παραπάνω.

**Συμβουλή:** Μπορείτε να χρησιμοποιήσετε το **systemd-delta** για να δείτε ποιες μονάδες έχουν παρακαμφθεί/αντιγραφεί και ποιες ακριβώς αλλαγές έχουν γίνει.

Όπως τα παρεχόμενα αρχεία μονάδων θα αναβαθμίζονται από καιρό σε καιρό, χρησιμοποιείστε το *systemd-delta* για συντήρηση του συστήματος.

### Επισήμανση σύνταξης για μονάδες με τον Vim

Η επισήμανση σύνταξης για τα αρχεία μονάδων του *systemd* μέσα στον [Vim(*αγγλικά*)](/index.php/Vim "Vim") μπορεί να ενεργοποιηθεί εγκαθιστώντας το [vim-systemd](https://www.archlinux.org/packages/?name=vim-systemd) από τα [επίσημα αποθετήρια(*αγγλικά*).](/index.php/Official_repositories "Official repositories")

## Targets

Το *systemd* χρησιμοποιεί τα *targets* τα οποία εξυπηρετούν έναν παρόμοιο σκοπό με τα runlevels όμως συμπεριφέρονται λίγο διαφορετικά. Κάθε *target* διαθέτει ένα όνομα αντί για αριθμό και προτίθεται να εξυπηρετήσει έναν συγκεκριμένο σκοπό με την πιθανότητα να υπάρχουν περισσότερα από ένα ενεργά την ίδια στιγμή. Κάποια *target*s εφαρμόζονται καθώς δανείζονται όλα τα services ενός άλλου *target* και προσθέτοντας επιπρόσθετα services σε αυτό. Στο *systemd* υπάρχουν *target*s τα οποία μιμούνται τα πιο κοινώς γνωστά runlevels του SystemVinit οπότε και μπορείτε ακόμη να αλλάξετε σε κάποια *target*s χρησιμοποιώντας την συνηθισμένη εντολή `telinit RUNLEVEL`.

### Δείτε τα τρέχοντα targets

Το παρακάτω πρέπει να χρησιμοποιείται στο *systemd* αντί του `runlevel`:

```
$ systemctl list-units --type=target

```

### Δημιουργία προσαρμοσμένου target

Τα runlevels στα οποία έχει ανατεθεί ένας συγκεκριμένος σκοπός σε μια "καθαρή" εγκατάσταση Fedora, 0, 1, 3, 5, και 6, έχουν μια αντιστοίχιση 1:1 με κάποιο συγκεκριμένο *systemd* *target*. Δυστυχώς, δεν υπάρχει κάποιος αξιόπιστος τρόπος να κάνετε το ίδιο σε runlevels επιπέδου χρήστη όπως τα 2 και 4\. Αν κάνετε χρήση των συγκεκριμένων, προτείνεται να δημιουργήσετε ένα νέο *systemd* *target* με όνομα `/etc/systemd/system/*your target*` το οποίο θα παίρνει ένα από τα ήδη υπάρχοντα runlevels ως βάση (μπορείτε να δείτε στο `/usr/lib/systemd/system/graphical.target` ως παράδειγμα), να δημιουργήσετε ένα κατάλογο `/etc/systemd/system/*your target*.wants`, και μετά να φτιάξετε ένα symlink των επιπρόσθετων services από το `/usr/lib/systemd/system/` τα οποία θέλετε να ενεργοποιήσετε.

### Πίνακας Targets

| SysV Runlevel | systemd Target | Σημειώσεις |
| 0 | runlevel0.target, poweroff.target | Τερματισμός συστήματος. |
| 1, s, single | runlevel1.target, rescue.target | Single user mode. |
| 2, 4 | runlevel2.target, runlevel4.target, multi-user.target | Runlevels ορισμένα από τον χρήστη. Από προεπιλογή, ακριβώς ίδιο με το 3. |
| 3 | runlevel3.target, multi-user.target | Πολλαπλού-χρήστη, μη-γραφικό. Οι χρήστες συνήθως μπορούν να κάνουν εισαγωγή στο σύστημα μέσα από πολλαπλές κονσόλες ή μέσω δικτύου. |
| 5 | runlevel5.target, graphical.target | Πολλαπλού-χρήστη, γραφικό. Συνήθως περιλαμβάνει όλα τα services του runlevel 3 και επιπροσθέτως ένα γραφικό περιβάλλον σύνδεσης. |
| 6 | runlevel6.target, reboot.target | Επανεκκίνηση |
| emergency | emergency.target | Κέλυφος έκτακτης ανάγκης |

### Αλλαγή τρέχοντος target

Στο *systemd* τα targets εκτίθενται μέσω των *target units*. Μπορείτε να τα αλλάξετε ως εξής:

```
# systemctl isolate graphical.target 

```

Αυτό θα τροποποιήσει μόνο το τρέχον target και δεν έχει καμία επίδραση στην επόμενη εκκίνηση συστήματος. Ισοδυναμεί με εντολές όπως `telinit 3` ή `telinit 5` του Sysvinit.

### Αλλαγή προεπιλεγμένου target εκκίνησης συστήματος

Το κανονικό target είναι το *default.target*, το οποίο από προεπιλογή είναι ένα alias του *graphical.target* (το οποίο αντιστοιχεί περίπου στο παλιό runlevel 5). Για να αλλάξετε το προεπιλεγμένο target κατά τη διάρκεια της εκκίνησης, προσθέστε μια από τις ακόλουθες [παραμέτρους πυρήνα(*αγγλικά*)](/index.php/Kernel_parameters "Kernel parameters") στον bootloader:

**Tip:** The η επέκταση*.target* μπορεί να παραληφθεί.

*   `systemd.unit=multi-user.target` (το οποίο αντιστοιχεί περίπου στο παλιό runlevel 3),
*   `systemd.unit=rescue.target` (το οποίο αντιστοιχεί περίπου στο παλιό runlevel 1).

Εναλλακτικά, μπορείτε να μην πειράξετε τον bootloader αλλά να αλλάξετε το *default.target*. Αυτό μπορεί να γίνει χρησιμοποιώντας την *systemctl*:

```
# systemctl enable multi-user.target

```

Η επίδραση αυτής της εντολής φαίνεται στη έξοδο της *systemctl*· ένα symlink στο νέο προεπιλεγμένο target δημιουργείται στο `/etc/systemd/system/default.target`. Αυτό λειτουργεί μόνον αν το:

```
[Install]
Alias=default.target

```

υπάρχει στο αρχείο ρυθμίσεων του target. Για τώρα, τα *multi-user.target* και *graphical.target* το έχουν και τα δυο.

## Temporary files

"**systemd-tmpfiles** creates, deletes and cleans up volatile and temporary files and directories." It reads configuration files in `/etc/tmpfiles.d/` and `/usr/lib/tmpfiles.d/` to discover which actions to perform. Configuration files in the former directory take precedence over those in the latter directory.

Configuration files are usually provided together with service files, and they are named in the style of `/usr/lib/tmpfiles.d/*program*.conf`. For example, the [Samba](/index.php/Samba "Samba") daemon expects the directory `/run/samba` to exist and to have the correct permissions. Therefore, the [samba](https://www.archlinux.org/packages/?name=samba) package ships with this configuration:

 `/usr/lib/tmpfiles.d/samba.conf`  `D /run/samba 0755 root root` 

Configuration files may also be used to write values into certain files on boot. For example, if you used `/etc/rc.local` to disable wakeup from USB devices with `echo USBE > /proc/acpi/wakeup`, you may use the following tmpfile instead:

 `/etc/tmpfiles.d/disable-usb-wake.conf`  `w /proc/acpi/wakeup - - - - USBE` 

See the `systemd-tmpfiles` and `tmpfiles.d(5)` man pages for details.

**Note:** This method may not work to set options in `/sys` since the *systemd-tmpfiles-setup* service may run before the appropriate device modules is loaded. In this case you could check whether the module has a parameter for the option you want to set with `modinfo *module*` and set this option with a [config file in /etc/modprobe.d](/index.php/Modprobe.d#Configuration "Modprobe.d"). Otherwise you will have to write a [udev rule](/index.php/Udev#About_udev_rules "Udev") to set the appropriate attribute as soon as the device appears.

## Timers

Systemd can replace cron functionality to a great extent. See [systemd/Timers](/index.php/Systemd/Timers "Systemd/Timers").

## Journal

*systemd* has its own logging system called the journal; therefore, running a syslog daemon is no longer required. To read the log, use:

```
# journalctl

```

In Arch Linux, the directory `/var/log/journal/` is a part of the [systemd](https://www.archlinux.org/packages/?name=systemd) package, and the journal (when `Storage=` is set to `auto` in `/etc/systemd/journald.conf`) will write to `/var/log/journal/`. If you or some program delete that directory, systemd will **not** recreate it automatically; however, it will be recreated during the next update of the systemd package. Until then, logs will be written to `/run/systemd/journal`, and logs will be lost on reboot.

**Tip:** If `/var/log/journal/` resides in a [btrfs](/index.php/Btrfs "Btrfs") file system, you should consider disabling Copy-on-Write for the directory. See the main article for details: [Btrfs#Copy-on-Write (CoW)](/index.php/Btrfs#Copy-on-Write_.28CoW.29 "Btrfs").

### Filtering output

*journalctl* allows you to filter the output by specific fields. Be aware that if there are many messages to display or filtering of large time span has to be done, the output of this command can be delayed for quite some time.

Examples:

Show all messages from this boot:

```
# journalctl -b

```

However, often one is interested in messages not from the current, but from the previous boot (e.g. if an unrecoverable system crash happened). This is possible through optional offset parameter of the `-b` flag: `journalctl -b -0` shows messages from the current boot, `journalctl -b -1` from the previous boot, `journalctl -b -2` from the second previous and so on. See `man 1 journalctl` for full description, the semantics is much more powerful.

Follow new messages:

```
# journalctl -f

```

Show all messages by a specific executable:

```
# journalctl /usr/lib/systemd/systemd

```

Show all messages by a specific process:

```
# journalctl _PID=1

```

Show all messages by a specific unit:

```
# journalctl -u netcfg

```

Show kernel ring buffer:

```
# journalctl _TRANSPORT=kernel

```

See `man 1 journalctl`, `man 7 systemd.journal-fields`, or Lennert's [blog post](http://0pointer.de/blog/projects/journalctl.html) for details.

### Journal size limit

If the journal is persistent (non-volatile), its size limit is set to a default value of 10% of the size of the respective file system. For example, with `/var/log/journal` located on a 50 GiB root partition this would lead to 5 GiB of journal data. The maximum size of the persistent journal can be controlled by `SystemMaxUse` in `/etc/systemd/journald.conf`, so to limit it for example to 50 MiB uncomment and edit the corresponding line to:

```
SystemMaxUse=50M

```

Refer to `man journald.conf` for more info.

### Journald in conjunction with syslog

Compatibility with classic syslog implementations is provided via a socket `/run/systemd/journal/syslog`, to which all messages are forwarded. To make the syslog daemon work with the journal, it has to bind to this socket instead of `/dev/log` ([official announcement](http://lwn.net/Articles/474968/)). The [syslog-ng](https://www.archlinux.org/packages/?name=syslog-ng) package in the repositories automatically provides the necessary configuration.

```
# systemctl enable syslog-ng

```

A good *journalctl* tutorial is [here](http://0pointer.de/blog/projects/journalctl.html).

### Forward journald to /dev/tty12

In `/etc/systemd/journald.conf` enable the following:

```
ForwardToConsole=yes
TTYPath=/dev/tty12
MaxLevelConsole=info

```

Restart journald with `sudo systemctl restart systemd-journald`.

## Troubleshooting

### Investigating systemd errors

As an example, we will investigate an error with `systemd-modules-load` service:

**1.** Lets find the systemd services which fail to start:

 `$ systemctl --state=failed`  `systemd-modules-load.service   loaded **failed failed**  Load Kernel Modules` 

**2.** Ok, we found a problem with `systemd-modules-load` service. We want to know more:

 `$ systemctl status systemd-modules-load` 
```
systemd-modules-load.service - Load Kernel Modules
   Loaded: loaded (/usr/lib/systemd/system/systemd-modules-load.service; static)
   Active: **failed** (Result: exit-code) since So 2013-08-25 11:48:13 CEST; 32s ago
     Docs: man:systemd-modules-load.service(8).
           man:modules-load.d(5)
  Process: **15630** ExecStart=/usr/lib/systemd/systemd-modules-load (**code=exited, status=1/FAILURE**)
```

If the `Process ID` is not listed, just restart the failed service with `systemctl restart systemd-modules-load`

**3.** Now we have the process id (PID) to investigate this error in depth. Enter the following command with the current `Process ID` (here: 15630):

 `$ journalctl -b _PID=15630` 
```
-- Logs begin at Sa 2013-05-25 10:31:12 CEST, end at So 2013-08-25 11:51:17 CEST. --
Aug 25 11:48:13 mypc systemd-modules-load[15630]: **Failed to find module 'blacklist usblp'**
Aug 25 11:48:13 mypc systemd-modules-load[15630]: **Failed to find module 'install usblp /bin/false'**
```

**4.** We see that some of the kernel module configs have wrong settings. Therefore we have a look at these settings in `/etc/modules-load.d/`:

 `$ ls -Al /etc/modules-load.d/` 
```
...
-rw-r--r--   1 root root    79  1\. Dez 2012  blacklist.conf
-rw-r--r--   1 root root     1  2\. Mär 14:30 encrypt.conf
-rw-r--r--   1 root root     3  5\. Dez 2012  printing.conf
-rw-r--r--   1 root root     6 14\. Jul 11:01 realtek.conf
-rw-r--r--   1 root root    65  2\. Jun 23:01 virtualbox.conf
...

```

**5.** The `Failed to find module 'blacklist usblp'` error message might be related to a wrong setting inside of `blacklist.conf`. Lets deactivate it with inserting a trailing **#** before each option we found via step 3:

 `/etc/modules-load.d/blacklist.conf` 
```
**#** blacklist usblp
**#** install usblp /bin/false

```

**6.** Now, try to start `systemd-modules-load`:

```
$ systemctl start systemd-modules-load.service

```

If it was successful, this shouldn't prompt anything. If you see any error, go back to step 3\. and use the new PID for solving the errors left.

If everything is ok, you can verify that the service was started successfully with:

 `$ systemctl status systemd-modules-load` 
```
systemd-modules-load.service - Load Kernel Modules
   Loaded: **loaded** (/usr/lib/systemd/system/systemd-modules-load.service; static)
   Active: **active (exited)** since So 2013-08-25 12:22:31 CEST; 34s ago
     Docs: man:systemd-modules-load.service(8)
           man:modules-load.d(5)
 Process: 19005 ExecStart=/usr/lib/systemd/systemd-modules-load (code=exited, status=0/SUCCESS)
Aug 25 12:22:31 mypc systemd[1]: **Started Load Kernel Modules**.
```

Often you can solve these kind of problems like shown above. For further investigation look at [Diagnosing boot problems](#Diagnosing_boot_problems).

### Diagnosing boot problems

Boot with these parameters on the kernel command line: `systemd.log_level=debug systemd.log_target=kmsg log_buf_len=1M`

[More Debugging Information](http://freedesktop.org/wiki/Software/systemd/Debugging)

### Shutdown/reboot takes terribly long

If the shutdown process takes a very long time (or seems to freeze) most likely a service not exiting is to blame. *systemd* waits some time for each service to exit before trying to kill it. To find out if you are affected, see [this article](http://freedesktop.org/wiki/Software/systemd/Debugging/#shutdowncompleteseventually).

### Short lived processes do not seem to log any output

If `journalctl -u foounit` does not show any output for a short lived service, look at the PID instead. For example, if `systemd-modules-load.service` fails, and `systemctl status systemd-modules-load` shows that it ran as PID 123, then you might be able to see output in the journal for that PID, i.e. `journalctl -b _PID=123`. Metadata fields for the journal such as _SYSTEMD_UNIT and _COMM are collected asynchronously and rely on the `/proc` directory for the process existing. Fixing this requires fixing the kernel to provide this data via a socket connection, similar to SCM_CREDENTIALS.

### Disabling application crash dumps journaling

Run the following in order to overwrite the settings from `/lib/sysctl.d/`:

```
# ln -s /dev/null /etc/sysctl.d/50-coredump.conf
# sysctl kernel.core_pattern=core

```

This will disable logging of coredumps to the journal.

Note that the default RLIMIT_CORE of 0 means that no core files are written, either. If you want them, you also need to "unlimit" the core file size in the shell:

```
$ ulimit -c unlimited

```

See [sysctl.d](http://www.freedesktop.org/software/systemd/man/sysctl.d.html) and [the documentation for /proc/sys/kernel](https://www.kernel.org/doc/Documentation/sysctl/kernel.txt) for more information.

### Error message on reboot or shutdown

#### cgroup : option or name mismatch, new: 0x0 "", old: 0x4 "systemd"

See [this thread](https://bbs.archlinux.org/viewtopic.php?pid=1372562#p1372562) for an explanation.

#### watchdog watchdog0: watchdog did not stop!

See [this thread](https://bbs.archlinux.org/viewtopic.php?pid=1372562#p1372562) for an explanation.

## See also

*   [Official web site](http://www.freedesktop.org/wiki/Software/systemd)
*   [Wikipedia article](https://en.wikipedia.org/wiki/systemd "wikipedia:systemd")
*   [Manual pages](http://0pointer.de/public/systemd-man/)
*   [systemd optimizations](http://freedesktop.org/wiki/Software/systemd/Optimizations)
*   [FAQ](http://www.freedesktop.org/wiki/Software/systemd/FrequentlyAskedQuestions)
*   [Tips and tricks](http://www.freedesktop.org/wiki/Software/systemd/TipsAndTricks)
*   [systemd for Administrators (PDF)](http://0pointer.de/public/systemd-ebook-psankar.pdf)
*   [About systemd on Fedora Project](http://fedoraproject.org/wiki/Systemd)
*   [How to debug systemd problems](http://fedoraproject.org/wiki/How_to_debug_Systemd_problems)
*   [Two](http://www.h-online.com/open/features/Control-Centre-The-systemd-Linux-init-system-1565543.html) [part](http://www.h-online.com/open/features/Booting-up-Tools-and-tips-for-systemd-1570630.html) introductory article in *The H Open* magazine.
*   [Lennart's blog story](http://0pointer.de/blog/projects/systemd.html)
*   [Status update](http://0pointer.de/blog/projects/systemd-update.html)
*   [Status update2](http://0pointer.de/blog/projects/systemd-update-2.html)
*   [Status update3](http://0pointer.de/blog/projects/systemd-update-3.html)
*   [Most recent summary](http://0pointer.de/blog/projects/why.html)
*   [Fedora's SysVinit to systemd cheatsheet](http://fedoraproject.org/wiki/SysVinit_to_Systemd_Cheatsheet)
*   [Configuring systemd to allow normal users to shutdown](/index.php/Allow_users_to_shutdown "Allow users to shutdown")