**Status de tradução:** Esse artigo é uma tradução de [Comparison of tiling window managers](/index.php/Comparison_of_tiling_window_managers "Comparison of tiling window managers"). Data da última tradução: 2019-10-08\. Você pode ajudar a sincronizar a tradução, se houver [alterações](https://wiki.archlinux.org/index.php?title=Comparison_of_tiling_window_managers&diff=0&oldid=581092) na versão em inglês.

Esse artigo fornece uma comparação imparcial dos [gerenciadores de janela](/index.php/Gerenciadores_de_janela "Gerenciadores de janela") *tiling* mais populares (diferentemente dos gerenciadores *flutuantes*).

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Tabela de comparação](#Tabela_de_comparação)
    *   [1.1 Estilo de gerenciamento](#Estilo_de_gerenciamento)
    *   [1.2 Layouts](#Layouts)
    *   [1.3 Associação de teclas](#Associação_de_teclas)
*   [2 Veja também](#Veja_também)

## Tabela de comparação

The following table lists the most popular tiling window managers alongside notable features, providing readers with a quick overview.

<caption>Comparison of tiling window managers</caption>
| Window Manager | Written in | Configured with | Management style | System tray support | On-the-fly reload | Information bars | Compositing | Default layouts | Pixel usage | External control | Library | Multiple (n) monitor behavior | ICCCM/EWMH compliant | Maintenance |
| [alopex](/index.php/Alopex "Alopex") | C | C (recompile) | Hybrid | None | No | Built-in; call script/program as first argument | External | max, h-stack, v-stack, h-tab | Variable borders, titles in-statusbar | Xlib | six tags, two views available by default | Active |
| [Awesome](/index.php/Awesome "Awesome") | C | Lua | Dynamic | Built-in | Yes | Built-in, images and text | External | max, nh-stack (and invert), nv-stack (and invert), free | Variable borders, optional h-tab titles | dbus (if enabled) | XCB | n-tags (workspaces). Per default 9 are enabled. [Example](https://awesome.naquadah.org/images/6mon.medium.png) | Yes | Active |
| [bspwm](/index.php/Bspwm "Bspwm") | C | Anything | Hybrid | None | Yes | Can write internal state to a FIFO | External | v-split, h-split | Variable borders | via `bspc` | XCB | Monitors hold Desktops | Yes | Active |
| [catwm](/index.php/Catwm "Catwm") | C | C (recompile) | Dynamic | None | No | None | No | v-stack, max | 1-pix borders | Xlib | Abandoned |
| dswm | Lisp | Lisp | Manual | None | Yes | Yes | No | Abandoned |
| [dwm](/index.php/Dwm "Dwm") | C | C (recompile) | Dynamic | Optional Patch | [Optional](/index.php/Dwm#Restart_dwm "Dwm") | Built-in, reads from root window name | External | v-stack, max | via [dwmfifo](https://dwm.suckless.org/patches/dwmfifo) | Xlib | n regions, 9 workspaces fixed to each region | Active |
| [echinus](/index.php/Echinus "Echinus") | C | Text | Dynamic | None | Yes | [ourico](https://aur.archlinux.org/packages/ourico/) | External | v-stack, b-stack, max | Variable borders, optional titles | Xlib | Yes | Unknown |
| euclid-wm | C | Text | Hybrid | None | Yes | External ([dzen](/index.php/Dzen "Dzen")) | rows, columns | 1-pix borders | Xlib | Dormant |
| [FrankenWM](/index.php/FrankenWM "FrankenWM") | C | C (recompile) | Dynamic | None | No | No, outputs information to stdout, which can easily be parsed and displayed by an external monitor or panel (dzen2, conky, etc) | External | v-stack (and invert), h-stack (and invert), dual-v/h-stack, grid, fibonacci (vh-stack), rows, columns, max, free | Variable borders | XCB | Active |
| [herbstluftwm](/index.php/Herbstluftwm "Herbstluftwm") | C | Text | Manual | None | Yes | rows, columns | 1-pix borders | commands via herbstclient | Xlib and Glib | n regions, 9 workspaces visible in any region | Active |
| [i3](/index.php/I3 "I3") | C | Text | Dynamic | i3bar | Yes (Layout is preserved) | text piped to i3bar (`i3status`/`conky` and others can be used) | External | tree, v-split, h-split, stacked, tabbed, max, can be nested infinitely | None, 1-pix or 2-pix, optional titlebars, can hide edge borders | commands via ipc (or i3-msg, which uses ipc) | XCB | n regions | Yes | Active |
| [Ion3](/index.php/Ion3 "Ion3") | C | Lua | Manual | trayion | Yes | configurable | ? | h-tab, max | Abandoned |
| LeftWM | Rust | toml (user settings) / Anything (themes) | Dynamic | None | Yes | Yes, many options through theme system | External | v-stack, columns, rows | Variable based on theme | supports `_NET_ACTIVE_WINDOW` and sending commands to a named pipe | Xlib | Workspaces and monitors are not tide. Many workspaces for monitor or many monitors for workspace | Yes | Active |
| monsterwm | C | C (recompile) | Dynamic | None | Optional, but windows are lost | No, outputs information to stdout, which can easily be parsed and displayed by an external monitor or panel (`dzen2`, `conky`, etc) | External | h-stack, v-stack, grid, max | supports `_NET_ACTIVE_WINDOW`, so external control can be supplied by `xdotool` and similar tools | Xlib primary and XCB fork | n workspaces per monitor | Abandoned |
| [Musca](/index.php/Musca "Musca") | C | Text, own command set, C(recompile) | Manual | None | No, but allows running of musca commands on the fly | None | No | h-split, v-split, max | commands, hooks | Xlib | Abandoned |
| [Notion](/index.php/Notion "Notion") | C, Lua | Lua, compatible with Ion3 configs | Manual | trayion, stalonetray | Yes | configurable | ? | h-tab, max | Configurable borders and titlebars/tabs | EWMH, arbitrary Lua scripts which have access to the rich internal API | Xlib | n workspaces on each monitor. Supports on-the-fly changes in topology | Active |
| [qtile](/index.php/Qtile "Qtile") | Python | Python | Dynamic | Yes | Yes | Yes | External | tree, v-split, h-split, stacked, tabbed, max | No borders, although customizable | Hooks, Server mode | XCB | Active |
| [Ratpoison](/index.php/Ratpoison "Ratpoison") | C | Text | Manual | None | Yes | Yes | External | max | No | Active |
| [Snapwm](/index.php/Snapwm "Snapwm") | C | Reloadable Text | Dynamic | None | Yes | Built-in, reads from root window name | External | nVertical, Fullscreen, nHorizontal, Grid, Center Stacking | Variable borders, no titles | Xlib | Number of desktops distributed evenly between monitors | Active |
| [Spectrwm](/index.php/Spectrwm "Spectrwm") | C | Text | Dynamic | None | Yes | Built-in, reads from user script | No | nv-stack, nh-stack, max | 1-pix borders, no titles | XCB | n regions, 10 workspaces visible in any region | Yes | Active |
| [Stumpwm](/index.php/Stumpwm "Stumpwm") | Lisp | Lisp | Manual | None | Yes | Yes | No | No | Active |
| [sway](/index.php/Sway "Sway") | C | Text (i3 compatible) | Dynamic | swaybar | Yes (Layout is preserved) | text piped to swaybar (`i3status`/`conky` and others can be used) | Yes | tree, v-split, h-split, stacked, tabbed, max, can be nested infinitely | None, 1-pix or 2-pix, optional titlebars, can hide edge borders | commands via ipc (or swaymsg, which uses ipc) | wlc (wayland) | n regions | No | Active |
| [subtle](/index.php/Subtle "Subtle") | C | Ruby | Manual | Built-in | Yes | Built-in (Ruby), external can be used as well | External | Variable grid | Variable borders, no titles | Hooks (Ruby), subtler (CLI), subtlext (Ruby extension) | Xlib | One workspace (view) per monitor (screen), placement on views via tags and per runtime | Yes | Active |
| [Wingo](/index.php/Wingo "Wingo") | Go | Text | Dynamic | None | Yes | No | External | floating, nv-stack, nh-stack, max | title bars in floating, skinny borders in tiling | via [wingo-cmd](https://github.com/BurntSushi/wingo/blob/master/HOWTO-COMMANDS) or UNIX sockets in any programming language | [X Go Binding](https://github.com/BurntSushi/xgb) | n regions, workspaces visible in any region | Yes | Active |
| [WMFS](/index.php/WMFS "WMFS") | C | Text | Dynamic | Built-in | Yes | Built-in, set with command, color text, images | External | nh-stack (and invert), nv-stack (and invert), mirror-v, mirror-h, grid, free, max | Variable borders, titles or no titles | commands | Xlib | Up to 36 tags(workspaces) per screen | Yes | Active |
| [wmii](/index.php/Wmii "Wmii") | C | Anything | Dynamic | witray | Yes | Built-in | External | columns, max, v-tab | titles | [9P filesystem](http://9p.cat-v.org) | one big region | Yes | Abandoned |
| [xmonad](/index.php/Xmonad "Xmonad") | Haskell | Haskell | Dynamic | None | Yes | No | Yes, with xmonad-contrib and an external manager | nv-stack, nh-stack, max | Variable borders, no titles | via [XMonad-Hooks-ServerMode](http://xmonad.org/xmonad-docs/xmonad-contrib/XMonad-Hooks-ServerMode.html) | Xlib | n regions, 9 workspaces visible in any region | Yes / ? | Active |
| Window Manager | Written in | Configured with | Management style | System tray support | On-the-fly reload | Information bars | Compositing | Default layouts | Pixel usage | External control | Library | Multiple (n) monitor behavior | ICCCM/EWMH compliant | Maintenance |

**Tip:** External control can also be achieved by programs like [xdotool](https://www.archlinux.org/packages/?name=xdotool) which simulate keystrokes.

### Estilo de gerenciamento

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
*   v-split: a keybinding splits the current window vertically creating space for another
*   columns: manual layout style which treats windows as belonging to vertical columns
*   rows: manual layout style which treats windows as belonging to horizontal rows
*   grid: window positions and sizes based on a regular NxM grid. May be automatic (like wmfs, monsterwm) or manual (like Subtle).

### Associação de teclas

Tiling window managers are usually designed to be used entirely with the keyboard or with keyboard & mouse. This is for speed (reaching for and moving a mouse is slow) and ease of use. Sensible key bindings are crucial to making workflow fast and efficient. Some default sets are better than others, but generally the keys can be rebound as desired by the user.

## Veja também

*   [Comparison of extensible window managers](http://sawfish.wikia.com/wiki/Comparison_of_extensible_window_managers) compares WMs "extensible" by scripting, like xmonad and Sawfish.