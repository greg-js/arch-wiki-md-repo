相关文章

*   [Arch Security Team](/index.php/Arch_Security_Team "Arch Security Team")
*   [General recommendations (简体中文)](/index.php/General_recommendations_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "General recommendations (简体中文)")
*   [PAM (简体中文)](/index.php/PAM_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "PAM (简体中文)")
*   [Capabilities (简体中文)](/index.php/Capabilities_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Capabilities (简体中文)")
*   [List of Applications/Security](/index.php/List_of_Applications/Security "List of Applications/Security")

**翻译状态：** 本文是英文页面 [Security](/index.php/Security "Security") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2019-02-04，点击[这里](https://wiki.archlinux.org/index.php?title=Security&diff=0&oldid=565780)可以查看翻译后英文页面的改动。

本文主要包括 [加固](https://en.wikipedia.org/wiki/Hardening_(computing) Arch Linux 系统的常用建议与最佳实践。

## Contents

*   [1 基本概念](#基本概念)
*   [2 密码](#密码)
    *   [2.1 选择高强度的密码](#选择高强度的密码)
    *   [2.2 维护密码安全](#维护密码安全)
    *   [2.3 密码的散列值](#密码的散列值)
    *   [2.4 用 pam_cracklib 强制使用强密码](#用_pam_cracklib_强制使用强密码)
*   [3 存储](#存储)
    *   [3.1 磁盘加密](#磁盘加密)
    *   [3.2 文件系统](#文件系统)
        *   [3.2.1 挂载点](#挂载点)
    *   [3.3 文件访问权限](#文件访问权限)
*   [4 账户安全设置](#账户安全设置)
    *   [4.1 在失败的登录尝试后强制延时一段时间](#在失败的登录尝试后强制延时一段时间)
    *   [4.2 在三次登录尝试失败后锁定用户](#在三次登录尝试失败后锁定用户)
    *   [4.3 限制进程数量](#限制进程数量)
    *   [4.4 避免用 root 运行 Xorg](#避免用_root_运行_Xorg)
*   [5 限制 root 权限](#限制_root_权限)
    *   [5.1 用 sudo 替代 su](#用_sudo_替代_su)
        *   [5.1.1 使用 sudo 编辑文件](#使用_sudo_编辑文件)
    *   [5.2 限制 root 登录](#限制_root_登录)
        *   [5.2.1 仅允许特定用户](#仅允许特定用户)
        *   [5.2.2 拒绝 SSH 登录](#拒绝_SSH_登录)
*   [6 强制访问控制](#强制访问控制)
    *   [6.1 基于路径的强制访问控制](#基于路径的强制访问控制)
    *   [6.2 基于标签的强制访问控制](#基于标签的强制访问控制)
    *   [6.3 访问控制表 (ACLs)](#访问控制表_(ACLs))
*   [7 内核加固](#内核加固)
    *   [7.1 内核自我保护 / 漏洞防护](#内核自我保护_/_漏洞防护)
        *   [7.1.1 用户空间 ASLR 比较](#用户空间_ASLR_比较)
            *   [7.1.1.1 64 位进程](#64_位进程)
            *   [7.1.1.2 32 位进程（运行在 x86_64 内核上）](#32_位进程（运行在_x86_64_内核上）)
    *   [7.2 限制访问内核日志](#限制访问内核日志)
    *   [7.3 限制访问 proc 文件系统中的内核指针](#限制访问_proc_文件系统中的内核指针)
    *   [7.4 禁用 BPF 即时编译](#禁用_BPF_即时编译)
    *   [7.5 ptrace 的可调用范围](#ptrace_的可调用范围)
        *   [7.5.1 示例：由于上述原因功能受限的程序](#示例：由于上述原因功能受限的程序)
    *   [7.6 隐藏进程](#隐藏进程)
*   [8 沙盒程序](#沙盒程序)
    *   [8.1 Firejail](#Firejail)
    *   [8.2 bubblewrap](#bubblewrap)
    *   [8.3 chroots](#chroots)
    *   [8.4 Linux containers](#Linux_containers)
    *   [8.5 其他虚拟化技术](#其他虚拟化技术)
*   [9 网络与防火墙](#网络与防火墙)
    *   [9.1 防火墙](#防火墙)
    *   [9.2 内核参数](#内核参数)
    *   [9.3 SSH](#SSH)
    *   [9.4 DNS](#DNS)
    *   [9.5 代理](#代理)
    *   [9.6 管理 SSL 证书](#管理_SSL_证书)
*   [10 软件包验证](#软件包验证)
*   [11 订阅漏洞告警](#订阅漏洞告警)
*   [12 物理安全](#物理安全)
    *   [12.1 锁定 BIOS](#锁定_BIOS)
    *   [12.2 引导加载程序 (Bootloader)](#引导加载程序_(Bootloader))
        *   [12.2.1 Syslinux](#Syslinux)
        *   [12.2.2 GRUB](#GRUB)
    *   [12.3 启动分区置于可移动闪存上](#启动分区置于可移动闪存上)
    *   [12.4 自动注销](#自动注销)
    *   [12.5 防范恶意 USB 设备](#防范恶意_USB_设备)
*   [13 重新构建软件包](#重新构建软件包)
*   [14 参考资料](#参考资料)

## 基本概念

*   有可能出现不停地加强系统安全性而导致系统无法正常使用的情况，因此不能过度加强安全。
*   提高安全性的方法有很多，但最致命的弱点永远在于人（用户）。考虑安全问题时，需要考虑多个层次。当一层防护被攻破时，另一层应该能够阻止攻击，但即使如此仍无法保证系统 100% 安全，除非把机器从网络上断开，锁进保险柜并不再使用它。
*   一点点的偏执和多疑有助于发现问题。如果某件事看起来太过完美，那可能问题就出在这。
*   [最小权限原则](https://en.wikipedia.org/wiki/Principle_of_least_privilege "wikipedia:Principle of least privilege")：系统的每一部分仅能访问到必要的内容，其他内容则不可见。

## 密码

密码是加强 Linux 系统的安全性的关键。它可以保护你的[用户账户](/index.php/Users_and_groups_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Users and groups (简体中文)")、[加密的文件系统](/index.php/Disk_encryption "Disk encryption")和[SSH](/index.php/SSH_keys "SSH keys")/[GPG](/index.php/GPG "GPG") 密钥。密码也是让计算机信任使用者的主要方式，所以大多数安全问题都出在如何选择高强度的密码并保护它们不被泄露上。

### 选择高强度的密码

当安全措施依赖于密码时，密码必须足够复杂，不能轻易地被猜中（比如和个人信息有关的密码），也不能轻易地被暴力尝试等方法 [破解](https://en.wikipedia.org/wiki/Password_cracking "wikipedia:Password cracking")，强密码的基本原则基于 *长度* 和 *随机性*，在密码学中，密码的质量与它的 [熵安全性](https://en.wikipedia.org/wiki/Entropic_security "wikipedia:Entropic security") 有关。

不安全的密码主要包括：

*   个人身份信息（如：狗的名字，出生日期，区号，最喜欢的视频游戏）
*   对一个单词简单地替换一些字符（如：`k1araj0hns0n`）
*   几个基本的常见字符，在它们的前后加上数字，符号或其他字符（如：`DG091101%`）
*   在语法上相关的常用短语（如：`all of the lights`），换掉了部分字符也不行。

好的密码首先要长（8~20 个字符，长度取决于重要程度），并且看起来完全随机。 有个方法可以产生安全性好的、看起来随机的密码，那就是从一句句子的每一个词中提炼出一个符号。 例如 “the girl is walking down the rainy street” 这句话可以转换为 `t6!WdtR5` 或是更加复杂的 `t&6!RrlW@dtR,57`。 这种方法可以更为简单地帮助记忆密码，但是请注意，不同字母出现在单词开头的概率不同 ([Wikipedia:Letter frequency](https://en.wikipedia.org/wiki/Letter_frequency#Relative_frequencies_of_the_first_letters_of_a_word_in_the_English_language "wikipedia:Letter frequency"))。同时也要考虑 [Diceware Passphrase](http://world.std.com/~reinhold/diceware.html) 中提到的方法，使用足够数量的单词。

更好的方法是使用 [pwgen](https://www.archlinux.org/packages/?name=pwgen) 或 [apg](https://aur.archlinux.org/packages/apg/) 等工具生成伪随机密码：为了记住它们，一种方法（仅针对经常输入的密码）是生成一个长密码并记住一小段（这一小段要能保证最低限度的安全），暂时把完整的密码写下来。随着时间推移，输入次数增加，密码会随着肌肉记忆根深蒂固。这种方法很难，但是能保证密码不会出现在破解用的字典里，也可以抵御能“智能地”组合单词并替换部分字符的暴力破解。

将生成与记忆密码两者结合的 [密码管理器](/index.php/Password_manager "Password manager") 也很有用，它可以保存长而复杂的随机密码，同时被一个方便记忆的密码保护着，该密码必须仅用于此密码管理器，特别注意要避免通过任何网络传输这个密码。当然这个方法限制了只能从存有密码库的电脑上使用已保存的密码（另一方面，这也可以视为额外的安全特性）。

可以看下 Bruce Schneier 的文章 [Choosing Secure Passwords](https://www.schneier.com/blog/archives/2014/03/choosing_secure_1.html)，[The passphrase FAQ](https://www.iusmentis.com/security/passphrasefaq/) 或 [Wikipedia:Password strength](https://en.wikipedia.org/wiki/Password_strength "wikipedia:Password strength") 获取额外背景信息。

### 维护密码安全

一旦你选择了一个强密码，一定要保证它的安全。当心 [键盘记录器](https://en.wikipedia.org/wiki/Keylogger "wikipedia:Keylogger")（软件或硬件层面上的），[社会工程](https://en.wikipedia.org/wiki/Social_engineering_(security) "wikipedia:Social engineering (security)")，[肩窥](https://en.wikipedia.org/wiki/Shoulder_surfing_(computer_security) "wikipedia:Shoulder surfing (computer security)")，并避免使用一样的密码，这样不安全的服务器就无法泄漏超出其范围的信息。[密码管理器](/index.php/List_of_applications/Security#Password_managers "List of applications/Security") 可以帮助管理大量复杂密码：将密码从管理器复制粘贴到其他程序中时，请确保每次粘贴完都清除复制缓冲区，并确保它们不会保存在日志记录里面（例如，不要将它们粘贴在普通的终端命令中，因为这些命令会存到 `.bash_history` 等文件里）。

最好不要因为安全性强的密码难记而选择不安全的密码，密码是它们之间的一种平衡。与拥有许多相似的弱密码相比，更好的做法是建立一个加密的安全密码数据库，数据库由密钥和一个强主密码保护着。把密码写下来可能同样有效[[1]](https://www.schneier.com/blog/archives/2005/06/write_down_your.html)，这样就避开了软件中的潜在漏洞，同时增加了物理安全性要求。

衡量密码强度的另一个指标是它能不能轻易从其他地方恢复。 如果你的登录密码和用于磁盘加密的密码相同（这在登录时自动挂载加密分区或目录很有用），请确保 `/etc/shadow` 也在加密分区上，或者使用强哈希算法（即 sha512/bcrypt，而不是 md5）来存储密码（详细信息请参阅 [SHA password hashes](/index.php/SHA_password_hashes "SHA password hashes")）。

如果要备份密码数据库，请勿将备份的副本存储在密码保护之下（比如存储在加密的驱动器或需要身份验证的远程存储服务），而解锁副本的密码又存储在副本中，这样在需要时将无法访问它。一个有用的技巧是，使用主密码的简单哈希来加密存储着密码数据库的驱动器或在线帐户。维护一份记录备份位置的列表：如果有一天担心主密码被泄露，一是要更改所有数据库备份的密码，二是要使用从新主密码派生的新哈希来保护存有数据库的位置。以安全的方式控制数据库的版本可能非常复杂：如果你这样做，那你必须有办法更新所有数据库版本的主密码。主密码泄露时可能并不能马上反映：为了降低其他人更早发现密码的风险，可以选择定期更改密码。如果你担心自己失去了对数据库副本的控制权，则需要在特定时间内更改其中包括的所有密码，这一特定时间是暴力破解主密码所用的时间，取决于主密码的熵。

### 密码的散列值

默认情况下，Arch 将用户密码散列值存储在仅 root 可读的 `/etc/shadow` 文件中，与存储在所有人可读的 `/etc/passwd` 文件中的其他用户参数分开，请参阅 [Users and groups (简体中文)#用户信息存储](/index.php/Users_and_groups_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)#用户信息存储 "Users and groups (简体中文)")。另请参阅 [#限制 root 权限](#限制_root_权限)。

密码应使用 **passwd** 命令来设置，该命令使用 [crypt](https://en.wikipedia.org/wiki/Crypt_(C) 函数对密码进行 [拉伸](https://en.wikipedia.org/wiki/Key_stretching "wikipedia:Key stretching")，然后将它们保存在 `/etc/shadow` 中。请参阅 [SHA password hashes](/index.php/SHA_password_hashes "SHA password hashes")。密码也被 [salted（加盐）](https://en.wikipedia.org/wiki/Salt_(cryptography) "wikipedia:Salt (cryptography)")，以抵御 [彩虹表](https://en.wikipedia.org/wiki/Rainbow_table "wikipedia:Rainbow table") 攻击。

另请参阅 [How are passwords stored in Linux (Understanding hashing with shadow utils)](http://www.slashroot.in/how-are-passwords-stored-linux-understanding-hashing-shadow-utils)。

### 用 pam_cracklib 强制使用强密码

*pam_cracklib* 提供针对 [字典攻击](https://en.wikipedia.org/wiki/Dictionary_attack "wikipedia:Dictionary attack") 的保护，并可用于配置在整个系统中实施的密码策略。

**警告:** *root* 账户不会受此策略影响。

**注意:** 可以用 *root* 帐户来帮助想绕过策略的用户设置他们的密码。这在设置临时密码时很有用。

举个例子，假设要强制执行下面的策略：

*   如果密码错误，请提示 2 次
*   最小长度为10个字符（minlen 选项）
*   输入新密码时，新密码应至少有 6 个字符与旧密码不同（difok 选项）
*   至少 1 个数字（dcredit 选项）
*   至少 1 个大写字母（ucredit 选项）
*   至少 1 个特殊字符（ocredit 选项）
*   至少 1 个小写字母（lcredit 选项）

编辑 `/etc/pam.d/passwd` 文件，把它改成：

```
#%PAM-1.0
password required pam_cracklib.so retry=2 minlen=10 difok=6 dcredit=-1 ucredit=-1 ocredit=-1 lcredit=-1
password required pam_unix.so use_authtok sha512 shadow
```

`password required pam_unix.so use_authtok` 用来告诉 *pam_unix* 模块不要显示输入密码的提示符，而是采用来自 *pam_cracklib* 的密码。

更多信息可以参考 [pam_cracklib(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/pam_cracklib.8) 和 [pam_unix(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/pam_unix.8) 手册页。

## 存储

### 磁盘加密

进行[磁盘加密](/index.php/Disk_encryption "Disk encryption")时最好使用[强密码](#密码)进行全盘加密，这是保护数据免受物理恢复的唯一方法。这也可以在计算机关闭或相关硬盘卸载时充分保护数据安全。

当然，一旦计算机启动，磁盘挂载完毕，这些数据就像存储在未加密的磁盘上一样易受攻击。因此，最佳做法是在不需要用到数据分区时立即卸载它们。

部分程序，比如 [dm-crypt](/index.php/Dm-crypt "Dm-crypt")，允许用户加密 Loop 文件并将其作为虚拟卷使用。当系统只有特定的部分需要加密时，这种方法可以替代全盘加密。

### 文件系统

如果用 sysctl 启用了内核的 `fs.protected_hardlinks` 和 `fs.protected_symlinks` 选项，内核就可以防止出现硬链接和软链接（符号链接）相关的安全问题。因此独立出一个全局可写的目录不再具有安全方面的优势。

文件系统中包含的全局可写的目录，仍然可以作为一种防止磁盘空间耗尽的粗略手段。但是，把 `/var` 或 `/tmp` 所在分区塞满也足以使系统停止响应。处理这种问题的更灵活的机制是存在的（比如 [磁盘配额](/index.php/Disk_quota "Disk quota")），并且某些 [文件系统](/index.php/File_systems_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "File systems (简体中文)") 自身就带有类似功能（Btrfs 的子卷可以设置配额）。

#### 挂载点

根据最小权限原则，挂载文件系统时应该采用最为严格的挂载选项（在不损失功能的情况下）。

相关的挂载选项有：

*   `nodev`: 文件系统中，禁止解释任何字符或屏蔽特殊设备。
*   `nosuid`: 禁止 set-user-identifier 或 set-group-identifier 标志位生效。
*   `noexec`: 禁止文件系统里的任何二进制文件直接运行。
    *   在 `/home` 上设置 `noexec` 选项会禁用可执行脚本，影响 [Wine](/index.php/Wine "Wine")* 和 [Steam](/index.php/Steam "Steam") 正常运行。
    *   部分软件包（比如编译 [nvidia-dkms](https://www.archlinux.org/packages/?name=nvidia-dkms)）可能需要 `/var` 有 `exec` 权限。

**注意:** Wine 运行 Windows 应用时不需要该应用带有 `exec` （可执行）标识，仅在 Wine 自身安装在 `/home` 时需要有可执行权限。

用于存放数据的文件系统应该坚持使用 `nodev`、`nosuid` 和 `noexec` 挂载。

文件系统划分参考：

*   `/var`
*   `/home`
*   `/dev/shm`
*   `/tmp`
*   `/boot`

### 文件访问权限

默认的 [文件权限](/index.php/File_permissions "File permissions") 对几乎所有文件都赋予了读权限，修改文件权限可以在取得了非 root 账户（`http` 或 `nobody` 账户）的攻击者前隐藏部分信息。

例如：

```
# chmod 700 /boot /etc/{iptables,arptables}

```

可以修改默认的 [Umask](/index.php/Umask "Umask") `0022` 来为新建的文件提高安全性。[NSA RHEL5 Security Guide](https://www.nsa.gov/ia/_files/os/redhat/rhel5-guide-i731.pdf) 建议将 umask 设置为 `0077` 以获得最充分的安全性，这将使得新文件无法被创建者之外的用户读取。要修改 umask，参见 [Umask#Set the mask value](/index.php/Umask#Set_the_mask_value "Umask")。

## 账户安全设置

安装后，请创建一个普通账户用于日常使用，不要日常使用 root 账户。

### 在失败的登录尝试后强制延时一段时间

将下方的行添加至 `/etc/pam.d/system-login` 即可在失败的登录尝试后延时至少 4 秒：

 `/etc/pam.d/system-login`  `auth optional pam_faildelay.so delay=4000000` 

`4000000` 是延时的微秒数。

### 在三次登录尝试失败后锁定用户

为了进一步提高安全性，可以在指定次数的登录尝试失败后锁定用户。普通账户可以被持续锁定直到 root 解锁它，也可以设置在指定的时间后自动解锁。

要在三次登录尝试失败后将用户锁定十分钟，需要将 `/etc/pam.d/system-login` 改为：

 `/etc/pam.d/system-login` 
```
#%PAM-1.0

auth required pam_tally2.so deny=3 unlock_time=600 onerr=succeed
account required pam_tally2.so
```

pam_tally 已被弃用并被 pam_tally2 取代，因此需要注释掉 pam_tally 行：

```
#auth required pam_tally.so onerr=succeed file=/var/log/faillog

```

全部工作就是这些。如果你有探索精神，请尝试三次登录失败，然后看看会发生什么。要手动解锁用户请执行：

```
# pam_tally2 --reset --user *username*

```

`unlock_time` 的单位为秒。如果你想在 3 次登录尝试失败后永久锁定用户，请删除该行的 `unlock_time` 部分。在 root 解锁该账户前，该账户将无法登录。

### 限制进程数量

在有很多不可信用户的系统上，限制每个用户可运行的进程数量非常重要，因为这样可以防止 [fork bombs](https://en.wikipedia.org/wiki/Fork_bomb "wikipedia:Fork bomb") 以及其他拒绝服务攻击。`/etc/security/limits.conf` 决定了每个用户或组可以运行的进程数，默认情况下为空（有用注释除外）。将以下行添加到此文件将限制所有用户每位最多运行 100 个活动进程，除非他们使用 `prlimit` 命令将此次会话的最大值显式地提高到 200。可以根据用户需要运行的进程数量或当前管理的系统的硬件条件来确定这些值。

```
* soft nproc 100
* hard nproc 200

```

当前每个用户运行的进程数量可以使用 `ps --no-headers -Leo user | sort | uniq -c` 查看。这可以帮助确定合适的进程限额。

### 避免用 root 运行 Xorg

由于其架构和过时的设计，[Xorg](/index.php/Xorg_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Xorg (简体中文)") 通常 [被认为是不安全的](https://security.stackexchange.com/questions/4641/why-are-people-saying-that-the-x-window-system-is-not-secure/4646#4646)。因此建议避免以 root 身份运行它。

有关如何在没有 root 权限的情况下运行 Xorg 的详细信息，请参阅 [Xorg#Rootless Xorg](/index.php/Xorg#Rootless_Xorg "Xorg")。

## 限制 root 权限

按照系统的设计，root 用户是系统中最强大的用户。因为这样，有许多方法可以既保持 root 用户的权限，同时限制其造成破坏的能力，或者至少可以追溯 root 用户的操作。

### 用 sudo 替代 su

出于 [多种原因](/index.php/Su_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)#另一个选择：Sudo "Su (简体中文)")，使用 [sudo](/index.php/Sudo_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Sudo (简体中文)") 进行特权访问比 [su](/index.php/Su_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Su (简体中文)") 更好。

*   sudo 记录了普通权限用户运行每个特权命令的日志。
*   root 用户的密码不需要告知每个请求 root 权限的用户。
*   `sudo` 可以防止用户意外地以 *root* 身份执行无需该权限的命令，因为 sudo 并没有为 root 创建完整的终端。这符合 [最小权限原则](https://en.wikipedia.org/wiki/Principle_of_least_privilege "wikipedia:Principle of least privilege")。

可以为单个用户启用单个程序的 root 权限，而不用为了运行一个程序启用该用户对 root 的完整访问权。例如，要授予用户 *alice* 对特定程序的访问权限：

```
# visudo

```
 `/etc/sudoers` 
```
alice ALL = NOPASSWD: /path/to/program

```

另外，也可以为所有用户开放单个程序。例如允许以普通用户身份从服务器挂载 Samba 共享：

```
%users ALL=/sbin/mount.cifs,/sbin/umount.cifs

```

这将允许 users 组中的所有用户从任何机器 (ALL) 运行此系统的 `/sbin/mount.cifs` 和 `/sbin/umount.cifs` 命令。

**提示：**

要 `visudo` 使用指定版本的 `nano` 而不是 `vi`，

 `/etc/sudoers`  `Defaults editor=/usr/bin/rnano` 

Export `# EDITOR=nano visudo` 被认为存在严重安全风险，因为任何程序都可以作为 `EDITOR`。

#### 使用 sudo 编辑文件

以 root 身份运行文本编辑器可能会变成安全漏洞，因为许多编辑器可以运行任意 shell 命令或更改正在编辑的文件以外的文件。要避免这一风险，请用 `sudoedit filename`（等同于 `sudo -e filename`）编辑文件。这将使用普通用户的权限来编辑文件的副本，在编辑器关闭后会使用 sudo 覆盖原始文件。可以通过设置 `SUDO_EDITOR` 环境变量来更改所使用的编辑器：

```
$ export SUDO_EDITOR=vim

```

也可以使用类似 `rvim` 这样的编辑器，它功能受限，以便以 root 用户身份安全运行。

### 限制 root 登录

正确配置 [sudo](/index.php/Sudo "Sudo") 后，完全的 root 权限就可以被严格限制或停用，且不会损失太多可用性。要禁用 root 而允许使用 [sudo](/index.php/Sudo "Sudo")，可以运行 `passwd -l root`。

#### 仅允许特定用户

[PAM](/index.php/PAM "PAM") 的 `pam_wheel.so` 模块可以做到仅允许 `wheel` 组中的用户使用 `su` 登录。编辑 `/etc/pam.d/su` 和 `/etc/pam.d/su-l` 两份文件，去掉以下行的注释：

```
# Uncomment the following line to require a user to be in the "wheel" group.
auth		required	pam_wheel.so use_uid

```

这一行表示只有已经能够运行特权命令的用户才能以 root 用户身份登录。

#### 拒绝 SSH 登录

即使你不想禁止 root 用户在本地登录，也最好 [禁止 root 通过 SSH 登录](/index.php/Secure_Shell_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)#禁用_root_登录 "Secure Shell (简体中文)")。这样做的目的是在用户可以在远程完全破坏系统之前添加额外的一层安全保护。

## 强制访问控制

[Mandatory access control](https://en.wikipedia.org/wiki/Mandatory_Access_Control "wikipedia:Mandatory Access Control")（MAC, 强制访问控制）是一种安全策略，它与 Arch 以及大部分 Linux 发行版默认使用的 [Discretionary access control](https://en.wikipedia.org/wiki/Discretionary_Access_Control "wikipedia:Discretionary Access Control") （DAC, 自主访问控制）有很大的不同。MAC 本质上是对照着一个安全规则集，检查程序的每一个可能对系统造成影响的操作。与 DAC 方式相比，用户不能修改 MAC 的规则集。使用几乎任何强制访问控制系统都将显著提高计算机的安全性，尽管它们的实现方式存在差异。

### 基于路径的强制访问控制

基于路径的访问控制是一种简单的访问控制形式，它根据文件的路径提供相应的权限。这种方式有个缺点，就是当文件改变路径以后相应的权限并没有随着文件一起移动。从积极的方面来说，基于路径的 MAC 可以在更广泛的文件系统上实现，这与基于标签的另一种可选方案是不同的。

[AppArmor](/index.php/AppArmor "AppArmor") 是一个由 [Canonical](https://en.wikipedia.org/wiki/Canonical "wikipedia:Canonical") 维护的 MAC 实现，它被看做是 SELinux 的简化版替代方案。

[Tomoyo](/index.php/Tomoyo "Tomoyo") 是另一种提供访问控制的系统，简单而易用。它的使用方式和内部实现都被设计得足够简单，需要的依赖也很少。

### 基于标签的强制访问控制

基于标签的访问控制意味着每份文件都带有扩展属性用于决定它的安全权限。虽然这类系统应该比基于路径的控制更灵活，但它只适用于支持这些扩展属性的文件系统。

[SELinux](/index.php/SELinux "SELinux") 是一个基于 [NSA](https://en.wikipedia.org/wiki/NSA "wikipedia:NSA") 的项目，用于提高 Linux 的安全性。它完整实现了 MAC，将系统用户与角色独立开来。它实现了一个非常强大的多级 MAC 策略，可以在系统扩大和改变得超出其原始配置时也能轻松控制系统。

### 访问控制表 (ACLs)

[Access Control Lists](/index.php/Access_Control_Lists "Access Control Lists")（ACLs，访问控制表）是以某种方式将规则直接附加到文件系统的一种可选方法。ACLs 将程序的实际操作与允许的操作对照，来实现访问控制。

## 内核加固

### 内核自我保护 / 漏洞防护

[linux-hardened](https://www.archlinux.org/packages/?name=linux-hardened) 相较于 [linux](https://www.archlinux.org/packages/?name=linux) 使用了 [基本内核加固补丁集](https://github.com/anthraxx/linux-hardened) 和更多安全相关的编译时配置选项。也可以使用自定义编译选项来把握安全性和性能之间的平衡，而不是使用强调安全性的默认选项。

如果你用了内核代码树以外的驱动，比如 [NVIDIA](/index.php/NVIDIA_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "NVIDIA (简体中文)")，可能会需要切换到它的 [DKMS](/index.php/Dynamic_Kernel_Module_Support_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Dynamic Kernel Module Support (简体中文)") 包。

#### 用户空间 ASLR 比较

[linux-hardened](https://www.archlinux.org/packages/?name=linux-hardened) 包为用户空间进程提供了改进的 ASLR（Address Space Layout Randomization，地址空间布局随机化）实现。[paxtest](https://www.archlinux.org/packages/?name=paxtest) 命令可用于获取所提供熵的估计值：

##### 64 位进程

 `linux-hardened` 
```
Anonymous mapping randomization test     : 32 quality bits (guessed)
Heap randomization test (ET_EXEC)        : 26 quality bits (guessed)
Heap randomization test (PIE)            : 40 quality bits (guessed)
Main executable randomization (ET_EXEC)  : No randomization
Main executable randomization (PIE)      : 32 quality bits (guessed)
Shared library randomization test        : 32 quality bits (guessed)
VDSO randomization test                  : 32 quality bits (guessed)
Stack randomization test (SEGMEXEC)      : 40 quality bits (guessed)
Stack randomization test (PAGEEXEC)      : 40 quality bits (guessed)
Arg/env randomization test (SEGMEXEC)    : 44 quality bits (guessed)
Arg/env randomization test (PAGEEXEC)    : 44 quality bits (guessed)
Offset to library randomisation (ET_EXEC): 32 quality bits (guessed)
Offset to library randomisation (ET_DYN) : 34 quality bits (guessed)
Randomization under memory exhaustion @~0: 32 bits (guessed)
Randomization under memory exhaustion @0 : 32 bits (guessed)

```
 `linux` 
```
Anonymous mapping randomization test     : 28 quality bits (guessed)
Heap randomization test (ET_EXEC)        : 13 quality bits (guessed)
Heap randomization test (PIE)            : 28 quality bits (guessed)
Main executable randomization (ET_EXEC)  : No randomization
Main executable randomization (PIE)      : 28 quality bits (guessed)
Shared library randomization test        : 28 quality bits (guessed)
VDSO randomization test                  : 20 quality bits (guessed)
Stack randomization test (SEGMEXEC)      : 30 quality bits (guessed)
Stack randomization test (PAGEEXEC)      : 30 quality bits (guessed)
Arg/env randomization test (SEGMEXEC)    : 22 quality bits (guessed)
Arg/env randomization test (PAGEEXEC)    : 22 quality bits (guessed)
Offset to library randomisation (ET_EXEC): 28 quality bits (guessed)
Offset to library randomisation (ET_DYN) : 28 quality bits (guessed)
Randomization under memory exhaustion @~0: 28 bits (guessed)
Randomization under memory exhaustion @0 : 28 bits (guessed)

```

##### 32 位进程（运行在 x86_64 内核上）

 `linux-hardened` 
```
Anonymous mapping randomization test     : 16 quality bits (guessed)
Heap randomization test (ET_EXEC)        : 22 quality bits (guessed)
Heap randomization test (PIE)            : 27 quality bits (guessed)
Main executable randomization (ET_EXEC)  : No randomization
Main executable randomization (PIE)      : 18 quality bits (guessed)
Shared library randomization test        : 16 quality bits (guessed)
VDSO randomization test                  : 16 quality bits (guessed)
Stack randomization test (SEGMEXEC)      : 24 quality bits (guessed)
Stack randomization test (PAGEEXEC)      : 24 quality bits (guessed)
Arg/env randomization test (SEGMEXEC)    : 28 quality bits (guessed)
Arg/env randomization test (PAGEEXEC)    : 28 quality bits (guessed)
Offset to library randomisation (ET_EXEC): 18 quality bits (guessed)
Offset to library randomisation (ET_DYN) : 16 quality bits (guessed)
Randomization under memory exhaustion @~0: 18 bits (guessed)
Randomization under memory exhaustion @0 : 18 bits (guessed)

```
 `linux` 
```
Anonymous mapping randomization test     : 8 quality bits (guessed)
Heap randomization test (ET_EXEC)        : 13 quality bits (guessed)
Heap randomization test (PIE)            : 13 quality bits (guessed)
Main executable randomization (ET_EXEC)  : No randomization
Main executable randomization (PIE)      : 8 quality bits (guessed)
Shared library randomization test        : 8 quality bits (guessed)
VDSO randomization test                  : 8 quality bits (guessed)
Stack randomization test (SEGMEXEC)      : 19 quality bits (guessed)
Stack randomization test (PAGEEXEC)      : 19 quality bits (guessed)
Arg/env randomization test (SEGMEXEC)    : 11 quality bits (guessed)
Arg/env randomization test (PAGEEXEC)    : 11 quality bits (guessed)
Offset to library randomisation (ET_EXEC): 8 quality bits (guessed)
Offset to library randomisation (ET_DYN) : 13 quality bits (guessed)
Randomization under memory exhaustion @~0: No randomization
Randomization under memory exhaustion @0 : No randomization

```

### 限制访问内核日志

**注意:** 这个功能在 [linux-hardened](https://www.archlinux.org/packages/?name=linux-hardened) 中是默认打开的。

内核日志包含了那些试图利用内核漏洞（如敏感内存地址）的攻击者的有用信息。`kernel.dmesg_restrict` 标记可以禁止不带 `CAP_SYS_ADMIN` 能力的进程访问内核日志（默认只有 root 运行的进程带有该能力）。

 `/etc/sysctl.d/50-dmesg-restrict.conf`  `kernel.dmesg_restrict = 1` 

### 限制访问 proc 文件系统中的内核指针

**注意:** [linux-hardened](https://www.archlinux.org/packages/?name=linux-hardened) 默认设置是 `kptr_restrict=2` 而不是 `0`。

将 `kernel.kptr_restrict` 设置为 1 将针对没有 `CAP_SYSLOG` 的普通用户隐藏 `/proc/kallsyms` 中的内核符号地址，这使得利用内核漏洞动态解析地址/符号变得更加困难。这对预编译好的 Arch Linux 内核没有多大帮助，因为攻击者可以直接下载到内核包并从那里手动获取符号，但如果你正在编译自己的内核，这可以帮助减轻本地根攻击。这样做以后会影响非 root 用户运行部分 [perf](https://www.archlinux.org/packages/?name=perf) 命令（虽然很多 [perf](https://www.archlinux.org/packages/?name=perf) 功能本身就需要 root 权限）。更多信息请参见 [FS#34323](https://bugs.archlinux.org/task/34323)。

将 `kernel.kptr_restrict` 设置为 2 将隐藏 `/proc/kallsyms` 中的内核符号地址，而忽略用户的权限。

 `/etc/sysctl.d/50-kptr-restrict.conf`  `kernel.kptr_restrict = 1` 

### 禁用 BPF 即时编译

Linux 内核有一个功能，就是将 BPF/Seccomp 规则集编译为原生代码来优化性能。`net.core.bpf_jit_enable` 标志位应设置为 `0` 以获得最大安全性。

BPF/Seccomp 编译在特定领域中很有用，比如各类动态服务（类似 Mesos 和 Kubernetes 这样的集群管理平台），它通常不适用于桌面用户或静态服务。JIT 编译器为攻击者提供了进行堆喷射攻击 (Heap spraying attack) 的可能性。在这种攻击中，他们用恶意代码填充内核堆，然后利用另一个漏洞执行此代码，比如解除引用一个不正确的函数指针。2018 年早先公布的 [幽灵](https://en.wikipedia.org/wiki/Spectre_(security_vulnerability) 漏洞，是其最为突出的一次利用过程。

### ptrace 的可调用范围

Arch 默认启用了 Yama LSM，提供了 `kernel.yama.ptrace_scope` 标志位作为开关。默认情况下这个开关是打开的，它可以使得没有 `CAP_SYS_PTRACE` 能力的进程无法对其作用域之外的其他进程执行 `ptrace` 调用。虽然许多调试工具需要 `ptrace` 来实现某些功能，但这一修改显著提高了安全性。如果没有此功能，且不使用命名空间等额外隔离层的情况下，同一用户运行的进程之间基本没有隔离。调试器可以附加到现有进程的能力证明了这个弱点确实存在。

#### 示例：由于上述原因功能受限的程序

**注意:** 你仍然可以以 root 身份执行这些命令（例如允许某些用户使用 [sudo](/index.php/Sudo "Sudo")，且无论是否需要密码）。

*   `gdb -p $PID`
*   `strace -p $PID`
*   `perf trace -p $PID`
*   `reptyr $PID`

### 隐藏进程

**警告:**

*   这可能会导致某些应用程序出现问题，例如在沙盒和 [Xorg](/index.php/Xorg "Xorg") 中运行的应用程序（请参阅解决方法）。
*   当所使用的 [systemd](https://www.archlinux.org/packages/?name=systemd) 版本大于 237.64-1 时，这可能会导致 [D-Bus](/index.php/D-Bus "D-Bus")、[PulseAudio](/index.php/PulseAudio "PulseAudio") 和 [bluetooth](/index.php/Bluetooth "Bluetooth") 出现问题。

其他用户的进程通常可以在 `/proc` 访问到，而内核有能力向非特权用户隐藏这些进程，按照 [此处](https://git.kernel.org/pub/scm/linux/kernel/git/torvalds/linux.git/tree/Documentation/filesystems/proc.txt#n1919) 记录的方法以 `hidepid=` 和 `gid=` 选项挂载 `proc` 文件系统即可。

这使得入侵者收集正在运行的进程信息变得异常艰难，同样艰难的还包括判断是否存在特权运行的守护进程、其他用户是否正在运行敏感程序，甚至无法捕捉到其他用户运行的任何程序，更无法捕捉到特定的程序是否正在运行（假设该程序不会因为其自身行为暴露自己），并且作为额外的优势，那些通过外部参数传递敏感信息的、写得不那么好的程序现在可以防范本地窃听了。

由 [filesystem](https://www.archlinux.org/packages/?name=filesystem) 软件包提供的 `proc` [用户组](/index.php/Users_and_groups#System_groups "Users and groups") 相当于一个白名单，包含了有权访问其他用户进程信息的用户。如果用户或服务需要访问除自身以外的 `/proc/<pid>` 目录，请 [将他们加入该用户组](/index.php/Users_and_groups#Group_management "Users and groups")。

例如，把除了 `proc` 组中用户之外的其他用户的进程信息都隐藏起来：

 `/etc/fstab`  `proc	/proc	proc	nosuid,nodev,noexec,hidepid=2,gid=proc	0	0` 

要使用户会话正常工作，需要为 *systemd-logind* 添加例外：

 `/etc/systemd/system/systemd-logind.service.d/hidepid.conf` 
```
[Service]
SupplementaryGroups=proc
```

## 沙盒程序

另请参阅 [Wikipedia:Sandbox (computer security)](https://en.wikipedia.org/wiki/Sandbox_(computer_security) "wikipedia:Sandbox (computer security)")。

**注意:** 用户命名空间配置项 `CONFIG_USER_NS` 当前在 [linux](https://www.archlinux.org/packages/?name=linux)（v4.14.5或更高版本）、[linux-lts](https://www.archlinux.org/packages/?name=linux-lts)（v4.14.15或更高版本）和 [linux-hardened](https://www.archlinux.org/packages/?name=linux-hardened) 中启用。关闭它可能会导致程序无法开启某些沙盒功能。由于会增加本地提权的可能性，非特权用法默认是禁用的，启用它需要将 `kernel.unprivileged_userns_clone` [sysctl](/index.php/Sysctl "Sysctl") 设置为 `1`。

### Firejail

[Firejail](/index.php/Firejail "Firejail") 是一个易于使用的、简单的工具，用于沙盒化程序和服务器。建议将 Firejail 也用于浏览器以及其他网络应用程序，就像对待正在运行的服务器程序一样。

### bubblewrap

[bubblewrap](/index.php/Bubblewrap "Bubblewrap") 是一个由 [Flatpak](https://en.wikipedia.org/wiki/Flatpak "wikipedia:Flatpak") 开发的基于 setuid 的沙盒程序，其资源占用比 Firejail 更小。虽然它缺少某些功能，例如文件路径白名单，但 bubblewrap 确实提供了 bind mounts 的功能，能够创建 user/IPC/PID/network/cgroup 命名空间，并且可以支持简单和 [复杂的沙盒](https://github.com/projectatomic/bubblewrap/blob/master/demos/bubblewrap-shell.sh)。

### chroots

手动构造 [chroot](/index.php/Chroot_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Chroot (简体中文)") jail 也是可以的。

### Linux containers

在不使用 KVM 和 VirtualBox 又需要更大程度隔离的情况下，[Linux Containers](/index.php/Linux_Containers "Linux Containers")（Linux 软件容器）是一个不错的选择。LXC 使用自己的虚拟硬件，在现有内核之上的 pseudo-chroot 内运行。

### 其他虚拟化技术

使用类似 [VirtualBox](/index.php/VirtualBox_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "VirtualBox (简体中文)")、[KVM](/index.php/KVM_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "KVM (简体中文)")、[Xen](/index.php/Xen_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Xen (简体中文)") 或 [Qubes OS](https://www.qubes-os.org/)（基于 Xen）的完全虚拟化技术，可以在运行有风险的应用程序或浏览危险网站时提高隔离性和安全性。

## 网络与防火墙

### 防火墙

虽然源里面的 Arch 内核能够启用 [Netfilter](https://en.wikipedia.org/wiki/Netfilter "wikipedia:Netfilter") 的 [iptables](/index.php/Iptables "Iptables") 和 [nftables](/index.php/Nftables "Nftables")，但它们默认是关闭的。因此强烈建议配置防火墙来保护系统上运行的服务。许多资料（包括 ArchWiki）没有明确说明哪些服务值得保护，因此启用防火墙是一个很好的预防措施。

*   参阅 [iptables](/index.php/Iptables_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Iptables (简体中文)") 和 [nftables](/index.php/Nftables "Nftables") 来获取一般信息。
*   参阅 [Simple stateful firewall](/index.php/Simple_stateful_firewall_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Simple stateful firewall (简体中文)") 来获取配置 iptables 防火墙的指南。
*   参阅 [Category:Firewalls](/index.php/Category:Firewalls "Category:Firewalls") 来获取设置 netfilter 的其他方法。
*   参阅 [Ipset](/index.php/Ipset_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Ipset (简体中文)") 以设置 IP 地址黑名单，内容可参考来自 Bluetack 的名单。

### 内核参数

作用于网络的内核参数可以使用 [Sysctl](/index.php/Sysctl "Sysctl") 来设置。要查询具体方法，请参阅 [Sysctl#TCP/IP stack hardening](/index.php/Sysctl#TCP/IP_stack_hardening "Sysctl")。

### SSH

为了减轻 [暴力攻击](https://en.wikipedia.org/wiki/Brute-force_attack "wikipedia:Brute-force attack")，建议强制使用基于密钥的身份验证。对于 OpenSSH，请参阅 [OpenSSH#Force public key authentication](/index.php/OpenSSH#Force_public_key_authentication "OpenSSH")。另外，[Fail2ban](/index.php/Fail2ban "Fail2ban") 或 [Sshguard](/index.php/Sshguard "Sshguard") 通过监控日志并写入 [iptables 规则](/index.php/Iptables "Iptables") 提供了较少形式的保护，但这样做可能会使服务器拒绝服务，因为攻击者可以伪装成管理员的地址并发送欺骗性的数据包。

你可以用双因素身份验证来进一步强化身份验证。[Google Authenticator](/index.php/Google_Authenticator "Google Authenticator")（Google 身份验证器）使用一次性密码 (OTP) 提供两步验证过程。

拒绝 root 登录也是一种很好的做法，既可以跟踪入侵，也可以在 root 访问之前添加额外的安全层。对于 OpenSSH，请参阅 [OpenSSH#Deny](/index.php/OpenSSH#Deny "OpenSSH")。

### DNS

默认情况下，多数系统上的 [DNS](/index.php/DNS "DNS") 查询请求的发送和接收是不加密的，并且不验证数据是否来自规范的服务器，这可能导致 [中间人攻击](https://en.wikipedia.org/wiki/Man-in-the-middle_attack "wikipedia:Man-in-the-middle attack")，攻击者拦截用户的 DNS 查询并修改响应数据为 [钓鱼](https://en.wikipedia.org/wiki/Phishing "wikipedia:Phishing") 网站的 IP 地址，导致钓鱼网站收集用户的宝贵信息。用户和浏览器/其他软件都不会知道发生了什么，因为 DNS 协议始终将查询结果视为合法的。

[DNSSEC](/index.php/DNSSEC "DNSSEC") 是一套标准，要求 DNS 服务器向客户端出示 DNS 数据的原始验证证明、曾经的验证失败记录和数据完整性。然而这一标准尚未广泛使用。启用 DNSSEC 后，攻击者无法修改您的 DNS 查询请求和返回的结果，但仍可以读取它们。

[DNSCrypt](/index.php/DNSCrypt_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "DNSCrypt (简体中文)") 以及后来的替代协议 *DNS over TLS* 和 *DNS over HTTPS*，使用加密技术来保护与 DNS 服务器的通信，系统层面上通常只采用其中一种协议。有关实现这些协议的软件，请参阅 [Domain name resolution#DNS servers](/index.php/Domain_name_resolution#DNS_servers "Domain name resolution")。

如果你有一个域名，请设置 [Sender Policy Framework](/index.php/Sender_Policy_Framework "Sender Policy Framework")（发件人策略框架）来抵御电子邮件欺骗。

### 代理

代理通常用作应用程序和网络之间的附加层，拦截不受信任的来源的数据。从攻击面上看，以较低权限运行的小代理的攻击面明显小于使用最终用户权限运行的复杂应用程序。

例如，DNS 解析器是在 [glibc](https://www.archlinux.org/packages/?name=glibc) 中实现的，它与应用程序链接（可能以root身份运行），因此 DNS 解析器中的 bug 可能导致本机执行远程代码。而这可以安装充当代理的 DNS 缓存服务器（例如 [dnsmasq](/index.php/Dnsmasq "Dnsmasq")）来避免。[[2]](https://googleonlinesecurity.blogspot.it/2016/02/cve-2015-7547-glibc-getaddrinfo-stack.html)

### 管理 SSL 证书

请参阅 [OpenSSL](/index.php/OpenSSL_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "OpenSSL (简体中文)") 和 [Network Security Services](/index.php/Network_Security_Services "Network Security Services")（NSS，网络安全服务）来管理各自的服务器端 SSL 证书。值得注意的是，与此相关的 [Let’s Encrypt](/index.php/Let%E2%80%99s_Encrypt "Let’s Encrypt") 项目也支持这些协议。

默认的 Internet SSL 证书信任链由 [ca-certificates](https://www.archlinux.org/packages/?name=ca-certificates) 包及其依赖项提供。请注意，Arch 依赖于信任源（例如 [ca-certificates-mozilla](https://www.archlinux.org/packages/?name=ca-certificates-mozilla)）来提供受系统信任的证书。

有时你可能需要暂时更改默认设置。例如，当你读到这一 [新闻](https://www.theregister.co.uk/2016/05/27/blue_coat_ca_certs/) 并希望手动解除证书信任，而不是等到信任源提供商这样做，在 Arch 的体系里非常简单：

1.  以 .crt 格式获取相应的证书（示例：[查看](https://crt.sh/?id=19538258), [下载](https://crt.sh/?d=19538258)；如果是现有的受信任的根证书颁发机构，你也可以在系统路径中找到它）
2.  将其复制到 `/etc/ca-certificates/trust-source/blacklist/`
3.  以 root 身份运行 *update-ca-trust*。

要检查黑名单是否按预期那样工作，请重新打开浏览器并通过其 GUI 执行此操作，现在浏览器应显示其为不受信任。

## 软件包验证

如果没有正确地对包进行签名，包管理器就有可能 [受到攻击](https://www.cs.arizona.edu/stork/packagemanagersecurity/attacks-on-package-managers.html#overview)，甚至可能会影响原本具有 [签名机制](https://www.cs.arizona.edu/stork/packagemanagersecurity/faq.html) 的包管理器。Arch 默认采用软件包签名机制，并依赖来自 5 个可信主密钥的信任网络。详情请参阅 [pacman/Package signing (简体中文)](/index.php/Pacman/Package_signing_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Pacman/Package signing (简体中文)")。

## 订阅漏洞告警

订阅国家漏洞数据库 (National Vulnerability Database) 提供的常见漏洞和披露 (Common Vulnerabilities and Exposure, CVE) 安全警报更新，相关内容可以在 [NVD 下载页](https://nvd.nist.gov/download.cfm) 上找到。[Arch Linux Security Tracker](https://security.archlinux.org/) 是一个特别有用的资源，它结合了 Arch Linux 安全通报 (ASA)，Arch Linux 漏洞组 (AVG) 以及 CVE 数据集，且以表格形式呈现。另请参阅 [Arch Security Team](/index.php/Arch_Security_Team "Arch Security Team")（Arch 安全团队）。

**警告:** 不要试图进行 [部分升级](/index.php/System_maintenance_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)#不支持部分升级 "System maintenance (简体中文)")，因为 Arch Linux 不支持部分升级且可能导致系统不稳定，要升级组件时应升级整个系统。另外，系统更新不及时可能会使以后的更新过程更加复杂。

## 物理安全

理论上如果有足够的时间和计算资源，对计算机的物理访问都将会变成 root 权限的访问。但通过设置足够的障碍可以获得切实的安全保障。

攻击者只需连接恶意的 IEEE 1394（火线接口），Thunderbolt 或 PCI Express 设备即可在下次启动时完全控制计算机，因为它们可以完全访问内存。[[3]](https://www.breaknenter.org/projects/inception/) 你无法阻止类似这样的操作，包括修改硬件本身的操作（比如将恶意固件刷到设备上）。但是，绝大多数攻击者都没有这样的知识和信心。

[#磁盘加密](#磁盘加密) 将在计算机被盗时保护数据，但经验丰富的攻击者可以给计算机安装恶意固件，在用户下次登录时获取加密的数据。

### 锁定 BIOS

向 BIOS 添加密码可防止其他人启动到可移动设备，否则这和其他人对计算机具有 root 访问权限基本相同。你应该确保你的磁盘在引导顺序中处于第一位，并且可以的话禁用其他引导设备。

### 引导加载程序 (Bootloader)

保护引导加载程序非常重要。因为有一个神奇的内核参数叫做 `init=/bin/sh`，它会使得任何用户的登录限制完全无用。

#### Syslinux

Syslinux 支持 [用密码保护引导加载程序](/index.php/Syslinux#Security "Syslinux")。它允许为每个菜单项设置密码或为整个引导程序设置密码。

#### GRUB

[GRUB](/index.php/GRUB_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "GRUB (简体中文)") 也可以设置引导密码。详情请参阅 [GRUB/Tips and tricks#Password protection of GRUB menu](/index.php/GRUB/Tips_and_tricks#Password_protection_of_GRUB_menu "GRUB/Tips and tricks")。它还支持 [加密的 /boot](/index.php/GRUB#Encrypted_/boot "GRUB")，这样只会使引导程序的部分代码保持未加密状态。GRUB 的配置、[内核](/index.php/Kernels_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Kernels (简体中文)") 和 [initramfs](/index.php/Arch_boot_process_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)#initramfs "Arch boot process (简体中文)") 都是加密的。

### 启动分区置于可移动闪存上

一个较为流行的做法是将启动分区放在可移动闪存上，在没有它的情况下系统便无法启动。这个想法的支持者经常使用 [全盘加密](#磁盘加密)，有些还用到了放在启动分区上的 [分离加密头](/index.php/Dm-crypt/Specialties#Encrypted_system_using_a_detached_LUKS_header "Dm-crypt/Specialties")。

### 自动注销

如果你用的是 [Bash](/index.php/Bash_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Bash (简体中文)") 或 [Zsh](/index.php/Zsh_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Zsh (简体中文)")，则可以设置 `TMOUT` 的值，使 shell 在超时后自动注销。

例如，下面的脚本内容将使用户自动从虚拟控制台（非 X11 中的终端模拟器）注销：

 `/etc/profile.d/shell-timeout.sh` 
```
TMOUT="$(( 60*10 ))";
[ -z "$DISPLAY" ] && export TMOUT;
case $( /usr/bin/tty ) in
	/dev/tty[0-9]*) export TMOUT;;
esac

```

如果确实想要所有 Bash/Zsh 提示符（包括 X 中的）都有超时，请使用：

```
$ export TMOUT="$(( 60*10 ))";

```

请注意，shell 中运行的某些命令（例如：SSH 会话或没有 `TMOUT` 支持的其他 shell）将使上述设置失效。但是如果你主要使用 VC 以 root 身份重新启动僵死的 GDM/Xorg，那么这非常有用。

### 防范恶意 USB 设备

请安装 [USBGuard](/index.php/USBGuard "USBGuard")，这是一个软件框架，通过基于设备属性的基本白名单和黑名单功能，帮助保护计算机免受恶意 USB 设备（例如 [BadUSB](https://srlabs.de/badusb)、[PoisonTap](https://github.com/samyk/poisontap) 或 [LanTurtle](https://lanturtle.com/)）的侵害。

## 重新构建软件包

软件包可以去除不需要的功能并重新构建，这样可以缩小受攻击范围。例如，[bzip2](https://www.archlinux.org/packages/?name=bzip2) 可以在没有 `bzip2recover` 的情况下重新构建，以试图规避 [CVE-2016-3189](https://security.archlinux.org/CVE-2016-3189) 漏洞。强化安全的自定义编译参数也可以手动或通过包装器在编译时加入。

## 参考资料

*   [Arch Linux Security Tracker](https://security.archlinux.org/)
*   [CentOS Wiki: OS Protection](https://wiki.centos.org/HowTos/OS_Protection)
*   [Hardening the Linux desktop](https://www.ibm.com/developerworks/linux/tutorials/l-harden-desktop/index.html)
*   [Hardening the Linux server](https://www.ibm.com/developerworks/linux/tutorials/l-harden-server/index.html)
*   [Linux Foundation: Linux workstation security checklist](https://github.com/lfit/itpol/blob/master/linux-workstation-security.md)
*   [privacytools.io Privacy Resources](https://www.privacytools.io/)
*   [Red Hat Enterprise Linux 7 Security Guide](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/7/html/Security_Guide/)
*   [Securing Debian Manual (PDF)](https://www.debian.org/doc/manuals/securing-debian-howto/securing-debian-howto.en.pdf)
*   [The paranoid #! Security Guide](https://web.archive.org/web/20140220055801/http://crunchbang.org:80/forums/viewtopic.php?id=24722)