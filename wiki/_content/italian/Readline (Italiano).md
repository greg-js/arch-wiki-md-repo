**Readline** è una libreria del [progetto GNU](/index.php/GNU_Project "GNU Project") usata da [Bash](/index.php/Bash_(Italiano) "Bash (Italiano)") e da altre interfacce per la linea di comando per modificare ed interagire con la linea di comando. Prima di leggere questo articolo fare riferimento alla [home page](http://www.gnu.org/s/readline/) del progetto dato che in questo articolo saranno introdotte solo semplici configurazioni.

## Contents

*   [1 Editing della linea di comando](#Editing_della_linea_di_comando)
*   [2 Cronologia](#Cronologia)
    *   [2.1 Ricerca nella cronologia](#Ricerca_nella_cronologia)
        *   [2.1.1 Evitare i duplicati](#Evitare_i_duplicati)
        *   [2.1.2 Evitare gli spazi](#Evitare_gli_spazi)
*   [3 Macro](#Macro)
*   [4 Tips and tricks](#Tips_and_tricks)
    *   [4.1 Disabilitare la visualizzazione delle combinazioni control](#Disabilitare_la_visualizzazione_delle_combinazioni_control)

## Editing della linea di comando

Come default Readline usa le combinazioni da tastiera di Emacs, per interagire con la linea di comando. Comunque, è supportata anche la modalità vi. Nel caso siate utenti [vi](/index.php/Vim_(Italiano) "Vim (Italiano)"), probabilmente vorrete inserire la seguente linea nel proprio `~/.inputrc` per abilitare le scorciatoie di vi:

```
set -o vi

```

Esistono a questo scopo le pagine dei trucchi di [vi](http://www.catonmat.net/download/bash-vi-editing-mode-cheat-sheet.pdf) o [emacs](http://www.catonmat.net/download/readline-emacs-editing-mode-cheat-sheet.pdf).

## Cronologia

Solitamente, premendo la freccia che punta in alto, verrà mostrato l'ultimo comando eseguito anche se sono stati digitati alcuni caratteri. Comunque, gli utenti potrebbero trovare più pratico elencare i comandi digitati che hanno una corrispondenza con quanto digitato.

Ad esempio, se l'utente ha digitato i seguenti comandi:

*   `ls /usr/src/linux-2.6.15-ARCH/kernel/power/Kconfig`
*   `who`
*   `mount`
*   `man mount`

In questa situazione, se digitiamo `ls` e successivamente premiamo la freccia su, l'attuale input sarà sostituito con `man mount`, cioè l'ultimo comando eseguito. Avendo la ricerca nella cronologia abilitata, verranno mostrati invece solo i comandi eseguiti che cominciano con `ls` (l'attuale input), in questo caso `ls /usr/src/linux-2.6.15-ARCH/kernel/power/Kconfig`.

Sarà possibile abilitare questa modalità aggiungendo le seguenti linee al file `/etc/inputrc` orppure al file `~/.inputrc`:

```
"\e[A":history-search-backward
"\e[B":history-search-forward

```

Se si usa la modalità "vi" è possibile aggiungere queste righe a `~/.inputrc` (come indicato in [questo posto](https://bbs.archlinux.org/viewtopic.php?pid=428760#p428760)):

```
set editing-mode vi
$if mode=vi
set keymap vi-command
# these are for vi-command mode
"\e[A": history-search-backward
"\e[B": history-search-forward
set keymap vi-insert
# these are for vi-insert mode
"\e[A": history-search-backward
"\e[B": history-search-forward
$endif

```

Se si sceglie di inserire le righe sopra al file `~/.inputrc`, è consigliato aggiungere anche la seguente linea all'inizio del file per evitare strani comportamenti come [questo](https://bbs.archlinux.org/viewtopic.php?id=112537):

```
$include /etc/inputrc

```

In alternativa, si può utilizzare la reverse-search-history (ricerca incrementale) premendo `Ctrl`+`R`, che non effettua una ricerca basata sull'input ma sposta il buffer di ricerca mentre i tasti vengono digitati ed utilizzandoli come termini di ricerca. Premendo nuovamente `Ctrl`+`R` durante questa modalità verrà mostrata la linea precedente nel buffer che corrisponde all'attuale termine di ricerca, mentre premendo `Ctrl`+`G` (abort) verrà annullata la ricerca e riproposto l'input corrente. Quindi per ricercare tra i precedenti comandi `mount`, sarà necessario premere `Ctrl`+`R`, digitare 'mount' e continuare a premere `Ctrl`+`R` finchè non si raggiunge la linea desiderata.

L'equivalente ricerca ma in avanti chiamata forward-search-history è legata alla combinazione `Ctrl`+`S` di default. Attenzione perché molti terminali sovrappongono la combinazione `Ctrl`+`S` per sospendere l'esecuzione fino a che non viene premuta la combinazione `Ctrl`+`Q`. (Questo viene chiamato XON/XOFF flow control). Per attivare la forward-search-history, e quindi disabilitare il flow control eseguire il comando:

```
$ stty -ixon

```

oppure utilizzare un'altra combinazione di tasti nel file `inputrc`. Ad esempio se si vuole utilizzare `Alt`+`S` che solitamente per default non è legato a nessun evento :

```
"\es":forward-search-history

```

### Ricerca nella cronologia

#### Evitare i duplicati

Se si ripetono spesso diversi comandi, essi verranno aggiunti ogni volta alla propria cronologia. Per evitarlo, aggiungere questo al proprio `~/.bashrc`:

```
export HISTCONTROL=ignoredups

```

#### Evitare gli spazi

Per impedire che vengano considerati nella cronologia i comandi vuoti aggiungere questa linea al file `~/.bashrc`:

```
export HISTCONTROL=ignorespace

```

Se nel file è già presente

```
export HISTCONTROL=ignoredups

```

Sostituirlo con

```
export HISTCONTROL=ignoreboth

```

## Macro

Readline supporta anche l'assegnazione di combinazioni di tasti a delle macro. Per esempio, eseguire questo comando in Bash:

```
bind '"\ew":"\C-e # macro"'

```

o aggiungere la parte contenuta tra apici al file `~/.inputrc`:

```
"\ew":"\C-e # macro"

```

Adesso scriviamo una linea e premiamo `Alt`+`W`. Readline si comporterà come se avessimo premuto `Ctrl`+`E` (spostamento a fine riga) ed aggiungerà ' `# macro`'.

Usare ogni possibile combinazione di tasti per una macro tramite readline, può essere molto utile per automatizzare le opreazioni effettuate spesso. Ad esempio questa macro fa si che la combinazione `Ctrl`+`Alt`+`L` aggiunga "| less" alla linea e la esegua (`Ctrl`+`M` equivale a `Enter`):

```
"\e\C-l":"\C-e | less\C-m"

```

Il comando successivo inserisce ad inizio riga la stringa 'yes |' quando viene premuta la combinazione `Ctrl`+`Alt`+`Y`, utile per confermare ogni domanda di tipo yes/no dal terminale:

```
"\e\C-y":"\C-ayes | \C-m"

```

Questo esempio incapsula la linea digitata all'interno di `su -c ''`, se viene premuta la combinazione `Alt`+`S`:

```
"\es":"\C-a su -c '\C-e'\C-m"

```

Come ultimo esempio, per avviare facilmente un comando in background con `Ctrl`+`Alt`+`B`, redirigendo ogni tipo di output:

```
"\e\C-b":"\C-e > /dev/null 2>&1 &\C-m"

```

## Tips and tricks

### Disabilitare la visualizzazione delle combinazioni control

A causa di un aggiornamento di [readline](https://www.archlinux.org/packages/?name=readline), il terminale ora visualizza `^C` dopo aver premuto `Ctrl`+`C`. Per gli utenti che vogliono disabilitare questa visualizzazione, basterà semplicemente aggiungere la seguente linea al file `~/.inputrc`:

```
set echo-control-characters off

```