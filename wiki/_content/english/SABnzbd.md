SABnzbd is an open-source binary newsreader written in Python.

From [sabnzbd.org](http://sabnzbd.org/):

	It's totally free, incredibly easy to use, and works practically everywhere. SABnzbd makes Usenet as simple and streamlined as possible by automating everything we can. All you have to do is add an .nzb. SABnzbd takes over from there, where it will be automatically downloaded, verified, repaired, extracted and filed away with zero human interaction.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Installation](#Installation)
    *   [1.1 SSL Support](#SSL_Support)
    *   [1.2 Archive unpacking](#Archive_unpacking)
*   [2 Usage](#Usage)
    *   [2.1 Global usage](#Global_usage)
    *   [2.2 Running SABnzbd as a user w/ systemd](#Running_SABnzbd_as_a_user_w/_systemd)
    *   [2.3 Stopping SABnzbd](#Stopping_SABnzbd)
    *   [2.4 Accessing the web-interface](#Accessing_the_web-interface)
*   [3 See also](#See_also)

## Installation

[Install](/index.php/Install "Install") [sabnzbd](https://aur.archlinux.org/packages/sabnzbd/) or [sabnzbd-git](https://aur.archlinux.org/packages/sabnzbd-git/).

### SSL Support

[Install](/index.php/Install "Install") [python2-pyopenssl](https://www.archlinux.org/packages/?name=python2-pyopenssl) to enable SSL support for news servers:

*   Transmission of data from the server to the NNTP client is encrypted, protecting your privacy
*   Decreasing the chances of throttling NNTP traffic done by the ISP.

### Archive unpacking

*   [Install](/index.php/Install "Install") [p7zip](https://www.archlinux.org/packages/?name=p7zip) and [unzip](https://www.archlinux.org/packages/?name=unzip) to allow unpacking of archives.

## Usage

SABnzbd is able to run globally (settings apply to all users) and locally (per user settings). The way of setting up SABnzbd depends on the way it is intended to be used. A local configuration may prove more useful on a desktop system when used by several people simultaneously.

**Note:** Both [sabnzbd](https://aur.archlinux.org/packages/sabnzbd/) and [sabnzbd-git](https://aur.archlinux.org/packages/sabnzbd-git/) provide the `sabnzbd.service` [systemd](/index.php/Systemd "Systemd") unit, create the [user](/index.php/User "User") and [user group](/index.php/User_group "User group") `sabnzbd`, and use `/opt/sabnzbd/sabnzbd.ini` for configuration.

If SABnzbd is started for the first time, the webinterface will present a setup wizard for configuring UI language and a single news server.

Further configuration can be done from within the UI (adding additional servers, setting folder paths etc.) or by editing `sabnzbd.ini`.

### Global usage

[Start/enable](/index.php/Start/enable "Start/enable") `sabnzbd.service`.

Add users to the `sabnzbd` [user group](/index.php/User_group "User group") to allow read/write access to SABnzbd files.

### Running SABnzbd as a user w/ systemd

Alternatively, [enable](/index.php/Enable "Enable") and [start](/index.php/Start "Start") the `sabnzbd@*myuser*.service` to run SABnzbd under the preferred user.

### Stopping SABnzbd

SABnzbd can be easily shutdown in the web-interface or the [systemd](/index.php/Systemd "Systemd") `sabnzbd.service` unit.

It is also possible to shutdown a running (remote) SABnzbd client using the provided API:

```
$ curl "http(s)://host:port/sabnzbd/api?mode=shutdown&apikey=API-key"

```

### Accessing the web-interface

After starting SABnzbd, access the web-interface by browsing to [http://127.0.0.1:8080](http://127.0.0.1:8080).

**Tip:**

*   SABnzbd can only be accessed on the running computer. Change `host = 127.0.0.1` in `/opt/sabnzbd/sabnzbd.ini` to `host = 0.0.0.0` (or the host IP-address) to allow access from another computer.
*   SABnzbd listens on port `8080`. Change `port = 8080` in `sabnzbd.ini` to the preferred port.

## See also

*   [SABnzbd homepage](http://sabnzbd.org/)
*   [SABnzbd wiki](http://wiki.sabnzbd.org/)