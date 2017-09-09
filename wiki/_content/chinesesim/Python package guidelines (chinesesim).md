**[Package creation guidelines](/index.php/Creating_packages "Creating packages")**

* * *

[CLR](/index.php/CLR_package_guidelines "CLR package guidelines") – [Cross](/index.php/Cross-compiling_tools_package_guidelines "Cross-compiling tools package guidelines") – [Eclipse](/index.php/Eclipse_plugin_package_guidelines "Eclipse plugin package guidelines") – [Free Pascal](/index.php/Free_Pascal_package_guidelines "Free Pascal package guidelines") – [GNOME](/index.php/GNOME_package_guidelines "GNOME package guidelines") – [Go](/index.php/Go_package_guidelines "Go package guidelines") – [Haskell](/index.php/Haskell_package_guidelines "Haskell package guidelines") – [Java](/index.php/Java_package_guidelines "Java package guidelines") – [KDE](/index.php/KDE_package_guidelines "KDE package guidelines") – [Kernel](/index.php/Kernel_module_package_guidelines "Kernel module package guidelines") – [Lisp](/index.php/Lisp_package_guidelines "Lisp package guidelines") – [MinGW](/index.php/MinGW_package_guidelines "MinGW package guidelines") – [Node.js](/index.php/Node.js_package_guidelines "Node.js package guidelines") – [Nonfree](/index.php/Nonfree_applications_package_guidelines "Nonfree applications package guidelines") – [OCaml](/index.php/OCaml_package_guidelines "OCaml package guidelines") – [Perl](/index.php/Perl_package_guidelines "Perl package guidelines") – [PHP](/index.php/PHP_package_guidelines "PHP package guidelines") – [Python](/index.php/Python_package_guidelines "Python package guidelines") – [Ruby](/index.php/Ruby_Gem_package_guidelines "Ruby Gem package guidelines") – [VCS](/index.php/VCS_package_guidelines "VCS package guidelines") – [Web](/index.php/Web_application_package_guidelines "Web application package guidelines") – [Wine](/index.php/Wine_package_guidelines "Wine package guidelines")

