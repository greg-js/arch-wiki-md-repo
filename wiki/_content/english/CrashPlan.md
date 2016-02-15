CrashPlan is a backup program that backs up data to remote servers, other computers, or hard drives. Backing up to the cloud servers requires a monthly subscription.

## Contents

*   [1 Installation](#Installation)
*   [2 Basic Usage](#Basic_Usage)
*   [3 Running Crashplan on a headless server](#Running_Crashplan_on_a_headless_server)
*   [4 Troubleshooting](#Troubleshooting)
    *   [4.1 Waiting for connection](#Waiting_for_connection)
    *   [4.2 Waiting for Backup](#Waiting_for_Backup)
    *   [4.3 Desktop GUI Crashes on startup](#Desktop_GUI_Crashes_on_startup)
    *   [4.4 Out of Memory](#Out_of_Memory)
    *   [4.5 Real time protection](#Real_time_protection)
*   [5 See also](#See_also)

## Installation

Install [crashplan](https://aur.archlinux.org/packages/crashplan/) from the [AUR](/index.php/AUR "AUR"). There is also [crashplan-pro](https://aur.archlinux.org/packages/crashplan-pro/) and [crashplan-pro-e](https://aur.archlinux.org/packages/crashplan-pro-e/) available which are the paid enterprise packages.

## Basic Usage

Before accessing CrashPlan's graphical user interface, you should start the service:

```
# systemctl start crashplan.service

```

CrashPlan can be configured entirely through its graphical user interface. To start the graphical interface:

```
$ CrashPlanDesktop

```

To make CrashPlan automatically start upon system startup:

```
# systemctl enable crashplan.service

```

## Running Crashplan on a headless server

Running CrashPlan on a headless server is not officially supported. However, it is possible to do so.

The CrashPlan daemon's configuration files (in `/opt/crashplan/conf`) are in an obscure XML format, and they are meant to be edited programmatically by the CrashPlan client. The CrashPlan client and daemon communicate on port 4243 by default. Thus, an easy way of configuring the CrashPlan daemon on a headless server is to create an SSH tunnel:

1.  Start the CrashPlan daemon. On the server: `systemctl start crashplan.service`.
2.  Create an SSH tunnel. On the client: `ssh -N -L 4243:localhost:4243 headless.example.com`.
3.  Start the CrashPlan client. (Again, the executable is named `CrashPlanDesktop`.)

More ideas can be found on these websites:

*   The CrashPlan support site [details](http://support.code42.com/CrashPlan/Latest/Configuring/Configuring_A_Headless_Client) a slightly more complicated method of tunneling traffic from the client (CrashPlan Desktop) to the daemon (CrashPlan Engine) through an SSH tunnel.
*   A [post by Bryan Ross](http://www.liquidstate.net/how-to-manage-your-crashplan-server-remotely/) details how to make CrashPlan Desktop connect directly to CrashPlan Engine. Note that this method can be less secure than tunneling traffic through an SSH tunnel.

Another, simpler, way of running CrashPlan headlessly is to use ssh's X11 forwarding. Ensure that `X11Forwarding` is set to `yes` in the headless server's `/etc/ssh/sshd_config` and from another machine running X11, ssh to the headless machine with either `-X` or `-Y` and from the remote shell run `CrashPlanDesktop`. The headless machine's windows will appear on the local X11 server.

## Troubleshooting

### Waiting for connection

On some systems it can happen that CrashPlan does not wait until an internet connection is established. If using [NetworkManager](/index.php/NetworkManager "NetworkManager"), you can install [networkmanager-dispatcher-crashplan-systemd](https://aur.archlinux.org/packages/networkmanager-dispatcher-crashplan-systemd/) which will automatically restart the CrashPlan service once a connection is successfully established.

### Waiting for Backup

If the backup is stuck on «Waiting for Backup» even after you engage it manually, it might be that CrashPlan cannot access the tempdir or it is mounted as `noexec`. It uses the default Java tmp dir which is normally `/tmp`. You can either remove the `noexec` mount option (not recommended) or change the tmpdir CrashPlan is using.

To change the tmpdir CrashPlan uses, open `/opt/crashplan/bin/run.conf` and insert `-Djava.io.tmpdir=/new-tempdir` to `SRV_JAVA_OPTS`, for example:

```
SRV_JAVA_OPTS="-Djava.io.tmpdir=/var/tmp/crashplan -Dfile.encoding=UTF-8 …

```

Make sure to create the new tmpdir and verify CrashPlan's user has access to it.

```
# mkdir /var/tmp/crashplan

```

Restart CrashPlan

```
# systemctl restart crashplan

```

### Desktop GUI Crashes on startup

On systems with Gnome 3 installed, or with libwebkit-gtk installed, there may be an issue where the GUI crashes on launch. This can be fixed by following the instructions [here](https://support.code42.com/CrashPlan/Latest/Troubleshooting/CrashPlan_Client_Closes_In_Some_Linux_Installations).

### Out of Memory

For backup sets containing large numbers of files (more than 100,000 or so), the default maximum heap size of 512M may be too small. If this is filled, the server will silently restart, and will usually get stuck restarting as it continually reaches the memory limit. The only sign of this happening is the creation of many small log files in `/opt/crashplan/bin` for each service restart (potentially hundreds of thousands, depending on how long it takes to notice the problem). To increase the heap size limit, adjust the `-Xmx` option in `/opt/crashplan/bin/run.conf` to a reasonable value for your system.

### Real time protection

If you use real time protection for your backup set and have a lot of files to backup, the default system configuration might not be able to allocate all required handle to follow all files in real time. This issue can manifest itself with logs like "inotify_add_watch: No space left on device" in the syslog journal. You can follow instruction [here](http://support.code42.com/CrashPlan/Latest/Troubleshooting/Real-Time_Backup_For_Network-Attached_Drives) and configure inotify max_user_watches to a bigger value to fix the iusse.

## See also

*   [Backup programs](/index.php/Backup_programs "Backup programs")
*   [CrashPlan home page](http://www.code42.com/crashplan/)
*   [CrashPlan On A Headless Server - Code42Support](http://support.code42.com/CrashPlan/Latest/Configuring/Using_CrashPlan_On_A_Headless_Computer)
*   [Wikipedia:CrashPlan](https://en.wikipedia.org/wiki/CrashPlan "wikipedia:CrashPlan")