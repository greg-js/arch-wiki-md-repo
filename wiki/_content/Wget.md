# Wget

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

GNU Wget is a free software package for retrieving files using HTTP, HTTPS and FTP, the most widely-used Internet protocols. It is a non-interactive commandline tool, so it may easily be called from scripts, cron jobs, terminals without X-Windows support, etc. [[source](http://www.gnu.org/software/wget/)]

## Contents

*   [1 Installing](#Installing)
*   [2 Configuring](#Configuring)
    *   [2.1 FTP automation](#FTP_automation)
    *   [2.2 Proxy](#Proxy)
    *   [2.3 pacman integration](#pacman_integration)
*   [3 Usage](#Usage)
    *   [3.1 Basic usage](#Basic_usage)
    *   [3.2 Archive a complete website](#Archive_a_complete_website)

## Installing

wget is normally installed as part of the base setup. If not present, install the [wget](https://www.archlinux.org/packages/?name=wget) package using [pacman](/index.php/Pacman "Pacman"). The git version is present in the AUR by the name [wget-git](https://aur.archlinux.org/packages/wget-git/)<sup><small>AUR</small></sup>.

## Configuring

Configuration is performed in `/etc/wgetrc`. Not only is the default configuration file well documented; altering it is seldom necessary. See the man page for more intricate options.

### FTP automation

Normally, [SSH](/index.php/SSH "SSH") is used to securely transfer files among a network. However, FTP is lighter on resources compared to scp and [rsyncing](/index.php/Rsync "Rsync") over SSH. FTP is not as secure, but when transfering large amounts of data inside a firewall protected environment on CPU-bound systems, using FTP can prove beneficial.

```
wget ftp://root:somepassword@10.13.X.Y//ifs/home/test/big/"*.tar"

3,562,035,200 74.4M/s   in 47s

```

In this case, Wget transfered a 3.3 G file at 74.4MB/second rate.

In short, this procedure is:

*   scriptable
*   faster than ssh
*   easily used by languages than can substitute string variables
*   globbing capable

### Proxy

Wget uses the standard proxy environment variables. See: [Proxy settings](/index.php/Proxy_settings "Proxy settings")

To use the proxy authentication feature:

```
$ wget --proxy-user "DOMAIN\USER" --proxy-password "PASSWORD" URL

```

Proxies that use HTML authentication forms are not covered.

### pacman integration

To have [pacman](/index.php/Pacman "Pacman") automatically use Wget and a proxy with authentication, place the Wget command into `/etc/pacman.conf`, in the `[options]` section:

```
XferCommand = /usr/bin/wget --proxy-user "domain\user" --proxy-password="password" --passive-ftp -q --show-progress -c -O %o %u

```

**Warning:** be aware that storing passwords in plain text is not safe. Make sure that only root can read this file with `chmod 600 /etc/pacman.conf`.

## Usage

This section explains some of the use case scenarios for Wget.

### Basic usage

One of the most basic and common use cases for Wget is to download a file from the internet. For example, to download [a picture of a gnu from Wikipedia](https://upload.wikimedia.org/wikipedia/commons/f/fb/Blue_Wildebeest%2C_Ngorongoro.jpg), you can type:

```
$ wget https://upload.wikimedia.org/wikipedia/commons/f/fb/Blue_Wildebeest%2C_Ngorongoro.jpg

```

When you already know the URL of a file to download, this can be much faster than the usual routine downloading it on your browser and moving it to the correct directory manually. Needless to say, just from the simplest usage, you can probably see a few ways of utilising this for some automated downloading if that's what you want.

### Archive a complete website

Wget can archive a complete website whilst preserving the correct link destinations by changing absolute links to relative links.

```
$ wget -np -r -k 'http://your-url-here'

```

Retrieved from "[https://wiki.archlinux.org/index.php?title=Wget&oldid=408322](https://wiki.archlinux.org/index.php?title=Wget&oldid=408322)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [Internet applications](/index.php/Category:Internet_applications "Category:Internet applications")