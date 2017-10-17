Related articles

*   [Security](/index.php/Security "Security")

[Firejail](https://firejail.wordpress.com/) is an easy to use SUID sandbox program that reduces the risk of security breaches by restricting the running environment of untrusted applications using Linux namespaces, seccomp-bpf and Linux capabilities.

## Contents

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
*   [3 Usage](#Usage)
    *   [3.1 Creating a custom profile](#Creating_a_custom_profile)
    *   [3.2 Persistent local customisation](#Persistent_local_customisation)
    *   [3.3 Private mode](#Private_mode)
    *   [3.4 Using Firejail by default](#Using_Firejail_by_default)
        *   [3.4.1 Verifying Firejail is being used](#Verifying_Firejail_is_being_used)
        *   [3.4.2 Desktop files](#Desktop_files)
        *   [3.4.3 Daemons](#Daemons)
        *   [3.4.4 Notes](#Notes)
*   [4 Firetools](#Firetools)
*   [5 Firejail with Apparmor](#Firejail_with_Apparmor)
    *   [5.1 Usage](#Usage_2)
*   [6 Troubleshooting](#Troubleshooting)
    *   [6.1 General](#General)
    *   [6.2 PulseAudio](#PulseAudio)
    *   [6.3 Hidepid](#Hidepid)
    *   [6.4 Makepkg](#Makepkg)
*   [7 See also](#See_also)

## Installation

**Note:** The User-namespace (`CONFIG_USER_NS=Y`) is not set in the [kernel](/index.php/Kernel "Kernel") configuration. Impact on Firejail users is [deemed negligable](https://github.com/netblue30/firejail/issues/1347). See [FS#36969](https://bugs.archlinux.org/task/36969) for details why this namespace is disabled by default. User-namespaces are [enabled](/index.php/Security#Sandboxing_applications "Security") by default in [linux-hardened](https://www.archlinux.org/packages/?name=linux-hardened) package.

[Install](/index.php/Install "Install") either [firejail](https://www.archlinux.org/packages/?name=firejail), [firejail-git](https://aur.archlinux.org/packages/firejail-git/) or the [firejail-apparmor](https://aur.archlinux.org/packages/firejail-apparmor/) package which provide all of the requirements out of the box.

## Configuration

Most users will not require any custom configuration, and can proceed to the usage section, below.

**Warning:** The default firejail profiles operate on a blacklist instead of a whitelist. This means that anything not explicitly forbidden by the profile will be accessible to the application. For example, if you have btrfs snapshots available in `/mnt/btrfs`, a jailed program may be forbidden from accessing `$HOME/.ssh`, but would be able to access `/mnt/btrfs/@some-snapshot/$HOME/.ssh`. Make sure to audit your profiles using e.g. `firejail --profile=/etc/firejail/firefox.profile /bin/bash`.

Firejail uses profiles to set the security protections for each of the applications executed inside of it - you can find the default profiles in `/etc/firejail/*application*.profile`. Should you require custom profiles for applications not included, or wish to modify the defaults, you may place new rules or copies of the defaults in the `~/.config/firejail/` directory. You may have multiple custom profile files for a single application, and you may share the same profile file among several applications.

If firejail does not have a profile for a particular application, it uses its restrictive system-wide default profile. This can result in the application not functioning as desired, without first creating a custom, and less restrictive profile.

Refer to man(5) firejail-profile.

**Tip:** Dealing with Paths containing spaces

If you need to reference, whitelist, or blacklist a directory within a custom profile, such as with [palemoon](https://aur.archlinux.org/packages/palemoon/), you must do so using the absolute path, without encapsulation or escapes:

```
/home/user/.moonchild productions

```

## Usage

To execute an application using firejail's default protections for that application (the default profile), execute the following:

```
$ firejail <program name>

```

One-time additions to the default profile can be added as command line options (see the man page). For example, to execute *okular* with seccomp protection, execute the following:

```
$ firejail --seccomp okular

```

You may define multiple non-default profiles for a single program. Once you create your profile file, you can use it by executing:

```
$ firejail --profile=/absolute/path/to/profile <program name>

```

### Creating a custom profile

See man(5) firejail-profile

### Persistent local customisation

The standard profile layout now includes the capability to make persistent local customisations through the inclusion of `.local` files. Basically, each officially supported profile contains the lines `include /etc/firejail/ProgramName.local` and `include /etc/firejail/globals.local`. Since the order of precedence is determined by which is read first, this makes for a very powerful way of making local customisations.

For example, with reference [this firejail question](https://github.com/netblue30/firejail/issues/1510#issuecomment-326443650), to globally enable Apparmor and disable Internet connectivity, one could simply create/edit `/etc/firejail/globals.local` to include the lines

```
# enable Apparmor and disable Internet globally
net none
apparmor

```

Then, to allow, for example, "curl" to connect to the internet, yet still maintain its apparmor confinement, one would create/edit `/etc/firejail/curl.local` to include the lines.

```
# enable internet for curl
ignore net

```

Since `curl.local` is read before `globals.local`, `ignore net` overrides `net none`, and, as a bonus, the above changes would be persistent across future updates.

### Private mode

Firejail also includes a one time private mode, in which no mounts are made in the chroots to your home directory. In doing this, you can execute applications without performing any changes to disk. For example, to execute okular in private mode, do the following:

```
$ firejail --seccomp --private okular

```

### Using Firejail by default

To use Firejail by default for all applications for which it has profiles, run the *firecfg* tool as root.

```
# firecfg

```

This creates symbolic links in `/usr/local/bin` pointing to `/usr/bin/firejail`, for all programs for which firejail has default profiles. Once this is done, you only need to prefix a program with *firejail* if you want to run it with some custom security setting.

You can manually do this for individual applications by executing:

```
# ln -s /usr/bin/firejail /usr/local/bin/<program name>

```

Note, `firecfg` doesn't work with some cli shells such as: `tar`, `curl`, `wget`, `git` and `ssh` which need to be symlinked manually. One should also note that, while symlinking these shells does not break official packages like`pacman`, doing so may break certain AUR packages. In particular, without weakening the `/etc/firejail/curl.profile`, symlinking `curl` will break [Yaourt](https://aur.archlinux.org/packages/Yaourt/), but not, for example, [Cower](https://aur.archlinux.org/packages/Cower/).

#### Verifying Firejail is being used

```
$ firejail --list

```

#### Desktop files

Some GUI application launchers (`.desktop` files) are coded using absolute paths to an executable, which circumvents firejail's symlink method of ensuring that it is being used. The *firecfg* tool includes an option to over-ride this on a per-user basis, by copying the `.desktop` files from `/usr/share/applications/*.desktop` to `~/.local/share/applications/` and replacing the absolute paths with simple file names.

```
$ firecfg --fix

```

There may be other cases for which you may need to do this manually, possibly needing to modify the EXEC line of the `.desktop` file to explicitly call firejail.

#### Daemons

For a daemon, you will need to overwrite the systemd unit file for that daemon to call firejail, see [systemd#Editing provided units](/index.php/Systemd#Editing_provided_units "Systemd").

#### Notes

Some applications do not work properly with Firejail, and others simply require special configuration. In the instance any directories are disallowed or blacklisted for any given application, you may have to further edit the profile to enable nonstandard directories that said application needs to access. One example is wine; wine will not work with seccomp in most cases.

Other configurations exist; it is suggested you check out the man page for firejail to see them all, as firejail is in rapid development.

## Firetools

A GUI application for use with Firejail is also available, [firetools](https://aur.archlinux.org/packages/firetools/).

## Firejail with Apparmor

Since 0.942, [firejail-apparmor](https://aur.archlinux.org/packages/firejail-apparmor/), has supported more direct integration with Apparmor through a generic apparmor profile. During installation, the profile, `firejail-default`, is placed in `/etc/apparmor.d` directory, and needs to be loaded into the kernel by running the following command as root:

```
# aa-enforce firejail-default

```

To quote the manual:

	*The installed profile tries to replicate some advanced security features inspired by kernel-based Grsecurity:*

	*- Prevent information leakage in /proc and /sys directories.The resulting filesystem is barely enough for running commands such as "top" and "ps aux".*

	*- Allow running programs only from well-known system paths, such as /bin, /sbin, /usr/bin etc. Running programs and scripts from user home or other directories writable by the user is not allowed.*

	*- Disable D-Bus. D-Bus has long been a huge security hole, and most programs don't use it anyway. You should have no problems running Chromium or Firefox.*

Note, with the release of 0.9.50, local customisations of the apparmor profile are also supported by editing the file `/etc/apparmor.d/local/firejail-local`

#### Usage

To enable Apparmor confinement on top of a Firejail security profile, pass the `--apparmor` flag to Firejail in the command line.

Example:

```
$ firejail --apparmor firefox

```

Alternatively, the apparmor flag could be added to a custom profile. Or, it could be enabled globally through `/etc/firejail/globals.local` and disabled as needed through the use of `ignore apparmor` in an applications local customisation file,

For example:

/etc/firejail/globals.local

```
# enables apparmor globally
apparmor

```

/etc/firejail/keepass.local

```
# disables apparmor for keepass
ignore apparmor

```

## Troubleshooting

### General

1\. If you are depending upon `firecfg` to have generated a symlink, ie. you followed the instructions for [#Using Firejail by default](#Using_Firejail_by_default), double-check that the symlink was actually created. You may need to create one manually.

2\. If the symlink exists, you may need to run `sudo updatedb` to update the location database.

3\. You may need to re-initialize the hash for the executable, ie. `hash -d <command_name>`.

### PulseAudio

If Firejail causes PulseAudio to misbehave, there is a [known issue.](https://firejail.wordpress.com/support/known-problems/) A temporary workaround:

 `cp /etc/pulse/client.conf ~/.config/pulse/`  `echo "enable-shm = no" >> ~/.config/pulse/client.conf` 

### Hidepid

if you have hidepid installed, Firemon can only be run as root. This, among other things, will cause problems with the Firetools GUI incorrectly reporting "Capabilities", "Protocols" and the status of "Seccomp". See [this issue](https://github.com/netblue30/firejail/issues/1564).

### Makepkg

With respect to this [Arch Forum](https://bbs.archlinux.org/viewtopic.php?id=230913) post. During the final stages of a pkgbuild, (when compressing the package,) symlinks to `gzip` and `xz` interfere with `makepkg’s` ability to preload the `libfakeroot.so` The most elegant way of solving the problem is to temporarily exclude `/usr/local/bin` from the `makepkg $PATH` by appending the following to `/etc/makepkg.conf`

```
# Temporarily alter the makepkg PATH variable to exclude /usr/local/bin
PATH=":$PATH"
PATH="${PATH/:\/usr\/local\/bin:/:}"
PATH="${PATH/:\/usr\/local\/sbin:/:}"
export PATH="${PATH#:}"

```

The linked post offers a fully tested `makepkg.profile` and using the above solution, `makepkg` can itself be symlinked to use firejail by default.

## See also

*   [Firejail GitHub project page](https://github.com/netblue30/firejail)
*   [bubblewrap](/index.php/Bubblewrap "Bubblewrap"), a minimal alternative to Firejail