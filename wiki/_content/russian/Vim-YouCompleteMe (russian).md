**Состояние перевода:** На этой странице представлен перевод статьи [Vim/YouCompleteMe](/index.php/Vim/YouCompleteMe "Vim/YouCompleteMe"). Дата последней синхронизации: 23 июня 2018\. Вы можете [помочь](/index.php/ArchWiki_Translation_Team_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "ArchWiki Translation Team (Русский)") синхронизировать перевод, если в английской версии произошли [изменения](https://wiki.archlinux.org/index.php?title=Vim/YouCompleteMe&diff=0&oldid=509307).

[YouCompleteMe](https://github.com/Valloric/YouCompleteMe) (сокращённо YCM) - это плагин для автодополнения в [Vim](/index.php/Vim "Vim"). YCM поддерживает следующие языки:

*   C/C++/Objective-C/Objective-C++
*   Python
*   C#
*   Go
*   Rust
*   JavaScript
*   TypeScript
*   Другие языки (Java, Ruby, PHP и т.д.) посредством использования omnicompletion.

## Contents

*   [1 Установка](#.D0.A3.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B0)
*   [2 Настройка](#.D0.9D.D0.B0.D1.81.D1.82.D1.80.D0.BE.D0.B9.D0.BA.D0.B0)
    *   [2.1 C/C++](#C.2FC.2B.2B)
        *   [2.1.1 Структура файла настроек](#.D0.A1.D1.82.D1.80.D1.83.D0.BA.D1.82.D1.83.D1.80.D0.B0_.D1.84.D0.B0.D0.B9.D0.BB.D0.B0_.D0.BD.D0.B0.D1.81.D1.82.D1.80.D0.BE.D0.B5.D0.BA)
        *   [2.1.2 Дополнительное расположение файла конфигурации](#.D0.94.D0.BE.D0.BF.D0.BE.D0.BB.D0.BD.D0.B8.D1.82.D0.B5.D0.BB.D1.8C.D0.BD.D0.BE.D0.B5_.D1.80.D0.B0.D1.81.D0.BF.D0.BE.D0.BB.D0.BE.D0.B6.D0.B5.D0.BD.D0.B8.D0.B5_.D1.84.D0.B0.D0.B9.D0.BB.D0.B0_.D0.BA.D0.BE.D0.BD.D1.84.D0.B8.D0.B3.D1.83.D1.80.D0.B0.D1.86.D0.B8.D0.B8)
    *   [2.2 Java](#Java)
    *   [2.3 C#](#C.23)
*   [3 Устранение неполадок](#.D0.A3.D1.81.D1.82.D1.80.D0.B0.D0.BD.D0.B5.D0.BD.D0.B8.D0.B5_.D0.BD.D0.B5.D0.BF.D0.BE.D0.BB.D0.B0.D0.B4.D0.BE.D0.BA)
    *   [3.1 E764: Option 'omnifunc' is not set](#E764:_Option_.27omnifunc.27_is_not_set)
    *   [3.2 Нет автодополнения в Java-файлах](#.D0.9D.D0.B5.D1.82_.D0.B0.D0.B2.D1.82.D0.BE.D0.B4.D0.BE.D0.BF.D0.BE.D0.BB.D0.BD.D0.B5.D0.BD.D0.B8.D1.8F_.D0.B2_Java-.D1.84.D0.B0.D0.B9.D0.BB.D0.B0.D1.85)
    *   [3.3 URLError: <urlopen error [Errno 111] Connection refused>](#URLError:_.3Curlopen_error_.5BErrno_111.5D_Connection_refused.3E)
    *   [3.4 RuntimeError: Error starting OmniSharp server: no solutionfile found](#RuntimeError:_Error_starting_OmniSharp_server:_no_solutionfile_found)
*   [4 Смотрите также](#.D0.A1.D0.BC.D0.BE.D1.82.D1.80.D0.B8.D1.82.D0.B5_.D1.82.D0.B0.D0.BA.D0.B6.D0.B5)

## Установка

Установите пакет [vim-youcompleteme-git](https://aur.archlinux.org/packages/vim-youcompleteme-git/) из [AUR](/index.php/AUR "AUR"). Для ручной установки Вы можете воспользоваться [инструкцией](https://github.com/Valloric/YouCompleteMe#full-installation-guide).

Установка может прерваться при проверке PGP-подписей, когда устанавливается пакет [ncurses5-compat-libs](https://aur.archlinux.org/packages/ncurses5-compat-libs/). Для исправления этой ошибки введите в терминале:

```
$ gpg --keyserver keys.gnupg.net --recv-keys 702353E0F7E48EDB

```

## Настройка

### C/C++

YCM использует скрипт `.ycm_extra_conf.py` для установки параметров проекта, необходимых для автодополнения и проверки синтаксиса. Ниже приводится краткое описание основной конфигурации. Подробности и расширенные параметры смотрите в [документации](https://github.com/Valloric/YouCompleteMe#options).

#### Структура файла настроек

Пример файла `.ycm_extra_conf.py` может быть найден [здесь](https://github.com/Valloric/ycmd/blob/master/cpp/ycm/.ycm_extra_conf.py). Вы должны сохранить копию этого файла в папке проекта и настроить его в соответствие своим потребностям. Наиболее важными параметрами (в минимальной конфигурации) являются опции `-x` и `--std`, которые соответственно указывают язык, используемый в проекте, и следуемый [стандарт](https://en.wikipedia.org/wiki/ISO/IEC_JTC_1/SC_22 "wikipedia:ISO/IEC JTC 1/SC 22"). `-x` может быть установлен для `C` и `C++`, а общими значениями для `--std` являются `--std=c89`, `--std=c99`, `--std=c11`, `--std=c14` и их соответствующие версии в C++. Стандартный параметр определяет предупреждения и ошибки при синтаксической проверке (например, строка, закомментированная с помощью `//` будет отмечена как неразрешенная в C89, но не в следующих версиях стандарта. Сторонний скрипт и vim-плагин для автоматического создания `.ycm_extra_conf.py` доступен [здесь](https://github.com/rdnetto/YCM-Generator).

#### Дополнительное расположение файла конфигурации

YCM выполняет поиск файла `.ycm_extra_conf.py` в каталоге исходного файла и в родительских директориях. Если файл конфигурации не найден, то функции YCM не будут доступны. Глобальный файл настроек, используемый, когда локальный файл не был найден, может быть выбран путём добавления в `~/.vimrc` следующих строк:

 `~/.vimrc`  `let g:ycm_global_ycm_extra_conf = '/путь/до/файла'` 

Так как `.ycm_extra_conf.py` является python-скриптом, то в целях безопасности каждый раз будет запрашиваться разрешение на его выполнение. Такое поведение можно отключить, добавив следующие строки в `~/.vimrc`:

 `~/.vimrc`  `let g:ycm_confirm_extra_conf = 0` 

### Java

Для автодополнения Java должен присутствовать файл проекта активен сервер Eclim.

1.  Установите [eclim](https://aur.archlinux.org/packages/eclim/) или [eclim-git](https://aur.archlinux.org/packages/eclim-git/)
2.  Добавьте следующие строки в `~/.vimrc`: `~/.vimrc`  `let g:EclimCompletionMethod = 'omnifunc'` 
3.  Запустите Eclimd в отдельном терминале: `$ /usr/lib/eclipse/plugins/org.eclim_$pkgver/bin/eclimd` 
4.  Создайте файл `.project` в той же директории, где находятся Ваши Java-файлы и добавьте в этот файл следующее: `.project` 
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

Чтобы выполнить только текущий файл, выполните:

```
:Java %

```

Список доступных команд можно найти [здесь](http://eclim.org/cheatsheet.html).

### C#

**Примечание:** Для автодополнения C# "из коробки" достаточно создать пустой `.sln` файл в текущем или родительском каталоге. Далее описывается, как вручную создать полноценный рабочий проект C#

Простой способ создать проект - установить [monodevelop-stable](https://aur.archlinux.org/packages/monodevelop-stable/). В остальной части раздела объясняется, как вручную создать проект C#, который также может быть из терминала с помощью `xbuild`.

Сперва создайте `.sln` файл. Части кода, выделенные ***жирным шрифтом*** замените на свои имена.

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

Затем создайте директорию `***PROJECT***` и там создайте файл с именем `***PROJECT***.csproj`

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

Поместите свои C#-файлы в созданную директорию `PROJECT` и не забудьте вручную добавить их в конце файла `PROJECT/PROJECT.csproj`.

Теперь YCM должен работать для файлов в этом каталоге, и вы можете создать проект. Чтобы скомпилировать проект из Vim, выполните:

```
:!xbuild

```

## Устранение неполадок

**Примечание:** Помните, что для создания списка завершения строк может потребоваться некоторое время для YCM

Для диагностики доступны следующие команды:

*   `:messages` - показывает предыдущие сообщения об ошибках в Vim
*   `:YcmDiags`
*   `:YcmDebugInfo`

### E764: Option 'omnifunc' is not set

Если это происходит, то Вы забыли поместить следующие строки в `~/.vimrc`:

 `~/.vimrc`  `let g:EclimCompletionMethod = 'omnifunc'` 

### Нет автодополнения в Java-файлах

Убедитесь, что демон `eclimd` активен:

```
$ ps -ax|grep eclimd

```

и что у Вас есть файлы проекта.

### URLError: <urlopen error [Errno 111] Connection refused>

Эта ошибка появляется, когда у Вас нет `.sln` файла.

### RuntimeError: Error starting OmniSharp server: no solutionfile found

Аналогично.

## Смотрите также

*   [Страница на Github](https://github.com/Valloric/YouCompleteMe)
*   [Домашняя страница проекта](http://valloric.github.io/YouCompleteMe/)