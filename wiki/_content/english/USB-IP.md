From the [USB/IP site](http://usbip.sourceforge.net/):

	*USB/IP Project aims to develop a general USB device sharing system over IP network. To share USB devices between computers with their full functionality, USB/IP encapsulates "USB I/O messages" into TCP/IP payloads and transmits them between computers.*

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Installation](#Installation)
*   [2 Usage](#Usage)
    *   [2.1 Server Setup](#Server_Setup)
        *   [2.1.1 Binding with systemd service](#Binding_with_systemd_service)
    *   [2.2 Client Setup](#Client_Setup)
    *   [2.3 Disconnecting Devices](#Disconnecting_Devices)
*   [3 Man Page](#Man_Page)
*   [4 See Also](#See_Also)

## Installation

[Install](/index.php/Install "Install") [usbip](https://www.archlinux.org/packages/?name=usbip).

## Usage

### Server Setup

The server should have the physical USB device connected to it.

Load the USB/IP kernel module:

```
$ sudo modprobe usbip_host

```

Start and Enable the USB/IP systemd service:

```
$ sudo systemctl start usbipd.service
$ sudo systemctl enable usbipd.service

```

List the connected devices:

```
$ usbip list -l

```

Bind the required device. For example, to share the device having *busid* 1-1.5:

```
$ usbip bind -b 1-1.5

```

To unbind the device:

```
$ usbip unbind -b 1-1.5

```

After binding, the device can be accessed from the client.

#### Binding with systemd service

In order to make binding persistent following systemd template unit file can be used:

 `/etc/systemd/system/usbip-bind@.service` 
```
[Unit]
 Description=USB-IP Binding on bus id %I
 After=network-online.target usbipd.service
 Wants=network-online.target
 Requires=usbipd.service
 #DefaultInstance=1-1.5

 [Service]
 Type=simple
 ExecStart=/usr/bin/usbip bind -b %i
 RemainAfterExit=yes
 ExecStop=/usr/bin/usbip unbind -b %i  
 Restart=on-failure

 [Install]
 WantedBy=multi-user.target
```

To bind the required device. For example to share the device having *busid* 1-1:

```
$ sudo systemctl enable usbip-bind\@1-1.service
$ sudo systemctl start usbip-bind\@1-1.service

```

### Client Setup

Load the VHCI kernel module:

```
$ sudo modprobe vhci-hcd

```

List devices available on the server:

```
$ usbip list -r <Server IP Address>

```

Attach the required device. For example, to attach the device having *busid* 1-1.5:

```
$ usbip attach -r <Server IP Address> -b 1-1.5

```

### Disconnecting Devices

A device can be disconnected only after detaching it on the client.

List attached devices:

```
$ usbip port

```

Detach the device:

```
$ usbip detach -p <Port Number>

```

Unbind the device on the server:

```
$ usbip unbind -b <busid>

```

**Note:** USB/IP by default requires port 3240 to be open. If a firewall is running, make sure that this port is open. For detailed instruction on configuring the firewall, go to [Category:Firewalls](/index.php/Category:Firewalls "Category:Firewalls")

## Man Page

See [usbip(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/usbip.8).

## See Also

*   [Official USB/IP Project Site](http://usbip.sourceforge.net/)
*   [Linux Kernel "README for usbip-utils"](https://www.kernel.org/doc/readme/tools-usb-usbip-README)
*   ["How To Setup and use USB/IP"](https://developer.ridgerun.com/wiki/index.php?title=How_to_setup_and_use_USB/IP)