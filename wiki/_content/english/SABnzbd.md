SABnzbd is an open-source binary newsreader written in Python.

From [sabnzbd.org](http://sabnzbd.org/):

	It's totally free, incredibly easy to use, and works practically everywhere. SABnzbd makes Usenet as simple and streamlined as possible by automating everything we can. All you have to do is add an .nzb. SABnzbd takes over from there, where it will be automatically downloaded, verified, repaired, extracted and filed away with zero human interaction.

## Contents

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
    *   [2.1 Starting SABnzbd](#Starting_SABnzbd)
    *   [2.2 Running as daemon](#Running_as_daemon)
    *   [2.3 Stopping SABnzbd](#Stopping_SABnzbd)
    *   [2.4 Accessing the web-interface](#Accessing_the_web-interface)
    *   [2.5 Local configuration](#Local_configuration)
        *   [2.5.1 Running as user without systemd user instance](#Running_as_user_without_systemd_user_instance)
*   [3 Tips and tricks](#Tips_and_tricks)
    *   [3.1 Enabling HTTPS](#Enabling_HTTPS)
    *   [3.2 Using a custom port](#Using_a_custom_port)
*   [4 See also](#See_also)

## Installation

Install the [sabnzbd](https://aur.archlinux.org/packages/sabnzbd/) or [sabnzbd-git](https://aur.archlinux.org/packages/sabnzbd-git/) package.

## Configuration

SABnzbd is able to run globally (settings apply to all users) and locally (per user settings). The way of setting up SABnzbd depends on the way it is intended to be used. A local configuration may prove more useful on a desktop system when used by several people simultaneously.

### Starting SABnzbd

The [sabnzbd](https://aur.archlinux.org/packages/sabnzbd/) package provides a `sabnzbd` [systemd](/index.php/Systemd "Systemd") service.

It is however possible to start SABnzbd using the following command:

```
$ sudo -u sabnzbd -H /opt/sabnzbd/SABnzbd.py -f /opt/sabnzbd/sabnzbd.ini

```

### Running as daemon

Append the `-d` parameter to start SABnzbd as [daemon](/index.php/Daemon "Daemon"):

```
$ sudo -u sabnzbd -H /opt/sabnzbd/SABnzbd.py -f /opt/sabnzbd/sabnzbd.ini -d

```

### Stopping SABnzbd

**Note:** SABnzbd can be easily shutdown by opening the main menu from the web-interface.

You need to know the `host`, `port` and `API-key`, which can all be found using the WebUI or by searching through `/opt/sabnzbd/sabnzbd.ini`.

Execute the following command to shutdown SABnzbd:

```
$ curl "[http://host:port/sabnzbd/api?mode=shutdown&apikey=API-key](http://host:port/sabnzbd/api?mode=shutdown&apikey=API-key)"

```

### Accessing the web-interface

**Tip:**

*   SABnzbd can only be accessed on the running computer. Change `host = 127.0.0.1` in `/opt/sabnzbd/sabnzbd.ini` to `host = 0.0.0.0` (or the host IP-address) to allow access from another computer.
*   SABnzbd listens on port `8080`. Change `port = 8080` in `/opt/sabnzbd/sabnzbd.ini` to the preferred port.

After starting SABnzbd, access the web-interface by browsing to [http://127.0.0.1:8080](http://127.0.0.1:8080).

### Local configuration

SABnzbd does not need to be run globally as a daemon and can rather work per user. The usual method to configure SABnzbd globally is because the listed files and folders in the default configuration file point to directories owned by sabnzbd (the `/opt/sabnzbd` directory).

A less used (but perhaps more sensible) method is to make SABnzbd work with files and directories owned by a normal user. Running SABnzbd as a normal user has the benefits of:

*   A single directory `~/.sabnzbd.ini` (or any other directory under `/home/username`) that will contain all the SABnzbd configuration files.
*   Easier to avoid unforeseen read/write permission errors.

In this case, we will use `~/.sabnzbd.ini/sabnzbd.ini` and not start sabnzbd.service as a daemon for the whole system and all users. We will NOT use the `/usr/lib/systemd/system/sabnzbd.service` which is intended to start the sabnzbd.service for all users. If you already enabled it, just disable it first:

 ` # systemctl disable sabnzbd.service` 

If you used to start SABnzbd inside your `~/.xinitrc`, comment or delete the line

 `sabnzbd -d` 

Then, edit a new file /etc/systemd/user/sabnzbd.service

 `/etc/systemd/user/sabnzbd.service` 
```
[Unit]
Description = SABnzbd binary newsreader

[Service]
EnvironmentFile = /etc/conf.d/sabnzbd_systemd
ExecStart = /bin/sh -c "python2 ${SABNZBD_DIR}/SABnzbd.py ${SABNZBD_ARGS} --pid /tmp"
ExecStop = /usr/bin/curl -f "${SABNZBD_PROTOCOL}://${SABNZBD_USPW}${SABNZBD_IP}:${SABNZBD_PORT}/sabnzbd/api?mode=shutdown&apikey=${SABNZBD_KEY}"
Type = forking
PIDFile = /tmp/sabnzbd-8080.pid

[Install]
WantedBy = default.target

```

Then, change this line in /etc/conf.d/sabnzbd_systemd

 `/etc/conf.d/sabnzbd_systemd` 
```
SABNZBD_ARGS=-f ${HOME}/.sabnzbd.ini -s ${SABNZBD_IP}:${SABNZBD_PORT} -d

```

Then, add this line if not already to [.xinitrc](/index.php/.xinitrc ".xinitrc")

 `~/.xinitrc` 
```
#run systemd as user intsance
systemd --user &

```

Now, enable and start sabnzbd.service as per user

```
$ systemctl --user enable sabnzbd
$ systemctl --user start sabnzbd

```

Check the SABnzbd status and see if sabnzbd.service is correctly enabled and started

 `$ systemctl --user status sabnzbd` 

#### Running as user without systemd user instance

If you dont like the local configuration option, you may run sabnzbd as a user by doing this instead:

```
$ cp /usr/lib/systemd/system/sabnzbd.service /etc/systemd/system/sabnzbd.service

```

Then edit :

 `/etc/systemd/system/sabnzbd.service` 
```
[Unit]
Description = SABnzbd binary newsreader

[Service]
ExecStart = /bin/sh -c "python2 /opt/sabnzbd/SABnzbd.py -l0 -f /home/m/.sabnzbd/sabnzbd.ini -d --pid /tmp"
Type = forking
PIDFile = /tmp/sabnzbd-8080.pid
User = desired_user_name
Group = desired_group_name
[Install]
WantedBy = default.target
```

## Tips and tricks

### Enabling HTTPS

Enabling https is a threefold process.

For global configuration:

*   edit `/opt/sabnzbd/sabnzbd.ini` and set **enable_https** to `1`

*   copy `/usr/lib/systemd/system/sabnzbd.service` to `/etc/systemd/system/` then edit it and set **PIDFile** to `/run/sabnzbd/sabnzbd-9090.pid`

*   reload systemd with `# systemctl --system daemon-reload`

For local configuration:

*   edit `/opt/sabnzbd/sabnzbd.ini` and set **enable_https** to `1`

*   then edit `/etc/systemd/user/sabnzbd.service` and set **PIDFile** to `/tmp/sabnzbd-9090.pid`

*   reload systemd with `$ systemctl --user daemon-reload`

You should now be able to start sabnzbd with SSL support.

### Using a custom port

Using a custom port is similar to using https.

For global configuration:

*   edit `/opt/sabnzbd/sabnzbd.ini` and set **port** in **[misc]** section to the port you wish to use.

*   copy `/usr/lib/systemd/system/sabnzbd.service` to `/etc/systemd/system/` then edit it and set **PIDFile** to `/run/sabnzbd/sabnzbd-*yourport*.pid` where *yourport* is the same as set in the first step.

*   edit `/etc/conf.d/sabnzbd_systemd` and set **SABNZBD_PORT** to the port set in the first step.

*   reload systemd with `# systemctl --system daemon-reload`

For local configuration:

*   edit `/opt/sabnzbd/sabnzbd.ini` and set **port** in **[misc]** section to the port you wish to use.

*   then edit `/etc/systemd/user/sabnzbd.service` and set **PIDFile** to `/tmp/sabnzbd-*yourport*.pid` where *yourport* is the same as set in the first step.

*   edit `/etc/conf.d/sabnzbd_systemd` and set **SABNZBD_PORT** to the port set in the first step.

*   reload systemd with `$ systemctl --user daemon-reload`

You should now be able to start sabnzbd with a custom port.

## See also

*   [SABnzbd homepage](http://sabnzbd.org/)
*   [SABnzbd wiki](http://wiki.sabnzbd.org/)