**Status de tradução:** Esse artigo é uma tradução de [Rust package guidelines](/index.php/Rust_package_guidelines "Rust package guidelines"). Data da última tradução: 2019-05-23\. Você pode ajudar a sincronizar a tradução, se houver [alterações](https://wiki.archlinux.org/index.php?title=Rust_package_guidelines&diff=0&oldid=571223) na versão em inglês.

**[Diretrizes de criação de pacotes](/index.php/Padr%C3%B5es_de_empacotamento_do_Arch "Padrões de empacotamento do Arch")**

* * *

[CLR](/index.php/Diretrizes_de_pacotes_CLR "Diretrizes de pacotes CLR") – [Cross](/index.php/Diretrizes_de_pacotes_de_ferramentas_de_compila%C3%A7%C3%A3o_cruzada "Diretrizes de pacotes de ferramentas de compilação cruzada") – [Eclipse](/index.php/Diretrizes_de_pacotes_de_plugin_do_Eclipse "Diretrizes de pacotes de plugin do Eclipse") – [Electron](/index.php/Diretrizes_de_pacotes_Electron "Diretrizes de pacotes Electron") – [Free Pascal](/index.php/Diretrizes_de_pacotes_Free_Pascal "Diretrizes de pacotes Free Pascal") – [GNOME](/index.php/Diretrizes_de_pacotes_GNOME "Diretrizes de pacotes GNOME") – [Go](/index.php/Diretrizes_de_pacotes_Go "Diretrizes de pacotes Go") – [Haskell](/index.php/Diretrizes_de_pacotes_Haskell "Diretrizes de pacotes Haskell") – [Java](/index.php/Diretrizes_de_pacotes_Java "Diretrizes de pacotes Java") – [KDE](/index.php/Diretrizes_de_pacotes_KDE "Diretrizes de pacotes KDE") – [Kernel](/index.php/Diretrizes_de_pacotes_de_m%C3%B3dulos_de_kernel "Diretrizes de pacotes de módulos de kernel") – [Lisp](/index.php/Diretrizes_de_pacotes_Lisp "Diretrizes de pacotes Lisp") – [MinGW](/index.php/Diretrizes_de_pacotes_MinGW "Diretrizes de pacotes MinGW") – [Node.js](/index.php/Diretrizes_de_pacotes_Node.js "Diretrizes de pacotes Node.js") – [Nonfree](/index.php/Diretrizes_de_pacotes_de_aplicativos_n%C3%A3o_livres "Diretrizes de pacotes de aplicativos não livres") – [OCaml](/index.php/Diretrizes_de_pacotes_OCaml "Diretrizes de pacotes OCaml") – [Perl](/index.php/Diretrizes_de_pacotes_Perl "Diretrizes de pacotes Perl") – [PHP](/index.php/Diretrizes_de_pacotes_PHP "Diretrizes de pacotes PHP") – [Python](/index.php/Diretrizes_de_pacotes_Python "Diretrizes de pacotes Python") – [R](/index.php/Diretrizes_de_pacotes_R "Diretrizes de pacotes R") – [Ruby](/index.php/Diretrizes_de_pacotes_Ruby_Gem "Diretrizes de pacotes Ruby Gem") – [Rust](/index.php/Diretrizes_de_pacotes_Rust "Diretrizes de pacotes Rust") – [VCS](/index.php/Diretrizes_de_pacotes_VCS "Diretrizes de pacotes VCS") – [Web](/index.php/Diretrizes_de_pacotes_de_aplicativos_da_Web "Diretrizes de pacotes de aplicativos da Web") – [Wine](/index.php/Diretrizes_de_pacotes_Wine "Diretrizes de pacotes Wine")

Esse documento cobre padrões e diretrizes sobre escrita de [PKGBUILDs](/index.php/PKGBUILD_(Portugu%C3%AAs) "PKGBUILD (Português)") para [Rust](/index.php/Rust "Rust").

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Diretrizes gerais](#Diretrizes_gerais)
    *   [1.1 Nomenclatura de pacote](#Nomenclatura_de_pacote)
*   [2 Compilação](#Compilação)
*   [3 Verificação](#Verificação)
*   [4 Pacote](#Pacote)

## Diretrizes gerais

### Nomenclatura de pacote

Para binários do [Rust](/index.php/Rust "Rust"), use apenas o nome do programa.

**Nota:** O nome do pacote deve estar todo em minúsculo.

## Compilação

Compilação de um pacote Rust.

```
 build() {
   cargo build --release --locked
 }

```

sendo que:

*   `--release` diz ao *cargo* para fazer uma compilação lançamento
*   `--locked` diz ao *cargo* para fazer uso do arquivo `Cargo.lock` e impedi-lo de atualizar dependências, o que é importante para [reproducible builds](https://reproducible-builds.org/).

## Verificação

A maioria dos projetos Rust fornecem uma forma simples de executar o conjunto de testes (*testsuite*).

```
 check() {
   cargo test --release --locked
 }

```

## Pacote

O Rust compila binários em `target/release` e pode simplesmente ser instalado em `/usr/bin`.

```
 package() {
   install -Dm 755 target/release/${pkgname} -t "${pkgdir}/usr/bin"
 }

```

Alguns pacotes podem instalar mais arquivos, como uma página man, caso em que pode ser melhor usar `cargo`:

```
 package() {
   cargo install --root "${pkgdir}"/usr --root "${srcdir}/${pkgname}-${pkgver}"
 }

```