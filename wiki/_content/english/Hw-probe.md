[Hw-probe](https://github.com/linuxhw/hw-probe) is a tool to check operability of hardware devices, collect system logs and contribute to the [Arch Linux hardware database](https://linux-hardware.org/?distro=Arch) and the [List of devices with poor Linux-compatibility](https://github.com/linuxhw/HWInfo).

## Installation

[Install](/index.php/Install "Install") the [hw-probe](https://aur.archlinux.org/packages/hw-probe/) package.

## Usage

Make a probe:

```
# hw-probe -all -upload

```

Decode ACPI tables (requires [acpica](https://www.archlinux.org/packages/?name=acpica) package):

```
# hw-probe -all -upload -decode-acpi

```

Perform simple graphics test (requires [mesa-demos](https://www.archlinux.org/packages/?name=mesa-demos) package):

```
# hw-probe -all -upload -check

```

Import created probes to a local directory:

```
# hw-probe -import *directory*

```

## See also

*   [lspci, and other hardware detection related tools](https://en.wikipedia.org/wiki/Lspci "wikipedia:Lspci")