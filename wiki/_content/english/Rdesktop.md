Related articles

*   [xrdp](/index.php/Xrdp "Xrdp")
*   [Remmina](/index.php/Remmina "Remmina")

[rdesktop](http://www.rdesktop.org/) is a free, open source client for Microsoft's proprietary RDP protocol released under the GNU General Public License. Use rdesktop to connect to Windows 2000/XP/Vista/Win7 RDP server to remotely administrate the Windows box.

As of July 2008, rdesktop implements a large subset of the RDP 5 protocol, including:

*   Bitmap caching
*   File system, audio, serial port and printer port redirection
*   Mappings for most international keyboards
*   Stream compression and encryption
*   Automatic authentication
*   Smartcard support
*   RemoteApp like support called "seamless" mode via SeamlessRDP

Still unimplemented are:

*   Remote Assistance requests
*   USB device redirection

Support for the additional features available in RDP 5.1 and RDP 6 (including multi-head display spanning and window composition) also have not yet been implemented.

## Contents

*   [1 Installation](#Installation)
*   [2 Usage](#Usage)
*   [3 Tips and tricks](#Tips_and_tricks)
    *   [3.1 Automatic scaling of geometry](#Automatic_scaling_of_geometry)
    *   [3.2 Remote desktop using NetBIOS names instead of using IP address](#Remote_desktop_using_NetBIOS_names_instead_of_using_IP_address)
    *   [3.3 Supplying missing cursors](#Supplying_missing_cursors)
*   [4 See also](#See_also)

## Installation

[Install](/index.php/Install "Install") [rdesktop](https://www.archlinux.org/packages/?name=rdesktop) from the [official repositories](/index.php/Official_repositories "Official repositories").

## Usage

For a complete listing of options see [rdesktop(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/rdesktop.1). Here is a typical line:

```
$ rdesktop -g 1440x900 -P -z -x l -r sound:off -u windowsuser 98.180.102.33:3389

```

Reading from left to right:

| `-g 1440x900` | Sets the resolution of the display to 1440x900 |
| `-P` | Enables bitmap caching/speeds up xfers. |
| `-z` | Enables RDP datastream compression |
| `-x l` | Uses the "lan" quality experience level, see the man page for additional options |
| `-r sound:off` | Redirects sound generated on the server to null |
| `-u windowsuser` | This defines the username to use when logging into the Windows box |
| `98.180.102.33:3389` | This is the IP address and port number of the target machine |

## Tips and tricks

### Automatic scaling of geometry

In order to automatically scale the geometry to fit the screen, pass

```
-g $(xrandr -q | awk '/Screen 0/ {print int($8/1.28) $9 int($10/1.2)}' | sed 's/,//g')

```

to the rdesktop command.

Another option is to use the "-g" flag

```
 $ rdesktop -g 100% -P -z 98.180.102.33:3389

```

### Remote desktop using NetBIOS names instead of using IP address

If you do not know the IP address of a Windows computer in a network, you have to enable wins support. To do so, you have to install [samba](/index.php/Samba "Samba"). Enabling wins in samba is surprisingly easy: just edit the `/etc/samba/smb.conf` and add the following line to it, or uncomment the appropriate line:

```
wins support = yes

```

Then you have to install winbind, then edit the `/etc/nsswitch.conf` and add the "wins" to the list of hosts.

Restart `smbd` and `nmbd` services and test your success by pinging a Windows NetBIOS host.

### Supplying missing cursors

See [Cursor themes#Supplying missing cursors](/index.php/Cursor_themes#Supplying_missing_cursors "Cursor themes").

## See also

*   [rdesktop official homepage](http://www.rdesktop.org/)
*   [freerdp](https://www.archlinux.org/packages/?name=freerdp) a rdesktop fork that supports RDP 7.1 features including network level authentication (NLA). See also [[1]](http://askubuntu.com/a/97932/217269).