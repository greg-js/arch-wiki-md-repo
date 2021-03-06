<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Introduction](#Introduction)
*   [2 Ideas and Suggestions](#Ideas_and_Suggestions)
    *   [2.1 OpenID](#OpenID)
    *   [2.2 Developer/Fellows profiles](#Developer/Fellows_profiles)
    *   [2.3 Navbar for internal Arch sites](#Navbar_for_internal_Arch_sites)
    *   [2.4 URI Linking](#URI_Linking)
    *   [2.5 Focus in Search](#Focus_in_Search)
    *   [2.6 Direct package links by name](#Direct_package_links_by_name)
    *   [2.7 Adopting archweb_manpages](#Adopting_archweb_manpages)

## Introduction

This article is intended as a sandbox of ideas for the Arch Linux website. Feel free to add suggestions and any thoughts you might have about how the Arch Linux website can be improved.

This article is part of the [DeveloperWiki](/index.php/DeveloperWiki "DeveloperWiki").

## Ideas and Suggestions

### OpenID

Implement an [OpenID](http://openid.net/)-like identity system for the official Arch Linux websites.

*   If we could integrate login/pass throughout AUR, Wiki, Forums, and Bugs this way ... well I'm afraid I'd get a bit moist. :)
    [georgia_tech_swagger](/index.php/User:Georgia_tech_swagger "User:Georgia tech swagger")
*   Might also consider Mozilla Persona[[1]](https://www.mozilla.org/en-US/persona/), which should be easier to implement than full blown openID.

I completely agree with this idea. I dreamed this since registration. Is it possible to implement? Also, it would be great that it would be possible to login to external arch wikis. — [Agent0](/index.php/User:Agent0 "User:Agent0") ([talk](/index.php/User_talk:Agent0 "User talk:Agent0")|[contribs](/index.php/Special:Contributions/Agent0 "Special:Contributions/Agent0")) 11:12, 22 July 2015 (UTC)

### Developer/Fellows profiles

Condense the developer profiles pages, reducing photo sizes and dropping relatively unimportant fields such as: Favourite Distros, Year of Birth, Interests, Other Contacts, etc.

*   I don't like this idea. I like any distro that has a soul and flavor to it. Sterile "strictly-business" design and community should be left to the Wall Street distros.
    [georgia_tech_swagger](/index.php/User:Georgia_tech_swagger "User:Georgia tech swagger")

### Navbar for internal Arch sites

Look at the feasibility of creating a unified navbar that would sit at the top of all Arch community sites (bbs.archlinux, wiki.archlinux, etc.), providing an exact copy of the main website hierarchy via drop-down menus (using CSS of course).

	The current navbar *is* unified. What hierarchy would you propose for the drop-down menus? -- [Lahwaacz](/index.php/User:Lahwaacz "User:Lahwaacz") ([talk](/index.php/User_talk:Lahwaacz "User talk:Lahwaacz")) 19:37, 13 December 2019 (UTC)

### URI Linking

Implement a pacman:// URI as an option to quickly let users quickly install packages from webpages and same the functionality for AUR packages. [9mmtylenol](/index.php/User:9mmtylenol "User:9mmtylenol")

	I think it is easy to implement. It is very similar to [apt urls](https://wiki.debian.org/AptProtocol). It is even possible to install several packages [at once](https://help.ubuntu.com/community/AptURL#Use_of_apturl). But what is the difference in using such *apt:vlc* links from such *apt://vlc* ? — [Agent0](/index.php/User:Agent0 "User:Agent0") ([talk](/index.php/User_talk:Agent0 "User talk:Agent0")|[contribs](/index.php/Special:Contributions/Agent0 "Special:Contributions/Agent0")) 16:10, 28 July 2015 (UTC)

### Focus in Search

Is it possible to make ArchWiki to automatically focus on search box? It is common behavior. Look for example to [youtube](https://youtube.com) or [wikipedia](https://wikipedia.org). I feel uncomfortable, when I go to wiki.archlinux.org and additionally need to use mouse to focus on search field. I know about `Alt + Shift + f`, but it is not working, because alt+shift changes keyboard layout. — [Agent0](/index.php/User:Agent0 "User:Agent0") ([talk](/index.php/User_talk:Agent0 "User talk:Agent0")|[contribs](/index.php/Special:Contributions/Agent0 "Special:Contributions/Agent0")) 12:29, 17 November 2015 (UTC)

	On HTML5 you just have to add the "autofocus" attribute to the input (in this case the element with id="searchInput"). -- **nucularJohn**

### Direct package links by name

On the ArchWiki we can only link to packages using the package search, for example [pacman](https://www.archlinux.org/packages/?name=pacman) links to [https://www.archlinux.org/packages/?name=pacman](https://www.archlinux.org/packages/?name=pacman), requiring the reader to always click twice to get to a package page. It would be nice if there were another argument like `direct` to directly take you to the respective package.

--[Larivact](/index.php/User:Larivact "User:Larivact") ([talk](/index.php/User_talk:Larivact "User talk:Larivact")) 14:06, 4 November 2018 (UTC)

	Packages can exist in multiple repositories, and formerly, in multiple architectures. This is why we never did this. Do you have a suggestion for figuring out which package it refers to? -- [Eschwartz](/index.php/User:Eschwartz "User:Eschwartz") ([talk](/index.php/User_talk:Eschwartz "User talk:Eschwartz")) 01:35, 11 November 2018 (UTC)

	Redirect to a stable package with the given name if it exists, otherwise return a 404\. Exemplary URL:

	[https://www.archlinux.org/packages/?stable_by_name=pacman](https://www.archlinux.org/packages/?stable_by_name=pacman)

	--[Larivact](/index.php/User:Larivact "User:Larivact") ([talk](/index.php/User_talk:Larivact "User talk:Larivact")) 06:47, 11 November 2018 (UTC)

	Figuring out if a pkgname is unique or not is very easy [in SQL](https://git.archlinux.org/archweb.git/tree/main/models.py#n88) - just `SELECT pkgname, repo, arch FROM Package WHERE pkgname = ?` and if you get just 1 result, you can show the package view, otherwise you have to show the package search view. -- [Lahwaacz](/index.php/User:Lahwaacz "User:Lahwaacz") ([talk](/index.php/User_talk:Lahwaacz "User talk:Lahwaacz")) 08:30, 11 November 2018 (UTC)

	I think you misunderstood, this is not about changing the search to redirect if there is only one result, this is about introducing a new API specifically for [Template:Pkg](/index.php/Template:Pkg "Template:Pkg"). We only link packages in the stable repositories, where pkgnames should be unique, so we can do:

	`SELECT pkgname, repo FROM packages INNER JOIN repos ON repo=packages.id WHERE pkgname = ? AND testing = false AND staging = false`

	--[Larivact](/index.php/User:Larivact "User:Larivact") ([talk](/index.php/User_talk:Larivact "User talk:Larivact")) 09:01, 11 November 2018 (UTC)

	The use of [Template:Pkg](/index.php/Template:Pkg "Template:Pkg") is not limited to stable repositories, see e.g. [[2]](https://wiki.archlinux.org/index.php?title=Thunderbolt&diff=583488&oldid=576452). My query is simpler and it would not limit the template. -- [Lahwaacz](/index.php/User:Lahwaacz "User:Lahwaacz") ([talk](/index.php/User_talk:Lahwaacz "User talk:Lahwaacz")) 19:28, 13 December 2019 (UTC)

### Adopting archweb_manpages

[Lahwaacz](/index.php/User:Lahwaacz "User:Lahwaacz") developed and hosts [https://jlk.fjfi.cvut.cz/arch/manpages/](https://jlk.fjfi.cvut.cz/arch/manpages/), which is used on the ArchWiki for links to man pages, e.g. [pacman(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/pacman.8). See [Template talk:Man#Sources](/index.php/Template_talk:Man#Sources "Template talk:Man") and the [GitHub repository](https://github.com/lahwaacz/archweb_manpages). I think this should be adopted as an official Arch Linux project if only for a nicer domain name (man.archlinux.org).

--[Larivact](/index.php/User:Larivact "User:Larivact") ([talk](/index.php/User_talk:Larivact "User talk:Larivact")) 14:27, 4 November 2018 (UTC)

	👍 You or Lahwaacz may want to email that proposal to the [arch-projects ML](https://lists.archlinux.org/listinfo/arch-projects). -- [Polyzen](/index.php?title=User:Polyzen&action=edit&redlink=1 "User:Polyzen (page does not exist)") ([talk](/index.php/User_talk:Polyzen "User talk:Polyzen")) 20:42, 11 January 2019 (UTC)

	I doubt that arch-projects is the right mailing list - it is used for development discussions of existing projects with their maintainers and not for a wider user discussion which is needed to propose and adopt a new project. -- [Lahwaacz](/index.php/User:Lahwaacz "User:Lahwaacz") ([talk](/index.php/User_talk:Lahwaacz "User talk:Lahwaacz")) 19:35, 13 December 2019 (UTC)