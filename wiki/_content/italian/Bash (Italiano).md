**Bash** (Bourne-again Shell) è una shell/linguaggio di programmazione appartenente al [progetto GNU](/index.php/GNU_Project "GNU Project"). Il suo nome è un omaggio al suo predecessore: la deprecata da tempo Bourne shell. Bash può essere eseguita su molti sistemi operativi UNIX-like, incluso GNU/Linux. Arch utilizza Bash per tutti i suoi init-scripts(script di avvio).

## Contents

*   [1 Invocazione](#Invocazione)
    *   [1.1 Login shell](#Login_shell)
    *   [1.2 Interactive shell](#Interactive_shell)
    *   [1.3 POSIX compliance](#POSIX_compliance)
    *   [1.4 Legacy mode](#Legacy_mode)
*   [2 Configurazione](#Configurazione)
    *   [2.1 Panoramica dei file di configurazione](#Panoramica_dei_file_di_configurazione)
        *   [2.1.1 /etc/profile](#.2Fetc.2Fprofile)
        *   [2.1.2 .profile](#.profile)
        *   [2.1.3 .bashrc](#.bashrc)
    *   [2.2 Ordine del source dei file di configurazione](#Ordine_del_source_dei_file_di_configurazione)
    *   [2.3 Shell e variabili d'ambiente](#Shell_e_variabili_d.27ambiente)
*   [3 Riga di comando](#Riga_di_comando)
*   [4 Alias](#Alias)
*   [5 Funzioni](#Funzioni)
*   [6 Trucchi e Consigli](#Trucchi_e_Consigli)
    *   [6.1 Personalizzazione del prompt](#Personalizzazione_del_prompt)
    *   [6.2 Auto-completamento](#Auto-completamento)
        *   [6.2.1 Completamento avanzato](#Completamento_avanzato)
        *   [6.2.2 Completamento veloce](#Completamento_veloce)
    *   [6.3 Disabilitare Ctrl+z nel terminale](#Disabilitare_Ctrl.2Bz_nel_terminale)
    *   [6.4 Ripulire lo schermo dopo il log out](#Ripulire_lo_schermo_dopo_il_log_out)
    *   [6.5 ASCII art, fortune e cowsay](#ASCII_art.2C_fortune_e_cowsay)
    *   [6.6 Calendario storico ASCII](#Calendario_storico_ASCII)
    *   [6.7 Personalizzare il Titolo](#Personalizzare_il_Titolo)
*   [7 Altre risorse](#Altre_risorse)

## Invocazione

Il comportamento di Bash può essere variato a seconda di come viene invocato. Alcune descrizioni dei diversi modi vengono riportati sotto.

### Login shell

Se Bash viene avviato da `login` in una tty. da un demone [SSH](/index.php/Secure_Shell_(Italiano) "Secure Shell (Italiano)"), o simili, viene considerato una login shell. Questo modo può essere ottenuto tramite l'uso delle opzioni `-l` oppure `--login` dalla riga di comando.

### Interactive shell

Bash è considerato una interactive shell se viene avviato senza l'utilizzo dell'opzione `-c` nè di altri argomenti che non siano opzioni, ed il cui standard input e standard error vengano indirizzati al terminale.

### POSIX compliance

Bash può essere eseguito con una maggiore conformità agli standard POSIX, avviando Bash utilizzando l'opzione `--posix` da riga di comando oppure eseguendo ‘`set -o posix`’ durante l'esecuzione di Bash.

### Legacy mode

In Arch `/bin/sh` (che era l'eseguibile per la Bourne shell) è un link simbolico a `/bin/bash`.

Se Bash viene invocato usando il nome `sh`, tenterà di imitare il solito comportamento di avvio della storica versione di `sh`, il più simile possibile, e cercherà anche di attenersi agli standard POSIX.

In questa modalità, Bash effettua il source dei file di avvio ed entrerà in **POSIX compliance**.

## Configurazione

### Panoramica dei file di configurazione

*   `/etc/profile`
*   `~/.bash_profile`
*   `~/.bash_login`
*   `~/.profile`
*   `/etc/bash.bashrc` (*Non-standard*: solo alcune distro, Arch inclusa)
*   `~/.bashrc`
*   `~/.bash_logout`

Una panoramica dei file di configurazione comunemente usati:

#### /etc/profile

Viene effettuato il source di `/etc/profile` da tutte le shell compatibili con la Bourne shell al momento del login. Imposta l'ambiente al login e carica le configurazioni specifiche per applicazione (`/etc/profile.d/*.sh`).

#### .profile

Questo file viene letto e ne viene effettuato il source da bash quando si effettua un login ed una shell interattiva viene avviata.

#### .bashrc

Il file `~/.bashrc` viene letto e ne viene effettuato il source da bash quando viene invocata senza login e senza una shell interattiva, ad esempio, quando si avvia una console virtuale dal proprio desktop environment. Questo file è utile per impostare l'ambiente specifico dell'utente.

### Ordine del source dei file di configurazione

Questi file vengono presi in considerazione da bash per il source in diverse circostanze.

*   se interattiva + login shell → `/etc/profile` poi il primo leggibile tra `~/.bash_profile`, `~/.bash_login`, e `~/.profile`
    *   Bash effettuerà il source di `~/.bash_logout` all'uscita.
*   se interattiva + non-login shell → `/etc/bash.bashrc` poi `~/.bashrc`
*   se login shell + legacy mode → `/etc/profile` poi `~/.profile`

Ma in Arch, per default:

*   `/etc/profile` (indirettamente) effettua il source di `/etc/bash.bashrc`
*   `/etc/skel/.bash_profile` che gli utenti sono incoraggiati a copiare in `~/.bash_profile`, effettua il source di `~/.bashrc`

il che implica che `/etc/bash.bashrc` e `~/.bashrc` saranno eseguiti per tutte le shell interattive, sia che siano login shell o meno.

Esempi dei file punto possono essere trovati in `/etc/skel/`.

**Nota:** legacy mode è quando viene invocato il comando `sh`

### Shell e variabili d'ambiente

La capacità di Bash e dei programmi eseguiti tramite essa, è che possono essere influenzati da un numero di variabili di ambiente. Le variabili d'ambiente sono usate per memorizzare valori come i percorsi contenenti gli eseguibili, oppure quale browser usare. Quando una shell o uno script viene lanciato esso eredita le sue variabili genitrici, questo a partire da una serie di variabili shell interne[[1]](http://www.kingcomputerservices.com/unix_101/understanding_unix_shells_and_environment_variables.htm).

Queste variabili possono essere esportate per far si che diventino variabili d'ambiente:

```
VARIABILE=contenuto
export VARIABILE

```

Oppure con un solo comando

```
export VARIABILE=content

```

Le variabili d'ambiente sono convenzionalmente contenute nel file `~/.profile` o in `/etc/profile` così che tutte le shell compatibili con la shell di Bourne possano utilizzarle.

Consultare [Environment variables](/index.php/Environment_variables "Environment variables") per maggiori informazioni.

## Riga di comando

La riga di comando di Bash è gestita da una libreria separata chiamata [Readline](/index.php/Readline_(Italiano) "Readline (Italiano)"). Readline fornisce molte scorciatoie da tastiera per interagire con la riga di comando ad esempio per spostarsi prima o dopo una parola, cancellare una parola eccetera. Spetta Readline gestire la [cronologia](/index.php/Readline_(Italiano)#Cronologia "Readline (Italiano)") dei comandi eseguiti. Ed inoltre, permette di creare delle [macro](/index.php/Readline_(Italiano)#Macro "Readline (Italiano)").

## Alias

[alias](https://en.wikipedia.org/wiki/alias "wikipedia:alias") è un comando, che abilita l'uso di una parola al posto di un'altra stringa. Esso viene spesso utilizzato per abbreviare un comando, o per aggiungere opzioni o argomenti ad un comando utilizzato regolarmente.

Gli alias personalizzati sono preferibilmente contenuti nel file `~/.bashrc`, mentre gli alias di sistema (che verranno utilizzati da tutti gli utenti) devono essere inseriti in `/etc/bash.bashrc`.

## Funzioni

Bash supporta anche l'uso delle funzioni. La seguente funzione estrarrà un ampio insieme di tipi di file compressi. Aggiungere la funzione al file `~/.bashrc` e viene utilizzato secondo la seguente sintassi `extract <file1> <file2> ...`:

```
~/.bashrc

```

```
extract() {
    local c e i

    (($#)) || return

    for i; do
        c=''
        e=1

        if [[ ! -r $i ]]; then
            echo "$0: file is unreadable: \`$i'" >&2
            continue
        fi

        case $i in
        *.t@(gz|lz|xz|b@(2|z?(2))|a@(z|r?(.@(Z|bz?(2)|gz|lzma|xz)))))
               c='bsdtar xvf';;
        *.7z)  c='7z x';;
        *.Z)   c='uncompress';;
        *.bz2) c='bunzip2';;
        *.exe) c='cabextract';;
        *.gz)  c='gunzip';;
        *.rar) c='unrar x';;
        *.xz)  c='unxz';;
        *.zip) c='unzip';;
        *)     echo "$0: unrecognized file extension: \`$i'" >&2
               continue;;
        esac

        command $c "$i"
        e=$?3
    done

    return $e
}

```

**Nota:** Gli utenti di Bash dovranno assicurarsi che `extglob` sia abilitato: `shopt -s extglob`, ad esempio aggiungendolo al file `.bashrc`. Viene abilitato di default se si utilizza il [completamento di Bash](#Completamento_avanzato). Gli utenti di [Zsh](/index.php/Zsh "Zsh") dovranno invece lanciare il comando: `setopt kshglob`.

Un altro metodo per fare questo è installare il pacchetto [unp](https://www.archlinux.org/packages/?name=unp).

## Trucchi e Consigli

### Personalizzazione del prompt

Il prompt è controllate dalla variabile `$PS1`. Per colorare il prompt di bash, prima commentare la variabile `$PS1` di default:

```
#PS1='[\u@\h \W]\$ '

```

Successivamente aggiungere la seguente riga:

```
PS1='\[\e[0;31m\]\u\[\e[m\] \[\e[1;34m\]\w\[\e[m\] \[\e[0;31m\]\$ \[\e[m\]\[\e[0;32m\] '

```

La variabile `$PS1` sopra è utile per il prompt dell'utente root, la parte iniziale in rosso e il testo della console verde. Per maggiori dettagli sulla personalizzazione del prompt della shell, consultare [Color Bash Prompt](/index.php/Color_Bash_Prompt_(Italiano) "Color Bash Prompt (Italiano)").

### Auto-completamento

Risulta utile avere l'auto-completamento attivo (premendo `Tab` due volte sulla tastiera) dopo che si è inserito un comando come `sudo`.

Per fare questo aggiungere una riga in questo formato nel file `~/.bashrc`:

```
complete -cf your_command

```

Ad esempio, per abilitare l'auto-completamento dopo i comandi `sudo` e `man`:

```
complete -cf sudo
complete -cf man

```

#### Completamento avanzato

Nonostante il supporto nativo per l'auto completamento di Bash per i nomi file, i comandi e le variabili, ci sono diversi metodi per aumentare ed estenere la sua portata.

Il pacchetto [bash-completion](https://www.archlinux.org/packages/?name=bash-completion) estende queste funzionalità aggiungendo l'auto completamento per un ampio numero di comandi ed le loro opzioni. Consentire il completamento avanzato su bash è molto semplice, basta installare il seguente pacchetto:

```
# pacman -S bash-completion

```

Per abilitare il completamento automatico di Bash, basterà avviare una nuova shell e sarà abilitato automaticamente grazie al file `/etc/bash.bashrc`.

#### Completamento veloce

Aggiungendo la seguente riga al file di inizializzazione di [readline](/index.php/Readline_(Italiano) "Readline (Italiano)") (`~/.inputrc` o `/etc/inputrc` di default):

```
set show-all-if-ambiguous on

```

non sarà necessario premere `Tab` (il tasto di default) due volte per ottenere una lista dei possibili completamenti (entrambi quando un parziale completamento sarà possibile), basterà una singola pressione del tasto per ottenerla. In alternativa per ottenere questa lista solo quando nessun completamento è possibile (quando non è possibile un completamento parziale), aggiungere la seguente riga al posto della precedente:

```
set show-all-if-unmodified on

```

### Disabilitare Ctrl+z nel terminale

Si può disabilitare la combinazione `Ctrl+z` (mette in pausa/chiude le applicazioni lanciate nel terminale) inserendo i propri comandi in questo script

```
#!/bin/bash
trap "" 20
/percorso_per_l'applicazione/

```

esempio:

```
#!/bin/bash
trap "" 20
/usr/bin/adom

```

Con questo script di esempio, quando si premerà accidentalmente `Ctrl+z` invece di `Shift+z` o di altre combinazioni, mentre si gioca a Adom(un gioco) il gioco non verrà chiuso. Non succederà nulla perché il comando verrà ignorato.

### Ripulire lo schermo dopo il log out

Per ripulire lo schermo dai precedenti output, una volta effettuato il log out da un terminale viruale, aggiungere le seguenti linee al file `~/.bash_logout`:

```
clear
reset

```

### ASCII art, fortune e cowsay

Oltre ai colori, le informazioni di sistema e i simboli ASCII, Bash può visualizzare dei disegni di ASCII art al login. Le immagini ASCII possono essere trovate online ed incollate all'interno di file di testo, o generate da zero. Per impostare la visualizzazione al login del terminale, inserire la riga

```
cat /percorso/del/file/di/testo

```

all'inizio del file `~/.bashrc`.

Sarà possibile visualizzare frasi commoventi, ispiranti, stupide o maligne in modo casuale. Per vederne un esempio installare il pacchetto [fortune-mod](https://www.archlinux.org/packages/?name=fortune-mod) dal repositroy `extra`.

```
**<font color="red">(</font><font color="green">user@host</font><font color="red">)-(</font><font color="green">10:10 AM Wed Dec 22</font><font color="red">)</font>**<font color="red">--(</font><font color="green">~</font><font color="red">)---> </font> fortune 

It is Texas law that when two trains meet each other at a railroad crossing,
each shall come to a full stop, and neither shall proceed until the other
has gone.
```

Per visualizzare una frase casuale quando si effettua il login in un terminale, aggiungere la riga

```
command fortune

```

all'inizio del file `~/.bashrc`.

**Nota:** Di default, `fortune` visualizza citazioni e frasi innocue. Comunque, il pacchetto contiene una serie di commenti che qualcuno potrebbe ritenere offensive, e si trovano in `/usr/share/fortune/off`. Consultare la pagina di manuale per maggiori informazioni su queste frasi.

Queste due capacità possono essere combinate, uando il programma [cowsay](https://www.archlinux.org/packages/?name=cowsay). Modificare la prima riga del file `~/.bashrc` in

```
command cowsay $(fortune)

```

oppure in

```
command cowthink $(fortune)

```

```
The earth is like a tiny grain of sand, 
only much, much heavier.                
----------------------------------------- 
       \   ^__^
        \  (oo)\_______
           (__)\       )\/\
               ||----w |
               ||     ||

```

Le immagini ASCII possono essere generate dai file di testo `.cow` situati in `/usr/share/cows`, e tutti i temi possono essere elencati con il comando `cowsay -l`. Questi file possono essere modificati a discrezione dell'utente; possono anche essere create immagini personalizzate creandole di sana pianta oppure scaricandole dalla rete. Il modo più semplice per creare un file `cow` da una immagine trovata online è quella di aprire un file `.cow` con un editor di testo, ed incollarvi l'immagine dal browser, successivamente salvarla con un altro nome. Per testare il file personalizzato usare il comando

```
# cowsay -f `cowfile` $(fortune)

```

In questo modo è possibile visualizzare immagini accattivanti ed i comandi possono essere più complessi. Per esempi specifici, consultare [questo sito](http://bambambambam.wordpress.com/2009/07/04/futurama-ascii-with-slashdot-header-quotes-in-your-terminal/). Un altro esempio, di uso casuale di cow, un immagine random, ed una buona formattazione di eventuali testi lunghi di fortunes.

```
fortune -a | fmt -80 -s | cowsay -$(shuf -n 1 -e b d g p s t w y) -f $(shuf -n 1 -e $(cowsay -l | tail -n +2)) -n

```

```
 ________________________________________ 
( Fry: I must be a robot. Why else would )
( human women refuse to date me?         )
---------------------------------------- 
       o
         o
           o  
              ,'``.._   ,'``.
             :,--._:)\,:,._,.:
             :`--,*@@@:`...';\* 
              `,'@@@@@@@`---'@@`.     
              /@@@@@@@@@@@@@@@@@:
             /@@@@@@@@@@@@@@@@@@@\
           ,'@@@@@@@@@@@@@@@@@@@@@:\.___,-.
          `...,---'``````-..._@@@@|:@@@@@@@\
            (                 )@@@;:@@@@)@@@\  _,-.
             `.              (@@@//@@@@@@@@@@`'@@@@\
              :               `.//@@)@@@@@@)@@@@@,@;
              |`.            _,'/@@@@@@@)@@@@)@,'@,'
              :`.`-..____..=:.-':@@@@@.@@@@@_,@@,'
             ,'\ ``--....-)='    `._,@@\    )@@@'``._
            /@_@`.       (@)      /@@@@@)  ; / \ \`-.'
           (@@@`-:`.     `' ___..'@@_,-'   |/   `.)
            `-. `.`.``-----``--,@@.'
              |/`.\`'        ,',');
                  `         (/  (/
**<font color="red">(</font><font color="green">user@host</font><font color="red">)-(</font><font color="green">10:10 AM Wed Dec 22</font><font color="red">)</font>**<font color="red">--(</font><font color="green">~</font>)<font color="red">)---></font>

```

### Calendario storico ASCII

Per installare i file del [calendario](http://www.openbsd.org/cgi-bin/man.cgi?query=calendar&sektion=1) nella cartella `~/.calendar`:

```
$ mkdir -p ~/.calendar
$ curl -o calendar.rpm [http://download.fedora.redhat.com/pub/epel/5/x86_64/calendar-1.25-4.el5.x86_64.rpm](http://download.fedora.redhat.com/pub/epel/5/x86_64/calendar-1.25-4.el5.x86_64.rpm)
$ rpm2cpio calendar.rpm | bsdtar -C ~/.calendar --strip-components=4 -xf - ./usr/share/c*

```

Questo comando visualizzerà gli oggetti nel calendario

```
$ sed -n "/$(date +%m\\/%d\\\|%b\*\ %d)/p" $(find ~/.calendar /usr/share/calendar -maxdepth 1 -type f -name 'c*' 2>/dev/null);

```

### Personalizzare il Titolo

La variabile `$PROMPT_COMMAND` vi permette di eseguire un comando prima del prompt. Ad esempio, è possibile cambiare il titolo con il path completo della directory in cui lavorate:

```
export PROMPT_COMMAND='echo -ne "\033]0;$PWD\007"'

```

## Altre risorse

*   [Advanced Bash Scripting Guide](http://tldp.org/LDP/abs/html/) - Una buona risorsa tratta lo shell scripting usando Bash
*   [Guida Avanzata di scripting Bash](http://www.pluto.it/files/ildp/guide/abs/index.html)
*   [Bash Reference Manual](http://www.gnu.org/software/bash/manual/bashref.html) - Manuale ufficiale (654K)
*   [Bash Hackers Wiki](http://wiki.bash-hackers.org/doku.php) - Excellent Bash Wiki
*   [Bash Scripting ad esempi](http://www.ibm.com/developerworks/linux/library/l-bash.html)
*   [Guida al completamento](http://www.caliban.org/bash)
*   [Greg's Wiki](http://wooledge.org/mywiki/BashFaq) - Altamente raccomandato
*   [Pagina di manuale](http://www.gnu.org/software/bash/manual/bash.html)
*   [Tutorial dei Quote](http://www.grymoire.com/Unix/Quote.html)
*   [irc://irc.freenode.net#bash](irc://irc.freenode.net#bash) - Chat amichevole ed interattiva canale di Bash.
*   [http://chakra-project.org/wiki/index.php/Startup_files](http://chakra-project.org/wiki/index.php/Startup_files)