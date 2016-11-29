[rTorrent](https://rakshasa.github.io/rtorrent/) is a quick and efficient BitTorrent client that uses, and is in development alongside, the libTorrent (not to be confused with [libtorrent-rasterbar](https://www.archlinux.org/packages/?name=libtorrent-rasterbar)) library. It is written in C++ and uses the [ncurses](https://en.wikipedia.org/wiki/ncurses "wikipedia:ncurses") programming library, which means it uses a text user interface. When combined with a terminal multiplexer (e.g. [GNU Screen](/index.php/GNU_Screen "GNU Screen") or [Tmux](/index.php/Tmux "Tmux")) and [Secure Shell](/index.php/Secure_Shell "Secure Shell"), it becomes a convenient remote [BitTorrent client](https://en.wikipedia.org/wiki/BitTorrent_(protocol)#Operation "wikipedia:BitTorrent (protocol)").

## Contents

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
    *   [2.1 Performance](#Performance)
    *   [2.2 Create and manage files](#Create_and_manage_files)
    *   [2.3 Port configuration](#Port_configuration)
    *   [2.4 Additional settings](#Additional_settings)
*   [3 Key bindings](#Key_bindings)
    *   [3.1 Redundant mapping](#Redundant_mapping)
*   [4 Additional tips](#Additional_tips)
    *   [4.1 systemd service file with tmux or screen](#systemd_service_file_with_tmux_or_screen)
    *   [4.2 systemd service file with dtach](#systemd_service_file_with_dtach)
    *   [4.3 Pre-allocation](#Pre-allocation)
    *   [4.4 Manage completed files](#Manage_completed_files)
        *   [4.4.1 Notification with Google Mail](#Notification_with_Google_Mail)
    *   [4.5 UI Tricks](#UI_Tricks)
    *   [4.6 Manually adding trackers to torrents](#Manually_adding_trackers_to_torrents)
*   [5 Troubleshooting](#Troubleshooting)
    *   [5.1 CA certificates](#CA_certificates)
    *   [5.2 Locked directories](#Locked_directories)
    *   [5.3 Event failed: bad return code](#Event_failed:_bad_return_code)
*   [6 Web interface](#Web_interface)
    *   [6.1 XMLRPC interface](#XMLRPC_interface)
    *   [6.2 Saving magnet links as torrent files in watch folder](#Saving_magnet_links_as_torrent_files_in_watch_folder)
*   [7 Magnet to Torrent](#Magnet_to_Torrent)
    *   [7.1 In order to use this with an ARM device](#In_order_to_use_this_with_an_ARM_device)
*   [8 rtorrent-pyro](#rtorrent-pyro)
    *   [8.1 PyroScope](#PyroScope)
*   [9 See also](#See_also)

## Installation

[Install](/index.php/Install "Install") the [rtorrent](https://www.archlinux.org/packages/?name=rtorrent) package that is available in the [official repositories](/index.php/Official_repositories "Official repositories").

Alternatively, install the [rtorrent-git](https://aur.archlinux.org/packages/rtorrent-git/) or [rtorrent-vi-color](https://aur.archlinux.org/packages/rtorrent-vi-color/) package.

## Configuration

**Note:**

*   See the rTorrent wiki article on this subject for more information: [Common Tasks in rTorrent for Dummies](http://web.archive.org/web/20140213003955/http://libtorrent.rakshasa.no/wiki/RTorrentCommonTasks).
*   Vim may mistake the syntax of the config file, causing errors in the highlighting. To resolve this you can [append](/index.php/Append "Append") a modeline `# vim: set syntax=conf:` to `~/.rtorrent.rc`.

Before running rTorrent, find the example configuration file `/usr/share/doc/rtorrent/rtorrent.rc` and copy it to `~/.rtorrent.rc`:

```
$ cp /usr/share/doc/rtorrent/rtorrent.rc ~/.rtorrent.rc

```

### Performance

**Note:** See the rTorrent wiki article on this subject for more information: [Performance Tuning](http://web.archive.org/web/20140213011439/http://libtorrent.rakshasa.no/wiki/RTorrentPerformanceTuning)

The values for the following options are dependent on the system's hardware and Internet connection speed. To find the optimal values read: [Optimize Your BitTorrent Download Speed](http://torrentfreak.com/optimize-your-BitTorrent-download-speed)

```
min_peers = 40
max_peers = 52

min_peers_seed = 10
max_peers_seed = 52

max_uploads = 8

download_rate = 200
upload_rate = 28

```

The `check_hash` option executes a hash check when rTorrent is started. It checks for errors in your completed files.

```
check_hash = yes

```

### Create and manage files

The `directory` option will determine where your torrent data will be saved (could be a relative path):

```
directory = ~/downloaded

```

The `session` option allows rTorrent to save the progess of your torrents. It is recommended to create a directory in home directory (e.g. `mkdir ~/.rtorrent.session`).

```
session = ~/.rtorrent.session

```

The `schedule` option has rTorrent watch a particular directory for new torrent files. Saving a torrent file to this directory will automatically start the download. Remember to create the directory that will be watched (e.g. `mkdir ~/watch`). Also, be careful when using this option as rTorrent will move the torrent file to your session folder and rename it to its hash value.

```
schedule = watch_directory,5,5,load_start=/home/*user*/watch/*.torrent
schedule = untied_directory,5,5,stop_untied=
schedule = tied_directory,5,5,start_tied=

```

The following `schedule` option is intended to stop rTorrent from downloading data when disk space is low.

```
schedule = low_diskspace,5,60,close_low_diskspace=100M

```

### Port configuration

The `port_range` option sets which port(s) to use for listening. It is recommended to use a port that is higher than 49152 (see: [List of port numbers](https://en.wikipedia.org/wiki/List_of_TCP_and_UDP_port_numbers "wikipedia:List of TCP and UDP port numbers")). Although, rTorrent allows a range of ports, a single port is recommended.

```
port_range = 49164-49164

```

Additionally, make sure port forwarding is enabled for the proper port(s) (see: [Port Forward guides](http://portforward.com/english/routers/port_forwarding/routerindex.htm)).

### Additional settings

The `encryption` option enables or disables encryption. It is very important to enable this option, not only for yourself, but also for your peers in the torrent swarm. Some users need to obscure their bandwidth usage from their ISP. And it does not hurt to enable it even if you do not need the added security.

```
encryption = allow_incoming,try_outgoing,enable_retry

```

It is also possible to force all connections to use encryption. However, be aware that this stricter rule will reduce your client's availability:

```
encryption = require,require_RC4,allow_incoming,try_outgoing

```

See also [Wikipedia:BitTorrent Protocol Encryption](https://en.wikipedia.org/wiki/BitTorrent_Protocol_Encryption "wikipedia:BitTorrent Protocol Encryption").

This final `dht` option enables [DHT](https://en.wikipedia.org/wiki/Distributed_hash_table "wikipedia:Distributed hash table") support. DHT is common among public trackers and will allow the client to acquire more peers.

```
dht = auto
dht_port = 6881
peer_exchange = yes

```

## Key bindings

rTorrent relies exclusively on keyboard shortcuts for user input. A quick reference is available in the table below. A complete guide is available on the rTorrent wiki (see: [rTorrent User Guide](https://github.com/rakshasa/rtorrent/wiki/User-Guide)).

**Note:** Striking `Ctrl-q` twice in quick succession will make rTorrent shutdown without waiting to send a stop announce to the connected trackers.

| Cmd | Action |
| Ctrl-q | Quit application |
| Ctrl-s | Start download. Runs hash first unless already done. |
| Ctrl-d | Stop an active download or remove a stopped download |
| Ctrl-k | Stop and close the files of an active download. |
| Ctrl-r | Initiate hash check of torrent. Starts downloading if file is not available. |
| Ctrl-o | Specify the download directory for a added, but not started torrent. |
| Left | Returns to the previous screen |
| Right | Goes to the next screen |
| Backspace | Adds and starts the specified *.torrent |
| Return | Adds and doesn't start the specified *.torrent |
| a|s|d | Increase global upload throttle about 1|5|50 KB/s |
| A|S|D | Increase global download throttle about 1|5|50 KB/s |
| z|x|c | Decrease global upload throttle about 1|5|50 KB/s |
| Z|X|C | Decrease global download throttle about 1|5|50 KB/s |

### Redundant mapping

`Ctrl-s` is often used for terminal control to stop screen output while `Ctrl-q` is used to start it. These mappings may interfere with rTorrent. Check to see if these terminal options are bound to a mapping:

 `$ stty -a` 
```
...
swtch = <undef>; start = ^Q; stop = ^S; susp = ^Z; rprnt = ^R; werase = ^W; lnext = ^V;
...

```

To remove the mappings, change the terminal characteristics to undefine the aforementioned special characters (i.e. `stop` and `start`):

```
# stty stop undef
# stty start undef

```

To remove these mappings automatically at startup you may add the two preceding commands to your `~/.bashrc` file.

## Additional tips

### systemd service file with tmux or screen

*   With independent tmux server (restart rtorrent if crashed)

 `~/.config/systemd/user/rt.service` 
```
[Unit]
Description=rtorrent
After=network.target

[Service]
Type=forking
ExecStartPre=/usr/bin/bash -c "if test -e ~/.session/rtorrent.lock && test -z `pidof rtorrent`; then rm -f ~/.session/rtorrent.lock; fi"
ExecStart=/usr/bin/tmux -L rt new-session -s rt -n rtorrent -d rtorrent 
ExecStop=/usr/bin/bash -c "/usr/bin/tmux -L rt send-keys -t rt:rtorrent.0 C-q; while pidof rtorrent > /dev/null; do echo stopping rtorrent...; sleep 1; done"
Restart=on-failure

[Install]
WantedBy=default.target

```

*   With tmux running as user rtorrent (restart rtorrent if crashed)

 `/etc/systemd/system/rtorrent.service` 
```
[Unit]
Description=rTorrent Daemon
After=network.target

[Service]
Type=forking
KillMode=none
User=rtorrent
ExecStart=/usr/bin/tmux new-session -c /mnt/storage/rtorrent -s rtorrent -n rtorrent -d rtorrent
ExecStop=/usr/bin/bash -c "/usr/bin/tmux send-keys -t rtorrent C-q && while pidof rtorrent > /dev/null; do sleep 0.5; done"
WorkingDirectory=/home/rtorrent/
Restart=on-failure

[Install]
WantedBy=multi-user.target

```

*   With screen

 `/etc/systemd/user/rt.service` 
```
[Unit]
Description=rTorrent
After=network.target

[Service]
Type=forking
KillMode=none
ExecStart=/usr/bin/screen -d -m -fa -S rtorrent /usr/bin/rtorrent
ExecStop=/usr/bin/killall -w -s 2 /usr/bin/rtorrent
WorkingDirectory=%h

[Install]
WantedBy=default.target

```

Start at boot time:

```
$ systemctl --user enable rt

```

Start manually:

```
$ systemctl --user start rt

```

Stop:

```
$ systemctl --user stop rt

```

Attach to rtorrent's session:

```
tmux -L rt attach -t rt
tmux attach -t rt

```

Or if you use screen:

```
screen -D -r rtorrent

```

Detach:

```
Ctrl-b d

```

Or if you use screen:

```
Ctrl-a d

```

### systemd service file with dtach

When running dtach from systemd unit, the `TERM` environment variable [has to be set explicitly](/index.php/Systemd/User#Environment_variables "Systemd/User") for rtorrent to work.

This service file has no restart because the author occasionally takes the drive in question offline, and rtorrent fails, shall we say, "suboptimally" when started in this scenario and loses many torrent specific settings such as the specific directories each torrent is stored in. In fact the symlinks that kick off rtorrent live on the relevant drive; if it is unmounted rtorrent cannot start. This use case of blocking rtorrent from starting is relevant to users who put the downloaded files on removable media such as NAS, USB or eSATA drives.

 `~/.config/systemd/user/rtorrent.service` 
```
[Unit]
Description=rTorrent
#After=network.target

[Service]
# set TERM according to your terminal
Environment="TERM=xterm"
#Environment="TERM=linux" 
Type=forking
KillMode=none
ExecStart=-/usr/bin/dtach -n /home/sam/run/dtach_fifos/fifo -e "^T" /home/sam/bin/rtr_new -n -o import=/home/sam/.config/rtorrent/new_.rc 
   # dtach -n <separate filename for each instance>
   # 
   # rtr_new -n to ignore the default .rtorrent.rc
   # rtr_new -o import to load the instance-specific rc
ExecStop=-/usr/bin/killall -u sam -e -w -s INT /home/sam/bin/rtr_new

[Install]
WantedBy=multi-user.target

```

Note some other issues exposed in this service file other than just dtach:

`/home/sam/bin/rtr_new` is a symlink to `/usr/bin/rtorrent`

This lets us run several instances and kill each one independently with a different version of the ExecStop, to wit:

```
ExecStop=-/usr/bin/killall -u sam -e -w -s INT /home/sam/bin/rtr_new
ExecStop=-/usr/bin/killall -u sam -e -w -s INT /home/sam/bin/rtr_academic
ExecStop=-/usr/bin/killall -u sam -e -w -s INT /home/sam/bin/rtr_other_stuff
```

These are each in a different service file, each of which controls one instance.

Without this step, when running multiple instances a killall solution would kill all the running rtorrent instances.

If multiple rtorrent instances are not needed and the rtorrent rc file is in the default location the above service file may be simplified. The entire file is included but only the ExecStart and ExecStop lines change.

 `~/.config/systemd/user/rtorrent.service` 
```
[Unit]
Description=rTorrent
#After=network.target

[Service]
# set TERM according to your terminal
Environment="TERM=xterm"
#Environment="TERM=linux" 
Type=forking
KillMode=none
ExecStart=-/usr/bin/dtach -n /home/sam/run/dtach_fifos/fifo -e "^T" /usr/bin/rtorrent 
   # dtach -n <user specified FIFO name> -e <user specified character> /usr/bin/rtorrent 
ExecStop=/usr/bin/killall -w -s INT /usr/bin/rtorrent
   # -e (exact match) and -u (user name) were added above to stop specific processes
   #  and may be omitted here because only one rtorrent will be running

[Install]
WantedBy=multi-user.target

```

The service can be controlled with [systemctl --user](/index.php/Systemctl_--user "Systemctl --user"). When it is started, you can attach to the session:

```
$ dtach -a  /home/sam/run/dtach_fifos/fifo -e "^T"

```

### Pre-allocation

The rTorrent package in the community repository lacks pre-allocation. Compiling rTorrent with pre-allocation allows files to be allocated before downloading the torrent. The major benefit is that it limits and avoids fragmentation of the filesystem. However, this introduces a delay during the pre-allocation if the filesystem does not support the fallocate syscall natively.

Therefore this switch is recommended for xfs, ext4 and btrfs filesystems, which have native fallocate syscall support. They will see no delay during preallocation and no fragmented filesystem. Pre-allocation on others filesystems will cause a delay but will not fragment the files.

To make pre-allocation available, recompile libTorrent from the [ABS](/index.php/ABS "ABS") tree with the following new switch:

```
 $ ./configure --prefix=/usr --disable-debug --with-posix-fallocate

```

To enable it, add the following to your `~/rtorrent.rc`:

 `~/rtorrent.rc` 
```
  # Preallocate files; reduces defragmentation on filesystems.
  system.file_allocate.set = yes

```

### Manage completed files

**Note:**

*   Currently, this part requires either the git version of rtorrent/libtorrent or having applied the patch to 0.8.6 that adds 'equal'.
*   If you are having trouble with this tip, it is probably easier to follow [this](http://web.archive.org/web/20140213003955/http://libtorrent.rakshasa.no/wiki/RTorrentCommonTasks#Movecompletedtorrentstodifferentdirectorydependingonwatchdirectory).

It is possible to have rtorrent sort completed torrent data to specific folders based on which 'watch' folder you drop the *.torrent into while continuing to seed. Many examples show how to do this with torrents downloaded by rtorrent. The problem is when you try to drop in 100% done torrent data and then have rtorrent check the data and resume, it will not be sorted.

As a solution, use the following example in your `~/.rtorrent.rc`. Make sure to change the paths.

```
# location where new torrent data is placed, and where you should place your
# 'complete' data before you place your *.torrent file into the watch folder
directory = /home/user/torrents/incomplete

# schedule a timer event named 'watch_directory_1':
# 1) triggers 10 seconds after rtorrent starts
# 2) triggers at 10 second intervals thereafter
# 3) Upon trigger, attempt to load (and start) new *.torrent files found in /home/user/torrents/watch/
# 4) set a variable named 'custom1' with the value "/home/user/torrents/complete"
# NOTE: if you do not want it to automatically start the torrent, change 'load_start' to 'load'
schedule = watch_directory_1,10,10,"load_start=/home/user/torrents/watch/*.torrent,d.set_custom1=/home/user/torrents/complete"

# insert a method with the alias 'checkdirs1'
# 1) returns true if the current path of the torrent data is not equal to the value of custom1
# 2) otherwise, returns false
system.method.insert=checkdirs1,simple,"not=\"$equal={d.get_custom1=,d.get_base_path=}\""

# insert a method with the alias 'movecheck1'
# 1) returns true if all 3 commands return true ('result of checkdirs1' && 'torrent is 100% done', 'custom1 variable is set')
# 2) otherwise, returns false
system.method.insert=movecheck1,simple,"and={checkdirs1=,d.get_complete=,d.get_custom1=}"

# insert a method with the alias 'movedir1'
# (a series of commands, separated by ';') 
# 1) "set path of torrent to equal the value of custom1";
# 2) "mv -u <current data path> <custom1 path>";
# 3) "clear custom1", "stop the torrent","resume the torrent"
# 4) stop the torrent
# 5) start the torrent (to get the torrent to update the 'base path')
system.method.insert=movedir1,simple,"d.set_directory=$d.get_custom1=;execute=mv,-u,$d.get_base_path=,$d.get_custom1=;d.set_custom1=;d.stop=;d.start="

# set a key with the name 'move_hashed1' that is triggered by the hash_done event.
# 1) When hashing of a torrent completes, this custom key will be triggered.
# 2) when triggered, execute the 'movecheck1' method and check the return value.
# 3) if the 'movecheck' method returns 'true', execute the 'movedir1' method we inserted above.
# NOTE-0: *Only* data that has had their hash checked manually with ^R [^R = Control r].
# Or on a rtorrent restart[which initiates a hash check]. Will the data move; ~/torrents/incomplete => ~/torrents/complete for example.
# NOTE-1: 'branch' is an 'if' conditional statement: if(movecheck1){movedir1}
system.method.set_key=event.download.hash_done,move_hashed1,"branch={$movecheck1=,movedir1=}"
```

You can add additional watch folders and rules should you like to sort your torrents into special folders.

For example, if you would like the torrents to download in:

```
/home/user/torrents/incomplete

```

and then sort the torrent data based on which folder you dropped the *.torrent into:

```
/home/user/torrents/watch => /home/user/torrents/complete
/home/user/torrents/watch/iso => /home/user/torrents/complete/iso
/home/user/torrents/watch/music => /home/user/torrents/complete/music

```

You can have the following in your .rtorrent.rc:

```
directory = /home/user/torrents/incomplete
schedule = watch_directory_1,10,10,"load_start=/home/user/torrents/watch/*.torrent,d.set_custom1=/home/user/torrents/complete"

schedule = watch_directory_2,10,10,"load_start=/home/user/torrents/watch/iso/*.torrent,d.set_custom1=/home/user/torrents/complete/iso"

schedule = watch_directory_3,10,10,"load_start=/home/user/torrents/watch/music/*.torrent,d.set_custom1=/home/user/torrents/complete/music"

system.method.insert=checkdirs1,simple,"not=\"$equal={d.get_custom1=,d.get_base_path=}\""
system.method.insert=movecheck1,simple,"and={checkdirs1=,d.get_complete=,d.get_custom1=}"
system.method.insert=movedir1,simple,"d.set_directory=$d.get_custom1=;execute=mv,-u,$d.get_base_path=,$d.get_custom1=;d.set_custom1=;d.stop=;d.start="
system.method.set_key=event.download.hash_done,move_hashed1,"branch={$movecheck1=,movedir1=}"
```

Also see [pyroscope](http://code.google.com/p/pyroscope/) especially the rtcontrol examples. There is an AUR package.

#### Notification with Google Mail

Cell phone providers allow you to "email" your phone:

```
Verizon: 10digitphonenumber@vtext.com
AT&T: 10digitphonenumber@txt.att.net
Former AT&T customers: 10digitphonenumber@mmode.com
Sprint: 10digitphonenumber@messaging.sprintpcs.com
T-Mobile: 10digitphonenumber@tmomail.net
Nextel: 10digitphonenumber@messaging.nextel.com
Cingular: 10digitphonenumber@cingularme.com
Virgin Mobile: 10digitphonenumber@vmobl.com
Alltel: 10digitphonenumber@alltelmessage.com OR
10digitphonenumber@message.alltel.com
CellularOne: 10digitphonenumber@mobile.celloneusa.com
Omnipoint: 10digitphonenumber@omnipointpcs.com
Qwest: 10digitphonenumber@qwestmp.com
Telus: 10digitphonenumber@msg.telus.com
Rogers Wireless: 10digitphonenumber@pcs.rogers.com
Fido: 10digitphonenumber@fido.ca
Bell Mobility: 10digitphonenumber@txt.bell.ca
Koodo Mobile: 10digitphonenumber@msg.koodomobile.com
MTS: 10digitphonenumber@text.mtsmobility.com
President's Choice: 10digitphonenumber@txt.bell.ca
Sasktel: 10digitphonenumber@sms.sasktel.com
Solo: 10digitphonenumber@txt.bell.ca

```

*   Install mailx which is provided by the [s-nail](https://www.archlinux.org/packages/?name=s-nail) package that is found in the [official repositories](/index.php/Official_repositories "Official repositories").

*   Clear the `/etc/mail.rc` file and enter:

```
set sendmail="/usr/bin/mailx"
set smtp=smtp.gmail.com:587
set smtp-use-starttls
set ssl-verify=ignore
set ssl-auth=login
set smtp-auth-user=USERNAME@gmail.com
set smtp-auth-password=PASSWORD

```

Now to send the text, we must pipe a message to the mailx program.

*   Make a Bash script:

 `/path/to/mail.sh` 
```
echo "$@: Done" | mailx 5551234567@vtext.com

```

Where the $@ is a variable holding all the arguments passed to our script.

*   And finally, add the important `~/.rtorrent.rc` line:

```
system.method.set_key = event.download.finished,notify_me,"execute=/path/to/mail.sh,$d.get_name="

```

Breaking it down:

`notify_me` is the command id, which may be used by other commands, it can be just about anything you like, so long as it is unique.

`execute=` is the rtorrent command, in this case to execute a shell command.

`/path/to/mail.sh` is the name of our script (or whatever command you want to execute) followed by a comma separated list of all the switches/arguments to be passed.

`$d.get_name=` 'd' is an alias to whatever download triggered the command, get_name is a function which returns the name of our download, and the '$' tells rTorrent to replace the command with its output before it calls execute.

The end result? When that torrent, 'All Live Nudibranches', that we started before leaving for work finishes, we will be texted:

```
All Live Nudibranches: Done

```

### UI Tricks

rTorrent does not list the active tab properly by default, add this line to your `.rtorrent.rc` to show only active torrents

```
schedule = filter_active,30,30,"view_filter = active,\"or={d.get_up_rate=,d.get_down_rate=}\""

```

Then press `9` in your rTorrent client to see the changes in action.

To sort the seeding view by the upload rate and only show torrents with peers:

```
# Sort the seeding view by the upload rate and only show torrents with peers
view.sort_current = seeding,greater=d.get_up_rate=
view.filter = seeding,"and=d.get_complete=,d.get_peers_connected="
view.sort_new = seeding,less=d.get_up_rate=
view.sort = seeding

```

To sort the complete view by the upload rate:

```
# Sort the complete view by the upload rate
view.sort_current = complete,greater=d.get_up_rate=
view.filter = seeding,"and=d.get_complete="
view.sort_new = seeding,less=d.get_up_rate=
view.sort = seeding

```

### Manually adding trackers to torrents

1.  Select torrent to edit from rTorrent console view.
2.  Hit `Ctrl+x`.
3.  If you had four trackers type following lines one at a time (always press `Ctrl+x` first) to add four more for example:

```
d.tracker.insert="5","udp://tracker.publicbt.com:80"
d.tracker.insert="6","udp://tracker.openbittorrent.com:80"
d.tracker.insert="7","udp://tracker.istole.it:80"
d.tracker.insert="8","udp://tracker.ccc.de:80"

```

## Troubleshooting

### CA certificates

To use rTorrent with a tracker that uses HTTPS, do the following as root:

```
# cd /etc/ssl/certs
# wget --no-check-certificate https://www.geotrust.com/resources/root_certificates/certificates/Equifax_Secure_Global_eBusiness_CA-1.cer
# mv Equifax_Secure_Global_eBusiness_CA-1.cer Equifax_Secure_Global_eBusiness_CA-1.pem
# c_rehash

```

And from now on run rTorrent with:

```
$ rtorrent -o http_capath=/etc/ssl/certs

```

If you use GNU Screen, update the `.screenrc` configuration file to reflect this change:

```
$ screen -t rtorrent rtorrent -o http_capath=/etc/ssl/certs

```

In rTorrent 0.8.9, set `network.http.ssl_verify_peer.set=0` to [fix the problem](https://bbs.archlinux.org/viewtopic.php?pid=981832#p981832).

For more information see: [rTorrent Error & CA Certificate](https://bbs.archlinux.org/viewtopic.php?pid=331850) and [rTorrent Certificates Problem](https://bbs.archlinux.org/viewtopic.php?id=45800)

### Locked directories

rTorrent can sometimes lock up after a crash or incorrect shutdown, and will complain about a lock file.

Per the error message, the file called "**rtorrent.lock**" can be found within the hidden folder `.rtorrentsession` for your download directory and manually removed.

### Event failed: bad return code

This is caused by there being spaces in your system.method.* lines. Remove the spaces and it will work.

## Web interface

There are numerous web interfaces and front ends for rTorrent including:

*   [WTorrent](/index.php/WTorrent "WTorrent") is a web interface to rtorrent programmed in php using Smarty templates and XMLRPC for PHP library.
*   [nTorrent](http://code.google.com/p/ntorrent/) is a graphical user interface client to rtorrent written in Java.
*   [rTWi](https://rtwi.jmk.hu/) is a simple rTorrent web interface written in PHP.
*   [Rtgui](/index.php/Rtgui "Rtgui") is a web based front end for rTorrent written in PHP and uses XML-RPC to communicate with the rTorrent client.
*   [rutorrent](https://github.com/Novik/ruTorrent) and [Forum](http://forums.rutorrent.org/) - A web-based front-end with an interface very similar to uTorrent which supports many plugins and advanced features (see also: [ruTorrent](/index.php/RuTorrent "RuTorrent") and [Guide on forum](https://bbs.archlinux.org/viewtopic.php?pid=897577#p897577)).

**Note:** rTorrent is currently built using [XML-RPC for C/C++](http://xmlrpc-c.sourceforge.net/), which is required for some web interfaces (e.g. ruTorrent).

### XMLRPC interface

If you want to use rtorrent with some web interfaces (e.g. rutorrent) you need to add the following line to the configuration file:

```
scgi_port = localhost:5000

```

For more information see: [Using XMLRPC with rtorrent](https://github.com/rakshasa/rtorrent/wiki/RPC-Setup-XMLRPC)

### Saving magnet links as torrent files in watch folder

**Note:** Rtorrent natively supports downloading torrents through magnet links. At the main view (reached by starting Rtorrent and pressing 1), press enter. At "load.normal>" paste the magnet link and press enter again. This will start the download.

If you wish to have magnet links automatically added to your watch folder, here is a script that will do the trick:

```
 #!/bin/bash
 watch_folder=~/.rtorrent/watch
 cd $watch_folder
 [[ "$1" =~ xt=urn:btih:([^&/]+) ]] || exit;
 echo "d10:magnet-uri${#1}:${1}e" > "meta-${BASH_REMATCH[1]}.torrent"

```

(adapted from [http://blog.gonzih.org/blog/2012/02/17/how-to-use-magnet-links-with-rtorrent/](http://blog.gonzih.org/blog/2012/02/17/how-to-use-magnet-links-with-rtorrent/)).

Save it, for instance as rtorrent-magnet, give it execution permission, and place it somewhere under your $PATH. Then in Firefox:

1.  Type `about:config` into the Location Bar (address bar) and press `Enter`.
2.  Right-click: *New > Boolean > Name: **network.protocol-handler.expose.magnet** > Value > false*.
3.  Next time you click a magnet link you will be asked which application to open it with. Select the script we just created and you will be done.

If you want xdg-open to handle this, which you need if you are using chrome instead of firefox, (though gnome and other DE might have their own programs overriding xdg-open) you need to create the desktop entry for the rtorrent-magnet script in `~/.local/share/applications/rtorrent-magnet.desktop` with the following content:

```
 [Desktop Entry]
 Type=Application
 Name=rtorrent-magnet
 Exec=rtorrent-magnet %U
 MimeType=x-scheme-handler/magnet;
 NoDisplay=true

```

Then all you need to do is to register the mimetype using

```
$ xdg-mime default rtorrent-magnet.desktop x-scheme-handler/magnet

```

## Magnet to Torrent

You could also use the [magnet2torrent-git](https://aur.archlinux.org/packages/magnet2torrent-git/) package which downloads the metadata and creates a torrent file.

How to use:

```
$ magnet2torrent <magnet link> [torrent file]

```

#### In order to use this with an ARM device

You should have package versions

```
python-libtorrent-rasterbar 1.0.8-1
libtorrent-rasterbar 1:1.0.9-1

```

Then you can compile magnet2torrent-git package.

## rtorrent-pyro

[rtorrent-pyro-git](https://aur.archlinux.org/packages/rtorrent-pyro-git/) from the [AUR](/index.php/AUR "AUR") comes with an extended rtorrent console interface. It does not contain the pyroscope tools yet though. If you also need the pyroscope tools see [#PyroScope](#PyroScope) .

Make sure you add following command to ~/.rtorrent.rc, which makes the asterisk key * to a shortcut for toggling between extended and collapsed view within rtorrent's interface:

 `schedule = bind_collapse,0,0,"ui.bind_key=download_list,*,view.collapsed.toggle="` 

Also set "pyro.extended" to 1 to activate rTorrent-PS features.

 `system.method.insert = pyro.extended, value|const, 1` 
**Note:** You may notice that some systemd service scripts for rtorrent do not work with rtorrent-ps installed. If you are using tmux or screen this may because it is exiting with the error, "your terminal only supports 8 colors". To fix this make sure your tmux/screen config sets the TERM variable to a 256 color variant, or change your rtorrent theme to an 8 color one such as [https://github.com/pyroscope/rtorrent-ps/blob/master/docs/examples/color_scheme8.rc](https://github.com/pyroscope/rtorrent-ps/blob/master/docs/examples/color_scheme8.rc).

### PyroScope

We create a directory for the installation of pyroscope, then download and update the source code from subversion:

```
mkdir -p ~/.lib
git clone "https://github.com/pyroscope/pyrocore.git" ~/.lib/pyroscope
~/.lib/pyroscope/update-to-head.sh
```

Adding pyroscope bin's PATH to .bashrc:

 `export PATH=$PATH:path_to_the_bin      # Example path for pyroscope bin's: /home/user/.lib/pyroscope/bin/` 

Creating the ~/.pyroscope/config.ini:

 `pyroadmin --create-config` 

Add this to your ~/.rtorrent.rc. Do not forget to add the path of your pyroscope bin's dir (see below).

```
system.method.insert = pyro.bin_dir, string|const, write_here_path_to_your_pyroscope_bin_dir     # Example path: /home/user/.lib/pyroscope/bin/
system.method.insert = pyro.rc_dialect, string|const|simple, "execute_capture=bash,-c,\"test $1 = 0.8.6 && echo -n 0.8.6 || echo -n 0.8.9\",dialect,$system.client_version="
system.method.insert = pyro.rtorrent_rc, string|const|private, "$cat=~/.pyroscope/rtorrent-,\"$pyro.rc_dialect=\",.rc.default"
import = $pyro.rtorrent_rc=
```

Optionally: TORQUE: Daemon watchdog schedule. Must be activated by touching the "~/.pyroscope/run/pyrotorque" file! You can also just use rtorrent watch dir or give pyro_watchdog a try, which comes with 'treewatch' ability, meaning it also watches for torrents recursively within the given watch path. Further documentation for pyro_watchdog is here: [[1]](http://code.google.com/p/pyroscope/wiki/QueueManager) To enable pyro_watchdog, add this in ~/.rtorrent.rc and further configurations are in ~/.pyroscope/torque.ini.

 `schedule = pyro_watchdog,30,300,"pyro.watchdog=~/.pyroscope,-v"` 

Following steps are important. Before using pyroscope tools you have to set the missing "loaded" times to that of the .torrent file. Run this in your terminal:

```
rtcontrol '!*"*' loaded=0 -q -sname -o 'echo "$(name)s"
test -f "$(metafile)s" && rtxmlrpc -q d.set_custom $(hash)s tm_loaded \$(\
    ls -l --time-style "+%%s" "$(metafile)s" \
    | cut -f6 -d" ")
rtxmlrpc -q d.save_session $(hash)s' | bash
```

And now set the missing "completed" times to that of the data file or directory:

```
rtcontrol '!*"*' completed=0 done=100 path=\! is_ghost=no -q -sname -o 'echo "$(name)s"
test -e "$(realpath)s" && rtxmlrpc -q d.set_custom $(hash)s tm_completed \$(\
    ls -ld --time-style "+%%s" "$(realpath)s" \
    | cut -f6 -d" ")
rtxmlrpc -q d.save_session $(hash)s' | bash
```

Example usage: Will print out all torrents older than 2 hours:

 `rtcontrol -V completed=+2h -scompleted -ocompleted` 

Deletes all torrents older than 48 hours:

 `rtcontrol -V completed=+48h -scompleted -ocompleted --cull --yes` 

## See also

*   [Manpage for rtorrent](http://linux.die.net/man/1/rtorrent)
*   [Screen Tips](/index.php/Screen_Tips "Screen Tips")
*   [Comparison of BitTorrent clients](https://en.wikipedia.org/wiki/Comparison_of_BitTorrent_clients "wikipedia:Comparison of BitTorrent clients") on Wikipedia
*   [rTorrent Community Wiki](http://community.rutorrent.org/) - Public place for information on rTorrent and any project related to rTorrent, regarding setup, configuration, operations, and development.
*   [PyroScope](http://code.google.com/p/pyroscope/) - Collection of command line tools for rTorrent. It provides commands for creating and modifying torrent files, moving data on completion without having multiple watch folders, and mass-controlling download items via rTorrent's XML-RPC interface: searching, start/stop, deleting items with or without their data, etc. It also offers a documented [Python](/index.php/Python "Python") API.
*   [ruTorrent with Lighttpd](/index.php/Rutorrent_with_lighttpd "Rutorrent with lighttpd")
*   [How-to install rTorrent and Hellanzb on CentOS 5 64-bit VPS](http://wiki.theaveragegeek.com/howto/installing_rtorrent_and_hellanzb_on_centos5_64-bit_vps)
*   [Installation guide for rTorrent and Pyroscope on Debian](http://code.google.com/p/pyroscope/wiki/DebianInstallFromSource) - Collection of tools for the BitTorrent protocol and especially the rTorrent client
*   [mktorrent](http://mktorrent.sourceforge.net/) - Command line application used to generate torrent files, which is available as [mktorrent](https://www.archlinux.org/packages/?name=mktorrent) in the [official repositories](/index.php/Official_repositories "Official repositories").
*   [docktorrent](https://github.com/kfei/docktorrent) - Using Docker, rTorrent and ruTorrent to run a full-featured BitTorrent box.
*   [reptyr](https://github.com/nelhage/reptyr) - another tool to take over a program's TTY (it is in the standard repos). The process may have started being attached to a terminal or to a socket in tmux, screen or dtach.
*   [neercs](http://caca.zoy.org/wiki/neercs) - a more screen/tmux like tool than reptyr, but, like reptyr, neercs can also "steal" a process that may have started slaved to a terminal or to a socket in tmux, screen or dtach. [neercs-git](https://aur.archlinux.org/packages/neercs-git/)

**Forum threads**

*   2009-03-11 - Arch Linux - [HOWTO: rTorrent stats in Conky](https://bbs.archlinux.org/viewtopic.php?id=67304)