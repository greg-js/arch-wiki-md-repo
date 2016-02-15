因為有 ABS，Arch 用戶可輕易將源代碼編譯為一個 .pkg.tar.gz **安裝包**.

## Contents

*   [1 什么是安裝包文件？](#.E4.BB.80.E4.B9.88.E6.98.AF.E5.AE.89.E8.A3.9D.E5.8C.85.E6.96.87.E4.BB.B6.EF.BC.9F)
*   [2 什么是 PKGBUILD 文件，其內容是什么？](#.E4.BB.80.E4.B9.88.E6.98.AF_PKGBUILD_.E6.96.87.E4.BB.B6.EF.BC.8C.E5.85.B6.E5.85.A7.E5.AE.B9.E6.98.AF.E4.BB.80.E4.B9.88.EF.BC.9F)
    *   [2.1 構建函數之解釋](#.E6.A7.8B.E5.BB.BA.E5.87.BD.E6.95.B8.E4.B9.8B.E8.A7.A3.E9.87.8B)
    *   [2.2 更多 ABS 相關資訊](#.E6.9B.B4.E5.A4.9A_ABS_.E7.9B.B8.E9.97.9C.E8.B3.87.E8.A8.8A)

# 什么是安裝包文件？

記住，ABS自動為你要編譯的那個軟體下載源代碼。然後解包，編譯，然後將編譯好的文件壓入一個安裝包中。
一般來說，得到的這個安裝包文件就是一個以 .pkg.tar.gz 結尾的文件，例如：_foo_.pkg.tar.gz.

事實上，它不僅僅是一個 gzip 壓縮過的 tar 檔案文件（'tarball'），它含有：

*   將要安裝的文件

*   .PKGINFO: 包含 pacman 要處理的安裝包，依賴性文件等所有的元數據。

*   .FILELIST: 該文件記錄了檔案中所有文件的列表。它被用於反安裝軟體，或檢查衝突文件。

*   .INSTALL: 該文件用在安裝/升級/刪除的階段之後執行命令(僅當 PKGBUILD 中創造出指定時，該文件才會存在)

因為 pacman 能管理 tar.gz 安裝包， 于是，用 ABS 創建的 ***.pkg.tar.gz 就能輕易被安裝或刪除了。

# 什么是 PKGBUILD 文件，其內容是什么？

前面解釋過了 PKGBUILD 文件，它記錄了一個安裝包的元數據。它是一個文本文件。這裡是一個例子：

```
# $Id: PKGBUILD,v 1.12 2003/11/06 08:26:13 dorphell Exp $
# Maintainer: judd <jvinet@zeroflux.org>
# Contributor: Judd Vinet <jvinet@zeroflux.org>
pkgname=foo
pkgver=0.99 # note: if the pkgver had been '0.99-10' then use an underscore, i.e. '0.99_10'
pkgrel=1
pkgdesc="short description of foo"
arch=(i686 x86_64)
url="http://www.foo.org"
license=('GPL')
groups=
provides=
depends=('qt' 'python')
makedepends=('guile')
conflicts=('yafoo')
replaces=('mffoo')
backup=('etc/foo/foo.conf')
install=('foo.install')
source=(http://www.foo.org/download/$pkgname-$pkgver.tar.gz)
md5sums=('2c0cca3ef6330a187c6ef4fe41ecaa4d35175bee593a7cc7d6205584a94d8625')

build() {
  cd $startdir/src/$pkgname-$pkgver
  ./configure --prefix=/usr
  make || return 1
  make prefix=$startdir/pkg/usr install
}

```

現在讓我們來逐條解釋一下：

*   **# abc ...** : 這是註釋文字
*   **# $Id: PKGBUILD,v ...**: 該安裝包的 cvs 標籤 (從 archlinux-cvs 系統創建)
*   **# Maintainer**: 在官方軟體庫中負責此安裝包的維護人
*   **# Contributor**: 寫出此安裝包 PKGBUILD 文件的第一人
*   **pkgname**: 安裝包名稱
*   **pkgver**: 安裝包的版本號
*   **pkgrel**: 此 Arch 安裝包的釋出號。它不同於版本號。當PKGBUILD 文件有改動時，釋出號就改變了。這種情況有多種原因，例如你為某個包開啟了編譯時間支援。
*   **pkgdesc**: 安裝包的簡明描述。這也是你瀏覽[package database](https://archlinux.org/packages/)時會見到的。
*   **arch**: 表明它在哪種架構下構建和工作的，軟體移植的細節可參閱[Arch64_FAQ](/index.php/Arch64_FAQ "Arch64 FAQ")。
*   **url**: 軟體的主頁 (當你在安裝包數據庫中點擊它時候，就能出現了)
*   **license**: 基於哪種軟體發佈許可
*   **groups**: 這一倏用於為軟體分組；例如當你要安裝 KDE 時，它就會安裝屬於 KDE 軟體組的所有安裝包。
*   **provides**: 如果一個安裝包也提供了其它包的安裝，那就使用它。例如，kernel-scsi 也提供了 kernel 的安裝包。
*   **depends**: 它列出了安裝包運行時的依賴軟體 (必須有這些軟體才能正常工作)
*   **makedepends**: 在構建安裝包時需要的依賴性軟體，不過一旦已經構建好的，就不再需要了。
*   **conflicts**: 這些包不能被同時安裝。這裡 _foo_ 跟 _yafoo (另外一個 foo)_ 有衝突。它們不能共存。
*   **replaces**: 新安裝包代替了舊的。這裡， _mffoo (第一個 foo)_ 不再受到支持了，被 _foo_ 所代替。
*   **backup**: 當刪除安裝包時，用哪個文件作為備份文件(如 file.pacsave) 。
*   **install**: 指定一個特別安裝腳本，它將被包含在安裝包中(必須跟 PKGBUILD 在同一個目錄下)
*   **source**: 它指定了從何處下載該安裝包的源代碼包。它可以在本地電腦上，也可以是從 "http" 或 "ftp" 上取得的。它用 _pkgver_ 來命名，以免每次源碼包變動時，源碼的名稱也要跟著變化。
*   **md5sums**: 計算源代碼包的 md5 值，以查驗完整性。

現在來解釋一下函數：

*   build: 構建一個安裝包時所需要的所有動作(稍候本文將作更詳細的說明)

好，你看到了 PKGBUILD 文件含有包管理器可能需要的所有資訊，它是 pacman 和 abs 的核心。

還會有些安裝文件。這個 PKGBUILD 指定了 'foo.install' 作為安裝包的安裝文件。這是例子：

```
post_install() {
/bin/true
}

post_upgrade() {
/bin/true
}

pre_remove() {
/bin/true
}

op=$1
shift

$op "$@"

```

其中的函數說明如下：

*   post_install: 文件一裝完，此腳本就運行。它跟了一行命令：
    *   對本安裝包版本操作
*   post_upgrade: 文件一升級完，此腳本就運行。它跟了兩行命令：
    *   對新安裝包版本操作
    *   對舊安裝包版本操作
*   pre_remove: 此腳本運行於文件刪除前（例如停止了一個守護進程）。它跟了一行命令：
    *   對本安裝包版本操作

底下的那三行是每一個安裝文件都需要的，以便安裝文件正常運行。

## 構建函數之解釋

那么來看看上面例子中用到的 ABS 的構建函數。注意 build 一節：

```
build() {
  cd $startdir/src/$pkgname-$pkgver
  ./configure --prefix=/usr
  make || return 1
  make prefix=$startdir/pkg/usr install
}

```

發生了什么：

*   進入源代碼包的解壓目錄：

 `cd $startdir/src/$pkgname-$pkgver` 

*   配置安裝包，並告訴它安裝到 `/usr` 這個目錄下：

 `  ./configure --prefix=/usr` 

*   編譯

 `  make || return 1` 

*   軟體不直接安裝到 `/usr` 下，而是裝到 `$startdir/pkg/usr` 下，以便 pacman 能控制這些文件。

 `  make prefix=$startdir/pkg/usr install` 

我們想要做的是構建這個安裝包，而不是去安裝它。所以我們告訴 `make` 將所有的文件放到指定目錄下面 `$startdir/pkg/usr` ，而不是安裝到標準的位置 `/usr` 。
這樣一來， makepkg 就能查看到這個安裝包要安裝哪些個文件了，並將其壓縮成 Arch 安裝包。

**注意**: 有時候，`Makefile` 中並未使用 `prefix` ；經常是用了 `DESTDIR` 。如果此安裝包是用 autoconf/automake 來構建的，就用 `DESTDIR` 。這是在手冊中 [詳細說明了的](http://sources.redhat.com/automake/automake.html#Install)。檢查一下產生的 `filelist` 是否比平常小很多，如果是這樣的話，嘗試用 `make DESTDIR=$startdir/pkg install` 來構建。如果不能正常工作，那就要深入研究一下安裝命令了，它們位於 "`make <...> install=`" 中。

## 更多 ABS 相關資訊

*   [ABS](/index.php/ABS "ABS") The Arch Build System
*   [Creating packages](/index.php/Creating_packages "Creating packages")
*   [Makepkg](/index.php/Makepkg "Makepkg")
*   [Safe Cflags](/index.php/Safe_Cflags "Safe Cflags")
*   [Kernel Compilation with ABS](/index.php/Kernel_Compilation_with_ABS "Kernel Compilation with ABS")
*   [Arch User Repository](/index.php/Arch_User_Repository "Arch User Repository")
*   [Custom local repository with ABS and gensync](/index.php/Custom_local_repository_with_ABS_and_gensync "Custom local repository with ABS and gensync")