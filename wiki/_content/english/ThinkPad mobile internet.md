Many Lenovo ThinkPads come with a mobile broadband modem. By inserting a SIM card into the modem, it is possible to use a cellular network to connect to the internet.

## Contents

*   [1 Requirements](#Requirements)
*   [2 Procedure](#Procedure)
*   [3 Alternative method](#Alternative_method)
*   [4 Troubleshooting](#Troubleshooting)
*   [5 See also](#See_also)

## Requirements

The broadband modems in newer ThinkPads use the QMI modem protocol---see [this article](http://sigquit.wordpress.com/2012/08/20/an-introduction-to-libqmi/) for more information. These modems will show up as `/dev/cdc-wdm` on the filesystem.

It is not yet (September 2014) possible to initialize a QMI modem for use on Linux. Use Windows to activate the modem using [Lenovo's activation app](http://support.lenovo.com/us/en/downloads/migr-68495) (or web search for "Lenovo mobile broadband" for the correct app for your modem). The modem will not work until it has been correctly initialized using the app.

## Procedure

[Install](/index.php/Install "Install") the [libqmi](https://www.archlinux.org/packages/?name=libqmi) package available in the [official repositories](/index.php/Official_repositories "Official repositories"), which provides the `qmicli` and `qmi-network` programs. Also install [net-tools](https://www.archlinux.org/packages/?name=net-tools), which provides the `ifconfig` command.

There is a [helper script](https://raw.githubusercontent.com/penguin2716/qmi_setup/master/qmi_setup.sh) for `qmi-network` available on GitHub. Save the script to somewhere in your `$PATH` and make it executable, and then review the script. The values of some of the variables might need to be changed, especially `WWAN_DEV`.

Load the kernel modules `qmi_wwan` and `qcserial`:

```
$ modprobe qmi_wwan
$ modprobe qcserial
```

Also read the readme on the [GitHub page of the QMI helper](https://github.com/penguin2716/qmi_setup) for any further prerequisites. In particular, you may need to set the APN provided by your cellular internet provider in `/etc/qmi-network.conf`.

 `/etc/qmi-network.conf`  `APN=foo.bar.net` 

Finally, running `qmi_setup.sh start` should start the cellular internet connection.

## Alternative method

Reference information: [http://www.thinkwiki.org/wiki/Qualcomm_Gobi_2000](http://www.thinkwiki.org/wiki/Qualcomm_Gobi_2000)

First of all you need to make sure what model your modem is. Open your thinkpads backplate and look for IC or FCC ID. For this example we're going to use GOBI2000 (IC: 2723A-GOBI2000, FCC ID: J9CGOBI2000-L)

Enable your modem device from you BIOS I/O settings.

Download the driver installer exe from support.lenovo.com/en_US/downloads/detail.page?DocID=DS001302 and extract it with Wine. It will unpack the drivers to ~/.wine/drive_c/DRIVERS/WWANQL. The unpacker will prompt you to install the drivers automatically after unpacking, but if you need the installer again it's GobiInstaller.msi in previously mentioned folder. The installer will in turn unpack the firmware images to ~/.wine/drive_c/Program\ Files\ \(x86\)/QUALCOMM/Images/Lenovo . Now refer to the reference information on what firmware you want/need. Generally you are good to go with the Generic UMTS and Default Firmware (Forlders 6 an UMTS)

Download gobi loader from [http://www.codon.org.uk/~mjg59/gobi_loader/](http://www.codon.org.uk/~mjg59/gobi_loader/), follow the instructions to make and install (you might need to 'sudo make install'). Now copy the 3 previous firmware files to /lib/firmware/gobi (if the folder doesn't exist, create it). Insert your sim card to the port found under your battery pack and restart. Your modem should now show up in your network manager.

## Troubleshooting

*   Ensure that you have initialized the modem on Windows.

## See also

*   [Thinkwiki](http://www.thinkwiki.org)