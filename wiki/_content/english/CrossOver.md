Related articles

*   [Wine](/index.php/Wine "Wine")

[CrossOver](http://www.codeweavers.com/) is the paid, commercialized version of Wine which provides more comprehensive end-user support. It includes scripts, patches, a [GUI](https://en.wikipedia.org/wiki/Graphical_user_interface "wikipedia:Graphical user interface"), and third-party software which may never be accepted in the Wine Project. This combination makes running Windows programs considerably easier for those less tech-savvy.

## Installation

In this article it is suggested that you install the trial version of crossover. [Install](/index.php/Install "Install") [crossover](https://aur.archlinux.org/packages/crossover/) package.

## Usage

If installed by a user in *single user mode*, Crossover binaries will be located in `~/cxoffice`. Windows applications and configuration files will be placed in `~/.cxoffice`.

If installed with root privileges in *multi-user shared mode*, Crossover binaries will be located in `/opt/cxoffice`. Each user's bottles will be placed in `~/.cxoffice`.

Some desktop environments like [KDE](/index.php/KDE "KDE") may have automatically placed menu entries as part of the installation process.

Installed programs should be located under a new menu entry called *Window Applications*.

**Tip:** If you get a registration failure, try to execute `/opt/cxoffice/bin/cxregister` as root. Registration should then complete and be valid for all users on the system.

## Troubleshooting

There is also a way to generate a log file to assist you in tracking down errors that may be preventing you from running your desired Windows application(s). Follow the menu path *CrossOver > Run a Windows Command > Debug Options* and click the "+" sign to expand the options. Click the "Create log file" checkbox. Enter the command you would use to run your Windows application in the "Command" text box. You can use the browse button, if you are not sure what to enter, to navigate to your Windows application. CrossOver will prompt you for a location to save the log file. Choose your location and press enter to have Crossover generate the log file in it.

Although the `libSM.so` library was not shown in the cxdiag list of missing libraries - it did appear in the log file. The library belongs to the [libsm](https://www.archlinux.org/packages/?name=libsm) package. If you are having problems getting your application to run, check its installation status.