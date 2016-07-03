The [OATH Toolkit](http://www.nongnu.org/oath-toolkit/index.html) provides a two-step authentication procedure using one-time passcodes (OTP). It complies to two OTP method RFC standards ([HOTP](https://en.wikipedia.org/wiki/HMAC-based_One-time_Password_Algorithm "w:HMAC-based One-time Password Algorithm"), [TOTP](https://en.wikipedia.org/wiki/Time-based_One-time_Password_Algorithm "w:Time-based One-time Password Algorithm")). The OTP generator applications are available for iOS, Android, Blackberry and other devices. Similar to [Google Authenticator](/index.php/Google_Authenticator "Google Authenticator") the authentication mechanism integrates into the Linux [PAM](/index.php/PAM "PAM") system. This guide shows the installation and configuration of this mechanism.

## Contents

*   [1 Installation](#Installation)
*   [2 Setting up the oath](#Setting_up_the_oath)
*   [3 Setting up the PAM](#Setting_up_the_PAM)
*   [4 Logging with an oath pass](#Logging_with_an_oath_pass)
*   [5 See also](#See_also)

## Installation

Install the [oath-toolkit](https://www.archlinux.org/packages/?name=oath-toolkit) package.

## Setting up the oath

The oath seed is an hexadecimal number that should be unique per user. To generate a new seed for a user, you could use the following command line:

```
$ head -10 /dev/urandom | sha512sum | cut -b 1-30
1ab4321412aebcw

```

Note the above output seed is used as example seed in this article and **must not** be used. There needs to be one oath per user and link to it in a configuration file `/etc/users.oath`. While being root create the file and insert the user seed:

 `/etc/users.oath` 
```
# Option User Prefix Seed
HOTP/T30/6 *user* - *1ab4321412aebcw*
```

Make sure that the file can only be accessed by root:

```
 # chmod 600 /etc/users.oath
 # chown root /etc/users.oath

```

## Setting up the PAM

To enable oath for a specific service only, like ssh, you can edit the file /etc/pam.d/sshd and add at the beginning of the file the following line :

```
 auth	  sufficient pam_oath.so usersfile=/etc/users.oath window=30 digits=6

```

This will allow authentification if you just enter the right oath code. You can make it a requirement and let the rest of the pam stack be processed if you use the following line instead :

```
 auth	  required pam_oath.so usersfile=/etc/users.oath window=30 digits=6

```

## Logging with an oath pass

Run the following command if you loggin and need the current oath pass :

```
 oathtool -v -d6 *1ab4321412aebcw*

```

Of course replace *1ab4321412aebcw* by the seed corresponding to your user. It will display something like that :

```
 Hex secret: 1ab4321412aebc
 Base32 secret: DK2DEFASV26A====
 Digits: 6
 Window size: 0
 Start counter: 0x0 (0)

```

```
 820170

```

The last number is actually the code you can use to log in right now, but more interestingly the Base32 secret, is actually what we need to generate a qr code for this user. To do so install the package [qrencode](https://www.archlinux.org/packages/?name=qrencode) to run the following command :

```
 qrencode -o *user*.png 'otpauth://totp/*user*@*machine*?secret=*DK2DEFASV26A===='*

```

Of course change *user*, *machine* and *DK2DEFASV26A====* accordingly. Once done, you can visualize your qrcode with your prefered image visualizer application and use that to configure your phone. It is pretty straigh forward to use FreeOTP to then take a screenshot of that png and get it to display OTP pass when needed.

**Note:** The secret key of your users is the most important information in this system. Once you setup a phone to provide OTP, it does have that key. The qr code in that png file does have that key. You need to take extra care of this file. They should only be stored on encrypted medium (Your phone need to be using encryption for any sane level of security). If not even confined in a sandbox like Samsung Knox to prevent third party application to potentially access them.

## See also

*   [Two-factor time based (TOTP) SSH authentication with pam_oath and Google Authenticator](http://spod.cx/blog/two-factor-ssh-auth-with-pam_oath-google-authenticator.shtml)
*   [pam_oath man page](http://www.nongnu.org/oath-toolkit/pam_oath.html)