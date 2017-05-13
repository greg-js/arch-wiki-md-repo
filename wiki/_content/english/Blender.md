From [Wikipedia](https://en.wikipedia.org/wiki/Blender_(software) "wikipedia:Blender (software)"):

	Blender is a professional free and open-source 3D computer graphics software product used for creating animated films, visual effects, art, 3D printed models, interactive 3D applications and video games. Blender's features include 3D modeling, UV unwrapping, texturing, raster graphics editing, rigging and skinning, fluid and smoke simulation, particle simulation, soft body simulation, sculpting, animating, match moving, camera tracking, rendering, video editing and compositing. It further features an integrated game engine.

[Blender](http://www.blender.org) is best known as a popular open source 3D modelling program.

## Contents

*   [1 Installation](#Installation)
*   [2 GPU Rendering](#GPU_Rendering)
*   [3 Professional Rendering Plugins](#Professional_Rendering_Plugins)
    *   [3.1 LuxRenderer](#LuxRenderer)
    *   [3.2 RenderMan](#RenderMan)
    *   [3.3 Pro-Render](#Pro-Render)
    *   [3.4 Blend4Web](#Blend4Web)
*   [4 Troubleshooting](#Troubleshooting)
    *   [4.1 Blender UI graphical corruption on AMDGPU driver](#Blender_UI_graphical_corruption_on_AMDGPU_driver)
    *   [4.2 Blender does not show the AMD card as an OpenCL rendering device](#Blender_does_not_show_the_AMD_card_as_an_OpenCL_rendering_device)

## Installation

[Install](/index.php/Install "Install") the [blender](https://www.archlinux.org/packages/?name=blender) package.

## GPU Rendering

Blender only officially supports only the proprietary drivers from both AMD (for GCN cards: [AMDGPU](/index.php/AMDGPU "AMDGPU"); For pre-GCN cards: [ATI](/index.php/ATI "ATI")) and [NVIDIA](/index.php/NVIDIA "NVIDIA"). After installing the proprietary drivers, one can select the graphics card as a compute device under **File -> User Preferences -> System**.

## Professional Rendering Plugins

Blender is becoming increasingly well known in the professional industry. As such, there are now alternative rendering methods to the Blender Render and Cycles, in the form of plugins. This should serve as a list of the major professional rendering plugins that are released or upcoming for Linux.

### LuxRenderer

[LuxRenderer](http://www.luxrender.net/en_GB/index) is an open source rendering method that can also make use of openCL to render. To make use of it, simple install the package [luxblend25](https://www.archlinux.org/packages/?name=luxblend25) from the offical arch community repo, Then enable the LuxRender addon in the User Preferences box in Blender.

### RenderMan

RenderMan is a linux compatible proprietary rendering plugin that is free for use with blender under a non-commercial licence. See the [Renderman page](http://renderman.pixar.com/view/renderman4blender) for setting it up with blender.

### Pro-Render

[Pro-Render](https://github.com/Radeon-prorender/Blender/releases) is an upcoming open source Blender rendering plugin from AMD that will allow any machine capable of OpenCL 1.2 the ability to create realistic GPU renders, allowing for faster work compared to the CPU.

### Blend4Web

[Blend4Web](http://www.blend4web.com/) is an open source framework for creating and displaying interactive 3D graphics in web browsers. It contains a Blender add-on to create and export 3D scenes directly into the web. A Blend4Web-specific profile can be activated in the add-on settings. When switching to this profile, the Blender interface changes so that it only reveals settings relevant to Blend4Web. See the [documentation](https://www.blend4web.com/doc/en/setup.html) on how to install Blend4Web SDK.

## Troubleshooting

### Blender UI graphical corruption on AMDGPU driver

You may experience graphical corruption on the Blender user interface. Until this is fixed, the workaround is to use Triple Buffering for blender, that however may increase VRAM usage. This can be enabled by going to **File -> User Preferences -> System**, changing the **Window Draw Method** to **Triple Buffering**.

### Blender does not show the AMD card as an OpenCL rendering device

Blender only supports the official AMD proprietary drivers for rendering with OpenCL, meaning you will need to use AMD OpenCL drivers:

*   Install [AMDGPU#AMDGPU PRO](/index.php/AMDGPU#AMDGPU_PRO "AMDGPU")
*   Install [opencl-amd](https://aur.archlinux.org/packages/opencl-amd/) driver alongside the open source AMDGPU driver

After installation, the AMD GPU should now appear as a selectable device under **File -> User Preferences -> System -> Compute Device**.