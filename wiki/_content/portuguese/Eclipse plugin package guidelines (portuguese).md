**[Package creation guidelines](/index.php/Creating_packages "Creating packages")**

* * *

[CLR](/index.php/CLR_package_guidelines "CLR package guidelines") – [Cross](/index.php/Cross-compiling_tools_package_guidelines "Cross-compiling tools package guidelines") – [Eclipse](/index.php/Eclipse_plugin_package_guidelines "Eclipse plugin package guidelines") – [Free Pascal](/index.php/Free_Pascal_package_guidelines "Free Pascal package guidelines") – [GNOME](/index.php/GNOME_package_guidelines "GNOME package guidelines") – [Go](/index.php/Go_package_guidelines "Go package guidelines") – [Haskell](/index.php/Haskell_package_guidelines "Haskell package guidelines") – [Java](/index.php/Java_package_guidelines "Java package guidelines") – [KDE](/index.php/KDE_package_guidelines "KDE package guidelines") – [Kernel](/index.php/Kernel_module_package_guidelines "Kernel module package guidelines") – [Lisp](/index.php/Lisp_package_guidelines "Lisp package guidelines") – [MinGW](/index.php/MinGW_package_guidelines "MinGW package guidelines") – [Node.js](/index.php/Node.js_package_guidelines "Node.js package guidelines") – [Nonfree](/index.php/Nonfree_applications_package_guidelines "Nonfree applications package guidelines") – [OCaml](/index.php/OCaml_package_guidelines "OCaml package guidelines") – [Perl](/index.php/Perl_package_guidelines "Perl package guidelines") – [PHP](/index.php/PHP_package_guidelines "PHP package guidelines") – [Python](/index.php/Python_package_guidelines "Python package guidelines") – [Ruby](/index.php/Ruby_Gem_package_guidelines "Ruby Gem package guidelines") – [VCS](/index.php/VCS_package_guidelines "VCS package guidelines") – [Web](/index.php/Web_application_package_guidelines "Web application package guidelines") – [Wine](/index.php/Wine_package_guidelines "Wine package guidelines")

Há muitas maneiras de instalar os plugins do [Eclipse](/index.php/Eclipse "Eclipse"), especialmente desde a introdução do diretório *dropins* no Eclipse 3.4, mas alguns deles são confusos, e ter uma maneira padronizada e consistente de empacotamento é muito importante levar a uma estrutura de sistema limpa. Não é fácil, no entanto, conseguir isso sem que o empacotador saiba todos os detalhes sobre como os plug-ins do Eclipse funcionam. Esta página tem como objetivo definir uma estrutura padrão e simples para [PKGBUILDs](/index.php/PKGBUILD_(Portugu%C3%AAs) "PKGBUILD (Português)") de plugins do Eclipse, para que a estrutura do sistema de arquivos permaneça consistente entre todos os plugins sem que o empacotador seja iniciado novamente para cada novo pacote.

## Contents

