Esta página descreve as diretrizes de empacotamento de segurança para pacotes do Arch Linux. Para projetos C/C++, o compilador e o vinculador podem aplicar opções de proteção de segurança. O Arch Linux, por padrão, aplica PIE, fonte Fortify, protetor de pilha, nx e relro. As proteções *hardening* podem ser revisadas executando [checksec](https://www.archlinux.org/packages/?name=checksec).

```
$ checksec --file=/usr/bin/cat

```

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 RELRO](#RELRO)
    *   [1.1 Haskell](#Haskell)
*   [2 Stack Canary](#Stack_Canary)
*   [3 NX](#NX)
    *   [3.1 C/C++](#C/C++)
*   [4 PIE](#PIE)
    *   [4.1 C/C++](#C/C++_2)
    *   [4.2 Golang](#Golang)
    *   [4.3 Haskell](#Haskell_2)
*   [5 RPATH/RUNPATH](#RPATH/RUNPATH)
*   [6 FORTIFY](#FORTIFY)
*   [7 Serviços systemd](#Serviços_systemd)
    *   [7.1 Acesso de arquivos](#Acesso_de_arquivos)
    *   [7.2 Usuário](#Usuário)
    *   [7.3 Memória](#Memória)
    *   [7.4 Chamadas de sistema](#Chamadas_de_sistema)
    *   [7.5 Rede](#Rede)
    *   [7.6 Várias](#Várias)

## RELRO

O RELRO é uma técnica genérica de mitigação para proteger as seções de dados de um processo/binário ELF. Quando um programa é carregado, várias seções da memória ELF precisam ser gravadas pelo vinculador. mas pode ser ativado como somente leitura antes de passar o controle para o programa. Isso evita que os invasores substituam algumas seções da ELF. Existem dois modos RELRO diferentes:

*   Partial RELRO (`-Wl,-z,relro`): algumas seções são marcadas como somente leitura após o carregamento do programa, exceto que o GOT (.got.plt) ainda pode ser gravado.

*   Full RELRO (`-Wl,-z,now`) durante o carregamento do programa, todos os símbolos dinâmicos são resolvidos, permitindo que o GOT completo seja marcado como somente leitura.

Se um aplicativo relatar relro parcial, investigue se a cadeia de ferramentas de compilação passa nossos LDFLAGS ou permite substituir LDFLAGS. Para os pacotes Go, investigue se o método de compilação usa "build.go" como uma substituição pura do Makefile golang, que não permite a passagem de LDFLAGS.

### Haskell

Para Haskell, não está claro como alcançar o Full RELRO no momento.

## Stack Canary

Um [stack canary](https://en.wikipedia.org/wiki/pt:Stack_canary "wikipedia:pt:Stack canary") é adicionado pelo compilador entre o buffer e os dados de controle na pilha. Se esse valor conhecido estiver corrompido, ocorreu um estouro de buffer e o programa em execução é segmentado para impedir uma possível execução arbitrária do código.

O pacote [gcc](https://www.archlinux.org/packages/?name=gcc) ativou a proteção de pilha por padrão com o [--enable-default-ssp](https://git.archlinux.org/svntogit/packages.git/tree/trunk/PKGBUILD?h=packages/gcc#n120) opção de compilação.

## NX

### C/C++

A proteção do espaço executável marca as regiões da memória como não executáveis, de modo que uma tentativa de executar o código da máquina nessas regiões causará uma exceção. Ele utiliza recursos de hardware como o bit NX (bit sem execução) ou, em alguns casos, emulação de software desses recursos.

## PIE

### C/C++

O pacote [gcc](https://www.archlinux.org/packages/?name=gcc) o tem habilitado por padrão para C/C++ com [--enable-default-pie](https://git.archlinux.org/svntogit/packages.git/tree/trunk/PKGBUILD?h=packages/gcc#n119).

### Golang

Para pacotes Go, adicione um [makedepend](/index.php/PKGBUILD_(Portugu%C3%AAs)#makedepends "PKGBUILD (Português)") de [go-pie](https://www.archlinux.org/packages/?name=go-pie).

### Haskell

Passe o seguinte sinalizador para a configuração de *runhaskell* Setup:

```
--ghc-option='-pie'

```

## RPATH/RUNPATH

RUNPATH/RPATH provides further search paths for the object it is listed in (it can be used both for executable and for shared objects).

```
$ objdump -x /usr/bin/perl | egrep 'RPATH|RUNPATH'

```

If the RPATH value contains a path within an attackers control it can possibly execute code by installing a malicious library in that directory for example [CVE-2006-1566](https://nvd.nist.gov/vuln/detail/CVE-2006-1566) [CVE-2005-4280](https://www.cvedetails.com/cve/CVE-2005-4280/).

The RPATH entry is set by the linker by passing for example the following string to LDFLAGS -Wl,-rpath -Wl,/usr/local/lib. To make an RUNPATH entry append --enable-new-dtags to the linker flags.

## FORTIFY

Fortify source is a macro that adds buffer overflow protection in various functions that perform operations on memory and strings. It checks whether an attacker tries to copy more bytes to overflow a buffer and then stops the execution of the program. This protection is enabled with the default CPPFLAGS in makepkg.conf:

```
CPPFLAGS="-D_FORTIFY_SOURCE=2"

```

## Serviços systemd

If a systemd service file is shipped with the package due to upstream not providing any, look into applying the following systemd service hardening features. Systemd provides a way to analyse security features which are enabled for a service.

```
$ systemd-analyze security pacman.service

```

### Acesso de arquivos

A service can be hardened by restricting filesystem access.

Set up a new fiel system namespace for the executed process and mounts private /tmp and var/tmp directories inside it that is not shared by processes outside the namespace. Useful for programs which write data to /tmp.

```
PrivateTmp=true

```

ProtectSystem has three different varieties of mounting directories as read-only for the executed process. The "full" option mounts /usr, /boot and /etc read only. ProtectHome makes /home, /root and /run/user inaccessible to the executed process.

```
ProtectSystem=strict
ProtectHome=true

```

Sets up a new /dev namespace for the executed process and only adds API pseudo devices such as /dev/null, /dev/zero or /dev/random, but not for physical devices or system memory, system ports and others. This is useful to secure the execute process from writing directly to physical devices, systemd also adds a system call filter for calls within the @raw-io set.

```
PrivateDevices=true

```

These options make the executed process unable to change kernel variables accessible through /proc/sys, /sys, etc. ProtectControlGroups makes the /sys/fs/cgroup hierarchy read-only.

```
ProtectKernelTunables=true
ProtectControlGroups=true

```

More detailed information can be found in [systemd.exec(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/systemd.exec.5).

### Usuário

Ensure that the executed process and it's children can never gain new privileges through execve().

```
NoNewPrivileges=true

```

### Memória

Prohibit attempts to create memory mappings that are both writable and executable, to change mappings to be executable or to crate executable shared memory. This sandboxes a process against allowing an attacker to write in to memory which is also executed. Note that enabling this is not compatible with all applications which rely on a JIT.

```
MemoryDenyWriteExecute=true

```

### Chamadas de sistema

Locks down the [personality(2)](https://jlk.fjfi.cvut.cz/arch/manpages/man/personality.2) system call so that the kernel execution domain can not be changed.

```
LockPersonality=true

```

System calls can be restricted in a service as well, systemd can display syscalls to filter on:

```
$ systemd-analyze syscall-filter

```

Restricting swap syscall can be done as following

```
SystemCallFilter=@swap

```

### Rede

If the running process does not require any network access it can be fully disabled by setting up a new network namespace for the process and only configuration a loopback interface.

```
PrivateNetwork=true

```

For when only network to localhost or specific IP ranges is required a process can be restricted by only allowing network access to localhost.

```
IPAddressAllow=localhost
IPAddressDeny=any

```

More information about network filtering can be found in [systemd.resource-control(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/systemd.resource-control.5).

### Várias

Sets up a new UTS namespace for the execute process and disallows changing the hostname or domainname.

```
ProtectHostname=true

```