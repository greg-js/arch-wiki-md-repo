[Transmission](http://www.transmissionbt.com/) è un client BitTorrent leggero e cross-platform. È il client BitTorrent di default in molte distribuzioni Linux.

## Installazione

Ci sono diverse opzioni nei [Repository Ufficiali](/index.php/Official_repositories_(Italiano) "Official repositories (Italiano)"):

	[transmission-cli](https://www.archlinux.org/packages/?name=transmission-cli)

	include i tools CLI, il demone e il web client.

	[transmission-gtk](https://www.archlinux.org/packages/?name=transmission-gtk)

	GTK+ GUI.

	[transmission-qt](https://www.archlinux.org/packages/?name=transmission-qt)

	Qt GUI.

## Configurazione

Per [transmission-gtk](https://www.archlinux.org/packages/?name=transmission-gtk) e [transmission-qt](https://www.archlinux.org/packages/?name=transmission-qt), il percorso di default del file di configurazione è `~/.config/transmission`.

Per [transmission-cli](https://www.archlinux.org/packages/?name=transmission-cli), il percorso di configurazione di default è `~/.config/transmission-daemon`.

### Lanciare come demone

Per lanciare transmission come un [demone](/index.php/Daemon_(Italiano) "Daemon (Italiano)"), è necessario aver installato [transmission-cli](https://www.archlinux.org/packages/?name=transmission-cli).

Editare `/etc/conf.d/transmissiond` e modificare l'utente usato per scaricare:

```
 TRANS_USER="<your user name>"

```

Quindi avviare il demone:

```
# systemctl start transmission

```

Navigate su `[http://127.0.0.1:9091](http://127.0.0.1:9091)` nel vostro browser web e potete vedere il Web client.

Per modificare le vostre preferenze, editare il file di configurazione principale in:

*   `/var/lib/transmission/.config/transmission-daemon/settings.json` se transmission è stato avviato con lo username di default `transmission`;
*   `~/.config/transmission-daemon/settings.json` se transmission è stato avviato con un diverso utente.

**Note:**

*   Se non si trova la cartella `~/.config/transmission-daemon`, lanciare una volta `transmission-daemon` per crearla.
*   È necessario **fermare** il demone prima di editare il file si configurazione, o le tue modifice **non** saranno salvate.