Related articles

*   [KDE](/index.php/KDE "KDE")

Krunner is an application built into Plasma 5 to perform functions and run commands quickly, and features a "runner" system to customize functions available for use.

## Contents

*   [1 Installation](#Installation)
*   [2 Usage](#Usage)
*   [3 Switch active windows using Krunner](#Switch_active_windows_using_Krunner)
    *   [3.1 Full list of windows with search by titles](#Full_list_of_windows_with_search_by_titles)
    *   [3.2 Search by titles without full windows list](#Search_by_titles_without_full_windows_list)
*   [4 See also](#See_also)

## Installation

For installation instructions regarding Plasma, see [KDE](/index.php/KDE "KDE").

## Usage

To open Krunner in Plasma, you can either right-click the desktop and press "run command", or you can use the default keybindings, `Alt+Space` or `Alt+F2`. In some workspaces such as a blank desktop, starting to type will automatically bring up Krunner.

## Switch active windows using Krunner

Plasma 5 doesn't contain default way to specify krunner search only by active window titles. Following approaches are used to work around this issue.

#### Full list of windows with search by titles

This approach will require [xdotool](https://www.archlinux.org/packages/?name=xdotool).

1.  Go to *System Settings > Workspace > Shortcuts > Custom Shortcuts*.
2.  Create new Global shortcut -> Command/URL (by right click)
3.  Tick the checkbox to the right of the name.
4.  In Trigger tab select the desired key combination.
5.  In Action tab type `/usr/local/bin/krunner-search-by-windows.sh`
6.  Create file `/usr/local/bin/krunner-search-by-windows.sh` with the following content:
    ```
    #!/bin/bash
    qdbus org.kde.krunner /App querySingleRunner windows "" 
    sleep 0.2
    xdotool type 'window '
    xdotool key "shift+BackSpace"
    ```

7.  Make file executable and give run permission to all `chmod a+x /usr/local/bin/krunner-search-by-windows.sh` 

Note the space after `window`.

Now you're able to get list of opened windows by specified shortcut and search by this list as you type;

#### Search by titles without full windows list

This approach is more limited but far less ugly.

1.  Go to *System Settings > Workspace > Shortcuts > Custom Shortcuts*.
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

## See also

[Krunner on KDE UserBase Wiki](https://userbase.kde.org/Plasma/Krunner)