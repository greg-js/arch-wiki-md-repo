**[Package creation guidelines](/index.php/Arch_packaging_standards "Arch packaging standards")**

* * *

[CLR](/index.php/CLR_package_guidelines "CLR package guidelines") – [Cross](/index.php/Cross-compiling_tools_package_guidelines "Cross-compiling tools package guidelines") – [Eclipse](/index.php/Eclipse_plugin_package_guidelines "Eclipse plugin package guidelines") – [Electron](/index.php/Electron_package_guidelines "Electron package guidelines") – [Free Pascal](/index.php/Free_Pascal_package_guidelines "Free Pascal package guidelines") – [GNOME](/index.php/GNOME_package_guidelines "GNOME package guidelines") – [Go](/index.php/Go_package_guidelines "Go package guidelines") – [Haskell](/index.php/Haskell_package_guidelines "Haskell package guidelines") – [Java](/index.php/Java_package_guidelines "Java package guidelines") – [KDE](/index.php/KDE_package_guidelines "KDE package guidelines") – [Kernel](/index.php/Kernel_module_package_guidelines "Kernel module package guidelines") – [Lisp](/index.php/Lisp_package_guidelines "Lisp package guidelines") – [MinGW](/index.php/MinGW_package_guidelines "MinGW package guidelines") – [Node.js](/index.php/Node.js_package_guidelines "Node.js package guidelines") – [Nonfree](/index.php/Nonfree_applications_package_guidelines "Nonfree applications package guidelines") – [OCaml](/index.php/OCaml_package_guidelines "OCaml package guidelines") – [Perl](/index.php/Perl_package_guidelines "Perl package guidelines") – [PHP](/index.php/PHP_package_guidelines "PHP package guidelines") – <a class="mw-selflink selflink">Python</a> – [R](/index.php/R_package_guidelines "R package guidelines") – [Ruby](/index.php/Ruby_Gem_package_guidelines "Ruby Gem package guidelines") – [Rust](/index.php/Rust_package_guidelines "Rust package guidelines") – [VCS](/index.php/VCS_package_guidelines "VCS package guidelines") – [Web](/index.php/Web_application_package_guidelines "Web application package guidelines") – [Wine](/index.php/Wine_package_guidelines "Wine package guidelines")

This document covers standards and guidelines on writing [PKGBUILDs](/index.php/PKGBUILD "PKGBUILD") for [Python](/index.php/Python "Python") software.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Package naming](#Package_naming)
*   [2 Architecture](#Architecture)
*   [3 Source](#Source)
*   [4 Installation methods](#Installation_methods)
    *   [4.1 distutils](#distutils)
    *   [4.2 setuptools](#setuptools)
    *   [4.3 pip](#pip)
    *   [4.4 Build-time 2to3 translation](#Build-time_2to3_translation)
*   [5 Check](#Check)
*   [6 Notes](#Notes)

## Package naming

For [Python 3](/index.php/Python#Python_3 "Python") library modules, use `python-*modulename*`. Also use the prefix if the package provides a program that is strongly coupled to the Python ecosystem (e.g. *pip* or *tox*). For other applications, use only the program name.

The same applies to Python 2 except that the prefix (if needed) is `python2-`.

**Note:** The package name should be entirely lowercase.

## Architecture

See [PKGBUILD#arch](/index.php/PKGBUILD#arch "PKGBUILD").

A Python package that contains C extensions using the `ext_modules` keyword in `setup.py`, is architecture-dependent. Otherwise it is most likely architecture-independent.

## Source

Download URLs linked from the PyPI website include an unpredictable hash that needs to be fetched from the PyPI website each time a package must be updated. This makes them unsuitable for use in a PKGBUILD. PyPI [provides](https://github.com/pypa/pypi-legacy/issues/438#issuecomment-226940730) an alternative stable scheme: [PKGBUILD#source](/index.php/PKGBUILD#source "PKGBUILD") `source=()` array should use the following URL templates:

	Source package

	`https://files.pythonhosted.org/packages/source/${_name::1}/$_name/$_name-$pkgver.tar.gz`

	Pure Python wheel package

	`https://files.pythonhosted.org/packages/py2.py3/${_name::1}/$_name/${_name/-/_}-$pkgver-py2.py3-none-any.whl` (Bilingual – Python 2 and Python 3 compatible)

	`https://files.pythonhosted.org/packages/py3/${_name::1}/$_name/${_name/-/_}-$pkgver-py3-none-any.whl` (Python 3 only)

	Note that the distribution name can contain dashes, while its representation in a wheel filename cannot (they are converted to underscores).

	Arch specific wheel package

	in this example for `source_x86_64=('...')`. Also `_py=py37` can be used to not repeat the python version:

	`https://files.pythonhosted.org/packages/$_py/${_name::1}/$_name/${_name/-/_}-$pkgver-$_py-${_py}m-manylinux1_x86_64.whl`

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

### Build-time 2to3 translation

Most Python projects target either Python 2 or Python 3, or target both using compatibility layers like [six](https://pythonhosted.org/six/). However, some use the deprecated 2to3 keyword in setuptools to heuristically convert the source code from Python 2 to Python 3 at build time. As a result, the same source directories cannot be used to build both Python 2 and Python 3 split packages.

For packages that do this, we need a [prepare()](/index.php/Creating_packages#prepare.28.29 "Creating packages") function that copies the source before it is built. Then the Python 2 and Python 3 packages can be converted and built independently without overriding each other.

```
makedepends=("python-setuptools" "python2-setuptools")

prepare() {
    cp -a foo-$pkgver{,-py2}
}

build() {
    cd "$srcdir/foo-$pkgver"
    python setup.py build

    cd "$srcdir/foo-$pkgver-py2"
    python2 setup.py build
}

package_python-foo() {
    depends=("python")
    cd "$srcdir/foo-$pkgver"
    python setup.py install --root="$pkgdir/" --optimize=1 --skip-build
}

package_python2-foo() {
    depends=("python2")
    cd "$srcdir/foo-$pkgver-py2"
    python2 setup.py install --root="$pkgdir/" --optimize=1 --skip-build
}
```

## Check

**Warning:** Avoid using `tox` to run testsuites as it is explicitly designed to test repeatable configurations downloaded from PyPI while `tox` is running, and does **not** test the version that will be installed by the package. This defeats the purpose of having a *check* function at all.

Most python projects providing a testsuite use nosetests or pytest to run tests with `test` in the name of the file or directory containing the testsuite. In general, simply running `nosetests` or `pytest` is enough to run the testsuite.

```
check(){
    cd "$srcdir/foo-$pkgver"

    # For nosetests
    nosetests

    # For pytest
    pytest
}

```

If there is a compiled C extension, the tests need to be run using a `$PYTHONPATH` hack in order to find and load it.

```
check(){
    cd "$srcdir/foo-$pkgver"

    # For nosetests
    PYTHONPATH="$PWD/build/lib.linux-$CARCH-3.7" nosetests

    # For pytest
    PYTHONPATH="$PWD/build/lib.linux-$CARCH-3.7" pytest
}
```

Some projects provide `setup.py` entry points for running the test. This works for both `pytest` and `nosetests`.

```
check(){
    cd "$srcdir/foo-$pkgver"

    # For nosetests
    python setup.py nosetests

    # For pytest - needs python-pytest-runner
    python setup.py pytest
}

```

## Notes

Please do not install a directory named just `tests`, as it easily conflicts with other Python packages (for example, `/usr/lib/python2.7/site-packages/tests/`).