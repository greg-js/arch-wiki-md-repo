Prodotto dall'iniziativa [OLPC](http://en.wikipedia.org/wiki/One_Laptop_per_Child), [Sugar](http://en.wikipedia.org/wiki/Sugar_(GUI)) è un ambiente desktop simile a [KDE](/index.php/KDE "KDE") e [GNOME](/index.php/GNOME "GNOME"), ma orientata verso i bambini e l'istruzione. Se avete un figlio giovane, figlia, fratello, sorella, cucciolo o alieno, il modo migliore per introdurli al mondo di Arch Linux è fargli utilizzare una piattaforma Arch/Sugar. La bellezza di un sistema Arch Linux (TM), e che una volta installato e ben configurato, lo si può utilizzare tranquillamente senza difficoltà, anche da un bambino in questo caso. (Ma bisogna sapere come configurarla).

Per facilitarne l'installazione e buona norma reperire alcuni pacchetti relativi a Sugar da [AUR](/index.php/AUR "AUR").

Sugar ha una speciale tassonomia per nominare le parti del suo sistema. Il desktop in sè costituisce il gruppo glucosio. Questo è il sistema di base che è ragionevolmente possibile aspettarsi di ottenere con l'installazione. Ma per usare realmente l'ambiente, si ha bisogno delle attività. Le attività Basic e Sample sono parte di fruttosio. Quindi, saccarosio è costituito sia da `glucose` che da `fructose` e rappresenta ciò che dovrebbe essere distribuito come un normale ambiente desktop Sugar. Notare che `ribose` (il sistema operativo sottostante) è rimpiazzato da Arch. `Honey` (le attività extra) non sono attualmente fornite in AUR ma possono essere installate come mostrato nella sezione [#Compilazione](#Compilazione).

## Contents

*   [1 Per iniziare: Glucosio](#Per_iniziare:_Glucosio)
    *   [1.1 Compilare da AUR](#Compilare_da_AUR)
    *   [1.2 Compilare da un Bundle](#Compilare_da_un_Bundle)
    *   [1.3 Albero delle dipendenze](#Albero_delle_dipendenze)
    *   [1.4 Compilare tramite gruppi modulari](#Compilare_tramite_gruppi_modulari)
*   [2 Attività](#Attivit.C3.A0)
    *   [2.1 Fruttosio](#Fruttosio)
    *   [2.2 Etoys](#Etoys)
    *   [2.3 Compilazione](#Compilazione)
    *   [2.4 Note](#Note)

## Per iniziare: Glucosio

### Compilare da AUR

Installare [AUR|sugar] da [AUR](/index.php/AUR_(Italiano) "AUR (Italiano)").

### Compilare da un Bundle

Questo [script](http://wiki.sugarlabs.org/go/Development_Team/Jhbuild), previsto dagli sviluppatori, è un sistema perfetto per compilare che permette di scaricare e costruire Sugar quasi nella sua interezza. Vi sarà richiesto di quali pacchetti avete bisogno, ma naturalmente non sono inclusi quei programmi che molti utenti avanzati di Arch richiedono.

Il risultato di questo progetto è offrire Sugar come un bundle. Nonostante la praticità dell'installazione, questo metodo di costruzione non dovrebbe essere incoraggiato, in quanto non è "modulare". Per fare una analogia si può prendere come esempio lo script [easy-e17](/index.php/Enlightenment_(Italiano)#Compilazione_tramite_easy_e17.sh "Enlightenment (Italiano)"), solo che siamo nella situazione opposta per cui non ci sono pacchetti modulari e quindi non vi è ancora una suddivisione in "*gruppi*".

L'aggiunta di alcune disposizioni (*provides*) è una misura di sicurezza. Es:

```
pkgname=sugar-bundle
pkgdesc="The Sugar environment and applications built with jhbuild"
provides=('sugar-desktop') # as in provides=('e')
conflicts=('sugar-desktop')

```

Ma non appena sarà disponibile un nuovo componente nella compilazione di Sugar come un pacchetto separato, deve essere parte del gruppo (e automaticamente il pacchetto bundle andrà in conflitto). Es:

```
pkgname=sugar-toolkit
pkgdesc="The Sugar environment toolkit"
groups=('sugar-desktop' 'sugar-desktop-base')

```

**Nota:** Potrebbe essere possibile usare la nuova funzionalità di "split" di makepkg, in questo caso si finirà per generare una compilazione modulare

### Albero delle dipendenze

Di seguito è riportato l'albero delle dipendenze di 0.86

```
|--sugar
   |--hicolor-icon-theme
   |--shared-mime-info
   |--metacity
   |--libwnck
   |--pygtksourceview2
   |--sugar-artwork
   |--python-xklavier
   |  |--libxklavier
   |  |--pygobject
   |  |--gtk2
   |--sugar-toolkit
      |--alsa-lib
      |--gnome-python-desktop
      |--hippo-canvas
      |  |--librsvg
      |     |--gtk2
      |     |--libcroco
      |--sugar-datastore
      |  |--dbus-python
      |  |--xapian-python-bindings
      |  |--python-cjson
      |  |--sugar-base
      |     |--pygobject
      |     |--python-decorator
      |--sugar-presence-service
         |--telepathy-gabble
         |--telepathy-salut
         |--python-telepathy
         |--sugar-base
         |  |--pygobject
         |  |--python-decorator
         |--gnome-python
            |--pygtk
            |--pyorbit
            |--libgnomeui
               |--libsm

```

### Compilare tramite gruppi modulari

Questa è la strada più adeguata da seguire. Di seguito viene fornita la lista attuale delle dipendenze osservate, acquisita da dall'albero di compilazione delle distribuzioni supportate da Sugar ( in particolare Gentoo):

```
# Syntax: pkgname .. :-> location + comment1 + comment2 ..

espeak			 :-> [community]
squeak			 :-> [unsupported]
evince			 :-> [extra]
pyabiword		 :-> [unsupported]
python-cjson		 :-> [community]
python-telepathy	 :-> [community]
gstreamer0.10-espeak	 :-> [unsupported]
olpcsound		 :-> [unsupported]
telepathy-glib		 :-> [community]
xulrunner		 :-> [extra]
telepathy-gabble	 :-> [community]
telepathy-salut         :-> [community]
hippo-canvas		 :-> [unsupported]

```

## Attività

### Fruttosio

Tutte le attività di `fructose` sono disponibili su AUR come `sugar-activity-**acttività**`:

*   [sugar-activity-browse](https://aur.archlinux.org/packages/sugar-activity-browse/)
*   [sugar-activity-calculate](https://aur.archlinux.org/packages/sugar-activity-calculate/)
*   [sugar-activity-chat](https://aur.archlinux.org/packages/sugar-activity-chat/)
*   [sugar-activity-imageviewer](https://aur.archlinux.org/packages/sugar-activity-imageviewer/)
*   [sugar-activity-jukebox](https://aur.archlinux.org/packages/sugar-activity-jukebox/)
*   [sugar-activity-log](https://aur.archlinux.org/packages/sugar-activity-log/)
*   [sugar-activity-pippy](https://aur.archlinux.org/packages/sugar-activity-pippy/)
*   [sugar-activity-read](https://aur.archlinux.org/packages/sugar-activity-read/)
*   [sugar-activity-terminal](https://aur.archlinux.org/packages/sugar-activity-terminal/)
*   [sugar-activity-turtleart](https://aur.archlinux.org/packages/sugar-activity-turtleart/)
*   [sugar-activity-write](https://aur.archlinux.org/packages/sugar-activity-write/)

### Etoys

`etoys` è fornito separatamente e fa parte di Glucosio, ma includono anche l'attività di Fruttosio, ed è disponibile su AUR con il pacchetto [etoys](https://aur.archlinux.org/packages/etoys/).

### Compilazione

Ora avete un ambiente di lavoro Sugar, è il momento di popolarlo con attività come un browser, una calcolatrice, un visualizzatore di immagini o giochi e giocattoli. Quasi tutti hanno la stessa procedura di compilazione, un file `setup.py` che chiama le funzioni fornite con Sugar. Ecco un tipico `PKGBUILD`:

 `PKGBUILD` 
```
# Contributor: Name <name@mail.com>
pkgname=sugar-activity-calculate
_realname=Calculate
pkgver=30
pkgrel=1
pkgdesc="A calculator for Sugar."
arch=('i686' 'x86_64')
url="[http://www.sugarlabs.org/](http://www.sugarlabs.org/)"
license=('GPL')
groups=('sucrose' 'fructose')
depends=('sugar')
source=([http://download.sugarlabs.org/sources/sucrose/fructose/${_realname}/${_realname}-$pkgver.tar.bz2](http://download.sugarlabs.org/sources/sucrose/fructose/${_realname}/${_realname}-$pkgver.tar.bz2))
md5sums=('011bd911516f27d05194320164c7dcd7')

build() {
  cd "$srcdir/${_realname}-$pkgver"
  ./setup.py install --prefix="$pkgdir/usr" || return 1
}
# vim:set ts=2 sw=2 et:
```

Potrebbe essere necessario eseguire `squeak` per alcune attività (come `etoys`).

### Note

*   La procedura della compilazione delle attività non è fatta per creare pacchetti e l'uso dell'opzione `--prefix` può essere dannoso se l'applicazione utilizza questo percorso internamente. Un sistema corretto sarebbe quello di specificare il percorso durante la procedura di installazione di `sugar` in modo che accetti un argomento come `--destdir=`.

*   Si *suggerisce* di generare pacchetti per le attività di Sugar in AUR utilizzando un prefisso -attività (`sugar-activity-`).

*   Potrebbe essere necessario installare `python-pygame` se le attività non dovessero avviarsi.