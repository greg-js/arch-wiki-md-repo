# Help:Reading

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

Related articles

*   [Help:Searching](/index.php/Help:Searching "Help:Searching")
*   [Help:Style](/index.php/Help:Style "Help:Style")

Because the vast majority of the ArchWiki contains indications that may need clarification for users new to GNU/Linux, this rundown of basic procedures was written both to avoid confusion in the assimilation of the articles and to deter repetition in the content itself.

## Contents

*   [1 Regular user or root](#Regular_user_or_root)
*   [2 Append, add, create, edit](#Append.2C_add.2C_create.2C_edit)
*   [3 Source](#Source)
*   [4 Installation of packages](#Installation_of_packages)
    *   [4.1 Official packages](#Official_packages)
    *   [4.2 Arch User Repository](#Arch_User_Repository)
*   [5 Control of systemd units](#Control_of_systemd_units)
*   [6 System-wide versus user-specific configuration](#System-wide_versus_user-specific_configuration)
    *   [6.1 Common shell files](#Common_shell_files)
*   [7 Pseudo-variables in code examples](#Pseudo-variables_in_code_examples)
    *   [7.1 Ellipses](#Ellipses)

## Regular user or root

Some lines are written like so:

```
# mkinitcpio -p linux

```

Others have a different prefix:

```
$ makepkg -s

```

The numeral or hash sign (`#`) indicates that the line is to be entered as _root_, whereas the dollar sign (`$`) shows that the line is to be entered as a _regular user_.

**Note:** The commands prefixed with `#` are intended to be executed from a _root shell_, which can for example be easily accessed with `sudo -i`. Running `sudo _command_` from an unprivileged shell instead of `_command_` from a root shell will also work in most cases, with some notable exceptions such as [redirection](https://en.wikipedia.org/wiki/Redirection_(computing) "wikipedia:Redirection (computing)") and [substitution](https://en.wikipedia.org/wiki/Command_substitution "wikipedia:Command substitution"), which strictly require a root shell. See also [sudo](/index.php/Sudo "Sudo").

A notable exception to watch out for:

```
# This alias makes ls colorize the listing
alias ls='ls --color=auto'

```

In this example, the context surrounding the numeral sign communicates that this is not to be run as a command; it should be edited into a file instead. So in this case, the numeral sign denotes a _comment_. A comment can be explanatory text that will not be interpreted by the associated program. [Bash](/index.php/Bash "Bash") scripts denotation for comments happens to coincide with the root _PS1_.

After further examination, "give away" signs include the uppercase character following the `#` sign. Usually, Unix commands are not written this way and most of the time they are short abbreviations instead of full-blown English words (e.g., _Copy_ becomes _cp_).

Regardless, most articles make this easy to discern by notifying the reader:

_Append_ to `~/path/to/file`:

```
# This alias makes ls colorize the listing
alias ls='ls --color=auto

```

## Append, add, create, edit

When prompted to _append_, _add_, _create_ or _edit_, consider it an indication for using a text editor, such as [nano](/index.php/Nano "Nano"), in order to make changes to configuration file(s):

```
# nano /etc/bash.bashrc

```

Creating or overwriting a file from a string can also be done with [output redirection](http://www.gnu.org/software/bash/manual/html_node/Redirections.html):

```
# echo myhostname > /etc/hostname

```

In a similar fashion, appending a string to a file can be done with:

```
# echo "[custom-repo]" >> /etc/pacman.conf

```

## Source

Some applications, notably [command-line shells](/index.php/Command-line_shell "Command-line shell"), use scripts for their configuration: after modifying them, they must be _sourced_ in order for the changes to be applied. In the case of [bash](/index.php/Bash "Bash"), for example, this is done by running (you can also replace `source` with `.`):

```
$ source ~/.bashrc

```

When the wiki will suggest to modify such a configuration script, it will not explicitly remind you to source the file, and only in some cases it will point you to this section with a reminder link.

## Installation of packages

When an article invites to install some packages in the conventional way, it will not indicate the detailed instructions to do so, instead it will simply mention the names of the packages to be installed, possibly with a link pointing to this very article's section. The subsections below give an overview of the generic installation procedures depending on the package type.

### Official packages

For packages from the [official repositories](/index.php/Official_repositories "Official repositories") you will read something like:

Install the [foobar](https://www.archlinux.org/packages/?name=foobar) package.

This means that you have to run:

```
# pacman -S foobar

```

The [pacman](/index.php/Pacman "Pacman") article contains detailed explanations to deal with package management in Arch Linux proficiently.

### Arch User Repository

For packages from the [Arch User Repository](/index.php/Arch_User_Repository "Arch User Repository") you will read something like:

Install the [foobar](https://aur.archlinux.org/packages/foobar/)<sup><small>AUR</small></sup> package.

This means that in general you have to follow the [foobar](https://aur.archlinux.org/packages/foobar/)<sup><small>AUR</small></sup> link, download the PKGBUILD archive, extract it, **verify the content** and finally run, in the same folder:

```
$ makepkg -sri

```

The [Arch User Repository](/index.php/Arch_User_Repository "Arch User Repository") article contains all the detailed explanations and best practices to deal with AUR packages.

## Control of systemd units

When an article invites to _start_, _enable_, _stop_ or _restart_ some systemd units (e.g. a service), it will not indicate the detailed instructions to do so, but instead you will read something like:

[Start](/index.php/Start "Start") `example.service`.

This means that you have to run:

```
# systemctl start example.service

```

The [Start](/index.php/Start "Start") link will lead you to the [systemd](/index.php/Systemd "Systemd") article, which contains all the detailed explanations to deal with systemd units in Arch Linux proficiently.

## System-wide versus user-specific configuration

It is important to remember that there are two different kinds of configurations on a GNU/Linux system. **System-wide** configuration affects all users. Since system-wide settings are generally located in the `/etc` directory, root privileges are required in order to alter them. For example, to apply a Bash setting that affects all users, `/etc/bash.bashrc` should be modified.

**User-specific** configuration affects only a single user. _Dotfiles_ are used for user-specific configuration. For example, the file `~/**.**bashrc` is the user-specific configuration file. The idea is that each user can define their own settings, such as aliases, functions and other interactive features like the prompt, without affecting other users' preferences.

**Note:** `~/` and `$HOME` are shortcuts for the user's home directory, usually `/home/_username_/`.

### Common shell files

Bash and other Bourne-compatible shells, such as [Zsh](/index.php/Zsh "Zsh"), also source files depending on whether the shell is a _login shell_ or an _interactive shell_. See [Bash#Configuration_files](/index.php/Bash#Configuration_files "Bash") and [Zsh#Configuration_files](/index.php/Zsh#Configuration_files "Zsh") for details.

## Pseudo-variables in code examples

Some code blocks may contain so-called _pseudo-variables_, which, as the name says, are not actual variables used in the code. Instead they are generic placeholders and have to be manually replaced with system-specific configuration items **before** the code may be run or parsed. In the articles that comply with [Help:Style/Formatting and punctuation](/index.php/Help:Style/Formatting_and_punctuation "Help:Style/Formatting and punctuation"), _pseudo-variables_ are formatted in italics.

For example:

*   [Enable](/index.php/Enable "Enable") the `dhcpcd@_interface_name_.service` for the network interface identified from the output of the `ip link` command.

In this case `_interface_name_` is used as a _pseudo-variable_ placeholder in a systemd template unit. All systemd template units, identifiable by the `@` sign, require a system-specific configuration item as argument. See [Systemd#Using units](/index.php/Systemd#Using_units "Systemd").

*   The command `dd if=_data_source_ of=/dev/sd"X" bs=_sector_size_ count=_sector_number_ seek=_partitions_start_sector_` can be run as root to wipe a partition with the specific parameters.

In this case the _pseudo-variables_ are used to describe the parameters that must be substituted for them. Details on how to gather them are elaborated on in the section [Securely wipe disk#Calculate blocks to wipe manually](/index.php/Securely_wipe_disk#Calculate_blocks_to_wipe_manually "Securely wipe disk"), which features the command.

[![Tango-view-fullscreen.png](/images/3/38/Tango-view-fullscreen.png)](/index.php/File:Tango-view-fullscreen.png)

[![Tango-view-fullscreen.png](/images/3/38/Tango-view-fullscreen.png)](/index.php/File:Tango-view-fullscreen.png)

**This article or section needs expansion.**

**Reason:** Mention other examples, ideally from other device categories (e.g. storage), with links to background articles. The examples are meant to avoid duplicating existing explanations in other articles. (Discuss in [Help talk:Reading#](https://wiki.archlinux.org/index.php/Help_talk:Reading))

In case of file examples, pasting pseudo-variables in real configuration files might break the programs that use them.

### Ellipses

In most cases ellipses (`...`) are not part of the actual file content or code output, and instead represent omitted or optional text that is not relevant for the discussed subject.

For example `HOOKS="... encrypt ... filesystems ..."` or:

 `/etc/X11/xorg.conf.d/50-synaptics.conf` 

```
Section "InputClass"
    ...
    Option      "CircularScrolling"          "on"
    Option      "CircScrollTrigger"          "0"
    ...
EndSection

```

Be aware though that, in a few instances, ellipses may be a meaningful part of the code syntax: attentive users will be able to easily recognize these cases by the context.

Retrieved from "[https://wiki.archlinux.org/index.php?title=Help:Reading&oldid=410007](https://wiki.archlinux.org/index.php?title=Help:Reading&oldid=410007)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [Help](/index.php/Category:Help "Category:Help")

Hidden category:

*   [Pages or sections flagged with Template:Expansion](/index.php/Category:Pages_or_sections_flagged_with_Template:Expansion "Category:Pages or sections flagged with Template:Expansion")