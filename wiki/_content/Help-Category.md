# Help:Category

Every article must be categorized: categories are displayed at the bottom of each article. This HOWTO will explain how to set page category, how to create missing categories pages and how to move a page to a different category. For the related style rules, see [Help:Style](/index.php/Help:Style "Help:Style").

Articles and categories used as examples in this article are not real. If you want to practice moving while reading this HOWTO, find a _real_ page you want to move.

**Note:** Everything that is discussed in this article applies to categories themselves in quite the same way (i.e. categories can also be categorized).

## Contents

*   [1 Set page category](#Set_page_category)
*   [2 Create new category page](#Create_new_category_page)
*   [3 Move a page into a different category](#Move_a_page_into_a_different_category)
*   [4 i18n category name](#i18n_category_name)
*   [5 Category list](#Category_list)

## Set page category

Click "edit" at the top of the page. Add the following to the beginning of the text:

```
[[Category:Some Category]]

```

Please try to use existing categories when possible: you can find the whole category tree at [Table of contents](/index.php/Table_of_contents "Table of contents"). Only if there is no suitable category for your new article, do save the page with the non-existent category name, but then follow [#Create new category page](#Create_new_category_page).

## Create new category page

After you have saved the page, you will see a "Category: Some Category" link at the bottom of the article. If this category does not exist it will be highlighted in red. Click the red link to go to the newly created category.

Set it to be a sub-category of an existing parent category:

```
[[Category:Parent Category]]

```

Finally save the category page.

If you think the new category needs a parent that does not exist yet either, please open a discussion in the new category's talk page instead of creating a whole new tree of categories by yourself.

## Move a page into a different category

To move a page into a category, edit the page's `[[Category:Some category]]` line.

For example, let us move a fictional page "ArchWiki Tutorial (Magyar)" to an appropriate fictional category. (Moving to existing categories is basically the same as moving to non-existing categories.)

Click "edit" at the top of the page. Find the following line at the beginning of the text:

```
[[Category:Help]]

```

change it to:

```
[[Category:Help (Magyar)]]

```

Save the page by clicking the "Save page" button just below the edit box.

## i18n category name

Category titles follow the same rules described in [Help:I18n#Article titles](/index.php/Help:I18n#Article_titles "Help:I18n").

## Category list

To find out more about ArchWiki categories:

*   Examine the [Table of contents](/index.php/Table_of_contents "Table of contents").
*   A full list of categories is [here](/index.php/Special:Categories "Special:Categories").
*   A list of uncategorized categories is [here](/index.php/Special:UncategorizedCategories "Special:UncategorizedCategories").
*   A list of uncategorized articles is [here](/index.php/Special:UncategorizedPages "Special:UncategorizedPages").
*   A list of empty categories is [here](/index.php/Special:UnusedCategories "Special:UnusedCategories").

Retrieved from "[https://wiki.archlinux.org/index.php?title=Help:Category&oldid=364655](https://wiki.archlinux.org/index.php?title=Help:Category&oldid=364655)"