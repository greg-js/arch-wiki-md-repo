The first step when setting up [OpenVPN](/index.php/OpenVPN "OpenVPN") is to create a [Public Key Infrastructure (PKI)](https://en.wikipedia.org/wiki/Public_key_infrastructure "wikipedia:Public key infrastructure"). The PKI consists of:

*   A public master [Certificate Authority (CA)](https://en.wikipedia.org/wiki/Certificate_Authority "wikipedia:Certificate Authority") certificate and a private key.
*   A separate public certificate and private key pair (hereafter referred to as a certificate) for each server and each client.

To facilitate the certificate creation process, OpenVPN comes with a collection of [RSA](https://en.wikipedia.org/wiki/RSA_(algorithm) key manangement scripts (based on the openssl command line tool) known as easy-rsa.

**Note:** Only .key files need to be kept secret, .crt and .csr files can be sent over insecure channels such as plaintext email.

In this article the needed certificates are created by root in root's home directory. This ensures that the generated files have the right ownership and permissions, and are safe from other users.

**Note:** The certificates can be created on any machine. For the highest security, generate the certificates on a physically secure machine disconnected from any network, and make sure that the generated ca.key private key is backed up and never accessible to anyone.

**Warning:** Make sure that the generated files are backed up, especially the ca.key and ca.crt files, since if lost you will not be able to create any new, nor revoke any compromised certificates, thus requiring the generation of a new [Certificate Authority (CA)](https://en.wikipedia.org/wiki/Certificate_Authority "wikipedia:Certificate Authority") certificate, invalidating the entire PKI infrastructure.

## Contents

*   [1 Installing the easy-rsa scripts](#Installing_the_easy-rsa_scripts)
*   [2 Creating certificates on the server](#Creating_certificates_on_the_server)
*   [3 Creating certificates on the client](#Creating_certificates_on_the_client)
    *   [3.1 Creating a certificate signing request](#Creating_a_certificate_signing_request)
    *   [3.2 Signing a certificate signing request](#Signing_a_certificate_signing_request)
*   [4 Converting certificates to encrypted .p12 format](#Converting_certificates_to_encrypted_.p12_format)
*   [5 See also](#See_also)

### Installing the easy-rsa scripts

First, install [easy-rsa](https://www.archlinux.org/packages/?name=easy-rsa) package and copy files as shown:

 `# cp -r /usr/share/easy-rsa /root` 

### Creating certificates on the server

Change to the directory where you installed the scripts.

 `# cd /root/easy-rsa` 

To ensure the consistent use of values when generating the PKI, set default values to be used by the PKI generating scripts. Edit /root/easy-rsa/vars and at a minimum set the KEY_COUNTRY, KEY_PROVINCE, KEY_CITY, KEY_ORG, and KEY_EMAIL parameters (do not leave any of these parameters blank). Change the KEY_SIZE parameter to 2048 for the SSL/TLS to use 2048bit RSA keys for authentication.

Delete any previously created certificates.

 `# ./clean-all` 
**Note:** Entering a . (dot) when prompted for a value, blanks out the parameter.

The build-ca script generates the [Certificate Authority (CA)](https://en.wikipedia.org/wiki/Certificate_Authority "wikipedia:Certificate Authority") certificate.

 `# ./build-ca` 
```
Generating a 2048 bit RSA private key
..............++++++
...++++++
writing new private key to 'ca.key'
-----
You are about to be asked to enter information that will be incorporated
into your certificate request.
What you are about to enter is what is called a Distinguished Name or a DN.
There are quite a few fields but you can leave some blank
For some fields there will be a default value,
If you enter '.', the field will be left blank.
-----
Country Name (2 letter code) [US]:
State or Province Name (full name) [CA]:
Locality Name (eg, city) [Acme Acres]:
Organization Name (eg, company) [Acme]:
Organizational Unit Name (eg, section) []:
Common Name (eg, your name or your server's hostname) [Acme-CA]:
Name [Acme-CA]:
Email Address [roadrunner@acmecorp.org]:

```

The build-key-server script `# ./build-key-server <server name>` generates a server certificate. Make sure that the server name (Common Name when running the script) is unique.

**Note:** Do not enter a challenge password or company name when the script prompts you for one.
 `# ./build-key-server elmer` 
```
Generating a 2048 bit RSA private key
.....................++++++
.......................................................++++++
writing new private key to 'elmer.key'
-----
You are about to be asked to enter information that will be incorporated
into your certificate request.
What you are about to enter is what is called a Distinguished Name or a DN.
There are quite a few fields but you can leave some blank
For some fields there will be a default value,
If you enter '.', the field will be left blank.
-----
Country Name (2 letter code) [US]:
State or Province Name (full name) [CA]:
Locality Name (eg, city) [Acme Acres]:
Organization Name (eg, company) [Acme]:
Organizational Unit Name (eg, section) []:
Common Name (eg, your name or your server's hostname) [elmer]:
Name [Acme-CA]:
Email Address [roadrunner@acmecorp.org]:

Please enter the following 'extra' attributes
to be sent with your certificate request
A challenge password []:
An optional company name []:
Using configuration from /root/easy-rsa/openssl-1.0.0.cnf
Check that the request matches the signature
Signature ok
The Subject's Distinguished Name is as follows
countryName           :PRINTABLE:'US'
stateOrProvinceName   :PRINTABLE:'CA'
localityName          :PRINTABLE:'Acme Acres'
organizationName      :PRINTABLE:'Acme'
commonName            :PRINTABLE:'elmer'
name                  :PRINTABLE:'Acme-CA'
emailAddress          :IA5STRING:'roadrunner@acmecorp.org'
Certificate is to be certified until Dec 27 19:11:59 2021 GMT (3650 days)
Sign the certificate? [y/n]:y

1 out of 1 certificate requests certified, commit? [y/n]y
Write out database with 1 new entries
Data Base Updated

```

The build-dh script generates the [Diffie-Hellman parameters](https://web.archive.org/web/20130701090246/https://www.rsa.com/rsalabs/node.asp?id=2248) .pem file needed by the server. This command will take some time, possibly around from 1 to 5 minutes.

**Note:** It would be better to generate a new one for each server, but you can use the same one if you want to.
 `# ./build-dh` 
```
Generating DH parameters, 2048 bit long safe prime, generator 2
This is going to take a long time
..+.............................................................................
.
.
.
............+...............+...................................................
..................................................................++*++*
```

To generate the client(s) key(s), one can either do so on the server side directly using the `./build-key` script, or generate the key entirely on the client side and then ask the CA authority to sign it. The first method is simpler and quicker, but the second method doesn't require the client private key to leave its machine and is therefore slightly more secure. (see [#Creating certificates on the client](#Creating_certificates_on_the_client) for an outline of the second method)

The build-key script `# ./build-key <client name>` generates a client certificate. Make sure that the client name (Common Name when running the script) is unique.

**Note:** Do not enter a challenge password or company name when the script prompts you for one.
 `# ./build-key bugs` 
```
Generating a 2048 bit RSA private key
....++++++
.............................................................++++++
writing new private key to 'bugs.key'
-----
You are about to be asked to enter information that will be incorporated
into your certificate request.
What you are about to enter is what is called a Distinguished Name or a DN.
There are quite a few fields but you can leave some blank
For some fields there will be a default value,
If you enter '.', the field will be left blank.
-----
Country Name (2 letter code) [US]:
State or Province Name (full name) [CA]:
Locality Name (eg, city) [Acme Acres]:
Organization Name (eg, company) [Acme]:
Organizational Unit Name (eg, section) []:
Common Name (eg, your name or your server's hostname) [bugs]:
Name [Acme-CA]:
Email Address [roadrunner@acmecorp.org]:

Please enter the following 'extra' attributes
to be sent with your certificate request
A challenge password []:
An optional company name []:
Using configuration from /root/easy-rsa/openssl-1.0.0.cnf
Check that the request matches the signature
Signature ok
The Subject's Distinguished Name is as follows
countryName           :PRINTABLE:'US'
stateOrProvinceName   :PRINTABLE:'CA'
localityName          :PRINTABLE:'Acme Acres'
organizationName      :PRINTABLE:'Acme'
commonName            :PRINTABLE:'bugs'
name                  :PRINTABLE:'Acme-CA'
emailAddress          :IA5STRING:'roadrunner@acmecorp.org'
Certificate is to be certified until Dec 27 19:18:27 2021 GMT (3650 days)
Sign the certificate? [y/n]:y

1 out of 1 certificate requests certified, commit? [y/n]y
Write out database with 1 new entries
Data Base Updated

```

This generates a client certificate (`bugs.crt`) and a client private key (`bugs.key`) which need to be transferred to the client through a secure channel.

Generate a secret [Hash-based Message Authentication Code (HMAC)](https://en.wikipedia.org/wiki/HMAC "wikipedia:HMAC") file by running:

```
# openvpn --genkey --secret /root/easy-rsa/keys/ta.key

```

This will be used to add an additional HMAC signature to all SSL/TLS handshake packets. In addition any UDP packet not having the correct HMAC signature will be immediately dropped, protecting against:

*   Portscanning.
*   DOS attacks on the OpenVPN UDP port.
*   SSL/TLS handshake initiations from unauthorized machines.
*   Any eventual buffer overflow vulnerabilities in the SSL/TLS implementation.

All the created keys and certificates have been stored in /root/easy-rsa/keys. If you make a mistake, you can start over by running the clean-all script again.

**Warning:** This will delete any previously generated certificates stored in /root/easy-rsa/keys, including the [Certificate Authority (CA)](https://en.wikipedia.org/wiki/Certificate_Authority "wikipedia:Certificate Authority") certificate.

### Creating certificates on the client

It might be desirable for the clients to generate their private keys on their own machine, removing the need to trust that the CA operator not keep the client's private key stored remotely (or other nefarious intentions). To do so, the client needs to create the private key locally, and create a [certificate signing request](https://en.wikipedia.org/wiki/Certificate_signing_request "wikipedia:Certificate signing request") (which is a `.csr` file) to the key-signing machine, run by the CA. The operator will then sign the request and return a signed certificate (a `.crt` file) which is then transferred back to the client.

#### Creating a certificate signing request

An outline of the required steps follows, assuming "bugs" is the client name:

1.  Transfer the `ca.crt` file from the CA to the client. The `ca.crt` file is public information, and thus this transfer can be done over an insecure channel. The file should be stored in `/root/easy-rsa/keys/ca.crt`
2.  Check that the `ca.crt` file has not been tampered with by either:
    1.  Having the file be signed by the CA and verified by the client using the CA's public key. Note that this is referring to standard [GnuPG](/index.php/GnuPG#Signatures "GnuPG")-style signature verification: `gpg --verify doc.sig`
    2.  Checking the hash of the file (e.g. using `sha1sum ca.crt`) and verifying that it matches the expected hash, provided you trust the "expected hash".
    3.  Simply transferring ca.crt over a trusted channel.
    4.  Some other mechanism that the reader sees fit.
3.  Run `./build-req bugs` which is analogous to running `./build-key bugs` in the server section above. The same warning, that the Common Name should be unique, still stands.
4.  Leave all password field blank. If you'd like to protect your private key with a password, use `./build-req-pass` instead. Note that this will require you to input the password whenever the key needs to be unlocked.
5.  You now have the `bugs.csr` and `bugs.key` files. Send your certificate signing request to the CA, e.g. by emailing your `bugs.csr` file. Keep your `bugs.key` file secret, this is your private key.
6.  Wait until you receive your signed certificate from the CA, which will be a file named `bugs.crt`.

#### Signing a certificate signing request

To sign a certificate signing request, the CA simply needs to run `./sign-req bugs` after placing `bugs.csr` into `/root/easy-rsa/keys/bugs.csr`. The CA can then transfer the resulting `bugs.crt` file back the client using an insecure channel (e.g. via email)

**Note:** When running the command, the error `chmod: cannot access `bugs.key': No such file or directory` will show up. This is expected, and is safe to ignore [[1]](https://forums.openvpn.net/topic13418.html)

### Converting certificates to encrypted .p12 format

Some software (such as Android) will only read VPN certificates that are stored in a password-encrypted .p12 file. These can be generated with the following command:

 `# openssl pkcs12 -export -inkey keys/bugs.key -in keys/bugs.crt -certfile keys/ca.crt -out keys/bugs.p12` 

## See also

*   [Official EasyRSA instructions](https://openvpn.net/index.php/open-source/documentation/miscellaneous/rsa-key-management.html)