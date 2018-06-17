**[Package creation guidelines](/index.php/Creating_packages "Creating packages")**

* * *

[CLR](/index.php/CLR_package_guidelines "CLR package guidelines") – [Cross](/index.php/Cross-compiling_tools_package_guidelines "Cross-compiling tools package guidelines") – [Eclipse](/index.php/Eclipse_plugin_package_guidelines "Eclipse plugin package guidelines") – [Free Pascal](/index.php/Free_Pascal_package_guidelines "Free Pascal package guidelines") – [GNOME](/index.php/GNOME_package_guidelines "GNOME package guidelines") – [Go](/index.php/Go_package_guidelines "Go package guidelines") – [Haskell](/index.php/Haskell_package_guidelines "Haskell package guidelines") – [Java](/index.php/Java_package_guidelines "Java package guidelines") – [KDE](/index.php/KDE_package_guidelines "KDE package guidelines") – [Kernel](/index.php/Kernel_module_package_guidelines "Kernel module package guidelines") – [Lisp](/index.php/Lisp_package_guidelines "Lisp package guidelines") – [MinGW](/index.php/MinGW_package_guidelines "MinGW package guidelines") – [Node.js](/index.php/Node.js_package_guidelines "Node.js package guidelines") – [Nonfree](/index.php/Nonfree_applications_package_guidelines "Nonfree applications package guidelines") – [OCaml](/index.php/OCaml_package_guidelines "OCaml package guidelines") – [Perl](/index.php/Perl_package_guidelines "Perl package guidelines") – [PHP](/index.php/PHP_package_guidelines "PHP package guidelines") – <a class="mw-selflink selflink">Python</a> – [Ruby](/index.php/Ruby_Gem_package_guidelines "Ruby Gem package guidelines") – [VCS](/index.php/VCS_package_guidelines "VCS package guidelines") – [Web](/index.php/Web_application_package_guidelines "Web application package guidelines") – [Wine](/index.php/Wine_package_guidelines "Wine package guidelines")

This document covers standards and guidelines on writing [PKGBUILDs](/index.php/PKGBUILD "PKGBUILD") for [Python](/index.php/Python "Python") software.

## Contents

