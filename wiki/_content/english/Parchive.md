[Parchive](https://github.com/Parchive/par2cmdline) (Parity archive) is a file verification and repair tool using PAR2 files to detect damage in data files and repair them if necessary. It can be used with any kind of file.

## Contents

*   [1 Installation](#Installation)
*   [2 How it works](#How_it_works)
*   [3 Tips and tricks](#Tips_and_tricks)
    *   [3.1 Batch-protecting your files](#Batch-protecting_your_files)
    *   [3.2 Verification](#Verification)
    *   [3.3 Multithreading](#Multithreading)

## Installation

[Install](/index.php/Install "Install") the [par2cmdline](https://www.archlinux.org/packages/?name=par2cmdline) package. The commands `par2`, `par2create`, `par2verify` and `par2repair` are now available.

## How it works

`par2create` takes the input file(s) and interprets the input as a certain number of data blocks. Based on the data blocks, `par2create` then creates recovery blocks with the help of the [w:Reed–Solomon error correction](https://en.wikipedia.org/wiki/Reed%E2%80%93Solomon_error_correction "w:Reed–Solomon error correction") code. Later, you can trade any recovery block for any corrupted data block in order to repair the source data. You need as much recovery blocks as data blocks have gone corrupted in order to repair the file(s) successfully.

Let's say you want to calculate 30% of recovery information for a precious file:

```
$ par2create -r30 <file>

```

Parchive now has created the <file>.par2 index file which is essentially not needed for recovery. Additionally, it has created the recovery blocks and has spread them into multiple files. If you created, say, 592 recovery blocks, you will find the files

```
<file>.vol000+001.par2
<file>.vol001+002.par2
<file>.vol003+004.par2
<file>.vol007+008.par2
<file>.vol015+016.par2
<file>.vol031+032.par2
<file>.vol063+064.par2
<file>.vol127+128.par2
<file>.vol255+256.par2
<file>.vol511+081.par2

```

The number left of the plus sign is the index of the first recovery block in the particular file and the number on the right the number of recovery blocks the file provides.

In the early days where no integrity check was done on link level these files proved useful since one could select recovery files based on the number of data blocks gone corrupted. If your download left you with 43 corrupted data blocks, you could convert the number to binary and instantly see what recovery files you had to fetch:

```
    32 16  8  4  2  1
43 = 1  0  1  0  1  1

→ download *+032.par2, *+008.par2, *+002.par2 and *+001.par2.

```

This is very efficient in terms of bandwidth usage. One would finally call

```
$ par2repair <file>*.par2

```

in order to repair the downloaded file(s). You can ignore the index file since Parchive can handle a missing index file. Sometimes it is useful to include the `-N` parameter in order to reach an intact data block which would otherwise go undetected.

## Tips and tricks

### Batch-protecting your files

It may be the case that you don't want to serve clients recovery files, but want to ensure additional integrity of your files. In times of helium filled hard disk drives, shingled-bit technology, dense capacity per square centimeter, transfer losses etc. the probability of bit rot is high. Remember that you should always have (automated) [backups of your data](/index.php/Synchronization_and_backup_programs "Synchronization and backup programs"), but a little additional protection does not hurt, especially since we have so much storage available today. By creating `par2` files you have a much more convenient way to verify the integrity of your data and restore the data than running application programs over the files and sieving for error outputs. Bit rot now can happen in both the original file(s) AND the recovery file(s), and you still can repair the original file(s).

As a consequence, one recovery file containing all recovery packets is sufficient (parameter `-n1`). This also reduces the amount of recovery data. An important question to answer is the percentage of redundancy you want to have. Especially for smaller files (<1 MiB) the amount of recovery data does not really correlate with the original file size:

| Original data | percentage | Recovery data (without index) |
| 184.8 KiB | 5 | 287.8 KiB |
| 184.8 KiB | 100 | 743.1 KiB |
| 3.4 MiB | 5 | 458.8 KiB |
| 3.4 MiB | 30 | 1.5 MiB |
| 3.4 MiB | 100 | 4 MiB |
| 1.7 GiB | 5 | 87.6 MiB |

5% is a reasonable amount of recovery data but you can go up to 100% recovery data for really important files. 100% recovery files can restore your file if you accidentally deleted the original one and you are too lazy to search for the file in your backup (you have one, have you? :).

Here is a simple script which runs over the current directory recursively and batch-protects the files:

**Tip:** You may have to make sure that your `bin/` folder is in the search path:
```
$ export PATH=$PATH:$HOME/bin/

```
Put this line in your init file in your home directory to make it permanent.
 `$HOME/bin/batchprotect.sh` 
```
#!/bin/bash
OIFS="$IFS"
IFS=$'
'
for file in $(find . -type f | shuf) ; do
	ending=$(echo "$file" | sed 's/\(.*\)\.\(.*\)$/\2/')

	#include this block if you want to have 5% recovery data
	if [ ! -e "$file-5.par2" -a $ending != "par2" -a $ending != "sig" ]; then
		par2create -n1 -r5 "$file"
		rm "$file".par2
		mv "$file".vol*par2 "$file"-5.par2
	fi

	#include this block if you want to have 100% recovery data
	if [ ! -e "$file-100.par2" -a $ending != "par2" -a $ending != "sig" ]; then
		par2create -n1 -r100 "$file"
		rm "$file".par2
		mv "$file".vol*par2 "$file"-100.par2
	fi

	#include this block if you want to check for normal AND cryptographic integrity 
	if [ ! -e "$file.sig" -a $ending != "par2" -a $ending != "sig" ]; then
		gpg --default-key C0FFEEBEEFC0FFEEBEEFC0FFEEDEADBEEF31415926 --detach-sign --yes "$file"
	fi
done
IFS="$OIFS"
```

You would then call `batchprotect.sh` in order to have all files in the current directory recursively protected by Parchive. The detached signature serves you to be sure that no one tampered with your data. Additionally, you don't have to maintain list of checksums since gpg can do that for you, too.

### Verification

```
$ par2verify <file>-5.par2
$ cfv <file>-5.par2
$ gpg --verify <file>.sig

```

And, if you changed the path of the original file:

```
$ par2verify <file>-5.par2 /new/path/to/<fileRenamed>
$ gpg --verify <file>.sig /new/path/to/<fileRenamed>

```

You can also change the path of the `par2`/`sig` file.

### Multithreading

Parchive unfortunately does not support multithreading. You can compile available versions using tbb or OpenMP, see the [w:Parchive](https://en.wikipedia.org/wiki/Parchive "w:Parchive") article. Since the script shuffles the given list of files, a workaround is possible. You can run the script as many times as you have cores available in different shells. The script will ignore already processed files which allows for the collaboration of multiple instances of the script.