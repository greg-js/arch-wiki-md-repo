EXWM is a [window manager](/index.php/Window_manager "Window manager") based on [Emacs](/index.php/Emacs "Emacs").

## Contents

*   [1 Installing](#Installing)
*   [2 Configuration](#Configuration)
    *   [2.1 Multi-monitor](#Multi-monitor)
    *   [2.2 System tray](#System_tray)
*   [3 Embedding within LXDE](#Embedding_within_LXDE)
    *   [3.1 lxsession-logout](#lxsession-logout)
*   [4 Troubleshooting](#Troubleshooting)
    *   [4.1 Screen tearing in Firefox](#Screen_tearing_in_Firefox)
*   [5 See also](#See_also)

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
(require 'exwm-config)
(exwm-config-default)

```

to use the default settings. If you want to use your own settings, use `(exwm-enable)` instead of `(exwm-config-default)` (and you do not need to `(require 'exwm-config)`).

It's also possible to start emacs in server mode and to start EXWM from commandline. See [https://github.com/ch11ng/exwm/issues/284](https://github.com/ch11ng/exwm/issues/284).

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

## Embedding within LXDE

EXWM can be used in place of openbox, allowing you to still use [LXDE](/index.php/LXDE "LXDE") session management tools.

Before doing this, make sure you have your init file for emacs already set up to run EXWM (see above)

First, run

```
lxsession-edit

```

and go to the Advanced Options tab. Replace openbox with emacs. Then, run

```
lxsession-default-apps

```

Go to the Core Applications tab, and ensure the Windows Manager option is also set to emacs.

Now, go to the Autostart tab and uncheck the pcmanfm --desktop option. You can choose to keep the lxpanel option checked if you would still like to use it.

Log out, select LXDE from your login manager, and it will load emacs and init your EXWM environment automatically.

### lxsession-logout

You can create the following function within emacs to log out, shutdown, or reboot cleanly from within a LXDE session:

```
(defun exwm-logout ()
  (interactive)
  (recentf-save-list)
  (save-some-buffers)
  (start-process-shell-command "logout" nil "lxsession-logout"))

```

This stores your recentf history to disk, prompts you to save, discard, or diff changes within unsaved buffers, then launches the logout manager. You can bind this function to any key within emacs.

## Troubleshooting

### Screen tearing in Firefox

Try turning off smooth scrolling in Preferences > Advanced > Use Smooth Scrolling

## See also

*   [EXWM wiki](https://github.com/ch11ng/exwm/wiki)