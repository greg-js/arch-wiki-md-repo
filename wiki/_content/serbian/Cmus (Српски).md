## Contents

*   [1 Opis](#Opis)
*   [2 Instalacija](#Instalacija)
*   [3 Korišćenje](#Kori.C5.A1.C4.87enje)
    *   [3.1 Pokretanje Cmusa](#Pokretanje_Cmusa)
    *   [3.2 Dodavanje Muzike](#Dodavanje_Muzike)
    *   [3.3 Puštanje Numera](#Pu.C5.A1tanje_Numera)
    *   [3.4 Tasteri](#Tasteri)
*   [4 Tabovi](#Tabovi)
    *   [4.1 Tab biblioteke (1)](#Tab_biblioteke_.281.29)
    *   [4.2 Tab sortirane biblioteke (2)](#Tab_sortirane_biblioteke_.282.29)
    *   [4.3 Tab plejliste (3)](#Tab_plejliste_.283.29)
    *   [4.4 Tab redosleda puštanja (4)](#Tab_redosleda_pu.C5.A1tanja_.284.29)
    *   [4.5 Pregledač (5)](#Pregleda.C4.8D_.285.29)
    *   [4.6 Tab filtera (6)](#Tab_filtera_.286.29)
    *   [4.7 Tab podešavanja (7)](#Tab_pode.C5.A1avanja_.287.29)
*   [5 Mogućnosti](#Mogu.C4.87nosti)
    *   [5.1 Pluginovi](#Pluginovi)
    *   [5.2 Puštanje muzike](#Pu.C5.A1tanje_muzike)
    *   [5.3 Interfejs](#Interfejs)
    *   [5.4 Ostalo](#Ostalo)
*   [6 Linkovi](#Linkovi)

# Opis

**cmus** _(C* Music Player)_ je mali, brz i moćan audio plejer.

# Instalacija

[cmus](https://aur.archlinux.org/packages.php?ID=15893) može biti instaliran iz [AUR](/index.php/AUR "AUR").

# Korišćenje

Cmus dolazi upakovan sa odličnim uputstvima.

```
$ man cmus 
$ man cmus-tutorial
$ man cmus-remote

```

## Pokretanje Cmusa

Kada prvi put pokrenete cmus odvešće vas pravo na album/izvođač tab. Da startujete cmus:

```
$ cmus

```

## Dodavanje Muzike

Pritisnite `5` da se prebacite u tab pregledanja fajlova da bi mogli da dodate muziku. Sada, koristite strelice (`gore`, `dole`), `Enter` i `Backspace` da bi došli do mesta gde su snimljeni vaši audio fajlovi. Da dodate muziku u cmus biblioteku, koristite strelice da označite fajl ili folder, i pritisnite `a`. Kada pritisnete `a` cmus će vas pomeriti za jednu liniju dole (tako da je lako dodati gomilu fajlova/foldera koji poređani u redu) i počeće dodavanje fajla/foldera za koji ste pritisnuli `a` u vašu biblioteku. Ovo može malo potrajati ako ste odabrali folder sa mnogo stvari u njemu. Kako se fajlovi dodaju, primetićete vreme u sekundama u donjem desnom uglu kako raste. To je totalna dužina sve muzike u vašoj cmus biblioteci.

**Note:** cmus ne pomera, duplira niti menja vaše fajlove. Samo pamti gde su i kešira metapodatke (dužinu, izvođača, itd.)

**Note:** cmus automatski snima vaša podešavanja, biblioteku i sve kada ga isključite

## Puštanje Numera

Pritisnite `1` da bi se prebacili u biblioteku. Koristite `gore` i `dole` strelice da odaberete numeru koju bi hteli da čujete, i pritisnite `Enter` da je pustite. Evo nekih tastera koji kontrolišu numeru:

	Pritisnite `c` da pauzirate/odpauzirate

	Pritisnite `desno`/`levo` strelice da tražite napred/nazad 10 sekundi

	Pritisnite `<`/`>` da tražite napred/nazad 1 minut

## Tasteri

Pritisnite `7` za brzi pregled trenutnih tastera i podešavanja. Da promenite podešavanje ili taster, samo ga označite sa (`gore`/`dole` strelicama) i odaberite sa `Enter`. Ovo će prikazati trenutnu komandu ili podešavanje (donji levi ugao ekrana), koju možete izmeniti i dodati novu vrednost/taster.

# Tabovi

Postoji 7 tabova u cmusu. Pritisnite tastere `1`-`7` da promenite aktivni tab.

## Tab biblioteke (1)

Prikazuje sve numere u takozvanoj **biblioteci**. Numere su sortirane u izvođač/album maniru. Sortiranje izvođača je odrađeno po alfabetu. Albumi su sortirani po godini.

## Tab sortirane biblioteke (2)

Prikazuje isti sadržaj kao i (1), ali kao prostu listu automatski sortiranu po korisnikovoj želji.

## Tab plejliste (3)

Prikazuje izmenljivu plejlistu sa opcionalnim sortiranjem.

## Tab redosleda puštanja (4)

Prikazuje redosled numera koje će sledeće biti puštene. Ove numere imaju prednost nad svim ostalim (Npr. plejlistom ili bibliotekom).

## Pregledač (5)

Pregledač direktorijuma. U ovom tabu, muzika može biti dodata u biblioteku, plejlistu ili u red puštanja iz vašeg fajl sistema.

## Tab filtera (6)

Prikazuje sve definisane filtere.

## Tab podešavanja (7)

Prikazuje listu tastera sa ili bez komande i opcije. Skidate komandu sa određenog tastera sa `D` ili `del`, menjate komande tastera i varijable sa`Enter` i birate varijablu sa `space`.

# Mogućnosti

## Pluginovi

	**Ulaz**: Ogg Vorbis, MP3, FLAC, Musepack, WavPack, WAV, AAC, MP4, i sve ostalo podržano od strane ffmpeg (WMA, APE, MKA, TTA, SHN, ...) i libmodplug

	**Izlaz**: PulseAudio, ALSA, OSS, RoarAudio, libao, aRts, Sun, and WaveOut (Windows)

## Puštanje muzike

	Gapless playback

	ReplayGain podrška

	MP3 and Ogg strimovanje (SHOUTcast/Icecast)

	Moćni plejlist filteri / filtriranje uživo

	Redosled puštanja numera (Queue)

	Opcionalni nastavak puštanja muzike pri pokretanju

## Interfejs

	Pokretanje istog trenutka, čak i sa hiljadama numera

	Pregledač direktorijuma koji je lak za korišćenje

	Biranje boja po vašoj želji

	Dinamički tasteri. Možete tasteru dodeliti bilo koju komandu, :seek +1m na primer

	Vi / less stil pretraživanja

	Vi stil komandne linije sa dodatkom tabova

## Ostalo

	Odlično rukovanje kompilacijama

	Koristi Unicode interno za rukovanje svim stringovima

	Može da pokrene eksterne komande za trenutno odabrane fajlove (tag-editor na primer)

	Može biti kontrolisan preko UNIX socketa korišćenjem cmus-remote komande

# Linkovi

1.  [Git Repozitorijum](http://gitorious.org/cmus)
2.  [Web strana](http://cmus.sourceforge.net/)