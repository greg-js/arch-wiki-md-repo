## Contents

*   [1 Introduction](#Introduction)
*   [2 Arch Specific](#Arch_Specific)
    *   [2.1 AUR Search](#AUR_Search)
    *   [2.2 BBS Search](#BBS_Search)
    *   [2.3 Bugtracker Search](#Bugtracker_Search)
    *   [2.4 Wiki Search](#Wiki_Search)
*   [3 Web Lookup](#Web_Lookup)
    *   [3.1 Man Page Search](#Man_Page_Search)
    *   [3.2 Whois Search](#Whois_Search)
    *   [3.3 Websters Dictionary](#Websters_Dictionary)
    *   [3.4 Websters Thesaurus](#Websters_Thesaurus)
*   [4 External links](#External_links)

# Introduction

Due to my recent discovery of [Ubiquity](http://labs.mozilla.com/2008/08/introducing-ubiquity/) and MrGreen's suggestion on the [forum](https://bbs.archlinux.org/viewtopic.php?pid=450773), here's a place for collecting Ubiquity commands that people find of interest.

# Arch Specific

**Requires Ubiquity 0.5+**

## AUR Search

```
CmdUtils.CreateCommand({
 names: ["aur-packages"],
 icon: "https://wiki.archlinux.org/favicon.ico",
 description: "Search the AUR for Packages.",
 help:  "Enter a string to search the AUR",
 contributors: ["Mr Green", "deadrabbit"],
 license: "MPL",
 arguments: [{role: 'object', nountype: noun_arb_text}],
 preview: function preview(pblock, args) {
   pblock.innerHTML = "Search the Arch Bugtracker for **" + args.object.html + "**.";
 },
 execute: function execute(args) {
   var before_url = "https://aur.archlinux.org/packages.php?O=0&L=0&C=0&K=";
   var after_url = "&SeB=nd&SB=n&SO=a&PP=25&do_Search=Go";
   Utils.openUrlInBrowser(before_url + args.object.text + after_url);
 }
}); 

```

## BBS Search

```
CmdUtils.CreateCommand({
 names: ["bbs-arch", "arch bbs"],
 icon: "https://wiki.archlinux.org/favicon.ico",
 description: "Search all of archlinux forums",
 help:  "Enter a string to search the archlinux forums",
 contributors: ["Mr Green", "deadrabbit"],
 license: "MPL",
 arguments: [{role: 'object', nountype: noun_arb_text}],
 preview: function preview(pblock, args) {
   pblock.innerHTML = "Search the Arch forums for **" + args.object.html + "**.";
 },
 execute: function execute(args) {
   var before_url = "https://bbs.archlinux.org/search.php?action=search&keywords=";
   var after_url = "&author=&forum=-1&search_in=all&sort_by=0&sort_dir=DESC&show_as=topics&search=Submit"
   Utils.openUrlInBrowser(before_url + args.object.text + after_url);
 }
});

```

## Bugtracker Search

```
CmdUtils.CreateCommand({
 names: ["arch-bugs"],
 icon: "https://wiki.archlinux.org/favicon.ico",
 description: "Search the Arch Bugtracker.",
  help: "Enter a string to search the Arch Bugtracker.",
 contributors: ["Mr Green", "deadrabbit"],
 license: "MPL",
 arguments: [{role: 'object', nountype: noun_arb_text}],
 preview: function preview(pblock, args) {
   pblock.innerHTML = "Search the Arch Bugtracker for **" + args.object.html + "**.";
 },
 execute: function execute(args) {
   var before_url = "https://bugs.archlinux.org/index.php?string=";
   Utils.openUrlInBrowser(before_url + args.object.text);
 }
});

```

## Wiki Search

```
CmdUtils.CreateCommand({
 names: ["awiki", "arch wiki"],
 icon: "https://wiki.archlinux.org/favicon.ico",
 description: "Search all of archlinux wiki",
 help: "Enter a search query",
 contributors: ["Mr Green", "deadrabbit"],
 license: "MPL",
 arguments: [{role: 'object', nountype: noun_arb_text}],
 preview: function preview(pblock, args) {
   pblock.innerHTML = "Search the wiki for **" + args.object.html + "**.";
 },
 execute: function execute(args) {
   Utils.openUrlInBrowser("https://wiki.archlinux.org/index.php/Special:Search?search=" + args.object.text);
 }
});

```

# Web Lookup

## Man Page Search

```
CmdUtils.CreateCommand({
 names: ["man", "man page" ],
 description: "Search man pages",
 help:  "Enter a string to search the man pages",
 contributors: ["Mr Green", "deadrabbit"],
 license: "MPL",
 arguments: [{role: 'object', nountype: noun_arb_text}],
 preview: function preview(pblock, args) {
   pblock.innerHTML = "Search the man pages for **" + args.object.html + "**.";
 },
 execute: function execute(args) {
   var before_url = "http://www.linuxmanpages.com/man1/";
   var after_url = ".1.php"
   Utils.openUrlInBrowser(before_url + args.object.text + after_url);
 }
});   

```

## Whois Search

```
CmdUtils.CreateCommand({
 names: ["whois"],
 description: "whois domain lookup",
 help:  "Enter a domain to query.",
 contributors: ["Mr Green", "deadrabbit"],
 license: "MPL",
 arguments: [{role: 'object', nountype: noun_arb_text}],
 preview: function preview(pblock, args) {
   pblock.innerHTML = "Whois search for **" + args.object.html + "**.";
 },
 execute: function execute(args) {
   var before_url = "http://reports.internic.net/cgi/whois?whois_nic=";
   var after_url = "&type=domain";
   Utils.openUrlInBrowser(before_url + args.object.text + after_url);
 }
});   

```

## Websters Dictionary

**Not updated for Ubiquity 0.5+ yet**

```
CmdUtils.CreateCommand({
  name: "webster-dictionary",
  author: {name: "Timothy Sorbera", email: "tim.sorbera@gmail.com"},
  license: "MPL",
  description: "Searches Webster's Dictionary for your words.",
  takes: {search: noun_arb_text},
  preview: function(pblock, searchText) {
    var html = "Searches Webster's Dictionary for ";
    if (searchText.text) {
      html += searchText.text;
    } else {
      html += "your words.";
    }
    pblock.innerHTML = html;
  },
  icon: "http://www.merriam-webster.com/favicon.ico",
  execute: function(directObject) {
    var searchUrl = "http://www.merriam-webster.com/dictionary/" + directObject.text;
    Utils.openUrlInBrowser(searchUrl);
  }
});

```

## Websters Thesaurus

**Not updated for Ubiquity 0.5+ yet**

```
CmdUtils.CreateCommand({
  name: "webster-thesaurus",
  author: {name: "Timothy Sorbera", email: "tim.sorbera@gmail.com"},
  license: "MPL",
  description: "Searches Webster's Thesaurus for your words.",
  takes: {search: noun_arb_text},
  preview: function(pblock, searchText) {
    var html = "Searches Webster's Thesaurus for ";
    if (searchText.text) {
      html += searchText.text;
    } else {
      html += "your words.";
    }
    pblock.innerHTML = html;
  },
  icon: "http://www.merriam-webster.com/favicon.ico",
  execute: function(directObject) {
    var searchUrl = "http://www.merriam-webster.com/thesaurus/" + directObject.text;
    Utils.openUrlInBrowser(searchUrl);
  }
});

```

# External links

*   [Ubiquity extension](https://ubiquity.mozilla.com/xpi/ubiquity-latest.xpi)
*   [Ubiquity commands on the Mozilla wiki](https://wiki.mozilla.org/Labs/Ubiquity/Commands_In_The_Wild)
*   [The Ubiquity article on The Sysadmin Wiki, featuring Ubiquity commands](http://sysadmin.wikia.com/wiki/Ubiquity)