[KiCad](http://kicad-pcb.org/) is an open source software suite for Electronic Design Automation (EDA). The programs handle Schematic Capture, and PCB Layout with Gerber output.

## Installation

[Install](/index.php/Install "Install") the [kicad](https://www.archlinux.org/packages/?name=kicad) and [kicad-library](https://www.archlinux.org/packages/?name=kicad-library) package. Optionally you can install the [kicad-library-3d](https://www.archlinux.org/packages/?name=kicad-library-3d) package, which provides 3D models for certain components.

### Upstream

The [AUR](/index.php/AUR "AUR") provides the packages [kicad-git](https://aur.archlinux.org/packages/kicad-git/), [kicad-symbols-git](https://aur.archlinux.org/packages/kicad-symbols-git/), [kicad-footprints-git](https://aur.archlinux.org/packages/kicad-footprints-git/). Optionally you can also install [kicad-packages3d-git](https://aur.archlinux.org/packages/kicad-packages3d-git/) and [kicad-templates-git](https://aur.archlinux.org/packages/kicad-templates-git/).

### Usage Guide

Getting started guide available [here](https://kicad-pcb.org/help/getting-started).
(From the above guide)
The basic workflow in KiCad is:

*   Create a project.
*   Create a schematic with 'eeschema'.
*   Assign footprints to symbols and generate the netlist.
*   Create a board with 'pcbnew', importing the netlist from 'eeschema'.
*   Test the board using the 'Design Rule Check'.
*   Generate production files.

Other KiCAD [Documentation](https://docs.kicad-pcb.org/)