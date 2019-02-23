[Amarok](http://amarok.kde.org/) è un lettore e organizzatore musicale per Linux con un'interfaccia in [Qt](/index.php/Qt "Qt") intuitiva che si integra molto bene con [KDE](/index.php/KDE "KDE").

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Installazione](#Installazione)
*   [2 Personalizzazione](#Personalizzazione)
    *   [2.1 Integrazione con Gnome](#Integrazione_con_Gnome)
    *   [2.2 Script e applet](#Script_e_applet)
    *   [2.3 Barra dell'atmosfera](#Barra_dell'atmosfera)
*   [3 SHOUTcast](#SHOUTcast)
*   [4 Ampache/Riproduzione degli MP3](#Ampache/Riproduzione_degli_MP3)
*   [5 Database per la raccolta](#Database_per_la_raccolta)
    *   [5.1 MySQL](#MySQL)
    *   [5.2 PostgreSQL](#PostgreSQL)
*   [6 Firefly / Daap-Share](#Firefly_/_Daap-Share)
*   [7 Altri articoli correlati](#Altri_articoli_correlati)

## Installazione

Amarok può essere installato dal repository [extra] con pacman:

```
# pacman -S amarok

```

Amarok ora dipende da Phonon, quindi si dovrà avere un back-end funzionante selezionato per lui. Si può dare un'occhiata a [KDE#Phonon](/index.php/KDE#Phonon "KDE"). Si potrebbe essere interessati anche a installare alcuni [codecs](/index.php/Codecs "Codecs") per l'uso del back-end prescelto.

## Personalizzazione

### Integrazione con Gnome

Si veda [questo articolo](/index.php/Uniform_look_for_Qt_and_GTK_applications_(Italiano) "Uniform look for Qt and GTK applications (Italiano)") per un'integrazione grafica nella GUI principale.

### Script e applet

Nuovi script e applet possono essere trovati sia direttamente dentro Amarok ("Impostazioni" -> "Configura Amarok" -> "Script" -> "Gestisci Script") sia su [kde-apps.org](http://kde-apps.org/content/search.php).

### Barra dell'atmosfera

La barra dell'atmosfera (o moodbar) è una funzione che trasforma la propria barra di scorrimento della traccia in una barra di scorrimento colorata che dipende dall'**atmosfera** della traccia. Si può installare la [barra dell'atmosfera](https://aur.archlinux.org/packages.php?ID=6552) da [AUR](/index.php/AUR "AUR").

Poi andare in "Impostazioni" -> "Configura amarok" e spuntare "Mostra la barra dell'atmosfera nella barra di avanzamento".

Si noti che a partire dal 19 febbraio Amarok 2 NON genera moodfile, è possibile tuttavia provare a seguire questo tutorial [[1]](http://amarok.kde.org/wiki/Moodbar) per crearle da soli o installare Amarok 1.4 da AUR e lasciargli creare tutti i file .mood che si desidera. Per questa soluzione andare in "Impostazioni" -> "Configura amarok", e nella scheda generale spuntare "use moods" e i box "store moods data files with music".

## SHOUTcast

Per ottenere SHOUTcast usa lo script "SHOUTcast service". Avviare Amarok, andare in "Impastazioni" -> "Configura Amarok" -> Tab "Script" -> "Gestisci gli script" -> cercare SHOUTcast -> installare il servizio Shoutcast, riavviare Amarok. Si ha poi nel contesto "Internet".

Vedi anche: [Come posso usare Amarok per trasmettere la mia stazione radio? (inglese)](http://amarok.kde.org/wiki/FAQ#How_can_I_use_Amarok_to_stream_to_my_own_radio_station.3F), che raccomanda [Internet DJ Console](http://giss.tv/sahabuntu/doc/idjc.html), reperibile in AUR ([idjc](https://aur.archlinux.org/packages/idjc/)).

## Ampache/Riproduzione degli MP3

Se si riproducono MP3 direttamente o con il plugin Ampache Plugin, non è possibile ricercare tracce se non si usa il backend gstreamer. Installarlo con:

```
# pacman -S phonon-gstreamer gstreamer0.10 gstreamer0.10-plugins

```

Poi andare su Amarok in "Impostazioni" -> "Configura Amarok" -> "Riproduzione" -> "Configura Phonon" -> Tab "Backend" -> imposta Gstreamer come Backend preferito

## Database per la raccolta

Amarok 2.x può usare sqlite (default) o mysql per memorizzare il database di raccolta. Gli utenti con grandi raccolte e più esigenti in termini di prestazioni potrebbero preferire mysql.

### MySQL

Per una configurazione di base di MySQL riferirsi alla pagina [MySQL](/index.php/MySQL_(Italiano) "MySQL (Italiano)").

Quando si usa Amarok con MySQL è necessario creare un utente MySQL che può accedere al database. Per fare questo, dare i seguenti comandi:

```
# mysql -p -u root
# CREATE DATABASE amarokdb;
# USE amarokdb;
# GRANT ALL ON amarokdb.* TO amarokuser@localhost IDENTIFIED BY 'password-user';
# FLUSH PRIVILEGES;
# quit

```

Questo crea un database di nome 'amarokdb' e un utente con il nome 'amarokuser' con la password 'password-user' che può accedere al suddetto database da localhost. Se si desidera connettersi al proprio computer con il database da un altro computer, cambiare la riga in

```
# GRANT ALL ON amarok.* TO amarokuser@'%' IDENTIFIED BY  'password-user';

```

Per ordinare ad Amarok di usare MySQL, entrare nella schermata di configurazione di Amarok, scegliere Database e spuntare 'Utilizza database MySQL esterno'. Impostare il server (di solito "localhost"), il nome utente ("amarokuser" in questo esempio) e la password utente scelta. Non dimenticarsi di scegliere il percorso alla propria raccolta musicale.

### PostgreSQL

Non ancora supportato, [maggiori informazioni](http://amarok.kde.org/blog/archives/812-MySQL-in-Amarok-2-The-Reality.html).

## Firefly / Daap-Share

Per rendere le condivisioni DAAP visibili in Amarok abilitare il plugin "DAAP Collection" nelle impostazioni di Amarok.

Installare nss-mdns:

```
# pacman -S nss-mdns 

```

e completare la riga host in /etc/nsswitch.conf in questo modo:

```
hosts: files mdns4_minimal [NOTFOUND=return] nis dns mdns4

```

avviare il demone avahi e aggiungerlo in /etc/rc.conf:

```
# /etc/rc.d/avahi-daemon start

```

## Altri articoli correlati

[Applicazioni audio più comuni](/index.php/Common_Applications_(Italiano)#Audio "Common Applications (Italiano)")