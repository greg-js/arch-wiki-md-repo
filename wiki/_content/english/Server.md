Related articles

*   [Arch Linux VPS](/index.php/Arch_Linux_VPS "Arch Linux VPS")

This guide will give you an overview for the most common server options in existence and will outline some administration and security guidelines.

## Contents

*   [1 Preface](#Preface)
    *   [1.1 What is a server?](#What_is_a_server?)
    *   [1.2 Arch Linux as a server OS](#Arch_Linux_as_a_server_OS)
*   [2 Requirements](#Requirements)
*   [3 Services](#Services)
    *   [3.1 Zeroconf](#Zeroconf)
*   [4 Security](#Security)
*   [5 Administration and maintenance](#Administration_and_maintenance)
    *   [5.1 Remote administration](#Remote_administration)
    *   [5.2 Local Package Repositories](#Local_Package_Repositories)

## Preface

### What is a server?

In essence, a server is a computer that runs services that involve clients working on remote locations. All computers run services of some kind, for example: when using Arch as a desktop you will have a network service running to connect to a network. A server will, however, run services that involve external clients, for example: a web server will run a web site to be viewed via the Internet or elsewhere on a local network.

### Arch Linux as a server OS

Arch Linux comes as a minimal (but solid) base system, that can be easily turned into a server. You just need to install the desired server software and configure it. All the popular server software is available in the [official repositories](/index.php/Official_repositories "Official repositories"), and even more in the [AUR](/index.php/AUR "AUR"). The wiki also contains much detailed documentation regarding how to set up server software.

## Requirements

In most GNU/Linux server operating systems, you have two options:

*   A 'text' version of the OS (where everything is done from the command line)
*   A GUI version of the OS (where you get a desktop interface, such as [GNOME](/index.php/GNOME "GNOME")/[KDE](/index.php/KDE "KDE"), etc).

For the installation of Arch Linux, please refer to the [Installation guide](/index.php/Installation_guide "Installation guide") and [General recommendations](/index.php/General_recommendations "General recommendations") articles, but do not go any further than [General recommendations#Graphical user interface](/index.php/General_recommendations#Graphical_user_interface "General recommendations") unless you require a GUI.

If the server has a dynamic IP address but you still want to be able to reliably address it you can use a [dynamic DNS](/index.php/Dynamic_DNS "Dynamic DNS").

## Services

*   [SCP and SFTP](/index.php/SCP_and_SFTP "SCP and SFTP")

### Zeroconf

[Avahi](/index.php/Avahi "Avahi") is a free [Zero-configuration networking](https://en.wikipedia.org/wiki/Zero-configuration_networking "wikipedia:Zero-configuration networking") (zeroconf) implementation, including a system for multicast DNS/DNS-SD service discovery. It allows programs to publish and discover services and hosts running on a local network with no specific configuration. For example you can plug into a network and instantly find printers to print to, files to look at and people to talk to.

## Security

*   [Security](/index.php/Security "Security")
*   [Category:Security](/index.php/Category:Security "Category:Security")
*   [Category:Firewalls](/index.php/Category:Firewalls "Category:Firewalls")
*   [Secure Shell#Protection](/index.php/Secure_Shell#Protection "Secure Shell")
*   [SELinux](/index.php/SELinux "SELinux")
*   [AppArmor](/index.php/AppArmor "AppArmor")

## Administration and maintenance

### Remote administration

**[SSH](/index.php/SSH "SSH")** is the **S**ecure **SH**ell, it allows you to remotely connect to your server and administer commands as if you were physically at the computer. Combined with [GNU Screen](/index.php/GNU_Screen "GNU Screen"), SSH can become an invaluable tool for remote maintenance and administration while on-the-move. Please note that a standard SSH install is not very secure and some configuration is needed before the server can be considered locked-down. This configuration includes disabling root log-in, disabling password-based log-in and setting up firewall rules. In addition, you may supplement the security of your SSH daemon by utilizing daemons, such as [sshguard](/index.php/Sshguard "Sshguard") or [fail2ban](/index.php/Fail2ban "Fail2ban"), which constantly monitor the log files for any suspicious activity and ban IP addresses with too many failed log-in attempts.

**X Forwarding** is forwarding your X session via SSH so you can log in to the desktop GUI remotely. Use of this feature will require SSH and an X server to be installed on the server. You will also need to have a working X server installed on the client system you will be using to connect to the server with. More information can be found in the [X Forwarding](/index.php/SSH#X11_forwarding "SSH") section of the [SSH](/index.php/SSH "SSH") guide.

### Local Package Repositories

[Repose](https://github.com/vodik/repose) ([repose](https://www.archlinux.org/packages/?name=repose)) can be used to create a package repository for a local server cluster where packages must be tested for quality and reliability before undergoing deployment into a production environment.