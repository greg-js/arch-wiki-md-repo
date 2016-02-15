The latest and fairly improved version (now not only reports the network activity) has been moved.

Full information and screenshots in [github](https://github.com/lightful/xfce-hkmon).

The original version is also available in git history, but the new one it is as simple and easy to install:

## Installation instructions

Download [xfce-hkmon.cpp](https://raw.githubusercontent.com/lightful/xfce-hkmon/master/xfce-hkmon.cpp) and compile it:

```
g++ -std=c++0x -O3 -lrt xfce-hkmon.cpp -o xfce-hkmon

```

Place the executable somewhere (e.g. /usr/local/bin) and add a **XFCE Generic Monitor Applet** with these settings: no label, 1 second period, _Bitstream Vera Sans Mono font_ (recommended) and the following command:

```
/usr/local/bin/xfce-hkmon NET CPU TEMP IO RAM

```

You may also add an interface name (eth0, ppp0,...) to override the automatic selection by traffic.