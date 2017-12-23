Related articles

*   [Default applications](/index.php/Default_applications "Default applications")

**翻译状态：** 本文是英文页面 [Environment_variables](/index.php/Environment_variables "Environment variables") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2016-09-07，点击[这里](https://wiki.archlinux.org/index.php?title=Environment_variables&diff=0&oldid=436138)可以查看翻译后英文页面的改动。

环境变量是一个有名称的对象，包含可被其它程序使用的数据。简单的说，它是一个名称和数值对。环境变量的值可以是文件系统上所有执行程序的位置，默认的编辑器，系统本地化设置等。Linux 新用户可能觉得这种管理变量的方式有点混乱。但是环境变量提供了一种在多个程序和进程间共享配置的方式。

## Contents

*   [1 工具](#.E5.B7.A5.E5.85.B7)
*   [2 定义变量](#.E5.AE.9A.E4.B9.89.E5.8F.98.E9.87.8F)
    *   [2.1 全局](#.E5.85.A8.E5.B1.80)
    *   [2.2 按用户](#.E6.8C.89.E7.94.A8.E6.88.B7)
        *   [2.2.1 图形程序](#.E5.9B.BE.E5.BD.A2.E7.A8.8B.E5.BA.8F)
    *   [2.3 按会话](#.E6.8C.89.E4.BC.9A.E8.AF.9D)
*   [3 示例](#.E7.A4.BA.E4.BE.8B)
    *   [3.1 使用 pam_env](#.E4.BD.BF.E7.94.A8_pam_env)
*   [4 参阅](#.E5.8F.82.E9.98.85)

## 工具

[coreutils](https://www.archlinux.org/packages/?name=coreutils)软件包含程序*printenv*和*env*. 要显示当前环境变量的值:

```
$ printenv

```

**Note:** 一些环境变量是属于特定用户的. 比较一般用户和*root*用户的 *printenv* 就可以看到差异。

工具 `env` 可以用指定的环境变量执行一个命令。下面例子把环境变量 `EDITOR` 设置为 `vim` 然后执行命令 *xterm*. 这个操作不会影响全局环境变量`EDITOR`.

```
$ env EDITOR=vim xterm

```

[Bash](/index.php/Bash "Bash") 内建的 *set* 命令可以设置 shell 选项值或显示 shell 变量的名称和数值。更多信息请参阅: [[1]](http://www.gnu.org/software/bash/manual/bash.html#The-Set-Builtin).

每个进程都把他们的环境变量保存在 `/proc/$PID/environ` 文件中。此文件包含用 nul (`\x0`) 字符分隔的键值对。用 [sed](/index.php/Sed "Sed") 可以获得用户可读的内容：`sed 's:\x0:
:g' /proc/$PID/environ`.

## 定义变量

### 全局

理论上，任何 shell 脚本都可以初始化环境变量，但为了维护方便，环境变量的定义集中在几个特定的文件中。对全局变量来说是：`/etc/profile`, `/etc/bash.bashrc` 和 `/etc/environment`. 每个文件都有不同的限制，请根据需要选择要使用的文件。

*   `/etc/profile` **仅**初始化登陆 shell 的环境变量。它可以执行脚本并支持 [Bash](https://en.wikipedia.org/wiki/Bourne_shell "wikipedia:Bourne shell") 兼容 Shell。
*   `/etc/bash.bashrc` **仅**初始化交互 shell，它也可以执行脚本但是只支持 Bash。
*   `/etc/environment` 被 PAM-env 模块使用，和登陆与否，交互与否，Bash与否无关，所以无法使用脚本或通配符展开。仅接受 `*variable=value*` 格式。

以将 `~/bin` 加入某些特定用户的 `PATH` 为例，可以将其放入 `/etc/profile` 或 `/etc/bash.bashrc`:

```
# If user ID is greater than or equal to 1000 & if ~/bin exists and is a directory & if ~/bin is not already in your $PATH
# then export ~/bin to your $PATH.
if [[ $UID -ge 1000 && -d $HOME/bin && -z $(echo $PATH | grep -o $HOME/bin) ]]
then
    export PATH=$HOME/bin:${PATH}
fi

```

### 按用户

**注意:** dbus 进程和 systemd 用户实例不会使用任何 .bashrc 等文件定义的环境变量。所以 dbus 启动的程序默认不会使用这些变量，请参考 [Systemd/User#Environment variables](/index.php/Systemd/User#Environment_variables "Systemd/User").

有时并不希望定义全局环境变量，比如要把 `/home/my_user/bin` 加入 `PATH` 变量但是不影响其它用户。本地环境变量可以在下面文件定义：

1.  shell 配置文件，例如 [Bash#Configuration files](/index.php/Bash#Configuration_files "Bash") 或 [Zsh#Configuration files](/index.php/Zsh#Configuration_files "Zsh").
2.  很多 shell 会使用 `~/.profile` 作为后备方案参考 [wikipedia:Unix shell#Configuration files](https://en.wikipedia.org/wiki/Unix_shell#Configuration_files "wikipedia:Unix shell").
3.  `~/.pam_environment` 是用户特有的环境变量，PAM-env 模块会使用它。参考 `pam_env(8)` 和 `pam_env.conf(5)`。

要修改本地用户的路径变量，修改 `~/.bash_profile`:

```
export PATH="${PATH}:/home/my_user/bin"

```

要更新变量，重新登录或 *source* 文件 `$ source ~/.bash_profile`.

#### 图形程序

要设置图形程序的环境变量，可以将变量放入 [xinitrc](/index.php/Xinitrc "Xinitrc") (从 [显示管理器](/index.php/Display_manager "Display manager") 登陆时，使用 [xprofile](/index.php/Xprofile "Xprofile"))，例如：

 `~/.xinitrc` 
```
export PATH="${PATH}:~/scripts"
export GUIVAR=value
```

### 按会话

如果需要更严格的定义，例如在运行程序时临时修改路径，在短时间改变 `~/.bash_profile` 等。这时，可以用 export 命令在当前会话修改 `PATH`，只要不退出登录，`PATH` 变量就会一直生效。增加 `PATH` 到一个会话:

```
$ export PATH="${PATH}:/home/my_user/tmp/usr/bin"

```

## 示例

The following section lists a number of common environment variables used by a Linux system and describes their values.

*   `DE` indicates the *D*esktop *E*nvironment being used. [xdg-open](/index.php/Xdg-open "Xdg-open") will use it to choose more user-friendly file-opener application that desktop environment provides. Some packages need to be installed to use this feature. For [GNOME](/index.php/GNOME "GNOME"), that would be [libgnome](https://aur.archlinux.org/packages/libgnome/); for [Xfce](/index.php/Xfce "Xfce") this is [exo](https://www.archlinux.org/packages/?name=exo). Recognised values of `DE` variable are: `gnome`, `kde`, `xfce`, `lxde` and `mate`.

	The `DE` environment variable needs to be exported before starting the window manager. For example:

 `~/.xinitrc` 
```
export DE="xfce"
exec openbox
```

	This will make *xdg-open* use the more user-friendly *exo-open*, because it assumes it is running inside Xfce. Use *exo-preferred-applications* for configuring.

*   `DESKTOP_SESSION` is similar to `DE`, but used in [LXDE](/index.php/LXDE "LXDE") desktop enviroment: when `DESKTOP_SESSION` is set to `LXDE`, *xdg-open* will use *pcmanfm* file associations.

*   `PATH` contains a colon-separated list of directories in which your system looks for executable files. When a regular command (e.g., *ls*, *rc-update* or *ic|emerge*) is interpreted by the shell (e.g., *bash* or *zsh*), the shell looks for an executable file with the same name as your command in the listed directories, and executes it. To run executables that are not listed in `PATH`, the absoute path to the executable must be given: `/bin/ls`.

**Note:** It is advised not to include the current working directory (`.`) into your `PATH` for security reasons, as it may trick the user to execute vicious commands.

*   `HOME` contains the path to the home directory of the current user. This variable can be used by applications to associate configuration files and such like with the user running it.

*   `PWD` contains the path to your working directory.

*   `OLDPWD` contains the path to your previous working directory, that is, the value of `PWD` before last *cd* was executed.

*   `SHELL` contains the name of the running, interactive shell, e.g., `bash`

*   `TERM` contains the name of the running terminal, e.g., `xterm`

*   `PAGER` contains command to run the program used to list the contents of files, e.g., `/bin/less`.

*   `EDITOR` contains the command to run the lightweight program used for editing files, e.g., `/usr/bin/nano`. For example, you can write an interactive switch between *gedit* under [X](/index.php/X "X") or *nano* in this example):

```
export EDITOR="$(if [[ -n $DISPLAY ]]; then echo 'gedit'; else echo 'nano'; fi)"

```

*   `VISUAL` contains command to run the full-fledged editor that is used for more demanding tasks, such as editing mail (e.g., `vi`, [vim](/index.php/Vim "Vim"), [emacs](/index.php/Emacs "Emacs") etc).

*   `MAIL` contains the location of incoming email. The traditional setting is `/var/spool/mail/$LOGNAME`.

*   `BROWSER` contains the path to the web browser. Helpful to set in an interactive shell configuration file so that it may be dynamically altered depending on the availability of a graphic environment, such as [X](/index.php/X "X"):

```
if [ -n "$DISPLAY" ]; then
    export BROWSER=firefox
else 
    export BROWSER=links
fi

```

*   `ftp_proxy and http_proxy` contains FTP and HTTP proxy server, respectively:

```
ftp_proxy="ftp://192.168.0.1:21"
http_proxy="http://192.168.0.1:80"

```

*   `MANPATH` contains a colon-separated list of directories in which *man* searches for the man pages.

**Note:** In `/etc/profile`, there is a comment that states "Man is much better than us at figuring this out", so this variable should generally be left as default, i.e. `/usr/share/man:/usr/local/share/man`

*   `INFODIR` contains a colon-separated list of directories in which the info command searches for the info pages, e.g., `/usr/share/info:/usr/local/share/info`

*   `TZ` can be used to to set a time zone different to the system zone for a user. The zones listed in `/usr/share/zoneinfo/` can be used as reference, for example `TZ="/usr/share/zoneinfo/Pacific/Fiji"`

### 使用 pam_env

Using `/etc/environment` and `~/.pam_environment` can be a little tricky, and the man pages (`pam_env(8)` and `pam_env.conf(5)`) are not particularly clear. So, here's an example:

 `~/.pam_environment` 
```
LANG             DEFAULT=en_US.UTF-8
LC_ALL           DEFAULT=${LANG}

XDG_CONFIG_HOME  DEFAULT=@{HOME}/.config
#XDG_CONFIG_HOME=@{HOME}/.config                    # is **not** valid see below
XDG_DATA_HOME    DEFAULT=@{HOME}/.local/share

# you can even use recently defined variables
RCRC             DEFAULT=${XDG_CONFIG_HOME}/rcrc
BROWSER=firefox
#BROWSER         DEFAULT=firefox # same as above
EDITOR=vim
```

In `~/.pam_environment` there are two ways to set environmental variables:

```
VARIABLE=VALUE

```

and

```
VARIABLE [DEFAULT=[value]] [OVERRIDE=[value]]

```

The first one **doesn't allow** the use of `${VARIABLES}` , while the second does. `@{HOME}` is a special variable that expands what is defined in `/etc/passwd` (same goes with `@{SHELL}` ). After defining a `VARIABLE`, you can recall it with `${VARIABLE}` . Note that curly braces and the dollar sign are needed ( `${}` ) when invoking the previously defined variable.

**Note:** This file is read before everything, even `~/.{,bash_,z}profile` and `~/.zshenv` .

## 参阅

*   [Gentoo Linux Documentation](https://wiki.gentoo.org/wiki/Handbook:X86/Working/EnvVar)