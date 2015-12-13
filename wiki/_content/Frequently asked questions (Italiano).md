# Frequently asked questions (Italiano)

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

Oltre alle domande seguenti, è possibile trovare utile leggere gli articoli [Il Metodo Arch](/index.php/Il_Metodo_Arch "Il Metodo Arch") e [Arch Linux](/index.php/Arch_Linux_(Italiano) "Arch Linux (Italiano)"). Entrambi contengono molte utili informazioni su Arch Linux.

## Contents

*   [1 Generale](#Generale)
    *   [1.1 D) Cos'è Arch Linux?](#D.29_Cos.27.C3.A8_Arch_Linux.3F)
    *   [1.2 D) Perchè si dovrebbe voler utilizzare Arch Linux?](#D.29_Perch.C3.A8_si_dovrebbe_voler_utilizzare_Arch_Linux.3F)
    *   [1.3 D) Perchè non si dovrebbe voler utilizzare Arch Linux?](#D.29_Perch.C3.A8_non_si_dovrebbe_voler_utilizzare_Arch_Linux.3F)
    *   [1.4 D) Su quale distribuzione GNU/Linux si basa Arch Linux?](#D.29_Su_quale_distribuzione_GNU.2FLinux_si_basa_Arch_Linux.3F)
    *   [1.5 D) Sono alle prime armi con Linux. Dovrei usare Arch Linux?](#D.29_Sono_alle_prime_armi_con_Linux._Dovrei_usare_Arch_Linux.3F)
    *   [1.6 D) Arch Linux richiede troppo tempo e troppi sforzi per l'installazione e l'uso. In più la comunità continua a dirmi: "leggi la wiki!" (o RTFM)](#D.29_Arch_Linux_richiede_troppo_tempo_e_troppi_sforzi_per_l.27installazione_e_l.27uso._In_pi.C3.B9_la_comunit.C3.A0_continua_a_dirmi:_.22leggi_la_wiki.21.22_.28o_RTFM.29)
    *   [1.7 D) Arch è più adatta a server, desktop o workstation?](#D.29_Arch_.C3.A8_pi.C3.B9_adatta_a_server.2C_desktop_o_workstation.3F)
    *   [1.8 D) Mi piace molto Arch, ma a mio parere i dev dovrebbero aggiungere la _funzionalità X_.](#D.29_Mi_piace_molto_Arch.2C_ma_a_mio_parere_i_dev_dovrebbero_aggiungere_la_funzionalit.C3.A0_X.)
    *   [1.9 D) Quando uscirà il prossimo rilascio ufficiale?](#D.29_Quando_uscir.C3.A0_il_prossimo_rilascio_ufficiale.3F)
    *   [1.10 D)Arch è un sistema operativo stabile? Avrò frequentemente problemi](#D.29Arch_.C3.A8_un_sistema_operativo_stabile.3F_Avr.C3.B2_frequentemente_problemi)
    *   [1.11 D) Cos'è esattamente questo sistema di init 'BSD-style' di cui ho sentito parlare?](#D.29_Cos.27.C3.A8_esattamente_questo_sistema_di_init_.27BSD-style.27_di_cui_ho_sentito_parlare.3F)
    *   [1.12 D) Arch ha bisogno di più pubblicità](#D.29_Arch_ha_bisogno_di_pi.C3.B9_pubblicit.C3.A0)
    *   [1.13 D) Arch ha bisogno di più sviluppatori](#D.29_Arch_ha_bisogno_di_pi.C3.B9_sviluppatori)
    *   [1.14 D) Perchè Arch è così lenta? Pensavo fosse veloce!](#D.29_Perch.C3.A8_Arch_.C3.A8_cos.C3.AC_lenta.3F_Pensavo_fosse_veloce.21)
    *   [1.15 D)Perchè Internet è così lento in confronto ad altri sistemi operativi?](#D.29Perch.C3.A8_Internet_.C3.A8_cos.C3.AC_lento_in_confronto_ad_altri_sistemi_operativi.3F)
    *   [1.16 D) Perchè Arch utilizza tutta la mia RAM?](#D.29_Perch.C3.A8_Arch_utilizza_tutta_la_mia_RAM.3F)
    *   [1.17 D) Dov'è finito tutto il mio spazio libero?](#D.29_Dov.27.C3.A8_finito_tutto_il_mio_spazio_libero.3F)
*   [2 Gestione Pacchetti](#Gestione_Pacchetti)
    *   [2.1 D)Il pacchetto X in quale è contenuto?](#D.29Il_pacchetto_X_in_quale_.C3.A8_contenuto.3F)
    *   [2.2 D) Ho trovato un errore nel pacchetto X. Che dovrei fare?](#D.29_Ho_trovato_un_errore_nel_pacchetto_X._Che_dovrei_fare.3F)
    *   [2.3 D) I pacchetti di Arch hanno bisogno di usare un'unica estensione. .pkg.tar.gz e .pkg.tar.xz sono troppo lunghe e/o poco chiare](#D.29_I_pacchetti_di_Arch_hanno_bisogno_di_usare_un.27unica_estensione._.pkg.tar.gz_e_.pkg.tar.xz_sono_troppo_lunghe_e.2Fo_poco_chiare)
    *   [2.4 D) Pacman ha bisogno di una libreria così che le altre applicazioni possano facilmente accedere alle informazioni sui pacchetti](#D.29_Pacman_ha_bisogno_di_una_libreria_cos.C3.AC_che_le_altre_applicazioni_possano_facilmente_accedere_alle_informazioni_sui_pacchetti)
    *   [2.5 D) Perchè pacman non ha un front end grafico (GUI)?](#D.29_Perch.C3.A8_pacman_non_ha_un_front_end_grafico_.28GUI.29.3F)
    *   [2.6 D) Pacman ha bisogno della _caratteristica X!_](#D.29_Pacman_ha_bisogno_della_caratteristica_X.21)
    *   [2.7 D) Arch ha bisogno di una versione stable](#D.29_Arch_ha_bisogno_di_una_versione_stable)
    *   [2.8 D) Qual è la differenza fra tutti questi repository?](#D.29_Qual_.C3.A8_la_differenza_fra_tutti_questi_repository.3F)
    *   [2.9 D) Ho appena installato il pacchetto X. Come lo avvio?](#D.29_Ho_appena_installato_il_pacchetto_X._Come_lo_avvio.3F)
    *   [2.10 D) Perchè nei repositories c'è solo una versione per ogni libreria?](#D.29_Perch.C3.A8_nei_repositories_c.27.C3.A8_solo_una_versione_per_ogni_libreria.3F)
    *   [2.11 D) Cosa succede se aggiornando il sistema ricevo aggiornamenti per una libreria e non per le sue dipendenze?](#D.29_Cosa_succede_se_aggiornando_il_sistema_ricevo_aggiornamenti_per_una_libreria_e_non_per_le_sue_dipendenze.3F)
    *   [2.12 D) È possibile che ci sia un aggiornamento di versione del kernel e al tempo stesso non ci sia un aggiornamento adeguato dei drivers?](#D.29_.C3.88_possibile_che_ci_sia_un_aggiornamento_di_versione_del_kernel_e_al_tempo_stesso_non_ci_sia_un_aggiornamento_adeguato_dei_drivers.3F)
    *   [2.13 D) Arch usa pacchetti firmati??](#D.29_Arch_usa_pacchetti_firmati.3F.3F)
*   [3 Installazione](#Installazione)
    *   [3.1 D) Arch ha bisogno di un migliore installer. Forse con una interfaccia grafica.](#D.29_Arch_ha_bisogno_di_un_migliore_installer._Forse_con_una_interfaccia_grafica.)
    *   [3.2 D) Ho installato con successo Arch e sono alla shell di login! ora come devo procedere?](#D.29_Ho_installato_con_successo_Arch_e_sono_alla_shell_di_login.21_ora_come_devo_procedere.3F)
    *   [3.3 D) Quali desktop environment e window manager posso usare su Arch?](#D.29_Quali_desktop_environment_e_window_manager_posso_usare_su_Arch.3F)
    *   [3.4 D) Cosa rende Arch diversa da altre distribuzioni "minimaliste"?](#D.29_Cosa_rende_Arch_diversa_da_altre_distribuzioni_.22minimaliste.22.3F)
*   [4 Altro](#Altro)
    *   [4.1 D) Pacman mi restituisce un errore: 'warning: current locale is invalid; using default "C" locale'. Cosa devo fare?](#D.29_Pacman_mi_restituisce_un_errore:_.27warning:_current_locale_is_invalid.3B_using_default_.22C.22_locale.27._Cosa_devo_fare.3F)
    *   [4.2 D) Come posso connettermi alle reti wifi?](#D.29_Come_posso_connettermi_alle_reti_wifi.3F)
    *   [4.3 D) Come posso connettermi alle reti cablate](#D.29_Come_posso_connettermi_alle_reti_cablate)
    *   [4.4 D) Che cos'è questo AUR di cui sento parlare spesso?](#D.29_Che_cos.27.C3.A8_questo_AUR_di_cui_sento_parlare_spesso.3F)
    *   [4.5 D) Perchè se tento di guardare un video il mio schermo diventa verde?](#D.29_Perch.C3.A8_se_tento_di_guardare_un_video_il_mio_schermo_diventa_verde.3F)
    *   [4.6 D) Lo spellcheck mi marca tutte le parole come errate](#D.29_Lo_spellcheck_mi_marca_tutte_le_parole_come_errate)

## Generale

### D) Cos'è Arch Linux?

**R)** Vedere l'articolo [Arch Linux](/index.php/Arch_Linux_(Italiano) "Arch Linux (Italiano)").

### D) Perchè si dovrebbe voler utilizzare Arch Linux?

**R)** Se si ha letto e si è d'accordo con la filosofia de [Il Metodo Arch](/index.php/Il_Metodo_Arch "Il Metodo Arch"), e piace l'approccio 'do-it-yourself' (fai-da-te) e si desidera o si aspira ad avere una semplice, elegante, altamente personalizzabile, aggiornatissima distribuzione GNU/Linux, ci sono buone possibilità che Arch Linux possa essere una delle scelte migliori.

### D) Perchè non si dovrebbe voler utilizzare Arch Linux?

**R)** Arch non fa per voi se:

*   dopo aver letto [Il Metodo Arch](/index.php/Il_Metodo_Arch "Il Metodo Arch") non si è d'accordo con la filosofia insita in Arch Linux.
*   non si ha il tempo\capacità\voglia di avere una distribuzione GNU/Linux 'do-it-yourself' (fai-da-te)
*   si ha necessita' di supporto per architetture diverse da x86_64, i686 o [ARM](http://archlinuxarm.org/)
*   si vuole utilizzare una distribuzione che fornisca esclusivamente "free software" , come definito da GNU.
*   si pensa che un sistema operativo debba "autoconfigurarsi" , funzionare "al volo" gia' subito dopo l'installazione ed includere sul supporto di installazione un set completo e predefinito di software e di ambienti desktop.
*   non si vuole una distribuzione GNU/Linux costantemente aggiornata (_bleeding edge rolling release_)
*   si è soddisfatti del proprio attuale sistema operativo.
*   si vuole un sistema operativo pensato per un target diverso di utenti.

### D) Su quale distribuzione GNU/Linux si basa Arch Linux?

**R)** Arch è sviluppata in maniera indipendente, costruita _from scratch_ e non è basata su nessun altra distribuzione. Prima di creare Arch Linux, Judd Vinet era utente e ammiratore della distribuzione CRUX, una distribuzione minimalista creata da Per Lidén. Originariamente quindi Arch era ideologicamente inspirata da CRUX ma Arch Linux è comunque scritta da zero e [pacman](/index.php/Pacman_(Italiano) "Pacman (Italiano)") è scritto in C.

