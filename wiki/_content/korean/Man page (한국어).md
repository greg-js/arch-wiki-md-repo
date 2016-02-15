**Man pages** ("manual pages"의 약어)는 아치 리눅스를 포함해 모든 UNIX와 비슷한 운영체제들에 기본적으로 제공되는 설명서들이며 `man`은 그 설명서들을 표시하는데 사용되는 명령어입니다.

In spite of their scope, man pages are designed to be self-contained documents, consequentially limiting themselves to referring to other man pages when discussing related subjects. This is in sharp contrast with the hyperlink-aware info files, GNU's attempt at replacing the traditional man page format.

## Contents

*   [1 Man 문서 접근하는 방법](#Man_.EB.AC.B8.EC.84.9C_.EC.A0.91.EA.B7.BC.ED.95.98.EB.8A.94_.EB.B0.A9.EB.B2.95)
*   [2 포멧](#.ED.8F.AC.EB.A9.A7)
*   [3 설명서 검색](#.EC.84.A4.EB.AA.85.EC.84.9C_.EA.B2.80.EC.83.89)
*   [4 Colored man pages](#Colored_man_pages)
    *   [4.1 First method: using 'most'](#First_method:_using_.27most.27)
    *   [4.2 Second method: using 'less'](#Second_method:_using_.27less.27)
*   [5 Reading man pages with a browser](#Reading_man_pages_with_a_browser)
    *   [5.1 Using Local Man Pages](#Using_Local_Man_Pages)
    *   [5.2 Using Online Man Pages](#Using_Online_Man_Pages)

## Man 문서 접근하는 방법

man 문서를 읽으려면 아래에 적힌 대로 입력한다.

```
$ man _page_name_

```

설명서들은 아래의 목록들로 정렬이된다.

1.  일반 명령
2.  시스템 콜 (커널에서 제공하는 함수들)
3.  라이브러리 콜 (C 라이브러리 함수들)
4.  특별한 파일들 (/dev 폴더에서 찾아서 사용랄 수 있는) 그리고 기기들
5.  파일 포멧들 그리고 conventions
6.  게임(?)
7.  여러가지들.. (conventions에 포함된)
8.  시스템 운영자 멘트 (root 권한을 가진) 그리고 데몬들

Man pages are usually referred to by their name, followed by their section number in parentheses. Often there are multiple man pages of the same name, such as man(1) and man(7). In this case, give man the section number followed by the name of the man page, for example:

```
$ man 5 passwd

```

to read the man page on `/etc/passwd`, rather than the `passwd` utility.

Very brief descriptions of programs can be read out of man pages without displaying the whole page using the `whatis` command. For example, for a brief description of ls, type:

```
$ whatis ls

```

and `whatis` will output "list directory contents."

## 포멧

Man pages all follow a fairly standard format, which helps in navigating them. Some sections which are often present include:

*   NAME - The name of the command and a one-line statement of its purpose.
*   SYNOPSIS - A list of the options and arguments a command takes or the parameters the function takes and its header file.
*   DESCRIPTION - A more in depth description of a command or function's purpose and workings.
*   EXAMPLES - Common examples, usually ranging from the simple to the relatively complex.
*   OPTIONS - Descriptions of each of the options a command takes and what they do.
*   EXIT STATUS - The meanings of different exit codes.
*   FILES - Files related to a command or function.
*   BUGS - Problems with the command or function that are pending repair. Also known as KNOWN BUGS.
*   SEE ALSO - A list of related commands or functions.
*   AUTHOR, HISTORY, COPYRIGHT, LICENSE, WARRANTY - Information about the program, its past, its terms of use, and its creator.

## 설명서 검색

Whilst the `man` utility allows users to display man pages, a problem arises when one knows not the exact name of the desired manual page in the first place! Fortunately, the `-k` or `--apropos` options can be used to search the manual page descriptions for instances of a given keyword. For example, to search for man pages related to "password":

```
$ man -k password

```

or:

```
$ man --apropos password

```

This is equivalent to calling the `apropos` command:

```
$ apropos password

```

The given keyword is interpreted as a regular expression by default.

## Colored man pages

For some users, color-enabled man pages allow for a clearer presentation and easier digestion of the content. Given that users new to Linux are prone to spend a considerable amount of time familiarizing themselves with basic userspace tools, setting up a comfortable environment is a necessity to most.

There are two prevalent methods for achieving colored man pages: using `most`, or opting for `less`. The former is simpler to configure, at the expense of the advanced functionality that is native to `less`.

### First method: using 'most'

Install [most](https://www.archlinux.org/packages/?name=most) using [pacman](/index.php/Pacman "Pacman"):

```
# pacman -S most

```

This is similar to `less` and `more`, yet allows rendering colored text in an easier way.

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

### Second method: using 'less'

	<small>_Source: [nion's blog - less colors for man pages](http://nion.modprobe.de/blog/archives/572-less-colors-for-man-pages.html)_</small>

Alternatively, getting an approximate coloured result in manual pages with `less` is also a possibility. This method has the advantage that `less` has a bigger feature set than `most`, and that might be the preference for advanced users.

Add the following to a shell configuration file. For [Bash](/index.php/Bash "Bash") it would be `~/.bashrc`:

```
man() {
	env \
		LESS_TERMCAP_mb=$(printf "\e[1;37m") \
		LESS_TERMCAP_md=$(printf "\e[1;37m") \
		LESS_TERMCAP_me=$(printf "\e[0m") \
		LESS_TERMCAP_se=$(printf "\e[0m") \
		LESS_TERMCAP_so=$(printf "\e[1;47;30m") \
		LESS_TERMCAP_ue=$(printf "\e[0m") \
		LESS_TERMCAP_us=$(printf "\e[0;36m") \
			man "$@"
}

```

To customize the colors, see [Wikipedia:ANSI escape code](https://en.wikipedia.org/wiki/ANSI_escape_code "wikipedia:ANSI escape code") for reference.

## Reading man pages with a browser

Instead of the standard interface, using browsers such as [lynx](/index.php/Lynx "Lynx") and [Firefox](/index.php/Firefox "Firefox") to view man pages allows users to reap info pages' main benefit: hyperlinked text. Additionally, [KDE](/index.php/KDE "KDE") users can read man pages in Konqueror using:

```
man:<name>

```

### Using Local Man Pages

First, install [man2html](https://www.archlinux.org/packages/?name=man2html) from the [AUR](/index.php/AUR "AUR").

Now, convert a man page:

```
$ man free | man2html -compress -cgiurl man$section/$title.$section$subsection.html > ~/man/free.html

```

Another use for `man2html` is exporting to raw, printer-friendly text:

```
$ man free | man2html -bare > ~/free.txt

```

The GNU implementation of man in the Arch repositories also has the ability to do this on its own:

```
$ man -H free

```

This will read your `BROWSER` environment variable to determine the browser. You can override this by passing the binary to the -H option.

### Using Online Man Pages

There are several online databases of man pages, many of them listed on [Wikipedia:Man_page#Repositories_of_manual_pages](https://en.wikipedia.org/wiki/Man_page#Repositories_of_manual_pages "wikipedia:Man page"), including:

*   [_Debian GNU/Linux man pages_](http://manpages.debian.net/)
*   [_DragonFlyBSD manual pages_](http://leaf.dragonflybsd.org/cgi/web-man)
*   [_FreeBSD Hypertext Man Pages_](http://www.freebsd.org/cgi/man.cgi)
*   [_Linux and Solaris 10 Man Pages_](http://www.manpages.spotlynx.com/)
*   [_Linux/FreeBSD Man Pages_](http://manpagehelp.net) with user comments
*   [_Linux man pages at die.net_](http://linux.die.net/man/)
*   [The Linux man-pages project at kernel.org](http://www.kernel.org/doc/man-pages/)
*   [Man-Wiki: _Linux / Solaris / UNIX / BSD_](http://man-wiki.net/index.php/Main_Page)
*   [_NetBSD manual pages_](http://netbsd.gw.com/cgi-bin/man-cgi)
*   [_Mac OS X Manual Pages_](http://developer.apple.com/documentation/Darwin/Reference/ManPages/index.html)
*   [_On-line UNIX manual pages_](http://unixhelp.ed.ac.uk/alphabetical/index.html)
*   [_OpenBSD manual pages_](http://www.openbsd.org/cgi-bin/man.cgi)
*   [_Plan 9 Manual — Volume 1_](http://man.cat-v.org/plan_9/)
*   [_Inferno Manual — Volume 1_](http://man.cat-v.org/inferno/)
*   [_Storage Foundation Man Pages_](http://sfdoccentral.symantec.com/sf/5.0MP3/linux/manpages/index.html)
*   [_The Missing Man Project_](http://markhobley.yi.org/manpages/missingman.html) [dead link as of 9 July 2010]
*   [_Gobuntu Manual Pages_](http://en.linuxpages.info/index.php?title=Main_Page) [dead link as of 9 July 2010]
*   [_The UNIX and Linux Forums Man Page Repository_](http://www.unix.com/man-page/OpenSolaris/1/man/)
*   [_Ubuntu Manpage Repository_](http://manpages.ubuntu.com/)