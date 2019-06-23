Related articles

*   [dotfiles](/index.php/Dotfiles "Dotfiles")
*   [Core utilities](/index.php/Core_utilities "Core utilities")

From [Wikipedia](https://en.wikipedia.org/wiki/Unix_shell "wikipedia:Unix shell"):

	A Unix shell is a command-line interpreter or shell that provides a traditional user interface for the Unix operating system and for Unix-like systems. Users direct the operation of the computer by entering commands as text for a command line interpreter to execute or by creating text scripts of one or more such commands.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 List of shells](#List_of_shells)
    *   [1.1 POSIX compliant](#POSIX_compliant)
    *   [1.2 Alternative shells](#Alternative_shells)
*   [2 Changing your default shell](#Changing_your_default_shell)
*   [3 Configuration files](#Configuration_files)
    *   [3.1 /etc/profile](#/etc/profile)
    *   [3.2 Standardisation](#Standardisation)
*   [4 Input and output](#Input_and_output)
*   [5 See also](#See_also)

## List of shells

Shells that are more or less [POSIX compliant](http://pubs.opengroup.org/onlinepubs/009695399/utilities/xcu_chap02.html) are listed under [#POSIX compliant](#POSIX_compliant), while shells that have a different syntax are under [#Alternative shells](#Alternative_shells).

### POSIX compliant

These shells can all be linked from `/usr/bin/sh`. When [Bash](/index.php/Bash "Bash"), [mksh](https://www.archlinux.org/packages/?name=mksh) and [zsh](/index.php/Zsh "Zsh") are invoked with the `sh` name, they automatically become more POSIX compliant.

*   **[Bash](/index.php/Bash "Bash")** — Bash extends the Bourne shell with command-line history and completion, indexed and associative arrays, integer arithmetic, process substitution, here strings, regular expression matching and brace expansion.

	[https://www.gnu.org/software/bash/](https://www.gnu.org/software/bash/) || [bash](https://www.archlinux.org/packages/?name=bash)

*   **[DASH](/index.php/Dash "Dash")** — Descendant of the NetBSD version of the Almquist SHell (ash). A fast POSIX-compliant shell that aims to be as small as possible.

	[http://gondor.apana.org.au/~herbert/dash/](http://gondor.apana.org.au/~herbert/dash/) || [dash](https://www.archlinux.org/packages/?name=dash)

*   **[KornShell](/index.php/KornShell "KornShell") (ksh)** — The KornShell language is a complete, powerful, high-level programming language for writing applications, often more easily and quickly than with other high-level languages. This makes it especially suitable for prototyping. ksh has the best features of the Bourne shell and the C shell, plus many new features of its own. Thus ksh can do much to enhance your productivity and the quality of your work, both in interacting with the system, and in programming. ksh programs are easier to write, and are more concise and readable than programs written in a lower level language such as C.

	[http://www.kornshell.com](http://www.kornshell.com) || See the [article](/index.php/Ksh#Installation "Ksh").

*   **[Zsh](/index.php/Zsh "Zsh")** — Shell designed for interactive use, although it is also a powerful scripting language. Many of the useful features of Bash, ksh, and tcsh were incorporated into Zsh; many original features were added. The [introductory document](http://zsh.sourceforge.net/Intro/intro_toc.html) details some of the unique features of Zsh.

	[https://www.zsh.org/](https://www.zsh.org/) || [zsh](https://www.archlinux.org/packages/?name=zsh)

**Tip:** POSIX and Bash scripts can be linted with [shellcheck](https://www.archlinux.org/packages/?name=shellcheck).

### Alternative shells

*   **[C shell](https://en.wikipedia.org/wiki/C_shell "wikipedia:C shell") (tcsh)** — Command language interpreter usable both as an interactive login shell and a shell script command processor. It includes a command-line editor, programmable word completion, spelling correction, a history mechanism, job control and a C-like syntax.

	[http://www.tcsh.org](http://www.tcsh.org) || [tcsh](https://www.archlinux.org/packages/?name=tcsh)

*   **Elvish** — Elvish is a modern and expressive shell, that can carry internal structured values through pipelines. This feature makes possible avoiding a lot of complex text processing code. It features an expressive programming language, with features like exceptions, namespacing and anonymous functions. It also has a powerful readline which checks the syntax while typing, and syntax highlighting by default.

	[https://elvish.io](https://elvish.io) || [elvish](https://aur.archlinux.org/packages/elvish/)

*   **[fish](/index.php/Fish "Fish")** — Smart and user-friendly command line shell. Fish performs full-color command line syntax highlighting, as well as highlighting and completion for commands and their arguments, file existence, and history. It supports complete-as-you-type for history and commands. Fish is able to parse the system's man pages in order to determine valid arguments for commands, allowing it to highlight and complete commands. Easy last-command revision can be done using `Alt+Up`. The fish daemon (fishd) facilitates synchronized history across all instances of fish, as well as universal and persistent environment variables. Additionally, fish features significantly simplified programming syntax and control flow (similar to ruby). For more information, see the [tutorial](http://fishshell.com/docs/current/tutorial).

	[http://fishshell.com/](http://fishshell.com/) || [fish](https://www.archlinux.org/packages/?name=fish)

*   **[Nash](/index.php/Nash "Nash")** — Nash is a system shell, inspired by plan9 rc, that makes it easy to create reliable and safe scripts taking advantages of operating systems namespaces (on linux and plan9) in an idiomatic way.

	[https://github.com/NeowayLabs/nash](https://github.com/NeowayLabs/nash) || [nash-git](https://aur.archlinux.org/packages/nash-git/)

*   **Oh** — Unix shell written in Go. It is similar in spirit but different in detail from other Unix shells. Oh extends the shell's programming language features without sacrificing the shell's interactive features.

	[https://github.com/michaelmacinnis/oh](https://github.com/michaelmacinnis/oh) || [oh-git](https://aur.archlinux.org/packages/oh-git/)

*   **[PowerShell](https://en.wikipedia.org/wiki/PowerShell "wikipedia:PowerShell")** — PowerShell is an object-oriented programming language and interactive command line shell, originally written for and exclusive to Windows. Later on, it was open sourced and ported to Mac OS X and Linux.

	[https://github.com/PowerShell/PowerShell](https://github.com/PowerShell/PowerShell) || [powershell](https://aur.archlinux.org/packages/powershell/)

*   **[rc](https://en.wikipedia.org/wiki/rc "wikipedia:rc")** — Command interpreter for Plan 9 that provides similar facilities to UNIX’s Bourne shell, with some small additions and less idiosyncratic syntax.

	[http://doc.cat-v.org/plan_9/4th_edition/papers/rc](http://doc.cat-v.org/plan_9/4th_edition/papers/rc) || [9base](https://www.archlinux.org/packages/?name=9base)

*   **xonsh** — A retrocompatible shell based on the python interpreter.

	[http://xon.sh/](http://xon.sh/) || [xonsh](https://www.archlinux.org/packages/?name=xonsh)

## Changing your default shell

After installing one the above shells, you can execute that shell inside of your current shell, by just running its executable. If you want to be served that shell when you login however, you will need to change your default shell.

To list all installed shells, run:

```
$ chsh -l

```

And to set one as default for your user do:

```
$ chsh -s *full-path-to-shell*

```

where *full-path-to-shell* is the full path as given by `chsh -l`.

If you now log out and log in again, you will be greeted by the other shell.

**Tip:** chsh uses `/etc/shells` as reference. If a recently installed shell is not present on the list, it can be manually added to this file.

## Configuration files

To autostart programs in console or upon login, you can use shell startup files/directories. Read the documentation for your shell, or its ArchWiki article, e.g. [Bash#Configuration files](/index.php/Bash#Configuration_files "Bash") or [Zsh#Startup/Shutdown files](/index.php/Zsh#Startup/Shutdown_files "Zsh").

See also [configuration files](https://en.wikipedia.org/wiki/Unix_shell#Configuration_files "wikipedia:Unix shell").

### /etc/profile

Upon login, all Bourne-compatible shells source `/etc/profile`, which in turn sources any readable `*.sh` files in `/etc/profile.d/`: these scripts do not require an interpreter directive, nor do they need to be executable. They are used to set up an environment and define application-specific settings.

### Standardisation

It is possible to make (some) shells configuration files follow the same naming convention, as well as supporting some common configuration between the shells.

See [the article about this](https://blog.flowblok.id.au/2013-02/shell-startup-scripts.html) and the [related repository](https://bitbucket.org/flowblok/shell-startup).

## Input and output

See also [GregsWiki](https://mywiki.wooledge.org/BashGuide/InputAndOutput "gregswiki:BashGuide/InputAndOutput") and [I/O Redirection](http://www.tldp.org/LDP/abs/html/io-redirection.html).

*   Redirections truncate files before commands are executed: `*command* *file* > *file*` will therefore not work as expected. While some commands ([sed](/index.php/Sed "Sed") for example) provide an option to edit files in-place, many do not. In such cases you can use the [sponge(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/sponge.1) command from the [moreutils](https://www.archlinux.org/packages/?name=moreutils) package.
*   Because *cat* is not built into the shell, on many occasions you may find it more convenient to use a [redirection](https://en.wikipedia.org/wiki/Redirection_(computing) "wikipedia:Redirection (computing)"), for example in scripts, or if you care a lot about performance. In fact `< *file*` does the same as `cat *file*`.
*   POSIX-compliant shells support [Here Documents](http://tldp.org/LDP/abs/html/here-docs.html):

```
$ cat << EOF
one
two
three
EOF

```

*   Shell [pipelines](https://en.wikipedia.org/wiki/Pipeline_(Unix) operate on stdout by default. To operate on [stderr(3)](https://jlk.fjfi.cvut.cz/arch/manpages/man/stderr.3) you can redirect *stderr* to *stdout* with `*command* 2>&1 | *othercommand*` or, for Bash 4, `*command* |& *othercommand*`.
*   Remember that many GNU [core utilities](/index.php/Core_utilities "Core utilities") accept files as arguments, so for example `grep *pattern* < *file*` is replaceable with `grep *pattern* *file*`.

## See also

*   [Evolution of shells in Linux](http://www.ibm.com/developerworks/linux/library/l-linux-shells/index.html) on the IBM developerWorks
*   [terminal.sexy](https://terminal.sexy/) — Terminal Color Scheme Designer
*   [Hyperpolyglot](http://hyperpolyglot.org/unix-shells) — Side-by-side comparison of shell syntaxes
*   [UNIX Power Tools](http://docstore.mik.ua/orelly/unix/upt/index.htm) — General command-line tool usage
*   [commandlinefu.com](https://www.commandlinefu.com/commands/browse) — Command-line snippets sharing
*   [List of applications#Terminal emulators](/index.php/List_of_applications#Terminal_emulators "List of applications")