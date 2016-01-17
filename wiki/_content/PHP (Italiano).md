# PHP (Italiano)

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

[PHP](http://www.php.net/) è un linguaggio di scripting general-purpose ampiamente utilizzato. È specialmente indicato per lo sviluppo Web e può essere integrato nell'HTML.

## Contents

*   [1 Installazione](#Installazione)
*   [2 Setup](#Setup)
*   [3 Configurazione](#Configurazione)
*   [4 Estensioni](#Estensioni)
    *   [4.1 gd](#gd)
    *   [4.2 imagemagick](#imagemagick)
    *   [4.3 pthreads](#pthreads)
    *   [4.4 mcrypt](#mcrypt)
    *   [4.5 PCNTL](#PCNTL)
*   [5 Zend Core + Apache](#Zend_Core_.2B_Apache)
*   [6 Strumenti per lo sviluppo](#Strumenti_per_lo_sviluppo)
    *   [6.1 Komodo](#Komodo)
    *   [6.2 Netbeans](#Netbeans)
    *   [6.3 Eclipse PDT](#Eclipse_PDT)
    *   [6.4 Zend Studio](#Zend_Studio)
    *   [6.5 Aptana Studio](#Aptana_Studio)
    *   [6.6 Zend Code Analyzer](#Zend_Code_Analyzer)
        *   [6.6.1 Installazione](#Installazione_2)
        *   [6.6.2 Vim Integration](#Vim_Integration)
        *   [6.6.3 Eclipse Integration](#Eclipse_Integration)
        *   [6.6.4 Komodo Integration](#Komodo_Integration)
*   [7 Risoluzione problemi](#Risoluzione_problemi)
    *   [7.1 PHP Fatal error: Class 'ZipArchive' not found](#PHP_Fatal_error:_Class_.27ZipArchive.27_not_found)
    *   [7.2 /etc/php/php.ini not parsed](#.2Fetc.2Fphp.2Fphp.ini_not_parsed)
*   [8 Altre risorse](#Altre_risorse)

## Installazione

[Installare](/index.php/Pacman "Pacman") il pacchetto [php](https://www.archlinux.org/packages/?name=php) dagli [official repositories](/index.php/Official_repositories "Official repositories").

Si noti che per eseguire script PHP come CGI, è necessario il pacchetto [php-cgi](https://www.archlinux.org/packages/?name=php-cgi).

## Setup

PHP può essere eseguito in modalità standalone, tuttavia in genere viene utilizzato con server HTTP come Apache, nginx e lighttpd.

*   **standalone**: `php -S localhost:8000 -t public_html/`. Leggi la [documentazione](http://docs.php.net/manual/en/features.commandline.webserver.php)
*   **Apache**: vedi [Apache HTTP Server](/index.php/Apache_HTTP_Server "Apache HTTP Server")
*   **lighttpd**: vedi [lighttpd](/index.php/Lighttpd "Lighttpd")
*   **nginx**: vedi [nginx](/index.php/Nginx "Nginx")

## Configurazione

Il file di configurazione principale di PHP è ben documentato e si trova a `/etc/php/php.ini`.

*   Si consiglia di impostare la propria timezone ([lista delle timezones](http://www.php.net/manual/en/timezones.php)) in `/etc/php/php.ini` per esempio:

```
date.timezone = Europe/Rome

```

*   Se si desidera visualizzare gli errori per il debug del priorio codice PHP, impostare `display_errors` su `On` in `/etc/php/php.ini`:

```
display_errors=On

```

*   Ricordarsi di aggiungere un gestore di file per `.phtml`, nel caso se ne abbia bisogno, in `/etc/httpd/conf/extra/php5_module.conf`:

```
DirectoryIndex index.php index.phtml index.html

```

## Estensioni

Nei repository ufficiali si possono trovare anche diverse estensioni per PHP comunemente usate:

```
# pacman -Ss php-

```

### gd

Per [php-gd](https://www.archlinux.org/packages/?name=php-gd) decommentare questa riga in `/etc/php/php.ini`:

```
extension=gd.so

```

### imagemagick

Per [imagemagick](https://www.archlinux.org/packages/?name=imagemagick) eseguire `# pecl install imagick`. I file binari di pecl sono inclusi nel pacchetto [php-pear](https://aur.archlinux.org/packages/php-pear/)<sup><small>AUR</small></sup>. Quindi aggiungere

```
extension=imagick.so

```

a `/etc/php/php.ini`.

### pthreads

Se si desidera avere POSIX multi-threading è necessaria l'estensione pthreads. Per installare l'estensione pthreads ([http://pecl.php.net/package/pthreads](http://pecl.php.net/package/pthreads)) tramite `pecl` si deve usare una versione compilata di PHP con il thread safety support flag `--enable-maintainer-zts`. Attualmente il modo più semplice per farlo sarebbe di fare il rebuild del pacchetto originale con la flag.

Si possono trovare altre istruzioni alla pagina [PHP pthreads extension](/index.php/PHP_pthreads_extension "PHP pthreads extension").

### mcrypt

*   Per il modulo `mcrypt`, installate [php-mcrypt](https://www.archlinux.org/packages/?name=php-mcrypt) e decommentate `extension=mcrypt.so` in `/etc/php/php.ini`:

```
extension=mcrypt.so

```

### PCNTL

PCNTL consente di creare processi direttamente nella macchina lato server. Tuttavia dà anche il potere a PHP di complicare le cose. Si tratta di un'estensione di PHP che non deve essere caricata con leggerezza, a causa del grande potere che dà a PHP. Per attivare (di default non è attiva) questa estensione PCNTL deve essere compilata all'interno di PHP.

## Zend Core + Apache

Zend Core è la distribuzione ufficiale di PHP fornito da [zend.com](http://www.zend.com). Essa comprende un installer/updater, Zend Optimizer, supporto Oracle, e le librerie necessarie. Tuttavia, manca il supporto per PostgreSQL, Firebird, e ODBC.

*   Installare [mod_fcgid](https://www.archlinux.org/packages/?name=mod_fcgid), un modulo FastCGI per Apache (quello ufficiale fa schifo).
*   Installare Zend Core (official PHP distribution)
    *   Disinstallare il pacchetto [php](https://www.archlinux.org/packages/?name=php).
    *   Scaricare e installare zend core da [[1]](http://www.zend.com/products/zend_core) ; **non** fategli installare il pacchetto apache o impostare il web server. Si installa sempre in `/usr/local/Zend/Core` per via di un hard-coded path.
    *   Creare uno script `/usr/local/bin/zendcore` e creare dei symlinks a _php_, _php-cgi_, _pear_, _phpize_ sotto _/usr/local/bin_  
        `#!/bin/bash  
        export LD_LIBRARY_PATH="/usr/local/Zend/Core/lib"  
        exec /usr/local/Zend/Core/bin/`basename $0` "$@"`
*   Setup Apache:
    *   In `/etc/httpd/conf/httpd.conf`, aggiungere  
        `LoadModule fcgid_module modules/mod_fcgid.so  
        <Directory /srv/http>  
        AddHandler fcgid-script .php  
        FCGIWrapper /usr/local/bin/php-cgi .php  
        Options ExecCGI  
        Allow from all  
        </Directory>  
        SocketPath /tmp/fcgidsock  
        SharememPath /tmp/fcgidshm`
    *   Ricordarsi di cambiare il Directory path
*   Disabilitare Zend Optimizer (così si può usare la cache):
    *   Modificare `/etc/php.ini`, decommentare la seguente riga quasi alla fine del file:  
        `zend_extension_manager.optimizer="/usr/local/Zend/Core/lib/zend/optimizer"`

[![Tango-dialog-warning.png](/images/d/d8/Tango-dialog-warning.png)](/index.php/File:Tango-dialog-warning.png)

[![Tango-dialog-warning.png](/images/d/d8/Tango-dialog-warning.png)](/index.php/File:Tango-dialog-warning.png)

**This article or section is out of date.**

**Reason:** Usare APCu/OPcache [https://www.archlinux.org/news/php-55-available-in-the-extra-repository/](https://www.archlinux.org/news/php-55-available-in-the-extra-repository/) (Discuss in [Talk:PHP (Italiano)#](https://wiki.archlinux.org/index.php/Talk:PHP_(Italiano)))

*   Installare APC (Cache PHP alternativa):
    *   Eseguire `pear install pecl.php.net/apc` come superuser.
    *   Modificare `/etc/php.ini`, aggiungere la riga dopo _"; Zend Core extensions..."_ (line 1205):  
        `extension=apc.so`
*   Aggiornare Zend Core e/o installare altre componenti
    *   Basta eseguire `/usr/local/Zend/Core/setup`

## Strumenti per lo sviluppo

### Komodo

Buona integrazione per PHP+HTML+JavaScript. Manca la formattazione del codice e il supporto unicode nei commenti doc.

[Komodo IDE](http://www.activestate.com/products/komodo_ide/) | [Komodo Edit (free)](http://www.activestate.com/products/komodo_edit/)

Aggiungere codifiche personalizzate:

*   Modificare `_KOMODO_INSTALL_DIR_/lib/mozilla/components/koEncodingServices.py`, riga 84, aggiungere:

```
 ('cp950', 'Chinese(CP-950/Big5)', 'CP950', '', 1,'cp950'),
 ('cp936', 'Chinese(CP-936/GB2312)', 'CP936', '', 1,'cp936'),
 ('GB2312', 'Chinese(GB-2312)', 'GB2312', '', 1,'GB2312'),
 ....

```

Il formato è (_encoding name in python_, _description_, _short description_, BOM, _is ASCII-superset?_, _font encoding_)

### Netbeans

Un IDE completo per molti linguaggi incluso PHP. Include caratteristiche come il debug, refactoring, code templating, autocompletamento, funzionalità XML e web design e funzionalità di sviluppo (ottima funzionalità di completamento automatico per CSS e notifiche/suggerimenti per il codice PHP/Javascript).

### Eclipse PDT

[Eclipse PDT](http://www.zend.com/pdt) non è molto completo allo stato attuale (v0.7).

Necessita di altri plugin per il supporto di JavaScript e delle query al database.

### Zend Studio

[Zend Studio](http://www.zend.com/products/studio/) è il PHP IDE ufficiale, basato su eclipse. Ha l'autocompletamento, formattazione del codice avanzata, editor HTML WYSIWYG, refactoring, e tutte le funzionalità di eclipse come l'accesso al database, l'integrazione del version control e qualunque altra cosa si possa ottenere da altri plugin per eclipse. Si può installare il pacchetto [zendstudio](https://aur.archlinux.org/packages/zendstudio/)<sup><small>AUR</small></sup> su AUR.

### Aptana Studio

Un buon IDE per PHP e web development. La versione corrente (3.2.2) non ha un debugger PHP.

### Zend Code Analyzer

Un analizzatore di codice PHP di Zend Studio. Indispensabile per ogni programmatore PHP che si rispetti.

#### Installazione

*   Scaricare ed installare Zend Studio Neon
*   Nella cartella di installazione, eseguire `find . -name "ZendCodeAnalyzer` per avere il percorso.
*   Copiare ZendCodeAnalyzer in `/usr/local/bin/zca`
*   Ora si può rimuovere zend studio; non serve nessuna chiave o cos'altro.

#### Vim Integration

Aggiungere le seguenti righe nel proprio `.vimrc`:

```
autocmd FileType php setlocal makeprg=zca\ %<.php
autocmd FileType php setlocal errorformat=%f(line\ %l):\ %m

```

#### Eclipse Integration

_Error Link_ plugin:

*   Symlink _zca_ verso _build.zca_ (così Error Link può riconoscerlo)
*   Installare [Sunshade](http://sunshade.sourceforge.net/) plugin suite;
*   Preference -> Sunshade -> Error Link -> Add: _`^(.*\.php)\(line (\d+)\): ()(.*)`_
*   Run -> External Tools -> Open External Tools Dialog -> Select "Program" -> Click on "New":  
    Name: Zend Code Analyzer  
    Location: _/usr/local/bin/build.zca_  
    Working Directory: _${container_loc}_  
    Arguments: _--recursive ${resource_name}_

#### Komodo Integration

Toolbox -> Add -> New Command:

*   Command: _zca --recursive %F_
*   Run in: Command Output Tab
*   Parse output with: _`^(?P<file>.+?)\(line (?P<line>\d+)\): (?P<content>.*)$`_
*   Select _Show parsed output as a list_

## Risoluzione problemi

### PHP Fatal error: Class 'ZipArchive' not found

Assicurarsi che l'estensione zip sia abilitata.

 `$ grep zip /etc/php/php.ini`  `extension=zip.so` 

### /etc/php/php.ini not parsed

Se il proprio php.ini non viene analizzato, il file ini è denominato in base alla SAPI che si sta utilizzando. Per esempio se si sta utilizzando UWSGI il file dovrebbe essere nominato /etc/php/php-uwsgi.ini, se si sta utilizzando CLI /etc/php/php-cli.ini

## Altre risorse

*   [PHP Official Website](http://www.php.net/)

Retrieved from "[https://wiki.archlinux.org/index.php?title=PHP_(Italiano)&oldid=415677](https://wiki.archlinux.org/index.php?title=PHP_(Italiano)&oldid=415677)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [Programming languages (Italiano)](/index.php/Category:Programming_languages_(Italiano) "Category:Programming languages (Italiano)")

Hidden category:

*   [Pages or sections flagged with Template:Out of date](/index.php/Category:Pages_or_sections_flagged_with_Template:Out_of_date "Category:Pages or sections flagged with Template:Out of date")