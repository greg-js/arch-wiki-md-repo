**[Package creation guidelines](/index.php/Creating_packages "Creating packages")**

* * *

[CLR](/index.php/CLR_package_guidelines "CLR package guidelines") – [Cross](/index.php/Cross-compiling_tools_package_guidelines "Cross-compiling tools package guidelines") – [Eclipse](/index.php/Eclipse_plugin_package_guidelines "Eclipse plugin package guidelines") – [Free Pascal](/index.php/Free_Pascal_package_guidelines "Free Pascal package guidelines") – [GNOME](/index.php/GNOME_package_guidelines "GNOME package guidelines") – [Go](/index.php/Go_package_guidelines "Go package guidelines") – [Haskell](/index.php/Haskell_package_guidelines "Haskell package guidelines") – [Java](/index.php/Java_package_guidelines "Java package guidelines") – [KDE](/index.php/KDE_package_guidelines "KDE package guidelines") – [Kernel](/index.php/Kernel_module_package_guidelines "Kernel module package guidelines") – [Lisp](/index.php/Lisp_package_guidelines "Lisp package guidelines") – [MinGW](/index.php/MinGW_package_guidelines "MinGW package guidelines") – [Node.js](/index.php/Node.js_package_guidelines "Node.js package guidelines") – [Nonfree](/index.php/Nonfree_applications_package_guidelines "Nonfree applications package guidelines") – [OCaml](/index.php/OCaml_package_guidelines "OCaml package guidelines") – [Perl](/index.php/Perl_package_guidelines "Perl package guidelines") – [PHP](/index.php/PHP_package_guidelines "PHP package guidelines") – [Python](/index.php/Python_package_guidelines "Python package guidelines") – [Ruby](/index.php/Ruby_Gem_package_guidelines "Ruby Gem package guidelines") – [VCS](/index.php/VCS_package_guidelines "VCS package guidelines") – [Web](/index.php/Web_application_package_guidelines "Web application package guidelines") – [Wine](/index.php/Wine_package_guidelines "Wine package guidelines")

Este documento define o padrão para a empacotamento de projetos Common Language Runtime (.NET) sob Arch Linux. Atualmente, apenas o [Mono](/index.php/Mono "Mono") é capaz de fornecer um runtime CLR usável e eficiente para vários sistemas e esse padrão refletirá seu uso. Esteja ciente de que muitos programas CLR foram desenvolvidos com o Microsoft .NET em mente e, como tal, podem ou não ser executados em Mono por causa de fatores exclusivos do .NET, como chamadas P/Invoke e APIs de Gestão Digital de Direitos (DRM) da Microsoft e, portanto, não produzirá um pacote utilizável para o Arch Linux. No entanto, se combinado com [Wine](/index.php/Wine "Wine") a partir da versão 1.5.6 (?), seu pacote pode ter a chance de executar sob ele. Consulte as [diretrizes de pacote Wine](/index.php/Wine_package_guidelines "Wine package guidelines") para obter mais informações, se tal for o caso.

## Contents

*   [1 Pegadinhas de empacotamento](#Pegadinhas_de_empacotamento)
    *   [1.1 Montagens assinadas](#Montagens_assinadas)
*   [2 Exemplos de PKGBUILD](#Exemplos_de_PKGBUILD)
    *   [2.1 xbuild](#xbuild)
        *   [2.1.1 Unsigned DLL](#Unsigned_DLL)
    *   [2.2 NAnt](#NAnt)
    *   [2.3 Prebuild](#Prebuild)

## Pegadinhas de empacotamento

*   Sempre adicione [mono](https://www.archlinux.org/packages/?name=mono) a `depends`
*   Sempre defina `arch` como `any`. Mono não oferece suporte a compilar (executar?) montagens de 64 bits.
*   Sempre adicione `!strip` a `options`
*   Se o pacote é uma biblioteca (DLL), considere instalá-lo ao *Global Assembly Cache* (GAC) do Mono, se ele for usado como uma dependência.
*   Se a montagem é pré-compilada e vem com um arquivo de banco de dados para depuração de programas (Foo.dll.pdb), considere convertê-la como tal: `pdb2mdb Foo.dll`
*   Se o pacote destina-se a ser um executável (EXE), certifique-se de instalar em `/usr/bin` um shell script para executá-lo, similar a esse:

```
#!/bin/sh
mono foo.exe $@

```

### Montagens assinadas

Se o pacote for instalado no GAC, certifique-se de ter um arquivo de chave assinado. Caso contrário, você pode gerar um como este: `sn -k 1024 Foo.snk`. Em seguida, a forma mais fácil de embutir o arquivo chave na montagem para ser desmontada assim: `monodis Foo.dll --output=Foo.il`. Após, remonte-o assim: `ilasm /dll /key:Foo.snk Foo.il`

## Exemplos de PKGBUILD

Os exemplos a seguir vão tentar cobrir algumas das convenções mais comuns e sistemas de compilação.

### xbuild

#### Unsigned DLL

```
# Maintainer: yourname <yourmail>
pkgname=foo
pkgver=1.0
pkgrel=1
pkgdesc="Fantabulous library for .Net"
arch=('any')
url="http://www.foo.bar"
license=('GPL')
depends=('mono')
options=('!strip')
source=("http://www.foo.bar/foobar.tar.gz")
md5sums=('4736ac4f34fd9a41fa0197eac23bbc24')

build() {
  cd "${srcdir}/foobar"

  xbuild Foo.sln

  # if the package is unsigned, do the following:
  cd "/bin/x86/Debug"
  monodis Foo.dll --output=Foo.il
  sn -k 1024 Foo.snk
  ilasm /dll /key:Foo.snk Foo.il
}

package() {
  cd "${srcdir}/foobar/bin/x86/Debug"

  install -Dm644 Foo.dll "$pkgdir/usr/lib/foobar/Foo.dll"
  install -Dm644 Foo.dll.mdb "$pkgdir/usr/lib/foobar/Foo.dll.mdb"

  # Register assembly into Mono's GAC
  gacutil -i Foo.dll -root "$pkgdir/usr/lib"
}

```

### NAnt

### Prebuild