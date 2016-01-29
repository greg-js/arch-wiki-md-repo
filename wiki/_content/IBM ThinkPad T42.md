# IBM ThinkPad T42

Related articles

*   [Wireless network configuration](/index.php/Wireless_network_configuration "Wireless network configuration")

This page documents configuration and troubleshooting of the IBM ThinkPad T42.

## Contents

*   [1 ACPI](#ACPI)
*   [2 CPU frequency scaling](#CPU_frequency_scaling)
*   [3 Suspend and hibernate](#Suspend_and_hibernate)
*   [4 Wireless](#Wireless)
    *   [4.1 IBM Cards](#IBM_Cards)
    *   [4.2 Intel Cards](#Intel_Cards)
*   [5 See Also](#See_Also)

## ACPI

If not already loaded, use [modprobe](/index.php/Modprobe "Modprobe") to load the `thinkpad_acpi` module. See the [acpi](/index.php/Acpi "Acpi") and [laptop](/index.php/Laptop "Laptop") articles for more information.

See [http://www.thinkwiki.org/wiki/How_to_make_ACPI_work](http://www.thinkwiki.org/wiki/How_to_make_ACPI_work) for more ThinkPad specific information.

## CPU frequency scaling

See [cpufrequtils](/index.php/Cpufrequtils "Cpufrequtils").

## Suspend and hibernate

See [Suspend and hibernate](/index.php/Suspend_and_hibernate "Suspend and hibernate").

## Wireless

The MiniPCI slot on the T42 usually comes with 1 of 6 wireless cards, 3 by IBM and 3 by Intel.

### IBM Cards

*   IBM 11b/g Wireless LAN Mini PCI Adapter
*   IBM 11a/b/g Wireless LAN Mini PCI Adapter
*   IBM 11a/b/g Wireless LAN Mini PCI Adapter II

For the `ath5k` module, please read the following article: [Wireless Setup#ath5k](/index.php/Wireless_Setup#ath5k "Wireless Setup").

If using the `ath_pci` module, you may need to [blacklist](/index.php/Modprobe#Blacklisting "Modprobe") the `ath5k` module.

### Intel Cards

See the following: [Wireless Setup#ipw2100 and ipw2200](/index.php/Wireless_Setup#ipw2100_and_ipw2200 "Wireless Setup").

*   Intel PRO/Wireless LAN 2100 3B Mini PCI Adapter (use [ipw2100](/index.php/Wireless_network_configuration#ipw2100_and_ipw2200 "Wireless network configuration"))
*   Intel PRO/Wireless 2200BG Mini-PCI Adapter (use [ipw2200](/index.php/Wireless_network_configuration#ipw2100_and_ipw2200 "Wireless network configuration"))
*   Intel PRO/Wireless 2915ABG Mini-PCI Adapter (use [ipw2200](/index.php/Wireless_network_configuration#ipw2100_and_ipw2200 "Wireless network configuration"))

## See Also

*   [T42 ThinkWiki page](http://www.thinkwiki.org/wiki/Category:)

Retrieved from "[https://wiki.archlinux.org/index.php?title=IBM_ThinkPad_T42&oldid=376817](https://wiki.archlinux.org/index.php?title=IBM_ThinkPad_T42&oldid=376817)"