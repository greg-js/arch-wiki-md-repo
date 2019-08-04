Related articles

*   [SSHFS](/index.php/SSHFS "SSHFS")
*   [Mosh](/index.php/Mosh "Mosh")
*   [VPN over SSH](/index.php/VPN_over_SSH "VPN over SSH")

According to [Wikipedia](https://en.wikipedia.org/wiki/Secure_Shell "wikipedia:Secure Shell"):

	Secure Shell (SSH) is a cryptographic network protocol for operating network services securely over an unsecured network. Typical applications include remote command-line login and remote command execution, but any network service can be secured with SSH.

Examples of services that can use SSH are [Git](/index.php/Git "Git"), [rsync](/index.php/Rsync "Rsync") and [X11 forwarding](/index.php/X11_forwarding "X11 forwarding"). Services that always use SSH are [SCP and SFTP](/index.php/SCP_and_SFTP "SCP and SFTP").

An SSH server, by default, listens on the standard TCP port 22\. An SSH client program is typically used for establishing connections to an *sshd* daemon accepting remote connections. Both are commonly present on most modern operating systems, including macOS, GNU/Linux, Solaris and OpenVMS. Proprietary, freeware and open source versions of various levels of complexity and completeness exist.

## Implementations

*   **[Dropbear](https://en.wikipedia.org/wiki/Dropbear_(software) "wikipedia:Dropbear (software)")** — Lightweight SSH server. The command-line ssh client is named [dbclient(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/dbclient.1).

	[https://matt.ucc.asn.au/dropbear/dropbear.html](https://matt.ucc.asn.au/dropbear/dropbear.html) || [dropbear](https://www.archlinux.org/packages/?name=dropbear)

*   **[OpenSSH](/index.php/OpenSSH "OpenSSH")** — Premier connectivity tool for remote login with the SSH protocol

	[https://www.openssh.com/portable.html](https://www.openssh.com/portable.html) || [openssh](https://www.archlinux.org/packages/?name=openssh)

*   **TinySSH** — A minimalistic SSH server which implements only a subset of SSHv2 features; glibc as its single dependency.

	[https://tinyssh.org/](https://tinyssh.org/) || [tinyssh](https://www.archlinux.org/packages/?name=tinyssh)

## Securing

See [Security#SSH](/index.php/Security#SSH "Security").

## See also

*   [Terminal multiplexers](/index.php/Terminal_multiplexer "Terminal multiplexer") (often used over SSH)
*   [Wikipedia:Comparison of SSH clients](https://en.wikipedia.org/wiki/Comparison_of_SSH_clients "wikipedia:Comparison of SSH clients")
*   [Wikipedia:Comparison of SSH servers](https://en.wikipedia.org/wiki/Comparison_of_SSH_servers "wikipedia:Comparison of SSH servers")
*   [SSH Key Fingerprint formats](https://blog.webernetz.net/ssh-key-fingerprints/)