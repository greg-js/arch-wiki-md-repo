Az [i3](http://i3wm.org/) egy dinamikus csempéző ablakkezelő ([tiling window manager](https://en.wikipedia.org/wiki/Tiling_window_manager "wikipedia:Tiling window manager")), amit a [wmii](/index.php/Wmii "Wmii") inspirált, legfőképp fejlesztőknek, és haladó felhasználóknak tervezve.

Az i3 céljai a letisztult dokumentáció, több monitor megfelelő támogatása, fa-struktúrájú ablakkezelés, és több mód, ahogyan a [vim](/index.php/Vim "Vim")-ben.

## Contents

*   [1 Telepítés](#Telep.C3.ADt.C3.A9s)
    *   [1.1 Display manager](#Display_manager)
    *   [1.2 xinitrc](#xinitrc)
*   [2 Használat](#Haszn.C3.A1lat)
    *   [2.1 Billentyűk](#Billenty.C5.B1k)
    *   [2.2 Tárolók](#T.C3.A1rol.C3.B3k)
    *   [2.3 Alkalmazásindító](#Alkalmaz.C3.A1sind.C3.ADt.C3.B3)
*   [3 Beállítás](#Be.C3.A1ll.C3.ADt.C3.A1s)
    *   [3.1 Konfiguráció varázsló és alternatív billentyűzetkiosztások](#Konfigur.C3.A1ci.C3.B3_var.C3.A1zsl.C3.B3_.C3.A9s_alternat.C3.ADv_billenty.C5.B1zetkioszt.C3.A1sok)
    *   [3.2 Színsémák](#Sz.C3.ADns.C3.A9m.C3.A1k)
    *   [3.3 i3bar](#i3bar)
        *   [3.3.1 i3bar alternatívák](#i3bar_alternat.C3.ADv.C3.A1k)
    *   [3.4 i3status](#i3status)
        *   [3.4.1 i3status helyettesítők](#i3status_helyettes.C3.ADt.C5.91k)
        *   [3.4.2 i3status wrapper-ek](#i3status_wrapper-ek)
        *   [3.4.3 Ikonszerű betűk az állapotsoron](#Ikonszer.C5.B1_bet.C5.B1k_az_.C3.A1llapotsoron)
    *   [3.5 Terminál emulátorok](#Termin.C3.A1l_emul.C3.A1torok)
*   [4 Tips and tricks](#Tips_and_tricks)
    *   [4.1 Advanced window navigation](#Advanced_window_navigation)
    *   [4.2 Jump to open window](#Jump_to_open_window)
    *   [4.3 Jump to urgent window](#Jump_to_urgent_window)
    *   [4.4 Save and restore the window layout](#Save_and_restore_the_window_layout)
        *   [4.4.1 Save the current window layout of a single workspace](#Save_the_current_window_layout_of_a_single_workspace)
        *   [4.4.2 Restore the window layout of the workspace](#Restore_the_window_layout_of_the_workspace)
    *   [4.5 Scratchpad containers](#Scratchpad_containers)
    *   [4.6 Screensaver and power management](#Screensaver_and_power_management)
    *   [4.7 Shutdown, reboot, lock screen](#Shutdown.2C_reboot.2C_lock_screen)
    *   [4.8 External displays manual management](#External_displays_manual_management)
    *   [4.9 Tabbed or stacked web-browsing](#Tabbed_or_stacked_web-browsing)
    *   [4.10 Workspace variables](#Workspace_variables)
    *   [4.11 Correct handling of floating dialogs](#Correct_handling_of_floating_dialogs)
    *   [4.12 Network Download/Upload speed on statusbar](#Network_Download.2FUpload_speed_on_statusbar)
*   [5 Patches](#Patches)
*   [6 Troubleshooting](#Troubleshooting)
    *   [6.1 General](#General)
    *   [6.2 Buttons in the i3 message bar do not work](#Buttons_in_the_i3_message_bar_do_not_work)
    *   [6.3 Faulty line wraps in tiled terminals](#Faulty_line_wraps_in_tiled_terminals)
    *   [6.4 Mouse cursor remains in waiting mode](#Mouse_cursor_remains_in_waiting_mode)
    *   [6.5 Unresponsive key bindings](#Unresponsive_key_bindings)
    *   [6.6 Tearing](#Tearing)
    *   [6.7 Tray icons not visible](#Tray_icons_not_visible)
*   [7 See also](#See_also)

## Telepítés

[Telepítsd](/index.php/Install "Install") az [i3](https://www.archlinux.org/groups/x86_64/i3/) [csoportot](/index.php/Pacman#Installing_package_groups "Pacman"). Ez tartalmazza az [i3-wm](https://www.archlinux.org/packages/?name=i3-wm) ablakkezelőt, az [i3status](https://www.archlinux.org/packages/?name=i3status)-t, ami rendszerinformációkat jelenít meg a [standard kimeneten](https://en.wikipedia.org/wiki/Standard_streams#Standard_output_.28stdout.29 "wikipedia:Standard streams") keresztül, és az [i3lock](https://www.archlinux.org/packages/?name=i3lock)-ot, egy képernyőzárat.

További csomagok az [Arch Felhasználói Tároló (AUR)](/index.php/Arch_User_Repository "Arch User Repository")-ban találhatóak. Lásd a [#Patch-ek](#Patch-ek) szakaszt példákért.

### Display manager

Az [i3-wm](https://www.archlinux.org/packages/?name=i3-wm) tartalmazza a `i3.desktop`-ot, ami [Xsession](/index.php/Xsession "Xsession")-ként indítja az ablakkezelőt. `i3-with-shmlog.desktop` engedélyezi a logokat (debugoláshoz hasznos). Az [i3-gnome](https://aur.archlinux.org/packages/i3-gnome/) integrálja az `i3`-at a [GNOME](/index.php/GNOME "GNOME")-ba.

### xinitrc

Add hozzá az [Xinitrc](/index.php/Xinitrc "Xinitrc")-hez a következőt:

```
exec i3

```

Ha az i3 kimenetét szeretnéd egy fájlban rögzíteni, akkor a következőt kell hozzáadni:

```
exec i3 -V >> ~/i3log-$(date +'%F-%k-%M-%S') 2>&1

```

## Használat

Lásd a [hivatalos dokumentációt](http://i3wm.org/docs) további információért, név szerint a [felhasználók kézikönyvét](http://i3wm.org/docs/userguide.html).

### Billentyűk

Az i3-ban a parancsok egy úgynevezett módosító billentyűvel hajthatók végre, ami `$mod`-ként lesz említve. Ez alapértelmezetten az `Alt` (Mod1), és a `Super` (Mod4) egy népszerű alternatíva. A Super billentyű a billentyűzeten Windows logóval jelölt billyentyű, vagy Apple billentyűzeten a Command billentyű.

Lásd az [i3 referencia kártyát](http://i3wm.org/docs/refcard.html) és az [i3 használatát](http://i3wm.org/docs/userguide.html#_using_i3) az alapértelmezett értékekért. Lásd a [billentyű hozzárendeléseket](http://i3wm.org/docs/userguide.html#keybindings) új gyorsbillentyűk hozzáadásához.

A nem Querty billentyűzetet használók hasznosnak találhatják a "beállítás varázslót", [lásd lejjebb](#Konfigur.C3.A1ci.C3.B3_var.C3.A1zsl.C3.B3_.C3.A9s_alternat.C3.ADv_billenty.C5.B1zetkioszt.C3.A1sok).

### Tárolók

Az i3 fa struktúrában kezeli az ablakokat, tárolókat használva blokkok létrehozásához. Ez a szerkezet elágazik vízszintes és függőleges kettéosztásokba. A tárolók alapértelmezésben csempézett kiosztásúak, de ez megváltoztatható füles, vagy halmozott kiosztásra, és lebegő módra is (például párbeszédablakok). A lebegő ablakok mindíg legfölül vannak.

Lásd az [i3 fát](http://i3wm.org/docs/userguide.html#_tree), és [Konténerek és adatszerkezet](http://www.youtube.com/watch?v=AWA8Pl57UBY)-et további részletekért.

### Alkalmazásindító

Az i3 a [dmenu](/index.php/Dmenu "Dmenu")-t használja alkalmazásindítónak, ami alapértelmezetten a `$mod+d` billentyűkombinációhoz van beállítva.

Az [i3-wm](https://www.archlinux.org/packages/?name=i3-wm) tartalmazza az *i3-dmenu-desktop*-ot, egy [Perl](https://en.wikipedia.org/wiki/Perl "wikipedia:Perl") wrapper-t a *dmenu*-hez ami [desktop entry](/index.php/Desktop_entries "Desktop entries")-k használatával létrehoz egy lisát a telepített alkalmazásokról. Alternatívaként a [j4-dmenu-desktop-git](https://aur.archlinux.org/packages/j4-dmenu-desktop-git/) csomag használható.

## Beállítás

See [Configuring i3](http://i3wm.org/docs/userguide.html#configuring) for details. The rest of this article assumes the *i3* configuration file to be in the folder `~/.config`.

### Konfiguráció varázsló és alternatív billentyűzetkiosztások

When *i3* is first started, it offers to run the configuration wizard *i3-config-wizard*. This tool creates `~/.config/i3/config` by rewriting a template configuration file in `/etc/i3/config.keycodes`. It makes two modifications to the default template:

1.  It asks the user to choose a default modifier key, which it adds to the template as a single line, like `set $mod Mod1`; and
2.  it replaces all *bindcode* lines with *bindsym* lines corresponding to the user's current keyboard layout.

Step 2 is designed to ensure that the four navigation shortcuts, `j`, `k`, `l` and "semicolon" on a Qwerty keyboard, will be mapped to keysyms which have the same location, e.g. `h`, `t`, `n`, `s` on a [Dvorak](/index.php/Dvorak "Dvorak") keyboard. The side-effect of this magic is that up to fifteen other keysyms may be remapped in ways which break the mnemonics - so that, for a Dvorak user, "restart" is bound to `$mod1+p` instead of `$mod1+r`, "split horizontally" is bound to `$mod1+d` instead of `$mod1+h`, and so on.

Therefore, users of alternate keyboard layouts who want straightforward key bindings, which match the bindings given in tutorials, may prefer to circumvent the "config wizard". This can be done by just copying `/etc/i3/config` into `~/.config/i3/config` (or `~/.i3/config`), and editing that file.

Note that a keycode-based configuration is also possible, e.g. for users who often switch between keyboard layouts, but want the i3 bindings to stay the same.

### Színsémák

The configuration file allows for customization of window decoration colors, but the syntax makes it impractical to create or share themes. There are several projects which make this easier and include a variety of user-contributed themes.

*   **i3-style** — Modifies your config in place from a theme stored in a JSON object, designed for frequently tweaking or changing a colorscheme

	[https://github.com/acrisci/i3-style](https://github.com/acrisci/i3-style) || [nodejs-i3-style](https://aur.archlinux.org/packages/nodejs-i3-style/)

*   **j4-make-config** — Merge your config with a collection of themes or personal config parts, for example host-specific configuration, allowing quick changing of the theme and flexible, dynamic customization of the configuration

	[https://github.com/okraits/j4-make-config](https://github.com/okraits/j4-make-config) || [j4-make-config-git](https://aur.archlinux.org/packages/j4-make-config-git/)

### i3bar

Amellett, hogy a munkaterületekről információt mutat, az i3bar bemenetként szolgálhat az i3status-nak, vagy egy alternatívájának, mint ahogy említve lesz a következő szekcióban. Például:

 `~/.config/i3/config` 
```
bar {
    output            LVDS1
    status_command    i3status
    position          top
    mode              hide
    workspace_buttons yes
    tray_output       none

    font -misc-fixed-medium-r-normal--13-120-75-75-C-70-iso10646-1

    colors {
        background #000000
        statusline #ffffff

        focused_workspace  #ffffff #285577
        active_workspace   #ffffff #333333
        inactive_workspace #888888 #222222
        urgent_workspace   #ffffff #900000
    }
}
```

Lásd az [i3bar konfigurálását](http://i3wm.org/docs/userguide.html#_configuring_i3bar) további részletekért.

#### i3bar alternatívák

Néhány felhasználó esetleg előnyben részesít olyan paneleket, amelyeket a hagyományos [asztali környezetek](/index.php/Desktop_environment "Desktop environment") biztosítanak. Ez elérhető a választott panel alkalmazás automatikus indításával az i3 indításakor.

Az [XFCE](/index.php/XFCE "XFCE") panel indításához add hozzá a következő sort az `~/.config/i3/config`-hoz:

```
exec --no-startup-id xfce4-panel --disable-wm-check

```

Az i3bar indítása kikapcsolható a `~/.config/i3/config` fájlban a `bar{ }` szakasz hatástalanításával, vagy egy gyorsbillentyű beállításával az i3bar elrejtéséhez:

 `~/.config/i3/config` 
```
# i3bar elrejtése, mutatása
bindsym $mod+m bar mode toggle

```

### i3status

Másold a konfigurációs fájlokat a felhasználói könyvtáradba:

```
$ cp /etc/i3status.conf ~/.config/i3status/config

```

Nem minden plugin van definiálva az alapértelmezett konfigurációban, és néhány konfigurációs érték esetleg érvénytelen a rendszereden, ezért szükség szerint szerkesztésre szorulhat. Lásd a `man i3status`-t a részletekért.

#### i3status helyettesítők

*   **[conky](/index.php/Conky "Conky")** — Nagymértékben bővíthető rendszermonitor. Az i3bar-ral való használathoz lásd [ezt a tutorialt](http://i3wm.org/docs/user-contributed/conky-i3bar.html)

	[https://github.com/brndnmtthws/conky](https://github.com/brndnmtthws/conky) || [conky](https://www.archlinux.org/packages/?name=conky)

*   **[i3blocks](/index.php/I3blocks "I3blocks")** — Shell scriptek által bővíthető. Kezelni tudja a kattintásokat, megszakításokat, és a blokkonkénti külön frissítési idótartam beállítását.

	[https://github.com/vivien/i3blocks](https://github.com/vivien/i3blocks) || [i3blocks](https://aur.archlinux.org/packages/i3blocks/)

*   **i3pystatus** — Bővíthető Python 3 rendszermonitor, számos pluginnel és konfigurálási opcióval.

	[https://github.com/enkore/i3pystatus](https://github.com/enkore/i3pystatus) i3pystatus || [i3pystatus-git](https://aur.archlinux.org/packages/i3pystatus-git/)

*   **i3situation** — Még egy Python 3 állapotsor generátor.

	[https://github.com/HarveyHunt/i3situation](https://github.com/HarveyHunt/i3situation) || [i3situation-git](https://aur.archlinux.org/packages/i3situation-git/)

*   **j4status** — Állapotsort biztosít, pluginek által bővíthető, C-ben van írca. További plugineket a [j4status-plugins-git](https://aur.archlinux.org/packages/j4status-plugins-git/) csomag biztosít.

	[http://j4status.j4tools.org/](http://j4status.j4tools.org/) || [j4status-git](https://aur.archlinux.org/packages/j4status-git/)

*   **goi3bar** — i3status alternatíva, Go-ban van írva. Konfigurációs fájl által vezérelt, jelentős plugin támogatással, minden elemhez saját frissítési időköz beállítása.

	[https://github.com/denbeigh2000/goi3bar/](https://github.com/denbeigh2000/goi3bar/) || [goi3bar-git](https://aur.archlinux.org/packages/goi3bar-git/)

*   **goblocks** — Gyors, könnyűsúlyú i3status alternatíva, Go-ban írva.

	[https://github.com/davidscholberg/goblocks](https://github.com/davidscholberg/goblocks) || [goblocks](https://aur.archlinux.org/packages/goblocks/)

*   **bumblebee-status** — Témák által testreszabható Python állapotsor generátor.

	[https://github.com/tobi-wan-kenobi/bumblebee-status](https://github.com/tobi-wan-kenobi/bumblebee-status) || [bumblebee-status-git](https://aur.archlinux.org/packages/bumblebee-status-git/)

*   **ty3status** — i3status alternatíva, Typescript-ben írva. JavaScript blokkokhoz első osztályú támogatással.

	[https://github.com/mrkmg/ty3status](https://github.com/mrkmg/ty3status) || [ty3status-git](https://aur.archlinux.org/packages/ty3status-git/)

#### i3status wrapper-ek

*   **i3cat** — Egy [go](/index.php/Go "Go") alapú wrapper, ami több külső forrásból is össze tudja fűzni a bemenetet. Tudja kezelni a kattintást, és továbbítani a felhasználó által meghatározott jeleket az alfolyamatoknak.

	[http://vincent-petithory.github.io/i3cat/](http://vincent-petithory.github.io/i3cat/) || [i3cat-git](https://aur.archlinux.org/packages/i3cat-git/)

*   **py3status** — Egy bővíthető i3status wrapper, Python-ban írva.

	[https://github.com/ultrabug/py3status](https://github.com/ultrabug/py3status) || [py3status](https://aur.archlinux.org/packages/py3status/)

#### Ikonszerű betűk az állapotsoron

*i3bar* [patchelhető](#Patches) XBM icon támogatáshoz, de használhatsz helyette ikonszerű betűket.

*   **ttf-font-awesome** — Nagyítható vektor ikonok, CSS-el szabhatóak testre. Ez a [cheatsheet](http://fortawesome.github.io/Font-Awesome/cheatsheet/) leírja az Unicode kódjait.

	[http://fortawesome.github.io/Font-Awesome/](http://fortawesome.github.io/Font-Awesome/) || [ttf-font-awesome](https://aur.archlinux.org/packages/ttf-font-awesome/)

*   **ttf-font-icons** — Átfedés nélküli, és következetesen méretezett keveréke az Awesome és Ionicons ikonoknak. Szintén megszüntet egy kisebb átfedést a DejaVu Sans és az Awesome között.

	[http://kageurufu.net/icons.pdf](http://kageurufu.net/icons.pdf) || [ttf-font-icons](https://aur.archlinux.org/packages/ttf-font-icons/).

Betűtípusok kombinálásához határozz meg egy tartalék betűtípust a konfigurációs fájlban, a betűtípusokat `,` karakterrel elválasztva, mint ez:

 `~/.config/i3/config` 
```
bar {
  ...
  font pango:DejaVu Sans Mono, Icons 8
  ...
}
```

A [pango szintaxis](https://developer.gnome.org/pango/stable/pango-Fonts.html#pango-font-description-from-string) szerint a betűméretet csak egyszer kell meghatározni, a vesszővel elválasztott lista végén.Külön méret beállítása minden betűtípushoz az összes betűtípus figyelmen kívül hagyását okozza, az utolsó kivételével.

Az ikonok hozzáadása a formázási sztringekhez a `~/.config/i3status/config`-ben a fenti cheatsheet-ben leírt számok használatával lehetséges. A beviteli mód szövegszerkesztőnként változik. Például a "szív" ikon beillesztése (unicode szám f004):

*   többféle GUI szövegszerkesztő: (pl.: [gedit](/index.php/Gedit "Gedit"), Leafpad) és terminálok (e.g. GNOME Terminal, xfce4-terminal): `ctrl+shift+u`, `f004`, `Enter`
*   [Emacs](/index.php/Emacs "Emacs"): `ctrl+x`, `8`, `Enter`, `f004`, `Enter`
*   [Vim](/index.php/Vim "Vim") (--insert-- módban): `Ctrl+v`, `uf004`
*   [urxvt](/index.php/Urxvt "Urxvt"): `Ctrl+Shift` lenyomva tartása közben írd be: `f004`

### Terminál emulátorok

Alapértelmezetten a `$mod+Return` lenyomása futtatja az `i3-sensible-terminal`-t, ami egy szkript egy terminál emulátor meghívására. Lásd `man i3-sensible-terminal`-t a meghívható terminálok sorrendjéért.

Ha ehelyett egy meghatározott terminált szeretnél indítani, módosítsd a következő sort az `~/.config/i3/config`-ben:

```
bindsym $mod+Return exec i3-sensible-terminal

```

Esetleg beállíthatod a `$TERMINAL` [környezeti változót](/index.php/Environment_variable "Environment variable").

## Tips and tricks

### Advanced window navigation

See [i3 window Navigation Tips](http://www.slackword.net/?p=657).

### Jump to open window

*   **quickswitch-i3** — Python utility to quickly change to and locate windows in i3

	[https://github.com/proxypoke/quickswitch-for-i3](https://github.com/proxypoke/quickswitch-for-i3) || [quickswitch-i3](https://aur.archlinux.org/packages/quickswitch-i3/)

*   **i3-wm-scripts** — search for and jump to windows with particular names matching regexp

	[https://github.com/yiuin/i3-wm-scripts](https://github.com/yiuin/i3-wm-scripts) ||

*   **winmenupy** — Launches dmenu with a list of clients, sorted after workspaces. Selecting a client jumps to that window.

	[https://github.com/ziberna/i3-py/blob/master/examples/winmenu.py](https://github.com/ziberna/i3-py/blob/master/examples/winmenu.py) ||

*   **[rofi](/index.php/Rofi "Rofi")** — Search and jump to open and scratchpad window

	[https://davedavenport.github.io/rofi/](https://davedavenport.github.io/rofi/) || [rofi](https://www.archlinux.org/packages/?name=rofi)

### Jump to urgent window

Add to `.i3/config`: [[1]](https://faq.i3wm.org/question/853/how-to-jump-to-urgent-workspace/)

```
bindsym $mod+x [urgent=latest] focus

```

### Save and restore the window layout

From version 4.8, and onward *i3* can save and restore workspace layouts. To do this, the following packages are needed: [perl-anyevent-i3](https://www.archlinux.org/packages/?name=perl-anyevent-i3) and [perl-json-xs](https://www.archlinux.org/packages/?name=perl-json-xs) from the [official repositories](/index.php/Official_repositories "Official repositories").

**Note:** This section only provides quick tutorial on how to save the current window layout of a single workspace and how to restore it for later use. Refer to the [official documentation](http://i3wm.org/docs/layout-saving.html) for more details

#### Save the current window layout of a single workspace

To save the current window layout, follow these steps:

1.  First, execute various commands to open windows in a preferred workspace and resize them if needed. Make sure to write down each executed command for each window.
2.  Now, in a new workspace, open a terminal and run the following: `i3-save-tree --workspace N > ~/.i3/workspace_N.json` where N is the number of the preferred workspace. This will save the current layout of workspace N to the file `~/.i3/workspace_N.json`.
3.  The newly created file needs to be edited, however this may be done with the following commands: `tail -n +2 ~/.i3/workspace_N.json | fgrep -v '// splitv' | sed 's|//||g' > ~/.i3/workspace_N.json` 

#### Restore the window layout of the workspace

There are two ways to restore the layout of the workspace: by writing a script, or by editing `~/.i3/config` to automatically load the layout. In this section only the first case will be considered, refer to the [official documentation](http://i3wm.org/docs/layout-saving.html#_restoring_the_layout) for the second case.

To restore the saved layout in the previous section, write a file named `load_layout.sh` with the following contents:

*   The starting lines:

 `~/load_layout.sh` 
```
#!/bin/bash
i3-msg "workspace M; append_layout ~/.i3/workspace_N.json"
```

where M is the number of the workspace in which you would like to load the previously saved layout and N is the number of workspace saved in the previous section.

*   And the commands used in the previous section to get the preferred windows, but enclosed in parentheses and with an ampersand appended before the last parentheses.

For example, if the saved layout contained three `uxterm` windows:

 `~/load_layout.sh` 
```
#!/bin/bash

# First we append the saved layout of worspace N to workspace M
i3-msg "workspace M; append_layout ~/.i3/workspace_N.json"

# And finally we fill the containers with the programs they had
(uxterm &)
(uxterm &)
(uxterm &)
```

Then set the file as executable:

```
chmod u+x ~/load_layout.sh

```

And finally, the layout of worskpace N can be loaded onto to workspace M by running:

```
~/load_layout.sh

```

**Tip:** Adding `bindsym $mod+g exec ~/load_layout.sh` to `~/.i3/config` and restarting i3 will bind Mod+g to run the above script.

**Note:** If the above script does not work properly, refer to the [official documentation](http://i3wm.org/docs/layout-saving.html#_editing_layout_files). The *swallows* sections of `~/.i3/workspace_N.json` needs to be manually edited.

### Scratchpad containers

By default, [scratchpads](http://i3wm.org/docs/userguide.html#_scratchpad) only contain a single window. However, containers can also be made a scratchpad.

Create a new container (for example, `Mod+Enter`), split it (`Mod+v`) and create another container. Focus the parent (`Mod+a`), split in the opposite direction (`Mod+h`), and create again.

Focus the first container (with focus parent as needed), make the window floating (`Mod+Shift+Space`), and move it to the scratchpad (`Mod+Shift+-`). You can now split containers to preference.

**Note:** Containers cannot be resized individually in floating windows. Resize the containers before making windows floating.

**Tip:** When only using terminal applications, consider a multiplexer such as [tmux](/index.php/Tmux "Tmux") instead.

See also [[2]](https://faq.i3wm.org/question/138/multiple-scratchpad/i3) for multiple scratchpads.

### Screensaver and power management

With [Power management#xss-lock](/index.php/Power_management#xss-lock "Power management") you can register a screenlocker for your i3 session. The `-time` option locks the screen after a given time period.

```
xautolock -time 10 -locker "i3lock -i 'background_image.png'" &

```

A [systemd](/index.php/Systemd "Systemd") service file can be used to lock the screen before the system is being sent to sleep or hibernation state. See [Power management#Suspend/resume service files](/index.php/Power_management#Suspend.2Fresume_service_files "Power management"). Note that i3lock requires the type of the service to be `forking`.

See also [DPMS](/index.php/DPMS "DPMS").

### Shutdown, reboot, lock screen

Key combinations for shutdown, reboot and screenlock can be added to `~/.config/i3/config`. The below example assumes you have [polkit](https://www.archlinux.org/packages/?name=polkit) installed to allow unprivileged users to run [power management](/index.php/Systemd#Power_management "Systemd") commands.

```
set $Locker i3lock && sleep 1

set $mode_system System (l) lock, (e) logout, (s) suspend, (h) hibernate, (r) reboot, (Shift+s) shutdown
mode "$mode_system" {
    bindsym l exec --no-startup-id $Locker, mode "default"
    bindsym e exec --no-startup-id i3-msg exit, mode "default"
    bindsym s exec --no-startup-id $Locker && systemctl suspend, mode "default"
    bindsym h exec --no-startup-id $Locker && systemctl hibernate, mode "default"
    bindsym r exec --no-startup-id systemctl reboot, mode "default"
    bindsym Shift+s exec --no-startup-id systemctl poweroff -i, mode "default"  

    # back to normal: Enter or Escape
    bindsym Return mode "default"
    bindsym Escape mode "default"
}

bindsym $mod+Pause mode "$mode_system"

```

Once completed, you will be presented with a prompt whenever you press `$mod+pause`. For more complex behaviour, use a separate script, and refer to it in the mode. [[3]](https://gist.github.com/anonymous/c8cd0a59bf4acb273068)

**Note:**

*   `sleep 1` adds a small delay to prevent possible race conditions with suspend [[4]](https://bugs.launchpad.net/ubuntu/+source/unity-2d/+bug/830348)
*   The `-i` argument for `systemctl poweroff` causes a shutdown even if other users are logged-in (this requires [polkit](https://www.archlinux.org/packages/?name=polkit)), or when *logind* (wrongly) assumes so. [[5]](https://bugs.freedesktop.org/show_bug.cgi?id=62676)

For a list of alternative screen lockers, see [List of applications/Security#Screen lockers](/index.php/List_of_applications/Security#Screen_lockers "List of applications/Security").

### External displays manual management

Thanks to [xrandr](/index.php/Xrandr "Xrandr") there are many ways to easily manage systems displays. The below example integrates it in the i3 config file, and behave as the Power Management section above.

Here a laptop with both VGA and HDMI outputs will use a menu selection to switch them On/Off:

```
## Manual management of external displays
# Set the shortcuts and what they do
set $mode_display Ext Screen (v) VGA ON, (h) HDMI ON, (x) VGA OFF, (y) HDMI OFF
mode "$mode_display" {
    bindsym v exec --no-startup-id xrandr --output VGA1 --auto --right-of LVDS1, mode "default"
    bindsym h exec --no-startup-id xrandr --output HDMI1 --auto --right-of LVDS1, mode "default"
    bindsym x exec --no-startup-id xrandr --output VGA1 --auto --off, mode "default"
    bindsym y exec --no-startup-id xrandr --output HDMI1 --auto --off, mode "default"

    # back to normal: Enter or Escape
    bindsym Return mode "default"
    bindsym Escape mode "default"
}
# Declare here the shortcut to bring the display selection menu
bindsym $mod+x mode "$mode_display"

```

Any window that is still open in a switched Off display will automatically come back to the remaining active display.

The simplest way to determine names of your devices is to plug the device you wish to use and run:

```
$ xrandr --query

```

which will output the available, recognized devices and their in-system names to set your config file appropriately.

Refer to the [xrandr](/index.php/Xrandr "Xrandr") page or man page for the complete list of available options, the [i3 userguide](http://i3wm.org/docs/userguide.html) and/or the [i3 FAQ on reddit](https://www.reddit.com/r/i3wm) for more info.

### Tabbed or stacked web-browsing

Some web-browsers intentionally do not implement tabs, since managing tabs is considered to be the task of the window manager, not the task of the browser.

To let i3 manage your tab-less web-browser, in this example for [uzbl](/index.php/Uzbl "Uzbl"), add the following line to your `~/.config/i3/config`

```
for_window [class="Uzbl-core"] focus child, layout stacking, focus

```

This is for stacked web browsing, meaning that the windows will be shown vertically. The advantage over tabbed browsing is that the window-titles are fully visible, even if a lot of browser windows are open.

If you prefer tabbed browsing, with windows in horizontal direction ('tabs'), use

```
for_window [class="Uzbl-core"] focus child, layout tabbed, focus

```

### Workspace variables

As workspaces are defined multiple times in i3, assigning workspace variables can be helpful. For example:

```
set $WS1 term
set $WS2 web
set $WS3 misc
set $WS4 media
set $WS5 code

```

Then replace workspace names with their matching variables:

```
bindsym $mod+1          workspace $WS1
...
bindsym $mod+Shift+1    move container to workspace $WS1

```

See [Changing named workspaces](http://i3wm.org/docs/userguide.html#_changing_named_workspaces_moving_to_workspaces) for more information.

### Correct handling of floating dialogs

While dialogs should open in floating mode by default [[6]](http://i3wm.org/docs/userguide.html#_floating), many still open in tiling mode. To change this behaviour, check the dialog's `WM_WINDOW_ROLE` with [xorg-xprop](https://www.archlinux.org/packages/?name=xorg-xprop) and add the correct rules to `~/.i3/config` (using [pcre](http://www.pcre.org/) syntax):

```
for_window [window_role="pop-up"] floating enable
for_window [window_role="task_dialog"] floating enable

```

You can also use title rules and regular expressions:

```
for_window [title="Preferences$"] floating enable

```

or `WM_CLASS`:

```
for_window [class="(?i)mplayer"] floating enable

```

### Network Download/Upload speed on statusbar

You might adapt this upstream [script](http://code.stapelberg.de/git/i3status/tree/contrib/measure-net-speed.bash). For that,

*   rename both network cards according to your system (use `ip addr`)
*   find them on `/sys/devices` then replace them appropriately:

```
$ find /sys/devices -name *network_interface*

```

**Tip:** Use `/sys/class/net/*interface*/statistics/` to not depend on PCI location.

Now, just save the script in a suitable place (for example `~/.config/i3`) and point your status program to it.

## Patches

Packages with patches not merged upstream are available in the [AUR](/index.php/AUR "AUR"):

*   **i3-wm-iconpatch** — Titlebar icon support

	[https://github.com/ashinkarov/i3-extras](https://github.com/ashinkarov/i3-extras) || [i3-wm-iconpatch](https://aur.archlinux.org/packages/i3-wm-iconpatch/)

## Troubleshooting

### General

In many cases, bugs are fixed in the development versions [i3-git](https://aur.archlinux.org/packages/i3-git/) and [i3status-git](https://aur.archlinux.org/packages/i3status-git/), and upstream will ask to reproduce any errors with this version. [[7]](http://i3wm.org/docs/debugging.html) See also [Debug - Getting Traces#General](/index.php/Debug_-_Getting_Traces#General "Debug - Getting Traces").

### Buttons in the i3 message bar do not work

Buttons such as "Edit config" in `i3-nagbar` call `i3-sensible-terminal`, so make sure your [Terminal emulator](#Terminal_emulator) is recognized by i3.

### Faulty line wraps in tiled terminals

i3 v4.3 and higher ignore size increment hints for tiled windows [[8]](https://www.mail-archive.com/i3-discuss@i3.zekjur.net/msg00709.html). This may cause terminals to wrap lines prematurely, amongst other issues. As a workaround, make the offending window floating, before tiling it again.

### Mouse cursor remains in waiting mode

When starting a script or application which does not support startup notifications, the mouse cursor will remain in busy/watch/clock mode for 60 seconds.

To solve this for a particlar application, use the `--no-startup-id` parameter, for example:

```
exec --no-startup-id ~/script
bindsym $mod+d exec --no-startup-id dmenu_run

```

To disable this animation globally, see [Cursor themes#Create links to missing cursors](/index.php/Cursor_themes#Create_links_to_missing_cursors "Cursor themes").

### Unresponsive key bindings

Some tools such as [scrot](/index.php/Taking_a_screenshot#scrot "Taking a screenshot") may not work when used with a regular key binding (executed after key press). In those cases, execute commands after key release with the `--release` argument [[9]](http://i3wm.org/docs/userguide.html#keybindings):

```
bindsym --release Print exec --no-startup-id scrot
bindsym --release Shift+Print exec --no-startup-id scrot -s

```

### Tearing

i3 does [not properly implement double buffering](https://github.com/i3/i3/issues/661) hence tearing or flickering may occur. To prevent this, install and configure [compton](/index.php/Compton "Compton"). [[10]](https://faq.i3wm.org/question/3279/do-i-need-a-composite-manager-compton.1#post-id-3282)

### Tray icons not visible

The `tray_output primary` directive may require setting a primary output with *xrandr*, specifying the output explicitly or simply removing this directive. [[11]](https://github.com/i3/i3/issues/1144) See [Xrandr](/index.php/Xrandr "Xrandr") for details. The default configuration created by i3-config-wizard no longer adds this directive to the configuration from i3 4.12.

## See also

*   [Official website](http://i3wm.org)
*   [funtoo Wiki](http://www.funtoo.org/I3_Tiling_Window_Manager)
*   [i3 Source code](http://code.stapelberg.de/git/i3)
*   [i3-extras](https://github.com/ashinkarov/i3-extras) - Collection of scripts and patches
*   [i3ipc-glib](https://github.com/acrisci/i3ipc-glib) - A library for i3 extensions
*   [i3ipc-ruby](https://github.com/veelenga/i3ipc-ruby) - An improved library for i3 extensions in Ruby
*   [j4tools](http://www.j4tools.org/) - non-official tools designed to work with i3

**Arch Linux Forums**

*   [The i3 thread](https://bbs.archlinux.org/viewtopic.php?id=99064) - A general discussion about i3
*   [i3 desktop screenshots and config sharing](https://bbs.archlinux.org/viewtopic.php?id=103369)

**Screencasts**

*   [i3 window manager v4.1 screencast](http://www.youtube.com/watch?v=Wx0eNaGzAZU)
*   [i3 window manager v4.1X screencasts](https://www.youtube.com/watch?v=j1I63wGcvU4&index=1&list=PL5ze0DjYv5DbCv9vNEzFmP6sU7ZmkGzcf)