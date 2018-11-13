[LIO](http://linux-iscsi.org/) (LinuxIO) is the in-kernel [iSCSI](/index.php/ISCSI "ISCSI") target (since Linux 2.6.38).

## Contents

*   [1 Installation](#Installation)
*   [2 targetcli](#targetcli)
    *   [2.1 Authentication](#Authentication)
        *   [2.1.1 Disable Authentication](#Disable_Authentication)
        *   [2.1.2 Set Credentials](#Set_Credentials)
*   [3 Tips & Tricks](#Tips_&_Tricks)
*   [4 See also](#See_also)

## Installation

The iSCSI target fabric is included since Linux 3.1.

The important kernel modules are *target_core_mod* and *iscsi_target_mod*, which should be in the kernel and loaded automatically.

It is highly recommended to use the free branch versions of the packages: [targetcli-fb](https://aur.archlinux.org/packages/targetcli-fb/), [python-rtslib-fb](https://aur.archlinux.org/packages/python-rtslib-fb/) and [python-configshell-fb](https://aur.archlinux.org/packages/python-configshell-fb/).

[Start/enable](/index.php/Start/enable "Start/enable") the `target.service`, included in [python-rtslib-fb](https://aur.archlinux.org/packages/python-rtslib-fb/), to load necessary modules, mount the configfs and load previously saved iSCSI target configuration.

## targetcli

Run `targetcli status` as [root](/index.php/Root_user "Root user") to see some information about the running configuration.

You can use **targetcli** to create the whole configuration, see targetcli(8).

The config shell creates most names and numbers for you automatically, but you can also provide your own settings. At any point in the shell you can type `help` in order to see what commands you can issue here.

**Tip:** In this shell you can use tab-completion and type `cd` to view & select paths.
After starting the target (see above) you enter the configuration shell with `# targetcli` 

In this shell you include a block device (here: `/dev/disk/by-id/md-name-nas:iscsi`) to use with

```
/> cd backstores/block
/backstores/block> create md_block0 /dev/disk/by-id/md-name-nas:iscsi

```

**Note:** You can use any block device, also RAID and LVM devices. You can also use files when you go to fileio instead of block.

You then create an iSCSI Qualified Name (IQN) and a target portal group (TPG) with:

```
...> cd /iscsi
/iscsi> create

```

**Note:** With appending an IQN of your choice to `create` you can keep targetcli from automatically creating an IQN.

In order to tell LIO that your block device should get used as *backstore* for the target you issue

**Note:** Remember that you can type `cd` to select the path of your <iqn>/tpg1

```
.../tpg1> cd luns
.../tpg1/luns> create /backstores/block/md_block0

```

Then you need to create a *portal*, making a daemon listen for incoming connections:

```
.../luns/lun0> cd ../../portals
.../portals> create

```

Targetcli will tell you the IP and port where LIO is listening for incoming connections (defaults to 0.0.0.0 (all)). You will need at least the IP for the clients. The port should be the standard port 3260.

In order for a client/[initiator](/index.php/ISCSI_Initiator "ISCSI Initiator") to connect you need to include the IQN of the initiator in the target configuration:

```
...> cd ../../acls
.../acls> create iqn.2005-03.org.open-iscsi:SERIAL

```

Instead of `iqn.2005-03.org.open-iscsi:SERIAL` you use the IQN of an initiator. It can normally be found in `/etc/iscsi/initiatorname.iscsi`. You have to do this for every initiator that needs to connect. Targetcli will automatically map the created LUN to the newly created ACL.

**Note:** You can change the mapped LUNs and whether the access should be rw or ro. See `help create` at this point in the targetcli shell.

The last thing you have to do in targetcli when everything works is saving the configuration with:

```
...> cd /
/> saveconfig

```

The will the configuration in `/etc/target/saveconfig.json`. You can now safely start and stop `target.service` without losing your configuration.

**Tip:** You can give a filename as a parameter to `saveconfig` and also clear a configuration with `clearconfig`.

### Authentication

Authentication per CHAP is enabled per default for your targets. You can either setup passwords or disable this authentication.

#### Disable Authentication

Navigate targetcli to your target (i.e. /iscsi/iqn.../tpg1) and:

```
.../tpg1> set attribute authentication=0

```

**Warning:** With this setting everybody that knows the iqn of one of your clients (initiators) can access the target. This is for testing or home purposes only.

#### Set Credentials

Navigate to a certain ACL of your target (i.e. /iscsi/iqn.../tpg1/acls/iqn.../) and

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

## Tips & Tricks

*   With `targetcli sessions` you can list the current open sessions.

## See also

*   [targetcli](http://www.linux-iscsi.org/wiki/Targetcli)
*   [Persistent block device naming](/index.php/Persistent_block_device_naming "Persistent block device naming") in order to use the correct block device for a target