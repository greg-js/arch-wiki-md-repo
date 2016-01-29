# Core utilities

Related articles

*   [Bash](/index.php/Bash "Bash")
*   [Zsh](/index.php/Zsh "Zsh")
*   [General recommendations](/index.php/General_recommendations "General recommendations")
*   [GNU Project](/index.php/GNU_Project "GNU Project")
*   [sudo](/index.php/Sudo "Sudo")
*   [cron](/index.php/Cron "Cron")
*   [man page](/index.php/Man_page "Man page")
*   [Securely wipe disk#shred](/index.php/Securely_wipe_disk#shred "Securely wipe disk")
*   [File permissions and attributes](/index.php/File_permissions_and_attributes "File permissions and attributes")

This article deals with so-called _core_ utilities on a GNU/Linux system, such as _less_, _ls_, and _grep_. The scope of this article includes, but is not limited to, those utilities included with the GNU [coreutils](https://www.archlinux.org/packages/?name=coreutils) package. What follows are various tips and tricks and other helpful information related to these utilities.

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
*   [11 mkdir](#mkdir)
*   [12 mv](#mv)
*   [13 od](#od)
*   [14 pv](#pv)
*   [15 rm](#rm)
*   [16 sed](#sed)
*   [17 seq](#seq)
*   [18 which](#which)
*   [19 See also](#See_also)

## Basic commands

The following table lists basic shell commands every Linux user should be familiar with. Commands in **bold** are part of the shell, others are separate programs called from the shell. See the below sections and _Related articles_ for details.

| Command | Description | Example |
| man | Show manual page for a command | man ed |
| **cd** | Change directory | cd /etc/pacman.d |
| mkdir | Create a directory | mkdir ~/newfolder |
| rmdir | Remove empty directory | rmdir ~/emptyfolder |
| rm | Remove a file | rm ~/file.txt |
| rm -r | Remove directory and contents | rm -r ~/.cache |
| ls | List files | ls *.avi |
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

[cat](https://en.wikipedia.org/wiki/cat_(Unix) "wikipedia:cat (Unix)") (_catenate_) is a standard Unix utility that concatenates and lists files.

*   Because _cat_ is not a built-in shell, on many occasions you may find it more convenient to use a [redirection](https://en.wikipedia.org/wiki/Redirection_(computing) "wikipedia:Redirection (computing)"), for example in scripts, or if you care a lot about performance. In fact `< _file_` does the same as `cat _file_`.

*   _cat_ is able to work with multiple lines, although this is sometimes regarded as bad practice:

```
$ cat << EOF >> _path/file_
_first line_
...
_last line_
EOF

```

NaN

```
$ echo "\
_first line_
...
_last line_" \
>> _path/file_

```

*   If you need to list file lines in reverse order, there is a utility called [tac](https://en.wikipedia.org/wiki/tac_(Unix) "wikipedia:tac (Unix)") (_cat_ reversed).

## dd

[dd](https://en.wikipedia.org/wiki/dd_(Unix) "wikipedia:dd (Unix)") is a command on Unix and Unix-like operating systems whose primary purpose is to convert and copy a file.

By default, _dd_ outputs nothing until the task has finished. To monitor the progress of the operation, add the `status=progress` option to the command. See the [manual](http://www.gnu.org/software/coreutils/manual/html_node/dd-invocation.html#dd-invocation) for more information.

**Note:** _cp_ does the same as _dd_ without any operands but is not designed for more versatile disk wiping procedures.

### dd spin-offs

[![Tango-go-next.png](/images/f/f0/Tango-go-next.png)](/index.php/File:Tango-go-next.png)

[![Tango-go-next.png](/images/f/f0/Tango-go-next.png)](/index.php/File:Tango-go-next.png)

**This article or section is a candidate for moving to [Disk cloning](/index.php/Disk_cloning "Disk cloning").**

**Notes:** See [Talk:Disk_cloning#ddrescue](/index.php/Talk:Disk_cloning#ddrescue "Talk:Disk cloning"). (Discuss in [Talk:Core utilities#](https://wiki.archlinux.org/index.php/Talk:Core_utilities))

Other _dd_-like programs feature periodical status output, e.g. a simple progress bar.

NaN

NaN

## grep

[grep](https://en.wikipedia.org/wiki/grep "wikipedia:grep") (from [ed](https://en.wikipedia.org/wiki/ed "wikipedia:ed")'s _g/re/p_, _global/regular expression/print_) is a command line text search utility originally written for Unix. The _grep_ command searches files or standard input globally for lines matching a given regular expression, and prints them to the program's standard output.

*   Remember that _grep_ handles files, so a construct like `cat _file_ | grep _pattern_` is replaceable with `grep _pattern_ _file_`

*   _grep_ alternatives optimized for VCS source code do exist, such as [the_silver_searcher](https://www.archlinux.org/packages/?name=the_silver_searcher) and [ack](https://www.archlinux.org/packages/?name=ack).

### Colored output

`grep`'s color output can be helpful for learning [regexp](https://en.wikipedia.org/wiki/regexp "wikipedia:regexp") and additional `grep` functionality.

To enable _grep_ coloring write the following entry to the shell configuration file (e.g. if using [Bash](/index.php/Bash "Bash")):

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
$ _command_ 2>&1 | grep _args_

```

or Bash 4 shorthand:

```
$ _command_ |& grep _args_

```

See also [I/O Redirection](http://www.tldp.org/LDP/abs/html/io-redirection.html).

## find

_find_ is part of the [findutils](https://www.archlinux.org/packages/?name=findutils) package, which belongs to the [base](https://www.archlinux.org/groups/x86_64/base/) package group.

One would probably expect a _find_ command to take as argument a file name and search the filesystem for files matching that name. For a program that does exactly that see [#locate](#locate) below.

Instead, find takes a set of directories and matches each file under them against a set of expressions. This design allows for some very powerful "one-liners" that would not be possible using the "intuitive" design described above. See [UsingFind](http://mywiki.wooledge.org/UsingFind) for usage details.

## locate

`locate` is a common Unix tool for quickly finding files by name. It offers speed improvements over the [find](http://en.wikipedia.org/wiki/Find) tool by searching a pre-constructed database file, rather than the filesystem directly. The downside of this approach is that changes made since the construction of the database file cannot be detected by `locate`. This problem is minimised by regular, typically scheduled use of the `updatedb` command, which (as the name suggests) updates the database.

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

Unlike [sed](#sed), _iconv_ does not provide an option to convert a file in place. However, `sponge` can be used to handle it, it comes with [moreutils](https://www.archlinux.org/packages/?name=moreutils).

```
$ iconv -f WINDOWS-1251 -t UTF-8 foobar.txt | sponge foobar.txt

```

See `man sponge` for details.

## ip

[ip](https://en.wikipedia.org/wiki/Iproute2 "wikipedia:Iproute2") allows you to show information about network devices, IP addresses, routing tables, and other objects in the Linux [IP](https://en.wikipedia.org/wiki/Internet_Protocol "wikipedia:Internet Protocol") software stack. By appending various commands, you can also manipulate or configure most of these objects.

**Note:** The _ip_ utility is provided by the [iproute2](https://www.archlinux.org/packages/?name=iproute2) package, which is included in the [base](https://www.archlinux.org/groups/x86_64/base/) group.

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

The [Network configuration](/index.php/Network_configuration "Network configuration") article shows how the _ip_ command is used in practice for various common tasks.

**Note:** You might be familiar with the [ifconfig](https://en.wikipedia.org/wiki/ifconfig "wikipedia:ifconfig") command, which was used in older versions of Linux for interface configuration. It is now deprecated in Arch Linux; you should use _ip_ instead.

## less

[![Tango-mail-mark-junk.png](/images/e/e7/Tango-mail-mark-junk.png)](/index.php/File:Tango-mail-mark-junk.png)

[![Tango-mail-mark-junk.png](/images/e/e7/Tango-mail-mark-junk.png)](/index.php/File:Tango-mail-mark-junk.png)

**This article or section needs language, wiki syntax or style improvements.**

**Reason:** less is a complex beast, and this section should explain some of the basic less commands - not go on a bunch of tangents like colored output (Discuss in [Talk:Core utilities#](https://wiki.archlinux.org/index.php/Talk:Core_utilities))

[less](https://en.wikipedia.org/wiki/less_(Unix) "wikipedia:less (Unix)") is a terminal pager program used to view the contents of a text file one screen at a time. Whilst similar to other pagers such as [more](https://en.wikipedia.org/wiki/more_(command) "wikipedia:more (command)") and [pg](https://en.wikipedia.org/wiki/pg_(Unix) "wikipedia:pg (Unix)"), _less_ offers a more advanced interface and complete [feature-set](http://www.greenwoodsoftware.com/less/faq.html).

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

**Note:** The `LESS_TERMCAL__xx_` variables is currently undocumented in less(1), for a detailed explanation on these sequences, see this [anwser](http://unix.stackexchange.com/questions/108699/documentation-on-less-termcap-variables/108840#108840).

### Colored output through wrappers

You can enable code syntax coloring in _less_. First, [install](/index.php/Install "Install") [source-highlight](https://www.archlinux.org/packages/?name=source-highlight), then add these lines to your shell configuration file:

 `~/.bashrc` 

```
export LESSOPEN="| /usr/bin/source-highlight-esc.sh %s"
export LESS='-R '

```

Frequent users of the command line interface might want to install [lesspipe](https://www.archlinux.org/packages/?name=lesspipe).

Users may now list the compressed files inside of an archive using their pager:

 `$ less _compressed_file_.tar.gz` 

```
==> use tar_file:contained_file to view a file in the archive
-rw------- _username_/_group_  695 2008-01-04 19:24 _compressed_file_/_content1_
-rw------- _username_/_group_   43 2007-11-07 11:17 _compressed_file_/_content2_
_compressed_file_.tar.gz (END)
```

_lesspipe_ also grants _less_ the ability of interfacing with files other than archives, serving as an alternative for the specific command associated for that file-type (such as viewing HTML via [python-html2text](https://www.archlinux.org/packages/?name=python-html2text)).

Re-login after installing _lesspipe_ in order to activate it, or source `/etc/profile.d/lesspipe.sh`.

### Vim as alternative pager

[Vim](/index.php/Vim "Vim") (_visual editor improved_) has a script to view the content of text files, compressed files, binaries, directories. Add the following line to your shell configuration file to use it as a pager:

 `~/.bashrc`  `alias less='/usr/share/vim/vim74/macros/less.sh'` 

There is also an alternative to _less.sh_ macro, which may work as the `PAGER` environment variable. Install [vimpager](https://www.archlinux.org/packages/?name=vimpager) and add the following to your shell configuration file:

 `~/.bashrc` 

```
export PAGER='vimpager'
alias less=$PAGER
```

Now programs that use the `PAGER` environment variable, like [git](/index.php/Git "Git"), will use _vim_ as pager.

### Colored output when reading from stdin

**Note:** It is recommended to add [#Colored output through environment variables](#Colored_output_through_environment_variables) to your `~/.bashrc` or `~/.zshrc`, as the below is based on `export LESS=R`

When you run a command and pipe its [standard output](https://en.wikipedia.org/wiki/Standard_output "wikipedia:Standard output") (_stdout_) to _less_ for a paged view (e.g. `pacman -Qe | less`), you may find that the output is no longer colored. This is usually because the program tries to detect if its _stdout_ is an interactive terminal, in which case it prints colored text, and otherwise prints uncolored text. This is good behaviour when you want to redirect _stdout_ to a file, e.g. `pacman -Qe > pkglst-backup.txt`, but less suited when you want to view output in `less`.

Some programs provide an option to disable the interactive tty detection:

```
# dmesg --color=always | less

```

In case that the program does not provide any similar option, it is possible to trick the program into thinking its _stdout_ is an interactive terminal with the following utilities:

*   **stdoutisatty** — A small program which catches the `isatty` function call.

NaN

*   **unbuffer** — A tclsh script comes with expect, it invokes desired program within a pty.

NaN

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
$ ptyless _program_

```

To pipe it to other pager (less in this example):

```
$ pty _program_ | less

```

## ls

[ls](https://en.wikipedia.org/wiki/ls "wikipedia:ls") (_list_) is a command to list files in Unix and Unix-like operating systems.

*   _ls_ can list [file permissions](/index.php/File_permissions_and_attributes#Viewing_permissions "File permissions and attributes").

*   Colored output can be enabled with a simple alias. File `~/.bashrc` should already have the following entry copied from `/etc/skel/.bashrc`:

NaN

The next step will further enhance the colored _ls_ output; for example, broken (orphan) symlinks will start showing in a red hue. Add the following to your shell configuration file:

NaN

## mkdir

[mkdir](https://en.wikipedia.org/wiki/mkdir "wikipedia:mkdir") (_make directory_) is a command to create directories.

*   To create a directory and its whole hierarchy, the `-p` switch is used, otherwise an error is printed. As users are supposed to know what they want, `-p` switch may be used as a default:

NaN

*   Changing mode of a just created directory using _chmod_ is not necessary as the `-m` option lets you define the access permissions.

**Tip:** If you just want a temporary directory, a better alternative may be [mktemp](https://en.wikipedia.org/wiki/Temporary_file "wikipedia:Temporary file") (_make temporary_): `mktemp -p`.

## mv

[mv](https://en.wikipedia.org/wiki/mv "wikipedia:mv") (_move_) is a command to move and rename files and directories.

*   It can be very dangerous so it is prudent to limit its scope:

NaN

## od

The [od](https://en.wikipedia.org/wiki/od_(Unix) "wikipedia:od (Unix)") (_o_ctal _d_ump) command is useful for visualizing data that is not in a human-readable format, like the executable code of a program, or the contents of an unformatted device. See the [manual](http://www.gnu.org/software/coreutils/manual/html_node/od-invocation.html#od-invocation) for more information.

## pv

You can use [pv](https://www.archlinux.org/packages/?name=pv) (_pipe viewer_) to monitor the progress of data through a pipeline, for example:

```
# dd if=_/source/filestream_ | pv -_monitor_options_ -s _size_of_file_ | dd of=_/destination/filestream_

```

In most cases `pv` functions as a drop-in replacement for `cat`, however there are undocumented differences. For example, under both Zsh and Bash, the following command hangs forever:

```
# cat <(pv /usr/share/dict/words)

```

Use of _strace_ shows that `pv` is stopped with `SIGTTOU`.

## rm

[rm](https://en.wikipedia.org/wiki/rm_(Unix) "wikipedia:rm (Unix)") (_remove_) is a command to delete files and directories.

*   It can be very dangerous, so it is prudent to limit its scope:

NaN

*   To remove directories known to be empty, use _rmdir_ as it fails in case of files inside the target.

## sed

[sed](https://en.wikipedia.org/wiki/sed "wikipedia:sed") (_stream editor_) is a Unix utility that parses and transforms text.

Here is a handy [list](http://sed.sourceforge.net/sed1line.txt) of _sed_ one-liners examples.

**Tip:** More powerful alternatives are [AWK](https://en.wikipedia.org/wiki/AWK "wikipedia:AWK") and even [Perl](https://en.wikipedia.org/wiki/Perl "wikipedia:Perl") language.

## seq

**seq** (_sequence_) is a utility for generating a sequence of numbers. Shell built-in alternatives are available, so it is good practice to use them as explained on [Wikipedia](https://en.wikipedia.org/wiki/Seq_(Unix) "wikipedia:Seq (Unix)").

## which

The [which](https://en.wikipedia.org/wiki/Which_(Unix) "wikipedia:Which (Unix)") command is useful to determine the path to an executable, for example:

```
# journalctl $(which sshd)

```

## See also

*   [A sampling of coreutils](http://www.reddit.com/r/commandline/comments/19garq/a_sampling_of_coreutils_120/) [, part 2](http://www.reddit.com/r/commandline/comments/19ge6v/a_sampling_of_coreutils_2040/) [, part 3](http://www.reddit.com/r/commandline/comments/19j1w3/a_sampling_of_coreutils_4060/) - Overview of commands in coreutils
*   [GNU Coreutils Manpage](http://www.gnu.org/software/coreutils/manual/coreutils.html)
*   [Learn the DD command](http://www.linuxquestions.org/questions/linux-newbie-8/learn-the-dd-command-362506/)

Retrieved from "[https://wiki.archlinux.org/index.php?title=Core_utilities&oldid=416598](https://wiki.archlinux.org/index.php?title=Core_utilities&oldid=416598)"