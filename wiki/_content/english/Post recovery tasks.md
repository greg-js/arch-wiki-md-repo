Related articles

*   [File recovery](/index.php/File_recovery "File recovery")
*   [Sort images by resolution](/index.php/Sort_images_by_resolution "Sort images by resolution")

**Note:** To speed up access to the recovered or restored files you can use [shake](https://www.archlinux.org/packages/?name=shake) utility to defragment them.

## Contents

*   [1 List only unique files by checksum](#List_only_unique_files_by_checksum)
    *   [1.1 Clean up and sort file names](#Clean_up_and_sort_file_names)
*   [2 Photorec](#Photorec)
    *   [2.1 Creation of a file with data for arrays](#Creation_of_a_file_with_data_for_arrays)
    *   [2.2 Post recovery tasks](#Post_recovery_tasks)
        *   [2.2.1 Head of the script](#Head_of_the_script)
        *   [2.2.2 Start variables](#Start_variables)
        *   [2.2.3 Populate an array](#Populate_an_array)
            *   [2.2.3.1 With a *While* loop](#With_a_While_loop)
        *   [2.2.4 Loops for restoration](#Loops_for_restoration)
*   [3 Enough if files are few](#Enough_if_files_are_few)

## List only unique files by checksum

**Note:**

*   To list only files where *photorec* could restore original names you can add `if(index(A,"_") != 0)` before `print` in *awk*. You can also use the *awk* as stand alone command on an already created file to list only file names or extensions you need.
*   To list only extensions you can use `D=B;gsub(/[^*\.]*\./,"",D)` in *awk* that will cut everything until the last `.` dot that will show only *gz* even from *tar.gz* extension or you can use *sub* instead of *gsub* that will cut only until the first dot in the filename.

When files are restored it might be that many of them have the same [hash sum](https://en.wikipedia.org/wiki/Checksum "wikipedia:Checksum") and by making a list of the unique files including only one of the found duplicate files you will speed up gathering extra information about files with other utilities by using stored file names and path in it.

```
find -type f -print0 | \
 xargs -0  md5sum | \
 awk '// {Count[$1]++;
 if( Count[$1] == 1 ){C=substr($0,index($0,"./"));A=$0;sub(/^.*\//,"",A);B=substr(A,index(A,"_")+1);HASHsum=$1;
 print A"|"B"|"C"|"HASHsum}}' 

```

This will print out result on screen with pattern: **filename|restored_filename|full_path_to_filename|check_sum**

```
f851733136_WindowMaker_Dockapps.pdf|WindowMaker_Dockapps.pdf|./f851733136_WindowMaker_Dockapps.pdf|272cc4fcdc8027e3b8b53318f08f3f01

```

See also [crctk-git](https://aur.archlinux.org/packages/crctk-git/) for working with CRC32 checksums.

### Clean up and sort file names

To make destination file names more *bash* friendly you can remove special symbols, spaces and sort by second column for a better overview of duplicate names with different checksums. To the duplicate file names will be added a number with `¤` as a separator in front of the *restored_filename*. The script will use file created by script from above and print result to *stdout*.

 `clean_and_sort.sh` 
```
if [ ! -z "$1" ];then
  awk -F"|" '{B=$2;
   gsub(/\(/,"",B);gsub(/\)/,"",B);
   gsub(/!/,"",B); gsub(/?/,"",B);
   gsub(/\[/,"",B);gsub(/\]/,"",B);
   gsub(/{/,"",B); gsub(/}/,"",B);
   gsub(/&/,"",B); gsub(/=/,"",B);
   gsub(/\^/,"",B);gsub(/~/,"",B);
   gsub(" ","",B) ;gsub(/#/,"",B);
   gsub(/\"/,"",B);gsub(/;/,"",B);
   gsub(/\\/,"",B);gsub(/\//,"",B);
   sub(/-*/,"",B); sub(/+*/,"",B);
   print $1" | "B" | "$3}' "$1" | \
  sort --field-separator=\| -s -d -k 2  \
awk -F'|' '{B=$2;Count[B]++;sub(/ */,"",B);if( Count[$2] == 1 ){print $1"|"B"|"$3}else{print $1"|"Count[$2]-1"¤"B"|"$3"|"$4} }'
else echo 'Path to file is missing!'
fi

```

File names with special symbols especially if file names begins with them are harder to manage with commands like `mv` or `cp` without using quotes or backslash `\` but if you want to keep information about them then they can be replaced with [HTML hex codes](http://www.obkb.com/dcljr/charstxt.html) instead of removing all of them.

## Photorec

### Creation of a file with data for arrays

In this example the [xdg-mime](/index.php/Xdg-utils#xdg-mime "Xdg-utils") is used to gather information about the mime types but the `file --mime-type -b` and `file -i -b` commands does the same output as the `xdg-mime query filetype` command, with more or less details. This script will collect a lot of more additional information about the files into the **info-mime-size-db.txt**. Put the script in the destination directory that you used in *photorec*, make it executable and use path to files from the list with unique checksums described from above. e.g. `awk -F" | " '{system("start-collect-file-info.sh "$3" "$1" "$2)}' *file_list-unique_checksums*`.

 `start-collect-file-info.sh` 
```
#!/bin/bash
if [ ! -z "$1" ] && [ ! -z "$2" ] && [ ! -z "$3" ]; then
if [ -f "$1"  ]; then
echo "$1"
echo "$(file "$1" -F"|"  )'|'$(xdg-mime query filetype "$1")'|'$(du -h "$1" |awk '{print $1}' )|$2|$3" >> info-mime-size-db.txt
else
echo The « "$1" » is not a valid file name.
fi
fi
```

The script will build a file with pattern **path to file/file name | info about the file | mime type | size | filename | restored_filename**, here is an example:`./recup_dir.1/f872690288_image.jpg|JPEG image data, JFIF standard 1.01|image/jpeg|24K|f872690288_image.jpg|image.jpg`

### Post recovery tasks

This will help you more to understand the script and make your own scripts base on it. You can also put all necessary parts together into a script, modify patterns for files to search and run it. You need to create a database file with name `info-mime-size-db.txt` with information about files.

**Warning:**

*   Remove the `echo` command in front of the `cp` and `mkdir` otherwise the script will only show what is gonna to be done without restoring anything to a destination, do a dry run. To use `echo` command is good for verify that settings for filenames and destinations looks correctly.
*   Those scripts are only examples for restoration of files from folders created by *photorec*, be careful!

#### Head of the script

Here is a simple check if the `info-mime-size-db.txt` exists in the current directory to prevent possible errors with rest of the script.

```
#!/bin/bash
if [ -f info-mime-size-db.txt ]; then echo The file info-mime-size-db.txt exists continuing... ;
  else 
  echo Error!! the info-mime-size-db.txt file cannot be found;exit 1; 
fi

```

#### Start variables

```
CountAll="0"
CountToLimit="0"
BaseSubDirName="MyRestoredFiles"
Destination="$HOME/NameOfBaseFolder/${BaseSubDirName}-MoreDetailsInFolderName/"
NewDirNumber="0"
CountToLimit="0"
```

#### Populate an array

**Warning:** Arrays become populated by reading data from a `info-mime-size-db.txt` file. Otherwise the script will not work correctly!

##### With a *While* loop

Here will be a short examples about how to speed up population of the array from a file with patterns by using [bash standard expressions](http://tldp.org/LDP/abs/html/string-manipulation.html) instead of *awk*, *grep* and *sed*. The `ArrayOfFiles` array will contain full path to the file and the `ArrayOfsorted` will contain original names restored by *photorec* but without random generated part.

```
WhileArray=0;
while read i; do
if [[ "$i" =~ "gif" ]]||[[ "$i" =~ "jpeg" ]];then
ArrayOfFiles[WhileArray]=${i/'|'*/}
ArrayOfsorted[WhileArray]=${i/[^*|]*|/}
WhileArray=$((WhileArray+1));
fi;
done <  info-mime-size-db.txt
echo done, the array is full

```

#### Loops for restoration

This is a finale part of a script that manages restoration of files. When limit of files in a destination sub-directory reached then it creates and new one numbered sub-directory in the destination folder and continuing to copy files there.

```
SizeOfArray=${#ArrayOfFiles[@]}
while [  "${SizeOfArray}" != "${CountAll}" ]; do

IfExist="${Destination}${BaseSubDirName}${NewDirNumber}"
if [ ! -d "${IfExist}" ]; then echo mkdir -v "${IfExist}" -p;fi

CountToLimit=$((CountToLimit+1 ))
FileName=${ArrayOfsorted[CountAll]}
    if [ $CountToLimit -gt 25 ]; then
CountToLimit="0"
NewDirNumber=$((NewDirNumber+1))
fi;
NewDestination="$IfExist"

echo cp -fv "$PWD/${ArrayOfFiles[CountAll]}" "${IfExist}${FileName}"
CountAll=$((CountAll+1))
done
```

**Note:** In order to add more specific details about files in their names or names of the destination directories you will need to gather information about them with external programs, e.g. for image resolution: [feh](https://www.archlinux.org/packages/?name=feh) `feh -l "${ArrayOfFiles[$CountAll]}" | tail -1 | awk '{print $3"x"$4}'`, [imagemagick](https://www.archlinux.org/packages/?name=imagemagick) `identify ${ArrayOfFiles[$CountAll]} | awk '{print $3}'`.

## Enough if files are few

If it is not so many files with the same extension then it will be enough to use something like `find -name *.xcf -exec copy "{}" $HOME/Desktop \;` to avoid the *overload* of a destination folder you can calculate how many files are found `find -type f -name *xcf | wc -l`.
**Note:** The photorec utility stores up to 500 recovered files in a single folder.