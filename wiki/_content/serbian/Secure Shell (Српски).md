Secure Shell или SSH је мрежни протокол који дозвољава размену података путем сигурног канала између два рачунара. Шифровање пружа поузданост и интегритет података. SSH користи криптографију јавног кључа за аутентификацију на удаљени рачунар и дозвољава удаљеном рачунару да аутентификује корисника, уколико је то неопходно.

SSH се обично користи за пријављивање на удаљени рачунар и извшавање команди, али се такође користи и за тунеловање, прослеђивање TCP портова и X11 веза; трансфер података се може извршити коришћењем додељених SFTP или SCP протокола.

SSH сервер слуша на стандардном TCP порту 22\. SSH клијент се користи за остваривање везе са *sshd* сервисом који прихвата удањене везе. Саставни су део модерних оперативних система као што су, Mac OS X, GNU/Linux, Solaris и OpenVMS. Постоје власничке, бесплатне и опен сорс верзије различитих нивоа комплексности.

(Source: [Wikipedia:Secure Shell](https://en.wikipedia.org/wiki/Secure_Shell "wikipedia:Secure Shell"))

## Contents

*   [1 OpenSSH](#OpenSSH)
    *   [1.1 OpenSSH инсталација](#OpenSSH_.D0.B8.D0.BD.D1.81.D1.82.D0.B0.D0.BB.D0.B0.D1.86.D0.B8.D1.98.D0.B0)
    *   [1.2 Конфигураисање SSH](#.D0.9A.D0.BE.D0.BD.D1.84.D0.B8.D0.B3.D1.83.D1.80.D0.B0.D0.B8.D1.81.D0.B0.D1.9A.D0.B5_SSH)
        *   [1.2.1 Клијент](#.D0.9A.D0.BB.D0.B8.D1.98.D0.B5.D0.BD.D1.82)
        *   [1.2.2 Сервис](#.D0.A1.D0.B5.D1.80.D0.B2.D0.B8.D1.81)
        *   [1.2.3 Дозвољавање приступа другим корисницима](#.D0.94.D0.BE.D0.B7.D0.B2.D0.BE.D1.99.D0.B0.D0.B2.D0.B0.D1.9A.D0.B5_.D0.BF.D1.80.D0.B8.D1.81.D1.82.D1.83.D0.BF.D0.B0_.D0.B4.D1.80.D1.83.D0.B3.D0.B8.D0.BC_.D0.BA.D0.BE.D1.80.D0.B8.D1.81.D0.BD.D0.B8.D1.86.D0.B8.D0.BC.D0.B0)
    *   [1.3 Управљање SSHD процесом](#.D0.A3.D0.BF.D1.80.D0.B0.D0.B2.D1.99.D0.B0.D1.9A.D0.B5_SSHD_.D0.BF.D1.80.D0.BE.D1.86.D0.B5.D1.81.D0.BE.D0.BC)
    *   [1.4 Повезивање на сервер](#.D0.9F.D0.BE.D0.B2.D0.B5.D0.B7.D0.B8.D0.B2.D0.B0.D1.9A.D0.B5_.D0.BD.D0.B0_.D1.81.D0.B5.D1.80.D0.B2.D0.B5.D1.80)
*   [2 Савети и трикови](#.D0.A1.D0.B0.D0.B2.D0.B5.D1.82.D0.B8_.D0.B8_.D1.82.D1.80.D0.B8.D0.BA.D0.BE.D0.B2.D0.B8)
    *   [2.1 Шифровани тунел](#.D0.A8.D0.B8.D1.84.D1.80.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8_.D1.82.D1.83.D0.BD.D0.B5.D0.BB)
        *   [2.1.1 Корак 1: Успостављање везе](#.D0.9A.D0.BE.D1.80.D0.B0.D0.BA_1:_.D0.A3.D1.81.D0.BF.D0.BE.D1.81.D1.82.D0.B0.D0.B2.D1.99.D0.B0.D1.9A.D0.B5_.D0.B2.D0.B5.D0.B7.D0.B5)
        *   [2.1.2 Корак 2: Конфигурисање браузера (или других програма)](#.D0.9A.D0.BE.D1.80.D0.B0.D0.BA_2:_.D0.9A.D0.BE.D0.BD.D1.84.D0.B8.D0.B3.D1.83.D1.80.D0.B8.D1.81.D0.B0.D1.9A.D0.B5_.D0.B1.D1.80.D0.B0.D1.83.D0.B7.D0.B5.D1.80.D0.B0_.28.D0.B8.D0.BB.D0.B8_.D0.B4.D1.80.D1.83.D0.B3.D0.B8.D1.85_.D0.BF.D1.80.D0.BE.D0.B3.D1.80.D0.B0.D0.BC.D0.B0.29)
    *   [2.2 X11 прослеђивање](#X11_.D0.BF.D1.80.D0.BE.D1.81.D0.BB.D0.B5.D1.92.D0.B8.D0.B2.D0.B0.D1.9A.D0.B5)
    *   [2.3 Убрзавање SSH](#.D0.A3.D0.B1.D1.80.D0.B7.D0.B0.D0.B2.D0.B0.D1.9A.D0.B5_SSH)
        *   [2.3.1 Решавање проблема](#.D0.A0.D0.B5.D1.88.D0.B0.D0.B2.D0.B0.D1.9A.D0.B5_.D0.BF.D1.80.D0.BE.D0.B1.D0.BB.D0.B5.D0.BC.D0.B0)
    *   [2.4 Монтирање удаљених фајл система коришћењем SSHFS](#.D0.9C.D0.BE.D0.BD.D1.82.D0.B8.D1.80.D0.B0.D1.9A.D0.B5_.D1.83.D0.B4.D0.B0.D1.99.D0.B5.D0.BD.D0.B8.D1.85_.D1.84.D0.B0.D1.98.D0.BB_.D1.81.D0.B8.D1.81.D1.82.D0.B5.D0.BC.D0.B0_.D0.BA.D0.BE.D1.80.D0.B8.D1.88.D1.9B.D0.B5.D1.9A.D0.B5.D0.BC_SSHFS)
    *   [2.5 Одржавање везе](#.D0.9E.D0.B4.D1.80.D0.B6.D0.B0.D0.B2.D0.B0.D1.9A.D0.B5_.D0.B2.D0.B5.D0.B7.D0.B5)
    *   [2.6 Чување података у .ssh/config](#.D0.A7.D1.83.D0.B2.D0.B0.D1.9A.D0.B5_.D0.BF.D0.BE.D0.B4.D0.B0.D1.82.D0.B0.D0.BA.D0.B0_.D1.83_.ssh.2Fconfig)
*   [3 Решавање проблема](#.D0.A0.D0.B5.D1.88.D0.B0.D0.B2.D0.B0.D1.9A.D0.B5_.D0.BF.D1.80.D0.BE.D0.B1.D0.BB.D0.B5.D0.BC.D0.B0_2)
    *   [3.1 Connection Refused проблем](#Connection_Refused_.D0.BF.D1.80.D0.BE.D0.B1.D0.BB.D0.B5.D0.BC)
        *   [3.1.1 Is SSH running and listening?](#Is_SSH_running_and_listening.3F)
        *   [3.1.2 Да ли firewall блокира безу?](#.D0.94.D0.B0_.D0.BB.D0.B8_firewall_.D0.B1.D0.BB.D0.BE.D0.BA.D0.B8.D1.80.D0.B0_.D0.B1.D0.B5.D0.B7.D1.83.3F)
        *   [3.1.3 Да ли је SSH додат у hosts.allow?](#.D0.94.D0.B0_.D0.BB.D0.B8_.D1.98.D0.B5_SSH_.D0.B4.D0.BE.D0.B4.D0.B0.D1.82_.D1.83_hosts.allow.3F)
        *   [3.1.4 Да ли саобраћај стиже до рачуанра?](#.D0.94.D0.B0_.D0.BB.D0.B8_.D1.81.D0.B0.D0.BE.D0.B1.D1.80.D0.B0.D1.9B.D0.B0.D1.98_.D1.81.D1.82.D0.B8.D0.B6.D0.B5_.D0.B4.D0.BE_.D1.80.D0.B0.D1.87.D1.83.D0.B0.D0.BD.D1.80.D0.B0.3F)
*   [4 Такође погледајте](#.D0.A2.D0.B0.D0.BA.D0.BE.D1.92.D0.B5_.D0.BF.D0.BE.D0.B3.D0.BB.D0.B5.D0.B4.D0.B0.D1.98.D1.82.D0.B5)
*   [5 Линкови и препоруке](#.D0.9B.D0.B8.D0.BD.D0.BA.D0.BE.D0.B2.D0.B8_.D0.B8_.D0.BF.D1.80.D0.B5.D0.BF.D0.BE.D1.80.D1.83.D0.BA.D0.B5)

# OpenSSH

OpenSSH (OpenBSD Secure Shell) је комплет рачунарских програма који пружају шифровану комуникацију преко рачунарске мреже коришћењем ssh протокола. Направљен је као опен сорс алтернатива власничком Secure Shell софтверском пакету који нуди SSH Communications Security. OpenSSH је разијен као део OpenBSD пројекта, који води Theo de Raadt.

OpenSSH се често меша са OpenSSL; ипак, пројекти имају различите сврхе и развијају их различити тимови.

## OpenSSH инсталација

```
# pacman -S openssh

```

## Конфигураисање SSH

### Клијент

SSH клијентска конфигурација се може наћи и изменити у `/etc/ssh/ssh_config`.

Пример конфигурације:

 `/etc/ssh/ssh_config` 
```
#       $OpenBSD: ssh_config,v 1.25 2009/02/17 01:28:32 djm Exp $

# This is the ssh client system-wide configuration file.  See
# ssh_config(5) for more information.  This file provides defaults for
# users, and the values can be changed in per-user configuration files
# or on the command line.

# Configuration data is parsed as follows:
#  1\. command line options
#  2\. user-specific file
#  3\. system-wide file
# Any configuration value is only changed the first time it is set.
# Thus, host-specific definitions should be at the beginning of the
# configuration file, and defaults at the end.

# Site-wide defaults for some commonly used options.  For a comprehensive
# list of available options, their meanings and defaults, please see the
# ssh_config(5) man page.

Host *
#   ForwardAgent no
#   ForwardX11 no
#   RhostsRSAAuthentication no
#   RSAAuthentication yes
#   PasswordAuthentication yes
#   HostbasedAuthentication no
#   GSSAPIAuthentication no
#   GSSAPIDelegateCredentials no
#   BatchMode no
#   CheckHostIP yes
#   AddressFamily any
#   ConnectTimeout 0
#   StrictHostKeyChecking ask
#   IdentityFile ~/.ssh/identity
#   IdentityFile ~/.ssh/id_rsa
#   IdentityFile ~/.ssh/id_dsa
#   Port 22
#   Protocol 2,1
#   Cipher 3des
#   Ciphers aes128-ctr,aes192-ctr,aes256-ctr,arcfour256,arcfour128,aes128-cbc,3des-cbc
#   MACs hmac-md5,hmac-sha1,umac-64@openssh.com,hmac-ripemd160
#   EscapeChar ~
#   Tunnel no
#   TunnelDevice any:any
#   PermitLocalCommand no
#   VisualHostKey no
HashKnownHosts yes
StrictHostKeyChecking ask
```

Препоручљиво је да се линија Protocol промени да изгледа овако:

```
Protocol 2

```

То значи да ће само Protocol 2 бити коришћен, пошто се Protocol 1 сматра несигурним.

### Сервис

SSH сервисни конфигурациони фајл се може наћи и изменити у `/etc/ssh/ssh**d**_config`.

Пример конфигурације:

 `/etc/ssh/sshd_config` 
```
#	$OpenBSD: sshd_config,v 1.75 2007/03/19 01:01:29 djm Exp $

# This is the sshd server system-wide configuration file.  See
# sshd_config(5) for more information.

# This sshd was compiled with PATH=/usr/bin:/bin:/usr/sbin:/sbin

# The strategy used for options in the default sshd_config shipped with
# OpenSSH is to specify options with their default value where
# possible, but leave them commented.  Uncommented options change a
# default value.

#Port 22
#Protocol 2,1
ListenAddress 0.0.0.0
#ListenAddress ::

# HostKey for protocol version 1
#HostKey /etc/ssh/ssh*host*key
# HostKeys for protocol version 2
#HostKey /etc/ssh/ssh*host*rsa_key
#HostKey /etc/ssh/ssh*host*dsa_key

# Lifetime and size of ephemeral version 1 server key
#KeyRegenerationInterval 1h
#ServerKeyBits 768

# Logging
#obsoletes ~QuietMode and ~FascistLogging
#SyslogFacility AUTH
#LogLevel INFO

# Authentication:

#LoginGraceTime 2m
#PermitRootLogin yes
#StrictModes yes
#MaxAuthTries 6

#RSAAuthentication yes
#PubkeyAuthentication yes
#AuthorizedKeysFile     .ssh/authorized_keys

# For this to work you will also need host keys in /etc/ssh/ssh*known*hosts
#RhostsRSAAuthentication no
# similar for protocol version 2
#HostbasedAuthentication no
# Change to yes if you don't trust ~/.ssh/known_hosts for
# RhostsRSAAuthentication and HostbasedAuthentication
#IgnoreUserKnownHosts no
# Don't read the user's ~/.rhosts and ~/.shosts files
#IgnoreRhosts yes

# To disable tunneled clear text passwords, change to no here!
#PasswordAuthentication yes
#PermitEmptyPasswords no

# Change to no to disable s/key passwords
#ChallengeResponseAuthentication yes

# Kerberos options
#KerberosAuthentication no
#KerberosOrLocalPasswd yes
#KerberosTicketCleanup yes
#KerberosGetAFSToken no

# GSSAPI options
#GSSAPIAuthentication no
#GSSAPICleanupCredentials yes

# Set this to 'yes' to enable PAM authentication, account processing,
# and session processing. If this is enabled, PAM authentication will
# be allowed through the ~ChallengeResponseAuthentication mechanism.
# Depending on your PAM configuration, this may bypass the setting of
# PasswordAuthentication, ~PermitEmptyPasswords, and
# "PermitRootLogin without-password". If you just want the PAM account and
# session checks to run without PAM authentication, then enable this but set
# ChallengeResponseAuthentication=no
#UsePAM no

#AllowTcpForwarding yes
#GatewayPorts no
#X11Forwarding no
#X11DisplayOffset 10
#X11UseLocalhost yes
#PrintMotd yes
#PrintLastLog yes
#TCPKeepAlive yes
#UseLogin no
#UsePrivilegeSeparation yes
#PermitUserEnvironment no
#Compression yes
#ClientAliveInterval 0
#ClientAliveCountMax 3
#UseDNS yes
#PidFile /var/run/sshd.pid
#MaxStartups 10

# no default banner path
#Banner /some/path

# override default of no subsystems
Subsystem       sftp    /usr/lib/ssh/sftp-server
```

За дозвољавање приступа само одређеним корисницима треба додати следећу линију:

```
AllowUsers    user1 user2

```

Можете променити и линије које изгледају као следеће:

```
Protocol 2
.
.
.
LoginGraceTime 120
.
.
.
PermitRootLogin no # (put yes here if you want root login)

```

Може се и склонити коментар са опције BANNER и изменити `/etc/issue` како би добили поруку добродошлице.

**Tip:** Може се променити подразумевани порт са 22 на неки други виши порт (види [security through obscurity](https://en.wikipedia.org/wiki/Security_through_obscurity "wikipedia:Security through obscurity")).

Иако се порт који је додељен ssh може детектовати коришћењем порт скенера као што је nmap, мењање порта ће смањити број уноса у дневник.

**Tip:** Онемогућавање шифре при пријављивању може повећати сигурност, пошто сваки корисник који приступа серверу мора да креира ssh кључ. (види [Using SSH Keys](/index.php/Using_SSH_Keys "Using SSH Keys")).
 `/etc/ssh/sshd_config` 
```
PasswordAuthentication no
ChallengeResponseAuthentication no
```

### Дозвољавање приступа другим корисницима

**Note:** Морате подесити овај фајл да би се удаљено повезали на Ваш рачунар пошто је после инсталације овај фајл празан.

Да дозволите другим корисницима да се повежу на Ваш рачунар мора се подесити `/etc/hosts.allow`, и додати следеће:

```
# let everyone connect to you
sshd: ALL

# OR you can restrict it to a certain ip
sshd: 192.168.0.1

# OR restrict for an IP range
sshd: 10.0.0.0/255.255.255.0

# OR restrict for an IP match
sshd: 192.168.1.

```

Сад треба проверити `/etc/hosts.deny` и постарати се да изгледа овако:

```
ALL: ALL

```

Да би користили нову конфигурацију, треба ресетовати сервис (као root):

```
# /etc/rc.d/sshd restart

```

## Управљање SSHD процесом

Треба додати sshd з "DAEMONS" одељак `/etc/[rc.conf](/index.php/Rc.conf "Rc.conf")`:

```
DAEMONS=(... ... **sshd** ... ...)

```

За start/restart/stop процеса, треба користити следеће:

```
# /etc/rc.d/sshd {start|stop|restart}

```

## Повезивање на сервер

За повезивање на сервер, покренути:

```
$ ssh -p port user@server-address

```

# Савети и трикови

## Шифровани тунел

Ово је корисно за лаптоп кориснике који су повезани на несигурне бежичне везе. Једина ствар која је потребна је SSH сервер покренут са неке сигурне локације, као што је кућа или са посла. Корисно је користити динамички DNS као што је [DynDNS](http://www.dyndns.org/) да не би морали да памтимо нашу IP адресу.

### Корак 1: Успостављање везе

Потребмо је извршити једну команту у Вашем омиљеном терминалу како би се веза успоставила:

```
$ ssh -ND 4711 user@host

```

где је `"user"` корисничко име на SSH серверу покренутом на `"host"`. Тражиће Вашу шифру, и онда сте повезани. `"N"` застава онемогућава интерактивну командну линију, а `"D"` застава спецификује локални порт на којем процес слуша (порт је могуће изабрати).

Један од начина са олакшавање успотаве везе је додавање псеудонима у `~/.bashrc` фајл:

```
alias sshtunnel="ssh -ND 4711 -v user@host"

```

Корисно је додати verbose заставу `"-v"`, јер тада можете да проверите да ли је то заиста повезано са тог излаза. Сад само морате да извршите `"sshtunnel"` команду.

### Корак 2: Конфигурисање браузера (или других програма)

Пређашњи корак је беспотребан ако се не конфигурише браузер (или други програми) за коришћење новокреираног тунела.

*   За Firefox: *Edit → Preferences → Advanced → Network → Connection → Setting*:

	Проверити *"Manual proxy configuration"* дугме, и унети "localhost" з *"SOCKS host"* текстуално поље, и онда унети број порта у следеће поље.

	Постарајте се да изаберете SOCKS4 као протокол који ће се користити. Ова процедура неће радити са SOCKS5.

## X11 прослеђивање

Да би користили графичке програме кроз SSH везу може се омогућити X11 прослеђивање. Једна опција се мора подесити у конфигурационим фајловима на серверу и клијенту (клијент представља десктоп рачунар са покренутим X11 сервером).

Инсталација xorg-xauth на сервер:

```
# pacman -S xorg-xauth

```

*   Омогућити **AllowTcpForwarding** опцију у `sshd_config` на **серверу**.
*   Омогућити **X11Forwarding** опцију у `sshd_config` на **серверу**.
*   Подесити **X11DisplayOffset** опцију у `sshd_config` на **серверу** до 10.
*   Омогућити **X11UseLocalhost** опцију у `sshd_config` на **северу**.

*   Омогућити **ForwardX11** опцију у `ssh_config` на **клијенту**.

Да би користили прослеђивање, потребно је повезати се на север помоћу ssh:

```
# ssh -X -p port user@server-address

```

Ако добијете грешке при покушају покретања графичких апликација пробајте поуздано прослеђивање:

```
# ssh -Y -p port user@server-address

```

Сад се може покренути било који X програм на удаљеном серверу, излаз ће бити прослеђен на локалну сесију:

```
# xclock

```

Ако се добије "Cannot open display" грешка, треба пробати следећу команду као не root корисник:

```
$ xhost +

```

ова команда ће дозволити свима прослеђивање X11 апликација. За ограничење прослеђивања на одређени хост треба уписати следеће:

```
$ xhost +hostname

```

где је hostname име одређеног хоста на који треба прослеђивати. Откуцајте "man xhost" за више детаља.

## Убрзавање SSH

Могуће је креирати све сесије ка истом хосту да користе једну везу, што ће повећати следећа пријављивања, додавањем тих линија под одговарајући хост у `/etc/ssh/ssh_config`:

```
ControlMaster auto
ControlPath ~/.ssh/socket-%r@%h:%p

```

Мењање шифре коју користи SSH на оне које мање захтевају побољшавају брзину. Код овог аспекта, најбољи избор су arcfour и blowfish-cbc. **Не радите ово ако не знате шта радите; arcfour има велики број познатих слабости**. Да би их користили, покрените SSH са `"c"` заставом, на овај начин:

```
# ssh -c arcfour,blowfish-cbc user@server-address

```

Да би их користили за стално, треба додати линију испод одговарајућег хоста у `/etc/ssh/ssh_config`:

```
Ciphers arcfour,blowfish-cbc

```

Друга опција за побољшавањне брзине је омогућавањне компресије са `"C"` заставом. Стално решење је додавање ове линије испод одговарајућег хоста у `/etc/ssh/ssh_config`:

```
Compression yes

```

Време пријављивањна се може смањити коришћењем `"4"` заставе, која заобилази IPv6 проналажење. Ово се може начинити сталним додавањем линије испод одговарајућег хоста у `/etc/ssh/ssh_config`:

```
AddressFamily inet

```

Други начин да ове промене остану сталне је креирање псеудонима у `~/.bashrc`:

```
alias ssh='ssh -C4c arcfour,blowfish-cbc'

```

### Решавање проблема

Постарајте се да је разрешавање DISPLAY низа омогућено на крају :

```
ssh -X user@server-address
server$ echo $DISPLAY
localhost:10.0
server$ telnet localhost 6010
localhost/6010: lookup failure: Temporary failure in name resolution   

```

Може се средити додавањем localhost з `/etc/hosts`.

## Монтирање удаљених фајл система коришћењем SSHFS

Инсталација sshfs

```
# pacman -S sshfs

```

Потребно је учитати Fuse модул

```
# modprobe fuse

```

Додавање fuse у *modules* одељак фајла `/etc/rc.conf` ће омогућити његово учитавање после сваког бутовања.

Монтирање удаљених фолдера помоћу sshfs

```
# mkdir ~/remote_folder
# sshfs USER@remote_server:/tmp ~/remote_folder

```

Ова команда ће монтирати фолдер /tmp са удаљеног сервера да се монтира као ~/remote_folder на локалном рачунару. Копирање фајлова у овај фолдер ће резултовати траспарентно копирање преко мреже помоћу SFTP. Исто се односи и на директно мењање фајлова, прављење нових или уклањање.

Кад се рад са удаљеним фајл системима заврши, демонтирање фолдера се врши на следећи начин:

```
# fusermount -u ~/remote_folder

```

Ако се на неком фолдеру ради свакодневно. паметно је додати га у `/etc/fstab` табелу. На овај начин фолдер ће се аутоматски монтирати кад се систем бутује или ручно монтира (ако је `noauto` опција изабрана) без потребе да се удаљена локација спецификује сваки пут. Ово је пример уноса у табелу:

```
sshfs#USER@remote_server:/tmp /full/path/to/directory fuse    defaults,auto,allow_other    0 0

```

## Одржавање везе

SSH сесија ће се аутоматски одјавити кад је у разном ходу (idle). Да се ова беза одржава нон стоп треба додати следећу линију у `~/.ssh/config` или у `/etc/ssh/ssh_config` на клијенту.

```
ServerAliveInterval 120

```

Ово ће послати "keep alive" сигнал серверу сваких 120 секунди.

Обрнуто, за одржавање долазећих веза, може се подесити

```
ClientAliveInterval 120

```

(или неки број већи од 0) у `/etc/ssh/sshd_config` на серверу.

## Чување података у .ssh/config

Кад год се повежемо на сервер, обично уносимо његову адресу и наше корисничко име. Да би сачували податке које уносимо за сервере које често користимо, може се користити `$HOME/.ssh/config` фајл на начин који је приказан у следећем примеру:

 `$HOME/.ssh/config` 
```
Host myserver
    HostName 123.123.123.123
    Port 12345
    User bob
Host other_server
    HostName test.something.org
    User alice
    CheckHostIP no
    Cipher blowfish

```

Сад се можемо једноставно повезати на сервер коришћењем имена које је наглашено:

```
$ ssh myserver

```

За комплетну листу могућих опција, треба прегледати ssh_config manpage или [ssh_config documentation](http://www.openbsd.org/cgi-bin/man.cgi?query=ssh_config) на официјалном сајту.

# Решавање проблема

## Connection Refused проблем

#### Is SSH running and listening?

```
$ ss -tnlp

```

If the above command do not show SSH port is open, SSH is NOT running. Check `/var/log/messages` for errors etc.

### Да ли firewall блокира безу?

Потребно је освежити iptables правила да би се уверили да се не мешају у везу:

```
 /etc/rc.d/iptables stop

```

или:

```
 iptables -P INPUT ACCEPT
 iptables -P OUTPUT ACCEPT
 iptables -F INPUT
 iptables -F OUTPUT

```

### Да ли је SSH додат у hosts.allow?

Два пута треба проверити да ли је [this section](#.D0.94.D0.BE.D0.B7.D0.B2.D0.BE.D1.99.D0.B0.D0.B2.D0.B0.D1.9A.D0.B5_.D0.BF.D1.80.D0.B8.D1.81.D1.82.D1.83.D0.BF.D0.B0_.D0.B4.D1.80.D1.83.D0.B3.D0.B8.D0.BC_.D0.BA.D0.BE.D1.80.D0.B8.D1.81.D0.BD.D0.B8.D1.86.D0.B8.D0.BC.D0.B0) исправно.

### Да ли саобраћај стиже до рачуанра?

Треба започети праћење саобраћаја на рачунару који има проблеме командом:

```
 tcpdump -lnn -i any port ssh and tcp-syn

```

Ово ће приказати неке основне информације, онда треба чекати за одговарајући саобраћај да се деси пре приказивања. Пробајте сад везу. Ако нема излаза приликом покушаја повезивања, онда нешто ван рачунара блокира саобраћај (нпр, хардверски firewall, NAT рутер итд.)

# Такође погледајте

*   [Using SSH Keys (Српски)](/index.php/Using_SSH_Keys_(%D0%A1%D1%80%D0%BF%D1%81%D0%BA%D0%B8) "Using SSH Keys (Српски)")

# Линкови и препоруке

*   [A Cure for the Common SSH Login Attack](http://www.soloport.com/iptables.html)
*   [Using your browser as SSH client](http://webssh.cz.cc)
*   [Defending against brute force ssh attacks](http://www.la-samhna.de/library/brutessh.html)