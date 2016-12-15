## Contents

*   [1 About](#About)
*   [2 Installation](#Installation)
*   [3 Status](#Status)
*   [4 Implementation plan](#Implementation_plan)
*   [5 First tasks](#First_tasks)
*   [6 Middle tasks](#Middle_tasks)
*   [7 Later tasks](#Later_tasks)
*   [8 SHARD1](#SHARD1)

## About

This is an experimental project to see the feasibility and issues with making a backup of the Internet Archive. This project should be considered to be in an alpha state. To read the original document suggesting the research, click here. Implementation ideas are discussed on this page. If you have (at least) hundreds of gigabytes of disk space, are comfortable with a linux/unix variant, and wish to take part in the project, the information to do so is here. As time progresses, the client that sets up your environment will become easier and more intuitive to use - right now, some things are still unclear or in need of clarification. Join #internetarchive.bak on EFNet (IRC) to get help.

## Installation

To install IA.BAK you first have to install [perl-cgi](https://www.archlinux.org/packages/?name=perl-cgi) and [git](https://www.archlinux.org/packages/?name=git).

Create a directory on the filesystem you want to provide as storage.

Enter that directory and run:

```
$ git clone [https://github.com/ArchiveTeam/IA.BAK](https://github.com/ArchiveTeam/IA.BAK)
$ cd IA.BAK
$ ./iabak

```

## Status

[Graphs of status](http://iabak.archiveteam.org/)

[raw data](http://iabak.archiveteam.org/stats/)

## Implementation plan

For more information, see [http://git-annex.branchable.com/design/iabackup/](http://git-annex.branchable.com/design/iabackup/)

## First tasks

Some first steps to work on:

*   Get a list of files, checksums, and urls. (done)
*   Write a script to generate a git-annex repository with 100k files from the list. (done)
*   Set up a server to serve up the git repos. Any linux system with a few hundred gb of disk and ssh and git-annex installed will do. It needs to accept incoming ssh connections from registered clients, only letting them run git-annex-shell. (done)
*   Put one shard repo on the server to start. (done)
*   Manually register a few clients to start, have them manually download some files, and `git annex sync` their state back to the server. See how it all hangs together. (done)
*   Get that first shard backed up enough to be able to say, "we have successfully backed up 1/1770th of the IA!" (done!)

## Middle tasks

*   get fscking and dead client expiry working (done)
*   Test a restore from a shard. Tell git-annex the content is no longer in the IA. Get the clients to upload it to our server.
*   Write client registration interface, which generates the client's ssh private key, git-annex UUID, and sends them to the client (done)
*   Help the user get the iabak-cronjob set up.
*   Email expire warnings (done)

## Later tasks

*   Create all 1770 shards, and see how that scales.
*   Write pre-receive git hook, to reject pushes of branches other then the git-annex branch (already done), and prevent bad/malicious pushes of the git-annex branch
*   Client runtime environment (docker image maybe?) with warrior-like interface (all that needs to do is configure things and get git-annex running)

## SHARD1

This is our first part of the IA that we want to get backed up. If we succeed, we will have backed up 1/1770th of the Internet Archive. This git-annex repository contains 100k files, the entire collections "internetarchivebooks" and "usenethistorical".

Some stats about the files this repository is tracking:

*   number of files: 103343
*   total file size: 2.91 terabytes
*   size of the git repository itself was 51 megabytes to start
*   after filling up shard1, the git repo had grown to 196 mb
*   We aimed for 4 copies of every file downloaded, but a few files got 5-8 copies made, due to eg, races and manual downloads. Want to keep an eye on this with future shards.
*   We got SHARD1 fully downloaded between April 1-6, 2016\. It took a while to ramp up as people came in, so later shards may download faster. Also, 2/3 of SHARD2 was downloaded during this same time period.