Using GNU Screen, Irssi, Bitlbee, and SSH together allows you to have a persistent connection to IRC servers, AOL Instant Messenger, and MSN Instant Messenger. Via SSH, you can access this persistent chat suite from anywhere. Putting the pieces together is not difficult, and this page will guide you through it.

## Contents

*   [1 Components](#Components)
    *   [1.1 GNU Screen](#GNU_Screen)
    *   [1.2 Irssi](#Irssi)
    *   [1.3 Bitlbee](#Bitlbee)
    *   [1.4 SSH](#SSH)
*   [2 Setting it up](#Setting_it_up)
    *   [2.1 Installing](#Installing)
    *   [2.2 Configuring SSH](#Configuring_SSH)
    *   [2.3 Configuring bitlbee](#Configuring_bitlbee)
    *   [2.4 Using Irssi in Screen](#Using_Irssi_in_Screen)
        *   [2.4.1 Connecting to Bitlbee](#Connecting_to_Bitlbee)
*   [3 Using It](#Using_It)
    *   [3.1 Launching the Setup](#Launching_the_Setup)
    *   [3.2 Doing More](#Doing_More)
        *   [3.2.1 Auto-away on screen detach](#Auto-away_on_screen_detach)
            *   [3.2.1.1 Modifying screen-away.pl for BitLBee](#Modifying_screen-away.pl_for_BitLBee)
        *   [3.2.2 Persisting the chat client through suspends and connectivity changes](#Persisting_the_chat_client_through_suspends_and_connectivity_changes)

## Components

### GNU Screen

First we will introduce [GNU Screen](/index.php/GNU_Screen "GNU Screen"). Screen lets you keep shells open, even when you are not actively using them. We will be using it here to keep our IRC session persistent so that we can reconnect to it from anywhere without having to close the IRC client. Read the wiki page and man page for GNU Screen for more information.

### Irssi

[Irssi](/index.php/Irssi "Irssi") is a command-line IRC client. It's very flexible and scriptable. We will be using it, obviously, as our IRC client.

### Bitlbee

[Bitlbee](/index.php/Bitlbee "Bitlbee") is an interesting project. It sets up an IRC server on your local machine, which connects to various instant messenger protocols, and represents logged-in users as IRC users.

### SSH

Everyone knows what [SSH](/index.php/SSH "SSH") is. This will let us use our persistent chat suite from anywhere with web access.

## Setting it up

### Installing

First, update your system and install all of the required packages:

```
pacman -Syu
pacman -S openssh irssi screen bitlbee

```

### Configuring SSH

Follow the directions on [SSH's wiki page](/index.php/SSH "SSH") to set up SSH. It's far too involved to summarize here.

### Configuring bitlbee

The only application which really requires you to configure is Bitlbee. You can follow the directions on [Bitlbee's wiki page](/index.php/Bitlbee "Bitlbee") if you like. All you really need to do is go through /etc/bitlbee/bitlbee.conf and configure it how you like. Below are some modifications worth pointing out.

This will have Bitlbee run as a daemon, which forks a new process for each user that joins. This is simpler than running it through xinetd, so I suggest it.

```
RunMode = ForkDaemon

```

This will have the daemon drop root priveledges after it launches on boot. Do this for security; there is no reason for Bitlbee to run as root.

```
User = bitlbee

```

Be sure to change the password here.

```
OperPassword = 

```

### Using Irssi in Screen

Open up a terminal and run screen. After the copyright message (read the wiki to disable that message), you should find yourself at a plain terminal. Launch irssi in this terminal.

Irssi is a full-fledged IRC client, so we cannot list a complete tutorial here. Use Google to find more information on what irssi can do for you. Now's the time to connect to whatever IRC networks you like.

#### Connecting to Bitlbee

Bitlbee sets up an IRC server on your local machine. To connect to it, run this in irssi:

```
/connect localhost <optional port>

```

You should immediately join a channel called &bitlbee. Here you will see a brief introduction to Bitlbee. Type help to get started. Set up Bitlbee to connect to your instant messenger accounts. You will see your contacts join the channel.

## Using It

Now that we have got Irssi, Bitlbee, and Screen all running, what can we do with it?

First, the whole point of this exercise was to create a persistent chat session that can be accessed from anywhere. From another computer, SSH into your server. Type in

```
screen -raAd 

```

and watch as irssi, with all of your channels and IM connections, pops up. Any messages left for you while you were away are visible, just as if you were at your server.

### Launching the Setup

Since it's a pain to manually connect to each IRC network, join channels, connect to Bitlbee, and have Bitlbee connect to your IM accounts every time you you log in, set up some scripts to help you out.

First, create a Screen initialization file. Here is mine:

```
# ~/irc_screen
source ~/.screenrc
screen -t IRC 1 irssi

```

This will launch irssi in window 1 and title the Screen session 'IRC'.

I then set up a short bash script to launch Screen with that config file:

```
#!/bin/bash
screen -d -m -c ~/irc_screen

```

The command line switches: "-d -m" starts screen in detached mode, so that it launches in the background. "-c ~/irc_screen" uses ~/irc_screen as the rc file for this session.

To launch and connect to the Screen session:

```
~/bin/irc_start
screen -raAd

```

### Doing More

Look into configuring irssi to behave more like you want: [http://www.quadpoint.org/articles/irssi](http://www.quadpoint.org/articles/irssi)

#### Auto-away on screen detach

Using the screen-away script, you can have yourself marked "away" on BitLBee when you disconnect your screen session. By default the script affects all servers but can easily be modified to only affect BitLBee.

Read more about scripts at the URL in 'Doing More'. Find the screen-away.pl script at [http://scripts.irssi.org/](http://scripts.irssi.org/)

##### Modifying screen-away.pl for BitLBee

First you need the server tag for BitLBee. You can get this by typing "/server" in irssi. The tag is the first word on the line. For me, the tag is "BitLBee". On the line following

```
foreach $server (Irssi::servers()) {

```

(which occurs twice) insert the line

```
next unless ( $server->{chatnet} eq 'TAG' );

```

replacing TAG as necessary. In the current version, those occur on lines 181 and 206. To use the script you need to load it - unless if if autoloaded, and set it active.

```
/script load screen_away
/set screen_away_active on

```

#### Persisting the chat client through suspends and connectivity changes

If you use a laptop, you likely suspend and change wireless networks often, which causes your ssh client to lose connection. This can be annoying for a chat client you expect to always be available.

To fix this, try [Mosh](/index.php/Secure_Shell#Mosh "Secure Shell"), which is a shell that seamlessly deals with reconnection after resuming or changing wireless networks.