## Fixes

### Backlight

From digging around, it looks like the Pixelbook did not connect the PWM line to control the backlight, rather is uses the DPCD. The patch can be seen here [https://patchwork.kernel.org/patch/9640237/](https://patchwork.kernel.org/patch/9640237/)

*   To enable DPCD, we need to patch the kernel with the submitted patch.
*   In addition, we need to create a `/etc/modprobe.d/i915.conf` with `options i915 enable_dpcd_backlight=1`