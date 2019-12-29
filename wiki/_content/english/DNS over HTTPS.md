**DNS over HTTPS** (DNS Queries over HTTPS; **DoH**) wraps [DNS](/index.php/DNS "DNS") queries in [HTTPS](/index.php/TLS "TLS"). Therefore, privacy and integrity of the DNS response is guaranteed, and the system is protected agains man-in-the-middle attacks.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Publicly available servers](#Publicly_available_servers)
*   [2 Configuration](#Configuration)
    *   [2.1 Firefox](#Firefox)
    *   [2.2 Google Chrome](#Google_Chrome)
    *   [2.3 Local DNS server](#Local_DNS_server)
        *   [2.3.1 CoreDNS](#CoreDNS)
*   [3 See also](#See_also)

## Publicly available servers

For a list of publicly available DoH servers see [[1]](https://github.com/curl/curl/wiki/DNS-over-HTTPS) in the *curl Wiki*.

## Configuration

To check whether your browser is using DoH, check [https://1.1.1.1/help](https://1.1.1.1/help).

### [Firefox](/index.php/Firefox "Firefox")

Based on [[2]](https://support.mozilla.org/en-US/kb/firefox-dns-over-https):

1.  open Network Settings in Preferences
2.  click Settings
3.  check Enable DNS over HTTPS

### [Google Chrome](/index.php/Google_Chrome "Google Chrome")

Chrome 78 includes an experimental support for DoH which can be configured via `chrome://flags/#dns-over-https`. [[3]](https://winaero.com/blog/chrome-78-is-out-with-shared-clipboard-and-more/)

### Local [DNS server](/index.php/DNS#DNS_servers "DNS")

You may want to run a local DNS server and configure it to use DoH.

#### CoreDNS

1\. Install [coredns](https://aur.archlinux.org/packages/coredns/) or [coredns-bin](https://aur.archlinux.org/packages/coredns-bin/)

2\. Configure CoreDNS to use Cloudflare, see [[4]](https://coredns.io/plugins/forward/) for details.

 `/etc/coredns/Corefile` 
```
. {
    forward . tls://1.1.1.1 tls://1.0.0.1 {
       tls_servername cloudflare-dns.com
       health_check 5s
    }
    cache 30
}
```

3\. [Start](/index.php/Start "Start") and [enable](/index.php/Enable "Enable") `coredns.service`

4\. Use CoreDNS as nameserver.

 `/etc/resolv.conf`  `nameserver 127.0.0.1` 

## See also

*   [wikipedia:DNS over HTTPS](https://en.wikipedia.org/wiki/DNS_over_HTTPS "wikipedia:DNS over HTTPS")
*   [RFC 8484 - DNS Queries over HTTPS (DoH)](https://tools.ietf.org/html/rfc8484)
*   DNS over TLS (DoT) from [RFC 7858](https://tools.ietf.org/html/rfc7858) provides similar protections.