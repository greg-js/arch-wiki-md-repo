[Telnet](https://en.wikipedia.org/wiki/Telnet "wikipedia:Telnet") is the traditional protocol for making remote console connections over TCP. Telnet is **not secure** and is mainly used to connect to legacy equipment nowadays. Telnet traffic is easily sniffed for passwords and connections should never be made over any untrusted network including the Internet unless encrypted with [SSH](/index.php/SSH "SSH") or tunneled though a VPN. For a secure alternative see [SSH](/index.php/SSH "SSH").

## Installation

The [inetutils](https://www.archlinux.org/packages/?name=inetutils) package, part of the [base group](/index.php/Base_group "Base group"), includes a telnet client.

A telnet server can be configured with [systemd](/index.php/Systemd "Systemd") sockets or xinetd. telnetd via systemd requires only the inetutils package. To configure a telnet server with xinetd, install [xinetd](https://www.archlinux.org/packages/?name=xinetd) as well.

## Configuration

To enable telnet server connections in systemd, [enable](/index.php/Enable "Enable") `telnet.socket` (if the telnet server should be started on every boot), and [start](/index.php/Start "Start") `telnet.socket` to test connectivity.

To enable telnet server connections in xinetd, edit `/etc/xinetd.d/telnet`, change `disable = yes` to `disable = no` and restart the xinetd service.

[Enable](/index.php/Enable "Enable") systemd xinetd service if you wish to start it at boot time.

### Testing the setup

Try opening a telnet connection to your server:

```
$ telnet localhost

```

Try a root login to see if your configuration permits it and the security implications that implies.

If the session disconnects before you receive a login prompt, try installing [inetutils-git](https://aur.archlinux.org/packages/inetutils-git/) in place of the current inetutils and restarting telnet.socket.

**Tip:** If you receive junk codes from a remote telnet server sending non-ascii chars with a non-unicode encoding, you might want to try [xorg-luit](https://www.archlinux.org/packages/?name=xorg-luit) to solve this problem.