## Contents

*   [1 安装](#.E5.AE.89.E8.A3.85)
*   [2 进入 /etc/west-chamber 导入默认的 ipset](#.E8.BF.9B.E5.85.A5_.2Fetc.2Fwest-chamber_.E5.AF.BC.E5.85.A5.E9.BB.98.E8.AE.A4.E7.9A.84_ipset)
*   [3 使用 iptables 设定过滤规则](#.E4.BD.BF.E7.94.A8_iptables_.E8.AE.BE.E5.AE.9A.E8.BF.87.E6.BB.A4.E8.A7.84.E5.88.99)
*   [4 修改 dns](#.E4.BF.AE.E6.94.B9_dns)
*   [5 重启网络](#.E9.87.8D.E5.90.AF.E7.BD.91.E7.BB.9C)
*   [6 自动化](#.E8.87.AA.E5.8A.A8.E5.8C.96)
    *   [6.1 导出规则](#.E5.AF.BC.E5.87.BA.E8.A7.84.E5.88.99)
    *   [6.2 编写 bash 脚本](#.E7.BC.96.E5.86.99_bash_.E8.84.9A.E6.9C.AC)
*   [7 测试](#.E6.B5.8B.E8.AF.95)
*   [8 参考文档](#.E5.8F.82.E8.80.83.E6.96.87.E6.A1.A3)

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
3.[https://wiki.archlinux.org/index.php/Resolv.conf](https://wiki.archlinux.org/index.php/Resolv.conf)
4.[http://blog.linjunpop.com/archives/2010/install-west-chamber-on-archlinux-step-by-step/](http://blog.linjunpop.com/archives/2010/install-west-chamber-on-archlinux-step-by-step/)

```