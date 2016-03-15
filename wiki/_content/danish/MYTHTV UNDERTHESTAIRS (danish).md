## Contents

*   [1 Introduktion](#Introduktion)
*   [2 Strukturen](#Strukturen)
    *   [2.1 mythbackend](#mythbackend)
    *   [2.2 mythfrontend](#mythfrontend)
*   [3 Under Trappen Løsningen](#Under_Trappen_L.C3.B8sningen)
    *   [3.1 Forberedelser](#Forberedelser)
*   [4 Installation af MythTV](#Installation_af_MythTV)
*   [5 Autostart af Frontend](#Autostart_af_Frontend)

## Introduktion

MythTV er en samlet applikation, designet til levere fantastiske multimedie oplevelser. Det leverer PVR-funktionen(Personal Video Recorder) til en linux baseret PC og supporterer også andre medietyper - såsom Xbox, IPhone og Windowsmobile. Kombineret med en stille Computer(Støjsvag) og et ordentligt TV - giver det et fantastisk alternativ til en hjemmebiograf.

* * *

Denne artikel foreskriver at man har leget med MythTV et stykke tid og forstår de muligheder og løsninger der kan være til de enkelte setup's mm.

## Strukturen

MythTV systemet er delt op i 2dele - 1 backend og frontend, hvor hver komponent har sine egne funktioner:

### mythbackend

*   Planlæg og optager TV, samt afspille LiveTV
*   Streame video data til frontends
*   Markerer reklamepause
*   Transcode videor fra det ene format til et andet

### mythfrontend

*   leverer en flot GUI
*   Afspiller optaget indhold
*   Leverer et interface til at planlægge optagelser

Frontend og Backend kan både være på seperate maskiner i et netværk, men der kan også være flere frontends på samme system. Arkitekturen tillader nemlig en central distribuering af medier der kan nå alle steder et netværk også kan. Det er et usædvanligt flexibelt system, som også muliggør meget små strømbesparende maskiner som de perfekte frontends.

## Under Trappen Løsningen

Som "Undertrappen" løsningen menes der, at vores Backend bliver gemt væk "under Trappen", imens den leverer fuldt funktionsdygtigt TV/medie til hele huset. Dette skal forståes således at backend maskinen kører konstant og styrer alle optagelser,trancodninger, reklamemærkning mm, og selve frontends kobler op til Backenden og henter diverse data mm. For at forklare vores setup lidt nemmere er der et overblik her:

```
    Netværk range: 10.0.0.0/24 
    dhcp range:    10.0.0.50 - 10.0.0.100
    Masterbackend IP: 10.0.0.10
    Gateway:          10.0.0.1

```

### Forberedelser

For opbevaring af Musik,TV,film mm på tværs af netværket, skal man beslutte hvor man vil ligge disse data. Jeg har valgt at oprette et bibliotek /storage - hvorefter jeg kan mounte diverse diske i dette bibliotek og dermed undgå min / bliver fyldt pga musik film mm.

```
    mkdir -p /storage/music
    mkdir -p /storage/movies
    mkdir -p /storage/records
    mkdir -p /storage/pictures

```

For at kunne installere og udvide ens system med de detaljer omkring musik,film mm på tværs af hele netværket - starter man med at installere NFS, som vil dele (kun linuxmaskiner) netværksdrev.

```
  # pacman -S nfs-common

```

Man skal nu vælge om man vil lade MythTV køre som root eller som seperat bruger - hvor jeg har valgt en seperat bruger for at adskille det lidt.Men for at sikre systemet har jeg valgt en specifik bruger - nemlig myth

```
    # adduser myth

```

Derefter chown'er vi bibliotekerne vi har oprettet og gør klar til brug af disse.

```
    # chown -R myth /storage
    # chmod -R 777 /storage

```

Nu skal filerne så exporteres via netværket, og dette sættes op i filen /etc/export.conf - ved at tiolføje dette i filen:

```
    ###################################################
    # My shared discs for use in my MythTV system
    ###################################################
    /storage/movies         10.0.0.1/24(rw,sync,subtree_check)
    /storage/music          10.0.0.1/24(rw,sync,subtree_check)
    /storage/pictures       10.0.0.1/24(rw,sync,subtree_check)
    /storage/records        10.0.0.1/24(rw,sync,subtree_check)

```

dette betyder at klienter indenfor det defineret subnet - kan mounte disse drev. Man skal også lige huske at ændre en linie i /etc/conf.d/nfs

```
    STATD_OPTS="—no-notify"

```

Og tilsidst skal man sikre sig at diverse host må connecte til masterbackend og adgang er muligt. Dette gøres ved at tilføje regler i /etc/hosts.allow:

```
    sshd: ALL
    nfsd: ALL
    portmap: ALL
    mountd: ALL
    statd: ALL
    rquotad: ALL
    lockd: ALL
    mysqld: ALL

```

Her kan man også se, adgang til MySQL er tilladt samt SSH(for adgang via konsol) Hermed er vores share så opsat på vores CORE-server(Som jeg kalder min Backend).

* * *

Da denne er vigtig for at vi kan rippe DVD mm fra vores Frontends, da vores bruger(myth) skal have adgang til denne. Jeg roede længe med at jeg ikke kunne få adgang til denne og kunne ikke få lov til at rippe DVD'er og musik. Derfor fandt jeg ud af denne løsning. Istedet for at skulle starte mtd(som mythtranscode hedder) som almindelig rootdaemon, skal den opstartes som vores bruger. Derfor har jeg indsat denne linie i /etc/rc.local:

```
    su myth -c 'mtd -d'

```

Nu skal resten af installationen foregå ligesom ved almindelig installation af backendserver [som beskrevet her:](/index.php/MYTHTV_HOWTO_(Dansk) "MYTHTV HOWTO (Dansk)") **(Dansk)** [MYTHTV HOWTO (Dansk)](/index.php/MYTHTV_HOWTO_(Dansk) "MYTHTV HOWTO (Dansk)")

## Installation af MythTV

Den generelle installation af MythTV, er beskrevet under Installationssiden, men da dette er en "Under trappen" løsning - er der nogle enkelte ting der skal tilpasses generelt imellem Frontends/backends. For det første skal vi have installeret MythTV (samme version) på alle frontends - det samme skal NFS - således at vi kan mounte de forskellige biblioteker shared fra Backend serveren:

```
    mkdir -p /storage/music
    mkdir -p /storage/movies
    mkdir -p /storage/records
    mkdir -p /storage/pictures

```

Husk at tilføje dette til opstartlinien i /etc/rc.conf DAEMONS, således at de starter ved boot!

Mangler man at installere NFS - gøres dette ved hjælp af følgende kommando:

```
  # pacman -S nfs-common

```

Man skal nu vælge om man vil lade MythTV køre som root eller som seperat bruger - hvor jeg har valgt en seperat bruger for at adskille det lidt.Men for at sikre systemet har jeg valgt en specifik bruger - nemlig myth

```
    # adduser myth

```

Derefter chown'er vi bibliotekerne vi har oprettet og gør klar til brug af disse.

```
    # chown -R myth /storage
    # chmod -R 777 /storage

```

for at disse netværksdrev bliver mountet ved boot, tilføjes følgende i /etc/fstab:

```
10.0.0.10:/storage/music        /storage/music                nfs        rw,sync        0        1
10.0.0.10:/storage/movies        /storage/movies                nfs        rw,sync        0        1
10.0.0.10:/storage/pictures        /storage/pictures        nfs        rw,sync        0        1
10.0.0.10:/storage/records        /storage/records        nfs        rw,sync        0        1 

```

Nu kan man så tjekke af di9verse drev bliver mountet med kommandoen:

```
$ mount -a

```

Det sidste man så stadig mangler på frontends også - er at få MTD til at fungere under samme bruiger som på Backend - så tilføj til /etc/rc-local

```
su myth -c 'mtd -d'

```

På alle frontends vil den reagere som om MythTV kører på localhost, og det skal vi lige ændre således at det kommer på plads - dette gøres med at editere indstillingeren i /home/myth/.mythtv/mysql.txt til at passe med jeres indstillinger - men hovedsagligt er det denne linie der er vigtigt:

```
DBHostName=localhost   -->  DBHostName=10.0.0.10

```

Men så skulle vi også kunne rippe DVD'er mm fra Frontend og alle andre steder i systemet.

## Autostart af Frontend

Efter at have fået lyd,grafik mm til at fungere ordentligt i almindelig GNOME, kan vi nu sætte vores Frontend til at starte automatisk ved opstart. Under

```
System -> Indstillinger -> Sessioner

```

kan man nu oprette et nyt opstartsprogram. Navn: MythFrontend Kommando: mythfrontend Hvis man vil have logfil på til test eller lign, kan kommandoen istedet for være: Kommando: mythfrontend -v all > /var/log/mythfrontend.log Således vil man nu lige skulle oprette denne fil i /var/log/ og tillade myth at skrive i den:

```
$ touch /var/log/mythfrontend.log
$ chmod 777 /var/log/mythfrontend.log

```

Det sidste man kan er så at tillade brugeren myth at logge ind automatisk. Dette gøres under Systemer -> Administration -> Login skærm . Her kan man under sikkerhed aktivere automatisk login for myth. Dermed vil Mythfrontend starte fremover hvergang der logges ind på maskinen. Herefter kan man nu bruge sit system som en "Under trappen" installation.