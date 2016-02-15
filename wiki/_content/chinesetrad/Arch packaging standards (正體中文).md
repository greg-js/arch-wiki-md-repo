## Contents

*   [1 套件規範](#.E5.A5.97.E4.BB.B6.E8.A6.8F.E7.AF.84)
    *   [1.1 套件命名規則](#.E5.A5.97.E4.BB.B6.E5.91.BD.E5.90.8D.E8.A6.8F.E5.89.87)
    *   [1.2 目錄](#.E7.9B.AE.E9.8C.84)
    *   [1.3 makepkg 的責任](#makepkg_.E7.9A.84.E8.B2.AC.E4.BB.BB)
        *   [1.3.1 Submitting Packages to the AUR](#Submitting_Packages_to_the_AUR)
    *   [1.4 套件規矩](#.E5.A5.97.E4.BB.B6.E8.A6.8F.E7.9F.A9)
    *   [1.5 許可](#.E8.A8.B1.E5.8F.AF)
    *   [1.6 提交套件](#.E6.8F.90.E4.BA.A4.E5.A5.97.E4.BB.B6)
*   [2 其他指導方針](#.E5.85.B6.E4.BB.96.E6.8C.87.E5.B0.8E.E6.96.B9.E9.87.9D)
    *   [2.1 CVS/SVN 套件](#CVS.2FSVN_.E5.A5.97.E4.BB.B6)
    *   [2.2 Java 套件](#Java_.E5.A5.97.E4.BB.B6)

## 套件規範

### 套件命名規則

*   套件名稱只能以數字跟字母組成，且全部都需為小寫。
*   版本號(version)要跟原作者釋出的相同。版本號可以由字母、數字跟 '.' 組成，但不能有 '-'。
*   釋出版號(release)是 Arch Linux 特有的，這用來讓使用者識別新舊版本。當一個新的套件釋出，釋出版號(release) 是從 1 開始算，當之後有作修正或是最佳化的版本釋出的話，釋出版號(release) 則累加 1。當原作者釋出新版的話，則釋出版號(release)重設為 1。釋出版號(release)與版本號(version)遵守相同的命名規則。
*   例如：目前最新的 nmap 版本為 4.20-1，4.20即為版本號(version)，'-1'的部份表示釋出版號(release)為1。

### 目錄

*   設定檔要被放在 <tt>/etc</tt> 目錄內。如果有超過一個以上的設定檔，應該在 <tt>/etc</tt> 內建立子目錄來放置，以保持 <tt>/etc</tt> 的整潔。使用如 <tt>/etc/{套件名}/</tt> 目錄來放置對應套件的設定檔，或是選用一個具有代表意義的亦可。
*   套件本身的檔案要遵守以下的規範：
    *   <tt>/etc</tt>: 系統必備的設定檔
    *   <tt>/usr/bin</tt>: 應用程式執行檔
    *   <tt>/usr/sbin</tt>: 系統執行檔
    *   <tt>/usr/lib</tt>: 函式庫
    *   <tt>/usr/include</tt>: 標頭檔
    *   <tt>/usr/lib/{pkg}</tt>: 套件 {pkg} 的模組、外掛等等
    *   <tt>/usr/man</tt>: Manpages
    *   <tt>/usr/share/{pkg}</tt>: 套件 {pkg} 的資料
    *   <tt>/etc/{pkg}</tt>: 套件 {pkg} 的設定檔
    *   <tt>/opt</tt>: Large self-contained packages such as KDE, Mozilla, etc.

### makepkg 的責任

當你使用 makepkg 來製作套件時，它會自動為你做下列動作：

1.  檢查套件的相依套件是否已被安裝
2.  從伺服器上下載原始碼
3.  解開原始碼
4.  使用需要的補丁
5.  編譯此軟體，並安裝在假的根目錄
6.  移除 <tt>/usr/doc, /usr/info, /usr/share/doc, /usr/share/info</tt> 這些目錄中此軟體安裝的資料
7.  去除掉二進位執行檔中的符號(symbols)
8.  去除掉函式庫中的除錯用符號
9.  產生每個套件中都會有的 meta file
10.  將假的根目錄壓縮起來成為套件檔
11.  將套件存在設定好的目的資料夾（預設是目前目錄）

#### Submitting Packages to the AUR

Note the following before submitting any packages to the AUR:

1.  The submitted PKGBUILDs **MUST NOT** build applications already in any of the official binary repositories under any circumstances. Exception to this strict rule may only be packages having extra features enabled and/or patches in compare to the official ones. In such an occasion the pkgname array should be different to express that differency. eg. A GNU screen PKGBUILD submitted containing the sidebar patch, could be named screen-sidebar etc. Additionally the **provides**('screen') PKGBUILD array should be used in order to avoid conflicts with the official package.
2.  To ensure the security of pkgs submitted to the AUR please **ensure** that you have correctly filled the `md5sum` field. The `md5sum`'s can be generated using the `makepkg -g` command.
3.  Please **add a comment line** to the top of your `PKGBUILD` file that follows this format: `# Contributor: Your Name <your.email>` 
4.  Verify the package **dependencies** (eg, run `ldd` on dynamic executables, check tools required by scripts, etc). The TU team **strongly** recommend the use of the `namcap` utility, written by Jason Chu (jason@archlinux.org), to analyze the sanity of your package. `namcap` will tell you about bad permissions, missing dependencies, un-needed dependencies, and other common mistakes. You can install the `namcap` package with `pacman`. Remember `namcap` can be used to check both pkg.tar.gz files and PKGBUILDs
5.  **Dependencies** are the most common packaging error. Namcap can help detect them, but it is not always correct. Verify dependencies by looking at source documentation and the program website.
6.  **Don't use <tt>replaces</tt>** in your PKGBUILD unless you want to rename your package, for example when _Ethereal_ became _Wireshark_. If you just provide an alternate version of an already existing package, use <tt>conflicts</tt> (and <tt>provides</tt> if that package is required by others). The main difference is: after syncing (-Sy) pacman immediately wants to replace an installed, 'offending' package upon encountering a package with the matching <tt>replaces</tt> anywhere in its repositories; <tt>conflicts</tt> on the other hand is only evaluated when actually installing the package, which is pretty much always the desired behavior because you don't push your package down other people's throat this way.
7.  All files uploaded to the AUR should be contained in a **compressed tar file** containing a directory with the **`PKGBUILD`** and **additional build files** (patches, install, ...) in it.

    ```
    foo/PKGBUILD
    foo/foo.install
    foo/foo_bar.diff
    foo/foo.rc.conf
    ```

    The archive name should contain the name of the package e.g. foo.tar.gz

    The tarball **should not** contain the binary tarball created by makepkg, nor should it contain the filelist

### 套件規矩

### 許可

### 提交套件

## 其他指導方針

### CVS/SVN 套件

### Java 套件