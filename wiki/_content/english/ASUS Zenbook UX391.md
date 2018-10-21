## Fixing screen glitches

By default screen glitches will appear at some point, but the system is fully usable nevertheless. To fix this add `intel_idle.max_cstate=4` to your boot options.

For [GRUB](/index.php/GRUB "GRUB") you can edit `/etc/default/grub`, add `intel_idle.max_cstate=4` to `GRUB_CMDLINE_LINUX_DEFAULT` and update grub with the new config.