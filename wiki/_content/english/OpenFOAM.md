According to [Wikipedia](https://en.wikipedia.org/wiki/OpenFOAM "wikipedia:OpenFOAM"):

	OpenFOAM (for "Open source Field Operation And Manipulation") is a [C++](/index.php/C%2B%2B "C++") toolbox for the development of customized [numerical solvers](https://en.wikipedia.org/wiki/numerical_analysis "wikipedia:numerical analysis"), and pre-/post-processing utilities for the solution of [continuum mechanics](https://en.wikipedia.org/wiki/continuum_mechanics "wikipedia:continuum mechanics") problems, including [computational fluid dynamics](https://en.wikipedia.org/wiki/computational_fluid_dynamics "wikipedia:computational fluid dynamics") (CFD).

## Contents

*   [1 Basic installation](#Basic_installation)
*   [2 Development installation](#Development_installation)
    *   [2.1 Prerequisites](#Prerequisites)
    *   [2.2 Obtain source files](#Obtain_source_files)
        *   [2.2.1 Latest stable release](#Latest_stable_release)
    *   [2.3 Environment variables](#Environment_variables)
*   [3 Troubleshooting](#Troubleshooting)
    *   [3.1 zsh](#zsh)
    *   [3.2 Paraview not installed](#Paraview_not_installed)
*   [4 See also](#See_also)

## Basic installation

If you do not plan on doing development tasks with OpenFOAM, there is an updated version of the program available in the [AUR](/index.php/AUR "AUR") package [openfoam](https://aur.archlinux.org/packages/openfoam/) and git versions [openfoam2.4-git](https://aur.archlinux.org/packages/openfoam2.4-git/) or [openfoam3.0-git](https://aur.archlinux.org/packages/openfoam3.0-git/). For most users, this will be everything needed to get an installation up and running.

## Development installation

For installation of OpenFOAM in a development environment, the process is fairly straight forward on Arch Linux. The basic steps are as follows:

1.  Obtain source files from OpenFOAM
2.  Prepare build directory
3.  Create Preference File and Set Environment Variables for your installation
4.  Compile OpenFOAM sources
5.  Test OpenFOAM installation

### Prerequisites

*   [openmpi](https://www.archlinux.org/packages/?name=openmpi)
*   [paraview](https://www.archlinux.org/packages/?name=paraview)
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

## Troubleshooting

### zsh

Some things don't work straightforward if you are not using bash. In the case of zsh, you will need the [bash-completion](https://www.archlinux.org/packages/?name=bash-completion) package, and add the following to your `.zshrc` for the OpenFOAM scripts to work.

```
autoload bashcompinit
bashcompinit
```

Add `export FOAM_INST_DIR=/opt/OpenFOAM` to your `.zshenv` and `alias ofoam="source ${FOAM_INST_DIR}/OpenFOAM-5.0/etc/bashrc"` to your `.zshrc`.

### Paraview not installed

This happens because the dependencies are installed as separate packages, and not in the third-party apps directory of OpenFOAM. Either;

*   Add `alias paraFoam='paraFoam -builtin'` to your `/opt/OpenFOAM/Open-FOAM-X.X/etc/bashrc`.
*   For each project, `touch `echo "${PWD##*/}"`.foam` and then open the touched file from paraview.

## See also

*   [Official website](https://openfoam.org/)