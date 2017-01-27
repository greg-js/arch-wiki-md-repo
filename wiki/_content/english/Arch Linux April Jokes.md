Every first day of April, the Arch Linux website traditionally features an [April Fools' Day](https://en.wikipedia.org/wiki/April_Fools%27_Day "wikipedia:April Fools' Day") joke on the front page. This document collects the jokes as a fun reading for readers of this Wiki.

## Contents

*   [1 2016](#2016)
*   [2 2015](#2015)
*   [3 2014](#2014)
*   [4 2013: Pacman depends on systemd](#2013:_Pacman_depends_on_systemd)
*   [5 2012](#2012)
*   [6 2011: Canterbury](#2011:_Canterbury)
    *   [6.1 History](#History)
    *   [6.2 Goal](#Goal)
    *   [6.3 Features](#Features)
*   [7 2010: April Fools Challenge](#2010:_April_Fools_Challenge)
    *   [7.1 About the april fools challenge joke](#About_the_april_fools_challenge_joke)
*   [8 2009: Dropping i686 Support](#2009:_Dropping_i686_Support)
    *   [8.1 About the dropping i686 support joke](#About_the_dropping_i686_support_joke)
    *   [8.2 After-action Report](#After-action_Report)
    *   [8.3 Actual end of support](#Actual_end_of_support)
*   [9 2008: Arch in German](#2008:_Arch_in_German)
    *   [9.1 About the German Arch joke](#About_the_German_Arch_joke)
*   [10 2007: Arch Ark](#2007:_Arch_Ark)
    *   [10.1 Ark Linux](#Ark_Linux)
*   [11 2006: Judd goes to Google](#2006:_Judd_goes_to_Google)
    *   [11.1 Judd's actual goodbye to Arch project](#Judd.27s_actual_goodbye_to_Arch_project)
    *   [11.2 Arch Linux and its release system](#Arch_Linux_and_its_release_system)
*   [12 2005: Arch against Wombats](#2005:_Arch_against_Wombats)
    *   [12.1 Wombats](#Wombats)
*   [13 2004: GNOME 2.6](#2004:_GNOME_2.6)
    *   [13.1 GNOME version history](#GNOME_version_history)

## 2016

There does not seem to have been an April Fools' Day joke for 2016.

## 2015

There does not seem to have been an April Fools' Day joke for 2015.

## 2014

There does not seem to have been an April Fools' Day joke for 2014\. [[1]](https://bbs.archlinux.org/viewtopic.php?id=179466)

## 2013: Pacman depends on systemd

**published:** 2013 / **permalink:** [Pacman 4.1 released](http://allanmcrae.com/2013/04/pacman-4-1-released/)

The major feature for the release is tight integration between the package manager and systemd. After much discussion about how best to perform updates on a rolling release system, we realized that it was essential to have updates preformed with minimal other processes running. Also, the security aspects of updates mean that it is essential that these get provided as soon as possible. We felt the best way to achieve this was to perform updates on shutdown. This is achieved through a new daemon, pacmand that monitors and downloads updates in the background. When updates are found, it schedules a reboot of the system (hence the need to integrate systemd). At the moment the timing of the reboots is not configurable, but a timer will pop-up to allow you to delay it for a preset amount of time. Configuration will likely be added in pacman-4.2, when pacmanctl will be ready for general use. Until that release is made, Arch Linux will minimize the impact by performing all updates in its [testing] repository and only push updates on a yet to be decided day and time of the week. A news post will be made when that is decided.

Of course, all this makes systemd a hard dependency of pacman. We felt this was acceptable given Arch Linux has officially switched to using systemd. As this release is not tested (and unlikely to work) on systems without systemd, Arch users or other distributions using pacman will be required to make the switch to systemd if they want to continue using pacman as their package manager. The integration with system will become tighter in pacman-4.2 where we plan to use the upcoming kdbus message passing interface – through libsystemd-bus – to allow other programs to interact with pacman, making the development of alternative front-ends easier.

## 2012

There does not seem to have been an April Fools' Day joke for 2012.

## 2011: Canterbury

**published:** 2011 / **permalink:** [Arch news archive #519](https://www.archlinux.org/news/519/)

### History

At the [FOSDEM 2011 Distribution collaboration event](http://www.fosdem.org/2011/schedule/event/distro_collaboration) the lead developers of Archlinux and Debian discussed the idea of combining the best features of their projects and work together to produce a new, superior distribution. This concept was first raised at an earlier openSUSE conference and they believe there is potential to work together, combining their efforts.

A week later, Feb 16, the [Linux Standard Base](http://www.linuxfoundation.org/collaborate/workgroups/lsb) version [4.1](http://www.linuxfoundation.org/collaborate/workgroups/lsb/lsb-41) was released. With a new standard base to work on, a unified distribution became a hot topic again; Gentoo and Grml got on board.

Dieter, the mastermind behind the dual ISO/usb-IMG installer file has already started working on the new installer discussion is underway, working out they will take care of further merging of the harder parts, such as infrastructure and system tools.

### Goal

The target is to produce a really unified effort and be able to stand up in a combined effort against proprietary operating systems, to show off that the Free Software community is actually able to work together for a common goal instead of creating more diversity.

### Features

The Canterbury distribution will combine the best of the linux world to another game changer for the good of the users:

*   Simple as Arch - technologically simple and bleeding edge.
*   Stable as Debian - highly dependable.
*   Malleable as Gentoo - you get what you really want.
*   Live as Grml - readily usable.
*   Openminded as openSUSE - broad and welcoming for everyone.

## 2010: April Fools Challenge

**published:** 2010 / **permalink:** [Arch news archive #492](https://www.archlinux.org/news/492/)

It is that time of year again, but this year we are being super subtle. In fact so subtle, many of you will not notice the April Fools at all. But there is definitely one there. Post your guesses in this dedicated forum thread. We have a donated netbook to give away as a prize for the first person who fully uncovers the joke.

### About the april fools challenge joke

**Arch Forum:** [April Fools Challenge](https://bbs.archlinux.org/viewtopic.php?id=94255)

Page 01: "it's all about recursion."

Page 15: "We're almost half way through April, why on earth is this thread still active?"

Page 16: "I'll add a 'move along, nothing to see here' just so people can be absolutely sure..."

Page 16: "Noting to see here???? There are 386 replies and 49,275 views!!! ....... Trapped in The Matrix."

## 2009: Dropping i686 Support

**published:** 2009 / **permalink:** [Arch news archive #440](https://www.archlinux.org/news/440/)

Recently the developers have been discussing the possibility of adding some additional optimizations to our i686 port to improve multimedia support. This would involve reducing the compatibility with older systems. As some of you may have heard ([1], Google translation [2]), this discussion has resulted in the decision to focus exclusively on the x86_64 port. The overall opinion of the developers is that the x86_64 port is now complete enough to justify this decision and that this is in keeping with Arch's philosophy of supporting current generation hardware. The x86_64 architecture has been available since 2002 (compared to i686 which is from 1995), and we believe most of our i686 users have x86_64 compatible hardware.

An official time-line for the deprecation of the i686 port has not been established, but an official announcement needs to be made, as the decision has already been leaked to the ArchLinux-BR community. However, it is likely that major updates (GNOME, KDE, Xorg, etc) will not be built for i686 in the immediate future. Users will still be able to build packages for i686 packages using ABS. As most of the architecture specific patches are for x86_64, this should be relatively pain free.

### About the dropping i686 support joke

On April 1st, 2009, it was announced on the frontpage, as well as the Arch-Dev-Public mailing list that Arch would be dropping support for the i686 architecture. This announcement spurred a number of heated debates across the forums, mailing lists, and on IRC. Among other things, the debates led Aaron to threaten to leave Arch. Similar to previous years, various phrases on the forums and other Arch sites were filtered to make life more entertaining.

### After-action Report

**published:** 2009 / **permalink:** [Arch news archive #441](https://www.archlinux.org/news/441/)

Hi, Arch Linux users, we are pleased to inform you that the i686 architecture is not going to be dropped from Arch Linux. It all was part of an April Fools joke, in which all the developers and the forum moderators played a big part.

Interestingly, this joke actually did some good. Some of our users discovered that they were, in fact, running 64-bit processors, and many of them switched to the Arch Linux 64-bit version. We encourage anyone who already switched to keep using the 64-bit version, to continue contributing to the architecture and encourage support from other major software vendors.

A prime example of a vendor giving in to the demands of the 64-bit community is Adobe. They've recently added 64-bit Linux support to the flash plug-in, for which we thank them.

Sorry for any inconvenience this joke may have caused, but how can we resist a prank on the 1st of April?

### Actual end of support

On 2017-01-25 it was [announced](https://www.archlinux.org/news/phasing-out-i686-support/) that support for the i686 architecture would be actually phased out due to its decreasing popularity among the developers and the community.

## 2008: Arch in German

**published:** 2008 / **permalink:** n/a

Important Notice for English Archers

Over the past two months, great discussion has passed on the private development list, and we have come to the conclusion that keeping Arch as a primarily English distro is a disservice to our largest user-base. As such, we have decided in majority vote to change the official, primary language of Arch Linux to German.

Please bear with us during this transition - we are working closely with archlinux.de to facilitate the switch, at which point we plan to merge the websites. Knowing the great community behind Arch, we are sure a community project will arise quickly to fill the small void left when we completely discontinue the English site.

Also, please note we're now using the German pronunciation for "Arch". Don't worry, you'll get used to it - 90% of our devs already are!

Happy Computenpeepers, The Management

### About the German Arch joke

On April 1st, 2008, most of Arch Linux websites (including the BBS) were translated to German. The above notice appeared on most of them, and the BBS rewrote strings posted by users so that references to the Wiki articles all pointed to a page called "Deutchland", and words like "joke" were rewritten as "genius idea". For example: "Arch Linux April Jokes Collection" would read "Arch Linux Deutschland genius idea Collection".

## 2007: Arch Ark

**published:** 2007 / **permalink:** [Arch news archive #307](https://www.archlinux.org/news/307/)

We're changing our name!

After 5 years of being called Arch Linux and 5 years of people confusing us with Ark Linux, we've finally come up with a solution. We've spent the last few months talking to the Ark Linux people to come up with a solution that's beneficial for both distributions. Today, we are happy to announce a name change for Arch Linux. Today, I am happy to announce, we will be known as Ark Linux!

We will keep our domain archlinux.org for the next few weeks, while people are still getting used to the name change, but eventually we will switch domains as well. In changing names, we are sure that people will never again have problems discerning Arch Linux with Ark Linux.

Long Live Ark Linux!

### Ark Linux

Ark Linux was an actual Linux distribution (since discontinued [[2]](http://distrowatch.com/table.php?distribution=ark)). The above joke is especially funny to those Archers who started using Arch after mistakingly typing "www.archlinux.org" instead of "www.arklinux.org". The "Arch Linux" name is considered to be pronounced as /a-ch/ (rhymes with larch, starch, as in "archer"). However, there does not seem to exist a consensus on how it is really pronounced.[[3]](https://bbs.archlinux.org/viewtopic.php?id=4901&p=2)

The same joke was also posted on Ark Linux to make it even more convincing (at the first glance, at least; sadly, there does not seem to be an archive of Ark Linux news).

## 2006: Judd goes to Google

**published:** 2006 / **permalink:** [Arch news archive #214](https://www.archlinux.org/news/214/)

Current Changes

I just thought I would bring you all up to speed on some of the information currently going around the watercooler.

Judd has officially accepted a job offer from Google, and as such, will be unable to continue with his Archlinux work.

Lead of the project has moved to the capable hands of Jason Chu (Xentac). Jason's first order of business, as we push towards the 0.7.1.1 release (Codename: Pony), will be creating a [stable] repository, with older software. This will be the main focus of our work from now on, with all the security backports and compatability fixes. As such, the normal repos will begin to lack a bit, but those will be removed in time as we move to a more 'stable' and 'production quality' release system.

Expect 0.7.1.1 in a few weeks.

Thanks, Aaron

### Judd's actual goodbye to Arch project

Judd Vinet, the founder of Arch Linux, has actually left the project on the 1st of October, 2007, and became the "Arch's Number One Cheerleader".[[4]](https://www.archlinux.org/news/350/) Since then, Aaron Griffin is the project leader.

### Arch Linux and its release system

Arch Linux does not use the *stable* and *production quality* release system. It is a [rolling release](https://en.wikipedia.org/wiki/Rolling_release "wikipedia:Rolling release") system, where the system is constantly kept up-to-date with no fixed release schedules.

## 2005: Arch against Wombats

**published:** 2005 / **permalink:** [Arch news archive #147](https://www.archlinux.org/news/147/)

CETW Problems

It is with great sadness that I write this message.

When we first released Arch Linux 0.7 (Wombat) we were contacted by the Centre for Ethical Treatment of Wombats (CETW). CETW felt that we were somehow hurting wombats worldwide by releasing an "open source project" with the codename Wombat. While we tried to convince them that Arch Linux was a Linux distribution and that no wombats were harmed during the creation of our release, they wouldn't accept it.

So they threatened to sue us unless we changed our destructive ways.

After much deliberation, we have figured out that we do not actually have enough money to fight them in court. Instead we have chosen to settle outside of court. Part of our settlement is to discontinue the development of Arch Linux.

And thus, through a poor choice of naming, Arch Linux is no more. All of the developers would like to thank the community for their support and contributions.

### Wombats

"Wombats are Australian marsupials; they are short-legged, muscular quadrupeds, approximately one metre (39 inches) in length with a very short tail. They are found in forested, mountainous, and heathland areas of south-eastern Australia and Tasmania. The name wombat comes from the Eora Aboriginal community who were the original inhabitants of the Sydney area." [wikipedia:Wombat](https://en.wikipedia.org/wiki/Wombat "wikipedia:Wombat")

Wombats are not known to hire lawyers to harass Linux distributions.[wikipedia:Wombat#Wombats and humans](https://en.wikipedia.org/wiki/Wombat#Wombats_and_humans "wikipedia:Wombat")

## 2004: GNOME 2.6

**published:** 2004 / **permalink:** [Arch news archive #58](https://www.archlinux.org/news/58/)

GNOME 2.6 Released!

As the title says, gnome 2.6 is in the house. There isn't much to watch out for, Arjan and JGC did a good job catching conflicts in the testing stage so the install should go flawlessly.

To upgrade: pacman -Syu To install: pacman -S gnome

Some GTK 2.x related packages were also upgraded to suit the requirements of gnome 2.6.

### GNOME version history

Before the above *news* was posted, the GNOME project had released 2.0 in 2002, and latest release before the 1st of April 2004 was GNOME 2.2.[[5]](http://www.greaterbostonrubyandrails.com/Release.html)