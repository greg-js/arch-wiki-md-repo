[taskd](https://github.com/GothenburgBitFactory/taskserver) is a lightweight, secure server providing multi-user, multi-client access to task data. This allows true syncing between desktop and mobile clients.

## Contents

*   [1 Server](#Server)
    *   [1.1 Installation](#Installation)
    *   [1.2 Setup](#Setup)
    *   [1.3 Adding a user in taskd](#Adding_a_user_in_taskd)
*   [2 Client](#Client)
    *   [2.1 User configuration](#User_configuration)
    *   [2.2 Using the Android Taskwarrior app](#Using_the_Android_Taskwarrior_app)
*   [3 Troubleshooting](#Troubleshooting)
    *   [3.1 Unreachable Server](#Unreachable_Server)
    *   [3.2 "Bad Key"](#"Bad_Key")
    *   [3.3 taskd.service fails to start on boot](#taskd.service_fails_to_start_on_boot)

## Server

### Installation

taskd is available in the AUR as [taskd](https://aur.archlinux.org/packages/taskd/) and [taskd-git](https://aur.archlinux.org/packages/taskd-git/).

### Setup

Once taskd is installed, you need to set it up. The first step is to `export TASKDDATA=/var/lib/taskd ` (otherwise you need to append `--data /var/lib/taskd` to every taskd command).

Next, edit the `/usr/share/doc/taskd/pki/vars` file. The `CN=` line must either match the server's hostname or IP address, depending on how you connect. Once the file is edited to your heart's content, change to the directory `/usr/share/doc/taskd/pki/` and run `./generate`. This will create selfsigned certificates for your server. Copy all generated *.pem-files to `/var/lib/taskd`. Note that at least the ca.cert.pem must remain in the pki folder for the user-certificate generation later on.

Now you need to configure the taskd config. This can be done by either using `taskd config` or editing `/var/lib/taskd/config` directly.

```
taskd config --force client.cert $TASKDDATA/client.cert.pem
taskd config --force client.key $TASKDDATA/client.key.pem
taskd config --force server.cert $TASKDDATA/server.cert.pem
taskd config --force server.key $TASKDDATA/server.key.pem
taskd config --force server.crl $TASKDDATA/server.crl.pem
taskd config --force ca.cert $TASKDDATA/ca.cert.pem
```

Additionally you should change where taskd logs to, since the default is /tmp/log. This can be done by running

```
touch /var/log/taskd.log
chown taskd:taskd /var/log/taskd.log
taskd config --force log /var/log/taskd.log
```

The last step is to set taskd's server name, which must be the same as the one used in the certificates: `taskd config --force server servername:port`. Note that taskd has no default port and it must be set manually.

### Adding a user in taskd

taskd knows about groups and users, and each user must be in a group. The group- and usernames can be whatever you want.

```
taskd add org group
taskd add user group username
```

Note the key the last command returns, the user will need it to synchronize.

Make sure new group and user are readable by user taskd.

 `chown -R taskd:taskd /var/lib/taskd/orgs` Return to `/usr/share/doc/taskd/pki/` and run `./generate.client username` This will return username.cert.pem and username.key.pem.

The username.key.pem, username.cert.pem and ca.cert.pem must be added to the user's `~/.task` directory.

## Client

### User configuration

Once the *.pem files are added to `~/.task`, they must be added to the task config, along with the servername and unique ID.

```
task config taskd.certificate ~/.task/username.cert.pem
task config taskd.key ~/.task/username.key.pem
task config taskd.ca ~/.task/ca.cert.pem
task config taskd.server servername:port
task config taskd.credentials group/username/key
```

After you're done, check the config file. task likes to escape slashes.

After running a `task sync init`, the user is able to synchronize taskwarrior whereever pleased.

### Using the Android Taskwarrior app

Before you even download the android app, you need to create a folder. On your external storage (or if you only have an internal one, then there) create the folder `Android/data/kvj.taskw/files/key` where "key" is the same as the key given when creating the user in taskd. Then add the username.key.pem, username.cert.pem and ca.cert.pem files to that folder. Create a new file in that folder called `.taskrc.android`. It should look like this:

```
taskd.server=servername:port
taskd.credentials=group/username/key
taskd.certificate=username.cert.pem
taskd.key=username.key.pem
taskd.ca=ca.cert.pem
```

Ensure that the config file `.taskrc.android` has a newline at the end. Otherwise, it will not be parsed correctly.

Now download the app and start it. When adding a profile, choose the datafolder you just created. Taskwarrior should now sync and work as expected.

## Troubleshooting

### Unreachable Server

Should the server be unreachable but running, it bound itself to an IPv6 address. You can force IPv4 by adding `family=IPv4` to `/var/lib/taskd/config`. Restart taskd afterwards.

### "Bad Key"

If the server responds with a "Bad Key" error even though you just generated them, check the permissions of the created folders (everything in `/var/lib/taskd/` and subfolders). taskd doesn't set it's own uid / gid, so those folders must be manually chowned to taskd.

### taskd.service fails to start on boot

In case your systemd unit for taskd fails to start on boot you can add a delay for this particular unit by adding a systemd timer.

Create `/etc/systemd/system/taskd.timer` file. It may look like this:

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