### D) Sono alle prime armi con Linux. Dovrei usare Arch Linux?

**R)** È una questione sulla quale si sono avute molte discussioni. Arch Linux è rivolta a utenti Linux avanzati; nonostante questo molti pensano: "Arch è un buon modo di iniziare". Se si è alle prime armi e si vuole usare Arch, è necessaria moltissima attenzione e si DEVE aver voglia di imparare. Prima di fare qualsiasi domanda, cercare su google, spulciare la Wiki, e cercare sui forum (e leggere le passate FAQs). Se si farà questo, non si avranno problemi. Inoltre è necessario capire che molta gente non vuole rispondere alla stessa domanda più e più volte. _C'è un motivo per cui queste risorse sono state create e rese disponibili per gli utenti_. Sono moltissimi i volontari che hanno impiegato ore del proprio tempo libero a scrivere la documentazione che state leggendo. ArchWiki è il migliore amico di ogni arciere, non dimenticarlo mai!

Lettura raccomandata: la [Guida per Principianti](/index.php/Guida_per_Principianti "Guida per Principianti") di ArchLinux.it .

### D) Arch Linux richiede troppo tempo e troppi sforzi per l'installazione e l'uso. In più la comunità continua a dirmi: "leggi la wiki!" (o RTFM)

**R)** Arch Linux è sviluppata e usata da un target specifico di utenti. Se si pensa davvero che gli sforzi richiesti da Arch Linux siano eccessivi è sicuramente meglio cambiare distribuzione, ce ne sono molte. Vedere [sopra](#D.29_Sono_alle_prime_armi_con_Linux._Dovrei_usare_Arch_Linux.3F).

### D) Arch è più adatta a server, desktop o workstation?

**R)** Arch non è sviluppata per un uso specifico, è sviluppata per una specifica _utenza_. Arch parte dal presupposto che all'utente piaccia l'approccio do-it-yourself e che quindi sia in grado di sagomarsi il sistema operativo "attorno alle proprie esigenze". Questo fa si che virtualmente Arch possa essere usato per qualsiasi scopo. Molti utenti usano Arch sia come desktop sia come workstation e sì, archlinux.org gira su server Arch.

