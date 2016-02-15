Projekt GNOME začal od píky a vytvořil úplně nový desktop jménem GNOME 3\. Nabízí:

*   Moderní vzhled a písmo
*   Přístup ke všem oknům a aplikacím pomocí "Činností"
*   Přívětivý systém notifikací a nenápadný horní panel
*   Integraci vylepšeného prohlížeče souborů Nautilus
*   Integrované služby pro komunikaci
*   Novou aplikaci pro nastavení systému
*   Vyhledávací funkci činností
*   Funkce jako automatické rozmisťování oken

Další informace najdete na [oficiálních stránkách GNOME 3.](http://www.gnome3.org/)

## Contents

*   [1 Úvod](#.C3.9Avod)
*   [2 Upgrade z GNOME 2](#Upgrade_z_GNOME_2)
*   [3 Instalace](#Instalace)
    *   [3.1 D-Bus démon](#D-Bus_d.C3.A9mon)
    *   [3.2 Spouštění GNOME](#Spou.C5.A1t.C4.9Bn.C3.AD_GNOME)
*   [4 Používání shellu](#Pou.C5.BE.C3.ADv.C3.A1n.C3.AD_shellu)
    *   [4.1 GNOME cheat sheet](#GNOME_cheat_sheet)
    *   [4.2 Restartování shellu](#Restartov.C3.A1n.C3.AD_shellu)
*   [5 Přizpůsobení vzhledu GNOME](#P.C5.99izp.C5.AFsoben.C3.AD_vzhledu_GNOME)
    *   [5.1 Celkový vzhled](#Celkov.C3.BD_vzhled)
        *   [5.1.1 Gsettings](#Gsettings)
        *   [5.1.2 GNOME tweak tool](#GNOME_tweak_tool)
        *   [5.1.3 settings.ini a nastavení vzhledu GTK3](#settings.ini_a_nastaven.C3.AD_vzhledu_GTK3)
        *   [5.1.4 Motiv ikon](#Motiv_ikon)
    *   [5.2 Nautilus](#Nautilus)
        *   [5.2.1 Vždy zobrazovat umístění jako text](#V.C5.BEdy_zobrazovat_um.C3.ADst.C4.9Bn.C3.AD_jako_text)
    *   [5.3 GNOME panel](#GNOME_panel)
        *   [5.3.1 Zobrazení data v horním panelu](#Zobrazen.C3.AD_data_v_horn.C3.ADm_panelu)
        *   [5.3.2 Skrytí ikonky zpřístupnění](#Skryt.C3.AD_ikonky_zp.C5.99.C3.ADstupn.C4.9Bn.C3.AD)
        *   [5.3.3 Skrytí ikonky bluetooth](#Skryt.C3.AD_ikonky_bluetooth)
        *   [5.3.4 Zobrazení ikonky baterie](#Zobrazen.C3.AD_ikonky_baterie)
        *   [5.3.5 Zakázání položky "Uspat" ve status menu](#Zak.C3.A1z.C3.A1n.C3.AD_polo.C5.BEky_.22Uspat.22_ve_status_menu)
        *   [5.3.6 Eliminate delay when logging out](#Eliminate_delay_when_logging_out)
        *   [5.3.7 Zobrazení sledování systému](#Zobrazen.C3.AD_sledov.C3.A1n.C3.AD_syst.C3.A9mu)
        *   [5.3.8 Zobrazení informací o počasí](#Zobrazen.C3.AD_informac.C3.AD_o_po.C4.8Das.C3.AD)
    *   [5.4 Zobrazení činností](#Zobrazen.C3.AD_.C4.8Dinnost.C3.AD)
        *   [5.4.1 Odstranění položek z přehledu aplikací](#Odstran.C4.9Bn.C3.AD_polo.C5.BEek_z_p.C5.99ehledu_aplikac.C3.AD)
        *   [5.4.2 Zmenšení velikosti ikon aplikací](#Zmen.C5.A1en.C3.AD_velikosti_ikon_aplikac.C3.AD)
    *   [5.5 Záhlaví okna](#Z.C3.A1hlav.C3.AD_okna)
        *   [5.5.1 Ztenčení záhlaví](#Zten.C4.8Den.C3.AD_z.C3.A1hlav.C3.AD)
        *   [5.5.2 Úprava tlačítek záhlaví](#.C3.9Aprava_tla.C4.8D.C3.ADtek_z.C3.A1hlav.C3.AD)
        *   [5.5.3 Skrytí záhlaví při maximalizaci](#Skryt.C3.AD_z.C3.A1hlav.C3.AD_p.C5.99i_maximalizaci)
        *   [5.5.4 Pozadí přihlašovací obrazovky](#Pozad.C3.AD_p.C5.99ihla.C5.A1ovac.C3.AD_obrazovky)
        *   [5.5.5 Větší písmo pro přihlášení](#V.C4.9Bt.C5.A1.C3.AD_p.C3.ADsmo_pro_p.C5.99ihl.C3.A1.C5.A1en.C3.AD)
        *   [5.5.6 Vypnutí zvuku](#Vypnut.C3.AD_zvuku)
        *   [5.5.7 Make the power button interactive](#Make_the_power_button_interactive)
        *   [5.5.8 Rozložení klávesnice v GDM](#Rozlo.C5.BEen.C3.AD_kl.C3.A1vesnice_v_GDM)
    *   [5.6 Další tipy](#Dal.C5.A1.C3.AD_tipy)
*   [6 Miscellaneous settings](#Miscellaneous_settings)
    *   [6.1 Nastavení aplikací spouštěných při přihlášení](#Nastaven.C3.AD_aplikac.C3.AD_spou.C5.A1t.C4.9Bn.C3.BDch_p.C5.99i_p.C5.99ihl.C3.A1.C5.A1en.C3.AD)
    *   [6.2 Aktivování numlocku při spuštění](#Aktivov.C3.A1n.C3.AD_numlocku_p.C5.99i_spu.C5.A1t.C4.9Bn.C3.AD)
    *   [6.3 Rozšíření GNOME shell](#Roz.C5.A1.C3.AD.C5.99en.C3.AD_GNOME_shell)
    *   [6.4 Výchozí terminál](#V.C3.BDchoz.C3.AD_termin.C3.A1l)
    *   [6.5 Prostřední tlačítko myši](#Prost.C5.99edn.C3.AD_tla.C4.8D.C3.ADtko_my.C5.A1i)
    *   [6.6 Xmonad](#Xmonad)
    *   [6.7 wmii](#wmii)
*   [7 Hidden features](#Hidden_features)
    *   [7.1 Úprava klávesových zkratek](#.C3.9Aprava_kl.C3.A1vesov.C3.BDch_zkratek)
    *   [7.2 Shutdown via the status menu](#Shutdown_via_the_status_menu)
*   [8 Integrated messaging (Empathy)](#Integrated_messaging_.28Empathy.29)
*   [9 Enabling fallback mode](#Enabling_fallback_mode)
*   [10 Troubleshooting](#Troubleshooting)
    *   [10.1 GNOME login takes a very long time](#GNOME_login_takes_a_very_long_time)
    *   [10.2 When an extension breaks GNOME](#When_an_extension_breaks_GNOME)
    *   [10.3 Extensions do not work after GNOME 3 update](#Extensions_do_not_work_after_GNOME_3_update)
    *   [10.4 Screen is not locked after resume](#Screen_is_not_locked_after_resume)
    *   [10.5 GTK2+ apps show segfaults and fail to launch](#GTK2.2B_apps_show_segfaults_and_fail_to_launch)
    *   [10.6 ATI Catalyst driver creates glitches and artifacts](#ATI_Catalyst_driver_creates_glitches_and_artifacts)
    *   [10.7 Multiple monitors and dock extension](#Multiple_monitors_and_dock_extension)
    *   [10.8 No event sounds for Empathy and other programs](#No_event_sounds_for_Empathy_and_other_programs)
    *   [10.9 Editing hotkeys via can-change-accels fails](#Editing_hotkeys_via_can-change-accels_fails)
    *   [10.10 Panels do not respond to right-click in fallback mode](#Panels_do_not_respond_to_right-click_in_fallback_mode)
    *   [10.11 "Show Desktop" keyboard shortcut does not work](#.22Show_Desktop.22_keyboard_shortcut_does_not_work)
    *   [10.12 Nautilus does not start](#Nautilus_does_not_start)
    *   [10.13 Epiphany does not play flash videos](#Epiphany_does_not_play_flash_videos)
    *   [10.14 Unable to apply stored configuration for monitors](#Unable_to_apply_stored_configuration_for_monitors)
    *   [10.15 Lock button fails to re-enable touchpad](#Lock_button_fails_to_re-enable_touchpad)
    *   [10.16 Ctrl+V pastes path instead of file in Nautilus](#Ctrl.2BV_pastes_path_instead_of_file_in_Nautilus)
    *   [10.17 Unable to connect to secured wi-fi network](#Unable_to_connect_to_secured_wi-fi_network)
    *   [10.18 "Any command has been defined 33"](#.22Any_command_has_been_defined_33.22)
    *   [10.19 GDM and Gnome use X11 cursors](#GDM_and_Gnome_use_X11_cursors)
*   [11 External links](#External_links)

## Úvod

GNOME 3 má _dvě_ prostředí: **GNOME Shell** (nový standardní layout) a **nouzový režim** (fallback mode). Sezení GNOME automaticky rozpozná, kdy počítač není schopen spustit Gnome Shell a v případě nutnosti spustí nouzový režim.

**Nouzový režim** se podobá GNOME 2\. (Používá gnome-panel/Metacity místo gnome-shell/Mutter.)

V nouzovém režimu můžete stále nahradit výchozí správce oken vámi preferovaným.

## Upgrade z GNOME 2

**Warning:** Upgrade na GNOME 3 z aktivního GNOME 2 sezení může způsobit poškození systému.

Aktualizaci je doporučeno spouštět z konzole nebo z jiného pracovního prostředí / správce oken.

```
# pacman -Syu 

```

Touto aktualizací jsme nainstalovali pouze _nouzový režim_ GNOME 3.x. Pro instaci nového GNOME shellu:

```
# pacman -S gnome-shell

```

V závislosti na vašem nastavení může být pro správnou funkčnost nezbytné odstranit starou konfiguraci:

```
$ mv .config .config.bak
$ mv .gconf .gconf.bak
$ mv .gnome2 .gnome2.bak

```

## Instalace

GNOME 3 se nachází v repozitáři [extra]. Skupina **gnome** obsahuje základní pracovní prostředí a aplikace, **gnome-extra** obsahuje některé další volitelné součásti. Pokud si nejste jisti, jestli všechny balíčky využijete, pročtěte si před instalací jejich popisy (nebo je prostě odstraňte později).

Příklad:

```
# pacman -Syu gnome
# pacman -S gnome-extra

```

### D-Bus démon

GNOME pro svůj běh vyžaduje [D-Bus](/index.php/D-Bus_(%C4%8Cesky) "D-Bus (Česky)") démon. V článku [D-Bus](/index.php/D-Bus_(%C4%8Cesky) "D-Bus (Česky)") najdete návod na jeho instalaci.

### Spouštění GNOME

Pro nejlepší integraci prostředí je doporučen správce přihlášení **GDM**. Nic vám ale nebrání v tom nainstalovat si místo GDM třeba [SLiM](/index.php/SLiM_(%C4%8Cesky) "SLiM (Česky)") nebo cokoliv jiného. Pro další informace o spouštění pracovního prostředí navštivte [článek o správcích displeje](/index.php/Display_Manager_(%C4%8Cesky) "Display Manager (Česky)").

```
# pacman -S gdm

```

Pokud GNOME radši spouštíte ručně z konzole, přidejte následující **jediný** řádek začínající slovem `exec` do souboru `~/.xinitrc`. Pro více informací viz [článek o xinitrc](/index.php/Xinitrc "Xinitrc").

 `~/.xinitrc` 

```
 #POUZE TENTO ŘÁDEK:
 exec gnome-session

```

Jakmile soubor uložíte, můžete GNOME spouštět příkazem `startx`.

## Používání shellu

### GNOME cheat sheet

Na stránkách GNOME najdete užitečný [GNOME Shell cheat sheet](https://live.gnome.org/GnomeShell/CheatSheet) s informacemi o přepínání úloh, klávesových zkratkách, práci s okny, panelem apod.

### Restartování shellu

Po úpravách vzhledu je často vyžadováno restartovat GNOME shell. Mohli bychom se odhlásit a přihlásit, nicméně mnohem jednodušší a rychlejší je stisknout `Alt` + `F2` a zadat `r` následované klávesou `Enter`.

## Přizpůsobení vzhledu GNOME

### Celkový vzhled

GNOME 3 sice začalo "od píky", to s sebou ale nese i některé nepříjemnosti. Jednou z nich je zatím nepříliš obsáhlý konfigurační nástroj. Pokročilejší volby tady stále jsou, akorát nejsou uživateli tolik na očích. Nové _Nastavení systému_ je sice přehledné, každopádně nejspíš zatoužíte po více možnostech přizpůsobení vzhledu.

#### Gsettings

Nový nástroj pro příkazový řádek **gsettings** uchovává nastavení v binárním formátu (na rozdíl od gconf a XML). Tutoriál [Customizing the GNOME Shell](http://blog.fpmurphy.com/2011/03/customizing-the-gnome-3-shell.html) odhaluje sílu gsettings.

#### GNOME tweak tool

Tento grafický nástroj umožňuje změnit písma, motivy, tlačítka oken a další nastavení.

```
# pacman -S gnome-tweak-tool

```

#### settings.ini a nastavení vzhledu GTK3

Podobně jako v **`~/.gtkrc-2.0`** u GTK2+, je i u GTK3 možné přizpůsobit vzhled v souboru **`${XDG_CONFIG_HOME}/gtk-3.0/settings.ini`**.

Proměnná `$XDG_CONFIG_HOME` je obvykle nastavená na **~/.config**.

_Adwaita,_ výchozí motiv GNOME 3, je součástí **gnome-themes-standard.** Další GTK3 motivy najdete třeba na [stránkách Deviantart.](http://browse.deviantart.com/customization/skins/linuxutil/desktopenv/gnome/gtk3/) Příklad:

 `${XDG_CONFIG_HOME}/gtk-3.0/settings.ini` 

```
  [Settings]
  gtk-theme-name = Adwaita
  gtk-fallback-icon-theme = gnome
  # následující volba funguje jen když ji motiv podporuje
  gtk-application-prefer-dark-theme = true
  # nastavení písma a jeho rozměrů
  gtk-font-name = Sans 10

```

Aby se změny projevily, je nezbytné [restartovat GNOME shell](#Restartov.C3.A1n.C3.AD_shellu). Další volby GTK najdete ve [vývojářské dokumentaci GNOME.](http://developer.gnome.org/gtk3/3.0/GtkSettings.html#GtkSettings.properties)

#### Motiv ikon

GNOME 3 je kompatibilní s motivy ikon GNOME 2, což znamená, že se nemusíme omezovat pouze na motiv výchozí. Pro instalaci nových ikon zkopírujte adresář s motivem do **`~/.icons`** například takto:

```
$ cp -R /home/user/Desktop/muj_motiv_ikon ~/.icons

```

Nový motiv _muj_motiv_ikon_ si můžete aktivovat v **gnome-tweak-tool** v sekci _**Motiv**_.

Jinak můžete motiv nastavit také ručně bez gnome-tweak-tool v **`${XDG_CONFIG_HOME}/gtk-3.0/settings.ini`**.

	 `${XDG_CONFIG_HOME}/gtk-3.0/settings.ini` 

```
... předchozí řádky ...

gtk-icon-theme-name = muj_motiv_ikon
```

### Nautilus

#### Vždy zobrazovat umístění jako text

Nástrojová lišta Nautilu standardně používá k navigaci v podsložkách tlačítka. Pokud si přejete zobrazit cestu jako textové pole, stiskněte `Ctrl` + `L`

Pro trvalé nastavení použijte následující příkaz:

```
$ gsettings set org.gnome.nautilus.preferences always-use-location-entry true

```

### GNOME panel

#### Zobrazení data v horním panelu

Jako výchozí zobrazuje GNOME v horním panelu pouze den v týdnu a čas. Datum můžeme přidat následujícím příkazem. Změny se projeví ihned.

```
# gsettings set org.gnome.shell.clock show-date true

```

#### Skrytí ikonky zpřístupnění

Nainstalujte [gnome-shell-extension-noa11y](https://aur.archlinux.org/packages/gnome-shell-extension-noa11y/) z [AUR](/index.php/AUR "AUR").

#### Skrytí ikonky bluetooth

Deactivate bluetooth as startup-service if that is your intent. Refer to section [Automatic program launch upon login](#Automatic_program_launch_upon_login)

Create a folder named **`nobluetooth.icon@panel.ui`** in **`~/.local/share/gnome-shell/extensions`**. Create two new files:

 `~/.local/share/gnome-shell/extensions/nobluetooth.icon@panel.ui/extension.js` 

```
const Panel = imports.ui.panel;

function main() {
  Panel.STANDARD_TRAY_ICON_SHELL_IMPLEMENTATION['bluetooth'] = '';
}

```

 `~/.local/share/gnome-shell/extensions/nobluetooth.icon@panel.ui/metadata.json` 

```
{
  "shell-version": ["3.0"],
  "uuid": "nobluetooth.icon@panel.ui",
  "name": "nbluetooth",
  "description": "Turn off the bluetooth icon in the panel"
}

```

[Restart the GNOME shell.](#Restartov.C3.A1n.C3.AD_shellu) The icon should be hidden. If this extension ceases to work in the future, adjust the shell version number in **`metadata.json.`**

#### Zobrazení ikonky baterie

Pro zobrazení ikony baterie v oznamovací oblasti nainstalujte `gnome-power-manager`.

```
# pacman -S gnome-power-manager

```

#### Zakázání položky "Uspat" ve status menu

Nainstalujte Gnome Shell rozšíření [alternative status menu](#Roz.C5.A1.C3.AD.C5.99en.C3.AD_GNOME_shell).

```
# pacman -S gnome-shell-extension-alternative-status-menu

```

#### Eliminate delay when logging out

The following tweak removes the confirmation dialog and sixty second delay for logging out.

This dialog normally appears when you log out with the status menu. This tweak affects the _**Power Off**_ dialog as well. This is not a system-wide change; it affects only the user who enters this command. The change takes effect immediately after entering the command.

```
$ gsettings set org.gnome.SessionManager logout-prompt 'false'

```

#### Zobrazení sledování systému

Nainstalujte rozšíření [gnome-shell-system-monitor-applet-git](https://aur.archlinux.org/packages/gnome-shell-system-monitor-applet-git/) dostupné v [AUR](/index.php/AUR "AUR").

#### Zobrazení informací o počasí

Nainstalujte [gnome-shell-extension-weather-git](https://aur.archlinux.org/packages/gnome-shell-extension-weather-git/) z [AUR](/index.php/AUR "AUR").

### Zobrazení činností

#### Odstranění položek z přehledu aplikací

Like other desktop environments, GNOME uses .desktop files to populate its Applications view. These text files are in **`/usr/share/applications`**. It is not possible to edit these files from a folder view ‒ Nautilus does not treat their icons as text files. Use a terminal to display or edit .desktop file entries.

```
# ls /usr/share/applications
# nano /usr/share/applications/foo.desktop

```

For system wide changes, edit files in **`/usr/share/applications`**. For local changes, make a copy of _foo.desktop_ in your home folder.

```
$ cp /usr/share/applications/foo.desktop ~/.local/share/applications/

```

Edit .desktop files to fit your wishes. **Note:** removing a .desktop file does not uninstall an application, but instead removes its desktop integration: MIME types, shortcuts, and so forth.

The following command appends one line to a .desktop file and hides its associated icon from Applications view:

```
$ echo "NoDisplay=true" >> foo.desktop

```

#### Zmenšení velikosti ikon aplikací

One awkward selection of the GNOME designers is their choice of large icons for Applications view. This view is painful when working with a small screen containing many large application icons. There is a way to reduce the icon size. It is done by editing the Gnome-Shell theme.

Edit system files directly (make a backup first) or copy theme files to your local folder and edit these files. For the default theme, edit **`/usr/share/gnome-shell/theme/gnome-shell.css`**

For user themes, edit **`/usr/share/themes/<UserTheme>/gnome-shell/gnome-shell.css`**

Edit _gnome-shell.css_ and replace the following values. Afterward, [restart the GNOME shell.](#Restartov.C3.A1n.C3.AD_shellu)

 `gnome-shell.css` 

```
 .icon-grid {
     spacing: 18px;
     -shell-grid-item-size: 82px;
 }

 .icon-grid .overview-icon {
     icon-size: 48px;
 }

```

A cloned GNOME Shell theme with smaller icons is available [on the AUR](https://aur.archlinux.org/packages.php?ID=51586).

### Záhlaví okna

#### Ztenčení záhlaví

```
# sed -i '/title_vertical_pad/s|value="[0-9]\{1,2\}"|value="0"|g' /usr/share/themes/Adwaita/metacity-1/metacity-theme-3.xml

```

[Restartujte GNOME shell.](#Restartov.C3.A1n.C3.AD_shellu) Příkaz změní vertikální odsazení titulku ze 14 na 0 a dodá záhlaví uhlazenější vzhled.

Pro obnovení původních hodnot:

```
$ sudo pacman -S gnome-themes-standard

```

#### Úprava tlačítek záhlaví

At present this setting is changeable only through **gconf-editor.**

For example, we move the close and minimize buttons to the left side of the titlebar. Open **gconf-editor** and locate the _**desktop.gnome.shell.windows.button_layout**_ key. Change its value to **`close,minimize:`** (Colon symbol designates the spacer between left side and right side of the titlebar.) Use whichever buttons in whatever order you prefer. You cannot use a button more than once. Also, keep in mind that certain buttons are deprecated. [Restart the shell](#Restartov.C3.A1n.C3.AD_shellu) to see your new button arrangement.

#### Skrytí záhlaví při maximalizaci

```
# sed -i -r 's|(<frame_geometry name="max")|\1 has_title="false"|' /usr/share/themes/Adwaita/metacity-1/metacity-theme-3.xml

```

[Restartujte GNOME shell.](#Restartov.C3.A1n.C3.AD_shellu) Po této úpravě možná budete mít problém zrušit maximalizaci okna, když ho nebude za co chytit.

With suitable keybindings, you should be able to use `Alt` + `F5`, `Alt` + `F10` or `Alt` + `Space` to remedy the situation.

To prevent **`metacity-theme-3.xml`** from being overwritten each time package "gnome-themes-standard" is upgraded, add its name to **`/etc/pacman.conf`** with `NoUpgrade`.

 `/etc/pacman.conf` 

```
... previous lines ...

# Pacman will not upgrade packages listed in IgnorePkg and members of IgnoreGroup
# IgnorePkg   =
# IgnoreGroup =

NoUpgrade = usr/share/themes/Adwaita/metacity-1/metacity-theme-3.xml    # Do not add a leading slash to the path

... more lines ...

```

To restore original Adwaita theme values:

```
# pacman -S gnome-themes-standard

```

#### Pozadí přihlašovací obrazovky

Once session variables have been exported as explained above, you may issue commands to retrieve or set items used by GDM.

The easiest way to changes all the settings is by launching the Configuration Editor gui with the command

```
$ dconf-editor

```

The location of each setting is the same as in the command line style of configuration shown below:

The following is the command-line approach to retrieve or set the file name used for GDM's wallpaper.

```
$  GSETTINGS_BACKEND=dconf gsettings get org.gnome.desktop.background picture-uri
$  GSETTINGS_BACKEND=dconf gsettings set org.gnome.desktop.background picture-uri 'file:///usr/share/backgrounds/gnome/SundownDunes.jpg'

$  GSETTINGS_BACKEND=dconf gsettings set org.gnome.desktop.background picture-options 'zoom'
## Possible values: centered, none, scaled, spanned, stretched, wallpaper, zoom
```

Note: You must specify a file which user "gdm" has permission to read. GDM cannot read files in your home directory.

An alternative graphical interface to changing themes (gtk3, icons and cursor), the wallpaper and minor other settings of the GDM login screen, you can install [gdm3setup](https://aur.archlinux.org/packages/gdm3setup/) from AUR.

#### Větší písmo pro přihlášení

This tweak enlarges the login font with a scaling factor. It is the same method employed by _Accessibility Manager_ on the desktop.

You must [export the GDM session variables](#Login_screen) before performing this tweak.

```
$ GSETTINGS_BACKEND=dconf gsettings set org.gnome.desktop.interface text-scaling-factor '1.25'

```

#### Vypnutí zvuku

This tweak disables the audible feedback heard when the system volume is adjusted (via keyboard) on the login screen. You must first export the GDM session variables.

```
$ GSETTINGS_BACKEND=dconf gsettings set org.gnome.desktop.sound event-sounds 'false'

```

If the above tweak does not work for you or you are unable to export the GDM session variables, there is always the easiest solution to the "ready sound" problem: mute or lower the sound while in GDM login screen using the media keys (if available) of your keyboard.

#### Make the power button interactive

The default installation sets the power button to suspend the system. _**Power off**_ or _**Show dialog**_ is a better choice. You must first export the GDM session variables as [outlined previously.](#Login_screen)

```
 $ GSETTINGS_BACKEND=dconf gsettings set org.gnome.settings-daemon.plugins.power button-power 'interactive'
 $ GSETTINGS_BACKEND=dconf gsettings set org.gnome.settings-daemon.plugins.power button-hibernate 'interactive'
 $ gsettings list-recursively org.gnome.settings-daemon.plugins.power

```

#### Rozložení klávesnice v GDM

GDM neví o vašem nastavení klávesnice v GNOME 3\. Pro změnu nastavení klávesnice v GDM nastavte požadované rozložení v Xorg konfiguraci. Viz [Beginner's Guide.](/index.php/Beginners%27_Guide_(%C4%8Cesky)#.C3.9Aprava_rozlo.C5.BEen.C3.AD_kl.C3.A1vesnice "Beginners' Guide (Česky)")

### Další tipy

Viz [GNOME Tips](/index.php/GNOME_Tips "GNOME Tips").

## Miscellaneous settings

### Nastavení aplikací spouštěných při přihlášení

Aplikace, které se automaticky spouští po přihlášení nastavíme pomocí `gnome-session-properties`. Tento nástroj je součástí balíčku `gnome-session`.

```
$ gnome-session-properties

```

### Aktivování numlocku při spuštění

Nainstalujte numlockx z repozitáře **[community]**. Pak přidejte příkaz numlockx do aplikací spouštěných po přihlášení.

```
# pacman -S numlockx
$ gnome-session-properties

```

Výše uvedený příkaz otevře nabídku **Předvolby aplikací spouštěných při přihlášení**. Zvolte _**Přidat**_ and vyplňte následovně:

| Název: | _Numlockx_ |
| Příkaz: | _/usr/bin/numlockx on_ |
| Komentář: | _Turns on numlock._ |

Toto nastavení bude platné pouze pro aktuálního uživatele. Pokud budete chtít toto nastavit i pro jiné uživatele, postupujte stejným způsobem.

### Rozšíření GNOME shell

GNOME Shell can be customized with extensions written by others. These provide features such as a dock or a widget for changing the theme. Details on available extensions are found at the [WEBUPD8](http://www.webupd8.org/2011/04/gnome-shell-extensions-additional.html) site. The most recent articles can be found using this [WEBUPD8 search link.](http://www.webupd8.org/search/label/gnome%20shell%20extensions?max-results=20)

Repository **[extras]** has a dozen extensions which can be installed individually. (The latest version of a given extension may be installed using its code snapshot, if preferred.) [List here.](https://www.archlinux.org/packages/?sort=&q=gnome-shell-extension&maintainer=&last_update=&flagged=&limit=50)

```
$ pacman -Ss gnome-shell-extension

```

Other useful extensions provided in the AUR:

| _[Presentation Mode](https://aur.archlinux.org/packages.php?ID=49368)_ | Adds option to inhibit screensaver in the power menu (battery icon). |
| _[Weather](https://aur.archlinux.org/packages.php?ID=49409)_ | Displays weather notifications. |
| _[Alternative Status Menu](https://aur.archlinux.org/packages.php?ID=48607)_ | Adds "Hibernate" and "Power Off" to the status menu. |
| _[Theme selector](https://aur.archlinux.org/packages.php?ID=51102)_ | Select a theme in the activities overview. To install a custom theme with Gnome Tweak Tool you need to install the _[User theme extension](https://www.archlinux.org/packages/extra/any/gnome-shell-extension-user-theme)_ |

[Restart the GNOME Shell](#Restartov.C3.A1n.C3.AD_shellu) after installing an extension. See [when an extension breaks GNOME](#When_an_extension_breaks_GNOME) for troubleshooting information.

### Výchozí terminál

`gsettings`, which replaces `gconftool-2` in GNOME 3, is used to set e. g. the default terminal manually. The setting is relevant for _nautilus-open-terminal_. The commands for [urxvt](/index.php/Rxvt-unicode "Rxvt-unicode") run as daemon:

```
gsettings set org.gnome.desktop.default-applications.terminal exec urxvtc
gsettings set org.gnome.desktop.default-applications.terminal exec-arg "'-e'"

```

**Note:** For _nautilus-open-terminal_, you may need a flag (e.g. `-e`) to indicate that a command will follow: _nautilus-open-terminal_ passes a `cd` command in order to change directories to the appropriate location.

### Prostřední tlačítko myši

By default, GNOME 3 disables middle mouse button emulation regardless of Xorg settings (**Emulate3Buttons**). To enable middle mouse button emulation use:

```
$ gsettings set org.gnome.settings-daemon.peripherals.mouse middle-button-enabled true

```

### Xmonad

[Xmonad](/index.php/Xmonad "Xmonad") is a tiling window manager.

Upgrading to GNOME 3 will likely break your xmonad setup. You can use xmonad again by [forcing fallback mode](#Enabling_fallback_mode) and creating two files:

	 `/usr/share/gnome-session/sessions/xmonad.session` 

```
[GNOME Session]
Name=Xmonad session
RequiredComponents=gnome-panel;gnome-settings-daemon;
RequiredProviders=windowmanager;notifications;
DefaultProvider-windowmanager=xmonad
DefaultProvider-notifications=notification-daemon
```

	 `/usr/share/xsessions/xmonad-gnome-session.desktop` 

```
[Desktop Entry]
Name=Xmonad GNOME
Comment=Tiling window manager
TryExec=/usr/bin/gnome-session
Exec=gnome-session --session=xmonad
Type=XSession
```

The next time you log in, you should have the ability to choose _Xmonad GNOME_ as your session.

### wmii

[wmii](/index.php/Wmii "Wmii") is a tiling window manager.

You can use wmii with gnome by [forcing fallback mode](#Enabling_fallback_mode) and creating tree files:

	 `/usr/share/applications/wmii.desktop` 

```
[Desktop Entry]
Version=1.0
Type=Application
Name=wmii
TryExec=wmii
Exec=wmii
```

	 `/usr/share/xsessions/gnome-wmii.desktop` 

```
[Desktop Entry]
Name=Gnome-wmii
Comment=Gnome with wmii as window manager
TryExec=gnome-session
Exec=gnome-session --session=wmii
Type=Application
```

	 `/usr/share/gnome-session/sessions/wmii.session` 

```
[GNOME Session]
Name=wmii
RequiredComponents=gnome-panel;gnome-settings-daemon;
RequiredProviders=windowmanager;notifications;
DefaultProvider-windowmanager=wmii
DefaultProvider-notifications=notification-daemon
```

The next time you log in, you should have the ability to choose _Gnome-wmii_ as your session.

The original info was taken from [running-the-awesome-window-manager-within-gnome](http://makandra.com/notes/1367-running-the-awesome-window-manager-within-gnome), go there for info on awesome-gnome.

Also it has info on how to:

- create a per session (wmii, gnome, gnome-wmii, etc) dconf database (useful if you ever plan on using regular gnome)

- Remove the bottom Gnome panel (with the task list)

- Move the top panel (with the menus) to the bottom

- Untick the expand option

- Set it to autohide

## Hidden features

GNOME 3 ukrývá spoustu užitečných voleb, které lze upravit pomocí **dconf-editor.** GNOME 3 dále podporuje **gconf-editor** pro úpravu nastavení, která ještě nepřešla pod správu pomocí dconf.

### Úprava klávesových zkratek

Firstly, use **dconf-editor** to place a checkmark next to `can-change-accels` in the key named _org.gnome.desktop.interface._

We will replace the hotkey — a.k.a. keyboard shortcut, keyboard accelerator — used by Nautilus to move files to the trash folder.

The default assignment is a somewhat-awkward `Ctrl` + `Delete`.

*   Open Nautilus, select any file, and click **Edit** on the menu bar.
*   Hover over the _Move to Trash_ menu item.
*   While hovering, press `Delete`. The current accelerator is now unset.
*   Press the key that you wish to become the new keyboard accelerator.
*   Press `Delete` to make the new accelerator be the Delete key.

Unless you select a file or folder, _Move to Trash_ will be grayed-out. Finally, disable `can-change-accels` to prevent accidental hotkey changes.

### Shutdown via the status menu

Presently, GNOME designers have hidden the Shutdown option inside the status menu. To shut down your system with the status menu, click the menu and hold down the **Alt** key so that the _**Suspend**_ item changes to _**Power Off.**_ The subsequent dialog allows you to shut down or restart your system.

If you disable the Suspend menu item system-wide as described [elsewhere in this document](#Disable_.22Suspend.22_in_the_status_menu) you do not have to go through these motions.

Another option is to install the _Alternative Status Menu_ extension. See the section on shell extensions. The alternative menu extension installs a new status menu with a non-hidden _**Power Off**_ entry.

## Integrated messaging (Empathy)

Empathy, the engine behind integrated messaging, and all system settings based on messaging accounts will not show up unless the **telepathy** group of packages or at least one of the backends (**telepathy-gabble**, or **telepathy-haze**, for example) is installed.

These packages are not included in default Arch GNOME installs. You can install the Telepathy and optionally any backends with:

```
# pacman -S telepathy

```

Without telepathy, Empathy will not open the account management dialog and can get stuck in this state. If this happens -- even after quitting Empathy cleanly -- the /usr/bin/empathy-accounts application can remain running and will need to be killed before you can add any new accounts.

View descriptions of telepathy components on the [Freedesktop.org Telepathy Wiki.](http://telepathy.freedesktop.org/wiki/Components)

## Enabling fallback mode

Your session automatically starts in fallback mode when **gnome-shell** is not present, or when your hardware cannot handle graphics acceleration — such as running within a virtual machine or running on old hardware.

If you wish to enable fallback mode while still having **gnome-shell** installed, make the following system change:

Open **gnome-control-center.** Click the _System Info_ icon. Click Graphics. Change _Forced Fallback Mode_ to `ON.`

You can alternatively choose the type of session from a terminal with a _gsettings_ command:

```
$ gsettings set org.gnome.desktop.session session-name 'gnome-fallback'

```

You may want to log out after making the change. You will see the chosen type of session upon your next login.

To disable forced-fallback mode (that is, launch the normal GNOME Shell) use a value of 'gnome' instead of 'gnome-fallback'.

## Troubleshooting

### GNOME login takes a very long time

See if you enabled _PulseAudio Network_ settings in **paprefs**. When any network audio settings are enabled, GNOME hangs about a minute after login.

One solution is to create a new user account and login to that account. Another solution is to move your **~/.gconf**, **~/.gconfd** and **~/.conf/dconf** folders to a holding area. Login again to see if the delay is gone.

If the excessive delay is gone, determine which setting causes the delay using trial-and-error.

### When an extension breaks GNOME

When enabling shell extensions causes GNOME breakage, you should first remove the _user-theme_ and _auto-move-windows_ extensions from their installation directory.

The installation directory could be one of **`~/.local/share/gnome‑shell/extensions,`** **`/usr/share/gnome‑shell/extensions,`** or **`/usr/local/share/gnome‑shell/extensions`**. Removing these two extension-containing folders may fix the breakage. Otherwise, isolate the problem extension with trial‑and‑error.

Removing or adding an extension-containing folder to the aforementioned directories removes or adds the corresponding extension to your system. Details on Gnome Shell extensions are available at the [GNOME web site.](https://live.gnome.org/GnomeShell/Extensions)

### Extensions do not work after GNOME 3 update

Locate the folder where your extensions are installed. It might be **`~/.local/share/gnome-shell/extensions`** or **`/usr/share/gnome-shell/extensions`**.

Edit each occurrence of **`metadata.json`** which appears in each extension sub-folder.

| Insert: | **`"shell-version": ["3.0"]`** |
| Instead of (for example): | **`"shell-version": ["3.0.1"]`** |
| You might instead use: | **`"shell-version": ["3.0.0", "3.0.1", "3.0.2"]`** |

**"3.0"** is the best solution. It indicates the extension works with every _**3.0.x**_ GNOME Shell version.

### Screen is not locked after resume

Screen lock only works when you suspend through GNOME's status menu. If you suspend or hibernate using the power button, your screen is not locked after resume. The problem is a configuration failure in dconf.

Open _dconf-editor_ and uncheck **`lock-use-screensaver`** in the key named _org.gnome.power-manager._

```
# gsettings set org.gnome.power-manager lock-use-screensaver 'false'

```

Your screen should now be locked after resume whether you used the status menu, the power button, or a key combination. Bug report: [Screen gets no more locked after suspend #Comment 8](https://bugzilla.redhat.com/show_bug.cgi?id=698135#c8)

### GTK2+ apps show segfaults and fail to launch

That usually happens when **oxygen-gtk** is installed. This theme appears to conflict with GNOME 3 or GTK3 settings. When **oxygen-gtk** has been set as a GTK2 theme, GTK2 apps segfault with errors like these:

```
 (firefox-bin:14345): GLib-GObject-WARNING **: invalid (NULL) pointer instance

(firefox-bin:14345): GLib-GObject-CRITICAL **: g_signal_connect_data: assertion `G_TYPE_CHECK_INSTANCE (instance)' failed
(firefox-bin:14345): Gdk-CRITICAL **: IA__gdk_screen_get_default_colormap: assertion `GDK_IS_SCREEN (screen)' failed
(firefox-bin:14345): Gdk-CRITICAL **: IA__gdk_colormap_get_visual: assertion `GDK_IS_COLORMAP (colormap)' failed
(firefox-bin:14345): Gdk-CRITICAL **: IA__gdk_screen_get_default_colormap: assertion `GDK_IS_SCREEN (screen)' failed
(firefox-bin:14345): Gdk-CRITICAL **: IA__gdk_screen_get_root_window: assertion `GDK_IS_SCREEN (screen)' failed
(firefox-bin:14345): Gdk-CRITICAL **: IA__gdk_screen_get_root_window: assertion `GDK_IS_SCREEN (screen)' failed
(firefox-bin:14345): Gdk-CRITICAL **: IA__gdk_window_new: assertion `GDK_IS_WINDOW (parent)' failed
Segmentation fault

```

The current workaround is to remove **oxygen-gtk** from the system and use a different theme for applications.

### ATI Catalyst driver creates glitches and artifacts

For the moment, Catalyst is not proposed to be used while running GNOME Shell. The opensource ATI driver, xf86-video-ati, however, seems to be working properly with the GNOME 3 composited desktop.

Note: Fix is promised with Catalyst 11.9\. See [http://ati.cchtml.com/show_bug.cgi?id=99](http://ati.cchtml.com/show_bug.cgi?id=99)

### Multiple monitors and dock extension

If you have multiple monitors configured using Nvidia Twinview, the dock extension may get sandwiched in-between the monitors. You can edit the source of this extension to reposition the dock to a position of your choosing.

Edit **/usr/share/gnome-shell/extensions/dock@gnome-shell-extensions.gnome.org/extension.js** and locate this line in the source:

```
this.actor.set_position(primary.width-this._item_size-this._spacing-2, (primary.height-height)/2);

```

The first parameter is the X position of the dock display, by subtracting 15 pixels as opposed to 2 pixels from this it correctly positioned on my primary monitor, you can play around with any X,Y coordinate pair to position it correctly.

```
this.actor.set_position(primary.width-this._item_size-this._spacing-15, (primary.height-height)/2);

```

### No event sounds for Empathy and other programs

If you are using [OSS](/index.php/OSS "OSS"), you may want to install **libcanberra-oss** [from AUR](https://aur.archlinux.org/packages.php?ID=31163).

### Editing hotkeys via can-change-accels fails

It is also possible to manually change the keys via an application's so-called accel map file. Where it is to be found is up to the application: For instance, Thunar's is at `~/.config/Thunar/accels.scm`, whereas Nautilus's is located at `~/.gnome2/accels/nautilus`. The file should contain a list of possible hotkeys, each unchanged line commented out with a leading ";" that has to be removed for a change to become active.

### Panels do not respond to right-click in fallback mode

Check Configuration Editor: /apps/metacity/general/mouse_button_modifier. This modifier key (<Alt>, <Super>, etc) used for normal windows is also used by panels and their applets.

### "Show Desktop" keyboard shortcut does not work

GNOME developers treated the corresponding binding as bug (see [https://bugzilla.gnome.org/show_bug.cgi?id=643609](https://bugzilla.gnome.org/show_bug.cgi?id=643609)) due to Minimization being deprecated. To show the desktop again assign ALT+STRG+D to the following setting:

```
System Settings --> Keyboard --> Shortcuts --> Windows --> Hide all normal windows

```

### Nautilus does not start

1.  Press `ALT`+`F2`
2.  Enter `gnome-tweak-tool`
3.  Select the _File Manager_ tab.
4.  Locate option _Have file manager handle the desktop_ and assure it is toggled **off**.

### Epiphany does not play flash videos

Epiphany now uses gtk3, but Adobe's Flash Player still relies on gtk2\. See [Epiphany#Flash](/index.php/Epiphany#Flash "Epiphany") for a workaround involving nspluginwrapper.

### Unable to apply stored configuration for monitors

If you encounter this message try to disable the xrandr gnome-settings-daemon plugin :

```
$ dconf write /org/gnome/settings-daemon/plugins/xrandr/active false

```

### Lock button fails to re-enable touchpad

Some laptops have a touchpad lock button that disables the touchpad so that users can type without worrying about touching the touchpad. It appears currently that although GNOME can lock the touchpad by pressing this button, it cannot unlock it. If the touchpad gets locked you can do the following to unlock it.

1.  Start a terminal. You can do this by pressing `ALT`+`F2` , then typing `gnome-terminal` and then pressing `ENTER`
2.  Type in the following command

```
$ xinput set-prop "SynPS/2 Synaptics TouchPad" "Device Enabled" 1

```

### Ctrl+V pastes path instead of file in Nautilus

If you are affected by this issue, edit `~/.gnome2/accels/nautilus` where you can find two lines for Ctrl+V :

 `~/.gnome2/accels/nautilus` 

```
(gtk_accel_path "<Actions>/DirViewActions/Paste" "<Control>v")
...
(gtk_accel_path "<Actions>/ClipboardActions/Paste" "<Control>v")

```

The issue appears to stem from the second entry. Deleting that line may fix the issue temporarily. You might have to reapply this fix after an update.

An alternative is to assign a different key combination to one of the actions.

### Unable to connect to secured wi-fi network

You see the network connections listing, but choosing an encrypted network fails to show a dialog for key entry. You may need to install network-manager-applet. See [GNOME NetworkManager setup](/index.php/NetworkManager#GNOME "NetworkManager").

### "Any command has been defined 33"

When you press print screen key to take screenshot and you got "Any command has been defined 33", install metacity:

```
# pacman -S metacity

```

### GDM and Gnome use X11 cursors

To fix this issue, you will have to copy paste these lines as root in a terminal:

```
$ mkdir /usr/share/icons/default
$ cd /usr/share/icons/default
$ echo "[Icon Theme]" >> index.theme
$ echo "Inherits=Adwaita" >> index.theme

```

Alternatively, you can install [gnome-cursors-fix](https://aur.archlinux.org/packages/gnome-cursors-fix/) from [AUR](/index.php/AUR "AUR").

## External links

*   [The Official Website](http://www.gnome.org/)
*   Themes, icons, and backgrounds:
    *   [Gnome Art](http://art.gnome.org/)
    *   [Gnome Look](http://www.gnome-look.org/)
*   GTK/GNOME programs:
    *   [Gnome Files](http://www.gnomefiles.org/)
    *   [Gnome Project Listing](http://www.gnome.org/projects/)