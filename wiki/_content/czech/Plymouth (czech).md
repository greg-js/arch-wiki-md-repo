## Contents

*   [1 Úvod](#.C3.9Avod)
*   [2 Instalace](#Instalace)
*   [3 Konfigurace](#Konfigurace)
*   [4 Změna tématu](#Zm.C4.9Bna_t.C3.A9matu)
*   [5 Řešení chyb](#.C5.98e.C5.A1en.C3.AD_chyb)
*   [6 Credits](#Credits)

## Úvod

[Plymouth](http://fedoraproject.org/wiki/Releases/FeatureBetterStartup) je projekt Fedory, který poskytuje bootovací obrazovku bez nepříjemného poblikávání. Pro nastavení nativního rozlišení displeje, jak nejdříve je to možné, spoléhá na KMS (kernel mode setting), poté zobrazí graficky pěkný splash screen trvající až do startu správce přihlášení.

**Note:** KMS je momentálně dostupné pro grafické karty Intel a ATI (tedy bylo tomu tak alespoň u jádra verze 2.6.31). Plymouth může fungovat i bez něj, ale je možné, že spustí méně hezký textový plugin.

**Warning:** Plymouth je momentálně velice živě vyvíjen a může obsahovat chyby.

## Instalace

Než začnete používat Plymouth, musíte povolit KMS. Následujte, prosím, instrukce [pro karty ATI](/index.php/ATI#AMD.2FAti_cards_and_KernelModeSetting_.28KMS.29 "ATI") a [pro karty Intel](/index.php/Intel#KMS_.28Kernel_Mode_Setting.29 "Intel"). Obě dvě možnosti vyžadují znovusestavení obrazu jádra. To budete muset provést i později v tomto článku, takže to prozatím můžete přeskočit.

Pokud nemáte KMS, budete místo něj potřebovat [framebuffer](/index.php/Framebuffer#Framebuffer_Resolution "Framebuffer").

**Note:** Ten nemusí fungovat dobře. Plymouth je navržený pro práci **s** KMS, přesto je schopen občas fungovat i s framebufferem.

Plymouth můžete získat z repozitáře AUR. Nejlepší je použít [git verzi](https://aur.archlinux.org/packages.php?ID=26117), je totiž nejnovější a tedy i nejlépe funkční.

Instrukce pro instalaci balíků z AURu jsou [dostupné zde](/index.php/Arch_User_Repository#Installing_packages "Arch User Repository").

## Konfigurace

Nejdříve ze všeho nastavte téma pro plymouth. Plymouth přichází s výběrem témat:

1.  Fade-in: "Jednoduché téma se slábnoucími a rozsvicujícími se mihotajícími se hvězdami"
2.  Glow: "Korporátní téma s koláčovým grafem zobrazujícím boot následované barvitým vynořujícím se logem"
3.  Solar: "Vesmírné téma s náhle se rozšiřující modrou "hvězdou"" a
4.  Spinfinty: "Jednoduché téma zobrazující rotující znak nekonečna ve středu obrazovky"

Nastavte požadované téma pomocí nástroje plymouth-set-default-theme, např:

```
$ su
# plymouth-set-default-theme spinfinity

```

Přidejte plymouth do pole `HOOKS` v souboru `mkinitcpio.conf`. **Musí** být přidán *až za* udev a autodetect, aby plymouth fungoval správně.

```
# nano /etc/mkinitcpio.conf

```

Přidejte plymouth do pole `HOOKS`:

```
HOOKS="base udev autodetect plymouth ..."

```

Sestavte znovu obraz jádra:

Pro nejnovější kernel (3.0+)

```
# mkinitcpio -p linux

```

Je třeba zkonfigurovat Grub tak, aby pracoval s Plymouth:

```
# nano /boot/grub/menu.lst

```

Pokud máte povolené KMS, odstraňte z řádky `kernel` veškeré `VGA=` záznamy. Pokud nemáte KMS, budete muset použít framebuffer a také přidat `VGA=` záznam. V obou případech přídejte na konec "quiet splash":

```
kernel /vmlinuz-linux root=/dev/disk/by-uuid/ff6e3888-b8f8-4a75-a08f-55ca30f4b330 ro quiet splash

```

Pozn: celý řáderk nekopírujte, na každém pc může být jiný , je zde uveden jen pro příklad!!! Na konci bootovacího procesu musí být Plymouth démon zastaven. Toho můžete dosáhnout tímto příkazem v `rc.local`:

```
# nano /etc/rc.local

```

a přidejte tento řádek

```
/bin/plymouth quit --retain-splash

```

Restartujte a užívejte si eye=candy start!

## Změna tématu

Jak jsem se již zmínil výše, Plymouth příchází s několika tématy. Pokud budete chtít vyzkoušet jiná, jednoduše zadejte příkaz

```
# plymouth-set-default-theme *název_téma*

```

Znovu sestavte obraz jádra: Pro nejnovější kernel (3.0+)

```
# mkinitcpio -p linux

```

A restartujte.

## Řešení chyb

Z nějakého důvodu na obou mých počítačích (notebook s grafickou kartou ATI a KMS, stolní počítač s kartou nVidia a framebufferem) příkaz pro ukončení Plymouthu zanechá v horní oblasti obrazovky malé černé čtverečky, které zastiňují okna pod nimi. Tento problém je způsoben volbou `--retain-splash`, která je potřebná pro zajištění souvislosti boot procesu, jak jen je to možné. Pokud jste zaznamenal tento problém, řešením je sestřelení Plymouthu *po* přihlášení, tehdy už není volba `--retain-splash` dále potřebná.

**Note:** To vyžaduje použití programu sudo. Instrukce pro instalaci a nastavení programu sudo můžete [nalézt zde](/index.php/Sudo "Sudo").

Upravte `/etc/rc.local` znovu a odstraňte řádek "/bin/plymouth quit --retain-splash".

Pod svým uživatelem upravte `.xinitrc` a přidejte řádek pro sestřelení Plymouthu.

**Warning:** To musí být **nad** řádkem, který startuje vaše sezení (např. `exec startxfce4`), jinak vaše desktopové sezení **nenastartuje**

```
$ nano ~/.xinitrc

```

A přidejte:

```
sudo /bin/plymouth quit &

```

Všimněte si chybějícího `--retain-splash` a přidaného znaku & na konci řádku. Je to nutné k tomu, aby xinitrc skript mohl spustit vaše desktopové sezení.

Nyní si dejte práva pro zabití Plymouth démona bez hesla, to provedete úpravou souboru `/etc/sudoers`:

```
$ su
# EDITOR=nano visudo

```

A přidejte:

```
*uzivatel*      ALL=(ALL) NOPASSWD: /bin/plymouth

```

Restartujte a vše by mělo být v pořádku.

## Credits

Díky drf za jeho [excelentní příspěvek ve fóru](https://bbs.archlinux.org/viewtopic.php?id=81406), na základě kterého je tento článek založen