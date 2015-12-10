# Exim with remote SMTP server

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

This document describes how to set up Exim (a mail transfer agent) to use a remote smtp server, for example your ISP's smtp server.

## Contents

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
    *   [2.1 Hide machine name](#Hide_machine_name)
*   [3 Update: 11-Feb-05](#Update:_11-Feb-05)
*   [4 Update: 10-Feb-08](#Update:_10-Feb-08)
*   [5 Update 10-Oct-15](#Update_10-Oct-15)
*   [6 Using GMail as smarthost](#Using_GMail_as_smarthost)
*   [7 Troubleshooting](#Troubleshooting)
    *   [7.1 451 Temporary local problem](#451_Temporary_local_problem)

## Installation

[Install](/index.php/Install "Install") the [exim](https://www.archlinux.org/packages/?name=exim) package.

## Configuration

Edit `/etc/mail/exim.conf` and add or change the following:

In Main Configuration Settings uncomment `primary_hostname` and add the hostname of your box (see the `/etc/hostname` file):

```
primary_hostname = myhostname          # change to your hostname

```

At the end of the Routers Configuration section add:

```
pass_on_to_isp:
  driver = manualroute
  domains = !+local_domains
  transport = remote_smtp
  route_list = * smtp.myisp.com        # change to the desired smtp server
```

Make sure that in Transports Configuration it says (uncommented):

```
remote_smtp:
  driver = smtp
```

### Hide machine name

If you have a laptop, or a machine in a smarthost configuration, where you do not want the name of the machine to appear in the outgoing email then you must enable exim's rewriting facilities.

In the Rewriting section you should have something like:

```
*@_machine_._mydomain_ $1@_mydomain_

```

where `_machine_` is the hostname of your laptop or PC and `_mydomain_` is the domain name of the machine and the outgoing mail.

## Update: 11-Feb-05

[![Tango-mail-mark-junk.png](/images/e/e7/Tango-mail-mark-junk.png)](/index.php/File:Tango-mail-mark-junk.png)

[![Tango-mail-mark-junk.png](/images/e/e7/Tango-mail-mark-junk.png)](/index.php/File:Tango-mail-mark-junk.png)

**This article or section needs language, wiki syntax or style improvements.**

**Reason:** Written in first person, see [Help:Style](/index.php/Help:Style "Help:Style"). Should be integrated normally with the rest of the article (a wiki is not a blog). (Discuss in [Talk:Exim with remote SMTP server#](https://wiki.archlinux.org/index.php/Talk:Exim_with_remote_SMTP_server))

FYI - I just got done wrestling with Exim (4.44) to get it up and running in this configuration on my machine, and I had to do a number of things quite differently than the other person. Thought I would capture them here for posterity, since I had to go through a pretty painful process that cost me a lot of time and aggravation before I hit upon the right config. Hopefully this will save others from a similar fate.

By the way, I should note: my Exim server does not receive any emails directly from the Net. I'm using fetchmail to grab the mail's from an external POP mail drop and dump them into my Exim server. So perhaps this is different than the other person's configuration.

Anyway, here is what worked for me.

I did not need to update `primary_hostname`. If you leave it commented out, like this:

 `# primary_hostname =` 

then exim will just automatically use whatever your system's `hostname` command outputs. (i.e., the `HOSTNAME` that you have set in rc.conf.) I very much DID need to update this line:

 `domainlist local_domains = @` 

and it caused me much grief until I got it right! In my case, it needed to look like this:

 `domainlist local_domains = @:localhost:mydnamicdnshostname.homeip.net` 

I think the dynamic dns entry might be optional (since I never really deliver any mail to an address at that FQDN), but the `@` and the `localhost` are both critical.

*   `@` basically means again to use whatever your system's `hostname` command outputs. That is needed because some daemons that run on your box may try to send emails to the root user at the host, and they will get rejected if you do not have the `@` entry.
*   `localhost` was necessary in order to allow fetchmail to deliver all the messages that it fetched. Without that entry there, Exim would fail to deliver them, and then generate a bounce message in response. Even worse, most of my fetched messages were spam, and so it would try to send the bounce back to the return address on the spam which 1) often was forged, and thus a bad thing to do, and 2) often would get rejected either due to an invalid email address or because I was trying to initiate email from a residential dynamic IP address and thus was also a bad thing to do. In the latter case, those messages wound up frozen on the queue, and I had to spend some time manually purging them from the queue. Just a bad situation all around until I got this piece right.
*   I also wanted to allow other boxes on my LAN to relay messages through this exim server. By default, though, that is blocked. You can enable it by changing this:

 `hostlist   relay_from_hosts = 127.0.0.1` 

to this:

 `hostlist   relay_from_hosts = 127.0.0.1 : 192.168.0.0/24` 

While, you are at it, it actually could not hurt to make it this:

 `hostlist   relay_from_hosts = 127.0.0.1 : ::::1 : 192.168.0.0/24` 

(The `::::1` is just the ipv6 equivalent of 127.0.0.1)

Despite what was written by the other person, I found that that the `pass_on_to_isp` router should NOT go at the end of the Routers Configuration section. Since it is at the end, it will not get executed if some other router gets executed first, and that is exactly what was happening to me. This router, which appears before it was getting executed instead:

```
dnslookup:
  driver = dnslookup
  domains = ! +local_domains
  transport = remote_smtp
  ignore_target_hosts = 0.0.0.0 : 127.0.0.0/8
  no_more
```

That router might be desired in some configurations, but not this one. That will cause exim to try to deliver the message itself, rather than passing it on to your ISP's MTA. (And as I indicated above, that will often fail if you are on a residential dynamic IP adddress.) To set this up properly, do it like this:

```
#dnslookup:
#  driver = dnslookup
#  domains = ! +local_domains
#  transport = remote_smtp
#  ignore_target_hosts = 0.0.0.0 : 127.0.0.0/8
#  no_more

pass_on_to_isp:
  driver = manualroute
  domains = !+local_domains
  transport = remote_smtp
  route_list = * smtp.myisp.com        # change to the desired smtp server
```

One last thing: make sure to also update the `/etc/mail/aliases` file, if you have got any daemons running on your box that need to send email to the root user. You will probably want those emails to get delivered to your non-root user account instead, and this is how you set that behavior. Look for these lines:

```
# Person who should get root's mail
#root:

```

And uncomment and add your local user account to the `root:` line:

```
# Person who should get root's mail
root: johndoe

```

Hope this all spares someone some hair-pulling and lost sleep down the road. I wish I had read an entry like this before I started - I would not be so tired right now!

## Update: 10-Feb-08

[![Tango-mail-mark-junk.png](/images/e/e7/Tango-mail-mark-junk.png)](/index.php/File:Tango-mail-mark-junk.png)

[![Tango-mail-mark-junk.png](/images/e/e7/Tango-mail-mark-junk.png)](/index.php/File:Tango-mail-mark-junk.png)

**This article or section needs language, wiki syntax or style improvements.**

**Reason:** Should be integrated normally with the rest of the article (a wiki is not a blog). (Discuss in [Talk:Exim with remote SMTP server#](https://wiki.archlinux.org/index.php/Talk:Exim_with_remote_SMTP_server))

```
pass_on_to_isp:
  driver = manualroute
  domains = !+local_domains
  transport = remote_smtp
  route_list = * smtp.myisp.com        # change to the desired smtp server
```

should be changed to

```
send_to_gateway:
  driver = manualroute
  domains = !+local_domains
  transport = remote_smtp
  route_list = * smtp.myisp.com        # change to the desired smtp server
```

## Update 10-Oct-15

[![Tango-mail-mark-junk.png](/images/e/e7/Tango-mail-mark-junk.png)](/index.php/File:Tango-mail-mark-junk.png)

[![Tango-mail-mark-junk.png](/images/e/e7/Tango-mail-mark-junk.png)](/index.php/File:Tango-mail-mark-junk.png)

**This article or section needs language, wiki syntax or style improvements.**

**Reason:** Written in first person, see [Help:Style](/index.php/Help:Style "Help:Style"). Should be integrated normally with the rest of the article (a wiki is not a blog). (Discuss in [Talk:Exim with remote SMTP server#](https://wiki.archlinux.org/index.php/Talk:Exim_with_remote_SMTP_server))

I found the information here a little confusing and may be out of date. The following sum total changes worked for me:

```
 diff /etc/exim.conf.orig /etc/exim.conf
 405c405
 <   require verify        = sender
 ---
 >   #require verify        = sender
 555,559c555,559
 < dnslookup:
 <   driver = dnslookup
 <   domains = ! +local_domains
 <   transport = remote_smtp
 <   ignore_target_hosts = 0.0.0.0 : 127.0.0.0/8
 ---
 > #dnslookup:
 > #  driver = dnslookup
 > #  domains = ! +local_domains
 > #  transport = remote_smtp
 > #  ignore_target_hosts = 0.0.0.0 : 127.0.0.0/8
 562c562
 <   no_more
 ---
 > #  no_more
 578a579,584
 > smarthost:
 >   driver = manualroute
 >   domains = !+local_domains
 >   transport = remote_smtp
 >   route_list = * mail.internode.on.net
 >   ignore_target_hosts = <; 0.0.0.0 ; 127.0.0.0/8 ; ::1
 772a779
 > *@* $1@bullet.homenet.org Ffr

```

I.e. just comment out the dnslookup block and add the smarthost block plus the single rewrite rule (last line above). That line is added just after the "begin rewrite" section. I was getting DNS timeouts for the "require verify = sender" for most messages so I had to disable that also. Restart exim and it is good to go.

## Using GMail as smarthost

**Note:** The following must be put in the appropriate sections of the configuration file, eg, after **begin authenticators**.

Add a router before or instead of the dnslookup router:

```
gmail_route:
  driver = manualroute
  transport = gmail_relay
  route_list = * smtp.gmail.com
```

Add a transport:

```
gmail_relay:
  driver = smtp
  port = 587
  hosts_require_auth = <; $host_address
  hosts_require_tls = <; $host_address
```

Add an authenticator (replacing myaccount@gmail.com and mypassword with your own account details):

```
gmail_login:
  driver = plaintext
  public_name = LOGIN
  hide client_send = : myaccount@gmail.com : mypassword
```

`$host_address` is used for `hosts_require_auth` and `hosts_require_tls` instead of smtp.gmail.com to avoid occasional 530 5.5.1 Authentication Required errors. These are caused by the changing IP addresses in DNS queries for smtp.gmail.com. `$host_address` will expand to the particular IP address that was resolved by the `gmail_route` router.

For added security, use a per-application password. This works with Google Apps accounts as well.

## Troubleshooting

### 451 Temporary local problem

If you are getting a "451 Temporary Local Problem" when testing SMTP, you are probably sending as root. By default Exim will not allow you to send as root.

Retrieved from "[https://wiki.archlinux.org/index.php?title=Exim_with_remote_SMTP_server&oldid=404158](https://wiki.archlinux.org/index.php?title=Exim_with_remote_SMTP_server&oldid=404158)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [Mail server](/index.php/Category:Mail_server "Category:Mail server")