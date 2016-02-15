## Contents

*   [1 Úvod](#.C3.9Avod)
*   [2 Potřebný software](#Pot.C5.99ebn.C3.BD_software)
*   [3 Konfigurace](#Konfigurace)
*   [4 Hledání bluetooth adresy vaší myši](#Hled.C3.A1n.C3.AD_bluetooth_adresy_va.C5.A1.C3.AD_my.C5.A1i)
*   [5 Kernel moduly](#Kernel_moduly)
*   [6 Připojení myši](#P.C5.99ipojen.C3.AD_my.C5.A1i)
*   [7 Připojení myši při startu počítače](#P.C5.99ipojen.C3.AD_my.C5.A1i_p.C5.99i_startu_po.C4.8D.C3.ADta.C4.8De)
*   [8 Řešení problémů](#.C5.98e.C5.A1en.C3.AD_probl.C3.A9m.C5.AF)

## Úvod

Tento článek popisuje, jak nastavit bluetooth myš na Archlinuxu. Použil jsem USB klíčenku Logitech v270 Trendnet TBW-101UB, ale tento postup by měl být stejný i pro klíčenky od jiných výrobců.

## Potřebný software

Nainstalujte balíčky [bluez-utils](https://www.archlinux.org/packages/?name=bluez-utils) a [bluez-libs](https://www.archlinux.org/packages/?name=bluez-libs) z repozitáře `[extra]`.

## Konfigurace

Dále byste měli v `/etc/conf.d/bluetooth` nastavit

```
HCID_ENABLE=true
HIDD_ENABLE=true

```

a poté nastartovat službu bluetooth pomocí

```
# /etc/rc.d/bluetooth start

```

## Hledání bluetooth adresy vaší myši

Adresa bude zápsána v hexadecimálním kódu. Měli byste ji najít v dokumentaci k vaší myšce, nebo ji vyhledejte pomocí příkazu **hcitool scan**.

## Kernel moduly

Příkazem

```
# modprobe -v hci_usb bluetooth hidp l2cap

```

nahrajete potřebné moduly do jádra, pokud nebyly načteny automaticky.

## Připojení myši

```
hidd --search
hcitool inq

```

jsou dobré pro hledání bluetooth zařízení.

```
hidd --connect <bdaddr>

```

pro připojení zařízení.

```
hidd --show

```

vám ukáže aktuálně připojená zařízení. Vaše myš by se měla objevit ve výpisu. Jestliže ne, stiskněte tlačítko reset, aby se zařízení ukázalo.

**Pozn.:** Jestliže máte načtený modul ipw3945If (pro wifi na počítačích od HP), bluetooth nebude fungovat.

## Připojení myši při startu počítače

Upravte `/etc/conf.d/bluetooth`:

```
# Arguments to hidd
HIDD_OPTIONS="--connect <Sem vložte adresu své bluetooth myši (**bez velkých písmen**)>"

```

a otestuje funkčnost nového nastavení:

```
/etc/rc.d/bluetooth stop
hidd --killall (zničení aktivního spojení s myší)
/etc/rc.d/bluetooth start

```

**Pozn.:** Instrukce pro start myši při startu počítače, které jsou uvedeny výše, nefungují s prácě prošlými 3.11 bluetooth balíčky. Nové verze jako nynější (3.32) balíčky nejsou ovlivněny. Pokud používáte starší verzi, přidejte pro spuštění myši při start-upu

```
hidd --connect <Sem vložte adresu své bluetooth myši (**bez velkých písmen**)>

```

do souboru `/etc/rc.local`.

**Pozn. #2:** Můžete připojit bluetooth myš či klávesnici bez další konfigurace a bez toho, že byste znali adresu zařízení. Uděláte to přidáním parametru `--master` a/nebo `--server` v HIDD_OPTIONS.

## Řešení problémů

Jestliže máte problémy se svou USB klíčenkou, měli byste zkusit

```
# modprobe -v rfcomm

```

V tomto případě, byste měli vidět zařízení hci0 pomocí příkazu

```
# hcitool dev

```

Občas se stává, že zařízení není aktivní. Proto ho zkuste zapnout příkazem

```
# hciconfig hci0 up

```

a zkuste vyhledat vaše bluetooth zařízení.