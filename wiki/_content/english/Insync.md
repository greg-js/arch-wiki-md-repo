Related articles

*   [Dropbox](/index.php/Dropbox "Dropbox")

[insync](https://insynchq.com) is an alternative Google Drive client which is available for Windows, Mac OS X and Linux which allows you to sync a local folder or symlinked folders with your Google Drive. Whilst previous Beta versions used to be for free, the final release features a trial period after which a one-time payment per Google account is required.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
    *   [2.1 Running as a systemd service](#Running_as_a_systemd_service)
    *   [2.2 Cinnamon](#Cinnamon)
*   [3 Usage](#Usage)
    *   [3.1 Control via CLI](#Control_via_CLI)
*   [4 Troubleshooting](#Troubleshooting)
    *   [4.1 Slow sync process](#Slow_sync_process)
    *   [4.2 GUI not starting and failing silently](#GUI_not_starting_and_failing_silently)

## Installation

Install [insync](https://aur.archlinux.org/packages/insync/), available in the [AUR](/index.php/AUR "AUR"). It contains the synchronization daemon, a systemd service file and a command line utility for configuration. It can be used and integrates nicely with different desktop environments such as KDE, Gnome or Cinnamon.

## Configuration

**Note:** Starting Insync with the `--set-files-path` flag is no longer necessary. The aforementioned flag has been removed from recent Insync releases.

Insync can be started with the `insync start` command and stopped with the `insync quit` command. A shortcut for starting Insync should be available in the applications menu of your desktop environment.

### Running as a systemd service

[Enable](/index.php/Enable "Enable") `insync@<user>.service`.

### Cinnamon

When you start insync from the start menu it may not appear in the task bar. For that you need to add the task bar applet by right-click on your panel.

## Usage

The usage is self-explanatory. Copy files and folders from and to your local folder to sync it with your Google Drive.

### Control via CLI

See [How to control Insync via command line (CLI)](https://support.insynchq.com/t/how-to-control-insync-via-command-line-cli/34).

## Troubleshooting

### Slow sync process

The default systemd service file provided in [insync](https://aur.archlinux.org/packages/insync/) uses the `--synchronous-full` flag to make sqlite transactions safer and prevent database corruption. However, for some users this might considerably slow down the sync process. If you do not need full synchronisation, create `/etc/systemd/system/insync@.service` to override the provided service file and modify the `ExecStart` variable:

 `/etc/systemd/system/insync@.service` 
```
.include /usr/lib/systemd/system/insync@.service
[Service]
ExecStart=/usr/bin/insync start

```

### GUI not starting and failing silently

When running `insync start`, the status tray icon does not appear and insync does not start.

According to [[1]](https://forums.insynchq.com/t/insync-arch-linux-not-starting-segfault-at-730-error-14/8893), this is due to `QGtkStyle`. You will need to set the Qt4 theme to something other than GTK using `qtconfig-qt4`.

This issue is sometimes observed when using the Nouveau driver for NVIDIA graphics cards, and can be resolved by using the proprietary [NVIDIA](/index.php/NVIDIA "NVIDIA") drivers.

Running `insync start --no-daemon` from the terminal logs output to stdout and prevents the process from being detached. This makes troubleshooting much simpler.