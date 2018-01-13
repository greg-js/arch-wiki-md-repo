[PAWM](https://sites.google.com/site/pleyadestest/david/projects/pawm) is an X11 stacking window manager. It is a very small, fast, and simple window manager. It is based on Xlib and needs no other external libraries to compile it. It provides an initial windowing environment for minimalist desktops or for single use purposes such as:

*   A web browser terminal computer.
*   Testing gui based programs.

PAWM was written by David Gómez and Raúl Núñez de Arenas Coronado. PAWM was written with the objective of creating a tiny window manager that would execute any X application, but still keep it simple and intuitive to use.

PAWM stands for *Puto Amo Window Manager*.

**Note:** It's unmaintained. Latest released version is 2.3.0.

## Contents

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
    *   [2.1 Icons](#Icons)
    *   [2.2 Application Launcher](#Application_Launcher)
        *   [2.2.1 Creating new Launcher files](#Creating_new_Launcher_files)
*   [3 Usage](#Usage)

## Installation

[Install](/index.php/Install "Install") the [pawm](https://aur.archlinux.org/packages/pawm/) package.

In order to run PAWM as your default window manager, edit the file `~/.xinitrc` (See [xinit](/index.php/Xinit "Xinit")) so the final line is:

```
exec pawm

```

## Configuration

By default, PAWM looks blue, plain and kind of dated. By editing the file `/etc/pawm.conf` you can customize the scheme of your PAWM.

Colors are changed through hexadecimal values. Fonts can be changed either through core fonts[wikipedia:X_logical_font_description](https://en.wikipedia.org/wiki/X_logical_font_description "wikipedia:X logical font description") or Xft fonts[[1]](http://www.x.org/archive/X11R6.8.2/doc/fonts.html).

You may also adjust adjust the behavior of pabar, paicons, pashut icon or any modules added.

### Icons

PAWM only supports [.xpm](https://en.wikipedia.org/wiki/X_PixMap "wikipedia:X PixMap") format. Programs like [GIMP](/index.php/GIMP "GIMP") can convert images appropriately.

*   Window icons must be 20x20 pixels.
*   Pashut icons must be 20x20 pixels.
*   Paicon icons may be of any size.

Any icons used in PAWM **must** be put in `/usr/share/pawm/icons/`

### Application Launcher

First, create a directory `~/.pawm` . This allows each user to have a unique application set.

There are 3 ways to launch programs in PAWM.

*   Add it to the `~/.xinitrc` file.
*   Execute the program from console with the **`-display`** paramater.
*   Use the PAWM application launcher

This article covers the third option.

#### Creating new Launcher files

Create a new file in the directory. For our example we will use the terminal emulator [Sakura](http://www.pleyades.net/david/sakura.php).

The filename must start with **app** with up to 20 characters after it.

```
appSakura

```

Then take your favorite file editor and open the file. The launcher apps have 4 lines that need editing.

1.  The name of the image you want to use.
2.  The initial icon screen position. As you move it, PAWM will edit the X Y coordinates accordingly.
3.  Icon text. This is optional.
4.  Application binary. This can be either relative or absolute path.

The finished file will look like this:

```
sakura.xpm
40 40
Sakura
sakura

```

When you next start PAWM your icons will be there. As well, any icon changes including position will be preserved.

## Usage

As PAWM is minimalistic, the controls are as well.

*   Double clicking a titlebar scrolls the window up or down respectively.
*   There are Minimize, Restore/Maximize, Close buttons.
*   You can drag windows around.
*   You can drag Launcher icons around.
*   Clicking on open applications on the PABar will minimize and restore.
*   Alt+Tab switches between windows.
*   Clicking on a Launcher executes the program.
*   Clicking on the power button brings up a dialog to quit PAWM.
*   Reloading PAWM refreshes any changes made.