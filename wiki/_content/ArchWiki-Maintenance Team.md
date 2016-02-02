# ArchWiki:Maintenance Team

Related articles

*   [ArchWiki:Administrators](/index.php/ArchWiki:Administrators "ArchWiki:Administrators")
*   [ArchWiki:Maintainers](/index.php/ArchWiki:Maintainers "ArchWiki:Maintainers")
*   [Help:Style](/index.php/Help:Style "Help:Style")
*   [ArchWiki:Requests](/index.php/ArchWiki:Requests "ArchWiki:Requests")
*   [ArchWiki:Tasks](/index.php/ArchWiki:Tasks "ArchWiki:Tasks")

The Maintenance Team is ArchWiki's official group of users whose goal is supervising and fixing the edits that are made every day to the articles in the wiki.

## Contents

*   [1 How to join](#How_to_join)
*   [2 Workflow](#Workflow)
    *   [2.1 Recent changes patrolling](#Recent_changes_patrolling)
    *   [2.2 Report solving](#Report_solving)
*   [3 Common problems and solutions](#Common_problems_and_solutions)
    *   [3.1 Content-related](#Content-related)
    *   [3.2 Style-related](#Style-related)
*   [4 See also](#See_also)

## How to join

Official [Maintainers](/index.php/ArchWiki:Maintainers "ArchWiki:Maintainers") are usually chosen by the [Administrators](/index.php/ArchWiki:Administrators "ArchWiki:Administrators") among the most active and collaborative users of the wiki, and personally invited to participate in the team. You can also explicitly present yourself as a candidate by contacting one of the Administrators. Maintainers belong to a particular group of wiki users with [special rights](/index.php/Special:ListGroupRights "Special:ListGroupRights"). Administrators are implicit members of the team.

Common requisites for becoming a Maintainer are:

*   Familiarity with how this team is organized and how its members work with each other (see [#Workflow](#Workflow)); will to collaborate and discuss with the other Maintainers.
*   Some free time and the commitment to contribute regularly enough.
*   Patience, accuracy and tidiness.
*   Experience in wiki editing and good knowledge of [wiki syntax](/index.php/Help:Editing "Help:Editing").
*   Good knowledge of the structure of the ArchWiki and its [style rules](/index.php/Help:Style "Help:Style").
*   Sufficient knowledge of Arch Linux and the subjects treated in the articles, or willingness to do some research or discuss with the edits' authors when fixing content-related issues.

If you are interested in joining the team, you can start making yourself visible to the community by helping with the [common tasks](/index.php/ArchWiki:Contributing "ArchWiki:Contributing"), in particular contributing to the discussions that take place in the various talk pages.

Once elected, members should add their username to [ArchWiki:Maintainers](/index.php/ArchWiki:Maintainers "ArchWiki:Maintainers") and also add a special tag in their user page: `[[ArchWiki:Maintainers|ArchWiki Maintainer]]`.

## Workflow

The supervision of the edits made to the wiki can be accomplished in two complementary stages: [#Recent changes patrolling](#Recent_changes_patrolling) and [#Report solving](#Report_solving). The former stage is where the problems are found and reported, while the latter is where they are finally processed and solved.

You can engage in one of the two tasks, or even in both if you want, keeping in mind that patrolling the recent changes obviously requires a more constant commitment, while fixing the reports is much more flexible and can be done whenever you find some time.

### Recent changes patrolling

There are two main ways you can patrol the recent changes:

*   Visiting [Special:RecentChanges](/index.php/Special:RecentChanges "Special:RecentChanges") at regular intervals, checking all the edits that have been made since the previous visit.
*   Subscribing to [Special:RecentChanges's Atom feed](https://wiki.archlinux.org/index.php?title=Special:RecentChanges&feed=atom) and checking the edits as soon as you find some time.

For each edit, or group of edits made to the same page, you should assess if it is questionable, according to your experience and knowledge, also taking into account the list of the [most frequent problems](#Common_problems_and_solutions).

*   If you think the edit requires a quick fix that you can perform immediately, just do it.
*   If instead the edit is questionable but you cannot fix it, you should look if it has already been reported in [ArchWiki:Reports](/index.php/ArchWiki:Reports "ArchWiki:Reports"):
    *   If not, add it to the table describing the problem in the _Notes_ field; note that the table distinguishes between _content_ and _style_-related reports with the _Type_ field: if an edit has both content and style problems, mark it as _content_.
        *   As an alternative, you may decide to add the report directly in [ArchWiki talk:Reports](/index.php/ArchWiki_talk:Reports "ArchWiki talk:Reports"), still checking that it is not there yet.
    *   In case the edit has already been reported, see if you can add useful details to the accompanying note or discussion.

**Tip:** Make patrolling easier by taking the following steps:

*   Enable the _Group changes by page in recent changes and watchlist_ setting under _Preferences > Recent changes > Advanced options_.
*   Quickly add reports to [ArchWiki:Reports](/index.php/ArchWiki:Reports "ArchWiki:Reports") with a dedicated script (e.g. [Wiki Monkey](/index.php/Wiki_Monkey "Wiki Monkey")'s _Patrol_ or _Patrol Lite_).
*   Add [ArchWiki:Reports](/index.php/ArchWiki:Reports "ArchWiki:Reports") to your watchlist or subscribe to the [edit history](https://wiki.archlinux.org/index.php?title=ArchWiki:Reports&action=history) and [talk page](https://wiki.archlinux.org/index.php?title=ArchWiki_talk:Reports&action=history) Atom feeds.
*   To follow your watched articles using a feed reader, use the "Atom" link in the left column of your [watchlist](/index.php/Special:Watchlist "Special:Watchlist") page.

### Report solving

[ArchWiki:Reports](/index.php/ArchWiki:Reports "ArchWiki:Reports") is the reference page for addressing maintenance problems. When working there, you should first choose one of the listed reports, also reading the accompanying patrol's note:

*   If you think you can fix the report, just do it and remove the entry from the table. Read also [#Common problems and solutions](#Common_problems_and_solutions).
*   If otherwise you feel it is better to contact the author of the edit, write him a message in his talk page, or send him an email in order to request an explanation or discuss further; then add a discussion in [ArchWiki talk:Reports](/index.php/ArchWiki_talk:Reports "ArchWiki talk:Reports") as a reminder and delete the report from [ArchWiki:Reports](/index.php/ArchWiki:Reports "ArchWiki:Reports").
*   If instead you think the problem deserves a discussion with the other members of the team, start it in [ArchWiki talk:Reports](/index.php/ArchWiki_talk:Reports "ArchWiki talk:Reports") and delete the report from [ArchWiki:Reports](/index.php/ArchWiki:Reports "ArchWiki:Reports").

The problems treated in [ArchWiki talk:Reports](/index.php/ArchWiki_talk:Reports "ArchWiki talk:Reports") will be solved when the related discussions reach definitive solutions.

**Tip:**

*   Prefer trying to fix the oldest reports
*   Prefer fixing content-related over style-related issues.
*   You may consider using an editor assistant (e.g. [Wiki Monkey](/index.php/Wiki_Monkey "Wiki Monkey")'s _Editor_ configuration) in order to solve some common style issues automatically.

## Common problems and solutions

The following are the most common problems that recent changes patrols can find and report, with brief tips for possible fixes.

### Content-related

*   Removal of useful content: undo or contact the author.
*   Unexplained modification or removal of content: contact the author.
*   Major modification (usually in a single bulky edit) without sufficient explanation: contact the author.

### Style-related

*   Signature, credits, personal observations in articles: undo or move to talk page.
*   Start headings from level 1: move all sections up 1 level.
*   Uncategorized new article: add category and fix header.
*   Improper use of templates: fix according to [Help:Style](/index.php/Help:Style "Help:Style").
*   Addition of installation instructions: undo or comply with [Help:Style](/index.php/Help:Style "Help:Style").

## See also

*   [Wikipedia:Recent changes patrol](https://en.wikipedia.org/wiki/Wikipedia:Recent_changes_patrol "wikipedia:Wikipedia:Recent changes patrol")

Retrieved from "[https://wiki.archlinux.org/index.php?title=ArchWiki:Maintenance_Team&oldid=374843](https://wiki.archlinux.org/index.php?title=ArchWiki:Maintenance_Team&oldid=374843)"