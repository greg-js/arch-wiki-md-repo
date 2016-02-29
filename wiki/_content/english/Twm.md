Twm is a window manager for X11\. It is a small program, being built against Xlib rather than using a widget library, and as such, it is very light on system resources. Though simple, it is highly configurable; fonts, colours, border widths, title bar buttons, etc. can all be set by the user.

## Contents

*   [1 Twm creation and name](#Twm_creation_and_name)
*   [2 Installation](#Installation)
*   [3 Start twm with X](#Start_twm_with_X)
*   [4 Configuration (editing your .twmrc)](#Configuration_.28editing_your_.twmrc.29)
*   [5 Resources](#Resources)
*   [6 References](#References)

### Twm creation and name

Twm was written by Tom LaStrange, a developer who was frustrated by the limitations of [uwm (Ultrix Window Manager)](https://en.wikipedia.org/wiki/UWM_(computing) "wikipedia:UWM (computing)")[[[1]](http://www.linuxplanet.com/linuxplanet/reports/3000/2/), the only window manager around when X11 was first released. Twm supplanted uwm as the default window manager supplied with X11 from the X11R4 release in 1989[wikipedia:UWM_(computing)](https://en.wikipedia.org/wiki/UWM_(computing) "wikipedia:UWM (computing)").

Twm has stood for *Tom's Window Manager*, *Tab Window Manager* and more recently *Timeless Window Manager*[wikipedia:Twm](https://en.wikipedia.org/wiki/Twm "wikipedia:Twm").

## Installation

Twm is provided by the package [xorg-twm](https://www.archlinux.org/packages/?name=xorg-twm).

## Start twm with X

In order for twm to be run as your window manager, edit the file `~/.xinitrc` so the final line is:

```
exec twm

```

If you now type:

```
startx

```

at the command prompt, [X](/index.php/X "X") will start using twm as its window manager.

If you would like to configure X (and twm) to start on boot (or when you login), read the wiki page [Start X at login](/index.php/Start_X_at_login "Start X at login") to find out how.

## Configuration (editing your .twmrc)

By default, twm looks very dated and unintuitive. By creating the file `~/.twmrc`, you can customize twm to make it more friendly.

## Resources

*   The twm man page gives full details of the commands which can be used in your `~/.twmrc` file. It can be viewed [online](http://linux.die.net/man/1/twm) or accessed once twm is installed by `man twm`.
*   Many `~/.twmrc` files have been posted online. The site [xwinman.org](http://xwinman.org/vtwm.php) has several `~/.twmrc` files with screenshots which might provide inspiration. A [Google search for "twmrc"](https://www.google.com/search?q=twmrc) can be used to find new ideas.
*   More information about twm can be found on the [twm Wikipedia page](https://en.wikipedia.org/wiki/Twm "wikipedia:Twm").
*   There is a patched version, not in the repositories, with updated features such as transparency. A description and build script is available on the [xorg mailing list](http://lists.x.org/archives/xorg/2010-January/048401.html). It can be tried out by installing [xcompmgr](/index.php/Xcompmgr "Xcompmgr"), running the build script, putting the resulting `twm` and `dot.twmrc` files in a convenient directory, and editing the `~/.xinitrc` file so that the last two lines are

```
xcompmgr -o 0.3  -c -r 8 -t -10 -l -12 &
/path-to-directory/twm -visual TrueColor -depth 32 -f /path-to-directory/dot.twmrc

```

## References

1.  Proffitt, Brian. "[From the Desktop: Tom LaStrange Speaks!](http://www.linuxplanet.com/linuxplanet/reports/3000/2/)", *LinuxPlanet*, February 6, 2001\. Retrieved October 22, 2009.
2.  "[UWM (computing)](https://en.wikipedia.org/wiki/UWM_(computing) "wikipedia:UWM (computing)")", *Wikipedia*. Retrieved October 22, 2009.
3.  "[Twm](https://en.wikipedia.org/wiki/Twm "wikipedia:Twm")", *Wikipedia*. Retrieved October 22, 2009.
4.  "[Twm man page](http://linux.die.net/man/1/twm)", *linux.die.net*. Retrieved October 22, 2009.
5.  "[Sample twmrc](http://www.custompc.plus.com/twm/configs/twmrc09)", *custompc.plus.com*. Retrieved August 12, 2013.
6.  "[Window Managers for X: TWM/VTWM](http://xwinman.org/vtwm.php)", *xwinman.org*. Retrieved October 22, 2009.
7.  "[Google search for twmrc](https://www.google.com/search?q=twmrc)", *google.com*. Retrieved October 22, 2009.
8.  Kask, Eeri. "[TWM -- Revised Edition -- Again](http://lists.x.org/archives/xorg/2010-January/048401.html)", *lists.x.org*, January 3, 2010.