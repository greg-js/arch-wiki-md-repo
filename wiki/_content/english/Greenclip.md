Greenclip[[1]](https://github.com/erebe/greenclip) is a simple clipboard manager designed to be integrated with [rofi](/index.php/Rofi "Rofi") and written in Haskell.

## Installation

[Install](/index.php/Install "Install") [greenclip](https://aur.archlinux.org/packages/greenclip/) from [AUR](/index.php/AUR "AUR").

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

1.  Spawn the daemon `/usr/bin/greenclip daemon`
2.  Show entries as a list whithin [rofi](/index.php/Rofi "Rofi") using: `rofi -modi "clipboard:greenclip print" -show clipboard`
3.  The entry that you have selected will be in your [clipboard](/index.php/Clipboard "Clipboard") now
4.  Configuration file is placed in `~/.config/greenclip.cfg`
5.  To clear all clipboard history run `greenclip clear`

## Configuration example

 `~/.config/greenclip.cfg` 
```
Config {maxHistoryLength = 250, historyPath = "~/.cache/greenclip.history", staticHistoryPath = "~/.cache/greenclip.staticHistory", usePrimarySelectionAsInput = False}

```