# Help:Editing

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

Related articles

*   [ArchWiki:About](/index.php/ArchWiki:About "ArchWiki:About")
*   [Help:Cheatsheet](/index.php/Help:Cheatsheet "Help:Cheatsheet")
*   [Help:Style](/index.php/Help:Style "Help:Style")
*   [Help:Reading](/index.php/Help:Reading "Help:Reading")
*   [Help:Template](/index.php/Help:Template "Help:Template")
*   [Help:Discussion](/index.php/Help:Discussion "Help:Discussion")
*   [ArchWiki:Sandbox](/index.php/ArchWiki:Sandbox "ArchWiki:Sandbox")
*   [Wiki Monkey](/index.php/Wiki_Monkey "Wiki Monkey")

ArchWiki is powered by [MediaWiki](https://www.mediawiki.org/wiki/MediaWiki), a free software wiki package written in PHP, originally designed for use on Wikipedia. More in-depth help can be found at [Help:Contents on MediaWiki](https://www.mediawiki.org/wiki/Help:Contents) and [Help:Contents on Wikipedia](https://en.wikipedia.org/wiki/Help:Contents "wikipedia:Help:Contents").

This is a short tutorial about editing the [ArchWiki](/index.php/ArchWiki:About "ArchWiki:About"). Before editing or creating pages, users are encouraged to familiarize themselves with the general tone, layout, and style of existing articles. An effort should be made to maintain a level of consistency throughout the wiki. See [Help:Reading](/index.php/Help:Reading "Help:Reading") for an overview of common stylistic conventions. See [Help:Style](/index.php/Help:Style "Help:Style") for more detail.

You must be logged-in to edit pages. Visit [Special:UserLogin](/index.php/Special:UserLogin "Special:UserLogin") to log in or create an account. To experiment with editing, please use the [sandbox](/index.php/Sandbox "Sandbox"). For an overview of wiki markup, see [Help:Cheatsheet](/index.php/Help:Cheatsheet "Help:Cheatsheet"). For wiki tasks, see [ArchWiki:Contributing](/index.php/ArchWiki:Contributing "ArchWiki:Contributing").

## Contents

*   [1 Editing](#Editing)
    *   [1.1 Reverting edits](#Reverting_edits)
*   [2 Creating pages](#Creating_pages)
*   [3 Formatting](#Formatting)
    *   [3.1 Headings and subheadings](#Headings_and_subheadings)
    *   [3.2 Line breaks](#Line_breaks)
    *   [3.3 Bold and italics](#Bold_and_italics)
    *   [3.4 Strike-out](#Strike-out)
    *   [3.5 Indenting](#Indenting)
    *   [3.6 Lists](#Lists)
        *   [3.6.1 Bullet points](#Bullet_points)
        *   [3.6.2 Numbered lists](#Numbered_lists)
        *   [3.6.3 Definition lists](#Definition_lists)
    *   [3.7 Code](#Code)
    *   [3.8 Tables](#Tables)
*   [4 Links](#Links)
    *   [4.1 Internal links](#Internal_links)
        *   [4.1.1 Links to sections of a document](#Links_to_sections_of_a_document)
        *   [4.1.2 Pipe trick](#Pipe_trick)
    *   [4.2 Interlanguage links](#Interlanguage_links)
    *   [4.3 Interwiki links](#Interwiki_links)
    *   [4.4 External links](#External_links)
*   [5 Redirects](#Redirects)
*   [6 Wiki variables, magic words, and templates](#Wiki_variables.2C_magic_words.2C_and_templates)

## Editing

To begin editing a page, click the **edit** tab at the top of the page. Alternatively, users may edit a specific section of an article by clicking the **edit** link to the right of the section heading. The _Editing_ page will be displayed, which consists of the following elements:

*   Edit toolbar (optional)
*   Edit box
*   Edit summary box
*   _Save page_, _Show preview_, _Show changes_, and _Cancel_ links

The edit box will contain the **wikitext** (the editable source code from which the server produces the web page) for the current revision of the page or section. To perform an edit:

1.  Modify the wikitext as needed (see [#Formatting](#Formatting) below for details).
2.  Explain the edit in the **Summary** box (e.g. "fixed typo" or "added info on xyz" (see [Help:Edit summary](https://en.wikipedia.org/wiki/Help:Edit_summary "wikipedia:Help:Edit summary") for details)).

    **Note:** **All edits should be accompanied by a descriptive summary.** The summary allows administrators and other maintainers to easily identify controversial edits and vandalism.

3.  Use the **Show preview** button to facilitate proofreading and verify formatting before saving.
4.  Mark the edit as [minor](https://en.wikipedia.org/wiki/Wikipedia:Minor_edit "wikipedia:Wikipedia:Minor edit") by checking the **This is a minor edit** box if the edit is superficial and indisputable.
5.  Save changes by clicking **Save page**. If unsatisfied, click **Cancel** instead (or repeat the process until satisfied).

**Note:**

*   If you are not going to use an external editor like [vim](/index.php/Vim "Vim"), you may want to consider using [wikEd](https://secure.wikimedia.org/wikipedia/en/wiki/User:Cacycle/wikEd), which adds syntax highlighting, regex search and replace and other nice features to the standard MediaWiki editor. The greasemonkey script works flawlessly with the ArchWiki. Remember to always double-check any automated tasks!
*   Articles should **not** be signed because they are _shared_ works; one editor should not be singled out above others.

### Reverting edits

If a page was edited incorrectly, the following procedures describe how to revert an article to a previous version. To revert a single edit:

1.  Click the **history** tab at the top of the page to be modified (beside the **edit** tab). A list of revisions is displayed.
2.  Click the **undo** link to the right of the unwanted edit. An edit preview is displayed, showing the current revision on the left and the text to be saved on the right.
3.  Write the reason why you are undoing this edit to the edit summary field.
4.  If satisfied, click the **Save page** button at the bottom of the page.

The wiki page should now be back in its original state.

Occasionally, it is necessary to revert several last edits at once. To revert an article to a previous version:

1.  Click the **history** tab at the top of the page to be modified (beside the **edit** tab). A list of revisions is displayed.
2.  View the desired revision (i.e. the last _good_ version) by clicking on the appropriate timestamp. That revision is displayed.
3.  Click the **edit** tab at the top of the page. A warning is displayed: **You are editing an out-of-date revision of this page.**
4.  Write the revision timestamp (displayed at the top of page) and a reason why you are reverting page state to the edit summary field.
5.  If satisfied, simply click the **Save page** button to revert to this version.

**Note:** **Avoid combining an undo and an edit!** Revert the edit first, then make additional changes; do not edit the revision preview.

## Creating pages

Before creating a new page, please consider the following:

1.  _Is your topic relevant to Arch Linux?_ Irrelevant or unhelpful articles will be deleted.
2.  _Is your topic of interest to others?_ Consider not only what you wish to write about, but also what others may wish to read. Personal notes belong on your _user_ page.
3.  _Is your topic worthy of a new page?_ Search the wiki for similar articles. If they exist, consider improving or adding a section to an existing article instead.
4.  _Will your contribution be significant?_ Avoid creating stubs unless planning to expand them shortly thereafter.

Creating a new page requires selection of a descriptive **title** and an appropriate **category**.

Please read [Help:Article naming guidelines](/index.php/Help:Article_naming_guidelines "Help:Article naming guidelines") and [Help:Style#Title](/index.php/Help:Style#Title "Help:Style") for article naming advice. Do not include "Arch Linux" or variations in page titles. This is the Arch Linux wiki; it is assumed that articles will be related to Arch Linux (e.g., "Installing Openbox"; not "Installing Openbox in Arch Linux").

Visit the [Table of contents](/index.php/Table_of_contents "Table of contents") to help choose an appropriate category. Articles may belong to multiple categories.

To add a new page to some category (say "My new page" to "Some category") you need to:

1.  Create a page with your new title by browsing to [https://wiki.archlinux.org/index.php/My_new_page](https://wiki.archlinux.org/index.php/My_new_page) (remember to replace "My_new_page" with the intended title!)
2.  Add `[[Category:Some category]]` to the **top** of your page

**Note:** **Do not create uncategorized pages!** All pages must belong to at least one category. If you cannot find a suitable category, consider creating a new one.

## Formatting

Text formatting is accomplished with wiki markup whenever possible; learning HTML is not necessary. Various templates are also available for common formatting tasks; see [Help:Template](/index.php/Help:Template "Help:Template") for information about templates. The [Help:Cheatsheet](/index.php/Help:Cheatsheet "Help:Cheatsheet") summarizes the most common formatting options.

### Headings and subheadings

Headings and subheadings are an easy way to improve the organization of an article. If you can see distinct topics being discussed, you can break up an article by inserting a heading for each section. See [Help:Style#Section headings](/index.php/Help:Style#Section_headings "Help:Style") and [Help:Effective use of headers](/index.php/Help:Effective_use_of_headers "Help:Effective use of headers") for style information.

Headings must start from second level, and can be created like this:

```
== Second-level heading ==

=== Third-level heading ===

==== Fourth-level heading ====

===== Fifth-level heading =====

====== Sixth-level heading ======

```

**Note:** First-level headings are not allowed, their formatting is reserved for the article title.

If an article has at least four headings, a table of contents (TOC) will be automatically generated. If this is not desired, place `__NOTOC__` in the article. Try creating some headings in the [Sandbox](/index.php/Sandbox "Sandbox") and see the effect on the TOC.

### Line breaks

An empty line is used to start a new paragraph while single line breaks have no effect in regular paragraphs.

The HTML `<br>` tag can be used to manually insert line breaks, but should be avoided. A manual break may be justified with other formatting elements, such as lists.

<table width="79%" class="wikitable">

<tbody>

<tr>

<th scope="col" width="50%">wikitext</th>

<th scope="col" width="50%">rendering</th>

</tr>

<tr>

<td>

```
This sentence
is broken into
three lines.

```

</td>

<td>

This sentence is broken into three lines.

</td>

</tr>

<tr>

<td>

```
This is paragraph number one.

This is paragraph number two.

```

</td>

<td>

This is paragraph number one.

This is paragraph number two.

</td>

</tr>

<tr>

<td>

```
* This point <br> spans multiple lines
* This point
ends the list

```

</td>

<td>

*   This point  
    spans multiple lines
*   This point

ends the list

</td>

</tr>

</tbody>

</table>

See [Help:Style/White space](/index.php/Help:Style/White_space "Help:Style/White space") for information on proper use of whitespace characters.

### Bold and italics

**Bold** and _italics_ are added by surrounding a word or phrase with two, three or five apostrophes (`'`):

<table width="79%" class="wikitable">

<tbody>

<tr>

<th scope="col" width="50%">wikitext</th>

<th scope="col" width="50%">rendering</th>

</tr>

<tr>

<td>

`''italics''`

</td>

<td>

_italics_

</td>

</tr>

<tr>

<td>

`'''bold'''`

</td>

<td>

**bold**

</td>

</tr>

<tr>

<td>

`'''''bold and italics'''''`

</td>

<td>

_**bold and italics**_

</td>

</tr>

</tbody>

</table>

### Strike-out

Use strike-out text to show that the text no longer applies or has relevance.

<table width="79%" class="wikitable">

<tbody>

<tr>

<th scope="col" width="50%">wikitext</th>

<th scope="col" width="50%">rendering</th>

</tr>

<tr>

<td> `<s>Strike-out text</s>` </td>

<td>

<s>Strike-out text</s>

</td>

</tr>

</tbody>

</table>

### Indenting

To indent text, place a colon (`:`) at the beginning of a line. The more colons you put, the further indented the text will be. A newline marks the end of the indented paragraph.

<table width="79%" class="wikitable">

<tbody>

<tr>

<th scope="col" width="50%">wikitext</th>

<th scope="col" width="50%">rendering</th>

</tr>

<tr>

<td>

```
This is not indented at all.
:This is indented slightly.
::This is indented more.

```

</td>

<td>

This is not indented at all.

This is indented slightly.

This is indented more.

</td>

</tr>

</tbody>

</table>

**Note:** Use indentation only when strictly necessary to obtain the desired layout. In talk pages, use it to indent replies (see [Help:Discussion](/index.php/Help:Discussion "Help:Discussion")).

### Lists

Remember that wiki syntax does not support multi-line list items; every newline character ends the list item definition. To start a new line inside a list item, use the `<br>` tag. To enter a multi-line code block inside a list item, use [Template:bc](/index.php/Template:Bc "Template:Bc") and escape the content using `<nowiki>` tags. See also [Help:Style/White space](/index.php/Help:Style/White_space "Help:Style/White space") and [Help:Template](/index.php/Help:Template "Help:Template").

#### Bullet points

Bullet points have no apparent order of items.

To insert a bullet, use an asterisk (`*`). Multiple `*`s will increase the level of indentation.

<table width="79%" class="wikitable">

<tbody>

<tr>

<th scope="col" width="50%">wikitext</th>

<th scope="col" width="50%">rendering</th>

</tr>

<tr>

<td>

```
* First item 
* Second item 
** Sub-item
* Third item 

```

</td>

<td>

*   First item
*   Second item
    *   Sub-item
*   Third item

</td>

</tr>

</tbody>

</table>

#### Numbered lists

Numbered lists introduce numbering and thus order the list items. You should generally use unordered lists as long as the order in which items appear is not the primary concern.

To create numbered lists, use the number sign or hash symbol (`#`). Multiple `#`s will increase the level of indentation.

<table width="79%" class="wikitable">

<tbody>

<tr>

<th scope="col" width="50%">wikitext</th>

<th scope="col" width="50%">rendering</th>

</tr>

<tr>

<td>

```
# First item 
# Second item 
## Sub-item
# Third item 

```

</td>

<td>

1.  First item
2.  Second item
    1.  Sub-item
3.  Third item

</td>

</tr>

<tr>

<td>

```
# First item
# Second item
#* Sub-item
# Third item

```

</td>

<td>

1.  First item
2.  Second item
    *   Sub-item
3.  Third item

</td>

</tr>

</tbody>

</table>

#### Definition lists

Definition lists are defined with a leading semicolon (`;`) and a colon (`:`) following the term.

<table width="79%" class="wikitable">

<tbody>

<tr>

<th scope="col" width="50%">wikitext</th>

<th scope="col" width="50%">rendering</th>

</tr>

<tr>

<td>

```
Definition lists:
; Keyboard: Input device with buttons or keys
; Mouse: Pointing device for two-dimensional input
or
; Keyboard
: Input device with buttons or keys
; Mouse
: Pointing device for two-dimensional input

```

</td>

<td>

Definition lists:

Keyboard

Input device with buttons or keys

Mouse

Pointing device for two-dimensional input

or

Keyboard

Input device with buttons or keys

Mouse

Pointing device for two-dimensional input

</td>

</tr>

<tr>

<td>

```
Use additional colons if a definition has multiple definitions:
; Term
: First definition
: Second definition

```

</td>

<td>

Use additional colons if a definition has multiple definitions:

Term

First definition

Second definition

</td>

</tr>

</tbody>

</table>

Definition lists must not be simply used for formatting, see [W3's examples](http://www.w3.org/TR/html4/struct/lists.html#edef-DL).

### Code

To add code to the wiki, use one of the [code formatting templates](/index.php/Help:Template#Code_formatting_templates "Help:Template"). Alternatively, simply start each line with a single whitespace character, for example:

```
 $ echo Hello World

```

See also [Help:Style#Code formatting](/index.php/Help:Style#Code_formatting "Help:Style").

### Tables

**Tip:** See [Mediawiki Tables Generator](http://www.tablesgenerator.com/mediawiki_tables) to automatically generate tables.

Used effectively, tables can help organize and summarize swaths of data. For advanced table syntax and formatting, see [Help:Table](https://en.wikipedia.org/wiki/Help:Table "wikipedia:Help:Table").

<table width="79%" class="wikitable">

<tbody>

<tr>

<th scope="col" width="50%">wikitext</th>

<th scope="col" width="50%">rendering</th>

</tr>

<tr>

<td>

```
{| class="wikitable"
|+ Tabular data
! Distro !! Color
|-
| Arch || Blue
|-
| Gentoo || Purple
|-
| Ubuntu || Orange
|}

```

</td>

<td>

<table class="wikitable"><caption>Tabular data</caption>

<tbody>

<tr>

<th>Distro</th>

<th>Color</th>

</tr>

<tr>

<td>Arch</td>

<td>Blue</td>

</tr>

<tr>

<td>Gentoo</td>

<td>Purple</td>

</tr>

<tr>

<td>Ubuntu</td>

<td>Orange</td>

</tr>

</tbody>

</table>

</td>

</tr>

<tr>

<td>

```
{| class="wikitable"
! Filesystem !! Size !! Used !! Avail !! Use% !! Mounted on
|-
| rootfs || 922G || 463G || 413G || 53% || /
|-
| /dev || 1.9G || 0 || 1.9G || 0% || /dev
|}
```

</td>

<td>

<table class="wikitable">

<tbody>

<tr>

<th>Filesystem</th>

<th>Size</th>

<th>Used</th>

<th>Avail</th>

<th>Use%</th>

<th>Mounted on</th>

</tr>

<tr>

<td>rootfs</td>

<td>922G</td>

<td>463G</td>

<td>413G</td>

<td>53%</td>

<td>/</td>

</tr>

<tr>

<td>/dev</td>

<td>1.9G</td>

<td>0</td>

<td>1.9G</td>

<td>0%</td>

<td>/dev</td>

</tr>

</tbody>

</table>

</td>

</tr>

</tbody>

</table>

## Links

Links are essential to help readers navigate the site. In general, editors should ensure that every article contains _outgoing_ links to other articles (avoid [dead-end pages](/index.php/Special:DeadendPages "Special:DeadendPages")) and is referenced by _incoming_ links from other articles (the [what links here](/index.php/Special:WhatLinksHere "Special:WhatLinksHere") special page can be used to display incoming links).

### Internal links

You can extensively cross-reference wiki pages using internal links. You can add links to existing titles, and also to titles you think ought to exist in future.

To make a link to another page on the same wiki, just put the title in double square brackets.

For example, if you want to make a link to, say, the [pacman](/index.php/Pacman "Pacman") article, use:

```
[[pacman]]

```

If you want to use words other than the article title as the text of the link, you can add an alternative name after the pipe "|" divider (`Shift` + `\` on English-layout and similar keyboards).

For example:

```
The [[ArchWiki:About|ArchWiki]] is the primary documentation source for Arch Linux. 

```

...is rendered as:

The [ArchWiki](/index.php/ArchWiki:About "ArchWiki:About") is the primary documentation source for Arch Linux.

When you want to use the plural of an article title (or add any other suffix) for your link, you can add the extra letters directly outside the double square brackets.

For example:

```
makepkg is used in conjunction with [[PKGBUILD]]s.

```

...is rendered as:

makepkg is used in conjunction with [PKGBUILDs](/index.php/PKGBUILD "PKGBUILD").

#### Links to sections of a document

To create a link to a section of a document, simply add a `#` followed by the section's heading.

For example:

```
[[Help:Editing#Links to sections of a document]]

```

...is rendered as:

[Help:Editing#Links to sections of a document](/index.php/Help:Editing#Links_to_sections_of_a_document "Help:Editing")

**Tip:** If linking to a section within the same page, the page name can be omitted (e.g. `[[#Links to sections of a document]]`). Do not needlessly reformat same-page section links to hide the anchor symbol (e.g. `[[#Links to sections of a document|Links to sections of a document]]`).

#### Pipe trick

In some cases, it is possible to use the [pipe trick](https://en.wikipedia.org/wiki/Help:Pipe_trick "wikipedia:Help:Pipe trick") to save writing the label of wiki links. The most important cases usable on ArchWiki are:

1.  In article titles, it allows to hide the language suffix. For example, `[[Main Page (Česky)|]]` is turned into [Main Page](/index.php/Main_Page_(%C4%8Cesky) "Main Page (Česky)").
2.  In links to different namespace or wiki, the pipe trick hides the prefix. For example, `[[ArchWiki:About|]]` is turned into [About](/index.php/ArchWiki:About "ArchWiki:About") and `[[wikipedia:Help:Pipe trick|]]` is turned into [Help:Pipe trick](https://en.wikipedia.org/wiki/Help:Pipe_trick "wikipedia:Help:Pipe trick").

When the page is saved, the pipe trick will automatically generate the alternative text for the link and change the wikitext accordingly.

### Interlanguage links

See [Help:i18n#Interlanguage links](/index.php/Help:I18n#Interlanguage_links "Help:I18n")

### Interwiki links

So-called _interwiki links_ can be used to easily link to articles in other external Wikis, like Wikipedia for example. The syntax for this link type is the wiki name followed by a colon and the article you want to link to enclosed in double square brackets.

If you want to create link to the [Wikipedia:Arch Linux](https://en.wikipedia.org/wiki/Arch_Linux "wikipedia:Arch Linux") article you can use the following:

```
[[Wikipedia:Arch Linux]]

```

Or you can create a piped link with an alternate link label to the [Arch Linux Wikipedia article](https://en.wikipedia.org/wiki/Arch_Linux "wikipedia:Arch Linux"):

```
[[Wikipedia:Arch Linux|Arch Linux Wikipedia article]]

```

**Note:** Using a piped link with an alternative link label should be reserved for abbreviating longer URLs.

See: [Wikipedia:Interwiki links](https://en.wikipedia.org/wiki/Interwiki_links "wikipedia:Interwiki links")

The list of all interwiki links working on ArchWiki can be viewed [here](https://wiki.archlinux.org/api.php?action=query&meta=siteinfo&siprop=interwikimap).

**Tip:** By default, all interwiki links to pages in Wikipedia are considered as a links to English pages. If you want to create a link to a page on some other language, you should add language prefix to the name of page. For example, to create a link to Russian page, prefix its name with `ru`:

```
[[Wikipedia:ru:Arch Linux]]

```

result: [Wikipedia:ru:Arch Linux](https://en.wikipedia.org/wiki/ru:Arch_Linux "wikipedia:ru:Arch Linux").

Note that it depends on the [interwiki configuration](/index.php/ArchWiki_talk:Administrators#Interwiki "ArchWiki talk:Administrators") for the target wiki, so it does not work on every wiki. It works for Wikipedia though.

### External links

If you want to link to an external site, just type the full URL for the page you want to link to.

```
http://www.google.com/

```

It is often more useful to make the link display something other than the URL, so use one square bracket at each end, with the alternative title after the address separated by a **space** (_not_ a pipe). So if you want the link to appear as [Google search engine](http://www.google.com/), just type:

```
[http://www.google.com/ Google search engine]

```

**Note:** If linking to another ArchWiki or Wikipedia page, **use [#Internal links](#Internal_links) or [#Interwiki links](#Interwiki_links) rather than external links!** That is, if your link starts with [https://wiki.archlinux.org/](https://wiki.archlinux.org/) **use an internal link;** if your link starts with [http://en.wikipedia.org/](http://en.wikipedia.org/) **use an interwiki link!**

## Redirects

[![Tango-view-fullscreen.png](/images/3/38/Tango-view-fullscreen.png)](/index.php/File:Tango-view-fullscreen.png)

[![Tango-view-fullscreen.png](/images/3/38/Tango-view-fullscreen.png)](/index.php/File:Tango-view-fullscreen.png)

**This article or section needs expansion.**

**Reason:** Should be split into subsections to clearly describe 1) what is a redirect, 2) when to redirect a page, 3) how to redirect a page. (Discuss in [Help talk:Editing#](https://wiki.archlinux.org/index.php/Help_talk:Editing))

To redirect automatically from one page to another, add `#REDIRECT` and an internal link to the page to be redirected to at the beginning of a page.

For example, you could redirect from "Cats" to "Cat":

```
#REDIRECT [[Cat]]

```

Thus, anyone typing either version in the search box will automatically go to "Cat".

Note that redirects are resolved internally by the server and will not make it any slower to open an article.

See also [Help:Procedures#Deal with talk pages after redirecting a page to another](/index.php/Help:Procedures#Deal_with_talk_pages_after_redirecting_a_page_to_another "Help:Procedures").

Note that redirecting an existing page to another can create [double redirects](/index.php/Special:DoubleRedirects "Special:DoubleRedirects"): see [Help:Procedures#Fix double redirects](/index.php/Help:Procedures#Fix_double_redirects "Help:Procedures") for fixing them.

## Wiki variables, magic words, and templates

MediaWiki recognizes certain special strings within an article that alter standard behavior. For example, adding the word `__NOTOC__` anywhere in an article will prevent generation of a table of contents. Similarly, the word `__TOC__` can be used to alter the default position of the table of contents. See [Help:Magic words](https://www.mediawiki.org/wiki/Help:Magic_words "mw:Help:Magic words") for details.

Templates and variables are predefined portions of wikitext that can be inserted into an article to aid in formatting content.

[Variables](https://www.mediawiki.org/wiki/Help:Magic_words#Variables "mw:Help:Magic words") are defined by the system and can be used to display information about the current page, wiki, or date. For example, use `{{SITENAME}}` to display the wiki's site name (here it displayed as "ArchWiki"). To set an alternate title header for the current page, another wiki variable can be used: `{{DISPLAYTITLE:New Title}}`. (But it's very restricted: you are only allowed to change first letter to lowercase and replace spaces with underscores — normalized title string must match with real page name, otherwise it will not work; use `{{Lowercase title}}` template to display first letter of title in lower case).

Templates, on the other hand, are user-defined. The content of _any_ page can be included in another page by adding `{{Namespace:Page Name}}` to an article, but this is rarely used with pages outside the _Template_ namespace. (If the namespace is omitted, _Template_ is assumed.) For example, [Template:Note](/index.php/Template:Note "Template:Note"), which can be included in an article with the following wikitext:

```
{{Note|This is a note.}}

```

...is rendered as:

**Note:** This is a note.

See [Help:Template](/index.php/Help:Template "Help:Template") for more information.

Retrieved from "[https://wiki.archlinux.org/index.php?title=Help:Editing&oldid=410138](https://wiki.archlinux.org/index.php?title=Help:Editing&oldid=410138)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [Help](/index.php/Category:Help "Category:Help")