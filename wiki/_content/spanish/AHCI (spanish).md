**Estado de la traducción**
Este artículo es una traducción de [AHCI](/index.php/AHCI "AHCI"), revisada por última vez el **2018-11-09**. Si advierte que la versión inglesa [ha cambiado](https://wiki.archlinux.org/index.php?title=AHCI&diff=0&oldid=553413) puede ayudar a actualizar la traducción, bien por [usted mismo](/index.php/ArchWiki:Translation_Team/Contributing_(Espa%C3%B1ol) "ArchWiki:Translation Team/Contributing (Español)") o bien avisando al [equipo de traducción](/index.php/ArchWiki:Translation_Team_(Espa%C3%B1ol) "ArchWiki:Translation Team (Español)").

[AHCI](https://en.wikipedia.org/wiki/es:AHCI "wikipedia:es:AHCI") (Advanced Host Controller Interface) es el modo de trabajo nativo para unidades SATA. AHCI tiene dos principales ventajas: compatibilidad con unidades SATA de acoplamiento activo (que simulan el comportamiento de las unidades USB) y [Native Command Queuing](https://en.wikipedia.org/wiki/es:_Native_Command_Queuing "wikipedia:es: Native Command Queuing") (NCQ). Ha estado presente en el kernel de Linux desde la versión 2.6.19 y se cargará automáticamente en el kernel actual de Arch.

## Configurarlo desde la BIOS

Si su BIOS estableció SATA como ATA heredado/paralelo, puede acceder a la configuración de BIOS dependiendo de la placa base que utilize; por lo general, se suele usar la tecla `Supr` para mostrar el menú.

Una vez que las opciones de la BIOS estén disponibles, busque parámetros que se parezcan a:

```
Enable SATA as: IDE/AHCI

```

o:

```
SATA: PATA Emulation/Native/Enhanced

```

Elija `AHCI` o `Native`, guarde la configuración y salga de la BIOS. Consulte el manual de la placa base si no está claro cuál de los modos es AHCI, ya que la denominación puede variar.

Después de modificar y guardar la configuración de la BIOS, Linux debería cargar el controlador AHCI en el próximo arranque. La salida de `dmesg` debería confirmar esto:

```
SCSI subsystem initialized
libata version 3.00 loaded.
ahci 0000:00:1f.2: version 3.0
ahci 0000:00:1f.2: PCI INT B -> GSI 19 (level, low) -> IRQ 19
ahci 0000:00:1f.2: irq 764 for MSI/MSI-X
ahci 0000:00:1f.2: AHCI 0001.0200 32 slots 6 ports 3 Gbps 0x3f impl SATA mode
ahci 0000:00:1f.2: flags: 64bit ncq sntf stag pm led clo pmp pio slum part ems 
ahci 0000:00:1f.2: setting latency timer to 64
scsi0 : ahci
scsi1 : ahci
scsi2 : ahci
scsi3 : ahci
scsi4 : ahci
scsi5 : ahci

```

y para NCQ:

```
ata2.00: 625142448 sectors, multi 16: LBA48 NCQ (depth 31/32)

```

## Solución de problemas

Es posible que el módulo AHCI no se cargue automáticamente, si la configuración SATA se cambia de IDE a AHCI después de instalar Arch. En ese caso, aparece un mensaje de error en el inicio prematuro que indica que no se encontró la partición raíz (/).

Si eso sucede, la opción de arranque `failsafe` todavía debería funcionar correctamente. Una vez iniciado en el modo a prueba de fallos, debe ejecutar [mkinitcpio](/index.php/Mkinitcpio_(Espa%C3%B1ol) "Mkinitcpio (Español)") para volver a generar una imagen de initramfs correcta.