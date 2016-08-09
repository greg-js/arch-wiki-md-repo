## Contents

*   [1 less](#less)
    *   [1.1 Colored output through environment variables](#Colored_output_through_environment_variables)
    *   [1.2 Colored output through wrappers](#Colored_output_through_wrappers)
    *   [1.3 Vim as alternative pager](#Vim_as_alternative_pager)
    *   [1.4 Colored output when reading from stdin](#Colored_output_when_reading_from_stdin)

## less

### Colored output through environment variables

Add the following lines to your shell configuration file:

 `~/.bashrc` 
```
export LESS=-R
export LESS_TERMCAP_mb=$'\E[1;31m'
export LESS_TERMCAP_md=$'\E[1;36m'
export LESS_TERMCAP_me=$'\E[0m'
export LESS_TERMCAP_se=$'\E[0m'
export LESS_TERMCAP_so=$'\E[01;44;33m'
export LESS_TERMCAP_ue=$'\E[0m'
export LESS_TERMCAP_us=$'\E[1;32m'
```

Change the values ([ANSI escape code](https://en.wikipedia.org/wiki/ANSI_escape_code#Colors "wikipedia:ANSI escape code")) as you like.

**Note:** The `LESS_TERMCAL_*xx*` variables is currently undocumented in less(1), for a detailed explanation on these sequences, see this [answer](http://unix.stackexchange.com/questions/108699/documentation-on-less-termcap-variables/108840#108840).

### Colored output through wrappers

You can enable code syntax coloring in *less*. First, [install](/index.php/Install "Install") [source-highlight](https://www.archlinux.org/packages/?name=source-highlight), then add these lines to your shell configuration file:

 `~/.bashrc` 
```
export LESSOPEN="| /usr/bin/source-highlight-esc.sh %s"
export LESS='-R '

```

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

### Vim as alternative pager

[Vim](/index.php/Vim "Vim") as a script to view the content of text files, compressed files, binaries, directories. Add the following line to your shell configuration file to use it as a pager:

 `~/.bashrc`  `alias less='/usr/share/vim/vim74/macros/less.sh'` 

There is also an alternative to *less.sh* macro, which may work as the `PAGER` environment variable. Install [vimpager](https://www.archlinux.org/packages/?name=vimpager) and add the following to your shell configuration file:

 `~/.bashrc` 
```
export PAGER='vimpager'
alias less=$PAGER
```

Now programs that use the `PAGER` environment variable, like [git](/index.php/Git "Git"), will use *vim* as pager.

### Colored output when reading from stdin

**Note:** It is recommended to add [#Colored output through environment variables](#Colored_output_through_environment_variables) to your `~/.bashrc` or `~/.zshrc`, as the below is based on `export LESS=R`

When you run a command and pipe its [standard output](https://en.wikipedia.org/wiki/Standard_output "wikipedia:Standard output") (*stdout*) to *less* for a paged view (e.g. `pacman -Qe | less`), you may find that the output is no longer colored. This is usually because the program tries to detect if its *stdout* is an interactive terminal, in which case it prints colored text, and otherwise prints uncolored text. This is good behaviour when you want to redirect *stdout* to a file, e.g. `pacman -Qe > pkglst-backup.txt`, but less suited when you want to view output in `less`.

Some programs provide an option to disable the interactive tty detection:

```
# dmesg --color=always | less

```

In case that the program does not provide any similar option, it is possible to trick the program into thinking its *stdout* is an interactive terminal with the following utilities:

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