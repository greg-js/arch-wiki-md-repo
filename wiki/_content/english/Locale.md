Locales are used by [glibc](https://www.archlinux.org/packages/?name=glibc) and other locale-aware programs or libraries for rendering text, correctly displaying regional monetary values, time and date formats, alphabetic idiosyncrasies, and other locale-specific standards.

## Contents

*   [1 Generating locales](#Generating_locales)
*   [2 Setting the locale](#Setting_the_locale)
    *   [2.1 Setting the system locale](#Setting_the_system_locale)
    *   [2.2 Overriding system locale per user session](#Overriding_system_locale_per_user_session)
    *   [2.3 Make locale changes immediate](#Make_locale_changes_immediate)
    *   [2.4 Other uses](#Other_uses)
*   [3 Variables](#Variables)
    *   [3.1 LANG: default locale](#LANG:_default_locale)
    *   [3.2 LANGUAGE: fallback locales](#LANGUAGE:_fallback_locales)
    *   [3.3 LC_TIME: date and time format](#LC_TIME:_date_and_time_format)
    *   [3.4 LC_COLLATE: collation](#LC_COLLATE:_collation)
    *   [3.5 LC_ALL: troubleshooting](#LC_ALL:_troubleshooting)
*   [4 Troubleshooting](#Troubleshooting)
    *   [4.1 My terminal does not support UTF-8](#My_terminal_does_not_support_UTF-8)
        *   [4.1.1 Gnome-terminal or rxvt-unicode](#Gnome-terminal_or_rxvt-unicode)
    *   [4.2 My system is still using wrong language](#My_system_is_still_using_wrong_language)
*   [5 See also](#See_also)

## Generating locales

Locale names are typically of the form `language[_territory][.codeset][@modifier]`, where *language* is an [ISO 639 language code](https://en.wikipedia.org/wiki/List_of_ISO_639-1_codes "w:List of ISO 639-1 codes"), *territory* is an [ISO 3166 country code](https://en.wikipedia.org/wiki/ISO_3166-1#Current_codes "w:ISO 3166-1"), and *codeset* is a [character set](https://en.wikipedia.org/wiki/Character_encoding "w:Character encoding") or encoding identifier like [ISO-8859-1](https://en.wikipedia.org/wiki/ISO/IEC_8859-1 "w:ISO/IEC 8859-1") or [UTF-8](https://en.wikipedia.org/wiki/UTF-8 "w:UTF-8"). See [setlocale(3)](http://man7.org/linux/man-pages/man3/setlocale.3.html).

For a list of enabled locales, run:

```
$ locale -a

```

Before a locale can be enabled on the system, it must be generated. This can be achieved by uncommenting applicable entries in `/etc/locale.gen`, and running *locale-gen*. Equivalently, commenting entries disables their respective locales. While making changes, consider any localisations required by other users on the system, as well as specific [#Variables](#Variables).

For example, uncomment `en_US.UTF-8 UTF-8` for American-English:

 `/etc/locale.gen` 
```
...
#en_SG ISO-8859-1
en_US.UTF-8 UTF-8
#en_US ISO-8859-1
...

```

Save the file, and generate the locale:

```
# locale-gen

```

**Note:**

*   `locale-gen` also runs with every update of [glibc](https://www.archlinux.org/packages/?name=glibc). [[1]](https://projects.archlinux.org/svntogit/packages.git/tree/trunk/glibc.install?h=packages/glibc#n5)
*   `UTF-8` is recommended over other character sets. [[2]](http://utf8everywhere.org/)

## Setting the locale

To display the currently set locale and its related environmental settings, type:

```
$ locale

```

The locale to be used, chosen among the previously generated ones, is set in `locale.conf` files. Each of these files must contain a new-line separated list of [environment variable](/index.php/Environment_variable "Environment variable") assignments, having the same format as output by *locale*.

To list available locales which have been previously generated, run:

```
$ localedef --list-archive

```

Alternatively, using [localectl(1)](http://man7.org/linux/man-pages/man1/localectl.1.html):

```
$ localectl list-locales

```

### Setting the system locale

To set the system locale, write the `LANG` variable to `/etc/locale.conf`, where `*en_US.UTF-8*` belongs to the **first column** of an uncommented entry in `/etc/locale.gen`:

 `/etc/locale.conf`  `LANG=*en_US.UTF-8*` 

Alternatively, run:

```
# localectl set-locale LANG=*en_US.UTF-8*

```

See [#Variables](#Variables) and [locale.conf(5)](http://man7.org/linux/man-pages/man5/locale.conf.5.html) for details.

### Overriding system locale per user session

The system-wide locale can be overridden in each user session by creating or editing `~/.config/locale.conf` (or, in general, `$XDG_CONFIG_HOME/locale.conf` or `$HOME/.config/locale.conf`).

The precedence of these `locale.conf` files is defined in `/etc/profile.d/locale.sh`.

**Tip:**

*   This can also allow keeping the logs in `/var/log` in English while using the local language in the user environment.
*   You can create a `/etc/skel/.config/locale.conf` file so that any new users added using *useradd* and the `-m` option will have `~/.config/locale.conf` automatically generated.

### Make locale changes immediate

Once system and user `locale.conf` files have been created or edited, their new values will take effect for new sessions at login. To have the current environment use the new settings unset `LANG` and source `/etc/profile.d/locale.sh`:

```
$ LANG= source /etc/profile.d/locale.sh

```

**Note:** The `LANG` variable has to be unset first, otherwise `locale.sh` will not update the values from `locale.conf`. Only new and changed variables will be updated; variables removed from `locale.conf` will still be set in the session.

### Other uses

Locale variables can also be defined with the standard methods as explained in [Environment variables](/index.php/Environment_variables "Environment variables").

For example, in order to test or debug a particular application during development, it could be launched with something like:

```
$ LANG=C ./my_application.sh

```

Similarly, to set the locale for all processes run from the current shell (for example, during system installation):

```
$ export LANG=C

```

## Variables

`locale.conf` files support the following environment variables:

*   [LANG](#LANG:_default_locale)
*   [LANGUAGE](#LANGUAGE:_fallback_locales)
*   `LC_ADDRESS`
*   [LC_COLLATE](#LC_COLLATE:_collation)
*   `LC_CTYPE`
*   `LC_IDENTIFICATION`
*   `LC_MEASUREMENT`
*   `LC_MESSAGES`
*   `LC_MONETARY`
*   `LC_NAME`
*   `LC_NUMERIC`
*   `LC_PAPER`
*   `LC_TELEPHONE`
*   [LC_TIME](#LC_TIME:_date_and_time_format)

Full meaning of the above `LC_*` variables can be found on manpage [locale(7)](http://man7.org/linux/man-pages/man7/locale.7.html), whereas details of their definition are described on [locale(5)](http://man7.org/linux/man-pages/man5/locale.5.html).

### LANG: default locale

The locale set for this variable will be used for all the `LC_*` variables that are not explicitly set.

### LANGUAGE: fallback locales

Programs which use gettext for translations respect the `LANGUAGE` option in addition to the usual variables. This allows users to specify a [list](http://www.gnu.org/software/gettext/manual/gettext.html#The-LANGUAGE-variable) of locales that will be used in that order. If a translation for the preferred locale is unavailable, another from a similar locale will be used instead of the default. For example, an Australian user might want to fall back to British rather than US spelling:

 `locale.conf` 
```
LANG=en_AU.UTF-8
LANGUAGE=en_AU:en_GB:en
```

### LC_TIME: date and time format

If `LC_TIME` is set to `en_US.UTF-8`, for example, the date format will be "MM/DD/YYYY". If wanting to use the the ISO 8601 date format of "YYYY-MM-DD" use:

 `locale.conf`  `LC_TIME=en_DK.UTF-8` 
**Note:** Programs do not necessarily respect this variable to format the date. For example, [date(1)](http://man7.org/linux/man-pages/man1/date.1.html) uses its own parameters to do so.

### LC_COLLATE: collation

This variable governs the collation rules used for sorting and regular expressions.

Setting the value to `C` can for example make the *ls* command sort dotfiles first, followed by uppercase and lowercase filenames:

 `locale.conf`  `LC_COLLATE=C` 

See also [[3]](http://superuser.com/a/448294/175967).

To get around potential issues, Arch used to set `LC_COLLATE=C` in `/etc/profile`, but this method is now deprecated.

### LC_ALL: troubleshooting

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
*   [xterm](/index.php/Xterm "Xterm") - Run with the argument `-u8` or configure resource `xterm*utf8: 2`.

#### Gnome-terminal or rxvt-unicode

You need to launch these applications from a UTF-8 locale or they will drop UTF-8 support. Enable the `en_US.UTF-8` locale (or your local UTF-8 alternative) per the instructions above and set it as the default locale, then reboot.

### My system is still using wrong language

It is possible that the environment variables are redefined in other files than `locale.conf`, for example `~/.pam_environment`. See [Environment variables#Defining variables](/index.php/Environment_variables#Defining_variables "Environment variables") for details.

If you're using a desktop environment, such as [GNOME](/index.php/GNOME "GNOME"), its language settings may be overriding the settings in `locale.conf`.

## See also

*   [Gentoo Linux Localization Guide](http://www.gentoo.org/doc/en/guide-localization.xml)
*   [Gentoo Wiki Archives: Locales](http://www.gentoo-wiki.info/Locales)
*   [ICU's interactive collation testing](http://demo.icu-project.org/icu-bin/locexp?_=en_US&x=col)
*   [Free Standards Group Open Internationalisation Initiative](http://www.openi18n.org/)
*   [*The Single UNIX Specification* definition of Locale](http://pubs.opengroup.org/onlinepubs/007908799/xbd/locale.html) by The Open Group
*   [Locale environment variables](https://help.ubuntu.com/community/EnvironmentVariables#Locale_setting_variables)