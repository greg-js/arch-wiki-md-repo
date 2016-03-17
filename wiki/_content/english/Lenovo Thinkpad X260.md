The Lenovo ThinkPad X260 is the successor to the [Lenovo ThinkPad X240](/index.php/Lenovo_ThinkPad_X240 "Lenovo ThinkPad X240") and [Lenovo ThinkPad X250](/index.php/Lenovo_ThinkPad_X250 "Lenovo ThinkPad X250"). Major differences include the removal of VGA, removal of the SATA channel in the M.2 slots, and end of the 400nit screen option. New in this gen is the addition of HDMI, DDR4 memory, and improved battery life.

## Contents

*   [1 Issues](#Issues)
    *   [1.1 fn-4 sleep hotkey not recognized](#fn-4_sleep_hotkey_not_recognized)
    *   [1.2 Kernels older than 4.4](#Kernels_older_than_4.4)
    *   [1.3 Crash on lid close](#Crash_on_lid_close)

### Issues

#### fn-4 sleep hotkey not recognized

Not sure if a BIOS level error or not. fn itself is regarded as an acpi wakeup event but fn-4 registers nothing, while working under windows.

#### Kernels older than 4.4

Kernels older than 4.4 won't support the new wifi chip and a great deal of Skylake features and hardware. 4.4 and 4.5 + ideal.

#### Crash on lid close

Boot with intel_pstate=no_hwp kernel param to resolve until [https://bugzilla.kernel.org/show_bug.cgi?id=110941](https://bugzilla.kernel.org/show_bug.cgi?id=110941) rolls.