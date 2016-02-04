# Weewx

[Weewx](http://weewx.com/) is a free, open source, software program, written in Python, which interacts with your weather station to produce graphs, reports, and HTML pages.

## Contents

*   [1 Prerequisites](#Prerequisites)
    *   [1.1 Using Pacman to Install Prerequisites](#Using_Pacman_to_Install_Prerequisites)
    *   [1.2 Using PIP to Install Prerequisites](#Using_PIP_to_Install_Prerequisites)
*   [2 Build and install](#Build_and_install)
*   [3 Running Weewx with systemd](#Running_Weewx_with_systemd)
    *   [3.1 As a Simple Service](#As_a_Simple_Service)
    *   [3.2 As a Forking Service](#As_a_Forking_Service)
*   [4 Getting graphs to work on Arch RaspberryPi](#Getting_graphs_to_work_on_Arch_RaspberryPi)

## Prerequisites

### Using Pacman to Install Prerequisites

Install [python2](https://www.archlinux.org/packages/?name=python2), [python2-configobj](https://www.archlinux.org/packages/?name=python2-configobj), [python2-cheetah](https://www.archlinux.org/packages/?name=python2-cheetah) and [python2-pillow](https://www.archlinux.org/packages/?name=python2-pillow) from the [official repositories](/index.php/Official_repositories "Official repositories"). You may be able to use [python2-imaging](https://aur.archlinux.org/packages/python2-imaging/) from the [AUR](/index.php/AUR "AUR") instead of [python2-pillow](https://www.archlinux.org/packages/?name=python2-pillow), but I have not tried this.

### Using PIP to Install Prerequisites

PIP is the native python package manager and can be used to install all the python prerequisites for WeeWX. Install the [python2-pip](https://www.archlinux.org/packages/?name=python2-pip) and [base-devel](https://www.archlinux.org/groups/x86_64/base-devel/) packages as a c-compiler is needed for both PIP to install both Cheetah and Pillow.

 `pacman -S base-devel python2-pip` 

From the [Weewx documentation](http://www.weewx.com/docs/setup.htm) install prerequisites 'pip' tab:

```
# python setup tool (pip)

# required packages:
sudo pip2 install configobj
sudo pip2 install Cheetah
sudo pip2 install pillow

# required if hardware is serial or USB:
sudo pip2 install pyserial
sudo pip2 install pyusb

# optional for extended almanac information:
sudo pip2 install pyephem

```

## Build and install

```
ln -s /usr/bin/python2 /usr/local/bin/python
./setup.py build
sudo ./setup.py install

```

Note that I have created a symlink so that "python" gives you python2 rather than python3\. That is because weewx requires python2, but python3 is default on Arch. I do not like this approach, and I'm sure there must a better way. See the installation notes under [Python](/index.php/Python "Python").

If you don't want to use a symlink call python2 directly as follows:

```
python2 ./setup.py build
sudo python2 ./setup.py install

```

You will also need PyUSB. I could not find a package for Arch, but it is easy enough to install from [https://walac.github.io/pyusb/](https://walac.github.io/pyusb/) . It uses setup.py, and installation instructions are included with the tarball. If you have installed [python2-pip](https://www.archlinux.org/packages/?name=python2-pip) you can use pip to download, build and install pyusb as follows:

```
sudo pip2 install pyusb

```

After installation, weewx would not run because I did not have permissions on the weewx installation or the usb device. The weewx installation by default goes in /home/weewx and is owned by root. For the device, run lsusb and look for a line like this:

```
Bus 002 Device 002: ID 0fde:ca01  

```

The device name for this example is /dev/bus/usb/002/002; modify yours to match the Bus and Device in the lsusb output.

I gave myself permissions like this:

```
sudo usermod -a -G adm my_username
sudo chgrp adm /dev/bus/usb/002/002
sudo chgrp -R adm /home/weewx
sudo chmod -R g+w /home/weewx

```

In retrospect it might have been easier just to chown all the files to myself, since I ended up running the weewx daemon as me. You could also create a weewx user to own the files and run the daemon, which would be the more "unixy" way.

After this it was just a matter of following the configuration instructions from the weewx docs, then running the daemon. Test the installation by running it in a terminal:

```
cd /home/weewx
./bin/weewxd weewx.conf

```

## Running Weewx with systemd

### As a Simple Service

Create a new file /etc/systemd/system/weewx.service containing:

```
[Unit]
Description=Daemon to control my Weewx weather station
After=ntpdate.service

[Service]
ExecStart=/home/weewx/bin/weewxd /home/weewx/weewx.conf  > /dev/null
Type=simple

[Install]
WantedBy=multi-user.target

```

This file is meant for the RaspberryPi - because the RPi has no system clock, systemctl will not start this service until after the ntp service has started, giving the system chance to sync the time before weewx starts up.

 `systemctl start weewx` 

### As a Forking Service

**Note:** Change the _After_ condition to match your setup, i.e., ntpd.service or ntpdate.service, etc.

Create a new file /usr/lib/systemd/system/weewx.service containing:

```
[Unit]
Description=Weewx weather station interface and internet weather updater
After=ntpd.service

[Service]
Type=forking
PIDFile=/var/run/weewx.pid
WorkingDirectory=/home/weewx
ExecStart=/home/weewx/bin/weewxd --daemon /home/weewx/weewx.conf
ExecStop=/bin/kill $MAINPID
ExecReload=/bin/kill -HUP $MAINPID

[Install]
WantedBy=multi-user.target

```

## Getting graphs to work on Arch RaspberryPi

To get the graphs to work on the RaspberryPI (arm6) you will need to compile your own version of PIL (not pillow) and have the truetype2 headers installed. For some reason the pillow version in the arch arm6 repository is compiled without truetype fonts.

To install PIL download the source from here: [http://www.pythonware.com/products/pil/](http://www.pythonware.com/products/pil/)

Then, after installing the arch developer tools: `pacman -S base-devel` Install the freetype2 tools: `pacman -S freetype2` You will then need to symbolic link the freetype2 directory to freetype because the PIL build looks for the freetype header files in the freetype directoy not in freetype2.: `ln -s /usr/include/freetype2 /usr/include/freetype` THEN you can build and install PIL from your build directory: `./setup.py install` 

Retrieved from "[https://wiki.archlinux.org/index.php?title=Weewx&oldid=412457](https://wiki.archlinux.org/index.php?title=Weewx&oldid=412457)"