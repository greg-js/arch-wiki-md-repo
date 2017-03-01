From [wikipedia:Vulkan (API)](https://en.wikipedia.org/wiki/Vulkan_(API) "wikipedia:Vulkan (API)"):

	Vulkan, initially referred to as "glNext", is a low-overhead, cross-platform 3D graphics and compute API.

Learn more at [Khronos](https://www.khronos.org/vulkan/).

## Contents

*   [1 Installation](#Installation)
*   [2 Troubleshooting](#Troubleshooting)
    *   [2.1 Error - vulkan: No DRI3 support](#Error_-_vulkan:_No_DRI3_support)
    *   [2.2 Nvidia - vulkan is not working and can not initialize](#Nvidia_-_vulkan_is_not_working_and_can_not_initialize)

## Installation

**Note:** Vulkan is not currently supported by [Bumblebee](/index.php/Bumblebee "Bumblebee"). See [[1]](https://github.com/Bumblebee-Project/Bumblebee/issues/769)

**Note:** The Radeon Vulkan driver now supports [PRIME](/index.php/PRIME "PRIME"). See [[2]](http://www.phoronix.com/scan.php?page=news_item&px=RADV-PRIME-Lands)

To run a Vulkan application, you will need to [install](/index.php/Install "Install") the [vulkan-icd-loader](https://www.archlinux.org/packages/?name=vulkan-icd-loader) package, as well as the Vulkan drivers for your graphics card(s):

*   Intel: [vulkan-intel](https://www.archlinux.org/packages/?name=vulkan-intel)
*   NVIDIA: [nvidia](https://www.archlinux.org/packages/?name=nvidia)
*   AMD: [vulkan-radeon](https://www.archlinux.org/packages/?name=vulkan-radeon) (open-source) or [amdgpu-pro-vulkan](https://aur.archlinux.org/packages/amdgpu-pro-vulkan/) (proprietary)

The other drivers are not packaged yet, so you will have to install them manually:

*   PowerVR: [https://imgtec.com/vulkan](https://imgtec.com/vulkan)
*   Adreno: [https://developer.qualcomm.com/software/adreno-gpu-sdk/gpu](https://developer.qualcomm.com/software/adreno-gpu-sdk/gpu)

To develop a Vulkan application, you will also need the [vulkan-headers](https://www.archlinux.org/packages/?name=vulkan-headers), and you will probably want the [vulkan-validation-layers](https://www.archlinux.org/packages/?name=vulkan-validation-layers).

Once this is done, it would really be appreciated if you would share the specs of your GPU/driver combination to [vulkan.gpuinfo.org](http://vulkan.gpuinfo.org/) by running [vulkan-caps-viewer](https://aur.archlinux.org/packages/vulkan-caps-viewer/). Thank you!

## Troubleshooting

### Error - vulkan: No DRI3 support

If you get the message above, make sure to create the following file with the given content and restart your X. This should not be necessary on Wayland.

 `/etc/X11/xorg.conf.d/20-intel.conf` 
```
Section "Device"
   Identifier  "Intel Graphics"
   Driver      "intel"
   Option      "DRI"    "3"
EndSection
```

### Nvidia - vulkan is not working and can not initialize

Check if you have [vulkan-intel](https://www.archlinux.org/packages/?name=vulkan-intel) installed, it may prevent Nvidia's vulkan driver from being detected.