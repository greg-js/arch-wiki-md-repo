Related articles

*   [List of games](/index.php/List_of_games "List of games")
*   [Xorg](/index.php/Xorg "Xorg")

Šiame puslapyje yra informacija apie veikiančius žaidimus, bei sistemos konfiguracijos patarimai.

## Contents

*   [1 Žaidimų aplinkos](#Žaidimų_aplinkos)
*   [2 Žaidimų gavimas](#Žaidimų_gavimas)
    *   [2.1 Skaitmeninis platinimas](#Skaitmeninis_platinimas)
*   [3 Emuliatoriai](#Emuliatoriai)
    *   [3.1 Konsolės](#Konsolės)
    *   [3.2 Kita](#Kita)
*   [4 Žaidimų paleidimas](#Žaidimų_paleidimas)
    *   [4.1 Daugiaekranė sąranka](#Daugiaekranė_sąranka)
    *   [4.2 Klaviatūros sugriebimas](#Klaviatūros_sugriebimas)
    *   [4.3 Žaidimo paleidimas atskirame X serveryje](#Žaidimo_paleidimas_atskirame_X_serveryje)
    *   [4.4 Pelės aptikimo reguliavimas](#Pelės_aptikimo_reguliavimas)
    *   [4.5 Binaurinis garsas su OpenAL](#Binaurinis_garsas_su_OpenAL)
    *   [4.6 PulseAudio reguliavimas](#PulseAudio_reguliavimas)
        *   [4.6.1 Realaus laiko prioriteto ir neigiamo nice lygio įjungimas](#Realaus_laiko_prioriteto_ir_neigiamo_nice_lygio_įjungimas)
        *   [4.6.2 Aukštesnės kokybės atkūrimo naudojimas geresniam garsui](#Aukštesnės_kokybės_atkūrimo_naudojimas_geresniam_garsui)
        *   [4.6.3 Techninės įrangos buferių suderinimas su Pulse buferingu](#Techninės_įrangos_buferių_suderinimas_su_Pulse_buferingu)
    *   [4.7 Dukart patikrinkite procesoriaus dažnio mąstelio keitimo nustatymus](#Dukart_patikrinkite_procesoriaus_dažnio_mąstelio_keitimo_nustatymus)
*   [5 Kadrų skaičiaus ir reagavimo gerenimas su planavimo politika](#Kadrų_skaičiaus_ir_reagavimo_gerenimas_su_planavimo_politika)
    *   [5.1 Wine programoms](#Wine_programoms)
    *   [5.2 Visam kitam](#Visam_kitam)
        *   [5.2.1 Politikos](#Politikos)
        *   [5.2.2 Nice lygiai](#Nice_lygiai)
        *   [5.2.3 Core affinity](#Core_affinity)
        *   [5.2.4 Bendras atvejis](#Bendras_atvejis)
        *   [5.2.5 Optimus ir kitos padedančios programos](#Optimus_ir_kitos_padedančios_programos)
*   [6 Alternatyvūs branduoliai](#Alternatyvūs_branduoliai)
    *   [6.1 BFQ naudojimas](#BFQ_naudojimas)

## Žaidimų aplinkos

Linux egzistuoja keletas aplinkų skirtų žaisti žaidimams:

*   Vietinė – žaidimai parašyti Linux'ams.
*   Internetinė – žaidimai veikiantys interneto naršyklėje.
    *   HTML5 žaidimai naudoja kanvas bei WebGL technologijas ir veikia visose moderniose naršyklėse.
    *   [Flash](/index.php/Flash "Flash")-paremti – žaidimui reikia įdiegti įskiepį.
*   Specializuotos aplinkos (programinės įrangos emuliatoriai) – Reikalingos paleisti kitoms architektūroms ar sistemoms sukurtą programinę įrangą. Daugiau detalių rasite [list of emulators](/index.php/List_of_applications/Other#Emulators "List of applications/Other").
    *   [Wine](/index.php/Wine "Wine") - leidžia paleisti kai kuriuos Windows žaidimus, taip pat didelį kiekį kitos Windows programinės įrangos. Wine aplinkoje našumas varijuoja, dėl papildomų CPU sąnaudų kai kurie žaidimai gali sulėtėti, kitais atvejais veikimas pagreitėja. Dėl specifinės suderinanumo informacijos konsultuokitės su [Wine AppDB](http://appdb.winehq.org/).
    *   [Crossover Games](http://www.codeweavers.com/) - Codeweavers komandos nariai yra didžiuliai Wine rėmėjai. Naudojantis Crossover Games kai kurių žaidimų įdiegimas ir konfigūravimas tampa daug paprastesnis, patikimesnis ir netgi įmanomesnis, nei naudojantis kitais metodais. Crossover yra mokamas komercinis produktas, turintis ir [forumą](http://www.codeweavers.com/support/forums/) kur kūrėjai aktyviai dalyvauja bendruomės veikloje.
    *   [DOSBox](/index.php/DOSBox "DOSBox") yra minimali virtualioji mašina, kurioje veikia pilna DOS aplinka. Ją galima naudoti žaižiant klasikinius DOS žaidimus.
    *   [scummvm](https://www.archlinux.org/packages/?name=scummvm) tai daugybės klasikinių point-and-click nuotykių žaidimų viskas-viename variklio reimplementacija. Visą suderinamų žaidimų sąrašą rasite [ScummVM svetainėje](http://scummvm.org).
    *   Panašiai į ScummVM, varikli7 reimplementacijos ir portai egzistuoja specifiniams žaidimams, kaip Doom.
*   Virtualias mašinas galima naudoti suderinamų operacinių sistemų įdiegimui(pvz.: Windows). [VirtualBox](/index.php/VirtualBox "VirtualBox") turi gerą 3D palaikymą. Sekant iš to, jeigu turite suderinamą techninę įrangą galite išbandyti VGA pralaidą į Windows KVM svečia, raktinis žodis yra ["virtual function I/O" (VFIO)](https://www.kernel.org/doc/Documentation/vfio.txt), arba [PCI passthrough via OVMF](/index.php/PCI_passthrough_via_OVMF "PCI passthrough via OVMF").

## Žaidimų gavimas

Nemažą skaičių galima rasti [official repositories](/index.php/Official_repositories "Official repositories") / [AUR](/index.php/AUR "AUR"), žiūrėti [List of games](/index.php/List_of_games "List of games").

### Skaitmeninis platinimas

Vien dėl to, kad žaidimai prieinami Linux aplinkoje doesn't nereiškia, kad jie vietiniai, jie gali būti supakuoti kartu su Wine ar DOSBox.

*   **[Steam](/index.php/Steam "Steam")** — Valve sukurta skaitmeninio platinimo ir bendravimo platforma.

	[https://store.steampowered.com](https://store.steampowered.com) || [steam](https://www.archlinux.org/packages/?name=steam)

*   **[itch.io](https://en.wikipedia.org/wiki/itch.io "wikipedia:itch.io")** — Indie žaidimų parduotuvė.

	[https://itch.io/](https://itch.io/) || [itch](https://aur.archlinux.org/packages/itch/)

*   [GOG.com](https://www.gog.com/games/linux)
    *   GOG.com oficialiai palaiko tik Ubuntu ir Linux Mint.
    *   [lgogdownloader](https://aur.archlinux.org/packages/lgogdownloader/) paketas gali būti naudojamas GOG žaidimų įdiegimui iš komandinės eilutės.

## Emuliatoriai

Emuliatorius tai programa, kurios tikslas replikuoti kitos platformos ar sistemos funkcijas taip leidžiant veikti žaidimams bei programoms, kurie esamai aplinkai nesuprogramuoti.

Taip pat žiūrėti [Category:Emulation](/index.php/Category:Emulation "Category:Emulation") ir [Emulation General wiki](http://emulation.gametechwiki.com/index.php/Main_Page).

**Note:** Galimai naujesniam emuliatorių pasirinkimui, patikrinkite [AUR su žodžiu 'emulator'](https://aur.archlinux.org/packages/?O=0&SeB=nd&K=emulator&outdated=off&SB=n&SO=a&PP=50&do_Search=Go)

**Warning:** Legalu turėti aukšto lygio emuliatorių, tačiau bet koks autorinių teisių saugomų ROMų platinimas ar neautorizuotos emuliacijos (be rašytinio autorių leidimo naudoti) yra **nelegalu**. To pasekoje, Arch Linux neplatina autorinių teisų saugomo turinio, įskaitant žæidimų ROMus ir rip'intus konsolių BIOSus. Jūs esate visiškai atsakingi už bet kokį emuliatorių gautų iš [official repositories](/index.php/Official_repositories "Official repositories") arba [Arch User Repository](/index.php/Arch_User_Repository "Arch User Repository") naudojimą, taip pat už bet kokias teisines pasekmes to rezultate. Arch Linux neprisiima visiškai jokios atsakomybės.

### Konsolės

Taip pat žiūrėti [Wikipedia:List of video game console emulators](https://en.wikipedia.org/wiki/List_of_video_game_console_emulators "wikipedia:List of video game console emulators").

*   **Citra** — Nintendo 3DS emuliatorius.

	[http://citra-emu.org/](http://citra-emu.org/) || [citra-git](https://aur.archlinux.org/packages/citra-git/)

*   **DeSmuME** — Nintendo DS emuliatorius.

	[http://desmume.org/](http://desmume.org/) || [desmume](https://www.archlinux.org/packages/?name=desmume)

*   **[Dolphin](/index.php/Dolphin_emulator "Dolphin emulator")** — Labai galingas GameCube ir Wii emuliatorius.

	[http://dolphin-emu.org/](http://dolphin-emu.org/) || [dolphin-emu](https://www.archlinux.org/packages/?name=dolphin-emu)

*   **epsxe** — PlayStation žaidimų konsolės skirtos x86 PK techninei įrangai emuliatorius.

	[http://www.epsxe.com/](http://www.epsxe.com/) || [epsxe](https://aur.archlinux.org/packages/epsxe/)

*   **FCEUX** — NTSC ir PAL 8 bit Nintendo/Famicom emuliatorius, kuris yra originalaus FCE Ultra emuliatoriaus evoliucija. Tikslus, suderinamas ir aktyviai palaikomas.

	[http://fceux.com/](http://fceux.com/) || [fceux](https://www.archlinux.org/packages/?name=fceux)

*   **Gambatte** — Tikslus Game Boy Color emuliatorius

	[https://github.com/sinamas/gambatte](https://github.com/sinamas/gambatte) || Qt grafinė naudotojo sąsają ([gambatte-qt](https://aur.archlinux.org/packages/gambatte-qt/)), SDL komandinės eilutės sąsaja ([gambatte-sdl](https://aur.archlinux.org/packages/gambatte-sdl/)).

*   **Gens2** — Sega Genesis, Sega CD ir 32X emuliatorius parašytas assembly kalba ir aktyviai nebevystomas.

*   aktyvuokite OpenGL, nustatykite 1024x600 rezoliuciją ištemptimui pilnam ekrane arba 800x600 neištemptai;
*   naudokite "Normal" renderimą.

	[http://www.gens.me/](http://www.gens.me/) || [gens](https://www.archlinux.org/packages/?name=gens)

*   **Gens-GS** — Gens2, perrašytas su C++, sudedant skirtingų Gens šakų funkcijas į vieną.

	[http://segaretro.org/Gens/GS](http://segaretro.org/Gens/GS) || [gens-gs](https://www.archlinux.org/packages/?name=gens-gs)

*   **gngeo** — NeoGeo emuliatorius komandinėje eilutėje.

	[http://gngeo.googlecode.com](http://gngeo.googlecode.com) || [gngeo](https://aur.archlinux.org/packages/gngeo/)

*   **higan** — Daugiasistemis emuliatorius daugiausiai dėmesio skiriantis tikslumui, palaikantis SNES, NES, GB, GBC, GBA.

	[https://byuu.org/emulation/higan/](https://byuu.org/emulation/higan/) || [higan](https://www.archlinux.org/packages/?name=higan)

*   **mednafen** — Komandine eilute varomas daugiasistemis emuliatorius.

	[http://mednafen.sourceforge.net/](http://mednafen.sourceforge.net/) || [mednafen](https://www.archlinux.org/packages/?name=mednafen)

*   **Mupen64Plus** — Aukšto suderinamumo Nintendo 64 emuliatorius su įskiepių sistema.

	[http://www.mupen64plus.org/](http://www.mupen64plus.org/) || [mupen64plus](https://www.archlinux.org/packages/?name=mupen64plus) arba grafine sąsaja, kaip [m64py](https://aur.archlinux.org/packages/m64py/) ar [cutemupen](https://aur.archlinux.org/packages/cutemupen/).

*   **[Nestopia](/index.php/Nestopia "Nestopia")** — Labai tikslus NES emuliatorius.

	[http://0ldsk00l.ca/nestopia/](http://0ldsk00l.ca/nestopia/) || [nestopia](https://aur.archlinux.org/packages/nestopia/)

*   **pSX** — Įskiepiais neparemtas PlayStation emuliatorius su neblogu suderinamumu.

	[http://psxemulator.gazaxian.com/](http://psxemulator.gazaxian.com/) || [psx](https://aur.archlinux.org/packages/psx/)

*   **[PCSXR](/index.php/PCSX-Reloaded "PCSX-Reloaded")** — PlayStation emuliatorius; Debian atšaka nuo originalaus bet apleisto PCSX

	[http://pcsxr.codeplex.com/](http://pcsxr.codeplex.com/) || [pcsxr](https://aur.archlinux.org/packages/pcsxr/)

*   **PCSX2** — PlayStation 2 emuliatorius. Visdar palaikomas ir vystomas. Reikalingi BIOS failai.

	[http://www.pcsx2.net/](http://www.pcsx2.net/) || [pcsx2](https://www.archlinux.org/packages/?name=pcsx2)

*   **PPSSPP** — PlayStation Portable emuliatorius.

	[http://ppsspp.org/](http://ppsspp.org/) || [ppsspp](https://www.archlinux.org/packages/?name=ppsspp)

*   **Snes9x** — Nešiojamos, nemokamos Super Nintendo Entertainment System (SNES) emuliatorius.

	[http://www.snes9x.com/](http://www.snes9x.com/) || [snes9x](https://www.archlinux.org/packages/?name=snes9x)

*   **[Visual Boy Advance](/index.php/Visual_Boy_Advance "Visual Boy Advance")** — Game Boy emuliatorius su Game Boy Advance, Game Boy Color, ir Super Game Boy palaikymu.

	[http://vba.ngemu.com/](http://vba.ngemu.com/) || [vbam-wx](https://www.archlinux.org/packages/?name=vbam-wx)

*   **ZSNES** — Aukšo suderinamumo Super Nintendo emuliatorius.

	[http://www.zsnes.com/](http://www.zsnes.com/) || [zsnes](https://www.archlinux.org/packages/?name=zsnes)

### Kita

*   **DOSBox** — Atviro kodo DOS emuliatorius su pirmine užduotimi paleisti DOS žaidimus.

	[http://www.dosbox.com/](http://www.dosbox.com/) || [dosbox](https://www.archlinux.org/packages/?name=dosbox)

*   **DOSEmu** — Atviro kodo DOS emuliatorius.

	[http://www.dosemu.org/](http://www.dosemu.org/) || [dosemu](https://www.archlinux.org/packages/?name=dosemu)

*   **MAME** — Multiple Arcade Machine Emuliatorius.

	[http://mamedev.org/](http://mamedev.org/) || [mame](https://www.archlinux.org/packages/?name=mame)

*   **ResidualVM** — Kliaplatformis 3D žaidimo vertiklis kuris leiia žaisti LucasArts' Lua-paremtus 3D nuotykius.

	[http://residualvm.org/](http://residualvm.org/) || [residualvm](https://aur.archlinux.org/packages/residualvm/)

*   **[RetroArch](/index.php/RetroArch "RetroArch")** — Libretro frontend'as (emuliacijos biblioteka, naudojanti modifikuotas egzistuojančių emuliatorių versijas kaip įskiepius).

	[http://www.libretro.com/](http://www.libretro.com/) || [retroarch](https://www.archlinux.org/packages/?name=retroarch)

*   **ScummVM** — Virtuali mašina seniems nuotykiams.

	[http://www.scummvm.org/](http://www.scummvm.org/) || [scummvm](https://www.archlinux.org/packages/?name=scummvm)

*   **X Neko Project II** — PC-9801 emuliatorius.

	[http://www.asahi-net.or.jp/~aw9k-nnk/np2/](http://www.asahi-net.or.jp/~aw9k-nnk/np2/) || [xnp2](https://aur.archlinux.org/packages/xnp2/)

## Žaidimų paleidimas

Kai kuriems žaidimams ar jų tipams gali būti reikalinga speciali konfigūracija, kad jie veiktų kaip numatyta. Iš esmės, žaidimai tiesiog veiks Arch Linux galimai su geresniu našumu, nei kitose distribucijose dėl kompiliavimo optimizacijos. Tačiau, kai kurioms specialioms sąrankoms gali būti reikalinga konfigūracija, kad viskas veiktų kaip tikėtasi.

### Daugiaekranė sąranka

Turint daugiau nei vieną ekraną gali kilti problemų su pilno ekrano žaidimais. Tokiu atveju, [antro X serverio paleidimas](#Žaidimo_paleidimas_atskirame_X_serveryje) gali būti išeitis. Kitą išeitį galima rasti [NVIDIA straipsnyje](/index.php/NVIDIA#Gaming_using_TwinView "NVIDIA") (gali tikti ir ne NVIDIA naudotojams).

### Klaviatūros sugriebimas

Daug žaidimų pagriebia klaviatūrą, taip neleisdami pakeisti langų (dar žinoma kaip alt-tabbing).

Kai kurie SDL žaidimai (pvz.: Guacamelee) leidžia išjungti pagriebimą paspaudžiant `Ctrl-g`.

Išjungti klaviatūros pagriebimą X11 lygyje, įdiekite [libx11-nokeyboardgrab](https://aur.archlinux.org/packages/libx11-nokeyboardgrab/) paketą.

**Note:** Žinoma, kad SDL kartais nepagriebia įvesties sistemos. Tokiu atveju, gali pavykti tiesiog kelias sekundes palaukus.

### Žaidimo paleidimas atskirame X serveryje

Kai kuriais atvejais, kaip paminėta aukščiau, gali būti reikalinga ar norėtūsi paleisti antrą X serverį. Antrojo X serverio paleidimas turi keletą privalumų, kaip: geresnis našumas, galimybė išsi"tab"inti iš žaidimo naudojant `Ctrl+Alt+F7`/`Ctrl+Alt+F8`, nenulūžta pagrininė X sesija (kuri gali būti atidaryta darbui), jei žaidimas sukonfliktuoja su grafine tvarkykle. Naujas X serveris bus kaip nuotolinės prieigos prisijungimas ALSA, todėl norėdamas girdėti audio naudotojas turės priklausyti `audio` grupei

Pradėti antrąjam X serveriui (kaip pavyzdį naudosime nemokamą pirmo asmens šaudyklę [Xonotic](http://www.xonotic.org/)) tiesiog padarykite:

```
$ xinit /usr/bin/xonotic-glx -- :1 vt$XDG_VTNR

```

Šitai toliau gali būti patobulinta naudojant atskirą X konfigūracijos failą:

```
$ xinit /usr/bin/xonotic-glx -- :1 -xf86config xorg-game.conf vt$XDG_VTNR

```

Gera priežastis čia naudoti atskirą *xorg.conf* jei jūsų pirminė konfigūracija naudoja NVIDIA Twinview kuris tokius 3D žaidimus kaip Xonotic renderina viduryje daugiaekranės sąsajos, ir eina per visus ekranus. Šitai nėra pageidautina, todėl patartina paleisti antrą X severį su alternatyvia konfigūracija kur antrasis ekranas yra išjungtas.

Žaidimo skriptas nauojantis Openbox jūsų namų direktorijoje arba `/usr/local/bin` galėtų atrodyti taip:

 `~/game.sh` 
```
if [ $# -ge 1 ]; then
        game="$(which $1)"
        openbox="$(which openbox)"
        tmpgame="/tmp/tmpgame.sh"
        DISPLAY=:1.0
        echo -e "${openbox} &
${game}" > ${tmpgame}
        echo "starting ${game}"
        xinit ${tmpgame} -- :1 -xf86config xorg-game.conf || exit 1
else
        echo "not a valid argument"
fi

```

Taigi, po `chmod +x` jūs galėtumėte naudoti skriptą:

```
$ ~/game.sh xonotic-glx

```

### Pelės aptikimo reguliavimas

Žaidimams kuriuose reikia išskirtinių įgūdžių pele, [mouse polling rate](/index.php/Mouse_polling_rate "Mouse polling rate") pareguliavimas, gali turėti įtakos tikslumui.

### Binaurinis garsas su OpenAL

Žaidimams naudojantiems [OpenAL](https://en.wikipedia.org/wiki/OpenAL "wikipedia:OpenAL"), geresniam poziciniam garso išgavimui galima naudoti OpenAL [HRTF](https://en.wikipedia.org/wiki/Head-related_transfer_function "wikipedia:Head-related transfer function") filtrus. Jie įjungiami su komanda:

```
echo "hrtf = true" >> ~/.alsoftrc

```

Alternatyvai, įdiekite [openal-hrtf](https://aur.archlinux.org/packages/openal-hrtf/) iš AUR, ir paredaguokite nustatymus /etc/openal/alsoftrc.conf

Source žaidimams, vidiniuose žaidimo nustatymuose norint įjungti HRTF `dsp_slow_cpu` turi būti `1`, kitaip žaidimas įjungs savo apdorojimą. Taip pat turėsite sureguliuoti Steam vietiniam "runtime" naudojimui, arba jo openal.so kopiją nukreipti į vietinę savo kopiją. Visiškam išpildymui naudokite šiuos nustatymus:

```
dsp_slow_cpu 1 # Disable in-game spatialiazation
snd_spatialize_roundrobin 1 # Disable spatialization 1.0*100% of sounds
dsp_enhance_stereo 0 # Disable DSP sound effects. You may want to leave this on, if you find it does not interfere with your perception of the sound effects.
snd_pitchquality 1 # Use high quality sounds

```

### PulseAudio reguliavimas

Jei naudojate [PulseAudio](/index.php/PulseAudio "PulseAudio"), galbūt norėsite pareguliuoti pradinius nustatymus optimalesniam veikimui.

#### Realaus laiko prioriteto ir neigiamo nice lygio įjungimas

Pulseaudio kaip auio daemon'as, sukurtas veikti su realaus laiko prioritetu. Tačiau saugumo sumetimais, pagal nutylėjimą įtrauktas į reugliarųjį posistemį. Šitam pataisymui, įsitikinkite, kad esate `audio` grupėje. Tuomet, nuimkite komentarą ir pakeiskite šitas eilutes `/etc/pulse/daemon.conf`:

```
high-priority = yes
nice-level = -11

```

```
realtime-scheduling = yes
realtime-priority = 5

```

tada perkraukite pulseaudio.

#### Aukštesnės kokybės atkūrimo naudojimas geresniam garsui

PulseAudio Arch sistemoje pagal numatytuosius nustatymus kanalų atkūrimui naudoja speex-float-0 , atkūrime jie laikomi 'vidutinės-žemos' kokybės. Jei jūsų sistema gali palaikyti papildomą apkrovą, galite gauti naudos naudodamiesi šituo nustatymu:

```
resample-method = speex-float-10

```

#### Techninės įrangos buferių suderinimas su Pulse buferingu

Buferių suderinimas gali sumažinti trukčiojimą ir marginaliai padidinti našumą. Daugiau detalių [čia](http://forums.linuxmint.com/viewtopic.php?f=42&t=44862).

### Dukart patikrinkite procesoriaus dažnio mąstelio keitimo nustatymus

Jei jūsų sistema šiuo metu yra sukonfigūruota tinkamai įterpti savo CPU dažnio mastelio keitmo tvarkyklę, systemos numatytasis valdytojas yra Ondemand. Pagal numatymą, šis valdytojas reduliuoja pastiprinimą jeigu sistema naudoja 95% savo CPU, ir tada tik labai trumpam laikui. Tai sutaupo energijos ir sumašiną karštį, bet pastebimai paveikia našumą. Vietoj to, jūs galite nuimti pastiprinimą tik tada kai sistema atsilaisvina, pareguliuodami sistemos valdytoją. Kad tai padarytumėte, žiūrėkite [Cpufrequtils#Tuning the ondemand governor](/index.php/Cpufrequtils#Tuning_the_ondemand_governor "Cpufrequtils").

## Kadrų skaičiaus ir reagavimo gerenimas su planavimo politika

Beveik kiekvienas žaidimas gauna naudos, jei branduoliui priskiriama teisinga planavimo politika užduočių prioretizavimui. Tačiau be daemon'o pagalbos šį perplanavimą reiktų atlikti patiems arba su keletu daemon'ų kiekvienai politikai. Šios politikos idealiai turėtų būtų nustatytos programų kiekvienai gijai atskirai, bet ne kiekvienas programuotojas šias politikas įgyvendina. Yra keletas metodų kurie vistiek turėtų veikti:

### Wine programoms

Žiūrėti [Wine#Performance](/index.php/Wine#Performance "Wine")

### Visam kitam

Programoms kurios pačios planavimo politikų neįgyvendina, daugelį funkcijų automatiškai gali atlikti **schedtool** įrankis, ir su juo susijęs daemon'as [schedtoold](https://aur.archlinux.org/packages/schedtoold/). Programų politikų pataisymui, redaguokite `/etc/schedtoold.conf` ir pridėkite programas su norimais *schedtool* argumentais.

#### Politikos

Visų pirma ir svarbiausia nustatant planavimo politiką į `SCHED_ISO` ne tik leis procesams naudoti daugiausiai 80 procentų CPU, bet ir bandys sumažinti vėlavimą, bei trukčiojimą, kada tik įmanoma. `SCHED_ISO` veikimui reikia [Linux-ck](/index.php/Linux-ck "Linux-ck"), kadangi jis įgyvendintas tik šiame branduolyje. [Linux-ck](/index.php/Linux-ck "Linux-ck") pots iš savęs turėtų sumažinti vėlavimą, ir idealiu atveju turėtų būti įdiegtas. Dauguma jei ne visi žaiimai gaus naudos iš:

```
bit.trip.runner -I

```

Naudotojams nenaudojanties [Linux-ck](/index.php/Linux-ck "Linux-ck"), `SCHED_FIFO` yra alternatyva, kuri galbūt veiks dar geriau. Turėtumėte išbandyti ar programos gerai veikia su `SCHED_FIFO`, jei taip, tisiog naudokite jį. Tačiau atsargiai, `SCHED_FIFO` gali priversti sistemą badaugti! Vietoje -I naudokite:

```
bit.trip.runner -F -p 15

```

#### Nice lygiai

Antra, nice lygiai nustato kurios užduotys atliekamos pirmiau, didėjimo tvarka.Daugumai mutimedijos užduočių rekomenduojamas -4 nice lygis, taip pat ir žaidimams:

```
bit.trip.runner -n -4

```

#### Core affinity

Vystyme yra truputis nesusipratimo, kas turėtų atlikti multithreading'ą tvarkyklė ar programa. Jei abu bandys tai atlikti, tai privers tik iki kadrų skaičiaus kritimo ir užlūžimo. Pavyzdžiai yra skaičius modernių žaidimų, ir bet kuri Wine programa veikianti su neišjungtu [GLSL](https://en.wikipedia.org/wiki/OpenGL_Shading_Language "wikipedia:OpenGL Shading Language"). pasirinkti vieną branduolį ir leisti tik tvarkyklei reguliuoti šį procesą, paprasčiausiai naudokite `-a 0x*#*` vėliavėlę, kur *#* branduolių skaičius, pvz.:

```
bit.trip.runner -a 0x1

```

naudoja pirmą branduolį. Kai kurie CPU hyperthreaded'inti ir turi tik 2 ar 4 branduolius, bet rodo 4 ar 8, tokiems geriausia:

```
bit.trip.runner -a 0x5

```

kur naudojami virtualūs branduoliai 0101, ar 1 ir 3.

#### Bendras atvejis

Daugumai žaidimų kuriuose reikalinga aukštas kadrų skaidrius ir žemas vėlavimas, geriausia naudoti šias vėliavėles. Dauguma modernių žaidimų supranta teisingą panauojimą, tačiau atitikimą reiktų patikrinti kiekvienai programai. Bendram atvejui:

```
bit.trip.runner -I -n -4
Amnesia.bin64 -I -n -4
hl2.exe -I -n -4 -a 0x1 #Wine with GLSL enabled

```

t.t.

#### Optimus ir kitos padedančios programos

Kaip bendra taisyklė, bet kuris kitas procesas reikalingas žaidimo veikimui turėtų būti su aukštesniu nice lygiu, nei pats žaiimas. Keista, Wine turi tokią problemą kaip *atvirkštinis planavimas*, iš todažnai galima gauti naudos svarbiems procesams nustatant aukštesnį nice lygį. Wineserver taip pat besąlygiškai gauna nauos iš `SCHED_FIFO`, kadangi retai sunaudoja visą CPU ar jam reikia aukšestnių prioritetų nei įmanoma.

```
optirun -I -n -5
wineserver -F -p 20 -n 19
steam.exe -I -n -5

```

## Alternatyvūs branduoliai

**Note:** Daug vartotojų praneša apie nepastovų kadrų skaičių, be kitus našumo trūkumus naudojant [Linux-ck](/index.php/Linux-ck "Linux-ck"), net jei bendrai kadrų skaičius ir yra aukštesnis. Jei norite tik BFQ gali pabandyti [linux-zen](https://www.archlinux.org/packages/?name=linux-zen).

Įprastinis Arch branduolys suteikia puikųn pagrindą bednram naudojimui. Tačiau jei sistema turi mažiau, nei 16 branduolių ir naudojama pirmiausia kaip darbo stotis, galite paakoti truputį našumo darbo krūviui ir gauti daugiau interaktyvumo su [Linux-ck](/index.php/Linux-ck "Linux-ck"). Naudodami pre-optimizuotą branduolį tikrai išlošite našume, tik svarbu pasirinkti tinkamą branduolio architektūrą.

### BFQ naudojimas

BFQ yra io-planuoklis ateinantis kaip [linux-zen](https://www.archlinux.org/packages/?name=linux-zen) ir [Linux-ck](/index.php/Linux-ck "Linux-ck") funkcija, ir yra optimizuotas būti paprastesniu, bet suteikiantis daugiau interaktyvumo ir našumo ne-serveriniam darbui. Norėdami jį įjungti pridėkite branduolio parametrą *elevator=bfq* į savo [bootloader](/index.php/Bootloader "Bootloader"). Svarbu paminėti, kad nors auguma gių rekomenduoja naudoti *noop* ar *deadline* SSD diskams dėl našumo, ttai iš tikrųjų kenkia našumui kai daugiau nei viena gija bando pasiekti prietaisą. Geriausia naudoti *bfq* nebent jums labai reikia to našumo privalumo.