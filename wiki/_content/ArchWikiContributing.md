# ArchWiki:Contributing

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

ArchWiki strives to be a clear, comprehensive and professional model of documentation. In order to reach that goal we have to organize the job in a rational and functional way: this article tries to explain schematically what are the most important tasks you can give your help to accomplish.

This is a community effort, but if you take on the task seriously, a formal position as a [wiki maintainer](/index.php/ArchWiki:Maintenance_Team "ArchWiki:Maintenance Team") may be in order.

## Contents

*   [1 The 3 fundamental rules](#The_3_fundamental_rules)
    *   [1.1 Always properly use the edit summary](#Always_properly_use_the_edit_summary)
    *   [1.2 Do not make complex edits at once](#Do_not_make_complex_edits_at_once)
    *   [1.3 Announce article rewrites in a talk page](#Announce_article_rewrites_in_a_talk_page)
*   [2 The most important task](#The_most_important_task)
*   [3 Resources](#Resources)
*   [4 Creating](#Creating)
*   [5 Improving](#Improving)
    *   [5.1 Non-Arch users](#Non-Arch_users)
*   [6 Maintaining](#Maintaining)
*   [7 Organizing](#Organizing)
*   [8 Translating](#Translating)
    *   [8.1 Special messages translation](#Special_messages_translation)
*   [9 Brainstorming](#Brainstorming)
*   [10 Back-end maintenance](#Back-end_maintenance)
*   [11 Complaining](#Complaining)

## The 3 fundamental rules

There are 3 simple rules that all contributors, including novices, should try their best to follow as a sign of **respect** to the other users of the wiki: [#Always properly use the edit summary](#Always_properly_use_the_edit_summary), [#Do not make complex edits at once](#Do_not_make_complex_edits_at_once) and [#Announce article rewrites in a talk page](#Announce_article_rewrites_in_a_talk_page).

All wiki contributors must assume and expect that other users will check their edits sooner or later, and respect their right to do so by making it as quick and easy as possible by following these recommendations. Those familiar with collaborative software projects will easily understand the analogy between wiki edit summaries and git commit messages, and between wiki edit diffs and git diffs.

**Warning:** Any edits to articles that do not respect these fundamental rules, and as such cannot be comprehended with reasonable effort, may be completely reverted without any other warnings, especially when affecting popular articles.

### Always properly use the edit summary

The edit summary is the little text box that is found below the main editing area and just above the "Save page" button. It is very important to always write, in a succinct way, **what** has been done and **why**. Note that internal wiki links do work in edit summaries, so use them to link to any related discussions or articles; similarly, paste any urls to relevant edit diffs or external resources, such as forum threads or mailing lists.

Only in case of [minor](https://en.wikipedia.org/wiki/Help:Minor_edit "wikipedia:Help:Minor edit") edits, e.g. grammar or orthography corrections or the simple rewording of a sentence, the "why" part can be omitted; analogously, starting a new [discussion](/index.php/Help:Discussion "Help:Discussion") or replying to an existing one does not require to restate the message in the edit summary.

**Tip:**

*   Take a look at the edit summaries in the [Recent Changes](/index.php/Special:RecentChanges "Special:RecentChanges") to get an idea of what you should write in your summary, but be warned that unfortunately not all users are aware of these guidelines.
*   To receive a warning when leaving a blank edit summary, check _"Prompt me when entering a blank edit summary"_ in [Special:Preferences](/index.php/Special:Preferences#mw-prefsection-editing "Special:Preferences").
*   Use links like [Special:Diff/359881/next](/index.php/Special:Diff/359881/next "Special:Diff/359881/next") for clickable references to diffs, see [mw:Help:Diff](https://www.mediawiki.org/wiki/Help:Diff "mw:Help:Diff") for syntax details.

### Do not make complex edits at once

If you want to make an extensive change to a page, be it a normal article or a discussion page, always split your work in several simple edits, for example according to the various logical steps needed to complete it. If in doubt, preview the resulting [diff](https://en.wikipedia.org/wiki/Help:Diff "wikipedia:Help:Diff") with the "Show changes" button and wonder if another user would be able to understand it, also considering the edit summary as explained above. Some common operations that generate confusing diffs are:

*   Moving a section in an article and at the same time editing its content. Solution: move the section unchanged, save, and change its content in a following edit.
*   Reordering several sections of an article at the same time. Solution: move only one section per edit.

**Note:** This practice will naturally increase the number of entries in [Special:RecentChanges](/index.php/Special:RecentChanges "Special:RecentChanges"): do not be worried at all by this, users can easily filter that list by enabling the _Group changes by page in recent changes and watchlist_ setting under _Preferences > Recent changes > Advanced options_.

### Announce article rewrites in a talk page

If you want to radically restructure or rewrite an article or a group of articles, announce and explain your intention in an appropriate talk page first, giving any other interested users some reasonable time to reply and share their view.

Keep in mind that announcing intended changes does **not** exempt edits from [#Always properly use the edit summary](#Always_properly_use_the_edit_summary) and [#Do not make complex edits at once](#Do_not_make_complex_edits_at_once).

## The most important task

In the remainder of this article you will be presented with the various ways you can contribute to the wiki. Among them, however, there is one that you should consider far more important than the others: **add your favorite articles to your watchlist** and protect them against counter-productive edits.

Every day, ArchWiki receives [several dozens](/index.php/ArchWiki:Statistics "ArchWiki:Statistics") of edits from many different users: while most of these changes are actual improvements, it only takes one single edit, often made in good faith, to inaccurately alter the meaning of a whole paragraph or a section, or sometimes even unreasonably delete it altogether; if gone unnoticed, this will ruin the valuable work that you and all the other previous editors had done. Unfortunately, this occurs more frequently than you would expect: the official wiki staff does try their best to filter and fix counter-productive edits, but you should never rely completely on them, both because, just like you, they have limited time to spend on the wiki, and also because they are not omniscient, and it is very likely that your knowledge on the topics treated in your favorite articles is greater than theirs. In general, a wiki simply does _not_ work if users only focus on writing new content but then do not care about what happens to their contributions.

Fortunately, there is a very easy way for you to follow the articles to which you contributed or those that you like the most or are most knowledgeable in: at the top of every article there is a "watch" link, and by following it, that article will be added to [your watchlist](/index.php/Special:EditWatchlist "Special:EditWatchlist"). You will then be able to follow the changes in [Special:Watchlist](/index.php/Special:Watchlist "Special:Watchlist"), or by choosing to be notified by email when the watched articles receive updates in the "Email options" field of [Special:Preferences#mw-prefsection-personal](/index.php/Special:Preferences#mw-prefsection-personal "Special:Preferences"); the pages you are following will also be highlighted in bold in [Special:RecentChanges](/index.php/Special:RecentChanges "Special:RecentChanges"). Finally, preferences for the watchlist are found in [Special:Preferences#mw-prefsection-watchlist](/index.php/Special:Preferences#mw-prefsection-watchlist "Special:Preferences"): among the options you can even choose to automatically start watching the pages that you create or edit.

If you notice that an article in your watchlist has received an inaccurate edit, or you just do not understand it, you are strongly encouraged to either fix it, if possible, or to start a discussion in the article's [talk page](/index.php/Help:Discussion "Help:Discussion"), or in the responsible author's talk page.

## Resources

Here is a list of pages that contain information needed for contributing:

*   [Help:Article naming guidelines](/index.php/Help:Article_naming_guidelines "Help:Article naming guidelines") discusses effective article naming strategies and considerations to ensure readability and improve navigation of the wiki. Read it before creating a new page.
*   [Help:Editing](/index.php/Help:Editing "Help:Editing") outlines both widely-known MediaWiki markup and ArchWiki-specific guidelines. A must-read for any would-be contributors.
*   [Help:Discussion](/index.php/Help:Discussion "Help:Discussion") guides you on how to discuss with people in talk pages.
*   [Help:Style](/index.php/Help:Style "Help:Style") gives guidelines for the standardization of style in ArchWiki articles.
*   [Help:Category](/index.php/Help:Category "Help:Category") explains how to set page categories, how to create missing category pages and how to move a page to a different category.
*   [ArchWiki Translation Team](/index.php/ArchWiki_Translation_Team "ArchWiki Translation Team") has a step-by-step introduction for creating a new translation page. Follow it to translate pages to your own language.
*   [Help:i18n](/index.php/Help:I18n "Help:I18n") serves as a comprehensive guideline for ArchWiki internationalization and localization.
*   [Help:Procedures](/index.php/Help:Procedures "Help:Procedures") is a collection of useful check lists for complex operations.

See [Category:Help](/index.php/Category:Help "Category:Help") for all help articles.

## Creating

Ensure you understand the philosophy of ArchWiki and think about what others may want to read (see [ArchWiki:Requests](/index.php/ArchWiki:Requests "ArchWiki:Requests") for ideas). As mentioned, the wiki's scope is quite wide.

Talk to the [admins](/index.php/ArchWiki:Administrators "ArchWiki:Administrators") for help coordinating major projects.

[Help:Editing#Creating pages](/index.php/Help:Editing#Creating_pages "Help:Editing") covers the steps to create a new article in the main namespace.

The wiki's subpage feature (article/subpage) is available for your userpage as well. Using it you could create the draft on a blank subpage. Please note that userpage content must not be categorized, but all other features can be used. Once you have finished drafting, you can simply move the subpage to its new name. Please add relevant article status templates (only) after you moved it. The better you describe a status template's reason, the easier it is for users [#Improving](#Improving) the wiki to collaborate with you.

## Improving

Content editing, proofreading, and updating are never-ending tasks on any wiki. If you want to help, just register an account and start performing your magic.

*   Help fulfilling [requests](/index.php/ArchWiki:Requests "ArchWiki:Requests").
*   Add content to [stubs](/index.php/Special:WhatLinksHere/Template:Stub "Special:WhatLinksHere/Template:Stub") and expand [incomplete](/index.php/Special:WhatLinksHere/Template:Expansion "Special:WhatLinksHere/Template:Expansion") or [poorly-written](/index.php/Special:WhatLinksHere/Template:Poor_writing "Special:WhatLinksHere/Template:Poor writing") articles.
*   Correct [inaccurate](/index.php/Special:WhatLinksHere/Template:Accuracy "Special:WhatLinksHere/Template:Accuracy") or [outdated](/index.php/Special:WhatLinksHere/Template:Out_of_date "Special:WhatLinksHere/Template:Out of date") content, spelling, grammar, language, and [style](/index.php/Help:Style "Help:Style").
*   Update the [FAQ](/index.php/FAQ "FAQ") with relevant questions from the forum and remove obsolete questions.

### Non-Arch users

Non-Arch users are welcome to contribute; in fact anyone can register an account. They should, however, be confident that any edits also apply to Arch, avoiding comments specific to other distributions. For example, a Fedora user contributing to the [systemd](/index.php/Systemd "Systemd") page would be fine, but mentioning that the newly added content works on Fedora would be edited out as irrelevant.

## Maintaining

*   Help patrolling the [Recent Changes](/index.php/Special:RecentChanges "Special:RecentChanges"), reporting and fixing [questionable edits](/index.php/ArchWiki:Reports "ArchWiki:Reports").
*   Flag articles with appropriate [article status templates](/index.php/Help:Template#Article_status_templates "Help:Template"), like `{{Deletion}}`, `{{Out of date}}`, `{{Accuracy}}`, etc.
*   Add your favorite articles to your watchlist and protect them against counter-productive edits ([#The most important task](#The_most_important_task)).
*   Participate in discussions in the various talk pages: most users will be interested in following the most recent posts to generic discussions at [this link](https://wiki.archlinux.org/index.php?namespace=1&title=Special%3ARecentChanges). Maintenance-specific posts are instead listed in [[1]](https://wiki.archlinux.org/index.php?namespace=13&title=Special%3ARecentChanges), [[2]](https://wiki.archlinux.org/index.php?namespace=11&title=Special%3ARecentChanges), [[3]](https://wiki.archlinux.org/index.php?namespace=5&title=Special%3ARecentChanges) and [[4]](https://wiki.archlinux.org/index.php?namespace=15&title=Special%3ARecentChanges); furthermore, [ArchWiki:Requests](/index.php/ArchWiki:Requests "ArchWiki:Requests") is used as a talk page despite its namespace.

## Organizing

Sorting, categorizing, and moving articles around has become a major task for all wiki maintainers implementing and improving the [category tree](/index.php/Table_of_contents "Table of contents").

*   Reduce and [combine](/index.php/Special:WhatLinksHere/Template:Merge "Special:WhatLinksHere/Template:Merge") duplicate pages.
*   Improve wiki [navigation](/index.php/Table_of_contents "Table of contents").
*   Categorize [uncategorized pages](/index.php/Special:UncategorizedPages "Special:UncategorizedPages"), [uncategorized categories](/index.php/Special:UncategorizedCategories "Special:UncategorizedCategories") and [wanted categories](/index.php/Special:WantedCategories "Special:WantedCategories"). See [Help:Style#Categories](/index.php/Help:Style#Categories "Help:Style") and [Help:Style#Category pages](/index.php/Help:Style#Category_pages "Help:Style").
*   Fix [broken](/index.php/Special:BrokenRedirects "Special:BrokenRedirects") and [double](/index.php/Special:DoubleRedirects "Special:DoubleRedirects") redirects.
*   See [Special:SpecialPages](/index.php/Special:SpecialPages "Special:SpecialPages") for other useful cleanup tools.

## Translating

[Add](/index.php/Special:WhatLinksHere/Template:Translateme "Special:WhatLinksHere/Template:Translateme") or [improve](/index.php/Special:WhatLinksHere/Template:Bad_translation "Special:WhatLinksHere/Template:Bad translation") translations; ensure that translations are in sync with each other. Some languages have started collaboration projects (see list below) to efficiently organize the translation of the articles. Please consider joining your language's Translation Team or at least informing it when you are starting translating an article.

*   [ArchWiki Translation Team](/index.php/ArchWiki_Translation_Team "ArchWiki Translation Team")
*   [ArchWiki Translation Team (Español)](/index.php/ArchWiki_Translation_Team_(Espa%C3%B1ol) "ArchWiki Translation Team (Español)")
*   [ArchWiki Translation Team (Hrvatski)](/index.php/ArchWiki_Translation_Team_(Hrvatski) "ArchWiki Translation Team (Hrvatski)")
*   [ArchWiki Translation Team (Italiano)](/index.php/ArchWiki_Translation_Team_(Italiano) "ArchWiki Translation Team (Italiano)")
*   [ArchWiki Translation Team (Polski)](/index.php/ArchWiki_Translation_Team_(Polski) "ArchWiki Translation Team (Polski)")
*   [ArchWiki Translation Team (Português)](/index.php/ArchWiki_Translation_Team_(Portugu%C3%AAs) "ArchWiki Translation Team (Português)")
*   [ArchWiki Translation Team (Русский)](/index.php/ArchWiki_Translation_Team_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "ArchWiki Translation Team (Русский)")
*   [ArchWiki Translation Team (日本語)](/index.php/ArchWiki_Translation_Team_(%E6%97%A5%E6%9C%AC%E8%AA%9E) "ArchWiki Translation Team (日本語)")
*   [ArchWiki Translation Team (简体中文)](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")
*   [ArchWiki Translation Team (Ελληνικά)](/index.php/ArchWiki_Translation_Team_(%CE%95%CE%BB%CE%BB%CE%B7%CE%BD%CE%B9%CE%BA%CE%AC) "ArchWiki Translation Team (Ελληνικά)")
*   [ArchWiki Translation Team (Català)](/index.php/ArchWiki_Translation_Team_(Catal%C3%A0) "ArchWiki Translation Team (Català)")

Some languages use external wiki, they may require different steps for translation. [Help:i18n](/index.php/Help:I18n "Help:I18n") has a list of external wikis.

### Special messages translation

There are some special messages used in Arch Wiki, please provide their translation for your language in the following link:

*   Also in (Message in Categories tree): Add translation [here](/index.php/Talk:Table_of_contents#.22also_in.22_translations "Talk:Table of contents")
*   Talkpagetext : Add translation [here](/index.php/MediaWiki_talk:Talkpagetext#Talkpagetext_translation "MediaWiki talk:Talkpagetext")

## Brainstorming

If unsure where to begin, or you feel awkward about editing other people's work, you may also contribute by posting ideas and suggestions at [Forum & Wiki discussion](https://bbs.archlinux.org/viewforum.php?id=13) section of the [Arch Linux Forums](https://bbs.archlinux.org/).

## Back-end maintenance

Use the [Arch Linux Bugtracker](https://bugs.archlinux.org/) to report bugs and contribute fixes and improvements to the MediaWiki codebase. See the [list of reported bugs](https://bugs.archlinux.org/index.php?string={wiki}&project=0) for the ArchWiki back-end.

## Complaining

If you have any _generic_ negative remarks or complaints about how the wiki is moderated or administered, please leave a message in [ArchWiki talk:Administrators](/index.php/ArchWiki_talk:Administrators "ArchWiki talk:Administrators"). Of course it should not be necessary to state that it is indeed possible to complain about something using a civil and respectful tone :) For complaints regarding _specific_ edits or articles, please use a more appropriate talk page.

Retrieved from "[https://wiki.archlinux.org/index.php?title=ArchWiki:Contributing&oldid=396525](https://wiki.archlinux.org/index.php?title=ArchWiki:Contributing&oldid=396525)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [ArchWiki](/index.php/Category:ArchWiki "Category:ArchWiki")