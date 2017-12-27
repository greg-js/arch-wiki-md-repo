**Visual Studio Code** (**VSCode**) is a cross-platform, free and open-source (licensed under the MIT License) text editor developed by Microsoft and written in JavaScript and TypeScript. It is built on the Electron framework and is extensible using extensions, which can be browsed from within the text editor itself (via its extension gallery) or from [https://marketplace.visualstudio.com/VSCode](https://marketplace.visualstudio.com/VSCode). While open-source, a proprietary build (licensed under an End-User License Agreement) provided by Microsoft is available and used as the basis for the [visual-studio-code-bin](https://aur.archlinux.org/packages/visual-studio-code-bin/) AUR package (for an explanation of the mixed licensing, see this GitHub [comment](https://github.com/Microsoft/vscode/issues/60#issuecomment-161792005)).

## Contents

*   [1 Installation](#Installation)
    *   [1.1 Debugging C#](#Debugging_C.23)
*   [2 Usage](#Usage)
*   [3 Configuration](#Configuration)
    *   [3.1 Integrated Terminal](#Integrated_Terminal)
    *   [3.2 External Terminal](#External_Terminal)

## Installation

The following packages provide VSCode:

*   [visual-studio-code-bin](https://aur.archlinux.org/packages/visual-studio-code-bin/)
*   [code](https://aur.archlinux.org/packages/code/)
*   [code-git](https://aur.archlinux.org/packages/code-git/)

### Debugging C#

If you want to debug C# code install [icu55](https://aur.archlinux.org/packages/icu55/) otherwise you will end up with a 'Debug adapter process has terminated unexpectedly' error

## Usage

Run `code`.

If for any reason you wish to launch multiple instances of Visual Studio Code, the `-n` flag can be used.

## Configuration

Visual Studio Code settings are stored in `~/.config/Code/User/settings.json`.

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