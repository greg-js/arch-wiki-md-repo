**[Package creation guidelines](/index.php/Creating_packages "Creating packages")**

* * *

[CLR](/index.php/CLR_package_guidelines "CLR package guidelines") – [Cross](/index.php/Cross-compiling_tools_package_guidelines "Cross-compiling tools package guidelines") – [Eclipse](/index.php/Eclipse_plugin_package_guidelines "Eclipse plugin package guidelines") – [Free Pascal](/index.php/Free_Pascal_package_guidelines "Free Pascal package guidelines") – [GNOME](/index.php/GNOME_package_guidelines "GNOME package guidelines") – [Go](/index.php/Go_package_guidelines "Go package guidelines") – [Haskell](/index.php/Haskell_package_guidelines "Haskell package guidelines") – [Java](/index.php/Java_package_guidelines "Java package guidelines") – [KDE](/index.php/KDE_package_guidelines "KDE package guidelines") – [Kernel](/index.php/Kernel_module_package_guidelines "Kernel module package guidelines") – [Lisp](/index.php/Lisp_package_guidelines "Lisp package guidelines") – [MinGW](/index.php/MinGW_package_guidelines "MinGW package guidelines") – [Node.js](/index.php/Node.js_package_guidelines "Node.js package guidelines") – [Nonfree](/index.php/Nonfree_applications_package_guidelines "Nonfree applications package guidelines") – [OCaml](/index.php/OCaml_package_guidelines "OCaml package guidelines") – [Perl](/index.php/Perl_package_guidelines "Perl package guidelines") – [PHP](/index.php/PHP_package_guidelines "PHP package guidelines") – [Python](/index.php/Python_package_guidelines "Python package guidelines") – [Ruby](/index.php/Ruby_Gem_package_guidelines "Ruby Gem package guidelines") – [VCS](/index.php/VCS_package_guidelines "VCS package guidelines") – [Web](/index.php/Web_application_package_guidelines "Web application package guidelines") – [Wine](/index.php/Wine_package_guidelines "Wine package guidelines")

Esse documento cobre padrões e diretrizes na escrita de [PKGBUILDs](/index.php/PKGBUILD_(Portugu%C3%AAs) "PKGBUILD (Português)") para softwares [Python](/index.php/Python "Python").

## Contents

