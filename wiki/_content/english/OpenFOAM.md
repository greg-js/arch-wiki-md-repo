The OpenFOAM® (Open Field Operation and Manipulation) CFD Toolbox is a free, open source CFD software package produced by OpenCFD Ltd. It has a large user base across most areas of engineering and science, from both commercial and academic organisations. OpenFOAM has an extensive range of features to solve anything from complex fluid flows involving chemical reactions, turbulence and heat transfer, to solid dynamics and electromagnetics. It includes tools for meshing, notably snappyHexMesh, a parallelised mesher for complex CAD geometries, and for pre- and post-processing. Almost everything (including meshing, and pre- and post-processing) runs in parallel as standard, enabling users to take full advantage of computer hardware at their disposal.

For more information on OpenFOAM and the OpenFOAM Foundation, please see [http://www.openfoam.com](http://www.openfoam.com) and [http://www.openfoam.org](http://www.openfoam.org) respectively.

## Contents

*   [1 Basic installation](#Basic_installation)
*   [2 Development installation](#Development_installation)
    *   [2.1 Prerequisites](#Prerequisites)
    *   [2.2 Obtain source files](#Obtain_source_files)
        *   [2.2.1 Latest stable release](#Latest_stable_release)
    *   [2.3 Environment variables](#Environment_variables)

## Basic installation

If you do not plan on doing development tasks with OpenFOAM, there is an updated version of the program available in the [AUR](/index.php/AUR "AUR") package [openfoam](https://aur.archlinux.org/packages/openfoam/) and git versions [openfoam2.4-git](https://aur.archlinux.org/packages/openfoam2.4-git/) or [openfoam3.0-git](https://aur.archlinux.org/packages/openfoam3.0-git/). For most users, this will be everything needed to get an installation up and running.

An **openfoam3.0.1** package is also available from the unofficial [home_Minerva_W_Science_Arch_Extra](/index.php/Unofficial_user_repositories#home_Minerva_W_Science_Arch_Extra "Unofficial user repositories") repository. Development and older versions are planned to be added as of April 2016.

## Development installation

For installation of OpenFOAM in a development environment, the process is fairly straight forward on Arch Linux. The basic steps are as follows:

1.  Obtain source files from OpenFOAM
2.  Prepare build directory
3.  Create Preference File and Set Environment Variables for your installation
4.  Compile OpenFOAM sources
5.  Test OpenFOAM installation

### Prerequisites

*   [openmpi](https://www.archlinux.org/packages/?name=openmpi)
*   [paraview](https://aur.archlinux.org/packages/paraview/)
*   [parmetis](https://aur.archlinux.org/packages/parmetis/)
*   [scotch](https://aur.archlinux.org/packages/scotch/)
*   [boost-libs](https://www.archlinux.org/packages/?name=boost-libs)
*   [boost](https://www.archlinux.org/packages/?name=boost)

### Obtain source files

#### Latest stable release

### Environment variables

Paste the following code into your ~/.bashrc file. Whenever you want to run OpenFOAM you just have to type of20x to initialize the environment.

```
# OpenFOAM Install
export FOAM_INST_DIR='$HOME/.OpenFOAM'
alias of20x='source $FOAM_INST_DIR/OpenFOAM-2.0.x/etc/bashrc'
```