## Quick draft on how to switch active windows using krunner

Plasma 5 doesn't contain default way to specify krunner search only by active window titles. Following approaches are used to work around this issue.

#### Full list of windows with search by titles

This approach will require `xdotool` installed.

1.  Go to System Settings -> Workspace -> Shortcuts -> Custom Shortcuts
2.  Create new Global shortcut -> Command/URL (by right click)
3.  Tick the checkbox to the right of the name
4.  In Trigger tab select desired key combination
5.  In Action tab type `/usr/local/bin/krunner-search-by-windows.sh`
6.  Create file `/usr/local/bin/krunner-search-by-windows.sh` with following content:

```
   #!/bin/bash
   qdbus org.kde.krunner /App querySingleRunner windows "" 
   sleep 0.4
   xdotool type 'window '
   xdotool key "shift+BackSpace"

```

1.  Make file executable and give run permission to all

```
  chmod a+x /usr/local/bin/krunner-search-by-windows.sh

```

Note the space after 'window'.

Now you're able to get list of opened windows by specified shortcut and search by this list as you type;

#### Search by titles without full windows list

This approach is more limited but far less ugly.

1.  Go to System Settings -> Workspace -> Shortcuts -> Custom Shortcuts
2.  Create new Global shortcut -> D-bus Command (by right click)
3.  Tick the checkbox to the right of the name
4.  In Trigger tab select desired key combination
5.  In Action tab insert following information:

```
  - Remote application : org.kde.krunner
  - Remote Object      : /App
  - Function           : querySingleRunner
  - Arguments          : windows ""

```

1.  Done