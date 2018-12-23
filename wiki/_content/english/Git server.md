This article gives an overview on how to host a [Git](/index.php/Git "Git") server. For more information, refer to the [Git on the Server chapter](https://git-scm.com/book/en/v2/Git-on-the-Server-The-Protocols) of the Pro Git book.

## Contents

*   [1 Protocols](#Protocols)
    *   [1.1 SSH](#SSH)
    *   [1.2 Smart HTTP](#Smart_HTTP)
        *   [1.2.1 Apache](#Apache)
    *   [1.3 Git](#Git)
*   [2 Access control](#Access_control)
*   [3 Web interfaces](#Web_interfaces)
    *   [3.1 Simple web applications](#Simple_web_applications)
    *   [3.2 Advanced web applications](#Advanced_web_applications)

## Protocols

Refer to [Git on the Server - The Protocols](https://git-scm.com/book/en/v2/Git-on-the-Server-The-Protocols) for a detailed description along with pros and cons.

### SSH

You only need to set up an [SSH server](/index.php/SSH "SSH").

You are able to secure the SSH user account even more allowing only push and pull commands on this user account. This is done by replacing the default login shell by git-shell. Described in [Setting Up the Server](https://git-scm.com/book/en/v2/Git-on-the-Server-Setting-Up-the-Server).

### Smart HTTP

The [git-http-backend(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/git-http-backend.1) is a CGI program, allowing efficient cloning, pulling and pushing over HTTP(S).

#### Apache

The setup for this is rather simple as all you need to have installed is the [Apache HTTP Server](/index.php/Apache_HTTP_Server "Apache HTTP Server"), with `mod_cgi`, `mod_alias`, and `mod_env` enabled) and of course, [git](https://www.archlinux.org/packages/?name=git).

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

The Git protocol is not encrypted or authenticated, and only allows read access.

The Git daemon ([git-daemon(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/git-daemon.1)) can be [started](/index.php/Start "Start") with `git-daemon.socket`.

The service uses the `--export-all` and `--base-path` parameters to serve all repositories placed in `/srv/git/`.

## Access control

For fine-grained access control, the following solutions are available:

*   **[Gitolite](/index.php/Gitolite "Gitolite")** — An access control layer on top of Git, written in Perl.

	[https://github.com/sitaramc/gitolite](https://github.com/sitaramc/gitolite) || [gitolite](https://www.archlinux.org/packages/?name=gitolite)

*   **[Gitosis](/index.php/Gitosis "Gitosis")** — Software for hosting Git repositories, written in Python.

	[https://github.com/tv42/gitosis](https://github.com/tv42/gitosis) || [gitosis-git](https://aur.archlinux.org/packages/gitosis-git/)

Note that if you are willing to create [user accounts](/index.php/User_account "User account") for all of the people that should have access to the repositories and do not need access control at the level of git objects (like branches), you can also use standard [file permissions](/index.php/File_permissions "File permissions") for access control.[[1]](https://github.com/sitaramc/gitolite/blob/d74e58b5de8c78bddd29b009ba2d606f7fcb4f2d/doc/overkill.mkd)

## Web interfaces

### Simple web applications

*   [Gitweb](/index.php/Gitweb "Gitweb") — the default web interface that comes with Git
*   **[cgit](/index.php/Cgit "Cgit")** — A web interface for git written in plain C.

	[http://git.zx2c4.com/cgit/](http://git.zx2c4.com/cgit/) || [cgit](https://www.archlinux.org/packages/?name=cgit)

### Advanced web applications

*   **[Gitea](/index.php/Gitea "Gitea")** — Painless self-hosted Git service. Community managed fork of Gogs.

	[https://gitea.io](https://gitea.io) || [gitea](https://www.archlinux.org/packages/?name=gitea)

*   **[GitLab](/index.php/GitLab "GitLab")** — Project management and code hosting application, written in Ruby.

	[https://gitlab.com/gitlab-org/gitlab-ce](https://gitlab.com/gitlab-org/gitlab-ce) || [gitlab](https://www.archlinux.org/packages/?name=gitlab)

*   **[Gogs](/index.php/Gogs "Gogs")** — Self Hosted Git Service, written in Go.

	[https://gogs.io](https://gogs.io) || [gogs](https://aur.archlinux.org/packages/gogs/)