*   [1 Package naming](#Package_naming)
*   [2 Source](#Source)
*   [3 Installation methods](#Installation_methods)
    *   [3.1 distutils](#distutils)
    *   [3.2 setuptools](#setuptools)
    *   [3.3 pip](#pip)
*   [4 Notes](#Notes)

## Package naming

For [Python 3](/index.php/Python#Python_3 "Python") library modules, use `python-*modulename*`. Also use the prefix if the package provides a program that is strongly coupled to the Python ecosystem (e.g. *pip* or *tox*). For other applications, use only the program name.

The same applies to Python 2 except that the prefix (if needed) is `python2-`.

**Note:** The package name should be entirely lowercase.

## Source

Download URLs linked from the PyPI website include an unpredictable hash that needs to be fetched from the PyPI website each time a package must be updated. This makes them unsuitable for use in a PKGBUILD. PyPI [provides](https://github.com/pypa/pypi-legacy/issues/438#issuecomment-226940730) an alternative stable scheme: [PKGBUILD#source](/index.php/PKGBUILD#source "PKGBUILD") `source=()` array should use the following URL templates:

	Source package

	`https://files.pythonhosted.org/packages/source/${_name::1}/${_name}/${_name}-${pkgver}.tar.gz`

	Bilingual wheel package (Python 2 and Python 3 compatible)

	`https://files.pythonhosted.org/packages/py2.py3/${_name::1}/$_name/$_name-$pkgver-py2.py3-none-any.whl`

	Arch specific wheel package

	in this example for `source_x86_64=('...')`. Also `_py=py36` can be used to not repeat the python version:

	`https://files.pythonhosted.org/packages/$_py/${_name::1}/$_name/$_name-$pkgver-$_py-${_py}m-manylinux1_x86_64.whl`

Note that a custom `**_name**` variable is used instead of `pkgname` since python packages are generally prefixed with `python-`. This variable can generically be defined as follows:

```
_name=${pkgname#python-}

```

## Installation methods

Python packages are generally installed using language-specific tools, such as [pip](https://pip.pypa.io/) or [easy_install](https://setuptools.readthedocs.io/en/latest/easy_install.html), which are comparable to dedicated package managers in that they are designed to fetch the source files from an online repository (usually [PyPI](https://pypi.org/), the Python Package Index) and track the relevant files (for a detailed comparison between the two, see [pip vs easy_install](https://packaging.python.org/pip_easy_install/#pip-vs-easy-install)).

However, for managing Python packages from within PKGBUILDs, the standard-provided [distutils](http://docs.python.org/library/distutils.html) proves to be the most convenient solution since it uses the downloaded source package's `setup.py` and easily installs files under `*$pkgdir*/usr/lib/python*<python version>*/site-packages/*$pkgname*` directory.

### distutils

A *distutils* PKGBUILD is usually quite simple:

```
build() {
    *python* setup.py build
}

package() {
    *python* setup.py install --root="$pkgdir/" --optimize=1 --skip-build
}

```

where:

*   *python* is replaced with the proper binary, `python` or `python2`
*   `--root="$pkgdir/"` prevents trying to directly install in the host system instead of inside the package file, which would result in a permission error
*   `--optimize=1` compiles optimized bytecode files (`.pyo` for Python 2, `opt-1.pyc` for Python 3) so they can be tracked by [pacman](/index.php/Pacman "Pacman").
*   `--skip-build` optimizes away the unnecessary attempt to re-run the build steps already run in the `build()` function.

### setuptools

The Python packaging scene has largely migrated from *distutils* to *setuptools*, which is actively developed and functions as a drop-in replacement import in `setup.py`. The main difference for packagers is that *setuptools* is packaged separately from Python itself, and must be specified as a `makedepends`.

If the resulting package includes executables which [import the `pkg_resources` module](https://setuptools.readthedocs.io/en/latest/setuptools.html#automatic-script-creation), then *setuptools* must be additionally specified as a `depends` in the split `package_*()` functions; alternatively, if the PKGBUILD only installs the Python package for a single version of Python, *setuptools* should be moved from `makedepends` to `depends`.

### pip

If you need to use *pip* (provided by [python-pip](https://www.archlinux.org/packages/?name=python-pip) and [python2-pip](https://www.archlinux.org/packages/?name=python2-pip)), *e.g.* for installing [wheel](https://github.com/pypa/wheel) packages, remember to pass the following flags:

```
PIP_CONFIG_FILE=/dev/null pip install --isolated --root="$pkgdir" --ignore-installed --no-deps *.whl

```

*   `PIP_CONFIG_FILE=/dev/null` ignores `{/etc,~/.config}/pip.conf` that may be appending arbitrary flags to **pip**.
*   `--isolated` ignores environment variables (and again `{/etc,~/.config}/pip/pip.conf`) that may otherwise also be appending arbitrary flags to **pip**.
*   `--ignore-installed` is necessary until [https://github.com/pypa/pip/issues/3063](https://github.com/pypa/pip/issues/3063) is resolved (otherwise **pip** skips the install in the presence of an earlier `--user` install).
*   `--no-deps` ensures, that dependencies do not get packaged together with the main package.

*pip* doesn't know how to generate `.pyo` files (see [https://github.com/pypa/pip/issues/2209](https://github.com/pypa/pip/issues/2209)). In order to generate them manually after *pip* has installed the module, run:

```
python -O -m compileall "${pkgdir}/path/to/module"

```

**Warning:** Use of *pip* and/or wheel packages is discouraged in favor of setuptools source packages, and should only be used when the latter is not a viable option (for example, packages which **only** come with wheel sources, and therefore cannot be installed using setuptools).

## Notes

In most cases, you should put `any` in the `arch` array since most Python packages are architecture independent.

Please do not install a directory named just `tests`, as it easily conflicts with other Python packages (for example, `/usr/lib/python2.7/site-packages/tests/`).