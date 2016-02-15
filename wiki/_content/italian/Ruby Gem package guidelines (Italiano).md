## Contents

*   [1 Nomenclatura del pacchetto](#Nomenclatura_del_pacchetto)
*   [2 Esempi](#Esempi)
*   [3 Esempio PKGBUILD](#Esempio_PKGBUILD)
*   [4 Automazione](#Automazione)

## Nomenclatura del pacchetto

Per le librerie, utilizzare "ruby-gemname". Per le applicazioni, utilizzare il nome del programma. In entrambi i casi il nome dovrebbe essere tutto in minuscolo.

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

## Automazione

Abhishek Dasgupta ha scritto [gem2arch](http://github.com/abhidg/gem2arch/) per aiutare ad automatizzare il processo di creazione di un PKGBUILD di un pacchetto gem ruby. Assicurarsi di controllare manualmente il PKGBUILD dopo la relativa creazione.