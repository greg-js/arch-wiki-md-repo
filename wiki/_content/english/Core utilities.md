Related articles

*   [Command-line shell](/index.php/Command-line_shell "Command-line shell")
*   [General recommendations](/index.php/General_recommendations "General recommendations")
*   [GNU Project](/index.php/GNU_Project "GNU Project")
*   [sudo](/index.php/Sudo "Sudo")
*   [cron](/index.php/Cron "Cron")
*   [man page](/index.php/Man_page "Man page")
*   [Securely wipe disk#shred](/index.php/Securely_wipe_disk#shred "Securely wipe disk")
*   [File permissions and attributes](/index.php/File_permissions_and_attributes "File permissions and attributes")
*   [Color output in console](/index.php/Color_output_in_console "Color output in console")
*   [Archiving and compression tools](/index.php/Archiving_and_compression_tools "Archiving and compression tools")

This article deals with so-called *core* utilities on a GNU/Linux system, such as *less*, *ls*, and *grep*. The scope of this article includes, but is not limited to, those utilities included with the GNU [coreutils](https://www.archlinux.org/packages/?name=coreutils) package. What follows are various tips and tricks and other helpful information related to these utilities.

Most command-line interfaces are documented in [man pages](/index.php/Man_page "Man page"), [GNU](/index.php/GNU "GNU") commands tend to be documented in [info(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/info.1) pages, some [shells](/index.php/Shell "Shell") provide a `help` command for [shell](/index.php/Shell "Shell")-builtin commands. Additionally most commands print their usage when run with the `--help` argument.

## Contents

*   [1 File management](#File_management)
    *   [1.1 ls](#ls)
        *   [1.1.1 Long format](#Long_format)
        *   [1.1.2 File names containing spaces enclosed in quotes](#File_names_containing_spaces_enclosed_in_quotes)
    *   [1.2 cat](#cat)
    *   [1.3 less](#less)
        *   [1.3.1 Vim as alternative pager](#Vim_as_alternative_pager)
    *   [1.4 mkdir](#mkdir)
    *   [1.5 mv](#mv)
    *   [1.6 rm](#rm)
    *   [1.7 chmod](#chmod)
    *   [1.8 chown](#chown)
    *   [1.9 find](#find)
    *   [1.10 locate](#locate)
*   [2 Text streams](#Text_streams)
    *   [2.1 grep](#grep)
    *   [2.2 sed](#sed)
    *   [2.3 awk](#awk)
    *   [2.4 pv](#pv)
*   [3 System administration](#System_administration)
    *   [3.1 sudo](#sudo)
    *   [3.2 which](#which)
    *   [3.3 lsblk](#lsblk)
    *   [3.4 ip](#ip)
    *   [3.5 ss](#ss)
*   [4 Miscellaneous](#Miscellaneous)
    *   [4.1 dd](#dd)
    *   [4.2 iconv](#iconv)
        *   [4.2.1 Convert a file in place](#Convert_a_file_in_place)
    *   [4.3 od](#od)
    *   [4.4 seq](#seq)
    *   [4.5 tar](#tar)
    *   [4.6 wipefs](#wipefs)
*   [5 See also](#See_also)

## File management

| Command | Description | Manual page | Example |
| cd | Change directory (shell built-in command) | [cd(1p)](https://jlk.fjfi.cvut.cz/arch/manpages/man/cd.1p) | cd /etc/pacman.d |
| mkdir | Create a directory | [mkdir(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/mkdir.1) | mkdir ~/newfolder |
| rmdir | Remove empty directory | [rmdir(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/rmdir.1) | rmdir ~/emptyfolder |
| rm | Remove a file | [rm(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/rm.1) | rm ~/file.txt |
| rm -r | Remove directory and contents | rm -r ~/.cache |
| ls | List files | [ls(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/ls.1) | ls *.mkv |
| ls -a | List hidden files | ls -a /home/archie |
| ls -al | List hidden files and file properties |
| mv | Move a file | [mv(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/mv.1) | mv ~/compressed.zip ~/archive/compressed2.zip |
| cp | Copy a file | [cp(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/cp.1) | cp ~/.bashrc ~/.bashrc.bak |
| chmod +x | Make a file [executable](/index.php/Executable "Executable") | [chmod(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/chmod.1) | chmod +x ~/.local/bin/myscript.sh |
| cat | Show file contents | [cat(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/cat.1) | cat /etc/hostname |
| find | Search for a file | [find(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/find.1) | find ~ -name myfile |

### ls

[ls](https://en.wikipedia.org/wiki/ls "wikipedia:ls") lists directory contents.

See `info ls` or [the online manual](https://www.gnu.org/software/coreutils/manual/html_node/ls-invocation.html#ls-invocation) for more information.

[exa](https://the.exa.website) is a modern, and more user friendly alternative to `ls` and `tree`, that has more features, such as displaying [Git](/index.php/Git "Git") modifications along with filenames, colouring differently each columnn in `--long` mode, or displaying `--long` mode metadata along with a `tree` view. [exa](https://www.archlinux.org/packages/?name=exa)

#### Long format

The `-l` option displays some metadata, for example:

 `$ ls -l */path/to/directory*` 
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

#### File names containing spaces enclosed in quotes

By default, file and directory names that contain spaces are displayed surrounded by single quotes. To change this behavior use the `-N` or `--quoting-style=literal` options. Alternatively, set the `QUOTING_STYLE` [environment variable](/index.php/Environment_variable "Environment variable") to `literal`. [[1]](https://unix.stackexchange.com/questions/258679/why-is-ls-suddenly-surrounding-items-with-spaces-in-single-quotes)

### cat

[cat](https://en.wikipedia.org/wiki/cat_(Unix) is a standard Unix utility that concatenates files to standard output.

*   Because *cat* is not built into the shell, on many occasions you may find it more convenient to use a [redirection](https://en.wikipedia.org/wiki/Redirection_(computing) "wikipedia:Redirection (computing)"), for example in scripts, or if you care a lot about performance. In fact `< *file*` does the same as `cat *file*`.

*   *cat* can work with multiple lines:

```
$ cat << EOF >> *path/file*
*first line*
...
*last line*
EOF

```

Alternatively, using `printf`:

```
$ printf '%s
' 'first line' ... 'last line'

```

*   If you need to list file lines in reverse order, there is a coreutil command called [tac](https://en.wikipedia.org/wiki/tac_(Unix) (*cat* reversed).

### less

[less](https://en.wikipedia.org/wiki/less_(Unix) is a terminal pager program used to view the contents of a text file one screen at a time. Whilst similar to other pagers such as [more](https://en.wikipedia.org/wiki/more_(command) and the [deprecated](https://git.kernel.org/cgit/utils/util-linux/util-linux.git/tree/Documentation/deprecated.txt) [pg](https://en.wikipedia.org/wiki/pg_(Unix) "wikipedia:pg (Unix)"), *less* offers a more advanced interface and complete [feature-set](http://www.greenwoodsoftware.com/less/faq.html).

See [List of applications#Terminal pagers](/index.php/List_of_applications#Terminal_pagers "List of applications") for alternatives.

#### Vim as alternative pager

[Vim](/index.php/Vim "Vim") includes a script to view the content of text files, compressed files, binaries and directories. Add the following line to your shell configuration file to use it as a pager:

 `~/.bashrc`  `alias less='/usr/share/vim/vim80/macros/less.sh'` 

There is also an alternative to the *less.sh* macro, which may work as the `PAGER` environment variable. Install [vimpager](https://www.archlinux.org/packages/?name=vimpager) and add the following to your shell configuration file:

 `~/.bashrc` 
```
export PAGER='vimpager'
alias less=$PAGER
```

Now programs that use the `PAGER` environment variable, like [git](/index.php/Git "Git"), will use *vim* as pager.

### mkdir

[mkdir](https://en.wikipedia.org/wiki/mkdir "wikipedia:mkdir") makes directories.

To create a directory and its whole hierarchy, the `-p` switch is used, otherwise an error is printed.

Changing mode of a just created directory using *chmod* is not necessary as the `-m` option lets you define the access permissions.

**Tip:** If you just want a temporary directory, a better alternative may be [mktemp](https://en.wikipedia.org/wiki/Temporary_file "wikipedia:Temporary file"): `mktemp -d`

### mv

[mv](https://en.wikipedia.org/wiki/mv "wikipedia:mv") moves and renames files and directories.

**Note:** "Security aliases" are dangerous because you get used to them, resulting in potential data loss when you use another system / user that doesn't have these aliases.

To limit potential damage caused by the command, use an alias:

```
alias mv='mv -iv'

```

This alias asks for confirmation before overwriting any existing files and lists the operations in progress.

### rm

[rm](https://en.wikipedia.org/wiki/rm_(Unix) removes files or directories.

**Note:** "Security aliases" are dangerous because you get used to them, resulting in potential data loss when you use another system / user that doesn't have these aliases.

To limit potential damage caused by the command, use an alias:

```
alias rm='rm -Iv --one-file-system'

```

This alias asks confirmation to delete three or more files, lists the operations in progress, does not involve more than one file systems. Substitute `-I` with `-i` if you prefer to confirm even for one file.

Zsh users may want to prefix `noglob` to avoid implicit expansions.

To remove directories believed to be empty, use *rmdir* as it fails if there are files inside the target.

### chmod

See [File permissions and attributes#Changing permissions](/index.php/File_permissions_and_attributes#Changing_permissions "File permissions and attributes").

### chown

See [File permissions and attributes#Changing ownership](/index.php/File_permissions_and_attributes#Changing_ownership "File permissions and attributes").

### find

*find* is part of the [findutils](https://www.archlinux.org/packages/?name=findutils) package, which belongs to the [base](https://www.archlinux.org/groups/x86_64/base/) package group.

**Tip:** [fd](https://www.archlinux.org/packages/?name=fd) is a simple, fast and user-friendly alternative to `find` that provides more sensible defaults (e.g. ignores hidden files, directories and `.gitignore`'d files, `fd PATTERN` instead of `find -iname '*PATTERN*'`). It features colorized output (similar to `ls`), Unicode awareness, regular expressions and more.

One would probably expect a *find* command to take as argument a file name and search the filesystem for files matching that name. For a program that does exactly that see [#locate](#locate) below.

Instead, find takes a set of directories and matches each file under them against a set of expressions. This design allows for some very powerful "one-liners" that would not be possible using the "intuitive" design described above. See [GregsWiki:UsingFind](https://mywiki.wooledge.org/UsingFind "gregswiki:UsingFind") for usage details.

### locate

[Install](/index.php/Install "Install") the [mlocate](https://www.archlinux.org/packages/?name=mlocate) package. The package contains an `updatedb.timer` unit, which invokes a database update each day. The timer is enabled right after installation, [start](/index.php/Start "Start") it manually if you want to use it before reboot. You can also manually run *updatedb* as root at any time. By default, paths such as `/media` and `/mnt` are ignored, so *locate* may not discover files on external devices. See [updatedb(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/updatedb.8) for details.

The *locate* command is a common Unix tool for quickly finding files by name. It offers speed improvements over the [find](https://en.wikipedia.org/wiki/Find_(Unix) tool by searching a pre-constructed database file, rather than the filesystem directly. The downside of this approach is that changes made since the construction of the database file cannot be detected by *locate*.

Before *locate* can be used, the database will need to be created. To do this, execute `updatedb` as root.

See also [How locate works and rewrite it in one minute](http://jvns.ca/blog/2015/03/05/how-the-locate-command-works-and-lets-rewrite-it-in-one-minute/).

## Text streams

### grep

[grep](https://en.wikipedia.org/wiki/grep "wikipedia:grep") is a command line text search utility originally written for Unix. The *grep* command searches files or standard input for lines matching a given regular expression, and prints these lines to standard output.

*   Remember that *grep* handles files, so a construct like `cat *file* | grep *pattern*` is replaceable with `grep *pattern* *file*`
*   There are *grep* alternatives optimized for VCS source code, such as [ripgrep](https://www.archlinux.org/packages/?name=ripgrep), [the_silver_searcher](https://www.archlinux.org/packages/?name=the_silver_searcher), and [ack](https://www.archlinux.org/packages/?name=ack).
*   To include file line numbers in the output, use the `-n` option.
*   *grep* can also be used for hexadecimal search in a binary file, to look for let say the `A1 F2` sequence in a file, the command line is: `$ LANG=C grep --text --perl-regexp "\xA1\xF2" */path/to/file*` 

**Note:** Some commands send their output to [stderr(3)](https://jlk.fjfi.cvut.cz/arch/manpages/man/stderr.3), and grep has no apparent effect. In this case, redirect *stderr* to *stdout* with `*command* 2>&1 | grep *args*` or (for Bash 4) `*command* |& grep *args*`. See also [I/O Redirection](http://www.tldp.org/LDP/abs/html/io-redirection.html).

For color support, see [Color output in console#grep](/index.php/Color_output_in_console#grep "Color output in console").

See [grep(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/grep.1) for more details.

### sed

[sed](https://en.wikipedia.org/wiki/sed "wikipedia:sed") is stream editor for filtering and transforming text.

Here is a handy [list](http://sed.sourceforge.net/sed1line.txt) of *sed* one-liners examples.

**Tip:** More powerful alternatives are [awk](#awk) and the [Perl](/index.php/Perl "Perl") language.

### awk

[AWK](https://en.wikipedia.org/wiki/AWK "wikipedia:AWK") is a pattern scanning and processing language. There are multiple implementations:

*   **gawk** — GNU version of awk, see [gawk(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/gawk.1).

	[https://www.gnu.org/software/gawk/](https://www.gnu.org/software/gawk/) || [gawk](https://www.archlinux.org/packages/?name=gawk) (part of [base](https://www.archlinux.org/groups/x86_64/base/))

*   **nawk** — The one, true implementation of AWK, see [nawk(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/nawk.1).

	[https://www.cs.princeton.edu/~bwk/btl.mirror/](https://www.cs.princeton.edu/~bwk/btl.mirror/) || [nawk](https://www.archlinux.org/packages/?name=nawk)

*   **mawk** — A very fast AWK implementation.

	[http://invisible-island.net/mawk/](http://invisible-island.net/mawk/) || [mawk](https://aur.archlinux.org/packages/mawk/)

*   [BusyBox](/index.php/BusyBox "BusyBox") also includes an AWK implementation.

### pv

You can use [pv](https://www.archlinux.org/packages/?name=pv) to monitor the progress of data through a pipeline, for example:

```
# dd if=*/source/filestream* | pv -*monitor_options* -s *size_of_file* | dd of=*/destination/filestream*

```

In most cases `pv` functions as a drop-in replacement for `cat`.

## System administration

| Command | Description | Manual page | Example |
| mount | Mount a partition | [mount(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/mount.8) | mount /dev/sdc1 /media/usb |
| df -h | Show remaining space on all partitions | [df(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/df.1) |
| ps -A | Show all running processes | [ps(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/ps.1) |
| killall | Kill all running instances of a process | [killall(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/killall.1) |
| ss -at | Display a list of open TCP sockets | [ss(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/ss.8) |

### sudo

See [Sudo](/index.php/Sudo "Sudo").

### which

[which](https://en.wikipedia.org/wiki/Which_(Unix) shows the full path of shell commands. In the following example the full path of `ssh` is used as an argument for `journalctl`:

```
# journalctl $(which sshd)

```

### lsblk

[lsblk(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/lsblk.8) will show all available [block devices](https://en.wikipedia.org/wiki/Device_file#Block_devices "wikipedia:Device file") along with their partitioning schemes, for example:

 `$ lsblk -f` 
```
NAME   FSTYPE   LABEL       UUID                                 MOUNTPOINT
sda
├─sda1 vfat                 C4DA-2C4D                            /boot
├─sda2 swap                 5b1564b2-2e2c-452c-bcfa-d1f572ae99f2 [SWAP]
└─sda3 ext4                 56adc99b-a61e-46af-aab7-a6d07e504652 /

```

The beginning of the device name specifies the type of block device. Most modern storage devices (e.g. hard disks, [SSDs](/index.php/SSD "SSD") and USB flash drives) are recognised as SCSI disks (`sd`). The type is followed by a lower-case letter starting from `a` for the first device (`sda`), `b` for the second device (`sdb`), and so on. *Existing* partitions on each device will be listed with a number starting from `1` for the first partition (`sda1`), `2` for the second (`sda2`), and so on. In the example above, only one device is available (`sda`), and that device has three partitions (`sda1` to `sda3`), each with a different [file system](/index.php/File_system "File system").

Other common block device types include for example `mmcblk` for memory cards and `nvme` for [NVMe](/index.php/NVMe "NVMe") devices. Unknown types can be searched in the [kernel documentation](https://www.kernel.org/doc/html/latest/admin-guide/devices.html).

### ip

[ip](https://en.wikipedia.org/wiki/Iproute2 "wikipedia:Iproute2") allows you to show information about network devices, IP addresses, routing tables, and other objects in the Linux [IP](https://en.wikipedia.org/wiki/Internet_Protocol "wikipedia:Internet Protocol") software stack. By appending various commands, you can also manipulate or configure most of these objects.

**Note:** The *ip* utility is provided by the [iproute2](https://www.archlinux.org/packages/?name=iproute2) package, which is included in the [base](https://www.archlinux.org/groups/x86_64/base/) group.

| Object | Purpose | Manual page |
| ip addr | protocol address management | [ip-address(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/ip-address.8) |
| ip addrlabel | protocol address label management | [ip-addrlabel(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/ip-addrlabel.8) |
| ip l2tp | tunnel Ethernet over IP (L2TPv3) | [ip-l2tp(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/ip-l2tp.8) |
| ip link | network device configuration | [ip-link(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/ip-link.8) |
| ip maddr | multicast addresses management | [ip-maddress(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/ip-maddress.8) |
| ip monitor | watch for netlink messages | [ip-monitor(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/ip-monitor.8) |
| ip mroute | multicast routing cache management | [ip-mroute(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/ip-mroute.8) |
| ip mrule | rule in multicast routing policy db |
| ip neigh | neighbour/ARP tables management | [ip-neighbour(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/ip-neighbour.8) |
| ip netns | process network namespace management | [ip-netns(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/ip-netns.8) |
| ip ntable | neighbour table configuration | [ip-ntable(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/ip-ntable.8) |
| ip route | routing table management | [ip-route(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/ip-route.8) |
| ip rule | routing policy database management | [ip-rule(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/ip-rule.8) |
| ip tcp_metrics | management for TCP Metrics | [ip-tcp_metrics(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/ip-tcp_metrics.8) |
| ip tunnel | tunnel configuration | [ip-tunnel(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/ip-tunnel.8) |
| ip tuntap | manage TUN/TAP devices |
| ip xfrm | manage IPsec policies | [ip-xfrm(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/ip-xfrm.8) |

The `help` command is available for all objects. For example, typing `ip addr help` will show you the command syntax available for the address object. For advanced usage see the [iproute2 documentation](http://www.policyrouting.org/iproute2.doc.html).

The [Network configuration](/index.php/Network_configuration "Network configuration") article shows how the *ip* command is used in practice for various common tasks.

**Note:** You might be familiar with the [ifconfig](https://en.wikipedia.org/wiki/ifconfig "wikipedia:ifconfig") command, which is deprecated in Arch Linux; use *ip* instead.

### ss

*ss* is a utility to investigate network ports and is part of the [iproute2](https://www.archlinux.org/packages/?name=iproute2) package in the [base](https://www.archlinux.org/groups/x86_64/base/) group. It has a similar functionality to the [deprecated](https://www.archlinux.org/news/deprecation-of-net-tools/) netstat utility.

Common usage includes:

Display all TCP Sockets with service names:

```
$ ss -at

```

Display all TCP Sockets with port numbers:

```
$ ss -atn

```

Display all UDP Sockets:

```
$ ss -au

```

For more information see [ss(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/ss.8) or `ss.html` from the [iproute2](https://www.archlinux.org/packages/?name=iproute2) package.

## Miscellaneous

| Command | Description | Manual page | Example |
| strings | Show printable characters in binary files | [strings(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/strings.1) | strings /usr/bin/free |

### dd

[dd](https://en.wikipedia.org/wiki/dd_(Unix) is a utility for Unix and Unix-like operating systems whose primary purpose is to convert and copy a file.

Similarly to *cp*, by default *dd* makes a bit-to-bit copy of the file, but with lower-level I/O flow control features.

Some notable applications of *dd* are:

*   [Disk cloning#Using dd](/index.php/Disk_cloning#Using_dd "Disk cloning"),

*   Binary file patching: let say one wants to replace offset `0x123AB` of a file with the `FF C0 14` hexadecimal sequence, this can be done with the command line: `# printf '\xff\xc0\x14' | dd seek=$((0x123AB)) conv=notrunc bs=1 of=*/path/to/file*` 

For more information see [dd(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/dd.1) or the [full documentation](https://www.gnu.org/software/coreutils/dd).

**Tip:** By default, *dd* outputs nothing until the task has finished. To monitor the progress of the operation, add the `status=progress` option to the command.

**Warning:** One should be extremely cautious using *dd*, as with any command of this kind it can destroy data irreversibly.

### iconv

*iconv* converts the encoding of characters from one codeset to another.

The following command will convert the file `*foo*` from ISO-8859-15 to UTF-8, saving it to `*foo*.utf`:

```
$ iconv -f ISO-8859-15 -t UTF-8 *foo* > *foo*.utf

```

See [iconv(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/iconv.1) for more details.

#### Convert a file in place

**Tip:** You can use [recode](https://www.archlinux.org/packages/?name=recode) instead of iconv if you do not want to touch the mtime.

Unlike [sed](#sed), *iconv* does not provide an option to convert a file in place. However, `sponge` from the [moreutils](https://www.archlinux.org/packages/?name=moreutils) package can help:

```
$ iconv -f WINDOWS-1251 -t UTF-8 *foobar*.txt | sponge *foobar*.txt

```

See [sponge(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/sponge.1) for details.

### od

The [od](https://en.wikipedia.org/wiki/od_(Unix) (*o*ctal *d*ump) command is useful for visualizing data that is not in a human-readable format, like the executable code of a program, or the contents of an unformatted device. See the [manual](https://www.gnu.org/software/coreutils/manual/html_node/od-invocation.html#od-invocation) for more information.

### seq

*seq* prints a sequence of numbers. Shell built-in alternatives are available, so it is good practice to use them as explained on [Wikipedia](https://en.wikipedia.org/wiki/Seq_(Unix) "wikipedia:Seq (Unix)").

### tar

As an early Unix archiving format, .tar files—known as "tarballs"—are widely used for packaging in Unix-like operating systems. Both [pacman](/index.php/Pacman "Pacman") and [AUR](/index.php/AUR "AUR") packages are compressed tarballs, and Arch uses [GNU's](/index.php/GNU_Project "GNU Project") *tar* program by default.

For *.tar* archives, *tar* by default will extract the file according to its extension:

```
$ tar xvf *file.EXTENSION*

```

Forcing a given format:

| File Type | Extraction Command |
| `*file*.tar` | `tar xvf *file*.tar` |
| `*file*.tgz` | `tar xvzf *file*.tgz` |
| `*file*.tar.gz` | `tar xvzf *file*.tar.gz` |
| `*file*.tar.bz` | `bzip -cd *file*.bz | tar xvf -` |
| `*file*.tar.bz2` | `tar xvjf *file*.tar.bz2`
`bzip2 -cd *file*.bz2 | tar xvf -` |
| `*file*.tar.xz` | `tar xvJf *file*.tar.xz`
`xz -cd *file*.xz | tar xvf -` |
| `*file*.tar.zst` | `tar -I zstd xvf *file*.tar.zst` |

The construction of some of these *tar* arguments may be considered legacy, but they are still useful when performing specific operations. See [tar(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/tar.1) for details.

**Note:** Although GNU's *tar* is installed as the default *tar* program, official Arch Linux projects like [pacman](/index.php/Pacman "Pacman") and [mkinitcpio](/index.php/Mkinitcpio "Mkinitcpio") use *bsdtar* from the [libarchive](https://www.archlinux.org/packages/?name=libarchive) package.

### wipefs

*wipefs* can list or erase [file system](/index.php/File_system "File system"), [RAID](/index.php/RAID "RAID") or [partition-table](/index.php/Partition "Partition") signatures (magic strings) from the specified device. It does not erase the file systems themselves nor any other data from the device.

See [wipefs(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/wipefs.8) for more information.

For example, to erase all signatures from the device `/dev/sdb` and create a signature backup `~/wipefs-sdb-*offset*.bak` file for each signature:

```
# wipefs --all --backup /dev/sdb

```

## See also

*   [POSIX Utilities](http://pubs.opengroup.org/onlinepubs/9699919799/idx/utilities.html)
*   [GNU Coreutils online documentation](https://www.gnu.org/software/coreutils/manual/coreutils.html)
*   [A sampling of coreutils on Reddit](http://www.reddit.com/r/commandline/comments/19garq/a_sampling_of_coreutils_120/) [, part 2](http://www.reddit.com/r/commandline/comments/19ge6v/a_sampling_of_coreutils_2040/) [, part 3](http://www.reddit.com/r/commandline/comments/19j1w3/a_sampling_of_coreutils_4060/) - Overview of commands in coreutils
*   [Learn the DD command](https://www.linuxquestions.org/questions/linux-newbie-8/learn-the-dd-command-362506/)