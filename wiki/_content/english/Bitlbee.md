[Bitlbee](https://www.bitlbee.org/main.php/news.r.html) is a "console-based IRC to IM chatting gateway, including ICQ/MSN/Jabber". It allows the user to interact with popular chat networks XMPP/Jabber, MSN Messenger, Yahoo! Messenger, AIM and ICQ, the Twitter microblogging network (plus all other Twitter API compatible services like identi.ca and status.net), and social networking chat networks like Facebook and StudiVZ within their IRC client.

The users' buddies appear as normal IRC users in a channel and conversations use the private message facility of IRC.

## Contents

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
    *   [2.1 Daemon](#Daemon)
*   [3 Basic Usage (Jabber/XMPP)](#Basic_Usage_.28Jabber.2FXMPP.29)
    *   [3.1 OTR](#OTR)
*   [4 External Services](#External_Services)
    *   [4.1 Telegram](#Telegram)
    *   [4.2 Twitter](#Twitter)
*   [5 See Also](#See_Also)

## Installation

[Install](/index.php/Install "Install") the [bitlbee](https://www.archlinux.org/packages/?name=bitlbee) package. Alternatively, install the development version, [bitlbee-git](https://aur.archlinux.org/packages/bitlbee-git/).

## Configuration

Various settings can be set using the `/etc/bitlbee/bitlbee.conf` configuration file.

### Daemon

It is recommended to run the Bitlbee daemon without root permission. Uncomment the following line so Bitlbee can run as the "bitlbee" user, which was created when the package was installed.

```
User = bitlbee

```

For daemon mode uncomment the following lines.

```
DaemonInterface = 0.0.0.0
DaemonPort = 6667

```

Ensure that the configuration directory is writeable with the user you configured:

 `# chown -R bitlbee:bitlbee /var/lib/bitlbee` 

Then [start](/index.php/Start "Start") the `bitlbee` daemon. You can also [enable](/index.php/Enable "Enable") the `bitlbee` daemon to start on boot.

Note that just starting the server does not log you into any of your chat accounts.

## Basic Usage (Jabber/XMPP)

Once Bitlbee is running connect to `localhost` using an IRC client. The control channel, `&bitlbee`, should already show you some basic information (if not, join it now). You can always type `help` to get help.

While in the control channel, enter

```
help quickstart

```

and follow the instructions

Your friend might be requesting authorization to add you back, so just reply according to the control channel prompts.

To initiate a chat, simply open a new IRC private window:

```
/msg friend hello!

```

### OTR

For OTR support you must have [libotr](https://www.archlinux.org/packages/?name=libotr) installed. Upon account registration, bitlbee will generate your OTR keys, and it will use them transparently whenever you are negotiating with an OTR-capable contact.

## External Services

### Telegram

To make Telegram work with bitlbee you need version compiled with libpurple support enabled - [bitlbee-libpurple](https://aur.archlinux.org/packages/bitlbee-libpurple/) for example, although there are patched or development versions also available.

Next, install [telegram-purple](https://aur.archlinux.org/packages/telegram-purple/) and restart bitlbee via systemd.

In the control channel, `&bitlbee`, type the following commands:

```
11:45:03 <@user> account add telegram <phone_number_with_region_prefix> <anything>
11:45:03 <@root> Account successfully added
11:45:06 <@user> account telegram on

```

After connecting a separate chat window will open, asking for the SMS code - enter it and Telegram will work with your setup.

### Twitter

In the control channel, `&bitlbee`, type the following commands:

```
11:45:03 <@user> account add twitter <handle>
11:45:03 <@root> Account successfully added
11:45:06 <@user> account on
11:45:06 <@root> Trying to get all accounts connected...
11:45:06 <@root> twitter - Logging in: Requesting OAuth request token

```

In a private channel, `twitter_handle`, you'll receive:

```
11:45:07 <twitter_handle> To finish OAuth authentication, please visit [http://api.twitter.com/oauth/authorize?oauth_token=xxxxxxxxx](http://api.twitter.com/oauth/authorize?oauth_token=xxxxxxxxx) and respond with the resulting PIN code.

```

Click the link and authorize the BitlBee app on Twitter. You should now see:

```
11:59:54 <@root> twitter - Logging in: Connecting to Twitter
11:59:55 <@root> twitter - Logging in: Logged in

```

## See Also

*   [Screen Irssi Bitlbee](/index.php/Screen_Irssi_Bitlbee "Screen Irssi Bitlbee")
*   [Bitlbee Wiki](http://wiki.bitlbee.org/)
*   [Introduction to Bitlbee](http://quark.humbug.org.au/publications/internet/bitlbee.pdf) by Bradley Marshall
*   [Quickstart Guide](http://princessleia.com/bitlbee.php) by Elizabeth Krumbach
*   [HOWTO: Connect to Twitter](http://wiki.bitlbee.org/HowtoTwitter) on the BitlBee wiki
*   [HOWTO: Connect to Facebook](https://wiki.bitlbee.org/HowtoFacebookMQTT) on the Bitlbee Wiki