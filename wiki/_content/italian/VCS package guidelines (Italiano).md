**[Linee guida per la creazione di pacchetti](/index.php/Creating_Packages_(Italiano) "Creating Packages (Italiano)")**

* * *

[Eclipse](/index.php/Eclipse_Plugin_Package_Guidelines_(Italiano) "Eclipse Plugin Package Guidelines (Italiano)") – [GNOME](/index.php/Gnome_Package_Guidelines_(Italiano) "Gnome Package Guidelines (Italiano)") – [Haskell](/index.php/Haskell_Package_Guidelines_(Italiano) "Haskell Package Guidelines (Italiano)") – [Java](/index.php/Java_Package_Guidelines_(Italiano) "Java Package Guidelines (Italiano)") – [Kernel](/index.php/Kernel_Module_Package_Guidelines_(Italiano) "Kernel Module Package Guidelines (Italiano)") – [Lisp](/index.php/Lisp_Package_Guidelines_(Italiano) "Lisp Package Guidelines (Italiano)") – [MinGW](/index.php?title=MinGW_PKGBUILD_Guidelines_(Italiano)&action=edit&redlink=1 "MinGW PKGBUILD Guidelines (Italiano) (page does not exist)") – [OCaml](/index.php/OCaml_Package_Guidelines_(Italiano) "OCaml Package Guidelines (Italiano)") – [Perl](/index.php/Perl_Package_Guidelines_(Italiano) "Perl Package Guidelines (Italiano)") – [Python](/index.php/Python_Package_Guidelines_(Italiano) "Python Package Guidelines (Italiano)") – [Ruby](/index.php/Ruby_Gem_Package_Guidelines_(Italiano) "Ruby Gem Package Guidelines (Italiano)") – [VCS](/index.php/VCS_PKGBUILD_Guidelines_(Italiano) "VCS PKGBUILD Guidelines (Italiano)") – [Wine](/index.php/Wine_PKGBUILD_Guidelines_(Italiano) "Wine PKGBUILD Guidelines (Italiano)") – [Other](/index.php?title=Nonfree_Applications_Package_Guidelines_(Italiano)&action=edit&redlink=1 "Nonfree Applications Package Guidelines (Italiano) (page does not exist)")

I sistemi di controllo di versioni possono essere usati per il recupero sia delle versioni dei pacchetti ufficialmente rilasciati, sia per quelle in sviluppo (trunk). Quest'articolo copre entrambi i casi.

## Prototipi

