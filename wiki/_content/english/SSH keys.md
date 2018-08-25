SSH keys serve as a means of identifying yourself to an SSH server using [public-key cryptography](https://en.wikipedia.org/wiki/Public-key_cryptography "wikipedia:Public-key cryptography") and [challenge-response authentication](https://en.wikipedia.org/wiki/Challenge-response_authentication "wikipedia:Challenge-response authentication"). One immediate advantage this method has over traditional password authentication is that you can be authenticated by the server without ever having to send your password over the network. Anyone eavesdropping on your connection will not be able to intercept and crack your password because it is never actually transmitted. Additionally, using SSH keys for authentication virtually eliminates the risk posed by brute-force password attacks by drastically reducing the chances of the attacker correctly guessing the proper credentials.

As well as offering additional security, SSH key authentication can be more convenient than the more traditional password authentication. When used with a program known as an SSH agent, SSH keys can allow you to connect to a server, or multiple servers, without having to remember or enter your password for each system.

SSH keys are not without their drawbacks and may not be appropriate for all environments, but in many circumstances they can offer some strong advantages. A general understanding of how SSH keys work will help you decide how and when to use them to meet your needs.

This article assumes you already have a basic understanding of the [Secure Shell](/index.php/Secure_Shell "Secure Shell") protocol and have [installed](/index.php/Install "Install") the [openssh](https://www.archlinux.org/packages/?name=openssh) package.

## Contents

*   [1 Background](#Background)
*   [2 Generating an SSH key pair](#Generating_an_SSH_key_pair)
    *   [2.1 Choosing the authentication key type](#Choosing_the_authentication_key_type)
        *   [2.1.1 RSA](#RSA)
        *   [2.1.2 ECDSA](#ECDSA)
        *   [2.1.3 Ed25519](#Ed25519)
    *   [2.2 Choosing the key location and passphrase](#Choosing_the_key_location_and_passphrase)
        *   [2.2.1 Changing the private key's passphrase without changing the key](#Changing_the_private_key.27s_passphrase_without_changing_the_key)
        *   [2.2.2 Managing multiple keys](#Managing_multiple_keys)
*   [3 Copying the public key to the remote server](#Copying_the_public_key_to_the_remote_server)
    *   [3.1 Simple method](#Simple_method)
    *   [3.2 Manual method](#Manual_method)
*   [4 SSH agents](#SSH_agents)
    *   [4.1 ssh-agent](#ssh-agent)
        *   [4.1.1 Start ssh-agent with systemd user](#Start_ssh-agent_with_systemd_user)
        *   [4.1.2 ssh-agent as a wrapper program](#ssh-agent_as_a_wrapper_program)
    *   [4.2 GnuPG Agent](#GnuPG_Agent)
    *   [4.3 Keychain](#Keychain)
        *   [4.3.1 Installation](#Installation)
        *   [4.3.2 Configuration](#Configuration)
        *   [4.3.3 Tips](#Tips)
    *   [4.4 x11-ssh-askpass](#x11-ssh-askpass)
        *   [4.4.1 Calling x11-ssh-askpass with ssh-add](#Calling_x11-ssh-askpass_with_ssh-add)
        *   [4.4.2 Theming](#Theming)
        *   [4.4.3 Alternative passphrase dialogs](#Alternative_passphrase_dialogs)
    *   [4.5 pam_ssh](#pam_ssh)
        *   [4.5.1 Using a different password to unlock the SSH key](#Using_a_different_password_to_unlock_the_SSH_key)
        *   [4.5.2 Known issues with pam_ssh](#Known_issues_with_pam_ssh)
    *   [4.6 GNOME Keyring](#GNOME_Keyring)
    *   [4.7 Store SSH keys with Kwallet](#Store_SSH_keys_with_Kwallet)
    *   [4.8 KeePass2 with KeeAgent plugin](#KeePass2_with_KeeAgent_plugin)
    *   [4.9 KeePassXC](#KeePassXC)
*   [5 Troubleshooting](#Troubleshooting)
    *   [5.1 Key ignored by the server](#Key_ignored_by_the_server)
*   [6 See also](#See_also)

## Background

SSH keys are always generated in pairs with one known as the private key and the other as the public key. The private key is known only to you and it should be safely guarded. By contrast, the public key can be shared freely with any SSH server to which you wish to connect.

If an SSH server has your public key on file and sees you requesting a connection, it uses your public key to construct and send you a challenge. This challenge is an encrypted message and it must be met with the appropriate response before the server will grant you access. What makes this coded message particularly secure is that it can only be understood by the private key holder. While the public key can be used to encrypt the message, it cannot be used to decrypt that very same message. Only you, the holder of the private key, will be able to correctly understand the challenge and produce the proper response.

This challenge-response phase happens behind the scenes and is invisible to the user. As long as you hold the private key, which is typically stored in the `~/.ssh/` directory, your SSH client should be able to reply with the appropriate response to the server.

A private key is a guarded secret and as such it is advisable to store it on disk in an encrypted form. When the encrypted private key is required, a passphrase must first be entered in order to decrypt it. While this might superficially appear as though you are providing a login password to the SSH server, the passphrase is only used to decrypt the private key on the local system. The passphrase is not transmitted over the network.

If you do use a private key passphrase, and you do not pass the `-o` option to *ssh-keygen*, your password will be encrypted with the MD5 hash function, which is not a secure password encryption method. If you use a password to encrypt your key, use the `-o` option. This will make your key incompatible with OpenSSH versions older than 6.5.

## Generating an SSH key pair

An SSH key pair can be generated by running the `ssh-keygen` command, defaulting to 2048-bit RSA (and SHA256) which the [ssh-keygen(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/ssh-keygen.1) man page says is "*generally considered sufficient*" and should be compatible with virtually all clients and servers:

```
$ ssh-keygen

```

```
Generating public/private rsa key pair.
Enter file in which to save the key (/home/<username>/.ssh/id_rsa): 
Enter passphrase (empty for no passphrase): 
Enter same passphrase again: 
Your identification has been saved in /home/<username>/.ssh/id_rsa.
Your public key has been saved in /home/<username>/.ssh/id_rsa.pub.
The key fingerprint is:
SHA256:gGJtSsV8BM+7w018d39Ji57F8iO6c0N2GZq3/RY2NhI username@hostname
The key's randomart image is:
+---[RSA 2048]----+
|   ooo.          |
|   oo+.          |
|  + +.+          |
| o +   +     E . |
|  .   . S . . =.o|
|     . + . . B+@o|
|      + .   oo*=O|
|       .   ..+=o+|
|           o=ooo+|
+----[SHA256]-----+
```

The [randomart image](http://www.cs.berkeley.edu/~dawnsong/papers/randomart.pdf) was [introduced in OpenSSH 5.1](http://www.openssh.com/txt/release-5.1) as an easier means of visually identifying the key fingerprint.

**Note:** If you set a passphrase for your key, it is *strongly encouraged* to use the `-o` option to *ssh-keygen*. This will save your private key in the new OpenSSH format, which has greatly increased resistance to brute-force password cracking, but is not supported by versions of OpenSSH prior to 6.5\. According to [ssh-keygen(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/ssh-keygen.1), Ed25519 keys always use the new private key format. Also use the `-a` switch to specify the number of KDF rounds on the password encryption.

You can also add an optional comment field to the public key with the `-C` switch, to more easily identify it in places such as `~/.ssh/known_hosts`, `~/.ssh/authorized_keys` and `ssh-add -L` output. For example:

```
$ ssh-keygen -C "$(whoami)@$(hostname)-$(date -I)"

```

will add a comment saying which user created the key on which machine and when.

### Choosing the authentication key type

OpenSSH supports several signing algorithms (for authentication keys) which can be divided in two groups depending on the mathematical properties they exploit:

1.  [DSA](https://en.wikipedia.org/wiki/Digital_Signature_Algorithm "wikipedia:Digital Signature Algorithm") and [RSA](https://en.wikipedia.org/wiki/RSA_(cryptosystem) "wikipedia:RSA (cryptosystem)"), which rely on the [practical difficulty](https://en.wikipedia.org/wiki/Integer_factorization#Difficulty_and_complexity "wikipedia:Integer factorization") of factoring the product of two large prime numbers,
2.  [ECDSA](https://en.wikipedia.org/wiki/Elliptic_Curve_Digital_Signature_Algorithm "wikipedia:Elliptic Curve Digital Signature Algorithm") and [Ed25519](https://en.wikipedia.org/wiki/Curve25519 "wikipedia:Curve25519"), which rely on the elliptic curve [discrete logarithm](https://en.wikipedia.org/wiki/Discrete_logarithm "wikipedia:Discrete logarithm") problem. ([example](https://www.certicom.com/content/certicom/en/52-the-elliptic-curve-discrete-logarithm-problem.html))

[Elliptic curve cryptography](https://blog.cloudflare.com/a-relatively-easy-to-understand-primer-on-elliptic-curve-cryptography/) (ECC) algorithms are a [more recent addition](https://en.wikipedia.org/wiki/Elliptic_curve_cryptography#History "wikipedia:Elliptic curve cryptography") to public key cryptosystems. One of their main advantages is their ability to provide [the same level of security with smaller keys](https://en.wikipedia.org/wiki/Elliptic_curve_cryptography#Rationale "wikipedia:Elliptic curve cryptography"), which makes for less computationally intensive operations (*i.e.* faster key creation, encryption and decryption) and reduced storage and transmission requirements.

OpenSSH 7.0 [deprecated and disabled support for DSA keys](https://www.archlinux.org/news/openssh-70p1-deprecates-ssh-dss-keys/) due to discovered vulnerabilities, therefore the choice of [cryptosystem](https://en.wikipedia.org/wiki/cryptosystem "wikipedia:cryptosystem") lies within RSA or one of the two types of ECC.

[#RSA](#RSA) keys will give you the greatest portability, while [#Ed25519](#Ed25519) will give you the best security but requires recent versions of client & server[[1]](https://www.gentoo.org/support/news-items/2015-08-13-openssh-weak-keys.html). [#ECDSA](#ECDSA) is likely more compatible than Ed25519 (though still less than RSA), but suspicions exist about its security (see below).

**Note:** These keys are used only to authenticate you; choosing stronger keys will not increase CPU load when transferring data over SSH.

#### RSA

`ssh-keygen` defaults to RSA therefore there is no need to specify it with the `-t` option. It provides the best compatibility of all algorithms but requires the key size to be larger to provide sufficient security.

Minimum key size is 1024 bits, default is 2048 (see [ssh-keygen(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/ssh-keygen.1)) and maximum is 16384.

If you wish to generate a stronger RSA key pair (*e.g.* to guard against cutting-edge or unknown attacks and more sophisticated attackers), simply specify the `-b` option with a higher bit value than the default:

```
$ ssh-keygen -b 4096

```

```
Generating public/private rsa key pair.
Enter file in which to save the key (/home/<username>/.ssh/id_rsa):
Enter passphrase (empty for no passphrase):
Enter same passphrase again:
Your identification has been saved in /home/<username>/.ssh/id_rsa.
Your public key has been saved in /home/<username>/.ssh/id_rsa.pub.
The key fingerprint is:
SHA256:+Pqo84NC+vAQQ9lUV0z+/zPHsyCe8oZpy6hLkIa7qfk <username>@<hostname>
The key's randomart image is:
+---[RSA 4096]----+
|   ... .+o       |
|  +   . ..       |
| o .     .       |
|. . .  .  .      |
|o. +  . S  .     |
| o+ .  .    .    |
|o+   o  . o. o . |
|.=+ + .oo=..o o+o|
|+=E..**+oo=+   o*|
+----[SHA256]-----+
```

Be aware though that there are diminishing returns in using longer keys.[[2]](https://security.stackexchange.com/a/25377)[[3]](https://www.gnupg.org/faq/gnupg-faq.html#no_default_of_rsa4096) The GnuPG FAQ reads: "*If you need more security than RSA-2048 offers, the way to go would be to switch to elliptical curve cryptography — not to continue using RSA*".[[4]](https://www.gnupg.org/faq/gnupg-faq.html#please_use_ecc)

On the other hand, the latest iteration of the [NSA Fact Sheet Suite B Cryptography](https://www.nsa.gov/ia/programs/suiteb_cryptography/index.shtml) suggests a minimum 3072-bit modulus for RSA while "*[preparing] for the upcoming quantum resistant algorithm transition*".[[5]](http://www.keylength.com/en/6/)

#### ECDSA

The Elliptic Curve Digital Signature Algorithm (ECDSA) was introduced as the preferred algorithm for authentication [in OpenSSH 5.7](http://www.openssh.com/txt/release-5.7). Some vendors also disable the required implementations due to potential patent issues.

There are two sorts of concerns with it:

1.  *Political concerns*, the trustworthiness of NIST-produced curves [being questioned](https://crypto.stackexchange.com/questions/10263/should-we-trust-the-nist-recommended-ecc-parameters) after revelations that the NSA willingly inserts backdoors into softwares, hardware components and published standards were made; well-known cryptographers [have](https://www.schneier.com/blog/archives/2013/09/the_nsa_is_brea.html#c1675929) [expressed](http://safecurves.cr.yp.to/rigid.html) [doubts](https://www.hyperelliptic.org/tanja/vortraege/20130531.pdf) about how the NIST curves were designed, and voluntary tainting has already [been](https://www.schneier.com/blog/archives/2007/11/the_strange_sto.html) [proved](http://www.scientificamerican.com/article/nsa-nist-encryption-scandal/) in the past.
2.  *Technical concerns*, about the [difficulty to properly implement the standard](http://blog.cr.yp.to/20140323-ecdsa.html) and the [slowness and design flaws](http://www.gossamer-threads.com/lists/openssh/dev/57162#57162) which reduce security in insufficiently precautious implementations.

Both of those concerns are best summarized in [libssh curve25519 introduction](https://git.libssh.org/projects/libssh.git/tree/doc/curve25519-sha256@libssh.org.txt#n4). Although the political concerns are still subject to debate, there is a [clear consensus](https://news.ycombinator.com/item?id=7597653) that [#Ed25519](#Ed25519) is technically superior and should therefore be preferred.

#### Ed25519

[Ed25519](http://ed25519.cr.yp.to/) was introduced in [OpenSSH 6.5](http://www.openssh.com/txt/release-6.5) of January 2014: "*Ed25519 is an elliptic curve signature scheme that offers better security than ECDSA and DSA and good performance*". Its main strengths are its speed, its constant-time run time (and resistance against side-channel attacks), and its lack of nebulous hard-coded constants.[[6]](https://git.libssh.org/projects/libssh.git/tree/doc/curve25519-sha256@libssh.org.txt) See also [this blog post](https://blog.mozilla.org/warner/2011/11/29/ed25519-keys/) by a Mozilla developer on how it works.

It is already implemented in [many applications and libraries](https://en.wikipedia.org/wiki/Curve25519#Popularity "wikipedia:Curve25519") and is the [default key exchange algorithm](https://www.libssh.org/2013/11/03/openssh-introduces-curve25519-sha256libssh-org-key-exchange/) (which is different from key *signature*) in OpenSSH.

Ed25519 key pairs can be generated with:

```
$ ssh-keygen -t ed25519

```

There is no need to set the key size, as all Ed25519 keys are 256 bits. Also, they rely on a [new key format](http://www.gossamer-threads.com/lists/openssh/dev/57162#57162) which "*uses a bcrypt-based key derivation function that makes brute-force attacks against stolen private keys far slower*".

For those reasons, compatibility with older versions of OpenSSH or [other SSH clients and servers](/index.php/Ssh#Other_SSH_clients_and_servers "Ssh") may prove troublesome.

### Choosing the key location and passphrase

Upon issuing the `ssh-keygen` command, you will be prompted for the desired name and location of your private key. By default, keys are stored in the `~/.ssh/` directory and named according to the type of encryption used. You are advised to accept the default name and location in order for later code examples in this article to work properly.

When prompted for a passphrase, choose something that will be hard to guess if you have the security of your private key in mind. A longer, more random password will generally be stronger and harder to crack should it fall into the wrong hands.

It is also possible to create your private key without a passphrase. While this can be convenient, you need to be aware of the associated risks. Without a passphrase, your private key will be stored on disk in an unencrypted form. Anyone who gains access to your private key file will then be able to assume your identity on any SSH server to which you connect using key-based authentication. Furthermore, without a passphrase, you must also trust the root user, as he can bypass file permissions and will be able to access your unencrypted private key file at any time.

**Note:** The old, default password encoding for *ssh* private keys keys **is insecure**; it is only a single round of an MD5 hash. Since OpenSSH version 6.5, use the `-o` option to `ssh-keygen` to encode your private key in a new, more secure format.

#### Changing the private key's passphrase without changing the key

If the originally chosen SSH key passphrase is undesirable or must be changed, one can use the `ssh-keygen` command to change the passphrase without changing the actual key.

To upgrade your private RSA key to use the more secure password encryption format, and also change the passphrase, run the following command:

```
$ ssh-keygen -o -f ~/.ssh/id_rsa -p

```

Otherwise, to use the old key format, run the following command:

```
$ ssh-keygen -f ~/.ssh/id_rsa -p

```

#### Managing multiple keys

It is possible —although [not considered best practice](http://security.stackexchange.com/questions/10963/whats-the-common-pragmatic-strategy-for-managing-key-pairs)— to use the same SSH key pair for multiple hosts.

On the other hand, it is rather easy to maintain distinct keys for multiple hosts by using the `IdentityFile` directive in your openSSH config file:

 `~/.ssh/config` 
```
Host SERVER1
   IdentitiesOnly yes
   IdentityFile ~/.ssh/id_rsa_SERVER1

Host SERVER2
   IdentitiesOnly yes
   IdentityFile ~/.ssh/id_ed25519_SERVER2

```

See [ssh_config(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/ssh_config.5) for full description of these options.

## Copying the public key to the remote server

Once you have generated a key pair, you will need to copy the public key to the remote server so that it will use SSH key authentication. The public key file shares the same name as the private key except that it is appended with a `.pub` extension. Note that the private key is not shared and remains on the local machine.

### Simple method

**Note:** This method might fail if the remote server uses a non-`sh` shell such as `tcsh` as default and uses OpenSSH older than 6.6.1p1\. See [this bug report](https://bugzilla.redhat.com/show_bug.cgi?id=1045191).

If your key file is `~/.ssh/id_rsa.pub` you can simply enter the following command.

```
$ ssh-copy-id remote-server.org

```

If your username differs on remote machine, be sure to prepend the username followed by `@` to the server name.

```
$ ssh-copy-id username@remote-server.org

```

If your public key filename is anything other than the default of `~/.ssh/id_rsa.pub` you will get an error stating `/usr/bin/ssh-copy-id: ERROR: No identities found`. In this case, you must explicitly provide the location of the public key.

```
$ ssh-copy-id -i ~/.ssh/id_ed25519.pub username@remote-server.org

```

If the ssh server is listening on a port other than default of 22, be sure to include it within the host argument.

```
$ ssh-copy-id -i ~/.ssh/id_ed25519.pub -p 221 username@remote-server.org

```

### Manual method

By default, for OpenSSH, the public key needs to be concatenated with `~/.ssh/authorized_keys`. Begin by copying the public key to the remote server.

```
$ scp ~/.ssh/id_ecdsa.pub username@remote-server.org:

```

The above example copies the public key (`id_ecdsa.pub`) to your home directory on the remote server via `scp`. Do not forget to include the `:` at the end of the server address. Also note that the name of your public key may differ from the example given.

On the remote server, you will need to create the `~/.ssh` directory if it does not yet exist and append your public key to the `authorized_keys` file.

```
$ ssh username@remote-server.org
username@remote-server.org's password:
$ mkdir ~/.ssh
$ chmod 700 ~/.ssh
$ cat ~/id_ecdsa.pub >> ~/.ssh/authorized_keys
$ rm ~/id_ecdsa.pub
$ chmod 600 ~/.ssh/authorized_keys

```

The last two commands remove the public key file from the server and set the permissions on the `authorized_keys` file such that it is only readable and writable by you, the owner.

## SSH agents

If your private key is encrypted with a passphrase, this passphrase must be entered every time you attempt to connect to an SSH server using public-key authentication. Each individual invocation of `ssh` or `scp` will need the passphrase in order to decrypt your private key before authentication can proceed.

An SSH agent is a program which caches your decrypted private keys and provides them to SSH client programs on your behalf. In this arrangement, you must only provide your passphrase once, when adding your private key to the agent's cache. This facility can be of great convenience when making frequent SSH connections.

An agent is typically configured to run automatically upon login and persist for the duration of your login session. A variety of agents, front-ends, and configurations exist to achieve this effect. This section provides an overview of a number of different solutions which can be adapted to meet your specific needs.

### ssh-agent

`ssh-agent` is the default agent included with OpenSSH. It can be used directly or serve as the back-end to a few of the front-end solutions mentioned later in this section. When `ssh-agent` is run, it forks to background and prints necessary environment variables. E.g.

 `$ ssh-agent` 
```
SSH_AUTH_SOCK=/tmp/ssh-vEGjCM2147/agent.2147; export SSH_AUTH_SOCK;
SSH_AGENT_PID=2148; export SSH_AGENT_PID;
echo Agent pid 2148;
```

To make use of these variables, run the command through the `eval` command.

 `$ eval $(ssh-agent)` 
```
Agent pid 2157

```

Once `ssh-agent` is running, you will need to add your private key to its cache:

 `$ ssh-add ~/.ssh/id_ed25519` 
```
Enter passphrase for /home/user/.ssh/id_ed25519:
Identity added: /home/user/.ssh/id_ed25519 (/home/user/.ssh/id_ed25519)

```

If your private key is encrypted, `ssh-add` will prompt you to enter your passphrase. Once your private key has been successfully added to the agent you will be able to make SSH connections without having to enter your passphrase.

**Tip:** To make all `ssh` clients, including `git` store keys in the agent on first use, add the configuration setting `AddKeysToAgent yes` to `~/.ssh/config`. Other possible values are `confirm`, `ask` and `no` (default).

In order to start the agent automatically and make sure that only one `ssh-agent` process runs at a time, add the following to your `~/.bashrc`:

```
if ! pgrep -u "$USER" ssh-agent > /dev/null; then
    ssh-agent > ~/.ssh-agent-thing
fi
if [[ "$SSH_AGENT_PID" == "" ]]; then
    eval "$(<~/.ssh-agent-thing)"
fi

```

This will run a `ssh-agent` process if there is not one already, and save the output thereof. If there is one running already, we retrieve the cached `ssh-agent` output and evaluate it which will set the necessary environment variables.

There also exist a number of front-ends to `ssh-agent` and alternative agents described later in this section which avoid this problem.

#### Start ssh-agent with systemd user

It is possible to use the [systemd/User](/index.php/Systemd/User "Systemd/User") facilities to start the agent.

 `~/.config/systemd/user/ssh-agent.service` 
```
[Unit]
Description=SSH key agent

[Service]
Type=simple
Environment=SSH_AUTH_SOCK=%t/ssh-agent.socket
ExecStart=/usr/bin/ssh-agent -D -a $SSH_AUTH_SOCK

[Install]
WantedBy=*default*.target

```

Add `SSH_AUTH_SOCK DEFAULT="${XDG_RUNTIME_DIR}/ssh-agent.socket"` to `~/.pam_environment`. Then [enable](/index.php/Enable "Enable") or [start](/index.php/Start "Start") the service.

**Note:** If you use GNOME, this environment variable is overridden by default. See [GNOME/Keyring#Disable keyring daemon components](/index.php/GNOME/Keyring#Disable_keyring_daemon_components "GNOME/Keyring").

#### ssh-agent as a wrapper program

An alternative way to start ssh-agent (with, say, each X session) is described in [this ssh-agent tutorial by UC Berkeley Labs](http://upc.lbl.gov/docs/user/sshagent.shtml). A basic use case is if you normally begin X with the `startx` command, you can instead prefix it with `ssh-agent` like so:

```
$ ssh-agent startx

```

And so you do not even need to think about it you can put an alias in your `.bash_aliases` file or equivalent:

```
alias startx='ssh-agent startx'

```

Doing it this way avoids the problem of having extraneous `ssh-agent` instances floating around between login sessions. Exactly one instance will live and die with the entire X session.

**Note:** As an alternative to calling `ssh-agent startx`, you can add `eval $(ssh-agent)` to `~/.xinitrc`.

See [the below notes on using x11-ssh-askpass with ssh-add](#Calling_x11-ssh-askpass_with_ssh-add) for an idea on how to immediately add your key to the agent.

### GnuPG Agent

The [gpg-agent](/index.php/GnuPG#gpg-agent "GnuPG") has OpenSSH agent emulation. See [GnuPG#SSH agent](/index.php/GnuPG#SSH_agent "GnuPG") for necessary configuration.

### Keychain

[Keychain](http://www.funtoo.org/Keychain) is a program designed to help you easily manage your SSH keys with minimal user interaction. It is implemented as a shell script which drives both *ssh-agent* and *ssh-add*. A notable feature of Keychain is that it can maintain a single *ssh-agent* process across multiple login sessions. This means that you only need to enter your passphrase once each time your local machine is booted.

#### Installation

[Install](/index.php/Install "Install") the [keychain](https://www.archlinux.org/packages/?name=keychain) package.

#### Configuration

**Warning:** As of 2015-09-26, the `-Q, --quick` option has the unexpected side-effect of making *keychain* switch to a newly-spawned *ssh-agent* upon relogin (at least on systems using [GNOME](/index.php/GNOME "GNOME")), forcing you to re-add all the previously registered keys.

Add a line similar to the following to your [shell](/index.php/Shell "Shell") configuration file, *e.g.* if using [Bash](/index.php/Bash "Bash"):

 `~/.bashrc` 
```
eval $(keychain --eval --quiet id_ed25519 id_rsa ~/.keys/my_custom_key)

```

**Note:** `~/.bashrc` is used instead of the upstream suggested `~/.bash_profile` because on Arch it is sourced by both login and non-login shells, making it suitable for textual and graphical environments alike. See [Bash#Invocation](/index.php/Bash#Invocation "Bash") for more information on the difference between those.

In the above example,

*   the `--eval` switch outputs lines to be evaluated by the opening `eval` command; this sets the necessary environments variables for SSH client to be able to find your agent.
*   `--quiet` will limit output to warnings, errors, and user prompts.

Multiple keys can be specified on the command line, as shown in the example. By default keychain will look for key pairs in the `~/.ssh/` directory, but absolute path can be used for keys in non-standard location. You may also use the `--confhost` option to inform keychain to look in `~/.ssh/config` for `IdentityFile` settings defined for particular hosts, and use these paths to locate keys.

See `keychain --help` or [keychain(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/keychain.1) for details on setting *keychain* for other shells.

To test Keychain, simply open a new terminal emulator or log out and back in your session. It should prompt you for the passphrase of the specified private key(s) (if applicable), either using the program set in `$SSH_ASKPASS` or on the terminal.

Because Keychain reuses the same *ssh-agent* process on successive logins, you should not have to enter your passphrase the next time you log in or open a new terminal. You will only be prompted for your passphrase once each time the machine is rebooted.

#### Tips

*   *keychain* expects public key files to exist in the same directory as their private counterparts, with a `.pub` extension. If the private key is a symlink, the public key can be found alongside the symlink or in the same directory as the symlink target (this capability requires the `readlink` command to be available on the system).

*   to disable the graphical prompt and always enter your passphrase on the terminal, use the `--nogui` option. This allows to copy-paste long passphrases from a password manager for example.

*   if you do not want to be immediately prompted for unlocking the keys but rather wait until they are needed, use the `--noask` option.

**Note:** Keychain is able to manage [GPG](/index.php/GPG "GPG") keys in the same fashion. By default it attempts to start *ssh-agent* only, but you can modify this behavior using the `--agents` option, *e.g.* `--agents ssh,gpg`. See [keychain(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/keychain.1).

### x11-ssh-askpass

The [x11-ssh-askpass](https://www.archlinux.org/packages/?name=x11-ssh-askpass) package provides a graphical dialog for entering your passhrase when running an X session. *x11-ssh-askpass* depends only on the [libx11](https://www.archlinux.org/packages/?name=libx11) and [libxt](https://www.archlinux.org/packages/?name=libxt) libraries, and the appearance of *x11-ssh-askpass* is customizable. While it can be invoked by the *ssh-add* program, which will then load your decrypted keys into [ssh-agent](#ssh-agent), the following instructions will, instead, configure *x11-ssh-askpass* to be invoked by the aforementioned [Keychain](#Keychain) script.

Install the [keychain](https://www.archlinux.org/packages/?name=keychain) and [x11-ssh-askpass](https://www.archlinux.org/packages/?name=x11-ssh-askpass) packages.

Edit your `~/.xinitrc` file to include the following lines, replacing the name and location of your private key if necessary. Be sure to place these commands **before** the line which invokes your window manager.

 `~/.xinitrc` 
```
keychain ~/.ssh/id_ecdsa
[ -f ~/.keychain/$HOSTNAME-sh ] && . ~/.keychain/$HOSTNAME-sh 2>/dev/null
[ -f ~/.keychain/$HOSTNAME-sh-gpg ] && . ~/.keychain/$HOSTNAME-sh-gpg 2>/dev/null
...
exec openbox-session
```

In the above example, the first line invokes *keychain* and passes the name and location of your private key. If this is not the first time *keychain* was invoked, the following two lines load the contents of `$HOSTNAME-sh` and `$HOSTNAME-sh-gpg`, if they exist. These files store the environment variables of the previous instance of *keychain*.

#### Calling x11-ssh-askpass with ssh-add

The *ssh-add* manual page specifies that, in addition to needing the `DISPLAY` variable defined, you also need `SSH_ASKPASS` set to the name of your askpass program (in this case *x11-ssh-askpass*). It bears keeping in mind that the default Arch Linux installation places the *x11-ssh-askpass* binary in `/usr/lib/ssh/`, which will not be in most people's `PATH`. This is a little annoying, not only when declaring the `SSH_ASKPASS` variable, but also when theming. You have to specify the full path everywhere. Both inconveniences can be solved simultaneously by symlinking:

```
$ ln -sv /usr/lib/ssh/x11-ssh-askpass ~/bin/ssh-askpass

```

This is assuming that `~/bin` is in your `PATH`. So now in your `.xinitrc`, before calling your window manager, one just needs to export the `SSH_ASKPASS` environment variable:

```
$ export SSH_ASKPASS=ssh-askpass

```

and your [X resources](/index.php/X_resources "X resources") will contain something like:

```
ssh-askpass*background: #000000

```

Doing it this way works well with [the above method on using *ssh-agent* as a wrapper program](#ssh-agent_as_a_wrapper_program). You start X with `ssh-agent startx` and then add *ssh-add* to your window manager's list of start-up programs.

#### Theming

The appearance of the *x11-ssh-askpass* dialog can be customized by setting its associated [X resources](/index.php/X_resources "X resources"). The *x11-ssh-askpass* [home page](http://www.jmknoble.net/software/x11-ssh-askpass/) presents some [example themes](http://www.jmknoble.net/software/x11-ssh-askpass/screenshots.html). See the *x11-ssh-askpass* manual page for full details.

#### Alternative passphrase dialogs

There are other passphrase dialog programs which can be used instead of *x11-ssh-askpass*. The following list provides some alternative solutions.

*   [ksshaskpass](https://www.archlinux.org/packages/?name=ksshaskpass) is dependent on [kdelibs](https://www.archlinux.org/packages/?name=kdelibs) and is suitable for the [KDE](/index.php/KDE "KDE") Desktop Environment.

*   [openssh-askpass](https://www.archlinux.org/packages/?name=openssh-askpass) depends on the [qt4](https://www.archlinux.org/packages/?name=qt4) libraries.

### pam_ssh

The [pam_ssh](http://pam-ssh.sourceforge.net/) project exists to provide a [Pluggable Authentication Module](/index.php/Pluggable_Authentication_Module "Pluggable Authentication Module") (PAM) for SSH private keys. This module can provide single sign-on behavior for your SSH connections. On login, your SSH private key passphrase can be entered in place of, or in addition to, your traditional system password. Once you have been authenticated, the pam_ssh module spawns ssh-agent to store your decrypted private key for the duration of the session.

To enable single sign-on behavior at the tty login prompt, install the unofficial [pam_ssh](https://aur.archlinux.org/packages/pam_ssh/) package.

**Note:** pam_ssh 2.0 now requires that all private keys used in the authentication process be located under `~/.ssh/login-keys.d/`.

Create a symlink to your private key file and place it in `~/.ssh/login-keys.d/`. Replace the `id_rsa` in the example below with the name of your own private key file.

```
$ mkdir ~/.ssh/login-keys.d/
$ cd ~/.ssh/login-keys.d/
$ ln -s ../id_rsa

```

Edit the `/etc/pam.d/login` configuration file to include the text highlighted in bold in the example below. The order in which these lines appear is significiant and can affect login behavior.

**Warning:** Misconfiguring PAM can leave the system in a state where all users become locked out. Before making any changes, you should have an understanding of how PAM configuration works as well as a backup means of accessing the PAM configuration files, such as an Arch Live CD, in case you become locked out and need to revert any changes. An IBM developerWorks [article](http://www.ibm.com/developerworks/linux/library/l-pam/index.html) is available which explains PAM configuration in further detail.
 `/etc/pam.d/login` 
```
#%PAM-1.0

auth       required     pam_securetty.so
auth       requisite    pam_nologin.so
auth       include      system-local-login
**auth       optional     pam_ssh.so        try_first_pass**
account    include      system-local-login
session    include      system-local-login
**session    optional     pam_ssh.so**
```

In the above example, login authentication initially proceeds as it normally would, with the user being prompted to enter his user password. The additional `auth` authentication rule added to the end of the authentication stack then instructs the pam_ssh module to try to decrypt any private keys found in the `~/.ssh/login-keys.d` directory. The `try_first_pass` option is passed to the pam_ssh module, instructing it to first try to decrypt any SSH private keys using the previously entered user password. If the user's private key passphrase and user password are the same, this should succeed and the user will not be prompted to enter the same password twice. In the case where the user's private key passphrase user password differ, the pam_ssh module will prompt the user to enter the SSH passphrase after the user password has been entered. The `optional` control value ensures that users without an SSH private key are still able to log in. In this way, the use of pam_ssh will be transparent to users without an SSH private key.

If you use another means of logging in, such as an X11 display manager like [SLiM](/index.php/SLiM "SLiM") or [XDM](/index.php/XDM "XDM") and you would like it to provide similar functionality, you must edit its associated PAM configuration file in a similar fashion. Packages providing support for PAM typically place a default configuration file in the `/etc/pam.d/` directory.

Further details on how to use pam_ssh and a list of its options can be found in the pam_ssh man page.

#### Using a different password to unlock the SSH key

If you want to unlock the SSH keys or not depending on whether you use your key's passphrase or the (different!) login password, you can modify `/etc/pam.d/system-auth` to

 `/etc/pam.d/system-auth` 
```
#%PAM-1.0

**auth      [success=1 new_authtok_reqd=1 ignore=ignore default=ignore]  pam_unix.so     try_first_pass nullok**
**auth      required  pam_ssh.so      use_first_pass**
auth      optional  pam_permit.so
auth      required  pam_env.so

account   required  pam_unix.so
account   optional  pam_permit.so
account   required  pam_time.so

password  required  pam_unix.so     try_first_pass nullok sha512 shadow
password  optional  pam_permit.so

session   required  pam_limits.so
session   required  pam_unix.so
session   optional  pam_permit.so
**session   optional  pam_ssh.so**
```

For an explanation, see [here](http://unix.stackexchange.com/a/239486/863).

#### Known issues with pam_ssh

Work on the pam_ssh project is infrequent and the documentation provided is sparse. You should be aware of some of its limitations which are not mentioned in the package itself.

*   Versions of pam_ssh prior to version 2.0 do not support SSH keys employing the newer option of ECDSA (elliptic curve) cryptography. If you are using earlier versions of pam_ssh you must use either RSA or DSA keys.

*   The `ssh-agent` process spawned by pam_ssh does not persist between user logins. If you like to keep a [GNU Screen](/index.php/GNU_Screen "GNU Screen") session active between logins you may notice when reattaching to your screen session that it can no longer communicate with ssh-agent. This is because the GNU Screen environment and those of its children will still reference the instance of ssh-agent which existed when GNU Screen was invoked but was subsequently killed in a previous logout. The [Keychain](#Keychain) front-end avoids this problem by keeping the ssh-agent process alive between logins.

### GNOME Keyring

If you use the [GNOME](/index.php/GNOME "GNOME") desktop, the [GNOME Keyring](/index.php/GNOME_Keyring "GNOME Keyring") tool can be used as an SSH agent. See the [GNOME Keyring](/index.php/GNOME_Keyring "GNOME Keyring") article for further details.

### Store SSH keys with Kwallet

For instructions on how to use kwallet to store your SSH keys, see [KDE Wallet#Using the KDE Wallet to store ssh key passhprases](/index.php/KDE_Wallet#Using_the_KDE_Wallet_to_store_ssh_key_passhprases "KDE Wallet").

### KeePass2 with KeeAgent plugin

[KeeAgent](http://lechnology.com/software/keeagent/) is a plugin for [KeePass](/index.php/KeePass "KeePass") that allows SSH keys stored in a KeePass database to be used for SSH authentication by other programs.

*   Supports both PuTTY and OpenSSH private key formats.
*   Works with native SSH agent on Linux/Mac and with PuTTY on Windows.

See [KeePass#Plugin Installation](/index.php/KeePass#Plugin_Installation "KeePass") or [install](/index.php/Install "Install") the [keepass-plugin-keeagent](https://www.archlinux.org/packages/?name=keepass-plugin-keeagent) package. There is also the beta version, where new features appear first, [keepass-plugin-keeagent-beta](https://aur.archlinux.org/packages/keepass-plugin-keeagent-beta/).

This agent can be used directly, by matching KeeAgent socket: `KeePass -> Tools -> Options -> KeeAgent -> Agent mode socket file -> %XDG_RUNTIME_DIR%/keeagent.socket`- and environment variable: `export SSH_AUTH_SOCK="$XDG_RUNTIME_DIR"'/keeagent.socket'`.

### KeePassXC

The KeePassXC fork of KeePass [supports being used as an SSH agent by default](https://keepassxc.org/docs/#faq-ssh-agent-how). It is also compatible with KeeAgent's database format.

## Troubleshooting

### Key ignored by the server

*   If it appears that the SSH server is ignoring your keys, ensure that you have the proper permissions set on all relevant files.

	For the local machine:

```
$ chmod 700 ~/.ssh
$ chmod 600 ~/.ssh/*key*

```

	For the remote machine:

```
$ chmod 700 ~/.ssh
$ chmod 600 ~/.ssh/authorized_keys

```

*   If that does not solve the problem you may try temporarily setting `StrictModes` to `no` in `/etc/ssh/sshd_config`. If authentication with `StrictModes off` is successful, it is likely an issue with file permissions persists.

*   Make sure keys in `~/.ssh/authorized_keys` are entered correctly and only use one single line.

*   Make sure the remote machine supports the type of keys you are using: some servers do not support ECDSA keys, try using RSA or DSA keys instead, see [#Generating an SSH key pair](#Generating_an_SSH_key_pair).

*   You may want to use debug mode and monitor the output while connecting:

```
# /usr/bin/sshd -d

```

## See also

*   [OpenSSH key management, Part 1](https://www.ibm.com/developerworks/linux/library/l-keyc/)
*   [OpenSSH key management, Part 2](https://www.ibm.com/developerworks/linux/library/l-keyc2/)
*   [OpenSSH key management, Part 3](https://www.ibm.com/developerworks/library/l-keyc3/)
*   [Getting started with SSH](https://web.archive.org/web/20170708074341/https://kimmo.suominen.com/docs/ssh/)
*   [OpenSSH 5.7 Release Notes](https://www.openssh.com/txt/release-5.7)
*   [Secure Secure Shell](https://stribika.github.io/2015/01/04/secure-secure-shell.html)