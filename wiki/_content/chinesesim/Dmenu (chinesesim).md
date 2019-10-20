dmenu是一个X下的快速、轻量级的软件启动器，它从stdin读取任意文本，并创建一个菜单，每一行都有一个菜单项。 然后，用户可以通过方向键或键入名称的一部分来选择一个项目，该行就会被输出到stdout。 dmenu_run是 dmenu 发行版附带的包装器，可将其用作应用程序启动器。

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 安装](#安装)
*   [2 设置](#设置)
    *   [2.1 显示自定义项目](#显示自定义项目)
    *   [2.2 手动添加项目](#手动添加项目)
    *   [2.3 字体](#字体)
    *   [2.4 shell 别名支持](#shell_别名支持)
*   [3 延伸](#延伸)
*   [4 其他资源](#其他资源)

## 安装

[安装](/index.php/%E5%AE%89%E8%A3%85 "安装") [dmenu](https://www.archlinux.org/packages/?name=dmenu)，或者是开发者版本的 [dmenu-git](https://aur.archlinux.org/packages/dmenu-git/)。

拓展了 dmenu 的默认功能的不同补丁版本也是存在的。可以考虑从 [AUR](/index.php/AUR "AUR") 安装下列之一的包：

*   [dmenu2](https://aur.archlinux.org/packages/dmenu2/): 增加了变暗、修改透明度、下划线等功能的 dmenu 分支。

通过以下命令来运行 *dmenu*：

```
$ dmenu_run

```

## 设置

现在你可以将此命令关联到一个快捷键，很多窗口管理器和桌面环境都有设置工具可以做到，用 [xbindkeys](/index.php/Xbindkeys "Xbindkeys") 也可以做到，想得到更详细的信息参见 [Hotkeys](/index.php/Hotkeys "Hotkeys") 条目。

### 显示自定义项目

自定义项目可以通过用换行符(*
*)来分隔并输入到 *dmenu* 来让它们显示出来，比如：

```
$ echo -e "第一个
第二个
第三个" | dmenu

```

### 手动添加项目

*dmenu* 会在你的 `$PATH` 路径下的目录里查找可执行文件并生成菜单项。如果要修改 `$PATH`，参见 [environment variables](/index.php/Environment_variables "Environment variables")。

### 字体

dmenu 4.6 起 XFT 字体渲染默认启用（[4.6 发行注记](http://lists.suckless.org/dev/1511/27503.html)）。[fontconfig](https://www.archlinux.org/packages/?name=fontconfig)的[font.conf 语法](http://www.freedesktop.org/software/fontconfig/fontconfig-user.html) 会被使用。

### shell 别名支持

*dmenu* 不支持 [shell 别名](/index.php/Bash#Aliases "Bash"). 为了让 *dmenu* 能够识别别名， [安装](/index.php/%E5%AE%89%E8%A3%85 "安装") *dmenu-recent-aliases*（已从AUR移除，镜像版本在：archived in [aur-mirror](https://github.com/felixonmars/aur3-mirror/tree/master/dmenu-recent-aliases)） 包然后运行 `dmenu_run_aliases`。 别名必须要在 `~/.bash_aliases` 或者 `~/.zsh_aliases` 文件里面来让 *dmenu_run_aliases* 识别出来。

## 延伸

```
$ pacman -Ql dmenu | grep bin
dmenu /usr/bin/dmenu
dmenu /usr/bin/dmenu_path
dmenu /usr/bin/dmenu_run

```

可见/usr/bin/下有三个文件，其中**dmenu_path**和**dmenu_run**是两个shell脚本，真正的执行/显示部分都由**dmenu**完成，其中**dmenu_path**用于列出$PATH里的可执行文件，每个文件名一行，然后通过“|”传递给**dmenu**，具体语法可从**dmenu_run**里找到。 你也可以在终端里执行：

```
$ echo | dmenu

```

然后输入任意字串，这个字串就会被显示在终端里，这其实才是dmenu的核心功能。

由此配合其他工具可以完成其他任务，比如运行：

```
$ notify-send "`exec $(echo | dmenu)`"

```

你可以试着在运行后输入date，之后系统就会借助notify-send弹出日期提示。

## 其他资源

*   [dmenu](http://tools.suckless.org/dmenu) - dmenu官方网站
*   [Yeganesh](http://dmwit.com/yeganesh) - dmenu的一个前段处理器，可以按照使用频率进行排序
*   [LinuxTOY](http://linuxtoy.org/archives/dmenu.html) - dmenu运行后的效果图