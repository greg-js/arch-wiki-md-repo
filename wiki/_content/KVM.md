# KVM

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

Related articles

*   [Category:Hypervisors](/index.php/Category:Hypervisors "Category:Hypervisors")
*   [Libvirt](/index.php/Libvirt "Libvirt")

**KVM**, Kernel-based Virtual Machine, is a [hypervisor](https://en.wikipedia.org/wiki/hypervisor "wikipedia:hypervisor") built into the Linux kernel. It is similar to [Xen](/index.php/Xen "Xen") in purpose but much simpler to get running. Unlike native [QEMU](/index.php/QEMU "QEMU"), which uses emulation, KVM is a special operating mode of QEMU that uses CPU extensions ([HVM](https://en.wikipedia.org/wiki/Hardware-assisted_virtualization "wikipedia:Hardware-assisted virtualization")) for virtualization via a kernel module.

Using KVM, one can run multiple virtual machines running unmodified GNU/Linux, Windows, or any other operating system. (See [Guest Support Status](http://www.linux-kvm.org/page/Guest_Support_Status) for more information.) Each virtual machine has private virtualized hardware: a network card, disk, graphics card, etc.

Differences between KVM and [Xen](/index.php/Xen "Xen"), [VMware](/index.php/VMware "VMware"), or QEMU can be found at the [KVM FAQ](http://www.linux-kvm.org/page/FAQ#General_KVM_information).

This article does not cover features common to multiple emulators using KVM as a backend. You should see related articles for such information.

## Contents

*   [1 Checking support for KVM](#Checking_support_for_KVM)
    *   [1.1 Hardware support](#Hardware_support)
    *   [1.2 Kernel support](#Kernel_support)
        *   [1.2.1 KVM modules](#KVM_modules)
*   [2 Para-virtualized devices](#Para-virtualized_devices)
    *   [2.1 VIRTIO modules](#VIRTIO_modules)
    *   [2.2 Loading kernel modules](#Loading_kernel_modules)
    *   [2.3 List of para-virtualized devices](#List_of_para-virtualized_devices)
*   [3 How to use KVM](#How_to_use_KVM)
*   [4 Tips and tricks](#Tips_and_tricks)
    *   [4.1 Nested virtualization](#Nested_virtualization)
    *   [4.2 Alternative Networking with SSH tunnels](#Alternative_Networking_with_SSH_tunnels)
    *   [4.3 Enabling huge pages](#Enabling_huge_pages)
*   [5 See also](#See_also)

## Checking support for KVM

### Hardware support

KVM requires that the virtual machine host's processor has virtualization support (named VT-x for Intel processors and AMD-V for AMD processors). You can check whether your processor supports hardware virtualization with the following command:

```
$ lscpu

```

Your processor supports virtualization only if there is a line telling you so.

You can also run:

```
$ egrep --color=auto 'vmx|svm|0xc0f' /proc/cpuinfo

```

If nothing is displayed after running that command, then your processor does **not** support hardware virtualization, and you will **not** be able to use KVM.

**Note:** You may need to enable virtualization support in your BIOS.

### Kernel support

Arch Linux kernels provide the appropriate [kernel modules](/index.php/Kernel_modules "Kernel modules") to support KVM and VIRTIO.

#### KVM modules

You can check if necessary modules (`kvm` and one of `kvm_amd`, `kvm_intel`) are available in your kernel with the following command (assuming your kernel is built with `CONFIG_IKCONFIG_PROC`):

```
$ zgrep CONFIG_KVM /proc/config.gz

```

If the module is not set equal to `y` or `m`, then the module is **not** available.

## Para-virtualized devices

Para-virtualization provides a fast and efficient means of communication for guests to use devices on the host machine. KVM provides para-virtualized devices to virtual machines using the Virtio API as a layer between the hypervisor and guest.

All virtio devices have two parts: the host device and the guest driver.

### VIRTIO modules

Use the following command to check if needed modules are available:

```
$ zgrep CONFIG_VIRTIO /proc/config.gz

```

### Loading kernel modules

First, check if the kernel modules are automatically loaded. This should be the case with recent versions of [udev](/index.php/Udev "Udev").

```
$ lsmod | grep kvm
$ lsmod | grep virtio

```

In case the above commands return nothing, you need to [load](/index.php/Kernel_modules#Loading "Kernel modules") kernel modules.

**Tip:** If modprobing `kvm_intel` or `kvm_amd` fails but modprobing `kvm` succeeds, (and `lscpu` claims that hardware acceleration is supported), check your BIOS settings. Some vendors (especially laptop vendors) disable these processor extensions by default. To determine whether there's no hardware support or there is but the extensions are disabled in BIOS, the output from `dmesg` after having failed to modprobe will tell.

### List of para-virtualized devices

*   network device (virtio-net)
*   block device (virtio-blk)
*   controller device (virtio-scsi)
*   serial device (virtio-serial)
*   balloon device (virtio-balloon)

## How to use KVM

See the main article: [QEMU](/index.php/QEMU "QEMU").

## Tips and tricks

**Note:** See [QEMU#Tips and tricks](/index.php/QEMU#Tips_and_tricks "QEMU") and [QEMU#Troubleshooting](/index.php/QEMU#Troubleshooting "QEMU") for general tips and tricks.

### Nested virtualization

[![Tango-view-fullscreen.png](/images/3/38/Tango-view-fullscreen.png)](/index.php/File:Tango-view-fullscreen.png)

[![Tango-view-fullscreen.png](/images/3/38/Tango-view-fullscreen.png)](/index.php/File:Tango-view-fullscreen.png)

**This article or section needs expansion.**

**Reason:** Is it possible also with `kvm_amd`? (Discuss in [Talk:KVM#](https://wiki.archlinux.org/index.php/Talk:KVM))

Nested virtualization enables existing virtual machines to be run on third-party hypervisors and on other clouds without any modifications to the original virtual machines or their networking.

On host, enable nested feature for `kvm_intel`:

```
# modprobe -r kvm_intel
# modprobe kvm_intel nested=1

```

To make it permanent (see [Kernel modules#Setting module options](/index.php/Kernel_modules#Setting_module_options "Kernel modules")):

 `/etc/modprobe.d/modprobe.conf` 

```
options kvm_intel nested=1

```

Verify that feature is activated:

 `$ systool -m kvm_intel -v | grep nested` 

```
    nested              = "Y"

```

Run guest VM with following command:

```
$ qemu-system-x86_64 -enable-kvm -cpu host

```

Boot VM and check if vmx flag is present:

```
$ egrep --color=auto 'vmx|svm' /proc/cpuinfo

```

### Alternative Networking with SSH tunnels

[![Tango-two-arrows.png](/images/7/72/Tango-two-arrows.png)](/index.php/File:Tango-two-arrows.png)

[![Tango-two-arrows.png](/images/7/72/Tango-two-arrows.png)](/index.php/File:Tango-two-arrows.png)

**This article or section is a candidate for merging with [QEMU](/index.php/QEMU "QEMU").**

**Notes:** This section is not KVM-specific, it's generally applicable to all QEMU VMs. (Discuss in [Talk:KVM#](https://wiki.archlinux.org/index.php/Talk:KVM))

Setting up bridged networking can be a bit of a hassle sometimes. If the sole purpose of the VM is experimentation, one strategy to connect the host and the guests is to use SSH tunneling.

The basic steps are as follows:

*   Setup an SSH server in the host OS
*   (optional) Create a designated user used for the tunneling (e.g. tunneluser)
*   Install SSH in the VM
*   Setup authentication

See: [SSH](/index.php/SSH "SSH") for the setup of SSH, especially [SSH#Forwarding other ports](/index.php/SSH#Forwarding_other_ports "SSH").

When using the default user network stack, the host is reachable at address 10.0.2.2.

[![Tango-mail-mark-junk.png](/images/e/e7/Tango-mail-mark-junk.png)](/index.php/File:Tango-mail-mark-junk.png)

[![Tango-mail-mark-junk.png](/images/e/e7/Tango-mail-mark-junk.png)](/index.php/File:Tango-mail-mark-junk.png)

**This article or section needs language, wiki syntax or style improvements.**

**Reason:** Usage of `/etc/rc.local` is discouraged. This should be a proper [systemd](/index.php/Systemd "Systemd") service file. (Discuss in [Talk:KVM#](https://wiki.archlinux.org/index.php/Talk:KVM))

If everything works and you can SSH into the host, simply add something like the following to your `/etc/rc.local`

```
# Local SSH Server
echo "Starting SSH tunnel"
sudo -u vmuser ssh tunneluser@10.0.2.2 -N -R 2213:127.0.0.1:22 -f
# Random remote port (e.g. from another VM)
echo "Starting random tunnel"
sudo -u vmuser ssh tunneluser@10.0.2.2 -N -L 2345:127.0.0.1:2345 -f

```

In this example a tunnel is created to the SSH server of the VM and an arbitrary port of the host is pulled into the VM.

This is a quite basic strategy to do networking with VMs. However, it is very robust and should be quite sufficient most of the time.

[![Tango-emblem-important.png](/images/c/c8/Tango-emblem-important.png)](/index.php/File:Tango-emblem-important.png)

[![Tango-emblem-important.png](/images/c/c8/Tango-emblem-important.png)](/index.php/File:Tango-emblem-important.png)

**The factual accuracy of this article or section is disputed.**

**Reason:** Isn't this option enough? I think it should have the same effect: `-redir tcp:2222:10.0.2.15:22` (it redirects port 2222 from host to 10.0.2.15:22, where 10.0.2.15 is guest's IP address. (Discuss in [Talk:KVM#](https://wiki.archlinux.org/index.php/Talk:KVM))

### Enabling huge pages

[![Tango-emblem-important.png](/images/c/c8/Tango-emblem-important.png)](/index.php/File:Tango-emblem-important.png)

[![Tango-emblem-important.png](/images/c/c8/Tango-emblem-important.png)](/index.php/File:Tango-emblem-important.png)

**The factual accuracy of this article or section is disputed.**

**Reason:** With systemd, `hugetlbfs` is mounted on `/dev/hugepages` by default, but with mode 0755 and root's uid and gid. (Discuss in [Talk:KVM#](https://wiki.archlinux.org/index.php/Talk:KVM))

[![Tango-two-arrows.png](/images/7/72/Tango-two-arrows.png)](/index.php/File:Tango-two-arrows.png)

[![Tango-two-arrows.png](/images/7/72/Tango-two-arrows.png)](/index.php/File:Tango-two-arrows.png)

**This article or section is a candidate for merging with [QEMU](/index.php/QEMU "QEMU").**

**Notes:** qemu-kvm no longer exists as all of its features have been merged into [qemu](https://www.archlinux.org/packages/?name=qemu). After the above issue is cleared, I suggest merging this section into [QEMU](/index.php/QEMU "QEMU"). (Discuss in [Talk:KVM#](https://wiki.archlinux.org/index.php/Talk:KVM))

You may also want to enable hugepages to improve the performance of your virtual machine. With an up to date Arch Linux and a running KVM you probably already have everything you need. Check if you have the directory `/dev/hugepages`. If not, create it. Now we need the right permissions to use this directory.

Add to your `/etc/fstab`:

```
hugetlbfs       /dev/hugepages  hugetlbfs       mode=1770,gid=78        0 0

```

Of course the gid must match that of the `kvm` group. The mode of `1770` allows anyone in the group to create files but not unlink or rename each other's files. Make sure `/dev/hugepages` is mounted properly:

```
# umount /dev/hugepages
# mount /dev/hugepages
$ mount | grep huge
```

 `hugetlbfs on /dev/hugepages type hugetlbfs (rw,relatime,mode=1770,gid=78)` 

Now you can calculate how many hugepages you need. Check how large your hugepages are:

```
$ grep Hugepagesize /proc/meminfo

```

Normally that should be 2048 kB ≙ 2 MB. Let's say you want to run your virtual machine with 1024 MB. 1024 / 2 = 512\. Add a few extra so we can round this up to 550\. Now tell your machine how many hugepages you want:

```
# echo 550 > /proc/sys/vm/nr_hugepages

```

If you had enough free memory you should see:

 `$ grep HugePages_Total /proc/meminfo ` 

```
HugesPages_Total:  550

```

If the number is smaller, close some applications or start your virtual machine with less memory (number_of_pages x 2):

```
$ qemu-system-x86_64 -enable-kvm -m 1024 -mem-path /dev/hugepages -hda <disk_image> [...]

```

Note the `-mem-path` parameter. This will make use of the hugepages.

Now you can check, while your virtual machine is running, how many pages are used:

 `$ grep HugePages /proc/meminfo ` 

```
HugePages_Total:     550
HugePages_Free:       48
HugePages_Rsvd:        6
HugePages_Surp:        0

```

Now that everything seems to work you can enable hugepages by default if you like. Add to your `/etc/sysctl.d/40-hugepage.conf`:

```
vm.nr_hugepages = 550

```

See also:

*   [https://www.kernel.org/doc/Documentation/vm/hugetlbpage.txt](https://www.kernel.org/doc/Documentation/vm/hugetlbpage.txt)
*   [http://wiki.debian.org/Hugepages](http://wiki.debian.org/Hugepages)
*   [http://www.linux-kvm.com/content/get-performance-boost-backing-your-kvm-guest-hugetlbfs](http://www.linux-kvm.com/content/get-performance-boost-backing-your-kvm-guest-hugetlbfs)

## See also

*   [KVM Howto](http://www.linux-kvm.org/page/HOWTO)
*   [KVM FAQ](http://www.linux-kvm.org/page/FAQ#General_KVM_information)

Retrieved from "[https://wiki.archlinux.org/index.php?title=KVM&oldid=400980](https://wiki.archlinux.org/index.php?title=KVM&oldid=400980)"

[Categories](/index.php/Special:Categories "Special:Categories"):

*   [Hypervisors](/index.php/Category:Hypervisors "Category:Hypervisors")
*   [Kernel](/index.php/Category:Kernel "Category:Kernel")