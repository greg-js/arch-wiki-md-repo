Related articles

*   [Network configuration](/index.php/Network_configuration "Network configuration")
*   [Software access point](/index.php/Software_access_point "Software access point")
*   [Ad-hoc networking](/index.php/Ad-hoc_networking "Ad-hoc networking")
*   [Internet sharing](/index.php/Internet_sharing "Internet sharing")

Η ρύθμιση του ασύρματου δικτύου, είναι μια διαδικασία που αποτελείται από δύο μέρη: Το πρώτο είναι η αναγνώριση και η επιβεβαίωση πως ο σωστός οδηγός για την ασύρματη κάρτα σας είναι εγκατεστημένος (υπάρχουν στο μέσο εγκατάστασης αλλά συχνά απαιτείται η ξεχωριστή εγκατάσταση), και η ρύθμιση της διεπαφής.

Το δεύτερο είναι η επιλογή μεθόδου διαχείρισης των ασυρμάτων συνδέσεων. Αυτό το άρθρο καλύπτει και τα δύο μέρη, και παρέχει επιπλέον συνδέσμους που αφορούν εργαλεία διαχείρισης ασύρματων δικτύων.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Οδηγός συσκευής](#Οδηγός_συσκευής)
    *   [1.1 Έλεγχος κατάστασης οδηγού](#Έλεγχος_κατάστασης_οδηγού)
    *   [1.2 Εγκατάσταση οδηγού/firmware](#Εγκατάσταση_οδηγού/firmware)
*   [2 Διαχείριση ασύρματης σύνδεσης](#Διαχείριση_ασύρματης_σύνδεσης)
    *   [2.1 Χειροκίνητη ρύθμιση](#Χειροκίνητη_ρύθμιση)
        *   [2.1.1 Λήψη ορισμένων χρήσιμων πληροφοριών](#Λήψη_ορισμένων_χρήσιμων_πληροφοριών)
        *   [2.1.2 Ενεργοποίηση διεπαφής](#Ενεργοποίηση_διεπαφής)
        *   [2.1.3 Εύρεση Access point](#Εύρεση_Access_point)
        *   [2.1.4 Τρόπος λειτουργίας (Operating mode)](#Τρόπος_λειτουργίας_(Operating_mode))
        *   [2.1.5 Σύνδεση (Association)](#Σύνδεση_(Association))
        *   [2.1.6 Getting an IP address](#Getting_an_IP_address)
        *   [2.1.7 Custom startup scripts/services](#Custom_startup_scripts/services)
            *   [2.1.7.1 Manual wireless connection at boot using systemd and dhcpcd](#Manual_wireless_connection_at_boot_using_systemd_and_dhcpcd)
            *   [2.1.7.2 Systemd with wpa_supplicant and static IP](#Systemd_with_wpa_supplicant_and_static_IP)
    *   [2.2 Automatic setup](#Automatic_setup)
        *   [2.2.1 Netctl](#Netctl)
        *   [2.2.2 Wicd](#Wicd)
        *   [2.2.3 NetworkManager](#NetworkManager)
        *   [2.2.4 WiFi Radar](#WiFi_Radar)
*   [3 Troubleshooting](#Troubleshooting)
    *   [3.1 Rfkill caveat](#Rfkill_caveat)
    *   [3.2 Observing Logs](#Observing_Logs)
    *   [3.3 Power saving](#Power_saving)
    *   [3.4 Failed to get IP address](#Failed_to_get_IP_address)
    *   [3.5 Connection always times out](#Connection_always_times_out)
        *   [3.5.1 Lowering the rate](#Lowering_the_rate)
        *   [3.5.2 Lowering the txpower](#Lowering_the_txpower)
        *   [3.5.3 Setting rts and fragmentation thresholds](#Setting_rts_and_fragmentation_thresholds)
    *   [3.6 Random disconnections](#Random_disconnections)
        *   [3.6.1 Cause #1](#Cause_#1)
        *   [3.6.2 Cause #2](#Cause_#2)
*   [4 Troubleshooting drivers and firmware](#Troubleshooting_drivers_and_firmware)
    *   [4.1 Ralink](#Ralink)
        *   [4.1.1 rt2x00](#rt2x00)
        *   [4.1.2 rt3090](#rt3090)
        *   [4.1.3 rt3290](#rt3290)
        *   [4.1.4 rt3573](#rt3573)
        *   [4.1.5 rt5572](#rt5572)
    *   [4.2 Realtek](#Realtek)
        *   [4.2.1 rtl8192cu](#rtl8192cu)
        *   [4.2.2 rtl8192e](#rtl8192e)
        *   [4.2.3 rtl8188eu](#rtl8188eu)
    *   [4.3 Atheros](#Atheros)
        *   [4.3.1 ath5k](#ath5k)
        *   [4.3.2 ath9k](#ath9k)
            *   [4.3.2.1 ASUS](#ASUS)
    *   [4.4 Intel](#Intel)
        *   [4.4.1 ipw2100 and ipw2200](#ipw2100_and_ipw2200)
        *   [4.4.2 iwlegacy](#iwlegacy)
        *   [4.4.3 iwlwifi](#iwlwifi)
        *   [4.4.4 Disabling LED blink](#Disabling_LED_blink)
        *   [4.4.5 Other Notes](#Other_Notes)
    *   [4.5 Broadcom](#Broadcom)
    *   [4.6 Other drivers/devices](#Other_drivers/devices)
        *   [4.6.1 Tenda w322u](#Tenda_w322u)
        *   [4.6.2 orinoco](#orinoco)
        *   [4.6.3 prism54](#prism54)
        *   [4.6.4 ACX100/111](#ACX100/111)
        *   [4.6.5 zd1211rw](#zd1211rw)
        *   [4.6.6 hostap_cs](#hostap_cs)
    *   [4.7 ndiswrapper](#ndiswrapper)
    *   [4.8 compat-drivers-patched](#compat-drivers-patched)
*   [5 See also](#See_also)

## Οδηγός συσκευής

Ο προεπιλεγμένος πυρήνας του Arch Linux είναι *αρθρωτός*, που σημαίνει πως πολλοί από τους απαιτούμενους από το υλικό σας οδηγοί βρίσκονται στον σκληρό δίσκο σας μετά την εγκατάσταση και είναι διαθέσιμοι ως [modules](/index.php/Kernel_modules "Kernel modules"). Κατά την εκκίνηση o [udev](/index.php/Udev "Udev") παίρνει έναν κατάλογο του υλικού σας και φορτώνει τα απαραίτητα για την λειτουργία του modules (οδηγοί), τα οποία επιτρέπουν την δημιουργία της *διεπαφής* δικτύου.

Ορισμένες υλοποιήσεις ασύρματης κάρτας απαιτούν και την ύπαρξη υλικολογισμικού (firmware) επιπροσθέτως του οδηγού. Πολλά τέτοια υλικολογισμικά πακέτα παρέχονται από το πακέτο [linux-firmware](https://www.archlinux.org/packages/?name=linux-firmware) το οποίο εγκαθίσταται από προεπιλογή, αλλά αν πρόκειται περί ιδιοταγούς-κλειστού, δεν παρέχεται και θα πρέπει να εγκατασταθεί ξεχωριστά. Η διαδικασία αυτή περιγράφεται στο [#Installing driver/firmware](#Installing_driver/firmware).

**Σημείωση:**

*   Ο Udev δεν είναι τέλειος. Αν ένα απαιτούμενο άρθρωμα (module) δεν φορτώνεται κατά την εκκίνηση, απλά [load it manually](/index.php/Kernel_modules#Loading "Kernel modules"). Σημειώστε επίσης πως ο udev περιστασιακά μπορεί να φορτώσει περισσότερους του ενός οδηγούς για το ίδιο υλικό, με αποτέλεσμα την ύπαρξη διένεξης (conflict) εξαιτίας της οποίας δεν θα υπάρξει σωστή ρύθμιση. Βεβαιωθείτε πως έχετε κάνει [blacklist](/index.php/Kernel_modules#Blacklisting "Kernel modules") το αχρείαστο άρθρωμα.
*   Το όνομα της διεπαφής για διαφορετικούς οδηγούς και υλικό ίσως να διαφέρει. Μερικά παραδείγματα είναι `wlan0`, `eth1`, and `ath0`. Δείτε επίσης το [Network configuration#Device names](/index.php/Network_configuration#Device_names "Network configuration").

**Συμβουλή:** Αν και δεν είναι απολύτως απαιτούμενο, είναι καλή ιδέα να εγκαταστήσετε πρώτα τα user-space tools που αναφέρονται στο [#Manual setup](#Manual_setup), ειδικά όταν παρουσιάζονται ορισμένα προβλήματα.

### Έλεγχος κατάστασης οδηγού

Για να ελέγξετε αν ο οδηγός για την κάρτα σας είναι φορτωμένος, ελέγξτε την έξοδο της εντολής `lspci -k`. Θα πρέπει να δείτε κάποιον οδηγό πυρήνα σε χρήση, για παράδειγμα:

 `$ lspci -k` 
```
06:00.0 Network controller: Intel Corporation WiFi Link 5100
	Subsystem: Intel Corporation WiFi Link 5100 AGN
	Kernel driver in use: iwlwifi
	Kernel modules: iwlwifi

```

**Σημείωση:** Η εσωτερική ασύρματη κάρτα σε ορισμένα laptop μπορεί στην πραγματικότητα να είναι συσκευή usb, άρα θα πρέπει να ελέγξετε και την εντολή:

*   `lsusb -v`
*   `dmesg | grep usbcore`, θα πρέπει να δείτε κάτι παρόμοιο με `usbcore: registered new interface driver rtl8187` στην έξοδο.

Επίσης ελέγξτε και την έξοδο της εντολής `ip link` ώστε να διαπιστώσετε αν κάποια ασύρματη διεπαφή ((π.χ. `wlan0`, `wlp2s1`, `ath0`) έχει δημιουργηθεί. Κατόπιν ενεργοποιήστε την με την `ip link set *interface* up`. Για παράδειγμα, υποθέτοντας πως η διεπαφή σας είναι η `wlan0`:

```
# ip link set wlan0 up

```

Αν λάβετε μηνύματα σφάλματος: `SIOCSIFFLAGS: No such file or directory`, είναι σχεδόν βέβαιο πως το υλικό της ασύρματης κάρτα σας απαιτεί firmware ώστε να λειτουργήσει.

Ελέγξτε τα μηνύματα λάθους που αφορούν το firmware:

 `$ dmesg | grep firmware` 
```
[   7.148259] iwlwifi 0000:02:00.0: loaded firmware version 39.30.4.1 build 35138 op_mode iwldvm

```

Αν δεν υπάρχει σχετική έξοδος, ελέγξτε για μηνύματα στην πλήρη έξοδο που αφορά το άρθρωμα (module) που αναγνωρίσατε προηγούμενα, σε αυτό το παράδειγμα το (`iwlwifi` ώστε να εξακριβώσετε σχετικά μηνύματα ή περαιτέρω προβλήματα:

 `$ dmesg | grep iwlwifi` 
```
[   12.342694] iwlwifi 0000:02:00.0: irq 44 for MSI/MSI-X
[   12.353466] iwlwifi 0000:02:00.0: loaded firmware version 39.31.5.1 build 35138 op_mode iwldvm
[   12.430317] iwlwifi 0000:02:00.0: CONFIG_IWLWIFI_DEBUG disabled
...
[   12.430341] iwlwifi 0000:02:00.0: Detected Intel(R) Corporation WiFi Link 5100 AGN, REV=0x6B

```

Αν το module είναι φορτωμένο επιτυχώς και η διεπαφή ενεργή, μπορείτε να παρακάμψετε το παρακάτω τμήμα.

### Εγκατάσταση οδηγού/firmware

Ελέγξτε τις παρακάτω λίστες ώστε να διαπιστώσετε αν η συσκευή σας υποστηρίζεται:

*   Η [Ubuntu Wiki](https://help.ubuntu.com/community/WifiDocs/WirelessCardsSupported) είναι μια καλή λίστα που περιέχει ασύρματε κάρτες οι οποίες υποστηρίζονται είτε από τον πυρήνα του Linux είτε από κάποιον οδηγό που δημιούργησε κάποιος χρήστης καθώς (και το όνομα του οδηγού).
*   Η [Linux Wireless Support](http://linux-wless.passys.nl/) and The Linux Questions' [Hardware Compatibility List](http://www.linuxquestions.org/hcl/index.php?cat=10) (HCL) περιέχει επίσης μια καλή βάση υλικού υποστηριζόμενου από τον πυρήνα Linux.
*   Η [kernel page](http://wireless.kernel.org/en/users/Devices) επιπρόσθετα περιέχει και έναν πίνακα υποστηριζόμενου υλικού.

Αν η ασύρματη κάρτα σας περιέχεται σε κάποια από τις παραπάνω λίστες, ακολουθείστε το τμήμα [#Troubleshooting drivers and firmware](#Troubleshooting_drivers_and_firmware) αυτής της σελίδας, το οποίο περιέχει πληροφορίες για την εγκατάσταση οδηγών και firmware ορισμένων ασύρματων καρτών. Κατόπιν [check the driver status](#Check_the_driver_status) ξανά.

Αν η κάρτα σας δεν περιλαμβάνεται σε κάποια από τις παραπάνω λίστες, είναι πολύ πιθανό να υποστηρίζεται μόνο από τα Windows ορισμένες κάρτες Broadcom, 3com, κλπ). Για αυτές, μπορείτε να δοκιμάσετε να χρησιμοποιήσετε το [ndiswrapper](#ndiswrapper).

## Διαχείριση ασύρματης σύνδεσης

Υποθέτοντας πως ο οδηγός έχει εγκατασταθεί και λειτουργεί σωστά, θα πρέπει να επιλέξετε μια μέθοδο διαχείρισης της ασύρματης σύνδεσής σας. Τα παρακάτω τμήματα θα σας βοηθήσουν να επιλέξετε.

Η μέθοδος και τα απαραίτητα εργαλεία εξαρτώνται από αρκετούς παράγοντες:

*   Η φύση της ρύθμισης διαχείρισης: Από εντελώς χειροκίνητη μέσω τερματικού έως την πλήρη αυτόματη λύση με χρήση γραφικού περιβάλλοντος.
*   Ο τύπος προστασίας (ή η έλλειψή του) που προστατεύει το ασύρματο δίκτυο.
*   Η ανάγκη για διαφορετικά χαρακτηριστικά δικτύου, αν ο υπολογιστής αλλάζει συχνά περιβάλλον (πχ laptop).

**Συμβουλή:**

*   Όποια και αν είναι η επιλογή σας, **θα πρέπει να προσπαθήσετε να συνδεθείτε χρησιμοποιώντας την χειροκίνητη μέθοδο πρώτα**. Αυτό θα σας βοηθήσει να κατανοήσετε τα διαφορετικά βήματα που απαιτούνται και να λύσετε πιθανά προβλήματα.
*   Αν είναι δυνατόν (πχ αν είστε ο διαχειριστής του δικτύου που θα συνδεθείτε), δοκιμάστε να συνδεθείτε χωρίς προστασία, ώστε να διαπιστώσετε πως όλα λειτουργούν. Κατόπιν δοκιμάστε είτε την μέθοδο προστασίας WEP (απλή στην ρύθμισή της, αλλά που πολύ εύκολα παρακάμπτεται), WPA ή WPA2.

Ο παρακάτω πίνακας δείχνει τις διαφορετικές μεθόδους που είναι δυνατόν να χρησιμοποιηθούν ώστε να ενεργοποιήσετε και να διαχειριστείτε μια ασύρματη σύνδεση, εξαρτώμενη από τον τύπο προστασίας και διαχείρισης, και τα απαραίτητα εργαλεία που απαιτούνται. Αν κει είναι δυνατόν να υπάρξουν και άλλοι συνδυασμοί, αυτοί είναι οι συχνότερα χρησιμοποιούμενοι:

| Μέθοδος διαχείρησης | Ενεργοποίηση διεπαφής | Διαχείριση ασύρματης σύνδεσης
(/=alternatives) | Απόδοση διεύθυνσης IP
(/=εναλλακτικά) |
| [Manually managed](#Manual_setup),
χωρίς ή με WEP προστασία | [ip](/index.php/Core_utilities#ip "Core utilities") | [iw](https://www.archlinux.org/packages/?name=iw) / [iwconfig](https://www.archlinux.org/packages/?name=wireless_tools) | [ip](/index.php/Core_utilities#ip "Core utilities") / [dhcpcd](https://www.archlinux.org/packages/?name=dhcpcd) / [dhclient](https://www.archlinux.org/packages/?name=dhclient) |
| [Manually managed](#Manual_setup),
με WPA ή WPA2 PSK προστασία | [ip](/index.php/Core_utilities#ip "Core utilities") | [iw](https://www.archlinux.org/packages/?name=iw) / [iwconfig](https://www.archlinux.org/packages/?name=wireless_tools) + [wpa_supplicant](/index.php/WPA_supplicant "WPA supplicant") | [ip](/index.php/Core_utilities#ip "Core utilities") / [dhcpcd](https://www.archlinux.org/packages/?name=dhcpcd) / [dhclient](https://www.archlinux.org/packages/?name=dhclient) |
| [Automatically managed](#Automatic_setup),
με υποστήριξη προφίλ δικτύου | [netctl](/index.php/Netctl "Netctl"), [Wicd](/index.php/Wicd "Wicd"), [NetworkManager](/index.php/NetworkManager "NetworkManager"), etc.

Αυτά τα εργαλεία, τραβούν και τις απαραίτητες εξαρτήσεις από την λίστα των πακέτων που αφορούν την χειροκίνητη μέθοδο.

 |

### Χειροκίνητη ρύθμιση

Όπως όλα οι άλλες διεπαφές δικτύου, έτσι και οι ασύρματες ελέγχονται με την `ip` από το πακέτο [iproute2](https://www.archlinux.org/packages/?name=iproute2). Το πακέτο [wireless_tools](https://www.archlinux.org/packages/?name=wireless_tools) παρέχει μια βασική δέσμη εργαλείων για τον έλεγχο των ασύρματων συνδέσεων, ωστόσο αυτά τα εργαλεία θεωρούνται ξεπερασμένα προς χάριν του εργαλείου [iw](https://www.archlinux.org/packages/?name=iw). Αν το *iw* δεν συνεργάζεται με την ασύρματη κάρτα σας, μπορείτε να χρησιμοποιήσετε τα *wireless_tools*, ο παρακάτω πίνακας δίνει μια σύνοψη των συγκρίσιμων εντολών τους (δείτε [[1]](http://wireless.kernel.org/en/users/Documentation/iw/replace-iwconfig) για περισσότερα παραδείγματα). Επιπρόσθετα, το πακέτο [wpa_supplicant](https://www.archlinux.org/packages/?name=wpa_supplicant) απαιτείται για την χρησιμοποίηση WPA/WPA2 προστασία. Αυτά τα δυνατά εργαλεία για τον χώρο του χρήστη, δουλεύουν εξαιρετικά καλά και επιτρέπουν τον πλήρη χειροκίνητο έλεγχο της ασύρματης σύνδεσης.

**Σημείωση:**

*   τα παραδείγματα σε αυτό το τμήμα λαμβάνουν δεδομένο πως η ασύρματη διεπαφή σας είναι η `wlan0` και πως είστε συνδεδεμένος στο δικό σας `*your_essid*` router. Αντικαταστήστε και τα δύο αναλόγως.
*   Σημειώστε πως οι περισσότερες εντολές θα πρέπει να εκτελεστούν με τον λογαριασμό του root ([root permissions](/index.php/Users_and_groups "Users and groups")). Αν εκτελεστούν με λογαριασμό χρήστη, μερικές από αυτές (πχ *iwlist*), θα δώσουν έξοδο χωρίς σφάλμα αλλά δεν θα δώσουν και σωστές πληροφορίες, πράγμα που θα προκαλέσει σύγχυση.

| *iw* command | *wireless_tools* command | Description |
| iw dev wlan0 link | iwconfig wlan0 | Getting link status. |
| iw dev wlan0 scan | iwlist wlan0 scan | Scanning for available access points. |
| iw dev wlan0 set type ibss | iwconfig wlan0 mode ad-hoc | Setting the operation mode to *ad-hoc*. |
| iw dev wlan0 connect *your_essid* | iwconfig wlan0 essid *your_essid* | Connecting to open network. |
| iw dev wlan0 connect *your_essid* 2432 | iwconfig wlan0 essid *your_essid* freq 2432M | Connecting to open network specifying channel. |
| iw dev wlan0 connect *your_essid* key 0:*your_key* | iwconfig wlan0 essid *your_essid* key *your_key* | Connecting to WEP encrypted network using hexadecimal key. |
| iw dev wlan0 connect *your_essid* key 0:*your_key* | iwconfig wlan0 essid *your_essid* key s:*your_key* | Connecting to WEP encrypted network using ASCII key. |
| iw dev wlan0 set power_save on | iwconfig wlan0 power on | Enabling power save. |

**Σημείωση:** Εξαρτώμενο από το υλικό σας και τον τύπο προστασίας που χρησιμοποιείται, μερικά βήματα ίσως να μην είναι απαραίτητα. Ορισμένες κάρτες είναι γνωστό πως απαιτούν ενεργοποίηση διεπαφής ή/και σάρωση δικτύου πριν γίνει εφικτό να συνεργαστούν με το router σας και να λάβουν διεύθυνση ip. ίσως να χρειάζεται να πειραματιστείτε λίγο. Για παράδειγμα, χρήστες με προστασία WPA/WPA2 είναι δυνατόν να δοκιμάσουν να ενεργοποιήσουν απευθείας το ασύρματο δίκτυό τους από το βήμα [#Association]].

#### Λήψη ορισμένων χρήσιμων πληροφοριών

**Συμβουλή:** Δείτε το [official documentation](http://wireless.kernel.org/en/users/Documentation/iw) που αφορά το *iw* εργαλείο για περισσότερα παραδείγματα.

*   Πρώτα θα πρέπει να βρείτε το όνομα της ασύρματης διεπαφής σας. Αυτό μπορείτε να το πετύχετε με την παρακάτω εντολή:

 `$ iw dev` 
```
phy#0
	Interface **wlan0**
		ifindex 3
		wdev 0x1
		addr 12:34:56:78:9a:bc
		type managed
		channel 1 (2412 MHz), width: 40 MHz, center1: 2422 MHz

```

*   Για να ελέγξετε την κατάσταση της σύνδεσης, χρησιμοποιείστε την παρακάτω. Παράδειγμα εξόδου όταν δεν είναι συνδεδεμένη σε κάποιο router:

 `$ iw dev wlan0 link` 
```
Not connected.

```

Ενώ όταν είναι συνδεδεμένη θα δείτε κάτι παρόμοιο με:

 `$ iw dev wlan0 link` 
```
Connected to 12:34:56:78:9a:bc (on wlan0)
	SSID: MyESSID
	freq: 2412
	RX: 33016518 bytes (152703 packets)
	TX: 2024638 bytes (11477 packets)
	signal: -53 dBm
	tx bitrate: 150.0 MBit/s MCS 7 40MHz short GI

	bss flags:	short-preamble short-slot-time
	dtim period:	1
	beacon int:	100

```

*   Μπορείτε να πάρετε πληροφορίες, όπως το ποσό των tx/rx bytes, την ένταση σήματος κλπ, με την ακόλουθη εντολή:

 `$ iw dev wlan0 station dump` 
```
Station 12:34:56:78:9a:bc (on wlan0)
	inactive time:	1450 ms
	rx bytes:	24668671
	rx packets:	114373
	tx bytes:	1606991
	tx packets:	8557
	tx retries:	623
	tx failed:	1425
	signal:  	-52 dBm
	signal avg:	-53 dBm
	tx bitrate:	150.0 MBit/s MCS 7 40MHz short GI
	authorized:	yes
	authenticated:	yes
	preamble:	long
	WMM/WME:	yes
	MFP:		no
	TDLS peer:	no

```

#### Ενεργοποίηση διεπαφής

*(Προαιρετικό, αλλά ίσως να απαιτείται)*

Ορισμένες κάρτες ασύρματης δικτύωσης, απαιτούν να ενεργοποιηθεί η διεπαφή πυρήνα πριν να είστε σε θέση να χρησιμοποιήσετε τα εργαλεία *iw* ή *wireless_tools*:

```
# ip link set wlan0 up

```

**Σημείωση:** Αν λάβετε λάθη όπως `RTNETLINK answers: Operation not possible due to RF-kill`, σιγουρευτείτε πως έχετε στην θέση *on* τον διακόπτη ενεργοποίησης υλικού. Δείτε επίσης [#Rfkill caveat](#Rfkill_caveat) για λεπτομέρειες.

#### Εύρεση Access point

Για να δείτε ποια ασύρματα δίκτυα είναι διαθέσιμα:

```
# iw dev wlan0 scan | less

```

**Σημείωση:** Αν η έξοδος είναι `Interface doesn't support scanning`, τότε πιθανότατα έχετε ξεχάσει να εγκαταστήσετε το αντίστοιχο firmware. Σε ορισμένες περιπτώσεις το ίδιο λάθος εμφανίζεται αν δεν τρέχετε την εντολή *iw* με τον λογαριασμό του root.

Τα σημαντικά προς έλεγχο σημεία:

*   **SSID:** το όνομα του δικτύου.
*   **Signal:** αναφέρεται σε αναλογία με την ένταση του ασύρματου σε dbm (πχ από -100 σε 0). Όσο πιο κοντά είναι στο 0, τόσο καλύτερο είναι το σήμα σας. Αν παρατηρήσετε την αναφερόμενη ένταση σε μια καλής ποιότητας σύνδεσης και σε μιας με κακή, θα έχετε μαι ιδέα για τα επιμέρους μεγέθη.
*   **Security:** δεν αναφέρεται άμεσα, ελέγξτε την γραμμή που ξεκινά με `capability`. Αν υπάρχει `Privacy`, για παράδειγμα `capability: ESS Privacy ShortSlotTime (0x0411)`, τότε το δίκτυο είναι προστατευμένο με κάποιον τρόπο.
    *   Αν δείτε ένα τμήμα πληροφοριών `RSN`, τότε το δίκτυο είναι προστατευμένο με πρωτόκολλο [Wi-Fi Protected Access](https://en.wikipedia.org/wiki/Wi-Fi_Protected_Access "wikipedia:Wi-Fi Protected Access") γνωστού και ως WPA2.
    *   Αν δείτε ένα τμήμα πληροφοριών `WPA`, τότε το δίκτυο είναι προστατευμένο με πρωτόκολλο [Wi-Fi Protected Access](https://en.wikipedia.org/wiki/Wi-Fi_Protected_Access "wikipedia:Wi-Fi Protected Access").

*   *   Στα τμήματα `RSN` και `WPA` μπορείτε να βρείτε τις παρακάτω πληροφορίες:
        *   **Ομάδα κρυπτογράφησης (Group cipher):** τιμή σε TKIP, CCMP, και τα δύο, άλλο.
        *   **Κρυπτογράφηση ζεύγους (Pairwise ciphers):** τιμή σε TKIP, CCMP, και τα δύο, άλλο. Όχι απαραίτητα ίδια τιμή με την τιμή της ομάδας κρυυπτογράφησης.
        *   **Έλεγχος ταυτότητας (Authentication suites):** τιμή σε PSK, 802.1x, άλλο. Προκειμένου για οικιακό router, συνήθως βρίσκετε PSK (πχ συνθηματική φράση). Σε δίκτυα πανεπιστημίων, συνήθως βρίσκεται κρυπτογράφηση 802.1x που απαιτεί είσοδο με όνομα χρήστη και κωδικό εισόδου. Κατόπιν θα πρέπει να γνωρίζετε ποια διαχείριση κλειδιού χρησιμοποιεί (πχ ΕΑΡ) καθώς και τον τύπο ενθυλάκωσης (encapsulation) (πχ ΡΕΑΡ). Βρείτε περισσότερες πληροφορίες στο [Wikipedia:Authentication protocol](https://en.wikipedia.org/wiki/Authentication_protocol "wikipedia:Authentication protocol") και στα περιεχόμενα άρθρα.
    *   Αν δεν δείτε `RSN` ή `WPA` τμήματα αλλά υπάρχει ένδειξη `Ιδιωτικό`, τότε σε χρήση είναι η μέθοδος κρυπτογράφησης WEP.

#### Τρόπος λειτουργίας (Operating mode)

*(Προαιρετικό, αλλά ίσως να απαιτείται)*

Σε αυτό το βήμα ίσως θα πρέπει να ορίσετε τον σωστό τρόπο λειτουργίας της ασύρματης κάρτας. Συγκεκριμένα, αν πρόκειται να συνδεθείτε σε ένα [ad-hoc network](/index.php/Ad-hoc_networking "Ad-hoc networking"), πρέπει να θέσετε τον τρόπο λειτουργίας σε `ibss`:

```
# iw dev wlan0 set type ibss

```

**Σημείωση:** Για να αλλάξετε τον τρόπο λειτουργίας σε ορισμένες κάρτες ίσως να απαιτεί να *απενεργοποιηθεί* (`ip link set wlan0 down`).

#### Σύνδεση (Association)

Αναλόγως της προστασίας, πρέπει να συνδέσετε την ασύρματη κάρτα σας με το σημείο πρόσβασης (access point) ώστε να είστε σε θέση να χρησιμοποιήσετε και να περάσετε το κλειδί προστασίας.

*   **Χωρίς προστασία**

```
# iw dev wlan0 connect *your_essid*

```

*   **WEP**

χρησιμοποιώντας ένα κλειδί δεκαεξαδικό ή ASCII (η μορφή είναι άμεσα διακριτή διότι το κλειδί που αφορά προστασία WEP είναι σταθερού αριθμού χαρακτήρων):

```
# iw dev wlan0 connect *your_essid* key 0:*your_key*

```

χρησιμοποιώντας ένα κλειδί δεκαεξαδικό ή ASCII, ορίζετε το τρίτο κλειδί ως προεπιλεγμένο (η αρίθμηση ξεκινά από το 0, μέχρι τέσσερα είναι δυνατόν:

```
# iw dev wlan0 connect *your_essid* key d:2:*your_key*

```

*   **WPA/WPA2**

Πρέπει να επεξεργαστείτε το αρχείο `/etc/wpa_supplicant.conf` όπως περιγράφεται στο [WPA supplicant](/index.php/WPA_supplicant "WPA supplicant") σύμφωνα με το τι έχετε βρει από το [#Access point discovery](#Access_point_discovery). Κατόπιν δώστε την παρακάτω εντολή:

```
# wpa_supplicant -i wlan0 -c /etc/wpa_supplicant.conf

```

[Opanos](/index.php/User:Opanos "User:Opanos") ([talk](/index.php?title=User_talk:Opanos&action=edit&redlink=1 "User talk:Opanos (page does not exist)")) 09:58, 20 December 2013 (UTC)

This is assuming your device uses the `wext` driver. If this does not work, you may need to adjust these options. If connected successfully, continue in a new terminal (or quit `wpa_supplicant` with `Ctrl+c` and add the `-B` switch to the above command to run it in the background). [WPA supplicant](/index.php/WPA_supplicant "WPA supplicant") contains more information and troubleshooting.

Regardless of the method used, you can check if you have associated successfully:

```
# iw dev wlan0 link

```

#### Getting an IP address

**Note:** See [Network configuration#Configure the IP address](/index.php/Network_configuration#Configure_the_IP_address "Network configuration") for more examples. This part is identical.

Finally, provide an IP address to the network interface. Simple examples are:

```
# dhcpcd wlan0

```

or

```
# dhclient wlan0

```

for DHCP, or

```
# ip addr add 192.168.0.2/24 dev wlan0
# ip route add default via 192.168.0.1

```

for static IP addressing.

**Tip:** [dhcpcd](https://www.archlinux.org/packages/?name=dhcpcd) contains a hook (enabled by default) to automatically launch [WPA supplicant](/index.php/WPA_supplicant "WPA supplicant") on wireless interfaces. It is started only if a configuration file at `/etc/wpa_supplicant.conf` exists and no *wpa_supplicant* process is listening on that interface. In most cases, you do not need to create any [custom service](#Manual_wireless_connection_at_boot_using_systemd_and_dhcpcd), just enable `dhcpcd@*interface*`.

#### Custom startup scripts/services

Although the manual configuration method will help troubleshoot wireless problems, you will have to re-type every command each time you reboot. You can also quickly write a shell script to automate the whole process, which is still a quite convenient way of managing network connection while keeping full control over your configuration. You can find some examples in this section.

##### Manual wireless connection at boot using systemd and dhcpcd

This example uses [systemd](/index.php/Systemd "Systemd") for start up, [WPA supplicant](/index.php/WPA_supplicant "WPA supplicant") for connecting, and [dhcpcd](https://www.archlinux.org/packages/?name=dhcpcd) for assigning an IP address.

**Note:** Make sure that [wpa_supplicant](https://www.archlinux.org/packages/?name=wpa_supplicant) is installed and create `/etc/wpa_supplicant.conf`. See [WPA supplicant](/index.php/WPA_supplicant "WPA supplicant") for details.

Create a systemd unit, e.g `/etc/systemd/system/network-wireless@.service`:

 `/etc/systemd/system/network-wireless@.service` 
```
[Unit]
Description=Wireless network connectivity (%i)
Wants=network.target
Before=network.target
BindsTo=sys-subsystem-net-devices-%i.device
After=sys-subsystem-net-devices-%i.device

[Service]
Type=oneshot
RemainAfterExit=yes

ExecStart=/usr/bin/ip link set dev %i up
ExecStart=/usr/bin/wpa_supplicant -B -i %i -c /etc/wpa_supplicant.conf
ExecStart=/usr/bin/dhcpcd %i

ExecStop=/usr/bin/ip link set dev %i down

[Install]
WantedBy=multi-user.target

```

Enable the unit and start it, passing the name of the interface:

```
# systemctl enable network-wireless@wlan0.service
# systemctl start network-wireless@wlan0.service

```

##### Systemd with wpa_supplicant and static IP

**Note:** Make sure that [wpa_supplicant](https://www.archlinux.org/packages/?name=wpa_supplicant) is installed and create `/etc/wpa_supplicant.conf`. See [WPA supplicant](/index.php/WPA_supplicant "WPA supplicant") for details.

First create configuration file for the [systemd](/index.php/Systemd "Systemd") service, replace `*interface*` with proper interface name:

 `/etc/conf.d/network-wireless@*interface*` 
```
address=192.168.0.10
netmask=24
broadcast=192.168.0.255
gateway=192.168.0.1

```

Create a systemd unit file:

 `/etc/systemd/system/network-wireless@.service` 
```
[Unit]
Description=Wireless network connectivity (%i)
Wants=network.target
Before=network.target
BindsTo=sys-subsystem-net-devices-%i.device
After=sys-subsystem-net-devices-%i.device

[Service]
Type=oneshot
RemainAfterExit=yes
EnvironmentFile=/etc/conf.d/network-wireless@%i

ExecStart=/usr/bin/ip link set dev %i up
ExecStart=/usr/bin/wpa_supplicant -B -i %i -c /etc/wpa_supplicant.conf
ExecStart=/usr/bin/ip addr add ${address}/${netmask} broadcast ${broadcast} dev %i
ExecStart=/usr/bin/ip route add default via ${gateway}

ExecStop=/usr/bin/ip addr flush dev %i
ExecStop=/usr/bin/ip link set dev %i down

[Install]
WantedBy=multi-user.target

```

Enable the unit and start it, passing the name of the interface:

```
# systemctl enable network-wireless@wlan0.service
# systemctl start network-wireless@wlan0.service

```

### Automatic setup

There are many solutions to choose from, but remember that all of them are mutually exclusive; you should not run two daemons simultaneously. The following table compares the different connection managers, additional notes are in subsections below.

| Connection manager | Network
profiles
support | Roaming
(auto connect dropped
or changed location) | [PPP](https://en.wikipedia.org/wiki/point-to-point_protocol "wikipedia:point-to-point protocol") support
(e.g. 3G modem) | Official
GUI | Console tools |
| [ConnMan](/index.php/ConnMan "ConnMan") | Yes | Yes | Yes | No | `connmanctl` |
| [Netctl](/index.php/Netctl "Netctl") | Yes | Yes | Yes | No | `netctl`,`wifi-menu` |
| [NetworkManager](/index.php/NetworkManager "NetworkManager") | Yes | Yes | Yes | Yes | `nmcli` |
| [Wicd](/index.php/Wicd "Wicd") | Yes | Yes | No | Yes | `wicd-curses` |

#### Netctl

*netctl* is a replacement for *netcfg* designed to work with systemd. It uses a profile based setup and is capable of detection and connection to a wide range of network types. This is no harder than using graphical tools.

See: [Netctl](/index.php/Netctl "Netctl")

#### Wicd

Wicd is a network manager that can handle both wireless and wired connections. It is written in Python and Gtk with fewer dependencies than NetworkManager, making it an ideal solution for lightweight desktop users. Wicd is available in the [official repositories](/index.php/Official_repositories "Official repositories").

See: [Wicd](/index.php/Wicd "Wicd")

**Note:** [wicd](/index.php/Wicd "Wicd") may cause excessive dropped connections with some drivers, while [NetworkManager](/index.php/NetworkManager "NetworkManager") might work better.

#### NetworkManager

NetworkManager is an advanced network management tool that is enabled by default in most popular GNU/Linux distributions. In addition to managing wired connections, NetworkManager provides worry-free wireless roaming with an easy-to-use GUI program for selecting your desired network.

See: [NetworkManager](/index.php/NetworkManager "NetworkManager")

**Note:** GNOME's [network-manager-applet](https://www.archlinux.org/packages/?name=network-manager-applet) also works under [Xfce](/index.php/Xfce "Xfce") if you install [xfce4-xfapplet-plugin](https://aur.archlinux.org/packages/xfce4-xfapplet-plugin/) (available in the [AUR](/index.php/Arch_User_Repository "Arch User Repository")) first. Additionally, there are applets available for [KDE](/index.php/KDE "KDE").

#### WiFi Radar

WiFi Radar is a Python/PyGTK2 utility for managing wireless (and **only** wireless) profiles. It enables you to scan for available networks and create profiles for your preferred networks.

See: [Wifi Radar](/index.php/Wifi_Radar "Wifi Radar")

## Troubleshooting

This section contains general troubleshooting tips, not strictly related to problems with drivers or firmware. For such topics, see next section.

### Rfkill caveat

Many laptops have a hardware button (or switch) to turn off wireless card, however, the card can also be blocked by kernel. This can be handled by rfkill. Use *rfkill* to show the current status:

 `# rfkill list` 
```
0: phy0: Wireless LAN
	Soft blocked: yes
	Hard blocked: yes

```

If the card is *hard-blocked*, use the hardware button (switch) to unblock it. If the card is not *hard-blocked* but *soft-blocked*, use the following command:

```
# rfkill unblock wifi

```

**Note:** It is possible that the card will go from *hard-blocked* and *soft-unblocked* state into *hard-unblocked* and *soft-blocked* state by pressing the hardware button (i.e. the *soft-blocked* bit is just switched no matter what). This can be adjusted by tuning some options of the `rfkill` [kernel module](/index.php/Kernel_modules "Kernel modules").

More info: [http://askubuntu.com/questions/62166/siocsifflags-operation-not-possible-due-to-rf-kill](http://askubuntu.com/questions/62166/siocsifflags-operation-not-possible-due-to-rf-kill)

### Observing Logs

A good first measure to troubleshoot is to analyze the system's logfiles first. In order not to manually parse through them all, it can help to open a second terminal/console window and watch the kernels messages with

```
$ dmesg -w

```

while performing the action, e.g. the wireless association attempt.

When using a tool for network management, the same can be done for systemd with

```
# journalctl -f 

```

The individual tools used in this article further provide options for more detailed debugging output, which can be used in a second step of the analysis, if required.

### Power saving

See [Power saving#Network interfaces](/index.php/Power_saving#Network_interfaces "Power saving").

### Failed to get IP address

*   If getting an IP address repeatedly fails using the default [dhcpcd](https://www.archlinux.org/packages/?name=dhcpcd) client, try installing and using [dhclient](https://www.archlinux.org/packages/?name=dhclient) instead. Do not forget to select *dhclient* as the primary DHCP client in your [connection manager](#Automatic_setup)!

*   If you can get an IP address for a wired interface and not for a wireless interface, try disabling the wireless card's power saving features:

```
# iwconfig wlan0 power off

```

*   If you get a timeout error due to a *waiting for carrier* problem, then you might have to set the channel mode to `auto` for the specific device:

```
# iwconfig wlan0 channel auto

```

Before changing the channel to auto, make sure your wireless interface is down. After it has successfully changed it, you can bring the interface up again and continue from there.

### Connection always times out

The driver may suffer from a lot of tx excessive retries and invalid misc errors for some unknown reason, resulting in a lot of packet loss and keep disconnecting, sometimes instantly. Following tips might be helpful.

#### Lowering the rate

Try setting lower rate, for example 5.5M:

```
# iwconfig wlan0 rate 5.5M auto

```

Fixed option should ensure that the driver does not change the rate on its own, thus making the connection a bit more stable:

```
# iwconfig wlan0 rate 5.5M fixed

```

#### Lowering the txpower

You can try lowering the transmit power as well. This may save power as well:

```
# iwconfig wlan0 txpower 5

```

Valid settings are from `0` to `20`, `auto` and `off`.

#### Setting rts and fragmentation thresholds

Default iwconfig options have rts and fragmentation thresholds off. These options are particularly useful when there are many adjacent APs or in a noisy environment.

The minimum value for fragmentation value is 256 and maximum is 2346\. In many windows drivers the maximum is the default value:

```
# iwconfig wlan0 frag 2346

```

For rts minimum is 0, maximum is 2347\. Once again windows drivers often use maximum as the default:

```
# iwconfig wlan0 rts 2347

```

### Random disconnections

#### Cause #1

If dmesg says `wlan0: deauthenticating from MAC by local choice (reason=3)` and you lose your Wi-Fi connection, it is likely that you have a bit too aggressive power-saving on your Wi-Fi card[[2]](http://us.generation-nt.com/answer/gentoo-user-wireless-deauthenticating-by-local-choice-help-204640041.html). Try disabling the wireless card's power-saving features:

```
# iwconfig wlan0 power off

```

See [Power saving](/index.php/Power_saving "Power saving") for tips on how to make it permanent (just specify `off` instead of `on`).

If your card does not support `iwconfig wlan0 power off`, check the **BIOS** for power management options. Disabling PCI-Express power management in the BIOS of a Lenovo W520 resolved this issue.

#### Cause #2

If you are experiencing frequent disconnections and dmesg shows messages such as

`ieee80211 phy0: wlan0: No probe response from AP xx:xx:xx:xx:xx:xx after 500ms, disconnecting`

try changing the channel bandwidth to `20MHz` through your router's settings page.

## Troubleshooting drivers and firmware

This section covers methods and procedures for installing kernel modules and *firmware* for specific chipsets, that differ from generic method.

See [Kernel modules](/index.php/Kernel_modules "Kernel modules") for general informations on operations with modules.

### Ralink

#### rt2x00

Unified driver for Ralink chipsets (it replaces `rt2500`, `rt61`, `rt73`, etc). This driver has been in the Linux kernel since 2.6.24, you only need to load the right module for the chip: `rt2400pci`, `rt2500pci`, `rt2500usb`, `rt61pci` or `rt73usb` which will autoload the respective `rt2x00` modules too.

A list of devices supported by the modules is available at the project's [homepage](http://rt2x00.serialmonkey.com/wiki/index.php/Hardware).

	Additional notes

*   Since kernel 3.0, rt2x00 includes also these drivers: `rt2800pci`, `rt2800usb`.
*   Since kernel 3.0, the staging drivers `rt2860sta` and `rt2870sta` are replaced by the mainline drivers `rt2800pci` and `rt2800usb`.
*   Some devices have a wide range of options that can be configured with `iwpriv`. These are documented in the [source tarballs](http://web.ralinktech.com/ralink/Home/Support/Linux.html) available from Ralink.

#### rt3090

For devices which are using the rt3090 chipset it should be possible to use `rt2800pci` driver, however, is not working with this chipset very well (e.g. sometimes it's not possible to use higher rate than 2Mb/s).

The best way is to use the [rt3090](https://aur.archlinux.org/packages/rt3090/) driver from [AUR](/index.php/AUR "AUR"). Make sure to [blacklist](/index.php/Kernel_modules#Blacklisting "Kernel modules") the `rt2800pci` module and setup the `rt3090sta` module to [load](/index.php/Kernel_modules#Loading "Kernel modules") at boot.

**Note:** This driver also works with rt3062 chipsets.

#### rt3290

The rt3290 chipset is recognised by the kernel `rt2800pci` module. However, some users experience problems and reverting to a patched Ralink driver seems to be beneficial in these [cases](https://bbs.archlinux.org/viewtopic.php?id=161952).

#### rt3573

New chipset as of 2012\. It may require proprietary drivers from Ralink. Different manufacturers use it, see the [Belkin N750 DB wireless usb adapter](https://bbs.archlinux.org/viewtopic.php?pid=1164228#p1164228) forums thread.

#### rt5572

New chipset as of 2012 with support for 5 Ghz bands. It may require proprietary drivers from Ralink and some effort to compile them. At the time of writing a how-to on compilation is available for a DLINK DWA-160 rev. B2 [here](http://bernaerts.dyndns.org/linux/229-ubuntu-precise-dlink-dwa160-revb2).

### Realtek

#### rtl8192cu

The driver is now in the kernel, but many users have reported being unable to make a connection although scanning for networks does work.

The [dkms-8192cu](https://aur.archlinux.org/packages/dkms-8192cu/) package in the AUR may be a better choice for some users.

#### rtl8192e

The driver is part of the current kernel package. The module initialization may fail at boot giving this error message:

```
rtl819xE:ERR in CPUcheck_firmware_ready()
rtl819xE:ERR in init_firmware() step 2
rtl819xE:ERR!!! _rtl8192_up(): initialization is failed!
r8169 0000:03:00.0: eth0: link down

```

A workaround is to simply unload the module:

```
# modprobe -r r8192e_pci

```

and reload the module (after a pause):

```
# modprobe r8192e_pci

```

#### rtl8188eu

Some dongles, like the TP-Link TL-WN725N v2 (not sure, but it seems that uses the rtl8179 chipset), use chipsets compatible with this driver. In order to use it you have to install the [dkms-8188eu](https://aur.archlinux.org/packages/dkms-8188eu/) package in the AUR.

### Atheros

The [MadWifi team](http://madwifi-project.org/) currently maintains three different drivers for devices with Atheros chipset:

*   `madwifi` is an old, obsolete driver. Not present in Arch kernel since 2.6.39.1.
*   `ath5k` is newer driver, which replaces the `madwifi` driver. Currently a better choice for some chipsets, but not all chipsets are supported (see below)
*   `ath9k` is the newest of these three drivers, it is intended for newer Atheros chipsets. All of the chips with 802.11n capabilities are supported.

There are some other drivers for some Atheros devices. See [Linux Wireless documentation](http://wireless.kernel.org/en/users/Drivers/Atheros#PCI_.2F_PCI-E_.2F_AHB_Drivers) for details.

#### ath5k

External resources:

*   [http://wireless.kernel.org/en/users/Drivers/ath5k](http://wireless.kernel.org/en/users/Drivers/ath5k)
*   [http://wiki.debian.org/ath5k](http://wiki.debian.org/ath5k)

If you find web pages randomly loading very slow, or if the device is unable to lease an IP address, try to switch from hardware to software encryption by loading the `ath5k` module with `nohwcrypt=1` option. See [Kernel modules#Options](/index.php/Kernel_modules#Options "Kernel modules") for details.

Some laptops may have problems with their wireless LED indicator flickering red and blue. To solve this problem, do:

```
# echo none > /sys/class/leds/ath5k-phy0::tx/trigger
# echo none > /sys/class/leds/ath5k-phy0::rx/trigger

```

For alternatives, see [this bug report](https://bugzilla.redhat.com/show_bug.cgi?id=618232).

#### ath9k

External resources:

*   [http://wireless.kernel.org/en/users/Drivers/ath9k](http://wireless.kernel.org/en/users/Drivers/ath9k)
*   [http://wiki.debian.org/ath9k](http://wiki.debian.org/ath9k)

In the unlikely event that you have stability issues that trouble you, you could try using the [compat-wireless](http://wireless.kernel.org/en/users/Download) package. An [ath9k mailing list](https://lists.ath9k.org/mailman/listinfo/ath9k-devel) exists for support and development related discussions.

##### ASUS

With some ASUS laptops (tested with ASUS U32U series), it could help to add `options asus_nb_wmi wapf=1` to `/etc/modprobe.d/asus_nb_wmi.conf` to fix rfkill-related issues.

### Intel

#### ipw2100 and ipw2200

These modules are fully supported in the kernel, but they require additional firmware. Depending on which of the chipsets you have, [install](/index.php/Pacman "Pacman") either [ipw2100-fw](https://www.archlinux.org/packages/?name=ipw2100-fw) or [ipw2200-fw](https://www.archlinux.org/packages/?name=ipw2200-fw). Then [reload](/index.php/Kernel_modules#Manual_module_handling "Kernel modules") the appropriate module.

**Tip:** You may use the following [module options](/index.php/Kernel_modules#Setting_module_options "Kernel modules"):

*   use the `rtap_iface=1` option to enable the radiotap interface
*   use the `led=1` option to enable a front LED indicating when the wireless is connected or not

#### iwlegacy

[iwlegacy](http://wireless.kernel.org/en/users/Drivers/iwlegacy) is the wireless driver for Intel's 3945 and 4965 wireless chips. The firmware is included in the [linux-firmware](https://www.archlinux.org/packages/?name=linux-firmware) package.

[udev](/index.php/Udev "Udev") should load the driver automatically, otherwise load `iwl3945` or `iwl4965` manually. See [Kernel modules#Loading](/index.php/Kernel_modules#Loading "Kernel modules") for details.

#### iwlwifi

[iwlwifi](http://wireless.kernel.org/en/users/Drivers/iwlwifi) is the wireless driver for Intel's current wireless chips, such as 5100AGN, 5300AGN, and 5350AGN. See the [full list of supported devices](http://wireless.kernel.org/en/users/Drivers/iwlwifi#Supported_Devices). The firmware is included in the [linux-firmware](https://www.archlinux.org/packages/?name=linux-firmware) package.

If you have problems connecting to networks in general or your link quality is very poor, try to disable 802.11n and enable software encryption:

 `/etc/modprobe.d/iwlwifi.conf` 
```
options iwlwifi 11n_disable=1
options iwlwifi swcrypto=1
```

#### Disabling LED blink

**Note:** This works with the `iwlegacy` and `iwlwifi` drivers.

The default settings on the module are to have the LED blink on activity. Some people find this extremely annoying. To have the LED on solid when Wi-Fi is active, you can use the [systemd-tmpfiles](/index.php/Systemd#Temporary_files "Systemd"):

 `/etc/tmpfiles.d/phy0-led.conf` 
```
w /sys/class/leds/phy0-led/trigger - - - - phy0radio

```

Run `systemd-tmpfiles --create phy0-led.conf` for the change to take effect, or reboot.

To see all the possible trigger values for this LED:

```
# cat /sys/class/leds/phy0-led/trigger

```

**Tip:** If you do not have `/sys/class/leds/phy0-led`, you may try to use the `led_mode="1"` [module option](/index.php/Kernel_modules#Setting_module_options "Kernel modules"). It should be valid for both `iwlwifi` and `iwlegacy` drivers.

#### Other Notes

*   By default, `iwl3945` is configured to only work with networks on channels 1-11\. Higher frequency bands are not allowed in some parts of the world (e.g. the US). In the EU however, channels 12 and 13 are used quite commonly (and Japan allows for channel 14). To make `iwl3945` scan for all channels, add `options cfg80211 ieee80211_regdom=EU` to `/etc/modprobe.d/modprobe.conf`. With `iwlist frequency` you can check which channels are allowed.
*   If you want to enable more channels on Intel Wifi 5100 (and quite possible other cards too), you can do that with the [crda](https://www.archlinux.org/packages/?name=crda) package. After installing the package, edit `/etc/conf.d/wireless-regdom` and uncomment the line where your country code is found. When executing `iwlist wlan0 channel`, you should now have access to more channels (depending on your location).

### Broadcom

See [Broadcom wireless](/index.php/Broadcom_wireless "Broadcom wireless").

### Other drivers/devices

#### Tenda w322u

Treat this Tenda card as an `rt2870sta` device. See [#rt2x00](#rt2x00).

#### orinoco

This should be a part of the kernel package and be installed already.

Some Orinoco chipsets are Hermes II. You can use the `wlags49_h2_cs` driver instead of `orinoco_cs` and gain WPA support. To use the driver, [blacklist](/index.php/Kernel_modules#Blacklisting "Kernel modules") `orinoco_cs` first.

#### prism54

The driver `p54` is included in kernel, but you have to download the appropriate firmware for your card from [this site](http://linuxwireless.org/en/users/Drivers/p54#firmware) and install it into the `/usr/lib/firmware` directory.

**Note:** There's also older, deprecated driver `prism54`, which might conflict with the newer driver (`p54pci` or `p54usb`). Make sure to [blacklist](/index.php/Kernel_modules#Blacklisting "Kernel modules") `prism54`.

#### ACX100/111

**Warning:** The drivers for these devices [are broken](https://mailman.archlinux.org/pipermail/arch-dev-public/2011-June/020669.html) and do not work with newer kernel versions.

Packages: `tiacx` `tiacx-firmware` (deleted from official repositories and AUR)

See [official wiki](http://sourceforge.net/apps/mediawiki/acx100/index.php?title=Main_Page) for details.

#### zd1211rw

[`zd1211rw`](http://zd1211.wiki.sourceforge.net/) is a driver for the ZyDAS ZD1211 802.11b/g USB WLAN chipset, and it is included in recent versions of the Linux kernel. See [[5]](http://www.linuxwireless.org/en/users/Drivers/zd1211rw/devices) for a list of supported devices. You only need to [install](/index.php/Pacman "Pacman") the firmware for the device, provided by the [zd1211-firmware](https://aur.archlinux.org/packages/zd1211-firmware/) package.

#### hostap_cs

[Host AP](http://hostap.epitest.fi/) is a Linux driver for wireless LAN cards based on Intersil's Prism2/2.5/3 chipset. The driver is included in Linux kernel.

**Note:** Make sure to [blacklist](/index.php/Kernel_modules#Blacklisting "Kernel modules") the `orinico_cs` driver, it may cause problems.

### ndiswrapper

Ndiswrapper is a wrapper script that allows you to use some Windows drivers in Linux. See the compatibility list [here](http://ndiswrapper.sourceforge.net/mediawiki/index.php/List). You will need the `.inf` and `.sys` files from your Windows driver. Be sure to use drivers appropriate to your architecture (x86 vs. x86_64).

**Tip:** If you need to extract these files from an `*.exe` file, you can use [cabextract](https://www.archlinux.org/packages/?name=cabextract).

Follow these steps to configure ndiswrapper.

1\. Install the driver to `/etc/ndiswrapper/*`

```
# ndiswrapper -i filename.inf

```

2\. List all installed drivers for ndiswrapper

```
$ ndiswrapper -l

```

3\. Write the following configuration file:

 `/etc/modprobe.d/ndiswrapper.conf` 
```
ndiswrapper -m
depmod -a

```

Now the ndiswrapper install is almost finished; follow the instructions on [Kernel modules#Loading](/index.php/Kernel_modules#Loading "Kernel modules") to automatically load the module at boot.

The important part is making sure that ndiswrapper exists on this line, so just add it alongside the other modules. It would be best to test that ndiswrapper will load now, so:

```
# modprobe ndiswrapper
# iwconfig

```

and *wlan0* should now exist. Check this page if you are having problems: [Ndiswrapper installation wiki](http://ndiswrapper.sourceforge.net/joomla/index.php?/component/option,com_openwiki/Itemid,33/id,installation/).

### compat-drivers-patched

Patched compat wireless drivers correct the "fixed-channel -1" issue, whilst providing better injection. Please install the [compat-drivers-patched](https://aur.archlinux.org/packages/compat-drivers-patched/) package from the [AUR](/index.php/Arch_User_Repository "Arch User Repository").

[compat-drivers-patched](https://aur.archlinux.org/packages/compat-drivers-patched/) does not conflict with any other package and the modules built reside in `/usr/lib/modules/*your_kernel_version*/updates`.

These patched drivers come from the [Linux Wireless project](http://wireless.kernel.org/) and support many of the above mentioned chips such as:

```
ath5k ath9k_htc carl9170 b43 zd1211rw rt2x00 wl1251 wl12xx ath6kl brcm80211

```

Supported groups:

```
atheros ath iwlagn rtl818x rtlwifi wl12xx atlxx bt

```

It is also possible to build a specific module/driver or a group of drivers by editing the [PKGBUILD](/index.php/PKGBUILD "PKGBUILD"), particularly uncommenting the **line #46**. Here is an example of building the atheros group:

```
scripts/driver-select atheros

```

Please read the package's [PKGBUILD](/index.php/PKGBUILD "PKGBUILD") for any other possible modifications prior to compilation and installation.

## See also

*   [The Linux Wireless project](http://wireless.kernel.org/)
*   [Aircrack-ng guide on installing drivers](http://aircrack-ng.org/doku.php?id=install_drivers)