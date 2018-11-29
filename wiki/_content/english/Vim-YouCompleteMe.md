[YouCompleteMe](https://github.com/Valloric/YouCompleteMe) (shortened as YCM) is a code-completion engine for [Vim](/index.php/Vim "Vim"). It supports the following languages:

*   C/C++/Objective-C/Objective-C++
*   Python
*   C#
*   Go
*   Rust
*   JavaScript
*   TypeScript
*   Other languages (Java, Ruby, PHP etc.) through the use of omnicompletion system

## Contents

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
    *   [2.1 C/C++](#C/C++)
        *   [2.1.1 Extra conf structure](#Extra_conf_structure)
        *   [2.1.2 Extra conf location](#Extra_conf_location)
    *   [2.2 Java](#Java)
    *   [2.3 C#](#C#)
*   [3 Troubleshooting](#Troubleshooting)
    *   [3.1 E764: Option 'omnifunc' is not set](#E764:_Option_'omnifunc'_is_not_set)
    *   [3.2 No completion in Java files](#No_completion_in_Java_files)
    *   [3.3 URLError: <urlopen error [Errno 111] Connection refused>](#URLError:_<urlopen_error_[Errno_111]_Connection_refused>)
    *   [3.4 RuntimeError: Error starting OmniSharp server: no solutionfile found](#RuntimeError:_Error_starting_OmniSharp_server:_no_solutionfile_found)
*   [4 See also](#See_also)

## Installation

Install [vim-youcompleteme-git](https://aur.archlinux.org/packages/vim-youcompleteme-git/) package from [AUR](/index.php/AUR "AUR"). For an alternative manual way of installing YouCompleteMe see [upstream instructions](https://github.com/Valloric/YouCompleteMe#full-installation-guide).

## Configuration

### C/C++

YCM uses a python script called `.ycm_extra_conf.py` to set project wide settings, needed to provide completion and syntax check. A brief introduction to essential configuration follows, for details and advanced options see the [upstream documentation](https://github.com/Valloric/YouCompleteMe#options).

#### Extra conf structure

A sample `.ycm_extra_conf.py` may be found in [[1]](https://github.com/Valloric/ycmd/blob/master/.ycm_extra_conf.py). You should save a copy of this file in your project folder and customize it with adequate settings for your source files.

The most important settings (which usually suffices for a minimal configuration) are the `-x` and `--std` options, which respectively tells the syntax checker the language used in the project and the [standard](https://en.wikipedia.org/wiki/ISO/IEC_JTC_1/SC_22 "wikipedia:ISO/IEC JTC 1/SC 22") followed. The `-x` value may be set to `c` or `c++`, while common values for the `--std` are `--std=c89`, `--std=c99`, `--std=c11`, `--std=c14` and their respective c++ version. The standard parameter will determine the warning and the errors in the syntax check (e.g., a line commented with `//` will be marked as unallowed in C89, but not under following versions of the standard).

A third party script and vim plugin for the automatic generation of the `.ycm_extra_conf.py` is available on [this repo](https://github.com/rdnetto/YCM-Generator).

#### Extra conf location

The program searches for the `.ycm_extra_conf.py` file on startup in the current source file directory and in its parent folders. If the file is not found, YCM features are not available. A global file (used as fallback when a local extra conf file is not found) may be set adding the following to `~/.vimrc`:

 `~/.vimrc`  `let g:ycm_global_ycm_extra_conf = '/path/to/the/file'` 

Being the extra conf file a python script, when a file is found a confirmation is asked for security reason before to load it. This behaviour may be disabled adding the following to `~/.vimrc`:

 `~/.vimrc`  `let g:ycm_confirm_extra_conf = 0` 

For a less unsecure solution, when the confirmation is enabled an extra conf file blacklist/whitelist may be set assigning a list of patterns to the `ycm_extra_conf_globlist` variable. A file matching one pattern is blacklisted if the pattern begins with `!`, whitelisted otherwise, confirmation is asked if the file does not match any pattern. Rule precedence is determined by the order, and the first match is applied. Some glob pattern rules are available:

*   * matches everything
*   ? matches any single character
*   [seq] matches any character in seq
*   [!seq] matches any char not in seq

In example, with the following setting

 `~/.vimrc`  `let g:ycm_extra_conf_globlist = ['~/dev/*','!~/*']` 

any file in `~/dev` will be whitelisted, any in `~/` will be blacklisted, and due to order precedence any file in `~/` excepted the `~/dev` folder will be blacklisted.

### Java

For Java completion, a project file should be present and Eclim headless server must be running.

1.  Install [eclim](https://aur.archlinux.org/packages/eclim/) or [eclim-git](https://aur.archlinux.org/packages/eclim-git/) from [AUR](/index.php/AUR "AUR").
2.  Put this in your [.vimrc](/index.php/Vim/.vimrc "Vim/.vimrc"): `~/.vimrc`  `let g:EclimCompletionMethod = 'omnifunc'` 
3.  Start `eclimd` script in a separate terminal: `$ /usr/lib/eclipse/plugins/org.eclim_$pkgver/bin/eclimd` 
4.  Create a file named `.project` in the same directory as your Java files: `.project` 
    ```
    <projectDescription>
        <name>*PROJECTNAME*</name>
    </projectDescription>

    ```

5.  Open your Java file in Vim and run: `:ProjectCreate . -n java` 

To compile the project:

```
:ProjectBuild

```

To run the project:

```
:Java

```

To run only current file:

```
:Java %

```

A list of available commands may be found [here](http://eclim.org/cheatsheet.html).

### C#

**Note:** For C# completion to "just work" simply create an empty `.sln` file in current or parent directory. The rest of this section explains how to manually create a full working C# project.

The easiest way to create a project is to use [monodevelop-stable](https://aur.archlinux.org/packages/monodevelop-stable/). The rest of this section explains how to manually create a C# project which can also be built from command line with `xbuild`.

First create a solution file. Replace ***bold-italic*** names appropriately.

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

Then create a directory named `PROJECT` and in it a file named `PROJECT.csproj`:

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

Place your C# files in `PROJECT` directory and do not forget to manually add them at the bottom of `PROJECT/PROJECT.csproj`.

Now YouCompleteMe should work for C# files in that directory and you can build the project. To compile the project from inside Vim:

```
:!xbuild

```

## Troubleshooting

Remember that it might take some time for YouCompleteMe to generate a list of completion strings.

The following commands are available for diagnostics:

*   `:messages` - show previous errors or messages from Vim
*   `:YcmDiags`
*   `:YcmDebugInfo`

### E764: Option 'omnifunc' is not set

If this happens for Java files, you forgot to put this in your *.vimrc*:

 `~/.vimrc`  `let g:EclimCompletionMethod = 'omnifunc'` 

### No completion in Java files

Make sure `eclimd` daemon is running:

```
$ ps -ax|grep eclimd

```

and that you have first generated project files.

### URLError: <urlopen error [Errno 111] Connection refused>

This error appears when you do not have a `.sln` file in current or parent directory.

### RuntimeError: Error starting OmniSharp server: no solutionfile found

Same as above.

## See also

*   [GitHub page](https://github.com/Valloric/YouCompleteMe)
*   [Project homepage](http://valloric.github.io/YouCompleteMe/)