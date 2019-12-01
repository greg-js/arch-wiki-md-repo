Following the [xterm automatic transparency guide](/index.php/Xterm_Automatic_Transparency "Xterm Automatic Transparency") it is possible to get per app window transparency, with just [xcompmgr](https://www.archlinux.org/packages/?name=xcompmgr), *or any other compositor*, and [transset-df](https://www.archlinux.org/packages/?name=transset-df) - just replace *xterm* with your program name:

```
xterm & sleep .8s && transset-df -a

```

For openbox key/mousebindings, use this inside your `rc.xml`:

```
<execute>sh -c 'xterm &amp; sleep .8s &amp;&amp; transset-df -a'</execute>

```

This article details how to achieve transparency *automatically* on an application-by-application basis.

While transparency assuredly makes your desktop look a little nicer, it has some practical usages as well. Specifically, with terminals and text editors. It can be useful to overlay them with some transparency when copying pieces of code, or reading from a manual. However, it can be distracting for use with things like a browser or an image viewer.

Usually, the case is that you can either make all windows transparent with xcompmgr, or make some special windows transparent for applications that support it natively (i.e., urxvt). There have also been numerous [tutorials](http://urukrama.wordpress.com/openbox-guide/#Transparency) on how to use transset-df to set transparency on individual windows, however, this requires that you manually set the transparency for each window that opens.

Adding [devilspie](http://burtonini.com/blog/computers/devilspie) to the mix however, will allow you to achieve per application transparency automatically.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
    *   [2.1 Finding the window](#Finding_the_window)
    *   [2.2 Matching different applications](#Matching_different_applications)
*   [3 Starting with X](#Starting_with_X)
*   [4 Advanced configuration](#Advanced_configuration)

## Installation

Firstly, you will need to make sure that [xcompmgr](https://www.archlinux.org/packages/?name=xcompmgr), [transset-df](https://www.archlinux.org/packages/?name=transset-df), and [devilspie](https://www.archlinux.org/packages/?name=devilspie) are installed. They are all available in the [official repositories](/index.php/Official_repositories "Official repositories"). Once installed, run *xcompmgr* (if you do not already have it running):

```
$ xcompmgr &

```

**Note:** You do not need to pass any arguments to it, but if you would like some other effects, check out the [Xcompmgr](/index.php/Xcompmgr "Xcompmgr") page. A fork of Xcompmgr available in the repositories, [compton](https://www.archlinux.org/packages/?name=compton), may provide a greater stability and less tearing issues.

## Configuration

Now that what you need is installed, we need to configure devilspie. Essentially, devilspie acts as a window matching utility. It runs as a daemon, and allows you to specify rules to match certain windows, which then provides the functionality to execute some command (usually pertaining to that window), much like Openbox's rc.xml, however, Openbox alone does not give us the power that we need in this case.

First, create an opacity.ds file in `~/.devilspie` (create that directory if it doesn't already exist):

```
$ mkdir -p ~/.devilspie
$ cd ~/.devilspie
$ touch opacity.ds

```

Now put something like the following in your opacity.ds file:

```
( if
( contains ( window_class ) "Gvim" )
( begin
( spawn_async (str "transset-df -i " (window_xid) " 0.85" ))
)
)

```

As you can see, the rule checks to see if the *window_class* contains the string "Gvim." If it does, it executes a command using the transset-df utility to lower the opacity to 0.85\. (Any value from 0 to 1 is valid- with the former being completely transparent, and the latter being completely opaque.) The key here is the availability of the *window_xid* variable, and thus, the power of devilspie in this example.

### Finding the window

The other trick here is knowing how to match the desired window. Sometimes you might want to use *application_name* instead of matching against *window_class*. It all depends on how devilspie reads the window information. To see how to identify your window, run this in a terminal:

```
$ devilspie -a

```

And then *start* your desired application. The terminal should output some identification details that you can use in your opacity.ds file. Alternatively, you could use xprop.

### Matching different applications

While this will simply make GVim transparent, you might want to do this with more than one application. Here's an example configuration that makes all GVim, Mirage, and Chromium windows transparent. (Adding more windows should be apparent from this example.)

```
( if
( or
( contains ( window_class ) "Gvim" )
( contains ( application_name ) "mirage" )
( contains ( application_name ) "chrome" )
)
( begin
( spawn_async (str "transset-df -i " (window_xid) " 0.85" ))
)
)

```

## Starting with X

Simply place the following in your X startup script (i.e., `~/.xinitrc`) to have per application window transparency load:

```
xcompmgr &
devilspie -a &

```

## Advanced configuration

[Comprehensive documentation of the devilspie configuration file](http://foosel.org/linux/devilspie).

Alternatively, [gdevilspie](https://aur.archlinux.org/packages/gdevilspie/) is a GUI configuration editor for [devilspie](https://www.archlinux.org/packages/?name=devilspie).