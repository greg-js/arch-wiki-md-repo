**Bemærk:** Dette er en del af en flersides artikel til Begynderguiden. **[Klik her](/index.php/Beginners%27_Guide_(Dansk) "Beginners' Guide (Dansk)")** hvis du hellere vil læse guiden i sin helhed.

## Contents

*   [1 Installer grundsystemet](#Installer_grundsystemet)
    *   [1.1 Vælg en installationskilde](#V.C3.A6lg_en_installationskilde)
        *   [1.1.1 Konfigurer netværk (Netinstall)](#Konfigurer_netv.C3.A6rk_.28Netinstall.29)
        *   [1.1.2 ADSL hurtigstart til det midlertidige miljø](#ADSL_hurtigstart_til_det_midlertidige_milj.C3.B8)
        *   [1.1.3 Trådløs hurtigstart til det midlertidige miljø](#Tr.C3.A5dl.C3.B8s_hurtigstart_til_det_midlertidige_milj.C3.B8)

## Installer grundsystemet

Som root, kør installationsscriptet fra tty1:

```
# /arch/setup

```

Herefter skulle du gerne se startskærmen i Arch Installation Framework.

### Vælg en installationskilde

Efter velkomstskærmen vil du blive spurgt efter en installationskilde. Vælg en kilde som passer til dit installationsmedium. Hvis du benytter et 'netinstall' medie, kan hastighed og opdateringsstatus af pakkespejlene kontrolleres [her](https://www.archlinux.de/?page=MirrorStatus).

*   Hvis du valgte en 'Core' udgave, og du ønsker at bruge pakkerne på CD'en, vælg da CD-ROM som kilde.
*   Alternativt, eller hvis du bruger "Netinstall' mediet, vælg NET og se sektionen nedenfor ([Konfigurer netværk](#Konfigurer_netv.C3.A6rk_.28Netinstall.29).)

#### Konfigurer netværk (Netinstall)

Hvis du ønsker, kan du manuelt indlæse drivere til dit netværkskort. Udev er meget effektiv til at indlæse de påkrævede moduler, så du kan gå ud fra at det allerede er sket. Ved det næste skærmbillede, vælg 'Setup Network'. Du kan verificere dette ved at trykke <Alt>+<F3> og køre `ifconfig -a`. Når du er færdig, skift tilbage til installationen med <Alt>+<F1>.

Tilgængelige netværkskort vil vises. Hvis et netværkskort og HWaddr (hardwareadresse) vises, er modulet allerede indlæst. Hvis dit netværkskort ikke er i listen, kan du indlæse det fra installationen, eller gøre det i en anden virtuel konsol. Vælg dit netværkskort for at fortsætte.

Installationen spørger om du vil benytte DHCP. Ved at vælge 'Yes', køres **dhcpcd** for at finde en tilgængelig _gateway_ og hente en IP-adresse. Hvis du vælger 'Np' vil du blive bedt om en statisk konfiguration af IP, netmaske, broadcast, DNS server, HTTP proxy og FTP proxy. Dernæst returneres du til menuen.

Vælg 'Choose Mirror' for at vælge et pakkespejl, og vælg et HTTP/FTP spejl. Vend tilbage til hovedmenuen når du er færdig.

**Bemærk:** archlinux.org er begrænset til 50 KB/s

#### ADSL hurtigstart til det midlertidige miljø

Hvis din internetudbyder bruger PPPoE, med brugernavn og kode er dette til dig.

Skift til en anden virtuel konsol (<Alt>+<F2>), log ind som root, og kør

```
# pppoe-setup

```

Hvis alt på dit system er rigtigt konfigureret, kan du forbinde til din internetudbyder med:

```
# pppoe-start

```

Skift tilbage til den første virtuelle konsol med <Alt>+<F1> og fortsæt med [Indstil tiden](#Indstil_tiden).

#### Trådløs hurtigstart til det midlertidige miljø

(Hvis du har brug for trådløs internetadgang under installationen)

Drivere og værktøjer til trådløst netværk er tilgængelige i installationsmiljøet. En god viden om hardwaren vil være vigtig for at konfigurere det rigtigt. Bemærk at ved at følge proceduren _på dette punkt i installationen_, vil gøre din trådløse hardware tilgængelig _i installationsmiljøet_. Disse trin (eller en anden form for håndtering af trådløst netværk) skal gentages i det færdige system efter genstart.

**Bemærk:** Det følgende eksempel benytter `wlan0` til netkort, og 'linksys' til ESSID. Husk at tilpasse disse til din situation

De grundlæggende trin er som følger:

*   Skift til en tilgængelig virtuel konsol, f.eks. <Alt>+<F3>
*   Log ind som root
*   (Valgfrit) identificér det trådløse netværkskort

```
# lspci | grep -i net

```

*   Sikr dig at udev har indlæst driveren, og at driveren har skabt et brugbart kerneinterface med `/usr/sbin/iwconfig`:

 `# iwconfig` 

```
 lo no wireless extensions.
 eth0 no wireless extensions.
 wlan0    unassociated  ESSID:""
          Mode:Managed  Channel=0  Access Point: Not-Associated
          Bit Rate:0 kb/s   Tx-Power=20 dBm   Sensitivity=8/0
          Retry limit:7   RTS thr:off   Fragment thr:off
          Power Management:off
          Link Quality:0  Signal level:0  Noise level:0
          Rx invalid nwid:0  Rx invalid crypt:0  Rx invalid frag:0
          Tx excessive retries:0  Invalid misc:0   Missed beacon:0

```

`wlan0` er i dette tilfælde det tilgængelige netværkskort.

**Bemærk:** Hvis udskriften af denne kommando ikke minder om ovenstående, er driveren til dit trådløse netværkskort ikke indlæst. Hvis dette er tilfældet skal du selv indlæse driveren. Se venligst [Opsætning af trådløst netværk](/index.php?title=Wireless_Setup_(Dansk)&action=edit&redlink=1 "Wireless Setup (Dansk) (page does not exist)") for mere information.