# Help:Procedures

A collection of check lists to be used when performing complex changes to articles.

## Contents

*   [1 Move a section within the same page](#Move_a_section_within_the_same_page)
*   [2 Split section to a new subpage](#Split_section_to_a_new_subpage)
*   [3 Deal with talk pages after redirecting a page to another](#Deal_with_talk_pages_after_redirecting_a_page_to_another)
*   [4 Fix double redirects](#Fix_double_redirects)
*   [5 Create a new page and its translation](#Create_a_new_page_and_its_translation)
*   [6 Move a discussion to another talk page](#Move_a_discussion_to_another_talk_page)
*   [7 Rename a category](#Rename_a_category)

## Move a section within the same page

1.  Open the article in an editor.
2.  Cut the text to be moved. Do **not** save the page now, i.e. do not perform the move in two edits, the first removing the section and the second pasting it, or in the second edit it will seem that you are the author of the section, especially if the accompanying edit summary is not clear.
3.  Paste the cut text at the new position.
4.  Adapt the heading level if needed, but do **not** make any other adaptations to the content for the moment, otherwise the modifications will not be visible in the resulting edit diff.
5.  Save the page, properly writing the edit summary.
6.  Now you can proceed to editing the section text normally, as required.

## Split section to a new subpage

This procedure is useful when moving a section of an article that has become too long to a subpage of that article.

1.  Open the origin article section in an editor.
2.  Copy the entire section content.
3.  Open the destination subpage in another editor.
4.  Paste the copied content in the destination editor _without_ modifications.
5.  Save the destination subpage with an edit summary like "content split from 'Origin article#Section'", where 'Origin article#Section' is an internal link.
6.  In the origin editor, replace the split content with a link to the destination subpage either leaving the section heading in place, or adding a link to the Related articles box of the article.
7.  Save the origin page with an edit summary like "content moved to 'Destination subpage'" where 'Destination subpage' is an internal link.
8.  Re-open the destination subpage in an editor.
9.  Categorize the destination subpage like the origin article.
10.  Add a link to the origin article at the top, for example "See 'Origin article' for the main article", where 'Origin article' is an internal link.
11.  Adapt the levels of the headings of the new subpage to start from the second level.

    **Tip:** This step can be done automatically with [Wiki Monkey](/index.php/Wiki_Monkey#Special_functions "Wiki Monkey")'s plugin.

12.  Save the destination subpage with a proper edit summary.

Further advanced additional steps:

*   Check and fix any broken links to sections in both the origin and destination pages, and in pages linking to the origin page.

**Tip:** This step can be done automatically with [Wiki Monkey](/index.php/Wiki_Monkey#Special_functions "Wiki Monkey")'s plugin.

## Deal with talk pages after redirecting a page to another

If page _A_ has been [redirected](/index.php/Help:Editing#Redirects "Help:Editing") to page _B_, for example after merging the content of _A_ into page _B_, and _Talk:A_ exists:

*   If _Talk:B_ does not exist, **move** the entire _Talk:A_ to _Talk:B_, letting MediaWiki automatically redirect _Talk:A_ to _Talk:B_.
*   If _Talk:B_ exists:
    1.  [Move](#Move_a_discussion_to_another_talk_page) the still relevant discussions, if any, from _Talk:A_ to _Talk:B_.
    2.  Ensure that the discussions left in _Talk:A_, if any, are [closed](/index.php/Help:Discussion#Closing_a_discussion "Help:Discussion").
        *   If _Talk:A_ hosts discussions that have been closed for less than the period specified in [Help:Discussion#Closing a discussion](/index.php/Help:Discussion#Closing_a_discussion "Help:Discussion"), flag _Talk:A_ with [Template:Redirect](/index.php/Template:Redirect "Template:Redirect"), so that the page will be redirected to _Talk:B_ after the closing period.
        *   Else, immediately redirect _Talk:A_ to _Talk:B_.

## Fix double redirects

1.  Read [this section](/index.php/Help:Editing#Redirects "Help:Editing") to understand what redirects are.
2.  Check out [Special:DoubleRedirects](/index.php/Special:DoubleRedirects "Special:DoubleRedirects") to see if there are any.
3.  For example, if you see `Pastebin Clients (Edit) →‎ Common Applications →‎ List of applications`, it means [Pastebin Clients](/index.php/Pastebin_Clients "Pastebin Clients") redirects to [Common Applications](/index.php/Common_Applications "Common Applications"), and [Common Applications](/index.php/Common_Applications "Common Applications") redirects to [List of applications](/index.php/List_of_applications "List of applications"). Therefore, [Pastebin Clients](/index.php/Pastebin_Clients "Pastebin Clients") is a double redirect.
4.  To fix it, edit [Pastebin Clients](/index.php/Pastebin_Clients "Pastebin Clients") and change `#REDIRECT [[Common Applications]]` to `#REDIRECT [[List of applications]]` to skip the middleman.
5.  Enter an edit summary such as `Fixed double redirect` and save.

**Tip:** This task can be done automatically with [Wiki Monkey](/index.php/Wiki_Monkey#Special_functions "Wiki Monkey")'s plugin.

## Create a new page and its translation

See [ArchWiki Translation Team#Create a new page and its translation](/index.php/ArchWiki_Translation_Team#Create_a_new_page_and_its_translation "ArchWiki Translation Team").

## Move a discussion to another talk page

1.  Copy the discussion text to the destination talk page, making sure to add, between the new heading and the pasted text, a note like:
    _[Moved from **Origin_talk_page#Heading**. -- Signature and timestamp]_
2.  Strike the heading in the origin talk page and replace the content with a note like:
    _[Moved to **Destination_talk_page#Heading**. -- Signature and timestamp]_

## Rename a category

1.  Move the category page the same way as you would move a normal page, ensuring a redirect is created from the old title to the new one. This will only rename the category page itself, the members of the category will not be recategorized.
2.  Recategorize all members of the old category to use the new one.

    **Tip:** This can be done automatically with a [script](https://github.com/lahwaacz/wiki-scripts/blob/master/recategorize-over-redirect.py), which relies on the redirect from the old category to detect the new name and thus it is not limited to changes in capitalization or similar heuristics.

3.  Update all interlanguage links.

    **Tip:** This can be done automatically with a [script](https://github.com/lahwaacz/wiki-scripts/blob/master/update-interlanguage-links.py) or [Wiki Monkey](/index.php/Wiki_Monkey#Page_lists_.28Bot.29 "Wiki Monkey")'s bot plugin.

4.  Update all backlinks of the old category to refer to the new one.

    **Tip:** This can be done automatically by running Wiki Monkey's _RegExp substitution_ plugin on the old category's [Special:WhatLinksHere](/index.php/Special:WhatLinksHere "Special:WhatLinksHere") page, with a substitution like `(\[\[|\{\{Related2?\|):[ _]*[Cc]ategory[ _]*:[ _]*[Oo]ld[ _]name[ _]*(#|\||\]\]|\}\})` -> `$1:Category:New name$2` (assuming the old category name is "Category:Old name").

5.  Mark the old category with [Template:Deletion](/index.php/Template:Deletion "Template:Deletion"), without destroying the redirect (the old category is likely still linked from [Table of contents](/index.php/Table_of_contents "Table of contents")).

    **Tip:** Before deleting the category, make sure that steps 2.-4\. have actually been performed. They can be done later in any order.

Retrieved from "[https://wiki.archlinux.org/index.php?title=Help:Procedures&oldid=414582](https://wiki.archlinux.org/index.php?title=Help:Procedures&oldid=414582)"