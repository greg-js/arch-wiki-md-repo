Jelikož Intel poskytuje a podporuje open source ovladače, grafické karty od něj jsou víceméně plug-and-play.

## Contents

*   [1 Modely](#Modely)
*   [2 Ovladač](#Ovlada.C4.8D)
*   [3 Instalace](#Instalace)
*   [4 Konfigurace](#Konfigurace)
*   [5 KMS (Kernel Mode Setting)](#KMS_.28Kernel_Mode_Setting.29)
    *   [5.1 Vizte též](#Vizte_t.C3.A9.C5.BE)
*   [6 Tipy a triky](#Tipy_a_triky)
    *   [6.1 Nastavení škálování](#Nastaven.C3.AD_.C5.A1k.C3.A1lov.C3.A1n.C3.AD)
    *   [6.2 Obejití chyby s otvíráním víka laptopu](#Obejit.C3.AD_chyby_s_otv.C3.ADr.C3.A1n.C3.ADm_v.C3.ADka_laptopu)
        *   [6.2.1 Řešení #1](#.C5.98e.C5.A1en.C3.AD_.231)
        *   [6.2.2 Řešení #2](#.C5.98e.C5.A1en.C3.AD_.232)
    *   [6.3 Problém s KMS: konzole je omezená na malou oblast](#Probl.C3.A9m_s_KMS:_konzole_je_omezen.C3.A1_na_malou_oblast)
*   [7 Řešení problémů](#.C5.98e.C5.A1en.C3.AD_probl.C3.A9m.C5.AF)
    *   [7.1 Glxgears ukazuje slabé výsledky](#Glxgears_ukazuje_slab.C3.A9_v.C3.BDsledky)
    *   [7.2 Prázdná obrazovka během bootu při "Loading modules"](#Pr.C3.A1zdn.C3.A1_obrazovka_b.C4.9Bhem_bootu_p.C5.99i_.22Loading_modules.22)

### Modely

Je oblíbenou chybou myslet si, že je "Intel 945G" a "Intel GMA 945" ten samý grafický čip, pouze jinak nazvaný. To druhé defakto ani neexistuje. Intel používá "GMA" pro označení grafického jádra nebo-li GPU. Cokoliv jiného je ve skutečnosti model **čipsetu** na základní desce, např. "915G", "945GM", "G965" nebo "G45".

Mezi ty běžnější GPU a jejich korespondující čipsety patří:

*   Intel GMA 900 (910, 915)
*   Intel GMA 950 (945)

Čipset "i810" (opět, na základní desce; ne GPU) je opravdu velmi starý a byl vyráběn dlouho před řadou produktů 9xx, u níž začalo označování integrované grafiky pomocí GMA. Podobně mohou alternativně jména pro čipy 910, 915 a 945 obsahovat předponu *i*.

Viz [tento seznam](https://en.wikipedia.org/wiki/Intel_GMA#Table_of_GMA_graphics_cores_and_chipsets "wikipedia:Intel GMA").

### Ovladač

*   xf86-video-intel

## Instalace

Předpokladem je [Xorg](/index.php/Xorg "Xorg").

```
# pacman -S xf86-video-intel

```

## Konfigurace

Od doby, co se o správu zařízení v Xorg začal starat HAL, není žádná potřeba pro jakýkoliv druh konfigurace.

Jediná věc, kterou byste měli udělat již na začátku (netýká se přímo konfigurace tohoto ovladače), je přidat svého uživatele do příslušné skupiny:

```
# gpasswd -a jménouživatele video

```

## KMS (Kernel Mode Setting)

[KMS](/index.php/KMS "KMS") je podporován těmi čipsety od Intelu, které používají DRM ovladač i915, a od verze jádra 2.6.32 je povolen ve výchozím nastavení. Od xf86-video-intel 2.10 je použití KMS [povinné](https://www.archlinux.org/news/484/). KMS se typicky inicializuje po bootstrapu jádra. Je nicméně možné zapnout KMS během samotného bootstrapu, v tom případě poběží celý proces bootování v nativním rozlišení.

**Note:** Pokud používáte KMS, *musíte* z `/boot/grub/menu.lst` v řádku "kernel" odstranit jakoukoliv zmínku o "vga" nebo "video".

Přidejte moduly `intel_agp` a `i915` do řádku MODULES v `/etc/mkinitcpio.conf`:

```
MODULES="**intel_agp i915**"

```

Nyní nechte znovu vygenerovat initramfs:

```
# mkinitcpio -p kernel26

```

Pokud byste někdy chtěli KMS vypnout, můžete bez nutnosti opětovného generování čehokoliv v `/boot/grub/menu.lst` GRUBu změnit volbu `i915.modeset` na 0:

```
# (0) Arch Linux
title  Arch Linux
root   (hd0,0)
kernel /boot/vmlinuz26 root=/dev/... **i915.modeset=0**
initrd /boot/kernel26.img

```

Abyste ho vypnuli bez nutnosti upravovat `menu.lst`, zapněte počítač a až uvidíte obrazovku GRUBu, stiskněte nějakou klávesu, abyste tím zastavili odpočet. Vyberte jádro, které chcete nabootovat (zřejmě to, které je již vybrané) a skiskněte "e" pro "editaci". Nyní vyberte řádek začínající na "kernel" a stiskněte opět "e" pro úpravy. Nyní můžete přidat volbu `i915.modeset` a vypnout KMS tím, že ji nastavíte na 0\. Stiskněte Enter a poté "b" pro nabootování tohoto jádra. Mějte na paměti, že toto je pouze dočasné, takže po dalším restartu bude KMS bez vašeho zásahu opět zapnuté.

**Note:** Pokud během bootu s Intel GMA 950 dostáváte prázdnou obrazovku, downgradujte na kernel 2.6.31.6-1 nebo vypněte modesetting pomocí zmíněného parametru jádra.

### Vizte též

*   [KMS](/index.php/KMS "KMS") (anglicky) — Článek o KMS na Arch Wiki
*   Fórum Arch Linuxu: [HOWTO: Enable KMS with the stock 2.6.29-ARCH kernel](https://bbs.archlinux.org/viewtopic.php?id=69083)
*   Fórum Arch Linuxu: [Intel 945GM, Xorg, Kernel - performance](https://bbs.archlinux.org/viewtopic.php?pid=522665#p522665)

## Tipy a triky

### Nastavení škálování

Toto může být užitečné pro některé aplikace, které běží na celé obrazovce a nastavují si vlastní rozlišení.

```
xrandr --output LVDS1 --set PANEL_FITTING parametr

```

kde <tt>parametr</tt> může být

*   <tt>center</tt>: rozlišení bude zachováno takové, jaké bylo definováno; nebude provedeno žádné škálování,
*   <tt>full</tt>: škálovat rozlišení tak, aby využilo celou obrazovku nebo
*   <tt>full_aspect</tt>: škálovat rozlišení na maximální možnou hodnotu ale zachovávat poměr stran.

Pokud tohle nefunguje, můžete zkusit

```
xrandr --output LVDS1 --set "scaling mode" parametr

```

kde <tt>parametr</tt> je jeden z <tt>"Full"</tt>, <tt>"Center"</tt> nebo <tt>"Full aspect"</tt>.

### Obejití chyby s otvíráním víka laptopu

#### Řešení #1

Na laptopech s grafickým čipsetem od Intelu se můžete setkat s nefunkčním displejem X, když zavřete víko laptopu pro jeho uspání, a opět ho otevřete. Vizte bug [https://bugs.freedesktop.org/show_bug.cgi?id=24970](https://bugs.freedesktop.org/show_bug.cgi?id=24970) pro více informací.

Zde je jedna možnost, jak tento problém obejít. Recept je založen na jednom podobném ze stránek Fedory: [https://fedoraproject.org/wiki/Common_F12_bugs#Display_cannot_be_reactivated_if_it_enters_sleep_mode_with_laptop_lid_closed](https://fedoraproject.org/wiki/Common_F12_bugs#Display_cannot_be_reactivated_if_it_enters_sleep_mode_with_laptop_lid_closed)

**Note:** Toto řešení bude fungovat pouze v jednouživatelském systému. Můžete ho rozchodit i pro více uživatelů, pokud přidáte nějakou proceduru, která bude zjišťovat, který uživatel systém uvedl do stavu spánku.

Nainstalujte acpid:

```
# pacman -S acpid

```

Poté umístěte acpid před hal do sekce DAEMONS ve vašem souboru `/etc/rc.conf`.

Vytvořte soubor `/etc/acpi/actions/reset-display.sh` s následujícím obsahem:

```
 #!/bin/bash
 PATH="/bin:/usr/bin:/sbin:/usr/sbin"
 export DISPLAY=:0.0
 sleep 10 
 if grep open /proc/acpi/button/lid/LID/state
 then
   su "$(getent passwd $UID | cut -d: -f1)" -c "xrandr --output LVDS1 --off" 
   su "$(getent passwd $UID | cut -d: -f1)" -c "xrandr --output LVDS1 --auto" 
 fi

```

kde <tt>$UID</tt> je UID uživatele (jímž jste vy), který uvedl laptop do stavu spánku. Hlavní rozdíl od původní metody z Fedořy je v použití příkazu <tt>sleep</tt>. Bez něj nebude stav tlačítka víčka ve chvíli, kdy ho bude skript `reset-display.sh` ověřovat, aktuální. V některých případech bude při běhu na síťový adaptér stačit menší prodleva (například 3 sekundy), 10 sekund ale bude fungovat vždy. Nezapomeňte učinit skript spustitelným:

```
 # chmod +x /etc/acpi/actions/reset-display.sh

```

Poté musíme přiřadit tuto akci k události pro tlačítko víčka. Do souboru `/etc/acpi/handler.sh` pod <tt>button/lid)</tt> přidejte následující řádek:

```
 /etc/acpi/actions/reset-display.sh

```

Nyní zrestartujte svůj laptop, případně pouze v následujícím pořadí restartujte tyto daemony:

```
 # /etc/rc.d/hal stop
 # /etc/rc.d/acpid start
 # /etc/rc.d/hal start

```

#### Řešení #2

Jednodušší, méně spolehlivá obezlička je prostě uspat počítač znovu a opět ho probudit. To často tento problém vyřeší a navrátí X do funkčního stavu.

### Problém s KMS: konzole je omezená na malou oblast

Při bootu může být zapnutý jeden z video portů s nízkým rozlišením, který způsobí, že terminál využije pouze malou oblast obrazovky. Pro opravu tohoto problému výslovně vypněte problematický port pomocí volby pro modul i915\. Například přidejte do řádku kernel v `/boot/grub/menu.lst` následující:

```
 video=SVIDEO-1:d

```

Pokud to takto nefunguje, můžete namísto SVIDEO-1 zkusit vypnout TV1 nebo VGA1.

## Řešení problémů

### Glxgears ukazuje slabé výsledky

Pokud pro prověření grafického výkonu vašeho systému spustíte glxgears, může se vám stát, že glxgears ukazuje výsledky okolo **60 FPS**:

```
...
311 frames in 5.0 seconds = 61.973 FPS
311 frames in 5.0 seconds = 62.064 FPS
311 frames in 5.0 seconds = 62.026 FPS
...

```

To je způsobeno nikoliv regresí ve výkonu ale tím, že grafická karta používá **VSync**, což znamená, že dané výsledky označují počet snímků za sekundu vaší obrazovky.

**Note:** glxgears není benchmark pro porovnávání výkonu mezi dvěma nebo více systémy.

### Prázdná obrazovka během bootu při "Loading modules"

Pokud používáte KMS s "pozdním startem" a obrazovka se během "Loading modules" vypne, může pomoci přidat i915 a intel_agp do initramfs. Viz [KMS](#KMS_.28Kernel_Mode_Setting.29) výše.