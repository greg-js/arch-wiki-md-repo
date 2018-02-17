Related articles

*   [Ceph](/index.php/Ceph "Ceph")

[Glusterfs](https://www.gluster.org/) is a scalable network [filesystem](/index.php/Filesystem "Filesystem").

## Installation

[Install](/index.php/Install "Install") the package [glusterfs](https://www.archlinux.org/packages/?name=glusterfs).

## Configuration

Glusterfs can be setup to run in many different configurations depending operating needs, including distributed and replicated. For the example below, a two node replicated server is being created, with nodes gluster1 and gluster2 each have two disks, one containing the OS sda, the other to be shared by glusterfs sdb. Unless stated all setup is carried on gluster1

*   [Start/enable](/index.php/Start/enable "Start/enable") the gluster daemon `glusterd.service` on both servers.

*   Connect the servers

```
 # gluster peer probe gluster2

```

*   Partition and format the glusterfs drive on both servers
    *   The upstream advises creating a single partition and formatting this as xfs

*   On both servers automount the drives by [appending](/index.php/Append "Append") `/etc/fstab` to include the following line, where `/dev/sd*XY*` is the appropriate device (e.g., `/dev/sdb1`).

 `/etc/fstab`  `/dev/sd*XY* /export/sd*XY* xfs defaults 0 0` 

*   On both servers [mount](/index.php/Mount "Mount") the drives. Then create a "brick":

```
 # mkdir -p /export/sd*XY*/brick

```

*   Enable replication on primary server

```
 # gluster volume create gv0 replica 2 gluster1.mydomain.net:/export/sdb1/brick gluster2.mydomain.net:/export/sdb1/brick

```

*   Ensure volume is created correctly

```
 # gluster volume info

```

*   Start volume

```
 # gluster volume start gv0

```

*   Mount the volume

```
 # mkdir -p /mnt/glusterClientMount
 # mount -t glusterfs gluster1:/gv0 /mnt/glusterClientMount

```

## See also

*   [Official glusterfs installation guide](http://gluster.readthedocs.io/en/latest/Install-Guide/Overview/)
*   [Blog covering the setup of Glusterfs on Arch Linux](https://blog.bastelfreak.de/2016/05/short-tip-setup-glusterfs-share-on-arch-linux/)