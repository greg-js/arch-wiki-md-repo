**CPU Frequency Scaling** είναι μια τεχνολογία, βασικά για laptops, που επιτρέπει στo λειτουργικό σύστημα να αλλάζει την ταχύτητα της CPU. Για παράδειγμα, μειώνοντας την ταχύτητα της CPU όταν το notebook λειτουργεί με μπαταρία, αυξάνεται η διάρκεια της μπαταρίας. Η Intel ονομάζει την τεχνολογία αυτή SpeedStep. Η AMD την ονομάζει PowerNow! ή Cool'n'Quiet

# Βήματα:

1\. Εγκατάσταση του πακέτου cpufrequtils

```
# pacman -S cpufrequtils

```

2\. Φορτώνουμε το kernel module acpi-cpufreq

Intel:

```
# modprobe acpi-cpufreq

```

AMD:

```
# modprobe powernow-k{6,7,8}

```

3\. Φορτώνουμε τους ελεγχτές κλιμάκωσης (scaling governor(s))

```
# modprobe cpufreq_ondemand
# modprobe cpufreq_powersave

```

Για να τα φορτώσουμε όλα αυτόματα στην εκκίνηση, προσθέτουμε τα acpi-cpufreq,cpufreq_ondemand και cpufreq_powersave στα MODULES στο αρχείο /etc/rc.conf. Για παράδειγμα:

```
#MODULES=( **acpi-cpufreq cpufreq_ondemand cpufreq_powersave** vboxdrv fuse fglrx iwl3945 ... )

```

4\. Επεξεργαζόμαστε το αρχείο /etc/conf.d/cpufreq σαν root, και επιλέγουμε το governor:

```
#configuration for cpufreq control
# valid governors:
#  ondemand, performance, powersave,
#  conservative, userspace
governor="ondemand"

# valid suffixes: Hz, kHz (default), MHz, GHz, THz
min_freq="1GHz"
max_freq="2GHz"

```

Σημείωση: η min_freq και η max_freq γραμμές μπορεί να μπουν σε σχόλιο (#) , αφού ο driver του πυρήνα θα δει τις τιμές αυτόματα.

Για να επιβεβαιώσουμε ότι τρέχει δίνουμε την εντολή:

```
# cpufreq-info

```

και ελέγχουμε την έξοδο

5\. Ξεκινάμε το cpufreq daemon με την εντολή:

```
# /etc/rc.d/cpufreq start

```

Προσθέτουμε το cpufreq στη DAEMONS λίστα στο αρχείο /etc/rc.conf. Για παράδειγμα:

DAEMONS=(syslog-ng network netfs crond dbus alsa hal fam **cpufreq**)

6\. (Προαιρετικό) Εγκατάσταση και ρύθμιση κάποιου GUI εργαλείου για το παραθυρικό περιβάλλον. Για το KDE υπάρχουν τα KLaptop KPowersave.

Περισσότερες πληροφορίες μπορείτε να βρείτε στη σελίδα [cpufrequtils](/index.php/Cpufrequtils "Cpufrequtils").

**Σημειώσεις για Dual/MultiCore επεξεργαστές**

1.Η κλιμάκωση θα λειτουργήσει μόνο στο βασικό cpu0 core. Προσθέστε αυτές τις γραμμές στο αρχείο /etc/rc.local για να κάνετε όλους τους cores να κλιμακώνονται.

```
# echo "ondemand" > /sys/devices/system/cpu/cpu0/cpufreq/scaling_governor
# echo "ondemand" > /sys/devices/system/cpu/cpu1/cpufreq/scaling_governor

```

...περισσότερες αν χρειάζεται

2\. Αν η δεύτερη CPU δεν ακουλουθεί τους κανόνες συχνότητας μετά από suspend στη ram, πρέπει να κάνετε επεξεργασία στο αρχείο /usr/lib/hal/scripts/linux/hal-system-power-suspend-linux και να προοσθέσετε τη γραμμή:

```
# echo "ondemand" > /sys/devices/system/cpu/cpu1/cpufreq/scaling_governor

```

**πριν** την τελική γραμμή ("exit $RET").