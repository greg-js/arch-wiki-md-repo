## Share files without a username and password

Edit `/etc/samba/smb.conf` and add the following line:

 `map to guest = Bad User` 

After this line:

 `security = user` 

Restrict the shares data to a specific interface replace:

 `;   interfaces = 192.168.12.2/24 192.168.13.2/24` 

with:

```
interfaces = lo eth0
bind interfaces only = true
```

Optionally edit the account that access the shares, edit the following line:

 `;   guest account = nobody` 

For example:

 `   guest account = pcguest` 

And do something in the likes of:

 `# useradd -c "Guest User" -d /dev/null -s /bin/false pcguest` 

Then setup a "" password for user pcguest.

The last step is to create share directory (for write access make writable = yes):

```
[Public Share]
path = /path/to/public/share
available = yes
browsable = yes
public = yes
writable = no

```

**Note:** Make sure the guest also has permission to visit /path, /path/to and /path/to/public, according to [http://unix.stackexchange.com/questions/13858/do-the-parent-directorys-permissions-matter-when-accessing-a-subdirectory](http://unix.stackexchange.com/questions/13858/do-the-parent-directorys-permissions-matter-when-accessing-a-subdirectory)

### Sample Passwordless Configuration

This is the configuration I use with samba 4 for easy passwordless filesharing with family on a home network. Change any options needed to suit your network (workgroup and interface). I'm restricting it to the static IP I have on my ethernet interface, just delete that line if you do not care which interface is used.

 `/etc/samba/smb.conf` 
```
[global]

   workgroup = WORKGROUP

   server string = Media Server

   security = user
   map to guest = Bad User

   log file = /var/log/samba/%m.log

   max log size = 50

   interfaces = 192.168.2.194/24

   dns proxy = no 

[media]
   path = /shares
   public = yes
   only guest = yes
   writable = yes

[storage]
   path = /media/storage
   public = yes
   only guest = yes
   writable = yes

```

## Build Samba without CUPS

Just build without cups installed. From the [Samba Wiki](https://wiki.samba.org/index.php/Samba_as_a_print_server):

> Samba has built-in support [for CUPS] and defaults to CUPS if the development package (aka header files and libraries) could be found at compile time.

Of course, modifications to the PKGBUILD will also be necessary: libcups will have to be removed from the depends and makedepends arrays and other references to cups and printing will need to be deleted. In the case of the 4.1.9-1 PKGBUILD, 'other references' includes lines 169, 170 and 236:

```
    mkdir -p ${pkgdir}/usr/lib/cups/backend
    ln -sf /usr/bin/smbspool ${pkgdir}/usr/lib/cups/backend/smb
  install -d -m1777 ${pkgdir}/var/spool/samba

```