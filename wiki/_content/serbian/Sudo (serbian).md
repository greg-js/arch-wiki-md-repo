Sudo (su "do") дозвољава систем администратору да повери ауторитет одређеним корисницима (или групи корисника) да имају способност да покрећу неке (или све) команде као root или неки други корисник пружајући ревизорски траг за команде и њихове аргументе. [[1]](http://www.gratisoft.us/sudo/)

## Contents

*   [1 Образложење](#.D0.9E.D0.B1.D1.80.D0.B0.D0.B7.D0.BB.D0.BE.D0.B6.D0.B5.D1.9A.D0.B5)
*   [2 Инсталација](#.D0.98.D0.BD.D1.81.D1.82.D0.B0.D0.BB.D0.B0.D1.86.D0.B8.D1.98.D0.B0)
*   [3 Коришћење](#.D0.9A.D0.BE.D1.80.D0.B8.D1.88.D1.9B.D0.B5.D1.9A.D0.B5)
*   [4 Конфигурација](#.D0.9A.D0.BE.D0.BD.D1.84.D0.B8.D0.B3.D1.83.D1.80.D0.B0.D1.86.D0.B8.D1.98.D0.B0)
    *   [4.1 sudoers подразумеване дозволе над фајловима](#sudoers_.D0.BF.D0.BE.D0.B4.D1.80.D0.B0.D0.B7.D1.83.D0.BC.D0.B5.D0.B2.D0.B0.D0.BD.D0.B5_.D0.B4.D0.BE.D0.B7.D0.B2.D0.BE.D0.BB.D0.B5_.D0.BD.D0.B0.D0.B4_.D1.84.D0.B0.D1.98.D0.BB.D0.BE.D0.B2.D0.B8.D0.BC.D0.B0)
    *   [4.2 Коришћење visudo](#.D0.9A.D0.BE.D1.80.D0.B8.D1.88.D1.9B.D0.B5.D1.9A.D0.B5_visudo)
    *   [4.3 Тајмаут кеш лозинке](#.D0.A2.D0.B0.D1.98.D0.BC.D0.B0.D1.83.D1.82_.D0.BA.D0.B5.D1.88_.D0.BB.D0.BE.D0.B7.D0.B8.D0.BD.D0.BA.D0.B5)
*   [5 Савети и трикови](#.D0.A1.D0.B0.D0.B2.D0.B5.D1.82.D0.B8_.D0.B8_.D1.82.D1.80.D0.B8.D0.BA.D0.BE.D0.B2.D0.B8)
    *   [5.1 Омогућити завршетак табом у bash-u](#.D0.9E.D0.BC.D0.BE.D0.B3.D1.83.D1.9B.D0.B8.D1.82.D0.B8_.D0.B7.D0.B0.D0.B2.D1.80.D1.88.D0.B5.D1.82.D0.B0.D0.BA_.D1.82.D0.B0.D0.B1.D0.BE.D0.BC_.D1.83_bash-u)
    *   [5.2 Онемогући per-terminal sudo](#.D0.9E.D0.BD.D0.B5.D0.BC.D0.BE.D0.B3.D1.83.D1.9B.D0.B8_per-terminal_sudo)
    *   [5.3 Променљиве околине (Застарело?)](#.D0.9F.D1.80.D0.BE.D0.BC.D0.B5.D0.BD.D1.99.D0.B8.D0.B2.D0.B5_.D0.BE.D0.BA.D0.BE.D0.BB.D0.B8.D0.BD.D0.B5_.28.D0.97.D0.B0.D1.81.D1.82.D0.B0.D1.80.D0.B5.D0.BB.D0.BE.3F.29)
    *   [5.4 Додајте /sbin и /usr/sbin у root путању](#.D0.94.D0.BE.D0.B4.D0.B0.D1.98.D1.82.D0.B5_.2Fsbin_.D0.B8_.2Fusr.2Fsbin_.D1.83_root_.D0.BF.D1.83.D1.82.D0.B0.D1.9A.D1.83)
    *   [5.5 Пренос псеудонима](#.D0.9F.D1.80.D0.B5.D0.BD.D0.BE.D1.81_.D0.BF.D1.81.D0.B5.D1.83.D0.B4.D0.BE.D0.BD.D0.B8.D0.BC.D0.B0)
    *   [5.6 Увреде](#.D0.A3.D0.B2.D1.80.D0.B5.D0.B4.D0.B5)
    *   [5.7 Root шифра](#Root_.D1.88.D0.B8.D1.84.D1.80.D0.B0)
    *   [5.8 Онемогући root логин](#.D0.9E.D0.BD.D0.B5.D0.BC.D0.BE.D0.B3.D1.83.D1.9B.D0.B8_root_.D0.BB.D0.BE.D0.B3.D0.B8.D0.BD)
        *   [5.8.1 kdesu](#kdesu)
*   [6 Sudo отклањање грешака](#Sudo_.D0.BE.D1.82.D0.BA.D0.BB.D0.B0.D1.9A.D0.B0.D1.9A.D0.B5_.D0.B3.D1.80.D0.B5.D1.88.D0.B0.D0.BA.D0.B0)
    *   [6.1 SSH TTY проблеми](#SSH_TTY_.D0.BF.D1.80.D0.BE.D0.B1.D0.BB.D0.B5.D0.BC.D0.B8)
    *   [6.2 Приказивање корисничких привилегија](#.D0.9F.D1.80.D0.B8.D0.BA.D0.B0.D0.B7.D0.B8.D0.B2.D0.B0.D1.9A.D0.B5_.D0.BA.D0.BE.D1.80.D0.B8.D1.81.D0.BD.D0.B8.D1.87.D0.BA.D0.B8.D1.85_.D0.BF.D1.80.D0.B8.D0.B2.D0.B8.D0.BB.D0.B5.D0.B3.D0.B8.D1.98.D0.B0)
*   [7 Sudoers пример](#Sudoers_.D0.BF.D1.80.D0.B8.D0.BC.D0.B5.D1.80)

## Образложење

Sudo је безбедна алтернатива традиционалној [su](/index.php/Su "Su") команди. Много пута корисник користи su да добије root привилегије. Генерално, сматра се да није паметно логовати се као root -- суперкорисник -- на дужи временски период. Root корисник ужива комплетну и апсолутну контролу над целим системом, али са великим ризиком! Једоноставне грешке у куцању могу лако да учине систем неупотребљивим, и било која апликација која се покреће као root дели овај неспутани приступ.

Sudo даје 'привремену' привилегију за једну команду (било као root или други корисник); враћајући непривилеговано стање после извршавања, и враћање система у безбедно стање од нежељених последица. Додатно, sudo чува све команде и неуспеле покушаје приступа.

## Инсталација

Да би инсталирали sudo покрећемо команду:

```
# pacman -S sudo

```

Кориснику неће бити дозвољено да покреће sudo уколико није експлицитно дозвољено у /etc/sudoers фајлу. Погледај [#Конфигурација](#.D0.9A.D0.BE.D0.BD.D1.84.D0.B8.D0.B3.D1.83.D1.80.D0.B0.D1.86.D0.B8.D1.98.D0.B0) за упутства.

## Коришћење

Са инсталираним и конфигурисаним sudo, корисници могу да користе команде са префиксом `sudo` да покрећу ту команду са привилегијама суперкорисника (или других). На пример:

```
$ sudo pacman -Syu

```

Види [sudo manual](http://www.gratisoft.us/sudo/man/sudo.html) за више информација.

## Конфигурација

Конфигурациони фајл за sudo је `/etc/sudoers`. **Овај фајл се не треба директно едитовати!** Корисници морају да покрену команду `visudo` као root, која отвара привремену копију конфигурационог фајла у *$EDITOR* и проверава синтаксу привремене копије пре чувања праве.

### sudoers подразумеване дозволе над фајловима

Власник и група за sudoers фајл мора бити 0\. Дозволе за фајлове морају бити подешене на 0440.

```
 chown -c root:root /etc/sudoers
 chmod -c 0440 /etc/sudoers

```

### Коришћење visudo

Фајл sudoers се увек мора мењати visudo командом која закључава фајл и проверава граматичке грешке. Важно је да sudoers буде без синтаксних грешака пошто sudo неће радити са синтаксно погрешним sudoers фајлом.

Sudo пакет укључује бинарни `visudo` који је једини начин за мењање `/etc/sudoers` фајла.

```
visudo [-c] [-q] [-s] [-V] [-f sudoers]

```

Подразумевани едитор је *vi*. Ако је коршћење *vi* тешко, покрените ову команду прво:

```
# export EDITOR=nano

```

Или да visudo команда користи Ваш EDITOR, ромените EDITOR променљиву само за visudo команду са:

```
# EDITOR=nano visudo

```

Добар начин за мењање /etc/sudoers је коришћењем vim.

```
# EDITOR=vim visudo

```

Или промените за стално додавањем следећих линија у `/etc/sudoers` где је vim Ваш подразумевани едитор:

```
# Defaults specification
# Reset environment by default
Defaults      env_reset
# Set default EDITOR to vim, and do not allow visudo to use EDITOR/VISUAL.
Defaults      editor=/usr/bin/vim, !env_editor

```

Напомена је да команду `visudo` треба да покренете као root иако користите други едитор.

Кад се фајл сачува, `visudo` ће два пута проверити фајл због синтаксних грешака пре замењивања постојећег `/etc/sudoers` фајла. Ова сигурносна карактеристика постоји зато што ће sudo бити неупотребљив ако садржи грешке.

Да дозволите кориснику пуне root привилегије кад он/она извршава команду са "sudo", додајте следећу линију:

```
USER_NAME   ALL=(ALL) ALL

```

и/или да дозволите sudo кориснику приступ само са локалног рачунара:

```
USER_NAME   HOSTNAME=(ALL) ALL

```

и/или да дозволите члану [group](/index.php/Group "Group") wheel sudo приступ који не захтева шифру:

```
%wheel      ALL=(ALL) NOPASSWD: ALL

```

где је USER_NAME корисничко име корисника.

Детаљни пример `sudoers` може се наћи на [here](http://www.gratisoft.us/sudo/sample.sudoers). У супротном, види [sudoers manual](http://www.gratisoft.us/sudo/man/sudoers.html) за детаљније информације.

### Тајмаут кеш лозинке

Корисници можда желе да промене подразумевани тајмаут пре него што кеширана шифра истекне. То се постиже додавањем следећег у `/etc/sudoers` (`visudo`) на пример:

```
Defaults:USER_NAME timestamp_timeout=20

```

где шифра истиће за корисника USER_NAME ако се не користи више од 20 минута. Вредности између 0 and 1 су такође дозвољене.

**Tip:** Да омогућите да sudo увек тражи шифру, подесите тајмаут на нула.

## Савети и трикови

### Омогућити завршетак табом у bash-u

Таб, подразумевано, неће радити када корисник буде додат у sudoers фајл. На пример, обично john само мора да напише:

```
fire<TAB>

```

и shell ће завршити команду за њега као:

```
firefox

```

Ако је john додат у sudoers фајл и он укуца :

```
sudo fire<TAB>

```

shell неће ништа урадити.

Да омогућите завршавање табом са sudo, додајте следеће у Ваш `~/.bashrc`:

```
complete -cf sudo

```

Поред тога, можете инсталирати и омогућити bash-completion да добијете паметније завршавање табом за команде као sudo, погледај [bash#Auto-completion](/index.php/Bash#Auto-completion "Bash") за више информација.

### Онемогући per-terminal sudo

**Warning:** Ово ће дозволити свим процесима да користе Вашу sudo сесију

Ако Вам смета кад sudo захтева Вашу шифру сваки пут кад отворите нови терминал, онемогућите **tty_tickets**:

```
Defaults !tty_tickets

```

### Променљиве околине (Застарело?)

Ако имате много променљивих околине, или извозите Ваша прокси подешавања преко <tt>export http_proxy="..."</tt>, кад користите sudo ове променљиве неће пролазити на root налог уколико не покрећете sudo са `-E` опцијом.

```
$ sudo -E pacman -Syu

```

Због овога можете да додате псеудоним у `~/.bashrc`:

```
alias sudo="sudo -E"

```

Други начин поправљања овога било би додавање у `/etc/sudoers`:

```
Defaults !env_reset

```

Ако желите да само прослеђује <tt>*_proxy</tt> променљиве, додајте следеће:

```
Defaults env_keep += "ftp_proxy http_proxy https_proxy no_proxy"

```

### Додајте /sbin и /usr/sbin у root путању

Ако желите да поркећете административне команде (оне у /sbin или /usr/sbin) са sudo без корисшћења њихових пуних путања, додајте:

```
Defaults secure_path="/bin:/sbin:/usr/bin:/usr/sbin" 

```

у `/etc/sudoers`.

Ово Вам дозвољава да урадите:

```
$ sudo command

```

уместо:

```
$ sudo /sbin/command

```

или:

```
$ sudo /usr/sbin/command

```

### Пренос псеудонима

Ако користите много псеудонима, можда сте приметили да се не преносе на root налог када се користи sudo. Ипак, постоји лак начин да их натерате да раде. Једноставно додајте следеће у Ваш `~/.bashrc` или `/etc/bash.bashrc`:

```
alias sudo='sudo '

```

### Увреде

Корисник може да конфигурише sudo да приказује паметне увреде кад је нетачна шифра унета уместо подразумеване "wrong password" поруке. Нађите Defaults линију у `/etc/sudoers` и додајте "insults" после запете на већ постојеће опције. Коначни резултат би требало да изгледа овако:

```
#Defaults specification
Defaults insults

```

За тестирање, укуцајте `sudo -K` за крај тренутне сесије и дозволите да sudo пита за шифру поново.

### Root шифра

Корисници могу да конфигуришу sudo да пита за root шифру уместо корисникове шифре додавањем "rootpw" у Defaults линију у `/etc/sudoers`:

```
Defaults timestamp_timeout=0,rootpw

```

### Онемогући root логин

**Warning:** Arch Linux није фино наштимован да ради са онемогућеним root налогом. Корисници могу да наиђу на проблеме са овом методом.

Са инсталираним и конфигурисаним sudo, корисници можда желе да онемогуће root логин. Без root, нападачи морају прво да погоде корисничко име конфигурисано као sudoer као и корисникову ширфу.

**Warning:** Уверите се да је корисник правилно конфигурисан као sudoer *пре* онемогућавања root налога!

Налог се може закључати преко `passwd`:

```
# passwd -l root

```

Слична команда откључава root.

```
$ sudo passwd -u root

```

Други начин је едитовање `/etc/shadow` и замена root шифре са "!":

```
root:!:12345::::::

```

Да опет омогућите root логин:

```
$ sudo passwd root

```

#### kdesu

kdesu може се користити под KDE окружењем за покретање GUI апликација са root привилегијама. Могуће је да ће подразумевани kdesu пробати да користи su иако је root налог онемогућен. Срећом kdesu се може подесити да користи sudo уместо su. Направите/измените фајл `/usr/share/config/kdesurc`:

```
[super-user-command]
super-user-command=sudo

```

## Sudo отклањање грешака

### SSH TTY проблеми

SSH не додељује tty по подразумеваној вредности када се покреће удаљена команда. Без tty, sudo не може да онемогући ехо кад тражи шифру. Може се користити ssh "-tt" опција да натера да додели tty. (користи -tt два пута).

The Defaults опција дозвољава корисницима да покрећу sudo ако имају tty

```
# Disable "ssh hostname sudo <cmd>", because it will show the password in clear. You have to run "ssh -t hostname sudo <cmd>".
#
#Defaults    requiretty

```

### Приказивање корисничких привилегија

Можете сазнати које привилегије одређени корисник има коришћењем следеће команде:

```
 sudo -lU askapache

```

Или погледати своје са

```
 sudo -l

```

```
Matching Defaults entries for askapache on this host:
    loglinelen=0, logfile=/var/log/sudo.log, log_year, syslog=auth, mailto=sqpt.webmaster@gmail.com, mail_badpass, mail_no_user, mail_no_perms, env_reset, always_set_home, tty_tickets, lecture=always, pwfeedback, rootpw, set_home

User askapache may run the following commands on this host:
    (ALL) ALL, 
    (ALL) NOPASSWD: /usr/sbin/lsof, /bin/nice, /usr/sbin/ss, /usr/bin/su, /usr/bin/locate, /usr/bin/find, /usr/bin/rsync, /usr/bin/strace, 
    (ALL) /bin/nice, /bin/kill, /usr/bin/nice, /usr/bin/ionice, /usr/bin/top, /usr/bin/kill, /usr/bin/killall, /usr/bin/ps, /usr/bin/pkill, 
    (ALL) /usr/sbin/gparted, /usr/bin/pacman, /usr/bin/powerpill, 
    (ALL) /usr/local/bin/synergyc, /usr/local/bin/synergys, 
    (ALL) /usr/bin/vim, /usr/bin/nano, /usr/bin/cat
    (root) NOPASSWD: /usr/local/bin/synergyc

```

## Sudoers пример

This is especially helpful for those using terminal multiplexers like screen, tmux, or ratpoison, and those using sudo from scripts/cronjobs.

```

Cmnd_Alias WHEELER = /usr/sbin/lsof, /bin/nice, /bin/ps, /usr/bin/top, /usr/local/bin/nano, /usr/sbin/ss, /usr/bin/locate, /usr/bin/find, /usr/bin/rsync
Cmnd_Alias PROCESSES = /bin/nice, /bin/kill, /usr/bin/nice, /usr/bin/ionice, /usr/bin/top, /usr/bin/kill, /usr/bin/killall, /usr/bin/ps, /usr/bin/pkill
Cmnd_Alias EDITS = /usr/bin/vim, /usr/bin/nano, /usr/bin/cat, /usr/bin/vi
Cmnd_Alias ARCHLINUX = /usr/sbin/gparted, /usr/bin/pacman, /usr/bin/powerpill

root ALL = (ALL) ALL
askapache ALL = (ALL) ALL, NOPASSWD: WHEELER, NOPASSWD: PROCESSES, NOPASSWD: ARCHLINUX, NOPASSWD: EDITS

Defaults !requiretty, !tty_tickets, !umask
Defaults visiblepw, path_info, insults, lecture=always
Defaults loglinelen = 0, logfile =/var/log/sudo.log, log_year, log_host, syslog=auth
Defaults mailto=webmaster@askapache.com, mail_badpass, mail_no_user, mail_no_perms
Defaults passwd_tries = 8, passwd_timeout = 1
Defaults env_reset, always_set_home, set_home, set_logname
Defaults !env_editor, editor="/usr/bin/vim:/usr/bin/vi:/usr/bin/nano"
Defaults timestamp_timeout=360
Defaults passprompt="Sudo invoked by [%u] on [%H] - Cmd run as %U - Password for user %p:"

```