### D) Mi piace molto Arch, ma a mio parere i dev dovrebbero aggiungere la _funzionalità X_.

**R)** Prima di andare oltre, hai letto il documento [Il Metodo Arch](/index.php/Il_Metodo_Arch "Il Metodo Arch")? Hai fornito la funzionalità\la soluzione? È conforme alla filosofia Arch di _minimalismo_ e _correttezza del codice_? Fatti coinvolgere, contribuisci con il tuo codice e le tue soluzioni alla comunità. Se il tuo lavoro verrà apprezzato dagli altri membri, può darsi che il tuo lavoro venga incluso in Arch stessa. La comunità di Arch approva e supporta la condivisione del proprio lavoro e delle proprie utility.

### D) Quando uscirà il prossimo rilascio ufficiale?

**R)** I rilasci di Arch Linux coincidono con l'uscita di una nuova versione principale del kernel, ma sono semplicemente una istantanea del repositori /core , combinata con varie caratteristiche o modifiche allo script di installazione stesso. Il modello "rolling release" mantiene ogni sistema Arch Linux aggiornato e "on the bleeding edge" ovvero con le ultime versioni disponibili ancora in testing fornendo un solo comando.

Per questa ragione, i rilasci non sono così importanti in Arch, perchè il sistema "rolling-release" rende ogni nuovo rilascio superato non appena un pacchetto viene aggiornato. Se stai cercando di ottenere l'ultimo rilascio di Arch Linux, non hai bisogno di reinstallare. Semplicemente esegui il comando `pacman -Syu` e il tuo sistema sarà identico a quello che otterresti con una installazione da zero.

