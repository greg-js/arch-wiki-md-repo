**[Diretrizes de criação de pacotes](/index.php/Criando_pacotes "Criando pacotes")**

* * *

[CLR](/index.php/Diretrizes_de_pacotes_CLR "Diretrizes de pacotes CLR") – [Cross](/index.php/Diretrizes_de_pacotes_de_ferramentas_de_compila%C3%A7%C3%A3o_cruzada "Diretrizes de pacotes de ferramentas de compilação cruzada") – [Eclipse](/index.php/Diretrizes_de_pacotes_de_plugin_do_Eclipse "Diretrizes de pacotes de plugin do Eclipse") – [Free Pascal](/index.php/Diretrizes_de_pacotes_Free_Pascal "Diretrizes de pacotes Free Pascal") – [GNOME](/index.php/Diretrizes_de_pacotes_GNOME "Diretrizes de pacotes GNOME") – [Go](/index.php/Diretrizes_de_pacotes_Go "Diretrizes de pacotes Go") – [Haskell](/index.php/Diretrizes_de_pacotes_Haskell "Diretrizes de pacotes Haskell") – [Java](/index.php/Diretrizes_de_pacotes_Java "Diretrizes de pacotes Java") – [KDE](/index.php/Diretrizes_de_pacotes_KDE "Diretrizes de pacotes KDE") – [Kernel](/index.php/Diretrizes_de_pacotes_de_m%C3%B3dulos_de_kernel "Diretrizes de pacotes de módulos de kernel") – [Lisp](/index.php/Diretrizes_de_pacotes_Lisp "Diretrizes de pacotes Lisp") – [MinGW](/index.php/Diretrizes_de_pacotes_MinGW "Diretrizes de pacotes MinGW") – [Node.js](/index.php/Diretrizes_de_pacotes_Node.js "Diretrizes de pacotes Node.js") – [Nonfree](/index.php/Diretrizes_de_pacotes_de_aplicativos_n%C3%A3o_livres "Diretrizes de pacotes de aplicativos não livres") –[OCaml](/index.php/Diretrizes_de_pacotes_OCaml "Diretrizes de pacotes OCaml") – [Perl](/index.php/Diretrizes_de_pacotes_Perl "Diretrizes de pacotes Perl") – [PHP](/index.php/Diretrizes_de_pacotes_PHP "Diretrizes de pacotes PHP") – [Python](/index.php/Diretrizes_de_pacotes_Python "Diretrizes de pacotes Python") – [Ruby](/index.php/Diretrizes_de_pacotes_Ruby_Gem "Diretrizes de pacotes Ruby Gem") – [VCS](/index.php/Diretrizes_de_pacotes_VCS "Diretrizes de pacotes VCS") – [Web](/index.php/Diretrizes_de_pacotes_de_aplicativos_da_Web "Diretrizes de pacotes de aplicativos da Web") – [Wine](/index.php/Diretrizes_de_pacotes_Wine "Diretrizes de pacotes Wine")

Esse documento cobre padrões e diretrizes de escrita [PKGBUILDs](/index.php/PKGBUILD_(Portugu%C3%AAs) "PKGBUILD (Português)") para pacotes [Node.js](/index.php/Node.js "Node.js").

## Nomenclatura de pacote

Nomes de pacote devem iniciar com um prefixo `nodejs-`.

## Usando npm

Ao instalar com [npm](https://www.archlinux.org/packages/?name=npm), adicione-o como dependência de compilação:

```
makedepends=('npm')

```

Essa é uma função `package` mínima:

```
package() {
    cd $srcdir/$pkgname-$pkgver
    npm install -g --user root --prefix "$pkgdir"/usr
    # Disputa não determinística no npm fornece permissões 777 para diretórios aleatórios.
    # Veja https://github.com/npm/npm/issues/9359 para detalhes.
    find "${pkgdir}"/usr -type d -exec chmod 755 {} +
}

```

### Definindo um cache temporário

Quando o npm processa `package.json` para compilar um pacote, ele baixa dependências para sua pasta de cache padrão em `$HOME/.npm`. Para evitar encher a pasta pessoa do usuário, podemos definir temporariamente uma pasta de cache diferente com a opção `--cache`:

Baixe as dependências para `${srcdir}/npm-cache` e instale-os no diretório do pacote

```
npm install --cache "${srcdir}/npm-cache" 

```

Continue com empacotamento de costume

```
npm run packager

```