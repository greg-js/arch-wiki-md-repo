Related articles

*   [Laptop](/index.php/Laptop "Laptop")
*   [Laptop Mode Tools](/index.php/Laptop_Mode_Tools "Laptop Mode Tools")

来自[项目主页](http://linrunner.de/en/tlp/tlp.html):

	TLP在不需要您了解所有技术细节的情况下给您带来优秀的Linux高级电源管理方案。TLP默认带有对电池使用时间最优化的配置，所以你只需要安装即可享受延长的使用时间。不过，TLP也是高度可配置的以满足您的特定需求。

## Contents

*   [1 安装](#.E5.AE.89.E8.A3.85)
    *   [1.1 只对Thinkpad有用的功能](#.E5.8F.AA.E5.AF.B9Thinkpad.E6.9C.89.E7.94.A8.E7.9A.84.E5.8A.9F.E8.83.BD)
*   [2 = 图形界面](#.3D_.E5.9B.BE.E5.BD.A2.E7.95.8C.E9.9D.A2)
*   [3 配置](#.E9.85.8D.E7.BD.AE)

## 安装

从[官方源](/index.php/%E5%AE%98%E6%96%B9%E6%BA%90 "官方源")[安装](/index.php/%E5%AE%89%E8%A3%85 "安装")[tlp](https://www.archlinux.org/packages/?name=tlp) - 注意它可能可以用于提供更佳的省电性能的可选依赖。

为了完成TLP的安装，您必须[启用systemd](/index.php/%E5%90%AF%E7%94%A8 "启用")服务`tl.service`以及`tlp-sleep.service`。您也应该[标记掉systemd](/index.php?title=%E6%A0%87%E8%AE%B0%E6%8E%89&action=edit&redlink=1 "标记掉 (page does not exist)")服务`systemd-rfkill.service`以及套接字`systemd-rfkill.socket`来防止冲突并保证TLP无线设备的开关选项的正确运行。

**注意:** 如果`NetworkManager.service`可用的话，`tlp.service` 将启动 `NetworkManager.service`；[FS#43733](https://bugs.archlinux.org/task/43733)。如果您使用不同的[网络管理器](/index.php/List_of_applications#Network_managers "List of applications")，编辑`tlp.service`来去除服务(line`Wants`)或[标记掉](/index.php?title=%E6%A0%87%E8%AE%B0%E6%8E%89&action=edit&redlink=1 "标记掉 (page does not exist)")它。

### 只对Thinkpad有用的功能

如果需要更优化的电池管理功能，比如充电阈值控制以及电池校准，安装下列软件包：

*   [tp_smapi](https://www.archlinux.org/packages/?name=tp_smapi) - 电池充电阈值控制，电池校准和特殊的tlp-stat输出需要tp-smapi。
*   [acpi_call](https://www.archlinux.org/packages/?name=acpi_call) - 在Sandy Bridge及更新型号（X220/T420,X230/T430等）的电池充电阈值控制和电池校准需要acpi-call。

访问TLP问答板块 ["Which kernel module?"](http://linrunner.de/en/tlp/docs/tlp-faq.html#kernmod)以获取详情。

使用[threshy](https://aur.archlinux.org/packages/threshy/)及其Qt图形界面[threshy-gui](https://aur.archlinux.org/packages/threshy-gui/)可在不使用Root权限的情况下用D-Bus控制电池充电阈值。

## = 图形界面

[tlpui-git](https://aur.archlinux.org/packages/tlpui-git/)是用Python和GTK编写的TLP的图形界面。该软件还处于测试阶段。

## 配置