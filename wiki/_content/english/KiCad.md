[KiCad](http://kicad-pcb.org/) is an open source software suite for Electronic Design Automation (EDA). The programs handle Schematic Capture, and PCB Layout with Gerber output.

## Installation

[Install](/index.php/Install "Install") the [kicad](https://www.archlinux.org/packages/?name=kicad) and [kicad-library](https://www.archlinux.org/packages/?name=kicad-library) package. Optionally you can install the [kicad-library-3d](https://www.archlinux.org/packages/?name=kicad-library-3d) package, which provides 3D models for certain components.

### Upstream Libraries

To have the most recent footprints, 3D models and tempaltes available, you can clone the upstream repositories and refere to them in the kicad config.

**Note:** Sadly, for the current version KiCad 4.0.7 (as of february 2018) doesn't support modifying the symbol library path. Appearently this will change in the version 5.x.x, which is not stable yet.

**Warning:** Using upstream libraries may result in warning messages during runtime.

```
mkdir -p ~/lib/KiCad                                       # create directory to footprint, 3D model and template repositories in
cd ~/lib/KiCad
git clone git@github.com:serioeseGmbH/kicad-footprints.git
git clone git@github.com:serioeseGmbH/kicad-packages3D.git # optional
git clone git@github.com:serioeseGmbH/kicad-templates.git  # optional

```

Change `KICAD_PTEMPLATES`, `KISYS3DMOD` and `KISYSMOD` accordingly in the kicad_common config.

 `~/.config/kicad/kicad_common` 
```
WorkingDir=/home/marble
ShowEnvVarWarningDialog=1
kicad_fplib_url=[https://github.com/KiCad](https://github.com/KiCad)
[EnvironmentVariables]
KICAD_PTEMPLATES=/home/user_name_here/lib/KiCad/kicad-templates/
KIGITHUB=[https://github.com/KiCad](https://github.com/KiCad)
KISYS3DMOD=/home/user_name_here/lib/KiCad/kicad-packages3D/
KISYSMOD=/home/user_name_here/lib/KiCad/kicad-footprints/
```