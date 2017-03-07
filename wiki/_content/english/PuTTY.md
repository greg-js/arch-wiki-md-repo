[PuTTY](http://www.chiark.greenend.org.uk/~sgtatham/putty/) is a port of the popular GUI SSH, Telnet, Rlogin and serial port connection client for Windows. It has support for advanced logging and termcap options, as well as a very configurable appearance and the ability to forward ports or create a SOCKS tunnel through an SSH destination. To start, simply run PuTTY, type the hostname of the host you would like to connect to and hit Open.

## Installation

[Install](/index.php/Install "Install") [putty](https://www.archlinux.org/packages/?name=putty). For a menu item and icon, install [putty-freedesktop](https://aur.archlinux.org/packages/putty-freedesktop/) from the [AUR](/index.php/AUR "AUR").

## Configuration

The settings can be modified through the tabs on the left, however they will be reset if not saved. To save your settings type a name into the box under Saved Sessions and click save. To load it again later, click the name of your save and click load. This allows you to persist your visual, termcap and connection settings between connections and also lets you keep one save per regularly used host. The save "Default Settings" is automatically loaded every time you start PuTTY, so save under that name with care.

**Tip:** PuTTY gained support for ECDSA, Ed25519 and other standard [SSH key types](/index.php/SSH_keys "SSH keys") with version 0.68 (February 2017).[[1]](http://www.chiark.greenend.org.uk/~sgtatham/putty/changes.html) Test it and remove eventual fallbacks to legacy key types you used.

## 256 color support

*Settings > Connection > Data : Terminal-type string = putty-256color*

To test color support, execute the following command: [reference](http://www.commandlinefu.com/commands/view/5879/show-numerical-values-for-each-of-the-256-colors-in-bash)

```
for code in {0..255}; do echo -e "\e[38;05;${code}m $code: Test"; done

```

See [256colours](http://www.robmeerman.co.uk/unix/256colours) for details.