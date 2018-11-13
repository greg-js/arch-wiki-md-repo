[feh](https://derf.homelinux.org/~derf/projects/feh/) yra lengvas ir galingas nuotraukų peržiūros įrankis, kuris taip pat gali būti naudojamas kaip darbastalio paveikslėlių tvarkyklė.

## Contents

*   [1 Diegimas](#Diegimas)
*   [2 Naudojimas](#Naudojimas)
    *   [2.1 Paveikslėlių peržiūros įrankis](#Paveikslėlių_peržiūros_įrankis)
    *   [2.2 Darbastalio užsklandos įrankis](#Darbastalio_užsklandos_įrankis)
        *   [2.2.1 Atsitiktinis darbastalio fonas](#Atsitiktinis_darbastalio_fonas)

## Diegimas

[feh](https://www.archlinux.org/packages/?name=feh) yra pasiekiamas **extra** saugykloje:

```
# pacman -S feh

```

## Naudojimas

feh yra pilnai konfigūruojamas. Jeigu norite sužinoti pilną operacijų sąrašą, terminale įvykdykite `feh --help`.

### Paveikslėlių peržiūros įrankis

Greitam paveikslėlių peržiūrėjimui kataloge, feh galite paleisti su sekančiais argumentais:

```
$ feh -g 640x480 -d -S filename /path/to/directory

```

*   -g argumentas priverčia paveikslėlius atvaizduoti nedidesnėje kaip 640x480 rezoliucijoje
*   -S filename argumentas surūšiuoja paveikslėlius pagal vardą

Tai tik vienas pavyzdys; egzistuoja daugiau parinkčių, kurios pagerina lankstumą.

### Darbastalio užsklandos įrankis

feh gali būti naudojamas darbastalio užsklandos paveikslui keisti tokioms langų tvarkyklėms, kurios tokios galimybės neturi, kaip [Openbox (Lietuviškai)](/index.php/Openbox_(Lietuvi%C5%A1kai) "Openbox (Lietuviškai)") arba [Fluxbox](/index.php/Fluxbox "Fluxbox").

Naudojant [GNOME](/index.php/GNOME "GNOME"), turite išjungti darbastalio Nautilus kontrolę. Lengviausias būdas yra paleisti tokią komandą:

```
$ gconftool-2 --set /apps/nautilus/preferences/show_desktop --type boolean false

```

Sekanti komanda yra pavyzdys, kaip galima pakeisti darbastalio foną:

```
$ feh --bg-scale /path/to/image.file

```

Kitos mastelio keitimo galimybės:

```
--bg-tile FILE
--bg-center FILE
--bg-seamless FILE

```

Norint atkurti darbastalio foną kitoje sesijoje, pridėkite sekančią eilutę paleisties faile (pvz.: `~/.xinitrc`, `~/.config/openbox/autostart.sh`, kt.):

```
sh ~/.fehbg &

```

#### Atsitiktinis darbastalio fonas

Norint atsitiktinai keisti darbastalio fonus, sukurkite skriptą su sekančiu kodu (pvz.: `wallpaper.sh`). Suteikite jam paleisties teises (`chmod +x wallpaper.sh`) ir paleiskite jį iš `~/.xinitrc`. Skriptą galite tiesiogiai rašyti į `~/.xinitrc`, nebūtinai jį rašyti į `wallpaper.sh`.

Pakeiskite `$HOME/.wallpaper` direktoriją į jums tinkamą ir "15m" (15 minučių) intervalą tarp darbastalio fonų keitimosi (peržiūrėkite [sleep(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/sleep.1) papildomoms opcijoms).

```
#!/bin/sh
while true;
do
   find $HOME/.wallpaper -type f -name '*.jpg' -o -name '*.png' | shuf -n 1 | xargs feh --bg-scale
   sleep 15m
done &

```

Jeigu jūsų failuose yra tarpai tarp vardų, pabandykite sekantį kodą:

```
#!/bin/sh
while true;
do
   feh --bg-scale "$(find ~/.wallpaper -name *.jpg | shuf -n 1)"
   sleep 15m
done &

```