[NoMachine](https://www.nomachine.com) enables you to access a graphical desktop of a computer over the network.

Until version 3.x, NoMachine was known as NX and available under GPL. There are derivatives based on core NX libraries like [FreeNX](/index.php/FreeNX "FreeNX") and [X2Go](/index.php/X2Go "X2Go"). The major drawback of these is that they utilise a built-in X server of nxagent, which originates from the year 2005 and some current X applications cannot run due to unsupported features available only in newer versions of X libraries.

Unlike some other remote desktop solutions (e.g. TeamViewer), NoMachine does not require an intermediary server to establish the connection.

Since NoMachine version 4, the software is proprietary and currently two editions are available: [Free and Enterprise](https://www.nomachine.com/AR07L00808). Clients exist for Linux, MS Windows, OS X, Android and iOS.

The free edition allows to connect to an existing X display (also known as display shadowing of a live session with a physical display) or, if no X display is available (e.g. on head-less machines), NoMachine tries to start its own X server with the default [Desktop environment](/index.php/Desktop_environment "Desktop environment") automatically. The major limitation of the free edition is that only a single remote desktop session may run on the server.

## Contents

*   [1 Installation](#Installation)
*   [2 Usage](#Usage)
*   [3 Troubleshooting](#Troubleshooting)
    *   [3.1 Headless server](#Headless_server)
    *   [3.2 Separate NoMachine X session in parallel with existing X session](#Separate_NoMachine_X_session_in_parallel_with_existing_X_session)
    *   [3.3 Problems with default keyboard in Display Manager](#Problems_with_default_keyboard_in_Display_Manager)
    *   [3.4 Connecting via SSH](#Connecting_via_SSH)

## Installation

Install the [nomachine](https://aur.archlinux.org/packages/nomachine/) package.

It includes both server and client tar balls. Note that the setup actually takes place by a post-installation script and therefore the list of files shown by command `pacman -Ql nomachine` is not complete!

In particular, the majority of NoMachine files are kept within `/usr/NX` directory, but a few more are added:

```
/etc/NX
/etc/pam.d/nx
/usr/lib/systemd/system/nxserver.service
/usr/local/share/applications/NoMachine*.desktop
/usr/share/polkit-1/actions/org.freedesktop.pkexec.nomachine.policy

```

The files created by NoMachine Player are stored in:

```
$HOME/.nx
$HOME/Documents/NoMachine

```

The post-install script also creates a new user `nx`.

If you have X2Go or FreeNX installed as well, do not get confused that some files use similar names (i.e. `/usr/bin/nx`).

The `nxserver.service` does not need to be enabled and started on computers, which will be used only as the client, but it must run on the server.

## Usage

On the target computer, [start/enable](/index.php/Start/enable "Start/enable") `nxserver.service` via systemd, or via menu in your desktop: *Internet > NoMachine > NoMachine Service*, which does the same via a GUI and offers extra info and configuration.

On the client, start the "Player" (menu *Internet > NoMachine > NoMachine*. Or start it with

```
/usr/NX/bin/nxplayer

```

It will search the LAN for available NoMachine servers or, if disabled or in a different subnet/WAN, you can type in the target hostname or IP address manually. The login credentials are the same as used for the user on the target computer.

## Troubleshooting

### Headless server

If no X server is running on the server, NoMachine starts its own X server (`DISPLAY :0`) and tries to run a `/etc/X11/Xsession` script to get the user into the default DE. This fails in Arch Linux (you get only a black screen) because an `Xsession` script does not exist.

To resolve this issue, edit the key `DefaultDesktopCommand` in `/usr/NX/etc/node.cfg`. E.g. for MATE desktop environment:

```
DefaultDesktopCommand "/usr/bin/mate-session"

```

### Separate NoMachine X session in parallel with existing X session

In default setup, the Free edition of NoMachine connects the client directly to an existing X session on the remote computer, even if it runs the X Display Manager only. This may be unwanted, because no other user may use the target computer locally at the same moment and because any person with physical access to the target computer can see on the physical display, what the remotely connected user is doing.

However, it is possible to setup NoMachine to check only for a particular DISPLAY, e.g. `DISPLAY :10` and it will ignore the existing X session on `DISPLAY :0` (standard setup in Arch Linux) and start a new virtual session for the remotely connecting user.

To do so, edit the key `PhysicalDisplays` in `/usr/NX/etc/node.cfg`:

```
PhysicalDisplays :10

```

### Problems with default keyboard in Display Manager

When NoMachine connects to display manager on the target computer and the user tries to login as if sitting at the target computer, the user authentication may fail due to a different keymap. A workaround is to type the user's password e.g. in a text editor and copy it via clipboard to the NoMachine session.

Once the user is logged in to the remote desktop environment, running `setxkb cz` ('cz' stands for the Czech keyboard as an example) should resolve the problem with key mappings.

### Connecting via SSH

The free edition of NoMachine does not allow to use the SSH protocol to connect to the target computer and only NX protocol (listening on port `4000` by default) is used.

If it is not preferred to open yet another port on the firewall, a workaround is to create a standard SSH tunnel between client and target computer and connect through it:

On the client computer, for example:

```
$ ssh -L 4000:localhost:4000 *user*@*targetmachine*

```

Then, start NoMachine Player and try to connect to `localhost` with the NX protocol. The connection will be tunneled to the *targetmachine* and redirected to the server's localhost port `4000`.