Per questa stessa ragione, i nuovi rilasci di Arch Linux non sono tipicamente pieni di nuove ed eccitanti caratteristiche. Nuove ed eccitanti caratteristiche sono rilasciate quando necessario con l'aggiornamento dei pacchetti, che possono essere ottenuti con un `pacman -Syu`.

### D)Arch è un sistema operativo stabile? Avrò frequentemente problemi

**R)** La risposta lunga in questo caso coincide con quella breve: è stabile se l'utente la rende tale.

L' _utente_ assemblea il suo sistema operativo. Il sistema di base è semplice, toccherà poi al singolo utente controllare gli aggiornamenti. (Ovviamente più si rende complesso il sistema più sarà importante essere in grado di gestirlo). Arch è rivolta a quegli utenti che sanno ciò che stan facendo, che hanno una competenza generica il UNIX e sono in grado di gestire gli aggiornamenti che giocano un ruolo fondamentale nella stabilità del sistema. Inoltre, alla stragrande maggioranza dei pacchetti per arch non viene applicata alcuna patch, quindi molti problemi sono direttamente legati allo sviluppo in upstream.

Pertanto, è l' _utente_, conscio di usare una rolling release, il responsabile della stabilità del proprio sistema. L'utente decide quando aggiornare e come effettuare il _merge_ delle nuove caratteristiche. C'è da sottolineare che la comunità di arch è sempre molto disponibile ad aiutare chi è in difficoltà nello svolgere questa operazione. Arch si contraddistingue da altre distribuzioni proprio per questo; il fatto di usare pacchetti _vanilla_ la rende davvero una distribuzione _do-it-yourself_, infatti, come già specificato qualche riga sopra, i cambiamenti ai pacchetti non vedono come responsabili gli sviluppatori di Arch.

### D) Cos'è esattamente questo sistema di init 'BSD-style' di cui ho sentito parlare?

**R)** Parte dell'eredita di BSD e' l'integrazione del concetto di init. La differenza principale tra l'init BDS e l'init sysV è che Arch, come BSD , utilizza un singolo file , `/etc/rc.conf` , per puntare agli scripts all'interno di una singola directory, `/etc/rc.d/` , per ogni servizio indipendentemente dal runlevel.

Un init sysV, invece , utilizza una directory per ogni runlevel `/etc/rc.0,1,2,3,4,5,6` , con una contorta disposizione di symlinks all'interno della directory; una per ogni servizio , con ogni link simbolico che punta al corrispondente script nella directory `/etc/init.d/`. È evidente come il metodo SysV sia molto più complesso, potendosi facilmente accumulare decine di symlinksin ogni directory `/etc/rc`. Restando fedele alla sua filosofia del "mantienilo semplice" , Arch utilizza un init alla BSD.

