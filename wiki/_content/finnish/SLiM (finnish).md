| **Summary**  |
| Yleiskatsaus yksinkertaisesta sisäänkirjautumismanagerista. |
| **Related** |
| [Display Manager](/index.php/Display_Manager "Display Manager") |

[SLiM](http://slim.berlios.de/) on akronyymi sanoista (Simple Login Manger), mikä tarkoittaa suomeksi helppo sisäänkirjautumismanageri. [SLiM](/index.php/SLiM "SLiM") on yksinkertainen, kevyt ja helposti muokattavissa. Kevyen työpöytäympäristön käyttäjät voivat valita [SLiM](/index.php/SLiM "SLiM"):in kirjatumismanageriksi. [SLiM](/index.php/SLiM "SLiM") on kevyt sisäänkirjatumismanagerii, koska sillä ei ole riippuvaisuuksia.

## Contents

*   [1 Asennus](#Asennus)
*   [2 Asetukset](#Asetukset)
    *   [2.1 Käyttöönotto](#K.C3.A4ytt.C3.B6.C3.B6notto)
    *   [2.2 Ympäristöt](#Ymp.C3.A4rist.C3.B6t)
    *   [2.3 Automaattinen sisäänkirjautuminen](#Automaattinen_sis.C3.A4.C3.A4nkirjautuminen)
    *   [2.4 Monta työpöytäympäristöä](#Monta_ty.C3.B6p.C3.B6yt.C3.A4ymp.C3.A4rist.C3.B6.C3.A4)
    *   [2.5 Teemat](#Teemat)
        *   [2.5.1 Kahden näytön asetukset](#Kahden_n.C3.A4yt.C3.B6n_asetukset)
*   [3 Lisätietoja](#Lis.C3.A4tietoja)

## Asennus

Asennetaan [slim](https://www.archlinux.org/packages/?name=slim) extra repositoriosta.

```
# pacman -S slim

```

## Asetukset

### Käyttöönotto

[SLiM](/index.php/SLiM "SLiM") voidaan käynnistää, joko palveluna `rc.conf` tai muokkaamalla tiedostoa `inittab`. Katso [Display manager](/index.php/Display_manager "Display manager") Löytääksesi enemmän tietoa.

### Ympäristöt

Asettaaksesi [SLiM](/index.php/SLiM "SLiM") käynnistysmanagerin tietylle työpöytäympäristölle, pitää tiedostoa `~/.xinitrc` muokata sopivaksi:

```
#!/bin/sh

#
# ~/.xinitrc
#
# Executed by startx (run your window manager from here)
#

exec [session-command]

```

[SLiM](/index.php/SLiM "SLiM") lukee tiedoston `~/.xinitrc` asetukset, jonka jälkeen työpöytä käynnistetään.See [Xinitrc](/index.php/Xinitrc "Xinitrc").

Muokkaa `[session-command]` sopivaksi istunto komennoksi. Seuraavaksi esimerkkejä istunto komennosta:

```
exec awesome
exec fluxbox
exec fvwm2
exec gnome-session
exec openbox-session
exec startkde
exec startlxde
exec startxfce4

```

Jos tästä puuttuu tarvitsemasi komento, voit yrittää etsiä sitä työpöytäympäristön wikistä.

### Automaattinen sisäänkirjautuminen

[SLiM](/index.php/SLiM "SLiM") voidaan asettaa automaattisesti sisäänkirjatumaan käyttäjänä. Se tehdään muokkaamalla `/etc/slim.conf` tiedostoa. Seuraavia oletusasetuksia muokataan:

```
# default_user        simone

```

Poista kommenttimerkki (#) ja vaihda "simone" halutuksi käyttäjäksi.

```
# auto_login          no

```

Poista kommenttimerkki (#) ja vaihda "no" "yes" sanaksi.

### Monta työpöytäympäristöä

Jos halutaan sisäänkirjautumisen yhteydessä valita työpöytäympäristö voidaan se tehdä muokkaamalla tiedostoa `~/.xinitrc`. Valinta tehdään F1 näppäimellä. Muista muokata `/etc/slim.conf` tiedostosta sessions muuttuja täsmäämään seuraavien asetusten kanssa. Huomio ominaisuus on kokeellinen.

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

### Teemat

Asenna [slim-themes](https://www.archlinux.org/packages/?name=slim-themes) paketti extra repositoriosta komennolla.

```
# pacman -S slim-themes archlinux-themes-slim

```

Paketti [archlinux-themes-slim](https://www.archlinux.org/packages/?name=archlinux-themes-slim) sisältää useita eri nimisiä teemoja. Katso tiedostoja kansiosta `/usr/share/slim/themes` nähdäksesi, mitä teemoja on saatavilla. Vaihda muuttuja 'current_theme' tiedostosta `/etc/slim.conf`:

```
#current_theme       default
current_theme       archlinux-simplyblack

```

Teemoja voi esikatsella, jos Xorg palvelin on käynnissä, seuraavalla komenolla:

```
$ slim -p /usr/share/slim/themes/<theme name>

```

Lopettaaksesi esikatselun kirjoita "exit" ja paina Enteriä.

Lisää teemapaketteja saatavilla [AUR](/index.php/AUR "AUR"):sta.

#### Kahden näytön asetukset

Voit muokata [SLiM](/index.php/SLiM "SLiM") teemaa /usr/share/slim/themes/<your-theme>/slim.theme vaihtaaksesi ne prosenttiarvoiksi. Sisäänkirjautumislaatikko on 450 kertaa 250 pikseliä.

```
input_panel_x           50%
input_panel_y           50%

```

Pikseli arvoiksi

```
# These settings set the "archlinux-simplyblack" panel in the center of a 1440x900 screen
input_panel_x           495
input_panel_y           325

```

```
# These settings set the "archlinux-retro" panel in the center of a 1680x1050 screen
input_panel_x           615
input_panel_y           400

```

Jos teemallasi on taustakuva, voit vaihtaa background_style asetusta ('stretch', 'tile', 'center' tai 'color') haluamaksesi. Voit hankkia lisätietoja teemojen muokkaamisesta [toiselta nettisivulta](http://slim.berlios.de/themes_howto.php)

## Lisätietoja

*   [SLiM homepage](http://slim.berlios.de/)
*   [SLiM documentation](http://slim.berlios.de/manual.php)