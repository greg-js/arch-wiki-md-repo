Related articles

*   [List of applications/Science](/index.php/List_of_applications/Science "List of applications/Science")

According to the [official website](http://www.gromacs.org/), GROMACS is:

	a versatile package to perform [molecular dynamics](https://en.wikipedia.org/wiki/Molecular_dynamics "wikipedia:Molecular dynamics"), i.e. simulate the Newtonian equations of motion for systems with hundreds to millions of particles.

	It is primarily designed for biochemical molecules like proteins, lipids and nucleic acids that have a lot of complicated bonded interactions, but since GROMACS is extremely fast at calculating the nonbonded interactions (that usually dominate simulations) many groups are also using it for research on non-biological systems, e.g. polymers.

**Note:** GROMACS should not be used as a [black box](https://en.wikipedia.org/wiki/black_box "wikipedia:black box"). The user is strongly encouraged to read and study the scientific papers related to the methods and force fields that are employed by GROMACS.

## Contents

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
*   [3 Usage](#Usage)
    *   [3.1 Setup](#Setup)
        *   [3.1.1 Obtain structure file](#Obtain_structure_file)
        *   [3.1.2 Generate a topology](#Generate_a_topology)
        *   [3.1.3 Box creation](#Box_creation)
        *   [3.1.4 Adding ions](#Adding_ions)
        *   [3.1.5 Parameter files](#Parameter_files)
    *   [3.2 Running](#Running)
        *   [3.2.1 Basics](#Basics)
        *   [3.2.2 Acceleration & Parallelization](#Acceleration_&_Parallelization)
        *   [3.2.3 Restart a simulation](#Restart_a_simulation)
        *   [3.2.4 Extend a simulation](#Extend_a_simulation)
    *   [3.3 Analysis](#Analysis)
        *   [3.3.1 Tools](#Tools)
        *   [3.3.2 Index Files](#Index_Files)
*   [4 Development](#Development)
*   [5 Tips and tricks](#Tips_and_tricks)
    *   [5.1 Create non-cubic box and fill with solvent](#Create_non-cubic_box_and_fill_with_solvent)
    *   [5.2 Use multiple solutes](#Use_multiple_solutes)
    *   [5.3 Use a non-water solvent](#Use_a_non-water_solvent)
*   [6 See also](#See_also)
    *   [6.1 Structure and Topology Databases](#Structure_and_Topology_Databases)
    *   [6.2 Development](#Development_2)
    *   [6.3 Documentation](#Documentation)
    *   [6.4 External libraries & programs](#External_libraries_&_programs)
        *   [6.4.1 Analysis libraries](#Analysis_libraries)
        *   [6.4.2 Free energy calculations](#Free_energy_calculations)
        *   [6.4.3 Structure creation](#Structure_creation)
        *   [6.4.4 Topology generation](#Topology_generation)
        *   [6.4.5 Visualization](#Visualization)
        *   [6.4.6 Wrappers](#Wrappers)
    *   [6.5 Tutorials](#Tutorials)

## Installation

[Install](/index.php/Install "Install") the [gromacs](https://aur.archlinux.org/packages/gromacs/) or [gromacs-mpi](https://aur.archlinux.org/packages/gromacs-mpi/) package. Be sure to [edit](/index.php/Textedit "Textedit") the [PKGBUILD](/index.php/PKGBUILD "PKGBUILD") to suit your system (i.e. for MPI or GPU support). Some of the [cmake](https://en.wikipedia.org/wiki/cmake "wikipedia:cmake") options you may want to add/modify in the PKGBUILD are (cf.[the latest GROMACS installation guide](http://manual.gromacs.org/documentation/)):

*   `-DGMX_DOUBLE=ON` - Add if you need [double precision](https://en.wikipedia.org/wiki/Double-precision_floating-point_format "wikipedia:Double-precision floating-point format"). According to the GROMACS install guide, double precision is "slower, and not normally useful." If you set this flag, the default suffix for all GROMACS programs is set to `_d`.
*   `-DGMX_GPU=ON` - Add in order to build with [GPU](https://en.wikipedia.org/wiki/Graphics_processing_unit "wikipedia:Graphics processing unit") support. Several other flags may be necessary; refer to the latest GROMACS installation guide.
*   `-DGMX_MPI=ON` - Add to create a build able to run across multiple compute nodes. You will also need to have an [MPI](https://en.wikipedia.org/wiki/Message_Passing_Interface "wikipedia:Message Passing Interface") library such as [openmpi](https://www.archlinux.org/packages/?name=openmpi) or [mpich](https://aur.archlinux.org/packages/mpich/). If you do not need MPI support (*i.e.*, you just run on a single computer), you do not need this flag. If you set this flag, the default suffix for all GROMACS programs is set to `_mpi`.
*   `-DGMX_SIMD=*xxx*` - GROMACS should detect the best [SIMD](https://en.wikipedia.org/wiki/simd "wikipedia:simd") instructions for your processor, so this flag should not be needed. But if you have some kind of compilation error, you can specify the SIMD level here. A list of available options for `*xxx*` is listed in the latest GROMACS installation guide.

**Note:** If you are compiling on a Haswell processor, you may need to configure [makepkg](/index.php/Makepkg "Makepkg") to use `-march=native` to successfully compile with AVX2_256 instructions.

*   `-DGMX_X11=ON` - Set to use `gmx view`, the built-in trajectory viewer. This flag requires the [openmotif](https://www.archlinux.org/packages/?name=openmotif) and [libx11](https://www.archlinux.org/packages/?name=libx11) packages.
*   `-DREGRESSIONTEST_DOWNLOAD=ON` - Set to test your GROMACS build. To run the tests [set your build to run](/index.php/Creating_packages#check.28.29 "Creating packages") `make check`. The [libxml2](https://www.archlinux.org/packages/?name=libxml2) package is required.
*   `-DGMX_DEFAULT_SUFFIX=OFF` - Set to turn of default suffix for GROMACS programs for MPI or double precision builds.
*   `-DGMX_BINARY_SUFFIX=*xxx*` and `-DGMX_LIBS_SUFFIX=*xxx*` - Set the default suffix to *xxx* for binaries and libraries, respectively.

Some other packages that may increase performance are:

*   [boost-libs](https://www.archlinux.org/packages/?name=boost-libs) - An external [Boost library](https://en.wikipedia.org/wiki/Boost_(C%2B%2B_libraries) can be used to provide better implementation support for smart pointers and exception handling.
*   [hwloc](https://www.archlinux.org/packages/?name=hwloc) - Run-time detection of hardware capabilities can be improved by linking with hwloc
*   [lapack](https://www.archlinux.org/packages/?name=lapack) - Hardware-optimized BLAS and LAPACK libraries are useful for a few of the GROMACS utilities focused on normal modes and matrix manipulation, but they do not provide any benefits for normal simulations.

The [gromacs-git](https://aur.archlinux.org/packages/gromacs-git/) package contains the latest development source, and should not be used in production.

## Configuration

By default the top-level force field directory is located at `/usr/share/gromacs/top`. This can be changed by setting a different directory to the `GMXLIB` [environment variable](/index.php/Environment_variable "Environment variable"). This is useful if you make modifications to a force field, or if you have another set of force fields you would like to use.

## Usage

Below is a basic workflow with most of the major commands mentioned. Every command should begin with `gmx`. For more details on using GROMACS [find a good tutorial and read the manual](#See_also). A helpful flow chart is [here](http://manual.gromacs.org/online/flow.html).

**Tip:** Each command has its own [man page](/index.php/Man_page "Man page"), with a hyphen substituted for the space in between `gmx` and the command. For example, the man page for *gmx pdb2gmx* is located at `gmx-pdb2gmx`.

### Setup

Simulations require a structure file (`.gro`/`.pdb`), a topology file (`.top`), and a parameters file (`.mdp`). The following steps illustrate how to obtain these.

#### Obtain structure file

A structure file, which contains the coordinates of all particles, can be obtained from a [protein database](https://en.wikipedia.org/wiki/Protein_Data_Bank "wikipedia:Protein Data Bank") or created by the user using a [program](#See_also).

**Tip:** One can use any structure file format (*e.g*, the [PDB file format](https://en.wikipedia.org/wiki/Protein_Data_Bank_(file_format) "wikipedia:Protein Data Bank (file format)")) with most GROMACS programs, not just the [GROMACS format](https://en.wikipedia.org/wiki/Chemical_file_format#GROMACS_format "wikipedia:Chemical file format").

#### Generate a topology

A topology file indicates how atomic particles interact with one another. One method for generating a topology file is to use *gmx pdb2gmx*. If your solute is in a file named `protein.pdb`, do the following:

```
$ gmx pdb2gmx -f protein.pdb

```

Then you will be prompted to select a [force field](https://en.wikipedia.org/wiki/Force_field_(chemistry) and [water model](https://en.wikipedia.org/wiki/Water_model "wikipedia:Water model"). A new structure file in gro format will be generated (`conf.gro`) as well as the corresponding topology file (`topol.top`).

If you did not obtain your structure file from a protein database, but instead created it yourself, most likely you will need to create a residue template file (`.rtp`) for your molecule as well as update the `.pdb` file. An example `.rtp` file for OPLS methane is found [here](https://gist.github.com/anonymous/a8e862c29a8c50f374f0#file-methane-rtp) with its corresponding `.pdb` file [here](https://gist.githubusercontent.com/wesbarnett/9814526/raw/fed66209a702645b1e0871396f58de6b8b610516/methane-1.pdb). The `.rtp` file must be placed in the force field directory for the force field you are going to use.

[See below](#See_also) for alternative ways to generate or obtain topologies.

#### Box creation

A quick way to create a simulation box full of water around a solute is to do:

```
$ gmx solvate -cp conf.gro -cs *water* -box *X* *Y* *Z* -o conf.gro -p topol.top

```

In the above the solute/protein's coordinates are initially stored in `conf.gro`. A water model using *water*.gro (either found in the top-level force field directory or the current one) is used to fill the box with solvent, and the box dimensions are `*X*`, `*Y*`, and `*Z*`. The topology file, `topol.top` is updated and the new system is output to `conf.gro`.

If `-cs` is omitted, a three-point water model is used. The other available water structures are `tip4p` and `tip5p`.

**Note:** `tip4p` is simply a set of four-point water model coordinates and can correspond to any four-point water model, not just [TIP4P](https://en.wikipedia.org/wiki/Water_model "wikipedia:Water model").

You can also [use different box types](#Create_non-cubic_box_and_fill_with_solvent) and [non-water solvents](#Use_a_non-water_solvent).

#### Adding ions

If the system is not charge-neutral, ions should generally be added. For example if the net charge of your system is -2, to add two positive sodium ions do:

```
$ gmx grompp -f grompp.mdp
$ gmx genion -s topol.tpr -np 2 -pname Na -o conf.gro -p topol.top
```

Then select the index group corresponding with the solvent, which will be replaced by the ions. The `-nname` argument should correspond to an ion in the force field you are using.

**Tip:** The `.mdp` file does not need to correspond to any particular simulation step. It is only used to generate the `.tpr` file for *gmx genion*.

#### Parameter files

A parameters file should be created for each different step of a set of simulations (*e.g.*, minimization, equilibration, production). A list of all possible options is [here](http://manual.gromacs.org/documentation/5.1.1/user-guide/mdp-options.html#mdp-nstcalcenergy).

Here is a sample parameter file for a ten second production run at standard conditions:

```
dt                       = 0.002
nsteps                   = 5000000

nstxout-compressed       = 2500

coulombtype              = PME
rcoulomb                 = 1.0

vdwtype                  = Cut-off
rvdw                     = 1.0
DispCorr                 = EnerPres

tcoupl                   = Nose-Hoover
nh-chain-length          = 1
tc-grps                  = System
tau-t                    = 2.0
ref-t                    = 298.15

pcoupl                   = Parrinello-Rahman 
tau_p                    = 2.0
compressibility          = 4.46e-5
ref_p                    = 1.0 

constraints              = h-bonds
continuation             = yes
```

**Tip:** A commented parameters file with all options (even those not explicitly listed in your file) is output when running *gmx grompp* and saved by default as `mdout.mdp`.

### Running

#### Basics

Simulations typically consist of two parts, described below.

First, there is a preprocessing step where the structure file, topology file, and parameters file are read in and written out to a single `.tpr` file, also sometimes referred to as a topology file:

```
$ gmx grompp -f grompp.mdp -c conf.gro -p topol.top -o topol.tpr

```

Here `grompp.mdp` is the parameters file for this simulation step, `conf.gro` is the structure file that begins this simulation step, and `topol.top` is the topology file. A structure file (`.gro`) is output at the end of every simulation, so it should be used with `-c` in a simulation that continues from the previous one (*e.g.*, an initial equilibration run should use the structure file output from a previous minimization step).

**Note:** When a checkpoint file is available, you should prefer to read in it with the `-t` flag (instead of just a structure file with `-c`), since it contains additional information. When using both the `-c` and `-t` flags *gmx grompp* checks for the checkpoint file first, and if it is not found, then falls back to the structure file indicated. If a structure file is not indicated in this case, the default filename `conf.gro` is used.

Next, there is the actual simulation. The `.tpr` file is read in with the main program *gmx mdrun* to run the simulation:

```
$ gmx mdrun -s topol.tpr

```

**Tip:** *gmx mdrun* outputs several files. To make them have the same prefix use the `-deffnm` flag.

In general these two parts are repeated for an energy minimization step, an equilibration step, and a production step. Multiple equilibration steps may be needed, especially when turning on pressure coupling. The production step and the last equilibration step should use the exact same parameters (`.mdp`) except for the length of the simulation.

As an example, a set of simulations consisting of one minimization step, one equilbration step, and one production step might look like this:

```
#!/bin/bash

gmx grompp -f min.mdp -o min.tpr -c conf.gro -p topol.top
gmx mdrun -deffnm min

gmx grompp -f eql.mdp -o eql.tpr -c min.gro -p topol.top
gmx mdrun -deffnm eql

gmx grompp -f prd.mdp -o prd.tpr -t eql.cpt -p topol.top
gmx mdrun -deffnm prd
```

Here `min.mdp`, `eql.mdp`, and `prd.mdp` are parameter files for the minimization, equilibration, and production steps, respectively.

#### Acceleration & Parallelization

By default GROMACS uses all available processors on a single node. To run across multiple nodes, an MPI library is required. Using openmpi to run GROMACS takes the following form:

```
$ mpirun -np *totalranks* -npernode *rankspernode* --hostfile *filename* gmx mdrun -s topol.tpr

```

Here *totalranks* is the total number of MPI ranks to create, *rankspernode* is the number of MPI ranks per node, and *filename* is the hostfile used to determine on which hosts to run the processes.

OpenMPI be used together with OpenMP as seen here:

```
$ mpirun -np *totalranks* -npernode *rankspernode* --hostfile *filename* gmx mdrun -ntomp *openmpthreads* -s topol.tpr

```

If compiled without an external MPI library one can control MPI ranks and OMP threads, using GROMAC's thread-MPI. This will not be able to be run across multiple compute nodes:

```
$ gmx mdrun -ntmpi *totalranks* -ntomp *openmpthreads* -s topol.tpr

```

Here *openmpthreads* is the number of OpenMP threads to create. *totalranks***openmpthreads* should equal the total number of processors.

**Tip:** Splitting up a simulation between MPI ranks and OMP threads is generally slower than using one or the other.

GROMACS automatically detects any available GPU's if it was compiled with GPU support. The number of MPI ranks must be a multiple of the number of GPU's to be used. Using a GPU requires the *Verlet* cut-off scheme, which is [set](#Parameter_files) with the parameter `cutoff-scheme` in your `.mdp` file. The command takes the basic form:

```
$ mpirun -np *totalranks* -npernode *rankspernode* --hostfile *filename* gmx mdrun -ntomp *openmpthreads* -s topol.tpr -gpu_id *gpuids*

```

Here *gpuids* is the zero-based id of each GPU in a list. That is, with only one GPU (`-np 1`), you would use `-gp_uid 0`. If two GPU's are available (`-np 2`), you would use `-gpu_id 01`. To use a GPU on multiple MPI ranks, simply list it's id the number of times to be used. For example, to use four MPI ranks on two GPUS one would use `-np 4`, and `-gpu_id 0011`, thus using each GPU on two MPI ranks. If running on two twenty-core machines, the command would look like:

```
$ mpirun -np 8 -npernode 4 --hostfile *filename* gmx mdrun -ntomp 5 -s topol.tpr -gpu_id 0011

```

If using GROMACS thread-MPI on one twenty core machine this would be:

```
$ gmx mdrun -ntmpi 4 -ntomp 5 -s topol.tpr -gpu_id 0011

```

**Tip:** Running multiple simulations on a GPU can be more efficient than running them separately. To do so use the `-multi` or `-multidir` flag.

See the man page on `mpirun` as well as the [GROMACS section on MPI acceleration and parallelization for more options](http://www.gromacs.org/Documentation/Acceleration_and_parallelization#MPI).

#### Restart a simulation

To restart a simulation from a checkpoint file do:

```
$ gmx mdrun -s topol.tpr -cpi state.cpt

```

Here `topol.tpr` is the original `.tpr` used in the simulation, and `state.cpt` is the last checkpoint file from that simulation.

#### Extend a simulation

To extend a simulation create a modified `.tpr` file and use it with *gmx mdrun*:

```
$ gmx convert-tpr -s topol.tpr -extend *time* -o tpxout.tpr
$ gmx mdrun -s tpxout.tpr -cpi state.cpt
```

Where *time* is how much longer to run the simulation in picoseconds, `topol.tpr` is the `.tpr` file associated with the original simulation, and `state.cpt` is the latest checkpoint file from that simulation. Instead of using `-extend` one can also use `-until` to specify the absolute ending time in picoseconds.

### Analysis

#### Tools

GROMACS comes with many analysis tools built-in. A list of all possible possible commands can be obtained by typing `gmx help commands` or by opening the man page for *gromacs*.

Some of the more prominent analysis commands are:

*   `gmx bar` — *calculate free energy difference estimates through [Bennett's acceptance ratio](https://en.wikipedia.org/wiki/Bennett_acceptance_ratio "wikipedia:Bennett acceptance ratio").*
*   `gmx energy` — *writes energies to xvg files and display averages.*
*   `gmx rdf` — *calculate [radial distribution functions](https://en.wikipedia.org/wiki/Radial_distribution_function "wikipedia:Radial distribution function")*.
*   `gmx trjconv` — *convert and manipulates trajectory files.*
*   `gmx wham` — *Perform weighted histogram analysis after [umbrella sampling](https://en.wikipedia.org/wiki/Umbrella_sampling "wikipedia:Umbrella sampling").*

[See below](#See_also) for other available tools.

#### Index Files

Index files are optionally used in almost all GROMACS analysis programs. The program *gmx make_ndx* controls the creation and modification of index files. Index files consist of group names and integer indices indicating the location of atomic sites in a trajectory frame. They are only required if the available residues found in a structure file do not group atomic sites together in the desired way. When running *gmx make_ndx* the user is presented with a prompt in order to select, combine, and split groups of atoms through various commands. Typing `h` at the make_ndx prompt gives a full description of the commands available.

## Development

GROMACS uses [git](/index.php/Git "Git") for version control, so familiarize yourself with its usage, especially the topic on [collaboration](/index.php/Git#Collaboration "Git"). To begin contributing you need to [sign up for a Gerrit account](https://gerrit.gromacs.org) and add an ssh key. Then clone `ssh://*user*@gerrit.gromacs.org/gromacs.git` where *user* is your user name. After cloning the repository, install the commit hook:

```
$ scp -p *user*@gerrit.gromacs.org:hooks/commit-msg .git/hooks/

```

When making commits, follow [the GROMACS guidelines on commit messages.](http://www.gromacs.org/Developer_Zone/Git/Basic_Git_Usage#Making_a_well-behaved_commit_message) Follow the [coding standard](http://www.gromacs.org/Developer_Zone/Programming_Guide) as you make changes.

When you are ready to share your changes, ensure your HEAD is up to date. Then push with the branch set as `HEAD:refs/for/*mybranch*`, where *mybranch* is the name of the actual branch. In general three branches are used:

*   *master* is used for long-term development of major features which may require large changes in code.
*   *release-*x*-*y is for features that do not require as much code change, where *x* and *y* are the major and minor version numbers of the next release respectively.
*   *release-*x*-*y*-patches* is for bug fixes and small documentation changes to a previous release.

Other branches can be seen on the Gerrit site.

If you want to push a draft commit, push with the branch set as `HEAD:refs/drafts/*mybranch*`. In this case you must explicitly invite others to review your code.

For more information see [the GROMACS page on Gerrit](http://www.gromacs.org/Developer_Zone/Git/Gerrit).

## Tips and tricks

### Create non-cubic box and fill with solvent

To create a non-cubic box filled with solvent, first do:

```
$ gmx editconf -f *protein*.pdb -bt *boxtype* -d *dist* -o box.gro

```

The above command creates a `*boxtype*` box around the molecule in `*protein*.pdb` at `*dist*` nm in every direction. The box is saved as `box.gro`. `*boxtype*` can be `triclinic`, `cubic`, `dodecahedron`, or `octahedron`.

Then fill with solvent:

```
$ gmx solvate -cs tip4p -cp box.gro -o conf.gro -p topol.top

```

### Use multiple solutes

If you want to use multiple solutes randomly inserted, first do:

```
$ gmx insert-molecules -box *X* *Y* *Z* -ci solute.pdb -nmol *N* -o box.gro

```

Where *X*, *Y*, and *Z* are the box dimensions in nanometers, and *N* is the number to insert. You will need to update your topology file with the inserted number of molecules.

Then fill with solvent:

```
$ gmx solvate -cs tip4p -cp box.gro -o conf.gro -p topol.top

```

**Note:** When using a visualization program you will see a triclinic box, since all non-cubic boxes are ultimately represented in GROMACS as a triclinic box.

### Use a non-water solvent

To use a non-water solvent with standard tools such as *gmx pdb2gmx* and *gmx solvate* do the following:

1.  Create one solvent molecule's structure file and topology.
2.  Create a box containing a couple hundred of the solvent molecules (216 seems to be a standard) and run a short equilibration on the system at standard conditions.
3.  Copy the output structure file `.gro` from the simulation to `*solvent*.gro`, where *solvent* is the name you wish to use for this molecule. Place this copy in the top level force field directory (where each force field has its own directory).
4.  Modify the topology file for the single solvent by removing everything but the `[moleculetype]` section and name the molecule in the file as `SOL`.
5.  Rename the topology file as `*solvent*.itp` and move it to the force field directory to which it applies.
6.  Update `watermodels.dat` for the force field you wish to use with this solvent (located in the force field's directory), adding the solvent. You will simply add a line with `*filename* *shortdescription* *longdescription*` where *filename* omits the file extension.

Now when you run *gmx pdb2gmx* this solvent model should be available for the applicable force field. Additionally you can use `-cs *solvent*` when running *gmx solvate*.

## See also

### Structure and Topology Databases

*   [Automated Topology Builder & Repository](http://compbio.biosci.uq.edu.au/atb/) — *repository for building blocks and interaction parameter files for molecules* as well as *an automated builder to help generate building blocks for novel molecules.*
*   [RCSB Protein Data Bank](http://www.rcsb.org/pdb/home/home.do) — *information about the 3D shapes of proteins, nucleic acids, and complex assemblies that helps students and researchers understand all aspects of biomedicine and agriculture, from protein synthesis to health and disease.*
*   [SwissParam](http://swissparam.ch/) — *provides topology and parameters for small organic molecules compatible with the CHARMM all atoms force field, for use with CHARMM and GROMACS.*
*   [TraPPE Parameter Database](http://www.chem.umn.edu/groups/siepmann/trappe/index.html) — search by molecule name, or build your own, in order to obtain TraPPE force field parameters. Note that it is necessary to convert the parameters to the correct units.
*   [Virtual Chemistry](http://www.virtualchemistry.org/index.php) — comparison of experimental and computational results for thousands of molecules. Contains validated topology input files for CGenFF, GAFF and OPLS/AA.

### Development

*   [GROMACS Redmine](http://redmine.gromacs.org/projects/gromacs) — project management page, where bugs, issues, and features are reported and tracked.
*   [GROMACS Gerrit](https://gerrit.gromacs.org) — the project's code review system.

### Documentation

*   [GROMACS Mailing List](https://mailman-1.sys.kth.se/mailman/listinfo/gromacs.org_gmx-users) — very active mailing list for users seeking help. Make sure to read the manual and search the archive before posting.
*   [GROMACS Manual](http://www.gromacs.org/Documentation/Manual) — official GROMACS manual.
*   [GROMACS Online Reference](http://manual.gromacs.org/)

### External libraries & programs

#### Analysis libraries

*   **libgmxcpp** — a C++ toolkit used for reading in Gromacs files (.xtc and .ndx) for use in analyzing simulation results.

	[https://github.com/wesbarnett/libgmxcpp](https://github.com/wesbarnett/libgmxcpp) || [libgmxcpp](https://aur.archlinux.org/packages/libgmxcpp/)

*   **libgmxfort** — a Modern Fortran toolkit used for reading in Gromacs files (.xtc and .ndx) for use in analyzing simulation results.

	[https://github.com/wesbarnett/libgmxcpp](https://github.com/wesbarnett/libgmxcpp) || [libgmxfort](https://aur.archlinux.org/packages/libgmxfort/)

*   **mdanalysis** — an object-oriented python toolkit to analyze molecular dynamics trajectories in many popular formats.

	[http://www.mdanalysis.org](http://www.mdanalysis.org) || [python2-mdanalysis](https://aur.archlinux.org/packages/python2-mdanalysis/)

*   **MDTraj** — a modern, open library for the analysis of molecular dynamics trajectories.

	[http://mdtraj.org/latest/](http://mdtraj.org/latest/) || [python-mdtraj](https://aur.archlinux.org/packages/python-mdtraj/)

*   **xdrfile** — allows to read GROMACS trr and xtc files and also to convert from one format to another.

	[http://gromacs.org](http://gromacs.org) || [xdrfile](https://aur.archlinux.org/packages/xdrfile/)

#### Free energy calculations

*   **alchemical_analysis** — an open tool implementing some recommended practices for analyzing alchemical free energy calculations.

	[https://github.com/MobleyLab/alchemical-analysis](https://github.com/MobleyLab/alchemical-analysis) || [python2-alchemical-analysis](https://aur.archlinux.org/packages/python2-alchemical-analysis/)

#### Structure creation

*   **[Avogadro](https://en.wikipedia.org/wiki/Avogadro_(software) "wikipedia:Avogadro (software)")** — an advanced molecule editor and visualizer designed for cross-platform use in computational chemistry, molecular modeling, bioinformatics, materials science, and related areas.

	[http://avogadro.cc](http://avogadro.cc) || [avogadro](https://aur.archlinux.org/packages/avogadro/)

#### Topology generation

*   **acpype** — a tool based on Python to use Antechamber to generate topologies for chemical compounds and to interface with other python applications like CCPN tools or ARIA...Topologies files to be generated so far: CNS/XPLOR, GROMACS, CHARMM and AMBER.

	[https://code.google.com/p/acpype](https://code.google.com/p/acpype) || <small>not packaged? [search in AUR](https://aur.archlinux.org/packages/)</small>

#### Visualization

*   **vmd** — molecular visualization program for displaying, animating, and analyzing large biomolecular systems using 3-D graphics and built-in scripting.

	[http://www.ks.uiuc.edu/Research/vmd/](http://www.ks.uiuc.edu/Research/vmd/) || [vmd](https://aur.archlinux.org/packages/vmd/)

#### Wrappers

*   **GromacsWrapper** — a python package that wraps system calls to Gromacs tools into thin classes.

	[http://becksteinlab.github.io/GromacsWrapper](http://becksteinlab.github.io/GromacsWrapper) || <small>not packaged? [search in AUR](https://aur.archlinux.org/packages/)</small>

### Tutorials

*   [GROMACS Tutorials](http://www.gromacs.org/Documentation/Tutorials)
*   [Justin Lemkul's Tutorials](http://www.bevanlab.biochem.vt.edu/Pages/Personal/justin/gmx-tutorials/index.html) — includes a variety of different simulation methods (umbrella sampling, free energy calculations, etc).
*   [James Barnett's Tutorials](http://wbarnett.us/tutorials/) — a few basic tutorials on simulations with an organic solute. Includes how to use *gmx pdb2gmx* with a user-created molecule.