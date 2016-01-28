# Fsniper

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

[![Tango-dialog-warning.png](/images/d/d8/Tango-dialog-warning.png)](/index.php/File:Tango-dialog-warning.png)

[![Tango-dialog-warning.png](/images/d/d8/Tango-dialog-warning.png)](/index.php/File:Tango-dialog-warning.png)

**This article or section is out of date.**

**Reason:** [initscripts](/index.php?title=Initscripts&action=edit&redlink=1 "Initscripts (page does not exist)") has been superseded by [systemd](/index.php/Systemd "Systemd") (Discuss in [Talk:Fsniper#](https://wiki.archlinux.org/index.php/Talk:Fsniper))

[![Tango-two-arrows.png](/images/7/72/Tango-two-arrows.png)](/index.php/File:Tango-two-arrows.png)

[![Tango-two-arrows.png](/images/7/72/Tango-two-arrows.png)](/index.php/File:Tango-two-arrows.png)

**This article or section is a candidate for merging with [List of applications](/index.php/List_of_applications "List of applications").**

**Notes:** no content of note (Discuss in [Talk:Fsniper#](https://wiki.archlinux.org/index.php/Talk:Fsniper))

Fsniper is a directory monitor that can be used to execute predefined actions on files that enter the monitored directory. This can, for example, be used to monitor your downloads folder and sort downloaded files automatically into your file system.

Unlike cron jobs or bash scripts, fsniper uses [inotify](https://en.wikipedia.org/wiki/inotify "wikipedia:inotify") to monitor file changes. This enable it to react immediately and efficiently to changes of the file system.

## Installation

[fsniper](https://aur.archlinux.org/packages/fsniper/)<sup><small>AUR</small></sup> is available from the [AUR](/index.php/AUR "AUR").

## Configuration

Fsniper comes with a self-explanatory example.conf found in /usr/share/sniper/ that can be copied to `~/.config/fsniper/config` for modification and personalisation.

```
 watch {
   # watch the ~/drop directory for new files
   ~/drop {
       # matches any mimetype beginning with image/
       image/* {
           # %% is replaced with the filename of the new file
           handler = echo found an image: %%
       }
       # matches any file ending with .extension
       *.extension {
           # the filename is added to the end of the handler line if %% is not present
           handler = echo glob handler 1: 
           # the second handler will be run if the first exits with a return code of 1
           handler = echo glob handler 2: %%
       }
       # run handlers on files that match this regex
       /.*regex.*/ {
           handler = echo regex handler
       }
       # generic handler to catch files that nothing else did
       * {
           handler = mv %% ~/downloads/
       }
   }
 }

```

Once configured, fsniper can be started by typing

```
 $ fsniper --daemon

```

## Daemonizing

Fsniper can also be started automatically at [boot](/index.php/Boot "Boot") time as an rc.d [daemon](/index.php/Daemon "Daemon") by placing the following script as `/etc/rc.d/fsniper`:

(Replace <your-user-name> with your user name(s))

```
 daemon_name=fsniper
 . /etc/rc.conf
 . /etc/rc.d/functions
 USERS=( '<your-user-name>' )
 for USER in ${USERS[@]}
 do
 	PID=$(pidof -o %PPID /usr/bin/fsniper)
 	case "$1" in
 	  start)
 		  stat_busy "Starting $daemon_name"
 		  [ -z "$PID" ] && su -c "/usr/bin/fsniper --daemon" $USER
 		  if [ $? -gt 0 ]; then
 			  stat_fail
 		  else
 			  add_daemon fsniper
 			  stat_done
 		  fi
 		  ;;
 	  stop)
 		  stat_busy "Stopping $daemon_name"
 		  [ ! -z "$PID" ] && kill $PID > /dev/null
 		  if [ $? -gt 0 ]; then
 			  stat_fail
 		  else
 			  rm_daemon fsniper
 			  stat_done
 		  fi
 		  ;;
 	  restart)
 		  $0 stop
 		  sleep 1
 		  $0 start
 		  ;;
 	  *)
   echo "usage: $0 {start|stop|restart}"
 esac
 done
 exit 0

```

The daemon can then be started by typing

```
 # rc.d start fsniper

```

or by placing fsniper in the daemons section of your [`/etc/rc.conf`](/index.php/Rc.conf "Rc.conf").

Retrieved from "[https://wiki.archlinux.org/index.php?title=Fsniper&oldid=399035](https://wiki.archlinux.org/index.php?title=Fsniper&oldid=399035)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [File systems](/index.php/Category:File_systems "Category:File systems")

Hidden categories:

*   [Pages or sections flagged with Template:Out of date](/index.php/Category:Pages_or_sections_flagged_with_Template:Out_of_date "Category:Pages or sections flagged with Template:Out of date")
*   [Pages or sections flagged with Template:Merge](/index.php/Category:Pages_or_sections_flagged_with_Template:Merge "Category:Pages or sections flagged with Template:Merge")