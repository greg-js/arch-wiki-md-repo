# Eclipse plugin package guidelines (Italiano)

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

**[Linee guida per la creazione di pacchetti](/index.php/Creating_Packages_(Italiano) "Creating Packages (Italiano)")**

* * *

[Eclipse](/index.php/Eclipse_Plugin_Package_Guidelines_(Italiano) "Eclipse Plugin Package Guidelines (Italiano)") – [GNOME](/index.php/Gnome_Package_Guidelines_(Italiano) "Gnome Package Guidelines (Italiano)") – [Haskell](/index.php/Haskell_Package_Guidelines_(Italiano) "Haskell Package Guidelines (Italiano)") – [Java](/index.php/Java_Package_Guidelines_(Italiano) "Java Package Guidelines (Italiano)") – [Kernel](/index.php/Kernel_Module_Package_Guidelines_(Italiano) "Kernel Module Package Guidelines (Italiano)") – [Lisp](/index.php/Lisp_Package_Guidelines_(Italiano) "Lisp Package Guidelines (Italiano)") – [MinGW](/index.php?title=MinGW_PKGBUILD_Guidelines_(Italiano)&action=edit&redlink=1 "MinGW PKGBUILD Guidelines (Italiano) (page does not exist)") – [OCaml](/index.php/OCaml_Package_Guidelines_(Italiano) "OCaml Package Guidelines (Italiano)") – [Perl](/index.php/Perl_Package_Guidelines_(Italiano) "Perl Package Guidelines (Italiano)") – [Python](/index.php/Python_Package_Guidelines_(Italiano) "Python Package Guidelines (Italiano)") – [Ruby](/index.php/Ruby_Gem_Package_Guidelines_(Italiano) "Ruby Gem Package Guidelines (Italiano)") – [VCS](/index.php/VCS_PKGBUILD_Guidelines_(Italiano) "VCS PKGBUILD Guidelines (Italiano)") – [Wine](/index.php/Wine_PKGBUILD_Guidelines_(Italiano) "Wine PKGBUILD Guidelines (Italiano)") – [Other](/index.php?title=Nonfree_Applications_Package_Guidelines_(Italiano)&action=edit&redlink=1 "Nonfree Applications Package Guidelines (Italiano) (page does not exist)")

Ci sono numerosi modi per installare un plugin funzionante di [Eclipse](/index.php/Eclipse_(Italiano) "Eclipse (Italiano)"), sopratutto da quando è stata introdotta la cartella "dropins" in Eclipse 3.4, tuttavia alcune di queste maniere risultano disordinate, e avere un forma di pacchettizzazione standardizzata e coerente è molto importante per ottenere una struttura di sistema pulita. Non è facile però ottenere questo risultato senza la consapevolezza di come funzionino i plugin di Eclipse. Questa pagina ha lo scopo di definire una struttura standard semplice per i [PKGBUILD](/index.php/PKGBUILD_(Italiano) "PKGBUILD (Italiano)") dei plugin di Eclipse, cosicché la struttura del filesystem possa rimanere coerente tra i plugin senza che il manutentore dei pacchetti debba fare tutto daccapo per ogni nuovo pacchetto.

## Contents

