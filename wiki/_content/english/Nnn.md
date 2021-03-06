Related articles

*   [File manager functionality](/index.php/File_manager_functionality "File manager functionality")
*   [Midnight Commander](/index.php/Midnight_Commander "Midnight Commander")
*   [ranger](/index.php/Ranger "Ranger")
*   [vifm](/index.php/Vifm "Vifm")

[nnn](https://github.com/jarun/nnn) is a portable terminal file manager written in C. It is easily extensible via its plugin system where you can add your own scripts alongside already available plugins. A [(neo)vim](https://github.com/mcchrish/nnn.vim) plugin is also available.

In addition to being a file manager, nnn is also a disk usage analyzer, a fuzzy app launcher, a batch file renamer and a file picker.

nnn supports instant *search-as-you-type* with regex (or simple string) filters and a *navigate-as-you-type* mode for continuous navigation in filter mode with directory auto-select. It supports contexts, bookmarks, multiple sorting options, SSHFS, batch operations on selections (a group of selected files) and a lot more.

Despite its capabilities, nnn is designed to be easy to use.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Installation](#Installation)
    *   [1.1 Usage](#Usage)
    *   [1.2 Configuration](#Configuration)
        *   [1.2.1 Get selected files in terminal](#Get_selected_files_in_terminal)
        *   [1.2.2 Indicate depth level within nnn shells](#Indicate_depth_level_within_nnn_shells)
        *   [1.2.3 cd on quit (Ctrl-G)](#cd_on_quit_(Ctrl-G))
        *   [1.2.4 Add your own plugins](#Add_your_own_plugins)
*   [2 See also](#See_also)

## Installation

nnn can be [installed](/index.php/Install "Install") with the [nnn](https://www.archlinux.org/packages/?name=nnn) package.

### Usage

nnn can be controlled with the vim-like characters `hjkl` or the `arrow keys`. Don't memorize keys. Arrows, `/` and `q` suffice. Press `?` for help on keyboard shortcuts anytime.

### Configuration

nnn is configured via environment variables, by editing `~/.bashrc`. For detailed information on these settings see the man page [nnn(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/nnn.1) as well as the [nnn wiki](https://github.com/jarun/nnn/wiki).

Here is an example configuration you can add to your `~/.bashrc`:

 `~/.bashrc` 
```
export NNN_BMS='d:~/Documents;u:/home/user/Cam Uploads;D:~/Downloads/'
export NNN_USE_EDITOR=1                                 # use the $EDITOR when opening text files
export NNN_SSHFS_OPTS="sshfs -o follow_symlinks"        # make sshfs follow symlinks on the remote
export NNN_CONTEXT_COLORS="2136"                        # use a different color for each context
export NNN_TRASH=1                                      # trash (needs trash-cli) instead of delete
```

The most important setting would be the `NNN_BMS` variable which lets you choose shortcuts to quickly jump to your bookmarked directories. They are reached with `b` followed by one of the letters that you have specified. In the example configuration hitting the keys `bD` would result in nnn jumping into `~/Downloads`. But all of these are optional, nnn will consistently behave the same on all of your machines.

#### Get selected files in terminal

To get a list of the files you have selected in `nnn` one could create the following alias:

 `~/.bashrc`  `alias ncp="cat ${XDG_CONFIG_HOME:-$HOME/.config}/nnn/.selection | tr '\0' '
'"` 

which later could be used to pipe the selected files to other tools.

#### Indicate depth level within nnn shells

If you use `!` to spawn a shell in the current directory, it could be nice to add:

 `~/.bashrc`  `[ -n "$NNNLVL" ] && PS1="N$NNNLVL $PS1"` 

To have your prompt indicate that you are within a shell that will return you to nnn when you are done.

This together with [#cd on quit (Ctrl-G)](#cd_on_quit_(Ctrl-G)) becomes a powerful combination.

#### cd on quit (Ctrl-G)

See the [nnn wiki](https://github.com/jarun/nnn/wiki/Basic-use-cases#configure-cd-on-quit).

#### Add your own plugins

You can run your own plugins by putting them in `${XDG_CONFIG_HOME:-$HOME/.config}/nnn/plugins`. For example you could create a executable shell script

 `${XDG_CONFIG_HOME:-$HOME/.config}/nnn/plugins/git-changes` 
```
#!/usr/bin/env sh
git log -p -- "$@"
```

And then trigger it by hitting `R` and selecting `git-changes` which will conveniently show the git log of changes to the particular file along with the code for a quick and easy review.

## See also

*   [nnn's official repository](https://github.com/jarun/nnn)
*   [Guides for additional configuration of nnn](https://github.com/jarun/nnn/wiki/Basic-use-cases)
*   [Introduction to nnn video](https://www.youtube.com/watch?v=U2n5aGqou9E)