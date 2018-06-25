[Google Authenticator](https://github.com/google/google-authenticator) provides a two-step authentication procedure using one-time passcodes ([OTP](https://en.wikipedia.org/wiki/One-time_pad "wikipedia:One-time pad")). The OTP generator application is available for iOS, Android and Blackberry. Similar to [S/KEY Authentication](/index.php/S/KEY_Authentication "S/KEY Authentication") the authentication mechanism integrates into the Linux [PAM](/index.php/PAM "PAM") system. This guide shows the installation and configuration of this mechanism.

For the reverse operation (generating codes compatible with Google Authenticator under Linux) see [#Code generation](#Code_generation) below.

## Contents

*   [1 Installation](#Installation)
*   [2 Setting up the PAM](#Setting_up_the_PAM)
*   [3 Generating a secret key file](#Generating_a_secret_key_file)
*   [4 Setting up your OTP-generator](#Setting_up_your_OTP-generator)
*   [5 Testing](#Testing)
*   [6 Storage location](#Storage_location)
*   [7 Desktop logins](#Desktop_logins)
*   [8 Code generation](#Code_generation)
    *   [8.1 Command line](#Command_line)

## Installation

Install [libpam-google-authenticator](https://www.archlinux.org/packages/?name=libpam-google-authenticator) package. Development version is also available with [google-authenticator-libpam-git](https://aur.archlinux.org/packages/google-authenticator-libpam-git/).

## Setting up the PAM

**Warning:** If you do all configuration via SSH do not close the session before you tested that everything is working, else you may lock yourself out. Furthermore consider generating the key file before activating the PAM.

Usually one demands two-pass authentication only for remote login. The corresponding PAM configuration file is `/etc/pam.d/sshd`. In case you want to use Google Authenticator globally you would need to change `/etc/pam.d/system-auth`, however, in this case proceed with extreme caution to not lock yourself out. In this guide we proceed with editing `/etc/pam.d/sshd` which is most safely (but not necessarily) done in a local session.

To enter both, your unix password and your OTP, add `pam_google_authenticator.so` above the system-remote-login lines to `/etc/pam.d/sshd`:

```
 **auth            required        pam_google_authenticator.so**
 auth            include         system-remote-login
 account         include         system-remote-login
 password        include         system-remote-login
 session         include         system-remote-login

```

This will ask for the OTP before prompting for your Unix password. Changing the order of the two modules will reverse this order.

**Warning:** Only users that have generated a secret key file (see below) will be allowed to log in using SSH.

To allow login with either the OTP or your Unix password use:

```
 auth            **sufficient**      pam_google_authenticator.so

```

Enable challenge-response authentication in `/etc/ssh/**sshd_config**`:

```
 ChallengeResponseAuthentication yes

```

Finally, [reload](/index.php/Reload "Reload") the `sshd` service.

**Warning:** OpenSSH will ignore all of this if you are authenticating with a SSH-key pair and have [disabled password logins](/index.php/Secure_Shell#Force_public_key_authentication "Secure Shell"). However, as of OpenSSH 6.2, you can add `AuthenticationMethods` to allow both: two-factor and key-based authentication. See [Secure Shell#Two-factor authentication and public keys](/index.php/Secure_Shell#Two-factor_authentication_and_public_keys "Secure Shell").

## Generating a secret key file

**Tip:** Install [qrencode](https://www.archlinux.org/packages/?name=qrencode) to generate a scannable QR. Scan the QR with the authenticator app to automatically configure the key.

Every user who wants to use two-pass authentication needs to generate a secret key file in his home folder. This can very easily be done using *google-authenticator*:

```
   $ google-authenticator
   Do you want authentication tokens to be time-based (y/n) y
   <Here you will see generated QR code>
   Your new secret key is: ZVZG5UZU4D7MY4DH
   Your verification code is 269371
   Your emergency scratch codes are:
     70058954
     97277505
     99684896
     56514332
     82717798

   Do you want me to update your "/home/username/.google_authenticator" file (y/n) y

   Do you want to disallow multiple uses of the same authentication
   token? This restricts you to one login about every 30s, but it increases
   your chances to notice or even prevent man-in-the-middle attacks (y/n) y

   By default, tokens are good for 30 seconds and in order to compensate for
   possible time-skew between the client and the server, we allow an extra
   token before and after the current time. If you experience problems with poor
   time synchronization, you can increase the window from its default
   size of 1:30min to about 4min. Do you want to do so (y/n) n

   If the computer that you are logging into is not hardened against brute-force
   login attempts, you can enable rate-limiting for the authentication module.
   By default, this limits attackers to no more than 3 login attempts every 30s.
   Do you want to enable rate-limiting (y/n) y

```

It is recommended to **store the emergency scratch codes safely** (print them out and keep them in a safe location) as they are your only way to log in (via SSH) when you lost your mobile phone (i.e. your OTP-generator). They are also stored in `~/.google_authenticator`, so you can look them up any time as long as you are logged in.

## Setting up your OTP-generator

Install generator application on your mobile phone from [Android market](http://m.google.com/authenticator) (e.g. [FreeOTP](https://play.google.com/store/apps/details?id=org.fedorahosted.freeotp)) or from [F-Droid](https://f-droid.org/repository/browse/?fdfilter=google&fdid=com.google.android.apps.authenticator2). In the applications menu click the corresponding button to create a new account and either scan the QR code from the URL you were told when generating the secret key file, or enter the secret key (in the example above 'ZVZG5UZU4D7MY4DH') manually.

Now you should see a new passcode token being generated every 30 seconds on your phone.

## Testing

SSH to your host from another machine and/or from another terminal window:

```
 $ ssh hostname
 login as: <username>
 Verification code: <generated/backup-code>
 Password: <password>
 $

```

## Storage location

If you want to change the secret key files' storage path, you can use the flag `--secret`:

```
$ google-authenticator --secret="/**PATH_FOLDER**/**USERNAME**"

```

Then, don't forget to change the location path for PAM, in `/etc/pam.d/sshd`:

 `/etc/pam.d/sshd`  `auth required pam_google_authenticator.so user=root secret=/**PATH_FOLDER**/${USER}` 

`user=root` is used to force PAM to search the file using root user.

Also, take care with the permissions of the secret key file. Indeed, the file **must** be only-readable by the owner (chmod: `400`). Here, the owner is root.

```
$ chown root.root /**PATH_FILE**/**SECRET_KEY_FILES**
  chmod 400 /**PATH_FILE**/**SECRET_KEY_FILES**

```

## Desktop logins

The Google Authenticator PAM plugin can also be used for console logins and with GDM. Just add the following to `/etc/pam.d/login` or the `/etc/pam.d/gdm-password` file:

```
   auth required pam_google_authenticator.so

```

## Code generation

If you have Google Authenticator configured with other systems, then losing your device can prevent you from being able to log in to those systems. Having additional ways to generate the codes can be helpful.

### Command line

The easiest way to generate codes is with `oath-tool`. It is available in the [oath-toolkit](https://www.archlinux.org/packages/?name=oath-toolkit) package, and can be used as follows:

```
oathtool --totp -b ABC123

```

Where `ABC123` is the secret key.

On most Android systems with sufficient user access, the Google Authenticator database can be copied off the device and accessed directly, as it is an sqlite3 database. This shell script will read a Google Authenticator database and generate live codes for each key found:

 `google-authenticator.sh` 
```
#!/bin/sh

# This is the path to the Google Authenticator app file.  It's typically located
# in /data under Android.  Copy it to your PC in a safe location and specify the
# path to it here.
DB="/path/to/com.google.android.apps.authenticator/databases/databases"

sqlite3 "$DB" 'SELECT email,secret FROM accounts;' | while read A
do
        NAME=`echo "$A" | cut -d '|' -f 1`
        KEY=`echo "$A" | cut -d '|' -f 2`
        CODE=`oathtool --totp -b "$KEY"`
        echo -e "\e[1;32m$CODE\e[0m - \e[1;33m$NAME\e[0m"
done
```