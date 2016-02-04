# GEDA

The gEDA project has produced and continues working on a full GPL'd suite and toolkit of Electronic Design Automation tools. These tools are used for electrical circuit design, schematic capture, simulation, prototyping, and production. Currently, the gEDA project offers a mature suite of free software applications for electronics design, including schematic capture, attribute management, bill of materials (BOM) generation, netlisting into over 20 netlist formats, analog and digital simulation, and printed circuit board (PCB) layout.

The gEDA project was started because of the lack of free EDA tools for POSIX systems with the primary purpose of advancing the state of free hardware or open source hardware. The suite is mainly being developed on the GNU/Linux platform with some development effort going into making sure the tools run on other platforms as well.

(Source: [gEDA homepage](http://www.gpleda.org/))

## Contents

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
*   [3 First PCB](#First_PCB)
    *   [3.1 Create schematic symbol](#Create_schematic_symbol)
        *   [3.1.1 Schematic Search Path](#Schematic_Search_Path)
    *   [3.2 Create PCB footprint](#Create_PCB_footprint)
    *   [3.3 Create schematic](#Create_schematic)
    *   [3.4 Create and route PCB](#Create_and_route_PCB)
    *   [3.5 Export to gerber](#Export_to_gerber)

## Installation

Installing [geda-gaf](https://www.archlinux.org/packages/?name=geda-gaf) will give you the schematic editor and attribute editor, which is available in the [official repositories](/index.php/Official_repositories "Official repositories"). It may also be necessary to install [ttf-dejavu](https://www.archlinux.org/packages/?name=ttf-dejavu) and [ttf-liberation](https://www.archlinux.org/packages/?name=ttf-liberation) to get the correct font scaling.

Installing [pcb](https://www.archlinux.org/packages/?name=pcb) will give you the PCB editor, available from the [AUR](/index.php/AUR "AUR").

Also you can install [xgsch2pcb](https://aur.archlinux.org/packages/xgsch2pcb/) ([AUR](/index.php/AUR "AUR")), graphical interface to the gsch2pcb command-line tool for converting *.sch to *.pcb.

## Configuration

## First PCB

### Create schematic symbol

You can create new as you are creating schematics themselves. Open an empty file

```
$ gschem mysymbol.sym

```

and add pins with `ap` and attributes with `aa`. Check the [geda wiki](http://wiki.geda-project.org/geda:master_attributes_list) for details. After you are done, do not forget to translate your symbol to absolute zero with `et`. If you do not, your symbol will probably be outside of your viewport once you are going to place it in your schematic.

Save the symbol with `fs` and check it with

```
$ gsymcheck -vv mysymbol.sym

```

#### Schematic Search Path

Do not forget to place your symbol within the search path of gschem. It may also be helpful to extend this path to a folder in your own project by creating a file named `gafrc` in the project folder with the following content

```
(component-library "./symbols")

```

and then copy all symbols required by the project into a subfolder called "symbols".

### Create PCB footprint

### Create schematic

Run schematic editor:

```
$ gschem

```

See also:

[FAQ page](http://wiki.geda-project.org/geda:faq-gschem)

### Create and route PCB

Once you have reached a point of your schematic where you want to start routing the PCB (you can do this in an iterative fashion), it is time to create a gsch2pcb project. Add the following lines to a newly created file, called `firstpcb.prj`:

```
schematics firstpcb.sch
empty-footprint nofootprint
output-name firstpcb

```

This project will read from firstpcb.sch, ignore any parts having a footprint called 'nofootprint' and the output files will start be:

*   The PCB: firstpcb.pcb
*   The netlist: firstpcb.net
*   Pin name commands: firstpcb.cmd
*   ...

If you opted for a local symbols directory, you should include it here. Also you probably want a local footprint directory, too. So add these lines to the prj file:

```
elements-dir footprints
elements-dir symbols

```

Now execute gsch2pcb with this project file:

```
$ gsch2pcb -f firstpcb.prj

```

gsch2pcb will tell you what to do next or if there were any errors.

### Export to gerber

Retrieved from "[https://wiki.archlinux.org/index.php?title=GEDA&oldid=412806](https://wiki.archlinux.org/index.php?title=GEDA&oldid=412806)"