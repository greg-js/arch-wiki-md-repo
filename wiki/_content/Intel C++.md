# Intel C++

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

Related articles

*   [ABS](/index.php/ABS "ABS")
*   [Creating packages](/index.php/Creating_packages "Creating packages")
*   [Makepkg](/index.php/Makepkg "Makepkg")

Installation and basic usage of Intel® C++ Composer XE (formerly Intel® C++ Compiler Professional Edition) for Linux on Arch.

## Contents

*   [1 Before you begin](#Before_you_begin)
*   [2 Setup and installation](#Setup_and_installation)
*   [3 Using icc with makepkg](#Using_icc_with_makepkg)
    *   [3.1 Method 1 (12/08/2012)](#Method_1_.2812.2F08.2F2012.29)
*   [4 icc CFLAGS](#icc_CFLAGS)
    *   [4.1 -xX](#-xX)
    *   [4.2 -Ox](#-Ox)
    *   [4.3 -w](#-w)
*   [5 Software compiled with Intel C / C++](#Software_compiled_with_Intel_C_.2F_C.2B.2B)

## Before you begin

**Note:** Packages that have been compiled by icc will depend on the associated libs contained in the **intel-openmp** package in order to run. Since **intel-openmp** depends on **intel-compiler-base**, users MUST have both packages installed at all times!

## Setup and installation

[intel-parallel-studio-xe](https://aur.archlinux.org/packages/intel-parallel-studio-xe/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/intel-parallel-studio-xe)]</sup> are available in the [AUR](/index.php/AUR "AUR"). To build the package, one needs a license file which is free for personal and for non-commercial use. The requisite license file is emailed to users upon [[registration](https://registrationcenter.intel.com/RegCenter/AutoGen.aspx?ProductID=1517&AccountID=&EmailID=&ProgramID=&RequestDt=&rm=NCOM&lang=)] and should be copied into the $startdir prior to running makepkg. The current PKGBUILD assembles 7 or 8 packages:

*   **intel-compiler-base** - Intel C/C++ compiler and base libs
*   **intel-fortran-compiler** - Intel fortran compiler and base libs (only Parallel Studio XE)
*   **intel-openmp** - Intel OpenMP Library
*   intel-idb- Intel C/C++ debugger
*   intel-ipp - Intel Integrated Performance Primitives
*   intel-mkl - Intel Math Kernel Library (Intel® MKL)
*   intel-sourcechecker - Intel Source Checker
*   intel-tbb - Intel Threading Building Blocks (TBB)

**Note:** A minimal working environment requires the **intel-compiler-base** and **intel-openmp** packages; if you want also the fortran compiler you must install **intel-fortran-compiler**.

## Using icc with makepkg

**Note:** Not every package will successfully compile with icc without heavy modifications to the underlying source.

There is currently no official guide to using icc with makepkg. This section is meant to capture various methods suggested by users. Please make a new sub-section with your suggested method titled as such.

### Method 1 (12/08/2012)

Modify `/etc/makepkg.conf` inserting the following code _under_ the existing line defining **CXXFLAGS** to enable makepkg to use icc. No special switches are needed when calling makepkg to build.

```
_CC=icc
if [ $_CC = "icc" ]; then
export CC="icc"
export CXX="icpc"
export CFLAGS="-march=native -O3 -no-prec-div -fno-alias -pipe"
export CXXFLAGS="${CFLAGS}"
export LDFLAGS="-Wl,-O1,--sort-common,--as-needed"
export AR="xiar"
export LD="xild"
fi
```

**Note:**

*   To toggle between the native gcc and icc, simple comment or uncomment the newly created **_CC** variable.
*   In some case the compilation method described above fails and the compilation will be performed with _gcc_, so you should test if yours application has been effectively compiled with _icc_.

To test if your package has been really compiled with icc:

*   Type the command **ldd [your_app] | grep intel** If the application is linked to a shared object located in the directory **/opt/intel/lib/** it is mind that has been complied with icc.

*   Another method is to observe the build output and watch if it is using the _icc_ or _icpc_ command.

*   The last method is to watch if the warnings are in _icc_ style or not.

## icc CFLAGS

In general, icc supports many of the same CFLAGS gcc supports and is also pretty tolerant to gcc flags it cannot use. In most cases it will happily ignore the flag warning the user and moving on. For an exhaustive list and explanation of available compiler flags, consult the icc manpage or better yet by invoking the compiler with the help flag:

```
icc --help

```

### -xX

Use to generate specialized code to run exclusively on processors supporting it. If unsure which option to use, simply inspect the **flags** section of `/proc/cpuinfo`. In the example below, **SSE4.1** would be the correct selection:

 `$ grep -m 1 flags /proc/cpuinfo` 

```
flags: fpu vme de pse tsc msr pae mce cx8 apic sep mtrr pge mca cmov pat pse36 clflush 
dts acpi mmx fxsr sse sse2 ss ht tm pbe syscall nx lm constant_tsc arch_perfmon pebs 
bts rep_good nopl aperfmperf pni dtes64 monitor ds_cpl vmx smx est tm2 ssse3 cx16 xtpr
pdcm sse4_1 lahf_lm dts tpr_shadow vnmi flexpriority

```

*   -xHost
*   -xSSE2
*   -xSSE3
*   -xSSSE3
*   -xSSE4.1
*   -xSSE4.2
*   -xAVX
*   -xCORE-AVX-I
*   -xSSSE3_ATOM

**Tip:** Use the **-xHost** flag if unsure what your specific processor supports.

### -Ox

Same behavior as gcc. x is one of the following options:

*   0 - disables optimizations
*   1 - optimize for maximum speed, but disable some optimizations which increase code size for a small speed benefit
*   2 - optimize for maximum speed (DEFAULT)
*   3 - optimize for maximum speed and enable more aggressive optimizations that may not improve performance on some programs (recommended for math intensive looping programs)

### -w

Similar to the gcc:

*   -w - disable all warnings (recommended for the package compilation)
*   -Wbrief - print brief one-line diagnostics
*   -Wall - enable all warnings
*   -Werror - force warnings to be reported as errors

## Software compiled with Intel C / C++

In the following table we report a list of packages from the officials repository that we have tried to compile with the intel C/C++ compiler. The compilation should be done by using the PKGBUILD from ABS.

<table class="wikitable sortable collapsible" border="1">

<tbody>

<tr style="background: #ffdead;">

<th>Application</th>

<th>Compile</th>

<th>Comments</th>

</tr>

<tr>

<td>**xvidcore**</td>

<td style="background: Lime">OK</td>

<td>Works with the [Method 1](#Method_1)</td>

</tr>

<tr>

<td>**kdebase**</td>

<td style="background: Lime">OK</td>

<td>Works with the [Method 1](#Method_1)</td>

</tr>

<tr>

<td>**conky 1.9.0**</td>

<td style="background: Lime">OK</td>

<td>Works with the [Method 1](#Method_1)</td>

</tr>

<tr>

<td>**nginx 1.4.2**</td>

<td style="background: Lime">OK</td>

<td>Works with the [Method 1](#Method_1)</td>

</tr>

<tr>

<td>**gzip 1.6**</td>

<td style="background: Lime">OK</td>

<td>Works with the [Method 1](#Method_1)</td>

</tr>

<tr>

<td>**xz**</td>

<td style="background: Lime">OK</td>

<td>Works with the [Method 1](#Method_1)</td>

</tr>

<tr>

<td>**lz4**</td>

<td style="background: GreenYellow">OK</td>

<td>We must edit the PKGBUILD.</td>

</tr>

<tr>

<td>**minetest**</td>

<td style="background: Lime">OK</td>

<td>Works with the [Method 1](#Method_1)</td>

</tr>

<tr>

<td>**opus**</td>

<td style="background: Lime">OK</td>

<td>Works with the [Method 1](#Method_1)</td>

</tr>

<tr>

<td>**zlib 1.2.8**</td>

<td style="background: yellow">Not recommended</td>

<td>Works with the [Method 1](#Method_1), but caused bugs in some apps, like tightvnc</td>

</tr>

<tr>

<td>**Gimp 2.8 / 2.9**</td>

<td style="background: Lime">OK</td>

<td>Works with the [Method 1](#Method_1)</td>

</tr>

<tr>

<td>**Pacman 4.0.3**</td>

<td style="background: Lime">OK</td>

<td>Works with the [Method 1](#Method_1)</td>

</tr>

<tr>

<td>**x264**</td>

<td style="background: Lime">OK</td>

<td>Works with the [Method 1](#Method_1)</td>

</tr>

<tr>

<td>**MySql**</td>

<td style="background: Lime">OK</td>

<td>Works with the [Method 1](#Method_1)</td>

</tr>

<tr>

<td>**SqlLite**</td>

<td style="background: Lime">OK</td>

<td>Works with the [Method 1](#Method_1)</td>

</tr>

<tr>

<td>**lame**</td>

<td style="background: Lime">OK</td>

<td>Works with the [Method 1](#Method_1)</td>

</tr>

<tr>

<td>**xaos**</td>

<td style="background: Lime">OK</td>

<td>Works with the [Method 1](#Method_1)</td>

</tr>

<tr>

<td>**gegl**</td>

<td style="background: Lime">OK</td>

<td>Works with the [Method 1](#Method_1)</td>

</tr>

<tr>

<td>**VLC**</td>

<td style="background: Tomato">Unsuccessful</td>

<td>There is some problem with the compiler flags</td>

</tr>

<tr>

<td>**bzip2**</td>

<td style="background: Tomato">Unsuccessful</td>

<td>There is some problem with the compiler flags</td>

</tr>

<tr>

<td>**mplayer**</td>

<td style="background: pink">Out of date</td>

<td>It do not recognize the Intel compiler</td>

</tr>

<tr>

<td>**optipng**</td>

<td style="background: GreenYellow">OK</td>

<td>Works with the [Method 1](#Method_1). Comment out LD=xild in makepkg.conf</td>

</tr>

<tr>

<td>**python-numpy**</td>

<td style="background: GreenYellow">OK</td>

<td>We must edit the PKGBUILD. [python-numpy-mkl](https://aur.archlinux.org/packages/python-numpy-mkl/)<sup><small>AUR</small></sup></td>

</tr>

<tr>

<td>**python-scipy**</td>

<td style="background: GreenYellow">OK</td>

<td>We must edit the PKGBUILD. [python-scipy-mkl](https://aur.archlinux.org/packages/python-scipy-mkl/)<sup><small>AUR</small></sup></td>

</tr>

<tr>

<td>**Qt**</td>

<td style="background: GreenYellow">OK</td>

<td>We must add the option _-platform linux-icc-64 (or 32)_ in the configure command</td>

</tr>

<tr>

<td>**systemd**</td>

<td style="background: red">Fail</td>

<td>undefined reference to `server_dispatch_message'</td>

</tr>

</tbody>

</table>

**Legend:**

<table>

<tbody>

<tr>

<td style="background: Lime">OK</td>

<td>The compilation with ICC works!</td>

</tr>

<tr>

<td style="background: GreenYellow">OK</td>

<td>The compilation works but is needed an editing of the PKGBUILD</td>

</tr>

<tr>

<td style="background: Tomato">Unsuccessful</td>

<td>The compilation may work, but there are some compilations errors.</td>

</tr>

<tr>

<td style="background: yellow">Not recommended</td>

<td>The compilation works, but is not recommended</td>

</tr>

<tr>

<td style="background: red">Fail</td>

<td>It is impossible to compile the PKG with ICC.</td>

</tr>

<tr>

<td style="background: pink">Out of date</td>

<td>It is unsuccessful or fails with older CFLAGS. You can try compiling it with new [Method 1](#Method_1).(Do not forget to paste your result here!)</td>

</tr>

</tbody>

</table>

Retrieved from "[https://wiki.archlinux.org/index.php?title=Intel_C%2B%2B&oldid=392271](https://wiki.archlinux.org/index.php?title=Intel_C%2B%2B&oldid=392271)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [Development](/index.php/Category:Development "Category:Development")

Hidden category:

*   [Pages with broken package links](/index.php/Category:Pages_with_broken_package_links "Category:Pages with broken package links")