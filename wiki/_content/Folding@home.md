# Folding@home

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

From the project [home page](http://folding.stanford.edu/):

_Help Stanford University scientists studying Alzheimer's, Huntington's, Parkinson's, and many cancers by simply running a piece of software on your computer. The problems we are trying to solve require so many calculations, we ask people to donate their unused computer power to crunch some of the numbers. In just 5 minutes... Add your computer to over 333,684 others around the world to form the world's largest distributed supercomputer._

## Contents

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
    *   [2.1 The graphical way](#The_graphical_way)
    *   [2.2 The terminal way](#The_terminal_way)
*   [3 Multi-Core CPUs and Folding@home](#Multi-Core_CPUs_and_Folding.40home)
    *   [3.1 A quick note on hyperthreading](#A_quick_note_on_hyperthreading)
    *   [3.2 Multiple Folding@home installs](#Multiple_Folding.40home_installs)
*   [4 Monitoring work-unit progress](#Monitoring_work-unit_progress)
*   [5 See also](#See_also)

## Installation

Install [foldingathome](https://aur.archlinux.org/packages/foldingathome/)<sup><small>AUR</small></sup> from the [AUR](/index.php/AUR "AUR").

## Configuration

Run `/opt/fah/FAHClient --configure` as root to generate a configuration file at `/opt/fah/config.xml` (the Arch Linux team number is 45032). Alternately, you can write `opt/fah/config.xml` by hand and use `/opt/fah/sample-config.xml` as a reference. With a config file in place, you can start the daemon, check its status, and make the daemon automatically start at boot time.

```
$ cd /opt/fah
# ./FAHClient --configure
# systemctl start foldingathome
$ systemctl status foldingathome
# systemctl enable foldingathome

```

### The graphical way

You can manage the daemon by opening a web browser and heading to [http://localhost:7396/](http://localhost:7396/). Alternately, you can install [fahcontrol](https://aur.archlinux.org/packages/fahcontrol/)<sup><small>AUR</small></sup> and use the FAHControl program.

The daemon can also be controlled remotely. Instructions for doing so are listed in `/opt/fah/sample-config.xml`. Remember to open firewall ports if necessary.

### The terminal way

To see the current progress of foldingathome, simply `$ tail /opt/fah/log.txt`.

The behaviour of foldingathome can be customized by editing `/opt/fah/config.xml`. Some options that can be specified:

*   bigpackets, defines whether you will accept memory intensive work loads. If you have no problem with Folding@home using up more of your RAM, then set this to big. Other settings are normal and small.
*   passkey, to uniquely identify you. Though not needed, it provides some measure of security. For details, see [[1]](http://folding.stanford.edu/English/FAQ-passkey)

```
<passkey v='passkey'/>

```

*   Slots for CPU or GPU

```
<slot id='0' type='CPU'/>

```

## Multi-Core CPUs and Folding@home

As of version 7.x, multi-core CPUs no longer require any special configuration. If you are using version 6.x, read on.

### A quick note on hyperthreading

[![Tango-emblem-important.png](/images/c/c8/Tango-emblem-important.png)](/index.php/File:Tango-emblem-important.png)

[![Tango-emblem-important.png](/images/c/c8/Tango-emblem-important.png)](/index.php/File:Tango-emblem-important.png)

**The factual accuracy of this article or section is disputed.**

**Reason:** "Hyperthreading is usually enabled in the BIOS by default, and we recommend that it stays enabled, as the SMP cores can use it to process Work Units faster." [[2]](http://folding.stanford.edu/English/FAQ-SMP#ntoc6) (Discuss in [Talk:Folding@home#](https://wiki.archlinux.org/index.php/Talk:Folding@home))

If you have a single-core hyperthreading CPU, you may be tempted to follow the multi-core instructions. It is highly recommenced that you do **not** do this as the Folding@home team prefers fewer results quickly, than more results slowly. There is also a time-limit on work-units, so if it runs slower, your work-units may not be returned in time, and so distributed to another user. If you have one core, run one folding process.

### Multiple Folding@home installs

Multiple installations of FAH on a single machine are useless, as in v7, you can use slots for every workload. The software is uniform now for GPU and CPU.

## Monitoring work-unit progress

There are several ways of monitoring the progress of your FAH clients, both on the command line and by GUI.

The FAHControl software distributed by folding at home provides you with efficient means to control remote hosts. Just add another client with the corresponding button "Add" and enter the name, ip address, port and password (if you set one) and hit save. The software should now try to establish a connection to the remote host and show you the progress in a seperate client tab.

In AUR there is [fahmon](https://aur.archlinux.org/packages/fahmon/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/fahmon)]</sup>, which provides a GUI with the ability to watch multiple clients and get info on the work-unit itself. Fahmon has a dedicated site at [http://www.fahmon.net/](http://www.fahmon.net/)

On the CLI, you can add a command to your shell configuration file (e.g: _.bashrc_ or _.zshrc_). Replace _fah_user_ with the actual user first.

```
fahstat() {
        echo
        echo $(date)
        echo
        cat /opt/fah/_fah_user_/unitinfo.txt
}

```

Or for multiple clients :

```
 fahstat() {
         echo
         echo $(date)
         echo
         echo "Core 1:";cat /opt/fah/_fah_user_/unitinfo.txt
         echo
         echo "Core 2:";cat /opt/fah2/_fah_user_/unitinfo.txt
 }

```

Also, replacing `cat` with `tail -n1` will give just the percentage of work unit complete.

On foldingathome-smp 6.43, the _unitinfo.txt_ file is not placed inside the user folder. The correct directory would be `/opt/fah-smp/unitinfo.txt`.

## See also

*   Folding@home [site](http://folding.stanford.edu/)
*   Folding@home [FAQ](http://folding.stanford.edu/home/faq/)
*   Folding@home [Configuration Guide](http://folding.stanford.edu/home/guide/configuration-guide/)
*   Folding@home [SMP Client FAQ](http://folding.stanford.edu/home/faq/faq-smp)
*   Arch Folding@home [team page](http://fah-web.stanford.edu/cgi-bin/main.py?qtype=teampage&teamnum=45032)
*   Extended Arch team statistics in [extremeoverclocking.com](http://folding.extremeoverclocking.com/team_summary.php?s=&t=45032)

Retrieved from "[https://wiki.archlinux.org/index.php?title=Folding@home&oldid=392138](https://wiki.archlinux.org/index.php?title=Folding@home&oldid=392138)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [Mathematics and science](/index.php/Category:Mathematics_and_science "Category:Mathematics and science")

Hidden categories:

*   [Pages or sections flagged with Template:Accuracy](/index.php/Category:Pages_or_sections_flagged_with_Template:Accuracy "Category:Pages or sections flagged with Template:Accuracy")
*   [Pages with broken package links](/index.php/Category:Pages_with_broken_package_links "Category:Pages with broken package links")