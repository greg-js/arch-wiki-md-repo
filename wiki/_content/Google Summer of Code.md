# Google Summer of Code

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

The Arch Linux development team is considering to participate this year in [Google Summer of Code (GSoC)](http://www.google-melange.com/gsoc/homepage/google/gsoc2012), here is a draft on what areas we are needing improvements.

The deadline to apply to mentor students is Friday, 9 March at 23:00 GMT. Google will begin accepting student applications on 26 March.

Discussion on dev-public mailing list: [Google Summer of Code](http://thread.gmane.org/gmane.linux.arch.devel/17159)

The main idea here is to help the development of these tools, improving it, making patches and fixing bugs for now.

**Arch Linux has its own projects; please read the entire article before thinking that we are just asking for packagers.**

### Project Ideas

*   AIF (Arch Linux Installation Framework)
    *   grub2 option: Provide grub2 as a bootloader to install.
    *   GPT/gdisk: Support gpt disk layouts for automatic and manual disk preperation.
    *   systemd: Add an option to choose between initscripts and systemd.
    *   complete rewrite (in python)?
        *   +1 for python, but the python package is ~80MB and current netinstall iso is ~200MB -> too fat?
*   [netcfg](/index.php/Netcfg "Netcfg")
*   automatic package buildfarm
    *   There has been some work on [Arch integration into openbuildservice.org](http://www.google-melange.com/gsoc/project/google/gsoc2011/madgnu/13001) - [[1]](http://lists.opensuse.org/opensuse-buildservice/2011-08/msg00179.html)
*   single authentication database and managing our packaging ssh accounts from archweb
*   Implement pkgstats submission and graph/stats creation in archweb

#### Pacman-related Ideas

*   coming soon
*   see the [Pacman Roadmap](/index.php/Pacman_Roadmap "Pacman Roadmap") for details

### Potential Mentors

*   Pacman mentor (Dan?)
*   AIF mentor (Dieter?)
*   pkgstats (Pierre; no idea about django though)
*   Netcfg (?)

Retrieved from "[https://wiki.archlinux.org/index.php?title=Google_Summer_of_Code&oldid=381003](https://wiki.archlinux.org/index.php?title=Google_Summer_of_Code&oldid=381003)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [Arch development](/index.php/Category:Arch_development "Category:Arch development")