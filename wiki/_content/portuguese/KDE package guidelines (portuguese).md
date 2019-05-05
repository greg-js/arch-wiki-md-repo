**Status de tradução:** Esse artigo é uma tradução de [KDE package guidelines](/index.php/KDE_package_guidelines "KDE package guidelines"). Data da última tradução: 2019-04-17\. Você pode ajudar a sincronizar a tradução, se houver [alterações](https://wiki.archlinux.org/index.php?title=KDE_package_guidelines&diff=0&oldid=569678) na versão em inglês.

**[Diretrizes de criação de pacotes](/index.php/Padr%C3%B5es_de_empacotamento_do_Arch "Padrões de empacotamento do Arch")**

* * *

[CLR](/index.php/Diretrizes_de_pacotes_CLR "Diretrizes de pacotes CLR") – [Cross](/index.php/Diretrizes_de_pacotes_de_ferramentas_de_compila%C3%A7%C3%A3o_cruzada "Diretrizes de pacotes de ferramentas de compilação cruzada") – [Eclipse](/index.php/Diretrizes_de_pacotes_de_plugin_do_Eclipse "Diretrizes de pacotes de plugin do Eclipse") – [Electron](/index.php/Diretrizes_de_pacotes_Electron "Diretrizes de pacotes Electron") – [Free Pascal](/index.php/Diretrizes_de_pacotes_Free_Pascal "Diretrizes de pacotes Free Pascal") – [GNOME](/index.php/Diretrizes_de_pacotes_GNOME "Diretrizes de pacotes GNOME") – [Go](/index.php/Diretrizes_de_pacotes_Go "Diretrizes de pacotes Go") – [Haskell](/index.php/Diretrizes_de_pacotes_Haskell "Diretrizes de pacotes Haskell") – [Java](/index.php/Diretrizes_de_pacotes_Java "Diretrizes de pacotes Java") – [KDE](/index.php/Diretrizes_de_pacotes_KDE "Diretrizes de pacotes KDE") – [Kernel](/index.php/Diretrizes_de_pacotes_de_m%C3%B3dulos_de_kernel "Diretrizes de pacotes de módulos de kernel") – [Lisp](/index.php/Diretrizes_de_pacotes_Lisp "Diretrizes de pacotes Lisp") – [MinGW](/index.php/Diretrizes_de_pacotes_MinGW "Diretrizes de pacotes MinGW") – [Node.js](/index.php/Diretrizes_de_pacotes_Node.js "Diretrizes de pacotes Node.js") – [Nonfree](/index.php/Diretrizes_de_pacotes_de_aplicativos_n%C3%A3o_livres "Diretrizes de pacotes de aplicativos não livres") – [OCaml](/index.php/Diretrizes_de_pacotes_OCaml "Diretrizes de pacotes OCaml") – [Perl](/index.php/Diretrizes_de_pacotes_Perl "Diretrizes de pacotes Perl") – [PHP](/index.php/Diretrizes_de_pacotes_PHP "Diretrizes de pacotes PHP") – [Python](/index.php/Diretrizes_de_pacotes_Python "Diretrizes de pacotes Python") – [R](/index.php/Diretrizes_de_pacotes_R "Diretrizes de pacotes R") – [Ruby](/index.php/Diretrizes_de_pacotes_Ruby_Gem "Diretrizes de pacotes Ruby Gem") – [Rust](/index.php/Diretrizes_de_pacotes_Rust "Diretrizes de pacotes Rust") – [VCS](/index.php/Diretrizes_de_pacotes_VCS "Diretrizes de pacotes VCS") – [Web](/index.php/Diretrizes_de_pacotes_de_aplicativos_da_Web "Diretrizes de pacotes de aplicativos da Web") – [Wine](/index.php/Diretrizes_de_pacotes_Wine "Diretrizes de pacotes Wine")

Os pacotes do [KDE](/index.php/KDE "KDE") no Arch Linux seguem um certo esquema.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Diretório de compilação](#Diretório_de_compilação)
*   [2 Prefixo de instalação](#Prefixo_de_instalação)
*   [3 Tipo de compilação](#Tipo_de_compilação)
*   [4 Forçar Qt4](#Forçar_Qt4)
    *   [4.1 KDE4](#KDE4)
    *   [4.2 KF5](#KF5)
*   [5 Nomenclatura de pacote KDE4](#Nomenclatura_de_pacote_KDE4)
    *   [5.1 Módulo de Configuração do KDE](#Módulo_de_Configuração_do_KDE)
    *   [5.2 Widgets do Plasma](#Widgets_do_Plasma)
    *   [5.3 Executores](#Executores)
    *   [5.4 Menus de serviço](#Menus_de_serviço)
    *   [5.5 Temas](#Temas)
*   [6 Nomenclatura de pacote KF5](#Nomenclatura_de_pacote_KF5)
    *   [6.1 Widgets de plasma](#Widgets_de_plasma)
    *   [6.2 Executores](#Executores_2)
    *   [6.3 Menus de serviço](#Menus_de_serviço_2)
    *   [6.4 Temas](#Temas_2)
*   [7 Instalação de arquivos de ícones e .desktop](#Instalação_de_arquivos_de_ícones_e_.desktop)

## Diretório de compilação

Uma boa maneira de compilar pacotes de [CMake](https://en.wikipedia.org/wiki/pt:CMake deve ficar assim:

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

Cada pacote deve definir a variável `CMAKE_INSTALL_PREFIX`, mas também temos que respeitar as versões personalizadas do KDE, então use:

```
-DCMAKE_INSTALL_PREFIX=$(kde4-config --prefix)

```

ou para KDE 5:

```
-DCMAKE_INSTALL_PREFIX=$(kf5-config --prefix)

```

Quando um pacote é movido para [extra] ou [community], essa linha deve ser alterada para:

```
-DCMAKE_INSTALL_PREFIX=/usr

```

## Tipo de compilação

Por favor, especifique o tipo de compilação; Isso torna realmente simples recompilar um pacote com símbolos de depuração usando apenas uma regra *sed*.

```
-DCMAKE_BUILD_TYPE=Release

```

## Forçar Qt4

### KDE4

Em sistemas onde ambos [qt4](https://aur.archlinux.org/packages/qt4/) e [qt5-base](https://www.archlinux.org/packages/?name=qt5-base) estão instalados, o *qmake* refere-se à versão 5.x, então force o *cmake* a usar o Qt4 desta maneira:

```
 export QT_SELECT=4

```

ou usando essa opção em *cmake*:

```
-DQT_QMAKE_EXECUTABLE=/usr/bin/qmake-qt4

```

### KF5

As mesmas regras que para o KDE4, mas você precisa forçar o *cmake* a usar o Qt5 ao invés do Qt4:

```
 export QT_SELECT=5

```

## Nomenclatura de pacote KDE4

### Módulo de Configuração do KDE

Pacotes de módulo de configuração do KDE devem ser nomeados `kcm-*módulo*`.

### Widgets do Plasma

Os pacotes de widgets de Plasma (anteriormente Plasmoids) devem ser nomeados `kdeplasma-applets-*nome_widget*` para que sejam reconhecidos como pacotes relacionados ao [KDE](/index.php/KDE "KDE"); isso também os distingue dos pacotes oficiais.

### Executores

Os pacotes de corredores de plasma devem ser nomeados `kdeplasma-runners-*nome_do_runner*` para que sejam reconhecidos como pacotes relacionados ao [KDE](/index.php/KDE "KDE"); isso também os distingue dos pacotes oficiais.

### Menus de serviço

Os pacotes de menus de serviço devem ser nomeados `kde-servicemenus-*nome_do_serviço*` para que sejam reconhecidos como pacotes relacionados ao [KDE](/index.php/KDE "KDE")

### Temas

Os pacotes de temas de plasma devem ser nomeados `kdeplasma-themes-*nome_do_tema*` para que sejam reconhecidos como pacotes relacionados ao [KDE](/index.php/KDE "KDE").

## Nomenclatura de pacote KF5

### Widgets de plasma

Os pacotes de widgets de plasma (anteriormente Plasmoids) devem ser nomeados `plasma5-applets-*nome_do_widget*` para que sejam reconhecíveis como pacotes relacionados ao Plasma 5; isso também os distingue dos pacotes oficiais.

### Executores

Os pacotes de corredores de plasma devem ser nomeados `plasma5-runners-*nome_do_runner*` para que sejam reconhecidos como pacotes relacionados ao Plasma 5; isso também os distingue dos pacotes oficiais.

### Menus de serviço

Os pacotes de menus de serviço devem ser nomeados `kf5-servicemenus-*nome_do_serviço*` para que sejam reconhecidos como pacotes relacionados ao KF5

### Temas

Os pacotes de temas de plasma devem ser nomeados `plasma5-themes-*nome_do_tema*` para que sejam reconhecidos como pacotes relacionados ao Plasma 5.

## Instalação de arquivos de ícones e .desktop

Alguns softwares do [KDE](/index.php/KDE "KDE") fornecem ícones em arquivos de *hicolor icon theme* e `.desktop`, os quais devem ser instalados via [hooks do pacman](/index.php/Hooks_do_pacman "Hooks do pacman"). Evite usar comando de instalação para esses tipos de arquivos em arquivos `.install`, pois resultaria em desnecessária execução duplicada.

O pacote [qt4](https://aur.archlinux.org/packages/qt4/) já depende de [xdg-utils](https://www.archlinux.org/packages/?name=xdg-utils), [hicolor-icon-theme](https://www.archlinux.org/packages/?name=hicolor-icon-theme) e [desktop-file-utils](https://www.archlinux.org/packages/?name=desktop-file-utils), então se seu pacote depender do [qt4](https://aur.archlinux.org/packages/qt4/), nenhuma outra ação deve ser necessária (isto é, desnecessário adicionar esses pacotes ao vetor de `depends`).