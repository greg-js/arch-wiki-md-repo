# Help:i18n

This article serves as a comprehensive guideline for ArchWiki [internationalization and localization](https://en.wikipedia.org/wiki/Internationalization_and_localization "wikipedia:Internationalization and localization").

See also [International communities](/index.php/International_communities "International communities").

## Contents

*   [1 Guidelines](#Guidelines)
    *   [1.1 Page titles](#Page_titles)
    *   [1.2 Localized redirects](#Localized_redirects)
    *   [1.3 Interlanguage links](#Interlanguage_links)
        *   [1.3.1 Finding articles with specific interlanguage links](#Finding_articles_with_specific_interlanguage_links)
*   [2 Languages](#Languages)
    *   [2.1 Adding local interlanguage links](#Adding_local_interlanguage_links)
    *   [2.2 Adding external interlanguage links](#Adding_external_interlanguage_links)
    *   [2.3 Moving local languages to external wikis](#Moving_local_languages_to_external_wikis)

## Guidelines

### Page titles

Non-English page titles must be of the form **"Title in English (Language)"** where "Language" is the localized spelling of said language. Note the space between the title and the language tag. For example: [Beginners' Guide (Nederlands)](/index.php/Beginners%27_Guide_(Nederlands) "Beginners' Guide (Nederlands)"). English titles should not include a language tag.

Also note that in case of sub-pages, the language tag still goes at the end, so **"Title (Language)/Sub-page"** is wrong, while **"Title/Sub-page (Language)"** is correct. For example: [PulseAudio/Examples (Italiano)](/index.php/PulseAudio/Examples_(Italiano) "PulseAudio/Examples (Italiano)"). This may seem inconsistent, but it is more practical and safe for bots to detect the language of a page.

The [root categories for every language](/index.php/Category:Languages "Category:Languages") are the only exception to this rule, as they must not repeat the language name in a suffix.

See [#Languages](#Languages) for a list of languages and expected localized spellings.

Rationale:

*   English titles facilitate administration; all [administrators](/index.php/ArchWiki:Administrators "ArchWiki:Administrators") understand English, but may not be multilingual. When browsing [Special:RecentChanges](/index.php/Special:RecentChanges "Special:RecentChanges") and other special pages, admins need to know what is being edited without resorting to external translation programs.
*   Standardized article titles simplify inter-language linking.

### Localized redirects

Localized titles can and should be created, but must redirect to the English-named article as described above. Redirect titles need not include language tags. For example: [Guía para Principiantes](/index.php/Gu%C3%ADa_para_Principiantes "Guía para Principiantes") redirects to [Beginners' Guide (Español)](/index.php/Beginners%27_Guide_(Espa%C3%B1ol) "Beginners' Guide (Español)").

Rationale:

*   Localized titles improve navigability for international readers. Both the internal search feature and external search engines can utilize such redirects.
*   Useful redirects facilitate internal linking.

### Interlanguage links

If an article exists in more than one language, please add interlanguage links at the top of each translation:

```
[[de:Title]]
[[en:Title]]
[[es:Title]]

```

**Note:** Interlanguage links add the suffix mentioned in [#Article titles](#Article_titles) automatically, so the interlanguage link associated to e.g. [Main Page (Dansk)](/index.php/Main_Page_(Dansk) "Main Page (Dansk)") is `[[da:Main Page]]`.

See [#Languages](#Languages) for a list of the available language tags. See [Help:Style#Interlanguage links](/index.php/Help:Style#Interlanguage_links "Help:Style") for usage guidelines.

Rationale:

*   Including inter-language links at the beginning of an article allows international readers to promptly determine whether content is available in their language, and similarly allows translators to ascertain whether an article requires translation.

#### Finding articles with specific interlanguage links

In order to obtain a list of the articles with interlanguage links pointing to a specific title (language backlinks), use:

[https://wiki.archlinux.org/api.php?action=query&list=langbacklinks&lbllimit=500&lblprop=lltitle&lbllang=en&lbltitle=Main%20Page](https://wiki.archlinux.org/api.php?action=query&list=langbacklinks&lbllimit=500&lblprop=lltitle&lbllang=en&lbltitle=Main%20Page)

This example looks for (`[[en:Main Page]]`), but for other links it is enough to change the value of `lbllang` and `lbltitle`.

If you want to obtain a list of the articles using interlanguage links of a specific language, just omit the `lbltitle` key:

[https://wiki.archlinux.org/api.php?action=query&list=langbacklinks&lbllimit=500&lblprop=lltitle&lbllang=de](https://wiki.archlinux.org/api.php?action=query&list=langbacklinks&lbllimit=500&lblprop=lltitle&lbllang=de)

This example uses German (`de`), but for the other languages it is enough to change the value of `lbllang`.

**Note:** This query may not find all redirects using interlanguage links (regulated by [Help:Style#Redirect pages](/index.php/Help:Style#Redirect_pages "Help:Style")): [a search like this](https://wiki.archlinux.org/index.php?title=Special%3ASearch&profile=advanced&limit=500&offset=0&search=%22redirect%20%5B%5Bde%3A%22&fulltext=Search&ns0=1&ns1=1&ns2=1&ns3=1&ns4=1&ns5=1&ns6=1&ns7=1&ns8=1&ns9=1&ns10=1&ns11=1&ns12=1&ns13=1&ns14=1&ns15=1&redirs=1&profile=advanced) should work instead (if you get zero results it means that everything is fine).

Note that API queries are always limited, so if a language has more than 500 backlinks it will be necessary to continue the search adding the `lblcontinue` attribute that appears at the bottom of the list to the query string.

## Languages

The following table lists all languages encountered on the wiki along with related links.

| English name | Localized name | Subtag | Root category | External wiki |
| Arabic | العربية | ar | [Category:العربية](/index.php/Category:%D8%A7%D9%84%D8%B9%D8%B1%D8%A8%D9%8A%D8%A9 "Category:العربية") |
| Bulgarian | Български | bg | [Category:Български](/index.php/Category:%D0%91%D1%8A%D0%BB%D0%B3%D0%B0%D1%80%D1%81%D0%BA%D0%B8 "Category:Български") |
| Catalan | Català | _not supported_ <sup>1</sup> | [Category:Català](/index.php/Category:Catal%C3%A0 "Category:Català") |
| Chinese (Simplified) | 简体中文 | zh-cn | [Category:简体中文](/index.php/Category:%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87 "Category:简体中文") |
| Chinese (Traditional) | 正體中文 | zh-tw | [Category:正體中文](/index.php/Category:%E6%AD%A3%E9%AB%94%E4%B8%AD%E6%96%87 "Category:正體中文") |
| Croatian | Hrvatski | hr | [Category:Hrvatski](/index.php/Category:Hrvatski "Category:Hrvatski") |
| Czech | Česky | cs | [Category:Česky](/index.php/Category:%C4%8Cesky "Category:Česky") |
| Danish | Dansk | da | [Category:Dansk](/index.php/Category:Dansk "Category:Dansk") |
| Dutch | Nederlands | nl | [Category:Nederlands](/index.php/Category:Nederlands "Category:Nederlands") |
| English | English | en | [Category:English](/index.php/Category:English "Category:English") |
| Esperanto | Esperanto | _not supported_ <sup>1</sup> | [Category:Esperanto](/index.php/Category:Esperanto "Category:Esperanto") |
| Finnish | Suomi | fi | [Category:Suomi](/index.php/Category:Suomi "Category:Suomi") | [http://www.archlinux.fi/wiki/](http://www.archlinux.fi/wiki/) |
| French | Français | fr | — | [http://wiki.archlinux.fr/](http://wiki.archlinux.fr/) |
| German | Deutsch | de | — | [https://wiki.archlinux.de/](https://wiki.archlinux.de/) |
| Greek | Ελληνικά | el | [Category:Ελληνικά](/index.php/Category:%CE%95%CE%BB%CE%BB%CE%B7%CE%BD%CE%B9%CE%BA%CE%AC "Category:Ελληνικά") |
| Hebrew | עברית | he | [Category:עברית](/index.php/Category:%D7%A2%D7%91%D7%A8%D7%99%D7%AA "Category:עברית") |
| Hungarian | Magyar | hu | [Category:Magyar](/index.php/Category:Magyar "Category:Magyar") |
| Indonesian | Bahasa Indonesia | id | [Category:Indonesia](/index.php/Category:Indonesia "Category:Indonesia") |
| Italian | Italiano | it | [Category:Italiano](/index.php/Category:Italiano "Category:Italiano") |
| Japanese | 日本語 | ja | — | [https://wiki.archlinuxjp.org/](https://wiki.archlinuxjp.org/) |
| Korean | 한국어 | ko | [Category:한국어](/index.php/Category:%ED%95%9C%EA%B5%AD%EC%96%B4 "Category:한국어") |
| Lithuanian | Lietuviškai | lt | [Category:Lietuviškai](/index.php/Category:Lietuvi%C5%A1kai "Category:Lietuviškai") |
| Norwegian (Bokmål) | Norsk Bokmål | _not supported_ <sup>1</sup> | [Category:Norsk Bokmål](/index.php/Category:Norsk_Bokm%C3%A5l "Category:Norsk Bokmål") |
| Persian | فارسی | fa | — | [http://wiki.archusers.ir/](http://wiki.archusers.ir/) |
| Polish | Polski | pl | [Category:Polski](/index.php/Category:Polski "Category:Polski") |
| Portuguese | Português | pt | [Category:Português](/index.php/Category:Portugu%C3%AAs "Category:Português") |
| Romanian | Română | ro | — | [http://wiki.archlinux.ro/](http://wiki.archlinux.ro/) |
| Russian | Русский | ru | [Category:Русский](/index.php/Category:%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9 "Category:Русский") |
| Serbian | Српски (Srpski) | sr | [Category:Српски](/index.php/Category:%D0%A1%D1%80%D0%BF%D1%81%D0%BA%D0%B8 "Category:Српски") | [http://wiki.archlinux.rs/](http://wiki.archlinux.rs/) |
| Slovak | Slovenský | sk | [Category:Slovenský](/index.php/Category:Slovensk%C3%BD "Category:Slovenský") |
| Spanish | Español | es | [Category:Español](/index.php/Category:Espa%C3%B1ol "Category:Español") |
| Swedish | Svenska | sv | — | [http://wiki.archlinux.se/](http://wiki.archlinux.se/) |
| Thai | ไทย | th | [Category:ไทย](/index.php/Category:%E0%B9%84%E0%B8%97%E0%B8%A2 "Category:ไทย") |
| Turkish | Türkçe | tr | — | [http://archtr.org/wiki/](http://archtr.org/wiki/) |
| Ukrainian | Українська | uk | [Category:Українська](/index.php/Category:%D0%A3%D0%BA%D1%80%D0%B0%D1%97%D0%BD%D1%81%D1%8C%D0%BA%D0%B0 "Category:Українська") |
| Vietnamese | Tiếng Việt | _not supported_ <sup>1</sup> | — | [http://archlinuxvn.tuxfamily.org/](http://archlinuxvn.tuxfamily.org/) |

<sup>1</sup> The _not supported_ note in the "Subtag" field means that interlanguage links for that language are not available. See [#Adding local interlanguage links](#Adding_local_interlanguage_links) and [#Adding external interlanguage links](#Adding_external_interlanguage_links).

Subtags are treated case-insensitively by the MediaWiki backend. By convention, the interlanguage links on ArchWiki should use the lowercase form of the subtag. For information regarding subtags, please see:

*   [http://www.iana.org/assignments/language-subtag-registry](http://www.iana.org/assignments/language-subtag-registry)
*   [http://tools.ietf.org/rfc/bcp/bcp47.txt](http://tools.ietf.org/rfc/bcp/bcp47.txt)
*   [http://rishida.net/utils/subtags/](http://rishida.net/utils/subtags/)

### Adding local interlanguage links

If you want interlanguage links to be enabled for a new language hosted in wiki.archlinux.org, please open a request in [Help talk:i18n](/index.php/Help_talk:I18n "Help talk:I18n"). Note that a minimum number of translated articles will be required by the administrators for the request to be fulfilled. Setting up an external wiki is however always preferable.

### Adding external interlanguage links

If you want interlanguage links to be set for a new or existing language that has set up a separate wiki, please open a request in [Help talk:i18n](/index.php/Help_talk:I18n "Help talk:I18n") or directly contact one of the [ArchWiki:Administrators](/index.php/ArchWiki:Administrators "ArchWiki:Administrators"): the interlanguage links will be set as soon as possible!

### Moving local languages to external wikis

Moving local languages to their own wikis is a very welcome and encouraged thing, which will get all the assistance that is needed. There are two possible procedures:

*   First move _all_ the articles to the external wiki. Once done, update the interlanguage links to point to the new domain, then fix all their target titles with the new ones. Finally, either delete the local articles, or, upon authorization from the [ArchWiki:Maintenance Team](/index.php/ArchWiki:Maintenance_Team "ArchWiki:Maintenance Team"), redirect them to the external wiki using the interlanguage links.
*   Set up temporary interlanguage links (e.g. `[[ja-temp:Title]]`) and use them to redirect the various articles to the external wiki as they are moved _one by one_. Once the move is complete, point the regular interlanguage links (i.e. `[[ja:Title]]`) to the external wiki, and update them all with the new target titles. Next, either delete the local redirects, or, upon authorization from the [ArchWiki:Maintenance Team](/index.php/ArchWiki:Maintenance_Team "ArchWiki:Maintenance Team"), update them to use the regular interlanguage links. Finally, disable the temporary interlanguage links.

Retrieved from "[https://wiki.archlinux.org/index.php?title=Help:I18n&oldid=416062](https://wiki.archlinux.org/index.php?title=Help:I18n&oldid=416062)"