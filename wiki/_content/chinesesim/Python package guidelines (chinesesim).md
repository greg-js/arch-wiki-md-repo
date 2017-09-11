**[Package creation guidelines](/index.php/Creating_packages "Creating packages")**

* * *

[CLR](/index.php/CLR_package_guidelines "CLR package guidelines") – [Cross](/index.php/Cross-compiling_tools_package_guidelines "Cross-compiling tools package guidelines") – [Eclipse](/index.php/Eclipse_plugin_package_guidelines "Eclipse plugin package guidelines") – [Free Pascal](/index.php/Free_Pascal_package_guidelines "Free Pascal package guidelines") – [GNOME](/index.php/GNOME_package_guidelines "GNOME package guidelines") – [Go](/index.php/Go_package_guidelines "Go package guidelines") – [Haskell](/index.php/Haskell_package_guidelines "Haskell package guidelines") – [Java](/index.php/Java_package_guidelines "Java package guidelines") – [KDE](/index.php/KDE_package_guidelines "KDE package guidelines") – [Kernel](/index.php/Kernel_module_package_guidelines "Kernel module package guidelines") – [Lisp](/index.php/Lisp_package_guidelines "Lisp package guidelines") – [MinGW](/index.php/MinGW_package_guidelines "MinGW package guidelines") – [Node.js](/index.php/Node.js_package_guidelines "Node.js package guidelines") – [Nonfree](/index.php/Nonfree_applications_package_guidelines "Nonfree applications package guidelines") – [OCaml](/index.php/OCaml_package_guidelines "OCaml package guidelines") – [Perl](/index.php/Perl_package_guidelines "Perl package guidelines") – [PHP](/index.php/PHP_package_guidelines "PHP package guidelines") – [Python](/index.php/Python_package_guidelines "Python package guidelines") – [Ruby](/index.php/Ruby_Gem_package_guidelines "Ruby Gem package guidelines") – [VCS](/index.php/VCS_package_guidelines "VCS package guidelines") – [Web](/index.php/Web_application_package_guidelines "Web application package guidelines") – [Wine](/index.php/Wine_package_guidelines "Wine package guidelines")

