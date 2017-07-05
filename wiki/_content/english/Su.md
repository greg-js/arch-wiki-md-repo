The **su** command (**s**ubstitute **u**ser) is used to assume the identity of another user on the system, normally root. This saves having to logout and log back in as the user you want to be. Instead, you may login as another user **during** your session by starting a sort of "sub-session", and then logout back to your own session when done.

## Contents

*   [1 Installation](#Installation)
*   [2 Usage](#Usage)
*   [3 Sudo, an alternative](#Sudo.2C_an_alternative)
*   [4 Tips and tricks](#Tips_and_tricks)
    *   [4.1 Login shell](#Login_shell)
    *   [4.2 su and wheel](#su_and_wheel)

## Installation

su is part of [util-linux](https://www.archlinux.org/packages/?name=util-linux) package, which is installed by default in Arch as member of [base](https://www.archlinux.org/groups/x86_64/base/) group.

## Usage

To assume the login of another user, pass the username that you want to become to su, as in:

```
# su *username*

```

You will be prompted for the password of the user you are attempting to become.

If no username is passed, su assumes the root user, and the password for which you are prompted will be that of root.

## Sudo, an alternative

[sudo](/index.php/Sudo "Sudo") is a more configurable program that can provide similar functionality to su, and can be a replacement for su, depending on specific requirements and threat models. The sudo system will prompt you for your own password – or no password at all, if configured in such a way – rather than that of the target user (the user account you are attempting to use). This way you do not have to share passwords between users, and if you ever need to stop a user having root access (or access to any other account, for that matter), you do not have to change the root password, which is an inconvenience to everyone else; you only need to revoke that user's sudo access.

If sudo has been configured to allow the user to run root's shell, the user can run `sudo -s` or `sudo -i` to mimic `su` or `su -l`, respectively, and supply his own password or no password rather than root's password. Similarly, `sudo -u john -i` mimics `su -l john` if you are allowed to run john's shell.

## Tips and tricks

### Login shell

The default behavior of su is to remain within the current directory and to maintain the environmental variables of the original user (rather than switch to those of the new user).

Note the following important contrasting considerations:

*   It sometimes can be advantageous for a system administrator to use the shell account of an ordinary user rather than its own. In particular, occasionally the most efficient way to solve a user's problem is to log into that user's account in order to reproduce or debug the problem.

*   However, in many situations it is not desirable, or it can even be dangerous, for the root user to be operating from an ordinary user's shell account and with that account's environmental variables rather than from its own. While inadvertently using an ordinary user's shell account, root could install a program or make other changes to the system that would not have the same result as if they were made while using the root account. For instance, a program could be installed that could give the ordinary user power to accidentally damage the system or gain unauthorized access to certain data.

Thus, it is advisable that administrative users, as well as any other users that are authorized to use su (and it is suggested that there be very few, if any) acquire the habit of always running the su command with the `-l`/`--login` option. It has two effects:

1.  switches from the current directory to the home directory of the new user (e.g., to `/root` in the case of the root user) by *logging in* as that user
2.  changes the environmental variables to those of the new user as dictated by their `~/.bashrc`. That is, the current directory and environment will be changed to what would be expected if the new user had actually logged on to a new session (rather than just taking over an existing session).

Thus, administrators should generally use su as follows:

```
$ su -l

```

An identical result is produced by adding the username root:

```
$ su -l root

```

Likewise, the same can be done for any other user (e.g. for a user named archie):

```
# su -l archie

```

You may wish to add an alias to `~/.bashrc` for this:

```
alias su="su -l"

```

### su and wheel

BSD su allows only members of the "wheel" [group](/index.php/Group "Group") to assume root's identity by default. This is not the default behavior of GNU su, but this behavior can be mimicked using [PAM](/index.php/PAM "PAM"). Uncomment the appropriate line in `/etc/pam.d/su` and `/etc/pam.d/su-l`:

```
auth required pam_wheel.so use_uid

```