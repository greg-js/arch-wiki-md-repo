> <font color="grey">*I've met people who thought that git is a front-end to GitHub. They were wrong, git is a front-end to AUR.*</font>
> — Linus Torvalds

[Git](https://en.wikipedia.org/wiki/Git_(software) is the version control system (VCS) designed and developed by Linus Torvalds, the creator of the Linux kernel. Git is now used to maintain [AUR](/index.php/AUR "AUR") packages, as well as many other projects, including sources for the Linux kernel.

## Contents

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
*   [3 Usage](#Usage)
    *   [3.1 Local repository](#Local_repository)
        *   [3.1.1 Staging operations](#Staging_operations)
        *   [3.1.2 Commit changes](#Commit_changes)
        *   [3.1.3 View changes](#View_changes)
        *   [3.1.4 Branch a repository](#Branch_a_repository)
    *   [3.2 Collaboration](#Collaboration)
        *   [3.2.1 Adopting a good etiquette](#Adopting_a_good_etiquette)
        *   [3.2.2 Clone a repository](#Clone_a_repository)
        *   [3.2.3 Pull requests](#Pull_requests)
        *   [3.2.4 Using remotes](#Using_remotes)
        *   [3.2.5 Push to a repository](#Push_to_a_repository)
        *   [3.2.6 Dealing with merges](#Dealing_with_merges)
        *   [3.2.7 Send patch to mailing list](#Send_patch_to_mailing_list)
    *   [3.3 History and versioning](#History_and_versioning)
        *   [3.3.1 Searching the history](#Searching_the_history)
        *   [3.3.2 Versioning for release](#Versioning_for_release)
        *   [3.3.3 Organizing commits](#Organizing_commits)
*   [4 Tips and tricks](#Tips_and_tricks)
    *   [4.1 Using git-config](#Using_git-config)
    *   [4.2 Speeding up authentication](#Speeding_up_authentication)
    *   [4.3 Protocol Defaults](#Protocol_Defaults)
    *   [4.4 Bash completion](#Bash_completion)
    *   [4.5 Git prompt](#Git_prompt)
    *   [4.6 Visual representation](#Visual_representation)
    *   [4.7 Commit tips](#Commit_tips)
    *   [4.8 Working with a non-master branch](#Working_with_a_non-master_branch)
*   [5 Git server](#Git_server)
    *   [5.1 SSH](#SSH)
    *   [5.2 Smart HTTP](#Smart_HTTP)
    *   [5.3 Git](#Git)
    *   [5.4 Setting access rights](#Setting_access_rights)
*   [6 See also](#See_also)

## Installation

[Install](/index.php/Install "Install") the [git](https://www.archlinux.org/packages/?name=git) package. For the development version, install [git-git](https://aur.archlinux.org/packages/git-git/) from the AUR. Check the optional dependencies when using tools such as *git svn*, *git gui* and *gitk*.

**Note:** To enable spell checking in *git-gui*, [aspell](https://www.archlinux.org/packages/?name=aspell) is required, along with the dictionary corresponding to the `LC_MESSAGES` [environment variable](/index.php/Environment_variable "Environment variable"). See [FS#28181](https://bugs.archlinux.org/task/28181) and the [aspell](/index.php/Aspell "Aspell") article.

## Configuration

In order to use Git you need to set at least a name and email:

```
$ git config --global user.name  "*John Doe*"
$ git config --global user.email "*johndoe@foobar.com*"

```

See [#Tips and tricks](#Tips_and_tricks) for more settings.

## Usage

This tutorial teaches how to use Git for basic distributed revision control of a project.

Git is a distributed version control system, which means that the entire history of changes to a repository is stored locally, in a directory called `./.git` in the project directory. The project files which are visible to the user constitute the *working tree*. These files can be updated to match revisions stored in `./.git` using `git` commands (e.g. `git checkout`), and new revisions can be created in turn by editing these files and running the appropriate `git` commands (e.g. `git commit`).

See `man gitglossary` for more complete definitions of the terms used in this tutorial.

A typical Git work-flow is:

1.  Create a new project or clone a remote one.
2.  Create a branch to make changes; then commit those changes.
3.  Consolidate commits for better organization/understanding.
4.  Merge commits back into the main branch.
5.  (Optional) Push changes to a remote server.

### Local repository

#### Staging operations

**Initialize** a new repository. This creates and initializes `./.git`:

```
$ cd (your project)/
$ git init

```

To record the changes to the repository, they must first be added to the *index*, or *staging area*, with an operation often also referred to as *staging*. When you commit changes using `git commit`, it is the contents of the index which are committed to the current branch, not the contents of the working tree.

**Note:** The index is actually a binary file `.git/index`, which can be queried with `git ls-files --stage`.

To **add files** to the index from the working tree:

```
$ git add *file1* *file2*

```

This records the current state of the files. If the files are subsequently modified, you can run `git add` again to "add" the new versions to the index.

**Add all** files:

```
$ git add .

```

**Tip:** To **ignore** some files from, e.g. `git add .`, create a `.gitignore` file (or files): `.gitignore` 
```
# File I'll likely delete
test-script

# Ignore all .html files, except 'important.html'
*.html
!important.html

# Ignore all files recursively in 'DoNotInclude'
DoNotInclude/**

```

See [gitignore(5)](http://git-scm.com/docs/gitignore) for details.

**Remove** a file from staging (`--cached` preserves the actual file(s)):

```
$ git rm *(--cached)* *file*

```

**Remove all** files:

```
$ git rm --cached -r .

```

Or:

```
$ git reset HEAD -- .

```

Here, `HEAD` is a "symbolic reference" to the current revision.

**Rename** a file:

```
$ git mv *file1* *file2*

```

**Note:** `git mv` is a convenience command, roughly equivalent to `mv file1 file2` followed by `git rm file1` and `git add file2`. Rename detection during merges is based only on content similarity, and ignores the actual commands used to rename files. The broader rationale for this approach, which distinguishes Git from patch-based systems like [Darcs](/index.php/Darcs "Darcs"), can be found [here](http://permalink.gmane.org/gmane.comp.version-control.git/217).

**List** files:

```
$ git ls-files

```

By default this shows files in the staging area (`--cached` files).

#### Commit changes

Once the content to be recorded is *staged*, **commit** them with:

```
$ git commit -m "*First commit.*"

```

The `-m (*--message)*` option is for a short message: if omitted, the preset editor will be spawned to allow entering a longer message.

**Tip:**

*   Always commit small changes frequently and with meaningful messages.
*   To **add** all the modified files to the index, **and commit** them in a single command (`-a` stands for `--all`):

```
$ git commit -am "*First commit.*"

```

**Edit** the commit message for the last commit. This also amends the commit with any files which have been newly staged:

```
$ git commit --amend -m "*Message.*"

```

Many of the commands in this article take commits as arguments. A commit can be identified by any of the following:

*   Its 40-digit SHA-1 hash (the first 7 digits are usually sufficient to identify it uniquely)
*   Any commit label such as a branch or tag name
*   The label `HEAD` always refers to the currently checked-out commit (usually the head of the branch, unless you used *git checkout* to jump back in history to an old commit)
*   Any of the above plus `~` to refer to previous commits. For example, `HEAD~` refers to one commit before `HEAD` and `HEAD~5` refers to five commits before `HEAD`.

#### View changes

**Show differences** between commits:

```
$ git diff HEAD HEAD~3

```

or between staging area and working tree:

```
$ git diff

```

**Get** a general **overview** of the changes:

```
$ git status

```

**View history** of changes (where "*-N*" is the number of latest commits):

```
$ git log -p *(-N)*

```

#### Branch a repository

Fixes and new features are usually tested in branches. When changes are satisfactory they can merged back into the default (master) branch.

**Create** a branch, whose name accurately reflects its purpose:

```
$ git branch *help-section-addition*

```

**List** branches:

```
$ git branch

```

**Switch** branches:

```
$ git checkout *branch*

```

**Create and switch**:

```
$ git checkout -b *branch*

```

**Merge** a branch back to the master branch:

```
$ git checkout master
$ git merge *branch*

```

The changes will be merged if they do not conflict. Otherwise, Git will print an error message, and annotate files in the working tree to record the conflicts. The annotations can be displayed with `git diff`. Conflicts are resolved by editing the files to remove the annotations, and committing the final version. See [#Dealing with merges](#Dealing_with_merges) below.

When done with a branch, **delete** it with:

```
$ git branch -d *branch*

```

### Collaboration

#### Adopting a good etiquette

*   When considering contributing to an existing project, read and understand its license, as it may excessively limit your ability to change the code. Some licenses can generate disputes over the ownership of the code.
*   Think about the project's community and how well you can fit into it. To get a feeling of the direction of the project, read any documentation and even the [log](#History_and_versioning) of the repository.
*   When requesting to pull a commit, or submit a patch, keep it small and well documented; this will help the maintainers understand your changes and decide whether to merge them or ask you to make some amendments.
*   If a contribution is rejected, do not get discouraged, it is their project after all. If it is important, discuss the reasoning for the contribution as clearly and as patiently as possible: with such an approach a resolution may eventually be possible.

#### Clone a repository

To begin contributing to a project, **clone** its repository:

```
$ git clone *location* *folder*

```

`*location*` can be either a path or network address. Also, when cloning is done, the location is recorded so just a `git pull` will be needed later.

#### Pull requests

After making and committing some changes, the contributor can ask the original author to merge them. This is called a *pull request*.

To **pull**:

```
$ git pull *location* master

```

The *pull* command combines both *fetching* and *merging*. If there are conflicts (e.g. the original author made changes in the same time span), then it will be necessary to manually fix them.

Alternatively, the original author can **pick** the **changes** wanting to be incorporated. Using the *fetch* option (and *log* option with a special `FETCH_HEAD` symbol), the contents of the pull request can be viewed before deciding what to do:

```
$ git fetch *location* master
$ git log -p HEAD..FETCH_HEAD
$ git merge *location* master

```

#### Using remotes

Remotes are aliases for tracked remote repositories. A *label* is created defining a location. These labels are used to identify frequently accessed repositories.

**Create** a remote:

```
$ git remote add *label* *location*

```

**Fetch** a remote:

```
$ git fetch *label*

```

**Show differences** between master and a remote master:

```
$ git log -p master..*label*/master

```

**View** remotes for the current repository:

```
$ git remote -v

```

When defining a remote that is a parent of the fork (the project lead), it is defined as *upstream*.

#### Push to a repository

After being given rights from the original authors, **push** changes with:

```
$ git push *location* *branch*

```

When *git clone* is performed, it records the original location and gives it a remote name of `origin`.

So what **typically** is done is this:

```
$ git push origin master

```

If the `-u` (`--set-upstream-to`) option is used, the location is recorded so the next time just a `git push` is necessary.

#### Dealing with merges

See [Basic Merge Conflicts](http://git-scm.com/book/en/Git-Branching-Basic-Branching-and-Merging#Basic-Merge-Conflicts) in the Git Book for a detailed explanation on how to resolve merge conflicts. Merges are generally reversible. If wanting to back out of a merge one can usually use the `--abort` command (e.g. `git merge --abort` or `git pull --abort`).

#### Send patch to mailing list

If you want to send patches directly to a mailing list, you have to install the following packages: [perl-authen-sasl](https://www.archlinux.org/packages/?name=perl-authen-sasl), [perl-net-smtp-ssl](https://www.archlinux.org/packages/?name=perl-net-smtp-ssl) and [perl-mime-tools](https://www.archlinux.org/packages/?name=perl-mime-tools).

Make sure you have configured you username and e-mail address, see [#Configuration](#Configuration).

**Configure** your **e-mail** settings:

```
$ git config --global sendemail.smtpserver *smtp.gmail.com*
$ git config --global sendemail.smtpserverport *587*
$ git config --global sendemail.smtpencryption *tls*
$ git config --global sendemail.smtpuser *foobar@gmail.com*

```

Now you should be able to **send** the **patch** to the mailing list (see also [OpenEmbedded:How to submit a patch to OpenEmbedded#Sending patches](http://www.openembedded.org/wiki/How_to_submit_a_patch_to_OpenEmbedded#Sending_patches)):

```
$ git add *filename*
$ git commit -s
$ git send-email --to=*openembedded-core@lists.openembedded.org* --confirm=always -M -1

```

### History and versioning

#### Searching the history

`git log` will give the history with a commit checksum, author, date, and the short message. The *checksum* is the "object name" of a commit object, typically a 40-character SHA-1 hash.

For **history** with a **long message** (where the "*checksum*" can be truncated, as long as it is unique):

```
$ git show (*checksum*)

```

**Search** for *pattern* in tracked files:

```
$ git grep *pattern*

```

**Search** in **`.c`** and **`.h`** files:

```
$ git grep *pattern* -- '*.[ch]'

```

#### Versioning for release

**Tag** commits for versioning:

```
$ git tag 2.14 *checksum*

```

*Tagging* is generally done for [releasing/versioning](https://www.drupal.org/node/1066342) but it can be any string. Generally annotated tags are used, because they get added to the Git database.

**Tag** the **current** commit with:

```
$ git tag -a 2.14 -m "Version 2.14"

```

**List** tags:

```
$ git tag -l

```

**Delete** a tag:

```
$ git tag -d 2.08

```

**Update remote** tags:

```
$ git push --tags

```

#### Organizing commits

Before submitting a pull request it may be desirable to **consolidate/organize** the commits. This is done with the *git rebase* `--interactive` option:

```
$ git rebase -i *checksum*

```

This will open the editor with a summary of all the commits in the range specified; in this case including the newest (`HEAD`) back to, but excluding, commit `*checksum*`. Or to use a number notation, use for example `HEAD~3`, which will rebase the last three commits:

```
pick d146cc7 Mountpoint test.
pick 4f47712 Explain -o option in readme.
pick 8a4d479 Rename documentation.

```

Editing the action in the first column will dictate how the rebase will be done. The options are:

*   `pick` — Apply this commit as is (the default).
*   `edit` — Edit files and/or commit message.
*   `reword` — Edit commit message.
*   `squash` — Merge/fold into previous commit.
*   `fixup` — Merge/fold into previous commit discarding its message.

The commits can be re-ordered or erased from the history (but be very careful with these). After editing the file, Git will perform the specified actions; if prompted to resolve merge problems, fix them and continue with `git rebase --continue` or back out with the `git rebase --abort` command.

**Note:** Squashing commits is only used for local commits, it will cause troubles on a repository that is shared by other people.

## Tips and tricks

### Using git-config

Git reads its configuration from a few INI-type configuration files:

*   Each repository contains a `.git/config` file for specific configuration.
*   Each user has a `$HOME/.gitconfig` file for fallback values.
*   `/etc/gitconfig` is used for system-wide defaults.

These files can be edited directly, but the usual method is to use *git config*, as shown in the examples below.

List the currently set variables:

```
$ git config {--local,--global,--system} --list

```

Set the default editor from [vim](/index.php/Vim "Vim") to [nano](/index.php/Nano "Nano"):

```
$ git config --global core.editor "nano -w"

```

Set the default push action:

```
$ git config --global push.default simple

```

Set a different tool for *git difftool* (*meld* by default):

```
$ git config --global diff.tool vimdiff

```

See [git-config(1)](https://www.kernel.org/pub/software/scm/git/docs/git-config.html) and [Git Configuration](http://git-scm.com/book/en/v2/Customizing-Git-Git-Configuration) for more information.

### Speeding up authentication

You may wish to avoid the hassle of authenticating interactively at every push to the Git server.

*   If you are authenticating with SSH keys, use an [SSH agent](/index.php/SSH_agent "SSH agent"). See also [SSH#Speeding up SSH](/index.php/SSH#Speeding_up_SSH "SSH") and [SSH#Keep alive](/index.php/SSH#Keep_alive "SSH").
*   If you are authenticating with username and password, switch to [SSH keys](/index.php/SSH_keys "SSH keys") if the server supports SSH, otherwise try [git-credential-cache](https://git-scm.com/docs/git-credential-cache) or [git-credential-store](https://git-scm.com/docs/git-credential-store).

### Protocol Defaults

If you are running a multiplexed SSH connection as shown above, Git over SSH might be faster than HTTPS. Also, some servers (like the AUR) only allow pushing via SSH. For example, the following config will set Git over SSH for any repository hosted on the AUR.

 `~/.gitconfig` 
```
[url "ssh://aur@aur.archlinux.org/"]
	insteadOf = https://aur.archlinux.org/
	insteadOf = http://aur.archlinux.org/
	insteadOf = git://aur.archlinux.org/

```

### Bash completion

In order to enable Bash completion, source `/usr/share/git/completion/git-completion.bash` in a [Bash startup file](/index.php/Bash#Configuration_files "Bash"). Alternatively, install [bash-completion](https://www.archlinux.org/packages/?name=bash-completion).

### Git prompt

The Git package comes with a prompt script. To enable it, source the `/usr/share/git/completion/git-prompt.sh` script in a [shell startup file](/index.php/Autostarting#Shells "Autostarting"), then set a custom prompt with the `%s` parameter:

*   For [Bash](/index.php/Bash "Bash"): `PS1='[\u@\h \W$(__git_ps1 " (%s)")]\$ '`
*   For [zsh](/index.php/Zsh "Zsh"): `PS1='[%n@%m %c$(__git_ps1 " (%s)")]\$ '`

When changing to a directory of a Git repository, the prompt will change to show the branch name. Extra details can be set to be shown by the prompt:

<caption></caption>
| Shell variable | Information |
| GIT_PS1_SHOWDIRTYSTATE | **+** for staged, ***** if unstaged. |
| GIT_PS1_SHOWSTASHSTATE | **$** if something is stashed. |
| GIT_PS1_SHOWUNTRACKEDFILES | **%** if there are untracked files. |
| GIT_PS1_SHOWUPSTREAM | **<,>,<>** behind, ahead, or diverged from upstream. |

`GIT_PS1_SHOWUPSTREAM` will need to be set to `auto` for changes to take effect.

**Note:** If you experience that `$(__git_ps1)` returns `((unknown))`, then there is a `.git` folder in your current directory which does not contain any repository, and therefore Git does not recognize it. This can, for example, happen if you mistake Git's configuration file to be `~/.git/config` instead of `~/.gitconfig`.

Alternatively, you can use one of git shell prompt customization packages from [AUR](/index.php/AUR "AUR") such as [bash-git-prompt](https://aur.archlinux.org/packages/bash-git-prompt/) or [gittify](https://aur.archlinux.org/packages/gittify/).

### Visual representation

To get an idea of the amount of work done:

```
$ git diff --stat

```

*git log* with forking representation:

```
$ git log --graph --oneline --decorate

```

*git log* graph alias (i.e. *git graph* will show a decorated version):

```
$ git config --global alias.graph 'log --graph --oneline --decorate'

```

### Commit tips

Reset to previous commit (very dangerous, erases everything to specified commit):

```
$ git reset --hard HEAD^

```

If a repository address gets changed, its remote location will need to be updated:

```
$ git remote set-url origin git@*address*:*user*/*repo*.git

```

Signed-off-by line append (a name-email signature is added to the commit which is required by some projects):

```
 $ git commit -s

```

Signed-off-by automatically append to patches (when using `git format-patch *commit*`):

```
$ git config --local format.signoff true

```

Commit specific parts of files that have changed. This is useful if there are a large number of changes made that would be best split into several commits:

```
$ git add -p

```

### Working with a non-master branch

Occasionally a maintainer will ask that work be done on a branch. These branches are often called `devel` or `testing`. Begin by cloning the repository.

To enter another branch beside master (*git clone* only shows master branch but others still exist, `git branch -a` to show):

```
$ git checkout -b *branch* origin/*branch*

```

Now edit normally; however to keep the repository tree in sync be sure to use both:

```
$ git pull --all
$ git push --all

```

## Git server

How to set up connecting to repositories using varying protocols.

### SSH

To use the SSH protocol, first set up a public SSH key; for that follow the guide at [SSH keys](/index.php/SSH_keys "SSH keys"). To set up a SSH server, follow the [SSH](/index.php/SSH "SSH") guide.

With SSH working and a key generated, paste the contents of `~/.ssh/id_rsa.pub` to `~/.ssh/authorized_keys` (be sure it is all on one line). Now the Git repository can be accessed with SSH by doing:

```
$ git clone *user*@*foobar.com*:*my_repository*.git

```

You should now get an SSH yes/no question, if you have the SSH client setting `StrictHostKeyChecking` set to `ask` (the default). Type `yes` followed by `Enter`. Then you should have your repository checked out. Because this is with SSH, you also have commit rights now.

To modify an existing repository to use SSH, the remote location will need to be redefined:

```
$ git remote set-url origin git@localhost:*my_repository*.git

```

Connecting on a port other than 22 can be configured on a per-host basis in `/etc/ssh/ssh_config` or `~/.ssh/config`. To set up ports for a repository (here 443 as example):

 `.git/config` 
```
[remote "origin"]
    url = ssh://*user*@*foobar*.com:443/~*my_repository*/repo.git
```

### Smart HTTP

Git is able to use the HTTP(S) protocol as efficiently as the SSH or Git protocols, by utilizing the git-http-backend. Furthermore it is not only possible to clone or pull from repositories, but also to push into repositories over HTTP(S).

The setup for this is rather simple as all you need to have installed is the Apache web server ([apache](https://www.archlinux.org/packages/?name=apache), with `mod_cgi`, `mod_alias`, and `mod_env` enabled) and of course, [git](https://www.archlinux.org/packages/?name=git).

Once you have your basic setup running, add the following to your Apache configuration file, which is usually located at:

 `/etc/httpd/conf/httpd.conf` 
```
<Directory "/usr/lib/git-core*">
    Require all granted
</Directory>

SetEnv GIT_PROJECT_ROOT /srv/git
SetEnv GIT_HTTP_EXPORT_ALL
ScriptAlias /git/ /usr/lib/git-core/git-http-backend/

```

This assumes your Git repositories are located at `/srv/git` and that you want to access them via something like: `http(s)://your_address.tld/git/your_repo.git`.

**Note:** Make sure that Apache can read and write to your repositories.

For more detailed documentation, visit the following links:

*   [http://progit.org/2010/03/04/smart-http.html](http://progit.org/2010/03/04/smart-http.html)
*   [https://www.kernel.org/pub/software/scm/git/docs/v1.7.10.1/git-http-backend.html](https://www.kernel.org/pub/software/scm/git/docs/v1.7.10.1/git-http-backend.html)

### Git

**Note:** The Git protocol is not encrypted or authenticated, and only allows read access.

[Start and enable](/index.php/Start "Start") `git-daemon.socket`.

The daemon is started with the following options:

```
ExecStart=-/usr/lib/git-core/git-daemon --inetd --export-all --base-path=/srv/git

```

Repositories placed in `/srv/git/` will be recognized by the daemon. Clients can connect with something similar to:

```
$ git clone git://*location*/*repository*.git

```

### Setting access rights

To restrict read and/or write access, use standard Unix permissions. Refer to [http://sitaramc.github.com/gitolite/doc/overkill.html](http://sitaramc.github.com/gitolite/doc/overkill.html) ([archive.org mirror](https://web.archive.org/web/20111004134500/http://sitaramc.github.com/gitolite/doc/overkill.html)) for more information.

For fine-grained access management, refer to [gitolite](/index.php/Gitolite "Gitolite") and [gitosis](/index.php/Gitosis "Gitosis").

## See also

*   Miscallaneous man pages available in the [git](https://www.archlinux.org/packages/?name=git) package: `gittutorial(7)`, `giteveryday(7)`, `gitworkflows(7)`
*   [Pro Git book](http://git-scm.com/book)
*   [Git Reference](http://gitref.org/)
*   [https://www.kernel.org/pub/software/scm/git/docs/](https://www.kernel.org/pub/software/scm/git/docs/)
*   [Git overall](https://gun.io/blog/how-to-github-fork-branch-and-pull-request)
*   [Git overall2](http://nathanhoad.net/git-workflow-forks-remotes-and-pull-requests)
*   [https://wiki.videolan.org/Git](https://wiki.videolan.org/Git)
*   [A comparison of protocols offered by GitHub](https://gist.github.com/grawity/4392747)