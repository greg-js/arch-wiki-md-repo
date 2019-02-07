Related articles

*   [Default applications](/index.php/Default_applications "Default applications")

An environment variable is a named object that contains data used by one or more applications. In simple terms, it is a variable with a name and a value. The value of an environmental variable can for example be the location of all executable files in the file system, the default editor that should be used, or the system locale settings. Users new to Linux may often find this way of managing settings a bit unmanageable. However, environment variables provide a simple way to share configuration settings between multiple applications and processes in Linux.

## Contents

*   [1 Utilities](#Utilities)
*   [2 Defining variables](#Defining_variables)
    *   [2.1 Globally](#Globally)
    *   [2.2 Per user](#Per_user)
        *   [2.2.1 Graphical applications](#Graphical_applications)
    *   [2.3 Per session](#Per_session)
*   [3 Examples](#Examples)
    *   [3.1 Default programs](#Default_programs)
    *   [3.2 Using pam_env](#Using_pam_env)
*   [4 See also](#See_also)

## Utilities

The [coreutils](https://www.archlinux.org/packages/?name=coreutils) package contains the programs *printenv* and *env*. To list the current environmental variables with values:

```
$ printenv

```

**Note:** Some environment variables are user-specific. Check by comparing the outputs of *printenv* as an unprivileged user and as *root*.

The *env* utility can be used to run a command under a modified environment. The following example will launch *xterm* with the environment variable `EDITOR` set to `vim`. This will not affect the global environment variable `EDITOR`.

```
$ env EDITOR=vim xterm

```

The [Bash](/index.php/Bash "Bash") builtin *set* allows you to change the values of shell options and set the positional parameters, or to display the names and values of shell variables. For more information, see [the set builtin documentation](http://www.gnu.org/software/bash/manual/bash.html#The-Set-Builtin).

Each process stores their environment in the `/proc/$PID/environ` file. This file contains each key value pair delimited by a nul character (`\x0`). A more human readable format can be obtained with [sed](/index.php/Sed "Sed"), e.g. `sed 's:\x0:
:g' /proc/$PID/environ`.

## Defining variables

### Globally

Most Linux distributions tell you to change or add environment variable definitions in `/etc/profile` or other locations. Keep in mind that there are also package-specific configuration files containing variable settings such as `/etc/locale.conf`. Be sure to maintain and manage the environment variables and pay attention to the numerous files that can contain environment variables. In principle, any shell script can be used for initializing environmental variables, but following traditional UNIX conventions, these statements should only be present in some particular files.

The following files should be used for defining global environment variables on your system: `/etc/environment`, `/etc/profile` and shell specific configuration files. Each of these files has different limitations, so you should carefully select the appropriate one for your purposes.

*   `/etc/environment` is used by the pam_env module and is shell agnostic so scripting or glob expansion cannot be used. The file only accepts `*variable=value*` pairs. See [pam_env(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/pam_env.8) and [pam_env.conf(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/pam_env.conf.5) for details.
*   Global configuration files of your [shell](/index.php/Shell "Shell"), initializes variables and runs scripts. For example [Bash#Configuration files](/index.php/Bash#Configuration_files "Bash") or [Zsh#Startup/Shutdown files](/index.php/Zsh#Startup/Shutdown_files "Zsh").
*   `/etc/profile` initializes variables for login shells *only*. It does, however, run scripts and can be used by all [Bourne shell](https://en.wikipedia.org/wiki/Bourne_shell "wikipedia:Bourne shell") compatible shells.

In this example, we add `~/bin` directory to the `PATH` for respective user. To do this, just put this in your preferred global environment variable config file (`/etc/profile` or `/etc/bash.bashrc`):

```
# If user ID is greater than or equal to 1000 & if ~/bin exists and is a directory & if ~/bin is not already in your $PATH
# then export ~/bin to your $PATH.
if [[ $UID -ge 1000 && -d $HOME/bin && -z $(echo $PATH | grep -o $HOME/bin) ]]
then
    export PATH="${PATH}:$HOME/bin"
fi

```

### Per user

**Note:** The dbus daemon and the user instance of systemd do not inherit any of the environment variables set in places like `~/.bashrc` etc. This means that, for example, dbus activated programs like Gnome Files will not use them by default. See [Systemd/User#Environment variables](/index.php/Systemd/User#Environment_variables "Systemd/User").

You do not always want to define an environment variable globally. For instance, you might want to add `/home/my_user/bin` to the `PATH` variable but do not want all other users on your system to have that in their `PATH` too. Local environment variables can be defined in many different files:

*   `~/.pam_environment` is the user specific equivalent of `/etc/security/pam_env.conf` [[1]](https://github.com/linux-pam/linux-pam/issues/6), used by pam_env module. See [pam_env(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/pam_env.8) and [pam_env.conf(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/pam_env.conf.5) for details.
*   User configuration files of your [shell](/index.php/Shell "Shell"), for example [Bash#Configuration files](/index.php/Bash#Configuration_files "Bash") or [Zsh#Startup/Shutdown files](/index.php/Zsh#Startup/Shutdown_files "Zsh").
*   `~/.profile` is used by many shells as fallback, see [wikipedia:Unix shell#Configuration files](https://en.wikipedia.org/wiki/Unix_shell#Configuration_files "wikipedia:Unix shell").
*   [systemd](/index.php/Systemd "Systemd") will load environment variables from `~/.config/environment.d/*.conf` see [environment.d(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/environment.d.5) and [https://wiki.gnome.org/Initiatives/Wayland/SessionStart](https://wiki.gnome.org/Initiatives/Wayland/SessionStart).

To add a directory to the `PATH` for local usage, put following in `~/.bash_profile`:

```
export PATH="${PATH}:/home/my_user/bin"

```

To update the variable, re-login or *source* the file: `$ source ~/.bash_profile`.

#### Graphical applications

Environment variables for [Xorg](/index.php/Xorg "Xorg") applications can be set in [xinitrc](/index.php/Xinitrc "Xinitrc"), or in [xprofile](/index.php/Xprofile "Xprofile") when using a [display manager](/index.php/Display_manager "Display manager"), for example:

 `~/.xinitrc` 
```
export PATH="${PATH}:~/scripts"
export GUIVAR=value
```

Applications running on [Wayland](/index.php/Wayland "Wayland") may use [systemd](/index.php/Systemd/User#Environment_variables "Systemd/User") user environment variables instead, as Wayland does not initiate any Xorg related files:

 `~/.config/environment.d/envvars.conf` 
```
PATH=$PATH:~/scripts
GUIVAR=value
```

### Per session

Sometimes even stricter definitions are required. One might want to temporarily run executables from a specific directory created without having to type the absolute path to each one, or editing shell configuration files for the short time needed to run them.

In this case, you can define the `PATH` variable in your current session, combined with the *export* command. As long as you do not log out, the `PATH` variable will be using the temporary settings. To add a session-specific directory to `PATH`, issue:

```
$ export PATH="${PATH}:/home/my_user/tmp/usr/bin"

```

## Examples

The following section lists a number of common environment variables used by a Linux system and describes their values.

*   `DE` indicates the *D*esktop *E*nvironment being used. [xdg-open](/index.php/Xdg-open "Xdg-open") will use it to choose more user-friendly file-opener application that desktop environment provides. Some packages need to be installed to use this feature. For [GNOME](/index.php/GNOME "GNOME"), that would be [libgnome](https://aur.archlinux.org/packages/libgnome/); for [Xfce](/index.php/Xfce "Xfce") this is [exo](https://www.archlinux.org/packages/?name=exo). Recognised values of `DE` variable are: `gnome`, `kde`, `xfce`, `lxde` and `mate`.

	The `DE` environment variable needs to be exported before starting the window manager. For example:

 `~/.xinitrc` 
```
export DE="xfce"
exec openbox
```

	This will make *xdg-open* use the more user-friendly *exo-open*, because it assumes it is running inside Xfce. Use *exo-preferred-applications* for configuring.

*   `DESKTOP_SESSION` is similar to `DE`, but used in [LXDE](/index.php/LXDE "LXDE") desktop environment: when `DESKTOP_SESSION` is set to `LXDE`, *xdg-open* will use *pcmanfm* file associations.

*   `PATH` contains a colon-separated list of directories in which your system looks for executable files. When a regular command (e.g. *ls*, *systemctl* or *pacman*) is interpreted by the shell (e.g. *bash* or *zsh*), the shell looks for an executable file with the same name as your command in the listed directories, and executes it. To run executables that are not listed in `PATH`, a relative or absolute path to the executable must be given, e.g. `./a.out` or `/bin/ls`.

**Note:** It is advised not to include the current working directory (`.`) into your `PATH` for security reasons, as it may trick the user to execute vicious commands.

*   `HOME` contains the path to the home directory of the current user. This variable can be used by applications to associate configuration files and such like with the user running it.

*   `PWD` contains the path to your working directory.

*   `OLDPWD` contains the path to your previous working directory, that is, the value of `PWD` before last *cd* was executed.

*   `TERM` contains the type of the running terminal, e.g. `xterm-256color`. It is used by programs running in the terminal that wish to use terminal-specific capabilities.

*   `MAIL` contains the location of incoming email. The traditional setting is `/var/spool/mail/$LOGNAME`.

*   `ftp_proxy` and `http_proxy` contains FTP and HTTP proxy server, respectively:

```
ftp_proxy="ftp://192.168.0.1:21"
http_proxy="http://192.168.0.1:80"

```

*   `MANPATH` contains a colon-separated list of directories in which *man* searches for the man pages.

**Note:** In `/etc/profile`, there is a comment that states "Man is much better than us at figuring this out", so this variable should generally be left unset. See [manpath(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/manpath.5).

*   `INFODIR` contains a colon-separated list of directories in which the *info* command searches for the info pages, e.g., `/usr/share/info:/usr/local/share/info`

*   `TZ` can be used to to set a time zone different to the system zone for a user. The zones listed in `/usr/share/zoneinfo/` can be used as reference, for example `TZ=":/usr/share/zoneinfo/Pacific/Fiji"`. When pointing the `TZ` variable to a zoneinfo file, it should start with a colon per [the GNU manual](https://www.gnu.org/software/libc/manual/html_node/TZ-Variable.html).

### Default programs

*   `SHELL` contains the path to the user's [preferred shell](http://pubs.opengroup.org/onlinepubs/9699919799/basedefs/V1_chap08.html#tag_08_03). Note that this is not necessarily the shell that is currently running, although [Bash](/index.php/Bash "Bash") sets this variable on startup.

*   `PAGER` contains command to run the program used to list the contents of files, e.g., `/bin/less`.

*   `EDITOR` contains the command to run the lightweight program used for editing files, e.g., `/usr/bin/nano`. For example, you can write an interactive switch between *gedit* under [X](/index.php/X "X") or *nano*, in this example:

```
export EDITOR="$(if [[ -n $DISPLAY ]]; then echo 'gedit'; else echo 'nano'; fi)"

```

*   `VISUAL` contains command to run the full-fledged editor that is used for more demanding tasks, such as editing mail (e.g., `vi`, [vim](/index.php/Vim "Vim"), [emacs](/index.php/Emacs "Emacs") etc).

*   `BROWSER` contains the path to the web browser. Helpful to set in an interactive shell configuration file so that it may be dynamically altered depending on the availability of a graphic environment, such as [X](/index.php/X "X"):

```
if [ -n "$DISPLAY" ]; then
    export BROWSER=firefox
else 
    export BROWSER=links
fi

```

### Using pam_env

The [PAM](/index.php/PAM "PAM") module [pam_env(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/pam_env.8) loads the variables to be set in the environment from the following files: `/etc/security/pam_env.conf`, `/etc/environment` and `~/.pam_environment`.

*   `/etc/environment` must consist of simple `*VARIABLE*=*value*` pairs on separate lines, for example: `EDITOR=NANO` 

*   `/etc/security/pam_env.conf` and `~/.pam_environment` share the same following format: `VARIABLE [DEFAULT=*value*] [OVERRIDE=*value*]` `@{HOME}` and `@{SHELL}` are special variables that expand to what is defined in `/etc/passwd`. The following example illustrates how to expand the `HOME` environment variable into another variable: `XDG_CONFIG_HOME   DEFAULT=@{HOME}/.config` 
    **Note:** The variables `${HOME}` and `${SHELL}` are not linked to the `HOME` and `SHELL` environment variables, they are not set by default.
    The format also allows to expand already defined variables in the values of other variables using `${*VARIABLE*}` , like this: `GNUPGHOME        DEFAULT=${XDG_CONFIG_HOME}/gnupg` `*VARIABLE*=*value*` pairs are also allowed, but variable expansion is not supported in those pairs. See [pam_env.conf(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/pam_env.conf.5) for more information.

**Note:** These files are read before other files, in particular before `~/.profile`, `~/.bash_profile` and `~/.zshenv`.

## See also

*   [Gentoo Linux Documentation](https://wiki.gentoo.org/wiki/Handbook:X86/Working/EnvVar)
*   [Ubuntu Community Wiki - Environment Variables](https://help.ubuntu.com/community/EnvironmentVariables)