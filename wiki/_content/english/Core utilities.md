This article deals with so-called *core* utilities on a GNU/Linux system, such as *less*, *ls*, and *grep*. The scope of this article includes, but is not limited to, those utilities included with the GNU [coreutils](https://www.archlinux.org/packages/?name=coreutils) package. What follows are various tips and tricks and other helpful information related to these utilities.

## Contents

*   [1 Basic commands](#Basic_commands)
*   [2 cat](#cat)
*   [3 dd](#dd)
    *   [3.1 dd spin-offs](#dd_spin-offs)
*   [4 grep](#grep)
    *   [4.1 Colored output](#Colored_output)
    *   [4.2 Standard error](#Standard_error)
*   [5 find](#find)
*   [6 locate](#locate)
    *   [6.1 Keeping the database up-to-date](#Keeping_the_database_up-to-date)
*   [7 iconv](#iconv)
    *   [7.1 Convert a file in place](#Convert_a_file_in_place)
*   [8 ip](#ip)
*   [9 less](#less)
    *   [9.1 Colored output through environment variables](#Colored_output_through_environment_variables)
    *   [9.2 Colored output through wrappers](#Colored_output_through_wrappers)
    *   [9.3 Vim as alternative pager](#Vim_as_alternative_pager)
    *   [9.4 Colored output when reading from stdin](#Colored_output_when_reading_from_stdin)
*   [10 ls](#ls)
    *   [10.1 Long format](#Long_format)
    *   [10.2 Colored output](#Colored_output_2)
    *   [10.3 File names containing spaces enclosed in quotes](#File_names_containing_spaces_enclosed_in_quotes)
*   [11 mkdir](#mkdir)
*   [12 mv](#mv)
*   [13 od](#od)
*   [14 pv](#pv)
*   [15 rm](#rm)
*   [16 sed](#sed)
*   [17 seq](#seq)
*   [18 which](#which)
*   [19 wipefs](#wipefs)
*   [20 See also](#See_also)

## Basic commands

The following table lists basic shell commands every Linux user should be familiar with. Commands in **bold** are part of the shell, others are separate programs called from the shell. See the below sections and *Related articles* for details.

| Command | Description | Example |
| man | Show manual page for a command | man ed |
| **cd** | Change directory | cd /etc/pacman.d |
| mkdir | Create a directory | mkdir ~/newfolder |
| rmdir | Remove empty directory | rmdir ~/emptyfolder |
| rm | Remove a file | rm ~/file.txt |
| rm -r | Remove directory and contents | rm -r ~/.cache |
| ls | List files | ls *.mkv |
| ls -a | List hidden files | ls -a /home/archie |
| ls -al | List hidden files and file properties |
| mv | Move a file | mv ~/compressed.zip ~/archive/compressed2.zip |
| cp | Copy a file | cp ~/.bashrc ~/.bashrc.bak |
| chmod +x | Make a file executable | chmod +x ~/.local/bin/myscript.sh |
| cat | Show file contents | cat /etc/hostname |
| strings | Show printable characters in binary files | strings /usr/bin/free |
| find | Search for a file | find ~ -name myfile |
| mount | Mount a partition | mount /dev/sdc1 /media/usb |
| df -h | Show remaining space on all partitions |
| ps -A | Show all running processes |
| killall | Kill all running instances of a process |
| ss -at | Display a list of open TCP sockets |

## cat

[cat](https://en.wikipedia.org/wiki/cat_(Unix) (*catenate*) is a standard Unix utility that concatenates and lists files.

*   Because *cat* is not a built-in shell, on many occasions you may find it more convenient to use a [redirection](https://en.wikipedia.org/wiki/Redirection_(computing) "wikipedia:Redirection (computing)"), for example in scripts, or if you care a lot about performance. In fact `< *file*` does the same as `cat *file*`.

*   *cat* is able to work with multiple lines, although this is sometimes regarded as bad practice:

```
$ cat << EOF >> *path/file*
*first line*
...
*last line*
EOF

```

	A better alternative is the *echo* command:

```
$ echo "\
*first line*
...
*last line*" \
>> *path/file*

```

*   If you need to list file lines in reverse order, there is a utility called [tac](https://en.wikipedia.org/wiki/tac_(Unix) (*cat* reversed).

## dd

[dd](https://en.wikipedia.org/wiki/dd_(Unix) is a command on Unix and Unix-like operating systems whose primary purpose is to convert and copy a file.

By default, *dd* outputs nothing until the task has finished. To monitor the progress of the operation, add the `status=progress` option to the command. See the [manual](http://www.gnu.org/software/coreutils/manual/html_node/dd-invocation.html#dd-invocation) for more information.

**Note:** *cp* does the same as *dd* without any operands but is not designed for more versatile disk wiping procedures.

### dd spin-offs

Other *dd*-like programs feature periodical status output, e.g. a simple progress bar.

	dcfldd 

	[dcfldd](https://www.archlinux.org/packages/?name=dcfldd) is an enhanced version of dd with features useful for forensics and security. It accepts most of dd's parameters and includes status output. The last stable version of dcfldd was released on December 19, 2006.

	ddrescue 

	GNU [ddrescue](https://www.archlinux.org/packages/?name=ddrescue) is a data recovery tool. It is capable of ignoring read errors, which is a useless feature for disk wiping in almost any case. See the [official manual](http://www.gnu.org/software/ddrescue/manual/ddrescue_manual.html) for details.

## grep

[grep](https://en.wikipedia.org/wiki/grep "wikipedia:grep") (from [ed](https://en.wikipedia.org/wiki/ed "wikipedia:ed")'s *g/re/p*, *global/regular expression/print*) is a command line text search utility originally written for Unix. The *grep* command searches files or standard input globally for lines matching a given regular expression, and prints them to the program's standard output.

*   Remember that *grep* handles files, so a construct like `cat *file* | grep *pattern*` is replaceable with `grep *pattern* *file*`

*   *grep* alternatives optimized for VCS source code do exist, such as [the_silver_searcher](https://www.archlinux.org/packages/?name=the_silver_searcher) and [ack](https://www.archlinux.org/packages/?name=ack).

### Colored output

`grep`'s color output can be helpful for learning [regexp](https://en.wikipedia.org/wiki/regexp "wikipedia:regexp") and additional `grep` functionality.

To enable *grep* coloring write the following entry to the shell configuration file (e.g. if using [Bash](/index.php/Bash "Bash")):

 `~/.bashrc`  `alias grep='grep --color=auto'` 

To include file line numbers in the output, add the option `-n` to the line.

The environment variable `GREP_COLOR` can be used to define the default highlight color (the default is red). To change the color find the [ANSI escape sequence](http://www.tldp.org/HOWTO/Bash-Prompt-HOWTO/x329.html) for the color liked and add it:

```
export GREP_COLOR="1;32"

```

`GREP_COLORS` may be used to define specific searches.

### Standard error

Some commands send their output to standard error, and grep has no apparent effect. In this case, redirect standard error next to standard out:

```
$ *command* 2>&1 | grep *args*

```

or Bash 4 shorthand:

```
$ *command* |& grep *args*

```

See also [I/O Redirection](http://www.tldp.org/LDP/abs/html/io-redirection.html).

## find

*find* is part of the [findutils](https://www.archlinux.org/packages/?name=findutils) package, which belongs to the [base](https://www.archlinux.org/groups/x86_64/base/) package group.

One would probably expect a *find* command to take as argument a file name and search the filesystem for files matching that name. For a program that does exactly that see [#locate](#locate) below.

Instead, find takes a set of directories and matches each file under them against a set of expressions. This design allows for some very powerful "one-liners" that would not be possible using the "intuitive" design described above. See [UsingFind](http://mywiki.wooledge.org/UsingFind) for usage details.

## locate

`locate` is a common Unix tool for quickly finding files by name. It offers speed improvements over the [find](https://en.wikipedia.org/wiki/Find "wikipedia:Find") tool by searching a pre-constructed database file, rather than the filesystem directly. The downside of this approach is that changes made since the construction of the database file cannot be detected by `locate`. This problem is minimised by regular, typically scheduled use of the `updatedb` command, which (as the name suggests) updates the database.

**Note:** Although in other distros `locate` and `updatedb` are in the [findutils](https://www.archlinux.org/packages/?name=findutils) package, they are no longer present in Arch's package. To use it, install the [mlocate](https://www.archlinux.org/packages/?name=mlocate) package. mlocate is a newer implementation of the tool, but is used in exactly the same way.

Before `locate` can be used, the database will need to be created. To do this, simply run `updatedb` as root.

See also [How locate works and rewrite it in one minute](http://jvns.ca/blog/2015/03/05/how-the-locate-command-works-and-lets-rewrite-it-in-one-minute/)

### Keeping the database up-to-date

When `mlocate` is installed, a script is automatically scheduled to run daily via `systemd`, to update the database. You can also manually run `updatedb` as root at any time.

To save time, the `updatedb` can be (and by default is) configured to ignore certain filesystems and paths by editing `/etc/updatedb.conf`. `man updatedb.conf` will tell you about the semantics of this file. It is worth noting that among the paths ignored in the default configuration (i.e. those in the "PRUNEPATHS" string) are `/media` and `/mnt`, so `locate` may not discover files on external devices.

## iconv

`iconv` converts the encoding of characters from one codeset to another.

The following command will convert the file `foo` from ISO-8859-15 to UTF-8 saving it to `foo.utf`:

```
$ iconv -f ISO-8859-15 -t UTF-8 foo >foo.utf

```

See `man iconv` for more details.

### Convert a file in place

**Tip:** You can use [recode](https://www.archlinux.org/packages/?name=recode) instead of iconv if you do not want to touch the mtime.

Unlike [sed](#sed), *iconv* does not provide an option to convert a file in place. However, `sponge` can be used to handle it, it comes with [moreutils](https://www.archlinux.org/packages/?name=moreutils).

```
$ iconv -f WINDOWS-1251 -t UTF-8 foobar.txt | sponge foobar.txt

```

See `man sponge` for details.

## ip

[ip](https://en.wikipedia.org/wiki/Iproute2 "wikipedia:Iproute2") allows you to show information about network devices, IP addresses, routing tables, and other objects in the Linux [IP](https://en.wikipedia.org/wiki/Internet_Protocol "wikipedia:Internet Protocol") software stack. By appending various commands, you can also manipulate or configure most of these objects.

**Note:** The *ip* utility is provided by the [iproute2](https://www.archlinux.org/packages/?name=iproute2) package, which is included in the [base](https://www.archlinux.org/groups/x86_64/base/) group.

| Object | Purpose | Manual Page Name |
| ip addr | protocol address management | ip-address |
| ip addrlabel | protocol address label management | ip-addrlabel |
| ip l2tp | tunnel Ethernet over IP (L2TPv3) | ip-l2tp |
| ip link | network device configuration | ip-link |
| ip maddr | multicast addresses management | ip-maddress |
| ip monitor | watch for netlink messages | ip-monitor |
| ip mroute | multicast routing cache management | ip-mroute |
| ip mrule | rule in multicast routing policy db |
| ip neigh | neighbour/ARP tables management | ip-neighbour |
| ip netns | process network namespace management | ip-netns |
| ip ntable | neighbour table configuration | ip-ntable |
| ip route | routing table management | ip-route |
| ip rule | routing policy database management | ip-rule |
| ip tcp_metrics | management for TCP Metrics | ip-tcp_metrics |
| ip tunnel | tunnel configuration | ip-tunnel |
| ip tuntap | manage TUN/TAP devices |
| ip xfrm | manage IPsec policies | ip-xfrm |

The `help` command is available for all objects. For example, typing `ip addr help` will show you the command syntax available for the address object. For advanced usage see the [iproute2 documentation](http://www.policyrouting.org/iproute2.doc.html).

The [Network configuration](/index.php/Network_configuration "Network configuration") article shows how the *ip* command is used in practice for various common tasks.

**Note:** You might be familiar with the [ifconfig](https://en.wikipedia.org/wiki/ifconfig "wikipedia:ifconfig") command, which was used in older versions of Linux for interface configuration. It is now deprecated in Arch Linux; you should use *ip* instead.

## less

[less](https://en.wikipedia.org/wiki/less_(Unix) is a terminal pager program used to view the contents of a text file one screen at a time. Whilst similar to other pagers such as [more](https://en.wikipedia.org/wiki/more_(command) and [pg](https://en.wikipedia.org/wiki/pg_(Unix) "wikipedia:pg (Unix)"), *less* offers a more advanced interface and complete [feature-set](http://www.greenwoodsoftware.com/less/faq.html).

See [List of applications#Terminal pagers](/index.php/List_of_applications#Terminal_pagers "List of applications") for alternatives.

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

[Vim](/index.php/Vim "Vim") (*visual editor improved*) has a script to view the content of text files, compressed files, binaries, directories. Add the following line to your shell configuration file to use it as a pager:

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

Alternatively, using [zpty](http://zsh.sourceforge.net/Doc/Release/Zsh-Modules.html#The-zsh_002fzpty-Module) module from [zsh](/index.php/Zsh "Zsh"): [[2]](http://lilydjwg.is-programmer.com/2011/6/29/using-zpty-module-of-zsh.27677.html)

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

## ls

[ls](https://en.wikipedia.org/wiki/ls "wikipedia:ls") (*list*) is a command to list files in Unix and Unix-like operating systems.

See `info ls` or [the online manual](http://www.gnu.org/software/coreutils/manual/html_node/ls-invocation.html#ls-invocation) for more information.

### Long format

The `-l` option displays some metadata, for example:

 `$ ls -l /path/to/directory` 
```
total 128
drwxr-xr-x 2 archie users  4096 Jul  5 21:03 Desktop
drwxr-xr-x 6 archie users  4096 Jul  5 17:37 Documents
drwxr-xr-x 2 archie users  4096 Jul  5 13:45 Downloads
-rw-rw-r-- 1 archie users  5120 Jun 27 08:28 customers.ods
-rw-r--r-- 1 archie users  3339 Jun 27 08:28 todo
-rwxr-xr-x 1 archie users  2048 Jul  6 12:56 myscript.sh

```

The `total` value represents the total disk allocation for the files in the directory, by default in number of blocks.

Below, each file and subdirectory is represented by a line divided into 7 metadata fields, in the following order:

*   type and permissions:
    *   the first character is the entry type, see `info ls -n "What information is listed"` for an explanation of all the possible types; for example:
        *   `-` denotes a normal file;
        *   `d` denotes a directory, i.e. a folder containing other files or folders;
        *   `p` denotes a named pipe (aka FIFO);
        *   `l` denotes a symbolic link;
    *   the remaining characters are the entry's [permissions](/index.php/Permissions "Permissions");
*   number of [hard links](https://en.wikipedia.org/wiki/Hard_link "wikipedia:Hard link") for the entity; files will have at least 1, i.e. the showed reference itself; folders will have at least 2: the showed reference, the self-referencing `.` entry, and then a `..` entry in each of its subfolders;
*   owner [user](/index.php/User "User") name;
*   [group](/index.php/Group "Group") name;
*   size;
*   last modification timestamp;
*   entity name.

### Colored output

Colored output can be enabled with a simple alias. File `~/.bashrc` should already have the following entry copied from `/etc/skel/.bashrc`:

```
alias ls='ls --color=auto'

```

The next step will further enhance the colored *ls* output; for example, broken (orphan) symlinks will start showing in a red hue. Add the following to your shell configuration file:

```
eval $(dircolors -b)

```

### File names containing spaces enclosed in quotes

By default, file and directory names that contain spaces are displayed surrounded by single quotes. To change this behavior use the `-N` or `--quoting-style=literal` options. Alternatively, set the `QUOTING_STYLE` [environment variable](/index.php/Environment_variable "Environment variable") to `literal`. [[3]](https://unix.stackexchange.com/questions/258679/why-is-ls-suddenly-surrounding-items-with-spaces-in-single-quotes)

## mkdir

[mkdir](https://en.wikipedia.org/wiki/mkdir "wikipedia:mkdir") (*make directory*) is a command to create directories.

*   To create a directory and its whole hierarchy, the `-p` switch is used, otherwise an error is printed. As users are supposed to know what they want, `-p` switch may be used as a default:

	 `alias mkdir='mkdir -p -v'` 

	The `-v` switch make it verbose.

*   Changing mode of a just created directory using *chmod* is not necessary as the `-m` option lets you define the access permissions.

**Tip:** If you just want a temporary directory, a better alternative may be [mktemp](https://en.wikipedia.org/wiki/Temporary_file "wikipedia:Temporary file") (*make temporary*): `mktemp -p`.

## mv

[mv](https://en.wikipedia.org/wiki/mv "wikipedia:mv") (*move*) is a command to move and rename files and directories.

*   It can be very dangerous so it is prudent to limit its scope:

	 `alias mv=' timeout 8 mv -iv'` 

	This alias suspends *mv* after eight seconds, asks confirmation to delete three or more files, lists the operations in progress and does not store itself in the shell history file if the shell is configured to ignore space starting commands.

## od

The [od](https://en.wikipedia.org/wiki/od_(Unix) (*o*ctal *d*ump) command is useful for visualizing data that is not in a human-readable format, like the executable code of a program, or the contents of an unformatted device. See the [manual](http://www.gnu.org/software/coreutils/manual/html_node/od-invocation.html#od-invocation) for more information.

## pv

You can use [pv](https://www.archlinux.org/packages/?name=pv) (*pipe viewer*) to monitor the progress of data through a pipeline, for example:

```
# dd if=*/source/filestream* | pv -*monitor_options* -s *size_of_file* | dd of=*/destination/filestream*

```

In most cases `pv` functions as a drop-in replacement for `cat`, however there are undocumented differences. For example, under both Zsh and Bash, the following command hangs forever:

```
# cat <(pv /usr/share/dict/words)

```

Use of *strace* shows that `pv` is stopped with `SIGTTOU`.

## rm

[rm](https://en.wikipedia.org/wiki/rm_(Unix) (*remove*) is a command to delete files and directories.

*   It can be very dangerous, so it is prudent to limit its scope:

	 `alias rm=' timeout 3 rm -Iv --one-file-system'` 

	This alias suspends *rm* after three seconds, asks confirmation to delete three or more files, lists the operations in progress, does not involve more than one file systems and does not store itself in the shell history file if the shell is configured to ignore space starting commands. Substitute `-I` with `-i` if you prefer to confirm even for one file.

	Zsh users may want to put `noglob` before `timeout` to avoid implicit expansions.

*   To remove directories known to be empty, use *rmdir* as it fails in case of files inside the target.

## sed

[sed](https://en.wikipedia.org/wiki/sed "wikipedia:sed") (*stream editor*) is a Unix utility that parses and transforms text.

Here is a handy [list](http://sed.sourceforge.net/sed1line.txt) of *sed* one-liners examples.

**Tip:** More powerful alternatives are [AWK](https://en.wikipedia.org/wiki/AWK "wikipedia:AWK") and even [Perl](https://en.wikipedia.org/wiki/Perl "wikipedia:Perl") language.

## seq

**seq** (*sequence*) is a utility for generating a sequence of numbers. Shell built-in alternatives are available, so it is good practice to use them as explained on [Wikipedia](https://en.wikipedia.org/wiki/Seq_(Unix) "wikipedia:Seq (Unix)").

## which

The [which](https://en.wikipedia.org/wiki/Which_(Unix) command is useful to determine the path to an executable, for example:

```
# journalctl $(which sshd)

```

## wipefs

**wipefs** can list or erase [file system](/index.php/File_system "File system"), [RAID](/index.php/RAID "RAID") or [partition-table](/index.php/Partition "Partition") signatures (magic strings) from the specified device. It does not erase the file systems themselves nor any other data from the device.

See wipefs(8) for more information.

For example, to erase all signatures from the device `/dev/sdb` and create a signature backup `~/wipefs-sdb-*offset*.bak` file for each signature:

```
# wipefs --all --backup /dev/sdb

```

## See also

*   [A sampling of coreutils](http://www.reddit.com/r/commandline/comments/19garq/a_sampling_of_coreutils_120/) [, part 2](http://www.reddit.com/r/commandline/comments/19ge6v/a_sampling_of_coreutils_2040/) [, part 3](http://www.reddit.com/r/commandline/comments/19j1w3/a_sampling_of_coreutils_4060/) - Overview of commands in coreutils
*   [GNU Coreutils online documentation](http://www.gnu.org/software/coreutils/manual/coreutils.html)
*   [Learn the DD command](http://www.linuxquestions.org/questions/linux-newbie-8/learn-the-dd-command-362506/)