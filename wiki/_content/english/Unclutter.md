Unclutter hides your X mouse cursor when you do not need it, to prevent it from getting in the way. You have only to move the mouse to restore the mouse cursor. Unclutter is very useful in tiling window managers where you do not need the mouse often.

## Contents

*   [1 Installation](#Installation)
*   [2 Usage](#Usage)
*   [3 Known bugs](#Known_bugs)
    *   [3.1 Misbehaviour of the mouse cursor](#Misbehaviour_of_the_mouse_cursor)
*   [4 Alternatives](#Alternatives)
    *   [4.1 unclutter-xfixes](#unclutter-xfixes)
    *   [4.2 xbanish](#xbanish)
*   [5 See also](#See_also)

## Installation

[Install](/index.php/Install "Install") the [unclutter](https://www.archlinux.org/packages/?name=unclutter) package.

**Note:** Arch actually ships unclutter-xfixes instead of the original in this package.

## Usage

Use your *.xinitrc* file or WM/DE to start unclutter. For example, add the following to your *.xinitrc*:

```
unclutter &

```

## Known bugs

### Misbehaviour of the mouse cursor

If you experience issues when using unclutter in conjunction with a tiling window manager (such as [xmonad](/index.php/Xmonad "Xmonad") or [i3](/index.php/I3 "I3")), install [unclutter-xfixes-git](https://aur.archlinux.org/packages/unclutter-xfixes-git/) instead or use the `-grab` option:

```
unclutter -grab &

```

**Note:** The `-grab` option breaks some screen locking applications such as *slock* and *i3lock*.

Unclutter could cause unusual mouse behaviour in some SDL Games. The mouse cursor might be reset to some positions in the screen because of this problem. The details can be found [here](https://bugs.launchpad.net/ubuntu/+source/unclutter/+bug/61105).

There are two known workarounds for this. You can either add `SDL_VIDEO_X11_DGAMOUSE=0` to your environment variables which does not work for all games or run unclutter with `-grab` option. However, it is important to note that the grab option may cause some applications such as gksu to not work properly.

## Alternatives

### unclutter-xfixes

Unclutter is a tool from the early 90s and has not been updated since. It works by creating fake windows or active pointer grabs, both of which often cause problems. By now, the X11 extensions Xinput2 and Xfixes have been released and are commonly found on most user systems. Using those, [unclutter-xfixes-git](https://aur.archlinux.org/packages/unclutter-xfixes-git/) can provide the cursor hiding functionality without interfering with any application.

As of December 2018, community/unclutter will actually ship this rewrite instead of the original[[2]](https://github.com/Airblader/unclutter-xfixes/issues/33#issuecomment-446209712)[[3]](https://git.archlinux.org/svntogit/community.git/commit/trunk?h=packages/unclutter&id=e652764bc5e55caefd3cd0df886554d3c76253ee).

### xbanish

xbanish is another tool similar to unclutter, but works in a different way. Instead of using cursor movements, xbanish hides the cursor during typing. You can grab it on the AUR as [xbanish](https://aur.archlinux.org/packages/xbanish/) or [xbanish-git](https://aur.archlinux.org/packages/xbanish-git/).

## See also

[http://linuxappfinder.com/package/unclutter](http://linuxappfinder.com/package/unclutter) - Unclutter on Linux App Finder