### D) Arch ha bisogno di più pubblicità

**R)** Già così Arch ha molta pubblicità. L'obbiettivo di Arch non è essere grande. L'obbiettivo è di essere ben fatta. La sua crescita deve avvenire in modo naturale. Cercare di forzare la crescita causerebbe solo problemi.

Allo stesso modo, non provare a limitare la sua naturale crescita. Più utenti potrebbero voler dire più sviluppatori che lavorano su Arch Linux. Questo potrebbe causare qualche problema di organizzazione alla fine, ma saranno risolti quando arriveranno.

### D) Arch ha bisogno di più sviluppatori

**R)** È possibile. Sentiti libero di mettere a disposizione il tuo tempo! Visita i [forum](http://www.archlinux.it/forum), i canali IRC, e le [mailing lists](https://mailman.archlinux.org/mailman/listinfo/), e vedi di cosa c'è bisogno. Farsi coinvolgere nella comunità è sicuramente un ottimo modo per iniziare.

### D) Perchè Arch è così lenta? Pensavo fosse veloce!

**R)** Assicurarsi che il proprio _hostname_ sia correttamente impostato in `/etc/hosts` (per es., che corrisponda all'hostname in `/etc/rc.conf` o `/etc/hostname`. Prendere visione della sezione "Configurare il Sistema" nella [Guida per Principianti](/index.php/Guida_per_Principianti "Guida per Principianti")). Se gli hostname non corrispondono, le applicazioni potrebbero avviarsi molto lentamente.

### D)Perchè Internet è così lento in confronto ad altri sistemi operativi?

**R)** La rete è configurata correttamente? Controllare bene i file `/etc/rc.conf`, `/etc/hosts` e `/etc/resolv.conf` dando particolare attenzione alla sintassi della variabile _localhost_.

Si noti inoltre che Arch Linux non applica alcun controllo sull'utilizzo del traffico internet (traffic shaping). È quindi possibile che un programma utilizzi completamente la banda disponibile (ad esempio client P2P o classiche connessioni client-server) causando lag, timeout e ping molto elevati. In ausilio può essere installato un [firewall](/index.php/Firewalls_(Italiano) "Firewalls (Italiano)") come Shorewall o Vuurmuur; si noti che esistono anche degli script statici per iproute2 (come ad esempio [[questo](http://serendipity.ruwenzori.net/index.php/2008/06/01/modified-wondershaper-for-better-voip-qos)]) che svolgono proprio questo compito.

### D) Perchè Arch utilizza tutta la mia RAM?

**R)** Fondamentalmente la RAM inutilizzata e' una RAM sprecata!

Per molti novelli utenti e' importante chiarire come Linux gestisca la memoria: in modo diverso a come erano abituati!

Dal momento che l'accedere a dati in RAM e' decisamente piu' rapido che accedervi dal disco, Linux "parcheggia" i dati recentemente utilizzati in memoria. Questi dati ( detti in cache ) vengono cancellati qualora il sistema si avvicini al limite della memoria disponile e nuovi dati debbano essere caricati.

Solitamente la più comune fonte di confusione e' data dal comando `free` :

 `$ free -m` 

```
$ free -m
             total       used       free     shared    buffers     cached
Mem:          1009        741        267          0        104        359
-/+ buffers/cache:        278        731     <-- **NOTA BENE**!
Swap:         1537          0       1537
```

E' importante notare la riga `-/+ buffers/cache:` , un conteggio della quantità di memoria in "uso attivo" ed uno di memoria definita "disponibile" piuttosto che "inutilizzata"

In questo esempio un laptop con 1G di RAM sembrerebbe utilizzarne 741M , con pochi inutili terminali aperti ed un browser attivo!

Tuttavia esaminando la riga `-/+ buffers/cache:` e' possibile notare come solo 278M siano effettivamente in "uso attivo" mentre 731M sono semplicemente disponibili a ricevere nuovi dati. Apparentemente 104M di quella memoria "utilizzata" contengono dati buffered e 359M contengono dati cached, ma entrambe le posizioni di memoria possono essere liberate in caso di necessita'. Soltanto 267M sono effettivamente liberi dalla gestione dati.

Il risultato finale? Migliori prestazioni!

