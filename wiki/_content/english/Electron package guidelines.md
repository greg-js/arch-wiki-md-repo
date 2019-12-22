**[Package creation guidelines](/index.php/Arch_packaging_standards "Arch packaging standards")**

* * *

[32-bit](/index.php/32-bit_package_guidelines "32-bit package guidelines") – [CLR](/index.php/CLR_package_guidelines "CLR package guidelines") – [Cross](/index.php/Cross-compiling_tools_package_guidelines "Cross-compiling tools package guidelines") – [Eclipse](/index.php/Eclipse_plugin_package_guidelines "Eclipse plugin package guidelines") – <a class="mw-selflink selflink">Electron</a> – [Free Pascal](/index.php/Free_Pascal_package_guidelines "Free Pascal package guidelines") – [GNOME](/index.php/GNOME_package_guidelines "GNOME package guidelines") – [Go](/index.php/Go_package_guidelines "Go package guidelines") – [Haskell](/index.php/Haskell_package_guidelines "Haskell package guidelines") – [Java](/index.php/Java_package_guidelines "Java package guidelines") – [KDE](/index.php/KDE_package_guidelines "KDE package guidelines") – [Kernel](/index.php/Kernel_module_package_guidelines "Kernel module package guidelines") – [Lisp](/index.php/Lisp_package_guidelines "Lisp package guidelines") – [MinGW](/index.php/MinGW_package_guidelines "MinGW package guidelines") – [Node.js](/index.php/Node.js_package_guidelines "Node.js package guidelines") – [Nonfree](/index.php/Nonfree_applications_package_guidelines "Nonfree applications package guidelines") – [OCaml](/index.php/OCaml_package_guidelines "OCaml package guidelines") – [Perl](/index.php/Perl_package_guidelines "Perl package guidelines") – [PHP](/index.php/PHP_package_guidelines "PHP package guidelines") – [Python](/index.php/Python_package_guidelines "Python package guidelines") – [R](/index.php/R_package_guidelines "R package guidelines") – [Ruby](/index.php/Ruby_Gem_package_guidelines "Ruby Gem package guidelines") – [Rust](/index.php/Rust_package_guidelines "Rust package guidelines") – [VCS](/index.php/VCS_package_guidelines "VCS package guidelines") – [Web](/index.php/Web_application_package_guidelines "Web application package guidelines") – [Wine](/index.php/Wine_package_guidelines "Wine package guidelines")

This document covers standards and guidelines on writing [PKGBUILDs](/index.php/PKGBUILD "PKGBUILD") for [Electron](/index.php/Electron "Electron").

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Using the system electron](#Using_the_system_electron)
    *   [1.1 Building compiled extensions against the system electron](#Building_compiled_extensions_against_the_system_electron)
    *   [1.2 Using electron-builder with system electron](#Using_electron-builder_with_system_electron)
*   [2 Architecture](#Architecture)
*   [3 Directory structure](#Directory_structure)

## Using the system electron

Arch Linux provides global [electron](https://www.archlinux.org/packages/?name=electron) and [electron2](https://www.archlinux.org/packages/?name=electron2) packages that can be used to run an electron application via a shellscript wrapper:

```
#!/bin/sh

exec electron /path/to/*appname*/ "$@"
```

The `*appname*/` directory, or alternatively a file bundle called `*appname*.asar`, can be found in a prebuilt electron application as the `resources/app/` folder (or `resources/app.asar`). Everything else is just a copy of the electron runtime and can be removed from the final package.

### Building compiled extensions against the system electron

Some electron applications have compiled native extensions which link to the electron runtime, and must be built using the correct electron version. Since npm/yarn will always build against a private prebuilt copy of electron, patch the electron dependency from `package.json` to reference the same version as the system electron dependency. The build system will download the prebuilt copy it requires, compile the native extensions, and package everything into a final distribution, but this can be pruned during the `package()` step as usual.

Alternatively, you can remove the electron dependency from `package.json` and set the correct environment variables before running npm:

```
export npm_config_target=$(tail /usr/lib/electron/version)
export npm_config_arch=x64
export npm_config_target_arch=x64
export npm_config_disturl=[https://atom.io/download/electron](https://atom.io/download/electron)
export npm_config_runtime=electron
export npm_config_build_from_source=true
HOME="$srcdir/.electron-gyp" npm install

```

Set `HOME` to a path inside the `$srcdir` so the build process doesn't place any files in your real `HOME` directory. Make sure to adjust the path for all further commands that make use of the `.electron-gyp` cache.

(more details [here](https://electronjs.org/docs/tutorial/using-native-node-modules)).

### Using electron-builder with system electron

Many projects use **electron-builder** to build and package the Javascript file and Electron binaries. By default electron-builder downloads the entire electron version that is defined in the package management file (e.g. `package.json`). This might not be desired if you want to use the system electron and save the bandwidth since you're going to throw away the electron binaries anyway. The electron-builder provides the configurations `electronDist` and `electronVersion`, to specify a custom path of Electron and the version the application is packaged for respectively.

Find the electron-builder configuration file (e.g. `electron-builder.json`) and add the following settings:

*   `electronDist` to `/usr/lib/electron` for [electron](https://www.archlinux.org/packages/?name=electron) or `/usr/lib/electron2` for [electron2](https://www.archlinux.org/packages/?name=electron2)
*   `electronVersion` to the contents of `/usr/lib/electron/version` without the leading `v`

Packages that apply this: [rocketchat-desktop](https://aur.archlinux.org/packages/rocketchat-desktop/) [ubports-installer-git](https://aur.archlinux.org/packages/ubports-installer-git/)

[electron-builder configuration](https://www.electron.build/configuration/configuration)

Alternatively you can use the CLI to change/add these settings like this:

```
./node_modules/.bin/electron-builder --linux --x64 --dir $dist -c.electronDist=$electronDist -c.electronVersion=$electronVer

```

Note that you have to specify all these options or it wont work.

Packages that apply this: [deezloader-remix-git](https://aur.archlinux.org/packages/deezloader-remix-git/)

## Architecture

See [PKGBUILD#arch](/index.php/PKGBUILD#arch "PKGBUILD").

An Electron package that contains compiled native extensions is architecture-dependent. Otherwise it is most likely architecture-independent.

If the package contains a prebuilt copy of electron, it is always architecture-dependent.

## Directory structure

If the package is architecture-dependent, install the `resources/app/` directory to `/usr/lib/*appname*/`. Otherwise use `/usr/share/*appname*/`.

If the package contains a prebuilt copy of electron, copy the final distribution in its entirety to `/opt/*appname*`.