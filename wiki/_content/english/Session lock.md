There are numerous utilities to lock the screen of a session. But it is important to note that the utility to use is highly dependant on the environment your are in, either the virtual console, or a specific display server (Xorg or Wayland).

See [List of screen lockers](/index.php/List_of_applications#Screen_lockers "List of applications").

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 By environment](#By_environment)
    *   [1.1 Virtual Console](#Virtual_Console)
    *   [1.2 Xorg](#Xorg)
    *   [1.3 Wayland](#Wayland)
*   [2 Triggering the lock](#Triggering_the_lock)
    *   [2.1 List of triggers](#List_of_triggers)
        *   [2.1.1 Manual](#Manual)
        *   [2.1.2 Inactivity](#Inactivity)
        *   [2.1.3 Suspend / Hibernate](#Suspend_/_Hibernate)
    *   [2.2 Shell triggers](#Shell_triggers)
        *   [2.2.1 ZSH](#ZSH)
    *   [2.3 Xorg triggers](#Xorg_triggers)
        *   [2.3.1 xss-lock](#xss-lock)
            *   [2.3.1.1 systemd events](#systemd_events)
            *   [2.3.1.2 DPMS](#DPMS)
        *   [2.3.2 xautolock](#xautolock)
    *   [2.4 Wayland triggers](#Wayland_triggers)
    *   [2.5 SystemD triggers](#SystemD_triggers)
        *   [2.5.1 DBUS Notification](#DBUS_Notification)
        *   [2.5.2 Inactivity](#Inactivity_2)
        *   [2.5.3 Units](#Units)
            *   [2.5.3.1 Before suspend/hibernate](#Before_suspend/hibernate)
            *   [2.5.3.2 Lid closing](#Lid_closing)
*   [3 Actions after the lock has been triggered](#Actions_after_the_lock_has_been_triggered)
*   [4 See also](#See_also)

## By environment

### Virtual Console

You can use `vlock` to lock a virtual console.

### Xorg

### Wayland

## Triggering the lock

You can lock a session using different methods:

*   from a terminal
*   using a GUI:
    *   from a desktop icon
    *   using hot corners
    *   from a menu (mouse or keyboard driven)
*   from a [shortcut](/index.php/Keyboard_shortcuts "Keyboard shortcuts")
*   from an event:
    *   inactivity
    *   another action (suspend, hibernate, ...)

The last point (triggering a lock from an event) is the trickiest, because you can do it one of two ways:

*   get the action trigger to execute your lock, then to execute the initial action.
*   from the event trigger, add the lock to the event chain. So far this can only be done using systemd.

### List of triggers

#### Manual

#### Inactivity

You can trigger a lock on inactivity using [systemd](#Inactivity_2), [DPMS](/index.php/DPMS "DPMS") (see [xss-lock](#xss-lock)) or [xautolock](#xautolock)

#### Suspend / Hibernate

See systemd

```
 Service file dependency
 Hook to xss-lock

```

### Shell triggers

#### ZSH

To execute a command after terminal inactivity, you can use the TMOUT environment variable.

You can combine it with a trap on the ALARM signal to execute the lock. Without a trap, it will just terminate the shell.

You might want to detect if you are in a graphical environments, otherwise your GUI terminals might start disappearing without you understanding why.

### Xorg triggers

#### xss-lock

[xss-lock](https://www.archlinux.org/packages/?name=xss-lock) is triggered by one of two things:

*   systemd events
*   [DPMS](/index.php/DPMS "DPMS")

The advantage of this is that you can control a lock issued manually, by inactivity, and by a suspend command at the same place.

To execute an action on one of those events:

```
xss-lock <locker-utility>

```

##### systemd events

By default, xss-lock subscribes to `suspend`, `hibernate`, `lock-session`, and `unlock-session` with appropriate actions (run locker and wait for user to unlock or kill locker).

You can prevent xss-lock from being triggered by `suspend` and `hibernate` using `--ignore-sleep`.

You can trigger a manual lock using loginctl lock-session.

##### DPMS

To configure DPMS signaling timeout:

```
  # Trigger screensaver after 10 minutes of inactivity
  xset s on
  xset s 600

```

DPMS signaling can also be configured in `/etc/X11/xorg.conf.d/` in the `Monitor` section.

Using DPMS signaling, you can set a second timer, for exemple to notify the user or to dim the screen. For exemple (from [xss-lock(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/xss-lock.1)):

```
# Dim the screen after three minutes of inactivity, lock the screen two minutes later using i3lock:

xset 180 120
xss-lock -n dim-screen.sh -- i3lock -n

```

**Note:**

When using xss-lock with [DPMS](/index.php/DPMS "DPMS"), you will have to blank the screen yourself. It will not be triggered when looking at videos

#### xautolock

```
xautolock -time 12 -locker "systemctl suspend" -detectsleep

```

**Note:**

xautolock has restrictive timer limits:

*   1 min to 1 hour for `time`
*   10 min to 2 hour for `killtime`

It might be necessary to add `-detectsleep` to prevent xautolock from locking the session after resuming. One nice feature of xautolock is the `corners`.

### Wayland triggers

### SystemD triggers

#### DBUS Notification

Using `loginctl lock-session`, or the `lock` action in [logind.conf(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/logind.conf.5), you can notify the system through DBUS that you want to lock. This notification can the be processed, for exemple by xss-lock.

#### Inactivity

In [logind.conf(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/logind.conf.5), you can configure the `IdleAction` to `lock`. This will trigger a DBUS notification, that will have to be processed (for exemple by xsslock) to lock the session.

Note that this is for a global system (so this is not ideal for a multi user environment).

Note also that "this requires that user sessions correctly report the idle status to the system".

#### Units

##### Before suspend/hibernate

You can use a [Sleep hook](/index.php/Power_management#Sleep_hooks "Power management").

```
[Unit]
Description=Lock the screen
Before=sleep.target

[Service]
#User=user
Environment=DISPLAY=:0
ExecStart=i3lock

[Install]
WantedBy=sleep.target
```

##### Lid closing

You can use the `lock` action using the related [ACPI Event](/index.php/Power_management#ACPI_events "Power management")

## Actions after the lock has been triggered

Suspend/Hibernate after X Shudown screen

## See also

*   [Geoff Greer's site: Linux Laptop Locking](https://geoff.greer.fm/2018/01/02/linux-laptop-locking/)