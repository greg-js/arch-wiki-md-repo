[USBGuard](https://github.com/dkopecek/usbguard) offers a white/black-listing mechanism for USB-devices. Inspiration for this is drawn from exploits like BadUSB. It makes use of a device blocking infrastructure included in the Linux kernel and consists of a daemon and some front-ends.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
*   [3 Usage](#Usage)
    *   [3.1 Rules](#Rules)
*   [4 See also](#See_also)

## Installation

[Install](/index.php/Install "Install") the [usbguard](https://www.archlinux.org/packages/?name=usbguard) package, or [usbguard-git](https://aur.archlinux.org/packages/usbguard-git/) for the development version. Qt applet was removed in USBGuard 0.7.5 and it is going to be maintained in a simplified form as a separate project later. [[1]](https://github.com/USBGuard/usbguard/releases/tag/usbguard-0.7.5)

## Configuration

The main configuration file is found in `/etc/usbguard/usbguard-daemon.conf`. To edit it, you need root privileges.

If you want to control the daemon via IPC, be sure to add your username to `IPCAllowedUsers` or your group to `IPCAllowedGroups` to make rules persistent. In most cases, you want this.

By default, USBGuard blocks all newly connected devices, and devices connected before daemon startup are left as is. This can be changed with the `PresentDevicePolicy` option. Setting this key to `apply-policy` is the most secure setting, which ensures security even when the daemon hits a restart.

With the key `ImplicitPolicyTarget` you can configure the default treatment of devices, if no rules match. The most secure option here is `block`.

For an in-depth documentation of configuration see the very well commented configuration file.

## Usage

USBGuard has a core daemon, a CLI, a DBUS interface and an API via libusbguard.

**Warning:** Make sure to actually configure the daemon before starting/enabling it or all USB devices will immediately be blocked!

If you want to use the Qt GUI or another program communicating via DBUS, [enable](/index.php/Enable "Enable") and [start](/index.php/Start "Start") `usbguard-dbus.service`.

If you only want to communicate via API (with the CLI tool or another software using libusbguard) [enable](/index.php/Enable "Enable") and [start](/index.php/Start "Start") `usbguard.service`.

The CLI is available via `usbguard`.

See the according man pages for more info.

### Rules

To configure USBGuard to your needs, you can edit `/etc/usbguard/rules.conf`. However manual editing of the rules is normally not necessary. You can generate a ruleset based on your currently attached USB devices by executing `usbguard generate-policy > /etc/usbguard/rules.conf` as root.

The rules syntax is formally explained [here](https://github.com/USBGuard/usbguard/blob/master/doc/man/usbguard-rules.conf.5.adoc). An example for a hp printer connected via USB can look like this:

```
allow id 03f0:0c17 serial "00CNFD234631" name "hp LaserJet 2020" hash "a0ef07fceb6fb77698f79a44a450121m" parent-hash "69d19c1a5733a31e7e6d9530e6k434a6" with-interface { 07:01:03 07:01:02 07:01:01 }

```

A rule begins with a policy. `allow` whitelists a device, `block` stops the device from being processed now and `reject` removes the device from the system. Then follows a set of attributes with their options, as detailed below.

| Attribute | Description |
| id usb-device-id | Match a USB device ID. |
| id [operator] { usb-device-id ... } | Match a set of USB device IDs. |
| hash "value" | Match a hash computed from the device attribute values and the USB descriptor data. The hash is computed for every device by USBGuard. |
| hash [operator] { "value" ... } | Match a set of device hashes. |
| parent-hash "value" | Match a hash of the parent device. |
| parent-hash [operator] { "value" ... } | Match a set of parent device hashes. |
| name "device-name" | Match the USB device name attribute. |
| name [operator] { "device-name" ... } | Match a set of USB device names. |
| serial "serial-number" | Match the USB iSerial device attribute. |
| serial [operator] { "serial-number" ... } | Match a set of USB iSerial device attributes. |
| via-port "port-id" | Match the USB port through which the device is connected. Note that some systems have unstable port numbering which change after the system reboots or certain kernel modules are reloaded (and maybe in other cases). Use the parent-hash attribute if you want to ensure that a device is connected via a specific parent device. |
| via-port [operator] { "port-id" ... } | Match a set of USB ports. |
| with-interface interface-type | Match an interface type that the USB device provides. |
| with-interface [operator] { interface-type interface-type ... } | Match a set of interface types against the set of interfaces that the USB device provides. |

## See also

*   [USBGuard Website](https://github.com/dkopecek/usbguard/)
*   [USBGuard component diagram](https://raw.githubusercontent.com/dkopecek/usbguard/master/doc/usbguard-component-diagram.png)
*   [BadUSB background info](https://srlabs.de/bites/usb-peripherals-turn/)
*   [Kernel interface for USB device control](https://www.kernel.org/doc/Documentation/usb/authorization.txt)