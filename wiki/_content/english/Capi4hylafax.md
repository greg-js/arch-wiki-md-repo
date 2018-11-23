**Capi4hylafax** is a CAPI plugin for [Hylafax](/index.php/Hylafax "Hylafax") to enable ISDN faxing over CAPI 2.0 devices.

## Installation

[Install](/index.php/Install "Install") the [capi4hylafax](https://www.archlinux.org/packages/?name=capi4hylafax) package.

## Configuration

Run *faxsetup* as root user to adjust hylafax to your needs. Further adjust `/var/spool/hylafax/etc/config/config.faxCAPI` to your needs.

**Warning:** Do not even try to run *faxaddmodem* for CAPI 2.0 devices!

*c2faxaddmodem* is a nice tool for configuring your ISDN card.

[Start](/index.php/Start "Start") `hylafax.service` and `c2faxrecv.service`.

Be sure that your device has the right permissions for the `uucp` [user group](/index.php/User_group "User group").

Add the following line to `/var/spool/hylafax/etc/config`:

```
SendFaxCmd: /usr/bin/c2faxsend

```

**Note:** If you need more than one ISDN controller, please read the capi4hylafax manual.

For hints and tips, see [Hylafax](/index.php/Hylafax "Hylafax").