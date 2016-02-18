**Note:** This is focused mostly on setting up recovery environment for the home user with low knowledge about computer usage or needs.

If something goes wrong during the update process, like your computer losing power half way through or the process getting stopped, some damage could be caused to your installation as a result of packages being half installed and some dependencies missing. This article covers the creation of a separate recovery environment in order to help mitigate damage caused by something going wrong during the update process and fix any issues arising from it.

## Contents

*   [1 GUI recovery environment](#GUI_recovery_environment)
*   [2 Prepare a safe restoration/reset of the whole storage device](#Prepare_a_safe_restoration.2Freset_of_the_whole_storage_device)
    *   [2.1 Physical locked storage](#Physical_locked_storage)
    *   [2.2 Virtualization](#Virtualization)
    *   [2.3 Restore desired parts on each boot](#Restore_desired_parts_on_each_boot)

### GUI recovery environment

If user did upgrade or update that prevents boot into the [desktop environment](/index.php/Desktop_environment "Desktop environment") or applications cannot start but user is able to see the [display manager](/index.php/Display_manager "Display manager") then it is good to make a separate environment for the user that is easy to use to try fix those errors on its own. This will be useful for users that has relatively low knowledge about computer specially about Linux. Install [openbox](https://www.archlinux.org/packages/?name=openbox) or any other equivalent window manager that they can use with the [idesk](https://www.archlinux.org/packages/?name=idesk) and create own buttons to the programs or better scripts that are configured to make actions and show warnings and the administrator contact information before starting. To prevent any unwanted user to use the "failsafe" environment or some of the recovery tasks you can add to begin of the script or window manager autostart something like:

```
AllowedUser="JolinTsai";
if [ "$(whoami)" != " ${AllowedUser,,}" ];then zenity --warning --text="You are not the allowed user!
The allowed user is "$AllowedUser;
#openbox --exit
exit 1
fi
```

You will need to remove all unnecessary entries from "type of session" list, you can do it by removing or better to moving the *.desktop files which contains information about them to the backup folder and create your own with a custom configuration, to make it simply just copy one of the *.desktop files to a file with the name you want and make changes in the Exec and description parts.

Something like this you can use to remove or move files to backup directory.

```
find /usr/share/apps/kdm/sessions/ -maxdepth 1 -type f \ 
! -name kde-plasma.desktop ! -name lxde.desktop ! -name openbox.desktop ! -name xfce4.desktop \
-exec mv "{}" /usr/share/apps/kdm/sessions/OLD_/ \;
```

You usually can find them in some of those folders:

```
/usr/share/config/kdm/sessions
/usr/share/apps/kdm/sessions
/usr/share/xsessions/
```

You will also need to remove borders from windows to prevent user to close the working window such as xterm if you will use it to show output of commands while they are working. You can do it by using the [devilspie](https://www.archlinux.org/packages/?name=devilspie).

To get list of the window names for using in the devilspie configuration file you can use the [wmctrl](https://www.archlinux.org/packages/?name=wmctrl) utility `wmctrl -l | awk '{print substr($0, index($0,$4))}'` or when you start [devilspie](https://www.archlinux.org/packages/?name=devilspie) you will see all information that is possible to use in the configuration file.

`Window Title: 'name@host:~/.path'; Application Name: **'name@host:~/.path'** ; Class: **'XTerm'** ; Geometry: 492x350+487+226`

The `window_name` , `application_name` and `window_class` can be used to change the window properties.

Example of the devilspie configuration file that you can use for the preferred application

 `.devilspie/DesktopConsole.ds` 
```
(if (is (**window_class**) "XTerm")
        (begin
(undecorate)
(skip_tasklist)
(above)
(fullscreen)
(maximize)                       
(unpin)                
(skip_pager)       
            )
        )
```

The XTerm has also a command line to start it in the full screen: `xterm -fullscreen`.

**Tip:** To run an application in the full screen makes user unable to click on other buttons on the desktop until task is completed.

## Prepare a safe restoration/reset of the whole storage device

Here will be described basic theoretical steps about how to make more easier restore of the default operation system (e.g. Arch Linux), just by using "Reset" function made by you that will be very useful for beginners/common users or if you will have plans to sell computers with a preferred Linux.

### Physical locked storage

*   The initial factory set up must be stored on the write protected storage device such as e.g. [Secure Digital SD cards](https://en.wikipedia.org/wiki/Secure_Digital_SD_cards "wikipedia:Secure Digital SD cards") that can be physically locked into the read only mode.
*   The latest updated factory set up must be stored on the writeable storage device or on a separate partition but with limited access such as write protected mount predefined in fstab and/or use in additional mount scripts mount.* with checks which device/partition is mounted and allow mount only in READ ONLY mode for a normal user.
*   It also good to have those destinations hidden in a file managers menu.
*   The BIOS will need to be configured to boot from SD Card and password protected(password can be name+model of the computer). The SD card need to be permanent attached and sealed(glued).

You can make your own custom Live CD with [Archiso](/index.php/Archiso "Archiso") that must have functions:

*   Health monitoring tools such as [smartmontools](https://www.archlinux.org/packages/?name=smartmontools) to show errors and instructions what to do if destination storage device is damaged.
*   Restore whole storage device with tools as [fsarchiver](https://www.archlinux.org/packages/?name=fsarchiver) from the back up image if the main partition is damaged or have it as an option
*   Retrieve updates from the internet if it is available.
*   Use latest created "ISO" if it is available to install updates

The additional ISO on a separate partition can be created after a certain amount of updates predefined by you or manually by user.

On the first login user must get an opportunity to choose a cloud server where was stored the list of all installed applications and updated configuration files.

On PC the restoration media can be stored inside the box by connecting to USB card with adaptor. Laptops are missing the ability of storing extra storage devices inside that can be used for reparation purposes, but some of them can have place for the addition storage that can be connected to them such as [Secure Digital SD cards](https://en.wikipedia.org/wiki/Secure_Digital_SD_cards "wikipedia:Secure Digital SD cards") where can be stored only initial "factory" ISO and optionally also the internal storage device back up image.

### Virtualization

Create a minimal installation of the Linux with a user that will be logged in automatically and start with .[xinitrc](/index.php/Xinitrc "Xinitrc") preconfigured virtual machine with scheduled snapshots that can even be stored on a remote storage.

### Restore desired parts on each boot

**Note:** It is might be useful to be used on computers in Internet Cafe or by children at home. To prevent damage by commands like mv/cp/rm might be useful to rename them and replace with scripts that has checks of which path/files are allowed to be removed.

By creating bootable ISO image or [SquashFS](https://en.wikipedia.org/wiki/SquashFS "wikipedia:SquashFS") that can be started with [GRUB](/index.php/GRUB "GRUB"). Those can be preconfigured even with minimal needed applications, X server or Wayland and users. After boot you can automatize mount of path to `/usr/`, `/home/` or other custom folders that can exist on physical storage or in a file. It is useful for protection of boot and kernel settings from possible damages. Users will be able to updated programs if partition/file is mounted to `/var/lib/pacman/` and has writeable access to it.