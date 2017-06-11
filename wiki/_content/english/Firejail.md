[Firejail](https://firejail.wordpress.com/) is an easy to use SUID sandbox program that reduces the risk of security breaches by restricting the running environment of untrusted applications using Linux namespaces, seccomp-bpf and Linux capabilities.

## Contents

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
*   [3 Usage](#Usage)
    *   [3.1 Creating a custom profile](#Creating_a_custom_profile)
    *   [3.2 Private mode](#Private_mode)
    *   [3.3 Using Firejail by default](#Using_Firejail_by_default)
        *   [3.3.1 Verifying Firejail is being used](#Verifying_Firejail_is_being_used)
        *   [3.3.2 Desktop files](#Desktop_files)
        *   [3.3.3 Daemons](#Daemons)
        *   [3.3.4 Notes](#Notes)
*   [4 Firetools](#Firetools)
*   [5 Troubleshooting](#Troubleshooting)
    *   [5.1 PulseAudio](#PulseAudio)
*   [6 See also](#See_also)

## Installation

**Note:** The User-namespace (`CONFIG_USER_NS=Y`) is not set in the [kernel](/index.php/Kernel "Kernel") configuration, but may be required for Firejail to function properly. See [FS#36969](https://bugs.archlinux.org/task/36969) for details why this namespace is disabled by default. User-namespaces are [enabled](/index.php/Security#Sandboxing_applications "Security") by default in [linux-hardened](https://www.archlinux.org/packages/?name=linux-hardened) package.

[Install](/index.php/Install "Install") the [firejail](https://www.archlinux.org/packages/?name=firejail) or [firejail-git](https://aur.archlinux.org/packages/firejail-git/) package which provide all of the requirements out of the box.

## Configuration

Most users will not require any custom configuration, and can proceed to the usage section, below.

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

## Troubleshooting

### PulseAudio

If Firejail causes PulseAudio to misbehave, there is a [known issue.](https://firejail.wordpress.com/support/known-problems/) A temporary workaround:

 `cp /etc/pulse/client.conf ~/.config/pulse/`  `echo "enable-shm = no" >> ~/.config/pulse/client.conf` 

## See also

*   [Firejail GitHub project page](https://github.com/netblue30/firejail)