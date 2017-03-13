ThinkFinger is a driver for the SGS Thomson Microelectronics fingerprint reader found in older IBM/Lenovo ThinkPads.

ThinkWiki has a [list of various fingerprint readers](http://www.thinkwiki.org/wiki/Integrated_Fingerprint_Reader) found in ThinkPads. Newer models using different readers might not work with ThinkFinger.

**Warning:** ThinkFinger-svn revisions above rev 72 require you to load the module `uinput`.

## Contents

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
    *   [2.1 TF-Tool](#TF-Tool)
*   [3 Pam](#Pam)
    *   [3.1 /etc/pam.d/login](#.2Fetc.2Fpam.d.2Flogin)
    *   [3.2 /etc/pam.d/su](#.2Fetc.2Fpam.d.2Fsu)
    *   [3.3 /etc/pam.d/sudo](#.2Fetc.2Fpam.d.2Fsudo)
    *   [3.4 /etc/pam.d/xscreensaver](#.2Fetc.2Fpam.d.2Fxscreensaver)
    *   [3.5 /etc/pam.d/gdm](#.2Fetc.2Fpam.d.2Fgdm)
    *   [3.6 /etc/pam.d/xdm](#.2Fetc.2Fpam.d.2Fxdm)
*   [4 SLiM](#SLiM)
*   [5 Alternative fingerprint reader software](#Alternative_fingerprint_reader_software)
*   [6 See also](#See_also)

## Installation

[Install](/index.php/Install "Install") the [thinkfinger](https://www.archlinux.org/packages/?name=thinkfinger) package.

## Configuration

### TF-Tool

Use `tf-tool` to test ThinkFinger. You will have to run this as root because a direct access to the usb devices is needed. Run `tf-tool --acquire` to generate a file at `/etc/pam_thinkfinger/test.bir` and `tf-tool --verify` to see if it identifies you correctly. `tf-tool --add-user <username>` acquires and stores your fingerprint in `/etc/pam_thinkfinger/<username>.bir`, which is needed for an authentication with pam.

## Pam

[PAM](/index.php/PAM "PAM") is the Pluggable Authentication Module, invented by Sun.

### /etc/pam.d/login

Change the file `/etc/pam.d/login` to look like this if you want to use your fingerprint to authenticate yourself on logon:

 `/etc/pam.d/login` 
```
#%PAM-1.0
auth		sufficient	pam_thinkfinger.so
auth		required	pam_unix.so use_first_pass nullok_secure
account		required	pam_unix.so
password	required	pam_unix.so
session		required	pam_unix.so
```

### /etc/pam.d/su

Change this file to confirm the `su` command with a finger-swipe:

 `/etc/pam.d/su` 
```
#%PAM-1.0
auth            sufficient      pam_rootok.so
auth		sufficient 	pam_thinkfinger.so
auth		required	pam_unix.so nullok_secure try_first_pass
account		required	pam_unix.so
session		required	pam_unix.so
```

**Tip:** Do not forget to do a `tf-tool --add-user root` to use this feature.

### /etc/pam.d/sudo

Change this file to confirm the `sudo` command with a finger-swipe:

 `/etc/pam.d/su` 
```
#%PAM-1.0
auth		sufficient 	pam_thinkfinger.so
auth		required	pam_unix.so nullok_secure try_first_pass
auth		required	pam_nologin.so
```

### /etc/pam.d/xscreensaver

XScreensaver is a bit tricky. First, configure PAM with a file `/etc/pam.d/xscreensaver` containing:

 `/etc/pam.d/xscreensaver` 
```
 auth            sufficient      pam_thinkfinger.so
 auth            required        pam_unix_auth.so try_first_pass
```

This still won't work because Xscreensaver cannot read/write from `/dev/misc/uinput` and `/dev/bus/usb*`. A [udev](/index.php/Udev "Udev") rule must be written to authorize a new group read/write access.

First, create a new group, let's say *fingerprint*:

```
# groupadd fingerprint

```

Add the user you want to be able to unlock Xscreensaver with the fingerprint reader to the group:

```
# gpasswd -a <user> fingerprint

```

Logout and login again for the changes to take effect.

Next, search for *uinput* and *bus/usb* in your udev rules directory:

```
$ grep -in uinput /etc/udev/rules.d/*

/etc/udev/rules.d/udev.rules:222:KERNEL=="uinput",  NAME="misc/%k", SYMLINK+="%k"
/etc/udev/rules.d/udev.rules:263:KERNEL=="uinput", NAME="input/%k"
```

```
$ grep -in "bus/usb" /etc/udev/rules.d/*

/etc/udev/rules.d/udev.rules:318:SUBSYSTEM=="usb_device", ACTION=="add", PROGRAM="/bin/sh -c 'K=%k; K=$${K#usbdev};printf bus/usb/%%03i/%%03i $${K%%%%.*} $${K#*.}'", NAME="%c", MODE="0664"
/etc/udev/rules.d/udev.rules:320:SUBSYSTEM=="usb", ACTION=="add", ENV{DEVTYPE}=="usb_device", NAME="bus/usb/$env{BUSNUM}/$env{DEVNUM}", MODE="0664"
```

Copy the lines you found with grep in the previous step to a new udev rules file:

 `/etc/udev/rules.d/99fingerprint.rules` 
```
KERNEL=="uinput",  NAME="misc/%k", SYMLINK+="%k", MODE="0660", GROUP="fingerprint"
SUBSYSTEM=="usb_device", ACTION=="add", PROGRAM="/bin/sh -c 'K=%k; K=$${K#usbdev};printf bus/usb/%%03i/%%03i $${K%%%%.*} $${K#*.}'", NAME="%c", MODE="0664", GROUP="fingerprint"
SUBSYSTEM=="usb", ACTION=="add", ENV{DEVTYPE}=="usb_device", NAME="bus/usb/$env{BUSNUM}/$env{DEVNUM}", MODE="0664", GROUP="fingerprint"
```

The difference between the rules in `/etc/udev/rules.d/99fingreprint.rules` and those in `/etc/udev/rules.d/udev.rules` should only be the addition of `MODE="0664", GROUP="fingerprint"` or `MODE="0660", GROUP="fingerprint"` at the end of the lines.

After adding the custom udev rules, you should give your user permissions to access their own fingerprint file:

```
$ chown $USERNAME:root /etc/pam_thinkfinger/$USERNAME.bir
$ chmod 400 /etc/pam_thinkfinger/$USERNAME.bir
$ chmod o+x /etc/pam_thinkfinger
```

**Note:** The last command is opening up a directory for execution to everyone, beware of the security implications this might have.

As a last step, you need to remove the root setuid from `/usr/bin/xscreensaver`, otherwise Xscreensaver wont be able to unlock with the fingerprint reader:

```
# chmod -s /usr/bin/xscreensaver

```

### /etc/pam.d/gdm

Edit `/etc/pam.d/gdm` and add the following line to the top:

 `/etc/pam.d/gdm` 
```
auth		sufficient 	pam_thinkfinger.so

```

Then modify `auth required pam_unix.so` to look like this:

 `/etc/pam.d/gdm` 
```
auth		required	pam_unix.so use_first_pass nullok_secure

```

### /etc/pam.d/xdm

Edit `/etc/pam.d/xdm` to look like this:

 `/etc/pam.d/xdm` 
```
#%PAM-1.0
auth            sufficient      pam_thinkfinger.so
auth            required        pam_unix.so use_first_pass nullok_secure
auth            required        pam_nologin.so
auth            required        pam_env.so
account         required        pam_unix.so
password        required        pam_unix.so
session         required        pam_unix.so
session         required        pam_limits.so

```

## SLiM

To have thinkfinger support for the [SLiM|SLiM Login Manager], you need to activate PAM support.

Get the package source of the slim package from [ABS](/index.php/ABS "ABS"), and edit the [PKGBUILD](/index.php/PKGBUILD "PKGBUILD") so that the `make` command builds SLiM with PAM support:

 `SLiM PKGBUILD`  `make USE_PAM=1` 

Rebuild the package and install it.

Then create `/etc/pam.d/slim`:

 `/etc/pam.d/slim` 
```
#%PAM-1.0
auth            sufficient      pam_thinkfinger.so
auth            requisite       pam_nologin.so
auth            required        pam_env.so
auth            required        pam_unix.so
account         required        pam_unix.so
session         required        pam_limits.so
session         required        pam_unix.so
password        required        pam_unix.so

```

Now restart SLiM and you may use the fingerprinter to login.

## Alternative fingerprint reader software

[Fprint](/index.php/Fprint "Fprint") is an alternative fingerprint reader software that works with some of the newer ThinkPad fingerprint readers.

## See also

*   [http://www.thinkwiki.org/wiki/Talk:How_to_enable_the_fingerprint_reader](http://www.thinkwiki.org/wiki/Talk:How_to_enable_the_fingerprint_reader)
*   [http://thinkfinger.sourceforge.net/](http://thinkfinger.sourceforge.net/)
*   [https://bbs.archlinux.org/viewtopic.php?id=36134](https://bbs.archlinux.org/viewtopic.php?id=36134)
*   [http://www.thinkwiki.org/wiki/How_to_enable_the_fingerprint_reader_with_ThinkFinger](http://www.thinkwiki.org/wiki/How_to_enable_the_fingerprint_reader_with_ThinkFinger)
*   [http://www.thinkwiki.org/index.php?title=Installing_Ubuntu_6.06_on_a_ThinkPad_T43#Fingerprint_Reader](http://www.thinkwiki.org/index.php?title=Installing_Ubuntu_6.06_on_a_ThinkPad_T43#Fingerprint_Reader)