**翻译状态：** 本文是英文页面 [Python package guidelines](/index.php/Python_package_guidelines "Python package guidelines") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2017-09-08，点击[这里](https://wiki.archlinux.org/index.php?title=Python+package+guidelines&diff=0&oldid=488822)可以查看翻译后英文页面的改动。

本文档描述了如何基于标准 [PKGBUILDs](/index.php/PKGBUILD "PKGBUILD") 来为 [Python](/index.php/Python "Python") 程序进行打包.

## Contents

*   [1 包命名](#.E5.8C.85.E5.91.BD.E5.90.8D)
    *   [1.1 带版本的软件包](#.E5.B8.A6.E7.89.88.E6.9C.AC.E7.9A.84.E8.BD.AF.E4.BB.B6.E5.8C.85)
*   [2 安装方式](#.E5.AE.89.E8.A3.85.E6.96.B9.E5.BC.8F)
    *   [2.1 distutils](#distutils)
    *   [2.2 setuptools](#setuptools)
    *   [2.3 pip](#pip)
*   [3 注意事项](#.E6.B3.A8.E6.84.8F.E4.BA.8B.E9.A1.B9)
    *   [3.1 PyPI 下载 URLs](#PyPI_.E4.B8.8B.E8.BD.BD_URLs)

## 包命名

Python 3 的包应该使用 `python-*modulename*` 进行命名。如果软件包与 Python 某个生态系统(例如 pip 或 tox) 关系密切，请添加相应前缀。对于其他 Python 程序来说, 使用程序名就足够了。无论如何, 包的名字应该完全使用小写。

这同样适用于 Python 2，只需要修改前缀为 `python2-` (如果必须)。

### 带版本的软件包

如果你需要添加一个带版本的软件包，请使用这种格式： `python-*模块名*-*版本*`, 比如 `python-colorama-0.2.5`。这样，Python 的依赖`colorama==0.2.5` 就会成为名为 `python-colorama-0.2.5` 的 Arch 软件包。

## 安装方式

Python 的包通常使用 Python 语言自带的工具来安装, 例如 [pip](https://pip.pypa.io/) 或者 [easy_install](https://setuptools.readthedocs.io/en/latest/easy_install.html), 这些工具就像是能从在线源 (通常是 [PyPI](https://pypi.python.org/), Python 包索引 (Python Package Index) ) 获取源文件的软件包管理器一样，而且还能跟踪相关的文件状态。 (如需这两个工具的详细比较，请参见 [pip vs easy_install](https://packaging.python.org/pip_easy_install/#pip-vs-easy-install)).

然而，如果要想从 PKGBUILD 文件内管理 Python 软件包的话，标准化的 [distutils](http://docs.python.org/library/distutils.html) 可以说是最方便的了。它会使用已下载源码包里面的 `setup.py` 接着就能很轻松地将文件安装到 `*$pkgdir*/usr/lib/python*<python 版本>*/site-packages/*$pkgname*` 这个文件夹下面了。

### distutils

[这里](https://projects.archlinux.org/abs.git/tree/prototypes/PKGBUILD-python.proto)有一个 *distutils* PKGBUILD 样本。他遵从下面的格式:

```
*<python 版本>* setup.py install --root="$pkgdir/" --optimize=1

```

其中:

*   根据程序所使用的 Python 版本来使用 `python` 或者 `python2` 替换 *<python 版本>* 。
*   `--root="$pkgdir/"` 选项是为了防止文件直接安装到主系统而不是打包目录中。如果直接安装到主系统中，会产生权限错误。
*   `--optimize=1` 选项是用来编译生成 `.pyo` 文件，好让 [pacman](/index.php/Pacman "Pacman") 更好的跟踪优化她们。

### setuptools

Python 包装机制已从 *distutils* 向 *setuptools* 迁移, 后者目前正处于活跃开发时期并且能直接在 `setup.py` 文件中替换前者。不过主要的区别在于，*setuptools* 并没有和 Python 主包打在一起，因此你必须将其指定为 `makedepends`。

如果成品包中存在导入 (import) 了 [`pkg_resources` 模块](https://setuptools.readthedocs.io/en/latest/setuptools.html#automatic-script-creation) 的二进制, 那么 *setuptools* 必须在分包函数 `package_*()` 中另外指定为 `depends`; 还有, 如果 PKGBUILD 只安装一个版本的 Python 包的话, *setuptools* 需要从 `makedepends` 移至 `depends`。

### pip

如果你需要使用 *pip* (由 [python-pip](https://www.archlinux.org/packages/?name=python-pip) 和 [python2-pip](https://www.archlinux.org/packages/?name=python2-pip) 提供)， *例如* 为了安装 [wheel](https://bitbucket.org/pypa/wheel/) 的Python包, 请记得传入下列参数:

```
PIP_CONFIG_FILE=/dev/null pip install --isolated --root="$pkgdir" --ignore-installed --no-deps *.whl

```

*   `PIP_CONFIG_FILE=/dev/null` 此参数会使 **pip** 忽略 `{/etc,~/.config}/pip.conf` 因为这个配置文件可能会向 **pip** 添加一些额外参数。
*   `--isolated` 此参数会使 **pip** 忽略环境变量 (以及 `{/etc,~/.config}/pip/pip.conf`) 否则 **pip** 又会被添加一些额外参数。
*   `--ignore-installed` 在 [https://github.com/pypa/pip/issues/3063](https://github.com/pypa/pip/issues/3063) 处提出的问题解决之前，把这个参数加上吧 (不然的话 **pip** 会在有早期 `--user` 安装痕迹的情况下跳过安装).
*   `--no-deps` 此参数能确保依赖不会跟着一起被打进主包里面去。

*pip* 不知道如何生成 `.pyo` 文件 (see [https://github.com/pypa/pip/issues/2209](https://github.com/pypa/pip/issues/2209)). 为了生成 `.pyo` 文件，在使用 *pip* 安装后, 运行:

```
python -O -m compileall "${pkgdir}/path/to/module

```

## 注意事项

绝大部分情况下， 你应该设置 `arch` 为 `any` ，因为绝大部分 Python 包是平台无关的。

请不要将文件安装到类似于 `tests` 这样名字的目录中, 因为这很容易与其他 Python 包发生文件冲突 (比方说, `/usr/lib/python2.7/site-packages/tests/`).

### PyPI 下载 URLs

PyPI 中像是这种格式 `https://pypi.python.org/packages/source/${_name:0:1}/${_name}/${_name}-${pkgver}.tar.gz`<footnote> 的 URL 已经在 2016 年静默失效了, 而新的格式需要一种只有从 PyPI 网站才能取得的不可预测的哈希码[[1]](https://bitbucket.org/pypa/pypi/issues/438/backwards-compatible-un-hashed-package#comment-27230605)。

在下游维护者向 PyPI 维护者抱怨了这个问题 [[2]](https://bitbucket.org/pypa/pypi/issues/438/backwards-compatible-un-hashed-package) 之后, 一种新的稳定的格式出现了 [[3]](https://bitbucket.org/pypa/pypi/issues/438/backwards-compatible-un-hashed-package#comment-27606213): [PKGBUILD#source](/index.php/PKGBUILD#source "PKGBUILD") `source=()` 数值现在需要使用如下 URL 模板：

请注意，我们使用了自定义的 `$_name` 而不是 `$pkgname`，因为 Python 包通常都命名成这样： `python-$_name`。

	源码包

	`https://files.pythonhosted.org/packages/source/${_name::1}/${_name}/${_name}-${pkgver}.tar.gz`

	双版本 wheel 包 (Python 2 和 Python 3 都兼容)

	`https://files.pythonhosted.org/packages/py2.py3/${_name::1}/$_name/$_name-$pkgver-$_name-$pkgver-py2.py3-none-any.whl`

	特定架构的 wheel 包

	in this example for `source_x86_64=('...')`. Also `_py=py36` can be used to not repeat the python version:

	`https://files.pythonhosted.org/packages/$_py/${_name::1}/$_name/$_name-$pkgver-$_py-${_py}m-manylinux1_x86_64.whl`