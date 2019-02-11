相关文章

*   [Users and groups (简体中文)](/index.php/Users_and_groups_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Users and groups (简体中文)")
*   [sudo (简体中文)](/index.php/Sudo_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Sudo (简体中文)")

**翻译状态：** 本文是英文页面 [su](/index.php/Su "Su") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2018-04-10，点击[这里](https://wiki.archlinux.org/index.php?title=su&diff=0&oldid=516603)可以查看翻译后英文页面的改动。

**su** 命令 (**s**ubstitute **u**ser) 用来切换当前用户身份到其他用户身份，默认切换成 root。

参阅 [PAM](/index.php/PAM "PAM") 可以找到配置 **su** 其他特性的方法。

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 安装](#安装)
*   [2 用法](#用法)
*   [3 另一个选择：Sudo](#另一个选择：Sudo)
*   [4 提示和技巧](#提示和技巧)
    *   [4.1 “登录至”其他用户](#“登录至”其他用户)
    *   [4.2 su 和 wheel 用户组](#su_和_wheel_用户组)

## 安装

su 是 [util-linux](https://www.archlinux.org/packages/?name=util-linux) 包的一部分，默认已经作为 [base](https://www.archlinux.org/groups/x86_64/base/) 组的一部分安装到 Arch 中了。

## 用法

要切换到其他用户身份，将要切换的用户名传递给 su，像这样：

```
# su *username*

```

然后就能看到提示符，要求输入所要切换用户的密码。

如果没有传入用户名，su 默认切换为 root 用户，要求输入的密码也应该是 root 用户的密码。

## 另一个选择：Sudo

[sudo](/index.php/Sudo "Sudo") 可以提供和 su 类似的功能，且更加可定制化，根据具体要求和威胁模型分析，可以作为 su 的一个替代。sudo 系统会提示你输入你自己的密码，或者根本没有密码（如果以这种方式配置的话），而不是目标用户（你正试图使用的帐户）的密码。这样就不必在用户之间共享密码，并且如果需要阻止一个用户获得 root 权限（或获得其他用户权限），则无需更改 root 密码（更改密码将给其他人造成不便），你只需要撤销该用户的 sudo 访问权。

如果 sudo 被配置为允许用户以 root 身份运行 shell，那么用户只要用 `sudo -s` 或 `sudo -i` 命令就可以分别模拟出 `su` 或 `su -l` 命令的效果，而且是用他自己的密码（或没有密码），而不是 root 的密码。同样，如果允许以 john 身份运行 shell，`sudo -u john -i` 和 `su -l john` 效果一样。

## 提示和技巧

### “登录至”其他用户

su 的默认行为是保持在当前目录中并保持原始用户的环境变量（而不是切换到新用户的环境变量）。

这一特性的优劣需要注意以下重要的对比因素：

*   系统管理员可以使用普通用户的 shell 而不是自己的。特别是在有些时候，解决用户问题的最有效的方法，就是登录到该用户的帐户以重现问题或进行调试。

*   但是通常情况下，root 用户不能登录普通用户的 shell 并使用该用户的环境变量进行操作，而是用自己的环境变量操作，这在很多情况下是不可取的，甚至是危险的。在无意中使用普通用户的 shell 时，root 可能会安装程序，或对系统进行其他更改，而这些更改与使用 root 帐户时所做的结果不同。例如，可能会安装某个程序，使得普通用户能够意外地损坏系统或未经授权访问某些数据。

因此，建议系统管理员以及被授权使用 su 的任何其他用户（建议只有极少数用户），始终保持用 `-l` 或 `--login` 选项运行 su 命令的习惯。它有两个作用：

1.  通过 *登录至* 目标用户，从当前工作目录切换到目标用户的主目录（比如切换到 root 用户就是 `/root`）。
2.  根据目标用户的 `~/.bashrc` 切换到目标用户的环境变量。也就是说，当前工作目录和环境将会切换到和目标用户登录新会话时一样的目录和环境（而不是仅接管现有用户的会话）。

因此，管理员通常应该这样使用 su：

```
$ su -l

```

添加用户名 root 结果一样：

```
$ su -l root

```

对于任何其他用户（如名为 archie 的用户），同样可以做到：

```
# su -l archie

```

你可能希望在 `~/.bashrc` 里为这个规则添加一个 alias：

```
alias su="su -l"

```

### su 和 wheel 用户组

BSD su 默认仅允许 "wheel" [用户组](/index.php/Users_and_groups_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)#用户组管理 "Users and groups (简体中文)") 成员切换至 root 身份。而 GNU su 默认没有这一特性，可以使用 [PAM](/index.php/PAM_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "PAM (简体中文)") 来模拟这一特性。将 `/etc/pam.d/su` 和 `/etc/pam.d/su-l` 中相应的行取消注释：

```
auth required pam_wheel.so use_uid

```