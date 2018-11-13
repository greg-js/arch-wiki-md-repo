Το παρόν άρθρο θα σας οδηγήσει στην διαδικασία εγκατάστασης του [Arch Linux](/index.php/Arch_Linux "Arch Linux") χρησιμοποιώντας τα [Arch Install Scripts](https://github.com/falconindy/arch-install-scripts). Πριν την εγκατάσταση, προτείνεται να συμβουλευτείτε το [FAQ](/index.php/FAQ "FAQ").

Το [Arch wiki](/index.php/Main_page "Main page") το οποίο διατηρείται από την κοινότητα είναι μία πολύ καλή πηγή και θα πρέπει να είναι το πρώτο που συμβουλεύεστε. Το κανάλι στο [IRC](https://en.wikipedia.org/wiki/IRC "wikipedia:IRC") ([irc://irc.freenode.net/#archlinux](irc://irc.freenode.net/#archlinux)), και τα [forums](https://bbs.archlinux.org/) είναι επίσης διαθέσιμα αν η απάντηση δεν μπορεί να βρεθεί αλλού. Επίσης, καλό είναι να βλέπετε και τις `man` σελίδες για όποια εντολή δεν ξέρετε καλά· αυτό μπορεί να γίνει καλώντας την `man *εντολή*`.

## Contents

*   [1 Λήψη](#Λήψη)
*   [2 Γλώσσα πληκτρολογίου](#Γλώσσα_πληκτρολογίου)
*   [3 Χώρισμα (Partition) δίσκων](#Χώρισμα_(Partition)_δίσκων)
*   [4 Διαμόρφωση των partitions](#Διαμόρφωση_των_partitions)
*   [5 Προσάρτηση των partitions](#Προσάρτηση_των_partitions)
*   [6 Σύνδεση στο internet](#Σύνδεση_στο_internet)
    *   [6.1 Ασύρματο](#Ασύρματο)
*   [7 Εγκατάσταση βασικού συστήματος](#Εγκατάσταση_βασικού_συστήματος)
*   [8 Εγκατάσταση του bootloader](#Εγκατάσταση_του_bootloader)
    *   [8.1 GRUB](#GRUB)
    *   [8.2 Syslinux](#Syslinux)
*   [9 Διαμόρφωση συστήματος](#Διαμόρφωση_συστήματος)
*   [10 Αποπροσάρτηση των partitions και επανεκκίνηση](#Αποπροσάρτηση_των_partitions_και_επανεκκίνηση)
*   [11 Διαμόρφωση του pacman](#Διαμόρφωση_του_pacman)
*   [12 Ενημέρωση συστήματος](#Ενημέρωση_συστήματος)
*   [13 Προσθήκη χρήστη](#Προσθήκη_χρήστη)

## Λήψη

Κατεβάστε το νέο Arch Linux ISO από τη [σελίδα λήψης](https://www.archlinux.org/download/).

*   Παρέχεται ένα εικονικό αρχείο, το οποίο μπορεί να εκκινήσει σε ένα i686 και x86_64 live σύστημα για την εγκατάσταση του Arch Linux μέσω του διαδικτύου. Μέσα τα οποία περιέχουν το [core] αποθετήριο πλέον δεν παρέχονται.
*   Τα εικονικά αρχεία είναι υπογεγραμμένα και προτείνεται να πιστοποιήσετε την υπογραφή τους πριν τη χρήση. Στο Arch Linux, αυτό μπορεί να γίνει χρησιμοποιώντας `pacman-key -v <iso-file>.sig` 
*   Το εικονικό αρχίο μπορεί να καεί σε ένα CD, να προσαρτηθεί σαν ένα αρχείο ISO, ή να γραφτεί κατ' ευθείαν σε ένα USB stick χρησιμοποιώντας την `dd`. Προορίζεται μόνο για νέες εγκαταστάσεις· ένα ήδη υπάρχον σύστημα Arch Linux μπορεί πάντα να ενημερωθεί με `pacman -Syu`.

## Γλώσσα πληκτρολογίου

Για πολλές χώρες και τύπους πληκτρολογίων τα κατάλληλα keymaps είναι ήδη διαθέσιμα, και μία εντολή όπως η `loadkeys uk` μπορεί να κάνει αυτό που θέλετε. Περισσότερα διαθέσιμα αρχεία keymap μπορούν να βρεθούν στο `/usr/share/kbd/keymaps/` (μπορείτε να παραλέιψετε το μονοπάτι του keymap και την κατάληξη όταν χρησιμοποιείτε την εντολή `loadkeys`).

## Χώρισμα (Partition) δίσκων

Δείτε το άρθρο [partitioning](/index.php/Partitioning "Partitioning") για λεπτομέρειες.

Αν θέλετε να δημιουργήσετε μια Στοίβα συσκευών αποθήκευσης (stacked block devices) όπως [LVM](/index.php/LVM "LVM"), [LUKS](/index.php/LUKS "LUKS"), ή [RAID](/index.php/RAID "RAID"), κάντε το τώρα.

## Διαμόρφωση των partitions

Δείτε [εδώ](/index.php/Format_a_device#Step_2:_create_the_new_file_system "Format a device") για λεπτομέρειες.

Αν χρησιμοποιείτε (U)EFI πολυ πιθανόν να χρειαστείτε κάποιο άλλο partition για να φιλοξενηθεί το UEFI System partition. Διαβάστε [αυτό το άρθρο](/index.php/Unified_Extensible_Firmware_Interface#Create_an_UEFI_System_Partition_in_Linux "Unified Extensible Firmware Interface").

## Προσάρτηση των partitions

Τώρα πρέπει να προσαρτήσουμε το root partition στο `/mnt`. Θα πρέπει επίσης να δημιουργήσετε καταλόγους και να προσαρτήσετε όποια άλλα partitions φτιάξετε (`/mnt/boot`, `/mnt/home`, ...) αν θέλετε να εντοπιστούν από το `genfstab`.

## Σύνδεση στο internet

Μία υπηρεσία DHCP είναι ήδη ενεργοποιημένη για όλες τις διαθέσιμες συσκευές. Αν κάποιος χρειάζεται να ορίσει μία στατική IP ή να χρησιμοποιήσει κάποιο εργαλείο όπως το [Netctl](/index.php/Netctl "Netctl"), θα πρέπει να σταματήσει την υπηρεσία dhcp πρώτα: `systemctl stop dhcpcd.service`. Για περισσότερες πληροφορίες επισκεφτείτε το [configuring network](/index.php/Configuring_network "Configuring network").

### Ασύρματο

Τρέξτε `wifi-menu` για να διαμορφώσετε το ασύρματο δίκτυο. Για πληροφορίες δείτε το [Wireless network configuration](/index.php/Wireless_network_configuration "Wireless network configuration") και το [Netctl](/index.php/Netctl "Netctl").

## Εγκατάσταση βασικού συστήματος

Πριν την εγκατάσταση, τροποποιήστε το `/etc/pacman.d/mirrorlist` και αφαιρέστε το σύμβολο `#` μπροστά από τους κοντινούς στην τοποθεσία σας διακομιστές (servers). Αυτό το αντίγραφο της mirrorlist θα εγκατασταθεί στο νέο σας σύστημα από το `pacstrap`, οπότε αξίζει να το φτιάξετε σωστά.

Χρησιμοποιώντας το [pacstrap](https://github.com/falconindy/arch-install-scripts/blob/master/pacstrap.in) script εγκαθιστούμε το βασικό σύστημα. Το group πακέτο `base-devel` παρά το ότι είναι προαιρετικό, θα πρέπει επίσης να εγκατασταθεί αν σχεδιάζετε να μεταγλωττίσετε κάποιο πρόγραμμα από το [AUR](/index.php/AUR "AUR") ή αν χρησιμοποιήσετε το [ABS](/index.php/ABS "ABS").

```
# pacstrap /mnt base base-devel

```

Άλλα πακέτα μπορούν να εγκατασταθούν προσαρτώντας το όνομά τους στην παραπάνω εντολή (χωρισμένα με κενό), περιλαμβανομένου του bootloader αν θέλετε.

## Εγκατάσταση του bootloader

### [GRUB](/index.php/GRUB "GRUB")

*   Για BIOS:

```
# arch-chroot /mnt pacman -S grub-bios

```

*   Για EFI (σε σπάνιες περιπτώσεις θα χρειαστείτε το `grub-efi-i386`):

```
# arch-chroot /mnt pacman -S grub-efi-x86_64

```

*   Εγκατάσταση του GRUB μετά το chrooting (αναφερθείτε στο τμήμα [Διαμόρφωση συστήματος](#Ενημέρωση_συστήματος)).

### [Syslinux](/index.php/Syslinux "Syslinux")

```
# arch-chroot /mnt pacman -S syslinux

```

## Διαμόρφωση συστήματος

Δημιουργήστε το [fstab](/index.php/Fstab "Fstab") με την εξής εντολή (αν προτιμάτε να χρησιμοποιήσετε UUIDs ή labels, προσθέστε την επιλογή `-U` ή `-L`, αντίστοιχα):

```
# genfstab -p /mnt >> /mnt/etc/fstab

```

Έπειτα κάνουμε [chroot](/index.php/Chroot "Chroot") στο νέο μας εγκατεστημένο σύστημα:

```
# arch-chroot /mnt

```

*   Γράψτε το hostname στο `/etc/hostname`.
*   Δημιουργήστε ένα symlink του `/etc/localtime` στο `/usr/share/zoneinfo/Zone/SubZone`. Αντικαταστήστε το `Zone` και το `Subzone` σε αυτό που προτιμάτε. Για παράδειγμα:

```
# ln -s /usr/share/zoneinfo/Europe/Athens /etc/localtime

```

*   Ρυθμίστε τις προτιμήσεις του [locale](/index.php/Locale#Setting_the_system_locale "Locale") στο `/etc/locale.conf`.
*   Προσθέστε τις προτίμήσεις του [console keymap και της γραμματοσειράς](/index.php/KEYMAP "KEYMAP") στο `/etc/vconsole.conf`
*   Αποσχολιάστε το locale που θέλετε να χρησιμοποιήσετε στο `/etc/locale.gen` και δημιουργήστε το με `locale-gen`.
*   Διαμορφώστε το `/etc/mkinitcpio.conf` όπως χρειάζεται (δείτε [mkinitcpio](/index.php/Mkinitcpio "Mkinitcpio")) και δημιουργήστε το initial RAM disk με:

```
# mkinitcpio -p linux

```

*   Διαμορφώστε τον bootloader: αναφερθείτε πίσω στο κατάλληλο άρθρο από το τμήμα εγκατάστασης του bootloader.

*   Ορίστε έναν κωδικό για τον root με την εντολή `passwd`.

## Αποπροσάρτηση των partitions και επανεκκίνηση

Αν είστε ακόμα στο chroot περιβάλλον πληκτρολογήστε `exit` ή πατήστε `Ctrl+D` για να βγείτε. Προηγουμένως είχαμε προσαρτήσει τα partitions στο `/mnt`, σε αυτό το βήμα θα τα αποπροσαρτήσουμε:

```
# umount /mnt/{boot,home,}

```

Τέλος κάντε επανεκκίνηση και συνδεθείτε στο νέο σύστημα με το λογαριασμό root.

## Διαμόρφωση του pacman

Επεξεργαστείτε το `/etc/pacman.conf` και διαμορφώστε τις επιλογές του pacman, ενεργοποιώντας επίσης όσα repositories χρειάζεστε.

Δείτε το [Pacman](/index.php/Pacman "Pacman") και το [Official repositories](/index.php/Official_repositories "Official repositories") για λεπτομέρειες.

## Ενημέρωση συστήματος

Σε αυτό το σημείο πρέπει να ενημερώσετε το σύστημά σας.

Δείτε το [Upgrading packages](/index.php/Pacman#Upgrading_packages "Pacman") για οδηγίες.

## Προσθήκη χρήστη

Τέλος, προσθέστε έναν κανονικό χρήστη όπως περιγράφεται στο [User management](/index.php/Users_and_groups#User_management "Users and groups").