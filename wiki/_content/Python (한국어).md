# Python (한국어)

Related articles

*   [Python package guidelines](/index.php/Python_package_guidelines "Python package guidelines")
*   [Python VirtualEnv](/index.php/Python_VirtualEnv "Python VirtualEnv")
*   [mod_wsgi](/index.php/Mod_wsgi "Mod wsgi")

From [Wikipedia](https://en.wikipedia.org/wiki/%ED%8C%8C%EC%9D%B4%EC%8D%AC "wikipedia:파이썬"):

	_파이썬(Python)은 1991년 프로그래머인 귀도 반 로섬(Guido van Rossum) 이 발표한 고급 프로그래밍 언어로, 플랫폼 독립적이며 인터프리터식, 객체지향적, 동적 타이핑(dynamically typed) 대화형 언어이다. 파이썬이라는 이름은 귀도가 좋아하는 코미디 〈Monty Python's Flying Circus〉에서 따온 것이다._

	_파이썬은 비영리의 파이썬 소프트웨어 재단이 관리하는 개방형, 공동체 기반 개발 모델을 가지고 있다. C언어로 구현된 C파이썬 구현이 사실상의 표준이다._

## Contents

*   [1 설치](#.EC.84.A4.EC.B9.98)
    *   [1.1 Python 3](#Python_3)
    *   [1.2 Python 2](#Python_2)
*   [2 Python 명령행에서 자동완성 사용하기](#Python_.EB.AA.85.EB.A0.B9.ED.96.89.EC.97.90.EC.84.9C_.EC.9E.90.EB.8F.99.EC.99.84.EC.84.B1_.EC.82.AC.EC.9A.A9.ED.95.98.EA.B8.B0)
*   [3 오래된 버전들](#.EC.98.A4.EB.9E.98.EB.90.9C_.EB.B2.84.EC.A0.84.EB.93.A4)
*   [4 팁과 트릭들](#.ED.8C.81.EA.B3.BC_.ED.8A.B8.EB.A6.AD.EB.93.A4)
*   [5 See also](#See_also)

## 설치

### Python 3

Python 3 는 Python 2 와 호환되며 가장 최신 버전의 Python 이다. Python3 와 Python2 는 거의 비슷하지만 내장되어 있는 객체들 (딕셔너리나 문자열 같은) 이 작동하는 방식의 차이나, 제거된 여러 기능들과 같이 세부적인 것들은 다르다. 표준 라이브러리의 몇몇 부분 또한 개편되었다. [Python2orPython3](http://wiki.python.org/moin/Python2orPython3) 이 문서를 통하여 둘의 차이를 좀 더 살펴 볼 수 있고, 이 [문서](http://getpython3.com/diveintopython3/porting-code-to-python-3-with-2to3.html) 를 통하여 Python 3 에 대하여 좀 더 알아볼 수 있다.

Python 3 의 가장 최신버전을 하려면, [공식 저장소](/index.php/Official_repositories "Official repositories") 에서 [python](https://www.archlinux.org/packages/?name=python) 꾸러미를 [설치](/index.php/Install "Install") 하면 된다.

만약 RC 혹은 BETA 버전의 소스코드를 이용하여 컴파일 설치를 하고 싶다면, [Python Downloads](http://www.python.org/download/) 이 페이지를 참고하면 된다. [Arch User Repository](/index.php/Arch_User_Repository "Arch User Repository") 에서 또한 좋은 [PKGBUILD](/index.php/PKGBUILD "PKGBUILD") 들을 찾을 수 있다. 만약, 컴파일 설치를 하기로 결정했다면, 기본적으로 `/usr/local/bin/python3.x` 에 설치 된다는 것에 주의 해야한다.

### Python 2

Python 2 의 최신 버전을 설치하려면 [공식 저장소](/index.php?title=Offcial_repositories&action=edit&redlink=1 "Offcial repositories (page does not exist)") 에서 [python2](https://www.archlinux.org/packages/?name=python2) 꾸러미를 [설치](/index.php/Install "Install") 하면 된다.

Python 3 와 Python2 가 동시에 설치가 되어있다면, Python 2 버전을 사용하는데에 있어서 명확하게 해야 할 필요가 있다.

어떤 프로그램은 Python 3 (`/usr/bin/python`) 대신에 Python 2 (`/usr/bin/python2`) 를 필요로 한다. Python 3 대신 Python 2 를 이용하기위해, 프로그램이나 스크립트를 [편집기](/index.php/List_of_applications/Documents#Text_editors "List of applications/Documents") 를 통하여 열고, 첫번째 줄을 수정 하면 된다. 첫번째 줄에 밑의 내용 중 하나가 있을 것이다.

```
#!/usr/bin/env python

```

또는

```
#!/usr/bin/python

```

둘 중, `python` 를 `python2` 로 바꾸면 프로그램이 Python 3 대신에 Python 2 를 이용하여 실행 될 것이다.

프로그램이나 스크립트의 내용을 수정하지 않고 강제로 Python 2 를 이용하여 실행하도록 하는 방법은 그 프로그램이나 스크립트 파일을 `python2` 를 이용하여 호출하는 것이다.

```
$ python2 _myScript.py_

```

## Python 명령행에서 자동완성 사용하기

**Note:** Python 3.4 버전 부터는 자동으로 [활성화](https://docs.python.org/3/tutorial/interactive.html) 되어있기 때문에, Python 2 에만 해당하는 항목입니다.

아래를 Python 명령행으로 복사하면 된다.

 `/usr/bin/python` 

```
import rlcompleter
import readline
readline.parse_and_bind("tab: complete")
```

원본: [http://algorithmicallyrandom.blogspot.com.es/2009/09/tab-completion-in-python-shell-how-to.html](http://algorithmicallyrandom.blogspot.com.es/2009/09/tab-completion-in-python-shell-how-to.html).

## 오래된 버전들

호기심에 오래된 Python 버전을 사용해 보고 싶다던가, 오래된 프로그램이 현재 Python 버전에서 동작하지 않는다던가, 혹은 오래된 Python 버전이 설치된 배포판 (RHEL 5.x 에는 Python 2.4 버전이 설치 되어있고, Ubuntu 12.04 에는 Python 3.1 버전이 설치 되어있다.) 을 대상으로 하여 프로그램을 테스트 해보고 싶은 경우가 있다면, [AUR](/index.php/AUR "AUR") 을 통하여 오래된 Python 버전들을 사용 가능하다.

*   [python15](https://aur.archlinux.org/packages/python15/)<sup><small>AUR</small></sup>: Python 1.5.2
*   [python24](https://aur.archlinux.org/packages/python24/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/python24)]</sup>: Python 2.4.6
*   [python25](https://aur.archlinux.org/packages/python25/)<sup><small>AUR</small></sup>: Python 2.5.6
*   [python26](https://aur.archlinux.org/packages/python26/)<sup><small>AUR</small></sup>: Python 2.6.9
*   [python30](https://aur.archlinux.org/packages/python30/)<sup><small>AUR</small></sup>: Python 3.0.1
*   [python31](https://aur.archlinux.org/packages/python31/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/python31)]</sup>: Python 3.1.5
*   [python32](https://aur.archlinux.org/packages/python32/)<sup><small>AUR</small></sup>: Python 3.2.5
*   [python33](https://aur.archlinux.org/packages/python33/)<sup><small>AUR</small></sup>: Python 3.3.5

2014 년 7 월 당시 Python 2.7, 3.2, 3.3, 그리고 3.4 버전들만 보안 패치를 지원하고 있다. 오래된 버전의 Python 으로 인터넷 통신을 하는 프로그램이나 믿을 수 없는 코드를 실행시키는 것은 위험하다.

기타 오래된 Python 버전에 대한 모듈이나 라이브러리들은 AUR 에서 찾을 수 있을 것이다. `python<_버전에서 마침표를 제거_>` 와 같이 찾아야 한다. 예) Python 2.6 버전에 대한 모듈이나 라이브러리는 python26 로 검색하여 찾을수 있다.

## 팁과 트릭들

[IPython](http://ipython.org/) 은 향상된 파이썬 명령행이다. 공식 저장소를 이용하여 사용 할 수 있다. [ipython](https://www.archlinux.org/packages/?name=ipython), [ipython2](https://www.archlinux.org/packages/?name=ipython2)

## See also

*   [Learning Python](http://shop.oreilly.com/product/9780596158071.do) is one of the most comprehensive, up to date, and well-written books on Python available today.
*   [Dive Into Python](http://www.diveintopython.net/) is an excellent (free) resource, but perhaps for more advanced readers and [has been updated for Python 3](http://diveintopython3.net/).
*   [A Byte of Python](http://www.swaroopch.com/notes/Python) is a book suitable for users new to Python (and scripting in general).
*   [Learn Python The Hard Way](http://learnpythonthehardway.org) the best intro to programming.
*   [Learn Python](http://learnpython.org) nice site to learn python.
*   [Crash into Python](http://stephensugden.com/crash_into_python/) Also known as _Python for Programmers with 3 Hours_, this guide gives experienced developers from other languages a crash course on Python.
*   [Beginning Game Development with Python and Pygame: From Novice to Professional](http://www.apress.com/book/view/9781590598726) for games.
*   [Think Python: How to Think Like a Computer Scientist](http://www.greenteapress.com/thinkpython/) A great introduction to Python programming for beginners.
*   [Pythonspot](https://pythonspot.com) Great Python programming tutorials.

Retrieved from "[https://wiki.archlinux.org/index.php?title=Python_(한국어)&oldid=404642](https://wiki.archlinux.org/index.php?title=Python_(한국어)&oldid=404642)"