See [Core utilities](/index.php/Core_utilities "Core utilities") for the main article.

## Contents

*   [1 grep](#grep)
    *   [1.1 Colored output](#Colored_output)
*   [2 less](#less)
    *   [2.1 Colored output through environment variables](#Colored_output_through_environment_variables)
    *   [2.2 Colored output through wrappers](#Colored_output_through_wrappers)
    *   [2.3 Vim as alternative pager](#Vim_as_alternative_pager)
    *   [2.4 Colored output when reading from stdin](#Colored_output_when_reading_from_stdin)
*   [3 ls](#ls)
    *   [3.1 Colored output](#Colored_output_2)
*   [4 tar](#tar)
    *   [4.1 Backup with parallel compression](#Backup_with_parallel_compression)
    *   [4.2 Restore name of a tar.gz archive](#Restore_name_of_a_tar.gz_archive)
        *   [4.2.1 Collect info data about tar.gz](#Collect_info_data_about_tar.gz)
        *   [4.2.2 Restore filenames](#Restore_filenames)

## grep

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

## ls

### Colored output

Colored output can be enabled with a simple alias. File `~/.bashrc` should already have the following entry copied from `/etc/skel/.bashrc`:

```
alias ls='ls --color=auto'

```

The next step will further enhance the colored *ls* output; for example, broken (orphan) symlinks will start showing in a red hue. Add the following to your shell configuration file:

```
eval $(dircolors -b)

```

## tar

### Backup with parallel compression

To back up using parallel compression ([SMP](https://en.wikipedia.org/wiki/Symmetric_multiprocessing "wikipedia:Symmetric multiprocessing")), use [pbzip2](https://www.archlinux.org/packages/?name=pbzip2) (Parallel bzip2).

First back up the files to a plain tarball with no compression:

```
# tar -cvf /*destionation_path*/etc-backup.tar /etc

```

Then use pbzip2 to compress it in parallel:

```
$ pbzip2 /path/to/chosen/directory/etc-backup.tar.bz2

```

Store `etc-backup.tar.bz2` on one or more offline media, such as a USB stick, external hard drive, or CD-R. Occasionally verify the integrity of the backup process by comparing original files and directories with their backups. Possibly maintain a list of hashes of the backed up files to make the comparison quicker.

Restore corrupted `/etc` files by extracting the `etc-backup.tar.bz2` file in a temporary working directory, and copying over individual files and directories as needed. To restore the entire `/etc` directory with all its contents execute the following command as root:

```
tar -xvjf etc-backup.tar.bz2 -C /

```

### Restore name of a tar.gz archive

Here describes about how you can restore normal names for the most of a recovered tar.gz archives by [photorec](/index.php/File_recovery#Testdisk_and_PhotoRec "File recovery"). First you need to create a file with a more detailed information about files, see: [post recovery tasks](/index.php/File_recovery#Creating_a_database_with_more_details_about_files "File recovery"). Restored tar.gz files with photorec might look like `./recup_dir.996/f864593944_wmmaiload-1.0.5.tar.gz` or `./recup_dir.996/f864589184.tar.gz`.

The *tar.gz* archive includes inside a *tar* archive whose name is used to restore filename of the *tar.gz* if it is possible or name of a first folder/file from inside of the archive.

The ways that might be used to restore the name of the tar.gz archives:

*   From part of a name by cutting everything before '_' in files with created by photorec with pattern: f864593944_wmmaiload-1.0.5.tar.gz
*   From name of a tar inside of the tar.gz archive.
*   From the name of the folder inside it. In many cases it usually compressed a whole folder that might be similar to the archive name.

**Note:** This script restores only by separating original name from the photorec generated name or use a name of the first folder or file inside of the archive.
To restore all of the files that contain only the original name as part of the generated you can download the *restore-orignames-only.sh* script from the [SourceForge](https://sourceforge.net/projects/postrecoverytasksphotorec/) website, but it will add the *Duplicate123* (123 is number of a processed file) to files with the same name in the destination directory.

#### Collect info data about tar.gz

Collecting needed data from inside of the archives in order to restore their names.

 `collect-info-about-tar-gz.sh` 
```
#!/bin/bash

FileName="$1"
IntCheck=$(7z t "$1" | grep ^"Everything is Ok"$ )
AddIt="False"

if [ 'XX'"$IntCheck" != 'XXEverything is Ok'   ]; then ErrorFlag="Damaged";else ErrorFlag='OK';fi;

if [ 'XX'"$(echo "$FileName" | grep -i tar.gz$ )" != 'XX'  ];then
AddIt='True'

BaseFileName=$(tar -tvf "$FileName" | head -1 | awk '{ print substr($0, index($0,$6)) }' )
OutOfOrig="$( echo "$1" | awk '{ print substr($0, index($0,$4)) }' )"
if [ 'XX'"$(echo "${BaseFileName}" | grep '/')" == 'XX' ]; then

BaseFileName="$(echo "${BaseFileName}"|  sed 's/\///m')"
fi
fi

if [ $AddIt == 'True'  ]; then

if [ 'XX'"${OutOfOrig}" != 'XX'   ]; then IfOrig=$(echo "$OutOfOrig" | grep -v '/') ;fi
if [ 'XX'"${IfOrig}" != 'XX'   ]; then BaseFileName="$IfOrig" ; fi
BF="$(echo "$BaseFileName" | sed 's/\///g' | sed 's/^\.//m' )"
echo "$1"'|'"${BF}"'.tar.gz''|'Errors:'|'$ErrorFlag'|' >> /tmp/tmpDB.txt
fi;

```

Run `find -type f -name *.tar.gz -exec collect-info-about-tar-gz.sh "{}"\;`

#### Restore filenames

This will restore file names based on collected ínfo about files.

 `restore-tar-gz-names.sh` 
```
#!/bin/bash
CountAll=0

Destination="$HOME/tar-gz"
mkdir -v "$(echo $Destination)" -p

  ArrayFillCount=0;
while read line ; do
  ArrayFillCount=$((ArrayFillCount+1))
      ArrayOfFiles[$ArrayFillCount]=$line
done < /tmp/tmpDB.txt;

XX=${#ArrayOfFiles[@]}
echo $XX
while [  $XX != $CountAll ] ; do
FolderName="$(echo ${ArrayOfFiles[$CountAll]} | awk -F'|' '{print $2}' | cut -c1-4 | tr '[:lower:]'  '[:upper:]' )"
PathToFile="$(echo ${ArrayOfFiles[$CountAll]} | awk -F'|' '{print $1}')"
  FileName="$(echo ${ArrayOfFiles[$CountAll]} | awk -F'|' '{print $2}')"
#SourceFolder="$(echo $PathToFile | sed s/$(basename $PathToFile)//m )"
 SourceFolder='./Sorted/'

if [  "$(echo $FolderName)" ==  '.TAR'  ];then
   FileName="$(echo ${ArrayOfFiles[$CountAll]} | awk -F'_' '{ print substr($0, index($0,$4))}'|awk -F'|' '{print $1}' )"
   FolderName="$(echo $FileName | cut -c1-4 | tr '[:lower:]'  '[:upper:]' )"
fi
if [ -f "$FileName" ]; then
     FIX="$(echo $PathToFile | sed s/$(basename $PathToFile)//m )"
     BadName="$(echo $PathToFile | awk -F"$FIX" '{print $2}' )"
     if [ -d "${Destination}/BadName"  ];then echo A > /dev/null;else mkdir "${Destination}/BadName";fi
     cp -fv "${PathToFile}" "${Destination}"'/'BadName'/'"$BadName"
else
  IfExist="$(echo $Destination/${SourceFolder}${FolderName})"
  if [ -d "$IfExist"  ]; then echo a > /dev/null;else mkdir -vp "$(echo $Destination/${SourceFolder}${FolderName})"; fi
     if [ -f "$Destination/${SourceFolder}${FolderName}"'/'"$FileName"   ]; 
     then DupName="${FileName}"_Duplicate"${CountAll}";
IfExist="$(echo $Destination/Duples)"
if [ -d "$IfExist"  ]; then echo a > /dev/null;
cp -fv "${PathToFile}" "$Destination/Duples"'/'"$DupName";
else 
mkdir -vp "$(echo $Destination/Duples)";
cp -fv "${PathToFile}" "$Destination/Duples"'/'"$DupName";fi
  else
cp -fv "${PathToFile}" "$Destination/${SourceFolder}${FolderName}"'/'"$FileName"
  fi

fi
CountAll=$((CountAll+1))
echo $CountAll
done;
echo $XX

```

Files will be restored with pattern like `$HOME/tar-gz/Sorted/MIXE` where *MIXE* is the first 4 letters of a filename. You can adjust it with the `cut -c1-4` command inside the script. In the `$HOME/tar-gz/BadName` places damaged files or files where it was impossible to get filename. In the `$HOME/tar-gz/Duples` places duplicates of files with pattern *filename.tar.gz_Duplicate123* where 123 is a number of a processed file.