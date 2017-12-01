**KVM**（Kernel-based Virtual Machine的縮寫）是於Linux內核內建的虛擬機。有點類似於 [Xen](/index.php/Xen "Xen") ，但更追求更簡單的運作，比如執行此虛擬機器，只需要載入相應的 `kvm` 模組即可後台待命。和 [Xen](/index.php/Xen "Xen") 的半虛擬不同的是，KVM 需要電腦支援虛擬化技術（Intel的 VT 扩展或者 AMD 的 AMD-V 擴充）。Xen的全虛擬化仍然要求電腦支援虛擬化技術。

在KVM中，可以執行各種未更改的GNU/Linux, Windows 或任何其他系統鏡像。(請看[[1]](http://www.linux-kvm.org/page/Guest_Support_Status))，每個虛擬機器都可提供獨享的虛擬硬體：網路卡，硬碟，顯卡等。请看 [KVM Howto](http://www.linux-kvm.org/page/HOWTO)

KVM, Xen, VMware, 和 QEMU 的不同之處，請看此處[KVM FAQ](http://www.linux-kvm.org/page/FAQ#What_is_the_difference_between_kvm_and_Xen.3F).

## Contents

*   [1 檢查您的電腦是否支援KVM](#.E6.AA.A2.E6.9F.A5.E6.82.A8.E7.9A.84.E9.9B.BB.E8.85.A6.E6.98.AF.E5.90.A6.E6.94.AF.E6.8F.B4KVM)
    *   [1.1 硬體支援](#.E7.A1.AC.E9.AB.94.E6.94.AF.E6.8F.B4)
    *   [1.2 內核支援](#.E5.85.A7.E6.A0.B8.E6.94.AF.E6.8F.B4)
    *   [1.3 KVM模組](#KVM.E6.A8.A1.E7.B5.84)
*   [2 Para-virtualized devices](#Para-virtualized_devices)
    *   [2.1 VirtIO modules](#VirtIO_modules)
    *   [2.2 Loading kernel modules](#Loading_kernel_modules)
    *   [2.3 List of para-virtualized devices](#List_of_para-virtualized_devices)
*   [3 如何使用KVM](#.E5.A6.82.E4.BD.95.E4.BD.BF.E7.94.A8KVM)
*   [4 小貼士与小技巧](#.E5.B0.8F.E8.B2.BC.E5.A3.AB.E4.B8.8E.E5.B0.8F.E6.8A.80.E5.B7.A7)
    *   [4.1 嵌套虛擬化](#.E5.B5.8C.E5.A5.97.E8.99.9B.E6.93.AC.E5.8C.96)

## 檢查您的電腦是否支援KVM

### 硬體支援

KVM需要宿主（host）機的處理器支援虛擬化（對於Intel CPU來說是VT-x，對於AMD CPU來說是AMD-V）。你可以通過[lscpu](/index.php?title=Lscpu&action=edit&redlink=1 "Lscpu (page does not exist)")命令來檢查你的CPU是否支援虛擬化：

```
$ lscpu

```

如果你的CPU支援虛擬化，輸出結果中會有一行Virtualization的諮詢。

你也可以執行：

```
$ grep -E "(vmx|svm)" --color=always /proc/cpuinfo

```

如果執行後沒有結果，那麼你的CPU**不**支援硬體虛擬化，你**不能**使用KVM。

**注意:** 您可能需要在BIOS中啟用虛擬化支援

### 內核支援

Arch Linux的內核提供了相應的[內核模組](/index.php/Kernel_modules "Kernel modules")來支援KVM和VirtIO。

### KVM模組

如果你的內核是用 CONFIG_IKCONFIG_PROC 這個選項編譯的話，你可以通過以下命令檢查你的內核是否已經包含了支援KVM所必須的模組（`kvm`及`kvm_amd`与`kvm_intel`這両者中的任意一個）：

```
$ zgrep KVM /proc/config.gz

```

如果模組設定不等於 `y`或`m`，則該模組**不**可用

## Para-virtualized devices

Para-virtualization provides a fast and efficient means of communication for guests to use devices on the host machine. KVM provides para-virtualized devices to virtual machines using the Virtio API as a layer between the hypervisor and guest.

All virtio devices have two parts: the host device and the guest driver.

### VirtIO modules

Use the following command to check if needed modules are available:

```
$ zgrep VIRTIO /proc/config.gz

```

### Loading kernel modules

First, check if the kernel modules are automatically loaded. This should be the case with recent versions of [udev](/index.php/Udev "Udev").

```
$ lsmod | grep kvm
$ lsmod | grep virtio

```

In case the above commands return nothing, you need to [load](/index.php/Kernel_modules#Loading "Kernel modules") kernel modules.

**Tip:** If modprobing `kvm_intel` or `kvm_amd` fails but modprobing `kvm` succeeds, (and `lscpu` claims that hardware acceleration is supported), check your BIOS settings. Some vendors (especially laptop vendors) disable these processor extensions by default. To determine whether there's no hardware support or there is but the extensions are disabled in BIOS, the output from `dmesg` after having failed to modprobe will tell.

### List of para-virtualized devices

*   network device (virtio-net)
*   block device (virtio-blk)
*   controller device (virtio-scsi)
*   serial device (virtio-serial)
*   balloon device (virtio-balloon)

## 如何使用KVM

必須使用[QEMU](/index.php/QEMU "QEMU")或[Libvirt](/index.php/Libvirt "Libvirt")作為KVM的控制界面和前端，請參考[Libvirt (正體中文)](/index.php/Libvirt_(%E6%AD%A3%E9%AB%94%E4%B8%AD%E6%96%87) "Libvirt (正體中文)")條目和[QEMU](/index.php/QEMU "QEMU")條目。

## 小貼士与小技巧

**注意:** 請參考[QEMU#Tips and tricks](/index.php/QEMU#Tips_and_tricks "QEMU")和[QEMU#Troubleshooting](/index.php/QEMU#Troubleshooting "QEMU")詞條。

### 嵌套虛擬化

在宿主機啟用`kvm_intel`模組的嵌套虛擬化機能：

```
# modprobe -r kvm_intel
# modprobe kvm_intel nested=1

```

使嵌套虛擬化永久生效（請參考[Kernel modules#Setting module options](/index.php/Kernel_modules#Setting_module_options "Kernel modules")）：

 `/etc/modprobe.d/modprobe.conf` 
```
options kvm_intel nested=1

```

檢驗嵌套虛擬化功能是否已被激活：

 `$ systool -m kvm_intel -v | grep nested` 
```
    nested              = "Y"

```

使用以下命令來執行guest虛擬機器：

```
$ qemu-system-x86_64 -enable-kvm -cpu host

```

啟動虛擬機並檢查是否有vmx標誌：

```
$ grep vmx /proc/cpuinfo

```