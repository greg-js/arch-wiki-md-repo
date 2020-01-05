Thinkorswim by TD Ameritrade (branded as "thinkorswim" and often referred to as "tos") is a trading platform for stock, options and futures traders.

## Installation

While no official support exists for Arch Linux specifically, there is a broad installation approach for most Linux distributions.

Install [jre8-openjdk](https://www.archlinux.org/packages/?name=jre8-openjdk) before proceeding. As per its installation page, thinkorswim requires Java 1.8.0_60 JRE to run.

[Download the thinkorswim installation script.](https://mediaserver.thinkorswim.com/installer/InstFiles/thinkorswim_installer.sh)

Execute the script by running:

```
# sh thinkorswim_installer.sh

```

When prompted, it is recommended to install thinkorswim into your `/home/$USER/thinkorswim` directory to avoid permissions issues, rather than `/opt/thinkorswim`.

## Configuration

Since thinkorswim is a Java application, creating a `.desktop` file in `/.local/share/applications` or `/usr/share/applications` is recommended as it enables application indexing.

Here is an example configuration. Replace the `$USER` parameter with your own username.

```
[Desktop Entry]
Type=Application
Name=thinkorswim
GenericName=Trading platform
Comment=Trading platform
Icon=thinkorswim
Exec=/home/$USER/thinkorswim/thinkorswim 
Path=/home/$USER/thinkorswim
Terminal=false
StartupNotify=true
Categories=Java;

```