# Globálně

**Note:** [Kernel_modules#Blacklisting](/index.php/Kernel_modules#Blacklisting "Kernel modules")

*   Kompletně zakázat modul repráčku při startu přidáním `pcspkr` do pole `MODULES` v `/etc/rc.conf`:

*   Pokud `lsmod` něco vypíše, přidej `snd_pcsp`.

# Lokálně

*   Pro zakázání obtěžujícího pípání repráčku v X:

```
$ xset -b

```

Pokud to chceš zakázat při každém startu X, přidej tento příkaz do nějakého startovacího skripu, jako `~/.xinitrc`.

*   Pro zakázání v konzoli:

```
$ setterm -blength 0

```

Podobně můžeš příkaz přidat do `~/.bashrc`.

*   Jiný způsob je přidání tohoto řádku do `~/.inputrc`:

```
set bell-style none

```

*   Uživatelé [ALSA](/index.php/ALSA "ALSA") můžou též zkusit zlumení PC Speakeru:

```
$ amixer set 'PC Speaker' 0% mute

```

Další informace najdeš v těchto *manuálových stránkách*: *xset(1), setterm(1), readline(3)*