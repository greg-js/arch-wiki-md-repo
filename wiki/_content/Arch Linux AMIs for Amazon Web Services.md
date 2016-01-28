# Arch Linux AMIs for Amazon Web Services

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

[![Tango-dialog-warning.png](/images/d/d8/Tango-dialog-warning.png)](/index.php/File:Tango-dialog-warning.png)

[![Tango-dialog-warning.png](/images/d/d8/Tango-dialog-warning.png)](/index.php/File:Tango-dialog-warning.png)

**This article or section is out of date.**

**Reason:** Links still work, but information from 2012 (Discuss in [Talk:Arch Linux AMIs for Amazon Web Services#](https://wiki.archlinux.org/index.php/Talk:Arch_Linux_AMIs_for_Amazon_Web_Services))

[![Tango-two-arrows.png](/images/7/72/Tango-two-arrows.png)](/index.php/File:Tango-two-arrows.png)

[![Tango-two-arrows.png](/images/7/72/Tango-two-arrows.png)](/index.php/File:Tango-two-arrows.png)

**This article or section is a candidate for merging with [VPS](/index.php/VPS "VPS").**

**Notes:** please use the second argument of the template to provide more detailed indications. (Discuss in [Talk:Arch Linux AMIs for Amazon Web Services#](https://wiki.archlinux.org/index.php/Talk:Arch_Linux_AMIs_for_Amazon_Web_Services))

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

These were updated as of 2012-10-19.

*   ami-6ee95107 = US East (N. Virginia)
*   ami-bcf77e8c = US West (Oregon)
*   ami-337d5b76 = US West (N. California)
*   ami-17595a63 = EU (Ireland)
*   ami-6af9b938 = Asia Pacific (Singapore)
*   ami-8cad138d = Asia Pacific (Tokyo)
*   ami-6259807f = South America (Sao Paulo)

### Other AMIs

Verified working public arch liunx AMIs are below

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

[linux-ec2](https://aur.archlinux.org/packages/linux-ec2/)<sup><small>AUR</small></sup> in [AUR](/index.php/AUR "AUR") compiles the Arch linux kernel for AWS with Xen modules enabled and the XSAVE patch applied.

Retrieved from "[https://wiki.archlinux.org/index.php?title=Arch_Linux_AMIs_for_Amazon_Web_Services&oldid=393507](https://wiki.archlinux.org/index.php?title=Arch_Linux_AMIs_for_Amazon_Web_Services&oldid=393507)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [Getting and installing Arch](/index.php/Category:Getting_and_installing_Arch "Category:Getting and installing Arch")

Hidden categories:

*   [Pages or sections flagged with Template:Out of date](/index.php/Category:Pages_or_sections_flagged_with_Template:Out_of_date "Category:Pages or sections flagged with Template:Out of date")
*   [Pages or sections flagged with Template:Merge](/index.php/Category:Pages_or_sections_flagged_with_Template:Merge "Category:Pages or sections flagged with Template:Merge")