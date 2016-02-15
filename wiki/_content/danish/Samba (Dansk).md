**BEMÆRK:**Dette er mere, hvad jeg har gjort, for at få SAMBA til at virke på min maskine. Der er altså ikke nogen garanti for, at det vil virke på din.

Først skal du sørge for, at du har en arbejdsgruppe i det hjemmenetværk, hvori du vil dele filer. Dette kommer vi til senere.

## Contents

*   [1 Installér Samba](#Install.C3.A9r_Samba)
*   [2 Installation via terminal](#Installation_via_terminal)
    *   [2.1 Globale parametre](#Globale_parametre)
    *   [2.2 Fildelingsmapper](#Fildelingsmapper)
    *   [2.3 Adgangskoder](#Adgangskoder)
    *   [2.4 Start Samba](#Start_Samba)

## Installér Samba

Dernæst installér SAMBA (som 'root') med:

```
pacman -S samba

```

## Installation via terminal

For nu at dele de aktuelle data, skal du (stadig som 'root') gå ind i mappen, hvor smb.conf (konfigurationsfilen for Samba) ligger.
Denne fil indeholder både konfigurationsindstillinger og informationer om fildeling, der benyttes af Samba.

```
cd /etc/samba

```

Under installation gemmes en standard konfigurationsfil. Lav en kopi af filen:

```
cp smb.conf.default smb.conf

```

Redigér filen med f.eks. Nano:

```
nano smb.conf

```

### Globale parametre

Den første sektion er _Global Parameters_ (globale parametre). Dette henviser til de bredere valgmuligheder. De fleste indstillinger laves her. Her er sektionen _Global Parameters_ fra min /etc/samba/smb.conf til sammenligning.

```
#Global Parameters
workgroup = HOME
netbios name = Bennett-DSLIN
encrypt passwords = yes

```

Parameteren _workgroup_ er navnet på den arbejdsgruppe, du ønsker, at maskinen skal være en del af. (Standard i Windows XP er MSHOME og WORKGROUP.)
Valgmuligheden _encrypt passwords_ (kryptér adgangskoder) burde forblive _yes_ (ja). Dette kan variere, hvis din anden maskine kører Windows 95 eller Windows 98, da disse tidligere versioner anvendte ikke-krypterede adgangskoder.
Parameteren "netbios name" er hvordan du vil have, at din maskine skal fremstå på netværket.

### Fildelingsmapper

For at sætte fildelingerne op, er den enkleste, hvor en bruger kan tilgå og skrive i sin egen hjemmemappe.

```
[homes]
browseable = no
read only = no

```

Hvis du ønsker, at alle skal kunne se filerne, men kun særlige grupper skal kunne skrive (dvs. alle kan læse, men kun f.eks. gruppen _staff_ kan skrive), skal sektionen se således ud:

```
[homes]
public = yes
writable = yes
write list = @staff

```

Hvis du vil ha', at alm. Windows-brugere skal se en 'ren' hjemmeside, uden at blive forvirrede over alle 'dot-filerne' (eks.: ~/.bashrc), skal sektionen se nogenlunde således ud:

```
[homes]
path = /home/%u/smb
browseable = no
read only = no

```

Husk at føje _smb_ til alles hjemmemapper. Føj også _smb_ til mappen /etc/skel, så alle nye brugere automatisk får føjet _smb_ til deres hjemmemappe:

```
 mkdir /etc/skel/smb

```

At gå ind i en fildelingsmappe ud over hjemmemappen er ikke sværere end at der egentlig kun er yderligere 2 parametre, der ikke lader sig anvende til hjemmemapperne. Det er søgestien (_path_) og 'godkendte brugere' (_valid users_).
Et eksempel: Moving on to shares other than the home directory isn't much harder, as there are really only two more commands that did not apply to the homes. These are the path command and the valid users. Looks like this:

```
[music]
path = /mnt/windows/Music/
browseable = yes
read only = yes
valid users = Bryan, Michael, David, Jane

```

Søgestien (_path_) er selvfølgelig, hvor på harddisken fildelingsmappen findes. Ganske enkelt - ikke?
Parameteren _valid users_ (godkendte brugere) lader Samba vide, hvilke brugere der overhovedet har lov til at logge ind på fildelingsområdet. Igen - ganske enkelt, selvom det giver os lidt mere arbejde.
Glem ikke, at brugernavnene **skal** stemme overens med brugerne på Linux-maskinen, og **bør** stemme overens med brugere på Windows-maskinen.

### Adgangskoder

Når filen /etc/samba/smb.conf er sat op, som du vil have det, skal du gemme og afslutte editoren (i Nano er det ctrl+O efterfulgt af ctrl+X).
Vi skal så have føjet brugere til Sambas brugerliste. Dette gøres med:

```
smbpasswd -a <brugernavn>

```

Følg instruktionerne, og opret adgangskoderne til de samme som Windows-adgangskoderne og brugernavnene til de samme som Linux-brugeren. Når du har gjort det, er du færdig (næsten).

### Start Samba

Start (eller genstart) Samba-dæmonen med flg. kommandoer (som 'root'):

```
/etc/rc.d/samba stop
/etc/rc.d/samba start

```

Nu kan du så løbe ovenpå (eller hvor den anden computer befinder sig) og genstarte. Log ind som en af de godkendte brugere, når systemet er klar efter boot, og prøv at tilgå dine delefiler. Dertil skal du anvende adgangskoden fra smbpasswd-trinet.

Hvis alt fungerer tilfredsstillende, kan du føje 'samba' til dine dæmoner i /etc/rc.conf

```
 DAEMONS=(syslog-ng network ... samba ...)

```