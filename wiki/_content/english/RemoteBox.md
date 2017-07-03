[RemoteBox](http://remotebox.knobgoblin.org.uk/) is an open source [VirtualBox](/index.php/VirtualBox "VirtualBox") remote client, written in Perl. In essence, you can remotely administer an installation of VirtualBox on a server, including its guests and interact with them as if they were running locally. VirtualBox is installed on 'the server' machine and RemoteBox runs on 'the client' machine. RemoteBox provides a complete GTK graphical interface with a look and feel very similar to that of VirtualBox's native GUI. If you're familiar with other virtualization software, such as VMWare ESX, then think of RemoteBox as the "poor man's" VI client.

## Contents

*   [1 Installation](#Installation)
    *   [1.1 VirtualBox web service](#VirtualBox_web_service)
*   [2 Connecting RemoteBox to the vboxweb service](#Connecting_RemoteBox_to_the_vboxweb_service)
*   [3 Troubleshooting](#Troubleshooting)
*   [4 External Resources](#External_Resources)

## Installation

RemoteBox can be installed on the client with the [remotebox](https://aur.archlinux.org/packages/remotebox/) package. It will pull in all the required GTK2 and Perl packages. However, an RDP client is also required, such as [freerdp](https://www.archlinux.org/packages/?name=freerdp) or [rdesktop](/index.php/Rdesktop "Rdesktop") and needs to be manually installed. As of this writing, [freerdp-git](https://aur.archlinux.org/packages/freerdp-git/) 2.0.0.beta1 has been tested and found working.

### VirtualBox web service

To use RemoteBox, you must have [VirtualBox](/index.php/VirtualBox "VirtualBox") installed on your server, along with [virtualbox-ext-oracle](https://aur.archlinux.org/packages/virtualbox-ext-oracle/) package. For a headless server not running a GUI, installing [virtualbox-headless](https://aur.archlinux.org/packages/virtualbox-headless/) is suggested. It is also suggested to install [virtualbox-guest-iso](https://www.archlinux.org/packages/?name=virtualbox-guest-iso) on your server too.

On your server running VirtualBox, create a new user with a homedir and login shell, for example:

```
# useradd -m -g vboxusers -s /bin/bash vbox

```

This will create a new user 'vbox' with its primary group as 'vboxusers', a homedir and a login shell. The homedir is required for storing VirtualBox settings and configurations for virtual machines. The shell is required because otherwise, RemoteBox won't be able to login. Now give it a password and record it somewhere safe:

```
# passwd vbox

```

Create a custom `vboxweb-mod.service` file by copying `/usr/lib/systemd/system/vboxweb.service` to `/usr/lib/systemd/system/vboxweb-mod.service`

Modify `/usr/lib/systemd/system/vboxweb-mod.service` as follows:

```
[Unit]
Description=VirtualBox Web Service
After=network.target

[Service]
Type=forking
PIDFile=/run/vboxweb/vboxweb.pid
ExecStart=/usr/bin/vboxwebsrv --pidfile /run/vboxweb/vboxweb.pid --host <your server ip> --background
User=vbox
Group=vboxusers

[Install]
WantedBy=multi-user.target

```

Note: Do not forget to edit <your server ip> with your server's main IP address.

Create a tmpfile rule for your `vboxweb-mod.service`:

```
# echo "d /run/vboxweb 0755 vbox vboxusers" > /etc/tmpfiles.d/vboxweb-mod.conf

```

Manually create the `/run/vboxweb` directory for first start `vboxweb-mod.service`:

```
# mkdir /run/vboxweb
# chown vbox:vboxusers /run/vboxweb
# chmod 755 /run/vboxweb

```

You can enable logging by editing the ExecStart line in the unit file above to include the `--logfile <logfile location>` directive. To enable verbose logging, you can also include the `--verbose` directive. Make sure the vbox user can create and write to the logile you are configuring.

[Start](/index.php/Start "Start")/[enable](/index.php/Enable "Enable") `vboxweb-mod.service`

## Connecting RemoteBox to the vboxweb service

Open RemoteBox and click the `Connect` button. Specify the following:

```
URL: http:<your server ip>:18083
Username: vbox
Password: <password recorded earlier>

```

To make it easier to connect during future sessions, after logging in goto `File` and create a new connection profile.

## Troubleshooting

If you encounter a login problem connecting to the server, first check that the service is running. From the server console, use

```
# systemctl status vboxweb-mod.service

```

It should output that it is running. If not, check logging with `journalctl` and, if you configured a `logfile`, the vboxweb service logfile for any leads.

Even on verbose, vboxweb service might not give you any lead as to what is the problem. In that case, you can become `vbox` and run `vboxwebsrv` from the command line.

```
# su vbox

```

Then manually start vboxwebsrv:

```
$ /usr/bin/vboxwebsrv --pidfile /run/vboxweb/vboxweb.pid --host <your server ip>

```

Omit the `--background` and `--logfile` directives. If the service starts, the problem could be permissions to the log file. Leave it running and check if you can connect with RemoteBox from the client.

If you still can't connect, you can stop the service with `Ctrl-c` and start it with the `--background` directive. Next, check using netstat or something similar whether vboxwebsrv is listening on port 18083\. If you see a different port, try connecting your RemoteBox on that port instead.

Another reason could be a firewall, either on your server, or on your client.

If you are getting the following error message:

```
vboxwebsrv: error: failed to initialize COM! hrc=NS_ERROR_FAILURE

```

Check that your home directory is writable for the user 'vbox'. Also, check the `~/.config/VirtualBox` file gets created and populated with config files.

## External Resources

*   [RemoteBox Home Page](http://remotebox.knobgoblin.org.uk/)
*   [RemoteBox Manual](http://remotebox.knobgoblin.org.uk/docs/remotebox.pdf)
*   [RemoteBox on Sourceforge](https://sourceforge.net/projects/remotebox/)