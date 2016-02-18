FreeIPA is an open-source Identity, Policy and Audit (IPA) suite, sponsored by RedHat, which provides services similar to Microsoft's Active Directory

## Configure as IPA client

Make sure your clocks are synchronized. Kerberos will not work otherwise. [NTP](/index.php/Network_Time_Protocol_daemon "Network Time Protocol daemon") is reccomended.

Follow the LDAP auth instructions to [setup SSSD](/index.php/LDAP_authentication#Online_and_Offline_Authentication_with_SSSD "LDAP authentication"). Use a SSSD configuration similar to the following, substituting the requisite fields:

 `/etc/sssd/sssd.conf` 
```
[sssd]
config_file_version = 2
services = nss, pam, sudo
domains = DOMAIN
debug_level = 9

[domain/DOMAIN]
debug_level = 9
cache_credentials = true
krb5_store_password_if_offline = true
id_provider = ipa
auth_provider = ipa
ipa_domain=ipa.domain.com
ipa_server=controller.domain.com
ipa_hostname=fqdn.for.machine
```

Configure pam in similar way to [LDAP](/index.php/LDAP_authentication#PAM_Configuration "LDAP authentication"), replacing `pam_ldap.so` with `pam_sss.so`.

Create an `/etc/krb5.conf` file for your domain:

 `/etc/krb5.conf` 
```
[libdefaults]
        default_realm = DOMAIN.COM
        dns_lookup_realm = false
        dns_lookup_kdc = false
        rdns = false
        ticket_lifetime = 24h
        fowardable = yes
        allow_weak_crypto = yes

[realms]
        DOMAIN.COM = {
                admin_server = controller.domain.com
                kdc = controller.domain.com:749
                default_admin = domain.com
        }

[domain_realm]
        domain.com = DOMAIN.COM
        .domain.com = DOMAIN.COM

[logging]
        default = FILE:/var/log/krb5libs.log
        kdc = FILE:/var/log/krb5kdc.log
        admin_server = FILE:/var/log/kadmin.log
```

Add the client to the IPA server ([From Fedora documentation](https://docs.fedoraproject.org/en-US/Fedora/15/html/FreeIPA_Guide/linux-manual.html)):

1.  Login and request and admin session `kinit admin`
2.  Create a host entry `ipa host-add --force --ip-address=192.168.166.31 client1.domain.com`
3.  Set the client to be managed by IPA `ipa host-add-managedby --hosts=controller.domain.com client1.domain.com`
4.  Generate keytab for the client `ipa-getkeytab -s controller.domain.com -p host/client1.domain.com -k /tmp/client1.keytab`

Install the keytab on the client:

```
$ scp user@controller.domain.com:/tmp/client1.keytab krb5.keytab
# mv krb5.ketab /etc/krb5.keytab

```