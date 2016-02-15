**Mutt** è un programma per la gestione della posta elettronica testuale rinomato per le sue straordinarie caratteristiche. Mutt è il client di posta preferito da un gran numero di utenti esperti. Sfortunatamente, un'installazione standard di Mutt è tormentata da complesse associazioni di tasti, e ha una quantità tale di documentazione da scoraggiare i nuovi utenti. Questa guida aiuterà l'utente medio a configurare ed eseguire Mutt, e iniziare a personalizzarlo secondo le proprie esigenze.

## Contents

*   [1 Generalità](#Generalit.C3.A0)
*   [2 Installazione](#Installazione)
*   [3 Configurazione](#Configurazione)
    *   [3.1 IMAP](#IMAP)
        *   [3.1.1 Utilizzo del supporto nativo IMAP](#Utilizzo_del_supporto_nativo_IMAP)
            *   [3.1.1.1 imap_user](#imap_user)
            *   [3.1.1.2 imap_pass](#imap_pass)
            *   [3.1.1.3 cartella](#cartella)
            *   [3.1.1.4 spoolfile](#spoolfile)
            *   [3.1.1.5 caselle postali](#caselle_postali)
            *   [3.1.1.6 Riepilogo](#Riepilogo)
        *   [3.1.2 Supporto esterno IMAP](#Supporto_esterno_IMAP)
    *   [3.2 POP3](#POP3)
        *   [3.2.1 Ricevere la posta](#Ricevere_la_posta)
            *   [3.2.1.1 Vari account e-mail con getmail](#Vari_account_e-mail_con_getmail)
        *   [3.2.2 Smistare la posta](#Smistare_la_posta)
    *   [3.3 Maildir](#Maildir)
    *   [3.4 SMTP](#SMTP)
        *   [3.4.1 Utilizzare il supporto nativo SMTP](#Utilizzare_il_supporto_nativo_SMTP)
        *   [3.4.2 Supporto esterno SMTP](#Supporto_esterno_SMTP)
*   [4 Personalizzazione](#Personalizzazione)
    *   [4.1 Stampa](#Stampa)
    *   [4.2 Blocco firma](#Blocco_firma)
        *   [4.2.1 Firma random](#Firma_random)
    *   [4.3 Visualizzazione URL e apertura di Firefox](#Visualizzazione_URL_e_apertura_di_Firefox)
    *   [4.4 Mutt e Vim](#Mutt_e_Vim)
    *   [4.5 Visualizzazione HTML all'interno delle impostazioni Vim/Mutt](#Visualizzazione_HTML_all.27interno_delle_impostazioni_Vim.2FMutt)
    *   [4.6 Mutt e GNU nano](#Mutt_e_GNU_nano)
    *   [4.7 Colori](#Colori)
*   [5 Suggerimenti](#Suggerimenti)
    *   [5.1 Utilizzo di Mutt per inviare mail da riga di comando](#Utilizzo_di_Mutt_per_inviare_mail_da_riga_di_comando)
    *   [5.2 Come visualizzare un'altra e-mail mentre si compone](#Come_visualizzare_un.27altra_e-mail_mentre_si_compone)
    *   [5.3 Mutt-Sidebar](#Mutt-Sidebar)
*   [6 Vedere anche](#Vedere_anche)

## Generalità

Mutt è un Mail User Agent (MUA), concepito in origine soltanto per leggere la posta. Per questo motivo, le funzioni di recupero, invio e filtraggio implementate successivamente sono gestibili da altre applicazioni. La maggior parte dei settaggi di Mutt riguarda programmi esterni che eseguano le azioni richieste.

In ogni caso, il pacchetto ufficiale [mutt](https://www.archlinux.org/packages/?name=mutt) è stato compilato con il supporto per IMAP, POP3 e SMTP e quindi non necessita di programmi esterni per trattare la posta elettronica.

Questo articolo tratterà sia l'utizzo nativo di IMAP per inviare/ricevere email, sia il settaggio basato su [OfflineIMAP](/index.php/OfflineIMAP "OfflineIMAP") o [getmail](/index.php/Getmail "Getmail") (POP3) per ricevere le mail, [procmail](/index.php/Procmail "Procmail") per filtrarle in caso di POP3, e [msmtp](/index.php/Msmtp "Msmtp") per inviarle.

## Installazione

[Installare](/index.php/Pacman_(Italiano) "Pacman (Italiano)") [mutt](https://www.archlinux.org/packages/?name=mutt) dai [repositories ufficiali](/index.php/Official_Repositories_(Italiano) "Official Repositories (Italiano)").

Opzionalmente è possibile installare applicazioni esterne, per il setup IMAP come [offlineimap](https://www.archlinux.org/packages/?name=offlineimap) e [msmtp](https://www.archlinux.org/packages/?name=msmtp).

O (se si usa POP3) [getmail](https://www.archlinux.org/packages/?name=getmail) o [fdm](https://www.archlinux.org/packages/?name=fdm) e [procmail](https://www.archlinux.org/packages/?name=procmail).

**Nota:** Se si ha bisogno dei soli metodi di autenticazione LOGIN e PLAIN, questi sono soddisfatti della dipendenza [libsasl](https://www.archlinux.org/packages/?name=libsasl).

**Nota:** Se si vuole (o deve) usare CRAM-MD5, GSSAPI o DIGEST-MD5, installare anche il pacchetto [cyrus-sasl-gssapi](https://www.archlinux.org/packages/?name=cyrus-sasl-gssapi).

**Nota:** Se si utilizza Gmail come server smtp, può essere necessario installare il pacchetto [cyrus-sasl](https://www.archlinux.org/packages/?name=cyrus-sasl).

## Configurazione

Questa sezione riguarda IMAP, [#POP3](#POP3), [#Maildir](#Maildir) e la configurazione [#SMTP](#SMTP).

Si noti che Mutt riconosce due posizioni per i propri file di configurazione: `~/.muttrc` e `~/.mutt/muttrc`. Funziona in entrambi i casi.

### IMAP

_Impostazioni locali ed esterne_

#### Utilizzo del supporto nativo IMAP

La versione Mutt dei [repositories ufficiali](/index.php/Official_Repositories_(Italiano) "Official Repositories (Italiano)") è compilata con il supporto IMAP. È necessario disporre per lo meno di 4 righe nel file muttrc per poter accedere alla posta.

##### imap_user

```
set imap_user=USERNAME

```

Continuando con l'esempio precedente, ricordate che Gmail richiede l'indirizzo email completo (questo non è standard):

```
set imap_user=your.username@gmail.com

```

##### imap_pass

Se non impostato, la password verrà richiesta, in quanto è l'opzione predefinita.

```
set imap_pass=SECRET

```

##### cartella

Invece di una directory locale che contiene tutta la posta (e relative directory), utilizzare il server (e se necessario, la cartella più in alto nella gerarchia).

```
set folder=imap[s]://imap.server.domain[:port]/[folder/]

```

Non è necessario utilizzare una cartella, ma potrebbe essere conveniente se si dispone di tutte le altre cartelle all'interno di Posta in arrivo, per esempio. Qualunque cosa venga impostata qui come cartella, sarà accessibile in seguito con Mutt con tramite il solo un segno di uguale (=). Esempio:

```
set folder=imaps://imap.gmail.com/

```

##### spoolfile

È ora possibile utilizzare "=" or "+" come una sostituzione per l'intero percorso cartella che è stato configurato in precedenza. Per esempio:

```
set spoolfile=+INBOX

```

##### caselle postali

Tutte le cartelle imap che dovrebbero essere controllate regolarmente per la nuova posta devono essere elencate qui:

```
mailboxes =INBOX =family
mailboxes imaps://imap.gmail.com/INBOX imaps://imap.gmail.com/family

```

In alternativa, controllare tutte le cartelle IMAP sottoscritte (come se fossero state tutte aggiunte con una linea di `mailboxes`):

```
set imap_check_subscribed

```

Queste due versioni sono equivalenti, ma la prima è molto più conveniente. Inoltre, le versioni più recenti di Mutt sono configurate di default per includere una macro associata al tasto "y", che permetterà di modificare ognuna delle cartelle elencate nelle caselle postali.

##### Riepilogo

Utilizzando queste opzioni, sarete in grado di avviaare mutt, inserire la password IMAP, e iniziare a leggere la posta. Ecco un frammento muttrc (per Gmail) con l'aggiunta di alcune ulteriori righe per un migliore supporto IMAP.

```
set folder      = imaps://imap.gmail.com/
set imap_user   = your.username@gmail.com
set imap_pass   = your-imap-password
set spoolfile   = +INBOX
mailboxes       = +INBOX

# store message headers locally to speed things up
set header_cache = ~/.mutt/hcache

# specify where to save and/or look for postponed messages
set postponed = +[Gmail]/Drafts

# allow mutt to open new imap connection automatically
unset imap_passive

# keep imap connection alive by polling intermittently (time in seconds)
set imap_keepalive = 300

# how often to check for new mail (time in seconds)
set mail_check = 120
```

#### Supporto esterno IMAP

La funzionalità IMAP incorporata in Mutt, non scarica la posta in modalità offline. L'articolo [OfflineIMAP](/index.php/OfflineIMAP "OfflineIMAP") descrive come scaricare le email in una cartella locale per essere elaborate in seguito da Mutt.

Considerare l'utilizzo di applicazioni come [spamassassin](https://www.archlinux.org/packages/?name=spamassassin) o [imapfilter](https://aur.archlinux.org/packages/imapfilter/) per smistare la posta.

### POP3

_Recupero e smistamento della posta con applicazioni esterne_

#### Ricevere la posta

Create la directory `~/.getmail/`. Aprite il file `~/.getmail/getmailrc` con l'editor di testo preferito.

Ecco un esempio di `getmailrc` usato con un account gmail.

```
[retriever]
type = SimplePOP3SSLRetriever
server = pop.gmail.com
username = username@gmail.com
port = 995
password = password

[destination]
type = Maildir
path = ~/mail/
```

Potete reperire queste informazioni dalle specifiche del vostro fornitore del servizio POP3.

Molti utenti potranno ritenere utile aggiungere queste righe a `getmailrc` per prevenire il fatto che le mail vengano scaricate tutte ogni qualvolta che getmail viene eseguito.

```
[options]
read_all = False
```

Come si può vedere `~/.getmail/getmailrc` contiene informazioni sensibili (in particolare, le password degli account e-mail in formato testo). Sarebbe buona norma cambiare le autorizzazioni di accesso alla directory in modo che solo il proprietario possa vederle:

```
$ chmod 700 ~/.getmail

```

Per questa guida memorizzeremo la nostra posta nel formato `maildir`. I due principali formati di mailbox sono `mbox` and `maildir`. La principale differenza fra i due formati è che `mbox` è un file, con tutti i vostri messaggi di posta e le loro intestazioni memorizzati lì, mentre una `maildir` è una directory. Ogni messaggio di posta è un file.

Una `maildir` è una cartella con all'interno le cartelle `cur`, `new` e `tmp`.

```
   mkdir -p ~/mail/{cur,new,tmp}

```

Avviate getmail. Se funziona, potete creare un _cronjob_ (un comando mandato in esecuzione da `crontab`) per mandare in esecuzione getmail ogni tot ore/minuti. Date da terminale il comando `crontab -e` per editare _cronjob_, e scrivete:

```
 */10 * * * * /usr/bin/getmail

```

`getmail` verrà eseguito ogni 10 minuti.

Inoltre, per ridurre l'output di getmail, è possibile ridurne verbosità a zero aggiungendo quanto segue a: `getmailrc`:

```
[options]
verbose = 0
```

##### Vari account e-mail con getmail

Per impostazione predefinita, quando si esegue `getmail` il programma cerca i file creati da getmailrc come visto sopra. Se si dispone di più di un account di posta elettronica dai quali si desidera ricevere posta, allora si può creare un file per ogni indirizzo e-mail, e poi istruire getmail ad eseguirli entrambi. Ovviamente avendo due account e due file non si possono avere entrambi in sincronizzazione con getmailrc. Quello che si può fare è dare loro due nomi diversi, prendendo spunto da questo esempio: chiamiamo uno "personale" e uno "universitario". Questi due file contengono contenuti pertinenti alla posta personale, ed alla posta di lavoro universitario, rispettivamente. Per far funzionare getmail con questi due file, invece di cercare getmailrc (default), si può usare l'opzione **rcfile switch** in questo modo: `getmail --rcfile university --rcfile personal`, che può operare con più file se si dispone di più account di posta, basta assicurarsi che ogni file sia nella cartella getmail, e assicurarsi di modificare il crontab per eseguire il comando con le opzioni --rcfile. Esempio:

```
 ***/30 * * * * /usr/bin/getmail --rcfile university --rcfile personal**

```

Ovviamente è possibile chiamare i propri file come si preferisce, provvedendo ad includerli in cronjob o nei comandi da shell, e sistemandoli nella cartella .getmail/. Getmail scaricherà la posta da questi due accounts.

#### Smistare la posta

[Procmail](http://www.procmail.org/) è uno strumento di smistamento estremamente potente. Per lo scopo di questo wiki, imposteremo alcune regole di smistamento per cominciare.

Bisogna editare getmailrc per passare a procmail i messaggi di posta ricevuti:

```
[destination]
type = MDA_external
path = /usr/bin/procmail
```

Ora, aprite `.procmailrc` nel vostro editor di testo preferito. Le righe che seguono smisteranno la mailing list di happy-kangaroos , e tutta la posta del vostro amico del cuore nelle rispettive maildir.

```
MAILDIR=$HOME/mail
DEFAULT=$MAILDIR/inbox/
LOGFILE=$MAILDIR/log

:0:
* ^To: happy-kangaroos@nicehost.com
happy-kangaroos/

:0:
* ^From: loveydovey@iheartyou.net
lovey-dovey/
```

Dopo aver salvato il vostro `.procmailrc`, avviate getmail e vedete se procmail riesce a a smistare la posta nelle directory giuste.

**Nota:** Un modo per ottenere errori con .procmailrc sono i permessi. Procmail richiede i permessi 644 e produrrà notevoli messaggi d'errore senza.

### Maildir

Maildir è un formato generico e standardizzato. Quasi tutti i MUA sono in grado di gestire il supporto Maildir, e Mutt in questo è eccellente. Ci sono solo alcune semplici cose da fare per consentire a Mutt di usarlo. Aggiungere le seguenti righe a muttrc:

```
set mbox_type=Maildir
set folder=$HOME/Mail
set spoolfile=+/INBOX
set header_cache=~/.hcache
```

Si tratta di una configurazione minima che permette di accedere al proprio Maildir e controllare le nuove mail locali in INBOX. Questa configurazione memorizza anche le intestazioni delle email per accelerare l'elenco della directory. Potrebbe non essere abilitato nel proprio build (ma lo è sicuramente nel pacchetto Arch). Si noti che questo non influisce in alcun modo su OfflineIMAP, e sincronizza sempre tutte le directory su un server. `spoolfile` istruisce Mutt su quali directory locali eseguire il polling per le nuove mail. È possibile aggiungere ulteriori spoolfiles (ad esempio la directory di mailing-list) e magari anche altre cose, ma questo è consultabile sul manuale di Mutt e non è lo scopo di questo documento.

### SMTP

Indipendentemente che si utilizzi POP o IMAP per ricevere la posta, sarà probabilmente ancora possibile inviare una mail utilizzando il protocollo SMTP.

#### Utilizzare il supporto nativo SMTP

La versione Mutt di pacman è compilata con il supporto SMTP. Basta controllare il manuale online [muttrc](http://manual.cream.org/index.cgi/muttrc.5), o `man muttrc` per ulteriori informazioni.

Per esempio:

```
set my_pass='mysecretpass'
set my_user=myname@gmail.com

set smtp_url=smtps://$my_user:$my_pass@smtp.gmail.com
set ssl_force_tls = yes
```

#### Supporto esterno SMTP

È possibile utilizzare un SMTP esterno come [msmtp](/index.php/Msmtp "Msmtp") o [SSMTP](/index.php/SSMTP "SSMTP"). Questa sezione riguarda esclusivamente la configurazione di Mutt per msmtp.

Modificare file di configurazione di Mutt o crealo se non esistente:

 `muttrc` 

```
set realname='Disgruntled Kangaroo'

set sendmail="/usr/bin/msmtp"

set edit_headers=yes
set folder=~/mail
set mbox=+mbox
set spoolfile=+inbox
set record=+sent
set postponed=+drafts
set mbox_type=Maildir

mailboxes +inbox +lovey-dovey +happy-kangaroos
```

Ora avviare `mutt`:

```
$ mutt

```

Si dovrebbe vedere tutta la posta in `~/mail/inbox`. Premere `m` per comporre mail; verrà utilizzato l'editor definito dalla variabile d'ambiente `EDITOR`. Se questa variabile non è impostata, digitare:

```
$ export EDITOR=editorbin

```

A fini di test, indirizzare la lettera a se stessi. Dopo aver scritto la lettera, salvare e uscire dall'editor. Si torna a Mutt, che ora mostra le informazioni sull'e-mail. Premere `y` per inviarlo.

## Personalizzazione

Guide per iniziare con l'utilizzo e la personalizzazione di Mutt:

*   [My first mutt](http://mutt.blackfish.org.uk/) (gestito da Bruno Postle)
*   [The Woodnotes Guide to the Mutt Email Client](http://www.therandymon.com/woodnotes/mutt/using-mutt.html) (gestito da Randall Wood)

In caso di domande specifiche su Mutt, non esitare a chiedere nel [canale irc](/index.php/ArchChannel "ArchChannel").

### Stampa

È possibile installare [muttprint](https://aur.archlinux.org/packages/muttprint/) da [AUR](/index.php/AUR "AUR") per una migliore qualità di stampa. Nel file muttrc, inserire:

```
set print_command="/usr/bin/muttprint %s -p {PrinterName}"

```

### Blocco firma

Creare un .signature nella cartella home. La propria firma verrà aggiunta alla fine dell'e-mail.

#### Firma random

È possibile utilizzare fortune per aggiungere una firma casuale a mutt.

 `$ pacman -S fortune-mod` 

Creare un file fortune e quindi aggiungere la seguente riga al muttrc:

 `set signature="fortune pathtofortunefile|"` 

Si noti la pipe finale. Questa fa si che mutt interpreti tale stringa non come un file, ma come un comando.

### Visualizzazione URL e apertura di Firefox

Si dovrebbe iniziare creando una directory .mutt in $HOME se non è ancora stato fatto. Una volta lì, creare un file denominato macros. Inserire le seguenti:

```
 macro pager \cb <pipe-entry>'urlview'<enter> 'Follow links with urlview'

```

Ora installare [urlview](https://aur.archlinux.org/packages/urlview/) da [AUR](/index.php/AUR_(Italiano) "AUR (Italiano)").

Creare un .urlview in $HOME ed inserire il seguente:

```
REGEXP (((http|https|ftp|gopher)|mailto)[.:][^ >"\t]*|www\.[-a-z0-9.]+)[^ .,;\t>">\):]
COMMAND firefox %s 

```

Quando si legge un'email sul pager, premendo ctrl + b verranno elencati tutti gli URL dall'e-mail. Navigare su o in giù con i tasti freccia e premere Invio sull'URL desiderata. Firefox si avvierà sul sito selezionato.

*   Note - Se si hanno dei problemi con urlview a causa dell'encoding url di Mutt si può provare [extract_url.pl](http://www.memoryhole.net/~kyle/extract_url/)

*   Note - Per vedere una breve anteprima contestuale del contenuto di ogni URL, provare [urlscan](https://aur.archlinux.org/packages.php?ID=44853). La macro nel file muttrc è lo stesso che per urlview (tranne che per il comando "urlscan"). Non vi è alcuna configurazione aggiuntiva richiesta oltre le impostazioni del $BROWSER.

### Mutt e Vim

*   Per limitare la larghezza del testo a 72 caratteri, modificare il proprio file .[vimrc](/index.php/Vim_(Italiano) "Vim (Italiano)") e aggiungere:

```
au BufRead /tmp/mutt-* set tw=72

```

*   Un'altra possibilità è quella di utilizzare il plugin di Vim "mail filetype" per attivare altre opzioni per le email e la larghezza a 72 caratteri. Modificare `~/.vim/filetype.vim`, creandolo se inesistente, e aggiungere:

```

augroup filetypedetect
  " Mail
  autocmd BufRead,BufNewFile *mutt-*              setfiletype mail
augroup END

```

*   Per impostare una diversa directory tmp, per esempio ~/.tmp, aggiungere una riga a muttrc come segue:

```
set tmpdir="~/.tmp"

```

*   Per riformattare un testo modificato consultare la guida contestuale di Vim

```
:h 10.7

```

### Visualizzazione HTML all'interno delle impostazioni Vim/Mutt

È possibile passare la consistenza HTML ad un programma esterno e poi scaricarlo, mantenendo la visualizzazione della posta elettronica uniforme e non invadente. Due programmi sono descritti qui: lynx and w3m.

Installare lynx o w3m:

```
pacman -S lynx

```

o

```
pacman -S w3m

```

Se _~/.mutt/mailcap_ non esiste, sarà necessario crearlo e aggiungere le seguenti righe:

```
text/html; lynx -display_charset=utf-8 -dump %s; nametemplate=%s.html; copiousoutput

```

o, nel caso di w3m,

```
text/html; w3m -I %{charset} -T text/html; copiousoutput;

```

Modificare muttrc e aggiungere la seguente:

```
set mailcap_path 	= ~/.mutt/mailcap

```

Per aprire automaticamente i messaggi HTML in lynx, aggiungere questa riga aggiuntiva a muttrc:

```
auto_view text/html

```

La bellezza di questo è che invece di visualizzare il formato HTML come sorgente, o essere aperto da un programma separato, in questo caso lynx, viene analizzato da Vim come HTML, ed i collegamenti URL nella email possono essere visualizzati con CTRL + b.

Se si ricevono molte email in formato di codifica diversi, mutt le considererà di default come html. Per evitare questo, aggiungere la seguente variabile al proprio `~/.muttrc`, che imposta il default di mutt su "text", mentre se i contenuti sono html, viene usato w3m/lynx:

```
alternative_order text/plain text/html

```

### Mutt e GNU nano

[nano](/index.php/Nano "Nano") è un altro editor da console piacevole da usare con Mutt.

Per limitare la larghezza del testo di 72 caratteri, modificare il file .nanorce ed aggiungere:

```
 set fill 72

```

Inoltre, nel file muttrc è possibile specificare la riga dove modificare, in modo che si ignori l'intestazione mail:

```
 set editor="nano +7"

```

### Colori

Aggiungere definizioni di colore d'esempio al file .muttrc:

```
$ cat /usr/share/doc/mutt/samples/colors.linux >> ~/.muttrc

```

Quindi regolare a proprio piacimento.

I colori così impostati coincideranno con quelli nel file `~/.Xresources`

## Suggerimenti

### Utilizzo di Mutt per inviare mail da riga di comando

Le pagine man mostreranno tutti i comandi disponibili e come usarli, ma qui ci sono un paio di esempi. Si potrebbe utilizzare Mutt per inviare avvisi, log o altre informazioni di sistema, attivate dal login tramite .bash_profile, o come un normale cron job.

Inviare un messaggio:

```
mutt -s "Subject" somejoeorjane@someserver.com < /var/log/somelog

```

Invia un messaggio con allegato:

```
mutt -s "Subject" -a somefile somejoeorjane@someserver.com < /tmp/sometext.txt

```

### Come visualizzare un'altra e-mail mentre si compone

Un problema comune con Mutt è che durante la composizione di una nuova mail (o risposta), non è possibile aprire un'altra mail (ad esempio per il controllo con un'altro corrispondente) senza chiudere la posta corrente (rinvio). La sezione seguente descrive una soluzione:

In primo luogo, avviare Mutt come al solito. Quindi, lanciare un'altra finestra del terminale. Ora avviare Mutt con

```
mutt -R

```

Ciò avvia Mutt in modalità di sola lettura, ed è possibile sfogliare le altre email a proprio piacimento. Si consiglia vivamente di lanciare sempre un secondo Mutt in modalità di sola lettura, altrimenti potrebbero insorgere facilmente alcuni conflitti.

Ora, questa soluzione richiede parecchia battitura, per cui sarebbe utile automatizzare un po'. Quanto segue funziona con [Awesome](/index.php/Awesome "Awesome"), per altri WM o DE, simili soluzioni sono probabilmente disponibili: cercare su google come aggiungere le scorciatoie da tastiera, e rendere eseguibili le scorciatoie desiderate

```
$TERM -e mutt -R 

```

dove $TERM è il proprio terminale.

Come per Awesome: editare il proprio rc.lua, e aggiungere il seguente su una delle prime righe, dove terminal = "yourTerminal", ecc.

```
mailview = terminal .. " -e mutt -R"

```

Questo utilizza automaticamente il terminale preferito, ".." è la concatenazione in Lua. Si noti lo spazio prima di -e.

Quindi, aggiungere il seguente all'interno di --{{{ Key bindings

```
awful.key({ modkey,           }, "m", function() awful.util.spawn(mailview) end),

```

Omettere la virgola finale se questa è l'ultima riga. È possibile, naturalmente usare un'altra chiave diversa da "m". Ora, salvare e uscire, e controllare la sintassi con

```
awesome -k

```

Se è tutto a posto, riavviare awesome e fare una prova!

Ora, un esempio di utilizzo: Lanciare mutt come di solito. Incominciare una nuova mail, poi premere "Mod4"+"m". Questo apre la casella di posta elettronica in un nuovo terminale, dove si può navigare e leggere altre e-mail. Ora, un accurato bonus: uscire da questa sessione di Mutt in sola lettura con "q", e la finestra di terminale creata scomparirà!

### Mutt-Sidebar

Il pacchetto [mutt-sidebar](https://aur.archlinux.org/packages/mutt-sidebar/) disponibile su [AUR](/index.php/AUR_(Italiano) "AUR (Italiano)") contiene una patch per avere la lista delle cartelle in una colonna a sinistra della finestra di mutt.

Per ogni informazione visitare l'homepage dello sviluppatore [qui](http://www.lunar-linux.org/mutt-sidebar/).

## Vedere anche

*   [The official Mutt website](http://www.mutt.org/)
*   [The Mutt wiki](http://wiki.mutt.org/)
*   [Brisbin's great guide on how to setup different IMAP accounts with mutt + offlineimap + msmtp](http://pbrisbin.com/posts/two_accounts_in_mutt/)
*   [Documentation on Configuring Getmail with rcfiles](http://pyropus.ca/software/getmail/configuration.html#running)