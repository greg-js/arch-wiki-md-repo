From [wikipedia:Vulkan (API)](https://en.wikipedia.org/wiki/Vulkan_(API) "wikipedia:Vulkan (API)"):

	Vulkan is a low-overhead, cross-platform 3D graphics and compute API.

Learn more at [Khronos](https://www.khronos.org/vulkan/).

## Contents

*   [1 Installation](#Installation)
*   [2 Vulkan Hardware Database](#Vulkan_Hardware_Database)
*   [3 Troubleshooting](#Troubleshooting)
    *   [3.1 Error - vulkan: No DRI3 support](#Error_-_vulkan:_No_DRI3_support)
    *   [3.2 Nvidia - vulkan is not working and can not initialize](#Nvidia_-_vulkan_is_not_working_and_can_not_initialize)

## Installation

**Note:** On hybrid graphics ([NVIDIA Optimus](/index.php/NVIDIA_Optimus "NVIDIA Optimus")/AMD Dynamic Switchable Graphics):

*   Vulkan is not currently supported by [Bumblebee](/index.php/Bumblebee "Bumblebee") [[1]](https://github.com/Bumblebee-Project/Bumblebee/issues/769).
*   The Radeon Vulkan driver now supports [PRIME](/index.php/PRIME "PRIME") [[2]](http://www.phoronix.com/scan.php?page=news_item&px=RADV-PRIME-Lands).

To run a Vulkan application, you will need to [install](/index.php/Install "Install") the [vulkan-icd-loader](https://www.archlinux.org/packages/?name=vulkan-icd-loader) package, as well as the Vulkan drivers for your graphics card(s):

*   [Intel](/index.php/Intel "Intel"): [vulkan-intel](https://www.archlinux.org/packages/?name=vulkan-intel)
*   [NVIDIA](/index.php/NVIDIA "NVIDIA"): [nvidia](https://www.archlinux.org/packages/?name=nvidia)
*   AMD: [vulkan-radeon](https://www.archlinux.org/packages/?name=vulkan-radeon) ([radeon](/index.php/Radeon "Radeon"), [AMDGPU](/index.php/AMDGPU "AMDGPU") [[3]](https://www.phoronix.com/scan.php?page=news_item&px=RADV-Vulkan-CTS-Conformant)) or [amdgpu-pro-vulkan](https://aur.archlinux.org/packages/amdgpu-pro-vulkan/) ([AMDGPU PRO](/index.php/AMDGPU_PRO "AMDGPU PRO"))

Other drivers may be installed manually instead:

*   PowerVR: [https://imgtec.com/vulkan](https://imgtec.com/vulkan)
*   Adreno: [https://developer.qualcomm.com/software/adreno-gpu-sdk/gpu](https://developer.qualcomm.com/software/adreno-gpu-sdk/gpu)

For Vulkan application development, [install](/index.php/Install "Install") [vulkan-headers](https://www.archlinux.org/packages/?name=vulkan-headers), and optional [vulkan-validation-layers](https://www.archlinux.org/packages/?name=vulkan-validation-layers).

## Vulkan Hardware Database

The [Vulkan Hardware Database](http://vulkan.gpuinfo.org/) provides user reported GPU/driver combinations. Supplying own information is possible by using [vulkan-caps-viewer](https://aur.archlinux.org/packages/vulkan-caps-viewer/).

## Troubleshooting

### Error - vulkan: No DRI3 support

If you get the message above and using [Intel graphics](/index.php/Intel_graphics "Intel graphics"), you may need to force DRI3 and restart [Xorg](/index.php/Xorg "Xorg"):

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

```
 export VK_ICD_FILENAMES=/usr/share/vulkan/icd.d/nvidia_icd.json

```