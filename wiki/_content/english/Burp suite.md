From the [official website](http://portswigger.net/burp/):

	Burp Suite is an integrated platform for performing security testing of web applications. Its various tools work seamlessly together to support the entire testing process, from initial mapping and analysis of an application's attack surface, through to finding and exploiting security vulnerabilities.

## Contents

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
    *   [2.1 Install HTTPS certificate in Firefox](#Install_HTTPS_certificate_in_Firefox)
*   [3 See also](#See_also)

## Installation

Install [burpsuite](https://aur.archlinux.org/packages/burpsuite/) from [AUR](/index.php/AUR "AUR").

This will install Burp Suite Community (free edition).

## Configuration

Burp Proxy will work out of the box with HTTP connections. For HTTPS, PortSwigger's certificate must be installed first.

### Install HTTPS certificate in Firefox

Start up Burp:

```
$ burpsuite

```

Open the *Proxy -> Options*. In the *Proxy Listeners* section add a new interface. Set *Interface* to `127.0.0.1:8080` and make sure the *Running* checkbox is enabled.

Navigate to `[http://127.0.0.1:8080/](http://127.0.0.1:8080/)` in Firefox, click the *CA Certificate* link at top right and save the certificate file somewhere.

In Firefox open the *Preferences* window and go to *Advanced -> Certificates -> View Certificates*. Click *Import* and select the file. Check the *Trust this CA to identify websites* checkbox and click *OK*.

## See also

*   [Wikipedia:Burp suite](https://en.wikipedia.org/wiki/Burp_suite "wikipedia:Burp suite")
*   [Burp Suite video tutorials](http://portswigger.net/burp/tutorials/)