# Firejail

[Firejail](https://firejail.wordpress.com/) is an easy to use SUID sandbox program that reduces the risk of security breaches by restricting the running environment of untrusted applications using Linux namespaces, seccomp-bpf and Linux capabilities. Used alone or combined with [Grsecurity](/index.php/Grsecurity "Grsecurity") or other kernel hardening systems can further increase the security provided. Firejail is ideal for use with browsers, desktop applications, and daemons/servers alike.

## Contents

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
    *   [2.1 Paths With Spaces](#Paths_With_Spaces)
*   [3 Usage](#Usage)
    *   [3.1 Private Mode](#Private_Mode)
    *   [3.2 Using Firejail by Default](#Using_Firejail_by_Default)
        *   [3.2.1 Desktop Files](#Desktop_Files)
        *   [3.2.2 Daemons](#Daemons)
        *   [3.2.3 Notes](#Notes)
*   [4 Firetools](#Firetools)

## Installation

[Install](/index.php/Install "Install") the [firejail](https://aur.archlinux.org/packages/firejail/)<sup><small>AUR</small></sup> or [firejail-git](https://aur.archlinux.org/packages/firejail-git/)<sup><small>AUR</small></sup> package which provide all of the requirements out of the box.

## Configuration

Firejail uses profiles for the applications executed inside of it - you can find the default profiles in /etc/firejail/_application_.profile. Should you require custom profiles for applications not included, or wish to modify the defaults, you may place new rules or copies of the defaults in ~/.config/firejail.

### Paths With Spaces

If you need to reference, whitelist, or blacklist a directory within a custom profile, such as with [palemoon](https://aur.archlinux.org/packages/palemoon/)<sup><small>AUR</small></sup>, you must do so using the absolute path, without encapsulation or escapes:

```
   /home/user/.moonchild productions

```

## Usage

To execute an application using firejail with seccomp protection, such as firefox, execute the following:

```
$ firejail --seccomp firefox

```

#### Private Mode

Firejail also includes a one time private mode, in which no mounts are made in the chroots to your home directory. In doing this, you can execute applications without performing any changes to disk. For example, to execute firefox in private mode, do the following:

```
$ firejail --seccomp --private firefox

```

### Using Firejail by Default

For most applications launched from the console, or from `.desktop` files, you can place your own launcher proxies for each in `/usr/local/bin`. For example, [create](/index.php/Help:Reading#Append.2C_add.2C_create.2C_edit "Help:Reading") the following file for firefox make it executable:

 `/usr/local/bin/firefox`  `firejail --seccomp /usr/bin/firefox $@` 

#### Desktop Files

Some applications use non standard paths. For these you will want to copy the `.desktop` launchers from `/usr/share/applications/*.desktop` to `~/.local/share/applications/` and then proceed to include firejail (and possibly seccomp) on the EXEC line.

#### Daemons

For daemons, you will have to edit the initscripts directly to call them with firejail.

#### Notes

Some applications do not work properly with Firejail, and others simply require special configuration. In the instance any directories are disallowed or blacklisted for any given application, you may have to further edit the profile to enable nonstandard directories that said application needs to access. One example is wine; wine will not work with seccomp in most cases.

Other configurations exist; it is suggested you check out the man page for firejail to see them all, as firejail is in rapid development.

## Firetools

A GUI application for use with Firejail is also available, [firetools](https://aur.archlinux.org/packages/firetools/)<sup><small>AUR</small></sup>.

Retrieved from "[https://wiki.archlinux.org/index.php?title=Firejail&oldid=418225](https://wiki.archlinux.org/index.php?title=Firejail&oldid=418225)"