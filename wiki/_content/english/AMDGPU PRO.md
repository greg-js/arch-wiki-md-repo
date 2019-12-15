The amdgpu-pro-installer contains proprietary components for AMDGPU (a.k.a. Radeon Software for Linux).

For proprietary OpenGL implementation, install [amdgpu-pro-libgl](https://aur.archlinux.org/packages/amdgpu-pro-libgl/). See [AMDGPU#AMDGPU PRO](/index.php/AMDGPU#AMDGPU_PRO "AMDGPU") for more details.

For proprietary OpenCL implementation, install [opencl-amdgpu-pro-orca](https://aur.archlinux.org/packages/opencl-amdgpu-pro-orca/) or [opencl-amdgpu-pro-pal](https://aur.archlinux.org/packages/opencl-amdgpu-pro-pal/). See [GPGPU#AMD/ATI](/index.php/GPGPU#AMD/ATI "GPGPU") for more details.

For proprietary Vulkan implementation, install [vulkan-amdgpu-pro](https://aur.archlinux.org/packages/vulkan-amdgpu-pro/). See [Vulkan](/index.php/Vulkan "Vulkan") for more details.

## Troubleshooting

### Intel + AMD hybrid graphics

Currently (version 19.30) there is a problem when using amdgpu pro opengl driver alongside with intel gpu. It is usual configuration for laptops, but also applies to desktop in case you set intel gpu as primary. When you boot your machine, you get a black screen, but mouse cursor is moving normally. If you have suggestion, please edit this wiki page. Reverse prime probably could be a solution, but [PRIME#Reverse PRIME](/index.php/PRIME#Reverse_PRIME "PRIME") lacks this information.

If you are affected, please upvote [this](https://gitlab.freedesktop.org/drm/amd/issues/985) bug report.

### Uninstalling packages

If you are in trouble, for example, you cannot login to your system due to black screen, you can revert all back by uninstalling all packages related to amdgpu pro. Switch to the tty2 (ctrl+alt+f2), login to the system and run `pacman -Qg Radeon_Software_for_Linux | cut -f2 -d" "` to get a list of installed packages of corresponding group. Then remove them with `pacman -R` and reboot.