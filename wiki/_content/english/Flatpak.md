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
    *   [3.6 Adding Flatpak .desktop files to your menu](#Adding_Flatpak_.desktop_files_to_your_menu)
*   [4 Creating a custom base runtime](#Creating_a_custom_base_runtime)
    *   [4.1 Creating apps with pacman](#Creating_apps_with_pacman)
*   [5 See also](#See_also)

## Installation

[Install](/index.php/Install "Install") the [flatpak](https://www.archlinux.org/packages/?name=flatpak) or [flatpak-git](https://aur.archlinux.org/packages/flatpak-git/) package.

If you want to have desktop integration using [portals](https://github.com/flatpak/flatpak/wiki/Portals) you can install the [xdg-desktop-portal-gtk](https://www.archlinux.org/packages/?name=xdg-desktop-portal-gtk) package.

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
$ flatpak list

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

### Adding Flatpak .desktop files to your menu

Flatpak expects window managers to respect the XDG_DATA_DIRS environment variable to discover applications. This may require restarting the session or the launcher may not support this. In such a case where you can edit the list of directories scanned, add these to it:

```
~/.local/share/flatpak/exports/applications
/var/lib/flatpak/exports/applications

```

This is known to be necessary in Awesome.

## Creating a custom base runtime

**Note:** You may want to use an untrusted, unprivileged user account for bundling untrusted software because the software is not sandboxed during app and runtime creation.

**Note:** When distributing bundles to others, you may be legally obliged to provide the source code of some of the bundled software upon request. You may want to use [ABS](/index.php/ABS "ABS") to build these packages from source.

You can create a custom Arch-based base runtime and base SDK for Flatpak using pacman. You can then use it for building and packaging applications. This is an alternative for personal use to the default `org.freedesktop.BasePlatform` and `org.freedesktop.BaseSdk` runtimes.

In addition to [flatpak](https://www.archlinux.org/packages/?name=flatpak), you need to have installed [fakeroot](https://www.archlinux.org/packages/?name=fakeroot) and for pacman hooks support also [fakechroot](https://www.archlinux.org/packages/?name=fakechroot).

First, start by creating a directory for building the runtime and possibly applications.

```
$ mkdir *myflatpakbuilddir*
$ cd *myflatpakbuilddir*

```

You can then prepare a directory for building the runtime base platform. The files subdirectory will contain what will later be the `/usr` directory in the sandbox. Therefore you will need to create symbolic links so the default `/usr/share` etc. from Arch can still be accessed at the usual path.

```
$ mkdir -p *myruntime*/files/var/lib/pacman
$ touch *myruntime*/files/.ref
$ ln -s /usr/usr/share *myruntime*/files/share
$ ln -s /usr/usr/include *myruntime*/files/include
$ ln -s /usr/usr/local *myruntime*/files/local

```

Make your host OS fonts available to the Arch runtime:

```
$ mkdir -p *myruntime*/files/usr/share/fonts
$ ln -s /run/host/fonts *myruntime*/files/usr/share/fonts/flatpakhostfonts

```

You need and may want to adapt your `pacman.conf` before installing packages to the runtime. Copy `/etc/pacman.conf` to your build directory and then make the following changes:

*   Remove the `CheckSpace` option so pacman will not complain about errors finding the root filesystem for checking disk space.
*   Remove any undesired custom repositories and `IgnorePkg`, `IgnoreGroup`, `NoUpgrade` and `NoExtract` settings that are needed only for the host system.

Now install the packages for the runtime.

```
$ fakechroot fakeroot pacman -Syu --root *myruntime*/files --dbpath *myruntime*/files/var/lib/pacman --config pacman.conf base
$ mv pacman.conf *myruntime*/files/etc/pacman.conf

```

Set up the [locales](/index.php/Locale "Locale") to be used by editing `*myruntime*/files/etc/locale.gen`. Then regenerate the runtime’s locales.

```
$ fakechroot chroot *myruntime*/files locale-gen

```

The base SDK can be created from the base runtime with added applications needed for building packages and running pacman.

```
$ cp -r *myruntime* mysdk
$ fakechroot fakeroot pacman -S --root mysdk/files --dbpath mysdk/files/var/lib/pacman --config mysdk/files/etc/pacman.conf base-devel fakeroot fakechroot --needed

```

Insert metadata about runtime and SDK.

 `*myruntime*/metadata` 
```
[Runtime]
name=org.mydomain.BasePlatform
runtime=org.mydomain.BasePlatform/x86_64/2016-06-26
sdk=org.mydomain.BaseSdk/x86_64/2016-06-26
```
 `mysdk/metadata` 
```
[Runtime]
name=org.mydomain.BaseSdk
runtime=org.mydomain.BasePlatform/x86_64/2016-06-26
sdk=org.mydomain.BaseSdk/x86_64/2016-06-26
```

Add base runtime and SDK to a local repository in the current directory. You may want to give them appropriate commit messages such as “My Arch base runtime” and “My Arch base SDK”.

```
$ ostree init --mode archive-z2 --repo=.
$ EDITOR="nano -w" ostree commit -b runtime/org.mydomain.BasePlatform/x86_64/2016-06-26 --tree=dir=*myruntime*
$ EDITOR="nano -w" ostree commit -b runtime/org.mydomain.BaseSdk/x86_64/2016-06-26 --tree=dir=mysdk
$ ostree summary -u

```

Install the runtime and SDK.

```
$ flatpak remote-add --user --no-gpg-verify myarchos file://$(pwd)
$ flatpak install --user myarchos org.mydomain.BasePlatform 2016-06-26
$ flatpak install --user myarchos org.mydomain.BaseSdk 2016-06-26

```

### Creating apps with pacman

As an alternative to building applications [the usual way](http://flatpak.org/developer.html), we can use pacman to create a containerized version of the regular Arch packages. Note that `/usr` is read-only when creating apps, so we can not use Arch’s packages when building an app. To create a real app with pacman, we can either

*   use pacman to create a runtime containing all dependencies
*   and compile the app ourselves [as usual](http://flatpak.org/developer.html) or perhaps using pacman with a custom [PKGBUILD](/index.php/PKGBUILD "PKGBUILD") tailored to Flatpak which uses `--prefix=/app` for the `configure` script,

or we can

*   use pacman to create a runtime containing the app installed with pacman
*   and create a dummy app to launch it.

For doing the latter, first create a runtime using pacman such as this one for [gedit](https://www.archlinux.org/packages/?name=gedit). The runtime is first initialized and prepared for use with pacman.

```
$ flatpak build-init -w geditruntime org.mydomain.geditruntime org.mydomain.BaseSdk org.mydomain.BasePlatform 2016-06-26
$ flatpak build geditruntime sed -i "s/^#Server/Server/g" /etc/pacman.d/mirrorlist
$ flatpak build geditruntime ln -s /usr/var/lib /var/lib
$ flatpak build geditruntime fakeroot pacman-key --init
$ flatpak build geditruntime fakeroot pacman-key --populate archlinux

```

Then the package is installed. The host’s network connection must be made available to pacman.

```
$ flatpak build --share=network geditruntime fakechroot fakeroot pacman --root /usr -S gedit

```

You can test the installation before finishing the runtime (without proper sandboxing).

```
$ flatpak build --socket=x11 geditruntime gedit

```

Now finish building the runtime and export it to a new local repository. pacman’s GnuPG keys have permissions that may interfere and need to be removed first.

```
$ flatpak build geditruntime rm -r /etc/pacman.d/gnupg
$ flatpak build-finish geditruntime
$ sed -i "s/\[Application\]/\[Runtime\]/;s/runtime=org.mydomain.BasePlatform/runtime=org.mydomain.geditruntime/" geditruntime/metadata
$ flatpak build-export -r geditrepo geditruntime

```

Then create a dummy app.

```
$ flatpak build-init geditapp org.gnome.gedit org.mydomain.BaseSdk org.mydomain.geditruntime

```

Now finish the dummy app. You can fine-tune the app’s access permissions when sandboxed by giving additional options when finishing the build. For possible options see the [Flatpak documentation](#See_also) and the [GNOME manifest files](https://git.gnome.org/browse/gnome-apps-nightly/tree). Alternatively, adapt `geditapp/metadata` to your needs after finishing the build but before exporting. When the metadata file is complete, export the app to the repository.

```
$ flatpak build-finish geditapp --socket=x11 *[possibly other options]* --command=gedit
$ flatpak build-export geditrepo geditapp

```

Install it along with the runtime.

```
$ flatpak --user remote-add --no-gpg-verify geditrepo geditrepo
$ flatpak install --user geditrepo org.mydomain.geditruntime
$ flatpak install --user geditrepo org.gnome.gedit
$ flatpak run org.gnome.gedit

```

## See also

*   [Official website](http://flatpak.org)
*   [Official Github wiki](https://github.com/flatpak/flatpak/wiki)
*   [Gnome SandboxedApps](https://wiki.gnome.org/Projects/SandboxedApps)
*   [KDE Testing Runtime and Applications](https://community.kde.org/Guidelines_and_HOWTOs/Flatpak)