See [rxvt-unicode](/index.php/Rxvt-unicode "Rxvt-unicode") for the main article.

## Contents

*   [1 Improved Kuake-like behavior in Openbox](#Improved_Kuake-like_behavior_in_Openbox)
    *   [1.1 Scriptlets](#Scriptlets)
    *   [1.2 urxvtq with tabbing](#urxvtq_with_tabbing)
        *   [1.2.1 Tab control](#Tab_control)
    *   [1.3 Openbox configuration](#Openbox_configuration)
    *   [1.4 Further configuration](#Further_configuration)
    *   [1.5 Related scripts](#Related_scripts)
*   [2 Improving performance](#Improving_performance)
    *   [2.1 Daemon-client](#Daemon-client)
        *   [2.1.1 Xinitrc](#Xinitrc)
        *   [2.1.2 systemd](#systemd)
*   [3 Advanced tab management](#Advanced_tab_management)
*   [4 Transparency](#Transparency)
    *   [4.1 True transparency](#True_transparency)
    *   [4.2 Native transparency](#Native_transparency)
*   [5 Set icon](#Set_icon)
*   [6 Use urxvt as application launcher](#Use_urxvt_as_application_launcher)
*   [7 Xterm escape sequences](#Xterm_escape_sequences)
*   [8 Bidirectional support](#Bidirectional_support)
*   [9 Bell Command](#Bell_Command)

## Improved Kuake-like behavior in Openbox

This was originally posted on the forum by Xyne [[1]](https://bbs.archlinux.org/viewtopic.php?pid=550380), and it relies on the [xdotool](https://www.archlinux.org/packages/?name=xdotool) found in the [official repositories](/index.php/Official_repositories "Official repositories").

### Scriptlets

Save this scriptlet from the `urxvtc` man page somewhere on your system as `urxvtc` (e.g., in `~/.config/openbox`):

```
#!/bin/sh

urxvtc "$@"
if [ $? -eq 2 ]; then
   urxvtd -q -o -f
   urxvtc "$@"
fi

```

and save this one as `urxvtq`:

```
#!/bin/bash

wid=$(xdotool search --classname urxvtq)
if [ -z "$wid" ]; then
  /path/to/urxvtc -name urxvtq -geometry 80x28
  wid=$(xdotool search --classname urxvtq | head -1)
  xdotool windowfocus "$wid"
  xdotool key Control_L+l
else
  if [ -z "$(xdotool search --onlyvisible --classname urxvtq 2>/dev/null)" ]; then
    xdotool windowmap "$wid"
    xdotool windowfocus "$wid"
  else
    xdotool windowunmap "$wid"
  fi
fi

```

Make sure that you change `/path/to/urxvtc` to the actual path to the `urxvtc` scriptlet that you saved above. We will be using `urxvtc` to launch both regular instances of `urxvt` and the kuake-like instance.

### urxvtq with tabbing

If you want to have tabs in your kuake-like `urxvtc` (here called `urxvtq`) just replace the third line in your `urxvtq`:

```
wid=$(xdotool search --classname urxvtq)

```

with:

```
wid=$(xdotool search --classname urxvtq | grep -m 1 "" )

```

To activate tab support, you can either replace the fifth line of your `urxvtq`:

```
/path/to/urxvtc -name urxvtq -geometry 80x28

```

with:

```
/path/to/urxvtc -name urxvtq -pe tabbed -geometry 80x28

```

or replace this line of your `~/.Xresources` file:

```
URxvt.perl-ext-common: default,matcher

```

with

```
URxvt.perl-ext-common: default,matcher,tabbed

```

#### Tab control

| Key | Description |
| Shift+Left | Switch to the tab left of the current one |
| Shift+Right | Switch to the tab right of the current one |
| Shift+Down | Create a new tab |

You can also use your mouse to switch the tabs by clicking the wished one and create a new tab by clicking on *[NEW].\\*

To close a tab just enter `exit` like you would to normally close a terminal.

### Openbox configuration

Now add the following lines to the `<applications>` section of `~/.config/openbox/rc.xml`:

```
<application name="urxvtq">
   <decor>no</decor>
   <position force="yes">
     <x>center</x>
     <y>0</y>
   </position>
   <desktop>all</desktop>
   <layer>above</layer>
   <skip_pager>yes</skip_pager>
   <skip_taskbar>yes</skip_taskbar>
   <maximized>Horizontal</maximized>
</application>
```

and add these lines to the `<keyboard>` section:

```
<keybind key="W-t">
  <action name="Execute">
    <command>/path/to/urxvtc</command>
  </action>
</keybind>
<keybind key="W-grave">
  <action name="Execute">
    <execute>/path/to/urxvtq</execute>
  </action>
</keybind>
```

Here too you need to change the `/path/to/*` lines to point to the scripts that you saved above. Save the file and then reconfigure Openbox. You should now be able to launch regular instances of urxvt with `Super+T`, and toggle the kuake-like console with `Super+**`**` (the grave key also known as the backtick).

### Further configuration

The advantage of this configuration over the urxvt kuake Perl script is that Openbox provides more keybinding options such as modifier keys. The kuake script hijacks an entire physical key regardless of any modifier combination. Review the [Openbox bindings documentation](http://openbox.org/wiki/Help:Bindings) for the full range or possibilities.

The [Openbox per-app settings](http://openbox.org/wiki/Help:Applications) can be used to further configure the behavior of the kuake-like console (e.g. screen position, layer, etc.). You may need to change the "geometry" parameter in the `urxvtq` scriptlet to adjust the height of the console.

### Related scripts

*   hbekel has posted a generalized version of the `urxvtq` [here](https://bbs.archlinux.org/viewtopic.php?pid=550380#p550380) which can be used to toggle any application using [xdotool](https://www.archlinux.org/packages/?name=xdotool).
*   [http://www.jukie.net/~bart/blog/20070503013555](http://www.jukie.net/~bart/blog/20070503013555) - A script for opening URLs with your keyboard instead of mouse with urxvt.

## Improving performance

*   Avoid the use of Xft fonts. If Xft fonts must be used, append `:antialias=false` to the setting value.[[2]](http://pod.tst.eu/http://cvs.schmorp.de/rxvt-unicode/doc/rxvt.7.pod#Can_I_speed_up_Xft_rendering_somehow)
*   Build rxvt-unicode with disabled support for unnecessary features, `--disable-xft` and `--disable-unicode3` in particular.
*   Limit the number of `saveLines` (option `-sl`) in the scrollback buffer to reduce memory usage. [[4]](http://pod.tst.eu/http://cvs.schmorp.de/rxvt-unicode/doc/rxvt.7.pod#Isn_t_rxvt_unicode_supposed_to_be_sm)
    *   Use tmux for scrollback buffer and set saveLines to 0
*   [Disable perl](/index.php/Rxvt-unicode#Disabling_Perl_extensions "Rxvt-unicode")
*   Consider running `urxvtd` as a daemon accepting connections from `urxvtc` clients.

### Daemon-client

**Warning:** If the server crashes, all processes in the clients are terminated. For example, *xkill* and server resets/restarts will kill the urxvtd instance including all windows it has opened. See [urxvtd(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/urxvtd.1) for details.

#### Xinitrc

See the *Examples* section in [urxvtd(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/urxvtd.1). This is the preferred option.

#### systemd

**Note:** Regular users cannot execute systemctl power commands (reboot, poweroff, etc) when logged in to a urxvt client/daemon setup which is started through systemd, as the client is not part of the [session](/index.php/Session "Session"). For this reason starting urxvt through systemd is discouraged.

System service:

 `/etc/systemd/system/urxvtd@.service` 
```
[Unit]
Description=RXVT-Unicode Daemon

[Service]
User=%i
ExecStart=/usr/bin/urxvtd -q -o

[Install]
WantedBy=multi-user.target

```

Pass the username when [starting the service](/index.php/Systemd#Using_units "Systemd"):

```
urxvtd@*username*.service

```

For a [systemd/User](/index.php/Systemd/User "Systemd/User") service, place the following unit files in `~/.config/systemd/user`:

 `urxvtd.service` 
```
[Unit]
Description=Urxvt Terminal Daemon
Requires=urxvtd.socket

[Service]
ExecStart=/usr/bin/urxvtd -o -q
Environment=RXVT_SOCKET=%t/urxvtd-%H

[Install]
WantedBy=*MyTarget*.target

```
 `urxvtd.socket` 
```
[Unit]
Description=urxvt daemon (socket activation)
Documentation=man:urxvtd(1) man:urxvt(1)

[Socket]
ListenStream=%t/urxvtd-%H

[Install]
WantedBy=sockets.target

```

## Advanced tab management

Install the [urxvt-tabbedex](https://aur.archlinux.org/packages/urxvt-tabbedex/) package from [AUR](/index.php/AUR "AUR"), then add the `tabbedex` value to the `URxvt.perl-ext-common` X resource in your `~/.Xresources`:

```
URxvt.perl-ext-common: ...,tabbedex,...

```

**Note:** If you have previously used the `tabbed` Perl extension and have defined the `tabbed` value for the `URxvt.perl-ext-common` X resource, please remove the `tabbed` value first to avoid conflict with `tabbedex`.

By default, the "[NEW]" button (which is rarely used and usable only with the mouse) is disabled with tabbedex. You can reenable this feature by setting the `new-button` to yes.

```
URxvt.tabbed.new-button: true

```

Tabs can be named with `Shift+ ↑` (`Enter` to confirm, `Escape` to cancel).

To automatically hide the tabs bar when only one tab is present, enable the following resource:

```
URxvt.tabbed.autohide: true

```

To prevent the last tab from closing Urxvt, enable the following resource:

```
URxvt.tabbed.reopen-on-close: yes

```

To start a new tab or cycle through tabs, use the following user commands: `tabbedex:(new|next|prev)_tab`. Example of mappings:

```
URxvt.keysym.Control-t: perl:tabbedex:new_tab
URxvt.keysym.Control-Tab: perl:tabbedex:next_tab
URxvt.keysym.Control-Shift-Tab: perl:tabbedex:prev_tab

```

To define your own key bindings to rename a tab or move a tab to the right or to the left, use the following commands: `tabbedex:move_tab_(left|right)` and `tabbedex:rename_tab`. Example of mappings:

```
URxvt.keysym.Control-Shift-Left: perl:tabbedex:move_tab_left
URxvt.keysym.Control-Shift-Right: perl:tabbedex:move_tab_right
URxvt.keysym.Control-Shift-R: perl:tabbedex:rename_tab

```

**Note:** Redefining the keys used for the user commands will not disable the default mappings, you have to set the X resource `no-tabbedex-keys` for that. However, currently it is not included in [urxvt-tabbedex](https://aur.archlinux.org/packages/urxvt-tabbedex/) package. Consider using [urxvt-tabbedex-git](https://aur.archlinux.org/packages/urxvt-tabbedex-git/) package instead:
```
URxvt.tabbed.no-tabbedex-keys: true

```

## Transparency

### True transparency

To use true transparency, you need to be using a [window manager](/index.php/Window_manager "Window manager") that supports compositing or a separate compositor.

From the command-line:

```
$ urxvt -depth 32 -bg rgba:3f00/3f00/3f00/dddd

```

Using the configuration file:

 `~/.Xresources` 
```
URxvt.depth: 32
URxvt.background: rgba:1111/1111/1111/dddd

```

or

 `~/.Xresources` 
```
URxvt.depth: 32
URxvt.background: [95]#000000

```

where '95' is the opacity level in percentage and '#000000' is the background color.

To use a color i.e. #302351 with the rgba:rrrr/gggg/bbbb/aaaa syntax it would be rgba:3000/2300/5100/ee00\. "ee00" (the alpha value) to make it nicely transparent.

**Note:** To make these settings universal for all forms of URxvt, you may add a wildcard. For example, `URxvt.depth` would become `URxvt*depth`.

### Native transparency

If there is no need for true transparency, or if compositing uses too many resources on your system, you can get transparency working in the following way:

 `~/.Xresources` 
```
! Xresources file

URxvt*inheritPixmap: true
URxvt*transparent: true
! URxvt*shading: 0 to 99 darkens, 101 to 200 lightens
URxvt*shading: 110

```

Using the URxvt*background setting exemplified above instead of URxvt*shading will also work.

**Note:** Avoid using shading if you have a `URxvt.tintColor` set. Use a different `tintColor` instead.

## Set icon

**Note:** Because of a bug report ([FS#34862](https://bugs.archlinux.org/task/34862)) complaining that the rxvt-unicode package had too many dependencies, you must now install the AUR package [rxvt-unicode-pixbuf](https://aur.archlinux.org/packages/rxvt-unicode-pixbuf/) in order to use the icon option.

By default URxvt does not feature a taskbar icon. However, this can be easily changed by adding the following line to `~/.Xresources` and pointing to the desired icon:

```
URxvt.iconFile:    /usr/share/icons/Clarity/scalable/apps/terminal.svg

```

## Use urxvt as application launcher

urxvt can be used as a lightweight alternative to application launchers such as [gmrun](https://www.archlinux.org/packages/?name=gmrun). Run urxvt with the following configuration to imitate look and behaviour of an application launcher or assign the command to a custom alias:

```
$ urxvt -geometry 80x3 -name 'bashrun' -e sh -c "/bin/bash -i -t"

```

## Xterm escape sequences

It is possible for rxvt-unicode to mimic the [Xterm](/index.php/Xterm "Xterm") escape sequences. These can be found for arbitrary key combinations by running `cat -v` inside *xterm*, then bound in *urxvt* using keysyms.

Take this word by word movement binding as an example:

 `~/.Xresources` 
```
!Xterm escapes, word by word movement
URxvt.keysym.Control-Left:    \033[1;5D
URxvt.keysym.Control-Right:    \033[1;5C

```

For more information, see ascii(7) and the keysym section of the urxvt(1) man page.

## Bidirectional support

It is possible to add bidirectional support for languages like Hebrew or Arabic using the extension: [urxvt-bidi](https://aur.archlinux.org/packages/urxvt-bidi/).

After installing it use it by either adding to your [Xresources](/index.php/Xresources "Xresources") file:

```
URxvt.perl-ext: [other extensions],bidi
URxvt.bidi.enabled: 1

```

Or run urxvt as follows:

```
urxvt -pe bidi

```

**Note:** The font you're using should support your language. For example, for viewing Hebrew you should a font like terminus.

## Bell Command

It is possible to execute a shell command when the terminal rings the bell. The pre-packed `bell-command` extension needs to be enabled first in the `~/.Xresources` file:

```
 URxvt.perl-ext-common: ...,bell-command,...

```

The following example will use [ALSA](/index.php/ALSA "ALSA")'s `aplay` command to play a `.wav` file:

```
 URxvt.bell-command: aplay /path/to/a/file.wav

```

And the next setting will pop a visual notification:

```
 URxvt.bell-command: notify-send "rxvt-unicode: bell!"

```

**Note:** Setting the `bell-command` option alone will not mute the buzzer in your computer, to do that take a look at the [PC speaker](/index.php/PC_speaker "PC speaker") article.