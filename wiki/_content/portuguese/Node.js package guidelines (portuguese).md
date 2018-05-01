**[Package creation guidelines](/index.php/Creating_packages "Creating packages")**

* * *

[CLR](/index.php/CLR_package_guidelines "CLR package guidelines") – [Cross](/index.php/Cross-compiling_tools_package_guidelines "Cross-compiling tools package guidelines") – [Eclipse](/index.php/Eclipse_plugin_package_guidelines "Eclipse plugin package guidelines") – [Free Pascal](/index.php/Free_Pascal_package_guidelines "Free Pascal package guidelines") – [GNOME](/index.php/GNOME_package_guidelines "GNOME package guidelines") – [Go](/index.php/Go_package_guidelines "Go package guidelines") – [Haskell](/index.php/Haskell_package_guidelines "Haskell package guidelines") – [Java](/index.php/Java_package_guidelines "Java package guidelines") – [KDE](/index.php/KDE_package_guidelines "KDE package guidelines") – [Kernel](/index.php/Kernel_module_package_guidelines "Kernel module package guidelines") – [Lisp](/index.php/Lisp_package_guidelines "Lisp package guidelines") – [MinGW](/index.php/MinGW_package_guidelines "MinGW package guidelines") – [Node.js](/index.php/Node.js_package_guidelines "Node.js package guidelines") – [Nonfree](/index.php/Nonfree_applications_package_guidelines "Nonfree applications package guidelines") – [OCaml](/index.php/OCaml_package_guidelines "OCaml package guidelines") – [Perl](/index.php/Perl_package_guidelines "Perl package guidelines") – [PHP](/index.php/PHP_package_guidelines "PHP package guidelines") – [Python](/index.php/Python_package_guidelines "Python package guidelines") – [Ruby](/index.php/Ruby_Gem_package_guidelines "Ruby Gem package guidelines") – [VCS](/index.php/VCS_package_guidelines "VCS package guidelines") – [Web](/index.php/Web_application_package_guidelines "Web application package guidelines") – [Wine](/index.php/Wine_package_guidelines "Wine package guidelines")

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