## Introduction

Here describes about how you can restore normal names for the most of a recovered tar.gz archives by [photorec](/index.php/File_recovery#Testdisk_and_PhotoRec "File recovery"). First you need to create a file with a more detailed information about files, see: [post recovery tasks](/index.php/File_recovery#Creating_a_database_with_more_details_about_files "File recovery"). Restored tar.gz files with photorec might look like `./recup_dir.996/f864593944_wmmaiload-1.0.5.tar.gz` or `./recup_dir.996/f864589184.tar.gz`.

The *tar.gz* archive includes inside a *tar* archive whose name is used to restore filename of the *tar.gz* if it is possible or name of a first folder/file from inside of the archive.

The ways that might be used to restore the name of the tar.gz archives:

*   From part of a name by cutting everything before '_' in files with created by photorec with pattern: f864593944_wmmaiload-1.0.5.tar.gz
*   From name of a tar inside of the tar.gz archive.
*   From the name of the folder inside it. In many cases it usually compressed a whole folder that might be similar to the archive name.

**Note:** This script restores only by separating original name from the photorec generated name or use a name of the first folder or file inside of the archive.
To restore all of the files that contain only the original name as part of the generated you can download the *restore-orignames-only.sh* script from the [SourceForge](https://sourceforge.net/projects/postrecoverytasksphotorec/) website, but it will add the *Duplicate123* (123 is number of a processed file) to files with the same name in the destination directory.

## Collect info data about tar.gz

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

## Restore filenames

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