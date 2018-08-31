[cmus](https://cmus.github.io/) *(C* MUsic Player)* is a small, fast and powerful console audio player which supports most major audio formats. Various features include gapless playback, ReplayGain support, MP3 and Ogg streaming, live filtering, instant startup, customizable key-bindings, and vi-style default key-bindings.

## Contents

*   [1 Installation](#Installation)
    *   [1.1 Using cmus with ALSA](#Using_cmus_with_ALSA)
*   [2 Usage](#Usage)
*   [3 Configuration](#Configuration)
    *   [3.1 Remote Control](#Remote_Control)
*   [4 See also](#See_also)

## Installation

[Install](/index.php/Install "Install") the [cmus](https://www.archlinux.org/packages/?name=cmus) package, or [cmus-git](https://aur.archlinux.org/packages/cmus-git/) for the development version.

See the optional dependencies for available [codecs](/index.php/Codecs "Codecs") and output plugins (installed can be listed with `cmus --plugins`).

### Using cmus with ALSA

[Install](/index.php/Install "Install") the [alsa-lib](https://www.archlinux.org/packages/?name=alsa-lib) package.

When using cmus with [ALSA](/index.php/ALSA "ALSA") the default configuration does not allow playing music. What you might encounter when trying to start cmus is a blank terminal line with no output whatsoever. To fix it, create a new config file and set the following variables

 `~/.config/cmus/rc` 
```
set output_plugin=alsa
set dsp.alsa.device=default
set mixer.alsa.device=default
set mixer.alsa.channel=Master
```

## Usage

See [cmus(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/cmus.1), [cmus-tutorial(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/cmus-tutorial.1) and [cmus-remote(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/cmus-remote.1).

## Configuration

To configure cmus start it and switch to the configuration tab by pressing `7`. Now you can see a list of default keybindings. Select a field in the list with the arrow keys and press`Enter` to edit the values. You can also remove bindings with `D` or `del`. To edit unbound commands and option variables scroll down in the list to the relevant section. Variables can also be toggled instead of edited with `space`. Cmus allows changing the color of nearly every interface element. You can prefix colors with "light" to make them appear brighter and set attributes for some text elements.

### Remote Control

Cmus can be controlled externally through a unix-socket with `cmus-remote`. This makes it easy to control playback through an external application or key-binding.

One such usage of this feature is to control playback in Cmus with the XF86 keyboard events. The following script when run will start Cmus in an xterm terminal if it is not running, otherwise it will will toggle play/pause:

```
#!/bin/sh

if ! pgrep -x cmus ; then
  xterm -e cmus
else
  cmus-remote -u
fi
```

Copy the code above into a file `~/bin/cplay` and make it [executable](/index.php/Executable "Executable").

To use cmus-remote in [Openbox](/index.php/Openbox "Openbox"), edit `~/.config/openbox/rc.xml` and change the following key-bindings to look like this:

**Note:** Make sure there are no conflicting keybindings in `rc.xml`
 `~/.config/openbox/rc.xml` 
```
  <keyboard>
    <keybind key="XF86AudioPlay">
      <action name="Execute">
        <command>cmus-remote -u</command>
      </action>
    </keybind>
    <keybind key="XF86AudioNext">
      <action name="Execute">
        <command>cmus-remote -n</command>
      </action>
    </keybind>
    <keybind key="XF86AudioPrev">
      <action name="Execute">
        <command>cmus-remote -r</command>
      </action>
    </keybind>
  </keyboard>

```

Now when you use the `XF86AudioPlay` key on your keyboard, cmus will open up. If it is opened already it will then start playing. Using the XF86AudioNext and XF86AudioPrev keys will change tracks.

## See also

*   [Git Repository](https://github.com/cmus/cmus)
*   [Website](https://cmus.github.io/)
*   [User submitted scripts](https://github.com/cmus/cmus/wiki)