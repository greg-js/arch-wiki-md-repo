# GPGPU

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

Related articles

*   [Catalyst](/index.php/Catalyst "Catalyst")
*   [Nvidia](/index.php/Nvidia "Nvidia")

GPGPU stands for [General-purpose computing on graphics processing units](https://en.wikipedia.org/wiki/GPGPU "wikipedia:GPGPU"). In Linux, there are currently two major GPGPU frameworks: [OpenCL](https://en.wikipedia.org/wiki/OpenCL "wikipedia:OpenCL") and [CUDA](https://en.wikipedia.org/wiki/CUDA "wikipedia:CUDA")

## Contents

*   [1 OpenCL](#OpenCL)
    *   [1.1 OpenCL ICD loader (libOpenCL.so)](#OpenCL_ICD_loader_.28libOpenCL.so.29)
    *   [1.2 Implementations](#Implementations)
        *   [1.2.1 AMD](#AMD)
        *   [1.2.2 Mesa (Gallium)](#Mesa_.28Gallium.29)
        *   [1.2.3 Nvidia](#Nvidia)
        *   [1.2.4 Intel](#Intel)
        *   [1.2.5 POCL](#POCL)
    *   [1.3 Development](#Development)
        *   [1.3.1 Language bindings](#Language_bindings)
*   [2 CUDA](#CUDA)
    *   [2.1 Development](#Development_2)
    *   [2.2 Language bindings](#Language_bindings_2)
    *   [2.3 Driver issues](#Driver_issues)
*   [3 List of OpenCL and CUDA accelerated software](#List_of_OpenCL_and_CUDA_accelerated_software)
*   [4 Links and references](#Links_and_references)

## OpenCL

OpenCL (Open Computing Language) is an open, royalty-free parallel programming specification developed by the Khronos Group, a non-profit consortium.

The OpenCL specification describes a programming language, a general environment that is required to be present, and a C API to enable programmers to call into this environment.

Arch Linux provides multiple packages for all of these.

To **execute** programs that use OpenCL, you need to install a runtime compatible with your hardware:

*   [opencl-nvidia](https://www.archlinux.org/packages/?name=opencl-nvidia): execute on your Nvidia GPU (official Nvidia runtime)
*   [opencl-mesa](https://www.archlinux.org/packages/?name=opencl-mesa): execute on AMD GPU's using the mesa drivers (currently under development, your mileage may vary)
*   [opencl-catalyst](https://aur.archlinux.org/packages/opencl-catalyst/)<sup><small>AUR</small></sup>: execute on your AMD GPU (official AMD runtime)
*   [intel-opencl-runtime](https://aur.archlinux.org/packages/intel-opencl-runtime/)<sup><small>AUR</small></sup>: execute on your CPU (official Intel runtime, also supports non-Intel CPUs)
*   [pocl](https://aur.archlinux.org/packages/pocl/)<sup><small>AUR</small></sup>: execute on your CPU (LLVM-based OpenCL implementation)

For OpenCL **development**, the bare minimum additional packages required, are:

*   [ocl-icd](https://www.archlinux.org/packages/?name=ocl-icd): OpenCL ICD loader implementation, up to date with the latest OpenCL specification.
*   [opencl-headers](https://www.archlinux.org/packages/?name=opencl-headers): OpenCL C/C++ API headers.

The vendors' SDKs provide a multitude of tools and support libraries:

*   [intel-opencl-sdk](https://aur.archlinux.org/packages/intel-opencl-sdk/)<sup><small>AUR</small></sup>: Intel's OpenCL SDK (old version, new OpenCL SDKs are included in the INDE and Intel Media Server Studio)
*   [amdapp-sdk](https://aur.archlinux.org/packages/amdapp-sdk/)<sup><small>AUR</small></sup>: AMD's OpenCL SDK
*   [cuda](https://www.archlinux.org/packages/?name=cuda): Nvidia's GPU SDK which includes support for OpenCL 1.1.

### OpenCL ICD loader (libOpenCL.so)

The OpenCL ICD loader is supposed to be a platform-agnostic library that provides the means to load device-specific drivers through the OpenCL API. Most OpenCL vendors provide their own implementation of an OpenCL ICD loader, and these should all work with the other vendors' OpenCL implementations. Unfortunately, most vendors do not provide completely up-to-date ICD loaders, and therefore Arch Linux has decided to provide this library from a separate project ([ocl-icd](https://www.archlinux.org/packages/?name=ocl-icd)) which currently provides a functioning implementation of the current OpenCL API.

The other ICD loader libraries are installed as part of each vendor's SDK. If you want to ensure the ICD loader from the [ocl-icd](https://www.archlinux.org/packages/?name=ocl-icd) package is used, you can create a file in `/etc/ld.so.conf.d` which adds `/usr/lib` to the dynamic program loader's search directories:

 `/etc/ld.so.conf.d/00-usrlib.conf`  `/usr/lib` 

This is necessary because all the SDKs add their runtime's lib directories to the search path through `ld.so.conf.d` files.

The available packages containing various OpenCL ICDs are:

*   [ocl-icd](https://www.archlinux.org/packages/?name=ocl-icd): recommended, most up-to-date
*   [libopencl](https://aur.archlinux.org/packages/libopencl/)<sup><small>AUR</small></sup> by AMD. Provides version 2.0 of OpenCL. It is currently distributed by AMD under a restrictive license and therefore could not have been pushed into official repo.
*   [intel-opencl-runtime](https://aur.archlinux.org/packages/intel-opencl-runtime/)<sup><small>AUR</small></sup>: Intel's libCL, provides OpenCL 1.2.

**Note:** ICD Loader's vendor is mentioned only to identify each loader, it is otherwise completely irrelevant. ICD loaders are vendor-agnostic and may be used interchangeably. (as long as they are implemented correctly)

### Implementations

To see which OpenCL implementations are currently active on your system, use the following command:

```
$ ls /etc/OpenCL/vendors

```

#### AMD

OpenCL implementation from AMD is known as [AMD APP SDK](http://developer.amd.com/sdks/AMDAPPSDK/Pages/default.aspx), formerly also known as AMD Stream SDK or ATi Stream.

It can be installed with the [amdapp-sdk](https://aur.archlinux.org/packages/amdapp-sdk/)<sup><small>AUR</small></sup> package. This package is installed as `/opt/AMDAPP` and apart from SDK files it also contains a number of code samples (`/opt/AMDAPP/SDK/samples/`). It also provides the `clinfo` utility which lists OpenCL platforms and devices present in the system and displays detailed information about them.

As AMD APP SDK itself contains CPU OpenCL driver, no extra driver is needed to use execute OpenCL on CPU devices (regardless of its vendor). GPU OpenCL drivers are provided by the [catalyst](https://aur.archlinux.org/packages/catalyst/)<sup><small>AUR</small></sup> package (an optional dependency).

Code is compiled using [llvm](https://www.archlinux.org/packages/?name=llvm) (dependency).

#### Mesa (Gallium)

[![Tango-dialog-warning.png](/images/d/d8/Tango-dialog-warning.png)](/index.php/File:Tango-dialog-warning.png)

[![Tango-dialog-warning.png](/images/d/d8/Tango-dialog-warning.png)](/index.php/File:Tango-dialog-warning.png)

**This article or section is out of date.**

**Reason:** How accurate is this part? (Discuss in [Talk:GPGPU#](https://wiki.archlinux.org/index.php/Talk:GPGPU))

OpenCL support from Mesa is in development (see [http://www.x.org/wiki/GalliumStatus/](http://www.x.org/wiki/GalliumStatus/)). AMD Radeon cards are supported by the r600g driver.

Arch Linux ships OpenCL support as a separate package [opencl-mesa](https://www.archlinux.org/packages/extra/x86_64/opencl-mesa/). See [http://dri.freedesktop.org/wiki/GalliumCompute/](http://dri.freedesktop.org/wiki/GalliumCompute/) for usage instructions.

You could also use [lordheavy's repo](http://pkgbuild.com/~lcarlier/mesa-git/). Install these packages:

*   ati-dri-git
*   opencl-mesa-git
*   libclc-git

Surprisingly, pyrit performs 20% better with radeon+r600g compared to Catalyst 13.11 Beta1 (tested with 7 other CPU cores):

```
catalyst     #1: 'OpenCL-Device 'Barts'': 21840.7 PMKs/s (RTT 2.8)
radeon+r600g #1: 'OpenCL-Device 'AMD BARTS'': 26608.1 PMKs/s (RTT 3.0)
```

At the time of this writing (30 October 2013), one must apply patches [[1]](http://people.freedesktop.org/~tstellar/pyrit-perf/0001-XXX-clover-Calculate-the-optimal-work-group-size.patch) and [[2]](http://people.freedesktop.org/~tstellar/pyrit-perf/0001-radeon-llvm-Specify-the-DataLayout-when-running-opti.patch) on top of Mesa commit ac81b6f2be8779022e8641984b09118b57263128 to get this performance improvement. The latest unpatched LLVM trunk was used (SVN rev 193660).

#### Nvidia

The Nvidia implementation is available as [opencl-nvidia](https://www.archlinux.org/packages/?name=opencl-nvidia) from the [official repositories](/index.php/Official_repositories "Official repositories"). It only supports Nvidia GPUs running the [nvidia](https://www.archlinux.org/packages/?name=nvidia) kernel module (nouveau does not support OpenCL yet).

#### Intel

The Intel implementation, named simply [Intel OpenCL SDK](http://software.intel.com/en-us/articles/opencl-sdk/), provides optimized OpenCL performance on Intel CPUs (mainly Core and Xeon) and CPUs only. Install it with the [intel-opencl-sdk](https://aur.archlinux.org/packages/intel-opencl-sdk/)<sup><small>AUR</small></sup> package. The runtime can be installed with the separate [intel-opencl-runtime](https://aur.archlinux.org/packages/intel-opencl-runtime/)<sup><small>AUR</small></sup> package. OpenCL for integrated graphics hardware is available through the [beignet](https://aur.archlinux.org/packages/beignet/)<sup><small>AUR</small></sup> package for Ivy Bridge and newer hardware.

#### POCL

CPU-only LLVM-based implementation. Available as [pocl](https://aur.archlinux.org/packages/pocl/)<sup><small>AUR</small></sup>.

### Development

The required packages for OpenCL development are listed in the overview. Installation of a full SDK is optional (depending on the runtime implementation, which is often only available as part of a vendor's SDK). Link your application to `libOpenCL.so`.

#### Language bindings

*   **JavaScript/HTML5**: [WebCL](http://www.khronos.org/webcl/)
*   **[Python](/index.php/Python "Python")**: [python-pyopencl](https://www.archlinux.org/packages/?name=python-pyopencl)
*   **[D](/index.php/D "D")**: [cl4d](https://bitbucket.org/trass3r/cl4d/wiki/Home)
*   **[Haskell](/index.php/Haskell "Haskell")**: OpenCLRaw: [haskell-openclraw-git](https://aur.archlinux.org/packages/haskell-openclraw-git/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/haskell-openclraw-git)]</sup>
*   **[Java](/index.php/Java "Java")**: [JOCL](http://jogamp.org/jocl/www/) (a part of [JogAmp](http://jogamp.org/))
*   **[Mono/.NET](/index.php/Mono "Mono")**: [Open Toolkit](http://sourceforge.net/projects/opentk/)
*   **[Go](/index.php/Go "Go")**: [OpenCL bindings for Go](https://github.com/samuel/go-opencl)
*   **Racket**: Racket has a native interface [on PLaneT](http://planet.racket-lang.org/display.ss?owner=jaymccarthy&package=opencl.plt) that can be installed via raco.

## CUDA

CUDA (Compute Unified Device Architecture) is [NVIDIA](/index.php/NVIDIA "NVIDIA")'s proprietary, closed-source parallel computing architecture and framework. It requires a Nvidia GPU. It consists of several components:

*   required:
    *   proprietary Nvidia kernel module
    *   CUDA "driver" and "runtime" libraries
*   optional:
    *   additional libraries: CUBLAS, CUFFT, CUSPARSE, etc.
    *   CUDA toolkit, including the `nvcc` compiler
    *   CUDA SDK, which contains many code samples and examples of CUDA and OpenCL programs

The kernel module and CUDA "driver" library are shipped in [nvidia](https://www.archlinux.org/packages/?name=nvidia) and [opencl-nvidia](https://www.archlinux.org/packages/?name=opencl-nvidia). The "runtime" library and the rest of the CUDA toolkit are available in [cuda](https://www.archlinux.org/packages/?name=cuda). The library is available [only in 64-bit version](https://projects.archlinux.org/svntogit/community.git/commit/trunk?h=packages/cuda&id=1b62c8bcb9194b2de1b750bd62a8dce1e7e549f5).

### Development

The [cuda](https://www.archlinux.org/packages/?name=cuda) package installs all components in the directory `/opt/cuda`. For compiling CUDA code, add `/opt/cuda/include` to your include path in the compiler instructions. For example this can be accomplished by adding `-I/opt/cuda/include` to the compiler flags/options. To use `nvcc`, a `gcc` wrapper provided by NVIDIA, just add `/opt/cuda/bin` to your path.

To find whether the installation was successful and if cuda is up and running, you can compile the samples installed on `/opt/cuda/sample` (you can simply run `make` inside the directory, altough is a good practice to copy the `/opt/cuda/samples` directory to your home directory before compiling) and running the compiled examples. A nice way to check the installation is to run one of the examples, called `deviceQuery`.

### Language bindings

*   **Fortran**: [PGI CUDA Fortran Compiler](http://www.pgroup.com/resources/cudafortran.htm)
*   **[Haskell](/index.php/Haskell "Haskell")**: The [accelerate package](http://hackage.haskell.org/package/accelerate) lists available CUDA backends
*   **[Java](/index.php/Java "Java")**: [JCuda](http://www.jcuda.org/jcuda/JCuda.html)
*   **[Mathematica](/index.php/Mathematica "Mathematica")**: [CUDAlink](http://reference.wolfram.com/mathematica/CUDALink/tutorial/Overview.html)
*   **[Mono/.NET](/index.php/Mono "Mono")**: [CUDA.NET](http://www.hoopoe-cloud.com/Solutions/CUDA.NET/Default.aspx), [CUDAfy.NET](http://www.hybriddsp.com/)
*   **Perl**: [Kappa](http://psilambda.com/download/kappa-for-perl), [CUDA-Minimal](https://github.com/run4flat/perl-CUDA-Minimal)
*   **[Python](/index.php/Python "Python")**: [python-pycuda](https://www.archlinux.org/packages/?name=python-pycuda) or [Kappa](http://psilambda.com/download/kappa-for-python)
*   **[Ruby](/index.php/Ruby "Ruby")**, **Lua**: [Kappa](http://psilambda.com/products/kappa/)

### Driver issues

It might be necessary to use the legacy driver [nvidia-304xx](https://www.archlinux.org/packages/?name=nvidia-304xx) or [nvidia-304xx-lts](https://www.archlinux.org/packages/?name=nvidia-304xx-lts) to resolve permissions issues when running CUDA programs on systems with multiple GPUs.

## List of OpenCL and CUDA accelerated software

[![Tango-view-fullscreen.png](/images/3/38/Tango-view-fullscreen.png)](/index.php/File:Tango-view-fullscreen.png)

[![Tango-view-fullscreen.png](/images/3/38/Tango-view-fullscreen.png)](/index.php/File:Tango-view-fullscreen.png)

**This article or section needs expansion.**

**Reason:** please use the first argument of the template to provide a brief explanation. (Discuss in [Talk:GPGPU#](https://wiki.archlinux.org/index.php/Talk:GPGPU))

*   [Bitcoin](/index.php/Bitcoin "Bitcoin")
*   [GIMP](/index.php/GIMP "GIMP") (experimental - see [[3]](http://www.h-online.com/open/news/item/GIMP-2-8-RC-1-arrives-with-GPU-acceleration-1518417.html))
*   [pyrit](https://www.archlinux.org/packages/?name=pyrit)
*   [aircrack-ng](https://www.archlinux.org/packages/?name=aircrack-ng)
*   [john-opencl](https://aur.archlinux.org/packages/john-opencl/)<sup><small>AUR</small></sup>
*   [cuda_memtest](https://aur.archlinux.org/packages/cuda_memtest/)<sup><small>AUR</small></sup> - a GPU memtest. Despite its name, is supports both CUDA and OpenCL
*   [blender](https://www.archlinux.org/packages/?name=blender) - CUDA support for Nvidia GPUs and OpenCL support for AMD GPUs. More information [here](http://blender.org/manual/render/cycles/features.html#features).

## Links and references

*   [OpenCL official homepage](http://www.khronos.org/opencl/)
*   [CUDA official homepage](http://www.nvidia.com/object/cuda_home_new.html)
*   [The ICD extension specification](http://www.khronos.org/registry/cl/extensions/khr/cl_khr_icd.txt)
*   [AMD APP SDK homepage](http://developer.amd.com/appsdk)
*   [CUDA Toolkit homepage](https://developer.nvidia.com/cuda-toolkit)
*   [Intel SDK for OpenCL Applications homepage](https://software.intel.com/en-us/intel-opencl)

Retrieved from "[https://wiki.archlinux.org/index.php?title=GPGPU&oldid=409454](https://wiki.archlinux.org/index.php?title=GPGPU&oldid=409454)"

[Categories](/index.php/Special:Categories "Special:Categories"):

*   [Development](/index.php/Category:Development "Category:Development")
*   [Graphics](/index.php/Category:Graphics "Category:Graphics")