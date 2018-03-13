*Conky* is a system monitor software for the X Window System. It is available for GNU/Linux and FreeBSD. It is free software released under the terms of the GPL license. Conky is able to monitor many system variables including CPU, memory, swap, disk space, temperature, top, upload, download, system messages, and much more. It is extremely configurable, however, the configuration can be a little hard to understand. *Conky* is a fork of torsmo.

## Contents

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
    *   [2.1 Config file syntax changed](#Config_file_syntax_changed)
*   [3 Fonts](#Fonts)
    *   [3.1 Symbolic Fonts](#Symbolic_Fonts)
*   [4 Tips and tricks](#Tips_and_tricks)
    *   [4.1 Autostart](#Autostart)
    *   [4.2 Prevent flickering](#Prevent_flickering)
    *   [4.3 Dual screen](#Dual_screen)
    *   [4.4 Display package update information](#Display_package_update_information)
    *   [4.5 Display weather forecast](#Display_weather_forecast)
    *   [4.6 Display a countdown timer](#Display_a_countdown_timer)
    *   [4.7 Display RSS feeds](#Display_RSS_feeds)
    *   [4.8 Display rTorrent stats](#Display_rTorrent_stats)
    *   [4.9 Display your WordPress blog stats](#Display_your_WordPress_blog_stats)
    *   [4.10 Display number of new emails](#Display_number_of_new_emails)
        *   [4.10.1 Gmail](#Gmail)
            *   [4.10.1.1 method 1](#method_1)
            *   [4.10.1.2 method 2](#method_2)
            *   [4.10.1.3 method 3](#method_3)
        *   [4.10.2 IMAP + SSL using Perl](#IMAP_.2B_SSL_using_Perl)
        *   [4.10.3 IMAP using PHP](#IMAP_using_PHP)
    *   [4.11 Show graphic of active network interface](#Show_graphic_of_active_network_interface)
    *   [4.12 Display log files](#Display_log_files)
*   [5 User-contributed configuration examples](#User-contributed_configuration_examples)
    *   [5.1 A sample rings script with nvidia support](#A_sample_rings_script_with_nvidia_support)
*   [6 Trouble Shooting](#Trouble_Shooting)
    *   [6.1 Conky starts and doesn't display anything on the screen](#Conky_starts_and_doesn.27t_display_anything_on_the_screen)
    *   [6.2 Transparency](#Transparency)
        *   [6.2.1 Pseudo-transparency](#Pseudo-transparency)
        *   [6.2.2 Enable real transparency](#Enable_real_transparency)
    *   [6.3 Do not minimize on Show Desktop](#Do_not_minimize_on_Show_Desktop)
    *   [6.4 Integrate with GNOME Shell](#Integrate_with_GNOME_Shell)
    *   [6.5 Fix scrolling with UTF-8 multibyte characters](#Fix_scrolling_with_UTF-8_multibyte_characters)
*   [7 See also](#See_also)

## Installation

[Install](/index.php/Install "Install") the [conky](https://www.archlinux.org/packages/?name=conky) package. There are also alternative packages you can install from [AUR](/index.php/AUR "AUR") with extra compile options enabled:

*   [conky-cli](https://aur.archlinux.org/packages/conky-cli/) - conky without X11 dependencies
*   [conky-lua](https://aur.archlinux.org/packages/conky-lua/) - with Lua support
*   [conky-lua-nv](https://aur.archlinux.org/packages/conky-lua-nv/) - with both Lua and Nvidia support
*   [conky-nvidia](https://aur.archlinux.org/packages/conky-nvidia/) - with Nvidia support

Some built in variables in conky require additional packages to be installed in order to be utilized, for example [Hddtemp](/index.php/Hddtemp "Hddtemp") for hard drive tempurature and [mpd](/index.php/Mpd "Mpd") for music.

## Configuration

By default conky uses a configuration file located at `~/.conkyrc`. You can print out an example configuration with:

```
$ conky -C

```

If you do not want to have a dotfile in home, you can create a file elsewhere and tell conky to use it using arguments.

For example to tell conky to use a file located in the user's configuration directory:

```
$ conky -c ~/.config/conky/conky.conf

```

Additional example configuration files are available at [this page](https://github.com/brndnmtthws/conky/wiki/User-Configs).

When editing your config file while conky is running, conky will update with the new changes every time you write to the file.

### Config file syntax changed

Since Conky 1.10, configuration files have been written with a new Lua syntax, like so:

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

## Fonts

For displaying Unicode pictures and emoji with conky you will need a [font](/index.php/Fonts#Emoji_and_symbols "Fonts") that supports this and then configure conky to use the font with the Unicode you want to display. For example:

```
 ${font Symbola:size=48}☺${font} 

```

### Symbolic Fonts

Symbolic fonts are also very commonly used in more decorated conky configurations, some of the more popular ones include;

*   [ttf-pizzadude-bullets](https://aur.archlinux.org/packages/ttf-pizzadude-bullets/) - PizzaDude Bullet's font
*   [otf-font-awesome-5-free](https://aur.archlinux.org/packages/otf-font-awesome-5-free/) - Font awesome icon from from [http://fontawesome.com/](http://fontawesome.com/)
*   [ttf-weather-icons](https://aur.archlinux.org/packages/ttf-weather-icons/) - Erik flowers weather icon font with 222 glyphs

## Tips and tricks

### Autostart

In `conky.conf` file:

```
background = true,

```

This variable will fork *conky* to your background. If you want to make your window always visible on your desktop, sticky across all workspaces and not showing in your taskbar, add these arguments:

```
own_window = true,
own_window_type = 'override',

```

The `override` takes *conky* out of the control of your window manager.

To autostart *conky*, create the following file:

 `~/.config/autostart/conky.desktop` 
```
[Desktop Entry]
Type=Application
Name=conky
Exec=conky --daemonize --pause=5
StartupNotify=false
Terminal=false
```

The `pause=5` parameter delays *conky'*s drawing for 5 seconds at startup to make sure that the desktop had time to load and is up.

### Prevent flickering

*Conky* needs Double Buffer Extension *(DBE)* support from the X server to prevent flickering because it cannot update the window fast enough without it. It can be enabled with [Xorg](/index.php/Xorg "Xorg") in `/etc/X11/xorg.conf` with `Load "dbe"` line in `"Module"` section. The `xorg.conf` file has been replaced (1.8.x patch upwards) by `/etc/X11/xorg.conf.d` which contains the particular configuration files. *DBE* is loaded automatically as long as it is present within `/usr/lib/xorg/modules`. The list of loaded modules can be checked with `grep LoadModule /var/log/Xorg.0.log`.

To enable double buffering, add the following option to `conky.conf`:

```
 double_buffer = true,

```

### Dual screen

When using a dual screen configuration, you will need to play with a few options to place your *conky* window.

By adjusting `gap_x`, let's say you are running a 1680x1050 pixels resolution and you want the window on middle top of your left monitor, you will use:

```
alignment = 'top_left',
gap_X = 840,

```

The `alignment` option is self-explanatory, the `gap_X` is the distance, in pixels, from the left border of your screen.

`xinerama_head` is an alternative useful option, the following will place the *conky* window at the top right of the second screen:

```
alignment = 'top_right',
xinerama_head = 2,

```

### Display package update information

[Pacman](/index.php/Pacman "Pacman") provides its own script called `checkupdates` which displays package updates from the official repos. Use `${execi 3600 checkupdates | wc -l}` to display the total number of packages.

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

#### Gmail

If you use 2-factor authentication, you need to use an [App Password](https://myaccount.google.com/apppasswords).

For method 1, 2 and 3:

Create one of the following files in a convenient location (for example in `~/.scripts/`).

Then add the following string to your `conky.conf` in order the check your Gmail account for new email every five minutes (300 seconds) and display:

```
${execi 300 python ~/.scripts/gmail.py}

```

##### method 1

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

##### method 2

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

##### method 3

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

Another alternative using PHP. PHP needs to be installed and `extension=imap.so` must be uncommented in `/etc/php/php.ini`.

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

### Display log files

One of the nice features of *conky* is to pipe to your desktop some `/var/log/` files to read all kinds of log messages. Most of these files can only be read by `root`, but running *conky* as `root` is not recommended, so you will need to add `*username*` to the `log` group:

```
# usermod -aG log *username*

```

## User-contributed configuration examples

### A sample rings script with nvidia support

See [[1]](https://gist.github.com/anonymous/85d052c0c23e58bc3666).

## Trouble Shooting

These are known issues people have with conky and their solutions.

### Conky starts and doesn't display anything on the screen

First check for syntax errors in your configuration file's text variable. Then double check that your user has permission to run every command inside your configuration file and that all needed packages are installed.

### Transparency

Conky supports two different types of transparency. Pseudo-transparency and real transparency that requires a [composite manager](/index.php/Xorg#Composite "Xorg") to be installed and running. If you enable real transparency and don't have a composite manager running your conky will not be alpha transparent with transparency enabled for fonts and images as well as the background.

#### Pseudo-transparency

Pseudo-transparency is enabled by default in conky. Pseudo-transparency works by copying the background image from the root window and using the relevant section as the background for conky. Some window managers set the background wallpaper to a level above the root window which can cause conky to have a grey background. To fix this issue you need to set it manually with feh.

In `~/.xinitrc`:

```
 sleep 1 && feh --bg-center ~/background.png &

```

#### Enable real transparency

To enable real transparency, you must have a [composite manager](/index.php/Xorg#Composite "Xorg") running and the following lines added to `.conkyrc` inside the conky.config array:

```
 conky.config = {
    own_window = true,
    own_window_transparent = true,
    own_window_argb_visual = true,
    own_window_type = desktop,
 }

```

If window type "desktop" does not work try changing it to `normal`. If that does not work try the other options: `dock`, `panel`, or `override` instead.

**Note:** [Xfce](/index.php/Xfce "Xfce") requires enabled compositing, see [[2]](https://forum.xfce.org/viewtopic.php?pid=25939).

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

### Integrate with GNOME Shell

Some have experienced problems with *conky* showing up under [GNOME](/index.php/GNOME "GNOME").

Add these lines to `conky.conf`:

```
own_window = true,
own_window_type = 'desktop',

```

### Fix scrolling with UTF-8 multibyte characters

The current version of *conky* (1.9.0) suffers from a [bug](https://github.com/brndnmtthws/conky/issues/129) where scrolling text increments by byte, not by character, resulting in text containing multibyte characters to disappear and reappear while scrolling. A package with a patch fixing this bug can be found in the AUR: [conky-utfscroll](https://aur.archlinux.org/packages/conky-utfscroll/)

## See also

*   [Official website](https://github.com/brndnmtthws/conky)
*   [Official Conky variables for configuration](http://conky.sourceforge.net/config_settings.html)
*   [Official Conky objects](http://conky.sourceforge.net/variables.html)
*   [Conky Configs on arch forums](https://bbs.archlinux.org/viewtopic.php?id=39906)
*   [Conky](http://freecode.com/projects/conky/) on [Freecode](https://en.wikipedia.org/wiki/Freecode "wikipedia:Freecode")
*   [#conky](irc://chat.freenode.org/conky) IRC chat channel on [freenode](https://en.wikipedia.org/wiki/Freenode "wikipedia:Freenode")
*   [FAQ](http://novel.evilcoder.org/wiki/index.php?title=ConkyFAQ&oldid=12463)