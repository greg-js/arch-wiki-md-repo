[Graphical Network Simulator](https://www.gns3.com/) (GNS3) allows you to simulate a network on your computer.

From the webpage:

	*GNS3 is an open source software that simulate complex networks while being as close as possible to the way real networks perform. All of this without having dedicated network hardware such as routers and switches.*

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Installation](#Installation)
*   [2 Adding virtual machines](#Adding_virtual_machines)
    *   [2.1 VirtualBox](#VirtualBox)
        *   [2.1.1 Install VirtualBox](#Install_VirtualBox)
        *   [2.1.2 Adding the GNS3 VM to VirtualBox](#Adding_the_GNS3_VM_to_VirtualBox)
        *   [2.1.3 Adding VMs to GNS3](#Adding_VMs_to_GNS3)
        *   [2.1.4 Adding VMs to your topology](#Adding_VMs_to_your_topology)
    *   [2.2 VMware](#VMware)
*   [3 Connecting devices](#Connecting_devices)
*   [4 VPCS](#VPCS)
*   [5 Wireshark packet capture](#Wireshark_packet_capture)

## Installation

GNS3 uses patched python extensions, [python-aiohttp-cors-gns3](https://aur.archlinux.org/packages/python-aiohttp-cors-gns3/) and [python-yarl-gns3](https://aur.archlinux.org/packages/python-yarl-gns3/), which need to be [installed](/index.php/Install "Install") before GNS3.

**Note:** That can potentially create trouble with another programs using the original extensions.

The [gns3-gui](https://aur.archlinux.org/packages/gns3-gui/) and [gns3-server](https://aur.archlinux.org/packages/gns3-server/) packages are needed to run the GNS3 GUI.

[libvirt](/index.php/Libvirt "Libvirt") can be used to create the end devices "Cloud" (providing a virtual wan interfaces, isolating the tested network to the other devices in the main network) and NAT. To make [libvirt](/index.php/Libvirt "Libvirt") work correctly, GNS3 needs [dnsmasq](/index.php/Dnsmasq "Dnsmasq") and [ubridge](https://aur.archlinux.org/packages/ubridge/). Install them and ensure the *libvirtd* daemon is running before using GNS3 for can use Cloud and NAT end devices.

## Adding virtual machines

When creating your topology (your virtual network), you most likely want to add machines to it. GNS3 supports [QEMU](/index.php/QEMU "QEMU") and [VirtualBox](/index.php/VirtualBox "VirtualBox") out of the box. [VMware](/index.php/VMware "VMware") does not make for as easy integration. You can use VMWare but you can not add the machines directly in your topology as you can with [QEMU](/index.php/QEMU "QEMU") and [VirtualBox](/index.php/VirtualBox "VirtualBox").

### VirtualBox

#### Install VirtualBox

To use [VirtualBox](/index.php/VirtualBox "VirtualBox") machines for your topology you need to [install](/index.php/Install "Install") [virtualbox](https://www.archlinux.org/packages/?name=virtualbox) and [virtualbox-sdk](https://www.archlinux.org/packages/?name=virtualbox-sdk). To avoid any problems with GNS3 not finding VirtualBox it is recommended to install VirtualBox AFTER you install GNS3\. If you already have VirtualBox installed, you should be able to just reinstall it.

If you don't install the [virtualbox-sdk](https://www.archlinux.org/packages/?name=virtualbox-sdk) package you will not get the `vboxapi.py` script and GNS3s `vboxwrapper.py` needs this to connect the VMs.

#### Adding the GNS3 VM to VirtualBox

The official GNS3 VM should be used to increase performance. Go to [GNS3 Github](https://github.com/GNS3/gns3-gui/releases\) and download the VirtualBox version of the GNS3 VM with the exact same version number as your GNS3 version. Unzip and import the VM in VirtualBox.

To create a network connection between the GNS3 VM and the host OS a host-only network must be configured. In *VirtualBox > Preferences > Network*, set up a host-only network. In most cases, it will be called `vboxnet0` or similar. Note the IP address dedicated to the interface in the GUI. For some reason, VirtualBox does not assign the IP to the interface, nor does it enable it. Therefore, this must be performed manually in the terminal. See [Network configuration#Routing table](/index.php/Network_configuration#Routing_table "Network configuration") for more information on assigning IP addresses.

```
# ip addr add *IP_address*/*subnet_mask* dev vboxnet0
# ip link set dev vboxnet0 up

```

Launch the GNS3 startup wizard and select the GNS3 VM and it should be able to start the VM.

#### Adding VMs to GNS3

When the connection between GNS3 and VirtualBox have been made you need to tell GNS3 which VMs it should see and be able to use.

1.  In GNS3, click on *Preferences > VirtualBox*. Check that the path to vboxwrapper.py (should be `/usr/share/gns3/vboxwrapper.py` and is set per default) is correct (if you get an OK when pressing the "Test Settings"-button, it works, otherwise see the installation step).
2.  Go to the VirtualBox Guest tab to add the VirtualBox VMs in GNS3\. Choose an identifier name, a VM from the VM list (you may have to refresh the list using the provided button). To avoud confusion and possible errors, it is recomended to use the same identifier name as the name of the VM. When a VM is selected you can choose other options for it as well:
    *   Number of NICs is the number of network interface cards you will see inside your VM (e.g. ifconfig on Linux, if you have 4 NICs on your VM, then set it to 4 in GNS3, if you have 1 NIC, then set it to 1 in GNS3).
    *   Reserve first NIC for VirtualBox NAT to host OS is to you have your first network interface card (e.g. eth0 on Linux) configured with network address translation (NAT), allowing your VM to access your host network and Internet (if your host can access it of course).
    *   Enable console support to activate a serial console access to your VM. Please note that serial console support must also be configured on the operating system running in your VirtualBox guest for this feature to work. [Here is a howto for Debian/Ubuntu Linux](http://help.ubuntu.com/community/SerialConsoleHowto).
    *   Enable console server (for remote access) is to remotely access to your VM serial console. GNS3 creates a mini Telnet server that act as a proxy between the serial console and Telnet clients. This feature requires the Enable console support to be enabled.
    *   Start in headless mode (without GUI) will hide the VirtualBox graphical interface when the VM is started. This option is mostly useful if you have configured the previously described console support.

#### Adding VMs to your topology

After you have told GNS3 which VMs is should be able to see you can drag'n'drop them in your topology. Simply select the computer-icon in the left sidebar. You can now choose "VirtualBox guest". Drag this to where you want to add your VM in your topology. When you drop it in you will be prompted about which VM to add. Select the one you want and click OK. You should now be able to boot the VM from GNS3 by right click -> start.

### VMware

To use [VMware](/index.php/VMware "VMware") in GNS3 you need to create a cloud in your GNS3 topology, and then in your VMware machine, connect it to the NIC of the cloud in your topology.

Instructions taken (and ported) from [GNS3 forums](http://forum.gns3.net/topic1139.html):

1.  Select network adapter "Host only" to your Virtual machine in Vmware
2.  Check how this network adapter (`vmnet1`) is named (*ifconfig* should list it).
3.  Add a cloud to your workspace in GNS3.
4.  Configure the cloud and select the network adapter you just looked up.
    *   Right Click on the cloud and select Configure.
    *   Select the C0 on the cloud.
    *   Select NIO Ethernet.
    *   Select Generic Ethernet NIO.
    *   Select the appropriate adapter from the drop-down menu and press the Add button.
    *   The adapter for your virtual machine should now be added to the cloud.
5.  Connect cloud to your topology, for example to a router.
6.  Assing IP addresses (in the same subnet) to the Virtual machine and the emulated router in GNS3.
7.  Ping between router and virtual machine should now be successful, otherwise, try to redo the steps.

## Connecting devices

When devices have been added to your topology you will need to connect them. Select the link-icon (the bottom icon in the left sidebar, looks sort of like a mouse or ethernet-port+rj45 connector), click on a device (like a switch). Next, click on the device (like a VM) you want to connect to the switch. You will be promted to select the NIC which should be used. When you have created all the links you want, click the link-icon in the left sidebar to deselect it, otherwise GNS3 will still be in 'create link'-mode.

## VPCS

VPCS is a simple virtual PC simulator, supported by GNS3 and useful to enhance the simulation of a full working network topology. It can be downloaded from [Sourceforge](https://sourceforge.net/projects/vpcs/files/). The VPCS's executable should be placed inside `~/GNS3` to keep it simple, then GNS3 must be instructed to search the `path/to/executable` (using GNS3 GUI, the option is easily found under *Preferences*).

**Note:** VPCS 0.8b is affected from [this](https://gns3.com/discussions/vpcs-it-just-just-allow-type-one) bug.

## Wireshark packet capture

[Wireshark](/index.php/Wireshark "Wireshark") can be used with GNS3 to "sniff" packets from the links between devices of a virtual topology. Install it, create a symlink under `~/GNS3/wireshark/` directory, then change the settings to instruct GNS3 to use the right version; e.g. if using [wireshark-gtk](https://www.archlinux.org/packages/?name=wireshark-gtk), opting for Wireshark Live Traffic Capture, go to *Preferences > Packet capture preferences* and change:

```
tail -f -c +0b %c | wireshark -o "gui.window_title:%d" -k -i -

```

to

```
tail -f -c +0b %c | wireshark-gtk -o "gui.window_title:%d" -k -i -

```