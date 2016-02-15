Firefox è un web browser open source di [Mozilla](http://www.mozilla.com). Il pacchetto di Firefox in Arch Linux è compilato in maniera indipendente dalla distribuzione ufficiale. Infatti sia l'icona (il pianeta..) che il nome sono diversi dal nome e dal logo ufficiale di Firefox. Questo perchè è possibile distribuire firefox, con il suo nome e il suo logo, a condizione che non siano state fatte modifiche non ufficiali (ad es. patch personalizzate).

## Contents

*   [1 Abilitare il Firefox Branding](#Abilitare_il_Firefox_Branding)
    *   [1.1 Ricompilare](#Ricompilare)
    *   [1.2 Configurazione Avanzata](#Configurazione_Avanzata)
    *   [1.3 Branding senza ricompilare](#Branding_senza_ricompilare)
*   [2 Estensioni](#Estensioni)
*   [3 Plugins](#Plugins)
    *   [3.1 Plugins utili](#Plugins_utili)
        *   [3.1.1 Flash](#Flash)
        *   [3.1.2 MPlayer](#MPlayer)
        *   [3.1.3 Gecko Media Player](#Gecko_Media_Player)
        *   [3.1.4 Java](#Java)
        *   [3.1.5 Citrix](#Citrix)
        *   [3.1.6 Adobe Reader](#Adobe_Reader)
    *   [3.2 I Plugins risultano installati ma non funzionano](#I_Plugins_risultano_installati_ma_non_funzionano)
    *   [3.3 Non riesco a scaricare i plugins](#Non_riesco_a_scaricare_i_plugins)
*   [4 Tips & Tricks](#Tips_.26_Tricks)
    *   [4.1 Font](#Font)
        *   [4.1.1 DPI](#DPI)
        *   [4.1.2 Rimpiazzamento dei Font](#Rimpiazzamento_dei_Font)
        *   [4.1.3 Configurazione dei Font](#Configurazione_dei_Font)
    *   [4.2 Alleggerire, Accellerare Firefox / Sistemare i fonts e i problemi dei controlli](#Alleggerire.2C_Accellerare_Firefox_.2F_Sistemare_i_fonts_e_i_problemi_dei_controlli)
    *   [4.3 Perchè ottengo questo errore quando clicco col tasto centrale del mouse?](#Perch.C3.A8_ottengo_questo_errore_quando_clicco_col_tasto_centrale_del_mouse.3F)
    *   [4.4 Perchè il pulsante _backspace_ non esegue la funzione 'Indietro'?](#Perch.C3.A8_il_pulsante_backspace_non_esegue_la_funzione_.27Indietro.27.3F)
    *   [4.5 Articoli con ulteriori consigli](#Articoli_con_ulteriori_consigli)
*   [5 Derivati di Firefox](#Derivati_di_Firefox)
*   [6 Alternative a Firefox](#Alternative_a_Firefox)
*   [7 Links Esterni](#Links_Esterni)

# Abilitare il Firefox Branding

Per attivare i vari marchi o cambiare l'user agent ci sono diversi modi. È possibile ricompilare, modificare il browser con le estensioni o utilizzare configurazioni avanzate. Nota che distrubuire una versione del genere potrebbe essere illegale!

## Ricompilare

La seguente procedura è per la versione 2.x di Firefox. Una versione ufficiale di Firefox 3.0.1-2 è disponibile da AUR [qui](https://aur.archlinux.org/packages.php?ID=18019). Sarà utilizzato [ABS](/index.php/ABS "ABS") per ricompilare Firefox. È necessario avere **cvsup** e **wget** installati. Lanciare il seguente comando:

```
abs

```

Se è il primo avvio ci vorrà qualche tempo, successivamente la sincronizzazione avverrà molto più rapidamente. Prima di fare un pacchetto personalizzato è generalmente consigliato lanciare abs. Ora bisogna creare una directory dove effettuare la ricompilazione:

```
 mkdir -p /var/abs/local/firefox
 cp /var/abs/extra/firefox/* /var/abs/local/firefox
 cd /var/abs/local/firefox

```

Con un editor di testo bisogna modificare il file mozconfig, aggiungendo la seguente linea alla fine del file.

```
ac_add_options --enable-official-branding

```

Salvare ed uscire, in seguito eseguire il comando:

```
md5sum mozconfig

```

Verrà generata una stringa, da copiare all'interno del file PKGBUILD. All'interno del file ci sono due array, "source" e "md5sum". Praticamente queste "md5sum" servono per controllare l'integrità del file al momento del download, il secondo elemento in md5sum corrisponde al file mozconfig, quindi va modificato sostituendolo con la stringa ottenuta precedentemente.

Sostituire questa stringa:

```
convert ${startdir}/src/mozilla/browser/app/default.xpm ${startdir}/pkg/usr/share/pixmaps/firefox.png

```

con la seguente:

```
convert ${startdir}/src/mozilla/dist/branding/default.xpm ${startdir}/pkg/usr/share/pixmaps/firefox.png

```

Più in giù ci sono queste due linee.

```
install -m644 ${startdir}/src/mozilla/browser/app/default.xpm ${startdir}/pkg/usr/lib/firefox/chrome/icons/default/
install -m644 ${startdir}/src/mozilla/browser/app/default.xpm ${startdir}/pkg/usr/lib/firefox/icons/

```

da sostituire con le seguenti.

```
install -m644 ${startdir}/src/mozilla/dist/branding/default.xpm ${startdir}/pkg/usr/lib/firefox/chrome/icons/default/
install -m644 ${startdir}/src/mozilla/dist/branding/default.xpm ${startdir}/pkg/usr/lib/firefox/icons/ 

```

Salvare anche questo file, uscire e poi eseguire:

```
makepkg

```

Ci vorrà del tempo, dipende anche dal sistema. Una volta creato il pacchetto va rimossa la versione di Firefox installata nel sistema.

```
pacman -Rd firefox

```

Installare la versione personalizzata.

```
pacman -A firefox-*.pkg.tar.gz

```

Si può anche provare ad aggiornare la versione precedente con.

```
pacman -U firefox-*.pkg.tar.gz

```

Ovviamente andrà sostituito l'asterisco * con la versione di firefox scelta.

## Configurazione Avanzata

Inserite `about:config` nella barra indirizzi di Firefox per accedere alla configurazione avanzata del browser. Nel filtro, inserire `useragent.extra.firefox`. Otterrete la stringa che indica il vostro corrente user-agent. Potete inserire ciò che volete qui. Se volete apparire sui siti come utenti della normale versione di Firefox, inserite **Firefox 3.0.6**. Modificate questa stringa in base alle successive versioni se ce ne sono.

## Branding senza ricompilare

Per "brandizzare" Bon Echo senza dover ricompilare l'intero browser, sarà necessario le icone di Bon Echo con quelle ufficiali di Firefox, e cambiare le stringhe "Bon Echo" e "BonEcho" in alcuni file. Lo script [firebrand](https://bbs.archlinux.org/viewtopic.php?pid=333606#p333606) si occupa proprio di questo. Eseguitelo dopo aver installato Firefox: per riottenere tutto come prima, basterà reinstallare di nuovo Firefox da zero. Lo script FireBrand si occuperà di scaricare le icone ufficiali da internet ogni volta che viene eseguito: per evitare ciò, basterà salvarsi da qualche parte le icone, e modificare lo script adattando la variabile NEWICONSDIR facendola puntare alla cartella dove avete appunto salvato le icone, ad esempio una cosa come

```
NEWICONSDIR=/usr/local/share/firebrand

```

# Estensioni

Prima di installare una qualsiasi estensione, assicuratevi che la cartella /tmp abbia i giusti permessi. Se le estensioni non si installano, un chmod 777 /tmp potrebbe infatti risolvere il problema.

*   [Adblock Plus](https://addons.mozilla.org/firefox/1865/) - Da non crederci, blocca le pubblicità.
*   [MediaPlayerConnectivity](https://addons.mozilla.org/firefox/446/) - Permette la visualizzazione di contenuti multimediali con un player esterno. Utile se si hanno problemi con qualche plugin tipo gecko-mediaplayer.
*   [CCK Wizard](https://addons.mozilla.org/firefox/2553/) - Permette di personalizzare molti aspetti di Firefox. Barra del titolo, user agent, icone, aspetti grafici, e molto altro.
*   [User Agent Switcher](https://addons.mozilla.org/firefox/59/) - Aggiunge un menu che permette di modificare l'user agent del browser al volo.

# Plugins

## Plugins utili

Per controllare quali plugin sono attualmente installati nel sistema, basta inserire il comando `about:plugins` nella barra degli indirizzi di Firefox.

#### Flash

```
pacman -S flashplugin

```

_Potreste aver bisogno di installare il pacchetto ttf-ms-fonts_ (pacman -S ttf-ms-fonts) _per permettere a flashplayer di visualizzare il testo correttamente._

#### MPlayer

Il plugin multimediale di Mplayer è uno dei più maturi. Questo permetterà di riprodurre praticamente tutti i file multimediali con cui potreste avere a che fare sulle pagine web.

```
pacman -S mplayer-plugin

```

#### Gecko Media Player

Un buon rimpiazzo dell'ormai anzianotto _mplayer-plugin_, è [Gecko Media Player](http://code.google.com/p/gecko-mediaplayer/). È generalmente più stabile se associato a MPlayer 1.0RC2\. _(Niente più crash con i trailer Apple.)_

```
$ sudo pacman -S gecko-mediaplayer

```

_(**Nota!** Assicuratevi di rimuovere il pacchetto mplayer-plugin se lo avevate già installato precedentemente.)_

#### Java

```
pacman -S jre

```

#### Citrix

```
(vedere [Citrix](/index.php/Citrix "Citrix") how-to)

```

#### Adobe Reader

Adobe Reader è disponibile solo su [AUR](https://aur.archlinux.org/packages.php?ID=16980) a causa di problemi di licenza.

```
yaourt -S --aur acroread

```

Sono consigliate comunque, alternative come l'estensione [PDF Download](http://www.pdfdownload.org/) e lettori pdf liberi come Evince (Gtk) o Okular (Qt4)

## I Plugins risultano installati ma non funzionano

Se avete installato i plugin come sopra descritto ma non sembrano venir utilizzati da Firefox (potete verificarlo scrivendo **about:config** nella barra indirizzi, premendo poi Invio), generalmente è a causa di un problema di permessi. Sistemateli col comando:

```
# chmod -R 755 /usr/lib/mozilla

```

Poi riavviate Firefox e tutto dovrebbe essere andato a posto.

## Non riesco a scaricare i plugins

In alcuni casi, non si riesce a scaricare e installare nessuno dei plugin di Firefox. La soluzione potrebbe essere quella di aggiungere la seguente linea al file /etc/hosts:

```
64.50.236.214   releases.mozilla.org

```

# Tips & Tricks

## Font

### DPI

Modificare il valore seguente ha come conseguenze note il miglioramento della resa visiva dei caratteri in Firefox. Scrivete _about:config_ nella barra indirizzi, e una volta confermato con OK, cercate per _dpi_, trovate la riga **layout.css.dpi** e cambiate il suo valore a **0**.

### Rimpiazzamento dei Font

Un altro modo per migliorare la resa dei caratteri è quello di sostituirli con degli altri. Create o modificate il file ~/.fonts.conf con questo contenuto:

```
<match target="pattern" name="family" >
       <test name="family" qual="any" >
               <string>**Helvetica**</string>
       </test>
       <edit mode="assign" name="family" >
               <string>**Bitstream Vera Sans**</string>
       </edit>
</match>

```

La prima voce riguarda il carattere che vogliamo sostituire, la seconda indica il carattere con il quale vogliamo sostituire il precedente.

### Configurazione dei Font

Per maggiori informazioni sulla configurazione dei caratteri in X, fare riferimento a [Xorg Font Configuration](/index.php/Xorg_Font_Configuration "Xorg Font Configuration").

## Alleggerire, Accellerare Firefox / Sistemare i fonts e i problemi dei controlli

_Rappresenta un fix per tutta la Suite Mozilla_

Provare ad aggiungere

```
 export MOZ_DISABLE_PANGO=1

```

al file /etc/profile (oppure al vostro .bashrc nella vostra home) e poi effettuare di nuovo il login.

## Perchè ottengo questo errore quando clicco col tasto centrale del mouse?

```
! The URL is not valid and cannot be loaded.

```

In alternativa, capita di vedersi caricare una pagina web a caso.

La ragione di questo sembra essere il comportamento predefinito, nei sistemi UNIX, nel caso si prema il pulsante centrale del mouse. Questo pulsante infatti è utilizzato comunemente per "incollare" una qualsiasi parte di testo si sia precedentemente evidenziata o aggiunta negli appunti. Inoltre, c'è una funzione in Firefox che di default carica l'indirizzo relativo al testo evidenziato, quando il tasto centrale viene rilasciato. Questo comportamento può essere disabilitato così:

Aprite il browser, e dopo aver scritto nella barra degli indirizzi:

```
about:config

```

cercate la riga 'middlemouse.contentLoadURL' e settate il suo valore a _falso_.

## Perchè il pulsante _backspace_ non esegue la funzione 'Indietro'?

Come descritto [qui](http://ubuntu.wordpress.com/2006/12/21/fix-firefox-backspace-to-take-you-to-the-previous-page/), questa funzione è stata rimossa per sistemare un bug. Ma la si può riattivare così:

Aprire il browser, e scrivere nella barra degli indirizzi

```
about:config

```

confermate, e cercate la riga 'browser.backspace_action' impostandola poi a 0 (zero).

## Articoli con ulteriori consigli

*   [Firefox Tips and Tweaks](/index.php/Firefox_Tips_and_Tweaks "Firefox Tips and Tweaks") -- in inglese
*   [Adding Firefox Search Engines As User](/index.php/Adding_Firefox_Search_Engines_As_User "Adding Firefox Search Engines As User") -- in inglese

# Derivati di Firefox

*   [Iceweasel](https://en.wikipedia.org/wiki/Iceweasel "wikipedia:Iceweasel") - Il nome di **due** differenti derivazioni di Firefox. Una è un progetto GNU basato su Firefox 1.5\. L'altro è in via di sviluppo da parte di Debian ed è basato sulla versione 2.0\. Al momento in cui scrivo, su [AUR](/index.php/AUR "AUR") c'è la versione GNU di Iceweasel.

*   [Swiftfox](http://getswiftfox.com/) - Una versione ottimizzata specificamente per vari processori di Firefox. Disponibile attualmente su AUR, anche se bisogna notare che su Archlinux è possibile ottimizzare il Firefox originale ottimizzandolo in equalmodo, semplicemente tramite ABS o comunque una normale compilazione.

*   [Swiftweasel](http://swiftweasel.sourceforge.net/) - Più o meno come Swiftfox, ma i suoi binari non sono coperti da licenze di tipo proprietario. Alcuni PKGBUILD sono disponibili su AUR.

# Alternative a Firefox

*   [Opera](/index.php/Opera "Opera") - Una completa suite per il web e le email. A codice chiuso, ma gratuito (come la birra).
*   [Epiphany](https://en.wikipedia.org/wiki/Epiphany_(browser) "wikipedia:Epiphany (browser)") - Il browser di default di GNOME. Usa lo stesso motore di Firefox.
*   [Konqueror](https://en.wikipedia.org/wiki/Konqueror "wikipedia:Konqueror") - Il browser di default di KDE. Usa il motore KHTML (dal quale è poi derivato Webkit).
*   [Dillo](https://en.wikipedia.org/wiki/Dillo "wikipedia:Dillo") - Un browser molto leggero.
*   [SeaMonkey](https://en.wikipedia.org/wiki/SeaMonkey "wikipedia:SeaMonkey") - Una naturale continuazione della Suite Mozilla originale. Include un web browser, un client email, ecc.
*   [Midori](https://en.wikipedia.org/wiki/Midori_(browser) "wikipedia:Midori (browser)") - Un browser GTK+ basato su Webkit. Leggerissimo e ancora in fase di sviluppo, ma già fornito di caratteristiche interessanti.

# Links Esterni

*   [Browser Speed Comparisons](http://www.howtocreate.co.uk/browserSpeed.html) - Vecchiotto ma ancora indicativo.
*   [Facts about Debian and Mozilla® Firefox](http://web.glandium.org/blog/?p=97) - Una raccolta di fatti relativi alle questioni sul trademark dal mantainer di Firefox per Debian.
*   [Gnuzilla and IceWeasel](http://www.gnu.org/software/gnuzilla/) - Sito ufficiale dei fork dei programmi GNU Mozilla.