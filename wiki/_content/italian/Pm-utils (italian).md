**pm-utils** è un framework per l'impostazione della sospensione e per la variazione dello stato di alimentazione. É progettato per sostituire gli script come quelli forniti dal pacchetto `powersave`.

pm-utils è una collezione di script di shell che integrano nella modalità kernel la sospensione/rispristino con vari hack necessari per risolvere i bug nei driver e sottosistemi che non sono ancora a conoscenza della sospensione. E 'facilmente estendibile tramite l'ausilio di hook personalizzati in una directory, che possono essere creati dall'amministratore di sistema o hook che possono forniti da un pacchetto, soprattutto se questo pacchetto richiede particolare attenzione nel corso di una sospensione del sistema o la variazione dello stato di alimentazione.

Un aspetto meno conosciuto è quello che simula le commutazioni fatte da [Laptop Mode Tools](/index.php/Laptop_Mode_Tools_(Italiano) "Laptop Mode Tools (Italiano)").

Utilizzato in combinazione col pacchetto [cpupower](/index.php/Cpupower "Cpupower"), gli utenti notebook (e desktop) sono dotati di una suite completa per la gestione dell'alimentazione.

## Contents

*   [1 Installazione](#Installazione)
    *   [1.1 Installare backend per la sospensione alternativi (opzionale)](#Installare_backend_per_la_sospensione_alternativi_.28opzionale.29)
*   [2 Configurazione di base](#Configurazione_di_base)
    *   [2.1 Standby / Sospensione su RAM](#Standby_.2F_Sospensione_su_RAM)
    *   [2.2 Ibernazione (suspend2disk)](#Ibernazione_.28suspend2disk.29)
    *   [2.3 Sospensione e Ibernazione come utente](#Sospensione_e_Ibernazione_come_utente)
        *   [2.3.1 Metodo UPower](#Metodo_UPower)
        *   [2.3.2 Metodo con i permessi Utente](#Metodo_con_i_permessi_Utente)
    *   [2.4 Risparmio Energetico](#Risparmio_Energetico)
        *   [2.4.1 Cambiare la retroilluminazione in dipendenza dell'alimentazione](#Cambiare_la_retroilluminazione_in_dipendenza_dell.27alimentazione)
    *   [2.5 Sospensione in caso di idle/inattività](#Sospensione_in_caso_di_idle.2Finattivit.C3.A0)
    *   [2.6 Utilizzare un file di Swap al posto della regolare partizione swap](#Utilizzare_un_file_di_Swap_al_posto_della_regolare_partizione_swap)
*   [3 Configurazione avanzata](#Configurazione_avanzata)
    *   [3.1 Variabili disponibili per l'uso nei file di configurazione](#Variabili_disponibili_per_l.27uso_nei_file_di_configurazione)
    *   [3.2 Disabilitare un Hook](#Disabilitare_un_Hook)
        *   [3.2.1 Metodo alternativo](#Metodo_alternativo)
    *   [3.3 Creazione di un Hook personale](#Creazione_di_un_Hook_personale)
*   [4 Come funziona](#Come_funziona)
    *   [4.1 Funzionamento di Pm-suspend](#Funzionamento_di_Pm-suspend)
*   [5 Risoluzione dei problemi](#Risoluzione_dei_problemi)
    *   [5.1 Segmentation faults](#Segmentation_faults)
    *   [5.2 Il sistema si riavvia invece di ripristinarsi dalla sospensione](#Il_sistema_si_riavvia_invece_di_ripristinarsi_dalla_sospensione)
    *   [5.3 Il sistema si spegne invece di ripristinarsi dalla sospensione](#Il_sistema_si_spegne_invece_di_ripristinarsi_dalla_sospensione)
    *   [5.4 Schermo nero al ripristino dalla sospensione](#Schermo_nero_al_ripristino_dalla_sospensione)
    *   [5.5 Problemi con VirtualBox](#Problemi_con_VirtualBox)
    *   [5.6 Ibernazione in assenza di una partizione di Swap](#Ibernazione_in_assenza_di_una_partizione_di_Swap)
    *   [5.7 Schermo nero con cursore fisso quando si tenta di sospendere il sistema](#Schermo_nero_con_cursore_fisso_quando_si_tenta_di_sospendere_il_sistema)
    *   [5.8 Problema schermo nero](#Problema_schermo_nero)
    *   [5.9 Impossibile il resume con arch 64 bit](#Impossibile_il_resume_con_arch_64_bit)
*   [6 Trucchi e Consigli / FAQ](#Trucchi_e_Consigli_.2F_FAQ)
    *   [6.1 Riprendere automaticamente i livelli della gestione dell'alimentazione di un HD dopo la sospensione](#Riprendere_automaticamente_i_livelli_della_gestione_dell.27alimentazione_di_un_HD_dopo_la_sospensione)
    *   [6.2 Riavviare il mouse](#Riavviare_il_mouse)
    *   [6.3 Aggiungere una modalità sleep al menu di Openbox](#Aggiungere_una_modalit.C3.A0_sleep_al_menu_di_Openbox)
    *   [6.4 Modificare i pulsanti "sleep" e "power"](#Modificare_i_pulsanti_.22sleep.22_e_.22power.22)
    *   [6.5 Bloccare lo schermo quando si iberna o si sospende](#Bloccare_lo_schermo_quando_si_iberna_o_si_sospende)
    *   [6.6 Disabilitare l'ibernazione tramite polkit](#Disabilitare_l.27ibernazione_tramite_polkit)
*   [7 Ulteriori Risorse](#Ulteriori_Risorse)

## Installazione

Il pacchetto [pm-utils](https://www.archlinux.org/packages/?name=pm-utils) è reperibile nei [Repository ufficiali](/index.php/Official_repositories_(Italiano) "Official repositories (Italiano)").

**Note:**

*   Se si riscontrano problemi durante la riproduzione di video, potrebbe essere necessario installare anche di [vbetool](https://www.archlinux.org/packages/?name=vbetool) dai [repository ufficiali](/index.php/Official_repositories_(Italiano) "Official repositories (Italiano)").
*   Se si parte da una nuova installazione, assicurarsi di installare anche il pacchetto [acpi](https://www.archlinux.org/packages/?name=acpi).

Eseguire `pm-suspend`, `pm-suspend-hybrid` o `pm-hibernate` come utente root per attivare la sospensione manualmente. Gli script di sospensione scrivono i loro log in `/var/log/pm-suspend.log`.

### Installare backend per la sospensione alternativi (opzionale)

Il pacchetto di Arch Linux viene fornito con il supporto per i seguenti backend: `kernel`,`tuxonice` e `uswsusp`, si può controllare quali backend sono presenti nel sistema con il seguente comando:

```
pacman -Ql pm-utils | grep module.d

```

Il backend per la sospensione è specificato dalla variabile SLEEP_MODULE nel file di configurazione `/etc/pm/config.d` ed è il backend predefinito il valore **kernel**. Se si desidera utilizzare dei backend per la sospensione alternativi, come uswsusp o tuxonice, è necessario che i relativi pacchetti siano installati, Alcuni di essi sono reperibili su [AUR](/index.php/AUR_(Italiano) "AUR (Italiano)"):

*   uswsusp - [uswsusp-git](https://aur.archlinux.org/packages/uswsusp-git/)
*   tuxonice - [linux-ice](https://aur.archlinux.org/packages/linux-ice/) / [linux-pf](/index.php/Linux-pf "Linux-pf")

Inoltre, [pm-utils](https://www.archlinux.org/packages/?name=pm-utils) contiene in `/usr/lib/pm-utils/video-quirks/` delle regole speciali per esigenze particolari, ad esempio se c'è un driver video problematico, in modo che venga attuata una politica non-standard all'atto della sospensione.

## Configurazione di base

### Standby / Sospensione su RAM

Nel caso ideale , l'esecusione di `sudo pm-suspend` dovrebbe inizializzare la sospensione in memoria RAM, ovvero tutti gli stati in esecuzione verranno preservati in RAM e tutti gli altri componenti che sono eseguiti in ram verrano spenti per risparmiare energia. la pressione del tasto di accensione dovrebbe inizializzare il rispristino da questo stato.

**Note:** Si raccomanda di mettere sempre i driver del network nella stringa SUSPENDED_MODULES, poichè è risaputo che la maggior parte di questi possa causare problemi dopo lo standby. I driver Intel iwlwifi, Atheros ath5k e Realtek r8* sono stati tutti segnalati per aver generato problemi dopo il resume dalla sospensione, sui vari forum. iwlwifi limita anche la connessione a 1Mbps se non è ricaricato dopo la sospensione.

In alcuni casi, può capitare che l'esecuzione di `pm-suspend` si blocchi o causi altri problemi. Ciò potrebbbe essere causato da un modulo che si comporta in modo "anomalo". Se si conosce quale moduli sia la causa di questi problemi, aggiungendo SUSPEND_MODULES al file di configurazione `/etc/pm/config.d/modules`, con la seguente sintassi

```
SUSPEND_MODULES="uhci_hd button ehci_hd"

```

dovrebbe imporre lo scaricamento dei moduli specificati prima di procedere alla sospensione, e di ricaricarli dopo il ripristino (resume).

Per configurare l'esecuzione automatica di `pm-suspend` in base ad eventi specifici, come la chiusura del coperchio di un portatile, si faccia riferimento all'articolo [Acpid](/index.php/Acpid_(Italiano) "Acpid (Italiano)").

### Ibernazione (suspend2disk)

Bisogna seguire le istruzioni in [Suspend and hibernate#Hibernation](/index.php/Suspend_and_hibernate#Hibernation "Suspend and hibernate") per configurare l'ibernazione.

In alternativa, se non si utilizza il `kernel` backend, si veda [Uswsusp#Configuration](/index.php/Uswsusp#Configuration "Uswsusp") o [TuxOnIce#Setting up the bootloader](/index.php/TuxOnIce#Setting_up_the_bootloader "TuxOnIce").

### Sospensione e Ibernazione come utente

Esistono tre metodi per avviare la sospensione senza avere la necessità di fornire la password di root : tramite [Udev](/index.php/Udev_(Italiano) "Udev (Italiano)"), UPower, e dando i giusti permessi all'utente tramite [visudo](/index.php/Sudo_(Italiano) "Sudo (Italiano)").

#### Metodo UPower

Installare [upower](https://www.archlinux.org/packages/?name=upower) per la sospensione su RAM (Sopsensione):

```
$ dbus-send --system --print-reply --dest="org.freedesktop.UPower" /org/freedesktop/UPower org.freedesktop.UPower.Suspend

```

Per la sospensione su disco (Ibernazione):

```
$ dbus-send --system --print-reply --dest="org.freedesktop.UPower" /org/freedesktop/UPower org.freedesktop.UPower.Hibernate

```

#### Metodo con i permessi Utente

Siccome gli script `pm-utils` devono essere eseguiti da root, si consiglia di rendere gli script accessibili agli utenti normali eseguendo `sudo` senza fornire la password di root. Per far ciò, editare il file `/etc/sudoers` con `visudo` come utente root. Si veda [sudo](/index.php/Sudo_(Italiano) "Sudo (Italiano)") per ulteriori informazioni.

Aggiungere le seguenti linee, sostituire `username` con il vostro nome utente, successivamente salvare ed uscire da `visudo`:

```
*username*  ALL = NOPASSWD: /usr/sbin/pm-hibernate
*username*  ALL = NOPASSWD: /usr/sbin/pm-suspend

```

In alternativa si può abilitare un intero gruppo utilizzando le seguenti linee, anche in questo caso sostituire `group` con il vostro:

```
*%group*   ALL = NOPASSWD: /usr/sbin/pm-hibernate
*%group*   ALL = NOPASSWD: /usr/sbin/pm-suspend

```

**Nota:** Queste devono essere poste dopo i privilegi degli utenti specificati, es., `username ALL=(ALL) ALL`, o non non funzionerà.

Ora potrete eseguire gli script senza utilizzare la password di root , semplicemente digitando:

```
$ sudo pm-hibernate

```

oppure :

```
$ sudo pm-suspend

```

Inoltre, aggiungere il proprio utente al [gruppo](/index.php/Users_and_groups_(Italiano) "Users and groups (Italiano)") `power` permette di utilizzare molti applet che si occupano della sospensione. Non non si effettua questa procedura quando si tenterà di utilizzare un applet integrato, come ad esempio [GNOME](/index.php/GNOME_(Italiano) "GNOME (Italiano)") shutdown, per sospendere o ibernare il proprio computer, esso non funzionerà correttamente ottenendo solo il blocco dello schermo.

 ` # gpasswd -a *username* power` 

Ora dovreste essere in grado di utilizzare gli strumenti di gestione energetica del vostro [ambiente desktop](/index.php/Desktop_environment_(Italiano) "Desktop environment (Italiano)"), ad esempio per sospendere o ibernare il sistema alla chiusura del coperchio del portatile, o quando si sta esaurendo la batteria, etc...

### Risparmio Energetico

pm-utils è in grado di eseguire dei comandi a seconda se il sistema è collegato alla rete o meno. Quindi uno script deve essere creato all'interno della cartella `/etc/pm/power.d/`. Un esempio di tale script può essere trovato nel forum [crunchbang](http://crunchbanglinux.org/forums/post/110148/#p110148). Assicuratevi che upower sia in esecuzione al fine di rilevare i cambiamenti Stati AC, si veda ([questa discussione](https://bbs.archlinux.org/viewtopic.php?id=132125) per maggiori informazioni).

#### Cambiare la retroilluminazione in dipendenza dell'alimentazione

Un possibile esempio è riportato qua sotto, per cambiare la luminosità dello schermo in accordo con lo stato dell'alimentazione. Creare un file chiamato `/etc/pm/power.d/00-brightness` col seguente contenuto; cambiare il percorso per l'impostazione della luminosità come pure il valore scritto in quel file tramite echo in base al tuo sistema.

```
#!/bin/bash

case $1 in
    true)
    echo "Enable screen power saving"
    echo 5 > /sys/class/backlight/acpi_video0/device/backlight/acpi_video0/brightness
    ;;
    false)
    echo "Disable screen power saving"
    echo 14 > /sys/class/backlight/acpi_video0/device/backlight/acpi_video0/brightness
    ;;
esac

```

### Sospensione in caso di idle/inattività

Un metodo si basa sul programma xautolock. Aggiungere quanto segue:

```
xautolock -time 30 -locker "sudo pm-suspend" &

```

in `~/.xinitrc`. Questo implica che `pm-suspend` verrà invocato dipo 30 minuti di inattività.

### Utilizzare un file di Swap al posto della regolare partizione swap

Se si desidera utilizzare un file di Swap al posto della partizione swap si veda [[[Swap#Swap file](/index.php/Swap#Swap_file "Swap")]].

## Configurazione avanzata

Il file di configurazione principale è `/usr/lib/pm-utils/defaults`. Si consiglia di non modificare questo file, dal momento che dopo un aggiornamento del pacchetto potrebbe essere sovrascritto con le impostazioni predefinite. Si metta il proprio file di configurazione in `/etc/pm/config.d/`. Si può semplicemente mettere un semplice file di testo con :

```
SUSPEND_MODULES="button uhci_hcd"

```

Nominandolo `modules` o `config` in `/etc/pm/config.d` verranno ignorate le impostazioni del sistema a livello di file di configurazione.

### Variabili disponibili per l'uso nei file di configurazione

	SUSPEND_MODULES="button"

	elenco dei moduli da scaricare prima di sospendere

	SLEEP_MODULE="tuxonice uswsusp kernel"

	Sistema predefinito per effettuare lo sleep/wake del sistema

	HIBERNATE_MODE="shutdown"

	forza il sistema di spegnimento, piuttosto che il riavvio

### Disabilitare un Hook

Se si esegue un Hook che non ci aggrada o che si pensa non sia utile o addirittura dannoso, gradiremmo un bug report per questo. Si può però facilmente disabilitare un Hook semplicemente creando un file vuoto corrispondente all'Hook in questione in `/etc/pm/sleep.d/`. Ad esempio se si desidera disattivare l'Hook `/usr/lib/pm-utils/sleep.d/45pcmcia`, lo si può fare facilmente eseguendo:

```
# touch /etc/pm/sleep.d/45pcmcia

```

E non impostare nessun bit eseguibile su quell'Hook fittizio .

Note: assicurarsi di creare il file nella cartella appropriata. Se si sta ad esempio cercando di disabilitare un hook in /usr/lib/pm-utils/power.d, l'hook fittizio dovrà essere inserito in /etc/pm/power.d.

#### Metodo alternativo

Creare un file in `/etc/pm/config.d` con i moduli che si desidera mettere in blacklist nella variabile `HOOK_BLACKLIST`. Ad esempio, per gestire il risparmio energetico da soli, utilizzare:

```
HOOK_BLACKLIST="hal-cd-polling intel-audio-powersave journal-commit laptop-mode pcie_aspm readahead sata_alpm sched-powersave xfs_buffer wireless"

```

### Creazione di un Hook personale

Se si vuole fare qualcosa di specifico per la configurazione durante la sospensione/ibernazione, allora si può facilmente mettere un Hook personale in `/etc/pm/sleep.d`. Gli Hook in questa directory saranno chiamati in ordine alfabetico durante la sospensione (che è la ragione i loro nomi iniziano tutti con 2 cifre, per rendere esplicito l'ordine) e in ordine inverso durante la ripresa. La convenzione generale da seguire su come ordinare il numero è il seguente:.

	00 - 49

	Hook in dotazione agli utenti e per la maggior parte dei pacchetti. Se un Hook si assume che tutti i soliti servizi e le infrastrutture userspace sono ancora in esecuzione, dovrebbe essere qui.

	50 - 74

	Hook di gestione di servizio. Hook che avviano o arrestano un servizio appartengono a questa gamma. Gli Hook a 50 o inferiori, suppongono che tutti i servizi siano ancora attivi.

	75 - 89

	Modulo e non-core di gestione hardware. Se un Hook ha bisogno di caricare/scaricare un modulo, o se ha bisogno di non avere un hardware video attivo che altrimenti bloccherebbero la sospensione o l'ibernazione in uno stato sicuro, appartiene a questa gamma. Gli Hook a 75 o precedenti possono presupporre che tutti i moduli siano ancora caricati.

	90 - 99

	Riservato ad Hook critici di sospensione.

Di seguito viene mostrato un Hook dimostrativo ed inutile, il quale aggiunge delle linee informative nel proprio file di log:

```
#!/bin/bash
case $1 in
    hibernate)
        echo "Il sistema si accinge alla sospensione su disco!"
        ;;
    suspend)
        echo "Il sistema si accinge alla sospensione in RAM!"
        ;;
    thaw)
        echo "La sospensione su disco è terminata, il sistema è in ripristino..."
        ;;
    resume)
        echo "La sospensione su Ram è terminata..."
        ;;
    *)  echo "C'è qualcosa di totalmente sbagliato."
        ;;
esac

```

Mettere questo file in `/etc/pm/sleep.d/66dummy`, dare un `chmod +x /etc/pm/sleep.d/66dummy` ed esso genererà alcuni messaggi inutili durante la sospensione ed il ripristino.

**Attenzione:** Tutti gli Hook sono eseguiti come utente root. Questo significa che è necessario fare molta attenzione quando si creano file temporanei, controllare che la variabile `PATH` sia impostata correttamente, ecc. Al fine di evitare problemi di sicurezza..

## Come funziona

Il concetto è abbastanza semplice: lo script principale (`pm-action`, denominato tramite link simbolici sia come `pm-suspend`, `pm-hibernate` o `pm-suspend-hybrid`) esegue i cosiddetti `hooks`, script eseguibili, nell'ordine alfabetico ordinato con il parametro `suspend` (sospensione in RAM) o `hibernate` (sospensione su disco). Una volta che tutti gli hooks sono eseguiti, mette la macchina in sleep. Dopo che la macchina viene ripresa dallo stato di sleep, tutti gli hooks vengono eseguiti in ordine inverso con il parametro `resume` (ripresa da RAM) o `thaw` (ripresa da disco). Gli hook sono in grado di eseguire diversi compiti, quali la preparazione del bootloader, fermando il sottosistema Bluetooth o lo scarico dei moduli critici.

Sia `pm-suspend` che `pm-hibernate` sono di solito chiamati da [Udev](/index.php/Udev_(Italiano) "Udev (Italiano)"), inizializzati da applet desktop come `gnome-power-manager` o `kpowersave`.

**Nota:** `suspend-hybrid` non è completamente implementato.

Esiste anche la possibilità di impostare la macchina in modalità high-power (performance) e low-power (risparmio energetico), il comando `pm-powersave` viene utilizzato con una parametro aggiuntivo `true` o `false`. Funziona praticamente allo stesso modo del quadro di sospensione.

Gli hooks per la sospensione sono situati in

*   `/usr/lib/pm-utils/sleep.d` (distribuzione / il pacchetto fornisce gli hooks)
*   `/etc/pm/sleep.d` (hooks aggiunti dall'amministratore di sistema)

Gli hooks per lo stato di alimentazione sono situati in

*   `/usr/lib/pm-utils/power.d` ((distribuzione / il pacchetto fornisce gli hooks)
*   `/etc/pm/power.d` (hooks aggiunti dall'amministratore di sistema)

Gli Hooks in `/etc/pm/` prevalgono rispetto a quelli situati in `/usr/lib/pm-utils/`, per cui l'amministratore di sistema può sovrascrivere le impostazioni di default fornite dalla distribuzione.

### Funzionamento di Pm-suspend

Vedremo come vengono delineate le azioni interne quando viene eseguito `pm-suspend`, descrivendo come `pm-utils` ricada nuovamente sul metodo **kernel** se i requisiti di altri metodi non sono soddisfatti.

```
$ pm-suspend

```

Il primo passo è quello di un set up preliminare delle variabili e degli script principali (genitori):

```
export STASHNAME=pm-suspend
export METHOD="$(echo ${0##*pm-} |tr - _)"
. "/usr/lib/pm-utils/pm-functions"

```

La variabile `METHOD` viene estratta dal nome del file eseguibile, *suspend* da `pm-suspend` e *hibernate* da `pm-hibernate`.

La posizione dei parametri di configurazione di runtime è definito in `/usr/lib/pm-utils/pm-functions` come `PM_UTILS_RUNDIR="/var/run/pm-utils"` e `STORAGEDIR="${PM_UTILS_RUNDIR}/${STASHNAME}/storage"`. Pertanto `STORAGEDIR="/var/run/pm-utils/pm-suspend/storage"` è dove `pm-suspend` posiziona la cache della sua configurazione. Gli hooks disabilitati sono memorizzati in un file di testo contentente il nome dell'hook preceduto da "*disable_hook:*". I parametri di configurazione vengono aggiunti al file *parameters*:

 `$  ls -lah /var/run/pm-utils/pm-suspend/storage/ ` 
```
-rw-r--r-- 1 root root  20 May 19 09:57 disable_hook:99video
-rw-r--r-- 1 root root   0 May 19 02:59 parameters
-rw-r--r-- 1 root root 247 May 19 02:59 parameters.rm
-rw-r--r-- 1 root root   9 May 19 02:59 state:cpu0_governor
-rw-r--r-- 1 root root   9 May 19 02:59 state:cpu1_governor
```

Successivamente `pm-functions` processerà le fonti dei file presenti in `/etc/pm/config.d/` in aggiunta a `/usr/lib/pm-utils/defaults`. Dopodichè, `pm-functions` procederà a controllare le fonti specificate dalla variabile **$SLEEP_METHOD** come `/usr/lib/pm-utils/module.d/$SLEEP_METHOD[...]` se esistenti:

```
for mod in $SLEEP_MODULE; do
    mod="${PM_UTILS_LIBDIR}/module.d/${mod}"
    [ -f "$mod" ] || continue
    . "$mod"
done

```

Altrimenti, se **$SLEEP_MODULE** risulta vuoto, `do_suspend()` sarà impostato dal backend *kernel*, come descritto sopra:

```
if [ -z "$SUSPEND_MODULE" ]; then
    if grep -q mem /sys/power/state; then
       SUSPEND_MODULE="kernel"
       do_suspend() { echo -n "mem" >/sys/power/state; }
    elif [ -c /dev/pmu ] && pm-pmu --check; then
       SUSPEND_MODULE="kernel"
       do_suspend() { pm-pmu --suspend; }
    elif grep -q standby /sys/power/state; then
       SUSPEND_MODULE="kernel"
       do_suspend() { echo -n "standby" >/sys/power/state; }
    fi
fi

```

Assumendo che **$SLEEP_MODULE** non sia vuoto, e che sia specificato il backend `uswsusp`, `/usr/lib/pm-utils/module.d/uswsusp` verrà eseguito. Questo script controlla che siano rispettati diversi requisiti (questi sono i requisiti per essere in grado di utilizzare uswsusp):

*   [ -z $SUSPEND_MODULE ]
*   command_exists s2ram
*   grep -q mem /sys/power/state || ( [ -c /dev/pmu ] && pm-pmu --check; );

Se questi requisiti sono soddisfatti, `do_suspend()` è definita come:

```
do_suspend()
{
   uswsusp_get_quirks
   s2ram --force $OPTS
}

```

Ma soprattutto, il modulo `uswsusp` viene eseguito:

```
add_before_hooks uswsusp_hooks
add_module_help uswsusp_help

```

La prioma funzione, *add_before_hook*, disabilita gli hook **pm-utils** e **99video**, in quanto questa funzionalità viene sostituita da **s2ram**. La seconda funzione, *add_module_help*, aggiunge in aiuto uswsusp-module-specific, che in sostanza sostituisce la funzione di aiuto fornito da **99video**.

Ritornare a `pm-suspend`:

```
command_exists "check_$METHOD" && command_exists "do_$METHOD"
"check_$METHOD"

```

Questo verifica che i metodi *check_suspend* e *do_suspend* siano stati definiti. Il metodo *check_suspend* verifica semplicemente che la variabile $SUSPEND_MODULE non sia vuota:

```
check_suspend() { [ -n "$SUSPEND_MODULE" ]; }

```

Infine, `pm-suspend` deve eseguire tutti gli hook che non sono stati disabilitati, sincronizza il buffer del file-system, ed esegue *do_suspend*:

```
if run_hooks sleep "$ACTION $METHOD"; then
    # Sleep only if we know how and if a hook did not inhibit us.
    log "$(date): performing $METHOD"
    sync
    "do_$METHOD" || r=128
    log "$(date): Awake."

```

Il metodo *run_hooks* è un wrapper per *_run_hooks*, nel casi che `pm-suspend` sia chiamato come *run_hooks sleep "suspend suspend"*. Premesso che:

```
PARAMETERS="${STORAGEDIR}/parameters"
PM_UTILS_LIBDIR="/usr/lib/pm-utils"
PM_UTILS_ETCDIR="/etc/pm"

```

Il metodo *_run_hooks*, sarà valido per ogni hook presente in `${PM_UTILS_LIBDIR}/$1.d` e `${PM_UTILS_ETCDIR}/$1.d`, verificando che la sospensione non li abbi inibiti e aggiornando i parametri di runtime memorizzati in `$PARAMETERS`, prima che venga eseguito ogni hook tramite `run_hook $hook $2`. Nel caso della sospensione in ram (Suspend-to-RAM), tutti gli hook presenti in `/usr/lib/pm-utils/sleep.d/,/etc/pm/sleep.d/` verranno enumerati, e *run_hook* passerà i parametri *$hook* e "*suspend suspend*". Il metodo *run_hook* utilizza la funzione *hook_ok* per verificare che l'hook non sia stato disattivato, prima di eseguire l'hook con il parametro "*suspend suspend*".

## Risoluzione dei problemi

Nel caso la sospensione o l'ibernazione non sia avvenuta correttamente, potrete trovare probabilmente delle informazioni nel file di log `/var/log/pm-suspend.log`. Ad esempio quali hook sono stati eseguiti e l'output del loro stato in uscita, dovrebbero essere presenti in quel file di log.

Inoltre, controllare l'output del comando `pm-is-supported`. Questo comando (con il flag `--Hibernate` o `--suspend`) farà qualche controllo di integrità e segnalerà eventuali errori rilevati nella configurazione. Non è in grado di rilevare tutti i possibili errori, ma può ancora essere utile.

### Segmentation faults

Se si riscontrano difetti di segmentazione che potrebbe causare il blocco del sistema e di chiavi mancanti, provare a impostare l'UUID nei punti di montaggio in `/boot/grub/menu.lst` come spiegato [sopra](#Ibernazione_.28suspend2disk.29).

### Il sistema si riavvia invece di ripristinarsi dalla sospensione

Questo problema è iniziato quando è stato introdotto nel kernel il salvataggio dell'area NVS durante la sospensione (dal kernel 2.6.35-rc4) ([messaggio sulla mailing list](http://www.spinics.net/lists/linux-acpi/msg29521.html)). Tuttavia, è noto che questo meccanismo non funziona su tutte le macchine, gli sviluppatori del kernel sono venuti in aiuto consentendo all'utente di disabilitarla tramite l'aggiunta dell'opzione `acpi_sleep=nonvs` alla riga del kernel. Questa opzione potrebbe essere passare al kernel attraverso le opzioni di [GRUB Legacy](/index.php/GRUB_Legacy_(Italiano) "GRUB Legacy (Italiano)") modificando il file `/boot/grub/menu.lst` (GRUB 0,97) sulla linea del `kernel`.

### Il sistema si spegne invece di ripristinarsi dalla sospensione

Su un Acer Aspire AS3810TG, riprendendo dalla sospensione si spegne il computer, invece di ripristinarsi. Se si verifica un problema simile, si provi a passare il parametro `i8042.reset=1` al kernel. In [GRUB2](/index.php/GRUB2_(Italiano) "GRUB2 (Italiano)"), la riga in `/boot/grub/grub.cfg` dovrebbe essere qualcosa simile a questo:

```
  linux /vmlinuz-linux root=/dev/vg00/root resume=/dev/vg00/swap i8042.reset=1 ro

```

Anceh se non testato, si potrebbe impostare questo parametro senza la necessità di riavviare il sistema, dando il seguente comando:

```
# sysctl -e -w i8042.reset=1

```

### Schermo nero al ripristino dalla sospensione

Alcuni portatili (ad esempio Dell Inspiron Mini 1018) mostrano una schermata nera senza retroilluminazione dopo il ripristino dalla sospensione. Se questo accade, provate a entrare nel BIOS del computer portatile e disabilitare il parametro `Intel SpeedStep`, se presente.

Si potrebbe provare anche di non disabilitare SpeedStep, creando un piccolo script in `/etc/pm/sleep.d/` con questo contenuto (richiede [vbetool](https://www.archlinux.org/packages/?name=vbetool)):

```
#!/bin/sh
#
case "$1" in
suspend)
;;
resume)
sleep 5
vbetool dpms off
vbetool dpms on
;;
*) exit $NA
;;
esac
```

Salvatelo nominandolo come desiderate, ma anteponete `00` all'inizio del nome, in questo modo verrà richiamato per ultimo quando il sistema si ripristinerà dalla sospensione; ricordarsi di dare i permessi di esecuzione, tramite il comando `chmod +x`, allo script. Provate a cambiare il valore del tempo di `sleep` se gli altri comandi vengono richiamati troppo presto, o nel caso funzioni a dovere potete anche eliminare quella stringa. Altri laptop (ad esempio Toshiba Portégé R830) presenteranno semplicemente uno schermo nero senza luminosità dopo il resume dalla sospensione, con le ventole alla massima velocità. Nel caso accadesse ciò, si provi a disabilitare dal BIOS il VT-d virtualization setting passando a "VT-x only".

### Problemi con VirtualBox

I moduli del kernel per VirtualBox causano il fallimento di `pm-suspend` e [[ic|pm-hibernate}} su alcuni laptop. (Vedi [questa discussione](https://bbs.archlinux.org/viewtopic.php?id=123354)). Invece di sospendere o di ibernare, il sistema si blocca e fa lampeggiare il LED (l'indicatore di sospensione nei ThinkPad sono gli indicatori Caps Lock e Scroll Lock, nel caso della MSI Wind U100). I log di `pm-suspend` e `pm-hibernate` sembrano normali.

Il problema può essere risolto rimuovendo i moduli prima della sospensione o della ibernazione e di ricaricarli in seguito. Ciò può essere realizzato attraverso uno script:

```
#!/bin/sh

 rmmod vboxdrv
 pm-hibernate
 modprobe vboxdrv
```

**Nota:** Alcuni utenti riportano che sia sufficiente ricompilare il modulo del kernel eseguendo `vboxbuild` da root.

### Ibernazione in assenza di una partizione di Swap

Se si tenta di ibernare senza una partizione di swap attiva, il sistema effettuerà la procedura di ibernazione, ma poi subito riprenderà di nuovo. Non ci sono messaggi di errore e di avviso che non vi è alcuna partizione di swap, anche quando è attivata la registrazione dettagliata, quindi questo problema può essere molto difficile da rilevare eseguendo il debug. Su un sistema, la partizione di swap è stata in qualche modo danneggiata e disattivata, per cui questo può accadere anche se si imposta una partizione di swap durante l'installazione. Se l'ibernazione visualizza questo comportamento, assicurarsi che effettivamente sia presente una partizione di swap che viene utilizzato come tale. L'output del comando `blkid` dovrebbe somigliare, come esempio, a questo:

```
# blkid
/dev/sda1: UUID="00000-000-000-0000000" TYPE="ext2" 
/dev/sda2: UUID="00000-000-000-0000000" TYPE="ext4"
/dev/sda3: UUID="00000-000-000-0000000" TYPE="ext4"
/dev/sda4: UUID="00000-000-000-0000000" TYPE="swap"
```

con una delle linee che hanno `"swap"` alla voce `TYPE=`. Se questo non è il caso, consultare il [wiki su Swap](/index.php/Swap#Swap_partition "Swap") per le istruzioni su come ricreare e/o riattivare una partizione di swap.

### Schermo nero con cursore fisso quando si tenta di sospendere il sistema

Se si ottiene una schermata nera con il cursore fisso quando si cerca di sospendere con:

```
$ Sudo pm-suspend

```

controllare il file `/var/log/pm-suspend.log` e si cerchi "ehci" o "xhci". Alcuni dei nomi che si possono leggere potrebbero essere "ehci_hd", "xhci_hd" o "ehci_hcd".

In seguito come root creare il file `/etc/pm/config.d/modules` e inserire questo codice con il nome esatto del modulo *ehci* o *xhci* che avete trovato. Ad esempio:

```
SUSPEND_MODULES = "ehci_hcd"

```

La sospensione dovrebbe ora funzionare.

### Problema schermo nero

Alcuni utenti hanno segnalato problemi con i loro computer portatili che non riprendono correttamente dopo una sospensione o una ibernazione. Ciò è causato dall'hook `autodetect`. Questo può essere disabilitato utilizzando lo stesso metodo per aggiungere l'HOOK `resume`. È sufficiente rimuovere l'hook `autodetect` dall'elenco e seguire le istruzioni per costruire la nuova immagine. Si veda il paragrafo [Hook per il ripristino](#Hook_Mkinitcpio_per_il_ripristino), per maggiori dettagli sulla costruzione della nuova immagine.

**Note:** Se si sta utilizzando [plymouth](/index.php/Plymouth "Plymouth") quest'ultimo potrebbe essere un'altra causa del problema. Aggiungendo `resume` davanti a `plymouth` nell'array "HOOKS" del file `/etc/mkinitcpio.conf` dovrebbe sistemare il problema.

### Impossibile il resume con arch 64 bit

Alcuna combinazioni di scheda madre/bios (nello specifico, conosciute, ci sono alcune Zotac ITX, forse altre) non si riprenderanno correttamente dalla sospensione se è installato un os a 64bit. La soluzione è di entrare nella configurazione del BIOS e disabilitare "Memory Remapping Hole" nella pagina della configurazione DRAM. Questo probabilmente sistemerà il problema della sospensione su ram, ma avrà anche come effetto che il tuo sistema operativo non rileverà tutta la tua ram.

## Trucchi e Consigli / FAQ

### Riprendere automaticamente i livelli della gestione dell'alimentazione di un HD dopo la sospensione

Si può procedere come segue:

 `/etc/pm/sleep.d/50-hdparm_pm` 
```

 #!/bin/dash

 if [ -n "$1" ] && ([ "$1" = "resume" ] || [ "$1" = "thaw" ]); then
 	hdparm -B 254 /dev/sda > /dev/null
 fi

```

Quindi eseguire:

```
$ sudo chmod +x /etc/pm/sleep.d/50-hdparm_pm

```

Se lo script in [BASH](/index.php/Bash_(Italiano) "Bash (Italiano)") precedente non funziona, provare il seguente al suo posto:

 `/etc/pm/sleep.d/50-hdparm_pm` 
```
 #!/bin/sh

 . "${PM_FUNCTIONS}"
 case "$1" in
        thaw|resume)
                sleep 6
                hdparm -B 254 /dev/sda
                ;;
        *)
                ;;
 esac
 exit $NA

```

Valori più bassi all'opzione `-B` possono essere più efficaci. Si veda [hdparm](/index.php/Hdparm "Hdparm").

### Riavviare il mouse

Su alcuni portatili il mouse non riprende dopo la sopsensione. Un modo per rimediare è quello di forzare una re-inizializziazione del driver PS/2 (in questo esempio `i8042`) attraverso un hook in `/etc/pm/hooks` (si veda [Creazione di un Hook personale](#Creazione_di_un_Hook_personale))

```
#!/bin/sh  
echo -n "i8042" > /sys/bus/platform/drivers/i8042/unbind
echo -n "i8042" > /sys/bus/platform/drivers/i8042/bind

```

### Aggiungere una modalità sleep al menu di Openbox

Gli utenti che utilizzano Openbox possono aggiungere nuovi script come opzioni adddizionali allo spegnimento del sistema all'interno del menu di openbox aggiungendo gli elementi nuovi o aggiungerli a sotto-menu esistenti in `~/.config/openbox/menu.xml`, ad esempio:

```
<menu id="64" label="Shutdown">
	<item label="Lock"> <action name="Execute"> <execute>xscreensaver-command -lock</execute> </action> </item>
	<item label="Logout"> <action name="Exit"/> </item>
	<item label="Reboot"> <action name="Execute"> <execute>sudo shutdown -r now</execute> </action> </item>
	<item label="Poweroff"> <action name="Execute"> <execute>sudo shutdown -h now </execute> </action> </item>
	***<item label="Hibernate"> <action name="Execute"> <execute>sudo pm-hibernate</execute> </action> </item>***
	***<item label="Suspend"> <action name="Execute"> <execute>sudo pm-suspend</execute> </action> </item>***
</menu>

```

### Modificare i pulsanti "sleep" e "power"

Il comportamento dei pulsanti "Sleep" e "power" può essere modificato tramite `acpid` in `/etc/acpi/handler.sh` (si vedano le voci "button/power" e "power/sleep" ). Si consiglia di sostituire le chiamate predefinite con `pm-suspend` e `pm-hibernate`.

### Bloccare lo schermo quando si iberna o si sospende

Si potrebbe desiderare che venga eseguito un lock screen prima della sospensione o ibernazione (di modo che venga richiesta una password al resume). Questo può essere fatto aggiungendo uno script alla cartella `/etc/pm/sleep.d` . Lo script deve essere eseguibile (chmod 755) e di proprietà di `root:root`.

Un semplice script di esempio è:

 `/etc/pm/sleep.d/00screensaver-lock` 
```
 #!/bin/sh
 #
 # 00screensaver-lock: lock workstation on hibernate or suspend

 username= # add username here; i.e.: username=foobar
 userhome=/home/$username
 export XAUTHORITY="$userhome/.Xauthority"
 export DISPLAY=":0"

  case "$1" in
    hibernate|suspend)
       su $username -c "/usr/bin/slimlock" & # or any other such as /usr/bin/xscreensaver-command -lock
       ;;
    thaw|resume)
       ;;
    *) exit $NA
       ;;
 esac
```

Modifica `/usr/bin/slimlock` col percorso del tuo screen lock.

Se non si desidera scrivere il proprio username nello script (ad esempio se si hanno più utenti), allora è necessario determinare il nome utente e il display della corrente sessione X. Per i sistemi che usano [systemd](/index.php/Systemd "Systemd"), esiste [xuserrun](https://github.com/rephorm/xuserrun) e il seguente script (modificare il percorso a xuserrun e il lock screen desiderato):

 `/etc/pm/sleep.d/00screensaver-lock` 
```
 #!/bin/sh
 #
 # 00screensaver-lock: lock workstation on hibernate or suspend

  case "$1" in
    hibernate|suspend)
       /path/to/xuserrun /usr/bin/slimlock & # or any other such as /usr/bin/xscreensaver-command -lock
       ;;
    thaw|resume)
       ;;
    *) exit $NA
       ;;
 esac

```

### Disabilitare l'ibernazione tramite polkit

Per disabilitare l'ibernazione, creare un nuovo file in /etc/polkit-1/ called 99-disable-hibernate.rules. Aggiungere poi le seguenti linee:

 `99-disable-hibernate.rules` 
```
polkit.addRule(function(action, subject) {
   if ((action.id == "org.freedesktop.login1.hibernate")) {
      return polkit.Result.NO;
   }
});

polkit.addRule(function(action, subject) {
   if ((action.id == "org.freedesktop.login1.hibernate-multiple-sessions")) {
      return polkit.Result.NO;
   }
});

```

Se si sta usando KDE, terminare la sessione una volta sola e l'opzione per ibernare dovrebbe essere sparita.

## Ulteriori Risorse

*   [OpenSUSE Wiki](http://en.opensuse.org/SDB:Pm-utils) - L'articolo da cui è stato originariamente presa questa pagina (sotto licenza GPL)
*   [Comprendere la sospensione](https://wiki.ubuntu.com/UnderstandingSuspend) - Articolo su sistema ubuntu che espone come lavora la sospensione su ram
*   [PM Debugging](http://www.mjmwired.net/kernel/Documentation/power/basic-pm-debugging.txt#178) - Debugging di base per PM
*   [CPU Frequency Scaling](/index.php/CPU_frequency_scaling_(Italiano) "CPU frequency scaling (Italiano)") - selettore per scalare le frequenze sulle CPU e schemi di risparmio energetico CPU
*   [Acpid](/index.php/Acpid_(Italiano) "Acpid (Italiano)") - Demone per gli eventi ACPI.
*   [Hibernate after sleep](http://superuser.com/questions/298672/linuxhow-to-hibernate-after-a-period-of-sleep) - Un esempio di hook di pm personalizzato in cui l'ibernazione è attivata dopo un periodo di tempo in sospensione.