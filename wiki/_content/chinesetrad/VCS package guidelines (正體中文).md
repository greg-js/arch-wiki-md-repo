## Contents

*   [1 用 makepkg 打包 CVS, SVN & GIT 文件](#.E7.94.A8_makepkg_.E6.89.93.E5.8C.85_CVS.2C_SVN_.26_GIT_.E6.96.87.E4.BB.B6)
    *   [1.1 一些小提示](#.E4.B8.80.E4.BA.9B.E5.B0.8F.E6.8F.90.E7.A4.BA)
    *   [1.2 CVS PKGBUILD 樣例](#CVS_PKGBUILD_.E6.A8.A3.E4.BE.8B)
    *   [1.3 SVN PKGBUILD 樣例](#SVN_PKGBUILD_.E6.A8.A3.E4.BE.8B)
    *   [1.4 GIT PKGBUILD 樣例](#GIT_PKGBUILD_.E6.A8.A3.E4.BE.8B)
    *   [1.5 versionpkg - a makepkg wrapper for CVS/SVN builds](#versionpkg_-_a_makepkg_wrapper_for_CVS.2FSVN_builds)
        *   [1.5.1 看看這個腳本!](#.E7.9C.8B.E7.9C.8B.E9.80.99.E5.80.8B.E8.85.B3.E6.9C.AC.21)

## 用 makepkg 打包 CVS, SVN & GIT 文件

事實上，這個工作非常簡單，您不需要什麼特殊的知識。不管怎麼樣，您對CVS和SVN的知識懂得越多越好。很多人在 PKGBUILD 文件裏面引入了不必要（譯注：這個詞是譯者加的，在儘量不影響理解的前提下，譯者可能會不自覺的使用自己的語言，後面不再聲明）的自定義變數，這樣會使工作變得複雜。這些看起來很複雜的語句並不是*必須的*，但是對於使語法結構清洗，是很有幫助的。

### 一些小提示

*   給 `pkgname` 加上 `-cvs` 或者 `-svn` 或者 `-git` 這樣的尾碼 （where applicable， 這個不知道怎麼翻譯） - 這樣可以防止和非devel版本的包名混淆，比如 fluxbox-svn ， fvwm-cvs 對 fluxbox ， fvwm.
*   您還必須小心處理 pacman 的衝突（依賴關係衝突）。比如 fluxbox-svn will 與 fluxbox 衝突。這樣您就需要使用 <tt>conflicts=</tt> 欄位（field）

```
conflicts=('fluxbox')

```

	您還應該使用 <tt>provides=</tt> 欄位，以便讓需要 fluxbox （作者這裏用fluxbox來舉例）的包知道 fluxbox-svn 就是 fluxbox

```
provides=('fluxbox')

```

	您最好不要使用(your should avoid using) <tt>replaces=</tt> ，它可能會產生不必要的麻煩

*   When using/defining the cvsroot use anonymous**:**@ rather than anonymous@ to avoid having to press enter to give blank password *OR* anonymous**:password**@ - if a password is required.
*   cvs and svn PKGBUILDs may not require a source or md5sum array but these fields **must** be included in the PKGBUILD if you wish to submit it to the AUR, otherwise the pkg will be rejected. They may be left blank though.

```
source=()
md5sums=()
```

*   使用 CVS/SVN/GIT 的時候，我們極少用到 pkgrel 欄位，因為原始檔案時有改動，所以我們通常用 pkgver 來標記改動（假定我們用 pkgver 來保存日期）（英文原文：It is rarely necessary to use the pkgrel field when building CVS/SVN/GIT pkgs - any changes to the pkg will often be on another day and so are usually accounted for by a change in pkgver (assuming pkgver is used to hold a date format)，英語不到家，有人會翻譯的mail:fluke at sfcube.net）
*   不要忘記把 svn 或者 cvs 包含在 `makedepends=` 裏面，如果必須的話（譯注：如果你要從 svn 來 checkout 源碼包，自然要要保證你有 svn 用戶端）
*   為了保證 check out(譯注：cvs和svn的術語，就不翻譯了) 下來的 code 的完整性，我們建立一個獨立的 build 目錄，比如你已經在 $startdir 把代碼 ckeck out 到了 src/$_cvsmod 目錄你可以:

```
  mkdir src/$_cvsmod-build

  cd src/$_cvsmod-build
  ../$_cvsmod/configure
```

*萬一* 這種方法失敗了，你可以嘗試：

```
  cp -r src/$_cvsmod src/$_cvsmod-build
  cd src/$_cvsmod-build
```

*   AUR的介紹中說最重要的是不要使用 backtick 擴展去創建 pkg 變數(With the introduction of the AUR it is most important to avoid using backtick execution to create pkg variables)
    *   對於 cvs 包 您應該避免 `pkgver=`date +%y%m%d`` - （譯注：this also inteferes with the functionality of the AUR.，這句話不好翻譯，我不知道inteferes什麼意思） 作為替代的方案，還可以用日期格式的 $pkgver 變數，並且使用 cvs -D 去獲取從那個日期起的代碼 （看下面）
    *   對於 svn 您可以使用修正號(revision number)。下面是一種簡易的獲取修正號的方法：

```
svn log $_svntrunk --limit 1 | grep -m 1 -o "r.*" | cut -d \| -f 1 | sed s@r@@g

```

這條命令從 svn repo (譯注：就是 svn 的源)最近額記錄裏面取得修正號--修正號的前面帶有*r*字母。下面的來自於 fluxbox 的 svn 記錄，修正號就在左上角，r4084。

```
------------------------------------------------------------------------
r4084 | mathias | 2005-07-20 19:29:01 +0100 (Wed, 20 Jul 2005) | 16 lines

Changed some *Focus options, just to make some things a bit more clear.
the "Sloppy" was always a bit .. unprecise.

```

### CVS PKGBUILD 樣例

這裏用一個 bmp-cvs 的 PKGBUILD 來說明上面的一些技巧（一些小提示）

```
# Contributor:  Lukas Sabota <punkrockguy318@comcast.net>
# Contributor: dibblethewrecker dibblethewrecker.at.jiwe.dot.org
pkgname=bmp-cvs
pkgver=20050728
pkgrel=1
pkgdesc="BeepMP is a multimedia player that uses the WinAmp 2.x UI, GTK2, and is based on XMMS. This will checkout and package the latest CVS version."
url="http://beepmp.sourceforge.net/"
license=
depends=('gtk2' 'libvorbis' 'alsa-lib' 'audiofile' 'libglade' 'id3lib' 'x-server')
provides=('bmp')
conflicts=('bmp')
makedepends=('cvs')
install=$pkgname.install

_cvsroot=":pserver:anonymous:@cvs.sourceforge.net:/cvsroot/beepmp"
_cvsmod="bmp"

build() {
  cd $startdir/src
  msg "Connecting to $_cvsmod.sourceforge.net CVS server...."
  cvs -z3 -d $_cvsroot co -D $pkgver -f $_cvsmod
  cd $_cvsmod
  ./autogen.sh

  msg "CVS checkout done or server timeout"
  msg "Starting make..."

  cp -r ../$_cvsmod ../$_cvsmod-build
  cd ../$_cvsmod-build

  ./configure --prefix=/usr
  make || return 1
  make DESTDIR=$startdir/pkg install || return 1

  mkdir -p $startdir/pkg/usr/share/xmms/Skins
  mv $startdir/pkg/usr/share/bmp/Skins/* $startdir/pkg/usr/share/xmms/Skins
  rmdir $startdir/pkg/usr/share/bmp/Skins

  rm -r $startdir/src/$_cvsmod-build
}
# vim:syntax=sh

```

### SVN PKGBUILD 樣例

假如您第一次對 PKGBUILD 使用 <tt>source</tt> 命令，它會填充(store) _svntrunk 和 _svnmod 變數。所以如果您運行：

```
source PKGBUILD
svn log $_svntrunk --limit 1 | grep -m 1 -o "r.*" | cut -d \| -f 1 | sed s@r@@g

```

你可以得到用於 pkgver 的修正號

```
# Contributor:  Lukas Sabota <punkrockguy318@comcast.net>
# Contributor: dibblethewrecker dibblethewrecker.at.jiwe.dot.org
pkgname=fluxbox-svn
pkgver=4084
pkgrel=1
pkgdesc="Fluxbox-svn is the bleeding edge version of a lightweight yet \
customizable windowmanager for X. This will checkout and package the latest SVN version."
url="http://www.fluxbox.org"
depends=('bash' 'x-server')
makedepends=('subversion')
conflicts=('blackbox' 'fluxbox' 'fluxbox-devel' 'fluxbox-cvs')
replaces=('fluxbox-cvs')
provides=('fluxbox')

_svntrunk=svn://svn.berlios.de/fluxbox/trunk
_svnmod=fluxbox

build() {
  cd $startdir/src

  svn co $_svntrunk --config-dir ./ -r $pkgver $_svnmod
  cd $_svnmod
  ./autogen.sh

  msg "SVN checkout done or server timeout"
  msg "Starting make..."

  mkdir ../$_svnmod-build
  cd ../$_svnmod-build

  # fix for crap fb issue
  mkdir data
  cp ../$_svnmod/data/keys data/

  ../$_svnmod/configure --prefix=/usr --enable-xinerama --enable-imlib2 --enable-debug
  #./configure --prefix=/usr --enable-xinerama --enable-imlib2 --enable-debug
  make || return 1
  make DESTDIR=$startdir/pkg/ install

  rm -r $startdir/src/$_svnmod-build
}
# vim:syntax=sh
```

### GIT PKGBUILD 樣例

```
pkgname=compiz-git
pkgver=20060707
pkgrel=1
pkgdesc="Composite and window manager for Xgl"
url="http://en.opensuse.org/Compiz"
license=""
depends=('xgl-cvs' 'mesa-xgl-cvs' 'cairo-devel' 'libxevie' \
         'startup-notification' 'libpng'  'libxdamage' \
         'libxrandr' 'libwnck-compiz' 'gnome-desktop' 'control-center' \
         'libsvg-cairo' 'libxcomposite')
makedepends=('git')
conflicts=()
replaces=()
backup=()
install=compiz.install
source=(compiz-intel-copy-pixel-issue-workaround-1.diff)
md5sums=('10a157b86d528bca2be6731c5eaff7b3')

_gitroot="git://anongit.freedesktop.org/git/xorg/app/compiz"
_gitname="compiz"
build() {
export CFLAGS="$CFLAGS -I/opt/mesa-xgl-cvs/include"
  cd $startdir/src
  msg "Connecting to git.freedesktop.org GIT server...."

  if [ -d $startdir/src/$_gitname ] ; then
  cd $_gitname && git-pull origin
  msg "The local files are updated."
  else
  git clone $_gitroot
  fi

  msg "GIT checkout done or server timeout"
  msg "Starting make..."

  cp -r $startdir/src/$_gitname $startdir/src/$_gitname-build
  cd $startdir/src/$_gitname-build
  patch -Np0 -i ${startdir}/src/compiz-intel-copy-pixel-issue-workaround-1.diff

  ACLOCAL="aclocal -I /opt/gnome/share/aclocal" ./autogen.sh --host=${CHOST} \
    --prefix=/usr \
    --infodir=/usr/share/info \
    --mandir=/usr/share/man \
    --sysconfdir=/opt/gnome/etc \
    --enable-gnome \
    --enable-libsvg-cairo \
    --enable-gconf-dump \
    --disable-kde || return 1
  make || return 1
  make DESTDIR=$startdir/pkg install

  find $startdir/pkg -type f -name '*.la' -exec rm {} \;
} 

```

如您所見，我在 pkgname 後面使用 "-git" 尾碼，另外兩個變數 -- _gitroot 和 _gitname 用來表示包的“源”和包名字。 我需要解釋一個 if 條件：

```
if [ -d $startdir/src/$_gitname ] ; then
cd $_gitname && git-pull origin
msg "The local files are updated."
else
git clone $_gitroot
fi

```

因為我們有兩個命令，一個用來更新，一個迎來取得代碼。我把源代碼 copy 到一個 "-build" 目錄（在 cvs 和 svn 版本的包裏面，我們也這樣做）。

### versionpkg - a <tt>makepkg</tt> wrapper for CVS/SVN builds

這是一個很簡單的腳本，它能夠讓你在不改動 PKGBUILD 檔裏面的日期或者修正號的前提下更新你的 CVS 或者 SVN 包。

簡單地在你的 build 目錄運行這個命令，代替 <tt>makepkg</tt>。這個腳本完全免除了用 backtick 擴展來設置 PKGBUILD 中的日期或者版本標記的必要。 （This script completely removes the need for backtick execution to set the date or tag version in PKGBUILDs.）

使用這個腳本之前;

*   確保在 PKGBUILD 的前10行的位置已經聲明了 pkgver， 否則這個腳本不會正常工作！
*   確保你的檔包含了下面的變數以及 checkout 命令：
*   CVS

```
_cvsroot=

```

	CVS 伺服器根目錄(The root of the CVS server) - 即的包含一個半形冒號 (:) 在用戶名後面，就像上面提到的一樣。

```
_cvsmod=

```

	你要 check out 的 CVS 模組，如：

```
_cvsroot=":pserver:anonymous:@mplayerhq.hu:/cvsroot/ffmpeg"
_cvsmod="ffmpeg"

```

	下面這個 check out 的例子用到了上面提到的變來嗯。**-D** 選項對於正確使用 `versionpkg` 是必須的，它和 **-f** 選項是很好的組合. 在不使用 **-f** 選項的情況下使用 **-D** 可能會導致錯誤

```
cvs -z9 -q -d $_cvsroot co -D $pkgver -f $_cvsmod

```

	-z 控制壓縮級別（1低9高）

	-D 指定 check out 的日期，這這個腳本裏面我們用 $pkgver 來在設置時間。

	-q 是 quiet （關閉詳細資訊）模式開關。

*   SVN

```
_svntrunk=

```

	SVN trunk 地址 （譯注，相當於 CVS root）

```
_svnmod=

```

	在說一次，這個是你想要 ckeck out 的模組名，如：

```
_svntrunk=[svn://svn.berlios.de/fluxbox/trunk](svn://svn.berlios.de/fluxbox/trunk)
_svnmod=fluxbox

```

	下面這個例子使用了上面的變數。**-r** 選項對於正確使用 `versionpkg` 是必要的（譯注，這個是用來設置修改號的，顯然）.

```
svn co $_svntrunk --config-dir ./ -r $pkgver $_svnmod

```

	這裏的 -r 指定修改號, 我們用 $pkgver 來表示修改號。

#### 看看這個腳本!

為了提高安全性， versionpkg 現在可以直接從 [community] 安裝，`pacman -S versionpkg`。 我強烈建議您這樣做（I strongly recommend that you use that. ）下面的腳本純粹用來解釋 :)
Changelog （修改記錄）:

*   check for both CVS/SVN vars (檢查 SVN 和 CVS vars)
*   如果失敗了，就回退到上一個 pkgver ，以便允許正確的 gensync 操作（譯注，我不知道 gensync, 從名字看應該是和更新有關，英文原文：If build fails revert to previous pkgver to allow correct gensync operation）
*   加入了有色消息（coloured messages）的支援

```
#!/bin/bash

# versionpkg - a makepkg wrapper for building CVS/SVN pkgs
# dibblethewrecker.at.jiwe.org

# makepkg configuration
[ -f /etc/makepkg.conf ] && source /etc/makepkg.conf

# SUBROUTINES
plain() {
	if [ "$USE_COLOR" = "Y" -o "$USE_COLOR" = "y" ]; then
		echo -e "    \033[1;1m$1\033[1;0m" >&2
	else
		echo "    $1" >&2
	fi
}
msg() {
	if [ "$USE_COLOR" = "Y" -o "$USE_COLOR" = "y" ]; then
		echo -e "\033[1;32m==>\033[1;0m \033[1;1m$1\033[1;0m" >&2
	else
		echo "==> $1" >&2
	fi
}
warning() {
	if [ "$USE_COLOR" = "Y" -o "$USE_COLOR" = "y" ]; then
		echo -e "\033[1;33m==> WARNING:\033[1;0m \033[1;1m$1\033[1;0m" >&2
	else
		echo "==> WARNING: $1" >&2
	fi
}
error() {
	if [ "$USE_COLOR" = "Y" -o "$USE_COLOR" = "y" ]; then
		echo -e "\033[1;31m==> ERROR:\033[1;0m \033[1;1m$1\033[1;0m" >&2
	else
		echo "==> ERROR: $1" >&2
	fi
	return 1
}

source ./PKGBUILD
oldpkgver=$pkgver

if [ ! -z ${_cvsroot} ] && [ ! -z ${_cvsmod} ] ; then
	cvsdate=`date +%Y%m%d`
	sed -i "1,11 s|pkgver=$oldpkgver|pkgver=$cvsdate|" ./PKGBUILD
	makepkg $@
	if [ $? -gt 0 ] ; then
		error "Reverting pkgver..."
		sed -i "1,11 s|pkgver=$cvsdate|pkgver=$oldpkgver|" ./PKGBUILD
	fi     	
elif [ ! -z ${_svntrunk} ] && [ ! -z ${_svnmod} ] ; then
	svnrevno=`svn log $_svntrunk --limit 1 | grep -m 1 -o "r.*" | cut -d \| -f 1 | sed s@r@@g`
	msg "Current revision number is $svnrevno"
	if [ "${1}" != "-f" ] && [ "${oldpkgver}" == "${svnrevno}" ] ; then
		error "No new revision available.  (use -f to overwrite)"
		exit
	fi
	sleep 3
	sed -i "1,11 s|pkgver=$oldpkgver|pkgver=$svnrevno|" ./PKGBUILD
	makepkg $@
	if [ $? -gt 0 ] ; then
		error "Reverting pkgver..."
		sed -i "1,11 s|pkgver=$svnrevno|pkgver=$oldpkgver|" ./PKGBUILD
	fi 
else
	error "No SVN or CVS variables found! Aborting..."
	exit
fi

```