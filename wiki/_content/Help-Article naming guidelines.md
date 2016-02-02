# Help:Article naming guidelines

Article naming is one of the most important tasks for wiki writers and editors. This article is a complete guideline on choosing appropriate article names, and also presents ArchWiki writers and editors with some issues to consider when naming their articles.

## Contents

*   [1 About article names](#About_article_names)
*   [2 Descriptive names](#Descriptive_names)
    *   [2.1 Example](#Example)
*   [3 Allowing for article enhancement](#Allowing_for_article_enhancement)
    *   [3.1 Example](#Example_2)
*   [4 Shorten article names](#Shorten_article_names)
    *   [4.1 Avoid using question form](#Avoid_using_question_form)
    *   [4.2 Rewording long parts](#Rewording_long_parts)
    *   [4.3 Avoid fancy words](#Avoid_fancy_words)
    *   [4.4 Deviating from formal technical expressions](#Deviating_from_formal_technical_expressions)
    *   [4.5 Review the result](#Review_the_result)
*   [5 Multi-language articles](#Multi-language_articles)
    *   [5.1 Example](#Example_3)

## About article names

Article names serve two purposes. They are identifiers of the wiki content on the ArchWiki site. Also, they are means by which readers identify the content. Therefore, an article name has to be unique and descriptive.

Sometimes, article names reflect the _type_ of article content, and also offer additional information like language in which the article was written.

## Descriptive names

**Names should be as specific as possible, and they should reflect the article scope.**

Documentation projects are seldom like software/hardware reviews commonly seen in newspapers and news sites. Documentation is usually read when some problem arises, or some other specific need has to be met. Therefore, quick identification of those needs and swift solution is of utmost importance. For improved readability and faster access to information, article names (and, therefore, their titles) should be as descriptive and specific as the article scope permits.

### Example

Titles like "Boost pacman" may be misleading for most readers. Some of the readers may be looking to boost _some aspect_ of pacman, and that aspect may not necessarily be the aspect described in the article. Therefore, the article name must be as specific as possible without being too long to quickly scan. Such an article may be renamed to read "How to improve pacman download speed using wget, snarf, and lftp".

## Allowing for article enhancement

**Names should be general enough to allow for future enhancement of the article contents.**

In order to allow room for future edits and enhancements, an article's name sometimes needs to be less specific. Of course, making article names less specific just for the sake of shortening it is not a good idea. On the other hand, if you think you have covered all the bases, and that no future edits will enhance the article's _scope_, make your article's name as specific as possible.

### Example

Let us go back to the previous example. The new title of the article is "Improve pacman download speed using wget, snarf, and lftp". However, some day, new download managers may emerge that would replace or become an alternative to wget, snarf, and/or lftp. This calls for a more generic title, something like: "How to improve pacman download speed using alternative download managers".

## Shorten article names

**Names should be as short as possible.**

Making article names short is important in order to allow quick scanning of article listings. Many people use the browsing technique when reading wikis, so you do not want to waste their time by writing article names that are miles long. Also, shorter names tend to sound more professional.

Hereinafter, we will use this name as an example: "How to improve pacman download speed using alternative download managers".

We will cover a few techniques that will help us shorten the name. There are probably many more techniques that do not apply to this particular example, but you will still get insight into the _concept_ of title editing.

**Note:** Literal translation of this article may prove to be a challenge for most languages. Please try to find alternative titles that may serve better for your language. Also, other languages may require different techniques than English.

### Avoid using question form

Instead of saying "How to improve", simply say "Improve".

Now compare the two:

*   "_How to improve_ pacman download speed using alternative download managers"
*   "_Improve_ pacman download speed using alternative download managers"

### Rewording long parts

The text "Improve pacman download speed" is rather long. Instead, we will say "Speed up pacman download".

Now compare:

*   "_Improve pacman download speed_ using alternative download managers"
*   "_Speed up pacman download_ using alternative download managers"

### Avoid fancy words

Fancy words (like "alternative" in our example) are not only fancy; they are used less often than ordinary words, and thus tend to be longer. It is well known that words that are used regularly are in most cases shorter, so try to find an ordinary alternative for your words.

Instead of saying "alternative", you may say "other".

Compare the two versions:

*   "Speed up pacman download using _alternative_ download managers"
*   "Speed up pacman download using _other_ download managers"

### Deviating from formal technical expressions

This may be frowned upon by some of the more technically oriented users, but most people would not mind at all. Avoid technical terms if that makes your article names shorter.

Instead of saying "download managers", you may say "downloaders".

Compare:

*   "Speed up pacman download using other _download managers_"
*   "Speed up pacman download using other _downloaders_"

### Review the result

Do not get too excited yet. We still need to review the two titles and see if they still communicate the same meaning.

*   "How to improve pacman download speed using alternative download managers"
*   "Speed up pacman download using other downloaders"

Okay, we see the end result is a much shorter article name, but what about its meaning? Well, it certainly seems like we did a good job. But now we have a different problem. pacman is _not_ a downloader; both "alternative download managers" and "other downloaders" imply that pacman _is_ a downloader, which is not what we want. We need to change the meaning by saying "external downloaders".

Compare:

*   "How to improve pacman download speed using _alternative_ download managers"
*   "Speed up pacman download using _other_ downloaders"
*   "Speed up pacman download using _external_ downloaders"

## Multi-language articles

**Non-English names are required to have a language identifier.**

To facilitate administration and inter-language linking, non-English articles should use titles of the form "Title in English (Language)" where "Language" is the localized spelling of said language. A redirect with a localized title can and should be added for convenience. See [Help:i18n](/index.php/Help:I18n "Help:I18n") for details.

### Example

For example, if you have an article called [pacman](/index.php/Pacman "Pacman"), you would call the Japanese translation [pacman (日本語)](/index.php/Pacman_(%E6%97%A5%E6%9C%AC%E8%AA%9E) "Pacman (日本語)"), and the Serbian translation [pacman (Српски)](/index.php/Pacman_(%D0%A1%D1%80%D0%BF%D1%81%D0%BA%D0%B8) "Pacman (Српски)").

Retrieved from "[https://wiki.archlinux.org/index.php?title=Help:Article_naming_guidelines&oldid=413273](https://wiki.archlinux.org/index.php?title=Help:Article_naming_guidelines&oldid=413273)"