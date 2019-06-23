[taskd](https://github.com/GothenburgBitFactory/taskserver) is a lightweight, secure server for [Taskwarrior](https://en.wikipedia.org/wiki/Taskwarrior "wikipedia:Taskwarrior") ([task](https://www.archlinux.org/packages/?name=task)). It allows users to intelligently synchronize their tasks between multiple clients, including between desktop and mobile ones.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Server](#Server)
    *   [1.1 Installation](#Installation)
    *   [1.2 Setup](#Setup)
    *   [1.3 Running](#Running)
    *   [1.4 Adding a user in taskd](#Adding_a_user_in_taskd)
*   [2 Client](#Client)
    *   [2.1 User configuration](#User_configuration)
    *   [2.2 Using the Android Taskwarrior app](#Using_the_Android_Taskwarrior_app)
*   [3 Troubleshooting](#Troubleshooting)
    *   [3.1 Unreachable Server](#Unreachable_Server)
    *   [3.2 "Bad Key"](#"Bad_Key")
    *   [3.3 taskd.service fails to start on boot](#taskd.service_fails_to_start_on_boot)

## Server

### Installation

taskd is available in the official repos as [taskd](https://www.archlinux.org/packages/?name=taskd) and in the AUR as [taskd-git](https://aur.archlinux.org/packages/taskd-git/).

### Setup

Once taskd is installed, you need to set it up. The first step is to `$ export TASKDDATA=/var/lib/taskd ` (otherwise you need to append `--data /var/lib/taskd` to every taskd command).

Next, edit the `/usr/share/doc/taskd/pki/vars` file. The `CN=` line must either match the server's hostname or IP address, depending on how you connect. Once the file is edited to your heart's content, change to the directory `/usr/share/doc/taskd/pki/` and run `./generate`. This will create self-signed certificates for your server. Copy all generated `.pem` to `/var/lib/taskd`. Note that at least the `ca.cert.pem` must remain in the `pki` folder for the user-certificate generation later on.

Now you need to configure taskd. Use `taskd config` or add the following to `/var/lib/taskd/config` directly.

 `/var/lib/taskd/config` 
```
client.cert=/var/lib/taskd/client.cert.pem
client.key=/var/lib/taskd/client.key.pem
server.cert=/var/lib/taskd/server.cert.pem
server.key=/var/lib/taskd/server.key.pem
server.crl=/var/lib/taskd/server.crl.pem
ca.cert=/var/lib/taskd/ca.cert.pem

```

Additionally you should change where taskd logs to, since the default is `/tmp/taskd.log`. This can be done by running

```
# touch /var/log/taskd.log
# chown taskd:taskd /var/log/taskd.log
# taskd config --force log /var/log/taskd.log
```

The last step is to set taskd's server name, which must be the same as the one used in the certificates: `taskd config --force server servername:port`. Note that taskd has no default port and it must be set manually.

### Running

[Start/enable](/index.php/Start/enable "Start/enable") `taskd.service`.

### Adding a user in taskd

taskd organizes data into groups and users, with each user being in a group.

To add a user, run the following commands, substituting `[group]` and `[username]` as you wish.

```
# taskd add org [group]
# taskd add user [group] [username]

```

Note the key the last command returns, the user will need it to synchronize.

Make sure new group and user are readable by user `taskd`.

 `# chown -R taskd:taskd /var/lib/taskd/orgs` Return to `/usr/share/doc/taskd/pki/` and run `# ./generate.client username` This will return `username.cert.pem` and `username.key.pem`.

The `username.key.pem`, `username.cert.pem` and `ca.cert.pem` must be copied into to the user's Taskwarrior user data directory (default `~/.task`).

## Client

### User configuration

Once the `.pem` files have been copied to a user's Taskwarrior data directory, their configuration must be updated to point to the files.

Add the following to the `config` file in the same directory:

 `/var/lib/taskd/config` 
```
taskd.server=servername:port
taskd.credentials=group/username/key
taskd.certificate=~/.task/username.cert.pem
taskd.key=~/.task/username.key.pem
taskd.ca=~/.task/ca.cert.pem

```

Paths are relative to the directory in which `task` is executed, so paths should be relative to `~` or absolute.

Perform the initial synchronization and consent to sending your Taskwarrior data to the server:

 `$ task sync init` 

Send local changes to the server:

 `$ task sync` 

### Using the Android Taskwarrior app

Before you even download the android app, you need to create a folder. On your external storage (or if you only have an internal one, then there) create the folder `Android/data/kvj.taskw/files/key` where "key" is the same as the key given when creating the user with `taskd`. Then add the `username.key.pem`, `username.cert.pem` and `ca.cert.pem` files to that folder.

Create a new file in that folder called `.taskrc.android`. It should look like this:

 `/sdcard/Android/data/kvj.taskw/files/[uuid]/.taskrc.android` 
```
taskd.server=servername:port
taskd.credentials=group/username/key
taskd.certificate=username.cert.pem
taskd.key=username.key.pem
taskd.ca=ca.cert.pem

```

Ensure that the config file `.taskrc.android` has a newline at the end. Otherwise, it will not be parsed correctly.

Now download the app and start it. When prompted to add a profile, choose the data folder that you just created. Taskwarrior should now sync and work as expected.

## Troubleshooting

### Unreachable Server

Should the server be unreachable but running, it bound itself to an IPv6 address. You can force IPv4 by adding `family=IPv4` to `/var/lib/taskd/config`.

If the server stalls on "Server starting", it may be failing to resolve the address you've specified in the `server` option. After a while the server will time out with "Name or service not known". In that case, try adding an external `/etc/hosts` entry aliasing that address to your external IP address (see [Domain name resolution](/index.php/Domain_name_resolution "Domain name resolution")),

Restart taskd after attempting these, then check if your issue is fixed.

### "Bad Key"

If the server responds with a "Bad Key" error even though you just generated them, check the permissions of the created folders (everything in `/var/lib/taskd/` and subfolders). taskd doesn't set it's own uid / gid, so those folders must be manually chowned to taskd.

### taskd.service fails to start on boot

In case your systemd unit for taskd fails to start on boot you can add a delay for this particular unit by adding a [systemd timer](/index.php/Systemd#Timers "Systemd"):

 `/etc/systemd/system/taskd.timer` 
```
[Unit]
Description=Start taskd.service after fixed amount of time

[Timer]
OnStartupSec=10
Unit=taskd.service

[Install]
WantedBy=multi-user.target

```

Then disable `taskd.service` and enable `taskd.timer`