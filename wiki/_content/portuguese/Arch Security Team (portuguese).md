**Status de tradução:** Esse artigo é uma tradução de [Arch Security Team](/index.php/Arch_Security_Team "Arch Security Team"). Data da última tradução: 2018-09-21\. Você pode ajudar a sincronizar a tradução, se houver [alterações](https://wiki.archlinux.org/index.php?title=Arch_Security_Team&diff=0&oldid=527154) na versão em inglês.

A Equipe de Segurança do Arch é um grupo de voluntários cujo objetivo é rastrear problemas de segurança com pacotes do Arch Linux. Todos os problemas são rastreados no [rastreador de segurança do Arch Linux](https://security.archlinux.org/). A equipe era conhecida como *Arch CVE Monitoring Team* (em português, Equipe de Monitoramento do Arch CVE).

## Contents

*   [1 Missão](#Miss.C3.A3o)
*   [2 Contribuir](#Contribuir)
*   [3 Procedimento](#Procedimento)
    *   [3.1 Fase de investigação e compartilhamento de informações](#Fase_de_investiga.C3.A7.C3.A3o_e_compartilhamento_de_informa.C3.A7.C3.B5es)
    *   [3.2 Situação do upstream e relatório de erros](#Situa.C3.A7.C3.A3o_do_upstream_e_relat.C3.B3rio_de_erros)
    *   [3.3 Rastreamento e publicação](#Rastreamento_e_publica.C3.A7.C3.A3o)
*   [4 Recursos](#Recursos)
    *   [4.1 RSS](#RSS)
    *   [4.2 Listas de discussão](#Listas_de_discuss.C3.A3o)
    *   [4.3 Outras distribuições](#Outras_distribui.C3.A7.C3.B5es)
    *   [4.4 Outros](#Outros)
    *   [4.5 Mais](#Mais)
*   [5 Membros da equipe](#Membros_da_equipe)

## Missão

A missão da Equipe de Segurança do Arch de é contribuir para a melhoria da segurança do Arch Linux.

O dever mais importante da equipe é encontrar e rastrear os problemas atribuídos a [Vulnerabilidades e Exposições Comuns](https://en.wikipedia.org/wiki/Common_Vulnerabilities_and_Exposures "wikipedia:Common Vulnerabilities and Exposures") (CVE). Um CVE é público, é identificado por um ID único do formulário *CVE-AAAA-número*.

Eles publicam ASAs (*Arch Linux Security Advisory*, que significa "Comunicado de Segurança do Arch Linux"), que é um aviso específico do Arch disseminado para os usuários do Arch. Os ASAs estão programados no rastreador para revisão por pares e precisam de duas confirmações dos membros da equipe antes de serem publicados.

O [rastreador de segurança do Arch Linux](https://security.archlinux.org/) é uma plataforma usada pela Equipe de Segurança do Arch para rastrear pacotes, adicionar CVEs e gerar texto de comunicados.

**Nota:**

*   Um *Arch Linux Vulnerability Group* (AVG) é um grupo de CVEs relacionados a um conjunto de pacotes dentro do mesmo *pkgbase*.
*   Pacotes qualificados para um comunicado devem ser parte do repositório *core*, *extra*, *community* ou *multilib*.

## Contribuir

Para se envolver na identificação das vulnerabilidades, é recomendado:

*   Seguir o canal IRC [#archlinux-security](irc://irc.freenode.net/archlinux-security). É o principal meio de comunicação para relatar e discutir CVEs, pacotes afetados e a primeira versão corrigida do pacote.
*   Para ser avisado antecipadamente sobre novos problemas, pode-se monitorar as [#Listas de discussão](#Listas_de_discuss.C3.A3o) recomendadas para novos CVEs, junto com outras fontes, se necessário.
*   Encorajamos os voluntários a examinar os avisos por erros, perguntas ou comentários e relatar no canal do IRC.
*   Inscrever-se nas listas de discussão [arch-security](https://lists.archlinux.org/listinfo/arch-security) e [oss-security](http://oss-security.openwall.org/wiki/mailing-lists/oss-security).
*   Fazer commit de código para o projeto [arch-security-tracker (GitHub)](https://github.com/archlinux/arch-security-tracker) é uma ótima forma de contribuir para a equipe.
*   As distribuições derivadas que dependem dos repositórios de pacotes do Arch Linux são incentivadas a contribuir. Isso ajuda a segurança de todos os usuários.

## Procedimento

O procedimento a seguir sempre que uma vulnerabilidade de segurança foi encontrada em um software empacotado nos repositórios oficiais do Arch Linux é o seguinte:

### Fase de investigação e compartilhamento de informações

*   Entre em contato com um membro da Equipe de Segurança do Arch por meio de seu canal preferido para garantir que o problema foi levado ao conhecimento da equipe.
*   Para substanciar a via mecanismos de pesquisa. Se você precisar de ajuda para investigar o problema de segurança, peça orientação ou suporte no canal do IRC.

### Situação do upstream e relatório de erros

Duas situações podem acontecer:

*   Se o upstream liberar uma nova versão que corrige o problema, o membro da equipe de segurança deve sinalizar o pacote desatualizado.
    *   Se o pacote não foi atualizado após um longo período, um relatório de erro deve ser arquivado sobre a vulnerabilidade.
    *   Se este for um problema de segurança crítico, um relatório de erro deve ser preenchido imediatamente após sinalizar o pacote como desatualizado.
*   Se não houver nenhum release upstream disponível, um relatório de erro deve ser preenchido, incluindo os *patches* para mitigação. As seguintes informações devem ser fornecidas no relatório de erros:
    *   Descrição sobre o problema de segurança e seu impacto
    *   Links para os CVE-IDs e (upstream) relatório
    *   Se nenhum lançamento estiver disponível, links para patches do upstream (ou anexos) que mitigam o problema

### Rastreamento e publicação

As seguintes tarefas devem ser executadas pelos membros da equipe:

*   Um membro da equipe criará um comunicado no [rastreador de segurança](https://security.archlinux.org/) e adicionará os CVEs para rastreamento.
*   Um membro da equipe com acesso a [arch-security](https://lists.archlinux.org/listinfo/arch-security) gerará um ASA do rastreador e o publicará.

**Nota:** Se você tiver um erro privado para relatar, entre em contato com [security@archlinux.org](https://mailman.archlinux.org/pipermail/arch-security/2014-June/000088.html). Por favor, note que o endereço para relatórios de erros privados é *security*, não *arch-security*. Um erro privado é aquele que é muito sensível para publicar, onde qualquer pessoa pode ler e explorar, por exemplo vulnerabilidades na infraestrutura do Arch Linux.

## Recursos

### RSS

	National Vulnerability Database (NVD)

	Todas as vulnerabilidades de CVE: [https://nvd.nist.gov/download/nvd-rss.xml](https://nvd.nist.gov/download/nvd-rss.xml)

	Todas as vulnerabilidades de CVE totalmente analisas: [https://nvd.nist.gov/download/nvd-rss-analyzed.xml](https://nvd.nist.gov/download/nvd-rss-analyzed.xml)

### Listas de discussão

	oss-sec

	Lista principal que trata da segurança do software livre; muitas atribuições CVE acontecem aqui, necessárias se você deseja seguir as notícias de segurança.

	Info: [http://oss-security.openwall.org/wiki/mailing-lists/oss-security](http://oss-security.openwall.org/wiki/mailing-lists/oss-security)

	Inscrição: oss-security-subscribe(at)lists.openwall.com

	Arquivo: [http://www.openwall.com/lists/oss-security/](http://www.openwall.com/lists/oss-security/)

	BugTraq

	Uma lista de discussão de full-disclosure* (muitas mensagens).

	Info: [http://www.securityfocus.com/archive/1/description](http://www.securityfocus.com/archive/1/description)

	Inscrição: bugtraq-subscribe(at)securityfocus.com

	Full-disclosure

	Outra lista de discussão de full-disclosure* (muitas mensagens).

	Info: [http://lists.grok.org.uk/full-disclosure-charter.html](http://lists.grok.org.uk/full-disclosure-charter.html)

	Inscrição: full-disclosure-request(at)lists.grok.org.uk

Considere também seguir as listas de discussão para pacotes específicos, como LibreOffice, X.org, Puppetlabs, ISC, etc.

1.  *full-disclosure*, que pode ser traduzido para "divulgação responsável" ou literalmente "revelação total", é a prática de publicação de aálise de vulnerabilidades de software o mais cedo possível, tornando-a acessível para ciência das pessoas e facilitando sua correção.

### Outras distribuições

Recursos de outras distribuições (para procurar por CVE, patch, comentários etc.):

	RedHat e Fedora

	Feed de comunicados: [https://bodhi.fedoraproject.org/rss/updates/?type=security](https://bodhi.fedoraproject.org/rss/updates/?type=security)

	Rastreador de CVE: [https://access.redhat.com/security/cve/](https://access.redhat.com/security/cve/)<CVE-ID>

	Rastreador de erros: [https://bugzilla.redhat.com/show_bug.cgi?id=](https://bugzilla.redhat.com/show_bug.cgi?id=)<CVE-ID>

	Ubuntu

	Feed de comunicados: [https://www.ubuntu.com/usn/atom.xml](https://www.ubuntu.com/usn/atom.xml)

	Rastreador de CVE: [https://people.canonical.com/~ubuntu-security/cve/?cve=](https://people.canonical.com/~ubuntu-security/cve/?cve=)<CVE-ID>

	Banco de dados: [https://code.launchpad.net/~ubuntu-security/ubuntu-cve-tracker/master](https://code.launchpad.net/~ubuntu-security/ubuntu-cve-tracker/master)

	Debian

	Rastreador de CVE: [https://security-tracker.debian.org/tracker/](https://security-tracker.debian.org/tracker/)<CVE-ID>/

	Rastreador de Patch: [https://tracker.debian.org/pkg/patch](https://tracker.debian.org/pkg/patch)

	Banco de dados: [https://anonscm.debian.org/viewvc/secure-testing/data/](https://anonscm.debian.org/viewvc/secure-testing/data/)

	OpenSUSE

	Rastreador de CVE: [https://www.suse.com/security/cve/](https://www.suse.com/security/cve/)<CVE-ID>/

### Outros

	Links de Mitre e NVD para CVEs

	[https://cve.mitre.org/cgi-bin/cvename.cgi?name=](https://cve.mitre.org/cgi-bin/cvename.cgi?name=)<CVE-ID>

	[https://web.nvd.nist.gov/view/vuln/detail?vulnId=](https://web.nvd.nist.gov/view/vuln/detail?vulnId=)<CVE-ID>

O NVD e o Mitre não preenchem necessariamente sua entrada no CVE imediatamente após a atribuição, portanto, isso nem sempre é relevante para o Arch. Os campos CVE-ID e "Data Entry Created" não têm significado particular. CVE são atribuídos pelas Autoridades de Numeração CVE (CNA) e cada CNA obtém blocos CVE de Mitre quando necessário/solicitado, portanto, o ID CVE não está vinculado à data de atribuição. O campo "Date Entry Created" geralmente indica apenas quando o bloco CVE foi dado ao CNA, nada mais.

	Linux Weekly News

	LWN fornece uma divulgação diária de atualizações de segurança para várias distribuições.

	[https://lwn.net/headlines/newrss](https://lwn.net/headlines/newrss)

### Mais

Para mais recursos, veja o [Open Source Software Security Wiki](http://oss-security.openwall.org/wiki/) do OpenWall.

## Membros da equipe

Veja [Arch Security Team](/index.php/Arch_Security_Team "Arch Security Team") para a relação dos atuais membros da Equipe de Segurança do Arch.