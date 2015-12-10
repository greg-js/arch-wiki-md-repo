# Comparison of tiling window managers

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

This article provides an unbiased comparison of the most popular _tiling_ [window managers](/index.php/Window_manager "Window manager") (as opposed to _floating_ window managers).

## Contents

*   [1 Comparison table](#Comparison_table)
    *   [1.1 Management style](#Management_style)
    *   [1.2 Layouts](#Layouts)
    *   [1.3 Key bindings](#Key_bindings)
*   [2 External links](#External_links)

## Comparison table

The following table lists the most popular tiling window managers alongside notable features, providing readers with a quick overview.

<table class="wikitable sortable"><caption>Comparison of tiling window managers</caption>

<tbody>

<tr>

<th scope="col">Window Manager</th>

<th scope="col">Written in</th>

<th scope="col">Configured with</th>

<th scope="col">Management style</th>

<th scope="col">System tray support</th>

<th scope="col">On-the-fly reload</th>

<th scope="col" class="unsortable">Information bars</th>

<th scope="col">Compositing</th>

<th scope="col" class="unsortable">Default layouts</th>

<th scope="col" class="unsortable">Pixel usage</th>

<th scope="col" class="unsortable">External control</th>

<th scope="col">Library</th>

<th scope="col" class="unsortable">Multiple (n) monitor behavior</th>

<th scope="col">ICCCM/EWMH compliant</th>

<th scope="col">Maintenance</th>

</tr>

<tr>

<th>[alopex](/index.php/Alopex "Alopex")</th>

<td>C</td>

<td>C (recompile)</td>

<td>Hybrid</td>

<td>None</td>

<td>No</td>

<td>Built-in; call script/program as first argument</td>

<td>external</td>

<td>max, h-stack, v-stack, h-tab</td>

<td>Variable borders; titles in-statusbar</td>

<td>Xlib</td>

<td>six tags, two views available by default</td>

<td>active</td>

</tr>

<tr>

<th>[Awesome](/index.php/Awesome "Awesome")</th>

<td>C</td>

<td>Lua</td>

<td>Dynamic</td>

<td>Built-in</td>

<td>Yes</td>

<td>Built-in, images and text</td>

<td>external</td>

<td>max, nh-stack (and invert), nv-stack (and invert), free</td>

<td>variable borders, optional h-tab titles</td>

<td>dbus (if enabled)</td>

<td>XCB</td>

<td>n-tags (workspaces). Per default 9 are enabled. [Example](https://awesome.naquadah.org/images/6mon.medium.png)</td>

<td>Yes</td>

<td>Active</td>

</tr>

<tr>

<th>[bspwm](/index.php/Bspwm "Bspwm")</th>

<td>C</td>

<td>Anything</td>

<td>Hybrid</td>

<td>None</td>

<td>Yes</td>

<td>Can write internal state to a FIFO</td>

<td>External</td>

<td>v-split, h-split</td>

<td>Variable borders</td>

<td>via `bspc`</td>

<td>XCB</td>

<td>Monitors hold Desktops</td>

<td>Yes</td>

<td>Active</td>

</tr>

<tr>

<th>[catwm](/index.php/Catwm "Catwm")</th>

<td>C</td>

<td>C (recompile)</td>

<td>Dynamic</td>

<td>None</td>

<td>No</td>

<td>None</td>

<td>No</td>

<td>v-stack, max</td>

<td>1-pix borders</td>

<td>Xlib</td>

<td>Abandoned</td>

</tr>

<tr>

<th>dswm</th>

<td>Lisp</td>

<td>Lisp</td>

<td>Manual</td>

<td>None</td>

<td>Yes</td>

<td>Yes</td>

<td>No</td>

<td>Active</td>

</tr>

<tr>

<th>[dwm](/index.php/Dwm "Dwm")</th>

<td>C</td>

<td>C (recompile)</td>

<td>Dynamic</td>

<td>Optional Patch</td>

<td>[Optional](/index.php/Dwm#Restart_dwm_without_logging_out_or_closing_programs "Dwm")</td>

<td>Built-in, reads from root window name</td>

<td>external</td>

<td>v-stack, max</td>

<td>Xlib</td>

<td>n regions, 9 workspaces fixed to each region</td>

<td>Active</td>

</tr>

<tr>

<th>[echinus](/index.php/Echinus "Echinus")</th>

<td>C</td>

<td>Text</td>

<td>Dynamic</td>

<td>None</td>

<td>Yes</td>

<td>[ourico](https://aur.archlinux.org/packages/ourico/)<sup><small>AUR</small></sup></td>

<td>external</td>

<td>v-stack, b-stack, max</td>

<td>Variable borders & optional titles</td>

<td>Xlib</td>

<td>Yes</td>

<td>Unknown</td>

</tr>

<tr>

<th>euclid-wm</th>

<td>C</td>

<td>Text</td>

<td>Hybrid</td>

<td>None</td>

<td>Yes</td>

<td>External ([dzen](/index.php/Dzen "Dzen"))</td>

<td>rows, columns</td>

<td>1-pix borders</td>

<td>Xlib</td>

<td>Dormant</td>

</tr>

<tr>

<th>[FrankenWM](/index.php/FrankenWM "FrankenWM")</th>

<td>C</td>

<td>C (recompile)</td>

<td>Dynamic</td>

<td>None</td>

<td>No</td>

<td>No, outputs information to stdout, which can easily be parsed and displayed by an external monitor or panel (dzen2, conky, etc)</td>

<td>external</td>

<td>v-stack (and invert), h-stack (and invert), dual-v/h-stack, grid, fibonacci (vh-stack), rows, columns, max, free</td>

<td>Variable borders</td>

<td>XCB</td>

<td>Active</td>

</tr>

<tr>

<th>[herbstluftwm](/index.php/Herbstluftwm "Herbstluftwm")</th>

<td>C</td>

<td>Text</td>

<td>Manual</td>

<td>None</td>

<td>Yes</td>

<td>rows, columns</td>

<td>1-pix borders</td>

<td>commands via herbstclient</td>

<td>Xlib and Glib</td>

<td>n regions, 9 workspaces visible in any region</td>

<td>Active</td>

</tr>

<tr>

<th>[i3](/index.php/I3 "I3")</th>

<td>C</td>

<td>Text</td>

<td>Dynamic</td>

<td>i3bar</td>

<td>Yes (Layout is preserved)</td>

<td>text piped to i3bar (`i3status`/`conky` and others can be used)</td>

<td>external</td>

<td>tree, v-split, h-split, stacked, tabbed, max, can be nested infinitely</td>

<td>none, 1-pix or 2-pix, optional titlebars, can hide edge borders</td>

<td>commands via ipc (or i3-msg, which uses ipc)</td>

<td>XCB</td>

<td>n regions</td>

<td>Yes</td>

<td>Active</td>

</tr>

<tr>

<th>[Ion3](/index.php/Ion3 "Ion3")</th>

<td>C</td>

<td>Lua</td>

<td>Manual</td>

<td>trayion</td>

<td>Yes</td>

<td>configurable</td>

<td> ?</td>

<td>h-tab, max</td>

<td>Abandoned</td>

</tr>

<tr>

<th>[monsterwm](/index.php/Monsterwm "Monsterwm")</th>

<td>C</td>

<td>C (recompile)</td>

<td>Dynamic</td>

<td>None</td>

<td>Optional, but windows are lost</td>

<td>No, outputs information to stdout, which can easily be parsed and displayed by an external monitor or panel (`dzen2`, `conky`, etc)</td>

<td>external</td>

<td>h-stack, v-stack, grid, max</td>

<td>supports `_NET_ACTIVE_WINDOW`, so external control can be supplied by `xdotool` and similar tools</td>

<td>[Xlib primary and XCB fork](/index.php/Monsterwm#Installation "Monsterwm")</td>

<td>n workspaces per monitor</td>

<td>Active</td>

</tr>

<tr>

<th>[Musca](/index.php/Musca "Musca")</th>

<td>C</td>

<td>Text, own command set, C(recompile)</td>

<td>Manual</td>

<td>None</td>

<td>No, but allows running of musca commands on the fly</td>

<td>None</td>

<td>No</td>

<td>h-split, v-split, max</td>

<td>commands, hooks</td>

<td>Xlib</td>

<td>Abandoned</td>

</tr>

<tr>

<th>[Notion](/index.php/Notion "Notion")</th>

<td>C, Lua</td>

<td>Lua, compatible with Ion3 configs</td>

<td>Manual</td>

<td>trayion, stalonetray</td>

<td>Yes</td>

<td>configurable</td>

<td> ?</td>

<td>h-tab, max</td>

<td>Configurable borders and titlebars/tabs</td>

<td>EWMH, arbitrary Lua scripts which have access to the rich internal API</td>

<td>Xlib</td>

<td>n workspaces on each monitor. Supports on-the-fly changes in topology</td>

<td>Active</td>

</tr>

<tr>

<th>[qtile](/index.php/Qtile "Qtile")</th>

<td>Python</td>

<td>Python</td>

<td>Dynamic</td>

<td>Yes</td>

<td>Yes</td>

<td>Yes</td>

<td>external</td>

<td>tree, v-split, h-split, stacked, tabbed, max</td>

<td>No borders, although customizable</td>

<td>Hooks, Server mode</td>

<td>XCB</td>

<td>Active</td>

</tr>

<tr>

<th>[Ratpoison](/index.php/Ratpoison "Ratpoison")</th>

<td>C</td>

<td>Text</td>

<td>Manual</td>

<td>None</td>

<td>Yes</td>

<td>Yes</td>

<td>external</td>

<td>max</td>

<td>No</td>

<td>Active</td>

</tr>

<tr>

<th>[Snapwm](/index.php/Snapwm "Snapwm")</th>

<td>C</td>

<td>Reloadable Text</td>

<td>Dynamic</td>

<td>None</td>

<td>Yes</td>

<td>Built-in, reads from root window name</td>

<td>External</td>

<td>nVertical, Fullscreen, nHorizontal, Grid, Center Stacking</td>

<td>variable borders, no titles</td>

<td>Xlib</td>

<td>Number of desktops distributed evenly between monitors</td>

<td>Active</td>

</tr>

<tr>

<th>[Spectrwm](/index.php/Spectrwm "Spectrwm")</th>

<td>C</td>

<td>Text</td>

<td>Dynamic</td>

<td>None</td>

<td>Yes</td>

<td>Built-in, reads from user script</td>

<td>No</td>

<td>nv-stack, nh-stack, max</td>

<td>1-pix borders, no titles</td>

<td>XCB</td>

<td>n regions, 10 workspaces visible in any region</td>

<td>Yes</td>

<td>Active</td>

</tr>

<tr>

<th>[Stumpwm](/index.php/Stumpwm "Stumpwm")</th>

<td>Lisp</td>

<td>Lisp</td>

<td>Manual</td>

<td>None</td>

<td>Yes</td>

<td>Yes</td>

<td>No</td>

<td>No</td>

<td>Active</td>

</tr>

<tr>

<th>[subtle](/index.php/Subtle "Subtle")</th>

<td>C</td>

<td>Ruby</td>

<td>Manual</td>

<td>Built-in</td>

<td>Yes</td>

<td>Built-in (Ruby), external can be used as well</td>

<td>external</td>

<td>Variable grid</td>

<td>Variable borders, no titles</td>

<td>Hooks (Ruby), subtler (CLI), subtlext (Ruby extension)</td>

<td>Xlib</td>

<td>One workspace (view) per monitor (screen), placement on views via tags and per runtime</td>

<td>Yes</td>

<td>Active</td>

</tr>

<tr>

<th>[Wingo](/index.php/Wingo "Wingo")</th>

<td>Go</td>

<td>Text</td>

<td>Dynamic</td>

<td>None</td>

<td>Yes</td>

<td>No</td>

<td>external</td>

<td>floating, nv-stack, nh-stack, max</td>

<td>title bars in floating, skinny borders in tiling</td>

<td>via [wingo-cmd](https://github.com/BurntSushi/wingo/blob/master/HOWTO-COMMANDS) or UNIX sockets in any programming language</td>

<td>[X Go Binding](https://github.com/BurntSushi/xgb)</td>

<td>n regions, workspaces visible in any region</td>

<td>Yes</td>

<td>Active</td>

</tr>

<tr>

<th>[WMFS](/index.php/WMFS "WMFS")</th>

<td>C</td>

<td>Text</td>

<td>Dynamic</td>

<td>Built-in</td>

<td>Yes</td>

<td>Built-in, set with command, color text, images</td>

<td>external</td>

<td>nh-stack (and invert), nv-stack (and invert), mirror-v, mirror-h, grid, free, max</td>

<td>variable borders, titles or no titles</td>

<td>commands</td>

<td>Xlib</td>

<td>Up to 36 tags(workspaces) per screen</td>

<td>Yes</td>

<td>Active</td>

</tr>

<tr>

<th>[wmii](/index.php/Wmii "Wmii")</th>

<td>C</td>

<td>Anything</td>

<td>Manual</td>

<td>witray</td>

<td>Yes</td>

<td>Built-in</td>

<td>external</td>

<td>columns, max, v-tab</td>

<td>titles</td>

<td>[9P filesystem](http://9p.cat-v.org)</td>

<td>one big region</td>

<td>Yes</td>

<td>active</td>

</tr>

<tr>

<th>[xmonad](/index.php/Xmonad "Xmonad")</th>

<td>Haskell</td>

<td>Haskell</td>

<td>Dynamic</td>

<td>None</td>

<td>Yes</td>

<td>No</td>

<td>Yes, with xmonad-contrib and an external manager</td>

<td>nv-stack, nh-stack, max</td>

<td>variable borders, no titles</td>

<td>via [XMonad-Hooks-ServerMode](http://xmonad.org/xmonad-docs/xmonad-contrib/XMonad-Hooks-ServerMode.html)</td>

<td>Xlib</td>

<td>n regions, 9 workspaces visible in any region</td>

<td>Yes / ?</td>

<td>Active</td>

</tr>

<tr class="sortbottom">

<th>Window Manager</th>

<th>Written in</th>

<th>Configured with</th>

<th>Management style</th>

<th>System tray support</th>

<th>On-the-fly reload</th>

<th>Information bars</th>

<th>Compositing</th>

<th>Default layouts</th>

<th>Pixel usage</th>

<th>External control</th>

<th>Library</th>

<th>Multiple (n) monitor behavior</th>

<th>ICCCM/EWMH compliant</th>

<th>Maintenance</th>

</tr>

</tbody>

</table>

**Tip:** External control can also be achieved by programs like [xdotool](https://www.archlinux.org/packages/?name=xdotool) which simulate keystrokes.

### Management style

Dynamic management emphasizes automatic management of window layouts for speed and simplicity. Manual management emphasizes manual adjustment of layout and sizing with potentially more precise control, at the cost of more time spent moving and sizing windows.

### Layouts

A number of common layout types appear in several tiling WMs, although the terminology varies somewhat.

*   max: one window shown fullscreen (with or without a status bar, title and borders). Aka: monocle (dwm, monsterwm).
*   h-stack: master area in top half, other windows stack up horizontally in the bottom half. The master area may be resizable. May be inverted top-bottom (wmfs). Aka: bottom stack (dwm), bstack(monsterwm).
*   v-stack: master area in left half, other windows stack up vertically in the right half. The master area may be resizable. May be inverted left-right (wmfs). Aka: tile (dwm, monsterwm).
*   nh-stack: h-stack allowing >=1 windows in master area. Aka: nbstack (dwm)
*   nv-stack: v-stack allowing >=1 windows in master area. Aka: ntile (dwm)
*   mirror-h: nh-stack with stacks above and below the master area
*   mirror-v: nv-stack with stacks to the left and right of the master area
*   h-tab: one window shown fullscreen with all window titles shown horizontally (like browser tabs)
*   v-tab: one window shown fullscreen with all window titles shown vertically. Aka: stack (wmii).
*   h-split: a keybinding splits the current window horizontally creating space for another
*   v-split: a keybinding splits the current window horizontally creating space for another
*   columns: manual layout style which treats windows as belonging to vertical columns
*   rows: manual layout style which treats windows as belonging to horizontal rows
*   grid: window positions and sizes based on a regular NxM grid. May be automatic (like wmfs, monsterwm) or manual (like Subtle).

### Key bindings

Tiling window managers are usually designed to be used entirely with the keyboard or with keyboard & mouse. This is for speed (reaching for and moving a mouse is slow) and ease of use. Sensible key bindings are crucial to making workflow fast and efficient. Some default sets are better than others, but generally the keys can be rebound as desired by the user.

## External links

*   [Comparison of extensible window managers](http://sawfish.wikia.com/wiki/Comparison_of_extensible_window_managers) compares WMs "extensible" by scripting, like Xmonad and Sawfish.

Retrieved from "[https://wiki.archlinux.org/index.php?title=Comparison_of_tiling_window_managers&oldid=399225](https://wiki.archlinux.org/index.php?title=Comparison_of_tiling_window_managers&oldid=399225)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [Tiling WMs](/index.php/Category:Tiling_WMs "Category:Tiling WMs")