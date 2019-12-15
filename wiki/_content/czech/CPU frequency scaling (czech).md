cpufreq odkazuje na infrastrukturu jádra, která umožuje škálovat frekvenci CPU. Tato technologie umožňuje operačnímu systému zvyšovat nebo snižovat rychlost procesoru. Frekvence CPU může být škálována podle zátěže systému, v závislosti na událostech ACPI nebo ručně.

Minimálně jsou potřeba patřičné moduly jádra a musí být použit regulátor. Pokročilé volby zahrnují [#cpufrequtils](#cpufrequtils),[acpid](/index.php/Acpid "Acpid"),[laptop-mode-tools](/index.php/Laptop-mode-tools "Laptop-mode-tools") nebo GUI nástroje poskytované vaším grafickým prostředím.

## cpufrequtils

[cpufrequtils](https://aur.archlinux.org/packages/cpufrequtils/) je sada nástrojů pro pomoc při škálování frekvence CPU. Balíček není přímo potřebný pro škálování procesoru ale je doporučený, protože poskytuje hodně command-line nástrojů a skript pro nastavení frekvence/regulátoru při startu počítače

balíček [cpufrequtils](https://aur.archlinux.org/packages/cpufrequtils/) je dostupný v repozitáři [extra]:

```
# pacman -S cpufrequtils

```

## Konfigurace

Konfigurace škálování procesoru je rozložená na tři části:

1.  Načtení odpovídajících ovladačů
2.  Načtení požadovaných regulátorů
3.  Volba metody pro změnu regulátoru:
    *   Ručně přes /sys nebo přes cpufreq-set
    *   Pomocí [démona cpufrequtils](#Démon)
    *   [Laptop Mode Tools](/index.php/Laptop_Mode_Tools "Laptop Mode Tools")
    *   Události [acpid](/index.php/Acpid "Acpid")
    *   Aplikace/applety grafického prostředí
    *   Kombinace několika výše uvedených možností

### Ovladač frekvence CPU

Pokud má škálování CPU fungovat správně, operační systém musí nejdříve znát limity procesoru(ů). Pokud má být toto zajištěno, musí být načten správný ovladač, který může číst a spravovat specifikace CPU. Tento ovladač potřebuje povolit funkce v BIOSu které mohou být pojmenovány jako: Speedstep, Cool and Quiet, PowerNow!, nebo ACPI.

Pokud máte 64-bitový procesor, budete nejspíš potřebovat buďto acpi-cpufreq pro Intel nebo powernow-k8 pro procesory AMD K8/K10 (Athlon 64, Opteron a Phenom. Tyto moduly jsou sestaveny jak pro 32- tak i pro 64-bitové systémy takže pokud máte 32 bitové jádro na 64 bitovém stroji, pořád jsou to pravděpodobně ty moduly které chcete.

Work in progress...