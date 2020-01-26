Related articles

*   [Users and groups](/index.php/Users_and_groups "Users and groups")
*   [su](/index.php/Su "Su")

[Sudo](https://www.sudo.ws/sudo/) allows a system administrator to delegate authority to give certain users—or groups of users—the ability to run commands as root or another user while providing an audit trail of the commands and their arguments.

Sudo is an alternative to [su](/index.php/Su "Su") for running commands as root. Unlike [su](/index.php/Su "Su"), which launches a root shell that allows all further commands root access, sudo instead grants temporary privilege escalation to a single command. By enabling root privileges only when needed, sudo usage reduces the likelihood that a typo or a bug in an invoked command will ruin the system.

Sudo can also be used to run commands as other users; additionally, sudo logs all commands and failed access attempts for security auditing.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Installation](#Installation)
*   [2 Usage](#Usage)
*   [3 Configuration](#Configuration)
    *   [3.1 View current settings](#View_current_settings)
    *   [3.2 Using visudo](#Using_visudo)
    *   [3.3 Example entries](#Example_entries)
    *   [3.4 Sudoers default file permissions](#Sudoers_default_file_permissions)
*   [4 Tips and tricks](#Tips_and_tricks)
    *   [4.1 Disable password *prompt* timeout](#Disable_password_prompt_timeout)
    *   [4.2 Add terminal bell to the password prompt](#Add_terminal_bell_to_the_password_prompt)
    *   [4.3 Disable per-terminal sudo](#Disable_per-terminal_sudo)
    *   [4.4 Environment variables](#Environment_variables)
    *   [4.5 Passing aliases](#Passing_aliases)
    *   [4.6 Root password](#Root_password)
    *   [4.7 Disable root login](#Disable_root_login)
        *   [4.7.1 kdesu](#kdesu)
    *   [4.8 Harden with Sudo Example](#Harden_with_Sudo_Example)
    *   [4.9 Configure sudo using drop-in files in /etc/sudoers.d](#Configure_sudo_using_drop-in_files_in_/etc/sudoers.d)
    *   [4.10 Editing files](#Editing_files)
    *   [4.11 Enable insults](#Enable_insults)
    *   [4.12 Play sound on password prompt](#Play_sound_on_password_prompt)
*   [5 Troubleshooting](#Troubleshooting)
    *   [5.1 SSH TTY Problems](#SSH_TTY_Problems)
    *   [5.2 Permissive umask](#Permissive_umask)
    *   [5.3 Defaults skeleton](#Defaults_skeleton)

## Installation

[Install](/index.php/Install "Install") the [sudo](https://www.archlinux.org/packages/?name=sudo) package.

## Usage

To begin using `sudo` as a non-privileged user, it must be properly configured. See [#Configuration](#Configuration).

To use *sudo*, simply prefix a command and its arguments with `sudo` and a space:

```
$ sudo *cmd*

```

For example, to use pacman:

```
$ sudo pacman -Syu

```

See [sudo(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/sudo.8) for more information.

## Configuration

See [sudoers(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/sudoers.5) for more information, such as configuring the password timeout.

### View current settings

Run `sudo -ll` to print out the current sudo configuration, or `sudo -lU *user*` for a specific user.

### Using visudo

The configuration file for sudo is `/etc/sudoers`. It should **always** be edited with the [visudo(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/visudo.8) command. `visudo` locks the `sudoers` file, saves edits to a temporary file, and checks that file's grammar before copying it to `/etc/sudoers`.

**Warning:**

*   It is imperative that `sudoers` be free of syntax errors! Any error makes sudo unusable. **Always** edit it with `visudo` to prevent errors.
*   From [visudo(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/visudo.8): *Note that this can be a security hole since it allows the user to execute any program they wish simply by setting VISUAL or EDITOR.*

The default editor for visudo is `vi`. sudo from the core repository is compiled with `--with-env-editor` by default and honors the use of the `VISUAL` and `EDITOR` variables. `EDITOR` is not used when `VISUAL` is set.

To establish nano as the **visudo** editor for the duration of the current shell session export `EDITOR=nano`; to use a different editor just once simply set the variable before calling **visudo**:

```
# EDITOR=nano visudo

```

Alternatively you may edit a copy of the `/etc/sudoers` file and check it using `visudo -c -f */copy/of/sudoers*`. This might come in handy in case you want to circumvent locking the file with visudo.

To change the editor permanently, see [Environment variables#Per user](/index.php/Environment_variables#Per_user "Environment variables"). To change the editor of choice permanently system-wide only for `visudo`, add the following to `/etc/sudoers` (assuming `nano` is your preferred editor):

```
# Reset environment by default
Defaults      env_reset
# Set default EDITOR to nano, and do not allow visudo to use EDITOR/VISUAL.
Defaults      editor=/usr/bin/nano, !env_editor

```

### Example entries

To allow a user to gain full root privileges when they precede a command with `sudo`, add the following line:

```
USER_NAME   ALL=(ALL) ALL

```

To allow a user to run all commands as any user but only on the machine with hostname `HOST_NAME`:

```
USER_NAME   HOST_NAME=(ALL) ALL

```

To allow members of group `wheel` sudo access:

```
%wheel      ALL=(ALL) ALL

```

**Tip:** When creating new administrators, it is often desirable to enable sudo access for the `wheel` group and [add the user to it](/index.php/Users_and_Groups#Other_examples_of_user_management "Users and Groups"), since by default [Polkit](/index.php/Polkit#Administrator_identities "Polkit") treats the members of the `wheel` group as administrators. If the user is not a member of `wheel`, software using Polkit may ask to authenticate using the root password instead of the user password.

To disable asking for a password for user `USER_NAME`:

**Warning:** This will let any process running with your user name to use sudo without asking for permission.

```
Defaults:USER_NAME      !authenticate

```

Enable explicitly defined commands only for user `USER_NAME` on host `HOST_NAME`:

```
USER_NAME HOST_NAME=/usr/bin/halt,/usr/bin/poweroff,/usr/bin/reboot,/usr/bin/pacman -Syu

```

**Note:** The most customized option should go at the end of the file, as the later lines overrides the previous ones. In particular such a line should be after the `%wheel` line if your user is in this group.

Enable explicitly defined commands only for user `USER_NAME` on host `HOST_NAME` without password:

```
USER_NAME HOST_NAME= NOPASSWD: /usr/bin/halt,/usr/bin/poweroff,/usr/bin/reboot,/usr/bin/pacman -Syu

```

A detailed `sudoers` example is available at `/usr/share/doc/sudo/examples/sudoers`. Otherwise, see the [sudoers(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/sudoers.5) for detailed information.

### Sudoers default file permissions

The owner and group for the `sudoers` file must both be 0\. The file permissions must be set to 0440\. These permissions are set by default, but if you accidentally change them, they should be changed back immediately or sudo will fail.

```
# chown -c root:root /etc/sudoers
# chmod -c 0440 /etc/sudoers

```

## Tips and tricks

### Disable password *prompt* timeout

A common annoyance is a long-running process that runs on a background terminal somewhere that runs with normal permissions and elevates only when needed. This leads to a sudo password prompt which goes unnoticed and times out, at which point the process dies and the work done is lost or, at best, cached. Common advice is to enable passwordless sudo, or extend the timeout of sudo remembering a password. Both of these have negative security implications. The **prompt** timeout can also be disabled and since that does not serve any reasonable security purpose it should be the solution here:

```
Defaults passwd_timeout=0

```

### Add terminal bell to the password prompt

To draw attention to a sudo prompt in a background terminal, users can simply make it echo a bell character:

```
Defaults passprompt="^G[sudo] password for %p: "

```

Note the ^G is a literal bell character. E.g. in vim, insert using the sequence ^V ^G.

### Disable per-terminal sudo

**Warning:** This will let any process use your sudo session.

If you are annoyed by sudo's defaults that require you to enter your password every time you open a new terminal, disable **tty_tickets**:

```
Defaults !tty_tickets

```

### Environment variables

If you have a lot of environment variables, or you export your proxy settings via `export http_proxy="..."`, when using sudo these variables do not get passed to the root account unless you run sudo with the `-E` option.

```
$ sudo -E pacman -Syu

```

The recommended way of preserving environment variables is to append them to `env_keep`:

 `/etc/sudoers` 
```
Defaults env_keep += "ftp_proxy http_proxy https_proxy no_proxy"

```

### Passing aliases

If you use a lot of aliases, you might have noticed that they do not carry over to the root account when using sudo. However, there is an easy way to make them work. Simply add the following to your `~/.bashrc` or `/etc/bash.bashrc`:

```
alias sudo='sudo '

```

### Root password

Users can configure sudo to ask for the root password instead of the user password by adding `targetpw` (target user, defaults to root) or `rootpw` to the Defaults line in `/etc/sudoers`:

```
Defaults targetpw

```

To prevent exposing your root password to users, you can restrict this to a specific group:

```
Defaults:%wheel targetpw
%wheel ALL=(ALL) ALL

```

### Disable root login

Users may wish to disable the root login. Without root, attackers must first guess a user name configured as a sudoer as well as the user password. See for example [OpenSSH#Deny](/index.php/OpenSSH#Deny "OpenSSH").

**Warning:**

*   Be careful, you may lock yourself out by disabling root login. Sudo is not automatically installed and its default configuration allows neither passwordless root access nor root access with your own password. Ensure a user is properly configured as a sudoer *before* disabling the root account!
*   If you have changed your sudoers -file to use rootpw as default, then do not disable root login with any of the following commands!
*   If you are already locked out, see [Password recovery](/index.php/Password_recovery "Password recovery") for help.

The account can be locked via `passwd`:

```
# passwd -l root

```

A similar command unlocks root.

```
$ sudo passwd -u root

```

Alternatively, edit `/etc/shadow` and replace the root's encrypted password with "!":

```
root:!:12345::::::

```

To enable root login again:

```
$ sudo passwd root

```

**Tip:** To get to an interactive root prompt, even after disabling the *root* account, use `sudo -i`.

#### kdesu

kdesu may be used under [KDE](/index.php/KDE "KDE") to launch GUI applications with root privileges. It is possible that by default kdesu will try to use su even if the root account is disabled. Fortunately one can tell kdesu to use sudo instead of su. Create/edit the file `~/.config/kdesurc`:

```
[super-user-command]
super-user-command=sudo

```

or use the following command:

```
$ kwriteconfig5 --file kdesurc --group super-user-command --key super-user-command sudo

```

Alternatively, install [kdesudo](https://aur.archlinux.org/packages/kdesudo/), which has the added advantage of tab-completion for the command following.

### Harden with Sudo Example

Let us say you create 3 users: admin, devel, and joe. The user "admin" is used for journalctl, systemctl, mount, kill, and iptables; "devel" is used for installing packages, and editing config files; and "joe" is the user you log in with. To let "joe" reboot, shutdown, and use netctl we would do the following:

Edit `/etc/pam.d/su` and `/etc/pam.d/su-l` Require user be in the wheel group, but do not put anyone in it.

```
#%PAM-1.0
auth            sufficient      pam_rootok.so
# Uncomment the following line to implicitly trust users in the "wheel" group.
#auth           sufficient      pam_wheel.so trust use_uid
# Uncomment the following line to require a user to be in the "wheel" group.
auth            required        pam_wheel.so use_uid
auth            required        pam_unix.so
account         required        pam_unix.so
session         required        pam_unix.so

```

Limit SSH login to the 'ssh' group. Only "joe" will be part of this group.

```
groupadd -r ssh
gpasswd -a joe ssh
echo 'AllowGroups ssh' >> /etc/ssh/sshd_config

```

[Restart](/index.php/Restart "Restart") `sshd.service`.

Add users to other groups.

```
for g in power network ;do ;gpasswd -a joe $g ;done
for g in network power storage ;do ;gpasswd -a admin $g ;done

```

Set permissions on configs so devel can edit them.

```
chown -R devel:root /etc/{http,openvpn,cups,zsh,vim,screenrc}

```

```
Cmnd_Alias  POWER       =   /usr/bin/shutdown -h now, /usr/bin/halt, /usr/bin/poweroff, /usr/bin/reboot
Cmnd_Alias  STORAGE     =   /usr/bin/mount -o nosuid\,nodev\,noexec, /usr/bin/umount
Cmnd_Alias  SYSTEMD     =   /usr/bin/journalctl, /usr/bin/systemctl
Cmnd_Alias  KILL        =   /usr/bin/kill, /usr/bin/killall
Cmnd_Alias  PKGMAN      =   /usr/bin/pacman
Cmnd_Alias  NETWORK     =   /usr/bin/netctl
Cmnd_Alias  FIREWALL    =   /usr/bin/iptables, /usr/bin/ip6tables
Cmnd_Alias  SHELL       =   /usr/bin/zsh, /usr/bin/bash
%power      ALL         =   (root)  NOPASSWD: POWER
%network    ALL         =   (root)  NETWORK
%storage    ALL         =   (root)  STORAGE
root        ALL         =   (ALL)   ALL
admin       ALL         =   (root)  SYSTEMD, KILL, FIREWALL
devel	    ALL         =   (root)  PKGMAN
joe	    ALL         =   (devel) SHELL, (admin) SHELL 

```

With this setup, you will almost never need to login as the Root user.

"joe" can connect to his home WiFi.

```
sudo netctl start home
sudo poweroff

```

"joe" can not use netctl as any other user.

```
sudo -u admin -- netctl start home

```

When "joe" needs to use journalctl or kill run away process he can switch to that user.

```
sudo -i -u devel
sudo -i -u admin

```

But "joe" cannot switch to the root user.

```
sudo -i -u root

```

If "joe" want to start a gnu-screen session as admin he can do it like this:

```
sudo -i -u admin
admin% chown admin:tty `echo $TTY`
admin% screen

```

### Configure sudo using drop-in files in /etc/sudoers.d

*sudo* parses files contained in the directory `/etc/sudoers.d/`. This means that instead of editing `/etc/sudoers`, you can change settings in standalone files and drop them in that directory. This has two advantages:

*   There is no need to edit a `sudoers.pacnew` file;
*   If there is a problem with a new entry, you can remove the offending file instead of editing `/etc/sudoers` (but see the warning below).

The format for entries in these drop-in files is the same as for `/etc/sudoers` itself. To edit them directly, use `visudo -f /etc/sudoers.d/*somefile*`. See the "Including other files from within sudoers" section of [sudoers(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/sudoers.5) for details.

The files in `/etc/sudoers.d/` directory are parsed in lexicographical order, file names containing `.` or `~` are skipped. To avoid sorting problems, the file names should begin with two digits, e.g. `01_foo`.

**Note:** The order of entries in the drop-in files is important: make sure that the statements do not override themselves.

**Warning:** The files in `/etc/sudoers.d/` are just as fragile as `/etc/sudoers` itself: any improperly formatted file will prevent `sudo` from working. Hence, for the same reason it is strongly advised to use `visudo`

### Editing files

`sudo -e` or `sudoedit` lets you edit a file as another user while still running the text editor as your user.

This is especially useful for editing files as root without elevating the privilege of your text editor, for more details read [sudo(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/sudo.8#e).

Note that you can set the editor to any program, so for example one can use [meld](https://www.archlinux.org/packages/?name=meld) to manage [pacnew](/index.php/Pacman/Pacnew_and_Pacsave "Pacman/Pacnew and Pacsave") files:

```
$ SUDO_EDITOR=meld sudo -e /etc/*file*{,.pacnew*}*

```

### Enable insults

Users can enable insults easter egg in sudo by adding the following line in sudoers file with `visudo`.

Upon entering an incorrect password this will replace `Sorry, try again.` message with humorous insults.

 `/etc/sudoers`  `Defaults insults` 

### Play sound on password prompt

To make a beep when the password prompt appears, set the `SUDO_PROMPT` [environment variable](/index.php/Environment_variable "Environment variable") and include the [bell character](https://en.wikipedia.org/wiki/Bell_character "wikipedia:Bell character") `\a`. For example:

```
export SUDO_PROMPT=$'\a[sudo] password for %p: '

```

## Troubleshooting

### SSH TTY Problems

SSH does not allocate a tty by default when running a remote command. Without a tty, sudo cannot disable echo when prompting for a password. You can use ssh's `-t` option to force it to allocate a tty.

The `Defaults` option `requiretty` only allows the user to run sudo if they have a tty.

```
# Disable "ssh hostname sudo <cmd>", because it will show the password in clear text. You have to run "ssh -t hostname sudo <cmd>".
#
#Defaults    requiretty

```

### Permissive umask

Sudo will union the user's [umask](/index.php/Umask "Umask") value with its own umask (which defaults to 0022). This prevents sudo from creating files with more open permissions than the user's umask allows. While this is a sane default if no custom umask is in use, this can lead to situations where a utility run by sudo may create files with different permissions than if run by root directly. If errors arise from this, sudo provides a means to fix the umask, even if the desired umask is more permissive than the umask that the user has specified. Adding this (using `visudo`) will override sudo's default behavior:

```
Defaults umask = 0022
Defaults umask_override

```

This sets sudo's umask to root's default umask (0022) and overrides the default behavior, always using the indicated umask regardless of what umask the user as set.

### Defaults skeleton

The authors site has a [list of all the options](http://www.sudo.ws/sudo/sudoers.man.html#x5355444f455253204f5054494f4e53) that can be used with the `Defaults` command in the `/etc/sudoers` file.

See [[1]](https://gist.github.com/AladW/7eca9799b9ea624eca31) for a list of options (parsed from the version 1.8.7 source code) in a format optimized for `sudoers`.