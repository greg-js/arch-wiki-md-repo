## Contents

*   [1 Introduzione](#Introduzione)
*   [2 Installazione](#Installazione)
*   [3 OpenGL e sistemi a 64Bit](#OpenGL_e_sistemi_a_64Bit)
*   [4 Collegamenti utili](#Collegamenti_utili)

## Introduzione

[Google Earth](http://earth.google.it/) è un software che visualizza tramite una rappresentazione tridimensionale della terra, i vari luoghi del nostro pianeta attraverso le mappe disponibili anche su [Google Maps](http://maps.google.com). Google Earth è presente su [AUR](/index.php/AUR "AUR") come [PKGBUILD](/index.php/PKGBUILD "PKGBUILD") non supportato. Richiede ovviamente che sia abilitata l'accelerazione hardware del server [X](/index.php/Xorg "Xorg").

## Installazione

Sono disponibili i tarball su [AUR](/index.php/AUR "AUR")

*   [google-earth](https://aur.archlinux.org/packages/google-earth/) (per i686)
*   [bin32-google-earth](https://aur.archlinux.org/packages/bin32-google-earth/) (per x86_64)

Una volta scaricati, estraete in una cartella nella vostra home, dopodichè entrateci da terminale, compilate e installate con il solito procedimento tramite [makepkg](/index.php/Makepkg "Makepkg").

32 bit:

```
tar -zxvf google-earth.tar.gz
cd google-earth
makepkg -cs
pacman -U *.pkg.tar.gz

```

64 bit:

```
tar -zxvf bin32-google-earth.tar.gz
cd bin32-google-earth
makepkg -cs
pacman -U *.pkg.tar.gz

```

## OpenGL e sistemi a 64Bit

Se utilizzate driver proprietari nVidia o ATI su sistemi a 64bit, non dimenticate di installare le librerie a 32bit [lib32-catalyst-utils](https://aur.archlinux.org/packages/lib32-catalyst-utils/) da [AUR](/index.php/AUR "AUR") o il pacchetto [lib32-nvidia-utils](https://www.archlinux.org/packages/?name=lib32-nvidia-utils) dal repository [community], altrimenti andrete incontro a malfunzionamenti in Google-Earth. Se usate driver open invece, dovrete usare il pacchetto [lib32-libgl-git](https://aur.archlinux.org/packages/lib32-libgl-git/).

## Collegamenti utili

1.  [Arch Build System (Italiano)](/index.php/Arch_Build_System_(Italiano) "Arch Build System (Italiano)")
2.  [Pacman (Italiano)](/index.php/Pacman_(Italiano) "Pacman (Italiano)")
3.  [Makepkg (Italiano)](/index.php/Makepkg_(Italiano) "Makepkg (Italiano)")