Vedi [questo articolo](http://www.linuxjournal.com/article/2770) ( in inglese) se vuoi approfondire!

### D) Dov'è finito tutto il mio spazio libero?

**R)** La risposta a questa domanda dipende esclusivamente dal proprio sistema. Ci sono alcuni [tools](/index.php/Common_Applications_(Italiano)#Programmi_per_la_visualizzazione_dell.27uso_del_Disco "Common Applications (Italiano)") che possono aiutare molto.

## Gestione Pacchetti

### D)Il pacchetto X in quale è contenuto?

**R** È possibile eseguire questo tipo di ricerca con [pkgfile](/index.php/Pkgfile "Pkgfile"). Ad esempio: `$ pkgfile glxinfo` restituirà come output: `extra/mesademos` ad indicare che `glxinfo` è contenuto nel pacchetto [mesa-demos](https://www.archlinux.org/packages/?name=mesa-demos) prensente nel [repository](/index.php/Official_Repositories_(Italiano) "Official Repositories (Italiano)") [extra].

### D) Ho trovato un errore nel pacchetto X. Che dovrei fare?

**R)** In primo luogo, devi capire se questo errore è qualcosa che il team Arch può sistemare. Qualche volta non è così (che Firefox vada in crash può essere colpa del gruppo Mozilla) - questo è chiamato un _upstream error_. Se è un problema di Arch , c'è una serie di passi che puoi seguire:

1.  Cerca sui forum per informazioni. Controlla se qualcun altro lo ha notato.
2.  Posta un [bug report](/index.php/Reporting_bug_guidelines "Reporting bug guidelines") con informazioni dettagliate su [https://bugs.archlinux.org](https://bugs.archlinux.org).
3.  Se preferisci, scrivi un post sul forum spiegando in dettaglio il problema a il fatto che hai già riportato.Questo aiuterà molte persone dal fare un report dello stesso errore.

### D) I pacchetti di Arch hanno bisogno di usare un'unica estensione. .pkg.tar.gz e .pkg.tar.xz sono troppo lunghe e/o poco chiare

**R)** Questo è stato discusso sulla Arch mailing list. Alcuni hanno proposto una estensione .pac. Da quanto si sa non c'è intenzione di cambiare l'estensione dei pacchetti. Come ha detto Tobias Kieslich, uno degli sviluppatori di Arch, "Un pacchetto **è** un gzipped tarball! E può essere aperto, ispezionato e manipolato da ogni applicazione che gestisca i tar. Inoltre, il tipo mime è automaticamente e correttamente rilevato dalla maggior parte delle applicazioni."

### D) Pacman ha bisogno di una libreria così che le altre applicazioni possano facilmente accedere alle informazioni sui pacchetti

**R)** Dalla versione 3.0.0, pacman è stato il front-end a libalpm, la libreria di mantenimento pacchetti di Arch Linux . Questa libreria permette di scrivere un alternativo front-end(per esempio, front-end grafico).

### D) Perchè pacman non ha un front end grafico (GUI)?

**R)** Hai letto [Il Metodo Arch](/index.php/Il_Metodo_Arch "Il Metodo Arch") e [Arh Linux](/index.php/Arch_Linux_(Italiano) "Arch Linux (Italiano)")? La risposta è fondamentalmente che gli sviluppatori di arch non ne forniranno uno. Puoi comunque usare uno di quelli sviluppati dagli utenti. Ce n'è una lista selettiva su [Pacman GUI Frontends](/index.php/Pacman_GUI_Frontends "Pacman GUI Frontends").

### D) Pacman ha bisogno della _caratteristica X!_

**R)** Hai letto [Il Metodo Arch](/index.php/Il_Metodo_Arch "Il Metodo Arch") e [Arch linux](/index.php/Arch_Linux_(Italiano) "Arch Linux (Italiano)")? La filosofia Arch è "Keep It Simple". Se tu pensi che l'idea meriti e non violi questo ideali di semplicità discutilo sul forum [qui](https://bbs.archlinux.org/). Potresti anche controllare [qui](https://bugs.archlinux.org); è un luogo dove effettuare richieste di caratteristiche se trovi che sia importante.

Comunque il miglior modo di ottenere una caratteristiche aggiuntiva per Pacman o Arch Linux è implementartela da solo. Nessuno ti dirà che la patch sarà ufficialmente accettata ma altri apprezzeranno e testeranno il tuo contributo.

### D) Arch ha bisogno di una versione stable

**R)** Date un'occhiata a [ArchServer](http://www.archserver.org/).

**Note:** Il 2011-09-12, il progetto ArchServer è stato dichiarato morto. Potete leggere l'annuncio [here](http://www.archserver.org/index.php?mact=News,cntnt01,detail,0&cntnt01articleid=52&cntnt01origid=15&cntnt01returnid=22).

