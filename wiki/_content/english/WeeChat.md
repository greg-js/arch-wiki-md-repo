**WeeChat** is a highly extendable and feature rich [IRC](https://en.wikipedia.org/wiki/Internet_Relay_Chat "wikipedia:Internet Relay Chat") Client currently under heavy development.

## Contents

*   [1 Installing](#Installing)
*   [2 Running WeeChat](#Running_WeeChat)
*   [3 Configuration](#Configuration)
    *   [3.1 Internal commands](#Internal_commands)
    *   [3.2 Internal menu-based](#Internal_menu-based)
    *   [3.3 Configuration Files](#Configuration_Files)
*   [4 Connecting to a server](#Connecting_to_a_server)
*   [5 Creating a Server profile](#Creating_a_Server_profile)
*   [6 Configuring SSL](#Configuring_SSL)
*   [7 Tips and Tricks](#Tips_and_Tricks)
    *   [7.1 Upgrading](#Upgrading)
    *   [7.2 Aliases](#Aliases)
    *   [7.3 Exec command](#Exec_command)
    *   [7.4 Key Bindings](#Key_Bindings)
    *   [7.5 SSH connection lost when idle](#SSH_connection_lost_when_idle)
    *   [7.6 OTR](#OTR)
    *   [7.7 Slack](#Slack)
        *   [7.7.1 IRC gateway](#IRC_gateway)
            *   [7.7.1.1 Upload file](#Upload_file)
        *   [7.7.2 Native client](#Native_client)
            *   [7.7.2.1 Upload file](#Upload_file_2)
    *   [7.8 Desktop notifications](#Desktop_notifications)
    *   [7.9 Mobile device notifications](#Mobile_device_notifications)
*   [8 Troubleshooting](#Troubleshooting)
    *   [8.1 Errors loading plugins](#Errors_loading_plugins)
*   [9 Getting Help](#Getting_Help)
*   [10 See also](#See_also)
    *   [10.1 Guides](#Guides)

## Installing

[Install](/index.php/Install "Install") the [weechat](https://www.archlinux.org/packages/?name=weechat) package, or [weechat-git](https://aur.archlinux.org/packages/weechat-git/) for the development version.

## Running WeeChat

WeeChat is going to have multiple interfaces at some point, run **weechat-[interface]** to start WeeChat.

As WeeChat currently only has an Ncurses interface. The command to start WeeChat is:

```
$ weechat

```

## Configuration

You can configure WeeChat in 3 ways: using WeeChat's internal commands; using **iset**; or by editing the .conf files directly. WeeChat will automatically save settings on exit or when you run `/save`, so if you are editing a .conf file in an editor, be sure to run `/reload` from the console before exiting, otherwise your changes will be lost.

### Internal commands

The `/set` command follows this structure: `/set [file.name].[section].[directive]`

You can get a list of all configurable options by typing `/set` in the **weechat** buffer window. Since there are nearly 600 default configurable options, you can search through them with a wildcard syntax: `/set irc.server.*` or `/set *server*` as an example. You can get help on each option with the `/help` command:

```
/help irc.server.freenode.autoconnect

```

### Internal menu-based

For a more convenient method, install the **iset** script. If you have weechat 0.3.9 or newer, run:

```
/script install iset.pl

```

In older versions, use `/weeget install iset`, or download [iset.pl](http://www.weechat.org/scripts/source/stable/iset.pl.html/) into your `~/.weechat/perl/autoload` directory manually.

Afterwards, run

```
/iset

```

to get a buffer with all configuration options.

### Configuration Files

The .conf files for WeeChat are saved to `~/.weechat`. These files are not commented. Detailed information can be found within the program itself (see **Internally** above), or WeeChat's [user guide](http://www.weechat.org/files/doc/stable/weechat_user.en.html).

**Tip:** in case you want to move `.weechat` directory somewhere else (like in your **$XDG_CONFIG_HOME**), use this option: `$weechat -d $XDG_CONFIG_HOME/weechat` or set the environment variable `WEECHAT_HOME`.

## Connecting to a server

**Note:** Using **/connect** to connect to a temporary server is disabled by default if you're using 1.1+ [Release Note](https://weechat.org/files/releasenotes/ReleaseNotes-devel.html#_temporary_servers_disabled_by_default_with_connect)

Enable by **/set irc.look.temporary_servers on**

You can connect to a IRC server by using **/connect**.

```
/connect chat.freenode.net

```

Or if there is already a **Server** setup you can use:

```
/connect freenode

```

## Creating a Server profile

If you plan on connecting to a server more than once it may be beneficial to create a **Server**.

```
/server add example irc.example.net/6667

```

Would create the server **example** which would connect to **irc.example.net** on port **6667**

See the WeeChat documentation and **/help server** for more information.

## Configuring SSL

Many IRC servers, including [freenode](https://freenode.net/) where [#archlinux](/index.php/IRC_channel "IRC channel") is, support SSL.

If you're making a server with **/server**, add the SSL port (usually 6697) and **-ssl** to the end of the line. For example:

```
/server add freenode chat.freenode.net/6697 -ssl

```

You can do the same thing if using **/connect**.

```
/connect chat.freenode.net/6697 -ssl

```

**Warning:** Some servers need the **ssl_dhkey_size** value changed to something lower. For example, if you're using freenode you'll need to set **/set irc.server.freenode.ssl_dhkey_size 1024** or **/set irc.server.chat.freenode.net.ssl_dhkey_size 1024** (see the server log)

**Note:** Different servers may have a different port than 6697 - this is server specific.

You may also want to change the location where WeeChat looks for trusted authorities (the default value is `%h/ssl/CAs.pem` which translates to `~/.weechat/ssl/CAs.pem)`:

```
/set weechat.network.gnutls_ca_file "/etc/ssl/certs/ca-certificates.crt"

```

## Tips and Tricks

### Upgrading

WeeChat can be upgraded without disconnecting from the IRC servers (non-SSL connections only):

```
/upgrade

```

This will load the new WeeChat binary and reload the current configuration.

### Aliases

Aliases can be created to simplify commonly executed commands. A nice example is Wraithan's **smart filter** alias:

**Smart Filter**

First, we need to enable smart filters:

```
/set irc.look.smart_filter "on"

```

Next, we will create the **sfilter** alias:

```
/alias add sfilter filter add irc_smart_$server_$channel irc.$server.$channel irc_smart_filter *

```

We can now type

```
/sfilter

```

in any buffer, and the smart filter will only be enabled for that buffer.

The following alias will remove a previously enabled smart filter in the current buffer. Add the alias:

```
/alias add rmsfilter filter del irc_smart_$server_$channel

```

and execute it by

```
/rmsfilter

```

### Exec command

A new plugin called "exec" has been added, with command `/exec`. It will execute external command and can display output to the current buffer with the **-o** option or locally (default).

### Key Bindings

Some helpful bindings:

To use ctrl-left/right arrow keys to jump to next/previous words on the input line:

```
/key bind meta2-1;5D /input move_previous_word
/key bind meta2-1;5C /input move_next_word

```

### SSH connection lost when idle

If you're connecting to your WeeChat through a remote shell using SSH, for example running it in [screen](/index.php/Screen "Screen") or [tmux](/index.php/Tmux "Tmux") you might experience getting disconnected after a while when idle. There are multiple factors in play why this might happen, but the easiest way to change this is to force the connection to be kept alive by appending this to your SSH-configuration on the remote shell.

This has nothing to do with WeeChat itself, but losing connection when idle won't happen with it's alternative [irssi](/index.php/Irssi "Irssi") by default, and thus is a common situation for those converting to WeeChat.

 `# /etc/ssh/sshd_config`  `ClientAliveInterval 300` 

Or have a look at [Mosh](http://mosh.mit.edu/).

### OTR

Install [python2-potr](https://aur.archlinux.org/packages/python2-potr/) and enable the script **otr.py**. Then:

```
/query <nick>
/otr start

```

Get help on the plugin with:

```
/help otr

```

### Slack

[Slack](https://slack.com/) is a platform for team communication; an IRC on steroids. Thanks to its open API, it is possible to connect to your slack team using weechat.

#### IRC gateway

Once weechat is running, all you have to is add a new server this way:

`/server add NAME HOST/6667 -autoconnect -ssl -ssl_dhkey_size=512 -password=PASSWORD -username=USERNAME -nicks=NICK`

where:

*   **NAME** is the name you want to give to the server
*   **HOST** is the the Host as provided on the Gateways page of your slack team
*   **PASSWORD** is the Pass as provided on the Gateways page of your slack team
*   **USERNAME** is the User as provided on the Gateways page of your slack team
*   **NICK** is your Slack username.

##### Upload file

To upload a file, run this following command from your shell :

`curl -F file=@/path/to/file -F channels=CHAN -F token=XXX https://slack.com/api/files.upload`

where:

*   **CHAN** is the channel ID as provided on the Gateways page of your slack team
*   **XXX** is the team token as provided on the Gateways page of your slack team

#### Native client

There is a native client for slack: [wee-slack](https://github.com/rawdigits/wee-slack)

You need to install the python2 librairy websocket-client:

`pacman -S python2-websocket-client`

Then install the wee-chat plugin into the weechat configuration folder

`curl -o ~/.weechat/python/autoload/wee_slack.py https://raw.githubusercontent.com/rawdigits/wee-slack/master/wee_slack.py`

Run `/python reload` to load the new plugin

You will need an access token. You can grab one at [here](https://api.slack.com/docs/oauth-test-tokens)

Once weechat is running, register your token into weechat:

`/set plugins.var.python.slack_extension.slack_api_token [YOUR_SLACK_TOKEN]`

And finally:

`/save`

`/python reload`

##### Upload file

To upload a file enter the following command into weechat:

`/slack upload [file_path]`

### Desktop notifications

To receive desktop notifications for mentions or private messages, the [weechat-notify-send](https://github.com/s3rvac/weechat-notify-send) script by Petr Zemek can be used.

To install, use:

```
cd ~/.weechat/python
curl -O https://raw.githubusercontent.com/s3rvac/weechat-notify-send/master/notify_send.py
ln -s ../notify_send.py autoload/

```

The script uses [libnotify](https://www.archlinux.org/packages/?name=libnotify) and is known to work with both KDE and Gnome.

### Mobile device notifications

To receive notifications for mentions or private messages to an Android mobile device, you can use the [IrssiNotifier](https://irssinotifier.appspot.com/) port to WeeChat from [here](http://www.weechat.org/files/scripts/irssinotifier.py). This script requires a Google Account, and a registration step with the service provider to obtain an API key. Then, install the plugin

```
cd ~/.weechat/python
curl -O http://www.weechat.org/files/scripts/irssinotifier.py
ln -s ../irssinotifier.py autoload/

```

and intialize the API token and end-to-end encryption password in WeeChat

```
/set plugins.var.python.irssinotifier.api_token your-api-token-from-website
/set plugins.var.python.irssinotifier.encryption_password your-password-same-as-in-andoid-app
/save

```

An alternative that does not require a Google Account is a Ruby script for [NotifyMyAndroid.com](http://www.notifymyandroid.com) from [here](https://github.com/jamtur01/nma-weechat), with a similar installation procedure to the above, but into `~/.weechat/ruby`.

## Troubleshooting

### Errors loading plugins

You may see output like the following in the main window after starting **weechat**:

```
12:29:37 =!= | Error: unable to load plugin "/usr/lib/weechat/plugins/**tcl.so**": libtcl8.6.so: cannot open shared object file: No such file or directory
12:29:37 =!= | If you're trying to load a script and not a C plugin, try command to load scripts (/perl, /python, ...)
12:29:37 =!= | Error: unable to load plugin "/usr/lib/weechat/plugins/**ruby.so**": libruby.so.2.0: cannot open shared object file: No such file or directory
12:29:37 =!= | If you're trying to load a script and not a C plugin, try command to load scripts (/perl, /python, ...)
12:29:37     | Plugins loaded: alias, aspell, charset, fifo, guile, irc, logger, lua, perl, python, relay, rmodifier, script, xfer

```

The default configuration for weechat attempts to load all plugins found in /usr/lib/weechat/plugins which in this case includes both tcl and ruby. These packages are not required by the weechat package and may not be installed on your machine. There are two options if these errors bother you:

1.  [Install](/index.php/Packages "Packages") [tcl](https://www.archlinux.org/packages/?name=tcl), [ruby](https://www.archlinux.org/packages/?name=ruby) from the [official repositories](/index.php/Official_repositories "Official repositories").
2.  Or, run `/set weechat.plugin.autoload "*,!tcl,!ruby"` which will prevent loading those plugins with a bang (!) prefix.

## Getting Help

To access WeeChat's built-in help, simply type

```
/help

```

and the help will be displayed in the main buffer (usually buffer 1).

## See also

*   [Home Page](http://www.weechat.org)
*   [WeeChat Documentation](http://www.weechat.org/doc/)
*   [WeeChat Scripts](http://www.weechat.org/scripts/)
*   [WeeChat Development Blog](http://dev.weechat.org/)

### Guides

*   [FiXato's guide to WeeChat](http://fixato.org/guides/setting_up_weechat.html)
*   [Thoughtbot article on weechat and slack](http://robots.thoughtbot.com/weechat-for-slacks-irc-gateway)