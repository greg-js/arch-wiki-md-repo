Related articles

*   [Conky](/index.php/Conky "Conky")

Go back to [Conky](/index.php/Conky "Conky").

## Contents

*   [1 Display package update information](#Display_package_update_information)
*   [2 Display log files](#Display_log_files)
*   [3 Display weather forecast](#Display_weather_forecast)
*   [4 Display a countdown timer](#Display_a_countdown_timer)
*   [5 Display RSS feeds](#Display_RSS_feeds)
*   [6 Display a calendar for the current month](#Display_a_calendar_for_the_current_month)
*   [7 Display rTorrent stats](#Display_rTorrent_stats)
*   [8 Display your WordPress blog stats](#Display_your_WordPress_blog_stats)
*   [9 Display number of new emails](#Display_number_of_new_emails)
    *   [9.1 Gmail](#Gmail)
        *   [9.1.1 method 1](#method_1)
        *   [9.1.2 method 2](#method_2)
        *   [9.1.3 method 3](#method_3)
        *   [9.1.4 IMAP + SSL using Perl](#IMAP_.2B_SSL_using_Perl)
        *   [9.1.5 IMAP using PHP](#IMAP_using_PHP)
*   [10 Show graphic of active network interface](#Show_graphic_of_active_network_interface)
*   [11 User-contributed configuration examples](#User-contributed_configuration_examples)

## Display package update information

[pacman-contrib](https://www.archlinux.org/packages/?name=pacman-contrib) provides a script called `checkupdates` which displays package updates from the official repos. Use `${execi 3600 checkupdates | wc -l}` to display the total number of packages.

## Display log files

One of the nice features of *conky* is to pipe to your desktop some `/var/log/` files to read all kinds of log messages. Most of these files can only be read by `root`, but running *conky* as `root` is not recommended, so you will need to add `*username*` to the `log` group:

```
# usermod -aG log *username*

```

## Display weather forecast

See [this thread](https://bbs.archlinux.org/viewtopic.php?id=37381).

Another weather script in lua: [here](https://bbs.archlinux.org/viewtopic.php?id=222998)

## Display a countdown timer

[ConkyTimer](https://github.com/orschiro/scriptlets/tree/master/ConkyTimer) is a simple countdown timer that displays the remaining time of a defined task.

Start the timer using `conkytimer "<task description>" <min>`.

## Display RSS feeds

*Conky* has the ability to display RSS feeds natively without the need for an outside script to run and output into Conky. For example, to display the titles of the ten most recent Planet Arch updates and refresh the feed every minute, you would put this into your `conky.conf` in the `TEXT` section:

```
${rss [https://planet.archlinux.org/rss20.xml](https://planet.archlinux.org/rss20.xml) 1 item_titles 10 }

```

If you want to display Arch Forum rss feed, add this line:

```
${rss [https://bbs.archlinux.org/extern.php?action=feed&type=rss](https://bbs.archlinux.org/extern.php?action=feed&type=rss) 1 item_titles 4}

```

where 1 is in minutes the refresh interval (15 mn is default),4 the number of items you wish to show.

## Display a calendar for the current month

You can use the following lua script to display a calendar. It uses `color1` and the default color from your configuration. It looks best with a monospace font.

```
 #!/usr/bin/env lua

 conky_color = "${color1}%2d${color}"

 t = os.date('*t', os.time())
 year, month, currentday = t.year, t.month, t.day

 daystart = os.date("*t",os.time{year=year,month=month,day=01}).wday

 month_name = os.date("%B")

 days_in_month = {
     31, 28, 31, 30, 31, 30, 
     31, 31, 30, 31, 30, 31
 }

 -- check for leap year
 -- Any year that is evenly divisible by 4 is a leap year
 -- Any year that is evenly divisible by 100 is a leap year if
 -- it is also evenly divisible by 400.
 LeapYear = function (year)
     return year % 4 == 0 and (year % 100 ~= 0 or year % 400 == 0)
 end

 if LeapYear(year) then
     days_in_month[2] = 29
 end

 title_start = (20 - (string.len(month_name) + 5)) / 2

 title = string.rep(" ", math.floor(title_start+0.5)) .. -- add padding to center the title
         (" %s %s
 Su Mo Tu We Th Fr Sa
"):format(month_name, year)

 io.write(title)

 function seq(a,b)
     if a > b then
         return
     else
         return a, seq(a+1,b)
     end 
 end

 days = days_in_month[month]

 io.write(
     string.format(
         string.rep("   ", daystart-1) ..
         string.rep(" %2d", days), seq(1,days)
     ):gsub(string.rep(".",21),"%0
")
      :gsub(("%2d"):format(currentday),
            (conky_color):format(currentday)
      ) .. "
"
 )

```

Inside your `conky.conf` you can then place the following, making sure the path matches where you saved the script.

```
 conky.text = [[
 ${execpi 3600 ~/.config/conky/cal.lua}
 ]]

```

## Display rTorrent stats

See [this thread](https://bbs.archlinux.org/viewtopic.php?id=67304).

## Display your WordPress blog stats

This can be achieved by using the in python written extension named [ConkyPress](http://evilshit.wordpress.com/2013/04/20/conkypress-a-wordpress-stats-visualization-tool-for-your-desktop/).

## Display number of new emails

Conky has built in support for IMAP and POP3, but does not have support for access over ssl. Conky's FAQ recommends using [stunnel](https://www.archlinux.org/packages/?name=stunnel) for this and has an example configuration [here](http://conky.sourceforge.net/faq.html#Conky's-built-in-IMAP-and-POP3-doesn't-support-SSL-or-TLS/).

Modify `/etc/stunnel/stunnel.conf` as follows, and then [start](/index.php/Start "Start") `stunnel.service`:

1.  Service-level configuration for TLS server

```
[imap]
client = yes
accept  = 143
connect = imap.gmail.com:143
protocol = imap
sslVersion = TLSv1
# Service-level configuration for SSL server
[imaps]
client = yes
accept  = 993
connect = imap.gmail.com:993

```

Then add the following to `conky.conf`:

```
conky.config = {
    imap = "localhost username password [-i 120] [-f 'inbox'] [-p 993]",
}

```

```
conky.text {
    Inbox: ${imap_unseen}/${imap_messages}
}

```

### Gmail

If you use 2-factor authentication, you need to use an [App Password](https://myaccount.google.com/apppasswords).

For method 1, 2 and 3:

Create one of the following files in a convenient location (for example in `~/.scripts/`).

Then add the following string to your `conky.conf` in order the check your Gmail account for new email every five minutes (300 seconds) and display:

```
${execi 300 python ~/.scripts/gmail.py}

```

#### method 1

This script uses retrieves the number of new email via Gmail's Atom API.

 `gmail.py` 
```
#!/usr/bin/env python3

import urllib.request

email = 'your email'
password = 'your password'

# Set up authentication for gmail
auth_handler = urllib.request.HTTPBasicAuthHandler()
auth_handler.add_password(realm='mail.google.com',
                          uri='https://mail.google.com/',
                          user=email,
                          passwd=password)
opener = urllib.request.build_opener(auth_handler)
# ...and install it globally so it can be used with urlopen.
urllib.request.install_opener(opener)

gmailurl = 'https://mail.google.com/gmail/feed/atom'
with urllib.request.urlopen(gmailurl) as page:
    contents = page.read().decode('utf-8')

ifrom = contents.index('<fullcount>') + 11
ito   = contents.index('</fullcount>')

fullcount = contents[ifrom:ito]

print('{} new emails'.format(fullcount))

```

#### method 2

Same as method 1, but does proper XML parsing.

 `gmail.py` 
```
#!/usr/bin/env python3

import urllib.request
from xml.etree import ElementTree as etree

email = 'your email'
password = 'your password'

# Set up authentication for gmail
auth_handler = urllib.request.HTTPBasicAuthHandler()
auth_handler.add_password(realm='mail.google.com',
                          uri='https://mail.google.com/',
                          user=email,
                          passwd=password)
opener = urllib.request.build_opener(auth_handler)
# ...and install it globally so it can be used with urlopen.
urllib.request.install_opener(opener)

gmailurl = 'https://mail.google.com/gmail/feed/atom'
NS = '{http://purl.org/atom/ns#}'
with urllib.request.urlopen(gmailurl) as source:
    tree = etree.parse(source)
fullcount = tree.find(NS + 'fullcount').text

print('{} new emails'.format(fullcount))

```

#### method 3

The same way, but with using `curl`, `grep` and `sed`:

 `gmail.sh` 
```
#!/usr/bin/sh

curl -s -u **email**:**password** https://mail.google.com/mail/feed/atom | grep fullcount | sed 's/<[^0-9]*>//g'

```

replace *email* and *password* with your data.

#### IMAP + SSL using Perl

*Conky* has built in support for IMAP accounts but does not support SSL. This can be provided using this script from [this forum post](http://www.unix.com/shell-programming-scripting/115322-perl-conky-gmail-imap-unread-message-count.html). This requires the Perl/CPAN Modules Mail::IMAPClient and IO::Socket::SSL which are in the [perl-mail-imapclient](https://aur.archlinux.org/packages/perl-mail-imapclient/) and [perl-io-socket-ssl](https://www.archlinux.org/packages/?name=perl-io-socket-ssl) packages

Create a file named `imap.pl` in a location to be read by *conky* (for example in `~/.scripts/`). In this file, add (with the appropriate changes):

 `imap.pl` 
```
#!/usr/bin/perl

# by gxmsgx
# description: get the count of unread messages on imap

use strict;
use Mail::IMAPClient;
use IO::Socket::SSL;

my $username = 'example.username'; 
my $password = 'password123'; 

my $socket = IO::Socket::SSL->new(
  PeerAddr => 'imap.server',
  PeerPort => 993
 )
 or die "socket(): $@";

my $client = Mail::IMAPClient->new(
  Socket   => $socket,
  User     => $username,
  Password => $password,
 )
 or die "new(): $@";

if ($client->IsAuthenticated()) {
  my $msgct;

  $client->select("INBOX");
  $msgct = $client->unseen_count||'0';
  print "$msgct
";
}

$client->logout();

```

Add to `conky.conf`:

```
${execi 300 ~/.scripts/imap.pl} 

```

or wherever you saved the file.

If you use Gmail you might need to [generate](http://www.google.com/accounts/IssuedAuthSubTokens?hide_authsub=1) an application specific password.

Alternatively, you can use stunnel as shown above: [#Gmail](#Gmail)

#### IMAP using PHP

Another alternative using PHP. PHP needs to be installed and `extension=imap` must be uncommented in `/etc/php/php.ini`.

Then create a file named `imap.php` in a location to be read by *conky* (for example in `~/.scripts/`). Make the file executable:

```
$ chmod +x imap.php

```

In this file, add (with the appropriate changes):

 `imap.php` 
```
#!/usr/bin/php
<?php
// See http://php.net/manual/function.imap-open.php for more information about
// the mailbox string in the first parameter of imap_open.
// This example is ready to use with Office 365 Exchange Mails,
// just replace your username (=email address) and the password.
$mbox = imap_open("{outlook.office365.com:993/imap/ssl/novalidate-cert}", "username", "password");

// Total number of emails
$nrTotal = imap_num_msg($mbox);

// Number of unseen emails. There are other ways using imap_status to count
// unseen messages, but they don't work with Office 365 Exchange. This one does.
$unseen = imap_search($mbox, 'UNSEEN');
$nrUnseen = $unseen ? count($unseen) : 0;

// Display the result, format as you like.
echo $nrUnseen.'/'.$nrTotal;

// Not needed, because the connection is closed after the script end.
// For the sake of clean public available scripts, we are nice to
// the imap server and close the connection manually.
imap_close($mbox);

```

Add to `conky.conf`:

```
${execi 300 ~/.scripts/imap.php} 

```

or wherever you saved the file.

This script displays A/B where A is the number of unseen emails and B is the total number of mails in the mailbox. There are a lot of other information available through a lot of PHP functions like with imap_Status ([http://php.net/manual/function.imap-status.php](http://php.net/manual/function.imap-status.php)). Just see the PHP docs about IMAP: [http://php.net/manual/ref.imap.php](http://php.net/manual/ref.imap.php).

## Show graphic of active network interface

To test if a network inferface is currently active, you can use the test conky variable `if_existing` on the `operstate` of the interface. Here's an example for wlo1 :

```
draw_graph_borders yes 
${if_existing /sys/class/net/wlo1/operstate up}
${color #0077ff}Net Down:$color ${downspeed wlo1}      ${color #0077ff}Net Up:$color ${upspeed wlo1}
${color #0077ff}${downspeedgraph wlo1 32,155 104E8B 0077ff} $alignr${color #0077ff}${upspeedgraph wlo1 32,155 104E8B 0077ff}
${endif}

```

This is the expected result :

[http://i.imgur.com/pQQbsP6.png](http://i.imgur.com/pQQbsP6.png)

## User-contributed configuration examples

*   A sample rings script with nvidia support - [gist](https://gist.github.com/anonymous/85d052c0c23e58bc3666)