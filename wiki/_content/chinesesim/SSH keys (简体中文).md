SSH 密钥对可以让您方便的登录到 SSH 服务器，而无需输入密码。由于您无需发送您的密码到网络中，SSH 密钥对被认为是更加安全的方式。再加上使用密码短语 (passphrase) 的使用，安全性会更上一层楼。

同时，我们可以使用 SSH agent 来帮助我们记住密码短语，无需我们记住每一个密钥对的密码短语，减轻了我们的负担。

本文将为您介绍如何管理密钥对，以方便的连接到您的 SSH 服务器。本文默认您已经熟知 [Secure Shell (简体中文)](/index.php/Secure_Shell_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Secure Shell (简体中文)")，并安装好位于[官方软件仓库](/index.php/Official_repositories_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Official repositories (简体中文)") 的 [openssh](https://www.archlinux.org/packages/?name=openssh)。

## Contents

*   [1 背景](#.E8.83.8C.E6.99.AF)
*   [2 生成密钥对](#.E7.94.9F.E6.88.90.E5.AF.86.E9.92.A5.E5.AF.B9)
    *   [2.1 选择合适的加密方式](#.E9.80.89.E6.8B.A9.E5.90.88.E9.80.82.E7.9A.84.E5.8A.A0.E5.AF.86.E6.96.B9.E5.BC.8F)
    *   [2.2 选择密钥存储位置以及密码短语](#.E9.80.89.E6.8B.A9.E5.AF.86.E9.92.A5.E5.AD.98.E5.82.A8.E4.BD.8D.E7.BD.AE.E4.BB.A5.E5.8F.8A.E5.AF.86.E7.A0.81.E7.9F.AD.E8.AF.AD)
        *   [2.2.1 不修改密钥对的情况下修改密码短语](#.E4.B8.8D.E4.BF.AE.E6.94.B9.E5.AF.86.E9.92.A5.E5.AF.B9.E7.9A.84.E6.83.85.E5.86.B5.E4.B8.8B.E4.BF.AE.E6.94.B9.E5.AF.86.E7.A0.81.E7.9F.AD.E8.AF.AD)
        *   [2.2.2 管理多组密钥对](#.E7.AE.A1.E7.90.86.E5.A4.9A.E7.BB.84.E5.AF.86.E9.92.A5.E5.AF.B9)
*   [3 将公钥复制到远程服务器上](#.E5.B0.86.E5.85.AC.E9.92.A5.E5.A4.8D.E5.88.B6.E5.88.B0.E8.BF.9C.E7.A8.8B.E6.9C.8D.E5.8A.A1.E5.99.A8.E4.B8.8A)
    *   [3.1 简单的方法](#.E7.AE.80.E5.8D.95.E7.9A.84.E6.96.B9.E6.B3.95)
    *   [3.2 传统的方法](#.E4.BC.A0.E7.BB.9F.E7.9A.84.E6.96.B9.E6.B3.95)
*   [4 安全性](#.E5.AE.89.E5.85.A8.E6.80.A7)
    *   [4.1 保证 authorized_keys 文件的安全](#.E4.BF.9D.E8.AF.81_authorized_keys_.E6.96.87.E4.BB.B6.E7.9A.84.E5.AE.89.E5.85.A8)
    *   [4.2 禁用密码登录](#.E7.A6.81.E7.94.A8.E5.AF.86.E7.A0.81.E7.99.BB.E5.BD.95)
    *   [4.3 双因素认证与公钥](#.E5.8F.8C.E5.9B.A0.E7.B4.A0.E8.AE.A4.E8.AF.81.E4.B8.8E.E5.85.AC.E9.92.A5)
*   [5 SSH agents](#SSH_agents)
    *   [5.1 ssh-agent](#ssh-agent)
        *   [5.1.1 ssh-agent 作为包装程序运行](#ssh-agent_.E4.BD.9C.E4.B8.BA.E5.8C.85.E8.A3.85.E7.A8.8B.E5.BA.8F.E8.BF.90.E8.A1.8C)
    *   [5.2 GnuPG](#GnuPG)
    *   [5.3 Keychain](#Keychain)
        *   [5.3.1 另一种启动 keychain 的方式](#.E5.8F.A6.E4.B8.80.E7.A7.8D.E5.90.AF.E5.8A.A8_keychain_.E7.9A.84.E6.96.B9.E5.BC.8F)
    *   [5.4 envoy](#envoy)
        *   [5.4.1 利用 KDE 电子钱包存储密码短语并和 envoy 配合工作](#.E5.88.A9.E7.94.A8_KDE_.E7.94.B5.E5.AD.90.E9.92.B1.E5.8C.85.E5.AD.98.E5.82.A8.E5.AF.86.E7.A0.81.E7.9F.AD.E8.AF.AD.E5.B9.B6.E5.92.8C_envoy_.E9.85.8D.E5.90.88.E5.B7.A5.E4.BD.9C)
    *   [5.5 pam_ssh](#pam_ssh)
        *   [5.5.1 pam_ssh 已知问题](#pam_ssh_.E5.B7.B2.E7.9F.A5.E9.97.AE.E9.A2.98)
    *   [5.6 GNOME Keyring](#GNOME_Keyring)
*   [6 疑难排解](#.E7.96.91.E9.9A.BE.E6.8E.92.E8.A7.A3)
    *   [6.1 使用 kdm](#.E4.BD.BF.E7.94.A8_kdm)

## 背景

SSH 密钥对总是成双出现的，一把公钥，一把私钥。公钥可以自由的放在您所需要连接的 SSH 服务器上，而私钥必须稳妥的保管好。

所谓"公钥登录"，原理很简单，就是用户将自己的公钥储存在远程主机上。登录的时候，远程主机会向用户发送一段随机字符串，用户用自己的私钥加密后，再发回来。远程主机用事先储存的公钥进行解密，如果成功，就证明用户是可信的，直接允许登录 shell，不再要求密码。这样子，我们即可保证了整个登录过程的安全，也不会受到中间人攻击。

## 生成密钥对

我们可以使用 `ssh-keygen` 命令生成密钥对

```
$ ssh-keygen -t ecdsa -b 521 -C "$(whoami)@$(hostname)-$(date -I)"

```

```
Generating public/private ecdsa key pair.
Enter file in which to save the key (/home/username/.ssh/id_ecdsa):
Enter passphrase (empty for no passphrase):
Enter same passphrase again:
Your identification has been saved in /home/username/.ssh/id_ecdsa.
Your public key has been saved in /home/username/.ssh/id_ecdsa.pub.
The key fingerprint is:
dd:15:ee:24:20:14:11:01:b8:72:a2:0f:99:4c:79:7f username@localhost-2011-12-22
The key's randomart image is:
+--[ECDSA  521]---+
|     ..oB=.   .  |
|    .    . . . . |
|  .  .      . +  |
| oo.o    . . =   |
|o+.+.   S . . .  |
|=.   . E         |
| o    .          |
|  .              |
|                 |
+-----------------+
```

在上面这个例子中，`ssh-keygen` 生成了一对长度为 521 bit (`-b 521`) 的 ECDSA (`-t ecdsa`) 加密的密钥对，comment 为 `-C "$(whoami)@$(hostname)-$(date -I)"`。而 [randomart image](http://www.cs.berkeley.edu/~dawnsong/papers/randomart.pdf) 是 OpenSSH 5.1 引入的一种简单的识别指纹 (fingerprint) 的图像。

### 选择合适的加密方式

椭圆曲线数字签名算法 (ECDSA) 生成的密钥更小，安全性更高。OpenSSH 5.7 建议默认使用 ECDSA，详情参见 [OpenSSH 5.7 Release Notes](http://www.openssh.com/txt/release-5.7)。较旧的 OpenSSH 版本可能不支持 ECDSA 密钥，需要注意。而一些厂商因专利问题，暂未提供 ECDSA 的实现。

**注意:** 截至 2014 年06 月 10 日，这个 [GNOME bug](https://bugzilla.gnome.org/show_bug.cgi?id=641082) 导致 Gnome Keyring 暂不支持 ECDSA。

如果您要生成 RSA (768-16384 bit) 或者 DSA (1024 bit) 密钥对，需要使用 `-t rsa` 或者 `-t dsa`，并修改 `-b` 选项。`-b` 可以省略，`ssh-keygen` 会生成一个默认大小的密钥对。

**注意:** 这些密钥对是用于认证的，选择更加复杂的密钥类型并不会在登录时加重您的 CPU 负担。

### 选择密钥存储位置以及密码短语

输入 `ssh-keygen` 时，它会询问您将密钥对保存到何处，文件名如何命令等。默认情况下，密钥对保存到 `~/.ssh` 下，文件名则根据加密类型自动命名为 `id_ecdsa` (私钥)，`id_ecdsa.pud` (公钥)。建议您采用默认的存储位置和文件名。

而在 `ssh-keygen` 请求您输入一个密码短语时，您应该输入一些难以猜到的短语。如果短语足够随机和复杂，则私钥落入贼人之手时就不会容易被破解掉。

当然，您也可以不输入任何密码短语，也能够生成所需的密钥对。虽然这用起来挺方便的，但是您应该知道这会很危险。在没有输入密码短语的情况下，您的私钥未经加密就存储在您的硬盘上，任何人拿到您的私钥都可以随意的访问对应的 SSH 服务器。还有一种情况，如果您不是 `root` 用户，则该机器上的 `root` 用户可以完全拥有您的密钥对，因为他的权限是最大的。

#### 不修改密钥对的情况下修改密码短语

您可以使用 `ssh-keygen` 命令来修改密码短语，而无需改动密钥对。假设您要修改的密钥对使用 RSA 加密，输入以下命令即可：

```
$ ssh-keygen -f ~/.ssh/id_rsa -p

```

#### 管理多组密钥对

您可以创建 `~/.ssh/config` 来管理多组密钥对，每一个 SSH 服务器对应一组密钥对。或者，您甚至可以对所有的 SSH 服务器使用同一组密钥对。不过如果您觉得这样不合适，还是编辑配置文件：

 `~/.ssh/config` 

```
Host SERVERNAME1
  IdentitiesOnly yes
  IdentityFile ~/.ssh/id_rsa_SERVER1
  # CheckHostIP yes
  # Port 22
Host SERVERNAME2
  IdentitiesOnly yes
  IdentityFile ~/.ssh/id_rsa_SERVER2
  # CheckHostIP no
  # Port 2177
ControlMaster auto
ControlPath /tmp/%r@%h:%p
```

更多选项帮助请参考

```
$ man ssh_config 5

```

## 将公钥复制到远程服务器上

创建好密钥对之后，您需要将公钥上传到远程服务器上，以便用于 SSH 密钥认证登录。公钥文件名和私钥文件名相同，只不过公钥文件带有扩展名 `.pub` 而私钥文件名则没有。千万不要将私钥上传，私钥应该保存在本地。

### 简单的方法

**注意:** 如果您的远程服务器默认使用的是 non-`sh` 的 shell，比如 `tcsh`，则此方法可能不奏效。详情参见这个 [bug](https://bugzilla.redhat.com/show_bug.cgi?id=1045191)。

**注意:** 如果使用以下两种方法外的方法请不要忘记注册公钥文件，您只需要命令

```
$ cat ~/.ssh/id_ecdsa.pub >> ~/.ssh/authorized_keys

```

如果您的私钥文件为 `~/.ssh/id_rsa.pub`，您只需要输入命令

```
$ ssh-copy-id remote-server.org

```

如果您的远程服务器用户名与本地的不同，您需要指明用户名

```
$ ssh-copy-id username@remote-server.org

```

如果您的私钥文件名不是默认的，您会得到错误 `/usr/bin/ssh-copy-id: ERROR: No identities found`。这种情况下，您需要修改命令为

```
$ ssh-copy-id -i ~/.ssh/id_ecdsa.pub username@remote-server.org

```

如果远程服务器监听端口不是 22,您也需要指明端口

```
$ ssh-copy-id -i ~/.ssh/id_ecdsa.pub -p 221 username@remote-server.org

```

### 传统的方法

使用命令

```
$ scp ~/.ssh/id_ecdsa.pub username@remote-server.org:

```

将公钥上传到服务器。注意，该命令最末的 `:` 不可省略。上传成功之后，先使用口令登录到服务器，将公钥文件重命名为 `authorized_keys`，并移动到 `~/.ssh` 下，若 `~/.ssh` 不存在则新建一个。

```
$ ssh username@remote-server.org
username@remote-server.org's password:
$ mkdir ~/.ssh
$ cat ~/id_ecdsa.pub >> ~/.ssh/authorized_keys
$ rm ~/id_ecdsa.pub
$ chmod 600 ~/.ssh/authorized_keys

```

上面最后两个命令移除服务器上的公钥，并设置 `authorized_keys` 的权限为只有您，也即文件拥有者，有读写权限。

## 安全性

### 保证 authorized_keys 文件的安全

为了保证安全，您应该阻止其他用户添加新的公钥。

将 `authorized_keys` 的权限设置为对拥有者只读，其他用户没有任何权限：

```
$ chmod 400 ~/.ssh/authorized_keys

```

为保证 `authorized_keys` 的权限不会被改掉，您还需要设置该文件的 immutable 位权限：

```
# chattr +i ~/.ssh/authorized_keys

```

然而，用户还可以重命名 `~/.ssh`，然后新建新的 `~/.ssh` 目录和 `authorized_keys` 文件。要避免这种情况，您需要设置 `~./ssh` 的 immutable 位权限：

```
# chattr +i ~/.ssh

```

**注意:** 如果您需要添加新的公钥，您需要移除 `authorized_keys` 的 immutable 位权限。然后，添加好新的公钥之后，按照上述步骤重新加上 immutable 位权限。

### 禁用密码登录

将公钥上传到 SSH 服务器上之后，您就不再需要输入 SSH 账户密码来登录了。直接使用账户密码登录容易受到暴力破解的攻击。倘若您没有提供 SSH 私钥，默认情况下，SSH 服务器就会让您直接使用密码登录，这就有可能让不法之徒来猜测您的密码，有一定的安全隐患。要禁用这一行为，您需要编辑 SSH 服务器上的 `/etc/ssh/sshd_config`：

 `/etc/ssh/sshd_config` 

```
PasswordAuthentication no
ChallengeResponseAuthentication no
```

### 双因素认证与公钥

从 OpenSSH 6.2 开始，您可以使用 `AuthenticationMethods` 选项来自己添加工具链进行认证。这样就可以配合公钥使用双因素认证了。

谷歌身份验证器设置请参考 [Google Authenticator](/index.php/Google_Authenticator "Google Authenticator")。

如果您使用 PAM (Pluggable Authentication Module，插入式验证模块)，编辑下面这几行：

 `/etc/ssh/sshd_config` 

```
ChallengeResponseAuthentication yes
AuthenticationMethods publickey,keyboard-interactive:pam

```

 `/etc/pam.d/sshd` 

```
#%PAM-1.0
auth required pam_google_authenticator.so

```

如果您设置 PAM 仅使用 `pam_google_authenticator.so`，则 `sshd` 则会采用双因素认证，而无需密码。如果双因素认证失败，即使有有效的公钥，_sshd_ 也不允许登录。您可以加上 `nullok` 选项来允许用户使用公钥登录：

 `/etc/pam.d/sshd` 

```
#%PAM-1.0
auth required pam_google_authenticator.so nullok

```

## SSH agents

如果您的私钥使用密码短语来加密了的话，每一次使用 SSH 密钥对进行登录的时候，您都必须输入正确的密码短语。

而 SSH agent 程序能够将您的已解密的私钥缓存起来，在需要的时候提供给您的 SSH 客户端。这样子，您就只需要将私钥加入 SSH agent 缓存的时候输入一次密码短语就可以了。这为您经常使用 SSH 连接提供了不少便利。

SSH agent 一般会设置成在登录会话的时候自动启动，并在整个会话中保持运行。有不少的 SSH agent 供您选择，我们将为您介绍几种常用的 SSH agent，您可以根据您的需要进行选择。

### ssh-agent

ssh-agent 是 OpenSSH 自带的一个 SSH agent，它可以直接作为 SSH agent 来使用，或者作为其他 SSH agent 的后端。`ssh-agent` 运行时会自动 fork 它自身，然收打印出其所需的环境变量。

```
$ ssh-agent
SSH_AUTH_SOCK=/tmp/ssh-vEGjCM2147/agent.2147; export SSH_AUTH_SOCK;
SSH_AGENT_PID=2148; export SSH_AGENT_PID;
echo Agent pid 2148;

```

要使用这些环境变量，您需要使用 `eval` 命令来运行它

```
$ eval $(ssh-agent)
Agent pid 2157

```

您可以将上述命令添加到 `~/.bash_profile`，以便您启动 [登录外壳](/index.php/Bash_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)#.E7.99.BB.E5.BD.95.E5.A4.96.E5.A3.B3 "Bash (简体中文)") 的时候它自动运行。

```
$ echo 'eval $(ssh-agent)' >> ~/.bash_profile

```

如果您想要所有的用户都可以使用 `ssh-agent`，可以直接把上述命令加入到 `/etc/profile`。

```
# echo 'eval $(ssh-agent)' >> /etc/profile

```

`ssh-agent` 运行起来之后，您还需要将您的私钥加入它的缓存。

```
$ ssh-add ~/.ssh/id_ecdsa
Enter passphrase for /home/user/.ssh/id_ecdsa:
Identity added: /home/user/.ssh/id_ecdsa (/home/user/.ssh/id_ecdsa)

```

如果您想要在登录 shell 的时候自动添加您的私钥到 `ssh-agent` 的缓存，您需要在 `~/.bash_profile` 加入以下命令：

```
ssh-add

```

如果您的私钥已用密码短语加密，`ssh-add` 会提示您输入密码短语。输入争取的密码短语之后，您在*当前会话*中就不需要再次输入密码短语就能够使用密钥对进行 SSH 登录了。

如果您想要在用到私钥的时候再输入密码短语，您可以添加以下命令到 `~/.bashrc`：

```
$ ssh-add -l >/dev/null || alias ssh='ssh-add -l >/dev/null || ssh-add && unalias ssh; ssh'

```

但是这样做有个缺点，每次启动 [登录外壳](/index.php/Bash_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)#.E7.99.BB.E5.BD.95.E5.A4.96.E5.A3.B3 "Bash (简体中文)") 都会产生一个 `ssh-agent` 实例，并在会话期间一直运行。不久之后，您的系统中就会有多个根本不再需要的 `ssh-agent` 进程在运行。稍后，我们将为您介绍其他 `ssh-agent` 前端，它们能够避免这个问题。

#### ssh-agent 作为包装程序运行

根据加州大学伯克利分校实验室的这份 [ssh-agent 教程](http://upc.lbl.gov/docs/user/sshagent.shtml)，还有一个随 X 会话启动 `ssh-agent` 的方法，该法用于您在使用命令 `startx` 启动 X的时候，可以在命令前加上 `ssh-agent`：

```
$ ssh-agent startx

```

您也可以在 `.bash_aliases` 中设置别名以方便使用：

```
alias startx='ssh-agent startx'

```

这样做可以避免多个会话中存在多余的 `ssh-agent` 进程，实际上，整个 X 会话中只有一个 `ssh-agent` 在运行了。

### GnuPG

**注意:** GnuPG < 2.0.21 不支持 ECC。GnuPG >= 2.0.21 支持 ECDSA。

[GnuPG](/index.php/GnuPG "GnuPG") 可以从 [官方软件仓库](/index.php/Official_repositories_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Official repositories (简体中文)") 安装 [gnupg](https://www.archlinux.org/packages/?name=gnupg)。如果您已经在使用 GnuPG，您也许想要 GnuPG 来缓存您的私钥。当然咯，有些用户比较喜欢在 GnuPG 对话框来输入 PIN 码，这样子管理密码短语也是不错的选择。

{注意|如果您使用 KDE 作为桌面环境，且安装了 [kde-agent](https://www.archlinux.org/packages/?name=kde-agent) 的话，您只需在 `~/.gnupg/gpg-agent.conf` 中设置 `enable-ssh-support`。否则，请继续阅读。}

要使用 GnuPG agent，您首先要启动 _gpg-agent_，并加上 `--enable-ssh-support` 选项。比如，记得给脚本加上可执行权限：

 `/etc/profile.d/gpg-agent.sh` 

```
#!/bin/sh

# Start the GnuPG agent and enable OpenSSH agent emulation
gnupginf="${HOME}/.gpg-agent-info"

if pgrep -x -u "${USER}" gpg-agent >/dev/null 2>&1; then
    eval `cat $gnupginf`
    eval `cut -d= -f1 $gnupginf | xargs echo export`
else
    eval `gpg-agent -s --enable-ssh-support --daemon --write-env-file "$gnupginf"`
fi

```

`gpg-agent` 运行起来之后，您就可以使用 `ssh-add` 命令来认证密钥对，正如上文中 `ssh-agent` 做的那样。已认证的密钥对列表保存在 `~/.gnupg/sshcontrol` 文件中。此后，在需要使用您的私钥密码短语是，GnuPG 会显示一个对话框让您输入。您可以通过配置文件 `~/.gnupg/gpg-agent.conf` 来管理您的密码短语缓存。比如，下面这个例子说明如何使用 `gpg-agent` 来缓存您的密钥 3 小时：

 `~/.gnupg/gpg-agent.conf` 

```
  # Cache settings
  default-cache-ttl 10800
  default-cache-ttl-ssh 10800

```

您还可以在此文件中设置 PIN 输入框 (GTK、QT 或者 ncurses 版本) 等内容。

**注意:** 您必须创建一个 `gpg-agent.conf` 文件，`write-env-file` 变量必须设置好，以便允许 `gpg-agent` 在 SSH 登录过程中的使用。

 `~/.gnupg/gpg-agent.conf` 

```
  # Environment file
  write-env-file /home/username/.gpg-agent-info

  # Keyboard control
  #no-grab

  # PIN entry program
  #pinentry-program /usr/bin/pinentry-curses
  #pinentry-program /usr/bin/pinentry-qt4
  #pinentry-program /usr/bin/pinentry-kwallet
  pinentry-program /usr/bin/pinentry-gtk-2

```

要使用 `gpg-agent` 作为 SSH agent，您需要 source & export `gpg-agent` 写入 `~/.gpg-agent-info` 文件的环境变量，也就是 `write-env-file` 所指的文件。

 `~/.bashrc` 

```
...

if [ -f "${HOME}/.gpg-agent-info" ]; then
  . "${HOME}/.gpg-agent-info"
  export GPG_AGENT_INFO
  export SSH_AUTH_SOCK
fi

```

### Keychain

[Keychain](http://www.funtoo.org/Keychain) 是一个用来方便管理 SSH 密钥对的程序，它能尽最大努力去减少对用户的打扰。实际上，它就是一个 shell 脚本，驱动 `ssh-agent` 或者 `gpg-add` 来工作。一个值得注意的特性是，keychain 在多个会话中重复使用同一个 `ssh-agent` 进程。这意味着您只需要在机器启动时输入一次密码短语即可。

您可以从 [官方软件仓库](/index.php/Official_repositories_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Official repositories (简体中文)") 安装 [keychain](https://www.archlinux.org/packages/?name=keychain)。

将下列内容加入到 `~/.bash_profile`：

 `~/.bash_profile` 

```
eval $(keychain --eval --agents ssh -Q --quiet id_ecdsa)

```

如有需要，请把 `id_ecdsa` 换成您的私钥路径。如果您使用的 shell 不兼容 [Bash (简体中文)](/index.php/Bash_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Bash (简体中文)")，请参考 `keychain --help` 或者 `man keychain`。

要测试 keychain 是否配置成功，请注销当前会话，重新登录。如果这是您第一次运行 keychain，则您会被要求输入私钥的密码短语。因为 keychain 复用已成功登录的会话中的 `ssh-agent` 进程，所以您再次登录是就无需输入密码短语了。当您重启机器时，您才会被要求再次输入密码短语。

#### 另一种启动 keychain 的方式

调用 keychain 的方法有很多种，您可以自行尝试，找到最适合您的那一种。`keychain` 命令提供了不少的选项来进行设置，您可以参考它的手册。

这里我们介绍其中一种不错的方法，以 `root` 身份创建 `/etc/profile.d/keychain.sh`，并添加下列内容：

 `/etc/profile.d/keychain.sh` 

```
/usr/bin/keychain -Q -q --nogui ~/.ssh/id_ecdsa
[[ -f $HOME/.keychain/$HOSTNAME-sh ]] && source $HOME/.keychain/$HOSTNAME-sh

```

记得给该脚本加上可执行权限：

```
# chmod +x /etc/profile.d/keychain.sh

```

如果您想要在第一次使用私钥时才输入密码短语，而非一开机登录就输入的话，您可以将下列内容加入 `~/.bashrc`：

```
alias ssh='eval $(/usr/bin/keychain --eval --agents ssh -Q --quiet ~/.ssh/id_ecdsa) && ssh'

```

这样子，当您开机后首次使用密钥对连接 SSH 服务器时，您才需要提供密码短语。但是，这只在 `~/.bashrc` 可用的情况下才奏效，所以您应该保证第一次使用 SSH 连接时是在终端下进行的。

### envoy

[Envoy](https://github.com/vodik/envoy) 算是 keychain 的一个替代品，您可以从 [官方软件仓库](/index.php/Official_repositories_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Official repositories (简体中文)") 下载安装 [envoy](https://www.archlinux.org/packages/?name=envoy)，或者从 [AUR](/index.php/Arch_User_Repository_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Arch User Repository (简体中文)") 安装 [envoy-git](https://aur.archlinux.org/packages/envoy-git/)。

安装完成之后，使用以下命令启用 envoy 套接字 (socket)：

```
# systemctl enable envoy@ssh-agent.socket

```

加入您的外壳 rc 文件：

```
 envoy -t ssh-agent -a _ssh_key_
 source <(envoy -p)

```

如果您的私钥为 `~/.ssh/id_rsa`, `~/.ssh/id_dsa`, `~/.ssh/id_ecdsa`，或者 `~/.ssh/identity`，则不需要 `-a _ssh_key_` 参数。

#### 利用 KDE 电子钱包存储密码短语并和 envoy 配合工作

如果您的密码短语很长很复杂，那记忆起来是有点痛苦。您可以让 KDE 电子钱包来为您记住密码短语哦！

安装位于 [官方软件仓库](/index.php/Official_repositories_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Official repositories (简体中文)") 的 [ksshaskpass](https://www.archlinux.org/packages/?name=ksshaskpass) 和 [kdeutils-kwalletmanager](https://www.archlinux.org/packages/?name=kdeutils-kwalletmanager)，然后按照上文介绍的方法启用 envoy 套接字。

添加一个脚本到 `~/.kde4/Autostart/`，输入以下内容：

 `~/.kde4/Autostart/ssh-agent.sh` 

```
#!/bin/sh
envoy -t ssh-agent -a _ssh_key_

```

记得加上可执行权限：

```
$ chmod +x ~/.kde4/Autostart/ssh-agent.sh

```

添加一个脚本到 `~/.kde4/env/`，加入以下内容：

 `~/.kde4/env/ssh-agent.sh` 

```
#!/bin/sh
eval $(envoy -p)
```

同样不要忘记加上可执行权限：

```
$ chmod +x ~/.kde4/env/ssh-agent.sh

```

当您登录到 KDE 桌面环境时，它就会自动运行脚本 `ssh-agent.sh`。这样子就能够调用 `ksshaskpass`，当 {{ic|envoy} 调用 {{ic|ssh-agent} 时，{{ic|ksshaskpass} 就会请求您输入 KDE 电子钱包的密码了。而 KDE 电子钱包则会保存您的密码短语，在 `ssh-agent` 需要的时候由 KDE 电子钱包提供。

### pam_ssh

[pam_ssh](http://pam-ssh.sourceforge.net/) 项目为 SSH 私钥提供了一个 [插入式验证模块](https://en.wikipedia.org/wiki/Pluggable_authentication_module "wikipedia:Pluggable authentication module") (PAM)。当您的密码短语与系统登录用户密码相同的时候，可以为您减去再次输入密码的麻烦。开机登录时，您需要输入您的登录密码，如有需要，还要输入 ssh 密钥的密码短语。您成功登录系统之后，`ssh-agent` 则会在整个会话期间缓存您已解密的私钥。

要在 tty 模式下使用 pam_ssh，您需要安装位于 [AUR](/index.php/AUR "AUR") 的 [pam_ssh](https://aur.archlinux.org/packages/pam_ssh/) 。

**注意:** pam_ssh 2.0 要求所有用于认证的私钥文件必须保存在 `~/.ssh/login-keys.d/` 下。

您可以为您的私钥文件创建一个软链接，并放到 `~/.ssh/login-keys.d/`：

```
$ mkdir ~/.ssh/login-keys.d/
$ cd ~/.ssh/login-keys.d/
$ ln -s ../id_rsa

```

注意将上述例子中的 `id_rsa` 换成您对应的私钥文件。

编辑 `/etc/pam.d/login`，将下面例子中高亮加粗的那几行加进去。请注意配置内容的顺序会影响到登录行为，应当按照例子中的来。

**警告:** PAM 配置丢失会导致系统中所有的用户被锁定。因此，您必须在保存任何 PAM 配置并生效之前，做好配置文件的备份，准备好一份 live CD，以防万一用户被锁定时还有办法恢复原样。您可以参阅 IBM 的 [这篇文章](http://www.ibm.com/developerworks/linux/library/l-pam/index.html) 详细了解一下 PAM 的配置。

 `/etc/pam.d/login` 

```
#%PAM-1.0

auth       required     pam_securetty.so
auth       requisite    pam_nologin.so
auth       include      system-local-login
**auth       optional     pam_ssh.so        try_first_pass**
account    include      system-local-login
session    include      system-local-login
**session    optional     pam_ssh.so**
```

在上面的例子中，登录认证初始化进程如平常那样启动，用户要输入登录密码。`try_first_pass` 选项传递给 `pam_ssh` 模块，它会尝试使用用户密码作为密码短语去解密 `~/.ssh/login-keys.d/` 下的私钥。如果用户密码与密码短语一致，那么私钥可以被解密，用户就无需再次输入相同的密码。如果两者不同，ssh_pam 模块会在用户正确输入登录密码之后输入密码短语。`optional` 可以保证 `~/.ssh/login-keys.d/` 下没有私钥时，用户也能够正常登录系统。这种情况下，ssh_pam 模块对于没有私钥的用户来说就等于无。

如果您使用其他方式登录，比如使用登录管理器 [SLiM (简体中文)](/index.php/SLiM_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "SLiM (简体中文)") 或者 [XDM (简体中文)](/index.php/XDM_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "XDM (简体中文)")，您必须按照类似的方法来编辑 PAM 配置文件，才能正常工作。`/etc/pam.d/` 目录下保存有默认的配置文件，您可以参考默认配置文件来进行配置。

#### pam_ssh 已知问题

pam_ssh 并不广泛使用，其提供的文档也比较少。您应该注意一下该软件包的一些使用限制，比如：

*   pam_ssh < 2.0 不支持 ECDSA，您必须使用 RSA 或者 DSA。
*   pam_ssh 调用的 `ssh-agent` 进程仅限于当前会话，不能在多个会话中共享。上文提到的 [keychain](#Keychain) 前端可以避免这个问题。

### GNOME Keyring

如果您使用 Gnome，您也可以使用 Gnome 钥匙圈 (GNOME Keyring) 作为 SSH agent。详情请参考 [GNOME Keyring](/index.php/GNOME_Keyring "GNOME Keyring")。

## 疑难排解

如果您的 SSH 服务器忽略了您的 SSH 密钥对，您需要检查一下相关文件的权限是否正确。

本地机器上：

```
$ chmod 700 ~/
$ chmod 700 ~/.ssh
$ chmod 600 ~/.ssh/id_ecdsa

```

服务器上：

```
$ chmod 700 ~/
$ chmod 700 ~/.ssh
$ chmod 600 ~/.ssh/authorized_keys

```

如果这样还不能解决您的问题，您可以试试将 `sshd_config` 中的 `StrictModes` 设为 `no`。如果将 `StrictModes` 关闭就能够顺利认证的话，说明相关文件的权限还没有改对。

**小贴士:** 为保证安全，记得把 `StrictModes` 设为 `yes`。

请确认您的 SSH 服务器支持您所使用的密钥类型， 可以实施 RSA 或者 DSA。某些服务器可能不支持 ECDSA 密钥。

如果还不行，打开 sshd 的 debug 模式，查看连接时的日志输出，查找原因吧：

```
# /usr/bin/sshd -d

```

### 使用 kdm

KDM 并不能直接启动 `ssh-agent`，KDM 要用 [kde-agent](https://www.archlinux.org/packages/?name=kde-agent) 来启动 `ssh-agent`，但是 `kde-agent` 自 20140102-1 开始已经被 [移除](https://projects.archlinux.org/svntogit/packages.git/commit/trunk?h=packages/kde-agent&id=1070467b0f74b2339ceca2b9471d1c4e2b9c9c8f)。

为了让 KDE 启动时启动 `ssh-agent`，您可以创建一个脚本用于登录时启动 `ssh-agent`，还有一个脚本用于注销时杀死进程：

```
echo -e '#!/bin/sh\n[ -n "$SSH_AGENT_PID" ] || eval "$(ssh-agent -s)"' > ~/.kde4/env/ssh-agent-startup.sh
echo -e '#!/bin/sh\n[ -z "$SSH_AGENT_PID" ] || eval "$(ssh-agent -k)"' > ~/.kde4/shutdown/ssh-agent-shutdown.sh
chmod 755 ~/.kde4/env/ssh-agent-startup.sh ~/.kde4/shutdown/ssh-agent-shutdown.sh

```