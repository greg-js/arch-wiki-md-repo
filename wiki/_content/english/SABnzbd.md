SABnzbd is an open-source binary newsreader written in Python.

From [sabnzbd.org](http://sabnzbd.org/):

	It's totally free, incredibly easy to use, and works practically everywhere. SABnzbd makes Usenet as simple and streamlined as possible by automating everything we can. All you have to do is add an .nzb. SABnzbd takes over from there, where it will be automatically downloaded, verified, repaired, extracted and filed away with zero human interaction.

## Contents

*   [1 Installation](#Installation)
*   [2 Usage](#Usage)
    *   [2.1 Using systemd](#Using_systemd)
    *   [2.2 Starting SABnzbd as user](#Starting_SABnzbd_as_user)
    *   [2.3 Stopping SABnzbd](#Stopping_SABnzbd)
    *   [2.4 Accessing the web-interface](#Accessing_the_web-interface)
*   [3 Tips and tricks](#Tips_and_tricks)
    *   [3.1 Enable SSL-support for news servers](#Enable_SSL-support_for_news_servers)
*   [4 See also](#See_also)

## Installation

Install the [sabnzbd](https://aur.archlinux.org/packages/sabnzbd/) or [sabnzbd-git](https://aur.archlinux.org/packages/sabnzbd-git/) package.

## Usage

SABnzbd is able to run globally (settings apply to all users) and locally (per user settings). The way of setting up SABnzbd depends on the way it is intended to be used. A local configuration may prove more useful on a desktop system when used by several people simultaneously.

If SABnzbd is started for the first time, the webinterface will present a setup wizard for configuring UI language and a single news server.

Further configuration can be done from within the UI (adding additional servers, setting folder paths etc.) or by editing `sabnzbd.ini`.

### Using systemd

Both [sabnzbd](https://aur.archlinux.org/packages/sabnzbd/) and [sabnzbd-git](https://aur.archlinux.org/packages/sabnzbd-git/) provide a [systemd](/index.php/Systemd "Systemd") service, create the [user](/index.php/User "User") and [group](/index.php/Group "Group") `sabnzbd`, and use `/opt/sabnzbd/sabnzbd.ini` for configuration.

Add users to the `sabnzbd` [group](/index.php/Group "Group") to allow access to SABnzbd files.

### Starting SABnzbd as user

Running `$ sabnzbd`, without any further configuration, results in two processes owned by the launching user: `/usr/bin/sabnzbd` and `/opt/sabnzbd/SABnzbd.py -f /home/**user**/.sabnzbd.ini`.

Append the `-d` parameter to start SABnzbd as [daemon](/index.php/Daemon "Daemon"):

```
$ sabnzbd -d

```

Use `~/sabnzbd.ini/sabnzbd.ini` for configuration.

### Stopping SABnzbd

SABnzbd can be easily shutdown in the web-interface or the [systemd](/index.php/Systemd "Systemd") `sabnzbd` unit.

It is also possible to shutdown a running (remote) SABnzbd client using the provided API:

```
$ curl "http(s)://host:port/sabnzbd/api?mode=shutdown&apikey=API-key"

```

### Accessing the web-interface

**Tip:**

*   SABnzbd can only be accessed on the running computer. Change `host = 127.0.0.1` in `/opt/sabnzbd/sabnzbd.ini` to `host = 0.0.0.0` (or the host IP-address) to allow access from another computer.
*   SABnzbd listens on port `8080`. Change `port = 8080` in `sabnzbd.ini` to the preferred port.

After starting SABnzbd, access the web-interface by browsing to [http://127.0.0.1:8080](http://127.0.0.1:8080).

## Tips and tricks

### Enable SSL-support for news servers

Install [python2-pyopenssl](https://www.archlinux.org/packages/?name=python2-pyopenssl) to enable SSL support for news servers.

The usage of SSL connections is recommend (if supported by the news server):

*   Transmission of data from the server to the NNTP client is encrypted, protecting your privacy.
*   Decreasing the chance of throttling NNTP traffic by the ISP.

## See also

*   [SABnzbd homepage](http://sabnzbd.org/)
*   [SABnzbd wiki](http://wiki.sabnzbd.org/)