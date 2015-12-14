# Demlo

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

[Demlo](http://ambrevar.bitbucket.org/demlo/) is a batch music tagger and library organizer powered by Lua and FFmpeg. It supports transcoding, case checking, cue sheets, online tagging with MusicBrainz, manual tag editing with you favorite editor, cover downloading and processing, and more.

## Contents

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
*   [3 Scripts](#Scripts)
*   [4 Usage](#Usage)
*   [5 See also](#See_also)

## Installation

[Install](/index.php/Install "Install") the [demlo](https://aur.archlinux.org/packages/demlo/)<sup><small>AUR</small></sup> package from the [AUR](/index.php/AUR "AUR").

## Configuration

The package provides a configuration sample. It is a good idea to start from there:

```
 $ install -Dm644 /usr/share/demlo/demlorc -t ~/.config/demlo

```

## Scripts

Demlo is bundled with some official scripts you are free to use.

If you want to write a temporary script (for instance a script that makes sense for one album only), you can create a script in the local folder, call it from command line, then remove it.

For more persistent user scripts, you can store them in Demlo's configuration folder.

You can find some inspiration as for the configuration:

```
 $ install -Dm644 /usr/share/demlo/scripts/tag.lua -t ~/.config/demlo/scripts/

```

If two scripts have the same name and are not specified by their full path in the scripts option, then the user script takes precedence.

## Usage

Run Demlo over a set of file to preview then changes:

```
 $ demlo *.ogg album/ other-album/*.flac

```

Set the script chain to change the result:

```
 $ demlo -s 'tag ./my-script.lua format' <input-files>

```

If you need fine-grained tuning, you can run Lua commands before and after the script chain from command line:

```
 $ demlo -e 'o.artist="John Doe";o.disc=output.filename:match("Disc (%d+)")' -E 'output.format=ogg' <input-files>

```

To process the files, use the `-p` parameter. Demlo will use all available cores by default. You can restrict it:

```
 $ demlo --cores 2 -p <input-files>

```

If you want to edit tags or properties manually (in case scripts would not be able to correct them automatically), you can export the changes to an index file:

```
 $ demlo -G <some-tuning> <input-files> >> ./index.json

```

You can stack different output to the same index file, Demlo does not mind. You can edit this file with your favorite editor. To apply the changes, call demlo over the desired set of files with the `-i,--index` option. The script chain can still be run, or totally disabled if you do not want to perform any additional change.

```
 $ demlo -i ./index.lua -s ' ' -E 'o.artist,o.album_artist=o.album_artist,artist' <input-files>

```

Index files can be used to interface Demlo with other programs, both as input and output.

See `demlo -h` and the demlo(1) man page.

## See also

*   [Arch Linux forum thread](https://bbs.archlinux.org/viewtopic.php?id=186890)
*   [Development page](https://bitbucket.org/ambrevar/demlo)

Retrieved from "[https://wiki.archlinux.org/index.php?title=Demlo&oldid=412062](https://wiki.archlinux.org/index.php?title=Demlo&oldid=412062)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [Multimedia](/index.php/Category:Multimedia "Category:Multimedia")