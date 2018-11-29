**Состояние перевода:** На этой странице представлен перевод статьи [Vim/YouCompleteMe](/index.php/Vim/YouCompleteMe "Vim/YouCompleteMe"). Дата последней синхронизации: 28 ноября 2018\. Вы можете [помочь](/index.php/ArchWiki_Translation_Team_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "ArchWiki Translation Team (Русский)") синхронизировать перевод, если в английской версии произошли [изменения](https://wiki.archlinux.org/index.php?title=Vim/YouCompleteMe&diff=0&oldid=557713).

[YouCompleteMe](https://github.com/Valloric/YouCompleteMe) (сокращённо YCM) — это плагин для автодополнения в [Vim (Русский)](/index.php/Vim_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Vim (Русский)"). YCM поддерживает следующие языки программирования:

*   C/C++/Objective-C/Objective-C++
*   Python
*   C#
*   Go
*   Rust
*   JavaScript
*   TypeScript
*   Другие языки (Java, Ruby, PHP и т.д.) посредством использования omnicompletion.

## Contents

*   [1 Установка](#Установка)
*   [2 Настройка](#Настройка)
    *   [2.1 C/C++](#C/C++)
        *   [2.1.1 Структура файла конфигурации](#Структура_файла_конфигурации)
        *   [2.1.2 Расположение файла конфигурации](#Расположение_файла_конфигурации)
    *   [2.2 Java](#Java)
    *   [2.3 C#](#C#)
*   [3 Решение проблем](#Решение_проблем)
    *   [3.1 E764: Option 'omnifunc' is not set](#E764:_Option_'omnifunc'_is_not_set)
    *   [3.2 Нет автодополнения в Java-файлах](#Нет_автодополнения_в_Java-файлах)
    *   [3.3 URLError: <urlopen error [Errno 111] Connection refused>](#URLError:_<urlopen_error_[Errno_111]_Connection_refused>)
    *   [3.4 RuntimeError: Error starting OmniSharp server: no solutionfile found](#RuntimeError:_Error_starting_OmniSharp_server:_no_solutionfile_found)
*   [4 Смотрите также](#Смотрите_также)

## Установка

Установите пакет [vim-youcompleteme-git](https://aur.archlinux.org/packages/vim-youcompleteme-git/) из [AUR (Русский)](/index.php/AUR_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "AUR (Русский)"). Для ручной установки Вы можете воспользоваться [официальной инструкцией](https://github.com/Valloric/YouCompleteMe#full-installation-guide).

## Настройка

### C/C++

YCM использует скрипт `.ycm_extra_conf.py` для установки параметров проекта, необходимых для автодополнения и проверки синтаксиса. Ниже приводится краткое описание основной конфигурации. Подробности и расширенные параметры смотрите в [официальной документации](https://github.com/Valloric/YouCompleteMe#options).

#### Структура файла конфигурации

Пример файла `.ycm_extra_conf.py` может быть найден в [[1]](https://github.com/Valloric/ycmd/blob/master/.ycm_extra_conf.py). Вы должны сохранить копию этого файла в папке проекта и настроить его в соответствие своим потребностям.

Наиболее важными параметрами (в минимальной конфигурации) являются опции `-x` и `--std`, которые соответственно указывают язык, используемый в проекте, и следуемый [стандарт](https://en.wikipedia.org/wiki/ISO/IEC_JTC_1/SC_22 "wikipedia:ISO/IEC JTC 1/SC 22"). `-x` может быть установлен для `C` и `C++`, а общими значениями для `--std` являются `--std=c89`, `--std=c99`, `--std=c11`, `--std=c14` и их соответствующие версии в C++. Стандартный параметр определяет предупреждения и ошибки при синтаксической проверке (например, строка, закомментированная с помощью `//` будет отмечена как неразрешенная в C89, но не в следующих версиях стандарта.

Сторонний скрипт и vim-плагин для автоматического создания `.ycm_extra_conf.py` доступен [в данном репозитории](https://github.com/rdnetto/YCM-Generator).

#### Расположение файла конфигурации

YCM выполняет поиск файла `.ycm_extra_conf.py` в каталоге исходного файла и в его родительских директориях. Если файл конфигурации не найден, то функции YCM не будут доступны. Глобальный файл настроек, используемый, когда локальный файл не был найден, может быть выбран путём добавления в `~/.vimrc` следующих строк:

 `~/.vimrc`  `let g:ycm_global_ycm_extra_conf = '/путь/до/файла'` 

Так как `.ycm_extra_conf.py` является python-скриптом, то в целях безопасности каждый раз будет запрашиваться разрешение на его выполнение. Такое поведение можно отключить, добавив следующие строки в `~/.vimrc`:

 `~/.vimrc`  `let g:ycm_confirm_extra_conf = 0` 

Для более безопасного решения, при включённом подтверждении можно определить белый/чёрный список с помощью шаблонов, назначаемых в переменной `ycm_extra_conf_globlist`. Файл попадает в чёрный список, если соответствует шаблону, начинающемуся с `!`. Если файл соответствует шаблону не начинающемуся с восклицательного знака, то он попадает в белый список. Запрос на подтверждение выполнения файла конфигурации возникает если файл не соответствует ни одному из шаблонов. Правила (шаблоны) сопоставляются в порядке очереди и применяется первое совпадение. Возможно использование следующих масок в шаблонах:

*   * — любые символы
*   ? — любой один символ
*   [последовательность] — любой символ в последовательности
*   [!последовательность] — любой символ не входящий в последовательность

Пример:

 `~/.vimrc`  `let g:ycm_extra_conf_globlist = ['~/dev/*','!~/*']` 

Любой файл в каталоге `~/dev` попадает в белый список, любой файл в каталоге `~/` попадает в чёрный список. И, согласно очереди приоритетности шаблонов, любой файл в каталоге `~/`, кроме каталога `~/dev`, попадёт в чёрный список.

### Java

Для автодополнения Java должен присутствовать файл проекта и активен headless-сервер Eclim.

1.  Установите [eclim](https://aur.archlinux.org/packages/eclim/) или [eclim-git](https://aur.archlinux.org/packages/eclim-git/) из [AUR (Русский)](/index.php/AUR_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "AUR (Русский)").
2.  Добавьте следующие строки в ваш `~/.vimrc`: `~/.vimrc`  `let g:EclimCompletionMethod = 'omnifunc'` 
3.  Запустите скрипт `eclimd` в отдельном терминале: `$ /usr/lib/eclipse/plugins/org.eclim_$pkgver/bin/eclimd` 
4.  Создайте файл `.project` в той же директории, где находятся Ваши Java-файлы и добавьте в этот файл следующее содержимое: `.project` 
    ```
    <projectDescription>
        <name>*PROJECTNAME*</name>
    </projectDescription>

    ```

5.  Откройте Ваш Java-файл в Vim и выполните: `:ProjectCreate . -n java` 

Для компиляции проекта выполните:

```
:ProjectBuild

```

Для запуска проекта выполните:

```
:Java

```

Чтобы запустить только текущий файл, выполните:

```
:Java %

```

Список доступных команд можно найти [здесь](http://eclim.org/cheatsheet.html).

### C#

**Примечание:** Для автодополнения C# "из коробки", достаточно создать пустой файл `.sln` в текущем или родительском каталоге. Далее описывается, как вручную создать полноценный рабочий проект C#.

Самый простой способ создать проект — установить [monodevelop-stable](https://aur.archlinux.org/packages/monodevelop-stable/). В остальной части раздела объясняется, как вручную создать проект C#, который также может быть создан из командной строки с помощью `xbuild`.

Сперва создайте файл `.sln`. Части кода, выделенные ***полужирным курсивом***, замените на свои названия.

 `***SOLUTION***.sln` 
```

Microsoft Visual Studio Solution File, Format Version 11.00
# Visual Studio 2010
Project("{00000000-0000-0000-0000-000000000000}") = "***PROJECT***", "***PROJECT***\***PROJECT***.csproj", "{11111111-1111-1111-1111-111111111111}"
EndProject
EndProject
Global
	GlobalSection(SolutionConfigurationPlatforms) = preSolution
		Debug|x86 = Debug|x86
		Release|x86 = Release|x86
	EndGlobalSection
	GlobalSection(ProjectConfigurationPlatforms) = postSolution
		{11111111-1111-1111-1111-111111111111}.Debug|x86.ActiveCfg = Debug|x86
		{11111111-1111-1111-1111-111111111111}.Debug|x86.Build.0 = Debug|x86
		{11111111-1111-1111-1111-111111111111}.Release|x86.ActiveCfg = Release|x86
		{11111111-1111-1111-1111-111111111111}.Release|x86.Build.0 = Release|x86
	EndGlobalSection
EndGlobal
```

Затем создайте директорию `PROJECT` и там создайте файл с названием `PROJECT.csproj`:

 `***PROJECT***/***PROJECT***.csproj` 
```
<?xml version="1.0" encoding="utf-8"?>
<Project DefaultTargets="Build" ToolsVersion="4.0" xmlns="http://schemas.microsoft.com/developer/msbuild/2003">
  <PropertyGroup>
    <Configuration Condition=" '$(Configuration)' == '' ">Debug</Configuration>
    <Platform Condition=" '$(Platform)' == '' ">x86</Platform>
    <ProductVersion>10.0.0</ProductVersion>
    <SchemaVersion>2.0</SchemaVersion>
    <ProjectGuid>{11111111-1111-1111-1111-111111111111}</ProjectGuid>
    <OutputType>Exe</OutputType>
    <RootNamespace>***PROJECT***</RootNamespace>
    <AssemblyName>***PROJECT***</AssemblyName>
  </PropertyGroup>
  <PropertyGroup Condition=" '$(Configuration)|$(Platform)' == 'Debug|x86' ">
    <DebugSymbols>true</DebugSymbols>
    <DebugType>full</DebugType>
    <Optimize>false</Optimize>
    <OutputPath>bin\Debug</OutputPath>
    <DefineConstants>DEBUG;</DefineConstants>
    <ErrorReport>prompt</ErrorReport>
    <WarningLevel>4</WarningLevel>
    <ConsolePause>false</ConsolePause>
    <PlatformTarget>x86</PlatformTarget>
  </PropertyGroup>
  <PropertyGroup Condition=" '$(Configuration)|$(Platform)' == 'Release|x86' ">
    <DebugType>full</DebugType>
    <Optimize>true</Optimize>
    <OutputPath>bin\Release</OutputPath>
    <ErrorReport>prompt</ErrorReport>
    <WarningLevel>4</WarningLevel>
    <ConsolePause>false</ConsolePause>
    <PlatformTarget>x86</PlatformTarget>
  </PropertyGroup>
  <Import Project="$(MSBuildBinPath)\Microsoft.CSharp.targets" />
  <ItemGroup>
    <Compile Include="***HelloWorld.cs***" />
    <Compile Include="***CSharpFile1.cs***" />
    <Compile Include="***CSharpFile2.cs***" />
  </ItemGroup>
</Project>
```

Поместите свои C#-файлы в директорию `PROJECT` и не забудьте вручную добавить их в конец файла `PROJECT/PROJECT.csproj`.

Теперь YouCompleteMe должен работать для файлов C# в этом каталоге и вы можете собирать проект. Чтобы скомпилировать проект из Vim, выполните следующую команду:

```
:!xbuild

```

## Решение проблем

Помните, что для создания списка завершения строк YouCompleteMe может потребоваться некоторое время.

Для диагностики доступны следующие команды:

*   `:messages` — показывает предыдущие сообщения об ошибках в Vim
*   `:YcmDiags`
*   `:YcmDebugInfo`

### E764: Option 'omnifunc' is not set

Если это происходит, то Вы забыли поместить следующие строки в `~/.vimrc`:

 `~/.vimrc`  `let g:EclimCompletionMethod = 'omnifunc'` 

### Нет автодополнения в Java-файлах

Убедитесь, что служба `eclimd` запущена:

```
$ ps -ax|grep eclimd

```

и что у Вас есть файлы проекта.

### URLError: <urlopen error [Errno 111] Connection refused>

Эта ошибка появляется, когда у Вас нет файла `.sln` в текущей или родительской директориях.

### RuntimeError: Error starting OmniSharp server: no solutionfile found

Аналогично.

## Смотрите также

*   [Страница на Github](https://github.com/Valloric/YouCompleteMe)
*   [Домашняя страница проекта](http://valloric.github.io/YouCompleteMe/)