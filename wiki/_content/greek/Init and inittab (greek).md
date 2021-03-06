Η διεργασία **init** είναι η πρώτη διεργασία που εκτελείται μόλις ολοκληρωθεί η φόρτωση του πυρήνα Linux. Το προκαθορισμένο πρόγραμμα init που χρησιμοποιεί το Arch είναι το `/sbin/init` και παρέχεται απο το [sysvinit](https://aur.archlinux.org/packages/sysvinit/). Η λέξη **init** εφεξής θα αναφέρεται στο sysvinit για το παρόν άρθρο.

Το **inittab** είναι το αρχείο ρυθμίσεων εκκίνησης για το init και βρίσκεται στον κατάλογο /etc. Περιέχει οδηγίες για την διεργασία init σχετικές με το ποιά προγράμματα και δέσμες εντολών θα πρέπει να εκτελεστούν κατα την είσοδο σε ένα συγκεκριμένο "επίπεδο εκκίνησης" (runlevel).

**Tip:** Δείτε το `man 5 inittab` και το `man 8 init` για μια πιο επίσημη και πληρέστερη περιγραφή.

**Tip:** Παρόλο που το Arch χρησιμοποιεί το init, Ο περισσότερος φόρτος εργασίας επιτελείται απο τα [#Main Boot Scripts](#Main_Boot_Scripts). Το παρόν άρθρο επικεντρώνεται στα init και inittab; αν ενδιαφέρεστε για μια επισκόπηση της διαδικασίας εκκίνησης του Arch's, δείτε το [Arch boot process](/index.php/Arch_boot_process "Arch boot process").

## Contents

*   [1 Επισκόπηση των init και inittab](#.CE.95.CF.80.CE.B9.CF.83.CE.BA.CF.8C.CF.80.CE.B7.CF.83.CE.B7_.CF.84.CF.89.CE.BD_init_.CE.BA.CE.B1.CE.B9_inittab)
*   [2 Αλλάζοντας runlevel](#.CE.91.CE.BB.CE.BB.CE.AC.CE.B6.CE.BF.CE.BD.CF.84.CE.B1.CF.82_runlevel)
    *   [2.1 Μέσω GRUB](#.CE.9C.CE.AD.CF.83.CF.89_GRUB)
    *   [2.2 Μετά την εκκίνηση](#.CE.9C.CE.B5.CF.84.CE.AC_.CF.84.CE.B7.CE.BD_.CE.B5.CE.BA.CE.BA.CE.AF.CE.BD.CE.B7.CF.83.CE.B7)
*   [3 inittab](#inittab)
    *   [3.1 Προκαθορισμένο Runlevel](#.CE.A0.CF.81.CE.BF.CE.BA.CE.B1.CE.B8.CE.BF.CF.81.CE.B9.CF.83.CE.BC.CE.AD.CE.BD.CE.BF_Runlevel)
    *   [3.2 Κύριες Δέσμες Εντολών Εκκίνησης](#.CE.9A.CF.8D.CF.81.CE.B9.CE.B5.CF.82_.CE.94.CE.AD.CF.83.CE.BC.CE.B5.CF.82_.CE.95.CE.BD.CF.84.CE.BF.CE.BB.CF.8E.CE.BD_.CE.95.CE.BA.CE.BA.CE.AF.CE.BD.CE.B7.CF.83.CE.B7.CF.82)
    *   [3.3 Εκκίνηση με έναν Χρήστη](#.CE.95.CE.BA.CE.BA.CE.AF.CE.BD.CE.B7.CF.83.CE.B7_.CE.BC.CE.B5_.CE.AD.CE.BD.CE.B1.CE.BD_.CE.A7.CF.81.CE.AE.CF.83.CF.84.CE.B7)
    *   [3.4 Gettys και Είσοδος στο σύστημα](#Gettys_.CE.BA.CE.B1.CE.B9_.CE.95.CE.AF.CF.83.CE.BF.CE.B4.CE.BF.CF.82_.CF.83.CF.84.CE.BF_.CF.83.CF.8D.CF.83.CF.84.CE.B7.CE.BC.CE.B1)
    *   [3.5 Ctrl+Alt+Del](#Ctrl.2BAlt.2BDel)
    *   [3.6 Προγράμματα X](#.CE.A0.CF.81.CE.BF.CE.B3.CF.81.CE.AC.CE.BC.CE.BC.CE.B1.CF.84.CE.B1_X)
    *   [3.7 Δέσμες ενεργειών Ανίχνευσης Ισχύος](#.CE.94.CE.AD.CF.83.CE.BC.CE.B5.CF.82_.CE.B5.CE.BD.CE.B5.CF.81.CE.B3.CE.B5.CE.B9.CF.8E.CE.BD_.CE.91.CE.BD.CE.AF.CF.87.CE.BD.CE.B5.CF.85.CF.83.CE.B7.CF.82_.CE.99.CF.83.CF.87.CF.8D.CE.BF.CF.82)
    *   [3.8 Προσαρμοσμένο Αίτημα πληκτρολογίου](#.CE.A0.CF.81.CE.BF.CF.83.CE.B1.CF.81.CE.BC.CE.BF.CF.83.CE.BC.CE.AD.CE.BD.CE.BF_.CE.91.CE.AF.CF.84.CE.B7.CE.BC.CE.B1_.CF.80.CE.BB.CE.B7.CE.BA.CF.84.CF.81.CE.BF.CE.BB.CE.BF.CE.B3.CE.AF.CE.BF.CF.85)
        *   [3.8.1 Ενεργοποίηση του αιτήματος πληκρολογίου](#.CE.95.CE.BD.CE.B5.CF.81.CE.B3.CE.BF.CF.80.CE.BF.CE.AF.CE.B7.CF.83.CE.B7_.CF.84.CE.BF.CF.85_.CE.B1.CE.B9.CF.84.CE.AE.CE.BC.CE.B1.CF.84.CE.BF.CF.82_.CF.80.CE.BB.CE.B7.CE.BA.CF.81.CE.BF.CE.BB.CE.BF.CE.B3.CE.AF.CE.BF.CF.85)
*   [4 See also](#See_also)
*   [5 External Links](#External_Links)

## Επισκόπηση των init και inittab

Το init είναι πάντα η διεργασία με αναγνωριστικό αριθμό 1 και, πέρα απο την διαχείριση κάποιου χώρου swap, είναι η γονική διεργασία **όλων** των άλλων διεργασιών. Μπορείτε να πάρετε μια ιδέα σχετικά με το που είναι η θέση της διεργασίας init στην ιεραρχία των διεργασιών του συστηματός σας χρησιμοποιώντας το `pstree`:

 `$ pstree -Ap` 
```
init(1)-+-acpid(3432)
        |-crond(3423)
        |-dbus-daemon(3469)
        |-gpm(3485)
        |-mylogin(3536)
        |-ngetty(3535)---login(3954)---zsh(4043)---pstree(4326)
        |-polkitd(4033)---{polkitd}(4035)
        |-syslog-ng(3413)---syslog-ng(3414)
        `-udevd(643)-+-udevd(3194)
                     `-udevd(3218)

```

Εκτός της συνήθους αρχικοποίησης του συστήματος (όπως υποδηλώνει το όνομα του), το init χειρίζεται επίσης την επανεκκίνηση, τον τερματισμό και την εκκίνηση σε λειτουργία ανάκτησης (κατάσταση ενός χρήστη). Για να υποστηρίξει τα παραπάνω, το inittab ομαδοποιεί τις καταχωρήσεις σε διαφορετικά **επίπεδα εκκίνησης** (runlevels). τα επίπεδα εκκίνησης που χρησιμοποιεί το Arch είναι 0 για τερματισμό, 1 (με προσονύμιο το S) για κατάσταση ενός χρήστη, 3 για κανονική εκκίνηση (κατάσταση πολλών χρηστών), 5 για X (παραθυρικό περιβάλλον X) και 6 για επανεκκίνηση. Άλλες διανομές μπορεί να υιοθετούν άλλες συμβάσεις, αλλά η σημασία των 0, 1 και 6 είναι καθολική.

Κατα την εκτελεσή του, το init σαρώνει το inittab και εκτελέι τις κατάλληλες ενέργειες. Μια καταχώρηση στο inittab έχει την μορφή

```
id:runlevels:action:process

```

Όπου το `id` είναι το μοναδικό αναγνωριστικό της καταχώρησης (απλά ένα όνομα, δεν έχει ουσιαστικό αντικτυπο στο init), και το `runlevels` είναι ένα (μη οριοθετημένο) αλφαριθμητικό το οποίο περιέχει τα runlevels. Εαν το runlevel στο οποίο εισέρχεται το init εμφανίζεται στο `runlevels`, το `action` διεκπεραιώνεται, εκτελώντας την `process` αν κριθεί σκόπιμο. κάποιες ειδικές `action` θα είχαν ως αποτέλεσμα το init να αγνοήσει τα `runlevels` και να υιοθετήσει μια ειδική αντίστοιχη μέθοδο. Περισσότερη επεξήγηση ακολουθεί στο επόμενο τμήμα.

## Αλλάζοντας runlevel

### Μέσω GRUB

Για να αλλάξετε το runlevel στο οποίο εκκινεί το σύστημα, απλά προσθέστε τον αναγνωριστικό αριθμό του εκάστοτε runlevel `n` στην γραμμή ορισμού πυρήνα (kernel) του GRUB. Μια συνήθης εφαρμογή της τεχνικής αυτής είναι [Start X at login#/etc/inittab](/index.php/Start_X_at_login#.2Fetc.2Finittab "Start X at login"). Στο αρχείο `/boot/grub/menu.lst` βρείτε το τμήμα που αναφέρεται στο Arch (το προκαθορισμένο είναι '# (0) Arch Linux'):

```
# (0)  Arch Linux
title  Arch Linux
root   (hd0,0)
kernel /vmlinuz-linux root=/dev/sda3 ro
initrd /initramfs-linux.img

```

Για εκκίνιση στο runlevel 3, αλλάξτε την γραμμή kernel σε

```
kernel /vmlinuz-linux root=/dev/sda3 ro **3**

```

Για εκκίνιση στο runlevel 5, αλλάξτε την γραμμή kernel σε

```
kernel /vmlinuz-linux root=/dev/sda3 ro **5**

```

Το run-level προστέθηκε στο τέλος ώστε να γνωρίζει το kernel σε ποιό run-level να εκκινήσει το σύστημα. Για να χρησιμοποιήσετε κάποιο άλλο πρόγραμμα init (π.χ. [systemd](/index.php/Systemd "Systemd")), προσθέστε το **init=/bin/systemd** η κάτι ανάλογο στην γραμμή kernel.

**Note:** Αν χρησιμοποιήσετε κάποιο άλλο προγραμμα init διαφορετικό απο το sysvinit, η παράμετρος runlevel μπορεί να αγνοηθεί.

### Μετά την εκκίνηση

Αφού το σύστημα έχει εκκινήσει, μπορείτε να εισάγετε την εντολή `telinit n` ώστε να ζητήσετε το init να αλλάξει το runlevel στο `n`. Τότε το init διαβάζει το inittab και "διαφοροποιεί" το runlevel n και το τρέχον runlevel - τερματίζοντας τις διεργασίες που δεν εμφανίζονται στο νέο runlevel διεκπεραιώνοντας τις ενέργειες οι οποίες δεν εμφανίζονται στο "παλαιό" runlevel. Οι διεργασίες που εμφανίζονται και στα δύο runlevels μένουν ανέπαφες. Οι διαδικασία τερματισμού είναι στην πραγματικότητα λίγο πολύπλοκη, σε αυτό το σημείο, πρέπει να σημειωθεί οτι τεχνικές λεπτομέρειες μπορούν να βρεθούν στο εγχειρίδιο (manpage) του init.

Το init δεν παρακολουθεί το inittab. Θα πρέπει να καλέσετε ρητά το `telinit` ώστε να εφαρμοστούν οποιεσδήποτε παραμετροποιήσεις στο. Η εντολή `telinit q` έχει σαν αποτέλεσμα την επανεξέταση του inittab απο το init αλλά όχι την αλλαγή runlevel.

## inittab

Σε αυτό το τμήμα εξετάζουμε συνήθεις καταχωρήσεις στο inittab, ακολουθώντας την ίδια σειρά με την οποία εμφανίζονται στο προκαθορισμένο inittab που χρησιμοποιείται από το Arch. Αμέσως μετά υπάρχουν λίγα παραδείγματα ώστε να σας βοηθήσουν να δημιουργήσετε την δική σας καταχώρηση στο inittab.

**Warning:** Πάντα ελέγξτε ένα παραμετροποιημένο `/etc/inittab` με την εντολή `telinit q` πρίν επανεκκινήσετε το σύστημα, ειδάλλως ένα μικρό συντακτικό λάθος μπορεί να εμποδίσει την εκκίνηση του συστήματος σας.

### Προκαθορισμένο Runlevel

Το προκαθορισμένο runlevel είναι το 3\. Αποσχολιάστε ή αν προτιμάτε προσθέστε τα ακόλουθα για να εκκινήσετε το σύστημα στο runlevel 5 (το οποίο χρησιμοποιείται για το παραθυρικό περιβάλλον X κατα σύμβαση) εκ προοιμίου:

```
id:5:initdefault:

```

### Κύριες Δέσμες Εντολών Εκκίνησης

Τα ακόλουθα αποτελούν τις κύριες δέσμες εντολών εκκίνησης του Arch.

```
rc::sysinit:/etc/rc.sysinit
rs:S1:wait:/etc/rc.single
rm:2345:wait:/etc/rc.multi
rh:06:wait:/etc/rc.shutdown

```

### Εκκίνηση με έναν Χρήστη

Μερικές φορές ο πυρήνας μπορεί να μην καταφέρει να εκκινήσει εντελώς, λόγω ενός μη συνεπούς ως προς τα δεδομένα ή κατεστραμμένου σκληρου δίσκου ή συστήματος αρχείων, ελλειπή ή κατεστραμμένα αρχεία ζωτικής σημασίας, κ.τ.λ.. Σε αυτήν την περίπτωση η εικόνα init σας μπορεί να μπεί αυτομάτως σε κατάσταση **ενός χρήστη** η οποία επιτρέπει την είσοδο στο σύστημα μόνο του χρήστη root και κάνει χρήση του `/sbin/sulogin` αντί του `/sbin/login` ώστε να ελέγξει την διεργασία εισόδου. Μπορείτε επίσης να εκκίνήσετε σε κάσταση ενός χρήστη προσθέτοντας το γράμμα `S` στην γραμμή ορισμού πυρήνα των ρυθμίσεων του [GRUB](/index.php/GRUB "GRUB"), [LILO](/index.php/LILO "LILO"), ή [syslinux](/index.php/Syslinux "Syslinux"). Εάν επιθυμείτε να εκτελεστεί κάτι άλλο αντί του sulogin, ορίστε το εδώ.

```
su:S:wait:/sbin/sulogin -p

```

### Gettys και Είσοδος στο σύστημα

Υπάρχουν καταχωρήσεις ζωτικής σημασίας που εκτελούν τα [gettys](/index.php/Getty "Getty") στα τερματικά σας. Τα περισσότερα σύνολα προκαθορισμένων ρυθμίσεων που θα συναντήσετε θα ορίζουν την εκτέλεση αρκετών gettys στα ttys1-6 τα οποία συνιστούν οτιδήποτε εμφανίζεται στην οθόνη σας κατά την προτροπή εισόδου. Επίσης δείτε τα openvt, chvt, stty, και ioctl.

```
c1:234:respawn:/sbin/agetty 9600 tty1 xterm-color
c5:5:respawn:/sbin/agetty 57600 tty2 xterm-256color

```

### Ctrl+Alt+Del

Όταν μια ειδική ακολουθία πλήκτρων `Ctrl+Alt+Del` πατηθεί, η παρακάτω καταχώρηση ορίζει τι θα συμβεί.

```
ca::ctrlaltdel:/sbin/shutdown -t3 -r now

```

### Προγράμματα X

Εάν δεν φοβάστε την αποσφαλμάτωση(debug), μπορείτε να κατανοήσετε πώς να εκκινήσετε όλων των ειδών τα προγράμματα μέσω του inittab. Ένα χρήσιμο είδος προγράμματος είναι η εκκίνηση του διαχειριστή εισόδου σας όταν το runlevel είναι το 5, κατάσταση πολλών χρηστών x. Στο ακόλουθο παράδειγμα μπορείτε να δείτε πώς να εκκινήσετε το [SLiM](/index.php/SLiM "SLiM") κατά την είσοδο στο runlevel 5.

```
x:5:respawn:/usr/bin/slim >/dev/null 2>&1
#x:5:respawn:/usr/bin/xdm -nodaemon -confi /etc/X11/xdm/archlinux/xdm-config

```

### Δέσμες ενεργειών Ανίχνευσης Ισχύος

Το Init μπορεί να επικοινωνήσει με την συσκευή UPS σας και να εκτελέσει διεργασίες βάσει της κατάστασης του. Ακολουθούν κάποια παραδείγματα:

```
pf::powerfail:/sbin/shutdown -f -h +2 "Power Failure; System Shutting Down"
pr:12345:powerokwait:/sbin/shutdown -c "Power Restored; Shutdown Cancelled"

```

### Προσαρμοσμένο Αίτημα πληκτρολογίου

Η ακόλυθη γραμμή προσθέτει μια προσαρμοσμένη λειτουργία η οποία εκτελείτε με το πάτημα μιας ακολουθίας πλήκτρων. Μπορείτε να τροποποιήσετε αυτήν την ακολουθία πλήκτρων ωστε να είναι οποιαδήποτε εσείς επιθυμείτε, παρόμια με την `Ctrl+Alt+Del`.

```
kb::kbrequest:/usr/bin/wall "Keyboard Request -- edit /etc/inittab to customize"

```

#### Ενεργοποίηση του αιτήματος πληκρολογίου

Μπορείτε να ενεργοποιήσετε την ειδική ακολουθία πλήκτρων **kbrequest** στέλνοντας το σήμα WINCH στην διεργασία init (1) ως root (μέσω sudo). Σε αυτό το παράδειγμα, η εντολή:

```
kill -WINCH 1

```

έχει ως αποτέλεσμα η διεργασία `wall` να γράψει σε όλα τα ttys:

```
Broadcast message from root@askapachehost (console) (Wed Oct 27 14:02:26 2010):  
Keyboard Request -- edit /etc/inittab to customize

```

## See also

*   [Automatic login to virtual console](/index.php/Automatic_login_to_virtual_console "Automatic login to virtual console")
*   [Disable clearing of boot messages](/index.php/Disable_clearing_of_boot_messages "Disable clearing of boot messages")
*   [Start X at login](/index.php/Start_X_at_login "Start X at login")
*   [xinitrc](/index.php/Xinitrc "Xinitrc")
*   [Display manager](/index.php/Display_manager "Display manager")
*   [SLiM](/index.php/SLiM "SLiM")

## External Links

*   [Wikipedia: Init](https://en.wikipedia.org/wiki/Init "wikipedia:Init")
*   [Γνωσιακή Βάση Linux και Οδηγός. Run Levels.](http://www.linux-tutorial.info/modules.php?name=MContent&pageid=65)
*   [Linux.com. Εισαγωγή στα runlevels και το inittab](http://www.linux.com/articles/114107)
*   [Linux.com. Μια εισαγωγή στις υπηρεσίες, τα runlevels, και τις δέσμες εντολών rc.d.](http://www.linux.com/news/enterprise/systems-management/8116-an-introduction-to-services-runlevels-and-rcd-scripts)