Related articles

*   [Session lock](/index.php/Session_lock "Session lock")
*   [List of applications#Screen lockers](/index.php/List_of_applications#Screen_lockers "List of applications")

Slock, or the "Simple X display locker", is a display locker for [X](/index.php/X "X") that aims to be minimal, fast, and lightweight.[[1]](http://tools.suckless.org/slock/).

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
*   [3 Usage](#Usage)
*   [4 Tips and tricks](#Tips_and_tricks)
    *   [4.1 Lock on suspend](#Lock_on_suspend)
    *   [4.2 Block VT switching and prevent killing X](#Block_VT_switching_and_prevent_killing_X)
*   [5 See also](#See_also)

## Installation

[Install](/index.php/Install "Install") the [slock](https://www.archlinux.org/packages/?name=slock) or [slock-git](https://aur.archlinux.org/packages/slock-git/) package.

## Configuration

Configuration is done by [editing](/index.php/Edit "Edit") the `config.h` header file and then recompiling the package. After configuration you should [create a package](/index.php/Create_a_package "Create a package").

## Usage

Simply run `slock` to lock the screen. You can also provide an argument to be run after the screen has been locked:

```
$ slock *cmd* *[arg ...]*

```

## Tips and tricks

### Lock on suspend

[Create](/index.php/Create "Create") the following service which turns off the monitor and locks the screen.

 `/etc/systemd/system/slock@.service` 
```
[Unit]
Description=Lock X session using slock for user %i
Before=sleep.target

[Service]
User=%i
Environment=DISPLAY=:0
ExecStartPre=/usr/bin/xset dpms force suspend
ExecStart=/usr/bin/slock

[Install]
WantedBy=sleep.target
```

[Enable](/index.php/Enable "Enable") the `slock@*user*.service` systemd unit for it to take effect for the username *user*.

### Block VT switching and prevent killing X

*slock* recommends blocking VT switching so that the screen lock cannot be bypassed. For the same reason, *slock* recommends preventing users from killing the X server. See [Xorg#Block TTY access](/index.php/Xorg#Block_TTY_access "Xorg") and [Xorg#Prevent a user from killing X](/index.php/Xorg#Prevent_a_user_from_killing_X "Xorg").

## See also

*   [Official homepage](http://tools.suckless.org/slock/)