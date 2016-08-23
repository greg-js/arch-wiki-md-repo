## Contents

*   [1 Browsing experience](#Browsing_experience)
    *   [1.1 chrome://xxx](#chrome:.2F.2Fxxx)
    *   [1.2 Broken icons in Download tab](#Broken_icons_in_Download_tab)
    *   [1.3 Chromium overrides/overwrites Preferences file](#Chromium_overrides.2Foverwrites_Preferences_file)
    *   [1.4 Search engines](#Search_engines)
    *   [1.5 Tmpfs](#Tmpfs)
        *   [1.5.1 Cache in tmpfs](#Cache_in_tmpfs)
        *   [1.5.2 Profile in tmpfs](#Profile_in_tmpfs)
    *   [1.6 Launch a new browser instance](#Launch_a_new_browser_instance)
    *   [1.7 Directly open *.torrent files and magnet links with a torrent client](#Directly_open_.2A.torrent_files_and_magnet_links_with_a_torrent_client)
    *   [1.8 Touch Scrolling on touchscreen devices](#Touch_Scrolling_on_touchscreen_devices)
    *   [1.9 Disable system tray icon](#Disable_system_tray_icon)
    *   [1.10 Reduce memory usage](#Reduce_memory_usage)
    *   [1.11 User Agent](#User_Agent)
*   [2 Profile maintenance](#Profile_maintenance)
*   [3 Security](#Security)
    *   [3.1 WebRTC](#WebRTC)
    *   [3.2 SSL certificates](#SSL_certificates)
        *   [3.2.1 Adding CAcert certificates for self-signed certificates](#Adding_CAcert_certificates_for_self-signed_certificates)
        *   [3.2.2 Example 1: Using a shell script to isolate the certificate from TomatoUSB](#Example_1:_Using_a_shell_script_to_isolate_the_certificate_from_TomatoUSB)
        *   [3.2.3 Example 2: Using Firefox to isolate the certificate from TomatoUSB](#Example_2:_Using_Firefox_to_isolate_the_certificate_from_TomatoUSB)
*   [4 Making flags persistent](#Making_flags_persistent)
*   [5 See also](#See_also)

## Browsing experience

### chrome://xxx

A number of tweaks can be accessed via typing *chrome://xxx* in the URL field. A complete list is available by typing **chrome://chrome-urls** into the URL field. Some of note are listed below:

*   **chrome://flags** - access experimental features such as WebGL and rendering webpages with GPU, etc.
*   **chrome://plugins** - view, enable and disable the currently used Chromium plugins.
*   **chrome://gpu** - status of different GPU options.
*   **chrome://sandbox** - indicate sandbox status.
*   **chrome://version** - display version and switches used to invoke the active `/usr/bin/chromium`.

An automatically updated, complete listing of Chromium switches is available [here](http://peter.sh/experiments/chromium-command-line-switches/).

### Broken icons in Download tab

If Chromium shows icon placeholders (icons representing broken documents) instead of appropriate icons in its Download tab, the likely cause is that the [gnome-icon-theme](https://www.archlinux.org/packages/?name=gnome-icon-theme) package is not installed.

### Chromium overrides/overwrites Preferences file

If you enabled syncing with a Google Account, then Chromium will override any direct edits to the Preferences file found under `$HOME/.config/chromium/Default/Preferences`. To work around this, start Chromium with the `--disable-sync-preferences` switch:

```
$ chromium --disable-sync-preferences

```

If Chromium is started in the background when you login in to your desktop environment, make sure the command your desktop environment uses is:

```
$ chromium --disable-sync-preferences --no-startup-window

```

### Search engines

Make sites like [wiki.archlinux.org](https://wiki.archlinux.org) and [wikipedia.org](https://en.wikipedia.org) easily searchable by first executing a search on those pages, then going to *Settings > Search* and click the *Manage search engines..* button. From there, "Edit" the Wikipedia entry and change its keyword to **w** (or some other shortcut you prefer). Now searching Wikipedia for "Arch Linux" from the address bar is done simply by entering "**w arch linux**".

**Note:** Google search is used automatically when typing something into the URL bar. A hard-coded keyword trigger is also available using the **?** prefix.

### Tmpfs

#### Cache in tmpfs

**Note:** Chromium actually keeps its cache directory **separate** from its browser profile directory.

To limit Chromium from writing its cache to a physical disk, one can define an alternative location via the `--disk-cache-dir=/foo/bar` flag:

```
$ chromium --disk-cache-dir=/tmp/cache

```

Cache should be considered temporary and will **not** be saved after a reboot or hard lock. Alternatively, use:

 `/etc/fstab`  `tmpfs	/home/*username*/.cache	tmpfs	noatime,nodev,nosuid,size=400M	0	0` 
**Warning:** Adjust the size as needed and be careful. If the size is too large and you are using a sync daemon such as [psd](/index.php/Psd "Psd") on a conventional HDD, it will likely result in very slow start-up times of your graphical system due to long sync back times of the daemon.

#### Profile in tmpfs

Relocate the browser profile to a [tmpfs](https://en.wikipedia.org/wiki/Tmpfs "wikipedia:Tmpfs") filesystem, including `/tmp`, or `/dev/shm` for improvements in application response as the entire profile is now stored in RAM.

Use an active profile management script for maximal reliability and ease of use.

[profile-sync-daemon](https://aur.archlinux.org/packages/profile-sync-daemon/) is such a script and is directly available from the [AUR](/index.php/AUR "AUR"). It symlinks and syncs the browser profile directories to RAM. Refer to the [Profile-sync-daemon](/index.php/Profile-sync-daemon "Profile-sync-daemon") wiki article for additional information on it.

### Launch a new browser instance

When you launch the browser, it first checks if another instance using the same profile is already running. If there is one, the new window is associated with the old instance. To prevent this, you can specifically ask the browser to run with a different profile.

```
$ chromium --user-data-dir=<PATH TO A PROFILE>

```

**Note:** It will not work if you specify a link or even a symlink to your regular Chromium profile (typically `~/.config/chromium/Default`). If you want to use the same profile as your current one for this new instance, first copy the folder `~/.config/chromium/Default` to a directory of your choice, keeping the same `Default` name, and launch the browser using the following command by specifying the parent folder of the `Default` folder you have just copied.

For example, if you copied the Default folder to `~/Downloads`:

 `$ chromium --user-data-dir=~/Downloads` 

### Directly open *.torrent files and magnet links with a torrent client

By default, Chromium downloads `*.torrent` files directly and you need to click the notification from the bottom-left corner of the screen in order for the file to be opened with your default torrent client. This can be avoided with the following method:

*   Download a `*.torrent` file.
*   Right-click the notification displayed at the bottom-left corner of the screen.
*   Check the "*Always Open Files of This Type*" checkbox.

See [xdg-open](/index.php/Xdg-open "Xdg-open") to change the default assocation.

### Touch Scrolling on touchscreen devices

Chrome and Chromium do not support touchscreen by default. There are a couple settings you can change in the "Flags" portion of Chrome to potentially make it work for your device. This has been tested in [chromium](https://www.archlinux.org/packages/?name=chromium) from the [official repositories](/index.php/Official_repositories "Official repositories") and [google-chrome](https://aur.archlinux.org/packages/google-chrome/) from the [AUR](/index.php/AUR "AUR").

*   Browse to **chrome://flags** and set everything to default
*   Switch "*Enable Touch events*" to "*Enabled*" (**chrome://flags/#touch-events**)
*   Restart Chrome and touch scrolling should work. If it does not, it is worth trying the other modes that are available.
*   You may need to specify which touch device to use. Find your touchscreen device with `xinput list` then launch Chromium with the `--touch-devices=**x**` parameter, where "**x**" is the id of your device.
    **Note:** If the device is designated as a slave pointer, using this may not work, use the master pointer's ID instead.

### Disable system tray icon

Open the URL `chrome://flags` in the browser. Disable this flag:

*   `device-discovery-notifications`

Click the restart button at the bottom of the page.

### Reduce memory usage

By default, Chromium uses a separate OS process for each *instance* of a visited web site. [[1]](https://www.chromium.org/developers/design-documents/process-models#Supported_Models) However, you can specify command-line switches when starting Chromium to modify this behaviour.

For example, to share one process for all instances of a website:

```
$ chromium --process-per-site

```

To use a single process model:

```
$ chromium --single-process

```

**Warning:** While the single-process model is the default in [Firefox](/index.php/Firefox "Firefox") [[2]](https://wiki.mozilla.org/Electrolysis) and other browsers, it may contain bugs not present in other models. [[3]](https://www.chromium.org/developers/design-documents/process-models#TOC-Single-process)

In addition, you can suspend or store inactive Tabs with extensions such as [Tab Suspender](https://chrome.google.com/webstore/detail/tab-suspender/fiabciakcmgepblmdkmemdbbkilneeeh?hl=en) and [OneTab](https://chrome.google.com/webstore/detail/onetab/chphlpgkkbolifaimnlloiipkdnihall?hl=en).

### User Agent

The User Agent can be arbitrarily modified at the start of Chromium's base instance via its `--user-agent="[string]"` parameter.

For the same User Agent as the stable Chrome release for Linux i686 (at the time of writing, the most popular Linux edition of Chrome) one would use:

```
--user-agent="Mozilla/5.0 (X11; Linux i686) AppleWebKit/535.2 (KHTML, like Gecko) Chrome/20.0.1132.47 Safari/536.11"

```

An official, automatically updated listing of Chromium releases which also shows the included WebKit version is available as the [OmahaProxy Viewer](https://omahaproxy.appspot.com/).

## Profile maintenance

Chromium uses [SQLite](/index.php/SQLite "SQLite") databases to manage history and the like. Sqlite databases become fragmented over time and empty spaces appear all around. But, since there are no managing processes checking and optimizing the database, these factors eventually result in a performance hit. A good way to improve startup and some other bookmarks- and history-related tasks is to defragment and trim unused space from these databases.

[profile-cleaner](https://aur.archlinux.org/packages/profile-cleaner/) and [browser-vacuum](https://aur.archlinux.org/packages/browser-vacuum/) in the [AUR](/index.php/AUR "AUR") do just this.

## Security

### WebRTC

WebRTC is a communication protocol that relies on JavaScript that can leak one's actual IP address from behind a VPN. While software like NoScript prevents this, it's probably a good idea to block this protocol directly as well, just to be safe. An [option to disable it](https://code.google.com/p/chromium/issues/detail?id=457492) is available via an [extension](https://chrome.google.com/webstore/detail/webrtc-network-limiter/npeicpdbkakmehahjeeohfdhnlpdklia).

One can test this via [this page](https://www.privacytools.io/webrtc.html).

### SSL certificates

Chromium does not have an SSL certificate manager. It relies on the NSS Shared DB `~/.pki.nssdb`. In order to add SSL certificates to the database, users will have to use the shell.

#### Adding CAcert certificates for self-signed certificates

Grab the CAcerts and create an `nssdb`, if one does not already exist. To do this, first install the [nss](https://www.archlinux.org/packages/?name=nss) package, then complete these steps:

```
$ mkdir -p $HOME/.pki/nssdb
$ cd $HOME/.pki/nssdb
$ certutil -N -d sql:.

```

```
$ curl -k -o "cacert-root.crt" "[http://www.cacert.org/certs/root.crt](http://www.cacert.org/certs/root.crt)"
$ curl -k -o "cacert-class3.crt" "[http://www.cacert.org/certs/class3.crt](http://www.cacert.org/certs/class3.crt)"
$ certutil -d sql:$HOME/.pki/nssdb -A -t TC -n "CAcert.org" -i cacert-root.crt 
$ certutil -d sql:$HOME/.pki/nssdb -A -t TC -n "CAcert.org Class 3" -i cacert-class3.crt

```

**Note:** Users will need to create a password for the database, if it does not exist.

Now users may manually import a self-signed certificate.

#### Example 1: Using a shell script to isolate the certificate from TomatoUSB

Below is a simple script that will extract and add a certificate to the user's `nssdb`:

```
#!/bin/sh
#
# usage:  import-cert.sh remote.host.name [port]
#
REMHOST=$1
REMPORT=${2:-443}
exec 6>&1
exec > $REMHOST
echo | openssl s_client -connect ${REMHOST}:${REMPORT} 2>&1 |sed -ne '/-BEGIN CERTIFICATE-/,/-END CERTIFICATE-/p'
certutil -d sql:$HOME/.pki/nssdb -A -t "P,," -n "$REMHOST" -i $REMHOST 
exec 1>&6 6>&-

```

Syntax is advertised in the commented lines.

References:

*   [http://blog.avirtualhome.com/adding-ssl-certificates-to-google-chrome-linux-ubuntu](http://blog.avirtualhome.com/adding-ssl-certificates-to-google-chrome-linux-ubuntu)
*   [https://chromium.googlesource.com/chromium/src/+/master/docs/linux_cert_management.md](https://chromium.googlesource.com/chromium/src/+/master/docs/linux_cert_management.md)

#### Example 2: Using Firefox to isolate the certificate from TomatoUSB

The [firefox](https://www.archlinux.org/packages/?name=firefox) browser can be used to save the certificate to a file for manual import into the database.

Using firefox:

1.  Browse to the target URL.
2.  Upon seeing the "This Connection is Untrusted" warning screen, click: *I understand the Risks > Add Exception...*
3.  Click: *View > Details > Export* and save the certificate to a temporary location (`/tmp/easy.pem` in this example).

Now import the certificate for use in Chromium:

```
$ certutil -d sql:$HOME/.pki/nssdb -A -t TC -n "easy" -i /tmp/easy.pem

```

**Note:** Adjust the name to match that of the certificate. In the example above, "easy" is the name of the certificate.

Reference:

*   [http://sahissam.blogspot.com/2012/06/new-ssl-certificates-for-tomatousb-and.html](http://sahissam.blogspot.com/2012/06/new-ssl-certificates-for-tomatousb-and.html)

## Making flags persistent

**Note:** Starting with `chromium 42.0.2311.90-1` only per-user flags are supported.

You can put your flags in a `chromium-flags.conf` file under `$HOME/.config/` (or under `$XDG_CONFIG_HOME` if you have configured that environment variable).

No special syntax is used; flags are defined as if they were written in a terminal.

*   The arguments are split on whitespace and shell quoting rules apply, but no further parsing is performed.
*   In case of improper quoting anywhere in the file, a fatal error is raised.
*   Flags can be placed in separate lines for readability, but this is not required.
*   Lines starting with a hash symbol (#) are skipped.

Below is an example `chromium-flags.conf` file that defines the flags `--start-maximized --incognito`:

```
# This line will be ignored.
--start-maximized
--incognito

```

**Tip:** If you have Pepper Flash installed, the launcher will automatically pass the correct flags to Chromium so you do not need to define any `--ppapi-flash-*` flags.

**Note:** The `chromium-flags.conf` file is specific to Arch Linux and is supported via a custom launcher script that was added in `chromium 42.0.2311.90-1`.

## See also

*   [Profile-sync-daemon](/index.php/Profile-sync-daemon "Profile-sync-daemon") - Systemd service that saves Chromium profile in tmpfs and syncs to disk
*   [Tmpfs](/index.php/Tmpfs "Tmpfs") - Tmpfs Filesystem in `/etc/fstab`
*   [Official tmpfs kernel Documentation](https://www.kernel.org/doc/Documentation/filesystems/tmpfs.txt)