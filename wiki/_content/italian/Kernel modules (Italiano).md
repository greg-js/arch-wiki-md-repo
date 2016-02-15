I moduli del [kernel](https://en.wikipedia.org/wiki/it:Kernel "wikipedia:it:Kernel") sono file di codice che possono essere caricati e rimossi dal kernel su richiesta. Essi estendono le funzionalità del kernel senza bisogno di riavviare il sistema. In questo articolo saranno approfonditi i metodi per la gestione dei moduli del kernel.

## Contents

*   [1 Panoramica](#Panoramica)
*   [2 Ottenere informazioni](#Ottenere_informazioni)
*   [3 Configurazione](#Configurazione)
    *   [3.1 Caricamento](#Caricamento)
    *   [3.2 Impostazione delle opzioni](#Impostazione_delle_opzioni)
        *   [3.2.1 Usando i file in /etc/modprobe.d/](#Usando_i_file_in_.2Fetc.2Fmodprobe.d.2F)
        *   [3.2.2 Usando la riga di comando del kernel](#Usando_la_riga_di_comando_del_kernel)
    *   [3.3 Alias](#Alias)
    *   [3.4 Blacklist](#Blacklist)
        *   [3.4.1 Usando i file in /etc/modprobe.d/](#Usando_i_file_in_.2Fetc.2Fmodprobe.d.2F_2)
        *   [3.4.2 Uso della riga di comando del kernel](#Uso_della_riga_di_comando_del_kernel)
*   [4 Gestione manuale dei moduli](#Gestione_manuale_dei_moduli)
*   [5 Trucchi e Consigli](#Trucchi_e_Consigli)
    *   [5.1 Funzione bash per elencare i parametri dei moduli](#Funzione_bash_per_elencare_i_parametri_dei_moduli)
*   [6 Altre risorse](#Altre_risorse)

## Panoramica

La creazione di un modulo del kernel è descritta in [questa guida](http://tldp.org/LDP/lkmpg/2.6/html/index.html). Un modulo può essere configurato per essere _build-in_ (incluso nel kernel) o _loadable_ (caricabile a richiesta). Per caricare o rimuovere dinamicamente un modulo, esso deve essere configurato come _loadable_ nella configurazione del kernel (la riga relativa al modulo mostrerà perciò la lettera `M`).

I moduli vengono archiviati nel percorso `/usr/lib/modules/_versione_del_kernel_` (per ottenere la versione del kernel usare il comando `uname -r`).

**Nota:** Nella nomenclatura dei moduli spesso compare il simbolo di _underscore_ (`_`) o il _dash_ (`-`), però nell'uso del comando `modprobe` oppure all'interno dei file di configurazione nella cartella `/etc/modprobe.d/` questi simboli sono perfettamente intercambiabili.

## Ottenere informazioni

Per mostrare quali moduli sono attualmente caricati:

```
$ lsmod

```

Per ottenere informazioni riguardo ad un modulo:

```
$ modinfo _nome_modulo_

```

Per elencare le opzioni configurate per un modulo caricato:

```
$ systool -v -m _nome_modulo_

```

Per controllare la configurazione di tutti i moduli:

```
$ modprobe -c | less

```

Per controllare la configurazione di uno specifico modulo:

```
$ modprobe -c | grep _nome_modulo_

```

Per elencare le dipendenze di un modulo (o un alias), incluso il modulo stesso:

```
$ modprobe --show-depends _nome_modulo_

```

## Configurazione

Ad oggi, tutti i moduli necessari da caricare sono gestiti automaticamente da [udev](/index.php/Udev_(Italiano) "Udev (Italiano)"), cosicché, se non si vuole usare qualcuno dei moduli fuori dal kernel, non c'è bisogno di mettere i moduli che dovrebbero essere caricati al boot in nessun file di configurazione. Tuttavia, ci sono casi in cui si vuole caricare un modulo extra durante il processo di avvio oppure evitare il caricamento di un altro perché il computer funzioni correttamente.

### Caricamento

I moduli extra al kernel da caricare durante il boot sono configurati in una lista statica in `/etc/modules-load.d/`. Ogni file di configurazione ha il nome nello stile di `/etc/modules-load.d/_programma_.conf/`. I files di configurazione dovrebbero semplicemente contenere una lista con i nomi dei moduli da caricare, separati da ritorni a capo. Le linee vuote o quelle il cui primo carattere non è né uno spazio né `#` né `;` sono ignorate. Ad esempio:

 `/etc/modules-load.d/virtio-net.conf` 

```
# Carica virtio-net.ko al boot
virtio-net
```

vedere `man 5 modules-load.d` per maggiori dettagli.

### Impostazione delle opzioni

Per passare parametri al modulo del kernel è possibile utilizzare un file di configurazione oppure la linea di comando del kernel.

#### Usando i file in /etc/modprobe.d/

La directory `/etc/modprobe.d/` può essere usata per passare la configurazione dei moduli a [udev](/index.php/Udev_(Italiano) "Udev (Italiano)"), il quale utilizza `modprobe` per gestire il caricamento dei moduli durante l'avvio del sistema. È possibile usare file di configurazione con qualunque nome in tale directory, purché terminino con l'estensione `.conf`. La sintassi è:

 `/etc/modprobe.d/mionomefile.conf`  `options nomemodulo nomeparametro=valoreparametro` 

Ad esempio:

 `/etc/modprobe.d/thinkfan.conf` 

```
#Sui Thinkpad, questo permette al demone 'thinkfan' di controllare la velocità delle ventole.
options thinkpad_acpi fan_control=1
```

**Nota:** Se qualcuno dei moduli coinvolti è caricato dal ramdisk di init, si dovranno aggiungere i necessari file _.conf_ all'array `FILES` in [mkinitcpio.conf](/index.php/Mkinitcpio_(Italiano) "Mkinitcpio (Italiano)"), o usare l'[hook](/index.php/Mkinitcpio_(Italiano)#HOOKS "Mkinitcpio (Italiano)") `modconf`, in maniera che i moduli siano inclusi nel ramdisk.

#### Usando la riga di comando del kernel

Se il modulo è compilato nel kernel è possibile passare le opzioni al modulo utilizzando la linea di comando del kernel. Tutti i bootloader più comuni supportano la seguente sintassi:

```
nomemodulo.nomeparametro=valoreparametro

```

Ad esempio:

```
thinkpad_acpi.fan_control=1

```

Basta semplicemente aggiungere queste opzioni alla linea del kernel per il proprio bootloader come descritto in [Kernel parameters](/index.php/Kernel_parameters "Kernel parameters").

### Alias

Gli alias sono nomi alternativi per un modulo. Ad esempio `alias mio-mod lunghissimo_nome_modulo` permette di usare `modprobe mio-mod` invece di `modprobe lunghissimo_nome_modulo`. Si possono anche usare wildcard come nella shell, per cui `alias mio-mod* lunghissimo_nome_modulo` permette di usare `modprobe mio-mod-qualcosa` con il medesimo risultato. Creare un alias:

 `/etc/modprobe.d/myalias.conf`  `alias mio-mod lunghissimo_nome_modulo` 

Alcuni moduli hanno alias che vengono utilizzati per il loro caricamento automatico quando vengono richiesti da una applicazione. Disabilitando questi alias verrà impedito il caricamento automatico, ma sarà comunque possibile caricarli manualmente.

 `/etc/modprobe.d/modprobe.conf` 

```
#Impedisci il caricamento automatico di Bluetooth.

alias net-pf-31 off
```

### Blacklist

Con l'espressione "mettere un modulo in blacklist" si intende il meccanismo che impedisce al kernel di caricare tale modulo. Questo può essere usato anche quando la periferica hardware associata al modulo non viene utilizzata e non si desidera farla funzionare, oppure perché il caricamento del modulo crea problemi: ad esempio potrebbe verificarsi il caricamento contemporaneo di due moduli che cercano di controllare la stessa periferica o componente hardware, creando quindi un conflitto.

Alcuni moduli vengono caricati in quanto parte dell'[initramfs](/index.php/Mkinitcpio_(Italiano) "Mkinitcpio (Italiano)"). Usando il comando `mkinitcpio -M` verranno mostrati tutti i moduli caricati dal hook `autodetect`: per impedire all'initramfs di caricare alcuni di quei moduli, sarà necessario inserirli in blacklist tramite il file `/etc/modprobe.d/modprobe.conf`. Utilizzando il comando `mkinitcpio -v` verranno elencati tutti i moduli inseriti nell'initramfs da tutti gli hook (ad esempio dal hook filesystem, dal hook SCSI eccetera). Ricordarsi di rigenerare l'initramfs una volta inseriti i moduli in blacklist.

#### Usando i file in /etc/modprobe.d/

Creare un file `.conf` all'interno della cartella `/etc/modprobe.d/` ed inserire all'interno una riga per ogni modulo che si desidera mettere in blacklist, usando la parola chiave `blacklist`. Ad esempio se si desidera impedire il caricamento del modulo `pcspkr`:

 `/etc/modprobe.d/nobeep.conf` 

```
# Non caricare il modulo pcspkr all'avvio
blacklist pcspkr
```

**Nota:** L'uso dell'opzione `blacklist` impedisce il caricamento automatico del modulo. Questo potrebbe però essere caricato nel caso in cui fosse dipendenza di un secondo modulo. E quindi, nel momento in cui quest'ultimo venisse caricato, verrebbe fatto lo stesso anche per il primo, nonostante il blacklist.

Esiste comunque un modo di evitare questo inconveniente; utilizzando l'opzione `install` sarà possibile eseguire un comando personalizzato invece di inserire il modulo in memoria, si potrà quindi forzare il fallimento nel caricamento del modulo usando:

 `etc/modprobe.d/blacklist.conf` 

```
...
install _nome_modulo_ /bin/false
...
```

Questo impedirà il caricamento del modulo e di tutti quelli che da esso dipendono.

#### Uso della riga di comando del kernel

**Tip:** Questo metodo è utile nel caso in cui un modulo mal funzionante impedisce il corretto avvio del sistema.

Si può inoltre impedire il caricamento dei moduli tramite il bootloader. Aggiungere `modprobe.blacklist=modname1,modname2,modname3` ai parametri del kernel. Leggere [kernel parameters](/index.php/Kernel_parameters "Kernel parameters") per maggiori informazioni.

**Nota:** Quando si mette in blacklist più di un modulo, fare attenzione a separarli solamente con virgole. Spazi o altri caratteri potrebbero infrangere la sintassi.

## Gestione manuale dei moduli

I moduli del kernel sono gestiti per mezzo di applicazioni fornite dal pacchetto [kmod](https://www.archlinux.org/packages/?name=kmod). Queste possono anche essere utilizzate manualmente.

Per caricare un modulo:

```
# modprobe _nome_modulo_

```

Per rimuovere un modulo:

```
# modprobe -r _nome_modulo_

```

O, in alternativa:

```
# rmmod _nome_modulo_

```

## Trucchi e Consigli

### Funzione bash per elencare i parametri dei moduli

Qui sotto è presentata una funzione bash, da usare come root, che mostra una lista di tutti i moduli attualmente caricati insieme a tutti i loro parametri, compreso il loro valore corrente. Utilizza `/proc/modules` per recuperare la lista dei moduli caricati, quindi accede al file del modulo direttamente con modinfo per ottenere una descrizione del modulo e le descrizioni per ogni parametro (se disponibile), ed infine accede al filesystem sysfs per ottenere i nomi dei parametri ed i loro valori.

```
function aa_mod_parameters () 
{ 
    N=/dev/null;
    C=`tput op` O=$(echo -en "\n`tput setaf 2`>>> `tput op`");
    for mod in $(cat /proc/modules|cut -d" " -f1);
    do
        md=/sys/module/$mod/parameters;
        [[ ! -d $md ]] && continue;
        m=$mod;
        d=`modinfo -d $m 2>$N | tr "\n" "\t"`;
        echo -en "$O$m$C";
        [[ ${#d} -gt 0 ]] && echo -n " - $d";
        echo;
        for mc in $(cd $md; echo *);
        do
            de=`modinfo -p $mod 2>$N | grep ^$mc 2>$N|sed "s/^$mc=//" 2>$N`;
            echo -en "\t$mc=`cat $md/$mc 2>$N`";
            [[ ${#de} -gt 1 ]] && echo -en " - $de";
            echo;
        done;
    done
}
```

Ed ecco un esempio di output:

 `# aa_mod_parameters` 

```
>>> ehci_hcd - USB 2.0 'Enhanced' Host Controller (EHCI) Driver
        hird=0 - hird:host initiated resume duration, +1 for each 75us (int)
        ignore_oc=N - ignore_oc:ignore bogus hardware overcurrent indications (bool)
        log2_irq_thresh=0 - log2_irq_thresh:log2 IRQ latency, 1-64 microframes (int)
        park=0 - park:park setting; 1-3 back-to-back async packets (uint)

>>> processor - ACPI Processor Driver
        ignore_ppc=-1 - ignore_ppc:If the frequency of your machine gets wronglylimited by BIOS, this should help (int)
        ignore_tpc=0 - ignore_tpc:Disable broken BIOS _TPC throttling support (int)
        latency_factor=2 - latency_factor: (uint)

>>> usb_storage - USB Mass Storage driver for Linux
        delay_use=1 - delay_use:seconds to delay before using a new device (uint)
        option_zero_cd=1 - option_zero_cd:ZeroCD mode (1=Force Modem (default), 2=Allow CD-Rom (uint)
        quirks= - quirks:supplemental list of device IDs and their quirks (string)
        swi_tru_install=1 - swi_tru_install:TRU-Install mode (1=Full Logic (def), 2=Force CD-Rom, 3=Force Modem) (uint)

>>> video - ACPI Video Driver
        allow_duplicates=N - allow_duplicates: (bool)
        brightness_switch_enabled=Y - brightness_switch_enabled: (bool)
        use_bios_initial_backlight=Y - use_bios_initial_backlight: (bool)
```

Di seguito è riportata una variazione della funzione precedente che include una descrizione completa per ogni parametro. L'output è formattato in maniera leggermente diversa ed usa più colori.

```
function show_mod_parameter_info ()
{
  if tty -s <&1
  then
    green="\e[1;32m"
    yellow="\e[1;33m"
    cyan="\e[1;36m"
    reset="\e[0m"
  else
    green=
    yellow=
    cyan=
    reset=
  fi
  newline="
"

  while read mod
  do
    md=/sys/module/$mod/parameters
    [[ ! -d $md ]] && continue
    d="$(modinfo -d $mod 2>/dev/null | tr "\n" "\t")"
    echo -en "$green$mod$reset"
    [[ ${#d} -gt 0 ]] && echo -n " - $d"
    echo
    pnames=()
    pdescs=()
    pvals=()
    pdesc=
    add_desc=false
    while IFS="$newline" read p
    do
      if [[ $p =~ ^[[:space:]] ]]
      then
        pdesc+="$newline    $p"
      else
        $add_desc && pdescs+=("$pdesc")
        pname="${p%%:*}"
        pnames+=("$pname")
        pdesc=("    ${p#*:}")
        pvals+=("$(cat $md/$pname 2>/dev/null)")
      fi
      add_desc=true
    done < <(modinfo -p $mod 2>/dev/null)
    $add_desc && pdescs+=("$pdesc")
    for ((i=0; i<${#pnames[@]}; i++))
    do
      printf "  $cyan%s$reset = $yellow%s$reset\n%s\n" \
        ${pnames[i]} \
        "${pvals[i]}" \
        "${pdescs[i]}"
    done
    echo

  done < <(cut -d' ' -f1 /proc/modules | sort)
}

```

## Altre risorse

*   [modprobe man page](http://linuxmanpages.com/man5/modprobe.conf.5.php)
*   [Disable PC Speaker Beep](/index.php/Disable_PC_Speaker_Beep "Disable PC Speaker Beep")