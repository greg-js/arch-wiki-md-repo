**翻译状态：** 本文是英文页面 [Visual Studio Code](/index.php/Visual_Studio_Code "Visual Studio Code") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2017-11-07，点击[这里](https://wiki.archlinux.org/index.php?title=Visual+Studio+Code&diff=0&oldid=494942)可以查看翻译后英文页面的改动。

**Visual Studio Code** (**VSCode**)是一个跨平台，免费，开源 (使用MIT协议)的文本编辑器，由微软使用JavaScript和TypeScript开发 。它构建于Electron框架之上，并且极具扩展性。 可以在编辑器自带的应用商店，或者从 [https://marketplace.visualstudio.com/VSCode](https://marketplace.visualstudio.com/VSCode) 中安装扩展。 微软在AUR中提供了一个专有的二进制构建版[visual-studio-code](https://aur.archlinux.org/packages/visual-studio-code/)（使用一个最终用户许可协议授权）供普通用户使用。

## Contents

*   [1 安装](#.E5.AE.89.E8.A3.85)
*   [2 调试 C#](#.E8.B0.83.E8.AF.95_C.23)
*   [3 命令行启动](#.E5.91.BD.E4.BB.A4.E8.A1.8C.E5.90.AF.E5.8A.A8)
*   [4 配置](#.E9.85.8D.E7.BD.AE)
*   [5 集成终端](#.E9.9B.86.E6.88.90.E7.BB.88.E7.AB.AF)
*   [6 外部终端](#.E5.A4.96.E9.83.A8.E7.BB.88.E7.AB.AF)

## 安装

下列安装包包含了 VSCode:

*   [visual-studio-code-bin](https://aur.archlinux.org/packages/visual-studio-code-bin/)
*   [visual-studio-code-oss](https://aur.archlinux.org/packages/visual-studio-code-oss/)
*   [visual-studio-code-git](https://aur.archlinux.org/packages/visual-studio-code-git/)
*   *code-oss*，来自非官方的 [pkgbuild-current](/index.php/Unofficial_user_repositories#pkgbuild-current "Unofficial user repositories") ，更多信息可以在它的README 。[README](https://github.com/fusion809/PKGBUILDs/blob/master/README.md)中找到

**Note:** 关于二进制安装包 *pkgbuild-current*的bug可以在 [GitHub](https://github.com/fusion809/PKGBUILDs/issues)讨论。关于 Visual Studio Code 的问题应该在上游的开发者那讨论。

## 调试 C#

如果你想调试 C#代码，安装 [icu55](https://aur.archlinux.org/packages/icu55/)，否则的话，程序会报错：'Debug adapter process has terminated unexpectedly'

## 命令行启动

在命令行终端下，输入 `code`即可启动。

如果你想打开多个实例，可以使用 `-n` 选项。

## 配置

Visual Studio Code配置文件保存在 `~/.config/Code/User/settings.json`.

## 集成终端

点击*查看 > 集成终端* 或使用快捷键`Ctrl + `` 打开集成终端。 一般情况下, [Bash](/index.php/Bash "Bash")以不带任何附加选项的方式启动作为默认终端。 `terminal.integrated.shell.linux` 可以配置使用的终端， `terminal.integrated.shellArgs.linux` 可以配置启动终端时的附加选项。

例子：

 `~/.config/Code/User/settings.json` 
```
"terminal.integrated.shell.linux": "/usr/bin/fish",
"terminal.integrated.shellArgs.linux": ["-l","-d 3"]

```

## 外部终端

If you are using **Terminator** as default terminal for Arch and you have an error on Visual Studio Code: `Unable to launch debugger worker process (vsdbg) through the terminal. spawn truecolor ENOENT`, you can change the terminal that will be used by Visual Studio to another terminal (eg gnome-terminal).

`"terminal.external.linuxExec": "Yours alternative terminal"` sets the default terminal to be used for exec debug.

Example:

 `~/.config/Code/User/settings.json` 
```
"terminal.external.linuxExec": "gnome-terminal"

```