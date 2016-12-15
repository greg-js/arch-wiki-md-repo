**翻译状态：** 本文是英文页面 [Atom](/index.php/Atom "Atom") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2016-12-14，点击[这里](https://wiki.archlinux.org/index.php?title=Atom&diff=0&oldid=459125)可以查看翻译后英文页面的改动。

[Atom](https://atom.io/) 是一个由 GitHub 开发的开源编辑器，采用 MIT 证书授权方式。主要是由 CoffeeScript 和 Javascript 编写，并使用 Node.js 作为运行时环境。超过 4,000 个插件和1,000 种主题使它具有很强的扩展性。它使用其内建的 apm 软件包管理器管理软件包和主题。

## Contents

*   [1 安装](#.E5.AE.89.E8.A3.85)
*   [2 插件](#.E6.8F.92.E4.BB.B6)
*   [3 问题处理](#.E9.97.AE.E9.A2.98.E5.A4.84.E7.90.86)
    *   [3.1 环境变量设置（Environment variables not sourced）](#.E7.8E.AF.E5.A2.83.E5.8F.98.E9.87.8F.E8.AE.BE.E7.BD.AE.EF.BC.88Environment_variables_not_sourced.EF.BC.89)

## 安装

以下软件包都可用于安装Atom:

*   [atom](https://www.archlinux.org/packages/?name=atom)
*   [atom-editor](https://aur.archlinux.org/packages/atom-editor/)
*   [atom-editor-bin](https://aur.archlinux.org/packages/atom-editor-bin/)
*   [atom-editor-git](https://aur.archlinux.org/packages/atom-editor-git/)
*   [atom-editor-beta](https://aur.archlinux.org/packages/atom-editor-beta/)
*   [atom-editor-beta-bin](https://aur.archlinux.org/packages/atom-editor-beta-bin/)
*   非官方的 [atom](/index.php/Unofficial_user_repositories#atom "Unofficial user repositories") 源提供的 *atom* 软件包 .
    **Note:** Bugs regarding binary packages from the *atom* repository can be reported on [GitHub](https://github.com/tensor5/arch-atom/issues). Bugs regarding Atom itself should be reported upstream.

## 插件

它的插件可以在Atom软件中或者使用apm命令完成安装，正确的apm命令语法是：

```
$ apm install *package_name1* *package_name2* *package_name3* ...

```

一些包已经被预装到Atom中，另一些包没有，包括：

*   [build](https://atom.io/packages/build) which enables Atom to compile source code.
*   [git-plus](https://atom.io/packages/git-plus) which allows one to manage git repositories from within Atom.
*   [language-archlinux](https://atom.io/packages/language-archlinux) which provides syntax-highlighting for PKGBUILDs (if installed along with the [language-unix-shell](https://atom.io/packages/language-unix-shell) package) along with support

为了在Atom中运行PKGBUILDs的测试和其他功能（包括[makepkg](/index.php/Makepkg "Makepkg"), [namcap](/index.php/Namcap "Namcap"), *updpkgsums*等）： for running several tests and other actions on PKGBUILDs without a terminal (including [makepkg](/index.php/Makepkg "Makepkg"), [namcap](/index.php/Namcap "Namcap"), *updpkgsums*, etc.).

*   [markdown-writer](https://atom.io/packages/markdown-writer) which turns Atom into an efficient Markdown writer.
*   [script](https://atom.io/packages/script) which enables Atom the ability to run scripts, based on file names.
*   [terminal-fusion](https://atom.io/packages/terminal-fusion) which adds an embedded terminal window to Atom.

## 问题处理

### 环境变量设置（Environment variables not sourced）

你可能会遇到一些因为软件包使用环境变量而引起的问题，像[go-plus](https://atom.io/packages/go-plus) (`$GOPATH not found`)。例如，Atom打开你的文件管理器所引起的问题（这是有DBUS-spawned引起的，因此，他不会继承在 `.bashrc` 中定义的环境变量）。

你可以通过[Systemd/User#Environment variables](/index.php/Systemd/User#Environment_variables "Systemd/User")为DBUS-spawned进程创建可用的环境变量

关于这个问题的更过内容，请参考 [Environment variables#Per user](/index.php/Environment_variables#Per_user "Environment variables").