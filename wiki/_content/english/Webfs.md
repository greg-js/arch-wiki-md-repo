[Webfs](http://linux.bytesex.org/misc/webfs.html) is a simple http server for mostly static content.

## Installation

It is available as [webfs](https://www.archlinux.org/packages/?name=webfs).

## Configuration

The configuration file is `/etc/conf.d/webfsd`. You need to create an `index.html` file if you want to make it web browser readable, and point to `index.html` in the configuration file.

It is set up for systemd. Use systemctl to start, stop, enable, disable webfsd.service.

The examples below are a local network server, used for downloading programs in an embedded Linux install.

An example `/etc/conf.d/webfsd`.

```
 #
 # Parameters passed to webfsd(1)
 #

 WEBFSD_ARGS="-p 80 -u nobody -R /home/jeff/www -f index.html"

```

An `index.html` example.

```
 <!DOCTYPE HTML>
  <html>
  <head>
  <title>Downloads</title>
  </head>
  <body>
  <h>Local network File Server</h>
  <table><tr><th></th>
<th><a href="./">Program</a></th>
<th><a href="?C=M;O=A"></a></th>
<th><a href="?C=S;O=A"></a></th>
<th><a href="?C=D;O=A"></a></th></tr>
<tr><th colspan="5"><hr></th></tr>

  <tr><td valign="top"></td><td><a href="flash_erase">flash_erase</a>

  <tr><td valign="top"></td><td><a href="fw_printenv">fw_printenv</a>

  <tr><td valign="top"></td><td><a href="fw_setenv">fw_setenv</a>

  <tr><td valign="top"></td><td><a href="nanddump">nanddump</a>

  <tr><td valign="top"></td><td><a href="nandwrite">nandwrite</a>

  <tr><th colspan="5"><hr></th></tr>
  </table>

  <address>webfs 1.21-12 (Arch) Server 192.168.2.2 Port 80</address>
  </body></html>

```

## See also

*   `man webfsd`