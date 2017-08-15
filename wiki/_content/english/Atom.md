[Atom](https://atom.io/) is an open-source text editor developed by GitHub that is licensed under the MIT License. It is written predominantly in CoffeeScript and JavaScript and uses Node.js as its runtime environment. It is extensively extensible via use of over 5,000 available packages and 1,000 themes. It uses its own package manager for managing these packages and themes, apm.

## Contents

*   [1 Installation](#Installation)
*   [2 Packages](#Packages)
*   [3 Troubleshooting](#Troubleshooting)
    *   [3.1 Environment variables not sourced](#Environment_variables_not_sourced)
    *   [3.2 Unable to delete files](#Unable_to_delete_files)
    *   [3.3 Black window content on startup](#Black_window_content_on_startup)
    *   [3.4 Spell Checker not working](#Spell_Checker_not_working)

## Installation

The following packages provide Atom:

*   [atom](https://www.archlinux.org/packages/?name=atom)
*   [atom-editor-bin](https://aur.archlinux.org/packages/atom-editor-bin/)
*   [atom-editor-git](https://aur.archlinux.org/packages/atom-editor-git/)
*   [atom-editor-beta](https://aur.archlinux.org/packages/atom-editor-beta/)
*   [atom-editor-beta-bin](https://aur.archlinux.org/packages/atom-editor-beta-bin/)
*   *atom* from the unofficial [atom](/index.php/Unofficial_user_repositories#atom "Unofficial user repositories") repository.
    **Note:** Bugs regarding binary packages from the *atom* repository can be reported on [GitHub](https://github.com/tensor5/arch-atom/issues). Bugs regarding Atom itself should be reported upstream.

## Packages

Its packages can be installed from within Atom itself or from the command-line using the apm command. The correct syntax of apm is:

```
$ apm install *package_name1* *package_name2* *package_name3* ...

```

Several packages come preinstalled with Atom, notable packages that are not, include:

*   [build](https://atom.io/packages/build) which enables Atom to compile source code.
*   [git-plus](https://atom.io/packages/git-plus) which allows one to manage git repositories from within Atom.
*   [language-archlinux](https://atom.io/packages/language-archlinux) which provides syntax-highlighting for PKGBUILDs (if installed along with the [language-unix-shell](https://atom.io/packages/language-unix-shell) package) along with support for running several tests and other actions on PKGBUILDs without a terminal (including [makepkg](/index.php/Makepkg "Makepkg"), [namcap](/index.php/Namcap "Namcap"), *updpkgsums*, etc.).
*   [markdown-writer](https://atom.io/packages/markdown-writer) which turns Atom into an efficient Markdown writer.
*   [script](https://atom.io/packages/script) which enables Atom the ability to run scripts, based on file names.
*   [terminal-fusion](https://atom.io/packages/terminal-fusion) which adds an embedded terminal window to Atom.

## Troubleshooting

### Environment variables not sourced

You may experience some problems with packages using environments variables, like [go-plus](https://atom.io/packages/go-plus) (`$GOPATH not found`). Moreover, it only appears when atom is opened by your file manager. (Because this one is DBUS-spawned, thus it does not inherit variables defined in `.bashrc`). A solution is to make available your variables to DBUS-spawned processes, by following [Systemd/User#Environment variables](/index.php/Systemd/User#Environment_variables "Systemd/User").

More info on this issue in [Environment variables#Per user](/index.php/Environment_variables#Per_user "Environment variables").

### Unable to delete files

By default, [Electron](https://electron.atom.io/) apps use `gvfs-trash` to delete files. For users not using [GNOME](/index.php/GNOME "GNOME") the `ELECTRON_TRASH` environmental variable can be used to specify which trash utility should be used.

For example, for deleting files under [Plasma](/index.php/Plasma "Plasma"):

```
$ ELECTRON_TRASH=kioclient5 atom

```

At the time of writing, Electron supports `kioclient5`, `kioclient`, `trash-cli` and `gvfs-trash` (default). More info is available at this [Github pull request page](https://github.com/electron/electron/pull/7178).

### Black window content on startup

With some video devices, such as the one for [VirtualBox](/index.php/VirtualBox "VirtualBox") guests, Atom wont render the window content without GPU acceleration disabled by starting it with the `--disable-gpu` flag, or by editing `.atom/config.cson` and adding/changing the config parameter `useHardwareAcceleration: false` under the `editor` section.

### Spell Checker not working

Make sure you have hunspell installed with a [suitable dictionary pack](https://www.archlinux.org/packages/?sort=&q=hunspell&maintainer=&flagged=).