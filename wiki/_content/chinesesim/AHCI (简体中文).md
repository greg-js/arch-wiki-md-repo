**AHCI**, *A*dvanced *H*ost *C*ontroller *I*nterface 的缩写，意思是 高级主机控制器接口, 这是一种SATA设备特有的工作模式.通常AHCI需要通过BIOS来开启或关闭，通过BIOS启用AHCI有两大好处：热插拔SATA驱动器（模拟USB驱动器的行为）和NCQ。该特性在 Linux kernel 2.6.19 以后开始提供支持,现在的 Arch 内核会自动加载 ahci 模块.

## 设置BIOS

进入BIOS的方法因主板的不同而不通; 通常, 在启动计算机时按`Del` 就可以进入BIOS，笔记本可能是`F2`。

进入BIOS之后, 找到跟下面类似的选项:

```
Enable SATA as: IDE/AHCI

```

或者:

```
SATA: PATA Emulation/Native/Enhanced

```

选择 `AHCI` 或 `Native`， 保存并退出 BIOS. 如果你没有找到对应的选项请参考主板说明书，因为选项的名字可能不一样。

BIOS修改完之后， Linux 下次启动将会加载 AHCI 驱动。 通过 `dmesg` 命令的输出可以确定是否正常加载:

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

## Pitfalls

*   Windows XP does not have stock AHCI drivers. A user with SATA drives wishing to enable AHCI mode and dual-boot into Windows XP will need AHCI drivers for their motherboard. This issue does not affect Windows Vista onwards.

## 参阅

*   [AHCI on Wikipedia](http://en.wikipedia.org/wiki/AHCI)
*   [NCQ on Wikipedia](http://en.wikipedia.org/wiki/NCQ)