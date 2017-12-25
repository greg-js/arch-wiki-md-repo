Related articles

*   [AIF-NG/Configuration file](/index.php/AIF-NG/Configuration_file "AIF-NG/Configuration file")

**Note:** The [previous AIF](https://bbs.archlinux.org/viewtopic.php?id=58110) is [dead and gone](https://www.archlinux.org/news/install-media-20120715-released/). This is not a fork of that project. This is a means for unattended installs (like [Kickstart](https://en.wikipedia.org/wiki/Kickstart_(Linux) "wikipedia:Kickstart (Linux)")), and an [entirely new codebase](https://git.square-r00t.net/AIF-NG/).

The full upstream documentation is available [here](https://aif.square-r00t.net/). It is currently in development/review stages in preparation for proposal for inclusion on the official Arch installation media.

## Contents

*   [1 What it Is](#What_it_Is)
*   [2 What it Isn't](#What_it_Isn.27t)
*   [3 Getting Started](#Getting_Started)
*   [4 Usage](#Usage)
*   [5 Configuration](#Configuration)

## What it Is

AIF(-NG) (Arch Install Framework, "Next-Generation") is a means to automatically install Arch Linux. Think of it as something akin to [Kickstart](https://en.wikipedia.org/wiki/Kickstart_(Linux) "wikipedia:Kickstart (Linux)").

It is written in Python 3 and uses an XML configuration file that is remotely fetched and supports "hook scripts" for modular functionality. It can be useful as a tool to quickly turn up new Arch Linux installs.

AIF-NG is not an official Arch Linux project (though this will hopefully change when the project reaches a level of maturity ready for inclusion). Support information is available in the [original documentation](https://aif.square-r00t.net/#further_information) ([bugs](https://aif.square-r00t.net/#bugs) | [feature requests](https://aif.square-r00t.net/#feature_requests) | [patches](https://aif.square-r00t.net/#patches)). It is highly unadvised that you go to the Arch Linux forums for support for this while its status is unofficial, and instead contact the author directly. This is to ensure possible bugs are dealt with.

## What it Isn't

Note the use of the word "quickly", not "easily"- it isn't for the faint of heart, and it is not designed to make the Arch install process any easier. It is recommended that the user run through several Arch installs by hand before attempting to use this tool.

It also is not intended to be a complete turnup solution. Through the use of packages you specify and various hook scripts, you could get there 100% but if you're looking for something to just pop in, run, and go, this is not the tool you're looking for - there are other outside projects that attempt to do this. It is most powerful when combined with a configuration management software (such as [Ansible](/index.php/Ansible "Ansible"), [Chef](/index.php/Chef "Chef"), [Puppet](/index.php/Puppet "Puppet"), [Salt(stack)](/index.php/Saltstack "Saltstack"), and [others](https://en.wikipedia.org/wiki/List_of_build_automation_software#Configuration_management_tools "wikipedia:List of build automation software")) - in other words, one would use AIF-NG to turn up the new machine from "baremetal" and install the configuration management agent, if necessary, and then complete the process on boot through the use of the configuration management system.

## Getting Started

In order for AIF-NG to be useful, you must first have a [configuration file](/index.php/AIF-NG/Configuration_file "AIF-NG/Configuration file"). It then must be accessible from the installer ISO. It is highly recommended that it be served from a webserver in the LAN via HTTPS with basic authentication and properly firewalled, but there are [several options](https://aif.square-r00t.net/#starting_an_install) for pointing to an AIF configuration (including a path on the local filesystem- though this would need to be present on the live/install system to work).

The documentation, as a temporary convenience while this project is under community review, offers [ways to enable AIF-NG automatically](https://aif.square-r00t.net/#building_a_compatible_livecd). Take heed, however- it will write over whatever is on the disk that this live image is booted from, and the default configuration file most likely will not suit your needs. It is easy and recommended instead to [build your own live image](https://aif.square-r00t.net/#recommended).

AIF-NG will then run silently in the background, logging to /root/aif.log.<TIMESTAMP>.

## Usage

The official Arch Linux installer currently does not provide AIF-NG functionality out of the box. However, one can install either the [aif](https://aur.archlinux.org/packages/aif/) or [aif-git](https://aur.archlinux.org/packages/aif-git/) packages. These will also handle the necessary dependencies. Once this is done, we will need to configure manual override enabling:

```
export DEBUG=true
cp /proc/cmdline /tmp/cmdline
sed -i -re 's/^(.*$)/\1 aif aif_url=YOUR_AIF-NG_CONFIGURATION_URI_HERE/g' /tmp/cmdline
aif &

```

AIF-NG will then run silently in the background, logging to `/root/aif.log.<TIMESTAMP>`.

## Configuration

Please see [AIF-NG/Configuration file](/index.php/AIF-NG/Configuration_file "AIF-NG/Configuration file").