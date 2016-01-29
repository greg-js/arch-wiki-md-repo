# Command-line shell

From [Wikipedia](https://en.wikipedia.org/wiki/Unix_shell "wikipedia:Unix shell"):

NaN

## List of shells

*   **[Bash](/index.php/Bash "Bash")** — Bash is an sh-compatible shell that incorporates useful features from the Korn shell (ksh) and C shell (csh). It is intended to conform to the IEEE POSIX P1003.2/ISO 9945.2 Shell and Tools standard. It offers functional improvements over sh for both programming and interactive use. In addition, most sh scripts can be run by Bash without modification.

NaN

*   **[C shell](https://en.wikipedia.org/wiki/C_shell "wikipedia:C shell")** — Command language interpreter usable both as an interactive login shell and a shell script command processor. It includes a command-line editor, programmable word completion, spelling correction, a history mechanism, job control and a C-like syntax.

NaN

*   **[DASH](/index.php/Dash "Dash")** — POSIX-compliant implementation of `/bin/sh` that aims to be as small as possible. It does this without sacrificing speed where possible. In fact, it is significantly faster than Bash (the GNU Bourne-Again SHell) for most tasks.

NaN

*   **[fish](/index.php/Fish "Fish")** — Smart and user-friendly command line shell. Fish performs full-color command line syntax highlighting, as well as highlighting and completion for commands and their arguments, file existence, and history. It supports complete-as-you-type for history and commands. Fish is able to parse the system's man pages in order to determine valid arguments for commands, allowing it to highlight and complete commands. Easy last-command revision can be done using Alt-Up. The fish daemon (fishd) facilitates synchronized history across all instances of fish, as well as universal and persistent environment variables.

NaN

*   **[Korn shell](/index.php/Korn_shell "Korn shell")** — The KornShell language is a complete, powerful, high-level programming language for writing applications, often more easily and quickly than with other high-level languages. This makes it especially suitable for prototyping. ksh has the best features of the Bourne shell and the C shell, plus many new features of its own. Thus ksh can do much to enhance your productivity and the quality of your work, both in interacting with the system, and in programming. ksh programs are easier to write, and are more concise and readable than programs written in a lower level language such as C.

NaN

*   **Oh** — Unix shell written in Go. It is similar in spirit but different in detail from other Unix shells. Oh extends the shell's programming language features without sacrificing the shell's interactive features.

NaN

*   **[rc](https://en.wikipedia.org/wiki/rc "wikipedia:rc")** — Command interpreter for Plan 9 that provides similar facilities to UNIX’s Bourne shell, with some small additions and less idiosyncratic syntax.

NaN

*   **[Zsh](/index.php/Zsh "Zsh")** — Shell designed for interactive use, although it is also a powerful scripting language. Many of the useful features of Bash, ksh, and tcsh were incorporated into Zsh; many original features were added. The [introductory document](http://zsh.sourceforge.net/Intro/intro_toc.html) details some of the unique features of Zsh.

NaN

## Changing your default shell

After installing one the above shells, you can execute that shell inside of your current shell, by just running its executable. If you want to be served that shell when you login however, you will need to change your default shell.

To list all installed shells, run:

```
$ chsh -l

```

And to set one as default for your user (make sure you use the full path, as given by `chsh -l`):

```
$ chsh -s _full-path-to-shell_

```

If you now log out and log in again, you will be greeted by the other shell.

## See also

*   [Evolution of shells in Linux](http://www.ibm.com/developerworks/linux/library/l-linux-shells/index.html) on the IBM developerWorks
*   [Goosh](http://www.goosh.org/) is the unofficial Google shell, which implements a shell interface over the commonly used Google search interface.
*   [>_ .bashrc PS1 generator](http://bashrcgenerator.com/) generate your .bashrc/PS1 bash prompt easily with a drag and drop interface.
*   [terminal.sexy](https://terminal.sexy/) — Terminal Color Scheme Designer
*   [Hyperpolyglot](http://hyperpolyglot.org/unix-shells) — Hyperpolyglot entry about shell

Retrieved from "[https://wiki.archlinux.org/index.php?title=Command-line_shell&oldid=416001](https://wiki.archlinux.org/index.php?title=Command-line_shell&oldid=416001)"