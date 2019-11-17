This page serves as a temporary list of packages from [core] at date 2019-11-14 that are reproducible using either the archlinux-repro [A] or makerepropkg [M] tools.

Reproducible:

```
acl-2.2.53-2-x86_64.pkg.tar.xz                      [A,M]
attr-2.4.48-2-x86_64.pkg.tar.xz                     [A,M]
btrfs-progs-5.3.1-3-x86_64.pkg.tar.xz               [A,M]
bzip2-1.0.8-3-x86_64.pkg.tar.xz                     [A,M]
coreutils-8.31-3-x86_64.pkg.tar.xz                  [A,M]
cronie-1.5.5-1-x86_64.pkg.tar.xz                    [A,M]
cryptsetup-2.2.2-1-x86_64.pkg.tar.xz                [A,M]
curl-7.67.0-3-x86_64.pkg.tar.xz                     [A,M]
dhcpcd-8.1.1-2-x86_64.pkg.tar.xz                    [A,M]
findutils-4.7.0-2-x86_64.pkg.tar.xz                 [A,M]
gawk-5.0.1-2-x86_64.pkg.tar.xz                      [A,M]
kmod-26-3-x86_64.pkg.tar.xz                         [A,M]
libedit-20191025_3.1-1-x86_64.pkg.tar.xz            [ ,M] - archlinux-repro fails to find PKGBUILD
mkinitcpio-27-2-any.pkg.tar.xz                      [A,M]
openssl-1.0-1.0.2.t-1-x86_64.pkg.tar.xz             [ ,M] - archlinux-repro fails to find PKGBUILD
openvpn-2.4.8-1-x86_64.pkg.tar.xz                   [A,M]
pacman-5.2.1-1-x86_64.pkg.tar.xz                    [A,M]
patch-2.7.6-8-x86_64.pkg.tar.xz                     [A,M]
sudo-1.8.29-1-x86_64.pkg.tar.xz                     [ ,M] - archlinux-repro fails to find PKGBUILD
systemd-243.78-2-x86_64.pkg.tar.xz                  [A,M]
zstd-1.4.3-2-x86_64.pkg.tar.xz                      [A, ]
xz-5.2.4-2-x86_64.pkg.tar.xz                        [A,M]

```

Tested but not reproducible:

```
grub-2:2.04-3-x86_64.pkg.tar.xz                     [ ,M] - archlinux-repro fails to find PKGBUILD
man-db-2.9.0-1-x86_64.pkg.tar.xz                    [A,M] - [https://lists.gnu.org/archive/html/bug-groff/2019-11/msg00000.html](https://lists.gnu.org/archive/html/bug-groff/2019-11/msg00000.html)

```

Remaining to test:

