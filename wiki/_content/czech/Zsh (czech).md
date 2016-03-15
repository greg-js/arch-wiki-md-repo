[Zsh](http://www.zsh.org) je mocný shell se kterým je možno pracovat jako s interaktivním shellem i jako se interpretrem skriptovacího jazyka. Je sice kompaktibilní se shellem [Bash](/index.php/Bash "Bash"), nabízí však další možnosti jako:

*   Rychlost
*   Vylepšené doplňování klávesou TAB
*   Vzlepšený globbing
*   Vylepšená práce s poli
*   Plně přizpůsobitelný

Zsh Faq nabízí [více důvodů](http://zsh.sourceforge.net/FAQ/zshfaq01.html#l4) proč používat Zsh.

## Contents

*   [1 Instrukce pro instalaci](#Instrukce_pro_instalaci)
    *   [1.1 Instalace](#Instalace)
    *   [1.2 Nastavení Zsh jako implicitní shell](#Nastaven.C3.AD_Zsh_jako_implicitn.C3.AD_shell)
*   [2 Konfigurace](#Konfigurace)
    *   [2.1 Ukázkový .zshrc](#Uk.C3.A1zkov.C3.BD_.zshrc)
    *   [2.2 /etc/zprofile](#.2Fetc.2Fzprofile)
    *   [2.3 Doplňování příkazů](#Dopl.C5.88ov.C3.A1n.C3.AD_p.C5.99.C3.ADkaz.C5.AF)
    *   [2.4 Nastavení kláves](#Nastaven.C3.AD_kl.C3.A1ves)
    *   [2.5 Výzvy příkazového řádku](#V.C3.BDzvy_p.C5.99.C3.ADkazov.C3.A9ho_.C5.99.C3.A1dku)
    *   [2.6 Rozšířený .zshrc](#Roz.C5.A1.C3.AD.C5.99en.C3.BD_.zshrc)
    *   [2.7 Ukázkové .zshrc soubory](#Uk.C3.A1zkov.C3.A9_.zshrc_soubory)
*   [3 Povolení Unicode (zastaralé)](#Povolen.C3.AD_Unicode_.28zastaral.C3.A9.29)
*   [4 Odinstalace](#Odinstalace)
*   [5 Zdroje](#Zdroje)

## Instrukce pro instalaci

Než začneš, zjisti který shell právě používáš:

```
$ echo $SHELL

```

### Instalace

Pro instalaci Zsh balíku, spusť:

```
# pacman -S zsh

```

Před nastavením Zsh jako impliticní shell se ujisti jestli byl nainstalován korektně jeho spuštěním např. v okně xtermu nebo tty:

```
$ zsh

```

Pokud instalace proběhla hladne, měl by jsi teď vidět neznámý prompt, zatím prostě napiš:

```
$ exit

```

### Nastavení Zsh jako implicitní shell

Pro změnu uživatelského implicitního shellu bez rootovských oprávnění se používá příkaz chsh. Příkaz chsh lze použít pro změnu implicitního shellu bez rootovských oprvávnění jen pokud je shell uveden v souboru `/etc/shells`. Pokud jsi Zsh instaloval použitím pacmana, Zsh již by měl mít odpovídající záznam v `/etc/shells`.

Pro pokračování potřebuješ znát plnou cestu k Zsh, proto spusť:

```
$ which zsh

```

Změn implicitní shelll pro práve přihlášeného uživatele:

```
$ chsh -s /bin/zsh

```

Alternativní cesta ke změně shellu vede přes příkaz usermod. Nevýhodou této metody je potřeba mít k pc rootovský přístup. Více uživatelských účtů může být změněno rychle jako root, použitím příkazu usermod nebo chsh.

Změna implicitního shellu pro více uživatelů použitím příkazu usermod:

```
# usermod -s /bin/zsh uzivatel

```

Změna implicitního shellu pro více uživatelů použitím příkazu chsh:

```
# chsh -s /bin/zsh username

```

**Note:** Je třeba se odhlásit a přihlaásit zpět pokud chceš začít používat Zsh hned.

Po opětovném přihlášení si můžeš ověřit, zda je Zsh opravdu tvým implicitním shellem:

```
$ echo $SHELL

```

Pokud nemáš rootovská práva a Zsh není zapsán v souboru `/etc/shells` ale i přesto by jsi rád používal Zsh jako implicitní shell, přejdi [na tento záznam](http://zsh.sunsite.dk/FAQ/zshfaq01.html#l8) ve Zsh FAQ.

## Konfigurace

Prestože je Zsh použitelný 'out of the box', skoro určitě nebude nastavený tak jak by sis přál. Kvůli velkému množství možných nastavení dostupných v Zsh se může vytváření konfiguračního souboru stát časově velice náročnou záležitostí.

Dále je přiložený ukázkový konfigurační soubor, poskytuje několik základních nastavení. Pokud chceš použít tento konfigurační soubor, ulož jej jako `.zshrc` ve svém domovském adresáři. Poté jej již můžeš upravovat bez potřeby odhlašování se tímto příkazem:

```
$ source ~/.zshrc

```

### Ukázkový .zshrc

Tady je základní `.zshrc`, který by měl být pro začátek dostačující:

 `~/.zshrc` 
```
autoload -U compinit promptinit
compinit
promptinit

# Tohle nastaví defaultní prompt na walters theme
prompt walters
```

### /etc/zprofile

Stejně jako `/etc/profile`, který používá Bash, tento soubor je pro globální nastavení Zsh + je to dobré místo pro pouštění skriptů z `/etc/profile.d/` a nastavování proměnných prostředí jako např. $PATH. Při nastavování $PATH atd. v `.zshrc` a používání login manažeru jako např. kdm, můžeš zjistit že tyto nastavení nebyly přebrány okením manažerem, zatímco používají `/etc/zprofile`.

Obecně řečeno, můžes skopírovat `/etc/profile` do `/etc/zprofile`.

Ukázková konfigurace:

 `/etc/zprofile` 
```
###############
# Zsh profil #
###############

export PATH="/bin:/usr/bin:/sbin:/usr/sbin:/usr/X11R6/bin:/opt/bin"

export MANPATH="/usr/man:/usr/X11R6/man"
export LESSCHARSET="latin1"
export LESS="-R"

# nahraje profily z adresáře /etc/profile.d
#  (pokud chceš některý z profilů zakázaz, prostě z příslušného souboru odstraň právo pro spouštění)
if [ `ls -A1 /etc/profile.d/
```

**Note:** PKGBUILD Zshellu definuje že profil se nachází v */etc/profile*, takže odkazování se na */etc/zprofile* může být poněkud zavádějící...

### Doplňování příkazů

Asi nejpůsobivější funkcí Zshellu jsou jeho rozšířené schopnosti doplňování. Přinejmenším budeš chtít povolit automatické doplňování ve tvém `.zshrc`. Pro povolení automatického doplňování, přidej následující:

 `~/.zshrc` 
```
autoload -U compinit
compinit
```

Pro automatické doplňování obohacené o možnost výběru kurzorovými šipkami přidej toto:

 `~/.zshrc`  `zstyle ':completion:*' menu select` 

### Nastavení kláves

Zsh nečte obsah souboru `/etc/inputrc`, který říká co který příkaz zaslaný emulátorem terminálu znamená. Pro povolení standardních kláves, přidej něco jako toto:

 `~/.zshrc` 
```
# Nastavení kláves
bindkey "\e[1~" beginning-of-line
bindkey "\e[4~" end-of-line
bindkey "\e[5~" beginning-of-history
bindkey "\e[6~" end-of-history
bindkey "\e[3~" delete-char
bindkey "\e[2~" quoted-insert
bindkey "\e[5C" forward-word
bindkey "\eOc" emacs-forward-word
bindkey "\e[5D" backward-word
bindkey "\eOd" emacs-backward-word
bindkey "\e\e[C" forward-word
bindkey "\e\e[D" backward-word
bindkey "^H" backward-delete-word
# pro rxvt
bindkey "\e[8~" end-of-line
bindkey "\e[7~" beginning-of-line
# pro ne RH/Debian xterm, nemůže ublížit RH/DEbian xtermu
bindkey "\eOH" beginning-of-line
bindkey "\eOF" end-of-line
# pro freebsd konzoli
bindkey "\e[H" beginning-of-line
bindkey "\e[F" end-of-line
# doplňování uprostřed řádku
bindkey '^i' expand-or-complete-prefix
```

### Výzvy příkazového řádku

Tady je rychlý a jednoduchý způsob jak nastavit barevnou výzvu příkazového řádku. Ujisti se že výzva je nastavena na autoload ve tvém `.zshrc`. Toho může být dosáhnuto přídáním:

 `~/.zshrc` 
```
autoload -U promptinit
promptinit
```

Nyní si můžeš vypsat dostupné výzvy příkazového řádku:

```
$ prompt -l

```

To try one of the commands that is listed, use the command prompt followed by the name of the prompt you like. For example, to use the "walters" prompt, you would enter:

```
$ prompt walters

```

### Rozšířený .zshrc

Tohle je ukázka rozšířeného `.zshrc`:

 `~/.zshrc` 
```
###########################################################        
# Vlastnosti Zsh

export HISTFILE=~/.zsh_history
export HISTSIZE=50000
export SAVEHIST=50000
eval `dircolors -b`

autoload -U compinit compinit
setopt autopushd pushdminus pushdsilent pushdtohome
setopt autocd
setopt cdablevars
setopt ignoreeof
setopt interactivecomments
setopt nobanghist
setopt noclobber
setopt HIST_REDUCE_BLANKS
setopt HIST_IGNORE_SPACE
setopt SH_WORD_SPLIT
setopt nohup

# PS1 a PS2
export PS1="$(print '%{\e[1;34m%}%n%{\e[0m%}'):$(print '%{\e[0;34m%}%~%{\e[0m%}')$ "
export PS2="$(print '%{\e[0;34m%}>%{\e[0m%}')"

# Proměnné použité později v Zsh
export EDITOR="gvim -geom 82x35"
export BROWSER=links
export XTERM="aterm +sb -geometry 80x29 -fg black -bg lightgoldenrodyellow -fn -xos4-terminus-medium-*-normal-*-14-*-*-*-*-*-iso8859-15"

##################################################################
# Pár věcí k usnadnění práce

# povol approximate
zstyle ':completion:*' completer _complete _match _approximate
zstyle ':completion:*:match:*' original only
zstyle ':completion:*:approximate:*' max-errors 1 numeric

# doplňování pomocí klávesy TAB pro PID :D
zstyle ':completion:*:*:kill:*' menu yes select
zstyle ':completion:*:kill:*' force-list always

# příkaz cd nevybere rodičovský adresář
zstyle ':completion:*:cd:*' ignore-parents parent pwd

##################################################################
# Nastavení kláves
# http://mundy.yazzy.org/unix/zsh.php
# http://www.zsh.org/mla/users/2000/msg00727.html

typeset -g -A key
bindkey '^?' backward-delete-char
bindkey '^[[1~' beginning-of-line
bindkey '^[[5~' up-line-or-history
bindkey '^[[3~' delete-char
bindkey '^[[4~' end-of-line
bindkey '^[[6~' down-line-or-history
bindkey '^[[A' up-line-or-search
bindkey '^[[D' backward-char
bindkey '^[[B' down-line-or-search
bindkey '^[[C' forward-char 

##################################################################
# Aliasy

# Nastavíme automatické rozpoznání koncovek souborů
alias -s html=$BROWSER
alias -s org=$BROWSER
alias -s php=$BROWSER
alias -s com=$BROWSER
alias -s net=$BROWSER
alias -s png=feh
alias -s jpg=feh
alias -s gif=feg
alias -s sxw=soffice
alias -s doc=soffice
alias -s gz=tar -xzvf
alias -s bz2=tar -xjvf
alias -s java=$EDITOR
alias -s txt=$EDITOR
alias -s PKGBUILD=$EDITOR

# Normální aliasy
alias ls='ls --color=auto -F'
alias lsd='ls -ld *(-/DN)'
alias lsa='ls -ld .*'
alias f='find |grep'
alias c="clear"
alias dir='ls -1'
alias gvim='gvim -geom 82x35'
alias ..='cd ..'
alias nicotine='/home/paul/downloads/nicotine-1.0.8rc1/nicotine'
alias ppp-on='sudo /usr/sbin/ppp-on'
alias ppp-off='sudo /usr/sbin/ppp-off'
alias firestarter='sudo su -c firestarter'
alias mpg123='mpg123 -o oss'
alias mpg321='mpg123 -o oss'
alias vba='/home/paul/downloads/VisualBoyAdvance -f 4'
alias hist="grep '$1' /home/paul/.zsh_history"
alias irssi="irssi -c irc.freenode.net -n yyz"
alias mem="free -m"
alias msn="tmsnc -l hutchy@subdimension.com"

# ekvivalentní příkazu less
alias -g L='|less' 

# command S equivalent to command &> /dev/null &
# ekvivalentní příkazu &> /dev/null &

# napiš jméno adresáře pro vstoupení do něj
compctl -/ cd

```

Je zde mnoho dalších možností jak si upravit chování Zsh, zjevně příliš mnoho pro probírání zde, podívej se na [Zsh manuál](http://zsh.sunsite.dk/Doc/) pro více informací.

### Ukázkové .zshrc soubory

Zde je seznam `.zshrc` souborů. Klidně přidej svůj vlastní:

*   Øyvind 'Mr.Elendig' Heggstad <=> Základní nastavení, s dynamickou výzvou příkazového řádku a titulkem okna/hardinfo <=> [http://arch.har-ikkje.net/configs/home/dot.zshrc](http://arch.har-ikkje.net/configs/home/dot.zshrc)

## Povolení Unicode (zastaralé)

**Note:** Unicode je v oficiálním balíku Arch Linuxu standardně povoleno.

The latest versions of Zsh support unicode characters. To enable it, just rebuild the package with the [Arch Build System](/index.php/Arch_Build_System "Arch Build System"). Poslední verze Zsh podporují unicode znaky. Pro jejich povolení znovu sestvat balík s pomocí [Arch Build System](/index.php/Arch_Build_System "Arch Build System").

A přidej volbu *--enable-multibyte* do:

 `PKGBUILD` 
```
build() {
cd $startdir/src/$pkgname-$pkgver
./configure --prefix=/usr --bindir=/bin \
--enable-etcdir=/etc/zsh \
--enable-zshenv=/etc/zsh/zshenv \
--enable-zlogin=/etc/zsh/zlogin \
--enable-zlogout=/etc/zsh/zlogout \
--enable-zprofile=/etc/profile \
--enable-zshrc=/etc/zsh/zshrc \
--enable-maildir-support \
--with-curses-terminfo \
--enable-zsh-secure-free \
**--enable-multibyte**
```

## Odinstalace

Pro případ že se rozhodneš, že Zsh není shell pro tebe a budeš se chtít vrátit Bashi. Nejprve musíš změnit tvůj implicitní shell na Bash.

Následuj, [Zsh#Nastavení Zsh jako implicitní shell](/index.php/Zsh#Nastaven.C3.AD_Zsh_jako_implicitn.C3.AD_shell "Zsh") pro změnu shellu zpět na Bash, jen nahraď Zsh Bashem.

Nyní můžeš bezpečně odstranit balík Zsh.

**Warning:** Pokud nedodržíš předchozí instrukce, může se vyrojit spousta problémů.

Pokud jsi nenásledoval instrukce viz výše, stále ještě můžeš změnt implicitní shell zpět na Bash pomocí editace /etc/passwd jako root. Ukázka:

z:

```
uzivatel:x:1000:1000:Full Name,,,:/home/username:/bin/zsh

```

na:

```
uzivatel:x:1000:1000:Full Name,,,:/home/username:/bin/bash

```

## Zdroje

*   [Zsh Introduction](http://zsh.sunsite.dk/Intro/intro_toc.html)
*   [Users Guide](http://zsh.sourceforge.net/Guide/zshguide.html)
*   [Zsh Docs](http://zsh.sunsite.dk/Doc/)
*   [Zsh FAQ](http://zsh.sunsite.dk/FAQ/)
*   [Zsh Wiki](http://zshwiki.org/home/)
*   [Zsh-lovers](http://grml.org/zsh/zsh-lovers.html)
*   [Bash2Zsh Reference Card](http://www.bash2zsh.com/zsh_refcard/refcard.pdf)

*   **IRC kanál:** #zsh at irc.freenode.org