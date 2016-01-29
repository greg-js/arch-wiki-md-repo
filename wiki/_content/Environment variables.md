# Environment variables

An environment variable is a named object that contains data used by one or more applications. In simple terms, it is a variable with a name and a value. The value of an environmental variable can for example be the location of all executable files in the file system, the default editor that should be used, or the system locale settings. Users new to Linux may often find this way of managing settings a bit unmanageable. However, environment variables provide a simple way to share configuration settings between multiple applications and processes in Linux.

## Contents

*   [1 Utilities](#Utilities)
*   [2 Examples](#Examples)
*   [3 Defining variables](#Defining_variables)
    *   [3.1 Globally](#Globally)
    *   [3.2 Per user](#Per_user)
        *   [3.2.1 Graphical applications](#Graphical_applications)
    *   [3.3 Per session](#Per_session)
*   [4 See also](#See_also)

## Utilities

The [coreutils](https://www.archlinux.org/packages/?name=coreutils) package contains the programs _printenv_ and _env_. To list the current environmental variables with values:

```
$ printenv

```

**Note:** Some environment variables are user-specific. Check by comparing the outputs of _printenv_ as an unprivileged user and as _root_.

The `env` utility can be used to run a command under a modified environment. The following example will launch _xterm_ with the environment variable `EDITOR` set to `vim`. This will not affect the global environment variable `EDITOR`.

```
$ env EDITOR=vim xterm

```

The [Bash](/index.php/Bash "Bash") builtin _set_ allows you to change the values of shell options and set the positional parameters, or to display the names and values of shell variables. For more information, see the _set_ documentation: [[1]](http://www.gnu.org/software/bash/manual/bash.html#The-Set-Builtin).

Each process stores their environment in the `/proc/$PID/environ` file. This file contained each key value pair delimited by a nul character (`\x0`). A more human readable format can be obtained with [sed](/index.php/Sed "Sed"), e.g. `sed 's:\x0:\n:g' /proc/$PID/environ`.

## Examples

The following section lists a number of common environment variables used by a Linux system and describes their values.

*   `DE` indicates the _D_esktop _E_nvironment being used. [xdg-open](/index.php/Xdg-open "Xdg-open") will use it to choose more user-friendly file-opener application that desktop environment provides. Some packages need to be installed to use this feature. For [GNOME](/index.php/GNOME "GNOME"), that would be [libgnome](https://www.archlinux.org/packages/?name=libgnome); for [Xfce](/index.php/Xfce "Xfce") this is [exo](https://www.archlinux.org/packages/?name=exo). Recognised values of `DE` variable are: `gnome`, `kde`, `xfce`, `lxde` and `mate`.

NaN

 `~/.xinitrc` 

```
export DE="xfce"
exec openbox
```

NaN

*   `DESKTOP_SESSION` is similar to `DE`, but used in [LXDE](/index.php/LXDE "LXDE") desktop enviroment: when `DESKTOP_SESSION` is set to `LXDE`, _xdg-open_ will use _pcmanfm_ file associations.

*   `PATH` contains a colon-separated list of directories in which your system looks for executable files. When a regular command (e.g., _ls_, _rc-update_ or _ic|emerge_) is interpreted by the shell (e.g., _bash_ or _zsh_), the shell looks for an executable file with the same name as your command in the listed directories, and executes it. To run executables that are not listed in `PATH`, the absoute path to the executable must be given: `/bin/ls`.

**Note:** It is advised not to include the current working directory (`.`) into your `PATH` for security reasons, as it may trick the user to execute vicious commands.

*   `HOME` contains the path to the home directory of the current user. This variable can be used by applications to associate configuration files and such like with the user running it.

*   `PWD` contains the path to your working directory.

*   `OLDPWD` contains the path to your previous working directory, that is, the value of `PWD` before last _cd_ was executed.

*   `SHELL` contains the name of the running, interactive shell, e.g., `bash`

*   `TERM` contains the name of the running terminal, e.g., `xterm`

*   `PAGER` contains command to run the program used to list the contents of files, e.g., `/bin/less`.

*   `EDITOR` contains the command to run the lightweight program used for editing files, e.g., `/usr/bin/nano`. For example, you can write an interactive switch between _gedit_ under [X](/index.php/X "X") or _nano_ in this example):

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

*   `MANPATH` contains a colon-separated list of directories in which _man_ searches for the man pages.

**Note:** In `/etc/profile`, there is a comment that states "Man is much better than us at figuring this out", so this variable should generally be left as default, i.e. `/usr/share/man:/usr/local/share/man`

*   `INFODIR` contains a colon-separated list of directories in which the info command searches for the info pages, e.g., `/usr/share/info:/usr/local/share/info`

*   `TZ` can be used to to set a time zone different to the system zone for a user. The zones listed in `/usr/share/zoneinfo/` can be used as reference, for example `TZ="/usr/share/zoneinfo/Pacific/Fiji"`

## Defining variables

### Globally

Most Linux distributions tell you to change or add environment variable definitions in `/etc/profile` or other locations. Be sure to maintain and manage the environment variables and pay attention to the numerous files that can contain environment variables. In principle, any shell script can be used for initializing environmental variables, but following traditional UNIX conventions, these statements should be only be present in some particular files.

The following files should be used for defining global environment variables on your system: `/etc/profile`, `/etc/bash.bashrc` and `/etc/environment`. Each of these files has different limitations, so you should carefully select the appropriate one for your purposes.

*   `/etc/profile` initializes variables for login shells _only_. It does, however, run scripts and can be used by all [Bourne shell](https://en.wikipedia.org/wiki/Bourne_shell "wikipedia:Bourne shell") compatible shells.
*   `/etc/bash.bashrc` initializes variables for interactive shells _only_. It also runs scripts but (as its name implies) is Bash specific.
*   `/etc/environment` is used by the PAM-env module and is agnostic to login/non-login, interactive/non-interactive and also Bash/non-Bash, so scripting or glob expansion cannot be used. The file only accepts `_variable=value_` pairs.

In this example, we add `~/bin` directory to the `PATH` for respective user. To do this, just put this in your preferred global environment variable config file (`/etc/profile` or `/etc/bash.bashrc`):

```
# If user ID is greater than or equal to 1000 & if ~/bin exists and is a directory & if ~/bin is not already in your $PATH
# then export ~/bin to your $PATH.
if [[ $UID -ge 1000 && -d $HOME/bin && -z $(echo $PATH | grep -o $HOME/bin) ]]
then
    export PATH=$HOME/bin:${PATH}
fi

```

### Per user

**Note:** The dbus daemon and the user instance of systemd do not inherit any of the environment variables set in places like .bashrc etc. This means that, for example, dbus activated programs like Nautilus will not use them by default. See [Systemd/User#Environment variables](/index.php/Systemd/User#Environment_variables "Systemd/User").

You do not always want to define an environment variable globally. For instance, you might want to add `/home/my_user/bin` to the `PATH` variable but do not want all other users on your system to have that in their `PATH` too. Local environment variables can be defined in many different files:

1.  Configuration files of your shell, for example [Bash#Configuration files](/index.php/Bash#Configuration_files "Bash") or [Zsh#Configuration files](/index.php/Zsh#Configuration_files "Zsh").
2.  `~/.profile` is used by many shells as fallback, see [wikipedia:Unix shell#Configuration files](https://en.wikipedia.org/wiki/Unix_shell#Configuration_files "wikipedia:Unix shell").
3.  `~/.pam_environment` is the user specific equivalent of `/etc/environment`, used by PAM-env module. See `pam_env(8)` for details.

To add a directory to the `PATH` for local usage, put following in `~/.bash_profile`:

```
export PATH="${PATH}:/home/my_user/bin"

```

To update the variable, re-login or _source_ the file: `$ source ~/.bash_profile`.

#### Graphical applications

To set environment variables for GUI applications, you can put your variables in [xinitrc](/index.php/Xinitrc "Xinitrc") (or [xprofile](/index.php/Xprofile "Xprofile") when using a [display manager](/index.php/Display_manager "Display manager")), for example:

 `~/.xinitrc` 

```
export PATH="${PATH}:~/scripts"
export GUIVAR=value
```

### Per session

Sometimes even stricter definitions are required. One might want to temporarily run executables from a specific directory created without having to type the absolute path to each one, or editing `~/.bash_profile` for the short time needed to run them.

In this case, you can define the `PATH` variable in your current session, combined with the _export_ command. As long as you do not log out, the `PATH` variable will be using the temporary settings. To add a session-specific directory to `PATH`, issue:

```
$ export PATH="${PATH}:/home/my_user/tmp/usr/bin"

```

## See also

*   [Gentoo Linux Documentation](https://wiki.gentoo.org/wiki/Handbook:X86/Working/EnvVar)
*   [Default applications](/index.php/Default_applications "Default applications")
*   [Xdg-open](/index.php/Xdg-open "Xdg-open")

Retrieved from "[https://wiki.archlinux.org/index.php?title=Environment_variables&oldid=413568](https://wiki.archlinux.org/index.php?title=Environment_variables&oldid=413568)"