Il pacchetto [abs](https://www.archlinux.org/packages/?name=abs) fornisce prototipi per PKGBUILDs relativi a software prelevabile da repository svn, git, mercurial, e darcs. Una volta installato il pacchetto abs, è possibile reperirli all'interno della directory `/usr/share/pacman`. Oppure navigare la directory [prototypes](https://projects.archlinux.org/abs.git/tree/prototypes) nel repository Git di [ABS](/index.php/ABS "ABS")

## Linee guida

*   Apporre il suffisso appropriato al `pkgname` scegliendo tra `-cvs`, `-svn`, `-hg`, `-darcs`, `-bzr` or `-git`. Se il pacchetto fa riferimento ad un ramo in sviluppo, dovrebbe essergli aggiunto un suffisso. Se il pacchetto scarica i sorgenti da un tag VCS, non si dovrebbe aggiungere nulla. Utilizzare questa regola comportamentale: se la riuscita del pacchetto dipende dalla data di compilazione, aggiungere un suffisso; altrimenti non farlo.

*   Un pacchetto VCS può essere aggiornato nel momento in cui si renda necessaria una modifica al sistema di compilazione, incluse correzioni di dipendenze, URL, indirizzi sorgente, etc. Se il numero di revisione rimane lo stesso dopo un aggiornamento di questo ripo, ma viene generato un binario differente, l'incremento manuale della variabile `pkgrel` è obbligatorio. Se sia il numero di revisione che il binario rimangono inalterati, `pkgrel` può essere lasciato invariato. Non è necessario aggiornare un pacchetto VCS per ogni commit che raggiunge il repo di revision control, ma si potrebbe anche farlo.

*   Quando [makepkg](/index.php/Makepkg "Makepkg") viene eseguito, di default controllerà la presenza di nuove revisioni ed aggiornerà il valore di `pkgver` all'interno del PKGBUILD. Consultare `--holdver` in [man makepkg](https://www.archlinux.org/pacman/makepkg.8.html) se si vuole imporre un comportamento differente. `--holdver` funziona solo per repository CVS ed SVN, che consentono l'utilizzo di sorgenti di revisioni precedenti.

*   Verificare i conflitti del pacchetto. Per esempio _fluxbox-svn_ andrà in conflitto con _fluxbox_. In questo caso sarà necessario utilizzare `conflicts=('fluxbox')`.

*   Utilizzare il campo `provides` in modo che le dipendenze dei pacchetti che richiedono la presenza della versione non-CVS del pacchetto da generare risultino soddisfatte (`provides=('fluxbox')`).

*   Bisognerebbe cercare di evitare, ove possibile, l'utilizzo di `replaces=...`, in quanto genera facilmente problemi che sarebbe meglio evitare.

*   Quando si definisce la root CVS, utilizzare `anonymous:@` piuttosto che `anonymous@` per evitare la richiesta di password e l'obbligo di inserire una password vuota, _O_ utilizzare `anonymous:password@` nel caso una password sia necessaria.

*   Nonostante non sarebbe necessario utilizzare il campo `pkgrel` quando si compila da repo CVS/SVN/GIT (in quanto i cambiamenti ai sorgenti sono frequenti, e saranno automaticamente notificati nel campo `pkgver`), makepkg lo richiede obbligatoriamente.

*   Non dimenticare di includere il tool VCS appropriato (cvs, subversion, git, ...) all'interno dell'array `makedepends=...`.

*   Per preservare l'integrità del codice originale scaricato, prendere in considerazione di copiare la directory di compilazione, se si presenta la necessità di effettuare modifiche al sorgente. Ad esempio, considerando di aver effettuato il check out dal repo in `src/$_cvsmod` da `$startdir`, ci si può comportare in questo modo

```
mkdir src/$_cvsmod-build

cd src/$_cvsmod-build
../$_cvsmod/configure

```

o:

```
cp -r src/$_cvsmod src/$_cvsmod-build
cd src/$_cvsmod-build

```

*   Con l'introduzione di [AUR](/index.php/AUR "AUR"), è importante evitare l'esecuzione degli apici inversi per la creazione di variabili del pacchetto. Makepkg aggiornerà automaticamente il campo `pkgver` in ogni caso durante la compilazione del pacchetto ( a meno che non venga utilizzato `--holdver`)

## Suggerimenti

*   Bisognerebbe accertarsi che non vengano lasciate directory proprie del VCS all'interno del pacchetto. Nel caso risultassero presenti, si potrebbe modificare la sezione package() del PKGBUILD aggiungendole in fondo una riga simile a questa per rimuoverle.

 `rm -rf `find "$pkgdir" -type d -name ".svn"`` 

*   Utilizzando GIT, è possibile velocizzare le operazioni di clonazione tramite il parametro `--depth=1`. In questo modo viene effettuata una copia superficiale, che contiene solo l'ultima parte della cronologia dei cambiamenti - dato che la precedente è solitamente inutili ai fini della compilazione.

 ` git clone [git://hostname.dom/project.git](git://hostname.dom/project.git) --depth=1` 

*   È possibile creare il pacchetto anche da un branch diverso dal master. Per farlo basta aggiungere un `--branch nome_branch` dopo il primo `git clone`, in questo modo:

 ` git clone "$_gitroot" "$_gitname" --branch nome_branch` 

Ricordarsi di rinominare il pacchetto in `pacchetto-branch-git` per evitare confusione con l'eventuale pacchetto dal branch master.

*   Porzione di codice da copia/incollare per la compilazione da repo VCS:

Per i pigri, è mostrato un semplice script di compilazione da repo GIT

```
cd "$srcdir"
 msg "Connecting to GIT server...."
 if [ -d $_gitname ] ; then
   cd $_gitname && git pull origin
   msg "The local files are updated."
 else
   git clone --depth=1 $_gitroot $_gitname
 fi
 msg "GIT checkout done or server timeout"

```

*   Directory temporanee di compilazione: Utilizzando GIT, ed avendo la necessità di creare una directory di compilazione separata, bisognerebbe evitare di copiare la directory `.git` all'interno della directory principale, visto che questa contiene informazioni sullo storico che GIT utilizza internamente. Nei repo con migliaia di commit, questa directory `.git` può contenere anche centinaia di MiB di unitile storico dei commit che non hanno nulla a che vedere con l'attuale albero di lavoro. L'unico caso in cui si potrebbe aver bisogno di copiare anche la directory `.git`, è quando si dovesse compilare uno specifico vecchio commit (eventualità molto remota, visto che lo scopo di un pacchetto VCS è proprio quello di fornire l'ultimo codice disponibile). Quindi, invece di

```
 rm -rf "$srcdir/$_gitname-build"
cp -R "$srcdir/$_gitname" "$srcdir/$_gitname-build" # copia tutto, inclusa l'inutile directory .git
cd "$srcdir/$_gitname-build"
make # build/compile from source

```

si dovrebbe utilizzare

```
 rm -rf "$srcdir/$_gitname-build"
cd "$srcdir/$_gitname" && ls -A 
```

per abbattere il tempo di compilazione e lo spazio utilizzato.