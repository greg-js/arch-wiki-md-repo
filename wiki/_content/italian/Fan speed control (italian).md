Controllare la velocità (e il rumore!) della ventola della CPU è facile!

**Warning:** Ciò che segue potrebbe danneggiare il proprio hardware. La ventola della CPU serve per raffreddarla e in questa guida verrà spenta per un paio di secondi. Se non si è preparati a questo, non farlo!

## Contents

*   [1 lm-sensors](#lm-sensors)
    *   [1.1 Incrementare fan_div](#Incrementare_fan_div)
*   [2 pwmconfig](#pwmconfig)
    *   [2.1 Ottimizzazioni](#Ottimizzazioni)
*   [3 fancontrol](#fancontrol)
*   [4 Semplice script Bash per regolazione fine delle ventole](#Semplice_script_Bash_per_regolazione_fine_delle_ventole)

### lm-sensors

Per prima cosa, bisogna configurare [lm_sensors](/index.php/Lm_sensors "Lm sensors").

Una volta installato [lm_sensors](https://www.archlinux.org/packages/?name=lm_sensors), si possono ottenere delle letture con il comando `sensors`.

```
$ sensors
coretemp-isa-0000
Adapter: ISA adapter
Core 0:      +29.0°C  (high = +76.0°C, crit = +100.0°C)  

coretemp-isa-0001
Adapter: ISA adapter
Core 1:      +29.0°C  (high = +76.0°C, crit = +100.0°C)  

coretemp-isa-0002
Adapter: ISA adapter
Core 2:      +31.0°C  (high = +76.0°C, crit = +100.0°C)  

coretemp-isa-0003
Adapter: ISA adapter
Core 3:      +29.0°C  (high = +76.0°C, crit = +100.0°C)  

it8718-isa-0290
Adapter: ISA adapter
Vcc:         +1.14 V  (min =  +0.00 V, max =  +4.08 V)   
VTT:         +2.08 V  (min =  +0.00 V, max =  +4.08 V)   
+3.3V:       +3.33 V  (min =  +0.00 V, max =  +4.08 V)   
NB Vcore:    +0.03 V  (min =  +0.00 V, max =  +4.08 V)   
VDRAM:       +2.13 V  (min =  +0.00 V, max =  +4.08 V)   
fan1:        690 RPM  (min =   10 RPM)
temp1:       +37.5°C  (low  = +129.5°C, high = +129.5°C)  sensor = thermistor
temp2:       +25.0°C  (low  = +127.0°C, high = +127.0°C)  sensor = thermal diode
```

Se nell'output non viene visualizzato il valore RPM per la ventola della CPU, ma si è sicuri che sia in esecuzione, è necessario aumentare il divisore della ventola. Se la velocità della ventola viene mostrata ed è superiore a 0, ignorare il passaggio successivo.

#### Incrementare fan_div

La prima riga emessa nell'output dei sensori è il chipset usato dalla scheda madre per leggere le velocità, temperature e voltaggi.

Creare il file di configurazione `libsensors` copiando il file di default in `/etc/sensors.d/`.

```
# cp /etc/sensors3.conf /etc/sensors.d/sensors.conf

```

Ora editare `/etc/sensors.d/sensors.conf` e cercare il chipset esatto. Alcuni nomi di chipset sono simili, quindi assicurarsi che quello che si sta modificando è il proprio. Aggiungere la riga `set fanX_div 4` vicino l'inizio della propria configurazione chipset, sostituendo X con il numero corrispondente di ventole della CPU.

Salvare ed eseguire:

```
# sensors -s

```

che ricaricherà le variabili impostate in `sensors.conf`. Eseguire `sensors` di nuovo e verificare se c'è una lettura RPM. In caso contrario, aumentare il divisore a 8, 16 o 32.

### pwmconfig

**Nota:** Gli utenti più smaliziati preferiranno magari saltare questa sezione e scrivere `/etc/fancontrol` da soli, risparmiandosi in questo modo di dover ascoltare le ventole a tutta velocità

Una volta configurato `lm sensor` correttamente, eseguire `pwmconfig` per testare e configurare il controllo della velocità delle ventole.

Seguire le istruzioni di `pwmconfig` per impostare una velocità di base.

Le opzioni di configurazione di default dovrebbero creare un nuovo file, `/etc/fancontrol`.

#### Ottimizzazioni

**Warning:** Alcune delle fasi descritte di seguito descrivono come modificare la velocità delle ventole. Prima di fare questo assicurarsi di avere un basso carico della CPU ed essere sicuri di volerlo fare. Se in qualsiasi momento durante i seguenti passaggi si nota la temperatura della CPU salire drammaticamente, fare un `echo "255" > /sys/class/hwmon/hwmon0/device/pwm1` per far girare la ventola a tutta velocità ed ottenere un raffreddamento completo in sicurezza. In sostanza, si dovrebbe sapere cosa si sta facendo prima di giocherellare con il file di configurazione.

**Nota:** Su numerosi sistemi, lo script incluso può segnalare errori in quanto cerca di calibrare la ventola al PWM. Si possono tranquillamente ignorare questi errori. Il problema è che lo script non aspetta abbastanza a lungo prima di scalare su o giù il PWM.

Se si desidera un maggiore controllo, si avrà probabilmente bisogno di modificare la configurazione generata. Ecco un file di configurazione d'esempio:

```
INTERVAL=10
DEVPATH=hwmon0=devices/platform/coretemp.0 hwmon2=devices/platform/w83627ehf.656
DEVNAME=hwmon0=coretemp hwmon2=w83627dhg
FCTEMPS=hwmon0/device/pwm1=hwmon0/device/temp1_input
FCFANS= hwmon0/device/pwm1=hwmon0/device/fan1_input
MINTEMP=hwmon0/device/pwm1=20
MAXTEMP=hwmon0/device/pwm1=55
MINSTART=hwmon0/device/pwm1=150
MINSTOP=hwmon0/device/pwm1=105
```

*   **INTERVAL**: quante volte il demone dovrebbe sondare le temperature della cpu e regolare la velocità delle ventole. L'intervallo è espresso in secondi.

Il resto del file di configurazione è diviso in (almeno) due valori per ogni opzione di configurazione. Ogni opzione di configurazione punta prima ad un dispositivo PWM con le istruzioni per impostare la velocità della ventola. Il secondo "campo" è il valore effettivo da impostare. Ciò consente di monitorare e controllare ventole multiple e temperature (se il pc lo supporta).

*   **FCTEMPS**: Il dispositivo di input della temperatura da leggere per la temperatura della CPU. L'esempio sopra riportato corrisponde a `/sys/class/hwmon/hwmon0/device/temp1_input`.
*   **FCFANS**: La velocità della ventola attuale, che può essere letto (come la temperatura) in `/sys/class/hwmon/hwmon0/device/fan1_input`
*   **MINTEMP**: La temperatura (°C) alla quale **SPEGNERE** la ventola della cpu. Le CPU efficienti non hanno normalmente bisogno di ventilazione mentre sono al minimo. Assicurarsi di impostare questo ad una temperatura di sicurezza *conosciuta*. Impostare questo valore a 0 non è consigliato, utilizzare un valore più sicuro.
*   **MAXTEMP**: La temperatura (°C) alla quale far girare la ventola alla *MASSIMA* velocità. Questo dovrebbe essere impostato, forse 10 o 20 gradi (°C) al di sotto della temperatura critica di spegnimento della CPU. Impostarla troppo vicina alla MINTEMP si tradurrà in superiore velocità generale della ventola.
*   **MINSTOP**: Il valore di PWM con cui il ventilatore si ferma. Ogni ventola è un po' diversa. Gli utenti esperti possono impostare valori differenti (tra 0 e 255) a `/sys/class/hwmon/hwmon0/device/pwm1` e poi monitorare la ventola della CPU. Quando si ferma, utilizzare quel valore.
*   **MINSTART**: Il valore di PWM con cui il ventilatore inizia a girare di nuovo. Questo è spesso un valore superiore a MINSTOP dal momento che è richiesto un maggiore voltaggio per superare l'inerzia.

Ci sono anche altre due impostazioni necessarie a fancontrol per verificare che il file di configurazione è ancora aggiornato. Le righe iniziano con il nome dell'impostazione e un segno di uguaglianza, seguiti dai gruppi di "hwmon-class-device=setting", separati da spazi. È necessario specificare ogni impostazione per ogni dispositivo di classe `hwmon` in uso in qualsiasi parte della configurazione, o `fancontrol` non funzionerà.

*   **DEVPATH**: Consente di impostare il dispositivo fisico. È possibile determinare questo eseguendo il comando

```
readlink -f /sys/class/hwmon/<hwmon-device>/device | sed -e 's/^\/sys\///'

```

*   **DEVNAME**: Imposta il nome del dispositivo. Provare con

```
cat /sys/class/hwmon/<hwmon-device>/device/name | sed -e 's/[[:space:]=]/_/g'

```

### fancontrol

Provare ad eseguire `fancontrol`:

```
/usr/sbin/fancontrol

```

Dovrebbe avviarsi e probabilmente si sentirà rallentare la ventola della CPU.

Se tutto funziona correttamente, per ottenere l'avvio al boot basta aggiungere `fancontrol` a DAEMONS in `/etc/rc.conf`, dato che uno script init per `fancontrol` è ora fornito di default!

*La maggior parte di questi howto è tratta da [[Forum di ubuntu](http://ubuntuforums.org/)] e dalla [[Guida di ubuntu](http://ubuntuguide.org/)].*

**Note:** Per i portatili Dell Latitude/Inspiron, si consiglia di utilizzare [i8kutils](https://aur.archlinux.org/packages/i8kutils/)/[i8kmonitor](https://aur.archlinux.org/packages/i8kmonitor/). Tenere conto che questi due pacchetti non funzionano su Ispiron 1764

### Semplice script Bash per regolazione fine delle ventole

Esegui questo come root per fare in modo che diversi valori pwm si convertano in RPM. Come si può vedere, questo script presuppone che "fancontrol" sia in esecuzione e lo disabilita automaticamente, per poi riattivarlo quando si ha terminato.

```
#!/bin/bash
clear

#################################################
# change the following lines to match your system
#################################################
pwmcontrol=/sys/class/hwmon/hwmon4/device/pwm1
fanrpmread=/sys/class/hwmon/hwmon4/device/fan1_input

# do not edit below this line
#################################################
log=`pwd`/fandata.log
echo "PWM,RPM" > $log

echo "This script will set your PWM to values from full power down to 0 decreasing in"
echo "approx 5 % steps and pausing 10 sec between steps to allow the fan RPM to catch"
echo "up to the new settings.  Data are logged to ${log}"
echo "which can be used to generate a graph or use as-is."

collectdata() {
array=( 255 242 230 217 204 191 178 165 152 139 126 113 100 87 74 48 22 0 )
for item in ${array[*]}
do
echo $item > $pwmcontrol
sleep 10s
rpm=`cat ${fanrpmread}`
echo $item,$rpm >> $log
echo "PWM: ${item} RPM: ${rpm}"
done
}

/etc/rc.d/fancontrol stop
echo "1" > ${pwmcontrol}_enable

collectdata

echo "0" > ${pwmcontrol}_enable
/etc/rc.d/fancontrol start
```