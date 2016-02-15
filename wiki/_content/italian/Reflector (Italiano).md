[Reflector](http://xyne.archlinux.ca/projects/reflector/) è uno script che permette di ottenere una lista di mirror dalla pagina [MirrorStatus](https://www.archlinux.org/mirrors/status/), filtrarli in base al loro aggiornamento, ordinarli per velocità e sovrascrive il file `/etc/pacman.d/mirrorlist`.

## Installazione

[Installare](/index.php/Pacman_(Italiano) "Pacman (Italiano)") [reflector](https://www.archlinux.org/packages/?name=reflector) dai [repository ufficiali](/index.php/Official_repositories "Official repositories").

## Usage

**Warning:** È prudente fare una copia di backup di `/etc/pacman.d/mirrorlist` prima di procedere: `# cp -vf /etc/pacman.d/mirrorlist /etc/pacman.d/mirrorlist.backup`

Il seguente comando ottiene cinque mirror scelti in base alla velocità e sovrascrive `/etc/pacman.d/mirrorlist`:

```
# reflector --verbose -l 5 --sort rate --save /etc/pacman.d/mirrorlist

```

Il seguente comando genera una lista di 200 server HTTP fra i più aggiornati, li ordina per velocità di scaricamento e sovrascrive `/etc/pacman.d/mirrorlist`:

```
# reflector --verbose -l 200 -p http --sort rate --save /etc/pacman.d/mirrorlist

```

Il seguente comando genera una lista di massimo 200 server HTTP fra i più aggiornati che si trovino in Italia, Francia e Germania, li ordina per velocità di download e sovrascrive `/etc/pacman.d/mirrorlist`:

```
# reflector --verbose -c Germany -c France -c Italy -l 200 -p http --sort rate --save /etc/pacman.d/mirrorlist

```

Per ottenere tutti i comandi:

```
# reflector --help

```

**Warning:** Assicurarsi che `/etc/pacman.d/mirrorlist` non contenga voci sospette prima di usare pacman.