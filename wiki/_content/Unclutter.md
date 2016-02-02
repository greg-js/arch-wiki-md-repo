# Unclutter

Unclutter hides your X mouse cursor when you do not need it, to prevent it from getting in the way. You have only to move the mouse to restore the mouse cursor. Unclutter is very useful in tiling window managers where you do not need the mouse often.

## Contents

*   [1 Installation](#Installation)
*   [2 Usage](#Usage)
*   [3 Known bugs](#Known_bugs)
    *   [3.1 Misbehaviour of the mouse cursor](#Misbehaviour_of_the_mouse_cursor)
*   [4 Alternatives](#Alternatives)
    *   [4.1 unclutter-xfixes](#unclutter-xfixes)
*   [5 See also](#See_also)

## Installation

[Install](/index.php/Install "Install") [unclutter](https://www.archlinux.org/packages/?name=unclutter) from the [official repositories](/index.php/Official_repositories "Official repositories") or the modern rewrite [unclutter-xfixes-git](https://aur.archlinux.org/packages/unclutter-xfixes-git/)<sup><small>AUR</small></sup> from the [AUR](/index.php/AUR "AUR").

## Usage

Use your _.xinitrc_ file or WM/DE to start unclutter. For example, add the following to your _.xinitrc_:

```
unclutter &

```

## Known bugs

### Misbehaviour of the mouse cursor

If you experience issues when using unclutter in conjunction with a tiling window manager (such as [xmonad](/index.php/Xmonad "Xmonad") or [i3](/index.php/I3 "I3")), install [unclutter-xfixes-git](https://aur.archlinux.org/packages/unclutter-xfixes-git/)<sup><small>AUR</small></sup> instead or use the `-grab` option:

```
unclutter -grab &

```

**Note:** The `-grab` option breaks some screen locking applications such as _slock_ and _i3lock_.

Unclutter could cause unusual mouse behaviour in some SDL Games. The mouse cursor might be reset to some positions in the screen because of this problem. The details can be found [here](https://bugs.launchpad.net/ubuntu/+source/unclutter/+bug/61105).

There are two known workarounds for this. You can either add `SDL_VIDEO_X11_DGAMOUSE=0` to your environment variables which does not work for all games or run unclutter with `-grab` option. However, it is important to note that the grab option may cause some applications such as gksu to not work properly.

## Alternatives

### unclutter-xfixes

Unclutter is a tool from the early 90s and has not been updated since. It works by creating fake windows or active pointer grabs, both of which often cause problems. By now, the X11 extensions Xinput2 and Xfixes have been released and are commonly found on most user systems. Using those, [unclutter-xfixes-git](https://aur.archlinux.org/packages/unclutter-xfixes-git/)<sup><small>AUR</small></sup> can provide the cursor hiding functionality without interfering with any application.

## See also

[http://linuxappfinder.com/package/unclutter](http://linuxappfinder.com/package/unclutter) - Unclutter on Linux App Finder

Retrieved from "[https://wiki.archlinux.org/index.php?title=Unclutter&oldid=412197](https://wiki.archlinux.org/index.php?title=Unclutter&oldid=412197)"