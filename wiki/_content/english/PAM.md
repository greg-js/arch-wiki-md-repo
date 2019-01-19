Related articles

*   [Security](/index.php/Security "Security")
*   [pam_mount](/index.php/Pam_mount "Pam mount")
*   [pam_usb](/index.php/Pam_usb "Pam usb")
*   [pam_abl](/index.php/Pam_abl "Pam abl")
*   [pam_oath](/index.php/Pam_oath "Pam oath")

The [Linux Pluggable Authentication Modules](http://www.linux-pam.org/) (PAM) provide a framework for system-wide user authentication. To quote the [project](http://www.linux-pam.org/whatispam.html):

	PAM provides a way to develop programs that are independent of authentication scheme. These programs need "authentication modules" to be attached to them at run-time in order to work. Which authentication module is to be attached is dependent upon the local system setup and is at the discretion of the local system administrator.

This article explains the Arch Linux base set-up defaults for PAM to authenticate local and remote users. Applying changes to the defaults is subject of crosslinked specialized per topic articles.

## Contents

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
    *   [2.1 Security parameters](#Security_parameters)
    *   [2.2 PAM base-stack](#PAM_base-stack)
        *   [2.2.1 Examples](#Examples)
*   [3 Configuration How-Tos](#Configuration_How-Tos)
    *   [3.1 Security parameter configuration](#Security_parameter_configuration)
    *   [3.2 PAM stack and module configuration](#PAM_stack_and_module_configuration)
*   [4 Further PAM packages](#Further_PAM_packages)
*   [5 See also](#See_also)

## Installation

The [pam](https://www.archlinux.org/packages/?name=pam) package is part of the [base group](/index.php/Base_group "Base group") of packages and, thereby, normally installed on an Arch system. The PAM modules are installed into `/usr/lib/security` exclusively.

The repositories contain a number of optional PAM packages, the [#Configuration How-Tos](#Configuration_How-Tos) show examples.

## Configuration

A number of `/etc` paths are relevant for PAM, execute `pacman -Ql pam |grep /etc` to see the default configuration files created. They relate to either [#Security parameters](#Security_parameters) for the modules, or the [#PAM base-stack](#PAM_base-stack) configuration.

### Security parameters

The path `/etc/security` contains system-specific configuration for variables the authentication methods offer. The base install populates it with default upstream configuration files.

Note Arch Linux does not provide distribution-specific configuration for these files. For example, the `/etc/security/pwquality.conf` file can be used to define system-wide defaults for password quality. Yet, to enable it the `pam_pwquality.so` module has to be added to the [#PAM base-stack](#PAM_base-stack) of modules, which is not the case per default.

See [#Security parameter configuration](#Security_parameter_configuration) for some of the possibilities.

### PAM base-stack

The `/etc/pam.d/` path is exclusive for the PAM configuration to link the applications to the individual systems' authentication schemes. During installation of the system base it is populated by:

*   the [pambase](https://www.archlinux.org/packages/?name=pambase) package, which contains the base-stack of Arch Linux specific PAM configuration to be used by applications, and
*   other base packages. For example, [util-linux](https://www.archlinux.org/packages/?name=util-linux) adds configuration for the central *login* and other programs, the [shadow](https://www.archlinux.org/packages/?name=shadow) package adds the Arch Linux defaults to secure and modify the user database (see [Users and groups](/index.php/Users_and_groups "Users and groups")).

The different configuration files of the base installation link together, are stacked during runtime. For example, on a local user logon, the *login* application sources the `system-local-login` policy, which in turn sources others:

 `/etc/pam.d/`  `login -> system-local-login -> system-login -> system-auth` 

For a different application, a different path may apply. For example, [openssh](https://www.archlinux.org/packages/?name=openssh) installs its `sshd` PAM policy:

 `/etc/pam.d/`  `sshd -> system-remote-login -> system-login -> system-auth` 

Consequently, the choice of the configuration file in the stack matters. For the above example, a special authentication method could be required for `sshd` only, or all remote logins by changing `system-remote-login`; both changes would not affect local logins. Applying the change to `system-login` or `system-auth` instead would affect local and remote logins.

Like the example of `sshd`, any **pam-aware** application is required to install its policy to `/etc/pam.d` in order to integrate and rely on the PAM stack appropriately. If an application fails to do it, the `/etc/pam.d/other` policy is applied per default. A permissive policy for it is installed per default ([FS#48650](https://bugs.archlinux.org/task/48650)).

**Tip:** PAM is dynamically linked at runtime. For example: `$ ldd /usr/bin/login |grep pam` 
```
libpam.so.0 => /usr/lib/libpam.so.0 (0x000003d8c32d6000)
libpam_misc.so.0 => /usr/lib/libpam_misc.so.0 (0x000003d8c30d2000)
```
the *login* application is pam-aware and **must**, therefore, have a policy.

The PAM package manual pages *pam(8)* and *pam.d(5)* describe the standardized content of the configuration files. In particular they explain the four PAM groups: account, authentication, password, and session management, as well as the control values that may be used to configure stacking and behaviour of the modules.

Additionally, an extensive documentation is installed to `/usr/share/doc/Linux-PAM/index.html` which, among various guides, contains browsable man pages for each of the standard modules.

**Warning:** Changes to the PAM configuration fundamentally affect user authentication. Erroneous changes can result in that **no** or **any** user can log in. Since changes are not effective for already authenticated users, a good precaution is to perform changes with one user and test the result with another user in a separate console.

#### Examples

Two short examples to illustrate the above warning.

First, we take the following two lines:

 `/etc/pam.d/system-auth` 
```
auth      required  pam_unix.so     try_first_pass nullok
auth      optional  pam_permit.so
```

From [pam_unix(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/pam_unix.8): "The authentication component `pam_unix.so` performs the task of checking the users credentials (password). The default action of this module is to not permit the user access to a service if their official password is blank. " - the latter being what `pam_permit.so` is used for. Simply swapping the control values `required` and `optional` for both lines is enough to disable password authentication, i.e. any user may logon without providing a password.

Second, as the contrary example, per default configuration creating the following file:

```
# touch /etc/nologin 

```

results in that no user other than root may login (if root logins are allowed, another default for Arch Linux). To allow logins again, remove the file from the console you created it with.

With that as background, see [#PAM stack and module configuration](#PAM_stack_and_module_configuration) for particular use-case configuration.

## Configuration How-Tos

This section provides an overview of content detailing how to apply changes to the PAM configuration and how to integrate special new PAM modules into the PAM stack. Note the man pages for the modules can generally be reached dropping the `.so` extension.

### Security parameter configuration

The following sections describe examples to change the default PAM parameter configuration:

*   [Security#Enforcing strong passwords using pam_cracklib](/index.php/Security#Enforcing_strong_passwords_using_pam_cracklib "Security")

	shows how to enforce strong passwords with `pam_cracklib.so`.

*   [Security#Lockout user after three failed login attempts](/index.php/Security#Lockout_user_after_three_failed_login_attempts "Security")

	shows how to limit login attempts with `pam_tally.so`.

*   [Security#Allow only certain users](/index.php/Security#Allow_only_certain_users "Security")

	limits user logons with `pam_wheel.so`.

*   [Realtime process management#Configuring PAM](/index.php/Realtime_process_management#Configuring_PAM "Realtime process management") and [Security#Limit amount of processes](/index.php/Security#Limit_amount_of_processes "Security")

	detail how to configure system process limits with `pam_limits.so`.

*   [Environment variables#Using pam_env](/index.php/Environment_variables#Using_pam_env "Environment variables")

	shows examples to set environment variables via `pam_env.so`.

### PAM stack and module configuration

The following articles detail how to change the [#PAM base-stack](#PAM_base-stack) for special use-cases.

PAM modules from the [Official repositories](/index.php/Official_repositories "Official repositories"):

*   [pam_mount](/index.php/Pam_mount "Pam mount")

	detail examples for using `pam_mount.so` to automount encrypted directory paths on user login.

*   [ECryptfs#Auto-mounting](/index.php/ECryptfs#Auto-mounting "ECryptfs")

	uses `pam_ecryptfs.so` to automount an encrypted directory.

*   [Dm-crypt/Mounting at login](/index.php/Dm-crypt/Mounting_at_login "Dm-crypt/Mounting at login")

	shows how to use `pam_exec.so` to execute a custom script on a user login.

*   [Active Directory Integration#Configuring PAM](/index.php/Active_Directory_Integration#Configuring_PAM "Active Directory Integration")

	uses `pam_winbind.so` and `pam_krb5.so` to let users authenticate via Active Directory (LDAP, [Kerberos](/index.php/Kerberos "Kerberos")) services.

*   [LDAP authentication](/index.php/LDAP_authentication "LDAP authentication") with its [LDAP authentication#NSS and PAM](/index.php/LDAP_authentication#NSS_and_PAM "LDAP authentication") section

	is an article about integrating LDAP client or server-side authentication with `pam_ldap.so`.

*   [YubiKey#Two-factor authentication with SSH](/index.php/YubiKey#Two-factor_authentication_with_SSH "YubiKey")

	relies on `pam_yubico.so` in the PAM stack to enable authentication via the proprietary Yubikey.

*   [pam_oath](/index.php/Pam_oath "Pam oath")

	shows an example to implement software based two-factor authentication with `pam_oath.so`.

*   [fprint](/index.php/Fprint "Fprint")

	employs `pam_fprintd.so` to setup fingerprint authentication.

PAM modules from the [Arch User Repository](/index.php/Arch_User_Repository "Arch User Repository"):

*   [pam_usb](/index.php/Pam_usb "Pam usb")

	shows how to configure `pam_usb.so` to use an usb-device for, optionally two-factor, authentication.

*   [SSH keys#pam_ssh](/index.php/SSH_keys#pam_ssh "SSH keys")

	uses `pam_ssh.so` to authenticate as a remote user.

*   [pam_abl](/index.php/Pam_abl "Pam abl")

	explains how `pam_abl.so` can be used to limit brute-forcing attacks via ssh.

*   [EncFS](/index.php/EncFS#.2Fetc.2Fpam.d.2F "EncFS")

	may get automounted via `pam_encfs.so`.

*   [Google Authenticator](/index.php/Google_Authenticator "Google Authenticator")

	shows how to set up two-factor authentication with `pam_google_authenticator.so`.

*   [Very Secure FTP Daemon#PAM with virtual users](/index.php/Very_Secure_FTP_Daemon#PAM_with_virtual_users "Very Secure FTP Daemon")

	explains how to configure a FTP chroot with `pam_pwdfile.so` to authenticate users without a local system account.

## Further PAM packages

Other than those packages mentioned so far, the [Arch User Repository](/index.php/Arch_User_Repository "Arch User Repository") contains a number of additional PAM modules and tools.

General purpose utilities relating to PAM are:

*   **[libx32_pam](https://github.com/ArchLinux-x32/libx32-pam)** — Arch Linux PAM x32 ABI library

	[http://linux-pam.org/](http://linux-pam.org/) || [libx32-pam](https://aur.archlinux.org/packages/libx32-pam/)

*   **[Pamtester](http://linux.die.net/man/1/pamtester)** — Program to test the pluggable authentication modules (PAM) facility

	[http://pamtester.sourceforge.net/](http://pamtester.sourceforge.net/) || [pamtester](https://aur.archlinux.org/packages/pamtester/)

Note the AUR features a keyword tag for [PAM](https://aur.archlinux.org/packages/?O=0&SeB=k&K=pam&outdated=off&SB=p&SO=d&PP=50&do_Search=Go), but not all available packages are updated to include it. Hence, searching the [package description](https://aur.archlinux.org/packages/?O=0&SeB=nd&K=pam&outdated=off&SB=p&SO=d&PP=50&do_Search=Go) may be necessary.

## See also

*   [linux-pam.org](http://www.linux-pam.org/) - The project homepage
*   [Understanding and configuring PAM](https://www.ibm.com/developerworks/linux/library/l-pam/index.html) - An introductory article