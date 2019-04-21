**[Package creation guidelines](/index.php/Arch_packaging_standards "Arch packaging standards")**

* * *

[CLR](/index.php/CLR_package_guidelines "CLR package guidelines") – [Cross](/index.php/Cross-compiling_tools_package_guidelines "Cross-compiling tools package guidelines") – [Eclipse](/index.php/Eclipse_plugin_package_guidelines "Eclipse plugin package guidelines") – [Electron](/index.php/Electron_package_guidelines "Electron package guidelines") – [Free Pascal](/index.php/Free_Pascal_package_guidelines "Free Pascal package guidelines") – [GNOME](/index.php/GNOME_package_guidelines "GNOME package guidelines") – [Go](/index.php/Go_package_guidelines "Go package guidelines") – [Haskell](/index.php/Haskell_package_guidelines "Haskell package guidelines") – [Java](/index.php/Java_package_guidelines "Java package guidelines") – [KDE](/index.php/KDE_package_guidelines "KDE package guidelines") – [Kernel](/index.php/Kernel_module_package_guidelines "Kernel module package guidelines") – [Lisp](/index.php/Lisp_package_guidelines "Lisp package guidelines") – [MinGW](/index.php/MinGW_package_guidelines "MinGW package guidelines") – [Node.js](/index.php/Node.js_package_guidelines "Node.js package guidelines") – [Nonfree](/index.php/Nonfree_applications_package_guidelines "Nonfree applications package guidelines") – [OCaml](/index.php/OCaml_package_guidelines "OCaml package guidelines") – [Perl](/index.php/Perl_package_guidelines "Perl package guidelines") – [PHP](/index.php/PHP_package_guidelines "PHP package guidelines") – [Python](/index.php/Python_package_guidelines "Python package guidelines") – [R](/index.php/R_package_guidelines "R package guidelines") – [Ruby](/index.php/Ruby_Gem_package_guidelines "Ruby Gem package guidelines") – <a class="mw-selflink selflink">Rust</a> – [VCS](/index.php/VCS_package_guidelines "VCS package guidelines") – [Web](/index.php/Web_application_package_guidelines "Web application package guidelines") – [Wine](/index.php/Wine_package_guidelines "Wine package guidelines")

This document covers standards and guidelines on writing [PKGBUILDs](/index.php/PKGBUILD "PKGBUILD") for [Rust](/index.php/Rust "Rust").

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 General guidelines](#General_guidelines)
    *   [1.1 Package naming](#Package_naming)
*   [2 Building](#Building)
*   [3 Check](#Check)
*   [4 Package](#Package)

## General guidelines

### Package naming

For [Rust](/index.php/Rust "Rust") binaries use only the program name.

**Note:** The package name should be entirely lowercase.

## Building

Building a Rust package.

```
 build() {
   cargo build --release --locked
 }

```

where:

*   `--release` tells *cargo* to compile a release build
*   `--locked` tells *cargo* to adhere the `Cargo.lock` file and prevent it from updating dependencies which is important for [reproducible builds](https://reproducible-builds.org/).

## Check

Most Rust projects provide a simple way to run the testsuite.

```
 check() {
   cargo test --release --locked
 }

```

## Package

Rust builds binaries in `target/release` and can simply be installed to `/usr/bin`.

```
 package() {
   install -Dm 755 target/release/${pkgname} -t "${pkgdir}/usr/bin"
 }

```

Some packages should install more files such as a man page, so in that case it would be better to use `cargo`:

```
 package() {
   cargo install --root "${pkgdir}"/usr --root "${srcdir}/${pkgname}-${pkgver}"
 }

```