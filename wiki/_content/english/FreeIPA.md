FreeIPA is an open-source Identity, Policy and Audit (IPA) suite, sponsored by RedHat, which provides services similar to Microsoft's Active Directory

## Contents

*   [1 Configure as IPA client](#Configure_as_IPA_client)
    *   [1.1 SSH integration](#SSH_integration)
        *   [1.1.1 authorized_keys](#authorized_keys)
        *   [1.1.2 known_hosts](#known_hosts)
    *   [1.2 See Also](#See_Also)

## Configure as IPA client

Make sure your clocks are synchronized. Kerberos will not work otherwise. [NTP](/index.php/Network_Time_Protocol_daemon "Network Time Protocol daemon") is recommended.

Follow the LDAP auth instructions to [setup SSSD](/index.php/LDAP_authentication#Online_and_Offline_Authentication_with_SSSD "LDAP authentication"). Use a SSSD configuration similar to the following, substituting the requisite fields:

 `/etc/sssd/sssd.conf` 
```
[sssd]
config_file_version = 2
services = nss, pam, sudo, ssh
domains = EXAMPLE.COM
#debug_level = 9

[domain/EXAMPLE.COM]
#debug_level = 9
cache_credentials = true
krb5_store_password_if_offline = true
id_provider = ipa
auth_provider = ipa
access_provider = ipa
chpass_provider = ipa
#ipa_domain=ipa.example.com  # Optional if you set SRV records in DNS
#ipa_server=controller.example.com  # Optional if you set SRV records in DNS
ipa_hostname=fqdn.for.machine
```

Configure pam in similar way to [LDAP](/index.php/LDAP_authentication#PAM_Configuration "LDAP authentication"), replacing `pam_ldap.so` with `pam_sss.so`.

Create an `/etc/krb5.conf` file for your domain:

 `/etc/krb5.conf` 
```
[libdefaults]
        default_realm = EXAMPLE.COM
        dns_lookup_realm = false
        dns_lookup_kdc = false
        rdns = false
        ticket_lifetime = 24h
        fowardable = yes
        #allow_weak_crypto = yes  # Only if absolutely necessary. Currently FreeIPA supports strong crypto.

[realms]
        EXAMPLE.COM = {
                admin_server = controller.example.com
                kdc = controller.example.com:749
                default_admin = example.com
        }

[domain_realm]
        example.com = EXAMPLE.COM
        .example.com = EXAMPLE.COM

[logging]
        default = FILE:/var/log/krb5libs.log
        kdc = FILE:/var/log/krb5kdc.log
        admin_server = FILE:/var/log/kadmin.log
```

Add the client to the IPA server ([From Fedora documentation](https://docs.fedoraproject.org/en-US/Fedora/15/html/FreeIPA_Guide/linux-manual.html)):

1.  Login and request and admin session `kinit admin`
2.  Create a host entry `ipa host-add --force --ip-address=192.168.166.31 client1.example.com`
    (if the host does not have a static IP, use `ipa host-add client1.example.com`)
3.  Set the client to be managed by IPA `ipa host-add-managedby --hosts=controller.example.com client1.example.com`
4.  Generate keytab for the client `ipa-getkeytab -s controller.example.com -p host/client1.example.com -k /tmp/client1.keytab`

Install the keytab on the client:

```
$ scp user@controller.example.com:/tmp/client1.keytab krb5.keytab
# mv krb5.ketab /etc/krb5.keytab

```

### SSH integration

#### authorized_keys

You can configure SSHD to fetch users SSH public key from the LDAP directory by uncommenting those lines in `/etc/ssh/sshd_config`:

```
 AuthorizedKeysCommand /usr/bin/sss_ssh_authorizedkeys
 AuthorizedKeysCommandUser nobody

```

Then restart sshd.

You can add your ssh key to your FreeIPA user account through the web interface or use the `-sshpubkey='ssh-rsa AAAA...'` argument to the `ipa user-mod` or `ipa user-create` commands.

Test it:

```
 sudo -u nobody sss_ssh_authorizedkeys <username>

```

You should see your ssh public key on standard output and no error message on standard error.

#### known_hosts

You can configure SSH to fetch hosts public key information from their directory entries in FreeIPA by adding those lines in `/etc/ssh/ssh_config`:

```
 GlobalKnownHostsFile /var/lib/sss/pubconf/known_hosts
 ProxyCommand /usr/bin/sss_ssh_knownhostsproxy -p %p %h

```

### See Also

*   [Manually Configuring a Linux Client](https://docs.fedoraproject.org/en-US/Fedora/15/html/FreeIPA_Guide/linux-manual.html) from the FreeIPA user guide
*   [Freeipa30_SSSD_OpenSSH_integration.pdf](https://www.freeipa.org/images/1/10/Freeipa30_SSSD_OpenSSH_integration.pdf)