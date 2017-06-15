EXWM is a [window manager](/index.php/Window_manager "Window manager") based on [Emacs](/index.php/Emacs "Emacs").

## Contents

*   [1 Installing](#Installing)
*   [2 Configuration](#Configuration)
    *   [2.1 Multi-monitor](#Multi-monitor)
    *   [2.2 System tray](#System_tray)
    *   [2.3 Compositing manager](#Compositing_manager)
*   [3 Troubleshooting](#Troubleshooting)
    *   [3.1 Screen tearing in Firefox](#Screen_tearing_in_Firefox)
*   [4 See also](#See_also)

## Installing

Make sure you have [emacs](https://www.archlinux.org/packages/?name=emacs) installed. You will also need [xorg-xinit](https://www.archlinux.org/packages/?name=xorg-xinit).

Install EXWM from within Emacs: `M-x package-install exwm RET`.

Edit [xinitrc](/index.php/Xinitrc "Xinitrc") and add:

```
exec emacs

```

In your emacs init file, add:

```
(require 'exwm)
(require 'exwm)
(exwm-config-default)

```

to use the default settings. If you want to use your own settings, use `(exwm-enable)` instead of `(exwm-config-default)` (and you may not need to `(require 'exwm-config)`).

## Configuration

EXWM is a full X window manager, so Emacs manages X windows such as your browser, vlc, etc. You may use all the normal Emacs window commands to control window placement. In X windows (i.e. not "normal" Emacs buffers), some commands are caught by EXWM and not passed through to the program. These keys are store in `exwm-input-prefix-keys`. Alternatively, you can set global commands by using the `exwm-input-set-key` function. For example, to use s-& as a keyboard shortcut to launch a program (e.g. firefox), you can do:

```
(exwm-input-set-key (kbd "s-&")
                    (lambda (command)
                      (interactive (list (read-shell-command "$ ")))
                      (start-process-shell-command command nil command)))

```

### Multi-monitor

EXWM can handle multi-monitor through the (optional) `exwm-randr` package. You will need to install [xrandr](/index.php/Xrandr "Xrandr") and enable exwm-randr in your emacs configuration file before calling `(exwm-enable)`. You will need to adjust the values of "DP-1" and "DP-2" to the values your computer uses; call `xrandr` at the command line with no arguments to see available outputs.

```
(require 'exwm-randr)
(setq exwm-randr-workspace-output-plist '(1 "DP-1"))
(add-hook 'exwm-randr-screen-change-hook
          (lambda ()
            (start-process-shell-command
             "xrandr" nil "xrandr --output DP-1 --right-of DP-2 --auto")))
(exwm-randr-enable)

```

### System tray

EXWM supports a system tray, but it is not enabled by default. To enable it, put the following before `(exwm-enable)` in your dotemacs file:

```
(require 'exwm-systemtray)
(exwm-systemtray-enable)

```

You may need to adjust the height afterwards; this can be adjusted with the `exwm-systemtray-height` variable.

### Compositing manager

**Warning:** The compositing manager may cause issues. If EXWM slows to a crawl, try turning off the cm

EXWM includes a compositing manager, but it is not enabled by default. To enable it, load the followng:

```
(require 'exwm-cm)
(exwm-cm-enable)

```

Alternatively, you may start/stop the compositing manager manually by omitting `(exwm-cm-enable)` and instead calling `exwm-cm-start` or `exwm-cm-stop` manually.

## Troubleshooting

### Screen tearing in Firefox

Try turning off smooth scrolling in Preferences > Advanced > Use Smooth Scrolling

## See also

*   [EXWM wiki](https://github.com/ch11ng/exwm/wiki)