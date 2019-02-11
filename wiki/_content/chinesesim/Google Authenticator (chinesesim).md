**翻译状态：** 本文是英文页面 [Google_Authenticator](/index.php/Google_Authenticator "Google Authenticator") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2017-07-26，点击[这里](https://wiki.archlinux.org/index.php?title=Google_Authenticator&diff=0&oldid=482958)可以查看翻译后英文页面的改动。

[Google Authenticator](https://github.com/google/google-authenticator) 使用一次性密码(**O**ne-**t**ime **P**asscodes)进行两步验证。iOS、Android 甚至 Blackberry 上都提供了 OTP 生成器应用。与 [S/KEY Authentication](/index.php/S/KEY_Authentication "S/KEY Authentication") 类似，两步验证将集成在Linux的 [PAM](/index.php/PAM "PAM") 系统中。此指南显示了此两步验证的安装与配置。

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 安装](#安装)
*   [2 设置插入式验证模块(**P**luggable **A**uthentication **M**odules)](#设置插入式验证模块(Pluggable_Authentication_Modules))
*   [3 生成密钥文件](#生成密钥文件)
*   [4 设置两步验证软件](#设置两步验证软件)
*   [5 测试](#测试)
*   [6 存储位置](#存储位置)
*   [7 用于桌面登陆](#用于桌面登陆)

## 安装

安装 [libpam-google-authenticator](https://www.archlinux.org/packages/?name=libpam-google-authenticator) 软件包或开发者版本 [google-authenticator-libpam-git](https://aur.archlinux.org/packages/google-authenticator-libpam-git/)。

## 设置插入式验证模块(**P**luggable **A**uthentication **M**odules)

**Warning:** 若通过 SSH 进行 Google Authenticator 的所有配置，在完成所有配置并测试正常之前，请勿关闭 SSH 会话，否则可能会无法登录。此外，最好在激活 PAM 之前生成密钥文件。

通常远程登录才需要设置两步验证。PAM的配置是在文件`/etc/pam.d/sshd`内。如果想全局使用谷歌两步身份验证，请**小心**的修改`/etc/pam.d/sshd`，以免锁定自己从而不能登录。在本指南中，我们将在本地会话中安全的编辑文件`/etc/pam.d/sshd`。

要同时输入 Unix 密码**与**两步验证码登录，请在 `/etc/pam.d/sshd`文件的system-remote-login行之上添加`pam_google_authenticator.so`：

```
 **auth            required        pam_google_authenticator.so**
 auth            include         system-remote-login
 account         include         system-remote-login
 password        include         system-remote-login
 session         include         system-remote-login

```

这样将会首先询问两步验证码，验证成功后才会询问 Unix 密码。改变上述添加于`/etc/pam.d/sshd`文件的配置顺序则会改变验证顺序。

**Warning:** 只有生成密钥文件(见下)的用户才会被允许SSH登录

要允许使用 Unix 密码**或**两步验证码登录，请修改:

```
 auth            **sufficient**      pam_google_authenticator.so

```

在文件`/etc/ssh/**sshd_config**`内开启质疑-应答认证(challenge-response authentication)：

```
 ChallengeResponseAuthentication yes

```

最后 [重新加载](/index.php/Reload "Reload") `sshd`服务

**Warning:** 如果设置使用密钥登陆并禁止密码登录，OpenSSH 会忽略如上所有的配置。但是在 OpenSSh 6.2 版本以后，允许使用基于密钥和两步验证的验证。请参阅 [Secure Shell#Two-factor authentication and public keys](/index.php/Secure_Shell#Two-factor_authentication_and_public_keys "Secure Shell")

## 生成密钥文件

**Tip:** 安装 [qrencode](https://www.archlinux.org/packages/?name=qrencode) 以生成二维码. 扫描二维码以自动配置两步验证器.

每一个想要使用两步验证的用户需要在其用户目录生成一个密钥文件，使用命令*google-authenticator*来完成：

```
   $ google-authenticator
   Do you want authentication tokens to be time-based (y/n) y
   <这里是自动生成的二维码>
   Your new secret key is: ZVZG5UZU4D7MY4DH          (密钥)
   Your verification code is 269371                  (验证码)
   Your emergency scratch codes are:                 (备用令牌码)
     70058954
     97277505
     99684896
     56514332
     82717798

   Do you want me to update your "/home/username/.google_authenticator" file (y/n) y

   Do you want to disallow multiple uses of the same authentication
   token? This restricts you to one login about every 30s, but it increases
   your chances to notice or even prevent man-in-the-middle attacks (y/n) y
   (是否拒绝多次使用使用相同的令牌？这将限制你每30s仅能登录一次，但会提醒/阻止中间人攻击。)

   By default, tokens are good for 30 seconds and in order to compensate for
   possible time-skew between the client and the server, we allow an extra
   token before and after the current time. If you experience problems with poor
   time synchronization, you can increase the window from its default
   size of 1:30min to about 4min. Do you want to do so (y/n) n
   (是否将窗口时间由1分30秒增加到约4分钟？这将缓解时间同步问题。)

   If the computer that you are logging into is not hardened against brute-force
   login attempts, you can enable rate-limiting for the authentication module.
   By default, this limits attackers to no more than 3 login attempts every 30s.
   Do you want to enable rate-limiting (y/n) y
   (是否启用此模块的登录频率限制，登录者将会被限制为最多在30秒内登录3次。)

```

建议您将**备用令牌码**保存在安全的地方，因为当丢失手机或其他原因不能使用两步验证器时，只能使用**备用令牌码**登录。它们同时也被保存在`~/.google_authenticator`。

## 设置两步验证软件

从谷歌市场安装两步验证器[Android market](http://m.google.com/authenticator)(如[FreeOTP](https://play.google.com/store/apps/details?id=org.fedorahosted.freeotp))，或者安装[F-Droid](https://f-droid.org/repository/browse/?fdfilter=google&fdid=com.google.android.apps.authenticator2)。在软件中创建一个新验证，输入密钥(如例子中的'ZVZG5UZU4D7MY4DH')或扫描二维码来导入密钥，并输入验证码。

软件现在应该会显示一个每30秒更新的验证码。

## 测试

连接SSH服务器:

```
 $ ssh hostname
 login as: <username>
 Verification code: <令牌码/备用令牌码>
 Password: <password>
 $

```

## 存储位置

如果想要改变密钥存储位置，请使用`--secret`参数:

```
$ google-authenticator --secret="/**PATH_FOLDER**/**USERNAME**"

```

然后更改`/etc/pam.d/sshd`内的路径配置:

 `/etc/pam.d/sshd`  `auth required pam_google_authenticator.so user=root secret=/**PATH_FOLDER**/${USER}` 

`user=root` 用于强制PAM使用root用户权限来搜索文件。

另外请注意，密钥文件的所有者是root，生成文件的用户只能读取文件(chmod: `400`)。

```
$ chown root.root /**PATH_FILE**/**SECRET_KEY_FILES**
  chmod 400 /**PATH_FILE**/**SECRET_KEY_FILES**

```

## 用于桌面登陆

谷歌两步认证插件可以同时用于控制台与 GNOME 桌面登录。只需要在文件 `/etc/pam.d/login` 或 `/etc/pam.d/gdm-password` 内加入

```
   auth required pam_google_authenticator.so

```