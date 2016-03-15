Tratto dal sito web di awesome:

"*[awesome](http://awesome.naquadah.org/) è un window manager di ultima generazione altamente configurabile, per X system. Molto veloce, espandibile e distribuito con licenza GNU GPLv2.* *Principalmente indicato per utenti avanzati, sviluppatori e persone che svolgono quotidianamente attività informatiche e che desiderano uno stretto controllo del loro ambiente grafico.*"

## Contents

*   [1 Installazione](#Installazione)
*   [2 Iniziare ad usare awesome](#Iniziare_ad_usare_awesome)
    *   [2.1 Uso di awesome](#Uso_di_awesome)
*   [3 Configurazione](#Configurazione)
    *   [3.1 Creazione del file di configurazione](#Creazione_del_file_di_configurazione)
    *   [3.2 Ulteriori risorse di configurazione](#Ulteriori_risorse_di_configurazione)
    *   [3.3 Debug di rc.lua usando Xephyr](#Debug_di_rc.lua_usando_Xephyr)
*   [4 Temi](#Temi)
    *   [4.1 Impostare lo sfondo](#Impostare_lo_sfondo)
        *   [4.1.1 Immagine di sfondo casuale](#Immagine_di_sfondo_casuale)
*   [5 Suggerimenti](#Suggerimenti)
    *   [5.1 Effetti stile compiz](#Effetti_stile_compiz)
    *   [5.2 Nascondere / mostrare wibox in awesome 3](#Nascondere_.2F_mostrare_wibox_in_awesome_3)
    *   [5.3 Abilitare le printscreens](#Abilitare_le_printscreens)
    *   [5.4 Tagging dinamico](#Tagging_dinamico)
    *   [5.5 Space Invaders](#Space_Invaders)
    *   [5.6 Menu popup](#Menu_popup)
    *   [5.7 Aggiungere widgets in awesome](#Aggiungere_widgets_in_awesome)
    *   [5.8 Trasparenze](#Trasparenze)
        *   [5.8.1 ImageMagick](#ImageMagick)
    *   [5.9 Autoavvio di programmi](#Autoavvio_di_programmi)
    *   [5.10 Passare dei contenuti ai widgets con l'awesome-client](#Passare_dei_contenuti_ai_widgets_con_l.27awesome-client)
    *   [5.11 Utilizzo di alcuni pannelli eyecandy con awesome](#Utilizzo_di_alcuni_pannelli_eyecandy_con_awesome)
*   [6 Risoluzione dei problemi](#Risoluzione_dei_problemi)
    *   [6.1 Tasto Mod4](#Tasto_Mod4)
        *   [6.1.1 Tasto Mod4 per versioni IBM ThinkPad](#Tasto_Mod4_per_versioni_IBM_ThinkPad)
*   [7 Links utili](#Links_utili)

## Installazione

[Awesome](https://aur.archlinux.org/packages.php?ID=41362) è disponibile su [AUR](/index.php/AUR_(Italiano) "AUR (Italiano)") a causa dell'utilizzo di cairo-xcb come backend.

In alternativa installare la il ramo di sviluppo più recente [awesome-git](https://aur.archlinux.org/packages/awesome-git/) sempre da [AUR](/index.php/AUR_(Italiano) "AUR (Italiano)")

**Nota:** Awesome viene continuamente modificato dai suoi sviluppatori, cambiando spesso anche la sintassi dei file di configurazione. Sia questo wiki che il [wiki ufficiale](https://awesome.naquadah.org/wiki/Main_Page) si basano esclusivamente sull'ultima versione stabile.

## Iniziare ad usare awesome

### Uso di awesome

Per avviare awesome senza un gestore di sessioni, semplicemente aggiungere **<tt>exec awesome</tt>** allo script di avvio di proprio gradimento (e.g. `~/.xinitrc`.)

Per avviare awesome da un gestore di sessioni, vedere [l'articolo qui](/index.php/Display_manager "Display manager").

**[SLiM](/index.php/SLiM "SLiM")** è un gestore di sessioni molto diffuso e leggero ed è vivamente raccomandato. Si potrebbe fare come segue:

1) Modificare `/etc/slim.conf` per avviare la sessione di awesome, aggiungere awesome alla riga delle sessioni.
Per esempio:

```
sessions             awesome,wmii,xmonad

```

2) Modificare il file `~/.xinitrc`

```
DEFAULT_SESSION=awesome
case $1 in
  awesome) exec awesome ;;
  wmii) exec wmii ;;
  xmonad) exec xmonad ;;
  *) exec $DEFAULT_SESSION ;;
esac

```

È anche possibile avviare awesome come utente privilegiato senza nessun gestore di sessioni e addirittura senza eseguire il log in, dopo alcune opportune modifiche su `~/.xinitrc` e `/etc/inittab`. Consultare [Start X at login](/index.php/Start_X_at_login "Start X at login").

## Configurazione

Awesome include alcune ottime configurazioni predefinite pronte all'uso, ma presto o tardi si vorrà cambiare qualcosa. Il file di configurazione lua-based è in `~/.config/awesome/rc.lua`.

### Creazione del file di configurazione

Per prima cosa, eseguire quanto segue per creare la directory necessaria ai seguenti passi:

```
$ mkdir -p ~/.config/awesome/

```

Una volta compilato, awesome proverà ad usare qualsiasi configurazione contenuta in `~/.config/awesome/rc.lua`. Questo file non viene creato di default, così per prima cosa bisognerà copiare il file template:

```
$ cp /etc/xdg/awesome/rc.lua ~/.config/awesome/

```

La sintassi in uso per la configurazione cambia spesso quando awesome viene aggiornato. Perciò ricordarsi di ripetere il comando sopra quando awesome da qualche strano comportamento, oppure quando si ha voglia di fare qualche cambiamento.

Per maggiori informazioni sulle configurazioni di awesome, consultare [la pagina wiki di awesome](http://awesome.naquadah.org/wiki/Awesome_3_configuration)

### Ulteriori risorse di configurazione

**Note:** La sintassi di configurazione di awesome cambia frequentemente, così probabilmente si dovrà modificare ogni file che si scarica.

Alcuni esempi efficaci di rc.lua sono i seguenti:

*   [http://git.sysphere.org/awesome-configs/tree/](http://git.sysphere.org/awesome-configs/tree/) - Awesome 3.4 configurations from Adrian C. (anrxc)
*   [http://pastebin.com/f6e4b064e](http://pastebin.com/f6e4b064e) - Darthlukan's awesome 3.4 configuration.
*   [http://www.calmar.ws/dotfiles/dotfiledir/dot_awesomerc.lua](http://www.calmar.ws/dotfiles/dotfiledir/dot_awesomerc.lua)
*   [http://github.com/wolgri/wolgri.config/tree/master/.config/awesome/rc.lua](http://github.com/wolgri/wolgri.config/tree/master/.config/awesome/rc.lua)
*   [http://oxmoz.no-ip.org/awesome/rc.lua](http://oxmoz.no-ip.org/awesome/rc.lua)
*   [http://www.ugolnik.info/downloads/awesome/rc.lua](http://www.ugolnik.info/downloads/awesome/rc.lua) (screen) - Awesome 3 with small titlebar and statusbar.
*   [http://github.com/bash/dotfiles/blob/master/.config/awesome/rc.lua](http://github.com/bash/dotfiles/blob/master/.config/awesome/rc.lua)
*   [http://github.com/nblock/config/blob/master/.config/awesome/rc.lua](http://github.com/nblock/config/blob/master/.config/awesome/rc.lua)
*   User Configuration Files [http://awesome.naquadah.org/wiki/User_Configuration_Files](http://awesome.naquadah.org/wiki/User_Configuration_Files)

### Debug di rc.lua usando Xephyr

Questo è un ottimo modo di fare un debug di rc.lua, senza intaccare il desktop corrente. Copiare rc.lua in un nuovo file, rc.lua.new, e modificarlo ssecondo necessità. Poi avviare una nuova istanza di awesome in Xephyr (che permetterà di eseguire X all'interno di un'altra sessione di X, fornendo rc.lua.new come un file di configurazione come quanto segue:

```
$ Xephyr -ac -br -noreset -screen 1152x720 :1 &
$ DISPLAY=:1.0 awesome -c ~/.config/awesome/rc.lua.new

```

Il grosso vantaggio di questo tipo di approccio è che se si interrompe rc.lua.new, non si interrompe la sessione desktop corrente di awesome (e possibili crash di tutte le applicazioni X, perdita di dati non salvati, etc). Una volta soddisfatti delle nuove impostazioni, spostare rc.lua.new a rc.lua e riavviare awesome. Si sarà così sicuri del buon esito al riavvio con le nuove configurazioni, e non si creeranno eventuali complicazioni.

## Temi

Beautiful è una libreria lua che permette la manipolazione di temi awesome usando un file esterno. Risulta molto semplice cambiare l'intero schema di colori e sfondi awesome senza fare cambiamenti in rc.lua.

Il tema predefinito si trova in `/usr/share/awesome/themes/default`. Copiarlo in `~/.config/awesome/themes/default` e modificare il percorso del tema in rc.lua.

Ulteriori dettagli [qui](http://awesome.naquadah.org/wiki/Beautiful)

Alcuni esempi di [temi](http://awesome.naquadah.org/wiki/Beautiful_themes)

### Impostare lo sfondo

Beautiful può occuparsi della gestione degli sfondi, quindi non si dovrà modificare i files `~/.xinitrc` o `~/.xsession`. Si potrà ottenere così un particolare sfondo per tema utilizzato. Dando un'occhiata al file del tema predefinito si osserverà una chiave wallpaper_cmd, il comando dato verrà eseguito quando beautiful.init ("percorso_al_file_del_tema") viene avviato. Si potrà dare qui il comando, oppure rimuovere/commentare la chiave se non si desidera che Beautiful interferisca con la gestione dello sfondo.

Per esempio, se si usa awsetbg per impostare lo sfondo, si potrà scrivere:

```
wallpaper_cmd = { "awsetbg -f .config/awesome/themes/awesome-wallpaper.png" }

```

**Nota:** Per avere awsetbg funzionante si necessità di avere un programma per la gestione degli sfondi già installato. Ad esempio potete utilizzare il semplice e leggero "[Feh](/index.php/Feh "Feh")".

#### Immagine di sfondo casuale

Per ottenere una rotazione casuale degli sfondi, commentare la riga wallpaper_cmd, ed aggiungere uno script in `~/.xinitrc` con il seguente codice:

```
while true;
do
  awsetbg -r <path/to/the/directory/of/your/wallpapers>
  sleep 15m
done &

```

## Suggerimenti

Chi lo desidera può aggiungere consigli, trucchi ed esperienze personali a beneficio di tutti gli altri utenti awesome .

### Effetti stile compiz

Revelation visualizza una panoramica di tutti i propri clients aperti; un click sinistro su un client visualizzerà sul primo tag che il client è visibile e lo evidenzierà. Inoltre, il tasto Enter evidenzierà il client corrente, mentre con Escape si potrà uscire.

[http://awesome.naquadah.org/wiki/Revelation](http://awesome.naquadah.org/wiki/Revelation)

### Nascondere / mostrare wibox in awesome 3

Per indicare a Modkey-b di nascondere/mostrare la statusbar predefinita sullo schermo attivo (opzione predefinita in awesome 2.3), aggiungere a *clientkeys* in rc.lua:

```
awful.key({ modkey }, "b", function ()
    mywibox[mouse.screen].visible = not mywibox[mouse.screen].visible
end),

```

### Abilitare le printscreens

Per abilitare su awesome le istantanee del desktop con il tasto PrtScr, si dovrà avere un programma di acquisizione dello schermo. Scrot è un'utilità di facile utilizzo , ed è disponibile nei repository di Arch.

Da console:

```
# pacman -S scrot

```

e installare anche le dipendenze opzionali se vi è la necessità.

La prossima cosa che si dovrà stabilire è il nome del tasto PrtScr, molto spesso è chiamato "Print" ma non si può mai esserne troppo sicuri. Avvio:

```
# xev

```

Premere il tasto PrtScr, che dovrebbe restituire qualcosa simile a:

```
 KeyPress event ....
     root 0x25c, subw 0x0, ...
     state 0x0, keycode 107 (keysym 0xff61, **Print**), same_screen YES,
     ....

```

In questo caso, come si vede, il nome del tasto è Print.

Segue la configurazione di awesome.

Da qualche parte, nella stringa globalkeys (non importa dove) scrivere:

Lua code:

```
 awful.key({ }, "Print", function () awful.util.spawn("scrot -e 'mv $f ~/screenshots/ 2>/dev/null'") end),

```

Un buon posto dove sistemarlo sarebbe sotto la keyhook per l'avvio del terminale. Per trovare questa riga cercare con un editor di testo:

```
awful.util.spawn(terminal)

```

Inoltre questa funzione salva le foto realizzate dentro `~/screenshots/`,nel caso, modificare a piacere.

### Tagging dinamico

[Eminent](http://awesome.naquadah.org/wiki/Eminent) è una piccola libreria lua che fornisce facilmente e velocemente un tagging dinamico stile wmii. Diversamente da shifty, eminent non ha lo scopo di rendere il sistema tagging un qualcosa di comprensibile, ma tenta di rendere il tagging dinamico il più semplice possibile. Infatti, a parte importare la libreria eminent, non si dovrà fare alcuna modifica a rc.lua, perchè eminent si occuperà di tutto.

[Shifty](http://awesome.naquadah.org/wiki/Shifty) è un'estensione di Awesome 3 che implementa il tagging dinamico. Fornisce inoltrre un'ottima configurazione per il client, lasciando che l'utente sia il "padrone" del proprio desktop con la sola impostazione di due variabili di configurazione ed alcuni ulteriori "keybindings".

### Space Invaders

[Space Invaders](http://awesome.naquadah.org/wiki/Space_Invaders) è un demo per illustrare Awesome Lua API.

Notare che non è più incluso nel pacchetto Awesome dalla release 3.4-rc1.

### Menu popup

Awesome3 dispone in modo predefinito di un semplice menu, la cui personalizzazione è molto semplice ora. Comunque se si usa awesome 2.x, dare un'occhiata a [awful.menu](http://awesome.naquadah.org/wiki/Awful.menu).

Un esempio per awesome3:

```
myawesomemenu = {
   { "lock", "xscreensaver-command -activate" },
   { "manual", terminal .. " -e man awesome" },
   { "edit config", editor_cmd .. " " .. awful.util.getdir("config") .. "/rc.lua" },
   { "restart", awesome.restart },
   { "quit", awesome.quit }
}

mycommons = {
   { "pidgin", "pidgin" },
   { "OpenOffice", "soffice-dev" },
   { "Graphic", "gimp" }
}

mymainmenu = awful.menu.new({ items = { 
                                        { "terminal", terminal },
                                        { "icecat", "icecat" },
                                        { "Editor", "gvim" },
                                        { "File Manager", "pcmanfm" },
                                        { "VirtualBox", "VirtualBox" },
                                        { "Common App", mycommons, beautiful.awesome_icon },
                                        { "awesome", myawesomemenu, beautiful.awesome_icon }
                                       }
                             })

```

### Aggiungere widgets in awesome

I *Widgets in awesome sono oggetti che si possono integrare nella widget-box (statusbars e titlebars), possono fornire varie ed utili informazioni riguardo al sistema, direttamente dal window manager. I Widgets sono semplici da usare e offrono un buon compromesso di flessibilità.* -- Fonte [Awesome Wiki: Widgets](http://awesome.naquadah.org/wiki/Widgets_in_awesome).

C'è un'intera libreria per widget chiamata **Wicked** (compatibile con le versioni di awesome **precedenti alla 3.4**), che fornisce ulteriori widgets, come MPD widget, uso CPU, uso memory, etc. Per ulteriori informazioni consultare [Wicked page](http://awesome.naquadah.org/wiki/Wicked).

Per un'alternativa a Wicked su awesome v3.4 consultare **[Vicious](http://awesome.naquadah.org/wiki/Vicious)**, **[Obvious](http://awesome.naquadah.org/wiki/Obvious)** and **[Bashets](http://awesome.naquadah.org/wiki/Bashets)**. Se si pensa di scegliere vicious, si consiglia di dare anche uno sguardo a [vicious documentation](http://git.sysphere.org/vicious/tree/README).

### Trasparenze

Awesome ha il supporto alla vera trasparenza utilizzando xcompmgr. Da notare che si potrebbe voler installare la versione git di xcompmgr, [disponibile su AUR](https://aur.archlinux.org/packages.php?ID=16554).

Aggiungere quanto segue a `~/.xinitrc`:

```
exec xcompmgr &

```

Consultare *man xcompmgr* o [xcompmgr](/index.php/Xcompmgr "Xcompmgr") per ulteriori opzioni.

In awesome 3.4, la transparenza delle finestre può essere impostata dinamicamente utilizzando dei segnali. Per esempio, il file rc.lua può contenere i seguenti:

```
client.add_signal("focus", function(c)
                              c.border_color = beautiful.border_focus
                              c.opacity = 1
                           end)
client.add_signal("unfocus", function(c)
                                c.border_color = beautiful.border_normal
                                c.opacity = 0.7
                             end)

```

**Se hai messaggi di errore relativi add_signal, utilizzando insteaded connect_signal.** Da notare che se si usa conky, bisogna impostarlo per creare la sua finestra invece di usare il desktop. Per fare ciò, modificare `~/.conkyrc` così:

```
own_window yes
own_window_transparent yes
own_window_type desktop

```

Altrimenti si potrebbero osservare strani comportamenti, come ad esempio la trasparenza di tutte le finestre. Da notare inoltre che da quando conky creerà la finestra trasparente sul desktop, ogni azione definita dal file rc.lua per il desktop non funzionerà dove c'è conky in esecuzione.

Su awesome 3.1, c'è un lavoro in fase di sviluppo per la psudo-trasparenza su wiboxes. Per abilitarlo, aggiungere 2 cifre esadecimali ai colori nel proprio file dei temi (`~/.config/awesome/themes/default`, che è normalmente una copia di `/usr/share/awesome/themes/default`), come illustrato qui:

```
bg_normal = #000000AA

```

dove "AA" è il valore impostato per la trasparenza.

#### ImageMagick

Si potrebbero avere problemi se si imposta il wallpaper con il comando *display* di imagemagick, dato che non funziona bene con xcompmgr. Notare che awsetbg userà *display* se non ha altre opzioni disponibili. Installare habak, feh, hsetroot o qualsiasi altro programma dovrebbe risolvere il problema (*grep -A 1 wpsetters /usr/bin/awsetbg* per vedere le opzioni).

### Autoavvio di programmi

Aggiungere i seguenti codici in rc.lua, e sostituire le applicazioni nella sezione autorunApps con quelle desiderate. Esempio:

```
-- Autorun programs
autorun = true
autorunApps = 
{ 
   "swiftfox",
   "mutt",
   "consonance",
   "linux-fetion",
   "weechat-curses",
}
if autorun then
   for _, app in pairs(autorunApps) do
       awful.util.spawn(autorunApps[app])
   end
end

```

oppure così:

```
os.execute("mutt &"),
os.execute("weechat-curses &"),

```

Per eseguire applicazioni solo una volta, ad esempio per riavviare awesome, usare questa funzione (da [awesome wiki](http://awesome.naquadah.org/wiki/Autostart)):

```
function run_once(prg)
	if not prg then
		do return nil end
	end
	awful.util.spawn_with_shell("pgrep -u $USER -x " .. prg .. " || (" .. prg .. ")")
end

```

```
-- AUTORUN APPS!
run_once("parcellite")

```

### Passare dei contenuti ai widgets con l'awesome-client

Si può facilmente inviare del testo ad un widget awesome. Creare un nuovo widget:

```
 mywidget = widget({ type = "textbox", name = "mywidget" })
 mywidget.text = "initial text"

```

Per aggiornare il testo da una fonte esterna, usare awesome-client:

```

 echo -e 'mywidget.text = "new text"' | awesome-client

```

Non dimenticare di aggiungere il widget alla propria wibox.

### Utilizzo di alcuni pannelli eyecandy con awesome

Se siete piacevolmente impressionati dalla leggerezza e funzionalità di Awesome, ma non vi piace la visualizzazione *stile hacker*, potete trasformarlo, tramite pannelli alternativi, rendendolo più gradevole alla vista. Basta installare xfce4-panel:

```
sudo pacman -S xfce4-panel

```

Quindi aggiungerlo al proprio [[filename|rc.lua}} nella sezione di avvio automatico (autorun) come descritto in precedenza. Si suppone che, per un utente Awesome, la configurazione del pannello non sia di particolare difficolta. È anche possibile commentare la sezione in modo che creino wiboxes per ogni schermo (partendo da "mywibox[s] = awful.wibox({ position = "top", screen = s })" ) ma ciò non è necessario. In ogni caso ricordarsi di controllare il proprio rc.lua con il comando

```
awesome -k rc.lua

```

Inoltre si dovrebbe modificare il tasto rapido "modkey+R", al fine di avviare qualche altro lanciatore di applicazione invece di costruirlo in awesome. Xfrun4, bashrun, etc. Come esempio controllare la sezione *Lanciatori di applicazioni* nell'articolo di [Openbox](/index.php/Openbox_(Italiano) "Openbox (Italiano)"). Non dimenticarsi di aggiungere:

```
      properties = { floating = true } },
    { rule = { instance = "$yourapplicationlauncher" },

```

Al proprio `rc.lua`. Questo metodo dovrebbe funzionare con altri pannelli, ma l'autore del wiki non ha potuto verificare. Sentitevi liberi di aggiungere altre parti di ambienti desktop al vostro Awesome.

## Risoluzione dei problemi

### Tasto Mod4

Il tasto Mod4 è in maniera predefinita il tasto **Win**. Se per qualche ragione non è indicato di default, si può verificare il tasto corrispondente al proprio Mod4 con

```
$ xev

```

Dovrebbe essere 115 per quello sinistro. Poi aggiungere quanto segue a `~/.xinitrc`

```
xmodmap -e "keycode 115 = Super_L" -e "add mod4 = Super_L"
exec awesome

```

Il problema in questo caso è che alcune installazioni di xorg riconoscono *keycode 115*, ma in modo non corretto come il tasto 'Seleziona'. Il comando precedente rimappa esplicitamente *keycode 115* alla corretta chiave 'Super_L'.

#### Tasto Mod4 per versioni IBM ThinkPad

IBM ThinkPads solitamente non include il tasto Window (sebbene Lenovo abbia infranto questa tradizione con i propri ThinkPads). Attualmente, il tasto Alt per combinazioni di comandi non è usato di default da rc.lua (consultare il wiki Awesome wiki per le liste di comandi), che gli permette di essere usato come un rimpiazzo per il tasto Super/Mod4/Win. Fatto questo, modificare rc.lua e sostituire:

```
modkey = "Mod4"

```

con:

```
modkey = "Mod1"

```

Note: Awesome possiede un paio di comandi che fanno uso di Mod4 più una singola lettera. Cambiare Mod4 per Mod1/Alt può causare sovrapposizioni per alcune combinazioni di tasti. Il limitato numero di circostanze in cui potrebbe succedere può essere cambiato nel file rc.lua.

Se non si ama cambiare gli standard di awesome, si potrebbe voler cambiare un singolo tasto. Per esempio il tasto blocco maiuscole è in genere poco usato (è un fatto soggettivo comunque) aggiungere il seguente contenuto a `~/.Xmodmap`

```
clear lock 
add mod4 = Caps_Lock

```

e [(ri)caricare](/index.php/Xmodmap#Custom_table "Xmodmap") il file. Così si cambierà il tasto blocco maiuscole nel tasto mod4 che funzionerà notevolmente bene con le impostazioni standard awesome. Inoltre, se necessario, fornisce il tasto mod4 al altri programmi basati su X.

## Links utili

*   [http://awesome.naquadah.org/wiki/FAQ](http://awesome.naquadah.org/wiki/FAQ) - FAQ
*   [http://www.lua.org/pil/](http://www.lua.org/pil/) - Programming in Lua (first edition)
*   [http://awesome.naquadah.org/](http://awesome.naquadah.org/) - The official awesome website
*   [http://awesome.naquadah.org/wiki/Main_Page](http://awesome.naquadah.org/wiki/Main_Page) - the awesome wiki
*   [http://www.penguinsightings.org/desktop/awesome/](http://www.penguinsightings.org/desktop/awesome/) - A review