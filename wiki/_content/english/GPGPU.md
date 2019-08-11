Related articles

*   [Catalyst](/index.php/Catalyst "Catalyst")
*   [Nvidia](/index.php/Nvidia "Nvidia")
*   [Hardware video acceleration](/index.php/Hardware_video_acceleration "Hardware video acceleration")

GPGPU stands for [General-purpose computing on graphics processing units](https://en.wikipedia.org/wiki/GPGPU "wikipedia:GPGPU"). In Linux, there are currently two major GPGPU frameworks: [OpenCL](https://en.wikipedia.org/wiki/OpenCL "wikipedia:OpenCL") and [CUDA](https://en.wikipedia.org/wiki/CUDA "wikipedia:CUDA").

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 OpenCL](#OpenCL)
    *   [1.1 OpenCL Runtime](#OpenCL_Runtime)
        *   [1.1.1 AMD/ATI](#AMD/ATI)
        *   [1.1.2 NVIDIA](#NVIDIA)
        *   [1.1.3 Intel](#Intel)
        *   [1.1.4 Others](#Others)
    *   [1.2 OpenCL ICD loader (libOpenCL.so)](#OpenCL_ICD_loader_(libOpenCL.so))
    *   [1.3 OpenCL Development](#OpenCL_Development)
    *   [1.4 Implementations](#Implementations)
        *   [1.4.1 Language bindings](#Language_bindings)
*   [2 SYCL](#SYCL)
    *   [2.1 Implementations](#Implementations_2)
    *   [2.2 Checking For SPIR Support](#Checking_For_SPIR_Support)
    *   [2.3 SYCL Development](#SYCL_Development)
*   [3 CUDA](#CUDA)
    *   [3.1 Development](#Development)
    *   [3.2 Language bindings](#Language_bindings_2)
*   [4 List of GPGPU accelerated software](#List_of_GPGPU_accelerated_software)
*   [5 Links and references](#Links_and_references)

## OpenCL

OpenCL (Open Computing Language) is an open, royalty-free parallel programming specification developed by the Khronos Group, a non-profit consortium.

The OpenCL specification describes a programming language, a general environment that is required to be present, and a C API to enable programmers to call into this environment.

**Tip:** The [clinfo](https://www.archlinux.org/packages/?name=clinfo) utility can be used to list OpenCL platforms, devices present and ICD loader properties.

### OpenCL Runtime

To **execute** programs that use OpenCL, a compatible hardware runtime needs to be installed.

#### AMD/ATI

*   [opencl-mesa](https://www.archlinux.org/packages/?name=opencl-mesa): free runtime for [AMDGPU](/index.php/AMDGPU "AMDGPU") and [Radeon](/index.php/Radeon "Radeon")
*   [opencl-amd](https://aur.archlinux.org/packages/opencl-amd/): proprietary standalone runtime for [AMDGPU](/index.php/AMDGPU "AMDGPU") (pal and legacy stacks in a single package)
*   [rocm-opencl-runtime](https://aur.archlinux.org/packages/rocm-opencl-runtime/): Part of AMD's fully open-source ROCm GPU compute stack, which supports GFX8 and later cards(Fiji, Polaris, Vega)
*   [opencl-amdgpu-pro-orca](https://aur.archlinux.org/packages/opencl-amdgpu-pro-orca/): proprietary runtime for [AMDGPU PRO](/index.php/AMDGPU_PRO "AMDGPU PRO") (supports legacy products older than Vega 10)
*   [opencl-amdgpu-pro-pal](https://aur.archlinux.org/packages/opencl-amdgpu-pro-pal/): proprietary runtime for [AMDGPU PRO](/index.php/AMDGPU_PRO "AMDGPU PRO") (supports Vega 10 and later products)
*   [opencl-catalyst](https://aur.archlinux.org/packages/opencl-catalyst/): AMD proprietary runtime, soon to be deprecated in favor of [AMDGPU](/index.php/AMDGPU "AMDGPU")
*   [amdapp-sdk](https://aur.archlinux.org/packages/amdapp-sdk/): AMD CPU runtime

#### NVIDIA

*   [opencl-nvidia](https://www.archlinux.org/packages/?name=opencl-nvidia): official [NVIDIA](/index.php/NVIDIA "NVIDIA") runtime

#### Intel

*   [intel-compute-runtime](https://www.archlinux.org/packages/?name=intel-compute-runtime): a.k.a. the Neo OpenCL runtime, the open-source implementation for Intel HD Graphics GPU on Gen8 (Broadwell) and beyond.
*   [beignet](https://www.archlinux.org/packages/?name=beignet): the open-source implementation for Intel HD Graphics GPU on Gen7 (Ivy Bridge) and beyond, deprecated by Intel in favour of NEO OpenCL driver, remains recommended solution for legacy HW platforms (e.g. Ivy Bridge, Sandy Bridge, Haswell).
*   [intel-opencl](https://aur.archlinux.org/packages/intel-opencl/): the proprietary implementation for Intel HD Graphics GPU on Gen7 (Ivy Bridge) and beyond, deprecated by Intel in favour of NEO OpenCL driver, remains recommended solution for legacy HW platforms (e.g. Ivy Bridge, Sandy Bridge, Haswell).
*   [intel-opencl-runtime](https://aur.archlinux.org/packages/intel-opencl-runtime/): the implementation for Intel Core and Xeon processors. It also supports non-Intel CPUs.

#### Others

*   [pocl](https://aur.archlinux.org/packages/pocl/): LLVM-based OpenCL implementation

### OpenCL ICD loader (libOpenCL.so)

The OpenCL ICD loader is supposed to be a platform-agnostic library that provides the means to load device-specific drivers through the OpenCL API. Most OpenCL vendors provide their own implementation of an OpenCL ICD loader, and these should all work with the other vendors' OpenCL implementations. Unfortunately, most vendors do not provide completely up-to-date ICD loaders, and therefore Arch Linux has decided to provide this library from a separate project ([ocl-icd](https://www.archlinux.org/packages/?name=ocl-icd)) which currently provides a functioning implementation of the current OpenCL API.

The other ICD loader libraries are installed as part of each vendor's SDK. If you want to ensure the ICD loader from the [ocl-icd](https://www.archlinux.org/packages/?name=ocl-icd) package is used, you can create a file in `/etc/ld.so.conf.d` which adds `/usr/lib` to the dynamic program loader's search directories:

 `/etc/ld.so.conf.d/00-usrlib.conf`  `/usr/lib` 

This is necessary because all the SDKs add their runtime's lib directories to the search path through `ld.so.conf.d` files.

The available packages containing various OpenCL ICDs are:

*   [ocl-icd](https://www.archlinux.org/packages/?name=ocl-icd): recommended, most up-to-date
*   [libopencl](https://aur.archlinux.org/packages/libopencl/) by AMD. Provides OpenCL 2.0\. It is distributed by AMD under a restrictive license and therefore cannot be included into the official repositories.
*   [intel-opencl](https://aur.archlinux.org/packages/intel-opencl/) by Intel. Provides OpenCL 2.0, deprecated in favour of [intel-compute-runtime](https://www.archlinux.org/packages/?name=intel-compute-runtime).

**Note:** ICD Loader's vendor is mentioned only to identify each loader, it is otherwise completely irrelevant. ICD loaders are vendor-agnostic and may be used interchangeably (as long as they are implemented correctly).

### OpenCL Development

For OpenCL **development**, the bare minimum additional packages required, are:

*   [ocl-icd](https://www.archlinux.org/packages/?name=ocl-icd): OpenCL ICD loader implementation, up to date with the latest OpenCL specification.
*   [opencl-headers](https://www.archlinux.org/packages/?name=opencl-headers): OpenCL C/C++ API headers.

The vendors' SDKs provide a multitude of tools and support libraries:

*   [intel-opencl-sdk](https://aur.archlinux.org/packages/intel-opencl-sdk/): [Intel OpenCL SDK](http://software.intel.com/en-us/articles/opencl-sdk/) (old version, new OpenCL SDKs are included in the INDE and Intel Media Server Studio)
*   [amdapp-sdk](https://aur.archlinux.org/packages/amdapp-sdk/): This package is installed as `/opt/AMDAPP` and apart from SDK files it also contains a number of code samples (`/opt/AMDAPP/SDK/samples/`). It also provides the `clinfo` utility which lists OpenCL platforms and devices present in the system and displays detailed information about them. As [AMD APP SDK](http://developer.amd.com/sdks/AMDAPPSDK/Pages/default.aspx) itself contains CPU OpenCL driver, no extra driver is needed to execute OpenCL on CPU devices (regardless of its vendor). GPU OpenCL drivers are provided by the [catalyst](https://aur.archlinux.org/packages/catalyst/) package (an optional dependency).
*   [cuda](https://www.archlinux.org/packages/?name=cuda): Nvidia's GPU SDK which includes support for OpenCL 1.1.

### Implementations

To see which OpenCL implementations are currently active on your system, use the following command:

```
$ ls /etc/OpenCL/vendors

```

To find out all possible (known) properties of the OpenCL platform and devices available on the system, [install](/index.php/Install "Install") [clinfo](https://www.archlinux.org/packages/?name=clinfo).

#### Language bindings

*   **JavaScript/HTML5**: [WebCL](http://www.khronos.org/webcl/)
*   **[Python](/index.php/Python "Python")**: [python-pyopencl](https://www.archlinux.org/packages/?name=python-pyopencl)
*   **[D](/index.php/D "D")**: [cl4d](https://bitbucket.org/trass3r/cl4d/wiki/Home)
*   **[Java](/index.php/Java "Java")**: [JOCL](http://jogamp.org/jocl/www/) (a part of [JogAmp](http://jogamp.org/))
*   **[Mono/.NET](/index.php/Mono "Mono")**: [Open Toolkit](http://sourceforge.net/projects/opentk/)
*   **[Go](/index.php/Go "Go")**: [OpenCL bindings for Go](https://github.com/samuel/go-opencl)
*   **Racket**: Racket has a native interface [on PLaneT](http://planet.racket-lang.org/display.ss?owner=jaymccarthy&package=opencl.plt) that can be installed via raco.
*   **[Rust](/index.php/Rust "Rust")**: [ocl](https://github.com/cogciprocate/ocl)
*   **[Julia](/index.php/Julia "Julia")**: [OpenCL.jl](https://github.com/JuliaGPU/OpenCL.jl)

## SYCL

[SYCL](https://en.wikipedia.org/wiki/SYCL "wikipedia:SYCL") is another open and royalty-free standard by the Khronos Group that defines a single-source heterogeneous programming model for C++ on top of OpenCL 1.2.

SYCL consists of a runtime part and a C++ device compiler. The device compiler may target any number and kind of accelerators. The runtime is required to fall back to a pure CPU code path in case no OpenCL implementation can be found.

### Implementations

*   [computecpp](https://aur.archlinux.org/packages/computecpp/) Codeplay's proprietary implementation of SYCL 1.2.1\. Can target SPIR, SPIR-V and experimentally PTX (NVIDIA) as device targets.
*   [trisycl-git](https://aur.archlinux.org/packages/trisycl-git/): Open source implementation mainly driven by Xilinx.
*   [hipsycl-cuda-git](https://aur.archlinux.org/packages/hipsycl-cuda-git/) and [hipsycl-rocm-git](https://aur.archlinux.org/packages/hipsycl-rocm-git/): Free implementation built over AMD's HIP instead of OpenCL. Is able to run on AMD and NVIDIA GPUs.

### Checking For SPIR Support

Most SYCL implementations are able to compile the accelerator code to [SPIR](https://en.wikipedia.org/wiki/Standard_Portable_Intermediate_Representation "wikipedia:Standard Portable Intermediate Representation") or [SPIR-V](https://en.wikipedia.org/wiki/Standard_Portable_Intermediate_Representation "wikipedia:Standard Portable Intermediate Representation"). Both are intermediate languages designed by Khronos that can be consumed by an OpenCL driver. To check whether SPIR or SPIR-V are supported [clinfo](https://www.archlinux.org/packages/?name=clinfo) can be used:

 `$ clinfo | grep -i spir` 
```
Platform Extensions                             cl_khr_icd cl_khr_global_int32_base_atomics cl_khr_global_int32_extended_atomics cl_khr_local_int32_base_atomics cl_khr_local_int32_extended_atomics cl_khr_byte_addressable_store cl_khr_depth_images cl_khr_3d_image_writes cl_intel_exec_by_local_thread cl_khr_spir cl_khr_fp64 cl_khr_image2d_from_buffer cl_intel_vec_len_hint 
  IL version                                    SPIR-V_1.0
  SPIR versions                                 1.2
```

ComputeCpp additionally ships with a tool that summarizes the relevant system information:

 `$ computecpp_info` 
```
Device 0:

  Device is supported                     : UNTESTED - Untested OS
  CL_DEVICE_NAME                          : Intel(R) Core(TM) i7-4770K CPU @ 3.50GHz
  CL_DEVICE_VENDOR                        : Intel(R) Corporation
  CL_DRIVER_VERSION                       : 18.1.0.0920
  CL_DEVICE_TYPE                          : CL_DEVICE_TYPE_CPU 

```

Drivers known to at least partially support SPIR or SPIR-V include [intel-compute-runtime](https://www.archlinux.org/packages/?name=intel-compute-runtime), [intel-opencl-runtime](https://aur.archlinux.org/packages/intel-opencl-runtime/), [pocl](https://aur.archlinux.org/packages/pocl/) and [amdgpu-pro-opencl](https://aur.archlinux.org/packages/amdgpu-pro-opencl/).

### SYCL Development

SYCL requires a working C++11 environment to be set up. There are a few open source libraries available:

*   [ComputeCpp SDK](https://github.com/codeplaysoftware/computecpp-sdk/): Collection of code examples, [cmake](https://www.archlinux.org/packages/?name=cmake) integration for ComputeCpp
*   [SYCL-DNN](https://github.com/codeplaysoftware/SYCL-DNN): Neural network performance primitives
*   [SYCL-BLAS](https://github.com/codeplaysoftware/SYCL-BLAS): Linear algebra performance primitives
*   [VisionCpp](https://github.com/codeplaysoftware/visioncpp): Computer Vision library
*   [SYCL Parallel STL](https://github.com/KhronosGroup/SyclParallelSTL): GPU implementation of the C++17 parallel algorithms

## CUDA

[CUDA](https://en.wikipedia.org/wiki/CUDA "wikipedia:CUDA") (Compute Unified Device Architecture) is [NVIDIA](/index.php/NVIDIA "NVIDIA")'s proprietary, closed-source parallel computing architecture and framework. It requires a NVIDIA GPU. It consists of several components:

*   required:
    *   proprietary Nvidia kernel module
    *   CUDA "driver" and "runtime" libraries
*   optional:
    *   additional libraries: CUBLAS, CUFFT, CUSPARSE, etc.
    *   CUDA toolkit, including the `nvcc` compiler
    *   CUDA SDK, which contains many code samples and examples of CUDA and OpenCL programs

The kernel module and CUDA "driver" library are shipped in [nvidia](https://www.archlinux.org/packages/?name=nvidia) and [opencl-nvidia](https://www.archlinux.org/packages/?name=opencl-nvidia). The "runtime" library and the rest of the CUDA toolkit are available in [cuda](https://www.archlinux.org/packages/?name=cuda). The library is available [only in 64-bit version](https://projects.archlinux.org/svntogit/community.git/commit/trunk?h=packages/cuda&id=1b62c8bcb9194b2de1b750bd62a8dce1e7e549f5). `cuda-gdb` needs [ncurses5-compat-libs](https://aur.archlinux.org/packages/ncurses5-compat-libs/) to be installed, see [FS#46598](https://bugs.archlinux.org/task/46598).

### Development

The [cuda](https://www.archlinux.org/packages/?name=cuda) package installs all components in the directory `/opt/cuda`. For compiling CUDA code, add `/opt/cuda/include` to your include path in the compiler instructions. For example this can be accomplished by adding `-I/opt/cuda/include` to the compiler flags/options. To use `nvcc`, a `gcc` wrapper provided by NVIDIA, just add `/opt/cuda/bin` to your path.

To find whether the installation was successful and if cuda is up and running, you can compile the samples installed on `/opt/cuda/samples` (you can simply run `make` inside the directory, altough is a good practice to copy the `/opt/cuda/samples` directory to your home directory before compiling) and running the compiled examples. A nice way to check the installation is to run one of the examples, called `deviceQuery`.

### Language bindings

*   **Fortran**: [PGI CUDA Fortran Compiler](http://www.pgroup.com/resources/cudafortran.htm)
*   **[Haskell](/index.php/Haskell "Haskell")**: The [accelerate package](http://hackage.haskell.org/package/accelerate) lists available CUDA backends
*   **[Java](/index.php/Java "Java")**: [JCuda](http://www.jcuda.org/jcuda/JCuda.html)
*   **[Mathematica](/index.php/Mathematica "Mathematica")**: [CUDAlink](http://reference.wolfram.com/mathematica/CUDALink/tutorial/Overview.html)
*   **[Mono/.NET](/index.php/Mono "Mono")**: [CUDA.NET](http://www.hoopoe-cloud.com/Solutions/CUDA.NET/Default.aspx), [CUDAfy.NET](http://www.hybriddsp.com/)
*   **Perl**: [KappaCUDA](https://metacpan.org/pod/KappaCUDA), [CUDA-Minimal](https://github.com/run4flat/perl-CUDA-Minimal)
*   **[Python](/index.php/Python "Python")**: [python-pycuda](https://www.archlinux.org/packages/?name=python-pycuda) or [Kappa](http://psilambda.com/download/kappa-for-python)
*   **[Ruby](/index.php/Ruby "Ruby")**, **Lua**: [Kappa](http://psilambda.com/products/kappa/)

## List of GPGPU accelerated software

*   [Bitcoin](/index.php/Bitcoin "Bitcoin")
*   [Blender](/index.php/Blender "Blender") – CUDA support for Nvidia GPUs and OpenCL support for AMD GPUs. More information [here](http://blender.org/manual/render/cycles/features.html#features).
*   [BOINC](/index.php/BOINC "BOINC")
*   [FFmpeg](/index.php/FFmpeg "FFmpeg") – more information [here](https://trac.ffmpeg.org/wiki/HWAccelIntro#OpenCL).
*   [GIMP](/index.php/GIMP "GIMP") – experimental – more information [here](http://www.h-online.com/open/news/item/GIMP-2-8-RC-1-arrives-with-GPU-acceleration-1518417.html).
*   [HandBrake](/index.php/HandBrake "HandBrake")
*   [Hashcat](/index.php/Hashcat "Hashcat")
*   [LibreOffice](/index.php/LibreOffice "LibreOffice") Calc – more information [here](https://help.libreoffice.org/Calc/OpenCL_Options).
*   [clinfo](https://www.archlinux.org/packages/?name=clinfo) – Find all possible (known) properties of the OpenCL platform and devices available on the system.
*   [cuda_memtest](https://aur.archlinux.org/packages/cuda_memtest/) – a GPU memtest. Despite its name, is supports both CUDA and OpenCL.
*   [davinci-resolve](https://aur.archlinux.org/packages/davinci-resolve/) - a non-linear video editor. Can use both OpenCL and CUDA.
*   [darktable](https://www.archlinux.org/packages/?name=darktable) – OpenCL feature requires at least 1 GB RAM on GPU and *Image support* (check output of clinfo command).
*   [imagemagick](https://www.archlinux.org/packages/?name=imagemagick)
*   [lc0](https://aur.archlinux.org/packages/lc0/) - Used for searching the neural network (supports tensorflow, OpenCL, CUDA, and openblas)
*   [opencv](https://www.archlinux.org/packages/?name=opencv)
*   [pyrit](https://www.archlinux.org/packages/?name=pyrit)
*   [tensorflow-cuda](https://www.archlinux.org/packages/?name=tensorflow-cuda) - Port of TensorFlow to CUDA
*   [tensorflow-computecpp](https://aur.archlinux.org/packages/tensorflow-computecpp/) - Port of TensorFlow to SYCL

## Links and references

*   [OpenCL official homepage](http://www.khronos.org/opencl/)
*   [SYCL official homepage](https://www.khronos.org/sycl/)
*   [SPIR official homepage](https://www.khronos.org/spir/)
*   [CUDA official homepage](http://www.nvidia.com/object/cuda_home_new.html)
*   [The ICD extension specification](http://www.khronos.org/registry/cl/extensions/khr/cl_khr_icd.txt)
*   [AMD APP SDK homepage](http://developer.amd.com/appsdk)
*   [CUDA Toolkit homepage](https://developer.nvidia.com/cuda-toolkit)
*   [Intel SDK for OpenCL Applications homepage](https://software.intel.com/en-us/intel-opencl)
*   [ComputeCpp official homepage](https://developer.codeplay.com/home/)