[Webfs](http://linux.bytesex.org/misc/webfs.html) is a simple HTTP server for mostly static content.

## Installation

[Install](/index.php/Install "Install") [webfs](https://www.archlinux.org/packages/?name=webfs).

## Configuration

The configuration file is `/etc/conf.d/webfsd`.

It is set up for systemd. Use systemctl to start, stop, enable, disable webfsd.service.

An example `/etc/conf.d/webfsd`.

```
#
# Parameters passed to webfsd(1)
#

WEBFSD_ARGS="-p 80 -u nobody -R /srv/http/"

```

If you have an `index.html` file with the main content of the website, add `-f index.html` to the arguments. Otherwise, *webfsd* generates a listing of the root directory by default.

## See also

*   `man webfsd`[[1]](https://manned.org/webfsd.1)