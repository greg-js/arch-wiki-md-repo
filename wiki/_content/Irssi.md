# Irssi

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

Related articles

*   [IRC channels](/index.php/IRC_channels "IRC channels")
*   [IRC](/index.php/IRC "IRC")
*   [WeeChat](/index.php/WeeChat "WeeChat")
*   [HexChat](/index.php/HexChat "HexChat")

[irssi](http://www.irssi.org/) is a modular, ncurses based IRC (Internet Relay Chat) client. It also supports [SILC](https://en.wikipedia.org/wiki/SILC_(protocol) "wikipedia:SILC (protocol)") and [ICB](http://www.icb.net/_jrudd/icb/protocol.html) protocols via plugins.

## Contents

*   [1 Installation](#Installation)
*   [2 Usage](#Usage)
    *   [2.1 Commands](#Commands)
*   [3 Configuration](#Configuration)
    *   [3.1 Authenticating with SASL](#Authenticating_with_SASL)
    *   [3.2 Automatically connect to #archlinux on startup](#Automatically_connect_to_.23archlinux_on_startup)
    *   [3.3 SSL Connection](#SSL_Connection)
        *   [3.3.1 Client certificates](#Client_certificates)
    *   [3.4 Automatic logging](#Automatic_logging)
    *   [3.5 Hide joins, parts, and quits](#Hide_joins.2C_parts.2C_and_quits)
*   [4 Tips and tricks](#Tips_and_tricks)
    *   [4.1 HTTP Proxy](#HTTP_Proxy)
    *   [4.2 irssi with nicklist in tmux](#irssi_with_nicklist_in_tmux)
    *   [4.3 Virtual hostname (vhost)](#Virtual_hostname_.28vhost.29)
        *   [4.3.1 Required preconfigurations](#Required_preconfigurations)
        *   [4.3.2 Enabling the vhost](#Enabling_the_vhost)
*   [5 See also](#See_also)

## Installation

[Install](/index.php/Pacman "Pacman") the [irssi](https://www.archlinux.org/packages/?name=irssi) package.

Several scripts are available in the AUR under [**irssi-script**](https://aur.archlinux.org/packages/?O=0&K=irssi-script), and in the [irssi script repository](http://scripts.irssi.org/).

## Usage

For a detailed introduction see the [official documentation](http://irssi.org/documentation).

**Note:** This section assumes you already know the basics of [IRC](https://en.wikipedia.org/wiki/Internet_Relay_Chat "wikipedia:Internet Relay Chat") and have used other clients in the past

A terminal multiplexer such as [tmux](/index.php/Tmux "Tmux") or [Screen](/index.php/Screen "Screen") is recommended. It allows the user to easily disconnect and reconnect to a session, and scripts such as [nicklist.pl](http://wouter.coekaerts.be/site/irssi/nicklist) depend on a secondary window. To start irssi, run:

```
$ irssi

```

### Commands

<table class="wikitable">

<tbody>

<tr>

<th style="font-weight: bold;">Command</th>

<th style="font-weight: bold;">Description</th>

</tr>

<tr>

<td>`/server`, `/s`</td>

<td>Change the server of the current network.</td>

</tr>

<tr>

<td>`/connect`, `/c`</td>

<td>Open a new connection to a server. This is used to connect to multiple servers simultaneously (`Ctrl+Shift+x` switches between multiple servers).</td>

</tr>

<tr>

<td>`/disconnect`, `/dc`</td>

<td>Closes the current connection to a server.</td>

</tr>

<tr>

<td>`ALT+(1-0,q-p,etc)`</td>

<td>Changes the currently active window. `Ctrl+n` cycles to the next window, `Ctrl+p` to the previous window.</td>

</tr>

<tr>

<td>`/window 1`</td>

<td>Go to the first window. Windows are ordered by the first two rows on the keyboard: (1-0), (q-p).</td>

</tr>

<tr>

<td>`/window close`, `/wc`</td>

<td>Close the current window.</td>

</tr>

<tr>

<td>`/window move 1`</td>

<td>Move the current window to the first window position.</td>

</tr>

<tr>

<td>`/layout save`</td>

<td>Save the current window positions for later use.</td>

</tr>

<tr>

<td>`/set`</td>

<td>Show a list of current settings.</td>

</tr>

<tr>

<td>`/help`</td>

<td>Describe a provided parameter.</td>

</tr>

<tr>

<td>`/alias`</td>

<td>Create a shortcut.</td>

</tr>

</tbody>

</table>

## Configuration

Personal configuration file should be located at `~/.irssi/config`; there is a template available in `/etc/irssi.conf`. You can start irssi with an alternate config file using the `--config` flag.

*   You can use `/save` to save your current configuration to the config file.
*   You can save the location of your currently opened windows by entering `/layout save`

### Authenticating with SASL

[Install](/index.php/Install "Install") the [irssi-script-sasl](https://aur.archlinux.org/packages/irssi-script-sasl/)<sup><small>AUR</small></sup> package. Load the script with each start of irssi:

```
$ mkdir -p ~/.irssi/scripts/autorun
$ cd ~/.irssi/scripts/autorun
$ ln -s /usr/share/irssi/scripts/cap_sasl.pl cap_sasl.pl

```

Then open irssi and run the SASL script and enter your SASL settings. Please use your main nick "your-primary-nick" and "your-password" which is registered with nickserv. See [here](https://freenode.net/sasl/sasl-irssi.shtml) for available authentication mechanisms (Note that DH-BLOWFISH is no longer supported):

```
/script load autorun/cap_sasl.pl
/sasl set Freenode _primary-nick_ _password_ _auth_
/sasl save
/save

```

**Note:**

*   Make sure to use the correct capitalization for the network name.
*   Your password will be visible when you type it and can also be seen in `~/.irssi/sasl.auth`
*   If your password contains `$`, you have to prefix it with another `$` for _irssi_ to properly parse it.

Restart irssi and look for "Irssi: SASL authentication successful".

### Automatically connect to #archlinux on startup

Start irssi and then type the following in it:

```
/server add -auto -network freenode chat.freenode.net

```

`freenode` can be substituted for any preferred word, such as the common abbreviation `fn`.

Ensure [SASL](#Authenticating_with_SASL) is configured correctly. You may use NickServ manually with `-autosendcmd` instead of SASL, but this causes a race condition when automatically joining channels. If desired, authenticate using SSL certificates, instead of passwords with NickServ.

```
/channel add -auto #archlinux freenode
/channel add -auto #archlinux-offtopic freenode

```

### SSL Connection

Freenode uses port 6697, 7000 and 7070 for SSL connections (**not** 6667). To connect to Freenode IRC network via SSL you have to setup an new connection. Start `irssi` and run:

```
/server add -auto -ssl -ssl_verify -ssl_capath /etc/ssl/certs -network freenode -port 6697 chat.freenode.net

```

Save your new settings with:

```
/save

```

If everything works you will see the "Z" mode set. It should look like this: "Mode change (+Zi) for user your-nick"

#### Client certificates

Freenode and OFTC support authentication using SSL certificates, providing an alternative to plaintext passwords. See Freenode's [Identifying with CERTFP](https://freenode.net/certfp/) and [Creating an SSL Certificate](https://freenode.net/certfp/makecert.shtml) for more extensive details.

To create an password-less certificate that is valid for 730 days (when requested to enter details like state or even Common Name (CN), you can fill anything you want):

```
$ openssl req -newkey rsa:2048 -days 730 -x509 -keyout irssi.key -out irssi.crt -nodes 
$ cat irssi.crt irssi.key > ~/.irssi/irssi.pem
$ chmod 600 ~/.irssi/irssi.pem
$ rm irssi.crt irssi.key

```

Next, find out the corresponding fingerprint:

```
$ openssl x509 -sha1 -fingerprint -noout -in ~/.irssi/irssi.pem | sed -e 's/^.*=//;s/://g;y/ABCDEF/abcdef/'

```

This will write the fingerprint to stdout. (The sed command is there to format the fingerprint correctly by removing unwanted text and characters.) Copy the fingerprint string as you will register it in irssi shortly.

In irssi, disconnect from the network and add the client certificate and keys. Omit the -ssl_pass option if your certificate was built without a password:

```
/disconnect Freenode
/server add -ssl_cert ~/.irssi/irssi.pem  -ssl_pass <irssi.pem_password> -network freenode chat.freenode.net 6697

```

Now connect (not `/reconnect`) and register your fingerprint

```
/connect Freenode
/msg NickServ identify YOUR_PASSWORD
/msg NickServ cert add YOUR_FINGERPRINT

```

At this point, you can remove your password from the configuration file (if you saved it in there) and save your config with:

```
/save

```

### Automatic logging

```
/SET autolog ON
/save

```

### Hide joins, parts, and quits

In order to ignore showing of joining, leaving and quiting of users for all channels type the following in irssi:

```
/ignore * joins
/ignore * parts
/ignore * quits

```

See [smartfilter](https://github.com/lifeforms/irssi-smartfilter) to restrict join messages to active users.

## Tips and tricks

### HTTP Proxy

To use _irssi_ behind a HTTP proxy, the following commands are required:

```
/SET use_proxy ON
/SET proxy_address <Proxy host address>
/SET proxy_port <Proxy port>
/SET -clear proxy_string
/SET proxy_string_after conn %s %d
/EVAL SET proxy_string CONNECT %s:%d HTTP/1.0\n\n

```

_irssi_ should then alter its config file correspondingly; if the proxy is not required, just set use_proxy to OFF.

Should the proxy require a password, try:

```
/SET proxy_password your_pass

```

Otherwise:

```
/SET -clear proxy_password

```

**Note:** SSL behind a proxy will fail with these settings.

### irssi with nicklist in tmux

The _irssi_ plugin '[nicklist](http://scripts.irssi.org/scripts/nicklist.pl)' offers to add a pane listing the users on the channel currently viewed. It has two methods to do this:

*   **screen**, which simply adds the list to the right of _irssi_, but brings the disadvantage that the entire window gets redrawn every time _irssi_ prints a line.

*   **fifo**, which like the name suggests writes the list into a fifo that can then be continuously read with e. g. _cat ~/.irssi/nicklistfifo_.

nicklist will use the more efficient _fifo_ with:

```
/NICKLIST FIFO

```

This fifo can be used in a [tmux](/index.php/Tmux "Tmux") window split vertically with _irssi_ in its left pane and the _cat_ from above in a small one in its right. Since the pane is dependent on its creating tmux session's geometry, a subsequent session with a different one needs to recreate it (which also implies a switch in _irssi_ windows to refill the fifo).

E. g., the following script first checks for a running _irssi_, presumed to have been run by a previous execution of itself. Unless found it creates a new tmux session, a window named after and running _irssi_ and then the pane with _cat_. If however _irssi_ was found it merely attaches to the session and recreates the _cat_ pane.

```
#!/bin/bash

T3=$(pgrep -u $USER -x irssi)

irssi_nickpane() {
    tmux setw main-pane-width $(( $(tput cols) - 21));
    tmux splitw -v "cat ~/.irssi/nicklistfifo";
    tmux selectl main-vertical;
    tmux selectw -t irssi;
    tmux selectp -t 0;
}

irssi_repair() {
    tmux selectw -t irssi
    (( $(tmux lsp | wc -l) > 1 )) && tmux killp -a -t 0
    irssi_nickpane
}

if [ -z "$T3" ]; then
    tmux new-session -d -s main;
    tmux new-window -t main -n irssi irssi;
    irssi_nickpane ;
fi
    tmux attach-session -d -t main;
    irssi_repair ;
exit 0

```

**Tip:** Instead of doing all this work, [this plugin](http://anti.teamidiot.de/static/nei/*/Code/Irssi/tmux-nicklist-portable.pl) does all the work needed for a nice nicklist inside tmux.

### Virtual hostname (vhost)

A vhost can be used to change your hostname when connected to an IRC-server, commonly viewed when joining/parting or doing a whois. This is most commonly done on a server which have a static IP address. Without a vhost it would commonly look like so when doing a 'whois':

```
nick@123.456.78.90.isp.com

```

The result of a successfull vhost could be like so if you have the domain example.com available:

```
nick@example.com

```

Keep in mind that not every IRC-server supports the use of vhost. This might be individually set between the servers and not the network, so if you are experiencing issues with one server try another on the same network.

#### Required preconfigurations

irssi supports using a vhost as long as the required configurations has been set. This includes especially that your host supports [Recursive DNS Lookup (rDNS)](https://en.wikipedia.org/wiki/Reverse_DNS_lookup "wikipedia:Reverse DNS lookup") using [Pointer record (PTR)](https://en.wikipedia.org/wiki/List_of_DNS_record_types "wikipedia:List of DNS record types"). Additionally you should add an appropriate line to your `/etc/hosts` file.

To see if this is working, test with the 'host' DNS lookup utility included in [bind-tools](https://www.archlinux.org/packages/?name=bind-tools) like so (where _ip_ is a normal IPv4 address):

```
host _ip_

```

If this returns something in the lines of this then you know that your rDNS is working.

```
_ip_.in-addr.arpa domain name pointer example.com

```

#### Enabling the vhost

There are a couple of ways to connect to a server with a given hostname. One is using the 'server' command with a -host argument like so:

```
/server -host example.com irc.freenode.org

```

Another way would be to set your hostname (vhost) with the 'set' command which will save your hostname to `~/.irssi/config`:

```
/set hostname example.com
/save
/server irc.freenode.org

```

## See also

*   [Official website](http://www.irssi.org/)
*   [Setting up Irssi](http://linuxtidbits.wordpress.com/2008/01/09/setting-up-irssi/)
*   [Guide to efficiently using Irssi and screen](http://quadpoint.org/articles/irssi) by Matt Sparks
*   [Official List of Irssi scripts](http://scripts.irssi.org/)
*   [IRC notifications with dzen2](http://jasonwryan.com/blog/2011/11/07/irc-dzen/) by Jason Ryan
*   [Irssi’s /channel, /network, /server and /connect – What it means](http://pthree.org/2010/02/02/irssis-channel-network-server-and-connect-what-it-means/) by Aaron Toponce
*   [awesome Wiki Irssi tips](http://awesome.naquadah.org/wiki/Irssi_tips)
*   [irssi systemd unit](https://github.com/GutenYe/systemd-units/tree/master/irssi)

Retrieved from "[https://wiki.archlinux.org/index.php?title=Irssi&oldid=407555](https://wiki.archlinux.org/index.php?title=Irssi&oldid=407555)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [Internet Relay Chat](/index.php/Category:Internet_Relay_Chat "Category:Internet Relay Chat")