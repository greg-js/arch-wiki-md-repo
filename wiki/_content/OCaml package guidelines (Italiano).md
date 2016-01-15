# OCaml package guidelines (Italiano)

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

## Contents

*   [1 Nominazione dei pacchetti](#Nominazione_dei_pacchetti)
*   [2 Ubicazione delle librerie OCaml](#Ubicazione_delle_librerie_OCaml)
*   [3 OASIS](#OASIS)
*   [4 Bytecode e Livelli di OCaml](#Bytecode_e_Livelli_di_OCaml)
*   [5 Esempio di PKGBUILD OCaml](#Esempio_di_PKGBUILD_OCaml)

## Nominazione dei pacchetti

Per le librerie, si usi `ocaml-modulename`. Per le applicazioni, si usi il nome del programma. In entrambi i casi, il nome del pacchetto dev'essere interamente in caratteri minuscoli.

## Ubicazione delle librerie OCaml

Le librerie OCaml devono essere installate sotto `/usr/lib/ocaml`. Precedentemente, le librerie venivano installate sia sotto `/usr/lib/ocaml` che sotto `/usr/lib/ocaml/site-lib`, a seconda del pacchetto. Questa confusione impediva ad alcuni pacchetti di funzionare con altri, ed inoltre frammentava lo sviluppo in OCaml su Arch Linux. Per questo l'uso di `/usr/lib/ocaml/site-lib` è stato interrotto.

Le librerie OCaml devono essere installate utilizzando [ocaml-findlib](https://www.archlinux.org/packages/?name=ocaml-findlib). `ocaml-findlib` include dei metadata nel pacchetto che facilitano la gestione delle librerie. È uno standard de-facto ed un requisito di gran parte dell'attuale software in OCaml.

`ocaml-findlib` estrae i dati necessari da un file chiamato `META` che deve essere incluso nell'archivio dei sorgenti. Se questo file non è incluso, è possibile ottenerne uno dal corrispondente pacchetto per Debian, Ubuntu o Fedora, altrimenti deve esserne creato uno apposito dal maintainer del pacchetto. La richiesta di includere tale file potrebbe anche essere fatta direttamente agli sviluppatori originali del pacchetto.

Quando si installano pacchetti con `ocaml-findlib` è necessario usare la variabile `OCAMLFIND_DESTDIR`. Vedere il PKGBUILD di esempio riportato sotto per i dettagli.

## OASIS

I pacchetti OCaml che installano eseguibili usando OASIS ignorano `DESTDIR`. Questa è una limitazione conosciuta di OASIS ([issue #852](https://forge.ocamlcore.org/tracker/?func=detail&atid=294&aid=852&group_id=54)). Una maniera per abilitare funzionalità simili a `DESTDIR` è lanciare lo script `configure` con l'argomento --destdir, ad esempio:

```
build() {
    cd "${srcdir}/${srcname}-${pkgver}"
    ./configure --prefix /usr --destdir "$pkgdir"

    # build commands
}
```

## Bytecode e Livelli di OCaml

OCaml può eseguire il codice su vari "livelli": il livello principale ("top level") interpreta il codice OCaml senza compilarlo, il livello bytecode crea appunto del bytecode indipendente dalla macchina, e il livello nativo crea dei binari con codice macchina (proprio come C/C++).

Quando si compilano pacchetti OCaml è necessario sapere se il processo di build compila codice macchina nativo, bytecode, o, come in molti casi, entrambi. Questo genera svariate situazioni in cui possono crearsi problemi con le opzioni dei pacchetti e le loro corrette dipendenze.

Se viene creato del bytecode, il PKGBUILD deve contenere la seguente linea per proteggerlo:

```
options=('!strip')

```

Se il pacchetto non contiene bytecode ma distribuisce solamente file binari, `ocaml` non è richiesto come dipendenza, ma è invece ovviamente necessario come makedepends, dato che il compilatore di OCaml è fornito dal pacchetto `ocaml`. Se il pacchetto contiene sia codice nativo che bytecode, `ocaml` deve essere sia una dipendenza che un makedepends.

Il codice OCaml è molto raramente distribuito solo come bytecode, infatti quasi sempre include del codice nativo: l'unico caso in cui è consigliabile usare _any_ come _arch_ è quando viene distribuito solamente codice sorgente non compilato, di solito con una libreria, benché appunto molte librerie distribuiscano anche codice nativo.

Per riassumere, è bene essere sempre coscienti di ciò che si va a distribuire, la probabilità maggiore è che il proprio pacchetto contenga sia codice macchina nativo che bytecode.

## Esempio di PKGBUILD OCaml

```
# Contributor: Your Name <youremail@domain.com>

pkgname=ocaml-<package name>
pkgver=4.2
pkgrel=1
license=('')
arch=('i686' 'x86_64')
pkgdesc="An OCaml Package"
url=""
depends=('ocaml')
makedepends=('ocaml-findlib')
source=()
options=('!strip')
md5sums=()

OCAMLFIND_DESTDIR="${pkgdir}$(ocamlfind printconf destdir)"

build() {
  cd "${srcdir}/${pkgname}-${pkgver}"
  mkdir -p "$OCAMLFIND_DESTDIR"
  ./configure --prefix=/usr
  make
}

package() {
  cd "${srcdir}/${pkgname}-${pkgver}"
  env DESTDIR="${pkgdir}" \
    OCAMLFIND_DESTDIR="$OCAMLFIND_DESTDIR" \
    make install
}

```

Tenere sempre presente che molti pacchetti OCaml avranno spesso bisogno che siano passati ulteriori parametri a make e make install. Ricordarsi anche di rimuovere l'opzione _'!strip'_ e cambiare l'architettura se il pacchetto non fornisce bytecode.

Retrieved from "[https://wiki.archlinux.org/index.php?title=OCaml_package_guidelines_(Italiano)&oldid=415139](https://wiki.archlinux.org/index.php?title=OCaml_package_guidelines_(Italiano)&oldid=415139)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [Package development (Italiano)](/index.php/Category:Package_development_(Italiano) "Category:Package development (Italiano)")