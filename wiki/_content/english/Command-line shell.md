Related articles

*   [Bash](/index.php/Bash "Bash")
*   [dotfiles](/index.php/Dotfiles "Dotfiles")

From [Wikipedia](https://en.wikipedia.org/wiki/Unix_shell "wikipedia:Unix shell"):

	A Unix shell is a command-line interpreter or shell that provides a traditional user interface for the Unix operating system and for Unix-like systems. Users direct the operation of the computer by entering commands as text for a command line interpreter to execute or by creating text scripts of one or more such commands.

## List of shells

*   **[Bash](/index.php/Bash "Bash")** — Bash is an sh-compatible shell that incorporates useful features from the Korn shell (ksh) and C shell (csh). It is intended to conform to the IEEE POSIX P1003.2/ISO 9945.2 Shell and Tools standard. It offers functional improvements over sh for both programming and interactive use. In addition, most sh scripts can be run by Bash without modification.

	[https://www.gnu.org/software/bash/](https://www.gnu.org/software/bash/) || [bash](https://www.archlinux.org/packages/?name=bash)

*   **[C shell](https://en.wikipedia.org/wiki/C_shell "wikipedia:C shell")** — Command language interpreter usable both as an interactive login shell and a shell script command processor. It includes a command-line editor, programmable word completion, spelling correction, a history mechanism, job control and a C-like syntax.

	[http://www.tcsh.org](http://www.tcsh.org) || [tcsh](https://www.archlinux.org/packages/?name=tcsh)

*   **[DASH](/index.php/Dash "Dash")** — POSIX-compliant implementation of `/bin/sh` that aims to be as small as possible. It does this without sacrificing speed where possible. In fact, it is significantly faster than Bash (the GNU Bourne-Again SHell) for most tasks.

	[http://gondor.apana.org.au/~herbert/dash/](http://gondor.apana.org.au/~herbert/dash/) || [dash](https://www.archlinux.org/packages/?name=dash)

*   **[fish](/index.php/Fish "Fish")** — Smart and user-friendly command line shell. Fish performs full-color command line syntax highlighting, as well as highlighting and completion for commands and their arguments, file existence, and history. It supports complete-as-you-type for history and commands. Fish is able to parse the system's man pages in order to determine valid arguments for commands, allowing it to highlight and complete commands. Easy last-command revision can be done using Alt-Up. The fish daemon (fishd) facilitates synchronized history across all instances of fish, as well as universal and persistent environment variables.

	[http://fishshell.com/](http://fishshell.com/) || [fish](https://www.archlinux.org/packages/?name=fish)

*   **[Korn shell](/index.php/Korn_shell "Korn shell")** — The KornShell language is a complete, powerful, high-level programming language for writing applications, often more easily and quickly than with other high-level languages. This makes it especially suitable for prototyping. ksh has the best features of the Bourne shell and the C shell, plus many new features of its own. Thus ksh can do much to enhance your productivity and the quality of your work, both in interacting with the system, and in programming. ksh programs are easier to write, and are more concise and readable than programs written in a lower level language such as C.

	[http://www.kornshell.com](http://www.kornshell.com) || See [article](/index.php/Ksh#Installation "Ksh")

*   **[Nash](/index.php/Nash "Nash")** — Nash is a system shell, inspired by plan9 rc, that makes it easy to create reliable and safe scripts taking advantages of operating systems namespaces (on linux and plan9) in an idiomatic way.

	[https://github.com/NeowayLabs/nash](https://github.com/NeowayLabs/nash) || [nash-git](https://aur.archlinux.org/packages/nash-git/)

*   **Oh** — Unix shell written in Go. It is similar in spirit but different in detail from other Unix shells. Oh extends the shell's programming language features without sacrificing the shell's interactive features.

	[https://github.com/michaelmacinnis/oh](https://github.com/michaelmacinnis/oh) || [oh-git](https://aur.archlinux.org/packages/oh-git/)

*   **[Powershell](https://en.wikipedia.org/wiki/Powershell "wikipedia:Powershell")** — PowerShell is an object-oriented programming language and interactive command line shell, originally written for and exclusive to Windows. Later on, it was open sourced and ported to Mac OS X and Linux.

	[https://github.com/PowerShell/PowerShell](https://github.com/PowerShell/PowerShell) || [powershell-git](https://aur.archlinux.org/packages/powershell-git/)

*   **[rc](https://en.wikipedia.org/wiki/rc "wikipedia:rc")** — Command interpreter for Plan 9 that provides similar facilities to UNIX’s Bourne shell, with some small additions and less idiosyncratic syntax.

	[http://plan9.bell-labs.com/sys/doc/rc.html](http://plan9.bell-labs.com/sys/doc/rc.html) || [9base-git](https://aur.archlinux.org/packages/9base-git/)

*   **xonsh** — A retrocompatible shell based on the python interpreter.

	[http://xon.sh/](http://xon.sh/) || [xonsh](https://aur.archlinux.org/packages/xonsh/)

*   **[Zsh](/index.php/Zsh "Zsh")** — Shell designed for interactive use, although it is also a powerful scripting language. Many of the useful features of Bash, ksh, and tcsh were incorporated into Zsh; many original features were added. The [introductory document](http://zsh.sourceforge.net/Intro/intro_toc.html) details some of the unique features of Zsh.

	[http://www.zsh.org/](http://www.zsh.org/) || [zsh](https://www.archlinux.org/packages/?name=zsh)

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

## See also

*   [Evolution of shells in Linux](http://www.ibm.com/developerworks/linux/library/l-linux-shells/index.html) on the IBM developerWorks
*   [Goosh](http://www.goosh.org/) is the unofficial Google shell, which implements a shell interface over the commonly used Google search interface.
*   [>_ .bashrc PS1 generator](http://bashrcgenerator.com/) generate your .bashrc/PS1 bash prompt easily with a drag and drop interface.
*   [terminal.sexy](https://terminal.sexy/) — Terminal Color Scheme Designer
*   [Hyperpolyglot](http://hyperpolyglot.org/unix-shells) — Hyperpolyglot entry about shell