The Lenovo ThinkPad X260 is the successor to the [Lenovo ThinkPad X240](/index.php/Lenovo_ThinkPad_X240 "Lenovo ThinkPad X240") and [Lenovo ThinkPad X250](/index.php/Lenovo_ThinkPad_X250 "Lenovo ThinkPad X250"). Major differences include the removal of VGA, removal of the SATA channel in the M.2 slots, and end of the 400nit screen option. New in this gen is the addition of HDMI, DDR4 memory, and improved battery life.

## Contents

*   [1 Configuration](#Configuration)
    *   [1.1 Fingerprint](#Fingerprint)
*   [2 Troubleshooting](#Troubleshooting)
    *   [2.1 fn-4 sleep hotkey not recognized](#fn-4_sleep_hotkey_not_recognized)

## Configuration

### Fingerprint

Some X260's come with vfs (Validity Sensors) fingerprint readers. If this is the case then you will need to additionally install [libfprint-git](https://aur.archlinux.org/packages/libfprint-git/), along with fprintd. See [fprint](/index.php/Fprint "Fprint") for details.

## Troubleshooting

### fn-4 sleep hotkey not recognized

Not sure if a BIOS level error or not. fn itself is regarded as an acpi wakeup event but fn-4 registers nothing, while working under windows.