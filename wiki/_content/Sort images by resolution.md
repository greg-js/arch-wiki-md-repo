# Sort images by resolution

**Note:** To speed up access to the recovered or restored files you can use [shake](https://www.archlinux.org/packages/?name=shake) utility to defragment them.

When recovery of files done and you restored images with help of a [post recovery tasks](/index.php/Post_recovery_tasks "Post recovery tasks") script then it could be wise to sort images by the resolution. This will help to sort the photos you made, webcam images or any other images into the folders by the resolutions, most of them are often using the same related image resolutions.

## Collect info about images

**Warning:** You must have installed the [feh](https://www.archlinux.org/packages/?name=feh) program before running the script.

**Note:** To speed up collecting info about images you can skip duplicate images by use a list of [non duplicate](/index.php/Post_recovery_tasks#List_only_unique_files_by_checksum "Post recovery tasks") files but you will also need to remove mime type check in this script and add check files by extension instead.

 `collect-info-about-images.sh` 

```
#!/bin/bash
if [ 'XX' != 'XX'"$1" ]; then 
 if [ -f "$1"  ]; then
# mime part start
  IsIt=$(file "$1" --mime-type -b);
  NeedImageOnly="ItIs_"${IsIt/'/'*/}
   if [ "$NeedImageOnly" == "ItIs_image" ] ; then
# mime part end
ImageInfoFEH=($(feh -l "$1"))
IfDamaged=${?}
ImageType=${ImageInfoFEH[9]}
   Height=${ImageInfoFEH[11]}
    Width=${ImageInfoFEH[10]}
   if [ "$IfDamaged" != '0'  ]; then 
    echo "$1" "Damaged" "${IfDamaged}";
   fi;
    echo "$1"'|'W'|'$Width'|'H'|'$Height'|'Format'|'$ImageType'|'Errors'|'$IfDamaged'|' >> collect-info-about-images.txt
# mime part start
  fi
# mime part end
   else
    echo The « "$1" » is not a valid file name.
  fi
 else
  ScriptsName=${0##*/}
   find -type f -exec sh -e "./$ScriptsName" "{}" \;
  #find -type f  -name "*.jpg" -o -name "*.gif" -o -name "*.png" -exec sh -e "./$ScriptsName" "{}" \;
fi

```

The _$IfDamaged_ variable contains an exit status code returned by [feh](https://www.archlinux.org/packages/?name=feh).

**Note:**

*   The [feh](https://www.archlinux.org/packages/?name=feh) program ignores some of errors, pixel data errors, in an image if it contains enough of a readable visual data to be shown.
*   A pixel error makes that a part of an image or a whole image can't be shown correctly, it causes wrong colors or blank/empty spaces that often makes the image more or less useless, mostly depends on the amount of a corrupted data in it.

You can also install [pngcheck](https://aur.archlinux.org/packages/pngcheck/) to check integrity of "PNG, JNG or MNG" and/or [jpeginfo](https://aur.archlinux.org/packages/jpeginfo/) and use output of errors in the _$IfDamaged_ variable or modify script to skip adding of damaged files into a `collect-info-about-images.txt` file.

Example of [pngcheck](https://aur.archlinux.org/packages/pngcheck/) check resuslt:

```
./f939799496.png  invalid IDAT row-filter type (11)
./f939799496.png  private (invalid?) IDAT row-filter type (236) (warning)
./f939799496.png  private (invalid?) IDAT row-filter type (231) (warning)
./f939799496.png  invalid IDAT row-filter type (49)
./f939799496.png  zlib: inflate error = -3 (data error)
ERROR: ./f939799496.png
OK: ./f218842888.png (532x552, 32-bit RGB+alpha, non-interlaced, 95.8%).

```

Example of [jpeginfo](https://aur.archlinux.org/packages/jpeginfo/) check result:

```
f62152912.jpg 5678 x 2829 24bit Exif  N 11625509  Corrupt JPEG data: 1074 extraneous bytes before marker 0xd9  [WARNING]
f124619744.jpg  144 x 119  24bit JFIF  N    5813  [OK]

```

**Note:** The [jpeginfo](https://aur.archlinux.org/packages/jpeginfo/) utility can't scan directories recursively but can read filenames from a file created by `find -type f -name "*.jpg">>FileWithPathTo-images.txt`, calculate their md5sums and has an option that makes it able to remove damaged image files.

To extract necessary data from a string in a script is better to use an [expression](http://tldp.org/LDP/abs/html/string-manipulation.html) instead of an extern program as [sed](https://www.archlinux.org/packages/?name=sed) or [gawk](https://www.archlinux.org/packages/?name=gawk) to make a script work a little faster, e.g.

```
AA="$(jpeginfo -c f62152912.jpg)";
ZZ="${AA/*' [OK]'/}"; 

if [ 'XX'"$ZZ" == 'XX' ]; then 
  echo File is good'!!!';
fi
```

The _collect-info-about-images.sh_ script generates data about images by pattern:

```
**full path to image**|**Width**|size|**Height**|size|**Format**|type of image|**Errors**|exit code by feh|

```

Example: `Images/f269351998.bmp|W|40|H|39|Format|bmp|Errors|0|`

## Sort images by resolution

This script creates folders based on the resolution. You can set your limitations about how many files should be in each folder and how many sub-directories in a base file type named folder. When limit is reached a new number in the order will be added to a directory name for creation. If you have a really huge amount of files and don't want to overload a single folder with all of them then you can also add your own counters for a new sub-folders after the base destination variable `IfExist="${Destination}/`, just look out for quotes " to be in the begin and end of a whole destination path. It use to be much more easier to browse folders with a limited amount of images, thumbnails loads much faster and to remember or add to favorite a folder number/name instead of trying to find once more same image in an overloaded folder out of probably thousand images there.

**Warning:**

*   Those script are only examples and you must modify them for your needs before using, be careful!
*   Remove the `echo` command only after you confirmed that path are created correctly and no problems with reading variables out of a source file, specially in case if you added your own options into the `collect-info-about-images.sh` file to gather, store and use even more information about images.

**Note:**

*   You must remove `echo` command in front of `mkdir` and `mv`.
*   Any output on screen slows script down, to make it even faster then disable verbose output for `mv` and `cp` by removing `-v` option.
*   To monitor that script is running you can use a CPU monitor utility and list folders in the destination directory. Or add `echo` command only in those script parts where it will minimize output, e.g. counter part for updating of a folder number to avoid a time endless feeling.
*   You can also replace `mv` with `cp` command for copying of files instead of moving them.

```
#!/bin/bash

NumberOfBaseDir="0"
SubDirNumber="0"
CountAll="0"
NumDir="0"

echo Creating destination.
Destination="./SortedImages"
echo mkdir -v "${Destination}" -p 
echo Created destination with status: $?

echo Your set of limitations.
SDN=50; echo Limit files in a subdir: $SDN
NBD=50; echo Limit subdirs in a file type named destination: $NBD

SourceDataFile="collect-info-about-images.txt"
echo Source file with a necessery data: $SourceDataFile

if [ 'XX' == 'XX'"$SourceDataFile" ] ; then 
 echo The '$SourceDataFile' variable is empty
 exit 1
else 
 if [ ! -f "$SourceDataFile" ]; then 
  echo The "$SourceDataFile" file doesn"'"t exist
  exit 2
 fi;
fi;

echo Populating an array from a file
ArrayFillCount=0;
while read line ; do
  tmpWb="${line/|H|*/}";
W="${tmpWb/*W|/}";
  tmpHb="${line/|Format|*/}";
H="${tmpHb/*|/}";

#if (( "$W" >= "800" )) && (( "$W" <=  "1000" )); then
#if (( "$H" >= "800" )) && (( "$H" <=  "1000" )); then
  ArrayOfFiles[$ArrayFillCount]="$line";
  ArrayFillCount=$((ArrayFillCount+1))
DupLimitKeeper[$W,$H]="0";
#fi;fi;

done < $SourceDataFile;
echo Done with extracting of necessary data about resolutions.

echo Starting loop of restoration
XX=${#ArrayOfFiles[@]}
while [  "${XX}" != "${CountAl}l" ] ; do
  preType=${ArrayOfFiles[$CountAll]/*"|Format|"/};
ImageType=${preType/|*/}
  preW=${ArrayOfFiles[$CountAll]/*"|W|"/};Width=${preW/|*/};preH=${ArrayOfFiles[$CountAll]/*"|H|"/} 
Height=${preH/|*/};
PathToFile=${ArrayOfFiles[$CountAll]/"|"*/}

DupLimitKeeper[Width,Height]=$((DupLimitKeeper[Width,Height]+1));

IfExist="${Destination}/${ImageType}${NumberOfBaseDir}/Resolution_${Width}x${Height}_DirN${SubDirNumber}"

if [ ! -d "$IfExist"  ];then 
  echo mkdir -vp "$IfExist"
NumDir=$((NumDir+1));
fi

## Creating a new numbered file type folders
if [ "${DupLimitKeeper[Width,Height]}" -gt $SDN ]; then 
  SubDirNumber=$((SubDirNumber+1));
  DupLimitKeeper[$Width,$Height]="0";
fi

## Adding a file number 
FileNameOnly="${PathToFile##*/}"
NewFileName="N${CountAll}C${FileNameOnly}"
#NewFileName="${FileNameOnly}"

## Creating a new sub-dir when limit of files in a sub-folder is reached
if [ $NumDir -gt $NBD ];then 
  NumberOfBaseDir=$((NumberOfBaseDir+1));
  NumDir="0";
fi
##
if [ -f "${PathToFile}" ];then
  echo mv -v "${PathToFile}" "$IfExist/$NewFileName";
# echo cp -v "${PathToFile}" "$IfExist/$NewFileName";
fi

CountAll=$((CountAll+1)) 
done
echo Total processed files: $CountAll

```

## See also

[sort photos into folders based on EXIF data](http://mikebeach.org/2011/12/10/bash-script-to-automatically-sort-photos-into-folders-based-on-exif-data-for-ubuntu-linux/)

Retrieved from "[https://wiki.archlinux.org/index.php?title=Sort_images_by_resolution&oldid=401679](https://wiki.archlinux.org/index.php?title=Sort_images_by_resolution&oldid=401679)"