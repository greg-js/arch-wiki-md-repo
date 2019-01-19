**Status de tradução:** Esse artigo é uma tradução de [Secure Shell](/index.php/Secure_Shell "Secure Shell"). Data da última tradução: 2019-01-18\. Você pode ajudar a sincronizar a tradução, se houver [alterações](https://wiki.archlinux.org/index.php?title=Secure_Shell&diff=0&oldid=560110) na versão em inglês.

Artigos relacionados

*   [SSHFS](/index.php/SSHFS "SSHFS")
*   [Mosh](/index.php/Mosh_(Portugu%C3%AAs) "Mosh (Português)")

De acordo com o [Wikipédia](https://en.wikipedia.org/wiki/Secure_Shell "wikipedia:Secure Shell"):

	O Secure Shell (SSH) é um protocolo de rede criptográfica para a operação segura de serviços de rede em uma rede desprotegida. Os aplicativos típicos incluem o login da linha de comando remota e a execução de comandos remotos, mas qualquer serviço de rede pode ser protegido com o SSH.

Exemplos de serviços que podem usar o SSH são [Git](/index.php/Git "Git"), [rsync](/index.php/Rsync "Rsync") e [encaminhamento de X11](/index.php/X11_forwarding "X11 forwarding"). Serviços que sempre usam SSH são [SCP e SFTP](/index.php/SCP_and_SFTP "SCP and SFTP").

Um servidor SSH, por padrão, escuta na porta TCP padrão 22\. Um programa cliente SSH é normalmente usado para estabelecer conexões com um daemon *sshd* aceitando conexões remotas. Ambos estão comumente presentes nos sistemas operacionais mais modernos, incluindo macOS, GNU/Linux, Solaris e OpenVMS. Existem versões proprietárias, freeware e de código aberto de vários níveis de complexidade e integridade.

## Implementações

*   **Dropbear** — Servidor SSH leve. O cliente ssh de linha de comando é chamado [dbclient(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/dbclient.1).

	[https://matt.ucc.asn.au/dropbear/dropbear.html](https://matt.ucc.asn.au/dropbear/dropbear.html) || [dropbear](https://www.archlinux.org/packages/?name=dropbear)

*   **[OpenSSH](/index.php/OpenSSH "OpenSSH")** — Ferramenta de conectividade *premier* para login remoto com o protocolo SSH

	[https://www.openssh.com/portable.html](https://www.openssh.com/portable.html) || [openssh](https://www.archlinux.org/packages/?name=openssh)

*   **TinySSH** — Um servidor SSH minimalista que implementa apenas um subconjunto de recursos do SSHv2; glibc como sua única dependência.

	[https://tinyssh.org/](https://tinyssh.org/) || [tinyssh](https://www.archlinux.org/packages/?name=tinyssh)

## Protegendo

Veja [Security#SSH](/index.php/Security#SSH "Security").

## Veja também

*   [Multiplexadores de terminal](/index.php/Terminal_multiplexer "Terminal multiplexer") (geralmente usados por SSH)
*   [Wikipedia:Comparison of SSH clients](https://en.wikipedia.org/wiki/Comparison_of_SSH_clients "wikipedia:Comparison of SSH clients")
*   [Wikipedia:Comparison of SSH servers](https://en.wikipedia.org/wiki/Comparison_of_SSH_servers "wikipedia:Comparison of SSH servers")