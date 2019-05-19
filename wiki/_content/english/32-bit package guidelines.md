**[Package creation guidelines](/index.php/Arch_packaging_standards "Arch packaging standards")**

* * *

<a class="mw-selflink selflink">32-bit</a> – [CLR](/index.php/CLR_package_guidelines "CLR package guidelines") – [Cross](/index.php/Cross-compiling_tools_package_guidelines "Cross-compiling tools package guidelines") – [Eclipse](/index.php/Eclipse_plugin_package_guidelines "Eclipse plugin package guidelines") – [Electron](/index.php/Electron_package_guidelines "Electron package guidelines") – [Free Pascal](/index.php/Free_Pascal_package_guidelines "Free Pascal package guidelines") – [GNOME](/index.php/GNOME_package_guidelines "GNOME package guidelines") – [Go](/index.php/Go_package_guidelines "Go package guidelines") – [Haskell](/index.php/Haskell_package_guidelines "Haskell package guidelines") – [Java](/index.php/Java_package_guidelines "Java package guidelines") – [KDE](/index.php/KDE_package_guidelines "KDE package guidelines") – [Kernel](/index.php/Kernel_module_package_guidelines "Kernel module package guidelines") – [Lisp](/index.php/Lisp_package_guidelines "Lisp package guidelines") – [MinGW](/index.php/MinGW_package_guidelines "MinGW package guidelines") – [Node.js](/index.php/Node.js_package_guidelines "Node.js package guidelines") – [Nonfree](/index.php/Nonfree_applications_package_guidelines "Nonfree applications package guidelines") – [OCaml](/index.php/OCaml_package_guidelines "OCaml package guidelines") – [Perl](/index.php/Perl_package_guidelines "Perl package guidelines") – [PHP](/index.php/PHP_package_guidelines "PHP package guidelines") – [Python](/index.php/Python_package_guidelines "Python package guidelines") – [R](/index.php/R_package_guidelines "R package guidelines") – [Ruby](/index.php/Ruby_Gem_package_guidelines "Ruby Gem package guidelines") – [Rust](/index.php/Rust_package_guidelines "Rust package guidelines") – [VCS](/index.php/VCS_package_guidelines "VCS package guidelines") – [Web](/index.php/Web_application_package_guidelines "Web application package guidelines") – [Wine](/index.php/Wine_package_guidelines "Wine package guidelines")

Legacy [32-bit](https://en.wikipedia.org/wiki/32-bit "wikipedia:32-bit") software can be built and installed on machines of another native architecture, such as [x86_64](https://en.wikipedia.org/wiki/x86_64 "wikipedia:x86 64"). This article explains the production and conventions of such packages.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Package naming](#Package_naming)
*   [2 Variables and parameters](#Variables_and_parameters)
    *   [2.1 lib32](#lib32)
        *   [2.1.1 File placement](#File_placement)
    *   [2.2 x32](#x32)

## Package naming

*   Prefix [32-bit versions](https://aur.archlinux.org/packages/?O=0&K=lib32-) of native packages with [lib32-](#lib32).

*   Suffix [packages](https://aur.archlinux.org/packages/?O=0&K=-x32) that utilize the [x32 ABI](https://en.wikipedia.org/wiki/x32_ABI "wikipedia:x32 ABI") with [-x32](#x32).

*   [Package decriptions](/index.php/PKGBUILD#pkgdesc "PKGBUILD") should distinguish these from native counterparts, ie `pkgdesc+=" (32-bit)"`.

## Variables and parameters

### lib32

Specify these [bash](/index.php/Bash "Bash") variables in a [PKGBUILD](/index.php/PKGBUILD "PKGBUILD") to tell the compiler to output 32-bit code:

```
export CFLAGS+=" -m32"
export CXXFLAGS+=" -m32"
export LDFLAGS+=" -m32"
export PKG_CONFIG_PATH='/usr/lib32/pkgconfig'

```

#### File placement

Ensure lib32 package files do not conflict with native package files and include all necessary files, such as architecture-specific includes. For example, if a package builds using [GNU Autoconf](https://en.wikipedia.org/wiki/Autoconf "wikipedia:Autoconf"), specify the following to `configure`:

```
--program-suffix="-32" \
--lib{exec,}dir=/usr/lib32 \
--includedir=/usr/include/"$pkgbase"32 \ 
--build=i686-pc-linux-gnu

```

### x32