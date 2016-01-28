# ASUS Eee PC 1018P

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

[![Tango-document-new.png](/images/f/f0/Tango-document-new.png)](/index.php/File:Tango-document-new.png)

[![Tango-document-new.png](/images/f/f0/Tango-document-new.png)](/index.php/File:Tango-document-new.png)

**This article is a stub.**

**Notes:** please use the first argument of the template to provide more detailed indications. (Discuss in [Talk:ASUS Eee PC 1018P#](https://wiki.archlinux.org/index.php/Talk:ASUS_Eee_PC_1018P))

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

Retrieved from "[https://wiki.archlinux.org/index.php?title=ASUS_Eee_PC_1018P&oldid=208391](https://wiki.archlinux.org/index.php?title=ASUS_Eee_PC_1018P&oldid=208391)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [ASUS](/index.php/Category:ASUS "Category:ASUS")

Hidden category:

*   [Pages flagged with Template:Stub](/index.php/Category:Pages_flagged_with_Template:Stub "Category:Pages flagged with Template:Stub")