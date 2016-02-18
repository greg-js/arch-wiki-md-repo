[Hamachi](https://en.wikipedia.org/wiki/Hamachi_(software) is a proprietary (closed source) commercial VPN software. With Hamachi you can organize two or more computers with an Internet connection into their own virtual network for direct secure communication.

## Contents

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
    *   [2.1 Hamachi 2 (beta)](#Hamachi_2_.28beta.29)
        *   [2.1.1 Using the hamachi command line tool as a regular user](#Using_the_hamachi_command_line_tool_as_a_regular_user)
        *   [2.1.2 Automatically setting a custom nickname](#Automatically_setting_a_custom_nickname)
*   [3 Running Hamachi](#Running_Hamachi)
    *   [3.1 Systemd](#Systemd)
*   [4 GUI](#GUI)
*   [5 See also](#See_also)

## Installation

[Install](/index.php/Install "Install") the [logmein-hamachi](https://aur.archlinux.org/packages/logmein-hamachi/) package.

## Configuration

### Hamachi 2 (beta)

Hamachi 2 is configured in `/var/lib/logmein-hamachi/h2-engine-override.cfg` (create that file if it doesn't exist). Unfortunately, it isn't easy to find a comprehensive list of possible configuration options, so here are a few that you can use.

#### Using the hamachi command line tool as a regular user

In order to use the `hamachi` command line tool as a regular user, add the following line to the configuration file:

```
Ipc.User YourUserNameHere

```

#### Automatically setting a custom nickname

Normally, Hamachi uses your system's hostname as the nickname that other Hamachi users will see. If you want to automatically set a custom nickname every time Hamachi starts, add the following line to the configuration file:

```
Setup.AutoNick YourNicknameHere

```

You can also manually set a nickname using the `hamachi` command line tool:

```
# hamachi set-nick YourNicknameHere

```

However, this needs to be done every time Hamachi is (re-)started, so if you always want to use the same nickname, setting it automatically (as explained above) is probably easier.

## Running Hamachi

[Start](/index.php/Start "Start") `logmein-hamachi.service`.

Now you have a whole bunch of commands at your disposal. These are in no particular order and are fairly self explanatory.

```
$ hamachi set-nick bob
$ hamachi login
$ hamachi create my-net secretpassword
$ hamachi go-online my-net
$ hamachi list
$ hamachi go-offline my-net

```

To get a list of all the commands, run: $ hamachi ?

**Note:** Make sure you change the status of the channel(s) you are in to "online" if you want to perform any network actions on computers in there.

### Systemd

The [logmein-hamachi](https://aur.archlinux.org/packages/logmein-hamachi/) package also includes a nice little [Systemd](/index.php/Systemd "Systemd") daemon.

If you feel like it, you can set Hamachi to start at every boot with Systemd by [enabling](/index.php/Enabling "Enabling") `logmein-hamachi.service`.

## GUI

The following GUI frontends for Hamachi are available in the AUR:

*   [haguichi](https://aur.archlinux.org/packages/haguichi/) (Gtk3, Vala)
*   [quamachi](https://aur.archlinux.org/packages/quamachi/) (Qt4, Python)

## See also

*   [Project home page](https://secure.logmein.com/products/hamachi/)