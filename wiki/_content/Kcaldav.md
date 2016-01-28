# Kcaldav

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

[![Tango-two-arrows.png](/images/7/72/Tango-two-arrows.png)](/index.php/File:Tango-two-arrows.png)

[![Tango-two-arrows.png](/images/7/72/Tango-two-arrows.png)](/index.php/File:Tango-two-arrows.png)

**This article or section is a candidate for merging with [KDE](/index.php/KDE "KDE").**

**Notes:** please use the second argument of the template to provide more detailed indications. (Discuss in [Talk:Kcaldav#](https://wiki.archlinux.org/index.php/Talk:Kcaldav))

Related articles

*   [DAViCal](/index.php/DAViCal "DAViCal")
*   [AgenDAV](/index.php/AgenDAV "AgenDAV")
*   [Radicale](/index.php/Radicale "Radicale")

If you want to connect your google calendar with korganizer you need kcaldav from [AUR](/index.php/AUR "AUR") package [kcaldav](https://aur.archlinux.org/packages/kcaldav/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/kcaldav)]</sup>.

After installing kcaldav you need to log out and in again to register the caldav service.

Now you can import your google calendar into korganizer:

*   open korganizer (or kontact)
*   click on the green '+' symbol to add a new calendar
*   select CalDAV server from the list of available types
*   address is: " https://www.google.com/calendar/dav/[calendar name]/events/ "
    *   you can get the calendar name, when you open google calendar in your browser, then go to

**My calendars** click on the down arrow for the calendar you want to import and select **Calendar settings**

*   *   copy the name of the calendar; the default name would be <name>@gmail.com
*   enter your username and password in the appropriate fields

Now you should be able to use google calendar from within korganizer.

Retrieved from "[https://wiki.archlinux.org/index.php?title=Kcaldav&oldid=400396](https://wiki.archlinux.org/index.php?title=Kcaldav&oldid=400396)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [Applications](/index.php/Category:Applications "Category:Applications")

Hidden categories:

*   [Pages or sections flagged with Template:Merge](/index.php/Category:Pages_or_sections_flagged_with_Template:Merge "Category:Pages or sections flagged with Template:Merge")
*   [Pages with broken package links](/index.php/Category:Pages_with_broken_package_links "Category:Pages with broken package links")