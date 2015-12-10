# Create A Home Cloud Server

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

With Arch Linux, you can easily make a home cloud server, to replace web-based data storage. This lets you store your data on your own computer, and have it be accessible across platforms.

## Contents

*   [1 Basic home cloud server components](#Basic_home_cloud_server_components)
*   [2 Prerequisites](#Prerequisites)
*   [3 Installation](#Installation)
*   [4 Extras](#Extras)

## Basic home cloud server components

*   A SMB server for file sharing
*   Zeroconf for service discovery
*   WebDAV for remote iPhone/web based file sharing
*   SSH / SFTP for remote access and file sharing
*   CardDAV/ConDAV for calendar, reminder, and contact sharing
*   A DLNA server for sharing music and photos with TVs and video game consoles

## Prerequisites

*   An IP address. For example a static IP address/ domain name, or something like [No-Ip](http://www.noip.com)
*   You'll need to know how to set up your firewall for port forwarding.

## Installation

*   Follow the [Installation guide](/index.php/Installation_guide "Installation guide")
*   Set up a [LAMP](/index.php/LAMP "LAMP") stack (Apache + Mysql + PHP)
*   Set up [PostgreSQL](/index.php/PostgreSQL "PostgreSQL") (for davical)
*   Install [Avahi](/index.php/Avahi "Avahi") (for zeroconf)
*   [Samba](/index.php/Samba "Samba")
*   [DAViCal](/index.php/DAViCal "DAViCal") / Webical - Make sure to check the user comments at [AUR](https://aur.archlinux.org/packages/davical/) and the [davical](http://www.davical.org) website, for help.
*   [SSH](/index.php/SSH "SSH")
*   [MiniDLNA](/index.php/MiniDLNA "MiniDLNA")

## Extras

Once you've got the base setup down, there's lots of other cool, optional stuff you can do, such as:

*   Set up [BIND](/index.php/BIND "BIND") so you can have a nameserver and DNS cache for your local network
*   Set up a web cache, for example with [Squid](/index.php/Squid "Squid")
*   Locally host your email and notes, for example via a [Simple Virtual User Mail System](/index.php/Simple_Virtual_User_Mail_System "Simple Virtual User Mail System")

Retrieved from "[https://wiki.archlinux.org/index.php?title=Create_A_Home_Cloud_Server&oldid=388020](https://wiki.archlinux.org/index.php?title=Create_A_Home_Cloud_Server&oldid=388020)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [Web server](/index.php/Category:Web_server "Category:Web server")