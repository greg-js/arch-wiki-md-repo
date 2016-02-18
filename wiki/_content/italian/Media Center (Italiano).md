Questo articolo guiderà l'utente alla creazione, installazione e configurazione di un Media Center sfruttando come base Arch Linux.

Un media center è un computer adibito all'ascolto di musica, visione di film e immagini memorizzati in un hard disk o in una rete (a volte anche wireless), visione di film DVD e spesso per guardare e registrare trasmissioni televisive. Alcuni software possono anche fare altre cose, come recapitare news (RSS) da internet. I media center sono spesso dotati di un telecomando, connessi ad un televisore.

## Contents

*   [1 Il mediacenter ideale](#Il_mediacenter_ideale)
    *   [1.1 Software](#Software)
    *   [1.2 Hardware](#Hardware)
    *   [1.3 Aspettando la domotica](#Aspettando_la_domotica)
*   [2 Una tv minimalista](#Una_tv_minimalista)
    *   [2.1 Il firmware](#Il_firmware)
    *   [2.2 Sintonizzazione dei canali](#Sintonizzazione_dei_canali)
    *   [2.3 Xine e mplayer](#Xine_e_mplayer)
*   [3 Un pvr molto kiss](#Un_pvr_molto_kiss)
*   [4 Un mediacenter accattivante](#Un_mediacenter_accattivante)
    *   [4.1 Prime configurazioni](#Prime_configurazioni)
    *   [4.2 Organizzare i media](#Organizzare_i_media)
    *   [4.3 La tv](#La_tv)
*   [5 Usare qualsiasi telecomando...](#Usare_qualsiasi_telecomando...)
    *   [5.1 Riconoscimento del ricevitore IR](#Riconoscimento_del_ricevitore_IR)
    *   [5.2 Configurare lirc](#Configurare_lirc)
        *   [5.2.1 Il driver /dev/lirc0](#Il_driver_.2Fdev.2Flirc0)
        *   [5.2.2 Il driver /dev/input](#Il_driver_.2Fdev.2Finput)
    *   [5.3 IRW ed eccezione in HAL](#IRW_ed_eccezione_in_HAL)
    *   [5.4 I telecomandi universali](#I_telecomandi_universali)
*   [6 ... per fare qualsiasi cosa](#..._per_fare_qualsiasi_cosa)
    *   [6.1 Configuriamo xine](#Configuriamo_xine)
    *   [6.2 Configuriamo xbmc](#Configuriamo_xbmc)
    *   [6.3 irxevent per registrare 'on the fly' la tv digitale con xine](#irxevent_per_registrare_.27on_the_fly.27_la_tv_digitale_con_xine)
    *   [6.4 irexec per avviare e spengere una applicazione con un singolo bottone](#irexec_per_avviare_e_spengere_una_applicazione_con_un_singolo_bottone)
*   [7 Il backup perfetto](#Il_backup_perfetto)

## Il mediacenter ideale

Il Personale Computer e' ormai diventato un meta-medium, un media che comprende tutti gli altri. La convergenza si e' realizzata da tempo: la musica e' 'liquida', i film vengono ormai largamente condivisi, le macchine fotografiche sono tutte digitali, internet a banda larga... Nonostante questo la situazione attuale nelle nostre case e' più' o meno la stessa di diversi anni fa': spesso il pc vero e proprio e' in un angolo della casa; ci sono 10 telecomandi, istruzioni, garanzie, interfacce da imparare... registrare una trasmissione televisiva e' una impresa e siamo ancora legati agli orari del flusso televisivo. Comunque e in ogni caso PC camuffati stanno gradualmente spostandosi in salotto e sostituendo la TV tradizionale. Pensiamo alle console giochi, a mysky ai lettori mulimediali che vengono venduti... In questo wiki vedremo come configurare un pc che dovrebbe fare tutto cio' che si possa desiderare in una casa, dovrebbe stare in salotto e comunicare in rete con gli altri PC della casa. Di seguito le scelte principali per questo Mediacenter divise tra Hardware e Software.

### Software

*   Sistema Operativo: [Linux](http://www.linux.it)
*   Distribuzione: [ArchLinux](http://www.archlinux.it/)
*   Desktop Environment: [Gnome](http://www.it.gnome.org/index.php/Home), [kde](http://www.kde.org/), [lxde](http://lxde.org/), [openbox](http://openbox.org/)... Una delle caratteristiche della distribuzione Arch e' quella di 'essere quello che vuoi'
*   MediaCenter: [xbmc](/index.php/Media_Center_(Italiano)#Un_mediacenter_molto_figo "Media Center (Italiano)")
*   Controllo Remoto: [lirc](/index.php/Media_Center_(Italiano)#Usare_qualsiasi_telecomando... "Media Center (Italiano)")
*   Backup: [rsnapshot](/index.php/Media_Center_(Italiano)#Il_backup_perfetto "Media Center (Italiano)")

### Hardware

*   PC principale: Questo e' il MC vero e proprio oltre ad essere un pc normale. Puo' essere usato a vari livelli: dalla potenza della linea di comando, ai pochi semplici pulsanti di un telecomando passando dalle varie interfacce grafiche. Un pc con un front end grafico bello e facile da usare. Fa' da server agli altri e contiene tutti i dati e le risorse (vedi sotto) che condivide in rete. Dovrebbe essere il meno ingombrante possibile, silenzioso, avere due HD: uno per il sistema operativo e uno per i dati, quindi molto capiente. Dovrebbe avere uscite hdmi, audio 5.1 digtale...
*   Schermo: collegato al pc principale serve per vedere i filmati e godere di un buona e robusta interfaccio grafica. Dovrebbe essere grande e sostituire quello della tv, spesso sarà proprio quello della tv. Opzionalmente si potrebbe collegare un secondo monitor per usare il pc come tale ed in contemporanea alla visione di film.
*   Sintonizzatori tv: quanti ne servono? quanti siamo in famiglia? Quanto viene vista la tv? Almeno uno ma anche due: uno per vedere uno per registrare. Il grande vantaggio di avere il sintonizzatore connesso al pc (non integrato nel monitor come di fatto e' l'attuale tv) e' che si può in questo modo registrare e sostituire il videoregistratore. Ma ci sono anche i vantaggi della gestione centralizzata e quindi dell'ottimizzazione delle risorse.
*   Casse 5.1 Importante che nel pc ci sia una scheda audio adeguata per avere un suono corposo e nitido per sfruttare anche gli effetti sonori dei titoli cinematografici più evoluti.
*   HardDisk: L'ideale sarebbe avere due HD fisici distinti interni: uno per il sistema operativo, che una volta configurato e ben ottimizzato dovrebbe essere clonato e backuppato nel secondo disco, che contiene i dati (Video, Musica, Foto...). Quest'ultimo dovrebbe essere backuppato interamente tramite un sistema a snapshot in un disco esterno.
*   Rete: tutti i PC dovrebbero essere interconnessi tra loro in rete locale cablata o wireless a seconda di gusti o possibilità (cavi, switch, routers , access point)
*   PC portatili: Ogni membro della famiglia alla fine dovrà avere il suo Personal Computer e il MC farà da server che contiene i dati e mette a disposizione le risorse per tutti.
*   Telecomandi: uno a testa che controllano tutto
*   Multifunzione a colori: Collegata in rete e disponibile a tutti i pc (stampa, copia, scanner...)
*   Palmari: collegati ai pc della rete in modo da sincronizzare i dati (agenda, posta, rubrica ecc..)
*   ...

### Aspettando la domotica

Quella sopra riportata non e' fantascienza ma tecnologia disponibile oggi non a costi esorbitanti: se facciamo il conto di quanto viene speso oggi dalle famiglie per esaurire le esigenze mediatiche coperte dallo scenario sopra riportato, vedremo che non si parla di una spesa maggiore ma forse diversa. Il problema principale di questo tipo di scelta stà nelle competenze informatiche necessarie alla completa configurazione iniziale e gestione del sistema.

Un altro media che e' vicino se non gia' inglobato nel PC e' il telefono: le video chiamate e skype non sono fantascienza e social network, chat, sms e dispositivi mobili sono ormai delle alternative usate quotidianamente. La domotica sembra lontana anche se far controllare al pc il termostato del riscaldamento e le luci di casa e' molto vicino e alla portata dello scenario sopra descritto.

Questi processi non si stravolgono dall'oggi al domani ma e' una evoluzione gia' in divenire. Quella presentata e' una delle visioni di prospettiva che guidano un percorso graduale, fatto di tappe, acquisti, tentativi riusciti o meno...

Uno dei problemi piu' grossi per gli utenti Linux e' il supporto HW... ma la forza più grossa e' la collaborazione, la condivisone degli sforzi il mettere d'accordo e armonizzare più visioni... la comunità. Questo wiki cerca di andare in questa direzione.

## Una tv minimalista

Nella configurazione del MC partiamo dalle basi e affrontiamo subito l'attuale regina nei salotti delle nostre case: la TV. Basta poco per riuscire a ottenere facilmente dal nostro PC quello che abbiamo oggi da una TV. In seguito daremo l'esempio del sintonizzatore Hauppauge WinTV MiniStick HD ma, a parte le piccole differenze specifiche, il wiki vale anche per altri sintonizzatori.

### Il firmware

Come ben indicato in [questo articolo](http://www.linux-magazine.it/La-TV-a-passeggio-pag_3.htm) scarichiamo e installiamo il firmware

```
cd /lib/firmware
sudo wget [http://steventoth.net/linux/sms1xxx/sms1xxx-hcw-55xxx-dvbt-02.fw](http://steventoth.net/linux/sms1xxx/sms1xxx-hcw-55xxx-dvbt-02.fw)

```

anche se forse questo passaggio con le nuove versioni di linux-firmware non e' necessario. Il sintonizzatore dovrebbe essere visibile dal kernel. Verifichiamo:

```
lsusb
Bus 002 Device 002: ID 2040:c000 Hauppauge Windham

```

Bene, ora dobbiamo sintonizzare i canali.

### Sintonizzazione dei canali

Molti programmi eseguono automaticamente la sintonizzazione dei canali una volta trovato il sintonizzatore. In questi casi, tra i canali sintonizzati dall'applicativo si tratta di scegliere quelli preferiti. Di seguito vengono illustrati due metodi minimalisti e abbastanza manuali: Il primo usa una utility **scan** contenuta in linuxtv-dvb-apps:

```
sudo pacman -S linuxtv-dvb-apps

```

che prende come input una lista di 'trasmettitori'. Una base la troviamo qui:

```
ls cd /usr/share/dvb/dvb-t/it-*

```

queste liste costituiscono una buona base di partenza che sarebbe comunque bene integrare cercando in internet gli eventuali aggiornamenti. Poi procediamo alla sintonizzazione ad es.

```
scan /usr/share/dvb/dvb-t/it-firenze > channels.conf

```

chiaramente bisogna sostituite il nome della citta' dell'esempio sopra riportato con quella a noi piu' vicina. La lista dei canali che il sintonizzatore trova viene salvata nel file channels.conf che contiene righe di questo genere:

```
ITALIA 1:826000000:INVERSION_AUTO:BANDWIDTH_8_MHZ:FEC_2_3:FEC_AUTO:QAM_64:TRANSMISSION_MODE_8K:GUAR_INTERVAL_1_32:HIERARCHY ...

```

dove la prima parte fino ai due punti contiene il nome del canale che possiamo cambiare. Possiamo per comodita' togliere spazi e maiuscole

```
italia1:826000000:INVERSION_AUTO:BANDWIDTH_8_MHZ:FEC_2_3:FEC_AUTO:QAM_64:TRANSMISSION_MODE_8K:GUARD_INTERVAL_1_32:HIERARCHY ...

```

e commentare con # i canali che non ci interessano. Un'altro modo piu' semplice e' usare **w_scan**

```
yaourt -S w_scan
w_scan -X -P -t 2 -E 0 -c IT > channels.conf

```

Anche in questo caso possiamo semplificare i nomi dei canali trovati. Ora possiamo finalmente iniziare a vedere la tv.

### Xine e mplayer

Due programmi molto minimalisti che fanno tra le altre cose *anche* questo sono mplayer e xine

```
sudo pacman -S mplayer xine-ui

```

copiamo i canali sintonizzati e personalizzati. Nel caso di mplayer

```
sudo cp channels.conf /etc/mplayer/channels.conf

```

oppure per xine

```
cp channels.conf .config/xine-lib/channels.conf

```

facciamo partire mplayer con

```
mplayer dvb://

```

che partira' sul primo canale della lista. Oppure partiamo da un canale specifico. In questo caso ci tornera' utile la semplificazione fatta prima sulla lista dei canali

```
mplayer dvb://italia1

```

scorriamo tra i canali con i tasti 'k' e 'v'. Per farlo partire direttamente in full screen:

```
mplayer -fs dvb://italia1

```

Per far partire la tv con xine in full screen:

```
xine -f dvb://

```

Con xine si cambia canale con i tasti freccia su e giu del keypad e la lista canali scritta in sovraimpressione, e tra un canale e l'altro non si vede lo sfondo scrivania come in mplayer ma si freeza l'immagine tv rendendo molto piu' piacevole lo zapping. Con il tasto F1 viene inoltre registrato il programma live 'on the fly' sull'hd senza interrompere la visione. Per vedere la lista completa delle scorciatoie da tastiera possibili possiamo lanciare il seguente comando:

```
xine --keymap > xinekeymap.

```

Sempre nello stile minimalista possiamo utilizzare un semplice script come PVR (videregistratore).

## Un pvr molto kiss

Per programmare semplici registrazioni di trasmissioni tv in digitale terrestre con Linux non servono programmi complicati. XBMC e' un sw [mediacenter](/index.php/User:Stele#Il_mediacenter_ideale "User:Stele"), molto ben fatto e completo che [vedremo in seguito](/index.php/User:Stele#Un_mediacenter_molto_figo "User:Stele") ma non ha la possibilità di registrare direttamente le trasmissioni TV. Si appoggia a tvheadend che registra tramite le guide elettroniche dei programmi (EPG) che in Italia sono poco affidabili. Abbiamo la possibilità di programmare ed effettuare le registrazioni con gli strumenti di base previsti in tutte le distribuzioni: uno script bash e la programmazione su crontab. Abbiamo inoltre bisogno di un [sintonizzatore tv configurato](/index.php/User:Stele#Una_tv_minimalista "User:Stele") e del programma mencoder

```
yaourt -S mencoder

```

Dobbiamo poi [effettuare la sintonizzazione dei canali per mplayer per avere una tv minimalista funzionante](/index.php/User:Stele#Una_tv_minimalista "User:Stele") con i canali definiti in .mplayer/channels.conf magari con nomi in minuscolo e senza spazio per semplicità come abbiamo visto sopra. Salviamo infine [questo script](http://pastebin.com/k2a2HGSH) in un posto sicuro e per praticità e pulizia facciamo un collegamento a /usr/bin.

```
sudo ln -s /percorso/allo/script /usr/bin/registra

```

La compressione 'on the fly' viene fatta da questo comando

```
 mencoder -o nome_file.avi -ovc xvid -xvidencopts bitrate=800 -oac mp3lame -lameopts cbr:br=128 dvb://

```

è migliorabile qualitativamente aumentando il bitrate. Possiamo anche registrare lo streaming senza comprimerlo. Dopo averlo controllato se non ci serve lo buttiamo altrimenti [facciamo i tagli con projectx](http://telperion.wordpress.com/2007/05/05/dvb-demux-cut-repair-con-projectx/) e [comprimiamo con HandBrake](http://telperion.wordpress.com/2009/01/17/codifica-video-h264-o-divx-xvid-con-handbrake/) come suggerito molto bene sempre ed esaustivamente [in questo sito](http://telperion.wordpress.com/). Sembra lungo ma con la versione interfaccia a linea di comando

```
sudo pacman -S handbrake-cli

```

e l'utlizzo di [questo script](http://pastebin.com/jpgiCA8K) alla fine si tratta di operazioni manuali di pochi secondi e pochi minuti di elaborazione. Contrariamente a mencoder handBrake sfrutta ad esempio i processori dual core. Rimane solo da programmare le registrazioni. Possiamo controllare guida tv da internet in siti [come questo](http://www.mymovies.it/tv/digitaleterrestre/) e poi programmare la registrazione su crontab che potrebbe presentarsi in modo simile:

```
$crontab -e
#PVR KISS==================================
# Feriali alle 10.40
40 10 * * 1-5 registra k2 60 Mr_Bean
# Feriali alle 16.55
55 16 * * 1-5 registra k2 35 Mr_Bean

# Esclusa domenica alle 20.20
20 20 * * 1-6 registra boing 35 Scooby-Doo-New

# I Sabati alle 19
00 19 * * 6 registra italia1 35 Scooby-Doo

# Sabato e Domenica alle 8.30
30 08 * * 6-7 registra gulp 25 Geronimo
# Sabato e Domenica alle 14.05
05 14 * * 6-7 registra gulp 25 I Flintstones

# Le Domeniche alle 10.25
25 10 * * 7 registra boing 45 Scooby-Doo-Speciale
#====================================================

```

Viene prima indicato l'orario in cui parte la registrazione, i giorni in cui effettuarla, il comando con cui e' stato fatto il collegamento allo script (in questo caso 'registra'), il canale da registrare, la durata della registrazione ed opzionalmente il nome del programma e se lo vogliamo compattare o meno. Per cambiare editor di crontab al posto di vi aggiungere al file ~/.bashrc la seguente riga

```
export VISUAL="/usr/bin/nano"

```

Possono essere utili ( anche perche' scritte in modo sintetico) [queste indicazioni su wikipedia](http://it.wikipedia.org/wiki/Crontab) per personalizzare crontab. Si tratta di un sistema molto semplice di registrazione. Se le necessita' crescono (ad es. la gestione dei conflitti tra le programmazioni o la presenza di piu' sintonizzatori) dobbiamo chiaramente rivolgerci a strumenti piu' adeguati come [MythTV](http://www.mythtv.org/) o [vdr](http://www.tvdr.de/).

La TV e' il primo passo verso la convergenza dei media che oggi e' una realta' con i mediacenter. Possiamo quindi gestire TV, MUSICA, VIDEO e FOTO in modo semplice piacevole e integrato con i mille vantaggi che questa integrazione comporta. Il MediaCenter di cui parliamo in questo wiki e' xbmc. Un blog ricco completo di suggerimenti preziosi su questo tema e' il sito di telperion [http://telperion.wordpress.com/](http://telperion.wordpress.com/) che andrebbe visitato.

## Un mediacenter accattivante

Nel pc si realizza oggi e nelle nostre case la convergenza dei media che ha enormi vantaggi e pressoche nessun svantaggio. Il sw mediacenter gioca un ruolo fondamentale nel rendere accessibile a tutti questa vera e propia rivoluzione. Un MC deve essere infatti semplice, bello e facile da usare e configurare. Ci sono molti sw mc per Linux. Il primo e forse il piu' importante o comunque un riferimento ineludibile del settore e' [Mythtv](http://www.mythtv.org/). [Freevo](http://freevo.sourceforge.net/) e' un MC minimalista da tenere sotto osservazione. [Moovida](http://www.moovida.com/) e' un altro mc interessante. Per questo wiki vedremo nel dettaglio [xbmc](http://xbmc.org/)

```
pacman -S xbmc

```

Tramite questo comando installiamo subito le varie dipendenze necessarie come ad esempio mesa-demos che contiene glxinfo che serve all'avvio di xbmc. In alcuni casi, se abbiamo problemi verifichiamo la presenza di xorg-utils come [segnalato in questo thread](http://www.archlinux.it/forum/viewtopic.php?id=10265), che contiene xdpyinfo usato da xbmc per verificare la profondità di colore sempre all'avvio.

Xbmc si presenta subito bene con la sua accattivante grafica in trasparenze, sfumature dissolvenze.. ma sono necessari due o tre passaggi per rendere il tutto ancora meglio: le prime configurazioni

### Prime configurazioni

*   Selezionare la lingua italiana: Sistema - Aspetto - Internazionale
*   Scegliere la città più vicina per le previsioni: Sistema -Meteo
*   Usare un buon scraper che tiri giù poster e fanart dei nostri film: Sistema - Add-ons - Scarica add-ons - XBMC.org Add-ons - Scraper Film - IMDb
*   Per rendere predefinito lo scarper appena scelto: Sistema - Video - Scraper - Scraper predefinito per i film
*   Indicare dove prendere la musica: Muscia - Aggiungi sorgente
*   Indicare dove prendere i video e scaricare i poster e fanart da web: Video - Aggiungi sorgente (percorso) - Questa directory contiene (Film) - Avvia la scansione automatica - Impostazioni - Generale - Preferred Title Language from (Italy)
*   ...

Se non si definisce il contenuto al momento della creazione della sorgente può essere sempre fatto in un secondo momento con il tasto destro del mouse e poi 'Imposta il contenuto'.

### Organizzare i media

Molto importante e' l'organizzazione dei media. Possiamo ad esempio dividere i video in 3 sorgenti che corrispondono a 3 cartelle del filesystem:

*   ANIMAZIONE: cartella con i film di animazione in files .avi
*   FILM: cartella con i film normali in files.avi
*   SERIE: cartella contenente le sottocartelle: una per serie tv (es. Batman, Mr Bean, Pimpa. Hazard, cavalieri dello zodiaco...)

Per le foto un criterio potrebbe essere la divisione in anni e poi in mesi. Per la musica: una cartella per autore e le sottocartelle per gli album che conterranno i file con i singoli brani. In ogni caso, qualsiasi criterio venga scelto e' bene utilizzarne uno e tenere i 'media' ordinati e archiviati in modo coerente. Per consentire la consultazione a tutti, anche a chi non sa' leggere (i piu' piccoli ad esempio) e renderla comunque più piacevole per tutti, possiamo cliccare con il tasto destro sui sorgenti video poi su 'seleziona icona' e selezionare una icona che appare sulla destra al posto di quelle anonime (e poco significative) di xbmc. Per consentire allo scraper di scaricare poster e copertine corretti sono molto importanti i nomi da assegnare ai film, agli album musicali ecc... Possiamo seguire ad esempio questo criterio:

1.  Il titolo del film in italiano.avi
2.  Il titolo del film in italiano (2010).avi
3.  The original title (2010)

Se con il titolo italiano lo scraper non riesce a trovare e quindi scaricare la corrispettiva fanart mettiamo anche l'anno di uscita del film tra parentesi e se ancora non basta il titolo in lingua originale con la data tra parentesi. Dopo aver spento con il tasto 's' o tasto 'fine' dalla home e riavviato, lo scraper iniziera' a scaricare. Se i file sono orinati e ben titolati rimarremo sorpresi della accuratezza dello scraper. In ogni caso possiamo poi intervenire sul singolo film (o album o ...) con il tasto destro sul film - informazioni film (o tasto 'i')- Ricarica. Questi aspetti sembrano dei dettagli ma in realta' le fanart riescono a rendere fruibile in modo piacevole dei media che la digitalizzazione, in mezzo agli innumerevoli e indiscutibili vantaggi, ha purtroppo smaterializzato e reso piu' astratti e quindi meno godibili.

Le viste del tema 'Confluence' (la skin predefinita di xbmc nella versione attuale) sono tutte molto ben curate, per sceglierle basta usare il tasto freccia su oppure sinistro a seconda della vista attuale mentre si naviga nella sorgente. Possiamo usare viste diverse a seconda del tipo di sorgenti:

*   Video: possiamo disattivare la modalità archivio e segliere tra POSTER e FANART ma anche LISTA. Per le serie possiamo mettere ICONE LARGHE.
*   Musica: mettiamo modo archivio - Vista: lista

Le viste dipendono molto dalla skin. Selezioniamo skin alternative che verranno automaticamente scaricate ed installate. Proviamole e cambiamole di tanto in tanto per variare un pochino. Tutte le info, i poster, le fanart scaricate ecc.. sono nella home sotto .xbmc/userdata. Qui c'è anche il file per cambiare le rss news che scorrono in home page: Per mettere le rss dell'ultimora di adnkronos ad esempio [http://rss.adnkronos.com/RSS_Ultimora.xml](http://rss.adnkronos.com/RSS_Ultimora.xml) basta cambiare l'indirizzo per personalizzare:

```
$ cat .xbmc/userdata/RssFeeds.xml 
<?xml version="1.0" encoding="UTF-8" standalone="yes"?>
<rssfeeds>
  <set id="1">
    <feed updateinterval="30">[http://rss.adnkronos.com/RSS_Ultimora.xml](http://rss.adnkronos.com/RSS_Ultimora.xml)</feed>
  </set>
</rssfeeds>

```

Dall'ultima versione la fonte rss può essere cambiata direttamente da interfaccia grafica 'Sistema - Programmi - rss editor'

### La tv

Per avere integratala TV in xbmc c'è un ottimo backend facile da configurare e da gestire. Visitiamo e seguiamo le precise istruzione dell'ottimo [post sull'argomento](http://telperion.wordpress.com/2010/01/13/la-tv-su-xbmc-con-tvheadend/) che è fatto molto bene e spiega tutti passaggi. Vediamo solo qualche considerazione per la nostra arch: Per installarlo basta:

```
yaourt -S hts-tvheadend-svn

```

Per lanciarlo

```
sudo /etc/rc.d/tvheadend start

```

e per averlo in automatico all'avvio nella solita mitica lista dei demoni in /etc/rc.conf

```
DAEMONS=(syslog-ng network netfs crond lircd tvheadend)

```

Purtroppo il sintonizzatore rimane sempre occupato, anche quando non vediamo la tv o registriamo qualcosa. Per registrare tvheadend usa solo epg o xmltv che in Italia non e' molto affidabile ma per questo problema possiamo usare il pvr kiss sopra descritto.

In alternativa a tvheadend possiamo usare la tv minimalista descritta sopra che è molto semplice anche se non è integrata. Bisogna configurare bene i tasti del telecomando in modo che sia facilmente e direttamente accessibile, propio come la 'vecchia tv normale' ed e' propio quello che vedremo subito.

## Usare qualsiasi telecomando...

Oggi un TV senza telecomando non è una tv. Il telecomando è fondamentale in un MC, rende il MediaCenter veramente completo e degno di tale nome. Vediamo come si configura con Linux e come fare ad utilizzare un **qualsiasi telecomando universale per fare quasi tutto**. Gli esempi sono fatti con il ricevitore e telecomando inclusi nel sintonizzatore tv Hauppauge WinTV MiniStick HD ma i metodi esposti potranno essere utili per la configurazione di tutti telecomandi con lirc in generale. Questa sezione potrebbe essere considerata una integrazione al [wiki di lirc](https://wiki.archlinux.org/index.php/Lirc).

### Riconoscimento del ricevitore IR

Prima di comprare l'hw per Linux è importante verificarne il supporto e la compatibilità. Dopo aver trovato [una recensione su LinuxMagazine](http://www.linux-magazine.it/La-TV-a-passeggio-pag_3.htm) con [il telecomando sul sito lirc](http://lirc.sourceforge.net/remotes/hauppauge/DSR-0112.jpg) e addirittura [il file di configurazione](http://lirc.sourceforge.net/remotes/hauppauge/DSR-0112) si potrebbe pensare di essere ragionevolmente sicuri del supporto Linux della [Hauppauge WinTV MiniStick HD](http://www.eprice.it/PC-TV-e-Radio-HAUPPAUGE/s-2024435).

Accertiamoci che il dispositivo si visto dal kernel

```
$lsusb
Bus 002 Device 002: ID 2040:c000 Hauppauge Windham

```

Dall'output sopra vediamo che il kernel riconosce il sintonizzatore. Si potrebbe pensare che basti configurare lirc ma una cosa è il sintonizzatore, un'altra è il ricevitore IR. Con la versione 2.26.35 il kernel non sapeva che in quel dispositivo c'era, oltre al sintonizzatore, anche un ricevitore IR.

```
$cat /proc/bus/input/devices

```

Il comando non restituisce nessun output. Con [questa patch](https://patchwork.kernel.org/patch/116347/) che possiamo applicare al kernel con le istruzioni [di questo wiki](https://wiki.archlinux.org/index.php/Kernel_Compilation) e di [questo post](http://www.archlinux.it/forum/viewtopic.php?pid=85583#p85583). Applicando la patch vediamo il ricevitore IR:

```
$cat /proc/bus/input/devices
I: Bus=0000 Vendor=0000 Product=0000 Version=0000
N: Name="SMS IR w/kbd type 0"
P: Phys=SMS IR w/kbd type 0
S: Sysfs=/devices/pci0000:00/0000:00:1d.7/usb2/2-3/input/input9
U: Uniq=
H: Handlers=event9
B: EV=3
B: KEY=1 0 0 0 0

```

ma niente di più. Una prova per capire se arrivano segnali ce la può dare evtest. Dal comando sopra vediamo che il ricevitore viene visto con il numero 9 che mettiamo nel comando per evtest:

```
$yaourt -S evtest
$sudo evtest /dev/input/event9
Supported events:
 Event type 0 (Sync)
 Event type 1 (Key)
 Event code 256 (Btn0)
Testing ... (interrupt to exit)

```

niente output. Possiamo applicare [questa patch di Richard Zidlicky](https://patchwork.kernel.org/patch/106247/) (il vero autore di questa sezione del wiki a parte gli errori) che, sebbene considerata 'superata', funziona!

```
$cat /proc/bus/input/devices
I: Bus=0000 Vendor=0000 Product=0000 Version=0000
N: Name="SMS IR w/kbd type 1"
P: Phys=SMS IR w/kbd type 1
S: Sysfs=/devices/pci0000:00/0000:00:1d.7/usb2/2-1/input/input9
U: Uniq=
H: Handlers=kbd event8
B: EV=3
B: KEY=100fc312 214a80200000000 0 18000 41a800004801 9e168000000000 10000ffc

```

```
$sudo evtest /dev/input/event9
Input driver version is 1.0.0
Input device ID: bus 0x0 vendor 0x0 product 0x0 version 0x0
Input device name: "SMS IR w/kbd type 1"
Supported events:
 Event type 0 (Sync)
 Event type 1 (Key)
 Event code 2 (1)
 Event code 3 (2)
 Event code 4 (3) 
(...)

  Event code 403 (ChannelDown)
  Event code 412 (Previous)
Testing ... (interrupt to exit)
Event: time 1289424399.849151, type 1 (Key), code 108 (Down), value 1
Event: time 1289424399.849161, type 1 (Key), code 108 (Down), value 0
Event: time 1289424399.849164, -------------- Report Sync ------------
^[[BEvent: time 1289424400.493828, type 1 (Key), code 106 (Right), value 1
Event: time 1289424400.493841, type 1 (Key), code 106 (Right), value 0
Event: time 1289424400.493846, -------------- Report Sync ------------
^[[CEvent: time 1289424405.057377, type 1 (Key), code 67 (F9), value 1
Event: time 1289424405.057387, type 1 (Key), code 67 (F9), value 0
Event: time 1289424405.057390, -------------- Report Sync ------------
^[[20~Event: time 1289424406.991615, type 1 (Key), code 119 (Pause), value 1
Event: time 1289424406.991624, type 1 (Key), code 119 (Pause), value 0
Event: time 1289424406.991626, -------------- Report Sync ------------
Event: time 1289424407.785255, type 1 (Key), code 4 (3), value 1
Event: time 1289424407.785264, type 1 (Key), code 4 (3), value 0
Event: time 1289424407.785266, -------------- Report Sync ------------
3Event: time 1289424408.430413, type 1 (Key), code 3 (2), value 1
Event: time 1289424408.430423, type 1 (Key), code 3 (2), value 0
Event: time 1289424408.430425, -------------- Report Sync ------------ 

```

Il telecomando viene visto come una tastiera: se apriamo un terminale, un editor... premendo il bottone '1' appare '1' con 'ok' va a capo, con i tasti freccia.... Inoltre cambiando i tasti nella patch (es. KEY_EXIT con KEY_ESC ) applicando la patch e ricompilando ottieniamo il risultato. In questo modo dobbiamo tuttavia armonizzare le scorciatoie da tastiera delle varie applicazioni tra loro, tenere conto di quelle del DE, evitare i conflitti e comunque arrivare ad un compromesso. Servirebbe un livello di astrazione che intermedi come lirc.

### Configurare lirc

See [LIRC](/index.php/LIRC "LIRC").

#### Il driver /dev/lirc0

Nel caso di LIRC0 il file di configurazione appare cosi'

```
$ cat /etc/conf.d/lircd.conf 
#
# Parameters for lirc daemon
#
LIRC_DEVICE="/dev/lirc0"
LIRC_DRIVER="default"
LIRC_EXTRAOPTS=""
LIRC_CONFIGFILE="/etc/lircd.conf"

```

In questo caso e' utile e prezioso [il file di configurazione scaricato dal sito lirc](http://lirc.sourceforge.net/remotes/hauppauge/DSR-0112) che dobbiamo mettere in /etc/lircd.conf Se non abbiamo trovato in internet il file di configurazione, o abbiamo acquistato un telecomando universale qualsiasi, possiamo produrre il file tramite irrecord:

```
sudo irrecord -d /dev/lirc0 /etc/lircd.conf

```

Seguiamo la procedura e alla fine verifichiamo il risultato

```
nano /etc/lircd.conf

```

Vediamo la corrispondenza valori tasti: con il driver /dev/lirc0 lircd prende un input di basso livello dal ricevitore, guarda nel lircd.conf

```
bits           13
flags RC5|CONST_LENGTH

```

decodifica l'input in accordo con il protocollo RC5 del telecomando che produce qualcosa come il codice 0x1741, guarda oltre sempre in /etc/lircd.conf e assegna l'evento KEY_1 a quel numero. Rispetto all'altro metodo si risparmia un livello di decodifica, in pratica tuttavia non c'e' gran differenza perche' la corrispondenza in lircd.conf.devinput e' molto diretta. Riavviamo e assicuriamoci che ci sia il demone e il dispositivo:

```
$ ls /dev/lirc*
/dev/lirc0  /dev/lircd

```

Vediamo adesso l'altro metodo: /dev/input

#### Il driver /dev/input

Nel caso del driver INPUT il file /etc/cond.d/lircd.conf appare cosi'

```
$ cat /etc/conf.d/lircd.conf 
#
# Parameters for lirc daemon
#
LIRC_DEVICE="/dev/input/by-path/pci-0000:00:1d.7-event-ir"
LIRC_DRIVER="devinput"
LIRC_EXTRAOPTS=""
LIRC_CONFIGFILE="/etc/lircd.conf" 

```

dove come argomento di LIRC_DEVICE bisogna mettere il device trovato con il comando che abbiamo visto sopra

```
cat /proc/bus/input/devices

```

e quindi nel mio caso

```
LIRC_DEVICE="/dev/input/event9"

```

Per evitare il rischio che con lo spostamento o l'aggiunta di altri dispositivi il numero vari e quindi il telecomando non funzioni, bisogna prendere questo valore scegliendolo tra quelli definiti con il percorso per evitare che vari:

```
ls /dev/input/by-path/*

```

In caso ci siano delle incertezze su quale scegliere possiamo intanto scegliere quello con il numero e quando tutto funzione ricordarci di sostituirlo con il nome. In quel momento, quando funziona tutto, diventa piu' semplice con un paio di prove trovare quello giusto.

Manca l'abbinamento con il tasto: la keytable che mappa valori a tasti. La corrispondenza non viene interamente fatta nel file /etc/lircd.conf che deve essere invece preso da qui

```
sudo cp /usr/share/lirc/remotes/devinput/lircd.conf.devinput /etc/lircd.conf

```

Con il sistema /dev/input la corrispondenza valori tasti viene fatta in 2 livelli. La decodifica RC5 e' fatta nel driver del kernel, e rende ad es 0x1d01 mappato come KEY_1 in input device. Lircd prende KEY_1 guarda in /etc/lircd.conf il valore KEY_1 and returns KEY_1 (ma potrebbe essere configurato per es. in "Channel1" o altro) La corrispondenza della keytable nel kernel può essere caricata in due modi:

*   [Applicando una patch al kernel](http://www.archlinux.it/forum/viewtopic.php?id=10487). Nel caso della Hauppauge WinTV MiniStick HD usiamo [questa patch](http://pastebin.com/GWyVbGUw) per la versione 2.6.36 del kernel (sarà presto inserita ufficialmente nel kernel).
*   Tramite **ir-keycode** contenuto nel pacchetto v4l-utils

```
$sudo pacman -S v4l-utils
$ ir-keytable
Found /sys/class/rc/rc0/ (/dev/input/event9) with:
    Driver smsmdtv, table rc-rc5-hauppauge-new
    Supported protocols: NEC RC-5 RC-6 JVC SONY LIRC     Enabled protocols: NEC RC-5 RC-6 JVC SONY LIRC

```

ha trovato il ricevitore e ci dice che usa la table rc-rc5-hauppauge-new che però non contiene i valori del telecomando altrimenti sarebbero apparsi su evtest sopra. Ce ne accertiamo leggendo (-r) la tabella con il seguente comando:

```
sudo ir-keytable -r

```

Nel kernel attuale e' gia' presente una tabella di associazione tra codici e nomi tasti:

```
scancode 0x1e21 = KEY_CHANNELDOWN (0x193)
scancode 0x1e22 = KEY_CHANNEL (0x16b)
scancode 0x1e24 = KEY_PREVIOUSSONG (0xa5)
scancode 0x1e25 = KEY_ENTER (0x1c)
scancode 0x1e26 = KEY_SLEEP (0x8e)
scancode 0x1e29 = KEY_BLUE (0x191)
scancode 0x1e2e = KEY_GREEN (0x18f)
scancode 0x1e30 = KEY_PAUSE (0x77)
scancode 0x1e32 = KEY_REWIND (0xa8)
scancode 0x1e34 = KEY_FASTFORWARD (0xd0)
scancode 0x1e35 = KEY_PLAY (0xcf)
scancode 0x1e36 = KEY_STOP (0x80)
scancode 0x1e37 = KEY_RECORD (0xa7)
scancode 0x1e38 = KEY_YELLOW (0x190)
scancode 0x1e3b = KEY_SELECT (0x161)
scancode 0x1e3c = KEY_ZOOM (0x174)
scancode 0x1e3d = KEY_POWER (0x74)
Enabled protocols: NEC RC-5 RC-6 JVC SONY LIRC

```

Ma anche nel caso il comando sopra non restituisca niente non ci sono problemi, basta creare un file di testo in cui creare l'associazione tra i codici presi dall'output di evtest e la lista dei possibili nomi che possiamo associare presa tramite questo comando:

```
 irrecord --list-namespace

```

Nel mio caso vediamo che i valori (0x1e35 0x1e36 ...) abbinati ai tasti (KEY_PLAY KEY_STOP ...) non sono quelli del nostro telecomando universale visti con evtest sopra (1d30 1d36 ...). A parte lo 0x vediamo che quelli nella tabella sono tutti del tipo 1exx mentre quelli del telcomando sono 1dxx Salviamo la tabella attuale in un file:

```
sudo ir-keytable -r > tabella_originale

```

Modifichiamolo aggiungendo i valori presi da evtest e abbiniamoli ai tasti corrispondenti. I valori tra parentesi possono essere omessi e otteniamo qualcosa del tipo:

```
scancode 0x1d11 = KEY_VOLUMEDOWN
scancode 0x1d12 = KEY_PREVIOUS
scancode 0x1d14 = KEY_UP
scancode 0x1d15 = KEY_DOWN
scancode 0x1d16 = KEY_LEFT
scancode 0x1d17 = KEY_RIGHT
scancode 0x1d1c = KEY_TV
scancode 0x1d1e = KEY_NEXT
scancode 0x1d1f = KEY_EXIT 

```

Dove, lo ripeto, il codice dopo 0x e' quello che si ricava da evtest premendo i pulsanti, e quello dopo l'uguale e' il nome che desideriamo dare a quel tasto, non totalmente a piacere ma preso dalla lista con il comando irrecord --list-namespace Per il telecomando della hauppauge il [risultato è qui](http://pastebin.com/t0HfXaxd). Andiamo a scrivere (-w) la tabella modificata:

```
ir-keytable --write=/percorso/tabella/modificata

```

Dove il /percorso/tabella/modificata e' il posto e il nome che abbiamo scelto di dare al file di testo creato sopra con l'associazione codice/nome proviamo subito il risultato con evtest:

```
$ sudo evtest /dev/input/event9
(...)
Event: time 1291327675.258200, type 4 (Misc), code 4 (ScanCode), value 1d3d
Event: time 1291327675.258219, type 1 (Key), code 116 (Power), value 1
Event: time 1291327675.258222, -------------- Report Sync ------------
Event: time 1291327675.258267, type 4 (Misc), code 4 (ScanCode), value 1d3d
Event: time 1291327675.506847, type 1 (Key), code 116 (Power), value 0
Event: time 1291327675.506852, -------------- Report Sync ------------
Event: time 1291327677.738160, type 4 (Misc), code 4 (ScanCode), value 1d3b
Event: time 1291327677.738175, type 1 (Key), code 354 (Goto), value 1
Event: time 1291327677.738179, -------------- Report Sync ------------
Event: time 1291327677.987007, type 1 (Key), code 354 (Goto), value 0
Event: time 1291327677.987017, -------------- Report Sync ------------
Event: time 1291327678.779761, type 4 (Misc), code 4 (ScanCode), value 1d1c
Event: time 1291327678.779778, type 1 (Key), code 377 (TV), value 1
Event: time 1291327678.779781, -------------- Report Sync ------------
Event: time 1291327679.027004, type 1 (Key), code 377 (TV), value 0
Event: time 1291327679.027014, -------------- Report Sync ------------
Event: time 1291327683.789267, type 4 (Misc), code 4 (ScanCode), value 1d24
Event: time 1291327683.789281, type 1 (Key), code 405 (Last), value 1
Event: time 1291327683.789285, -------------- Report Sync ------------
Event: time 1291327683.789324, type 4 (Misc), code 4 (ScanCode), value 1d24
Event: time 1291327684.037014, type 1 (Key), code 405 (Last), value 0
Event: time 1291327684.037024, -------------- Report Sync ------------
Event: time 1291327684.930302, type 4 (Misc), code 4 (ScanCode), value 1d1e
Event: time 1291327684.930317, type 1 (Key), code 407 (Next), value 1
Event: time 1291327684.930320, -------------- Report Sync ------------
Event: time 1291327685.180341, type 1 (Key), code 407 (Next), value 0
Event: time 1291327685.180352, -------------- Report Sync ------------

```

Abbiamo ora l'abbinamento codice '1d3d' con il nome 'Power'. La cosa importante è che questo può essere fatto con qualsiasi telecomando. Io ne ho configurato uno universale. Ricordiamoci di mettere il keytable modificato in una posizione sicura e di aggiungere il comando

```
ir-keytable --write=/percorso/tabella/modificata

```

in /etc/rc.local per fare in modo che ad ogni avvio il kernel possa modificare automaticamente la keytable.

### IRW ed eccezione in HAL

In entrambi i casi (/dev/lirc0 oppure /dev/input) questo dovrebbe essere l'output in irw (con il demone lircd in ascolto):

```
$ irw
0000000080010067 00 KEY_UP devinput
000000008001006c 00 KEY_DOWN devinput
0000000080010160 00 KEY_OK devinput
0000000080010080 00 KEY_STOP devinput
0000000080010077 00 KEY_PAUSE devinput
00000000800100cf 00 KEY_PLAY devinput
0000000080010002 00 KEY_1 devinput
00000000800100a8 00 KEY_REWIND devinput
00000000800100d0 00 KEY_FASTFORWARD devinput
0000000080010192 00 KEY_CHANNELUP devinput

```

Se ci accorgiamo aprendo un terminale e premendo i tasti numerici che questi compaiono o che i tasti del volume e del mute vengono subito interpretati da x che alza, abbassa e muta, dobbiamo fermare hal [come indicato in questo avviso](http://lirc.org/html/devinput.html). Prima qualche info. Troviamo il dispositivo preso da hal:

```
$lshal
(...)
udi = '/org/freedesktop/Hal/devices/usb_device_2040_c000_4033519634_logicaldev_input'
  info.addons.singleton = {'hald-addon-input'} (string list)
  info.capabilities = {'input', 'input.keyboard', 'input.keys', 'button'} (string list)
  info.category = 'input'  (string)
  info.parent = '/org/freedesktop/Hal/devices/usb_device_2040_c000_4033519634'  (string)
  info.product = 'SMS IR (Hauppauge WinTV MiniStick)'  (string)
  info.subsystem = 'input'  (string)
  info.udi = '/org/freedesktop/Hal/devices/usb_device_2040_c000_4033519634_logicaldev_input'       (string)
  input.device = '/dev/input/event9'  (string)
  input.originating_device = '/org/freedesktop/Hal/devices/usb_device_2040_c000_4033519634'  (string)
  input.product = 'SMS IR (Hauppauge WinTV MiniStick)'  (string)
  input.x11_driver = 'evdev'  (string)
  input.xkb.layout = 'it'  (string)
  input.xkb.model = 'evdev'  (string)
  input.xkb.rules = 'base'  (string)
  input.xkb.variant = *  (string)*
  linux.device_file = '/dev/input/event9'  (string)
  linux.hotplug_type = 2  (0x2)  (int)
  linux.subsystem = 'input'  (string)
  linux.sysfs_path = '/sys/devices/pci0000:00/0000:00:1d.7/usb2/2-1/rc/rc0/input9/event9'  (string)

```

bisogna mettere una regola ad hal in modo che cerchi nel campo info.product la stringa 'SMS IR' e blocchi il controllo di quel dispositivo

```
sudo nano /usr/share/hal/fdi/preprobe/20thirdparty/lirc.fdi

```

con queste queste righe

```
<?xml version="1.0" encoding="UTF-8"?>
<deviceinfo version="0.2">
<device>
 <match key="info.product" contains_ncase="SMS IR">
    <merge key="info.ignore" type="bool">true</merge>
 </match>
</device>
</deviceinfo>

```

### I telecomandi universali

Possiamo acquistare un telecomando universale e configurarlo con lirc tramite il driver /dev/input in modo da avere comodamente due o piu' telecomandi con lo stesso ricevitore. Con evtest catturiamo i codici e costruiamo la tabella che viene caricata con ir-keycode ad ogni avvio. Se assegnamo lo stesso nome ai bottoni faremo in modo che i telecomandi facciano le stesse cose. I telecomandi universali per adattarsi ai vari dispositivi sono configurati per essere settati su diversi gruppi divisi per marca. Si tratta di una lista di decine e decine di insiemi possibili. Ad esempio [questo è il modello H-1080E marca CHUNGHOP](http://image.made-in-china.com/2f0j00yehQnCoZpiqw/Universal-HDTV-Remote-Control-H-1080E.jpg): delle varie combinazioni moltissime NON fanno funzionare tutti i tasti, ce ne possiamo accorgere facilmente perchè quando un tasto non funziona il led rosso è fisso acceso mentre quando invia il codice lampeggia. La Philips 245 e' una combinazione che li fa' funzionare tutti ma verificando l'output su irw ci accorgiamo che i valori del tasto menu e freccia sono identici: l'usabilità del telecomando viene irrimediabilmente compromessa. La combinazione Hitachi 382 consente di far funzionare quasi tutti i tasti in modo univoco e saprattutto non esclude i più importanti: [questa la ir-keytable](http://pastebin.com/Eh4bmgkm). Con [il telecomando della hauppauge](http://lirc.sourceforge.net/remotes/hauppauge/DSR-0112.jpg) condivide 35 tasti e in questo universale ne abbiamo qualcuno in più. La situazione migliore e' quella di avere pochi tasti ben configurati. Possiamo usare qualsiasi telecomando ma teniamo molto d'occhio l'usabilità e se vogliamo qualcosa di pronto subito il telecomando di Windows MediaCenter è largamente supportato da Linux, facile da capire e ben fatto.

Ora viene la parte finale: la configurazione del comportamento delle singole applicazioni che interagiscono con lirc.

## ... per fare qualsiasi cosa

Abbiamo visto come fare a configurare **qualsiasi telecomando**... ora vedremo come **fare qualsiasi cosa** con questo telecomando. Nell'ottica del mediacenter come unica fonte di intrattenimento in casa da fare usare a tutti si tratta di una questione molto importante.

### Configuriamo xine

Ci eravamo lasciati con l'output di irw

```
$ irw
0000000080010067 00 KEY_UP devinput
000000008001006c 00 KEY_DOWN devinput

```

Se non ottieniamo questo output torniamo indietro alla configurazione di lirc, se invece fila tutto liscio possiamo configurare le applicazioni in modo da definire il comportamento di ogni singolo tasto in ogni applicazione. Vediamo adesso xine e xbmc. Per la TV minimalista con xine vista precedentemente iniziamo a creare lircrc nella nostra home con questo comando

```
xine --keymap=lirc>.lircrc

```

che ci fornisce una lista di possibili azioni da far compiere alla pressine di un tasto del telecomando con xine. Basta sostituire 'remote = xxxxx' con 'remote = devinput' (o il nome che compare in irw) e definire il comportamento dei tasti sostituendo 'button = xxxxx' con 'button = KEY_VOLUMEUP' alla funzione che vogliamo assegnare. Per esempio la funzione per alzare il volume da cosi

```
# increment audio volume
begin
    remote = xxxxx
    button = xxxxx
    prog   = xine
    repeat = 0
    config = Volume+
end

```

nel nostro caso diventa cosi

```
# increment audio volume
begin
    remote = devinput
    button = KEY_VOLUMEUP
    prog   = xine
    repeat = 0
    config = Volume+
end

```

Possiamo togliere molte funzioni in quanto utilizzando xine per la tv abbiamo bisogno solo di pochi tasti.

### Configuriamo xbmc

Il controllo remoto di Xbmc, contrariamente alle convenzioni usate da quasi tutte le applicazioni (come xine), non viene fatto in .lircrc ma dal file .xbmc/userdata/Lircmap.xml che va creato copiando da /usr/share/xbmc/system/Lircmap.xml uno dei telecomandi già preconfigurati e che quindi dovrebbero funzionare 'out of the box' con xbmc. Tra i telecomandi preconfigurati ce ne è uno che si chiama propio 'devinput' ma che deve essere ritoccato per funzionare nel nostro caso. Xbmc considera entrambi i files, quello locale e quello generale, e se i nomi dei telecomandi coincidono come nel nostro caso sovrascrive le impostazioni che trova su /usr/share/xbmc/system/Lircmap.xml con quelle locali in .xbmc/userdata/Lircmap.xml che hanno la precedenza. Rispetto a quelle generali facciamo solo pochi cambiamenti. Mettiamo un nome unico altrimenti con gli alternativi xbmc non si avvia:

```
$cat .xbmc/userdata/Lirmap.xml
<remote device="devinput">

```

Per chi non usa il driver /dev/input basta prendere il nome del telecomando preso da irw e cambiare il valore tra i tags (che sono le azioni triggerate) con i nomi dei bottoni sempre presi da irw. Nel nostro caso aggiungiamo alcuni bottoni che nell'originale era definiti con nomi diversi sempre assegnando le solite funzioni:

```
<select>KEY_OK</select>
<start>KEY_GOTO</start>
<skipplus>KEY_NEXT</skipplus>
<skipminus>KEY_LAST</skipminus>

```

'Disattiviamo' il pulsante KEY_TV che ci serve per lanciare xine assegnando ad una funzione che non c'è cambiando l'originale:

```
<mytv>KEY_TV</mytv>

```

con il modificato

```
<NOmytv>KEY_TV</NOmytv>

```

che assegna il pulsante KEY_TV ad una non esistente funzione 'NOmytv'. Infine aggiungiamo due pulsanti che prima non c'erano cercando le funzioni in /usr/share/xbmc/system/keymaps/remote.xml (oppure in /opt/xbmc/system/keymaps/remote.xml a seconda delle versioni).

```
<info>KEY_PREVIOUS</info>
<menu>KEY_MENU</menu>

```

Comunque non tutte servono e sarebbe meglio non appesantire troppo con molte funzioni privilegiando l'usabilità. Motivo per cui non ci addentreremo in [configurazioni spinte](http://forum.xbmc.org/showthread.php?t=45972). Un dettaglio cambiamolo: mentre vediamo un film se premiamo back (o exit) la funzione contestuale invece di tonare indietro nei menu manda un 'piccolo passo indietro' nel film, funzione già egregiamente coperta da molti altri pulsanti (Left, rewind e last). Cambiamo in questo modo:

```
$ cat .xbmc/userdata/keymaps/remote.xml 
<keymap>
<FullscreenVideo>
    <remote>
      <back>Stop</back>
    </remote>
  </FullscreenVideo>
</keymap>

```

viene così sovrascitta l'impostazione 'SmallStepBack' presente in /usr/share/xbmc/system/keymaps/remote.xml con 'Stop' in .xbmc/userdata/keymaps/remote.xml

Abbiamo visto xine e xbmc ma ogni applicazione compatibile con lirc ha le sue funzioni e il suo modo per assegnarle ai tasti, di solito tramite lircrc. Ci sono poi due strumenti importanti che ci mette a disposizione lirc: **irxevent** e **irexec**.

### irxevent per registrare 'on the fly' la tv digitale con xine

Nelle funzioni che abbiamo visto sopra di xine c'è quella di 'record' che tuttavia si limita a salvare una screenshot e non salva lo streaming. Per questo c'è il tasto F1 che possiamo associare a xine tramite [irxevent](http://www.lirc.org/html/irxevent.html) che è un programma da lanciare in background come utente in quanto prende come configurazione il file .lircrc della home e quando vien invocato si limita a passare l'evento definito alla applicazione definita. Se usiamo gnome lo possiamo far partire in automatico da Sistema - Preferenze - Applicazioni di avvio ma probabilmente anche su /etc/rclocal cambiando utente o forzando il percorso del file di configurazione. Nel nostro caso il pulsante su .lircrc viene definito cosi

```
begin
        remote = devinput
        prog = irxevent
        button = KEY_RECORD
        repeat = 0
        config = Key F1 xine
end

```

Premendo il tasto record sul telecomando irxevent passa all'applicazione xine l'evento di pressione del tasto F1 come se fossimo sulla tastiera e quindi xine registra lo streaming nella nostra home e quando lo ripremiamo stoppiamo la registrazione. Su xbmc non accade niente perchè xine non gira. Dovremmo assegnare un'altro tasto al record di xbmc ma anche questo si limita ad uno screenshot.

### irexec per avviare e spengere una applicazione con un singolo bottone

Se dobbiamo alzarci e usare il mouse per far partire xbmc o xine crolla tutto il progetto. Per fortuna ci viene in aiuto [irexec](http://www.lirc.org/html/irexec.html) che come irxevent è una applicazione in background (da mettere in avvio automatico) che si limita a lanciare altre applicazioni o scripts.

```
begin
        remote = devinput
        prog = irexec
        button = KEY_POWER
        repeat = o
        config = xbmc
end

```

In questo modo il pulsante power richiama irexec che lancia xbmc. In Lircmap.xml abbiamo definito power in questo modo

```
<power>KEY_POWER</power>

```

Quindi mentre ci gustiamo xbmc se premiamo il tasto power xbmc si spenge ma irexec lo riapre. Potremmo utilizzare due pulsanti diversi, uno per accendere e uno per spengere ma sarebbe brutto e poco usabile. In [questo thread](http://www.gossamer-threads.com/lists/mythtv/users/134389) troviamo una soluzione intelligente. Creaiamo un file (in questo caso lo ho chiamatop popo) con il seguente script:

```
$ nano /media/dati/popo 
#!/bin/sh 
pkill irexec; 
xbmc && irexec -d;
$cat .xbmc/userdata/Lircmap.xml
(...)
<power>KEY_POWER</power>
(...)

```

e poi modifichiamo lircrc in questo modo:

```
$nano .lircrc
begin
        remote = devinput
        prog = irexec
        button = KEY_POWER
        repeat = 0
        config = /media/dati/stele/popo
end
(...)

```

In pratica irexec lancia lo script 'popo' che uccide il processo irexec e lancia xbmc e solo quando questo si spenge (tramite il pulsante power definito in Lircmap.xml) riavvia irexec come demone pronto a rilanciare lo script appena premuto il power di nuovo. Basta solo generalizzare per sfruttare il solito script anche per xine

```
$ nano /media/dati/popo 
#!/bin/sh 
pkill irexec; 
if [ "$1" = "xbmc" ]
then
$1 && irexec -d;
else
$1 -f dvb:// && irexec -d;
fi

```

e dare in lircrc il nome dell'applicazione da lanciare come argomento dello script popo

```
$nano .lircrc
begin
        remote = devinput
        prog = irexec
        button = KEY_POWER
        repeat = 0
        config = /media/dati/stele/popo xbmc
end
begin
        remote = devinput
        prog = irexec
        button = KEY_TV
        repeat = 0
        config = /media/dati/stele/popo xine
end

```

[Qui](http://pastebin.com/kC04Jw1y) abbiamo i files .lircrc e Lircmap.xml completi. Con il tasto TV accendiamo e spengiamo la tv e con il tasto power xbmc. Abbiamo inoltre imparato due strumenti (irxevent e irexec) che potenzialmente ci consentono di configurare davvero di tutto!

## Il backup perfetto

Quando il pc di casa inizia ad essere utilizzato massicciamente e quasi esclusivamente come mediacenter o comunque per la gestione per i propi dati come le foto ecc... e' **fondamentale** provvedere ad un sistema di backup. Considero [questo articolo](http://www.dei.unipd.it/~sbologna/backupinlinux3.html) una raro esempio di chiarezza e competenza, precisione e accuratezza. Complimenti a Saverio Bolognani e al suo articolo: [http://www.dei.unipd.it/~sbologna/backupinlinux3.html](http://www.dei.unipd.it/~sbologna/backupinlinux3.html) 'Il backup perfetto'.

In estrema sintesi riporto i punti principali e i passaggi per la nostra amata arch. Il backup perfetto deve essere:

*   Completamente automatico
*   Prevedere la separazione fisica dei supporti
*   Consentire un recupero semplice dei file

Per ottenere questi risultati ci avvaleremo delle caratteristiche del filesystem e di due potenti programmi: rsync e rsnapshot come spiegato nei dettagli molto bene nell'articolo.

```
sudo pacman -S rsync rsnapshot

```

Aggiungiamo poi un pacchetto necessario per evitare un errore che invaliderebbe tutto: perl-lchown [preparato per noi dall'ottimo Giovanni](http://www.archlinux.it/forum/viewtopic.php?id=6933)

```
yaourt -S perl-lchown

```

Siamo pronti per personalizzare l'unico file di configurazione /etc/rsnapshot.conf partendo da dove vogliamo che vengano salvati i backup. Cito dall'articolo:

```
# Tutti gli snapshot vengono salvati in questa cartella.
snapshot_root /media/LACIE_ext3/
# Se no_create_root è settato a 1, rsnapshot non creerà
# automaticamente la cartella snapshot_root. Ciò è particolarmente
# utile per fare backup su supporti rimovibili, come hard disk USB o
# FireWire.
no_create_root 1

```

Poi definiamo, sempre nello stesso file piu' in basso gli intervalli in cui viene effettuato il backup ovvero la struttura dei backup nel tempo. Nel mio caso e diversamente dall'articolo preferisco conservare 7 immagini quotidiane e 4 settimanali

```
Backup intervals
# I nomi degli intervalli (weekly = settimanale, monthly = mensile, ...)
# sono solo nomi e non hanno nessun effetto sulla reale lunghezza
# dell'intervallo. I numeri impostano il numero di snapshot da
# conservare per ogni intervallo (weekly.0, weekly.1, ...).
# La lunghezza dell'intervallo viene impostato dall'intervallo temporale
# tra due esecuzioni di rsnapshot <nome intervallo>, generalmente
# tramite cron. Sentitevi liberi di adattare i nomi degli intervalli, e di
# conseguenza il file /etc/cron.d/rsnapshot secondo le vostre
# esigenze. L'unica vincolo è che gli intervalli devono essere elencati
# in ordine ascendente.
interval daily   7
interval weekly 4

```

Dobbiamo poi specificare di quali cartelle vogliamo fare il backup (nel mio caso la directory /media/dati che e' una intera partizione dedicata). Il secondo argomento di ogni riga specifica sotto quale cartella vanno salvate le copie sul supporto di backup. Attenzione alle barre (/) alla fine dei percorsi!

```
# LOCALHOST
backup /media/dati/ localhost/

```

A me interessa escludere la cartella new e i files/cartelle nascosti (che iniziano con il punto) in cui metto la roba scaricata da eMule e che non mi interessa backuppare. Quindi aggiungo le seguenti righe:

```
exclude .*
exclude new

```

Siamo arrivati al momento della pianificazione del backup. Diversamente all'articolo ho preferito modificare lo script e crearne [uno personalizzato](http://pastebin.com/drftQiiU) che ho chiamato backup_script che faccio lanciare con i privilegi di utente root dal mio crontab ad ogni ora

```
$crontab -e
# Tutti i giorni al 3 minuto di ogni ora verifica backup
3 * * * * sudo /percorso/al/backup_script

```

Lo script usa due file che che vanno creati la prima volta

```
touch /percorso/al/backup_timestamp_quotidiano /percorso/al/backup_timestamp_settimanale

```

Chiaramente i percorsi sono personali. In realta' sono files vuoti e servono esclusivamente per schedulare i backup. Lo script infatti ogni ora verifica quanto tempo e' passato dall'ultimo backup quotidiano e se sono passate oltre 24 ore lo effettua. Allo stesso modo se sono passati piu' di 7 giorni dall'ultimo backup settimanale lo effettua. In caso contrario si limita a scrivere nel file di log la data. Fatto. Tutto automatico. Con il fidato conky è comodo tenere d'occhio il file log per verificare che sia tutto ok ma senza fare niente siamo tranquilli che tutti inostri files sono sicuro, facilmente e immediatamente accessibili per ogni evenienza.