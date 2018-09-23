Articoli correlati

*   [Xfce](/index.php/Xfce "Xfce")
*   [GNOME Files](/index.php/GNOME_Files "GNOME Files")

[Thunar](http://thunar.xfce.org/index.html) è un file manager che ha l'obiettivo di essere veloce, leggero e facile da usare. È parte integrante del desktop [xfce4](https://www.archlinux.org/groups/x86_64/xfce4/), ma è possibile usarlo anche in maniera indipendente. Ciò lo rende molto attraente per utenti di vari window manager autonomi, come [Openbox](/index.php/Openbox_(Italiano) "Openbox (Italiano)"), [Awesome](/index.php/Awesome3_(Italiano) "Awesome3 (Italiano)") e anche [Compiz](/index.php/Compiz_(Italiano) "Compiz (Italiano)") se usato in maniera *standalone*.

## Contents

*   [1 Installazione](#Installazione)
*   [2 Automount](#Automount)
*   [3 Thunar Volume Manager](#Thunar_Volume_Manager)
    *   [3.1 Installazione](#Installazione_2)
    *   [3.2 Configurazione](#Configurazione)
*   [4 Consigli utili](#Consigli_utili)
    *   [4.1 Usare Thunar per esplorare cartelle remote](#Usare_Thunar_per_esplorare_cartelle_remote)
    *   [4.2 Eseguire in Modalità Demone](#Eseguire_in_Modalit.C3.A0_Demone)
    *   [4.3 Tema icone](#Tema_icone)
    *   [4.4 Partenza lenta "da freddo"](#Partenza_lenta_.22da_freddo.22)
*   [5 Altri plugin e addon](#Altri_plugin_e_addon)
    *   [5.1 Thunar Archive Plugin](#Thunar_Archive_Plugin)
        *   [5.1.1 Installazione](#Installazione_3)
    *   [5.2 Thunar Media Tags Plugin](#Thunar_Media_Tags_Plugin)
        *   [5.2.1 Installazione](#Installazione_4)
    *   [5.3 Miniature](#Miniature)
    *   [5.4 Thunar Shares](#Thunar_Shares)
        *   [5.4.1 Installazione](#Installazione_5)
        *   [5.4.2 Configurazione](#Configurazione_2)
*   [6 Azioni personalizzate](#Azioni_personalizzate)
    *   [6.1 Scanione virus](#Scanione_virus)
    *   [6.2 Link a Dropbox](#Link_a_Dropbox)
*   [7 Links e Riferimenti](#Links_e_Riferimenti)

## Installazione

[thunar](https://www.archlinux.org/packages/?name=thunar) è presente nei [repository ufficiali](/index.php/Official_repositories_(Italiano) "Official repositories (Italiano)"), quindi è facilmente installabile tramite [pacman](/index.php/Pacman_(Italiano) "Pacman (Italiano)").

Se si ha già installato [Xfce4](/index.php/Xfce_(Italiano) "Xfce (Italiano)") sul proprio sistema, si avrà già installato sicuramente anche Thunar.

## Automount

Thunar usa [gvfs](https://www.archlinux.org/packages/?name=gvfs) per gestire l'automount dei dispositivi inseriti. Per ulteriori informazioni si consulti [GVFS](/index.php/GVFS "GVFS").

## Thunar Volume Manager

Thunar supporta già di suo il montaggio\smontaggio delle periferiche. Questo plugin, però, fornisce funzionalità aggiuntive, come la possibilità di eseguire comandi particolari alla connessione di una periferica o di aprire automaticamente una finestra di Thunar per una periferica appena montata.

#### Installazione

Il pacchetto [thunar-volman](https://www.archlinux.org/packages/?name=thunar-volman) è presente nei [repositories ufficiali](/index.php/Official_repositories_(Italiano) "Official repositories (Italiano)").

#### Configurazione

È possibile configurare l'esecuzione di certe azioni alla connessione di videocamere o player audio. Dopo aver installato il plugin:

1.  Lanciare Thunar e aprire le Preferenze
2.  Sotto la scheda 'Avanzate', spuntare la casella 'Abilita la gestione dei volumi'
3.  Cliccare su 'Configura' e controllare le seguenti entrate:

*   Mount removable drivers when hot-pluged.
*   Mount removable media whe insertd.

1.  Cliccare su Configura e fare le modifiche desiderate.

Ad esempio, per impostare l'apertura di Amarok all'inserimento di un cd audio,

```
Multimedia - CD Audio: `amarok --cdplay %d`

```

## Consigli utili

### Usare Thunar per esplorare cartelle remote

Da Xfce 4.8 e Thunar 1.2 è possibile esplorare cartelle remote (server FTP o cartelle condivise con [Samba](/index.php/Samba_(Italiano) "Samba (Italiano)")) direttamente in Thunar. Una funzionalità simile è disponibile anche con [GNOME](/index.php/GNOME_(Italiano) "GNOME (Italiano)") e [KDE](/index.php/KDE_(Italiano) "KDE (Italiano)"). I pacchetti necessari sono [gvfs](https://www.archlinux.org/packages/?name=gvfs) e [gvfs-smb](https://www.archlinux.org/packages/?name=gvfs-smb), entrambi disponibili nei [repositories ufficiali](/index.php/Official_repositories_(Italiano) "Official repositories (Italiano)").

Dopo aver riavviato Xfce ci sarà un link "Network" nella barra laterale di Thunar e le directory remote si potranno aprire agevolmente con questi URIs nella cartella di dialogo (da aprire con `Ctrl+L`): smb://, ftp:// e ssh:// .

### Eseguire in Modalità Demone

Thunar può essere eseguito in modalità demone. Questo comporta una serie di vantaggi, primo fra tutti una maggiore velocità nell'apertura delle finestre di Thunar (poichè appunto esso sarà in esecuizione in background) all'inserimento, ad esempio, di una chiavetta USB.

Per farlo partire in questa modalità, è possibile utilizzare il file `.xinitrc` o uno script di autostart (come quello di [Openbox](/index.php/Openbox_(Italiano) "Openbox (Italiano)"), il file `~/.config/openbox/autostart`). Un metodo vale l'altro, sta all'utente scegliere quale utilizzare.

Per eseguirlo in questa modalità, è semplicemente necessario lanciare Thunar tramite il comando:

```
thunar --daemon &

```

### Tema icone

Se si sta usando thunar all'infuori di GNOME o Xfce certi file di configurazione potrebbero venire meno. Il file che regola l'aspetto di tutte le applicazioni che sfruttano le gtk2 è ~/.gtkrc-2.0\. Per avere ad esempio le icone "Tango", aggiungere:

```
gtk-icon-theme-name = "Tango"

```

Naturalmente è fondamentale avere installato il pacchetto [gnome-icon-theme](https://www.archlinux.org/packages/?name=gnome-icon-theme) dai [repository ufficiali](/index.php/Official_repositories_(Italiano) "Official repositories (Italiano)").

### Partenza lenta "da freddo"

Alcuni utenti lamentano un avvio lento di Thunar la prima volta che viene avviato. Ciò è dovuto al fatto che gvfs attua un controllo sulla rete e Thunar non si avvio fino a che questo processo è in corso. per cambiare questa caratteristica editare il file: `/usr/share/gvfs/mounts/network.mount` e cambiare **AutoMount=true** in **AutoMount=false**.

## Altri plugin e addon

Molti plugin sono parte del pacchetto [xfce4-goodies](https://www.archlinux.org/groups/x86_64/xfce4-goodies/)

### Thunar Archive Plugin

Thunar Archive Plugin è un frontend per programmi di archiviazione come File Roller, Ark, o Xarchiver che permette un'integrazione tra uno di questi programmi e il menu di Thunar.

#### Installazione

Il pacchetto necessario è [thunar-archive-plugin](https://www.archlinux.org/packages/?name=thunar-archive-plugin) ed è disponibile nei [repository ufficiali](/index.php/Official_repositories_(Italiano) "Official repositories (Italiano)"), quindi facilmente installabile con [Pacman](/index.php/Pacman_(Italiano) "Pacman (Italiano)").

### Thunar Media Tags Plugin

Il plugin media tags mostra informazioni dettagliate sui tag dei file multimediali. Supporta tag su ID3 (MP3) e Ogg/Vorbis. È in grado anche di rinominare i tags di molti file contemporaneamente.

#### Installazione

Thunar Media Tags è installabile con:

```
# pacman -S thunar-media-tags-plugin

```

### Miniature

Thunar si basa su un programma esterno chiamato [tumbler](http://git.xfce.org/xfce/tumbler/tree/README) per generare le miniature. [tumbler](https://www.archlinux.org/packages/?name=tumbler) è installabile con pacman in quanto presente in [extra]. Per generare miniature di video è necessario installare [ffmpegthumbnailer](https://www.archlinux.org/packages/?name=ffmpegthumbnailer) da [[extra]](/index.php/Repository_Ufficiali "Repository Ufficiali").

### Thunar Shares

Thunar Shares è un plugin che permette di condividere cartelle usando Samba da Thunar da utente semplice.

#### Installazione

Installare il pacchetto [thunar-shares-plugin](https://aur.archlinux.org/packages/thunar-shares-plugin/) da [AUR](/index.php/AUR_(Italiano) "AUR (Italiano)").

#### Configurazione

This marks the named objects for automatic export to the environment of subsequently executed commands:

```
# export USERSHARES_DIR="/var/lib/samba/usershares"
# export USERSHARES_GROUP="sambashare"
```

Questo crea la directory var/lib/samba:

 `# mkdir -p ${USERSHARES_DIR}` 

Questo crea il gruppo **sambashare**:

 `# groupadd ${USERSHARES_GROUP}` 

Questo cambia i permessi alla directory appena creata dandoli agli utenti del gruppo **sambashare**:

 `# chown root:${USERSHARES_GROUP} ${USERSHARES_DIR}` 

Questo cambia i permessi delle directory in modo che gli utenti che fanno parte del gruppo **sambashare** abbiano la possibilità di aprire le suddette directory in lettura e scrittura:

 `# chmod 01770 ${USERSHARES_DIR}` 

Usare il proprio editor preferito per creare il file `/etc/samba/smb.conf`

 `# nano /etc/samba/smb.conf` 

Usare questo file di configurazione `smb.conf`:

 `/etc/samba/smb.conf` 
```
  ##This is the main Samba configuration file. You should read the
  ##smb.conf(5) manual page in order to understand the options listed
  ##here. Samba has a huge number of configurable options (perhaps too
  ##many!) most of which are not shown in this example
  ##
  ##For a step to step guide on installing, configuring and using samba, 
  ## read the Samba-HOWTO-Collection. This may be obtained from:
  ##  http://www.samba.org/samba/docs/Samba-HOWTO-Collection.pdf
  ##
  ## Many working examples of smb.conf files can be found in the 
  ## Samba-Guide which is generated daily and can be downloaded from: 
  ##  http://www.samba.org/samba/docs/Samba-Guide.pdf
  ##
  ## Any line which starts with a ; (semi-colon) or a # (hash) 
  ## is a comment and is ignored. In this example we will use a #
  ## for commentry and a ; for parts of the config file that you
  ## may wish to enable
  ##
  ## NOTE: Whenever you modify this file you should run the command "testparm"
  ## to check that you have not made any basic syntactic errors. 
  ##
  #[global]
  #  workgroup = WORKGROUP
  #  security = share
  #  server string = My Share
  #  load printers = yes
  #  log file = /var/log/samba/%m.log
  #  max log size = 50
  #  usershare path = /var/lib/samba/usershares
  #  usershare max shares = 100
  #  usershare allow guests = yes
  #  usershare owner only = yes
  #  
  #
  # #Windows Internet Name Serving Support Section:
  #
  # #WINS Support - Tells the NMBD component of Samba to enable it's WINS Server
  #;   wins support = yes
  #
  ## WINS Server - Tells the NMBD components of Samba to be a WINS Client
  ##	Note: Samba can be either a WINS Server, or a WINS Client, but NOT both
  #;   wins server = w.x.y.z
  #
  ##WINS Proxy - Tells Samba to answer name resolution queries on
  ## behalf of a non WINS capable client, for this to work there must be
  ## at least one	WINS Server on the network. The default is NO.
  #;   wins proxy = yes
```

Salvare il file e aggiungere il proprio utente al gruppo "sambashares" :

 `# usermod -a -G ${USERSHARES_GROUP} your_username` 

Riavviare il demone Samba.

Effettuare un log out e poi riloggarsi. Ora è possibile condividere ogni directory tramite una voce del menu raggiungibile con il click-destro. Se dovesse apparire l'errore `You are not the owner of the folder` provare a riavviare il sistema. Per avere Samba sempre attivo abilitare il relativo `service`. Per maggiori informazioni, visitare la wiki di [Samba](/index.php/Samba_(Italiano) "Samba (Italiano)").

## Azioni personalizzate

Questa sezione tratta delle utilissime azioni personalizzabili che si trovano in Modifica -> Imposta azioni personalizzate. Molti esempi possono essere trovati [sulla wiki di thunar](http://docs.xfce.org/xfce/thunar/custom-actions).

### Scanione virus

È necessario installare clamav e clamtk.

| Nome | Comando | File patterns | Appears if selection contains |
| Scan for virus | clamtk %F | * | Select all |

### Link a Dropbox

<caption>Azione</caption>
| Nome | Comando | File patterns | Appears if selection contains |
| Link a Dropbox | ln -s %f /path/to/DropboxFolder | * | Directories, other files |

Se si usano molti link simbolici a cartelle o file, sarebbe più utile e veloce mettere questi nella cartella `Invia a` del menu contestuale per evitare che questo diventi troppo ingombrante una volta aperto. Questa è un'operazione facile, richiede i file `.desktop` in `~/.local/share/Thunar/sendto` per ogni azione da eseguire. Per esempio, volendo creare un link simbolico alla cartella di dropbox, bisogna creare il file `dropbox_folder.desktop` con il seguente contenuto. Dopo ogni azione personalizzata Thunar va riavviato (se si usa thunar demonizzato va riavviato il demone).

```
[Desktop Entry]
Type=Application
Version=1.0
Encoding=UTF-8
Exec=ln -s %f /percorso/alla/cartella/dropbox
Icon=/usr/share/icons/dropbox.png
Name=Dropbox

```

## Links e Riferimenti

*   [Thunar](http://thunar.xfce.org/index.html) pagina del progetto.
*   [Thunar Volume Manager](http://goodies.xfce.org/projects/thunar-plugins/thunar-volman) pagina del progetto.
*   [Thunar Archive Plugin](http://goodies.xfce.org/projects/thunar-plugins/thunar-archive-plugin) pagina del progetto.
*   [Thunar Media Tags Plugin](http://goodies.xfce.org/projects/thunar-plugins/thunar-media-tags-plugin) pagina del progetto.
*   [Thunar Shares Plugin](http://goodies.xfce.org/projects/thunar-plugins/thunar-shares-plugin/) pagina del progetto.
*   [Lista di plugins](http://goodies.xfce.org/projects/thunar-plugins/start).