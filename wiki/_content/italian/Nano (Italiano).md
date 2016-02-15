[GNU nano](http://www.nano-editor.org/) (o nano) è un editor di testo per console, che si propone di introdurre una semplice interfaccia ed opzioni di comando molto intuitivi per la modifica base di un testo. nano è l'editor predefinito per console in distribuzioni come Ubuntu e supporta svariate funzioni, tra cui l'evidenziazione colorata della sintassi, conversione dei file di tipo DOS/Mac, controllo ortografico e la codifica [UTF-8](http://it.wikipedia.org/wiki/UTF-8). L'avvio di nano con un buffer vuoto occupa in genere meno di 1,5 MB di memoria. [Una immagine di nano](http://i275.photobucket.com/albums/jj281/adamchrista/Arch%20Linux/Wiki%20Examples/nano-man.png).

## Contents

*   [1 Installazione](#Installazione)
*   [2 Configurazione](#Configurazione)
    *   [2.1 Creare il file ~/.nanorc](#Creare_il_file_.7E.2F.nanorc)
    *   [2.2 Evidenziazione della sintassi](#Evidenziazione_della_sintassi)
        *   [2.2.1 PKGBUILD](#PKGBUILD)
        *   [2.2.2 Altri file](#Altri_file)
    *   [2.3 Configurazione consigliata](#Configurazione_consigliata)
        *   [2.3.1 Sospensione](#Sospensione)
        *   [2.3.2 Non avvolgimento del testo](#Non_avvolgimento_del_testo)
*   [3 Utilizzo di nano](#Utilizzo_di_nano)
    *   [3.1 Funzioni Speciali](#Funzioni_Speciali)
        *   [3.1.1 Panoramica sui tasti di scelta rapida](#Panoramica_sui_tasti_di_scelta_rapida)
        *   [3.1.2 Abilitazione/Disabilitazione delle funzioni speciali](#Abilitazione.2FDisabilitazione_delle_funzioni_speciali)
*   [4 Suggerimenti](#Suggerimenti)
    *   [4.1 Sostituire vi con nano](#Sostituire_vi_con_nano)
        *   [4.1.1 Primo metodo](#Primo_metodo)
            *   [4.1.1.1 Esempio di utilizzo](#Esempio_di_utilizzo)
        *   [4.1.2 Secondo metodo](#Secondo_metodo)
            *   [4.1.2.1 Esempio di .bash_profile](#Esempio_di_.bash_profile)
        *   [4.1.3 Terzo Metodo](#Terzo_Metodo)
            *   [4.1.3.1 Link simbolici](#Link_simbolici)
            *   [4.1.3.2 Ripristino di vi](#Ripristino_di_vi)
        *   [4.1.4 Quarto metodo](#Quarto_metodo)
            *   [4.1.4.1 Rimozione e link simbolici](#Rimozione_e_link_simbolici)
            *   [4.1.4.2 Rispristino di vi](#Rispristino_di_vi)
*   [5 Fonti esterne](#Fonti_esterne)

## Installazione

[nano](https://www.archlinux.org/packages/?name=nano) è incluso nel [repository ufficiale di Arch Linux [core]](/index.php/Official_Repositories_(Italiano) "Official Repositories (Italiano)") e, generalmente, viene installato di default.

## Configurazione

### Creare il file `~/.nanorc`

L'aspetto e la funzione di nano è in genere controllata per mezzo sia di argomenti espressi da riga di comando, sia di comandi di configurazione presenti all'interno del file `~/.nanorc`. Un file di configurazione di esempio viene allocato con l'installazione del programma e lo potete trovare in `/etc/nanorc`. Il file `~/.nanorc` deve essere prima creato dall'utente:

```
$ cd ~
$ touch .nanorc

```

oppure copiare il file di default nella propria home

```
$ cp /etc/nanorc ~/.nanorc

```

Si può procedere a stabilire le varie variabili di configurazione semplicemente commentando/decommentando i vari comandi presenti in `.nanorc`.

**Tip:** Nella pagina [NANORC](http://www.nano-editor.org/dist/v2.2/nanorc.5.html) è elencata la lista completa dei vari comandi di configurazione avviabili in nano.

**Nota:** Gli argomenti a riga di comando sovrascrinono e prevalgono sui comandi di configurazione stabiliti in `.nanorc`.

### Evidenziazione della sintassi

#### PKGBUILD

Questa è nuova versione per Arch Linux ["svntogit-server"](https://projects.archlinux.org/svntogit/packages.git/tree).

```
# Arch PKGBUILD files
#
syntax "pkgbuild" "^.*PKGBUILD*"
# commands
color red "\<(cd|echo|enable|exec|export|kill|popd|pushd|read|source|touch|type)\>"
color brightblack "\<(case|cat|chmod|chown|cp|diff|do|done|elif|else|esac|exit|fi|find|for|ftp|function|grep|gzip|if|in)\>"
color brightblack "\<(install|ln|local|make|mv|patch|return|rm|sed|select|shift|sleep|tar|then|time|until|while|yes)\>"
# ${*}
icolor blue "\$\{?[0-9A-Z_!@#$*?-]+\}?"
# numerics
color blue "\ [0-9]*"
color blue "\.[0-9]*"
color blue "\-[0-9]*"
color blue "=[0-9]"
# spaces
color ,green "[[:space:]]+$"
# strings; multilines are not supported
color brightred ""(\\.|[^"])*"" "'(\\.|[^'])*'"
# comments
color brightblack "#.*$"

```

Questa è un'altra versione discussa [qui](https://bbs.archlinux.org/viewtopic.php?pid=565476).

 `/usr/share/nano/pkgbuild.nanorc` 

```
 ## Arch PKGBUILD files
 ##
 syntax "pkgbuild" "^.*PKGBUILD$"
 color green start="^." end="$"
 color cyan "^.*(pkgbase|pkgname|pkgver|pkgrel|pkgdesc|arch|url|license).*=.*$"
 color brightcyan "\<(pkgbase|pkgname|pkgver|pkgrel|pkgdesc|arch|url|license)\>"
 color brightcyan "(\$|\$\{|\$\()(pkgbase|pkgname|pkgver|pkgrel|pkgdesc|arch|url|license)(|\}|\))"
 color cyan "^.*(depends|makedepends|optdepends|conflicts|provides|replaces).*=.*$"
 color brightcyan "\<(depends|makedepends|optdepends|conflicts|provides|replaces)\>"
 color brightcyan "(\$|\$\{|\$\()(depends|makedepends|optdepends|conflicts|provides|replaces)(|\}|\))"
 color cyan "^.*(groups|backup|noextract|options).*=.*$"
 color brightcyan "\<(groups|backup|noextract|options)\>"
 color brightcyan "(\$|\$\{|\$\()(groups|backup|noextract|options)(|\}|\))"
 color cyan "^.*(install|source|md5sums|sha1sums|sha256sums|sha384sums|sha512sums).*=.*$"
 color brightcyan "\<(install|source|md5sums|sha1sums|sha256sums|sha384sums|sha512sums)\>"
 color brightcyan "(\$|\$\{|\$\()(install|source|md5sums|sha1sums|sha256sums|sha384sums|sha512sums)(|\}|\))"
 color brightcyan "\<(startdir|srcdir|pkgdir)\>"
 color cyan "\.install"
 color brightwhite "=" "'" "\(" "\)" "\"" "#.*$" "\," "\{" "\}"
 color brightred "build\(\)"
 color brightred "package_.*.*$"
 color brightred "\<(configure|make|cmake|scons)\>"
 color red "\<(DESTDIR|PREFIX|prefix|sysconfdir|datadir|libdir|includedir|mandir|infodir)\>"

```

Per poterla utilizzare salvatela come /usr/share/nano/pkgbuild.nanorc e aggiungete:

```
include "/usr/share/nano/pkgbuild.nanorc"

```

nel vostro file `~/.nanorc` oppure in `/etc/nanorc`.

#### Altri file

Installare il pacchetto [AUR](/index.php/AUR_(Italiano) "AUR (Italiano)"): [nano-syntax-highlighting-git](https://aur.archlinux.org/packages/nano-syntax-highlighting-git/).

### Configurazione consigliata

#### Sospensione

A differenza di molti programmi interattivi, la sospensione non è abilitata di default. Per modificare questo comportamento, decommentate la linea

```
set suspend

```

in `/etc/nanorc`. Questo vi permetterà di utilizzare i tasti `Ctrl + z` per inviare nano in background.

#### Non avvolgimento del testo

Provenendo da un'altra distro, il comportamento di nano potrebbe risultare anomalo; basterà modificare il file `/etc/nanorc` in questo modo:

```
## Don't wrap text at all.
set nowrap

```

## Utilizzo di nano

### Funzioni Speciali

La notazione per i tasti di scelta rapida è la seguente:

*   Le sequenze identificate con il simbolo `^` sono introdotte usando il tasto Control (`Ctrl`), oppure premendo il tasto `Esc` due volte.

*   Le sequenze identificate col simbolo Meta `M` possono essere inserite usato alternativamente il tasto `Esc`, `Alt` o `Meta`, a seconda della configurazione della tastiera. Inoltre, premendo `Esc` due volte e digitando i numeri da _000_ a _255_ si possono inserire i caratteri con il codice ASCII corrispondente.

#### Panoramica sui tasti di scelta rapida

*   `Ctrl`+`G` Aiuto (`F1`)

	Consente di visualizzare la Guida in linea all'interno della finestra di sessione. Se ne consiglia la lettura.

*   `Ctrl`+`O` Salva (`F3`)

	Salva il file corrente su disco

*   `Ctrl`+`R` Inserisci (`F5`)

	Inserisce un altro file nella posizione corrente del cursore

*   `Ctrl`+`Y` Pagina precedente (`F7`)

	Mostra la schermata precedente

*   `Ctrl`+`K` Taglia (`F9`)

	Taglia la riga corrente e la memorizza nel cutbuffer

*   `Ctrl`+`C` Posizione (`F11`)

	Mostra la posizione del cursore dando informazioni sulla linea, colonna e carattere

*   `Ctrl`+`X` Esci (`F2`)

	Chiude ed esce da nano, se il file è stato modificato ne chiede il salvataggio

*   `Ctrl`+`J` Giustifica (`F4`)

	Giustifica il paragrafo corrente in base alla geometria della finestra

*   `Ctrl`+`W` Cerca (`F6`)

	Cerca una stringa o un'espressione regolare

*   `Ctrl`+`V` Pagina successiva (`F8`)

	Mostra la schermata successiva

*   `Ctrl`+`U` Incolla (`F10`)

	Incolla dal cutbuffer nella riga corrente

*   `Ctrl`+`T` Ortografia (`F12`)

	Esegue il correttore ortografico, se disponibile, utilizza _spell_

**Tip:** Consultare l'aiuto in linea di nano tramite `Ctrl + g` all'interno dell'editor e il [manuale dei comandi di nano](http://www.nano-editor.org/dist/v2.1/nano.html) per una completa descrizione e supporto addizionale.

#### Abilitazione/Disabilitazione delle funzioni speciali

*   `Meta + c` (or `Esc + c`)

	Abilita/disabilita la visualizzazione della posizione del cursore.

*   `Meta + i` (or `Esc + i`)

	Abilita/disabilita l'indentazione automatica

*   `Meta + k` (or `Esc + k`)

	Abilita/disabilita la possibilità di tagliare la riga intera nella posizione del cursore

*   `Meta + m` (or `Esc + m`)

	Abilita/disabilita il supporto del mouse

*   `Meta + x` (or `Esc + x`)

	Abilita/disabilita la visualizzazione della barra inferiore dei comandi

**Tip:** La pagina sulle [caratteristiche aggiuntive](http://www.nano-editor.org/dist/v2.1/nano.html#Feature-Toggles) elenca tutte le alternative disponibili in nano.

## Suggerimenti

### Sostituire vi con nano

Molti utenti preferiscono utilizzare `nano` al posto di `vi` poiché risulta più semplice e facile da utilizzare, inoltre possono scegliere di sostituire `vi` con `nano` come editor predefinito per i comandi di testo come **visudo**.

#### Primo metodo

**Attenzione:** Dal `man 8 visudo`: _Si noti che questo metodo potrebbe compromettere la sicurezza in quanto permette all'utente di eseguire qualsiasi programma che desiderano semplicemente impostando le variabili VISUAL o EDITOR._

[sudo](/index.php/Sudo_(Italiano) "Sudo (Italiano)") reperibile nel repository _core_, è compilato in modo predefinito con l'opzione `--with-env-editor` e rispetta l'uso delle variabili `VISUAL` ed `EDITOR`. Per poter stabilire di utilizzare _nano_ come editor per il comando **visudo** per tutta la durata della sessione corrente della console, bisogna impostare ed esportare la variabile `EDITOR` prima di chiamare **visudo**.

```
export EDITOR=nano 

```

##### Esempio di utilizzo

```
 export EDITOR=nano && sudo visudo

```

#### Secondo metodo

**Attenzione:** Dal `man 8 visudo`: _Si noti che questo metodo potrebbe compromettere la sicurezza in quanto permette all'utente di eseguire qualsiasi programma che desiderano semplicemente impostando le variabili VISUAL o EDITOR._

La variabile **EDITOR** può anche essere impostata all'interno dei seguenti file per un uso persistente:

*   ~/[.bash_profile](http://www.gnu.org/software/bash/manual/bashref.html#Bash-Startup-Files) (shell di login)
*   ~/.bashrc (shell interattiva, non di login)
*   [`/etc/profile`](http://www.gnu.org/software/bash/manual/bashref.html#Bash-Startup-Files) (impostazioni globali per tutti gli utenti del sistema, tranne `root`)

##### Esempio di `.bash_profile`

```
. $HOME/.bashrc

export EDITOR=nano
export GREP_COLOR="1;33"

if [[ -z "$DISPLAY" ]] && [[ $(tty) = /dev/vc/1 ]]; then
  startx
  logout
fi
```

#### Terzo Metodo

**Nota:** Questo metodo può essere considerato draconiano e potrebbe non essere adatto a tutti gli utenti. Tuttavia, la seguente procedura esiste come esempio di una soluzione praticabile.

##### Link simbolici

come root, o tramite il comando `su -`

Rinominare l'eseguibile `vi` in `vi.old` per un semplice ripristino:

```
# mv /usr/bin/vi /usr/bin/vi.old

```

Creare un link simbolico da `/usr/bin/nano` a `/usr/bin/vi`:

```
# ln -s /usr/bin/nano /usr/bin/vi

```

**Nota:** Questo link simbolico andrà ricreato ad ogni aggiornamento di `Vi`.

##### Ripristino di `vi`

Rimuovere il link simbolico `/usr/bin/vi`:

```
# unlink /usr/bin/vi

```

Rinominare l'eseguibile `vi.old` a `vi`:

```
# mv /usr/bin/vi.old /usr/bin/vi

```

#### Quarto metodo

**Nota:** Questo metodo può essere considerato draconiano e potrebbe non essere adatto a tutti gli utenti. Tuttavia, la seguente procedura esiste come esempio di una soluzione praticabile.

##### Rimozione e link simbolici

Usare [pacman](/index.php/Pacman_(Italiano) "Pacman (Italiano)") per rimuovere `vi`, le sue configuazioni e le dipendenze:

```
# pacman -Rns vi

```

Creare il link simbolico da `/usr/bin/nano` a `/usr/bin/vi`:

```
# ln -s /usr/bin/nano /usr/bin/vi

```

##### Rispristino di `vi`

Rimuovere il link simbolico `/usr/bin/vi`

```
# unlink /usr/bin/vi

```

Utilizzare pacman per installare il pacchetto `vi` precedentemente disinstallato.

```
# pacman -S vi 

```

**Nota:** Non pulire `-c` o aggiornare `-y` il database dei pacchetti, se volete mantenere la versione precedentemente installata del pacchetto `vi`. In questo caso, gli aggiornamenti successivi richiederanno anche l'uso giudizioso dell'opzione `--ignore vi` (ed in modo facoltativo di `--ignore glibc ncurses coreutils`.

## Fonti esterne

*   [nano (text editor)](https://en.wikipedia.org/wiki/Nano_(text_editor) "wikipedia:Nano (text editor)") - Articolo Wikipedia inglese
*   [GNU nano Homepage](http://www.nano-editor.org/) - Sito Ufficiale
*   [GNU nano Bugs](https://savannah.gnu.org/bugs/?group=nano) - Segnalazione Bug
*   [Better syntax highlighting definitions](https://github.com/craigbarnes/nanorc)