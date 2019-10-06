Related articles

*   [nftables](/index.php/Nftables "Nftables")

[firewalld](https://firewalld.org/) is firewall daemon developed by Red Hat. It uses [nftables](/index.php/Nftables "Nftables") by default. From project home page:

	Firewalld provides a dynamically managed firewall with support for network/firewall zones that define the trust level of network connections or interfaces. It has support for IPv4, IPv6 firewall settings, ethernet bridges and IP sets. There is a separation of runtime and permanent configuration options. It also provides an interface for services or applications to add firewall rules directly.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Installation](#Installation)
*   [2 Usage](#Usage)
*   [3 Configuration](#Configuration)
    *   [3.1 Zones](#Zones)
        *   [3.1.1 Zone information](#Zone_information)
        *   [3.1.2 Changing zone of an interface](#Changing_zone_of_an_interface)
        *   [3.1.3 Default zones](#Default_zones)
    *   [3.2 Services](#Services)
        *   [3.2.1 Adding or removing services from a zone](#Adding_or_removing_services_from_a_zone)
    *   [3.3 Ports](#Ports)
*   [4 Tips and tricks](#Tips_and_tricks)
    *   [4.1 Port or service timeout](#Port_or_service_timeout)
    *   [4.2 Converting run-time configuration to permanent](#Converting_run-time_configuration_to_permanent)
    *   [4.3 Check services details](#Check_services_details)
*   [5 See also](#See_also)

## Installation

[Install](/index.php/Install "Install") the [firewalld](https://www.archlinux.org/packages/?name=firewalld) package.

## Usage

[Enable](/index.php/Enable "Enable") and [start](/index.php/Start "Start") `firewalld.service`.

You can control the firewall rules with the `firewall-cmd` console utility.

`firewall-offline-cmd` utility can be used to configure when firewalld is not running. It features similar syntax to `firewall-cmd`.

GUI is available as `firewall-config` which comes with [firewalld](https://www.archlinux.org/packages/?name=firewalld) package.

## Configuration

Configuration at run time can be changed using `firewall-cmd`.

**Note:** Most commands will only change run-time configuration and will not persist through restart. To make changes permanent there are two options:

*   Use `--permanent` option. This will **not** change run-time configuration until the firewall service is restarted or rules are reloaded with `--reload` command.
*   Change the run-time configuration and make it permanent as described in [#Converting run-time configuration to permanent](#Converting_run-time_configuration_to_permanent)

### Zones

Zone is a collection of rules that can be applied to a specific interface.

To have an overview of the current zones and interfaces they are applied to:

```
# firewall-cmd --get-active-zones

```

Some commands (such as adding/removing ports/services) require a zone to specified.

Zone can be specified by name by passing `--zone=*zone_name*` parameter.

If no zone is specified default zone is assumed.

#### Zone information

You can list all the zones with entirety their configuration:

```
# firewall-cmd --list-all-zones

```

or just a specific zone

```
# firewall-cmd --info-zone=*zone_name*

```

#### Changing zone of an interface

```
# firewall-cmd --zone=*zone* --change-interface=*interface_name*

```

There `*zone*` is a new zone that you want to assign interface to.

#### Default zones

When a new interface is connected the default zone will be applied. You can query the name of the default zone using:

```
# firewall-cmd --get-default-zone

```

The default zone can be changed using following command.

```
# firewall-cmd --set-default-zone=*zone*

```

**Note:** This change is always permanent.

### Services

Service is a pre-made rules corresponding to a specific daemon. For example, `ssh` service corresponds to [SSH](/index.php/SSH "SSH") and opens ports 22 when assigned to a zone.

To get a list of available services enter following command:

```
# firewall-cmd --get-services

```

You can query information about particular service:

```
# firewall-cmd --info-service *service_name*

```

#### Adding or removing services from a zone

To add a service to a zone:

```
# firewall-cmd --zone=*zone_name* --add-service *service_name*

```

Removing service:

```
# firewall-cmd --zone=*zone_name* --remove-service *service_name*

```

### Ports

Ports can be directly opened on a specific zone.

```
# firewall-cmd --zone=*zone_name* --add-port *port_num*/*protocol*

```

There `*protocol*` is either `tcp` or `udp`.

To close the port use `--remove-port` option with same port number and protocol.

## Tips and tricks

### Port or service timeout

Service or port can be added for a limited amount of time using `--timeout=*value*` option passed during addition command. Value is either number of seconds, minutes if postfixed with `m` or hours `h`. For example, adding [SSH](/index.php/SSH "SSH") service for 3 hours:

```
# firewall-cmd --add-service ssh --timeout=3h

```

### Converting run-time configuration to permanent

You can make current temporary configuration permanent (meaning it persists through restarts)

```
# firewall-cmd --runtime-to-permanent

```

### Check services details

The configuration files for the default supported services are located at `/usr/lib/firewalld/services/` and user-created service files would be in `/etc/firewalld/services/`.

## See also

*   [firewall-cmd(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/firewall-cmd.1)
*   [Official documentation](https://firewalld.org/documentation)
*   [Fedora Wiki](https://fedoraproject.org/wiki/Firewalld)