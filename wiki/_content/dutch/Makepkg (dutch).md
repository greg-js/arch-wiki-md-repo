`makepkg` wordt gebruikt om je eigen software te compileren voor gebruik met [Pacman](/index.php/Pacman "Pacman"). Het gebruikt een script-gebaseerd bouwsysteem dat de broncode kan downloaden en valideren, afhankelijkheden controleert, instellingen configureert, het pakket bouwt, het pakket installeert in een tijdelijke omgeving, aanpassingen maakt, meta-gegevens genereert en vervolgens de hele handel in een tarball rolt. Zoals je kunt zien, heeft makepkg veel features, waarvan de belangrijkste hieronder beschreven worden.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Het systeem configureren](#Het_systeem_configureren)
    *   [1.1 Arch Build System](#Arch_Build_System)
    *   [1.2 Makepkg](#Makepkg)
*   [2 Een pakket bouwen](#Een_pakket_bouwen)
*   [3 Installeren vanuit bouwscripts](#Installeren_vanuit_bouwscripts)
*   [4 Handige links](#Handige_links)

## Het systeem configureren

### Arch Build System

Verzeker jezelf er eerst van, dat je alle tools hebt geinstalleerd, die nodig zijn om [Arch Build System](/index.php/Arch_Build_System "Arch Build System")/makepkg te draaien en om software te kunnen compileren vanaf broncode:

```
pacman -S base-devel
pacman -S abs

```

Nu zou je abs kunnen uitvoeren, om alle PKGBUILDS en bijbehorende bestanden te downloaden, waarmee je de originele Arch pakketten kunt bouwen:

```
abs

```

ABS zal een SVN hierarchie van de repository's maken in de map /var/abs op je hardeschijf. Standaard zijn een aantal repository's uitgeschakeld. Je zult /etc/abs.conf eerst moeten wijzigen en de uitroeptekens (!) moeten verwijderen voor de repository's die je wilt activeren.

Maak een bouwmap. Bijvoorbeeld:

```
$ mkdir ~/abs

```

### Makepkg

Als je in staat wilt zijn om afhankelijkheden met makepkg als gewone gebruiker (met makepkg -s, zie onder) te installeren, moet je [Sudo](/index.php/Sudo "Sudo") installeren en jezelf toevoegen aan /etc/sudoers, door het commando "visudo" uit te voeren en de onderstaande regel toe te voegen:

```
USER_NAME    ALL=(ALL)    NOPASSWD: /usr/bin/pacman

```

De bovenstaande regel zorgt ervoor dat je geen wachtwoord hoeft in te voeren om pacman te gebruiken. Zie de pagina over [Sudo](/index.php/Sudo "Sudo") voor meer informatie.

Nu moet je beslissen waar je gebouwde pakketten wilt neerzetten. Je kunt deze pakketten bijvoorbeeld in je thuismap in een aparte submap plaatsen. Je kunt deze stap ook overslaan, waardoor je pakketten gemaakt worden in dezelfde map als waar je makepkg uitvoert.

Maak de map:

```
mkdir /home/$USER/packages

```

Wijzig vervolgens de PKGDEST variabele in /etc/makepkg.conf in overeenstemming met de gemaakte map.

Terwijl je /etc/makepkg.conf aan het wijzigen bent, kun je ook eens kijken naar de andere waarden in makepkg.conf. Je kunt bijvoorbeeld PACKAGER wijzigen, of het uitroepteken (!) voor docs in de standaard OPTIONS array verwijderen, als je niet wilt dat de /usr/share/doc/<package> map wordt verwijderd door makepkg. Zie [Makepkg.conf](/index.php/Makepkg.conf "Makepkg.conf") voor meer informatie.

## Een pakket bouwen

Voordat je doorgaat, moet je controleren of je de base-devel groep hebt geinstalleerd. Pakketten die tot deze groep behoren, worden normaliter niet genoemd als afhankelijkheden in de PKGBUILD van een pakket. Je kunt de pakketten in de groep base-devel installeren door als de gebruiker "root" het volgende commando uit te voeren:

```
pacman -S base-devel

```

Om een pakket te bouwen, kun je zelf een PKGBUILD voor een softwarepakket schrijven, zoals beschreven in [Creating packages](/index.php/Creating_packages "Creating packages"), of je kunt een PKGBUILD downloaden van [AUR](https://aur.archlinux.org) of [ABS](/index.php/ABS "ABS") (zie boven) of een andere bron. Je moet voorzichtig zijn, als je een PKGBUILD download, en alleen degenen installeren van mensen en bronnen die je vertrouwd.

Zeg dat je een perfect pakket hebt gevonden op AUR, welke je wilt bouwen en installeren (in dit voorbeeld zullen we "rufus" gebruiken, een in Python geschreven Bittorrent client). Je kunt de PKGBUILD en andere benodigde bestanden verkrijgen van [deze AUR pagina](https://aur.archlinux.org/packages.php?do_Details=1&ID=3394), door op de Tarball link te klikken.

```
cd /path/to/file
tar -zxf rufus.tar.gz
cd rufus

```

Je zult opmerken dat er een aantal bestanden gesitueerd zijn in de map "rufus", waaronder het bestand PKGBUILD, dat wordt gebruikt om je pakket te bouwen. Om het pakket te bouwen, voer je als normale gebruiker (niet als root) het volgende commando uit:

```
makepkg

```

Makepkg zal dan de broncode voor het pakket downloaden en het pakket proberen te bouwen. Als je alle afhankelijkheden nog niet hebt geinstalleerd, zal makepkg je een waarschuwing geven, alvorens er mee te kappen. Om makepkg de benodigde afhankelijkheden automatisch te laten installeren met pacman, kun je de "-s" parameter meegeven aan makepkg:

```
makepkg -s

```

Merk op dat de afhankelijkheden in je geconfigureerde repository's aanwezig moeten zijn. Je kunt deze pakketten ook handmatig installeren met `pacman -S dep1 dep2 etc`.

Zodra alle afhankelijkheden zijn geinstalleerd en je pakket succesvol is gebouwd, zou je het bestand rufus-0.7.0-1.pkg.tar.gz in de huidige map moeten hebben staan (tenzij je in makepkg.conf een PKGDEST hebt opgegeven). Om het pakket te installeren, gebruik je het volgende commando (als gebruiker root):

```
pacman -U rufus-0.7.0-1.pkg.tar.gz

```

## Installeren vanuit bouwscripts

Soms krijgen we alleen *.pkgbuild bestanden van 3rd party repository's. In dat geval kun je het volgende commando gebruiken:

```
$ makepkg -p <file>

```

Gefeliciteerd! Je hebt nu met succes je eigen pakket gebouwd en geinstalleerd!

## Handige links

*   [Creating packages](/index.php/Creating_packages "Creating packages")
*   [AUR](https://aur.archlinux.org)
*   [de Makepkg manual](https://www.archlinux.org/pacman/makepkg.8.html)
*   [Arch CVS & SVN PKGBUILD guidelines](/index.php/Arch_CVS_%26_SVN_PKGBUILD_guidelines "Arch CVS & SVN PKGBUILD guidelines")
*   [Makepkg.conf](/index.php/Makepkg.conf "Makepkg.conf")