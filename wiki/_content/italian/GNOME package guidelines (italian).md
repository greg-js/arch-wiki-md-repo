**[Linee guida per la creazione di pacchetti](/index.php/Creating_Packages_(Italiano) "Creating Packages (Italiano)")**

* * *

[Eclipse](/index.php/Eclipse_Plugin_Package_Guidelines_(Italiano) "Eclipse Plugin Package Guidelines (Italiano)") – [GNOME](/index.php/Gnome_Package_Guidelines_(Italiano) "Gnome Package Guidelines (Italiano)") – [Haskell](/index.php/Haskell_Package_Guidelines_(Italiano) "Haskell Package Guidelines (Italiano)") – [Java](/index.php/Java_Package_Guidelines_(Italiano) "Java Package Guidelines (Italiano)") – [Kernel](/index.php/Kernel_Module_Package_Guidelines_(Italiano) "Kernel Module Package Guidelines (Italiano)") – [Lisp](/index.php/Lisp_Package_Guidelines_(Italiano) "Lisp Package Guidelines (Italiano)") – [MinGW](/index.php?title=MinGW_PKGBUILD_Guidelines_(Italiano)&action=edit&redlink=1 "MinGW PKGBUILD Guidelines (Italiano) (page does not exist)") – [OCaml](/index.php/OCaml_Package_Guidelines_(Italiano) "OCaml Package Guidelines (Italiano)") – [Perl](/index.php/Perl_Package_Guidelines_(Italiano) "Perl Package Guidelines (Italiano)") – [Python](/index.php/Python_Package_Guidelines_(Italiano) "Python Package Guidelines (Italiano)") – [Ruby](/index.php/Ruby_Gem_Package_Guidelines_(Italiano) "Ruby Gem Package Guidelines (Italiano)") – [VCS](/index.php/VCS_PKGBUILD_Guidelines_(Italiano) "VCS PKGBUILD Guidelines (Italiano)") – [Wine](/index.php/Wine_PKGBUILD_Guidelines_(Italiano) "Wine PKGBUILD Guidelines (Italiano)") – [Other](/index.php?title=Nonfree_Applications_Package_Guidelines_(Italiano)&action=edit&redlink=1 "Nonfree Applications Package Guidelines (Italiano) (page does not exist)")

I pacchetti GNOME di Archlinux seguono un determinato schema.

## Contents

*   [1 Profilo di inizializzazione di GNOME](#Profilo_di_inizializzazione_di_GNOME)
*   [2 Schemi GConf](#Schemi_GConf)
*   [3 Schemi GSettings](#Schemi_GSettings)
*   [4 Scrollkeeper e la documentazione](#Scrollkeeper_e_la_documentazione)
*   [5 File .desktop](#File_.desktop)
*   [6 Cache delle icone GTK](#Cache_delle_icone_GTK)
*   [7 File .install](#File_.install)
*   [8 Esempio](#Esempio)

## Profilo di inizializzazione di GNOME

Non c'è più alcun profilo di inizializzazione. La vecchia riga dovrebbe essere eliminata da ogni PKGBUILD:

```
[ -z "$GNOMEDIR" ] && . /etc/profile.d/gnome.sh

```

## Schemi GConf

Molti pacchetti GNOME installano schemi Gconf. Questi schemi vengono installati nel database del sistema GConf, che andrebbe evitato. Alcuni pacchetti mettono a disposizione l'opzione `--disable-schemas-install` per il `./configure`, che spesso non funziona. Per questo motivo gconftool-2, possiede una variabile chiamata `GCONF_DISABLE_MAKEFILE_SCHEMA_INSTALL`, se questa viene impostata, gconftool-2 non aggiornerà alcun database. Nel creare pacchetti che installano file schema, utilizzare

```
make GCONF_DISABLE_MAKEFILE_SCHEMA_INSTALL=1 DESTDIR=${pkgdir} install

```

nello stage di installazione del pacchetto.

È necessario installare e rimuovere gli schemi GConf nel file .install, utilizzando pre_remove(), pre_upgrade(), post_upgrade() e post_install(). Utilizzare gconf-merge-schemas per unire diversi schemi in unico file specifico per uno pacchetto, installarli o disinstallarli tramite `usr/sbin/gconfpkg --(un)install $pkgname`. L'utilizzo di gconfpkg richieda la dipendenza gconf>=2.18.0.1-4 (or gconfmm>=2.20.0).

## Schemi GSettings

Gli schemi Gconf verranno rimpiazzati dagli schemi Gsettings in un futuro molto prossimo, anche se alcune applicazioni li usano già (ad es. Empathy). Il sistema GSettings utilizza dconf come backend, perciò ogni pacchetto che contiene schemi GSettings deve avere dconf come dipendenza. Quando viene installato un nuovo schema GSettings sul sistema, il database GSettings deve essere rigenerato, ciò non deve accadere invece durante la fase di pacchettizzazione. Per evitare che avvenga la rigenerazione del database GSettings durante la pacchettizzazione, utilizzare lo switch `--disable-schemas-compile` sul ./configure. Per ricompilarlo al momento dell'installazione, aggiungere le righe seguenti al file `.install` nel blocco post_install, post_upgrade e post_remove: `glib-compile-schemas usr/share/glib-2.0/schemas`

## Scrollkeeper e la documentazione

A partire da GNOME 2.20 non vi è più la necessità di utilizzare Scrollkeeper, in quanto Rarian legge direttamente i file OMF. Scrollkeeper-update è quindi un'abitudine superata, ormai. L'unico requisito è la soddisfazione della dipendenza di compilazione gnome-doc-utils>=0.11.2.

## File .desktop

Molti pacchetti installano file .dektop compatibili con le specifiche di Freedesktop.org, e registrano chiavi MimeType al loro interno. L'esecuzione di `update-desktop-database -q` all'interno del post_install() e del post_remove() è raccomandata (il pacchetto dovrebbe dipendere da desktop-file-utils in questo caso)

## Cache delle icone GTK

Alcuni pacchetti installano le proprie icone all'interno del tema hicolor. Questi pacchetti dovrebbero dipendere da hicolor-icon-theme e dovrebbero eseguire `gtk-update-icon-cache -q -t -f usr/share/icons/hicolor` nelle funzioni post_install(), post_upgrade() e post_remove().

## File .install

Per molti pacchetti GNOME, i file .install sono esattamente identici. Il pacchetto gedit contiene un file .install molto generico. [https://projects.archlinux.org/svntogit/packages.git/tree/gedit/repos/extra-i686/gedit.install](https://projects.archlinux.org/svntogit/packages.git/tree/gedit/repos/extra-i686/gedit.install)

Fondamentalmente, l'unica cosa che deve essere modificata è la variabile pkgname in cima al file .install. Visto che pacman non fornisce il nome del pacchetto come variabile, dovremo fornirlo noi nel file .install. Nel caso il pacchetto non contenesse schemi GConf, icone per il tema hicolor, o file .desktop, si possono tranquillamente rimuovere le parti che gestiscono questi ultimi.

## Esempio

Per un esempio delle regole citate, consultare il PKGBUILD del pacchetto gedit con relativo file .install fornito al seguente indirizzo: [https://projects.archlinux.org/svntogit/packages.git/tree/gedit/repos/extra-i686/](https://projects.archlinux.org/svntogit/packages.git/tree/gedit/repos/extra-i686/)