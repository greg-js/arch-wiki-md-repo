# Gapless Audio CD Creation from MP3s

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

[![Tango-two-arrows.png](/images/7/72/Tango-two-arrows.png)](/index.php/File:Tango-two-arrows.png)

[![Tango-two-arrows.png](/images/7/72/Tango-two-arrows.png)](/index.php/File:Tango-two-arrows.png)

**This article or section is a candidate for merging with [Optical_disc_drive#Burning_an_audio_CD](/index.php/Optical_disc_drive#Burning_an_audio_CD "Optical disc drive").**

**Notes:** please use the second argument of the template to provide more detailed indications. (Discuss in [Talk:Gapless Audio CD Creation from MP3s#](https://wiki.archlinux.org/index.php/Talk:Gapless_Audio_CD_Creation_from_MP3s))

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

We'll be using a few programs for this.

```
pacman -S lame cdrdao

```

Optional: Let's configure cdrdao to use our CD burner. Open up `/etc/cdrdao.conf` (as root), and enter the /dev entry for your burner in this format:

```
write_device: "/dev/cdrw"

```

## Decode the MP3s

First of all, copy all the songs you want on the CD to a folder. If necessary, rename them to reflect the order you want the tracks to be laid out (such as 01.mp3, 02.mp3, etc). Now we're going to decode all the mp3s into uncompressed wav files. Take note that a full album can take up more than 800MB in wav files alone.

```
mkdir wav
for file in *.mp3 ; do
   lame --decode "$file" "wav/$file.wav" ;
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

Retrieved from "[https://wiki.archlinux.org/index.php?title=Gapless_Audio_CD_Creation_from_MP3s&oldid=389799](https://wiki.archlinux.org/index.php?title=Gapless_Audio_CD_Creation_from_MP3s&oldid=389799)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [Multimedia](/index.php/Category:Multimedia "Category:Multimedia")

Hidden category:

*   [Pages or sections flagged with Template:Merge](/index.php/Category:Pages_or_sections_flagged_with_Template:Merge "Category:Pages or sections flagged with Template:Merge")