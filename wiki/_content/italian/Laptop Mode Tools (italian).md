*[Laptop Mode Tools](http://samwel.tk/laptop_mode/) è un pacchetto per il risparmio energetico dei computer portatile per i sistemi Linux. E 'il modo principale per attivare la funzionalità Laptop Mode del kernel Linux, che consente llo spin down dei dischi rigidi. Inoltre, permette di ottimizzare una serie di altre impostazioni relative al risparmio energetico utilizzando un semplice file di configurazione.*

In combinazione con [acipd](/index.php/Acpid_(Italiano) "Acpid (Italiano)"), [CPU Frequency Scaling](/index.php/CPU_frequency_scaling_(Italiano) "CPU frequency scaling (Italiano)") e [pm-utils](/index.php/Pm-utils_(Italiano) "Pm-utils (Italiano)"), LMT fornisce alla maggior parte degli utenti una completa suite di gestione energetica del notebook.

## Contents

*   [1 Installazione](#Installazione)
*   [2 Configurazione](#Configurazione)
    *   [2.1 Hard disks](#Hard_disks)
        *   [2.1.1 Dispositivi a stato solido](#Dispositivi_a_stato_solido)
    *   [2.2 Ho un disco a stato solido ( SSD) nella mia macchina. Devo permettere una qualsiasi delle modalità relative ai dischi di laptop-mode-tools, o sono irrilevanti ?](#Ho_un_disco_a_stato_solido_.28_SSD.29_nella_mia_macchina._Devo_permettere_una_qualsiasi_delle_modalit.C3.A0_relative_ai_dischi_di_laptop-mode-tools.2C_o_sono_irrilevanti_.3F)
    *   [2.3 Frequenza della CPU](#Frequenza_della_CPU)
    *   [2.4 Dispositivi e bus](#Dispositivi_e_bus)
        *   [2.4.1 Intel SATA](#Intel_SATA)
        *   [2.4.2 Autosospensione delle porte USB](#Autosospensione_delle_porte_USB)
    *   [2.5 Schermo e grafica](#Schermo_e_grafica)
        *   [2.5.1 Luminosità LCD](#Luminosit.C3.A0_LCD)
            *   [2.5.1.1 ThinkPad T40/T42](#ThinkPad_T40.2FT42)
            *   [2.5.1.2 ThinkPad T60](#ThinkPad_T60)
        *   [2.5.2 Terminal blanking](#Terminal_blanking)
    *   [2.6 Controllo di rete](#Controllo_di_rete)
        *   [2.6.1 Ethernet](#Ethernet)
        *   [2.6.2 Wireless LAN](#Wireless_LAN)
    *   [2.7 Audio](#Audio)
        *   [2.7.1 AC97](#AC97)
        *   [2.7.2 Intel HDA](#Intel_HDA)
*   [3 Tips and tricks](#Tips_and_tricks)
    *   [3.1 Aliases](#Aliases)
    *   [3.2 lm-profiler](#lm-profiler)
    *   [3.3 Disabling](#Disabling)
*   [4 Risoluzione dei problemi](#Risoluzione_dei_problemi)
    *   [4.1 Laptop-mode-tools non rileva gli eventi](#Laptop-mode-tools_non_rileva_gli_eventi)
    *   [4.2 Con alimentazione AC Laptop-mode-tools non si disabilita](#Con_alimentazione_AC_Laptop-mode-tools_non_si_disabilita)
*   [5 Vedi anche](#Vedi_anche)

## Installazione

[laptop-mode-tools](https://aur.archlinux.org/packages/laptop-mode-tools/) può esser installato da [AUR](/index.php/AUR_(Italiano) "AUR (Italiano)")

## Configurazione

Aggiungere `laptop-mode` alla stringa `DAEMONS` in `/etc/rc.conf`:

```
DAEMONS=(...laptop-mode...)

```

Per utenti che utilizzano Systemd eseguire:

```
systemctl enable laptop-mode.service

```

La configurazione è gestita attraverso i file:

*   `/etc/laptop-mode/laptop-mode.conf` - File principale di configurazione
*   `/etc/laptop-mode/conf.d/*` che contiene decine di funzionalità specifiche per i "moduli"

Alcuni moduli possono essere esplicitamente abilitati/disabilitati tramite il cambiamento della variabile `CONTROL_*` nel file di impostazione individuale allocato in `conf.d/*`.

Se la variabile `ENABLE_AUTO_MODULES` è impostata in `/etc/laptop-mode/laptop-mode.conf`, LMT è in grado di abilitare automaticamente tutti i moduli dove `CONTROL_*` è impostato su `auto`.

Se si vuole controlla quale modulo è abilitato, disabilitato o impostato su "auto", lanciare:

 `grep -r '^\(CONTROL\|ENABLE\)_' /etc/laptop-mode/conf.d` 
**Nota:** `auto-hibernate.conf` e `battery-level-polling.conf` sono un eccezione e utilizzano una variabnile `ENABLE_*` al posto di `CONTROL_*`.

### Hard disks

Per questo funzionalità è necessaria disporre di hdparm e/o sdparm installato. Si Veda [Hdparm](/index.php/Hdparm "Hdparm").

Riducendo la velocità del disco rigido attraverso il valore `hdparm -S` viene salvaguardata la potenza, rendendo tutto molto più silenzioso. Utilizzando la funzione *readahead* è possibile consentire alle unità di riposare più spesso anche se si sta utilizzando il computer. LMT può anche stabilire il valore `hdparm -B`. Il valore massimo per il risparmio energetico di un hard disk è 1 e il minimo è 254\. Ad esempio, impostare questo valore a 254 quando si è alimentati tramite AC e 20 quando a batteria. Se ci si accorge che la normale attività dell'hard disk si blocca spesso in attesa , potrebbe essere una buona idea impostare a un valore più alto (es. 128) che metterà a riposo il disco meno spesso. I valori di `hdparm -S` e `hdparm -B` sono configurate in `/etc/laptop-mode/laptop-mode.conf`.

**Attenzione:** Abbassare lo Spinning di un disco rigido troppo spesso può accorciare la sua durata. Fate attenzione quando si sceglie un valore adeguato.

Con la variabile `CONTROL_MOUNT_OPTIONS` (di default "on"), laptop-mode-tools rimonta automaticamente le partizioni aggiungendo `commit=600,noatime` nelle opzioni di mount. Con questa opzione jbd2 accede al disco ogni pochi secondi, invece il journaling del disco viene aggiornato ogni 10 minuti (ATTENZIONE: con questa impostazione si potrebbero perdere fino a 10 minuti di lavoro).

**Attenzione:** Con questa impostazione si potrebbe perdere fino a 10 minuti di lavoro. Assicurarsi di non utilizzare l'opzione di mount `atime` , utilizzare invece `noatime` o `relatime`.

**Nota:** `CONTROL_MOUNT_OPTIONS` non deve essere abilitato con partizioni nilfs2\. Si veda la discussione sul forum [https://bbs.archlinux.org/viewtopic.php?id=134656](https://bbs.archlinux.org/viewtopic.php?id=134656) .

#### Dispositivi a stato solido

Dalle [official, upstream FAQ](http://samwel.tk/laptop_mode/faq):

### Ho un disco a stato solido ( SSD) nella mia macchina. Devo permettere una qualsiasi delle modalità relative ai dischi di laptop-mode-tools, o sono irrilevanti ?

Essi possono essere rilevanti, perché (A) una modalità laptop ridurrà il numero di scritture , che migliora la vita di un SSD, e (B) modalità portatile rende le scritture consecutive, che consente ai meccanismi un risparmio energetico come ALPM. Tuttavia, il vostro chilometraggio può variare a seconda dell'hardware specifico sostenuto. Per alcuni componenti hardware non si otterrà nessun guadagno, per alcuni il guadagno potrebbe essere sostanziale.

### Frequenza della CPU

Per gestire le frequenze della CPU è necessario aver installato il driver appropriato. Si veda [CPU Frequency Scaling](/index.php/CPU_frequency_scaling_(Italiano) "CPU frequency scaling (Italiano)").

```
# cpufreq.conf
# ThinkPad T40/T42/T60 Example
#
CONTROL_CPU_FREQUENCY=1
BATT_CPU_MAXFREQ=fastest
BATT_CPU_MINFREQ=slowest
BATT_CPU_GOVERNOR=ondemand
BATT_CPU_IGNORE_NICE_LOAD=1
LM_AC_CPU_MAXFREQ=fastest
LM_AC_CPU_MINFREQ=slowest
LM_AC_CPU_GOVERNOR=ondemand
LM_AC_CPU_IGNORE_NICE_LOAD=1
NOLM_AC_CPU_MAXFREQ=fastest
NOLM_AC_CPU_MINFREQ=slowest
NOLM_AC_CPU_GOVERNOR=ondemand
NOLM_AC_CPU_IGNORE_NICE_LOAD=0
CONTROL_CPU_THROTTLING=0

```

### Dispositivi e bus

#### Intel SATA

*   Abilitare la funzione Aggressive Link Power Management per il controller Intel SATA AHCI, per impostare il disco in una modalità di risparmio energetico molto basso, in assenza di scrittura IO del disco.

```
# intel-sata-powermgmt.conf
# ThinkPad T40/T42/T60 Example
#
DEBUG=0
CONTROL_INTEL_SATA_POWER=1
BATT_ACTIVATE_SATA_POWER=1
LM_AC_ACTIVATE_SATA_POWER=1
NOLM_AC_ACTIVATE_SATA_POWER=0

```

**Nota:** Si veda il ben documentato file `/etc/laptop-mode/conf.d/intel-sata-powermgmt.conf` per dettagliate configurazione aggiuntive.

#### Autosospensione delle porte USB

```
# usb-autosuspend.conf
# ThinkPad T40/T42/T60 Example
#
DEBUG=0
CONTROL_USB_AUTOSUSPEND=1
BATT_SUSPEND_USB=1
LM_AC_SUSPEND_USB=1
NOLM_AC_SUSPEND_USB=0
AUTOSUSPEND_TIMEOUT=2

```

**Nota:** Si veda il ben documentato file `/etc/laptop-mode/conf.d/usb-autosuspend.conf` per dettagliate configurazioni aggiuntive. Se si dispone di un dispositivo USB che si usa sempre (come un mouse USB), aggiungerle in blacklist dovrebbe permettere di fermarli dopo la sospensione.

### Schermo e grafica

#### Luminosità LCD

*   Valori di luminosità disponibili per alcuni modelli di laptop possono possono essere ottenuti eseguendo il comando seguente:

```
$ cat /proc/acpi/video/VID/LCD/brightness

```

##### ThinkPad T40/T42

Per i notebook [ThinkPad](https://en.wikipedia.org/wiki/ThinkPad "wikipedia:ThinkPad") T40/T42, il valore minimo e massimo della luminosità possono essere ottenuti con uno dei seguenti comandi:

```
$ cat /sys/class/backlight/acpi_video0/brightness
$ cat /sys/class/backlight/acpi_video0/max_brightness

```

```
# lcd-brightness.conf
# ThinkPad T40/T42 Example
#
DEBUG=0
CONTROL_BRIGHTNESS=1
BATT_BRIGHTNESS_COMMAND="echo 0"
LM_AC_BRIGHTNESS_COMMAND="echo 7"
NOLM_AC_BRIGHTNESS_COMMAND="echo 7"
BRIGHTNESS_OUTPUT="/sys/class/backlight/thinkpad_screen/brightness"

```

##### ThinkPad T60

Per i notebook [ThinkPad](https://en.wikipedia.org/wiki/ThinkPad "wikipedia:ThinkPad") T60, il valore minimo e massimo della luminosità possono essere ottenuti con uno dei seguenti comandi:

```
$ cat /sys/class/backlight/thinkpad_screen/max_brightness
$ cat /sys/class/backlight/thinkpad_screen/brightness

```

```
# lcd-brightness.conf
# ThinkPad T60 Example
#
DEBUG=0
CONTROL_BRIGHTNESS=1
BATT_BRIGHTNESS_COMMAND="echo 0"
LM_AC_BRIGHTNESS_COMMAND="echo 7"
NOLM_AC_BRIGHTNESS_COMMAND="echo 7"
BRIGHTNESS_OUTPUT="/sys/class/backlight/acpi_video0/brightness"

```

**Nota:** Si veda il ben documentato file `/etc/laptop-mode/conf.d/lcd-brightness.conf` per dettagliate configurazioni aaggiuntive.

#### Terminal blanking

```
# terminal-blanking.conf
# ThinkPad T40/T42/T60 Example
#
DEBUG=0
CONTROL_TERMINAL=1
TERMINALS="/dev/tty1"
BATT_TERMINAL_BLANK_MINUTES=1
BATT_TERMINAL_POWERDOWN_MINUTES=2
LM_AC_TERMINAL_BLANK_MINUTES=10
LM_AC_TERMINAL_POWERDOWN_MINUTES=10
NOLM_AC_TERMINAL_BLANK_MINUTES=10
NOLM_AC_TERMINAL_POWERDOWN_MINUTES=10

```

**Nota:** Si veda il ben documentato file `/etc/laptop-mode/conf.d/terminal-blanking.conf` per dettagliate configurazioni aggiuntive.

### Controllo di rete

#### Ethernet

```
# ethernet.conf
# ThinkPad T40/T42/T60 Example
#
DEBUG=0
CONTROL_ETHERNET=1
LM_AC_THROTTLE_ETHERNET=0
NOLM_AC_THROTTLE_ETHERNET=0
DISABLE_WAKEUP_ON_LAN=1
DISABLE_ETHERNET_ON_BATTERY=1
ETHERNET_DEVICES="eth0"

```

#### Wireless LAN

Il risparmio energetico delle interfacce wirelees è dipendente dal tipo di hardware, e quindi risulta più complicato da configurare. A seconda del chipset wireless, le impostazioni vengono gestite in uno dei seguenti tre file:

1.  `/etc/laptop-mode/conf.d/wireless-power.conf` per un metodo generico di risparmio energetico (con "iwconfig wlan0 power on/off"). Questo vale per la maggior parte chipset (diversamente dai chipset Intel elencati di seguito).
2.  `/etc/laptop-mode/conf.d/wireless-ipw-power.conf` per i chipset Intel chipsets funzionanti con i vecchi driver ipw. Si applicano a IPW3945, IPW2200 and IPW2100\. Attualmente (dalla versione 1.55-1 di LMT) viene utilizzato iwpriv per IPW3945, e una combinazione della impostazioni di iwconfig e iwpriv per IPW2100 w IPW220\. Si veda il file `/usr/share/laptop-mode-tools/modules/wireless-ipw-power` per maggiori dettagli. (si noti che ipw3945 non è più utilizzato, si veda di seguito)
3.  `/etc/laptop-mode/conf.d/wireless-iwl-power.conf` per i chipset Intel che utilizzano i moduli iwl4965, iwl3945 e iwlagn (quest'ultimo supporta i chipsets 4965, 5100, 5300, 5350, 5150, 1000, e 6000)

Si noti che l'attivazione del tre di loro non dovrebbe essere un gran problema, dal momento che LMT rileva il modulo utilizzato dall'interfaccia e agisce di conseguenza.

I moduli supportati per ogni file di configurazione, sopra indicati, sono presi direttamente da LMT. Tuttavia, questo sembra essere un po datata come soluzione, dal momento che dal kernel 2.6.34 non vengono più forniti i moduli la ipw3945 e iwl4965 (i chipset invece del modulo 3945 utilizzano iwl3945, mentre 4965 utilizza il modulo generico iwlagn). Questo dato viene riportato solo a titolo informativo, in quanto non (o non dovrebbe) influenzare il corretto funzionamento di LMT.

C'è un problema noto con alcuni chipset in esecuzione con il modulo iwlagn (cioè il chipset 5300, e forse altri). Per questi chipset, le seguenti impostazioni di `/etc/laptop-mode/conf.d/wireless-iwl-power.conf` :

```
IWL_AC_POWER
IWL_BATT_POWER

```

sono ignorati, perché il file `/sys/class/net/wlan*/device/power_level` non esiste. Invece, il metodo standard (con "iwconfig wlan0 power on / off") viene utilizzato automaticamente.

### Audio

#### AC97

```
# ac97-powersave.conf
# ThinkPad T40/T42/T60 Example
#
DEBUG=0
CONTROL_AC97_POWER=1

```

#### Intel HDA

```
# intel-hda-powersave.conf
# ThinkPad T40/T42/T60 Example
#
DEBUG=0
CONTROL_INTEL_HDA_POWER=1
BATT_INTEL_HDA_POWERSAVE=1
LM_AC_INTEL_HDA_POWERSAVE=1
NOLM_AC_INTEL_HDA_POWERSAVE=0
INTEL_HDA_DEVICE_TIMEOUT=10
INTEL_HDA_DEVICE_CONTROLLER=0

```

## Tips and tricks

### Aliases

### lm-profiler

### Disabling

## Risoluzione dei problemi

### Laptop-mode-tools non rileva gli eventi

Installare [acpid](https://www.archlinux.org/packages/?name=acpid) e attivare il proprio servizio `acpid.service` tramite [systemd](/index.php/Systemd_(Italiano) "Systemd (Italiano)").

Se questo non risolve il problema, passare attraverso il file di configurazione di lapotop-mode e fare in modo che il servizio che si desidera attivare sia impostato a 1\. Molti servizi (compreso il controllo cpufreq) di default è impostata su "auto", che potrebbe non abilitarli.

Alcuni problemi con il bluetooth non funzionante con avvio da batteria, possono essere corretti con la disattivazione di runtime-pm.

### Con alimentazione AC Laptop-mode-tools non si disabilita

Ciò è possibile se si dispone sia di laptop-mode-tools che di pm-utils installato, poichè possono entrare in conflitto tra di loro, con la conseguenza che laptop-mode-tools non riesca ad impostare correttamente il suo stato.

Questo può essere risolto disattivando gli script con funzionalità duplicate in pm-utils. La causa principale di questo problema particolare è che gli script di laptop-mode si trovano in `/usr/lib/pm-utils/power.d`. È possibile interrompere qualsiasi hook indesiderato e in esecuzione creando un file fittizio in `/etc/pm/power.d` con lo stesso nome dell'hook corrispondente in `/usr/lib/pm-tils/power.d`. Per esempio, se si desidera disattivare l'hook laptop-mode:

```
 # touch /etc/pm/power.d/laptop.mode

```

Nota : Non si imposti il bit di esecuzione su questo hook fittizio.

Si consiglia di disattivare qualsiasi hook con funzionalità equivalente in LMT.

## Vedi anche

*   [Laptop Mode Tools](http://samwel.tk/laptop_mode/)
*   [Mailing List Archives](http://mailman.samwel.tk/pipermail/laptop-mode/)