[hpfall](https://github.com/srijan/hpfall) is a simple daemon providing HDD shock protection for HP laptops supporting the feature officially called "HP Mobile Data Protection System 3D" or "HP 3D DriveGuard".

## Contents

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
*   [3 Testing](#Testing)
    *   [3.1 Testing Shock protection](#Testing_Shock_protection)

## Installation

You can install [hpfall-git](https://aur.archlinux.org/packages/hpfall-git/), which is available in the [AUR](/index.php/AUR "AUR").

## Configuration

You need to set your HDD in `/etc/conf.d/hpfall`.

If your HDD is `/dev/sda`, your config file should look like this:

 `/etc/conf.d/hpfall` 
```
#
# Parameters to be passed to hpfall
#
DEVICE=/dev/sda

```

[Start](/index.php/Start "Start") and [enable](/index.php/Enable "Enable") `hpfall.service`

## Testing

After reboot with new kernel, check if hp_accel driver was initialised correctly:

 `# dmesg | grep hp_accel` 

### Testing Shock protection

**Warning:** Be careful while performing this test and keep your laptop above something soft. Simulating free fall over the desk is bad idea.

Find your HDD's unload_heads file:

 `# find /sys -name unload_heads` 

Go to it's directory and run:

 `# watch --difference=permanent cat unload_heads` 

Lift your laptop into free space and simulate a free fall while holding it firmly with your hands (~10 cm should be enough). If the disk protection works, you should hear your HDD making "click" sound and see one of your laptop's LEDs flashing. The watch value's background should also permanently turn black.