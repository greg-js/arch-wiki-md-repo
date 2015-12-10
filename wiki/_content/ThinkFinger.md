# ThinkFinger

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

[![Tango-mail-mark-junk.png](/images/e/e7/Tango-mail-mark-junk.png)](/index.php/File:Tango-mail-mark-junk.png)

[![Tango-mail-mark-junk.png](/images/e/e7/Tango-mail-mark-junk.png)](/index.php/File:Tango-mail-mark-junk.png)

**This article or section needs language, wiki syntax or style improvements.**

**Reason:** Article contains many HTML tags and requires some cleanup. Use `''italic''` for italic text, `{{ic|text}}` for inline code including files/directories, etc. See [Help:Style](/index.php/Help:Style "Help:Style"). (Discuss in [Talk:ThinkFinger#](https://wiki.archlinux.org/index.php/Talk:ThinkFinger))

Related articles

*   [Fingerprint-gui](/index.php/Fingerprint-gui "Fingerprint-gui")
*   [Fprint](/index.php/Fprint "Fprint")

ThinkFinger is a driver for the SGS Thomson Microelectronics fingerprint reader found in older IBM/Lenovo ThinkPads.

ThinkWiki has a [list of various fingerprint readers](http://www.thinkwiki.org/wiki/Integrated_Fingerprint_Reader) found in ThinkPads. Newer models using different readers might not work with ThinkFinger.

**Warning:** ThinkFinger-svn revisions above rev 72 require you to load the module _uinput_!

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

Install [thinkfinger](https://www.archlinux.org/packages/?name=thinkfinger) from the [official repositories](/index.php/Official_repositories "Official repositories").

## Configuration

### TF-Tool

Use _tf-tool_ to test ThinkFinger. You will have to run this as root because a direct access to the usb devices is needed. Run _tf-tool --acquire_ to generate a test.bir and _tf-tool --verify_ to see if it identifies you correctly. _tf-tool --add-user <username>_ acquires and stores your fingerprint in _/etc/pam_thinkfinger/username.bir_, which is needed for an authentication with pam.

## Pam

PAM is the Pluggable Authentication Module, invented by Sun.

### /etc/pam.d/login

Change the file _/etc/pam.d/login_ to look like this if you want to use your fingerprint to authenticate yourself on logon:

```
#%PAM-1.0
auth		sufficient	pam_thinkfinger.so
auth		required	pam_unix.so use_first_pass nullok_secure
account		required	pam_unix.so
password	required	pam_unix.so
session		required	pam_unix.so

```

### /etc/pam.d/su

Change this file to confirm the _su_ command with a finger-swipe!

```
#%PAM-1.0
auth            sufficient      pam_rootok.so
auth		sufficient 	pam_thinkfinger.so
auth		required	pam_unix.so nullok_secure try_first_pass
account		required	pam_unix.so
session		required	pam_unix.so

```

**Tip:** Do not forget to do a _tf-tool --add-user root to use this feature_!

### /etc/pam.d/sudo

Change this file to confirm the _sudo_ command with a finger-swipe!

```
#%PAM-1.0
auth		sufficient 	pam_thinkfinger.so
auth		required	pam_unix.so nullok_secure try_first_pass
auth		required	pam_nologin.so

```

### /etc/pam.d/xscreensaver

XScreensaver is a bit tricky. First, configure PAM with a file "/etc/pam.d/xscreensaver" containing :

```
auth            sufficient      pam_thinkfinger.so
auth            required        pam_unix_auth.so try_first_pass

```

But it still wont work with only that because xscreensaver cannot read/write from /dev/misc/uinput and /dev/bus/usb*. A udev rule must be written to authorize a new group read/write access.

First, create a new group. I suggest "fingerprint":

```
> sudo groupadd fingerprint
Add the user you want to be able to unlock xscreensaver with the fingerprint reader to the group:
> sudo gpasswd -a <user> fingerprint

```

Don't forget to logout and login again!

Search for "uinput" and "bus/usb" in your udev rules directory :

```
> grep -in uinput /etc/udev/rules.d/*
/etc/udev/rules.d/udev.rules:222:KERNEL=="uinput",  NAME="misc/%k", SYMLINK+="%k"
/etc/udev/rules.d/udev.rules:263:KERNEL=="uinput", NAME="input/%k"
> grep -in "bus/usb" /etc/udev/rules.d/*
/etc/udev/rules.d/udev.rules:318:SUBSYSTEM=="usb_device", ACTION=="add", PROGRAM="/bin/sh -c 'K=%k; K=$${K#usbdev};printf bus/usb/%%03i/%%03i $${K%%%%.*} $${K#*.}'", NAME="%c", MODE="0664"
/etc/udev/rules.d/udev.rules:320:SUBSYSTEM=="usb", ACTION=="add", ENV{DEVTYPE}=="usb_device", NAME="bus/usb/$env{BUSNUM}/$env{DEVNUM}", MODE="0664"

```

Now copy the previous lines (222, 318 and 320 from /etc/udev/rules.d/udev.rules) to a new udev rules file. I suggest /etc/udev/rules.d/99my.rules

```
KERNEL=="uinput",  NAME="misc/%k", SYMLINK+="%k", MODE="0660", GROUP="fingerprint"
SUBSYSTEM=="usb_device", ACTION=="add", PROGRAM="/bin/sh -c 'K=%k; K=$${K#usbdev};printf bus/usb/%%03i/%%03i $${K%%%%.*} $${K#*.}'", NAME="%c", MODE="0664", GROUP="fingerprint"
SUBSYSTEM=="usb", ACTION=="add", ENV{DEVTYPE}=="usb_device", NAME="bus/usb/$env{BUSNUM}/$env{DEVNUM}", MODE="0664", GROUP="fingerprint"

```

The difference between the rules in /etc/udev/rules.d/99my.rules and those in /etc/udev/rules.d/udev.rules should only be the addition of MODE="0664", GROUP="fingerprint" or MODE="0660", GROUP="fingerprint" at the end of the lines.

After this you must actually give your user permissions to access his own fingerprint file, this can be done as in the following:

```
> chown $USERNAME:root /etc/pam_thinkfinger/$USERNAME.bir
> chmod 400 /etc/pam_thinkfinger/$USERNAME.bir
> chmod o+x /etc/pam_thinkfinger

```

Yes that last one is opening up a directory for execution to everyone so if you are super paranoid you might consider that a security flaw, just putting the warning out there.

The last part is about xscreensaver. If you check xscreensaver file, you will see it is setuid to root :

```
> ls -l /usr/bin/xscreensaver
-rwsr-sr-x 1 root root 217K aoû  2 20:47 /usr/bin/xscreensaver

```

Because of this, xscreensaver wont be able to unlock with the fingerprint reader. You need to remove the setuid root with :

```
> sudo chmod -s /usr/bin/xscreensaver
> ls -l /usr/bin/xscreensaver
-rwxr-xr-x 1 root root 217K aoû  2 20:47 /usr/bin/xscreensaver

```

That's it!

### /etc/pam.d/gdm

[I am not an expert in PAMs but this works, This section may need corrections]

Edit _/etc/pam.d/gdm_ as done in sections 3.1 and 3.2

```
add as the first line in the file: 
auth		sufficient 	pam_thinkfinger.so

```

```
Modify:
auth		required	pam_unix.so ==> auth		required	pam_unix.so use_first_pass nullok_secure

```

### /etc/pam.d/xdm

Change /etc/pam.d/xdm to look like this:

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

To have thinkfinger support for the SLiM Login Manager you need to activate PAM support:

Get the package source of the slim package from ABS and change the "make" line in the PKGBUILD:

```
make USE_PAM=1 || return 1

```

Rebuild the package and install it.

Then create a file /etc/pam.d/slim:

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

Now restart slim and swipe your finger.

## Alternative fingerprint reader software

[Fprint](/index.php/Fprint "Fprint") is an alternative fingerprint reader software that works with some of the newer ThinkPad fingerprint readers.

## See also

*   [http://www.thinkwiki.org/wiki/Talk:How_to_enable_the_fingerprint_reader](http://www.thinkwiki.org/wiki/Talk:How_to_enable_the_fingerprint_reader)
*   [http://thinkfinger.sourceforge.net/](http://thinkfinger.sourceforge.net/)
*   [https://bbs.archlinux.org/viewtopic.php?id=36134](https://bbs.archlinux.org/viewtopic.php?id=36134)
*   [http://www.thinkwiki.org/wiki/How_to_enable_the_fingerprint_reader_with_ThinkFinger](http://www.thinkwiki.org/wiki/How_to_enable_the_fingerprint_reader_with_ThinkFinger)
*   [http://www.thinkwiki.org/index.php?title=Installing_Ubuntu_6.06_on_a_ThinkPad_T43#Fingerprint_Reader](http://www.thinkwiki.org/index.php?title=Installing_Ubuntu_6.06_on_a_ThinkPad_T43#Fingerprint_Reader)

Retrieved from "[https://wiki.archlinux.org/index.php?title=ThinkFinger&oldid=404386](https://wiki.archlinux.org/index.php?title=ThinkFinger&oldid=404386)"

[Categories](/index.php/Special:Categories "Special:Categories"):

*   [Input devices](/index.php/Category:Input_devices "Category:Input devices")
*   [Lenovo](/index.php/Category:Lenovo "Category:Lenovo")