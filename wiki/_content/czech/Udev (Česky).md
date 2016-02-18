## Contents

*   [1 Úvod](#.C3.9Avod)
*   [2 O automatickém nahrávání modulů](#O_automatick.C3.A9m_nahr.C3.A1v.C3.A1n.C3.AD_modul.C5.AF)
*   [3 O pravidlech pro udev](#O_pravidlech_pro_udev)
*   [4 Řešení problémů](#.C5.98e.C5.A1en.C3.AD_probl.C3.A9m.C5.AF)
    *   [4.1 Vypínání automatického nahrávání modulů za pomoci boot parametru load_modules](#Vyp.C3.ADn.C3.A1n.C3.AD_automatick.C3.A9ho_nahr.C3.A1v.C3.A1n.C3.AD_modul.C5.AF_za_pomoci_boot_parametru_load_modules)
    *   [4.2 Zakazování modulů](#Zakazov.C3.A1n.C3.AD_modul.C5.AF)
    *   [4.3 Známé problémy s hardwarem](#Zn.C3.A1m.C3.A9_probl.C3.A9my_s_hardwarem)
        *   [4.3.1 Zařízení BusLogic mohou být rozbitá a způsobit během startu zamrznutí systému](#Za.C5.99.C3.ADzen.C3.AD_BusLogic_mohou_b.C3.BDt_rozbit.C3.A1_a_zp.C5.AFsobit_b.C4.9Bhem_startu_zamrznut.C3.AD_syst.C3.A9mu)
        *   [4.3.2 Čtečky PCMCIA karet nejsou brány jako vyměnitelná zařízení](#.C4.8Cte.C4.8Dky_PCMCIA_karet_nejsou_br.C3.A1ny_jako_vym.C4.9Bniteln.C3.A1_za.C5.99.C3.ADzen.C3.AD)
    *   [4.4 Známé problémy s automatickým nahráváním](#Zn.C3.A1m.C3.A9_probl.C3.A9my_s_automatick.C3.BDm_nahr.C3.A1v.C3.A1n.C3.ADm)
        *   [4.4.1 Moduly frekvence CPU](#Moduly_frekvence_CPU)
        *   [4.4.2 Problémy se zvukem / Některé moduly se nenahrávají automaticky](#Probl.C3.A9my_se_zvukem_.2F_N.C4.9Bkter.C3.A9_moduly_se_nenahr.C3.A1vaj.C3.AD_automaticky)
*   [5 Další zdroje](#Dal.C5.A1.C3.AD_zdroje)

## Úvod

*"udev je správce zařízení pro linuxová jádra ze série 2.6\. Jeho primární úkol je správa souborů zařízení v `/dev`. Je to následník devfs a hotplugu, což znamená, že se kromě adresáře `/dev` stará i o veškeré akce v uživatelském prostoru během přidávání a odebírání zařízení, včetně nahrávání firmware."* Zdroj: [Wikipedia](http://en.wikipedia.org/wiki/Udev)

udev nahrazuje funkcionalitu balíčků `hotplug` a `hwdetect`.

udev nahrává jaderné moduly souběžně, čímž může urychlit boot systému. Jeho nevýhoda je nicméně ta, že pokaždé nenahrává moduly v tom samém pořadí, a to může způsobovat potíže se zvukovými a síťovými kartami (pokud jich máte více). Pro podrobnosti vizte níže.

## O automatickém nahrávání modulů

udev nebude nahrávat *žádné* moduly, pokud není v souboru `/etc/rc.conf` povoleno `MOD_AUTOLOAD`. V případě, že automatické nahrávání povolené nemáte, musíte moduly nahrávat manuálně jejich vložením do seznamu `MODULES` v souboru `[rc.conf](/index.php/Rc.conf "Rc.conf")`. Výčet potřebných modulů si můžete nechat generovat příkazem `hwdetect --modules`.

## O pravidlech pro udev

Pravidla pro udev patří do `/etc/udev/rules.d/`; názvy souborů musí končit na `.rules`.

Pokud se chcete naučit psát pravidla pro udev, vizte [Writing udev rules (anglicky)](http://www.reactivated.net/writing_udev_rules.html).

Pro získání seznamu všech atributů nějakého zařízení, jenž můžete použít pro psaní pravidel:

```
# udevadm info -a -p $(udevadm info -q path -n [název zařízení])

```

Nahraďte [název zařízení] za zařízení přítomné v systému, jako např. '/dev/sda' nebo '/dev/ttyUSB0'.

Jakmile vytvoříte nová nebo upravíte stávající pravidla pro udev, můžete použít následující příkaz pro restartování systému udev. Zařízení připojitelná za běhu, jakými jsou např. USB zařízení, budete muset pravděpodobně pro uplatnění nových pravidel připojit znovu.

```
# udevadm control restart

```

## Řešení problémů

### Vypínání automatického nahrávání modulů za pomoci boot parametru load_modules

Pokud na bootovací řádek jádra přidáte `load_modules=off`, udev přeskočí veškeré automatické nahrávání. Tato možnost vám poskytuje pojistné lanko, za které můžete zatáhnout, když se něco pokazí. Pokud udev nahraje problematický modul, který způsobí zatuhnutí vašeho systému nebo něco obdobně příšerného, můžete automatické nahrávání tímto parametrem přeskočit a onen výbojný modul zakázat.

### Zakazování modulů

V ojedinělých případech se Udev může splést a nahrát špatné moduly. Tomu můžete předejít zakázáním oněch modulů. Jakmile je zakážete, Udev je už nikdy nebude nahrávat. Ani při bootu ani později, když je přijata událost připojení některého zařízení za běhu (tj. např. když zasunete do USB portu flash disk).

Abyste zakázali nějaký modul, napište před něj do pole `MODULES` v souboru `[rc.conf](/index.php/Rc.conf "Rc.conf")` výkřičník:

```
MODULES=(!moduleA !moduleB)

```

### Známé problémy s hardwarem

#### Zařízení BusLogic mohou být rozbitá a způsobit během startu zamrznutí systému

Toto je bug v jádře a zatím pro něj nebyla poskytnuta žádná oprava.

#### Čtečky PCMCIA karet nejsou brány jako vyměnitelná zařízení

Aby k nim získal backend halu pmount přístup, přidejte je do souboru `/etc/pmount.allow`.

### Známé problémy s automatickým nahráváním

#### Moduly frekvence CPU

Současná metoda detekce rozličných řadičů frekvence CPU je nevhodná, takže byla prozatím z procesu automatického nahrávání vynechána. Pokud chcete využívat škálování frekvence CPU, nahrajte příslušný modul explicitně v poli `MODULES` v souboru `[rc.conf](/index.php/Rc.conf "Rc.conf")`.

#### Problémy se zvukem / Některé moduly se nenahrávají automaticky

Někteří uživatelé našli příčinu problému ve starých záznamech v souboru `/etc/modprobe.d/modprobe.conf`. Zkuste onen soubor pročistit a zkuste to znova.

## Další zdroje

*   [Homepage Udev (anglicky)](http://www.kernel.org/pub/linux/utils/kernel/hotplug/udev.html)
*   [Úvod do Udev (anglicky)](http://www.linux.com/news/hardware/peripherals/180950-udev)
*   [Mailing listy Udev (anglicky)](http://vger.kernel.org/vger-lists.html#linux-hotplug)