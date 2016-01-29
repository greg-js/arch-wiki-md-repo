# Help:Style/White space

< [Help:Style](/index.php/Help:Style "Help:Style")

Related articles

*   [Help:Editing#Line breaks](/index.php/Help:Editing#Line_breaks "Help:Editing")

This article defines the standards for the use of whitespace characters in the source code of articles. The style used in the examples is to be considered an integral part of the rules.

## Contents

*   [1 Generic rules](#Generic_rules)
*   [2 Main, Category, ArchWiki, Help namespaces](#Main.2C_Category.2C_ArchWiki.2C_Help_namespaces)
    *   [2.1 Example](#Example)
*   [3 Talk, *_talk namespaces](#Talk.2C_.2A_talk_namespaces)
    *   [3.1 Example](#Example_2)

## Generic rules

*   Use a single space to separate sentences in the same paragraph (i.e. after period marks).
*   Avoid using multiple blank lines to space out paragraphs or sections.
*   Separate section titles from the `=` characters with a single space character.
*   Separate section headers from section bodies with an empty line.
*   There should be no spaces around template names, template parameters, link titles, and alternative link text.
*   There should be no spaces between [indentation](/index.php/Help:Editing#Indenting "Help:Editing") colons and indented text.
*   Separate [list](/index.php/Help:Editing#Lists "Help:Editing") characters (`*` and `#`) from their items with a space.
*   Individual list items cannot be separated by blank lines, otherwise the wiki parser will start a new list for each item.
*   Separate special blocks (lists, code blocks, [notes](/index.php/Template:Note "Template:Note"), [tips](/index.php/Template:Tip "Template:Tip"), [warnings](/index.php/Template:Warning "Template:Warning") etc.) from normal text with an empty line.

## Main, Category, ArchWiki, Help namespaces

*   Separate categories with single line breaks.
*   Separate interlanguage links with single line breaks.

### Example

```
[[Category:Example A]]
[[Category:Example B]]
[[es:Article]]
[[zh-CN:Article]]
{{Expansion|Example status template}}

{{Related articles start}}
{{Related|Related article A}}
{{Related|Related article B}}
{{Related articles end}}

Example introduction.

== Section 1 ==

Example section body.

=== Section 1.1 ===

Example section body with [[Related article|link]].

== Section 2 ==

=== Section 2.1 ===

Example section body with {{Template|Parameter 1|2=Parameter 2}}.

* List item
** List item
* List item

=== Section 2.2 ===

 Singe-line code example

{{bc|
Multiline code example
1
2
3
}}

{{bc|1=
Multiline code example
1
2
3
}}

{{bc|<nowiki>
Multiline code example
1
2
3
</nowiki>}}

=== Section 2.3 ===

Paragraph text

{{Note|
* first note
* second note
}}

Second paragraph

{{Tip|some useful tip}}

```

## Talk, *_talk namespaces

*   Separate different replies with an empty line.

### Example

```
== Discussion 1 ==

First post, paragraph 1.

First post, paragraph 2.

-- ~~~~

:Reply 1, single paragraph. -- ~~~~

::Reply 2, paragraph 1.
::Reply 2, paragraph 2.
::-- ~~~~

== Discussion 2 ==

First post, single paragraph. -- ~~~~

:Reply 1, paragraph 1.
:Reply 1, paragraph 2.
:-- ~~~~

::Reply 2, single paragraph. -- ~~~~

```

Retrieved from "[https://wiki.archlinux.org/index.php?title=Help:Style/White_space&oldid=357504](https://wiki.archlinux.org/index.php?title=Help:Style/White_space&oldid=357504)"