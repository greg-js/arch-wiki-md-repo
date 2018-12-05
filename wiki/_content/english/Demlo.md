[Demlo](http://ambrevar.bitbucket.io/demlo/) is a batch music tagger and library organizer powered by Lua and [FFmpeg](/index.php/FFmpeg "FFmpeg"). It supports transcoding, case checking, cue sheets, online tagging with MusicBrainz, manual tag editing with you favorite editor, cover downloading and processing, and more.

## Contents

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
*   [3 Scripts](#Scripts)
*   [4 Usage](#Usage)
*   [5 See also](#See_also)

## Installation

[Install](/index.php/Install "Install") the [demlo](https://aur.archlinux.org/packages/demlo/) package from the [AUR](/index.php/AUR "AUR").

## Configuration

The package provides a configuration sample. It is a good idea to start from there:

```
 $ install -Dm644 /usr/share/demlo/demlorc -t ~/.config/demlo

```

## Scripts

Demlo runs a chain of Lua scripts of the files passed as arguments. You can select which scripts from the config file or at run-time.

Each script can access an `input` table and modify an `output` table with information such as the path, tags, covers and encoding properties.

Demlo comes with its set of official scripts to choose from.

If you want to write a temporary script (for instance a script that makes sense for one album only), you can create a script in the local folder, call it from command line, then remove it.

For more persistent user scripts, you can store them in Demlo's configuration folder.

You can derive your scripts from the official ones as for the configuration:

```
 $ install -Dm644 /usr/share/demlo/scripts/tag.lua -t ~/.config/demlo/scripts/

```

The user script folder has precedence over the system script folder: if two scripts share the same basename, the user script will be used.

## Usage

By default Demlo only previews changes. Use the `-p` commandline flag to confirm processing.

See `demlo -h` for all options and parameters, the [demlo manual](https://godoc.org/gitlab.com/ambrevar/demlo) is also available.

Usage examples:

Run Demlo over a set of file to preview the changes:

```
 $ demlo *.ogg *album*/ *other-album*/*.flac

```

Set the script chain to change the result:

```
 $ demlo -s tag -s ./my-script.lua -s encoding *input-files*

```

If you need fine-grained tuning, you can run Lua commands before and after the script chain from command line:

```
 $ demlo -pre 'o.artist="John Doe";o.disc=output.filename:match("Disc (\d+)")' -post 'output.format="ogg"' *input-files*

```

To process the files, use the `-p` parameter. Demlo uses all available cores by default. You can restrict it:

```
 $ demlo -cores 2 -p *input-files*

```

If you just want to fetch covers online:

```
 $ demlo -c -s cover -s 90-rmsrc -p *input-files*

```

If you want to edit tags or properties manually (in case scripts would not be able to fix them automatically), you can export the changes to an index file:

```
 $ demlo *some-tuning* *input-files* >> ./index.json

```

You can stack different output to the same index file, Demlo does not mind. You can edit this file with your favorite editor. To apply the changes, call Demlo over the desired set of files with the `-i` option. Scripts can still be called or they can be left out if you do not want to perform any additional change.

```
 $ demlo -i ./index.json -r '' -post 'o.artist,o.album_artist=o.album_artist,artist' *input-files*

```

Index files can be used to interface Demlo with other programs, both as input and output.

## See also

*   [Arch Linux forum thread](https://bbs.archlinux.org/viewtopic.php?id=186890)
*   [Development page](https://github.com/Ambrevar/demlo)