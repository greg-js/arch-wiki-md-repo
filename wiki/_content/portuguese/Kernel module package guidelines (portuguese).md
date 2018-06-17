**[Diretrizes de criação de pacotes](/index.php/Criando_pacotes "Criando pacotes")**

* * *

[CLR](/index.php/Diretrizes_de_pacotes_CLR "Diretrizes de pacotes CLR") – [Cross](/index.php/Diretrizes_de_pacotes_de_ferramentas_de_compila%C3%A7%C3%A3o_cruzada "Diretrizes de pacotes de ferramentas de compilação cruzada") – [Eclipse](/index.php/Diretrizes_de_pacotes_de_plugin_do_Eclipse "Diretrizes de pacotes de plugin do Eclipse") – [Free Pascal](/index.php/Diretrizes_de_pacotes_Free_Pascal "Diretrizes de pacotes Free Pascal") – [GNOME](/index.php/Diretrizes_de_pacotes_GNOME "Diretrizes de pacotes GNOME") – [Go](/index.php/Diretrizes_de_pacotes_Go "Diretrizes de pacotes Go") – [Haskell](/index.php/Diretrizes_de_pacotes_Haskell "Diretrizes de pacotes Haskell") – [Java](/index.php/Diretrizes_de_pacotes_Java "Diretrizes de pacotes Java") – [KDE](/index.php/Diretrizes_de_pacotes_KDE "Diretrizes de pacotes KDE") – [Kernel](/index.php/Diretrizes_de_pacotes_de_m%C3%B3dulos_de_kernel "Diretrizes de pacotes de módulos de kernel") – [Lisp](/index.php/Diretrizes_de_pacotes_Lisp "Diretrizes de pacotes Lisp") – [MinGW](/index.php/Diretrizes_de_pacotes_MinGW "Diretrizes de pacotes MinGW") – [Node.js](/index.php/Diretrizes_de_pacotes_Node.js "Diretrizes de pacotes Node.js") – [Nonfree](/index.php/Diretrizes_de_pacotes_de_aplicativos_n%C3%A3o_livres "Diretrizes de pacotes de aplicativos não livres") –[OCaml](/index.php/Diretrizes_de_pacotes_OCaml "Diretrizes de pacotes OCaml") – [Perl](/index.php/Diretrizes_de_pacotes_Perl "Diretrizes de pacotes Perl") – [PHP](/index.php/Diretrizes_de_pacotes_PHP "Diretrizes de pacotes PHP") – [Python](/index.php/Diretrizes_de_pacotes_Python "Diretrizes de pacotes Python") – [Ruby](/index.php/Diretrizes_de_pacotes_Ruby_Gem "Diretrizes de pacotes Ruby Gem") – [VCS](/index.php/Diretrizes_de_pacotes_VCS "Diretrizes de pacotes VCS") – [Web](/index.php/Diretrizes_de_pacotes_de_aplicativos_da_Web "Diretrizes de pacotes de aplicativos da Web") – [Wine](/index.php/Diretrizes_de_pacotes_Wine "Diretrizes de pacotes Wine")

## Contents

*   [1 Separação de pacote](#Separa.C3.A7.C3.A3o_de_pacote)
    *   [1.1 Diretrizes](#Diretrizes)
    *   [1.2 Motivos](#Motivos)
*   [2 Colocação de arquivos](#Coloca.C3.A7.C3.A3o_de_arquivos)

## Separação de pacote

Packages that contain [kernel modules](/index.php/Kernel_modules "Kernel modules") should be treated specially, to support users who wish to have more than one kernel installed on a system.

When packaging software containing a kernel module and other non-module supporting files/utilities, it is important to separate the kernel modules from the supporting files.

### Diretrizes

When packaging such software (using the [NVIDIA](/index.php/NVIDIA "NVIDIA") drivers as an example) the convention is:

*   create an `nvidia` package containing just the kernel modules built for the vanilla kernel
*   create an `nvidia-utils` package containing the supporting files
*   make sure `nvidia` depends on `nvidia-utils` (unless there's a good reason not to do so)
*   for another kernel like `kernel26-mm`, create `nvidia-mm` containing the kernel modules built against that kernel which provides nvidia and also depends on `nvidia-utils`
*   make sure `nvidia` depends on the current major kernel version, for example:

```
depends=('kernel26>=2.6.24-2' 'kernel26<2.6.25-0' 'nvidia-utils')

```

Note that it is `2.6.24-2`, not `-1` in above example - this is because there was a configuration change to important kernel subsystem that required all modules to be rebuilt. You should always change depends version in such cases, otherwise some people with out-of-sync kernel and module version will report that module is broken.

### Motivos

While kernel modules built for different kernels always live in different directories and can peacefully coexist, the supporting files are expected to be found in one location. If one package contained module and supporting files, you would be unable to install the modules for more than one kernel because the supporting files in the packages would cause pacman file conflicts.

The separation of modules and accompanying files allows multiple kernel module packages to be installed for multiple kernels on the same system while sharing the supporting files among them in the expected location.

## Colocação de arquivos

If a package includes a kernel module that is meant to override an existing module of the same name, such module should be placed in the `/lib/modules/2.6.xx-ARCH/updates` directory. When **depmod** is run, modules in this directory will take precedence.