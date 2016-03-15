[Telnet](https://en.wikipedia.org/wiki/Telnet "wikipedia:Telnet") is the traditional protocol for making remote console connections over TCP. Telnet is **not secure** and is mainly used to connect to legacy equipment nowadays. For a secure alternative see [SSH](/index.php/SSH "SSH").

Follow these instructions to configure an Arch Linux machine as a telnet server.

## Instalación

Para usar telnet solo para conectar con otras maquinas, instale el paquete inetutils (si no esta instalado):

```
# pacman -S inetutils

```

To configure a telnet server, install xinetd as well:

```
# pacman -S xinetd

```

## Configuración

1\. To allow telnet connections in xinetd, edit `/etc/xinetd.d/telnet` and change '<tt>disable = yes</tt>' to '<tt>disable = no</tt>'

2\. Add <tt>xinetd</tt> to the <tt>DAEMONS</tt> array of your [rc.conf](/index.php/Rc.conf "Rc.conf"):

```
DAEMONS=(... **xinetd**)

```

3\. Reboot or restart xinetd:

```
# /etc/rc.d/xinetd restart

```

### Testing the setup

Try opening a telnet connection to your server:

```
$ telnet localhost

```

Note that you can not login as root.