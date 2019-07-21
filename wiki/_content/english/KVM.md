Related articles

*   [Category:Hypervisors](/index.php/Category:Hypervisors "Category:Hypervisors")
*   [Libvirt](/index.php/Libvirt "Libvirt")

**KVM**, [Kernel-based Virtual Machine](https://en.wikipedia.org/wiki/Kernel-based_Virtual_Machine "wikipedia:Kernel-based Virtual Machine"), is a [hypervisor](https://en.wikipedia.org/wiki/hypervisor "wikipedia:hypervisor") built into the Linux kernel. It is similar to [Xen](/index.php/Xen "Xen") in purpose but much simpler to get running. Unlike native [QEMU](/index.php/QEMU "QEMU"), which uses emulation, KVM is a special operating mode of QEMU that uses CPU extensions ([HVM](https://en.wikipedia.org/wiki/Hardware-assisted_virtualization "wikipedia:Hardware-assisted virtualization")) for virtualization via a kernel module.

Using KVM, one can run multiple virtual machines running unmodified GNU/Linux, Windows, or any other operating system. (See [Guest Support Status](http://www.linux-kvm.org/page/Guest_Support_Status) for more information.) Each virtual machine has private virtualized hardware: a network card, disk, graphics card, etc.

Differences between KVM and [Xen](/index.php/Xen "Xen"), [VMware](/index.php/VMware "VMware"), or QEMU can be found at the [KVM FAQ](http://www.linux-kvm.org/page/FAQ#General_KVM_information).

This article does not cover features common to multiple emulators using KVM as a backend. You should see related articles for such information.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Checking support for KVM](#Checking_support_for_KVM)
    *   [1.1 Hardware support](#Hardware_support)
    *   [1.2 Kernel support](#Kernel_support)
*   [2 Para-virtualization with Virtio](#Para-virtualization_with_Virtio)
    *   [2.1 Kernel support](#Kernel_support_2)
    *   [2.2 List of para-virtualized devices](#List_of_para-virtualized_devices)
*   [3 How to use KVM](#How_to_use_KVM)
*   [4 Tips and tricks](#Tips_and_tricks)
    *   [4.1 Nested virtualization](#Nested_virtualization)
    *   [4.2 Enabling huge pages](#Enabling_huge_pages)
*   [5 See also](#See_also)

## Checking support for KVM

### Hardware support

KVM requires that the virtual machine host's processor has virtualization support (named VT-x for Intel processors and AMD-V for AMD processors). You can check whether your processor supports hardware virtualization with the following command:

```
$ LC_ALL=C lscpu | grep Virtualization

```

Alternatively:

```
$ grep -E --color=auto 'vmx|svm|0xc0f' /proc/cpuinfo

```

If nothing is displayed after running either command, then your processor does **not** support hardware virtualization, and you will **not** be able to use KVM.

**Note:** You may need to enable virtualization support in your BIOS.

### Kernel support

Arch Linux kernels provide the required [kernel modules](/index.php/Kernel_modules "Kernel modules") to support KVM.

*   One can check if the necessary modules, `kvm` and either `kvm_amd` or `kvm_intel`, are available in the kernel with the following command:

```
$ zgrep CONFIG_KVM /proc/config.gz

```

The module is available only if it is set to either `y` or `m`.

*   Then, ensure that the kernel modules are automatically loaded, with the command:

 `$ lsmod | grep kvm` 
```
kvm_intel             245760  0
kvmgt                  28672  0
mdev                   20480  2 kvmgt,vfio_mdev
vfio                   32768  3 kvmgt,vfio_mdev,vfio_iommu_type1
kvm                   737280  2 kvmgt,kvm_intel
irqbypass              16384  1 kvm

```

If the command returns nothing, the module needs to be loaded manually, see [Kernel modules#Manual module handling](/index.php/Kernel_modules#Manual_module_handling "Kernel modules").

**Tip:** If modprobing `kvm_intel` or `kvm_amd` fails but modprobing `kvm` succeeds, and `lscpu` claims that hardware acceleration is supported, check the BIOS settings. Some vendors, especially laptop vendors, disable these processor extensions by default. To determine whether there is no hardware support or whether the extensions are disabled in BIOS, the output from `dmesg` after having failed to modprobe will tell.

## Para-virtualization with Virtio

Para-virtualization provides a fast and efficient means of communication for guests to use devices on the host machine. KVM provides para-virtualized devices to virtual machines using the **Virtio** API as a layer between the hypervisor and guest.

All Virtio devices have two parts: the host device and the guest driver.

### Kernel support

*   Use the following command to check if the VIRTIO modules are available in the kernel: `$ zgrep VIRTIO /proc/config.gz` 
*   Then, check if the kernel modules are automatically loaded with the command: `$ lsmod | grep virtio` 

In case the above commands return nothing, you need to [Kernel modules#Manual module handling](/index.php/Kernel_modules#Manual_module_handling "Kernel modules") kernel modules.

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

Nested virtualization enables existing virtual machines to be run on third-party hypervisors and on other clouds without any modifications to the original virtual machines or their networking.

On host, enable nested feature for `kvm_intel`:

```
# modprobe -r kvm_intel
# modprobe kvm_intel nested=1

```

To make it permanent (see [Kernel modules#Setting module options](/index.php/Kernel_modules#Setting_module_options "Kernel modules")):

 `/etc/modprobe.d/kvm_intel.conf`  `options kvm_intel nested=1` 

Verify that feature is activated:

 `$ systool -m kvm_intel -v | grep nested`  `nested              = "Y"` 

Enable the "host passthrough" mode to forward all CPU features to the guest system:

1.  If using [QEMU](/index.php/QEMU "QEMU"), run the guest virtual machine with the following command: `qemu-system-x86_64 -enable-kvm -cpu host`.
2.  If using *virt-manager*, change the CPU model to `host-passthrough` (it will not be in the list, just write it in the box).
3.  If using *virsh*, use `virsh edit *vm-name*` and change the CPU line to `<cpu mode='host-passthrough' check='partial'/>`

Boot VM and check if vmx flag is present:

```
$ grep -E --color=auto 'vmx|svm' /proc/cpuinfo

```

### Enabling huge pages

You may also want to enable hugepages to improve the performance of your virtual machine. With an up to date Arch Linux and a running KVM you probably already have everything you need. Check if you have the directory `/dev/hugepages`. If not, create it. Now we need the right permissions to use this directory. The default permission is root's uid and gid with 0755, but we want anyone in the kvm group to have access to hugepages.

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

Normally that should be 2048 kB ≙ 2 MB. Let us say you want to run your virtual machine with 1024 MB. 1024 / 2 = 512\. Add a few extra so we can round this up to 550\. Now tell your machine how many hugepages you want:

```
# echo 550 > /proc/sys/vm/nr_hugepages

```

If you had enough free memory you should see:

 `$ grep HugePages_Total /proc/meminfo` 
```
HugesPages_Total:  550

```

If the number is smaller, close some applications or start your virtual machine with less memory (number_of_pages x 2):

```
$ qemu-system-x86_64 -enable-kvm -m 1024 -mem-path /dev/hugepages -hda <disk_image> [...]

```

Note the `-mem-path` parameter. This will make use of the hugepages.

Now you can check, while your virtual machine is running, how many pages are used:

 `$ grep HugePages /proc/meminfo` 
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

*   [summary of hugetlbpage support in the Linux kernel](https://www.kernel.org/doc/Documentation/vm/hugetlbpage.txt)
*   [Debian Wiki - Hugepages](https://wiki.debian.org/Hugepages "debian:Hugepages")

## See also

*   [KVM Howto](http://www.linux-kvm.org/page/HOWTO)
*   [KVM FAQ](http://www.linux-kvm.org/page/FAQ#General_KVM_information)