[DOSBox](http://www.dosbox.com/) je x86 PC DOS emulátor pro spuštění starých her nebo programů.

## Contents

*   [1 Instalace](#Instalace)
*   [2 Konfigurace](#Konfigurace)
*   [3 Použití](#Pou.C5.BEit.C3.AD)
*   [4 Další zdroje](#Dal.C5.A1.C3.AD_zdroje)

# Instalace

Instalace je velmi jednoduchá, stačí nainstalovat balíček [dosbox](https://www.archlinux.org/packages/?name=dosbox).

# Konfigurace

Žádná počáteční konfigurace není nutná, avšak oficiální DOSBox manuál odkazuje na konfigurační soubor pojmenovaný `dosbox.conf`. Defaultně však tento soubor neexistuje.

Pro jeho vytvoření jednoduše spusťte <tt>dosbox</tt> bez jakýchkoli parametrů:

```
$ dosbox

```

Poté v příkazovém řádku DOSu napište:

```
**Z:\>** config -wc dosbox.conf

```

Konfigurační soubor `dosbox.conf` bude vytvořen v aktuální složce.

# Použití

Jednoduchý způsob jak spustit dosbox je umístit DOSovou hru (nebo její instalační soubor) do složky, a pak spustit dosbox se jménem spožky jako parametrem. Např.:

```
$ dosbox ./složka-hry/

```

Měli byste mít příkazový řádek DOSu, jehož pracovní složka je složka specifikovaná výše (v našem případě složka-hry). Odtud můžete spouštět požadované programy:

```
**C:\>** SETUP.EXE

```

# Další zdroje

Pro více informací navštivte oficiální stránku DOSBoxu: [http://www.dosbox.com/](http://www.dosbox.com/)

[Abandonia](http://www.abandonia.com/) - Veliký repozitář starých opuštěných DOSových her