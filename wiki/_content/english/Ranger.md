[ranger](http://ranger.nongnu.org/) is a text-based file manager written in Python. Directories are displayed in one pane with three columns. Moving between them is accomplished with keystrokes, bookmarks, the mouse or the command history. File previews and directory contents show automatically for the current selection.

Features include: vi-style key bindings, bookmarks, selections, tagging, tabs, command history, the ability to make symbolic links, several console modes, and a task view. *ranger* has customizable commands and key bindings, including bindings to external scripts. The closest competitor is [Vifm](/index.php/Vifm "Vifm"), which has two panes and vi-style key bindings, but fewer features overall.

## Contents

*   [1 Installation](#Installation)
*   [2 Usage](#Usage)
*   [3 Configuration](#Configuration)
    *   [3.1 Defining commands](#Defining_commands)
    *   [3.2 Color schemes](#Color_schemes)
    *   [3.3 File association](#File_association)
*   [4 Tips and tricks](#Tips_and_tricks)
    *   [4.1 Archives](#Archives)
        *   [4.1.1 Archive extraction](#Archive_extraction)
        *   [4.1.2 Compression](#Compression)
    *   [4.2 External drives](#External_drives)
    *   [4.3 Image mounting](#Image_mounting)
    *   [4.4 New tab in current folder](#New_tab_in_current_folder)
    *   [4.5 PDF file preview](#PDF_file_preview)
    *   [4.6 Shell tips](#Shell_tips)
        *   [4.6.1 Synchronize path](#Synchronize_path)
        *   [4.6.2 Start a shell from ranger](#Start_a_shell_from_ranger)
            *   [4.6.2.1 A simpler solution](#A_simpler_solution)
        *   [4.6.3 Preventing nested ranger instances](#Preventing_nested_ranger_instances)
*   [5 Troubleshooting](#Troubleshooting)
    *   [5.1 Artifacts in image preview](#Artifacts_in_image_preview)
*   [6 See also](#See_also)

## Installation

[Install](/index.php/Install "Install") the [ranger](https://www.archlinux.org/packages/?name=ranger) package, or [ranger-git](https://aur.archlinux.org/packages/ranger-git/) for the development version.

## Usage

To start ranger, launch a [terminal](/index.php/List_of_applications#Terminal_emulators "List of applications") and run `ranger`.

<caption></caption>
| Key | Command |
| `?` | Open the manual or list keybindings, commands and settings |
| `l`, `Enter` | Launch files |

## Configuration

After startup, *ranger* creates a directory `~/.config/ranger`. To copy the default configuration to this directory issue the following command:

```
ranger --copy-config=all

```

*   `rc.conf` - startup commands and key bindings
*   `commands.py` - commands which are launched with `:`
*   `rifle.conf` - applications used when a given type of file is launched.

`rc.conf` only needs to include changes from the default file as both are loaded. For `commands.py`, if you do not include the whole file, put this line at the top:

```
from ranger.api.commands import *

```

To add a keybind that moves files to a created directory `~/.Trash/` with `DD`, add to `~/.config/ranger/rc.conf`:

```
map DD shell mv -t /home/${USER}/.Trash %s

```

See [man ranger](http://ranger.nongnu.org/ranger.1.html) for general configuration.

### Defining commands

Continuing the above example, add the following entry to `~/.config/ranger/commands.py` to empty the trash directory `~/.Trash`.

```
class empty(Command):
    """:empty

    Empties the trash directory ~/.Trash
    """

    def execute(self):
        self.fm.run("rm -rf /home/myname/.Trash/{*,.[^.]*}")

```

To use it, type `:empty` and `Enter` with tab completion as desired.

**Warning:** `[^.]` is an essential part of the above command. Without it, all files and directories of the form `..*` will be deleted, wiping out everything in your home directory.

### Color schemes

Ranger comes with three color schemes: `default`, `jungle` and `snow`. You can change your color scheme using:

```
set colorscheme *scheme*

```

Custom color schemes can be placed in `~/.config/ranger/colorschemes`.

### File association

Ranger uses its own file opener called `rifle`. It's configured in `~/.config/ranger/rifle.conf`. Run `ranger --copy-config=rifle` if it does not exist. For example, the following line makes [kile](https://www.archlinux.org/packages/?name=kile) the default program for tex files:

```
ext tex = kile "$@"

```

To open all files with [xdg-utils](https://www.archlinux.org/packages/?name=xdg-utils):

```
has xdg-open, flag f = xdg-open "$1"

```

## Tips and tricks

### Archives

These commands use [atool](https://www.archlinux.org/packages/?name=atool) to perform archive operations.

#### Archive extraction

The following command implements archive extraction by copying (yy) one or more archive files and then executing `:extracthere` on the desired directory.

```
import os
from ranger.core.loader import CommandLoader

class extracthere(Command):
    def execute(self):
        """ Extract copied files to current directory """
        copied_files = tuple(self.fm.copy_buffer)

        if not copied_files:
            return

        def refresh(_):
            cwd = self.fm.get_directory(original_path)
            cwd.load_content()

        one_file = copied_files[0]
        cwd = self.fm.thisdir
        original_path = cwd.path
        au_flags = ['-X', cwd.path]
        au_flags += self.line.split()[1:]
        au_flags += ['-e']

        self.fm.copy_buffer.clear()
        self.fm.cut_buffer = False
        if len(copied_files) == 1:
            descr = "extracting: " + os.path.basename(one_file.path)
        else:
            descr = "extracting files from: " + os.path.basename(one_file.dirname)
        obj = CommandLoader(args=['aunpack'] + au_flags \
                + [f.path for f in copied_files], descr=descr)

        obj.signal_bind('after', refresh)
        self.fm.loader.add(obj)

```

#### Compression

The following command allows the user to compress several files on the current directory by marking them and then calling `:compress *package name*`. It supports name suggestions by getting the basename of the current directory and appending several possibilities for the extension. You need to have [atool](https://www.archlinux.org/packages/?name=atool) installed. Otherwise you will see an error message when you create the archive.

```
import os
from ranger.core.loader import CommandLoader

class compress(Command):
    def execute(self):
        """ Compress marked files to current directory """
        cwd = self.fm.thisdir
        marked_files = cwd.get_selection()

        if not marked_files:
            return

        def refresh(_):
            cwd = self.fm.get_directory(original_path)
            cwd.load_content()

        original_path = cwd.path
        parts = self.line.split()
        au_flags = parts[1:]

        descr = "compressing files in: " + os.path.basename(parts[1])
        obj = CommandLoader(args=['apack'] + au_flags + \
                [os.path.relpath(f.path, cwd.path) for f in marked_files], descr=descr)

        obj.signal_bind('after', refresh)
        self.fm.loader.add(obj)

    def tab(self):
        """ Complete with current folder name """

        extension = ['.zip', '.tar.gz', '.rar', '.7z']
        return ['compress ' + os.path.basename(self.fm.thisdir.path) + ext for ext in extension]

```

### External drives

External drives can be automatically mounted with [udev](/index.php/Udev "Udev") or [udisks](/index.php/Udisks "Udisks"). Drives mounted under `/media` can be easily accessed by pressing `gm` (go, media).

### Image mounting

The following command assumes you are using [CDemu](/index.php/CDemu "CDemu") as your image mounter and some kind of system like [autofs](/index.php/Autofs "Autofs") which mounts the virtual drive to a specified location ('/media/virtualrom' in this case). **Do not forget to change mountpath to reflect your system settings**.

To mount an image (or images) to a cdemud virtual drive from ranger you select the image files and then type ':mount' on the console. The mounting may actually take some time depending on your setup (in mine it may take as long as one minute) so the command uses a custom loader that waits until the mount directory is mounted and then opens it on the background in tab 9.

```
import os, time
from ranger.core.loader import Loadable
from ranger.ext.signals import SignalDispatcher
from ranger.ext.shell_escape import *

class MountLoader(Loadable, SignalDispatcher):
    """
    Wait until a directory is mounted
    """
    def __init__(self, path):
        SignalDispatcher.__init__(self)
        descr = "Waiting for dir '" + path + "' to be mounted"
        Loadable.__init__(self, self.generate(), descr)
        self.path = path

    def generate(self):
        available = False
        while not available:
            try:
                if os.path.ismount(self.path):
                    available = True
            except:
                pass
            yield
            time.sleep(0.03)
        self.signal_emit('after')

class mount(Command):
    def execute(self):
        selected_files = self.fm.thisdir.get_selection()

        if not selected_files:
            return

        space = ' '
        self.fm.execute_command("cdemu -b system unload 0")
        self.fm.execute_command("cdemu -b system load 0 " + \
                space.join([shell_escape(f.path) for f in selected_files]))

        mountpath = "/media/virtualrom/"

        def mount_finished(path):
            currenttab = self.fm.current_tab
            self.fm.tab_open(9, mountpath)
            self.fm.tab_open(currenttab)

        obj = MountLoader(mountpath)
        obj.signal_bind('after', mount_finished)
        self.fm.loader.add(obj)

```

### New tab in current folder

You may have noticed there are two shortcuts for opening a new tab in home (`g``n` and `Ctrl+n`). Let us rebind `Ctrl+n`:

 `rc.conf` 
```
map <c-n>  eval fm.tab_new('%d')

```

### PDF file preview

You can preview PDF files in ranger by first converting the PDF file to an image. Ranger will store the image previews in `~/.cache/ranger/`.

First, ensure image preview is enabled:

 `~/.config/ranger/rc.conf` 
```
# Use one of the supported image preview protocols
set preview_images true

```

Ranger can preview images using, for example, [w3m](https://www.archlinux.org/packages/?name=w3m); see `~/.config/ranger/rc.conf` for all available preview methods.

Finally, add the following pdf preview command:

 `~/.config/ranger/scope.sh` 
```
# Image previews, if enabled in ranger.
if [ "$preview_images" = "True" ]; then
    case "$mimetype" in
        application/pdf)
             pdftoppm -jpeg -singlefile "$path" "${cached//.jpg}" && exit 6;;
    esac
fi

```

In this example the `pdftoppm` utility from [poppler](https://www.archlinux.org/packages/?name=poppler) is used to create the image preview. Other (usually slower) options are available, for example [ghostscript](https://www.archlinux.org/packages/?name=ghostscript) or [imagemagick](https://www.archlinux.org/packages/?name=imagemagick).

### Shell tips

#### Synchronize path

*ranger* provides a shell [function](/index.php/Bash/Functions "Bash/Functions") `/usr/share/doc/ranger/examples/bash_automatic_cd.sh`. Running `ranger-cd` instead of `ranger` will automatically *cd* to the last browsed folder.

If you launch ranger from a graphical launcher (such as `$TERMCMD -e ranger`, where TERMCMD is an X terminal), you cannot use `ranger-cd`. Create an executable script:

 `ranger-launcher.sh` 
```
#!/bin/sh
export RANGERCD=true
$TERMCMD

```

and add at the *very end* of your shell configuration:

 `.*shell*rc` 
```
$RANGERCD && unset RANGERCD && ranger-cd

```

This will launch `ranger-cd` only if the `RANGERCD` variable is set. It is important to unset this variable again, otherwise launching a subshell from this terminal will automatically relaunch `ranger`.

#### Start a shell from ranger

With the previous method you can switch to a shell in last browsed path simply by leaving ranger. However you may not want to quit ranger for several reasons (numerous opened tabs, copy in progress, etc.). You can start a shell from ranger (`S` by default) without losing your ranger session. Unfortunately, the shell will not switch to the current folder automatically. Again, this can be solved with an executable script:

 `shellcd` 
```
#!/bin/sh
export AUTOCD="$(realpath "$1")"

$SHELL

```

and - as before - add this to at the very end of your shell configuration:

 `shellrc` 
```
cd "$AUTOCD"

```

Now you can change your shell binding for ranger:

 `rc.conf` 
```
map S shell shellcd %d

```

Alternatively, you can make use of your shell history file if it has any. For instance, you could do this for [zsh](/index.php/Zsh#Dirstack "Zsh"):

 `shellcd` 
```
## Prepend argument to zsh dirstack.
BUF="$(realpath "$1")
$(grep -v "$(realpath "$1")" "$ZDIRS")"
echo "$BUF" > "$ZDIRS"

zsh

```

Change ZDIRS for your dirstack.

##### A simpler solution

 `rc.conf` 
```
map S shell bash -c "cd %d; bash"

```

This could probably be adapted to other shells as well. Instead of just running a shell (like the default config), this will run `cd` in a shell, then execute a interactive shell which will not immediately exit so that you can continue with what you wanted.

#### Preventing nested ranger instances

You can start a shell in the current directory with `S`, when you exit the shell you get back to your ranger instance.

When you however forget that you already are in a ranger shell and start ranger again you end up with ranger running a shell running ranger.

To prevent this you can create the following function in your [shell's startup file](/index.php/Autostarting#Shells "Autostarting"):

```
ranger() {
    if [ -z "$RANGER_LEVEL" ]; then
        /usr/bin/ranger "$@"
    else
        exit
    fi
}

```

## Troubleshooting

### Artifacts in image preview

Borderless columns may cause stripes in image previews. [[1]](https://bbs.linuxdistrocommunity.com/showthread.php?tid=1051) In `~/.config/ranger/rc.conf` set:

```
set draw_borders true

```

## See also

*   [BBS thread](https://bbs.archlinux.org/viewtopic.php?id=93025)
*   [DotShare.it configurations](http://dotshare.it/category/fms/ranger/)
*   [GitHub](https://github.com/hut/ranger)
*   [Installing and using ranger](https://www.digitalocean.com/community/tutorials/installing-and-using-ranger-a-terminal-file-manager-on-a-ubuntu-vps)
*   [Mailing list](https://lists.nongnu.org/mailman/listinfo/ranger-users)
*   [Ranger tutorial](https://bloerg.net/2012/10/17/ranger-file-manager.html)