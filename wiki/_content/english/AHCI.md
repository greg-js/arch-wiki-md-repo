**AHCI**, abbreviation for *a*dvanced *h*ost *c*ontroller *i*nterface, is the native work mode for SATA drives. AHCI has two main benefits: support for hot pluggable SATA drives (mimicking USB drives' behavior) and NCQ, or *n*ative *c*ommand *q*ueuing. It has been present in the Linux kernel since version 2.6.19 and will be loaded automatically in current Arch kernel.

## Configure from BIOS

If your BIOS set SATA as legacy/parallel ATA, you can access BIOS setting depends on the motherboard; usually, `Del` is used to display the menu.

Once the BIOS options are available, search for parameters resembling:

```
Enable SATA as: IDE/AHCI

```

or:

```
SATA: PATA Emulation/Native/Enhanced

```

Choose `AHCI` or `Native`, save the settings and exit the BIOS. Consult the motherboard's manual if it's not clear which of the modes is AHCI, since the naming can vary.

After altering and saving the BIOS settings, Linux should load the AHCI driver on the next boot. `dmesg`'s output should confirm this:

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

and for NCQ:

```
ata2.00: 625142448 sectors, multi 16: LBA48 NCQ (depth 31/32)

```

## See also

*   [AHCI on Wikipedia](http://en.wikipedia.org/wiki/AHCI)
*   [NCQ on Wikipedia](http://en.wikipedia.org/wiki/NCQ)