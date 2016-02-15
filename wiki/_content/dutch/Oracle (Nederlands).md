Dit artikel behandelt de installatie van Oracle 11g (r2) - 64-bit.

**Note:** Arch Linux is geen door Oracle ondersteunde distributie !

In deze handleiding wordt er vanuit gegaan dat [Xorg](/index.php/Xorg "Xorg") is geconfigureerd en er een [Window manager](/index.php/Window_manager "Window manager") of [Desktop environment](/index.php/Desktop_environment "Desktop environment") is geinstalleerd.

## Contents

*   [1 Benodigdheden voor Oracle Database installatie](#Benodigdheden_voor_Oracle_Database_installatie)
    *   [1.1 Dependencies](#Dependencies)
    *   [1.2 Oracle user](#Oracle_user)
*   [2 Configuratie](#Configuratie)
    *   [2.1 Kernel parameters](#Kernel_parameters)
    *   [2.2 Pam Limits](#Pam_Limits)
    *   [2.3 Installatie](#Installatie)
    *   [2.4 Directory structuur](#Directory_structuur)
    *   [2.5 Installatie](#Installatie_2)
        *   [2.5.1 Errors](#Errors)
    *   [2.6 Start scripts](#Start_scripts)
    *   [2.7 Afronding](#Afronding)
    *   [2.8 Listener](#Listener)
*   [3 Post Install](#Post_Install)
*   [4 Listener IPv6 probleem](#Listener_IPv6_probleem)

## Benodigdheden voor Oracle Database installatie

### Dependencies

Vanuit de Arch repositories moet geinstalleerd worden:

*   base-devel
*   jre7-openjdk, pdksh, gdb, gawk, libelf, sysstat, libstdc++5, unzip, sudo, icu, lib32-libstdc++5, python2
*   gcc-multilib, gcc-libs-multilib, libtool-multilib

Vervolgens moeten er symbolic links worden aangemaakt omdat de installatie software bepaalde bestanden op andere locaties verwacht:

```
ln -s /usr/lib /usr/lib64
ln -s /usr/bin/basename /bin/basename
rm /usr/bin/python
ln -s /usr/bin/python2 /usr/bin/python
ln -s /usr/lib64/libgcc_s.so.1 /lib64/

```

**Note:** Tijdens de requirement check in de installatie wordt ook gezocht naar o.a. rpm. Deze is echter niet benodigd !

### Oracle user

Maak een gebruiker oracle aan die lid is van de groep oinstall en dba:

```
 groupadd oinstall
 groupadd dba
 useradd -m -g oinstall -G dba oracle

```

Configureer het wachtwoord voor deze gebruiker:

```
passwd oracle

```

Bewerk, bijvoorbeeld met `vi` het .bashrc bestand van deze gebruiker

```
sudo oracle
vi ~/.bashrc

```

En geef dit bestand de volgende inhoud:

```
export ORACLE_BASE=/oracle
export ORACLE_HOME=/oracle/product/db
export ORACLE_INVENTORY=/oracle/inventory
export ORACLE_SID=<SID van je DB>
export PATH=$ORACLE_HOME/bin:$PATH
export LD_LIBRARY_PATH=$ORACLE_HOME/lib:$LD_LIBRARY_PATH
export EDITOR=vi
export VISUAL=vi

```

Waarbij je de editor vi kunt vervangen bij variabelen EDITOR en VISUAL door je eigen favoriete editor. Vergeet niet je ORACLE_SID de juiste naam te geven. Dit is de SID die je verderop kiest bij de `dbca` tool. Wanneer je die nu nog niet weet, moet je dit na het draaien van dbca alsnog doen.

## Configuratie

### Kernel parameters

Een aantal kernel parameters moeten worden aangepast. Voeg aan het bestand `/etc/sysctl.d/99-sysctl.conf` het volgende toe:

```
fs.file-max = 6815744
fs.aio-max-nr = 1048576
kernel.shmall = 2097152
kernel.shmmax = 2147483648
kernel.shmmni = 4096
kernel.sem = 250 32000 100 128
net.ipv4.ip_local_port_range = 9000 65500
net.core.rmem_default = 4194304
net.core.rmem_max = 4194304
net.core.wmem_default = 262144
net.core.wmem_max = 1048576

```

En activeer deze instellingen met:

```
# sysctl --system

```

### Pam Limits

Ook de PAM module limits (Zie ook: [Realtime_process_management](/index.php/Realtime_process_management "Realtime process management")) moet geconfigureerd worden. Voeg aan het bestand /etc/security/limits.conf het volgende toe:

```
oracle           soft    nproc   2047
oracle           hard    nproc   16384
oracle           soft    nofile  1024
oracle           hard    nofile  65536

```

### Installatie

Het meest gemakkelijke is om nu als de gebruiker oracle in te loggen. Als alternatief:

```
DISPLAY=:0.0; export DISPLAY; xhost +
su - oracle
DISPLAY=:0.0; export DISPLAY

```

Download de software van: [http://www.oracle.com/technology/software/products/database/index.html](http://www.oracle.com/technology/software/products/database/index.html)

En unzip deze:

```
 su -
 unzip /usr/src/oracle/linux.x64_11gR2_database_2of2.zip -d /media
 unzip /usr/src/oracle/linux.x64_11gR2_database_2of2.zip -d /media

```

Op de nu ontstane directory structuur moeten de rechten worden aangepast:

```
 chown -R oracle:oinstall /media/database

```

### Directory structuur

Maak nu de directory structuur aan waar de Oracle software in geinstalleerd moet worden:

```
mkdir -p /oracle/{inventory,recovery,product/db}

```

### Installatie

Start nu de installatie software:

```
/media/database/runInstaller

```

Je krijgt nu een aantal vragen:

	Installation option

	"Install database software only"

	Grid Options

	"Single instance database installation"

	Product Languages

	"English"

	Database Edition

	"Enterprise Edition"

	Installation Location

	Oracle Base: /oracle en de Software Location: /oracle/product/db

	Create Inventory

	Inventory Directory: /oracle/inventory en de oraInventory Group Name: oinstall

	Operating System Groups

	Database Administrator Group: dba en de Database Operator Group: oinstall

	Prerequisite Checks

	Ignore all

#### Errors

Tijdens de installatie krijg je een aantal foutmeldingen. De eerste foutmelding in de bijbehorende logfile is:

**Note:** Deze foutmelding lijkt zich in 11gR2 x64 niet (meer) voor te doen...

```
INFO: /usr/lib64/libstdc++.so.5: undefined reference to `memcpy@GLIBC_2.14'
collect2: error: ld returned 1 exit status

```

Deze foutmelding negeren door op "Continue" te klikken. Helaas heeft dit wel tot gevolg dat de Lexical Compiler niet werkt. Deze Lexical Compiler wordt gebruikt om eigen chinese en japanse woordenboeken te kunnen genereren.

De volgende foutmelding geeft in het logbestand:

```
/oracle/product/db/lib/libnnz11.so: could not read symbols: Invalid operation
collect2: error: ld returned 1 exit status

```

Dit is op te lossen: open het bestand $ORACLE_HOME/sysman/lib/ins_emagent.mk in je favoriete editor en ga naar regel 190. Vervang `$(MK_EMAGENT_NMECTL)` door:

```
$(MK_EMAGENT_NMECTL) -lnnz11

```

Kies nu in de grafische installer voor "Retry"

### Start scripts

Wanneer je de Oracle Database wilt starten tijdens het bootproces dan moeten er een tweetal init scripts aangemaakt worden.

**/etc/rc.d/ora.listener**

```
#!/bin/sh
export ORACLE_HOME="/oracle/product/db"
export ORACLE_BASE=/oracle
export ORACLE_SID=<SID van je DB>
export ORACLE_INVENTORY=/oracle/inventory
export PATH=$ORACLE_HOME/bin:$PATH
export LD_LIBRARY_PATH=$ORACLE_HOME/lib:$LD_LIBRARY_PATH

case "$1" in
start)
 echo "Start Oracle Listeners"
 /bin/su oracle -c "$ORACLE_HOME/bin/lsnrctl start LISTENER"
 ;;
stop)
/bin/su oracle -c "$ORACLE_HOME/bin/lsnrctl stop LISTENER"
;;
esac

```

**/etc/rc.d/ora.database**

```
#!/bin/sh
export ORACLE_HOME="/oracle/product/db"
export ORACLE_BASE=/oracle
export ORACLE_SID=<SID van je DB>
export ORACLE_INVENTORY=/oracle/inventory
export PATH=$ORACLE_HOME/bin:$PATH
export LD_LIBRARY_PATH=$ORACLE_HOME/lib:$LD_LIBRARY_PATH

case "$1" in
start)
 echo "Start Oracle Database"
 /bin/su oracle -c "$ORACLE_HOME/bin/dbstart"
 ;;
stop)
 /bin/su oracle -c "$ORACLE_HOME/bin/dbshut"
 ;;
esac

```

Maak nu beide scripts executable:

```
chmod +x /etc/rc.d/ora*

```

Je kunt nu beide scripts aanroepen vanuit `/etc/rc.conf`

```
DAEMONS=( ... ora.listener ora.database ...)

```

Een alternatieve manier om de database te starten is door in te loggen op de inactieve database als sysdba:

```
$ su - oracle
$ sqlplus / as sysdba

```

En vervolgens

```
SQL> startup

```

In te voeren. Shutten van de DB doe je dan met:

```
SQL> shutdown immediate

```

De listener kan je starten en stoppen met lsnrctl:

```
$ su - oracle
$ lsnrctl start

```

of:

```
$ su - oracle
$ lsnrctl stop

```

### Afronding

Je krijgt nu in de grafische installer te zien dat 2 scripts als root moeten worden uitgevoerd:

```
su
/oracle/inventory/orainstRoot.sh
/oracle/product/db/root.sh

```

Het laatste script vraagt naar de full pathname. Vul hier in:

```
/usr/local/bin

```

### Listener

Als laatste stap moet de listener worden aangemaakt. Dit doe je door het starten (als gebruiker oracle) van een grafische tool:

```
netca

```

Beantwoord in de wizard de volgende vragen als volgt:

	Choose the configuration you would like to do

	Listener configuration

	Select what you want to do

	Add

	Listener name

	LISTENER

	Selected Protocols

	TCP

	Which TCP?IP port number should the listener use ?

	standard port number of 1521

	Would you like to configure another listener

	No

Vervolgens klik je op "Finish"

Wanneer je overigens verbinding maakt met een Oracle DB die op dezelfde machine draait, heb je geen listener nodig. Dit proces hoef je dan ook alleen maar op te starten wanneer je de DB van 'buitenaf' wilt kunnen benaderen, of wanneer je middels de thin jdbc driver verbinding maakt. Ook dan is de listener noodzakelijk.

## Post Install

Een database kan nu aangemaakt worden, door als gebruiker oracle de grafische tool te starten:

```
dbca

```

Nadat dit gedaan is bewerk je het bestand /etc/oratab

```
<your sid>:<oracle home>:N

```

Verander je in:

```
<your sid>:<oracle home>:Y

```

## Listener IPv6 probleem

Standaard staat de listener geconfigureerd om op `localhost.localdomain` te luisteren. Het lijkt er op dat Arch default op IPv6 inzet waardoor de database instance zich niet kan registreren bij de listener.

```
# lsnrctl status

```

Geeft dan:

```
The listener supports no services

```

Dit kan je oplossen door in `$ORACLE_HOME/network/admin` het bestand `listener.ora` te openen in een editor en de volgende regel:

```
      (ADDRESS = (PROTOCOL = TCP)(HOST = localhost.localdomain)(PORT = 1521))

```

te veranderen in:

```
      (ADDRESS = (PROTOCOL = TCP)(HOST = 127.0.0.1)(PORT = 1521))

```

Gebruik je externe IP adres ipv `127.0.0.1` wanneer je wilt dat de DB van buitenaf te benaderen is. Dit dwingt de listener om IPv4 te gebruiken.

Daarna zou een

```
# lsnrctl status

```

Weer moeten geven dat de database geregistreerd is:

```
Service "<SID name>" has 1 instance(s).
Instance "<SID name>", status READY, has 1 handler(s) for this service...

```