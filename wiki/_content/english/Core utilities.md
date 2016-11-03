This article deals with so-called *core* utilities on a GNU/Linux system, such as *less*, *ls*, and *grep*. The scope of this article includes, but is not limited to, those utilities included with the GNU [coreutils](https://www.archlinux.org/packages/?name=coreutils) package. What follows are various tips and tricks and other helpful information related to these utilities.

## Contents

*   [1 Basic commands](#Basic_commands)
*   [2 cat](#cat)
*   [3 dd](#dd)
*   [4 grep](#grep)
*   [5 find](#find)
*   [6 iconv](#iconv)
    *   [6.1 Convert a file in place](#Convert_a_file_in_place)
*   [7 ip](#ip)
*   [8 locate](#locate)
*   [9 less](#less)
    *   [9.1 Vim as alternative pager](#Vim_as_alternative_pager)
*   [10 ls](#ls)
    *   [10.1 Long format](#Long_format)
    *   [10.2 File names containing spaces enclosed in quotes](#File_names_containing_spaces_enclosed_in_quotes)
*   [11 lsblk](#lsblk)
*   [12 mkdir](#mkdir)
*   [13 mv](#mv)
*   [14 od](#od)
*   [15 pv](#pv)
*   [16 rm](#rm)
*   [17 sed](#sed)
*   [18 seq](#seq)
*   [19 ss](#ss)
*   [20 tar](#tar)
*   [21 which](#which)
*   [22 wipefs](#wipefs)
*   [23 See also](#See_also)

## Basic commands

The following table lists basic shell commands every Linux user should be familiar with. Commands in **bold** are part of the shell, others are separate programs called from the shell. See the below sections and *Related articles* for details.

| Command | Description | Manual page | Example |
| man | Show manual page for a command | [man(7)](http://man7.org/linux/man-pages/man7/man.7.html) | man ed |
| **cd** | Change directory | [cd(1)](http://man7.org/linux/man-pages/man1/cd.1.html) | cd /etc/pacman.d |
| mkdir | Create a directory | [mkdir(1)](http://man7.org/linux/man-pages/man1/mkdir.1.html) | mkdir ~/newfolder |
| rmdir | Remove empty directory | [rmdir(1)](http://man7.org/linux/man-pages/man1/rmdir.1.html) | rmdir ~/emptyfolder |
| rm | Remove a file | [rm(1)](http://man7.org/linux/man-pages/man1/rm.1.html) | rm ~/file.txt |
| rm -r | Remove directory and contents | rm -r ~/.cache |
| ls | List files | [ls(1)](http://man7.org/linux/man-pages/man1/ls.1.html) | ls *.mkv |
| ls -a | List hidden files | ls -a /home/archie |
| ls -al | List hidden files and file properties |
| mv | Move a file | [mv(1)](http://man7.org/linux/man-pages/man1/mv.1.html) | mv ~/compressed.zip ~/archive/compressed2.zip |
| cp | Copy a file | [cp(1)](http://man7.org/linux/man-pages/man1/cp.1.html) | cp ~/.bashrc ~/.bashrc.bak |
| chmod +x | Make a file executable | [chmod(1)](http://man7.org/linux/man-pages/man1/chmod.1.html) | chmod +x ~/.local/bin/myscript.sh |
| cat | Show file contents | [cat(1)](http://man7.org/linux/man-pages/man1/cat.1.html) | cat /etc/hostname |
| strings | Show printable characters in binary files | [strings(1)](http://man7.org/linux/man-pages/man1/strings.1.html) | strings /usr/bin/free |
| find | Search for a file | [find(1)](http://man7.org/linux/man-pages/man1/find.1.html) | find ~ -name myfile |
| mount | Mount a partition | [mount(8)](http://man7.org/linux/man-pages/man8/mount.8.html) | mount /dev/sdc1 /media/usb |
| df -h | Show remaining space on all partitions | [df(1)](http://man7.org/linux/man-pages/man1/df.1.html) |
| ps -A | Show all running processes | [ps(1)](http://man7.org/linux/man-pages/man1/ps.1.html) |
| killall | Kill all running instances of a process | [killall(1)](http://man7.org/linux/man-pages/man1/killall.1.html) |
| ss -at | Display a list of open TCP sockets | [ss(8)](http://man7.org/linux/man-pages/man8/ss.8.html) |

## cat

[cat](https://en.wikipedia.org/wiki/cat_(Unix) is a standard Unix utility that concatenates and lists files.

*   Because *cat* is not a built-in shell, on many occasions you may find it more convenient to use a [redirection](https://en.wikipedia.org/wiki/Redirection_(computing) "wikipedia:Redirection (computing)"), for example in scripts, or if you care a lot about performance. In fact `< *file*` does the same as `cat *file*`.

*   *cat* is able to work with multiple lines:

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

*   If you need to list file lines in reverse order, there is a utility called [tac](https://en.wikipedia.org/wiki/tac_(Unix) (*cat* reversed).

## dd

[dd](https://en.wikipedia.org/wiki/dd_(Unix) is a utility for Unix and Unix-like operating systems whose primary purpose is to convert and copy a file.

Similarly to *cp*, by default *dd* makes a bit-to-bit copy of the file, but with lower-level I/O flow control features.

**Tip:** By default, *dd* outputs nothing until the task has finished. To monitor the progress of the operation, add the `status=progress` option to the command.

'dd' can be used to:

*   [drive-related](/index.php/Disk_cloning#Using_dd "Disk cloning") tasks:
    *   Create an image.
    *   Write an image.
    *   Clone whole drive, or partition.
    *   Wipe drive or partition.
    *   Erase partition table or boot sector.
    *   Backup boot sector.
    *   Restore system.
*   Get stream from device, `dd /dev/random`, or some input device.
*   Create load on CPU (example: `dd if=/dev/zero of=/dev/null`).
*   Create load on disk (example: `dd if=/dev/zero of=/*path*/*testfile* bs=*number_of*G count=*times* oflag=*fdatasync*`).
*   Create I/O load on disk (many rapid read/writes) (example above with little block size (`bs`) and big amount of cycles (`count`) and needed `oflag`, based on what and how you want to test).
*   As a backup utility or part of solution.
*   Convert a file to upper/lower case.

For more information see [dd(1)](http://man7.org/linux/man-pages/man1/dd.1.html) or the [full documentation](http://www.gnu.org/software/coreutils/dd).

## grep

[grep](https://en.wikipedia.org/wiki/grep "wikipedia:grep") (from [ed](https://en.wikipedia.org/wiki/ed "wikipedia:ed")'s *g/re/p*, *global/regular expression/print*) is a command line text search utility originally written for Unix. The *grep* command searches files or standard input for lines matching a given regular expression, and prints these lines to the program's standard output.

*   Remember that *grep* handles files, so a construct like `cat *file* | grep *pattern*` is replaceable with `grep *pattern* *file*`
*   There are *grep* alternatives optimized for VCS source code, such as [the_silver_searcher](https://www.archlinux.org/packages/?name=the_silver_searcher) and [ack](https://www.archlinux.org/packages/?name=ack).
*   To include file line numbers in the output, use the `-n` option.

**Note:** Some commands send their output to [stderr(3)](http://man7.org/linux/man-pages/man3/stderr.3.html), and grep has no apparent effect. In this case, redirect *stderr* to *stdout* with `*command* 2>&1 | grep *args*` or (for Bash 4) `*command* |& grep *args*`. See also [I/O Redirection](http://www.tldp.org/LDP/abs/html/io-redirection.html).

For color support, see [Color output in console#grep](/index.php/Color_output_in_console#grep "Color output in console").

## find

*find* is part of the [findutils](https://www.archlinux.org/packages/?name=findutils) package, which belongs to the [base](https://www.archlinux.org/groups/x86_64/base/) package group.

One would probably expect a *find* command to take as argument a file name and search the filesystem for files matching that name. For a program that does exactly that see [#locate](#locate) below.

Instead, find takes a set of directories and matches each file under them against a set of expressions. This design allows for some very powerful "one-liners" that would not be possible using the "intuitive" design described above. See [UsingFind](http://mywiki.wooledge.org/UsingFind) for usage details.

## iconv

*iconv* converts the encoding of characters from one codeset to another.

The following command will convert the file `foo` from ISO-8859-15 to UTF-8 saving it to `foo.utf`:

```
$ iconv -f ISO-8859-15 -t UTF-8 foo > foo.utf

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

| Object | Purpose | Manual page |
| ip addr | protocol address management | ip-address(8) |
| ip addrlabel | protocol address label management | [ip-addrlabel(8)](http://man7.org/linux/man-pages/man8/ip-addrlabel.8.html) |
| ip l2tp | tunnel Ethernet over IP (L2TPv3) | [ip-l2tp(8)](http://man7.org/linux/man-pages/man8/ip-l2tp.8.html) |
| ip link | network device configuration | ip-link(8) |
| ip maddr | multicast addresses management | [ip-maddress(8)](http://man7.org/linux/man-pages/man8/ip-maddress.8.html) |
| ip monitor | watch for netlink messages | [ip-monitor(8)](http://man7.org/linux/man-pages/man8/ip-monitor.8.html) |
| ip mroute | multicast routing cache management | [ip-mroute(8)](http://man7.org/linux/man-pages/man8/ip-mroute.8.html) |
| ip mrule | rule in multicast routing policy db |
| ip neigh | neighbour/ARP tables management | [ip-neighbour(8)](http://man7.org/linux/man-pages/man8/ip-neighbour.8.html) |
| ip netns | process network namespace management | [ip-netns(8)](http://man7.org/linux/man-pages/man8/ip-netns.8.html) |
| ip ntable | neighbour table configuration | [ip-ntable(8)](http://man7.org/linux/man-pages/man8/ip-ntable.8.html) |
| ip route | routing table management | ip-route(8) |
| ip rule | routing policy database management | [ip-rule(8)](http://man7.org/linux/man-pages/man8/ip-rule.8.html) |
| ip tcp_metrics | management for TCP Metrics | [ip-tcp_metrics(8)](http://man7.org/linux/man-pages/man8/ip-tcp_metrics.8.html) |
| ip tunnel | tunnel configuration | [ip-tunnel(8)](http://man7.org/linux/man-pages/man8/ip-tunnel.8.html) |
| ip tuntap | manage TUN/TAP devices |
| ip xfrm | manage IPsec policies | [ip-xfrm(8)](http://man7.org/linux/man-pages/man8/ip-xfrm.8.html) |

The `help` command is available for all objects. For example, typing `ip addr help` will show you the command syntax available for the address object. For advanced usage see the [iproute2 documentation](http://www.policyrouting.org/iproute2.doc.html).

The [Network configuration](/index.php/Network_configuration "Network configuration") article shows how the *ip* command is used in practice for various common tasks.

**Note:** You might be familiar with the [ifconfig](https://en.wikipedia.org/wiki/ifconfig "wikipedia:ifconfig") command, which was used in older versions of Linux for interface configuration. It is now deprecated in Arch Linux; you should use *ip* instead.

## locate

[Install](/index.php/Install "Install") the [mlocate](https://www.archlinux.org/packages/?name=mlocate) package. After installation a script is automatically scheduled to run a daily task to update its database. You can also manually run *updatedb* as root at any time. By default, paths such as `/media` and `/mnt` are ignored, so *locate* may not discover files on external devices. See [updatedb(1)](http://man7.org/linux/man-pages/man1/updatedb.1.html) for details.

The *locate* command is a common Unix tool for quickly finding files by name. It offers speed improvements over the [find](https://en.wikipedia.org/wiki/Find "wikipedia:Find") tool by searching a pre-constructed database file, rather than the filesystem directly. The downside of this approach is that changes made since the construction of the database file cannot be detected by *locate*. This problem is minimised by regular, typically scheduled use of the *updatedb* command, which (as the name suggests) updates the database.

Before *locate* can be used, the database will need to be created. To do this, execute `updatedb` as root.

See also [How locate works and rewrite it in one minute](http://jvns.ca/blog/2015/03/05/how-the-locate-command-works-and-lets-rewrite-it-in-one-minute/).

## less

[less](https://en.wikipedia.org/wiki/less_(Unix) is a terminal pager program used to view the contents of a text file one screen at a time. Whilst similar to other pagers such as [more](https://en.wikipedia.org/wiki/more_(command) and [pg](https://en.wikipedia.org/wiki/pg_(Unix) "wikipedia:pg (Unix)"), *less* offers a more advanced interface and complete [feature-set](http://www.greenwoodsoftware.com/less/faq.html).

See [List of applications#Terminal pagers](/index.php/List_of_applications#Terminal_pagers "List of applications") for alternatives.

### Vim as alternative pager

[Vim](/index.php/Vim "Vim") includes a script to view the content of text files, compressed files, binaries, directories. Add the following line to your shell configuration file to use it as a pager:

 `~/.bashrc`  `alias less='/usr/share/vim/vim74/macros/less.sh'` 

There is also an alternative to *less.sh* macro, which may work as the `PAGER` environment variable. Install [vimpager](https://www.archlinux.org/packages/?name=vimpager) and add the following to your shell configuration file:

 `~/.bashrc` 
```
export PAGER='vimpager'
alias less=$PAGER
```

Now programs that use the `PAGER` environment variable, like [git](/index.php/Git "Git"), will use *vim* as pager.

## ls

[ls](https://en.wikipedia.org/wiki/ls "wikipedia:ls") lists directory contents.

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

### File names containing spaces enclosed in quotes

By default, file and directory names that contain spaces are displayed surrounded by single quotes. To change this behavior use the `-N` or `--quoting-style=literal` options. Alternatively, set the `QUOTING_STYLE` [environment variable](/index.php/Environment_variable "Environment variable") to `literal`. [[1]](https://unix.stackexchange.com/questions/258679/why-is-ls-suddenly-surrounding-items-with-spaces-in-single-quotes)

## lsblk

[lsblk(8)](http://man7.org/linux/man-pages/man8/lsblk.8.html) will show all available [block devices](https://en.wikipedia.org/wiki/Device_file#Block_devices "w:Device file") along with their partitioning schemes, for example:

 `$ lsblk -f` 
```
NAME   FSTYPE   LABEL       UUID                                 MOUNTPOINT
sda
├─sda1 vfat                 C4DA-2C4D                            /boot
├─sda2 swap                 5b1564b2-2e2c-452c-bcfa-d1f572ae99f2 [SWAP]
└─sda3 ext4                 56adc99b-a61e-46af-aab7-a6d07e504652 /

```

The beginning of the device name specifies the type of block device. Most modern storage devices (e.g. hard disks, [SSDs](/index.php/SSD "SSD") and USB flash drives) are recognised as SCSI disks (`sd`). The type is followed by a lower-case letter starting from `a` for the first device (`sda`), `b` for the second device (`sdb`), and so on. *Existing* partitions on each device will be listed with a number starting from `1` for the first partition (`sda1`), `2` for the second (`sda2`), and so on. In the example above, only one device is available (`sda`), and that device has three partitions (`sda1` to `sda3`), each with a different [file system](/index.php/File_system "File system").

Other common block device types include for example `mmcblk` for memory cards and `nvme` for [NVMe](/index.php/Solid_State_Drives/NVMe "Solid State Drives/NVMe") devices. Unknown types can be searched in the [kernel documentation](https://www.kernel.org/doc/Documentation/devices.txt).

## mkdir

[mkdir](https://en.wikipedia.org/wiki/mkdir "wikipedia:mkdir") makes directories.

To create a directory and its whole hierarchy, the `-p` switch is used, otherwise an error is printed. As users are supposed to know what they want, `-p` switch may be used as a default:

```
alias mkdir='mkdir -p -v'

```

The `-v` switch make it verbose.

Changing mode of a just created directory using *chmod* is not necessary as the `-m` option lets you define the access permissions.

**Tip:** If you just want a temporary directory, a better alternative may be [mktemp](https://en.wikipedia.org/wiki/Temporary_file "wikipedia:Temporary file"): `mktemp -p`.

## mv

[mv](https://en.wikipedia.org/wiki/mv "wikipedia:mv") moves and renames files and directories.

To limit potential damage caused by the command, use an alias:

```
alias mv='timeout 8 mv -iv'

```

This alias suspends *mv* after eight seconds, asks for confirmation before overwriting any existing files, lists the operations in progress and does not store itself in the shell history file if the shell is configured to ignore space starting commands.

## od

The [od](https://en.wikipedia.org/wiki/od_(Unix) (*o*ctal *d*ump) command is useful for visualizing data that is not in a human-readable format, like the executable code of a program, or the contents of an unformatted device. See the [manual](http://www.gnu.org/software/coreutils/manual/html_node/od-invocation.html#od-invocation) for more information.

## pv

You can use [pv](https://www.archlinux.org/packages/?name=pv) (*pipe viewer*) to monitor the progress of data through a pipeline, for example:

```
# dd if=*/source/filestream* | pv -*monitor_options* -s *size_of_file* | dd of=*/destination/filestream*

```

In most cases `pv` functions as a drop-in replacement for `cat`.

## rm

[rm](https://en.wikipedia.org/wiki/rm_(Unix) removes files or directories.

To limit potential damage caused by the command, use an alias:

```
alias rm='timeout 3 rm -Iv --one-file-system'

```

This alias suspends *rm* after three seconds, asks confirmation to delete three or more files, lists the operations in progress, does not involve more than one file systems and does not store itself in the shell history file if the shell is configured to ignore space starting commands. Substitute `-I` with `-i` if you prefer to confirm even for one file.

Zsh users may want to put `noglob` before `timeout` to avoid implicit expansions.

To remove directories known to be empty, use *rmdir* as it fails in case of files inside the target.

## sed

[sed](https://en.wikipedia.org/wiki/sed "wikipedia:sed") is stream editor for filtering and transforming text.

Here is a handy [list](http://sed.sourceforge.net/sed1line.txt) of *sed* one-liners examples.

**Tip:** More powerful alternatives are [AWK](https://en.wikipedia.org/wiki/AWK "wikipedia:AWK") and even [Perl](https://en.wikipedia.org/wiki/Perl "wikipedia:Perl") language.

## seq

*seq* prints a sequence of numbers. Shell built-in alternatives are available, so it is good practice to use them as explained on [Wikipedia](https://en.wikipedia.org/wiki/Seq_(Unix) "wikipedia:Seq (Unix)").

## ss

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

For more information see [ss(8)](http://man7.org/linux/man-pages/man8/ss.8.html) or [introductory examples](http://www.cyberciti.biz/files/ss.html).

## tar

As an early Unix archiving format, .tar files—known as "tarballs"—are widely used for packaging in Unix-like operating systems. Both [pacman](/index.php/Pacman "Pacman") and [AUR](/index.php/AUR "AUR") packages are compressed tarballs, and Arch uses [GNU's](/index.php/GNU_Project "GNU Project") *tar* program by default.

For .tar archives, *tar* by default will extract the file according to its extension:

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

The construction of some of these *tar* arguments may be considered legacy, but they are still useful when performing specific operations. See its [man page](/index.php/Man_page "Man page") with `man tar` for details.

## which

[which](https://en.wikipedia.org/wiki/Which_(Unix) shows the full path of shell commands. In the following example the full path of `ssh` is used as an argument for `journalctl`:

```
# journalctl $(which sshd)

```

## wipefs

*wipefs* can list or erase [file system](/index.php/File_system "File system"), [RAID](/index.php/RAID "RAID") or [partition-table](/index.php/Partition "Partition") signatures (magic strings) from the specified device. It does not erase the file systems themselves nor any other data from the device.

See [wipefs(8)](http://man7.org/linux/man-pages/man8/wipefs.8.html) for more information.

For example, to erase all signatures from the device `/dev/sdb` and create a signature backup `~/wipefs-sdb-*offset*.bak` file for each signature:

```
# wipefs --all --backup /dev/sdb

```

## See also

*   [A sampling of coreutils](http://www.reddit.com/r/commandline/comments/19garq/a_sampling_of_coreutils_120/) [, part 2](http://www.reddit.com/r/commandline/comments/19ge6v/a_sampling_of_coreutils_2040/) [, part 3](http://www.reddit.com/r/commandline/comments/19j1w3/a_sampling_of_coreutils_4060/) - Overview of commands in coreutils
*   [GNU Coreutils online documentation](http://www.gnu.org/software/coreutils/manual/coreutils.html)
*   [Learn the DD command](http://www.linuxquestions.org/questions/linux-newbie-8/learn-the-dd-command-362506/)