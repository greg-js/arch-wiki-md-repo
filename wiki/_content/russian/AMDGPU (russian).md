Related articles

*   [AMD Catalyst](/index.php/AMD_Catalyst "AMD Catalyst")
*   [ATI](/index.php/ATI "ATI")
*   [Xorg](/index.php/Xorg "Xorg")

**amdgpu** это свободный грфический драйвер для последних видеокарт AMD Radeon.

В настоящий момент поддерживаются видекорты с архитектурой [Volcanic Islands (VI)](http://xorg.freedesktop.org/wiki/RadeonFeature/),некоторые видеокарты семейства [Sea Islands (CI)](https://www.phoronix.com/scan.php?page=news_item&px=AMD-AMDGPU-Released) и [Southern Islands (SI)](https://www.phoronix.com/scan.php?page=news_item&px=AMDGPU-SI-Experimental-Code) (поддержку старее Sea Islands введут только в [Xorg 1.2.0](https://lists.x.org/archives/xorg-announce/2016-November/002741.html) и Linux 4.9). AMD не планируют поддержку видеокарт c архитектуройй до GCN.

Владельцы неподдерживаемых видеокарт AMD/ATI могут использовать драйвера [Radeon (с открытым кодом)](/index.php/ATI "ATI") или [Catalyst (проприетарный драйвер от AMD)](/index.php/AMD_Catalyst "AMD Catalyst").

## Contents

*   [1 Выбор правильного драйвера](#Выбор_правильного_драйвера)
*   [2 Установка](#Установка)
    *   [2.1 AMDGPU PRO](#AMDGPU_PRO)
*   [3 Configuration](#Configuration)
*   [4 Loading](#Loading)
    *   [4.1 Enable early KMS](#Enable_early_KMS)
*   [5 Performance tuning](#Performance_tuning)
    *   [5.1 Enabling video acceleration](#Enabling_video_acceleration)
*   [6 Enable amdgpu for Sea Islands or Southern Islands cards](#Enable_amdgpu_for_Sea_Islands_or_Southern_Islands_cards)
*   [7 Disable radeon driver](#Disable_radeon_driver)
*   [8 Troubleshooting](#Troubleshooting)
    *   [8.1 Xorg or applications won't start](#Xorg_or_applications_won't_start)

## Выбор правильного драйвера

В зависимости от вашей карты, выберите правильный драйвер на странице [Xorg#AMD](/index.php/Xorg#AMD "Xorg"). Здесь - инструкция для **AMDGPU** и **AMDGPU PRO**.

## Установка

**Note:** Если ранее был установлен проприетарный драйвер Catalyst - сначала посмотрите, как его удалить: [AMD Catalyst#Uninstallation](/index.php/AMD_Catalyst#Uninstallation "AMD Catalyst").

[Install](/index.php/Install "Install") пакет [xf86-video-amdgpu](https://www.archlinux.org/packages/?name=xf86-video-amdgpu). В нем содержится драйвер DDX для 2D ускорения, и он является зависимостью [mesa](https://www.archlinux.org/packages/?name=mesa), обесппечивающей драйвер DRI для 3D ускорения.

Чтобы имелась поддержка OpenGL, также нужно установить [mesa-libgl](https://www.archlinux.org/packages/?name=mesa-libgl). Если у Вас архитектура x86_64 и нужна поддержка 32-разрядных приложений, установите еще [lib32-mesa-libgl](https://www.archlinux.org/packages/?name=lib32-mesa-libgl) из репозитория [multilib](/index.php/Multilib "Multilib").

Поддержка [accelerated video decoding](#Enabling_video_acceleration) обеспечивается пакетами [mesa-vdpau](https://www.archlinux.org/packages/?name=mesa-vdpau) и [lib32-mesa-vdpau](https://www.archlinux.org/packages/?name=lib32-mesa-vdpau).

**Note:** Пакет [xf86-video-amdgpu](https://www.archlinux.org/packages/?name=xf86-video-amdgpu) предназначен только для ускорения Xorg и не является строго необходимым.

### AMDGPU PRO

**Warning:** Arch Linux официально не поддерживается.

AMD поставляет проприетарный бинарный драйвер *AMDGPU PRO*, который работает поверх открытого драйвера ядра AMDGPU. Такой гибридный подход позволяет компиляцию модуля ядра мейнтейнерами Arch Linux, когда это понадобится (т.е., обновление ядра или Xorg), оставляя неизменной бинарную составляющую в пользовательском пространстве. Это должно устранить проблему несовместимости драйвера AMD с новыми сборками ядра и Xorg (что было бедой старого драйвера [AMD Catalyst](/index.php/AMD_Catalyst "AMD Catalyst")). Вы можете ознакомиться подробнее, прочитав [эту статью](http://www.phoronix.com/scan.php?page=news_item&px=MTgwODA).

AMDGPU PRO обеспечивает поддержку OpenGL, OpenCL, Vulkan и VDPAU. Он имеет более высокую производительность в сравнении со свободным драйвером ([тест производительности](http://www.phoronix.com/scan.php?page=news_item&px=AMDGPU-PRO-16.40-Deus-MD)).

Посмотрите [заметки к выпуску](http://support.amd.com/en-us/kb-articles/Pages/AMD-Radeon-GPU-PRO-Linux-Beta-Driver%E2%80%93Release-Notes.aspx) и [ветку на форуме Phoronix](https://www.phoronix.com/forums/forum/linux-graphics-x-org-drivers/amd-linux/855699-amd-representative-says-their-vulkan-linux-driver-will-be-here-soon/page6), чтобы узнать больше.

В [AUR](/index.php/AUR "AUR") ([amdgpu-pro](https://aur.archlinux.org/packages/amdgpu-pro/)) есть пакет с компонентами amdgpu-pro. А еще существует [репозиторий на GitHub](https://github.com/Corngood/archlinux-amdgpu).

## Configuration

Xorg will automatically load the driver and it will use your monitor's EDID to set the native resolution. Configuration is only required for tuning the driver.

If you want manual configuration, create `/etc/X11/xorg.conf.d/20-amdgpu.conf`, and add the following:

```
Section "Device"
    Identifier "AMD"
    Driver "amdgpu"
EndSection

```

Using this section, you can enable features and tweak the driver settings.

## Loading

The `amdgpu` kernel module should load fine automatically on system boot.

If it does not happen, then:

*   Make sure you have the latest [linux-firmware](https://www.archlinux.org/packages/?name=linux-firmware) package installed. This driver requires the latest firmware for each model to successfully boot.
*   Make sure you do **not** have `nomodeset` or `vga=` as a [kernel parameter](/index.php/Kernel_parameter "Kernel parameter"), since `amdgpu` requires [KMS](/index.php/KMS "KMS").
*   Also, check that you have not disabled `amdgpu` by using any [kernel module blacklisting](/index.php/Kernel_modules#Blacklisting "Kernel modules").

### Enable early KMS

**Tip:** If you have problems with the resolution, [Kernel mode setting#Forcing modes and EDID](/index.php/Kernel_mode_setting#Forcing_modes_and_EDID "Kernel mode setting") may help.

[Kernel mode setting](/index.php/Kernel_mode_setting "Kernel mode setting") (KMS) is supported by the amdgpu driver and is mandatory and enabled by default.

KMS is typically initialized after the [initramfs stage](/index.php/Arch_boot_process#initramfs "Arch boot process"). It is possible, however, to enable KMS during the initramfs stage. To do this, add the `amdgpu` module to the `MODULES` line in `/etc/mkinitcpio.conf`:

```
MODULES="... amdgpu ..."

```

Now, regenerate the initramfs:

```
# mkinitcpio -p linux

```

The change takes effect at the next reboot.

## Performance tuning

### Enabling video acceleration

See [Hardware video acceleration](/index.php/Hardware_video_acceleration "Hardware video acceleration").

## Enable amdgpu for Sea Islands or Southern Islands cards

`amdgpu` has experimental support for Sea Islands (CIK) and Southern Islands (SI; since Linux 4.9) cards, which is disabled by default. One possible reason why you might want to enable it and switch from radeon to `amdgpu` is that AMD announced their user space [Vulkan](https://www.khronos.org/vulkan/) driver will only be supporting the new `amdgpu` stack [[1]](https://phoronix.com/scan.php?page=news_item&px=AMDGPU-Vulkan-Driver-Only). Same might be the case for the new OpenCL driver, which was also mentioned in the [XDC presentation](http://www.x.org/wiki/Events/XDC2015/Program/deucher_zhou_amdgpu.pdf).

If you want to enable `amdgpu` and use it with your Sea Islands or Southern Islands product, you have to recompile your kernel. Probably the easiest way to setup a custom kernel is using the ABS, described in [Kernels/Arch Build System](/index.php/Kernels/Arch_Build_System "Kernels/Arch Build System"). You can also uncomment `make menuconfig` or `make nconfig` in the PKGBUILD, which will allow you to verify that the CIK option is selected by following the instructions from [Gentoo wiki](https://wiki.gentoo.org/wiki/Amdgpu#Feature_support).

For Sea Islands (CIK), set "Enable amdgpu support for CIK parts" to "yes", then compile and install your kernel.

```
CONFIG_DRM_AMDGPU_CIK=Y

```

For Southern Islands (SI; since Linux 4.9), set "Enable amdgpu support for SI parts" to "yes", then compile and install your kernel.

```
CONFIG_DRM_AMDGPU_SI=Y

```

It may also be needed to use the `amdgpu.exp_hw_support=1` [[2]](https://www.phoronix.com/scan.php?page=news_item&px=AMDGPU-Iceland-Experimental) as [kernel parameter](/index.php/Kernel_parameter "Kernel parameter") or by setting the [kernel module](/index.php/Kernel_modules#Using_files_in_.2Fetc.2Fmodprobe.d.2F "Kernel modules") options.

## Disable radeon driver

To prevent `radeon` from loading, you can disable it in the Kconfig or [blacklist](/index.php/Blacklist "Blacklist") the `radeon` module.

 `/etc/modprobe.d/radeon.conf`  `blacklist radeon` 

## Troubleshooting

### Xorg or applications won't start

*   "(EE) AMDGPU(0): [DRI2] DRI2SwapBuffers: drawable has no back or front?" error after opening glxgears, can open Xorg server but OpenGL apps crash.
*   "(EE) AMDGPU(0): Given depth (32) is not supported by amdgpu driver" error, Xorg won't start.

Setting the screen's depth under Xorg to 16 or 32 will cause problems/crash. To avoid that, you should use a standard screen depth of 24 by adding this to your "screen" section (assuming you have one, assuming you don't add this to `/etc/X11/xorg.conf.d/10-screen.conf`).

```
Section "Screen"
       DefaultDepth    24
       SubSection      "Display"
               Depth   24
       EndSubSection
EndSection

```