# BOINC

From the [BOINC website](http://boinc.berkeley.edu/):

NaN

From [Wikipedia:BOINC](https://en.wikipedia.org/wiki/BOINC "wikipedia:BOINC"):

NaN

## Contents

*   [1 Installation](#Installation)
*   [2 Using BOINC](#Using_BOINC)
    *   [2.1 BOINC via the GUI](#BOINC_via_the_GUI)
        *   [2.1.1 Projects using GPU](#Projects_using_GPU)
    *   [2.2 BOINC via the CLI](#BOINC_via_the_CLI)
*   [3 Log files](#Log_files)
*   [4 Considerations when choosing a project](#Considerations_when_choosing_a_project)
    *   [4.1 Running on Arch64](#Running_on_Arch64)
*   [5 Troubleshooting](#Troubleshooting)
    *   [5.1 GPU missing](#GPU_missing)
    *   [5.2 Laptop overheating and battery duration reduction](#Laptop_overheating_and_battery_duration_reduction)
    *   [5.3 Unable to download with World Community Grid](#Unable_to_download_with_World_Community_Grid)
*   [6 See also](#See_also)

## Installation

[Install](/index.php/Install "Install") either the [boinc](https://www.archlinux.org/packages/?name=boinc) or the [boinc-nox](https://www.archlinux.org/packages/?name=boinc-nox) package. The latter omits [Xorg](/index.php/Xorg "Xorg") dependencies, and is therefore suited for use on headless servers.

Both packages install a [unit](/index.php/Systemd#Using_units "Systemd") file named `boinc.service`.

You will also need to add yourself to the `boinc` group in order for the manager to connect:

```
# usermod -a -G boinc $(whoami)

```

To generate the necessary files referenced in the next section, make sure to [start](/index.php/Start "Start") `boinc.service`.

## Using BOINC

### BOINC via the GUI

By default, a password is created in `/var/lib/boinc/gui_rpc_auth.cfg` for connecting to the daemon. To simplify connection of the GUI to the daemon, cd to your home directory, create a link to the file, and change permissions to allow read access to boinc group members.

```
$ cd ~/
$ ln -s /var/lib/boinc/gui_rpc_auth.cfg gui_rpc_auth.cfg
# chmod 640 gui_rpc_auth.cfg

```

If you prefer a different password, or none at all, you can edit `/var/lib/boinc/gui_rpc_auth.cfg`. Then restart BOINC daemon.

If you do not like the idea of having this file in your home directory, there is an alternative approach. BOINC Manager will also look for a readable gui_rpc_auth.cfg file in the current working directory. If you make the file readable by the **boinc** group and ensure that the manager is run with `/var/lib/boinc` as the working directory, you should find that the client connects to the daemon automatically, as desired. This can usually be achieved via the menu editor in your desktop environment of choice.

To start the GUI, use the _boincmgr_ command

```
$ boincmgr

```

BOINC should now take you through the process of attaching to a project. NB, some projects will let you create an account remotely via the GUI while some may require you to first create an account via their website. You can attach to multiple projects if you have the resources (disk space, time, CPU power). Do this via menu option _Tools / Attach to project_.

If BOINC did not ask you to connect to a project, then make sure you are connected to the daemon. Go to menu option _Advanced / Select computer_, choose your machine's name and enter the password. (To avoid this, make sure the above steps regarding gui_rpc_auth.cfg have been done.)

#### Projects using GPU

If you want to use your GPU, you need the proprietary nvidia or amd drivers. For ATI/AMD Cards you also need [Catalyst](/index.php/Catalyst "Catalyst") driver for stock kernel which you can get from AUR. For Nvidia, you also need the package [opencl-nvidia](https://www.archlinux.org/packages/?name=opencl-nvidia) located in extra.

In addition, the boinc user should be in the video group:

```
# gpasswd -a boinc video

```

The boinc user also needs to have access to your X session. Use this command to accomplish this:

```
xhost local:boinc

```

You may want to add that to a startup script.

### BOINC via the CLI

For [boinc-nox](https://www.archlinux.org/packages/?name=boinc-nox), `boinccmd` and `boinc` have help information that can be referenced. `boinccmd` is BOINC's recommended command line interface.

## Log files

NB, BOINC places log files in `/var/lib/boinc/`

```
/var/lib/boinc/stderrdae.txt
/var/lib/boinc/stdoutdae.txt

```

## Considerations when choosing a project

Projects have different minimum hardware requirements (CPU, disk space), and different times to taken to run each work unit. If you do not finish a work unit before the deadline it will sent out to someone else, but it is better to look around to see what projects suit your machine and your uptime patterns to avoid this happening.

Also, if it is important to you, check if the project makes the data and results publicly available.

### Running on Arch64

Some projects provide only 32bit applications which may require 32bit libraries to run work units or show graphics. You will find most of these libraries in the [multilib] repository.

NaN

## Troubleshooting

### GPU missing

If you get this error :

 `GPU Missing` 

and the Work Unit does not start, you should [restart](/index.php/Daemons "Daemons") the `boinc.service` daemon.

This will happen if the BOINC daemon starts before the an X session is fully initialized.

### Laptop overheating and battery duration reduction

If you run BIONC on a laptop with the ondemand governor (the default), it will keep the CPUs at their maximum frequencies (over)heating them and decreasing battery duration. The best way to fix this is to tell the ondemand to not rise the CPU frequencies for BOINC:

 `# echo 1 >/sys/devices/system/cpu/cpufreq/ondemand/ignore_nice_load` 

To do this on boot, create the following tmpfiles.d config:

 `/etc/tmpfiles.d/ondemand-ignore-nice.conf`  `w /sys/devices/system/cpu/cpufreq/ondemand/ignore_nice_load - - - - 1` 

### Unable to download with World Community Grid

[![Tango-emblem-important.png](/images/c/c8/Tango-emblem-important.png)](/index.php/File:Tango-emblem-important.png)

[![Tango-emblem-important.png](/images/c/c8/Tango-emblem-important.png)](/index.php/File:Tango-emblem-important.png)

**The factual accuracy of this article or section is disputed.**

**Reason:** Pointing to modified PKGBUILD without explaining the differences from the official one is just wrong. (Discuss in [Talk:BOINC#](https://wiki.archlinux.org/index.php/Talk:BOINC))

[![Tango-mail-mark-junk.png](/images/e/e7/Tango-mail-mark-junk.png)](/index.php/File:Tango-mail-mark-junk.png)

[![Tango-mail-mark-junk.png](/images/e/e7/Tango-mail-mark-junk.png)](/index.php/File:Tango-mail-mark-junk.png)

**This article or section needs language, wiki syntax or style improvements.**

**Reason:** Modified PKGBUILD should be in [AUR](/index.php/AUR "AUR") (Discuss in [Talk:BOINC#](https://wiki.archlinux.org/index.php/Talk:BOINC))

If you are unable to download new work units for the World Community Grid project, [makepkg](/index.php?title=Rebuild&action=edit&redlink=1 "Rebuild (page does not exist)") [openssl](https://www.archlinux.org/packages/?name=openssl) using a [modified PKGBUILD](http://pastebin.com/pYcYf4dr). Then [restart](/index.php/Restart "Restart") `boinc.service`.

Your new work units should now be able to download. If you have any trouble, the original thread on the forum can be seen [here](https://bbs.archlinux.org/viewtopic.php?pid=1160393#p1160393).

## See also

*   [BOINC homepage](http://boinc.berkeley.edu/)
*   [List of BOINC projects](http://boinc.berkeley.edu/projects.php)
*   [Wikipedia entry](https://en.wikipedia.org/wiki/BOINC "wikipedia:BOINC")

Retrieved from "[https://wiki.archlinux.org/index.php?title=BOINC&oldid=400170](https://wiki.archlinux.org/index.php?title=BOINC&oldid=400170)"