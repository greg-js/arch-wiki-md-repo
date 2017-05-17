The AIF-NG configuration file is in [XML](https://en.wikipedia.org/wiki/XML "wikipedia:XML"). While not perhaps the most "human-readable" format, it is well-structured (unlike JSON), can be parsed by python 3 with no additional modules (unlike YAML), supports nesting (unlike INI), supports commenting (unlike JSON/simple YAML), and supports data validation (unlike both JSON and YAML).

## Contents

*   [1 By Hand](#By_Hand)
*   [2 Generating via aif-config](#Generating_via_aif-config)
*   [3 Validating](#Validating)

## By Hand

For detailed explanation of each component, see [the upstream documentation](https://aif.square-r00t.net/#writing_an_xml_configuration_file). However, here's a quick example with comments (so you can deploy this example live and it will still validate) explaining what each component does/is for.

The comments are enclosed as such:

 `<!-- Comments look like this -->` 
```
<?xml version="1.0" encoding="UTF-8" ?>
<!-- ^ The declaration. Not strictly necessary per spec but highly recommended. -->
<!-- The header and root element. You should leave this as-is. -->
<aif xmlns:aif="http://aif.square-r00t.net/"
     xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
     xsi:schemaLocation="http://aif.square-r00t.net aif.xsd">
    <!-- A storage element contains information about disks, partitions, mounts, etc. -->
    <storage>
        <!-- Each 'disk' element specifies a disk to format. 'diskfmt' can be either "gpt" or "bios". -->
        <disk device="/dev/sda" diskfmt="gpt">
            <!-- Each 'part' element configures a partition. The below would create partitions relative to the entire disk size,
                 but you can specify explicit sizes too (e.g. "200M"). 'fstype' must be one of the disk format type IDs
                 listed at http://www.rodsbooks.com/gdisk/cgdisk-walkthrough.html -->
            <!-- The below would create /dev/sda1 that takes up the first 10% of the disk, and /dev/sda2
                 that takes up the remaining 90%. -->
            <part num="1" start="0%" stop="10%" fstype="ef00" />
            <part num="2" start="10%" stop="100%" fstype="8300" />
        </disk>
        <!-- Self-explanatory. Note that the 'target' is relative to the install HOST, not the newly installed system. -->
        <!-- 'order' is the order in which the mountpoints are to be executed in preparation for install, from lowest to highest. -->
        <!-- Not shown is the 'fstype' and 'opts' attributes. 'fstype' would be used to force an explicit filesystem at mounttime
             (e.g. mount -t ext3... would be fstype="ext3"). 'opts' is equivalent to mount's -o option, e.g. opts="defaults,noatime". -->
        <mount source="/dev/sda2" target="/mnt/aif" order="1" />
        <mount source="/dev/sda1" target="/mnt/aif/boot" order="2" />
    </storage>
    <!-- The 'network' container element has one attribute, 'hostname'.
         It should be a FQDN, but the domain doesn't need to actually "exist". -->
    <network hostname="aiftest.loc.lan">
        <!-- 'iface' elements specify network interfaces to configure for the newly installed system.
               device: the persistently-named device (e.g. "ens3") or "auto". "auto" will cause AIF-NG to use the
                           first interface it finds with an active link and ignore all other <iface> elements.
               address: either the address (IPv4/IPv6) in CIDR format or "auto" for DHCP(v6).
               netproto: must be either "ipv4", "ipv6", or "both"- "both" is really only useful if address="auto". 
               gateway (not shown): for configuring a gateway if 'address' is a CIDR address (a.k.a. static)
               resolvers (not shown): a comma-separated list of DNS resolvers to configure (especially useful if
                            'address' is a static IP/CIDR) -->
        <iface device="auto" address="auto" netproto="ipv4" />
    </network>
    <!-- The 'system' element controls some basic system settings. -->
    <!-- If e.g. locale="en_US", it will generate locales for all those matching that (i.e. both en_US ISO-8859-1
               and en_US.UTF-8 UTF-8). locale="en" would generate locales for ALL en localizations. -->
    <!-- The 'timezone' attribute should be one of the outputs offered by `timedatectl list-timezones`. -->
    <!-- The 'chrootpath' attribute should be where to chroot into for the install, which means you should probably have it
               as one of your <mount>s, and it should probably be the first one (order="1"). -->
    <!-- The 'reboot' attribute is a boolean, 1/true means "reboot the host after the install completes" and 0/false means
               "leave the installing host running after install has completed". -->
    <system timezone="UTC" locale="en_US.UTF-8" chrootpath="/mnt/aif" reboot="1">
        <!-- The 'users' container contains users to configure. -->
        <!-- The 'rootpass' attribute is a properly hashed/salted string suitable for /etc/shadow. It can also be "" (which means
                            a BLANK password- just hit enter to log in) or "!" (disable TTY login but still allow e.g. SSH access) -->
        <users rootpass="!" />
            <!-- Each user gets their own element. -->
            <!-- ATTRIBUTES:
                      name: the username
                      sudo: a boolean; should full sudo access be given to this user? 0/false or 1/true
                      password: same rules for rootpass
                      comment: the comment for the user, usually the user's full name
                      uid: an explicit UID to give the user, if you'd like
                      group: a primary group to assign to the user, otherwise the user's username.
                      gid: the GID to use as the primary group for the user if 'group' was specified; optional. -->
            <!-- The below password is a salted and hashed string "test" (without quotes). -->
            <user name="aifusr"
                      sudo="1"
                      password="$6$FT90VH.6ZTtrsMQr$uFdpknTbVFYsiP1XB1qe84Lgfbofx9UaGVUq4qNlNuGoHT0.dpVewqC79b/TN/LtqUrRi/qvkgjqnJ8ntbbwD0"
                      comment="A Test User"/>
            <!-- Here we do something a little differently; we essentially create another "nobody" user (uid/gid 99 is nobody)... -->
            <user name="anotherusr" sudo="0" password="" comment="Another Test User" uid="99" group="nobody" gid="99">
                <!-- And give it a 'home' element so it doesn't have a /home/anotherusr directory as its home.
                        We also tell AIF-NG the directory needs to be created via the 'create' boolean. -->
                <home path="/var/empty/anotherusr" create="1" />
                <!-- And we also assign it its own group as well via an "eXtra GROUP", or 'xgroup'. Not shown is the 'gid' attribute,
                        which behaves like <user>'s 'gid' attribute- except it's applied to the group (/etc/group). -->
                <xgroup name="unprivileged" create="1"/>
            </user>
        <!-- Services that should be enabled or disabled. They'll probably require installation, see the <package> element. -->
        <!-- The 'name' attribute is the name of the service (can also be e.g. "sshd.service"). The 'status' attribute is a boolean;
                0/false for explicitly disabled and 1/true for enabled. -->
        <service name="sshd" status="1" />
        <service name="cronie" status="1" />
        <service name="haveged" status="1" />
    </system>
    <!-- The 'pacman' container element is used to install extra software and configure the package manager you would like to use. -->
    <!-- The 'command' attribute is the command to use to install packages. We have configured and installed apacman via a "pkg-execution
            hook script", see the <script> element below. -->
    <pacman command="apacman -S">
        <!-- These are the repositories used for bootstrapping on the host and installation of extra software in the newly-installed
                system (inside the chroot). -->
        <repos>
            <!-- Each repository for pacman.conf gets its own element. -->
            <!-- ATTRIBUTES:
                    name: the name of the repository, as it would appear in /etc/pacman.conf inside the brackets (leave the brackets off)
                    enabled: a boolean; 1/true means "add the repository to pacman.conf",
                                0/false means "add the repository but leave it commented out"
                    siglevel: "default" means use the default in pacman.conf, otherwise you can specify another siglevel here- exactly as
                                it would be specified in pacman.conf (e.g. siglevel="Required DatabaseOptional")
                    mirror: the URI to use for the mirror (either http://, https://, or file://. If it's a file://, it's treated
                                as an Include = directive
                                    (e.g. mirror="file:///var/tmp/mirrorlist" in <repo> == "Include = /var/tmp/mirrorlist" in pacman.conf -->
            <repo name="core" enabled="true" siglevel="default" mirror="file:///etc/pacman.d/mirrorlist" />
            <repo name="extra" enabled="true" siglevel="default" mirror="file:///etc/pacman.d/mirrorlist" />
            <repo name="community" enabled="true" siglevel="default" mirror="file:///etc/pacman.d/mirrorlist" />
            <repo name="multilib" enabled="true" siglevel="default" mirror="file:///etc/pacman.d/mirrorlist" />
            <repo name="testing" enabled="false" siglevel="default" mirror="file:///etc/pacman.d/mirrorlist" />
            <repo name="multilib-testing" enabled="false" siglevel="default" mirror="file:///etc/pacman.d/mirrorlist" />
            <repo name="archlinuxfr" enabled="false" siglevel="Optional TrustedOnly" mirror="http://repo.archlinux.fr/$arch" />
        </repos>
        <!-- These are the mirrors you want to use in /etc/pacman.d/mirrorlist (for the host and installed guest). It is optional. -->
        <!-- Note that specifying a <mirrorlist> will cause the entirety of /etc/pacman.d/mirrorlist to be overwritten with the mirrors you specify. -->
        <mirrorlist>
            <!-- Each line in the mirrorlist is represented by a <mirror></mirror> encapsulation. They are added (and therefore tried by pacman etc.)
                    in order. -->
            <mirror>http://mirror.us.leaseweb.net/archlinux/$repo/os/$arch</mirror>
            <mirror>http://mirrors.advancedhosters.com/archlinux/$repo/os/$arch</mirror>
            <mirror>http://ftp.osuosl.org/pub/archlinux/$repo/os/$arch</mirror>
            <mirror>http://arch.mirrors.ionfish.org/$repo/os/$arch</mirror>
            <mirror>http://mirrors.gigenet.com/archlinux/$repo/os/$arch</mirror>
            <mirror>http://mirror.jmu.edu/pub/archlinux/$repo/os/$arch</mirror>
        </mirrorlist>
        <!-- The 'software' element contains <package> subelements. -->
        <software>
            <!-- Each package gets its own element. You can specify a repo to install from, but it's optional. -->
            <package name="sed" repo="core" />
            <package name="python" />
            <package name="openssh" />
            <package name="vim" />
            <package name="vim-plugins" />
            <package name="haveged" />
            <package name="byobu" />
            <package name="etc-update" />
            <package name="cronie" />
            <package name="mlocate" />
            <package name="mtree-git" />
        </software>
    </pacman>
    <!-- The bootloader configuration. The 'type' attribute can either be "grub" (for grub2) or "systemd" (for systemd-boot). Note that
            systemd-boot only supports UEFI, so if you're on a BIOS system/configured your disk as "bios", you'll need to use type="grub". -->
    <!-- The 'target' attribute tells the bootloader where to install. For UEFI, this should be where your ESP is located (*inside* the newly-installed
            system/chroot). For BIOS, this should be the path to your boot partition (e.g. /dev/sda1). -->
    <!-- The 'efi' attribute is a boolean that only has meaning if you specified grub as the bootloader. If it's 1/true, install as UEFI. If it's false,
            install as a non-UEFI. -->
    <bootloader type="grub" target="/boot" efi="true" />
    <!-- The 'scripts' element serves as a container for hook scripts. -->
    <scripts>
        <!-- Each script gets its own element. -->
        <!-- ATTRIBUTES:
                uri: can be an http://, https://, ftp://, ftps://, or file:// URI and should point to the script.
                execution: one of "pre", "pkg", or "post":
                            pre: run before we even configure the disks - run on the install host
                            pkg: run before we configure pacman/install packages - run inside the install/chroot
                            post: run after everything else is done and right before we exit the chroot, unmount
                                    everything, and reboot - run inside the install/chroot
                order: the order is unique to each execution section, but it must be unique inside each. i.e. you can have a script ordered
                                    at 1 inside execution="pre", and a script ordered at 1 inside execution="post" but you CANNOT have
                                    two scripts ordered at 1 inside execution="post"; they are run in order lowest to highest inside each
                                    execution hook section.
                authtype (not shown): either "basic" or "digest", if your scripts are behind an HTTP/HTTPS authentication.
                user (not shown): the user to use if authentication is needed - for basic/digest http/https auth or ftp/ftps login
                password (not shown): the password for 'user' (http, https, ftp, ftps URIs if auth is needed)
                realm (not shown): if a realm is needed for HTTP DIGEST auth, you can specify it here- AIF-NG will try to guess otherwise -->
        <script uri="https://aif.square-r00t.net/cfgs/scripts/pkg/python.sh" order="1" execution="pkg" />
        <script uri="https://aif.square-r00t.net/cfgs/scripts/pkg/apacman.py" order="2" execution="pkg" />
        <script uri="https://aif.square-r00t.net/cfgs/scripts/post/sshsecure.py" order="1" execution="post" />
        <script uri="https://aif.square-r00t.net/cfgs/scripts/post/sshkeys.py" order="2" execution="post" />
        <script uri="https://aif.square-r00t.net/cfgs/scripts/post/configs.py" order="3" execution="post" />
    </scripts>
</aif>
```

## Generating via aif-config

The [aif](https://aur.archlinux.org/packages/aif/) and [aif-git](https://aur.archlinux.org/packages/aif-git/) packages provide **/usr/bin/aif-config**, which can be used to generate a configuration file, convert a configuration file from JSON, or validate an existing configuration file.

To create a new configuration file, simply run:

```
aif-config create

```

It will run you through an interactive prompt. If you encounter a question you're not sure how to answer, reply with **wikihelp** and it will display some links to relevant documentation.

By default it will create a file called ./aif.xml but you can change where to save it by invoking as:

```
aif-config create -f path/to/where/to/save/it.xml

```

## Validating

It is a **very** good idea to validate your configuration file before deploying. The aif-config tool will do this by default when creating a configuration file if you have the [python-lxml](https://www.archlinux.org/packages/?name=python-lxml) package installed.

It of course can't logically do every sort of validation, but it will make sure your XML is valid and matches the appropriate schema/spec (/usr/share/doc/aif/aif.xsd). This should rule out most common errors.