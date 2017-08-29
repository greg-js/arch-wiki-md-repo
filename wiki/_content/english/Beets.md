[Beets](http://beets.radbox.org/) is a music tagger and library organizer using the [MusicBrainz](http://musicbrainz.org/) database.

## Contents

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
*   [3 Usage](#Usage)
    *   [3.1 Add music](#Add_music)
    *   [3.2 List music](#List_music)
    *   [3.3 Remove music](#Remove_music)
*   [4 Tips and tricks](#Tips_and_tricks)
    *   [4.1 Enabling tab-completion in bash](#Enabling_tab-completion_in_bash)

## Installation

[Install](/index.php/Install "Install") the [beets](https://www.archlinux.org/packages/?name=beets) package or [beets-git](https://aur.archlinux.org/packages/beets-git/) from the [AUR](/index.php/AUR "AUR") for the development version.

## Configuration

**Tip:** Beets provides a command for configuration manipulations. To edit the configuration file, run `beet config -e`. It will be opened with the text editor specified in the [environment variable](/index.php/Environment_variable "Environment variable") `EDITOR`.

User configuration is done in `~/.config/beets/config.yaml` using [YAML](https://en.wikipedia.org/wiki/YAML "wikipedia:YAML") syntax. For example:

 `~/.config/beets/config.yaml` 
```
directory: ~/Music            # The default library root directory.
library: ~/Music/library.db   # The default library database file to use.

```

## Usage

### Add music

Add music to your library and attempt to fix tags:

```
$ beet import <path>

```

Add the single track without an album:

```
$ beet import -s <path>

```

### List music

List all music in your library:

```
$ beet ls

```

List all albums in your library:

```
$ beet ls -a

```

### Remove music

**Tip:** If you remove music from your filesystem or do any changes to the files without using `beet`, do not forget to run `beet upd` to update your library database.

Remove track(s) from your library:

```
$ beet rm <part of name>

```

Remove album(s) from your library:

```
$ beet rm -a <part of name>

```

## Tips and tricks

### Enabling tab-completion in bash

Beets includes support for Bash shell [command completion](/index.php/Bash#Tab_completion "Bash"). To enable completion, put the following line into your `.bashrc`:

 `~/.bashrc`  `eval "$(beet completion)"` 

You will also need to [install](/index.php/Install "Install") [bash-completion](https://www.archlinux.org/packages/?name=bash-completion) for this to work.