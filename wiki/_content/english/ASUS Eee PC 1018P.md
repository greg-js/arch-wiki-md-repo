## Pm-utils

To pm-suspend get working:

```
echo 'SUSPEND_MODULES="xhci_hcd"' > /etc/pm/config.d/00sleep_module

```

```
echo 'SUSPEND_MODULES="xhci_hcd"' > /etc/pm/config.d/unload_modules

```

## Fn Keys

After installing aur/acpi-eeepc-generic and

```
cp /etc/acpi/eeepc/models/acpi-eeepc-1001P-events.conf /etc/acpi/eeepc/models/acpi-eeepc-1018P-events.conf

```

Some keys (like F1 - suspend) starts to working correctly. Suspend key need to be configured to pm-suspend.