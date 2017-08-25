I have just bought this laptop from Packard Bell (model PB BU45 O O61). The configuration of xorg and wifi have been a bit (just a bit) difficult, so I will be posting here my configuration files and my experiences. **This wiki page is still a work in progress**, if somebody is having problems, just send me an email at yiyu dot jgl at gmail.

## Wifi configuration

The wireless card included in this laptop is an *Intel® Pro WLAN 3945 Internal Wireless (802.11a/b/g 54 Mbps)*. I think you can use the ipw drivers, but they will be deprecated in favour of new iwl drivers, so we will be using the last ones. You will need `iwlwifi` and `iwlwifi-3945-ucode` packages.

The configuration is standard, as with any other wlan (I will try to document it more extensively in the future, but you can find good general instructions in the wiki) except that the drivers gives some problems if you do not pass the `disable_hw_scan=1` option to the module when you load it into the kernel. To not have to do it manually each time, add this to your `/etc/modprobe.d/modprobe.conf`:

```
options iwl3945 disable_hw_scan=1

```

To test your wireless connection you can use the instructions found on [HOWTO-iwlwifi](http://intellinuxwireless.org/?p=iwlwifi&n=HOWTO-iwlwifi).

## Web cam

It works perfectly with the driver available in aur for syntek webcams: [stk11xx-svn](https://aur.archlinux.org/packages/stk11xx-svn/)

## Hibernation

If you want, you can hibernate and resume your system with the help of the kernel26suspend2 kernel. I just followed the steps in the wiki page, and then found my system was hanging during the hibernation. I solved the problems adding this two options to the kernel parameter in /boot/grub/menu.lst : highres=off nohz=off

I found this solution in a forum and do not know why it wasn't working or why it works now. Some help would be welcomed.