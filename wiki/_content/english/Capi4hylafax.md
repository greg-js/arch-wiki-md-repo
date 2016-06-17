### Installation

[Install](/index.php/Install "Install") the [capi4hylafax](https://www.archlinux.org/packages/?name=capi4hylafax) package.

### Setup

Run *faxsetup* as root user to adjust hylafax to your needs. Further adjust `/var/spool/hylafax/etc/config/config.faxCAPI` to your needs.

**Warning:** Do not even try to run faxaddmodem for capi20 devices!

*c2faxaddmodem* is a nice tool for configuring your ISDN card.

[Start](/index.php/Start "Start") `hylafax.service` and `c2faxrecv.service`.

Be sure that your device has the right permissions 'uucp'.

Add the following line to `/var/spool/hylafax/etc/config`:

```
SendFaxCmd: /usr/bin/c2faxsend

```

**Note:** If you need more than one isdn controller please read the manual of capi4hylafax.

For hints and tips see [Hylafax](/index.php/Hylafax "Hylafax").