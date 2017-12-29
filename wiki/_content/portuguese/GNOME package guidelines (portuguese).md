**[Package creation guidelines](/index.php/Creating_packages "Creating packages")**

* * *

[CLR](/index.php/CLR_package_guidelines "CLR package guidelines") – [Cross](/index.php/Cross-compiling_tools_package_guidelines "Cross-compiling tools package guidelines") – [Eclipse](/index.php/Eclipse_plugin_package_guidelines "Eclipse plugin package guidelines") – [Free Pascal](/index.php/Free_Pascal_package_guidelines "Free Pascal package guidelines") – [GNOME](/index.php/GNOME_package_guidelines "GNOME package guidelines") – [Go](/index.php/Go_package_guidelines "Go package guidelines") – [Haskell](/index.php/Haskell_package_guidelines "Haskell package guidelines") – [Java](/index.php/Java_package_guidelines "Java package guidelines") – [KDE](/index.php/KDE_package_guidelines "KDE package guidelines") – [Kernel](/index.php/Kernel_module_package_guidelines "Kernel module package guidelines") – [Lisp](/index.php/Lisp_package_guidelines "Lisp package guidelines") – [MinGW](/index.php/MinGW_package_guidelines "MinGW package guidelines") – [Node.js](/index.php/Node.js_package_guidelines "Node.js package guidelines") – [Nonfree](/index.php/Nonfree_applications_package_guidelines "Nonfree applications package guidelines") – [OCaml](/index.php/OCaml_package_guidelines "OCaml package guidelines") – [Perl](/index.php/Perl_package_guidelines "Perl package guidelines") – [PHP](/index.php/PHP_package_guidelines "PHP package guidelines") – [Python](/index.php/Python_package_guidelines "Python package guidelines") – [Ruby](/index.php/Ruby_Gem_package_guidelines "Ruby Gem package guidelines") – [VCS](/index.php/VCS_package_guidelines "VCS package guidelines") – [Web](/index.php/Web_application_package_guidelines "Web application package guidelines") – [Wine](/index.php/Wine_package_guidelines "Wine package guidelines")

Os pacotes do [GNOME](/index.php/GNOME_(Portugu%C3%AAs) "GNOME (Português)") no Arch Linux segue, um certo esquema.

## Contents

*   [1 GConf schemas](#GConf_schemas)
*   [2 GSettings schemas](#GSettings_schemas)
*   [3 Documentação do Scrollkeeper](#Documenta.C3.A7.C3.A3o_do_Scrollkeeper)
*   [4 Cache de ícones do GTK](#Cache_de_.C3.ADcones_do_GTK)
*   [5 Arquivos .desktop](#Arquivos_.desktop)
*   [6 Arquivos .install](#Arquivos_.install)

## GConf schemas

Alguns pacotes do GNOME instalam [schemas do GConf](https://en.wikipedia.org/wiki/pt:GConf#Schemas "wikipedia:pt:GConf"), apesar de muitos outros já terem migrados para GSettings. Aqueles pacotes devem depender de [gconf](https://www.archlinux.org/packages/?name=gconf).

Schemas do Gconf são instalados na base de dados GConf do sistema, que deve ser evitado. Alguns pacotes fornecem uma opção `--disable-schemas-install` para o **./configure**, que dificilmente funciona. Porém, gconftool-2 tem uma variável chamada `GCONF_DISABLE_MAKEFILE_SCHEMA_INSTALL` a qual você pode definir para dizer ao gconftool-2 para não atualizar qualquer base de dados.

Ao criar pacotes que instalam arquivos schemas de GConf, use

 `make GCONF_DISABLE_MAKEFILE_SCHEMA_INSTALL=1 DESTDIR=${pkgdir} install` 

para a etapa de instalação do pacote no PKGBUILD.

Não chame `gconfpkg` no arquivo .install, pois schemas do GConf são automaticamente instalados/removidos (na instalação/remoção de um pacote GNOME) via [hooks do *pacman*](/index.php/Pacman_(Portugu%C3%AAs)#hooks "Pacman (Português)") desde o [gconf](https://www.archlinux.org/packages/?name=gconf)=3.2.6-4

## GSettings schemas

Os schemas de Gconf foram migrados para schemas do GSettings, então muitos aplicativos pode ser encontrados usando esse novo arquivo de schema. GSettings usa o dconf como backend, então todos os pacotes que contêm schemas de GSettings exigem [dconf](https://www.archlinux.org/packages/?name=dconf) como dependência. Quando um novo schema de GSettings é instalado no sistema, a base de dados do GSettings tem que ser recompilada, mas não durante o empacotamento.

Para evitar recompilação da base de dados do GSettings no empacotamento, use a opção `--disable-schemas-compile` para o **./configure**.

Não chame `glib-compile-schemas` no arquivo .install, pois as bases de dados de schemas do GSettings são recompilados automaticamente via [hooks do pacman](/index.php/Pacman_(Portugu%C3%AAs)#hooks "Pacman (Português)") desde [glib2](https://www.archlinux.org/packages/?name=glib2)=2.48.0-2.

## Documentação do Scrollkeeper

A partir do GNOME 2.20, não há mais necessidade de lidar com scrollkeeper, pois [rarian](https://www.archlinux.org/packages/?name=rarian) lê seus arquivos OMF diretamente. Scrollkeeper-update é um link dos dias atuais. A única coisa que é necessário agora é acrescentar [gnome-doc-utils](https://www.archlinux.org/packages/?name=gnome-doc-utils)>=0.11.2 ao vetor `makedepends`.

Ele pode ser desabilitado usando a opção `--disable-scrollkeeper` no **./configure**.

## Cache de ícones do GTK

Alguns ícones de instalação de pacotes no tema do ícone do hicolor. Esses pacotes devem depender de [gtk-update-icon-cache](https://www.archlinux.org/packages/?name=gtk-update-icon-cache).

Não chame `gtk-update-icon-cache` no arquivo .install, pois o cache de ícone é atualizado via [hooks do pacman](/index.php/Pacman_(Portugu%C3%AAs)#hooks "Pacman (Português)") desde [gtk-update-icon-cache](https://www.archlinux.org/packages/?name=gtk-update-icon-cache)=3.20.3-2.

## Arquivos .desktop

Muitos pacotes instalam arquivos `.desktop` compatíveis com Freedesktop.org e registram entradas tipo MIME neles. Eles devem depender de [desktop-file-utils](https://www.archlinux.org/packages/?name=desktop-file-utils).

Não chame `update-desktop-database` no arquivo .install, pois a base de dados é atualizada automaticamente via [hooks do pacman](/index.php/Pacman_(Portugu%C3%AAs)#hooks "Pacman (Português)") desde [desktop-file-utils](https://www.archlinux.org/packages/?name=desktop-file-utils)=0.22-2.

## Arquivos .install

Anteriormente, a maioria dos pacotes GNOME tinham um arquivo .install chamando comandos como `glib-compile-schemas`, `gtk-update-icon-cache` e `update-desktop-database` para instalar/atualizar cache local ou base de dados. Isso está obsoleto desde o pacman 5.0, que trouxe a implementação de [hooks](/index.php/Pacman_(Portugu%C3%AAs)#Hooks "Pacman (Português)") que chamam aqueles comandos automaticamente ao instalar o pacote.

Para evitar ser chamado duas vezes, os comandos supramencionados devem ser removidos do arquivo .install.