Παρακάτω αναφέρονται κάποιες χρήσιμες πληροφορίες και συμβουλές για τους νεοεισελθέντες στο Arch Linux.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Αυτόματη Αναγνώριση Hardware](#Αυτόματη_Αναγνώριση_Hardware)
*   [2 Επιτάχυνση της Διαδικασίας Εκκίνησης του Lilo](#Επιτάχυνση_της_Διαδικασίας_Εκκίνησης_του_Lilo)
*   [3 Πάυση στο Τέλος της Διαδικασίας Εκκίνησης](#Πάυση_στο_Τέλος_της_Διαδικασίας_Εκκίνησης)
*   [4 Χρωματίστε το PS1 και την Κονσόλα](#Χρωματίστε_το_PS1_και_την_Κονσόλα)
*   [5 "Ντοπαρισμένο" Less](#"Ντοπαρισμένο"_Less)
*   [6 Αλλάξτε τα Fonts της Κονσόλας](#Αλλάξτε_τα_Fonts_της_Κονσόλας)
*   [7 Δίνοντας Χρώμα σε μια Manpage](#Δίνοντας_Χρώμα_σε_μια_Manpage)
*   [8 Άμεση Πρόσβαση στο AUR](#Άμεση_Πρόσβαση_στο_AUR)
*   [9 Ενεργοποιώντας το Shellcompletion](#Ενεργοποιώντας_το_Shellcompletion)
*   [10 Ενεργοποιώντας την Υποστήριξη για Ποντίκι στην Κονσόλα (gpm)](#Ενεργοποιώντας_την_Υποστήριξη_για_Ποντίκι_στην_Κονσόλα_(gpm))
*   [11 Εκκινώντας τον X στο Boot](#Εκκινώντας_τον_X_στο_Boot)
*   [12 Ομορφαίνοντας τα Fonts στις LCD Οθόνες](#Ομορφαίνοντας_τα_Fonts_στις_LCD_Οθόνες)
*   [13 Ενεργοποιώντας το Numlock στο Bootup](#Ενεργοποιώντας_το_Numlock_στο_Bootup)
*   [14 ABS για να χτίζετε τα δικά σας πακέτα](#ABS_για_να_χτίζετε_τα_δικά_σας_πακέτα)
*   [15 Βελτιστοποιώντας τα πακέτα σας](#Βελτιστοποιώντας_τα_πακέτα_σας)
*   [16 Εξοικονομώντας χρόνο με Command-aliases](#Εξοικονομώντας_χρόνο_με_Command-aliases)
*   [17 Απενεργοποιώντας το IPv6](#Απενεργοποιώντας_το_IPv6)
*   [18 Χρήσιμες Εντολές & Προγράμματα](#Χρήσιμες_Εντολές_&_Προγράμματα)
    *   [18.1 pacman](#pacman)
    *   [18.2 makepkg](#makepkg)
    *   [18.3 ABS](#ABS)
*   [19 Αποσυμπιέζοντας συμπιεσμένα αρχεία](#Αποσυμπιέζοντας_συμπιεσμένα_αρχεία)

#### Αυτόματη Αναγνώριση Hardware

*   Το `lshwd` είναι το εργαλείο που θα σας πληροφορήσει σχετικό με το ποια *modules* θα χρειαστεί να φορτώσετε και να ρυθμίσετε.

*   Εναλλακτικά μπορείτε να χρησιμοποιήσετε το `hwdetect`. Κατά την εμπειρία του συγγραφέα του αγγλικού λήμματος, το συγκεκριμένο εντοπίζει περισσότερο *hardware* και είναι πιο γρήγορο από το lshwd. Για περισσότερες πληροφορίες: [hwdetect](/index.php/Hwdetect "Hwdetect")

#### Επιτάχυνση της Διαδικασίας Εκκίνησης του Lilo

*   Για να επιταχύνετε την διαδικασία εκκίνησης του lilo, προσθέστε την εντολή που ακολουθεί στο `/etc/lilo.conf`:

```
 compact

```

### Πάυση στο Τέλος της Διαδικασίας Εκκίνησης

*   Για να περάσετε σε πάυση στο τέλος της διαδικασίας εκκίνησης και πριν φτάσετε στο *login prompt* (συνήθως χρησιμοποιείται για το *debugging* των μηνυμάτων κατά την εκκίνηση), προσθέστε στο τέλος του `/etc/rc.local`:

```
 read KEY

```

*   ή αποσύρετε τον πρώτο χαρακτήρα στο αρχείο `/etc/issue`, το οποίο είναι ένα *escape code* για *"clear screen"*.
*   Εναλλακτικά, τρέχοντας το `dmesg` από το bash prompt, θα προβάλλει όλα τα μηνύματα κατά την εκκίνηση που προηγήθηκαν του initd.

### Χρωματίστε το PS1 και την Κονσόλα

Τα ~/.bashrc και /root/.bashrc περιέχουν τα *default* PS1 (*shell prompt*) *variables* για χρήστη και root, αντίστοιχα.

Ως χρήστης:

```
nano ~/.bashrc

```

Σχολιάστε το *default prompt*:

```
#PS1='[\u@\h \W]\$ '

```

Και προσθέστε:

```
PS1='\[\e[0;32m\]\u\[\e[m\] \[\e[1;34m\]\w\[\e[m\] \[\e[m\] \[\e[1;32m\]\$ \[\e[m\]\[\e[1;37m\] '

```

Αυτό θα δώσει ένα πολύ ευχάριστο, χρωματιστό prompt με φωτεινό άσπρο χρώμα για το κείμενο.

Ως root, επεξεργαστείτε το /root/.bashrc:

```
# nano /root/.bashrc

```

Σχολίαστε το *default* PS1:

```
#PS1='[\u@\h \W]\$ '

```

Το PS1 που ακολουθεί είναι χρήσιμο για *root bash prompt*, με κόκκινη εμφάνιση στο *prompt* και πράσινο χρώμα για το κείμενο.

```
PS1='\[\e[0;31m\]\u\[\e[m\] \[\e[1;34m\]\w\[\e[m\] \[\e[0;31m\]\$ \[\e[m\]\[\e[0;32m\] '

```

Για περισσότερα, δείτε το λήμμα [Color Bash Prompt](/index.php/Color_Bash_Prompt "Color Bash Prompt").

### "Ντοπαρισμένο" Less

Αν είστε συχνός χρήστης της κονσόλας, ίσως θα θελήσετε να εκγκαταστήσετε το *lesspipe* (το οποίο θα βρείτε στο AUR). Αυτό θα σας επιτρέψει να πληκτρολογήσετε:

```
less lesspipe.tar.gz
==> use tar_file:contained_file to view a file in the archive
-rw------- solstice/users  695 2008-01-04 19:24 lesspipe/PKGBUILD
-rw------- solstice/users   43 2007-11-07 11:17 lesspipe/lesspipe.sh
lesspipe.tar.gz (END)

```

και έτσι να χρησιμοποιήσετε το *less* για να δείτε το περιεχόμενο πολλών αρχείων αντί να χρησιμοποιείτε συγκεκριμένη εντολή κάθε φορά. Δώστε <tt>man lesspipe</tt> για να δείτε πως θα το ενεργοποιήσετε.

### Αλλάξτε τα Fonts της Κονσόλας

Το Terminus είναι μία δημοφιλής επιλογή μεταξύ των *Archers*. Το εγκαθιστάτε έτσι:

```
pacman -S terminus-font

```

Επεξεργαστείτε το /etc/rc.conf:

```
CONSOLEFONT="ter-v16b"

```

Αλλάξτε fonts *on-the-fly* με το **setfont**:

```
setfont ter-v16b

```

### Δίνοντας Χρώμα σε μια Manpage

Αν είστε νέος στο linux, θα χρειαστεί να διαβάσετε πολλές manpages αν θέλετε να μάθετε. Το χρώμα θα κάνει την παρουσίαση των περιεχομένων τους πιο ευκρινή και ίσως θα βοηθήσει στην πιο εύκολη εμπέδωσή τους. Για να κάνετε τις manpages να εμφανιστούν σε χρώμα, εγκαταστήστε κάποιο πρόγραμμα *reader* όπως το most(8).

```
pacman -S most

```

Το most είναι παρεμφερές με το less και το more αλλά επιτρέπει την εμφάνιση χρώματος στο κείμενο με πιο εύκολο τρόπο.

Για να το ενεργοποιήσετε, επεξεργαστείτε το αρχείο /etc/man.conf και αλλάξτε τις μεταβλητές PAGER και BROWSER σε:

```
PAGER           /usr/bin/most -s
BROWSER         /usr/bin/most -s

```

Τώρα μπορείτε να πληκτρολογήσετε:

```
man οποιαδήποτε_manpage

```

και να τη δείτε με ευκρινή χρώματα.

Αν θέλετε να αλλάξετε τα χρώματα, πειραματιστείτε με το αρχείο ~/.mostrc (δημιουργήστε το αν δεν υπάρχει) ή χρησιμοποιήστε το /etc/most.conf.

Παράδειγμα ~/.mostrc:

```
% Color settings

color normal lightgray black
color status yellow blue
color underline yellow black
color overstrike brightblue black

```

ένα άλλο παράδειγμα με *keybindings* τύπου less (*jump to line* με 'J'):

```
% less-like keybindings

unsetkey "^K"
unsetkey "g"
unsetkey "G"
unsetkey ":"

setkey next_file ":n"
setkey find_file ":e"
setkey next_file ":p"
setkey toggle_options ":o"
setkey toggle_case ":c"
setkey delete_file ":d"
setkey exit ":q"

setkey bob "g"
setkey eob "G"
setkey down "e"
setkey down "E"
setkey down "j"
setkey down "^N"
setkey up "y"
setkey up "^Y"
setkey up "k"
setkey up "^P"
setkey up "^K"
setkey page_down "f"
setkey page_down "^F"
setkey page_up "b"
setkey page_up "^B"
setkey other_window "z"
setkey other_window "w"
setkey search_backward "?"
setkey bob "p"
setkey goto_mark "'"
setkey find_file "E"
setkey edit "v"

```

Εναλλακτικά μπορείτε να πάρετε το ίδιο έγχρωμο αποτέλεσμα στις *manpages* με το less. Αυτή η μέθοδος έχει το πλεονέκτημα ότι το less είναι πιο πλούσιο σε χαρακτηριστικά σε σχέση με το most και έτσι είναι πολύ πιο χρήσιμο για τους προχωρημένους χρήστες. Απλά προσθέστε τα παρακάτω στο .SHELLrc

```
export LESS_TERMCAP_mb=$'\E[01;31m'
export LESS_TERMCAP_md=$'\E[01;31m'
export LESS_TERMCAP_me=$'\E[0m'
export LESS_TERMCAP_se=$'\E[0m'                           
export LESS_TERMCAP_so=$'\E[01;44;33m'                                 
export LESS_TERMCAP_ue=$'\E[0m'
export LESS_TERMCAP_us=$'\E[01;32m'

```

Πηγή: [http://nion.modprobe.de/blog/archives/572-less-colors-for-man-pages.html](http://nion.modprobe.de/blog/archives/572-less-colors-for-man-pages.html)

### Άμεση Πρόσβαση στο AUR

Όλοι θα πρέπει να γνωρίζουν πως να χρησιμοποιήσουν τα AUR, ABS και makepkg αν θέλουν να χτίσουν πακέτα. Όμως ο εντοπισμός και το update των custom πακέτων μπορούν να γίνουν κουραστικά, ειδικά αν έχετε πολλά. Υπάρχουν μερικά προγράμματα και scripts που βοηθούν στο να γίνει το χτίσιμο των custom πακέτων πιο εύκολο.

Το πιο δημοφιλές third-party πρόγραμμα που μπορεί να ψάξει στο και να εγκαταστήσει απευθείας από το AUR είναι το [yaourt](https://aur.archlinux.org/packages.php?ID=5863).

[Δείτε μία λίστα από άλλα προγράμματα που σας βοηθούν να προσβείτε στο AUR](/index.php/AUR_helpers "AUR helpers")

### Ενεργοποιώντας το Shellcompletion

Αυτό είναι ένα πολύ δημοφιλές χαρακτηριστικό από το οποίο χωρίς αμφιβολία θα ευεργετηθείτε σημαντικά.

```
pacman -S bash-completion

```

και κατόπιν προσθέστε

```
if [ -f /etc/bash_completion ]; then
    . /etc/bash_completion
fi

```

στο ~/.bashrc

### Ενεργοποιώντας την Υποστήριξη για Ποντίκι στην Κονσόλα (gpm)

*   Μπορείτε να ενεργοποιήσετε την υποστήριξη για ποντίκι στην κονσόλα εγκαθιστώντας το **gpm**:

```
pacman -S gpm

```

*   Αν δείτε τον κέρσορα του ποντικιού να τρεμοπαίζει και να μην λειτουργεί σωστά, θα πρέπει να αλλάξετε το `/etc/conf.d/gpm`.

**Για ποντίκι PS/2 αντικαταστήστε την υπάρχουσα γραμμή με:**

```
GPM_ARGS="-m /dev/psaux -t ps2"

```

**Για ποντίκι USB αντικαταστήστε την υπάρχουσα γραμμή με:**

```
GPM_ARGS="-m /dev/input/mice -t imps2"

```

**Για IBM Trackpoint, αντικαταστήστε την υπάρχουσα γραμμή με:**

```
GPM_ARGS="-m /dev/input/mice -t ps2"

```

*   Όταν λειτουργήσει σωστά, μπορείτε να προσθέσετε `gpm` στην `DAEMONS` σειρά στο `/etc/rc.conf` για να ξεκινά κάθε φορά με την εκκίνηση.
*   Η υποστήριξη για ποντίκι στην κονσόλα είναι χρήσιμη για πολλά πράγματα, συμπεριλαμβανομένων των προγραμμάτων Links και Lynx.

### Εκκινώντας τον X στο Boot

*   [Start X at login](/index.php/Start_X_at_login "Start X at login")

### Ομορφαίνοντας τα Fonts στις LCD Οθόνες

Δείτε το λήμμα [Fonts](/index.php/Fonts "Fonts"), και ιδιαίτερα τις δύο μεθόδους περιγράφονται στην παράγραφο 5.

### Ενεργοποιώντας το Numlock στο Bootup

*   [Activating numlock on bootup](/index.php/Activating_numlock_on_bootup "Activating numlock on bootup")

### ABS για να χτίζετε τα δικά σας πακέτα

*   Αν χρησιμοποιείτε το [ABS](/index.php/ABS "ABS") για να χτίζετε τα δικά σας πακέτα, θυμηθείτε να το κάνετε έξω από το κύριο /var/abs *tree*. Αντιγράψτε το PKGBUILD και όλα τα συνοδευτικά αρχεία σε ένα άδειο *directory* στο *homedir* σας και χτίστε από εκεί. Με αυτόν τον τρόπο δεν θα ρισκάρετε οι αλλαγές σας να χαθούν στο επόμενο τρέξιμο του `abs` και είναι πιο εύκολο να τις παρακολουθείτε.

### Βελτιστοποιώντας τα πακέτα σας

*   Για να βελτιστοποιήσετε τα πακέτα που χτίζετε χρησιμοποιώντας το makepkg (ο kernel είναι ένα καλό παράδειγμα), είσάγετε τις προτιμώμενες ρυθμίσεις σας του GCC στο `/etc/makepkg.conf`:

```
 (παράδειγμα για επεξεργαστή Athlon)
 export CFLAGS="-march=athlon -O2 -pipe -fomit-frame-pointer"
 export CXXFLAGS="-march=athlon -O2 -pipe -fomit-frame-pointer"

```

Για περισσότερες πληροφορίες δείτε το λήμμα [Safe CFlags](/index.php/Safe_Cflags "Safe Cflags").

### Εξοικονομώντας χρόνο με Command-aliases

*   Μπορείτε να δημιουργήσετε τα δικά σας commands-aliases κάνοντας χρησιμοποιώντας το `<homedir>/.bashrc` ή το `/etc/profile`. Και τα δύο μπορούν να χρησιμοποιηθούν για να καθορίσετε τα δικά σας aliases:

Παράδειγμα:

```
alias p="pacman"
alias ll="ls -lh"
alias la="ls -a"
alias exit="clear; exit"
alias x="startx"

# Lets you search through all available packages simply using 'pacsearch packagename'
alias pacsearch="pacman -Sl | cut -d' ' -f2 | grep "

# sudo pacman -Syu by typing pacup (sudo must be installed and configured first)
alias pacup="sudo pacman -Syu"

# sudo pacman -S by typing pac
alias pac="sudo pacman -S"

```

Για *output* με χρώματα στην αναζήτηση με pacman -Ss μπορείτε να προσθέσετε το παρακάτω:

```
# colorized pacman output with pacs alias:
alias pacs="pacsearch"
pacsearch () {
   echo -e "$(pacman -Ss $@ | sed \
     -e 's#core/.*#\\033[1;31m&\\033[0;37m#g' \
     -e 's#extra/.*#\\033[0;32m&\\033[0;37m#g' \
     -e 's#community/.*#\\033[1;35m&\\033[0;37m#g' \
     -e 's#^.*/.* [0-9].*#\\033[0;36m&\\033[0;37m#g' ) \
     \033[0m"
             }

```

### Απενεργοποιώντας το IPv6

Μέχρι να έρθει η ευρεία εξάπλωση και υιοθέτηση του IPv6, ίσως να ευεργετηθείτε από την απενεργοποίησή του. Για περισσότερα δείτε το λήμμα [Disabling the IPv6 Module](/index.php/IPv6_-_Disabling_the_Module "IPv6 - Disabling the Module").

### Χρήσιμες Εντολές & Προγράμματα

*   `grep` - ψάχνει για αρχεία κοιτώντας στα περιεχόμενά τους (παράδειγμα: το `grep -i syslog /etc/*` θα αναζητήσει όλα τα αρχεία στο /etc που περιέχουν την λέξη "syslog". ΜΗ case-sensitive αναζήτηση (χρησιμοποιώντας την παράμετρο `-i`)
*   `pkill/killall <process_name>` - κάνει kill σε διεργασίες (*processes*) κατά όνομα (παράδειγμα: `killall kdm`)
*   `ps` - προβάλλει το στάτους των διεργασιών (παράδειγμα: το `ps -xau` θα προβάλλει όλες τις ενεργές διεργασίες)
*   `locate` - εντοπίζει γρήγορα αρχεία στον σκληρό σας δίσκο (χρησιμοποιείστε πρώτα το `locate -u` για να δημιουργήσετε/ενημερώσετε τη βάση δεδομένων με τα αρχεία) (παράδειγμα: το `locate Xservers` θα εντοπίσει όλα τα αρχεία που ονομάζονται Xservers)

#### pacman

Υπάρχουν μερικοί ωραίοι τρόποι για να κάνετε κάποια πράγματα εύκολα με εντολές bash. Αν θέλουμε να εγκαταστήσουμε έναν αριθμό πακέτων που έχουν όμοια στοιχεία στα ονόματά τους - όχι όλο το group και ούτε και όλα τα πακέτα που έχουν αυτά τα όμοια στοιχεία - π.χ. **kdemod**, μπορούμε να κάνουμε το εξής:

```
pacman -S kdemod-{applets,theme,tools}

```

Φυσικά, δεν μας περιορίζει τίποτα εκεί, μπορούμε να επεκταθούμε σε όσα επίπεδα χρειαζόμαστε:

```
pacman -S kdemod-{ui-{kde,kdemod},kdeartwork}

```

Ο Pacman έχει την επιλογή **-q** για να κρύψει τη στήλη με τις εκδόσεις, και μπορούμε με αυτό να κάνουμε κάτι σαν την επανεγκατάσταση πακέτων που έχουν σαν μέρος του ονόματος του το "compiz":

```
pacman -S `pacman -Qq | grep compiz`

```

Το παραπάνω μπορεί να επιτευχθεί χωρίς το **-q** αν δοθεί μια **awk** λειτουργία:

```
pacman -S `pacman -Q | awk '{ print $1 }' | grep compiz`

```

Θέλετε να επανεγκαταστήσετε τα πάντα; Εύκολο! Μισό λεπτό - όχι τόσο γρήγορα. Η προβολή όλων των εγκατεστημένων πακέτων θα περιέχει όλα τα πακέτα, συμπεριλαμβανομένων αυτών που χτίστηκαν με *makepkg*. Απλά τρέχοντας pacman -S `pacman -Qq` θα επιστρέψει λάθη επειδή κάποια (ή πολλά) απ'αυτά δεν βρέθηκαν στη βάση δεδομένων. Χρειαζόμαστε έναν τρόπο να προβάλλουμε μόνο τα πακέτα που εγκαταστάθηκαν με τον pacman. Για να το κάνουμε αυτό, πρέπει να συνδυάσουμε μία εντολή που θα προβάλλει όλα τα πακέτα με μία άλλη που θα κρύβει τα "ξένα" πακέτα. Αυτό το πετυχαίνουμε με **-m** και **grep -v**.

```
pacman -S $(pacman -Qq | grep -v "`pacman -Qqm`")

```

Παρατηρείστε τις παρενθέσεις **$()** και τα **``** μεταξύ των εισαγωγικών (το **grep** θα αποτύχει επειδή χωρίς εισαγωγικά θα νομίσει ότι το κάθε *string* είναι ένα ανεξάρτητο *directory*). Μπορείτε να χρησιμοποιήσετε το τελευταίο για το πρώτο επίπεδο επίσης (ή να χρησιμοποιήσετε το πρώτο και για τα δύο επίπεδα) αλλά όπως κι αν γίνει, θυμηθείτε ότι οι παρενθέσεις είναι μια καλή πρακτική στα μαθηματικά και τον προγραμματισμό.

#### makepkg

Ένα αυτοματοποιημένο εργαλείο που δημιουργεί πακέτα - αυτό που πρακτικά κάνει είναι να αυτοματοποιεί τη διαδικασία `./configure && make && make install`, (ή όποιονδήποτε συνδυασμό εντολών χρησιμοποιείται για το χτίσιμο της εκάστοτε εφαρμογής) και πακετάρει την εφαρμογή σε ένα .pkg.tar.gz που θα εγκατασταθεί εύκολα με τον pacman. Χρησιμοποιεί ένα *script* αρχείο που ονομάζεται PKGBUILD και το οποίο πρέπει να υπάρχει μέσα στο directory όπου θα γίνει το χτίσιμο. Δείτε ένα αρχείο PKGBUILD και διαβάστε το κείμενο εγκατάστασης για να μάθετε περισσότερα σχετικά με το πως να δουλεύετε με το makepkg.

#### ABS

Ένα αυτοματοποιημένο toolkit που σας επιτρέπει να ξαναχτίσετε οποιοδήποτε από τα πακέτα του pacman. Τρέχοντας απλά abs θα συγχρονιστούν όλα τα PKGBUILD scripts από το *SVN repository* στο `/var/abs`.

### Αποσυμπιέζοντας συμπιεσμένα αρχεία

```
 file.tar : tar xvf file.tar
 file.tgz : tar xvzf file.tgz
 file.tar.gz : tar xvzf file.tar.gz
 file.bz : bzip -cd file.bz | tar xvf -
 file.bz2 : tar xvjf file.tar.bz2 **OR** bzip2 -cd file.bz2 | tar xvf -
 file.zip : unzip file.zip
 file.rar : unrar x file.rar

```

Η δομή αυτών των *tar arguments* είναι αρκετά αρχαία (αλλά χρήσιμη παρ'όλα αυτά). Δείτε την manpage του bsdtar στο τμήμα COMPATIBILITY για λεπτομέρειες σχετικά με τη λειτουργία τους. (το bsdtar περιέχεται στο πακέτο libarchive)