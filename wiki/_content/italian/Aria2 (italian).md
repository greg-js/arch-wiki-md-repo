[aria2](http://aria2.sourceforge.net/) è un [download manager](https://en.wikipedia.org/wiki/Download_Manager e [Metalink](https://en.wikipedia.org/wiki/Metalink "wikipedia:Metalink"). aria2 è considerato uno dei programmi più veloci e leggeri della sua categoria disponibile per molte piattaforme. È uno strumento flessibile per merito dell'ampio numero di opzioni utilizzabili anche nei file di configurazione e per la possibilità di essere gestito tramite [XML-RPC](https://en.wikipedia.org/wiki/XML-RPC "wikipedia:XML-RPC") e [JSON-RPC](https://en.wikipedia.org/wiki/JSON-RPC "wikipedia:JSON-RPC").

## Contents

*   [1 Installazione](#Installazione)
*   [2 Esecuzione](#Esecuzione)
*   [3 Configurazione](#Configurazione)
    *   [3.1 aria2.conf](#aria2.conf)
    *   [3.2 Esempio di .bash_alias](#Esempio_di_.bash_alias)
    *   [3.3 Esempio di aria2.conf](#Esempio_di_aria2.conf)
        *   [3.3.1 Dettaglio delle opzioni](#Dettaglio_delle_opzioni)
            *   [3.3.1.1 Esempio di file di input #1](#Esempio_di_file_di_input_.231)
            *   [3.3.1.2 Esempio di file di input #2](#Esempio_di_file_di_input_.232)
        *   [3.3.2 Additional Notes](#Additional_Notes)
    *   [3.4 Example aria2.rapidshare](#Example_aria2.rapidshare)
        *   [3.4.1 Option Details](#Option_Details)
        *   [3.4.2 Additional Notes](#Additional_Notes_2)
    *   [3.5 Example aria2.bittorrent](#Example_aria2.bittorrent)
        *   [3.5.1 Option Details](#Option_Details_2)
    *   [3.6 Frontends](#Frontends)
*   [4 Useful Tips & Tricks](#Useful_Tips_.26_Tricks)
    *   [4.1 pacman XferCommand](#pacman_XferCommand)
    *   [4.2 Custom Minimal Build](#Custom_Minimal_Build)
        *   [4.2.1 Minimal PKGBUILD Example](#Minimal_PKGBUILD_Example)
    *   [4.3 aria2 sometimes stops downloading without exiting](#aria2_sometimes_stops_downloading_without_exiting)
*   [5 Riferimenti esterni](#Riferimenti_esterni)

## Installazione

Installate [aria2](https://www.archlinux.org/packages/?name=aria2) dai [repository ufficiali](/index.php/Official_repositories_(Italiano) "Official repositories (Italiano)").

Potreste trovare utile installare [aria2-systemd](https://github.com/GutenYe/systemd-units/tree/master/aria2).

## Esecuzione

Per motivi di retrocompatibilità il programma si chiama `aria2c`.

## Configurazione

### aria2.conf

aria2 legge il file `~/.aria2/aria2.conf` per ottenere le impostazioni generali desiderate. Si può scegliere un file di configurazione alternativo tramite l'opzione `--conf-path`:

*   Per scaricare `aria2.example.rar` si sceglie il file di configurazone `/file/aria2.rapidshare`

```
$ aria2c --conf-path=/file/aria2.rapidshare [http://rapidshare.com/files/12345678/aria2.example.rar](http://rapidshare.com/files/12345678/aria2.example.rar)

```

Se `~/.aria2/aria2.conf` esiste ma si vogliono applicare solo le impostazioni in `/file/aria2.rapidshare` si deve aggiungere l'opzione `--no-conf`:

*   Do not use the default configuration file and download `aria2.example.rar` using the options specified in the configuration file `/file/aria2.rapidshare`

```
$ aria2c --no-conf --conf-path=/file/aria2.rapidshare [http://rapidshare.com/files/12345678/aria2.example.rar](http://rapidshare.com/files/12345678/aria2.example.rar)

```

### Esempio di .bash_alias

```
alias down='aria2c --conf-path=${HOME}/.aria2/aria2.conf'
alias rapid='aria2c --conf-path=/file/aria2.rapidshare'

```

### Esempio di aria2.conf

```
continue
dir=${HOME}/Desktop
file-allocation=none
input-file=${HOME}/.aria2/input.conf
log-level=warn
max-connection-per-server=4
min-split-size=5M
on-download-complete=exit

```

Questo è equivalente a scrivere il comando:

```
$ aria2c dir=${HOME}/Desktop file-allocation=none input-file=${HOME}/.aria2/input.conf on-download-complete=exit log-level=warn FILE

```

**Note:** Il precedente esempio di aria2.conf può usare in modo sbagliato la variabile $HOME. Some users have reported the curly brace syntax to explicitly create a separate ${HOME} subdirectory in the aria2 working directory. Such a directory may be difficult to traverse as bash will consider it to be the $HOME environment variable. Per adesso si raccomanda di usare percorsi assoluti in `aria2.conf`.

#### Dettaglio delle opzioni

	`continue`

	Continua il download di un file scaricato parzialmente se esiste un corrispondente file di controllo.

	`dir=${HOME}/Desktop`

	Archivia i file scaricati in `~/Desktop`.

	`file-allocation=none`

	Non prepara spazio su disco prima che cominci il download. (Valore predefinito: prealloc) 

	`input-file=${HOME}/.aria2/input.conf`

	Download a list of line, or TAB separated URIs found in `~/.aria2/input.conf`

	`log-level=warn`

	Set log level to output warnings and errors only. (Default: debug)

	`max-connection-per-server=4`

	Set a maximum of four (4) connections to each server per file. (Default: 1)

	`min-split-size=5M`

	Only split the file if the size is larger than 2*5MB = 10MB. (Default: 20M)

	`on-download-complete=exit`

	Run the `exit` command and exit the shell once the download session is complete.

##### Esempio di file di input #1

*   Scarica `aria2-1.10.0.tar.bz2` da due fonti separate in `~/Desktop` per unirle in `aria2-1.10.0.tar.bz2`

```
[http://aria2.net/files/stable/aria2-1.10.0/aria2-1.10.0.tar.bz2](http://aria2.net/files/stable/aria2-1.10.0/aria2-1.10.0.tar.bz2)    [http://sourceforge.net/projects/aria2/files/stable/aria2-1.10.0/aria2-1.10.0.tar.bz2](http://sourceforge.net/projects/aria2/files/stable/aria2-1.10.0/aria2-1.10.0.tar.bz2)

```

##### Esempio di file di input #2

*   Scarica `aria2-1.9.5.tar.bz2` e lo salva in `/file/old` come `aria2.old.tar.bz2` &
*   Scarica `aria2-1.10.0.tar.bz2` e lo salva in `~/Desktop` come `aria2.new.tar.bz2`

```
[http://aria2.net/files/stable/aria2-1.9.5/aria2-1.9.5.tar.bz2](http://aria2.net/files/stable/aria2-1.9.5/aria2-1.9.5.tar.bz2)
  dir=/file/old
  out=aria2.old.tar.bz2
[http://aria2.net/files/stable/aria2-1.10.0/aria2-1.10.0.tar.bz2](http://aria2.net/files/stable/aria2-1.10.0/aria2-1.10.0.tar.bz2)
  out=aria2.new.tar.bz2

```

#### Additional Notes

	 `--file-allocation=falloc`

	Recommended for newer file systems such as ext4 (with extents support), btrfs or xfs as it allocates large files (GB) almost instantly. Do not use falloc with legacy file systems such as ext3 as prealloc consumes approximately the same amount of time as standard allocation would while locking the aria2 process from proceeding to download.

**Tip:** See `aria2c -help#all` and the aria2 man page for a complete list of configuration options.

### Example aria2.rapidshare

```
http-user=USER_NAME
http-passwd=PASSWORD
allow-overwrite=true
dir=/file/Downloads
file-allocation=falloc
enable-http-pipelining=true
input-file=/file/input.rapidshare
log-level=error
max-connection-per-server=2
summary-interval=120

```

#### Option Details

	`http-user=USER_NAME`

	Set HTTP [username](https://en.wikipedia.org/wiki/User_(computing) as USER_NAME for password-protected logins. This affects all [URIs](https://en.wikipedia.org/wiki/Uniform_Resource_Identifier "wikipedia:Uniform Resource Identifier").

	`http-passwd=PASSWORD`

	Set HTTP [password](https://en.wikipedia.org/wiki/Password "wikipedia:Password") as PASSWORD for password-protected logins. This affects all URIs.

	`allow-overwrite=true`

	Restart download if a corresponding control file does not exist. (Default: false)

	`dir=/file/Downloads`

	Store the downloaded file(s) in `/file/Downloads`.

	`file-allocation=falloc`

	Call [posix_fallocate()](http://www.kernel.org/doc/man-pages/online/pages/man2/fallocate.2.html) to allocate disk space before downloading begins. (Default: prealloc)

	`enable-http-pipelining=true`

	Enable [HTTP/1.1 pipelining](https://en.wikipedia.org/wiki/HTTP_Pipelining "wikipedia:HTTP Pipelining") to overcome network latency and to reduce network load. (Default: false)

	`input-file=/file/input.rapidshare`

	Download a list of single line of TAB separated URIs found in `/file/input.rapidshare`

	`log-level=error`

	Set log level to output errors only. (Default: debug)

	`max-connection-per-server=2`

	Set a maximum of two (2) connections to each server per file. (Default: 1)

	`summary-interval=120`

	Output download progress summary every 120 seconds. (Default: 60) 

#### Additional Notes

*   Because `aria2.rapidshare` the contains a username and password, it is advisable to set permissions on the file to 600, or similar.

```
arch ~ $ cd /file
arch /file  $ chmod 600 /file/aria2.rapidshare
arch /file $ ls -l
total 128M
-rw------- 1 arch users  167 Aug 20 00:00 aria2.rapidshare

```

	 `summary-interval=0`

	Supresses download progress summary output and may improve overall performance. Logs will continue to be output according to the value specified in the `log-level` option.

**Tip:** The example configuration file can also be applied to [Hotfile](http://www.hotfile.com/), [DepositFiles](http://depositfiles.com/), et.al.

**Note:** Command-line options always take precedence over options listed in a configuration file.

### Example aria2.bittorrent

```
bt-seed-unverified
max-overall-upload-limit=1M
max-upload-limit=128K
seed-ratio=5.0
seed-time=240

```

#### Option Details

	`bt-seed-unverified=false`

	Do not check the hash of the file(s) before seeding. (Default: true)

	`max-overall-upload-limit=1M`

	Set maximum overall upload speed to 1MB/sec (Default: 0)

	`max-upload-limit=128K`

	Set maximum upload speed per torrent to 128K/sec (Default: 0)

	`seed-ratio=5.0`

	Seed completed torrents until share ratio reaches 5.0\. (Default: 1.0)

	`seed-time=240`

	Seed completed torrents for 240 minutes.

**Note:** If both `seed-ratio` and `seed-time` are specified, seeding ends when at least one of the conditions is satisfied.

### Frontends

In order to use frontends start aria2c with `--enable-rpc` option. Here is a list of available UIs.

**Warning:** Note that configurations changed using these tools are not stored.

*   **Diana** — A command line tool

	[https://github.com/baskerville/diana](https://github.com/baskerville/diana) || [diana-git](https://aur.archlinux.org/packages/diana-git/)

*   **Webui** — Html frontend

	[https://github.com/ziahamza/webui-aria2](https://github.com/ziahamza/webui-aria2) ||

It is convenient to append a monitor function based on diana in your shell configuration file:

```
da(){ watch -ctn 1 "(echo -e '\033[32mGID\t\t Name\t\t\t\t\t\t\t%\tDown\tSize\tSpeed\tUp\tS/L\tTime\033[36m'; diana list| cut -c -112; echo -e '\033[37m'; diana stats)" }

```

## Useful Tips & Tricks

### pacman XferCommand

aria2c can be used as the default download manager for the [pacman](/index.php/Pacman "Pacman") package manager. See the [ArchWiki](/index.php/Main_page "Main page") article [Improve Pacman Performance](/index.php/Improve_pacman_performance "Improve pacman performance") for additional details.

### Custom Minimal Build

Gains in application response can be gleaned by removing unused features and protocols. Further gains can be accomplished by removing support for external libraries with a custom build. The following example creates an `aria2c` executable with HTTP/HTTPS, FTP download and asynchronous DNS support only. See the [Arch Build System](/index.php/Arch_Build_System "Arch Build System") page for further details.

#### Minimal PKGBUILD Example

```
pkgname=aria2
pkgver=1.10.0
pkgrel=100
pkgdesc="Download utility that supports HTTP(S) and FTP"
arch=('i686' 'x86_64')
url="[http://aria2.sourceforge.net/](http://aria2.sourceforge.net/)"
license=('GPL')
depends=('c-ares' 'gnutls' 'zlib' 'ca-certificates')
source=([http://downloads.sourceforge.net/aria2/aria2-${pkgver}.tar.bz2](http://downloads.sourceforge.net/aria2/aria2-${pkgver}.tar.bz2))
md5sums=('1386df9b2003f42695062a0e1232e488')

build() {
  cd ${srcdir}/${pkgname}-${pkgver}

 ./configure --disable-bittorrent --disable-metalink \
 --disable-dependency-tracking --disable-xmltest --disable-nls \
 --without-sqlite3 --without-libxml2 --without-libexpat \
 --with-ca-bundle=/etc/ssl/certs/ca-certificates.crt --prefix=/usr

 make
}

package() {
	cd ${srcdir}/${pkgname}-${pkgver}
	make DESTDIR=${pkgdir} install
}

```

### aria2 sometimes stops downloading without exiting

You can use this little script to restart the download every 30 minutes:

```
 #! /bin/bash

 if [ ! -x /usr/bin/aria2c ]; then
     echo "aria2c is not installed"
     exit 1
 fi

 if [ ! -d ~/.torrentdl ]; then
     mkdir ~/.torrentdl
 fi

 while :; do
     for i in $@; do
         MAGNET=false
 	if [[ "$i" = magnet* ]]; then
 	    MAGNET=true
 	elif [ ! -f "$i" ]; then
 	    echo "The file ('$i') is not given or does not exist"
 	    exit 1
 	fi
 	if ! aria2c --hash-check-only=true "$i" &> /dev/null; then
 	    aria2c "$i"
 	    sleep 30m && kill -9 $(pidof aria2c)
 	else
 	    echo "Torrent is downloaded!"
 	fi
     done
 done

```

## Riferimenti esterni

*   [Wiki di aria2](http://sourceforge.net/apps/trac/aria2/wiki) - Sito ufficiale
*   [Come si usa aria2](http://sourceforge.net/apps/trac/aria2/wiki/UsageExample) - Sito ufficiale
*   [Aria2c attraverso un tunnel VPN](http://gotux.net/arch-linux/aria2c-downloader-through-vpn-tunnel/) - sito non ufficiale