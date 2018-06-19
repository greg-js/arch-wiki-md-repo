**[Diretrizes de criação de pacotes](/index.php/Criando_pacotes "Criando pacotes")**

* * *

[CLR](/index.php/Diretrizes_de_pacotes_CLR "Diretrizes de pacotes CLR") – [Cross](/index.php/Diretrizes_de_pacotes_de_ferramentas_de_compila%C3%A7%C3%A3o_cruzada "Diretrizes de pacotes de ferramentas de compilação cruzada") – [Eclipse](/index.php/Diretrizes_de_pacotes_de_plugin_do_Eclipse "Diretrizes de pacotes de plugin do Eclipse") – [Free Pascal](/index.php/Diretrizes_de_pacotes_Free_Pascal "Diretrizes de pacotes Free Pascal") – [GNOME](/index.php/Diretrizes_de_pacotes_GNOME "Diretrizes de pacotes GNOME") – [Go](/index.php/Diretrizes_de_pacotes_Go "Diretrizes de pacotes Go") – [Haskell](/index.php/Diretrizes_de_pacotes_Haskell "Diretrizes de pacotes Haskell") – [Java](/index.php/Diretrizes_de_pacotes_Java "Diretrizes de pacotes Java") – [KDE](/index.php/Diretrizes_de_pacotes_KDE "Diretrizes de pacotes KDE") – [Kernel](/index.php/Diretrizes_de_pacotes_de_m%C3%B3dulos_de_kernel "Diretrizes de pacotes de módulos de kernel") – [Lisp](/index.php/Diretrizes_de_pacotes_Lisp "Diretrizes de pacotes Lisp") – [MinGW](/index.php/Diretrizes_de_pacotes_MinGW "Diretrizes de pacotes MinGW") – [Node.js](/index.php/Diretrizes_de_pacotes_Node.js "Diretrizes de pacotes Node.js") – [Nonfree](/index.php/Diretrizes_de_pacotes_de_aplicativos_n%C3%A3o_livres "Diretrizes de pacotes de aplicativos não livres") –[OCaml](/index.php/Diretrizes_de_pacotes_OCaml "Diretrizes de pacotes OCaml") – [Perl](/index.php/Diretrizes_de_pacotes_Perl "Diretrizes de pacotes Perl") – [PHP](/index.php/Diretrizes_de_pacotes_PHP "Diretrizes de pacotes PHP") – [Python](/index.php/Diretrizes_de_pacotes_Python "Diretrizes de pacotes Python") – [Ruby](/index.php/Diretrizes_de_pacotes_Ruby_Gem "Diretrizes de pacotes Ruby Gem") – [VCS](/index.php/Diretrizes_de_pacotes_VCS "Diretrizes de pacotes VCS") – [Web](/index.php/Diretrizes_de_pacotes_de_aplicativos_da_Web "Diretrizes de pacotes de aplicativos da Web") – [Wine](/index.php/Diretrizes_de_pacotes_Wine "Diretrizes de pacotes Wine")

Os pacotes do [KDE](/index.php/KDE "KDE") no Arch Linux seguem um certo esquema.

## Contents

