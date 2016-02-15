Ο **MPlayer** είναι το πιο δημοφιλές πρόγραμμα αναπαραγωγής video για το Linux. Ο MPlayer υποστηρίζει σχεδόν όλα τα format ήχου και video που υπάρχουν οπότε είναι πολύ ευέλικτος, αν και οι περισσότεροι τον χρησιμοποιούνε για την αναπαραγωγή video.

## Contents

*   [1 Εγκατάσταση](#.CE.95.CE.B3.CE.BA.CE.B1.CF.84.CE.AC.CF.83.CF.84.CE.B1.CF.83.CE.B7)
*   [2 Πρόσθετες συμβουλές εγκατάστασης](#.CE.A0.CF.81.CF.8C.CF.83.CE.B8.CE.B5.CF.84.CE.B5.CF.82_.CF.83.CF.85.CE.BC.CE.B2.CE.BF.CF.85.CE.BB.CE.AD.CF.82_.CE.B5.CE.B3.CE.BA.CE.B1.CF.84.CE.AC.CF.83.CF.84.CE.B1.CF.83.CE.B7.CF.82)
    *   [2.1 Περισσότερα codecs (κωδικοποιητές)](#.CE.A0.CE.B5.CF.81.CE.B9.CF.83.CF.83.CF.8C.CF.84.CE.B5.CF.81.CE.B1_codecs_.28.CE.BA.CF.89.CE.B4.CE.B9.CE.BA.CE.BF.CF.80.CE.BF.CE.B9.CE.B7.CF.84.CE.AD.CF.82.29)
    *   [2.2 Frontends/GUIs](#Frontends.2FGUIs)
    *   [2.3 Ενσωμάτωση σε Browser](#.CE.95.CE.BD.CF.83.CF.89.CE.BC.CE.AC.CF.84.CF.89.CF.83.CE.B7_.CF.83.CE.B5_Browser)
        *   [2.3.1 Firefox](#Firefox)
        *   [2.3.2 Konqueror](#Konqueror)
*   [3 Χρήση](#.CE.A7.CF.81.CE.AE.CF.83.CE.B7)
    *   [3.1 Ρύθμιση](#.CE.A1.CF.8D.CE.B8.CE.BC.CE.B9.CF.83.CE.B7)
    *   [3.2 Παρακολουθώντας Video streams](#.CE.A0.CE.B1.CF.81.CE.B1.CE.BA.CE.BF.CE.BB.CE.BF.CF.85.CE.B8.CF.8E.CE.BD.CF.84.CE.B1.CF.82_Video_streams)
    *   [3.3 Συντομεύσεις πληκτρολογίου](#.CE.A3.CF.85.CE.BD.CF.84.CE.BF.CE.BC.CE.B5.CF.8D.CF.83.CE.B5.CE.B9.CF.82_.CF.80.CE.BB.CE.B7.CE.BA.CF.84.CF.81.CE.BF.CE.BB.CE.BF.CE.B3.CE.AF.CE.BF.CF.85)
*   [4 Εξωτερικοί σύνδεσμοι](#.CE.95.CE.BE.CF.89.CF.84.CE.B5.CF.81.CE.B9.CE.BA.CE.BF.CE.AF_.CF.83.CF.8D.CE.BD.CE.B4.CE.B5.CF.83.CE.BC.CE.BF.CE.B9)

### Εγκατάσταση

Πληκτρολογείστε `pacman -S mplayer` σε ένα κέλυφος ως root. Τελειώσατε.

## Πρόσθετες συμβουλές εγκατάστασης

### Περισσότερα codecs (κωδικοποιητές)

Για αξιοποιήσετε όσον το δυνατόν περισσότερο των MPlayer, πρέπει να εγκαταστήσετε το πακέτο `codecs`, το οποίο προσθέτει υποστήριξη για Windows codecs, Real9 codecs και Quicktime codecs(.mov). Πληκτρολογήστε `pacman -S codecs` και είστε έτοιμοι.

### Frontends/GUIs

Υπάρχουν αρκετά GUIs για τον MPlayer αν πρέπει να χρησιμοποιήσετε ένα. To πακέτο `smplayer` περιέχει ένα από αυτά και το πακέτο `smplayer-themes` παρέχει θέματα για αυτό.

### Ενσωμάτωση σε Browser

Εάν θέλετε να αφήσετε τον MPlayer να ελέγχει την αναπαραγωγή video στον αγαπημένο σας web browser, δοκιμάστε ένα από τα ακόλουθα:

#### Firefox

`pacman -S mplayer-plugin`

#### Konqueror

`pacman -S kmplayer` (επίσης παρέχει ένα πλήρες frontend για τον MPlayer.)

## Χρήση

### Ρύθμιση

Οι γενικές ρυθμίσεις για τον MPlayer, που αφορούν όλο το σύστημα, βρίσκονται στο `/usr/local/etc/mplayer/mplayer.conf`, ενώ οι τοπικές ρυθμίσεις των χρηστών αποθηκεύονται στο `~/.mplayer/config`.

### Παρακολουθώντας Video streams

Εάν θέλετε να αναπαράγετε ένα video stream (π.χ. ένα *.asx σύνδεσμο) χρησιμοποιείστε την εντολή `mplayer -playlist linktostream.asx`, καθώς αυτές είναι λίστες αναπαραγωγής stream και δεν θα ήταν δυνατόν να αναπαραχθούν παραλείποντας την επιλογή -playlist.

### Συντομεύσεις πληκτρολογίου

	_Αυτή είναι μια λίστα με τις πιο γνωστές συντομεύσεις πληκτρολογίου για τον MPlayer_

| Πλήκτρο | Περιγραφή |
| p | Εκκίνηση/παύση αναπαραγωγής |
| Space | Εκκίνηση/παύση αναπαραγωγής |
| Left | Αναζήτηση 10 δευτερολέπτων προς τα πίσω |
| Right | Αναζήτηση 10 δευτερολέπτων προς τα μπροστά |
| Down | Αναζήτηση 1 λεπτού προς τα πίσω |
| Up | Αναζήτηση 1 λεπτού προς τα μπροστά |
| < | Προηγούμενο αρχείο στον playlist |
| > | Επόμενο αρχείο στον playlist |
| m | Σίγαση ήχου |
| 0 | Αύξηση έντασηςήχου |
| 9 | Μείωση έντασης ήχου |
| f | Εναλλαγή πλήρους οθόνης |
| o | Εμφάνιση/απόκρυψη OSD |
| j | Εμφάνιση/απόκρυψη υποτίτλων |
| `I` | Εμφάνιση ονόματος αρχείου |
| 1, 2 | Ρύθμιση αντίθεσης |
| 3, 4 | Ρύθμιση φωτεινότητας |

## Εξωτερικοί σύνδεσμοι

*   [Official MPlayer website](http://www.mplayerhq.hu/)