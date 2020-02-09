Related articles

*   [Emacs#Custom colors and theme](/index.php/Emacs#Custom_colors_and_theme "Emacs")
*   [nano#Syntax highlighting](/index.php/Nano#Syntax_highlighting "Nano")

This page was created to consolidate colorization of CLI outputs.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Applications](#Applications)
    *   [1.1 diff](#diff)
    *   [1.2 grep](#grep)
    *   [1.3 less](#less)
        *   [1.3.1 Environment variables](#Environment_variables)
        *   [1.3.2 Reading from stdin](#Reading_from_stdin)
    *   [1.4 ls](#ls)
    *   [1.5 man](#man)
        *   [1.5.1 Using less](#Using_less)
        *   [1.5.2 Using most](#Using_most)
        *   [1.5.3 Using X resources](#Using_X_resources)
            *   [1.5.3.1 xterm](#xterm)
            *   [1.5.3.2 rxvt-unicode](#rxvt-unicode)
    *   [1.6 pacman](#pacman)
*   [2 Wrappers](#Wrappers)
    *   [2.1 Universal wrappers](#Universal_wrappers)
    *   [2.2 Libraries for colorizing an output](#Libraries_for_colorizing_an_output)
    *   [2.3 Application specific](#Application_specific)
        *   [2.3.1 Compilers](#Compilers)
        *   [2.3.2 diff](#diff_2)
        *   [2.3.3 less](#less_2)
            *   [2.3.3.1 source-highlight](#source-highlight)
            *   [2.3.3.2 lesspipe](#lesspipe)
        *   [2.3.4 Make](#Make)
        *   [2.3.5 Ping](#Ping)
*   [3 Shells](#Shells)
    *   [3.1 bash](#bash)
    *   [3.2 zsh](#zsh)
    *   [3.3 Fish](#Fish)
*   [4 Terminal emulators](#Terminal_emulators)
    *   [4.1 Virtual console](#Virtual_console)
        *   [4.1.1 Login screen](#Login_screen)
    *   [4.2 X window system](#X_window_system)
    *   [4.3 Display all 256 colors](#Display_all_256_colors)
    *   [4.4 Display tput escape codes](#Display_tput_escape_codes)
    *   [4.5 Enumerate supported colors](#Enumerate_supported_colors)
    *   [4.6 Enumerate terminal capabilities](#Enumerate_terminal_capabilities)
    *   [4.7 Color scheme scripts](#Color_scheme_scripts)
    *   [4.8 True color support](#True_color_support)
*   [5 See also](#See_also)

## Applications

### diff

diffutils from version 3.4 includes the `--color` option ([GNU mailing list](https://lists.gnu.org/archive/html/info-gnu/2016-08/msg00004.html)).

```
$ alias diff='diff --color=auto'

```

### grep

The `--color=auto` option enables color highlighting. Color codes are emitted only on standard output; not in pipes or redirection.

Color output in *grep* is also useful with [regexp](https://en.wikipedia.org/wiki/regexp "wikipedia:regexp") tasks.

Use an [alias](/index.php/Alias "Alias") to permanently enable this option:

```
alias grep='grep --color=auto'

```

The `GREP_COLORS` variable is used to define colors, and it configures various parts of highlighting.

See [grep(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/grep.1) for more information.

The `GREP_COLOR` environment variable can be used to define the default highlight color (the default is red). To change the color, find the needed [ANSI escape sequence](http://www.tldp.org/HOWTO/Bash-Prompt-HOWTO/x329.html) and apply it with:

```
export GREP_COLOR="1;32"

```

The `-n` option includes file line numbers in the output.

### less

#### Environment variables

Add the following lines to your shell configuration file:

```
export LESS=-R
export LESS_TERMCAP_mb=$'\E[1;31m'     # begin blink
export LESS_TERMCAP_md=$'\E[1;36m'     # begin bold
export LESS_TERMCAP_me=$'\E[0m'        # reset bold/blink
export LESS_TERMCAP_so=$'\E[01;44;33m' # begin reverse video
export LESS_TERMCAP_se=$'\E[0m'        # reset reverse video
export LESS_TERMCAP_us=$'\E[1;32m'     # begin underline
export LESS_TERMCAP_ue=$'\E[0m'        # reset underline
# and so on

```

Change the values ([ANSI escape code](https://en.wikipedia.org/wiki/ANSI_escape_code#Colors "wikipedia:ANSI escape code")) as you like. [This blog post](http://boredzo.org/blog/archives/2016-08-15/colorized-man-pages-understood-and-customized) and the page [Bash/Prompt customization](/index.php/Bash/Prompt_customization "Bash/Prompt customization") also help.

**Note:** The `LESS_TERMCAP_*xx*` variables are currently undocumented in [less(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/less.1). For a detailed explanation, see [this answer](http://unix.stackexchange.com/questions/108699/documentation-on-less-termcap-variables/108840#108840).

#### Reading from stdin

**Note:** It is recommended to add colored output through [#Environment variables](#Environment_variables) to your `~/.bashrc` or `~/.zshrc`, as the below is based on `export LESS=R`

When you run a command and pipe its [standard output](https://en.wikipedia.org/wiki/Standard_output "wikipedia:Standard output") (*stdout*) to *less* for a paged view (e.g. `pacman -Qe | less`), you may find that the output is no longer colored. This is usually because the program tries to detect if its *stdout* is an interactive terminal, in which case it prints colored text, and otherwise prints uncolored text. This is good behaviour when you want to redirect *stdout* to a file, e.g. `pacman -Qe > pkglst-backup.txt`, but less suited when you want to view output in `less`.

Some programs provide an option to disable the interactive tty detection:

```
# dmesg --color=always | less

```

In case that the program does not provide any similar option, it is possible to trick the program into thinking its *stdout* is an interactive terminal with the following utilities:

*   **ColorThis** — Force colored output of a program by running it within a (group of) pty, support forwarding stdin.

	[https://github.com/Sasasu/ColorThis](https://github.com/Sasasu/ColorThis) || <small>not packaged? [search in AUR](https://aur.archlinux.org/packages/)</small>

*   **stdoutisatty** — A small program which catches the `isatty` function call.

	[https://github.com/lilydjwg/stdoutisatty](https://github.com/lilydjwg/stdoutisatty). || [stdoutisatty-git](https://aur.archlinux.org/packages/stdoutisatty-git/)

	Example: `stdoutisatty *program* | less`

*   **unbuffer** — A tclsh script comes with expect, it invokes desired program within a pty.

	[http://expect.sourceforge.net/example/unbuffer.man.html](http://expect.sourceforge.net/example/unbuffer.man.html) || [expect](https://www.archlinux.org/packages/?name=expect)

	Example: `unbuffer *program* | less`

Alternatively, using [zpty](http://zsh.sourceforge.net/Doc/Release/Zsh-Modules.html#The-zsh_002fzpty-Module) module from [zsh](/index.php/Zsh "Zsh"): [[1]](http://lilydjwg.is-programmer.com/2011/6/29/using-zpty-module-of-zsh.27677.html)

 `~/.zshrc` 
```
zmodload zsh/zpty

pty() {
	zpty pty-${UID} ${1+$@}
	if [[ ! -t 1 ]];then
		setopt local_traps
		trap '' INT
	fi
	zpty -r pty-${UID}
	zpty -d pty-${UID}
}

ptyless() {
	pty $@ | less
}

```

Usage:

```
$ ptyless *program*

```

To pipe it to other pager (less in this example):

```
$ pty *program* | less

```

### ls

The `--color=auto` option enables color highlighting. Color codes are emitted only on standard output; not in pipes or redirection.

Use an [alias](/index.php/Alias "Alias") to permanently enable this option:

```
alias ls='ls --color=auto'

```

The `LS_COLORS` variable is used to define colors, and it configures various parts of highlighting. Use the [dircolors(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/dircolors.1) command to set it.

**Note:** Using the `--color` option may incur a noticeable performance penalty when *ls* is run in a directory with very many entries. The default settings require *ls* to [stat(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/stat.1) every single file it lists. However, if you would like most of the file-type coloring but can live without the other coloring options (e.g. executable, orphan, sticky, other-writable, capability), use *dircolors* to set the `LS_COLORS` environment variable like this:
```
eval $(dircolors -p | perl -pe 's/^((CAP|S[ET]|O[TR]|M|E)\w+).*/$1 00/' | dircolors -)

```

See [ls(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/ls.1) for more information.

### man

To enable colored `man`, two main pagers, `less` and `most`, are hacked here.

#### Using less

See [#less](#less) for a more detailed description.

For bash or zsh, add the following `less` wrapper function to `~/.bashrc` or `~/.zshrc`:

```
man() {
    LESS_TERMCAP_md=$'\e[01;31m' \
    LESS_TERMCAP_me=$'\e[0m' \
    LESS_TERMCAP_se=$'\e[0m' \
    LESS_TERMCAP_so=$'\e[01;44;33m' \
    LESS_TERMCAP_ue=$'\e[0m' \
    LESS_TERMCAP_us=$'\e[01;32m' \
    command man "$@"
}

```

For [Fish](/index.php/Fish "Fish") you could accomplish this with:

 `~/.config/fish/config.fish` 
```
set -xU LESS_TERMCAP_md (printf "\e[01;31m")
set -xU LESS_TERMCAP_me (printf "\e[0m")
set -xU LESS_TERMCAP_se (printf "\e[0m")
set -xU LESS_TERMCAP_so (printf "\e[01;44;33m")
set -xU LESS_TERMCAP_ue (printf "\e[0m")
set -xU LESS_TERMCAP_us (printf "\e[01;32m")

```

Remember to source your config or restart your shell to make the changes take effect.

#### Using most

The basic function of 'most' is similar to `less` and `more`, but it has a smaller feature set. Configuring most to use colors is easier than using less, but additional configuration is necessary to make most behave like less. Install the [most](https://www.archlinux.org/packages/?name=most) package.

Edit `/etc/man_db.conf`, uncomment the pager definition and change it to:

```
DEFINE     pager     most -s

```

Test the new setup by typing:

```
$ man whatever_man_page

```

Modifying the color values requires editing `~/.mostrc` (creating the file if it is not present) or editing `/etc/most.conf` for system-wide changes. Example `~/.mostrc`:

```
% Color settings
color normal lightgray black
color status yellow blue
color underline yellow black
color overstrike brightblue black

```

A list of all keybindings may be found at `/usr/share/doc/most/most-fun.txt`. To get a basic `less`/`vim`-like configuration, you can copy `/usr/share/doc/most/lesskeys.rc` to `~/.mostrc`. The lesskeys rc included with most does not include 'g' or 'G', so you will also have to add these lines to `~/.mostrc`:

```
setkey bob "g"
setkey eob "G"
setkey page_down "d"
setkey page_up "u"

```

You may also want to set the `goto_line` keybinding in the rc if you don't like the default of 'J'.

Another example showing keybindings similar to `less` (jump to line is set to 'J'):

```
% less-like keybindings
unsetkey "^K"
unsetkey "g"
unsetkey "G"
unsetkey ":"

setkey next_file ":n"
setkey find_file ":e"
setkey next_file ":p"
setkey toggle_options ":o"
setkey toggle_case ":c"
setkey delete_file ":d"
setkey exit ":q"

setkey bob "g"
setkey eob "G"
setkey down "e"
setkey down "E"
setkey down "j"
setkey down "^N"
setkey up "y"
setkey up "^Y"
setkey up "k"
setkey up "^P"
setkey up "^K"
setkey page_down "f"
setkey page_down "^F"
setkey page_up "b"
setkey page_up "^B"
setkey other_window "z"
setkey other_window "w"
setkey search_backward "?"
setkey bob "p"
setkey goto_mark "'"
setkey find_file "E"
setkey edit "v"

```

#### Using X resources

A quick way to add color to manual pages viewed on [xterm](https://www.archlinux.org/packages/?name=xterm)/`uxterm` or [rxvt-unicode](https://www.archlinux.org/packages/?name=rxvt-unicode) is to modify `~/.Xresources`.

##### xterm

```
*VT100.colorBDMode:     true
*VT100.colorBD:         red
*VT100.colorULMode:     true
*VT100.colorUL:         cyan

```

which *replaces* the decorations with the colors. Also add:

```
*VT100.veryBoldColors: 6

```

if you want colors and decorations (bold or underline) *at the same time*. See [xterm(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/xterm.1) for a description of the `veryBoldColors` resource.

##### rxvt-unicode

```
URxvt.colorIT:      #87af5f
URxvt.colorBD:      #d7d7d7
URxvt.colorUL:      #87afd7

```

Run:

```
$ xrdb -load ~/.Xresources

```

Launch a new `xterm/uxterm` or `rxvt-unicode` and you should see colorful man pages.

This combination puts colors to **bold** and <u>underlined</u> words in `xterm/uxterm` or to **bold**, <u>underlined</u>, and *italicized* text in `rxvt-unicode`. You can play with different combinations of these attributes (see the [sources](http://pub.ligatura.org/fs/xfree86/xresources/xterm) of this item).

### pacman

[Pacman](/index.php/Pacman "Pacman") has a color option. Uncomment the `Color` line in `/etc/pacman.conf`.

## Wrappers

### Universal wrappers

(most of them outdated but still functioning)

They go with multiple preconfigured presets that can be changed, and new can be created/contributed.

**Warning:** Wrappers replace output of commands with escape sequences. Some shell scripts and programs which use the output of standard shell utilities may work wrong.

*   **rainbow** — Colorize commands output or STDIN using patterns.
    Presets: df, diff, env, host, ifconfig, java-stack-trace, jboss, jonas, md5sum, mvn2, mvn3, ping, tomcat, top, traceroute.

	[https://github.com/nicoulaj/rainbow](https://github.com/nicoulaj/rainbow) || [rainbow](https://aur.archlinux.org/packages/rainbow/)

*   **grc** — Yet another colouriser for beautifying your logfiles or output of commands.
    Presets: cat, cvs, df, digg, gcc, g++, ls, ifconfig, make, mount, mtr, netstat, ping, ps, tail, traceroute, wdiff, blkid, du, dnf, docker, docker-machine, env, id, ip, iostat, last, lsattr, lsblk, lspci, lsmod, lsof, getfacl, getsebool, ulimit, uptime, nmap, fdisk, findmnt, free, semanage, sar, ss, sysctl, systemctl, stat, showmount, tune2fs and tcpdump.

	[https://github.com/pengwynn/grc](https://github.com/pengwynn/grc) || [grc](https://www.archlinux.org/packages/?name=grc)

*   **colorlogs** — Colorize commands output or STDIN using patterns.
    Presets: logs, git status, ant, maven.

	[https://github.com/memorius/colorlogs](https://github.com/memorius/colorlogs) || <small>not packaged? [search in AUR](https://aur.archlinux.org/packages/)</small>

*   **cope** — A colourful wrapper for terminal programs.
    Presets: acpi, arp, cc, df, dprofpp, fdisk, free, g++, gcc, id, ifconfig, ls, lspci, lsusb, make, md5sum, mpc, netstat, nm, nmap, nocope, ping, pmap, ps, readelf, route, screen, sha1sum, sha224sum, sha256sum, sha384sum, sha512sum, shasum, socklist, stat, strace, tcpdump, tracepath, traceroute, w, wget, who, xrandr.

	[https://github.com/yogan/cope](https://github.com/yogan/cope) || [cope-git](https://aur.archlinux.org/packages/cope-git/)

*   **cw** — A non-intrusive real-time ANSI color wrapper for common unix-based commands. Wraps [file](https://www.archlinux.org/packages/?name=file) which can cause issues.
    Presets: arp, arping, auth.log@, blockdev, cal, cksum, clock, configure, cpuinfo@, crontab@, cw-pipe, cw-test.cgi, date, df, diff, dig, dmesg, du, env, figlet, file, find, finger, free, fstab@, fuser, g++, gcc, group@, groups, hdparm, hexdump, host, hosts@, id, ifconfig, inittab@, iptables, last, lastlog, lsattr, lsmod, lsof, ltrace-color, make, md5sum, meminfo@, messages@, mount, mpg123, netstat, nfsstat, nmap, nslookup, objdump, passwd@, ping, pmap, pmap_dump, praliases, profile@, protocols@, ps, pstree, quota, quotastats, resolv.conf@, route, routel, sdiff, services@, showmount, smbstatus, stat, strace-color, sysctl, syslog, tar, tcpdump, tracepath, traceroute, umount, uname, uptime, users, vmstat, w, wc, whereis, who, xferlog.

	[http://cwrapper.sourceforge.net/](http://cwrapper.sourceforge.net/) || [cw](https://aur.archlinux.org/packages/cw/)

*   **ccze** — A fast log colorizer written in C, intended to be a drop-in replacement for colorize

	[https://github.com/cornet/ccze/](https://github.com/cornet/ccze/) || [ccze](https://www.archlinux.org/packages/?name=ccze)

### Libraries for colorizing an output

*   **libtextstyle** — A C library for styling text output to terminals

	[https://ftp.gnu.org/gnu/gettext/gettext-0.20.1.tar.gz](https://ftp.gnu.org/gnu/gettext/gettext-0.20.1.tar.gz) || <small>not packaged? [search in AUR](https://aur.archlinux.org/packages/)</small>

*   **ruby-rainbow** — Rainbow is extension to ruby's String class adding support for colorizing text on ANSI terminal

	[https://rubygems.org/gems/rainbow/](https://rubygems.org/gems/rainbow/) || [ruby-rainbow](https://www.archlinux.org/packages/?name=ruby-rainbow)

*   **python-blessings** — A thin, practical wrapper around terminal coloring, styling, and positioning

	[https://github.com/erikrose/blessings](https://github.com/erikrose/blessings) || [python-blessings](https://www.archlinux.org/packages/?name=python-blessings), [python2-blessings](https://www.archlinux.org/packages/?name=python2-blessings)

*   **lolcat** — Ruby program that makes the output colorful like a rainbow

	[https://github.com/busyloop/lolcat/](https://github.com/busyloop/lolcat/) || [lolcat](https://www.archlinux.org/packages/?name=lolcat)

### Application specific

#### Compilers

*   **colorgcc** — A Perl wrapper to colorize the output of compilers with warning/error messages matching the gcc output format

	[https://schlueters.de/colorgcc.html](https://schlueters.de/colorgcc.html) || [colorgcc](https://www.archlinux.org/packages/?name=colorgcc)

#### diff

Diff has [built-in color output](#diff), which is reasonable to use. But the following wrappers can be used:

*   **colordiff** — Perl script for *diff* highlighting.

	[http://www.colordiff.org/](http://www.colordiff.org/) || [colordiff](https://www.archlinux.org/packages/?name=colordiff)

*   **cwdiff** — *(w)diff* wrapper with directories support and highlighting.

	[https://github.com/junghans/cwdiff](https://github.com/junghans/cwdiff) || [cwdiff](https://aur.archlinux.org/packages/cwdiff/), [cwdiff-git](https://aur.archlinux.org/packages/cwdiff-git/)

#### less

##### source-highlight

You can enable code syntax coloring in *less*. First, [install](/index.php/Install "Install") [source-highlight](https://www.archlinux.org/packages/?name=source-highlight), then add these lines to your shell configuration file:

 `~/.bashrc` 
```
export LESSOPEN="| /usr/bin/source-highlight-esc.sh %s"
export LESS='-R '

```

##### lesspipe

Frequent users of the command line interface might want to install [lesspipe](https://www.archlinux.org/packages/?name=lesspipe).

Users may now list the compressed files inside of an archive using their pager:

 `$ less *compressed_file*.tar.gz` 
```
==> use tar_file:contained_file to view a file in the archive
-rw------- *username*/*group*  695 2008-01-04 19:24 *compressed_file*/*content1*
-rw------- *username*/*group*   43 2007-11-07 11:17 *compressed_file*/*content2*
*compressed_file*.tar.gz (END)
```

*lesspipe* also grants *less* the ability of interfacing with files other than archives, serving as an alternative for the specific command associated for that file-type (such as viewing HTML via [python-html2text](https://www.archlinux.org/packages/?name=python-html2text)).

Re-login after installing *lesspipe* in order to activate it, or source `/etc/profile.d/lesspipe.sh`.

#### Make

*   **colormake** — A simple wrapper around make to make its output more readable.

	[http://bre.klaki.net/programs/colormake/](http://bre.klaki.net/programs/colormake/) || [colormake](https://aur.archlinux.org/packages/colormake/), [colormake-git](https://aur.archlinux.org/packages/colormake-git/)

#### Ping

*   **prettyping** — Add some great features to ping monitoring. A wrapper around the standard ping tool with the objective of making the output prettier, more colorful, more compact, and easier to read.

	[http://denilson.sa.nom.br/prettyping/](http://denilson.sa.nom.br/prettyping/) || [prettyping](https://www.archlinux.org/packages/?name=prettyping)

## Shells

### bash

See [Bash/Prompt customization#Colors](/index.php/Bash/Prompt_customization#Colors "Bash/Prompt customization").

### zsh

See [Zsh#Colors](/index.php/Zsh#Colors "Zsh").

### Fish

See [Fish#Web interface](/index.php/Fish#Web_interface "Fish").

## Terminal emulators

### Virtual console

The colors in the [Linux virtual console](https://en.wikipedia.org/wiki/Virtual_console "w:Virtual console") running on the framebuffer can be changed. This is done by writing the escape code `\\e]PXRRGGBB`, where `X` is the hexadecimal index of the color from 0-F, and `RRGGBB` is a traditional hexadecimal RGB code.

For example, to reuse existing colors defined in `~/.Xresources`, add the following to the shell initialization file (such as `~/.bashrc`):

```
if [ "$TERM" = "linux" ]; then
    _SEDCMD='s/.*\*color\([0-9]\{1,\}\).*#\([0-9a-fA-F]\{6\}\).*/\1 \2/p'
    for i in $(sed -n "$_SEDCMD" $HOME/.Xresources | awk '$1 < 16 {printf "\\e]P%X%s", $1, $2}'); do
        echo -en "$i"
    done
    clear
fi

```

#### Login screen

The below is a colored example of the virtual console login screen in `/etc/issue`. Create a backup of the original file with `mv /etc/issue /etc/issue.bak` as root, and create a new `/etc/issue`:

```
\e[H\e[2J
                                                            \e[1;30m| \e[34m\r \s
      \e[36;1m/\\\\                        \e[37m||      \e[36m| =                 \e[30m|
     \e[36m/  \\\\                       \e[37m||      \e[36m|                   \e[30m| \e[32m\t
    \e[1;36m/ \e[0;36m.. \e[1m\\\\   \e[37m//==\\\\\\ ||/= /==\\\\ ||/=\\\\  \e[36m| | |/\\\\ |  | \\\\ /  \e[30m| \e[32m\d
   \e[0;36m/ .  . \\\\ \e[37m||    || ||  ||     ||  ||  \e[36m| | |  | |  |   X   \e[1;30m|
  \e[0;36m/  .  .  \\\\ \e[37m\\\\\\==/| ||   \\\\==/ ||  ||  \e[36m| | |  |\  \\/|  / \\\\ \e[1;30m| \e[31m\U
 \e[0;36m/ ..    .. \\\\   \e[0;37mA simple, lightweight linux distribution.   \e[1;30m|
\e[0;36m/_'        `_\\\\                                              \e[1;30m| \e[35m\l \e[0mon \e[1;33m

\e[0m 

```

See also:

*   [https://bbs.archlinux.org/viewtopic.php?pid=386429#p386429](https://bbs.archlinux.org/viewtopic.php?pid=386429#p386429)
*   [http://www.linuxfromscratch.org/blfs/view/svn/postlfs/logon.html](http://www.linuxfromscratch.org/blfs/view/svn/postlfs/logon.html)

### X window system

Most [Xorg](/index.php/Xorg "Xorg") terminals, including [xterm](/index.php/Xterm "Xterm") and [urxvt](/index.php/Urxvt "Urxvt"), support at least 16 basic colors. The colors 0-7 are the 'normal' colors. Colors 8-15 are their 'bright' counterparts, used for highlighting. These colors can be modified through [X resources](/index.php/X_resources "X resources"), or through specific terminal settings. For example:

 `~/.Xresources` 
```
! Black + DarkGrey
*color0:  #000000
*color8:  #555753
! DarkRed + Red
*color1:  #ff6565
*color9:  #ff8d8d
! DarkGreen + Green
*color2:  #93d44f
*color10: #c8e7a8
! DarkYellow + Yellow
*color3:  #eab93d
*color11: #ffc123
! DarkBlue + Blue
*color4:  #204a87
*color12: #3465a4
! DarkMagenta + Magenta
*color5:  #ce5c00
*color13: #f57900
!DarkCyan + Cyan (both not tango)
*color6:  #89b6e2
*color14: #46a4ff
! LightGrey + White
*color7:  #cccccc
*color15: #ffffff
```

**Warning:** Color resources such as `foreground` and `background` can be read by other applications (such as [emacs](https://www.gnu.org/software/emacs/manual/html_node/emacs/Table-of-Resources.html)). This can be avoided by specifiying the class name, for example `XTerm.foreground`.

See also:

*   [#Using X resources](#Using_X_resources) for how to color bold and underlined text automatically.
*   [Color Themes](https://web.archive.org/web/20090130061234/http://phraktured.net/terminal-colors/) - Extensive list of terminal color themes by Phraktured.
*   [Xcolors by dkeg](http://beta.andrewrcraig.us/index.php?page=xcolors)

*   [base16 color schemes](https://github.com/chriskempson/base16)

### Display all 256 colors

Prints all 256 colors across the screen.

```
$ (x=`tput op` y=`printf %76s`;for i in {0..256};do o=00$i;echo -e ${o:${#o}-3:3} `tput setaf $i;tput setab $i`${y// /=}$x;done)

```

### Display tput escape codes

Replace `tput op` with whatever tput you want to trace. `op` is the default foreground and background color.

 `$ ( strace -s5000 -e write tput op 2>&2 2>&1 ) | tee -a /dev/stderr | grep -o '"[^"]*"'` 
```
033[\033[1;34m"\33[39;49m"\033[00m

```

### Enumerate supported colors

The following command will let you discover all the terminals you have terminfo support for, and the number of colors each terminal supports. The possible values are: 8, 15, 16, 52, 64, 88 and 256.

 `$ for T in `find /usr/share/terminfo -type f -printf '%f '`;do echo "$T `tput -T $T colors`";done|sort -nk2` 
```
Eterm-88color 88
rxvt-88color 88
xterm+88color 88
xterm-88color 88
Eterm-256color 256
gnome-256color 256
konsole-256color 256
putty-256color 256
rxvt-256color 256
screen-256color 256
screen-256color-bce 256
screen-256color-bce-s 256
screen-256color-s 256
xterm+256color 256
xterm-256color 256

```

### Enumerate terminal capabilities

This command is useful to see what features that are supported by your terminal.

 `$ infocmp -1 | tr -d '\0\t,' | cut -f1 -d'=' | grep -v "$TERM" | sort | column -c80` 
```
acsc		ed		kcuu1		kich1		rmso
am		el		kDC		kLFT		rmul
bce		el1		kdch1		km		rs1
bel		enacs		kel		kmous		rs2
blink		eo		kend		knp		s0ds
bold		flash		kEND		kNXT		s1ds
btns#5		fsl		kent		kpp		s2ds
bw		home		kf1		kPRV		s3ds
ccc		hpa		kf10		kRIT		sc
civis		hs		kf11		kslt		setab
clear		ht		kf12		lines#24	setaf
cnorm		hts		kf13		lm#0		setb
colors#0x100	ich		kf14		mc0		setf
cols#80		ich1		kf15		mc4		sgr
cr		il		kf16		mc5		sgr0
csr		il1		kf17		mc5i		sitm
cub		ind		kf18		mir		smacs
cub1		indn		kf19		msgr		smam
cud		initc		kf2		ncv#0		smcup
cud1		is1		kf20		npc		smir
cuf		is2		kf3		op		smkx
cuf1		it#8		kf4		pairs#0x7fff	smso
cup		ka1		kf5		rc		smul
cuu		ka3		kf6		rev		tbc
cuu1		kb2		kf7		ri		tsl
cvvis		kbs		kf8		rin		u6
dch		kc1		kf9		ritm		u7
dch1		kc3		kfnd		rmacs		u8
dl		kcbt		kFND		rmam		u9
dl1		kcub1		kHOM		rmcup		vpa
dsl		kcud1		khome		rmir		xenl
ech		kcuf1		kIC		rmkx		xon

```

### Color scheme scripts

See [[2]](https://paste.xinu.at/m-dAiJ/) for scripts which display a chart of your current terminal scheme.

### True color support

Some terminals support the full range of 16 million colors (RGB, each with 8 bit resolution): xterm, konsole, st, etc. The corresponding TERM values `xterm-direct`, `konsole-direct`, `st-direct`, etc. are supported starting with ncurses version 6.1 [[3]](http://lists.gnu.org/archive/html/bug-ncurses/2018-01/msg00045.html). For more info about terminal emulators and applications that support true color, see [[4]](https://gist.github.com/XVilka/8346728).

Note that the Linux kernel supports the SGR escape sequences for true-color, but it is pointless to use it, because the driver maps the 24-bit color specifications to a 256-colors color map in the kernel (see the functions `rgb_foreground`, `rgb_background`). For this reason, there is no terminfo entry `linux-direct`.

## See also

*   [lolcat clone in x64 assembly](https://gkbrk.com/2016/07/lolcat-clone-in-x64-assembly/)
*   [Setting colors for less](http://unix.stackexchange.com/a/147) and [solving related problems](http://unix.stackexchange.com/a/6357) (threads on StackExchange)