*   [1 Diretório de compilação](#Diret.C3.B3rio_de_compila.C3.A7.C3.A3o)
*   [2 Prefixo de instalação](#Prefixo_de_instala.C3.A7.C3.A3o)
*   [3 Tipo de compilação](#Tipo_de_compila.C3.A7.C3.A3o)
*   [4 Forçar Qt4](#For.C3.A7ar_Qt4)
    *   [4.1 KDE4](#KDE4)
    *   [4.2 KF5](#KF5)
*   [5 Nomenclatura de pacote KDE4](#Nomenclatura_de_pacote_KDE4)
    *   [5.1 Módulo de Configuração do KDE](#M.C3.B3dulo_de_Configura.C3.A7.C3.A3o_do_KDE)
    *   [5.2 Widgets do Plasma](#Widgets_do_Plasma)
    *   [5.3 Executores](#Executores)
    *   [5.4 Menus de serviço](#Menus_de_servi.C3.A7o)
    *   [5.5 Temas](#Temas)
*   [6 Nomenclatura de pacote KF5](#Nomenclatura_de_pacote_KF5)
    *   [6.1 Widgets de plasma](#Widgets_de_plasma)
    *   [6.2 Executores](#Executores_2)
    *   [6.3 Menus de serviço](#Menus_de_servi.C3.A7o_2)
    *   [6.4 Temas](#Temas_2)
*   [7 Arquivos de .install](#Arquivos_de_.install)

## Diretório de compilação

A good way of building [CMake](https://en.wikipedia.org/wiki/CMake "wikipedia:CMake") packages is to make a build directory outside the root of the project and run cmake from that directory. The [PKGBUILD](/index.php/PKGBUILD "PKGBUILD") should look this way:

```
prepare() {
  mkdir -p build
}

build() {
  cd build
  cmake ../${pkgname}-${pkgver}
}

```

## Prefixo de instalação

Every packages must set the `CMAKE_INSTALL_PREFIX` variable, but also we have to respect custom built versions of KDE, so please use:

```
-DCMAKE_INSTALL_PREFIX=$(kde4-config --prefix)

```

When a package is moved to [extra] or [community] that line must be changed to:

```
-DCMAKE_INSTALL_PREFIX=/usr

```

## Tipo de compilação

Please specify the build type; this makes it really simple to rebuild a package with debug symbols by just using a sed rule.

```
-DCMAKE_BUILD_TYPE=Release

```

## Forçar Qt4

### KDE4

On systems where both [qt4](https://www.archlinux.org/packages/?name=qt4) and [qt5-base](https://www.archlinux.org/packages/?name=qt5-base) are installed, `qmake` refers to the 5.x version, so force cmake to use Qt4 this way:

```
 export QT_SELECT=4

```

or using this option in cmake:

```
-DQT_QMAKE_EXECUTABLE=/usr/bin/qmake-qt4

```

### KF5

The same rules as for KDE4, but you need force cmake to use Qt5 instead of Qt4:

```
 export QT_SELECT=5

```

## Nomenclatura de pacote KDE4

### Módulo de Configuração do KDE

KDE Config Module packages should be named `kcm-*module*`.

### Widgets do Plasma

Plasma widgets (formerly Plasmoids) packages should be named `kdeplasma-applets-*widgetname*` so that they are recognizable as [KDE](/index.php/KDE "KDE")-related packages; this also distinguishes them from the official packages.

### Executores

Plasma runners packages should be named `kdeplasma-runners-*runnername*` so that they are recognizable as [KDE](/index.php/KDE "KDE")-related packages; this also distinguishes them from the official packages.

### Menus de serviço

Service menus packages should be named `kde-servicemenus-*servicename*` so that they are recognizable as [KDE](/index.php/KDE "KDE")-related packages

### Temas

Plasma themes packages should be named `kdeplasma-themes-*themename*` so that they are recognizable as [KDE](/index.php/KDE "KDE")-related packages.

## Nomenclatura de pacote KF5

### Widgets de plasma

Plasma widgets (formerly Plasmoids) packages should be named `plasma5-applets-*widgetname*` so that they are recognizable as Plasma 5-related packages; this also distinguishes them from the official packages.

### Executores

Plasma runners packages should be named `plasma5-runners-*runnername*` so that they are recognizable as Plasma 5-related packages; this also distinguishes them from the official packages.

### Menus de serviço

Service menus packages should be named `kf5-servicemenus-*servicename*` so that they are recognizable as KF5-related packages

### Temas

Plasma themes packages should be named `plasma5-themes-*themename*` so that they are recognizable as Plasma 5-related packages.

## Arquivos de .install

For many [KDE](/index.php/KDE "KDE") packages, all `.install` files look almost exactly the same. Some packages install icons in the hicolor icon theme; use the `xdg-icon-resource` utility provided by the [xdg-utils](https://www.archlinux.org/packages/?name=xdg-utils) package, which is a dependency of the [qt4](https://www.archlinux.org/packages/?name=qt4) package. So use this line:

```
xdg-icon-resource forceupdate --theme hicolor &> /dev/null

```

Many packages install Freedesktop.org compatible `.desktop` files and register MimeType entries in them. Running `update-desktop-database` in `post_install` is recommended as that tool is provided by the [desktop-file-utils](https://www.archlinux.org/packages/?name=desktop-file-utils) package which is a dependency of the [qt4](https://www.archlinux.org/packages/?name=qt4) package. So use this line:

```
update-desktop-database -q

```