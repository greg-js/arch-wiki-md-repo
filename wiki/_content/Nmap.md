# Nmap

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

[![Tango-view-fullscreen.png](/images/3/38/Tango-view-fullscreen.png)](/index.php/File:Tango-view-fullscreen.png)

[![Tango-view-fullscreen.png](/images/3/38/Tango-view-fullscreen.png)](/index.php/File:Tango-view-fullscreen.png)

**This article or section needs expansion.**

**Reason:** DNS resolution; Ping scanning; Default options; Idle scan; FTP bounce; Timing options; (Discuss in [Talk:Nmap#](https://wiki.archlinux.org/index.php/Talk:Nmap))

From the [official website](http://nmap.org/):

_Nmap (“Network Mapper”) is an open source tool for network exploration and security auditing. It was designed to rapidly scan large networks, although it works fine against single hosts. Nmap uses raw IP packets in novel ways to determine what hosts are available on the network, what services (application name and version) those hosts are offering, what operating systems (and OS versions) they are running, what type of packet filters/firewalls are in use, and dozens of other characteristics. While Nmap is commonly used for security audits, many systems and network administrators find it useful for routine tasks such as network inventory, managing service upgrade schedules, and monitoring host or service uptime._

**Warning:** Invoking network scan techniques on systems, hosts or network ranges other than those under the own responsibility is illegal in quite a few jurisdictions. Double-check you scan your own hosts only (see [#List scan](#List_scan)), or re-confirm the approval of the respective owner, before executing a scan!

## Contents

*   [1 Installation](#Installation)
*   [2 Usage](#Usage)
    *   [2.1 Specifying the target](#Specifying_the_target)
        *   [2.1.1 Specifying multiple targets](#Specifying_multiple_targets)
    *   [2.2 List scan](#List_scan)
    *   [2.3 Default options](#Default_options)
*   [3 Ping scan](#Ping_scan)
    *   [3.1 Ping scan types](#Ping_scan_types)
*   [4 Port scan](#Port_scan)
    *   [4.1 Scan types](#Scan_types)
*   [5 Anti-scanning techniques](#Anti-scanning_techniques)
    *   [5.1 iptables PSD module](#iptables_PSD_module)
    *   [5.2 Avoiding detection](#Avoiding_detection)
*   [6 Tips and Tricks](#Tips_and_Tricks)
    *   [6.1 Limiting scan speed](#Limiting_scan_speed)
    *   [6.2 Specify targets input from a list file](#Specify_targets_input_from_a_list_file)
    *   [6.3 Specify targets to exclude from scan](#Specify_targets_to_exclude_from_scan)
    *   [6.4 Spoofing](#Spoofing)
    *   [6.5 Speeding up the scan](#Speeding_up_the_scan)
    *   [6.6 Scan port number 0](#Scan_port_number_0)
    *   [6.7 File output formats](#File_output_formats)
*   [7 See also](#See_also)

## Installation

[Install](/index.php/Install "Install") [nmap](https://www.archlinux.org/packages/?name=nmap) from [official repositories](/index.php/Official_repositories "Official repositories").

Nmap package comes with a GUI called `zenmap`, but this article will cover only command-line usage.

## Usage

### Specifying the target

**Tip:** To print every packet that Nmap sends and receives, use the `--packet-trace` option.

There are a number of ways to tell Nmap the list of IP addresses to scan. The simplest form is to just pass the address or domain name:

```
$ nmap scanme.nmap.org
$ nmap 74.207.244.221

```

#### Specifying multiple targets

Using [CIDR](https://en.wikipedia.org/wiki/CIDR "wikipedia:CIDR") notation, for example to scan all 256 addresses beginning with `10.1.1`:

```
$ nmap 10.1.1.0/24

```

**Note:** The ending `0` in the above example does not have an effect: `nmap 10.1.1.0/24` and for example `nmap 10.1.1.134/24` commands are the same.

Using the dash, for example to scan `10.1.50.1`, `10.1.51.1` and `10.1.52.1`:

```
$ nmap 10.1.50-52.1

```

Using commas (does what you expect):

```
$ nmap 10.1.50,51,52,57,59.1

```

All combined:

```
$ nmap 10.1,2.50-52.1/30 10.1.1.1 10.1.1.2

```

### List scan

The list scan option (`-sL`) is useful for making sure that correct addresses are specified before doing the real scan:

```
$ nmap -sL 10.1,2.50-52.1/30 10.1.1.1 10.1.1.2

```

List scan simply prints the specified addresses without sending a single packet to the target.

### Default options

If you specify only an IP address or damain name and no other options:

```
$ nmap 74.207.244.221

```

Nmap will do the following:

1.  The IP address is reverse-DNS resolved to domain name, or vice-versa in case a domain name is specified (to disable, pass `-n`)
2.  Ping scanning using TCP ACK:80 and ICMP. This is equivalent to `-PA -PE` (to disable, pass `-PN`)
3.  Scans the host(s)'s top 1000 most popular ports. When running as root, SYN stealth scan is used. When running as user, connect scan is used.

## Ping scan

Ping scanning (host discovery) is a technique for determining whether the specified computers are up and running. Nmap performs ping scan by default before port scan to avoid wasting time on hosts that are not even connected. To instruct Nmap to **only** perform ping scan:

```
$ nmap -sP 10.1.1.1/8

```

This will cause Nmap to ping every one of the specified addresses and then report the list of hosts which did respond to the ping.

Nmap uses different kinds of ping packets when run with user or root privileges and when scanning the same or different subnets:

<table class="wikitable">

<tbody>

<tr>

<th>External IP</th>

<th>Local IP</th>

</tr>

<tr>

<th>User privileges</th>

<td>TCP SYN at ports 80 & 443</td>

<td>TCP SYN at ports 80 & 443 and ARP</td>

</tr>

<tr>

<th>Root privileges</th>

<td>TCP SYN at ports 80 & 443 and IGMP</td>

<td>ARP</td>

</tr>

</tbody>

</table>

### Ping scan types

<table class="wikitable">

<tbody>

<tr>

<th>Option</th>

<th>Ping scan type</th>

</tr>

<tr>

<td>`-Pn`</td>

<td>Disable ping scan entirely</td>

</tr>

<tr>

<td>`-PS`</td>

<td>TCP **S**YN (default at port 80)</td>

</tr>

<tr>

<td>`-PA`</td>

<td>TCP **A**CK (default at port 80)</td>

</tr>

<tr>

<td>`-PU`</td>

<td>**U**DP</td>

</tr>

<tr>

<td>`-PY`</td>

<td>SCTP INIT</td>

</tr>

<tr>

<td>`-PE`</td>

<td>ICMP **E**cho</td>

</tr>

<tr>

<td>`-PP`</td>

<td>ICMP timestam**p**</td>

</tr>

<tr>

<td>`-PM`</td>

<td>ICMP address **m**ask</td>

</tr>

<tr>

<td>`-PO`</td>

<td>**O**ther IP protocol</td>

</tr>

<tr>

<td>`-PR`</td>

<td>[ARP](https://en.wikipedia.org/wiki/Address_Resolution_Protocol "wikipedia:Address Resolution Protocol") scan</td>

</tr>

</tbody>

</table>

`-Pn` is useful when the machine is heavily firewalled, TCP 80 and 443 ports and IGMP requests are blocked, but the IP address might still have a machine listening on other less common ports.

## Port scan

There are 3 main states a port can be in:

*   `open` - there is a program listening and responding to requests on this port
*   `closed` - the host replys with an "error: no program listening on this port" reply to requests to this port
*   `filtered` - the host doesn't reply at all. This can be due to restrictive firewall rules, which "drop" a packet without sending a reply

In addition to these there are 3 more states that Nmap can classify a port. These are used when Nmap cannot reliably determine the state but suspects two of the three possible states:

*   `open|closed` (`unfiltered`) - the port is either open or closed
*   `closed|filtered` - the port is either closed or filtered
*   `open|filtered` - the port is either open or filtered

By default Nmap scans the 1000 most popular ports found in `/etc/nmap/nmap-services`. To specify a different number of common ports:

```
$ nmap --top-ports 10.1.1.1

```

To specify custom port numbers, use `-p`:

```
$ nmap -p -25,135-137 10.1.1.1

```

Dashes and commas work just like in [#Specifying the target](#Specifying_the_target). In addition, it is possible to specify all ports before/after given one by skipping the starting/ending port when using a dash. For example to scan all possible 65535 ports (except [port number 0](#Scan_port_number_0)):

```
$ nmap -p -

```

### Scan types

<table class="wikitable">

<tbody>

<tr>

<th>Option</th>

<th>Port scan type</th>

</tr>

<tr>

<td>`-sP`</td>

<td>[Ping scan](#Ping_scan) only</td>

</tr>

<tr>

<td>`-sS`</td>

<td>TCP SYN (stealth) (Default as root)</td>

</tr>

<tr>

<td>`-sT`</td>

<td>TCP connect (Default as user)</td>

</tr>

<tr>

<td>`-sA`</td>

<td>TCP ACK</td>

</tr>

<tr>

<td>`-sF`</td>

<td>TCP FIN</td>

</tr>

<tr>

<td>`-sX`</td>

<td>TCP FIN, SYN, ACK</td>

</tr>

<tr>

<td>`-sW`</td>

<td>TCP window</td>

</tr>

<tr>

<td>`-sM`</td>

<td>TCP Miamon</td>

</tr>

<tr>

<td>`-sU`</td>

<td>UDP scan</td>

</tr>

<tr>

<td>`-sI`</td>

<td>Idle scan</td>

</tr>

<tr>

<td>`-b`</td>

<td>FTP bounce scan</td>

</tr>

<tr>

<td>`-sO`</td>

<td>Other IP protocol</td>

</tr>

</tbody>

</table>

## Anti-scanning techniques

### iptables PSD module

[PSD](http://sourceforge.net/p/xtables-addons/xtables-addons/ci/master/tree/extensions/xt_psd.c) is an extension module of [iptables](/index.php/Iptables "Iptables"). It is used on some linux-based commercial routers as well.

It has 4 parameters:

*   `--psd-weight-threshold _threshold_`, default value: `21`

Total weight of the latest TCP/UDP packets with different destination ports coming from the same host to be treated as port scan sequence.

*   `--psd-delay-threshold _delay_`, default value: `300` (3 seconds)

Delay (in hundredths of second) for the packets with different destination ports coming from the same host to be treated as possible port scan subsequence.

*   `--psd-lo-ports-weight _weight_`, default value: `3`

Weight of the packet with privileged (<=1024) destination port.

*   `--psd-hi-ports-weight _weight_`, default value: `1`

Weight of the packet with non-priviliged (>1024) destination port.

The principle behind PSD is simple. If requests from a single IP have gained a value more than _threshold_ in _delay_ seconds, then the IP is classified as a port scanner. In a math expression:

```
_lo_ports_weight_ * **REQUESTS_LOW** + _hi_ports_weight_ * **REQUESTS_HIGH** >= _threshold_

```

where

```
**REQUESTS_LOW** = number of requests to priviliged (0 to 1024) ports within last _delay_ seconds
**REQUESTS_HI** = number of requests to privileged (1024 to 65535) ports within last _delay_ seconds

```

Here are some examples:

*   With default parameters, if at least 7 priviliged ports are hit within 3 seconds, it is classified as a port scan.
*   With default parameters, if at least 21 non-privilged ports are hit withing 3 seconds, it is classified as a port scan.
*   With default parameters, if 4 privileged ports and 9 non-priviliged ports are hit within 3 seconds, it is classified as a port scan, because `4*3 + 9*1 >= 21`.

### Avoiding detection

One of the simplest ways to avoid PSD is to simply [scan slowly](#Limiting_scan_speed). For default values this parameter would suffice:

```
$ nmap --scan-delay 3.1 192.168.56.1

```

Another interesing fact about PSD is that it does not detect a request as a port scan when the `ack` or `rst` flags are set (See the function `is_portscan` in [xt_psd.c](http://sourceforge.net/p/xtables-addons/xtables-addons/ci/master/tree/extensions/xt_psd.c))

Also, if you are port scanning a host and the latter has an HTTP(S) service running on it, nmap will use `Mozilla/5.0 (compatible; Nmap Scripting Engine; [http://nmap.org/book/nse.html](http://nmap.org/book/nse.html))` as default user agent. Your action will thus be easily detected, especially if an administrator or a robot are taking measures if such an user agent appears in the logs. Hopefully, nmap allows us to change that string easily: just pass `-script-args http.useragent="_user agent you want_"`. [Source](http://www.kroosec.com/2012/02/making-nmap-scripting-engine-stealthier.html)

## Tips and Tricks

### Limiting scan speed

Nmap scans are _fast_. While this is often a desirable feature, it can be counter-productive as well. For example when you want to test your system's firewall without disabling any activated flood detection rules, or when you want to run a long-term test for a specific port/service. The following options specify how fast Nmap sends packets.

To send a packet at most every 3.333 seconds:

```
$ nmap --max-rate 0.3 192.168.56.1

```

Alternatively, to send a packet every 3.1 seconds:

```
$ nmap --scan-delay 3.1 192.168.56.1

```

For other timing and parallelization options, see `man nmap`.

### Specify targets input from a list file

Often it is necessary to scan a large number of non-adjuscent addresses. Passing them on the command line is usually not convenient. For this reason Nmap supports **i**nput from a **l**ist file (`-iL`):

 `addresses.txt` 

```
10.1.1.1 10.1.1.2 10.1.1-10.3
10.3.1.3 10.3.1.50 10.3.2.55
10.1.1.100
...

```

```
$ nmap -iL addresses.txt

```

Addresses in the file must be separated with a whitespace.

Alternatively, Nmap can read the list from standard input (the `-` means standard input in many command-line programs):

```
$ echo "10.1.1.1 10.1.1.2 10.1.1-10.3" | nmap -iL -

```

### Specify targets to exclude from scan

```
$ nmap 10.1.1.1-10 --exclude 10.1.1.5,7 

```

The same from a file:

```
$ nmap 10.1.1.1-10 --excludefile excludeaddr.txt

```

### Spoofing

To spoof source IP:

```
$ nmap -S 192.168.56.35 -e vboxnet0 192.168.56.11

```

To spoof the source MAC address:

```
$ nmap --spoof-mac 192.168.56.11

```

To spoof source port:

```
$ nmap --source-port 22 192.168.56.11

```

### Speeding up the scan

By default, Nmap performs DNS/reverse-DNS resolution on targets. To tell Nmap **n**ever do any DNS resolution, pass the `-n` option:

```
$ nmap -n 192.168.56.0/24

```

This will speed the scan about 2 times.

### Scan port number 0

By default port 0 is skipped from scans, even if `-p -` is specified. To scan it, it must be explicitly specified. For example to scan every possible port:

```
$ nmap -p 0-65535

```

Remember that this port number is invalid in RFC standards. However it can be used by malware and the like to avoid more naive port scanners.

### File output formats

Nmap has built-in support for for file output alongside with terminal output:

*   `-oN _filename_`

Normal output, same as the terminal output

*   `-oX _filename_`

XML output, contains very detailed information about the scan, easy to parse with software

*   `-oG _filename_`

Grepable output, deprecated

*   `-oA`

All of the above combined. Creates files called `_sitename_.nmap`, `_sitename_.xml` and `_sitename_.gnmap` if no filename is specified

For example to output to the terminal, to file and to XML file:

```
$ nmap -oN output.txt -oX output.xml scanme.nmap.org

```

## See also

*   [Official website](http://nmap.org/)
*   [Nmap Network Scanning book](http://nmap.org/book/)
*   [Nmap on Wikipedia](https://en.wikipedia.org/wiki/Nmap "wikipedia:Nmap")

Retrieved from "[https://wiki.archlinux.org/index.php?title=Nmap&oldid=413277](https://wiki.archlinux.org/index.php?title=Nmap&oldid=413277)"

[Categories](/index.php/Special:Categories "Special:Categories"):

*   [Networking](/index.php/Category:Networking "Category:Networking")
*   [Security](/index.php/Category:Security "Category:Security")

Hidden category:

*   [Pages or sections flagged with Template:Expansion](/index.php/Category:Pages_or_sections_flagged_with_Template:Expansion "Category:Pages or sections flagged with Template:Expansion")