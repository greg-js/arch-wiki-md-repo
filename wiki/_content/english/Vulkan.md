From [wikipedia:Vulkan (API)](https://en.wikipedia.org/wiki/Vulkan_(API) "wikipedia:Vulkan (API)"):

	Vulkan, initially referred to as "glNext", is a low-overhead, cross-platform 3D graphics and compute API.

Learn more at [Khronos](https://www.khronos.org/vulkan/).

## Installation

To run a Vulkan appplication, you will need to [install](/index.php/Install "Install") the [vulkan-icd-loader](https://www.archlinux.org/packages/?name=vulkan-icd-loader) package, as well as the Vulkan drivers for your graphics card(s):

*   Intel: [vulkan-intel](https://www.archlinux.org/packages/?name=vulkan-intel)

The other drivers are not packaged yet, so you will have to install them manually:

*   NVIDIA: [https://developer.nvidia.com/vulkan-driver](https://developer.nvidia.com/vulkan-driver)
*   AMD: [http://gpuopen.com/gaming-product/vulkan/](http://gpuopen.com/gaming-product/vulkan/)
*   PowerVR: [https://imgtec.com/vulkan](https://imgtec.com/vulkan)
*   Adreno: [https://developer.qualcomm.com/software/adreno-gpu-sdk/gpu](https://developer.qualcomm.com/software/adreno-gpu-sdk/gpu)

To develop a Vulkan application, you will also need the [vulkan-headers](https://www.archlinux.org/packages/?name=vulkan-headers), and you will probably want the [vulkan-validation-layers](https://www.archlinux.org/packages/?name=vulkan-validation-layers) and the [vulkan-tools](https://www.archlinux.org/packages/?name=vulkan-tools).