**翻译状态：** 本文是英文页面 [Python package guidelines](/index.php/Python_package_guidelines "Python package guidelines") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2017-09-08，点击[这里](https://wiki.archlinux.org/index.php?title=Python+package+guidelines&diff=0&oldid=488822)可以查看翻译后英文页面的改动。

本文档描述了如何基于标准 [PKGBUILDs](/index.php/PKGBUILD "PKGBUILD") 来为 [Python](/index.php/Python "Python") 程序进行打包.

## Contents

*   [1 包命名](#.E5.8C.85.E5.91.BD.E5.90.8D)
    *   [1.1 带版本的软件包](#.E5.B8.A6.E7.89.88.E6.9C.AC.E7.9A.84.E8.BD.AF.E4.BB.B6.E5.8C.85)
*   [2 Installation methods](#Installation_methods)
    *   [2.1 distutils](#distutils)
    *   [2.2 setuptools](#setuptools)
    *   [2.3 pip](#pip)
*   [3 注意事项](#.E6.B3.A8.E6.84.8F.E4.BA.8B.E9.A1.B9)
    *   [3.1 PyPI download URLs](#PyPI_download_URLs)

## 包命名

Python 3 的包应该使用 `python-*modulename*` 进行命名。如果软件包与 Python 某个生态系统(例如 pip 或 tox) 关系密切，请添加相应前缀。对于其他 Python 程序来说, 使用程序名就足够了。无论如何, 包的名字应该完全使用小写。

这同样适用于 Python 2，只需要修改前缀为 `python2-` (如果必须)。

### 带版本的软件包

If you need to add a versioned package then use `python-*modulename*-*version*`, e.g. `python-colorama-0.2.5`. So python dependency `colorama==0.2.5` will turn into `python-colorama-0.2.5` Arch package.

## Installation methods

Python 的包通常使用 Python 语言自带的工具来安装, 例如 [pip](https://pip.pypa.io/) 或者 [easy_install](https://setuptools.readthedocs.io/en/latest/easy_install.html), which are comparable to dedicated package managers in that they are designed to fetch the source files from an online repository (usually [PyPI](https://pypi.python.org/), the Python Package Index) and track the relevant files (for a detailed comparison between the two, see [pip vs easy_install](https://packaging.python.org/pip_easy_install/#pip-vs-easy-install)).

However, for managing Python packages from within PKGBUILDs, the standard-provided [distutils](http://docs.python.org/library/distutils.html) proves to be the most convenient solution since it uses the downloaded source package's `setup.py` and easily installs files under `*$pkgdir*/usr/lib/python*<python version>*/site-packages/*$pkgname*` directory.

### distutils

[这里](https://projects.archlinux.org/abs.git/tree/prototypes/PKGBUILD-python.proto)有一个 *distutils* PKGBUILD 样本。他遵从下面的格式:

```
*<python version>* setup.py install --root="$pkgdir/" --optimize=1

```

where:

*   根据程序所使用的 Python 版本来使用 `python` 或者 `python2` 替换 *<python version>* 。
*   `--root="$pkgdir/"` prevents trying to directly install in the host system instead of inside the package file, which would result in a permission error
*   `--optimize=1` 选项是用来编译生成 `.pyo` 文件，好让 [pacman](/index.php/Pacman "Pacman") 更好的跟踪优化她们。

### setuptools

The Python packaging scene has largely migrated from *distutils* to *setuptools*, which is actively developed and functions as a drop-in replacement import in `setup.py`. The main difference for packagers is that *setuptools* is packaged separately from Python itself, and must be specified as a `makedepends`.

If the resulting package includes executables which [import the `pkg_resources` module](https://setuptools.readthedocs.io/en/latest/setuptools.html#automatic-script-creation), then *setuptools* must be additionally specified as a `depends` in the split `package_*()` functions; alternatively, if the PKGBUILD only installs the Python package for a single version of Python, *setuptools* should be moved from `makedepends` to `depends`.

### pip

如果你需要使用 *pip* (由 [python-pip](https://www.archlinux.org/packages/?name=python-pip) 和 [python2-pip](https://www.archlinux.org/packages/?name=python2-pip) 提供)， *例如* 为了安装 [wheel](https://bitbucket.org/pypa/wheel/) 的Python包, remember to pass the following flags:

```
PIP_CONFIG_FILE=/dev/null pip install --isolated --root="$pkgdir" --ignore-installed --no-deps *.whl

```

*   `PIP_CONFIG_FILE=/dev/null` ignores `{/etc,~/.config}/pip.conf` that may be appending arbitrary flags to **pip**.
*   `--isolated` ignores environment variables (and again `{/etc,~/.config}/pip/pip.conf`) that may otherwise also be appending arbitrary flags to **pip**.
*   `--ignore-installed` is necessary until [https://github.com/pypa/pip/issues/3063](https://github.com/pypa/pip/issues/3063) is resolved (otherwise **pip** skips the install in the presence of an earlier `--user` install).
*   `--no-deps` ensures, that dependencies do not get packaged together with the main package.

*pip* 不知道如何生成 `.pyo` 文件 (see [https://github.com/pypa/pip/issues/2209](https://github.com/pypa/pip/issues/2209)). 为了生成 `.pyo` 文件，在使用 *pip* 安装后, 运行:

```
python -O -m compileall "${pkgdir}/path/to/module

```

## 注意事项

绝大部分情况下， 你应该设置 `arch` 为 `any` ，因为绝大部分 Python 包是平台无关的。

Please do not install a directory named just `tests`, as it easily conflicts with other Python packages (for example, `/usr/lib/python2.7/site-packages/tests/`).

### PyPI download URLs

PyPI URLs of the form `https://pypi.python.org/packages/source/${_name:0:1}/${_name}/${_name}-${pkgver}.tar.gz`<footnote> were silently abandoned for new package versions in the course of 2016, replaced by a scheme using an unpredictable hash that needs to be fetched from the PyPI website each time a package must be updated[[1]](https://bitbucket.org/pypa/pypi/issues/438/backwards-compatible-un-hashed-package#comment-27230605).

As downstream packagers voiced their concerns to PyPI maintainers[[2]](https://bitbucket.org/pypa/pypi/issues/438/backwards-compatible-un-hashed-package), a new stable scheme was provided[[3]](https://bitbucket.org/pypa/pypi/issues/438/backwards-compatible-un-hashed-package#comment-27606213): [PKGBUILD#source](/index.php/PKGBUILD#source "PKGBUILD") `source=()` array should now use the following URL templates.

Note that a custom `$_name` variable is used instead of `$pkgname` since python packages are generally named `python-$_name`

	Source package

	`https://files.pythonhosted.org/packages/source/${_name::1}/${_name}/${_name}-${pkgver}.tar.gz`

	Bilingual wheel package (Python 2 and Python 3 compatible)

	`https://files.pythonhosted.org/packages/py2.py3/${_name::1}/$_name/$_name-$pkgver-$_name-$pkgver-py2.py3-none-any.whl`

	Arch specific wheel package

	in this example for `source_x86_64=('...')`. Also `_py=py36` can be used to not repeat the python version:

	`https://files.pythonhosted.org/packages/$_py/${_name::1}/$_name/$_name-$pkgver-$_py-${_py}m-manylinux1_x86_64.whl`