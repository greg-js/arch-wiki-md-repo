[nnn](https://github.com/jarun/nnn) is a very fast and minimalistic file manager that runs in your terminal. It is a excellent choice if you need a file manager on multiple machines, as it is highly portable and doesn't require exotic dependencies. Even though it is minimalistic it still offers a full experience of a file manager and it is easily extensible via its plugin system where you can add your own scripts.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Installation](#Installation)
    *   [1.1 Usage](#Usage)
    *   [1.2 Configuration](#Configuration)
        *   [1.2.1 cd on quit (CTRL-G)](#cd_on_quit_(CTRL-G))
*   [2 See also](#See_also)

## Installation

nnn can be [installed](/index.php/Install "Install") with the [nnn](https://www.archlinux.org/packages/?name=nnn) package.

### Usage

nnn can be controlled with the vim-like characters `hjkl` or the `arrow keys`. Don't memorize keys. Arrows, `/` and `q` suffice. Press `?` for help on keyboard shortcuts anytime.

### Configuration

nnn is configured via environment variables, by editing `~/.bashrc`. For detailed information on these settings see the included, well-documented man page `man nnn` as well as the [additional configurations](https://github.com/jarun/nnn/wiki/hacking-nnn) on the nnn wiki.

Here is a exmaple configuration you can add to you `~/.bashrc`:

 `~/.bashrc` 
```
export NNN_BMS='d:~/Documents;u:/home/user/Cam Uploads;D:~/Downloads/'
export NNN_USE_EDITOR=1                                 # Use the $EDITOR when opening text files
export NNN_NO_AUTOSELECT=1                              # Do not auto select in navigate-as-you-type-mode
export NNN_NOTE="$HOME/mynotes"                         # If you already have your own notebook, 
export NNN_OPS_PROG=1                                   # If you have installed advcp from the AUR. Giving you progress bars for mv and cp
export NNN_SSHFS_OPTS="sshfs -o follow_symlinks"        # make sshfs follow symlinks on the remote
alias ncp="cat ~/.config/nnn/.selection
```

The most important setting would be the `NNN_BMS` variable which lets you choose shortcuts to quickly jump to your bookmarked directories. By default they are reached with `<leader-key>` which is set to `,` (a comma). In the example configuration hitting the keys: `,D` would result in nnn jumping into `~/Downloads`. But all of these are optional, nnn will consistently behave the same on all of your machines.

##### cd on quit (CTRL-G)

To exit nnn and cd to the current working directory, you could add the following to your `~/.bashrc`.

**Note:** You can find similar scripts for various shells [here](https://github.com/jarun/nnn/tree/master/misc/quitcd).
 `~/.bashrc` 
```
n()
{
    export NNN_TMPFILE=${XDG_CONFIG_HOME:-$HOME/.config}/nnn/.lastd

    nnn "$@"

    if [ -f $NNN_TMPFILE ]; then
            . $NNN_TMPFILE
            rm -f $NNN_TMPFILE > /dev/null
    fi
}

```

And then start another terminal or run:

 `source ~/.bashrc` 

This will cause your shell to reload the `~/.bashrc`.

From now on you can run nnn as:

 `$ n` 

Which will correctly handle CTRL-G upon exiting nnn.

## See also

*   [nnn's official repository](https://github.com/jarun/nnn)
*   [Guides for additional configuration of nnn](https://github.com/jarun/nnn/wiki/hacking-nnn)
*   [Introduction to nnn video](https://www.youtube.com/watch?v=U2n5aGqou9E)