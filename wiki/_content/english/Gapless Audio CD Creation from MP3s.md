## Contents

*   [1 Introduction](#Introduction)
*   [2 Setup](#Setup)
*   [3 Decode the MP3s](#Decode_the_MP3s)
*   [4 Create a Table of Contents file](#Create_a_Table_of_Contents_file)
*   [5 Burn](#Burn)

## Introduction

Some albums are meant to be played without any silent gap between tracks -- especially live albums. Furthermore, when you copy a regular album that has gaps, the ripped audio files will actually include this gap at the end of each track -- to burn these tracks with a gap will actually increase the length of silence between tracks. Therefore, in almost all cases, you are better off burning all your CD backups gaplessly.

Here's an easy way to burn a gapless audio CD from the shell using cdrdao.

## Setup

[Install](/index.php/Install "Install") the [lame](https://www.archlinux.org/packages/?name=lame) and [cdrdao](https://www.archlinux.org/packages/?name=cdrdao) packages.

Optional: Let's configure cdrdao to use our CD burner. Open up `/etc/cdrdao.conf` (as root), and enter the /dev entry for your burner in this format:

```
write_device: "/dev/cdrw"

```

## Decode the MP3s

First of all, copy all the songs you want on the CD to a folder. If necessary, rename them to reflect the order you want the tracks to be laid out (such as 01.mp3, 02.mp3, etc). Now we're going to decode all the mp3s into uncompressed wav files. Take note that a full album can take up more than 800MB in wav files alone.

```
mkdir wav
for file in *.mp3 ; do
   lame --decode "$file" "wav/${file%.mp3}.wav" ;
done

```

## Create a Table of Contents file

Once finished, let's make a Table of Contents file that describes the layout of the CD.

```
cd wav
{
  echo "CD_DA"
  for file in *.wav ; do
    echo "TRACK AUDIO"
    echo "FILE \"$file\" 0"
  done
} > toc

```

Optionally, if you would like to insert a 2-second gap between certain tracks, you can edit the toc file and insert this line between the TRACK AUDIO and FILE lines for that track:

```
PREGAP 00:02:00

```

Of course, you can change the gap length to any time you desire.

## Burn

Finally, all we have to do is burn the CD.

```
cdrdao write toc

```

Some people prefer to burn audio CDs at a low speed for higher quality. Here's an example for burning at 8x:

```
cdrdao write --speed 8 toc

```