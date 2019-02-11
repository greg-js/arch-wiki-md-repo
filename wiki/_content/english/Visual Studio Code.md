[Visual Studio Code](https://code.visualstudio.com/) is a cross-platform, free and open-source (licensed under the MIT License) text editor developed by Microsoft and written in JavaScript and TypeScript. It is built on the Electron framework and is extensible using extensions, which can be browsed [on the web](https://marketplace.visualstudio.com/VSCode) or from within the text editor itself. While the project is open-source, a proprietary build (licensed under an End-User License Agreement) is also provided by Microsoft. For an explanation of the mixed licensing, see [this GitHub comment](https://github.com/Microsoft/vscode/issues/60#issuecomment-161792005).

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Installation](#Installation)
*   [2 Usage](#Usage)
*   [3 Configuration](#Configuration)
    *   [3.1 Integrated Terminal](#Integrated_Terminal)
    *   [3.2 External Terminal](#External_Terminal)
*   [4 Troubleshooting](#Troubleshooting)
    *   [4.1 Global menu not working in KDE/Plasma](#Global_menu_not_working_in_KDE/Plasma)
    *   [4.2 Unable to move items to trash](#Unable_to_move_items_to_trash)

## Installation

The following packages provide VSCode:

*   [code](https://www.archlinux.org/packages/?name=code) (open-source release)
*   [visual-studio-code-bin](https://aur.archlinux.org/packages/visual-studio-code-bin/) (Microsoft-branded release)
*   [code-git](https://aur.archlinux.org/packages/code-git/) (in-development open-source version)

## Usage

Run `code` to start the application (or `code-git` when using [code-git](https://aur.archlinux.org/packages/code-git/)).

If for any reason you wish to launch multiple instances of Visual Studio Code, the `-n` flag can be used.

## Configuration

[code](https://www.archlinux.org/packages/?name=code) stores settings in `~/.config/Code - OSS/User/settings.json`.

[visual-studio-code-bin](https://aur.archlinux.org/packages/visual-studio-code-bin/) stores settings in `~/.config/Code/User/settings.json`.

### Integrated Terminal

*View > Integrated Terminal* or `Ctrl + `` opens up an integrated terminal. By default, [Bash](/index.php/Bash "Bash") is used with no additional arguments, although this can be changed. `terminal.integrated.shell.linux` sets the default shell to be used and `terminal.integrated.shellArgs.linux` sets the arguments to be passed to the shell.

Example:

 `~/.config/Code/User/settings.json` 
```
"terminal.integrated.shell.linux": "/usr/bin/fish",
"terminal.integrated.shellArgs.linux": ["-l","-d 3"]

```

### External Terminal

If you are using **Terminator** as default terminal for Arch and you have an error on Visual Studio Code: `Unable to launch debugger worker process (vsdbg) through the terminal. spawn truecolor ENOENT`, you can change the terminal that will be used by Visual Studio to another terminal (eg gnome-terminal).

`"terminal.external.linuxExec": "Yours alternative terminal"` sets the default terminal to be used for exec debug.

Example:

 `~/.config/Code/User/settings.json` 
```
"terminal.external.linuxExec": "gnome-terminal"

```

## Troubleshooting

### Global menu not working in KDE/Plasma

Visual Studio Code uses DBus to pass the menu to Plasma, try installing [libdbusmenu-glib](https://www.archlinux.org/packages/?name=libdbusmenu-glib)

### Unable to move items to trash

By default, [Electron](https://electron.atom.io/) apps use `gvfs-trash` to delete files. This command is [deprecated and no longer exists](https://github.com/electron/electron/issues/15011), so the `ELECTRON_TRASH` environment variable must be used instead to specify which trash utility should be used.

For example, for deleting files under [Plasma](/index.php/Plasma "Plasma"):

```
$ ELECTRON_TRASH=kioclient5 code

```

At the time of writing, Electron supports `kioclient5`, `kioclient`, `trash-cli`, `gio` and `gvfs-trash` (default). More info is available at this [Github pull request page](https://github.com/electron/electron/pull/7178).