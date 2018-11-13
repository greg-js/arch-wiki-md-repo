**Warning:** 2015年5月发布的对OpenSSL协议使用情况的合作研究显示，SSL连接存在风险([https://weakdh.org/](https://weakdh.org/) Logjam attack)。有关建议的服务器端配置，请参阅：[https://weakdh.org/sysadmin.html](https://weakdh.org/sysadmin.html)

[OpenSSL](http://www.openssl.org)是SSL和TLS协议的开源实现，在OpenSSL（Apache License 1.0）和SSLeay（4-clause BSD）下拥有双重开源许可证。在各种平台上得到支持：BSD,Linux,OpenVMS,Solaris,Windows。 可以免费用于个人和商业用途。基于早期的SSLeay库。OpenSSL 1.0.0版发布于2010年3月29日。

Arch Linux已默认安装[openssl](https://www.archlinux.org/packages/?name=openssl)（作为[coreutils](https://www.archlinux.org/packages/?name=coreutils)的依赖）。

## Contents

*   [1 SSL介绍](#SSL介绍)
*   [2 配置](#配置)
    *   [2.1 req部分](#req部分)
        *   [2.1.1 终端用户req设置](#终端用户req设置)
    *   [2.2 GOST引擎的支持](#GOST引擎的支持)
*   [3 生成私钥](#生成私钥)
*   [4 证书](#证书)
    *   [4.1 创建证书签名请求](#创建证书签名请求)
    *   [4.2 自签名证书](#自签名证书)
    *   [4.3 证书颁发机构(CA)](#证书颁发机构(CA))
        *   [4.3.1 Makefile文件](#Makefile文件)
*   [5 故障排除](#故障排除)
    *   [5.1 解密时”解密不好”("bad decrypt"）](#解密时”解密不好”("bad_decrypt"）)
*   [6 另请参阅](#另请参阅)

## SSL介绍

本文主要介绍设置SSL/TLS解决方案，而不解释有关该主题基本知识。本文中解释SSL概念的方法基本上是“面向文件”的。

有关更多信息，请参阅[Wikipedia:Certificate authority](https://en.wikipedia.org/wiki/Certificate_authority "wikipedia:Certificate authority")和[Wikipedia:Public key infrastructure](https://en.wikipedia.org/wiki/Public_key_infrastructure "wikipedia:Public key infrastructure")。

	证书颁发机构(CA)

	根据用户请求，返回证书的机构。返回的最终用户证书(end-user certificate)使用CA的私钥和CA的证书签名，CA证书又包含CA公钥。CA还分发证书吊销列表(CRL),通知用户哪些证书不再有效和下一个CRL何时到期。

	CA private key

	CA私钥非常重要。公开CA私钥和指定权威机构验证和撤销权限的做法背道而驰，并且CA私钥是CA证书中CA公钥的用于签名的对应部分。由于CA私钥签名包含在CA证书本身当中，因此暴露的CA私钥给攻击者复制CA证书提供可乘之机。原文：

The CA private key is the crucial part of the trifecta. Exposing it would defeat the purpose of designating a central authority that validates and revokes permissions, and at the same time, it is the signed counter part to the CA public key used to certify against the CA certificate. An exposed CA private key could allow an attacker to replicate the CA certificate since the CA private key signature is embedded in the CA certificate itself.

	CA证书和公钥

	这些以单个文件的形式分发给所有最终用户，来证明其他声称是由相同CA签名的最终用户证书，例如网站，邮件服务器。原文：

These are distributed in a single file to all end-users. They are used to certify other end-user certificates that claimed to be signed by the matching CA, such as mail servers or websites.

	终端用户

	终端用户向CA提交包含独一无二名称DN(distinguished name)的证书请求。通常，CA不允许在撤消前一个证书前，签发具有相同DN的多个有效证书。如果最终用户证书在证书到期时未续期或者因为其他原因，证书会被撤销。

	终端用户生成的密钥

	最终用户生成密钥以便签署提交给CA的证书请求。 与CA私钥一样，暴露用户密钥，会导致别人假冒你的身份，攻击者可以使用相同的用户名提交请求，从而导致CA撤销前一个合法的用户证书。

	证书申请

	这些包含用户的DN和公钥。顾名思义，这是从CA获得认证过程的最开始的部分。

	最终用户证书

最终用户证书与CA证书之间的主要区别在于最终用户证书本身无法签署证书; 它们只是在信息交换中提供识别手段。

	证书撤销清单CRL(Certificate revocation list)

	CRL也使用CA密钥签名，但它们仅表示有关最终用户证书的信息。通常，CRL提交的时间间隔为30天。

## 配置

OpenSSL配置文件通常在`/etc/ssl/openssl.cnf`,并且显得很复杂。 Remember that variables may be expanded in assignments, much like how shell scripts work. For a thorough explanation of the configuration file format, see [config(5ssl)](https://jlk.fjfi.cvut.cz/arch/manpages/man/config.5ssl). In some operating systems, this [man page](/index.php/Man_page "Man page") is named config(5) or openssl-config(5). Sometimes, it may not even be available through the man hierarchy at all, for example, it may be placed in the following location `/usr/share/openssl`.

### req部分

Settings related to generating keys, requests and self-signed certificates.

The req section is responsible for the DN prompts. A general misconception is the *Common Name* (CN) prompt, which suggests that it should have the user's proper name as a value. End-user certificates need to have the **machine hostname** as CN, whereas CA should *not* have a valid TLD, so that there is no chance that, between the possible combinations of certified end-users' CN and the CA certificate's, there is a match that could be misinterpreted by some software as meaning that the end-user certificate is self-signed. Some CA certificates do not even have a CN, such as [Equifax](http://www.equifax.com):

 `$ openssl x509 -subject -noout < /etc/ssl/certs/Equifax_Secure_CA.pem`  `subject= /C=US/O=Equifax/OU=Equifax Secure Certificate Authority` 

Even though splitting the files is not strictly necessary to normal functioning, it is very confusing to handle request generation and CA administration from the same configuration file, so it is advised to follow the convention of clearly separating the settings into two `cnf` files and into two containing directories.

Here are the settings that are common to both tasks:

```
[ req ]
# Default bit encryption and out file for generated keys.
default_bits=	2048
default_keyfile=private/cakey.pem

string_mask=	utf8only	# Only allow utf8 strings in request/ca fields.
prompt=		no		# Do not prompt for field value confirmation.
```

#### 终端用户req设置

Makes a v3 request suitable for most circumstances:

```
distinguished_name=ca_dn	# Distinguished name contents.
req_extensions=req_v3		# For generating ca certificates.

[ ca_dn ]
C=	US
ST=	New Jersey
O=	localdomain
CN=	localhost

[ req_v3 ]
basicConstraints=	CA:FALSE
keyUsage=		nonRepudiation, digitalSignature, keyEncipherment
```

### GOST引擎的支持

First, be sure that libgost.so exist on your system

```
$ pacman -Ql openssl | grep libgost

```

In case everything is fine, add the following lines to the config:

```
openssl_conf = openssl_def # this must be a top-level declaration

```

Put the following lines in the end of the document:

```
[ openssl_def ]
engines = engine_section

[ engine_section ]
gost = gost_section

[ gost_section ]
engine_id = gost
soft_load = 1
dynamic_path = /usr/lib/engines/libgost.so
default_algorithms = ALL
CRYPT_PARAMS = id-Gost28147-89-CryptoPro-A-ParamSet

```

The official [README.gost](http://ftp.netbsd.org/pub/NetBSD/NetBSD-current/src/crypto/external/bsd/openssl/dist/engines/ccgost/README.gost) should contain more examples on this.

## 生成私钥

**Warning:** The [openssl](https://www.archlinux.org/packages/?name=openssl) package doesn't properly safeguard the `/etc/ssl/private/` directory like most other distributions do, see [FS#43059](https://bugs.archlinux.org/task/43059).

Before generating the key, make a secure directory to host it:

```
$ mkdir -m0700 private

```

Followed by preemptively assigning secure permissions for the key itself:

```
$ touch private/key.pem
$ chmod 0600 private/key.pem

```

Alternatively set [umask](/index.php/Umask "Umask") to restrict permissions of newly created files and directories:

```
$ umask 077

```

An example `genpkey` key generation:

```
$ openssl genpkey -algorithm RSA -out private/key.pem -pkeyopt rsa_keygen_bits:4096

```

If an encrypted key is desired, use the following command. Password will be prompted for:

```
$ openssl genpkey -aes-256-cbc -algorithm RSA -out private/key.pem -pkeyopt rsa_keygen_bits:4096

```

## 证书

If you want to communicate securely with a server for the first time, you need to trust an unknown public key. [TLS](https://en.wikipedia.org/wiki/TLS "wikipedia:TLS") solves this using the [Public Key Infrastructrue](https://en.wikipedia.org/wiki/Public_Key_Infrastructrue "wikipedia:Public Key Infrastructrue"). Basically clients trust a set of [certificate authorities](https://en.wikipedia.org/wiki/Certificate_authority "wikipedia:Certificate authority") (CAs) (on Arch Linux the [ca-certificates packages](https://www.archlinux.org/packages/?q=ca-certificates)). When a certificate is received from a server, your client (mostly [gnutls](https://www.archlinux.org/packages/?name=gnutls)) verifies that it is signed by a certificate authority you trust.

### 创建证书签名请求

To obtain a certificate from a certificate authority, you need to create a [Certificate Signing Request](https://en.wikipedia.org/wiki/Certificate_signing_request "wikipedia:Certificate signing request") (CSR) and sign it with a previously [generated private key](#Generating_private_keys):

```
$ openssl req -new -sha256 -key private/key.pem -out req.csr

```

**Tip:** You can get free certificates from the [Let's Encrypt](https://letsencrypt.org/) certificate authority using an [ACME](/index.php/ACME "ACME") client.

### 自签名证书

Clients reject [self-signed certificates](https://en.wikipedia.org/wiki/Self-signed_certificate "wikipedia:Self-signed certificate") by default, requiring you to manually configure every client to trust your self-signed certificate. Maintaining more than one self-signed certificate is more trouble than investing the initial effort in setting up a [certificate authority](#Certificate_authority).

To create a self-signed certificate with a previously [generated private key](#Generating_private_keys):

```
$ openssl req -key private/key.pem -x509 -new -days 3650 -out selfcert.pem

```

### 证书颁发机构(CA)

[OpenSSL Certificate Authority](https://jamielinux.com/docs/openssl-certificate-authority/) is a detailed guide on using OpenSSL to act as a CA.

The method shown in this section is mostly meant to show how signing works; it is not suited for large deployments that need to automate signing a large number of certificates. Consider installing an SSL server for that purpose.

Before using the Makefile, make a configuration file according to [#Configuration](#Configuration). Be sure to follow instructions relevant to CA administration; not request generation.

#### Makefile文件

Saving the file as `Makefile` and issuing `make` in the containing directory will generate the initial CRL along with its prerequisites:

```
OPENSSL=	openssl
CNF=		openssl.cnf
CA=		${OPENSSL} ca -config ${CNF}
REQ=		${OPENSSL} req -config ${CNF}

KEY=		private/cakey.pem
KEYMODE=	RSA

CACERT=		cacert.pem
CADAYS=		3650

CRL=		crl.pem
INDEX=		index.txt
SERIAL=		serial

CADEPS=		${CNF} ${KEY} ${CACERT}

all:	${CRL}

${CRL}:	${CADEPS}
	${CA} -gencrl -out ${CRL}

${CACERT}: ${CNF} ${KEY}
	${REQ} -key ${KEY} -x509 -new -days ${CADAYS} -out ${CACERT}
	rm -f ${INDEX}
	touch ${INDEX}
	echo 100001 > ${SERIAL}

${KEY}: ${CNF}
	mkdir -m0700 -p $(dir ${KEY})
	touch ${KEY}
	chmod 0600 ${KEY}
	${OPENSSL} genpkey -algorithm ${KEYMODE} -out ${KEY}

revoke:	${CADEPS} ${item}
	@test -n $${item:?'usage: ${MAKE} revoke item=cert.pem'}
	${CA} -revoke ${item}
	${MAKE} ${CRL}

sign:	${CADEPS} ${item}
	@test -n $${item:?'usage: ${MAKE} sign item=request.csr'}
	mkdir -p newcerts
	${CA} -in ${item} -out ${item:.csr=.crt}
```

To sign certificates:

```
$ make sign item=**req.csr**

```

To revoke certificates:

```
$ make revoke item=**cert.pem**

```

## 故障排除

### 解密时”解密不好”("bad decrypt"）

OpenSSL 1.1.0 changed the default digest algorithm for the dgst and enc commands from MD5 to SHA256\. [[1]](https://www.openssl.org/news/changelog.html#x6)

Therefore if a file has been encrypted using OpenSSL 1.0.2 or older, trying to decrypt it with an up to date version may result in an error like:

```
error:06065064:digital envelope routines:EVP_DecryptFinal_ex:bad decrypt:crypto/evp/evp_enc.c:540

```

Supplying the `-md md5` option should solve the issue:

```
$ openssl enc -d -md md5 -in encrypted -out decrypted

```

## 另请参阅

*   [Wikipedia page](https://en.wikipedia.org/wiki/OpenSSL "wikipedia:OpenSSL") on OpenSSL, with background information.
*   [OpenSSL](http://www.openssl.org) project page.
*   [FreeBSD Handbook](http://www.freebsd.org/doc/en/books/handbook/openssl.html)
*   [Step-by-step guide to create a signed SSL certificate](http://www.akadia.com/services/ssh_test_certificate.html)
*   [OpenSSL Certificate Authority](https://jamielinux.com/docs/openssl-certificate-authority/)
*   [Bulletproof SSL and TLS](https://www.feistyduck.com/books/bulletproof-ssl-and-tls/bulletproof-ssl-and-tls-introduction.pdf) by Ivan Ristić, a more formal introduction to SSL/TLS