VirtualGL redirects an application's *OpenGL/GLX commands* to a separate X server (that has access to a 3D graphics card), captures the rendered images, and then streams them to the X server that actually handles the application.

The main use-case is to enable server-side hardware-accelerated 3D rendering for *remote desktop* set-ups where the X server that handles the application is either on the other side of the network *(in the case of X11 forwarding)*, or a "virtual" X server that cannot access the graphics hardware *(in the case of VNC)*.

## Contents

*   [1 Installation and setup](#Installation_and_setup)
*   [2 Using VirtualGL with X11 forwarding](#Using_VirtualGL_with_X11_forwarding)
    *   [2.1 Instructions](#Instructions)
*   [3 Using VirtualGL with VNC](#Using_VirtualGL_with_VNC)
    *   [3.1 Instructions](#Instructions_2)
    *   [3.2 Choosing an appropriate VNC package](#Choosing_an_appropriate_VNC_package)
*   [4 Running applications](#Running_applications)
    *   [4.1 Confirming that VirtualGL rendering is active](#Confirming_that_VirtualGL_rendering_is_active)
    *   [4.2 Measuring performance](#Measuring_performance)
*   [5 Troubleshooting](#Troubleshooting)
    *   [5.1 Problem: vglrun aborts with "Could not open display"](#Problem:_vglrun_aborts_with_.22Could_not_open_display.22)
    *   [5.2 Problem: vglrun seems to have no effect at all](#Problem:_vglrun_seems_to_have_no_effect_at_all)
    *   [5.3 Problem: vglrun fails with ld.so errors](#Problem:_vglrun_fails_with_ld.so_errors)
    *   [5.4 Problem: vglrun fails with ERROR: Could not connect to VGL client.](#Problem:_vglrun_fails_with_ERROR:_Could_not_connect_to_VGL_client.)
    *   [5.5 Problem: Error messages about /etc/opt/VirtualGL/vgl_xauth_key not existing](#Problem:_Error_messages_about_.2Fetc.2Fopt.2FVirtualGL.2Fvgl_xauth_key_not_existing)
    *   [5.6 Problem: rendering glitches, unusually poor performance, or application errors](#Problem:_rendering_glitches.2C_unusually_poor_performance.2C_or_application_errors)
*   [6 See also](#See_also)

## Installation and setup

Install the virtualgl package using pacman, then follow the instructions [here](https://cdn.rawgit.com/VirtualGL/virtualgl/2.5/doc/index.html#hd006) to configure it. On arch, /opt/VirtualGL/bin/vglserver_config is just vglserver_config and /opt/VirtualGL/bin/glxinfo is vglxinfo.

## Using VirtualGL with X11 forwarding

```
 **server:                                              client:**
······································               ·················
: ┌───────────┐ *X11 commands*         :               : ┌───────────┐ :
: │application│━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━▶│<font color="blue">X server</font>   │ :
: │           │        ┌───────────┐ :               : │           │ :
: │           │        │<font color="red">X server</font>   │ :               : ├┈┈┈┈┈┈┈┈┈╮ │ :
: │ ╭┈┈┈┈┈┈┈┈┈┤ *OpenGL* │ ╭┈┈┈┈┈┈┈┈┈┤ : *image stream*  : │VirtualGL┊ │ :
: │ ┊VirtualGL│━━━━━━━▶│ ┊VirtualGL│━━━━━━━━━━━━━━━━━━▶│client   ┊ │ :     <font color="blue">⬛</font> = "2D" rendering happens here
: └─┴─────────┘        └─┴─────────┘ :               : └─────────┴─┘ :     <font color="red">⬛</font> = "3D" rendering happens here
······································               ·················

```

*Advantages of this set-up, compared to using [VirtualGL with VNC](#Using_VirtualGL_with_VNC):*

*   seamless windows
*   uses a little less CPU resources on the server side
*   supports stereo rendering (for viewing with "3D glasses")

### Instructions

***1\. Preparation***

In addition to setting up VirtualGL on the remote server [as described above](#Installation_and_setup), this usage scenario requires you to:

*   install the [virtualgl](https://www.archlinux.org/packages/?name=virtualgl) package on the client side as well *(but no need to set it up like on the server side, we just need the `vglconnect` and `vglclient` binaries on this end)*.
*   set up [SSH with X11 forwarding](/index.php/SSH#X11_forwarding "SSH") *(confirm that connecting from the client to the server via `ssh -X user@server` and running GUI applications in the resulting shell works)*

***2\. Connecting***

Now you can use `vglconnect` on the client computer whenever you want to connect to the server:

```
$ vglconnect user@server     *# X11 traffic encrypted, VGL image stream unencrypted*

```

```
$ vglconnect -s user@server  *# both X11 traffic and VGL image stream encrypted*

```

This opens an SSH session with X11 forwarding just like `ssh -X` would, and also automatically starts the VirtualGL Client (`vglclient`) with the right parameters as a background daemon. This daemon will handle incoming VirtualGL image streams from the server, and will keep running in the background even after you close the SSH shell - you can stop it with `vglclient -kill`.

***3\. Running applications***

Once connected, you can run remote applications with VirtualGL rendering enabled for their OpenGL parts, by starting them inside the SSH shell with `vglrun` as described in [Running Applications](#Running_applications) below.

You do not need to restrict yourself to the shell that `vglconnect` opened for you; any `ssh -X` or `ssh -Y` shell you open from the same X session on the client to the same *user*@*server* should work. `vglrun` will detect that you are in an SSH shell, and make sure that the VGL image stream is sent over the network to the IP/hostname belonging to the SSH client (where the running `vglclient` instance will intercept and process it).

## Using VirtualGL with VNC

```
 **server:                                                           client:**
···················································               ················
: ┌───────────┐ *X11 commands*         ┌──────────┐ : *image stream*  : ┌──────────┐ :
: │application│━━━━━━━━━━━━━━━━━━━━━▶│<font color="blue">VNC server</font>│━━━━━━━━━━━━━━━━━━▶│VNC viewer│ :
: │           │        ┌───────────┐ └──────────┘ :               : └──────────┘ :
: │           │        │<font color="red">X server</font>   │        ▲     :               :              :
: │ ╭┈┈┈┈┈┈┈┈┈┤ *OpenGL* │ ╭┈┈┈┈┈┈┈┈┈┤ *images* ┃     :               :              :
: │ ┊VirtualGL│━━━━━━━▶│ ┊VirtualGL│━━━━━━━━┛     :               :              :     <font color="blue">⬛</font> = "2D" rendering happens here
: └─┴─────────┘        └─┴─────────┘              :               :              :     <font color="red">⬛</font> = "3D" rendering happens here
···················································               ················

```

*Advantages of this set-up, compared to using [VirtualGL with X11 Forwarding](#Using_VirtualGL_with_X11_forwarding):*

*   can maintain better performance in case of low-bandwidth/high-latency networks
*   can send the same image stream to multiple clients ("desktop sharing")
*   the remote application can continue running even when the network connection drops
*   better support for non-Linux clients, as the architecture does not depend on a client-side X server

### Instructions

After setting up VirtualGL on the remote server [as described above](#Installation_and_setup), and establishing a working remote desktop connection using the [VNC client/server](/index.php/Vncserver "Vncserver") implementation of your choice, no further configuration should be needed.

Inside the VNC session (e.g. in a terminal emulator within the VNC desktop or even directly in `~/.vnc/xstartup`), simply run selected applications with `vglrun` as described in [Running Applications](#Running_applications) below.

You can also run your entire session with `vglrun`, so that all opengl applications work by default. For example, if you use xfce, you can run `vglrun startxfce4` instead of `startxfce4` in your X startup scripts (`~/.vnc/xstartup`, `.xinitrc` or equivalent), or copy and edit a .desktop file in /usr/share/xsessions if you're using a display manager.

### Choosing an appropriate VNC package

VirtualGL can provide 3D rendering for *any* general-purpose [vncserver](/index.php/Vncserver "Vncserver") implementation (e.g. TightVNC, RealVNC, ...).

However, if you want to really get good performance out of it *(e.g. to make it viable to watch videos or play OpenGL games over VNC)*, you might want to use one of the VNC implementations that are specifically optimized for this use-case:

*   [turbovnc](https://aur.archlinux.org/packages/turbovnc/): Developed by the same team as VirtualGL, with the explicit goal of providing the best performance in combination with it. However, its vncserver implementation does not support all features a normal Xorg server provides, thus *some* applications will run unusually slow or not at all in it.
*   [TigerVNC](/index.php/TigerVNC "TigerVNC"): Also developed with VirtualGL in mind and achieves good performance with it, while providing better Xorg compatibility than TurboVNC.

## Running applications

Once you have set up your remote desktop connection with VirtualGL support, you can use `vglrun` to run selected applications with VirtualGL-accelerated rendering of their OpenGL parts:

```
$ vglrun glxgears

```

This has to be executed on the remote computer of course (where the application will run), i.e. inside your SSH or VNC session. The X servers that will be used, are determined from the following two environment variables:

| `<font color="blue">DISPLAY</font>` | *The X server that will handle the application, and render its non-OpenGL parts.*

If using VNC, this refers to the VNC server. In the case of SSH forwarding, it is a virtual X server number on the remote computer that SSH internally maps to the real X server on the client. There is nothing VirtualGL-specific about this variable, and it will already be set to the correct value within your SSH or VNC session.

 |
| `<font color="red">VGL_DISPLAY</font>` | *The X server to which VirtualGL should redirect OpenGL rendering.*

See [Installation and setup](#Installation_and_setup) above. If not set, the value `:0.0` is assumed. Note that the number after the dot can be used to select the graphics card.

 |

Many more environment variables and command-line parameters are available to fine-tune `vglrun` - refer to the user manual and `vglrun -help` for reference. VirtualGL's behavior furthermore depends on which of its two main modes of operation is active (which `vglrun` will choose automatically, based on the environment in which it is executed):

*   *"**VGL Transport**" - default when [using X11 forwarding](#Using_VirtualGL_with_X11_forwarding)*

	In this mode, a compressed image stream of the rendered OpenGL scenes is sent through a custom network protocol to a `vglclient` instance. By default it uses JPEG compression at 90% quality, but this can be fully customized, e.g.:

	 `$ vglrun -q 30 -samp 4x glxgears              *# use aggressive compression (to reduce bandwidth demand)*` 

	 `$ VGL_QUAL=30 VGL_SUBSAMP=4x vglrun glxgears  *# same as above, using environment variables*` 

	There is also a GUI dialog that lets you change the most common VirtualGL rendering/compression options for an application on the fly, after you have already started it with `vglrun` - simply press `Ctrl+Shift+F9` while the application has keyboard focus, to open this dialog.

*   *"**X11 Transport**" - default when [using VNC](#Using_VirtualGL_with_VNC)*

	In this mode, VirtualGL feeds raw (uncompressed) images through the normal X11 protocol directly to the X server that handles the application - e.g. a VNC server running on the same machine. Many of `vglrun`'s command-line options (e.g. those relating to image stream compression or stereo rendering) are not applicable here, because there is no `vglclient` running on the other end. It is now the VNC server that handles all the image stream optimization/compression, so it is there that you should turn to for fine-tuning.

**Tip:** `vglrun` is actually just a shell script that (temporarily) sets some environment variables before running the requested application - most importantly it adds the libraries that provide all the VirtualGL functionality to `LD_PRELOAD`. If it better suits your workflow, you could just set those variables yourself instead. The following command lists all environment variables that vglrun would set for your particular set-up: `comm -1 -3 <(env | sort) <(vglrun env | grep -v '^\[' | sort)` 

### Confirming that VirtualGL rendering is active

If you set the `VGL_LOGO` environment variable before starting an application, a small logo reading "VGL" will be shown in the bottom-right corner of any OpenGL scene that is rendered through VirtualGL in that application:

```
$ VGL_LOGO=1 vglrun glxgears

```

If the application runs but the logo does not appear, it means VirtualGL has failed to take effect (see [#Troubleshooting](#Troubleshooting) below) and the application has probably fallen back to software rendering.

### Measuring performance

Many OpenGL programs or games can display an embedded FPS ("frames per second") counter - however when using VirtualGL these values will not be very useful, as they merely measure the rate at which frames are rendered on the server side (through the 3D-capable X server), not the rate at which frames actually end up being rendered on the client side.

The "Performance Measurement" chapter of the user manual describes how to get a measurement of the throughput at various stages of the VirtualGL image pipeline, and how to identify bottlenecks (especially when using VirtualGL with X11 forwarding). When using VNC, the VNC client should be able to tell you its rendering frame-rate as well.

## Troubleshooting

**Tip:** Running `vglrun` with the `+v` command-line switch (or environment variable `VGL_VERBOSE=1`) makes VirtualGL print out some details about its attempt to initialize rendering for the application in question. The `+tr` switch (or variable `VGL_TRACE=1`) will make it print out lots of live info on intercepted OpenGL function calls during the actual rendering. By default VirtualGL prints all its debug output to the shell - if you want to separate it from the application's own STDERR output you can set `VGL_LOG=/tmp/virtualgl-$USER.log`.

### Problem: vglrun aborts with "Could not open display"

If `vglrun` exits with an error messages like...

```
[VGL] ERROR: Could not open display :0.

```

...in the shell output, then this means that the 3D-capable X server on the server side (that is supposed to handle the OpenGL rendering) is either not running, or not properly set up for use with VirtualGL (see [Installation and setup](#Installation_and_setup)), or `VGL_DISPLAY` is not set correctly (see [Running Applications](#Running_applications)). If it used to work but not anymore, a package upgrade may have overwritten files modified by `vglserver_config`, so run that script again and then restart the server-side X server (e.g. `systemctl restart kdm`).

### Problem: vglrun seems to have no effect at all

Symptoms:

*   no VirtualGL-accelerated 3D rendering - the program either aborts, or falls back to software rendering ([how to check](#Confirming_that_VirtualGL_rendering_is_active))
*   at the same time, *no* VirtualGL related error messages or info is printed to the shell

This may happen when something blocks VirtualGL from getting preloaded into the application's executable(s). The way pre-loading works, is that `vglrun` adds the names of some VirtualGL libraries to the `LD_PRELOAD` environment variable before running the command that starts the application. Now when an application binary is executed as part of this command, the Linux kernel loads the dynamic linker which in turn detects the `LD_PRELOAD` variable and links the specified libraries into the in-memory copy of the application binary before anything else. This will obviously not work if the environment variable is not propagated to the dynamic linker, e.g. in the following cases:

*   **The application is started through a script that explicitly unsets/overrides LD_PRELOAD**

	*Solution:* Edit the script to comment out or fix the offending line. (You can put the modified script in `/usr/local/bin/` to prevent it from being reverted on the next package upgrade.)

*   **The application is started through multiple layers of scripts, and environment variables get lost along the way**

	*Solution:* Modify the final script that actually runs the application, to make it run the application with `vglrun`.

*   **The application is started through a loader binary *(possibly itself!)*, in a way that fails to propagate LD_PRELOAD**

	*Solution:* If possible, bypass the loader binary and start the actual OpenGL application directly with `vglrun` - an example is VirtualBox where you need to start your virtual machine session directly with `vglrun VirtualBox -startvm "Name of the VM"` rather then through the VirtualBox main program GUI. If it is a matter of LD_PRELOAD being explicitly unset within the binary, running `vglrun` with the `-ge` command-line switch can prevent that in some cases.

See the "Application Recipes" section in the user manual for a list of some applications that are known to require such work-arounds.

### Problem: vglrun fails with ld.so errors

If VirtualGL-accelerated 3D rendering does not work (like with the previous section), but in addition you see error messages like...

```
ERROR: ld.so: object 'libdlfaker.so' from LD_PRELOAD cannot be preloaded: ignored.
ERROR: ld.so: object 'librrfaker.so' from LD_PRELOAD cannot be preloaded: ignored.

```

...in the shell output, then the dynamic linker is correctly receiving instructions to preload the VirtualGL libraries into the application, but something prevents it from successfully performing this task. Two possible causes are:

*   **The VirtualGL libraries for the correct architecture are not installed**

	If you are using a 64-bit Arch Linux system and want to run a 32-bit application (like [Wine](/index.php/Wine "Wine")) with VirtualGL, you need to install [lib32-virtualgl](https://www.archlinux.org/packages/?name=lib32-virtualgl) from the [[multilib]](/index.php/Multilib "Multilib") repository.

*   **The application executable has the setuid/setgid flag set**

	You can confirm whether this is the case by inspecting the executable's file permissions using `ls -l`: It will show the letter `s` in place of the *user executable* bit if setuid is set (for example `-rw**s**r-xr-x`), and in place of the *group executable* bit if setgid is set. For such an application any preloading attempts will fail, unless the libraries to be preloaded have the setuid flag set as well. You can set this flag for the VirtualGL libraries in question by executing the following as root:

```
$ chmod u+s /usr/lib/lib{rr,dl}faker.so    # for the native-architecture versions provided by [virtualgl](https://www.archlinux.org/packages/?name=virtualgl)
$ chmod u+s /usr/lib32/lib{rr,dl}faker.so  # for the multilib versions provided by [lib32-virtualgl](https://www.archlinux.org/packages/?name=lib32-virtualgl)

```

	However, make sure you fully understand the security implications of [setuid](https://en.wikipedia.org/wiki/Setuid "wikipedia:Setuid") before deciding to do this in a server environment where security is critical.

### Problem: vglrun fails with ERROR: Could not connect to VGL client.

If your 'client' program is running on the same server as virtualGL (e.g. if you're using virtualGL for VNC), try using `vglrun -c proxy`.

### Problem: Error messages about /etc/opt/VirtualGL/vgl_xauth_key not existing

This means that `vglgenkey` is either not being run at all for your virtualGL X server, or that it is being run again by another X server. For me, lightdm was running `vglgenkey` on the wrong (vnc remote) X servers, because `vglserver_config` adds the following:

 `/etc/lightdm/lightdm.conf` 
```
...
[Seat:*]
display-setup-script=/usr/bin/vglgenkey

```

Changing it to

 `/etc/lightdm/lightdm.conf` 
```
...
[Seat:seat0]
display-setup-script=/usr/bin/vglgenkey

```

so it only runs on the first X server fixed my problem.

### Problem: rendering glitches, unusually poor performance, or application errors

OpenGL has a really low-level and flexible API, which means that different OpenGL applications may come up with very different rendering techniques. VirtualGL's default strategy for how to redirect rendering and how/when to capture a new frame works well with most interactive 3D programs, but may prove inefficient or even problematic for *some* applications. If you suspect that this may be the case, you can tweak VirtualGL's mode of operation by setting certain environment variables before starting your application with `vglrun`. For example you could try setting some of the following values *(try them one at a time, and be aware that each of them could also make things worse!)*:

```
VGL_ALLOWINDIRECT=1
VGL_FORCEALPHA=1
VGL_GLFLUSHTRIGGER=0
VGL_READBACK=pbo
VGL_SPOILLAST=0
VGL_SYNC=1  # use VNC with this one, it is very slow with X11 forwarding

```

A few OpenGL applications also make strong assumptions about their X server environment or loaded libraries, that may not be fulfilled by a VirtualGL set-up - thus causing those applications to fail. The environment variables `VGL_DEFAULTFBCONFIG`, `VGL_GLLIB`, `VGL_TRAPX11`, `VGL_X11LIB`, `VGL_XVENDOR` can be used to fix this in some cases.

See the "Advanced Configuration" section in the user manual for a proper explanation of all supported environment variables, and the "Application Recipes" section for info on some specific applications that are known to require tweaking to work well with VirtualGL.

## See also

*   [VirtualGL Online Documentation](http://www.virtualgl.org/Documentation/Documentation) (you can also find it at `/usr/share/doc/virtualgl/index.html` if you have [virtualgl](https://www.archlinux.org/packages/?name=virtualgl) installed)