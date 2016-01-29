# Dofus

[Dofus](http://www.dofus.com) is an MMORPG by [Ankama](http://www.ankama.com).

## AUR

Installation can be automated with the [AUR](/index.php/AUR "AUR") package [dofus](https://aur.archlinux.org/packages/dofus/)<sup><small>AUR</small></sup>, which depends on [ankama-transition](https://aur.archlinux.org/packages/ankama-transition/)<sup><small>AUR</small></sup>, the updater.

Currently the game files are installed under the "games" group with group writability. You can add your user to the group (<tt>usermod -a -G games _username_</tt>) to take advantage of this. Otherwise, you may need to enter your password in order to update the game files.

## Manual Installation

Ankama provides official Linux packages for Dofus, but some modifications are necessary for them to work on Arch Linux.

There is no Adobe Air runtime on Arch Linux, so it is necessary to use this [workaround](/index.php/Adobe_AIR "Adobe AIR") involving <tt>adobe-air-sdk</tt>. <tt>transition</tt> needs to be configured to use the sdk launcher instead of binaries provided by Dofus. Additionally, <tt>transition</tt> will by default attempt to install Adobe Air, and this needs to be disabled in its configuration.

The [dofus](https://aur.archlinux.org/packages/dofus/)<sup><small>AUR</small></sup> AUR package accomplishes these with the following code in <tt>transition.conf</tt>:

```
 bypass_air_installation = true
 dofus.reg.path = "${root}/share/reg/bin/air-generic-launcher.sh"

 launcher.command = """
 "${root}/bin/air-generic-launcher.sh" --lang=${i18n.lang} --update-server-port=${service_port} --updater_version=v2

```

It installs <tt>air-generic-launcher.sh</tt> in the same locations as the game client and sound engine executables, to run them with the SDK launcher:

```
 #!/bin/bash

 # This is a generic launcher script for AIR applications on Arch Linux

 SCRIPT_PATH=`readlink -f $0`
 SCRIPT_DIR=`dirname $SCRIPT_PATH`
 BASE_DIR=`readlink -f $SCRIPT_DIR/..`

 if [ "`uname -m`" == "x86_64" ]; then
 	export GTK_PATH=/usr/lib32/gtk-2.0
 	export G_FILENAME_ENCODING=UTF-8
 fi

 /opt/adobe-air-sdk/bin/adl -nodebug $BASE_DIR/share/META-INF/AIR/application.xml $BASE_DIR/share -- $*

```

## Troubleshooting

When debugging problems, it is helpful to set the environment variable `AK_LOG_CONSOLE=1` when running Dofus. It will then print detailed logs in the console.

A known problem is that some systems require <tt>unset SESSION_MANAGER</tt> in the environment, to avoid crashes on start up.

Occasionally the updater cannot function because of a leftover process from previous runs. Killing <tt>transition</tt> processes can solve this problem.

Retrieved from "[https://wiki.archlinux.org/index.php?title=Dofus&oldid=376650](https://wiki.archlinux.org/index.php?title=Dofus&oldid=376650)"