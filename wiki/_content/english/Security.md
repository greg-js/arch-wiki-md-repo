Related articles

*   [PAM](/index.php/PAM "PAM")
*   [Capabilities](/index.php/Capabilities "Capabilities")
*   [List of Applications/Security](/index.php/List_of_Applications/Security "List of Applications/Security")

This article contains recommendations and best practices for [hardening](https://en.wikipedia.org/wiki/Hardening_(computing) an Arch Linux system.

## Contents

*   [1 Concepts](#Concepts)
*   [2 Passwords](#Passwords)
    *   [2.1 Choosing secure passwords](#Choosing_secure_passwords)
    *   [2.2 Maintaining passwords](#Maintaining_passwords)
    *   [2.3 Password hashes](#Password_hashes)
    *   [2.4 Enforcing strong passwords using pam_cracklib](#Enforcing_strong_passwords_using_pam_cracklib)
*   [3 Storage](#Storage)
    *   [3.1 Disk encryption](#Disk_encryption)
    *   [3.2 File systems](#File_systems)
        *   [3.2.1 Mount options](#Mount_options)
    *   [3.3 File access permissions](#File_access_permissions)
*   [4 User setup](#User_setup)
    *   [4.1 Enforce a delay after a failed login attempt](#Enforce_a_delay_after_a_failed_login_attempt)
    *   [4.2 Lockout user after three failed login attempts](#Lockout_user_after_three_failed_login_attempts)
    *   [4.3 Limit amount of processes](#Limit_amount_of_processes)
    *   [4.4 Run Xorg rootless](#Run_Xorg_rootless)
*   [5 Restricting root](#Restricting_root)
    *   [5.1 Use sudo instead of su](#Use_sudo_instead_of_su)
        *   [5.1.1 Editing files using sudo](#Editing_files_using_sudo)
    *   [5.2 Restricting root login](#Restricting_root_login)
        *   [5.2.1 Allow only certain users](#Allow_only_certain_users)
        *   [5.2.2 Denying SSH login](#Denying_SSH_login)
*   [6 Mandatory access control](#Mandatory_access_control)
    *   [6.1 Pathname MAC](#Pathname_MAC)
    *   [6.2 Labels MAC](#Labels_MAC)
    *   [6.3 Access Control Lists](#Access_Control_Lists)
*   [7 Kernel hardening](#Kernel_hardening)
    *   [7.1 Kernel self-protection / exploit mitigation](#Kernel_self-protection_.2F_exploit_mitigation)
        *   [7.1.1 Userspace ASLR comparison](#Userspace_ASLR_comparison)
            *   [7.1.1.1 64-bit processes](#64-bit_processes)
            *   [7.1.1.2 32-bit processes (on an x86_64 kernel)](#32-bit_processes_.28on_an_x86_64_kernel.29)
    *   [7.2 Restricting access to kernel logs](#Restricting_access_to_kernel_logs)
    *   [7.3 Restricting access to kernel pointers in the proc filesystem](#Restricting_access_to_kernel_pointers_in_the_proc_filesystem)
    *   [7.4 Keep BPF JIT compiler disabled](#Keep_BPF_JIT_compiler_disabled)
    *   [7.5 ptrace scope](#ptrace_scope)
        *   [7.5.1 Examples of broken functionality](#Examples_of_broken_functionality)
    *   [7.6 hidepid](#hidepid)
*   [8 Sandboxing applications](#Sandboxing_applications)
    *   [8.1 Firejail](#Firejail)
    *   [8.2 bubblewrap](#bubblewrap)
    *   [8.3 chroots](#chroots)
    *   [8.4 Linux containers](#Linux_containers)
    *   [8.5 Other virtualization options](#Other_virtualization_options)
*   [9 Network and firewalls](#Network_and_firewalls)
    *   [9.1 Firewalls](#Firewalls)
    *   [9.2 Kernel parameters](#Kernel_parameters)
    *   [9.3 SSH](#SSH)
    *   [9.4 DNS](#DNS)
    *   [9.5 Proxies](#Proxies)
    *   [9.6 Managing SSL certificates](#Managing_SSL_certificates)
*   [10 Authenticating packages](#Authenticating_packages)
*   [11 Follow NVD/CVE alerts](#Follow_NVD.2FCVE_alerts)
*   [12 Physical security](#Physical_security)
    *   [12.1 Locking down BIOS](#Locking_down_BIOS)
    *   [12.2 Bootloaders](#Bootloaders)
        *   [12.2.1 Syslinux](#Syslinux)
        *   [12.2.2 GRUB](#GRUB)
    *   [12.3 Boot partition on removable flash drive](#Boot_partition_on_removable_flash_drive)
    *   [12.4 Denying console login as root](#Denying_console_login_as_root)
    *   [12.5 Automatic logout](#Automatic_logout)
    *   [12.6 Block TTY access from X](#Block_TTY_access_from_X)
    *   [12.7 Protect against rogue USB devices](#Protect_against_rogue_USB_devices)
*   [13 Rebuilding packages](#Rebuilding_packages)
*   [14 See also](#See_also)

## Concepts

*   It *is* possible to tighten the security so much as to make your system unusable. The trick is to secure it without overdoing it.
*   There are many other things that can be done to heighten the security, but the biggest threat is, and will always be, the user. When you think security, you have to think layers. When one layer is breached, another should stop the attack. But you can never make the system 100% secure unless you unplug the machine from all networks, lock it in a safe and never use it.
*   Be a little paranoid. It helps. And be suspicious. If anything sounds too good to be true, it probably is!
*   The [principle of least privilege](https://en.wikipedia.org/wiki/Principle_of_least_privilege "wikipedia:Principle of least privilege"): each part of a system should only be able to access what is required to use it, and nothing more.

## Passwords

Passwords are key to a secure Linux system. They secure your [user accounts](/index.php/Users_and_groups "Users and groups"), [encrypted filesystems](/index.php/Disk_encryption "Disk encryption"), and [SSH](/index.php/SSH_keys "SSH keys")/[GPG](/index.php/GPG "GPG") keys. They are the main way a computer chooses to trust the person using it, so a big part of security is just about picking secure passwords and protecting them.

### Choosing secure passwords

When relying on a passphrase, it must be complex enough to not be easily guessed from e.g. personal information, or [cracked](https://en.wikipedia.org/wiki/Password_cracking "wikipedia:Password cracking") using methods like brute-force attacks. The tenets of strong passphrases are based on *length* and *randomness*. In cryptography the quality of a passphrase is referred to as its [entropic security](https://en.wikipedia.org/wiki/Entropic_security "wikipedia:Entropic security").

Insecure passwords include those containing:

*   Personally identifiable information (e.g., your dog's name, date of birth, area code, favorite video game)
*   Simple character substitutions on words (e.g., `k1araj0hns0n`)
*   Root "words" or common strings followed or preceded by added numbers, symbols, or characters (e.g., `DG091101%`)
*   Common phrases or short phrases of grammatically related words (e.g. `all of the lights`), and even with character substitution.

The right choice for a password is something long (8-20 characters, depending on importance) and seemingly completely random. A good technique for building secure, seemingly random passwords is to base them on characters from every word in a sentence. Take for instance “the girl is walking down the rainy street” could be translated to `t6!WdtR5` or, less simply, `t&6!RrlW@dtR,57`. This approach could make it easier to remember a password, but note that the various letters have very different probabilities of being found at the start of words ([Wikipedia:Letter frequency](https://en.wikipedia.org/wiki/Letter_frequency#Relative_frequencies_of_the_first_letters_of_a_word_in_the_English_language "wikipedia:Letter frequency")). Also consider the [Diceware Passphrase](http://world.std.com/~reinhold/diceware.html) method, using a sufficient number of words.

A better approach is to generate pseudo-random passwords with tools like [pwgen](https://www.archlinux.org/packages/?name=pwgen) or [apg](https://aur.archlinux.org/packages/apg/): for memorizing them, one technique (for ones typed often) is to generate a long password and memorize a minimally secure number of characters, temporarily writing down the full generated string. Over time, increase the number of characters typed - until the password is ingrained in muscle memory and need not be remembered. This technique is more difficult, but can provide confidence that a password will not turn up in wordlists or "intelligent" brute force attacks that combine words and substitute characters.

It is also very effective to combine these two techniques by saving long, complex random passwords with a [password manager](/index.php/Password_manager "Password manager"), which will be in turn accessed with a mnemonic password that will have to be used only for that purpose, especially avoiding to ever transmit it over any kind of network. This method of course limits the use of the stored passwords to the terminals where the database is available for reading (which on the other hand could be seen as an added security feature).

See Bruce Schneier's article [Choosing Secure Passwords](https://www.schneier.com/blog/archives/2014/03/choosing_secure_1.html), [The passphrase FAQ](https://www.iusmentis.com/security/passphrasefaq/) or [Wikipedia:Password strength](https://en.wikipedia.org/wiki/Password_strength "wikipedia:Password strength") for some additional background.

### Maintaining passwords

Once you pick a strong password, be sure to keep it safe. Watch out for [keyloggers](https://en.wikipedia.org/wiki/Keylogger "wikipedia:Keylogger") (software and hardware), [social engineering](https://en.wikipedia.org/wiki/Social_engineering_(security) "wikipedia:Social engineering (security)"), [shoulder surfing](https://en.wikipedia.org/wiki/Shoulder_surfing_(computer_security) "wikipedia:Shoulder surfing (computer security)"), and avoid reusing passwords so insecure servers cannot leak more information than necessary. [Password managers](/index.php/List_of_applications/Security#Password_managers "List of applications/Security") can help manage large numbers of complex passwords: if you are copy-pasting the stored passwords from the manager to the applications that need them, make sure to clear the copy buffer every time, and ensure they are not saved in any kind of log (e.g. do not paste them in plain terminal commands, which would store them in files like `.bash_history`).

As a rule, do not pick insecure passwords just because secure ones are harder to remember. Passwords are a balancing act. It is better to have an encrypted database of secure passwords, guarded behind a key and one strong master password, than it is to have many similar weak passwords. Writing passwords down is perhaps equally effective[[1]](https://www.schneier.com/blog/archives/2005/06/write_down_your.html), avoiding potential vulnerabilities in software solutions while requiring physical security.

Another aspect of the strength of the passphrase is that it must not be easily recoverable from other places. If you use the same passphrase for disk encryption as you use for your login password (useful e.g. to auto-mount the encrypted partition or folder on login), make sure that `/etc/shadow` either also ends up on an encrypted partition, or uses a strong hash algorithm (i.e. sha512/bcrypt, not md5) for the stored password hash (see [SHA password hashes](/index.php/SHA_password_hashes "SHA password hashes") for more info).

If you are backing up your password database, make sure that each copy is not stored behind any other passphrase which in turn is stored in it, e.g. an encrypted drive or an authenticated remote storage service, or you will not be able to access it in case of need; a useful trick is to protect the drives or accounts where the database is backed up using a simple cryptographic hash of the master password. Maintain a list of all the backup locations: if one day you fear that the master passphrase has been compromised you will have to change it immediately on all the database backups and the locations protected with keys derived from the master password. Version-controlling the database in a secure way can be very complicated: if you choose to do it, you must have a way to update the master password of all the database versions. It may not always be immediately clear when the master password is leaked: to reduce the risk of somebody else discovering your password before you realize that it leaked, you may choose to change it on a periodical basis. If you fear that you have lost control over a copy of the database, you will need to change all the passwords contained in it within the time that it may take to brute-force the master password, according to its entropy.

### Password hashes

By default, Arch stores the hashed user passwords in the root-only-readable `/etc/shadow` file, separated from the other user parameters stored in the world-readable `/etc/passwd` file, see [Users and groups#User database](/index.php/Users_and_groups#User_database "Users and groups"). See also [#Restricting root](#Restricting_root).

Passwords are set with the **passwd** command, which [stretches](https://en.wikipedia.org/wiki/Key_stretching function and then saves them in `/etc/shadow`. See also [SHA password hashes](/index.php/SHA_password_hashes "SHA password hashes"). The passwords are also [salted](https://en.wikipedia.org/wiki/Salt_(cryptography) in order to defend them against [rainbow table](https://en.wikipedia.org/wiki/Rainbow_table "wikipedia:Rainbow table") attacks.

See also [How are passwords stored in Linux (Understanding hashing with shadow utils)](http://www.slashroot.in/how-are-passwords-stored-linux-understanding-hashing-shadow-utils).

### Enforcing strong passwords using pam_cracklib

*pam_cracklib* provides protection against [Dictionary attacks](https://en.wikipedia.org/wiki/Dictionary_attack "wikipedia:Dictionary attack") and helps configure a password policy that can be enforced throughout the system.

**Warning:** The *root* account is not affected by this policy.

**Note:** You can use the *root* account to set a password for a user that bypasses the desired/configured policy. This is useful when setting temporary passwords.

If for example you want to enforce this policy:

*   prompt 2 times for password in case of an error
*   10 characters minimum length (minlen option)
*   at least 6 characters should be different from old password when entering a new one (difok option)
*   at least 1 digit (dcredit option)
*   at least 1 uppercase (ucredit option)
*   at least 1 other character (ocredit option)
*   at least 1 lowercase (lcredit option)

Edit the `/etc/pam.d/passwd` file to read as:

```
#%PAM-1.0
password required pam_cracklib.so retry=2 minlen=10 difok=6 dcredit=-1 ucredit=-1 ocredit=-1 lcredit=-1
password required pam_unix.so use_authtok sha512 shadow
```

The `password required pam_unix.so use_authtok` instructs the *pam_unix* module to not prompt for a password but rather to use the one provided by *pam_cracklib*.

You can refer to the [pam_cracklib(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/pam_cracklib.8) and [pam_unix(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/pam_unix.8) man pages for more information.

## Storage

### Disk encryption

[Disk encryption](/index.php/Disk_encryption "Disk encryption"), preferably full disk encryption with a [strong passphrase](#Passwords), is the only way to guard data against physical recovery. This provides complete security when the computer is turned off or the disks in question are unmounted.

Once the computer is powered on and the drive is mounted, however, its data becomes just as vulnerable as an unencrypted drive. It is therefore best practice to unmount data partitions as soon as they are no longer needed.

Certain programs, like [Dm-crypt](/index.php/Dm-crypt "Dm-crypt"), allow the user to encrypt a loop file as a virtual volume. This is a reasonable alternative to full disk encryption when only certain parts of the system need be secure.

### File systems

The kernel now prevents security issues related to hardlinks and symlinks if the `fs.protected_hardlinks` and `fs.protected_symlinks` sysctl switches are enabled, so there is no longer a major security benefit from separating out world-writable directories.

Partitions containing world-writable directories can still be kept separate as a coarse way of limiting the damage from disk space exhaustion. However, filling a partition like `/var` or `/tmp` is enough to take down services. More flexible mechanisms for dealing with this concern exist (like quotas), and some filesystems include related features themselves (btrfs has quotas on subvolumes).

#### Mount options

Following the principle of least privilege, filesystems should be mounted with the most restrictive mount options possible (without losing functionality).

Relevant mount options are:

*   `nodev`: Do not interpret character or block special devices on the file system.
*   `nosuid`: Do not allow set-user-identifier or set-group-identifier bits to take effect.
*   `noexec`: Do not allow direct execution of any binaries on the mounted filesystem.

Partitions used for data should always be mounted with `nodev`, `nosuid`, `noexec`. Potential usage is presented in the table below.

| Partition | `nodev` | `nosuid` | `noexec` |
| `/var` | yes | yes | yes  |
| `/home` | yes | yes | yes, if you do not code, use wine or steam  |
| `/dev/shm` | yes | yes | yes |
| `/tmp` | yes | yes | maybe, breaks compiling packages and various other things |
| `/boot` | yes | yes | yes |

 Note that some packages (building [nvidia-dkms](https://www.archlinux.org/packages/?name=nvidia-dkms) for example) may require `exec` on `/var`.

 Applications that use QML may crash or not work properly starting with Qt 5.8 if `noexec` is set on these partitions. A workaround is available at [Qt#Applications using QML crash or don't work with Qt 5.8 - 5.10](/index.php/Qt#Applications_using_QML_crash_or_don.27t_work_with_Qt_5.8_-_5.10 "Qt").

### File access permissions

The default [file permissions](/index.php/File_permissions "File permissions") allow read access to almost everything and changing the permissions can hide valuable information from an attacker who gains access to a non-root account such as the `http` or `nobody` users.

For example:

```
# chmod 700 /boot /etc/{iptables,arptables}

```

The default [Umask](/index.php/Umask "Umask") `0022` can be changed to improve security for newly created files. The [NSA RHEL5 Security Guide](https://www.nsa.gov/ia/_files/os/redhat/rhel5-guide-i731.pdf) suggests a umask of `0077` for maximum security, which makes new files not readable by users other than the owner. To change this, see [Umask#Set the mask value](/index.php/Umask#Set_the_mask_value "Umask").

## User setup

After installation make a normal user for daily use. Do not use the root user for daily use.

### Enforce a delay after a failed login attempt

Add the following line to `/etc/pam.d/system-login` to add a delay of at least 4 seconds between failed login attempts:

 `/etc/pam.d/system-login`  `auth optional pam_faildelay.so delay=4000000` 

`4000000` is the time in microseconds to delay.

### Lockout user after three failed login attempts

To further heighten the security it is possible to lockout a user after a specified number of failed login attempts. The user account can either be locked until the root user unlocks it, or automatically be unlocked after a set time.

To lockout a user for ten minutes after three failed login attempts you have to modify `/etc/pam.d/system-login` to read as:

 `/etc/pam.d/system-login` 
```
#%PAM-1.0

auth required pam_tally2.so deny=3 unlock_time=600 onerr=succeed
account required pam_tally2.so
```

pam_tally is deprecated and superseded by pam_tally2, so you will want to comment out the pam_tally line:

```
#auth required pam_tally.so onerr=succeed file=/var/log/faillog

```

That is all there is to it. If you feel adventurous, make three failed login attempts. Then you can see for yourself what happens. To unlock a user manually do:

```
# pam_tally2 --user *username* --reset

```

If you want to permanently lockout a user after 3 failed login attempts remove the `unlock_time` part of the line. The user can then not login until root unlocks the account.

### Limit amount of processes

On systems with many, or untrusted users, it is important to limit the number of processes each can run at once, therefore preventing [fork bombs](https://en.wikipedia.org/wiki/Fork_bomb "wikipedia:Fork bomb") and other denial of service attacks. `/etc/security/limits.conf` determines how many processes each user, or group can have open, and is empty (except for useful comments) by default. adding the following lines to this file will limit all users to 100 active processes, unless they use the `prlimit` command to explicitly raise their maximum to 200 for that session. These values can be changed according to the appropriate number of processes a user should have running, or the hardware of the box you are administrating.

```
* soft nproc 100
* hard nproc 200

```

The current number of threads for each user can be found with `ps --no-headers -Leo user | sort | uniq -c`. This may help with determining appropriate values for the limits.

### Run Xorg rootless

[Xorg](/index.php/Xorg "Xorg") is commonly [considered insecure](https://security.stackexchange.com/questions/4641/why-are-people-saying-that-the-x-window-system-is-not-secure/4646#4646) because of its architecture and dated design. Thus it is recommended to avoid running it as root.

See [Xorg#Rootless Xorg](/index.php/Xorg#Rootless_Xorg "Xorg") for more details how to run it without root privileges.

## Restricting root

The root user is, by definition, the most powerful user on a system. Because of this, there are a number of ways to keep the power of the root user while limiting its ability to cause harm, or at least to make root user actions more traceable.

### Use sudo instead of su

Using [sudo](/index.php/Sudo "Sudo") for privileged access is preferable to [su](/index.php/Su "Su") for [a number of reasons](/index.php/Su#Sudo.2C_an_alternative "Su").

*   It keeps a log of which normal privilege user has run each privileged command.
*   The root user password need not be given out to each user who requires root access.
*   `sudo` prevents users from accidentally running commands as *root* that do not need root access, because a full root terminal is not created. This aligns with the [principle of least privilege](https://en.wikipedia.org/wiki/Principle_of_least_privilege "wikipedia:Principle of least privilege").
*   Individual programs may be enabled per user, instead of offering complete root access just to run one command. For example, to give the user *alice* access to a particular program:

```
# visudo

```
 `/etc/sudoers`  `alice ALL = NOPASSWD: /path/to/program` 

Or, individual commands can be allowed for all users. To mount Samba shares from a server as a regular user:

```
%users ALL=/sbin/mount.cifs,/sbin/umount.cifs

```

This allows all users who are members of the group users to run the commands `/sbin/mount.cifs` and `/sbin/umount.cifs` from any machine (ALL).

**Tip:**

To use restricted version of `nano` instead of `vi` with `visudo`,

 `/etc/sudoers`  `Defaults editor=/usr/bin/rnano` 

Exporting `# EDITOR=nano visudo` is regarded as a severe security risk since everything can be used as an `EDITOR`.

#### Editing files using sudo

Running a text editor as root can be a security vulnerability as many editors can run arbitrary shell commands or affect files other than the one you intend to edit. To avoid this, use `sudoedit filename` (equivalently, `sudo -e filename`) to edit files. This edits a copy of the file using your normal user privileges and then overwrites the original using sudo only after the editor is closed. You can change the editor this uses by setting the `SUDO_EDITOR` environment variable:

```
export SUDO_EDITOR=vim

```

Alternatively, use an editor like `rvim` which has restricted capabilities in order to be safe to run as root.

### Restricting root login

Once [sudo](/index.php/Sudo "Sudo") is properly configured, full root access can be heavily restricted or denied without losing much usability. To disable root, but still allowing to use [sudo](/index.php/Sudo "Sudo"), you can use `passwd -l root`.

#### Allow only certain users

The [PAM](/index.php/PAM "PAM") `pam_wheel.so` lets you allow only users in the group `wheel` to login using `su`. Edit both `/etc/pam.d/su` and `/etc/pam.d/su-l`, then uncomment the line:

```
# Uncomment the following line to require a user to be in the "wheel" group.
auth		required	pam_wheel.so use_uid

```

This means only users who are already able to run privileged commands may login as root.

#### Denying SSH login

Even if you do not wish to deny root login for local users, it is always good practice to [deny root login via SSH](/index.php/Ssh#Deny "Ssh"). The purpose of this is to add an additional layer of security before a user can completely compromise your system remotely.

## Mandatory access control

[Mandatory access control](https://en.wikipedia.org/wiki/Mandatory_Access_Control "wikipedia:Mandatory Access Control") (MAC) is a type of security policy that differs significantly from the [discretionary access control](https://en.wikipedia.org/wiki/Discretionary_Access_Control "wikipedia:Discretionary Access Control") (DAC) used by default in Arch and most Linux distributions. MAC essentially means that every action a program could perform that affects the system in any way is checked against a security ruleset. This ruleset, in contrast to DAC methods, cannot be modified by users. Using virtually any mandatory access control system will significantly improve the security of your computer, although there are differences in how it can be implemented.

### Pathname MAC

Pathname-based access control is a simple form of access control that offers permissions based on the path of a given file. The downside to this style of access control is that permissions are not carried with files if they are moved about the system. On the positive side, pathname-based MAC can be implemented on a much wider range of filesystems, unlike labels-based alternatives.

*   [AppArmor](/index.php/AppArmor "AppArmor") is a [Canonical](https://en.wikipedia.org/wiki/Canonical "wikipedia:Canonical")-maintained MAC implementation seen as an "easier" alternative to SELinux.
*   [Tomoyo](/index.php/Tomoyo "Tomoyo") is another simple, easy-to-use system offering mandatory access control. It is designed to be both simple in usage and in implementation, requiring very few dependencies.

### Labels MAC

Labels-based access control means the extended attributes of a file are used to govern its security permissions. While this system is arguably more flexible in its security offerings than pathname-based MAC, it only works on filesystems that support these extended attributes.

*   [SELinux](/index.php/SELinux "SELinux"), based on a [NSA](https://en.wikipedia.org/wiki/NSA "wikipedia:NSA") project to improve Linux security, implements MAC completely separate from system users and roles. It offers an extremely robust multi-level MAC policy implementation that can easily maintain control of a system that grows and changes past its original configuration.

### Access Control Lists

[Access Control Lists](/index.php/Access_Control_Lists "Access Control Lists") (ACLs) are an alternative to attaching rules directly to the filesystem in some way. ACLs implement access control by checking program actions against a list of permitted behavior.

## Kernel hardening

### Kernel self-protection / exploit mitigation

The [linux-hardened](https://www.archlinux.org/packages/?name=linux-hardened) package uses a [basic kernel hardening patch set](https://github.com/thestinger/linux-hardened) and more security-focused compile-time configuration options than the [linux](https://www.archlinux.org/packages/?name=linux) package. A custom build can be made to choose a different compromise between security and performance than the security-leaning defaults.

If you use an out-of-tree driver such as [NVIDIA](/index.php/NVIDIA "NVIDIA"), you may need to switch to its [DKMS](/index.php/DKMS "DKMS") package.

#### Userspace ASLR comparison

The [linux-hardened](https://www.archlinux.org/packages/?name=linux-hardened) package provides an improved implementation of Address Space Layout Randomization for userspace processes. The [paxtest](https://www.archlinux.org/packages/?name=paxtest) command can be used to obtain an estimate of the provided entropy:

##### 64-bit processes

 `linux-hardened` 
```
Anonymous mapping randomization test     : 32 quality bits (guessed)
Heap randomization test (ET_EXEC)        : 26 quality bits (guessed)
Heap randomization test (PIE)            : 40 quality bits (guessed)
Main executable randomization (ET_EXEC)  : No randomization
Main executable randomization (PIE)      : 32 quality bits (guessed)
Shared library randomization test        : 32 quality bits (guessed)
VDSO randomization test                  : 32 quality bits (guessed)
Stack randomization test (SEGMEXEC)      : 40 quality bits (guessed)
Stack randomization test (PAGEEXEC)      : 40 quality bits (guessed)
Arg/env randomization test (SEGMEXEC)    : 44 quality bits (guessed)
Arg/env randomization test (PAGEEXEC)    : 44 quality bits (guessed)
Offset to library randomisation (ET_EXEC): 32 quality bits (guessed)
Offset to library randomisation (ET_DYN) : 34 quality bits (guessed)
Randomization under memory exhaustion @~0: 32 bits (guessed)
Randomization under memory exhaustion @0 : 32 bits (guessed)
```
 `linux` 
```
Anonymous mapping randomization test     : 28 quality bits (guessed)
Heap randomization test (ET_EXEC)        : 13 quality bits (guessed)
Heap randomization test (PIE)            : 28 quality bits (guessed)
Main executable randomization (ET_EXEC)  : No randomization
Main executable randomization (PIE)      : 28 quality bits (guessed)
Shared library randomization test        : 28 quality bits (guessed)
VDSO randomization test                  : 20 quality bits (guessed)
Stack randomization test (SEGMEXEC)      : 30 quality bits (guessed)
Stack randomization test (PAGEEXEC)      : 30 quality bits (guessed)
Arg/env randomization test (SEGMEXEC)    : 22 quality bits (guessed)
Arg/env randomization test (PAGEEXEC)    : 22 quality bits (guessed)
Offset to library randomisation (ET_EXEC): 28 quality bits (guessed)
Offset to library randomisation (ET_DYN) : 28 quality bits (guessed)
Randomization under memory exhaustion @~0: 28 bits (guessed)
Randomization under memory exhaustion @0 : 28 bits (guessed)
```

##### 32-bit processes (on an x86_64 kernel)

 `linux-hardened` 
```
Anonymous mapping randomization test     : 16 quality bits (guessed)
Heap randomization test (ET_EXEC)        : 22 quality bits (guessed)
Heap randomization test (PIE)            : 27 quality bits (guessed)
Main executable randomization (ET_EXEC)  : No randomization
Main executable randomization (PIE)      : 18 quality bits (guessed)
Shared library randomization test        : 16 quality bits (guessed)
VDSO randomization test                  : 16 quality bits (guessed)
Stack randomization test (SEGMEXEC)      : 24 quality bits (guessed)
Stack randomization test (PAGEEXEC)      : 24 quality bits (guessed)
Arg/env randomization test (SEGMEXEC)    : 28 quality bits (guessed)
Arg/env randomization test (PAGEEXEC)    : 28 quality bits (guessed)
Offset to library randomisation (ET_EXEC): 18 quality bits (guessed)
Offset to library randomisation (ET_DYN) : 16 quality bits (guessed)
Randomization under memory exhaustion @~0: 18 bits (guessed)
Randomization under memory exhaustion @0 : 18 bits (guessed)

```
 `linux` 
```
Anonymous mapping randomization test     : 8 quality bits (guessed)
Heap randomization test (ET_EXEC)        : 13 quality bits (guessed)
Heap randomization test (PIE)            : 13 quality bits (guessed)
Main executable randomization (ET_EXEC)  : No randomization
Main executable randomization (PIE)      : 8 quality bits (guessed)
Shared library randomization test        : 8 quality bits (guessed)
VDSO randomization test                  : 8 quality bits (guessed)
Stack randomization test (SEGMEXEC)      : 19 quality bits (guessed)
Stack randomization test (PAGEEXEC)      : 19 quality bits (guessed)
Arg/env randomization test (SEGMEXEC)    : 11 quality bits (guessed)
Arg/env randomization test (PAGEEXEC)    : 11 quality bits (guessed)
Offset to library randomisation (ET_EXEC): 8 quality bits (guessed)
Offset to library randomisation (ET_DYN) : 13 quality bits (guessed)
Randomization under memory exhaustion @~0: No randomization
Randomization under memory exhaustion @0 : No randomization

```

### Restricting access to kernel logs

**Note:** This is enabled by default in [linux-hardened](https://www.archlinux.org/packages/?name=linux-hardened).

The kernel logs contain useful information for an attacker trying to exploit kernel vulnerabilities, such as sensitive memory addresses. The `kernel.dmesg_restrict` flag was to forbid access to the logs without the `CAP_SYS_ADMIN` capability (which only processes running as root have by default).

 `/etc/sysctl.d/50-dmesg-restrict.conf`  `kernel.dmesg_restrict = 1` 

### Restricting access to kernel pointers in the proc filesystem

**Note:** [linux-hardened](https://www.archlinux.org/packages/?name=linux-hardened) sets `kptr_restrict=2` by default rather than `0`.

Setting `kernel.kptr_restrict` to 1 will hide kernel symbol addresses in `/proc/kallsyms` from regular users without `CAP_SYSLOG`, making it more difficult for kernel exploits to resolve addresses/symbols dynamically. This will not help that much on a pre-compiled Arch Linux kernel, since a determined attacker could just download the kernel package and get the symbols manually from there, but if you're compiling your own kernel, this can help mitigating local root exploits. This will break some [perf](https://www.archlinux.org/packages/?name=perf) commands when used by non-root users (but many [perf](https://www.archlinux.org/packages/?name=perf) features require root access anyway). See [FS#34323](https://bugs.archlinux.org/task/34323) for more information.

Setting `kernel.kptr_restrict` to 2 will hide kernel symbol addresses in `/proc/kallsyms` regardless of privileges.

 `/etc/sysctl.d/50-kptr-restrict.conf`  `kernel.kptr_restrict = 1` 

### Keep BPF JIT compiler disabled

The Linux kernel includes the ability to compile BPF/Seccomp rule sets to native code as a performance optimization. The `net.core.bpf_jit_enable` flag should be left at 0 for a maximum level of security.

This can be helpful in specific domains, but is not usually useful. A JIT compiler opens up the possibility for an attacker to perform a heap spraying attack, where they fill the kernel's heap with malicious code. This code can then potentially be executed via another exploit, like an incorrect function pointer dereference.

### ptrace scope

Arch enables the Yama LSM by default, providing a `kernel.yama.ptrace_scope` flag. This flag is enabled by default and prevents processes from performing a `ptrace` call on other processes outside of their scope without `CAP_SYS_PTRACE`. While many debugging tools require this for some of their functionality, it is a significant improvement in security. Without this feature, there is essentially no separation between processes running as the same user without applying extra layers like namespaces. The ability to attach a debugger to an existing process is a demonstration of this weakness.

#### Examples of broken functionality

**Note:** You can still execute these commands as root (such as allowing them through [sudo](/index.php/Sudo "Sudo") for certain users, with or without a password).

*   `gdb -p $PID`
*   `strace -p $PID`
*   `perf trace -p $PID`
*   `reptyr $PID`

### hidepid

**Warning:**

*   This may cause issues for certain applications like an application running in a sandbox and [Xorg](/index.php/Xorg "Xorg") (see workaround).
*   This causes issues with [D-Bus](/index.php/D-Bus "D-Bus"), [PulseAudio](/index.php/PulseAudio "PulseAudio") and [bluetooth](/index.php/Bluetooth "Bluetooth") when using [systemd](https://www.archlinux.org/packages/?name=systemd) > 237.64-1.

The kernel has the ability to hide other users' processes, normally accessible via `/proc`, from unprivileged users by mounting the `proc` filesystem with the `hidepid=` and `gid=` options documented [here](https://git.kernel.org/pub/scm/linux/kernel/git/torvalds/linux.git/tree/Documentation/filesystems/proc.txt#n1919).

This greatly complicates an intruder's task of gathering information about running processes, whether some daemon runs with elevated privileges, whether other user runs some sensitive program, whether other users run any program at all, makes it impossible to learn whether any user runs a specific program (given the program doesn't reveal itself by its behaviour), and, as an additional bonus, poorly written programs passing sensitive information via program arguments are now protected against local eavesdroppers.

The `proc` [group](/index.php/Users_and_groups#System_groups "Users and groups"), provided by the [filesystem](https://www.archlinux.org/packages/?name=filesystem) package, acts as a whitelist of users authorized to learn other users' process information. If users or services need access to `/proc/<pid>` directories beyond their own, [add them to the group](/index.php/Users_and_groups#Group_management "Users and groups").

For example, to hide process information from other users except those in the `proc` group:

 `/etc/fstab`  `proc	/proc	proc	nosuid,nodev,noexec,hidepid=2,gid=proc	0	0` 

For user sessions to work correctly, an exception needs to be added for *systemd-logind*:

 `/etc/systemd/system/systemd-logind.service.d/hidepid.conf` 
```
[Service]
SupplementaryGroups=proc
```

## Sandboxing applications

**Note:** The user namespace configuration item `CONFIG_USER_NS` is currently enabled in [linux](https://www.archlinux.org/packages/?name=linux) (v4.14.5 or later), [linux-lts](https://www.archlinux.org/packages/?name=linux-lts) (v4.14.15 or later) and [linux-hardened](https://www.archlinux.org/packages/?name=linux-hardened). Lack of it may prevent certain sandboxing features from being made available to applications. Unprivileged usage is disabled by default unless the `kernel.unprivileged_userns_clone` [sysctl](/index.php/Sysctl "Sysctl") is set to `1`, since it greatly increases the attack surface for local privilege escalation.

### Firejail

[Firejail](/index.php/Firejail "Firejail") is an easy to use and simple tool for sandboxing applications and servers alike. Firejail is suggested for browsers and internet facing applications, as well as any servers you may be running.

### bubblewrap

[bubblewrap](/index.php/Bubblewrap "Bubblewrap") is a setuid sandbox application developed from [Flatpak](https://en.wikipedia.org/wiki/Flatpak "wikipedia:Flatpak") with an even smaller resource footprint than Firejail. While it lacks certain features such as file path whitelisting, bubblewrap does offer bind mounts as well as the creation of user/IPC/PID/network/cgroup namespaces and can support both simple and [complex sandboxes](https://github.com/projectatomic/bubblewrap/blob/master/demos/bubblewrap-shell.sh).

### chroots

Manual [chroot](/index.php/Chroot "Chroot") jails can also be constructed.

### Linux containers

[Linux Containers](/index.php/Linux_Containers "Linux Containers") are another good option when you need more separation than the other options (short of KVM and VirtualBox) provide. LXC's run on top of the existing kernel in a pseudo-chroot with their own virtual hardware.

### Other virtualization options

Using full virtualization options such as [VirtualBox](/index.php/VirtualBox "VirtualBox"), [KVM](/index.php/KVM "KVM"), [Xen](/index.php/Xen "Xen") or [Qubes OS](https://www.qubes-os.org/) (based on Xen) can also improve isolation and security in the event you plan on running risky applications or browsing dangerous websites.

## Network and firewalls

### Firewalls

While the stock Arch kernel is capable of using [Netfilter](https://en.wikipedia.org/wiki/Netfilter "wikipedia:Netfilter")'s [iptables](/index.php/Iptables "Iptables") and [nftables](/index.php/Nftables "Nftables"), they are not enabled by default. It is highly recommended to set up some form of firewall to protect the services running on the system. Many resources (including ArchWiki) do not state explicitly which services are worth protecting, so enabling a firewall is a good precaution.

*   See [iptables](/index.php/Iptables "Iptables") and [nftables](/index.php/Nftables "Nftables") for general info.
*   See [Simple stateful firewall](/index.php/Simple_stateful_firewall "Simple stateful firewall") for a guide on setting up an iptables firewall.
*   See [Category:Firewalls](/index.php/Category:Firewalls "Category:Firewalls") for other ways of setting up netfilter.
*   See [Ipset](/index.php/Ipset "Ipset") for blocking lists of ip addresses, such as those from Bluetack.

### Kernel parameters

Kernel parameters which affect networking can be set using [Sysctl](/index.php/Sysctl "Sysctl"). For how to do this, see [Sysctl#TCP/IP stack hardening](/index.php/Sysctl#TCP.2FIP_stack_hardening "Sysctl").

### SSH

Avoid using [Secure Shell](/index.php/Secure_Shell "Secure Shell") without [requiring SSH keys](/index.php/Secure_Shell#Force_public_key_authentication "Secure Shell"). This prevents [brute-force attacks](https://en.wikipedia.org/wiki/Brute-force_attack "wikipedia:Brute-force attack"). Alternatively [Fail2ban](/index.php/Fail2ban "Fail2ban") or [Sshguard](/index.php/Sshguard "Sshguard") offer lesser forms of protection by monitoring logs and writing [iptables rules](/index.php/Iptables "Iptables") but open up the potential for a denial of service, since an attacker can spoof packets as if they came from the administrator after identifying their address.

You may want to harden authentication even more by using two-factor authentication. [Google Authenticator](/index.php/Google_Authenticator "Google Authenticator") provides a two-step authentication procedure using one-time passcodes (OTP).

[Denying root login](/index.php/Secure_Shell#Deny "Secure Shell") is good practice, both for tracing intrusions and adding an additional layer of security before root access.

### DNS

[Domain Name System](https://en.wikipedia.org/wiki/DNS "wikipedia:DNS") queries are, by default on most systems, sent and received unencrypted and without checking for authentication of receipt from qualified servers. This could then allow [man-in-the-middle attacks](https://en.wikipedia.org/wiki/Man-in-the-middle_attack "wikipedia:Man-in-the-middle attack"), whereby an attacker intercepts your DNS queries and modifies the responses to deliver you an IP address leading to a [phishing](https://en.wikipedia.org/wiki/Phishing "wikipedia:Phishing") page to collect your valuable information. You nor your browser would be aware since the DNS query was believed to be legitimate.

[DNSSEC](/index.php/DNSSEC "DNSSEC") is a set of standards in place that would require DNS servers to provide clients with origin authentication of DNS data, authenticated denial of existence, and data integrity. It, however, is not yet widely used. With DNSSEC enabled, an attacker could not make modifications to your DNS queries, but would still be able to read them. [DNSCrypt](/index.php/DNSCrypt "DNSCrypt") uses cryptography to secure your communications with DNS resolvers.

If you have a domain name, set a [Sender Policy Framework](/index.php/Sender_Policy_Framework "Sender Policy Framework") policy to combat email spoofing.

### Proxies

Proxies are commonly used as an extra layer between applications and the network, sanitizing data from untrusted sources. The attack surface of a small proxy running with lower privileges is significantly smaller than a complex application running with the end user privileges.

For example the DNS resolver is implemented in [glibc](https://www.archlinux.org/packages/?name=glibc), that is linked with the application (that may be running as root), so a bug in the DNS resolver might lead to a remote code execution. This can be prevented by installing a DNS caching server, such as [Dnsmasq](/index.php/Dnsmasq "Dnsmasq"), which acts as a proxy. [[2]](https://googleonlinesecurity.blogspot.it/2016/02/cve-2015-7547-glibc-getaddrinfo-stack.html)

### Managing SSL certificates

See [OpenSSL](/index.php/OpenSSL "OpenSSL") and [Network Security Services](/index.php/Network_Security_Services "Network Security Services") (NSS) for managing custom server-side SSL certificates. Notably, the related [Let’s Encrypt](/index.php/Let%E2%80%99s_Encrypt "Let’s Encrypt") project is also supported.

The default internet SSL certificate trustchains are provided by the [ca-certificates](https://www.archlinux.org/packages/?name=ca-certificates) package and its dependencies. Note that Arch relies on trust-sources (e.g. [ca-certificates-cacert](https://www.archlinux.org/packages/?name=ca-certificates-cacert), [ca-certificates-mozilla](https://www.archlinux.org/packages/?name=ca-certificates-mozilla)) providing the certificates to be trusted per default by the system.

There may be occasions when you want to deviate from the default. For example, you may read some [news](https://www.theregister.co.uk/2016/05/27/blue_coat_ca_certs/) and want to distrust a certificate rather than wait until the trust-source providers do. The Arch infrastructure makes such easy:

1.  Obtain the respective certificate in .crt format (Example: [view](https://crt.sh/?id=19538258), [download](https://crt.sh/?d=19538258); in case of an existing trusted root certificate authority, you may also find it extracted in the system path),
2.  Copy it to `/etc/ca-certificates/trust-source/blacklist/` and
3.  Run *update-ca-trust* as root.

To check the blacklisting works as intended, you may re-open your preferred browser and do so via its GUI, which should show it as **untrusted** now.

## Authenticating packages

[Attacks on package managers](https://www.cs.arizona.edu/stork/packagemanagersecurity/attacks-on-package-managers.html#overview) are possible without proper use of package signing, and can affect even package managers with [proper signature systems](https://www.cs.arizona.edu/stork/packagemanagersecurity/faq.html). Arch uses package signing by default and relies on a web of trust from 5 trusted master keys. See [Pacman-key](/index.php/Pacman-key "Pacman-key") for details.

## Follow NVD/CVE alerts

Subscribe to the Common Vulnerabilities and Exposure (CVE) Security Alert updates, made available by National Vulnerability Database, and found on the [NVD Download webpage](https://nvd.nist.gov/download.cfm). The [Arch Linux Security Tracker](https://security.archlinux.org/) serves as a particularly useful resource in that it combines Arch Linux Security Advisory (ASA), Arch Linux Vulnerability Group (AVG) and CVE data sets in tabular format. See also [Arch Security Team](/index.php/Arch_Security_Team "Arch Security Team").

**Warning:** Do not be tempted to perform [partial upgrades](/index.php/Partial_upgrades "Partial upgrades"), as they are not supported by Arch Linux and may cause instability: the whole system should be upgraded when upgrading a component. Also note that infrequent system updates can complicate the update process.

## Physical security

**Note:** You can ignore this section if you just want to secure your computer against remote threats.

Physical access to a computer is root access given enough time and resources. However, a high *practical* level of security can be obtained by putting up enough barriers.

An attacker can gain full control of your computer on the next boot by simply attaching a malicious IEEE 1394 (FireWire), Thunderbolt or PCI Express device as they are given full memory access.[[3]](https://www.breaknenter.org/projects/inception/) There is little you can do from preventing this, or modification of the hardware itself - such as flashing malicious firmware onto a drive. However, the vast majority of attackers will not be this knowledgeable and determined.

[#Disk encryption](#Disk_encryption) will prevent access to your data if the computer is stolen, but malicious firmware can be installed to obtain this data upon your next log in by a resourceful attacker.

### Locking down BIOS

Adding a password to the BIOS prevents someone from booting into removable media, which is basically the same as having root access to your computer. You should make sure your drive is first in the boot order and disable the other drives from being bootable if you can.

### Bootloaders

It is highly important to protect your bootloader. There is a magic kernel parameter called `init=/bin/sh`. This makes any user/login restrictions totally useless.

#### Syslinux

Syslinux supports [password-protecting your bootloader](/index.php/Syslinux#Security "Syslinux"). It allows you to set either a per-menu-item password or a global bootloader password.

#### GRUB

[GRUB](/index.php/GRUB "GRUB") supports bootloader passwords as well. See [GRUB/Tips and tricks#Password protection of GRUB menu](/index.php/GRUB/Tips_and_tricks#Password_protection_of_GRUB_menu "GRUB/Tips and tricks") for details. It also has support for [encrypted boot partitions](/index.php/GRUB#Boot_partition "GRUB"), which only leaves some parts of the bootloader code unencrypted. GRUB's configuration, [kernel](/index.php/Kernel "Kernel") and [initramfs](/index.php/Initramfs "Initramfs") are encrypted.

### Boot partition on removable flash drive

One popular idea is to place the boot partition on a flash drive in order to render the system unbootable without it. Proponents of this idea often use [full disk encryption](#Disk_encryption) alongside, and some also use [detached encryption headers](/index.php/Dm-crypt/Specialties#Encrypted_system_using_a_detached_LUKS_header "Dm-crypt/Specialties") placed on the boot partition.

### Denying console login as root

Changing the configuration to disallow root to login from the TTYs makes it harder for an intruder to gain access to the system. The intruder would have to guess both a username that exists on the system and that user's password. When root is allowed to log in via the console, an intruder only needs to guess a password. Blocking root login at the console is done by commenting out the tty lines in `/etc/securetty`.

 `/etc/securetty` 
```
#tty1

```

Repeat for any tty you wish to block. To check the effect of this change, start by commenting out only one line and go to that particular console and try to login as root. You will be greeted by the message `Login incorrect`. Now that we are sure it works, go back and comment out the rest of the tty lines.

**Note:** If you see `ttyS0` this is for a serial console. Similarly, on Xen virtualized systems `hvc0` is for the administrator.

### Automatic logout

If you are using [Bash](/index.php/Bash "Bash") or [Zsh](/index.php/Zsh "Zsh"), you can set `TMOUT` for an automatic logout from shells after a timeout.

For example, the following will automatically log out from virtual consoles (but not terminal emulators in X11):

 `/etc/profile.d/shell-timeout.sh` 
```
TMOUT="$(( 60*10 ))";
[ -z "$DISPLAY" ] && export TMOUT;
case $( /usr/bin/tty ) in
	/dev/tty[0-9]*) export TMOUT;;
esac

```

If you really want EVERY Bash/Zsh prompt (even within X) to timeout, use:

```
$ export TMOUT="$(( 60*10 ))";

```

Note that this will not work if there is some command running in the shell (eg.: an SSH session or other shell without `TMOUT` support). But if you are using VC mostly for restarting frozen GDM/Xorg as root, then this is very useful.

### Block TTY access from X

See [Xorg#Block TTY access](/index.php/Xorg#Block_TTY_access "Xorg").

### Protect against rogue USB devices

Install [USBGuard](/index.php/USBGuard "USBGuard"), which is a software framework that helps to protect your computer against rogue USB devices (a.k.a. [BadUSB](https://srlabs.de/badusb), [PoisonTap](https://github.com/samyk/poisontap) or [LanTurtle](https://lanturtle.com/)) by implementing basic whitelisting and blacklisting capabilities based on device attributes.

## Rebuilding packages

Packages can be rebuilt and stripped of undesired functions and features as a means to reduce attack surface. For example, [bzip2](https://www.archlinux.org/packages/?name=bzip2) can be rebuilt without `bzip2recover` in an attempt to circumvent [CVE-2016-3189](https://security.archlinux.org/CVE-2016-3189). Custom hardening flags can also be applied either manually or via a wrapper.

## See also

*   [Arch Linux Security Tracker](https://security.archlinux.org/)
*   [List of applications/Security](/index.php/List_of_applications/Security "List of applications/Security")
*   [CentOS Wiki: OS Protection](https://wiki.centos.org/HowTos/OS_Protection)
*   [Hardening the Linux desktop](https://www.ibm.com/developerworks/linux/tutorials/l-harden-desktop/index.html)
*   [Hardening the Linux server](https://www.ibm.com/developerworks/linux/tutorials/l-harden-server/index.html)
*   [Linux Foundation: Linux workstation security checklist](https://github.com/lfit/itpol/blob/master/linux-workstation-security.md)
*   [privacytools.io Privacy Resources](https://www.privacytools.io/)
*   [Red Hat Enterprise Linux 7 Security Guide](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/7/html/Security_Guide/)
*   [Securing Debian Manual (PDF)](https://www.debian.org/doc/manuals/securing-debian-howto/securing-debian-howto.en.pdf)
*   [The paranoid #! Security Guide](https://web.archive.org/web/20140220055801/http://crunchbang.org:80/forums/viewtopic.php?id=24722)
*   [UNIX and Linux Security Checklist v3.0](https://archive.fo/wrjIM)