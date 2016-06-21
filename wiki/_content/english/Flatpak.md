From [Wikipedia](https://en.wikipedia.org/wiki/flatpak "wikipedia:flatpak"): "[Flatpak](http://flatpak.org), named xdg-app until May 2016, is a system for application virtualization for Linux desktop computer environments."

## Contents

*   [1 Installation](#Installation)
*   [2 Managing repositories](#Managing_repositories)
    *   [2.1 Add a repository](#Add_a_repository)
    *   [2.2 Delete a repository](#Delete_a_repository)
*   [3 Managing runtimes and applications](#Managing_runtimes_and_applications)
    *   [3.1 List available runtimes and applications](#List_available_runtimes_and_applications)
    *   [3.2 Install a runtime or application](#Install_a_runtime_or_application)
    *   [3.3 List installed runtimes and applications](#List_installed_runtimes_and_applications)
    *   [3.4 Update a runtime or application](#Update_a_runtime_or_application)
    *   [3.5 Uninstall a runtime or application](#Uninstall_a_runtime_or_application)
*   [4 See also](#See_also)

## Installation

[Install](/index.php/Install "Install") the [flatpak](https://www.archlinux.org/packages/?name=flatpak) or [flatpak-git](https://aur.archlinux.org/packages/flatpak-git/) package.

## Managing repositories

### Add a repository

To add a remote flatpak repository do:

```
$ flatpak remote-add *name* *location*

```

where *name* is the name for the new remote, and *location* is the path or URL for the repository.

### Delete a repository

To delete a remote flatpak repository do:

```
$ flatpak remote-delete *name*

```

where *name* is the name of the remote repository to be deleted.

## Managing runtimes and applications

### List available runtimes and applications

To list available runtimes and applications in a remote repository named *remote* do:

```
$ flatpak remote-ls *remote*

```

### Install a runtime or application

To install a runtime or application do:

```
$ flatpak install *remote* *name*

```

where *remote* is the name of the remote repository, and *name* is the name of the application or runtime to install.

### List installed runtimes and applications

To list installed runtimes and applications do:

```
$ flatpak ls

```

### Update a runtime or application

To update a runtime or application named *name* do:

```
$ flatpak update *name*

```

### Uninstall a runtime or application

To uninstall a runtime or application named *name* do:

```
$ flatpak uninstall *name*

```

## See also

*   [Official website](http://flatpak.org)
*   [Official Github wiki](https://github.com/flatpak/flatpak/wiki)
*   [Gnome SandboxedApps](https://wiki.gnome.org/Projects/SandboxedApps)