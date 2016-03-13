From [Wikipedia](https://en.wikipedia.org/wiki/Jumbo_frame "wikipedia:Jumbo frame"):

	*In computer networking, jumbo frames are Ethernet frames with more than 1,500 bytes of payload (MTU). Conventionally, jumbo frames can carry up to 9,000 bytes of payload, but variations exist and some care must be taken when using the term. Many, but not all, Gigabit Ethernet switches and Gigabit Ethernet network interface cards support jumbo frames, but all Fast Ethernet switches and Fast Ethernet network interface cards support only standard-sized frames.*

Using a larger MTU value (jumbo frames) can significantly speed up your network transfers.

## Contents

*   [1 Notes on jumbo frames](#Notes_on_jumbo_frames)
    *   [1.1 Some drivers will prevent lower C-states](#Some_drivers_will_prevent_lower_C-states)
*   [2 Requirements](#Requirements)
*   [3 Configuration](#Configuration)
    *   [3.1 Systemd unit](#Systemd_unit)
    *   [3.2 Netctl](#Netctl)
*   [4 Examples](#Examples)
    *   [4.1 Example LAN Architecture using Jumbo Frames](#Example_LAN_Architecture_using_Jumbo_Frames)
*   [5 See also](#See_also)

## Notes on jumbo frames

### Some drivers will prevent lower C-states

Some kernel drivers, like e1000e will prevent the CPU from entering C-states under C3 with non-standard MTU sizes by design. See [bugzilla #77361](https://bugzilla.kernel.org/show_bug.cgi?id=77361) for comments by the developers.

## Requirements

1.  Must be GigLAN backbone (i.e. 1000baseT)
2.  Local NICs in the local PCs must support JFs
3.  Switches must support JFs

## Configuration

Invoke `ip` with the mtu parameter as follows:

 `# ip link set ethx mtu <size>` 

Where `ethx` is the ethernet adapter in question (eth0, eth1, etc.) and `<size>` is the size of the frame you wish to use (1500, 4000, 9000).

Use `ip link show | grep mtu` to verify that the setting has been applied.

Example:

 `$ ip link show | grep mtu` 
```
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 16436 qdisc noqueue state UNKNOWN 
2: eth0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 4000 qdisc pfifo_fast state UP qlen 1000
3: eth1: <BROADCAST,MULTICAST> mtu 1500 qdisc noop state DOWN qlen 1000

```

### Systemd unit

**Tip:** If supported, it's recommend to set the MTU value in the [Network manager](/index.php/List_of_applications/Internet#Network_managers "List of applications/Internet") instead (see [systemd-networkd](/index.php/Systemd-networkd#.5BLink.5D_section "Systemd-networkd")).

To make the setting permanent, we will create a systemd unit.

 `/etc/systemd/system/setmtu@.service` 
```
[Unit]
Description=Set mtu on device
Before=network.target

[Service]
Type=oneshot
EnvironmentFile=/etc/conf.d/setmtu
ExecStart=/usr/bin/ip link set dev %i up mtu ${%i}

[Install]
WantedBy=multi-user.target

```

Now create the configuration. Adjust it as necessary, adding one line for each device:

 `/etc/conf.d/setmtu` 
```
eth0=4000

```

That will set the mtu of `eth0` to 4000.

And now [enable and start the service](/index.php/Daemon "Daemon") on every device you want to configure. (In this example, the service would be `setmtu@eth0.service`)

### Netctl

For adapters configured by [netctl](/index.php/Netctl "Netctl"), another way to set the mtu persistently is to use the `ExecUpPost` variable in the network profile:

```
ExecUpPost='/usr/bin/ip link set eth0 mtu 4000'

```

## Examples

**Note:** These tests were performed on old hardware without the use of a RAM disk, so these results may be quite different from a test performed on modern systems using RAM disks. Using RAM disks would remove potential performance degradation due to slow, magnetic hard disks and would likely increase the benefit of using jumbo frames.

It is important to test various frame sizes doing typical file transfers to determine the optimal setting. There is not a one-size-fits-all setting for jumbo frames. In fact, as illustrated below, depending on the hardware, a frame size that is too large can actually hurt network throughput.

Three different frame sizes (standard 1500, jumbo 4000, and jumbo 9000) were tested under several different conditions (single large file and multiple small files). The results indicate that for this particular hardware, a 4000 frame size gave the optimal results. Again, this result is not general; users will need to evaluate the effect that different frame sizes have on different file transfers on a case-by-case basis.

Both machine A and machine B are using EIDE hard drives circa ~2004; a modern SATA II HDD and MB will give higher throughput for sure, but the data are still valid. Also, both machines are using [D-Link 530T](http://us.dlink.com/search/keyword/530T/) NICs (PCI bus) and are set to the frame size indicated in the tables below (1500, 4000, and 9000).

**Test 1 - Single large file (1,048,522 kb) via Samba**

*Times and throughput represent the average of three runs.*

| mtu=1500 | t (sec) | Kb/sec | mtu=4000 | t (sec) | Kb/sec | mtu=9000 | t (sec) | Kb/sec |
| A to B | 48 | 21,844 | A to B | 44 | 23,830 | A to B | 49 | 21,398 |
| B to A | 81 | 12,945 | B to A | 41 | 25,574 | B to A | 41 | 25,574 |

**Summary of Test 1**

| 4k vs. 1.5k |  % change | 9k vs. 1.5k |  % change |
| A to B | +9 % | A to B | -2 % |
| B to A | +98 % | B to A | +98 % |

* * *

**Test 2 - Several small files (1,283,439 kb total) via Samba**

*Times and throughput represent the average of three runs.*

| mtu=1500 | t (sec) | Kb/sec | mtu=4000 | t (sec) | Kb/sec | mtu=9000 | t (sec) | Kb/sec |
| A to B | 59 | 21,753 | A to B | 51 | 25,165 | A to B | 57 | 22,516 |
| B to A | 94 | 13,654 | B to A | 46 | 27,901 | B to A | 49 | 26,193 |

**Summary of Test 2**

| 4k vs. 1.5k |  % change | 9k vs. 1.5k |  % change |
| A to B | +16 % | A to B | +4 % |
| B to A | +4% | B to A | +92 % |

* * *

**Sustained Transfer Speed**

An average speed of 26.6 MB/s on a 30+ GB transfer using 4k jumbo frames. The slowest drive in the link was a Western Digital WD3200JB - circa 2004, EIDE 320 GB (ATA100/7200 RPM/8 MB cache). Burst speeds (i.e. 300-400 megabyte files) through the network are about 80% of the burst speed drive-to-drive which is not too bad (approximately 30 MB/s network vs. approximately 38 MB/s drive-to-drive).

### Example LAN Architecture using Jumbo Frames

```
PC1 (JF Enabled)

PC2 (JF Enabled) <----> Gigabit Ethernet switch (JF Enabled) <----> Router (JF Unenabled) <----> Cable modem (JF Unenabled)

PC3 (JF Enabled)

```

In the above example, all the PCs have NICs set to use JFs and are all connected to a Gigabit Ethernet switch that can also use JFs. The switch is in turn connected via the uplink port to a router that **cannot** use jumbo frames which is in turn connected to a cable modem which also **cannot** use jumbo frames.

Contrary to what some web sites state, this setup works 100% fine. Transfers inside the JF portion on the network (i.e. behind the switch) are very fast. Transfers to the WAN (the Internet) from PCs behind the switch are just as fast as a PC without JFs enabled connected either directly to the cable modem, or to the router.

## See also

*   [Gigabit Ethernet Jumbo Frames - And why you should care](http://sd.wareonearth.com/~phil/jumbo.html)