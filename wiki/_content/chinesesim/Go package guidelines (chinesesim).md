**[Package creation guidelines](/index.php/Creating_packages "Creating packages")**

* * *

[CLR](/index.php/CLR_package_guidelines "CLR package guidelines") – [Cross](/index.php/Cross-compiling_tools_package_guidelines "Cross-compiling tools package guidelines") – [Eclipse](/index.php/Eclipse_plugin_package_guidelines "Eclipse plugin package guidelines") – [Free Pascal](/index.php/Free_Pascal_package_guidelines "Free Pascal package guidelines") – [GNOME](/index.php/GNOME_package_guidelines "GNOME package guidelines") – [Go](/index.php/Go_package_guidelines "Go package guidelines") – [Haskell](/index.php/Haskell_package_guidelines "Haskell package guidelines") – [Java](/index.php/Java_package_guidelines "Java package guidelines") – [KDE](/index.php/KDE_package_guidelines "KDE package guidelines") – [Kernel](/index.php/Kernel_module_package_guidelines "Kernel module package guidelines") – [Lisp](/index.php/Lisp_package_guidelines "Lisp package guidelines") – [MinGW](/index.php/MinGW_package_guidelines "MinGW package guidelines") – [Node.js](/index.php/Node.js_package_guidelines "Node.js package guidelines") – [Nonfree](/index.php/Nonfree_applications_package_guidelines "Nonfree applications package guidelines") – [OCaml](/index.php/OCaml_package_guidelines "OCaml package guidelines") – [Perl](/index.php/Perl_package_guidelines "Perl package guidelines") – [PHP](/index.php/PHP_package_guidelines "PHP package guidelines") – [Python](/index.php/Python_package_guidelines "Python package guidelines") – [Ruby](/index.php/Ruby_Gem_package_guidelines "Ruby Gem package guidelines") – [VCS](/index.php/VCS_package_guidelines "VCS package guidelines") – [Web](/index.php/Web_application_package_guidelines "Web application package guidelines") – [Wine](/index.php/Wine_package_guidelines "Wine package guidelines")

