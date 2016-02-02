# Burp suite

From the [official website](http://portswigger.net/burp/):

	_Burp Suite is an integrated platform for performing security testing of web applications. Its various tools work seamlessly together to support the entire testing process, from initial mapping and analysis of an application's attack surface, through to finding and exploiting security vulnerabilities._3

## Contents

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
    *   [2.1 Install HTTPS certificate in Firefox](#Install_HTTPS_certificate_in_Firefox)
*   [3 See also](#See_also)

## Installation

Install [burpsuite](https://aur.archlinux.org/packages/burpsuite/)<sup><small>AUR</small></sup> from [AUR](/index.php/AUR "AUR").

## Configuration

Burp Proxy will work out of the box with HTTP connections. For HTTPS, PortSwigger's certificate must be installed first.

### Install HTTPS certificate in Firefox

Start up Burp:

```
$ burpsuite

```

and open the _Proxy -> Options_. In the _Proxy Listeners_ section add a new interface. Set _Interface_ to `127.0.0.1:8080` and make sure the _Running_ checkbox is enabled.

Navigate to `[http://127.0.0.1:8080/](http://127.0.0.1:8080/)` in Firefox, click the _CA Certificate_ link at top right and save the certificate file somewhere.

In Firefox open the _Preferences_ window and go to _Advanced -> Certificates -> View Certificates_. Click _Import_ and select the file. Check the _Trust this CA to identify websites_ checkbox and click _OK_.

## See also

*   [Burp Suite Video Tutorials](http://portswigger.net/burp/tutorials/)

Retrieved from "[https://wiki.archlinux.org/index.php?title=Burp_suite&oldid=396983](https://wiki.archlinux.org/index.php?title=Burp_suite&oldid=396983)"