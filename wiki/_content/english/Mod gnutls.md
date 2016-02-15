From [mod_gnutls wiki](https://mod.gnutls.org/wiki):

	mod_gnutls is an extension for ​Apache's httpd uses the ​GnuTLS library to provide HTTPS.

	It is similar to ​mod_ssl in purpose, but it supports some features and protocols that mod_ssl does not, and it does not use ​OpenSSL.

## Installation

Install [mod_gnutls](https://aur.archlinux.org/packages/mod_gnutls/), available in the [Arch User Repository](/index.php/Arch_User_Repository "Arch User Repository").

### Configure Apache

Add these lines to `/etc/httpd/conf/httpd.conf`:

```
LoadModule gnutls_module modules/mod_gnutls.so
Include conf/extra/httpd-gnutls.conf
```

Make sure that the following line is commented in `/etc/httpd/conf/httpd.conf`:

 `Include conf/extra/httpd-ssl.conf` 

Make sure no vhost definitions include mod_ssl.

Create the file `/etc/httpd/conf/extra/httpd-gnutls.conf` with the following content:

 `/etc/httpd/conf/extra/httpd-gnutls.conf` 

```
Listen 443

AddType application/x-x509-ca-cert .crt
AddType application/x-pkcs7-crl    .crl

GnuTLSCache dbm "/var/run/httpd/gnutls_scache"
GnuTLSCacheTimeout 600

<VirtualHost _default_:443>

DocumentRoot "/srv/http"
ServerName www.example.org
ServerAdmin youremail@example.org
ErrorLog "/var/log/httpd/error_log"
TransferLog "/var/log/httpd/access_log"

GnuTLSEnable on
GnuTLSPriorities NORMAL

GNUTLSExportCertificates on

GnuTLSCertificateFile /path/to/certificate/domain.tld.crt
GnuTLSKeyFile /path/to/certificate/domain.tld.key

</VirtualHost>
```

[Restart](/index.php/Restart "Restart") `httpd.service`.

Check that Apache loaded correctly and answers on port 443.

Additional documentation of configuration directives is on the [outoforder.cc mod_gnutls](http://www.outoforder.cc/projects/apache/mod_gnutls/docs/) documentation page.

## Testing

You can test or verify your https configuration via [SSL Labs analyze tool](https://www.ssllabs.com/ssltest/analyze.html).