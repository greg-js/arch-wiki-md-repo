On occasion, users may wish to completely reset an SSD's cells to the same virgin state they were manufactured, thus restoring it to its [factory default write performance](http://www.anandtech.com/storage/showdoc.aspx?i=3531&p=8). Write performance is known to degrade over time even on SSDs with native TRIM support. TRIM only safeguards against file deletes, not replacements such as an incremental save.

**Warning:**

*   Back up ALL data of importance prior to continuing! Using this procedure will destroy ALL data on the SSD and render it unrecoverable by even data recovery services! Users will have to repartition the device and restore the data after completing this procedure!
*   Do **not** proceed with this if the target drive isn't connected directly to a SATA interface. Issuing the Secure Erase command on a drive connected via USB or a SAS/RAID card could potentially brick the drive!

## Contents

*   [1 Step 1 - Make sure the drive security is not frozen](#Step_1_-_Make_sure_the_drive_security_is_not_frozen)
*   [2 Step 2 - Enable security by setting a user password](#Step_2_-_Enable_security_by_setting_a_user_password)
*   [3 Step 3 - Issue the ATA Secure Erase command](#Step_3_-_Issue_the_ATA_Secure_Erase_command)
*   [4 Tips](#Tips)

## Step 1 - Make sure the drive security is not frozen

Issue the following command:

```
# hdparm -I /dev/sdX

```

If the command output shows "frozen" one cannot continue to the next step. Some BIOSes block the ATA Secure Erase command by issuing a "SECURITY FREEZE" command to "freeze" the drive before booting an operating system.

A possible solution is to simply suspend the system. Upon waking up, it is likely that the freeze will be lifted. If unsuccessful, one can try hot-(re)plug the data cable (which might crash the kernel). If hot-(re)plugging the SATA data cable crashes the kernel try letting the operating system fully boot up, then quickly hot-(re)plug both the SATA power and data cables. If hot-(re)plugging of SATA cables still crashes the kernel, make sure that AHCI is enabled in the BIOS (AHCI allows hot-(re)plugging operations without a crash). Using a USB-to-SATA adapter is an option if it supports hotplugging. One can also use [hdparm](https://www.archlinux.org/packages/?name=hdparm) via USB.

## Step 2 - Enable security by setting a user password

**Note:** When the user password is set the drive will be locked after next power cycle denying normal access until unlocked with the correct password.

**Warning:** If you have a Lenovo laptop, do **not** reboot it after this step. Certain variants of Lenovo's BIOS are susceptible to use a deviating algorithm for calculating the encryption key. After startup the machine will not be able to connect the SSD drive.[[1]](https://jbeekman.nl/blog/2015/03/lenovo-thinkpad-hdd-password/)

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