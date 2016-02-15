## Contents

*   [1 Skype diegimas ir paleidimas](#Skype_diegimas_ir_paleidimas)
    *   [1.1 Skype diegimas 32-bitų procesoriams](#Skype_diegimas_32-bit.C5.B3_procesoriams)
    *   [1.2 Skype diegimas 64-bitų procesoriams](#Skype_diegimas_64-bit.C5.B3_procesoriams)
        *   [1.2.1 Rankinis būdas](#Rankinis_b.C5.ABdas)
    *   [1.3 Skype paleidimas](#Skype_paleidimas)
*   [2 Skype garsas](#Skype_garsas)
    *   [2.1 Skype garsas su PulseAudio (2.1+)](#Skype_garsas_su_PulseAudio_.282.1.2B.29)
    *   [2.2 Skype garsas su ALSA (2.0+)](#Skype_garsas_su_ALSA_.282.0.2B.29)

## Skype diegimas ir paleidimas

### Skype diegimas 32-bitų procesoriams

Norint įdiegti Skype pirmiausia reikia aktyvuoti officialų repozitą. Pagal nutylėjimą jis jau turėtų būti aktyvuotas, bet jei taip nėra, tą galima padaryti nuėmus _"#"_ faile `pacman.conf` šioms dviems eilutėms:

```
/etc/pacman.conf

```

```
...
[community]
Include = /etc/pacman.d/mirrorlist
...

```

Tuomet Skype įdiegiamas terminale įrašant:

```
# pacman -S skype

```

### Skype diegimas 64-bitų procesoriams

Skype officialiai yra siūlomas tik 32-bitų procesoriams, todėl officialiame repozite 64-bitų versijos nėra. Nepaisant to, pastarąją versiją galima įdiegti iš AUR repozito arba rankiniu būdu.

#### Rankinis būdas

Pirma sukurkime darbo katalogą:

```
$ cd ~ && mkdir temp-skype-install

```

Pašalinam visas ankstesnes Skype versijas:

```
$ sudo rm -rf /usr/share/skype/ && sudo rm -rf /usr/bin/skype

```

Tuomet atsisiunčiame Skype:

```
$ wget [http://www.skype.com/go/getskype-linux-beta-static](http://www.skype.com/go/getskype-linux-beta-static) 

```

Išskleidžiame archyvą:

```
$ tar xvf skype_static-2.1.0.81.tar.bz2 && cd skype_static-2.1.0.81 

```

Diegiame Skype:

```
$ sudo mkdir /usr/share/skype/ 
$ sudo mv avatars/ /usr/share/skype/ 
$ sudo mv icons/ /usr/share/skype/ 
$ sudo mv lang/ /usr/share/skype/ 
$ sudo mv sounds/ /usr/share/skype/ 
$ sudo mv skype /usr/bin/ 

```

Ištriname darbinį katalogą:

```
$ cd ~ && rm -rf temp-skype-install

```

**Note:** Jums taip pat reikės 32-bitų bibliotekų, kurias galima gauti komanda: # pacman -S lib32

### Skype paleidimas

Skype paleidimas nesudėtingas. Tiesiog terminale įveskite _skype_ arba du kartus spragtelkite pelės klavišu ant Skype ikonos darbastalyje arba programų meniu.

## Skype garsas

Skype nuo 2.0 versijos palaiko [ALSA](/index.php/ALSA "ALSA") ir nuo 2.1 - [PulseAudio](/index.php/PulseAudio "PulseAudio"). Ankstesnės versijos palaiko tik [OSS](/index.php/OSS "OSS").

### Skype garsas su PulseAudio (2.1+)

Viskas turėtų veikti kuo puikiausiai, jei ne, tuomet galima pasirinkti kitą įvesties įrenginį naudojant pavucontrol (iš pradžių gali tekti jį įdiegti).

Jei naudojate 64-bitų Skype versiją, jums taip pat reikės lib32-libpulse.

### Skype garsas su ALSA (2.0+)

Pagal nutylėjimą viskas turėtų veikti, jei ne, galima pakeisti garso įrenginį Skype nustatymuose. Jei Skype blokuoja jūsų garso plokštę, tuomet tereikia `~/.asoundrc` faile pridėti šias eilutes:

```
pcm.dmixout {
  # Just pass this on to the system dmix
  type plug
  slave {
     pcm "dmix"
  }
}

```

Tuomet paleidžiame Skype, nueiname į garso nustatymus ir pasirenkame dmixout kaip skambėjimo ir garso įrenginį.