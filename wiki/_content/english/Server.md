This guide will give you an overview for the most common server options in existence and will outline some administration and security guidelines.

## Contents

*   [1 Preface](#Preface)
    *   [1.1 What is a server?](#What_is_a_server.3F)
    *   [1.2 Arch Linux as a server OS](#Arch_Linux_as_a_server_OS)
*   [2 Requirements](#Requirements)
*   [3 Basic set-up](#Basic_set-up)
    *   [3.1 SSH](#SSH)
    *   [3.2 LAMP](#LAMP)
*   [4 Additional web-services](#Additional_web-services)
    *   [4.1 E-Mail](#E-Mail)
    *   [4.2 FTP](#FTP)
    *   [4.3 DAViCal](#DAViCal)
    *   [4.4 WebDAV](#WebDAV)
    *   [4.5 DLAN](#DLAN)
    *   [4.6 Web cache](#Web_cache)
*   [5 Local Network Services](#Local_Network_Services)
    *   [5.1 Zeroconf](#Zeroconf)
    *   [5.2 CUPS (printing)](#CUPS_.28printing.29)
    *   [5.3 DHCP](#DHCP)
    *   [5.4 Samba (Windows-compatible file and printer sharing)](#Samba_.28Windows-compatible_file_and_printer_sharing.29)
    *   [5.5 DNS](#DNS)
*   [6 Security](#Security)
    *   [6.1 Firewall](#Firewall)
    *   [6.2 Protecting SSH](#Protecting_SSH)
    *   [6.3 SELinux](#SELinux)
*   [7 Administration and maintenance](#Administration_and_maintenance)
    *   [7.1 Accessibility](#Accessibility)
    *   [7.2 Local Package Repositories](#Local_Package_Repositories)
*   [8 See also](#See_also)

## Preface

### What is a server?

In essence, a server is a computer that runs services that involve clients working on remote locations. All computers run services of some kind, for example: when using Arch as a desktop you will have a network service running to connect to a network. A server will, however, run services that involve external clients, for example: a web server will run a web site to be viewed via the Internet or elsewhere on a local network.

### Arch Linux as a server OS

You may have seen the comments or claims: *Arch Linux was never intended as a server operating system!* This is correct: there is no server installation disc available, *per se*, such as those you may find for other distributions. This is because Arch Linux comes as a minimal (but solid) base system, with very few desktop or server features pre-installed. This does not mean you should not use Arch Linux as a server; **quite the contrary**. Arch's core installation is a secure and capable foundation. Since only a small number of features come pre-installed, this core installation can easily be used as a basis for a Linux server. All the popular server software ([Apache](/index.php/Apache "Apache"), [MySQL](/index.php/MySQL "MySQL")/[MariaDB](/index.php/MariaDB "MariaDB"), [PHP](/index.php/PHP "PHP"), [Samba](/index.php/Samba "Samba"), and plenty more) is available in the official repository, and even more is available on the [AUR](/index.php/AUR "AUR"). The wiki also contains much detailed documentation regarding how to get set up with this software.

## Requirements

For using Arch Linux on a server, you will need to have an Arch Linux [installation](/index.php/Installation_guide "Installation guide") ready.

In most GNU/Linux server operating systems, you have two options:

*   A 'text' version of the OS (where everything is done from the command line)
*   A GUI version of the OS (where you get a desktop interface, such as [GNOME](/index.php/GNOME "GNOME")/[KDE](/index.php/KDE "KDE"), etc).

**Note:** If you have services on your server that need to be administered using a GUI and cannot be done remotely, you must choose the second option.

For the installation of Arch Linux, please refer to the [Beginners' guide](/index.php/Beginners%27_guide "Beginners' guide") and [General recommendations](/index.php/General_recommendations "General recommendations") articles, but do not go any further than [this section](/index.php/General_recommendations#Graphical_user_interface "General recommendations") unless you require a GUI.

For remote access to this server, you need a static IP address/ domain name, or something like [No-Ip](http://www.noip.com).

## Basic set-up

So what is a "basic" set-up:

*   Remote access to the server.

We want to be able to remotely log-on to our server to perform several administrative tasks. When your server is located elsewhere or does not have a monitor attached: removing or adding files, changing configuration options and server rebooting are all tasks which are impossible to do without a way to log on to your server remotely. SSH nicely provides this functionality.

*   Your Arch **L**inux server.
*   A http server (**A**pache), required for serving web pages.
*   A database server (**M**ySql/**M**ariaDB), often required for storing data of address book-, forum- or blog scripts.
*   The **P**HP scripting language, a highly popular internet scripting language used in blogs, forums, content management systems and many other web-scripts.

As the bold letters suggest, there is a name for this combination of applications: LAMP.

The following sections will guide you through the installation and configuration of the above mentioned basic set-up features.

### SSH

SSH stands for **S**ecure **Sh**ell. SSH enables you to log on to your server through an SSH client, presenting you with a recognizable terminal-like interface. Users available on the system can be given access to log on remotely though SSH, thereby enabling remote administration of your server.

The [Arch wiki SSH page](/index.php/SSH "SSH") covers Installation and Configuration nicely.

### LAMP

A [LAMP](/index.php/LAMP "LAMP") server is a reasonably standard web server.

There are often disputes as to what the 'P' stands for, some people say it is [PHP](/index.php/PHP "PHP") some people say it is Perl while others say it is [Python](/index.php/Python "Python"). For the purposes of this guide I am going to make it PHP, although there are some nice Perl and Python modules for Linux so you may wish to install Perl or Python as well.

Having said that, it is by no means simple so there may be a lot to take in here.

Please refer to the [LAMP](/index.php/LAMP "LAMP") wiki page for instructions on installation and configuration.

## Additional web-services

### E-Mail

Please refer to pages in [Category:Mail server](/index.php/Category:Mail_server "Category:Mail server") for instructions on mail server installation and configuration.

### FTP

FTP stands for **F**ile **T**ransfer **P**rotocol. FTP is a service that can provide access to the file system from a remote location through an FTP client (FileZilla, gftp, etc.) or FTP-capable browser. Through FTP, you are able to add or remove files from a remote location, as well as apply some chmod commands to these files to set certain permissions.

FTP access will be related to user accounts available on the system, allowing simple rights management. FTP is a much used tool for adding files to a web server from a remote locations.

There are several FTP daemons available. See [List of applications#FTP servers](/index.php/List_of_applications#FTP_servers "List of applications") for a list of them.

There is also the option of FTP over SSH, or [SFTP](/index.php/SFTP "SFTP").

### DAViCal

[DAViCal](/index.php/DAViCal "DAViCal") is a server implementing the CalDAV and CardDAV protocol for calendar, reminder, and contact sharing.

### WebDAV

[WebDAV](/index.php/WebDAV "WebDAV")(Web Distributed Authoring and Versioning) is an extension of HTTP 1.1\. It contains a set of concepts and accompanying extension methods to allow read and write across the HTTP 1.1 protocol. Instead of using NFS or SMB, WebDAV offers file transfers via HTTP.

### DLAN

[ReadyMedia](/index.php/ReadyMedia "ReadyMedia") (previously **MiniDLNA**) is server software with the aim of being fully compliant with [DLNA](https://en.wikipedia.org/wiki/Digital_Living_Network_Alliance "wikipedia:Digital Living Network Alliance")/[UPnP](https://en.wikipedia.org/wiki/Universal_Plug_and_Play "wikipedia:Universal Plug and Play") clients to serves media files (music, pictures, and video) to clients on a network.

### Web cache

[Squid](/index.php/Squid "Squid") is a caching proxy for the Web supporting HTTP, HTTPS, FTP, and more. It reduces bandwidth and improves response times by caching and reusing frequently-requested web pages. Squid has extensive access controls and makes a great server accelerator.

## Local Network Services

### Zeroconf

[Avahi](/index.php/Avahi "Avahi") is a free [Zero-configuration networking](https://en.wikipedia.org/wiki/Zero-configuration_networking "wikipedia:Zero-configuration networking") (zeroconf) implementation, including a system for multicast DNS/DNS-SD service discovery. It allows programs to publish and discover services and hosts running on a local network with no specific configuration. For example you can plug into a network and instantly find printers to print to, files to look at and people to talk to.

### CUPS (printing)

CUPS, or **C**ommon **U**NIX **P**rinting **S**ystem, can provide a central point via which a number of users can print. For instance, you have several (say 3) printers and several people on a local network that wish to print. You can either add all these printers to every user's computer, or add all printers to a server running CUPS, and then simply adding the server to all clients. This allows for a central printing system that can be online 24/7, which is especially nice for printers that do not have networking capabilities.

Please refer to the [CUPS](/index.php/CUPS "CUPS") wiki page for instructions on installation and configuration.

### DHCP

**Note:** dhcp v4 does not currently work due to IPv6 issues, this part of the guide will be written when that issue is resolved.

### Samba (Windows-compatible file and printer sharing)

Samba is an open-source implementation of the SMB/CIFS networking protocols, effectively allowing you to share files and printers between Linux and Windows systems. Samba can provide public shares or require several forms of authentication.

Please refer to the [Samba](/index.php/Samba "Samba") wiki page for instructions on installation and configuration.

### DNS

[Category:Domain Name System](/index.php/Category:Domain_Name_System "Category:Domain Name System") contains many implementations of the Domain Name System (DNS) protocols.

## Security

### Firewall

Refer to [Firewalls](/index.php/Firewalls "Firewalls") for details regarding available firewall software.

### Protecting SSH

Allowing remote log-on through SSH is good for administrative purposes, but can pose a threat to your server's security. Often the target of brute force attacks, SSH access needs to be limited properly to prevent third parties gaining access to your server. See [Secure Shell#Protection](/index.php/Secure_Shell#Protection "Secure Shell") for how to configure it.

### SELinux

Please refer to the [SELinux](/index.php/SELinux "SELinux") wiki page for instructions on installation and configuration.

## Administration and maintenance

### Accessibility

**[SSH](/index.php/SSH "SSH")** is the **S**ecure **SH**ell, it allows you to remotely connect to your server and administer commands as if you were physically at the computer. Combined with [Screen](/index.php/Screen "Screen"), SSH can become an invaluable tool for remote maintenance and administration while on-the-move. Please note that a standard SSH install is not very secure and some configuration is needed before the server can be considered locked-down. This configuration includes disabling root log-in, disabling password-based log-in and setting up firewall rules. In addition, you may supplement the security of your SSH daemon by utilizing daemons, such as [sshguard](/index.php/Sshguard "Sshguard") or [fail2ban](/index.php/Fail2ban "Fail2ban"), which constantly monitor the log files for any suspicious activity and ban IP addresses with too many failed log-in attempts.

**X Forwarding** is forwarding your X session via SSH so you can log in to the desktop GUI remotely. Use of this feature will require SSH and an X server to be installed on the server. You will also need to have a working X server installed on the client system you will be using to connect to the server with. More information can be found in the [X Forwarding](/index.php/SSH#X11_forwarding "SSH") section of the [SSH](/index.php/SSH "SSH") guide.

### Local Package Repositories

[Repose](https://github.com/vodik/repose) can be used to create a package repository for a local server cluster where packages must be tested for quality and reliability before undergoing deployment into a production environment.

## See also

*   [Virtual Private Server](/index.php/Virtual_Private_Server "Virtual Private Server") - A list of VPS providers offering Arch