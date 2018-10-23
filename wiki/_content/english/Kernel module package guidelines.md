**[Package creation guidelines](/index.php/Arch_packaging_standards "Arch packaging standards")**

* * *

[CLR](/index.php/CLR_package_guidelines "CLR package guidelines") – [Cross](/index.php/Cross-compiling_tools_package_guidelines "Cross-compiling tools package guidelines") – [Eclipse](/index.php/Eclipse_plugin_package_guidelines "Eclipse plugin package guidelines") – [Free Pascal](/index.php/Free_Pascal_package_guidelines "Free Pascal package guidelines") – [GNOME](/index.php/GNOME_package_guidelines "GNOME package guidelines") – [Go](/index.php/Go_package_guidelines "Go package guidelines") – [Haskell](/index.php/Haskell_package_guidelines "Haskell package guidelines") – [Java](/index.php/Java_package_guidelines "Java package guidelines") – [KDE](/index.php/KDE_package_guidelines "KDE package guidelines") – <a class="mw-selflink selflink">Kernel</a> – [Lisp](/index.php/Lisp_package_guidelines "Lisp package guidelines") – [MinGW](/index.php/MinGW_package_guidelines "MinGW package guidelines") – [Node.js](/index.php/Node.js_package_guidelines "Node.js package guidelines") – [Nonfree](/index.php/Nonfree_applications_package_guidelines "Nonfree applications package guidelines") – [OCaml](/index.php/OCaml_package_guidelines "OCaml package guidelines") – [Perl](/index.php/Perl_package_guidelines "Perl package guidelines") – [PHP](/index.php/PHP_package_guidelines "PHP package guidelines") – [Python](/index.php/Python_package_guidelines "Python package guidelines") – [R](/index.php/R_package_guidelines "R package guidelines") – [Ruby](/index.php/Ruby_Gem_package_guidelines "Ruby Gem package guidelines") – [VCS](/index.php/VCS_package_guidelines "VCS package guidelines") – [Web](/index.php/Web_application_package_guidelines "Web application package guidelines") – [Wine](/index.php/Wine_package_guidelines "Wine package guidelines")

## Contents

*   [1 Package separation](#Package_separation)
    *   [1.1 Guidelines](#Guidelines)
    *   [1.2 Rationale](#Rationale)
*   [2 File placement](#File_placement)

## Package separation

Packages that contain [kernel modules](/index.php/Kernel_modules "Kernel modules") should be treated specially, to support users who wish to have more than one kernel installed on a system.

When packaging software containing a kernel module and other non-module supporting files/utilities, it is important to separate the kernel modules from the supporting files.

### Guidelines

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

### Rationale

While kernel modules built for different kernels always live in different directories and can peacefully coexist, the supporting files are expected to be found in one location. If one package contained module and supporting files, you would be unable to install the modules for more than one kernel because the supporting files in the packages would cause pacman file conflicts.

The separation of modules and accompanying files allows multiple kernel module packages to be installed for multiple kernels on the same system while sharing the supporting files among them in the expected location.

## File placement

If a package includes a kernel module that is meant to override an existing module of the same name, such module should be placed in the `/lib/modules/2.6.xx-ARCH/updates` directory. When **depmod** is run, modules in this directory will take precedence.