```
amd-ucode-20191022.2b016af-2-any.pkg.tar.xz
archlinux-keyring-20191018-2-any.pkg.tar.xz
argon2-20190702-2-x86_64.pkg.tar.xz
audit-2.8.5-6-x86_64.pkg.tar.xz
autoconf-2.69-6-any.pkg.tar.xz
automake-1.16.1-2-any.pkg.tar.xz
b43-fwcutter-019-3-x86_64.pkg.tar.xz
base-2-2-any.pkg.tar.xz
bash-5.0.011-2-x86_64.pkg.tar.xz
binutils-2.33.1-2-x86_64.pkg.tar.xz
bison-3.4.2-2-x86_64.pkg.tar.xz
bridge-utils-1.6-4-x86_64.pkg.tar.xz
ca-certificates-20181109-2-any.pkg.tar.xz
ca-certificates-mozilla-3.47-2-x86_64.pkg.tar.xz
ca-certificates-utils-20181109-2-any.pkg.tar.xz
cracklib-2.9.7-2-x86_64.pkg.tar.xz
crda-4.14-3-x86_64.pkg.tar.xz
dash-0.5.10.2-2-x86_64.pkg.tar.xz
db-5.3.28-5-x86_64.pkg.tar.xz
dbus-1.12.16-3-x86_64.pkg.tar.xz
dbus-docs-1.12.16-3-x86_64.pkg.tar.xz
device-mapper-2.02.186-3-x86_64.pkg.tar.xz
dialog-1:1.3_20191110-2-x86_64.pkg.tar.xz
diffutils-3.7-3-x86_64.pkg.tar.xz
ding-libs-0.6.1-3-x86_64.pkg.tar.xz
dmraid-1.0.0.rc16.3-12-x86_64.pkg.tar.xz
dnssec-anchors-20190629-2-any.pkg.tar.xz
dosfstools-4.1-3-x86_64.pkg.tar.xz
e2fsprogs-1.45.4-2-x86_64.pkg.tar.xz
ed-1.15-2-x86_64.pkg.tar.xz
efibootmgr-16-2-x86_64.pkg.tar.xz
efivar-37-2-x86_64.pkg.tar.xz
elfutils-0.177-2-x86_64.pkg.tar.xz
expat-2.2.9-2-x86_64.pkg.tar.xz
fakeroot-1.24-2-x86_64.pkg.tar.xz
file-5.37-4-x86_64.pkg.tar.xz
filesystem-2019.10-2-x86_64.pkg.tar.xz
flex-2.6.4-3-x86_64.pkg.tar.xz
gcc-9.2.0-4-x86_64.pkg.tar.xz
gcc-ada-9.2.0-4-x86_64.pkg.tar.xz
gcc-d-9.2.0-4-x86_64.pkg.tar.xz
gcc-fortran-9.2.0-4-x86_64.pkg.tar.xz
gcc-go-9.2.0-4-x86_64.pkg.tar.xz
gcc-libs-9.2.0-4-x86_64.pkg.tar.xz
gcc-objc-9.2.0-4-x86_64.pkg.tar.xz
gdbm-1.18.1-3-x86_64.pkg.tar.xz
gettext-0.20.1-3-x86_64.pkg.tar.xz
glib2-2.62.2-2-x86_64.pkg.tar.xz
glib2-docs-2.62.2-2-x86_64.pkg.tar.xz
glibc-2.30-3-x86_64.pkg.tar.xz
gmp-6.1.2-3-x86_64.pkg.tar.xz
gnupg-2.2.17-3-x86_64.pkg.tar.xz
gnutls-3.6.10-2-x86_64.pkg.tar.xz
gpgme-1.13.1-3-x86_64.pkg.tar.xz
gpm-1.20.7.r27.g1fd1941-2-x86_64.pkg.tar.xz
grep-3.3-3-x86_64.pkg.tar.xz
groff-1.22.4-2-x86_64.pkg.tar.xz
grub-2:2.04-3-x86_64.pkg.tar.xz
gssproxy-0.8.2-2-x86_64.pkg.tar.xz
gzip-1.10-3-x86_64.pkg.tar.xz
hdparm-9.58-3-x86_64.pkg.tar.xz
hwids-20191025-2-any.pkg.tar.xz
iana-etc-20191030-1-any.pkg.tar.xz
icu-65.1-2-x86_64.pkg.tar.xz
ifenslave-1.1.0-11-x86_64.pkg.tar.xz
inetutils-1.9.4-8-x86_64.pkg.tar.xz
iproute2-5.3.0-2-x86_64.pkg.tar.xz
iptables-1:1.8.3-3-x86_64.pkg.tar.xz
iptables-nft-1:1.8.3-3-x86_64.pkg.tar.xz
iputils-20190709-2-x86_64.pkg.tar.xz
ipw2100-fw-1.3-10-any.pkg.tar.xz
ipw2200-fw-3.1-8-any.pkg.tar.xz
iw-5.3-2-x86_64.pkg.tar.xz
jfsutils-1.1.15-7-x86_64.pkg.tar.xz
json-c-0.13.1-3-x86_64.pkg.tar.xz
kbd-2.2.0-5-x86_64.pkg.tar.xz
keyutils-1.6.1-2-x86_64.pkg.tar.xz
krb5-1.17-2-x86_64.pkg.tar.xz
ldns-1.7.1-2-x86_64.pkg.tar.xz
less-551-3-x86_64.pkg.tar.xz
lib32-gcc-libs-9.2.0-4-x86_64.pkg.tar.xz
lib32-glibc-2.30-3-x86_64.pkg.tar.xz
libaio-0.3.112-2-x86_64.pkg.tar.xz
libarchive-3.4.0-3-x86_64.pkg.tar.xz
libassuan-2.5.3-2-x86_64.pkg.tar.xz
libcap-2.27-2-x86_64.pkg.tar.xz
libcap-ng-0.7.9-2-x86_64.pkg.tar.xz
libelf-0.177-2-x86_64.pkg.tar.xz
libevent-2.1.11-3-x86_64.pkg.tar.xz
libffi-3.2.1-4-x86_64.pkg.tar.xz
libgcrypt-1.8.5-2-x86_64.pkg.tar.xz
libgpg-error-1.36-3-x86_64.pkg.tar.xz
libgssglue-0.4-4-x86_64.pkg.tar.xz
libidn-1.35-2-x86_64.pkg.tar.xz
libidn2-2.3.0-1-x86_64.pkg.tar.xz
libksba-1.3.5-2-x86_64.pkg.tar.xz
libldap-2.4.48-2-x86_64.pkg.tar.xz
libmnl-1.0.4-3-x86_64.pkg.tar.xz
libmpc-1.1.0-2-x86_64.pkg.tar.xz
libnftnl-1.1.4-2-x86_64.pkg.tar.xz
libnghttp2-1.39.2-2-x86_64.pkg.tar.xz
libnl-3.5.0-2-x86_64.pkg.tar.xz
libnsl-1.2.0-2-x86_64.pkg.tar.xz
libpcap-1.9.1-2-x86_64.pkg.tar.xz
libpipeline-1.5.1-2-x86_64.pkg.tar.xz
libpsl-0.21.0-2-x86_64.pkg.tar.xz
libsasl-2.1.27-2-x86_64.pkg.tar.xz
libseccomp-2.4.1-3-x86_64.pkg.tar.xz
libsecret-0.19.1-2-x86_64.pkg.tar.xz
libssh2-1.9.0-2-x86_64.pkg.tar.xz
libtasn1-4.14-3-x86_64.pkg.tar.xz
libtirpc-1.1.4-2-x86_64.pkg.tar.xz
libtool-2.4.6+42+gb88cebd5-7-x86_64.pkg.tar.xz
libunistring-0.9.10-2-x86_64.pkg.tar.xz
libusb-1.0.23-2-x86_64.pkg.tar.xz
libutil-linux-2.34-6-x86_64.pkg.tar.xz
licenses-20191011-2-any.pkg.tar.xz
links-2.20.2-2-x86_64.pkg.tar.xz
linux-5.3.11.1-1-x86_64.pkg.tar.xz
linux-api-headers-5.3.1-2-any.pkg.tar.xz
linux-docs-5.3.11.1-1-x86_64.pkg.tar.xz
linux-firmware-20191022.2b016af-2-any.pkg.tar.xz
linux-headers-5.3.11.1-1-x86_64.pkg.tar.xz
linux-lts-4.19.84-1-x86_64.pkg.tar.xz
linux-lts-docs-4.19.84-1-x86_64.pkg.tar.xz
linux-lts-headers-4.19.84-1-x86_64.pkg.tar.xz
logrotate-3.15.1-2-x86_64.pkg.tar.xz
lvm2-2.02.186-3-x86_64.pkg.tar.xz
lz4-1:1.9.2-2-x86_64.pkg.tar.xz
lzo-2.10-3-x86_64.pkg.tar.xz
m4-1.4.18-3-x86_64.pkg.tar.xz
make-4.2.1-4-x86_64.pkg.tar.xz
man-db-2.9.0-1-x86_64.pkg.tar.xz
man-pages-5.03-2-any.pkg.tar.xz
mdadm-4.1-2-x86_64.pkg.tar.xz
minizip-1:1.2.11-4-x86_64.pkg.tar.xz
mkinitcpio-busybox-1.30.1-2-x86_64.pkg.tar.xz
mkinitcpio-nfs-utils-0.3-7-x86_64.pkg.tar.xz
mlocate-0.26.git.20170220-2-x86_64.pkg.tar.xz
mpfr-4.0.2-2-x86_64.pkg.tar.xz
nano-4.5-2-x86_64.pkg.tar.xz
ncurses-6.1-7-x86_64.pkg.tar.xz
net-tools-1.60.20181103git-2-x86_64.pkg.tar.xz
netctl-1.20-2-any.pkg.tar.xz
nettle-3.5.1-2-x86_64.pkg.tar.xz
nfs-utils-2.4.1-3-x86_64.pkg.tar.xz
nfsidmap-2.4.1-3-x86_64.pkg.tar.xz
nilfs-utils-2.2.8-2-x86_64.pkg.tar.xz
npth-1.6-2-x86_64.pkg.tar.xz
nspr-4.23-2-x86_64.pkg.tar.xz
nss-3.47-2-x86_64.pkg.tar.xz
openldap-2.4.48-2-x86_64.pkg.tar.xz
openresolv-3.9.2-2-any.pkg.tar.xz
openssh-8.1p1-2-x86_64.pkg.tar.xz
openssl-1.1.1.d-2-x86_64.pkg.tar.xz
p11-kit-0.23.18.1-2-x86_64.pkg.tar.xz
pacman-mirrorlist-20191001-2-any.pkg.tar.xz
pam-1.3.1-2-x86_64.pkg.tar.xz
pambase-20190105.1-2-any.pkg.tar.xz
pciutils-3.6.2-2-x86_64.pkg.tar.xz
pcre-8.43-2-x86_64.pkg.tar.xz
pcre2-10.33-2-x86_64.pkg.tar.xz
perl-5.30.1-1-x86_64.pkg.tar.xz
pinentry-1.1.0-5-x86_64.pkg.tar.xz
pkcs11-helper-1.25.1-2-x86_64.pkg.tar.xz
pkgconf-1.6.3-3-x86_64.pkg.tar.xz
popt-1.16-11-x86_64.pkg.tar.xz
ppp-2.4.7-6-x86_64.pkg.tar.xz
pptpclient-1.10.0-2-x86_64.pkg.tar.xz
procinfo-ng-2.0.304-8-x86_64.pkg.tar.xz
procps-ng-3.3.15-2-x86_64.pkg.tar.xz
psmisc-23.3-2-x86_64.pkg.tar.xz
pth-2.0.7-7-x86_64.pkg.tar.xz
python-audit-2.8.5-6-x86_64.pkg.tar.xz
python-gpgme-1.13.1-3-x86_64.pkg.tar.xz
qgpgme-1.13.1-3-x86_64.pkg.tar.xz
readline-8.0.001-2-x86_64.pkg.tar.xz
reiserfsprogs-3.6.27-3-x86_64.pkg.tar.xz
rpcbind-1.2.5-3-x86_64.pkg.tar.xz
run-parts-4.8.6.1-2-x86_64.pkg.tar.xz
s-nail-14.9.15-2-x86_64.pkg.tar.xz
sdparm-1.10-3-x86_64.pkg.tar.xz
sed-4.7-3-x86_64.pkg.tar.xz
shadow-4.7-3-x86_64.pkg.tar.xz
sqlite-3.30.1-2-x86_64.pkg.tar.xz
sqlite-analyzer-3.30.1-2-x86_64.pkg.tar.xz
sqlite-doc-3.30.1-2-x86_64.pkg.tar.xz
sqlite-tcl-3.30.1-2-x86_64.pkg.tar.xz
sysfsutils-2.1.0-11-x86_64.pkg.tar.xz
syslinux-6.04.pre2.r11.gbf6db5b4-2-x86_64.pkg.tar.xz
tar-1.32-3-x86_64.pkg.tar.xz
texinfo-6.7-2-x86_64.pkg.tar.xz
thin-provisioning-tools-0.8.5-3-x86_64.pkg.tar.xz
traceroute-2.1.0-3-x86_64.pkg.tar.xz
tzdata-2019c-3-x86_64.pkg.tar.xz
usbutils-012-2-x86_64.pkg.tar.xz
util-linux-2.34-6-x86_64.pkg.tar.xz
vi-1:070224-4-x86_64.pkg.tar.xz
which-2.21-5-x86_64.pkg.tar.xz
wireless-regdb-2019.06.03-2-any.pkg.tar.xz
wireless_tools-30.pre9-3-x86_64.pkg.tar.xz
wpa_supplicant-2:2.9-2-x86_64.pkg.tar.xz
xfsprogs-5.2.1-3-x86_64.pkg.tar.xz
xinetd-2.3.15-6-x86_64.pkg.tar.xz
zlib-1:1.2.11-4-x86_64.pkg.tar.xz

```