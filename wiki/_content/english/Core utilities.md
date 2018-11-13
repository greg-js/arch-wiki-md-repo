Related articles

*   [Command-line shell](/index.php/Command-line_shell "Command-line shell")
*   [Users and groups](/index.php/Users_and_groups "Users and groups")
*   [systemd](/index.php/Systemd "Systemd")
*   [pacman](/index.php/Pacman "Pacman")
*   [General recommendations](/index.php/General_recommendations "General recommendations")

*Core utilities* are the basic, fundamental tools of a [GNU](/index.php/GNU "GNU")/[Linux](/index.php/Linux "Linux") system. On Arch Linux they are found in the [base group](/index.php/Base_group "Base group"). This article provides an incomplete overview of them, links their documentation and describes useful alternatives. The scope of this article includes, but is not limited to, the [GNU coreutils](https://www.gnu.org/software/coreutils/coreutils.html). Most core utilities are traditional [Unix](https://en.wikipedia.org/wiki/Unix "wikipedia:Unix") tools (see [Heirloom](/index.php/Heirloom "Heirloom")) and many were standardized by [POSIX](https://en.wikipedia.org/wiki/POSIX "wikipedia:POSIX") but have been developed further to provide more features.

Most command-line interfaces are documented in [man pages](/index.php/Man_page "Man page"), utilities by the [GNU Project](/index.php/GNU_Project "GNU Project") are documented in [Info manuals](/index.php/Info_manual "Info manual"), some [shells](/index.php/Shell "Shell") provide a `help` command for shell builtin commands. Additionally most utilities print their usage when run with the `--help` flag.

## Contents

*   [1 Essentials](#Essentials)
    *   [1.1 Preventing data loss](#Preventing_data_loss)
*   [2 Nonessentials](#Nonessentials)
*   [3 Alternatives](#Alternatives)
    *   [3.1 find alternatives](#find_alternatives)
    *   [3.2 diff alternatives](#diff_alternatives)
    *   [3.3 grep alternatives](#grep_alternatives)
        *   [3.3.1 Code searchers](#Code_searchers)
        *   [3.3.2 Interactive filters](#Interactive_filters)
*   [4 See also](#See_also)

## Essentials

The following table lists some important utilities which Arch Linux users should be familiar with. See also [intro(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/intro.1).

| Package | Utility | Description | Documentation | Alternatives |
| shell built-ins | cd | change directory | [cd(1p)](https://jlk.fjfi.cvut.cz/arch/manpages/man/cd.1p) |
| GNU [coreutils](https://www.archlinux.org/packages/?name=coreutils) | ls | list directory | [ls(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/ls.1), [info](https://www.gnu.org/software/coreutils/manual/html_node/ls-invocation.html) | [exa](https://www.archlinux.org/packages/?name=exa), [tree](https://www.archlinux.org/packages/?name=tree) |
| cat | concatenate files to stdout | [cat(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/cat.1), [info](https://www.gnu.org/software/coreutils/manual/html_node/cat-invocation.html) | [tac(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/tac.1) |
| mkdir | make directory | [mkdir(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/mkdir.1), [info](https://www.gnu.org/software/coreutils/manual/html_node/mkdir-invocation.html) |
| rmdir | remove empty directory | [rmdir(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/rmdir.1), [info](https://www.gnu.org/software/coreutils/manual/html_node/rmdir-invocation.html) |
| rm | remove files or directories | [rm(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/rm.1), [info](https://www.gnu.org/software/coreutils/manual/html_node/rm-invocation.html) | [shred](/index.php/Shred "Shred") |
| cp | copy files or directories | [cp(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/cp.1), [info](https://www.gnu.org/software/coreutils/manual/html_node/cp-invocation.html) |
| mv | move files or directories | [mv(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/mv.1), [info](https://www.gnu.org/software/coreutils/manual/html_node/mv-invocation.html) |
| ln | make hard or symbolic links | [ln(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/ln.1), [info](https://www.gnu.org/software/coreutils/manual/html_node/ln-invocation.html) |
| [chown](/index.php/Chown "Chown") | change file owner and group | [chown(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/chown.1), [info](https://www.gnu.org/software/coreutils/manual/html_node/chown-invocation.html) | [chgrp(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/chgrp.1) |
| [chmod](/index.php/Chmod "Chmod") | change file permissions | [chmod(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/chmod.1), [info](https://www.gnu.org/software/coreutils/manual/html_node/chmod-invocation.html) |
| [dd](/index.php/Dd "Dd") | convert and copy a file | [dd(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/dd.1), [info](https://www.gnu.org/software/coreutils/manual/html_node/dd-invocation.html) |
| df | report file system disk space usage | [df(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/df.1), [info](https://www.gnu.org/software/coreutils/manual/html_node/df-invocation.html) |
| GNU [tar](https://www.archlinux.org/packages/?name=tar) | [tar](/index.php/Tar "Tar") | tar archiver | [tar(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/tar.1), [info](https://www.gnu.org/software/tar/manual/html_chapter/index.html) | [archivers](/index.php/Archiver "Archiver") |
| GNU [less](https://www.archlinux.org/packages/?name=less) | less | terminal pager | [less(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/less.1) | [terminal pagers](/index.php/Terminal_pager "Terminal pager") |
| GNU [findutils](https://www.archlinux.org/packages/?name=findutils) | find | search files or directories | [find(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/find.1), [info](https://www.gnu.org/software/findutils/manual/html_node/find_html/index.html), [GregsWiki](https://mywiki.wooledge.org/UsingFind "gregswiki:UsingFind") | [#find alternatives](#find_alternatives) |
| GNU [diffutils](https://www.archlinux.org/packages/?name=diffutils) | diff | compare files line by line | [diff(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/diff.1), [info](https://www.gnu.org/software/diffutils/manual/html_node/Invoking-diff.html) | [#diff alternatives](#diff_alternatives) |
| GNU [grep](https://www.archlinux.org/packages/?name=grep) | grep | print lines matching a pattern | [grep(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/grep.1), [info](https://www.gnu.org/software/grep/manual/html_node/index.html) | [#grep alternatives](#grep_alternatives) |
| GNU [sed](https://www.archlinux.org/packages/?name=sed) | sed | stream editor | [sed(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/sed.1), [info](https://www.gnu.org/software/sed/manual/html_node/index.html), [one-liners](http://sed.sourceforge.net/sed1line.txt) |
| GNU [gawk](https://www.archlinux.org/packages/?name=gawk) | awk | pattern scanning and processing language | [gawk(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/gawk.1), [info](https://www.gnu.org/software/gawk/manual/html_node/index.html) | [nawk](https://www.archlinux.org/packages/?name=nawk), [mawk](https://aur.archlinux.org/packages/mawk/) |
| [util-linux](https://www.archlinux.org/packages/?name=util-linux) | [dmesg](https://en.wikipedia.org/wiki/dmesg "wikipedia:dmesg") | print or control the kernel ring buffer | [dmesg(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/dmesg.1) | [systemd journal](/index.php/Systemd_journal "Systemd journal") |
| [lsblk](/index.php/Lsblk "Lsblk") | list block devices | [lsblk(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/lsblk.8) |
| [mount](/index.php/Mount "Mount") | mount a filesystem | [mount(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/mount.8) |
| [umount](/index.php/Umount "Umount") | unmount a filesystem | [umount(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/umount.8) |
| [su](/index.php/Su "Su") | substitute user | [su(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/su.1) | [sudo](/index.php/Sudo "Sudo") |
| kill | terminate a process | [kill(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/kill.1) | [pkill(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/pkill.1), [killall(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/killall.1) |
| [procps-ng](https://www.archlinux.org/packages/?name=procps-ng) | pgrep | look up processes by name or attributes | [pgrep(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/pgrep.1) | [pidof(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/pidof.1) |
| ps | show information about processes | [ps(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/ps.1) | [top(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/top.1), [htop](https://www.archlinux.org/packages/?name=htop) |
| free | display amount of free and used memory | [free(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/free.1) |

### Preventing data loss

rm, mv, cp and shell redirections happily delete or overwrite files without asking. rm, mv and cp all support the `-i` flag to prompt the user before every removal / overwrite. Some users like to enable the `-i` flag by default using [aliases](/index.php/Alias "Alias"). Such shell settings are however dangerous because you get used to them, resulting in potential data loss when you use another system or user that does not have them. The best way to prevent data loss is to do [backups](/index.php/Backup "Backup").

## Nonessentials

This table lists core utilities that often come in handy.

| Package | Utility | Description | Documentation | Alternatives |
| shell built-ins | alias | define or display aliases | [alias(1p)](https://jlk.fjfi.cvut.cz/arch/manpages/man/alias.1p) |
| type | print the type of a command | [type(1p)](https://jlk.fjfi.cvut.cz/arch/manpages/man/type.1p) | [which(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/which.1) |
| time | time a command | [time(1p)](https://jlk.fjfi.cvut.cz/arch/manpages/man/time.1p) |
| GNU [coreutils](https://www.archlinux.org/packages/?name=coreutils) | tee | read stdin and write to stdout and files | [tee(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/tee.1), [info](https://www.gnu.org/software/coreutils/manual/html_node/tee-invocation.html) |
| mktemp | make a temporary file or directory | [mktemp(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/mktemp.1), [info](https://www.gnu.org/software/coreutils/manual/html_node/mktemp-invocation.html) |
| cut | print selected parts of lines | [cut(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/cut.1), [info](https://www.gnu.org/software/coreutils/manual/html_node/cut-invocation.html) |
| tr | translate or delete characters | [tr(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/tr.1), [info](https://www.gnu.org/software/coreutils/manual/html_node/tr-invocation.html) |
| od | dump files in octal and other formats | [od(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/od.1), [info](https://www.gnu.org/software/coreutils/manual/html_node/od-invocation.html) | [hexdump(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/hexdump.1), [vim](/index.php/Vim "Vim")'s [xxd(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/xxd.1) |
| sort | sort lines | [sort(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/sort.1), [info](https://www.gnu.org/software/coreutils/manual/html_node/sort-invocation.html) |
| uniq | report or omit repeated lines | [uniq(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/uniq.1), [info](https://www.gnu.org/software/coreutils/manual/html_node/uniq-invocation.html) |
| comm | compare two sorted files line by line | [comm(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/comm.1), [info](https://www.gnu.org/software/coreutils/manual/html_node/comm-invocation.html) |
| head | output the first part of files | [head(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/head.1), [info](https://www.gnu.org/software/coreutils/manual/html_node/head-invocation.html) |
| tail | output the last part of files, or follow files | [tail(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/tail.1), [info](https://www.gnu.org/software/coreutils/manual/html_node/tail-invocation.html) |
| wc | print newline, word and byte count | [wc(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/wc.1), [info](https://www.gnu.org/software/coreutils/manual/html_node/wc-invocation.html) |
| GNU [binutils](https://www.archlinux.org/packages/?name=binutils) | strings | print printable characters in binary files | [strings(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/strings.1), [info](https://sourceware.org/binutils/docs/binutils/strings.html) |
| GNU [glibc](https://www.archlinux.org/packages/?name=glibc) | iconv | convert character encodings | [iconv(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/iconv.1) | [recode](https://www.archlinux.org/packages/?name=recode) |
| [file](https://www.archlinux.org/packages/?name=file) | file | guess file type | [file(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/file.1) |

The [moreutils](https://www.archlinux.org/packages/?name=moreutils) package provides useful tools like [sponge(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/sponge.1) that are missing from the GNU coreutils.

## Alternatives

Alternatives to the core utilities in the [base](https://www.archlinux.org/groups/x86_64/base/) group are [BusyBox](/index.php/BusyBox "BusyBox"), the [Heirloom Toolchest](/index.php/Heirloom "Heirloom"), [9base](https://www.archlinux.org/packages/?name=9base), [sbase-git](https://aur.archlinux.org/packages/sbase-git/) and [ubase-git](https://aur.archlinux.org/packages/ubase-git/).

### find alternatives

*   **fd** — Simple, fast and user-friendly alternative to find. Ignores hidden and `.gitignore`'d files by default.

	[https://github.com/sharkdp/fd](https://github.com/sharkdp/fd) || [fd](https://www.archlinux.org/packages/?name=fd)

*   **fuzzy-find** — Fuzzy completion for finding files.

	[https://github.com/silentbicycle/ff](https://github.com/silentbicycle/ff) || [ff-git](https://aur.archlinux.org/packages/ff-git/)

*   **[mlocate](/index.php/Mlocate "Mlocate")** — Merging locate/updatedb implementation.

	[https://pagure.io/mlocate](https://pagure.io/mlocate) || [mlocate](https://www.archlinux.org/packages/?name=mlocate)

For graphical file searchers, see [List of applications/Utilities#File searching](/index.php/List_of_applications/Utilities#File_searching "List of applications/Utilities").

### diff alternatives

While [diffutils](https://www.archlinux.org/packages/?name=diffutils) does not provide a word-wise diff, several other programs do:

*   [git](/index.php/Git "Git") diff can do a word diff with `--color-words`, using `--no-index` it can also be used for files outside of Git working trees.
*   **dwdiff** — A word diff front-end for the diff program; supports colors.

	[https://os.ghalkes.nl/dwdiff.html](https://os.ghalkes.nl/dwdiff.html) || [dwdiff](https://www.archlinux.org/packages/?name=dwdiff)

*   **GNU wdiff** — A wordwise implementation of GNU diff; does not support colors.

	[https://www.gnu.org/software/wdiff/](https://www.gnu.org/software/wdiff/) || [wdiff](https://www.archlinux.org/packages/?name=wdiff)

*   **cwdiff** — A GNU wdiff wrapper that colorizes the output.

	[https://github.com/junghans/cwdiff](https://github.com/junghans/cwdiff) || [cwdiff](https://aur.archlinux.org/packages/cwdiff/), [cwdiff-git](https://aur.archlinux.org/packages/cwdiff-git/)

See also [List of applications/Utilities#Comparison, diff, merge](/index.php/List_of_applications/Utilities#Comparison,_diff,_merge "List of applications/Utilities").

### grep alternatives

*   **mgrep** — A multiline grep.

	[https://sourceforge.net/projects/multiline-grep/](https://sourceforge.net/projects/multiline-grep/) || [mgrep](https://aur.archlinux.org/packages/mgrep/)

#### Code searchers

The following three tools aim to replace grep for code search. They do recursive search by default, skip binary files and respect `.gitignore`.

*   **ack** — A Perl-based grep replacement, aimed at programmers with large trees of heterogeneous source code.

	[https://beyondgrep.com/](https://beyondgrep.com/) || [ack](https://www.archlinux.org/packages/?name=ack)

*   **ripgrep (rg)** — A search tool that combines the usability of ag with the raw speed of grep.

	[https://github.com/BurntSushi/ripgrep](https://github.com/BurntSushi/ripgrep) || [ripgrep](https://www.archlinux.org/packages/?name=ripgrep)

*   **The Silver Searcher (ag)** — Code searching tool similar to Ack, but faster.

	[https://github.com/ggreer/the_silver_searcher](https://github.com/ggreer/the_silver_searcher) || [the_silver_searcher](https://www.archlinux.org/packages/?name=the_silver_searcher)

#### Interactive filters

*   **[fzf](/index.php/Fzf "Fzf")** — General-purpose command-line fuzzy finder, powered by find by default.

	[https://github.com/junegunn/fzf](https://github.com/junegunn/fzf) || [fzf](https://www.archlinux.org/packages/?name=fzf), [fzf-git](https://aur.archlinux.org/packages/fzf-git/)

*   **fzy** — A fast, simple fuzzy text selector with an advanced scoring algorithm.

	[https://github.com/jhawthorn/fzy](https://github.com/jhawthorn/fzy) || [fzy](https://www.archlinux.org/packages/?name=fzy), [fzy-git](https://aur.archlinux.org/packages/fzy-git/)

*   **peco** — Simplistic interactive filtering tool.

	[https://github.com/peco/peco](https://github.com/peco/peco) || [peco](https://aur.archlinux.org/packages/peco/), [peco-git](https://aur.archlinux.org/packages/peco-git/)

*   **percol** — Adds flavor of interactive filtering to the traditional pipe concept of the UNIX shell.

	[https://github.com/mooz/percol](https://github.com/mooz/percol) || [percol](https://www.archlinux.org/packages/?name=percol), [percol-git](https://aur.archlinux.org/packages/percol-git/)

## See also

*   [GNU Coreutils documentation](https://www.gnu.org/software/coreutils/manual/coreutils.html)
*   [POSIX utilities](http://pubs.opengroup.org/onlinepubs/9699919799/idx/utilities.html)