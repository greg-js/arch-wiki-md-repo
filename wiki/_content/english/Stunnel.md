[stunnel](https://www.stunnel.org) (“Secure Tunnel”) is a

	multi-platform application used to provide a universal TLS/SSL tunneling service. It is sort of proxy designed to add TLS encryption functionality to existing clients and servers without any changes in the programs' code. It is designed for security, portability, and scalability (including load-balancing), making it suitable for large deployments. It uses [OpenSSL](/index.php/OpenSSL "OpenSSL"), and distributed under GNU GPL version 2 or later with OpenSSL exception.

Can tunnel only TCP packets. Its [FAQ](https://www.stunnel.org/faq.html) has some work around for UDP. [WireGuard](/index.php/WireGuard "WireGuard") also has UDP capabilities.

Authentication can also be used by the server to allow access only to approved clients.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Installation](#Installation)
*   [2 Setup](#Setup)
    *   [2.1 Byte order mark (BOM)](#Byte_order_mark_(BOM))
    *   [2.2 Authentication](#Authentication)
*   [3 Tips and Tricks](#Tips_and_Tricks)
    *   [3.1 DNS over TLS](#DNS_over_TLS)
    *   [3.2 Encrypting NFSv4 with Stunnel TLS](#Encrypting_NFSv4_with_Stunnel_TLS)
*   [4 See also](#See_also)

## Installation

[Install](/index.php/Install "Install") [stunnel](https://www.archlinux.org/packages/?name=stunnel) from [official repositories](/index.php/Official_repositories "Official repositories").

Depending on your usage, you might also [Systemd#Editing provided units](/index.php/Systemd#Editing_provided_units "Systemd") to better [Systemd#Handling dependencies](/index.php/Systemd#Handling_dependencies "Systemd"). In order for the stunnel to start up automatically at system boot you must [enable](/index.php/Enable "Enable") it.

## Setup

The main configuration file is read from `/etc/stunnel/stunnel.conf`. It is an ini-style file. It is composed from a global section, followed by one, or more, service sections.

A client is one to accept non TLS encrypted data. Stunnel will TLS encrypts its data and connects to the stunnel server. The stunnel server accepts TLS encrypted data and extracts it. It then connects to where the data should be sent to.

The default `debug` value is 5, which is very verbose. After verifying correct operation, it is worth explicitly setting lower value in the configuration file.

 `/etc/stunnel/stunnel.conf`  `debug = 3` 

For better security, it is advised to explicitly set an appropriate uid and gid, other then root, for the global section and the per service sections. The configuration tokens `setuid` and `setgid` are available for this purpose.

### Byte order mark (BOM)

The configuration file should have a UTF-8 [byte order mark (BOM)](https://en.wikipedia.org/wiki/Byte_order_mark "wikipedia:Byte order mark"), at the beginning of the file. A BOM is the unicode character U+FEFF. Its UTF-8 representation is the (hexadecimal) byte sequence 0xEF, 0xBB, 0xBF. Creating a file with these bytes at its beginning can be done by

```
# echo -e '\x**ef**\x**bb**\x**bf**; BOM composed of non printable characters. It is here, before the semicolon!' > /etc/stunnel/stunnel.conf

```

To test if those bytes appear, one can use

```
% od --address-radix=n --format=x1c --read-bytes=8 /etc/stunnel/stunnel.conf
  **ef  bb  bf**  3b  20  42  4f  4d
 357 273 277   ;       B   O   M
```

Note that when printing the file to the screen, such as with `cat`, or when editing the file with a text editor, the BOM bytes are usually not displayed. They should be there, though. Which is why you might want to verify that they are still there after editing is completed with the above `od`, or similar, command.

### Authentication

At least one of the client and the server, and optionally both, should be authenticated. Either a pre shared secret, or a key and certificate pair, can be used for authentication. A pre shared secret has to be transferred to all involved machines a priory by other means, such as [SCP and SFTP](/index.php/SCP_and_SFTP "SCP and SFTP"). When such transfer is acceptable, pre shared key is the fastest method. Its speed might help mitigating attacks. A simple configuration for a single server with a single client that are using a pre shared secret is:

 `client:/etc/stunnel/stunnel.conf` 
```
; BOM composed of non printable characters. It is here, before the semicolon!
setuid = stunnel
setgid = stunnel

[trivial client]
client     = yes
accept     = 127.0.0.1:<src_port>
connect    = <server_host>:<server_port>
debug      = 3
PSKsecrets = /etc/stunnel/psk.txt
setuid     = stunnel
setgid     = stunnel
```
 `server:/etc/stunnel/stunnel.conf` 
```
; BOM composed of non printable characters. It is here, before the semicolon!
setuid = stunnel
setgid = stunnel

[trivial server]
accept     = <server_port>
connect    = <dst_port>
ciphers    = PSK
debug      = 3
PSKsecrets = /etc/stunnel/psk.txt
setuid     = stunnel
setgid     = stunnel
```

where `/etc/stunnel/psk.txt` could be created on one machine by

```
# openssl rand -base64 -out /etc/stunnel/psk.txt 180
# sed --in-place '1s/^/psk:/' /etc/stunnel/psk.txt

```

and copied to the other machine by secure means before starting stunnel. The [permissions](/index.php/Permissions "Permissions") for each `psk.txt` file should be set appropriately. The psk string from the `sed` command is just a random name for the sake of the example. Do read [stunnel(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/stunnel.8).

## Tips and Tricks

### DNS over TLS

[BIND](/index.php/BIND "BIND") does not offer builtin facilities for encryption of queries and answers. Bind knowledge base suggests using stunnel. See [https://kb.isc.org/docs/aa-01386](https://kb.isc.org/docs/aa-01386). The link mentions [unbound](/index.php/Unbound "Unbound") at the bottom of the page. A user that have only shell accounts on both the client and the server can still tunnel DNS traffic even when both the resolver and the NS do not support DNS over TLS.

### Encrypting NFSv4 with Stunnel TLS

See [Encrypting NFSv4 with Stunnel TLS](https://www.linuxjournal.com/content/encrypting-nfsv4-stunnel-tls)

## See also

*   [Wikipedia:stunnel](https://en.wikipedia.org/wiki/stunnel "wikipedia:stunnel")
*   [SSL encryption for Pan](https://wiki.debian.org/Pan?highlight=%28stunnel%29#SSL_encryption)
*   [Paranoid Penguin - Rehabilitating Clear-Text Network Applications with Stunnel](https://www.linuxjournal.com/article/7628)