# Server

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
*   [5 Local Network Services](#Local_Network_Services)
    *   [5.1 CUPS (printing)](#CUPS_.28printing.29)
    *   [5.2 DHCP](#DHCP)
    *   [5.3 Samba (Windows-compatible file and printer sharing)](#Samba_.28Windows-compatible_file_and_printer_sharing.29)
*   [6 Security](#Security)
    *   [6.1 Firewall](#Firewall)
    *   [6.2 Protecting SSH](#Protecting_SSH)
    *   [6.3 SELinux](#SELinux)
*   [7 Administration and maintenance](#Administration_and_maintenance)
    *   [7.1 Accessibility](#Accessibility)
*   [8 Extras](#Extras)
    *   [8.1 phpMyAdmin](#phpMyAdmin)
*   [9 Local Package Repositories](#Local_Package_Repositories)
*   [10 Home cloud server](#Home_cloud_server)
    *   [10.1 Basic home cloud server components](#Basic_home_cloud_server_components)
    *   [10.2 Prerequisites](#Prerequisites)
    *   [10.3 Installation](#Installation)
    *   [10.4 Extras](#Extras_2)
*   [11 More Resources](#More_Resources)

## Preface

### What is a server?

In essence, a server is a computer that runs services that involve clients working on remote locations. All computers run services of some kind, for example: when using Arch as a desktop you will have a network service running to connect to a network. A server will, however, run services that involve external clients, for example: a web server will run a web site to be viewed via the Internet or elsewhere on a local network.

### Arch Linux as a server OS

You may have seen the comments or claims: _Arch Linux was never intended as a server operating system!_ This is correct: there is no server installation disc available, _per se_, such as those you may find for other distributions. This is because Arch Linux comes as a minimal (but solid) base system, with very few desktop or server features pre-installed. This does not mean you should not use Arch Linux as a server; **quite the contrary**. Arch's core installation is a secure and capable foundation. Since only a small number of features come pre-installed, this core installation can easily be used as a basis for a Linux server. All the popular server software ([Apache](/index.php/Apache "Apache"), [MySQL](/index.php/MySQL "MySQL")/[MariaDB](/index.php/MariaDB "MariaDB"), [PHP](/index.php/PHP "PHP"), [Samba](/index.php/Samba "Samba"), and plenty more) is available in the official repository, and even more is available on the [AUR](/index.php/AUR "AUR"). The wiki also contains much detailed documentation regarding how to get set up with this software.

## Requirements

For using Arch Linux on a server, you will need to have an Arch Linux installation ready.

In most GNU/Linux server operating systems, you have two options:

*   A 'text' version of the OS (where everything is done from the command line)
*   A GUI version of the OS (where you get a desktop interface, such as [GNOME](/index.php/GNOME "GNOME")/[KDE](/index.php/KDE "KDE"), etc).

**Note:** If you have services on your server that need to be administered using a GUI and cannot be done remotely, you must choose the second option.

For the installation of Arch Linux, please refer to the [Beginners' guide](/index.php/Beginners%27_guide "Beginners' guide") and [General recommendations](/index.php/General_recommendations "General recommendations") articles, but do not go any further than [this section](/index.php/General_recommendations#Graphical_user_interface "General recommendations") unless you require a GUI.

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

## Local Network Services

### CUPS (printing)

CUPS, or **C**ommon **U**NIX **P**rinting **S**ystem, can provide a central point via which a number of users can print. For instance, you have several (say 3) printers and several people on a local network that wish to print. You can either add all these printers to every user's computer, or add all printers to a server running CUPS, and then simply adding the server to all clients. This allows for a central printing system that can be online 24/7, which is especially nice for printers that do not have networking capabilities.

Please refer to the [CUPS](/index.php/CUPS "CUPS") wiki page for instructions on installation and configuration.

### DHCP

**Note:** dhcp v4 does not currently work due to IPv6 issues, this part of the guide will be written when that issue is resolved.

### Samba (Windows-compatible file and printer sharing)

Samba is an open-source implementation of the SMB/CIFS networking protocols, effectively allowing you to share files and printers between Linux and Windows systems. Samba can provide public shares or require several forms of authentication.

Please refer to the [Samba](/index.php/Samba "Samba") wiki page for instructions on installation and configuration.

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

## Extras

### phpMyAdmin

[phpMyAdmin](/index.php/PhpMyAdmin "PhpMyAdmin") is a free software tool written in PHP intended to handle the administration of MySQL over the Internet. phpMyAdmin supports a wide range of operations with MySQL. The most frequently used operations are supported by the user interface (managing databases, tables, fields, relations, indexes, users, permissions, etc), while you still have the ability to directly execute any SQL statement." [http://www.phpmyadmin.net/home_page/index.php](http://www.phpmyadmin.net/home_page/index.php)

## Local Package Repositories

[Repose](https://github.com/vodik/repose) can be used to create a package repository for a local server cluster where packages must be tested for quality and reliability before undergoing deployment into a production environment.

## Home cloud server

With Arch Linux, you can easily make a home cloud server, to replace web-based data storage. This lets you store your data on your own computer, and have it be accessible across platforms.

### Basic home cloud server components

*   A SMB server for file sharing
*   Zeroconf for service discovery
*   WebDAV for remote iPhone/web based file sharing
*   SSH / SFTP for remote access and file sharing
*   CardDAV/ConDAV for calendar, reminder, and contact sharing
*   A DLNA server for sharing music and photos with TVs and video game consoles

### Prerequisites

*   An IP address. For example a static IP address/ domain name, or something like [No-Ip](http://www.noip.com)
*   You'll need to know how to set up your firewall for port forwarding.

### Installation

*   Follow the [Installation guide](/index.php/Installation_guide "Installation guide")
*   Set up a [LAMP](/index.php/LAMP "LAMP") stack (Apache + Mysql + PHP)
*   Set up [PostgreSQL](/index.php/PostgreSQL "PostgreSQL") (for davical)
*   Install [Avahi](/index.php/Avahi "Avahi") (for zeroconf)
*   [Samba](/index.php/Samba "Samba")
*   [DAViCal](/index.php/DAViCal "DAViCal") / Webical - Make sure to check the user comments at [AUR](https://aur.archlinux.org/packages/davical/) and the [davical](http://www.davical.org) website, for help.
*   [SSH](/index.php/SSH "SSH")
*   [MiniDLNA](/index.php/MiniDLNA "MiniDLNA")

### Extras

Once you've got the base setup down, there's lots of other cool, optional stuff you can do, such as:

*   Set up [BIND](/index.php/BIND "BIND") so you can have a nameserver and DNS cache for your local network
*   Set up a web cache, for example with [Squid](/index.php/Squid "Squid")
*   Locally host your email and notes, for example via a [Simple Virtual User Mail System](/index.php/Simple_Virtual_User_Mail_System "Simple Virtual User Mail System")

## More Resources

*   [LAMP](/index.php/LAMP "LAMP")
*   [MySQL](/index.php/MySQL "MySQL") - ArchWiki article for MySQL
*   [Virtual Private Server](/index.php/Virtual_Private_Server "Virtual Private Server") - A list of VPS providers offering Arch
*   [https://mariadb.org/](https://mariadb.org/)
*   [https://www.apache.org/](https://www.apache.org/)
*   [https://www.php.net/](https://www.php.net/)

Retrieved from "[https://wiki.archlinux.org/index.php?title=Server&oldid=417223](https://wiki.archlinux.org/index.php?title=Server&oldid=417223)"