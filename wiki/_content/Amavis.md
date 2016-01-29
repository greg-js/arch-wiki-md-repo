# Amavis

Related articles

*   [ClamAV](/index.php/ClamAV "ClamAV")
*   [Postfix](/index.php/Postfix "Postfix")
*   [Dovecot](/index.php/Dovecot "Dovecot")

From [Amavis's site](http://www.ijs.si/software/amavisd/):

NaN

## Contents

*   [1 Installation and Setup](#Installation_and_Setup)
    *   [1.1 Basic Configuration](#Basic_Configuration)
    *   [1.2 Testing](#Testing)
*   [2 Integration with Postfix](#Integration_with_Postfix)
    *   [2.1 Quick start](#Quick_start)
*   [3 SpamAssassin support](#SpamAssassin_support)
*   [4 Final test](#Final_test)
*   [5 See also](#See_also)

## Installation and Setup

In this setup it is assumed that you are using [ClamAV](/index.php/ClamAV "ClamAV") as anti-virus scanner.

*   Install [amavisd-new](https://aur.archlinux.org/packages/amavisd-new/)<sup><small>AUR</small></sup> from the [AUR](/index.php/AUR "AUR"). You would be wise to also install optdepends such as [p7zip](https://www.archlinux.org/packages/?name=p7zip) and [unrar](https://www.archlinux.org/packages/?name=unrar) so your filters can actually see inside compressed files.
*   Install [clamav](https://www.archlinux.org/packages/?name=clamav) from the [official repositories](/index.php/Official_repositories "Official repositories").

### Basic Configuration

If your hostname is not a FQDN, you must set `$myhostname` and `$mydomain` accordingly in `/etc/amavisd/amavisd.conf`.

You can enable [ClamAV](/index.php/ClamAV "ClamAV") support by commenting out the following lines (do not forget to put the same `clamd.sock` as in `/etc/clamav/clamd.sock`):

```
# ### http://www.clamav.net/
['ClamAV-clamd',
   \&ask_daemon, ["CONTSCAN {}\n", "/var/lib/clamav/clamd.sock"],
   qr/\bOK$/m, qr/\bFOUND$/m,
   qr/^.*?: (?!Infected Archive)(.*) FOUND$/m ],
# # NOTE: run clamd under the same user as amavisd - or run it under its own
# #   uid such as clamav, add user clamav to the amavis group, and then add
# #   AllowSupplementaryGroups to clamd.conf;
# # NOTE: match socket name (LocalSocket) in clamav.conf to the socket name in
# #   this entry; when running chrooted one may prefer a socket under $MYHOME.

```

Add a comment to this line to enable anti-virus scan:

```
# @bypass_virus_check_maps = (1);  # controls running of anti-virus code

```

Add `AllowSupplementaryGroups true` to `/etc/clamav/clamd.conf`.

After that, add `clamav` user to `amavis` group to avoid permission problems:

```
# usermod -a -G amavis clamav

```

Finally restart the services:

*   [restart](/index.php/Restart "Restart") `clamd.service`.
*   [start](/index.php/Start "Start") `amavisd.service` and possibly [enable](/index.php/Enable "Enable") it.

Check for errors with these commands:

```
# systemctl status amavisd
# journalctl -xbo short -u amavisd

```

### Testing

To test the new configuration just telnet to the amavisd default listening port:

```
$ telnet 127.0.0.1 10024

```

You should see something like:

```
Trying 127.0.0.1...
Connected to 127.0.0.1.
Escape character is '^]'
220 [127.0.0.1] ESMTP amavisd-new service ready

```

Type `ehlo 127.0.0.1`:

```
EHLO localhost
250-[127.0.0.1]
250-VRFY
250-PIPELINING
250-SIZE
250-ENHANCEDSTATUSCODES
250-8BITMIME
250-DSN
250 XFORWARD NAME ADDR PORT PROTO HELO IDENT SOURCE

```

Now just type `quit` to exit.

## Integration with Postfix

### Quick start

To configure amavis for [Postfix](/index.php/Postfix "Postfix") add the following to `/etc/postfix/master.cf`:

```
#
# anti spam & anti virus section
#
amavisfeed      unix  -    -       n       -       2       smtp
 -o smtp_data_done_timeout=1200
 -o smtp_send_xforward_command=yes
 -o disable_dns_lookups=yes
 -o max_use=20
127.0.0.1:10025 inet n  -       y       -       -       smtpd
 -o content_filter=
 -o smtpd_delay_reject=no
 -o smtpd_client_restrictions=permit_mynetworks,reject
 -o smtpd_helo_restrictions=
 -o smtpd_sender_restrictions=
 -o smtpd_recipient_restrictions=permit_mynetworks,reject
 -o smtpd_data_restrictions=reject_unauth_pipelining
 -o smtpd_end_of_data_restrictions=
 -o smtpd_restrictions_classes=
 -o mynetworks=127.0.0.0/8
 -o smtpd_error_sleep_time=0
 -o smtpd_soft_error_limit=1001 
 -o smtpd_hard_error_limit=1000
 -o smtpd_client_connection_count_limit=0
 -o smtpd_client_connection_rate_limit=0
 -o receive_override_options=no_header_body_checks,no_unknown_recipient_checks,no_milters
 -o local_header_rewrite_clients=
```

In this configuration we assume that postfix and Amavis are running on the same machine (i.e. `127.0.0.1`). If that is not the case edit `/etc/amavisd/amavisd.conf` and the prevous Postfix entry accordingly.

Postfix will listen to port `10025` so that Amavis can send back checked emails to that port.

You also have to add another other configuration in your `smtp` or `submission` sections:

```
-o content_filter=amavisfeed:[127.0.0.1]:10024

```

Using this options implies that Postfix will send emails to Amavis on port `10024`, so that these can be checked. If mail passes the control then these are sent to port `10025`, as explained before.

We can now [restart](/index.php/Restart "Restart") `postfix.service` and `amavis.service`.

To check that Postfix is listening on port `10025` do the same operations as the port `10024` case.

## SpamAssassin support

[![Tango-view-fullscreen.png](/images/3/38/Tango-view-fullscreen.png)](/index.php/File:Tango-view-fullscreen.png)

[![Tango-view-fullscreen.png](/images/3/38/Tango-view-fullscreen.png)](/index.php/File:Tango-view-fullscreen.png)

**This article or section needs expansion.**

**Reason:** todo (Discuss in [Talk:Amavis#](https://wiki.archlinux.org/index.php/Talk:Amavis))

Spamassassin is integrated in Amavis so you do not have to start `spamassassin.service`. To enable support for Spamassassin comment the following line in `/etc/amavis/amavis.conf` like this:

```
# @bypass_spam_checks_maps = (1);  # controls running of anti-spam code

```

Edit the SpamAssassin configuration based on your needs:

```
$sa_tag_level_deflt  = 1.0;  # add spam info headers if at, or above that level
$sa_tag2_level_deflt = 1.0;  # add 'spam detected' headers at that level
$sa_kill_level_deflt = 5.0;  # triggers spam evasive actions (e.g. blocks mail)
$sa_dsn_cutoff_level = 8;   # spam level beyond which a DSN is not sent
# $sa_quarantine_cutoff_level = 25; # spam level beyond which quarantine is off
$penpals_threshold_high = $sa_kill_level_deflt;  # do not waste time on hi spam
$bounce_killer_score = 100;  # spam score points to add for joe-jobbed bounces
```

Now you just need to [restart](/index.php/Restart "Restart") `amavisd` service.

## Final test

[![Tango-view-fullscreen.png](/images/3/38/Tango-view-fullscreen.png)](/index.php/File:Tango-view-fullscreen.png)

[![Tango-view-fullscreen.png](/images/3/38/Tango-view-fullscreen.png)](/index.php/File:Tango-view-fullscreen.png)

**This article or section needs expansion.**

**Reason:** todo (Discuss in [Talk:Amavis#](https://wiki.archlinux.org/index.php/Talk:Amavis))

To check that everything is working all right:

*   Send a normal email.
*   Send an email with an [EICAR](http://www.eicar.org/86-0-Intended-use.html) file as attachment.
*   Send an email that would result as spam.
*   Check both Postfix and Amavis logs.

## See also

*   [Amavis official documentation](http://www.ijs.si/software/amavisd/README.postfix.html)
*   [Complete Virtual Mail Server/amvisd spamassassin clamav](https://wiki.gentoo.org/wiki/Complete_Virtual_Mail_Server/amvisd_spamassassin_clamav) on Gentoo wiki.

Retrieved from "[https://wiki.archlinux.org/index.php?title=Amavis&oldid=409034](https://wiki.archlinux.org/index.php?title=Amavis&oldid=409034)"