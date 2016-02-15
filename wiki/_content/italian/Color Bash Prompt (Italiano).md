Esistono varie possibilità per il proprio `prompt` di bash e personalizzarlo aiuterà ad essere più produttivi dalla riga di comando. Si possono aggiungere informazioni al `prompt`, o semplicemente colorarlo per farlo risaltare.

## Contents

*   [1 Prompt basilari](#Prompt_basilari)
    *   [1.1 Prompt un po' più elaborati](#Prompt_un_po.27_pi.C3.B9_elaborati)
*   [2 Prompt avanzati](#Prompt_avanzati)
    *   [2.1 Caricamento Stato della memoria per 256 colori](#Caricamento_Stato_della_memoria_per_256_colori)
    *   [2.2 Lista di colori per il prompt e Bash](#Lista_di_colori_per_il_prompt_e_Bash)
    *   [2.3 Prompt di escape](#Prompt_di_escape)
    *   [2.4 Posizionamento del cursore](#Posizionamento_del_cursore)
    *   [2.5 Visualizzazione valore di ritorno](#Visualizzazione_valore_di_ritorno)
        *   [2.5.1 Visualizzazione del valore di ritorno avanzata](#Visualizzazione_del_valore_di_ritorno_avanzata)
    *   [2.6 Prompt di Wolfman](#Prompt_di_Wolfman)
    *   [2.7 Prompt di KitchM](#Prompt_di_KitchM)
*   [3 Impostazione titolo finestra](#Impostazione_titolo_finestra)
*   [4 Colori diversi per l'immissione di testo e output su console](#Colori_diversi_per_l.27immissione_di_testo_e_output_su_console)
*   [5 Esempi di bashrc da Gentoo](#Esempi_di_bashrc_da_Gentoo)
*   [6 Colori generalizzati per tutti gli utenti](#Colori_generalizzati_per_tutti_gli_utenti)
    *   [6.1 Ripristino del file originale /etc/bash.bashrc file](#Ripristino_del_file_originale_.2Fetc.2Fbash.bashrc_file)
*   [7 Vedere anche](#Vedere_anche)
*   [8 Risorse esterne](#Risorse_esterne)

## Prompt basilari

Le seguenti impostazioni sono utili per distinguere il `prompt` di root da quello di utente normale.

*   Editare il file di configurazione personale di `Bash`:

```
$ nano ~/.bashrc

```

*   Decommentare il `prompt` di default:

```
#PS1='[\u@\h \W]\$ '

```

*   Aggiungere il seguente `prompt` verde per gli utenti normali:

[chiri@zetsubou ~]$ _

```
PS1='\[\e[1;32m\][\u@\h \W]\$\[\e[0m\] '

```

*   Editare il file `.bashrc` per root; copiarlo da `/etc/skel` in caso non sia già presente:

```
# nano /root/.bashrc

```

*   Assegnare il `prompt` rosso per root:

[root@zetsubou ~]# _

```
PS1='\[\e[1;31m\][\u@\h \W]\$\[\e[0m\] '

```

### Prompt un po' più elaborati

*   Un `prompt` verde e blu per utenti normali:

chiri ~/docs $ echo "sample output text" sample output text chiri ~/docs $ _

```
PS1='\[\e[0;32m\]\u\[\e[m\] \[\e[1;34m\]\w\[\e[m\] \[\e[1;32m\]\$\[\e[m\] \[\e[1;37m\]'

```

Questo visualizzerà un `prompt` molto piacevole, colorato con un colore di testo bianco brillante.

La stringa sopra contiene le impostazioni colore per le sequenze di escape (inizio colorazione: `\[\e[color\]`, fine colorazione: `\[\e[m\]`) e le informazioni segnaposto:

*   \u - Nome utente. Il prompt originale ha anche `\h`, che stampa il nome dell'host.
*   \w - Attuale percorso assoluto. Usa `\W` per l'attuale percorso relativo percorso.
*   \$ - Il carattere di prompt (es.`#` per root,`$` per gli utenti normali).

L'ultimo sequenza di colore, `\[\e[1;37m\]`, non è chiusa, in modo che il testo rimanente (tutto quello che è scritto nel terminale, l'output dei programmi e così via) saranno in quel colore (bianco brillante). Può essere auspicabile cambiare questo colore, o cancellare l'ultima sequenza di escape in modo da lasciare l'attuale output con colori inalterati.

*   Un `prompt` rosso e blu per root:

root ~/docs # echo "sample output text" sample output text root ~/docs # _

```
PS1='\[\e[0;31m\]\u\[\e[m\] \[\e[1;34m\]\w\[\e[m\] \[\e[0;31m\]\$ \[\e[m\]\[\e[0;32m\]'

```

Questo darà una denominazione rossa con il testo della console verde.

Una volta effettuate le modifiche al bashrc, per applicare le modifiche.:

$ source ~/.bashrc

## Prompt avanzati

### Caricamento Stato della memoria per 256 colori

Questo non è nemmeno superare i limiti... altro che utilizzare `sed` per analizzare memoria e carico medio (usando l'opzione `-u` per il non-buffering), oppure l'arrangiamento per salvare la cronologia al proprio "HISTFILE" dopo ogni comando. Queste soluzioni sono estremamente utili quando si tratta di crash di shell o subshell, ed essenzialmente si tratta solo di far stampare a `Bash` variabili già note, rendendo l'operazione estremamente veloce rispetto al `prompt` con i comandi builtin.

Questo `prompt` è tratto dall'articolo di AskApache.com, [BASH Power Prompt article](http://www.askapache.com/linux-unix/bash-power-prompt.html), che fornisce maggiore approfondimenti. È particolarmente utile per coloro che vogliono comprendere i terminali a 256 colori, `ncurses`, `termcap` e `terminfo`.

Questo è per **terminali a 256 colori**, che è da dove provengono gli `escape` **\033[38;5;22m**.

```
802/1024MB      1.28 1.20 1.13 3/94 18563
[5416:17880 0:70] 05:35:50 Wed Apr 21 [srot@host.sqpt.net:/dev/pts/0 +1] ~

(1:70)$ _
```

```
 PROMPT_COMMAND='history -a;echo -en "\033[m\033[38;5;2m"$(( `sed -nu "s/MemFree:[\t ]\+\([0-9]\+\) kB/\1/p" /proc/meminfo`/1024))"\033[38;5;22m/"$((`sed -nu "s/MemTotal:[\t ]\+\([0-9]\+\) kB/\1/Ip" /proc/meminfo`/1024 ))MB"\t\033[m\033[38;5;55m$(< /proc/loadavg)\033[m"'
 PS1='\[\e[m\n\e[1;30m\][$$:$PPID \j:\!\[\e[1;30m\]]\[\e[0;36m\] \T \d \[\e[1;30m\][\[\e[1;34m\]\u@\H\[\e[1;30m\]:\[\e[0;37m\]${SSH_TTY} \[\e[0;32m\]+${SHLVL}\[\e[1;30m\]] \[\e[1;37m\]\w\[\e[0;37m\] \n($SHLVL:\!)\$ '

```

### Lista di colori per il prompt e Bash

Aggiungere questo al file di `Bash` per definire i colori per il `prompt` e i comandi:

```
txtblk='\e[0;30m' # Nero - Regular
txtred='\e[0;31m' # Rosso
txtgrn='\e[0;32m' # Verde
txtylw='\e[0;33m' # Giallo
txtblu='\e[0;34m' # Blu
txtpur='\e[0;35m' # Viola
txtcyn='\e[0;36m' # Ciano
txtwht='\e[0;37m' # Bianco
bldblk='\e[1;30m' # Nero - Bold
bldred='\e[1;31m' # Rosso
bldgrn='\e[1;32m' # Verde
bldylw='\e[1;33m' # Giallo
bldblu='\e[1;34m' # Blu
bldpur='\e[1;35m' # Viola
bldcyn='\e[1;36m' # Ciano
bldwht='\e[1;37m' # Bianco
unkblk='\e[4;30m' # Nero - Underline
undred='\e[4;31m' # Rosso
undgrn='\e[4;32m' # Verde
undylw='\e[4;33m' # Giallo
undblu='\e[4;34m' # Blu
undpur='\e[4;35m' # Viola
undcyn='\e[4;36m' # Ciano
undwht='\e[4;37m' # Bianco
bakblk='\e[40m'   # Nero - Background
bakred='\e[41m'   # Rosso
badgrn='\e[42m'   # Verde
bakylw='\e[43m'   # Giallo
bakblu='\e[44m'   # Blu
bakpur='\e[45m'   # Viola
bakcyn='\e[46m'   # Ciano
bakwht='\e[47m'   # Bianco
txtrst='\e[0m'    # Text Reset
```

O se si preferiscono i nomi dei colori o si vogliono colori ad alta intensità:

```
# Reset
Color_Off='\e[0m'       # Text Reset

# Regular Colors
Black='\e[0;30m'        # Nero
Red='\e[0;31m'          # Rosso
Green='\e[0;32m'        # Verde
Yellow='\e[0;33m'       # Giallo
Blue='\e[0;34m'         # Blu
Purple='\e[0;35m'       # Viola
Cyan='\e[0;36m'         # Ciano
White='\e[0;37m'        # Bianco

# Bold
BBlack='\e[1;30m'       # Nero
BRed='\e[1;31m'         # Rosso
BGreen='\e[1;32m'       # Verde
BYellow='\e[1;33m'      # Giallo
BBlue='\e[1;34m'        # Blu
BPurple='\e[1;35m'      # Viola
BCyan='\e[1;36m'        # Ciano
BWhite='\e[1;37m'       # Bianco

# Underline
UBlack='\e[4;30m'       # Nero
URed='\e[4;31m'         # Rosso
UGreen='\e[4;32m'       # Verde
UYellow='\e[4;33m'      # Giallo
UBlue='\e[4;34m'        # Blu
UPurple='\e[4;35m'      # Viola
UCyan='\e[4;36m'        # Ciano
UWhite='\e[4;37m'       # Bianco

# Background
On_Black='\e[40m'       # Nero
On_Red='\e[41m'         # Rosso
On_Green='\e[42m'       # Verde
On_Yellow='\e[43m'      # Giallo
On_Blue='\e[44m'        # Blu
On_Purple='\e[45m'      # Purple
On_Cyan='\e[46m'        # Ciano
On_White='\e[47m'       # Bianco

# High Intensty
IBlack='\e[0;90m'       # Nero
IRed='\e[0;91m'         # Rosso
IGreen='\e[0;92m'       # Verde
IYellow='\e[0;93m'      # Giallo
IBlue='\e[0;94m'        # Blu
IPurple='\e[0;95m'      # Viola
ICyan='\e[0;96m'        # Ciano
IWhite='\e[0;97m'       # Bianco

# Bold High Intensty
BIBlack='\e[1;90m'      # Nero
BIRed='\e[1;91m'        # Rosso
BIGreen='\e[1;92m'      # Verde
BIYellow='\e[1;93m'     # Giallo
BIBlue='\e[1;94m'       # Blu
BIPurple='\e[1;95m'     # Viola
BICyan='\e[1;96m'       # Ciano
BIWhite='\e[1;97m'      # Bianco

# High Intensty backgrounds
On_IBlack='\e[0;100m'   # Nero
On_IRed='\e[0;101m'     # Rosso
On_IGreen='\e[0;102m'   # Verde
On_IYellow='\e[0;103m'  # Giallo
On_IBlue='\e[0;104m'    # Blu
On_IPurple='\e[10;95m'  # Viola
On_ICyan='\e[0;106m'    # Ciano
On_IWhite='\e[0;107m'   # Bianco
```

Per utilizzare i comandi dal proprio ambiente shell:

```
$ echo -e "${txtblu}test"
<font color="blue">test</font>
$ echo -e "${bldblu}test"
<font color="lightblue">**test**</font>
$ echo -e "${undblu}test"
<font color="lightblue">**<u>test</u>**</font>
$ echo -e "${bakblu}test"
**test**

```

Per utilizzare nei `prompt` (notare le virgolette e la barra `\[ \]` usati dalla shell per calcolare la lunghezza corretta):

```
PS1="\[$txtblu\]foo\[$txtred\] bar\[$txtrst\] baz : "

```

### Prompt di escape

Di seguito i vari comandi di escape elencati nella pagina di manuale di bash:

```
Bash permette che queste stringhe di prompt possano essere personalizzate inserendo un
numero di _backslash-escaped special characters_ che vengono interpretati come segue:

  \a         il carattere ASCII beep (07)
  \d         la data nel formato "Giorno-della-settimana Mese Data"
  \D{format} the format is passed to strftime(3) and the result
             is inserted into the prompt string an empty format
             results in a locale-specific time representation.
             The braces are required
  \e         un carattere di escape ASCII (033)
  \h         l'hostname fino al primo `.'
  \H         l'hostname
  \j         the number of jobs currently managed by the shell
  \l         the basename of the shell's terminal device name
  \n         il carattere "newline"
  \r         il carattere "carriage return"
  \s         il nome della shell, il nome base di $0
             (la parte che segue lo slash finale)
  \t         l'ora corrente nel formato 24-ore HH:MM:SS
  \T         l'ora corrente nel formato 12-ore HH:MM:SS
  \@         l'ora corrente nel formato 12-ore am/pm
  \A         the current time in 24-hour HH:MM format
  \u         lo username dell'utente corrente
  \v         la versione di bash (e.g., 2.00)
  \V         la release di bash, versione + patchlevel
             (es, 2.00.0)
  \w         la directory di lavoro corrente, con $HOME abbreviato con una tilde
  \W         il nome di base della directory di lavoro corrente
             abbreviato con una tilde
  \!         il numero cronologico (history number) di questo comando
  \#         il numero di questo comando
  \$         se l'UID effettivo è 0, un #, altrimenti un $
  \nnn       il carattere corrispondente al numero ottale nnn
  \\         un backslash
  \[         comincia una sequenza di caratteri non stampabili, che
             potrebbero essere usati per inserire una sequenza di
             controllo del terminale nel prompt
  \]         termina la sequenza di caratteri non stampabili

  Il numero di comando e il numero della cronologia sono usualmente diversi: 
  il numero della cronologia di una comando è la sua posizione nella lista della 
  cronologia, che potrebbe includere comandi reintegrati dal file di cronologia 
  (vedere HISTORY di seguito), mentre il numero di comando è la posizione nella 
  sequenza di comandi eseguiti durante la sessione di shell attuale. Dopo che la 
  stringa sia stata decodificata, e' espansa attraverso espansione di parametri, 
  sostituzione di comandi, espansione aritmetica, rimozione di apici, soggetta al 
  valore delle opzioni di promptvars della shell (vedere la descrizione del comando 
  shopt sotto SHELL BUILTIN COMMANDS, di seguito).

```

### Posizionamento del cursore

La sequenza che segue imposta la posizione del cursore:

```
\[\033[<row>;<column>f\]

```

La posizione del cursore può essere salvata utilizzando:

```
\[\033[s\]

```

Per ripristinare una posizione, utilizzare la seguente sequenza:

```
\[\033[u\]

```

L'esempio seguente utilizza queste sequenze per visualizzare l'ora in alto a destra:

```
PS1=">\[\033[s\]\[\033[1;\$((COLUMNS-4))f\]\$(date +%H:%M)\[\033[u\]"

```

La variabile d'ambiente _COLUMNS_ contiene il numero di colonne del terminale. L'esempio precedente sottrae 4 dal proprio valore per giustificare i cinque caratteri dell'output largo della "data" sul bordo destro.

### Visualizzazione valore di ritorno

ATTENZIONE
Questo è sembrato non essere esente da bug, vedere la voce aggiunta alla pagina di discussione. È possibile aggiungere un \n dopo la faccina per evitare calcoli sbagliati sulla lunghezza della linea.

Aggiungere questa riga se si desidera vedere il valore di ritorno dell'ultimo comando eseguito. Questo dovrebbe funzionare con qualsiasi tipo di prompt fino a quando non ha bisogno di PROMPT_COMMAND:

```
PROMPT_COMMAND='RET=$?; if [[ $RET -eq 0 ]]; then echo -ne "\033[0;32m$RET\033[0m ;)"; else echo -ne "\033[0;31m$RET\033[0m ;("; fi; echo -n " "'

```

E sarà simile a questo:

```
<font color="green">0</font>** ;)** harvie@harvie-ntb ~/ $ true
<font color="green">0</font>** ;)** harvie@harvie-ntb ~/ $ false
<font color="red">1</font>** ;(** harvie@harvie-ntb ~/ $ 

```

Zero è verde e non-zero è di colore rosso. C'è anche l'indicazione smiley (sostituirlo con quello che si preferisce); così il prompt sorriderà se l'ultima operazione ha avuto successo.

#### Visualizzazione del valore di ritorno avanzata

Se si vogliono i colori, è necessario impostare i valori _$RED_ e _$GREEN_:

```
RED='\e[0;31m'
GREEN='\e[0;32m'

```

È necessario specificare questi valori nei file di configurazione di Bash:

```
#return value visualisation
PROMPT_COMMAND='RET=$?;'
RET_VALUE='$(echo $RET)' #Ret value not colorized - you can modify it.
RET_SMILEY='$(if [[ $RET = 0 ]]; then echo -ne "\[$GREEN\];)"; else echo -ne "\[$RED\];("; fi;)'

```

Quindi è possibile utilizzare le variabili _$RET_VALUE_ e _$RET_SMILEY_ nel prompt. Si noti che è necessario usare le virgolette:

```
#prompt
PS1="$RET_VALUE $RET_SMILEY : "

```

Questo darà un prompt di base:

```
0 <font color="green">;)</font> : true
0 <font color="green">;)</font> : false
1 <font color="red">;(</font> : 

```

Ma probabilmente si desidera utilizzare _$RET_VALUE_ or _$RET_SMILEY_ nel proprio prompt, così:

 `PS1="\[$WHITE\]$RET_VALUE $RET_SMILEY \[$BLUE\]\u\[$RED\]@\[$EBLUE\]\h\[$WHITE\] \W \[$ERED\]\\$\[$EWHITE\] "` 

### Prompt di Wolfman

Dopo aver letto la maggior parte dei [Bash Prompt Howto](http://www.tldp.org/HOWTO/Bash-Prompt-HOWTO/index.html), l'autore ha sviluppato questo prompt di Bash che mostra gli ultimi 25 caratteri della directory di lavoro attuale. I risultati migliori si ottengono su terminali con sfondo nero. Il codice seguente va inserito nel file `~/.bashrc`.

*   Aggiungere la funzione bash_prompt_command. Se si possiedono alcune directory con nomi lunghi o che iniziano con molte sottodirectory, tale funzione evitera' al prompt dei compandi di riempire lo schermo, mostrando al massimo gli ultimi pwdmaxlen caratteri della PWD (directory corrente). Questo codice è tratto dalla sezione _Bash Prompt Howto_ su [Controlling the Size and Appearance of $PWD](http://www.tldp.org/HOWTO/Bash-Prompt-HOWTO/x783.html) e modificato per sostituire la directory home dell'utente con una tilde.

```
##################################################
# Fancy PWD display function
##################################################
# The home directory (HOME) is replaced with a ~
# The last pwdmaxlen characters of the PWD are displayed
# Leading partial directory names are striped off
# /home/me/stuff          -> ~/stuff               if USER=me
# /usr/share/big_dir_name -> ../share/big_dir_name if pwdmaxlen=20
##################################################
bash_prompt_command() {
    # How many characters of the $PWD should be kept
    local pwdmaxlen=25
    # Indicate that there has been dir truncation
    local trunc_symbol=".."
    local dir=${PWD##*/}
    pwdmaxlen=$(( ( pwdmaxlen < ${#dir} ) ? ${#dir} : pwdmaxlen ))
    NEW_PWD=${PWD/#$HOME/\~}
    local pwdoffset=$(( ${#NEW_PWD} - pwdmaxlen ))
    if [ ${pwdoffset} -gt "0" ]
    then
        NEW_PWD=${NEW_PWD:$pwdoffset:$pwdmaxlen}
        NEW_PWD=${trunc_symbol}/${NEW_PWD#*/}
    fi
}

```

*   Questo codice genera il prompt dei comandi in cui sono definiti un paio di colori. Il colore dell'utente per il nome utente, l'hostname e il prompt ($ o #) è impostato a ciano, mentre se l'utente è root (l'UID di root è sempre 0), imposta il colore a rosso. Il prompt dei comandi è una versione colorata del prompt di default di Arch, con NEW_PWD proveniente dalla precedente funzione.

	Si presti inoltre attenzione che le variabili dei colori sono racchiuse tra doppi apici (virgolette), non singoli apici (apostrofi). L'uso di singoli apici sembra creare problemi a bash per la corretta separazione di righe.

```
bash_prompt() {
    case $TERM in
     xterm*|rxvt*)
         local TITLEBAR='\[\033]0;\u:${NEW_PWD}\007\]'
          ;;
     *)
         local TITLEBAR=""
          ;;
    esac
    local NONE="\[\033[0m\]"    # unsets color to term's fg color

    # regular colors
    local K="\[\033[0;30m\]"    # black
    local R="\[\033[0;31m\]"    # red
    local G="\[\033[0;32m\]"    # green
    local Y="\[\033[0;33m\]"    # yellow
    local B="\[\033[0;34m\]"    # blue
    local M="\[\033[0;35m\]"    # magenta
    local C="\[\033[0;36m\]"    # cyan
    local W="\[\033[0;37m\]"    # white

    # emphasized (bolded) colors
    local EMK="\[\033[1;30m\]"
    local EMR="\[\033[1;31m\]"
    local EMG="\[\033[1;32m\]"
    local EMY="\[\033[1;33m\]"
    local EMB="\[\033[1;34m\]"
    local EMM="\[\033[1;35m\]"
    local EMC="\[\033[1;36m\]"
    local EMW="\[\033[1;37m\]"

    # background colors
    local BGK="\[\033[40m\]"
    local BGR="\[\033[41m\]"
    local BGG="\[\033[42m\]"
    local BGY="\[\033[43m\]"
    local BGB="\[\033[44m\]"
    local BGM="\[\033[45m\]"
    local BGC="\[\033[46m\]"
    local BGW="\[\033[47m\]"

    local UC=$W                 # user's color
    [ $UID -eq "0" ] && UC=$R   # root's color

    PS1="$TITLEBAR ${EMK}[${UC}\u${EMK}@${UC}\h ${EMB}\${NEW_PWD}${EMK}]${UC}\\$ ${NONE}"
    # without colors: PS1="[\u@\h \${NEW_PWD}]\\$ "
    # extra backslash in front of \$ to make bash colorize the prompt
}

```

*   Infine, aggiungere questo codice, il quale assicura che la variabile `NEW_PWD` sia aggiornata quando si cambia directory e imposta la variabile PS1, che contiene il `prompt` dei comandi.

```
PROMPT_COMMAND=bash_prompt_command
bash_prompt
unset bash_prompt

```

### Prompt di KitchM

Questi `prompt` offrono una maggiore chiarezza visiva e testo lampeggiante. Si noti che l'uso del colore rosso nel `prompt` dell'utente root potrebbe dare luogo a indicazioni di attenzione.

**Primo**, cambiare lo sfondo di default nelle preferenze del terminale (In questo esempio si usa iul terminal di Xfce) a #D2D2D2, ed il colore del testo a #000000\. I font sono impostati come DejaVu Sans Mono Book 12\. Il colore del cursore è #00AA00, e il colore dell'attività dei tab è #AF0000.

**Secondo**, in `~/.bashrc` dopo la riga PS1=, inserire una nuova riga con il seguente:

```
PS1='\e[1;33;47m\u \e[1;32;47mon \h \e[1;35;47m\d \@\e[0;0m\n\e[1;34m[dir.= \w] \# > \e[0;0m'

```

E poi mettere un # davanti alla prima riga PS1.

**Terzo**, per l'utente root, modificare il file `/root/.bashrc` nello stesso modo per includere:

```
PS1='\e[1;31;47m\u \e[1;32;47mon \h \e[1;35;47m\d \@\e[0;0m\n\e[1;31m[dir.= \w] \# > \e[0;0m'

```

Non dimenticare di commentare la riga vecchia.

Questi sono prompt a doppia linea, e dovrebbero apparire così:

Utente-

```

**Username** **on myhost** **Sun Jan 15 12:30 PM**  
**[dir.= /home/username] 1 >                ** 

```

Root-

```

**Root** **on myhost**  **Sun Jan 15 12:30 PM**           
**[dir.= /etc/rc.d] 1 >                     ** 

```

Si noterà che i colori di sfondo renderanno più confortevole la lettura, ed i colori del testo manterranno le cose un po' più "interessanti". C'è un ampio margine di manovra per personalizzarli a piacere, in modo semplice con l'uso di colori.

## Impostazione titolo finestra

[Xterm](/index.php/Xterm "Xterm") e molti altri emulatori di terminale (PuTTY incluso) consentono di impostare il titolo della finestra utilizzando speciali sequenze di escape. Si possono impostare le variabili `${XTERM_TITLE}` come segue, poi inserirle all'inizio del prompt per impostare il titolo di [xterm](/index.php/Xterm "Xterm") (se disponibile) su directory@user@hostname:

```
#set xterm title
case "$TERM" in
  xterm | xterm-color)
    XTERM_TITLE='\[\e]0;\W@\u@\H\a\]'
  ;;
esac

```

Il testo tra `0;` e `\a` può essere impostato come si preferisce, per esempio:

```
export PS1='\[\e]0;Welcome to ArchLinux\a\]\$>> '

```

imposta il titolo della finestra con "Benvenuto su ArchLinux" e mostra questo messaggio semplice:

 `$>> _` 

## Colori diversi per l'immissione di testo e output su console

Se non si azzera il colore del testo alla fine del prompt, sia il testo inserito che il testo della console rimarranno di quel colore. Se si vuole modificare il testo in un colore speciale, ma si usa ancora il colore predefinito per l'output del comando, è necessario ripristinare il colore dopo aver premuto Invio, ma ancora prima di eseguire qualsiasi comando. È possibile farlo tramite l'installazione di una DEBUG trap nel file `~/.bashrc`, in questo modo:

```
trap 'echo -ne "\e[0m"' DEBUG

```

## Esempi di bashrc da Gentoo

```
# /etc/bash.bashrc
#
# This file is sourced by all *interactive* bash shells on startup,
# including some apparently interactive shells such as scp and rcp
# that can't tolerate any output.  So make sure this doesn't display
# anything or bad things will happen !

# Test for an interactive shell.  There is no need to set anything
# past this point for scp and rcp, and it's important to refrain from
# outputting anything in those cases.

if [[ $- != *i* ]] ; then
	# Shell is non-interactive.  Be done now!
	return
fi

# Bash won't get SIGWINCH if another process is in the foreground.
# Enable checkwinsize so that bash will check the terminal size when
# it regains control.  #65623
# http://cnswww.cns.cwru.edu/~chet/bash/FAQ (E11)
shopt -s checkwinsize

# Enable history appending instead of overwriting.  #139609
shopt -s histappend

# Change the window title of X terminals 
case ${TERM} in
	xterm*|rxvt*|Eterm|aterm|kterm|gnome*|interix)
		PROMPT_COMMAND='echo -ne "\033]0;${USER}@${HOSTNAME%%.*}:${PWD/$HOME/~}\007"'
		;;
	screen)
		PROMPT_COMMAND='echo -ne "\033_${USER}@${HOSTNAME%%.*}:${PWD/$HOME/~}\033\\"'
		;;
esac

use_color=false

# Set colorful PS1 only on colorful terminals.
# dircolors --print-database uses its own built-in database
# instead of using /etc/DIR_COLORS.  Try to use the external file
# first to take advantage of user additions.  Use internal bash
# globbing instead of external grep binary.
safe_term=${TERM//[^[:alnum:]]/?}   # sanitize TERM
match_lhs=""
[[ -f ~/.dir_colors   ]] && match_lhs="${match_lhs}$(<~/.dir_colors)"
[[ -f /etc/DIR_COLORS ]] && match_lhs="${match_lhs}$(</etc/DIR_COLORS)"
[[ -z ${match_lhs}    ]] \
	&& type -P dircolors >/dev/null \
	&& match_lhs=$(dircolors --print-database)
[[ $'\n'${match_lhs} == *$'\n'"TERM "${safe_term}* ]] && use_color=true

if ${use_color} ; then
	# Enable colors for ls, etc.  Prefer ~/.dir_colors #64489
	if type -P dircolors >/dev/null ; then
		if [[ -f ~/.dir_colors ]] ; then
			eval $(dircolors -b ~/.dir_colors)
		elif [[ -f /etc/DIR_COLORS ]] ; then
			eval $(dircolors -b /etc/DIR_COLORS)
		fi
	fi

	if [[ ${EUID} == 0 ]] ; then
		PS1='\[\033[01;31m\]\h\[\033[01;34m\] \W \$\[\033[00m\] '
	else
		PS1='\[\033[01;32m\]\u@\h\[\033[01;34m\] \w \$\[\033[00m\] '
	fi

	alias ls='ls --color=auto'
	alias grep='grep --colour=auto'
else
	if [[ ${EUID} == 0 ]] ; then
		# show root@ when we do not have colors
		PS1='\u@\h \W \$ '
	else
		PS1='\u@\h \w \$ '
	fi
fi

# Try to keep environment pollution down, EPA loves us.
unset use_color safe_term match_lhs
```

## Colori generalizzati per tutti gli utenti

Se si vuole generalizzare l'impiego di colori per tutti gli utenti del sistema, è necessario modificare il file `/etc/bash.bashrc` e creare un file `/etc/DIR_COLORS`. Ecco una generalizzazione possibile con la combinazione di colori di Gentoo per Arch Linux:

/etc/bash.bashrc:

```
# /etc/bash.bashrc
#
# https://wiki.archlinux.org/index.php/Color_Bash_Prompt
#
# This file is sourced by all *interactive* bash shells on startup,
# including some apparently interactive shells such as scp and rcp
# that can't tolerate any output.  So make sure this doesn't display
# anything or bad things will happen !

# Test for an interactive shell.  There is no need to set anything
# past this point for scp and rcp, and it's important to refrain from
# outputting anything in those cases.

if [[ $- != *i* ]] ; then
	# Shell is non-interactive.  Be done now!
	return
fi

# Bash won't get SIGWINCH if another process is in the foreground.
# Enable checkwinsize so that bash will check the terminal size when
# it regains control.  #65623
# http://cnswww.cns.cwru.edu/~chet/bash/FAQ (E11)
shopt -s checkwinsize

# Enable history appending instead of overwriting.  #139609
shopt -s histappend

case ${TERM} in
  xterm*|rxvt*|Eterm|aterm|kterm|gnome*)
    PROMPT_COMMAND=${PROMPT_COMMAND:+$PROMPT_COMMAND; }'printf "\033]0;%s@%s:%s\007" "${USER}" "${HOSTNAME%%.*}" "${PWD/#$HOME/~}"'
    ;;
  screen)
    PROMPT_COMMAND=${PROMPT_COMMAND:+$PROMPT_COMMAND; }'printf "\033_%s@%s:%s\033\\" "${USER}" "${HOSTNAME%%.*}" "${PWD/#$HOME/~}"'
    ;;
esac

# Fortune is a simple program that displays a pseudorandom message
# from a database of quotations at logon and/or logout;
# type: "pacman -S fortune-mod" to install it, then uncomment the
# following lines:

# if [ "$PS1" ]; then
#	/usr/bin/fortune
# fi

# Set colorful PS1 only on colorful terminals.
# dircolors --print-database uses its own built-in database
# instead of using /etc/DIR_COLORS.  Try to use the external file
# first to take advantage of user additions.  Use internal bash
# globbing instead of external grep binary.

# Dynamically modified variables. Do not change them!
use_color=false
# sanitize TERM:
safe_term=${TERM//[^[:alnum:]]/?}
match_lhs=""

[[ -f ~/.dir_colors   ]] && match_lhs="${match_lhs}$(<~/.dir_colors)"
[[ -f /etc/DIR_COLORS ]] && match_lhs="${match_lhs}$(</etc/DIR_COLORS)"
[[ -z ${match_lhs}    ]] \
	&& type -P dircolors >/dev/null \
	&& match_lhs=$(dircolors --print-database)
[[ $'\n'${match_lhs} == *$'\n'"TERM "${safe_term}* ]] && use_color=true

if ${use_color} ; then
	# Enable colors for ls, etc.  Prefer ~/.dir_colors #64489
	if type -P dircolors >/dev/null ; then
		if [[ -f ~/.dir_colors ]] ; then
			eval $(dircolors -b ~/.dir_colors)
		elif [[ -f /etc/DIR_COLORS ]] ; then
			eval $(dircolors -b /etc/DIR_COLORS)
		fi
	fi

	if [[ ${EUID} == 0 ]] ; then
		PS1='\[\033[01;31m\]\h\[\033[01;34m\] \W \$\[\033[00m\] '
	else
		PS1='\[\033[01;32m\]\u@\h\[\033[01;34m\] \w \$\[\033[00m\] '
	fi

	alias ls='ls --color=auto'
	alias dir='dir --color=auto'
	alias grep='grep --colour=auto'
else
	if [[ ${EUID} == 0 ]] ; then
		# show root@ when we do not have colors
		PS1='\u@\h \W \$ '
	else
		PS1='\u@\h \w \$ '
	fi
fi

PS2='> '
PS3='> '
PS4='+ '

# Try to keep environment pollution down, EPA loves us.
unset use_color safe_term match_lhs

[ -r /etc/bash_completion ] && . /etc/bash_completion
```

/etc/DIR_COLORS:

```
# Configuration file for the color ls utility
# This file goes in the /etc directory, and must be world readable.
# You can copy this file to .dir_colors in your $HOME directory to override
# the system defaults.

# COLOR needs one of these arguments: 'tty' colorizes output to ttys, but not
# pipes. 'all' adds color characters to all output. 'none' shuts colorization
# off.
COLOR all

# Extra command line options for ls go here.
# Basically these ones are:
#  -F = show '/' for dirs, '*' for executables, etc.
#  -T 0 = don't trust tab spacing when formatting ls output.
OPTIONS -F -T 0

# Below, there should be one TERM entry for each termtype that is colorizable
TERM linux
TERM console
TERM con132x25
TERM con132x30
TERM con132x43
TERM con132x60
TERM con80x25
TERM con80x28
TERM con80x30
TERM con80x43
TERM con80x50
TERM con80x60
TERM xterm
TERM vt100

# EIGHTBIT, followed by '1' for on, '0' for off. (8-bit output)
EIGHTBIT 1

# Below are the color init strings for the basic file types. A color init
# string consists of one or more of the following numeric codes:
# Attribute codes: 
# 00=none 01=bold 04=underscore 05=blink 07=reverse 08=concealed
# Text color codes:
# 30=black 31=red 32=green 33=yellow 34=blue 35=magenta 36=cyan 37=white
# Background color codes:
# 40=black 41=red 42=green 43=yellow 44=blue 45=magenta 46=cyan 47=white
NORMAL 00	# global default, although everything should be something.
FILE 00 	# normal file
DIR 01;34 	# directory
LINK 01;36 	# symbolic link
FIFO 40;33	# pipe
SOCK 01;35	# socket
BLK 40;33;01	# block device driver
CHR 40;33;01 	# character device driver

# This is for files with execute permission:
EXEC 01;32 

# List any file extensions like '.gz' or '.tar' that you would like ls
# to colorize below. Put the extension, a space, and the color init string.
# (and any comments you want to add after a '#')
.cmd 01;32 # executables (bright green)
.exe 01;32
.com 01;32
.btm 01;32
.bat 01;32
.tar 01;31 # archives or compressed (bright red)
.tgz 01;31
.arj 01;31
.taz 01;31
.lzh 01;31
.zip 01;31
.z   01;31
.Z   01;31
.gz  01;31
.jpg 01;35 # image formats
.gif 01;35
.bmp 01;35
.xbm 01;35
.xpm 01;35
.tif 01;35
```

### Ripristino del file originale /etc/bash.bashrc file

Se vi pentite di aver modificato il file `/etc/bash.bashrc`, è sempre possibile ripristinare il file originale di Arch `/etc/bash.bashrc` e rimuovere il file `/etc/DIR_COLORS`. Si noti che non c'è un file "ufficiale" bash.bashrc: ogni distribuzione ha il suo. Ecco la copia esatta del file `/etc/bash.bashrc` originale di Arch.

/etc/bash.bashrc:

```
#
# /etc/bash.bashrc
#

# If not running interactively, don't do anything
[[ $- != *i* ]] && return

PS1='[\u@\h \W]\$ '
PS2='> '
PS3='> '
PS4='+ '

case ${TERM} in
  xterm*|rxvt*|Eterm|aterm|kterm|gnome*)
    PROMPT_COMMAND=${PROMPT_COMMAND:+$PROMPT_COMMAND; }'printf "\033]0;%s@%s:%s\007" "${USER}" "${HOSTNAME%%.*}" "${PWD/#$HOME/~}"'

    ;;
  screen)
    PROMPT_COMMAND=${PROMPT_COMMAND:+$PROMPT_COMMAND; }'printf "\033_%s@%s:%s\033\\" "${USER}" "${HOSTNAME%%.*}" "${PWD/#$HOME/~}"'
    ;;
esac

[ -r /etc/bash_completion   ] && . /etc/bash_completion
```

## Vedere anche

*   [gentoo-bashrc](https://aur.archlinux.org/packages/gentoo-bashrc/) da [AUR](/index.php/AUR "AUR")
*   tput(1)
*   [Colours and Cursor Movement With tput](http://tldp.org/HOWTO/Bash-Prompt-HOWTO/x405.html)

## Risorse esterne

*   Discussioni dei forum:
    *   [BASH prompt](https://bbs.archlinux.org/viewtopic.php?id=1817)
    *   [What's your PS1?](https://bbs.archlinux.org/viewtopic.php?id=50885)
*   [http://www.tldp.org/HOWTO/Bash-Prompt-HOWTO/x329.html](http://www.tldp.org/HOWTO/Bash-Prompt-HOWTO/x329.html)
*   [Giles Orr's collection of sample prompts](http://gilesorr.com/bashprompt/prompts/index.html)