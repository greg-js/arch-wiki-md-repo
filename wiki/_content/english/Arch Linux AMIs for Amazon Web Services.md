## Public community Arch AMIs

**Note:** Arch Linux currently does not offer official AMIs. The AMIs listed here are created by the community.

### AMI Images from Uplink Labs

Uplink Labs creates new images approximately twice a month. Images are being built for a number of regions, and cover the following configurations:

*   ebs hvm x86_64 lts
*   s3 hvm x86_64 lts
*   ebs hvm x86_64 stable
*   s3 hvm x86_64 stable

AMI links and more information are available at [https://www.uplinklabs.net/projects/arch-linux-on-ec2/](https://www.uplinklabs.net/projects/arch-linux-on-ec2/) .

## Building Arch AMIs

You can also build your own Arch Linux AMIs.

[linux-ec2](https://aur.archlinux.org/packages/linux-ec2/) in [AUR](/index.php/AUR "AUR") compiles the Arch linux kernel for AWS with Xen modules enabled and the XSAVE patch applied. Note that at least some instance types will also work with the stock Arch Linux kernel.

Aforementioned [Uplink Labs webpage](https://www.uplinklabs.net/projects/arch-linux-on-ec2/) also has a manual on the build process.

Another tutorial on building your own AMIs can be found at [https://gitlab.com/bitfehler/archlinux-ec2](https://gitlab.com/bitfehler/archlinux-ec2)