*"[Vim](http://www.vim.org/about.php) è un editor di testi avanzato che mira a fornire la potenza del de-facto editor UNIX ‘vi’, con maggiori caratteristiche e funzionalità."* Vim non è un semplice editor di testo come nano o pico. Esso richiede un po' di pratica per imparare, e molto tempo per padroneggiarlo.

Vim è ideato per ridurre al minimo il lavoro delle dita, e non ci sarà mai bisogno di usare il mouse. Questo può sembrare sciocco, ma una volta padroneggiato vim, se ne comprenderà il motivo.

## Contents

*   [1 Caratteristiche](#Caratteristiche)
*   [2 Installazione](#Installazione)
*   [3 Uso](#Uso)
    *   [3.1 Editing di base](#Editing_di_base)
    *   [3.2 Spostamento](#Spostamento)
    *   [3.3 Ripetere i comandi](#Ripetere_i_comandi)
    *   [3.4 Cancellare](#Cancellare)
    *   [3.5 Annulla e ripeti](#Annulla_e_ripeti)
    *   [3.6 Modalità visuale](#Modalit.C3.A0_visuale)
    *   [3.7 Trova e sostituisci](#Trova_e_sostituisci)
    *   [3.8 Salvare ed uscire](#Salvare_ed_uscire)
    *   [3.9 Altri comandi](#Altri_comandi)
*   [4 Configurazione](#Configurazione)
    *   [4.1 File di backup](#File_di_backup)
    *   [4.2 Ripetizione della ricerca](#Ripetizione_della_ricerca)
    *   [4.3 Controllo ortografico](#Controllo_ortografico)
    *   [4.4 Evidenziare la sintassi](#Evidenziare_la_sintassi)
    *   [4.5 Esempio di ~/.vimrc](#Esempio_di_.7E.2F.vimrc)
*   [5 Unire file (Vimdiff)](#Unire_file_.28Vimdiff.29)
*   [6 Vim Tips](#Vim_Tips)
    *   [6.1 Numeri linea](#Numeri_linea)
    *   [6.2 Sostituzioni tra linee](#Sostituzioni_tra_linee)
    *   [6.3 Ripristinare la posizione del cursore nei file](#Ripristinare_la_posizione_del_cursore_nei_file)
    *   [6.4 Spazio vuoto all'inizio della finestra di gvim](#Spazio_vuoto_all.27inizio_della_finestra_di_gvim)
    *   [6.5 Sostituire il comando vi con vim](#Sostituire_il_comando_vi_con_vim)
*   [7 Altre risorse](#Altre_risorse)
    *   [7.1 Ufficiali](#Ufficiali)
    *   [7.2 Tutorial](#Tutorial)
    *   [7.3 Video](#Video)
    *   [7.4 Esempi di configurazione](#Esempi_di_configurazione)
    *   [7.5 Altro](#Altro)

## Caratteristiche

*   Vim è molto potente per effettuare editing avanzati
*   Espandibile, grazie alle opzioni di configurazione
*   Semplici e robuste scorciatoie da tastiera
*   Evidenziazione della sintassi

## Installazione

Si può [installare](/index.php/Pacman_(Italiano) "Pacman (Italiano)") la versione da linea di comando con il pacchetto [vim](https://www.archlinux.org/packages/?name=vim), oppure si può installare la versione con interfaccia grafica (che fornisce anche `vim`) installando il pacchetto [gvim](https://www.archlinux.org/packages/?name=gvim).

**Nota:** [vim](https://www.archlinux.org/packages/?name=vim) non è più compilato con l'opzione X server. Per molti utenti, significa che la normale funzione di copia e incolla dagli appunti di un ambiente grafico non funzionerà. Se non si vuole rinunciare a questa funzionalità, considerare l'installazione di [gvim](https://www.archlinux.org/packages/?name=gvim) che include una versione di Vim con questo supporto. Vedere [FS#14609](https://bugs.archlinux.org/task/14609) per maggiori informazioni.

**Nota:** Il pacchetto vim è concepito per essere il più leggero possibile, per cui non supporta gli interpreti di Python, Lua, e Ruby. Se si richiede tale supporto, scegliere il pacchetto gvim, il quale include il binario vim. Il repository non ufficiale `herecura-stable` fornisce qualche variante di vim / gvim: `$ pacman -Slq herecura-stable | grep vim` 
```
vim-cli
vim-gvim-gtk
vim-gvim-motif
vim-gvim-qt
vim-gvim-x11
vim-rt
vim-tiny

```

## Uso

Questa è una panoramica base su come utilizzare vim. Alternativamente, è possibile utilizzare `vimtutor` per familiarizzare con l'editor. Vim ha quattro differenti modalità:

*   *Command mode* (modalità comando): i tasti premuti vengono interpretati come comandi.
*   *Insert mode* (modalità inserimento): i tasti premuti vengono inseriti nel file.
*   *Visual mode* (modalità visuale): i tasti premuti selezionano, tagliano o copiano il testo.
*   *Ex mode* (modalità ex): una modalità di input per comandi addizionali (esempio salvare un file, sostituire parti di testo, ecc.).

### Editing di base

Se si avvia vim con:

```
$ vim somefile.txt

```

si vedrà un documento vuoto (presumendo che somefile.txt non esista. Se esiste, si vedrà il suo contenuto). Non sarà possibile modificarlo immediatamente - la modalità in cui si avvia vim è la modalità comando(*Command Mode*). In questa modalità sarà possibile utilizzare i comandi vim dalla tastiera.

**Nota:** Vim è un esempio dello stile Unix. Questo significa che non è vistoso, e non lascerà ferme le nostre mani. Non ha assistenti o giochi integrati. Esso però ci permetterà comunque di portare a termine il lavoro, ed anche velocemente. Anche tutti i suoi comandi sono case sensitive. A volte i comandi maiuscoli sono una versione con effetto più ampio (`s` sostituisce un carattere, `S` sostituisce una linea), altre volte sono comandi completamente diversi (`j` sposta il cursore in basso, `J` unisce due linee).

Per inserire il testo (prima del cursore) usare il comando `i`. `I` (**i** maiuscola) entra in inserimento all'inizio della linea. Per aggiungere del testo dopo il cursore (quello che la maggior parte degli utenti si aspetta) premere `a`. Premendo `A` posizionerà il cursore per l'inserimento alla fine della linea.

Si può tornare in modalità comando, in qualsiasi momento premendo `Esc`.

### Spostamento

In vim, è possibile spostare il cursore usando le frecce della tastiera, ma questa non è considerata la **vim way**. Si dovrebbe spostare la mano tropo a destra dalla normale posizione di battitura per raggiungere le frecce, e poi ritornare in posizione. Non è divertente.

In vim ci si può spostare in basso premendo `j`. Si può ricordare perché la lettera "j" punta verso il basso. Per spostare il cursore in alto premendo `k`. A sinistra con `h` (si trova a sinistra di "j"), ed a destra con `l` (**L** minuscolo).

`^` posizionerà il cursore all'inizio della linea, e `$` alla fine di essa.

**Nota:** `^` e `$` sono comunemente utilizzati nelle espressioni regolari per rappresentare l'inizio e la fine della linea. Le espressioni regolari sono molto potenti e comunemente usate negli ambienti *nix, quindi per ora sarà ingannevole, ma più avanti si capirà "l'idea" dietro a molti di queste combinazioni da tastiera.

Per spostarsi di una parola premere `w`. `W` considera come appartenenti alla parola più caratteri (ad esempio gli underscore, i trattini come parte della parola). Per tornare indietro di una parola si usa `b`. Anche in questo caso `B` considera come appartenenti alla parola più caratteri. Per avanzare fino alla fine di una parola `e`, `E` per comprendere altri caratteri.

Per spostarsi all'inizio di una frase `(` effettuerà lo spostamento. `)` farà invece l'opposto, spostandosi alla fine della frase. Per uno spostamento maggiore `{` posizionerà il cursore all'inizio del paragrafo. `}` sposterà il cursore alla fine dell'intero paragrafo.

Per spostarsi all'inizio dello schermo, `H` effettuerà lo spostamento. `M` sposterà il cursore al centro dello schermo, ed `L` alla fine della schermata. `gg` posizionerà il cursore all'inizio del file, `G` invece alla sua fine. `Ctrl+D` permetterà di scorrere pagina per pagina.

### Ripetere i comandi

Se un comando è preceduto da un numero, allora questo comando verrà eseguito un numero di volte uguale al numero premuto (ci sono delle eccezioni, ma possono avere senso, come il comando `s`). Ad esempio premendo `3i` ed inserendo il testo "Help! " e successivamente `Esc` verrà inserito il testo "Help! Help! Help! “. Premendo `2}` il cursore si sposterà in avanti di due paragrafi. Questo è utile con alcuni dei comandi di seguito.

### Cancellare

Il comando `x` cancellerà il carattere sotto al cursore. `X` cancellerà il carattere prima del cursore. Qui è dove la funzione dei numeri diventa interessante. `6x` cancellerà 6 caratteri. Premere `.` (punto) ripeterà il comando precedente. Quindi, ipotizzando di avere la parola "foobar" in diversi punti, ma dopo averci pensato, si preferisce usare la parola "foo". Spostare il cursore sopra la lettera "b", premere `3x`, spostare il cursore sulla successiva parola "foobar" e premere `.` (punto).

Il comando `d` comunicherà a vim che si intende cancellare qualcosa. Dopo aver premuto `d`, sarà necessario indicare cosa cancellare. Si possono utilizzare anche i comandi di movimento. `dW` cancellerà finito alla prossima parola. `d^` cancellerà fino all'inizio della linea. Anteporre un numero al comando di eliminazione funzionerà altrettanto: `3dW` cancellerà fino alle tre parole successive. `D` (maiuscolo) è una scorciatoia per cancellare fino alla fine della linea (come `d$`). Premere `dd` cancellerà tutta la linea.

Per cancellare e sostituire la parola corrente, posizionare il cursore sulla parola ed eseguire il comando `cw`. Questo comando cancellerà la parola e cambierà la modalità in inserimento. Per sostituire una singola lettera usare `r`.

### Annulla e ripeti

Vim ha una funzione appunti integrata (anche nota come buffer). Le azioni possono essere annullate con il tasto `u` e ripetute con la combinazione `Ctrl+r`.

### Modalità visuale

Premendo `v` si entrerà in *visual mode*. In questa modalità è possibile selezionare parti di testo, una volta selezionato premendo `y` verrà memorizzato nel buffer, è possibile tagliare il testo premendo `c`. `p` incollerà il testo memorizzato nel buffer dopo il cursore, `P` prima. Il tasto `V` attiverà la *visual line mode*, analoga alla modalità precedente ma con effetto su intere linee. `Ctrl+v` invece per i blocchi di testo.

**Nota:** In qualsiasi momento si cancelli del testo, questo vine inserito nel buffer e sarà disponibile per essere incollato.

### Trova e sostituisci

Per cercare una parola o un carattere nel file, basterà semplicemente premere `/` e successivamente il/i carattere/i da cercare ed infine premere `ENTER`. Per visualizzare l'occorrenza successiva della ricerca usare `n`, mentre per la precedente usare `N`.

Per cercare e sostituire usare il comando *substitute* `:s/`. La sua sintassi è `[range]s///[arguments]`. Ad esempio:

```
Comando        Risultato
:s/xxx/yyy/    Sostituisce xxx con yyy alla prima occorrenza
:s/xxx/yyy/g   Sostituisce xxx con yyy alla prima occorrenza, globalmente, (in una intera frase)
:s/xxx/yyy/gc  Sostituisce xxx con yyy globalmente con conferma
:%s/xxx/yyy/g  Sostituisce xxx con yyy globalmente in tutto il file

```

Si può usare il comando *global* `:g/` per ricercare un pattern ed eseguire un comando per ogni corrispondenza. La sintassi è: `[range]:g//[cmd]`.

```
Comando  Risultato
:g/^#/d  Cancella tutte le linee che iniziano per #
:g/^$/d  Cancella tutte le linee che sono vuote

```

### Salvare ed uscire

Per salvare e/o uscire, sarà necessario usare la modalità *Ex*. I comandi della modalità *Ex* sono preceduti da `:`. Per salvare un file usare `**:w** nomefile`. Per uscire `:q`. Se invece si desidera uscire senza salvare le modifiche effettuate, usare `:q!`. Per salvare ed uscire `:x`. Esiste anche un'altra scorciatoia per salvare ed uscire cioè la combinazione `ZZ` (maiuscole).

### Altri comandi

1.  Premendo `s` verrà cancellato il carattere sotto al cursore, e verrà attivata la modalità inserimento. `S` cancellerà l'intera linea ed attiverà la modalità inserimento.
2.  `o` creerà una nuova linea sotto alla linea corrente ed attiverà la modalità inserimento. `O` invece creerà una nuova linea sopra a quella corrente ed avvierà la modalità inserimento.
3.  `yy` memorizzerà una linea nel buffer.
4.  `cc` cancellerà la linea corrente ed attiverà la modalità inserimento.
5.  `*` evidenzierà la parola corrente e `n` la cercherà.

## Configurazione

Il file di configurazione personale di vim si trova nella cartella home dell'utente `~/.vimrc`. Gli utenti esperti di vim tendono a tenere un `~/.vimrc` molto ben strutturato. La configurazione globale di vim è situata in `/etc/vimrc`. La variabile di ripiego `$VIM` è definita come `/usr/share/vim/`. Ad esempio per creare uno schema di colori globale il file `*.vim` dello shema di colori dovrebbe essere salvato in `/usr/share/vim/vimfiles/`.

Correntemente, la configurazione globale di vim in Arch Linux è molto basilare a differenza delle configurazioni di default di vim nelle altre distribuzioni. Per ottenere i comportamenti comunemente utilizzati (come evidenziare la sintassi, il ritorno alla linea dell'ultima modifica...), utilizzare il file di configurazione d'esempio:

```
cp /etc/vimrc /etc/vimrc.bak
cp /usr/share/vim/vim73/vimrc_example.vim /etc/vimrc

```

### File di backup

Vim per default crea un backup di un file modificato nella stesa cartella del file chiamandolo `nomefile~`. Per evitare di ingombrare, alcuni utenti impostano vim per utilizzare una apposita cartella per i backup:

```
set backupdir=~/.vim/backup,/tmp

```

Oppure è possibile disabilitare questa funzione:

```
set nobackup
set nowritebackup
set noswapfile    ! (disabilita i file swap)

```

### Ripetizione della ricerca

Con quest'opzione, *trova successivo* torna all'inizio del file quando ne raggiunge la fine. Similarmente, *trova precedente* va alla fine del file quando ne raggiunge l'inizio.

```
set wrapscan

```

### Controllo ortografico

```
set spell

```

Con questa opzione Vim evidenzierà le parole non scritte correttamente. Muovere il cursore su una parola errata e usare `z=` per vedere le correzioni proposte.

Solo il dizionario inglese sarà installato di default, altri possono essere trovati nei [repository ufficiali](/index.php/Official_Repositories_(Italiano) "Official Repositories (Italiano)"). Per ottenere una lista dei linguaggi disponibili, eseguire:

```
# pacman -Ss vim-spell

```

I file dei dizionari possono essere trovati anche nell'[archivio FTP di Vim](http://ftp.vim.org/vim/runtime/spell/). Mettere i dizionari scaricati nella cartella `~/.vim/spell` e configurare il dizionario eseguendo: `:setlocal spell spelllang=LL`.

**Tip:**

*   Per abilitare il controllo ortografico soltanto per i documenti LaTeX (o TeX), aggiungere `autocmd FileType tex setlocal spell spelllang=en_us` al file `~/.vimrc` oppure in `/etc/vimrc`, e riavviare vim. Per il controllo ortografico di linguaggi diversi dall'inglese, semplicemente sostituire `en_us` con il valore appropriato al proprio linguaggio.
*   Sarà possibile abilitare il controllo ortografico per alcuni tipi di file (ad esempio *.txt) usando il plugin FileType ed una regola personalizzata per dichiarare il tipo di file. Per abilitare il controllo ortografico per ogni file di tipo `*.txt`, creare il file `/usr/share/vim/vimfiles/ftdetect/plaintext.vim`, ed inserire la linea `autocmd BufRead,BufNewFile *.txt setfiletype plaintext` nel file. Successivamente, inserire la linea `autocmd FileType plaintext setlocal spell spelllang=en_us` nel proprio file `~/.vimrc` oppure in `/etc/vimrc`, e riavviare vim.

### Evidenziare la sintassi

Per abilitare l'opzione ed evidenziare la sintassi (*syntax highlighting*) (vim supporta una vasta lista di linguaggi di programmazione):

```
filetype plugin on
syntax on

```

### Esempio di ~/.vimrc

Un esempio della [configurazione di Vim](/index.php/Vim/.vimrc_(Italiano) "Vim/.vimrc (Italiano)").

## Unire file (Vimdiff)

Vim include un editor di comparazione (un programma che può mostrare le differenze tra due file). Può essere avviato con `vimdiff file1 file2`; successivamente usare:

```
]c :        - differenza successiva
[c :        - differenza precedente
Ctrl+w +w   - cambio finestra
do          - invia modifica
dp          - ottieni modifica
zo          - mostra il testo nascosto
zc          - nasconde il testo
:diffupdate - ricontrolla i file in cerca di differenze

```

## Vim Tips

Trucchi per portare a termine alcuni compiti.

### Numeri linea

1.  Per mostrare i numeri linea `:set number`.
2.  Per andare ad una linea specifica `:<numero linea>`.

### Sostituzioni tra linee

Per sostituire solo tra un intervallo di certe linee:

```
:*n*,*n*s/one/two/g

```

Ad esempio, per sostituire il pattern 'one' con 'two' tra le linee 3 e 4, è possibile eseguire:

```
:3,4s/one/two/g

```

### Ripristinare la posizione del cursore nei file

Se si desidera che all'apertura di un file vim posizioni il cursore dove era situato durante l'ultima modifica del file, aggiungere la seguente linea al file `~/.vimrc`:

```
if has("autocmd")
au BufReadPost * if line("'\"") > 1 && line("'\"") <= line("$") | exe "normal! g`\"" | endif
endif

```

Consultare anche [questo articolo](http://vim.wikia.com/wiki/Restore_cursor_to_file_position_in_previous_editing_session) del wiki di Vim.

### Spazio vuoto all'inizio della finestra di gvim

Quando si usa un [window manager](/index.php/Window_Manager_(Italiano) "Window Manager (Italiano)") configurato per ignorare le dimensioni delle finestre, gvim riempirà l'area non funzionale con il colore dell sfondo del tema GTK.

Una soluzione è disabilitare la barra dei menu in `.vimrc`, questo farà apparire la finestra di gvim come dovrebbe, occupando l'intera area:

```
set go-=m "remove menubar

```

Un'altra soluzione consiste nel rendere più omogeneo il colore dello sfondo: semplicemente inserendo questa linea nel file `~/.gtkrc-2.0`:

```
style "vimfix" {
  bg[NORMAL] = "#242424" # this matches my gvim theme 'Normal' bg color.
}
widget "vim-main-window.*GtkForm" style "vimfix"

```

### Sostituire il comando vi con vim

Eseguire questi comandi:

```
# ln -s $(which vim) /usr/local/bin/vi
# ln -s $(which vim) /usr/local/bin/view

```

Leggere anche [http://superuser.com/questions/27091/vim-to-replace-vi](http://superuser.com/questions/27091/vim-to-replace-vi)

## Altre risorse

### Ufficiali

*   [Homepage](http://www.vim.org/)
*   [Documentazione](http://vimdoc.sourceforge.net/)
*   [Tips Wiki](http://vim.wikia.com)

### Tutorial

*   [vi Tutorial e Reference Guide](http://usalug.org/vi.html)
*   [vi-vim trucchi consigli e Tutorial grafici](http://www.viemu.com/a_vi_vim_graphical_cheat_sheet_tutorial.html)
*   [Vim introduzione e tutorial](http://blog.interlinked.org/tutorials/vim_tutorial.html)
*   [Vim Recipes](http://vim.runpaint.org/) - Un manuale liberamente consultabile.

### Video

*   [Vimcasts](http://vimcasts.org/) - Screencasts in formato .ogg.
*   [Video tutorial](http://www.derekwyatt.org/vim/vim-tutorial-videos/vim-novice-tutorial-videos/) - Tratta dagli argomenti base a quelli avanzati.

### Esempi di configurazione

*   [Setup di nion](http://nion.modprobe.de/setup/vimrc)
*   [Una configurazione dettagliata da Amir Salihefendic](http://amix.dk/vim/vimrc.html)
*   [Bart Trojanowski](http://www.jukie.net/~bart/conf/vimrc)
*   [Basic .vimrc](https://gist.github.com/anonymous/c966c0757f62b451bffa)

### Altro

*   [HOWTO Vim](http://www.gentoo-wiki.info/HOWTO_VIM) - Articolo del wiki di Gentoo su cui è basato questo articolo (autore sconosciuto).
*   [Vivify](http://bytefluent.com/vivify/) - Un editor dello schema di colori per Vim