### D) Qual è la differenza fra tutti questi repository?

**R)** Leggi [Official Repositories](/index.php/Official_Repositories_(Italiano) "Official Repositories (Italiano)").

### D) Ho appena installato il pacchetto X. Come lo avvio?

**R)** Se tu stai usando un ambiente desktop come [KDE](/index.php/KDE_(Italiano) "KDE (Italiano)") o [GNOME](/index.php/GNOME_(Italiano) "GNOME (Italiano)"), il programma dovrebbe automaticamente mostrarsi nel tuo menu. Se stai cercando di avviare il programma da un terminale e non sai il nome del file binario prova a eseguire `pacman -Qlq nomepacchetto | grep bin`. Un Problema comune per pacchetti come Firefox o Openoffice è che vengono installati in `/opt`, che non è nel tuo `$PATH` - tu puoi `source /etc/profile` o riloggarti per risolvere.

### D) Perchè nei repositories c'è solo una versione per ogni libreria?

**R)** Molte distribuzioni, come ad esempio Debian, mantengono nei propri repositories più versioni dello stesso pacchetto, ad esempio `libfool1`, `libfool2`, `libfool3` ecc. In questo modo è possibile compilare il proprio sistema in modo differente in base alla versione di libreria installata.

A differenza di Debian però, Arch è una distribuzione rolling-release cutting-edge. Questo significa che nei [repositories ufficiali](/index.php/Official_Repositories_(Italiano) "Official Repositories (Italiano)") si trovi **solo** l'ultima versione della libreria in questione e quindi solo quest ultima versione risulta essere ufficialmente supportata. Ogni volta che lo sviluppo in upstream _sforna_ una nuova libreria, questa entra immediatamente nei repositories facendo _uscire_ la versione precedente. Ne consegue che tutti i pacchetti che si trovano ufficiali vengano ricompilati dai developers ogni qualvolta c'è un aggiornamento delle librerie comuni.

### D) Cosa succede se aggiornando il sistema ricevo aggiornamenti per una libreria e non per le sue dipendenze?

**R)**Questa è una situazione praticamente impossibile. Supponiamo di avere un'applicazione il cui pacchetto risponde il nome di `foobaz`, compilata dal manteiner con la libreria `libbaz`, se un aggiornamento di `libbaz` non crea problemi a `foobar`, pacman aggiornerà `libbaz` tranquillamente. In caso contrario, sarà premura del manteiner, inserire una _dipendenza di versione_ a `foobar`, ad esempio:

```
libbaz=1.5

```

Il conflitto verrà segnalato da pacman.

Se `foobaz` è invece un pacchetto compilato da [AUR](/index.php/AUR_(Italiano) "AUR (Italiano)"), si dovrà procedere manualmente alla ricompilazione quando la nuova libreria `libbaz` viene installata sul sistema. Se il pacchetto dovesse presentare errori di compilazione, farlo presente al manteiner di `foobar`.

### D) È possibile che ci sia un aggiornamento di versione del kernel e al tempo stesso non ci sia un aggiornamento adeguato dei drivers?

**R)** No, impossibile. Ogni qualvolta il kernel viene aggiornato viene ricreata l'immagine del kernel con, di conseguenza, la ricompilazione dei driver. In altre parole, se si usano pacchetti non supportati come ad esempio i [driver proprietari ATI](/index.php/ATI_Catalyst_(Italiano) "ATI Catalyst (Italiano)") [catalyst](https://aur.archlinux.org/packages/catalyst/)<sup><small>AUR</small></sup>, l'utente deve essere in grado di gestirne l'upgrade e la necessaria ricompilazione.

### D) Arch usa pacchetti firmati??

**R)**La firma dei pacchetti di [pacman](/index.php/Pacman_(Italiano) "Pacman (Italiano)") è stata introdotta dalla release 4 del package manager. Non ancora tutti i pacchetti risultano provvisti di firma. Per maggiori informazioni consultare: [package signing](/index.php/Package_signing "Package signing") e [pacman-key](/index.php/Pacman-key_(Italiano) "Pacman-key (Italiano)").

## Installazione

### D) Arch ha bisogno di un migliore installer. Forse con una interfaccia grafica.

