This article describes how to access an [iSCSI](/index.php/ISCSI "ISCSI") target with the [Open-iSCSI](https://github.com/open-iscsi/open-iscsi) initiator.

**Note:** ISCSI is NOT encrypted. Transmitting data over unsecured channel is not recommended.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Installation](#Installation)
*   [2 Overview](#Overview)
*   [3 Configuration](#Configuration)
    *   [3.1 Start the Service](#Start_the_Service)
    *   [3.2 ISCSI Qualified Name (IQN)](#ISCSI_Qualified_Name_(IQN))
    *   [3.3 Authentication](#Authentication)
    *   [3.4 Target discovery](#Target_discovery)
    *   [3.5 Add target manually](#Add_target_manually)
    *   [3.6 Delete obsolete targets](#Delete_obsolete_targets)
    *   [3.7 Login to available targets](#Login_to_available_targets)
    *   [3.8 Info](#Info)
    *   [3.9 Online resize of volumes](#Online_resize_of_volumes)
*   [4 Tips & Troubleshooting](#Tips_&_Troubleshooting)

## Installation

[Install](/index.php/Install "Install") the [open-iscsi](https://www.archlinux.org/packages/?name=open-iscsi) package from the [official repositories](/index.php/Official_repositories "Official repositories").

**Note:** An older initiator, [Linux-iSCSI](http://sourceforge.net/projects/linux-iscsi/), was merged with Open-iSCSI in April 2005. This should not be confused with [linux-iscsi.org](http://linux-iscsi.org/), the website for the LIO [target](/index.php/ISCSI_Target "ISCSI Target").

## Overview

The following diagram shows how the Components work together. A more detailed version can be found here: [Open-iSCSI modules (Outdated)](https://archive.is/HHYKR/90a7a1c178a2c069a7cbc0b578b6fb5854f827fa.jpg)

```
 +--------------------------------------------------------+             
 | Targets & Sessions configuration files and directories |             
 +--------------------------------------------------------+             

 +--------------------------+     +----------------------------------+ 
 | iscsiadm                 |     | iscsid: iSCSI daemon             | 
 |                          |     |                                  | 
 |  * Command line tool     |<--->|  * Implements Session management | 
 |  * Manages database of   |     |  * Communicates with iscsiadm    | 
 |    sessions and targets  |     |    and iscsi kernel modules      | 
 +--------------------------+     +---------------+------------------+ 
                                                  |                    
 User space                                       |                    
- - - - - - - - - - - - - - - - - - - - - - - - - | - - - - - - - - - -
 Kernel                                           v                    
         +-----------------------------------------------------------+ 
         | kernel modules: scsi_transport_iscsi, iscsi_tcp, libiscsi | 
         +-----------------------------------------------------------+ 

```

From the Open-iSCSI [README](https://github.com/open-iscsi/open-iscsi):

Persistent configuration is implemented as a tree of files and directories, which are contained in two directories:

*   Discovery directory `/etc/iscsi/send_targets` which has directories named after target addresses.
*   Node directory `/etc/iscsi/nodes` which has directories named after IQN (ISCSI Unique Name) of particular device.

## Configuration

### Start the Service

`iscsid` is managed by a systemd Unit.

[Start](/index.php/Start "Start") `iscsid.service` or `iscsid.socket`.

### ISCSI Qualified Name (IQN)

IQN is used for identifying every device.

Open-ISCSI stores its initiator IQN in the `/etc/iscsi/initiatorname.iscsi` file with a format `InitiatorName=*iqn*`

During installation the initial IQN will be generated. If you wish to generate new IQN the `iscsi-iname` utility can be used which prints out new IQN.

### Authentication

If the ISCSI target requires authentication by the initiator, the configuration file `/etc/iscsi/iscsid.conf` may need to be updated.

The following parameters are used for authenticating a login session of an initiator to a target:

```
node.session.auth.authmethod = CHAP
node.session.auth.username = *initiators_username*
node.session.auth.password = *initiators_password*

```

If your target has two-way authentication enabled then those lines also need to be edited:

```
node.session.auth.username_in = *targets_username*
node.session.auth.password_in = *targets_password*

```

If your target requires authentication to get the list of its nodes (most won't) then following lines should be edited:

```
discovery.sendtargets.auth.authmethod = CHAP
discovery.sendtargets.auth.username = *initiators_username*
discovery.sendtargets.auth.password = *initiators_password*

```

If your target has two-way authentication enabled then those lines also need to be edited:

```
discovery.sendtargets.auth.username_in = *targets_username*
discovery.sendtargets.auth.password_in = *targets_password*

```

**Warning:** No two passwords may be the same. This means that you need four unique passwords in the configuration above.

### Target discovery

Request the target its nodes.

```
# iscsiadm --mode discovery --portal *target_ip* --type sendtargets

```

On success information about nodes and target will be saved on your initiator.

### Add target manually

```
# iscsiadm -m node --target *targetname* --portal *target_ip* -o new

```

A possible scenario to use this is when server does not allow discovery.

### Delete obsolete targets

```
# iscsiadm -m discovery -p *target_ip* -o delete

```

### Login to available targets

```
# iscsiadm -m node -L all

```

or login to specific target

```
# iscsiadm -m node --targetname=*targetname* --login

```

logout:

```
# iscsiadm -m node -U all

```

### Info

For running session

```
# iscsiadm -m session -P 3

```

The last line of the above command will show the name of the attached dev e.g

```
Attached scsi disk **sdd** State: running

```

For the known nodes

```
# iscsiadm -m node

```

### Online resize of volumes

If the iscsi blockdevice contains a partitiontable, you will not be able to do an online resize. In this case you have to unmount the filesystem and alter the size of the affected partition.

1.  Rescan active nodes in current session `# iscsiadm -m node -R` 
2.  If you use multipath, you also have to rescan multipath volume information. `# multipathd -k"resize map sdx"` 
3.  Finally resize the filesystem. `# resize2fs /dev/sdx` 

## Tips & Troubleshooting

You can also check where the attached iSCSI devices are located in the /dev tree with `ls -lh /dev/disk/by-path/*` .

At the server (target) you might need to include the client iqn from `/etc/iscsi/initiatorname.iscsi` in the acl configuration.

Many of the `iscsiadm` operations require that the iSCSI daemon `iscsid` is running. To verify that this is the case, [check the status](/index.php/Systemd#Using_units "Systemd") of the `iscsid.service`.

To run the iSCSI daemon in debug mode (make sure you stopped `iscsid.service` before)

```
# iscsid -d 8 -c /etc/iscsi/iscsid.conf -i /etc/iscsi/initiatorname.iscsi -f

```