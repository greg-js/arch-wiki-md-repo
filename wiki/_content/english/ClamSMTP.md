[ClamSMTP](http://thewalter.net/stef/software/clamsmtp/) is a very simple virus filtering tool for any SMTP server. It is very usable with the Postfix MTA, so the following article applies to this and gives you an example of a simple configuration.

The basic requirements are a working [Postfix](/index.php/Postfix "Postfix") installation with users set up and a working [ClamAV](/index.php/ClamAV "ClamAV") daemon, so be sure you have installed and configured them properly.

## Contents

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
    *   [2.1 CLAMSMTP](#CLAMSMTP)
    *   [2.2 CLAMAV](#CLAMAV)
    *   [2.3 POSTFIX](#POSTFIX)
*   [3 Testing](#Testing)
*   [4 See also](#See_also)

## Installation

Before you install Clamsmtp, install and configure Postfix, create users for your SMTP server, and test if it is working. Install Clamav, and test it too.

If both of your tools work well, [install](/index.php/Install "Install") the [clamsmtp](https://aur.archlinux.org/packages/clamsmtp/).

## Configuration

### CLAMSMTP

Let's see `/etc/conf.d/clamsmtp` first

change the line:

```
START_CLAMSMTP="no" 

```

to

```
START_CLAMSMTP="yes"

```

Now, we will configure the daemon, by editing `/etc/clamav/clamsmtpd.conf`. You can erase the original file or simply make a backup of it. Create a new file with this contents:

```
# Simple clamsmtpd config file

OutAddress: 10025 
Listen: 127.0.0.1:10026 
TempDirectory: /var/spool/clamsmtp
User: clamav

```

Clamsmtp works as a daemon. The workflow is simple, it listens on a port specified in its configuration file, catches the mails, scans them via Clamav, and then it pushes them back to Postfix via another port. Here, the daemon will listen on port 10026, then scan the mails as user clamav, and will send them back to Postfix on port 10025.

Next we create the cache for clamsmtp by:

```
mkdir /var/spool/clamsmtp
chown clamav:clamav /var/spool/clamsmtp

```

(for whatever reason, the default TempDirectory: `/tmp` returns permission errors )

### CLAMAV

check your `/etc/clamav/clamd.conf`, and uncomment the line ( normally, it is already done ):

```
#ScanMail yes

```

to

```
ScanMail yes

```

### POSTFIX

Now, we have to configure Postfix to work together with Clamsmtp. Edit `/etc/postfix/main.cf`, and add this two lines to the end of the file:

```
content_filter = scan:127.0.0.1:10026 
receive_override_options = no_address_mappings 

```

Postfix will send mails to localhost on port 10026.

Edit `/etc/postfix/master.cf`:

```
scan      unix  -       -       n       -       16      smtp 
        -o smtp_send_xforward_command=yes 
# For injecting mail back into postfix from the filter 
127.0.0.1:10025 inet  n -       n       -       16      smtpd 
       -o content_filter= 
       -o receive_override_options=no_unknown_recipient_checks,no_header_body_checks
       -o smtpd_helo_restrictions= 
       -o smtpd_client_restrictions= 
       -o smtpd_sender_restrictions= 
       -o smtpd_recipient_restrictions=permit_mynetworks,reject 
       -o mynetworks_style=host 
       -o smtpd_authorized_xforward_hosts=127.0.0.0/8 

```

The first two lines create the service „scan”, the others take charge of accepting the already scanned mail from Clamsmtp from port 10025 and delivering them to the recipients.

## Testing

Now, test your server:

```
/etc/rc.d/clamav restart
/etc/rc.d/postfix restart
/etc/rc.d/clamsmtp restart

```

Send yourself a mail, without any viruses

If you do not have any arriving mails, check `/var/log/mail.log` for errors

Then, download a test-virus

```
wget [http://eicar.org/download/eicar_com.zip](http://eicar.org/download/eicar_com.zip)

```

and send it as an attachment.

Check your server's logfile again, you should get something similar to this:

```
May 23 00:04:08 servername postfix/smtp[2415]: A9B941F911: to=<user@your.postfix.server>, relay=127.0.0.1[127.0.0.1]:10026, delay=0.13, delays=0.08/0/0.04/0, dsn=2.0.0, status=sent (250 Virus Detected; Discarded Email)

```

## See also

*   [http://memberwebs.com/stef/software/clamsmtp/](http://memberwebs.com/stef/software/clamsmtp/)
*   [http://www.postfix.org/](http://www.postfix.org/)