Related articles

*   [Gitweb](/index.php/Gitweb "Gitweb")
*   [Cgit](/index.php/Cgit "Cgit")
*   [HTTP tunneling#Tunneling Git](/index.php/HTTP_tunneling#Tunneling_Git "HTTP tunneling")
*   [Subversion](/index.php/Subversion "Subversion")
*   [Concurrent Versions System](/index.php/Concurrent_Versions_System "Concurrent Versions System")

> I've met people who thought that git is a front-end to GitHub. They were wrong, git is a front-end to the AUR.
> — Linus Torvalds

[Git](https://en.wikipedia.org/wiki/Git_(software) is the version control system (VCS) designed and developed by Linus Torvalds, the creator of the Linux kernel. Git is now used to maintain [AUR](/index.php/AUR "AUR") packages, as well as many other projects, including sources for the Linux kernel.

## Contents

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
*   [3 Usage](#Usage)
    *   [3.1 Getting a Git repository](#Getting_a_Git_repository)
    *   [3.2 Recording changes](#Recording_changes)
        *   [3.2.1 Staging changes](#Staging_changes)
        *   [3.2.2 Committing changes](#Committing_changes)
        *   [3.2.3 Revision selection](#Revision_selection)
        *   [3.2.4 Viewing changes](#Viewing_changes)
    *   [3.3 Undoing things](#Undoing_things)
    *   [3.4 Branching](#Branching)
    *   [3.5 Collaboration](#Collaboration)
        *   [3.5.1 Pull requests](#Pull_requests)
        *   [3.5.2 Using remotes](#Using_remotes)
        *   [3.5.3 Push to a repository](#Push_to_a_repository)
        *   [3.5.4 Dealing with merges](#Dealing_with_merges)
    *   [3.6 History and versioning](#History_and_versioning)
        *   [3.6.1 Searching the history](#Searching_the_history)
        *   [3.6.2 Tagging](#Tagging)
        *   [3.6.3 Organizing commits](#Organizing_commits)
*   [4 Tips and tricks](#Tips_and_tricks)
    *   [4.1 Using git-config](#Using_git-config)
    *   [4.2 Adopting a good etiquette](#Adopting_a_good_etiquette)
    *   [4.3 Speeding up authentication](#Speeding_up_authentication)
    *   [4.4 Protocol Defaults](#Protocol_Defaults)
    *   [4.5 Bash completion](#Bash_completion)
    *   [4.6 Git prompt](#Git_prompt)
    *   [4.7 Visual representation](#Visual_representation)
    *   [4.8 Commit tips](#Commit_tips)
    *   [4.9 Signing commits](#Signing_commits)
    *   [4.10 Working with a non-master branch](#Working_with_a_non-master_branch)
    *   [4.11 Directly sending patches to a mailing list](#Directly_sending_patches_to_a_mailing_list)
*   [5 Git server](#Git_server)
    *   [5.1 SSH](#SSH)
    *   [5.2 Smart HTTP](#Smart_HTTP)
    *   [5.3 Git](#Git)
    *   [5.4 Setting access rights](#Setting_access_rights)
*   [6 See also](#See_also)

## Installation

[Install](/index.php/Install "Install") the [git](https://www.archlinux.org/packages/?name=git) package. For the development version, install the [git-git](https://aur.archlinux.org/packages/git-git/) package. Check the optional dependencies when using tools such as *git svn*, *git gui* and *gitk*.

**Note:** To enable spell checking in *git-gui*, [aspell](https://www.archlinux.org/packages/?name=aspell) is required, along with the dictionary corresponding to the `LC_MESSAGES` [environment variable](/index.php/Environment_variable "Environment variable"). See [FS#28181](https://bugs.archlinux.org/task/28181) and the [aspell](/index.php/Aspell "Aspell") article.

## Configuration

In order to use Git you need to set at least a name and email:

```
$ git config --global user.name  "*John Doe*"
$ git config --global user.email "*johndoe@example.com*"

```

See [Getting Started - First-Time Git Setup](https://git-scm.com/book/en/Getting-Started-First-Time-Git-Setup).

See [#Tips and tricks](#Tips_and_tricks) for more settings.

## Usage

A Git repository is contained in a `.git` directory, which holds the revision history and other metadata. The directory tracked by the repository, by default the parent directory, is called the working directory. Changes in the working tree need to be staged before they can be recorded (committed) to the repository. Git also lets you restore, previously committed, working tree files.

See [Getting Started - Git Basics](https://git-scm.com/book/en/Getting-Started-Git-Basics).

### Getting a Git repository

*   Initialize a repository

	`git init`, see [git-init(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/git-init.1)

*   Clone an existing repository

	`git clone *repository*`, see [git-clone(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/git-clone.1)

### Recording changes

Git projects have a staging area, which is an `index` file in your Git directory, that stores the changes that will go into your next commit. To record a modified file you therefore firstly need to add it to the index (stage it). The `git commit` command then stores the current index in a new commit.

#### Staging changes

*   Add working tree changes to the index

	`git add *pathspec*`, see [git-add(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/git-add.1)

*   Remove changes from the index

	`git reset *pathspec*`, see [git-reset(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/git-reset.1)

*   Show changes to be committed, unstaged changes and untracked files

	`git status`, see [git-status(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/git-status.1)

You can tell Git to ignore certain untracked files using `.gitignore` files, see [gitignore(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/gitignore.5).

Git does not track file movement. Move detection during merges is based only on content similarity. The `git mv` command is just there for convenience and is equivalent to:

```
$ mv -i foo bar
$ git reset -- foo
$ git add bar

```

#### Committing changes

The `git commit` command records the staged changes to the repository, see [git-commit(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/git-commit.1).

*   `-m` – supply the commit message as an argument, instead of composing it in your default text editor
*   `-a` – automatically stage files that have been modified or deleted (does not add untracked files)
*   `--amend` – redo the last commit, amending the commit message or the committed files

**Tip:** Always commit small changes frequently and with meaningful messages.

#### Revision selection

Git offers multiple ways to specify revisions, see [gitrevisions(7)](https://jlk.fjfi.cvut.cz/arch/manpages/man/gitrevisions.7) and [Revision Selection](https://git-scm.com/book/tr/v2/Git-Tools-Revision-Selection).

Many Git commands take revisions as arguments. A commit can be identified by any of the following:

*   SHA-1 hash of the commit (the first 7 digits are usually sufficient to identify it uniquely)
*   Any commit label such as a branch or tag name
*   The label `HEAD` always refers to the currently checked-out commit (usually the head of the branch, unless you used *git checkout* to jump back in history to an old commit)
*   Any of the above plus `~` to refer to previous commits. For example, `HEAD~` refers to one commit before `HEAD` and `HEAD~5` refers to five commits before `HEAD`.

#### Viewing changes

Show differences between commits:

```
$ git diff HEAD HEAD~3

```

or between staging area and working tree:

```
$ git diff

```

View history of changes (where "*-N*" is the number of latest commits):

```
$ git log -p *(-N)*

```

### Undoing things

*   `git reset` - reset current HEAD to the specified state, see [git-reset(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/git-reset.1)

*   `git checkout` - to restore working tree files, see [git-checkout(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/git-checkout.1)

### Branching

Fixes and new features are usually tested in branches. When changes are satisfactory they can merged back into the default (master) branch.

Create a branch, whose name accurately reflects its purpose:

```
$ git branch *help-section-addition*

```

List branches:

```
$ git branch

```

Switch branches:

```
$ git checkout *branch*

```

Create and switch:

```
$ git checkout -b *branch*

```

Merge a branch back to the master branch:

```
$ git checkout master
$ git merge *branch*

```

The changes will be merged if they do not conflict. Otherwise, Git will print an error message, and annotate files in the working tree to record the conflicts. The annotations can be displayed with `git diff`. Conflicts are resolved by editing the files to remove the annotations, and committing the final version. See [#Dealing with merges](#Dealing_with_merges) below.

When done with a branch, delete it with:

```
$ git branch -d *branch*

```

### Collaboration

A typical Git work-flow is:

1.  Create a new repository or clone a remote one.
2.  Create a branch to make changes; then commit those changes.
3.  Consolidate commits for better organization/understanding.
4.  Merge commits back into the main branch.
5.  (Optional) Push changes to a remote server.

#### Pull requests

After making and committing some changes, the contributor can ask the original author to merge them. This is called a *pull request*.

To pull:

```
$ git pull *location* master

```

The *pull* command combines both *fetching* and *merging*. If there are conflicts (e.g. the original author made changes in the same time span), then it will be necessary to manually fix them.

Alternatively, the original author can pick the changes wanting to be incorporated. Using the *fetch* option (and *log* option with a special `FETCH_HEAD` symbol), the contents of the pull request can be viewed before deciding what to do:

```
$ git fetch *location* master
$ git log -p HEAD..FETCH_HEAD
$ git merge *location* master

```

#### Using remotes

Remotes are aliases for tracked remote repositories. A *label* is created defining a location. These labels are used to identify frequently accessed repositories.

Create a remote:

```
$ git remote add *label* *location*

```

Fetch a remote:

```
$ git fetch *label*

```

Show differences between master and a remote master:

```
$ git log -p master..*label*/master

```

View remotes for the current repository:

```
$ git remote -v

```

When defining a remote that is a parent of the fork (the project lead), it is defined as *upstream*.

#### Push to a repository

After being given rights from the original authors, push changes with:

```
$ git push *location* *branch*

```

When *git clone* is performed, it records the original location and gives it a remote name of `origin`.

So what *typically* is done is this:

```
$ git push origin master

```

If the `-u` (`--set-upstream-to`) option is used, the location is recorded so the next time just a `git push` is necessary.

#### Dealing with merges

See [Basic Merge Conflicts](http://git-scm.com/book/en/Git-Branching-Basic-Branching-and-Merging#Basic-Merge-Conflicts) in the Git Book for a detailed explanation on how to resolve merge conflicts. Merges are generally reversible. If wanting to back out of a merge one can usually use the `--abort` command (e.g. `git merge --abort` or `git pull --abort`).

### History and versioning

#### Searching the history

`git log` will give the history with a commit checksum, author, date, and the short message. The *checksum* is the "object name" of a commit object, typically a 40-character SHA-1 hash.

For history with a long message (where the "*checksum*" can be truncated, as long as it is unique):

```
$ git show (*checksum*)

```

Search for *pattern* in tracked files:

```
$ git grep *pattern*

```

Search in `.c` and `.h` files:

```
$ git grep *pattern* -- '*.[ch]'

```

#### Tagging

Tag commits for versioning:

```
$ git tag 2.14 *checksum*

```

*Tagging* is generally done for [releasing/versioning](https://www.drupal.org/node/1066342) but it can be any string. Generally annotated tags are used, because they get added to the Git database.

Tag the current commit with:

```
$ git tag -a 2.14 -m "Version 2.14"

```

List tags:

```
$ git tag -l

```

Delete a tag:

```
$ git tag -d 2.08

```

Update remote tags:

```
$ git push --tags

```

#### Organizing commits

Before submitting a pull request it may be desirable to consolidate/organize the commits. This is done with the *git rebase* `--interactive` option:

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

Git reads its configuration from three INI-type configuration files:

*   `/etc/gitconfig` for system-wide defaults
*   `~/.gitconfig` for user-specific configuration
*   `.git/config` for repository-specific configuration

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

See [git-config(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/git-config.1) and [Git Configuration](http://git-scm.com/book/en/v2/Customizing-Git-Git-Configuration) for more information.

### Adopting a good etiquette

*   When considering contributing to an existing project, read and understand its license, as it may excessively limit your ability to change the code. Some licenses can generate disputes over the ownership of the code.
*   Think about the project's community and how well you can fit into it. To get a feeling of the direction of the project, read any documentation and even the [log](#History_and_versioning) of the repository.
*   When requesting to pull a commit, or submit a patch, keep it small and well documented; this will help the maintainers understand your changes and decide whether to merge them or ask you to make some amendments.
*   If a contribution is rejected, do not get discouraged, it is their project after all. If it is important, discuss the reasoning for the contribution as clearly and as patiently as possible: with such an approach a resolution may eventually be possible.

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
*   For [zsh](/index.php/Zsh "Zsh"): `setopt PROMPT_SUBST ; PS1='[%n@%m %c$(__git_ps1 " (%s)")]\$ '`

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

### Signing commits

Git allows commits and tags to be signed using [GnuPG](/index.php/GnuPG "GnuPG"), see [Signing Your Work](https://git-scm.com/book/en/Git-Tools-Signing-Your-Work).

**Note:** To use [pinentry](https://www.archlinux.org/packages/?name=pinentry) curses for GPG signing make sure to `export GPG_TTY=$(tty)` (alternatively use pinentry-tty) otherwise the signing step will fail if GPG is currently in a locked state (since it cannot prompt for pin).

To configure Git to automatically sign commits:

```
$ git config --global commit.gpgSign true

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

### Directly sending patches to a mailing list

If you want to send patches directly to a mailing list, you have to install the following packages: [perl-authen-sasl](https://www.archlinux.org/packages/?name=perl-authen-sasl), [perl-net-smtp-ssl](https://www.archlinux.org/packages/?name=perl-net-smtp-ssl) and [perl-mime-tools](https://www.archlinux.org/packages/?name=perl-mime-tools).

Make sure you have configured your username and e-mail address, see [#Configuration](#Configuration).

Configure your e-mail settings:

```
$ git config --global sendemail.smtpserver *smtp.example.com*
$ git config --global sendemail.smtpserverport *587*
$ git config --global sendemail.smtpencryption *tls*
$ git config --global sendemail.smtpuser *foobar@example.com*

```

Now you should be able to send the patch to the mailing list (see also [OpenEmbedded:How to submit a patch to OpenEmbedded#Sending patches](http://www.openembedded.org/wiki/How_to_submit_a_patch_to_OpenEmbedded#Sending_patches)):

```
$ git add *filename*
$ git commit -s
$ git send-email --to=*openembedded-core@lists.openembedded.org* --confirm=always -M -1

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

You are able to secure the SSH user account even more allowing only push and pull commands on this user account. This is done by replacing the default login shell by git-shell. Described in [Setting Up the Server](https://git-scm.com/book/en/v2/Git-on-the-Server-Setting-Up-the-Server).

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

*   [https://git-scm.com/book/en/v2/Git-on-the-Server-Smart-HTTP](https://git-scm.com/book/en/v2/Git-on-the-Server-Smart-HTTP)
*   [https://git-scm.com/docs/git-http-backend](https://git-scm.com/docs/git-http-backend)

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

To restrict read and/or write access, use standard Unix permissions. Refer to [when gitolite is overkill](https://github.com/sitaramc/gitolite/blob/d74e58b5de8c78bddd29b009ba2d606f7fcb4f2d/doc/overkill.mkd) for more information.

For fine-grained access management, refer to [gitolite](/index.php/Gitolite "Gitolite") and [gitosis](/index.php/Gitosis "Gitosis").

## See also

*   Git man pages, see [git(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/git.1)
*   [Pro Git book](https://git-scm.com/book/en/)
*   [Git Reference](https://git.github.io/git-reference/) by GitHub
*   [Git workflow: Forks, remotes, and pull requests](http://nathanhoad.net/git-workflow-forks-remotes-and-pull-requests)
*   [VideoLAN wiki article](https://wiki.videolan.org/Git)
*   [A comparison of protocols GitHubGist](https://gist.github.com/grawity/4392747)
*   [How to GitHub](https://gun.io/blog/how-to-github-fork-branch-and-pull-request)