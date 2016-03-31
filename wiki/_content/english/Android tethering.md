Tethering is a way to have internet access on your PC through your smartphone using its network connection. USB tethering and Wi-Fi access point tethering are natively supported since Android Froyo (2.2). In older versions of the Android OS, most unofficial ROMs have this option enabled.

## Contents

*   [1 Wi-Fi access point](#Wi-Fi_access_point)
*   [2 USB tethering](#USB_tethering)
    *   [2.1 Tools Needed](#Tools_Needed)
    *   [2.2 Procedure](#Procedure)
        *   [2.2.1 Using systemd-networkd with udev](#Using_systemd-networkd_with_udev)
*   [3 USB tethering with OpenVPN](#USB_tethering_with_OpenVPN)
    *   [3.1 Tools Needed](#Tools_Needed_2)
        *   [3.1.1 Configuring the phone connection in Arch Linux](#Configuring_the_phone_connection_in_Arch_Linux)
    *   [3.2 Procedure](#Procedure_2)
    *   [3.3 Troubleshooting](#Troubleshooting)
        *   [3.3.1 DNS](#DNS)
        *   [3.3.2 NetworkManager](#NetworkManager)
*   [4 Tethering via Bluetooth](#Tethering_via_Bluetooth)
*   [5 Tethering with SOCKS proxy](#Tethering_with_SOCKS_proxy)
    *   [5.1 Tools Needed](#Tools_Needed_3)
    *   [5.2 Instructions](#Instructions)
        *   [5.2.1 Tetherbot](#Tetherbot)
        *   [5.2.2 Proxoid](#Proxoid)
*   [6 ClockworkMod Tether](#ClockworkMod_Tether)

## Wi-Fi access point

Using an Android phone as a Wi-Fi access point (using 3G) has been accessible by default since Froyo (Android 2.2) without needing to root the phone. Moreover, this method will discharge the battery rapidly and tends to cause intense heating, unlike USB. See : **menu/wireless & networks/Internet tethering/Wi-Fi access point**

## USB tethering

### Tools Needed

*   Root access to the phone (for old Android versions, Froyo (Android 2.2) and beyond can do it natively)
*   USB connection cable from your phone to PC

### Procedure

*   Disconnect your computer from any wireless or wired networks
*   Connect the phone to your computer using the USB cable (the USB connection mode -- Phone Portal, Memory Card or Charge only -- is not important, but please note that you will not be able to change the USB mode during tethering)
*   Enable the tethering option from your phone. This is usually done from `Settings --> Wireless & Networks --> Internet tethering` (or `Tethering & portable hotspot`, for more recent versions)
*   Make sure that the USB interface is recognized by the system by using the following command:

	 `$ ip link` 

	You should be able to see a `usb0` or `enp?s??u?` device listed like this (notice the enp0s20u3 device).

 `# ip link` 
```
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN mode DEFAULT group default 
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
2: enp4s0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc pfifo_fast state UP mode DEFAULT group default qlen 1000
    link/ether ##:##:##:##:##:## brd ff:ff:ff:ff:ff:ff
3: wlp2s0: <BROADCAST,MULTICAST> mtu 1500 qdisc mq state DOWN mode DEFAULT group default qlen 1000
    link/ether ##:##:##:##:##:## brd ff:ff:ff:ff:ff:ff
5: enp0s20u3: <BROADCAST,MULTICAST> mtu 1500 qdisc noop state DOWN mode DEFAULT group default qlen 1000
    link/ether ##:##:##:##:##:## brd ff:ff:ff:ff:ff:ff

```

**Note:** Take care to use the device name from your own system in the following commands.

**Warning:** The name may change depending on the usb port you use. You may want to [change the device name](/index.php/Network_configuration#Change_device_name "Network configuration") to create a unique name for your device regardless of the usb port.

*   The final step is to [configure a network connection](/index.php/Network_configuration#Configure_the_IP_address "Network configuration") on this interface. For example:

	 `# dhcpcd enp0s20u3` 

#### Using systemd-networkd with udev

Using [systemd-networkd](/index.php/Systemd-networkd "Systemd-networkd") you can automatically adjust the networking to use the phone as the gateway when plugged in.

 `/etc/udev/rules.d/90-android-tethering.rules` 
```
# Execute pairing program when appropriate
ACTION=="add|remove", SUBSYSTEM=="net", ATTR{idVendor}=="18d1" ENV{ID_USB_DRIVER}=="rndis_host", SYMLINK+="android", RUN+="/usr/bin/systemctl restart systemd-networkd.service"

```

You may have to adjust the `idVendor` attribute depending on your phone. You can check using *udevadm*:

```
$ udevadm info /sys/class/net/enp0s26u1u2

```

Then create the corresponding systemd-networkd file:

 `/etc/systemd/network/enp0s26u1u2.network` 
```
[Match]
Name=enp0s26u1u2

[Network]
DHCP=ipv4

```

## USB tethering with OpenVPN

This method works for any old Android version and requires neither root access nor modifications in the phone (it is also suitable for Android 2.2 and later, but no longer required).

It does not require changes to your browser. In fact, all network traffic is transparently handled for any PC application (except ICMP pings). It is somewhat CPU intensive on the phone at high usage rates (a 500 kBytes/sec data transfer rate may take more than 50% of phone CPU on a powerful Acer Liquid).

### Tools Needed

For Arch, you need to [install](/index.php/Install "Install") the [openvpn](https://www.archlinux.org/packages/?name=openvpn) package. It is also required to have the Android SDK installed (which can be obtained [here](http://developer.android.com/sdk/index.html) or from the AUR). On the phone, you need the [azilink](http://code.google.com/p/azilink/) application, which is a Java-based NAT that will communicate with OpenVPN on your computer.

#### Configuring the phone connection in Arch Linux

Once you have installed the Android SDK, in order to use the provided tools your phone must be properly set up in [udev](/index.php/Udev "Udev") and your Linux user needs to be granted rights. Otherwise you may need root privileges to use the Android SDK, which is not recommended. To perform this configuration, turn on USB debugging on the phone (usually in Settings -> Applications -> Development -> USB debugging), connect it to the PC by the USB cable and run the `lsusb` command. The device should be listed. Example output for the Acer Liquid phone:

```
Bus 001 Device 006: ID **0502**:3202 Acer, Inc. 

```

Then, create the following file, replacing *ciri* by your own Linux user name, and **0502** by the vendor ID of your own phone:

 `/etc/udev/rules.d/51-android.rules` 
```
SUBSYSTEM=="usb", ATTR(idVendor)=="0502", MODE="0666" OWNER="ciri"

```

As root run the `udevadm control restart` command (or reboot your computer) to make the change effective.

Now run in your linux PC the `adb shell` command from the Android SDK as plain (non root) user: you should get a unix prompt *in your phone*.

### Procedure

Run the AziLink application in the phone and select "About" at the bottom to receive instructions, which basically are:

1.  You will have to enable USB debugging on the phone if it was not already enabled (usually in Settings -> Applications -> Development -> USB debugging).
2.  Connect the phone with the USB cable to the PC.
3.  Run AziLink and make sure that the **Service active** option at the top is checked.
4.  Run the following commands in your Linux PC:

	 `$ adb forward tcp:41927 tcp:41927` 

	 `# openvpn AziLink.ovpn` 

 `AziLink.ovpn` 
```
dev tun
remote 127.0.0.1 41927 tcp-client
ifconfig 192.168.56.2 192.168.56.1
route 0.0.0.0 128.0.0.0
route 128.0.0.0 128.0.0.0
socket-flags TCP_NODELAY
keepalive 10 30
dhcp-option DNS 192.168.56.1

```

### Troubleshooting

#### DNS

You may need to manually update the contents of [resolv.conf](/index.php/Resolv.conf "Resolv.conf") to

 `/etc/resolv.conf` 
```
nameserver 192.168.56.1

```

#### NetworkManager

If you're running NetworkManager, you may need to stop it before running OpenVPN.

## Tethering via Bluetooth

Android (from at least 4.0 onwards, possibly earlier) can provide a Bluetooth personal-area network (PAN) in access point mode.

NetworkManager can perform this action and handle the network initialisation itself; consult its documentation for more details.

Alternatively: pair and ensure you can connect your computer and Android device, as described on [Bluetooth](/index.php/Bluetooth "Bluetooth"), then, substituting the address of the device (here given as `AA_BB_CC_DD_EE_FF`), do:

 `$ dbus-send --system --type=method_call --dest=org.bluez /org/bluez/hci0/dev_AA_BB_CC_DD_EE_FF org.bluez.Network1.Connect string:'nap'` 

This will create a network interface `bnep0`. Finally, [configure a network connection](/index.php/Network_configuration#Configure_the_IP_address "Network configuration") on this interface; Android offers DHCP by default.

## Tethering with SOCKS proxy

With this method tethering is achieved by port forwarding from the phone to the PC. This is suitable only for browsing. For Firefox, you should set **network.proxy.socks_remote_dns** to **true** in **about:config** ( address bar )

### Tools Needed

*   [android-sdk](https://aur.archlinux.org/packages/android-sdk/) and [android-sdk-platform-tools](https://aur.archlinux.org/packages/android-sdk-platform-tools/) from [AUR](/index.php/AUR "AUR") and [android-udev](https://www.archlinux.org/packages/?name=android-udev) from [official repositories](/index.php/Official_repositories "Official repositories")
*   USB connection cable from your phone to PC
*   Either [Tetherbot](http://graha.ms/androidproxy/) or [Proxoid](https://code.google.com/p/proxoid/)

### Instructions

#### Tetherbot

Follow the instructions under **Using the Socks Proxy** on [[1]](http://graha.ms/androidproxy/).

#### Proxoid

Follow the instructions demonstrated in the following [link](http://androidcommunity.com/forums/f23/android-usb-tethering-for-linux-using-proxoid-24875/)

## ClockworkMod Tether

Clockworkmod Tether is a tethering app for android, but also requires software installed on your desktop. The linux application is available at [clockworkmod.com](http://download.clockworkmod.com/tether/tether-linux.tgz).

*   Create a temporary symlink in `/usr/local/bin/python` to `/usr/bin/python2`, as multiple files refer to python2\. Then follow the instructions in the README file.

*   The included *adb* binary requires [Multilib](/index.php/Multilib "Multilib") and [installation](/index.php/Install "Install") of the [lib32-libstdc++5](https://www.archlinux.org/packages/?name=lib32-libstdc%2B%2B5) and [lib32-ncurses5-compat-libs](https://aur.archlinux.org/packages/lib32-ncurses5-compat-libs/) packages. Use *ldd* to find any other missing libraries.

When *adb* is working, the command line will repeated say "Checking phone status...". Make sure you launch the android app as well.