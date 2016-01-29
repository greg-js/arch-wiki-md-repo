# Bootchart

[Bootchart](https://meego.gitorious.org/meego-developer-tools/bootchart) is a handy tool used for profiling the Linux boot sequence, generally used for making your computer boot faster. It consists of the bootchartd daemon, which records and renders a chart of profiling data.

**Note:** Bootchart is now a part of systemd, see [Improve boot performance#Analyzing the boot process](/index.php/Improve_boot_performance#Analyzing_the_boot_process "Improve boot performance") for details. This page covers the original bootchart and bootchart2 (init daemon) before it was merged.

## Contents

*   [1 Installing Bootchart](#Installing_Bootchart)
*   [2 Running Bootchart](#Running_Bootchart)
    *   [2.1 Boot loader setup](#Boot_loader_setup)
*   [3 Generating a chart](#Generating_a_chart)
    *   [3.1 Troubleshooting](#Troubleshooting)
    *   [3.2 Example bootcharts](#Example_bootcharts)
        *   [3.2.1 Boot in 5 seconds](#Boot_in_5_seconds)
*   [4 Bootchart2](#Bootchart2)
    *   [4.1 Running Bootchart2](#Running_Bootchart2)
        *   [4.1.1 Boot loader setup](#Boot_loader_setup_2)
        *   [4.1.2 Configure Bootchart2](#Configure_Bootchart2)
            *   [4.1.2.1 Stop Bootchartd2 after login](#Stop_Bootchartd2_after_login)
    *   [4.2 Generating a chart](#Generating_a_chart_2)
*   [5 Useful links](#Useful_links)

## Installing Bootchart

Bootchart can be found in extra [bootchart](https://www.archlinux.org/packages/?name=bootchart).

## Running Bootchart

To make use of bootchart, you have to either set it as the init process in your boot loader or starting it manually from one of the init scripts (`rc.sysinit` preferably). Note that if you start bootchartd manually, you have to stop it manually too. In general, be extra careful with this step.

### Boot loader setup

This generally involves making a copy of the boot option you want to profile and adding `init=/usr/bin/bootchartd` to it. See [kernel parameters](/index.php/Kernel_parameters "Kernel parameters") for instructions. When started from the boot loader, bootchart will stop when you get to the login prompt.

## Generating a chart

Generating a bootchart involves running:

```
bootchart-render

```

in a folder to which you have write access. This will generate a `bootchart.png` image with your chart. You'll have to have a Java runtime installed and properly set up before you can do this.

### Troubleshooting

Bootchart-render cannot generate a 'bootchart.png' image and shows the error message:

```
/var/log/bootchart.tgz not found

```

It mostly means that bootchartd was unable to detect when the booting process was finished. This can happen when you are using different login manager than [KDM](/index.php/KDM "KDM") or GDM such as [SLiM](/index.php/SLiM "SLiM") or entrance. You have to open `/usr/bin/bootchartd` script and append those applications to `exit_proc` variable, for example:

```
# The processes we have to wait for
local exit_proc="gdmgreeter gdm-binary kdm_greet kdm slim"

```

If you are using no login manager, edit the `exit_proc` variable in this way:

```
# The processes we have to wait for
local exit_proc="login"

```

### Example bootcharts

#### Boot in 5 seconds

[LWN Article on fast booting netbooks](http://lwn.net/Articles/299483/)

This article is really awesome and along with a bunch of bootcharts provides some tips on how to boot faster. Some of those improvements are beyond reach of the ordinary user though (patching X.org, kernel, etc.).

## Bootchart2

**Note:** An alternative to Bootchart is [bootchart2](https://github.com/mmeeks/bootchart). It uses python for generating the final chart instead of a JVM, and only requires: pygtk, git and busybox. See GRUB and GRUB2 configuration bellow

### Running Bootchart2

#### Boot loader setup

This generally involves making a copy of the boot option you want to profile and adding `initcall_debug printk.time=y init=/usr/bin/bootchartd` to it. See [kernel parameters](/index.php/Kernel_parameters "Kernel parameters") for instructions. When started from the boot loader, bootchart2 will stop after either a default 120 seconds, or when you get to the login prompt (as opposite). Note that Bootchart2-git can also be run as a **systemd** service, as described in [Improve boot performance#Using bootchart2](/index.php/Improve_boot_performance#Using_bootchart2 "Improve boot performance")

#### Configure Bootchart2

##### Stop Bootchartd2 after login

Bootchart2 **/etc/bootchartd.conf**

```
EXIT_PROC="kdm_greet xterm konsole gnome-terminal metacity mutter compiz ldm icewm-session enlightenment"

```

can be adjusted, or left empty for logging to be stopped manually rather than at a predetermined programme start.

### Generating a chart

Is as straightforward with Bootchart2 as it is with Bootchart Legacy: After bootup, run

```
$ pybootchartgui -i 

```

to get an interactive chart rendering tool. You can get more details on the [Gentoo Wiki](http://wiki.gentoo.org/wiki/Bootchart2) until someone further edit this page.

Note that Bootchart2 can be used along with [E4rat](/index.php/E4rat "E4rat").

## Useful links

*   [Bootchart home page](http://www.bootchart.org/)

Retrieved from "[https://wiki.archlinux.org/index.php?title=Bootchart&oldid=400576](https://wiki.archlinux.org/index.php?title=Bootchart&oldid=400576)"