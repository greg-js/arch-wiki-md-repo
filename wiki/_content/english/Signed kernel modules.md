Related articles

*   [Kernels](/index.php/Kernels "Kernels")
*   [Kernel module](/index.php/Kernel_module "Kernel module")
*   [Kernel/Arch_Build_System](/index.php/Kernel/Arch_Build_System "Kernel/Arch Build System")

Signed [[1]](https://www.kernel.org/doc/html/v5.4-rc2/admin-guide/module-signing.html) [Kernel modules](/index.php/Kernel_modules "Kernel modules") provide a mechanism for the kernel to verify the integrity of a module.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Overview](#Overview)
*   [2 How to sign kernel modules using a custom kernel](#How_to_sign_kernel_modules_using_a_custom_kernel)
*   [3 Summary of what needs to be done](#Summary_of_what_needs_to_be_done)
*   [4 Kernel Config](#Kernel_Config)
    *   [4.1 Boot Command Line](#Boot_Command_Line)
*   [5 Tools needed](#Tools_needed)
    *   [5.1 kernel build package](#kernel_build_package)
    *   [5.2 dkms support](#dkms_support)
*   [6 Modify PKGBUILD](#Modify_PKGBUILD)
    *   [6.1 prepare()](#prepare())
    *   [6.2 _package-headers()](#package-headers())
*   [7 Files Required](#Files_Required)
    *   [7.1 certs-local/fix_config.sh](#certs-local/fix_config.sh)
    *   [7.2 certs-local/x509.oot.genkey](#certs-local/x509.oot.genkey)
    *   [7.3 certs-local/genkeys.sh](#certs-local/genkeys.sh)
    *   [7.4 certs-local/sign_manual.sh](#certs-local/sign_manual.sh)
    *   [7.5 certs-local/dkms/kernel-sign.conf](#certs-local/dkms/kernel-sign.conf)
    *   [7.6 certs-local/dkms/kernel-sign.sh](#certs-local/dkms/kernel-sign.sh)

## Overview

The Linux Kernel distinguishes and keeps separate the verification of modules from requiring or forcing modules to verify before allowing them to be loaded. Kernel modules fall into 2 classes:

*   Standard 'in tree' modules which come with the kernel source
    *   compiled during the normal kernel build.

*   Out of tree (aka oot) modules which are not part of the kernel source distribution:
    *   Built outside of the kernel tree
    *   Require kernel headers package for each kernel they are to be built for. They can be built manually for a specific kernel and packaged - or they can be built whenever needed using [dkms](/index.php/Dkms "Dkms")
    *   Examples of such packages, provided by arch, include virtualbox and wireguard.

**Note:** During a standard kernel compile, the kernel build tools create a private/public key pair and signs every in tree module (using private key). The public key is saved in the kernel itself. When a module is subsequently loaded, the public key can then be used to verify the module is unchanged.

The kernel can be enabled to always verify modules, and it then reports any failures to standard logs, the choice to permit the loading and use of a module which does not verify can be either compiled in to kernel or turned on at run time using a command line option to kernel boot command as explained below.

## How to sign kernel modules using a custom kernel

The starting point is based on a custom kernel package as outlined in this article [Kernel/Arch Build System](/index.php/Kernel/Arch_Build_System "Kernel/Arch Build System"). We will modify the build to:

*   Sign the standard in tree kernel modules
*   Provide what is needed to have signed out of tree modules and for the kernel to verify those modules.

**Note:** The goal here is to have:

*   In tree modules signed during the standard kernel build process.
    *   The standard kernel build creates a fresh public/private key pair on each build.
*   Out of tree modules are signed and the associated public key is compiled in to the kernel.
    *   We will create a separate public/private key pair on each build.

## Summary of what needs to be done

Each kernel build needs to made aware of the key/cert being used. Fresh keys are generated with each new kernel build.

A kernel config parameter is now used to make kernel aware of additional signing key: `CONFIG_SYSTEM_TRUSTED_KEYS="/path/to/oot-signing_keys.pem"`.

Keys and signing tools will be stored in current module build directory. Nothing needs to be done to clean this as removal is handled by the standard module cleanup. Certs are thus installed in `/usr/lib/modules/<kernel-vers>-<build>/certs-local`

## Kernel Config

**Note:** `CONFIG_SYSTEM_TRUSTED_KEYS` will be added automatically as explained below. In addition the following config options should be set by either manually editing the 'config' file, or via `make menuconfig` in the linux 'src' area and subsequently copying the updated '.config' file back to the build file 'config'.

```
Enable Loadable module suppot --->
Module Signature Verification           -  activate
        CONFIG_MODULE_SIG=y

Require modules to be validly signed -> leave off
        CONFIG_MODULE_SIG_FORCE=n

        This allows the decision to enforce verified modules only as boot command line.
        If you're comfortable all is working then by all means change this to 'y'
        Command line version of this is : module.sig_enforce=1

Automatically sign all modules  - activate
Which hash algorithm    -> SHA-512

Compress modules on installation        - activate
        Compression algorithm (XZ)

Allow loading of modules with missing namespace imports - set to no

```

### Boot Command Line

After you are comfortable things are working well you can enable the boot command line option to require that the kernel only permit verified modules to be loaded:

```
module.sig_enforce=1

```

## Tools needed

### kernel build package

```
       In the directory where the kernel package is built:

       `% mkdir certs-local`

       This directory will provide the tools to create the keys, as well as signing kernel modules.
       Put the 4 files into certs-local:

               fix_config.sh
               x509.oot.genkey
               genkeys.sh
               sign_manual.sh

       The files genkeys.sh and its config x509.oot.genkey are used to create key pairs.
       the file fix_config.sh is run after that to provide the kernel with the key info by updating
       the config file used to build the kernel.
       The script sign_manual will be used to sign out of tree kernel modules.

       genkeys.sh will create the key pairs in a dir named by date-time.
       It also creates file 'current_key_dir' with that dir name and a soft link 'current' to 
       the same dir with the 'current' key pairs.

       These files are all provided below.

```

### dkms support

```
       `% mkdir certs-local/dkms`

       Add 2 files to the dkms dir:
               kernel-sign.conf
               kernel-sign.sh

       These will be installed in /etc/dkms and provide a mechanism for dkms to automatically
       sign modules (using the local key above) - this is the reccommended way to sign kernel 
       modules. As explained, below - once this is installed - all that is needed to have dkms
       automatically sign modules is to make a soft link:

       % cd /etc/dkms
       % ln -s kernel-sign.conf <package-name>

       e.g.
       % ln -s kernel-sign.conf virtualbox

       The link creation can easily be added to an arch package to simplify further if desired.

```

## Modify PKGBUILD

We need to make changes to kernel build as follows:

### prepare()

**Note:** Add the following to the top of the prepare() function:

```
       prepare() {

           msg2 "Rebuilding local signing key..."
           cd ../certs-local
           ./genkeys.sh 

           msg2 "Updating kernel config with new key..."
           ./fix_config.sh ../config
           cd ../src

           ... 
       }

```

### _package-headers()

**Note:** Add the following to the bottom of the _package-headers() function:

```
        _package-headers() {

       ...

         #
         # Out of Tree Module signing
         # This is run in the kernel source / build directory
         #
         msg2 "Local Signing certs for out of tree modules..."

         certs_local_src="../../certs-local" 
         key_dir=$(<${certs_local_src}/current_key_dir)

         certs_local_dst="${builddir}/certs-local"
         signer="sign_manual.sh"
         mkdir -p ${certs_local_dst}
         rsync -a $certs_local_src/{current,$key_dir,$signer} $certs_local_dst/

         # dkms tools
         dkms_src="$certs_local_src/dkms"
         dkms_dst="${pkgdir}/etc/dkms"
         mkdir -p $dkms_dst

         rsync -a $dkms_src/{kernel-sign.conf,kernel-sign.sh} $dkms_dst/
   }

```

## Files Required

**Note:** These are the 6 supporting files referenced above

**Tip:** Don't forget to make the scripts executable.

i.e.

```
chmod +x certs-local/*.sh certs-local/dkms/*.sh

```

### certs-local/fix_config.sh

```
#!/bin/bash
#
# Arg: config file
# 
# Update kernel config : CONFIG_SYSTEM_TRUSTED_KEYS to use current keys
#

Config="$1"

KeyDir=$(<current_key_dir)

sed -e "s|^CONFIG_SYSTEM_TRUSTED_KEYS=.*|CONFIG_SYSTEM_TRUSTED_KEYS=\"../../certs-local/$KeyDir/signing_key.pem\"|"  < $Config  > $Config.tmp

mv $Config.tmp $Config

exit 0
```

### certs-local/x509.oot.genkey

```
[ req ]
default_bits = 4096
distinguished_name = req_distinguished_name
prompt = no
string_mask = utf8only
x509_extensions = myexts 

[ req_distinguished_name ]
#O = Unspecified company
CN = Out of tree kernel module signing key
#emailAddress = unspecified.user@unspecified.company

[ myexts ]
basicConstraints=critical,CA:FALSE
keyUsage=digitalSignature
subjectKeyIdentifier=hash
authorityKeyIdentifier=keyid
```

### certs-local/genkeys.sh

```
#!/bin/bash
#
# Create new pub/priv key pair for signing out of tree kernel modules.
#
# Each key pair is stored by date-time
#

Dt=$(date +'%Y%m%d-%H%M')

mkdir -p $Dt

KernKey="${Dt}/signing_key.pem"
PrivKey="${Dt}/signing_prv.key"
KernCrt="${Dt}/signing_crt.crt"

openssl req -new -nodes -utf8 -sha512 -days 36500 -batch -x509 -config ./x509.oot.genkey \
        -outform PEM -out $KernKey -keyout $KernKey

chmod 0600 $KernKey
openssl pkey -in $KernKey -out $PrivKey
openssl x509 -outform der -in $KernKey -out $KernCrt

rm -f current; ln -s $Dt current

rm -f current_key_dir
echo "$Dt" > ./current_key_dir

exit 0
```

### certs-local/sign_manual.sh

```
#!/bin/bash
#
# Out of Tree Module Sign script:
#
# This will be installed in 
#
# /usr/lib/modules/<kernel-vers>/build/certs-local
#
#  Uses dirs :
#    Tmp   - working directory
#
# Requires:
# 
# Ensure that signing is idempotent.
#

#
# Inputs
#
HASH=sha512
Modules="$@"

#
# Where 
#
MyRealpath=$(realpath $0)
MyDirName=$(dirname $MyRealpath)
BuildDir=${MyDirName%/*}

SIGN=${BuildDir}/scripts/sign-file

#
# Keys
#
KEY=${MyDirName}/current/signing_key.pem
CRT=${MyDirName}/current/signing_crt.crt

#
# Sign them 
#
echo "Module signing key : $KEY"

function is_signed () {
     f=$1
     has_sig='n'
     hexdump -C $f |tail  |grep 'Module sign' > /dev/null
     rc=$?
     if [ $rc = 0 ] ; then
         has_sig='y' 
     fi
     echo $has_sig
}

#
# Do it
#
for mod in $Modules
do

    moddir=$(dirname $mod) 

    if [ "$moddir" = "." ] ; then
        moddir="./"
    fi

    #
    # Create Tmp
    #
    if [ ! -d $moddir/Tmp ] ; then
        mkdir -p $moddir/Tmp
    fi

    rsync -a $mod $moddir/Tmp/
    mod_tmp=$moddir/Tmp/${mod}

    #
    # Decompress tmp file if needed
    #

    ext=${mod##*.}
    isxz='n'
    if [ "$ext" = "xz" ] ; then
        echo "Decompressing :"
        isxz='y'
        xz -f --decompress $mod_tmp
        mod_tmp=${mod_tmp%*.xz}
    fi

    #
    # remove any existing signature before signing
    #
    is_sig=$(is_signed $mod_tmp)
    if [ "$is_sig" = 'y' ] ; then
        echo "Removing old sig :"
        strip --strip-debug $mod_tmp
    fi

    echo "Signing $mod_tmp"
    $SIGN  sha512 $KEY $CRT $mod_tmp

    if [ "$isxz" = "y" ] ; then
        echo "Compressing:"
        xz -f $mod_tmp
        mod_tmp=${mod_tmp}.xz
    fi

    #
    # backup current and install newly signed module
    # How to backup without older module being treated as a real module?
    # Maybe create /usr/lib/modules/<vers>/module-backup/xxx
    # real modules are in usr/lib/modules/<vers>/kernel/xxx
    # so could derive backup path by s/kernel/module-backup/
    # rsync -a $mod $moddir/Prev/${mod}
    # problem is this script could be run on modules outside standard kernel module tree
    # so for now no backups
    #
    mv $mod_tmp $mod

done

exit
```

### certs-local/dkms/kernel-sign.conf

```
# 
# Installed as /etc/dkms/kernel-sign.conf
#
# link this to any module to be signed
#
# e.g. ln -s /etc/dkms/kernel-sign.conf /etc/dkms/virtualbox.conf

POST_BUILD=../../../../../../etc/dkms/kernel-sign.sh
```

### certs-local/dkms/kernel-sign.sh

```
#!/bin/bash
#
# Installed in /etc/dkms/kernel-sign.sh
#
#  This is called via POST_BUILD for each module 
#  We use this to sign in the dkms build directory.  
#

cd ../$kernelver/$arch/module/

#SIGN=$kernel_source_dir/certs-local/sign_manual.sh
SIGN=/usr/lib/modules/$kernelver/build/certs-local/sign_manual.sh

if [ -f $SIGN ] ;then

   list=$(/bin/ls -1 *.ko *.ko.xz 2>/dev/null)

   if [ "$list" != "" ]  ; then
       for mod in $list
       do
           echo "DKMS: Signing kernel ($kernelver) module: $mod"
           $SIGN "$mod"
       done
   fi
else
   echo "kernel $kernelver doesn't have out of tree module signing tools"
   echo "skipping signing out of tree modules"
fi
```