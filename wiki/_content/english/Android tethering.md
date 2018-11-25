[Tethering](https://en.wikipedia.org/wiki/Tethering "wikipedia:Tethering") is a way to have internet access on your PC through your smartphone using its network connection. USB tethering and Wi-Fi access point tethering are natively supported since Android 2.2 "Froyo".

## Contents

*   [1 Wi-Fi access point](#Wi-Fi_access_point)
*   [2 USB tethering](#USB_tethering)
    *   [2.1 Using systemd-networkd with udev](#Using_systemd-networkd_with_udev)
*   [3 USB tethering with AziLink](#USB_tethering_with_AziLink)
    *   [3.1 Tools needed](#Tools_needed)
        *   [3.1.1 Configuring the phone connection in Arch Linux](#Configuring_the_phone_connection_in_Arch_Linux)
    *   [3.2 Procedure](#Procedure)
*   [4 USB tethering with EasyTether](#USB_tethering_with_EasyTether)
*   [5 Tethering via Bluetooth](#Tethering_via_Bluetooth)
*   [6 Tethering with SOCKS proxy](#Tethering_with_SOCKS_proxy)
    *   [6.1 Tools needed](#Tools_needed_2)
    *   [6.2 Instructions](#Instructions)
        *   [6.2.1 Tetherbot](#Tetherbot)
        *   [6.2.2 Proxoid](#Proxoid)

## Wi-Fi access point

Using an Android phone as a Wi-Fi access point (to a 3G/4G mobile internet connection) is available for devices running Android 2.2 "Froyo" or newer.

Enable it via one of the following:

*   *Settings > Wireless & networks > Internet tethering > Wi-Fi access point*
*   *Settings > More... > Tethering & mobile hotspot > Mobile Wi-Fi hotspot*

**Note:** On some phones, this method will discharge the battery rapidly and tends to cause intense heating, unlike USB.

## USB tethering

USB tethering is available since Android 2.2 "Froyo".

*   Connect the phone to your computer via USB (the USB connection mode -- Phone Portal, Memory Card or Charge only -- is not important, but please note that you will not be able to change the USB mode during tethering)
*   Enable the tethering option from your phone. This is usually done from one of:
    *   *Settings -> Wireless & networks -> Internet tethering* (or *Tethering & portable hotspot*, for more recent versions)
    *   *Settings -> More... -> Tethering & mobile hotspot -> USB tethering*
*   Follow [Network configuration](/index.php/Network_configuration "Network configuration").

**Note:** The network interface name may change depending on the USB port you use. You may want to [change the interface name](/index.php/Network_configuration#Change_interface_name "Network configuration") to create a unique name for your device regardless of the USB port.

*   If you're using a cellular data plan and you have recently entered a new billing period, you may need to restart your phone.

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

 `/etc/systemd/network/50-enp0s26u1u2.network` 
```
[Match]
Name=enp0s26u1u2

[Network]
DHCP=ipv4

```

## USB tethering with AziLink

This method works for all known Android versions and requires neither root access nor modifications in the phone. It does not require changes to your browser. All network traffic is transparently handled (except ICMP pings). It may be somewhat CPU intensive on the phone at high usage rates (a 500 kBytes/sec data transfer rate may take more than 50% of phone CPU).

### Tools needed

For Arch, you need to [install](/index.php/Install "Install") the [openvpn](https://www.archlinux.org/packages/?name=openvpn) package. You will also need to install the [android-tools](https://www.archlinux.org/packages/?name=android-tools) package for the *adb* tool and [android-udev](https://www.archlinux.org/packages/?name=android-udev) which sets up the correct `/usr/lib/udev/rules.d/51-android.rules` file for your device to be recognized. On the phone, you need the [azilink.apk](http://lfx.org/azilink/azilink.apk) ([azilink homepage](https://github.com/aziwoqpd/azilink)). The android application acts as a NAT, adb forwards the ports to your phone, and your openvnp setup will connect to it.

#### Configuring the phone connection in Arch Linux

So that you do not have to run adb as root, we are going to grant your user permissions to your usb device. Make sure you have turned on USB debugging on the phone (usually in Settings -> Applications -> Development -> USB debugging) so that it will be shown as a device, and that it is plugged in to your computer via the USB cable. You should see it with you run the `lsusb` command. Original azi link instructions are [here](https://raw.githubusercontent.com/aziwoqpd/azilink/master/HOWTO)

The device should be listed. Example output for the Acer Liquid phone:

```
Bus 001 Device 006: ID **0502**:3202 Acer, Inc. 

```

Then, create the following file, replacing *ciri* by your own Linux user name, and **0502** by the vendor ID of your own phone:

 `/etc/udev/rules.d/51-android.rules` 
```
SUBSYSTEM=="usb", ATTR(idVendor)=="0502", MODE="0666" OWNER="ciri"

```

As root run the `udevadm control --reload` command to make the change effective. To make sure the change took effect, run 'adb devices' and it should say 'device' instead of 'unauthorized'. Another way to make it take effect is to reboot. Another test is to run `adb shell` to get to your phones unix prompt.

### Procedure

Run the AziLink application in the phone and select "About" at the bottom to receive instructions, which basically are:

1.  You will have to enable USB debugging on the phone if it was not already enabled (usually in Settings -> Applications -> Development -> USB debugging).
2.  Connect the phone with the USB cable to the PC.
3.  Run AziLink and make sure that the **Service active** option at the top is checked.
4.  Run the following commands in your Linux PC:

	 `$ adb forward tcp:41927 tcp:41927` 

	 `# openvpn azilink.ovpn` 

azilink.ovpn source from [here](https://raw.githubusercontent.com/aziwoqpd/azilink/master/azilink.ovpn)

 `azilink.ovpn` 
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

You may need to manually update the contents of [resolv.conf](/index.php/Resolv.conf "Resolv.conf") to

 `/etc/resolv.conf` 
```
nameserver 192.168.56.1

```

If you're running NetworkManager, you may need to stop it before running OpenVPN.

## USB tethering with EasyTether

Get the [easytether](http://www.mobile-stream.com/easytether/drivers.html) linux client software. The commands to set it up and run it are as follows.

```
# pacman -U easytether-0.8.5-2-x86_64.pkg.tar.xz
# easytether-usb
# dhcpcd tap-easytether

```

Make sure you have the EasyTether android app installed on your phone for it to connect to. Note: The Lite app disables some connections and you must have the paid app for full functionality. For this reason, using the AziLink setup is recommended instead.

## Tethering via Bluetooth

Android (from at least 4.0 onwards, possibly earlier) can provide a Bluetooth personal-area network (PAN) in access point mode.

NetworkManager can perform this action and handle the network initialisation itself; consult its documentation for more details.

Alternatively: pair and ensure you can connect your computer and Android device, as described on [Bluetooth](/index.php/Bluetooth "Bluetooth"), then, substituting the address of the device (here given as `AA_BB_CC_DD_EE_FF`), do:

 `$ dbus-send --system --type=method_call --dest=org.bluez /org/bluez/hci0/dev_AA_BB_CC_DD_EE_FF org.bluez.Network1.Connect string:'nap'` 

This will create a network interface `bnep0`. Finally, [configure a network connection](/index.php/Network_configuration "Network configuration") on this interface; Android offers DHCP by default.

## Tethering with SOCKS proxy

With this method tethering is achieved by port forwarding from the phone to the PC. This is suitable only for browsing. For Firefox, you should set **network.proxy.socks_remote_dns** to **true** in **about:config** ( address bar )

### Tools needed

*   The [android-tools](https://www.archlinux.org/packages/?name=android-tools) and [android-udev](https://www.archlinux.org/packages/?name=android-udev) packages
*   USB connection cable from your phone to PC
*   Either [Tetherbot](http://graha.ms/androidproxy/) or [Proxoid](https://code.google.com/p/proxoid/)

### Instructions

#### Tetherbot

Follow the instructions under **Using the Socks Proxy** on [[1]](http://graha.ms/androidproxy/).

#### Proxoid

Follow the instructions demonstrated in the following [link](http://www.linux-magazine.com/Online/Blogs/Productivity-Sauce/Tether-an-Android-Phone-Using-Proxoid).