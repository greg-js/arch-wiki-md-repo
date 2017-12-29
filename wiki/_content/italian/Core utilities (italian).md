Articoli correlati

*   [Bash (Italiano)](/index.php/Bash_(Italiano) "Bash (Italiano)")
*   [Zsh](/index.php/Zsh "Zsh")
*   [General Recommendations (Italiano)](/index.php/General_Recommendations_(Italiano) "General Recommendations (Italiano)")
*   [GNU Project](/index.php/GNU_Project "GNU Project")

In questo articolo si trovano trucchi e consigli a proposito degli strumenti di base dei sistemi GNU/Linux, come **less**, **ls**, and **grep**. L'ambito di questa pagine include le utility contenute nel pacchetto [coreutils](https://www.archlinux.org/packages/?name=coreutils), ma non solo.

## Contents

*   [1 grep](#grep)
*   [2 less](#less)
    *   [2.1 Output colorato tramite variabili di ambiente](#Output_colorato_tramite_variabili_di_ambiente)
    *   [2.2 Output colorato tramite wrappers](#Output_colorato_tramite_wrappers)
    *   [2.3 Vim come pager alternativo](#Vim_come_pager_alternativo)
*   [3 ls](#ls)
*   [4 rm](#rm)
*   [5 Altre risorse](#Altre_risorse)

## grep

[grep](https://en.wikipedia.org/wiki/grep "wikipedia:grep") è uno strumento a linea di comando già presente in Unix. **grep** permette la ricerca globale di corrispondenze nelle linee dei file e del testo tramite le espressioni regolari e le resttuisce in output.

Si può impostare un output colorato per migliorare la comprensione del funzionamento delle espressioni regolari. È necessario impostare un alias in `~/.bashrc`:

```
alias grep='grep --color=auto' 

```

In alternativa, si può impostare [la variabile d'ambiente](/index.php/Environment_variables "Environment variables") **GREP_OPTIONS** [[1]](http://www.gnu.org/software/grep/manual/html_node/Environment-Variables.html), ma questo può rendere inutilizzabile alcuni scipt che usano **grep** [[2]](http://brainstorm.ubuntu.com/idea/24141/):

```
export GREP_OPTIONS='--color=auto'

```

Per includere il conteggio delle linee del file nell'output si usa l'opzione "*-n*":

```
alias grep='grep -n --color=auto'

```

Si può usare la variabile **GREP_COLORS** per specificare colori diversi dai predefiniti.

## less

[less](https://en.wikipedia.org/wiki/less_(Unix) permette di visualizzare il contenuto di un file diviso una schermata alla volta. Anche se è simile a **more** e **pg**, **less** offre un'interfaccia più avanzata e un insieme di caratteristiche più completo.[[3]](http://www.greenwoodsoftware.com/less/faq.html)

Si può abilitare la colorazione sintattica per **less**.

### Output colorato tramite variabili di ambiente

Aggiungete le seguenti righe a un file di configurazione della shell usata, per esempio `~/.bashrc` nel caso usiate [Bash](/index.php/Bash_(Italiano) "Bash (Italiano)"):

```
export LESS=-R
export LESS_TERMCAP_me=$(printf '\e[0m')
export LESS_TERMCAP_se=$(printf '\e[0m')
export LESS_TERMCAP_ue=$(printf '\e[0m')
export LESS_TERMCAP_mb=$(printf '\e[1;32m')
export LESS_TERMCAP_md=$(printf '\e[1;34m')
export LESS_TERMCAP_us=$(printf '\e[1;32m')
export LESS_TERMCAP_so=$(printf '\e[1;44;1m')

```

I valori possono essere cambiati a piacimento. Per maggiori informazioni [Wikipedia:ANSI_escape_code#Colors](https://en.wikipedia.org/wiki/ANSI_escape_code#Colors "wikipedia:ANSI escape code").

### Output colorato tramite wrappers

Installate [source-highlight](https://www.archlinux.org/packages/?name=source-highlight) e aggiungete le seguenti linee a un file di configurazione della propria shell, es. `~/.bashrc` nel caso di Bash:

```
export LESSOPEN="| /usr/bin/source-highlight-esc.sh %s"
export LESS='-R '

```

Se si usa di frequente la linea di comando, può essere utile installare [lesspipe](https://www.archlinux.org/packages/?name=lesspipe), che permette anche di esplorare archivi.

**lesspipe** garantisce inoltre la possibilità di trattare anche altri tipi di files, perciò costituisce una alternativa a strumenti dedicati, come [python-html2text](https://www.archlinux.org/packages/?name=python-html2text) nel caso dei files HTML.

Rieffettuate il login o scrivete `source /etc/profile.d/lesspipe.sh` per cominciare a usare **lesspipe**.

### Vim come pager alternativo

Vim dispone di uno script che permette di visualizzare il contenuto di file di testo, binari, archivi, directories. Aggiungete la seguente linea a un file di configurazione della propria shell, es. `~/.bashrc` nel caso di Bash:

```
alias less='/usr/share/vim/vim73/macros/less.sh'

```

## ls

[ls](https://en.wikipedia.org/wiki/ls "wikipedia:ls") è un comando per elencare files in un sistema operativo Unix o Unix-like.

Per colorare l'output si usa un alias nel file di configurazione della propria shell `~/.bashrc`:

```
alias ls='ls --color=auto'

```

Si può ulteriormente miglorare il risultato: per esempio per mostrare i collegamenti simbolici non funzionanti si aggiunge al consueto file:

```
eval $(dircolors -b)

```

## rm

[rm](https://en.wikipedia.org/wiki/rm_(Unix) è il comando per eliminare file e directory. Può essere molto pericoloso, quindi è prudente usare un alias depotenziato:

```
alias rm=' timeout 3 rm -Iv'

```

Questo alias sospende il comando dopo tre secondi, chede conferma per tre o più files da eliminare, manda in output la lista dei files cancellati e non viene memorizzato nella cronologia della shell se la shell ignora i comandi che cominciano con uno spazio.

## Altre risorse

*   [Una panoramica sulle coreutils](http://www.reddit.com/r/commandline/comments/19garq/a_sampling_of_coreutils_120/) [, parte 2](http://www.reddit.com/r/commandline/comments/19ge6v/a_sampling_of_coreutils_2040/) [, parte 3](http://www.reddit.com/r/commandline/comments/19j1w3/a_sampling_of_coreutils_4060/).