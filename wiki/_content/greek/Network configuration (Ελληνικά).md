Αυτή η σελίδα εξηγεί πως θα δημιουργήσετε μια **ενσύρματη** σύνδεση σε ένα δίκτυο. Αν θέλετε να δημιουργήσετε **ασύρματη** σύνδεση δείτε το [Wireless Setup](/index.php/Wireless_Setup_(%CE%95%CE%BB%CE%BB%CE%B7%CE%BD%CE%B9%CE%BA%CE%AC) "Wireless Setup (Ελληνικά)")

## Contents

*   [1 Έλεγχος σύνδεσης](#.CE.88.CE.BB.CE.B5.CE.B3.CF.87.CE.BF.CF.82_.CF.83.CF.8D.CE.BD.CE.B4.CE.B5.CF.83.CE.B7.CF.82)
*   [2 Ορίστε το όνομα του υπολογιστή σας (hostname)](#.CE.9F.CF.81.CE.AF.CF.83.CF.84.CE.B5_.CF.84.CE.BF_.CF.8C.CE.BD.CE.BF.CE.BC.CE.B1_.CF.84.CE.BF.CF.85_.CF.85.CF.80.CE.BF.CE.BB.CE.BF.CE.B3.CE.B9.CF.83.CF.84.CE.AE_.CF.83.CE.B1.CF.82_.28hostname.29)
*   [3 Οδηγός Συσκευής (Device driver)](#.CE.9F.CE.B4.CE.B7.CE.B3.CF.8C.CF.82_.CE.A3.CF.85.CF.83.CE.BA.CE.B5.CF.85.CE.AE.CF.82_.28Device_driver.29)
    *   [3.1 Έλεγχος κατάστασης συσκευής](#.CE.88.CE.BB.CE.B5.CE.B3.CF.87.CE.BF.CF.82_.CE.BA.CE.B1.CF.84.CE.AC.CF.83.CF.84.CE.B1.CF.83.CE.B7.CF.82_.CF.83.CF.85.CF.83.CE.BA.CE.B5.CF.85.CE.AE.CF.82)
    *   [3.2 Φόρτωση λειτουργικής μονάδας (module)](#.CE.A6.CF.8C.CF.81.CF.84.CF.89.CF.83.CE.B7_.CE.BB.CE.B5.CE.B9.CF.84.CE.BF.CF.85.CF.81.CE.B3.CE.B9.CE.BA.CE.AE.CF.82_.CE.BC.CE.BF.CE.BD.CE.AC.CE.B4.CE.B1.CF.82_.28module.29)
*   [4 Διασυνδέσεις δικτύου](#.CE.94.CE.B9.CE.B1.CF.83.CF.85.CE.BD.CE.B4.CE.AD.CF.83.CE.B5.CE.B9.CF.82_.CE.B4.CE.B9.CE.BA.CF.84.CF.8D.CE.BF.CF.85)
    *   [4.1 Ονομασία συσκευών](#.CE.9F.CE.BD.CE.BF.CE.BC.CE.B1.CF.83.CE.AF.CE.B1_.CF.83.CF.85.CF.83.CE.BA.CE.B5.CF.85.CF.8E.CE.BD)
        *   [4.1.1 Αλλαγή ονόματος συσκευής](#.CE.91.CE.BB.CE.BB.CE.B1.CE.B3.CE.AE_.CE.BF.CE.BD.CF.8C.CE.BC.CE.B1.CF.84.CE.BF.CF.82_.CF.83.CF.85.CF.83.CE.BA.CE.B5.CF.85.CE.AE.CF.82)
    *   [4.2 Ορισμός της μονάδας μέγιστης μετάδοσης (MTU) και μεγέθους ουράς (queue Length)](#.CE.9F.CF.81.CE.B9.CF.83.CE.BC.CF.8C.CF.82_.CF.84.CE.B7.CF.82_.CE.BC.CE.BF.CE.BD.CE.AC.CE.B4.CE.B1.CF.82_.CE.BC.CE.AD.CE.B3.CE.B9.CF.83.CF.84.CE.B7.CF.82_.CE.BC.CE.B5.CF.84.CE.AC.CE.B4.CE.BF.CF.83.CE.B7.CF.82_.28MTU.29_.CE.BA.CE.B1.CE.B9_.CE.BC.CE.B5.CE.B3.CE.AD.CE.B8.CE.BF.CF.85.CF.82_.CE.BF.CF.85.CF.81.CE.AC.CF.82_.28queue_Length.29)
    *   [4.3 Βρείτε τα τρέχοντα ονόματα των συσκευών](#.CE.92.CF.81.CE.B5.CE.AF.CF.84.CE.B5_.CF.84.CE.B1_.CF.84.CF.81.CE.AD.CF.87.CE.BF.CE.BD.CF.84.CE.B1_.CE.BF.CE.BD.CF.8C.CE.BC.CE.B1.CF.84.CE.B1_.CF.84.CF.89.CE.BD_.CF.83.CF.85.CF.83.CE.BA.CE.B5.CF.85.CF.8E.CE.BD)
    *   [4.4 Ενεργοποίηση και απενεργοποίηση συσκευών δικτύου](#.CE.95.CE.BD.CE.B5.CF.81.CE.B3.CE.BF.CF.80.CE.BF.CE.AF.CE.B7.CF.83.CE.B7_.CE.BA.CE.B1.CE.B9_.CE.B1.CF.80.CE.B5.CE.BD.CE.B5.CF.81.CE.B3.CE.BF.CF.80.CE.BF.CE.AF.CE.B7.CF.83.CE.B7_.CF.83.CF.85.CF.83.CE.BA.CE.B5.CF.85.CF.8E.CE.BD_.CE.B4.CE.B9.CE.BA.CF.84.CF.8D.CE.BF.CF.85)
*   [5 Ρύθμιση της διεύθυνσης ip](#.CE.A1.CF.8D.CE.B8.CE.BC.CE.B9.CF.83.CE.B7_.CF.84.CE.B7.CF.82_.CE.B4.CE.B9.CE.B5.CF.8D.CE.B8.CF.85.CE.BD.CF.83.CE.B7.CF.82_ip)
    *   [5.1 Δυναμική διεύθυνση ip](#.CE.94.CF.85.CE.BD.CE.B1.CE.BC.CE.B9.CE.BA.CE.AE_.CE.B4.CE.B9.CE.B5.CF.8D.CE.B8.CF.85.CE.BD.CF.83.CE.B7_ip)
        *   [5.1.1 Χειροκίνητη εκκίνηση DHCP Client Daemon](#.CE.A7.CE.B5.CE.B9.CF.81.CE.BF.CE.BA.CE.AF.CE.BD.CE.B7.CF.84.CE.B7_.CE.B5.CE.BA.CE.BA.CE.AF.CE.BD.CE.B7.CF.83.CE.B7_DHCP_Client_Daemon)
        *   [5.1.2 Ενεργοποίηση DHCP κατά την εκκίνηση](#.CE.95.CE.BD.CE.B5.CF.81.CE.B3.CE.BF.CF.80.CE.BF.CE.AF.CE.B7.CF.83.CE.B7_DHCP_.CE.BA.CE.B1.CF.84.CE.AC_.CF.84.CE.B7.CE.BD_.CE.B5.CE.BA.CE.BA.CE.AF.CE.BD.CE.B7.CF.83.CE.B7)
    *   [5.2 Στατική διεύθυνση ip](#.CE.A3.CF.84.CE.B1.CF.84.CE.B9.CE.BA.CE.AE_.CE.B4.CE.B9.CE.B5.CF.8D.CE.B8.CF.85.CE.BD.CF.83.CE.B7_ip)
        *   [5.2.1 Χειροκίνητη απόδοση στατικής ip](#.CE.A7.CE.B5.CE.B9.CF.81.CE.BF.CE.BA.CE.AF.CE.BD.CE.B7.CF.84.CE.B7_.CE.B1.CF.80.CF.8C.CE.B4.CE.BF.CF.83.CE.B7_.CF.83.CF.84.CE.B1.CF.84.CE.B9.CE.BA.CE.AE.CF.82_ip)
        *   [5.2.2 Χειροκίνητη σύνδεση κατά την εκκίνηση με χρήση του systemd](#.CE.A7.CE.B5.CE.B9.CF.81.CE.BF.CE.BA.CE.AF.CE.BD.CE.B7.CF.84.CE.B7_.CF.83.CF.8D.CE.BD.CE.B4.CE.B5.CF.83.CE.B7_.CE.BA.CE.B1.CF.84.CE.AC_.CF.84.CE.B7.CE.BD_.CE.B5.CE.BA.CE.BA.CE.AF.CE.BD.CE.B7.CF.83.CE.B7_.CE.BC.CE.B5_.CF.87.CF.81.CE.AE.CF.83.CE.B7_.CF.84.CE.BF.CF.85_systemd)
        *   [5.2.3 Υπολογισμός διευθύνσεων](#.CE.A5.CF.80.CE.BF.CE.BB.CE.BF.CE.B3.CE.B9.CF.83.CE.BC.CF.8C.CF.82_.CE.B4.CE.B9.CE.B5.CF.85.CE.B8.CF.8D.CE.BD.CF.83.CE.B5.CF.89.CE.BD)
*   [6 Φόρτωση ρυθμίσεων](#.CE.A6.CF.8C.CF.81.CF.84.CF.89.CF.83.CE.B7_.CF.81.CF.85.CE.B8.CE.BC.CE.AF.CF.83.CE.B5.CF.89.CE.BD)
*   [7 Συμπληρωματικές ρυθμίσεις](#.CE.A3.CF.85.CE.BC.CF.80.CE.BB.CE.B7.CF.81.CF.89.CE.BC.CE.B1.CF.84.CE.B9.CE.BA.CE.AD.CF.82_.CF.81.CF.85.CE.B8.CE.BC.CE.AF.CF.83.CE.B5.CE.B9.CF.82)
    *   [7.1 ifplugd για laptops](#ifplugd_.CE.B3.CE.B9.CE.B1_laptops)
    *   [7.2 Ενσωμάτωση ή Συσσώρευση συνδέσεων (Bonding or LAG)](#.CE.95.CE.BD.CF.83.CF.89.CE.BC.CE.AC.CF.84.CF.89.CF.83.CE.B7_.CE.AE_.CE.A3.CF.85.CF.83.CF.83.CF.8E.CF.81.CE.B5.CF.85.CF.83.CE.B7_.CF.83.CF.85.CE.BD.CE.B4.CE.AD.CF.83.CE.B5.CF.89.CE.BD_.28Bonding_or_LAG.29)
    *   [7.3 IP address aliasing](#IP_address_aliasing)
        *   [7.3.1 Παράδειγμα](#.CE.A0.CE.B1.CF.81.CE.AC.CE.B4.CE.B5.CE.B9.CE.B3.CE.BC.CE.B1)
    *   [7.4 Αλλαγή διεύθυνσης MAC/hardware](#.CE.91.CE.BB.CE.BB.CE.B1.CE.B3.CE.AE_.CE.B4.CE.B9.CE.B5.CF.8D.CE.B8.CF.85.CE.BD.CF.83.CE.B7.CF.82_MAC.2Fhardware)
    *   [7.5 Κοινή χρήση δικτύου (Sharing Internet)](#.CE.9A.CE.BF.CE.B9.CE.BD.CE.AE_.CF.87.CF.81.CE.AE.CF.83.CE.B7_.CE.B4.CE.B9.CE.BA.CF.84.CF.8D.CE.BF.CF.85_.28Sharing_Internet.29)
    *   [7.6 Διαμόρφωση δρομολογητή (Router)](#.CE.94.CE.B9.CE.B1.CE.BC.CF.8C.CF.81.CF.86.CF.89.CF.83.CE.B7_.CE.B4.CF.81.CE.BF.CE.BC.CE.BF.CE.BB.CE.BF.CE.B3.CE.B7.CF.84.CE.AE_.28Router.29)
    *   [7.7 Ανάλυση ονομασίας κεντρικού υπολογιστή δικτύου (Host name resolution)](#.CE.91.CE.BD.CE.AC.CE.BB.CF.85.CF.83.CE.B7_.CE.BF.CE.BD.CE.BF.CE.BC.CE.B1.CF.83.CE.AF.CE.B1.CF.82_.CE.BA.CE.B5.CE.BD.CF.84.CF.81.CE.B9.CE.BA.CE.BF.CF.8D_.CF.85.CF.80.CE.BF.CE.BB.CE.BF.CE.B3.CE.B9.CF.83.CF.84.CE.AE_.CE.B4.CE.B9.CE.BA.CF.84.CF.8D.CE.BF.CF.85_.28Host_name_resolution.29)
*   [8 Αντιμετώπιση προβλημάτων](#.CE.91.CE.BD.CF.84.CE.B9.CE.BC.CE.B5.CF.84.CF.8E.CF.80.CE.B9.CF.83.CE.B7_.CF.80.CF.81.CE.BF.CE.B2.CE.BB.CE.B7.CE.BC.CE.AC.CF.84.CF.89.CE.BD)
    *   [8.1 Εναλλαγή υπολογιστών σε καλωδιακό μόντεμ (cable modem)](#.CE.95.CE.BD.CE.B1.CE.BB.CE.BB.CE.B1.CE.B3.CE.AE_.CF.85.CF.80.CE.BF.CE.BB.CE.BF.CE.B3.CE.B9.CF.83.CF.84.CF.8E.CE.BD_.CF.83.CE.B5_.CE.BA.CE.B1.CE.BB.CF.89.CE.B4.CE.B9.CE.B1.CE.BA.CF.8C_.CE.BC.CF.8C.CE.BD.CF.84.CE.B5.CE.BC_.28cable_modem.29)
    *   [8.2 Το πρόβλημα του εύρους τιμής του TCP](#.CE.A4.CE.BF_.CF.80.CF.81.CF.8C.CE.B2.CE.BB.CE.B7.CE.BC.CE.B1_.CF.84.CE.BF.CF.85_.CE.B5.CF.8D.CF.81.CE.BF.CF.85.CF.82_.CF.84.CE.B9.CE.BC.CE.AE.CF.82_.CF.84.CE.BF.CF.85_TCP)
        *   [8.2.1 Αναγνώριση του προβλήματος](#.CE.91.CE.BD.CE.B1.CE.B3.CE.BD.CF.8E.CF.81.CE.B9.CF.83.CE.B7_.CF.84.CE.BF.CF.85_.CF.80.CF.81.CE.BF.CE.B2.CE.BB.CE.AE.CE.BC.CE.B1.CF.84.CE.BF.CF.82)
        *   [8.2.2 Επίλυση του προβλήματος (Η λάθος μέθοδος)](#.CE.95.CF.80.CE.AF.CE.BB.CF.85.CF.83.CE.B7_.CF.84.CE.BF.CF.85_.CF.80.CF.81.CE.BF.CE.B2.CE.BB.CE.AE.CE.BC.CE.B1.CF.84.CE.BF.CF.82_.28.CE.97_.CE.BB.CE.AC.CE.B8.CE.BF.CF.82_.CE.BC.CE.AD.CE.B8.CE.BF.CE.B4.CE.BF.CF.82.29)
        *   [8.2.3 Επίλυση του προβλήματος (Η σωστή μέθοδος)](#.CE.95.CF.80.CE.AF.CE.BB.CF.85.CF.83.CE.B7_.CF.84.CE.BF.CF.85_.CF.80.CF.81.CE.BF.CE.B2.CE.BB.CE.AE.CE.BC.CE.B1.CF.84.CE.BF.CF.82_.28.CE.97_.CF.83.CF.89.CF.83.CF.84.CE.AE_.CE.BC.CE.AD.CE.B8.CE.BF.CE.B4.CE.BF.CF.82.29)
        *   [8.2.4 Επίλυση του προβλήματος (Η βέλτιστη μέθοδος)](#.CE.95.CF.80.CE.AF.CE.BB.CF.85.CF.83.CE.B7_.CF.84.CE.BF.CF.85_.CF.80.CF.81.CE.BF.CE.B2.CE.BB.CE.AE.CE.BC.CE.B1.CF.84.CE.BF.CF.82_.28.CE.97_.CE.B2.CE.AD.CE.BB.CF.84.CE.B9.CF.83.CF.84.CE.B7_.CE.BC.CE.AD.CE.B8.CE.BF.CE.B4.CE.BF.CF.82.29)
        *   [8.2.5 Περισσότερα](#.CE.A0.CE.B5.CF.81.CE.B9.CF.83.CF.83.CF.8C.CF.84.CE.B5.CF.81.CE.B1)
    *   [8.3 Πρόβλημα με Realtek (no link / WOL)](#.CE.A0.CF.81.CF.8C.CE.B2.CE.BB.CE.B7.CE.BC.CE.B1_.CE.BC.CE.B5_Realtek_.28no_link_.2F_WOL.29)
        *   [8.3.1 Μέθοδος 1 - Υποβάθμιση/αλλαγή οδηγού Windows](#.CE.9C.CE.AD.CE.B8.CE.BF.CE.B4.CE.BF.CF.82_1_-_.CE.A5.CF.80.CE.BF.CE.B2.CE.AC.CE.B8.CE.BC.CE.B9.CF.83.CE.B7.2F.CE.B1.CE.BB.CE.BB.CE.B1.CE.B3.CE.AE_.CE.BF.CE.B4.CE.B7.CE.B3.CE.BF.CF.8D_Windows)
        *   [8.3.2 Μέθοδος 2 - Ενεργοποίηση του WOL στον οδηγό των Windows](#.CE.9C.CE.AD.CE.B8.CE.BF.CE.B4.CE.BF.CF.82_2_-_.CE.95.CE.BD.CE.B5.CF.81.CE.B3.CE.BF.CF.80.CE.BF.CE.AF.CE.B7.CF.83.CE.B7_.CF.84.CE.BF.CF.85_WOL_.CF.83.CF.84.CE.BF.CE.BD_.CE.BF.CE.B4.CE.B7.CE.B3.CF.8C_.CF.84.CF.89.CE.BD_Windows)
        *   [8.3.3 Μέθοδος 3 - Νεώτερος οδηγός Realtek Linux](#.CE.9C.CE.AD.CE.B8.CE.BF.CE.B4.CE.BF.CF.82_3_-_.CE.9D.CE.B5.CF.8E.CF.84.CE.B5.CF.81.CE.BF.CF.82_.CE.BF.CE.B4.CE.B7.CE.B3.CF.8C.CF.82_Realtek_Linux)
        *   [8.3.4 Μέθοδος 4 - Ενεργοποίηση *LAN Boot ROM* στο BIOS/CMOS](#.CE.9C.CE.AD.CE.B8.CE.BF.CE.B4.CE.BF.CF.82_4_-_.CE.95.CE.BD.CE.B5.CF.81.CE.B3.CE.BF.CF.80.CE.BF.CE.AF.CE.B7.CF.83.CE.B7_LAN_Boot_ROM_.CF.83.CF.84.CE.BF_BIOS.2FCMOS)
    *   [8.4 Πρόβλημα με DNS στο DLink G604T/DLink G502T](#.CE.A0.CF.81.CF.8C.CE.B2.CE.BB.CE.B7.CE.BC.CE.B1_.CE.BC.CE.B5_DNS_.CF.83.CF.84.CE.BF_DLink_G604T.2FDLink_G502T)
        *   [8.4.1 Πως θα αναγνωρίσετε το πρόβλημα](#.CE.A0.CF.89.CF.82_.CE.B8.CE.B1_.CE.B1.CE.BD.CE.B1.CE.B3.CE.BD.CF.89.CF.81.CE.AF.CF.83.CE.B5.CF.84.CE.B5_.CF.84.CE.BF_.CF.80.CF.81.CF.8C.CE.B2.CE.BB.CE.B7.CE.BC.CE.B1)
        *   [8.4.2 Περισσότερα για αυτό το πρόβλημα](#.CE.A0.CE.B5.CF.81.CE.B9.CF.83.CF.83.CF.8C.CF.84.CE.B5.CF.81.CE.B1_.CE.B3.CE.B9.CE.B1_.CE.B1.CF.85.CF.84.CF.8C_.CF.84.CE.BF_.CF.80.CF.81.CF.8C.CE.B2.CE.BB.CE.B7.CE.BC.CE.B1)
    *   [8.5 Έλεγχος προβλήματος DHCP με αποδέσμευση ΙΡ](#.CE.88.CE.BB.CE.B5.CE.B3.CF.87.CE.BF.CF.82_.CF.80.CF.81.CE.BF.CE.B2.CE.BB.CE.AE.CE.BC.CE.B1.CF.84.CE.BF.CF.82_DHCP_.CE.BC.CE.B5_.CE.B1.CF.80.CE.BF.CE.B4.CE.AD.CF.83.CE.BC.CE.B5.CF.85.CF.83.CE.B7_.CE.99.CE.A1)
    *   [8.6 Απουσία ενσύρματης σύνδεσης eth0 με Atheros AR8161](#.CE.91.CF.80.CE.BF.CF.85.CF.83.CE.AF.CE.B1_.CE.B5.CE.BD.CF.83.CF.8D.CF.81.CE.BC.CE.B1.CF.84.CE.B7.CF.82_.CF.83.CF.8D.CE.BD.CE.B4.CE.B5.CF.83.CE.B7.CF.82_eth0_.CE.BC.CE.B5_Atheros_AR8161)
    *   [8.7 Απουσία ενσύρματης σύνδεσης eth0 με Atheros AR9485](#.CE.91.CF.80.CE.BF.CF.85.CF.83.CE.AF.CE.B1_.CE.B5.CE.BD.CF.83.CF.8D.CF.81.CE.BC.CE.B1.CF.84.CE.B7.CF.82_.CF.83.CF.8D.CE.BD.CE.B4.CE.B5.CF.83.CE.B7.CF.82_eth0_.CE.BC.CE.B5_Atheros_AR9485)
    *   [8.8 Ανυπαρξία φορέα / σύνδεσης μετά από αναστολή λειτουργίας (Suspend)](#.CE.91.CE.BD.CF.85.CF.80.CE.B1.CF.81.CE.BE.CE.AF.CE.B1_.CF.86.CE.BF.CF.81.CE.AD.CE.B1_.2F_.CF.83.CF.8D.CE.BD.CE.B4.CE.B5.CF.83.CE.B7.CF.82_.CE.BC.CE.B5.CF.84.CE.AC_.CE.B1.CF.80.CF.8C_.CE.B1.CE.BD.CE.B1.CF.83.CF.84.CE.BF.CE.BB.CE.AE_.CE.BB.CE.B5.CE.B9.CF.84.CE.BF.CF.85.CF.81.CE.B3.CE.AF.CE.B1.CF.82_.28Suspend.29)
    *   [8.9 Broadcom BCM57780](#Broadcom_BCM57780)

## Έλεγχος σύνδεσης

**Σημείωση:** Αν λαμβάνετε σφάλμα όπως `ping: icmp open socket: Operation not permitted` όταν προσπαθείτε να κάνετε ping, δοκιμάστε να εγκαταστήσετε το πακέτο `iputils`.

Συνήθως η διαδικασία της βασικής εγκατάστασης, έχει δημιουργήσει μια σωστά διαμορφωμένη και ενεργή σύνδεση δικτύου. Για να το διαπιστώσετε δώστε την παρακάτω εντολή:

**Σημείωση:** Η επιλογή `-c 3` την επαναλαμβάνει τρεις φορές. Δείτε `man ping` για περισσότερες πληροφορίες.
 `$ ping -c 3 www.google.com` 
```
PING www.l.google.com (74.125.224.146) 56(84) bytes of data.
64 bytes from 74.125.224.146: icmp_req=1 ttl=50 time=437 ms
64 bytes from 74.125.224.146: icmp_req=2 ttl=50 time=385 ms
64 bytes from 74.125.224.146: icmp_req=3 ttl=50 time=298 ms

--- www.l.google.com ping statistics ---
3 packets transmitted, 3 received, 0% packet loss, time 1999ms
rtt min/avg/max/mdev = 298.107/373.642/437.202/57.415 ms

```

Αν λειτουργεί τότε το μόνο θα χρειαστεί να κάνετε είναι να κάνετε τις ρυθμίσεις που αφορούν το δικό σας δίκτυο, που αναφέρονται παρακάτω.

Αν η προηγούμενη εντολή δώσει έξοδο για άγνωστο προορισμό (unknown hosts), σημαίνει πως ο υπολογιστής σας απέτυχε να "μεταφράσει" αυτό το όνομα χώρου (domain name). Ίσως είναι πρόβλημα του δρομολογητή σας (router) και της διεύθυνσης εξόδου του (gateway) ή υπάρχει πρόβλημα με τον πάροχο δικτύου σας (ISP). Προσπαθήστε να κάνετε ping σε στατική ip για να διαπιστώσετε αν κάτι από τα παραπάνω ισχύει

 `$ ping -c 3 8.8.8.8` 
```
PING 8.8.8.8 (8.8.8.8) 56(84) bytes of data.
64 bytes from 8.8.8.8: icmp_req=1 ttl=53 time=52.9 ms
64 bytes from 8.8.8.8: icmp_req=2 ttl=53 time=72.5 ms
64 bytes from 8.8.8.8: icmp_req=3 ttl=53 time=70.6 ms

--- 8.8.8.8 ping statistics ---
3 packets transmitted, 3 received, 0% packet loss, time 2002ms
rtt min/avg/max/mdev = 52.975/65.375/72.543/8.803 ms

```

**Σημείωση:** Η διεύθυνση (ip) 8.8.8.8 , είναι η διεύθυνση ip του πρωτεύοντος υπολογιστή επίλυσης ονομάτων (primary DNS) της Google, και θεωρείται αξιόπιστη καθώς γενικά δεν είναι αποκλεισμένη από φίλτρα αποκλεισμού πρόσβασης (firewall) ή από ενδιάμεσους υπολογιστές δικτύου (proxies).

Αν το ping ήταν επιτυχές, δοκιμάστε να προσθέσετε αυτόν τον DNS στο αρχείο `/etc/resolv.conf`

## Ορίστε το όνομα του υπολογιστή σας (hostname)

Το [hostname](https://en.wikipedia.org/wiki/Hostname "wikipedia:Hostname") είναι ένα μοναδικό όνομα που δημιουργείται με σκοπό την αναγνώριση κάποιου υπολογιστή στο δίκτυο. Βρίσκεται διαμορφωμένο στο αρχείο `/etc/hostname`. Το αρχείο είναι δυνατό να περιέχει οποιοδήποτε όνομα. Για να ορίσετε το δικό σας, δώστε:

```
# hostnamectl set-hostname **myhostname**

```

Ορίσατε ως όνομα του υπολογιστή σας το **myhostname** στο `/etc/hostname`.

Δείτε `man 5 hostname` και `man 1 hostnamectl` για λεπτομέρειες.

**Σημείωση:** Η διεργασία `hostnamectl` υποστηρίζει FQDNs. Δεν είναι πλέον αναγκαίο να επεξεργαστείτε το αρχείο `/etc/hosts`, αφού το [systemd](https://www.archlinux.org/packages/?name=systemd) παρέχει την δυνατότητα επίλυσης ονομάτων στο δίκτυο και εγκαθίσταται από προεπιλογή και αυτόματα σε όλα τα συστήματα.

Για προσωρινή ονομασία του υπολογιστή σας (έως την πρώτη επανεκκίνηση) χρησιμοποιήστε την εντολή `hostname` από το πακέτο [inetutils](https://www.archlinux.org/packages/?name=inetutils):

```
# hostname *myhostname*

```

## Οδηγός Συσκευής (Device driver)

### Έλεγχος κατάστασης συσκευής

O [udev](/index.php/Udev "Udev") πρέπει να έχει αναγνωρίσει την συσκευή σας ([NIC](https://en.wikipedia.org/wiki/Network_interface_controller "wikipedia:Network interface controller")) και να έχει φορτώσει αυτόματα την απαραίτητη λειτουργική μονάδα (module) κατά την εκκίνηση. Ελέγξτε την γραμμή "Ethernet controller" (ή κάποια παρόμοια) στα αποτελέσματα της εντολής `lspci -v`. Θα πρέπει να αναφέρει ποια λειτουργική μονάδα του πυρήνα (kernel module) περιέχει τον οδηγό για την συσκευή σας. Για παράδειγμα:

 `$ lspci -v` 
```
02:00.0 Ethernet controller: Attansic Technology Corp. L1 Gigabit Ethernet Adapter (rev b0)
 	...
 	Kernel driver in use: atl1
 	Kernel modules: atl1

```

Κατόπιν βεβαιωθείτε πως ο οδηγός είναι ήδη φορτωμένος με την εντολή `dmesg | grep *module_name*`. Για παράδειγμα:

```
$ dmesg | grep atl1
    ...
    atl1 0000:02:00.0: eth0 link is up 100 Mbps full duplex

```

Αν ο οδηγός έχει φορτωθεί επιτυχώς, παραλείψτε το επόμενο βήμα. Αλλιώς θα πρέπει να βρείτε ποια ακριβώς λειτουργική μονάδα (module) απαιτεί η συγκεκριμένη συσκευή σας.

### Φόρτωση λειτουργικής μονάδας (module)

Κάντε αναζήτηση στο διαδίκτυο για τον ακριβή οδηγό / λειτουργική μονάδα (module / driver) που χρησιμοποιείται από την συσκευή σας. Μερικές συνήθεις λειτουργικές μονάδες (modules) είναι τα `8139too` για κάρτες που χρησιμοποιούν κυκλώματα της εταιρείας Realtek, ή τα `sis900` για αυτές που χρησιμοποιούν κυκλώματα της SiS. Όταν μάθετε ποια ακριβώς λειτουργική μονάδα (module) απαιτείται για την καλή λειτουργία του υλικού σας, δοκιμάστε να το [φορτώσετε χειροκίνητα](/index.php/Kernel_modules#Manual_module_handling "Kernel modules"). Αν λάβετε σφάλμα πως "η λειτουργική μονάδα δεν βρέθηκε (module not found)" είναι πιθανή η περίπτωση ο οδηγός να μην συμπεριλαμβάνεται στο πυρήνα του Arch. Αναζητήστε το στο αποθετήριο [AUR](/index.php/AUR "AUR").

Αν ο [udev](/index.php/Udev "Udev") δεν αναγνωρίσει και δεν φορτώσει αυτόματα κατά την εκκίνηση το κατάλληλο στοιχείο (module) για την συσκευή σας, δείτε το τμήμα [Kernel modules#Loading](/index.php/Kernel_modules#Loading "Kernel modules").

## Διασυνδέσεις δικτύου

### Ονομασία συσκευών

Για υπολογιστές με πολλές κάρτες δικτύου, είναι σημαντικό η κάθε μια να έχει το μοναδικό όνομά της. Η αλλαγή όνοματος συσκευής διασύνδεσης δικτύου, δημιουργεί πολλά προβλήματα στην διαμόρφωση τους.

Ο [udev](/index.php/Udev "Udev") είναι υπεύθυνος για το ποια συσκευή θα πάρει ποιο όνομα. Το [systemd](/index.php/Systemd "Systemd") από την έκδοση v197 (βρισκόμαστε ήδη στην έκδοση v208 την ώρα που γράφεται το παρόν άρθρο) εισήγαγε το [Predictable Network Interface Names](http://www.freedesktop.org/wiki/Software/systemd/PredictableNetworkInterfaceNames), το οποίο αυτόματα δίνει στατικά ονόματα (τα οποία δεν επιδέχονται αλλαγή) στις συσκευές δικτύου. Οι διασυνδέσεις πλέον έχουν το εξής πρόθεμα ανά τύπο διασύνδεσης, `en` (ethernet), `wl` (WLAN) ή `ww` (WWAN) ακολουθούμενο από ένα αυτόματα δημιουργούμενο αναγνωριστικό, δημιουργώντας μια καταχώρηση όπως `enp0s25`.

Αυτό μπορεί να παρακαμφθεί, δημιουργώντας έναν συμβολικό σύνδεσμο (symlink):

```
# ln -s /dev/null /etc/udev/rules.d/80-net-name-slot.rules

```

Χρήστες που αναβαθμίζουν το σύστημά τους από προηγούμενη έκδοση του systemd, θα έχουν ένα κενό κανόνων αρχείο. Έτσι, αν επιθυμείτε να δώσετε συγκεκριμένα ονόματα στις διεπαφές σας, απλά διαγράψτε το αρχείο.

**Συμβουλή:** Με `ip link` ή `ls /sys/class/net` μπορείτε να δείτε όλες τις διαθέσιμες διασυνδέσεις δικτύου του συστήματος σας.

**Σημείωση:** Όταν αλλάξετε το όνομα κάποιας διεπαφής σας, μην ξεχάσετε να ενημερώσετε όλες τις σχετικές με το δίκτυο διαμορφώσεις και τα σχετικά με το systemd αρχεία (αν έχετε επέμβει στην διαμόρφωσή του χειροκίνητα) ώστε να λάβουν τα νέα ονόματα. Ειδικά, αν έχετε ενεργό το [netctl static profiles](/index.php/Netctl#Basic_method "Netctl"). τρέξτε `netctl reenable *profile*` ώστε να αναβαθμιστεί το παραγόμενο αρχείο.

#### Αλλαγή ονόματος συσκευής

Μπορείτε να αλλάξετε το όνομα της συσκευής σας ορίζοντας το νέο, χειροκίνητα με έναν udev-rule. Για παράδειγμα:

 `/etc/udev/rules.d/10-network.rules` 
```
SUBSYSTEM=="net", ACTION=="add", ATTR{address}=="aa:bb:cc:dd:ee:ff", NAME="net1"
SUBSYSTEM=="net", ACTION=="add", ATTR{address}=="ff:ee:dd:cc:bb:aa", NAME="net0"

```

Δύο πράγματα πρέπει να προσέξετε:

*   Για να δείτε την διεύθυνση MAC (MAC address) της κάθε συσκευής σας χρησιμοποιείστε την παρακάτω εντολή: `cat /sys/class/net/*device_name*/address`

*   Βεβαιωθείτε πως χρησιμοποιείτε πεζούς χαρακτήρες στους udev-rules. Δεν καταλαβαίνει τα κεφαλαία.

Αν η κάρτα δικτύου σας έχει δυναμική διεύθυνση MAC (dynamic MAC address), μπορείτε να χρησιμοποιήσετε την εντολή DEVPATH για παράδειγμα

 `/etc/udev/rules.d/10-network.rules` 
```
SUBSYSTEM=="net", DEVPATH=="/devices/platform/wemac.*", NAME="int"

```

**Σημείωση:** Όταν επιλέγετε στατικά ονόματα συσκευών **πρέπει να αποφεύγετε να χρησιμοποιείτε ονόματα μορφής "eth*Χ*" και "wlan*Χ*"**, διότι μπορεί να εξελιχθεί σε αγώνα ([https://en.wikipedia.org/wiki/Race_condition](https://en.wikipedia.org/wiki/Race_condition)) μεταξύ kernel και udev κατά την διάρκεια της εκκίνησης. Αντ' αυτού είναι καλύτερο να χρησιμοποιείτε ονόματα για τις συσκευές σας που δεν χρησιμοποιούνται από τον πυρήνα από προεπιλογή π.χ. `net0`, `net1`, `wifi0`, `wifi1`. Για περισσότερες πληροφορίες δείτε την τεκμηρίωση του [systemd](http://www.freedesktop.org/wiki/Software/systemd/PredictableNetworkInterfaceNames).

### Ορισμός της μονάδας μέγιστης μετάδοσης (MTU) και μεγέθους ουράς (queue Length)

Μπορείτε να αλλάξετε το MTU και το queue Length ορίζοντας το επιθυμητό σε εσάς με έναν κανόνα udev (udev-rule). Για παράδειγμα:

 `/etc/udev/rules.d/10-network.rules` 
```
ACTION=="add", SUBSYSTEM=="net", KERNEL=="wl*", ATTR{mtu}="1480", ATTR{tx_queue_len}="2000"

```

**Προσοχή:** Το MTU και το queue length είναι κρίσιμα στοιχεία της συσκευής δικτύου και θα πρέπει να είστε ιδιαίτερα προσεκτικοί όταν επεμβαίνετε χειροκίνητα σε αυτά. Λάθος επιλογή μεγέθους έχει ως αποτέλεσμα την μη καλή λειτουργία τους έως ότου επαναφερθούν στις προεπιλογές του κατασκευαστή. Κάντε τις αλλαγές όταν ξέρετε τι ακριβώς κάνετε

### Βρείτε τα τρέχοντα ονόματα των συσκευών

Τα ονόματα των συσκευών δικτύου σας, μπορούν να βρεθούν με την εντολή sysfs

 `$ ls /sys/class/net` 
```
lo eth0 eth1 firewire0

```

### Ενεργοποίηση και απενεργοποίηση συσκευών δικτύου

Μπορείτε να ενεργοποιήσετε ή να απενεργοποιήσετε συσκευές δικτύου που γνωρίζετε το όνομά τους με τις παρακάτω εντολές:

```
# ip link set eth0 up
# ip link set eth0 down

```

Για να ελέγξετε το αποτέλεσμα:

 `$ ip link show dev eth0` 
```
2: eth0: <BROADCAST,MULTICAST,PROMISC,UP,LOWER_UP> mtu 1500 qdisc pfifo_fast master br0 state UP mode DEFAULT qlen 1000
...

```

## Ρύθμιση της διεύθυνσης ip

Έχετε δύο επιλογές: Εκχώρηση δυναμικής διεύθυνσης ip χρησιμοποιώντας [DHCP](https://en.wikipedia.org/wiki/Dynamic_Host_Configuration_Protocol "wikipedia:Dynamic Host Configuration Protocol"), ή εκχώρηση στατικής διεύθυνσης.

### Δυναμική διεύθυνση ip

#### Χειροκίνητη εκκίνηση DHCP Client Daemon

Σημειώστε πως ο δαίμονας `dhcpcd` (DHCP *client* daemon) δεν είναι ο ίδιος με τον `dhcpd` (DHCP *(server)* daemon).

 `# dhcpcd eth0` 
```
 dhcpcd: version 5.1.1 starting
 dhcpcd: eth0: broadcasting for a lease
 ...
 dhcpcd: eth0: leased 192.168.1.70 for 86400 seconds

```

Η επόμενη εντολή, `ip addr show dev eth0` την ip διεύθυνσή σας.

Αν η `dhcpcd` αποτύχει, μπορείτε να χρησιμοποιήσετε την `dhclient` (από το πακέτο [dhclient](https://www.archlinux.org/packages/?name=dhclient))

#### Ενεργοποίηση DHCP κατά την εκκίνηση

Αν θέλετε να χρησιμοποιήσετε DHCP για την ενσύρματη σύνδεσή σας, θα το κάνετε με την `dhcpcd@.service` (από το πακέτο [dhcpcd](https://www.archlinux.org/packages/?name=dhcpcd)).

Για να εκκινήσετε άμεσα την DHCP για την σύνδεση `eth0`, απλώς δώστε:

```
# systemctl start dhcpcd@eth0.service

```

Κάντε την ενεργή κατά την εκκίνηση του υπολογιστή με την παρακάτω:

```
# systemctl enable dhcpcd@eth0.service

```

Αν η διεργασία dhcpd, εκκινήσει πριν φορτωθεί στον πυρήνα το άρθρωμα (module) που αφορά την κάρτα σας ([FS#30235](https://bugs.archlinux.org/task/30235)), χειροκίνητα προσθέστε την στο αρχείο `/etc/modules-load.d/*.conf`. Για παράδειγμα, αν η Realtek κάρτα σας απαιτεί το άρθρωμα (module) `r8169`, δημιουργήστε το αρχείο `/etc/modules-load.d/realtek.conf` όπως εμφανίζεται παρακάτω:

 `/etc/modules-load.d/realtek.conf` 
```
r8169

```

**Συμβουλή:** Για να βρείτε ποια αρθρώματα (modules) απαιτούνται για την λειτουργία της κάρτας δικτύου σας, χρησιμοποιήστε `lspci -k`.

Αν χρησιμοποιήτε DHCP και **δεν** θέλετε να σας αποδίδονται αυτόματα οι DNS servers κάθε φορά που εκκινήτε την σύνδεση με το δίκτυό σας, σιγουρευτείτε πως έχετε προσθέσει στο τελευταίο τμήμα του αρχείου `dhcpcd.conf` την παρακάτω γραμμή:

 `/etc/dhcpcd.conf` 
```
nohook resolv.conf

```

Επίσης αν είστε σε ένα δίκτυο με ενεργό DHCPv4, το οποίο κάνει επιλογή ταυτότητας client με βάση τις MAC διευθύνσεις, ίσως θα θέλατε να αλλάξετε την ακόλουθη γραμμή:

 `/etc/dhcpcd.conf` 
```
# Use the same DUID + IAID as set in DHCPv6 for DHCPv4 Client ID as per RFC4361\. 
duid

```

Σε:

 `/etc/dhcpcd.conf` 
```
# Use the hardware address of the interface for the Client ID (DHCPv4).
clientid

```

Αλλιώς, ίσως να μην πάρετε άδεια πρόσβασης, αφού υπάρχει περίπτωση ο DHCP server να μην είναι σε θέση να διαβάσει σωστά την [DHCPv6-style](http://en.wikipedia.org/wiki/DHCPv6) ταυτότητα πελάτη (Client id) του υπολογιστή σας. Δείτε [RFC 4361](http://tools.ietf.org/html/rfc4361) για περισσότερες πληροφορίες.

Για να αποτρέψετε τον `dhcpcd` από το να προσθέσει DNS servers στο αρχείο `/etc/resolv.conf`, χρησιμοποιήστε την επιλογή `nooption`:

 `/etc/dhcpcd.conf` 
```
nooption domain_name_servers

```

Μετά προσθέστε τους δικούς σας στο αρχείο `/etc/resolv.conf`.

Μπορείτε να χρησιμοποιήσετε το πακέτο [openresolv](https://www.archlinux.org/packages/?name=openresolv) αν διαφορετικές διεργασίες θέλουν να ελέγξουν το αρχείο `/etc/resolv.conf` (π.χ. [dhcpcd](https://www.archlinux.org/packages/?name=dhcpcd) και ένας πελάτης εικονικού δικτύου (VPN client)). Δεν απαιτείται περαιτέρω διαμόρφωση του [dhcpcd](https://www.archlinux.org/packages/?name=dhcpcd) ώστε να χρησιμοποιήσετε το [openresolv](https://www.archlinux.org/packages/?name=openresolv).

### Στατική διεύθυνση ip

Υπάρχουν πολλοί λόγοι για τους οποίους θα θέλατε να έχετε μια στατική διεύθυνση ip (static ip address) στο δίκτυό σας. Για παράδειγμα μπορεί να μην υπάρχει διαθέσιμος DHCP server.

**Σημείωση:** Αν μοιράζεστε την σύνδεση σας από έναν υπολογιστή με λειτουργικό Windows χωρίς ενδιάμεσο δρομολογητή (router), βεβαιωθείτε πως χρησιμοποιείτε στατική ip **και** στους δύο ώστε να αποφύγετε προβλήματα τοπικού δικτύου σας (LAN).

Χρειάζεστε:

*   Στατικές διευθύνση ip (Static ip address)
*   [Subnet mask](https://en.wikipedia.org/wiki/Subnetwork "wikipedia:Subnetwork")
*   [Broadcast address](https://en.wikipedia.org/wiki/Broadcast_address "wikipedia:Broadcast address")
*   [Gateway](https://en.wikipedia.org/wiki/Default_gateway "wikipedia:Default gateway")'s IP address

Αν είστε σε ιδιωτικό δίκτυο, είναι ασφαλέστερο να χρησιμοποιήσετε ip διευθύνσεις στο εύρος 192.168.*.*255 . Η πύλη εξόδου (gateway) είναι συνήθως στο 192.168.*.1 ή στο 192.168.*.254 .

#### Χειροκίνητη απόδοση στατικής ip

Μπορείτε να αποδώσετε την στατική διεύθυνση ip που εποθυμείτε, μέσω κονσόλας:

```
# ip addr add <IP address>/<subnet mask> dev <interface>

```

Για παράδειγμα:

```
# ip addr add 192.168.1.2/24 dev eth0

```

**Σημείωση:** Η μάσκα υποδικτύου (subnet mask) προσδιορίστηκε χρησιμοποιώντας [CIDR notation](https://en.wikipedia.org/wiki/CIDR_notation "wikipedia:CIDR notation").

Για περισσότερες επιλογές, δείτε `man ip`.

Προσθέστε την πύλη εξόδου σας (gateway) με:

```
# ip route add default via <default gateway IP address>

```

Για παράδειγμα:

```
# ip route add default via 192.168.1.1

```

Αν λάβετε το σφάλμα "No such process", θα πρέπει να τρέξετε την `ip link set dev eth0 up` με τον λογαριασμό του root.

#### Χειροκίνητη σύνδεση κατά την εκκίνηση με χρήση του systemd

Πρώτα πρέπει να δημιουργήσετε ένα αρχείο διαμόρφωσης για την διεργασία [systemd](/index.php/Systemd "Systemd"), αντικαθιστώντας το `<interface>` με το σωστό:

 `/etc/conf.d/network@<interface>` 
```
address=192.168.0.15
netmask=24
broadcast=192.168.0.255
gateway=192.168.0.1

```

Δημιουργήστε ένα αρχείο μονάδας systemd:

 `/etc/systemd/system/network@.service` 
```
[Unit]
Description=Network connectivity (%i)
Wants=network.target
Before=network.target
BindsTo=sys-subsystem-net-devices-%i.device
After=sys-subsystem-net-devices-%i.device

[Service]
Type=oneshot
RemainAfterExit=yes
EnvironmentFile=/etc/conf.d/network@%i

ExecStart=/usr/bin/ip link set dev %i up
ExecStart=/usr/bin/ip addr add ${address}/${netmask} broadcast ${broadcast} dev %i
ExecStart=/usr/bin/ip route add default via ${gateway}

ExecStop=/usr/bin/ip addr flush dev %i
ExecStop=/usr/bin/ip link set dev %i down

[Install]
WantedBy=multi-user.target

```

Ενεργοποιήστε την διεργασία και εκκινήστε την, προσθέτοντας το όνομα της διεπαφής σας:

```
# systemctl enable network@eth0.service
# systemctl start network@eth0.service

```

#### Υπολογισμός διευθύνσεων

Μπορείτε να χρησιμοποιήσετε το `ipcalc` που περιέχεται στο πακέτο (ip broadcast), [ipcalc](https://www.archlinux.org/packages/?name=ipcalc) το εύρος από την διεύθυνση εκπομπής (ip broadcast), δίκτυο, μάσκα δικτύου (netmask), και εύρος υποδοχής (host range) για προηγμένες ρυθμίσεις. Για παράδειγμα, χρησιμοποιώ ενσύρματη σύνδεση πάνω από firewire ώστε να συνδέσω έναν υπολογιστή με windows σε αυτόν με arch. Για ασφάλεια και οργάνωση δικτύου, τα τοποθέτησα σε ένα δικό τους δίκτυο και διαμόρφωσα το netmask και το broadcast ώστε να είναι οι μόνοι υπολογιστές σε αυτό το δίκτυο. Για να βρω τις διευθύνσεις του netmask και του broacast για αυτό, χρησιμοποίησα ipcalc, δίνοντάς την διεύθυνση ip του arch firewire nic 10.66.66.1, διευκρινίζοντας στο ipcalc πως θα πρέπει να δημιουργήσει ένα δίκτυο με μόνο δύο οικοδεσπότες (hosts).

 `$ ipcalc -nb 10.66.66.1 -s 1` 
```
Address:   10.66.66.1

Netmask:   255.255.255.252 = 30
Network:   10.66.66.0/30
HostMin:   10.66.66.1
HostMax:   10.66.66.2
Broadcast: 10.66.66.3
Hosts/Net: 2                     Class A, Private Internet

```

## Φόρτωση ρυθμίσεων

Για να ελέγξετε τις ρυθμίσεις σας, μπορείτε είτε να κάνετε επανεκκίνηση είτε να επανεκκινήσετε την σχετική διεργασία του systemd:

```
# systemctl restart dhcpcd@eth0

```

Δοκιμάστε να κάνετε ping την πύλη εξόδου σας (gateway), τον DNS server, τον παροχέα της σύνδεσής σας (provider) και μερικά sites με αυτή την σειρά, ώστε να διαγνώσετε τυχόν προβλήματα συνδεσιμότητας, όπως το παράδειγμα:

```
$ ping -c 3 www.google.com

```

## Συμπληρωματικές ρυθμίσεις

### ifplugd για laptops

**Συμβουλή:** Το πακέτο [dhcpcd](https://www.archlinux.org/packages/?name=dhcpcd) έχει ακριβώς τις ίδιες δυνατότητες

Το πακέτο [ifplugd](https://www.archlinux.org/packages/?name=ifplugd) από τα [Official repositories](/index.php/Official_repositories "Official repositories") είναι ένας δαίμονας ο οποίος θα διαμορφώσει αυτόματα την Ενσύρματη συσκευή σας μόλις συνδέσετε το καλώδιο και αυτόματα θα την επαναδιαμορφώσει μόλις το καλώδιο αποσυνδεθεί. Αυτό είναι πολύ χρήσιμο για φορητούς υπολογιστές με ενσωματωμένες κάρτες δικτύου, αφού θα διαμορφώσουν την διεπαφή μόνο όταν το καλώδιο έχει συνδεθεί. Άλλη μια χρήση είναι όταν θέλετε να επανεκκινήσετε το δίκτυό σας αλλά όχι τον υπολογιστή σας η να το κάνετε από κονσόλα.

Από προεπιλογή είναι ρυθμισμένο να λειτουργεί για την συσκευή {{ic|eth0||. Αυτή και μερικές άλλες ρυθμίσεις μπορούν να διαμορφωθούν στο αρχείο `/etc/ifplugd/ifplugd.conf`.

**Σημείωση:** Το πακέτο [Netctl](/index.php/Netctl "Netctl") περιλαμβάνει την `netctl-ifplugd@.service`, ενώ ένας άλλος τρόπος είναι με την `ifplugd@.service` από το πακέτο [ifplugd](https://www.archlinux.org/packages/?name=ifplugd). Για παράδειγμα χρησιμοποιήστε την `systemctl enable ifplugd@eth0.service`.

### Ενσωμάτωση ή Συσσώρευση συνδέσεων (Bonding or LAG)

Δείτε [netctl#Bonding](/index.php/Netctl#Bonding "Netctl").

### IP address aliasing

Η ψευδονομασία των διευθύνσεων ip (ip aliasing) είναι η διαδικασία της πρόσθεσης ή της απόδοσης πάνω από μιας διεύθυνσης δικτύου (ip) στην ίδια συσκευή. Με αυτή, ένας δικτυακός κόμβος μπορεί να έχει πολλαπλές συνδέσεις στο δίκτυο, που η κάθε μια να εξυπηρετεί διαφορετικό σκοπό. Η τυπική εφαρμογή της είναι η εικονική φιλοξενία διακομιστών ιστού ή διακομιστών ftp (Web ή FTP servers), ή την αναδιοργάνωση εξυπηρετητών (servers) χωρίς να απαιτείται η ενημέρωση κανενός άλλου υπολογιστή στο δίκτυο (ιδιαίτερα χρήσιμο για την οργάνωση των DNS).

#### Παράδειγμα

Θα χρειαστείτε το πακέτο [netctl](https://www.archlinux.org/packages/?name=netctl) από τα [Official repositories](/index.php/Official_repositories "Official repositories").

Προετοιμάστε την διαμόρφωση:

 `/etc/netctl/mynetwork` 
```
Connection='ethernet'
Description='Five different addresses on the same NIC.'
Interface='eth0'
IP='static'
Address=('192.168.1.10' '192.168.178.11' '192.168.1.12' '192.168.1.13' '192.168.1.14' '192.168.1.15')
Gateway='192.168.1.1'
DNS=('192.168.1.1')

```

κατόπιν απλά δίνετε:

```
$ netctl start mynetwork

```

### Αλλαγή διεύθυνσης MAC/hardware

Δείτε [MAC address spoofing](/index.php/MAC_address_spoofing "MAC address spoofing").

### Κοινή χρήση δικτύου (Sharing Internet)

Δείτε [Internet sharing](/index.php/Internet_sharing "Internet sharing").

### Διαμόρφωση δρομολογητή (Router)

Δείτε [Router](/index.php/Router "Router").

### Ανάλυση ονομασίας κεντρικού υπολογιστή δικτύου (Host name resolution)

Το προαπαιτούμενο είναι να ορίσετε το όνομα [#Set the hostname](#Set_the_hostname) αφού υπάρχει σε κάθε τοπικό σύστημα.

 `$ ping hostname` 
```
PING hostname (192.168.1.2) 56(84) bytes of data.
64 bytes from hostname (192.168.1.2): icmp_seq=1 ttl=64 time=0.043 ms
```

Για να δώσετε την δυνατότητα σε άλλους υπολογιστές να "απευθύνονται" στον κεντρικό με το όνομά του, χειροκίνητη επέμβαση και ορισμός του στο αρχείο `/etc/hosts` ή η δημιουργία μιας διεργασίας ώστε να διαδοθεί / αναγνωριστεί αυτό είναι απαιτούμενη.

Όταν η δημιουργία ενός DNS sever όπως [BIND](/index.php/BIND "BIND") ή [Unbound](/index.php/Unbound "Unbound") είναι υπερβολικά δύσκολη, η χειροκίνητη επέμβαση του αρχείου `/etc/hosts` είναι περίπλοκη, ή όταν επιθυμείτε μεγαλύτερη ευελιξία με δυναμική είσοδο / έξοδο εξυπηρετητών στο δίκτυο, είναι δυνατή η διαχείριση της επίλυσης του ονόματος στο τοπικό σας δίκτυο με την χρησιμοποίηση δικτύου zero-configuration. Υπάρχουν δύο επιλογές:

*   [Samba](/index.php/Samba "Samba") παρέχει επίλυση ονομασίας εξυπηρετητών (Hostname resolution ) μέσω **NetBIOS** της Microsft. Το μόνο που χρειάζεται είναι η εγκατάσταση του [samba](https://www.archlinux.org/packages/?name=samba) και η ενεργοποίηση της διεργασίας `nmbd.service`. Υπολογιστές με λειτουργικό σύστημα Windows, OS X, ή Linux με ενεργό `nmbd`, θα μπορούν να εντωπίσουν τον δικό σας.

*   [Avahi](/index.php/Avahi "Avahi") παρέχει επίλυση ονομασίας εξυπηρετητών (Hostame resolution) μέσω του **zeroconf**, επίσης γνωστού ως Avahi ή Bonjour.

Απαιτεί λίγο περίπλοκη διαμόρφωση από το Samba: Δείτε [Avahi#Hostname resolution](/index.php/Avahi#Hostname_resolution "Avahi") για λεπτομέρειες. Υπολογιστές με λειτουργικά συστήματα OS X, ή Linux με ενεργό τον Avahi δαίμονα (Avahi daemon), θα μπορούν να βρούν τον δικό σας. Το λειτουργικό Windows δεν παρέχουν εγγενώς το Avahi πελάτη ή δαίμονα (client or daemon).

## Αντιμετώπιση προβλημάτων

### Εναλλαγή υπολογιστών σε καλωδιακό μόντεμ (cable modem)

Οι περισσότεροι τοπικοί καλωδιακοί πάροχοι δικτύου (ISP) έχουν παραμετροποιήσει το μόντεμ ώστε να αναγνωρίζει μόνο έναν υπολογιστή, βάσει της διεύθυνσης MAC της διεπαφής του. Μόλις το μόντεμ αποθηκεύσει την MAC διεύθυνση του πρώτου υπολογιστή ή συσκευής που θα συνδεθεί, δεν θα ανταποκριθεί σε άλλη διεύθυνση MAC με κανέναν τρόπο. Έτσι αν αλλάξετε υπολογιστή (ή δρομολογητή), το νέο υλικό δεν θα συνεργαστεί με το καλωδιακό μόντεμ, διότι έχουν διαφορετική MAC διεύθυνση. Για να επαναφέρετε το μόντεμ στις αρχικές ρυθμίσεις του και να είναι σε θέση να αναγνωρίσει την νέα διεύθυνση MAC του υλικού που έχετε συνδέσει, θα πρέπει να του διακόψετε την τροφοδοσία και να το ανάψετε ξανά. Μόλις αυτό γίνει, θα πρέπει να κάνετε επανεκκίνηση στο νέο υλικό ώστε να στείλει ένα αίτημα DHCP, η κάντε το χειροκίνητα.

Αν αυτή η μέθοδος αποτύχει, θα πρέπει να δημιουργήσετε έναν κλώνο της διεύθυνσης MAC του αρχικού υπολογιστή. Δείτε επίσης [Change MAC/hardware address](/index.php/Configuring_Network#Change_MAC.2Fhardware_address "Configuring Network").

### Το πρόβλημα του εύρους τιμής του TCP

Τα πακέτα TCP περιέχουν από "κατασκευή" ένα εύρος τιμής το οποίο καθορίζει πόσα δεδομένα θα επιστραφούν ως απάντηση από κάποιον άλλον εξυπηρετητή. Αυτή η τιμή εκπροσωπείται από μόνο 16bits, μιας και αυτό το "παράθυρο" είναι μόνο 64kb. Τα πακέτα TCP αποθηκεύονται στην προσωρινή μνήμη για λίγο (πρέπει να αναδιοργανωθούν), και μιας και η μνήμη είναι (ή συνήθως είναι) περιορισμένη, ένας εξυπηρετητής εύκολα μπορεί να την εξαντλήσει.

Το 1992, μιας και όλο και περισσότερη μνήμη γίνεται διαθέσιμη, ήρθε το [RFC 1323](http://www.faqs.org/rfcs/rfc1323.html) ώστε να βελτιώσει την κατάσταση: Εύρος "παραθύρου". Η τιμή του"παραθύρου", αποδίδεται σε όλα τα πακέτα, τροποποιημένη βάσει ενός Συντελεστή κλίμακας ο οποίος ορίζεται μόνο μια φορά, κατά την έναρξη της σύνδεσης.

Αυτός ο 8-bit Συντελεστής κλίμακας, επιτρέπει στο "παράθυρο" να λαμβάνει τιμή μέχρι και 32 φορές μεγαλύτερη από την αρχική.

Φαίνεται [ως μερικά χαλασμένα routers και firewalls στο διαδίκτυο, επανακαθορίζουν αυτόν τον συντελεστή στο 0 το οποίο προκαλεί προβλήματα σύνδεσης μεταξύ των εξυπηρετητών.

Ο Linux Kernel από την έκδοση 2.6.17 εισήγαγε ένα νέο σενάριο υπολογισμού υψηλότερου Συντελεστή κλίμακας, κάνοντας στην ουσία τα προβλήματα που προκαλούν τα χαλασμένα routers και firewalls πιο ορατά.

Το αποτέλεσμα αυτού του προβλήματος στην καλύτερη περίπτωση είναι μια ελαττωματική σύνδεση ή πολύ χαμηλής ταχύτητας.

#### Αναγνώριση του προβλήματος

Πρώτα απ' όλα να κάνουμε κάτι σαφές: αυτό το πρόβλημα είναι περίεργο. Σε ορισμένες περιπτώσεις, δεν θα μπορείτε να χρησιμοποιήσετε συνδέσεις TCP (HTTP, FTP, ...) καθόλου, και παό την άλλη μεριά θα είστε σε θέση να επικοινωνείτε με κάποιους (πολύ λίγους) εξυπηρετητές.

Όταν έχετε το παραπάνω πρόβλημα, τα μηνύματα από το `dmesg` θα φαίνονται καθαρά, η αναφορά εργασιών (logs) χωρίς πρόβλημα η έξοδος της `ip addr` χωρίς πρόβλημα και γενικά όλα θα φαίνονται φυσιολογικά. Αν δεν μπορείτε να συνδεθείτε με κανένα site, αλλά μπορείτε να κάνετε Ping σε μερικούς τυχαίους εξυπηρετητές, υπάρχουν σοβαρές υπόνοιες πως έχετε το παραπάνω πρόβλημα μιας και το ping βασίζεται στο ICMP και δεν επηρεάζεται από την κατάσταση των TCP πακέτων.

Μπορείτε να δοκιμάσετε να χρησιμοποιήσετε το Whireshark. Ίως δείτε επιτυχείς συνδέσεις UDP & ICMP, αλλά όχι TCP (μόνο σε εξυπηρετητές του εξωτερικού).

#### Επίλυση του προβλήματος (Η λάθος μέθοδος)

Για να το διορθώσετε με την μη συνιστώμενη μέθοδο, μπορείτε να αλλάξετε την τιμή tcp_rmem στην οποία βασίζεται ο τρόπος υπολογισμού του Συντελεστή τιμής εύρους "παραθύρου". Αν και θα λειτουργήσει στους περισσότερους εξυπηρετητές, φεν είναι εγγυημένη, ειδικά για τους περισσότερο απομακρυσμένους.

```
# echo "4096 87380 174760" > /proc/sys/net/ipv4/tcp_rmem

```

#### Επίλυση του προβλήματος (Η σωστή μέθοδος)

Απλά απενεργοποιήστε το εύρος "παραθύρο". Μιας και το εύρος "παραθύρου" είναι λειτουργία που παρέχει το TCP, ίσως να μην είναι εφικτό να απενεργοποιηθεί, ειδικά αν δεν μπορείτε να διορθώσετε το χαλασμένο router. Υπάρχουν αρκετοί τρόποι για την απενεργοποίηση του εύρους "παραθύρου", και φαίνεται πως η πιο μόνιμη και ανθεκτική (η οποία έχει εφαρμογή και σε όλους τους πυρήνες) είναι να προσθέστε την παρακάτω γραμμή στο αρχείο `/etc/sysctl.d/99-sysctl.conf` (δείτε επίσης [sysctl](/index.php/Sysctl "Sysctl"))

```
net.ipv4.tcp_window_scaling = 0

```

#### Επίλυση του προβλήματος (Η βέλτιστη μέθοδος)

Μιας και το πρόβλημα δημιουργείται από χαλασμένο router/forewall, ας το αντικαταστήσουμε.

#### Περισσότερα

Αυτό το τμήμα βασίστηκε σε άρθρο που δημοσιεύτηκε στο LWN [TCP window scaling and broken routers](http://lwn.net/Articles/92727/) καθώς και σε άρθρο από το Kernel Trap: [Window Scaling on the Internet](http://kerneltrap.org/node/6723).

Υπάρχουν αρκετές δημοσιεύσεις επίσης και στην LKML (Linux Kenel Mailing List).

### Πρόβλημα με Realtek (no link / WOL)

Χρήστες με κάρτες δικτύου (κάρτες ή ενσωματωμένες στην μητρική -on-board-) βασισμένες στα Realtek 8168 8169 8101 8111(C) ίσως παρατηρήσουν πως κατά την εκκίνηση η διεπαφή δικτύου τους είναι ανενεργή χωρίς να υπάρχει αναμμένη η ενδεικτική λυχνία λειτουργίας. Συνήθως παρατηρείται σε συστήματα με δύο λειτουργικά, που το δεύτερο είναι τα Windows. Φαίνεται πως η εγκατάσταση του επίσημου οδηγού της Realtek (νεώτερου από τον Μάϊο του 2007) στα Windows, είναι το πρόβλημα. Αυτοί οι νεώτεροι οδηγοί, απενεργοποιούν την δυνατότητα Wake-On-Lan απενεργοποιώντας την διεπαφή δικτύου κατά το κλείσιμο του υπολογιστή από τα Windows, η οποία θα παραμείνει ανενεργή έως την στιγμή της εκκίνησης ξανά των Windows. Μπορείτε εύκολα να διαπιστώσετε αν έχετε το παραπάνω πρόβλημα, αν και έως την εκκίνηση των Windows η ενδεικτική λυχνία της σύνδεσης παραμένει σβηστή. Η αναμενόμενη λειτουργία είναι η λυχνία σύνδεσης να παραμένει ανοιχτή και για όσο παραμένει ανοιχτό το σύστημα, ακόμα και κατά την διάρκεια του POST. Το πρόβλημα αυτό επηρεάζει ακόμα και άλλα λειτουργικά συστήματα χωρίς νεώτερους οδηγούς (πχ Live CDs). Εδώ μπορείτε να βρείτε ορισμένες λύσεις για αυτό το πρόβλημα:

#### Μέθοδος 1 - Υποβάθμιση/αλλαγή οδηγού Windows

Μπορείτε να υποβαθμίσετε τον οδηγό διεπαφής σας σε αυτόν των Windows (αν υπάρχει), ή να εγκαταστήσετε / υποβαθμίσετε τον επίσημο οδηγό Realtek ο οποίος έχει ημερομηνία έκδοσης πρίν τον Μάιο 2007 (ίσως να βρίσκεται στο συνοδευτικό cd που αφορά το υλικό σας).

#### Μέθοδος 2 - Ενεργοποίηση του WOL στον οδηγό των Windows

Πιθανώς ο ταχύτερος και ασφαλέστερος τρόπος επιδιόρθωσης είναι να αλλάξετε αυτή την ρύθμιση στον οδηγό των Windows. Με αυτόν τον τρόπο θα επιδιορθωθεί σε ολόκληρο το σύστημα και όχι μόνο στο λειτουργικό Arch (πχ live CDs, άλλα λειτουργικά συστήματα). Στα Windows και στην καρτέλα Device Manager, εντοπείστε την διεπαφή σας Realtek και κάντε διπλό κλικ πάνω της. Στην καρτέλα Advanced αλλάξτε την επιλογή "Wake-on-Lan after shutdown" σε Ενεργό.

```
Σε Windows XP (παράδειγμα)
Δεξί κλικ στο my computer
--> Καρτέλα Hardware 
  -->Επιλογή Device Manager
    -->Καρτέλα Network Adapters
      --> "διπλό κλικ" στο Realtek ...
        -->Καρτέλα Advanced
          --> Wake-On-Lan After Shutdown
            --> Enable

```

**Σημείωση:** Νεώτεροι οδηγοί για Windows (δοκιμασμένοι με *Realtek 8111/8169 LAN Driver v5.708.1030.2008*, ημερομηνίας 22/01/2009, διαθέσιμοι από την GIGABYTE) ίσως να αναφέρονται σε αυτή την επιλογή ελαφρά διαφορετικά, όπως *Shutdown Wake-On-LAN --> Enable*. Φαίνεται πως αλλάζοντάς το σε `Disable` δεν έχει καμία διαφορά (θα παρατηρήσετε πως η λυχνία σύνδεσης θα σβήσει με το κλείσιμο των Windows). Μία κακή λύση είναι να εκκινήσετε στο λειτουργικό Windows και αμέσως να κάνετε reset το σύστημα (πραγματοποιώντας μια απότομη επανεκκίνηση / εκκίνηση) μη δίνοντας την ευκαιρία στον οδηγό των Windows να κάνει ανενεργή την σύνδεση LAN. Η λυχνία της σύνδεσης θα παραμείνει ενεργή και η LAN διεπαφή σας θα παραμείνει προσβάσιμη μετά το POST - μέχρι την επόμενη εκκίνηση των Windows και τον σωστό τερματισμό τους
.

#### Μέθοδος 3 - Νεώτερος οδηγός Realtek Linux

Νεώτερος οδηγός για τις κάρτες Relatek για Linux, μπορεί να βρεθεί στο site της Realtek. (μη δοκιμασμένο αλλά ίσως να λύνει το πρόβλημα).

#### Μέθοδος 4 - Ενεργοποίηση *LAN Boot ROM* στο BIOS/CMOS

Φαίνεται πως η ρύθμιση *Integrated Peripherals --> Onboard LAN Boot ROM --> Enabled* στο BIOS/CMOS ενεργοποιεί το Realtek LAN chip κατά την εκκίνηση του συστήματος, άσχετα αν ο οδηγός των Windows το έχει απενεργοποιήσει κατά τον τερματισμό τους.

**Σημείωση:** Αυτό έχει δοκιμαστεί επιτυχώς πολλές φορές με την μητρική κάρτα GIGABYTE system board GA-G31M-ES2L με έκδοση BIOS F8 κυκλοφορίας 02/05/2009\. YMMV.

[Opanos](/index.php/User:Opanos "User:Opanos") ([talk](/index.php?title=User_talk:Opanos&action=edit&redlink=1 "User talk:Opanos (page does not exist)")) 16:56, 26 November 2013 (UTC)

### Πρόβλημα με DNS στο DLink G604T/DLink G502T

Χρήστες με router DLink G604T/DLink G502T, που χρησιμοποιούν DHCP και με firmware v2.00+ (χρήστες AUS firmware) ίσως έχουν προβλήματα με ορισμένα προγράμματα, καθώς δεν επιλύουν τις διευθύνσεις DNS. Ένα από αυτά τα προγράμματα ατυχώς είναι ο pacman. Το πρόβλημα έγκειται βασικά στο ότι το router κάτω από συγκεκριμένες συνθήκες δεν στέλνει σωστά DNS στο DHCP, το οποίο οδηγεί το πρόγραμμα να προσπαθεί να συνδεθεί στους εξυπηρετητές με διεύθυνση IP 1.0.0.0 και να αποτυγχάνει λόγω του λάθους: εξάντληση χρόνου.

#### Πως θα αναγνωρίσετε το πρόβλημα

Ο καλύτερος τρόπος για την διάγνωση του προβλήματος είναι η χρησιμοποίηση Firefox/Konqueror/links/seamonkey και η ενεργοποίηση του wget για τον pacman. Αν είστε σε φρέσκια εγκατάσταση του Arch Linux, τότε ίσως να πρέπει να σκεφτείτε την εγκατάσταση του `links` από το live CD.

Πρώτα, ενεργοποιήστε το wget για τον pacman (μιας και μας δείνει πληροφορίες για τον pacman κατά το downloading πακέτων). Ανοίχτε το αρχείο `/etc/pacman.conf` με τον επεξεργαστή κειμένου που χρησιμοποιείται και αφαιρέστε το σημείο σχολίου από την επόμενη γραμμή (αφαιρέστε το σύμβολο # αν υπάρχει)

```
XferCommand=/usr/bin/wget --passive-ftp -c -O %o %u

```

Όσο είστε στο αρχείο `/etc/pacman.conf`, ελέγξτε τον προεπιλεγμένο εξυπηρετητή που χρησιμοποιεί ο pacman για το κατέβασμα πακέτων.

Τώρα, ανοίξτε τον προεπιλεγμένο εξυπηρετητή στον φυλλομετρητή σας (browser) ώστε να διαπιστώσετε αν ο εξυπηρετητής είναι πράγματι ενεργός. Αν είναι, τότε δώστε `pacman -Syy` (σε άλλη περίπτωση επιλέξτε άλλον εξυπηρετητή ο οποίος θα είναι ενεργός και δώστε τον ως προεπιλογή στον pacman). Αν λάβετε κάτι παρόμοιο με (δώστε σημασία στο 1.0.0.0)

```
ftp://mirror.pacific.net.au/linux/archlinux/extra/os/i686/extra.db.tar.gz
           => '/var/lib/pacman/community.db.tar.gz.part'
Resolving mirror.pacific.net.au... 1.0.0.0

```

τότε το πιθανότερο είναι να έχετε το ίδιο πρόβλημα. Το 1.0.0.0 σημαίνει πως είναι αδύνατη η επίλυση DNS, έτσι πρέπει να τον προσθέσουμε στο `/etc/resolv.conf`.

#### Περισσότερα για αυτό το πρόβλημα

Αυτό είναι το Forum Wirlpool (Κοινότητα παρόχων Αυστραλίας) που μιλάνε για αυτό και δίνουν την ίδια λύση στο πρόβλημα:

[http://forums.whirlpool.net.au/forum-replies-archive.cfm/461625.html](http://forums.whirlpool.net.au/forum-replies-archive.cfm/461625.html)

### Έλεγχος προβλήματος DHCP με αποδέσμευση ΙΡ

Ίσως να παρουσιαστεί πρόβλημα όταν ο DHCP λάβει λάθος αντιστοίχηση διευθύνσεων IP. Για παράδειγμα όταν δύο routers είναι συνδεδεμένα μέσω VPN. Το router που είναι συνδεδεμένο με εμένα μέσω VPN μπορεί να αποδώσει διεύθυνση IP. Για να το διορθώσετε: Σε κονσόλα, με τον λογαριασμό του root, αποδεσμεύστε την διεύθυνση IP:

```
# dhcpcd -k

```

Κατόπιν, ζητήστε μια νέα:

```
# dhcpcd

```

Ίσως να χρειαστεί να τρέξετε τις παραπάνω δύο εντολές αρκετές φορές.

### Απουσία ενσύρματης σύνδεσης eth0 με Atheros AR8161

**Σημείωση:** Από την έκδοση 3.10.2-1-ARCH kernel και μετά, το alx ethernet άρθρωμα οδηγού (driver module) περιέχεται στο πακέτο.

Με την κάρτα Atheros AR8161 Gigabit Ethernet, η ενσύρματη σύνδεση δεν λειτουργεί άμεσα λαι χωρίς επέμβαση (με το μέσο εγκατάστασης του Μαϊου 2013). Το άρθρωμα (module) "alx" απαιτείται να φορτωθεί αλλά δεν παρέχεται.

Ο οδηγός από [compat-wireless](http://linuxwireless.org/en/users/Download/stable/#compat-wireless_stable_releases) (που έχει γίνει [compat-drives](https://backports.wiki.kernel.org/index.php/Releases) από την έκδοση του πυρήνα linux 3.7) πρέπει να εγκατασταθεί. Η σήμανση με την προσθήκη της μεταβλητής "-u" δηλώνει πως η Qualcomm εφάρμοσε έναν οδηγό κάτω από έναν ενοποιημένο.

```
$ wget [https://www.kernel.org/pub/linux/kernel/projects/backports/2013/03/28/compat-drivers-2013-03-28-5-u.tar.bz2](https://www.kernel.org/pub/linux/kernel/projects/backports/2013/03/28/compat-drivers-2013-03-28-5-u.tar.bz2)
$ tar xjf compat*
$ cd compat*
$ ./scripts/driver-select alx
$ make
$ sudo make install
$ sudo modprobe alx

```

Ο οδηγός alx δεν συμπεριλαμβάνεται στον Linux Kernel λόγω διάφορων προβλημάτων. Συμβατότητα μεταξύ των διαφορετικών εκδόσεων πυρήνα έχει επισημανθεί. Για καλύτερη υποστήριξη ακολουθείστε την [mailing list](http://lists.infradead.org/mailman/listinfo/unified-drivers) και την [alx page](http://www.linuxfoundation.org/collaborate/workgroups/networking/alx) για τα τελευταία νέα πάνω στην λύση του alx.

Ο οδηγός πρέπει να κατασκευαστεί και εγκατασταθεί ξανά μετά από κάθε αναβάθμιση του πυρήνα.

Εναλλακτικά μπορείτε να χρησιμοποιήσετε το πακέτο από το AUR [compat drivers](https://aur.archlinux.org/packages/compat-drivers-patched/), που εγκαθιστά πολλούς άλλους οδηγούς.

### Απουσία ενσύρματης σύνδεσης eth0 με Atheros AR9485

Η ενσύρματη σύνδεση (eth0) με την κάρτα Atheros AR9485 δεν λειτουργεί άμεσα και χωρίς επέμβαση (με το μέσο εγκατάστασης του Μαϊου 2013). Η λύση είναι να εγκαταστήσετε το πακέτο [compat-drivers-patched](https://aur.archlinux.org/packages/compat-drivers-patched/) από το AUR.

### Ανυπαρξία φορέα / σύνδεσης μετά από αναστολή λειτουργίας (Suspend)

Μετά από αναστολή λειτουργίας στην μνήμη RAM δεν εμφανίζεται σύνδεση παρά το ότι το καλώδιο είναι συνδεδεμένο. Αυτό ίσως να οφείλεται στην διαχείριση ενέργειας της κάρτας PCI. Ποια είναι η έξοδος της

```
# ip link show eth0

```

Αν στην γραμμή περιέχεται το "NO-CARRIER" παρά το γεγονός πως το καλώδιο είναι συνδεδεμένο στην είσοδο της ενσύρματης σύνδεσης, είναι πιθανόν η συσκευή να έχει αυτόματα αναστείλει την λειτουργία της και ο έλεγχος ύπαρξης μέσου να μην λειτουργεί. Για να το λύσετε, το πρώτο που να κάνετε είναι να βρείτε την διεύθυνση του ελεγκτή ενσύρματης σύνδεσης με την

```
# lspci

```

Θα πρέπει να μοιάζει με:

```
...
00:19.0 Ethernet controller: Intel Corporation 82577LM Gigabit Network Connection (rev 06)
...

```

Άρα, η διεύθυνση είναι η 00:19.0.

Τώρα ελέγξτε την κατάσταση της διαχείρισης ενέργειας με την

```
# cat "/sys/bus/pci/devices/0000:00:19.0/power/control"

```

αντικαθιστώντας το 00:19.0 με την πραγματική δική σας διεύθυνση.

Αν η έξοδος είναι ""auto"", μπορείτε να δοκιμάσετε να επαναφέρετε την συσκευή με την

```
# echo on > "/sys/bus/pci/devices/0000:00:19.0/power/control"

```

Μην ξεχνάτε να αντικαθιστάτε την 00:19.0 με την δική σας.

**Σημείωση:** Αυτό φαίνεται να είναι ελάττωμα (bug) στον πυρήνα 3.8.4.1- (ο 3.8.8.1 ακόμα το έχει): [Forum discussion.](https://bbs.archlinux.org/viewtopic.php?id=159837&p=2) Επίσης φαίνεται μια διόρθωση [να επεξεργάζεται. (Θα έχει διορθωθεί στην έκδοση 3.9.)](https://lkml.org/lkml/2013/1/18/147) Στο μεταξύ η παραπάνω προσωρινή λύση ταιριάζει απόλυτα.

### Broadcom BCM57780

Αυτό το υλικό της Broadcom μερικές φορές δεν λειτουργεί όπως πρέπει, εκτός και αν του ορίσεις την σειρά φόρτωσης αρθρωμάτων. Τα αρθρώματα είναι τα: `broadcom` and `tg3`, το πρώτο πρέπει να φορτωθεί πρώτα.

Αυτά τα βήματα πρέπει να βοηθήσουν αν ο υπολογιστής σας έχει τέτοιο υλικό:

```
$ lspci | grep Ethernet
02:00.0 Ethernet controller: Broadcom Corporation NetLink BCM57780 Gigabit Ethernet PCIe (rev 01)

```

Εάν η ενσύρματη σύνδεσή σας δεν λειτουργεί όπως πρέπει, δοκιμάστε να βγάλετε το καλώδιο και μετά με το λογαριασμό του root σε κονσόλα δώστε τις παρακάτω:

```
# modprobe -r tg3
# modprobe broadcom
# modprobe tg3

```

Τώρα, επανασυνδέστε το καλώδιο. Αν το πρόβλημα έχει λυθεί, μπορείτε να το κάνετε μόνιμο προσθέτοντας τα `broadcom` και `tg3` (με αυτή την σειρά) στον πίνακα `MODULES` στο αρχείο `/etc/mkinitcpio.conf`:

```
MODULES=".. broadcom tg3 .."

```

Κατόπιν δημιουργήστε πάλι το initramfs:

```
# mkinitcpio -p linux

```

**Σημείωση:** Αυτές οι μέθοδοι, είναι δυνατόν να λειτουργούν και με άλλα υλικά, όπως το BCM57760.