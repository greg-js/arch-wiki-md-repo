# FTP over SSH

[FTP over SSH](https://en.wikipedia.org/wiki/File_Transfer_Protocol#FTP_over_SSH "wikipedia:File Transfer Protocol") encrypts passwords unlike plain FTP. FTP over SSH is not really a true protocol, it is just SSH + FTP.

This setup in particular (using [pure-ftpd](https://aur.archlinux.org/packages/pure-ftpd/)<sup><small>AUR</small></sup> + TLS) encrypts usernames, passwords, commands and server replies, but does NOT encrypt the data channel. This also means that there is reduced performance cost on data transfer.

## Setting up FTP with pure-ftpd

Install [pure-ftpd](https://aur.archlinux.org/packages/pure-ftpd/)<sup><small>AUR</small></sup> from [AUR](/index.php/AUR "AUR").

The configuration file is `/etc/pure-ftpd.conf`.

[Start/Enable](/index.php/Systemd#Using_units "Systemd") the `pure-ftpd.service` daemon.

## Set up Certificates

Refer to [the documentation](http://download.pureftpd.org/pub/pure-ftpd/doc/README.TLS) for more information. The short version is this:

Create a Self-Signed Certificate:

```
# mkdir -p /etc/ssl/private
# openssl req -x509 -nodes -days 7300 -newkey rsa:1024 -keyout /etc/ssl/private/pure-ftpd.pem -out /etc/ssl/private/pure-ftpd.pem

```

Make it private:

```
# chmod 600 /etc/ssl/private/*.pem

```

**Warning:** Be aware that using 1024 bits in some countries is against the law. Choose 512 or less if unsure.

## Enable TLS

Towards the bottom of `/etc/pure-ftpd.conf` you should find a section for TLS. Uncomment and change the TLS setting to `1` to enable both FTP and SFTP:

```
TLS             1

```

Now restart the `pure-ftpd.service` daemon and you should be able to log in with SFTP-enabled clients, e.g. [filezilla](https://www.archlinux.org/packages/?name=filezilla) or [SmartFTP](https://www.smartftp.com/).

Retrieved from "[https://wiki.archlinux.org/index.php?title=FTP_over_SSH&oldid=362439](https://wiki.archlinux.org/index.php?title=FTP_over_SSH&oldid=362439)"