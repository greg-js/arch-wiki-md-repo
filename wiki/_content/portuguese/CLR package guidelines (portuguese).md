**[Diretrizes de criação de pacotes](/index.php/Criando_pacotes "Criando pacotes")**

* * *

[CLR](/index.php/Diretrizes_de_pacotes_CLR "Diretrizes de pacotes CLR") – [Cross](/index.php/Diretrizes_de_pacotes_de_ferramentas_de_compila%C3%A7%C3%A3o_cruzada "Diretrizes de pacotes de ferramentas de compilação cruzada") – [Eclipse](/index.php/Diretrizes_de_pacotes_de_plugin_do_Eclipse "Diretrizes de pacotes de plugin do Eclipse") – [Free Pascal](/index.php/Diretrizes_de_pacotes_Free_Pascal "Diretrizes de pacotes Free Pascal") – [GNOME](/index.php/Diretrizes_de_pacotes_GNOME "Diretrizes de pacotes GNOME") – [Go](/index.php/Diretrizes_de_pacotes_Go "Diretrizes de pacotes Go") – [Haskell](/index.php/Diretrizes_de_pacotes_Haskell "Diretrizes de pacotes Haskell") – [Java](/index.php/Diretrizes_de_pacotes_Java "Diretrizes de pacotes Java") – [KDE](/index.php/Diretrizes_de_pacotes_KDE "Diretrizes de pacotes KDE") – [Kernel](/index.php/Diretrizes_de_pacotes_de_m%C3%B3dulos_de_kernel "Diretrizes de pacotes de módulos de kernel") – [Lisp](/index.php/Diretrizes_de_pacotes_Lisp "Diretrizes de pacotes Lisp") – [MinGW](/index.php/Diretrizes_de_pacotes_MinGW "Diretrizes de pacotes MinGW") – [Node.js](/index.php/Diretrizes_de_pacotes_Node.js "Diretrizes de pacotes Node.js") – [Nonfree](/index.php/Diretrizes_de_pacotes_de_aplicativos_n%C3%A3o_livres "Diretrizes de pacotes de aplicativos não livres") –[OCaml](/index.php/Diretrizes_de_pacotes_OCaml "Diretrizes de pacotes OCaml") – [Perl](/index.php/Diretrizes_de_pacotes_Perl "Diretrizes de pacotes Perl") – [PHP](/index.php/Diretrizes_de_pacotes_PHP "Diretrizes de pacotes PHP") – [Python](/index.php/Diretrizes_de_pacotes_Python "Diretrizes de pacotes Python") – [R](/index.php/Diretrizes_de_pacotes_R "Diretrizes de pacotes R") – [Ruby](/index.php/Diretrizes_de_pacotes_Ruby_Gem "Diretrizes de pacotes Ruby Gem") – [VCS](/index.php/Diretrizes_de_pacotes_VCS "Diretrizes de pacotes VCS") – [Web](/index.php/Diretrizes_de_pacotes_de_aplicativos_da_Web "Diretrizes de pacotes de aplicativos da Web") – [Wine](/index.php/Diretrizes_de_pacotes_Wine "Diretrizes de pacotes Wine")

Este documento define o padrão para a empacotamento de projetos Common Language Runtime (.NET) sob Arch Linux. Atualmente, apenas o [Mono](/index.php/Mono "Mono") é capaz de fornecer um runtime CLR usável e eficiente para vários sistemas e esse padrão refletirá seu uso. Esteja ciente de que muitos programas CLR foram desenvolvidos com o Microsoft .NET em mente e, como tal, podem ou não ser executados em Mono por causa de fatores exclusivos do .NET, como chamadas P/Invoke e APIs de Gestão Digital de Direitos (DRM) da Microsoft e, portanto, não produzirá um pacote utilizável para o Arch Linux. No entanto, se combinado com [Wine](/index.php/Wine "Wine") a partir da versão 1.5.6 (?), seu pacote pode ter a chance de executar sob ele. Consulte as [diretrizes de pacotes Wine](/index.php/Diretrizes_de_pacotes_Wine "Diretrizes de pacotes Wine") para obter mais informações, se tal for o caso.

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