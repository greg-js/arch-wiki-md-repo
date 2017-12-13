Articoli correlati

*   [Power saving](/index.php/Power_saving "Power saving")
*   [Laptop Mode Tools](/index.php/Laptop_Mode_Tools_(Italiano) "Laptop Mode Tools (Italiano)")
*   [pm-utils](/index.php/Pm-utils_(Italiano) "Pm-utils (Italiano)")
*   [PHC](/index.php/PHC "PHC")

[Cpufreq](https://www.kernel.org/doc/Documentation/cpu-freq/index.txt) consente al sistema operativo di scalare la velocità della CPU verso l'alto o verso il basso in modo da risparmiare energia. Le frequenze della CPU possono essere scalati automaticamente a seconda del carico del sistema, in risposta agli eventi ACPI, o manualmente da programmi userspace. Gestori della variazione

CPU frequency scaling è implementato nel kernel Linux, l'infrastruttura è chiamata *cpufreq*. Dalla versione del kernel 3.4 i moduli necessari sono caricati automaticamente e il governatore raccomandato [ondemand](#Gestori_della_variazione) è abilitato in maniera predefinita. Tuttavia gli strumenti a livello utente come [cpupower](https://www.archlinux.org/packages/?name=cpupower), [acpid](/index.php/Acpid_(Italiano) "Acpid (Italiano)") , [laptop-mode-tools](/index.php/Laptop_Mode_Tools_(Italiano) "Laptop Mode Tools (Italiano)") o le GUI fornite dagli ambienti desktop possono essere ancora utilizzati per la configurazione avanzata.

## Contents

*   [1 tool userspace](#tool_userspace)
    *   [1.1 cpupower](#cpupower)
    *   [1.2 Estensione per GNOME Shell](#Estensione_per_GNOME_Shell)
    *   [1.3 Granola](#Granola)
*   [2 Driver per la frequenza della CPU](#Driver_per_la_frequenza_della_CPU)
    *   [2.1 Impostare una frequenza Massima e Minima](#Impostare_una_frequenza_Massima_e_Minima)
*   [3 Gestori della variazione](#Gestori_della_variazione)
    *   [3.1 Ottimizzare il governatore ondemand](#Ottimizzare_il_governatore_ondemand)
        *   [3.1.1 Soglia di commutazione (threshold)](#Soglia_di_commutazione_.28threshold.29)
        *   [3.1.2 Sampling rate (Frequenza di campionamento)](#Sampling_rate_.28Frequenza_di_campionamento.29)
*   [4 Interazione con gli eventi ACPI](#Interazione_con_gli_eventi_ACPI)
*   [5 Concessione dei privilegi sotto Gnome](#Concessione_dei_privilegi_sotto_Gnome)
*   [6 Risoluzione dei problemi](#Risoluzione_dei_problemi)
    *   [6.1 Limitazione BIOS della frequenza](#Limitazione_BIOS_della_frequenza)
*   [7 Altre risorse](#Altre_risorse)

## tool userspace

### cpupower

[cpupower](https://www.archlinux.org/packages/?name=cpupower) è un insieme di utility in userspace che contribuire ad assicurare *lo scaling della frequenza della CPU*. Il pacchetto non è richiesto per l'uso dello scaling, ma è altamente consigliato in quanto fornisce utility a riga di comando e uno servizio per cambiare il governatore all'avvio.

Il file di configurazione di [cpupower](https://www.archlinux.org/packages/?name=cpupower) è situato in `/etc/default/cpupower`. Questo file di configurazione viene letto da script bash situati in `/usr/lib/systemd/scripts/cpupower`, i quali vengono attivati da *systemd* tramite `cpupower.service`. Si consiglia di abilitare `cpupower.service` all'avvio.

### Estensione per GNOME Shell

Diversi frontend per GNOME Shell sono disponibili in [AUR](/index.php/Arch_User_Repository_(Italiano) "Arch User Repository (Italiano)"):

*   [gnome-shell-cpufreq-git](https://aur.archlinux.org/packages/gnome-shell-cpufreq-git/)
*   [gnome-shell-extension-cpupower-git](https://aur.archlinux.org/packages/gnome-shell-extension-cpupower-git/) (ultimo aggiornamento per la versione 3.6 di GNOME)

### Granola

[Granola](https://aur.archlinux.org/packages/Granola/) (disponibile in [AUR](/index.php/Arch_User_Repository_(Italiano) "Arch User Repository (Italiano)")) è un demone che controlla l'utilizzo della CPU e utilizza il [governatore userspace](#Gestori_della_variazione) per diminuire il consumo di energia senza alcuna differenza notevole nelle prestazioni. Le impostazioni predefinite funzionano per la maggior parte delle configurazioni .

Per testare se funziona, eseguire :

```
 $ cat /sys/devices/system/cpu/cpu0/cpufreq/cpuinfo_cur_freq

```

e verificare che la frequenza della CPU è inferiore al massimo.

## Driver per la frequenza della CPU

**Nota:**

*   Dalla versione 3.4 del kernel, i moduli nativi della CPU sono caricati automaticamente.
*   A partire dal kernel 3.9, il nuovo driver `pstate` per lo scaling di potenza viene usato automaticamente per le moderne CPU Intel al posto degli altri driver elencati sotto. Questo driver ha la priorità su tutti gli altri, e infatti è all'interno del kernel invece di essere un modulo da caricare. Questo driver è attualmente utilizzato automaticamente per tutti i tipi di CPU Sandy Bridge e Ivy Bridge. Se si verifica un problema durante l'utilizzo di questo driver, aggiungere `intel_pstate=disable` alla linea del kernel. É possibile utilizzare le solite utility in userpace con questo driver, ma non possono controllarne l'utilizzo.
*   Anche il comportamento di P State, menzionato sopra, può essere influenzato con `/sys/devices/system/cpu/intel_pstate`, ad esempio, Intel Turbo Boost può essere disattivato con `# echo 1> /sys/devices/system/cpu/intel_pstate/no_turbo` per mantenere basse le temperature delle CPU.
*   Un controllo supplementare per le CPU Intel moderne è disponibile con il [Linux Thermal Daemon](https://01.org/linux-thermal-daemon) ( disponibile su AUR con il pacchetto [thermald](https://www.archlinux.org/packages/?name=thermald)), che controlla la temperatura in modo pro-attivo utilizzando i P-states, T-states, e il driver Intel power clamp.

*cpupower* necessita di moduli per conoscere i limiti della cpu nativa.

| Module | Description |
| acpi-cpufreq | CPUFreq driver che utilizza le ACPI Processor Performance States. Questo driver supporta anche i processori Intel Enhanced Speedstep (precedentemente supportato dal deprecato modulo speedstep-centrino). |
| speedstep-lib | CPUFreq driver per processori Intel che abilita lo SpeedStep (per lo più Atom e vecchi Pentium (<3)). |
| powernow-k8 | CPUFreq driver processori K8/K10 Athlon64/Opteron/Phenom. **Deprecato dalla versione linux 3.7 - Utilizzare acpi_cpufreq.** |
| pcc-cpufreq | Questo driver supporta l'interfaccia di controllo della frequenza di Clock dei processori da Hewlett-Packard e Microsoft Corporation, che è utile in alcuni server Proliant. |
| p4-clockmod | CPUFreq driver processori Intel Pentium 4/XEON/Celeron. Quando è abilitato lo abbasserà soltanto la temperatura della CPU saltando la frequenza di clocks.
Probabilmente si preferisce usare un driver Speedstep al suo posto. |

Per visualizzare un elenco completo dei moduli disponibili, eseguire :

```
$ ls /lib/modules/$(uname -r)/kernel/drivers/cpufreq/

```

Caricare il modulo appropriato (vedi [Kernel modules](/index.php/Kernel_modules "Kernel modules") per i dettagli). Una volta che avete caricato il driver appropriato per la gestione della frequenza della CPU, potrete ottenere delle informazioni dettagliate lanciando il seguente comando:

```
$ cpupower frequency-info

```

### Impostare una frequenza Massima e Minima

In rari casi , può essere necessario impostare manualmente le frequenze massima e minima.

Per impostare la frequenza massima di clock (*clock_freq* è la frequenza di clock espressa in unità: GHz, MHz):

```
# cpupower frequency-set -u *clock_freq*

```

Per impostare la frequenza minima di clock:

```
# cpupower frequency-set -d *clock_freq*

```

Per impostare il processore ad una determinata frequenza:

```
# cpupower frequency-set -f *clock_freq*

```

**Nota:**

*   Per regolare la frequenza solo per un singolo core della CPU, aggiungere `-c *core_number*`.
*   Il governatore e le frequenze massimo e minimo possono essere impostati in `/etc/default/cpupower`.

## Gestori della variazione

I gestori della variazione (Governor - vedi tabella sotto) sono gli schemi di alimentazione per la CPU. Può essere attivo solo un governatore alla volta. Per maggiori dettagli si veda la [documentazione ufficiale](https://www.kernel.org/doc/Documentation/cpu-freq/governors.txt) nei sorgenti del kernel.

| Governor | Descrizione |
| ondemand | Passa dinamicamente tra le varie frequenze disponibili per le CPU(s) se il carico della cpu raggiunge il 95% |
| performance | Fa funzionare le CPU(s) alla frequenza massima |
| conservative | Passa gradualmente tra le varie frequenze disponibili per le CPU(s) se il carico della cpu raggiunge il 75% |
| powersave | Fa funzionare le CPU(s) alla frequenza minima |
| userspace | Fa funzionare le CPU(s) alla frequenza specificata dall'utente |

A seconda del driver per lo scaling utilizzato, uno di questi governatori sarà caricato per impostazione predefinita:

*   `ondemand` per AMD e vecchie CPU Intel.
*   `powersave` per CPU Intel Sandybridge e successive.

Per attivare una particolare governatore, eseguire :

```
# cpupower frequency-set -g *governor*

```

**Nota:**

*   Per regolare la frequenza solo per un singolo core della CPU, aggiungere `-c *core_number*` al comando sopra.
*   Attivando un governatore, lo specifico [modulo del kernel](/index.php/Kernel_modules "Kernel modules") richiesto (denominato `cpufreq_*governatore*`) viene caricato. A partire dal kernel 3.4, questi moduli vengono caricati automaticamente.

In alternativa, è possibile attivare manualmente un governatore su ogni CPU disponibile :

```
 # echo *governor* | tee /sys/devices/system/cpu/cpu*/cpufreq/scaling_governor >/dev/null

```

**Suggerimento:** Per monitorare la velocità della CPU in tempo reale, eseguire :
```
 $ watch grep \"cpu MHz\" /proc/cpuinfo

```

### Ottimizzare il governatore ondemand

Vedere la [documentazione del kernel](https://www.kernel.org/doc/Documentation/cpu-freq/governors.txt) per i dettagli.

#### Soglia di commutazione (threshold)

Per impostare la soglia massima per passare ad un'altra frequenza

```
# echo -n *percent* > /sys/devices/system/cpu/cpufreq/*governor*/up_threshold

```

Per impostare la soglia minima per passare ad un'altra frequenza

```
# echo -n *percent* > /sys/devices/system/cpu/cpufreq/*governor*/down_threshold

```

#### Sampling rate (Frequenza di campionamento)

Il Sampling rate determina l'intervallo con cui il governatore effettua un controllo per regolare la frequenza della cpu. Impostare il `sampling_down_factor` maggiore di 1 migliora le prestazioni riducendo l'overhead di valutazione del carico e mantiene la CPU alla frequenza massima di clock a causa del carico elevato. Questo parametro non ha alcun effetto sul comportamento a frequenze/carichi inferiori della CPU.

Per leggere l'attuale valore (default=1), eseguire:

```
$ cat /sys/devices/system/cpu/cpufreq/ondemand/sampling_down_factor

```

Per impostare un valore, eseguire:

```
# echo -n *valore* > /sys/devices/system/cpu/cpufreq/ondemand/sampling_down_factor

```

## Interazione con gli eventi ACPI

Gli utenti possono configurare i gestori della variazione in modo tale che varino automaticamente in base agli eventi ACPI, come il collegamento all'adattatore di corrente o la chiusura di un coperchio del portatile. Un esempio veloce è riportata qui sotto, ma si consiglia la lettura dell'articolo completo su [acpid](/index.php/Acpid_(Italiano) "Acpid (Italiano)").

Gli eventi sono definiti in `/etc/acpi/handler.sh`. Se il pacchetto [acpid](https://www.archlinux.org/packages/?name=acpid) è installato, il file deve già esistere ed essere eseguibile. Ad esempio, per cambiare il governatore da `performance` a `conservative` quando l'adattatore CA viene scollegato, e viceversa se ricollegata:

 `/etc/acpi/handler.sh` 
```
[...]

 ac_adapter)
     case "$2" in
         AC*)
             case "$4" in
                 00000000)
                     echo "conservative" >/sys/devices/system/cpu/cpu0/cpufreq/scaling_governor    
                     echo -n $minspeed >$setspeed
                     #/etc/laptop-mode/laptop-mode start
                 ;;
                 00000001)
                     echo "performance" >/sys/devices/system/cpu/cpu0/cpufreq/scaling_governor
                     echo -n $maxspeed >$setspeed
                     #/etc/laptop-mode/laptop-mode stop
                 ;;
             esac
         ;;
         *) logger "ACPI action undefined: $2" ;;
     esac
 ;;

[...]

```

## Concessione dei privilegi sotto Gnome

**Nota:** Systemd ha introdotto logind, che gestisce le azioni consolekit e policykit. di conseguenza il seguente codice qui sotto non funziona. Con logind, si editi semplicemente nel file `/usr/share/polkit-1/actions/org.gnome.cpufreqselector.policy` la voce *defaults* con ciò che si necessita, in base alle direttive del manuale di polkit [[1]](http://www.freedesktop.org/software/polkit/docs/latest/polkit.8.html)

[GNOME](/index.php/GNOME_(Italiano) "GNOME (Italiano)") include un gradevole applet per cambiare il governatore al volo. Per usarlo senza la necessità di inserire la password di root bisogna creare il file :

 `/var/lib/polkit-1/localauthority/50-local.d/org.gnome.cpufreqselector.pkla` 
```
[org.gnome.cpufreqselector]
Identity=unix-user:*utente*
Action=org.gnome.cpufreqselector
ResultAny=no
ResultInactive=no
ResultActive=yes
```

Dove la parola *utente* deve essere rimpiazzata con il proprio nome utente.

Il pacchetto [desktop-privileges](https://aur.archlinux.org/packages/desktop-privileges/) contenuto in [AUR](/index.php/AUR_(Italiano) "AUR (Italiano)") contiene un file .pkla simile, per autorizzare tutti gli utenti del [gruppo](/index.php/Users_and_groups_(Italiano) "Users and groups (Italiano)") `power` di cambiare il governatore.

## Risoluzione dei problemi

*   Alcune applicazioni, come [ntop](/index.php/Ntop_(Italiano) "Ntop (Italiano)"), non rispondono bene alla variazione di frequenza automatica. Nel caso di ntop può causare difetti di segmentazione e un sacco di informazioni perse. Allo stesso modo il governatore `ondemand` non può cambiare la frequenza abbastanza rapidamente quando molti di pacchetti arrivano improvvisamente alla interfaccia di rete monitorata che non possono essere gestiti da la velocità del processore corrente.

*   Alcune CPU possono soffrire di scarse prestazioni con le impostazioni predefinite del governatore `ondemand` (ad esempio i video in flash possono soffrire di rallentamenti, o scatti nelle animazioni delle finestre). Invece di disabilitare completamente il frequency scaling per risolvere questi problemi, l'aggressività dello variazione di frequenza può essere aumentata riducendo la variabile [sysctl](/index.php/Sysctl "Sysctl") *up_threshold* per ogni CPU. Si veda [Modifica della soglia (threshold) del governatore 'ondemand'](#Modifica_della_soglia_.28threshold.29_del_governatore_.27ondemand.27).

*   A volte il governatore `ondemand` non può acceleratore alla frequenza massima, ma un gradino sotto. Questo può essere risolto impostando il valore max_freq ad uno leggermente superiore a quella massima reale. Per esempio, se la gamma di frequenza della CPU va da 2,00 GHz a 3,00 GHz, impostare max_freq a 3,01 GHz può essere una soluzione.

*   Alcune combinazioni di driver [ALSA](/index.php/ALSA "ALSA") e chip sonori possono causare il salto dell'audio quando i governatori cambiano tra le frequenze, al passaggio del governatore l'audio potrebbe interrompersi per un attimo o saltare.

### Limitazione BIOS della frequenza

Alcune configurazioni CPU/BIOS possono avere difficoltà a scalare le frequenze massime o scalare alla massima frequenza disponibile. Questo è probabilmente causato da eventi del BIOS che dicono al sistema operativo di limitare la frequenza con la conseguenza di impostare `/sys/devices/system/cpu/cpu0/cpufreq/bios_limit` al valore minimo.

Oppure, se si sono cambiate specifiche impostazione nel BIOS Setup Utility (frequenza , gestione termica , ecc), si può incolpare un BIOS danneggiato/obsoleto, altrimenti il BIOS potrebbe avere un motivo valido per limitare la frequenza della CPU.

Motivi del genere possono essere (se il vostro computer è un notebook ) causati da una rimozione incauta della batteria (o se sia prossima alla morte ), in modo da essere costretti ad utilizzare solo la rete elettrica. In questo caso, un debole alimentatore AC potrebbe non fornire energia elettrica sufficiente a soddisfare le richieste di picco estreme del sistema generale, e quando non vi è alcuna batteria inserita di supporto, potrebbe portare alla perdita di dati , la corruzione dei dati o nel peggiore dei casi , anche a danni hardware!

Non tutti i BIOS limitano la frequenza della CPU, in questo caso , ma per esempio accade sulla maggior parte dei IBM/Thinkpad Lenove, per maggiori informazioni relativi ai thinkpad, fare riferimento a thinkwiki [su questa discussione](http://www.thinkwiki.org/wiki/Problem_with_CPU_frequency_scaling).

Se avete controllato che non è solo un comportamento strano dell'ambiente BIOS e si sa cosa si sta facendo, allora si può dire al Kernel di ignorare questa limitazione del BIOS.

**Attenzione:** Assicurarsi di aver letto e compreso quanto descritto nella sezione precedente. La limitazione di frequenza della CPU è una caratteristica di sicurezza del vostro BIOS e non dovrebbe essere necessario lavorarci sopra. E bene capirne la causa prima.

Un speciale parametro deve essere passato al modulo del processore.

Per effetuare una prova temporanea, modificare il valore in `/sys/module/processor/parameters/ignore_ppc` da 0 a 1.

Per impostarlo in maniera permanente, si faccia riferimento alla pagina [Kernel parameters](/index.php/Kernel_parameters "Kernel parameters") o continuare a leggere. Aggiungere `processor.ignore_ppc=1` alla linea di caricamento del kernel o creare :

 `/etc/modprobe.d/ignore_ppc.conf` 
```
# If the frequency of your machine gets wrongly limited by BIOS, this should help
options processor ignore_ppc=1
```

## Altre risorse

*   [Linux CPUFreq - kernel documentation](https://www.kernel.org/doc/Documentation/cpu-freq/index.txt)
*   [spiegazione completa di pstate](http://www.reddit.com/r/linux/comments/1hdogn/acpi_cpufreq_or_intel_pstates/)