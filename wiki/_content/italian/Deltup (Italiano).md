L'uso degli aggiornamenti delta consente di scaricare meno dati durante la fase di aggiornamento. Questo metodo consiste nello scaricare una sorta di "diff" del pacchetto da aggiornare, che verrà quindi utilizzato per "costruire" il pacchetto per l'aggiornamento dopo il download.

Questa opzione per ArchLinux supporta sia l'architettura i686 che x86_64.

1\. Installare il pacchetto [xdelta3](https://www.archlinux.org/packages/?name=xdelta3):

```
# pacman -S xdelta3 

```

2\. Modificare il file `/etc/pacman.d/mirrorlist` ed aggiungere l'apposito repositroy:

 `/etc/pacman.d/mirrorlist` 

```
##
## Arch Linux repository mirrorlist
## Generated on 2011-03-24
##

## Delta Archlinux.fr
Server = http://delta.archlinux.fr/$repo/os/$arch
.....
```

3\. Controllare prima di attivare l'opzione `UseDelta` a quanto ammonta la dimensione dei file da aggiornare.

```
#  pacman -Syu

 :: Sincronizzazione dei database in corso...
 kde4-eyecandy-64 è aggiornato
 core è aggiornato
 extra è aggiornato
 community è aggiornato
 multilib è aggiornato
 :: Aggiornamento del sistema in corso...
 Attenzione: frozen-bubble: l'aggiornamento del pacchetto è stato ignorato (2.2.0-3 => 2.2.1beta1-1)
 :: Vuoi sostituire lib32-libjpeg con multilib/lib32-libjpeg-turbo? [Y/n] 
 :: Voui sostituire vlc-plugin con extra/vlc? [Y/n] 
 Attenzione: warmux: l'aggiornamento del pacchetto è stato ignorato  (11.01-1 => 11.04.1-3)
 Risoluzione delle dipendenze in corso...
 Attenzione: individuato un possibile ciclo di dipendenze:
 Attenzione: lib32-gcc-libs sarà installato prima della sua dipendenza gcc-libs-multilib
 ricerca dei conflitti in corso...

 Da rimuovere (2): lib32-libjpeg-8.3.0-1 [0,48 MB]  vlc-plugin-1.1.9-1 [0,13 MB]

 Dimensione totale dei pacchetti da rimuovere:   0,61 MB

 Pacchetti (147): attr-2.4.46-1 [0,06 MB]  acl-2.2.51-1 [0,13 MB]  acpid-2.0.10-2 [0,04 MB]
            lib32-gcc-libs-4.6.0-6 [0,71 MB]  gcc-libs-multilib-4.6.0-6 [0,73 MB]
            icu-4.8-1 [5,10 MB]  boost-libs-1.46.1-3 [1,49 MB]  libmysqlclient-5.5.13-1 [2,92 MB]
            mysql-clients-5.5.13-1 [0,79 MB]  mysql-5.5.13-1 [5,70 MB]  akonadi-1.5.3-2 [0,63 MB]
            util-linux-2.19.1-2 [1,37 MB]  apr-1.4.5-1 [0,22 MB]  apr-util-1.3.12-1 [0,14 MB]
            sqlite3-3.7.6.3-1 [0,36 MB]  glib2-2.28.8-1 [1,58 MB]  gstreamer0.10-0.10.34-1 [1,33 MB]
            gstreamer0.10-base-0.10.34-1 [1,13 MB]  gnutls-2.12.6.1-1 [1,49 MB]
            glib-networking-2.28.7-1 [0,04 MB]  libsoup-2.34.2-1 [0,30 MB]
            hunspell-1.3.2-1 [0,18 MB]  enchant-1.6.0-2 [0,03 MB]  libwebkit-1.4.1-1 [5,03 MB]
            pango-1.28.4-3 [0,48 MB]  gstreamer0.10-base-plugins-0.10.34-1 [0,16 MB]
            banshee-2.0.1-2 [2,57 MB]  binutils-multilib-2.21-8 [3,25 MB]  bison-2.5-1 [0,42 MB]
            bluez-4.93-2 [0,49 MB]  boost-1.46.1-3 [6,56 MB]  cairomm-1.10.0-1 [0,41 MB]
            ccrtp-1.8.0-1 [0,17 MB]  nspr-4.8.8-1 [0,22 MB]  nss-3.12.10-1 [1,37 MB]
            chromium-12.0.742.91-1 [19,41 MB]  consolekit-0.4.5-1 [0,08 MB]  gmp-5.0.2-1 [0,41 MB]
            coreutils-8.12-2 [2,00 MB]  module-init-tools-3.13-1 [0,34 MB]  udev-171-2 [0,20 MB]
            device-mapper-2.02.85-2 [0,12 MB]  cryptsetup-1.3.1-1 [0,09 MB]
            libssh2-1.2.7-2 [0,17 MB]  curl-7.21.6-2 [0,46 MB]  libgnome-keyring-3.0.3-1 [0,09 MB]
            libsoup-gnome-2.34.2-1 [0,01 MB]  icon-naming-utils-0.8.90-2 [0,01 MB]
            gnome-icon-theme-3.0.0-2 [8,21 MB]  libgweather-3.0.2-1 [2,15 MB]
            evolution-data-server-3.0.2.1-1 [2,48 MB]  fam-2.7.0-15 [0,07 MB]
            gstreamer0.10-good-0.10.29-1 [0,94 MB]  gstreamer0.10-bad-0.10.22-1 [0,83 MB]
            farsight2-0.0.28-2 [0,21 MB]  file-5.07-3 [0,19 MB]  nspluginwrapper-1.4.2-1 [0,13 MB]
            flashplugin-10.3.181.22-1 [6,02 MB]  gcc-multilib-4.6.0-6 [17,44 MB]
            glew-1.6.0-1 [0,28 MB]  startup-notification-0.12-1 [0,02 MB]  libcups-1.4.6-3 [0,26 MB]
            gtk3-3.0.11-1 [4,66 MB]  gnome-desktop-3.0.2-1 [0,48 MB]  libwnck3-3.0.2-1 [0,34 MB]
            telepathy-glib-0.14.7-1 [1,07 MB]  gnome-panel-3.0.2-1 [1,49 MB]  gperf-3.0.4-3 [0,09 MB]
            grep-2.8-1 [0,17 MB]  libjpeg-turbo-1.1.1-1 [0,20 MB]  v4l-utils-0.8.4-1 [0,23 MB]
            jack-0.120.2-1 [0,28 MB]  gstreamer0.10-good-plugins-0.10.29-1 [0,31 MB]
            gvfs-1.8.2-1 [0,80 MB]  help2man-1.39.4-1 [0,06 MB]  iproute2-2.6.38-3 [0,36 MB]
            kbd-1.15.3-1 [0,98 MB]  initscripts-2011.06.3-1 [0,02 MB]  poppler-0.16.5-1 [0,71 MB]
            poppler-glib-0.16.5-1 [0,17 MB]  inkscape-0.48.1-3 [12,51 MB]
            inputproto-2.0.2-1 [0,04 MB]  jre-6u26-1 [20,85 MB]  kdesdk-okteta-4.6.3-2 [0,54 MB]
            kdesdk-scripts-4.6.3-2 [0,17 MB]  linux-firmware-20110512-2 [9,17 MB]
            mkinitcpio-busybox-1.18.4-1 [0,16 MB]  mkinitcpio-0.6.12-1 [0,02 MB]
            kernel26-2.6.38.8-1 [35,93 MB]  kernel26-headers-2.6.38.8-1 [4,18 MB]
            laptop-mode-tools-1.57-3 [0,05 MB]  less-443-2 [0,09 MB]
            lib32-libjpeg-turbo-1.1.1-1 [0,14 MB]  libass-0.9.12-1 [0,06 MB]
            libdvbpsi-0.2.0-1 [0,05 MB]  libftdi-0.19-1 [0,04 MB]  libgsf-1.14.21-1 [0,18 MB]
            libgssglue-0.1-4 [0,03 MB]  libwps-0.2.2-1 [0,04 MB]  neon-0.29.6-1 [0,17 MB]
            libtextcat-2.2-8 [0,29 MB]  libreoffice-3.4.0-2 [73,84 MB]
            libreoffice-ru-3.4.0-1 [7,76 MB]  libssh-0.5.0-1 [0,11 MB]
            libvncserver-0.9.8-2 [0,23 MB]  libzrtpcpp-1.4.2-5 [0,09 MB]  lvm2-2.02.85-2 [0,54 MB]
            lzo2-2.05-1 [0,07 MB]  make-3.82-3 [0,34 MB]  man-db-2.6.0.2-2 [0,38 MB]
            mercurial-1.8.4-1 [1,36 MB]  net-tools-1.60-16 [0,10 MB]  qt-4.7.3-2 [24,12 MB]
            ntrack-1:13-2 [0,03 MB]  parted-2.4-1 [0,47 MB]  perl-capture-tiny-0.11-1 [0,01 MB]
            php-5.3.6-4 [2,90 MB]  php-pear-5.3.6-4 [0,24 MB]  pixman-0.22.0-1 [0,16 MB]
            pkg-config-0.26-1 [0,03 MB]  poppler-qt-0.16.5-1 [0,11 MB]  raptor-2.0.3-1 [0,23 MB]
            skype-2.2.0.35-1 [21,56 MB]  sox-14.3.2-3 [0,49 MB]  strigi-0.7.5-1 [0,67 MB]
            sudo-1.8.1.p2-1 [0,37 MB]  telepathy-farsight-0.0.18-1 [0,04 MB]
            telepathy-qt4-0.6.1-1 [1,16 MB]  twinkle-1.4.2-10 [1,23 MB]  udisks-1.0.3-3 [0,15 MB]
            upower-0.9.11-1 [0,09 MB]  virtualbox-4.0.8-2 [16,53 MB]  vlc-1.1.10-1 [7,07 MB]
            vte-common-0.28.0-2 [0,00 MB]  vte-0.28.0-2 [0,33 MB]  vte3-0.28.0-2 [0,32 MB]
            webkit-sharp-0.3-2 [0,02 MB]  wine-1.3.21-2 [25,78 MB]  xorg-iceauth-1.0.5-1 [0,01 MB]
            xorg-server-common-1.10.2-1 [0,02 MB]  xorg-server-1.10.2-1 [1,21 MB]
            xorg-xauth-1.0.6-1 [0,02 MB]  xorg-xlsclients-1.1.2-1 [0,01 MB]  xterm-270-1 [0,22 MB]
            xulrunner-2.0.1-2 [18,57 MB]  xvidcore-1.3.2-1 [0,25 MB]  xz-5.0.3-1 [0,31 MB]

 Dimensione totale dei pacchetti da scaricare:   416,89 MB
 Dimensione totale dei pacchetti da installare:   1933,56 MB

 Vuoi procedere con l'installazione? [Y/n]
```

Premere `**N**` per non confermare l'aggiornamento. Notare bene ora le dimensioni dei file da scaricare sono di 416,89 MB

4\. Nel file `/etc/pacman.conf` decommentare (rimuovendo il simbolo `#`) l'opzione `UseDelta`:

 `/etc/pacman.conf` 

```
.....
# Misc options (all disabled by default)
#UseSyslog
ShowSize
UseDelta
TotalDownload
.....
```

5\. Adesso provare nuovamente ad effettuare l'aggiornamento del sistema (questa volta l'opzione `UseDelta` sarà abilitata):

