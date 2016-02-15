Un window manager (WM) è un componente dell'interfaccia grafica di un sistema (GUI) ad uso dell'utente. Molti potrebbero preferire l'installazione di un vero e proprio [Desktop environment](/index.php/Desktop_environment "Desktop environment"), che offre un'interfaccia utente completa, comprese icone, finestre, barre degli strumenti, sfondi e widget per il desktop.

## Contents

*   [1 X Window System](#X_Window_System)
*   [2 Window manager](#Window_manager)
    *   [2.1 Tipi](#Tipi)
    *   [2.2 Confronto tra gestori di finestre](#Confronto_tra_gestori_di_finestre)
    *   [2.3 Elenco dei gestori di finestre](#Elenco_dei_gestori_di_finestre)

## X Window System

Il [sistema X Window](https://en.wikipedia.org/wiki/X_Window_System "wikipedia:X Window System") fornisce le basi per un'interfaccia utente grafica. Prima di installare un gestore di finestre, è necessaria l'installazione di un server X funzionante. Vedere [Xorg](/index.php/Xorg_(Italiano) "Xorg (Italiano)") per informazioni più dettagliate.

	_X fornisce il quadro di base per la configurazione di tali ambienti GUI: disegnare e muovere le finestre sullo schermo e interagire con il mouse e la tastiera. Non ha competenze specifiche per l'interfaccia utente; saranno i programmi dei singoli client, noti come "window manager" ad occuparsi della gestione di tutto questo. Come tale, lo stile visivo degli ambienti basati su X può variare molto: differenti tipi di programmi possono presentare interfacce radicalmente molto diverse. X è costruito come una ulteriore applicazione (a livello di astrazione), al di sopra del kernel del sistema operativo._

L'utente è libero di configurare il proprio ambiente GUI in molti modi.

## Window manager

I Window Manager (WM) sono client per X che forniscono il bordo intorno ad una finestra. Controllano l'aspetto delle applicazioni e il modo in cui gestirle: il bordo, barra del titolo, la dimensione e la capacità di ridimensionare una finestra; sono tutte funzionalità gestite dai Window manager. Molti window manager forniscono altre funzionalità, quali le [dockapps](http://www.dockapps.org), come [Window Maker](/index.php/Window_Maker_(Italiano) "Window Maker (Italiano)"), un menu per avviare i programmi, i menu per configurare il WM e altre cose utili. [Fluxbox](/index.php/Fluxbox_(Italiano) "Fluxbox (Italiano)"), per esempio, fornisce la funzione "tab" per le finestre.

I window manager in genere non offrono gli _extra_ come le icone del desktop, che sono così comuni nei [desktop environment](/index.php/Desktop_environment "Desktop environment") (anche se è possibile aggiungere le icone in un WM con un altro programma).

E proprio grazie della mancanza di tali _extra_, i WM sono molto più leggeri per quanto riguarda le risorse del sistema.

### Tipi

*   I window manager **Stacking** (o "floating") forniscono l'analoga funzionalità della scrivania tradizionale usata nei sistemi operativi commerciali come Windows e OS X. Gestiscono le finestre come pezzi di carta su una scrivania, e possono essere sovrapposte le une sopra le altre.
*   I window manager **Tiling** "affiancano" le finestre in modo che non si sovrappongano. Di solito fanno un uso molto esteso di scorciatoie da tastiera e sono meno (se non del tutto) dipendenti dal mouse. In genere devono essere configurati manualmente, anche se talvolta vengono forniti con delle impostazioni predefinite.
*   I window manager **Dinamici** possono essere dinamicamente cambiati tra layout "tiling" e "floating".

*   [Category:Stacking WMs](/index.php/Category:Stacking_WMs "Category:Stacking WMs")
*   [Category:Tiling WMs](/index.php/Category:Tiling_WMs "Category:Tiling WMs")
*   [Category:Dynamic WMs](/index.php/Category:Dynamic_WMs "Category:Dynamic WMs")

### Confronto tra gestori di finestre

Consultare [Comparison of tiling window managers](/index.php/Comparison_of_tiling_window_managers "Comparison of tiling window managers") e [Wikipedia:Comparison of X window managers](https://en.wikipedia.org/wiki/Comparison_of_X_window_managers "wikipedia:Comparison of X window managers").

### Elenco dei gestori di finestre

<center>**Stacking WMs**</center>

**aewm** — aewm è un moderno window manager minimale per X11\. Controllabile interamente con il mouse, non contiene alcuna interfaccia salvo quella delle finestre. Il set di comandi è una sorta di Vi: progettato tempo addietro, nel 1997, per favorire le macchine con poche risorse, molto poco intuituivo ed ostile ai principianti, ma veloce ed elegante a suo modo.

	[http://www.red-bean.com/decklin/aewm/](http://www.red-bean.com/decklin/aewm/) || [aewm](https://aur.archlinux.org/packages/aewm/) [unsupported]

**[AfterStep](https://en.wikipedia.org/wiki/AfterStep "wikipedia:AfterStep")** — AfterStep è un window manager per l'X Window System Unix. Originariamente basato sul look and feel dell'interfaccia NeXTStep, fornisce agli utenti finali un desktop coerente, pulito ed elegante. L'obiettivo di sviluppo AfterStep è quello di fornire la flessibilità di configurazione del desktop, il miglioramento estetico, e un uso efficiente delle risorse di sistema.

	[http://www.afterstep.org/](http://www.afterstep.org/) || [afterstep](https://aur.archlinux.org/packages/afterstep/) [unsupported]

**[Blackbox](https://en.wikipedia.org/wiki/Blackbox "wikipedia:Blackbox")** — Blackbox è tra i più veloci e leggeri window manager per X che ci si possa immaginare, senza tutte quelle fastidiose dipendenze dalle librerie. Blackbox è compilato in C + + e contiene tutto il codice originale (anche se la realizzazione grafica è simile a quella di WindowMaker).

	[http://blackboxwm.sourceforge.net/](http://blackboxwm.sourceforge.net/) || [blackbox](https://www.archlinux.org/packages/?name=blackbox)

**[Compiz](/index.php/Compiz_(Italiano) "Compiz (Italiano)")** — Compiz è un compositing manager OpenGL che utilizza GLX_EXT_texture_from_pixmap per l'associazione di primo livello delle finestre alla texture degli oggetti. Ha un flessibile sistema di plug-in ed è progettato per funzionare bene sulla maggior parte dell'hardware grafico.

	[http://www.compiz.org/](http://www.compiz.org/) || [compiz-core](https://aur.archlinux.org/packages/compiz-core/)

**[Enlightenment](/index.php/Enlightenment_(Italiano) "Enlightenment (Italiano)")** — Enlightenment non è solo un window manager per Linux/X11 e altri, ma anche una intera suite di librerie che consentono di creare interfacce utente molto carine con molto meno lavoro rispetto al metodo tradizionale.

	[http://www.enlightenment.org/](http://www.enlightenment.org/) || [enlightenment](https://www.archlinux.org/packages/?name=enlightenment)

**[evilwm](/index.php/Evilwm_(Italiano) "Evilwm (Italiano)")** — Un window manager minimalista per l'X Window System. Minimalista in questo caso non significa che sia troppo scarno per essere utilizzabile, significa solo che omette un sacco di cose che rendono altri window manager "usabili".

	[http://www.6809.org.uk/evilwm/](http://www.6809.org.uk/evilwm/) || [evilwm](https://aur.archlinux.org/packages/evilwm/)

**Firebox** — Firebox è ancora un altro Window Manager per sistemi X11\. Ancora in sviluppo, non è un "fork" di Openbox, Fluxbox, Blackbox o addirittura di Hackedbox; è scritto da zero, in linguaggio C.

	[http://firebox.intuxication.org/](http://firebox.intuxication.org/) || [firebox](https://aur.archlinux.org/packages/firebox/) [unsupported]

**[Fluxbox](/index.php/Fluxbox_(Italiano) "Fluxbox (Italiano)")** — Fluxbox è un window manager per X che si basa sul codice di Blackbox 0.61.1\. È molto leggero in quanto a risorse, facilmente gestibile, ma comunque pieno di quelle caratteristiche che permettono di allestire un sistema desktop veloce ed estremamente completo. È compilato in C + + e rilasciato sotto licenza MIT.

	[http://www.fluxbox.org/](http://www.fluxbox.org/) || [fluxbox](https://www.archlinux.org/packages/?name=fluxbox)

**[Flwm](https://en.wikipedia.org/wiki/FLWM "wikipedia:FLWM")** — Flwm è un tentativo di combinare insieme le migliori idee osservate in diversi altri window manager. L'influenza principale e il codice di base di provengono da wm2, di Chris Cannam.

	[http://flwm.sourceforge.net/](http://flwm.sourceforge.net/) || [flwm](https://aur.archlinux.org/packages/flwm/) [unsupported]

**[FVWM](/index.php/FVWM_(Italiano) "FVWM (Italiano)")** — FVWM è un window manager estremamente potente, compatibile con ICCCM, desktop virtuali multipli, per il sistema X Window. Lo sviluppo è attivo, e il supporto è eccellente.

	[http://www.fvwm.org/](http://www.fvwm.org/) || [fvwm](https://www.archlinux.org/packages/?name=fvwm)

**[Hackedbox](https://en.wikipedia.org/wiki/Hackedbox "wikipedia:Hackedbox")** — Hackedbox è una versione ridotta di Blackbox, il window manager di X. La barra degli strumenti e lo Slit ono stati rimossi. L'obiettivo di Hackedbox è di essere un piccolo "feature-set" window manager, senza eccessive pomposità. Non sono previste aggiunte future di nuove funzionalità, solo bugfix e miglioramenti prestazionali, quando possibile.

	[http://scrudgeware.org/projects/Hackedbox/](http://scrudgeware.org/projects/Hackedbox/) || [hackedbox](https://aur.archlinux.org/packages/hackedbox/) [unsupported]

**[IceWM](/index.php/IceWM_(Italiano) "IceWM (Italiano)")** — IceWM è un window manager per X Window System. L'obiettivo di IceWM è la velocità, semplicità, e non necessariamente la facilità nel senso "dell'utente".

	[http://www.icewm.org/](http://www.icewm.org/) || [icewm](https://www.archlinux.org/packages/?name=icewm)

**[JWM](/index.php/JWM_(Italiano) "JWM (Italiano)")** — JWM è un window manager per l'X11 Window System. JWM è scritto in C e usa solo un minimo di Xlib.

	[http://joewing.net/programs/jwm/](http://joewing.net/programs/jwm/) || [jwm](https://www.archlinux.org/packages/?name=jwm)

**Karmen** — Karmen è un window manager per X, scritto da Johan Veenhuizen. Progettato per "funzionare!" Non c'è un file di configurazione ne dipendenze da librerie eccetto Xlib. Il focus del modello input è click-to-focus. Karmen punta ad essere compatibile con ICCCM e EWMH.

	[http://karmen.sourceforge.net/](http://karmen.sourceforge.net/) || [karmen](https://aur.archlinux.org/packages/karmen/) [unsupported]

**[KWin](https://en.wikipedia.org/wiki/KWin "wikipedia:KWin")** — KWin, il gestore di finestre KDE standard in KDE 4.0, fornito con la prima versione di supporto integrato per la composizione, lo rende anche un compositing manager. Questo permette a KWin di fornire effetti grafici avanzati, simili a Compiz, fornendo nel contempo tutte le caratteristiche delle precedenti versioni di KDE (come una buona integrazione con il resto di KDE, configurabilità avanzata, la prevenzione del focus, un window manager ben testato, manipolazione del comportamento anomalo di applicazioni/toolkit, ecc.).

	[http://techbase.kde.org/Projects/KWin](http://techbase.kde.org/Projects/KWin) || [kdebase-workspace](https://aur.archlinux.org/packages/kdebase-workspace/)

**[lwm](https://en.wikipedia.org/wiki/Lightweight_window_manager "wikipedia:Lightweight window manager")** — lwm è un window manager per X che cerca di mantenersi completamente fuori dai piedi! Non ci sono icone, ne barre ne pulsanti, nessun menu principale, niente di niente: se si desiderano queste cose, bisognerà rivolgersi verso altri programmi che le possano offrire. Non c'è nemmeno una opzione di configurabilità: se la si vuole, bisognerà scegliere un window manager diverso: uno che aiuti il sistema operativo ad aumentare lo spazio occupato su disco e la memoria fisica occupata!

	[http://www.jfc.org.uk/software/lwm.html](http://www.jfc.org.uk/software/lwm.html) || [lwm](https://www.archlinux.org/packages/?name=lwm)

**[Metacity](https://en.wikipedia.org/wiki/Metacity "wikipedia:Metacity")** — Questa non è la home page di Metacity. Non vi è alcun home page Metacity. Questo è per la stessa ragione per cui non vi è alcun logo appariscente: Metacity si sforza di essere invisibile, di dimensioni contenute, stabile, di eseguire il proprio lavoro, e non disturbare l'utente.

	[http://blogs.gnome.org/metacity/](http://blogs.gnome.org/metacity/) || [metacity](https://www.archlinux.org/packages/?name=metacity)

**[Openbox](/index.php/Openbox_(Italiano) "Openbox (Italiano)")** — Openbox è un window manager di ultima generazione, altamente configurabile, con un ampio supporto standard. Lo stile visivo *box è ben noto per il suo aspetto minimalista. Utilizza lo stile *box, pur fornendo un numero maggiore di opzioni per gli sviluppatori di temi in confronto alle implementazioni precedenti. La documentazione dei temi descrive la gamma completa delle opzioni disponibili nei temi di Openbox.

	[http://openbox.org/wiki/Main_Page](http://openbox.org/wiki/Main_Page) || [openbox](https://www.archlinux.org/packages/?name=openbox)

**[Pawm](/index.php/Pawm_(Italiano) "Pawm (Italiano)")** — Pawm Pawm è un window manager per il sistema X Window. Quindi non è un "desktop" e non offre un mucchio enorme di opzioni inutili, solo i servizi necessari per eseguire le applicazioni X e allo stesso tempo, avere un'interfaccia amichevole e facile da usare.

	[http://www.pleyades.net/pawm/](http://www.pleyades.net/pawm/) || [pawm](https://www.archlinux.org/packages/?name=pawm)

**[pekwm](/index.php/PekWM_(Italiano) "PekWM (Italiano)")** — pekwm è un window manager che un tempo era basato sul WM aewm++. Causa le modifiche applicate con il passare del tempo, non assomiglia più molto a aewm++. Ha un esteso insieme di caratteristiche, tra cui il raggruppamento delle finestre (simili a Ion, PWM, o Fluxbox), auto-proprietà, Xinerama, keygrabber, che supporta le gestioni portachiavi, e molto altro.

	[http://www.pekwm.org/projects/pekwm](http://www.pekwm.org/projects/pekwm) || [pekwm](https://www.archlinux.org/packages/?name=pekwm)

**[Sawfish](/index.php/Sawfish "Sawfish")** — Sawfish è un window manager espandibile che usa un linguaggio di scripting basato su Lisp. La sua politica è molto minimale rispetto alla maggior parte dei window manager. Il suo scopo è semplicemente quello di gestire le finestre nel modo più flessibile ed attraente. Tutte le funzioni di livello elevato di WM sono implementate in Lisp per eventuali espandibilità o ridefinizioni future.

	[http://sawfish.wikia.com/wiki/Main_Page](http://sawfish.wikia.com/wiki/Main_Page) || [sawfish](https://aur.archlinux.org/packages/sawfish/)

**TinyWM** — TinyWM è un gestore di finestra molto ridotto, creato come un esercizio di minimalismo. Può inoltre essere utile per imparare alcune delle basi per la creazione di un gestore di finestre. È composto da sole 50 righe circa di C. Esiste anche una versione di Python che utilizza python-Xlib.

	[http://incise.org/tinywm.html](http://incise.org/tinywm.html) || [tinywm](https://aur.archlinux.org/packages/tinywm/) [unsupported]

**[twm](/index.php/Twm_(Italiano) "Twm (Italiano)")** — Twm è un window manager per l'X Window System. Fornisce la barra del titolo, finestre ridimensionabili, gestione per iconizzare le finestre, macro per le funzioni definite dall'utente, clic per la messa a fuoco, personalizzazione del comportamento del mouse, di tasti di scelta rapida e del menu.

	[http://cgit.freedesktop.org/xorg/app/twm/](http://cgit.freedesktop.org/xorg/app/twm/) || [xorg-twm](https://www.archlinux.org/packages/?name=xorg-twm)

**WindowLab** — WindowLab è un window manager piccolo e semplice di nuovo design. Orienta le funzionalità del puntatore del mouse al clic per la messa a fuoco, ma non per il sollevamento del focus, un meccanismo di ridimensionamento delle finestre, che consente di modificare uno o più margini delle finestre in una sola azione, e una innovativa barra dei menu che condivide la stessa parte dello schermo con la barra delle applicazioni. Alle barre dei titoli delle finestre viene impedito di andare oltre il bordo dello schermo, limitando il puntatore del mouse, a cui eventualmente si possono vincolare anche la barra delle applicazioni e dei menu, in modo da renderle più facili da selezionare.

	[http://nickgravgaard.com/windowlab/](http://nickgravgaard.com/windowlab/) || [windowlab](https://www.archlinux.org/packages/?name=windowlab)

**[Window Maker](/index.php/Window_Maker_(Italiano) "Window Maker (Italiano)")** — Window Maker è un window manager per X11 originariamente progettato per fornire supporto di integrazione per il Desktop Environment GNUstep. Riproduce il più possibile l'aspetto elegante e dell'interfaccia utente NeXTSTEP. È veloce, ricco di funzionalità, facile da configurare e da usare. È totalmente "free software", con contributi da programmatori di tutto il mondo.

	[http://windowmaker.org/](http://windowmaker.org/) || [windowmaker](https://www.archlinux.org/packages/?name=windowmaker)

**Xfwm** — Il window manager di Xfce gestisce il posizionamento delle finestre delle applicazioni sullo schermo, offre belle decorazioni alle finestre, gestisce le aree di lavoro o dei desktop virtuali e supporta nativamente la modalità multischermo. Fornisce il proprio compositing manager (dall'estensione X. Org Composite) per la trasparenza vera e le ombre. Il window manager di Xfce comprende anche un editor di scorciatoie da tastiera per i comandi specifici dell'utente e manipolazioni di base delle finestre, includendo inoltre una finestra di dialogo per le preferenze delle modifiche avanzate.

	[http://www.xfce.org/projects/xfwm4/](http://www.xfce.org/projects/xfwm4/) || [xfwm4](https://www.archlinux.org/packages/?name=xfwm4)

<center>**Tiling window managers**</center>

**[dswm](/index.php?title=Dswm&action=edit&redlink=1 "Dswm (page does not exist)")** — dswm(Deep Space Window Manager) è un derivato di [Stumpwm](/index.php/Stumpwm "Stumpwm")

	[https://github.com/dss-project/dswm](https://github.com/dss-project/dswm) || [dswm](https://aur.archlinux.org/packages/dswm/) [unsupported]

**[euclid-wm](/index.php?title=Euclid-wm&action=edit&redlink=1 "Euclid-wm (page does not exist)")** — euclid-wm è un semplice e leggero gestore delle finestre per X11 con funzionalità di tiling e floating, con il supporto per la minimizzazione delle finestre. Un file di testo contiene le configurazioni per le scorciatoie della tastiera e per le impostazioni. Inizialmente nato come fork di dwm con una facile configurazione, è diventato un completo gestore delle finestre con supporto EWMH. Ha una barra/pannello delle applicazioni EWMH-compatibile chiamata [ourico](https://aur.archlinux.org/packages/ourico/).

	[http://euclid-wm.sourceforge.net/index.php](http://euclid-wm.sourceforge.net/index.php) || [euclid-wm](https://aur.archlinux.org/packages/euclid-wm/) [unsupported]

**[Herbstluftwm](/index.php/Herbstluftwm "Herbstluftwm")** — herbstluftwm un manuale tiling window manager per X11 che utilizza Xlib e Glib. Il layout è basato su frames che si dividono in subframe, che può essere diviso ancora una volta o possono essere riempiti con le finestre (simile a i3/MUSCA). Tag (o area di lavoro o di desktop virtuali) può essere aggiunto/rimosso al volo. Ogni tag contiene un layout proprio. Esattamente un tag viene visualizzato su ogni monitor. I tag sono indipendenti dal monitor (simile a xmonad). E sono configurati da herbstclient in runtime tramite chiamate IPC . Quindi il file di configurazione è solo uno script che viene eseguito all'avvio. (simile a wmii/ musca)

	[http://wwwcip.cs.fau.de/~re06huxa/herbstluftwm](http://wwwcip.cs.fau.de/~re06huxa/herbstluftwm) || [herbstluftwm-git](https://aur.archlinux.org/packages/herbstluftwm-git/) [unsupported]

**[i3](/index.php/I3 "I3")** — i3 è un tiling window manager, completamente scritto da zero. i3 è stato creato perché wmii, il nostro window manager preferito, al momento, non ha fornito alcune caratteristiche che volevamo (multi-monitor per esempio) alcuni bugs, pochi progressi nel corso del tempo e varie difficoltà per migliorarlo (commenti del codice sorgente/documentazione completamente assente). Notevoli differenze sono nelle aree di supporto multi-monitor e della distribuzione ad albero. Per velocizzare l'interfaccia Plane9 di wmii non sono implementati.

	[http://i3.zekjur.net/](http://i3.zekjur.net/) || [i3-wm](https://www.archlinux.org/packages/?name=i3-wm)

**[Ion3](/index.php/Ion3 "Ion3")** — Ion è un tiling window manager per X11 progettato pensando alle tastiere degli utenti. È stato uno dei primi della "nuova ondata" tra gli ambienti "tiling window" (l'altro è stato LarsWM, ma con un approccio piuttosto diverso) e da allora ha generato tutta una categoria di tiling window manager per X11 – nessuno dei quali però, è riuscito a riprodurre "l'appeal" e la funzionalità di Ion. Utilizza Lua come interprete integrato che gestisce tutta la configurazione.

	[http://tuomov.iki.fi/software](http://tuomov.iki.fi/software) || [ion3](https://aur.archlinux.org/packages/ion3/) [unsupported]

**[Musca](/index.php/Musca "Musca")** — Un gestore di finestre semplice e dinamico per X, con caratteristiche prese da ratpoison e dwm. Musca funziona come un gestore di finestre tilling di default. L'utente determina come lo schermo è diviso in frame non sovrapposti, senza restrizioni sul layout. Le finestre delle applicazioni riempono sempre il frame assegnato, ad eccezione delle finestre transitorie e le finestre di dialogo che galleggiano sopra la loro applicazione principale con le dimensioni appropriate. Una volta visibile, le applicazioni non cambiano il frame a meno di non farlo manualmente.

	[http://aerosuidae.net/musca/](http://aerosuidae.net/musca/) || [musca](https://aur.archlinux.org/packages/musca/)

**[Notion](/index.php/Notion "Notion")** — Notion + un gestore delle finestre con funzionalità di tiling, tabbed per il sistema di finestre di X che utilizza finestre a 'piastrelle' e 'schede'.

*   Tiling: si divide lo schermo in 'piastrelle' non sovrapposte . Ogni finestra occupa una piastrella, e in esso viene massimizzata
*   Tabbing: Una piastrella può contenere più finestre - Esse appariranno come 'Schede'
*   Statico: moli gestori di finestre con funzionalità di tilling (piastrelle) sono 'dinamiche', nel senso che si ridimensionano e si spostano automaticamente tra le piastrelle ogni volta che una finestra appare o scompare. Notion, al contrario, non effettua questi cambiamenti automatici.

Notion è un fork di Ion3.

	[http://notion.sf.net/](http://notion.sf.net/) || [notion](https://www.archlinux.org/packages/?name=notion)

**[Ratpoison](/index.php/Ratpoison "Ratpoison")** — Ratpoison è un semplicissimo window manager senza alcuna dipendenza da ingombranti librerie, senza elementi grafici fantasiosi, senza decorazioni per le finestre, e senza nessuna dipendenza parassita. È in gran parte modellato da "GNU Screen", che ha fatto meraviglie nel mercato dei terminali virtuali. Ratpoison è configurato con un semplice file di testo. La barra delle informazioni in Ratpoison è leggermente diversa, in quanto mostra solo quando necessario. Serve sia come application launcher che come una barra di notifica. Ratpoison non include un vassoio di sistema.

	[http://www.nongnu.org/ratpoison/](http://www.nongnu.org/ratpoison/) || [ratpoison](https://www.archlinux.org/packages/?name=ratpoison)

**[Stumpwm](/index.php/Stumpwm "Stumpwm")** — Stumpwm è un tiling window manager per X11, orientato all'uso della tastiera. Interamente scritto in Common Lisp, stumpwm cerca di essere minimamente personalizzabile in senso visuale. Non ci sono decorazioni di finestre, non le icone, e nessun tasto. Fornisce vari hooks per le proprie personalizzazioni, e variabili di ottimizzazione.

	[http://www.nongnu.org/stumpwm/](http://www.nongnu.org/stumpwm/) || [stumpwm-git](https://aur.archlinux.org/packages/stumpwm-git/) [unsupported]

**[subtle](/index.php/Subtle "Subtle")** — subtle è un "tiling window manager" manuale con un approccio piuttosto raro di tiling: Per default non c'è il tipico layout d'esecuzione, le finestre sono posizionate in alcun punto (gravità) di una griglia personalizzata. Si può cambiare la gravità di ogni finestra direttamente o per mezzo di regole definite dai tags nella configurazione. Ha i tag di lavoro e il tagging automatico dei client, controllo di mouse e tastiera, nonché una barra di stato estensibile.

	[http://subforge.org/projects/subtle](http://subforge.org/projects/subtle) || [subtle](https://aur.archlinux.org/packages/subtle/) [unsupported]

**[WMFS](/index.php/WMFS "WMFS")** — WMFS (Window Manager From Scratch) è un "tiling window manager", leggero ed altamente configurabile per X. Può essere configurato con un file di configurazione, supporta i caratteri Xft (FreeType) ed è compatibile con la (EWMH), specifiche estese per il gestore finestre, Xinerama e xrandr. WMFS può essere gestito con i comandi (basati su Vi) ViWMFS.

	[http://wmfs.info/projects/wmfs](http://wmfs.info/projects/wmfs) || [wmfs](https://aur.archlinux.org/packages/wmfs/) [unsupported]

**[wmii](/index.php/Wmii "Wmii")** — wmii è un piccolo window manager dinamico per X11\. Supporta gli script, ha un interfaccia filesystem 9P e supporta la gestione delle finestre sia "classic" che "tiling" (Acme-like). Punta a mantenere un codice di base contenuto e pulito. La configurazione di default è in bash e [rc (la shell Plan 9)](http://rc.cat-v.org), ma esistono programmi scritti in Ruby, e qualsiasi programma in grado di lavorare con il testo può essere configurato. Ha una barra di stato, un launcher integrato, ed anche un vassoio di sistema opzionale (`witray`).

	[http://wmii.suckless.org/](http://wmii.suckless.org/) || [wmii](https://www.archlinux.org/packages/?name=wmii)

<center>**Dynamic window managers**</center>

**[awesome](/index.php/Awesome_(Italiano) "Awesome (Italiano)")** — awesome è un window manager di ultima generazione altamente configurabile per il server X. È molto veloce, espandibile e concesso su licenza GNU GPLv2\. È principalmente destinato agli utenti avanzati, gli sviluppatori e le persone quotidianamente a contatto con ogni attività di elaborazione che vogliono avere un controllo molto "fine" sul loro ambiente grafico. Configurato in Lua, ha un vassoio di sistema, la barra informazioni e lanciatore di applicazioni compilati in esso. Ci sono estensioni disponibili per averlo scritto in Lua. Awesome usa xcb al posto di Xlib, che può causare un aumento di velocità. Awesome ha anche altre caratteristiche, come un demone per le notifiche di sistema, un menu sul tasto destro del mouse menu simile a quello dei windows manager *box, e molte altre cose.

	[http://awesome.naquadah.org/](http://awesome.naquadah.org/) || [awesome](https://www.archlinux.org/packages/?name=awesome) [unsupported]

**[catwm](/index.php/Catwm "Catwm")** — catwm è un piccolo gestore delle finestre, anche più semplice di dwm, e scritto in C. Una volta configurato modificando il file config.h file deve essere ricompilato.

	[https://github.com/pyknite/catwm](https://github.com/pyknite/catwm) || [catwm-git](https://aur.archlinux.org/packages/catwm-git/) [unsupported]

**[dwm](/index.php/Dwm "Dwm")** — dwm è un window manager dinamico per X. Gestisce il layout delle finestre in stile floating e tiling. Tutti i layout possono essere applicati in modo dinamico, ottimizzando l'ambiente per l'applicazione in uso e le operazioni svolte. Non include un vassoio delle applicazioni o un lanciatore automatico, anche se dmenu si integra bene con esso, in quanto sono dello stesso autore. Non ha un file di testo. La configurazione viene fatta interamente modificando il codice sorgente in C, e deve essere ricompilato e riavviato ogni volta che viene cambiato. La dimensione del programma è già al limite di linea autoimposto , limitandone un ulteriore sviluppo.

	[http://dwm.suckless.org/](http://dwm.suckless.org/) || [dwm](https://www.archlinux.org/packages/?name=dwm)

**[echinus](/index.php/Echinus "Echinus")** — Semplice e leggero "tiling e floating" window manager per X11\. Iniziato come un "fork" di dwm con una maggiore facilità di configurazione, echinus è diventato un window manager full-optional con supporto a EWMH.

	[http://plhk.ru/echinus](http://plhk.ru/echinus) || [echinus](https://aur.archlinux.org/packages/echinus/) [unsupported]

**[spectrwm](/index.php/Spectrwm "Spectrwm")** — spectrwm è un piccolo e dinamico tiling window manager per X11\. Il suo scopo è quello di rimanere "in secondo piano", in modo che il prezioso spazio sullo schermo possa essere utilizzato per cose molto più importanti. Ha valori predefiniti piuttosto semplici, e non richiede l'apprendimento di un linguaggio per fare qualsiasi configurazione. È stato scritto dagli hacker per gli hacker, e si sforza di essere piccolo, compatto e veloce.

	[https://github.com/conformal/spectrwm/wiki](https://github.com/conformal/spectrwm/wiki) || [spectrwm](https://www.archlinux.org/packages/?name=spectrwm)

**[xmonad](/index.php/Xmonad "Xmonad")** — xmonad è un tiling window manager dinamico che è scritto e configurato in Haskell. In un WM normale, si spende la metà del proprio tempo allineando e cercando le finestre. xmonad rende il lavoro più facile, grazie all'automazione di quest'ultima caratteristica. Ad ogni cambiamento di configurazione, xmonad deve essere ricompilato, quindi il compilatore Haskell deve essere installato (occupa 485MB). Una libreria estesa chiamata [xmonad-contrib](https://www.archlinux.org/packages/?name=xmonad-contrib) fornisce molte caratteristiche aggiuntive

	[http://xmonad.org/](http://xmonad.org/) || [xmonad](https://www.archlinux.org/packages/?name=xmonad)