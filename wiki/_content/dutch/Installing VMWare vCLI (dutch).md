De vCLI utilities maken het mogelijk om VMWare ESX servers te beheren al dan niet via vCenter. Hoewel Arch Linux niet behoort tot de "supported platforms" voor deze utilities is het vrij eenvoudig deze te installeren

## Download lokatie

De utilities zijn te downloaden vanaf [http://www.vmware.com/support/developer/vcli](http://www.vmware.com/support/developer/vcli), registratie is hierbij vereist.

## Dependencies

Om vCLI te installeren zijn er de nodige dependencies. Die kun je als volgt installeren:

```
pacman -S e2fsprogs openssl libxml2 perl libxml-perl perl-xml-sax perl-crypt-ssleay \ 
perl-archive-zip perl-html-parser perl-data-dump perl-soap-lite perl-uri \ 
perl-lwp-protocol-https perl-class-methodmaker perl-net-ssleay perl-xml-libxml

```

## Installatie

Pak het archiefbestand uit:

```
tar xzvf VMware-vSphere-CLI-5*.tar.gz

```

En ga naar de aangemaakte directory toe:

```
cd vmware-vsphere-cli-distrib/

```

Open nu het bestand `vmware-install.pl` in je favoriete editor. Pas nu de volgende regels aan:

```
my $installed_ssl_version = '1.0.0';   # regel 5248
my $ssleay_installed = 1;              # regel 5250
my $OpenSSL_installed = 1;             # regel 5256
my $LibXML2_installed = 1;             # regel 5257
my $OpenSSL_dev_installed = 1;         # regel 5258
my $e2fsprogs_installed = 1;           # regel 5261 
my $e2fsprogs_version = '1.42';        # regel 5262
my $install_rhel55_local = 1;          # regel 5266

```

Vervolgens moet er een ftp en een http proxy geconfigureerd worden, ook wanneer deze niet nodig zijn:

```
export ftp_proxy=""
export http_proxy=""

```

Vervolgens kan de installatie gestart worden met:

```
./vmware-install.pl 

```

Foutmeldingen en waarschuwingen over rpm en versie nummers kunnen veilig genegeerd worden.