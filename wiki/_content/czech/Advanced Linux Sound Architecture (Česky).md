## Contents

*   [1 Úvod](#.C3.9Avod)
*   [2 Instalace](#Instalace)
*   [3 Konfigurace](#Konfigurace)
*   [4 Jste stále bez zvuku?](#Jste_st.C3.A1le_bez_zvuku.3F)
    *   [4.1 Nastavení povolení](#Nastaven.C3.AD_povolen.C3.AD)
    *   [4.2 Obnovení nastavení Alsa Mixer při startu systému](#Obnoven.C3.AD_nastaven.C3.AD_Alsa_Mixer_p.C5.99i_startu_syst.C3.A9mu)
    *   [4.3 Nastavení KDE](#Nastaven.C3.AD_KDE)

## Úvod

Tento dokument popisuje jak nastavit systém ALSA, aby fungoval s kernely 2.4 a 2.6\. Napsané na základě Alsa Setup howto od Arjana Timmermana: [http://www.soulfly.nl/~arjan/archlinux/alsa-setup.html](http://www.soulfly.nl/~arjan/archlinux/alsa-setup.html)

Další informace: [[1]](https://bbs.archlinux.org/viewtopic.php?t=2544)

Pokud máte počítač Dell vybavený kartou Creative Labs Sound Blaster Live!, budete muset skompilovat systém ALSA manuálně.

## Instalace

*   Nevyhnutné pro kernely 2.4 a 2.6:

```
 # pacman -S alsa-lib alsa-utils

```

*   Nevyhnutné pre kernely 2.4:

```
 # pacman -S alsa-driver
 # depmod -a

```

*   Doporučené ale ne nevyhnutelné:

```
 # pacman -S alsa-oss

```

Zapamatujte si, že balíček 'alsa-driver' zahrnuje potřebné moduly založené na Arch stock kernelu! Pokud jste kompilovali svůj vlastní kernel 2.4, tak zřejmě nebudou fungovat a měli by jste skompilovat nový balíček 'alsa-driver' pomocí ABS a nainstalovat tento balíček.

## Konfigurace

_**Poznámka:** Pokud hotplug detekuje vaši zvukovou kartu správně, nemusíte nahrávat moduly manuálně. Pokud je toto váš případ, potřebujete udělat pouze krok 3 (a 4). Jestli si nejste jistí zda vaše zvuková karta byla detekovaná správně, jako root napište "lsmod". Měli by jste vidět několik nahraných modulů začínajícich na "snd-"._

*   Najděte modul pro svoji zvukovou kartu: [http://www.alsa-project.org/alsa-doc/](http://www.alsa-project.org/alsa-doc/) Modul bude s prefixem 'snd-' (Například: 'snd-via82xx'). Také můžete spustit 'alsaconf' jako root.

*   Nahrajte moduly:

```
 # modprobe snd-NAME-OF-MODULE
 # modprobe snd-pcm-oss

```

*   Přidejte hlasitost zvukové karty a zapněte zvuk:

```
 # amixer set Master 75 unmute
 # amixer set PCM 75 unmute

```

Nebo to můžete udělat graficky použitím příkazu 'alsamixer'

_**Poznámka:** Pokud používáte 'alsamixer', ujistěte se, že zapnete zvuk (**unmute**) (Stiskněte klávesu M) také přidejte úroveň hlasitosti._

*   Test vašeho systému na soubory wav:

```
 # aplay mywav.wav

```

*   Přidejte `snd-pcm-oss` a 'snd-NAME-OF-MODULE' do seznamu modulů (MODULES) v '/etc/rc.conf'

## Jste stále bez zvuku?

Dokonce i přes to, že máte ovládače nahrané správně a hlasitost je v pořádku, nic není vypnuté, neslyšíte nic! Přidání následujícího řádku do `/etc/modprobe.d/modprobe.conf` spraví tento problém (minimálně s ovladačem `via82xx` ).

```
options snd-NAME-OF-MODULE ac97_quirk=0

```

### Nastavení povolení

*   Přidejte svého užívatele do skupiny Audio:

```
 # gpasswd -a jméno_uživatele audio

```

*   Odhlaste se a znovu přihlašte, aby jste zajistili, že skupina audio je nahraná.

### Obnovení nastavení Alsa Mixer při startu systému

*   Spusťte 'alsactl' pro vytvoření '/etc/asound.state'

```
 alsactl store

```

*   Upravte '/etc/rc.conf' a přidejte 'alsa' do seznamu daemons, aby zvuk nabíhal při bootování

### Nastavení KDE

*   Spusťte KDE:

```
 # startx

```

*   Nastavte úrovně hlasitosti, jak chcete pro daného uživatele (každý užívatel má svoje vlastní nastavení):

```
 # alsamixer

```

*   **KDE 3.3** Jděte do K Menu > Multimedia > KMix
    *   Vyberte nastavení> Konfigurace KMix...
    *   Odškrtěte možnost "Restore volumes on logon" (Obnovit hlasitost při prihlásení)
    *   Stiskněte OK, a měli by jste mít vše nastavené. Teď všechny úrovně hlasitosti budou stejné z příkazového řádku a KDE.