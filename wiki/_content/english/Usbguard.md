This software allows one to implement a white/black-listing mechanism for usb-devices. Inspiration for this is drawn from exploits like BadUSB. It makes use of a device blocking infrastructure included in the linux kernel and consists of a daemon and some front-ends.

## Contents

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
*   [3 Usage](#Usage)
    *   [3.1 Rules](#Rules)
*   [4 Weblinks](#Weblinks)

## Installation

[Install](/index.php/Install "Install") the [usbguard](https://aur.archlinux.org/packages/usbguard/) package, or [usbguard-git](https://aur.archlinux.org/packages/usbguard-git/) for the development version.

## Configuration

The main configuration file is found in `/etc/usbguard/usbguard-daemon.conf`. To edit it, you need root privileges.

If you want to control the daemon via IPC, be sure to add your username to `IPCAllowedUsers` or your group to `IPCAllowedGroups` to make rules persistent. In most cases, you want this.

Per default, usbguard blocks all newly connected devices and devices connected before daemon startup are left as is. This can be changed with the `PresentDevicePolicy` option. Setting this key to `apply-policy` is the most secure setting, which ensures security even when the daemon hits a restart.

With the key `ImplicitPolicyTarget` you can configure the default treatment of devices, if no rules match. The most secure option here is `block`.

For an in-depth documentation of configuration see the very well commented configuration file.

## Usage

USBGuard has a core deamon, a CLI, a QT GUI, a DBUS interface and an API via libusbguard. If you want to use the QT GUI or another program communicating via DBUS, enable and start `usbguard-dbus.service`. If you only want to communicate via API (with the CLI tool or another software using libusbguard) enable and start `usbguard.service`.

The CLI is available via `usbguard`.

See the according man pages for more info.

A QT applet can be started with `usbguard-applet-qt` and provides an interactive graphical interface.

### Rules

To configure usbguard to your needs, you can edit `/etc/usbguard/rules.conf`. However manual editing of the rules is normally not necessary.

The rules syntax is formally explained [here](https://github.com/dkopecek/usbguard#rule-language). An example for a hp printer connected via USB can look like this:

`allow id 03f0:0c17 serial "00CNFD234631" name "hp LaserJet 2020" hash "a0ef07fceb6fb77698f79a44a450121m" parent-hash "69d19c1a5733a31e7e6d9530e6k434a6" with-interface { 07:01:03 07:01:02 07:01:01 }`

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

## Weblinks

*   [USBGuard Website](https://github.com/dkopecek/usbguard/)
*   [USBGuard component diagram](https://raw.githubusercontent.com/dkopecek/usbguard/master/doc/usbguard-component-diagram.png)
*   [BadUSB background info](https://srlabs.de/bites/usb-peripherals-turn/)
*   [Kernel interface for USB device control](https://www.kernel.org/doc/Documentation/usb/authorization.txt)