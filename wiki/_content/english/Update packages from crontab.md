**Warning:** **Doing automatic updates from cron is strongly discouraged. It is likely to leave your machine in a broken and unbootable state.** If this breaks your machine, do not hold anyone but yourself responsible. You have been warned.

## Contents

*   [1 Do not try this at home!](#Do_not_try_this_at_home.21)
*   [2 Do try this at home!](#Do_try_this_at_home.21)
*   [3 Using systemd](#Using_systemd)
*   [4 Manual set up of auto-update](#Manual_set_up_of_auto-update)
    *   [4.1 Update notifier](#Update_notifier)
    *   [4.2 Download updates](#Download_updates)
    *   [4.3 Download and install updates from short list](#Download_and_install_updates_from_short_list)
    *   [4.4 Download and install at night](#Download_and_install_at_night)
    *   [4.5 Update packages from the AUR](#Update_packages_from_the_AUR)
    *   [4.6 Update the mirrorlist file](#Update_the_mirrorlist_file)

## Do not try this at home!

1.  First, you (obviously!) need to [install cron itself](/index.php/Cron "Cron"). Do that first.
2.  It is highly recommended to also install a mail transfer agent, such as [Postfix](/index.php/Postfix "Postfix"), to send you notifications if pacman fails.
3.  Run as root: `crontab -e`
4.  Copy-paste this to your crontab:

```
MAILTO=your@email
LOGFILE=/var/log/cron-pacman.log

# 1\. minute (0-59)
# |   2\. hour (0-23)
# |   |   3\. day of month (1-31)
# |   |   |   4\. month (1-12)
# |   |   |   |   5\. day of week (0-7: 0 or 7 is Sun, or use names)
# |   |   |   |   |   6\. commandline
# |   |   |   |   |   |
#min hr  dom mon dow command
00   13   *   *   *  . /etc/profile && (echo; date; pacman -Syuq --noconfirm) &>>$LOGFILE || (echo 'pacman failed!'; tail $LOGFILE; false)

```
To check every */time you must use e.g. `*/2` to check every 2 min or any other time value.

If you want to automatically reboot your computer upon a successful upgrade, append '&& reboot' to the above line.

## Do try this at home!

Instead of using `pacman -Syuq` above, use `pacman -Syuwq`. The '-w' will cause pacman to "retrieve all packages from the server, but do not install/upgrade anything." While you will still have to manually update your system, you will not have to wait (as long) for packages to download while doing so.

## Using systemd

Instead of installing and configuring cron, you can directly use [systemd](/index.php/Systemd "Systemd"). [Here](http://www.techrapid.co.uk/linux/arch-linux/automatic-update-arch-linux-with-systemd/) is an article on how to do it.

## Manual set up of auto-update

**Note:** The sections below are mostly focused on setting up Linux on computer for the home user.

**Warning:**

*   The [KCron](https://userbase.kde.org/KCron) and [GNOME Schedule](https://wiki.gnome.org/Schedule) can use own wrappers inside crontab to run scheduled tasks that will cause problems such as use of the `pacman-db-upgrade` may leave the `/var/lib/pacman/db.lck` lock file that will prevent run of the next [pacman](https://www.archlinux.org/packages/?name=pacman) command.
*   You must make backup of [pacman database](/index.php/Pacman_tips#Backing_up_Local_database_with_systemd "Pacman tips") before giving computer to user.

If you want to set up Arch Linux for home user and still keep system up to date you will need to make work in background without distraction of user.

### Update notifier

There are many programs such as [zenity](https://www.archlinux.org/packages/?name=zenity) that can show GUI messages from program or scripts that runs in console. In this example you will see a dialog with list with file names and size for each of them that need to be downloaded for installation. By clicking Yes it will return exit code 0 respective 1 for No that will be placed in the [$?](http://www.tldp.org/LDP/Bash-Beginners-Guide/html/sect_03_02.html) variable.

```
$ zenity --question --text="$(pacman -Qu|awk '//{if(index($0,"[ignored]") == 0 )print $1  }'|pacman -Si -|grep '^[a-Z]'| \
 sed 's/ //g'|  awk -F':' '//{ZZ=ZZ+1;XX[ZZ]=$1;SS[ZZ]=$2;}   
 END{AA=ZZ/18;for(i=1;i <= AA;i++){print XX[i*18-16]": "SS[18*i-16]" | "XX[i*18-4]": "SS[i*18-4];}}' )"
```

For a long list of updates is better to use this example and `zenity` can also read data from stdin.

```
$ pacman -Qu |awk '//{if(index($0,"[ignored]") == 0 )print $1  }'|pacman -Si -|grep '^[a-Z]'|\
  sed 's/ //g'|awk -F':' '//{ZZ=ZZ+1;XX[ZZ]=$1;SS[ZZ]=$2;}
  END{AA=ZZ/18;for(i=1;i <= AA;i++){print XX[i*18-16]": "SS[18*i-16]" | "XX[i*18-4]": "SS[i*18-4];}}' | zenity --text-info --title=Uppdateringar
```

Is suitable to use after updates has been downloaded.

This will show progress bar. Depends on amount of repositories you will need to calculate correct step size, you can do it simply by dividing 100 with amount of lines printed by [pacman](/index.php/Pacman "Pacman") or use `LCount=$(grep ^"\[" /etc/pacman.conf -c);echo $((100/LCount))` to calculate and pass it to the [awk](https://www.gnu.org/software/gawk/manual/html_node/Using-Shell-Variables.html) command.

```
$ pacman -Sy --noprogressbar |awk '{AA=AA+16.7;system("echo "AA)}' | zenity --progress --no-cancel

```

In comparison to [zenity](https://www.archlinux.org/packages/?name=zenity) the program `xmessage` from [xorg-xmessage](https://www.archlinux.org/packages/?name=xorg-xmessage) package shows much smaller windows but does not support UTF and has some more limitations but here we will not discuss them, it is just a perfect light notifier.

```
...........
...........
STARTit=$(date '+%M-%S')
xmessage -timeout 2 "Starting downloading of updates" & disown
...........
...........
ENDit="$(date '+%M-%S')"
xmessage -timeout 3 "${STARTit}"' * '"${ENDit}" & disown
...........
...........
```

See also: [How to show a message box from a bash script in Linux](http://stackoverflow.com/questions/7035/how-to-show-a-message-box-from-a-bash-script-in-linux).

### Download updates

The easiest way of creating a short list of updates is by creating the script that will print them to stdout, e.g.

 `ShortListUpdates.sh` 
```
#!/bin/bash
pacman -Qq | \
grep -e smplayer \
-e smtube \
-e ^jre \
-e ^gst \
-e firefox | \
grep -v -e 'to_ignore_package1' -e 'to_ignore_package2' -e 'to_ignore_package3'
#Files from a group to add
pacman -Qqg kde | grep -v -e 'to_ignore_package1' -e 'to_ignore_package2' -e 'to_ignore_package3'

```

Good to download updates after few hours of idle and limit it only to a day time and make similar just that will download and possible also install updates at night time if computer is powered on. To speed up update process at night and lower possible damage add some of packages to [ignore list](/index.php/Pacman#Skip_package_from_being_upgraded "Pacman"), such as fonts, kernel and mkinitcpio or any other that you think is not at all necessary to be updated. But still you can make a script that user can manually run to update all packages, e.g. `pacman -Qqen | pacman -S --needed --noconfirm -` but do not forget to add safety check of battery status if it is a laptop.

Steps for downloading process

1.  Check if stop mark after download exist, e.g. `if [ ! -f /tmp/.downloaded_yes ];then echo Is OK to download;else echo Already downloaded;fi`
2.  Check if computer is idle and how long time. Utilities [xprintidle](https://aur.archlinux.org/packages/xprintidle/)[[1]](http://www.ruddwire.com/handy-code/date-to-millisecond-calculators/) for X and command `w` for tty.
3.  Check if computer is connected with cable or how much battery is charged. You will need to install [upower](https://www.archlinux.org/packages/?name=upower).
    ```
    #!/bin/bash

    MAXpower="60"

    ST=($(upower -i "$(upower -e | grep 'BAT')" | grep -e "state" -e percentage | awk '{print $2}' | sed 's/%//g'))
    if [ ! -z ${ST[0]} ];then
     if [ ${ST[1]} -gt ${MAXpower} ]  || [ ${ST[0]} == 'charging' ] || [ ${ST[0]} == 'fully-charged' ]; then
      echo "OK"
       else
      echo "Fail"
     fi
      else 
     echo "OK"
    fi
    ```

4.  Check type of connection to prevent downloading due huge amount of data if computer using 3G or other PPP connection. Command `ifconfig | grep ^ppp -c`.
5.  Check if is online `ping -c 1 8.8.8.8 ; if [ "${?}" != "0" ]; then echo bad; else echo good; fi`, if the firewall is blocking ping requests then you can use `ifconfig | grep -v 'lo:' | grep RUNNING -c` or by trying to download a file and check if no errors accrued during downloading.
6.  Make a short list of the most important updates, e.g. for average internet user will be good to have a web-browser and its plugins,extensions, certifications and SSL componets and some of media players that you configured as default will need to be downloaded.
    **Note:** Do not make list too big for daily downloads and do not start installation directly after them were downloaded to avoid possible conflicts.

7.  Create a stop mark to prevent multiple update checks after download were finished, e.g. `echo downloaded > /tmp/.downloaded_yes`.

**Note:** The stop mark can be also created after all checks are passed in case if check of idle time is too low and download time might take more time depends on the connection and total size of updates.

### Download and install updates from short list

To download updates from the short list you can use this line `pacman -Sw --noconfirm --needed $(/full/path/to/ShortListUpdates.sh)`.

You will need to add only a power check before continue with installation of updates.

```
...............
...............
yes | pacman -S --noconfirm --needed $(/full/path/to/ShortListUpdates.sh)
systemctl daemon-reload
sleep 2
...............
...............
```

If you will use a GUI notifier then you may want to use this part in the begin of the update script if updates runs after reboot and user comes to log in screen([Display manager](/index.php/Display_manager "Display manager")). Be careful with the `sleep` timeout if too low it might freeze the screen. The notifier will be shown even on the login screen that will probably make user wait until updates are finished or after user logged if you will set *sleep* timeout too high and user logged in before script started.

```
#!/bin/bash
sleep 5
if [ "$(pgrep X -c)"  != "0" ]; then
export DISPLAY=:0
else
export DISPLAY=:0
startx "$0"
fi
.........
.........
.........
```

You may also will make it remove unnecessary locales for spell check in e.g. `/usr/include/hunspell`, `/usr/lib/aspell-0.60` or any other that contains unnecessary files that created after update or install of packages.

In the crone you can schedule installation of updates from a short list on each boot by using in `crontab`:

```
@reboot /usr/local/bin/update

```

**Note:** You can also make it copy the update-downloading scripts to `/tmp` to minimize disk usage because the `/tmp` is using RAM for storage of files.

### Download and install at night

If user will leave computer powered on at night then this example could be used to download and install after computer become idle for a some time to be more sure that user will not interrupt.

```
..............
..............# Battery and connection safety checks
..............
yes | pacman -S --needed $(pacman -Ssq openjdk | grep -v -e doc -e src)
  if [ $(ifconfig | grep ^ppp -c)  != "0" ];then
    pacman -Suw --noconfirm
   else
    pacman -Qq --native  | pacman -Sw --needed -
  fi
yes | pacman -Su
if [ "${?}" != "0"  ];then beep -f 100 -l 1000 && zenity --warning --text="Ett problem har uppstått. Kontakta Admin!"
if [ -f "/var/lib/pacman/db.lck"  ];then zenity --warning --text="Databasfilen är skadat eller används: /var/lib/pacman/db.lck";fi;
exit 1
else
BkupDate=$(date '+%A-day_of_the_week-%u')
pacman -Q --native > /opt/.alt_db_bkup-"${BkupDate}"
date >> /opt/.alt_db_bkup-"${BkupDate}"
systemctl daemon-reload
sleep 2
fi
pacman-db-upgrade
..............
..............
..............
```

Some of updates can be installed directly if you want make it download new releases of updates and not only updates for existing. If computer will use wireless or cable connection it will download all even packages that are in the ignore list but install only updates that are not in the ignore list. You can also make it download all updates one day and install next day, for that you will need to modify script and schedule days of the week for downloading and another script for installing or use command line variables to switch from downloading to installing.

### Update packages from the AUR

First must be created the [GPG key](/index.php/GnuPG#Create_key_pair "GnuPG") and added to the `makepkg` configuration file.

 `/etc/makepkg.conf` 
```
...............
PKGDEST=/path/to/custom_repo
GPGKEY="XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX"
...............
```

This can be used as a part in the download scripts and in the end of them.

**Warning:** Sometimes packages can change their names that will prevent update of the equivalent installed or if dependencies will be changed.

When you are installing Arch Linux on someones computer for use as a desktop then you are responsible too keep it working and the hardest part is too keep packages from the [AUR](/index.php/AUR "AUR") up to date. There are a few alternatives that you can use:

*   Make a script that will download files from the AUR or use [AUR helpers](/index.php/AUR_helpers "AUR helpers") but this can result that installed packages will not be updated if them are moved to the [Official repositories](/index.php/Official_repositories "Official repositories") in that case you will need to make a check even there if not found and vice versa.
*   Update packages by downloading and extracting binaries if they are available for your architecture, but version of the packages will not be registered in the [pacman](/index.php/Pacman "Pacman") database. The best way if it is possible then download by using a single URL instead of parsing the downloaded file for the URLs.
*   Have a cloned installation in the virtual environment and keep watching for updates and test them there if any problem accrued then create a fix that you can delivery to the user. The ways that you can use are by mailing a script with the configuration files or by setting up own repository that will keep only fixes and probably also packages that has often problem with updating in time.

This example shows how to start "makepkg" as root, for that you should have created an user with limited rights for that purpose.

 `runuser -u *user_name_with_limited_rights* makepkg` 

### Update the mirrorlist file

This can be scheduled to update mirrors once a week or few times in a month only for countries you want:

```
rm  /etc/pacman.d/mirrorlist
for Cnt in China Iran Russia Korea;
 do 
awk -v GG=$Cnt '{if(index($0,GG) != 0)AA=1;if(AA == 1)
   {if( match($0,"#") != "0"){SS=$0;sub("#","",SS);print SS ;}else AA=0} }' \
 /etc/pacman.d/mirrorlist.pacnew >> /etc/pacman.d/mirrorlist;

done

```

**Note:** It is assumed that the `/etc/pacman.d/mirrorlist.pacnew` file exists, usually created by the [pacman-mirrorlist](https://www.archlinux.org/packages/?name=pacman-mirrorlist) after update.

See also: [What to do if pacman-mirrorlist is not installed](/index.php/Mirrors#Official_mirrors "Mirrors").