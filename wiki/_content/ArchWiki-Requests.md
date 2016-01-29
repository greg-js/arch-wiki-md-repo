# ArchWiki:Requests

Is the wiki missing documentation for a popular software package or coverage of an important topic? Or, is existing content in need of correction, updating, or expansion? Write your requests below and share your ideas...

See [ArchWiki:Reports](/index.php/ArchWiki:Reports "ArchWiki:Reports") to report questionable contributions. Please sign your edits and feel free to comment on others' requests.

## Contents

*   [1 General requests](#General_requests)
    *   [1.1 Problem redirects](#Problem_redirects)
    *   [1.2 Broken package links](#Broken_package_links)
*   [2 Creation requests](#Creation_requests)
    *   [2.1 HOWTO: SAMBA PDC + LDAP](#HOWTO:_SAMBA_PDC_.2B_LDAP)
    *   [2.2 Left-Handed Adjustments for Desktop Environments](#Left-Handed_Adjustments_for_Desktop_Environments)
    *   [2.3 Input methods](#Input_methods)
    *   [2.4 DRI](#DRI)
    *   [2.5 ldns](#ldns)
    *   [2.6 Perl](#Perl)
    *   [2.7 Linux console](#Linux_console)
    *   [2.8 Sublime-text](#Sublime-text)
    *   [2.9 Forum link](#Forum_link)
*   [3 Modification requests](#Modification_requests)
    *   [3.1 Automatic loading of kernel modules](#Automatic_loading_of_kernel_modules)
    *   [3.2 Links to Gentoo wiki](#Links_to_Gentoo_wiki)
    *   [3.3 Should we remove or archive obsolete articles?](#Should_we_remove_or_archive_obsolete_articles.3F)
        *   [3.3.1 List of suggested solutions](#List_of_suggested_solutions)
        *   [3.3.2 Enforcement](#Enforcement)
            *   [3.3.2.1 Restoring revisions and redirection](#Restoring_revisions_and_redirection)
            *   [3.3.2.2 Separation of archive content](#Separation_of_archive_content)
            *   [3.3.2.3 Double redirects](#Double_redirects)
            *   [3.3.2.4 Rename Template:Deletion](#Rename_Template:Deletion)
    *   [3.4 Broken redirects](#Broken_redirects)
    *   [3.5 Hide irrelevant pages in search suggestions](#Hide_irrelevant_pages_in_search_suggestions)
    *   [3.6 Article guideline](#Article_guideline)
        *   [3.6.1 Contributing](#Contributing)
    *   [3.7 TrackPoint](#TrackPoint)
    *   [3.8 Renamed software](#Renamed_software)
        *   [3.8.1 Nautilus got renamed to Gnome Files](#Nautilus_got_renamed_to_Gnome_Files)
            *   [3.8.1.1 List](#List)
        *   [3.8.2 XBMC renamed to Kodi](#XBMC_renamed_to_Kodi)
        *   [3.8.3 Gummiboot](#Gummiboot)
    *   [3.9 Cleanup: links to non-existent packages](#Cleanup:_links_to_non-existent_packages)
        *   [3.9.1 Surrounding link text](#Surrounding_link_text)
    *   [3.10 Strategy for updating package templates](#Strategy_for_updating_package_templates)
    *   [3.11 index.php in url address](#index.php_in_url_address)
    *   [3.12 Change drive naming/accessing to UUID?](#Change_drive_naming.2Faccessing_to_UUID.3F)
    *   [3.13 User and group pacnew files](#User_and_group_pacnew_files)
    *   [3.14 FAQ](#FAQ)
*   [4 Bot requests](#Bot_requests)

## General requests

NaN

Also note that [Special:WantedCategories](/index.php/Special:WantedCategories "Special:WantedCategories") can show additional automatic [tracking categories](https://www.mediawiki.org/wiki/Help:Tracking_categories "mw:Help:Tracking categories").

### Problem redirects

**Note:** Redirects should not point to other sites and ones that do sometimes erroneously show up on these pages.

*   [Special:BrokenRedirects](/index.php/Special:BrokenRedirects "Special:BrokenRedirects")
*   [Special:DoubleRedirects](/index.php/Special:DoubleRedirects "Special:DoubleRedirects")

### Broken package links

[![Tango-view-fullscreen.png](/images/3/38/Tango-view-fullscreen.png)](/index.php/File:Tango-view-fullscreen.png)

[![Tango-view-fullscreen.png](/images/3/38/Tango-view-fullscreen.png)](/index.php/File:Tango-view-fullscreen.png)

**This article or section needs expansion.**

**Reason:** Add documentation for all the hints: meaning + recommended action (Discuss in [ArchWiki:Requests#Strategy for updating package templates](https://wiki.archlinux.org/index.php/ArchWiki:Requests#Strategy_for_updating_package_templates))

ArchWiki contains many broken links to packages not found either in [official repositories](/index.php/Official_repositories "Official repositories") or [AUR](/index.php/AUR "AUR"), which is the result of packages being merged, split or removed from the repositories. All pages in the main namespace are regularly checked by a bot, which checks all instances of [AUR](/index.php/Template:AUR "Template:AUR"), [Grp](/index.php/Template:Grp "Template:Grp") and [Pkg](/index.php/Template:Pkg "Template:Pkg") templates, tries to automatically update them and marks them with [Template:Broken package link](/index.php/Template:Broken_package_link "Template:Broken package link") when it is not possible to update them automatically.

To fix a broken package link, do **not** simply remove the reference to the packages from the wiki, do some research first:

*   Search the package database (`pacman -Ss`) and [AUR](https://aur.archlinux.org/packages/), it is possible that the package was merged/renamed.
*   If looking for a specific file, for example a binary that was part of the package, [pkgfile](/index.php/Pkgfile "Pkgfile") might do the trick.
*   If unsure, mark the page or section with an appropriate [status template](/index.php/Help:Template#Article_status_templates "Help:Template") rather than completely removing the reference to the package.
*   For AUR3 package links marked with [Template:Aur-mirror](/index.php/Template:Aur-mirror "Template:Aur-mirror"), you may consider resubmitting them to the AUR if interested in maintaining them.

All pages with broken package links are tracked in [Category:Pages with broken package links](/index.php/Category:Pages_with_broken_package_links "Category:Pages with broken package links").

## Creation requests

_Here, list requests for topics that you think should be covered on ArchWiki. If not obvious, explain why ArchWiki coverage is justified (rather than existing Wikipedia articles or other documentation). Furthermore, please consider researching and creating the initial article yourself (see [Help:Editing](/index.php/Help:Editing "Help:Editing") for content creation help)._

### HOWTO: SAMBA PDC + LDAP

How to configure SAMBA PDC + LDAP in Arch Linux? (Moved from another page. [Hokstein](/index.php?title=User:Hokstein&action=edit&redlink=1 "User:Hokstein (page does not exist)") 19:57, 16 September 2007 (EDT))

### Left-Handed Adjustments for Desktop Environments

I was thinking it would be helpful for lefties if there were a list of configuration options for each desktop environment that facilitate left-handed use of mice and touchpads. I'm not sure if this is related enough to Arch to include in this wiki, but I haven't had a lot of luck finding information for my own DE (KDE) let alone for others. I will start writing down information, and if no one else thinks there should be a separate page for this, I'll just add the information I find to each individual DE's page. —[ajrl](/index.php/User:Ajrl "User:Ajrl") 2013-08-11T15:09−06:00

NaN

### Input methods

Currently there is no page on ArchWiki properly describing various input methods _generally_. There is only [Internationalization#Input_methods_in_Xorg](/index.php/Internationalization#Input_methods_in_Xorg "Internationalization"), but it has several problems:

*   missing descriptions
*   [X compose key](/index.php/Keyboard_configuration_in_Xorg#Configuring_compose_key "Keyboard configuration in Xorg") does not fit in
*   GTK has a default "simple" input method featuring the `Ctrl+Shift+u` shortcut for entering a unicode character (this was added recently into a wrong article: [[1]](https://wiki.archlinux.org/index.php?title=Bash&diff=289079&oldid=287436)) - again, no description
*   no description of XIM - outdated, but sometimes used as fallback?

So this is quite enough material to start a new great article ;)

-- [Lahwaacz](/index.php/User:Lahwaacz "User:Lahwaacz") ([talk](/index.php/User_talk:Lahwaacz "User talk:Lahwaacz")) 18:23, 18 December 2013 (UTC)

NaN

### DRI

An article, or even stub that links to resources, explaining what DRI is, why it's important, differences between DRI 1, 2, 3, how DRI1 is no longer supported as of xorg-server 1.13, simple xorg.conf code explaining the DRI section, enabling the composite and render extensions there, these and more. Just my thoughts.

### ldns

ldns is a core package with no wiki documentation. It is also relatively new in the world of DNS tools and is not well covered on the Internet. Documentation of basic features and what it is not (eg a replacement for bind) would provide a valueable resource. [MichaelRpdx](/index.php/User:MichaelRpdx "User:MichaelRpdx") ([talk](/index.php?title=User_talk:MichaelRpdx&action=edit&redlink=1 "User talk:MichaelRpdx (page does not exist)")) 20:07, 17 February 2014 (UTC)

NaN

### Perl

Surprisingly, there is no wiki page describing the installation and configuration of Perl, unlike Python, Ruby etc. Could include the installation of CPAN modules and a list of good tutorials for beginners, too. So far there is only guides for packaging Perl and its modules ([Perl Policy](/index.php/Perl_Policy "Perl Policy") and [Perl package guidelines](/index.php/Perl_package_guidelines "Perl package guidelines") respectively) -- [bluestreak0](/index.php?title=User:Bluestreak0&action=edit&redlink=1 "User:Bluestreak0 (page does not exist)") 01:32, 17 April 2014 (UTC)

### Linux console

I was thinking that a new page for the console would be a good idea. The [Wikipedia:Linux console](https://en.wikipedia.org/wiki/Linux_console "wikipedia:Linux console") article gives a short general overview, but obviously doesn't concern the configuration. Since it's an independent system, configured separately from any graphical environment, it would bring together several related sections across multiple articles in one place. It's a fairly complex system and difficult to cover in any depth in small sections across other articles (such as [Fonts](/index.php/Fonts "Fonts")). I've put together a basic example, [User:Teppic74/Linux_console](/index.php/User:Teppic74/Linux_console "User:Teppic74/Linux console"). -- [Teppic74](/index.php/User:Teppic74 "User:Teppic74") ([talk](/index.php/User_talk:Teppic74 "User talk:Teppic74")) 17:11, 3 July 2014 (UTC)

NaN

NaN

### Sublime-text

I think creating a page and mentioning ways to improve sublime-text integration with Gnome would be a good idea. The trick is if you run sublime with _--class=<filename of sublime text .desktop file, e.g. sublime_text_3>_, it would help Gnome and XFCE to group sublime instances with its respective desktop file. This is mentioned in the comments of the aur package but I think it's better that this would be in the wiki.--[183.amir](/index.php?title=User:183.amir&action=edit&redlink=1 "User:183.amir (page does not exist)") ([talk](/index.php?title=User_talk:183.amir&action=edit&redlink=1 "User talk:183.amir (page does not exist)")) 12:41, 19 December 2014 (UTC)

### Forum link

NaN

The article has two types of forum links:

*   [BBS#30155](https://bbs.archlinux.org/viewtopic.php?id=30155) (intro, as in [Template:Bug](/index.php/Template:Bug "Template:Bug")) and
*   [https://bbs.archlinux.org/viewtopic.php?id=101010](https://bbs.archlinux.org/viewtopic.php?id=101010) (section [#Kingbash](/index.php/Bash/Functions#Kingbash "Bash/Functions"))

Which one is right again? --**[Det](/index.php/User:Det "User:Det")[<sup><font color="white">talk</font></sup>](/index.php/User_talk:Det "User talk:Det")** 11:44, 24 July 2015 (UTC)

NaN

NaN

NaN

NaN

NaN

NaN

NaN

NaN

## Modification requests

_Here, list requests for correction or other modification of existing articles. Only systemic modifications that affect multiple articles should be included here. If a specific page needs modification, use that page's_ discussion _or_ talk _page instead and one of the [#General requests](#General_requests) templates._

As a rolling release, Arch is constantly receiving updates and improvements. Because of this the Arch wiki must be updated quickly to reflect these changes.

### Automatic loading of kernel modules

There are notes like "Since kernel 3.4 all necessary modules are loaded automatically" and "Newer versions of udev load the module automatically", which are usually followed by rather long section "If that does not work, do `modprobe _foo_`" and "To make it permanent after reboot, add the following to `/etc/modules-load.d/_module.conf_`".

Examples: [Kernel_modules#Configuration](/index.php/Kernel_modules#Configuration "Kernel modules"), [CPU frequency scaling](/index.php/CPU_frequency_scaling "CPU frequency scaling"), [CPU frequency scaling#CPU_frequency_driver](/index.php/CPU_frequency_scaling#CPU_frequency_driver "CPU frequency scaling"), [Network configuration#Check_the_driver_status](/index.php/Network_configuration#Check_the_driver_status "Network configuration"), [Wireless_Setup#Device_driver](/index.php/Wireless_Setup#Device_driver "Wireless Setup").

There are several problems with this, so quick list of tasks:

*   ~~Verify kernel and udev version, because this also depends on the resolution of [ArchWiki_talk:Reports#Minimum_supported_kernel_version](/index.php/ArchWiki_talk:Reports#Minimum_supported_kernel_version "ArchWiki talk:Reports").~~
*   Perhaps the notes should be unified (though autoloading on hotplug and when some command is executed are different). Also note that some notes mentioning _udev_ might be inaccurate and need to be changed to mention _kernel_ (and vice versa).
*   Replace verbose `modprobe` fallback commands with link to [Kernel modules#Loading](/index.php/Kernel_modules#Loading "Kernel modules") - see [Help:Style#Kernel module operations](/index.php/Help:Style#Kernel_module_operations "Help:Style").
*   There's small problem with similar instructions to use some kernel module option - I don't consider it to be _basic_ operation according to [Help:Style#Kernel module operations](/index.php/Help:Style#Kernel_module_operations "Help:Style"), but [this](/index.php/Wireless_Setup#madwifi-ng "Wireless Setup") to be too verbose. I think some clear note (can't think of any right now) and link to [Kernel modules#Setting module options](/index.php/Kernel_modules#Setting_module_options "Kernel modules") should be provided.

-- [Lahwaacz](/index.php/User:Lahwaacz "User:Lahwaacz") ([talk](/index.php/User_talk:Lahwaacz "User talk:Lahwaacz")) 19:09, 5 August 2013 (UTC)

NaN

### Links to Gentoo wiki

[http://en.gentoo-wiki.com/](http://en.gentoo-wiki.com/) is offline for some quite time now, the new address is [http://wiki.gentoo.org/](http://wiki.gentoo.org/). There are several links that need to be updated: [[3]](https://wiki.archlinux.org/index.php?title=Special%3ALinkSearch&target=http%3A%2F%2Fen.gentoo-wiki.com&namespace=0). I don't really know what (and when) happened there, I just suppose that there has been some major restructuring of the Gentoo documentation - there is not direct 1:1 mapping of the old links to the new address, so it will have to be done manually. -- [Lahwaacz](/index.php/User:Lahwaacz "User:Lahwaacz") ([talk](/index.php/User_talk:Lahwaacz "User talk:Lahwaacz")) 14:06, 22 February 2014 (UTC)

NaN

NaN

### Should we remove or archive obsolete articles?

[Ubuntu One](/index.php?title=Ubuntu_One&action=edit&redlink=1 "Ubuntu One (page does not exist)") is one I stumbled upon. I think it can be safely deleted. -- [Karol](/index.php/User:Karol "User:Karol") ([talk](/index.php/User_talk:Karol "User talk:Karol")) 19:22, 30 July 2014 (UTC)

NaN

NaN

NaN

NaN

NaN

NaN

NaN

NaN

NaN

NaN

NaN

NaN

NaN

NaN

NaN

NaN

NaN

NaN

NaN

NaN

NaN

NaN

NaN

NaN

NaN

NaN

NaN

NaN

NaN

NaN

NaN

NaN

NaN

Why exactly was the "separate namespace" way discarded? Was it [FS#35545](https://bugs.archlinux.org/task/35545)? -- [Lahwaacz](/index.php/User:Lahwaacz "User:Lahwaacz") ([talk](/index.php/User_talk:Lahwaacz "User talk:Lahwaacz")) 23:20, 13 August 2014 (UTC)

NaN

I have modified the row "Permission to perform archiving" for the "ArchWiki:Deleted" way to be simply "editors", which is the least privileged group which could perform archiving under ideal circumstances. There are some cases when editors wouldn't be able to perform the operation by themselves: for example if the archived page had some redirects pointing to it, they should be deleted, because archiving would create a double redirect and "normal" fix would cause the redirects to be archived too, which is useless since there is usually no history.

Also note that archiving would most likely involve more people from different groups: for example everybody could propose a page to be archived, then after reaching a consensus, admins/editors would archive the page, then editors/patrols would check the operation etc. This is not a good material for the table below since it applies to all methods, however it should be discussed because we will have to write guidelines for the archiving anyway.

-- [Lahwaacz](/index.php/User:Lahwaacz "User:Lahwaacz") ([talk](/index.php/User_talk:Lahwaacz "User talk:Lahwaacz")) 19:53, 16 August 2014 (UTC)

NaN

NaN

NaN

NaN

NaN

NaN

NaN

NaN

NaN

NaN

NaN

NaN

NaN

NaN

NaN

#### List of suggested solutions

A table of additional properties to follow the discussion more easily:

 Ideal | ~~Delete, don't look back~~
(current method, not a solution) | ~~Separate namespace~~
(discarded) | Redirect to a page like
"ArchWiki:Deleted" | Publicize [Special:Undelete](/index.php/Special:Undelete "Special:Undelete") |
| Type of archive operation | - | delete | move | redirect
<small>(i.e. modify content, then protect<sup>questioned</sup>)</small> | delete |
| Permission to perform archiving |  ??? | admins | depends on [config](https://www.mediawiki.org/wiki/Manual:$wgNamespaceProtection "mw:Manual:$wgNamespaceProtection") | editors | admins |
| Permission to undo archiving |  ??? | admins | depends on [config](https://www.mediawiki.org/wiki/Manual:$wgNamespaceProtection "mw:Manual:$wgNamespaceProtection") (?)
<small>(can be forced w/ copy/paste)</small> | editors | admins
<small>(can be forced w/ copy/paste)</small> |
| Page titles show in wiki search results | no | no | yes | yes
<small>(if redirects are included)</small> | no |
| Page content shows in wiki search results | no | no | yes | no | no |
| Page titles/content show in external search results | no | no | yes
<small>(unless disabled
with [1](https://www.mediawiki.org/wiki/Manual:$wgExemptFromUserRobotsControl "mw:Manual:$wgExemptFromUserRobotsControl") or [2](https://www.mediawiki.org/wiki/Manual:$wgNamespaceRobotPolicies "mw:Manual:$wgNamespaceRobotPolicies"))</small> | no | no |
| Secure (see discussion) | yes | yes | yes | yes |  ???
<small>(ask upstream)</small> |
| Pollutes other pages' backlinks and special pages | no | no | yes | no | no |
| Can link to archived revisions |  ??? | no | yes | yes | no |

#### Enforcement

In light of recent issues, I'd say it's time to finalize this discussion: anyone against enforcing the [ArchWiki:Deleted](/index.php?title=ArchWiki:Deleted&action=edit&redlink=1 "ArchWiki:Deleted (page does not exist)") redirect way? The new "deletion" procedure would be:

New but inappropriate articles:

*   If inappropriate because of spam or other clearly malicious content (evaluation is made by an admin), it's deleted right away.
*   In most of the other cases the article should be moved as a subpage of its author's User page.

Old articles gone deprecated:

1.  Mark for deletion;
2.  Wait at least 7 days: in absence of discussions/objections, redirect to [ArchWiki:Deleted](/index.php?title=ArchWiki:Deleted&action=edit&redlink=1 "ArchWiki:Deleted (page does not exist)").

Double redirects might be created after redirecting to [ArchWiki:Deleted](/index.php?title=ArchWiki:Deleted&action=edit&redlink=1 "ArchWiki:Deleted (page does not exist)"): these will have to be deleted, unless for some reason they contain part of the history of their targets; in this case a [merge](/index.php/Special:MergeHistory "Special:MergeHistory") should be considered, or the redirect should be moved to a "Target page (redirect[0-9]+)" title and redirected to [ArchWiki:Deleted](/index.php?title=ArchWiki:Deleted&action=edit&redlink=1 "ArchWiki:Deleted (page does not exist)") too, thus making it clear where to look for the more recent history.

In both cases, all the backlinks to the deleted or semi-deleted page will have to be removed.

I've left out the "notability" assessment (redirect if notable, fully delete if not) as there can't be objective guidelines for the choice and it might unnecessarily expose the responsible admin to complaints.

The [ArchWiki:Deleted](/index.php?title=ArchWiki:Deleted&action=edit&redlink=1 "ArchWiki:Deleted (page does not exist)") page (better title proposals will be considered) must be initialized with an evident link to its WhatLinksHere page.

I think it would make sense to start a campaign to restore articles that are currently in a deleted state; requesting restorations should be explicitly made possible in [ArchWiki talk:Deleted](/index.php?title=ArchWiki_talk:Deleted&action=edit&redlink=1 "ArchWiki talk:Deleted (page does not exist)").

Do we want to rename [Template:Deletion](/index.php/Template:Deletion "Template:Deletion") to [Template:Archive](/index.php?title=Template:Archive&action=edit&redlink=1 "Template:Archive (page does not exist)") or similar?

We'll also need a news entry to make this official, ~~I'll probably get there by the upcoming weekend in absence of substantial objections~~. Please help improve the procedure in case I missed something: it will have to be moved to [Help:Procedures](/index.php/Help:Procedures "Help:Procedures") once enforced.

— [Kynikos](/index.php/User:Kynikos "User:Kynikos") ([talk](/index.php/User_talk:Kynikos "User talk:Kynikos")) 06:09, 6 May 2015 (UTC) (Last edit: 03:02, 21 May 2015 (UTC))

PS: We must also address the problem of what to do with the talk pages of deleted articles, since I've seen discordant actions recently. — [Kynikos](/index.php/User:Kynikos "User:Kynikos") ([talk](/index.php/User_talk:Kynikos "User talk:Kynikos")) 06:18, 6 May 2015 (UTC)

PPS: I'd also like to better define "inappropriate", and at the same time give a more liberal and inclusive definition of "Stub", possibly shifting a bit our traditional perception of short-and-ugly articles, giving them more chances of being expanded/improved by other users than the original authors. Please share your ideas. — [Kynikos](/index.php/User:Kynikos "User:Kynikos") ([talk](/index.php/User_talk:Kynikos "User talk:Kynikos")) 06:33, 6 May 2015 (UTC)

##### Restoring revisions and redirection

About restoring revisions deleted in the past, we can use [mw:API:Deletedrevs](https://www.mediawiki.org/wiki/API:Deletedrevs "mw:API:Deletedrevs") to list and filter them. — [Kynikos](/index.php/User:Kynikos "User:Kynikos") ([talk](/index.php/User_talk:Kynikos "User talk:Kynikos")) 03:05, 9 May 2015 (UTC)

NaN

NaN

> anyone against enforcing the [ArchWiki:Deleted](/index.php?title=ArchWiki:Deleted&action=edit&redlink=1 "ArchWiki:Deleted (page does not exist)") redirect way? Since it is the only method that does not involve waiting for ~~Godot~~ Pierre, it seems logical to at least try it. After all, returning to the current method in case of dissatisfaction would involve only deleting the restored pages. Since we want MediaWiki to do something it is not built for, there are many issues. The most outstanding is the limited control over the archive. We've had disagreements in the maintenance team, imagine what might happen when everybody is technically, not per policy able to archive pages. -- [Lahwaacz](/index.php/User:Lahwaacz "User:Lahwaacz") ([talk](/index.php/User_talk:Lahwaacz "User talk:Lahwaacz")) 21:43, 9 May 2015 (UTC)

NaN

NaN

NaN

As another note on the redirect method, it should be mentioned that even redirects can be categorized, which could be utilized. -- [Lahwaacz](/index.php/User:Lahwaacz "User:Lahwaacz") ([talk](/index.php/User_talk:Lahwaacz "User talk:Lahwaacz")) 21:43, 10 May 2015 (UTC)

NaN

##### Separation of archive content

Next issue is with separation of the archive from the normal content. Since your proposed way of dealing with double redirect involves messing with the pages' histories and titles, there is inevitable need to organize the archive. I think that "ArchWiki is not a muzeum" should still apply regardless of the chosen archival method, ideally the motto would be as easily followed as it is now. Ideally the archive functionality would be built into MediaWiki itself (or any other backend we might use in the future), but publicizing [Special:Undelete](/index.php/Special:Undelete "Special:Undelete") is the closest (also accidentally keeping the maintenance burden on minimum). As far as I learned since the last summer, the "security" consideration could be dealt with by deleting an individual revision instead of the whole page, for which there is a separate `deleterevision` [right](http://www.mediawiki.org/wiki/Manual:User_rights). -- [Lahwaacz](/index.php/User:Lahwaacz "User:Lahwaacz") ([talk](/index.php/User_talk:Lahwaacz "User talk:Lahwaacz")) 21:43, 9 May 2015 (UTC)

NaN

NaN

NaN

NaN

NaN

NaN

NaN

NaN

NaN

##### Double redirects

I agree to most of the procedure. For double redirects, I vote for just delete them. Check their history is to much effort. --[Fengchao](/index.php/User:Fengchao "User:Fengchao") ([talk](/index.php/User_talk:Fengchao "User talk:Fengchao")) 13:04, 27 May 2015 (UTC)

NaN

##### Rename Template:Deletion

As for the [Template:Deletion](/index.php/Template:Deletion "Template:Deletion") --> [Template:Archive](/index.php?title=Template:Archive&action=edit&redlink=1 "Template:Archive (page does not exist)") renaming, I think that we could make use of both. After all _archiving_ does not fully replace _deleting_, there are more [reasons for deletion](/index.php/MediaWiki:Deletereason-dropdown "MediaWiki:Deletereason-dropdown") (archiving is currently one of them). Moreover, [Template:Deletion](/index.php/Template:Deletion "Template:Deletion") can be used to flag sections, whereas [Template:Archive](/index.php?title=Template:Archive&action=edit&redlink=1 "Template:Archive (page does not exist)") is/will be only for the whole pages. In a similar fashion, I think that the master page should not be called [ArchWiki:Deleted](/index.php?title=ArchWiki:Deleted&action=edit&redlink=1 "ArchWiki:Deleted (page does not exist)") but [ArchWiki:Archived](/index.php?title=ArchWiki:Archived&action=edit&redlink=1 "ArchWiki:Archived (page does not exist)"). -- [Lahwaacz](/index.php/User:Lahwaacz "User:Lahwaacz") ([talk](/index.php/User_talk:Lahwaacz "User talk:Lahwaacz")) 15:18, 1 June 2015 (UTC)

NaN

NaN

### Broken redirects

I have written a simple [script](https://github.com/lahwaacz/wiki-scripts/blob/master/list-redirects-broken-fragments.py) to list redirects with broken fragments (i.e. when no section with given title is found on the target page). After filtering out some false positives, here is the result. (And because I am incredibly selfish, I have eaten the low-hanging fruit before sharing the rest with others ;) )

As usual, please strike the fixed items off the list. Some things to consider:

*   The section might have been renamed, either to simplify the title, or just to fix capitalization as per [Help:Style#Section headings](/index.php/Help:Style#Section_headings "Help:Style").
*   Or it might have been merged with other, more generic section. Use the most relevant section for the redirect, or just redirect directly to the relevant page.
*   In the worst case, there is no relevant content on the target page. This will probably deserve a separate discussion.

-- [Lahwaacz](/index.php/User:Lahwaacz "User:Lahwaacz") ([talk](/index.php/User_talk:Lahwaacz "User talk:Lahwaacz")) 20:01, 18 August 2014 (UTC)

NaN

NaN

**Update:** I have removed the fixed redirects for better readability of the rest, for reference they can be found [here](https://wiki.archlinux.org/index.php?title=ArchWiki:Requests&oldid=353237#Broken_redirects). -- [Lahwaacz](/index.php/User:Lahwaacz "User:Lahwaacz") ([talk](/index.php/User_talk:Lahwaacz "User talk:Lahwaacz")) 17:51, 26 December 2014 (UTC)

Another update to the list, there are about 50 more broken redirects since the last time... -- [Lahwaacz](/index.php/User:Lahwaacz "User:Lahwaacz") ([talk](/index.php/User_talk:Lahwaacz "User talk:Lahwaacz")) 13:33, 11 April 2015 (UTC)

*   [Beginners' Guide/Installation](/index.php/Beginners%27_Guide/Installation "Beginners' Guide/Installation") --> [Beginners' guide#Installation](/index.php/Beginners%27_guide#Installation "Beginners' guide")
*   [Beginners' Guide/Installation (Español)](/index.php/Beginners%27_Guide/Installation_(Espa%C3%B1ol) "Beginners' Guide/Installation (Español)") --> [Beginners' guide (Español)#Instalación](/index.php/Beginners%27_guide_(Espa%C3%B1ol)#Instalaci.C3.B3n "Beginners' guide (Español)")
*   [Beginners' Guide/Installation (Русский)](/index.php/Beginners%27_Guide/Installation_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Beginners' Guide/Installation (Русский)") --> [Beginners' guide (Русский)#Установка](/index.php/Beginners%27_guide_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#.D0.A3.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B0 "Beginners' guide (Русский)")
*   [Beginners' Guide/Preface](/index.php/Beginners%27_Guide/Preface "Beginners' Guide/Preface") --> [Beginners' guide#Preparation](/index.php/Beginners%27_guide#Preparation "Beginners' guide")
*   [Beginners' Guide/Preparation](/index.php/Beginners%27_Guide/Preparation "Beginners' Guide/Preparation") --> [Beginners' guide#Preparation](/index.php/Beginners%27_guide#Preparation "Beginners' guide")
*   [Beginners' Guide/Preparation (Español)](/index.php/Beginners%27_Guide/Preparation_(Espa%C3%B1ol) "Beginners' Guide/Preparation (Español)") --> [Beginners' guide (Español)#Preparación](/index.php/Beginners%27_guide_(Espa%C3%B1ol)#Preparaci.C3.B3n "Beginners' guide (Español)")
*   [Beginners' Guide/Preparation (Русский)](/index.php/Beginners%27_Guide/Preparation_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Beginners' Guide/Preparation (Русский)") --> [Beginners' guide (Русский)#Подготовка](/index.php/Beginners%27_guide_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#.D0.9F.D0.BE.D0.B4.D0.B3.D0.BE.D1.82.D0.BE.D0.B2.D0.BA.D0.B0 "Beginners' guide (Русский)")
*   [Beginners' guide/Installation](/index.php/Beginners%27_guide/Installation "Beginners' guide/Installation") --> [Beginners' guide#Installation](/index.php/Beginners%27_guide#Installation "Beginners' guide")
*   [Beginners' guide/Installation (Español)](/index.php/Beginners%27_guide/Installation_(Espa%C3%B1ol) "Beginners' guide/Installation (Español)") --> [Beginners' guide (Español)#Instalación](/index.php/Beginners%27_guide_(Espa%C3%B1ol)#Instalaci.C3.B3n "Beginners' guide (Español)")
*   [Beginners' guide/Preparation](/index.php/Beginners%27_guide/Preparation "Beginners' guide/Preparation") --> [Beginners' guide#Preparation](/index.php/Beginners%27_guide#Preparation "Beginners' guide")
*   [Beginners' guide/Preparation (Español)](/index.php/Beginners%27_guide/Preparation_(Espa%C3%B1ol) "Beginners' guide/Preparation (Español)") --> [Beginners' guide (Español)#Preparación](/index.php/Beginners%27_guide_(Espa%C3%B1ol)#Preparaci.C3.B3n "Beginners' guide (Español)")
*   [Map Custom Device Entries with udev (Español)](/index.php/Map_Custom_Device_Entries_with_udev_(Espa%C3%B1ol) "Map Custom Device Entries with udev (Español)") --> [Udev (Español)#Escribir reglas udev](/index.php/Udev_(Espa%C3%B1ol)#Escribir_reglas_udev "Udev (Español)")
*   [Pacman Color Output (Español)](/index.php/Pacman_Color_Output_(Espa%C3%B1ol) "Pacman Color Output (Español)") --> [Pacman tips (Español)#Coloriando la salida de pacman](/index.php/Pacman_tips_(Espa%C3%B1ol)#Coloriando_la_salida_de_pacman "Pacman tips (Español)")
*   [Redownloading all installed packages](/index.php/Redownloading_all_installed_packages "Redownloading all installed packages") --> [Pacman tips#Redownloading All Installed Packages (minus AUR)](/index.php/Pacman_tips#Redownloading_All_Installed_Packages_.28minus_AUR.29 "Pacman tips") -- section renamed with [[6]](https://wiki.archlinux.org/index.php?title=Pacman_tips&diff=166562&oldid=166129), does the redirect still make sense?

### Hide irrelevant pages in search suggestions

Is it possible to hide some irrelevant pages in search suggestion? For example, we should not hide [Dkms](/index.php/Dkms "Dkms") page, because someone will looking that word. But we should hide irrelevant suggestions, such as [Internet Share](/index.php/Internet_Share "Internet Share"). It pollutes search and more unpleasant, I have sometimes created russian page with wrong title, because of this. I mean, I just added ' (Русский)' to english title, because when you are redirected, page's title in address string is still wrong. I understand, that we could not just delete them, because of some forums may use old titles. But making them invisible in Archwiki I think is good idea. [Agent0](/index.php/User:Agent0 "User:Agent0") ([talk](/index.php/User_talk:Agent0 "User talk:Agent0")) 14:39, 9 October 2014 (UTC)

NaN

NaN

NaN

### Article guideline

#### Contributing

Large portion of my Arch Wiki time is spent to below pages. Need a way to improve the situation. I think [Archwiki:Contributing](/index.php/ArchWiki:Contributing "ArchWiki:Contributing") could/should hold such information.

*   Specific Laptop pages - User should: Only add information to fix things that do not work. Do not list things already work well. Do not duplicate information from [Laptop](/index.php/Laptop "Laptop").
*   Specific Application pages - If the application work out of box and the page only list needed packages. Add it to [List of applications](/index.php/List_of_applications "List of applications").
*   Network related apps. For example [OwnCloud](/index.php/OwnCloud "OwnCloud"), only base platform setup (php, Apache) are Arch Linux specific. General settings should go upstream instead.

--[Fengchao](/index.php/User:Fengchao "User:Fengchao") ([talk](/index.php/User_talk:Fengchao "User talk:Fengchao")) 09:50, 11 December 2014 (UTC)

NaN

NaN

NaN

NaN

### TrackPoint

A new page, [TrackPoint](/index.php/TrackPoint "TrackPoint"), has been created to cover the configuration of the special input device typical to all/most ThinkPad laptops. There are still many pages duplicating the information, below is a complete list of pages that need to be merged. -- [Lahwaacz](/index.php/User:Lahwaacz "User:Lahwaacz") ([talk](/index.php/User_talk:Lahwaacz "User talk:Lahwaacz")) 20:56, 22 December 2014 (UTC)

*   [IBM_ThinkPad_X41#Scrolling_with_trackpoint](/index.php/IBM_ThinkPad_X41#Scrolling_with_trackpoint "IBM ThinkPad X41")
*   [Lenovo ThinkPad Edge E430](/index.php/Lenovo_ThinkPad_Edge_E430 "Lenovo ThinkPad Edge E430")
*   [Lenovo ThinkPad T410](/index.php/Lenovo_ThinkPad_T410 "Lenovo ThinkPad T410")
*   [Lenovo ThinkPad T420s](/index.php/Lenovo_ThinkPad_T420s "Lenovo ThinkPad T420s")
*   [Lenovo ThinkPad T530](/index.php/Lenovo_ThinkPad_T530 "Lenovo ThinkPad T530")
*   [Lenovo ThinkPad T61](/index.php/Lenovo_ThinkPad_T61 "Lenovo ThinkPad T61")
*   [Lenovo ThinkPad X120e](/index.php/Lenovo_ThinkPad_X120e "Lenovo ThinkPad X120e")
*   [Lenovo ThinkPad X220](/index.php/Lenovo_ThinkPad_X220 "Lenovo ThinkPad X220")
*   [Lenovo ThinkPad X230](/index.php/Lenovo_ThinkPad_X230 "Lenovo ThinkPad X230")
*   [Lenovo Thinkpad X60 Tablet](/index.php/Lenovo_Thinkpad_X60_Tablet "Lenovo Thinkpad X60 Tablet")

### Renamed software

#### Nautilus got renamed to Gnome Files

Do we want to rename every occurrence of 'nautilus' in Arch wiki or is [the redirect](https://wiki.archlinux.org/index.php?title=Nautilus&redirect=no) enough? -- [Karol](/index.php/User:Karol "User:Karol") ([talk](/index.php/User_talk:Karol "User talk:Karol")) 23:49, 21 August 2014 (UTC)

NaN

NaN

NaN

NaN

NaN

##### List

A list of pages where all possible instances Nautilus have been changed so we know what's been done and what hasn't. I will add to the list as I go through the pages returned in the search. -- [Chazza](/index.php/User:Chazza "User:Chazza") ([talk](/index.php/User_talk:Chazza "User talk:Chazza")) 11:41, 6 November 2014 (UTC)

*   [Nautilus](/index.php/Nautilus "Nautilus") - Completed
*   [Nautilus (日本語)](/index.php/Nautilus_(%E6%97%A5%E6%9C%AC%E8%AA%9E) "Nautilus (日本語)") - No changeable instances
*   [Digital Cameras](/index.php/Digital_Cameras "Digital Cameras") - Completed
*   [Awesome (한국어)](/index.php/Awesome_(%ED%95%9C%EA%B5%AD%EC%96%B4) "Awesome (한국어)") - Completed
*   [GNOME (简体中文)](/index.php/GNOME_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "GNOME (简体中文)") - Completed
*   [GNOME tips](/index.php/GNOME_tips "GNOME tips") - Completed
*   [Desktop environment](/index.php/Desktop_environment "Desktop environment") - No changeable instances
*   [Lineak](/index.php?title=Lineak&action=edit&redlink=1 "Lineak (page does not exist)") - No changeable instances
*   [GNOME tips (Nederlands)](/index.php/GNOME_tips_(Nederlands) "GNOME tips (Nederlands)") - Completed
*   [Firefox (العربية)](/index.php/Firefox_(%D8%A7%D9%84%D8%B9%D8%B1%D8%A8%D9%8A%D8%A9) "Firefox (العربية)") - No changeable instances
*   ~~[Bug Day/2010](/index.php/Bug_Day/2010 "Bug Day/2010") - No changeable instances~~
*   [Openbox (Česky)](/index.php/Openbox_(%C4%8Cesky) "Openbox (Česky)") - Completed
*   [fuseiso](/index.php/Fuseiso "Fuseiso") - Completed
*   [Beginners' Guide (Indonesia)](/index.php/Beginners%27_Guide_(Indonesia) "Beginners' Guide (Indonesia)") - Completed
*   [Feh](/index.php/Feh "Feh") - Completed
*   [Bluetooth (Italiano)](/index.php/Bluetooth_(Italiano) "Bluetooth (Italiano)") - Completed
*   [Feh (Italiano)](/index.php/Feh_(Italiano) "Feh (Italiano)") - Completed
*   [Samba (Italiano)](/index.php/Samba_(Italiano) "Samba (Italiano)") - Completed
*   [Backup programs](/index.php/Backup_programs "Backup programs") - Completed
*   [Oggenc](/index.php/Oggenc "Oggenc") - Completed
*   [Samba](/index.php/Samba "Samba") - Completed
*   [IPod](/index.php/IPod "IPod") - Completed
*   [Dropbox](/index.php/Dropbox "Dropbox") - Completed
*   [GNOME (Italiano)](/index.php/GNOME_(Italiano) "GNOME (Italiano)") - No changeable instances
*   [Samba (日本語)](/index.php/Samba_(%E6%97%A5%E6%9C%AC%E8%AA%9E) "Samba (日本語)") - Completed
*   [GNOME Tips (简体中文)](/index.php/GNOME_Tips_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "GNOME Tips (简体中文)") - Completed

#### XBMC renamed to Kodi

Since version 14 XBMC was renamed to Kodi, see [FS#43220](https://bugs.archlinux.org/task/43220). There are also some typos that say 'xmbc'. -- [Karol](/index.php/User:Karol "User:Karol") ([talk](/index.php/User_talk:Karol "User talk:Karol")) 10:59, 25 December 2014 (UTC)

NaN

NaN

NaN

#### Gummiboot

Gummiboot is included in [systemd](https://www.archlinux.org/packages/?name=systemd) since 220-2 as [systemd-boot](/index.php/Systemd-boot "Systemd-boot"). Relevant search: [gummiboot](https://wiki.archlinux.org/index.php?title=Special:Search&limit=500&offset=0&profile=default&search=gummiboot) -- [Lahwaacz](/index.php/User:Lahwaacz "User:Lahwaacz") ([talk](/index.php/User_talk:Lahwaacz "User talk:Lahwaacz")) 14:05, 30 August 2015 (UTC)

### Cleanup: links to non-existent packages

As of today, there are exactly 714 invalid uses (413 unique) of [Template:AUR](/index.php/Template:AUR "Template:AUR") or [Template:Pkg](/index.php/Template:Pkg "Template:Pkg"), spread across 398 pages. The complete list is on ~~[User:Lahwaacz.bot/Report 2014-04-05](/index.php?title=User:Lahwaacz.bot/Report_2014-04-05&action=edit&redlink=1 "User:Lahwaacz.bot/Report 2014-04-05 (page does not exist)")~~. I will try to go through it and update the links, but this is not a one-man job, so I would really appreciate some help. Please remember to strike/remove the items from the list to save others' time. -- [Lahwaacz](/index.php/User:Lahwaacz "User:Lahwaacz") ([talk](/index.php/User_talk:Lahwaacz "User talk:Lahwaacz")) 16:42, 5 April 2014 (UTC)

NaN

NaN

NaN

NaN

NaN

#### Surrounding link text

While performing [#Cleanup: links to non-existent packages](#Cleanup:_links_to_non-existent_packages), the bot updated a lot of package links, but of course it couldn't update the text around them accordingly, for example [[10]](https://wiki.archlinux.org/index.php?title=Smokeping&diff=prev&oldid=308608), so that's something else that could be done. Here's the list of the changes: ~~[[11]](https://wiki.archlinux.org/index.php?limit=250&tagfilter=&title=Special%3AContributions&contribs=user&target=Lahwaacz.bot&namespace=&year=2014&month=4)~~. -- [Kynikos](/index.php/User:Kynikos "User:Kynikos") ([talk](/index.php/User_talk:Kynikos "User talk:Kynikos")) 03:24, 7 April 2014 (UTC)

NaN

NaN

NaN

NaN

NaN

### Strategy for updating package templates

It is an open secret that the current strategy for updating package templates, which lies in creating a dedicated report page, is not very effective. The number of broken package links was 714 before the [first cleanup](https://lists.archlinux.org/pipermail/arch-general/2014-April/035793.html) almost a year ago. Today, after several successful cleanups the number is 979.

The first problem is that the report page is being noticed only a short time after announcing the cleanup and (almost) completely overlooked after a few days. Updating a wiki should be a continuous effort, but this strategy relies on announcing an event.

The second problem is that only English pages were consistently updated in the cleanups. No wonder since the events were announced only in English...

I have a proposal to solve the first problem, and partially also the second: instead of creating report pages and organizing cleanups, the broken package links could be marked directly in wiki pages, similarly to the way external links are marked with [Template:Dead link](/index.php/Template:Dead_link "Template:Dead link"). The result could look like this: [pkgname](https://www.archlinux.org/packages/?name=pkgname)<sup>broken link: hint</sup> where "broken link" is a link to a section with detailed instructions to fix the package link and "hint" is a short hint uniquely identifying the problem (given by the bot).

The proposal could be implemented in multiple ways:

1.  By introducing a single template, e.g. "Broken package link", which would take "hint" as a parameter and produce `<sup>broken link: _hint_</sup>`. This template would be added immediately after the broken instance of [Pkg](/index.php/Template:Pkg "Template:Pkg"), [AUR](/index.php/Template:AUR "Template:AUR") or [Grp](/index.php/Template:Grp "Template:Grp"), exactly the same way as [Template:Dead link](/index.php/Template:Dead_link "Template:Dead link") is added to broken external links.
2.  By introducing a separate template for each [Pkg](/index.php/Template:Pkg "Template:Pkg"), [AUR](/index.php/Template:AUR "Template:AUR") and [Grp](/index.php/Template:Grp "Template:Grp"), for example "Broken Pkg link", "Broken AUR link" and "Broken Grp link". These templates would take two parameters, the (broken) package name and the hint. Then, "Broken Pkg link" would produce `{{Pkg|_pkgname_}}<sup>broken link: _hint_</sup>` and so on.

So far I'm for the second way, which should be more favourable to the bot.

The advantage of this strategy is that broken package links and hints are continuously visible to everybody reading the wiki page, which are presumably people most interested in the topic at the moment, while maintainers can still easily go through full lists generated by [Special:WhatLinksHere](/index.php/Special:WhatLinksHere "Special:WhatLinksHere"). Also, I would not have to announce events :)

Of course I'm still open to other suggestions on solving the above problems, or any other if I missed something.

-- [Lahwaacz](/index.php/User:Lahwaacz "User:Lahwaacz") ([talk](/index.php/User_talk:Lahwaacz "User talk:Lahwaacz")) 18:51, 10 February 2015 (UTC)

NaN

NaN

NaN

NaN

NaN

NaN

NaN

NaN

### index.php in url address

Admins of Arch Wiki, do you noticed, that in every page address begins with _[https://wiki.archlinux.org/index.php?title=](https://wiki.archlinux.org/index.php?title=)_? Why? It is uncomfortable. Why could not you do just article name after _[https://wiki.archlinux.org/](https://wiki.archlinux.org/)_? — [Agent0](/index.php/User:Agent0 "User:Agent0") ([talk](/index.php/User_talk:Agent0 "User talk:Agent0")|[contribs](/index.php/Special:Contributions/Agent0 "Special:Contributions/Agent0")) 22:48, 6 March 2015 (UTC)

NaN

NaN

### Change drive naming/accessing to UUID?

Trying to install drives with/out Luks, LVM on internal, external drives is quite complicated currently. Following the ralated articles suggest different ways of reaching the goal. Many different drive name conventions are suggested, eg.:

*   /dev/sda2
*   /dev/md0
*   /dev/mapper/md/0
*   /dev/mapper/vgroup-lvm-root
*   /dev/vgroup-luks/root
*   ...

Some of them don't work with portable external drives. This overcomplicates setting up encrypted drives in different situations. My suggestion is, to change all drive related articles to one specific solution of addressing drives universal. Currently I think of UUDI drive naming as a way to go. This would ease the process of drive naming in all kinds of situations:

*   The reader is guided through system setup along one red line
*   Troubleshootiing "no drie found" is strait forward
*   Many sections become clearer to read even when not reading the whole article
*   Articles are easier to write and maintain
*   Beginners have an easier read and geta better idea of how to access drives
*   Accessing internal/external encrypted drives is easy

' LMV or other virtual file systems are easier to describe and setup

Ok, I know it is a big suggestion. I wanted to bring it up here, bacause I have the impression that following one primary path would help a lot - everyone involved. It doesn't need to be done in one day. While I think to have one suggested guideline would be a good start. Then with thain mind, we all have it easier to change those sections while Writing/editing Wiki entries.

[T.ask](/index.php?title=User:T.ask&action=edit&redlink=1 "User:T.ask (page does not exist)") ([talk](/index.php/User_talk:T.ask "User talk:T.ask")) 11:22, 30 March 2015 (UTC)

NaN

NaN

NaN

NaN

NaN

NaN

### User and group pacnew files

I just went about handling .pacnew files of [filesystem](https://www.archlinux.org/packages/?name=filesystem) and believe we are missing content for it. It's important, as one can havoc a system mishandling them. Neither [Users and groups](/index.php/Users_and_groups "Users and groups") nor [Pacnew and Pacsave files](/index.php/Pacnew_and_Pacsave_files "Pacnew and Pacsave files") mentions it; both should in my view. I'm creating the item here to:

1.  Check if I missed where it may be mentioned.
2.  Confirm procedure for handling them: can anyone think of valid reasons/cases in the current situation not to delete passwd/group/shadow.pacnew files?
3.  Ensure we add it to the relevant places. Opinions?

--[Indigo](/index.php/User:Indigo "User:Indigo") ([talk](/index.php/User_talk:Indigo "User talk:Indigo")) 12:03, 18 April 2015 (UTC)

NaN

NaN

### FAQ

The [FAQ](/index.php/FAQ "FAQ") could use an entry like "After upgrading my kernel, I can't mount USB devices", preferably linking [FS#16702](https://bugs.archlinux.org/task/16702). See [[21]](https://wiki.archlinux.org/index.php?title=VirtualBox&curid=3745&diff=400434&oldid=400154) for a case where users are not aware of this. -- [Alad](/index.php/User:Alad "User:Alad") ([talk](/index.php/User_talk:Alad "User talk:Alad")) 22:55, 18 September 2015 (UTC)

NaN

## Bot requests

_Here, list requests for repetitive, systemic modifications to a series of existing articles to be performed by a wiki bot._

Retrieved from "[https://wiki.archlinux.org/index.php?title=ArchWiki:Requests&oldid=416989](https://wiki.archlinux.org/index.php?title=ArchWiki:Requests&oldid=416989)"