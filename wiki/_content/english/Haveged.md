The [haveged project](http://www.issihosts.com/haveged/) is an attempt to provide an easy-to-use, unpredictable [random number generator](/index.php/Random_number_generator "Random number generator") based upon an adaptation of the HAVEGE algorithm. Haveged was created to remedy low-entropy conditions in the Linux random device that can occur under some workloads, especially on headless servers.

**Warning:** The quality of the generated entropy is not guaranteed and sometimes contested (see [LCE: Do not play dice with random numbers](https://lwn.net/Articles/525459/) and [Is it appropriate to use haveged as a source of entropy on virtual machines?](http://security.stackexchange.com/questions/34523/is-it-appropriate-to-use-haveged-as-a-source-of-entropy-on-virtual-machines)). Use it at your own risk or use it with a hardware based random number generator with the [rng-tools](https://www.archlinux.org/packages/?name=rng-tools) (see Alternative section)

## Contents

*   [1 Alternative](#Alternative)
*   [2 List available entropy](#List_available_entropy)
*   [3 Virtual machines](#Virtual_machines)
*   [4 Installation](#Installation)
*   [5 Service](#Service)
*   [6 See also](#See_also)

## Alternative

Unless you have a specific reason to not trust any hardware random number generator on your system, you should try to use them with the [rng-tools](/index.php/Rng-tools "Rng-tools") first and if it turns out not to be enough (or if you do not have a hardware random number generator available), then use Haveged.

## List available entropy

If you are not sure, whether you need haveged, run:

```
# cat /proc/sys/kernel/random/entropy_avail

```

This command shows you how much entropy your server has collected. If it is rather low (<1000), you should probably install haveged. Otherwise cryptographic applications will block until there is enough entropy available, which eg. could result in slow wlan speed, if your server is a [Software access point](/index.php/Software_access_point "Software access point").

You should use this command again to verify how much haveged boosted your entropy pool after the installation.

## Virtual machines

As discussed at [Is it appropriate to use haveged as a source of entropy on virtual machines?](http://security.stackexchange.com/questions/34523/is-it-appropriate-to-use-haveged-as-a-source-of-entropy-on-virtual-machines), it can be contested whether haveged provides quality entropy within a virtual environment. Haveged relies on the rdtsc instruction, which may be virtualized within a virtual machine resulting in lower quantity entropy. On some hypervisors, it is possible to disable the virtualization of rdtsc, which would in theory allow haveged to provide higher quality entropy.

To disable the virtualization of the rdtsc instruction in VMware ESXi, add the setting `monitor_control.virtual_rdtsc = "FALSE"` to the virtual machine’s .vmx configuration file. VMware recommends the setting for use when performing measurements that require a precise source of real time in the virtual machine. [[1]](http://www.vmware.com/files/pdf/Timekeeping-In-VirtualMachines.pdf)

## Installation

[Install](/index.php/Install "Install") the [haveged](https://www.archlinux.org/packages/?name=haveged) package from the [official repositories](/index.php/Official_repositories "Official repositories").

## Service

The package provides `haveged.service`, see [systemd](/index.php/Systemd "Systemd") for details.

## See also

*   [http://www.issihosts.com/haveged](http://www.issihosts.com/haveged)
*   [http://www.digitalocean.com/community/tutorials/how-to-setup-additional-entropy-for-cloud-servers-using-haveged](http://www.digitalocean.com/community/tutorials/how-to-setup-additional-entropy-for-cloud-servers-using-haveged)