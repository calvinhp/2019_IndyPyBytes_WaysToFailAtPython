---
title: Half a Dozen Ways to Fail at Python
author: Calvin Hendryx-Parker, CTO, Six Feet Up
date: IndyPy Bytes -- May 2019
---

# Where you don’t want to end up {data-background-image="https://imgs.xkcd.com/comics/python_environment.png"}

# 

![](https://imgs.xkcd.com/comics/python_environment.png)

https://xkcd.com/1987/

::: notes

April 2018 Randall Munroe posted this comic and admitted he did some bad things to get to this point.

The Python environmental protection agency wants to seal it in a cement chamber, with pictorial messages to future civilizations warning them about the danger of using `sudo` to install random Python packages.

:::

# 

![](https://paper-attachments.dropbox.com/s_592264EC504FCAD385868533320593CD1F97F1FB64D61A77B9E1A6B7FA7B4701_1558972953603_image.png)

    $ python
    command not found: python


::: notes
##  Fail 1 

 - Installing Python on Windows/OS X/Linux

Be careful of the default Python if it is included by default. Mac OS X includes an old Python 2.7 that is linked against a very old version of OpenSSL.

Generally, if Python is present and you are serious about your Python Craft, you will treat that install as private to the OS and install your own.

:::

# Installing Python

# Mac via [Homebrew](https://brew.sh)

    $ brew install python

::: notes
Again, take note that there is python here, but if you are serious, get your own installed
:::

# Windows via [Chocolatey](https://chocolatey.org/)

    C:\\> choco install python

or

![](images/MicrosoftStorePython.png)

::: notes
PATH management is going to be key to make sure you get the Python you expect
:::

# Linux

    $ apt install python3.7

::: notes
Disco Dingo has 🐍 Python 3.7.3 as default, but when I upgraded, my python command still gives me 2.7
:::

---

#### Ubuntu Fix for Correct Versions

    $ sudo update-alternatives --install /usr/bin/python python \
        /usr/bin/python3.7 20
    $ sudo update-alternatives --install /usr/bin/python python \
        /usr/bin/python2.7 10

# Verify!

    $ python --version
    Python 3.7.3

::: notes
Note, this is modern python, but we are going to run into some issues...
:::

# 

![](https://paper-attachments.dropbox.com/s_592264EC504FCAD385868533320593CD1F97F1FB64D61A77B9E1A6B7FA7B4701_1558973132749_image.png)

    ImportError: No module named requests

::: notes
## Fail 2

- How do I get 3rd party tools installed
- Using/installing pip if you can’t find it
   - included with python as of 2.7 and 3.4 but may not be obvious
   - it also may not be included in your distribution by default
:::

# No `sudo`

## 🚫

#

~~~ {.stretch .shell}
$ pip3 install httpie
Looking in links: https://dist.sixfeetup.com/public/
Collecting httpie
  Using cached https://files.pythonhosted.org/packages/d7/46/cfb014b9de6ac5cdd1fa06d85f411dd9506102c8b094906460b4a1710681/httpie-1.0.2-py2.py3-none-any.whl
  Requirement already satisfied: requests>=2.18.4 in /usr/lib/python3/dist-packages (from httpie) (2.21.0)
  Requirement already satisfied: Pygments>=2.1.3 in /usr/lib/python3/dist-packages (from httpie) (2.3.1)
  Installing collected packages: httpie
  ERROR: Could not install packages due to an EnvironmentError: [Errno 13] Permission denied: '/usr/local/lib/python3.7/dist-packages/httpie'
  Consider using the `--user` option or check the permissions.
~~~

::: notes
discuss using the `--user` option called the user scheme

Where python can pick up modules from is a multi layer cake and the user scheme adds another layer

It will install into your home dir on unix in `.local` and in Windows to `%APPDATA%/Python`
:::

# Except possibly here

~~~ {.console}
$ sudo pip install virtualenv
~~~

But you can avoid it!

::: notes
At a bare minimum, you may need to install `virtualenv` into your global python

Let's come back to this topic after we discuss virtualenvs as this can still cause you to step on a mine or two in the minefield
:::

# 

![](https://paper-attachments.dropbox.com/s_592264EC504FCAD385868533320593CD1F97F1FB64D61A77B9E1A6B7FA7B4701_1558971804604_image.png)

### My two projects need different versions

::: notes
## Fail 3
  - Proj A requires v 1.2 of dependent package and Proj B needs version 2.5…


  - virtualenv — sandboxing your Python for specific projects
    - Created by Ian Bicking
    - Needs to be installed, maybe with `pip`, but could also be used standalone
    - What if you don’t install it globally?
    - using `pip` safely in the sandbox
    - virtualenvwrapper — bonus material
:::

# Lucky You!
## 🍀

~~~ {.shell}
$ mkdir MyProject
$ cd MyProject
$ python -m venv venv
~~~

::: notes
We are on modern Python lucky user!

works great if you are on python 3.3 or newer

use the convention of `venv` for your project as may source control tools are already setup to ignore this.

Some folks use some shell prompt trickery to make the virtual env name appear to be the project directory
:::

---

## 😢

~~~ {.shell}
$ python -m venv foo
The virtual environment was not created successfully because ensurepip is not
available.  On Debian/Ubuntu systems, you need to install the python3-venv
package using the following command.

apt-get install python3-venv

You may need to use sudo with that command.  After installing the python3-venv
package, recreate your virtual environment.
~~~

::: notes
As of Python 3.3, virtual environments are included via the `venv` modules except when it is not.

Demo the two project environments created with `venv`
:::

# Legacy Python

Use `virtualenv`

~~~ {.shell}
$ mkdir MyProject
$ cd MyProject
$ virtualenv venv
~~~

::: notes
Use this for legacy python and be careful what version of Python it is using.

Since you are just running the random one that got installed globally, it will create environments with that version of python by default
:::

# `virtualenvwrapper`

    $ mkvirtualenv tools
    (tools) $ pip install httpie
    ...
    (tools) $ http -h
    ...

::: notes
Same issues as virtualenv, but nice that it hides them away for you

## Windows users have a clone
https://bitbucket.org/guillermooo/virtualenvwrapper-powershell
:::

# 

![](https://paper-attachments.dropbox.com/s_592264EC504FCAD385868533320593CD1F97F1FB64D61A77B9E1A6B7FA7B4701_1558971763326_image.png)

##  It works for me™

::: notes
## Fail 4

  - My Co-worker cloned the repo and can’t get the project started due to version issues
  - pipenv — repeatable sandboxes and installing packages
    - Alternatives to pipenv, because it may not fit your workflow
      - Poetry
      - Hatch
:::

# `pipenv` to the Rescue

<https://pipenv.readthedocs.io/>

::: notes
  - pipenv — repeatable sandboxes and installing packages
    - Alternatives to pipenv, because it may not fit your workflow
      - Poetry
      - Hatch
:::

# Installing

    $ brew install pipenv

㋈

    $ apt install pipenv

㋈

    $ pip install --user pipenv

#

~~~ {.shell}
$ mkdir MyProject
$ cd MyProject
$ pipenv install requests
~~~

::: notes
creates a `Pipfile` and `Pipfile.lock` if they didn't exist

On initialization you can choose a specific python
:::

#

    $ pipenv shell
    (aws-log-tools-GqD1dvo5) $

::: notes
demo here the cloudfront tools pipfile compared to requrements.txt

Show off `pipenv` subcommands:
    - shell
    - graph
    - check

Also show `pip list --outdated`
:::

# 

![](https://paper-attachments.dropbox.com/s_592264EC504FCAD385868533320593CD1F97F1FB64D61A77B9E1A6B7FA7B4701_1558971706396_image.png)

## My old Python project won’t run
### Or worse, my system Python is incomplete

::: notes
## Fail 5
  - I’ve been told to work on a legacy project that requires Python 2.6 and I only have newer python installed
  - pyenv — using different versions of python for your projects
:::

# pyenv

From <https://github.com/pyenv/pyenv-installer>

    $ curl https://pyenv.run | bash

::: notes
pyvenv is not the same as pyenv

If you are using homebrew, that is probably the easiest way to get started.

`pyenv` is not compatible for Windows, but there is a pyenv-win clone for windows.

https://github.com/pyenv-win/pyenv-win
:::

# Build Issues?

<https://github.com/pyenv/pyenv/wiki/Common-build-problems>

# Install and Use a Fresh Python

    $ pyenv install 3.6.2
    $ mkdir MyProject
    $ cd MyProject
    $ pyenv local 3.6.2
    $ pyenv versions
      system
      2.7.16
    * 3.6.2 (set by /home/calvin/Projects/MyProject/.python-version)
      3.7.3

::: notes
works around some issues with platform specific installs that don't contain everything like `ensurepip`
:::

#

![](https://paper-attachments.dropbox.com/s_592264EC504FCAD385868533320593CD1F97F1FB64D61A77B9E1A6B7FA7B4701_1558971681645_image.png)

## Halp, I’m on Windows!

::: notes
Fail 6:
  - Halp, I’m on Windows and don’t have a C compiler and want to use NumPy!
  - Data scienctist rejoice!
  - What about anaconda?

Wheels have made this nicer for python, but not everyone compiles wheels for each platform
:::

# Installation

<https://www.anaconda.com/distribution/>

::: notes
If you are on a platform other than windows, you will have to install some dependancies to use the GUI features

Be warned, this downloads over 650MB to install the full set of tools
:::

# Anaconda Tools

### `anaconda-navigator`
### Anaconda Prompt
### Spyder IDE
### Jupyter Notebooks
### `conda` CLI Tools

#

![](https://paper-attachments.dropbox.com/s_592264EC504FCAD385868533320593CD1F97F1FB64D61A77B9E1A6B7FA7B4701_1558972909570_image.png)

::: notes

- Top recommendations:
  - Never use sudo or admin mode
  - Always use a Sandbox
  - Always track your requirements and their versions

:::

# Questions?

#### <calvin@sixfeetup.com>

[`@calvinhp`](https://twitter.com/calvinhp)

