Related articles

*   [Display Manager](/index.php/Display_Manager "Display Manager")

[SLiM](http://slim.berlios.de/) egy betűszó a Simple Login Manager-ből. SLiM egyszerű, könnyűsúlyú és könnyen konfigurálható. SLiM-et azért használják, mert nem követeli meg a [GNOME](/index.php/GNOME "GNOME") vagy [KDE](/index.php/KDE "KDE") függőségeket, segíthet a felhasználóknak egy könnyű rendszer összeállítani, akik szeretik használni a kis erőforrásigényű asztali rendszereket, mint [Xfce](/index.php/Xfce "Xfce"), [Openbox](/index.php/Openbox "Openbox") vagy [Fluxbox](/index.php/Fluxbox "Fluxbox").

## Contents

*   [1 Telepítés](#Telep.C3.ADt.C3.A9s)
*   [2 Beállítás](#Be.C3.A1ll.C3.ADt.C3.A1s)
    *   [2.1 SLiM engedélyezése](#SLiM_enged.C3.A9lyez.C3.A9se)
    *   [2.2 Egyszerű környezetek](#Egyszer.C5.B1_k.C3.B6rnyezetek)
    *   [2.3 Automatikus bejelentkezés](#Automatikus_bejelentkez.C3.A9s)
    *   [2.4 Többszörös környezetek](#T.C3.B6bbsz.C3.B6r.C3.B6s_k.C3.B6rnyezetek)
    *   [2.5 Témák](#T.C3.A9m.C3.A1k)
        *   [2.5.1 Kettős képernyő beállítás](#Kett.C5.91s_k.C3.A9perny.C5.91_be.C3.A1ll.C3.ADt.C3.A1s)
*   [3 Egyéb opciók](#Egy.C3.A9b_opci.C3.B3k)
    *   [3.1 Kurzor változtatása](#Kurzor_v.C3.A1ltoztat.C3.A1sa)
    *   [3.2 SLiM és az asztal hátterének illesztése](#SLiM_.C3.A9s_az_asztal_h.C3.A1tter.C3.A9nek_illeszt.C3.A9se)
    *   [3.3 Leállítás, újraindítás, felfüggesztés, kilépés, terminál indítása SLiM-ből](#Le.C3.A1ll.C3.ADt.C3.A1s.2C_.C3.BAjraind.C3.ADt.C3.A1s.2C_felf.C3.BCggeszt.C3.A9s.2C_kil.C3.A9p.C3.A9s.2C_termin.C3.A1l_ind.C3.ADt.C3.A1sa_SLiM-b.C5.91l)
    *   [3.4 SLiM init hiba rc.d daemon-nal](#SLiM_init_hiba_rc.d_daemon-nal)
    *   [3.5 Power-off hiba Splashy-vel](#Power-off_hiba_Splashy-vel)
    *   [3.6 Login információk SLiM-mel](#Login_inform.C3.A1ci.C3.B3k_SLiM-mel)
    *   [3.7 SLiM és a Gnome Keyring](#SLiM_.C3.A9s_a_Gnome_Keyring)
    *   [3.8 DPI beállítása SLiM-mel](#DPI_be.C3.A1ll.C3.ADt.C3.A1sa_SLiM-mel)
    *   [3.9 Véletlen téma használata](#V.C3.A9letlen_t.C3.A9ma_haszn.C3.A1lata)
*   [4 Az összes SLiM opció](#Az_.C3.B6sszes_SLiM_opci.C3.B3)
*   [5 Források](#Forr.C3.A1sok)
*   [6 Segítség](#Seg.C3.ADts.C3.A9g)

## Telepítés

Telepítsd a SLiM-et az **extra** tárolóból:

```
# pacman -S slim

```

## Beállítás

### SLiM engedélyezése

SLiM induláskor betöltődik, hogyha beírod a daemon-ok közé `rc.conf`-ban vagy módosítod az `inittab`-ot. Lásd a [Display managert](/index.php/Display_manager "Display manager") részletesebb utasításokért.

### Egyszerű környezetek

Ahhoz, hogy a SLiM betöltsön egy adott asztali környezetet, szerkeszd `~/.xinitrc` fájlodat:

```
#!/bin/sh

#
# ~/.xinitrc
#
# Executed by startx (run your window manager from here)
#

exec [session-command]

```

Cseréld `[session-command]` részt a megfelelő paranccsal. Néhány példa a különböző asztalok indítási parancsaira:

```
exec awesome
exec dwm
exec fluxbox
exec fvwm2
exec gnome-session
exec openbox-session
exec startkde
exec startlxde
exec startxfce4

```

Ha az asztali környezeted nem szerepel itt, nézd meg a megfelelő wiki oldalt.

### Automatikus bejelentkezés

Ahhoz, hogy a SLiM automatikusan bejelentkezzen egy adott felhasználónévvel (a jelszó beírásának szüksége nélkül), az /etc/slim.conf fájl alábbi sorait kell módosítani:

```
# default_user        simone

```

Tedd érvényessé ezt a sort (töröld az elejéről a #-t, angolul: 'uncomment'), és a simone nevet írd át a megfelelő felhasználónévre.

```
# auto_login          no

```

Ezt a sort is tedd érvényessé, és írd át a 'no'-t 'yes'-re. Ez fogja az automatikus bejelntkezés funkciót bekapcsolni.

### Többszörös környezetek

A SLiM és beállítható úgy, hogy több környezet közül tudj választani bejelentkezéskor.

Az alábbihoz hasonló 'case' struktúrát kell a `~/.xinitrc` fájlodba beleírni, és a `/etc/slim.conf` 'sessions' változóját úgy módosítani, hogy passzoljon azzal a névvel, ami a 'case' struktúrát kezeli. A bejelentkezéskor az F1 billenytűvel tudsz váltani köztük. Fontos, hogy ez még csak kísérleti stádiumban lévő funkció!

```
# The following variable defines the session which is started if the user doesn't explicitly select a session
# Source: http://svn.berlios.de/svnroot/repos/slim/trunk/xinitrc.sample

DEFAULT_SESSION=twm

case $1 in
kde)
	exec startkde
	;;
xfce4)
	exec startxfce4
	;;
icewm)
	icewmbg &
	icewmtray &
	exec icewm
	;;
wmaker)
	exec wmaker
	;;
blackbox)
	exec blackbox
	;;
*)
	exec $DEFAULT_SESSION
	;;
esac

```

### Témák

Telepítsd a [slim-themes](https://www.archlinux.org/packages/?name=slim-themes) csomagot:

```
# pacman -S slim-themes archlinux-themes-slim

```

A [archlinux-themes-slim](https://www.archlinux.org/packages/?name=archlinux-themes-slim) csomagok sok különböző témát tartalmaznak. Nézz bele az `/usr/share/slim/themes` könyvtárba, hogy lásd az elérhető témákat. Adott téma használatához add meg a téma nevét a 'current_theme' sorban a `/etc/slim.conf`-ban:

```
#current_theme       default
current_theme       archlinux-simplyblack

```

To preview a theme run if no instance of the Xorg server is running by: A kiválasztott témát ki tudod próbálni, akkor is ha éppen fut a Xorg , a következő paranccsal:

```
$ slim -p /usr/share/slim/themes/<theme name>

```

Bezáráshoz, írd be "exit" a Login sorba és nyomj Entert.

Kiegészítő témacsomagok találhatók az [AUR](/index.php/AUR "AUR")-ban.

#### Kettős képernyő beállítás

A SLiM témát módosíthatod a /usr/share/slim/themes/<your-theme>/slim.theme szerkesztésével. Például az 'input panel' helyét az alábbi százalékos értékek beállításával módosíthatod (magának a panelnak a mérete 450x250 pixel):

```
input_panel_x           50%
input_panel_y           50%

```

vagy pixelértékekben is megadhatod:

```
# Ezekkel az értékekkel az "archlinux-simplyblack" panel a 1440x900 méretű képernyő közepére kerül
input_panel_x           495
input_panel_y           325

```

```
# Ezekkel az értékekkel az "archlinux-retro" panel a 1680x1050 képernyő közepére kerül
input_panel_x           615
input_panel_y           400

```

Ha az általad használt témának van háttérképe is, annak megjelenítését a background_style segítségével módosíthatod ('stretch', 'tile', 'center' vagy 'color'). További információért látogass el a [a slim hivatalos témákkal kapcsolatos dokumentációs](http://slim.berlios.de/themes_howto.php) oldalára (angol).

## Egyéb opciók

Egy pár dolog, amit lehet ki szeretnél próbálni.

### Kurzor változtatása

Ha le szeretnéd cserélni az X alapértelmezett kurzorját egy másikra, a [slim-cursor](https://aur.archlinux.org/packages/slim-cursor/) csomag áll rendelkezésedre.

Miután telepítetted, szerkeszd a `/etc/slim.conf` fájlt és tedd érvényessé az alábbi sort:

```
cursor   left_ptr

```

Ez egy sima kurzort fog adni neked. A beállítás továbbításra kerül a `xsetroot -cursor_name`-nek. A beállítható kurzorok nevéért nézz szét [itt](http://cvsweb.xfree86.org/cvsweb/*checkout*/xc/lib/X11/cursorfont.h?rev=HEAD&content-type=text/plain) vagy `/usr/share/icons/<your-cursor-theme>/cursors/` fájlban.

Ha a bejelentkező képernyőn megjelenő kurzort szeretnéd kicserélni, hozz létre egy fájlt a `/usr/share/icons/default/index.theme` névvel, az alábbi tartalommal:

```
[Icon Theme]
Inherits=<your-cursor-theme>

```

Cseréld le a <your-cursor-theme> szót az általad használni kívánt kurzortéma nevével (pl. whiteglass).

### SLiM és az asztal hátterének illesztése

Ha ugyanazt a hátteret szeretnéd a SLiM-ben használni mint az asztalodon, akkor nevezd át a használt téma háttérkép fájlját, és csinálj egy linket az asztalod háttérjéről a SLiM témád mappájába:

```
# mv /usr/share/slim/themes/default/background.jpg{,.bck}
# ln -s /path/to/mywallpaper.jpg /usr/share/slim/themes/default/background.jpg

```

### Leállítás, újraindítás, felfüggesztés, kilépés, terminál indítása SLiM-ből

A SLiM bejelntkező képernyőből is leállíthatod, újraindíthatod, felfüggesztheted a géped, kiléphetsz, vagy indíthatsz egy terminált. Hogy ezt meg tudd tenni, az alábbi szavak egyikét írd be a felhasználónévhez, a jelszóhoz pedig a root jelszót:

*   Terminál indításához írd be a **console** szót felhasználónévként (az alapértelmezett az xterm, amit külön kell telepíteni... írd át a `/etc/slim.conf` fájlt ha más terminált szeretnél használni)
*   Leállításhoz írd be a **halt** szót felhasználónévként
*   Újraindításhoz írd be **reboot** szót felhasználónévként
*   Bash-be való kilépéshez írd be **exit** szót felhasználónévként
*   Felfüggesztéshez írd be a **suspend** szót felhasználónévként (ez alapból ki van kapcsolva, szerkeszd a `/etc/slim.conf` fájlt root-ként hogy érvényesítsd a `suspend_cmd` sort és, ha szükséges, módosítsd magát a suspend parancsot is (pl. cseréld ki a `/usr/sbin/suspend` sort `sudo /usr/sbin/pm-suspend`-re))

### SLiM init hiba rc.d daemon-nal

Ha a SLiM-et a `/etc/rc.conf` fájlt DAEMON szekciójával indítod, és nem indul el, az valószínűleg egy ún. 'lock' fájl hibája. Ugyanis a SLiM létrehoz egy 'lock' fájlt a `/var/lock` mappában minden egyes induláskor. Azonban előfordulhat, hogy ez a lock mappa ne létezik a /var mappán belül, így a SLiM nem tud elindulni. Nézd meg biztos létezik-e a `/var/lock` mappa, és ha nem, root-ként létre tudod hozni az alábbi paranccsal:

```
# mkdir /var/lock/

```

### Power-off hiba Splashy-vel

Ha Splashy-t és SLiM-et is használsz előfordulhat, hogy időnként nem tudod a géped kikapcsolni vagy újraindítani a GNOME, Xfce, LXDE vagy bármi egyéb menüjéből. Nézd meg a `/etc/slim.conf` és `/etc/splash.conf` fájljaidat, és írd át: DEFAULT_TTY=7 és xserver_arguments vt07 (ugyanarra mutasson).

### Login információk SLiM-mel

Alapból a SLiM nem tudja loggolni a bejelentkezéseket az utmp-be és a wtmp-be, ami miatt hibás jelentések kerülnek rögzítésre a bejelentkezési információkról. Ez javítható ha módosítod a `slim.conf` fájlodat az alábbiak szerint:

```
 sessionstart_cmd    /usr/bin/sessreg -a -l $DISPLAY %user
 sessionstop_cmd     /usr/bin/sessreg -d -l $DISPLAY %user

```

### SLiM és a Gnome Keyring

**Note:** slim 1.3.5-1 ships with `/etc/pam.d/slim` preconfigured to unlock keyring upon login. Users no longer need to modify the file.

**Warning:** If auto login is enabled, the GNOME keyring will not be unlocked automatically on login. This will cause dependent applications, such as Chrome/Chromium and NetworkManager, to misbehave (see [https://bbs.archlinux.org/viewtopic.php?id=167579](https://bbs.archlinux.org/viewtopic.php?id=167579)).

See [GNOME Keyring#Use Without GNOME, and without a display manager](/index.php/GNOME_Keyring#Use_Without_GNOME.2C_and_without_a_display_manager "GNOME Keyring") to use GNOME Keyring in a custom session.

### DPI beállítása SLiM-mel

A Xorg szerver általában megkapja a DPI értéket, de ha nem, a SLiM beállítható úgy, hogy megtörténjen. A SLiM-mel nem fog működni, ha úgy állítod be a DPI-t, hogy a `/etc/X11/xinit/xserverrc` fájlhoz hozzáadod a -dpi 96 argumentumot. Ennek javítására módosítsd a `slim.conf` fájlt a következőről:

```
 xserver_arguments   -nolisten tcp vt07 

```

az alábbira:

```
 xserver_arguments   -nolisten tcp vt07 -dpi 96

```

### Véletlen téma használata

A current_theme változót kell úgy használni, hogy utána vesszővel elválasztva szerepeljenek azok a témák, amik közül a véletlenszerű kiválasztás történjen.

## Az összes SLiM opció

Ez egy lista a SLiM összes konfigurációs beállítási lehetőségéről az alapértelmezett értékeikkel.

**Note:** welcome_msg két változót engedélyez: **%host** és **%domain**
sessionstart_cmd **%user** változót engedélyezi *(közvetlenül a login_cmd előt kelrül végrehajtásra)* és ez a sessionstop_cmd esetén is engedélyezett
login_cmd a **%session** és **%theme** változókat engedélyezi

| Option Name | Default Value |
| default_path | <tt>/bin:/usr/bin:/usr/local/bin</tt> |
| default_xserver | <tt>/usr/bin/X</tt> |
| xserver_arguments | <tt>vt07 -auth /var/run/slim.auth</tt> |
| numlock |
| daemon | <tt>yes</tt> |
| xauth_path | <tt>/usr/bin/xauth</tt> |
| login_cmd | <tt>exec /bin/bash -login ~/.xinitrc %session</tt> |
| halt_cmd | <tt>/sbin/shutdown -h now</tt> |
| reboot_cmd | <tt>/sbin/shutdown -r now</tt> |
| suspend_cmd |
| sessionstart_cmd |
| sessionstop_cmd |
| console_cmd | <tt>/usr/bin/xterm -C -fg white -bg black +sb -g %dx%d+%d+%d -fn %dx%d -T</tt> |
| screenshot_cmd | <tt>import -window root /slim.png</tt> |
| welcome_msg | <tt>Welcome to %host</tt> |
| session_msg | <tt>Session:</tt> |
| default_user |
| focus_password | <tt>no</tt> |
| auto_login | <tt>no</tt> |
| current_theme | <tt>default</tt> |
| lockfile | <tt>/var/run/slim.lock</tt> |
| logfile | <tt>/var/log/slim.log</tt> |
| authfile | <tt>/var/run/slim.auth</tt> |
| shutdown_msg | <tt>The system is halting...</tt> |
| reboot_msg | <tt>The system is rebooting...</tt> |
| sessions | <tt>wmaker,blackbox,icewm</tt> |
| sessiondir |
| hidecursor | <tt>false</tt> |
| input_panel_x | <tt>50%</tt> |
| input_panel_y | <tt>40%</tt> |
| input_name_x | <tt>200</tt> |
| input_name_y | <tt>154</tt> |
| input_pass_x | <tt>-1</tt> |
| input_pass_y | <tt>-1</tt> |
| input_font | <tt>Verdana:size=11</tt> |
| input_color | <tt>#000000</tt> |
| input_cursor_height | <tt>20</tt> |
| input_maxlength_name | <tt>20</tt> |
| input_maxlength_passwd | <tt>20</tt> |
| input_shadow_xoffset | <tt>0</tt> |
| input_shadow_yoffset | <tt>0</tt> |
| input_shadow_color | <tt>#FFFFFF</tt> |
| welcome_font | <tt>Verdana:size=14</tt> |
| welcome_color | <tt>#FFFFFF</tt> |
| welcome_x | <tt>-1</tt> |
| welcome_y | <tt>-1</tt> |
| welcome_shadow_xoffset | <tt>0</tt> |
| welcome_shadow_yoffset | <tt>0</tt> |
| welcome_shadow_color | <tt>#FFFFFF</tt> |
| intro_msg |
| intro_font | <tt>Verdana:size=14</tt> |
| intro_color | <tt>#FFFFFF</tt> |
| intro_x | <tt>-1</tt> |
| intro_y | <tt>-1</tt> |
| background_style | <tt>stretch</tt> |
| background_color | <tt>#CCCCCC</tt> |
| username_font | <tt>Verdana:size=12</tt> |
| username_color | <tt>#FFFFFF</tt> |
| username_x | <tt>-1</tt> |
| username_y | <tt>-1</tt> |
| username_msg | <tt>Please enter your username</tt> |
| username_shadow_xoffset | <tt>0</tt> |
| username_shadow_yoffset | <tt>0</tt> |
| username_shadow_color | <tt>#FFFFFF</tt> |
| password_x | <tt>-1</tt> |
| password_y | <tt>-1</tt> |
| password_msg | <tt>Please enter your password</tt> |
| msg_color | <tt>#FFFFFF</tt> |
| msg_font | <tt>Verdana:size=16:bold</tt> |
| msg_x | <tt>40</tt> |
| msg_y | <tt>40</tt> |
| msg_shadow_xoffset | <tt>0</tt> |
| msg_shadow_yoffset | <tt>0</tt> |
| msg_shadow_color | <tt>#FFFFFF</tt> |
| session_color | <tt>#FFFFFF</tt> |
| session_font | <tt>Verdana:size=16:bold</tt> |
| session_x | <tt>50%</tt> |
| session_y | <tt>90%</tt> |
| session_shadow_xoffset | <tt>0</tt> |
| session_shadow_yoffset | <tt>0</tt> |
| session_shadow_color | <tt>#FFFFFF</tt> |

## Források

*   [SLiM weboldala](http://slim.berlios.de/) (angol)
*   [SLiM dokumentáció](http://slim.berlios.de/manual.php) (angol)

## Segítség

*   [Magyar Arch Linux oldal](http://archlinux.fsf.hu/)
*   [Linux Empire Archlinux fóruma](http://www.linuxempire.hu/viewforum.php?f=36)