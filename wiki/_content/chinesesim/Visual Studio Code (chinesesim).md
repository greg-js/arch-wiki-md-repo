**翻译状态：** 本文是英文页面 [Visual Studio Code](/index.php/Visual_Studio_Code "Visual Studio Code") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2018-03-02，点击[这里](https://wiki.archlinux.org/index.php?title=Visual+Studio+Code&diff=0&oldid=494942)可以查看翻译后英文页面的改动。

[Visual Studio Code](https://code.visualstudio.com/)是一个跨平台，免费，开源 (使用MIT协议)的文本编辑器，由微软使用JavaScript和TypeScript开发。它构建于Electron框架之上，并且极具扩展性。可以在编辑器自带的应用商店，或者从 [https://marketplace.visualstudio.com/VSCode](https://marketplace.visualstudio.com/VSCode) 中安装扩展。Visual Studio Code为开源，微软提供一个专有版本（使用终端用户许可协议授权），被用作[visual-studio-code-bin](https://aur.archlinux.org/packages/visual-studio-code-bin/)AUR软件包的基础（有关混合授权的说明，请参阅此 GitHub[评论](https://github.com/Microsoft/vscode/issues/60#issuecomment-161792005)）。

## Contents

*   [1 安装](#安装)
*   [2 调试 C#](#调试_C#)
*   [3 使用](#使用)
*   [4 配置](#配置)
*   [5 集成终端](#集成终端)
*   [6 外部终端](#外部终端)

## 安装

下列安装包包含了 VSCode:

*   [visual-studio-code-bin](https://aur.archlinux.org/packages/visual-studio-code-bin/)
*   [code](https://www.archlinux.org/packages/?name=code)
*   [code-git](https://aur.archlinux.org/packages/code-git/)

## 调试 C#

如果你想调试 C#代码，请安装 [icu55](https://aur.archlinux.org/packages/icu55/)，否则的话，程序会报错：'Debug adapter process has terminated unexpectedly'。

## 使用

在命令行终端下，输入 `code`即可启动。

如果你想打开多个实例，可以使用 `-n` 选项。

## 配置

Visual Studio Code配置文件保存在 `~/.config/Code/User/settings.json`.

## 集成终端

点击*查看 > 集成终端* 或使用快捷键`Ctrl + `` 打开集成终端。 [Bash](/index.php/Bash "Bash")作为默认终端不带任何附加选项的方式启动。 `terminal.integrated.shell.linux` 可以配置默认终端， `terminal.integrated.shellArgs.linux` 可以配置启动终端时的附加选项。

例子：

 `~/.config/Code/User/settings.json` 
```
"terminal.integrated.shell.linux": "/usr/bin/fish",
"terminal.integrated.shellArgs.linux": ["-l","-d 3"]

```

## 外部终端

如果你使用**Terminator**z 作为Arch的默认终端，而且在Visual Studio Code中遇到一个报错`Unable to launch debugger worker process (vsdbg) through the terminal. spawn truecolor ENOENT`，可以换另一个终端（比如，gnome-terminal）供Visual Studio Code使用。

`"terminal.external.linuxExec": "Yours alternative terminal"` 设置调试默认终端。

Example:

 `~/.config/Code/User/settings.json` 
```
"terminal.external.linuxExec": "gnome-terminal"

```