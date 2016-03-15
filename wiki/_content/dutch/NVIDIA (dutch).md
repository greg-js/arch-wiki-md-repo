## Contents

*   [1 Installatie](#Installatie)
*   [2 Configuratie van X](#Configuratie_van_X)
*   [3 Problemen die mogelijk kunnen optreden](#Problemen_die_mogelijk_kunnen_optreden)
    *   [3.1 Hoe het NVIDIA Graphics startup-logo uit te zetten](#Hoe_het_NVIDIA_Graphics_startup-logo_uit_te_zetten)

## Installatie

De pakketten staan in het extra-repository, zet deze aan voor pacman. De X-server moet eerst afgesloten worden, anders kan de installatie niet voltooid worden en zullen de drivers niet werken. Normale drivers

```
pacman -S nvidia (voor de nieuwere kaarten)
pacman -S nvidia-legacy (voor de oudere kaarten)

```

Drivers voor een **-beyond** kernel

```
pacman -S nvidia-beyond (voor de nieuwere kaarten)
pacman -S nvidia-legacy-beyond (voor de oudere kaarten)

```

In de [README](http://download.nvidia.com/XFree86/Linux-x86/1.0-8762/README/appendix-a.html) op de Nvidia site kan gelezen worden welke kaarte ondersteund zijn.

Als er fouten optreden kan men kijken naar:

```
/var/log/nvidia-installer.log

```

## Configuratie van X

Bewerk het configuratiebestand `/etc/X11/xorg.conf`. Maak commentaar (zet een hekje voor) de volgende regels in de sectie 'modules': `GLcore` en `DRI`

Voeg aan de sectie 'modules' toe:

```
Load "glx"

```

Maak commentaar van de sectie `DRI`:

```
#Section "DRI"
# Mode 0666
#EndSection

```

Verander `Driver "nv"` in `Driver "nvidia"` Als het bestaat, maak dan commentaar van de `Chipset` optie (die is alleen nodig voor nv).

Dat was het. Voor fijnstelling, zie `/usr/share/doc/NVIDIA_GLX-1.0/README.txt`.

Voor een automatische configuratie kan je ook het volgende proberen:

```
# nvidia-xconfig

```

Start de X-server weer en test met 'glxgears' (onderdeel van mesa, installeer met pacman) of leuker, speel wat tuxracer (ook te installeren met pacman).

## Problemen die mogelijk kunnen optreden

**GCC updates**: De nvidia-module moet gecompileerd worden met dezelfde compiler die gebruikt is voor het compileren van de kernel. Bij een GCC update kan het dus zijn dat de nvidia-module niet gecompileerd kan worden totdat er een nieuw kernel is.
**Kernel updates**: Bij een kernelupdate moet de nvidia-module opnieuw gecompileerd worden.

### Hoe het NVIDIA Graphics startup-logo uit te zetten

Pas in de Device sectie van Xorg.conf aan. Voeg de volgende regels toe:

```
Option "NoLogo" "true"

```