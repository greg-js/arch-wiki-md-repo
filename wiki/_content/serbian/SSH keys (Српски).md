## Contents

*   [1 Шта су SSH кључеви?](#.D0.A8.D1.82.D0.B0_.D1.81.D1.83_SSH_.D0.BA.D1.99.D1.83.D1.87.D0.B5.D0.B2.D0.B8.3F)
    *   [1.1 Генерисање SSH кључева](#.D0.93.D0.B5.D0.BD.D0.B5.D1.80.D0.B8.D1.81.D0.B0.D1.9A.D0.B5_SSH_.D0.BA.D1.99.D1.83.D1.87.D0.B5.D0.B2.D0.B0)
    *   [1.2 Копирање кључева на удаљени сервер](#.D0.9A.D0.BE.D0.BF.D0.B8.D1.80.D0.B0.D1.9A.D0.B5_.D0.BA.D1.99.D1.83.D1.87.D0.B5.D0.B2.D0.B0_.D0.BD.D0.B0_.D1.83.D0.B4.D0.B0.D1.99.D0.B5.D0.BD.D0.B8_.D1.81.D0.B5.D1.80.D0.B2.D0.B5.D1.80)
*   [2 Памћење лозинки кључева](#.D0.9F.D0.B0.D0.BC.D1.9B.D0.B5.D1.9A.D0.B5_.D0.BB.D0.BE.D0.B7.D0.B8.D0.BD.D0.BA.D0.B8_.D0.BA.D1.99.D1.83.D1.87.D0.B5.D0.B2.D0.B0)
    *   [2.1 ssh-agent](#ssh-agent)
        *   [2.1.1 Коришћење GnuPG агента](#.D0.9A.D0.BE.D1.80.D0.B8.D1.88.D1.9B.D0.B5.D1.9A.D0.B5_GnuPG_.D0.B0.D0.B3.D0.B5.D0.BD.D1.82.D0.B0)
        *   [2.1.2 Коришћење keychain програма](#.D0.9A.D0.BE.D1.80.D0.B8.D1.88.D1.9B.D0.B5.D1.9A.D0.B5_keychain_.D0.BF.D1.80.D0.BE.D0.B3.D1.80.D0.B0.D0.BC.D0.B0)
        *   [2.1.3 Коришћење ssh-agent и x11-ssh-askpass](#.D0.9A.D0.BE.D1.80.D0.B8.D1.88.D1.9B.D0.B5.D1.9A.D0.B5_ssh-agent_.D0.B8_x11-ssh-askpass)
    *   [2.2 GNOME Keyring](#GNOME_Keyring)
*   [3 Решавање проблема](#.D0.A0.D0.B5.D1.88.D0.B0.D0.B2.D0.B0.D1.9A.D0.B5_.D0.BF.D1.80.D0.BE.D0.B1.D0.BB.D0.B5.D0.BC.D0.B0)
*   [4 Корисни линкови / Информације](#.D0.9A.D0.BE.D1.80.D0.B8.D1.81.D0.BD.D0.B8_.D0.BB.D0.B8.D0.BD.D0.BA.D0.BE.D0.B2.D0.B8_.2F_.D0.98.D0.BD.D1.84.D0.BE.D1.80.D0.BC.D0.B0.D1.86.D0.B8.D1.98.D0.B5)

## Шта су SSH кључеви?

Коришћењем SSH кључева (прецизније јавних и приватних), лако се може повезати на сервер, или на више сервера, без потребе да се уноси шифра за сваки сервер.

### Генерисање SSH кључева

Ако OpenSSH није инсталиран, потребно га је инсталирати.

```
# pacman -S openssh

```

Кључеви се могу генерисати покретањем the ssh-keygen команде као регуларни корисник:

```
$ ssh-keygen -b 1024 -t dsa
Generating public/private dsa key pair.
Enter file in which to save the key (/home/mith/.ssh/id_dsa):
Enter passphrase (empty for no passphrase):
Enter same passphrase again:
Your identification has been saved in /home/mith/.ssh/id_dsa.
Your public key has been saved in /home/mith/.ssh/id_dsa.pub.
The key fingerprint is:
x6:68:xx:93:98:8x:87:95:7x:2x:4x:x9:81:xx:56:94 mith@middleearth

```

То ће питати за локацију (коју треба оставити као што јесте), али лозинка је важна! Познато је који су критеријуми за добру лозинку.

Шта смо сад урадили? Генерисали смо 1024 бита дугачак (`-b 1024`) public/private dsa (`-t dsa`) пар кључева коришћењем `ssh-keygen` команде.

За прављење RSA парова кључева уместо DSA потребно је користити `-t rsa` (не треба наводити дужину кључа "-b" јер је подразумевана дужина за RSA 2048 и то је сасвим довољно).

**Note:** DSA кључ мора да буде тачно 1024 бита дугачак. RSA кључ може да варира између 768 и 4096 бита.

### Копирање кључева на удаљени сервер

Пошто су кључеви генерисани морају се копирати на удаљени сервер. За OpenSSH, јавни кључ се мора налазити у `~/.ssh/authorized_keys`.

```
$ scp ~/.ssh/id_dsa.pub mith@metawire.org:

```

Ово копира јавни кључ (`id_dsa.pub`) на удаљени сервер преко `scp` (обратите пажњу на `:` на крају адресе сервера). Фајл ће се ископирати у home директоријум, али може се навести и нека друга адреса ако је то потребно.

Следеће, на удаљеном серверу, неопходно је креирати `~/.ssh` директоријум и додати фајл са кључевима `authorized_keys` :

```
$ ssh mith@metawire.org
mith@metawire.org's password:
$ mkdir ~/.ssh
$ cat ~/id_dsa.pub >> ~/.ssh/authorized_keys
$ rm ~/id_dsa.pub
$ chmod 600 ~/.ssh/authorized_keys

```

Последње две команде уклањају јавни кључ са сервера (који више није потребан), и подешава исправне дозволе на authorized_keys фајлу.

Ако се дисконектујемо са сервера, и покушамо да се поново повежемо, бићемо упитани за лозинку кључа:

```
$ ssh mith@metawire.org
Enter passphrase for key '/home/mith/.ssh/id_dsa':

```

Ако не можете да се пријавите са кључем, два пута проверите дозволе на `authorized_keys` фајлу.

Такође проверите дозволе на `~/.ssh` директоријуму, који би требало да има дозволе писања искључене за групе и друге. Следећа команда искљулује дозволе за групе и друге за `~/.ssh` директоријум:

```
$ chmod go-w ~/.ssh

```

## Памћење лозинки кључева

Сада се можемо пријавити на сервер коришћењем кључа уместо шифре, али како је лакше, јер је и даље потребно унети лозинку кључа? Одговор је коришћење SSH агента, програм који памти лозинке за кључеве! Постоји више различитих алата који су доступни, па је потребно пронаћи онај који вама највише одговара..

### ssh-agent

ssh-agent је основни агент који долази уз OpenSSH.

```
$ ssh-agent
SSH_AUTH_SOCK=/tmp/ssh-vEGjCM2147/agent.2147; export SSH_AUTH_SOCK;
SSH_AGENT_PID=2148; export SSH_AGENT_PID;
echo Agent pid 2148;

```

Када се покрене `ssh-agent`, појавиће се променљиве које могу да се користе. Да би искористили те променљиве, потребно је покренути команду кроз `eval` команду.

```
$ eval `ssh-agent`
Agent pid 2157

```

Ово се може додати у `/etc/profile` да би се покретало сваки пут кад се отвори сесија:

```
# echo 'eval `ssh-agent`' >> /etc/profile

```

Обратите пажњу на исправне наводнике!

Сад кад је `ssh-agent` покренут, морамо да му кажемо да имамо приватне кључеве и где се налазе.

```
$ ssh-add ~/.ssh/id_dsa
Enter passphrase for /home/user/.ssh/id_dsa:
Identity added: /home/user/.ssh/id_dsa (/home/user/.ssh/id_dsa)

```

Упитани смо за лозинку, унели смо је, и то је то. Сад се можемо пријавити на удаљени сервер без потребе да уносимо шифру.

Једина лоша страна `ssh-agent` је потреба за креирањем нове конзоле (shell), то значи да морамо да покренемо `ssh-add` сваки пут за сваку конзолу. Постоји радно окружење за то тј. скрипта која се зове [keychain](http://www.gentoo.org/proj/en/keychain/index.xml) која ће бити покривена у следећем одељку.

#### Коришћење GnuPG агента

[GnuPG](/index.php/GnuPG "GnuPG") агент, се дистрибуира са [gnupg2](https://www.archlinux.org/packages/?name=gnupg2) пакетом, има OpenSSH емулацију агента. Ако користите GPG можете узети у обзир овог агента да брине о свим вашим кључевима. У супротном можда желите PIN дијалог који пружа управљање лозинкама, који се разликује од ланца кључева.

Да би почели са коришћењем GPG агента за SSH кључеве потребно је прво покренути gpg-agent са `--enable-ssh-support` опцијом. Пример (не заборавите да учините фајл извршивим):

 `/etc/profile.d/gpg-agent.sh` 
```
#!/bin/sh

# Start the GnuPG agent and enable OpenSSH agent emulation
gnupginf="${HOME}/.gnupg/gpg-agent.info"

if pgrep -u "${USER}" gpg-agent >/dev/null 2>&1; then
    eval `cat $gnupginf`
    eval `cut -d= -f1 $gnupginf | xargs echo export`
else
    eval `gpg-agent --enable-ssh-support --daemon`
fi

```

Кад је gpg-agent покренут може се користити ssh-add за одобравање кључева, као што би радили са обичним ssh-agent. Листа одобрених кључева се чува у `~/.gnupg/sshcontrol` фајлу. Једном кад је кључ одобрен добићете дијалог PIN уноса сваки пут кад је лозинка потребна. Кеширање лозинки се контролише у `~/.gnupg/gpg-agent.conf` фајлу. Следећи пример показује како gpg-agent кешира кључеве на 3 сата:

```
 # Cache settings
 default-cache-ttl 10800
 default-cache-ttl-ssh 10800

```

Друга корисна подешавања овог фајла укључују програм за унос PIN-а (GTK, QT или ncurses верзија), итд...:

```
 # Environment file
 write-env-file /home/username/.gnupg/gpg-agent.info

 # Keyboard control
 #no-grab

 # PIN entry program
 #pinentry-program /usr/bin/pinentry-curses
 #pinentry-program /usr/bin/pinentry-qt4
 pinentry-program /usr/bin/pinentry-gtk-2

```

#### Коришћење keychain програма

[Keychain](http://www.funtoo.org/en/security/keychain/intro/) управља једним или више дефинисаних приватних кључева. Кад се покрене тражиће лозинку за приватне кључеве и сачуваће их. На тај начин су приватни кључеви заштићени лозинком.

Keychain се инсталира из репозиторијума extra:

```
# pacman -S keychain

```

Потребно је креирати следећи фаји и учинити га извршним:

 `/etc/profile.d/keychain.sh` 
```
eval `keychain --eval --nogui -Q -q id_rsa`

```

или

 `/etc/profile.d/keychain.sh` 
```
/usr/bin/keychain -Q -q --nogui ~/.ssh/id_dsa
[[ -f $HOME/.keychain/$HOSTNAME-sh ]] && source $HOME/.keychain/$HOSTNAME-sh

```

или

Додати

```
eval `keychain --eval --agents ssh id_dsa`

```

у `.bashrc` или `.bash_profile`.

**Tip:** Ако желите већу сигурност треба заменити -Q са --clear али ће бити мање погодно.

Ако је потребно, замените `~/.ssh/id_dsa` са `~/.ssh/id_rsa`. За оне који не користе non-Bash компатибилну љуску, погледати `keychain --help` или `man keychain` за детаље о другим љускама.

Затворите љуску и отворите је опет. Keychain би требало да се подигне и ако је то први пут да се поркеће тражиће лозинку за спецификовани приватни кључ.

#### Коришћење ssh-agent и x11-ssh-askpass

Потребно је да се ssh-agent покрене сваки пут кад се покрене и нови Xsession. ssh-agent ће се затворити кад се X сесија заврши.

Инсталирајте различите x11-ssh-askpass који ће тражити лозинку сваки пут кад се покрене нови Xsession. Или користите оригинални x11-ssh-askpass из [AUR](/index.php/AUR "AUR") или ksshaskpass (користи kdelibs):

```
# pacman -S ksshaskpass

```

или openssh-askpass (користи qt):

```
# pacman -S openssh-askpass

```

После инсталирања ових програма, затварање Xsession и при поновном пријављивању ћете бити упитани за лозинку.

### GNOME Keyring

Ако користите [GNOME](/index.php/GNOME "GNOME") десктоп, [Gnome Keyring](/index.php/Gnome_Keyring "Gnome Keyring") алат се може користити као SSH агент. Посетите [Gnome Keyring](/index.php/Gnome_Keyring "Gnome Keyring") чланак.

## Решавање проблема

Ако SSH сервер игнорише кључеве, постарајте се да имате правилно подешене дозволе на свим битним фајловима.

За локалну машину:

```
$ chmod 700 ~/
$ chmod 700 ~/.ssh
$ chmod 600 ~/.ssh/id_rsa

```

За удаљену машину:

```
$ chmod 700 ~/
$ chmod 700 ~/.ssh
$ chmod 600 ~/.ssh/authorized_keys

```

У супротном, покрените sshd у debug режиму и посматрајте излаз команде док се повезујете:

```
# /usr/sbin/sshd -d

```

## Корисни линкови / Информације

*   [HOWTO: set up ssh keys](http://www.arches.uga.edu/~pkeck/ssh/)
*   [OpenSSH key management, Part 1](http://www-106.ibm.com/developerworks/linux/library/l-keyc.html)
*   [OpenSSH key management, Part 2](http://www-106.ibm.com/developerworks/linux/library/l-keyc2/)
*   [OpenSSH key management, Part 3](http://www-106.ibm.com/developerworks/library/l-keyc3/)
*   [Getting started with SSH](http://kimmo.suominen.com/docs/ssh/)
*   Manual Pages: [ssh-keygen(1)](http://www.openbsd.org/cgi-bin/man.cgi?query=ssh-keygen&apropos=0&sektion=0&manpath=OpenBSD+Current&arch=i386&format=html)