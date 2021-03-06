**翻译状态：** 本文是英文页面 [Python/Virtualenv](/index.php/Python/Virtualenv "Python/Virtualenv") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2017-10-19，点击[这里](https://wiki.archlinux.org/index.php?title=Python%2FVirtualenv&diff=0&oldid=492893)可以查看翻译后英文页面的改动。

*virtualenv* 是为 [Python](/index.php/Python "Python") 程序建立独立环境的工具，可以安装本地软件包，建立工作环境并在其中执行 [Python](/index.php/Python "Python")。

## Contents

*   [1 概览](#.E6.A6.82.E8.A7.88)
*   [2 安装](#.E5.AE.89.E8.A3.85)
*   [3 使用](#.E4.BD.BF.E7.94.A8)
    *   [3.1 创建虚拟环境](#.E5.88.9B.E5.BB.BA.E8.99.9A.E6.8B.9F.E7.8E.AF.E5.A2.83)
        *   [3.1.1 venv](#venv)
        *   [3.1.2 virtualenv](#virtualenv)
    *   [3.2 Activation](#Activation)
*   [4 Python versions](#Python_versions)
*   [5 virtualenvwrapper](#virtualenvwrapper)
    *   [5.1 Installation](#Installation)
    *   [5.2 Basic usage](#Basic_usage)
*   [6 See also](#See_also)

## 概览

虚拟环境是一个包含二进制程序和 shell 脚本的目录。二进制程序包含执行脚本的 *python* 和安装其它模块的 *pip*。脚本包括激活环境的脚本，[bash](/index.php/Bash "Bash"), csh 和[fish](/index.php/Fish "Fish") 个有一个。这个虚拟环境模拟了一个完整的 [Python](/index.php/Python "Python") 执行环境和需要的模块，将程序运行的环境与系统其它部分隔离开来。

## 安装

[Python](/index.php/Python "Python") 从 3.3 开始包含了 *venv* 程序，无需单独安装。 如果使用的是老版本的 Python, 需要额外[安装](/index.php/%E5%AE%89%E8%A3%85 "安装") *virtualenv*。

*   Python 3.3+: [python](https://www.archlinux.org/packages/?name=python)
*   Python 3: [python-virtualenv](https://www.archlinux.org/packages/?name=python-virtualenv)
*   Python 2: [python2-virtualenv](https://www.archlinux.org/packages/?name=python2-virtualenv)

## 使用

不同工具的使用方式基本相同。

### 创建虚拟环境

Use *venv* or *virtualenv* to create the virtual environment within your project directory. Be sure to exclude the venv directory from version control--a copy of `pip freeze` will be enough to rebuild it.

#### venv

**Note:** This method replaces the *pyvenv* script, which is deprecated since [python](https://www.archlinux.org/packages/?name=python) 3.6.

This tool is provided by [python](https://www.archlinux.org/packages/?name=python) (3.3+):

```
$ python -m venv venv

```

#### virtualenv

Use *virtualenv* for Python 3, available in [python-virtualenv](https://www.archlinux.org/packages/?name=python-virtualenv).

```
$ virtualenv venv

```

And *virtualenv2* for Python 2, available in [python2-virtualenv](https://www.archlinux.org/packages/?name=python2-virtualenv).

```
$ virtualenv2 venv

```

### Activation

Use one of the provided shell scripts to activate and deactivate the environment. This example assumes bash is used.

```
$ source venv/bin/activate
(venv) $

```

Once inside the virtual environment, modules can be installed with *pip* and scripts can be run as normal.

To exit the virtual environment, run the function provided by `bin/activate`:

```
(venv) $ deactivate

```

## Python versions

The binary versions depend on which virtual environment tool was used. For instance, the *python* command used in the Python 2 example points to `bin/python2.7`, while the one in the *venv* example points to `bin/python3.6`.

One major difference between *venv* and *virtualenv* is that the former uses the system's Python binary by default:

```
$ ls -l venv/bin/python3.6
lrwxrwxrwx 1 foo foo 7 Jun  3 19:57 venv/bin/python3.6 -> /usr/bin/python3

```

The *virtualenv* tool uses a separate Python binary in the environment directory:

```
$ ls -l virtualenv/bin/python3.6
lrwxrwxrwx 1 foo foo 7 Jun  3 19:58 virtualenv/bin/python3.6 -> python3

```

## virtualenvwrapper

*virtualenvwrapper* allows more natural command line interaction with your virtual environemnts by exposing several useful commands to create, activate and remove virtual environments. This package is a wrapper for both [python-virtualenv](https://www.archlinux.org/packages/?name=python-virtualenv) and [python2-virtualenv](https://www.archlinux.org/packages/?name=python2-virtualenv).

### Installation

[Install](/index.php/Install "Install") the [python-virtualenvwrapper](https://www.archlinux.org/packages/?name=python-virtualenvwrapper) package from the [official repositories](/index.php/Official_repositories "Official repositories").

Now add the following lines to your `~/.bashrc`:

```
export WORKON_HOME=~/.virtualenvs
source /usr/bin/virtualenvwrapper.sh

```

Since python3 is a system-wide default in Arch, in order to be able to create python2 environments, you need to set `VIRTUALENVWRAPPER_PYTHON` and `VIRTUALENVWRAPPER_VIRTUALENV` prior to sourcing `virtualenvwrapper.sh` in your `~/.bashrc`:

```
export VIRTUALENVWRAPPER_PYTHON=/usr/bin/python2.7
export VIRTUALENVWRAPPER_VIRTUALENV=/usr/bin/virtualenv2

```

The line `source /usr/bin/virtualenvwrapper.sh` can cause some slowdown when starting a new shell. To fix this try using `source /usr/bin/virtualenvwrapper_lazy.sh`, which will load virtualenvwrapper the first time a virtualenvwrapper function is called.

If you are not using python3 by default (check the output of `python --version`) you need to add the following line to your `~/.bashrc` prior sourcing the `virtualenvwrapper.sh` script.

```
export VIRTUALENVWRAPPER_PYTHON=/usr/bin/python3

```

Re-open your console and create the `WORKON_HOME` folder:

```
$ mkdir $WORKON_HOME

```

**Note:** This seems to happen now automatically after re-open the console for the first time.

### Basic usage

The main information source on virtualenvwrapper usage (and extension capability) is Doug Hellmann's [page](http://www.doughellmann.com/docs/virtualenvwrapper/).

Create the virtual environment:

```
$ mkvirtualenv -p /usr/bin/python2.7 my_env

```

Activate the virtual environment:

```
$ workon my_env

```

Install some package inside the virtual environment (say, Django):

```
(my_env) $ pip install django

```

After you have done your things, leave the virtual environment:

```
(my_env) $ deactivate

```

## See also

*   [Python venv](https://docs.python.org/3/library/venv.html)
*   [virtualenv Pypi page](https://pypi.python.org/pypi/virtualenv)
*   [Tutorial for virtualenv](http://wiki.pylonshq.com/display/pylonscookbook/Using+a+Virtualenv+Sandbox)
*   [virtualenvwrapper page at Doug Hellmann's](http://www.doughellmann.com/docs/virtualenvwrapper/)