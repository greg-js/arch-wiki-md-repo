SSMTP is a program which delivers email from a local computer to a configured mailhost (mailhub). It is not a mail server (like feature-rich mail server [sendmail](/index.php/Sendmail "Sendmail")) and does not receive mail, expand aliases or manage a queue. One of its primary uses is for forwarding automated email (like system alerts) off your machine and to an external email address.

ssmtp is unmaintained. Consider using something like [msmtp](/index.php/Msmtp "Msmtp") instead.

## Contents

*   [1 Installation](#Installation)
*   [2 Forward to a Gmail mail server](#Forward_to_a_Gmail_mail_server)
*   [3 Security](#Security)
*   [4 Sending email](#Sending_email)
    *   [4.1 Attachments](#Attachments)
*   [5 References](#References)

## Installation

[Install](/index.php/Install "Install") the package [ssmtp](https://www.archlinux.org/packages/?name=ssmtp).

## Forward to a Gmail mail server

To configure SSMTP, you will have to edit its configuration file (`/etc/ssmtp/ssmtp.conf`) and enter your account settings.

If your Gmail account is secured with two-factor authentication, you need to generate a unique [App Password](https://support.google.com/mail/answer/185833) to use in `ssmtp.conf`. You can do so on your [App Passwords](https://security.google.com/settings/security/apppasswords) page. Use the generated 16-character password in the `AuthPass` line. Spaces in the password can be omitted.

 `/etc/ssmtp/ssmtp.conf` 
```

# The user that gets all the mails (UID < 1000, usually the admin)
root=username@gmail.com

# The mail server (where the mail is sent to), both port 465 or 587 should be acceptable
# See also https://support.google.com/mail/answer/78799
mailhub=smtp.gmail.com:587

# The address where the mail appears to come from for user authentication.
rewriteDomain=gmail.com

# The full hostname.  Must be correctly formed, fully qualified domain name or GMail will reject connection.
hostname=yourlocalhost.yourlocaldomain.tld

# Use SSL/TLS before starting negotiation
UseTLS=Yes
UseSTARTTLS=Yes

# Username/Password
AuthUser=username
AuthPass=password
AuthMethod=LOGIN

# Email 'From header's can override the default domain?
FromLineOverride=yes

```

**Note:** Take note, that the shown configuration is an example for Gmail, You may have to use other settings. If it is not working as expected read the man page [ssmtp(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/ssmtp.8), please.

Create aliases for local usernames (optional)

 `/etc/ssmtp/revaliases` 
```
root:username@gmail.com:smtp.gmail.com:587
mainuser:username@gmail.com:smtp.gmail.com:587
```

To test whether the Gmail server will properly forward your email:

 `$ echo test | mail -v -s "testing ssmtp setup" tousername@somedomain.com` 
**Note:**Gmail has recently started blocking emails from senders that do not authenticate using OAuth. To allow SSMTP to use gmail's SMTP server, you need to [allow access to unsecure apps](https://support.google.com/accounts/answer/6010255).

Change the 'From' text by editing `/etc/passwd` to receive mail from 'root at myhost' instead of just 'root'.

```
# chfn -f 'root at myhost' root
# chfn -f 'mainuser at myhost' mainuser
```

Which changes `/etc/passwd` to:

 `$ grep myhostname /etc/passwd` 
```
root:x:0:0:root@myhostname,,,:/root:/bin/bash
mainuser:x:1000:1000:mainuser@myhostname,,,:/home/mainuser:/bin/bash
```

## Security

Because your email password is stored as cleartext in `/etc/ssmtp/ssmtp.conf`, it is important to secure the file. Securing ssmtp.conf will ensure that:

*   if any users have unprivileged access to your system, they cannot read the file and see your email password, while still letting them send out email
*   if your user account is ever compromised, the hacker cannot read the `ssmtp.conf` file, and therefore your email password, unless he gains access to the root account as well

To secure `ssmtp.conf`, do this:

Create an `ssmtp` group:

```
# groupadd ssmtp

```

Set ssmtp.conf group owner to the new `ssmtp` group:

```
# chown :ssmtp /etc/ssmtp/ssmtp.conf

```

Set the group owner of the *ssmtp* binary to the new `ssmtp` group:

```
# chown :ssmtp /usr/bin/ssmtp

```

Make sure only root, and the `ssmtp` group can access `ssmtp.conf`:

```
# chmod 640 /etc/ssmtp/ssmtp.conf

```

Set the SGID bit on the *ssmtp* binary.

```
# chmod g+s /usr/bin/ssmtp

```

Finally add a pacman hook to always set the file permissions on `/usr/bin/ssmtp` after the package has been upgraded:

 `/root/bin/ssmtp-set-permissions` 
```
#!/bin/bash

chown :ssmtp /usr/bin/ssmtp
chmod g+s /usr/bin/ssmtp

```

Make the file executable:

```
# chmod u+x /root/bin/ssmtp-set-permissions

```

Now add the pacman hook:

 `/usr/share/libalpm/hooks/ssmtp-set-permissions.hook` 
```
[Trigger]
Operation = Install
Operation = Upgrade
Type = Package
Target = ssmtp

[Action]
Description = Set ssmtp permissions for security
When = PostTransaction
Exec = /root/bin/set-ssmtp-permissions
```

Now, all the regular users can still send email using the terminal, but none can read the `ssmtp.conf` file.

## Sending email

To send email from the terminal, do:

```
$ echo "this is the body" | mail -s "Subject" username@somedomain.com

```

or interactively as:

```
$ mail username@somedomain.com

```

**Note:** When using mail interactively, after typing the Subject and hitting enter, you type the body. Hit `Ctrl`+`d` on a blank line to end your message and automatically send it out.

An alternate method for sending emails is to create a text file and send it with *ssmtp* or *mail*

 `test-mail.txt` 
```
To:username@somedomain.com
From:youraccount@gmail.com
Subject: Test

This is a test mail.
```

Send the `test-mail.txt` file

```
$ mail username@somedomain.com < test-mail.txt

```

### Attachments

If you need to be able to add attachments, install and configure [Mutt](/index.php/Mutt "Mutt") and [Msmtp](/index.php/Msmtp "Msmtp") and then go see the tip at [nixcraft](http://www.cyberciti.biz/tips/sending-mail-with-attachment.html).

Alternatively, you can attach using *uuencode*:

```
$ uuencode file.txt file.txt | mail user@domain.com

```

## References

*   [SSMTP and Gmail on the Arch forums](https://bbs.archlinux.org/viewtopic.php?pid=446831)
*   [Sending Email From Your System with sSMTP](http://tombuntu.com/index.php/2008/10/21/sending-email-from-your-system-with-ssmtp/)
*   [The Qnd Guide to ssmtp](http://www.scottro.net/qnd/qnd-ssmtp.html)
*   [GMail Support - Configuring other mail clients](https://support.google.com/mail/answer/78799)