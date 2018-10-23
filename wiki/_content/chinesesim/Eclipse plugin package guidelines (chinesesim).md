**翻译状态：** 本文是英文页面 [Eclipse_plugin_package_guidelines](/index.php/Eclipse_plugin_package_guidelines "Eclipse plugin package guidelines") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2015-03-13，点击[这里](https://wiki.archlinux.org/index.php?title=Eclipse_plugin_package_guidelines&diff=0&oldid=365147)可以查看翻译后英文页面的改动。

**[Package creation guidelines](/index.php/Arch_packaging_standards "Arch packaging standards")**

* * *

[CLR](/index.php/CLR_package_guidelines "CLR package guidelines") – [Cross](/index.php/Cross-compiling_tools_package_guidelines "Cross-compiling tools package guidelines") – [Eclipse](/index.php/Eclipse_plugin_package_guidelines "Eclipse plugin package guidelines") – [Free Pascal](/index.php/Free_Pascal_package_guidelines "Free Pascal package guidelines") – [GNOME](/index.php/GNOME_package_guidelines "GNOME package guidelines") – [Go](/index.php/Go_package_guidelines "Go package guidelines") – [Haskell](/index.php/Haskell_package_guidelines "Haskell package guidelines") – [Java](/index.php/Java_package_guidelines "Java package guidelines") – [KDE](/index.php/KDE_package_guidelines "KDE package guidelines") – [Kernel](/index.php/Kernel_module_package_guidelines "Kernel module package guidelines") – [Lisp](/index.php/Lisp_package_guidelines "Lisp package guidelines") – [MinGW](/index.php/MinGW_package_guidelines "MinGW package guidelines") – [Node.js](/index.php/Node.js_package_guidelines "Node.js package guidelines") – [Nonfree](/index.php/Nonfree_applications_package_guidelines "Nonfree applications package guidelines") – [OCaml](/index.php/OCaml_package_guidelines "OCaml package guidelines") – [Perl](/index.php/Perl_package_guidelines "Perl package guidelines") – [PHP](/index.php/PHP_package_guidelines "PHP package guidelines") – [Python](/index.php/Python_package_guidelines "Python package guidelines") – [R](/index.php/R_package_guidelines "R package guidelines") – [Ruby](/index.php/Ruby_Gem_package_guidelines "Ruby Gem package guidelines") – [VCS](/index.php/VCS_package_guidelines "VCS package guidelines") – [Web](/index.php/Web_application_package_guidelines "Web application package guidelines") – [Wine](/index.php/Wine_package_guidelines "Wine package guidelines")

有许多安装有效 [Eclipse](/index.php/Eclipse "Eclipse") 插件的方法。尤其是在 Eclipse 3.4 里引入 *dropins* 文件夹之后。但其中一些比较凌乱，而且具有标准化和一致的封装方法对于一个干净的系统结构是非常重要的。然而，如果没有一个对 Eclipse 插件如何工作一清二楚的打包者的话，要实现这一切并不简单。本文试图定义一个标准且精简的 Eclipse 插件 [PKGBUILD](/index.php/PKGBUILD "PKGBUILD") 的结构，如此来在不用麻烦打包者全部重新打包的情况下保持一个干净的文件系统结构。

## Contents

*   [1 Eclipse 插件结构以及安装](#Eclipse_.E6.8F.92.E4.BB.B6.E7.BB.93.E6.9E.84.E4.BB.A5.E5.8F.8A.E5.AE.89.E8.A3.85)
*   [2 打包](#.E6.89.93.E5.8C.85)
    *   [2.1 PKGBUILD 样例](#PKGBUILD_.E6.A0.B7.E4.BE.8B)
    *   [2.2 如何自定义](#.E5.A6.82.E4.BD.95.E8.87.AA.E5.AE.9A.E4.B9.89)
    *   [2.3 深入分析 PKGBUILD](#.E6.B7.B1.E5.85.A5.E5.88.86.E6.9E.90_PKGBUILD)
        *   [2.3.1 包的命名](#.E5.8C.85.E7.9A.84.E5.91.BD.E5.90.8D)
        *   [2.3.2 文件](#.E6.96.87.E4.BB.B6)
            *   [2.3.2.1 解压](#.E8.A7.A3.E5.8E.8B)
            *   [2.3.2.2 地址](#.E5.9C.B0.E5.9D.80)
        *   [2.3.3 build() 函数](#build.28.29_.E5.87.BD.E6.95.B0)

## Eclipse 插件结构以及安装

一般的 Eclipse 插件包含两个目录，`features` 和 `plugins`, 自从 Eclipse 3.3 起它们只能放在 `/usr/share/eclipse/`. 这两个文件夹的内容可以与其他插件的混合，如此会导致混乱并且结构难以管理，也很难来一目了然地区分哪个软件包包含哪些文件。

这种安装方法依然被 Eclipse 3.4 支持，然而我们更推荐使用 `/usr/share/eclipse/dropins/` 目录。该文件夹内可包含不限数目的子目录，每个子目录包含自己的 `features` 和 `plugins` 子目录。这也能保持一个干净而精简的系统结构，并应当成为打包的标准。

## 打包

### PKGBUILD 样例

这里是一个样例，稍后我们将介绍如何自定义修改。

 `PKGBUILD-eclipse.proto` 
```
pkgname=eclipse-mylyn
pkgver=3.0.3
pkgrel=1
pkgdesc="A task-focused interface for Eclipse"
arch=('i686' 'x86_64')
url="http://www.eclipse.org/mylyn/"
license=('EPL')
depends=('eclipse')
optdepends=('bugzilla: ticketing support')
source=(http://download.eclipse.org/tools/mylyn/update/mylyn-${pkgver}-e3.4.zip)
md5sums=('e98cd7ab3c5d5aeb7c32845844f85c22')

prepare() {
  # remove features and plug-ins containing sources
  rm features/*.source_*
  rm plugins/*.source_*
  # remove gz files
  rm plugins/*.pack.gz
}

package() {
  _dest=${pkgdir}/usr/share/eclipse/dropins/${pkgname/eclipse-}/eclipse

  # Features
  find features -type f | while read _feature ; do
    if [[ ${_feature} =~ (.*\.jar$) ]] ; then
      install -dm755 ${_dest}/${_feature%*.jar}
      cd ${_dest}/${_feature/.jar}
      # extract features (otherwise they are not visible in about dialog)
      jar xf ${srcdir}/${_feature} || return 1
    else
      install -Dm644 ${_feature} ${_dest}/${_feature}
    fi
  done

  # Plugins
  find plugins -type f | while read _plugin ; do
    install -Dm644 "${_plugin}" "${_dest}/${_plugin}"
  done
}

```

### 如何自定义

需要修改的，最主要的变量就是 `pkgname`. 如果你要打包一个一般的插件，那么你只需要做这些: 大部分插件以 zip 文件发布，其中只含有 `features` 和 `plugins` 子目录。所以，如果你要打包 `foo` 插件并且源文件只包含 `features` 和 `plugins`, 只需把 `pkgname` 改成 `eclipse-foo`, 这样就完成了。

请仔细阅读，获取 PKGBUILD 的内部结构，这能帮助你理解在其他情况下如何设置编译。

### 深入分析 PKGBUILD

#### 包的命名

包应该命名为 `eclipse-*pluginname*`, 如此能被识别为 Eclipse 相关软件包并且能轻松使用 shell 替代来提取出如 `${pkgname/eclipse-}` 的插件名称，而不用使用不需要的 `${_realname}` 变量。插件名对于清理安装时临时文件并避免冲突是必需的。

#### 文件

##### 解压

一些插件需要的功能要从 jar 文件中提取。已包含于 JRE 的 `jar` 工具,就是用来干这个的。然而，`jar` 并不能解压到当前目录以外的地方: 这意味着，创建每个目录之后，在解压之前需要 `cd` 进入该目录。`${_dest}` 变量被用在这样的背景下，以提高文本可读性和PKGBUILD整洁性。

##### 地址

如同我们所说，源文档提供两个目录 `features` 和 `plugins`, 每个打包为 jar 文件。更好的嵌入式结构应该如下:

```
/usr/share/eclipse/dropins/pluginname/eclipse/features/feature1/...
/usr/share/eclipse/dropins/pluginname/eclipse/features/feature2/...
/usr/share/eclipse/dropins/pluginname/eclipse/plugins/plugin1.jar
/usr/share/eclipse/dropins/pluginname/eclipse/plugins/plugin2.jar

```

这种结构支持把不同插件需要的不同版本的库混起来，同时很清楚它是属于那个包的。这也能避免当不同插件提供了相同库时的冲突。唯一的选择是把每个包和它的库一起它所需的一切乱七八糟的东西分离，并且你也别想这样就能起效，因为有些包需要旧版的库才能工作。 必须要从 jar 里解压出来因为 Eclipse 不会自动检测它们，不然的话整个安装的插件都不会工作。这归因于 Eclipse 认为更新站点和本地安装是不同的 (别问为什么，它就这样).

#### build() 函数

首先要注意的就是 `cd ${srcdir}` 命令。通常源压缩文档直接在 `${srcdir}` 下解压出 `features` 和 `plugins` 文件夹，但并不是所有的都这样。总之，对大多数*(事实上)*非标准的插件这是需要改变的唯一路线。

某些特性也随源码发布。对一个普通的释出版来说源码并不需要，可以删除。更多的特性包含 `*.pack.gz` 文件，与 jar 文档相比内容相同。所以这些文件也能删除。

接下来是 `features` 部分。它为每个 jar 文件创建必要的目录并解压到对应的目录去。同样，`plugins` 部分把 jar 安装到文件夹里去。一个 while 循环用于防止生成名字奇怪的文件。