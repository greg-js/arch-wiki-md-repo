## Contents

*   [1 Disabling the hardware write protection](#Disabling_the_hardware_write_protection)
*   [2 Flashing custom firmware](#Flashing_custom_firmware)
*   [3 Boot into SeaBIOS](#Boot_into_SeaBIOS)
*   [4 Boot into ChromeOS](#Boot_into_ChromeOS)
*   [5 Installation Media](#Installation_Media)
*   [6 Post Installation Configuration](#Post_Installation_Configuration)

## Disabling the hardware write protection

*   Unscrew all 12 screws on the back of the chromebook and use your finger or a spudger to remove the back, being careful not to rip the ribbon cable attached to both sides.
*   Remove the big flat screw near the wireless NIC. [Picture](https://samsclass.info/128/proj/asus-screw.jpg)
*   Verify that hardware write is disabled by typing the following commands in crosh (Ctrl+Alt+T)

	shell

	sudo su

	flashrom --wp-disable

	flashrom --wp-status

*   The output should include 'WP: write protect is disabled'

## Flashing custom firmware

**Warning:** Flashing custom firmware to your Chromebook is risky, do so at your own risk.

**Warning:** You need to have developer mode at this point.

*   Hit Ctrl+Alt+T
*   Execute the following commands:

	shell

	cd

	curl -k -L -O [https://johnlewis.ie/flash_chromebook_rom.sh](https://johnlewis.ie/flash_chromebook_rom.sh)

	sudo -E bash flash_chromebook_rom.sh

*   Follow the following menu's according to instructions (and cross your fingers that your Chromebook doesn't get bricked).

## Boot into SeaBIOS

*   With the white "OS verification disabled" page on the screen, hit Ctrl+L to boot into SeaBios.

## Boot into ChromeOS

**Warning:** You will only be able to boot into ChromeOS if you have not formatted the internal SSD (for example, installed Arch to a USB drive)

*   With the white "OS verification disabled" page on the screen, hit Ctrl+D to continue to boot ChromeOS.

## Installation Media

Since the CB3-111 only has a 16GB (non-upgradeable) eMMC drive, it may be a good idea to install Arch Linux on a fast USB 3.0 drive rather than the internal drive. This will allow you to boot into ChromeOS as well as Arch Linux. Make sure to use a fast drive, since not just any drive will provide a comfortable experience.

## Post Installation Configuration

For information on general Chromebook post installation configuration (hotkeys, power key handling ...) see the [Post installation configuration](/index.php/Chromebook#Post_installation_configuration "Chromebook") on the [Chromebook](/index.php/Chromebook "Chromebook") page.