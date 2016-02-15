[Telnet](https://en.wikipedia.org/wiki/Telnet "wikipedia:Telnet") is the traditional protocol for making remote console connections over TCP. Telnet is **not secure** and is mainly used to connect to legacy equipment nowadays. Telnet traffic is easily sniffed for passwords and connections should never be made over any untrusted network including the Internet unless encrypted with [SSH](/index.php/SSH "SSH") or tunneled though a VPN. For a secure alternative see [SSH](/index.php/SSH "SSH").

Follow these instructions to configure an Arch Linux machine for telnet.

## Installation

To use the telnet client to connect to other machines, [install](/index.php/Install "Install") [inetutils](https://www.archlinux.org/packages/?name=inetutils).

A telnet server can be configured with [systemd](/index.php/Systemd "Systemd") sockets or xinetd. telnetd via systemd requires only the inetutils package. To configure a telnet server with xinetd, install [xinetd](https://www.archlinux.org/packages/?name=xinetd) as well.

## Configuration

To enable telnet server connections in systemd, [enable](/index.php/Enable "Enable") `telnet.socket` if the telnet server should be started on every boot, and [start](/index.php/Start "Start") `telnet.socket` to test connectivity.

To enable telnet server connections in xinetd, edit `/etc/xinetd.d/telnet`, change `disable = yes` to `disable = no` and restart the xinetd service.

[Enable](/index.php/Enable "Enable") systemd xinetd service if you wish to start it at boot time.

### Testing the setup

Try opening a telnet connection to your server:

```
$ telnet localhost

```

Try a root login to see if your configuration permits it and the security implications that implies.