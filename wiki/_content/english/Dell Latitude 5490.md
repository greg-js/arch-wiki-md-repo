Intel Core i5-8350U CPU, Intel UHD Graphics 620
16GB of DDR4 RAM

## Installation

You can follow the [Installation guide](/index.php/Installation_guide "Installation guide") to get yourself up and running
UEFI booting works with [GRUB](/index.php/GRUB "GRUB")

## Hardware

lspci output:

 `lspci` 
```
00:00.0 Host bridge: Intel Corporation Xeon E3-1200 v6/7th Gen Core Processor Host Bridge/DRAM Registers (rev 08)
00:02.0 VGA compatible controller: Intel Corporation UHD Graphics 620 (rev 07)
00:04.0 Signal processing controller: Intel Corporation Xeon E3-1200 v5/E3-1500 v5/6th Gen Core Processor Thermal Subsystem (rev 08)
00:14.0 USB controller: Intel Corporation Sunrise Point-LP USB 3.0 xHCI Controller (rev 21)
00:14.2 Signal processing controller: Intel Corporation Sunrise Point-LP Thermal subsystem (rev 21)
00:15.0 Signal processing controller: Intel Corporation Sunrise Point-LP Serial IO I2C Controller #0 (rev 21)
00:15.1 Signal processing controller: Intel Corporation Sunrise Point-LP Serial IO I2C Controller #1 (rev 21)
00:16.0 Communication controller: Intel Corporation Sunrise Point-LP CSME HECI #1 (rev 21)
00:17.0 RAID bus controller: Intel Corporation 82801 Mobile SATA Controller [RAID mode] (rev 21)
00:1c.0 PCI bridge: Intel Corporation Sunrise Point-LP PCI Express Root Port #1 (rev f1)
00:1c.2 PCI bridge: Intel Corporation Sunrise Point-LP PCI Express Root Port #3 (rev f1)
00:1f.0 ISA bridge: Intel Corporation Sunrise Point LPC Controller/eSPI Controller (rev 21)
00:1f.2 Memory controller: Intel Corporation Sunrise Point-LP PMC (rev 21)
00:1f.3 Audio device: Intel Corporation Sunrise Point-LP HD Audio (rev 21)
00:1f.4 SMBus: Intel Corporation Sunrise Point-LP SMBus (rev 21)
00:1f.6 Ethernet controller: Intel Corporation Ethernet Connection (4) I219-LM (rev 21)
01:00.0 Unassigned class [ff00]: Realtek Semiconductor Co., Ltd. RTS525A PCI Express Card Reader (rev 01)
02:00.0 Network controller: Intel Corporation Wireless 8265 / 8275 (rev 78)

```

Detected modules:

 `hwdetect --show-modules` 
```
AGP      : agpgart intel-gtt 
ACPI     : ac battery 
BLOCK    : scsi_mod sd_mod ahci libahci libata uvcvideo xhci-hcd xhci-pci intel-xhci-usb-role-switch roles typec typec_ucsi ucsi_acpi snd-usb-audio snd-usbmidi-lib 
BLUETOOTH: btbcm btintel btrtl btusb bluetooth 
CPUFREQ  : acpi-cpufreq pcc-cpufreq 
CRYPTO   : aesni-intel aes-x86_64 crc32c-intel crc32-pclmul crct10dif-pclmul ghash-clmulni-intel glue_helper cryptd crypto_simd ecc ecdh_generic 
DRM      : drm_kms_helper drm i915 
HWMON    : coretemp dell-smm-hwmon 
I2C      : i2c-algo-bit i2c-i801 
INPUT    : evdev input-leds joydev atkbd mousedev i8042 libps2 serio serio_raw sparse-keymap hid-generic hid hid-multitouch i2c-hid usbhid 
KVM      : kvm-intel kvm 
MEDIA    : videobuf2-common videobuf2-memops videobuf2-v4l2 videobuf2-vmalloc media uvcvideo videodev 
NET      : e1000e fjes iwlwifi bluetooth rfkill cfg80211 
SOUND    : pcspkr ac97_bus snd-compress snd-hwdep snd snd-pcm-dmaengine snd-pcm snd-rawmidi snd-seq-device snd-timer snd-hda-ext-core snd-hda-core snd-hda-codec-generic snd-hda-codec-hdmi snd-hda-codec snd-hda-codec-realtek snd-hda-intel snd-soc-hdac-hda snd-soc-acpi-intel-match snd-soc-sst-dsp snd-soc-sst-ipc snd-soc-skl-ipc snd-soc-skl snd-soc-acpi snd-soc-core soundcore snd-usb-audio snd-usbmidi-lib 
TPM      : tpm_crb tpm tpm_tis_core tpm_tis 
WATCHDOG : iTCO_vendor_support iTCO_wdt mei_wdt 
OTHER    : intel-cstate intel-rapl-perf intel-uncore rng-core idma64 ledtrig-audio mac_hid memstick rtsx_pci_ms intel-lpss intel-lpss-pci rtsx_pci mei_hdcp mei mmc_core rtsx_pci_sdmmc dcdbas dell-laptop dell-smbios dell-smo8800 dell-wmi-descriptor dell-wmi intel-hid intel-wmi-thunderbolt wmi-bmof wmi intel_rapl acpi_thermal_rel int3400_thermal int3403_thermal int340x_thermal_zone processor_thermal_device intel_pch_thermal intel_powerclamp intel_soc_dts_iosf x86_pkg_temp_thermal fb_sys_fops syscopyarea sysfillrect sysimgblt crc16 irqbypass

```