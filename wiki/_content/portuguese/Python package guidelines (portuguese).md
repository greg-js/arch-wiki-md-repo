**Status de tradução:** Esse artigo é uma tradução de [Python package guidelines](/index.php/Python_package_guidelines "Python package guidelines"). Data da última tradução: 2019-11-22\. Você pode ajudar a sincronizar a tradução, se houver [alterações](https://wiki.archlinux.org/index.php?title=Python_package_guidelines&diff=0&oldid=589438) na versão em inglês.

**[Diretrizes de criação de pacotes](/index.php/Padr%C3%B5es_de_empacotamento_do_Arch "Padrões de empacotamento do Arch")**

* * *

[32-bit](/index.php/Diretrizes_de_pacotes_32-bit "Diretrizes de pacotes 32-bit") – [CLR](/index.php/Diretrizes_de_pacotes_CLR "Diretrizes de pacotes CLR") – [Cross](/index.php/Diretrizes_de_pacotes_de_ferramentas_de_compila%C3%A7%C3%A3o_cruzada "Diretrizes de pacotes de ferramentas de compilação cruzada") – [Eclipse](/index.php/Diretrizes_de_pacotes_de_plugin_do_Eclipse "Diretrizes de pacotes de plugin do Eclipse") – [Electron](/index.php/Diretrizes_de_pacotes_Electron "Diretrizes de pacotes Electron") – [Free Pascal](/index.php/Diretrizes_de_pacotes_Free_Pascal "Diretrizes de pacotes Free Pascal") – [GNOME](/index.php/Diretrizes_de_pacotes_GNOME "Diretrizes de pacotes GNOME") – [Go](/index.php/Diretrizes_de_pacotes_Go "Diretrizes de pacotes Go") – [Haskell](/index.php/Diretrizes_de_pacotes_Haskell "Diretrizes de pacotes Haskell") – [Java](/index.php/Diretrizes_de_pacotes_Java "Diretrizes de pacotes Java") – [KDE](/index.php/Diretrizes_de_pacotes_KDE "Diretrizes de pacotes KDE") – [Kernel](/index.php/Diretrizes_de_pacotes_de_m%C3%B3dulos_de_kernel "Diretrizes de pacotes de módulos de kernel") – [Lisp](/index.php/Diretrizes_de_pacotes_Lisp "Diretrizes de pacotes Lisp") – [MinGW](/index.php/Diretrizes_de_pacotes_MinGW "Diretrizes de pacotes MinGW") – [Node.js](/index.php/Diretrizes_de_pacotes_Node.js "Diretrizes de pacotes Node.js") – [Nonfree](/index.php/Diretrizes_de_pacotes_de_aplicativos_n%C3%A3o_livres "Diretrizes de pacotes de aplicativos não livres") – [OCaml](/index.php/Diretrizes_de_pacotes_OCaml "Diretrizes de pacotes OCaml") – [Perl](/index.php/Diretrizes_de_pacotes_Perl "Diretrizes de pacotes Perl") – [PHP](/index.php/Diretrizes_de_pacotes_PHP "Diretrizes de pacotes PHP") – [Python](/index.php/Diretrizes_de_pacotes_Python "Diretrizes de pacotes Python") – [R](/index.php/Diretrizes_de_pacotes_R "Diretrizes de pacotes R") – [Ruby](/index.php/Diretrizes_de_pacotes_Ruby_Gem "Diretrizes de pacotes Ruby Gem") – [Rust](/index.php/Diretrizes_de_pacotes_Rust "Diretrizes de pacotes Rust") – [VCS](/index.php/Diretrizes_de_pacotes_VCS "Diretrizes de pacotes VCS") – [Web](/index.php/Diretrizes_de_pacotes_de_aplicativos_da_Web "Diretrizes de pacotes de aplicativos da Web") – [Wine](/index.php/Diretrizes_de_pacotes_Wine "Diretrizes de pacotes Wine")

Esse documento cobre padrões e diretrizes na escrita de [PKGBUILDs](/index.php/PKGBUILD_(Portugu%C3%AAs) "PKGBUILD (Português)") para softwares [Python](/index.php/Python "Python").

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Nome do pacote](#Nome_do_pacote)
    *   [1.1 Arquitetura](#Arquitetura)
    *   [1.2 Fonte](#Fonte)
*   [2 Métodos de instalação](#Métodos_de_instalação)
    *   [2.1 distutils](#distutils)
    *   [2.2 setuptools](#setuptools)
    *   [2.3 pip](#pip)
    *   [2.4 Tradução 2to3 em tempo de compilação](#Tradução_2to3_em_tempo_de_compilação)
*   [3 Verificação](#Verificação)
*   [4 Dicas e truques](#Dicas_e_truques)
    *   [4.1 Usando site-packages](#Usando_site-packages)
    *   [4.2 Diretório de teste em site-package](#Diretório_de_teste_em_site-package)

## Nome do pacote

Para módulos de biblioteca do [Python 3](/index.php/Python#Python_3 "Python"), use `python-*nomemódulo*`. Também use o prefixo se o pacote fornece um programa fortemente atrelado ao ecossistema do Python (p. ex. *pip* or *tox*). Para outros aplicativos, use apenas o nome do programa.

O mesmo se aplica para Python 2, exceto que o prefixo (se necessário) é `python2-`.

**Nota:** O nome do pacote deve estar todo em minúsculo.

### Arquitetura

Veja [PKGBUILD (Português)#arch](/index.php/PKGBUILD_(Portugu%C3%AAs)#arch "PKGBUILD (Português)").

Um pacote Python que contenha extensões C usando a palavra-chave `ext_modules` no `setup.py` é dependente da arquitetura. Do contrário, muito provavelmente será independente desta.

### Fonte

As URLs de download vinculadas do site do PyPI incluem um hash imprevisível que precisa ser obtido no site do PyPI sempre que um pacote precisar ser atualizado. Isso os torna inadequados para uso em um PKGBUILD. PyPI [fornece](https://github.com/pypa/pypi-legacy/issues/438#issuecomment-226940730) um esquema estável alternativo: matriz [PKGBUILD (Português)#source](/index.php/PKGBUILD_(Portugu%C3%AAs)#source "PKGBUILD (Português)") `source=()` deve usar os seguintes modelos de URL:

	Pacote fonte

	`https://files.pythonhosted.org/packages/source/${_name::1}/$_name/$_name-$pkgver.tar.gz`

	Pacote wheel Python puro

	`https://files.pythonhosted.org/packages/py2.py3/${_name::1}/$_name/${_name/-/_}-$pkgver-py2.py3-none-any.whl` (Bilíngue compatível com Python 2 e Python 3):`https://files.pythonhosted.org/packages/py3/${_name::1}/$_name/${_name/-/_}-$pkgver-py3-none-any.whl` (Python 3 apenas)

	Note que o nome da distribuição pode conter traços, enquanto sua representação em um nome de arquivo wheel não pode (eles são convertidos em sublinhados).

	Pacote wheel específico para arquitetura

	neste exemplo para `source_x86_64=('...')`. Também `_py=cp38` pode ser usado para não repetir a versão do python:

	`https://files.pythonhosted.org/packages/$_py/${_name::1}/$_name/{_name/-/_}-$pkgver-$_py-${_py}m-manylinux1_x86_64.whl`

Note que uma variável personalizada `**$_name**` é usada em vez de `pkgname` já que nomes de pacotes python são geralmente prefixados com `python-`. Essa variável pode ser definida genericamente da seguinte forma:

```
_name=${pkgname#python-}

```

## Métodos de instalação

Os pacotes Python geralmente são instalados usando ferramentas específicas da linguagem, como [pip](https://pip.pypa.io/) ou [easy_install](https://setuptools.readthedocs.io/en/latest/easy_install.html), que são comparáveis aos gerenciadores de pacotes dedicados na medida em que foram projetados para buscar os arquivos fonte de um repositório online (geralmente [PyPI](https://pypi.org/), o Python Package Index) e rastrear o arquivos relevantes (para uma comparação detalhada entre os dois, veja [pip vs easy_install](https://packaging.python.org/pip_easy_install/#pip-vs-easy-install)).

No entanto, para gerenciar pacotes Python dentro de PKGBUILDs, o [distutils](http://docs.python.org/library/distutils.html) fornecido de forma padrão é a solução mais conveniente, pois usa o `setup.py` do pacote fonte baixado e instala facilmente arquivos no diretório `*$pkgdir*/usr/lib/python*<versão python>*/site-packages/*$pkgname*`.

### distutils

Um PKGBUILD de *distutils* é geralmente bem simples:

```
build() {
    *python* setup.py build
}

package() {
    *python* setup.py install --root="$pkgdir/" --optimize=1 --skip-build
}
```

sendo que:

*   *python* é substituído com o binário correto, `python` ou `python2`
*   `--root="$pkgdir/"` evita a tentativa de instalar diretamente no sistema hospedeiro em vez do arquivo de pacote, que resultaria em um erro de permissão
*   `--optimize=1` compila arquivos bytecode otimizados (`.pyo` para Python 2, `opt-1.pyc` para Python 3) de forma que eles possam ser rastreados pelo [pacman](/index.php/Pacman_(Portugu%C3%AAs) "Pacman (Português)").
*   `--skip-build` otimiza, evitando tentativas desnecessárias de reexecutar as etapas de compilação já executadas na função `build()`.

### setuptools

A cena de empacotamento de Python migrou em grande parte do *distutils* para o *setuptools*, que está ativamente desenvolvido e funciona como uma importação de substituição ao `setup.py`. A principal diferença para os empacotadores é que *setuptools* é empacotado separadamente do próprio Python e deve ser especificado como um `makedepends`:

```
makedepends=('python-setuptools')

```

Se o pacote resultante incluir executáveis que [importam o módulo `pkg_resources`](https://setuptools.readthedocs.io/en/latest/setuptools.html#automatic-script-creation), os *setuptools* devem ser adicionalmente especificados como `depends` das funções de `package_*()` divididas; alternativamente, se o PKGBUILD apenas instalar o pacote Python para uma única versão do Python, *setuptools* deve ser movido de `makedepends` para `depends`.

### pip

Se você precisar usar o *pip* (fornecido por [python-pip](https://www.archlinux.org/packages/?name=python-pip) e [python2-pip](https://www.archlinux.org/packages/?name=python2-pip)) para, por exemplo, instalar pacotes [wheel](https://github.com/pypa/wheel), lembre-se de passar as seguintes opções:

```
PIP_CONFIG_FILE=/dev/null pip install --isolated --root="$pkgdir" --ignore-installed --no-deps *.whl

```

*   `PIP_CONFIG_FILE=/dev/null` ignora `{/etc,~/.config}/pip.conf`, o qual pode estar anexando sinalizadores arbitrários ao **pip**.
*   `--isolated` ignora variáveis de ambiente (e, novamente, `{/etc,~/.config}/pip/pip.conf`) que, do contrário, poderia também estar anexando sinalizadores arbitrários ao **pip**.
*   `--ignore-installed` é necessário até [https://github.com/pypa/pip/issues/3063](https://github.com/pypa/pip/issues/3063) estar resolvido (do contrário, **pip** ignora a instalação na presença de uma instalação `--user` anterior).
*   `--no-deps` assegura que dependências não sejam empacotadas junto com pacote principal.

*pip* não sabe como gerar arquivos `.pyo` (veja [https://github.com/pypa/pip/issues/2209](https://github.com/pypa/pip/issues/2209)). Para gerá-los manualmente após *pip* ter instalado o módulo, execute:

```
python -O -m compileall "${pkgdir}/caminho/para/o/módulo"

```

**Atenção:** O uso de pacotes *pip* e/ou de wheel é desencorajado em favor dos pacotes fonte setuptools, e deve ser usado somente quando o último não é uma opção viável (por exemplo, pacotes que **somente** vêm com fontes de wheel e, portanto, não pode ser instalado usando setuptools).

### Tradução 2to3 em tempo de compilação

A maioria dos projetos em Python tem como alvo o Python 2 ou o Python 3, ou ambos usam camadas de compatibilidade como [six](https://pythonhosted.org/six/). No entanto, alguns usam a palavra-chave 2to3 reprovada em setuptools para converter heuristicamente o código-fonte do Python 2 para o Python 3 no momento da criação. Como resultado, os mesmos diretórios de origem não podem ser usados para construir os pacotes divididos do Python 2 e do Python 3.

Para pacotes que fazem isso, precisamos de uma função [prepare()](/index.php/Criando_pacotes#prepare() "Criando pacotes") que copie a fonte antes que ela seja construída. Em seguida, os pacotes do Python 2 e do Python 3 podem ser convertidos e construídos independentemente, sem se sobreporem uns aos outros.

```
makedepends=("python-setuptools" "python2-setuptools")

prepare() {
    cp -a foo-$pkgver{,-py2}
}

build() {
    cd "$srcdir/foo-$pkgver"
    python setup.py build

    cd "$srcdir/foo-$pkgver-py2"
    python2 setup.py build
}

package_python-foo() {
    depends=("python")
    cd "$srcdir/foo-$pkgver"
    python setup.py install --root="$pkgdir/" --optimize=1 --skip-build
}

package_python2-foo() {
    depends=("python2")
    cd "$srcdir/foo-$pkgver-py2"
    python2 setup.py install --root="$pkgdir/" --optimize=1 --skip-build
}
```

## Verificação

**Atenção:** Evite usar o `tox` para executar os *testsuites*, pois ele é projetado explicitamente para testar as configurações repetidas baixadas do PyPI enquanto `tox` está sendo executado, e não testa a versão que será instalado pelo pacote. Isso anula o propósito de ter uma função *check*.

A maioria dos projetos python que fornecem *testsuites* (que são conjunto ou coleção de testes) usam *nosetests* ou *pytest* para executar os testes com `test` no nome do arquivo ou diretório contendo a *testsuite*. Em geral, só executar `nosetests` ou `pytest` é o suficiente para executar a *testsuite*.

```
check(){
    cd "$srcdir/foo-$pkgver"

    # Para nosetests
    nosetests

    # Para pytest
    pytest
}

```

Se houver uma extensão C compilada, os testes precisam ser executados usando um `$PYTHONPATH`, que reflete a versão maior e menor do Python, para localizá-la e carregá-la.

```
check(){
  cd "$pkgname-$pkgver"
  local python_version=$(python -c 'import sys; print(".".join(map(str, sys.version_info[:2])))')
  # Para nosetests
  PYTHONPATH="$PWD/build/lib.linux-$CARCH-${python_version}" nosetests

  # Para pytest
  PYTHONPATH="$PWD/build/lib.linux-$CARCH-${python_version}" pytest
}
```

Alguns projetos fornecem pontos de entrada no `setup.py` para executar o teste. Isso funciona para `pytest` e `nosetests`.

```
check(){
    cd "$srcdir/foo-$pkgver"

    # para nosetests
    python setup.py nosetests

    # Para pytest - precisa de python-pytest-runner
    python setup.py pytest
}

```

## Dicas e truques

### Usando site-packages

Às vezes, durante a compilação, o teste ou a instalação, é necessário consultar o diretório `site-packages` do sistema. Para não codificar o diretório, use uma chamada para a versão Python do sistema para recuperar o caminho e armazená-lo em uma variável local:

```
check(){
  cd "$pkgname-$pkgver"
  local site_packages=$(python -c "import site; print(site.getsitepackages()[0])")
  ...
}
```

### Diretório de teste em site-package

Certifique-se de não instalar um diretório chamado apenas `tests` em `site-packages` (por exemplo, `/usr/lib/python2.7/site-packages/tests/`), pois ele facilmente entra em conflito com outros pacotes Python.