*   [1 Nome do pacote](#Nome_do_pacote)
*   [2 Métodos de instalação](#M.C3.A9todos_de_instala.C3.A7.C3.A3o)
    *   [2.1 distutils](#distutils)
    *   [2.2 setuptools](#setuptools)
    *   [2.3 pip](#pip)
*   [3 Notas](#Notas)
    *   [3.1 URLs de download do PyPI](#URLs_de_download_do_PyPI)

## Nome do pacote

Para módulos de [Python 3](/index.php/Python#Python_3 "Python"), use a sistemática de nome `python-*nomemódulo*`; se o pacote é para [Python 2](/index.php/Python#Python_2 "Python"), use o prefixo `python2-`.

Se você precisar adicionar um pacote versionado, use `python-*nomemódulo*-*versão*` (ex.: `python-colorama-0.2.5`). Então, uma dependência python `colorama==0.2.5` vai se tornar em um pacote Arch `python-colorama-0.2.5`.

## Métodos de instalação

Os pacotes Python geralmente são instalados usando ferramentas específicas da linguagem, como [pip](https://pip.pypa.io/) ou [easy_install](https://setuptools.readthedocs.io/en/latest/easy_install.html), que são comparáveis aos gerenciadores de pacotes dedicados na medida em que foram projetados para buscar os arquivos fonte de um repositório online (geralmente [PyPI](https://pypi.python.org/), o Python Package Index) e rastrear o arquivos relevantes (para uma comparação detalhada entre os dois, veja [pip vs easy_install](https://packaging.python.org/pip_easy_install/#pip-vs-easy-install)).

No entanto, para gerenciar pacotes Python dentro de PKGBUILDs, o [distutils](http://docs.python.org/library/distutils.html) fornecido de forma padrão é a solução mais conveniente, pois usa o `setup.py` do pacote fonte baixado e instala facilmente arquivos no diretório `*$pkgdir*/usr/lib/python*<versão python>*/site-packages/*$pkgname*`.

### distutils

Um exemplo de PKGBUILD com *distutils* pode ser encontrado [aqui](https://projects.archlinux.org/abs.git/tree/prototypes/PKGBUILD-python.proto). Ele segue a forma:

```
python setup.py install --root="$pkgdir/" --optimize=1

```

sendo que:

*   python é substituído com o binário correto, `python` ou `python2`
*   `--root="$pkgdir/"` evita a tentativa de instalar diretamente no sistema hospedeiro em vez do arquivo de pacote, que resultaria em um erro de permissão
*   `--optimize=1` compila arquivos `.pyo` de forma que eles possam ser rastreados pelo [pacman](/index.php/Pacman_(Portugu%C3%AAs) "Pacman (Português)").

### setuptools

A cena de empacotamento de Python migrou em grande parte do *distutils* para o *setuptools*, que está ativamente desenvolvido e funciona como uma importação de substituição ao `setup.py`. A principal diferença para os empacotadores é que *setuptools* é empacotado separadamente do próprio Python e deve ser especificado como um `makedepends`.

Se o pacote resultante incluir executáveis que [importam o módulo `pkg_resources`](https://setuptools.readthedocs.io/en/latest/setuptools.html#automatic-script-creation), os *setuptools* devem ser adicionalmente especificados como `depends` das funções de `package_*()` divididas; alternativamente, se o PKGBUILD apenas instalar o pacote Python para uma única versão do Python, *setuptools* deve ser movido de `makedepends` para `depends`.

### pip

Se você precisar usar o *pip* (fornecido por [python-pip](https://www.archlinux.org/packages/?name=python-pip) e [python2-pip](https://www.archlinux.org/packages/?name=python2-pip)) para, por exemplo, instalar pacotes [wheel](https://bitbucket.org/pypa/wheel/), lembre-se de passar as seguintes opções:

```
PIP_CONFIG_FILE=/dev/null pip install --isolated --root="$pkgdir" --ignore-installed --no-deps *.whl

```

*   `PIP_CONFIG_FILE=/dev/null` ignora `{/etc,~/.config}/pip.conf`, o qual pode estar anexando sinalizadores arbitrários ao **pip**.
*   `--isolated` ignora variáveis de ambiente (e, novamente, `{/etc,~/.config}/pip/pip.conf`) que, do contrário, poderia também estar anexando sinalizadores arbitrários ao **pip**.
*   `--ignore-installed` é necessário até [https://github.com/pypa/pip/issues/3063](https://github.com/pypa/pip/issues/3063) estar resolvido (do contrário, **pip** ignora a instalação na presença de uma instalação `--user` anterior).
*   `--no-deps` assegura que dependências não sejam empacotadas junto com pacote principal.

*pip* não sabe como gerar arquivos `.pyo` (veja [https://github.com/pypa/pip/issues/2209](https://github.com/pypa/pip/issues/2209)). Para gerá-los manualmente após *pip* ter instalado o módulo, execute:

```
python -O -m compileall "${pkgdir}/caminho/para/o/módulo

```

## Notas

Na maioria dos casos, você deve colocar `any` no vetor `arch`, já que a maioria dos pacotes Python são independentes da arquitetura.

Não instale um diretório chamado apenas `tests`, pois ele facilmente entra em conflito com outros pacotes Python (por exemplo, `/usr/lib/python2.7/site-packages/tests/`).

### URLs de download do PyPI

URL PyPI na forma `https://pypi.python.org/packages/source/${_name:0:1}/${_name}/${_name}-${pkgver}.tar.gz` foram abandonados silenciosamente para novas versões de pacotes no curso de 2016, substituídos por um esquema usando um hash impredizível que precisa ser obtido do site do PYPI toda vez que um pacote precisa ser atualizado[[1]](https://github.com/pypa/pypi-legacy/issues/438#issuecomment-226940764).

Como os empacotadores *downstream* relataram seus problemas aos mantenedores do PyPI[[2]](https://github.com/pypa/pypi-legacy/issues/438), um novo esquema estável foi fornecido[[3]](https://github.com/pypa/pypi-legacy/issues/438#issuecomment-226940730): [PKGBUILD (Português)#source](/index.php/PKGBUILD_(Portugu%C3%AAs)#source "PKGBUILD (Português)") o vetor `source=()` deve agora usar os modelos de URL a seguir.

Note que uma variável `$_name` personalizada é usada em vez de `$pkgname` já que pacotes python são geralmente chamados `python-$_name`.

	Pacote fonte

	`https://files.pythonhosted.org/packages/source/${_name::1}/${_name}/${_name}-${pkgver}.tar.gz`

	Pacote wheel bilingual (compatível com Python 2 e Python 3)

	`https://files.pythonhosted.org/packages/py2.py3/${_name::1}/$_name/$_name-$pkgver-$_name-$pkgver-py2.py3-none-any.whl`

	Pacote wheel específico para arquitetura

	neste exemplo para `source_x86_64=('...')`. Também `_py=py36` pode ser usado para não repetir a versão do python:

	`https://files.pythonhosted.org/packages/$_py/${_name::1}/$_name/$_name-$pkgver-$_py-${_py}m-manylinux1_x86_64.whl`