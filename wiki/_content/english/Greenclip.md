[Greenclip](https://github.com/erebe/greenclip) is a simple [clipboard manager](/index.php/Clipboard_manager "Clipboard manager") designed to be integrated with [rofi](/index.php/Rofi "Rofi") and written in Haskell.

## Installation

[Install](/index.php/Install "Install") [rofi-greenclip](https://aur.archlinux.org/packages/rofi-greenclip/) from [AUR](/index.php/AUR "AUR").

To integrate the daemon start-up on boot is it possibile to create a service:

 `/usr/lib/systemd/user/greenclip.service` 
```
[Unit]
Description=Start greenclip daemon
After=display-manager.service

[Service]
ExecStart=/usr/bin/greenclip daemon
Restart=always

[Install]
WantedBy=default.target

```

Enable the service to start at boot:

`systemctl --user enable greenclip.service`

## Usage

1.  Spawn the daemon with `/usr/bin/greenclip daemon` or start/enable the service `systemctl --user start greenclip.service`
2.  Show entries as a list whithin [rofi](/index.php/Rofi "Rofi") using: `rofi -modi "clipboard:greenclip print" -show clipboard -run-command '{cmd}'`
3.  The entry that you have selected will be in your [clipboard](/index.php/Clipboard "Clipboard") now
4.  Configuration file is placed in `~/.config/greenclip.cfg`
5.  To clear all clipboard history run `greenclip clear`

## Configuration example

 `~/.config/greenclip.cfg` 
```
Config {
 maxHistoryLength = 250,
 historyPath = "~/.cache/greenclip.history",
 staticHistoryPath = "~/.cache/greenclip.staticHistory",
 imageCachePath = "/tmp/",
 usePrimarySelectionAsInput = False,
 blacklistedApps = [],
 trimSpaceFromSelection = True
}

```