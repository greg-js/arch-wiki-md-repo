## Contents

*   [1 Εγκατάσταση](#.CE.95.CE.B3.CE.BA.CE.B1.CF.84.CE.AC.CF.83.CF.84.CE.B1.CF.83.CE.B7)
*   [2 Ρύθμισεις του OpenOffice](#.CE.A1.CF.8D.CE.B8.CE.BC.CE.B9.CF.83.CE.B5.CE.B9.CF.82_.CF.84.CE.BF.CF.85_OpenOffice)
    *   [2.1 Υποστήριξη πολυμέσων στο OpenOffice.org 2](#.CE.A5.CF.80.CE.BF.CF.83.CF.84.CE.AE.CF.81.CE.B9.CE.BE.CE.B7_.CF.80.CE.BF.CE.BB.CF.85.CE.BC.CE.AD.CF.83.CF.89.CE.BD_.CF.83.CF.84.CE.BF_OpenOffice.org_2)
    *   [2.2 Χειροκίνητη εγκατάσταση λεξικών](#.CE.A7.CE.B5.CE.B9.CF.81.CE.BF.CE.BA.CE.AF.CE.BD.CE.B7.CF.84.CE.B7_.CE.B5.CE.B3.CE.BA.CE.B1.CF.84.CE.AC.CF.83.CF.84.CE.B1.CF.83.CE.B7_.CE.BB.CE.B5.CE.BE.CE.B9.CE.BA.CF.8E.CE.BD)
*   [3 Running](#Running)
*   [4 Γνωστά προβλήματα](#.CE.93.CE.BD.CF.89.CF.83.CF.84.CE.AC_.CF.80.CF.81.CE.BF.CE.B2.CE.BB.CE.AE.CE.BC.CE.B1.CF.84.CE.B1)
*   [5 Εγκατάσταση του OpenOffice.org 1.1.4](#.CE.95.CE.B3.CE.BA.CE.B1.CF.84.CE.AC.CF.83.CF.84.CE.B1.CF.83.CE.B7_.CF.84.CE.BF.CF.85_OpenOffice.org_1.1.4)
    *   [5.1 Εγκατάσταση](#.CE.95.CE.B3.CE.BA.CE.B1.CF.84.CE.AC.CF.83.CF.84.CE.B1.CF.83.CE.B7_2)
    *   [5.2 Πρόσθετα](#.CE.A0.CF.81.CF.8C.CF.83.CE.B8.CE.B5.CF.84.CE.B1)
    *   [5.3 Ρυθμίσεις](#.CE.A1.CF.85.CE.B8.CE.BC.CE.AF.CF.83.CE.B5.CE.B9.CF.82)

## Εγκατάσταση

*   Κατ' αρχήν,χρειάζεται να κάνετε εγκατάσταση το Java Runtime Environment (προαιρετικά,αλλά καλό είναι να υπάρχει):

```
# pacman -S jre

```

*   Κατεβάστε το πακέτο base:

```
# pacman -S openoffice-base

```

*   Κάντε εγκατάσταση ένα ή περισσότερα γλωσσικά πακέτα.Το βήμα αυτό είναι προαιρετικό μια και τα Αγγλικά *περιλαμβάνονται* στο πακέτο base:

```
# pacman -S openoffice-XX (όπου XX είναι η γλώσσα σας)

```

*   Κάντε εγκατάσταση έναν ορθογράφο (προαιρετικό):

```
# pacman -S openoffice-spell-XX (όπου XX είναι η γλώσσα σας)

```

*   Οι ορθογράφοι και τα πακέτα γλωσσών μπορούν να βρεθούν στο [AUR](/index.php/AUR "AUR").

Παρατήρηση:Αν έχετε προβλήματα με την εκκίνηση του OpenOffice,πιθανόν να χρειαστεί να κάνετε εγκατάσταση τα πακέτα **libsndfile**. **libsndfile** μιας και δεν είναι στις εξαρτήσεις του **openoffice-base**. [Odd-rationale](/index.php/User:Odd-rationale "User:Odd-rationale") 21:26, 16 June 2008 (EDT)

## Ρύθμισεις του OpenOffice

Τρέξτε το '/opt/openoffice/program/soffice' για να ρυθμίσετε το OpenOffice 2 για τον χρήστη **και** για να ξεκινήσετε το OpenOffice 2.

Το OpenOffice 2 εισάγει την ικανότητα χρήσης πολλών εργαλείων για την κατάρτιση και τα ενσωματώνει σε διαφορετικά περιβάλλοντα εργασίας σε έναν καθαρό τρόπο.Πρέπει να ορίσετε την OOO_FORCE_DESKTOP μεταβλητή περιβάλλοντος, είτε system-wise(όπως και στο /etc/profile.d/) ή στο ειδικό shell του OpenOffice.org

Για να τρέξετε το OpenOffice.org σε κατάσταση GTK2 (χρησιμοποιώντας bash):

```
 # OOO_FORCE_DESKTOP=gnome soffice

```

Ίσως να θέλετε να το τοποθετήσετε και στο /usr/bin/soffice:

```
 export OOO_FORCE_DESKTOP=gnome

```

ή απλά τοποθετώντας το στο ~/.bashrc

```
export OOO_FORCE_DESKTOP=gnome

```

### Υποστήριξη πολυμέσων στο OpenOffice.org 2

Αν θέλετε να χρησιμοποιείτε ήχο και εικόνα στο OpenOffice.org Impress, πρέπει να κάνετε εγκατάσταση το [Java Media Framework](/index.php/Java_Media_Framework "Java Media Framework") και το [configure OpenOffice.org to use it](/index.php/Java_Media_Framework#Adding_media_support_to_OpenOffice.org "Java Media Framework")

### Χειροκίνητη εγκατάσταση λεξικών

Αν θέλετε για κάποιο λόγο να εγκαταστήσετε λεξικά πακετά χειροκίνητα (π.χ. να μην υπάρχουν πακέτα στη γλώσσα σας) ακολουθήστε τις παρακάτω οδηγίες:

*   Κατεβάστε το λεξικό για τη δική σας γλώσσα. Μια λίστα με τα υπάρχουσα πακέτα τωνλεξικών βρίσκεται στο [OOoDictionaries](http://wiki.services.openoffice.org/wiki/Dictionaries)
*   Αποσυμπιέστε τα στο /opt/openoffice/share/dict/ooo/

Τα απαραίτητα αρχεία ονομάζονται ως en_US.dic και en_US.aff για ορθογραφικό έλεγχο, hyph_en_US.dic για hyphenation λεξικά,th_en_US.dat και th_en_US.idx για τα αρχεία θησαυρός.

*   Ανοίξτε το /opt/openoffice/share/dict/ooo/dictionary.lst με τον αγαπημένο σας επεξεργαστή κειμένου.Προσθέστε τα επιθυμητά λεξικά στη λίστα,με τους παρακάτω κανόνες :

```
 # List of All Dictionaries to be Loaded by OpenOffice
 # ---------------------------------------------------
 # Each Entry in the list have the following space delimited fields
 #
 # Field 1: Entry Type "DICT" - spellchecking dictionary
 # "HYPH" - hyphenation dictionary
 # "THES" - thesaurus files
 #
 # Field 2: Language code from Locale "en" or "de" or "pt" ... 
 #
 # Field 3: Country Code from Locale "US" or "GB" or "PT"
 #
 # Field 4: Root name of file(s) "en_US" or "hyph_de" or "th_en_US
 # (do not add extensions to the name)

```

*   Ένα παράδειγμα χρησιμοποιώντας ελληνικά λεξικό είναι το παρακάτω:

```
 ### start gr
 HYPH el GR hyph_el_GR
 DICT el GR el_GR
 THES el GR th_el_GR_v2
 ### end gr

```

*   Αποθηκεύστε το αρχείο και επανεκκινήστε το OpenOffice. Σιγουρευτείτε ότι όλες οι διεργασίες του Openoffice έχουν τερματισθεί.Αλλιώς τα εγκατεστημένα λεξικά δεν θα λειτουργούν.

## Running

Αν θέλετε να τρέξετε μόνο μία εφαρμογή του OpenOffice.org (αντί για όλη την σουίτα), για παράδειγμα τον επεξεργαστή κειμένου (Write), η την εφαρμογή λογιστικών φύλλων (Calc) ή presentation program (Impress),ελέγξτε τα παρακάτω :

Writer

```
 /opt/openoffice/program/swriter

```

Calc

```
 /opt/openoffice/program/scalc

```

Impress

```
 /opt/openoffice/program/simpress

```

Math (Formula Editor)

```
 /opt/openoffice/program/smath

```

Base (Database frontend)

```
 /opt/openoffice/program/sbase

```

Printer Administration (προτείνετε να το τρέχετε ως υπερχρήστης/root)

```
 /opt/openoffice/program/spadmin

```

## Γνωστά προβλήματα

*   Αν έχετε προβλήματα αναβάθμισης από το OOo 1.1.x σε OOo 2.x δοκιμάστε τα εξής:

- If the install wizard asks you for taking old options from 1.1.x deny that.
- Αφαιρέστε τους παλιούς φακέλους του .openoffice* (κρυφός φάκελος) από το <home> σας
- Αφαιρέστε τους παλιούς φακέλους του OpenOffice* από το <home> σας
- Αφαιρέστε το .sversionrc από το <home> σας
Η ίδια διαδικασία ισχύει εάν το OOo τερματίζεται με μια εξαίρεση σαν *terminate called after throwing an instance of com::sun::star::uno::RuntimeException*.Αυτό μπορεί να γίνει σε μια αναβάθμιση,π.χ. από OOo 2.2 σε 2.3.

*   Για να αφαιρέσετε τις καταχωρήσεις στο μενού του OOo 1.1.x στο KDE:

- Αφαιρέστε το ~/.kde/share/applnk/OpenOffice*

*   Αν δεν μπορείτε να διαβάσετε/γράψετε σε δίσκους NFS ,επεξεργαστείτε το /opt/openoffice2/program/soffice. Θα πρέπει να απενεργοποιήσετε το file locking όπως παρακάτω:

```
# file locking now enabled by default
#SAL_ENABLE_FILE_LOCKING=1
#export SAL_ENABLE_FILE_LOCKING

```

*   Αν δεν μπορεί να ξεκινήσει με πιθανό σφάλμα javaldx: Could not find a Java Runtime Environment!

and then you get a plain error dialog about init failed, then remove your ~/.openoffice2 dir.

*   Αν το OpenOffice.org αποτύχει να ξεκινήσει,σιγουρευτείτε ότι έχετε τα σωστά δικαιώματα στο /etc/X11/xorg.conf, κοιτώντας στις ρυθμίσεις του DRI.
*   Σε περίπτωση αμφιβολίας, η παρακάτω ρύθμιση πρέπει να λειτουργήσει:

```
 Section "DRI"
 Group "users"
 Mode 0660
 EndSection

```

*   Ή αν δεν θέλετε να ενεργοποιήσετε το DRI,τρέξτε το ως ROOT.
*   Αν ο οδηγός εγκατάστασης εμφανίζεται κάθε φορά που ξεκινάει το OpenOffice (και η απόδοση είναι μειωμένη και κολλάει) τότε ελέγξτε τα δικαιώματα στο ~/.openoffice2; μπορεί να είναι στον root.

# Εγκατάσταση του OpenOffice.org 1.1.4

## Εγκατάσταση

*   Κατεβάστε το πακέτο base

```
# pacman -S openoffice-base

```

*   **Πρέπει να εγκαταστήσετε ένα πακέτο γλώσσας**, αλλιώς δεν θα μπορείτε να εκκινήσετε την εφαρμογή! (τα Αγγλικά δεν περιλαμβάνονται)

```
# pacman -S openoffice-XX (όπου XX είναι η γλώσσα σας)

```

*   **Ο ορθογραφικός έλεχγος** χρειάζεται πρόσθετα πακέτα!

```
# pacman -S openoffice-spell-XX (όπου XX είναι η γλώσσα σας)

```

## Πρόσθετα

Το OpenOffice.org quickstarter είναι διαθέσιμο για το KDE

```
# pacman -S oooqs

```

## Ρυθμίσεις

1.  Τρέξτε το '/opt/openoffice/setup' για να ρυθμίσετε το OpenOffice.org για τον χρήστη.
2.  Τρέξτε 'soffice' για να ξεκινήσετε το OpenOffice.org.