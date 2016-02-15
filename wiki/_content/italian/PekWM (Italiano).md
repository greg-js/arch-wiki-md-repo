[Pek Window Manager](http://pekwm.org) è stato scritto da Claes Nästen. Il codice è basato su un'altro gestore di finestre aewm++, ma si è evoluto talmente da non avere più nulla in comune con aewm++. Dispone anche di un esteso set di funzioni, tra cui il raggruppamento delle finestre (non diverso da [ion3](/index.php/Ion3 "Ion3"), pwm o [fluxbox](/index.php/Fluxbox "Fluxbox")), proprietà automatiche, xinerama e keygrabber per il supporto al portachiavi, e molto altro.

## Contents

*   [1 Installazione](#Installazione)
*   [2 Avvio](#Avvio)
    *   [2.1 Metodo 1: avviare tramite kdm/gdm](#Metodo_1:_avviare_tramite_kdm.2Fgdm)
    *   [2.2 Metodo 2: avviare tramite xinitrc](#Metodo_2:_avviare_tramite_xinitrc)
*   [3 Configurazione](#Configurazione)
    *   [3.1 Menu](#Menu)
        *   [3.1.1 Modifica con MenuMaker](#Modifica_con_MenuMaker)
        *   [3.1.2 Utilizzando pekwm-menu](#Utilizzando_pekwm-menu)
        *   [3.1.3 Modifica manuale](#Modifica_manuale)
    *   [3.2 Tasti di scelta rapida](#Tasti_di_scelta_rapida)
    *   [3.3 Mouse](#Mouse)
    *   [3.4 Avvio automatico dei programmi](#Avvio_automatico_dei_programmi)
    *   [3.5 Variabii](#Variabii)
    *   [3.6 Proprietà automatiche](#Propriet.C3.A0_automatiche)
*   [4 Temi](#Temi)
    *   [4.1 GTK Appearance](#GTK_Appearance)
*   [5 Impostare uno sfondo](#Impostare_uno_sfondo)
*   [6 Problemi comuni](#Problemi_comuni)
    *   [6.1 Quando si utilizza la modalità TwinView di Nvidia, le finestre massimizzate attraversano entrambi gli schermi](#Quando_si_utilizza_la_modalit.C3.A0_TwinView_di_Nvidia.2C_le_finestre_massimizzate_attraversano_entrambi_gli_schermi)
    *   [6.2 La trasparenza e il composite non funzionano correttamente](#La_trasparenza_e_il_composite_non_funzionano_correttamente)
*   [7 Link esterni](#Link_esterni)

## Installazione

Potete installare PekWM dai repository.

```
pacman -S pekwm

```

## Avvio

### Metodo 1: avviare tramite kdm/gdm

Per prima cosa installare e attivare kdm o gdm. Per le istruzioni su come attivare un **login manager** , consultare la pagina [Display Manager](/index.php/Display_Manager_(Italiano) "Display Manager (Italiano)").

Pekwm dovrebbe essere aggiunta ai tipi di sessione. Selezionare pekwm dal menu a destra prima di effettuare la sessione di Login.

### Metodo 2: avviare tramite xinitrc

Nella cartella `home` del proprio utente, aggiungere il seguente comando nel file `.xinitrc` (~/.xinitrc)

```
exec pekwm

```

## Configurazione

Tutte le configurazioni principali vengono memorizzate nel file `~/.pekwm/config`. Questo file controlla tutta la tua configurazione, controlla l'area di lavoro e le impostazioni delle finestre, menu, la resistenza ed il comportamento dei bordi finestra, e altro ancora. Un esempio di un file di configurazione completo è presente nella documentazione ufficiale di PekWM in questa [pagina](http://www.pekwm.org/files/pekwm/doc/git/html/config/configfile.html).

### Menu

Pekwm, per impostazione predefinita, quando viene installato dal repositiori di arch utilizza alcuni menu predefiniti. Questi non riflettono ciò che esiste sul vostro sistema e come tali è altamente probabile che sia molto impreciso, rispetto a quello che effettivamente avete installato. Queste devono essere considerate come un esempio e non qualcosa che si dovrebbe usare senza alcuna modifica.

I menu sono memorizzati nel percorso `.pekwm/menu` sito nella vostra directory home (~/.pekwm/menu)

#### Modifica con MenuMaker

Un modo per impostare automaticamente i menu per le vostre applicazioni installate è utilizzare MenuMaker, previa sua installazione. Per impostare i menu di tutte le applicazioni installate eseguirlo con il seguente comando:

```
mmaker --no-desktop pekwm

```

**Nota:** con questo comando non si sovrascrive il precedente file di menu. Se invece si desidera sovrascriverlo dovete utilizzate l'opzione -f al comando.

Per una lista completa delle ozpioni disponibili digitare **mmaker --help**

Questo vi darà un menu piuttosto completo rispetto al software presente nel vostro sistema. Ora è possibile modificare il file di menu a mano, o semplicemente rigenerare la lista ogni volta che si installa un nuovo software.

#### Utilizzando pekwm-menu

Il programma [pekwm-menu](https://aur.archlinux.org/packages/pekwm-menu/), reperibile su AUR, può creare un menu dinamico per le applicazioni, aggiornato in base alle specifiche del freedesktop.org xdg menu. L'uso è abbastanza semplice. Aggiungere una sezione simile alla seguente al vostro file `~/.pekwm/menu`:

```
 Submenu = "Applications" { Icon = "ICON"
   Entry { Actions = "Dynamic pekwm-menu MENUFILE" }
 }

```

Cambia "ICONA " e "MENUFILE" con la vostra icona preferita e file di menu. Il file di menu può essere fornita tramite GNOME, Xfce, LXDE o crearlo personalmente. I file xdg di menu sono normalmente memorizzati in `/etc/xdg/menus`.

Per visualizzare un elenco completo di opzioni , eseguire `pekwm-menu -help`.

#### Modifica manuale

Come già menzionato il file di configurazione del menu è `~/.pekwm/menu`. La sintassi del file è abbastanza semplice ed una voce di menu ha generalmente la seguente struttura:

```
Entry = "NAME" { Actions = "Exec COMMAND &" }

```

Un sotto-menu segue invece la seguente sintassi:

```
Submenu = "NAME" {
     Entry = "NAME" { Actions = "Exec COMMAND &" }
     Entry = "NAME" { Actions = "Exec COMMAND &" }
}

```

(Assicurarsi che queste parentesi siano sempre chiuse, o avrete degli errori ed il menu non verrà visualizzato)

Per aggiungere una linea di separazione al menu, utilizzare la seguente sintassi:

```
Separator {}

```

PekWM può supportare menu dinamici. Queste sono fondamentalmente le voci di menu o sottomenu che visualizzano l'output di uno script che viene eseguito ogni volta che la voce o un sottomenu si seleziona.

Potete trovare alcuni menu dinamici online. Purtroppo non ci sono in giro molti script, e di quelli in circolazione è bene controllare la sintassi esatta, poichè potrebbero variare. Potete trovare menu dinamici per Gmail o le connessioni di rete [qui](http://www.hewphoria.com/?p=submission&type=config), e uno per visuallizzare la date e l'ora qui [qui](http://urukrama.wordpress.com/2008/01/02/show-the-date-and-time-in-pekwms-menu/). Esiste anche un'altro progetto chiamato [pekwm_menu_tools](http://www.pekwm.org/projects/11) che mira a mettere a disposizione una serie di applicazioni utili per la generazione di menu dinamici sotto PekWM.

### Tasti di scelta rapida

Le impostazioni per i tasti di scelta rapida sono memorizzate nel file `~/.pekwm/keys`. Questo file controlla tutte le associazioni della tastiera ed il portachiavi usato in pekwm. È possibile aggiungere delle associazioni a tasti di scelta rapida per avviare programmi o per eseguire azioni in pekwm, come la visualizzazione di un menu, spostare una finestra, spostarsi tra i desktop, ecc. Per una lista completa delle azioni possibili in PekWM vedere [la documentazione](http://www.pekwm.org/files/pekwm/doc/git/html/config/keys_mouse.html#config-keys_mouse-actions).

È possibile avere più di una azione assegnata ad una combinazione di tasti. Per farlo, basta separare le azioni di un punto e virgola. Ecco un esempio:

```
KeyPress = "Ctrl Mod1 R" { Actions = "Exec osdctl -s 'Reconfiguring'; Reload" }

```

Quando si preme Ctrl+Alt+R pekwm visualizzerà sullo schermo il testo 'Riconfigurazione' (osdctl-s 'Riconfigurazione') e ricarica l'istanza (Reload). (Si noti che questo richiede che osdsh sia installato)

Si possono anche "concatenare" i tasti per eseguire delle operazioni, così per esempio il codice:

```
Chain = "Ctrl Mod1 C" {
     KeyPress = "Q" { Actions = "MoveToEdge TopLeft" }
     KeyPress = "W" { Actions = "MoveToEdge TopCenterEdge" }
}

```

Farebbe in modo che se in primo luogo si preme Ctrl+Alt+C e Q si sposta la finestra attiva in alto a sinistra dello schermo, e se si preme Ctrl+Alt+C e poi W si sposta la finestra verso il bordo in alto al centro.

### Mouse

Le impostazoni del mouse sono memorizzate nel file `~/.pekwm/mouse`. Questo file è anche piuttosto auto-esplicativo nel suo layout. Per esempio:

```
FrameTitle {
     ButtonRelease = "1" { Actions = "Raise; Focus" }
}

```

significa che se si rilascia il pulsante 1 (di solito il tasto sinistro del mouse) sul titolo cornice di una finestra della finestra sarà "rialzato" sopra le altre finestre e diventerà la finestra in primo piano.

Una delle impostazioni predefinite di pekwm è quello di concentrare le finestre quando il mouse si sposta su di loro (in contrapposizione al metodo "click per mettere a fuoco"). Questa è una opzione che alcuni utenti vorrebbero cambiare nel "modo più" tradizionale. Per modificare ciò, bisogna cercare le righe inerenti a tali comandi nel file (vi sono più stringhe relative al primo comportamento e solo una in relazione al click per mettere a fuoco) e procedere come descritto.

1.  Rimuovere la riga inerente al comportamento predefinito.
2.  Decommentare quella che ci interessa per attivare il focus della finestra con un click.

### Avvio automatico dei programmi

Puoi aggiungere un programma all'avvio nel file `~/.pekwm/start`. Allo stesso modo si può aggiungere che venga visualizzato uno sfondo , oppure che sia avviato un pannello ogni volta che viene avviato pekwm. In pratica si può avviare qualsiasi cosa, ma queste applicazioni vengono eseguite ogni volta che si avvia pekwm, anche quando si esegue 'Restart' nel menu principale. I comandi vengono eseguiti solo dopo pekwm è avviato.

Per aggiungere una applicazione si aggiunge quanto segue:

```
nameofapplication &

```

La **&** è fondamentale, altrimenti non verranno eseguiti altri comandi successivamente. Di seguito un piccolo esempio di come potrebbe essere strutturato il file in questione:

```
xfce4-panel &
conky &
hsetroot -fill ~/images/darkwood.jpg &

```

Prima di poterlo utilizzare bisogna renderlo eseguibile, ciò si può ottenere con il seguente comando:

```
chmod +x ~/.pekwm/start

```

### Variabii

Le file delle _variabili_ contiene le variabili utilizzate in generale da pekwm, la voce di default dovrebbe spiegarlo abbastanza chiaramente:

```
$TERM="xterm -fn fixed +sb -bg white -fg black"

```

Ogni volta che la variabile $TERM sarà utilizzato in un file di configurazione di PekWM, il comando _xterm -fn fixed +sb -bg white -fg black_ sarà eseguito. Ad esempio , cambiandolo in

```
$TERM="urxvt"

```

significherebbe che urxvt verrà caricato per i comandi da terminale.

### Proprietà automatiche

Se si desidera che alcune applicazioni si avviino in determinate aree di lavoro, con un certo titolo, privi del menu nella finestra, oppure essere automaticamente raggruppati in schede, allora bisogna specificare queste modalità in questo file. È probabilmente il file di configurazione più confuso , ma anche il più potente di PekWM. La quantità di cose che possono essere impostate in questo file è troppo grande per essere descritta in questo wiki, ma è spiegato in dettaglio nella pagina della documentazione ufficiale di [autoproperties](http://www.pekwm.org/files/pekwm/doc/git/html/config/autoprops.html). Il file predefinito `~/.pekwm/autoproperties` contiene anche un corso di autopropping.

## Temi

Alcuni temi possono essere reperiti in rete. Per installare un tema estrarre l'archivio in una cartella dei temi, quelli di default sono:

*   global - /usr/share/pekwm/themes
*   user only - ~/.pekwm/themes

In alternativa è disponibile su [AUR](https://aur.archlinux.org/packages.php?ID=21416) un paccheto contenente alcuni temi già pronti.

### GTK Appearance

Per personalizzare l'aspetto delle applicazioni GTK è possibile utilizzare [LXAppearance](http://www.gnomefiles.org/app.php/LXAppearance) (Reperibile nei repositori).

## Impostare uno sfondo

Poiché pekwm è solo un windows manager è necessario utilizzare un programma separato per impostare uno sfondo del desktop. I programmi più usati a questo scopo sono:

*   [feh](/index.php/Feh "Feh")
*   [Nitrogen](/index.php/Nitrogen "Nitrogen")
*   [xli](https://aur.archlinux.org/packages/xli/)
*   [esetroot](https://aur.archlinux.org/packages/esetroot/)
*   [hsetroot](https://aur.archlinux.org/packages/hsetroot/)
*   [habak](https://www.archlinux.org/packages/?name=habak)

## Problemi comuni

### Quando si utilizza la modalità TwinView di Nvidia, le finestre massimizzate attraversano entrambi gli schermi

Aprire il file `~/.pekwm/config` cercare la linea:

 `HonourRandr = "True"` 

e modificarla in

 `HonourRandr = "False"` 

[Source](https://projects.pekdon.net/projects/pekwm/tasks/124)

### La trasparenza e il composite non funzionano correttamente

Dalla versione v0.1.11, PekWM non sembra supportare correttamente il compositing. Nonostante xcompmgr sia attivo, la trasparenza delle docks e dei pannelli non funzionano, e l'ombreggiatura delle finestre creano artefatti grafici. Una correzione possibile e settare il valore della trasparenza di ogni finestra a .999 (o qualsiasi altro valore) con devilspie e transset-df, in questo modo l'ombra delle finestre vengono visualizzate correttamente.

Di seguito l'esempio di uno script devilspie che imposta la trasparenza di ogni finestra con un valore di .999 tramite _transset-df_:

```
(spawn_async (str "transset-df -i " (window_xid) " .999" ))

```

## Link esterni

*   [Pekwm Homepage](http://pekwm.org/)
*   [gentoo-wiki PekWM page](http://en.gentoo-wiki.com/wiki/PekWM)
*   [Box-Look PekWM Themes](http://box-look.org/index.php?xcontentmode=7403)
*   [Hewphoria PekWM Themes](http://hewphoria.com/?p=submission&type=theme&cat=1)
*   [Freshmeat PekWM Themes](http://themes.freshmeat.net/search/?q=pekwm&section=projects)