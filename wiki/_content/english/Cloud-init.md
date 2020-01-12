[Cloud-init](https://cloud-init.io/) is a package that contains utilities for early initialization of cloud instances. It is needed in Arch Linux images that are built with the intention of being launched in cloud environments like [OpenStack](/index.php/OpenStack "OpenStack"), [AWS](/index.php/AWS "AWS") etc.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
    *   [2.1 Default user configuration](#Default_user_configuration)
    *   [2.2 Configuring data sources](#Configuring_data_sources)
    *   [2.3 Modules](#Modules)
*   [3 Systemd integration](#Systemd_integration)

## Installation

[Install](/index.php/Install "Install") the [cloud-init](https://www.archlinux.org/packages/?name=cloud-init) package.

If you intend to use the [growpart module](https://cloudinit.readthedocs.io/en/latest/topics/modules.html#growpart) you will also need the [growpart](https://aur.archlinux.org/packages/growpart/) package.

## Configuration

This section only discusses the most basic settings. For a full list of available configuration options, please see the [cloud-init documentation](https://cloudinit.readthedocs.io).

The main configuration file is `/etc/cloud/cloud.cfg`. Optionally, additional `*.cfg` files to be loaded can be placed in `/etc/cloud/cloud.cfg.d`. All of their contents will be [merged](https://cloudinit.readthedocs.io/en/latest/topics/merging.html).

The default configuration shipped with cloud-init 19.3 and later should work out of the box with most major cloud environments. In rough terms, it does the following:

*   Disable the root user, create a user `arch` for logging in
*   Rely on cloud-init's built-in detection for data sources
*   Run all modules known to work on Arch Linux

Depending on the use case, the default configuration might need to be adapted.

### Default user configuration

As of January 2020, the configuration includes the following contents (comments omitted for brevity):

```
users:
   - default

```

The users to be added to the system. The special name `default` is just a reference to the `default_user` in the `sytem_info` section (see below), but [the syntax](https://cloudinit.readthedocs.io/en/latest/topics/examples.html#including-users-and-groups) supports configuring arbitrary users with many options. The first user in this list will be considered the "default" user by other modules, for example the one that sets up SSH keys passed in from the cloud environment.

```
disable_root: true

```

Disable root SSH access. You may also delete the root user password on the cloud image:

```
# passwd -d root

```

```
system_info:
   default_user:
     name: arch
     lock_passwd: True
     gecos: arch Cloud User
     groups: [wheel, users]
     sudo: ["ALL=(ALL) NOPASSWD:ALL"]
     shell: /bin/bash

```

This is the specification of the distribution's default user:

*   the default user's name will be `arch`
*   the default user is password locked, which means you can only log into the instance with the SSH keys configured during boot
*   the default user will be added to the groups `users` and `wheel`
*   the default user is allowed passwordless `sudo` usage
*   the default user's shell is `/bin/bash`

Note that the user specified here will only be created if the special user "default" is included in the `users:` section above (or the section is omitted entirely).

### Configuring data sources

Data Sources define how the instance metadata is pulled during boot. This depends on the cloud environment (OpenStack, AWS, OpenNebula etc.) you are running your instance in. Under the hood, this translates to a corresponding module which implements a few methods defined in a common interface.

The default config specifies no data sources, which means that cloud-init will attempt to auto-detect the cloud environment. However, some environments cannot be detected or may require special configuration to work. In this case, the data sources to be used can be explictly specified and configured. Refer to the [list of known data sources](https://cloudinit.readthedocs.io/en/latest/topics/datasources.html#known-sources) in the documentation.

To specify a list of data sources to be used in your `/etc/cloud/cloud.cfg` add something like this:

```
datasource_list: [ NoCloud, ConfigDrive, OpenNebula, Azure, AltCloud, OVF, MAAS, GCE, OpenStack, CloudSigma, Ec2, CloudStack, None ]

```

This instructs cloud-init what modules to load while trying to download instance metadata. Optionally further configuration parameters may be passed specific to each datasource as follows:

```
datasource:
  OpenStack:
    metadata_urls: [ 'http://169.254.169.254:80' ]
    dsmode: net

```

The above configuration tells OpenStack datasource to use the url `http://169.254.169.254:80` to download metadata and to run after network initialization, both of which are the default behaviour and may be omitted.

### Modules

Cloud-init comes with a [set of modules](https://cloudinit.readthedocs.io/en/latest/topics/modules.html) the can be enabled or disabled in the configuration. The default config enables all modules that are known to work on Arch Linux. Omitted modules include e.g. those specific to other distributions or operating systems.

The fact that a module is enabled usually does not mean that it will actually do anything. It will however check if any configuration relevant to it was passed in, e.g. from the cloud environment via the data source. Only then it will attempt to act. As such, enabling all modules usually helps to maximize compatibility with cloud environments. Nevertheless, modules known to be not needed can be removed from configuration, e.g. to improve start-up times. You can use `cloud-init analyze` on a booted instance to see how much time was spent on individual modules.

Some modules declare to cloud-init which distros they have been verified for. Even if you specify that you want to run them, they will refuse to run unless the distro specified in `cloud.cfg` is one of the verified distros for that module. If you need to override this behaviour to run a module on Arch anyway, add the module to the `unverified_modules` section in the cloud config, e.g.:

```
unverified_modules: ['ssh-import-id']

```

## Systemd integration

Package cloud-init provides four systemd [services](https://www.freedesktop.org/software/systemd/man/systemd.service.html), two systemd [targets](https://www.freedesktop.org/software/systemd/man/systemd.target.html), and a systemd [generator](https://www.freedesktop.org/software/systemd/man/systemd.generator.html), whose dependencies are constructed in a way that they are activated in the sequence listed:

*   `cloud-init-generator`. Determines availability of any data source and enables or disables `cloud-init.target`
*   `cloud-init-local.service`. Only requires the filesystems to be up. Executes `cloud-init init --local`
*   `cloud-init.service`. Requires the network to be up. Executes `cloud-init init`
*   `cloud-config.target`. Corresponds to the cloud-config upstart event "to inform third parties that cloud-config is available"
*   `cloud-config.service`. Executes `cloud-init modules --mode=config`
*   `cloud-final.service`. Executes `cloud-init modules --mode=final`
*   `cloud-init.target`. Reached when all services have been started

The [Uplink Labs EC2 images](/index.php/Arch_Linux_AMIs_for_Amazon_Web_Services "Arch Linux AMIs for Amazon Web Services") have all of them enabled, although that appears to be overkill due to the dependencies. When preparing an image, enabling `cloud-init.service` and `cloud-final.service` should be sufficient. Note that this does not mean that the cloud-init services will actually be run - that still depends on the generator enabling the `cloud-init.target` on early boot.

See also the [cloud-init boot stages documentation](https://cloudinit.readthedocs.io/en/latest/topics/boot.html) for more info.