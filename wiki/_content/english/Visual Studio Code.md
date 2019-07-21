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
    *   [4.3 Unable to debug C#](#Unable_to_debug_C#)
    *   [4.4 Error from OmniSharp that MSBuild cannot be located](#Error_from_OmniSharp_that_MSBuild_cannot_be_located)

## Installation

The following packages provide VSCode:

*   [code](https://www.archlinux.org/packages/?name=code) (open-source release)
*   [visual-studio-code-bin](https://aur.archlinux.org/packages/visual-studio-code-bin/) (Microsoft-branded release)
*   [code-git](https://aur.archlinux.org/packages/code-git/) (in-development open-source version)
*   [vscodium-bin](https://aur.archlinux.org/packages/vscodium-bin/) (another open-source version with a community-driven default configuration)

The Microsoft [ptvsd](https://github.com/microsoft/ptvsd) (Python Tools for Visual Studio Debug) server/module is available at [python-ptvsd](https://aur.archlinux.org/packages/python-ptvsd/).

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

By default, [Electron](https://electron.atom.io/) apps use `gvfs-trash` to delete files. This command is [deprecated and no longer exists](https://github.com/electron/electron/issues/15011), so the `ELECTRON_TRASH` [environment variable](/index.php/Environment_variable "Environment variable") must be used instead to specify which trash utility should be used.

For example, for deleting files under [Plasma](/index.php/Plasma "Plasma"):

```
$ ELECTRON_TRASH=kioclient5 code

```

At the time of writing, Electron supports `kioclient5`, `kioclient`, `trash-cli`, `gio` and `gvfs-trash` (default). More info is available at this [Github pull request page](https://github.com/electron/electron/pull/7178).

### Unable to debug C#

If you want to debug C#[.NET](/index.php/.NET_Core ".NET Core") (using the [OmniSharp extension](http://www.omnisharp.net)) then you need to install the Microsoft branded release (from the AUR). This is apparently because the .NET Core debugger is only licensed to be used with official Microsoft products - see [https://github.com/OmniSharp/omnisharp-vscode/issues/1431#issuecomment-297578930](https://github.com/OmniSharp/omnisharp-vscode/issues/1431#issuecomment-297578930)

Using the the open-source package, debugging fails fairly quietly. The debug console will just show the initial message and nothing more:

```
You may only use the Microsoft .NET Core Debugger (vsdbg) with
Visual Studio Code, Visual Studio or Visual Studio for Mac software
to help you develop and test your applications.
```

But in another way, you can use [netcoredbg](https://github.com/Samsung/netcoredbg),[netcoredbg](https://aur.archlinux.org/packages/netcoredbg/)

### Error from OmniSharp that MSBuild cannot be located

It's noted in the [OmniSharp introduction](https://github.com/OmniSharp/omnisharp-roslyn#introduction) that Arch Linux users should install the [msbuild-stable](https://aur.archlinux.org/packages/msbuild-stable/) package. Without it, you might get an error like:

 `OmniSharp Log` 
```
[info]: OmniSharp.MSBuild.Discovery.MSBuildLocator
        Registered MSBuild instance: StandAlone 15.0 - "~/.vscode/extensions/ms-vscode.csharp-1.18.0/.omnisharp/1.32.11/omnisharp/msbuild/15.0/Bin"
            MSBuildExtensionsPath = /usr/lib/mono/xbuild
            BypassFrameworkInstallChecks = true
            CscToolPath = ~/.vscode/extensions/ms-vscode.csharp-1.18.0/.omnisharp/1.32.11/omnisharp/msbuild/15.0/Bin/Roslyn
            CscToolExe = csc.exe
            MSBuildToolsPath = ~/.vscode/extensions/ms-vscode.csharp-1.18.0/.omnisharp/1.32.11/omnisharp/msbuild/15.0/Bin
            TargetFrameworkRootPath = /usr/lib/mono/xbuild-frameworks
System.TypeLoadException: Could not load type of field 'OmniSharp.MSBuild.ProjectManager:_queue' (13) due to: Could not load file or assembly 'System.Threading.Tasks.Dataflow, Version=4.5.24.0, Culture=neutral, PublicKeyToken=b03f5f7f11d50a3a' or one of its dependencies.
...
```

You might be able to build anyway (possibly depending whether you have [mono](https://www.archlinux.org/packages/?name=mono) installed too)