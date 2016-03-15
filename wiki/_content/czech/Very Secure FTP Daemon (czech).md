**vsftpd** (Very Secure FTP Daemon) je lehký, stabilní a bezpečný FTP server pro UNIX-like systémy.

## Contents

*   [1 Instalace](#Instalace)
*   [2 Konfigurace](#Konfigurace)
    *   [2.1 Povolení uploadu](#Povolen.C3.AD_uploadu)
    *   [2.2 Přihlašování lokálních uživatelů](#P.C5.99ihla.C5.A1ov.C3.A1n.C3.AD_lok.C3.A1ln.C3.ADch_u.C5.BEivatel.C5.AF)
    *   [2.3 Anonymní přihlašování](#Anonymn.C3.AD_p.C5.99ihla.C5.A1ov.C3.A1n.C3.AD)
    *   [2.4 Prostředí chroot](#Prost.C5.99ed.C3.AD_chroot)
    *   [2.5 Zamezení přihlašování uživatelů](#Zamezen.C3.AD_p.C5.99ihla.C5.A1ov.C3.A1n.C3.AD_u.C5.BEivatel.C5.AF)
    *   [2.6 Omezení připojení](#Omezen.C3.AD_p.C5.99ipojen.C3.AD)
    *   [2.7 Použití xinetd](#Pou.C5.BEit.C3.AD_xinetd)
*   [3 Tipy a triky](#Tipy_a_triky)
    *   [3.1 PAM s virtuálními uživatelskými účty](#PAM_s_virtu.C3.A1ln.C3.ADmi_u.C5.BEivatelsk.C3.BDmi_.C3.BA.C4.8Dty)
        *   [3.1.1 Přidání soukromých adresářů pro virtuální uživatelské účty](#P.C5.99id.C3.A1n.C3.AD_soukrom.C3.BDch_adres.C3.A1.C5.99.C5.AF_pro_virtu.C3.A1ln.C3.AD_u.C5.BEivatelsk.C3.A9_.C3.BA.C4.8Dty)
*   [4 Další zdroje](#Dal.C5.A1.C3.AD_zdroje)

## Instalace

Vsftpd je začleněn do oficiálního repozitáře. Instalovat můžete např. pomocí utility pacman:

```
# pacman -S vsftpd

```

Připojení povolíte modifikací souboru `/etc/hosts.allow`:

```
# Povolit všechna připojení
vsftpd: ALL
# Omezit na určený rozsah IP adres
vsftpd: 10.0.0.0/255.255.255.0

```

Server můžete spustit tímto skriptem:

```
# /etc/rc.d/vsftpd start

```

Pokud chcete spustit vsftpd při startu počítače, přidejte ho do pole DAEMONS v souboru `/etc/rc.conf`.

Pokud chcete použít vsftpd s xinetd následujte postup napsaný níže.

## Konfigurace

Většiny nastavení docílíte editací souboru `/etc/vsftpd.conf`. Soubor je dobře zdokumentovaný, a proto tato sekce poukazuje pouze na některé důležité změny. Pro všechny možnosti a dokumentaci můžete použít man vsftpd.conf (5).

### Povolení uploadu

Pokud chcete povolit změny na souborovém systému, jako například při uploadu, `WRITE_ENABLE` musíte nastavit na YES v souboru `/etc/vsftpd.conf`:

```
write_enable=YES

```

### Přihlašování lokálních uživatelů

Pro povolení přihlašování uživatelů v souboru `/etc/passwd` nastavte tento řádek v souboru `/etc/vsftpd.conf`:

```
local_enable=YES

```

### Anonymní přihlašování

Tyto řádky v souboru `/etc/vsftpd.conf` určují, zda se anonymní uživatelé mohou přihlásit:

```
anonymous_enable=YES # Povolí anonymní přihlášení
no_anon_password=YES # Nevyžadovat heslo k anonymnímu přihlášení
anon_max_rate=30000  # Maximální rychlost přenosu anonymními uživateli v bytech za sekundu

```

### Prostředí chroot

Je možné nastavit prostředí chroot, které uživatelům zamezí opouštění jejich domovského adresáře. Pro povolení zapište následující řádky do souboru `/etc/vsftpd.conf`:

```
chroot_list_enable=YES
chroot_list_file=/etc/vsftpd.chroot_list

```

Proměnná `chroot_list_file` udává soubor se seznamem uživatelů, kteří jsou uzavřeni do prostředí chroot.

Pro ještě přísnější nastavení můžete použít tyto řádky:

```
chroot_local_user=YES

```

Toto nastavení v základu uzavře lokální uživatele fo prostředí chroot. V tomto případě, soubor udaný proměnnou `chroot_list_file` obsahuje seznam uživatelů, kteří **nejsou** uzavřeni do prostředí chroot.

### Zamezení přihlašování uživatelů

Je možné zamezit uživatelům přístup k FTP serveru přidáním 2 řádek do souboru `/etc/vsftpd.conf`:

```
userlist_enable=YES
userlist_file=/etc/vsftpd.user_list

```

`chroot_list_file` nyní určuje uživatele, kteří se nesmí přihlásit.

Pokud chcete naopak pouze některým uživatelům povolit přístup, přidejte řádek:

```
userlist_deny=NO

```

Soubor určený na řádku `chroot_list_file` pak obsahuje uřivatele, kteří se mohou přihlásit.

### Omezení připojení

Můžete omezit rychlost přenosu dat, počet klientů a počet připojení na jednu IP adresu pro lokální uživatele, přidáním těchto řádek do souboru `/etc/vsftpd.conf`:

```
local_max_rate=1000000 # Maximální rychlost přenosu dat v bytech za sekundu
max_clients=50         # Maximální počet klientů, kteří mohou být připojeni
max_per_ip=2           # Maximální počet připojení na jednu IP adresu

```

### Použití xinetd

Pokud chcete použít vsftpd s xinetd, přidejte následující řádky do souboru `/etc/xinetd.d/vsftpd`:

```
service ftp
{
        socket_type             = stream
        wait                    = no
        user                    = root
        server                  = /usr/sbin/vsftpd
        log_on_success  += HOST DURATION
        log_on_failure  += HOST
        disable                 = no
}

```

Tyto volby by měly být nastaveny v souboru `/etc/vsftpd.conf`:

```
tcp_wrappers=YES        # Použít tcp_wrappers ke správě připojení. Poté povolit v hosts.allow
pam_service_name=vsftpd

```

Poté se ujistěte, že je vsftpd povolen pro IP adresy, které se mají připojovat k serveru, v souboru `/etc/hosts.allow`:

```
vsftpd: ALL

```

Nakonec přidejte xinetd do pole DAEMONS v souboru `/etc/rc.conf`. Není třeba přidávat vsftpd, neboť bude spuštěn utilitou xinetd kdykoliv bude třeba.

Pokud při připojování k serveru dostáváte chybová hlášení jako toto:

```
500 OOPS: cap_set_proc

```

Je třeba přidat *capability* do pole MODULES= v souboru `/etc/rc.conf`.

Po přejití na verzi 2.1.0 můžete dostávát během připojování chybová hlášení jako toto:

```
500 OOPS: could not bind listening IPv4 socket

```

V předešlých verzích stačilo nechat tyto řádky zakomentované:

```
# Toto použijte k nastavení vsftpd do samostatného módu nebo vsftpd bude fungovat s (x)inetd
# listen=YES

```

V této verzi, a nejspíše i v budoucích, je třeba explicitně nastavit vsftpd, aby neběžel v samostatném módu:

```
# Toto použijte k nastavení vsftpd do samostatného módu nebo vsftpd bude fungovat s (x)inetd
listen=NO

```

## Tipy a triky

### PAM s virtuálními uživatelskými účty

Používání virtuálních uživatelů přináší výhodu v nevyžadování reálného uživatelského účtu v systému. Keeping the environment in a container is of course a more secure option.

Pro vytvoření databáze uživatelů, je nejdříve třeba vytvořit jednoduchý textový soubor, jako například tento:

```
uživatel1
heslo1
uživatel2
heslo2

```

Vložte kolik virtuálních uživatelů potřebujete, jen je třeba zachovat strukturu souboru. Seznam uložte jako logins.txt; na názvu souboru nezáleží. Další krok závisí na databázovém systému Berkeley, který je zahrnutý v základním systému Arch. Jako uživatel root vytvořte databázi ze souboru login.txt (nebo jak jste ho pojmenovali):

```
# db_load -T -t hash -f logins.txt /etc/vsftpd_login.db

```

Je vhodné omezit oprávnění k nově vzniklému souboru `vsftpd_login.db`:

```
# chmod 600 /etc/vsftpd_login.db

```

**Warning:** Ukládání hesel v čistém textu není bezpečné, proto nezapomeňte smazat dočasný soubor tímto příkazem `rm logins.txt`.

Nyní je třeba zajistit aby PAM byl schopný uživatele identifikovat podle vsftpd_login.db. K docílení tohoto stavu je třeba vytvořit soubor s názvem ftp v adresáři `/etc/pam.d/`, který obsahuje tyto volby:

```
auth required pam_userdb.so db=/etc/vsftpd_login crypt=hash 
account required pam_userdb.so db=/etc/vsftpd_login crypt=hash

```

**Note:** Při nastavování PAM je použit /etc/vsftpd_login bez přípony .db!

Dále je třeba vytvořit domovské adresáře pro virtuální uživatele. Pro příklad můžete použít adresář `/srv/ftp` pro hosting dat virtuálních uživatelů. Tento příklad také respektuje základní adresářovou strukturu systému Arch. Nejdříve tedy vytvořte uživatele virtual a učiňte `/srv/ftp` jeho domovským adresářem:

```
# useradd -d /srv/ftp virtual

```

Učiňte uživatele virtual vlastníkem:

```
# chown virtual:virtual /srv/ftp

```

Nastavte vsftpd, aby využíval právě vytvořené prostředí, v souboru /etc/vsftpd.conf. Toto je nezbytné nastavení, které omezí přístup pouze na virtuální uživatele, kteří se boudou moci přihlásit pod svým uživatelským jménem a heslem a omezí jejich přístup pouze na adresář `/srv/ftp`:

```
anonymous_enable=NO
local_enable=YES
chroot_local_user=YES
guest_enable=YES
guest_username=virtual
virtual_use_local_privs=YES

```

Pokud je použita metoda, kdy xinetd spouští službu, vsftpd by měl povolit přístup pouze po přihlášení kombinací uživatelského jména a hesla, která byla definována v databázi.

#### Přidání soukromých adresářů pro virtuální uživatelské účty

Nejdříve vytvořte složky pro uživatele:

```
# mkdir /srv/ftp/user1
# mkdir /srv/ftp/user2
# chown virtual:virtual /srv/ftp/user?/

```

Poté přidejte následující řádky do souboru `/etc/vsftpd.conf`:

```
local_root=/srv/ftp/$USER
user_sub_token=$USER

```

## Další zdroje

*   [Oficiální stránka vsftpd](http://vsftpd.beasts.org/)
*   [vsftpd.conf man stránka](http://vsftpd.beasts.org/vsftpd_conf.html)