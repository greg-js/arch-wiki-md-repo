[Wiki Monkey](https://github.com/kynikos/wiki-monkey/wiki) is a MediaWiki-compatible bot and editor assistant that can be used directly within wiki pages in the browser as a user script. It is developed and tested on [Firefox](/index.php/Firefox "Firefox"), and designed to work also on [Chromium](/index.php/Chromium "Chromium") and [Opera](/index.php/Opera "Opera"), for which full support is given; it is very likely to work also on other browsers out of the box or with minor adaptations.

The project is currently focused on ArchWiki, and as such most plugins address ArchWiki-specific problems.

## Contents

*   [1 Installation](#Installation)
*   [2 Tour of the features](#Tour_of_the_features)
    *   [2.1 Editor pages](#Editor_pages)
    *   [2.2 Diff pages](#Diff_pages)
    *   [2.3 Page lists (Bot)](#Page_lists_.28Bot.29)
    *   [2.4 Special functions](#Special_functions)
    *   [2.5 Recent Changes and New Pages](#Recent_Changes_and_New_Pages)
    *   [2.6 Contributions](#Contributions)
*   [3 See also](#See_also)

## Installation

Follow the instructions at [Getting started](https://github.com/kynikos/wiki-monkey/wiki/Getting-started).

## Tour of the features

Discover the features of Wiki Monkey by following this tour. See [Usage](https://github.com/kynikos/wiki-monkey/wiki/Usage) and [Bundled plugins](https://github.com/kynikos/wiki-monkey/wiki/Bundled-plugins) for more detailed information.

**Tip:** At the bottom of Wiki Monkey's interface you will always find a log area, on dark background, where Wiki Monkey and its plugins will output their messages.

### Editor pages

In every *editor* page (e.g. [ArchWiki:Sandbox's](https://wiki.archlinux.org/index.php?title=ArchWiki:Sandbox&action=submit)) you will find Wiki Monkey's interface right below the *Save page* button row. As you can see there are some buttons, each of which either represents a plugin or a group of plugins accessible in a submenu; clicking on the labeled buttons will execute the associated plugin or the whole group of plugins sequentially; clicking on the ">" button next to a submenu button will open the submenu; clicking on the "*" button in the root menu will execute all the plugins; clicking on the "<" button in a submenu will return to the parent menu.

By executing a plugin, the text in the editor will be modified, but note that the page will not be saved, so you will still be able to see the diff or the preview and perform other modifications manually.

*   *Text plugins* groups all plugins that act immediately on the source text.
    *   *Fix header* reorders the elements in the header, warns about possible problems (e.g. lack of category) and tries to fix some.
    *   *Fix headings* tries to fix the levels of section headings so that they start from level 2 and do not increase by more than 1 level with relation to the parent section.
    *   *Fix external links* tries to turn external links into proper internal/interwiki links (e.g. Wikipedia), or templates (e.g. [Template:Pkg](/index.php/Template:Pkg "Template:Pkg")).
    *   *Fix section links* checks links to sections (`[[#Section]]`) and tries to fix them if broken.
    *   *Use code templates* replaces `<pre>`, `<code>` and `<tt>` with [Template:bc](/index.php/Template:Bc "Template:Bc") and [Template:ic](/index.php/Template:Ic "Template:Ic"), taking care of adding numbered parameters or `<nowiki>` tags when necessary.
    *   *Expand contractions* expands some common English contractions, e.g. "don't" becomes "do not".
    *   *Squash multiple line breaks* compresses multiple empty lines into one.
    *   *Convert summary to related* starts the conversion discussed in [Help talk:Style/Article summary templates#Deprecation of summaries and overviews](/index.php/Help_talk:Style/Article_summary_templates#Deprecation_of_summaries_and_overviews "Help talk:Style/Article summary templates"); the user will have to finish it manually.
*   *RegExp substitution* lets you perform a regular expression substitution.
*   *Query plugins* groups all the plugins that need to query external pages in order to obtain the information needed to update the page.
    *   *Fix external section links* checks links to sections of other articles (`[[Article#Section]]`) and tries to fix them if broken; it also supports [Template:Related](/index.php/Template:Related "Template:Related") and [Template:Related2](/index.php/Template:Related2 "Template:Related2").
    *   *Sync interlanguage links* synchronizes the interlanguage links of the edited page with those of its translations.
    *   *Fix old AUR links* converts direct AUR-1.x package links to instances of [Template:AUR](/index.php/Template:AUR "Template:AUR") (or [Template:Pkg](/index.php/Template:Pkg "Template:Pkg") if the package has been moved to the official repositories).
    *   *Update package templates* checks the existence of the packages and groups linked through [Template:Pkg](/index.php/Template:Pkg "Template:Pkg"), [Template:AUR](/index.php/Template:AUR "Template:AUR") and [Template:Grp](/index.php/Template:Grp "Template:Grp") and tries to update any broken template.

In addition to these plugins, Wiki Monkey also suppresses the default browser behavior of saving a page when — usually accidentally — pressing `Enter` in the Summary field of an editor page; this functionality can however be re-enabled in Wiki Monkey's configuration.

### Diff pages

In every *diff* page (e.g. [one from ArchWiki:Sandbox's history](https://wiki.archlinux.org/index.php?title=ArchWiki:Sandbox&diff=262475&oldid=261738)) you will find Wiki Monkey's interface right below the two diff panes. Here the only bundled plugin is *Quick report*, which adds a row with a link to the visited diff in the specialized table of [ArchWiki:Reports](/index.php/ArchWiki:Reports "ArchWiki:Reports"). See also [ArchWiki:Maintenance Team](/index.php/ArchWiki:Maintenance_Team "ArchWiki:Maintenance Team").

### Page lists (Bot)

You will find Wiki Monkey's Bot interface in many pages that show lists of pages (e.g. [Category pages](/index.php/Special:Categories "Special:Categories"), [What Links Here pages](/index.php/Special:WhatLinksHere "Special:WhatLinksHere") and many [Special pages](/index.php/Special:SpecialPages "Special:SpecialPages"); see [Category:Sandbox](/index.php/Category:Sandbox "Category:Sandbox") for a specific example). The usage of the Bot interface is explained in [the upstream documentation](https://github.com/kynikos/wiki-monkey/wiki/Usage#bot-interface). The actions that can be executed by the bot are:

*   Substituting text through regular expressions.
*   Checking and trying to fix any broken links (including [Template:Related](/index.php/Template:Related "Template:Related") and [Template:Related2](/index.php/Template:Related2 "Template:Related2")) to specific sections of a target article, which can be specified through a text field and in [What Links Here pages](/index.php/Special:WhatLinksHere "Special:WhatLinksHere") defaults to the linked page.
*   Synchronizing the interlanguage links of pages with those of their translations.
*   Checking the existence of the packages and groups linked through [Template:Pkg](/index.php/Template:Pkg "Template:Pkg"), [Template:AUR](/index.php/Template:AUR "Template:AUR") and [Template:Grp](/index.php/Template:Grp "Template:Grp") and trying to update any broken templates.
*   Converting direct AUR-1.x package links to instances of [Template:AUR](/index.php/Template:AUR "Template:AUR") (or [Template:Pkg](/index.php/Template:Pkg "Template:Pkg") if the package has been moved to the official repositories) (the Bot is shown only if there is at least one item in the list).

**Note:** The Bot interface is hidden by default, you will have to show it by clicking on the dedicated link.

### Special functions

You will also find Wiki Monkey's interface at the top of [Special:SpecialPages](/index.php/Special:SpecialPages "Special:SpecialPages"): here you will be able to access those plugins that have a generic purpose and are not based on a specific page. The available plugins are a function to update [Table of contents](/index.php/Table_of_contents "Table of contents") pages, and a function to fix [double redirects](/index.php/Special:DoubleRedirects "Special:DoubleRedirects").

### Recent Changes and New Pages

At the top of [Special:RecentChanges](/index.php/Special:RecentChanges "Special:RecentChanges") and [Special:NewPages](/index.php/Special:NewPages "Special:NewPages") you will find Wiki Monkey's filter: currently the bundled filter only groups the list entries by the language of the respective article.

**Note:** The default filter is designed to work on top of MediaWiki's Recent Changes filter, which can be enabled in [Special:Preferences#mw-prefsection-rc](/index.php/Special:Preferences#mw-prefsection-rc "Special:Preferences"). This also means that you must be logged on in order to use it.

Also, *rollback* links are hidden by default in [Special:RecentChanges](/index.php/Special:RecentChanges "Special:RecentChanges") pages; they can be reenabled in the configuration.

### Contributions

*Rollback* links are hidden by default in [Special:Contributions](/index.php/Special:Contributions "Special:Contributions") pages; they can be reenabled in the configuration.

## See also

*   [Configuration](https://github.com/kynikos/wiki-monkey/wiki/Configuration)
*   [Changelog](https://github.com/kynikos/wiki-monkey/wiki/Changelog)
*   [Troubleshooting](https://github.com/kynikos/wiki-monkey/wiki/Troubleshooting)
*   [Bug reports, feature requests, questions](https://github.com/kynikos/wiki-monkey/issues)