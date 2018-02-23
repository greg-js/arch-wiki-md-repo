GoG supports only ubuntu and related distibutions, but with this fix it's possible to enjoy this game on Archlinux using opensource drivers.

After installation create a file `divos-hack.c` on `~/GOG Games/Divinity Original Sin Enhanced Edition/game/`, paste inside that file the following code:

 `~/GOG Games/Divinity Original Sin Enhanced Edition/game/divos-hack.c` 
```
/*
 * LD_PRELOAD shim which applies two patches necesary to get the game
 * Divinity: Original Sin Enhanded Edition for Linux to work with Mesa (12+)
 *
 * Build with: gcc -s -O2 -shared -fPIC -o divos-hack.{so,c} -ldl
 */

/* for RTLD_NEXT */
#ifndef _GNU_SOURCE
#define _GNU_SOURCE
#endif
#include <dlfcn.h>
#include <GL/gl.h>
#include <string.h>

#define _GLX_PUBLIC

/*
 *   [https://github.com/karolherbst/mesa/commit/aad2543bf6cfbd7df795d836e5ff4ec8686e4fdf](https://github.com/karolherbst/mesa/commit/aad2543bf6cfbd7df795d836e5ff4ec8686e4fdf)
 *     - allow env override of vendor string.  I actually just hard-coded
 *       ATI Technologies, Inc., since that appears to be what's needed
 */
const GLubyte *GLAPIENTRY glGetString( GLenum name )
{
    static void *next = NULL;
    static const char *vendor = "ATI Technologies, Inc.";
    if(name == GL_VENDOR)
	return (const GLubyte *)vendor;
    if(!next)
	next = dlsym(RTLD_NEXT, "glGetString");
    return ((const GLubyte *GLAPIENTRY (*)(GLenum))next)(name);
}

/*
 *   [https://gist.github.com/karolherbst/b279233f8b13c9db1f3e1e57c6ecfbd2](https://gist.github.com/karolherbst/b279233f8b13c9db1f3e1e57c6ecfbd2)
 */
_GLX_PUBLIC void (*glXGetProcAddressARB(const GLubyte * procName)) (void)
{
   static void *next = NULL;
   if (strcmp((const char *) procName, "glNamedStringARB") == 0
```
After that, compile it using this command: `# gcc -s -O2 -shared -fPIC -o divos-hack.{so,c} -ldl` 

Now, edit the file `runner.sh` with the following lines:

 `~/GOG Games/Divinity Original Sin Enhanced Edition/game/runner.sh` 
```
#!/bin/sh

#LD_LIBRARY_PATH="." ./EoCApp
MESA_GLSL_VERSION_OVERRIDE=420 MESA_GL_VERSION_OVERRIDE=4.2 allow_glsl_extension_directive_midshader=true LD_PRELOAD="./divos-hack.so" LD_LIBRARY_PATH="." ./EoCApp
# Restore resolution
xrandr --output eDP1 --mode 1920x1080 --rate 60
```

## External Links

[divos-hack.c on GitHub](https://gist.github.com/romanoaugusto88/eb6a2598fb10d1468da6f4497b0fa2de#file-divos-hack-c-L27)

[Divinity: Original Sin may soon work with Mesa drivers on Gaming on Linux](https://www.gamingonlinux.com/articles/divinity-original-sin-may-soon-work-with-mesa-drivers.8867/page=2)