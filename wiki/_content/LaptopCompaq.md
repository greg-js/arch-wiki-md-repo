# Laptop/Compaq

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

<table style="background-color: #f3f9ff; margin: 1em 2.5% 0 2.5%; border: 1px solid #aaa;">

<tbody>

<tr>

<td align="center" style="padding: 0.5em; font-size: medium;">[Laptop main page](/index.php/Laptop "Laptop")</td>

</tr>

<tr>

<td align="center" style="padding: 0.5em;">[Acer](/index.php/Laptop/Acer "Laptop/Acer") - [Apple](/index.php/Laptop/Apple "Laptop/Apple") - [Asus](/index.php/Laptop/Asus "Laptop/Asus") - **Compaq** - [Dell](/index.php/Laptop/Dell "Laptop/Dell") - [Fujitsu](/index.php/Laptop/Fujitsu "Laptop/Fujitsu") - [HP](/index.php/Laptop/HP "Laptop/HP") - [IBM/Lenovo](/index.php/Laptop/Lenovo "Laptop/Lenovo") - [Samsung](/index.php/Laptop/Samsung "Laptop/Samsung") - [Sony](/index.php/Laptop/Sony "Laptop/Sony") - [Toshiba](/index.php/Laptop/Toshiba "Laptop/Toshiba") - [Other](/index.php/Laptop/Other "Laptop/Other")</td>

</tr>

</tbody>

</table>

## Model List

<table class="wikitable">

<tbody>

<tr>

<th rowspan="2" style="padding: 0.5em;">Model Version</th>

<th rowspan="2" style="padding: 0.5em;">Arch Linux  
Install CD Version  
</th>

<th colspan="8" style="padding: 0.5em;">Hardware Support</th>

<th rowspan="2" style="padding: 0.5em;">Remark</th>

</tr>

<tr>

<th style="padding: 0.5em;">Video</th>

<th style="padding: 0.5em;">Sound</th>

<th style="padding: 0.5em;">Ethernet</th>

<th style="padding: 0.5em;">Wireless</th>

<th style="padding: 0.5em;">Bluetooth</th>

<th style="padding: 0.5em;">Power Management</th>

<th style="padding: 0.5em;">Modem</th>

<th style="padding: 0.5em;">Other</th>

</tr>

<tr>

<td>Compaq nx7300</td>

<td>Duke/2007.5</td>

<td>Intel 955GM + 3D/AIGLX</td>

<td>Intel HD audio with [ALSA](/index.php/ALSA "ALSA")</td>

<td>Yes</td>

<td>Yes, IPW3945</td>

<td>YES</td>

<td>ACPI</td>

<td>Untested</td>

<td>Everything works fantastic. Easiest install of any Linux distribution</td>

</tr>

<tr>

<td>Compaq Presario F700</td>

<td>2009.02</td>

<td>Nvidia 7000M driver: _nvidia_</td>

<td>Nvidia HD audio with ALSA</td>

<td>Nvidia: OK</td>

<td>Atheros: OK  
driver: _ath5k_</td>

<td>none</td>

<td>ACPI  
Suspend to RAM/disk: OK  
Used pm-utils + uswsusp  
CPU frequency scaling: OK</td>

<td>N/A</td>

<td>Hangs for 20-30s when loading ACPI modules when on battery power. Some hotkeys do not work. Need to turn `AutoAddDevices` to `false` in [Xorg](/index.php/Xorg "Xorg") configuration to fix keyboard layout problems.</td>

</tr>

<tr>

<td>Compaq Presario CQ60-420ED</td>

<td>2009.08</td>

<td>Nvidia GeForce 8200M driver: _nvidia_</td>

<td>nVidia MCP72XE/MCP72P/MCP78U/MCP78S HD Audio using ALSA</td>

<td>nVidia MCP77 Ethernet</td>

<td>Atheros AR5001 driver: _ath5k_</td>

<td>none</td>

<td>Using [laptop-mode-tools](https://aur.archlinux.org/packages/laptop-mode-tools/)<sup><small>AUR</small></sup> and [cpupower](https://www.archlinux.org/packages/?name=cpupower) (replaces _cpufrequtils_), haven't properly tested yet</td>

<td>Untested</td>

<td>The console framebuffer is a bit slow (using `vga=773` in [GRUB](/index.php/GRUB "GRUB")) and the wireless LED indicator flickers red and blue. Touchpad (scrolling) works with GNOME</td>

</tr>

<tr>

<td>[Compaq Armada M300](/index.php/Compaq_Armada_M300 "Compaq Armada M300")</td>

<td>2010.05</td>

<td>ATI 3D Rage LT Pro driver: _mach64_</td>

<td>ESS Technology ES1978 Maestro 2E</td>

<td>Intel 82557/8/9/0/1</td>

<td>none</td>

<td>none</td>

<td>ACPI + [cpupower](https://www.archlinux.org/packages/?name=cpupower) (replaces _cpufrequtils_)</td>

<td>Untested</td>

<td>Everything is perfect except for 3D support.</td>

</tr>

</tbody>

</table>

Retrieved from "[https://wiki.archlinux.org/index.php?title=Laptop/Compaq&oldid=375517](https://wiki.archlinux.org/index.php?title=Laptop/Compaq&oldid=375517)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [Laptops](/index.php/Category:Laptops "Category:Laptops")