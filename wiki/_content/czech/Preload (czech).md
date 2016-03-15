**preload** je program, který beží v pozadí jako démon a monitoruje používání programů pomocí *Markov chains*(Markovovo algoritmu ?). Často používané programy jsou načítány do paměti během nízkého vytížení počítače. To vede k rychlejšímu spouštěcímu času a menší velioksti dat, která jsou získávána z disku. preload je často používán s [prelink](/index.php/Prelink "Prelink"). Autorem preloadu je Behdade Esfahbod.

## Instalace

preload je instalovatelný pacmanem:

```
pacman -S preload

```

Spouští se přímo:

```
/etc/rc.d/preload start

```

Aby se preload spouštěl automaticky při startu systému, je potřeba ho přidat do seznamu démonů v [/etc/rc.conf](/index.php/Rc.conf "Rc.conf"):

```
DAEMONS =(... preload ...)

```