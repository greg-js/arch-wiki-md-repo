**翻譯狀態：** 本文章是 [Network_Configuration](/index.php/Network_Configuration "Network Configuration") 的翻譯版本。最近一次的翻譯時間：2014-05-02。點擊[本連結](https://wiki.archlinux.org/index.php?title=Network_Configuration&diff=0&oldid=311601)查看英文頁面之後的變更。

本頁將介紹如何設定**有線**網路連線。若您需要設定**無線**網路，請參考[無線網路設定](/index.php/Wireless_network_configuration "Wireless network configuration")。

## Contents

*   [1 檢查連線](#.E6.AA.A2.E6.9F.A5.E9.80.A3.E7.B7.9A)
*   [2 設定主機名稱](#.E8.A8.AD.E5.AE.9A.E4.B8.BB.E6.A9.9F.E5.90.8D.E7.A8.B1)
*   [3 裝置驅動程式](#.E8.A3.9D.E7.BD.AE.E9.A9.85.E5.8B.95.E7.A8.8B.E5.BC.8F)
    *   [3.1 檢查驅動程式狀態](#.E6.AA.A2.E6.9F.A5.E9.A9.85.E5.8B.95.E7.A8.8B.E5.BC.8F.E7.8B.80.E6.85.8B)
    *   [3.2 載入裝置模組](#.E8.BC.89.E5.85.A5.E8.A3.9D.E7.BD.AE.E6.A8.A1.E7.B5.84)
*   [4 網路介面](#.E7.B6.B2.E8.B7.AF.E4.BB.8B.E9.9D.A2)
    *   [4.1 裝置名稱](#.E8.A3.9D.E7.BD.AE.E5.90.8D.E7.A8.B1)
        *   [4.1.1 更改裝置名稱](#.E6.9B.B4.E6.94.B9.E8.A3.9D.E7.BD.AE.E5.90.8D.E7.A8.B1)
    *   [4.2 設定裝置的 MTU 與佇列長度](#.E8.A8.AD.E5.AE.9A.E8.A3.9D.E7.BD.AE.E7.9A.84_MTU_.E8.88.87.E4.BD.87.E5.88.97.E9.95.B7.E5.BA.A6)
    *   [4.3 取得目前的裝置名稱](#.E5.8F.96.E5.BE.97.E7.9B.AE.E5.89.8D.E7.9A.84.E8.A3.9D.E7.BD.AE.E5.90.8D.E7.A8.B1)
    *   [4.4 啟用與禁用網路介面](#.E5.95.9F.E7.94.A8.E8.88.87.E7.A6.81.E7.94.A8.E7.B6.B2.E8.B7.AF.E4.BB.8B.E9.9D.A2)
*   [5 組態設定 IP 位址](#.E7.B5.84.E6.85.8B.E8.A8.AD.E5.AE.9A_IP_.E4.BD.8D.E5.9D.80)
    *   [5.1 動態 IP 位址](#.E5.8B.95.E6.85.8B_IP_.E4.BD.8D.E5.9D.80)
        *   [5.1.1 dhcpcd](#dhcpcd)
    *   [5.2 靜態 IP 位址](#.E9.9D.9C.E6.85.8B_IP_.E4.BD.8D.E5.9D.80)
        *   [5.2.1 手動指派](#.E6.89.8B.E5.8B.95.E6.8C.87.E6.B4.BE)
        *   [5.2.2 永久於啟動時通過 systemd 進行組態設定與 udev 規則](#.E6.B0.B8.E4.B9.85.E6.96.BC.E5.95.9F.E5.8B.95.E6.99.82.E9.80.9A.E9.81.8E_systemd_.E9.80.B2.E8.A1.8C.E7.B5.84.E6.85.8B.E8.A8.AD.E5.AE.9A.E8.88.87_udev_.E8.A6.8F.E5.89.87)
        *   [5.2.3 計算位址](#.E8.A8.88.E7.AE.97.E4.BD.8D.E5.9D.80)
    *   [5.3 systemd-networkd](#systemd-networkd)
*   [6 載入組態設定](#.E8.BC.89.E5.85.A5.E7.B5.84.E6.85.8B.E8.A8.AD.E5.AE.9A)
*   [7 附加設定](#.E9.99.84.E5.8A.A0.E8.A8.AD.E5.AE.9A)
    *   [7.1 筆記型電腦之 ifplugd](#.E7.AD.86.E8.A8.98.E5.9E.8B.E9.9B.BB.E8.85.A6.E4.B9.8B_ifplugd)
    *   [7.2 Bonding 或 LAG](#Bonding_.E6.88.96_LAG)
    *   [7.3 IP 別名](#IP_.E5.88.A5.E5.90.8D)
        *   [7.3.1 範例](#.E7.AF.84.E4.BE.8B)
    *   [7.4 更改 MAC/硬體 位址](#.E6.9B.B4.E6.94.B9_MAC.2F.E7.A1.AC.E9.AB.94_.E4.BD.8D.E5.9D.80)
    *   [7.5 網路共享](#.E7.B6.B2.E8.B7.AF.E5.85.B1.E4.BA.AB)
    *   [7.6 路由組態設定](#.E8.B7.AF.E7.94.B1.E7.B5.84.E6.85.8B.E8.A8.AD.E5.AE.9A)
    *   [7.7 區域網路主機名稱解析](#.E5.8D.80.E5.9F.9F.E7.B6.B2.E8.B7.AF.E4.B8.BB.E6.A9.9F.E5.90.8D.E7.A8.B1.E8.A7.A3.E6.9E.90)
    *   [7.8 雜亂模式](#.E9.9B.9C.E4.BA.82.E6.A8.A1.E5.BC.8F)
*   [8 診斷](#.E8.A8.BA.E6.96.B7)
    *   [8.1 Swapping computers on the cable modem](#Swapping_computers_on_the_cable_modem)
    *   [8.2 The TCP window scaling problem](#The_TCP_window_scaling_problem)
        *   [8.2.1 How to diagnose the problem](#How_to_diagnose_the_problem)
        *   [8.2.2 How to fix it (The bad way)](#How_to_fix_it_.28The_bad_way.29)
        *   [8.2.3 How to fix it (The good way)](#How_to_fix_it_.28The_good_way.29)
        *   [8.2.4 How to fix it (The best way)](#How_to_fix_it_.28The_best_way.29)
        *   [8.2.5 More about it](#More_about_it)
    *   [8.3 Realtek no link / WOL problem](#Realtek_no_link_.2F_WOL_problem)
        *   [8.3.1 Method 1 - Enable the NIC directly in Linux](#Method_1_-_Enable_the_NIC_directly_in_Linux)
        *   [8.3.2 Method 2 - Rollback/change Windows driver](#Method_2_-_Rollback.2Fchange_Windows_driver)
        *   [8.3.3 Method 3 - Enable WOL in Windows driver](#Method_3_-_Enable_WOL_in_Windows_driver)
        *   [8.3.4 Method 4 - Newer Realtek Linux driver](#Method_4_-_Newer_Realtek_Linux_driver)
        *   [8.3.5 Method 5 - Enable *LAN Boot ROM* in BIOS/CMOS](#Method_5_-_Enable_LAN_Boot_ROM_in_BIOS.2FCMOS)
    *   [8.4 No interface with Atheros chipsets](#No_interface_with_Atheros_chipsets)
    *   [8.5 Broadcom BCM57780](#Broadcom_BCM57780)

## 檢查連線

**註記:** 若您在執行 ping 時收到了類似 `ping: icmp open socket: Operation not permitted` 這樣的錯誤訊息，請嘗試重新安裝 `iputils` 軟體包。

一般來說，基本的安裝過程都已經建立了可運作的網路設定。請執行下列指令以進行檢查：

**註記:** `-c 3` 選項表示將會呼叫三次。詳細請參閱 `man ping` 。

**提示：** 您也可以嘗試使用其他的 Domain ，如 www.hinet.net 。
 `$ ping -c 3 www.google.com` 
```
PING www.l.google.com (74.125.224.146) 56(84) bytes of data.
64 bytes from 74.125.224.146: icmp_req=1 ttl=50 time=437 ms
64 bytes from 74.125.224.146: icmp_req=2 ttl=50 time=385 ms
64 bytes from 74.125.224.146: icmp_req=3 ttl=50 time=298 ms

--- www.l.google.com ping statistics ---
3 packets transmitted, 3 received, 0% packet loss, time 1999ms
rtt min/avg/max/mdev = 298.107/373.642/437.202/57.415 ms

```

如果沒問題的話，您可能只是想以本文的下列部分來自定您的設定。

若剛才的指令出現了 unknown hosts 之類的訊息，代表您的機器無法解析網域。這可能是因為您的網路服務提供商/閘道造成的。您可以嘗試 ping 一個靜態 IP 以實驗您的機器能否存取網際網路。

**提示：** 您也可以嘗試使用其他的 IP ，如 168.95.1.1 。
 `$ ping -c 3 8.8.8.8` 
```
PING 8.8.8.8 (8.8.8.8) 56(84) bytes of data.
64 bytes from 8.8.8.8: icmp_req=1 ttl=53 time=52.9 ms
64 bytes from 8.8.8.8: icmp_req=2 ttl=53 time=72.5 ms
64 bytes from 8.8.8.8: icmp_req=3 ttl=53 time=70.6 ms

--- 8.8.8.8 ping statistics ---
3 packets transmitted, 3 received, 0% packet loss, time 2002ms
rtt min/avg/max/mdev = 52.975/65.375/72.543/8.803 ms

```

**註記:** `8.8.8.8` 為一個好記的靜態 IP 位置。這是 Google 的主要 DNS 伺服器，這表示其有一定的可信度，並且通常不會被系統或代理伺服器擋下。

若您可以 Ping 通 `8.8.8.8` ，但 `www.google.com` 不能，請檢查您的 DNS 組態設定檔。詳情請參考 [resolv.conf](/index.php/Resolv.conf "Resolv.conf")。

## 設定主機名稱

[主機名稱](https://en.wikipedia.org/wiki/Hostname "wikipedia:Hostname")為網路中用於識別機器的唯一識別名稱：主機名稱可以通過 `/etc/hostname` 檔案來進行設定。一般來說該檔案包含了系統的網域名稱。下面為設定主機名稱的方法：

```
# hostnamectl set-hostname **myhostname**

```

這樣會將 `*myhostname*` 寫入 `/etc/hostname` 檔案中。

詳細請參閱 `man 5 hostname` 與 `man 1 hostnamectl` 。

在 `/etc/hosts` 中加入相同的主機名稱：

 `/etc/hosts` 
```

#<ip-address> <hostname.domain.org> <hostname>
127.0.0.1 localhost.localdomain localhost *myhostname*
::1 localhost.localdomain localhost

```

使用來自 [inetutils](https://www.archlinux.org/packages/?name=inetutils) 的 *hostname* 以設定臨時主機名稱（直到重新啟動）：

```
# hostname *myhostname*

```

## 裝置驅動程式

### 檢查驅動程式狀態

[udev](/index.php/Udev "Udev") 應該會檢測您的網路介面卡（[NIC](https://en.wikipedia.org/wiki/Network_interface_controller "wikipedia:Network interface controller")）並自動於啟動時載入必要的模組。檢查 `lspci -v` 輸出內容中的「Ethernet controller」 項目（或類似的）。這應該會告訴您哪些核心模組包含了網路設備的驅動程式。舉例來說：

 `$ lspci -v` 
```
02:00.0 Ethernet controller: Attansic Technology Corp. L1 Gigabit Ethernet Adapter (rev b0)
 	...
 	Kernel driver in use: atl1
 	Kernel modules: atl1

```

接下來，確認該驅動程式已經通過 `dmesg | grep *module_name*` 載入了。舉例來說：

```
$ dmesg | grep atl1
    ...
    atl1 0000:02:00.0: eth0 link is up 100 Mbps full duplex

```

若驅動程式已成功加載可以跳過接下來這段。否則，您會需要知道哪些模組時您的特定型號的裝置需要哪個模組。

### 載入裝置模組

以 Google 搜尋正確的晶片組模組/驅動程式。常見的驅動模組有 Realtek 晶片組網卡的 `8139too` ，或是 SiS 晶片組網卡的 `sis900`。當您知道要使用何種模組了之後，試著[手動將其載入](/index.php/Kernel_modules#Manual_module_handling "Kernel modules")。若您得到了錯誤訊息告訴您找不到該模組，則該驅動可能未包含於 Arch 核心中。您可以在 [AUR](/index.php/AUR "AUR") 中搜尋該模組名稱。

若 udev 未在開機期間檢測與載入正確的模組，請參閱 [Kernel modules#Loading](/index.php/Kernel_modules#Loading "Kernel modules")。

## 網路介面

### 裝置名稱

對於多網路卡的電腦，固定裝置名稱非常重要。許多設定問題都是因為介面卡名稱的改動造成的。

[udev](/index.php/Udev "Udev") 負責命名裝置。Systemd v197 則有[可預測之網路介面名稱](http://www.freedesktop.org/wiki/Software/systemd/PredictableNetworkInterfaceNames)並可自動支配靜態名稱給網路裝置。介面名稱以 `en` （乙太網路）、 `wl` （無線網路） 或是 `ww` （WWAN）作為前置字串並附上一個自動產生的識別名稱，進而產生了類似 `enp0s25` 這樣的名稱。

要禁用這種行為，可以將 `net.ifnames=0` 到您的核心指令列。

**提示：** 您可以執行 `ip link` 或是 `ls /sys/class/net` 以列出所有可用的介面。

**註記:** 當您更改了介面名稱規則後，別忘了更新所有跟網路有關的組態檔案與自定的 systemd unit 檔案以因應該更改。特別是當您啟用了 [netctl 靜態設定檔](/index.php/Netctl#Basic_method "Netctl") ，請執行 `netctl reenable *profile*` 以更新所有產生的服務檔案。

#### 更改裝置名稱

您可以使用 udev-rule 來手動定義裝置名稱。舉例來說：

 `/etc/udev/rules.d/10-network.rules` 
```
SUBSYSTEM=="net", ACTION=="add", ATTR{address}=="aa:bb:cc:dd:ee:ff", NAME="net1"
SUBSYSTEM=="net", ACTION=="add", ATTR{address}=="ff:ee:dd:cc:bb:aa", NAME="net0"

```

請注意這兩點：

*   使用這個指令以取得 MAC 位置：`cat /sys/class/net/*設備名稱*/address`。
*   請確定 udev 規則中使用的是小寫的十六進位數值而不是大寫。

若該網路卡為動態 MAC ，您可以使用 DEVPATH ，例如：

 `/etc/udev/rules.d/10-network.rules` 
```
SUBSYSTEM=="net", DEVPATH=="/devices/platform/wemac.*", NAME="int"

```

**註記:** 當使用了靜態的名稱時，**應該要避免使用類似 "eth*X*" 與 "wlan*X*"** 這樣的名稱，因為這可能會導致核心與 udev 在開機時發生衝突。而剛好相反地，最好使用核心預設不會使用的介面名稱，如 `net0` 、 `net1` 、 `wifi0` 、 `wifi1` 。詳細說明請參閱 [systemd](http://www.freedesktop.org/wiki/Software/systemd/PredictableNetworkInterfaceNames) 文件。

### 設定裝置的 MTU 與佇列長度

您可以手動定義 udev 規則來更改裝置的 MTU 與佇列長度。舉例來說：

 `/etc/udev/rules.d/10-network.rules` 
```
ACTION=="add", SUBSYSTEM=="net", KERNEL=="wl*", ATTR{mtu}="1480", ATTR{tx_queue_len}="2000"

```

### 取得目前的裝置名稱

目前的 NIC 名稱可以通過 sysfs 找到

 `$ ls /sys/class/net` 
```
lo eth0 eth1 firewire0

```

### 啟用與禁用網路介面

您可以使用下列指令來啟用或禁用網路介面：

```
# ip link set eth0 up
# ip link set eth0 down

```

要確認結果，請執行：

 `$ ip link show dev eth0` 
```
2: eth0: <BROADCAST,MULTICAST,PROMISC,UP,LOWER_UP> mtu 1500 qdisc pfifo_fast master br0 state UP mode DEFAULT qlen 1000
...

```

## 組態設定 IP 位址

您有兩個選擇：使用 [DHCP](https://en.wikipedia.org/wiki/Dynamic_Host_Configuration_Protocol "wikipedia:Dynamic Host Configuration Protocol") 指派動態位址，或是使用「靜態」的位址。

### 動態 IP 位址

#### dhcpcd

最簡單的方式就是使用 [dhcpcd](/index.php/Dhcpcd "Dhcpcd")，它包含在 [base](https://www.archlinux.org/groups/x86_64/base/) 群組中。無論是使用提供服務檔案 `dhcpcd@.service` ，以參數方式傳入介面卡名稱，或是手動通過 `dhcpcd *interface*` 將其執行。

### 靜態 IP 位址

您可能因為各種原因而希望在您的網路中指派靜態 IP 位址，例如靜態的位址可以獲得一定程度的可預測性，或是您沒有可用的 DHCP 伺服器。

**註記:** 若您通過 Windows 機器來共享您的網路而不是使用路由器，請確保兩台電腦皆使用了靜態 IP 位址以避免區域網路問題。

您需要：

*   靜態 IP 位址
*   [子網路遮罩](https://en.wikipedia.org/wiki/Subnetwork "wikipedia:Subnetwork")
*   [廣播位址](https://en.wikipedia.org/wiki/Broadcast_address "wikipedia:Broadcast address")
*   [預設閘道器](https://en.wikipedia.org/wiki/Default_gateway "wikipedia:Default gateway")的 IP 位址

若您處在內部網路中，使用 192.168.*.* 這樣的 IP 位址較為安全，搭配其的子網路遮罩 255.255.255.0 ，廣播位址為 192.168.*.255 。而閘道通常是 192.168.*.1 或是 192.168.*.254 。

**Tip:** You may need to manually set the DNS servers, see [resolv.conf](/index.php/Resolv.conf "Resolv.conf") for details.

#### 手動指派

您可於控制台中指派一靜態 IP 位址：

```
# ip addr add *IP位址*/*子網路遮罩* broadcast *廣播* dev *介面*

```

舉例來說：

```
# ip addr add 192.168.1.2/24 broadcast 192.168.1.255 dev eth0

```

**註記:** 子網路遮罩使用了 [CIDR 表示法](https://en.wikipedia.org/wiki/CIDR_notation "wikipedia:CIDR notation")（CIDR，Classless Inter-Domain Routing，無類別網路間路由）。

詳情請參閱 `man ip` 。

以類似下列的方法加上您的 IP 位址：

```
# ip route add default via *預設閘道IP位址*

```

舉例來說：

```
# ip route add default via 192.168.1.1

```

若您得到了 "No such process" 這樣的錯誤訊息，這代表您必須以 root 執行 `ip link set dev eth0 up` 。

#### 永久於啟動時通過 systemd 進行組態設定與 udev 規則

首先先為 [systemd](/index.php/Systemd "Systemd") 服務建立一個組態設定檔，請以網路介面卡名稱取代下列的 `*interface*`：

 `/etc/conf.d/network@*interface*` 
```
address=192.168.0.15
netmask=24
broadcast=192.168.0.255
gateway=192.168.0.1

```

建立 systemd unit 檔案：

 `/etc/systemd/system/network@.service` 
```
[Unit]
Description=Network connectivity (%i)
Wants=network.target
Before=network.target
BindsTo=sys-subsystem-net-devices-%i.device
After=sys-subsystem-net-devices-%i.device

[Service]
Type=oneshot
RemainAfterExit=yes
EnvironmentFile=/etc/conf.d/network@%i

ExecStart=/usr/bin/ip link set dev %i up
ExecStart=/usr/bin/ip addr add ${address}/${netmask} broadcast ${broadcast} dev %i
ExecStart=/usr/bin/sh -c 'test -n ${gateway} && /usr/bin/ip route add default via ${gateway}'

ExecStop=/usr/bin/ip addr flush dev %i
ExecStop=/usr/bin/ip link set dev %i down

[Install]
WantedBy=multi-user.target

```

啟用該 unit 並將其啟動，傳入介面名稱：

```
# systemctl enable network@*介面名稱*.service
# systemctl start network@*介面名稱*.service

```

#### 計算位址

您可以使用 [ipcalc](https://www.archlinux.org/packages/?name=ipcalc) 提供的 `ipcalc` 來計算 IP 廣播、網域、子網路遮罩與主機範圍等進階設定舉例來說，我使用了位於防火牆後的乙太網路來連線 Windows 機器至 Arch。為了安全性與網路組織，我將他們放置於各自獨立的網路，接著組態設定子網路遮罩與廣播位址，如此一來網路中就只有兩台機器。為了找出子網路遮罩跟廣播位址，我使用了 ipcalc ，提供其 Arch firewire nic 的 IP 位址 10.66.66.1 ，並指定 ipcalc 要建立一個只有兩台主機的網路。

 `$ ipcalc -nb 10.66.66.1 -s 1` 
```
Address:   10.66.66.1

Netmask:   255.255.255.252 = 30
Network:   10.66.66.0/30
HostMin:   10.66.66.1
HostMax:   10.66.66.2
Broadcast: 10.66.66.3
Hosts/Net: 2                     Class A, Private Internet

```

### systemd-networkd

若 [systemd](/index.php/Systemd "Systemd") 的版本為 209 以上（含），則可使用 [systemd-networkd](/index.php/Systemd-networkd "Systemd-networkd") 來管理網路，可輕鬆地代替在 Containers 與虛擬機中設定網路。並可同時管理動態與靜態 IP 位址。

## 載入組態設定

要測試您的設定，您可以重新啟動電腦或是重新載入相關的 systemd 服務。然後嘗試 Ping 您的閘道器、DNS 伺服器、ISP 業者與其他的網際網路站台，用這樣的方式便能檢測哪裡出了問題，舉例來說：

```
$ ping -c 3 www.google.com

```

## 附加設定

### 筆記型電腦之 ifplugd

**提示：** [dhcpcd](/index.php/Dhcpcd "Dhcpcd") 提供了開箱即用的相同功能。

[官方軟體套件庫](/index.php/Official_repositories_(%E6%AD%A3%E9%AB%94%E4%B8%AD%E6%96%87) "Official repositories (正體中文)")中的 [ifplugd](https://www.archlinux.org/packages/?name=ifplugd) 為一個當網路線插入後自動組態乙太設備；網路線拔除後自動取消組態的 Daemon 。 這對於搭載內建網路介面卡的筆記型電腦特別有用，因為其只會在網路線真正連上後才會對介面進行組態。另一個會用到的情況為，當您需要重新啟動網路，但您並不想重開及或在 Shell 中進行設定。

預設情況下，其會對 `eth0` 裝置進行設定使其運作。這與其他設定類似延遲之類的設定能在 `/etc/ifplugd/ifplugd.conf` 中進行設定。

**註記:** [Netctl](/index.php/Netctl "Netctl") 軟體包包含了 `netctl-ifplugd@.service`，否則您可以使用來自 [ifplugd](https://www.archlinux.org/packages/?name=ifplugd) 軟體包的 `ifplugd@.service` 。例如這樣使用：`systemctl enable ifplugd@eth0.service`。

### Bonding 或 LAG

請參閱 [netctl#Bonding](/index.php/Netctl#Bonding "Netctl") 。

### IP 別名

IP 別名為讓同一個網路介面有多個 IP 位址。如此一來，單個節點的網路就能有多個網路連線，進而實現不同的作用。經典的使用方法為網頁與 FTP 伺服器的虛擬主機，或是重組伺服器而無需更新任何其他的機器（對於名稱伺服器來說特別有用）。

#### 範例

您將需要來自[官方軟體套件庫](/index.php/Official_repositories_(%E6%AD%A3%E9%AB%94%E4%B8%AD%E6%96%87) "Official repositories (正體中文)")的 [netctl](https://www.archlinux.org/packages/?name=netctl) 。

準備組態設定檔：

 `/etc/netctl/mynetwork` 
```
Connection='ethernet'
Description='Five different addresses on the same NIC.'
Interface='eth0'
IP='static'
Address=('192.168.1.10' '192.168.178.11' '192.168.1.12' '192.168.1.13' '192.168.1.14' '192.168.1.15')
Gateway='192.168.1.1'
DNS=('192.168.1.1')

```

接著只需要將其執行即可：

```
$ netctl start mynetwork

```

### 更改 MAC/硬體 位址

請參閱 [MAC address spoofing](/index.php/MAC_address_spoofing "MAC address spoofing") 。

### 網路共享

請參閱 [Internet sharing](/index.php/Internet_sharing "Internet sharing") 。

### 路由組態設定

請參閱 [Router](/index.php/Router "Router") 。

### 區域網路主機名稱解析

先決條件為[設定主機名稱](#.E8.A8.AD.E5.AE.9A.E4.B8.BB.E6.A9.9F.E5.90.8D.E7.A8.B1)之後，主機名稱可在本機系統上解析：

 `$ ping hostname` 
```
PING hostname (192.168.1.2) 56(84) bytes of data.
64 bytes from hostname (192.168.1.2): icmp_seq=1 ttl=64 time=0.043 ms
```

要以其他機器的名稱來解析主機，需要手動設定各自的 `/etc/hosts` 檔案或是廣播/解析名稱的服務。

過度設定 DNS 伺服器，如 [BIND](/index.php/BIND "BIND") 、 [Unbound](/index.php/Unbound "Unbound") ，手動編輯 `/etc/hosts` 過於繁瑣，或是您希望對於動態地將主機離開、加入網路有更大的靈活性，您可以在您的區域網路中使用 Zero-configuration networking 來進行主機名稱解析。這裡有兩個可用選擇：

*   [Samba](/index.php/Samba "Samba") 提供了通過微軟 **NetBIOS** 的主機名稱解析。其只需要安裝 [samba](https://www.archlinux.org/packages/?name=samba) 並啟用 `nmbd.service` 服務。執行 Windows 、OS X 或執行了 `nmbd` 的 Linux ，將能夠找到您的機器。

*   [Avahi](/index.php/Avahi "Avahi") 提供通過 **zeroconf** 的主機名稱解析，也稱作 Avahi 或 Boujour 。它比 Samba 還需要稍微複雜一點的設定：詳情請參考 [Avahi#Hostname resolution](/index.php/Avahi#Hostname_resolution "Avahi")。執行 OS X 或執行了 Avahi daemon 的 Linux ，將能夠找到您的機器。Windows 並無內建 Avahi 用戶端或 Daemon 。

### 雜亂模式

Toggling [promiscuous mode](https://en.wikipedia.org/wiki/Promiscuous_mode "wikipedia:Promiscuous mode") will make a (wireless) NIC forward all traffic it receives to the OS for further processing. This is opposite to "normal mode" where a NIC will drop frames it is not intended to receive. It is most often used for advanced network troubleshooting and [packet sniffing](https://en.wikipedia.org/wiki/Packet_sniffing "wikipedia:Packet sniffing").

 `/etc/systemd/system/promiscuous@.service` 
```
[Unit]
Description=Set %i interface in promiscuous mode
After=network.target

[Service]
Type=oneshot
ExecStart=/usr/bin/ip link set dev %i promisc on
RemainAfterExit=yes

[Install]
WantedBy=multi-user.target

```

若您想在介面卡 `eth0` 中啟用雜亂模式，請執行：

```
# systemctl enable promiscuous@eth0.service

```

## 診斷

### Swapping computers on the cable modem

Some cable ISPs (videotron for example) have the cable modem configured to recognize only one client PC, by the MAC address of its network interface. Once the cable modem has learned the MAC address of the first PC or equipment that talks to it, it will not respond to another MAC address in any way. Thus if you swap one PC for another (or for a router), the new PC (or router) will not work with the cable modem, because the new PC (or router) has a MAC address different from the old one. To reset the cable modem so that it will recognise the new PC, you must power the cable modem off and on again. Once the cable modem has rebooted and gone fully online again (indicator lights settled down), reboot the newly connected PC so that it makes a DHCP request, or manually make it request a new DHCP lease.

If this method does not work, you will need to clone the MAC address of the original machine. See also [Change MAC/hardware address](/index.php/Configuring_Network#Change_MAC.2Fhardware_address "Configuring Network").

### The TCP window scaling problem

TCP packets contain a "window" value in their headers indicating how much data the other host may send in return. This value is represented with only 16 bits, hence the window size is at most 64Kb. TCP packets are cached for a while (they have to be reordered), and as memory is (or used to be) limited, one host could easily run out of it.

Back in 1992, as more and more memory became available, [RFC 1323](http://www.faqs.org/rfcs/rfc1323.html) was written to improve the situation: Window Scaling. The "window" value, provided in all packets, will be modified by a Scale Factor defined once, at the very beginning of the connection.

That 8-bit Scale Factor allows the Window to be up to 32 times higher than the initial 64Kb.

It appears that some broken routers and firewalls on the Internet are rewriting the Scale Factor to 0 which causes misunderstandings between hosts.

The Linux kernel 2.6.17 introduced a new calculation scheme generating higher Scale Factors, virtually making the aftermaths of the broken routers and firewalls more visible.

The resulting connection is at best very slow or broken.

#### How to diagnose the problem

First of all, let's make it clear: this problem is odd. In some cases, you will not be able to use TCP connections (HTTP, FTP, ...) at all and in others, you will be able to communicate with some hosts (very few).

When you have this problem, the `dmesg`'s output is OK, logs are clean and `ip addr` will report normal status... and actually everything appears normal.

If you cannot browse any website, but you can ping some random hosts, chances are great that you're experiencing this problem: ping uses ICMP and is not affected by TCP problems.

You can try to use Wireshark. You might see successful UDP and ICMP communications but unsuccessful TCP communications (only to foreign hosts).

#### How to fix it (The bad way)

To fix it the bad way, you can change the tcp_rmem value, on which Scale Factor calculation is based. Although it should work for most hosts, it is not guaranteed, especially for very distant ones.

```
# echo "4096 87380 174760" > /proc/sys/net/ipv4/tcp_rmem

```

#### How to fix it (The good way)

Simply disable Window Scaling. Since Window Scaling is a nice TCP feature, it may be uncomfortable to disable it, especially if you cannot fix the broken router. There are several ways to disable Window Scaling, and it seems that the most bulletproof way (which will work with most kernels) is to add the following line to `/etc/sysctl.d/99-disable_window_scaling.conf` (see also [sysctl](/index.php/Sysctl "Sysctl"))

```
net.ipv4.tcp_window_scaling = 0

```

#### How to fix it (The best way)

This problem is caused by broken routers/firewalls, so let's change them. Some users have reported that the broken router was their very own DSL router.

#### More about it

This section is based on the LWN article [TCP window scaling and broken routers](http://lwn.net/Articles/92727/) and a Kernel Trap article: [Window Scaling on the Internet](http://kerneltrap.org/node/6723).

There are also several relevant threads on the LKML.

### Realtek no link / WOL problem

Users with Realtek 8168 8169 8101 8111(C) based NICs (cards / and on-board) may notice a problem where the NIC seems to be disabled on boot and has no Link light. This can usually be found on a dual boot system where Windows is also installed. It seems that using the offical Realtek drivers (dated anything after May 2007) under Windows is the cause. These newer drivers disable the Wake-On-LAN feature by disabling the NIC at Windows shutdown time, where it will remain disabled until the next time Windows boots. You will be able to notice if this problem is affecting you if the Link light remains off until Windows boots up; during Windows shutdown the Link light will switch off. Normal operation should be that the link light is always on as long as the system is on, even during POST. This problem will also affect other operative systems without newer drivers (eg. Live CDs). Here are a few fixes for this problem:

#### Method 1 - Enable the NIC directly in Linux

Get the ethernet NIC name from the output of

```
$ ip a

```

Bring up the device as root using the NIC name:

```
# ip link set dev <NIC_name> up

```

For ex, if <NIC_name> is enp7s0

```
# ip link set dev enp7s0 up

```

If it worked and the card is powered on, you should see `state UP` for the given interface in the output of `ip link`.

#### Method 2 - Rollback/change Windows driver

You can roll back your Windows NIC driver to the Microsoft provided one (if available), or roll back/install an official Realtek driver pre-dating May 2007 (may be on the CD that came with your hardware).

#### Method 3 - Enable WOL in Windows driver

Probably the best and the fastest fix is to change this setting in the Windows driver. This way it should be fixed system-wide and not only under Arch (eg. live CDs, other operative systems). In Windows, under Device Manager, find your Realtek network adapter and double-click it. Under the Advanced tab, change "Wake-on-LAN after shutdown" to Enable.

```
In Windows XP (example)
Right click my computer
--> Hardware tab
  --> Device Manager
    --> Network Adapters
      --> "double click" Realtek ...
        --> Advanced tab
          --> Wake-On-Lan After Shutdown
            --> Enable

```

**Note:** Newer Realtek Windows drivers (tested with *Realtek 8111/8169 LAN Driver v5.708.1030.2008*, dated 2009/01/22, available from GIGABYTE) may refer to this option slightly differently, like *Shutdown Wake-On-LAN --> Enable*. It seems that switching it to `Disable` has no effect (you will notice the Link light still turns off upon Windows shutdown). One rather dirty workaround is to boot to Windows and just reset the system (perform an ungraceful restart/shutdown) thus not giving the Windows driver a chance to disable LAN. The Link light will remain on and the LAN adapter will remain accessible after POST - that is until you boot back to Windows and shut it down properly again.

#### Method 4 - Newer Realtek Linux driver

Any newer driver for these Realtek cards can be found for Linux on the realtek site. (untested but believed to also solve the problem).

#### Method 5 - Enable *LAN Boot ROM* in BIOS/CMOS

It appears that setting *Integrated Peripherals --> Onboard LAN Boot ROM --> Enabled* in BIOS/CMOS reactivates the Realtek LAN chip on system boot-up, despite the Windows driver disabling it on OS shutdown.

**Note:** This was tested successfully multiple times with GIGABYTE system board GA-G31M-ES2L with BIOS version F8 released on 2009/02/05\. YMMV.

### No interface with Atheros chipsets

Users of some Atheros ethernet chips are reporting it does not work out-of-the-box (with installation media of February 2014). The working solution for this is to install the package [backports-patched](https://aur.archlinux.org/packages/backports-patched/) from AUR.

### Broadcom BCM57780

This Broadcom chipset sometimes does not behave well unless you specify the order of the modules to be loaded. The modules are `broadcom` and `tg3`, the former needing to be loaded first.

These steps should help if your computer has this chipset:

```
$ lspci | grep Ethernet
02:00.0 Ethernet controller: Broadcom Corporation NetLink BCM57780 Gigabit Ethernet PCIe (rev 01)

```

If your wired networking is not functioning in some way or another, try unplugging your cable then doing the following (as root):

```
# modprobe -r tg3
# modprobe broadcom
# modprobe tg3

```

Now plug you network cable in. If this solves your problems you can make this permanent by adding `broadcom` and `tg3` (in this order) to the `MODULES` array in `/etc/mkinitcpio.conf`:

```
MODULES=".. broadcom tg3 .."

```

Then rebuild the initramfs:

```
# mkinitcpio -p linux

```

**Note:** These methods may work for other chipsets, such as BCM57760.