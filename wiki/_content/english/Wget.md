[GNU Wget](http://www.gnu.org/software/wget/) is a free software package for retrieving files using [HTTP](/index.php/HTTP "HTTP"), HTTPS, [FTP](/index.php/FTP "FTP") and FTPS *(FTPS since version 1.18)*. It is a non-interactive commandline tool, so it may easily be called from scripts.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
    *   [2.1 FTP automation](#FTP_automation)
    *   [2.2 Proxy](#Proxy)
    *   [2.3 pacman integration](#pacman_integration)
*   [3 Usage](#Usage)
    *   [3.1 Basic usage](#Basic_usage)
    *   [3.2 Archive a complete website](#Archive_a_complete_website)

## Installation

[Install](/index.php/Install "Install") the [wget](https://www.archlinux.org/packages/?name=wget) package. The [git](/index.php/Git "Git") version is present in the [AUR](/index.php/AUR "AUR") by the name [wget-git](https://aur.archlinux.org/packages/wget-git/).

## Configuration

Configuration is performed in `/etc/wgetrc`. Not only is the default configuration file well documented; altering it is seldom necessary. See the man page for more intricate options.

### FTP automation

Normally, [SSH](/index.php/SSH "SSH") is used to securely transfer files among a network. However, FTP is lighter on resources compared to scp and [rsyncing](/index.php/Rsync "Rsync") over SSH. FTP is not secure, but when transfering large amounts of data inside a firewall protected environment on CPU-bound systems, using FTP can prove beneficial.

```
wget ftp://root:somepassword@10.13.X.Y//ifs/home/test/big/"*.tar"

3,562,035,200 74.4M/s   in 47s

```

In this case, Wget transfered a 3.3 GiB file at 74.4MB/second rate.

In short, this procedure is:

*   scriptable
*   faster than ssh
*   easily used by languages than can substitute string variables
*   [globbing](https://en.wikipedia.org/wiki/glob_(programming) capable

### Proxy

Wget uses the standard proxy environment variables. See [Proxy settings](/index.php/Proxy_settings "Proxy settings").

To use the proxy authentication feature:

```
$ wget --proxy-user "DOMAIN\USER" --proxy-password "PASSWORD" URL

```

Proxies that use HTML authentication forms are not covered.

### pacman integration

To have [pacman](/index.php/Pacman "Pacman") automatically use Wget and a proxy with authentication, place the Wget command into `/etc/pacman.conf`, in the `[options]` section:

```
XferCommand = /usr/bin/wget --proxy-user "domain\user" --proxy-password="password" --passive-ftp -q --show-progress -c -O %o %u

```

**Warning:** Be aware that storing passwords in plain text is not safe. Make sure that only root can read this file with `chmod 600 /etc/pacman.conf`.

## Usage

This section explains some of the use case scenarios for Wget.

### Basic usage

One of the most basic and common use cases for Wget is to download a file from the internet.

```
$ wget <url>

```

When you already know the URL of a file to download, this can be much faster than the usual routine downloading it on your browser and moving it to the correct directory manually. Needless to say, just from the simplest usage, you can probably see a few ways of utilising this for some automated downloading if that's what you want.

### Archive a complete website

Wget can archive a complete website whilst preserving the correct link destinations by changing absolute links to relative links.

```
$ wget -np -r -k 'http://your-url-here'

```