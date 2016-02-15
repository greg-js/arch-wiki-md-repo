**MPlayer** je populární přehrávač videa pro GNU/Linux. Podporuje všechny možné dostupné video a audio formáty a je velmi všestranný. Většina uživatelů jej používá pro přehrávání videa.

## Contents

*   [1 Instalace](#Instalace)
*   [2 Instalační tipy](#Instala.C4.8Dn.C3.AD_tipy)
    *   [2.1 Grafická prostředí](#Grafick.C3.A1_prost.C5.99ed.C3.AD)
    *   [2.2 Integrace do prohlížeče](#Integrace_do_prohl.C3.AD.C5.BEe.C4.8De)
        *   [2.2.1 Firefox](#Firefox)
        *   [2.2.2 Konqueror](#Konqueror)
*   [3 Použití](#Pou.C5.BEit.C3.AD)
    *   [3.1 Konfigurace](#Konfigurace)
    *   [3.2 Průhledné video na kartě radeon s povoleným Composite](#Pr.C5.AFhledn.C3.A9_video_na_kart.C4.9B_radeon_s_povolen.C3.BDm_Composite)
    *   [3.3 Průhledný SMPlayer v Gnome s povoleným Composite](#Pr.C5.AFhledn.C3.BD_SMPlayer_v_Gnome_s_povolen.C3.BDm_Composite)
    *   [3.4 Streamované video](#Streamovan.C3.A9_video)
    *   [3.5 Podpora dvd menu v mplayeru - dvdnav](#Podpora_dvd_menu_v_mplayeru_-_dvdnav)
    *   [3.6 Streamované audio v mplayeru na jackd](#Streamovan.C3.A9_audio_v_mplayeru_na_jackd)
    *   [3.7 Klávesové zkratky](#Kl.C3.A1vesov.C3.A9_zkratky)
    *   [3.8 Automatické rozpoznání kódování titulků](#Automatick.C3.A9_rozpozn.C3.A1n.C3.AD_k.C3.B3dov.C3.A1n.C3.AD_titulk.C5.AF)
*   [4 Řešení problémů](#.C5.98e.C5.A1en.C3.AD_probl.C3.A9m.C5.AF)
    *   [4.1 Mplayer selže při otvírání souborů s mezerami v názvu](#Mplayer_sel.C5.BEe_p.C5.99i_otv.C3.ADr.C3.A1n.C3.AD_soubor.C5.AF_s_mezerami_v_n.C3.A1zvu)
*   [5 Externí odkazy](#Extern.C3.AD_odkazy)

## Instalace

Balíček [mplayer](https://www.archlinux.org/packages/?name=mplayer) je dostupný v repozitáři [extra]:

```
# pacman -S mplayer

```

Poslední vývojová verze je v repozitáři [AUR](/index.php/AUR "AUR") ([mplayer-svn](https://aur.archlinux.org/packages/mplayer-svn/)) volitelně s podporou vícevláknového FFmpeg (experimentální) ([mplayer-mt-lite-git](https://aur.archlinux.org/packages/mplayer-mt-lite-git/)).

## Instalační tipy

### Grafická prostředí

Existuje několik grafických prostředí pro MPlayer.

*   Qt: smplayer je v repozitáři extra. Jsou pro něj dostupná témata smplayer-themes.
*   Gtk+: pymp a gnome-mplayer jsou v repozitáři AUR a community v tomto pořadí.
*   gmplayer: toto prostředí již není v balíčku mplayer dostupné. Existuje alternativní balíček pro mplayer (mplayer-x) v AUR, ve kterém je gmplayer obsažen.

### Integrace do prohlížeče

Pokud chcete, aby MPlayer přehrával video ve vašem oblíbeném internetovém prohlížeči, nainstalujte si toto:

#### Firefox

```
# pacman -S gecko-mediaplayer

```

#### Konqueror

```
# pacman -S kmplayer

```

**Note:** Také nabízí kompletní rozhraní pro MPlayer.

## Použití

### Konfigurace

Systémová konfigurace je uložena v souboru `/etc/mplayer/mplayer.conf`, uživatelská nastavení jsou v souboru `~/.mplayer/config`. Příklad konfigurace je v souboru `/etc/mplayer/example.conf`.

Příklad konfigurace:

 `/etc/mplayer/example.conf` 

```
#profil pro mixování dvou-kanálového audia na šest kanálů
# aktivace parametrem -profile 2chto6ch
[2chto6ch]
af-add=pan=6:1:0:.4:0:.6:2:0:1:0:.4:.6:2

#profil pro mixování šesti-kanálového audia na dva kanály
# aktivace parametrem -profile 6chto2ch
[6chto2ch]
af-add=pan=2:0.7:0:0:0.7:0.5:0:0:0.5:0.6:0.6:0:0

#předvolená konfigurace pro každý soubor
[default]
#použít X11 pro výstup videa
vo=x11
#výstup audia
ao=alsa
#preferovat použití šesti-kanálového audia
channels = 6
#velikost titulků na 3% velikosti obrazovky
subfont-text-scale = 3
#nikdy nepoužít konfiguraci písma
nofontconfig = 1
#přidat černé okraje, aby video mělo na monitoru korektní poměr stran
#změnit, pokud váš monitor není 16/9
vf-add=expand=::::1:16/9:16
```

### Průhledné video na kartě radeon s povoleným Composite

Aby šlo použít průhledný výstup videa v X je nutné v mplayeru povolit dekorované video:

```
$ mplayer -vo xv:adaptor=1 <File>

```

Nebo přidat následující řádek do souboru `~/.mplayer/config`:

```
vo=xv:adaptor=1

```

Ke zjištění, jaké grafické režimy vaše grafická karta podporuje můžete použít program xvinfo.

### Průhledný SMPlayer v Gnome s povoleným Composite

Pokud se při použití compiz a panelu cairo-dock v smplayeru nezobrazuje video a funguje pouze audio, je nutný následující postup: [kopírovat/vložit do terminálu]

```
   sudo bash -c “cat > /usr/bin/smplayer.helper” <<EOF
   export XLIB_SKIP_ARGB_VISUALS=1
   exec smplayer.real “\$@”
   EOF
   sudo chmod 755 /usr/bin/smplayer.helper
   sudo mv /usr/bin/smplayer{,.real}
   sudo ln -sf smplayer.helper /usr/bin/smplayer

```

Pokud nechcete použít příkaz sudo, použijte “su” pro přihlášení pod uživatelem root - další postup viz výše.

### Streamované video

Pokud chcete sledovat streamované video, (např. odkazy *.asx):

```
$ mplayer -playlist link-to-stream.asx 

```

Playlisty streamů nelze použitím parametru -playlist přehrát.

### Podpora dvd menu v mplayeru - dvdnav

Pokud chcete použít mplayer s podporou dvdnav, aby mohl otvírat dvd menu, použijte následující syntaxi:

```
$ mplayer -nocache dvdnav://

```

### Streamované audio v mplayeru na jackd

Editujte soubor `~/.mplayer/config` a přidejte:

ao=jack

### Klávesové zkratky

	_Toto je seznam nejzákladnějších kláves programu MPlayer._

| Key | Description |
| p | Pauza/přehrát. |
| Space | Pauza/přehrát. |
| Backspace | Návrat do menu při použití dvdnav. |
| Left | Posun 10 vteřin zpět. |
| Right | Posun 10 vteřin vpřed. |
| Down | Posunt minutu zpět. |
| Up | Posunt minutu vpřed. |
| < | Zpět v playlistu. |
| > | Vpřed v playlistu. |
| m | Ztišit zvuk. |
| 0 | Zvýšit hlasitost. |
| 9 | Snížit hlasitost. |
| f | Přepnout do módu fullscreen. |
| o | Přepnout stav OSD. |
| j | Přepnout zobrazování titulků. |
| `I` | Zobrazit název souboru. |
| 1, 2 | Upravit kontrast. |
| 3, 4 | Upravit jas. |

### Automatické rozpoznání kódování titulků

Mplayer podporuje automatické rozpoznávání titulků. Pomocí knihovny [enca](http://trific.ath.cx/software/enca/).

Spustíme s parametrem subcp

```
mplayer -subcp enca:cs:cp1250 

```

Nebo můžeme přidat subcp do _/etc/mplayer/mplayer.conf_

```
subcp=enca:cs:cp1250

```

*   cs je kód jazyka

*   cp1250 je kódování, co se použije v případě selhání autodetekce.

## Řešení problémů

### Mplayer selže při otvírání souborů s mezerami v názvu

Pokud se pokusíte otevřít soubor, který má v názvu mezery (např. The Movie) a mplayer selže s hláškou, že nelze otevřít soubor (file:///The%20Movie), kde jsou všechny mezery zkonvertované na znak %20:

editujte soubor `/usr/share/applications/mplayer.desktop` a změňte tento řádek:

```
Exec=mplayer %U

```

na:

```
Exec=mplayer %F

```

Pokud používáte grafické prostředí, vložte jméno prostředí do: Exec=GUI jméno %F.

## Externí odkazy

*   [Oficiální stránka MPlayeru](http://www.mplayerhq.hu/)
*   [často kladené otázky](http://www.abclinuxu.cz/clanky/multimedia/na-co-se-casto-ptame-mplayer)
*   [manuálová stránka (v češtině)](http://www.mplayerhq.hu/DOCS/man/cs/mplayer.1.html)