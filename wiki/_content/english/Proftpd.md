[proFtpd](http://proftpd.org/) (Pro FTP daemon) is a highly feature rich FTP server, exposing large amount of configuration options to the user.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
    *   [2.1 Anonymous access](#Anonymous_access)
*   [3 See also](#See_also)

## Installation

[proftpd](https://aur.archlinux.org/packages/proftpd/) is available in the AUR. [Enable](/index.php/Enable "Enable") and start `proftpd.service`.

## Configuration

The [configuration file](http://www.proftpd.org/docs/howto/ConfigFile.html) is available at `/etc/proftpd.conf`. The project's website has an extensive [documentation](http://www.proftpd.org/docs/).

### Anonymous access

To head off a common problem, for anonymous access to work with `/bin/false` as the shell for the ftp user (the default configuration), you must add the line `RequireValidShell off` to `/etc/proftpd.conf`. Otherwise anonymous logins will receive a 530 error.

## See also

*   [BLFS: ProFTPD](http://www.linuxfromscratch.org/blfs/view/7.6/server/proftpd.html)