Related articles

[Daemons](/index.php/Daemons "Daemons")

From the [IPFS README.md on GitHub](https://github.com/ipfs/ipfs):

	IPFS (the [InterPlanetary File System](https://en.wikipedia.org/wiki/IPFS "wikipedia:IPFS")) is a new hypermedia distribution protocol, addressed by content and identities. IPFS enables the creation of completely distributed applications. It aims to make the web faster, safer, and more open.

	IPFS is a distributed file system that seeks to connect all computing devices with the same system of files. In some ways, this is similar to the original aims of the Web, but IPFS is actually more similar to a single BitTorrent swarm exchanging git objects.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Installation](#Installation)
*   [2 Using a service to start the daemon](#Using_a_service_to_start_the_daemon)
*   [3 File sharing](#File_sharing)
*   [4 Simple hosting with name resolution](#Simple_hosting_with_name_resolution)
*   [5 See also](#See_also)

## Installation

[Install](/index.php/Install "Install") the [go-ipfs](https://www.archlinux.org/packages/?name=go-ipfs) package or the [go-ipfs-git](https://aur.archlinux.org/packages/go-ipfs-git/) package.

To start using IPFS you must first issue

```
$ ipfs init

```

as a user. This creates a `~/.ipfs` directory with all the necessary files in it.

Now you can start the IPFS daemon:

```
$ ipfs daemon

```

This starts your node, available via the `ipfs` cli, or the web interface on [localhost:5001/webui](http://localhost:5001/webui). Additionally, a local gateway goes up on localhost:8080 (the default port can be changed in `~/.ipfs/config`).

## Using a service to start the daemon

For convenience you can automate the startup of <a class="mw-selflink selflink">IPFS</a> daemon using a [Systemd/User](/index.php/Systemd/User "Systemd/User") service. This ensures that the daemon starts when you log in, and that it is restarted if it crashes.

 `~/.config/systemd/user/ipfs.service` 
```
[Unit]
Description=IPFS daemon
After=network.target

[Service]
ExecStart=/usr/bin/ipfs daemon
Restart=on-failure

[Install]
WantedBy=default.target
```

You can then enable and start the service unit:

```
$ systemctl --user enable --now ipfs

```

If you want the unit to keep working even after you have logged out, and start before you log in, you can enable lingering:

```
# loginctl enable-linger *username*

```

## File sharing

To share a file using IPFS you need the daemon to be running.

```
$ ipfs add file

```

returns a hash. If someone shared this file via IPFS before, the hash would match that previous upload, making you the second source of the file.

To retrieve a file via the IPFS hash, use `ipfs cat`:

```
$ ipfs cat /ipfs/QmYwAPJzv5CZsnA625s3Xf2nemtYgPpHdWEz79ojWnPbdG/readme

```

You can pipe this into any other application, for example, to watch a video with [mpv](/index.php/Mpv "Mpv"):

```
$ ipfs cat QmWenbjgZnA6UguLtmUYayS6e7UQM7woB15zuEymSRRMoi | mpv -

```

Or you can download the file:

```
$ ipfs get QmWenbjgZnA6UguLtmUYayS6e7UQM7woB15zuEymSRRMoi

```

There is also an [ipget](https://aur.archlinux.org/packages/ipget/) utility, which acts like [wget](/index.php/Wget "Wget") for IPFS. In addition it includes a bootstrap node, so you won't have to have ipfs daemon running or installed in order to use it. To download a file:

```
$ ipget QmWenbjgZnA6UguLtmUYayS6e7UQM7woB15zuEymSRRMoi

```

You can share both files and folders. Folders should be shared recursively:

```
$ ipfs add -r folder

```

To view all the files and caches in a folder (if hash is a folder):

```
$ ipfs ls QmYwAPJzv5CZsnA625s3Xf2nemtYgPpHdWEz79ojWnPbdG

```

Every file shared with network is accessible via the IPFS gateway on `localhost:8080` like this:

```
http://localhost:8080/ipfs/QmWenbjgZnA6UguLtmUYayS6e7UQM7woB15zuEymSRRMoi

```

There are public gateways, allowing users with no IPFS node running to access files on the network. For example, the official [website](http://ipfs.io):

```
[http://ipfs.io/ipfs/QmYwAPJzv5CZsnA625s3Xf2nemtYgPpHdWEz79ojWnPbdG](http://ipfs.io/ipfs/QmYwAPJzv5CZsnA625s3Xf2nemtYgPpHdWEz79ojWnPbdG)

```

## Simple hosting with name resolution

In IPFS files shared are never deleted, and with any change of a file its hash changes too. This makes such tasks as website hosting difficult, as any changes to a webpage, for example to an `index.html`, would result in this webpage having a different hash, and the old webpage would be still accessible with the old hash. It is one of a network's goals to store all the content persistently with full history. IPFS offers a name service you can use to generate persistent caches - ipns. Ipns allows you to bind any hash to your node's unique id, generated at initialization. You can view your id like this:

```
$ ipfs id

```

And to bind any hash to it:

```
$ ipfs name publish *HASH*

```

This would assign new hash generated by `ipfs add` after file change to your node id, and hence make updated version of a folder/file accessible using the same address.

Note that when using ipns the address would have an ipns prefix instead of ipfs:

```
 [http://localhost:8080/ipns/QmPtMQErTfQMbZTMMpQh65cpk5y7D94WdYJurCeRqvXKmD/](http://localhost:8080/ipns/QmPtMQErTfQMbZTMMpQh65cpk5y7D94WdYJurCeRqvXKmD/)

```

## See also

*   [IPFS Homepage](https://ipfs.io)
*   [IPFS Examples](https://github.com/ipfs/website/tree/master/content/docs/examples)
*   [Awesome IPFS](https://github.com/ipfs/awesome-ipfs)
*   [IPFS and pacman](https://github.com/ipfs/notes/issues/84)