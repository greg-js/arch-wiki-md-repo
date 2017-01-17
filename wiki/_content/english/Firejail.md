[Firejail](https://firejail.wordpress.com/) is an easy to use SUID sandbox program that reduces the risk of security breaches by restricting the running environment of untrusted applications using Linux namespaces, seccomp-bpf and Linux capabilities. Used alone or combined with [Grsecurity](/index.php/Grsecurity "Grsecurity") or other kernel hardening systems can further increase the security provided. Firejail is ideal for use with browsers, desktop applications, and daemons/servers alike.

## Contents

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
    *   [2.1 Paths with spaces](#Paths_with_spaces)
*   [3 Usage](#Usage)
    *   [3.1 Private mode](#Private_mode)
    *   [3.2 Using Firejail by default](#Using_Firejail_by_default)
        *   [3.2.1 Desktop files](#Desktop_files)
        *   [3.2.2 Daemons](#Daemons)
        *   [3.2.3 Notes](#Notes)
*   [4 Firetools](#Firetools)
*   [5 Troubleshooting](#Troubleshooting)
    *   [5.1 PulseAudio](#PulseAudio)
*   [6 See also](#See_also)

## Installation

**Note:** The User-namespace (`CONFIG_USER_NS=Y`) isn't set in the [kernel](/index.php/Kernel "Kernel") configuration, but may be required for Firejail to function properly. See [bug #36969](https://bugs.archlinux.org/task/36969) for details why this namespace is disabled by default.

[Install](/index.php/Install "Install") the [firejail](https://www.archlinux.org/packages/?name=firejail) or [firejail-git](https://aur.archlinux.org/packages/firejail-git/) package which provide all of the requirements out of the box.

## Configuration

Firejail uses profiles for the applications executed inside of it - you can find the default profiles in `/etc/firejail/*application*.profile`. Should you require custom profiles for applications not included, or wish to modify the defaults, you may place new rules or copies of the defaults in `~/.config/firejail`.

### Paths with spaces

If you need to reference, whitelist, or blacklist a directory within a custom profile, such as with [palemoon](https://aur.archlinux.org/packages/palemoon/), you must do so using the absolute path, without encapsulation or escapes:

```
/home/user/.moonchild productions

```

## Usage

To execute an application using firejail with seccomp protection, such as okular, execute the following:

```
$ firejail --seccomp okular

```

#### Private mode

Firejail also includes a one time private mode, in which no mounts are made in the chroots to your home directory. In doing this, you can execute applications without performing any changes to disk. For example, to execute okular in private mode, do the following:

```
$ firejail --seccomp --private okular

```

### Using Firejail by default

To execute an application in Firejail per default, create a symbolic link pointing to `/usr/bin/firejail`. For example:

```
$ ln -s /usr/bin/firejail /usr/local/bin/okular

```

The *firecfg* tool can be used to automate this process.

**Tip:** To open the application with your custom Firejail options, [create](/index.php/Help:Reading#Append.2C_add.2C_create.2C_edit "Help:Reading") the following file instead for Okular and make it [executable](/index.php/File_permissions_and_attributes "File permissions and attributes"): `/usr/local/bin/okular`  `firejail --seccomp /usr/bin/okular $@` 

#### Desktop files

Some applications use non standard paths. For these you will want to copy the `.desktop` launchers from `/usr/share/applications/*.desktop` to `~/.local/share/applications/` and then proceed to include firejail (and possibly seccomp) on the EXEC line.

#### Daemons

For a daemon, you will need to overwrite the systemd unit file for that daemon to call firejail, see [systemd#Editing provided units](/index.php/Systemd#Editing_provided_units "Systemd").

#### Notes

Some applications do not work properly with Firejail, and others simply require special configuration. In the instance any directories are disallowed or blacklisted for any given application, you may have to further edit the profile to enable nonstandard directories that said application needs to access. One example is wine; wine will not work with seccomp in most cases.

Other configurations exist; it is suggested you check out the man page for firejail to see them all, as firejail is in rapid development.

## Firetools

A GUI application for use with Firejail is also available, [firetools](https://aur.archlinux.org/packages/firetools/).

## Troubleshooting

### PulseAudio

If Firejail causes PulseAudio to misbehave, there is a [known issue.](https://firejail.wordpress.com/support/known-problems/) A temporary workaround:

 `cp /etc/pulse/client.conf ~/.config/pulse/`  `echo "enable-shm = no" >> ~/.config/pulse/client.conf` 

## See also

*   [Firejail GitHub project page](https://github.com/netblue30/firejail)