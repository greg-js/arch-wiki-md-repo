## Contents

*   [1 Popis](#Popis)
*   [2 Instalace](#Instalace)
*   [3 Audtool](#Audtool)
*   [4 GTK prostředí v Audacious 2](#GTK_prost.C5.99ed.C3.AD_v_Audacious_2)
*   [5 Standardní skiny](#Standardn.C3.AD_skiny)
    *   [5.1 Použití skinů pro Winamp](#Pou.C5.BEit.C3.AD_skin.C5.AF_pro_Winamp)
    *   [5.2 Přidání skinů z programu Winamp](#P.C5.99id.C3.A1n.C3.AD_skin.C5.AF_z_programu_Winamp)
*   [6 Přehrávání zvukových CD](#P.C5.99ehr.C3.A1v.C3.A1n.C3.AD_zvukov.C3.BDch_CD)
*   [7 Podpora OSS](#Podpora_OSS)

# Popis

[Audacious](http://audacious-media-player.org/) je rozšířená větev programu Beep Media Player. Je zdarma, odlehčený, založený na GTK2 a je zaměřený na kvalitu zvuku a podporu mnoha audio kodeků. Audacious lze rozšířit pomocí pluginů.

Vlastnosti:

*   Podpora velkého množství audio kodeků (a mnoha dalších s pluginem [xmp](https://aur.archlinux.org/packages/xmp/)),
*   Výstup na PulseAudio, ALSA, OSS, Crossfade (také do souboru či na null),
*   Převod WAV, Vorbis, Mp3, FLAC,
*   Zvukové efekty,
*   Vizualizace,
*   Scrobbler plugin, OSD, EvDev, stavová ikona, budík,
*   Podpora streamingu

# Instalace

Audacious 2.2.0 je dostupný z oficiálních repozitářů. Instalace programem [Pacman](/index.php/Pacman "Pacman"):

```
pacman -S audacious

```

Pluginy pro rozšíření schopností programu Audacious:

```
pacman -S audacious-plugins

```

# Audtool

Audacious je vybaven výborným nástrojem pro správu Audtool. Audtool lze použít pro získávání informací nebo na ovládání přehrávače.

Např. pro získání názvu skladby či jména interpreta lze použít příkaz:

```
audtool2 current-song

```

```
audtool2 current-song-tuple-data artist

```

Dále obsahuje funkce pro ovládání přehrávače, manipulaci s playlistem, eqalizérem a hlavním oknem. Všechny možnosti lze vypsat příkazem

```
audtool2 --help

```

# GTK prostředí v Audacious 2

Audacious 2 má možnost použití alternativních uživatelských prostředí. Pro použití nového GTK uživatelského prostředí spusťte audacious2 s parametrem

```
audacious2 -i gtkui

```

# Standardní skiny

## Použití skinů pro Winamp

Audacious podporuje klasické skiny z programu Winamp, takže v něm můžete libovolný použít. Spusťte Audacious s parametrem

```
audacious2 -i skinned

```

## Přidání skinů z programu Winamp

Přidání skinů z programu Winamp do Audacious je velice jednoduché. Zkopírujte váš skin (soubor ve formátu .zip, .wsz, .tgz, .tar.gz, či .tar.bz2) do adresáře **`/usr/share/audacious/Skins`**. Potom jej můžete vybrat z menu *Témata rozhraní* v *Nastavení*.

Skiny jsou dostupné na serverech:

[http://www.customize.org/list/winamp2](http://www.customize.org/list/winamp2)

[http://www.deviantart.com/#catpath=customization/skins/media/winamp/classic](http://www.deviantart.com/#catpath=customization/skins/media/winamp/classic)

[http://www.1001skins.com](http://www.1001skins.com)

# Přehrávání zvukových CD

```
pacman -S libcdio

```

Po instalaci libcdio Audacious dokáže přehrát zvuková CD z hlavní obrazovky (kliknout pravým tlačítkem) > Služby modulů > Přidat CD.

Odkazy: [https://bbs.archlinux.org/viewtopic.php?id=40075](https://bbs.archlinux.org/viewtopic.php?id=40075)

# Podpora OSS

Pokud místo ALSA používáte Open Sound System, ověřte si, zda je Audacious korektně nastaven. Zvolte: *Nastavení*-->*Zvuk*-->*Aktuální výstupní modul*-->***OSS Output Plugin***.