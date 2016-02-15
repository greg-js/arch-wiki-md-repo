Tento dokument je venovaný tomu, ako nastaviť systém ALSA, aby fungoval s kernelmi 2.4 a 2.6.

Založené na Alsa Setup howto od Arjana Timmermana: [http://www.soulfly.nl/~arjan/archlinux/alsa-setup.html](http://www.soulfly.nl/~arjan/archlinux/alsa-setup.html) s ďalšou informáciou: [https://bbs.archlinux.org/viewtopic.php?t=2544](https://bbs.archlinux.org/viewtopic.php?t=2544) Ak máte počítač Dell vybavený kartou Creative Labs Sound Blaster Live! budete musieť skompilovať systém ALSA manuálne.

## Contents

*   [1 Inštalácia](#In.C5.A1tal.C3.A1cia)
*   [2 Konfigurácia](#Konfigur.C3.A1cia)
*   [3 Ste stále bez zvuku?](#Ste_st.C3.A1le_bez_zvuku.3F)
    *   [3.1 Nastavenie povolení](#Nastavenie_povolen.C3.AD)
    *   [3.2 Obnovenie nastavení Alsa Mixer pri štarte systému](#Obnovenie_nastaven.C3.AD_Alsa_Mixer_pri_.C5.A1tarte_syst.C3.A9mu)
    *   [3.3 Nastavenia KDE](#Nastavenia_KDE)

## Inštalácia

*   Nevyhnutné pre kernely 2.4 a 2.6:

```
 # pacman -S alsa-lib alsa-utils

```

*   nevyhnutné pre kernely 2.4:

```
 # pacman -S alsa-driver
 # depmod -a

```

*   Odporúčané ale nie nevyhnutné:

```
 # pacman -S alsa-oss

```

Zapamätajte si, že balíček 'alsa-driver' zahŕňa potrebné moduly založené na Arch stock kerneli! Ake ste kompilovali svoj vlastný kernel 2.4, tak najskôr nebudú fungovať, a mali by ste skompilovať nový balíček 'alsa-driver' pomocou ABS počas behu skompilovaného jadra, a nainštalovať tento balíček.

## Konfigurácia

_Poznámka: Ak hotplug detekuje vašu zvukovú kartu správne, nemusíte nahrávať moduly manuálne. Ak je toto váš prípad, potrebujete spraviť iba krok 3 (a 4). Ak si nie ste istí, či vaša zvuková karta bola detekovaná správne, ako root napíšte "lsmod". Mali bzy ste vidieť niekoľko nahratých modulov začínajúcich sa na "snd-"._

*   Nájdite modul pre svoju zvukovú kartu: [http://www.alsa-project.org/alsa-doc/](http://www.alsa-project.org/alsa-doc/) Modul bude s prefixom 'snd-' (Napríklad: 'snd-via82xx'). Taktiež môžte spustiť 'alsaconf' ako root.

*   Nahrajte moduly:

```
 # modprobe snd-NAME-OF-MODULE
 # modprobe snd-pcm-oss

```

*   Pridajte hlasitosť zvukovej karty a zapnite jej zvuk:

```
 # amixer set Master 75 unmute
 # amixer set PCM 75 unmute

```

Alebo to môžte urobiť graficky použitím príkazu 'alsamixer'
POZNÁMKA Keď používate 'alsamixer', uistite sa, že zapnete zvuk (**unmute**) (stlačte klávesu M) taktiež pridajte úroveň hlasitosti.

*   Test vášho systému na súbore wav:

```
 # aplay mywav.wav

```

*   Pridajte `snd-pcm-oss` a 'snd-NAME-OF-MODULE' do zoznamu modulov (MODULES) v '/etc/rc.conf'

*   [Umožnenie viacerým programom prehrávať zvuk v tom istom čase](/index.php?title=Umo%C5%BEnenie_viacer%C3%BDm_programom_prehr%C3%A1va%C5%A5_zvuk_v_tom_istom_%C4%8Dase&action=edit&redlink=1 "Umožnenie viacerým programom prehrávať zvuk v tom istom čase (page does not exist)")

## Ste stále bez zvuku?

Dokonca aj napriek tomu, že máte ovládače nahraté správne, and hlasitosť je v poriadku, nič nie je vypnuté, nepočujete nič! Pridanie nasledujúceho riadku do `/etc/modprobe.d/modprobe.conf` opraví tento problém (minimálne s ovládačom `via82xx` ).

```
options snd-NAME-OF-MODULE ac97_quirk=0

```

### Nastavenie povolení

*   Pridajte svojho užívateľa do skupiny Audio:

```
 # gpasswd -a Meno_užívateľa audio

```

*   Odhláste sa a prihláste, aby ste zaistili, že skupina audio je nahraná.

### Obnovenie nastavení Alsa Mixer pri štarte systému

*   Spustite 'alsactl' raz pre vytvorenie '/etc/asound.state'

```
 alsactl store

```

*   Upravte '/etc/rc.conf' a pridajte 'alsa' do zoznamu daemons, aby zvuk nabiehal pri bootovaní

### Nastavenia KDE

*   spustite KDE:

```
 # startx

```

*   Nastavte úrovne hlasitosti ako ich chcete pre daného užívateľa (každý užívateľ má svoje vlastné nastavenia):

```
 # alsamixer

```

*   **KDE 3.3** Choďte do K Menu > Multimédiá > KMix
    *   Vyberte nastavenia> Konfigurácia KMix...
    *   Odškrtnite možnosť "Restore volumes on logon" (Obnoviť hlasitosť pri prihlásení)
    *   Stlačte OK, a mali by ste mať všetko nastavené. Teraz všetky úrovne hlasitosti budú rovnaké z príkazového riadka a KDE.