## Contents

*   [1 Úvod](#.C3.9Avod)
*   [2 Instalace](#Instalace)
    *   [2.1 Instalace nebo obnova GRUBu na EFI oddíl (moderní UEFI zařízení)](#Instalace_nebo_obnova_GRUBu_na_EFI_odd.C3.ADl_.28modern.C3.AD_UEFI_za.C5.99.C3.ADzen.C3.AD.29)
    *   [2.2 Instalace nebo obnova GRUBu do hlavního spouštěcího záznamu (MBR)](#Instalace_nebo_obnova_GRUBu_do_hlavn.C3.ADho_spou.C5.A1t.C4.9Bc.C3.ADho_z.C3.A1znamu_.28MBR.29)
*   [3 Konfigurace](#Konfigurace)
*   [4 Kontrola](#Kontrola)
*   [5 Další zdroje](#Dal.C5.A1.C3.AD_zdroje)

## Úvod

Mezi GRUBem a GRUB2 proběhly změny v příkazech. Než budete pokračovat, můžete se s nimi chtít seznámit. Např.: "find" bylo změněno na "search".

[http://grub.enbug.org/CommandList](http://grub.enbug.org/CommandList)

## Instalace

Nejdříve nainstalujte GRUB pomocí pacmana:

```
# pacman -S grub

```

### Instalace nebo obnova GRUBu na EFI oddíl (moderní UEFI zařízení)

Ujistěte se, že je EFI systémový oddíl připojen na /boot, třeba kontrolou příkazem **mount**.

Projistotu doinstalujte efibootmgr, který GRUB použije pro konfiguraci BIOSU v režimu EFI zavádění:

```
# pacman -S efibootmgr

```

Nainstalujte Grub na EFI systémový oddíl:

```
# grub-install --target=x86_64-efi --efi-directory=/boot

```

### Instalace nebo obnova GRUBu do hlavního spouštěcího záznamu (MBR)

Tato sekce se zabývá případem, kdy máte zařízení s MBR tabulkou oddílů. Pokud jste použíli předchozí sekci pro UEFI, ignorujte tuto sekci.

GRUB může být nainstalován buď z live prostředí nebo přímo z běžící instalace Arch Linuxu.

Ve většině případů je instalace grub tak jednoduchá jako spuštění příkazu **grub-install** pod rootem:

```
# grub-install /dev/sda

```

kde /dev/sda je cíl instalace (v tomto případě MBR prvního SATA disku).

Pokud toto selže s chybou:

```
grub-probe: error: Cannot get the real path of `/dev/fd0'
Auto-detection of a filesystem module failed.
Please specify the module with the option `--modules' explicitly.

```

Zkuste do parametrů přidat `--recheck` takto:

```
# grub-install --recheck /dev/sda

```

## Konfigurace

"Starý" soubor menu.lst (používaný v Grub 1.x) je nahrazen novým souborem grub.cfg. Tento soubor se však nyní generuje automaticky ze zdrojových souborů umístěných pod /etc/grub.d/. Pokud potřebujete, udělejte změny v souborech tohoto adresáře (běžně není nutné) a vygenerujte konfiguraci:

```
# grub-mkconfig -o /boot/grub/grub.cfg

```

Po každé změně souborů v /etc/grub.d/ je potřeba znova vygenerovat konfiguraci. Výsledný konfigurační soubor bude zapsán do /boot/grub/grub.cfg.

## Kontrola

Správně nainstalovaný /boot vypadá nějak takto:

```
# tree -L 2 /boot
/boot
├── grub
│   ├── fonts
│   ├── grub.cfg
│   ├── grub.cfg.example
│   ├── grubenv
│   ├── i386-pc
│   ├── locale
│   └── themes
├── initramfs-linux-fallback.img
├── initramfs-linux.img
├── lost+found
└── vmlinuz-linux

```

## Další zdroje

*   [GRUB Homepage](http://www.gnu.org/software/grub/)
*   [GRUB wiki](http://grub.enbug.org/)