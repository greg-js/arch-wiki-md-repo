| **Device** | **Status** | **Modules** |
| Display | Working | xf86-video-intel |
| Touchscreen | Working,with firmware [mssl1680-firmware](https://aur.archlinux.org/packages/mssl1680-firmware/) | silead_ts |
| Wireless | Working | iwlwifi |
| Audio | Working | alc269 |
| Touchpad | Working |
| Battery Status | Working |
| Camera | Not working |
| Bluetooth | Working | btintel |
| MicroSD Reader | Working |
| Power Management | Seems work fine |
| Accelerometer | Working, with custom build kernel | bma150_accel_i2c |
| Hardware Buttons | Working |
| Lid/Keyboard | Working |

Cube KNote i1101 is a 11-inch tablet with Apollo Lake(Celeron N3450) and 6GB RAM. It also comes with a FHD (1920x1080) resolusion screen.

## Contents

*   [1 Installation and configuration](#Installation_and_configuration)
    *   [1.1 Sound](#Sound)
        *   [1.1.1 No sound](#No_sound)
        *   [1.1.2 3.5mm jack not recognized](#3.5mm_jack_not_recognized)
    *   [1.2 Accelerometer](#Accelerometer)

## Installation and configuration

Most devices should work out-of-box after a standard installation, some devices need extra configuration.

### Sound

#### No sound

You need to add yourself to audio group.

#### 3.5mm jack not recognized

Add following lines to `/etc/modprobe.d/50-sound.conf`

```
alias snd-card-0 snd-hda-intel
alias sound-slot-0 snd-hda-intel

```

### Accelerometer

You need to build kernel manually to enable `bmc150_accel_i2c` IIO driver, and install [iio-sensor-proxy](https://aur.archlinux.org/packages/iio-sensor-proxy/) if you use a desktop environment. The DSDT data gives a faulty `ACCEL_MOUNT_MATRIX` data, so create the following file in `/etc/udev/hwdb.d/61-sensor-local.hwdb` with the following contents:

```
sensor:modalias:acpi:BOSC0200*:dmi:*:svnALLDOCUBE:pni1101:*
 ACCEL_MOUNT_MATRIX=1, 0, 0; 0, -1, 0; 0, 0, -1

```

Reboot and accelerometer works. However, it will fail after sleep and wake up, which considered as a driver bug.