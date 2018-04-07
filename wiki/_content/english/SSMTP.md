Related articles

*   [msmtp](/index.php/Msmtp "Msmtp")
*   [S-nail](/index.php/S-nail "S-nail")

SSMTP is a program which delivers email from a local computer to a configured mailhost (mailhub). It is not a mail server (like feature-rich mail server [sendmail](/index.php/Sendmail "Sendmail")) and does not receive mail, expand aliases or manage a queue. One of its primary uses is for forwarding automated email (like system alerts) off your machine and to an external email address.

ssmtp is unmaintained. Consider using something like [msmtp](/index.php/Msmtp "Msmtp") instead.

## Contents

*   [1 Installation](#Installation)
*   [2 Forward to a Gmail mail server](#Forward_to_a_Gmail_mail_server)
*   [3 Security](#Security)
*   [4 Sending email](#Sending_email)
    *   [4.1 Attachments](#Attachments)
    *   [4.2 Mail to Local Users](#Mail_to_Local_Users)
*   [5 References](#References)

## Installation

[Install](/index.php/Install "Install") the package [ssmtp](https://www.archlinux.org/packages/?name=ssmtp).

## Forward to a Gmail mail server

To configure SSMTP, you will have to edit its configuration file (`/etc/ssmtp/ssmtp.conf`) and enter your account settings.

*   If your Gmail account is secured with two-factor authentication, you need to generate a unique [App Password](https://support.google.com/mail/answer/185833) to use in `ssmtp.conf`. You can do so on your [App Passwords](https://myaccount.google.com/apppasswords) page. Use the generated 16-character password in the `AuthPass` line. Spaces in the password can be omitted.
*   If you do *not* use two-factor authentication, you need to [allow access to unsecure apps](https://support.google.com/accounts/answer/6010255). You can do so on your [Less Secure Apps](https://myaccount.google.com/lesssecureapps) page.

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

 `$ echo -n 'Subject: test

Testing ssmtp' | sendmail -v tousername@example.com` 

Change the 'From' text by editing `/etc/passwd` to receive mail from 'root at myhost' instead of just 'root'.

```
# chfn -f 'root at myhost' root
# chfn -f 'mainuser at myhost' mainuser
```

Which changes `/etc/passwd` to:

 `$ grep myhost /etc/passwd` 
```
root:x:0:0:root at myhost,,,:/root:/bin/bash
mainuser:x:1000:1000:mainuser at myhost,,,:/home/mainuser:/bin/bash
```

## Security

Because your email password is stored as cleartext in `/etc/ssmtp/ssmtp.conf`, it is important that this file is secure. By default, the entire `/etc/ssmtp` directory is accessible only by root and the mail group. The `/usr/bin/ssmtp` binary runs as the mail group and can read this file. There is no reason to add yourself or other users to the mail group.

## Sending email

To send email from the terminal, do:

```
$ echo -e "Subject: this is the subject

this is the body" | mail user@example.com

```

or interactively as:

```
$ sendmail username@example.com
Subject: this is my subject
CC: optional@example.com

Now I can type the body here

```

**Note:** When using mail interactively, after typing the *Subject: subject* and other headers, hit enter twice, and then type the body. Hit `Ctrl`+`d` on a blank line to end your message and automatically send it out.

An alternate method for sending emails is to create a text file and send it with *ssmtp* or *mail*

 `test-mail.txt` 
```
To:username@example.com
From:youraccount@gmail.com
Subject: Test

This is a test mail.
```

Send the `test-mail.txt` file

```
$ sendmail -t < test-mail.txt

```

Some users might prefer the syntax of *mail* from [s-nail](https://www.archlinux.org/packages/?name=s-nail), [mailutils](https://www.archlinux.org/packages/?name=mailutils), or other *mailx* providers instead. For example, *mail* has options to provide the subject as an argument. *mail* requires *sendmail* and can use [ssmtp](https://www.archlinux.org/packages/?name=ssmtp) as *sendmail*.

### Attachments

If you need to be able to add attachments, install and configure [Mutt](/index.php/Mutt "Mutt") and [Msmtp](/index.php/Msmtp "Msmtp") and then go see the tip at [nixcraft](http://www.cyberciti.biz/tips/sending-mail-with-attachment.html).

Alternatively, you can attach using *uuencode* from [sharutils](https://www.archlinux.org/packages/?name=sharutils). To attach 'file.txt' as 'myfile.txt':

```
$ uuencode file.txt myfile.txt | sendmail user@example.com

```

### Mail to Local Users

Messages sent to local users (or any other address not ending in *@fqdn* are treated in one of two ways

*   destination user has UID < 1000 - The address is replaced by the address defined by `root=user@fqdn` in `/etc/ssmtp/ssmtp.conf`
*   destination user has UID ≥ 1000 or the user is unknown - The the value from `rewriteDomain=` in `/etc/ssmtp/ssmtp.conf` is appended to the end of the user id.

This can lead to problems if local users on your system aren't also valid users at your `rewriteDomain`, but are receiving mail from system services, esp if your rewrite domain is a public service like `gmail.com`.

To work around this, you can use *mail* from [s-nail](https://www.archlinux.org/packages/?name=s-nail). The *mail* command can read aliases defined in `/etc/mail.rc`. Example:

 `$ grep alias /etc/mail.rc` 
```
alias git git<username@example.com>
alias archuser 'My Name'<someone@example.com>
```

You can then pipe messages into *mail* instead of into *sendmail*.

```
$ echo -e "Hey archuser." | mail archuser

```

**Note:** You might be tempted to symlink *sendmail* to `/bin/mail`. Don't do this. *sendmail* and *mail* have different syntax for both arguments and standard input. It is better to find the processes that are using sendmail directly and configure them to use mail instead.

## References

*   [SSMTP and Gmail on the Arch forums](https://bbs.archlinux.org/viewtopic.php?pid=446831)
*   [Sending Email From Your System with sSMTP](http://tombuntu.com/index.php/2008/10/21/sending-email-from-your-system-with-ssmtp/)
*   [The Qnd Guide to ssmtp](http://www.scottro.net/qnd/qnd-ssmtp.html)
*   [GMail Support - Configuring other mail clients](https://support.google.com/mail/answer/78799)