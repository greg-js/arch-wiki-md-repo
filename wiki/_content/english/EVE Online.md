EVE Online is a space MMORPG game. It has no Linux client but the Windows client works through [Wine](/index.php/Wine "Wine").

## Contents

*   [1 Installation](#Installation)
*   [2 Troubleshooting](#Troubleshooting)
    *   [2.1 Performance](#Performance)
    *   [2.2 Wine errors and font incompatibilities](#Wine_errors_and_font_incompatibilities)

## Installation

Install Wine as described in [Wine](/index.php/Wine "Wine").

[Install](/index.php/Install "Install") the [lib32-libxml2](https://www.archlinux.org/packages/?name=lib32-libxml2) and [lib32-libldap](https://www.archlinux.org/packages/?name=lib32-libldap) packages.

In a fresh WINEPREFIX, follow the directions at [https://appdb.winehq.org/objectManager.php?sClass=version&iId=25823](https://appdb.winehq.org/objectManager.php?sClass=version&iId=25823) under "HOWTO - Eve Online install on Linux".

## Troubleshooting

### Performance

If you are on a multi-core processer and are experiencing occasional multi-second freezes, instead of running wine directly, add "taskset -c 0 wine ...". This forces the EVE process to stay on one of your cores, preventing very slow context switches (every 20-30 seconds). If you are not experiencing freezes, this will probably decrease performance, and is not recommended.

### Wine errors and font incompatibilities

Running the installer (several post-Rubicon versions tried) on wine-1.7.36 with the [ttf-ms-fonts](https://aur.archlinux.org/packages/ttf-ms-fonts/) package installed results in wine throwing "fixme:uniscribe:GSUB_apply_lookup We do not handle SubType 7" in a loop when trying to render the actual MS fonts on the installer, since the second installer page features an RTF/HTML-formatter EULA. This freezes the install process right after the first "Next >" button press. Uninstalling the [ttf-ms-fonts](https://aur.archlinux.org/packages/ttf-ms-fonts/) package then re-running the installer works fine as a workaround.