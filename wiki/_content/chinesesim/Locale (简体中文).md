**翻译状态：** 本文是英文页面 [Locale](/index.php/Locale "Locale") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2016-02-05，点击[这里](https://wiki.archlinux.org/index.php?title=Locale&diff=0&oldid=409611)可以查看翻译后英文页面的改动。

Locales 被 [glibc](https://www.archlinux.org/packages/?name=glibc) 和其它需要本地化的应用程序和库用来解析文本(或正确的显示当前区域的某些文字样式,如货币,时间,日期,特殊字符和其他的区域格式).

## Contents

*   [1 生成 locale](#.E7.94.9F.E6.88.90_locale)
*   [2 设置 locale](#.E8.AE.BE.E7.BD.AE_locale)
    *   [2.1 其它用例](#.E5.85.B6.E5.AE.83.E7.94.A8.E4.BE.8B)
*   [3 支持的变量](#.E6.94.AF.E6.8C.81.E7.9A.84.E5.8F.98.E9.87.8F)
    *   [3.1 LANG: 默认的 Locale](#LANG:_.E9.BB.98.E8.AE.A4.E7.9A.84_Locale)
    *   [3.2 LANGUAGE: 后备 Locale](#LANGUAGE:_.E5.90.8E.E5.A4.87_Locale)
    *   [3.3 LC_TIME: 时间和日期格式](#LC_TIME:_.E6.97.B6.E9.97.B4.E5.92.8C.E6.97.A5.E6.9C.9F.E6.A0.BC.E5.BC.8F)
    *   [3.4 LC_COLLATE: 排序格式](#LC_COLLATE:_.E6.8E.92.E5.BA.8F.E6.A0.BC.E5.BC.8F)
*   [4 LC_ALL](#LC_ALL)
*   [5 自定义 Locale](#.E8.87.AA.E5.AE.9A.E4.B9.89_Locale)
    *   [5.1 设置每周的第一天](#.E8.AE.BE.E7.BD.AE.E6.AF.8F.E5.91.A8.E7.9A.84.E7.AC.AC.E4.B8.80.E5.A4.A9)
*   [6 提示和技巧](#.E6.8F.90.E7.A4.BA.E5.92.8C.E6.8A.80.E5.B7.A7)
    *   [6.1 从终端中以另一 Locale 运行程序](#.E4.BB.8E.E7.BB.88.E7.AB.AF.E4.B8.AD.E4.BB.A5.E5.8F.A6.E4.B8.80_Locale_.E8.BF.90.E8.A1.8C.E7.A8.8B.E5.BA.8F)
    *   [6.2 从桌面以另一 Locale 运行程序](#.E4.BB.8E.E6.A1.8C.E9.9D.A2.E4.BB.A5.E5.8F.A6.E4.B8.80_Locale_.E8.BF.90.E8.A1.8C.E7.A8.8B.E5.BA.8F)
    *   [6.3 Python, ViM 和 UTF-8](#Python.2C_ViM_.E5.92.8C_UTF-8)
*   [7 排除问题](#.E6.8E.92.E9.99.A4.E9.97.AE.E9.A2.98)
    *   [7.1 我的终端不支持 UTF-8](#.E6.88.91.E7.9A.84.E7.BB.88.E7.AB.AF.E4.B8.8D.E6.94.AF.E6.8C.81_UTF-8)
        *   [7.1.1 Gnome-terminal / rxvt-unicode 不支持 UTF-8](#Gnome-terminal_.2F_rxvt-unicode_.E4.B8.8D.E6.94.AF.E6.8C.81_UTF-8)
    *   [7.2 我的系统的语言还是不对](#.E6.88.91.E7.9A.84.E7.B3.BB.E7.BB.9F.E7.9A.84.E8.AF.AD.E8.A8.80.E8.BF.98.E6.98.AF.E4.B8.8D.E5.AF.B9)
*   [8 另见](#.E5.8F.A6.E8.A7.81)

## 生成 locale

设置 locale 前，需要先准备需要的 locale。要列出所有启用的locale，使用：

```
$ locale -a

```

可生成的 Locale 保存在 `/etc/locale.gen` 中,用以下的格式来定义：`[language][_TERRITORY][.CODESET][@modifier]`.要开启某个Locale,反注释对应的行即可.

尽管在你的电脑上你很可能只使用一种语言,但同时开启其它的 Locale 有时会有帮助、甚至是必要的.比如你正运行着一个多用户的系统，而有的用户并不懂en_US，那么你的系统需要支持他们需要的 locale.

例如对于使用美式英语的用户,反注释 `en_US.UTF-8 UTF-8` 一行.

 `/etc/locale.gen` 
```
...
#en_SG ISO-8859-1
en_US.UTF-8 UTF-8
#en_US ISO-8859-1
...

```

编辑完成以后,通过下面的命令生成 Locale :

```
# locale-gen

```

**Note:**

*   每次更新 [glibc](https://www.archlinux.org/packages/?name=glibc) 时 `locale-gen` 会自动运行.
*   建议开启 `UTF-8` Locales. [[1]](http://utf8everywhere.org/)

## 设置 locale

想要显示正在使用的 Locale 和相关的环境变量，运行:

```
$ locale

```

`locale.conf` 文件存放如何使用和选择不同的 Locale 相关的环境变量.一行一个,例如:

 `locale.conf` 
```
LANG=en_AU.UTF-8
LC_COLLATE=C
LC_TIME=en_DK.UTF-8
```

*   **整个系统** 使用的 Locale 可以通过创建或编辑 `/etc/locale.conf` 来设置,或者通过 *localectl* 设置:

	 `# localectl set-locale LANG=en_US.UTF-8` 

	参阅 `man 1 localectl` 获得更多细节.

**Tip:** 如果安装是使用的 `locale` 正是你需要的，可以在 chroot 后通过 `# locale > /etc/locale.conf`进行设置。

*   **整个系统** 使用的 Locale 可以由用户通过编辑用户自己的 `~/.config/locale.conf` (或者 {ic|$XDG_CONFIG_HOME/locale.conf}} 或 `$HOME/.config/locale.conf`) 来覆盖.

**Tip:**

*   设置用户级 Locale ，就能让日志(例如 `/var/log` )中的文件以英语输出.
*   建立 `/etc/skel/.config/locale.conf` 文件,可以让新用户建立且同时创建主目录时( *useradd -m* )自动应用其中的 Locale (会将这个文件复制到 `~/.config/locale.conf` 中.)

这些 `locale.conf` 文件的优先级定义在 `/etc/profile.d/locale.sh` 中.

参阅 [#支持的变量](#.E6.94.AF.E6.8C.81.E7.9A.84.E5.8F.98.E9.87.8F), `man 5 locale.conf` 和相关连的文章获得更多细节.

`locale.conf` 的变更会在下次登录时生效,要立刻应用新的设置的话,可以运行:

```
$ LANG= source /etc/profile.d/locale.sh

```

**Note:** 这只有在 `LANG` 变量没设置时才会有用.而且如果你在 `locale.conf` 中移除了某些变量再运行这个命令,移除的那些变量在注销前依然存在.

### 其它用例

和 Locale 相关的变量也能像其他的 [环境变量](/index.php/Environment_variables "Environment variables") 一样传递给其它程序.

例如在开发时进行测试时,可以这样运行:

```
$ LANG="en_AU.UTF-8" ./my_application.sh

```

类似的,也可以通过设置环境变量让当前 shell中运行的程序使用特定的 Locale,(例如安装系统时):

```
$ export LANG="en_AU.UTF-8"

```

## 支持的变量

`locale.conf` files support the following environment variables:

*   [LANG](#LANG:_.E9.BB.98.E8.AE.A4.E7.9A.84_Locale)
*   [LANGUAGE](#LANGUAGE:_.E5.90.8E.E5.A4.87_Locale)
*   `LC_CTYPE`
*   `LC_NUMERIC`
*   [LC_TIME](#LC_TIME:_.E6.97.B6.E9.97.B4.E5.92.8C.E6.97.A5.E6.9C.9F.E6.A0.BC.E5.BC.8F)
*   [LC_COLLATE](#LC_COLLATE:_.E6.8E.92.E5.BA.8F.E6.A0.BC.E5.BC.8F)
*   `LC_MONETARY`
*   `LC_MESSAGES`
*   `LC_PAPER`
*   `LC_NAME`
*   `LC_ADDRESS`
*   `LC_TELEPHONE`
*   `LC_MEASUREMENT`
*   `LC_IDENTIFICATION`

### LANG: 默认的 Locale

这个变量的值会覆盖掉所有未设置的 `LC_*` 变量的值.

### LANGUAGE: 后备 Locale

使用 gettext 翻译的软件会按照 `LANGUAGE` 选择使用的语言。用户通过这个变量指定一个[locale 列表](http://www.gnu.org/software/gettext/manual/gettext.html#The-LANGUAGE-variable)，如果前面的 locale 缺少翻译，会自动使用后面的 locale 显示界面。 例如下面的例子使用简体中文,没有翻译时使用英文：

 `locale.conf` 
```
LANG="zh_CN"
LANGUAGE="zh_CN:en_GB:en"
```

### LC_TIME: 时间和日期格式

如果 `LC_TIME` 设置成 `en_US.UTF-8`, 日期的格式为 "MM/DD/YYYY". 要使用 ISO 8601 标准的日期格式( "YYYY-MM-DD" ) ,使用:

 `locale.conf`  `LC_TIME=en_DK.UTF-8` 

### LC_COLLATE: 排序格式

这个变量的值决定排序和正则表达式的格式顺序.

例如将它设置为 `C` 可以让 *ls* 命令按顺序列出 dotfile,大写字母开头的文件和小写字母开头的文件:

 `locale.conf`  `LC_COLLATE=C` 

另见 [[2]](http://superuser.com/a/448294/175967).

为了避免可能的问题,Arch Linux 曾经在 `/etc/profile` 中设置 `LC_COLLATE=C` ,这个方法已经过时了.w deprecated.

## LC_ALL

这个变量的值会覆盖掉 `LANG` 和所有 `LC_*` 变量的值,无论它们是否设置.

只有 `LC_ALL` 不能在 `locale.conf` 文件中,这意味着它只是为了测试和排除问题而设置,例如在 `/etc/profile` 中.

## 自定义 Locale

`/usr/share/i18n/locales/` 存放着所有的 Locale,并且可以被修改以适应不同的需要.

记得在修改 Locale 文件以后[重新生成](#.E7.94.9F.E6.88.90_locale) Locale 并重新启动以让新的 Locales 生效.

### 设置每周的第一天

很多国家都把星期一作为每周的第一天,可以像这样进行修改:

 `/usr/share/i18n/locales/*chosen_locale*` 
```
LC_TIME
[...]
week            7;19971130;5
first_weekday   2
first_workday   2

```

## 提示和技巧

### 从终端中以另一 Locale 运行程序

例如用 Hebrew Locale 运行 Abiword :

```
$ env LANG=he_IL.UTF-8 abiword &

```

### 从桌面以另一 Locale 运行程序

把 *.desktop* 文件复制到你的用户目录:

```
$ cp /usr/share/applications/abiword.desktop ~/.local/share/applications/

```

编辑 `Exec` 选项:

 `~/.local/share/applications/abiword.desktop`  `Exec=env LANG=he_IL.UTF-8 abiword %U` 

### Python, ViM 和 UTF-8

在 ViM 中运行 `:!python -c "import sys; print(sys.stdout.encoding)"` 时,输出可能是 `ANSI_X3.4-1968` (即使你设置了正确的Locale) . 把 `PYTHONIOENCODING` 变量设置成 `utf-8` 可以规避这个问题.

## 排除问题

### 我的终端不支持 UTF-8

这些终端(不是全部)支持 UTF-8:

*   gnustep-terminal
*   konsole
*   [mlterm](/index.php/Mlterm "Mlterm")
*   [rxvt-unicode](/index.php/Rxvt-unicode "Rxvt-unicode")
*   [st](/index.php/St "St")
*   [termite](/index.php/Termite "Termite")
*   [VTE-based terminals](/index.php/List_of_applications/Utilities#VTE-based "List of applications/Utilities")
*   [xterm](/index.php/Xterm "Xterm") - 必须包含参数 `-u8`. 或者 *uxterm*, 随 [xterm](https://www.archlinux.org/packages/?name=xterm) 提供.

#### Gnome-terminal / rxvt-unicode 不支持 UTF-8

你必须在 UTF-8 的 Locale 下运行它们在会有作用.按照上面的方法启用 `en_US.UTF-8` Locale ,将它设置成默认 Locale 后重新启动.

### 我的系统的语言还是不对

可能其它文件设置了本该由 `locale.conf` 设置的 Locale (例如 `~/.pam_environment` ),详见 [Environment variables#Defining variables](/index.php/Environment_variables#Defining_variables "Environment variables") .

## 另见

*   [Gentoo Linux 本地化指南](http://www.gentoo.org/doc/en/guide-localization.xml)
*   [Gentoo Wiki Archives: Locales](http://www.gentoo-wiki.info/Locales)
*   [ICU's interactive collation testing](http://demo.icu-project.org/icu-bin/locexp?_=en_US&x=col)
*   [Free Standards Group Open Internationalisation Initiative](http://www.openi18n.org/)
*   [*The Single UNIX Specification* definition of Locale](http://pubs.opengroup.org/onlinepubs/007908799/xbd/locale.html) by The Open Group
*   [Locale environment variables](https://help.ubuntu.com/community/EnvironmentVariables#Locale_setting_variables)