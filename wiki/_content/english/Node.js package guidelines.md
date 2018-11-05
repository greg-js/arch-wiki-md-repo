**[Package creation guidelines](/index.php/Arch_packaging_standards "Arch packaging standards")**

* * *

[CLR](/index.php/CLR_package_guidelines "CLR package guidelines") – [Cross](/index.php/Cross-compiling_tools_package_guidelines "Cross-compiling tools package guidelines") – [Eclipse](/index.php/Eclipse_plugin_package_guidelines "Eclipse plugin package guidelines") – [Free Pascal](/index.php/Free_Pascal_package_guidelines "Free Pascal package guidelines") – [GNOME](/index.php/GNOME_package_guidelines "GNOME package guidelines") – [Go](/index.php/Go_package_guidelines "Go package guidelines") – [Haskell](/index.php/Haskell_package_guidelines "Haskell package guidelines") – [Java](/index.php/Java_package_guidelines "Java package guidelines") – [KDE](/index.php/KDE_package_guidelines "KDE package guidelines") – [Kernel](/index.php/Kernel_module_package_guidelines "Kernel module package guidelines") – [Lisp](/index.php/Lisp_package_guidelines "Lisp package guidelines") – [MinGW](/index.php/MinGW_package_guidelines "MinGW package guidelines") – <a class="mw-selflink selflink">Node.js</a> – [Nonfree](/index.php/Nonfree_applications_package_guidelines "Nonfree applications package guidelines") – [OCaml](/index.php/OCaml_package_guidelines "OCaml package guidelines") – [Perl](/index.php/Perl_package_guidelines "Perl package guidelines") – [PHP](/index.php/PHP_package_guidelines "PHP package guidelines") – [Python](/index.php/Python_package_guidelines "Python package guidelines") – [R](/index.php/R_package_guidelines "R package guidelines") – [Ruby](/index.php/Ruby_Gem_package_guidelines "Ruby Gem package guidelines") – [VCS](/index.php/VCS_package_guidelines "VCS package guidelines") – [Web](/index.php/Web_application_package_guidelines "Web application package guidelines") – [Wine](/index.php/Wine_package_guidelines "Wine package guidelines")

This document covers standards and guidelines on writing [PKGBUILDs](/index.php/PKGBUILD "PKGBUILD") for [Node.js](/index.php/Node.js "Node.js") packages.

## Contents

*   [1 Package naming](#Package_naming)
*   [2 Using npm](#Using_npm)
    *   [2.1 Setting temporary cache](#Setting_temporary_cache)
    *   [2.2 Package contains reference to $srcdir/$pkgdir](#Package_contains_reference_to_.24srcdir.2F.24pkgdir)

## Package naming

Package names should start with a `nodejs-` prefix.

## Using npm

When installing with [npm](https://www.archlinux.org/packages/?name=npm), add it as a build dependency:

```
makedepends=('npm')

```

This is a minimal `package` function:

```
package() {
    npm install -g --user root --prefix "$pkgdir"/usr "$srcdir"/source-tarball.tar.gz

    # Non-deterministic race in npm gives 777 permissions to random directories.
    # See https://github.com/npm/npm/issues/9359 for details.
    find "${pkgdir}"/usr -type d -exec chmod 755 {} +
}

```

### Setting temporary cache

When npm processes `package.json` in order to build a package it downloads dependencies to its default cache folder at `$HOME/.npm`. To avoid littering user's home folder we can temporarily set a different cache folder with `--cache` flag:

Download dependencies to `${srcdir}/npm-cache` and install them in package directory

```
npm install --cache "${srcdir}/npm-cache" 

```

Continue with packaging as usual

```
npm run packager

```

### Package contains reference to $srcdir/$pkgdir

npm unfortunately creates references to the source dir and the pkg dir. This is [a known issue in NPM](https://github.com/npm/npm/issues/12110), and actually considered a feature. However, you may remove those reference manually, since they are not used in any way.

All dependencies will contain a reference to `$pkgdir`, in the `_where` attribute. You can usually remove those attributes with some sed magic as follows:

```
 find "$pkgdir" -name package.json -print0 | xargs -0 sed -i '/_where/d'

```

Your main package will have some other references too. The easiest way to remove those is to remove all underscored properties, but that is not as easy with sed. Instead, you can use [jq](https://www.archlinux.org/packages/?name=jq) for similar results as follows:

```
local tmppackage="$(mktemp)"
local pkgjson="$pkgdir/usr/lib/node_modules/$pkgname/package.json"
jq '.|=with_entries(select(.key|test("_.+")|not))' "$pkgjson" > "$tmppackage"
mv "$tmppackage" "$pkgjson"
chmod 644 "$pkgjson"

```

An example of both techniques can be seen in [bower-away](https://aur.archlinux.org/packages/bower-away/).