From [Wikipedia](https://en.wikipedia.org/wiki/UW_IMAP "wikipedia:UW IMAP"):

	**UW IMAP** is the reference server implementation of the IMAP protocol, developed at the University of Washington.

Although it has not been actively developed in many years, it still works well as a basic IMAPS server. (For other IMAP servers, see [Mail server#POP3/IMAP servers](/index.php/Mail_server#POP3/IMAP_servers "Mail server").)

## Installation

In arch, UW IMAP is simply called imap.

[Install](/index.php/Install "Install") [imap](https://www.archlinux.org/packages/?name=imap). It does not use a configuration file.

## Setup

Although it was originally designed to be used with [inetd](https://en.wikipedia.org/wiki/inetd "wikipedia:inetd"), on modern Arch systems a better solution is to use a systemd socket file:

 `/etc/systemd/system/imaps.socket` 
```
[Unit]
Description=IMAP Server Activation Socket
Documentation=https://www.washington.edu/imap/

[Socket]
ListenStream=0.0.0.0:993
Accept=true

[Install]
WantedBy=sockets.target

```

Also, a corresponding .service file needs to be created:

 `/etc/systemd/system/imaps@.service` 
```
[Unit]
Description=IMAP Server

[Service]
ExecStart=-/usr/bin/imapd
StandardInput=socket

```

UW-IMAPD uses [PAM](/index.php/PAM "PAM"), so a PAM authorization file will also need to be created. This example will provide authentication using standard system passwords:

 `/etc/pam.d/imap` 
```
auth		required	pam_unix.so
account		required	pam_unix.so
session		required	pam_unix.so

```

[Enable](/index.php/Enable "Enable") and [start](/index.php/Start "Start") `imaps.socket` and test.

## SSL

A generic SSL certificate and key will be created at `/etc/ssl/certs/imapd.pem` if it doesn't yet exist. This can (and should) be [replaced](/index.php/Transport_Layer_Security#Obtaining_a_certificate "Transport Layer Security") with a signed certificate for the specific server.