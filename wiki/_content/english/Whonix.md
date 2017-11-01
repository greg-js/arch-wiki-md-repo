**This page is a work in progress.** I hope to be done by next week.

[Whonix](https://www.whonix.org) is a desktop operating system designed for advanced security and privacy. It works by compartmentalizing two different operating systems running in two separate virtual machines for greater security. The first operating system is "The Workstation" and is the OS you perform your normal tasks inside like you would using a normal virtual machine. The second is "The Gateway" that forces all traffic from the Workstation through tor such that your ip address is always protected, even in the case of the Gateway being compromised, while your other activities are compartmentalized from the internet.

The main Whonix team provides both the Gateway and Workstation running on top of Debian but Arch users may enjoy using Arch as their main Workstation OS. This page describes how that is to be done. This is done in three steps:

1\. **Download and install the Whonix Gateway:** You will not use the Gateway for everyday tasks. It only serves to compartmentalize your Workstation activity from the internet and route all traffic through Tor.

2\. **Install Arch as a Whonix Workstation:** It may be helpful to see the official Whonix documentation for using Ubuntu as a Workstation to get a feel for what needs to happen[[1]](https://www.whonix.org/wiki/Ubuntu). For Arch we do these similar steps as follows. Edit these files. First /etc/netctl/whonix:

`Description='Whonix static ethernet connection' Interface=enp0s3 Connection=ethernet IP=static Address=('10.152.152.50/18') Gateway='10.152.152.10'`

Then /etc/resolv.conf:

`nameserver 10.152.152.10`

Then: netctl enable whonix

Then edit /etc/environment:

1.  Deactivate tor-launcher,
2.  a Vidalia replacement as browser extension,
3.  to prevent running Tor over Tor.
4.  [https://trac.torproject.org/projects/tor/ticket/6009](https://trac.torproject.org/projects/tor/ticket/6009)
5.  [https://gitweb.torproject.org/tor-launcher.git](https://gitweb.torproject.org/tor-launcher.git)

TOR_SKIP_LAUNCH=1

1.  Environment variable to disable the "TorButton" ->
2.  "Open Network Settings..." menu item. It is not useful and confusing to have
3.  on a workstation, because this is forbidden for security reasons. Tor must be
4.  configured on the gateway.

TOR_NO_DISPLAY_NETWORK_SETTINGS=1

1.  environment variable to skip TorButton control port verification
2.  [https://trac.torproject.org/projects/tor/ticket/13079](https://trac.torproject.org/projects/tor/ticket/13079)

TOR_SKIP_CONTROLPORTTEST=1

3\. **(Optional) Configure Arch to use the official Tor browser:** First download TOR Browser then follow the "Whonix-Custom-Linux-Workstation" instructions here[[2]](https://www.whonix.org/wiki/Tor_Browser/Advanced_Users):

edit: ~/.tb/tor-browser/Browser/TorBrowser/Data/Browser/profile.default/user.js

user_pref("extensions.torbutton.use_privoxy", false); user_pref("extensions.torbutton.settings_method", "custom"); user_pref("extensions.torbutton.socks_host", "10.152.152.10"); user_pref("extensions.torbutton.socks_port", 9100); user_pref("network.proxy.socks", "10.152.152.10"); user_pref("network.proxy.socks_port", 9100); user_pref("extensions.torbutton.custom.socks_host", "10.152.152.10"); user_pref("extensions.torbutton.custom.socks_port", 9100); user_pref("extensions.torlauncher.control_host", "10.152.152.10"); user_pref("extensions.torlauncher.control_port", 9052);