From the project [home page](https://aria2.github.io/):

	*aria2 is a lightweight multi-protocol & multi-source command-line download utility. It supports [HTTP](https://en.wikipedia.org/wiki/HTTP and [Metalink](https://en.wikipedia.org/wiki/Metalink "wikipedia:Metalink"). aria2 can be manipulated via built-in [JSON-RPC](https://en.wikipedia.org/wiki/JSON-RPC "wikipedia:JSON-RPC") and [XML-RPC](https://en.wikipedia.org/wiki/XML-RPC "wikipedia:XML-RPC") interfaces.*

## Contents

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
    *   [2.1 aria2.conf](#aria2.conf)
    *   [2.2 Example aria2.conf](#Example_aria2.conf)
        *   [2.2.1 Option details](#Option_details)
            *   [2.2.1.1 Example input file #1](#Example_input_file_.231)
            *   [2.2.1.2 Example input file #2](#Example_input_file_.232)
        *   [2.2.2 Additional notes](#Additional_notes)
    *   [2.3 Example aria2.rapidshare](#Example_aria2.rapidshare)
        *   [2.3.1 Option details](#Option_details_2)
        *   [2.3.2 Additional notes](#Additional_notes_2)
    *   [2.4 Example aria2.bittorrent](#Example_aria2.bittorrent)
        *   [2.4.1 Option details](#Option_details_3)
    *   [2.5 Example aria2.daemon](#Example_aria2.daemon)
*   [3 Frontends](#Frontends)
    *   [3.1 Web UIs](#Web_UIs)
    *   [3.2 Other UIs](#Other_UIs)
*   [4 Tips and tricks](#Tips_and_tricks)
    *   [4.1 Download the packages without installing them](#Download_the_packages_without_installing_them)
    *   [4.2 pacman XferCommand](#pacman_XferCommand)
    *   [4.3 Changing the User Agent](#Changing_the_User_Agent)
    *   [4.4 Using Aria2 with makepkg](#Using_Aria2_with_makepkg)
*   [5 See also](#See_also)

## Installation

[Install](/index.php/Install "Install") the [aria2](https://www.archlinux.org/packages/?name=aria2) package.

You may also want to install [aria2-systemd](https://github.com/GutenYe/systemd-units/tree/master/aria2) to use aria2 as [daemon](/index.php/Daemon "Daemon").

**Note:** The executable name for the aria2 package is `aria2c`. This legacy naming convention has been retained for backwards compatibility.

## Configuration

### aria2.conf

aria2 looks to `$XDG_CONFIG_HOME/aria2/aria2.conf` for a set of global configuration options by default. This behavior can be modified with the `--conf-path` switch:

*   Download `aria2.example.rar` using the options specified in the configuration file `/file/aria2.rapidshare`

```
$ aria2c --conf-path=/file/aria2.rapidshare http://rapidshare.com/files/12345678/aria2.example.rar

```

If `$XDG_CONFIG_HOME/aria2/aria2.conf` exists and the options specified in `/file/aria2.rapidshare` are desired, the `--no-conf` switch must be appended to the command:

*   Do not use the default configuration file and download `aria2.example.rar` using the options specified in the configuration file `/file/aria2.rapidshare`

```
$ aria2c --no-conf --conf-path=/file/aria2.rapidshare http://rapidshare.com/files/12345678/aria2.example.rar

```

If `$XDG_CONFIG_HOME/aria2/aria2.conf` does not yet exist and you wish to simplify the management of configuration options:

```
$ touch $XDG_CONFIG_HOME/aria2/aria2.conf

```

### Example aria2.conf

```
continue
dir=${HOME}/Desktop
file-allocation=none
input-file=${HOME}/.aria2/input.conf
log-level=warn
max-connection-per-server=4
min-split-size=5M
on-download-complete=exit

```

This is essentially the same as if running the following:

```
$ aria2c dir=${HOME}/Desktop file-allocation=none input-file=${HOME}/.aria2/input.conf on-download-complete=exit log-level=warn FILE

```

**Note:** The example aria2.conf above may incorrectly use the $HOME variable. Some users have reported the curly brace syntax to explicitly create a separate ${HOME} subdirectory in the aria2 working directory. Such a directory may be difficult to traverse as bash will consider it to be the $HOME environment variable. For now, it is recommended to use absolute path names in aria2.conf.

#### Option details

	`continue`

	Continue downloading a partially downloaded file if a corresponding control file exists.

	`dir=${HOME}/Desktop`

	Store the downloaded file(s) in `~/Desktop`.

	`file-allocation=none`

	Do not pre-allocate disk space before downloading begins. (Default: prealloc) 

	`input-file=${HOME}/.aria2/input.conf`

	Download a list of line, or TAB separated URIs found in `~/.aria2/input.conf`

	`log-level=warn`

	Set log level to output warnings and errors only. (Default: debug)

	`max-connection-per-server=4`

	Set a maximum of four (4) connections to each server per file. (Default: 1)

	`min-split-size=5M`

	Only split the file if the size is larger than 2*5MB = 10MB. (Default: 20M)

	`on-download-complete=exit`

	Run the `exit` command and exit the shell once the download session is complete.

##### Example input file #1

*   Download `aria2-1.10.0.tar.bz2` from two separate sources to `~/Desktop` before merging as `aria2-1.10.0.tar.bz2`

```
http://aria2.net/files/stable/aria2-1.10.0/aria2-1.10.0.tar.bz2    http://sourceforge.net/projects/aria2/files/stable/aria2-1.10.0/aria2-1.10.0.tar.bz2

```

##### Example input file #2

*   Download `aria2-1.9.5.tar.bz2` and save to `/file/old` as `aria2.old.tar.bz2` &
*   Download `aria2-1.10.0.tar.bz2` and save to `~/Desktop` as `aria2.new.tar.bz2`

```
http://aria2.net/files/stable/aria2-1.9.5/aria2-1.9.5.tar.bz2
  dir=/file/old
  out=aria2.old.tar.bz2
http://aria2.net/files/stable/aria2-1.10.0/aria2-1.10.0.tar.bz2
  out=aria2.new.tar.bz2

```

#### Additional notes

	 `--file-allocation=falloc`

	Recommended for newer file systems such as ext4 (with extents support), btrfs or xfs as it allocates large files (GB) almost instantly. Do not use falloc with legacy file systems such as ext3 as prealloc consumes approximately the same amount of time as standard allocation would while locking the aria2 process from proceeding to download.

**Tip:** See `aria2c --help=#all` and the aria2 man page for a complete list of configuration options.

### Example aria2.rapidshare

```
http-user=USER_NAME
http-passwd=PASSWORD
allow-overwrite=true
dir=/file/Downloads
file-allocation=falloc
enable-http-pipelining=true
input-file=/file/input.rapidshare
log-level=error
max-connection-per-server=2
summary-interval=120

```

#### Option details

	`http-user=USER_NAME`

	Set HTTP [username](https://en.wikipedia.org/wiki/User_(computing) as USER_NAME for password-protected logins. This affects all [URIs](https://en.wikipedia.org/wiki/Uniform_Resource_Identifier "wikipedia:Uniform Resource Identifier").

	`http-passwd=PASSWORD`

	Set HTTP [password](https://en.wikipedia.org/wiki/Password "wikipedia:Password") as PASSWORD for password-protected logins. This affects all URIs.

	`allow-overwrite=true`

	Restart download if a corresponding control file does not exist. (Default: false)

	`dir=/file/Downloads`

	Store the downloaded file(s) in `/file/Downloads`.

	`file-allocation=falloc`

	Call [posix_fallocate()](http://www.kernel.org/doc/man-pages/online/pages/man2/fallocate.2.html) to allocate disk space before downloading begins. (Default: prealloc)

	`enable-http-pipelining=true`

	Enable [HTTP/1.1 pipelining](https://en.wikipedia.org/wiki/HTTP_Pipelining "wikipedia:HTTP Pipelining") to overcome network latency and to reduce network load. (Default: false)

	`input-file=/file/input.rapidshare`

	Download a list of single line of TAB separated URIs found in `/file/input.rapidshare`

	`log-level=error`

	Set log level to output errors only. (Default: debug)

	`max-connection-per-server=2`

	Set a maximum of two (2) connections to each server per file. (Default: 1)

	`summary-interval=120`

	Output download progress summary every 120 seconds. (Default: 60) 

#### Additional notes

*   Because `aria2.rapidshare` the contains a username and password, it is advisable to set permissions on the file to 600, or similar.

```
$ cd /file
$ chmod 600 /file/aria2.rapidshare
$ ls -l
total 128M
-rw------- 1 arch users  167 Aug 20 00:00 aria2.rapidshare

```

	 `summary-interval=0`

	Supresses download progress summary output and may improve overall performance. Logs will continue to be output according to the value specified in the `log-level` option.

**Tip:** The example configuration file can also be applied to [Hotfile](http://www.hotfile.com/), [DepositFiles](http://depositfiles.com/), et.al.

**Note:** Command-line options always take precedence over options listed in a configuration file.

### Example aria2.bittorrent

```
bt-seed-unverified
max-overall-upload-limit=1M
max-upload-limit=128K
seed-ratio=5.0
seed-time=240

```

#### Option details

	`bt-seed-unverified=false`

	Do not check the hash of the file(s) before seeding. (Default: true)

	`max-overall-upload-limit=1M`

	Set maximum overall upload speed to 1MB/sec. (Default: 0)

	`max-upload-limit=128K`

	Set maximum upload speed per torrent to 128K/sec. (Default: 0)

	`seed-ratio=5.0`

	Seed completed torrents until share ratio reaches 5.0\. (Default: 1.0)

	`seed-time=240`

	Seed completed torrents for 240 minutes.

**Note:** If both `seed-ratio` and `seed-time` are specified, seeding ends when at least one of the conditions is satisfied.

### Example aria2.daemon

This configuration can be used to start Aria2 as a service. It can be used in conjunction with several of the frontends listed below. Note that rpc-user and rpc-pass are deprecated, but most frontends have not been ported to the new authentication yet. Do not forget to change user, password and Download directory.

```
continue
daemon=true
dir=/home/aria2/Downloads
file-allocation=falloc
log-level=warn
max-connection-per-server=4
max-concurrent-downloads=3
max-overall-download-limit=0
min-split-size=5M
enable-http-pipelining=true

enable-rpc=true
rpc-listen-all=true
rpc-user=rpcuser
rpc-passwd=rpcpass

```

## Frontends

**Note:** Settings implemented in frontends do not affect `aria2`'s own configuration, and it is uncertain whether the different UIs reuse `aria2` configuration if a custom one has been made. Users should ensure their desired parameters are effectively implemented within selected tools and that they are stored persistently (uGet for example has its own `aria2`'s command line which sticks across reboots).

### Web UIs

**Note:** These frontends need `aria2c` to be started with `--enable-rpc` in order to work. They are meant to run on your local computer, not on a remote server that downloads using aria

*   **YaaW** — Yet Another Aria2 Web Frontend in pure HTML/CSS/Javascirpt.

	[https://github.com/binux/yaaw](https://github.com/binux/yaaw) || [yaaw-git](https://aur.archlinux.org/packages/yaaw-git/)

*   **Webui** — Html frontend for aria2.

	[https://github.com/ziahamza/webui-aria2](https://github.com/ziahamza/webui-aria2) || [webui-aria2](https://aur.archlinux.org/packages/webui-aria2/)

*   **aria2rpc** — Command line tool for connecting to a remote instance of `aria2c`. If `aria2c` is installed it can be found under `/usr/share/doc/aria2/xmlrpc/aria2rpc`.

	[https://github.com/tatsuhiro-t/aria2/blob/master/doc/xmlrpc/aria2rpc](https://github.com/tatsuhiro-t/aria2/blob/master/doc/xmlrpc/aria2rpc) || [aria2](https://www.archlinux.org/packages/?name=aria2)

### Other UIs

**Note:** These frontends **do not need** `aria2c` to be started with `--enable-rpc` to function.

*   **aria2fe** — A GUI for the CLI-based aria2 download utility.

	[http://sourceforge.net/projects/aria2fe/](http://sourceforge.net/projects/aria2fe/) || [aria2fe](https://aur.archlinux.org/packages/aria2fe/)

*   **Diana** — Command line tool for aria2

	[https://github.com/baskerville/diana](https://github.com/baskerville/diana) || [diana-git](https://aur.archlinux.org/packages/diana-git/)

*   **downloadm** — A download accelerator/manager which uses aria2c as a backend.

	[http://sourceforge.net/projects/downloadm/](http://sourceforge.net/projects/downloadm/) || [downloadm](https://aur.archlinux.org/packages/downloadm/)

*   **eatmonkey** — Download manager for Xfce that works with aria2.

	[http://goodies.xfce.org/projects/applications/eatmonkey](http://goodies.xfce.org/projects/applications/eatmonkey) || [eatmonkey](https://aur.archlinux.org/packages/eatmonkey/)

*   **karia2** — QT4 interface for aria2 download mananger.

	[http://sourceforge.net/projects/karia2/](http://sourceforge.net/projects/karia2/) || [karia2-svn](https://aur.archlinux.org/packages/karia2-svn/)

*   **uGet** — Feature-rich GTK+/CLI download manager which can use aria2 as a back-end by enabling a built-in plugin.

	[http://ugetdm.com](http://ugetdm.com) || [uget](https://www.archlinux.org/packages/?name=uget)

*   **yaner** — GTK+ interface for aria2 download mananger.

	[http://iven.github.com/Yaner](http://iven.github.com/Yaner) || [yaner-git](https://aur.archlinux.org/packages/yaner-git/)

## Tips and tricks

### Download the packages without installing them

Just use the command below:

```
 # pacman -Sp packages | aria2c -i -

```

`pacman -Sp` lists the urls of the packages on stdout, instead of downloading them, then `|` pipes it to the next command. Finally, The `-i` in `aria2c -i -` switch to aria2c means that the urls for files to be downloaded should be read from the file specified, but if `-` is passed, then read the urls from stdin.

### pacman XferCommand

See [pacman/Tips and tricks#aria2](/index.php/Pacman/Tips_and_tricks#aria2 "Pacman/Tips and tricks").

### Changing the User Agent

Some sites may filter the requests based on your User Agent, since Aria2 is not a well known downloader, it may be good to use a most known downloader or browser as the Aria's User Agent. Just use the -U option like this:

```
$ aria2c -UWget http://some-url-to-download/file.xyz

```

You can use whatever you want, like **-UMozilla/5.0** and so on.

### Using Aria2 with makepkg

You can use <a class="mw-selflink selflink">Aria2</a> instead of curl to download source files, just change the `DLAGENTS` variable as follows:

 `/etc/makepkg.conf` 
```
[...]
DLAGENTS=('ftp::/usr/bin/aria2c -UWget -s4 %u -o %o'
          'http::/usr/bin/aria2c -UWget -s4 %u -o %o'
          'https::/usr/bin/aria2c -UWget -s4 %u -o %o'
          'rsync::/usr/bin/rsync --no-motd -z %u %o'
          'scp::/usr/bin/scp -C %u %o')
[...]
```

**Note:** Use the `-UWget` option to change the user agent to Wget. It may prevent problems when downloading from sites that filters the requests based on the user agent to provide different responses on what the users uses to access the URL. Since Aria2 is a lesser known downloader it may be recognized by the site as a browser instead of a downloader, so changing the user agent to Wget may fix it in most cases

## See also

*   [aria2 manual](https://aria2.github.io/manual/en/html/index.html) - Official site
*   [aria2 usage examples](https://aria2.github.io/manual/en/html/aria2c.html#example) - Official site