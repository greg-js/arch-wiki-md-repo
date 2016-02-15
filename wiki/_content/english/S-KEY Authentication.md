This guide shows you how you can enable S/KEY one-time password authentication on your Arch.

**Warning:** Do following actions on secure connection from a secure computer. A chain is as strong as its weakest link.

## Contents

*   [1 Install opie](#Install_opie)
*   [2 Config pam module](#Config_pam_module)
*   [3 Create an OTP key](#Create_an_OTP_key)
*   [4 Get yourself some passwords](#Get_yourself_some_passwords)

## Install opie

Install the following packages from the [AUR](/index.php/AUR "AUR"):

*   [pam-opie](https://aur.archlinux.org/packages/pam-opie/)
*   [opie](https://aur.archlinux.org/packages/opie/)

## Config pam module

In /etc/pam.d tweak config files for wanted logins. I tweaked sshd and sudo. Do the following to selected files:

```
auth  required  pam_unix.so
change to (note order)-->
auth sufficient pam_unix.so
auth sufficient pam_opie.so

```

If you want to use SSH, change ChallengeResponseAuthentication to yes in /etc/ssh/sshd_config

## Create an OTP key

As your user (no root), run:

```
# opiepasswd -c

```

After entering a passphrase you get your OTP key:

```
ID busk OTP key is 499 fe6839
MIRE MORE ODE DOME REAM

```

## Get yourself some passwords

```
# opiekey -n 20 499 fe6839

```

OR alternative way for Java-enabled mobile phone owners: Get [VeJotp](http://fatsquirrel.org/software/vejotp/), It's free and you can generate passwords on the run.

Now, when you ssh to your box, hit Enter to the password prompt and you will be prompted for onetime password.

This guide is based on [[1]](http://busk.blogs.lysator.liu.se/2009/12/12/skey-one-time-passwords-using-opie/)