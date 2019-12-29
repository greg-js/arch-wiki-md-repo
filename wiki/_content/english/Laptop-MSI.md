[Acer](/index.php/Laptop/Acer "Laptop/Acer") – [Apple](/index.php/Laptop/Apple "Laptop/Apple") – [ASUS](/index.php/Laptop/ASUS "Laptop/ASUS") – [Dell](/index.php/Laptop/Dell "Laptop/Dell") – [Fujitsu](/index.php/Laptop/Fujitsu "Laptop/Fujitsu") – [HP](/index.php/Laptop/HP "Laptop/HP") – [IBM/Lenovo](/index.php/Laptop/Lenovo "Laptop/Lenovo") – <a class="mw-selflink selflink">MSI</a> – [Samsung](/index.php/Laptop/Samsung "Laptop/Samsung") – [Sony](/index.php/Laptop/Sony "Laptop/Sony") – [Toshiba](/index.php/Laptop/Toshiba "Laptop/Toshiba") – [Other](/index.php/Laptop/Other "Laptop/Other")

## Model List

| Model version | Arch Linux
install CD version
 | Hardware support | Remarks |
| Video | Sound | Ethernet | Wireless | Bluetooth | Power management | Modem | Other |
| [MSI PS63 Modern](/index.php?title=MSI_PS63_Modern&action=edit&redlink=1 "MSI PS63 Modern (page does not exist)") | [Optimus](/index.php/Optimus "Optimus") | Yes | Yes | Yes | Yes | Yes | n/a | BisonCam integrated webcam works out of the box with [Cheese](/index.php?title=Cheese&action=edit&redlink=1 "Cheese (page does not exist)") just needs to be activated with Fn + F6. | All works out of the box with newer kernel above 5.x. However touchpad is disable when wake up from suspend. Needs to reset i2c bus. Add a custom script in

**/lib/systemd/system-sleep/restart_trackpad**

```
#!/bin/sh
case "$1" in
    post)
            echo -n "i2c_designware.0" > /sys/bus/platform/drivers/i2c_designware/unbind
            echo -n "i2c_designware.0" > /sys/bus/platform/drivers/i2c_designware/bind
    ;;
esac

```

source : [https://bbs.archlinux.org/viewtopic.php?pid=1865745#p1865745](https://bbs.archlinux.org/viewtopic.php?pid=1865745#p1865745)

 |
| [MSI GS63VR](/index.php/MSI_GS63VR "MSI GS63VR") | Optimus with i915 and nvidia | Yes | Yes | Yes | Yes | n/a |
| [MSI GS65](/index.php/MSI_GS65 "MSI GS65") | 2018.06.01 | [PRIME](/index.php/PRIME "PRIME") with intel and nvidia | snd_hda_intel | alx | Killer 1550 | btusb | Yes | n/a | Sleep turns on airplane mode. Nouveau does not work. |
| [MSI GS73VR](/index.php/MSI_GS73VR "MSI GS73VR") | Intel HD graphics + NVIDIA Corporation GP106M [ GeForce GTX 1060 | Realtek ALC898 Analog | Qualcomm Atheros Device e0b1 | Qualcomm Atheros QCA6174 802.11ac |
| [MSI GT72-6QE](/index.php/MSI_GT72-6QE "MSI GT72-6QE") |
| [MSI GP602QF](/index.php?title=MSI_GP602QF&action=edit&redlink=1 "MSI GP602QF (page does not exist)") | NVIDIA GeForce GTX950M [Optimus](/index.php/Optimus "Optimus") with Intel inactive | Yes | Killer E2200 | Yes | Yes | N/A | BisonCam integrated webcam works out of the box with [Cheese](/index.php?title=Cheese&action=edit&redlink=1 "Cheese (page does not exist)") just needs to be activated with Fn + F6 | Almost everything works out of the box, some configuration needed for NVIDIA just follow [Optimus](/index.php/Optimus "Optimus") instructions. |
| [MSI GE60-0ND](/index.php?title=MSI_GE60-0ND&action=edit&redlink=1 "MSI GE60-0ND (page does not exist)") | NVIDIA GeForce GTX660M [Optimus](/index.php/Optimus "Optimus") with Intel inactive | Yes | Killer E2200 | Yes | Yes | N/A | BisonCam integrated webcam works out of the box with [Cheese](/index.php?title=Cheese&action=edit&redlink=1 "Cheese (page does not exist)") just needs to be activated with Fn + F6 | Almost everything works out of the box, some configuration needed for NVIDIA just follow [Optimus](/index.php/Optimus "Optimus") instructions. |