**翻译状态：** 本文是英文页面 [Polkit](/index.php/Polkit "Polkit") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2016-03-20，点击[这里](https://wiki.archlinux.org/index.php?title=Polkit&diff=0&oldid=411919)可以查看翻译后英文页面的改动。

来自 [polkit 主页](http://www.freedesktop.org/wiki/Software/polkit/)：

	*polkit is an application-level toolkit for defining and handling the policy that allows unprivileged processes to speak to privileged processes: It is a framework for centralizing the decision making process with respect to granting access to privileged operations for unprivileged applications.*

Polkit is used for controlling system-wide privileges. It provides an organized way for non-privileged processes to communicate with privileged ones. In contrast to systems such as sudo, it does not grant root permission to an entire process, but rather allows a finer level of control of centralized system policy.

Polkit works by delimiting distinct actions, e.g. running GParted, and delimiting users by group or by name, e.g. members of the wheel group. It then defines how – if at all – those users are allowed those actions, e.g. by identifying as members of the group by typing in their passwords.

## Contents

*   [1 安装](#.E5.AE.89.E8.A3.85)
    *   [1.1 认证代理](#.E8.AE.A4.E8.AF.81.E4.BB.A3.E7.90.86)
*   [2 架构](#.E6.9E.B6.E6.9E.84)
    *   [2.1 行为](#.E8.A1.8C.E4.B8.BA)
    *   [2.2 认证规则](#.E8.AE.A4.E8.AF.81.E8.A7.84.E5.88.99)
        *   [2.2.1 管理员标识](#.E7.AE.A1.E7.90.86.E5.91.98.E6.A0.87.E8.AF.86)
*   [3 界限](#.E7.95.8C.E9.99.90)
*   [4 范例](#.E8.8C.83.E4.BE.8B)
    *   [4.1 禁用挂起和休眠](#.E7.A6.81.E7.94.A8.E6.8C.82.E8.B5.B7.E5.92.8C.E4.BC.91.E7.9C.A0)
    *   [4.2 跳过口令提示](#.E8.B7.B3.E8.BF.87.E5.8F.A3.E4.BB.A4.E6.8F.90.E7.A4.BA)
        *   [4.2.1 特定行为](#.E7.89.B9.E5.AE.9A.E8.A1.8C.E4.B8.BA)
        *   [4.2.2 Udisks](#Udisks)
        *   [4.2.3 全局规则](#.E5.85.A8.E5.B1.80.E8.A7.84.E5.88.99)
    *   [4.3 要求 root 口令](#.E8.A6.81.E6.B1.82_root_.E5.8F.A3.E4.BB.A4)
*   [5 参阅](#.E5.8F.82.E9.98.85)

## 安装

安装 [polkit](https://www.archlinux.org/packages/?name=polkit) 包。

### 认证代理

An authentication agent is used to make the user of a session prove that the user of the session really is the user (by authenticating as the user) or an administrative user (by authenticating as an administrator). The [polkit](https://www.archlinux.org/packages/?name=polkit) package contains a textual authentication agent called 'pkttyagent', which is used as a general fallback.

If you are using a graphical environment, make sure that a graphical authentication agent is installed and [autostarted](/index.php/Autostarting "Autostarting") on login.

[Cinnamon](/index.php/Cinnamon "Cinnamon"), [Deepin](/index.php/Deepin_Desktop_Environment "Deepin Desktop Environment"), [GNOME](/index.php/GNOME "GNOME"), [GNOME Flashback](/index.php/GNOME_Flashback "GNOME Flashback"), [KDE](/index.php/KDE "KDE"), [LXDE](/index.php/LXDE "LXDE"), [LXQt](/index.php/LXQt "LXQt"), [MATE](/index.php/MATE "MATE") and [Xfce](/index.php/Xfce "Xfce") have an authentication agent already. In other desktop environments, you have to choose one of the following implementations:

*   [lxqt-policykit](https://www.archlinux.org/packages/?name=lxqt-policykit), which provides `/usr/bin/lxqt-policykit-agent`
*   [lxsession](https://www.archlinux.org/packages/?name=lxsession), which provides `/usr/bin/lxpolkit`
*   [mate-polkit](https://www.archlinux.org/packages/?name=mate-polkit), which provides `/usr/lib/mate-polkit/polkit-mate-authentication-agent-1`
*   [polkit-efl-git](https://aur.archlinux.org/packages/polkit-efl-git/), which provides `/usr/bin/polkit-efl-authentication-agent-1`
*   [polkit-gnome](https://www.archlinux.org/packages/?name=polkit-gnome), which provides `/usr/lib/polkit-gnome/polkit-gnome-authentication-agent-1`
*   [polkit-kde-agent](https://www.archlinux.org/packages/?name=polkit-kde-agent), which provides `/usr/lib/polkit-kde/polkit-kde-authentication-agent-1`
*   [xfce-polkit-git](https://aur.archlinux.org/packages/xfce-polkit-git/), which provides `/usr/lib/xfce-polkit/xfce-polkit`

## 架构

**Warning:** Do not amend the default permission files of packages, as these may be be overwritten on package upgrades.

Polkit definitions can be divided into two kinds:

*   **Actions** are defined in XML `.policy` files located in `/usr/share/polkit-1/actions`. Each action has a set of default permissions attached to it (e.g. you need to identify as an administrator to use the GParted action). The defaults can be overruled but editing the actions files is NOT the correct way.
*   **Authorization rules** are defined in JavaScript `.rules` files. They are found in two places: 3rd party packages can use `/usr/share/polkit-1/rules.d` (though few if any do) and `/etc/polkit-1/rules.d` is for local configuration. The .rules files designate a subset of users, refer to one (or more) of the actions specified in the actions files and determine with what restrictions these actions can be taken by that/those user(s). As an example, a rules file could overrule the default requirement for all users to authenticate as an admin when using GParted, determining that some specific user doesn't need to. Or isn't allowed to use GParted at all.

### 行为

**Tip:** To display Policykit actions in a graphical interface, install the [polkit-explorer](https://aur.archlinux.org/packages/polkit-explorer/) package.

The actions available to you via polkit will depend on the packages you have installed. Some are used in multiple desktop environments *(org.freedesktop.*)*, some are DE-specific *(org.gnome.*)* and some are specific to a single program *(org.archlinux.pkexec.gparted.policy)*. The command `pkaction` lists all the actions defined in `/usr/share/polkit-1/actions` for quick reference.

To get an idea of what polkit can do, here are a few commonly used groups of actions:

*   **[systemd-logind](/index.php/Systemd "Systemd")** *(org.freedesktop.login1.policy)* actions regulated by polkit include powering off, rebooting, suspending and hibernating the system, including when other users may still be logged in.
*   **[udisks](/index.php/Udisks "Udisks")** *(org.freedesktop.udisks2.policy)* actions regulated by polkit include mounting file systems and unlocking encrypted devices.
*   **[NetworkManager](/index.php/NetworkManager "NetworkManager")** *(org.freedesktop.NetworkManager.policy)* actions regulated by polkit include turning on and off the network, wifi or mobile broadband.

Each action is defined in an `<action>` tag in a .policy file. The `org.archlinux.pkexec.gparted.policy` contains a single action and looks like this:

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

The attribute **id** is the actual command sent to [D-Bus](/index.php/D-Bus "D-Bus"), the **message** tag is the explanation to the user when authentication is required and the **icon_name** is sort of obvious.

The **defaults** tag is where the permissions or lack thereof are located. It contains three settings: **allow_any**, **allow_inactive**, and **allow_active**. Inactive sessions are generally remote sessions (SSH, VNC, etc.) whereas active sessions are logged directly into the machine on a TTY or an X display. allow_any is the setting encompassing both scenarios.

For each of these settings the following options are available:

*   *no*: The user is not authorized to carry out the action. There is therefore no need for authentication.
*   *yes*: The user is authorized to carry out the action without any authentication.
*   *auth_self*: Authentication is required but the user need not be an administrative user.
*   *auth_admin*: Authentication as an administrative user is require.
*   *auth_self_keep*: The same as auth_self but, like sudo, the authorization lasts a few minutes.
*   *auth_admin_keep*: The same as auth_admin but, like sudo, the authorization lasts a few minutes.

These are default setting and unless overruled in later configuration will be valid for all users.

As can be seen from the GParted action, users are required to authenticate as administrators in order to use GParted, regardless of whether the session is active or inactive.

### 认证规则

Authorization rules that overrule the default settings are laid out in a set of directories as described above. For all purposes relating to personal configuration of a single system, only `/etc/polkit-1/rules.d` should be used.

The `addRule()` method is used for adding a function that may be called whenever an authorization check for action and subject is performed. Functions are called in the order they have been added until one of the functions returns a value. Hence, to add an authorization rule that is processed before other rules, put it in a file in `/etc/polkit-1/rules.d` with a name that sorts before other rules files, for example `00-early-checks.rules`.

The layout of the .rules files is fairly self-explanatory:

```
/* Allow users in admin group to run GParted without authentication */
polkit.addRule(function(action, subject) {
    if (action.id == "org.archlinux.pkexec.gparted" &&
        subject.isInGroup("admin")) {
        return polkit.Result.YES;
    }
});

```

Inside the function, we check for the specified action ID *(org.archlinux.pkexec.gparted)* and for the user's group *(admin)*, then return a value "yes".

#### 管理员标识

The `addAdminRule()` method is used for adding a function that may be called whenever administrator authentication is required. The function is used to specify what identities may be used for administrator authentication for the authorization check identified by action and subject. Functions added are called in the order they have been added until one of the functions returns a value.

The default configuration for administrator identities is contained in the file `50-default.rules` so any changes to that configuration should be made by copying the file to, say, `40-default.rules` and editing that file.

 `/etc/polkit-1/rules.d/50-default.rules` 
```
polkit.addAdminRule(function(action, subject) {
    return ["unix-group:wheel"];
});
```

The only part to edit (once copied) is the return array of the function: as whom should a user authenticate when asked to authenticate as an administrative user? If she herself is a member of the group designated as admins, she only need enter her own password. If some other user, e.g. root, is the only admin identity, she would need to enter in root's password. The format of the user identification is the same as the one used in designating authorities. The Arch default is to make all members of the group **wheel** administrators.

## 界限

Polkit operates on top of the existing permissions systems in Linux – group membership, administrator status – it does not replace them. The example above prohibited the user *jack* from using the GParted action, but it does not preclude him running GParted by some means that do not respect polkit, e.g. the command line. Therefore it's probably better to use polkit to expand access to privileged services for unprivileged users, rather than to try using it to curtail the rights of (semi-)privileged users. For security purposes, the [sudoers file](/index.php/Sudo "Sudo") is still the way to go.

## 范例

### 禁用挂起和休眠

The following rule disables suspend and hibernate for all users.

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

To achieve something similar to the [sudo](/index.php/Sudo "Sudo") `NOPASSWD` option and get authorized solely based on [user/group](/index.php/Users_and_groups "Users and groups") identity, you can create custom rules in `/etc/polkit-1/rules.d/`. This allows you to override password authentication either [only for specific actions](#For_specific_actions) or [globally](#Globally). See [[1]](https://gist.github.com/4013294/ccacedd69d54de7f2fd5881b546d5192d6a2bddb) for an example rule set.

#### 特定行为

Create the following file as root:

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

The `action.id`s selected here are just (working) examples for GParted and [Libvirt](/index.php/Libvirt "Libvirt"), but you can replace them by any other of your liking as long as they exist (custom made or supplied by a package), and so can you define any group instead of `wheel`.

The `||` operator is used to delimit actions (logical OR), and `&&` means logical AND and must be kept as the last operator.

#### Udisks

[File managers](/index.php/File_manager "File manager") may ask for a password when trying to mount a storage device, or yield a *Not authorized* or similar error. See [Udisks#Configuration](/index.php/Udisks#Configuration "Udisks") for details.

#### 全局规则

Create the following file as root:

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

Replace `wheel` by any group of your preference.

This will result in automatic authentication for **any** action requiring admin rights via Polkit. As such, be careful with the group you choose to give such rights to.

### 要求 root 口令

A rule like this will have polkit ask for the root password instead of the users password for Admin authentication.

 `/etc/polkit-1/rules.d/49-rootpw_global.rules` 
```
/* Always authenticate Admins by prompting for the root
 * password, similar to the rootpw option in sudo
 */
polkit.addAdminRule(function(action, subject) {
    return ["unix-user:root"];
});

```

## 参阅

*   [Polkit 手册页面](http://www.freedesktop.org/software/polkit/docs/latest/polkit.8.html)