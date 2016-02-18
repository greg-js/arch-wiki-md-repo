E17 je vývojovou větví 17 (Development Release 17 - DR17) desktopového prostředí Enlightenment.

E17 se v současnosti intenzivně vyvíjí, je ve stádiu pre-alpha. Přestože je docela mladé, je docela stabilní. Mnoho lidí jej denně používá.

Nové verze jsou denně dostupné v SVN. SVN snapshoty jsou také z důvodu snadné instalace dostupné v repozitářích community - instalační instrukce jsou uvedené níže.

## Contents

*   [1 Instalace E17 z repozitářů community](#Instalace_E17_z_repozit.C3.A1.C5.99.C5.AF_community)
    *   [1.1 Častější upgrade balíčků e17](#.C4.8Cast.C4.9Bj.C5.A1.C3.AD_upgrade_bal.C3.AD.C4.8Dk.C5.AF_e17)
*   [2 Instalace E17 pomocí easy_e17.sh](#Instalace_E17_pomoc.C3.AD_easy_e17.sh)
    *   [2.1 Update_e17.sh](#Update_e17.sh)
    *   [2.2 Nastavení Entrance](#Nastaven.C3.AD_Entrance)
*   [3 Instalace témat](#Instalace_t.C3.A9mat)
*   [4 Problémy](#Probl.C3.A9my)
*   [5 Externí odkazy](#Extern.C3.AD_odkazy)

## Instalace E17 z repozitářů community

*   Nejdříve editujte soubor /etc/pacman.conf a odkomentujte repozitáře community odstraněním znaku # na začátku řádku; mělo by to vypadat nějak takto:

```
[community]
# Add your preferred servers here, they will be used first
Include = /etc/pacman.d/mirrorlist

```

*   Nyní synchronizujte pacmana a proveďte upgrade systému:

```
pacman -Syu

```

*   Instalujte skupinu e17:

```
pacman -S e-svn

```

*   Instalujte moduly a aplikace e17:

```
pacman -S desktop-file-utils e17-extra-svn

```

*   Instalujte fonty, aby se zabránilo problémům při prvním spuštění e17:

```
pacman -S artwiz-fonts ttf-ms-fonts

```

*   Pokud potřebujete balíček e17, který ještě není dostupný v repozitáři [community], podívejte se, zda není dostupný v repozitáři [AUR](https://aur.archlinux.org/).

Nyní v souboru **~/.xinitrc** povolte spuštění prostředí *enlightenment*:

```
...
# exec gnome-session
# exec startkde
# exec startxfce4
# ...or the Window Manager of your choice
exec enlightenment_start

```

Pokud jako přihlašovací manažer chcete použít *entrance* (náhradou za [KDM](/index.php/KDM "KDM")/[GDM](/index.php/GDM "GDM")), lze to nastavit v souboru:

*   **/etc/rc.conf** - přihlašovací manažer bude dostupný pouze po startu systému, nikoliv po stisku kláves CTRL+ALT+BACKSPACE

```
...
DAEMONS=(... entranced)
...

```

NEBO v souboru:

*   **/etc/inittab** - doporučený způsob

```
...
## Only one of the following two lines can be uncommented!
# Boot to console                                         
#id:3:initdefault:                                        
# Boot to X11                                             
id:5:initdefault:

...

# Example lines for starting a login manager
#x:5:respawn:/usr/bin/xdm -nodaemon
#x:5:respawn:/usr/sbin/gdm -nodaemon
#x:5:respawn:/usr/bin/kdm -nodaemon
#x:5:respawn:/usr/bin/slim >& /dev/null
#x:5:once:/bin/su johndoe -l -c "/bin/bash --login -c startx >/dev/null 2>&1"
x:5:respawn:/usr/sbin/entranced --nodaemon >& /dev/null

```

Poznámka: e17 je stále ve verzi alfa. Vše nemusí fungovat podle očekávání. Všechny balíčky jsou sice před přidáním do repozitáře [community] otestovány, některé věci mohou i tak přestat fungovat. Je doporučeno ponechat si balíčky z předchozích verzí v počítači, aby byl v případě potřeby možný downgrade.

Pokud nastanou nějaké problémy, lze postupovat následovně: nejdříve si ověřte, zda se problém projevuje i s defaultním tématem. Dále odstraňte adresář ~/.e (nejdříve si udělejte zálohu). Pokud jste našli chybu, ohlašte ji prosím vývojářům. Pokud nemáte jistotu, zda je chyba v softwaru nebo v balíčku, ohlaste ji do [community] bug trackeru.

#### Častější upgrade balíčků e17

Můžete si svoje vlastní balíčky Arch Linux e17 vytvářet malým skriptem, napsaným v pythonu, který se jmenuje ArchE17\. Další informace a download poslední verze: [https://dev.archlinux.org/~ronald/e17.html](https://dev.archlinux.org/~ronald/e17.html)

## Instalace E17 pomocí easy_e17.sh

Důvodem pro použití této metody místo dříve zmíněných je možnost větší kontroly nad E17 při aktualizaci. Umožňuje instalovat komponenty z repozitářů E17 bez nutnosti vytváření nových PKGBUILDů pro balíčky. Tento skript umožňuje odinstalovat vše, co bylo jeho pomocí nainstalováno. Další informace viz [vlákno na ubuntuforums.org](http://ubuntuforums.org/showthread.php?t=916690).

Instalace E17 skriptem easy_e17: [stáhněte si tarball z AUR](https://aur.archlinux.org/packages.php?ID=22793), rozbalte jej do nového adresáře, spusťte makepkg. Dále spusťte jako root:

```
 pacman -U *.pkg.tar.gz.

```

Zodpovězte několik otázek, potom proběhne instalace. Do souboru .xinitrc je nutné ke spuštění E17 přidat řádek:

```
exec /opt/e17/bin/enlightenment_start

```

Doporučuje se do proměnné cesty PATH přidat /opt/e17/bin, aby šlo spouštět programy bez nutnosti zadávat cestu /opt/e17/bin před jejich název: v souboru /etc/profile upravte řádek:

```
PATH="/bin:/usr/bin:/sbin:/usr/sbin"

```

na:

```
PATH="/bin:/usr/bin:/sbin:/usr/sbin:/opt/e17/bin"

```

Pokud narazíte na nějaké problémy s instalací E17, nejdříve se přesvědčte, zda to není problém závislostí. Pokud ano, doinstalujte závislost a pokračujte v instalaci e17 pomocí příkazu, spuštěného jako root:

```
easy_e17.sh -i

```

K instalaci jedné nebo více aplikací z repozitáře E17 svn jednoduše odstraňte jméno programu ze souboru /etc/easy_e17.conf a potom spusťte jako root příkaz (nahraďte jméno a jméno2 jménem programu, který jste odstranili ze souboru easy_e17.conf):

```
easy_e17.sh -i --only=*jméno*,*jméno2*

```

Update E17 lze provést (bez použití níže uvedeného programu) příkazem, spuštěným jako root:

```
easy_e17.sh -u

```

### Update_e17.sh

Další balíček je OzOsův skript update_e17.sh, který je praktický při použití s easy_e17, protože umožňuje zálohovat a obnovit strom E17 svn (v případě havárie), vrátit se zpět k určité revizi (opět v případě havárie) nebo jen k upozornění, že je ve stromu E17 svn k dispozici nová revize. Pro detailnější informace navštivte [tuto stránku](http://cafelinux.org/OzOs/content/how-administer-your-ozos-e17-desktop). Instalace viz výše uvedeným způsobem z repozitáře AUR [tímto balíčkem](https://aur.archlinux.org/packages.php?ID=23227).

### Nastavení Entrance

Pokud instalujete e17 pomocí skriptu easy_e17.sh, je nutné provést pro funkčnost entrance další nastavení.

**Nastavení entrance jako přihlašovací manažer** viz postup, uvedený výše. Do souboru `/etc/inittab` vložte řádek:

```
x:5:respawn:/usr/sbin/entranced --nodaemon >& /dev/null

```

Pokud chcete spustit entrance jako daemon, vložte soubor [entranced](https://repos.archlinux.org/wsvn/community/entrance-svn/trunk/entranced) z [entrance-git](https://aur.archlinux.org/packages/entrance-git/) do adresáře `/etc/rc.d/` a přidejte jej do řetězce DAEMONS v souboru `/etc/rc.conf`.

Nejdříve je nutné **povolit ověření přes PAM**. Stáhněte si [entrance.pam](https://repos.archlinux.org/wsvn/community/entrance-svn/trunk/entrance.pam) z balíčku [entrance-git](https://aur.archlinux.org/packages/entrance-git/) a uložte jej jako `/etc/pam.d/entrance`.

Další dva odstavce jsou **jen doplňující informace**, pokud spěcháte, klidně je přeskočte.

Nyní probíha spouštění i ověřování uživatelů korektně. Jak jste si všimli, po ověření entrance zmizí a vrátí se zpět. Důvod je ten, že entrance neví, co po ověření spustit. Toto se nastaví pomocí souboru `/etc/X11/Xsession` (lze nastavit během kompilace pomocí ENTRANCE_XSESSION) a pomocí souborů .desktop v adresářích xsessions. Adresáře xsessions, které entrance prochází: `/opt/e17/etc/xsessions/` (lze nastavit během kompilace pomocí ENTRANCE_SESSIONS_DIR), `$XDG_DATA_HOME/xsessions/` a všechny další `xsessions` adresáře ve vašem $XDG_DATA_DIRS.

Entrance umožňuje výběr z více sezení, která jsou definována pomocí souborů .desktop v adresářích xsessions. Po úspěšném ověření uživatele entrance spustí soubor `/etc/X11/Xsession` a jako parametr přidá řetězec podle zvoleného sezení. Pokud jako sezení zvolíte *Default*, je to sekce "default" nebo jen prázdný řetězec, zatímco *Failsafe* provede sekci "failsafe". Pro ostatní sezení je to řádek *exec* v souboru .desktop.

Nyní musíme **konfigurovat sezení X11**. Vytvoříme soubor `/etc/X11/Xsession` a nastavíme jej jako spustitelný

```
touch /etc/X11/Xsession
chmod +x /etc/X11/Xsession  # toto je důležité!

```

Lze použít modifikovanou verzi skriptu Xsession pro KDM (základní verze je v [gentoo bug trackeru](http://bugs.gentoo.org/show_bug.cgi?id=301051)):

 `/etc/X11/Xsession` 
```
 #! /bin/sh
 # Xsession - run as user

 session=${1:-default}

 # Note that the respective logout scripts are not sourced.
 case $SHELL in
   */bash)
     [ -z "$BASH" ] && exec $SHELL $0 "$@"
     set +o posix
     [ -f /etc/profile ] && . /etc/profile
     if [ -f $HOME/.bash_profile ]; then
       . $HOME/.bash_profile
     elif [ -f $HOME/.bash_login ]; then
       . $HOME/.bash_login
     elif [ -f $HOME/.profile ]; then
       . $HOME/.profile
     fi
     ;;
   */zsh)
     [ -z "$ZSH_NAME" ] && exec $SHELL $0 "$@"
     emulate -R zsh
     [ -d /etc/zsh ] && zdir=/etc/zsh || zdir=/etc
     zhome=${ZDOTDIR:-$HOME}
     # zshenv is always sourced automatically.
     [ -f $zdir/zprofile ] && . $zdir/zprofile
     [ -f $zhome/.zprofile ] && . $zhome/.zprofile
     [ -f $zdir/zlogin ] && . $zdir/zlogin
     [ -f $zhome/.zlogin ] && . $zhome/.zlogin
    ;;
   */csh|*/tcsh)
     # [t]cshrc is always sourced automatically.
     # Note that sourcing csh.login after .cshrc is non-standard.
     xsess_tmp=`mktemp /tmp/xsess-env-XXXXXX`
     $SHELL -c "if (-f /etc/csh.login) source /etc/csh.login; if (-f ~/.login) source ~/.login; /bin/sh -c export -p >! $xsess_tmp"
     . $xsess_tmp
     rm -f $xsess_tmp
     ;;
   *) # Plain sh, ksh, and anything we do not know.
     [ -f /etc/profile ] && . /etc/profile
     [ -f $HOME/.profile ] && . $HOME/.profile
     ;;
 esac

 [ -f /etc/xprofile ] && . /etc/xprofile
 [ -f $HOME/.xprofile ] && . $HOME/.xprofile

 # run all system xinitrc shell scripts.
 if [ -d /etc/X11/xinit/xinitrc.d ]; then
     for i in /etc/X11/xinit/xinitrc.d/* ; do
         if [ -x "$i" ]; then
             . "$i"
         fi
     done
 fi

 case $session in
   "")
     exec xmessage -center -buttons OK:0 -default OK "Sorry, $DESKTOP_SESSION is no valid session."
     ;;
   failsafe)
     exec xterm -geometry 80x24-0-0
     ;;
   custom)
     exec $HOME/.xsession
     ;;
   default)
     exec /opt/e17/bin/enlightenment_start
### if you have installed enlightenment via pacman and want to youse this Xsession, the line above would be: ###
#    exec /usr/bin/enlightenment_start
     ;;
   *)
     eval exec "$session"
     ;;
 esac
 exec xmessage -center -buttons OK:0 -default OK "Sorry, cannot execute $session. Check $DESKTOP_SESSION.desktop."

```

Po restartu je vše připraveno a po ověření uživatele volba sezení *Default* spustí E.

## Instalace témat

Témata pro změnu vzhledu e17 jsou dostupná na serveru [exchange.enlightenment.org](http://exchange.enlightenment.org/). Také se podívejte na [e17-stuff.org](http://www.e17-stuff.org).

Témata lze instalovat (ve formátu .edj) z konfiguračního dialogu.

Téma lze také změnit téma pro etk toolkit (ten, který používá exhibit). Dialog pro změnu vzhledu etk toolkitu se spustí příkazem /usr/bin/etk_prefs

Balíček [e17-themes](https://aur.archlinux.org/packages/e17-themes/) z AUR stáhne a nainstaluje mnoho témat ze serveru exchange.enlightenment.org

## Problémy

*   Pokud v X nejsou dostupné X kurzory, nainstalujte balíček 'libxcursor'.
*   Pokud screenlock neakceptuje vaše heslo, přidejte do souboru /etc/pam.d/enlightenment:

```
auth required pam_unix_auth.so

```

## Externí odkazy

*   [Exchange.enlightenment.org je nový, integrovaný server, který nahradil dřívější get-e.org. get-e.org skončil v srpnu 2008.](http://exchange.enlightenment.org/)
*   [e17-stuff.org - témata, pozadí atd.](http://e17-stuff.org/)
*   [Článek o Entrance na oficiální E17 wiki](http://trac.enlightenment.org/e/wiki/Entrance)