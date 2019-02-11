<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Nomenclatura del pacchetto](#Nomenclatura_del_pacchetto)
    *   [1.1 Versionamento dei pacchetti](#Versionamento_dei_pacchetti)
*   [2 Esempi](#Esempi)
*   [3 Esempio PKGBUILD](#Esempio_PKGBUILD)
*   [4 Note](#Note)
    *   [4.1 Quarry](#Quarry)
*   [5 Automazione](#Automazione)

## Nomenclatura del pacchetto

Per le librerie, utilizzare `ruby-$gemname`. Per le applicazioni, utilizzare il nome del programma. In entrambi i casi il nome dovrebbe essere tutto in minuscolo. Usare sempre il prefisso `ruby-` anche se `$gemname` inizia già con `ruby`. È necessario per evitare ambiguità sui nomi nel caso ci sia un gem con un nome più corto. Rende anche i nomi più facilmente analizzabili dai tool.

### Versionamento dei pacchetti

Se si vuole aggiungere un pacchetto con versionamento va usato `ruby-$gemname-$version`, ad esempio `ruby-builder-3.2.1`. Così la dipendenza rubygem `builder=3.2.1` diventerà `ruby-builder-3.2.1` che è un pacchetto Arch.

Se va risolta una dipendenza "approssimativamente più grande" `~>` allora il pacchetto deve usare la versione senza l'ultima parte, ad esempio la dipendenza rubygem `builder~>3.2.1` diventerà `ruby-builder-3.2`. Un'eccezione a questa regola va applicata quando la dipendenza "approssimativamente più grande" è uguale all'ultima versione del gem - in questo caso evitare di introdurre un nuovo pacchetto versionato e usare solo `ruby-$gemname` .

Un altro problema con il versionamento dei pacchetti si ha quando ci sono conflitti con altre versioni, ad esempio perché i pacchetti installano gli stessi file in `/usr/bin`. Una soluzione per questo problema è quella di non fare installare questi file dai pacchetti versionati - solo la versione HEAD dei pacchetti può fare questo.

## Esempi

Ad esempio, si vedano [github-gem](https://aur.archlinux.org/packages.php?ID=24484) [ruby-json_pure](https://aur.archlinux.org/packages/ruby-json_pure/) [ruby-hpricot](https://www.archlinux.org/packages/?name=ruby-hpricot)

## Esempio PKGBUILD

```
 # Contributor: YourName <YourEmail AT example DOT com>
 pkgname=ruby-GEMNAME # All lowercase
 pkgver=GEMVERSION
 pkgrel=1
 pkgdesc="Ruby gem FooBar which implements BazQuux"
 arch=(any)
 url=""
 license=()
 depends=(ruby) # Gem may depend on other gems as well (you can get dependency information from the yaml specification)
 makedepends=(rubygems)
 source=([http://rubygems.org/downloads/GEMNAME-$pkgver.gem](http://rubygems.org/downloads/GEMNAME-$pkgver.gem))
 noextract=(GEMNAME-$pkgver.gem)
 md5sums=()

 build() {
   cd $srcdir
   # _gemdir is defined inside build() because if ruby[gems] is not installed on the system
   #  makepkg will barf when sourcing the PKGBUILD
   local _gemdir="$(ruby -rubygems -e'puts Gem.default_dir')"

   gem install --ignore-dependencies -i "$pkgdir$_gemdir" GEMNAME-$pkgver.gem
 }

 # vim:set ts=2 sw=2 et:

```

## Note

Aggiungi `--verbose` agli argomenti di **gem** per ricevere informazioni addizionali in caso di errori.

**Nota:** L'uso dell'argomento `--no-user-install` per **gem** è obbligatorio per le ultime versioni di Ruby (Vedi[FS#28681](https://bugs.archlinux.org/task/28681) per i dettagli).

### Quarry

Un'alternativa per gestire manualmente i gemfiles è considerare quarry, un repository non ufficiale di pacchetti arch pre-compilati. Vedi [Quarry](/index.php/Quarry "Quarry") per i dettagli.

## Automazione

Abhishek Dasgupta ha scritto [gem2arch](http://github.com/abhidg/gem2arch/) per aiutare ad automatizzare il processo di creazione di un PKGBUILD di un pacchetto gem ruby. Assicurarsi di controllare manualmente il PKGBUILD dopo la relativa creazione.