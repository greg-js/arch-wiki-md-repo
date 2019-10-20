[dma](https://github.com/corecode/dma) (*Dragonfly Mail Agent*) is a tiny Mail Transport Agent (MTA). It is able to accept mails and deliver it to local or remote destinations; however, if you want to send and receive mails with your domain name then you'll need full-featured [mail server](/index.php/Mail_server "Mail server").

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
    *   [2.1 SMTP transport](#SMTP_transport)
    *   [2.2 Encryption](#Encryption)
    *   [2.3 Masquerading](#Masquerading)
    *   [2.4 Testing](#Testing)
*   [3 Examples](#Examples)
    *   [3.1 Send mails through Google's SMTP servers](#Send_mails_through_Google's_SMTP_servers)
        *   [3.1.1 Prerequisites](#Prerequisites)
        *   [3.1.2 Configuration](#Configuration_2)

## Installation

Package [dma](https://aur.archlinux.org/packages/dma/) is available in the AUR.

## Configuration

dma have two main configuration files: `/etc/dma/dma.conf` contains main setup directives and `/etc/dma/auth.conf` is necessary for authentication on SMTP server. dma provides sane defaults so you may be able to use it without special configuration.

### SMTP transport

If you want to route mail through external SMTP server you must set `SMARTHOST` address (also known as relay host) in `/etc/dma/dma.conf`:

```
SMARTHOST smtp-host

```

Also don't forget to set authentication credentials in `/etc/dma/auth.conf` (or in whatever file `AUTHPATH` points to) in the following format:

```
user|smarthost.example.com:password

```

To change default port set `PORT` directive (25 is default):

```
# accept mail from external MTAs (STARTTLS is also an option)
PORT 25

# accept mail from MUAs with TLS
PORT 465

# accept mail from MUAs (STARTTLS is also an option)
PORT 587

```

### Encryption

`SECURETRANSFER` directive enables encryption during mail transfers. Depending on your needs uncomment `STARTTLS` to enable [STARTTLS](https://en.wikipedia.org/wiki/Opportunistic_TLS "wikipedia:Opportunistic TLS") support and activate `OPPORTUNISTIC_TLS` to permit unencrypted fallback in case of error.

For whatever reason you may want to perform plain text SMTP authentication. In such case uncomment `SECURE` directive and change it to `INSECURE` explicitly.

### Masquerading

If you want to substitute original *From:* field in envelope you can use `MASQUERADE` feature:

```
# send mails as user foo (hostname will be derived with gethostbyname() or set to MAILNAME directive)
MASQUERADE foo@

# send mails from host bar (username will be substitued)
MASQUERADE bar

# send mail as user foo from host bar
MASQUERADE foo@bar

```

### Testing

To send test mail execute the following from command line:

```
$ mail -s "Just a dma test" foo@bar.example.com
This is just a small test message
<Ctrl+D>

```

Use `journalctl -r` to see if all went good. Also you can check dma queue with:

```
$ dma -bp

```

`/var/spool/dma` directory also holds undelivered/unprocessed mails.

## Examples

### Send mails through Google's SMTP servers

#### Prerequisites

If you use [2-Step Verification](https://www.google.com/landing/2step/) (also known as [two-factor authentication](https://en.wikipedia.org/wiki/Multi-factor_authentication "wikipedia:Multi-factor authentication")) procedure then you should create so-called [App Password](https://myaccount.google.com/apppasswords).

To do that login into your [Google Account](https://myaccount.google.com/), choose *Security* entry on the left panel and click on *App Passwords* in *Signing in to Google* panel. If you don't see this item please consult [corresponding thread](https://support.google.com/mail/answer/185833) on Google.

Click on *Select app* and choose desired application (usual called as **Mail**). Then click on *Select device* and choose the device, but it's better to add custom device and call it appropriately for easy future management. Then click on *Generate* and write down your **App Password** (16-character code in the yellow bar).

**Warning:** It isn't possible to review or change app password later so use it immediately.

#### Configuration

 `/etc/dma/dma.conf` 
```
 SMARTHOST smtp.gmail.com
 PORT 587
 AUTHPATH /etc/dma/auth.conf
 SECURETRANSFER
 STARTTLS
 MASQUERADE alias-user@gmail.com

```
 `/etc/dma/auth.conf` 
```
 user|smtp.gmail.com:password

```

**Note:** Don't forget to specify your Google account login and password (or App Password instead, see previous section)