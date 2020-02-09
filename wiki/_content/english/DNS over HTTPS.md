Related articles

*   [DNS over HTTPS servers](/index.php/DNS_over_HTTPS_servers "DNS over HTTPS servers")

**DNS over HTTPS** (DNS Queries over HTTPS; **DoH**) wraps [DNS](/index.php/DNS "DNS") queries in HTTPS. Therefore, privacy and integrity of the DNS response is guaranteed, and the system is protected agains man-in-the-middle attacks.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Publicly available servers](#Publicly_available_servers)
*   [2 Client Configuration](#Client_Configuration)
    *   [2.1 Firefox](#Firefox)
    *   [2.2 Google Chrome](#Google_Chrome)
*   [3 Local DNS server](#Local_DNS_server)
    *   [3.1 cloudflared](#cloudflared)
*   [4 See also](#See_also)

## Publicly available servers

For a list of publicly available DoH servers see [[1]](https://github.com/curl/curl/wiki/DNS-over-HTTPS) in the *curl Wiki*.

## Client Configuration

To check whether your browser is using Cloudflare DoH, visit [https://1.1.1.1/help](https://1.1.1.1/help).

### Firefox

Based on [[2]](https://support.mozilla.org/en-US/kb/firefox-dns-over-https):

1.  open Network Settings in Preferences
2.  click Settings
3.  check Enable DNS over HTTPS

### Google Chrome

[Chrome](/index.php/Chrome "Chrome") 78 includes an experimental support for DoH which can be configured via `chrome://flags/#dns-over-https`. [[3]](https://winaero.com/blog/chrome-78-is-out-with-shared-clipboard-and-more/)

## Local DNS server

You may want to run a [local DNS server](/index.php/Domain_name_resolution#DNS_servers "Domain name resolution") and configure it to use DoH.

### cloudflared

1\. Install [cloudflared-bin](https://aur.archlinux.org/packages/cloudflared-bin/)

2\. Create the following file:

 `/etc/cloudflared/cloudflared.yml` 
```
proxy-dns: true
proxy-dns-upstream:
 - https://1.0.0.1/dns-query
 - https://1.1.1.1/dns-query
 - https://2606:4700:4700::1111/dns-query
 - https://2606:4700:4700::1001/dns-query
proxy-dns-port: 5053
proxy-dns-address: 0.0.0.0

```

3\. [Start](/index.php/Start "Start") and [enable](/index.php/Enable "Enable") `cloudflared@cloudflared.service`

4\. Use `127.0.0.1:5053` as a DNS server

Upstream documentation: [https://developers.cloudflare.com/1.1.1.1/dns-over-https/cloudflared-proxy/](https://developers.cloudflare.com/1.1.1.1/dns-over-https/cloudflared-proxy/)

## See also

*   [wikipedia:DNS over HTTPS](https://en.wikipedia.org/wiki/DNS_over_HTTPS "wikipedia:DNS over HTTPS")
*   [RFC 8484 - DNS Queries over HTTPS (DoH)](https://tools.ietf.org/html/rfc8484)