*Conky* is a system monitor software for the X Window System. It is available for GNU/Linux and FreeBSD. It is free software released under the terms of the GPL license. Conky is able to monitor many system variables including CPU, memory, swap, disk space, temperature, top, upload, download, system messages, and much more. It is extremely configurable, however, the configuration can be a little hard to understand. *Conky* is a fork of torsmo.

## Contents

*   [1 Installation and configuration](#Installation_and_configuration)
    *   [1.1 AUR packages](#AUR_packages)
*   [2 Tips and tricks](#Tips_and_tricks)
    *   [2.1 Config file syntax changed](#Config_file_syntax_changed)
    *   [2.2 Enable real transparency in KDE4 and Xfce4](#Enable_real_transparency_in_KDE4_and_Xfce4)
    *   [2.3 Autostart with Xfce4](#Autostart_with_Xfce4)
    *   [2.4 Prevent flickering](#Prevent_flickering)
    *   [2.5 Custom colors](#Custom_colors)
    *   [2.6 Dual Screen](#Dual_Screen)
    *   [2.7 Do not minimize on Show Desktop](#Do_not_minimize_on_Show_Desktop)
    *   [2.8 Integrate with GNOME](#Integrate_with_GNOME)
    *   [2.9 Integrate with Razor-qt](#Integrate_with_Razor-qt)
    *   [2.10 Display package update information](#Display_package_update_information)
    *   [2.11 Display weather forecast](#Display_weather_forecast)
    *   [2.12 Display a countdown timer](#Display_a_countdown_timer)
    *   [2.13 Display RSS feeds](#Display_RSS_feeds)
    *   [2.14 Display rTorrent stats](#Display_rTorrent_stats)
    *   [2.15 Display your WordPress blog stats](#Display_your_WordPress_blog_stats)
    *   [2.16 Display number of new emails](#Display_number_of_new_emails)
        *   [2.16.1 Gmail](#Gmail)
            *   [2.16.1.1 method 1](#method_1)
            *   [2.16.1.2 method 2](#method_2)
            *   [2.16.1.3 method 3](#method_3)
            *   [2.16.1.4 method 4](#method_4)
        *   [2.16.2 IMAP + SSL using Perl](#IMAP_.2B_SSL_using_Perl)
        *   [2.16.3 IMAP using PHP](#IMAP_using_PHP)
    *   [2.17 Show graphic of active network interface](#Show_graphic_of_active_network_interface)
    *   [2.18 Fix scrolling with UTF-8 multibyte characters](#Fix_scrolling_with_UTF-8_multibyte_characters)
*   [3 User-contributed configuration examples](#User-contributed_configuration_examples)
    *   [3.1 A sample rings script with nvidia support](#A_sample_rings_script_with_nvidia_support)
*   [4 A note about symbolic fonts](#A_note_about_symbolic_fonts)
*   [5 Fonts appear smaller than they should with Infinality](#Fonts_appear_smaller_than_they_should_with_Infinality)
*   [6 Universal method to enable true transparency](#Universal_method_to_enable_true_transparency)
*   [7 See also](#See_also)

## Installation and configuration

[Install](/index.php/Install "Install") the [conky](https://www.archlinux.org/packages/?name=conky) package. For alternative packages with more features, see [#AUR packages](#AUR_packages).

Create a local configuration file:

```
$ mkdir -p ~/.config/conky
$ conky -C > ~/.config/conky/conky.conf

```

Now you can edit `~/.config/conky/conky.conf` to customize conky as you wish. For a few example configuration files, see [this page](https://github.com/brndnmtthws/conky/wiki/User-Configs).

When editing your config file, you will see immediately the effect of any change as soon as you save it. There is no need to log out/log in your X session. So best is to test all kind of options, one by one, save the configuration file and see the change on your *conky* window, and correct if your change is inappropriate.

One of the nice features of *conky* is to pipe to your desktop some `/var/log/` files to read all kinds of log messages. Most of these files can only be read by `root`, but running *conky* as `root` is not recommended, so you will need to add `*username*` to the `log` group:

```
# usermod -aG log *username*

```

### AUR packages

In addition to the basic *conky* package, there are various [AUR](/index.php/AUR "AUR") packages available with extra compile options enabled:

*   **conky-cli** — *Conky* without X11 dependencies

	|| [conky-cli](https://aur.archlinux.org/packages/conky-cli/)

*   **conky-lua** — *Conky* with Lua support

	|| [conky-lua](https://aur.archlinux.org/packages/conky-lua/)

*   **conky-lua-nv** — *Conky* with both Lua and Nvidia support

	|| [conky-lua-nv](https://aur.archlinux.org/packages/conky-lua-nv/)

*   **conky-nvidia** — *Conky* with Nvidia support

	|| [conky-nvidia](https://aur.archlinux.org/packages/conky-nvidia/)

## Tips and tricks

### Config file syntax changed

Since Conky 1.10, configuration files have been written with Lua syntax, like so:

```
 conky.config = {
   -- Comments start with a double dash
   bool_value = true,
   string_value = 'foo',
   int_value = 42,
 }
 conky.text = [[
 $variable
 ${evaluated variable}
 ]]

```

Some examples below may still use the old syntax, which looks like this:

```
 bool_value yes
 string_value 'foo'
 int_value 42

```

A Lua script is available to convert from the old syntax to the new Lua syntax [here](https://github.com/brndnmtthws/conky/blob/master/extras/convert.lua).

If in doubt, or something doesn't work at all, you can start with the default config file:

```
 $ conky -C > conky.conf.default

```

### Enable real transparency in KDE4 and Xfce4

Since version 1.8.0 *conky* supports real transparency. To enable it add this line to `conky.conf`:

```
own_window_transparent = true,

```

The above option is not desired with the `OWN_WINDOW_ARGB_VISUAL yes` option. This replaces the [feh](https://www.archlinux.org/packages/?name=feh) method described below.

**Note:** [Xfce](/index.php/Xfce "Xfce") requires enabled compositing, see [[1]](https://forum.xfce.org/viewtopic.php?pid=25939).

### Autostart with Xfce4

In `conky.conf` file:

```
background = yes,

```

This variable will fork *conky* to your background. If you want to make your window always visible on your desktop, sticky across all workspaces and not showing in your taskbar, add these arguments:

```
own_window = true,
own_window_type = 'override',

```

The `override` takes *conky* out of the control of your window manager.

Add a `~/.config/autostart/conky.desktop`:

```
[Desktop Entry]
Encoding=UTF-8
Version=0.9.4
Type=Application
Name=conky
Comment=
Exec=conky -d
StartupNotify=false
Terminal=false
Hidden=false

```

### Prevent flickering

*Conky* needs Double Buffer Extension (DBE) support from the X server to prevent flickering because it cannot update the window fast enough without it. It can be enabled in `/etc/X11/xorg.conf` with `Load "dbe"` line in `"Module"` section. The `xorg.conf` file has been replaced (1.8.x patch upwards) by `/etc/X11/xorg.conf.d` which contains the particular configuration files. *DBE* is loaded automatically.

To enable double buffering, add the option

```
 double_buffer = true,

```

to your `conky.conf`.

### Custom colors

Aside the classic preset colors (white, black, yellow...), you can set your own custom color using the color name code. To determine the code of a color, use a color selector app. The basic [gcolor2](https://www.archlinux.org/packages/?name=gcolor2) package in the [official repositories](/index.php/Official_repositories "Official repositories") will give you the color name. It is made of six hexadecimal digits (0-9, A-F). Add this line in your configuration file for a custom color:

```
 color0 = 'white', --convention for standard named colors
 color1 = '00CC00', --convention for hex colors: no pound sign

```

Then, when editing the `TEXT` section, use custom color number previously defined, for example `${color3}` .

### Dual Screen

When using a dual screen configuration, you will need to play with two options to place your *conky* window. Let's say you are running a 1680X1050 pixels resolution, and you want the window on middle top of your left monitor, you will use this:

```
alignment = 'top_left',
gap_X = 840,

```

The `alignment` option is trivial, and `gap_X` option is the distance, in pixels, from the left border of your screen.

The `xinerama_head` option might also need to be set.

### Do not minimize on Show Desktop

**Using Compiz:** If the 'Show Desktop' button or key-binding minimizes Conky along with all other windows, start the Compiz configuration settings manager, go to "General Options" and uncheck the "Hide Skip Taskbar Windows" option.

If you do not use Compiz, try editing `conky.conf` and adding/changing the following line:

```
own_window_type = 'override',

```

or

```
own_window_type = 'desktop',

```

Refer to *conky*s man page for the exact differences. But the latter option enables you to snap windows to *conky*s border using resize key-binds in e.g. Openbox, which the first one does not.

### Integrate with GNOME

Some have experienced problems with *conky* showing up under [GNOME](/index.php/GNOME "GNOME").

*   Add these lines to `conky.conf`:

```
own_window yes
own_window_type conky
own_window_transparent yes
own_window_hints undecorated,below,sticky,skip_taskbar,skip_pager

```

If you still experience problems with transparency. You could add these lines.

```
own_window_argb_visual yes
own_window_argb_value 255

```

### Integrate with Razor-qt

With *conky'*s default configuration, its window might disappear from the desktop when you click on the latter. Add these lines to:

 `conky.conf` 
```
own_window yes
own_window_class Conky
own_window_type normal
own_window_hints undecorated,below,sticky,skip_taskbar,skip_pager
own_window_transparent yes

```

### Display package update information

*   [Pacman](/index.php/Pacman "Pacman") provides its own script called `checkupdates` which displays package updates from the official repos. Use `${execpi 3600 checkupdates | wc -l}` to display the total number of packages.
*   [Paconky](https://bbs.archlinux.org/viewtopic.php?id=68104) - Displays package update information in a user-defined format. The output of this program can be included in Conky with the `${execpi}` command.
*   [Scrolling Notifications](https://bbs.archlinux.org/viewtopic.php?id=53761) - Prints scrolling update notifications. From the author of *paconky*.
*   [Perl Script](https://bbs.archlinux.org/viewtopic.php?id=57291) - Simpler and earlier script from the author of *paconky*. Prints only the number of packages needing an update.
*   [Python Script](https://bbs.archlinux.org/viewtopic.php?id=37284) - Fairly configurable update notification program in [Python](/index.php/Python "Python").
*   [Bash Script](https://bbs.archlinux.org/viewtopic.php?pid=483742#p483742) - [Bash](/index.php/Bash "Bash") script for users that have enabled ShowSize.

### Display weather forecast

See [this thread](https://bbs.archlinux.org/viewtopic.php?id=37381).

### Display a countdown timer

[ConkyTimer](https://github.com/orschiro/scriptlets/tree/master/ConkyTimer) is a simple countdown timer that displays the remaining time of a defined task.

Start the timer using `conkytimer "<task description>" <min>`.

### Display RSS feeds

*Conky* has the ability to display RSS feeds natively without the need for an outside script to run and output into Conky. For example, to display the titles of the ten most recent Planet Arch updates and refresh the feed every minute, you would put this into your `conky.conf` in the `TEXT` section:

```
${rss [https://planet.archlinux.org/rss20.xml](https://planet.archlinux.org/rss20.xml) 1 item_titles 10 }

```

If you want to display Arch Forum rss feed, add this line:

```
${rss [https://bbs.archlinux.org/extern.php?action=feed&type=rss](https://bbs.archlinux.org/extern.php?action=feed&type=rss) 1 item_titles 4}

```

where 1 is in minutes the refresh interval (15 mn is default),4 the number of items you wish to show.

### Display rTorrent stats

See [this thread](https://bbs.archlinux.org/viewtopic.php?id=67304).

### Display your WordPress blog stats

This can be achieved by using the in python written extension named [ConkyPress](http://evilshit.wordpress.com/2013/04/20/conkypress-a-wordpress-stats-visualization-tool-for-your-desktop/).

### Display number of new emails

#### Gmail

##### method 1

Create a file named `gmail.py` in a convenient location (this example uses `~/.scripts/`) with the following [Python](/index.php/Python "Python") code:

 `gmail.py` 
```
#!/usr/bin/env python

from urllib.request import FancyURLopener

email = 'your email' # @gmail.com can be left out
password  = 'your password'

url = 'https://%s:%s@mail.google.com/mail/feed/atom' % (email, password)

opener = FancyURLopener()
page = opener.open(url)

contents = page.read().decode('utf-8')

ifrom = contents.index('<fullcount>') + 11
ito   = contents.index('</fullcount>')

fullcount = contents[ifrom:ito]

print(fullcount + ' new')

```

##### method 2

The following script does less "by hand", and uses more of the capabilities of Python.

 `gmail.py` 
```
#! /usr/bin/env python

import urllib.request
from xml.etree import ElementTree as etree

# Enter your username and password below within quotes below, in place of ****.
# Set up authentication for gmail
auth_handler = urllib.request.HTTPBasicAuthHandler()
auth_handler.add_password(realm='mail.google.com',
                          uri='https://mail.google.com/',
                          user= '****',
                          passwd= '****')
opener = urllib.request.build_opener(auth_handler)
# ...and install it globally so it can be used with urlopen.
urllib.request.install_opener(opener)

gmail = 'https://mail.google.com/gmail/feed/atom'
NS = '{http://purl.org/atom/ns#}'
with urllib.request.urlopen(gmail) as source:
    tree = etree.parse(source)
fullcount = tree.find(NS + 'fullcount').text

print(fullcount + ' new')

```

Add the following string to your `conky.conf` in order the check your Gmail account for new email every five minutes (300 seconds) and display:

```
${execpi 300 python ~/.scripts/gmail.py}

```

##### method 3

The same way, but with using `curl`, `grep` and `sed`:

```
$ curl -s -u '''email''':'''password''' https://mail.google.com/mail/feed/atom | grep fullcount | sed 's/<[^0-9]*>//g'

```

replace *email* and *password* with your data.

##### method 4

Alternatively, you can use [stunnel](http://www.stunnel.org/) which is provided by the [stunnel](https://www.archlinux.org/packages/?name=stunnel) package.

The following configuration is taken from [Conky's FAQ](https://github.com/brndnmtthws/conky/wiki/FAQ)

Modify `/etc/stunnel/stunnel.conf` as follows, and then [start](/index.php/Start "Start") `stunnel.service`:

```
# Service-level configuration for TLS server
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

The only thing left is our `conky.conf`:

```
imap localhost username * -i 120 -p 993
TEXT
Inbox: ${imap_unseen}/${imap_messages}

```

Here I used `*` as the password for *conky* to ask for it at start, but you do **not** have to do it.

#### IMAP + SSL using Perl

*Conky* has built in support for IMAP accounts but does not support SSL. This can be provided using this script from [this forum post](http://www.unix.com/shell-programming-scripting/115322-perl-conky-gmail-imap-unread-message-count.html). This requires the Perl/CPAN Modules Mail::IMAPClient and IO::Socket::SSL which are in the [perl-mail-imapclient](https://aur.archlinux.org/packages/perl-mail-imapclient/) and [perl-io-socket-ssl](https://www.archlinux.org/packages/?name=perl-io-socket-ssl) packages

Create a file named `imap.pl` in a location to be read by *conky*. In this file, add (with the appropriate changes):

```
#!/usr/bin/perl

# gimap.pl by gxmsgx
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
${execpi 300 ~/.conky/imap.pl} 

```

or wherever you saved the file.

If you use Gmail you might need to [generate](http://www.google.com/accounts/IssuedAuthSubTokens?hide_authsub=1) an application specific password.

Alternatively, you can use stunnel as shown above: [#Gmail](#Gmail)

#### IMAP using PHP

Another alternative using PHP. PHP needs to be installed and `extension=imap.so` must be uncommented in `/etc/php/php.ini`.

Then create a file named `imap.php` in a location to be read by *conky*. Make the file executable:

```
$ chmod +x imap.php

```

In this file, add (with the appropriate changes):

```
#!/usr/bin/php
<?php
// See [http://php.net/manual/function.imap-open.php](http://php.net/manual/function.imap-open.php) for more information about
// the mailbox string in the first parameter of imap_open.
// This example is ready to use with Office 365 Exchange Mails,
// just replace your username (=email address) and the password.
$mbox = imap_open("{outlook.office365.com:993/imap/ssl/novalidate-cert}", "username", "password");

// Total number of emails
$nrTotal = imap_num_msg($mbox);

// Number of unseen emails. There are other ways using imap_status to count
// unseen messages, but they don't work with Office 365 Exchange. This one does.
$unseen = imap_search($mbox, 'UNSEEN');
$nrUnseen = $unseen ? count($unseen) : 0;

// Display the result, format as you like.
echo $nrUnseen.'/'.$nrTotal;

// Not needed, because the connection is closed after the script end.
// For the sake of clean public available scripts, we are nice to
// the imap server and close the connection manually.
imap_close($mbox);

```

Add to `conky.conf`:

```
${execpi 300 ~/.conky/imap.php} 

```

or wherever you saved the file.

This script displays A/B where A is the number of unseen emails and B is the total number of mails in the mailbox. There are a lot of other informations available through a lot of PHP functions like with imap_Status ([http://php.net/manual/function.imap-status.php](http://php.net/manual/function.imap-status.php)). Just see the PHP docs about IMAP: [http://php.net/manual/ref.imap.php](http://php.net/manual/ref.imap.php).

### Show graphic of active network interface

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

### Fix scrolling with UTF-8 multibyte characters

The current version of *conky* (1.9.0) suffers from a [bug](https://github.com/brndnmtthws/conky/issues/129) where scrolling text increments by byte, not by character, resulting in text containing multibyte characters to disappear and reappear while scrolling. A package with a patch fixing this bug can be found in the AUR: [conky-utfscroll](https://aur.archlinux.org/packages/conky-utfscroll/)

## User-contributed configuration examples

### A sample rings script with nvidia support

See [[2]](https://gist.github.com/anonymous/85d052c0c23e58bc3666).

## A note about symbolic fonts

Many of the more decorated `conky.conf`'s use the fonts PizzaDude Bullets and Pie Charts for Maps. They are available from the AUR as [ttf-pizzadude-bullets](https://aur.archlinux.org/packages/ttf-pizzadude-bullets/) and [ttf-piechartsformaps](https://aur.archlinux.org/packages/ttf-piechartsformaps/) respectively, or they can be found and downloaded with a quick search and manually installed using the instructions in [Fonts](/index.php/Fonts "Fonts").

## Fonts appear smaller than they should with Infinality

If you notice that your *conky* fonts appear smaller than they should, or they do not align properly, it could be caused by a default setting in the infinality freetype2 patch. This setting can cause some programs to display fonts at 72 DPI instead of 96 even if the rest of your system is set to 96\. If you notice a problem open `/etc/fonts/infinality/infinality.conf` search for the section on DPI and change 72 to 96.

## Universal method to enable true transparency

Transparency is a strange beast in *conky*, but there is a way to universally apply true transparency with any environment or window manager by using *xcompmgr* and *transset-df*. [Install](/index.php/Pacman#Installing_specific_packages "Pacman") [xcompmgr](https://www.archlinux.org/packages/?name=xcompmgr) and [transset-df](https://www.archlinux.org/packages/?name=transset-df).

**Note:** This may conflict with any other compositing manager you are already using.

Check *xcompmgr* documentation to help you decide which compositing options you would like to enable. The following is a common standard command.

```
$ xcompmgr -c -t-5 -l-5 -r4.2 -o.55 &

```

Make sure *conky* is running with `conky &`. Use *transset-df* to enable transparency on the *conky* window. Set '.5' to any value in the range 0 - 1.

```
$ transset-df .5 -n Conky

```

This should give your *conky* window true transparency. If you get an error like:

```
No Window matching Conky exists!

```

verify that *conky* is running, and use *xprop* and click on the *conky* window to find the name you should pass to `transset-df`.

 `$ xprop | grep WM_NAME`  `WM_NAME(STRING) = "Conky (ArchitectLinux)"` 

In this case, *conky* is right, but for you it may be different, so be sure to use your output instead. If `conky.conf` has an option `own_window_type` set to `panel`, then this *xprop* invocation may show no output. Try using `dock`, `normal`, `override` or `desktop` instead.

Use this in `~/.xinitrc` to have transparent *conky* after [X](/index.php/X "X") starts up:

```
xcompmgr -c -t-5 -l-5 -r4.2 -o.55 &
conky -d; sleep 1 && transset-df .5 -n Conky

```

## See also

*   [Official website](https://github.com/brndnmtthws/conky)
*   [Official Conky variables for configuration](http://conky.sourceforge.net/config_settings.html)
*   [Official Conky objects](http://conky.sourceforge.net/variables.html)
*   [Conky Configs on arch forums](https://bbs.archlinux.org/viewtopic.php?id=39906)
*   [Conky](http://freshmeat.net/projects/conky/) on [Freshmeat](https://en.wikipedia.org/wiki/Freshmeat "wikipedia:Freshmeat")
*   [#conky](irc://chat.freenode.org/conky) IRC chat channel on [freenode](https://en.wikipedia.org/wiki/Freenode "wikipedia:Freenode")
*   [FAQ](http://novel.evilcoder.org/wiki/index.php?title=ConkyFAQ&oldid=12463)