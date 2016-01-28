# ISCSI Target

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

Related articles

*   [iSCSI Initiator](/index.php/ISCSI_Initiator "ISCSI Initiator")
*   [iSCSI Boot](/index.php/ISCSI_Boot "ISCSI Boot")

With [iSCSI](https://en.wikipedia.org/wiki/iSCSI "wikipedia:iSCSI") you can access storage over an IP-based network.

The exported storage entity is the **target** and the importing entity is the **[initiator](/index.php/ISCSI_Initiator "ISCSI Initiator")**. There are different modules available to set up the target:

*   The [SCSI Target Framework (STGT/TGT)](http://stgt.berlios.de/) was the standard before linux 2.6.38.
*   The current standard is the [LIO target](http://linux-iscsi.org/).
*   The [iSCSI Enterprise Target (IET)](http://iscsitarget.sourceforge.net/) is an old implementation and [SCSI Target Subsystem (SCST)](http://scst.sourceforge.net/) is the successor of IET and was a possible candidate for kernel inclusion before the decision fell for LIO.

## Contents

*   [1 Setup with LIO Target](#Setup_with_LIO_Target)
    *   [1.1 Using targetcli](#Using_targetcli)
        *   [1.1.1 Authentication](#Authentication)
            *   [1.1.1.1 Disable Authentication](#Disable_Authentication)
            *   [1.1.1.2 Set Credentials](#Set_Credentials)
    *   [1.2 Using (plain) LIO utils](#Using_.28plain.29_LIO_utils)
    *   [1.3 Tips & Tricks](#Tips_.26_Tricks)
    *   [1.4 Upstream Documentation](#Upstream_Documentation)
*   [2 Setup with SCSI Target Framework (STGT/TGT)](#Setup_with_SCSI_Target_Framework_.28STGT.2FTGT.29)
*   [3 Setup with iSCSI Enterprise Target (IET)](#Setup_with_iSCSI_Enterprise_Target_.28IET.29)
    *   [3.1 Create the Target](#Create_the_Target)
        *   [3.1.1 Hard Drive Target](#Hard_Drive_Target)
        *   [3.1.2 File based Target](#File_based_Target)
    *   [3.2 Start server services](#Start_server_services)
*   [4 See also](#See_also)

## Setup with LIO Target

LIO target is included in the kernel since 2.6.38\. However, the iSCSI target fabric is included since linux 3.1.

The important kernel modules are _target_core_mod_ and _iscsi_target_mod_, which should be in the kernel and loaded automatically.

It is highly recommended to use the free branch versions of the packages: [targetcli-fb](https://aur.archlinux.org/packages/targetcli-fb/)<sup><small>AUR</small></sup>, [python-rtslib-fb](https://aur.archlinux.org/packages/python-rtslib-fb/)<sup><small>AUR</small></sup> and [python-configshell-fb](https://aur.archlinux.org/packages/python-configshell-fb/)<sup><small>AUR</small></sup>. The original [targetcli](https://aur.archlinux.org/packages/targetcli/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/targetcli)]</sup> is also available but has a different way of saving the configuration using the deprecated _lio-utils_ and depends on _epydoc_.

A systemd `target.service` is included in [python-rtslib-fb](https://aur.archlinux.org/packages/python-rtslib-fb/)<sup><small>AUR</small></sup> when you use the free branch and a `/etc/rc.d/target` in [lio-utils](https://aur.archlinux.org/packages/lio-utils/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/lio-utils)]</sup> when you use the original _targetcli_ or _lio-utils_ directly.

You start LIO target with `# systemctl start target` 

This will load necessary modules, mount the configfs and load previously saved iscsi target configuration.

With `# targetcli status` you can show some information about the running configuration (only with the free branch). You might want to enable the lio target on boot with `# systemctl enable target` 

You can use **targetcli** to create the whole configuration or you can alternatively use the **lio utils** tcm_* and lio_* directly (deprecated).

### Using targetcli

The external manual is only available in the _free branch_. [targetd](https://github.com/agrover/targetd) is not in AUR yet, but this depends on the free branch.

The config shell creates most names and numbers for you automatically, but you can also provide your own settings. At any point in the shell you can type `help` in order to see what commands you can issue here.

**Tip:** You can use tab-completion in this shell

**Tip:** You can type `cd` in this shell to view & select paths

After starting the target (see above) you enter the configuration shell with `# targetcli` 

In this shell you include a block device (here: `/dev/disk/by-id/md-name-nas:iscsi`) to use with

```
/> cd backstores/block  
/backstores/block> create md_block0 /dev/disk/by-id/md-name-nas:iscsi
```

**Note:** You can use any block device, also raid and lvm devices. You can also use files when you go to fileio instead of block.

You then create an iSCSI Qualified Name (iqn) and a target portal group (tpg) with

```
...> cd /iscsi  
/iscsi> create
```

**Note:** With appending an iqn of your choice to `create` you can keep targetcli from automatically creating an iqn

In order to tell LIO that your block device should get used as _backstore_ for the target you issue

**Note:** Remember that you can type `cd` to select the path of your <iqn>/tpg1

```
.../tpg1> cd luns  
.../tpg1/luns> create /backstores/block/md_block0
```

Then you need to create a _portal_, making a daemon listen for incoming connections:

```
.../luns/lun0> cd ../../portals  
.../portals> create
```

Targetcli will tell you the IP and port where LIO is listening for incoming connections (defaults to 0.0.0.0 (all)). You will need at least the IP for the clients. The port should be the standard port 3260.

In order for a client/[initiator](/index.php/ISCSI_Initiator "ISCSI Initiator") to connect you need to include the iqn of the initiator in the target configuration:

```
...> cd ../../acls  
.../acls> create iqn.2005-03.org.open-iscsi:SERIAL
```

Instead of `iqn.2005-03.org.open-iscsi:SERIAL` you use the iqn of an initiator. It can normally be found in `/etc/iscsi/initiatorname.iscsi`. You have to do this for every initiator that needs to connect. Targetcli will automatically map the created lun to the newly created acl.

**Note:** You can change the mapped luns and whether the access should be rw or ro. See `help create` at this point in the targetcli shell.

The last thing you have to do in targetcli when everything works is saving the configuration with:

```
...> cd /
/> saveconfig

```

The will the configuration in `/etc/target/saveconfig.json`. You can now safely start and stop `target.service` without losing your configuration.

**Tip:** You can give a filename as a parameter to `saveconfig` and also clear a configuration with `clearconfig`

#### Authentication

Authentication per CHAP is enabled per default for your targets. You can either setup passwords or disable this authentication.

##### Disable Authentication

Navigate targetcli to your target (i.e. /iscsi/iqn.../tpg1) and

```
.../tpg1> set attribute authentication=0

```

**Warning:** With this setting everybody that knows the iqn of one of your clients (initiators) can access the target. This is for testing or home purposes only.

##### Set Credentials

Navigate to a certain acl of your target (i.e. /iscsi/iqn.../tpg1/acls/iqn.../) and

```
...> get auth

```

will show you the current authentication credentials.

```
...> set auth userid=<username in target>
...> set auth password=<password in target>
...> set auth mutual_userid=<username in initiator>  (optional)
...> set auth mutual_password=<password in initiator>  (optional)

```

The first two fields are the username and password of the target. The initiator will use this to log into the target. The last two fields (prefixed with "mutual_") are the username and password of the initiators (note that all initiators will have the same username and password). These two are optional parameters and it ensures that initiators will only accept connections from permitted targets.

### Using (plain) LIO utils

You have to install [lio-utils](https://aur.archlinux.org/packages/lio-utils/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/lio-utils)]</sup> from [AUR](/index.php/AUR "AUR") and the dependencies (python2).

### Tips & Tricks

*   With `targetcli sessions` you can list the current open sessions. This command is included in the [targetcli-fb](https://aur.archlinux.org/packages/targetcli-fb/)<sup><small>AUR</small></sup> package, but not in _lio-utils_ or the original _targetcli_.

### Upstream Documentation

*   [targetcli](http://www.linux-iscsi.org/wiki/Targetcli)
*   [LIO utils](http://www.linux-iscsi.org/wiki/Lio-utils_HOWTO)
*   You can also use `man targetcli` when you installed the _free branch_ version [targetcli-fb](https://aur.archlinux.org/packages/targetcli-fb/)<sup><small>AUR</small></sup>.

## Setup with SCSI Target Framework (STGT/TGT)

You will need the Package [tgt](https://aur.archlinux.org/packages/tgt/)<sup><small>AUR</small></sup> from [AUR](/index.php/AUR "AUR").

See: [TGT iSCSI Target](/index.php/TGT_iSCSI_Target "TGT iSCSI Target")

## Setup with iSCSI Enterprise Target (IET)

You will need [iscsitarget-kernel](https://aur.archlinux.org/packages/iscsitarget-kernel/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/iscsitarget-kernel)]</sup> and [iscsitarget-usr](https://aur.archlinux.org/packages/iscsitarget-usr/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/iscsitarget-usr)]</sup> from [AUR](/index.php/AUR "AUR").

### Create the Target

Modify /etc/iet/ietd.conf accordingly

#### Hard Drive Target

```
Target iqn.2010-06.ServerName:desc
Lun 0 Path=/dev/sdX,Type=blockio

```

#### File based Target

Use "dd" to create a file of the required size, this example is 10GB.

```
dd if=/dev/zero of=/root/os.img bs=1G count=10

```

```
Target iqn.2010-06.ServerName:desc
Lun 0 Path=/root/os.img,Type=fileio

```

### Start server services

[![Tango-dialog-warning.png](/images/d/d8/Tango-dialog-warning.png)](/index.php/File:Tango-dialog-warning.png)

[![Tango-dialog-warning.png](/images/d/d8/Tango-dialog-warning.png)](/index.php/File:Tango-dialog-warning.png)

**This article or section is out of date.**

**Reason:** Mentions rc.d scripts and rc.conf. (Discuss in [Talk:ISCSI Target#](https://wiki.archlinux.org/index.php/Talk:ISCSI_Target))

```
rc.d start iscsi-target

```

Also you can "iscsi-target" to DAEMONS in /etc/rc.conf so that it starts up during boot.

## See also

*   [iSCSI Boot](/index.php/ISCSI_Boot "ISCSI Boot") Booting Arch Linux with / on an iSCSI target.
*   [Persistent block device naming](/index.php/Persistent_block_device_naming "Persistent block device naming") in order to use the correct block device for a target

Retrieved from "[https://wiki.archlinux.org/index.php?title=ISCSI_Target&oldid=402168](https://wiki.archlinux.org/index.php?title=ISCSI_Target&oldid=402168)"

[Categories](/index.php/Special:Categories "Special:Categories"):

*   [Storage](/index.php/Category:Storage "Category:Storage")
*   [Networking](/index.php/Category:Networking "Category:Networking")

Hidden categories:

*   [Pages with broken package links](/index.php/Category:Pages_with_broken_package_links "Category:Pages with broken package links")
*   [Pages or sections flagged with Template:Out of date](/index.php/Category:Pages_or_sections_flagged_with_Template:Out_of_date "Category:Pages or sections flagged with Template:Out of date")