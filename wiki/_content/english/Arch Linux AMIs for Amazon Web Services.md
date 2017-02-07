## Contents

*   [1 Running public Arch AMIs](#Running_public_Arch_AMIs)
    *   [1.1 AMI Images from Uplink Labs](#AMI_Images_from_Uplink_Labs)
    *   [1.2 Archlinux AMI](#Archlinux_AMI)
    *   [1.3 Other AMIs](#Other_AMIs)
*   [2 Building Arch AMIs](#Building_Arch_AMIs)

## Running public Arch AMIs

### AMI Images from Uplink Labs

Uplink Labs creates new images approximately twice a month, for a number of regions:

[http://www.uplinklabs.net/projects/arch-linux-on-ec2/](http://www.uplinklabs.net/projects/arch-linux-on-ec2/)

### Archlinux AMI

current releases: **Release 2017.01.15**

*   ebs hvm x86_64 lts
*   s3 hvm x86_64 lts
*   ebs hvm x86_64 stable
*   s3 hvm x86_64 stable

for update list: [https://www.uplinklabs.net/projects/arch-linux-on-ec2/](https://www.uplinklabs.net/projects/arch-linux-on-ec2/)

### Other AMIs

Verified working public arch linux AMIs are below

```
AMI          Store Build   Release     Kernel Last verified
ami-07be766e  EBS  64 bit  2011-04-15  3.0+   2012-01-14    
ami-19be7670  EBS  64 bit  2011-11-18  3.0+   2012-01-14    
ami-26e8144f  EBS  32 bit  2011-04-15  2.6    2012-01-14    
ami-38e81451  EBS  32 bit  2011-04-15  2.6    2012-01-14    

```

These AMIs ship with Arch linux kernels that are booted by PV-GRUB.

(2012-01-14) The 64 bit AMIs consistently failed to boot on Micro instances in us-east-1a and us-east-1d. In us-east-1b and us-east-1c the AMIs occasionally fail to boot. Stop and start the instance to reassign it a random machine in these cases.

This may be an issue with Amazon running different versions of Xen on different machines / older availability zones.

## Building Arch AMIs

[linux-ec2](https://aur.archlinux.org/packages/linux-ec2/) in [AUR](/index.php/AUR "AUR") compiles the Arch linux kernel for AWS with Xen modules enabled and the XSAVE patch applied.