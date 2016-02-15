Questa pagina mira a configurare correttamente libgphoto2 così che gli appartenenti al [gruppo](/index.php/Users_and_Groups_(Italiano) "Users and Groups (Italiano)") _camera_ possano accedere a una fotocamera digitale connessa tramite USB. L'obiettivo è stato nel mantenere ciò che è scritto qui, il più semplice possibile, per questo motivo non sono considerati i casi particolari che si possono incontrare.

**Nota:** **dall'autore**: mi piacerebbe cambiare quest'ultima considerazione, così da realizzare una pagina meglio strutturata e che possa essere d'aiuto per tutta la comunità. Sentitevi quindi liberi di aggiungere i vostri problemi\considerazioni nella pagina _discussione_ così che possa magari essere aggiunto qualcosa in una sezione tipo _Risoluzione dei problemi_.

Non tutte le fotocamere digitali sono rilevate con l'opzione --auto-detect (in gphoto2). Alcune fotocamere potrebbero essere riconosciute con un nome generico, o altre avere un nome di un modello differente. Se la fotocamera funziona, non è consigliabile intervenire per sistemare questi _dettagli_.

## Contents

*   [1 Libgphoto2](#Libgphoto2)
    *   [1.1 Installazione e Configurazione](#Installazione_e_Configurazione)
    *   [1.2 Problemi con i permessi](#Problemi_con_i_permessi)
*   [2 GPhoto2](#GPhoto2)
    *   [2.1 Installazione e configurazione](#Installazione_e_configurazione_2)
*   [3 Applicazioni frontend (esterne) per GPhoto2](#Applicazioni_frontend_.28esterne.29_per_GPhoto2)
*   [4 Risoluzione dei problemi](#Risoluzione_dei_problemi)
    *   [4.1 Gruppi](#Gruppi)
*   [5 Articoli wiki relativi a foto e videocamere](#Articoli_wiki_relativi_a_foto_e_videocamere)

## Libgphoto2

[Libgphoto2](http://www.gphoto.org/proj/libgphoto2/) è la principale libreria progettata per fornire accesso ad una fotocamera digitale da programmi esterni, come Digikam o gphoto2\. Le fotocamere supportate _ufficialmente_ sono elencate [qui](http://www.gphoto.org/proj/libgphoto2/support.php) anche se è possibile che ne funzionino delle altre.

### Installazione e Configurazione

Da root, eseguire:

```
# pacman -S libgphoto2

```

E poi:

```
# gpasswd -a $nomeutente camera

```

**Note:** $nomeutente è un qualsiasi account NON root che vogliate aggiungere al gruppo camera.

### Problemi con i permessi

Se si riscontrano problemi di autorizzazioni, digitare da root:

```
# /usr/lib/libgphoto2/print-camera-list udev-rules mode 0660 version 0.98 group camera > /etc/udev/rules.d/90-libgphoto2.rules

```

Se dopo aver seguito i passi precedenti si hanno ancora problemi di accesso, provare a modificare `/etc/udev/rules.d/90-libgphoto2.rules` sostituendo la riga PROGRAM=, nella parte finale del file, con la seguente:

```
PROGRAM="/lib/udev/check-ptp-camera", MODE="0660", GROUP="camera"

```

Se la fotocamera non è presente in nessuna regola di [udev](/index.php/Udev "Udev"), è possibile controllare "vendor" e "id" del prodotto ed aggiungerlo. Per verificarlo basta eseguire:

```
# lsusb
...
Bus 001 Device 005: ID 04a9:318e Canon, Inc.
...

```

Oppure è possibile aggiungere le regole udev locali in `/etc/udev/rules.d/90-local.rules` per garantire che non vengano sovrascrittoe da eventuali nuovi pacchetti.

 `90-local.rules` 

```
PROGRAM="/lib/udev/check-ptp-camera", MODE="0660", GROUP="camera"
ATTRS{idVendor}=="04a9", ATTRS{idProduct}=="318e", MODE="0660",  GROUP="camera"
```

Per fare in modo che le modifiche abbiano effetto è necessario riavviare udevd

```
# killall udevd && udevd -d

```

Ora, dopo aver inserito la fotocamera, è possibile verificare che i permessi siano a posto eseguendo:

```
# ls -lR /dev/bus/usb

```

**Tip:** Può essere raccomandabile eseguire un riavvio.

## GPhoto2

GPhoto2 è un client a riga di comando per libgphoto2\. GPhoto2 consente l'accesso alla libreria libgpohoto2 da un terminale o da uno script di shell per eseguire qualsiasi operazione possibile con la fotocamera. Questa è l'interfaccia utente principale.

GPhoto2 offre inoltre funzionalità di debug utili agli sviluppatori de driver delle fotocamere.

### Installazione e configurazione

Per installare Gphoto2, da root:

```
# pacman -S gphoto2

```

È inoltre possibile installare gvfs-gphoto2 come backend di gphoto2 per gvfs.

```
# pacman -S gvfs-gphoto2

```

**Quick Commands**

*   gphoto2 --list-ports
*   gphoto2 --auto-detect
*   gphoto2 --summary
*   gphoto2 --list-files
*   gphoto2 --get-all-files

Per la manipolazione avanzato dei file, utilizzare

*   gphoto2 --shell

## Applicazioni frontend (esterne) per GPhoto2

*   [gphotofs](http://www.gphoto.org/proj/gphotofs/) - permette di utilizzare la fotocamera con qualsiasi strumento in grado di leggere da un file system montato.
*   [RawTherapee](http://www.rawtherapee.com/)
*   [Darktable](http://darktable.org/)
*   [Digikam](http://www.digikam.org/)
*   [F-Spot](http://f-spot.org/)
*   [Gthumb](http://live.gnome.org/gthumb)
*   [GTKam](http://www.gphoto.org/proj/gtkam/)

## Risoluzione dei problemi

### Gruppi

È necessario che l'utente a cui si desidera concedere l'accesso alla fotocamera appartenga allo [storage group](/index.php/Users_and_groups#Groups "Users and groups").

## Articoli wiki relativi a foto e videocamere

*   [Jalbum](/index.php/Jalbum "Jalbum") - Freeware per la creazione di album professionali e gallerie.