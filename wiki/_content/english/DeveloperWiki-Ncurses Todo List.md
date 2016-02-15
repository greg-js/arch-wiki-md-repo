## Contents

*   [1 Introduction](#Introduction)
*   [2 Ncurses Rebuild List](#Ncurses_Rebuild_List)
    *   [2.1 Stage 1](#Stage_1)
    *   [2.2 Stage 2](#Stage_2)
    *   [2.3 Stage 3](#Stage_3)
    *   [2.4 Stage 4](#Stage_4)

# Introduction

This article is part of the [DeveloperWiki](/index.php/DeveloperWiki "DeveloperWiki").

# Ncurses Rebuild List

This is a list of packages which link to the ncurses libraries (as of 2008-08) and a recommended build order

#### Stage 1

Packages required for bash to continue working. Note: this probably requires some bootstraping

```
ncurses
readline
bash

```

#### Stage 2

The rest of base and base-devel:

```
dialog
gettext
grub
less
nano
procinfo
procps
psmisc
texinfo
util-linux-ng
vi  _(Requires gettext)_

```

#### Stage 3

Rebuild rest of [core]:

```
gpm
heimdal
isdn4k-utils
links
netkit-telnet

```

#### Stage 4

Packages in [extra]:

```
aalib
abiword-plugins  _(Requires aspell, gnutls, smbclient, postgresql-libs, unixodbc, sqlite3, libgda)_
abook
achessclock  _(Source location unknown - remove on next update)_
afterstep  _(Requires gnutls, libxml2)_
alpine
alsa-utils
aspell
bc
blassic
bs
bzflag
cdargs
cdcd
centerim
clisp
cmake
cmatrix
cmus  _(Requires lame)_
cscope
darcs
ddd
dopewars
duhdraw
elinks
emacs  _(Requires gnutls)_
enigma
erlang
ethstatus
ettercap
ettercap-gtk  _(Requires ettercap)_
evms
fortunelock
freeciv  _(Requires gnutls)_
fvwm
fvwm-devel
gdb
gftp
ghc  _(Requires bootstraping)_
gnuchess
giftcurs
gnome-terminal
gnugo
gnuplot  _(Requires gnutls)_
gnutls
gphoto2
gstreamer-good-plugins  _(Requires aalib, gnutls, libxml2)_
guile
gutenprint  _(Requires gnutls)_
gvim  _(Requires vim, gnutls)_
hexcurse
hexedit
htop
hugs98 
iptraf
irssi
ispell
jack-audio-connection-kit
joe
kismet  _(Requires gnutls)_
lame
lexter
lftp
libcaca
libcdio
libgda  _(Requires sqlite3, postgresql-libs, unixodbc, libxml2)_
libnjb
libqalculate  _(Requires libxml2)_
librep
libxml2
lua
lynx
maxima  _(Requires clisp)_
mc
minicom
moc _(Requores jack-audio-connection-kit, lame)_
mplayer  _(Requires aalib, gnutls, jack-audio-connection-kit, lame, smbclient)_
mp3blaster
moon-buggy
mtr  _(Requires gnutls)_
multitail
mysql-clients
naim
ncftp
ncmpc
ne
nethack
netkit-ftp
netris
nph  _(Requires termcap-compat)_
nppangband
ntp
ocaml
octave
openupsmart
pal
parted
pente
php  _(Requires sqlite3)_
pilot-link
pinentry
proftpd
postgresql-libs
python
r
ratpoison
ruby  _(Requires termcap-compat)_
screen
socat
sqlite2
sqlite3
smbclient
swi-prolog
tcsh
termcap-compat
terminal  _(Requires vte)_
timidity++  _(Requires jack-audio-connection-kit, gnutls)_
tin
uml_utilities
unixodbc
vice
vim  _(Requires ruby)_
vte  _(Requires gnutls, libxml2)_
w3m
wvstreams
xaos  _(Requires aalib)_
xawtv _(Requires aalib)_
xemacs
xfsdump
xine-ui  _(Requires lame)_
xorg-server
xterm
yabasic
zile
zsh
zsnes

```