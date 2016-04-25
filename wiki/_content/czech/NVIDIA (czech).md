## Contents

*   [1 Instalace ovladačů NVIDIA pomocí pacmanu](#Instalace_ovlada.C4.8D.C5.AF_NVIDIA_pomoc.C3.AD_pacmanu)
    *   [1.1 Informace od správce balíčku *tpowa*](#Informace_od_spr.C3.A1vce_bal.C3.AD.C4.8Dku_tpowa)
    *   [1.2 Instalace ovladačů](#Instalace_ovlada.C4.8D.C5.AF)
    *   [1.3 Nastavení X-Serveru](#Nastaven.C3.AD_X-Serveru)
    *   [1.4 Aktivace kompozitního rozšíření](#Aktivace_kompozitn.C3.ADho_roz.C5.A1.C3.AD.C5.99en.C3.AD)
    *   [1.5 Úprava rc.conf](#.C3.9Aprava_rc.conf)
    *   [1.6 Problémy, které mohou nastat](#Probl.C3.A9my.2C_kter.C3.A9_mohou_nastat)
        *   [1.6.1 Způsobené ovladači nVidia](#Zp.C5.AFsoben.C3.A9_ovlada.C4.8Di_nVidia)
        *   [1.6.2 Způsobené Archem](#Zp.C5.AFsoben.C3.A9_Archem)
    *   [1.7 Nástroje pro nastavení ovladačů](#N.C3.A1stroje_pro_nastaven.C3.AD_ovlada.C4.8D.C5.AF)
    *   [1.8 Známé potíže](#Zn.C3.A1m.C3.A9_pot.C3.AD.C5.BEe)
*   [2 Špatný výkon po instalaci ovladačů](#.C5.A0patn.C3.BD_v.C3.BDkon_po_instalaci_ovlada.C4.8D.C5.AF)
*   [3 Jak nainstalovat ovladače NVIDIA tradičním způsobem](#Jak_nainstalovat_ovlada.C4.8De_NVIDIA_tradi.C4.8Dn.C3.ADm_zp.C5.AFsobem)
*   [4 Ladění ovladačů NVIDIA](#Lad.C4.9Bn.C3.AD_ovlada.C4.8D.C5.AF_NVIDIA)
    *   [4.1 Vypnutí loga NVIDIA](#Vypnut.C3.AD_loga_NVIDIA)
    *   [4.2 Aktivace HW akcelerace](#Aktivace_HW_akcelerace)
    *   [4.3 Přepsání nalezený monitor](#P.C5.99eps.C3.A1n.C3.AD_nalezen.C3.BD_monitor)
    *   [4.4 Zapnutí TripleBufferu](#Zapnut.C3.AD_TripleBufferu)
    *   [4.5 Použití událostí na úrovní OS](#Pou.C5.BEit.C3.AD_ud.C3.A1lost.C3.AD_na_.C3.BArovn.C3.AD_OS)
    *   [4.6 Zapnutí úspory energie](#Zapnut.C3.AD_.C3.BAspory_energie)
    *   [4.7 Další texty:](#Dal.C5.A1.C3.AD_texty:)
*   [5 Použití TV výstupu na kartách NVIDIA](#Pou.C5.BEit.C3.AD_TV_v.C3.BDstupu_na_kart.C3.A1ch_NVIDIA)
*   [6 Jak nainstalovat ovladače NVIDIA s vlastním jádrem?](#Jak_nainstalovat_ovlada.C4.8De_NVIDIA_s_vlastn.C3.ADm_j.C3.A1drem.3F)

### Instalace ovladačů NVIDIA pomocí pacmanu

#### Informace od správce balíčku *tpowa*

Tento balíček je pro ty, kdo používájí distribuční verzi jádra! Testuju pouze s jádrem 2.6 a Xorgem.

*Poznámka: nezapomněli jsme ani na lidi používající jádro -beyond, viz další odstavec*

Pro uživatele více jader: Pro každé jádro musíte nainstalovat balíček nvidia zvlášt!

#### Instalace ovladačů

Balíčky jsou umístěny v repozitáři extra. Vypněte X-Server, jinak pacman nebude moci dokončit instalaci! Jako root spusťte:

```
pacman -S nvidia (pro nové karty)
pacman -S nvidia-96xx nebo pacman -S nvidia-71xx (pro starší karty)

```

Pro uživatele jádra **-beyond**:

```
pacman -S nvidia-beyond
pacman -S nvidia-96xx-beyond or pacman -S nvidia-71xx-beyond (pro starší)

```

Pokud používáte jádra **-ck**, **-suspend2** nebo **-mm** - nahraďdte pouze koncovky z předchozího případu.

Vizte [`README`](http://us.download.nvidia.com/XFree86/Linux-x86_64/100.14.11/README/appendix-a.html) od nvidia, kde se dozvíte, který ovladač podporuje které karty.

#### Nastavení X-Serveru

Upravte `/etc/X11/XF86Config` nebo `/etc/X11/xorg.conf`: V sekci modules odstraňtě: `GLcore` a `DRI`

A přidejte modul:

```
Load "glx"

```

Ujistěte se, že NEMÁTE zapnutý tento modul:

```
 Load           "type1"

```

Zakomentujte celou část `Section DRI`:

```
#Section "DRI"
# Mode 0666
#EndSection

```

Změňte `Driver "nv"` nebo `Driver "vesa"` na `Driver "nvidia"` Pokud existuje volba `Chipset`, vypněte ji.

To bylo základní nastavení. Pokud potřebujete detailnější popis, podívejte se do `/usr/share/doc/NVIDIA_GLX-1.0/README.txt`.

Můžete také spustit:

```
nvidia-xconfig

```

Vizte [Instalace a Nastavení Xorgu](/index.php/Xorg_(%C4%8Cesky) "Xorg (Česky)").

#### Aktivace kompozitního rozšíření

Více informací najdete ve článku [Composite_(Česky) Composite (česky)].

#### Úprava `rc.conf`

Do sekce MODULES v `/etc/rc.conf` přidejte `nvidia` (není potřeba pokud máte nové jádro a udev). Vyžadováno u nvidia-71xx a jádra >=2.6.13!

#### Problémy, které mohou nastat

##### Způsobené ovladači nVidia

Xorg7: Prosím odstraňte váš starý adresář /usr/X11R6, může způsobovat potíže během instalace. Také se ujistěte, že máte nainstalovaný `pkgconfig`. Instalační program NVIDIA používá pkgconfig pro zjištění, které moduly Xorgu jsou nainstalované.

Pokud jste zaznamenali špatný výkon grafiky, podívejte se na `/usr/lib/libGL.so.1`, `/usr/lib/libGL.so`, `/usr/lib/libGLcore.so.1` Možná jsou špatně vytvořené symlinky na MESu nebo tak něco. Zkuste reinstalovat ovldače pomocí `pacman -S nvidia`.

Pokud při spouštění OpenGL aplikace (např. enemy-territory nebo glxgear) uvidíte tuto hlášku:

```
Error: Could not open /dev/nvidiactl because the permissions are too
restrictive. Please see the `FREQUENTLY ASKED QUESTIONS` 
section of `/usr/share/doc/NVIDIA_GLX-1.0/README` 
for steps to correct.

```

Přidejte svého uživatele do skupiny `video` pomocí `gpasswd -a *yourusername* video` (nezapomeňte se přelogovat, nebo napište: source /etc/profile).

##### Způsobené Archem

**GCC update:** Musíte zkompilovat modul stejným kompilátorem (stejnou verzí), jaký byl použitý na kompilaci jádra, jinak drivery nemusí fungovat. Jednoduché `pacman -S nvidia` by mělo vše napravit, pokud ne, počkejte na nové jádro a zatím zůstaňte u starého jádra a gcc.

**Update jádra:** Update jádra vyžaduje přeinstalování ovladačů. Postup je popsaný výš.

#### Nástroje pro nastavení ovladačů

Nový konfigurační nástroj ovladačů nVidia se nazývá 'nvidia-settings'. Nemusíte ho používat, je to jen addon!
Pro více informací o použití se podívejte do /usr/share/doc/NVIDIA_GLX-1.0/nvidia-settings-user-guide.txt
Prosím nainstalujte gtk2 pomocí *pacman -S gtk2* abyste mohli tento nástroj použít.

**Poznámka:** Pokud máte problémy, jako pád X-serveru při spuštění nástroje nvidia-settings, smažte soubor `.nvidia-settings-rc` ve svém domovském adresáři.

**Automatické spuštění nvidia-settings:** Pokud chcete použít nastavení z nvidia-settings při spuštění, spusťte nvidia-settings alespoň jednou, aby se nastavení obnovilo. Konfigurační soubor se vytvoří v ~/.nvidia-settings-rc. Potom přidejte následující příkaz do auto-start modulu ve vašem prostředí:

```
nvidia-settings --load-config-only

```

#### Známé potíže

Pokud zaznamenáváte pády, zkuste vypnout `RenderAccel "True"`.

Pokud instalační program nvidia hlásí rozdílnou verzi GCC u současných ovladačů a u jádra, podívejte se, jak nainstalovat ovladače tradičním způsobem, ale nezapomeňte na `export IGNORE_CC_MISMATCH=1`

Pokud máte nějaké připomínky k balíčku, pište je prosím sem: [https://bbs.archlinux.org/viewtopic.php?t=10692](https://bbs.archlinux.org/viewtopic.php?t=10692) Pokud máte problém s ovladači, podívejte se na fórum nvidia: [http://www.nvnews.net/vbulletin/forumdisplay.php?s=&forumid=14](http://www.nvnews.net/vbulletin/forumdisplay.php?s=&forumid=14) Changelog se nachází zde: [http://www.nvidia.com/object/linux_display_ia32_1.0-8762.html](http://www.nvidia.com/object/linux_display_ia32_1.0-8762.html)

### Špatný výkon po instalaci ovladačů

Pokud máte velmi malé FPS v porovnání s předchozími ovladači, zkontrolujte nejprve, jestli máte zapnuté přímé renderování. To provedete takto:

```
glxinfo | grep direct

```

Pokud dostanete: 'direct rendering: No', pak máte problém. Dále zkontrolujte jestli odpovídají verze glx u klienta a serveru:

```
glxinfo | egrep "glx (vendor|version)"

```

Pokud vidíte rozdílné výrobce nebo verze, spusťte tyto příkazy:

```
ln -fs /usr/lib/libGL.so.$VER /usr/X11R6/lib/libGL.so
ln -fs /usr/lib/libGL.so.$VER /usr/X11R6/lib/libGL.so.1
ln -fs /usr/lib/libGL.so.$VER /usr/lib/libGL.so.1.2

```

kde $VER je verze balíčku nvidia, který právě používáte. Tu zjístíte například pomocí `nvidia-settings`

To je vše. Teď restartujte Xserver a měli byste mít normální akceleraci.

### Jak nainstalovat ovladače NVIDIA tradičním způsobem

**VAROVÁNÍ** Tento postup vám pravděpodobně způsobí dost závažných problémů, protože libgl je poskytována balíčkem z pacmanu, musíte vytvořit prázdný balíček libgvl a dále nvidia-utils pro Mesa OpenGL Library. Jiné balíčky které budete instalovat zavisí na mese také. Více informací naleznete zde: [https://bbs.archlinux.org/viewtopic.php?pid=286530](https://bbs.archlinux.org/viewtopic.php?pid=286530)

*   Stáhněte nejnovější ovladače z: [http://www.nvidia.com/object/linux.html](http://www.nvidia.com/object/linux.html)

Soubor by se měl jmenovat nějak takto: `NVIDIA-Linux-x86-1.0-7167-pkg0.run`

Následující 4 kroky ohledně jádra můžete přeskočit, pokud používáte alespoň jádro 2.6.5, protože potřebné inkluze jsou už v balíčku s jádrem

*   Stáhnete nejnovější balíček pro jádro, které používáte

`uname -r` vám zobrazí verzi jádra

*   *   [http://www.kernel.org/pub/linux/kernel/v2.6/](http://www.kernel.org/pub/linux/kernel/v2.6/) - for the 2.6 series
    *   [http://www.kernel.org/pub/linux/kernel/v2.4/](http://www.kernel.org/pub/linux/kernel/v2.4/) - for the 2.4 series

*   Přesuňte aktuální nekompletní zdroj jádra do 2.x.x.old:

```
mv /usr/src/2.x.x /usr/src/2.x.x.old

```

*   Rozbalte svůj zdroják do `/usr/src`:

```
mv /path/to/linux-2.x.x.tar.bz2 /usr/src
cd /usr/src
tar --bzip2 -xvf linux-2.x.x.tar.bz2

```

*   Zkopířujte staré adresáře pro inkluzi a `.config` do nového stromu:

```
cp -rp linux-2.x.x.old/include/ linux-2.x.x/include/
cp linux-2.x.x.old/.config linux-2.x.x/.config

```

*   Ukončete Xka
    *   Použijte Control-Alt-F5 (nebo jakoukoliv F* klávesu chcete)
    *   Přihlašte se jako root
    *   Přejděte do runlevelu 3

```
init 3

```

*   Spusťte instalátor nvidia

```
sh /path/to/NVIDIA-Linux-x86-1.0-5336-pkg0.run

```

Budete dotázáni, jestli souhlasíte s jejich licencí, takže klikněte parkrát na OK, ovladač se nyní sestaví a nainstaluje

*   Upravte XFree86Config
    *   Otevřete `/etc/X11/XFree86Config` a jděte do sekce `Device`
    *   Změňte ovladač z aktuálního (nejspíš `nv` či `vesa`) na `nvidia`:
        *   `Driver "nv"` na `Driver "nvidia"`
    *   Odkomentujte řádek `#Load "glx"`
    *   Odstraňte řádku Chipset, pokud existuje

*   Přidejte nvidia do modulů do /etc/rc.conf:

```
MODULES=(*... some modules ...* nvidia)

```

*   Restartujte PC a užívejte 3D akceleraci :)

## Ladění ovladačů NVIDIA

Otevřete `/etc/X11/xorg.conf` nebo `/etc/X11/XFree86Config` a zkuste následující možnosti: *Ne všechny možnosti musí na vašem systému fungovat; zkoušejte je opatrně a nezapomínejte zálohovat váš konfigurační soubor.*

### Vypnutí loga NVIDIA

V sekci `Device` přidejte Option `"NoLogo"`

```
Option "NoLogo" "True"

```

### Aktivace HW akcelerace

Do sekce `Device` přidejte `"RenderAccel"`.

```
Option "RenderAccel" "True"

```

### Přepsání nalezený monitor

Volba `"ConnectedMonitor"` v sekci code>Device</code> dovoluje přenastavit detekci monitoru když se spouští Xserver. Tohle by měl být párvteřinový návod jak zprovoznit ovladače. Dostupné volby jsou: `"CRT"` (cathode ray tube), `"DFP"` (digital flat panel), or `"TV"` (television).

Přidejte následujicí volbu pro vynucení použití DFP monitorů.

```
Option "ConnectedMonitor" "DFP"

```

**Poznámka:** používejte "CRT" pro všechny analogové 15ti pinové koncovky (i pokud máte plochý monitor). "DFP" je určeno pouze pro digitální DVI!

### Zapnutí TripleBufferu

TripleBuffering zapnete přidáním volby `"TrippleBuffer"` do sekce `Device`.

```
Option "TripleBuffer" "True"

```

Používejte tuto volbu pouze pokud má vaše grafická karta dostatek paměti (128mb a víc) a kombinujte ji s "Sync to VBlanc" (tuto volbu můžete nastavit v nvidia-settings).

### Použití událostí na úrovní OS

Převzato z README souboru od NVIDIA: *"Použijte události na úrovni OS pro efektivní zaznamenání, kdy klient podporuje přímé renderování v okně které má být kompozitní."* Ať to znamená co chce, může to pomoci zlěpšit výkon. Tento volba je v současnosti nekompatibilní s SLI a multi-GPU módy.

Do sekce `Device` přidejte:

```
Option "DamageEvents" "True"

```

V novějších ovladačích je tato funkce zapnutá

### Zapnutí úspory energie

... Pro zelenjší planetu (nesouvisí přímo s ovladači nvidia). Do sekce `Monitor` vložte:

```
Option "DPMS" "True"

```

### Další texty:

*   [NVIDIA drivers README file](http://us.download.nvidia.com/XFree86/Linux-x86/100.14.19/README/appendix-b.html) (aktuální drivery)
*   [Compiz Fusion wiki](http://wiki.compiz-fusion.org/Hardware/NVIDIA)

## Použití TV výstupu na kartách NVIDIA

Dobrý článek na toto téma najdete zde:

```
 [http://en.wikibooks.org/wiki/NVidia/TV-OUT](http://en.wikibooks.org/wiki/NVidia/TV-OUT)

```

## Jak nainstalovat ovladače NVIDIA s vlastním jádrem?

Znalost fungování systému ABS je výhodou, proto si přečtěte nejprvé pár článků:

*   [ABS - The Arch Build System (Česky)](/index.php/ABS_-_The_Arch_Build_System_(%C4%8Cesky) "ABS - The Arch Build System (Česky)")
*   [Makepkg](/index.php/Makepkg "Makepkg")

Vytvoříme si vlastní balíček s použitím balíčku, který už je připravený v ABS:

Vytvořte dočasný adresář, kde sestavíme nový balíček:

```
 mkdir -p /var/abs/local/

```

Zkopírujte do něj soubory z původního nvidiackého balíčku:

```
 cp -r /var/abs/extra/x11/nvidia/ /var/abs/local/

```

Jděte do našeho dočasného adresáře:

```
 cd /var/abs/local/nvidia

```

Teď potřebujeme upravit soubory nvidia.install a PKGBUILD, v obou je nutné změnit KERNEL_VERSION podle verze jádra na kterou chcete drivery instalovat. Tu zjistíte pomocí:

```
 uname -r

```

Tedy např. 2.6.24-ARCH změníte na 2.4.12-MT

Poté spusťte:

```
 makepkg -i -c

```

.. Teď počkejte, než se vytvoří balíček pro vaše vlastní jádro. Hodně štěstí!