```
# pacman -Syu

 :: Sincronizzazione dei database in corso...
 kde4-eyecandy-64 è aggiornato
 core è aggiornato
 extra è aggiornato
 community è aggiornato
 multilib è aggiornato
 :: Aggiornamento del sistema in corso...
 Attenzione: frozen-bubble: l'aggiornamento del pacchetto è stato ignorato (2.2.0-3 => 2.2.1beta1-1)
 :: Vuoi sostituire lib32-libjpeg con multilib/lib32-libjpeg-turbo? [Y/n] 
 :: Vuoi sostituire vlc-plugin con extra/vlc? [Y/n] 
 Attenzione: warmux: l'aggiornamento del pacchetto è stato ignorato  (11.01-1 => 11.04.1-3)
 Risoluzione delle dipendenze in corso...
 Attenzione: individuato un possibile ciclo di dipendenze:
 Attenzione: lib32-gcc-libs sarà installato prima della sua dipendenza gcc-libs-multilib
 ricerca dei conflitti in corso...

 Da rimuovere (2): lib32-libjpeg-8.3.0-1 [0,48 MB]  vlc-plugin-1.1.9-1 [0,13 MB]

 Dimensione totale dei pacchetti da rimuovere:   0,61 MB

 Pacchetti (147): attr-2.4.46-1 [0,06 MB]  acl-2.2.51-1 [0,13 MB]  acpid-2.0.10-2 [0,04 MB]
            lib32-gcc-libs-4.6.0-6 [0,71 MB]  gcc-libs-multilib-4.6.0-6 [0,73 MB]
            icu-4.8-1 [5,10 MB]  boost-libs-1.46.1-3 [1,49 MB]  libmysqlclient-5.5.13-1 [2,92 MB]
            mysql-clients-5.5.13-1 [0,79 MB]  mysql-5.5.13-1 [5,70 MB]  akonadi-1.5.3-2 [0,63 MB]
            util-linux-2.19.1-2 [1,37 MB]  apr-1.4.5-1 [0,22 MB]  apr-util-1.3.12-1 [0,14 MB]
            sqlite3-3.7.6.3-1 [0,36 MB]  glib2-2.28.8-1 [1,58 MB]  gstreamer0.10-0.10.34-1 [1,33 MB]
            gstreamer0.10-base-0.10.34-1 [1,13 MB]  gnutls-2.12.6.1-1 [1,49 MB]
            glib-networking-2.28.7-1 [0,04 MB]  libsoup-2.34.2-1 [0,30 MB]
            hunspell-1.3.2-1 [0,18 MB]  enchant-1.6.0-2 [0,03 MB]  libwebkit-1.4.1-1 [5,03 MB]
            pango-1.28.4-3 [0,48 MB]  gstreamer0.10-base-plugins-0.10.34-1 [0,16 MB]
            banshee-2.0.1-2 [2,57 MB]  binutils-multilib-2.21-8 [3,25 MB]  bison-2.5-1 [0,42 MB]
            bluez-4.93-2 [0,49 MB]  boost-1.46.1-3 [6,56 MB]  cairomm-1.10.0-1 [0,41 MB]
            ccrtp-1.8.0-1 [0,17 MB]  nspr-4.8.8-1 [0,22 MB]  nss-3.12.10-1 [1,37 MB]
            chromium-12.0.742.91-1 [19,41 MB]  consolekit-0.4.5-1 [0,08 MB]  gmp-5.0.2-1 [0,41 MB]
            coreutils-8.12-2 [2,00 MB]  module-init-tools-3.13-1 [0,34 MB]  udev-171-2 [0,20 MB]
            device-mapper-2.02.85-2 [0,12 MB]  cryptsetup-1.3.1-1 [0,09 MB]
            libssh2-1.2.7-2 [0,17 MB]  curl-7.21.6-2 [0,46 MB]  libgnome-keyring-3.0.3-1 [0,09 MB]
            libsoup-gnome-2.34.2-1 [0,01 MB]  icon-naming-utils-0.8.90-2 [0,01 MB]
            gnome-icon-theme-3.0.0-2 [8,21 MB]  libgweather-3.0.2-1 [2,15 MB]
            evolution-data-server-3.0.2.1-1 [2,48 MB]  fam-2.7.0-15 [0,07 MB]
            gstreamer0.10-good-0.10.29-1 [0,94 MB]  gstreamer0.10-bad-0.10.22-1 [0,83 MB]
            farsight2-0.0.28-2 [0,21 MB]  file-5.07-3 [0,19 MB]  nspluginwrapper-1.4.2-1 [0,13 MB]
            flashplugin-10.3.181.22-1 [6,02 MB]  gcc-multilib-4.6.0-6 [17,44 MB]
            glew-1.6.0-1 [0,28 MB]  startup-notification-0.12-1 [0,02 MB]  libcups-1.4.6-3 [0,26 MB]
            gtk3-3.0.11-1 [4,66 MB]  gnome-desktop-3.0.2-1 [0,48 MB]  libwnck3-3.0.2-1 [0,34 MB]
            telepathy-glib-0.14.7-1 [1,07 MB]  gnome-panel-3.0.2-1 [1,49 MB]  gperf-3.0.4-3 [0,09 MB]
            grep-2.8-1 [0,17 MB]  libjpeg-turbo-1.1.1-1 [0,20 MB]  v4l-utils-0.8.4-1 [0,23 MB]
            jack-0.120.2-1 [0,28 MB]  gstreamer0.10-good-plugins-0.10.29-1 [0,31 MB]
            gvfs-1.8.2-1 [0,80 MB]  help2man-1.39.4-1 [0,06 MB]  iproute2-2.6.38-3 [0,36 MB]
            kbd-1.15.3-1 [0,98 MB]  initscripts-2011.06.3-1 [0,02 MB]  poppler-0.16.5-1 [0,71 MB]
            poppler-glib-0.16.5-1 [0,17 MB]  inkscape-0.48.1-3 [12,51 MB]
            inputproto-2.0.2-1 [0,04 MB]  jre-6u26-1 [20,85 MB]  kdesdk-okteta-4.6.3-2 [0,54 MB]
            kdesdk-scripts-4.6.3-2 [0,17 MB]  linux-firmware-20110512-2 [9,17 MB]
            mkinitcpio-busybox-1.18.4-1 [0,16 MB]  mkinitcpio-0.6.12-1 [0,02 MB]
            kernel26-2.6.38.8-1 [35,93 MB]  kernel26-headers-2.6.38.8-1 [4,18 MB]
            laptop-mode-tools-1.57-3 [0,05 MB]  less-443-2 [0,09 MB]
            lib32-libjpeg-turbo-1.1.1-1 [0,14 MB]  libass-0.9.12-1 [0,06 MB]
            libdvbpsi-0.2.0-1 [0,05 MB]  libftdi-0.19-1 [0,04 MB]  libgsf-1.14.21-1 [0,18 MB]
            libgssglue-0.1-4 [0,03 MB]  libwps-0.2.2-1 [0,04 MB]  neon-0.29.6-1 [0,17 MB]
            libtextcat-2.2-8 [0,29 MB]  libreoffice-3.4.0-2 [73,84 MB]
            libreoffice-ru-3.4.0-1 [7,76 MB]  libssh-0.5.0-1 [0,11 MB]
            libvncserver-0.9.8-2 [0,23 MB]  libzrtpcpp-1.4.2-5 [0,09 MB]  lvm2-2.02.85-2 [0,54 MB]
            lzo2-2.05-1 [0,07 MB]  make-3.82-3 [0,34 MB]  man-db-2.6.0.2-2 [0,38 MB]
            mercurial-1.8.4-1 [1,36 MB]  net-tools-1.60-16 [0,10 MB]  qt-4.7.3-2 [24,12 MB]
            ntrack-1:13-2 [0,03 MB]  parted-2.4-1 [0,47 MB]  perl-capture-tiny-0.11-1 [0,01 MB]
            php-5.3.6-4 [2,90 MB]  php-pear-5.3.6-4 [0,24 MB]  pixman-0.22.0-1 [0,16 MB]
            pkg-config-0.26-1 [0,03 MB]  poppler-qt-0.16.5-1 [0,11 MB]  raptor-2.0.3-1 [0,23 MB]
            skype-2.2.0.35-1 [21,56 MB]  sox-14.3.2-3 [0,49 MB]  strigi-0.7.5-1 [0,67 MB]
            sudo-1.8.1.p2-1 [0,37 MB]  telepathy-farsight-0.0.18-1 [0,04 MB]
            telepathy-qt4-0.6.1-1 [1,16 MB]  twinkle-1.4.2-10 [1,23 MB]  udisks-1.0.3-3 [0,15 MB]
            upower-0.9.11-1 [0,09 MB]  virtualbox-4.0.8-2 [16,53 MB]  vlc-1.1.10-1 [7,07 MB]
            vte-common-0.28.0-2 [0,00 MB]  vte-0.28.0-2 [0,33 MB]  vte3-0.28.0-2 [0,32 MB]
            webkit-sharp-0.3-2 [0,02 MB]  wine-1.3.21-2 [25,78 MB]  xorg-iceauth-1.0.5-1 [0,01 MB]
            xorg-server-common-1.10.2-1 [0,02 MB]  xorg-server-1.10.2-1 [1,21 MB]
            xorg-xauth-1.0.6-1 [0,02 MB]  xorg-xlsclients-1.1.2-1 [0,01 MB]  xterm-270-1 [0,22 MB]
            xulrunner-2.0.1-2 [18,57 MB]  xvidcore-1.3.2-1 [0,25 MB]  xz-5.0.3-1 [0,31 MB]

 Dimensione totale dei pacchetti da scaricare:   343,15 MB
 Dimensione totale dei pacchetti da installare:   1933,56 MB

 Vuoi procedere con l'installazione? [Y/n]

```

In questo esempio adesso sarebbe necessario scaricare solo 343,15 MB per aggiornare il sistema.

6\. Conclusioni:

In questo modo non sarà necessario scaricare 416,89 MB di dati ma 343,15 MB, ottenendo quindi quasi 100 MB in meno nel download e di conseguenza anche una riduzione del tempo di aggiornamento.

7\. Svantaggi di questo metodo:

Purtroppo questo metodo non è ampiamente supportato per ArchLinux al contrario di distriubuzioni come [OpenSuSE](http://www.opensuse.org) o [Gentoo](http://www.gentoo.org). Infatti i repostirory disponibili per gli aggiornamenti delta sono pochi. I risultati possono migliorare, se nel repositry delta sono presenti più pacchetti delta tra le versioni dei pacchetti. Nell'esempio precedente vine usato solo 1 pacchetto delta per la costruzione del nuovo pacchetto.

```
kdeartwork-kscreensaver-4.6.2-1_to_4.6.3-1-x86_64.delta	2011-May-06 22:35:41	301.8K	 application/octet-stream 
kdeartwork-kscreensaver-4.6.3-1-x86_64.pkg.tar.xz	2011-May-06 08:57:57	589.2K	 application/octet-stream

```