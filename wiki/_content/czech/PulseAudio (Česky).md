**PulseAudio** je univerzální zvukový server pro systémy POSIX a WIN32, jehož základním rysem je mixování zdrojů zvuku což umožňuje přehrávat na zvukovém zařízení více zvukových zdrojů najednou.

## Contents

*   [1 Instalace](#Instalace)
*   [2 Spuštění](#Spu.C5.A1t.C4.9Bn.C3.AD)
*   [3 Konfigurace backendů](#Konfigurace_backend.C5.AF)
    *   [3.1 ALSA](#ALSA)
    *   [3.2 OSS](#OSS)
        *   [3.2.1 osspd](#osspd)
        *   [3.2.2 padsp wrapper](#padsp_wrapper)
    *   [3.3 GStreamer](#GStreamer)
    *   [3.4 OpenAL](#OpenAL)
    *   [3.5 libao](#libao)
    *   [3.6 PortAudio](#PortAudio)
    *   [3.7 ESD](#ESD)
*   [4 Desktopová prostředí](#Desktopov.C3.A1_prost.C5.99ed.C3.AD)
    *   [4.1 Obecné X11](#Obecn.C3.A9_X11)
        *   [4.1.1 X11 zvonek](#X11_zvonek)
    *   [4.2 GNOME](#GNOME)
    *   [4.3 KDE 3](#KDE_3)
    *   [4.4 KDE 4 a Qt4](#KDE_4_a_Qt4)
*   [5 Aplikace](#Aplikace)
    *   [5.1 Audacious](#Audacious)
    *   [5.2 mpd](#mpd)
    *   [5.3 MPlayer](#MPlayer)
    *   [5.4 "Flashový" obsah](#.22Flashov.C3.BD.22_obsah)
    *   [5.5 Flashplugin (pouze pro x86_64)](#Flashplugin_.28pouze_pro_x86_64.29)
*   [6 Alternativní konfigurace](#Alternativn.C3.AD_konfigurace)
    *   [6.1 Surround sound systémy](#Surround_sound_syst.C3.A9my)
    *   [6.2 Rozšířená konfigurace ALSA](#Roz.C5.A1.C3.AD.C5.99en.C3.A1_konfigurace_ALSA)
        *   [6.2.1 ALSA zvukový monitor](#ALSA_zvukov.C3.BD_monitor)
    *   [6.3 PulseAudio přes síť](#PulseAudio_p.C5.99es_s.C3.AD.C5.A5)
    *   [6.4 TCP podpora (zvuk po síti)](#TCP_podpora_.28zvuk_po_s.C3.ADti.29)
        *   [6.4.1 Zeroconf (Avahi) publiskování](#Zeroconf_.28Avahi.29_publiskov.C3.A1n.C3.AD)
    *   [6.5 Přepínání PulseAudio serverů lokálními klienty](#P.C5.99ep.C3.ADn.C3.A1n.C3.AD_PulseAudio_server.C5.AF_lok.C3.A1ln.C3.ADmi_klienty)
    *   [6.6 Pulseaudio přes JACK](#Pulseaudio_p.C5.99es_JACK)
        *   [6.6.1 QjackCtl se Start/Stop Skripty](#QjackCtl_se_Start.2FStop_Skripty)
    *   [6.7 Pulseaudio zkrz OSS](#Pulseaudio_zkrz_OSS)
    *   [6.8 Pulseaudio z chroot (př. 32-bit chroot v 64-bit instalaci)](#Pulseaudio_z_chroot_.28p.C5.99._32-bit_chroot_v_64-bit_instalaci.29)
*   [7 Rady při potížích](#Rady_p.C5.99i_pot.C3.AD.C5.BE.C3.ADch)
    *   [7.1 Žádný zvuk po instalaci](#.C5.BD.C3.A1dn.C3.BD_zvuk_po_instalaci)
        *   [7.1.1 Žádné zvukové karty](#.C5.BD.C3.A1dn.C3.A9_zvukov.C3.A9_karty)
        *   [7.1.2 KDE4](#KDE4)
        *   [7.1.3 Ztlumené audio zařízení](#Ztlumen.C3.A9_audio_za.C5.99.C3.ADzen.C3.AD)
    *   [7.2 Daemon nenastartuje](#Daemon_nenastartuje)
    *   [7.3 padevchooser](#padevchooser)
    *   [7.4 Škubání zvuku a vysoké vytížení CPU od verze 0.9.14](#.C5.A0kub.C3.A1n.C3.AD_zvuku_a_vysok.C3.A9_vyt.C3.AD.C5.BEen.C3.AD_CPU_od_verze_0.9.14)
    *   [7.5 Nekvalitní zvuk](#Nekvalitn.C3.AD_zvuk)
    *   [7.6 Nefunkční nastavení hlasitosti](#Nefunk.C4.8Dn.C3.AD_nastaven.C3.AD_hlasitosti)
    *   [7.7 Hlasitost je vyšší po každém spuštění aplikace](#Hlasitost_je_vy.C5.A1.C5.A1.C3.AD_po_ka.C5.BEd.C3.A9m_spu.C5.A1t.C4.9Bn.C3.AD_aplikace)
    *   [7.8 Realtime plánování](#Realtime_pl.C3.A1nov.C3.A1n.C3.AD)
*   [8 Viz také](#Viz_tak.C3.A9)
*   [9 Externí odkazy](#Extern.C3.AD_odkazy)

## Instalace

Všechny potrebné balíčky se nacházejí v repozitáři community, který by měl být povolen. Pro instalaci :

```
# pacman -S pulseaudio

```

Volitelně lze nainstalovat GTK aplikace, které umožní nastavovat vstupní a výstupní zařízení apod. :

```
# pacman -S paprefs pavucontrol

```

## Spuštění

Pulseaudio potřebuje pro svou činnost spuštěný dbus daemon. Proto ho spusťte pokud ještě neběží:

```
# /etc/rc.d/dbus start

```

Start pulseaudia lze provést příkazem:

```
$ pulseaudio --start

```

Pokud spouštíme pulseaudio v grafickém prostředí:

```
$ start-pulseaudio-x11

```

Pulseaudio lze zastavit příkazem:

```
$ pulseaudio --kill

```

Nutno upozornit, že některá X11 prostředí startují Pulseaudio automaticky při přihlášení uživatele, proto zkontrolujte pro jistotu wiki sekci pro dané desktopové prostředí.

## Konfigurace backendů

Slouží pro nastavení podpory pro mixování audio streamu od aplikace, která nepodporuje přímo PulseAudio.

### ALSA

Pro aplikace, které nepodporují PulseAudio, ale podporují ALSA je doporučeno nainstalovat ALSA plugin pro PulseAudio:

```
# pacman -S pulseaudio-alsa

```

Tento balíček obsahuje i nezbytný konfigurační soubor `/etc/asound.conf` pro nastavení ALSA výstupu na PulseAudio server. Pokud používáte x86_64 Archlinux a požadujete fungující zvuk i pro 32bit aplikace (jako Wine), musíte mít nainstalované i 32bit verze knihoven lib32-libpulse and lib32-alsa-plugins. Některé aplikace, keré používají ALSA OSS emulaci by mohly PulseAudio obejít. Pro tento případ je dobré odstranit `snd_pcm_oss` modul jádra:

```
# rmmod snd_pcm_oss

```

Poté je vhodné daný modul zakázat, což se provede v souboru `/etc/rc.conf` v sekci MODULES přídáním `!snd_pcm_oss`.

### OSS

Existuje několik cest jak donutit OSS programy hrát přes PulseAudio:

#### osspd

Nejjednodušší metoda.

Nainstalujte ossp a spusťte daemona příkazem:

```
/etc/rc.d/osspd start

```

Nezapomeňte přidát osspd do sekce DAEMONS v souboru rc.conf pro automatické spouštění při startu.

#### padsp wrapper

Pokud máte program užívající OSS, můžete ho donutit pracovat s PulseAudiem spuštěním přes wrapper padsp:

```
$ padsp OSSprogram

```

Několik příkladů:

```
$ padsp aumix
$ padsp sox foo.wav -t ossdsp /dev/dsp

```

Pokud preferujete jednoduché spouštění, je možné použít script jako například tento, kde původní program byl přejmenován (přidána koncovka -bin) a takto vytvořený script pojmenovaný dle programu je pak spouštěn jako aplikace. Nutno podotknout, že tato metoda selže v případě aktualizace daného programu balíčkovacím systémem, který tento skript přepíše. Proto ji berte pouze jako příklad:

 `/usr/bin/OSSProgram` 
```
#!/bin/sh
if test -x /usr/bin/padsp; then
    exec /usr/bin/padsp /usr/bin/OSSprogram-bin "$@"
else
    exec /usr/bin/OSSprogram "$@"
fi

```

### GStreamer

Abychom přiměli [GStreamer](/index.php/GStreamer "GStreamer") používat PulseAudio, nastavíme gconf proměnné `/system/gstreamer/0.10/default/audiosink` na 'pulsesink *a `/system/gstreamer/0.10/default/audiosrc` na* pulsesrc *následujícími příkazy:*

```
 $ gconftool-2 -t string --set /system/gstreamer/0.10/default/audiosink pulsesink
 $ gconftool-2 -t string --set /system/gstreamer/0.10/default/audiosrc pulsesrc

```

Některé aplikace (jako Rhythmbox) ignorují *audiosink* nastavení a používají *musicaudiosink*. Proto musíme *musicaudiosink* přenastavit pro tyto aplikace také:

```
 $ gconftool-2 -t string --set /system/gstreamer/0.10/default/musicaudiosink pulsesink

```

### OpenAL

OpenAL software využívá defaultně PulseAudio, ale můžeme ho také explicitně nastavit : `/etc/openal/alsoft.conf`  `drivers=pulse,alsa` 

### libao

Editací libao konfiguračního souboru nastavíme pulse:

 `/etc/libao.conf`  `default_driver=pulse` 

### PortAudio

Aktuální verze PortAudio v community repozitáři nedpodporuje PulseAudio a non-mmap audio zařízení. Pro podporu PulseAudia lze překompilovat balíček z ABS aplikováním [patche](http://svn.mandriva.com/cgi-bin/viewvc.cgi/packages/cooker/portaudio/current/SOURCES/portaudio-19-alsa_pulse.patch?revision=313993).

### ESD

PulseAudio je v podstatě náhrada za zvukový daemon ESD, proto pokud běží PulseAudio, klienti ESD hrají automaticky přes PulseAudio bez nutné ruční konfigurace.

## Desktopová prostředí

### Obecné X11

Spusťte PulseAudio po startu X11 příkazem:

```
$ start-pulseaudio-x11

```

Pokud používáte GNOME nebo KDE, PulseAudio se spouští automaticky s příhlášením uživatele a není třeba nic dělat.

#### X11 zvonek

Pokud požadujete, aby PulseAudio zahrálo zvuk generovaný X11 zvonkem či pípnutím při nějaké akci (například v terminálu), přidejte následující nastavení do `/etc/pulse/default.pa`:

```
load-sample-lazy x11-bell /usr/share/sounds/freedesktop/stereo/dialog-error.oga
load-module module-x11-bell sample=x11-bell 

```

Samozřejmě si můžete nastavit použití i jiného zvukového vzorku než `dialog-error.oga`, který je částí balíčku *sound-theme-freedesktop*.

### GNOME

Úplná integrace PulseAudia do GNOME vyžaduje speciální nahrazující balíčky:

*   gnome-media-pulse
*   gnome-settings-daemon-pulse
*   libcanberra-pulse

Tyto jsou součástí skupiny balíčků *pulseaudio-gnome*.

### KDE 3

Pokud používáte KDE 3, nelze provozovat PulseAudio jakož náhradu za aRts.

### KDE 4 a Qt4

Pulseaudio lze používat pro KDE4/Qt4 aplikace. Více informací lze nalézt na [PulseAudio wiki stránce věnované KDE](http://www.pulseaudio.org/wiki/KDE). Pro KDE existuje také jakási alternativa za pavucontrol [veromix plasmoid](https://aur.archlinux.org/packages.php?ID=43848), kterou lze nalézt v AURu.

## Aplikace

### Audacious

Audacious nativně podporuje PulseAudio takže stačí najít v nastavení Preferences -> Audio -> Current output nastavit na 'PulseAudio Output Plugin'.

### mpd

Je nutno nakonfigurovat mpd dle [návodu](http://mpd.wikia.com/wiki/PulseAudio) pro nastavení výstupu na PulseAudio. Na multimediálním zařízení spusťte PulseAudio jako *mpd* uživatele. Na běžném PC spouštějte mpd i PulseAudio pod vlastním účtem a nepoužívejte *mpd* uživatele.

### MPlayer

MPlayer nativně podporuje PulseAudio výstup s volbou "`-ao pulse`". Toto lze také nastavit jako výchozí v konfiguračním souboru pro každého uživatele `~/.mplayer/config` nebo pro celý systém `/etc/mplayer/mplayer.conf`:

 `/etc/mplayer/mplayer.conf`  `ao=pulse` 

### "Flashový" obsah

Pokud neslyšíte žádný zvukový výstup z multimediálního obsahu typu flash, můžete zkusit nainstalovat z AURu [libflashsupport-pulse](https://aur.archlinux.org/packages/libflashsupport-pulse/).

### Flashplugin (pouze pro x86_64)

Pokud používáte flashplugin z multilib repozitáře, který je 32bit, je nutno nainstalovat také lib32-alsa-plugins a lib32-libcanberra-pulse pokud chcete mixování zvuku. Jinak nebude možné přehrávat jiný zvuk pokud zrovna přehráváte flash.

```
# pacman -S lib32-alsa-plugins lib32-libcanberra-pulse

```

## Alternativní konfigurace

### Surround sound systémy

Pro povolení všech zvukových výstupů vaší karty editujte `/etc/pulse/daemon.conf` kde odkomentujte default-sample-channels řádek a nastavte na potřebnou hodnotu (**6** *5.1* **8** *7.1*):

```
# Výchozí 2 kanály
default-sample-channels=2
# nebo pro 5.1 výstup
default-sample-channels=6
# nebo pro 7.1 výstup
default-sample-channels=8

```

Po editaci je nutné restartovat PulseAudio.

### Rozšířená konfigurace ALSA

Někdy je nutno nastavit ručně soubor `/etc/asound.conf` (systémové nastavení) nebo `~/.asoundrc` (pro každého uživatele), aby ALSA používala PulseAudio:

 `/etc/asound.conf` 
```
pcm.pulse {
    type pulse
}
ctl.pulse {
    type pulse
}
pcm.!default {
    type pulse
}
ctl.!default {
    type pulse
}

```

Pokud vynecháte poslední dvě skupiny nastavení, pak budete muset konfigurovat každou ALSA aplikaci zvlášť v jejím nastavení, aby použila "pulse" výstup.

#### ALSA zvukový monitor

Pro možnost záznamu ze zvukového monitoru (př. Monitor pro to co slyším, Stereo Mix, .. ) musíte použit `pactl list` pro nalezení názvu zvukového zdroje PulseAudia (př. `alsa_output.pci-0000_00_1b.0.analog-stereo.monitor`). Pak přidat tyto do `/etc/asound.conf` nebo `~/.asoundrc`:

```
pcm.pulse_monitor {
  type pulse
  device alsa_output.pci-0000_00_1b.0.analog-stereo.monitor
}

ctl.pulse_monitor {
  type pulse
  device alsa_output.pci-0000_00_1b.0.analog-stereo.monitor
}

```

Nyní můžete vybrat `pulse_monitor` jako zdroj nahrávání zvuku.

### PulseAudio přes síť

Jedna z předností PulseAudia je možnost streamování audia pomocí clientů a serveru s běžícím pulseaudio daemonem přes vaší LAN. Pro tuto možnost musíte povolit module-native-protocol-tcp a zkopírovat pulse-cookie do klientů v síťi.

### TCP podpora (zvuk po síti)

Pro povolení TCP modulu přidejte či odkomentujte `/etc/pulse/default.pa`:

```
load-module module-native-protocol-tcp

```

Pro povolení vzdáleného připojení na TCP modul musíte odblokovat službu v `/etc/hosts.allow`:

```
pulseaudio-native: ALL

```

Pozor: Pokud máte problém s připojením, zkuste na serveru:

```
pacmd>> list-modules

```

(zde můžete také nahrávat moduly!)

#### Zeroconf (Avahi) publiskování

Je možné že pro nastavení vzdáleného přístupu na server přes (`padevchooser`) budete potřebovat také nainstalovaný a spuštěný `avahi-daemon` přidaný v sekci DAEMONS v rc.conf na serveru tak i na klientských stanicích.

### Přepínání PulseAudio serverů lokálními klienty

Pro přepínání serveru na klientské stanici lze použít příkaz `pax11publish`. Pro příklad přepnutí z výchozího serveru na server s názvem (hostname) foo:

```
$ pax11publish -e -S foo

```

Nebo přepnutí zpět na výchozí server:

```
$ pax11publish -e -r

```

Pozor při přepnutí musejí být programy používající Pulse pravděpodobně restartovány.

### Pulseaudio přes JACK

Je podobný PulseAudiu, ale je více zaměřen na profesionální práci s audiem. Pulseaudio používá modul module-jack-source a module-jack-sink což mu umožňuje běžet jako zvukový server nad JACK démonem. Takto je pulseaudiem umožněno nastavení zesílení pro každou běžnou aplikaci zvlášť, přehrávání filmů písniček apod., zatímco je také umožněno nízkolatenční nahrávání a přehrávání a zpracování zvuku aplikacemi napojenými na JACK. Toto však zabrání PulseAudiu přímý zápis do bufferů zvukové karty, což má za následek zvýšení vytížení CPU. Pro vyzkoušení běhu PA s JACK stačí načíst nezbytné moduly při startu:

```
pulseaudio -L module-jack-sink -L module-jack-source

```

Pro použití Pulseaudia s JACK musí být JACK spuštěn před startem PA. PulseAudio vyžaduje pro běh 2 moduly, které změníme editováním `/etc/pulse/default.pa`:

```
### Load audio drivers statically (it is probably better to not load
### these drivers manually, but instead use module-hal-detect --
### see below -- for doing this automatically)
#load-module module-alsa-sink
#load-module module-alsa-source device=hw:1,0
#load-module module-oss device="/dev/dsp" sink_name=output source_name=input
#load-module module-oss-mmap device="/dev/dsp" sink_name=output source_name=input
#load-module module-null-sink
#load-module module-pipe-sink

### Automatically load driver modules depending on the hardware available
.ifexists module-udev-detect.so
load-module module-udev-detect
.else
### Alternatively use the static hardware detection module (for systems that
### lack udev support)
load-module module-detect
.endif

```

na následující podobu:

```
### Load audio drivers statically (it is probably better to not load
### these drivers manually, but instead use module-hal-detect --
### see below -- for doing this automatically)
#load-module module-alsa-sink
#load-module module-alsa-source device=hw:1,0
#load-module module-oss device="/dev/dsp" sink_name=output source_name=input
#load-module module-oss-mmap device="/dev/dsp" sink_name=output source_name=input
#load-module module-null-sink
#load-module module-pipe-sink
load-module module-jack-source
load-module module-jack-sink

### Automatically load driver modules depending on the hardware available
#.ifexists module-udev-detect.so
#load-module module-udev-detect
#.else
### Alternatively use the static hardware detection module (for systems that
### lack udev support)
#load-module module-detect
#.endif

```

Tohle zamezí načtení module-udev-detect, který se snaží převzít zvukovou kartu což již provedl JACK. Explicitně načten musí být také JACK source a sink modul což je patrné z úpravy.

#### QjackCtl se Start/Stop Skripty

Po provedení nastavení probraných výše lze použít QjackCtl pro spouštění skriptu během startu a vypnutí pro start/stop PulseAudia. Proč tohle dělat? Protože změny provedené při zprovoznění JACK nám zakázaly automatickou detekci hardware pomocí modulu pulseaudia. Pomocí těchto skriptů lze patřičná nastavení aplikovat jen pokud zrovna vyžadujeme pro práci JACK.

Následující příklad může být použitý jakož startovací skript, který démonizuje pulseaudio a spouští *padevchooser*. Tento skript nutno upravit pro volby konfigurace pulseaudia, které zde nejsou uvedeny `jack_startup`:

```
#!/bin/bash
#Load PulseAudio and PulseAudio Device Chooser

pulseaudio -D
padevchooser&

```

příklad skriptu pro vypnutí pulseaudia `jack_shutdown`:

```
#!/bin/bash
#Kill PulseAudio and PulseAudio Device Chooser

pulseaudio --kill
killall padevchooser

```

Oběma skriptům nutno povolit spouštění:

```
chmod +x jack_startup jack_shutdown

```

Pak po načtení QjackCtl přejdeme do *Setup* a v *Options* je tab "Execute Script after Startup:" a "Execute Script on Shutdown:" kde zadáme cestu ke skriptům.

### Pulseaudio zkrz OSS

Přidejte následující do `/etc/pulse/default.pa`:

```
 load-module module-oss

```

Pak spusťte Pulseaudio jako obvykle. Měli by jste mít zdroje vstupu a vystupů pro vaše OSS zařízení.

### Pulseaudio z chroot (př. 32-bit chroot v 64-bit instalaci)

Protože chroot nastavuje alternativní root, musí být puselaudio nainstaované také uvnitř chroot prostředí.

Pokud se PA nepřipojí na specifikovaný server v konfiguračním souboru `/etc/pulse/client.conf` nebo přes X11 nastavení používající modul module-x11-publish, pak začne hledat lokální server a pokud ho nenalezne tak si vytvoří nový server. Každý server má unikátní ID založené na id stroje z `/var/lib/dbus`. Pro umožnění aplikací pod chroot k přístupu na server je nutno připojit následující adresáře pod chroot:

```
/var/run
/var/lib/dbus
/tmp
~/.pulse

```

`/dev/shm` měl by být pro dobrý výkon taktéž připojen. Nutno podotknout, že pokud připojujete /home, pak je i .pulse adresář již připojen.

Pro další upřesnění a možnosti navštivte tuto wiki [stránku](https://wiki.archlinux.org/index.php?title=Arch64_Install_bundled_32bit_system#Additional_mount_option_to_allow_32-bit_apps_to_access_the_64-bit_Pulseaudio_server).

## Rady při potížích

### Žádný zvuk po instalaci

#### Žádné zvukové karty

Když PulseAudio nastartuje, spusťte `pacmd list`. Jestliže zde nejsou žádné zvukové karty, ujistěte se, že ALSA zařízení nejsou v používání tj blokovány jiným programem:

```
$ fuser -v /dev/snd/*
$ fuser -v /dev/dsp

```

Ujistěte se, že všechny aplikace používající pcm nebo dsp jsou ukončeny před restartem PA.

#### KDE4

Je možné, že máte nastavené jiné výstupní zařízení v phonon nastavení. Ujistěte se tedy, že máte nastavené správné výstupní zařízení na vrchu seznamu a zkontrolujte přes pavucontrol, že spuštěné aplikace používají Pulseaudio a zároveň PulseAudio používá správný zvukový výstup.

#### Ztlumené audio zařízení

Pokud neslyšíte zvuk ani defaultně pod ALSAou, pak patrně máte ztlumený výstup což ověříte přes alsamixer, kde nesmí mít výstup zesílení 00 nebo m ( stiskem m lze aktivovat/deaktivovat mute)

```
$ alsamixer -c 0

```

Někdy se stane, že snd_pcsp je v konfliktu s modulem snd_hda_intel (Intel zvukové karty). Pak je nutno zakázat snd_pcsp v souboru `/etc/rc.conf` v sekci MODULES přidáním `!snd_pcsp`.

### Daemon nenastartuje

Zkuste resetovat PulseAudio:

```
$ pulseaudio --kill
$ killall pulseaudio
$ killall -9 pulseaudio
$ rm -rf ~/.pulse*
$ rm -rf /tmp/pulse*

```

Pak zkuste znovu spustit.

### padevchooser

Pokud nemůžete spustit PulseAudio Device Chooser - padevchooser program pro výběr zařízení, pak zkuste restartovat Avahi démona:

```
$ /etc/rc.d/avahi-daemon restart

```

### Škubání zvuku a vysoké vytížení CPU od verze 0.9.14

PulseAudio bylo přepsáno pro využívání časově založeného audio plánování místo tradičního přerušením řízeného. To může způsobovat problémy v některých Alsa ovladačích. Pro vypnutí časového plánování změnit:

```
load-module module-udev-detect 

```

v `/etc/pulse/default.pa` na:

```
load-module module-udev-detect tsched=0

```

### Nekvalitní zvuk

Může být způsoben špatným nastavením vzorkovací frekvence zvuku v /etc/pulse/daemon.conf. Zkuste odkomentovat nebo změnit řádek:

```
; default-sample-rate = 44100

```

na

```
default-sample-rate = 48000

```

a restartujte PulseAudio:

```
pulseaudio --kill && pulseaudio --start

```

44100Hz je dobré pro kvalitní přehrávání audio souborů bez převzorkování, tyto jsou v drtivé většině právě v 44100Hz. 48000Hz je vhodné pro drtivou většinu zvukových karet.

### Nefunkční nastavení hlasitosti

Zkontrolujte

```
/usr/share/pulseaudio/alsa-mixer/paths/analog-output.conf.common

```

Pokud hlasitost nejde měnit použitím `alsamixer` nebo `amixer`, může to být kvůli větším hodnotám, které PulseAudio používá ( 65537 ). Zkuste proto větší hodnoty př. `amixer set Master 655+` nebo použijte vyjádření v %.

### Hlasitost je vyšší po každém spuštění aplikace

Můžete zkusit odkomentovat.

```
flat-volumes = no

```

v

```
/etc/pulse/daemon.conf

```

### Realtime plánování

Pokud rtkit nepracuje, zkuste ručně nastavit PulseAudio s realtime časováním v `/etc/security/limits.conf`:

```
@pulse-rt - rtprio 9
@pulse-rt - nice -11

```

Nezapomeňte se přidat jakož uživatel do skupiny `pulse-rt`:

```
# gpasswd -a <user> pulse-rt

```

## Viz také

*   [Allow multiple programs to play sound at once](/index.php/Allow_multiple_programs_to_play_sound_at_once "Allow multiple programs to play sound at once")

## Externí odkazy

*   [http://www.pulseaudio.org/wiki/PerfectSetup](http://www.pulseaudio.org/wiki/PerfectSetup) - Pokud chcete mít své nastavení perfektní, následujte tento odkaz
*   [http://www.alsa-project.org/main/index.php/Asoundrc](http://www.alsa-project.org/main/index.php/Asoundrc) - Alsa wiki na .asoundrc
*   [http://www.pulseaudio.org/](http://www.pulseaudio.org/) - Oficiální stránka PulseAudia
*   [http://www.pulseaudio.org/wiki/FAQ](http://www.pulseaudio.org/wiki/FAQ) - PulseAudio FAQ