| Wireless | Working | iwlwifi |
| Thunderbolt | Working | thunderbolt |
    *   [1.2 Video](#Video)
        *   [1.2.1 Backlight](#Backlight)
        *   [1.2.2 Drivers](#Drivers)
        *   [1.2.3 Multihead](#Multihead)
    *   [1.3 Webcam](#Webcam)
    *   [1.4 Power Management](#Power_Management)
    *   [1.5 Keyboard](#Keyboard)
        *   [1.5.1 Lights](#Lights)
        *   [1.5.2 Button Mapping](#Button_Mapping)
            *   [1.5.2.1 Airplane Mode Key Combination](#Airplane_Mode_Key_Combination)
            *   [1.5.2.2 Unmapped Buttons](#Unmapped_Buttons)
    *   [1.6 Touchpad](#Touchpad)
    *   [4.5 Display outputs don't work after suspend](#Display_outputs_don.27t_work_after_suspend)
The Steel Series lights on the keyboard cannot be configured with [msi-keyboard-git](https://aur.archlinux.org/packages/msi-keyboard-git/) or [msiklm-git](https://aur.archlinux.org/packages/msiklm-git/), because those tools only work with region-based RGB lighting. For this laptop model, the tool [msi-perkeyrgb](https://aur.archlinux.org/packages/msi-perkeyrgb/) provides partial control.
The commit [[1]](https://github.com/systemd/systemd/commit/e05c8b44622afe4256f3bb361cfb2c7db32fff8e) to fix this in systemd has been merged and should be available in the next release of systemd (240).

##### Airplane Mode Key Combination

The airplane mode key combination (FN + F10) is disabled by default. Adding the following kernel parameters activates airplane mode:

`acpi_osi=! acpi_osi="Windows 2009"`
Waking from suspend will have wifi in airplane mode. [[2]](https://askubuntu.com/questions/1043547/wifi-hard-blocked-after-suspend-in-ubuntu-on-gs65)
Wifi can be reactivated by either using the [airplane mode key combination](#Airplane_Mode_Button) twice or by hibernating and rebooting.
A way to mitigate this is by setting systemd to hibernate instead of suspending.
 `/etc/systemd/logind.conf` 
HandleSuspendKey=hibernate
HandleLidSwitch=hibernate
### Display outputs don't work after suspend

If the laptop is suspended with another monitor connected, then on wake all display outputs do not recognise when an external display is connected to any port. This persists across reboots. Worryingly it also persists if you reboot into Windows.

One workaround is to boot into Windows, suspend the laptop, then wake it. Connected displays will then be recognised when rebooting into Windows or Arch.

Bus 001 Device 005: ID 5986:211c Acer, Inc