**Bemærk:** Dette er en del af en flersides artikel til Begynderguiden. **[Klik her](/index.php/Beginners%27_Guide_(Dansk) "Beginners' Guide (Dansk)")** hvis du hellere vil læse guiden i sin helhed.

## Contents

*   [1 Forbered installationen](#Forbered_installationen)
    *   [1.1 Få det nyeste installationsmedie](#F.C3.A5_det_nyeste_installationsmedie)
        *   [1.1.1 Kontroller integriteten af den hentede fil](#Kontroller_integriteten_af_den_hentede_fil)
        *   [1.1.2 Installer over et netværk](#Installer_over_et_netv.C3.A6rk)
        *   [1.1.3 CD installation](#CD_installation)
        *   [1.1.4 Flash-hukommelse eller USB-pen](#Flash-hukommelse_eller_USB-pen)
            *   [1.1.4.1 *nix metode](#.2Anix_metode)
            *   [1.1.4.2 Microsoft Windows metode](#Microsoft_Windows_metode)
    *   [1.2 Boot Arch Linux installationen](#Boot_Arch_Linux_installationen)
        *   [1.2.1 Boot fra mediet](#Boot_fra_mediet)
        *   [1.2.2 Start operativsystemet](#Start_operativsystemet)
        *   [1.2.3 At ændre tastaturudlægning](#At_.C3.A6ndre_tastaturudl.C3.A6gning)
        *   [1.2.4 Dokumentation](#Dokumentation)

## Forbered installationen

**Bemærk:** Hvis du ønsker at installere til en anden partition fra en eksisterende GNU/Linux-distribution eller LiveCD, se venligst [denne wikiartikel](/index.php?title=Install_from_Existing_Linux_(Dansk)&action=edit&redlink=1 "Install from Existing Linux (Dansk) (page does not exist)") for skridt til at gøre dette. Dette kan være specielt nyttigt hvis du planlægger at fjerninstallere Arch Linux gennem VNC eller SSH. Det følgende går ud fra, at installationen udføres på normal vis.

### Få det nyeste installationsmedie

Du kan få Arch's officielle installationsmedier [herfra](https://archlinux.org/download/). Den nyeste er 2010.05.

*   Både _core_ og _netinstall_ diskaftrykkene har kun pakker til at installere et **Arch Linux grundsystem**. _Bemærk at grundsystemet ikke indeholder nogen grafisk brugerflade. Det indeholder overvejende GNU værktøjskæden, Linuxkernen, og få ekstra softwarebiblioteker og moduler._
*   _Core_ aftrykket kan både installere fra CD og fra internettet.
*   _Netinstall_ aftryk er mindre, og indeholder ingen pakker selv, hele systemet hentes fra internettet.
*   [OSS til Arch64](/index.php?title=Arch64_FAQ_(Dansk)&action=edit&redlink=1 "Arch64 FAQ (Dansk) (page does not exist)") kan hjælpe dig med at vælge mellem i686, x86_64 og dualversionerne.
*   Glem ikke at hente checksum tekstfilen sammen med din valgte ISO.

#### Kontroller integriteten af den hentede fil

`cd` til mappen hvor de hentede filer er placeret, og kør `sha1sum`:

```
$ sha1sum --check navn_på_checksum_filen.txt navn_på_valgt_iso_fil.iso

```

Dette skulle give dig et "OK" for den du har (ignorer blot de andre linjer.) Hvis ikke, hent alle filer igen. md5sum kontrollen virker på samme måde.

#### Installer over et netværk

I stedet for at skrive opstartsmediet til en skive eller et USB-drev, kan du starte .iso filen over et netværk. Dette virker godt hvis du allerede har sat en server op. Se venligst [denne artikel](/index.php?title=Install_Arch_from_network_(via_PXE)_(Dansk)&action=edit&redlink=1 "Install Arch from network (via PXE) (Dansk) (page does not exist)") for mere information, og fortsæt med [Boot Arch Linux installationen](#Boot_Arch_Linux_installationen).

#### CD installation

Brænd ISO-filen til en CD eller DVD med dit foretrukne CD/DVD-brænderdrev og software, og fortsætte med [Boot Arch Linux installationen](#Boot_Arch_Linux_installationen).

**Bemærk:** Kvaliteten af optiske drev, såvel som CD'erne selv, varierer meget. Generelt anbefales det at anvende langsomme brændehastigheder for at opnå pålidelige brændinger; nogle brugere anbefaler hastigheder _**så langsomme som 4x eller 2x**_. Hvis du oplever uforventet opførsel fra CD'en, forsøg da at brænde ved den langsomste hastighed understøttet af dit system.

#### Flash-hukommelse eller USB-pen

Se [Installer fra en USB-pen](/index.php?title=Install_from_a_USB_flash_drive_(Dansk)&action=edit&redlink=1 "Install from a USB flash drive (Dansk) (page does not exist)") for mere detaljerede instruktioner.

Denne metode vil virke for enhver slags USB-medie som din BIOS vil lade dig starte fra, både en kortlæser og en USB-pen.

**Advarsel:** Denne metode vil uigenkaldeligt destruere al data på dit medie! Vær også meget forsigtig med hvorhen du sender ISO-aftryksfilen, da `dd` adlydende vil skrive til ethvert mål du giver, selvom det er en harddisk.

##### *nix metode

Indsæt en tom eller ligegyldig flashenhed, bestem dens sti, og skriv ISO-filen til enheden med programmet `dd`:

```
$ dd if=archlinux-2010.05-_{core|netinstall}_-_{i686|x86_64|dual}_.iso of=/dev/sd_x_

```

hvor `if=` er stien til ISO-filen og `of=` er din flashenhed. Husk at bruge `/dev/sd**x**` og **ikke** `/dev/sd**x1**`

For at bekræfte at aftrykket blev skrevet korrekt til enheden, notér antallat af skrevne blokke ind og ud, , og udfør følgende check:

```
$ dd if=/dev/sdx count=antal_blokke status=noxfer | md5sum

```

Den returnerede md5sum skulle matche den til den hentede aftryksfil. Udskriften i konsollen vil typisk være således:

 `$ [sudo] dd if=archlinux-2010.05-core-i686.iso of=/dev/sdc #Write .iso to drive` 

```
 744973+0 records in
 744973+0 records out
 381426176 bytes (381 MB) copied, 106.611 s, 3.6 MB/s

```

 `$ [sudo] dd if=/dev/sdc count=744973 status=noxfer | md5sum #Verify integrity` 

```
 4850d533ddd343b80507543536258229  -
 744973+0 records in
 744973+0 records out
```

Fortsæt med [Boot Arch Linux installationen](#Boot_Arch_Linux_installationen).

##### Microsoft Windows metode

Hent Disk Imager fra [https://launchpad.net/win32-image-writer/+download](https://launchpad.net/win32-image-writer/+download). Indsæt flash-mediet. Start Disk Imager, og vælg aftryksfilen (Disk Imager accepterer kun .img filer, så du skal skrive '*.iso' i vinduet for at vælge aftryksfilen.) Vælg din enheds drevbogstav, og klik 'Write.'

Fortsæt med [Boot Arch Linux installationen](#Boot_Arch_Linux_installationen).

### Boot Arch Linux installationen

**Tip:** Hukommelseskravet til en grundlæggende installation er 64 MiB RAM.

**Tip:** Igennem processen kan den automatiske skærmrydder aktiveres. Hvis det sker kan man trykke på <Alt> for sikkert at få inholdet tilbage på skærmen.

#### Boot fra mediet

Insæt CD'en eller flashdrevet du har forberedt, og boot fra det. Du skal måske først ændre boot-rækkefølgen i BIOS, eller trykke en tast (normalt DEL, F1, F2, F11 eller F12) under BIOS POST-fasen.

**Hovedmenu:** Hovedmenuen skulle vises på nuværende tidspunkt. Vælg den foretrukne valgmulighed ved at bruge piletasterne til at markere dit valg, og derefter trykke på <Retur>. Menuen varierer en smule mellem de forskellige ISO'er.

**Bemærk:** Brugere som ønsker at fjerninstallere Arch Linux gennem en SSH-forbindelse bør lave et par ændringer på nuværende tidspunkt for at tillade SSH-forbindelser direkte til LiveCD-miljøet. Hvis du er interesseret, se venligt [artiklen](/index.php?title=Install_from_SSH_(Dansk)&action=edit&redlink=1 "Install from SSH (Dansk) (page does not exist)").

#### Start operativsystemet

Systemet vil nu indlæses og fremvise en login-prompt. Log ind som root.

Hvis du benytter et Intel chipsæt og din skærm bliver sort i bootprocessen, er det sandsynligvis et problem med _kernel mode setting_ (KMS), eller skærmopsætning i kernen. En mulig løsning er at genstarte, og ved GRUB-menuen, taste <Tab>, og dernæst for enden af linjen med kernen skrive:

```
i915.modeset=0

```

alternativt, tilføj:

```
video=SVIDEO-1:d

```

hvilket (hvis det virker) ikke vil slå KMS fra.

Når du er færdig med at lave ændringer til boot-linjen, trykker du blot på <Retur> for at boote med den opsætning.

Se [artiklen om Intel](/index.php?title=Intel_(Dansk)&action=edit&redlink=1 "Intel (Dansk) (page does not exist)") for mere information.

#### At ændre tastaturudlægning

Hvis du ikke har et tastatur med amerikansk layout, kan du interaktivt vælge dit layout/konsolfont med kommandoen:

```
# km

```

eller benytte 'loadkeys' kommandoen:

```
# loadkeys _layout_

```

hvor _layout_ er dit tastaturlayout som f.eks. "`dk`".

#### Dokumentation

Den officielle installationsguide er let tilgængelige lige på det live system! For at tilgå den, skift til tty2 (virtuel konsol nr. 2) med <Alt> + <F2>, log ind som root, og kør `/usr/bin/less` ved at skrive følgende efter #:

```
# less /usr/share/aif/docs/official_installation_guide_en

```

`less` vil lade dig bladre igennem dokumentet.

Skift tilbage til tty1 med <Alt> + <F1> for at følge resten af installationsprocessen. (Skift tilbage til tty2 til enhver tid hvis du har behov for at referere den officielle guide under installationsprocessen.)

**Bemærk:** Den officielle guide dækker kun installation af grundsystemet. Når det er installeret er det anbefalet at du vender tilbage til wiki'en og ud af mere om efter-installations overvejelser og andre relaterede problemer.

**[Begynderguiden](/index.php/Beginners%27_Guide_(Dansk) "Beginners' Guide (Dansk)")**

* * *

[Forord](/index.php/Beginners%27_Guide/Preface_(Dansk) "Beginners' Guide/Preface (Dansk)") >> **Forbered installationen** >> [Installer grundsystemet](/index.php/Beginners%27_Guide/Installation_(Dansk) "Beginners' Guide/Installation (Dansk)") >> [Efter installationen](/index.php?title=Beginners%27_Guide/Post-Installation_(Dansk)&action=edit&redlink=1 "Beginners' Guide/Post-Installation (Dansk) (page does not exist)") >> [Yderligere læsning](/index.php?title=Beginners%27_Guide/Extra_(Dansk)&action=edit&redlink=1 "Beginners' Guide/Extra (Dansk) (page does not exist)")