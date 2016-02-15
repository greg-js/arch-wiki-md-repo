## Contents

*   [1 Εισαγωγή](#.CE.95.CE.B9.CF.83.CE.B1.CE.B3.CF.89.CE.B3.CE.AE)
*   [2 Εγκατάσταση του Xorg](#.CE.95.CE.B3.CE.BA.CE.B1.CF.84.CE.AC.CF.83.CF.84.CE.B1.CF.83.CE.B7_.CF.84.CE.BF.CF.85_Xorg)
*   [3 Ρύθμιση του xorg](#.CE.A1.CF.8D.CE.B8.CE.BC.CE.B9.CF.83.CE.B7_.CF.84.CE.BF.CF.85_xorg)
    *   [3.1 hwd](#hwd)
    *   [3.2 xorgconfig](#xorgconfig)
    *   [3.3 Xorg -configure](#Xorg_-configure)
    *   [3.4 nvidia-xconfig](#nvidia-xconfig)
*   [4 Επεξεργασία του xorg.conf](#.CE.95.CF.80.CE.B5.CE.BE.CE.B5.CF.81.CE.B3.CE.B1.CF.83.CE.AF.CE.B1_.CF.84.CE.BF.CF.85_xorg.conf)
    *   [4.1 Ρυθμίσεις οθόνης](#.CE.A1.CF.85.CE.B8.CE.BC.CE.AF.CF.83.CE.B5.CE.B9.CF.82_.CE.BF.CE.B8.CF.8C.CE.BD.CE.B7.CF.82)
        *   [4.1.1 Horizontal Sync](#Horizontal_Sync)
        *   [4.1.2 Refresh Rate](#Refresh_Rate)
        *   [4.1.3 Βάθος χρώματος](#.CE.92.CE.AC.CE.B8.CE.BF.CF.82_.CF.87.CF.81.CF.8E.CE.BC.CE.B1.CF.84.CE.BF.CF.82)
        *   [4.1.4 Ανάλυση οθόνης](#.CE.91.CE.BD.CE.AC.CE.BB.CF.85.CF.83.CE.B7_.CE.BF.CE.B8.CF.8C.CE.BD.CE.B7.CF.82)
    *   [4.2 Ρυθμίσεις πληκτρολογίου](#.CE.A1.CF.85.CE.B8.CE.BC.CE.AF.CF.83.CE.B5.CE.B9.CF.82_.CF.80.CE.BB.CE.B7.CE.BA.CF.84.CF.81.CE.BF.CE.BB.CE.BF.CE.B3.CE.AF.CE.BF.CF.85)
        *   [4.2.1 Διάταξη πληκτρολογίου](#.CE.94.CE.B9.CE.AC.CF.84.CE.B1.CE.BE.CE.B7_.CF.80.CE.BB.CE.B7.CE.BA.CF.84.CF.81.CE.BF.CE.BB.CE.BF.CE.B3.CE.AF.CE.BF.CF.85)
        *   [4.2.2 Μοντέλο πληκτρολογίου](#.CE.9C.CE.BF.CE.BD.CF.84.CE.AD.CE.BB.CE.BF_.CF.80.CE.BB.CE.B7.CE.BA.CF.84.CF.81.CE.BF.CE.BB.CE.BF.CE.B3.CE.AF.CE.BF.CF.85)
        *   [4.2.3 Πρόβλημα με το πληκτρολόγιο της Apple ;](#.CE.A0.CF.81.CF.8C.CE.B2.CE.BB.CE.B7.CE.BC.CE.B1_.CE.BC.CE.B5_.CF.84.CE.BF_.CF.80.CE.BB.CE.B7.CE.BA.CF.84.CF.81.CE.BF.CE.BB.CF.8C.CE.B3.CE.B9.CE.BF_.CF.84.CE.B7.CF.82_Apple_.3B)
    *   [4.3 Display Size/DPI](#Display_Size.2FDPI)
    *   [4.4 Proprietary Drivers](#Proprietary_Drivers)
    *   [4.5 Γραμματοσειρές](#.CE.93.CF.81.CE.B1.CE.BC.CE.BC.CE.B1.CF.84.CE.BF.CF.83.CE.B5.CE.B9.CF.81.CE.AD.CF.82)
    *   [4.6 Sample Xorg.conf Files](#Sample_Xorg.conf_Files)
*   [5 Εκκίνηση του Xorg](#.CE.95.CE.BA.CE.BA.CE.AF.CE.BD.CE.B7.CF.83.CE.B7_.CF.84.CE.BF.CF.85_Xorg)
*   [6 X startup (/usr/bin/startx) tweaking](#X_startup_.28.2Fusr.2Fbin.2Fstartx.29_tweaking)
*   [7 Changes with modular Xorg](#Changes_with_modular_Xorg)
    *   [7.1 Most Common Packages](#Most_Common_Packages)
    *   [7.2 OpenGL 3D Acceleration](#OpenGL_3D_Acceleration)
    *   [7.3 Glxgears and Glxinfo](#Glxgears_and_Glxinfo)
    *   [7.4 Changed paths (and configuration)](#Changed_paths_.28and_configuration.29)
*   [8 Αντιμετώπιση προβλημάτων](#.CE.91.CE.BD.CF.84.CE.B9.CE.BC.CE.B5.CF.84.CF.8E.CF.80.CE.B9.CF.83.CE.B7_.CF.80.CF.81.CE.BF.CE.B2.CE.BB.CE.B7.CE.BC.CE.AC.CF.84.CF.89.CE.BD)
    *   [8.1 Ο Xorg "δεν μπορεί να δει" τις αναλύσεις που υποστηρίζει η οθόνη](#.CE.9F_Xorg_.22.CE.B4.CE.B5.CE.BD_.CE.BC.CF.80.CE.BF.CF.81.CE.B5.CE.AF_.CE.BD.CE.B1_.CE.B4.CE.B5.CE.B9.22_.CF.84.CE.B9.CF.82_.CE.B1.CE.BD.CE.B1.CE.BB.CF.8D.CF.83.CE.B5.CE.B9.CF.82_.CF.80.CE.BF.CF.85_.CF.85.CF.80.CE.BF.CF.83.CF.84.CE.B7.CF.81.CE.AF.CE.B6.CE.B5.CE.B9_.CE.B7_.CE.BF.CE.B8.CF.8C.CE.BD.CE.B7)
    *   [8.2 Προβλήματα με το πληκτρολόγιο](#.CE.A0.CF.81.CE.BF.CE.B2.CE.BB.CE.AE.CE.BC.CE.B1.CF.84.CE.B1_.CE.BC.CE.B5_.CF.84.CE.BF_.CF.80.CE.BB.CE.B7.CE.BA.CF.84.CF.81.CE.BF.CE.BB.CF.8C.CE.B3.CE.B9.CE.BF)
    *   [8.3 A Quick Fix for the Bitstream-Vera Conflict](#A_Quick_Fix_for_the_Bitstream-Vera_Conflict)
    *   [8.4 A Quick Fix for file conflicts in /usr/include](#A_Quick_Fix_for_file_conflicts_in_.2Fusr.2Finclude)
    *   [8.5 Η ροδέλα του ποντικιού δεν λειτουργεί](#.CE.97_.CF.81.CE.BF.CE.B4.CE.AD.CE.BB.CE.B1_.CF.84.CE.BF.CF.85_.CF.80.CE.BF.CE.BD.CF.84.CE.B9.CE.BA.CE.B9.CE.BF.CF.8D_.CE.B4.CE.B5.CE.BD_.CE.BB.CE.B5.CE.B9.CF.84.CE.BF.CF.85.CF.81.CE.B3.CE.B5.CE.AF)
    *   [8.6 Μερικά κουμπιά του ποντικιού δεν λειτουργούν](#.CE.9C.CE.B5.CF.81.CE.B9.CE.BA.CE.AC_.CE.BA.CE.BF.CF.85.CE.BC.CF.80.CE.B9.CE.AC_.CF.84.CE.BF.CF.85_.CF.80.CE.BF.CE.BD.CF.84.CE.B9.CE.BA.CE.B9.CE.BF.CF.8D_.CE.B4.CE.B5.CE.BD_.CE.BB.CE.B5.CE.B9.CF.84.CE.BF.CF.85.CF.81.CE.B3.CE.BF.CF.8D.CE.BD)
    *   [8.7 Προβλήματα πληκτρολογίου](#.CE.A0.CF.81.CE.BF.CE.B2.CE.BB.CE.AE.CE.BC.CE.B1.CF.84.CE.B1_.CF.80.CE.BB.CE.B7.CE.BA.CF.84.CF.81.CE.BF.CE.BB.CE.BF.CE.B3.CE.AF.CE.BF.CF.85)
        *   [8.7.1 AltGR (Compose Key) not working properly](#AltGR_.28Compose_Key.29_not_working_properly)
        *   [8.7.2 Can't set qwerty layouts using the setxkbmap command](#Can.27t_set_qwerty_layouts_using_the_setxkbmap_command)
        *   [8.7.3 Setup French Canadian (old ca_enhanced) layout](#Setup_French_Canadian_.28old_ca_enhanced.29_layout)
    *   [8.8 Missing libraries](#Missing_libraries)
    *   [8.9 Some packages fail to build and complain about missing X11 includes](#Some_packages_fail_to_build_and_complain_about_missing_X11_includes)
    *   [8.10 Unable to load font '(null)'](#Unable_to_load_font_.27.28null.29.27)
    *   [8.11 KDE Taskbar/Desktop Icons Broken](#KDE_Taskbar.2FDesktop_Icons_Broken)
    *   [8.12 Updating from testing version to extra (missing files)](#Updating_from_testing_version_to_extra_.28missing_files.29)
    *   [8.13 Problem with MIME types in various desktop environments](#Problem_with_MIME_types_in_various_desktop_environments)
    *   [8.14 DRI stops working with Matrox cards](#DRI_stops_working_with_Matrox_cards)
    *   [8.15 Cannot start any clients under Xephyr](#Cannot_start_any_clients_under_Xephyr)
    *   [8.16 Cannot start X clients as root using "su"](#Cannot_start_X_clients_as_root_using_.22su.22)
*   [9 Σύνδεσμοι](#.CE.A3.CF.8D.CE.BD.CE.B4.CE.B5.CF.83.CE.BC.CE.BF.CE.B9)
*   [10 Εξωτερικοί σύνδεσμοι](#.CE.95.CE.BE.CF.89.CF.84.CE.B5.CF.81.CE.B9.CE.BA.CE.BF.CE.AF_.CF.83.CF.8D.CE.BD.CE.B4.CE.B5.CF.83.CE.BC.CE.BF.CE.B9)

## Εισαγωγή

**Xorg** is the public, open-source implementation of the X11 X Window System. (See the [X.org Wikipedia Article](http://en.wikipedia.org/wiki/X.Org_Server) or [X.org](http://wiki.x.org/wiki/) for details.) Basically, if you want a GUI atop Arch, you will want xorg.

## Εγκατάσταση του Xorg

Πριν ξεκινήσετε, σιγουρευτείτε να κάνετε τα παρακάτω:

1.  Σιγουρευτείτε ότι ο [pacman](/index.php/Pacman "Pacman") είναι ρυθμισμένος και updated.
2.  Αν τρέχετε άλλον X server πρέπει να τον κλείσετε. `ctrl+alt+backspace`
3.  Make a note about third-party drivers (π.χ, nVidia ή ATI drivers).

Πρώτα ας εγκαταστήσουμε ολόκληρο το πακέτο του 'xorg' με:

```
# pacman -S xorg

```

O προεπιλεγμένος driver 'vesa' είναι απλά ένας εφεδρικός (δεν υποστηρίζει 3D επιτάχυνση αλλά ούτε και πολλές αναλύσεις), οπότε χρειάζεστε τον κατάλληλο driver για την κάρτα γραφικών σας. Πληκτρολογήστε την παρακάτω εντολή για να δείτε τους διαθέσιμους drivers:

```
# pacman -Ss xf86-video

```

Κοιτάξτε για τον κατάλληλο driver για την κάρτα σας και κάντε τον εγκατάσταση με pacman -S.Για να ελέγξετε τη κάρτα σας,αν το hwd είναι ήδη εγκατεστημένο,τρέξτε 'hwd -s', ή 'lspci' (lψάξτε για 'VGA compatible controller').

Αν ο Xorg έχει εγκατασταθεί, είναι ώρα να κάνουμε το `xorg.conf`

## Ρύθμιση του xorg

Πριν τρέξετε το xorg, χρειάζεται να τον ρυθμίσετε για να αναγνωρίσει τη κάρτα γραφικών σας, την οθόνη, ποντίκι και πληκτρολόγιο. Υπάρχουν αρκετοί μέθοδοι για να γίνει αυτοματοποιημένη η διαδικασία αυτήν:

### hwd

Ίσως ο ευκολότερος και γρηγορότερος τρόπος να κάνετε το Xorg να λειτουργήσει είναι να χρησιμοποιήσετε το <tt>hwd</tt>, ένα εργαλείο γραμμένο από την κοινότητα του Arch Linux. Βασικά είναι εργαλείο που ανιχνεύει το hardware του υπολογιστή και έχει πολλαπλές χρήσεις, μία από αυτή είναι το "σετάρισμα" του X server. Ευτυχώς, hwd είναι πολύ πιο εκσυγχρονισμένο απ´ ό,τι το `xorgconf` και δεν χρειάζεται τη λήψη πληροφοριών

Κατ'αρχήν, κάντε εγκατάσταση το πακέτο <tt>hwd</tt> με:

```
# pacman -S hwd

```

Τώρα απλά τρέξτε την παρακάτω εντολή με δικαιώματα υπερχήστη (root),για να δημιουργηθεί το αρχείο `xorg.conf`:

```
# hwd -xa

```

Αυτή η διαδικασία θα αντικαταστήσει οποιοδήποτε /etc/X11/xorg.conf αρχείο με ένα άλλο,βασισμένο στην εντολή <tt>hwd</tt> και το hardware του υπολογιστή σας.

Εναλλακτικά, μπορείτε να δημιουργήσετε ένα δείγμα του xorg (/etc/X11/xorg.conf.hwd) χωρίς να αντικατασταθούν οι τρέχουσες ρυθμίσεις.Για να γίνει αυτό, τρέξτε <tt>hwd</tt> με **-x** flag:

```
# hwd -x

```

Αποτέλεσμα δείγματος:

```
/etc/X11/xorg.conf.ati
/etc/X11/xorg.conf.vesa

Τα δείγματα του xorg σας είναι έτοιμα, μετονομάστε ένα από αυτά σε 'xorg.conf'.
Αν δεν είστε σίγουροι χρησιμοποιήστε τον 'vesa' driver (προεπιλογή).

```

Για να χρησιμοποιήσετε τις ρυθμίσεις του δείγματος,χρειάζεται να το μετονιμάσετε,όπως παρακάτω:

```
# mv /etc/X11/xorg.conf.vesa /etc/X11/xorg.conf

```

AD: In my experience hwd creates XF86Config-4 file and if there is not xorg.conf present Xorg uses it automatically.

### xorgconfig

Για την εκκίνηση του <tt>xorgconfig</tt>:

```
# xorgconfig

```

ή

```
# xorgcfg -textmode

```

Οι παραπάνω εντολές θα δημιουργήσουν το <tt>xorg.conf</tt>.

Απαντήστε στις ερωτήσεις,και το πρόγραμμα θα ρυθμίσει το αρχείο για εσάς.Το συγκεκριμένο πρόγραμμα δεν είναι το καλύτερο αλλά είναι μια αρχή.

### Xorg -configure

Μπορείτε επίσης να χρησιμοποιήσετε το

```
# Xorg -configure

```

ή

```
# X -configure

```

### nvidia-xconfig

Οι χρήστες τις nVidia μπορούν επίσης να κάνουν το εξης:

```
# nvidia-xconfig

```

μόνο όταν έχουν τους επίσημους nvidia drivers [installed](/index.php/NVIDIA "NVIDIA").

Comment the line

```
 Load           "type1"

```

in the Module section since recent versions of xorg-server does not include the type1 font module (completely replaced by freetype).

## Επεξεργασία του xorg.conf

Αν θέλετε μπορείτε να επεξεργαστείτε τις ρυθμίσεις του Xorg.Ανοίξτε το αρχείο με τον αγαπημένο σας επεξεργαστή κειμένου,όπως ο nano (θα χρειαστεί να έχετε δικαιώματα υπερχρήστη/root):

```
# nano /etc/X11/xorg.conf

```

ή μπορείτε να χρησιμοποιήσετε το εργαλείο ρυθμίσεων του Xorg :

```
# xorgcfg -textmode

```

Αν θέλετε να έχετε περισσότερη υποστήριξη για το ποντίκι,δείτε [Get All Mouse Buttons Working](/index.php/Get_All_Mouse_Buttons_Working "Get All Mouse Buttons Working").

### Ρυθμίσεις οθόνης

Εξαρτώμενοι από το υλικό του υπολογιστή σας,ο Xorg μπορεί να αποτύχει να ανιχνεύση σωστά τις ρυθμίσεις της οθόνη σας, ή απλά να θέλετε να έχετε χαμηλότερη ανάλυση απ'ότι υποστηρίζει η οθόνη σας.Επίσης ρίξτε μια ματιά στις παρακάτω ρυθμίσεις μπορεί να φανούν χρήσιμες. The following settings are specified in the Monitor section:

#### Horizontal Sync

```
HorizSync 28-64

```

#### Refresh Rate

```
VertRefresh 60

```

The following are specified in the Screen section:

#### Βάθος χρώματος

```
Depth 24

```

#### Ανάλυση οθόνης

```
Modes "1280x1024" "1024x768" "800x600"

```

### Ρυθμίσεις πληκτρολογίου

Ο Xorg μπορεί να αποτύχει να ανιχνεύσει σωστά το πληκτρολόγιο σας. Αυτό μπορεί να δημιουργήσει προβλήματα με τη διάταξη του πληκτρολογίου σας ή απλά το μοντέλο πληκτρολογίου δεν θα ρυθμιστεί σωστά.

Για να δείτε μια λίστα με τα υποστηριζόμενα μοντέλα πληκτρολογίου,layouts, variants and options, ανοίξτε το.

```
/usr/share/X11/xkb/rules/xorg.lst

```

#### Διάταξη πληκτρολογίου

Αν θέλετε να αλλάξετε την διάταξη του πληκτρολογίου,χρησιμοποιήστε την XkbLayout επιλογή στην κατηγορία keyboard InputDevice.Για παράδειγμα, αν έχετε ένα πληκτρολόγιο με Αγγλική διάταξη:

```
Option "XkbLayout" "gb"

```

Για να διευκολύνετε την εναλλαγή μεταξύ των γλωσσών ,για παράδειγμα μεταξύ US και ελληνικά δείτε το παρακάτω:

```
Option "XkbLayout" "us,el"
Option "XkbVariant" ",extended"
Option "XkbOptions" "grp:alt_shift_toggle,grp:control,grp_led:scroll"

```

Το παραπάνω κάνει εναλλαγή μεταξύ Αγγλικών και Ελληνικών με τον συνδιασμό πλήκτρων "Alt+Shift".Επίσης ανάβει και η ένδειξη του Scroll Lock για να καταλάβετε σε ποια γλώσσα είστε.

#### Μοντέλο πληκτρολογίου

Για να αλλάξετε το μοντέλο του πληκτρολογίου, χρησιμοποιήστε την επιλογή XkbModel στην κατηγορία keyboard InputDevice.Για παράδειγμα,αν έχετε το Microsoft Wireless Multimedia Keyboard:

```
Option "XkbModel" "microsoftmult"

```

#### Πρόβλημα με το πληκτρολόγιο της Apple ;

Για περισσότερες πληροφορίες δείτε [here](/index.php/Apple_Keyboard "Apple Keyboard").

### Display Size/DPI

Για να έχετε σωστή απεικόνιση των γραμματοσειρών θα πρέπει να καθορίσετε το επιθυμητό DPI. Στην κατηγορία `"Monitor"` τοποθετήστε το μέγεθος σε mm:

```
Section "Monitor"
   ...
 DisplaySize 336 252 # 96 DPI @ 1280x960
   ...
EndSection

```

The formula for calculating the DisplaySize values is Width x 25.4 / DPI and Height x 25.4 / DPI. If you're running Xorg with a resolution of 1024x768 and want a DPI of 96, use 1024 x 25.4 / 96 and 768 x 25.4 / 96\. Round numbers down.

```
# calc: (x|y)pixels * 25.4 / dpi
# DisplaySize 168 126 # 96 DPI @ 640x480
# DisplaySize 210 157 # 96 DPI @ 800x600
# DisplaySize 269 201 # 96 DPI @ 1024x768
# DisplaySize 302 227 # 96 DPI @ 1152x864
# DisplaySize 336 252 # 96 DPI @ 1280x960
# DisplaySize 336 210 # 96 DPI @ 1280x800 (non 4:3 aspect)
# DisplaySize 339 271 # 96 DPI @ 1280x1024 (non 4:3 aspect)
# DisplaySize 370 277 # 96 DPI @ 1400x1050
# DisplaySize 420 315 # 96 DPI @ 1600x1200
# DisplaySize 444 277 # 96 DPI @ 1680x1050
# DisplaySize 506 315 # 96 DPI @ 1920x1200 (non 4:3 aspect)

```

Για τους χρήστες της nVidia πρέπει να απενεργοποιήσετε την αυτόματη ρύθμιση του DPI και να το καθορίσετε εσείς χειροκίνητα. Υπάρχει επίσης ένα ευκολότερος τρόπος να ρυθμίσετε το DPI σε τέτοιες κάρτες.Είτε τη μία ή ακόμη και τις δύο ακόλουθες γραμμές πρέπει να ρυθμιστούν για τις κάρτες τις nVidia.

```
  Option   "UseEdidDpi" "false"
  Option   "DPI" "96 x 96"

```

Results can be checked by issuing the following command, which should return 96x96 dots per inch if you set DPI @ 96.

```
$ xdpyinfo | grep -B1 dot

```

### Proprietary Drivers

If you wish to use third-party graphics drivers, do check first that the X server runs OK first. Xorg should run smoothly without official drivers, which are typically needed only for advanced features such as 3D-accelerated rendering for games, dual-screen setups, and TV-out. Refer to the [NVIDIA](/index.php/NVIDIA "NVIDIA") and [ATI](/index.php/ATI "ATI") wikis for help with driver installation.

### Γραμματοσειρές

Μερικές συμβουλές για την ρύθμιση των γραμματοσειρών δείτε [Xorg Font Configuration](/index.php/Xorg_Font_Configuration "Xorg Font Configuration").

### Sample Xorg.conf Files

Anyone who has an Xorg.conf file written up that works, go ahead and post a link to it here for others to look at! Please don't inline the entire conf file; upload it somewhere else and link. Thanks!

*   Shadowhand (nv and nvidia drivers): [http://people.os-zen.net/shadowhand/configs/xorg.conf](http://people.os-zen.net/shadowhand/configs/xorg.conf)
*   Cerebral (fglrx and radeon drivers): [http://www.student.cs.uwaterloo.ca/~tjwillar/configs/xorg.conf](http://www.student.cs.uwaterloo.ca/~tjwillar/configs/xorg.conf)
*   raskolnikov (via unichrome and synaptics drivers): [http://athanatos.free.fr/Arch/xorg.conf](http://athanatos.free.fr/Arch/xorg.conf)
*   Leigh (Three independent screens - Three nvidia cards): [http://files.myopera.com/allisonleigh/linuxbackup/xorg.conf](http://files.myopera.com/allisonleigh/linuxbackup/xorg.conf)
*   Mr.Elendig (nvidia with composite and "stuff") [http://arch.har-ikkje.net/stuff/xorg.conf](http://arch.har-ikkje.net/stuff/xorg.conf)

## Εκκίνηση του Xorg

Αυτό γίνεται απλά με την παρακάτω εντολή:

```
$ startx

```

The default X environment is rather bare, and you will typically seek to install window managers or desktop environments to supplement X.

Για να τεστάρετε το αρχείο ρυθμίσεων που έχετε κάνει,δείτε το παρακάτω:

```
$ X -config _<your config file>_

```

If a problem occurs, then view the log at <tt>/var/log/Xorg.0.log</tt>. Be on the lookout for any lines beginning with _(EE)_ which represent errors, and also _(WW)_ which are warnings that could indicate other issues.

**Note:** Using startx requires a [~/.xinitrc](/index.php/Xinitrc "Xinitrc") file, so that X knows what to run when it starts.

In addition, you can also install twm and xterm (via pacman), which will be used as a fallback if ~/.xinitrc does not exist (as stated in /etc/X11/xinit/xinitrc).

## X startup (/usr/bin/startx) tweaking

For X's option reference see

```
$ man Xserver

```

The following options have to be appended to the variable "defaultserverargs" in the /usr/bin/startx file.

prevent X from listening on tcp:

```
-nolisten tcp

```

getting rid of the gray weave pattern while X is starting and let X set a black root window:

```
-br

```

enable deferred glyph loading for 16 bit fonts:

```
-deferglyphs 16

```

Note: If you start X with kdm, the startx script does not seem to be executed. X options must be appended to the variable "ServerCmd" in the /opt/kde/share/config/kdm/kdmrc file. By default kdm options are

```
  ServerCmd=/usr/bin/X -br -nolisten tcp

```

## Changes with modular Xorg

### Most Common Packages

Σιγουρευτείτε ότι έχετε drivers για το ποντίκι σας,το πληκτρολόγιο και την κάρτα γραφικών σας. Για το πληκτρολόγιο και το ποντίκι είναι τα, **xf86-input-keyboard** και **xf86-input-mouse** αντίστοιχα. Υπάρχουν και άλλα πακέτα για διάφορες συσκευές **xf86-input-***.

Για την κάρτα γραφικών σας, βρείτε ποιος σωστός driver χρειάζεται και κάντε εγκατάσταση το πακέτο **xf86-video-*** .Οι χρήστες της ATI και της Nvidia μπορεί να θέλουν να εγκαταστήσουν τους drivers κλειστού κώδικα για την κάρτα τους ([NVIDIA](/index.php/NVIDIA "NVIDIA"), [ATI](/index.php/ATI "ATI")).

To install all drivers in one run, the **xorg-input-drivers** and **xorg-video-drivers** are available.

### OpenGL 3D Acceleration

X.Org 7.0 on Arch Linux uses a modular design for mesa, the OpenGL rendering system. Several implementations are available:

*   libgl-dri: Open-source DRI OpenGL implementation. Falls back to software rendering when no DRI driver is installed
*   some other driver providing libGL (ati, nvidia)

When pacman installs an application that needs mesa, it will install one of these packages. To be sure about the right library for your setup, install the library you want prior to installing Xorg. Installing the right package afterwards is also possible, though this gives some dependency errors sometimes, which can be ignored with the -d switch.

### Glxgears and Glxinfo

Αυτές οι εφαρμογές περιλαμβάνονται στο πακέτο 'mesa'.

### Changed paths (and configuration)

**See this entry for additional upgrade info:** [https://www.archlinux.org/blog/2006/01/02/how-to-upgrade-xorg/](https://www.archlinux.org/blog/2006/01/02/how-to-upgrade-xorg/)

Modular X.Org 7 installs everything in `/usr`, where the older versions installed in `/usr/X11R6`. Several configuration files need updates:

*   _/etc/X11/xorg.conf_
    *   Fontpaths live in /usr/share/fonts now
    *   RGB database is in /usr/share/X11/rgb
    *   module path is /usr/lib/xorg/modules

Also note that some X configuration tools might stop working. The easiest way to configure X.org is by installing the correct driver packages and running _Xorg -configure_, which results in a `/root/xorg.conf.new` which only needs modification in the resolutions, mouse configuration and keyboard layouts.

Some packages have hard-coded references to `/usr/X11R6`. These packages need fixing. In the meantime, look what packages install files in `/usr/X11R6`, uninstall those, make a symlink from `/usr` to `/usr/X11R6` and reinstall the affected packages. Another option is to move the contents of `/usr/X11R6` to `/usr` and make the symlink.

Or you can just add a second module path via <code/>ModulePath "/usr/X11R6/lib/modules"</code> This works e.g. for Nvidia 76.76

## Αντιμετώπιση προβλημάτων

### Ο Xorg "δεν μπορεί να δει" τις αναλύσεις που υποστηρίζει η οθόνη

I found myself in a situation where if i used one of my monitors(a gnr ts902) Xorg would only present me with the options 640x480 and 320x480 which ofcourse was less than i desired. After a lot of research i found through read-edid(in aur) that part of my EDID was corrupt and so i could only read my HorizSync with read-edid. This fortunately was enough and after adding the right Horisync line to the xorg.conf's Monitor section(didn't have to add VertRefresh...) I restarted X to see the right resolution :)

note: I'm not sure:

```
Option "ModeValidation" "NoEdidModes"
Option   "UseEdid" "false"

```

in Device section in xorg config are needed aswell, to lazy now to test without them :)

### Προβλήματα με το πληκτρολόγιο

Auto-generated xorg.conf files may cause you problems. If you cannot get to tty1 by holding CTRL-ALT and pressing F1 or cannot get the £ sign for gb people, check to see if the following entries are in your /etc/X11/xorg.conf:

```
Option "XkbLayout"  "uk"         #"uk" is not a real layout, look in /usr/share/X11/xkb/symbols/ for a list of real ones.
Option "XkbRules"   "xfree86"    #this should be "xorg"
Option "XkbVariant" "nodeadkeys" #This line is also known to cause the problems described, try commenting it out.

```

Για να αλλάξετε γλώσσες με το Alt+Shift:

```
Option "XkbOptions" "grp:alt_shift_toggle,grp_led:scroll"

```

### A Quick Fix for the Bitstream-Vera Conflict

Αν δείτε μήνυμα ότι το πακέτο ttf-bitstream-vera "συγκρούεται" με το xorg:

1.  Βγείτε από τη συνδρία του pacman απατώντας όχι.
2.  Τρέξτε `pacman -Rd xorg`
3.  Μετά `pacman -Syu`
4.  Και `pacman -S xorg`
5.  Ανανεώστε τις τοποθεσίες (paths) στο /etc/X11/xorg.conf

### A Quick Fix for file conflicts in /usr/include

Αν δείτε μήνυμα ότι το αρχείο συγκρούεται με το /usr/include/X11 και /usr/include/GL:

1.  Τρέξτε `rm /usr/include/{GL,X11}`
2.  Μετά `pacman -Su`

The symlinked directories removed by this operation are replaced by real directories in the new xorg package, causing these file conflicts to appear.

### Η ροδέλα του ποντικιού δεν λειτουργεί

Η επιλογή "Auto" δεν λειτουργεί σστά στην έκδοση 7 του Xorg.Στην κατηγορία InputDevice για το ποντίκι,αλλάξτε:

```
Option         "Protocol" "auto"

```

σε

```
Option         "Protocol" "IMPS/2"

```

ή

```
Option         "Protocol" "ExplorerPS/2"

```

### Μερικά κουμπιά του ποντικιού δεν λειτουργούν

Οι χρήστες του USB Mice πρέπει να διαβάσουν [Get_All_Mouse_Buttons_Working](/index.php/Get_All_Mouse_Buttons_Working "Get All Mouse Buttons Working").

Οι χρήστες Intellimouse (ExplorerPS/2) users might find their scroll and side buttons aren't behaving as they used to. Previously xorg.conf needed:

```
Option      "Buttons" "7"
Option      "ZAxisMapping" "6 7"

```

and users also had to run xmodmap to get the side buttons working with a command like:

```
xmodmap -e "pointer = 1 2 3 6 7 4 5"

```

Now xmodmap is no longer required. Instead, make xorg.conf look like this:

```
Option      "Buttons" "5"
Option      "ZAxisMapping" "4 5"
Option      "ButtonMapping" "1 2 3 6 7"

```

and the side buttons on a 7-button Intellimouse will work like they used to, without needing to run xmodmap.

### Προβλήματα πληκτρολογίου

Μερικές διατάξεις πλκτρολογίου έχουν αλλάξει.

*   I wasn't able to Ctrl+Alt+Fx to switch to console
*   I wasn't able to use layouts

The problem was that the _sk_qwerty_ layout doesn't exist anymore. I had to replace

```
Option         "XkbLayout" "us,sk_qwerty"

```

with

```
Option         "XkbLayout" "us,sk"
Option         "XkbVariant" ",qwerty"

```

Another thing to look for if your keyboard isn't properly functioning is the XkbRules option:
You'll need to change

```
Option         "XkbRules" "xfree86"

```

to

```
Option         "XkbRules" "xorg"

```

#### AltGR (Compose Key) not working properly

If, after the update, you can't use the AltGr key as expected any more, try adding this to your keyboard section:

```
Option      "XkbOptions" "compose:ralt"

```

This is not the correct way to activate the AltGr Key on a German keyboard (for example, to use the '|' and '@' keys on German keyboards). Just choose a valid keyboard variant for it to work again, for example (the example is for a German keyboard):

```
Option      "XkbLayout" "de"
Option      "XkbVariant" "nodeadkeys"

```

The solutions above don't work on an Italian keyboard. To activate the AltGr key on an Italian keyboard make sure you have the following lines set up properly:

```
 Driver          "kbd"
 Option          "XkbRules"      "xorg"
 Option          "XkbVariant"    ""

```

This might still not be enough for a swedish keyboard. Try the above, but with lv3 instead of compose. (Thank you wyvern!) That is:

```
 Option "XkbLayout" "se"
 Option "XkbVariant" "nodeadkeys"
 Option "XkbOptions" "lv3:ralt_switch"

```

#### Can't set qwerty layouts using the setxkbmap command

After the update, there aren't qwerty layouts as for example sk_qwerty. If you want to switch your present keyboard layout to any qwerty keyboard layout use this command:

```
$ setxkbmap NAME_OF_THE_LAYOUT qwerty

```

e.g.: for sk_qwerty use:

```
$ setxkbmap sk qwerty

```

After the update, trying the above command I had this message "Error loading new keyboard description". I find out that the xserver doesn't have the rights to write, execute, read in the directory /var/tmp So give the permissions to that directory. Restart the xserver and you will have your deadkeys back! Don't believe? Try out the code e.g.: it layout

```
$ setxkbmap -layout it

```

#### Setup French Canadian (old ca_enhanced) layout

With Xorg7, "ca_enhanced" is no more. You have to do a little trick to get the same layout that you are used to: Switch the old:

```
       Option          "XkbLayout"     "ca_enhanced"

```

To:

```
       Option          "XkbLayout"     "ca"
       Option          "XkbVariant"    "fr"

```

It will be similar with other layout, I presume. You can refer to Gentoo HowTo there: [http://www.gentoo.org/proj/en/desktop/x/x11/modular-x-howto.xml](http://www.gentoo.org/proj/en/desktop/x/x11/modular-x-howto.xml)

### Missing libraries

*   **Help! I get an error message running my favourite app saying "libXsomething" doesn't exist!**

In most cases, all you need to do is take the name of the library (eg libXau.so.1), convert it all to lowercase, remove the extension, and pacman for it:

```
# pacman -S libxau

```

This will install the library you're missing, and all will be well again!

### Some packages fail to build and complain about missing X11 includes

Just reinstall the packages xproto and libx11, even if they are already installed.

### Unable to load font '(null)'

*   **Some programs don't work and say unable to load font `(null)'.**

These packages would like some extra fonts. Some programs only work with bitmap fonts. Two major packages with bitmap fonts are available, xorg-fonts-75dpi and xorg-fonts-100dpi. You don't need both; one should be enough. To find out which one would be better in your case, try this:

```
$ xdpyinfo | grep resolution

```

and grab what is closer to you (75 or 100 instead of XX)

```
# pacman -S xorg-fonts-XXdpi

```

### KDE Taskbar/Desktop Icons Broken

*   **KDE taskbar doesn't work and the desktop icons disappear**

Install the packages libxcomposite and libxss. It will be fine.

```
# pacman -S libxcomposite libxss

```

### Updating from testing version to extra (missing files)

If you've updated from Xorg 7 in testing to Xorg 7 in extra and are finding that many files seem to be missing (including startx, /usr/share/X11/rgb.txt, and others), you may have lost many files due to the xorg-clients package splitting from a single package into many smaller sub packages.

You need to reinstall all the packages that are dependencies of xorg-clients:

```
# pacman -S xorg-apps xorg-font-utils xorg-res-utils xorg-server-utils \
          xorg-twm xorg-utils xorg-xauth xorg-xdm xorg-xfs xorg-xfwp \
          xorg-xinit xorg-xkb-utils xorg-xsm

```

This should fix the problem.

### Problem with MIME types in various desktop environments

If you noticed icons missing and can't click-open files in desktop environments, add the following lines to /etc/profile or your preferred init script and reboot.

```
XDG_DATA_DIRS=$XDG_DATA_DIRS:/usr/share
export XDG_DATA_DIRS

```

### DRI stops working with Matrox cards

If you use a Matrox card and DRI stops working after upgrading to xorg7, try adding the line

```
Option "OldDmaInit" "On"

```

to the Device section that references the video card in xorg.conf.

### Cannot start any clients under Xephyr

The client connections are rejected by the X server's security mechanism, you can find a complete explanation and solution in [[1]](http://wiki.debian.org/XStrikeForce/FAQ#howtoxnest).

### Cannot start X clients as root using "su"

If you're getting "Client is not authorized to connect to server", try adding the line

```
 session        optional        pam_xauth.so

```

to the file `/etc/pam.d/su`. pam_xauth will properly set environment variables and handle xauth keys.

## Σύνδεσμοι

Δείτε επίσης:

*   [Display manager](/index.php/Display_manager "Display manager")
*   [Start X at login](/index.php/Start_X_at_login "Start X at login")
*   [Xorg Font Configuration](/index.php/Xorg_Font_Configuration "Xorg Font Configuration")
*   Proprietary Video Drivers
    *   [ATI](/index.php/ATI "ATI")
    *   [NVIDIA](/index.php/NVIDIA "NVIDIA")
*   [Desktop environment](/index.php/Desktop_environment "Desktop environment")
    *   [KDE](/index.php/KDE "KDE")
    *   [GNOME](/index.php/GNOME "GNOME")
    *   [Xfce](/index.php/Xfce "Xfce")
    *   [Enlightenment](/index.php/Enlightenment "Enlightenment")
    *   [Fluxbox](/index.php/Fluxbox "Fluxbox")
    *   [Openbox](/index.php/Openbox "Openbox")

## Εξωτερικοί σύνδεσμοι

*   [X.org Wikipedia Article](http://en.wikipedia.org/wiki/X.Org_Server)
*   [X.org](http://wiki.x.org/wiki/)
*   [Installing and setting up Xorg](http://archux.com/page/installing-and-setting-xorg)