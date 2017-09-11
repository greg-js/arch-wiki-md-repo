Feh是一个轻量级、强大的图像查看器，同时它也可以用来管理桌面壁纸，特别适合缺少这类特性的独立窗口管理器。

## Contents

*   [1 安装](#.E5.AE.89.E8.A3.85)
*   [2 用法](#.E7.94.A8.E6.B3.95)
    *   [2.1 图像浏览](#.E5.9B.BE.E5.83.8F.E6.B5.8F.E8.A7.88)
        *   [2.1.1 文件浏览器图片启动器](#.E6.96.87.E4.BB.B6.E6.B5.8F.E8.A7.88.E5.99.A8.E5.9B.BE.E7.89.87.E5.90.AF.E5.8A.A8.E5.99.A8)
    *   [2.2 桌面壁纸](#.E6.A1.8C.E9.9D.A2.E5.A3.81.E7.BA.B8)
        *   [2.2.1 随机背景图片](#.E9.9A.8F.E6.9C.BA.E8.83.8C.E6.99.AF.E5.9B.BE.E7.89.87)

## 安装

feh 可从[官方源](/index.php/Official_repositories_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Official repositories (简体中文)")安装：

```
# pacman -S feh

```

## 用法

feh具有很高的可配置性。运行**feh --help**可以得到详细的选项列表。

### 图像浏览

要快速的浏览指定目录里的图像，你可以用以下参数启动feh：

```
$ feh -g 640x480 -d -S filename /path/to/directory

```

*   -g 选项强制图像的显示大小不大于640x480
*   -S filename 选项按文件名排列图像

这只是一个小例子，它还有其他大量选项可供你灵活使用。

#### 文件浏览器图片启动器

下面的脚本原来贴在 [这里](https://bbs.archlinux.org/viewtopic.php?pid=884635#p884635)，对于文件管理器很有用。它会先在 feh 中显示你选中的图片，但是它同时也允许你浏览该目录中的其他图片(按照默认顺序，也就是说，与你直接运行 "feh *" 的顺序相同)。

该脚本假设第一个参数是文件名。

```
#!/bin/bash

shopt -s nullglob

if [[ ! -f $1 ]]; then
	echo "$0: first argument is not a file" >&2
	exit 1
fi

file=$(basename -- "$1")
dir=$(dirname -- "$1")
arr=()
shift

cd -- "$dir"

for i in *; do
	[[ -f $i ]] || continue
	arr+=("$i")
	[[ $i == $file ]] && c=$((${#arr[@]} - 1))
done

exec feh "$@" -- "${arr[@]:c}" "${arr[@]:0:c}"

```

使用选中的路径调用该脚本，接着是可选的传递给 feh 的参数。这是一个你可以在文件浏览器中调用的例子：

```
 /path/to/script %f -F -Z

```

`-F` 和 `-Z` 是 feh 的参数。 `-F` 用全屏模式打开图片，`-Z` 自动缩放图片。添加 `-q` 标志 (quiet) 抑制终端中的当 feh 视图打开当前文件夹中的非图片文件时的错误输出。

### 桌面壁纸

feh也适合缺少管理桌面壁纸特性的独立窗口管理器，例如[Openbox](/index.php/Openbox "Openbox")和[Fluxbox](/index.php/Fluxbox "Fluxbox")。以下命令是一个设置初始背景的例子：

```
$ feh --bg-scale /path/to/image.file

```

其它缩放选项包含了：

```
--bg-tile FILE
--bg-center FILE
--bg-seamless FILE

```

要在下一次会话期恢复背景，把以下内容加入到你的启动文件（例如~/.xinitrc、~/.config/openbox/autostart.sh等）：

```
eval `cat ~/.fehbg` &

```

#### 随机背景图片

为了随机切换桌面壁纸，用下面的代码创建一个脚本 (例如 `wallpaper.sh`)。设置脚本为可执行 (`chmod +x wallpaper.sh`) 然后从 `~/.xinitrc` 中调用。你也可以直接把代码放置在 `~/.xinitrc` 中而不是放在单独文件中。

按照您的需要更改 `~/.wallpaper` 目录，以及 `15m` 延时 (参见 [sleep(1)](http://jlk.fjfi.cvut.cz/arch/manpages/man/sleep.1) 查看选项)。

```
#!/bin/sh

while true; do
	find ~/.wallpaper -type f \( -name '*.jpg' -o -name '*.png' \) -print0 |
		shuf -n1 -z | xargs -0 feh --bg-scale
	sleep 15m
done

```

下面的版本不会fork太多次，但是无法递归到子目录：

```
#!/bin/bash

shopt -s nullglob

cd ~/.wallpaper

while true; do
	files=()
	for i in *.jpg *.png; do
		[[ -f $i ]] && files+=("$i")
	done
	range=${#files[@]}

	((range)) && feh --bg-scale "${files[RANDOM % range]}"

	sleep 15m
done

```