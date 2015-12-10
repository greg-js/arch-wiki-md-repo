# Eclipse plugin package guidelines

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

**[Package creation guidelines](/index.php/Creating_packages "Creating packages")**

* * *

[CLR](/index.php/CLR_package_guidelines "CLR package guidelines") – [Cross](/index.php/Cross-compiling_tools_package_guidelines "Cross-compiling tools package guidelines") – **Eclipse** – [Free Pascal](/index.php/Free_Pascal_package_guidelines "Free Pascal package guidelines") – [GNOME](/index.php/GNOME_package_guidelines "GNOME package guidelines") – [Go](/index.php/Go_package_guidelines "Go package guidelines") – [Haskell](/index.php/Haskell_package_guidelines "Haskell package guidelines") – [Java](/index.php/Java_package_guidelines "Java package guidelines") – [KDE](/index.php/KDE_package_guidelines "KDE package guidelines") – [Kernel](/index.php/Kernel_module_package_guidelines "Kernel module package guidelines") – [Lisp](/index.php/Lisp_package_guidelines "Lisp package guidelines") – [MinGW](/index.php/MinGW_package_guidelines "MinGW package guidelines") – [Nonfree](/index.php/Nonfree_applications_package_guidelines "Nonfree applications package guidelines") – [OCaml](/index.php/OCaml_package_guidelines "OCaml package guidelines") – [Perl](/index.php/Perl_package_guidelines "Perl package guidelines") – [PHP](/index.php/PHP_package_guidelines "PHP package guidelines") – [Python](/index.php/Python_package_guidelines "Python package guidelines") – [Ruby](/index.php/Ruby_Gem_package_guidelines "Ruby Gem package guidelines") – [VCS](/index.php/VCS_package_guidelines "VCS package guidelines") – [Web](/index.php/Web_application_package_guidelines "Web application package guidelines") – [Wine](/index.php/Wine_package_guidelines "Wine package guidelines")

There are many ways to install working [Eclipse](/index.php/Eclipse "Eclipse") plugins, especially since the introduction of the _dropins_ directory in Eclipse 3.4, but some of them are messy, and having a standardized and consistent way of packaging is very important to lead to a clean system structure. It's not easy, however, to achieve this without the packager knowing every detail about how Eclipse plugins work. This page aims to define a standard and simple structure for Eclipse plugin [PKGBUILDs](/index.php/PKGBUILD "PKGBUILD"), so that the filesystem structure can remain consistent between all plugins without having the packager to start again for every new package.

## Contents

*   [1 Eclipse plugin structure and installation](#Eclipse_plugin_structure_and_installation)
*   [2 Packaging](#Packaging)
    *   [2.1 Sample PKGBUILD](#Sample_PKGBUILD)
    *   [2.2 How to customize the build](#How_to_customize_the_build)
    *   [2.3 In-depth PKGBUILD review](#In-depth_PKGBUILD_review)
        *   [2.3.1 Package naming](#Package_naming)
        *   [2.3.2 Files](#Files)
            *   [2.3.2.1 Extraction](#Extraction)
            *   [2.3.2.2 Locations](#Locations)
        *   [2.3.3 The build() function](#The_build.28.29_function)

## Eclipse plugin structure and installation

The typical Eclipse plugin contains two directories, `features` and `plugins`, and since Eclipse 3.3 they could only be placed in `/usr/lib/eclipse/`. The content of these two directories could be mixed with that of other plugins, and it created a mess and rendered the structure difficult to manage. It was also very difficult to tell at a glance which package contained which file.

This installation method is still supported in Eclipse 3.4, but the preferred one is now using the `/usr/lib/eclipse/dropins/` directory. Inside this directory can live an unlimited number of subdirectories, each one containing its own `features` and `plugins` subdirectories. This allows to keep a tidy and clean structure, and should be the standard packaging way.

## Packaging

### Sample PKGBUILD

Here is an example, we will detail how to customize it below.

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

### How to customize the build

The main variable which needs to be customized is the `pkgname`. If you are packaging a typical plugin, then this is the only thing you need to do: most plugins are distributed in zip files which only contain the two `features` and `plugins` subdirectories. So, if you are packaging the `foo` plugin and the source file only contains the `features` and `plugins`, you just need to change `pkgname` to `eclipse-foo` and you are set.

Read on to get to the internals of the PKGBUILD, which help to understand how to setup the build for all the other cases.

### In-depth PKGBUILD review

#### Package naming

Packages should be named `eclipse-_pluginname_`, so that they are recognizable as Eclipse-related packages and it is easy to extract the plugin name with a simple shell substitution like `${pkgname/eclipse-}`, not having to resort to an unneeded `${_realname}` variable. The plugin name is necessary to tidy up everything during installation and to avoid conflicts.

#### Files

##### Extraction

Some plugins need the features to be extracted from jar files. The `jar` utility, already included in the JRE, is used to do this. However, `jar` cannot extract to directories other than the current one: this means that, after every directory creation, it is necessary to `cd` inside it before extracting. The `${_dest}` variable is used in this context to improve readability and PKGBUILD tidiness.

##### Locations

As we said, source archives provide two directories, `features` and `plugins`, each one packed up with jar files. The preferred dropins structure should look like this:

```
/usr/lib/eclipse/dropins/pluginname/eclipse/features/feature1/...
/usr/lib/eclipse/dropins/pluginname/eclipse/features/feature2/...
/usr/lib/eclipse/dropins/pluginname/eclipse/plugins/plugin1.jar
/usr/lib/eclipse/dropins/pluginname/eclipse/plugins/plugin2.jar

```

This structure allows for mixing different versions of libraries that may be needed by different plugins while being clear about which package owns what. It will also avoid conflicts in case different packages provide the same library. The only alternative would be splitting every package from its libraries, with all the extra fuss it requires, and it would not even be guaranteed to work because of packages needing older library versions. Features have to be unjarred since Eclipse will not detect them otherwise, and the whole plugin installation will not work. This happens because Eclipse treats update sites and local installations differently (do not ask why, it just does).

#### The build() function

First thing to be noticed is the `cd ${srcdir}` command. Usually source archives extract the `features` and `plugins` folders directly under `${srcdir}`, but this is not always the case. Anyway, for most non-_(de facto)_-standard plugins this is the only line that needs to be changed.

Some released features include their sources, too. For a normal release version these sources are not needed and can be removed. Furthermore same features include `*.pack.gz` files, which contain the same files compared to the jar archives. So these files can be removed, too.

Next is the `features` section. It creates the necessary directories, one for every jar file, and extracts the jar in the corresponding directory. Similarly, the `plugins` section installs the jar files in their directory. A while cycle is used to prevent funny-named files.

Retrieved from "[https://wiki.archlinux.org/index.php?title=Eclipse_plugin_package_guidelines&oldid=405205](https://wiki.archlinux.org/index.php?title=Eclipse_plugin_package_guidelines&oldid=405205)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [Package development](/index.php/Category:Package_development "Category:Package development")