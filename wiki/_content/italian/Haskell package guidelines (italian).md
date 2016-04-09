**[Linee guida per la creazione di pacchetti](/index.php/Creating_Packages_(Italiano) "Creating Packages (Italiano)")**

* * *

[Eclipse](/index.php/Eclipse_Plugin_Package_Guidelines_(Italiano) "Eclipse Plugin Package Guidelines (Italiano)") – [GNOME](/index.php/Gnome_Package_Guidelines_(Italiano) "Gnome Package Guidelines (Italiano)") – [Haskell](/index.php/Haskell_Package_Guidelines_(Italiano) "Haskell Package Guidelines (Italiano)") – [Java](/index.php/Java_Package_Guidelines_(Italiano) "Java Package Guidelines (Italiano)") – [Kernel](/index.php/Kernel_Module_Package_Guidelines_(Italiano) "Kernel Module Package Guidelines (Italiano)") – [Lisp](/index.php/Lisp_Package_Guidelines_(Italiano) "Lisp Package Guidelines (Italiano)") – [MinGW](/index.php?title=MinGW_PKGBUILD_Guidelines_(Italiano)&action=edit&redlink=1 "MinGW PKGBUILD Guidelines (Italiano) (page does not exist)") – [OCaml](/index.php/OCaml_Package_Guidelines_(Italiano) "OCaml Package Guidelines (Italiano)") – [Perl](/index.php/Perl_Package_Guidelines_(Italiano) "Perl Package Guidelines (Italiano)") – [Python](/index.php/Python_Package_Guidelines_(Italiano) "Python Package Guidelines (Italiano)") – [Ruby](/index.php/Ruby_Gem_Package_Guidelines_(Italiano) "Ruby Gem Package Guidelines (Italiano)") – [VCS](/index.php/VCS_PKGBUILD_Guidelines_(Italiano) "VCS PKGBUILD Guidelines (Italiano)") – [Wine](/index.php/Wine_PKGBUILD_Guidelines_(Italiano) "Wine PKGBUILD Guidelines (Italiano)") – [Other](/index.php?title=Nonfree_Applications_Package_Guidelines_(Italiano)&action=edit&redlink=1 "Nonfree Applications Package Guidelines (Italiano) (page does not exist)")

Haskell è ben supportato su Arch Linux, poichè GHC ed altri tools fondamentali sono disponibili nei [repository ufficiali](/index.php/Official_repositories_(Italiano) "Official repositories (Italiano)"). Per chi usa Haskell in modo più pesante, la community di [ArchHaskell](/index.php/ArchHaskell "ArchHaskell") fornisce molti pacchetti provenienti da [Hackage](http://hackage.haskell.org/), in numero sempre crescente.

Si faccia riferimento alla pagina wiki di [ArchHaskell](/index.php/ArchHaskell "ArchHaskell") per eventuali contatti e per scoprire come si può essere d'aiuto.

## Contents

*   [1 Pacchetti Haskell](#Pacchetti_Haskell)
    *   [1.1 [haskell]](#.5Bhaskell.5D)
    *   [1.2 [haskell-web]](#.5Bhaskell-web.5D)
    *   [1.3 Ultima spiaggia](#Ultima_spiaggia)
*   [2 Migliorare ArchHaskell](#Migliorare_ArchHaskell)

## Pacchetti Haskell

Per utilizzare Haskell su Arch Linux, si dispone di due opzioni mutualmente esclusive:

1.  Utilizzare i pacchetti dei repository ufficiali di Arch Linux, che però sono solamente una piccola parte di tutti i pacchetti Haskell disponibili, anche se ben mantenuti. Li si installi come si farebbe con qualsiasi altro pacchetto. Esempi sui pacchetti disponibili nei repository [extra](https://www.archlinux.org/packages/?arch=x86_64&repo=Extra&q=haskell&last_update=&limit=50) e [community](https://www.archlinux.org/packages/?arch=x86_64&repo=Community&q=haskell&last_update=&limit=50), che dovrebbero soddisfare chi vuole semplicemente utilizzare la piattaforma Haskell. È inoltre possibile integrare questi pacchetti con quelli non ufficiali presenti su AUR.
2.  Utilizzare i repository non ufficiali del progetto ArchHaskell, che offrono una maggiore varietà di pacchetti tra quelli disponibili su Hackage. Dal momento che questo progetto è mantenuto dalla comunità, abbiamo spesso bisogno di volontari che ci aiutino a mantenere ed aggiungere altri pacchetti a questi repository. Si continui la lettura per ulteriori informazioni sul loro utilizzo.

### [haskell]

Il repository [haskell] costituisce il contenitore principale dei pacchetti mantenuti dal team di ArchHaskell ed è possibile utilizzarlo aggiungendo la seguente riga a `/etc/pacman.conf` (sopra [extra]):

```
[haskell]
Server = [http://xsounds.org/~haskell/$arch](http://xsounds.org/~haskell/$arch)

```

Questo gruppo di pacchetti deriva dal tree di **habs**, accessibile [qui](https://github.com/archhaskell/habs). Viene utilizzato un tool chiamato [cblrepo](https://github.com/magthe/cblrepo) per sincronizzare il tree di **habs** con i pacchetti Haskell ufficiali provenienti da [Hackage](http://hackage.haskell.org/packages/hackage.html)

Inserire [haskell] sopra [extra] consentirà ai pacchetti del repository [haskell] di avere la precedenza, in caso di duplicati.

### [haskell-web]

Il repository [haskell-web] si basa su [haskell] e fornisce numerosi pacchetti aggiuntivi, adatti alle web applications.

```
[haskell-web]
Server = [http://archhaskell.mynerdside.com/$repo/$arch](http://archhaskell.mynerdside.com/$repo/$arch)

```

Lo si aggiunga dopo [haskell].

### Ultima spiaggia

*   [pacchetti Haskell su AUR](https://aur.archlinux.org/packages.php?O=0&K=haskell-)
*   utilizzare `cabal-install` direttamente

Sfortunatamente, molti dei pacchetti presenti su AUR non sono aggiornati a causa della mancanza di manodopera. Se si ha del tempo libero, è consigliabile utilizzare `cblrepo` per creare un repository sulla falsariga di [haskell-web], che potrà poi essere aggiunto alla collezione dei repository esistenti.

## Migliorare ArchHaskell

Si legga la pagina wiki di [ArchHaskell](/index.php/ArchHaskell "ArchHaskell") e ci si metta in contatto con la community attraverso le mailing lists o il canale IRC. Stiamo lavorando alla documentazione e allo sviluppo di un workflow per consentire la creazione di repository stile [haskell-web] e mantenerli in modo distribuito, facendo sì che tutti i pacchetti in essi contenuti vengano esposti all'utenza attraverso un unico repository.