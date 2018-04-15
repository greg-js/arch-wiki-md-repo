**[Package creation guidelines](/index.php/Creating_packages "Creating packages")**

* * *

[CLR](/index.php/CLR_package_guidelines "CLR package guidelines") – [Cross](/index.php/Cross-compiling_tools_package_guidelines "Cross-compiling tools package guidelines") – [Eclipse](/index.php/Eclipse_plugin_package_guidelines "Eclipse plugin package guidelines") – [Free Pascal](/index.php/Free_Pascal_package_guidelines "Free Pascal package guidelines") – [GNOME](/index.php/GNOME_package_guidelines "GNOME package guidelines") – [Go](/index.php/Go_package_guidelines "Go package guidelines") – [Haskell](/index.php/Haskell_package_guidelines "Haskell package guidelines") – [Java](/index.php/Java_package_guidelines "Java package guidelines") – [KDE](/index.php/KDE_package_guidelines "KDE package guidelines") – [Kernel](/index.php/Kernel_module_package_guidelines "Kernel module package guidelines") – [Lisp](/index.php/Lisp_package_guidelines "Lisp package guidelines") – [MinGW](/index.php/MinGW_package_guidelines "MinGW package guidelines") – [Node.js](/index.php/Node.js_package_guidelines "Node.js package guidelines") – [Nonfree](/index.php/Nonfree_applications_package_guidelines "Nonfree applications package guidelines") – [OCaml](/index.php/OCaml_package_guidelines "OCaml package guidelines") – [Perl](/index.php/Perl_package_guidelines "Perl package guidelines") – [PHP](/index.php/PHP_package_guidelines "PHP package guidelines") – [Python](/index.php/Python_package_guidelines "Python package guidelines") – [Ruby](/index.php/Ruby_Gem_package_guidelines "Ruby Gem package guidelines") – [VCS](/index.php/VCS_package_guidelines "VCS package guidelines") – [Web](/index.php/Web_application_package_guidelines "Web application package guidelines") – [Wine](/index.php/Wine_package_guidelines "Wine package guidelines")

Este documento cobre a criação de [PKGBUILDs](/index.php/PKGBUILD_(Portugu%C3%AAs) "PKGBUILD (Português)") para bibliotecas PHP. Este documento tem como público-alvo aqueles que desejam ser empacotadores de bibliotecas PHP. Para aplicativos da Web PHP, consulte [Diretrizes de pacotes de aplicativos da Web](/index.php/Diretrizes_de_pacotes_de_aplicativos_da_Web "Diretrizes de pacotes de aplicativos da Web").

### Nomes de pacotes

Para módulos, o nome do pacote deve começar com `php-` e o resto do nome deve ser construído a partir do nome da biblioteca, convertendo-o em palavras minúsculas e separadas com hífenes. Por exemplo, o nome do pacote correspondente a `File iterator` será `php-file-iterator`.

### Colocação de arquivos no pacote

Pacotes PHP devem instalar arquivos em `/usr/share/php/`. Esse caminho deve estar na diretiva include_path ou open_basedir do php.ini para poder incluir arquivos de bibliotecas em aplicativos da Web PHP.

### Arquitetura

Na maioria dos casos, o vetor `arch` deve conter `'any'` porque a maioria dos pacotes PHP são independentes de arquitetura.