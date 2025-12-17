Ссылки по теме

*   [Устранение часто встречающихся неполадок#Разрешения сессии](/index.php/%D0%A3%D1%81%D1%82%D1%80%D0%B0%D0%BD%D0%B5%D0%BD%D0%B8%D0%B5_%D1%87%D0%B0%D1%81%D1%82%D0%BE_%D0%B2%D1%81%D1%82%D1%80%D0%B5%D1%87%D0%B0%D1%8E%D1%89%D0%B8%D1%85%D1%81%D1%8F_%D0%BD%D0%B5%D0%BF%D0%BE%D0%BB%D0%B0%D0%B4%D0%BE%D0%BA#.D0.A0.D0.B0.D0.B7.D1.80.D0.B5.D1.88.D0.B5.D0.BD.D0.B8.D1.8F_.D1.81.D0.B5.D1.81.D1.81.D0.B8.D0.B8 "Устранение часто встречающихся неполадок")
*   [Sudo](/index.php/Sudo "Sudo")
*   [Пользователи и группы](/index.php/%D0%9F%D0%BE%D0%BB%D1%8C%D0%B7%D0%BE%D0%B2%D0%B0%D1%82%D0%B5%D0%BB%D0%B8_%D0%B8_%D0%B3%D1%80%D1%83%D0%BF%D0%BF%D1%8B "Пользователи и группы")

Выдержка из [домашней страницы polkit](http://www.freedesktop.org/wiki/Software/polkit/):

	*polkit — это средство для управления правами приложений пользовательского уровня, позволяющее непривилегированным процессам решать административные задачи: единый интерфейс предоставления прав доступа к привилегированным операциям для непривилегированных приложений при помощи набора правил (политик) и шины D-Bus.*

Polkit используется для управления общесистемными привилегиями. Данный фреймворк используется для предоставления непривилегированным процессам возможность выполнения действий, требующих прав администратора. В отличие от sudo, Polkit не наделяет процесс правами суперпользователя, а позволяет точно контролировать, какие действия разрешены, а какие нет.

Polkit может контролировать отдельные действия, такие как запуск GParted: при этом он проверяет имя пользователя и принадлежность оного к группе, например, является ли он членом группы wheel. Далее Polkit проверяет, какими правами наделены пользователи данной группы (есть ли вообще права на запуск?) и, если всё сходится (пользователь в нужной группе и у группы есть соответствующие права), требует ввести пароль для идентификации пользователя.

## Contents

*   [1 Установка](#.D0.A3.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B0)
    *   [1.1 Агенты аутентификации](#.D0.90.D0.B3.D0.B5.D0.BD.D1.82.D1.8B_.D0.B0.D1.83.D1.82.D0.B5.D0.BD.D1.82.D0.B8.D1.84.D0.B8.D0.BA.D0.B0.D1.86.D0.B8.D0.B8)
*   [2 Конфигурация](#.D0.9A.D0.BE.D0.BD.D1.84.D0.B8.D0.B3.D1.83.D1.80.D0.B0.D1.86.D0.B8.D1.8F)
    *   [2.1 Actions](#Actions)
    *   [2.2 Правила авторизации](#.D0.9F.D1.80.D0.B0.D0.B2.D0.B8.D0.BB.D0.B0_.D0.B0.D0.B2.D1.82.D0.BE.D1.80.D0.B8.D0.B7.D0.B0.D1.86.D0.B8.D0.B8)
    *   [2.3 Administrator identities](#Administrator_identities)
*   [3 Примеры](#.D0.9F.D1.80.D0.B8.D0.BC.D0.B5.D1.80.D1.8B)
    *   [3.1 Debugging/logging](#Debugging.2Flogging)
    *   [3.2 Disable suspend and hibernate](#Disable_suspend_and_hibernate)
    *   [3.3 Bypass password prompt](#Bypass_password_prompt)
        *   [3.3.1 Globally](#Globally)
        *   [3.3.2 For specific actions](#For_specific_actions)
        *   [3.3.3 Udisks](#Udisks)
    *   [3.4 Allow management of individual systemd units by regular users](#Allow_management_of_individual_systemd_units_by_regular_users)
*   [4 See also](#See_also)

## Установка

Установите пакет [polkit](https://www.archlinux.org/packages/?name=polkit).

### Агенты аутентификации

Агент аутентификации используется для установления подлинности оператора либо как обычный пользователь (путём ввода пароля пользователя), либо как суперпользователь (путём ввода пароля рута). Пакет [polkit](https://www.archlinux.org/packages/?name=polkit) содержит текстовый агент аутентификации, 'pkttyagent', который используется в качестве запасного варианта.

Если вы пользуетесь графической оболочкой, убедитесь, что установлен графический агент аутентификации и что он [автоматически запускается](/index.php/Autostarting_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Autostarting (Русский)") при входе в систему.

Такие графические оболочки как [Cinnamon](/index.php/Cinnamon "Cinnamon"), [Deepin](/index.php/Deepin "Deepin"), [GNOME](/index.php/GNOME "GNOME"), [GNOME Flashback](/index.php/GNOME_Flashback "GNOME Flashback"), [KDE](/index.php/KDE "KDE"), [LXDE](/index.php/LXDE "LXDE"), [LXQt](/index.php/LXQt "LXQt"), [MATE](/index.php/MATE "MATE"), и [Xfce](/index.php/Xfce "Xfce") уже имеют в своём составе агенты аутентификации. В других графических окружениях вы можете выбрать одну из реализаций:

*   [lxqt-policykit](https://www.archlinux.org/packages/?name=lxqt-policykit), который предоставляет `/usr/bin/lxqt-policykit-agent`
*   [lxsession](https://www.archlinux.org/packages/?name=lxsession), который предоставляет `/usr/bin/lxpolkit`
*   [mate-polkit](https://www.archlinux.org/packages/?name=mate-polkit), который предоставляет `/usr/lib/mate-polkit/polkit-mate-authentication-agent-1`
*   [polkit-efl-git](https://aur.archlinux.org/packages/polkit-efl-git/), который предоставляет `/usr/bin/polkit-efl-authentication-agent-1`
*   [polkit-gnome](https://www.archlinux.org/packages/?name=polkit-gnome), который предоставляет `/usr/lib/polkit-gnome/polkit-gnome-authentication-agent-1`
*   [polkit-kde-agent](https://www.archlinux.org/packages/?name=polkit-kde-agent), который предоставляет `/usr/lib/polkit-kde/polkit-kde-authentication-agent-1`
*   [ts-polkitagent](https://aur.archlinux.org/packages/ts-polkitagent/), который предоставляет `/usr/lib/ts-polkitagent`
*   [xfce-polkit-git](https://aur.archlinux.org/packages/xfce-polkit-git/), который предоставляет `/usr/lib/xfce-polkit/xfce-polkit`

## Конфигурация

**Warning:** Do not amend the default permission files of packages, as these may be be overwritten on package upgrades.

Polkit definitions can be divided into two kinds:

*   **Actions** are defined in XML `.policy` files located in `/usr/share/polkit-1/actions`. Each action has a set of default permissions attached to it (e.g. you need to identify as an administrator to use the GParted action). Значения по умолчанию могут быть отменены, но редактирование файлов действий - это неправильный способ.
*   **Authorization rules** are defined in JavaScript `.rules` files. They are found in two places: 3rd party packages can use `/usr/share/polkit-1/rules.d` (though few if any do) and `/etc/polkit-1/rules.d` is for local configuration.

Polkit работает поверх существующих в Linux систем разрешений – членства в группах, статуса администратора – но не заменяет их. Файлы .rules определяют подмножество пользователей, ссылаются на одно (или более) из действий, указанных в файлах actions, и определяют, с какими ограничениями эти действия могут выполняться этим пользователем (ами). Например, файл правил может отменить требование по умолчанию для всех пользователей проходить аутентификацию в качестве администратора при использовании GParted, определение того, что какому-то конкретному пользователю не нужно. Or isn't allowed to use GParted at all.

**Note:** Это не исключает запуска GParted средствами, которые не поддерживают polkit, такими как командная строка. Следовательно, polkit следует использовать для расширения доступа к привилегированным сервисам для непривилегированных пользователей, а не пытаться ограничить права (полу-)привилегированных пользователей. For security purposes, [sudoers](/index.php/Sudo "Sudo") is still the way to go.

### Actions

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

The **defaults** тег - это место, где находятся разрешения или их отсутствие. It contains three settings: **allow_any**, **allow_inactive**, and **allow_active**. Inactive sessions are generally remote sessions (SSH, VNC, etc.) whereas active sessions are logged directly into the machine on a TTY or an X display. allow_any is the setting encompassing both scenarios.

For each of these settings the following options are available:

*   *no*: The user is not authorized to carry out the action. There is therefore no need for authentication.
*   *yes*: Пользователь имеет право выполнять это действие без какой-либо аутентификации.
*   *auth_self*: Authentication требуется, но пользователь не обязательно должен быть администратором.
*   *auth_admin*: Authentication as an administrative user is required.
*   *auth_self_keep*: The same as auth_self but, like sudo, авторизация длится несколько минут.
*   *auth_admin_keep*: The same as auth_admin but, like sudo, авторизация длится несколько минут.

These are default setting and unless overruled in later configuration will be valid for all users.

As can be seen from the GParted action, users are required to authenticate as administrators in order to use GParted, regardless of whether the session is active or inactive.

### Правила авторизации

Authorization rules that overrule the default settings are laid out in a set of directories as described above. For all purposes relating to personal configuration of a single system, only `/etc/polkit-1/rules.d` should be used.

The `addRule()` метод используется для добавления функции, которая может быть вызвана всякий раз, когда выполняется проверка авторизации для действия и субъекта. Функции вызываются в порядке их добавления, пока одна из функций не вернет значение. Следовательно, чтобы добавить правило авторизации, которое обрабатывается раньше других правил, поместите его в файл внутри `/etc/polkit-1/rules.d` с именем, которое сортируется перед другими файлами правил, например `00-early-checks.rules`.

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

### Administrator identities

The `addAdminRule()` метод используется для добавления функции, которая может вызываться всякий раз, когда требуется аутентификация администратора. Функция используется для указания того, какие идентификаторы могут использоваться для аутентификации администратора при проверке авторизации, определенной по действию и субъекту. Добавленные функции вызываются в том порядке, в котором они были добавлены, до тех пор, пока одна из функций не вернет значение.

The default configuration for administrator identities is contained in the file `50-default.rules` so any changes to that configuration should be made by copying the file to, say, `40-default.rules` and editing that file.

 `/etc/polkit-1/rules.d/50-default.rules` 
```
polkit.addAdminRule(function(action, subject) {
    return ["unix-group:wheel"];
});
```

Единственная часть, которую нужно отредактировать (после копирования), - это возвращаемый массив функции: от имени кого пользователь должен проходить аутентификацию, когда его попросят пройти аутентификацию в качестве администратора? Если он сам является членом группы, обозначенной как "администраторы", ему нужно только ввести свой собственный пароль. Если какой-либо другой пользователь, например root, является единственным администратором, ему нужно будет ввести пароль root. Формат идентификации пользователя такой же, как и тот, который используется при назначении полномочий.

По умолчанию Arch назначает администраторами всех участников группы wheel. В соответствии с приведенным ниже правилом polkit будет запрашивать пароль root вместо пароля пользователя для аутентификации администратора.

 `/etc/polkit-1/rules.d/49-rootpw_global.rules` 
```
/* Always authenticate Admins by prompting for the root
 * password, similar to the rootpw option in sudo
 */
polkit.addAdminRule(function(action, subject) {
    return ["unix-user:root"];
});

```

## Примеры

### Debugging/logging

The following rule logs detailed information about any requested access.

 `/etc/polkit-1/rules.d/00-log-access.rules` 
```
polkit.addRule(function(action, subject) {
    polkit.log("action=" + action);
    polkit.log("subject=" + subject);
});
```

### Disable suspend and hibernate

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

### Bypass password prompt

To achieve something similar to the [sudo](/index.php/Sudo "Sudo") `NOPASSWD` option and get authorized solely based on [user/group](/index.php/Users_and_groups "Users and groups") identity, you can create custom rules in `/etc/polkit-1/rules.d/`. This allows you to override password authentication either [only for specific actions](#For_specific_actions) or [globally](#Globally). See [[1]](https://gist.github.com/4013294/ccacedd69d54de7f2fd5881b546d5192d6a2bddb) for an example rule set.

#### Globally

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

#### For specific actions

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

The `||` оператор используется для разграничения действий (logical OR), and `&&` means logical AND and must be kept as the last operator.

#### Udisks

[File managers](/index.php/File_manager "File manager") may ask for a password when trying to mount a storage device, or yield a *Not authorized* or similar error. See [Udisks#Configuration](/index.php/Udisks#Configuration "Udisks") for details.

### Разрешить управление отдельными systemd units обычным пользователям

By checking for certain values passed to the polkit policy check, you can give specific users or groups the ability to manage specific units. As an example, you might want regular users to start and stop [wpa_supplicant](/index.php/Wpa_supplicant "Wpa supplicant"):

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

## See also

*   [Polkit manual page](http://www.freedesktop.org/software/polkit/docs/latest/polkit.8.html)
