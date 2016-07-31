The first step when setting up [OpenVPN](/index.php/OpenVPN "OpenVPN") is to create a [Public Key Infrastructure (PKI)](https://en.wikipedia.org/wiki/Public_key_infrastructure "wikipedia:Public key infrastructure"). The PKI consists of:

*   A public master [Certificate Authority (CA)](https://en.wikipedia.org/wiki/Certificate_Authority "wikipedia:Certificate Authority") certificate and a private key.
*   A separate public certificate and private key pair for each server and each client.

To facilitate the certificate creation process, [easy-rsa](https://www.archlinux.org/packages/?name=easy-rsa) provides a [RSA](https://en.wikipedia.org/wiki/RSA_(algorithm) key management script.

**Note:** The certificates can be created on any machine. For the highest security, generate the certificates on a physically secure machine disconnected from any network, and make sure that the generated ca.key private key is backed up kept secret from users.

## Contents

*   [1 OpenVPN Server and Client Configuration](#OpenVPN_Server_and_Client_Configuration)
    *   [1.1 Create the CA](#Create_the_CA)
    *   [1.2 Create and and sign an entity keypair](#Create_and_and_sign_an_entity_keypair)
    *   [1.3 Generate a secret Hash-based Message Authentication Code (HMAC) key](#Generate_a_secret_Hash-based_Message_Authentication_Code_.28HMAC.29_key)
*   [2 See also](#See_also)

## OpenVPN Server and Client Configuration

**Note:** All commands below are expected to be run as the root user. To make them more copy/paste friendly for readers, they are not prefixed.

### Create the CA

After installing [easy-rsa](https://www.archlinux.org/packages/?name=easy-rsa), initialize a new PKI and generate a CA:

```
cd /etc/easy-rsa
easyrsa init-pki
easyrsa build-ca

```

### Create and and sign an entity keypair

The term entity generally means either a server or client. For ease, substitute the word "entity" below with "server" or "client" as an example.

Generate and sign a key pair:

```
cd /etc/easy-rsa
easyrsa gen-req entity

```

Sign the server cert and key with the CA.

**Note:** Servers need to be signed with "server" type whereas clients need to be signed with the "client" type. Make the appropriate substitution for the word "type" in the following command.

```
cd /etc/easy-rsa
easyrsa sign-req type entity

```

A blank password is expected if using the openvpn systemd service. This can be accomplished via the following command:

```
cd /etc/easy-rsa
easyrsa set-rsa-pass server nopass

```

### Generate a secret Hash-based Message Authentication Code (HMAC) key

```
openvpn --genkey --secret /root/easy-rsa/keys/ta.key

```

This will be used to add an additional HMAC signature to all SSL/TLS handshake packets. In addition any UDP packet not having the correct HMAC signature will be immediately dropped, protecting against:

*   Portscanning.
*   DOS attacks on the OpenVPN UDP port.
*   SSL/TLS handshake initiations from unauthorized machines.
*   Any eventual buffer overflow vulnerabilities in the SSL/TLS implementation.

## See also

*   [Official EasyRSA instructions](https://openvpn.net/index.php/open-source/documentation/miscellaneous/rsa-key-management.html)