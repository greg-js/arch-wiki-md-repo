| **Device** | **Status** | **Modules** |
| Intel | Working | mesa |
| Nvidia | Working | nvidia *or* (nouveau not tested) |
| Wireless | Working |
| Audio | Working |
| Touchpad | Working | xf86-input-libinput |
| Touchscreen | Not working |
| Camera | Working | linux-uvc |

Currently not listed on the HP site, but basically a lower-spec version of [HP ENVY 13-ah0003na](https://store.hp.com/UKStore/Merch/Product.aspx?id=4EY21EA&opt=ABU&sel=NTB), i.e. 256 GB SSD, 8GB RAM, Core i5.

## Contents

*   [1 Installation](#Installation)
    *   [1.1 Video](#Video)
        *   [1.1.1 Drivers](#Drivers)
    *   [1.2 Audio](#Audio)
    *   [1.3 Keyboard](#Keyboard)
        *   [1.3.1 Brightness](#Brightness)
    *   [1.4 Touchpad](#Touchpad)
    *   [1.5 Touchscreen](#Touchscreen)

## Installation

To start, you best disable Secure Boot in the BIOS by pressing `Esc` after pressing the power button until the BIOS appears.

### Video

#### Drivers

This laptop has both an Nvidia GPU and integrated Intel chipset. Follow the instructions in the [NVIDIA Optimus](/index.php/NVIDIA_Optimus "NVIDIA Optimus") article.

### Audio

Works out of the box

Install [PulseAudio](/index.php/PulseAudio "PulseAudio").

### Keyboard

#### Brightness

Screen brightness works out of the box in KDE, similarly for the keyboard backlight toggle button.

### Touchpad

Install [libinput](/index.php/Libinput "Libinput"). If there are any problems, try [Touchpad Synaptics](/index.php/Touchpad_Synaptics "Touchpad Synaptics").

### Touchscreen

Definitely works on Windows, but is apparently not even detected as a USB device.