*   [1 Struttura ed installazione dei plugin di Eclipse](#Struttura_ed_installazione_dei_plugin_di_Eclipse)
*   [2 Pacchettizzazione](#Pacchettizzazione)
    *   [2.1 Esempio di PKGBUILD](#Esempio_di_PKGBUILD)
    *   [2.2 Come personalizzare il pacchetto](#Come_personalizzare_il_pacchetto)
    *   [2.3 Analisi approfondita del PKGBUILD](#Analisi_approfondita_del_PKGBUILD)
        *   [2.3.1 Nome del pacchetto](#Nome_del_pacchetto)
        *   [2.3.2 File](#File)
            *   [2.3.2.1 Estrazione](#Estrazione)
            *   [2.3.2.2 Posizione](#Posizione)
        *   [2.3.3 La funzione build()](#La_funzione_build.28.29)

## Struttura ed installazione dei plugin di Eclipse

Il tipico plugin di Eclipse contiene due cartelle, `features` e `plugins`, e a partire da Eclipse 3.3 potevano essere posizionate solamente in `/usr/share/eclipse/`. Il contenuto di queste due cartelle poteva essere mescolato con quello degli altri plugin, e ciò creava confusione, rendendo la struttura di difficile amministrazione. Era inoltre molto difficile capire a colpo d'occhio a quale pacchetto appartenesse ciascun file.

Questo metodo di installazione è ancora supportato in Eclipse 3.4, ma quello preferibile ora è quello che usa la cartella `/usr/share/eclipse/dropins/`. All'interno di questa cartella possono trovarsi un numero indefinito di sottocartelle, ognuna delle quali contenente le proprie sottocartelle `features` e `plugins`. Ciò permette di mantenere una struttura ordinata e pulita, e dovrebbe essere la maniera standard di pacchettizzazione.

## Pacchettizzazione

### Esempio di PKGBUILD

Qui c'è un esempio, discuteremo più avanti su come personalizzarlo.

 `PKGBUILD-eclipse.proto` 

```
pkgname=eclipse-mylyn
pkgver=3.0.3
pkgrel=1
pkgdesc="A task-focused interface for Eclipse"
arch=('i686' 'x86_64')
url="http://www.eclipse.org/mylyn/"
license=('EPL')
depends=('eclipse')
optdepends=('bugzilla: ticketing support')
source=(http://download.eclipse.org/tools/mylyn/update/mylyn-${pkgver}-e3.4.zip)
md5sums=('e98cd7ab3c5d5aeb7c32845844f85c22')

build() {
  _dest=${pkgdir}/usr/share/eclipse/dropins/${pkgname/eclipse-}/eclipse

  cd ${srcdir}

  # Features
  find features -type f | while read _feature ; do
    if [[ ${_feature} =~ (.*\.jar$) ]] ; then
      install -dm755 ${_dest}/${_feature%*.jar}
      cd ${_dest}/${_feature/.jar}
      jar xf ${srcdir}/${_feature} || return 1
    else
      install -Dm644 ${_feature} ${_dest}/${_feature}
    fi
  done

  # Plugins
  find plugins -type f | while read _plugin ; do
    install -Dm644 ${_plugin} ${_dest}/${_plugin}
  done
}

```

### Come personalizzare il pacchetto

La variabile principale che dev'essere personalizzata è `pkgname`. Se si sta pacchettizzando un plugin standard, allora questa è l'unica cosa da fare: la maggior parte dei plugin viene distribuita in file zip che contengono solamente le due sottocartelle `features` e `plugins`. Perciò, se si sta pacchettizzando il plugin `foo` e il file sorgente contiene solamente `features` e `plugins`, allora occorre cambiare solamente `pkgname` in `eclipse-foo` e si è a posto.

Si legga avanti per le istruzioni sulla parte interna del PKGBUILD, che aiutano a capire come impostarlo per tutte le altre situazioni.

### Analisi approfondita del PKGBUILD

#### Nome del pacchetto

I pacchetti dovrebbero sempre chiamarsi `eclipse-_nomedelplugin_`, così da renderli riconoscibili come pacchetti relativi a Eclipse e rendere facile il riconoscimento del nome del plugin con una semplice sostituzione tramite shell come `${pkgname/eclipse-}`, senza dover ricorrere ad una variabile `${_nomereale}` non necessaria. Il nome del plugin è necessario per ordinare ogni cosa durante l'installazione ed evitare conflitti.

#### File

##### Estrazione

Per alcuni plugin è necessario estrarre le features da file jar. L'utility `jar`, già inclusa in JRE, serve a tale scopo. Però, `jar` non non è in grado di estrarre in una cartella diversa da quella corrente: ciò significa che, dopo avere creato ogni cartella, è necessario spostarsi al suo interno con `cd` prima di effettuare l'estrazione. La variabile `${_dest}` è usata in questo contesto per aumentare la leggibilità e l'ordine del PKGBUILD.

##### Posizione

Come abbiamo detto, gli archivi sorgenti forniscono due cartelle, `features` e `plugins`, ognuna delle quali contenente file jar. La struttura preferibile di dropins dovrebbe apparire così:

```
/usr/share/eclipse/dropins/pluginname/eclipse/features/feature1/...
/usr/share/eclipse/dropins/pluginname/eclipse/features/feature2/...
/usr/share/eclipse/dropins/pluginname/eclipse/plugins/plugin1.jar
/usr/share/eclipse/dropins/pluginname/eclipse/plugins/plugin2.jar

```

Questa struttura permette di mescolare diverse versioni di librerie che potrebbero essere necessarie a plugin differenti mantenendo chiara la struttura di appartenenza dei pacchetti. Permette anche di evitare conflitti nel caso in cui diversi pacchetti forniscano le stesse librerie. L'unica alternativa sarebbe quella di dividere ogni pacchetto dalle proprie librerie, con tutta la confusione che ne deriverebbe, e non sarebbe nemmeno assicurato il funzionamento a causa di pacchetti che hanno bisogno di vecchie versioni di librerie. La cartella `features` dev'essere estratta altrimenti Eclipse non sarà in grado di vederla, e l'intera installazione del plugin non funzionerà. Ciò accade perché Eclipse tratta le installazioni dai siti di aggiornamento e quelle locali in maniera differente (per ragioni non trattate in questo articolo).

#### La funzione build()

La prima cosa da notare è il comando `cd ${srcdir}`. Solitamente gli archivi sorgente estraggono le cartelle `features` e `plugins` direttamente sotto `${srcdir}`, ma questo non è sempre vero. Ad ogni modo, per la maggior parte dei plugin non-_(de facto)_-standard questa è l'unica linea che dev'essere cambiata. La prossima è la sezione `features`. Essa crea le cartelle necessarie, una per ogni file jar, ed estrae il file nella cartella corrispondente. Alla stessa maniera, la sezione `plugins` installa i file jar nelle relative cartelle. Un ciclo while viene nel frattempo usato per evitare strani nomi di file.

Retrieved from "[https://wiki.archlinux.org/index.php?title=Eclipse_plugin_package_guidelines_(Italiano)&oldid=415134](https://wiki.archlinux.org/index.php?title=Eclipse_plugin_package_guidelines_(Italiano)&oldid=415134)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [Package development (Italiano)](/index.php/Category:Package_development_(Italiano) "Category:Package development (Italiano)")