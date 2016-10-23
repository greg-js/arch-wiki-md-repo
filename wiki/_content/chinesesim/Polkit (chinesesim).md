**翻译状态：** 本文是英文页面 [Polkit](/index.php/Polkit "Polkit") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2016-04-11，点击[这里](https://wiki.archlinux.org/index.php?title=Polkit&diff=0&oldid=430809)可以查看翻译后英文页面的改动。

来自 [polkit 主页](http://www.freedesktop.org/wiki/Software/polkit/)：

	*polkit 是一个应用程序级别的工具集，通过定义和审核权限规则，实现不同优先级进程间的通讯：控制决策集中在统一的框架之中，决定低优先级进程是否有权访问高优先级进程。*

Polkit 在系统层级进行权限控制，提供了一个低优先级进程和高优先级进程进行通讯的系统。和 sudo 等程序不同，Polkit 并没有赋予进程完全的 root 权限，而是通过一个集中的策略系统进行更精细的授权。

Polkit 定义出一系列操作，例如运行 GParted, 并将用户按照群组或用户名进行划分，例如 wheel 群组用户。然后定义每个操作是否可以由某些用户执行，执行操作前是否需要一些额外的确认，例如通过输入密码确认用户是不是属于某个群组。

## Contents

*   [1 安装](#.E5.AE.89.E8.A3.85)
    *   [1.1 身份认证组件](#.E8.BA.AB.E4.BB.BD.E8.AE.A4.E8.AF.81.E7.BB.84.E4.BB.B6)
*   [2 配置](#.E9.85.8D.E7.BD.AE)
    *   [2.1 操作](#.E6.93.8D.E4.BD.9C)
    *   [2.2 认证规则](#.E8.AE.A4.E8.AF.81.E8.A7.84.E5.88.99)
    *   [2.3 管理员身份认证](#.E7.AE.A1.E7.90.86.E5.91.98.E8.BA.AB.E4.BB.BD.E8.AE.A4.E8.AF.81)
*   [3 范例](#.E8.8C.83.E4.BE.8B)
    *   [3.1 禁用挂起和休眠](#.E7.A6.81.E7.94.A8.E6.8C.82.E8.B5.B7.E5.92.8C.E4.BC.91.E7.9C.A0)
    *   [3.2 跳过口令提示](#.E8.B7.B3.E8.BF.87.E5.8F.A3.E4.BB.A4.E6.8F.90.E7.A4.BA)
        *   [3.2.1 全局规则](#.E5.85.A8.E5.B1.80.E8.A7.84.E5.88.99)
        *   [3.2.2 针对特定的动作设置](#.E9.92.88.E5.AF.B9.E7.89.B9.E5.AE.9A.E7.9A.84.E5.8A.A8.E4.BD.9C.E8.AE.BE.E7.BD.AE)
        *   [3.2.3 Udisks](#Udisks)
    *   [3.3 允许一般用户管理某个 systemd 单元](#.E5.85.81.E8.AE.B8.E4.B8.80.E8.88.AC.E7.94.A8.E6.88.B7.E7.AE.A1.E7.90.86.E6.9F.90.E4.B8.AA_systemd_.E5.8D.95.E5.85.83)
*   [4 参阅](#.E5.8F.82.E9.98.85)

## 安装

安装 [polkit](https://www.archlinux.org/packages/?name=polkit) 包。

### 身份认证组件

Polkit 的权限管理是基于用户或群组进行配置，而身份认证组件的作用就是让会话用户证明自己是某个用户或属于某个群组。

图形化环境[Cinnamon](/index.php/Cinnamon "Cinnamon")、[Deepin](/index.php/Deepin_Desktop_Environment "Deepin Desktop Environment")、[GNOME](/index.php/GNOME "GNOME")、[GNOME Flashback](/index.php/GNOME_Flashback "GNOME Flashback")、[KDE](/index.php/KDE "KDE")、[LXDE](/index.php/LXDE "LXDE")、[LXQt](/index.php/LXQt "LXQt")、[MATE](/index.php/MATE "MATE") 和 [Xfce](/index.php/Xfce "Xfce") 各自都已有认证组件。请按照下列清单确认安装了对应的身份认证组件，并且在登录时 [自动启动](/index.php/Autostarting "Autostarting") 它。

其他桌面环境需要从下列实现中选用一种，[polkit](https://www.archlinux.org/packages/?name=polkit) 软件包提供了一个名为“pkttyagent”的基于文本方式的认证代理，作为后备方案。

*   [lxqt-policykit](https://www.archlinux.org/packages/?name=lxqt-policykit)，提供了 `/usr/bin/lxqt-policykit-agent`
*   [lxsession](https://www.archlinux.org/packages/?name=lxsession)，提供了 `/usr/bin/lxpolkit`
*   [mate-polkit](https://www.archlinux.org/packages/?name=mate-polkit)，提供了 `/usr/lib/mate-polkit/polkit-mate-authentication-agent-1`
*   [polkit-efl-git](https://aur.archlinux.org/packages/polkit-efl-git/)，提供了 `/usr/bin/polkit-efl-authentication-agent-1`
*   [polkit-gnome](https://www.archlinux.org/packages/?name=polkit-gnome)，提供了 `/usr/lib/polkit-gnome/polkit-gnome-authentication-agent-1`
*   [polkit-kde-agent](https://www.archlinux.org/packages/?name=polkit-kde-agent)，提供了 `/usr/lib/polkit-kde/polkit-kde-authentication-agent-1`
*   [xfce-polkit-git](https://aur.archlinux.org/packages/xfce-polkit-git/)，提供了 `/usr/lib/xfce-polkit/xfce-polkit`

## 配置

**警告:** 不要更改包文件的默认权限，因其可能在软件包更新时被覆盖。

Polkit 定义了两种不同的内容：

*   **操作（Actions）**：在 `/usr/share/polkit-1/actions` 中定义，文件是 XML 格式，以 `.policy` 结尾。每个**操作**都有一个默认的权限集合（例如，你需要标识为管理员以使用 GParted 操作）。默认值是可以修改的，但是不应该通过修改操作文件实现。
*   **认证规则（Authorization rules）**：用 JavaScript 语法定义，文件以 `.rules` 结尾。有两个目录可放置规则文件：第三方的包将文件放置在 `/usr/share/polkit-1/rules.d`（尽管很少见），本地配置应该放置在 `/etc/polkit-1/rules.d`。

Polkit 没有取代系统已有的权限系统，而是在已有的群组和管理员上进行管控。**.rules** 文件指定了一个用户的子集合，涉及到一个或多个**操作**文件中指定的操作，并规定这些用户可以执行哪些操作，需要满足哪些限制。举例来说，GParted 默认规则要求所有用户认证为管理员之后才能使用，可以用规则文件修改默认规则，规定某个用户不需要管理员身份认证就可以执行操作，也可以完全禁止某个用户使用 GParted。

**注意:** 如果用户不是通过 polkit 申请权限，比如通过命令行直接以 root 权限执行，这里的禁止设定就无法起作用。所以应该用 polkit 给低权限用户更高的权限，而不应该用 polkit 限制高权限用户可以执行的操作。

### 操作

**提示:** 要在图形程序中显示 Polikit 操作，可以安装软件包 [polkit-explorer](https://aur.archlinux.org/packages/polkit-explorer/) 。

polkit 中的可用操作是安装的软件包决定的。有些在多种桌面环境下都可以使用，文件命名为 *（org.freedesktop.*）*，有些只能在特定桌面下使用，文件命名类似 *(org.gnome.*)*，有些操作是单个程序特有的，命名类类似 *(org.archlinux.pkexec.gparted.policy)*。`pkaction` 命令会显示所有定义在 `/usr/share/polkit-1/actions` 操作。

通过下面几个常用的操作类型，可以了解 polkit 到底能做什么：

*   **[systemd-logind](/index.php/Systemd "Systemd")** *(org.freedesktop.login1.policy)* 定义用户是否有权限进行关机、重启、挂起、休眠等操作，即使有其它用户登录时， polkit 也能管控某个用户的上述权限。
*   **[udisks](/index.php/Udisks "Udisks")** *(org.freedesktop.udisks2.policy)* 定义文件系统挂载、加密磁盘打开等操作。
*   **[NetworkManager](/index.php/NetworkManager "NetworkManager")** *(org.freedesktop.NetworkManager.policy)* 定义网络打开和关闭， wifi 和移动网络间的切换。

每个操作都定义在 .policy 文件的 `<action>` 标签中。例如 `org.archlinux.pkexec.gparted.policy` 包含一个操作：

```
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE policyconfig PUBLIC
 "-//freedesktop//DTD PolicyKit Policy Configuration 1.0//EN"
 "http://www.freedesktop.org/software/polkit/policyconfig-1.dtd">
<policyconfig>

  <action id="org.archlinux.pkexec.gparted">
    <message>Authentication is required to run the GParted Partition Editor</message>
    <icon_name>gparted</icon_name>
    <defaults>
      <allow_any>auth_admin</allow_any>
      <allow_inactive>auth_admin</allow_inactive>
      <allow_active>auth_admin</allow_active>
    </defaults>
    <annotate key="org.freedesktop.policykit.exec.path">/usr/bin/gparted</annotate>
    <annotate key="org.freedesktop.policykit.exec.allow_gui">true</annotate>
  </action>

</policyconfig>

```

**id** 属性是发送给 [D-Bus](/index.php/D-Bus "D-Bus") 的命令，**message** 属性用来在身份认证时向用户解释当前动作，**icon_name** 是图标。

**defaults** 标签下定义权限。包含三种设置：**allow_any**、**allow_inactive** 和 **allow_active**。 Inactive 会话是远程会话（例如 SSH、VNC 等。）active 会话是本地终端或图形界面直接登录机器的会话。allow_any 同时包含两种会话。

对每个设置，都有如下选项：

*   *no*：不允许用户执行操作，不需要身份认证。
*   *yes*：用户可以不进行认证就执行操作。
*   *auth_self*：需要认证，但是用户可以只输入自己的密码，不需要属于管理员。
*   *auth_admin*：需要用户认证为管理员。
*   *auth_self_keep*：和 auth_self 类似，认证状态会保持一段时间。
*   *auth_admin_keep*：和 auth_admin 类似，认证状态会保持一段时间。

这些设置是默认设置，只要没有被配置规则覆盖，适用于所有用户。

从上面的 Gparted 操作示例可以看出，不管用户是本地还是远程，都需要先认证为管理员之后才能使用 GParted。

### 认证规则

认证规则可以覆盖默认的设置，个人使用的单个系统设置，应该放到 `/etc/polkit-1/rules.d` 目录。

`addRule()` 方法可以增加一个函数，输入操作和用户，只要进行权限检查，这个函数就会被调用。所有函数会按添加顺序依次调用，只要遇到第一个 return 返回。所以，要将规则放到其它规则前，需要将规则文件放到 `/etc/polkit-1/rules.d` 的其它规则之前，最早的检查是 `00-early-checks.rules`。

.rules 文件的层级是完全自解释的：

```
/* Allow users in admin group to run GParted without authentication */
polkit.addRule(function(action, subject) {
    if (action.id == "org.archlinux.pkexec.gparted" &&
        subject.isInGroup("admin")) {
        return polkit.Result.YES;
    }
});

```

上面函数检查操作 ID *（是否 org.archlinux.pkexec.gparted）*，再确认用户群组*（是否属于 admin ）*，如果是，返回 "yes"。

### 管理员身份认证

`addAdminRule()` 方法会添加一个在每个管理员认证时被执行的函数。此函数用来规定什么用户可被视作系统管理员。函数的输入是操作和用户，函数按顺序依次执行，直到第一个 return。

系统默认的配置位于 `50-default.rules`，如果要修改这个值，需要把自定义的身份确认函数加到 50 之前，比如 `40-default.rules`。

 `/etc/polkit-1/rules.d/50-default.rules` 
```
polkit.addAdminRule(function(action, subject) {
    return ["unix-group:wheel"];
});
```

需要配置的是 return 返回值：输入谁的密码之后就被认为是系统管理员。如果用户自己属于管理员群组，只需要输入自己的密码。如果只有 root 是管理员，需要输入 root 密码。

Arch 的默认设置中会将所有 **wheel** 群组用户视作管理员，如果用下面的规则文件，那么用户需要输入 root 用户密码才会被认为是管理员。

 `/etc/polkit-1/rules.d/49-rootpw_global.rules` 
```
/* Always authenticate Admins by prompting for the root
 * password, similar to the rootpw option in sudo
 */
polkit.addAdminRule(function(action, subject) {
    return ["unix-user:root"];
});

```

## 范例

### 禁用挂起和休眠

下面规则禁止所有用户通过 Polkit 进行挂起和休眠。

 `/etc/polkit-1/rules.d/10-disable-suspend.rules` 
```
polkit.addRule(function(action, subject) {
    if (action.id == "org.freedesktop.login1.suspend" ||
        action.id == "org.freedesktop.login1.suspend-multiple-sessions" ||
        action.id == "org.freedesktop.login1.hibernate" ||
        action.id == "org.freedesktop.login1.hibernate-multiple-sessions")
    {
        return polkit.Result.NO;
    }
});
```

### 跳过口令提示

要模拟 [sudo](/index.php/Sudo "Sudo") 的 `NOPASSWD` 选项，完全根据 [user/group](/index.php/Users_and_groups "Users and groups") 身份进行认证，可以在 `/etc/polkit-1/rules.d/` 中创建规则进行设置。参考：[示例](https://gist.github.com/4013294/ccacedd69d54de7f2fd5881b546d5192d6a2bddb).

#### 全局规则

创建下列文件：

 `/etc/polkit-1/rules.d/49-nopasswd_global.rules` 
```
/* Allow members of the wheel group to execute any actions
 * without password authentication, similar to "sudo NOPASSWD:"
 */
polkit.addRule(function(action, subject) {
    if (subject.isInGroup("wheel")) {
        return polkit.Result.YES;
    }
});

```

请将 `wheel` 替换为需要的群组。 设置完成后，所有操作通过 Polkit 授权时，都不需要密码。因此，请仔细选择授权的群组。

#### 针对特定的动作设置

创建文件：

 `/etc/polkit-1/rules.d/49-nopasswd_limited.rules` 
```
/* Allow members of the wheel group to execute the defined actions 
 * without password authentication, similar to "sudo NOPASSWD:"
 */
polkit.addRule(function(action, subject) {
    if ((action.id == "org.archlinux.pkexec.gparted" ||
	 action.id == "org.libvirt.unix.manage") &&
        subject.isInGroup("wheel"))
    {
        return polkit.Result.YES;
    }
});

```

示例中 `action.id` 选择了 GParted 和 [Libvirt](/index.php/Libvirt "Libvirt")，可以根据需要进行选择。`||` 操作符是“或”操作，`&&` 是“与”操作。

#### Udisks

[文件管理器](/index.php/File_manager "File manager")在挂载磁盘时可能要求输入密码，或报告 *Not authorized* 或类似错误，详情请查看：[Udisks#Configuration](/index.php/Udisks#Configuration "Udisks").

### 允许一般用户管理某个 systemd 单元

通过检查 polkit 策略中的某些值，可以指定某些用户和群组管理 systemd 的权限。例如下面配置允许一般用户启动和停止 [wpa_supplicant](/index.php/Wpa_supplicant "Wpa supplicant")：

 `/etc/polkit-1/rules.d/10-wifimanagement.rules` 
```
polkit.addRule(function(action, subject) {
    if (action.id == "org.freedesktop.systemd1.manage-units") {
        if (action.lookup("unit") == "wpa_supplicant.service") {
            var verb = action.lookup("verb");
            if (verb == "start" || verb == "stop" || verb == "restart") {
                return polkit.Result.YES;
            }
        }
    }
});

```

## 参阅

*   [Polkit 手册页面](http://www.freedesktop.org/software/polkit/docs/latest/polkit.8.html)