From the [BOINC website](http://boinc.berkeley.edu/):

	Use the idle time on your computer (Windows, Mac, or Linux) to cure diseases, study global warming, discover pulsars, and do many other types of scientific research. It's safe, secure, and easy.

From [Wikipedia:BOINC](https://en.wikipedia.org/wiki/BOINC "wikipedia:BOINC"):

	The Berkeley Open Infrastructure for Network Computing (BOINC) is a non-commercial middleware system for volunteer and grid computing. It was originally developed to support the SETI@home project before it became useful as a platform for other distributed applications in areas as diverse as mathematics, medicine, molecular biology, climatology, and astrophysics. The intent of BOINC is to make it possible for researchers to tap into the enormous processing power of personal computers around the world.

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

Both packages install a [unit](/index.php/Systemd#Using_units "Systemd") file named `boinc-client.service`.

**Note:** In [boinc](https://www.archlinux.org/packages/?name=boinc) 7.10.3-1, the unit was renamed from `boinc.service` to `boinc-client.service`.

You will also need to add yourself to the `boinc` group in order for the manager to connect:

```
# usermod -a -G boinc $(whoami)

```

To generate the necessary files referenced in the next section, make sure to [start](/index.php/Start "Start") `boinc-client.service`.

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

To start the GUI, use the *boincmgr* command

```
$ boincmgr

```

BOINC should now take you through the process of attaching to a project. NB, some projects will let you create an account remotely via the GUI while some may require you to first create an account via their website. You can attach to multiple projects if you have the resources (disk space, time, CPU power). Do this via menu option *Tools / Attach to project*.

If BOINC did not ask you to connect to a project, then make sure you are connected to the daemon. Go to menu option *Advanced / Select computer*, choose your machine's name and enter the password. (To avoid this, make sure the above steps regarding gui_rpc_auth.cfg have been done.)

#### Projects using GPU

If you want to use your GPU, you need the proprietary nvidia or amd drivers. For ATI/AMD Cards you also need [Catalyst](/index.php/Catalyst "Catalyst") driver for stock kernel which you can get from AUR. For Nvidia, you also need the package [opencl-nvidia](https://www.archlinux.org/packages/?name=opencl-nvidia) located in extra. To prevent computing errors on x86_64 you most likely need the *OpenGL (Multilib)* package listed in [Xorg#Driver installation](/index.php/Xorg#Driver_installation "Xorg").

In addition, the boinc user should be in the video group:

```
# gpasswd -a boinc video

```

In order to suspend GPU computing when the computer is in use, the boinc user should have access to your X session so that mouse/keyboard input can be communicated to the client. This can be accomplished by installing the package [xorg-xhost](https://www.archlinux.org/packages/?name=xorg-xhost) (Extra) and executing the following command:

```
$ xhost si:localuser:boinc

```

You may want to [autostart that on Xorg startup](/index.php/Autostarting#On_Xorg_startup "Autostarting").

### BOINC via the CLI

Install [boinc-nox](https://www.archlinux.org/packages/?name=boinc-nox) to use BOINC on a headless system. Two command-line management tools are available: `boinccmd` and `boinc`. `boinccmd` is recommended. To use `boinccmd`, you must:

1.  Start the BOINC service.
2.  Provide `boinccmd` with a password for communicating with the service's RPC API.

To start the BOINC service, use the provided `boinc-client.service` unit file. (For more information, see [Systemd#Using units](/index.php/Systemd#Using_units "Systemd").) The first time BOINC starts, it will generate a password and save it to `/var/lib/boinc/gui_rpc_auth.cfg`. To provide `boinccmd` with this password, consider one of the following:

*   Provide the password as a command-line flag, e.g. `boinccmd --passwd abc123 --get_host_info`.
*   Ensure a file named `gui_rpc_auth.cfg` is present in the current directory.

That done, you can register with a project and attach BOINC to the project.

To register with a project, you may be able to use the command-line client, or you may need to register with a separate website. To register with a project from the command-line, pick a project from [BOINC Wiki Project List](https://boinc.berkeley.edu/wiki/Project_list), and execute a command like `boinccmd --passwd abc123 --create_account ${project_url} ${my_email} ${project_password} ${project_username}` . Regardless of how you register, you must obtain a key for each project you'd like BOINC to attach to. To attach BOINC to a project, execute a command like `boinccmd --passwd abc123 --project_attach ${project_url} ${project_key}` .

By default, BOINC uses at most 60% of available CPU time. If you wish to let boinc do more work, edit the CPU-related options in its configuration file:

 `/var/lib/boinc/global_prefs.xml` 
```
<global_preferences>
    <cpu_usage_limit>100.0</cpu_usage_limit>
    ...
</global_preferences>
```

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

	To run WUs (e.g. Climateprediction)

	[lib32-glibc](https://www.archlinux.org/packages/?name=lib32-glibc), [lib32-glib2](https://www.archlinux.org/packages/?name=lib32-glib2)

	To show graphics (e.g. Several projects of WCG, Climateprediction, Quake-Catcher Network)

	[lib32-pango](https://www.archlinux.org/packages/?name=lib32-pango), [lib32-libxi](https://www.archlinux.org/packages/?name=lib32-libxi), [lib32-mesa](https://www.archlinux.org/packages/?name=lib32-mesa), [lib32-libjpeg6-turbo](https://www.archlinux.org/packages/?name=lib32-libjpeg6-turbo), [lib32-libxmu](https://www.archlinux.org/packages/?name=lib32-libxmu), [lib32-glu](https://www.archlinux.org/packages/?name=lib32-glu) and [lib32-freeglut](https://www.archlinux.org/packages/?name=lib32-freeglut)

## Troubleshooting

### GPU missing

If you get this error :

 `GPU Missing` 

and the Work Unit does not start, you should [restart](/index.php/Daemons "Daemons") the `boinc-client.service` daemon.

This will happen if the BOINC daemon starts before the an X session is fully initialized.

### Laptop overheating and battery duration reduction

If you run BIONC on a laptop with the ondemand governor (the default), it will keep the CPUs at their maximum frequencies (over)heating them and decreasing battery duration. The best way to fix this is to tell the ondemand to not rise the CPU frequencies for BOINC:

 `# echo 1 >/sys/devices/system/cpu/cpufreq/ondemand/ignore_nice_load` 

To do this on boot, create the following tmpfiles.d config:

 `/etc/tmpfiles.d/ondemand-ignore-nice.conf`  `w /sys/devices/system/cpu/cpufreq/ondemand/ignore_nice_load - - - - 1` 

### Unable to download with World Community Grid

If you are unable to download new work units for the World Community Grid project, [makepkg](/index.php?title=Rebuild&action=edit&redlink=1 "Rebuild (page does not exist)") [openssl](https://www.archlinux.org/packages/?name=openssl) using a [modified PKGBUILD](http://pastebin.com/pYcYf4dr). Then [restart](/index.php/Restart "Restart") `boinc-client.service`.

Your new work units should now be able to download. If you have any trouble, the original thread on the forum can be seen [here](https://bbs.archlinux.org/viewtopic.php?pid=1160393#p1160393).

## See also

*   [BOINC homepage](http://boinc.berkeley.edu/)
*   [List of BOINC projects](http://boinc.berkeley.edu/projects.php)
*   [Wikipedia entry](https://en.wikipedia.org/wiki/BOINC "wikipedia:BOINC")