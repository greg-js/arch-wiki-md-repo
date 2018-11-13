Articoli correlati

*   [Thunderbird Export URLs](/index.php/Thunderbird_Export_URLs "Thunderbird Export URLs")
*   [Firefox (Italiano)](/index.php/Firefox_(Italiano) "Firefox (Italiano)")

**Mozilla Thunderbird** è un client email, newsgroup, e aggregatore di notizie progettato attorno alla semplicità e alla completa personalizzazione evitando la pesantezza. Supporta POP, IMAP, SMTP, S/MIME, e la criptazione OpenPGP (attraverso l'estensione Enigmail). Similmente a [Firefox](/index.php/Firefox "Firefox"), possiede una grande varietà di estensioni e addon, disponibili per il download, che aggiungono nuove funzionalità.

## Contents

*   [1 Installazione](#Installazione)
*   [2 Estensioni](#Estensioni)
    *   [2.1 EnigMail - Criptazione](#EnigMail_-_Criptazione)
        *   [2.1.1 Condivisione della chiave pubblica](#Condivisione_della_chiave_pubblica)
        *   [2.1.2 Criptazione email](#Criptazione_email)
        *   [2.1.3 Decriptazione Email](#Decriptazione_Email)
    *   [2.2 Lightning - Calendario](#Lightning_-_Calendario)
    *   [2.3 FireTray - Tray icon](#FireTray_-_Tray_icon)
*   [3 Impostazioni Varie](#Impostazioni_Varie)
    *   [3.1 Impostare il browser predefinito](#Impostare_il_browser_predefinito)
    *   [3.2 Impostare la modalità del testo e font uniformi](#Impostare_la_modalità_del_testo_e_font_uniformi)
    *   [3.3 Webmail con Thunderbird](#Webmail_con_Thunderbird)
*   [4 Risoluzione dei Problemi](#Risoluzione_dei_Problemi)

## Installazione

Installare il pacchetto [thunderbird](https://www.archlinux.org/packages/?name=thunderbird) dal repository [extra].

Sono disponibili anche diverse alternative su [AUR](/index.php/AUR "AUR"):

*   [thunderbird-esr-bin](https://aur.archlinux.org/packages/thunderbird-esr-bin/) (versione con supporto a [lungo termine](http://www.mozilla.org/thunderbird/organizations/))
*   [thunderbird-beta-bin](https://aur.archlinux.org/packages/thunderbird-beta-bin/) (la versione ufficiale di [sviluppo](http://www.mozilla.org/en-US/thunderbird/channel/))
*   [thunderbird-nightly](https://aur.archlinux.org/packages/thunderbird-nightly/) (una versione [nightly](https://ftp.mozilla.org/pub/mozilla.org/thunderbird/nightly/latest-comm-central/))

Sono disponibili svariati pacchetti di localizzazione per un gran numero di lingue. Per installare il pacchetto italiano:

```
$ pacman -S thunderbird-i18n-it

```

## Estensioni

### EnigMail - Criptazione

[EnigMail](https://www.enigmail.net) è un'estensione che permette di scrivere e ricevere email firmate e/o criptate con lo standard OpenPGP, ed è rilasciata sotto la [GNU Privacy Guard (GnuPG)](https://en.wikipedia.org/wiki/GNU_Privacy_Guard "wikipedia:GNU Privacy Guard").

Può essere installata da [addons.mozilla.org](https://addons.mozilla.org/thunderbird/addon/enigmail/) (utilizzando `Add-ons Manager`) oppure da [AUR](/index.php/AUR "AUR"). I relativi pacchetti sono: [thunderbird-enigmail](https://aur.archlinux.org/packages/thunderbird-enigmail/) e [thunderbird-enigmail-bin](https://aur.archlinux.org/packages/thunderbird-enigmail-bin/).

#### Condivisione della chiave pubblica

Ci sono molti modi per distribuire la chiave pubblica. Uno di questi è quello di caricarla su un *public keyserver network*. Un'altro modo può essere quello di condividerla con gli amici usando email criptate.

#### Criptazione email

Può accadere che la criptazione non funzioni bene con email che contengono HTML. Prima di tutto è raccomandabile impostare nella finestra della mail da criptare: *Opzioni > Formato di Consegna > Solo testo*.

Una volta terminata la mail è possibile firmarla attraverso il menu *OpenPGP*.

#### Decriptazione Email

Nel caso in cui un'email sia criptata, provando ad aprirla apparirà una finestra popup in cui digitare la *keyphrase*.

### Lightning - Calendario

[Lightning](https://www.mozilla.org/projects/calendar/lightning/) è un calendario che aggiunge ulteriori funzionalità a Thunderbird. Per installarlo è possibile utilizzare [addons.mozilla.org](https://addons.mozilla.org/thunderbird/addon/lightning/) oppure il pacchetto presente in [AUR](/index.php/AUR "AUR") [lightning-bin](https://aur.archlinux.org/packages/lightning-bin/).

### FireTray - Tray icon

FireTray è un'estensione che aggiunge un'icona di sistema personalizzabile per Thunderbird nel pannello. E' possibile installarla da qui [addons.mozilla.org](https://addons.mozilla.org/thunderbird/addon/firetray/) oppure è reperibile il pacchetto [thunderbird-firetray](https://aur.archlinux.org/packages/thunderbird-firetray/) su [AUR](/index.php/AUR "AUR").

## Impostazioni Varie

### Impostare il browser predefinito

**Nota:** Dalla versione 24 le chiavi `network.protocol-handler.app.*` non hanno più effetto e non possono essere utilizzate per impostare il browser predefinito.

Le versioni più recenti di Thunderbird usano il browser predefinito impostato sul sistema. Attraverso Gnome Control Center si possono modificare le applicazioni predefinite: (*Gnome Control Center > Dettagli > Applicazioni Predefinite*) (disponibile in: [gnome-control-center](https://www.archlinux.org/packages/?name=gnome-control-center))

Ciò può essere annullato attraverso Thunderbird con *Preferenze > Avanzate > Generale > Editor di Configurazione* e cercando: `network.protocol-handler.warn-external`.

Se le seguenti linee sono tutte impostate su `false` (default), cambiarle con `true`, e quando verrà aperto un link Thunderbird chiederà quale applicazione utilizzare. Il risultato dipende dal [Desktop environment (Italiano)](/index.php/Desktop_environment_(Italiano) "Desktop environment (Italiano)") in uso, valori più comuni sono `/usr/bin/firefox`, `/usr/bin/google-chrome-stable`, per XFCE `/usr/bin/exo-open` o `/usr/bin/xdg-open` per gli ambienti senza DE.

```
network.protocol-handler.warn-external.ftp
network.protocol-handler.warn-external.http
network.protocol-handler.warn-external.https

```

### Impostare la modalità del testo e font uniformi

Per impostare la modalità testo in modo da leggere le mail senza sfruttare il rendering in HTML modificare *Visualizza > Corpo del messaggio come > ...*. Questo è il font standard [Monospace](https://en.wikipedia.org/wiki/Monospace_(Unicode) ma la grandezza del carattere è stata ereditata dalle impostazioni del sistema originale *fontconfig*. L'esempio seguente è una sua riscrittura con Ubuntu Mono di 10 pixel (disponibile in:[ttf-ubuntu-font-family](https://www.archlinux.org/packages/?name=ttf-ubuntu-font-family)).

Ricordarsi di digitare `fc-cache -fv` per aggiornare la cache di sistema dei font. Per maggiori informazioni vedere [Font configuration](/index.php/Font_configuration "Font configuration").

 `~/.config/fontconfig/fonts.conf` 
```
<?xml version="1.0"?>
<!DOCTYPE fontconfig SYSTEM "fonts.dtd">
<fontconfig>
  <match target="pattern">
    <test qual="any" name="family"><string>monospace</string></test>
    <edit name="family" mode="assign" binding="same"><string>Ubuntu Mono</string></edit>
    <!-- For Thunderbird, lowering default font size to 10 for uniformity -->
    <edit name="pixelsize" mode="assign"><int>10</int></edit>
  </match>
</fontconfig>

```

### Webmail con Thunderbird

Vedere il seguente wiki: [Using webmail with your email client](http://kb.mozillazine.org/Using_webmail_with_your_email_client).

## Risoluzione dei Problemi