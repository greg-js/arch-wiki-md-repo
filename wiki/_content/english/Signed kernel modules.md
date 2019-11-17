Related articles

*   [Kernels](/index.php/Kernels "Kernels")
*   [Kernel module](/index.php/Kernel_module "Kernel module")
*   [Kernel/Arch Build System](/index.php/Kernel/Arch_Build_System "Kernel/Arch Build System")

[Signed](https://www.kernel.org/doc/html/latest/admin-guide/module-signing.html) [kernel modules](/index.php/Kernel_modules "Kernel modules") provide a mechanism for the kernel to verify the integrity of a module.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Overview](#Overview)
*   [2 Summary of what needs to be done](#Summary_of_what_needs_to_be_done)
*   [3 Kernel configuration](#Kernel_configuration)
    *   [3.1 Kernel command line](#Kernel_command_line)
*   [4 Tools needed](#Tools_needed)
    *   [4.1 kernel build package](#kernel_build_package)
    *   [4.2 DKMS support](#DKMS_support)
*   [5 Modify PKGBUILD](#Modify_PKGBUILD)
    *   [5.1 prepare()](#prepare())
    *   [5.2 _package-headers()](#package-headers())
*   [6 Files required](#Files_required)

## Overview

The Linux kernel distinguishes and keeps separate the verification of modules from requiring or forcing modules to verify before allowing them to be loaded. Kernel modules fall into 2 classes:

*   Standard *in-tree* modules which come with the kernel source code. They are compiled during the normal kernel build.
*   *Out-of-tree* modules which are not part of the kernel source distribution. They are built outside of the kernel tree, requiring the kernel headers package for each kernel they are to be built for. They can be built manually for a specific kernel and packaged, or they can be built whenever needed using [DKMS](/index.php/DKMS "DKMS"). Examples of such packages, provided by Arch, include [virtualbox-guest-modules-arch](https://www.archlinux.org/packages/?name=virtualbox-guest-modules-arch) and [wireguard-arch](https://www.archlinux.org/packages/?name=wireguard-arch).

During a standard kernel compilation, the kernel build tools create a private/public key pair and sign every in-tree module (using the private key). The public key is saved in the kernel itself. When a module is subsequently loaded, the public key can then be used to verify that the module is unchanged.

The kernel can be enabled to always verify modules and report any failures to standard logs. The choice to permit the loading and use of a module which could not be verified can be either compiled into kernel or turned on at runtime using a [kernel parameter](/index.php/Kernel_parameter "Kernel parameter") as explained below.

## Summary of what needs to be done

The starting point is based on a custom kernel package as outlined in [Kernel/Arch Build System](/index.php/Kernel/Arch_Build_System "Kernel/Arch Build System"). We will modify the build to sign the standard in-tree kernel modules and to provide the prerequisites for signing and verifying out-of-tree modules.

**Note:**

The goal is to have:

*   In-tree modules signed during the standard kernel build process. The standard kernel build creates a fresh public/private key pair on each build.
*   Out-of-tree modules are signed and the associated public key is compiled into the kernel. We will create a separate public/private key pair on each build.

Each kernel build needs to made aware of the key pair to be used for signing out-of-tree modules. A kernel configuration parameter is now used to make the kernel aware of additional signing keys: `CONFIG_SYSTEM_TRUSTED_KEYS="/path/to/oot-signing_keys.pem"`.

Keys and signing tools will be stored in the current module build directory. Nothing needs to be done to clean this as removal is handled by the standard module cleanup. The private and public keys are both installed in `/usr/lib/modules/*kernel_version*-*build*/certs-local`.

## Kernel configuration

`CONFIG_SYSTEM_TRUSTED_KEYS` will be updated automatically using the script `fix_config.sh` provided below. In addition, the following configuration options should be set either manually by editing the `.config` file, or via `make menuconfig` in the Linux `src` directory and subsequently copying the updated `.config` file back to the build file `config`.

```
Enable Loadable module suppot --->
Module Signature Verification           -  activate
        CONFIG_MODULE_SIG=y

Require modules to be validly signed -> leave off
        CONFIG_MODULE_SIG_FORCE=n

        This allows the decision to enforce verified modules only as boot command line.
        If you are comfortable all is working then by all means change this to 'y'
        Command line version of this is : module.sig_enforce=1

Automatically sign all modules  - activate
Which hash algorithm    -> SHA-512

Compress modules on installation        - activate
        Compression algorithm (XZ)

Allow loading of modules with missing namespace imports - set to no

```

### Kernel command line

When you have confirmed that the modules are being signed and that the kernel works as it should, you can enable the following [kernel parameter](/index.php/Kernel_parameter "Kernel parameter") to require that the kernel only permits verified modules to be loaded:

```
module.sig_enforce=1

```

Before forcing verified modules on, please confirm that the system logs do not show any module signature failures being reported.

## Tools needed

### kernel build package

In the directory where the kernel package is built:

```
$ mkdir certs-local

```

This directory will provide the tools to create the keys, as well as signing kernel modules.

Put the 4 files into `certs-local`:

*   `fix_config.sh`
*   `x509.oot.genkey`
*   `genkeys.sh`
*   `sign_manual.sh`

The files `genkeys.sh` and its configuration file `x509.oot.genkey` are used to create key pairs.

The file `fix_config.sh` is run after that to provide the kernel with the key information by updating the configuration file used to build the kernel.

The script `sign_manual` will be used to sign out-of-tree kernel modules.

`genkeys.sh` will create the key pairs in a directory named by date-time.

It also creates file `current_key_dir` with that directory name and a soft link `current` to the same directory holding the current key pairs.

These files are all provided below.

### DKMS support

```
$ mkdir certs-local/dkms

```

Add 2 files to the `dkms` directory:

*   `kernel-sign.conf`
*   `kernel-sign.sh`

These will be installed in `/etc/dkms` and provide the means for DKMS to automatically sign modules using the local key. This is the recommended way to sign out-of-tree kernel modules. As explained below, once this is installed, all that is needed is for DKMS to automatically sign modules is to make a soft link for each package to the configuration file.

```
$ cd /etc/dkms
# ln -s kernel-sign.conf *package_name*

```

For example:

```
# ln -s kernel-sign.conf virtualbox

```

The link creation can easily be added to an arch package to simplify further if desired.

## Modify PKGBUILD

We need to make changes to kernel build as follows:

### prepare()

Add the following to the top of the `prepare()` function:

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

Add the following to the bottom of the `_package-headers()` function:

```
_package-headers() {

    ...

    #
    # Out-of-tree module signing
    # This is run in the kernel source / build directory
    #
    msg2 "Local Signing certs for out-of-tree modules..."

    certs_local_src="../../certs-local" 
    key_dir=$(<${certs_local_src}/current_key_dir)

    certs_local_dst="${builddir}/certs-local"
    signer="sign_manual.sh"
    mkdir -p ${certs_local_dst}
    rsync -a $certs_local_src/{current,$key_dir,$signer} $certs_local_dst/

    # DKMS tools
    dkms_src="$certs_local_src/dkms"
    dkms_dst="${pkgdir}/etc/dkms"
    mkdir -p $dkms_dst

    rsync -a $dkms_src/{kernel-sign.conf,kernel-sign.sh} $dkms_dst/
}
```

## Files required

The 6 supporting files referenced above are available for download from the [github.com/gene-git/Arch-SKM](https://github.com/gene-git/Arch-SKM/tree/master) repository:

*   [certs-local/fix_config.sh](https://github.com/gene-git/Arch-SKM/blob/master/certs-local/fix_config.sh)
*   [certs-local/x509.oot.genkey](https://github.com/gene-git/Arch-SKM/blob/master/certs-local/x509.oot.genkey)
*   [certs-local/genkeys.sh](https://github.com/gene-git/Arch-SKM/blob/master/certs-local/genkeys.sh)
*   [certs-local/sign_manual.sh](https://github.com/gene-git/Arch-SKM/blob/master/certs-local/sign_manual.sh)
*   [certs-local/dkms/kernel-sign.conf](https://github.com/gene-git/Arch-SKM/blob/master/certs-local/dkms/kernel-sign.conf)
*   [certs-local/dkms/kernel-sign.sh](https://github.com/gene-git/Arch-SKM/blob/master/certs-local/dkms/kernel-sign.sh)

Remember to ensure that the scripts are [executable](/index.php/Executable "Executable").