Locales are used by [glibc](https://www.archlinux.org/packages/?name=glibc) and other locale-aware programs or libraries for rendering text, correctly displaying regional monetary values, time and date formats, alphabetic idiosyncrasies, and other locale-specific standards.

## Contents

*   [1 Generating locales](#Generating_locales)
*   [2 Setting the locale](#Setting_the_locale)
    *   [2.1 Other uses](#Other_uses)
*   [3 Supported variables](#Supported_variables)
    *   [3.1 LANG: default locale](#LANG:_default_locale)
    *   [3.2 LANGUAGE: fallback locales](#LANGUAGE:_fallback_locales)
    *   [3.3 LC_TIME: date and time format](#LC_TIME:_date_and_time_format)
    *   [3.4 LC_COLLATE: collation](#LC_COLLATE:_collation)
    *   [3.5 LC_ALL](#LC_ALL)
*   [4 Troubleshooting](#Troubleshooting)
    *   [4.1 My terminal does not support UTF-8](#My_terminal_does_not_support_UTF-8)
        *   [4.1.1 Gnome-terminal or rxvt-unicode does not support UTF-8](#Gnome-terminal_or_rxvt-unicode_does_not_support_UTF-8)
    *   [4.2 My system is still using wrong language](#My_system_is_still_using_wrong_language)
*   [5 See also](#See_also)

## Generating locales

Before a locale can be enabled on the system, it has to be generated. The current generated/available locales can be viewed with:

```
$ locale -a

```

The locales that can be generated are listed in the `/etc/locale.gen` file: their names are defined using the format `[language][_TERRITORY][.CODESET][@modifier]`. To generate a locale, first uncomment the corresponding line in the file (or comment to remove); when doing this, also consider localizations needed by other users on the system and specific [variables](#Supported_variables). For example, for American-English uncomment `en_US.UTF-8 UTF-8`.

 `/etc/locale.gen` 
```
...
#en_SG ISO-8859-1
en_US.UTF-8 UTF-8
#en_US ISO-8859-1
...

```

When done, save the file and generate the uncommented locale(s) by executing:

```
# locale-gen

```

**Note:**

*   `locale-gen` also runs with every update of [glibc](https://www.archlinux.org/packages/?name=glibc). [[1]](https://projects.archlinux.org/svntogit/packages.git/tree/trunk/glibc.install?h=packages/glibc#n5)
*   `UTF-8` is recommended over other options. [[2]](http://utf8everywhere.org/)

## Setting the locale

To display the currently set locale and its related environmental settings, type:

```
$ locale

```

The locale to be used, chosen among the previously generated ones, is set in `locale.conf` files, each of which must contain a new-line separated list of environment variable assignments, for example:

 `locale.conf` 
```
LANG=en_AU.UTF-8
LC_COLLATE=C
LC_TIME=en_DK.UTF-8
```

*   A **system-wide** locale can be set by creating or editing `/etc/locale.conf`. The same result can be obtained with the *localectl* command:

	 `# localectl set-locale LANG=en_US.UTF-8` 

	See `man 1 localectl` for details.

**Tip:** During system installation, if the output of *locale* is to your liking, you can save a little time by doing: `locale > /etc/locale.conf` while chrooted.

*   The system-wide locale can be overridden in each **user session** by creating or editing `~/.config/locale.conf` (or, in general, `$XDG_CONFIG_HOME/locale.conf` or `$HOME/.config/locale.conf`).

**Tip:**

*   This can also allow keeping the logs in `/var/log` in English while using the local language in the user environment.
*   You can create a `/etc/skel/.config/locale.conf` file so that any new users added using *useradd* and the `-m` option will have `~/.config/locale.conf` automatically generated.

The precedence of these `locale.conf` files is defined in `/etc/profile.d/locale.sh`.

See [#Supported variables](#Supported_variables), `man 5 locale.conf` and related for details.

Once `locale.conf` files have been created or edited, their new values will take effect for new sessions at login. To have the current environment use the new settings, do:

```
$ LANG= source /etc/profile.d/locale.sh

```

**Note:** The `LANG` variable has to be unset first, otherwise `locale.sh` will not update the values from `locale.conf`. Only new and changed variables will be updated, variables removed from `locale.conf` will still be set in the session.

### Other uses

Locale variables can also be defined with the standard methods as explained in [Environment variables](/index.php/Environment_variables "Environment variables").

For example, in order to test or debug a particular application during development, it could be launched with something like:

```
$ LANG="en_AU.UTF-8" ./my_application.sh

```

Similarly, to set the locale for all processes run from the current shell (for example, during system installation):

```
$ export LANG="en_AU.UTF-8"

```

## Supported variables

`locale.conf` files support the following environment variables:

*   [LANG](#LANG:_default_locale)
*   [LANGUAGE](#LANGUAGE:_fallback_locales)
*   `LC_CTYPE`
*   `LC_NUMERIC`
*   [LC_TIME](#LC_TIME:_date_and_time_format)
*   [LC_COLLATE](#LC_COLLATE:_collation)
*   `LC_MONETARY`
*   `LC_MESSAGES`
*   `LC_PAPER`
*   `LC_NAME`
*   `LC_ADDRESS`
*   `LC_TELEPHONE`
*   `LC_MEASUREMENT`
*   `LC_IDENTIFICATION`

### LANG: default locale

The locale set for this variable will be used for all the `LC_*` variables that are not explicitly set.

### LANGUAGE: fallback locales

Programs which use gettext for translations respect the `LANGUAGE` option in addition to the usual variables. This allows users to specify a [list](http://www.gnu.org/software/gettext/manual/gettext.html#The-LANGUAGE-variable) of locales that will be used in that order. If a translation for the preferred locale is unavailable, another from a similar locale will be used instead of the default. For example, an Australian user might want to fall back to British rather than US spelling:

 `locale.conf` 
```
LANG=en_AU
LANGUAGE=en_AU:en_GB:en
```

### LC_TIME: date and time format

If `LC_TIME` is set to `en_US.UTF-8`, for example, the date format will be "MM/DD/YYYY". If wanting to use the the ISO 8601 date format of "YYYY-MM-DD" use:

 `locale.conf`  `LC_TIME=en_DK.UTF-8` 

### LC_COLLATE: collation

This variable governs the collation rules used for sorting and regular expressions.

Setting the value to `C` can for example make the *ls* command sort dotfiles first, followed by uppercase and lowercase filenames:

 `locale.conf`  `LC_COLLATE=C` 

See also [[3]](http://superuser.com/a/448294/175967).

To get around potential issues, Arch used to set `LC_COLLATE=C` in `/etc/profile`, but this method is now deprecated.

### LC_ALL

The locale set for this variable will always override `LANG` and all the other `LC_*` variables, whether they are set or not.

`LC_ALL` is the only `LC_*` variable, which **cannot** be set in `locale.conf` files: it is meant to be used only for testing or troubleshooting purposes, for example in `/etc/profile`.

## Troubleshooting

### My terminal does not support UTF-8

The following lists some (not all) terminals that support UTF-8:

*   gnustep-terminal
*   konsole
*   [mlterm](/index.php/Mlterm "Mlterm")
*   [rxvt-unicode](/index.php/Rxvt-unicode "Rxvt-unicode")
*   [st](/index.php/St "St")
*   [termite](/index.php/Termite "Termite")
*   [VTE-based terminals](/index.php/List_of_applications/Utilities#VTE-based "List of applications/Utilities")
*   [xterm](/index.php/Xterm "Xterm") - Must be run with the argument `-u8`. Alternatively run *uxterm*, which is provided by the package [xterm](https://www.archlinux.org/packages/?name=xterm).

#### Gnome-terminal or rxvt-unicode does not support UTF-8

You need to launch these applications from a UTF-8 locale or they will drop UTF-8 support. Enable the `en_US.UTF-8` locale (or your local UTF-8 alternative) per the instructions above and set it as the default locale, then reboot.

### My system is still using wrong language

It is possible that the environment variables are redefined in other files than `locale.conf`, for example `~/.pam_environment`. See [Environment variables#Defining variables](/index.php/Environment_variables#Defining_variables "Environment variables") for details.

## See also

*   [Gentoo Linux Localization Guide](http://www.gentoo.org/doc/en/guide-localization.xml)
*   [Gentoo Wiki Archives: Locales](http://www.gentoo-wiki.info/Locales)
*   [ICU's interactive collation testing](http://demo.icu-project.org/icu-bin/locexp?_=en_US&x=col)
*   [Free Standards Group Open Internationalisation Initiative](http://www.openi18n.org/)
*   [*The Single UNIX Specification* definition of Locale](http://pubs.opengroup.org/onlinepubs/007908799/xbd/locale.html) by The Open Group
*   [Locale environment variables](https://help.ubuntu.com/community/EnvironmentVariables#Locale_setting_variables)