From the [USB/IP site](http://usbip.sourceforge.net/):

	*USB/IP Project aims to develop a general USB device sharing system over IP network. To share USB devices between computers with their full functionality, USB/IP encapsulates "USB I/O messages" into TCP/IP payloads and transmits them between computers.*

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Installation](#Installation)
*   [2 Usage](#Usage)
    *   [2.1 Server setup](#Server_setup)
        *   [2.1.1 Binding with systemd service](#Binding_with_systemd_service)
    *   [2.2 Client setup](#Client_setup)
    *   [2.3 Disconnecting devices](#Disconnecting_devices)
*   [3 Man page](#Man_page)
*   [4 See also](#See_also)

## Installation

[Install](/index.php/Install "Install") [usbip](https://www.archlinux.org/packages/?name=usbip).

## Usage

### Server setup

The server should have the physical USB device connected to it, and the `usbip_host` USB/IP [kernel module](/index.php/Kernel_module "Kernel module") loaded. Then [start](/index.php/Start "Start") and [enable](/index.php/Enable "Enable") the USB/IP systemd service `usbipd.service`.

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

So, e.g., to share the device having *busid* 1-1, one should [start](/index.php/Start "Start") and/or [enable](/index.php/Enable "Enable") `usbip-bind@1-1.service`.

### Client setup

Make sure the `vhci-hcd` [kernel module](/index.php/Kernel_module "Kernel module") is loaded.

Then list devices available on the server:

```
$ usbip list -r *server_IP_address*

```

Attach the required device. For example, to attach the device having *busid* 1-1.5:

```
$ usbip attach -r *server_IP_address* -b 1-1.5

```

### Disconnecting devices

A device can be disconnected only after detaching it on the client.

List attached devices:

```
$ usbip port

```

Detach the device:

```
$ usbip detach -p *port_number*

```

Unbind the device on the server:

```
$ usbip unbind -b *busid*

```

**Note:** USB/IP by default requires port 3240 to be open. If a firewall is running, make sure that this port is open. For detailed instruction on configuring the firewall, go to [Category:Firewalls](/index.php/Category:Firewalls "Category:Firewalls")

## Man page

See [usbip(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/usbip.8).

## See also

*   [Official USB/IP project site](http://usbip.sourceforge.net/)
*   [Linux Kernel "README for usbip-utils"](https://www.kernel.org/doc/readme/tools-usb-usbip-README)
*   ["How To Setup and use USB/IP"](https://developer.ridgerun.com/wiki/index.php?title=How_to_setup_and_use_USB/IP)