Arch Linux 对 [Go](https://en.wikipedia.org/wiki/Go_(programming_language) 的支持非常完善。

软件包 [go](https://www.archlinux.org/packages/?name=go) 中包含了 **go** 工具 (用于运行 `go fix`, `go build` 等)。 另外还有个提供 `gccgo` 的 [gcc-go](https://www.archlinux.org/packages/?name=gcc-go) 软件包。

你可以用 [go-makepkg](https://github.com/seletskiy/go-makepkg) 工具来协助你简单的打包Go程序，而不用从头到尾手动编写 PKGBUILD 。

## Contents

*   [1 通用准则](#.E9.80.9A.E7.94.A8.E5.87.86.E5.88.99)
    *   [1.1 命名](#.E5.91.BD.E5.90.8D)
    *   [1.2 打包](#.E6.89.93.E5.8C.85)
*   [2 PKGBUILD 范例](#PKGBUILD_.E8.8C.83.E4.BE.8B)
    *   [2.1 Go 语言开发的独立程序 PKGBUILD](#Go_.E8.AF.AD.E8.A8.80.E5.BC.80.E5.8F.91.E7.9A.84.E7.8B.AC.E7.AB.8B.E7.A8.8B.E5.BA.8F_PKGBUILD)
        *   [2.1.1 参考示例包](#.E5.8F.82.E8.80.83.E7.A4.BA.E4.BE.8B.E5.8C.85)
    *   [2.2 仅包含单个Go文件的程序 PKGBUILD](#.E4.BB.85.E5.8C.85.E5.90.AB.E5.8D.95.E4.B8.AAGo.E6.96.87.E4.BB.B6.E7.9A.84.E7.A8.8B.E5.BA.8F_PKGBUILD)
        *   [2.2.1 参考示例包](#.E5.8F.82.E8.80.83.E7.A4.BA.E4.BE.8B.E5.8C.85_2)
    *   [2.3 包含可执行文件的Go语言库 PKGBUILD](#.E5.8C.85.E5.90.AB.E5.8F.AF.E6.89.A7.E8.A1.8C.E6.96.87.E4.BB.B6.E7.9A.84Go.E8.AF.AD.E8.A8.80.E5.BA.93_PKGBUILD)
        *   [2.3.1 使用 *go get*](#.E4.BD.BF.E7.94.A8_go_get)
        *   [2.3.2 使用 *go get*](#.E4.BD.BF.E7.94.A8_go_get_2)

## 通用准则

### 命名

*   对于使用Go语言编写的独立应用，使用小写字母的应用名作为软件包名。
    *   如果软件包名已被占用，请另选一个合适的。
*   对于使用Go语言编写的软件库，请使用小写字母的 `go-*库名*` 作为软件包名。
    *   如果软件库名本身就是以 `go-` 开头的，请不要使用 `go-*go-模块名*` 这样的名字，而改用 `go-*模块名*`。
*   对于使用"go"工具下载的软件包，只有当它不是从tar包或者tagged提交(而是从trunk/HEAD)下载源码时，软件包名才添加"-git"后缀。
    *   类似的，对于mercurial 版本控制系统，只有当软件包未从release-revision下载源码时，才添加"-hg"后缀。
    *   其他版本控制系统，请一并参考该准则。
    *   "go"工具下载那个分支或者Tag通常有他自己的一套逻辑。请参考 `go get --help`.
*   如果有多个同名的软件包，可考虑将作者的名字添加到软件包名之中，例如：[dcpu16-kballard](https://aur.archlinux.org/packages/dcpu16-kballard/)。
    *   当然，通常情况下，最流行的软件包会使用最短或者"最佳"的软件包名。
*   如果软件开发者本身并没有正式的官方发布，那么这种后缀名 (例如 `-hg`, `-git` 或 `-svn`) 只是可选的。 一方面，这种软件包通常都是直接通过源码版本库下载使用的。另一方面, 大多数 Go 语言项目从不发布任何tarball，而只发布源码版本库。并将版本库的master分支、HEAD提交以外的分支、Tag作为官方发布的方式。另一方面，Go语言官方的模块安装方式 `go get` 也往往直接使用源码版本库。所以请根据情况作出最佳选择。

### 打包

*   Go 语言项目通常只包含软件库、可执行文件或者两者俱有。请以合适的方式打包他们。后续有几个例子以供参考。
*   有些 Go 语言项目并不支持最新版本的Go编译。这种情况下
    *   直接执行 `go build -fix` 一般就可以搞定了。如果仍有问题，请上报给上游开发者，并且他们修复。
*   有些Go语言项目并没有版本号或者授权协议文件。这种情况下：
    *   使用 license=('unknown') 并向上游开发者提交授权协议缺失的报告。
    *   如果没有版本号，请使用 "0.1", "1" 或者Git库的revision ( 其他版本控制系统类似)。
    *   作为备选，可以用当前日期作为版本号，格式形如 `YYYYMMDD`。
*   由于Go语言应用常常都是静态编译后发布可执行文件，因此通常都会直接打包Go语言应用而不是他的库。

## PKGBUILD 范例

### Go 语言开发的独立程序 PKGBUILD

```
# Maintainer: NAME <EMAIL>

pkgname=PACKAGE NAME
pkgver=1.2.3
pkgrel=1
pkgdesc="PACKAGE DESCRIPTION"
arch=('x86_64' 'i686')
url="http://SERVER/$pkgname/"
license=('MIT')
makedepends=('go')
options=('!strip' '!emptydirs')
source=("http://SERVER/$pkgname/$pkgname-$pkgver.tar.gz")
sha256sums=('00112233445566778899aabbccddeeff')

build() {
  cd "$pkgname-$pkgver"

  go build
}

package() {
  cd "$pkgname-$pkgver"

  install -Dm755 "$pkgname-$pkgver" "$pkgdir/usr/bin/$pkgname"
  install -Dm644 LICENSE "$pkgdir/usr/share/licenses/$pkgname/LICENSE"
}

# vim:set ts=2 sw=2 et:
```

#### 参考示例包

*   [gendesk](https://www.archlinux.org/packages/?name=gendesk)
*   [dcpu16](https://aur.archlinux.org/packages/dcpu16/)

### 仅包含单个Go文件的程序 PKGBUILD

```
# Maintainer: NAME <EMAIL>

pkgname=PACKAGE NAME
pkgver=1.2.3
pkgrel=1
pkgdesc="PACKAGE DESCRIPTION"
arch=('x86_64' 'i686')
url="http://SERVER/$pkgname/"
license=('GPL3')
makedepends=('go')
options=('!strip' '!emptydirs')
source=("http://SERVER/$pkgname/$pkgname.go")
sha256sums=('00112233445566778899aabbccddeeff')

build() {
  go build -o "$pkgname"
}

package() {
  install -Dm755 "$pkgname" "$pkgdir/usr/bin/$pkgname"
}

# vim:set ts=2 sw=2 et:
```

#### 参考示例包

*   [gorun](https://aur.archlinux.org/packages/gorun/)

### 包含可执行文件的Go语言库 PKGBUILD

#### 使用 *go get*

这是推荐的使用"go get"的方式，请优先选用这种方式，后文介绍的那种仅供参考。

这种方式将依赖于"go get"。

通常情况下你无需修改 build() 或 package() 函数，只需要修改前面定义的变量 (pkgname 等)即可。

如果打包失败，请先确保手动执行"go get"能成功。

**提示：** 如果打包失败，尝试去掉 `/...`再试试！

```
# Maintainer: NAME <EMAIL>

pkgname=codesearch
pkgver=20120515
pkgrel=1
pkgdesc="Code indexing and search written in Go"
arch=('x86_64' 'i686')
url="https://github.com/google/codesearch"
license=('BSD')
depends=('go')
makedepends=('mercurial')
options=('!strip' '!emptydirs')
_gourl=github.com/google/codesearch

build() {
  GOPATH="$srcdir" go get -fix -v -x ${_gourl}/...
}

check() {
  GOPATH="$GOPATH:$srcdir" go test -v -x ${_gourl}/...
}

package() {
  mkdir -p "$pkgdir/usr/bin"
  install -p -m755 "$srcdir/bin/"* "$pkgdir/usr/bin"

  mkdir -p "$pkgdir/$GOPATH"
  cp -Rv --preserve=timestamps "$srcdir/"{src,pkg} "$pkgdir/$GOPATH"

  # Package license (if available)
  for f in LICENSE COPYING LICENSE.* COPYING.*; do
    if [ -e "$srcdir/src/$_gourl/$f" ]; then
      install -Dm644 "$srcdir/src/$_gourl/$f" \
        "$pkgdir/usr/share/licenses/$pkgname/$f"
    fi
  done
}

# vim:set ts=2 sw=2 et:
```

感谢 Rémy Oudompheng‎ 提供该范例。

#### 使用 *go get*

另外一种依靠 `go get`的方式如下。

你一般不需要修改 build() 或 package() 函数，只需要修改前面的变量 (pkgname 等)即可。

如果打包有问题，请先确保手动执行 `go get` 没问题。

```
# Maintainer: NAME <EMAIL>

pkgname=PACKAGE NAME
pkgver=1.2.3
pkgrel=1
pkgdesc="PACKAGE DESCRIPTION"
arch=('x86_64' 'i686')
url="http://SERVER/$pkgname/"
license=('MIT')
makedepends=('go' 'git')
options=('!strip' '!emptydirs')
_gourl=SERVER.NET/PATH/MODULENAME

build() {
  export GOROOT=/usr/lib/go

  rm -rf build
  mkdir -p build/go
  cd build/go

  for f in "$GOROOT/"*; do
    ln -s "$f"
  done

  rm pkg
  mkdir pkg
  cd pkg

  for f in "$GOROOT/pkg/"*; do
    ln -s "$f"
  done

  platform=`for f in "$GOROOT/pkg/"*; do echo \`basename $f\`; done|grep linux`

  rm "$platform"
  mkdir "$platform"
  cd "$platform"

  for f in "$GOROOT/pkg/$platform/"*.h; do
    ln -s "$f"
  done

  export GOROOT="$srcdir/build/go"
  export GOPATH="$srcdir/build"

  go get -fix "$_gourl"

  # Prepare executable
  if [ -d "$srcdir/build/src" ]; then
    cd "$srcdir/build/src/$_gourl"
    go build -o "$srcdir/build/$pkgname"
  else
    echo 'Old sources for a previous version of this package are already present!'
    echo 'Build in a chroot or uninstall the previous version.'
    return 1
  fi
}

package() {
  export GOROOT="$GOPATH"

  # Package go package files
  for f in "$srcdir/build/go/pkg/"* "$srcdir/build/pkg/"*; do
    # If it's a directory
    if [ -d "$f" ]; then
      cd "$f"
      mkdir -p "$pkgdir/$GOROOT/pkg/`basename $f`"
      for z in *; do
        # Check if the directory name matches
        if [ "$z" == `echo $_gourl | cut -d/ -f1` ]; then
          cp -r $z "$pkgdir/$GOROOT/pkg/`basename $f`"
        fi
      done
      cd ..
    fi
  done

  # Package source files
  if [ -d "$srcdir/build/src" ]; then
    mkdir -p "$pkgdir/$GOROOT/src/pkg"
    cp -r "$srcdir/build/src/"* "$pkgdir/$GOROOT/src/pkg/"
    find "$pkgdir" -depth -type d -name .git -exec rm -r {} \;
  fi

  # Package license (if available)
  for f in LICENSE COPYING; do
    if [ -e "$srcdir/build/src/$_gourl/$f" ]; then
      install -Dm644 "$srcdir/build/src/$_gourl/$f" \
        "$pkgdir/usr/share/licenses/$pkgname/$f"
    fi
  done

  # Package executables
  if [ -e "$srcdir/build/$pkgname" ]; then
    install -Dm755 "$srcdir/build/$pkgname" \
      "$pkgdir/usr/bin/$pkgname"
  fi
}

# vim:set ts=2 sw=2 et:
```