Cloud-init is a package that contains utilities for early initialization of cloud instances. It is needed in Arch Linux images that are built with the intention of being launched in cloud like [OpenStack](/index.php/OpenStack "OpenStack"), [AWS](/index.php/AWS "AWS") etc.

## Contents

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
    *   [2.1 Default user configuration](#Default_user_configuration)
    *   [2.2 Disable login as root](#Disable_login_as_root)
    *   [2.3 Configuring data sources](#Configuring_data_sources)
*   [3 Other sections in cloud.cfg](#Other_sections_in_cloud.cfg)
*   [4 Systemd integration](#Systemd_integration)

## Installation

[Install](/index.php/Install "Install") [cloud-init](https://aur.archlinux.org/packages/cloud-init/) from the [official repositories](/index.php/Official_repositories "Official repositories").

## Configuration

In order to make an Arch image cloud ready, a few steps have to be followed:

*   Create a default user. You can login to your instance as this user. We will create and use a user called `arch`.
*   Install sudo and add the default user to sudo group. This can be used later to execute commands as privileged user.
*   Enable password less sudo for the default user.
*   Configure cloud-init to pull instance metadata to configure the instance. This includes but not limited to:
    *   Setting up the instance `hostname`
    *   Configuring instance's `resolv.conf`
    *   Configuring `~/.ssh/authorized_keys` file for the default user

The cloud-init's main configuration file is `/etc/cloud/cloud.cfg`. Optionally the user can place `*.cfg` files in `/etc/cloud/cloud.cfg.d` to be loaded.

### Default user configuration

As of February 2016, the default `/etc/cloud/cloud.cfg` shipped with the package has not been adapted to Arch, and still states that the distro is Ubuntu, therefore it requires editing.

Edit `/etc/cloud/cloud.cfg` to have the following contents:

```
users:
  - default

```

This tells cloud-init to use the user configured under `system_info` > `default_user` as the default user:

```
system_info:
   distro: arch
   default_user:
     name: arch 
     lock_passwd: true
     gecos: Arch
     groups: [adm, audio, cdrom, dialout, dip, floppy, netdev, plugdev, sudo, video]
     sudo: ["ALL=(ALL) NOPASSWD:ALL"]
     shell: /bin/bash

```

Under `system_info` we specify the distro as "arch". This will instruct cloud-init to use `arch.py` module for configuration. Further we specify that:

*   the default user's name would be `arch`
*   the default user is password locked, which means you can not login to the instance without the ssh keys configured during boot
*   the default user should be added to the groups `adm`, `audio`, `cdrom`, `dialout`, `dip`, `floppy`, `netdev`, `plugdev`, `sudo`, `video`
*   the default user is allow passwordless sudo usage
*   the default user's shell is `/bin/bash`

### Disable login as root

To do this you can specify in `/etc/cloud/cloud.cfg`:

```
disable_root: true

```

You may also delete the root user password:

```
# passwd -d root

```

Do not perform this step unless you are sure the configuration in previous section works. Otherwise you might be completely locked out of your instance.

### Configuring data sources

Data Sources define how the instance metadata is pulled during boot. This depends on what cloud (OpenStack, AWS, OpenNebula etc.) you are running your instance on. Under the hood this translates to a corresponding module which implement a few methods defined in a common interface. Edit your `/etc/cloud/cloud.cfg` to have the below contents:

```
datasource_list: [ NoCloud, ConfigDrive, OpenNebula, Azure, AltCloud, OVF, MAAS, GCE, OpenStack, CloudSigma, Ec2, CloudStack, None ]

```

This instructs cloud-init what modules to load while trying to download instance metadata. Optionally further configuration parameters may be passed specific to each datasource as below:

```
datasource:
  OpenStack:
    metadata_urls: [ 'http://169.254.169.254:80' ]
    dsmode: net

```

The above configuration tells OpenStack datasource to use the url `http://169.254.169.254:80` to download metadata and to run after network initialization, both of which are the default behaviour and may be omitted.

## Other sections in cloud.cfg

`cloud.cfg` defines several other sections which includes but not limited to `cloud_init_modules`, `cloud_config_modules` and `cloud_final_modules` that define the modules that would be run at various stages during instance initialization. These modules are loaded dynamically from the path `/usr/lib/python2.7/site-packages/cloudinit/config/` and run at boot time. The user may define their own modules and configure them to be called during every boot like say to:

*   perform disk resize
*   perform package update

etc.

The various modules declare to cloud-init which distros they have been verified for. Even if you specify that you want to run them, they will refuse to run unless the distro specified in `cloud.cfg` is one of the verified distros for the given module. If you want to run a module on Arch anyway that does not specify `arch`, add the module to the `unverified_modules:` section in `cloud.cfg`, e.g.:

```
unverified_modules: ['ssh-import-id']

```

## Systemd integration

Package cloud-init provides 4 systemd services, and a systemd target, whose dependencies are constructed in a way that they are activated in the sequence listed:

*   `cloud-init-local.service`. Only requires the filesystems to be up. Executes `cloud-init init --local`
*   `cloud-init.service`. Requires the network to be up. Executes `cloud-init init`
*   `cloud-config.target`. Corresponds to the cloud-config upstart event "to inform third parties that cloud-config is available"
*   `cloud-config.service`. Executes `cloud-init modules --mode=config`
*   `cloud-final.service`. Executes `cloud-init modules --mode=final`

The [Uplink Labs EC2 images](/index.php/Arch_Linux_AMIs_for_Amazon_Web_Services "Arch Linux AMIs for Amazon Web Services") have all of them enabled, although that appears to be overkill due to the dependencies.