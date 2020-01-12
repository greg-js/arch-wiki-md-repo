<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 安装](#安装)
*   [2 进入 /etc/west-chamber 导入默认的 ipset](#进入_/etc/west-chamber_导入默认的_ipset)
*   [3 使用 iptables 设定过滤规则](#使用_iptables_设定过滤规则)
*   [4 修改 dns](#修改_dns)
*   [5 重启网络](#重启网络)
*   [6 自动化](#自动化)
    *   [6.1 导出规则](#导出规则)
    *   [6.2 编写 bash 脚本](#编写_bash_脚本)
*   [7 测试](#测试)
*   [8 参考文档](#参考文档)

## 安装

```
yaourt -S west-chamber

```

## 进入 /etc/west-chamber 导入默认的 ipset

```
sudo ipset -R < CHINA
sudo ipset -R < GOOGLE
sudo ipset -R < NOCLIP
sudo ipset -R < YOUTUBE

```

## 使用 iptables 设定过滤规则

```
sudo iptables -A INPUT -p tcp --sport 80 --tcp-flags FIN,SYN,RST,ACK SYN,ACK -m state --state ESTABLISHED -m set --match-set NOCLIP src -j ZHANG -m comment --comment "client-side connection obfuscation"
sudo iptables -A INPUT -p tcp --dport 80 --tcp-flags FIN,SYN,RST,ACK SYN -m state --state NEW -j CUI -m set --match-set CHINA src -m comment --comment "server-side connection obfuscation"
sudo iptables -A INPUT -p tcp --sport 80 -m state --state ESTABLISHED -m gfw -j DROP --log-level info --log-prefix "gfw: " -m comment --comment "log gfw tcp resets"
sudo iptables -A INPUT -p udp --sport 53 -m state --state ESTABLISHED -m gfw -j DROP -m comment --comment "drop gfw dns hijacks"

```

## 修改 dns

编辑 /etc/resolv.conf.head (默认无此文件) 加入以下内容或其他的干净纯洁洁白无污染的 DNS

```
# openDNS (在我这里使用后解析相当慢)
208.67.222.222
208.67.220.220

```

建议使用 namebench ([http://code.google.com/p/namebench/](http://code.google.com/p/namebench/)) 选择最佳的 dns

```
yaourt -S namebench

```

## 重启网络

```
# ip link set dev eth0 down
# ip link set dev eth0 up

```

## 自动化

### 导出规则

```
sudo ipset -S > ipset.rules
sudo iptables-save > iptables.rules
sudo mv ipset.rules iptables.rules /etc

```

### 编写 bash 脚本

```
#!/bin/bash
ifconfig eth0 down
ipset -R < /etc/ipset.rules
iptables-restore < /etc/iptables.rules
ifconfig eth0 up

```

## 测试

测试 Google SpreadSheet 正常，BlogSpot正常 , PicasaWeb 正常，bit.ly 正常 ，Youtube 无法访问，Facebook 无法访问

## 参考文档

```
1.[http://blog.xiaogaozi.org/2010/03/ubuntu.htm](http://blog.xiaogaozi.org/2010/03/ubuntu.htm)
2.[http://code.google.com/p/scholarzhang/wiki/USAGE](http://code.google.com/p/scholarzhang/wiki/USAGE)
3.[Resolv.conf](/index.php/Resolv.conf "Resolv.conf")
4.[http://blog.linjunpop.com/archives/2010/install-west-chamber-on-archlinux-step-by-step/](http://blog.linjunpop.com/archives/2010/install-west-chamber-on-archlinux-step-by-step/)

```