The amdgpu-pro-installer contains proprietary components for AMDGPU (a.k.a. Radeon Software for Linux).

For proprietary OpenGL implementation, install [amdgpu-pro-libgl](https://aur.archlinux.org/packages/amdgpu-pro-libgl/). See [AMDGPU#AMDGPU PRO](/index.php/AMDGPU#AMDGPU_PRO "AMDGPU") for more details.

For proprietary OpenCL implementation, install [opencl-amdgpu-pro-orca](https://aur.archlinux.org/packages/opencl-amdgpu-pro-orca/) or [opencl-amdgpu-pro-pal](https://aur.archlinux.org/packages/opencl-amdgpu-pro-pal/). See [GPGPU#AMD/ATI](/index.php/GPGPU#AMD/ATI "GPGPU") for more details.

For proprietary Vulkan implementation, install [vulkan-amdgpu-pro](https://aur.archlinux.org/packages/vulkan-amdgpu-pro/). See [Vulkan](/index.php/Vulkan "Vulkan") for more details.

## Troubleshooting

### Intel + AMD hybrid graphics

Currently (version 19.30) there is a problem when using amdgpu pro opengl driver alongside with intel gpu. It is usual configuration for laptops, but also applies to desktop in case you set intel gpu as primary. When you boot your machine, you get a black screen, but mouse cursor is moving normally. If you have suggestion, please edit this wiki page. Reverse prime probably could be a solution, but [PRIME#Reverse_PRIME](/index.php/PRIME#Reverse_PRIME "PRIME") lacks this information.