p7zip 是 [7-Zip](https://en.wikipedia.org/wiki/7zip "wikipedia:7zip") 的 [POSIX](https://en.wikipedia.org/wiki/POSIX "wikipedia:POSIX") 實作，支援Linux。

## Contents

*   [1 安裝＆使用](#.E5.AE.89.E8.A3.9D.EF.BC.86.E4.BD.BF.E7.94.A8)
*   [2 範例](#.E7.AF.84.E4.BE.8B)
*   [3 7z, 7za 與 7zr 之差異](#7z.2C_7za_.E8.88.87_7zr_.E4.B9.8B.E5.B7.AE.E7.95.B0)
*   [4 參見](#.E5.8F.83.E8.A6.8B)

## 安裝＆使用

可以從[官方軟體庫](/index.php/Official_repositories "Official repositories")中[安裝](/index.php/Pacman "Pacman")[p7zip](https://www.archlinux.org/packages/?name=p7zip)。

透果以下指令可以執行p7zip：

```
# 7z

```

## 範例

不指定解壓縮目錄，直接解壓縮到目前資料夾內，執行下面指令:

```
# 7z e <壓縮檔名稱>

```

實例：

```
# 7z e test.7z

```

此種方式會將壓縮檔內所有檔案解壓縮於同一資料夾內，無視壓縮檔內的路徑。

解壓縮檔案，使用完整路徑，執行下面指令：

```
# 7z x <壓縮檔名稱>

```

實例：

```
# 7z x test.7z

```

解壓縮檔案，並且指定輸出目錄，加上-o參數，如下面指令：

```
# 7z x -o<資料夾名稱> <壓縮檔名稱>

```

實例：

```
# 7z x -o./outdir test.7z

```

## 7z, 7za 與 7zr 之差異

軟體包中包含三個可執行二進制檔案 `/usr/bin/7z`、`/usr/bin/7za`及 `/usr/bin/7zr`。 他們的手冊解釋他們的差異之處：

*   7z 使用外掛（Plugins）去操作壓縮檔。
*   7za 可獨立執行。 7za 可以使用的壓縮檔種類較7z少，但是他不需要其他外掛。
*   7zr 可獨立執行。 7zr 可以使用的壓縮檔種類較7z少，但是他不需要其他外掛。 7zr是一個「輕量級」7z，所以他只能使用7z壓縮檔。

## 參見

[Homepage.](http://p7zip.sourceforge.net/)

[7zip homepage.](http://www.7-zip.org/download.html)

[How to use 7zip on Linux command Line.](https://www.ibm.com/developerworks/community/blogs/6e6f6d1b-95c3-46df-8a26-b7efd8ee4b57/entry/how_to_use_7zip_on_linux_command_line144?lang=en)