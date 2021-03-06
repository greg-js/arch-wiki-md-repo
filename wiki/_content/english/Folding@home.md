From the project [home page](http://folding.stanford.edu/):

	Help Stanford University scientists studying Alzheimer's, Huntington's, Parkinson's, and many cancers by simply running a piece of software on your computer. The problems we are trying to solve require so many calculations, we ask people to donate their unused computer power to crunch some of the numbers. In just 5 minutes... Add your computer to over 333,684 others around the world to form the world's largest distributed supercomputer.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
    *   [2.1 The graphical way](#The_graphical_way)
    *   [2.2 The terminal way](#The_terminal_way)
    *   [2.3 Run f@h with limited privileges](#Run_f@h_with_limited_privileges)
*   [3 Monitoring work-unit progress](#Monitoring_work-unit_progress)
*   [4 See also](#See_also)

## Installation

[Install](/index.php/Install "Install") the [foldingathome](https://aur.archlinux.org/packages/foldingathome/) package. In order to use your GPU for folding (highly recommended), you'll need the appropriate [OpenCL](/index.php/GPGPU#OpenCL "GPGPU") package for your GPU. Nvidia users can also use [CUDA](/index.php/CUDA "CUDA").

## Configuration

Run `/opt/fah/FAHClient --configure` as root to generate a configuration file at `/opt/fah/config.xml` (the Arch Linux team number is 45032). Alternately, you can write `/opt/fah/config.xml` by hand and use `/opt/fah/sample-config.xml` as a reference. With a config file in place, you can start the daemon, check its status, and make the daemon automatically start at boot time.

```
$ cd /opt/fah
# ./FAHClient --configure

```

Then [start/enable](/index.php/Start/enable "Start/enable") the `foldingathome.service` systemd unit.

### The graphical way

You can manage the daemon by opening a web browser and heading to [http://localhost:7396/](http://localhost:7396/). Alternately, you can install [fahcontrol](https://aur.archlinux.org/packages/fahcontrol/) and use the FAHControl program.

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

### Run f@h with limited privileges

It's not necessary to run folding with root privileges. The easy way is to use [foldingathome-noroot](https://aur.archlinux.org/packages/foldingathome-noroot/), which makes use of `systemd`'s `DynamicUser` feature. Note that certain files are in different locations, and there is a script `/opt/fah/fah-config` to generate the `config.xml`. To set it up manually, read on.

* * *

Create a dedicated user `fah` for folding without critical privileges:

```
# useradd -u 999 -s /sbin/nologin fah

```

**Note:** If -u 999 is already taken, choose another number below 1000 to make login managers hide the user.

Now [edit](/index.php/Edit "Edit") the `foldingathome.service` to use the new user:

 `# systemctl edit foldingathome.service` 
```
[Service]
User=fah
WorkingDirectory=/var/lib/fah
ExecStart=
ExecStart=/opt/fah/FAHClient --config /var/lib/fah/config.xml --exec-directory=/opt/fah --data-directory=/var/lib/fah
```

Make the user `fah` own it:

```
# chown -R fah:fah /var/lib/fah

```

[Start](/index.php/Start "Start") `foldingathome.service`.

## Monitoring work-unit progress

There are several ways of monitoring the progress of your FAH clients, both on the command line and by GUI.

The FAHControl software distributed by folding at home provides you with efficient means to control remote hosts. Just add another client with the corresponding button "Add" and enter the name, ip address, port and password (if you set one) and hit save. The software should now try to establish a connection to the remote host and show you the progress in a seperate client tab.

In AUR there is [fahmon](https://aur.archlinux.org/packages/fahmon/), which provides a GUI with the ability to watch multiple clients and get info on the work-unit itself. Fahmon has a dedicated site at [http://www.fahmon.net/](http://www.fahmon.net/)

On the CLI, you can add a command to your shell configuration file (e.g: *.bashrc* or *.zshrc*). Replace *fah_user* with the actual user first.

```
fahstat() {
        echo
        echo $(date)
        echo
        cat /opt/fah/*fah_user*/unitinfo.txt
}

```

Or for multiple clients :

```
 fahstat() {
         echo
         echo $(date)
         echo
         echo "Core 1:";cat /opt/fah/*fah_user*/unitinfo.txt
         echo
         echo "Core 2:";cat /opt/fah2/*fah_user*/unitinfo.txt
 }

```

Also, replacing `cat` with `tail -n1` will give just the percentage of work unit complete.

On foldingathome-smp 6.43, the *unitinfo.txt* file is not placed inside the user folder. The correct directory would be `/opt/fah-smp/unitinfo.txt`.

## See also

*   Folding@home [site](http://folding.stanford.edu/)
*   Folding@home [FAQ](http://folding.stanford.edu/home/faq/)
*   Folding@home [Configuration Guide](http://folding.stanford.edu/home/guide/configuration-guide/)
*   Folding@home [SMP Client FAQ](http://folding.stanford.edu/home/faq/faq-smp)
*   Arch Folding@home [team page](http://fah-web.stanford.edu/cgi-bin/main.py?qtype=teampage&teamnum=45032)
*   Extended Arch team statistics in [extremeoverclocking.com](http://folding.extremeoverclocking.com/team_summary.php?s=&t=45032)