**R)** La discussione su un installer "migliore" è un argomento soggettivo. Il modo migliore di cavarsela con questi problemi è quello di adattare l'installer alla "[Il Metodo Arch](/index.php/Il_Metodo_Arch "Il Metodo Arch")". Se questa opinione su un miglior installer è appoggiata da argomentazioni più concrete, potrebbe essere presa in considerazione per un prossimo sviluppo dell'installer. Visto che l'installazione non avviene spesso (vedere la domanda sopra sulla rolling release), non è una alta priorità per gli sviluppatori o gli utenti. È comunque possibile usare [archiso](/index.php/Archiso "Archiso") o [larch](/index.php/Larch "Larch").

### D) Ho installato con successo Arch e sono alla shell di login! ora come devo procedere?

**R)** Guardare la [Guida per Principianti](/index.php/Guida_per_Principianti "Guida per Principianti").

### D) Quali desktop environment e window manager posso usare su Arch?

**R)** Arch supporta e pacchettizza praticamente tutti gli "ambienti grafici" opensource. Per maggiori informazioni visitare [Desktop Environment](/index.php/Desktop_Environment_(Italiano) "Desktop Environment (Italiano)") o [Window Manager](/index.php/Window_Manager_(Italiano) "Window Manager (Italiano)").

### D) Cosa rende Arch diversa da altre distribuzioni "minimaliste"?

**R)** Esistono certamente altre distribuzioni GNU/Linux che hanno un metodo d'installazione simile ad Arch. Gli aspetti caratteristici quindi sono:

1.  Arch è fondamentalmente disegnata per essere leggera, minimale e per dare un ambiente base su cui costruire il proprio ambiente di lavoro.
2.  Se si installa Arch da Netinstall o Core, l'unico modo per avere un sistema usabile è costruire tutto da questa (solida) base.
3.  L'installer, il sistema di base e l'intera distribuzione seguono totalmente la filosofia KISS, rendendo questo sistema operativo adatto solo ad una piccola parte di utenti.
4.  Installare pacchetti su arch generalmente richiede una configurazione da parte dell'utente. A differenza di altre distribuzioni nulla risulta essere configurato di default. Questo tipo di filosofia fa si che l'utente sia responsabile del proprio sistema.
5.  Anche la pacchettizzazione di arch segue questo approccio. Infatti le dipendenze opzionali di ogni pacchetto (segnalate in modo molto chiaro nell'output di pacman) non vengono installate, sarà l'utente a decidere se usarle o meno. Il risultato è un sistema molto leggero.
6.  <s>AIF, l'installer di Arch, è sviluppato con un elevato grado di trasparenza e il sistema di base è configurato a mano dall'utente consapevole delle proprie necessità.</s>
7.  Arch ha una documentazione eccellente che può guidare gli utenti passo passo nell'assemblare il proprio sistema.

## Altro

### D) Pacman mi restituisce un errore: 'warning: current locale is invalid; using default "C" locale'. Cosa devo fare?

**R)** Come dice l'output di pacman, il _locale_ non è correttamente settato. Vedere [questa pagina per ulteriori informazioni](/index.php/Configuring_locales "Configuring locales").

### D) Come posso connettermi alle reti wifi?

**R)** Vedere [Wireless Setup](/index.php/Wireless_Setup_(Italiano) "Wireless Setup (Italiano)").

### D) Come posso connettermi alle reti cablate

**R)** Vedere [configuring network](/index.php/Configuring_Network_(Italiano) "Configuring Network (Italiano)").

### D) Che cos'è questo AUR di cui sento parlare spesso?

**R)** Vedere [AUR](/index.php/AUR_(Italiano) "AUR (Italiano)").

### D) Perchè se tento di guardare un video il mio schermo diventa verde?

**R)** La profondità di colore è errata. Usare, ad esempio, 24 al posto di 16.

### D) Lo spellcheck mi marca tutte le parole come errate

**R)** Il dizionario è correttamente installato? Con il comando `pacman -Ss aspell` si possono vedere le lingue disponibili.

Se, una volta installato il pacchetto, il problema persiste è molto probabile che ci sia un problema con `enchant`.

Innanzitutto controllare quale file di dizionario viene riconosciuto con `aspell dists`:

```
$ aspell dicts

```

output: en en_GB it_IT ...etc

Se fra quelle elencate c'è la lingua che interessa aggiungere a `/usr/share/enchant/enchant.ordering`:

```
language:aspell
it_IT:aspell #esempio

```

Retrieved from "[https://wiki.archlinux.org/index.php?title=Frequently_asked_questions_(Italiano)&oldid=411872](https://wiki.archlinux.org/index.php?title=Frequently_asked_questions_(Italiano)&oldid=411872)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [About Arch (Italiano)](/index.php/Category:About_Arch_(Italiano) "Category:About Arch (Italiano)")