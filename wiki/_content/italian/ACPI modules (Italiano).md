## Contents

*   [1 Sommario](#Sommario)
*   [2 Quali sono i moduli disponibili?](#Quali_sono_i_moduli_disponibili.3F)
*   [3 Come scegliere i moduli corretti](#Come_scegliere_i_moduli_corretti)
*   [4 Aggiornamento dalla versione 2.6.24](#Aggiornamento_dalla_versione_2.6.24)
*   [5 Risoluzione dei problemi](#Risoluzione_dei_problemi)
    *   [5.1 DSDT fix](#DSDT_fix)

## Sommario

A partire dalla versione 2.6.20.7 del kernel, i moduli ACPI sono tutti modularizzati per prevenire i problemi che si incontravano su alcune macchine.

Quella che segue è una lista dei moduli ACPI che abilitano funzioni speciali o aggiungono informazioni a `/proc`, e possono essere richiamate con `acpid`.

## Quali sono i moduli disponibili?

*   ac (stato dell'alimentazione) => caricato automaticamente dal boot initscripts-0.8-7
*   asus-laptop (utile sui laptop ASUS/medion)
*   battery (stato della batteria) => caricato automaticamente dal boot initscripts-0.8-7
*   bay (bay status)
*   button (riconosce la pressione di pulsanti come LID o POWER BUTTON) => caricato automaticamente dal boot initscripts-0.8-7
*   container (stato del container)
*   dock (stato della docking station)
*   fan (stato della ventola) => caricato automaticamente dal boot initscripts-0.8-7
*   i2c_ec (driver EC SMBUs)
*   ibm_acpi (utile sui laptop IBM) (thinkpad_acpi a partire dalla versione 2.6.22)
*   processor (stato del processore) => presente nel kernel dalla versione 2.6.20.7-2
*   sbs (smart battery status, stato della batteria "intelligente")
*   thermal (stato dei sensori termici) => presente nel kernel dalla versione 2.6.20.7-2
*   toshiba_acpi (utile per i laptop Toshiba)
*   video (stato dei dispositivi video)

lista completa per il kernel in uso:

 `# ls -l /lib/modules/$(uname -r)/kernel/drivers/acpi` 

```
total 112
-rw-r--r-- 1 root root  2808 Aug 29 23:58 ac.ko.gz
-rw-r--r-- 1 root root  3021 Aug 29 23:58 acpi_ipmi.ko.gz
-rw-r--r-- 1 root root  3354 Aug 29 23:58 acpi_memhotplug.ko.gz
-rw-r--r-- 1 root root  4628 Aug 29 23:58 acpi_pad.ko.gz
drwxr-xr-x 2 root root  4096 Aug 29 23:59 apei
-rw-r--r-- 1 root root  7120 Aug 29 23:58 battery.ko.gz
-rw-r--r-- 1 root root  3700 Aug 29 23:58 button.ko.gz
-rw-r--r-- 1 root root  2181 Aug 29 23:58 container.ko.gz
-rw-r--r-- 1 root root  1525 Aug 29 23:58 custom_method.ko.gz
-rw-r--r-- 1 root root  1909 Aug 29 23:58 ec_sys.ko.gz
-rw-r--r-- 1 root root  2001 Aug 29 23:58 fan.ko.gz
-rw-r--r-- 1 root root  1532 Aug 29 23:58 hed.ko.gz
-rw-r--r-- 1 root root  3241 Aug 29 23:58 pci_slot.ko.gz
-rw-r--r-- 1 root root 17742 Aug 29 23:58 processor.ko.gz
-rw-r--r-- 1 root root  3073 Aug 29 23:58 sbshc.ko.gz
-rw-r--r-- 1 root root  7098 Aug 29 23:58 sbs.ko.gz
-rw-r--r-- 1 root root  6311 Aug 29 23:58 thermal.ko.gz
-rw-r--r-- 1 root root  8891 Aug 29 23:58 video.ko.gz

```

## Come scegliere i moduli corretti

È necessario provare autonomamente quali moduli funzionano per la propria macchina, caricandoli con

 `# modprobe <yourmodule>` 

e quindi controllando se il modulo è supportato usando

 `$ dmesg` 
**Suggerimento:** Potrebbe essere utile filtrare i risultati con il comando grep.

```
[blue@wanders ~]$ dmesg | grep acpi
[    0.000000] ACPI: LAPIC (acpi_id[0x00] lapic_id[0x00] enabled)
[    0.000000] ACPI: LAPIC (acpi_id[0x01] lapic_id[0x04] enabled)
[    0.000000] ACPI: LAPIC (acpi_id[0x02] lapic_id[0x01] enabled)
[    0.000000] ACPI: LAPIC (acpi_id[0x03] lapic_id[0x05] enabled)
[    0.000000] ACPI: LAPIC_NMI (acpi_id[0x00] high edge lint[0x1])
[    0.000000] ACPI: LAPIC_NMI (acpi_id[0x01] high edge lint[0x1])
[    0.000000] ACPI: LAPIC_NMI (acpi_id[0x02] high edge lint[0x1])
[    0.000000] ACPI: LAPIC_NMI (acpi_id[0x03] high edge lint[0x1])
[    5.066752] ACPI: acpi_idle yielding to intel_idle
[    5.438998] acpi device:04: registered as cooling_device4

```

Per caricare i moduli funzionanti basta aggiungerli all'array MODULES=() in `/etc/rc.conf`

Su tutti i laptop i seguenti moduli dovrebbero funzionare:

*   ac
*   battery
*   button
*   fan

Sui desktop computer e i server dovrebbe funzionare:

*   button

## Aggiornamento dalla versione 2.6.24

`/proc` è sconsigliato, le informazioni sono disponibili in sysfs. Ad esempio per la batteria:

```
/sys/class/power_supply/BAT0/

```

## Risoluzione dei problemi

### DSDT fix

Se i problemi con la gestione dell'alimentazione continuano pur avendo caricato i moduli corretti, la causa potrebbe essere una DSDT non completamente compatibile con Linux. Per ulteriori informazioni fare riferimento a [DSDT](/index.php/DSDT "DSDT").