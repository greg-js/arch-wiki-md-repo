Related articles

*   [IRC channels](/index.php/IRC_channels "IRC channels")
*   [IRC](/index.php/IRC "IRC")
*   [irssi](/index.php/Irssi "Irssi")
*   [HexChat](/index.php/HexChat "HexChat")
*   [Quassel](/index.php/Quassel "Quassel")

[WeeChat](https://weechat.org/) is a highly extendable and feature rich [IRC](https://en.wikipedia.org/wiki/Internet_Relay_Chat "wikipedia:Internet Relay Chat") client.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Installation](#Installation)
*   [2 Usage](#Usage)
*   [3 Configuration](#Configuration)
*   [4 Connecting to a server](#Connecting_to_a_server)
*   [5 Creating a Server profile](#Creating_a_Server_profile)
*   [6 Configuring SSL](#Configuring_SSL)
*   [7 Tips and Tricks](#Tips_and_Tricks)
    *   [7.1 Upgrading](#Upgrading)
    *   [7.2 Aliases](#Aliases)
    *   [7.3 Exec command](#Exec_command)
    *   [7.4 Key Bindings](#Key_Bindings)
    *   [7.5 SSH connection lost when idle](#SSH_connection_lost_when_idle)
    *   [7.6 Slack](#Slack)
        *   [7.6.1 IRC gateway](#IRC_gateway)
            *   [7.6.1.1 Upload file](#Upload_file)
        *   [7.6.2 Native client](#Native_client)
    *   [7.7 Desktop notifications](#Desktop_notifications)
    *   [7.8 Mobile device notifications](#Mobile_device_notifications)
    *   [7.9 WeeChat Relay with a Systemd User Service](#WeeChat_Relay_with_a_Systemd_User_Service)
        *   [7.9.1 Tmux Method](#Tmux_Method)
        *   [7.9.2 Headless Method](#Headless_Method)
*   [8 Troubleshooting](#Troubleshooting)
    *   [8.1 Errors loading plugins](#Errors_loading_plugins)
*   [9 Getting Help](#Getting_Help)
*   [10 See also](#See_also)
    *   [10.1 Guides](#Guides)

## Installation

[Install](/index.php/Install "Install") the [weechat](https://www.archlinux.org/packages/?name=weechat) package, or [weechat-git](https://aur.archlinux.org/packages/weechat-git/) for the development version.

## Usage

WeeChat provides two executables:

*   `weechat`, the curses interface, see [weechat(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/weechat.1)
*   `weechat-headless`, the headless version, see [weechat-headless(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/weechat-headless.1)

Read the [quick start guide](https://weechat.org/files/doc/stable/weechat_quickstart.en.html). For details consult the [user's guide](https://weechat.org/files/doc/stable/weechat_user.en.html).

## Configuration

By default WeeChat stores its configuration files in `~/.weechat`. Editing these files directly is not recommended because WeeChat may write them at any time.[[1]](https://www.weechat.org/files/doc/stable/weechat_user.en.html#files_and_directories)

Instead you should use the [/set command](https://weechat.org/files/doc/devel/weechat_user.en.html#command_weechat_set). You can get a list of all configurable options by running `/set` in the WeeChat buffer window. Since there are nearly 600 default configurable options, you can search through them with a wildcard syntax: `/set irc.server.*` or `/set *server*` as an example. You can get help on each option with the `/help` command:

```
/help irc.server.freenode.autoconnect

```

**Tip:** In case you want to move `~/.weechat` directory somewhere else (like in your `$XDG_CONFIG_HOME`), use this option: `$weechat -d $XDG_CONFIG_HOME/weechat` or set the environment variable `WEECHAT_HOME`.

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

See `/help key`.

### SSH connection lost when idle

If you're connecting to your WeeChat through a remote shell using SSH, for example running it in [GNU Screen](/index.php/GNU_Screen "GNU Screen") or [tmux](/index.php/Tmux "Tmux") you might experience getting disconnected after a while when idle. There are multiple factors in play why this might happen, but the easiest way to change this is to force the connection to be kept alive by appending this to your SSH-configuration on the remote shell.

This has nothing to do with WeeChat itself, but losing connection when idle won't happen with it's alternative [irssi](/index.php/Irssi "Irssi") by default, and thus is a common situation for those converting to WeeChat.

 `# /etc/ssh/sshd_config`  `ClientAliveInterval 300` 

Or have a look at [Mosh](https://mosh.org).

### Slack

**Warning:** [Slack will end support for IRC gateways on 2018-05-15.](https://get.slack.help/hc/en-us/articles/201727913-Connect-to-Slack-over-IRC-and-XMPP)

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

### Desktop notifications

To receive desktop notifications for mentions or private messages, the [weechat-notify-send](https://github.com/s3rvac/weechat-notify-send) script by Petr Zemek can be used.

To install, use:

```
cd ~/.weechat/python
curl -O https://raw.githubusercontent.com/s3rvac/weechat-notify-send/master/notify_send.py
ln -s ../notify_send.py autoload/

```

The script uses [libnotify](https://www.archlinux.org/packages/?name=libnotify) and is known to work with both KDE and Gnome.

Another alternative with the built-in `trigger` plugin is to set a value for `trigger.trigger.beep.command`.

```
 /set trigger.trigger.beep.command "/print -beep;/exec -bg notify-send -i '/usr/share/icons/hicolor/32x32/apps/weechat.png' 'IRC Notification' "${tg_tag_nick}: ${tg_message_nocolor}""

```

### Mobile device notifications

To receive notifications for mentions or private messages to an Android mobile device, you can use the [IrssiNotifier](https://irssinotifier.appspot.com/) port to WeeChat from [here](https://www.weechat.org/files/scripts/irssinotifier.py). This script requires a Google Account, and a registration step with the service provider to obtain an API key. Then, install the plugin

```
cd ~/.weechat/python
curl -O https://www.weechat.org/files/scripts/irssinotifier.py
ln -s ../irssinotifier.py autoload/

```

and intialize the API token and end-to-end encryption password in WeeChat

```
/set plugins.var.python.irssinotifier.api_token your-api-token-from-website
/set plugins.var.python.irssinotifier.encryption_password your-password-same-as-in-andoid-app
/save

```

An alternative that does not require a Google Account is a Ruby script for [NotifyMyAndroid.com](https://www.notifymyandroid.com) from [here](https://github.com/jamtur01/nma-weechat), with a similar installation procedure to the above, but into `~/.weechat/ruby`.

### WeeChat Relay with a Systemd User Service

To use your WeeChat instance as a WeeChat relay for other WeeChat clients (not to be confused with the IRC relay feature) you can use the WeeChat relay plugin and either a [systemd user service](/index.php/Systemd/User "Systemd/User"), if you only want headless operation, or a combination of a systemd user service and [tmux](/index.php/Tmux "Tmux") to maintain full command line functionality.

Either method involves creating a service file in the directory `~/.config/systemd/user/`

#### Tmux Method

Due to the incompatibilities between how systemd manages jobs and the client-server behavior of tmux you will want to use the -L option to separate your default tmux sessions from the WeeChat one being managed by systemd. If this is the first tmux session started using the default socket then stopping and restarting the WeeChat user service will kill all the sessions connected to the default tmux socket. If the WeeChat tmux session is started after another default tmux session then the WeeChat session will die once systemd moves onto the next service unit. Sequestering the WeeChat tmux server to its own socket forces the expected behaviors when invoking systemctl start, stop, and restart. This does however mean that you will not see the WeeChat session when using tmux without using -L to select the correct socket.

 `~/.config/systemd/user/weechat.service` 
```
[Unit]
Description=A WeeChat client and relay service using Tmux
After=network.target

[Service]
Type=forking
RemainAfterExit=yes
ExecStart=/usr/bin/tmux -L weechat new -d -s weechat weechat
ExecStop=/usr/bin/tmux -L weechat kill-session -t weechat

[Install]
WantedBy=default.target
```

Once the service is in place all you need to do is enable it with `systemctl --user enable weechat`

From there you can start the service and connect to the tmux session in order to configure the weechat relay plugin.

```
systemctl --user start weechat
tmux -L weechat attach

```

From there you can configure the WeeChat relay plugin with the desired settings on the console: [https://www.weechat.org/files/doc/stable/weechat_user.en.html#relay_plugin](https://www.weechat.org/files/doc/stable/weechat_user.en.html#relay_plugin)

#### Headless Method

A key difference with this method is that you will either need to start WeeChat normally, configure the relay plugin, stop WeeChat, and then start the service or edit your relay.conf file manually while WeeChat is not running and then start your service. Either way you will need to configure your relay settings before starting your systemd WeeChat service: [https://www.weechat.org/files/doc/stable/weechat_user.en.html#relay_plugin](https://www.weechat.org/files/doc/stable/weechat_user.en.html#relay_plugin)

 `~/.config/systemd/user/weechat-headless.service` 
```
[Unit]
Description=A headless WeeChat client and relay service 
After=network.target

[Service]
Type=forking
ExecStart=/usr/bin/weechat-headless --daemon

[Install]
WantedBy=default.target
```

Note that we do not need an ExecStop defined because systemd will automatically track the PID and send the appropriate shutdown signal to the daemon.

Once the service is in place all you need to do is enable it with `systemctl --user enable weechat-headless`

When you are ready to start your headless relay use `systemctl --user start weechat-headless`

## Troubleshooting

### Errors loading plugins

You may see output like the following in the main window after starting **weechat**:

```
13:26:10 =!= | Error: unable to load plugin "/usr/lib/weechat/plugins/ruby.so": libruby.so.2.4: cannot open shared object file: No such file or directory
13:26:10 =!= | If you're trying to load a script and not a C plugin, try command to load scripts (/perl, /python, ...)
13:26:10 =!= | Error: unable to load plugin "/usr/lib/weechat/plugins/lua.so": liblua.so.5.3: cannot open shared object file: No such file or directory
13:26:10 =!= | If you're trying to load a script and not a C plugin, try command to load scripts (/perl, /python, ...)
13:26:10 =!= | Error: unable to load plugin "/usr/lib/weechat/plugins/aspell.so": libaspell.so.15: cannot open shared object file: No such file or directory
13:26:10 =!= | If you're trying to load a script and not a C plugin, try command to load scripts (/perl, /python, ...)
13:26:10 =!= | Error: unable to load plugin "/usr/lib/weechat/plugins/tcl.so": libtcl8.6.so: cannot open shared object file: No such file or directory
13:26:10 =!= | If you're trying to load a script and not a C plugin, try command to load scripts (/perl, /python, ...)
```

The default configuration for weechat attempts to load all plugins found in /usr/lib/weechat/plugins which in this case includes ruby, lua, aspell and tcl. These packages are not required by the weechat package and may not be installed on your machine. There are two options if these errors bother you:

1.  [Install](/index.php/Install "Install") [ruby](https://www.archlinux.org/packages/?name=ruby), [lua](https://www.archlinux.org/packages/?name=lua), [aspell](https://www.archlinux.org/packages/?name=aspell) and/or [tcl](https://www.archlinux.org/packages/?name=tcl) from the [official repositories](/index.php/Official_repositories "Official repositories").
2.  Or, run `/set weechat.plugin.autoload "*,!ruby,!lua,!aspell,!tcl"` which will prevent loading those plugins with a bang (!) prefix.

## Getting Help

To access WeeChat's built-in help, simply type

```
/help

```

and the help will be displayed in the main buffer (usually buffer 1).

## See also

*   [Home Page](https://www.weechat.org)
*   [WeeChat Documentation](https://www.weechat.org/doc/)
*   [WeeChat Scripts](https://www.weechat.org/scripts/)
*   [WeeChat Development Blog](https://weechat.org/blog/)

### Guides

*   [Official WeeChat quick start guide](https://weechat.org/files/doc/stable/weechat_quickstart.en.html) - a good place to start
*   [FiXato's guide to WeeChat](https://guides.fixato.org/weechat) - A Weechat Contributers Guide
*   [My always up-to-date WeeChat configuration](https://gist.github.com/pascalpoitras/8406501) - r3m (weechat-dev)