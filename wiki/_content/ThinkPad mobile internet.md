# ThinkPad mobile internet

Many Lenovo ThinkPads come with a mobile broadband modem. By inserting a SIM card into the modem, it is possible to use a cellular network to connect to the internet.

## Contents

*   [1 Requirements](#Requirements)
*   [2 Procedure](#Procedure)
*   [3 Troubleshooting](#Troubleshooting)
*   [4 See also](#See_also)

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

## Troubleshooting

*   Ensure that you have initialized the modem on Windows.

## See also

*   [Thinkwiki](http://www.thinkwiki.org)

Retrieved from "[https://wiki.archlinux.org/index.php?title=ThinkPad_mobile_internet&oldid=412188](https://wiki.archlinux.org/index.php?title=ThinkPad_mobile_internet&oldid=412188)"