# CrossOver

Related articles

*   [Wine](/index.php/Wine "Wine")

[CrossOver](http://www.codeweavers.com/) is the paid, commercialized version of Wine which provides more comprehensive end-user support. It includes scripts, patches, a [GUI](https://en.wikipedia.org/wiki/Graphical_user_interface "wikipedia:Graphical user interface"), and third-party software which may never be accepted in the Wine Project. This combination makes running Windows programs considerably easier for those aren't so tech-savvy.

## Installation

In this article it is suggested that you want install trial verison of crossover. [Install](/index.php/Install "Install") [crossover](https://aur.archlinux.org/packages/crossover/)<sup><small>AUR</small></sup> package.

## Using CrossOver

If installed by a user in _single user mode_, Crossover binaries will be located in `~/cxoffice`.`` Windows applications and configuration files will be placed in ~/.cxoffice.

If installed with root privileges in _multi-user shared mode_, Crossover binaries will be located in `/opt/cxoffice`. Each user's bottles will be placed in ~/.cxoffice.

Some desktop environments like [KDE](/index.php/KDE "KDE") may have automatically placed menu entries as part of the installation process.

Installed programs should be located under a new menu entry called _Window Applications_.

**Tip:** If you get a registration failure, try: `# /opt/cxoffice/bin/cxregister`. Registration should then complete and be valid for all users on the system.

## Troubleshooting

There is also a way to generate a logfile to assist you in tracking down errors that may be preventing you from running your desired Windows application(s). From the CrossOver menu, choose "Run a Windows Command". You will see "Debug Options". Click the "+" sign to expand the options. Click the "Create log file" checkbox. Enter the command you would use to run your Windows application in the "Command" text box. (You can use the Browse button if you aren't sure what to enter, to navigate to your Windows application). CrossOver will prompt you for a location to save the log file. Choose your location and press enter. Crossover will generate the logfile in the location you chose.

Although the libSM.so.6 library was not shown in the cxdiag list of missing libraries - it DID appear in the logfile. The library belongs to the lib32-libsm package. If you're having problems getting your application to run, you might want to try installing lib32-libsm.

Retrieved from "[https://wiki.archlinux.org/index.php?title=CrossOver&oldid=381043](https://wiki.archlinux.org/index.php?title=CrossOver&oldid=381043)"