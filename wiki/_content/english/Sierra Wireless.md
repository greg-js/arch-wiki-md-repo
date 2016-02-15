This installation guide was written for the Sierra Wireless 875U USB 3.5G HSDPA Modem but should apply to others.

Required software includes ppp (part of the base Arch installation) and a package of [Sierra ppp scripts](http://www.sierrawireless.com/resources/support/Software/Linux/ppp-scripts.tar.gz). Using a ppp frontend may eliminate the need for the scripts.

The next steps are to place these scripts in the right places under /etc/ppp, set permissions, configure pppd, and test the connection. For more detailed information, please refer to [Sierra's FAQ](http://www.sierrawireless.com/faq/ShowFAQ.aspx?ID=607).

Note that the stock Arch kernel seems to include support for this type of card, and that the drivers available from Sierra are for older kernel versions than those found in Arch.