*   [1 Estrutura e instalação de plugins do Eclipse](#Estrutura_e_instala.C3.A7.C3.A3o_de_plugins_do_Eclipse)
*   [2 Empacotamento](#Empacotamento)
    *   [2.1 Exemplo de PKGBUILD](#Exemplo_de_PKGBUILD)
    *   [2.2 Como personalizar a compilação](#Como_personalizar_a_compila.C3.A7.C3.A3o)
    *   [2.3 Revisão aprofundada do PKGBUILD](#Revis.C3.A3o_aprofundada_do_PKGBUILD)
        *   [2.3.1 Nomenclatura de pacote](#Nomenclatura_de_pacote)
        *   [2.3.2 Arquivos](#Arquivos)
            *   [2.3.2.1 Extração](#Extra.C3.A7.C3.A3o)
            *   [2.3.2.2 Localizações](#Localiza.C3.A7.C3.B5es)
        *   [2.3.3 A função build()](#A_fun.C3.A7.C3.A3o_build.28.29)
*   [3 Solução de problemas](#Solu.C3.A7.C3.A3o_de_problemas)

## Estrutura e instalação de plugins do Eclipse

O plug-in típico do Eclipse contém dois diretórios, `features` e `plugins` e, desde o Eclipse 3.3, eles podem ser colocados apenas em `/usr/lib/eclipse/`. O conteúdo desses dois diretórios pode ser mesclado com o de outros plugins, e criou uma confusão e tornou a estrutura difícil de gerenciar. Também foi muito difícil dizer rapidamente qual pacote continha qual arquivo.

Ainda há suporte a esse método de instalação no Eclipse 3.4, mas o preferido agora está usando o diretório `/usr/lib/eclipse/dropins/`. Dentro deste diretório pode-se viver um número ilimitado de subdiretórios, cada um contendo seus próprios subdiretórios `features` e `plugins`. Isso permite manter uma estrutura limpa e arrumada e deve ser o modo de empacotamento padrão.

## Empacotamento

### Exemplo de PKGBUILD

Arquivo está um exemplo, nós vamos detalhar como personalizá-lo.

 `PKGBUILD-eclipse.proto` 
```
pkgname=eclipse-mylyn
pkgver=3.0.3
pkgrel=1
pkgdesc="A task-focused interface for Eclipse"
arch=('any')
url="https://eclipse.org/mylyn/"
license=('EPL')
depends=('eclipse')
optdepends=('bugzilla: ticketing support')
source=(https://download.eclipse.org/tools/mylyn/update/mylyn-${pkgver}-e3.4.zip)
sha512sums=('aa6289046df4c254567010b30706cc9cb0a1355e9634adcb2052127030d2640f399caf20fce10e8b4fab5885da29057ab9117af42472bcc1645dcf9881f84236')

prepare() {
  # remove features and plug-ins containing sources
  rm -f features/*.source_*
  rm -f plugins/*.source_*
  # remove gz files
  rm -f plugins/*.pack.gz
}

package() {
  _dest="${pkgdir}/usr/lib/eclipse/dropins/${pkgname/eclipse-}/eclipse"

  # Features
  find features -type f | while read -r _feature ; do
    if [[ "${_feature}" =~ (.*\.jar$) ]] ; then
      install -dm755 "${_dest}/${_feature%*.jar}"
      cd "${_dest}/${_feature/.jar}"
      # extract features (otherwise they are not visible in about dialog)
      jar xf "${srcdir}/${_feature}" || return 1
    else
      install -Dm644 "${_feature}" "${_dest}/${_feature}"
    fi
  done

  # Plugins
  find plugins -type f | while read -r _plugin ; do
    install -Dm644 "${_plugin}" "${_dest}/${_plugin}"
  done
}

```

### Como personalizar a compilação

The main variable which needs to be customized is the `pkgname`. If you are packaging a typical plugin, then this is the only thing you need to do: most plugins are distributed in zip files which only contain the two `features` and `plugins` subdirectories. So, if you are packaging the `foo` plugin and the source file only contains the `features` and `plugins`, you just need to change `pkgname` to `eclipse-foo` and you are set.

Read on to get to the internals of the PKGBUILD, which help to understand how to setup the build for all the other cases.

### Revisão aprofundada do PKGBUILD

#### Nomenclatura de pacote

Packages should be named `eclipse-*pluginname*`, so that they are recognizable as Eclipse-related packages and it is easy to extract the plugin name with a simple shell substitution like `${pkgname/eclipse-}`, not having to resort to an unneeded `${_realname}` variable. The plugin name is necessary to tidy up everything during installation and to avoid conflicts.

#### Arquivos

##### Extração

Some plugins need the features to be extracted from jar files. The `jar` utility, already included in the JRE, is used to do this. However, `jar` cannot extract to directories other than the current one: this means that, after every directory creation, it is necessary to `cd` inside it before extracting. The `${_dest}` variable is used in this context to improve readability and PKGBUILD tidiness.

##### Localizações

As we said, source archives provide two directories, `features` and `plugins`, each one packed up with jar files. The preferred dropins structure should look like this:

```
/usr/lib/eclipse/dropins/pluginname/eclipse/features/feature1/...
/usr/lib/eclipse/dropins/pluginname/eclipse/features/feature2/...
/usr/lib/eclipse/dropins/pluginname/eclipse/plugins/plugin1.jar
/usr/lib/eclipse/dropins/pluginname/eclipse/plugins/plugin2.jar

```

This structure allows for mixing different versions of libraries that may be needed by different plugins while being clear about which package owns what. It will also avoid conflicts in case different packages provide the same library. The only alternative would be splitting every package from its libraries, with all the extra fuss it requires, and it would not even be guaranteed to work because of packages needing older library versions. Features have to be unjarred since Eclipse will not detect them otherwise, and the whole plugin installation will not work. This happens because Eclipse treats update sites and local installations differently (do not ask why, it just does).

#### A função build()

First thing to be noticed is the `cd ${srcdir}` command. Usually source archives extract the `features` and `plugins` folders directly under `${srcdir}`, but this is not always the case. Anyway, for most non-*(de facto)*-standard plugins this is the only line that needs to be changed.

Some released features include their sources, too. For a normal release version these sources are not needed and can be removed. Furthermore same features include `*.pack.gz` files, which contain the same files compared to the jar archives. So these files can be removed, too.

Next is the `features` section. It creates the necessary directories, one for every jar file, and extracts the jar in the corresponding directory. Similarly, the `plugins` section installs the jar files in their directory. A while cycle is used to prevent funny-named files.

## Solução de problemas

*   Sometimes cleaning of Eclipse helps to repair some problems: `$ eclipse -clean` 
*   If new installed plugins do not appear in Eclipse, try with a clean `~/.eclipse` directory, for example by renaming the existing one. Be aware that this will of course make all the user-installed plugins via Marketplace unavailable.