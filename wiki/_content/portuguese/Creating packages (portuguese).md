Esse artigo objetiva auxiliar usuários na criação de seus próprios pacotes usando o [sistema de compilação](/index.php/Arch_Build_System_(Portugu%C3%AAs) "Arch Build System (Português)") "tipo *ports*" do Arch Linux, também para enviou ao [AUR](/index.php/AUR_(Portugu%C3%AAs) "AUR (Português)"). Ele cobre criação de um [PKGBUILD](/index.php/PKGBUILD "PKGBUILD") – um arquivo de descrição de compilação de pacote carregado pelo `makepkg` para criar um pacote binário a partir do fonte. Se já estiver em posse de um `PKGBUILD`, veja [makepkg](/index.php/Makepkg_(Portugu%C3%AAs) "Makepkg (Português)"). Para instruções sobre regras e formas existentes para melhorar a qualidade de pacote, veja [Padrões de empacotamento do Arch](/index.php/Padr%C3%B5es_de_empacotamento_do_Arch "Padrões de empacotamento do Arch").

## Contents

*   [1 Visão Geral](#Vis.C3.A3o_Geral)
    *   [1.1 Pacotes e grupos meta](#Pacotes_e_grupos_meta)
*   [2 Preparação](#Prepara.C3.A7.C3.A3o)
    *   [2.1 Pré-requisito de software](#Pr.C3.A9-requisito_de_software)
    *   [2.2 Baixe e teste a instalação](#Baixe_e_teste_a_instala.C3.A7.C3.A3o)
*   [3 Criação de um PKGBUILD](#Cria.C3.A7.C3.A3o_de_um_PKGBUILD)
    *   [3.1 Definindo as variáveis do PKGBUILD](#Definindo_as_vari.C3.A1veis_do_PKGBUILD)
    *   [3.2 Funções do PKGBUILD](#Fun.C3.A7.C3.B5es_do_PKGBUILD)
        *   [3.2.1 prepare()](#prepare.28.29)
        *   [3.2.2 pkgver()](#pkgver.28.29)
        *   [3.2.3 build()](#build.28.29)
        *   [3.2.4 check()](#check.28.29)
        *   [3.2.5 package()](#package.28.29)
*   [4 Teste do PKGBUILD e pacote](#Teste_do_PKGBUILD_e_pacote)
    *   [4.1 Verificando sanidade do pacote](#Verificando_sanidade_do_pacote)
*   [5 Enviando pacotes para o AUR](#Enviando_pacotes_para_o_AUR)
*   [6 Resumo](#Resumo)
    *   [6.1 Avisos](#Avisos)
*   [7 Diretrizes mais detalhadas](#Diretrizes_mais_detalhadas)
*   [8 Veja também](#Veja_tamb.C3.A9m)

## Visão Geral

Pacotes no Arch Linux são compilados usando o utilitário [makepkg](/index.php/Makepkg_(Portugu%C3%AAs) "Makepkg (Português)") e as informações armazenadas em um arquivo [PKGBUILD](/index.php/PKGBUILD "PKGBUILD"). Quando `makepkg` é executado, ele pesquisa por um `PKGBUILD` no diretório atual e segue as instruções nele para obter os arquivos necessários e/ou compilá-los para serem empacotados dentro do arquivo de pacote (`pkgname.pkg.tar.xz`). O pacote resultante contém arquivos binários e instruções de instalação prontos para serem instalados pelo [pacman](/index.php/Pacman_(Portugu%C3%AAs) "Pacman (Português)").

Um pacote do Arch é nada mais que um pacote tar, ou "tarball", comprimido usando xz, que contém os seguintes arquivos gerados pelo makepkg:

*   Os arquivos binários para serem instalados.
*   `.PKGINFO`: contém todos os metadados necessários pelo pacman para lidar com pacotes, dependências, etc.
*   `.MTREE`: contém *hashes* e *timestamps* dos arquivos, que são incluídos na base de dados local de forma que o pacman possa verificar a integridade do pacote.
*   `.INSTALL`: um arquivo opcional usado para executar comandos após o estágio instalação/atualização/remoção. (Esse arquivo está presente apenas se especificado no `PKGBUILD`.)
*   `.Changelog`: um arquivo opcional mantido pelo mantenedor do pacote documentando as chances do pacote. (Ele não está presente em todos pacotes.)

### Pacotes e grupos meta

Um grupo de pacotes é um conjunto de pacotes relacionados, definido pelo empacotador, que pode ser instalado ou desinstalado simultaneamente usando o nome de grupo como um substituto para cada nome de pacote individual. Enquanto um grupo não é um pacote, ele pode ser instalado de forma similar a um pacote, veja [Pacman (Português)#Instalando grupos de pacotes](/index.php/Pacman_(Portugu%C3%AAs)#Instalando_grupos_de_pacotes "Pacman (Português)") e [PKGBUILD#groups](/index.php/PKGBUILD#groups "PKGBUILD").

Um pacote meta, frequentemente (mas nem sempre) intitulado com o sufixo *-meta*, fornece funcionalidade similar a um grupo de pacotes no sentido que ele permite múltiplos pacotes relacionados serem instalados ou desinstalados simultaneamente. Pacotes meta podem ser instalados como qualquer outro pacote, veja [Pacman (Português)#Instalando Pacotes específicos](/index.php/Pacman_(Portugu%C3%AAs)#Instalando_Pacotes_espec.C3.ADficos "Pacman (Português)"). A única diferença entre um pacote meta e um pacote comum é que um pacote meta é vazio e existe apenas para fazer um vínculo de pacotes relacionados por meio de dependências.

A vantagem de um pacote meta, comparado com um grupo, é que quaisquer novos pacotes membros serão instalados quando o pacote meta em si for atualizado com um novo conjunto de dependências. Isso é um contraste a um grupo em que novos membros de grupos não serão instalados automaticamente. A desvantagem de um pacote meta é que ele não é tão flexível quanto um grupo — você pode escolher quais membros do grupo você deseja instalar, mas não pode escolher qual dependência do pacote meta você deseja instalar. Da mesma forma, você pode desinstalar membros do grupo sem ter que remover todo o grupo, porém você não pode remover dependências de pacotes meta sem ter que desinstalar o pacote meta em si.

## Preparação

### Pré-requisito de software

First ensure that the necessary tools are installed. [Installing](/index.php/Install "Install") the package group [base-devel](https://www.archlinux.org/groups/x86_64/base-devel/) should be sufficient; it includes **make** and additional tools needed for compiling from source.

One of the key tools for building packages is [makepkg](/index.php/Makepkg "Makepkg") (provided by [pacman](https://www.archlinux.org/packages/?name=pacman)), which does the following:

1.  Checks if package dependencies are installed.
2.  Downloads the source file(s) from the specified server(s).
3.  Unpacks the source file(s).
4.  Compiles the software and installs it under a fakeroot environment.
5.  Strips symbols from binaries and libraries.
6.  Generates the package meta file which is included with each package.
7.  Compresses the fakeroot environment into a package file.
8.  Stores the package file in the configured destination directory, which is the present working directory by default.

### Baixe e teste a instalação

Download the source tarball of the software you want to package, extract it, and follow the author's steps to install the program. Make a note of all commands and/or steps needed to compile and install it. You will be repeating those same commands in the *PKGBUILD* file.

Most software authors stick to the 3-step build cycle:

```
./configure
make
make install

```

This is a good time to make sure the program is working correctly.

## Criação de um PKGBUILD

When you run `makepkg`, it will look for a `PKGBUILD` file in the present working directory. If a `PKGBUILD` file is found it will download the software's source code and compile it according to the instructions specified in the `PKGBUILD` file. The instructions must be fully interpretable by the [Bash](https://en.wikipedia.org/wiki/Bash_(Unix_shell) shell. After successful completion, the resulting binaries and metadata of the package, i.e. package version and dependencies, are packed in a `pkgname.pkg.tar.xz` package file that can be installed with `pacman -U *<package file>*`.

To begin with a new package, you should first create an empty working directory, (preferably `~/abs/**pkgname**`), change into that directory, and create a `PKGBUILD` file. You can either copy the prototype PKGBUILD `/usr/share/pacman/PKGBUILD.proto` to your working directory or copy a `PKGBUILD` from a similar package. The latter may be useful if you only need to change a few options.

**Warning:** Use only the PKGBUILD prototypes provided in the [pacman](https://www.archlinux.org/packages/?name=pacman) package (PKGBUILD-split.proto, PKGBUILD-vcs.proto and PKGBUILD.proto). The prototypes files in the [abs](https://www.archlinux.org/packages/?name=abs) package and in [the ABS git repository](https://projects.archlinux.org/abs.git/tree/prototypes) are significantly out of date and should not be used. See [FS#34485](https://bugs.archlinux.org/task/34485).

### Definindo as variáveis do PKGBUILD

Example PKGBUILDs are located in `/usr/share/pacman/`. An explanation of possible `PKGBUILD` variables can be found in the [PKGBUILD](/index.php/PKGBUILD "PKGBUILD") article.

*makepkg* defines two variables that you should use as part of the build and install process:

	`srcdir`

	This points to the directory where *makepkg* extracts or symlinks all files in the source array.

	`pkgdir`

	This points to the directory where *makepkg* bundles the installed package, which becomes the root directory of your built package.

All of them contain *absolute* paths, which means, you do not have to worry about your working directory if you use these variables properly.

**Note:** *makepkg*, and thus the `build()` and `package()` functions, are intended to be non-interactive. Interactive utilities or scripts called in those functions may break *makepkg*, particularly if it is invoked with build-logging enabled (`-L`). (See [FS#13214](https://bugs.archlinux.org/task/13214).)

**Note:** Apart from the current package Maintainer, there may be previous maintainers listed above as Contributors.

### Funções do PKGBUILD

There are five functions, listed here in the order they are executed if all of them exist. If one does not exist, it is simply skipped.

**Note:** This does not apply to the `package()` function, as it is required in every PKGBUILD

#### prepare()

This function, commands that are used to prepare sources for building are run, such as [patching](/index.php/Patching_in_ABS "Patching in ABS"). This function runs right after package extraction, before [pkgver()](#pkgver.28.29) and the build function. If extraction is skipped (`makepkg -e`), then `prepare()` is not run.

**Note:** (From `man PKGBUILD`) The function is run in `bash -e` mode, meaning any command that exits with a non-zero status will cause the function to exit.

#### pkgver()

`pkgver()` runs after the sources are fetched, extracted and [prepare()](#prepare.28.29) executed. So you can update the pkgver variable during a makepkg stage.

This is particularly useful if you are [making git/svn/hg/etc. packages](/index.php/VCS_PKGBUILD_Guidelines "VCS PKGBUILD Guidelines"), where the build process may remain the same, but the source could be updated every day, even every hour. The old way of doing this was to put the date into the pkgver field which, if the software was not updated, makepkg would still rebuild it thinking the version had changed. Some useful commands for this are `git describe`, `hg identify -ni`, etc. Please test these before submitting a PKGBUILD, as a failure in the `pkgver()` function can stop a build in its tracks.

**Note:** pkgver cannot contain spaces or hyphens (`-`). Using sed to correct this is common.

#### build()

Now you need to implement the `build()` function in the `PKGBUILD` file. This function uses common shell commands in [Bash](https://en.wikipedia.org/wiki/Bash_(Unix_shell) syntax to automatically compile software and create a `pkg` directory to install the software to. This allows *makepkg* to package files without having to sift through your file system.

The first step in the `build()` function is to change into the directory created by uncompressing the source tarball. *makepkg* will change the current directory to `$srcdir` before executing the `build()` function. Therefore, in most cases, like suggested in `/usr/share/pacman/PKGBUILD.proto`, the first command will look like this:

```
cd "$pkgname-$pkgver"

```

Now, you need to list the same commands you used when you manually compiled the software. The `build()` function in essence automates everything you did by hand and compiles the software in the fakeroot build environment. If the software you are packaging uses a configure script, it is good practice to use `--prefix=/usr` when building packages for pacman. A lot of software installs files relative to the `/usr/local` directory, which should only be done if you are manually building from source. All Arch Linux packages should use the `/usr` directory. As seen in the `/usr/share/pacman/PKGBUILD.proto` file, the next two lines often look like this:

```
./configure --prefix=/usr
make

```

**Note:** If your software does not need to build anything, DO NOT use the `build()` function. The `build()` function is not required, but the `package()` function is.

#### check()

Place for calls to `make check` and similar testing routines. It is highly recommended to have `check()` as it helps to make sure software has been built correctly and works fine with its dependencies.

Users who do not need it (and occasionally maintainers who can not fix a package for this to pass) can disable it using `BUILDENV+=('!check')` in PKGBUILD/makepkg.conf or call `makepkg` with `--nocheck` flag.

#### package()

The final step is to put the compiled files in a directory where *makepkg* can retrieve them to create a package. This by default is the `pkg` directory—a simple fakeroot environment. The `pkg` directory replicates the hierarchy of the root file system of the software's installation paths. If you have to manually place files under the root of your filesystem, you should install them in the `pkg` directory under the same directory structure. For example, if you want to install a file to `/usr/bin`, it should instead be placed under `$pkgdir/usr/bin`. Very few install procedures require the user to copy dozens of files manually. Instead, for most software, calling `make install` will do so. The final line should look like the following in order to correctly install the software in the `pkg` directory:

```
make DESTDIR="$pkgdir/" install

```

**Note:** It is sometimes the case where `DESTDIR` is not used in the `Makefile`; you may need to use `prefix` instead. If the package is built with *autoconf* / *automake*, use `DESTDIR`; this is what is [documented](https://www.gnu.org/software/automake/manual/automake.html#Install) in the manuals. If `DESTDIR` does not work, try building with `make prefix="$pkgdir/usr/" install`. If that does not work, you will have to look further into the install commands that are executed by "`make <...> install`".

In some odd cases, the software expects to be run from a single directory. In such cases, it is wise to simply copy these to `$pkgdir/opt`.

More often than not, the installation process of the software will create sub-directories below the `pkg` directory. If it does not, however, *makepkg* will generate a lot of errors and you will need to manually create sub-directories by adding the appropriate `mkdir -p` commands in the `build()` function before the installation procedure is run.

In old packages, there was no `package()` function. So, files were put into the *pkg* directory at the end of the `build()` function. If `package()` is not present, `build()` runs via *fakeroot*. In new packages, `package()` is required and runs via *fakeroot* instead, and `build()` runs without any special privileges.

`makepkg --repackage` runs only the `package()` function, so it creates a `*.pkg.*` file without compiling the package. This may save time e.g. if you just have changed the `depends` variable of the package.

**Note:** The `package()` function is the only required function in a PKGBUILD. If you must only copy files into their respective directories to install a program, do not put it in the `build()` function, put that in the `package()` function.

**Note:** Creating symlinks is a slightly awkward process in the `package()` function. Using the naive approach `ln -s "${pkgdir}/from/foo" "${pkgdir}/to/goo"` will result in a broken symlink to the build directory. The way to create a proper link is to create it pointing to an initially-broken source, `ln -s "/from/foo" "${pkgdir}/to/goo"`. Once the package is installed, the link will point to the right place.

## Teste do PKGBUILD e pacote

As you are writing the `build()` function, you will want to test your changes frequently to ensure there are no bugs. You can do this using the `makepkg` command in the directory containing the `PKGBUILD` file. With a properly formatted `PKGBUILD`, makepkg will create a package; with a broken or unfinished `PKGBUILD`, it will raise an error.

If makepkg finishes successfully, it will place a file named `pkgname-pkgver.pkg.tar.xz` in your working directory. This package can be installed with the `pacman -U` command. However, just because a package file was built does not imply that it is fully functional. It might conceivably contain only the directory and no files whatsoever if, for example, a prefix was specified improperly. You can use pacman's query functions to display a list of files contained in the package and the dependencies it requires with `pacman -Qlp [package file]` and `pacman -Qip [package file]` respectively.

If the package looks sane, then you are done! However, if you plan on releasing the `PKGBUILD` file, it is imperative that you check and double-check the contents of the `depends` array.

Also ensure that the package binaries actually *run* flawlessly! It is annoying to release a package that contains all necessary files, but crashes because of some obscure configuration option that does not quite work well with the rest of the system. If you are only going to compile packages for your own system, though, you do not need to worry too much about this quality assurance step, as you are the only person suffering from mistakes, after all.

### Verificando sanidade do pacote

After testing package functionality check it for errors using [namcap](/index.php/Namcap "Namcap"):

```
$ namcap PKGBUILD
$ namcap *<package file name>*.pkg.tar.xz

```

Namcap will:

1.  Check PKGBUILD contents for common errors and package file hierarchy for unnecessary/misplaced files
2.  Scan all ELF files in package using `ldd`, automatically reporting which packages with required shared libraries are missing from `depends` and which can be omitted as transitive dependencies
3.  Heuristically search for missing and redundant dependencies

and much more. Get into the habit of checking your packages with namcap to avoid having to fix the simplest mistakes after package submission.

## Enviando pacotes para o AUR

Please read [AUR User Guidelines#Submitting packages](/index.php/AUR_User_Guidelines#Submitting_packages "AUR User Guidelines") for a detailed description of the submission process.

## Resumo

1.  Download the source tarball of the software you want to package.
2.  Try compiling the package and installing it into an arbitrary directory.
3.  Copy over the prototype `/usr/share/pacman/PKGBUILD.proto` and rename it to `PKGBUILD` in a temporary working directory -- preferably `~/abs/`.
4.  Edit the `PKGBUILD` according to the needs of your package.
5.  Run `makepkg` and see whether the resulting package is built correctly.
6.  If not, repeat the last two steps.

### Avisos

*   Before you can automate the package building process, you should have done it manually at least once unless you know *exactly* what you are doing *in advance*, in which case you would not be reading this in the first place. Unfortunately, although a good bunch of program authors stick to the 3-step build cycle of "`./configure`; `make`; `make install`", this is not always the case, and things can get real ugly if you have to apply patches to make everything work at all. Rule of thumb: If you cannot get the program to compile from the source tarball, and make it install itself to a defined, temporary subdirectory, you do not even need to try packaging it. There is not any magic pixie dust in `makepkg` that makes source problems go away.
*   In a few cases, the packages are not even available as source and you have to use something like `sh installer.run` to get it to work. You will have to do quite a bit of research (read READMEs, INSTALL instructions, man pages, perhaps ebuilds from Gentoo or other package installers, possibly even the MAKEFILEs or source code) to get it working. In some really bad cases, you have to edit the source files to get it to work at all. However, `makepkg` needs to be completely autonomous, with no user input. Therefore if you need to edit the makefiles, you may have to bundle a custom patch with the `PKGBUILD` and install it from inside the `prepare()` function, or you might have to issue some `sed` commands from inside the `prepare()` function.

## Diretrizes mais detalhadas

**[Package creation guidelines](/index.php/Creating_packages "Creating packages")**

* * *

[CLR](/index.php/CLR_package_guidelines "CLR package guidelines") – [Cross](/index.php/Cross-compiling_tools_package_guidelines "Cross-compiling tools package guidelines") – [Eclipse](/index.php/Eclipse_plugin_package_guidelines "Eclipse plugin package guidelines") – [Free Pascal](/index.php/Free_Pascal_package_guidelines "Free Pascal package guidelines") – [GNOME](/index.php/GNOME_package_guidelines "GNOME package guidelines") – [Go](/index.php/Go_package_guidelines "Go package guidelines") – [Haskell](/index.php/Haskell_package_guidelines "Haskell package guidelines") – [Java](/index.php/Java_package_guidelines "Java package guidelines") – [KDE](/index.php/KDE_package_guidelines "KDE package guidelines") – [Kernel](/index.php/Kernel_module_package_guidelines "Kernel module package guidelines") – [Lisp](/index.php/Lisp_package_guidelines "Lisp package guidelines") – [MinGW](/index.php/MinGW_package_guidelines "MinGW package guidelines") – [Node.js](/index.php/Node.js_package_guidelines "Node.js package guidelines") – [Nonfree](/index.php/Nonfree_applications_package_guidelines "Nonfree applications package guidelines") – [OCaml](/index.php/OCaml_package_guidelines "OCaml package guidelines") – [Perl](/index.php/Perl_package_guidelines "Perl package guidelines") – [PHP](/index.php/PHP_package_guidelines "PHP package guidelines") – [Python](/index.php/Python_package_guidelines "Python package guidelines") – [Ruby](/index.php/Ruby_Gem_package_guidelines "Ruby Gem package guidelines") – [VCS](/index.php/VCS_package_guidelines "VCS package guidelines") – [Web](/index.php/Web_application_package_guidelines "Web application package guidelines") – [Wine](/index.php/Wine_package_guidelines "Wine package guidelines")

## Veja também

*   [How to correctly create a patch file](https://bbs.archlinux.org/viewtopic.php?id=91408).
*   [Arch Linux Classroom IRC Logs of classes about creating PKGBUILDs](https://archwomen.org/media/project_classroom/classlogs/).
*   [Fakeroot approach for package installation](http://www.linuxfromscratch.org/hints/downloads/files/fakeroot.txt)