On occasion, users may wish to completely reset an SSD's cells to the same virgin state they were manufactured, thus restoring it to its [factory default write performance](http://www.anandtech.com/storage/showdoc.aspx?i=3531&p=8). Write performance is known to degrade over time even on SSDs with native TRIM support. TRIM only safeguards against file deletes, not replacements such as an incremental save.

**Warning:**

*   Back up ALL data of importance prior to continuing! Using this procedure will destroy ALL data on the SSD and render it unrecoverable by even data recovery services! Users will have to repartition the device and restore the data after completing this procedure!
*   Do **not** proceed with this if the target drive isn't connected directly to a SATA interface. Issuing the Secure Erase command on a drive connected via USB or a SAS/RAID card could potentially brick the drive!

**Note:** Following information has been taken from the official ATA wiki page[[1]](https://ata.wiki.kernel.org/index.php/ATA_Secure_Erase).

## Contents

*   [1 Step 1 - Make sure the drive security is not frozen](#Step_1_-_Make_sure_the_drive_security_is_not_frozen)
    *   [1.1 Dell Systems](#Dell_Systems)
*   [2 Step 2 - Enable security by setting a user password](#Step_2_-_Enable_security_by_setting_a_user_password)
*   [3 Step 3 - Issue the ATA Secure Erase command](#Step_3_-_Issue_the_ATA_Secure_Erase_command)
*   [4 Tips](#Tips)

## Step 1 - Make sure the drive security is not frozen

Issue the following command:

```
# hdparm -I /dev/sdX

```

If the command output shows "frozen" one cannot continue to the next step. Some BIOSes block the ATA Secure Erase command by issuing a "SECURITY FREEZE" command to "freeze" the drive before booting an operating system.

A possible solution is to simply [suspend](/index.php/Suspend "Suspend") the system. Upon waking up, it is likely that the freeze will be lifted. If unsuccessful, one can try hot-(re)plug the data cable (which might crash the kernel). If hot-(re)plugging the SATA data cable crashes the kernel try letting the operating system fully boot up, then quickly hot-(re)plug both the SATA power and data cables. If hot-(re)plugging of SATA cables still crashes the kernel, make sure that AHCI is enabled in the BIOS (AHCI allows hot-(re)plugging operations without a crash). Using a USB-to-SATA adapter is an option if it supports hotplugging. One can also use [hdparm](https://www.archlinux.org/packages/?name=hdparm) via USB.

### Dell Systems

If the command output shows "frozen", you may be able to work around it by:

1.  Reboot into the Dell BIOS by pressing F2 on startup.
2.  Set the Internal HDD Password in the BIOS.
3.  Apply the changes and reboot.
4.  When prompted for the password by Dell Security Manager, press Escape rather than entering it. The drive will remain locked but not frozen.
5.  Skip to Step 3 below.

**Note:** If you are using a Lenovo system and can not remove the "frozen" state (e.g. Lenovo tablets use SSD on M.2 interface), you can use a **[proprietary tool](https://pcsupport.lenovo.com/us/en/olddownloads/ds019026)** to accomplish the memory cell clearing rather than following this article. See also: [https://superuser.com/questions/763642/secure-erase-ssd-on-lenovo-thinkpad-t520-cant-unfreeze-ssd-machine-reboots-on](https://superuser.com/questions/763642/secure-erase-ssd-on-lenovo-thinkpad-t520-cant-unfreeze-ssd-machine-reboots-on)

## Step 2 - Enable security by setting a user password

**Note:** When the user password is set the drive will be locked after next power cycle denying normal access until unlocked with the correct password.

**Warning:** If you have a Lenovo laptop, do **not** reboot it after this step. Certain variants of Lenovo's BIOS are susceptible to use a deviating algorithm for calculating the encryption key. After startup the machine will not be able to connect the SSD drive.[[2]](https://jbeekman.nl/blog/2015/03/lenovo-thinkpad-hdd-password/)

Any password will do, as this should only be temporary. After the secure erase the password will be set back to NULL. In this example, the password is "PasSWorD" as shown:

```
# hdparm --user-master u --security-set-pass PasSWorD /dev/sdX
security_password="PasSWorD"
/dev/sdX:
Issuing SECURITY_SET_PASS command, password="PasSWorD", user=user, mode=high

```

As a sanity check, issue the following command

```
# hdparm -I /dev/sdX

```

The command output should display "enabled":

```
Security: 
        Master password revision code = 65534
                supported
                enabled
        not     locked
        not     frozen
        not     expired: security count
                supported: enhanced erase
        Security level high
        2min for SECURITY ERASE UNIT. 2min for ENHANCED SECURITY ERASE UNIT.
```

## Step 3 - Issue the ATA Secure Erase command

The final step is to issue the secure erase command, instructing the device's bios to erase its contents. Note for the device used in this example, earlier output states:

```
2min for SECURITY ERASE UNIT. 2min for ENHANCED SECURITY ERASE UNIT.

```

As per ATA specification the *enhanced* security erase (`--security-erase-enhanced`) performs a more elaborate wipe. If the estimated completion time for both commands is equal, it indicates the drive manufacturer shortcut the specification and uses the same erase function for both. A short time (like 2 minutes) in turn indicates the device is self-encrypting and its bios function will wipe the internal encryption key instead of overwriting all data cells.[[3]](http://security.stackexchange.com/questions/62253/what-is-the-difference-between-ata-secure-erase-and-security-erase-how-can-i-en)

**Warning:** Triple check that the correct drive designation is used. There is **no turning back** once the command is confirmed. You have been warned.

```
# hdparm --user-master u --security-erase PasSWorD /dev/sdX

```

Wait until the command completes. This example output shows it took about 40 seconds for an Intel X25-M 80GB SSD.

```
security_password="PasSWorD"
/dev/sdX:
Issuing SECURITY_ERASE command, password="PasSWorD", user=user
0.000u 0.000s 0:39.71 0.0%      0+0k 0+0io 0pf+0w

```

The drive is now erased. After a successful erasure the drive security should automatically be set to disabled (thus no longer requiring a password for access). Verify this by running the following command:

```
# hdparm -I /dev/sdX

```

The command output should display "not enabled":

```
Security: 
        Master password revision code = 65534
                supported
        not     enabled
        not     locked
        not     frozen
        not     expired: security count
                supported: enhanced erase
        2min for SECURITY ERASE UNIT. 2min for ENHANCED SECURITY ERASE UNIT.
```

## Tips

See the [GRUB EFI Examples](/index.php/GRUB_EFI_Examples "GRUB EFI Examples") for hardware-specific instructions to get GRUB EFI working following a wipe.