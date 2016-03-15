[LAMP](https://en.wikipedia.org/wiki/LAMP_(software_bundle) αναφέρεται σε ένα κοινό συνδυασμό προγραμμάτων που χρησιμοποιείται σε πολλούς web servers: **L**inux, **A**pache, **M**ySQL, και **P**HP. Αυτό το άρθρο περιγράφει την παραμετροποίηση ενός [Apache HTTP Server](http://httpd.apache.org) σε ένα Arch Linux σύστημα. Επίσης, περιγράφει την προαιρετική εγκατάσταση της [PHP](/index.php/PHP "PHP") και της [MySQL](/index.php/MySQL "MySQL") και την ενσωμάτωση τους στον Apache Server.

Αν χρειάζεστε απλά έναν web server για ανάπτυξη λογισμικού και δοκιμές, ο [Xampp](/index.php/Xampp "Xampp") ίσως είναι μια καλυτέρη και πιο εύκολη επιλογή.

## Εγκατάσταση

```
# pacman -S apache php php-apache mysql

```

Σε αυτό το άρθρο υποθέτουμε ότι θα εγκαταστήσετε Apache, PHP και MySQL μαζί. Φυσικά, μπορείτε να εγκαταστήσετε Apache, PHP και MySQL ξεχωριστά και να προχωρήσετε στις αντίστοιχες ενότητες παρακάτω.

**Note:** Νέο προεπιλεγμένο user και group: Αντί για το group "nobody", o apache τώρα τρέχει ως user/group "http" από προεπιλογή. Προσαρμόστε το httpd.conf σύμφωνα με αυτή την αλλαγή, αν και ίσως θέλετε να τρέξετε το httpd ως nobody.

## Παραμετροποίηση

### Apache

Για λόγους ασφαλείας, από την στιγμή που ξεκινήσει ο Apache από τον root χρήστη (άμεσα ή μέσω startup scripts) αλλάζει στο UID/GID που ορίζεται στο `/etc/httpd/conf/httpd.conf`

*   Ελέγξτε για την ύπαρξη του χρήστη http ψάχνοντας στην έξοδο της ακόλουθης εντολής:

```
 # grep http /etc/passwd

```

*   Δημιουργήστε τον χρήστη http αν δεν υπάρχει ήδη:

```
 # useradd -d /srv/http -r -s /bin/false -U http

```

	Έτσι δημιουργείται ο χρήστης http με φάκελο home `/srv/http/`, ως λογαριασμός του συστήματος (-r), με ψευδές shell (-s `/bin/false`) και δημιουργείται ένα group με το ίδιο όνομα (-U).