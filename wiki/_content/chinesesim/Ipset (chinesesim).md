[ipset](http://ipset.netfilter.org/)是 Linux [防火墙](/index.php?title=%E9%98%B2%E7%81%AB%E5%A2%99&action=edit&redlink=1 "防火墙 (page does not exist)")[iptables](/index.php/Iptables "Iptables")的一个伴随工具。 除了其他众多功能，它允许你建立规则来轻松愉快地屏蔽一组IP地址。

## Contents

*   [1 安装](#.E5.AE.89.E8.A3.85)
*   [2 配置](#.E9.85.8D.E7.BD.AE)
    *   [2.1 屏蔽一组地址](#.E5.B1.8F.E8.94.BD.E4.B8.80.E7.BB.84.E5.9C.B0.E5.9D.80)
    *   [2.2 使ipset持久化](#.E4.BD.BFipset.E6.8C.81.E4.B9.85.E5.8C.96)
    *   [2.3 使用PeerGuardian和其它列表屏蔽](#.E4.BD.BF.E7.94.A8PeerGuardian.E5.92.8C.E5.85.B6.E5.AE.83.E5.88.97.E8.A1.A8.E5.B1.8F.E8.94.BD)
*   [3 其他命令](#.E5.85.B6.E4.BB.96.E5.91.BD.E4.BB.A4)
*   [4 优化](#.E4.BC.98.E5.8C.96)

## 安装

从[官方源](/index.php/%E5%AE%98%E6%96%B9%E6%BA%90 "官方源")[安装](/index.php/%E5%AE%89%E8%A3%85 "安装") [ipset](https://www.archlinux.org/packages/?name=ipset)。

## 配置

### 屏蔽一组地址

先创建一个新的网络地址的“集合”。下面的命令创建了一个新的叫做“myset”的“net”网络地址的“hash”集合。 Start by creating a new "set" of network addresses. This creates a new "hash" set of "net" network addresses named "myset".

```
# ipset create myset hash:net

```

把你希望屏蔽的IP地址添加到集合中。 Add any IP address that you'd like to block to the set.

```
# ipset add myset 14.144.0.0/12
# ipset add myset 27.8.0.0/13
# ipset add myset 58.16.0.0/15

```

最后，配置[iptables](/index.php/Iptables "Iptables")来屏蔽这个集合中的所有地址。这个命令将会向“INPUT”链顶端添加一个规则来从ipset中“-m”匹配名为“myset”的集合，当匹配到的包是一个“src”包时，“DROP”屏蔽掉它。 Finally, configure [iptables](/index.php/Iptables "Iptables") to block any address in that set. This command will add a rule to the top of the "INPUT" chain to "-m" match the set named "myset" from ipset (--match-set) when it's a "src" packet and "DROP", or block, it.

```
# iptables -I INPUT -m set --match-set myset src -j DROP

```

### 使ipset持久化

你创建的ipse存在于内存中，重启后将会消失。要使ipset持久化，你要这样做：

首先把ipset保存到/etc/ipset.conf:

```
# ipset save > /etc/ipset.conf

```

然后[激活](/index.php?title=%E6%BF%80%E6%B4%BB&action=edit&redlink=1 "激活 (page does not exist)") `ipset.service`,这个服务与用于恢复[iptables rules](/index.php/Iptables#Configuration_and_usage "Iptables")的`iptables.service`相似。

### 使用PeerGuardian和其它列表屏蔽

maeyanie.com所作的[pg2ipset-git](https://aur.archlinux.org/packages/pg2ipset-git/)与[ipset-update.sh](https://github.com/ilikenwf/pg2ipset/blob/master/ipset-update.sh) 脚本配合可以用cron来自动更新多个屏蔽列表。 当前实现了按默认国家屏蔽，tor退出节点屏蔽，和来自Bluetack的pg2列表屏蔽。

## 其他命令

查看集合。

```
# ipset list

```

删除名为“myset”的集合。

```
# ipset destroy myset

```

删除所有集合。

```
# ipset destroy

```

更多信息请参考ipset的man手册页。

## 优化

[iprange](https://aur.archlinux.org/packages/iprange/)工具可以通过合并相邻范围或消除重复范围来帮助减少ipset.conf中的项目。 在表的大小很大时，这有助于改善路由/防火墙的性能。这个工具也可以把一个主机名的列表转换成IP列表。