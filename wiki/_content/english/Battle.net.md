## Contents

*   [1 Installation](#Installation)
    *   [1.1 Packages](#Packages)
*   [2 Wine Config](#Wine_Config)
*   [3 Known Issues](#Known_Issues)
    *   [3.1 Crash when some game load](#Crash_when_some_game_load)
    *   [3.2 Login Region Select](#Login_Region_Select)
    *   [3.3 White Flashing](#White_Flashing)

## Installation

### Packages

You need to install [wine](/index.php/Wine "Wine"), [winetricks](https://www.archlinux.org/packages/?name=winetricks), and [lib32-libldap](https://www.archlinux.org/packages/?name=lib32-libldap)

From winetricks, install:

```
$ winetricks corefonts vcrun2005 vcrun2008 vcrun2015

```

## Wine Config

The Battle.net client must be ran as Windows Version 'Windows XP'. Other versions will result in the client being a blank white window.

## Known Issues

### Crash when some game load

If you got this error 'api-ms-win-crt-math-l1-1-0.dll._except1', it's caused by a bug about winetricks: he tried to override vcrun2015 math library, but the filename is wrong. In order to fix it, change the line of '/usr/bin/winetricks' with this patch: [https://github.com/boltronics/winetricks/commit/7bd342522d4f59c4416580decf53f4a97623214e](https://github.com/boltronics/winetricks/commit/7bd342522d4f59c4416580decf53f4a97623214e)

### Login Region Select

When logging in, you must move the mouse over where the dropdown would be for 'Region Select' - otherwise it does not show up.

### White Flashing

The client often flashes when the window is moved, or other windows are moved over it. This should not affect the running of the app.