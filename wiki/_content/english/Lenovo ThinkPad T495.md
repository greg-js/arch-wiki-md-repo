Related articles

*   [Lenovo ThinkPad T490](/index.php/Lenovo_ThinkPad_T490 "Lenovo ThinkPad T490")
*   [Lenovo ThinkPad T490s](/index.php?title=Lenovo_ThinkPad_T490s&action=edit&redlink=1 "Lenovo ThinkPad T490s (page does not exist)")
*   [Lenovo ThinkPad T480](/index.php/Lenovo_ThinkPad_T480 "Lenovo ThinkPad T480")
*   [Lenovo ThinkPad T480s](/index.php/Lenovo_ThinkPad_T480s "Lenovo ThinkPad T480s")
*   [Lenovo ThinkPad T470](/index.php/Lenovo_ThinkPad_T470 "Lenovo ThinkPad T470")
*   [Lenovo ThinkPad T495s](/index.php/Lenovo_ThinkPad_T495s "Lenovo ThinkPad T495s")

| **Device** | **Status** |
| [AMDGPU](/index.php/AMDGPU "AMDGPU") | Yes |
| [Wireless](/index.php/Wireless "Wireless") | Yes |
| [ALSA](/index.php/ALSA "ALSA") | Yes |
| [TrackPoint](/index.php/TrackPoint "TrackPoint") | Yes |
| [Touchpad](/index.php/Touchpad "Touchpad") | Yes |
| [Webcam](/index.php/Webcam "Webcam") | Yes |
| [Bluetooth](/index.php/Bluetooth "Bluetooth") | Yes |
| [Mobile internet](/index.php/ThinkPad_mobile_Internet "ThinkPad mobile Internet") | not tested |
| [Fingerprint Sensor](/index.php/Fprint "Fprint") | Yes |
| MicroSD Reader | Yes |

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Hardware](#Hardware)
*   [2 Backlight](#Backlight)
*   [3 Power management](#Power_management)
    *   [3.1 Suspend and resume](#Suspend_and_resume)
    *   [3.2 TLP](#TLP)
*   [4 Fingerprint Sensor](#Fingerprint_Sensor)
*   [5 Known Issues](#Known_Issues)

## Hardware

Using kernel 5.3.11-arch1-1-ARCH

```
Version: ThinkPad T490
Product Name: 20NJCTO1WW

```

additional hardware information from `lsusb` and `lspci` can be found bellow:

`lsusb`

```
Bus 005 Device 001: ID 1d6b:0003 Linux Foundation 3.0 root hub
Bus 004 Device 005: ID 06cb:00bd Synaptics, Inc. 
Bus 004 Device 004: ID 04f2:b681 Chicony Electronics Co., Ltd 
Bus 004 Device 003: ID 05e3:0610 Genesys Logic, Inc. 4-port hub
Bus 004 Device 002: ID 8087:0025 Intel Corp. 
Bus 004 Device 001: ID 1d6b:0002 Linux Foundation 2.0 root hub
Bus 003 Device 001: ID 1d6b:0003 Linux Foundation 3.0 root hub
Bus 002 Device 001: ID 1d6b:0002 Linux Foundation 2.0 root hub
Bus 001 Device 001: ID 1d6b:0002 Linux Foundation 2.0 root hub

```

`lspci`

```
00:00.0 Host bridge: Advanced Micro Devices, Inc. [AMD] Raven/Raven2 Root Complex
00:00.2 IOMMU: Advanced Micro Devices, Inc. [AMD] Raven/Raven2 IOMMU
00:01.0 Host bridge: Advanced Micro Devices, Inc. [AMD] Family 17h (Models 00h-1fh) PCIe Dummy Host Bridge
00:01.2 PCI bridge: Advanced Micro Devices, Inc. [AMD] Raven/Raven2 PCIe GPP Bridge [6:0]
00:01.3 PCI bridge: Advanced Micro Devices, Inc. [AMD] Raven/Raven2 PCIe GPP Bridge [6:0]
00:01.4 PCI bridge: Advanced Micro Devices, Inc. [AMD] Raven/Raven2 PCIe GPP Bridge [6:0]
00:01.6 PCI bridge: Advanced Micro Devices, Inc. [AMD] Raven/Raven2 PCIe GPP Bridge [6:0]
00:01.7 PCI bridge: Advanced Micro Devices, Inc. [AMD] Raven/Raven2 PCIe GPP Bridge [6:0]
00:08.0 Host bridge: Advanced Micro Devices, Inc. [AMD] Family 17h (Models 00h-1fh) PCIe Dummy Host Bridge
00:08.1 PCI bridge: Advanced Micro Devices, Inc. [AMD] Raven/Raven2 Internal PCIe GPP Bridge 0 to Bus A
00:14.0 SMBus: Advanced Micro Devices, Inc. [AMD] FCH SMBus Controller (rev 61)
00:14.3 ISA bridge: Advanced Micro Devices, Inc. [AMD] FCH LPC Bridge (rev 51)
00:18.0 Host bridge: Advanced Micro Devices, Inc. [AMD] Raven/Raven2 Device 24: Function 0
00:18.1 Host bridge: Advanced Micro Devices, Inc. [AMD] Raven/Raven2 Device 24: Function 1
00:18.2 Host bridge: Advanced Micro Devices, Inc. [AMD] Raven/Raven2 Device 24: Function 2
00:18.3 Host bridge: Advanced Micro Devices, Inc. [AMD] Raven/Raven2 Device 24: Function 3
00:18.4 Host bridge: Advanced Micro Devices, Inc. [AMD] Raven/Raven2 Device 24: Function 4
00:18.5 Host bridge: Advanced Micro Devices, Inc. [AMD] Raven/Raven2 Device 24: Function 5
00:18.6 Host bridge: Advanced Micro Devices, Inc. [AMD] Raven/Raven2 Device 24: Function 6
00:18.7 Host bridge: Advanced Micro Devices, Inc. [AMD] Raven/Raven2 Device 24: Function 7
01:00.0 Network controller: Intel Corporation Wireless-AC 9260 (rev 29)
02:00.0 Non-Volatile memory controller: Samsung Electronics Co Ltd NVMe SSD Controller SM981/PM981/PM983
03:00.0 Ethernet controller: Realtek Semiconductor Co., Ltd. RTL8111/8168/8411 PCI Express Gigabit Ethernet Controller (rev 0e)
03:00.1 Serial controller: Realtek Semiconductor Co., Ltd. Device 816a (rev 0e)
03:00.2 Serial controller: Realtek Semiconductor Co., Ltd. Device 816b (rev 0e)
03:00.3 IPMI Interface: Realtek Semiconductor Co., Ltd. Device 816c (rev 0e)
03:00.4 USB controller: Realtek Semiconductor Co., Ltd. Device 816d (rev 0e)
04:00.0 Ethernet controller: Realtek Semiconductor Co., Ltd. RTL8111/8168/8411 PCI Express Gigabit Ethernet Controller (rev 10)
05:00.0 Unassigned class [ff00]: Realtek Semiconductor Co., Ltd. RTS522A PCI Express Card Reader (rev 01)
06:00.0 VGA compatible controller: Advanced Micro Devices, Inc. [AMD/ATI] Picasso (rev d2)
06:00.1 Audio device: Advanced Micro Devices, Inc. [AMD/ATI] Raven/Raven2/Fenghuang HDMI/DP Audio Controller
06:00.2 Encryption controller: Advanced Micro Devices, Inc. [AMD] Family 17h (Models 10h-1fh) Platform Security Processor
06:00.3 USB controller: Advanced Micro Devices, Inc. [AMD] Raven USB 3.1
06:00.4 USB controller: Advanced Micro Devices, Inc. [AMD] Raven USB 3.1
06:00.5 Multimedia controller: Advanced Micro Devices, Inc. [AMD] Raven/Raven2/FireFlight/Renoir Audio Processor
06:00.6 Audio device: Advanced Micro Devices, Inc. [AMD] Family 17h (Models 10h-1fh) HD Audio Controller

```

## Backlight

You need to add `acpi_backlight=native` to your [kernel parameters](/index.php/Kernel_parameters "Kernel parameters").

## Power management

### Suspend and resume

Users have reported that the laptop is waking up immediately after entering suspending (see [[1]](https://www.reddit.com/r/thinkpad/comments/ckkbej/t495_linux_avoid/) and [[2]](https://www.reddit.com/r/thinkpad/comments/cveeyl/linux_on_t495t495sx395_suspendresume_fix/)). However, this seems to be fixed in the latest kernel. Suspend and resume works fine out-of-the-box.

### TLP

If you have installed [TLP](/index.php/TLP "TLP") to enable advance power management, you might notice that USB ports will not work under battery mode. Disable [Runtime Power Management](https://linrunner.de/en/tlp/docs/tlp-configuration.html#runtimepm) for USB controllers to fix this. To get PCIe device addresses of USB controllers:

```
$ lspci | grep -i usb

```

The first column of the output is the address:

```
03:00.4 USB controller: Realtek Semiconductor Co., Ltd. Device 816d (rev 0e)
07:00.3 USB controller: Advanced Micro Devices, Inc. [AMD] Raven USB 3.1
07:00.4 USB controller: Advanced Micro Devices, Inc. [AMD] Raven USB 3.1

```

To disable runtime power management for these devices, edit `/etc/default/tlp`:

 `/etc/default/tlp`  `RUNTIME_PM_BLACKLIST="03:00.4 07:00.3 07:00.4"` 

## Fingerprint Sensor

Fingerprint sensor seems to work with some recent firmware and software updates (2019-12-15). Driver development info: [[3]](https://gitlab.freedesktop.org/vincenth/libfprint/tree/synaptics-driver-20190617)[[4]](https://gitlab.freedesktop.org/libfprint/libfprint/issues/181).

1\. Use [fwupd](/index.php/Fwupd "Fwupd") to install the latest firmware for "Synaptics Prometheus Fingerprint Reader". The update might have to be done manually (the released firmware is in testing). [[5]](https://fwupd.org/lvfs/devices/com.synaptics.prometheus.firmware)[[6]](https://fwupd.org/lvfs/devices/com.synaptics.prometheus.config)

2\. Latest fprintd and libfprint are required[[7]](https://fprint.freedesktop.org/). [fprintd-libfprint2](https://aur.archlinux.org/packages/fprintd-libfprint2/) and [libfprint-git](https://aur.archlinux.org/packages/libfprint-git/) can be useful here.

3\. [fprint](/index.php/Fprint "Fprint") has more details on how to setup the fingerprint for [PAM](/index.php/PAM "PAM") authentication for example.

## Known Issues

The following issues are commonly seen even with recent kernels such as 5.5-rc2:

`Kernel warning: irq 7: nobody cared`

```
[ 6402.261413] irq 7: nobody cared (try booting with the "irqpoll" option)
[ 6402.261423] CPU: 0 PID: 0 Comm: swapper/0 Tainted: G        W         5.5.0-rc2 #1-NixOS
[ 6402.261425] Hardware name: LENOVO 20NJCTO1WW/20NJCTO1WW, BIOS R12ET46W(1.16 ) 10/28/2019
[ 6402.261426] Call Trace:
[ 6402.261430]  <IRQ>
[ 6402.261439]  dump_stack+0x66/0x90
[ 6402.261444]  __report_bad_irq+0x37/0xb1
[ 6402.261449]  note_interrupt.cold.10+0xa/0x6d
[ 6402.261452]  handle_irq_event_percpu+0x6a/0x80
[ 6402.261455]  handle_irq_event+0x3c/0x5c
[ 6402.261459]  handle_fasteoi_irq+0xa3/0x150
[ 6402.261463]  do_IRQ+0x51/0xe0
[ 6402.261465]  common_interrupt+0xf/0xf
[ 6402.261467]  </IRQ>
[ 6402.261472] RIP: 0010:cpuidle_enter_state+0xbe/0x3f0
[ 6402.261476] Code: e8 27 c6 b3 ff 80 7c 24 13 00 74 17 9c 58 0f 1f 44 00 00 f6 c4 02 0f 85 d5 02 00 00 31 ff e8 f9 d3 b9 ff fb 66 0f 1f 44 00 00 <85> ed 0f 88 42 02 00 00 48 63 c5 4c 8b 3c 24 4c 2b 7c 24 08 48 8d
[ 6402.261478] RSP: 0018:ffffffff95a03e48 EFLAGS: 00000246 ORIG_RAX: ffffffffffffffc8
[ 6402.261482] RAX: ffff8e4a38a2c300 RBX: ffff8e4a3482b800 RCX: 000000000000001f
[ 6402.261483] RDX: 000005d2a483e85f RSI: 0000000037c1c5c9 RDI: 0000000000000000
[ 6402.261485] RBP: 0000000000000002 R08: 0000000000000002 R09: 000000000002bb80
[ 6402.261486] R10: 0000000270e10990 R11: ffff8e4a38a2b3e4 R12: ffffffff95ab9da0
[ 6402.261487] R13: ffffffff95ab9e88 R14: 0000000000000002 R15: 0000000000000002
[ 6402.261493]  ? cpuidle_enter_state+0x99/0x3f0
[ 6402.261496]  cpuidle_enter+0x29/0x40
[ 6402.261501]  do_idle+0x22b/0x260
[ 6402.261506]  cpu_startup_entry+0x19/0x20
[ 6402.261509]  start_kernel+0x4e2/0x504
[ 6402.261514]  secondary_startup_64+0xb6/0xc0
[ 6402.261517] handlers:
[ 6402.261524] [<000000002329e34f>] amd_gpio_irq_handler [pinctrl_amd]
[ 6402.261527] Disabling IRQ #7

```

Please see [https://bugzilla.kernel.org/show_bug.cgi?id=201817](https://bugzilla.kernel.org/show_bug.cgi?id=201817) for more information.

`Kernel warning: nvme_poll_irqdisable`

```
[ 6390.413248] ------------[ cut here ]------------
[ 6390.413259] WARNING: CPU: 4 PID: 13706 at kernel/irq/chip.c:210 irq_startup+0xe1/0xf0
[ 6390.413260] Modules linked in: cpufreq_powersave fuse ctr ccm af_packet cmac algif_hash bnep uvcvideo videobuf2_vmalloc videobuf2_memops videobuf2_v4l2 videobuf2_common videodev mc joydev mousedev btusb btrtl btbcm btintel bluetooth uas ecdh_generic ecc crc16 amdgpu wmi_bmof iwlmvm amd_iommu_v2 gpu_sched mac80211 ttm edac_mce_amd edac_core snd_hda_codec_realtek drm_kms_helper libarc4 snd_hda_codec_generic snd_hda_codec_hdmi deflate efi_pstore pstore nls_iso8859_1 drm evdev crct10dif_pclmul nls_cp437 iwlwifi snd_hda_intel mac_hid ghash_clmulni_intel vfat sp5100_tco fat psmouse snd_intel_dspcfg agpgart serio_raw tpm_crb r8169 i2c_algo_bit snd_hda_codec efivars watchdog fb_sys_fops tpm_tis realtek tpm_tis_core snd_hda_core syscopyarea k10temp ucsi_acpi thinkpad_acpi sysfillrect i2c_piix4 snd_pci_acp3x cfg80211 sysimgblt snd_hwdep typec_ucsi ipmi_devintf libphy nvram tpm 8250_pci ledtrig_audio ipmi_msghandler typec rng_core wmi rfkill video i2c_scmi battery ac backlight i2c_core pinctrl_amd
[ 6390.413323]  button acpi_cpufreq ip6table_nat iptable_nat nf_nat xt_conntrack nf_conntrack nf_defrag_ipv4 libcrc32c crc32c_generic ip6t_rpfilter ipt_rpfilter ip6table_raw iptable_raw xt_pkttype nf_log_ipv6 nf_log_ipv4 nf_log_common xt_LOG xt_tcpudp ip6table_filter ip6_tables iptable_filter sch_fq_codel snd_pcm_oss snd_mixer_oss snd_pcm snd_timer snd soundcore msr loop cpufreq_ondemand tun tap macvlan bridge stp llc kvm_amd kvm irqbypass efivarfs ip_tables x_tables ipv6 nf_defrag_ipv6 crc_ccitt autofs4 f2fs dm_crypt algif_skcipher af_alg sd_mod usb_storage scsi_mod input_leds rtsx_pci_sdmmc led_class mmc_core atkbd libps2 crc32_pclmul crc32c_intel xhci_pci xhci_hcd ehci_pci aesni_intel ehci_hcd crypto_simd usbcore cryptd glue_helper nvme rtsx_pci nvme_core usb_common i8042 rtc_cmos serio dm_mod
[ 6390.413371] CPU: 4 PID: 13706 Comm: kworker/u32:9 Tainted: G        W         5.5.0-rc2 #1-NixOS
[ 6390.413372] Hardware name: LENOVO 20NJCTO1WW/20NJCTO1WW, BIOS R12ET46W(1.16 ) 10/28/2019
[ 6390.413378] Workqueue: events_unbound async_run_entry_fn
[ 6390.413380] RIP: 0010:irq_startup+0xe1/0xf0
[ 6390.413383] Code: 31 f6 4c 89 ef e8 8f 3e 00 00 85 c0 75 20 48 89 ee 31 d2 4c 89 ef e8 5e cd ff ff 48 89 df e8 a6 fe ff ff 89 c5 e9 54 ff ff ff <0f> 0b eb b6 0f 0b eb b2 0f 1f 80 00 00 00 00 0f 1f 44 00 00 55 48
[ 6390.413384] RSP: 0018:ffffa3bb03717c38 EFLAGS: 00010002
[ 6390.413385] RAX: 0000000000000180 RBX: ffff8e4a324e9000 RCX: 0000000000000180
[ 6390.413386] RDX: 0000000000000005 RSI: ffffffff95b13a20 RDI: ffff8e4a324e9018
[ 6390.413387] RBP: ffff8e4a324e9018 R08: 0000000000000000 R09: ffff8e4a36bd7718
[ 6390.413388] R10: 0000000000000000 R11: ffffffff95a4cba8 R12: 0000000000000001
[ 6390.413388] R13: 0000000000000001 R14: ffff8e4a349c9000 R15: 0000000000000000
[ 6390.413389] FS:  0000000000000000(0000) GS:ffff8e4a38b00000(0000) knlGS:0000000000000000
[ 6390.413390] CS:  0010 DS: 0000 ES: 0000 CR0: 0000000080050033
[ 6390.413391] CR2: 00007fce04010826 CR3: 0000000137940000 CR4: 00000000003406e0
[ 6390.413391] Call Trace:
[ 6390.413398]  enable_irq+0x49/0x90
[ 6390.413405]  nvme_poll_irqdisable+0x2d0/0x350 [nvme]
[ 6390.413408]  __nvme_disable_io_queues+0x1b2/0x1f0 [nvme]
[ 6390.413410]  ? nvme_del_queue_end+0x20/0x20 [nvme]
[ 6390.413412]  nvme_dev_disable+0x17c/0x240 [nvme]
[ 6390.413414]  nvme_suspend+0x51/0x150 [nvme]
[ 6390.413418]  pci_pm_suspend+0x73/0x150
[ 6390.413420]  ? pci_pm_freeze+0xb0/0xb0
[ 6390.413424]  dpm_run_callback+0x4f/0x140
[ 6390.413426]  __device_suspend+0x103/0x450
[ 6390.413428]  async_suspend+0x1a/0x90
[ 6390.413430]  async_run_entry_fn+0x37/0x140
[ 6390.413433]  process_one_work+0x206/0x3c0
[ 6390.413435]  worker_thread+0x2d/0x3e0
[ 6390.413436]  ? process_one_work+0x3c0/0x3c0
[ 6390.413439]  kthread+0x112/0x130
[ 6390.413440]  ? kthread_park+0x80/0x80
[ 6390.413444]  ret_from_fork+0x22/0x40
[ 6390.413447] ---[ end trace 9878c5f80dece12a ]---

```

Please see [https://bugzilla.kernel.org/show_bug.cgi?id=202891](https://bugzilla.kernel.org/show_bug.cgi?id=202891) for more information.

`Kernel warning: pending airtime underflow`

```
[  112.406635] ------------[ cut here ]------------
[  112.406641] STA 00:xx:xx:xx:xx:xx AC 2 txq pending airtime underflow: 4294967200, 96
[  112.406694] WARNING: CPU: 2 PID: 913 at net/mac80211/sta_info.c:1933 ieee80211_sta_update_pending_airtime+0x110/0x120 [mac80211]
[  112.406695] Modules linked in: fuse ctr ccm af_packet cmac algif_hash bnep uvcvideo videobuf2_vmalloc videobuf2_memops videobuf2_v4l2 videobuf2_common videodev mc joydev mousedev btusb btrtl btbcm btintel bluetooth uas ecdh_generic ecc crc16 amdgpu wmi_bmof iwlmvm amd_iommu_v2 gpu_sched mac80211 ttm edac_mce_amd edac_core snd_hda_codec_realtek drm_kms_helper libarc4 snd_hda_codec_generic snd_hda_codec_hdmi deflate efi_pstore pstore nls_iso8859_1 drm evdev crct10dif_pclmul nls_cp437 iwlwifi snd_hda_intel mac_hid ghash_clmulni_intel vfat sp5100_tco fat psmouse snd_intel_dspcfg agpgart serio_raw tpm_crb r8169 i2c_algo_bit snd_hda_codec efivars watchdog fb_sys_fops tpm_tis realtek tpm_tis_core snd_hda_core syscopyarea k10temp ucsi_acpi thinkpad_acpi sysfillrect i2c_piix4 snd_pci_acp3x cfg80211 sysimgblt snd_hwdep typec_ucsi ipmi_devintf libphy nvram tpm 8250_pci ledtrig_audio ipmi_msghandler typec rng_core wmi rfkill video i2c_scmi battery ac backlight i2c_core pinctrl_amd button acpi_cpufreq
[  112.406743]  ip6table_nat iptable_nat nf_nat xt_conntrack nf_conntrack nf_defrag_ipv4 libcrc32c crc32c_generic ip6t_rpfilter ipt_rpfilter ip6table_raw iptable_raw xt_pkttype nf_log_ipv6 nf_log_ipv4 nf_log_common xt_LOG xt_tcpudp ip6table_filter ip6_tables iptable_filter sch_fq_codel snd_pcm_oss snd_mixer_oss snd_pcm snd_timer snd soundcore msr loop cpufreq_ondemand tun tap macvlan bridge stp llc kvm_amd kvm irqbypass efivarfs ip_tables x_tables ipv6 nf_defrag_ipv6 crc_ccitt autofs4 f2fs dm_crypt algif_skcipher af_alg sd_mod usb_storage scsi_mod input_leds rtsx_pci_sdmmc led_class mmc_core atkbd libps2 crc32_pclmul crc32c_intel xhci_pci xhci_hcd ehci_pci aesni_intel ehci_hcd crypto_simd usbcore cryptd glue_helper nvme rtsx_pci nvme_core usb_common i8042 rtc_cmos serio dm_mod
[  112.406788] CPU: 2 PID: 913 Comm: irq/81-iwlwifi: Not tainted 5.5.0-rc2 #1-NixOS
[  112.406789] Hardware name: LENOVO 20NJCTO1WW/20NJCTO1WW, BIOS R12ET46W(1.16 ) 10/28/2019
[  112.406798] RIP: 0010:ieee80211_sta_update_pending_airtime+0x110/0x120 [mac80211]
[  112.406800] Code: ba d3 0f 0b 8b 44 24 04 eb a0 48 83 c6 40 41 89 e8 89 c1 48 c7 c7 28 71 f3 c0 89 44 24 04 c6 05 32 27 09 00 01 e8 db 4a ba d3 <0f> 0b 8b 44 24 04 eb 8f 0f 1f 84 00 00 00 00 00 0f 1f 44 00 00 55
[  112.406802] RSP: 0018:ffffa3bb00737ba8 EFLAGS: 00010286
[  112.406803] RAX: 0000000000000000 RBX: 00000000ffffffa0 RCX: 0000000000000000
[  112.406804] RDX: 0000000000000000 RSI: ffffffff95fc05c8 RDI: 0000000000000246
[  112.406805] RBP: 0000000000000060 R08: ffffffff95fc0580 R09: 000000000002bb80
[  112.406806] R10: 00000042845c12d5 R11: 0000000000000391 R12: ffff8e49c87a87c0
[  112.406806] R13: 0000000000000002 R14: ffff8e49c569c5c0 R15: ffffa3bb00737c58
[  112.406808] FS:  0000000000000000(0000) GS:ffff8e4a38a80000(0000) knlGS:0000000000000000
[  112.406809] CS:  0010 DS: 0000 ES: 0000 CR0: 0000000080050033
[  112.406810] CR2: 00002a29a779c000 CR3: 0000000182128000 CR4: 00000000003406e0
[  112.406811] Call Trace:
[  112.406825]  __ieee80211_tx_status+0x67d/0x800 [mac80211]
[  112.406833]  ieee80211_tx_status+0x6a/0x90 [mac80211]
[  112.406842]  iwl_mvm_tx_reclaim+0x2ad/0x3c0 [iwlmvm]
[  112.406849]  iwl_mvm_rx_ba_notif+0x10c/0x2e0 [iwlmvm]
[  112.406854]  iwl_mvm_rx_common+0xae/0x2c0 [iwlmvm]
[  112.406867]  iwl_pcie_rx_handle+0x3fd/0xa60 [iwlwifi]
[  112.406875]  ? irq_finalize_oneshot.part.46+0xf0/0xf0
[  112.406879]  iwl_pcie_irq_rx_msix_handler+0x54/0x100 [iwlwifi]
[  112.406881]  ? irq_finalize_oneshot.part.46+0xf0/0xf0
[  112.406883]  irq_thread_fn+0x1f/0x60
[  112.406885]  irq_thread+0xe7/0x170
[  112.406887]  ? irq_forced_thread_fn+0x70/0x70
[  112.406889]  ? irq_thread_check_affinity+0xc0/0xc0
[  112.406892]  kthread+0x112/0x130
[  112.406894]  ? kthread_park+0x80/0x80
[  112.406898]  ret_from_fork+0x22/0x40
[  112.406900] ---[ end trace 9878c5f80dece128 ]---
[  112.406901] ------------[ cut here ]------------

```

Please see [https://bugzilla.kernel.org/show_bug.cgi?id=205869](https://bugzilla.kernel.org/show_bug.cgi?id=205869) for more information.