# Overview
[That section](http://github.com/machine-learning-helpers/induction-python/tree/master/installation/virtual-env)
explains how to install and configure Python virtual environments.
It is part of [the Python induction for Machine Learning (ML) project](http://github.com/machine-learning-helpers/induction-python),
but may be referenced by many other projects.

An alternative way to install Python virtual environments, and software pieces
such as Jupyter Lab, is to use a
[Docker image for Python Jupyter Lab notebooks](http://github.com/machine-learning-helpers/docker-python-jupyter).

## See also
* [Pipenv: Python Development Workflow for Humans](http://pypi.org/project/pipenv)
* [Basic Usage of Pipenv](http://pipenv.readthedocs.io/en/latest/basics/)
* [Pipenv and Virtual Environments](http://docs.python-guide.org/dev/virtualenvs/)
* [Pyenv on GitHub](http://github.com/pyenv/pyenv)
* [How to install `Pyenv` in Linux](http://www.tecmint.com/pyenv-install-and-manage-multiple-python-versions-in-linux/)
* [Installing Python `virtualenv` on CentOS 7](http://blog.teststation.org/centos/python/2016/05/11/installing-python-virtualenv-centos-7)

# Installation
As the way to manage virtual environments in Python is still not fully stable,
we explain here a robust way to use those Python virtual environments on any
platform.

## Introduction to Pyenv
[Pyenv](https://github.com/pyenv/pyenv) allows to install in parallel
on any platform any version of Python, from old deprecated ones to
the most recent ones, including the development versions.

Pyenv is packaged on some platforms (e.g., MacOS), but needs to be installed
manually on some others (e.g., CentOS). The procedure of installation
for `pyenv` is given below.

Pyenv installs the Python binaries into a folder structure local
to the user (typically, `~/.pyenv/`), so that they do not interfere
with the system-wide Python version.

## Introduction to `pipenv`
[`pipenv`](http://pypi.org/project/pipenv) is now an official part of Python
and integrates well with `virtualenv` and `pyenv`, even though that latter
is not (yet?) part of the official Python distribution.

`pipenv` allows to install in parallel, for any specific project,
the full stack of Python dependencies (e.g., NumPy) needed
by those projects.

`pipenv` installs the Python dependencies into `virtualenv` directories
(typically, in `~/.local/share/virtualenvs/`),
one per specific project or directory, and manages those dependencies
through human-readable text files (`Pipfile` and `Pipfile.lock`),
which can be added to the projects.

## Installation of `pyenv`
The Python binaries are installed in `~/.pyenv`, where `pipenv` can find them.

### CentOS 7
* (As `root`,) Install a few dependencies:
```bash
$ sudo yum -y install epel-release
# sudo yum -y install git gcc zlib-devel bzip2-devel readline-devel sqlite-devel openssl-devel libffi-devel
```

* (As a standard user,) Grab the the latest `pyenv` source tree
  from its Github repository and install it in `~/.pyenv`:
```bash
$ git clone https://github.com/pyenv/pyenv.git $HOME/.pyenv
```

* The environment variable `PYENV_ROOT` needs to be set,
  and `$PYENV_ROOT/bin` added to `PATH`. `shims` then has to be enabled,
  as well as relevant auto-completion:
```bash
$ cat >> ~/.bashrc << _EOF

## Python pyenv
export PYENV_ROOT="${HOME}/.pyenv"
export PATH="${PYENV_ROOT}/bin:${PATH}"

if command -v pyenv 1>/dev/null 2>&1; then
  eval "$(pyenv init -)"
fi
_EOF
$ . ~/.bashrc
```

### MacOS
```bash
$ brew install pyenv
```

### All: Install a specific version of Python
* Check which versions of Python 3.7 are available to `pyenv` to install:
```bash
$ pyenv install --list | cut -d' ' -f3,3 | grep -e "^3.7"
3.7.0
3.7-dev
3.7.1
```

* Install the version `3.7.1` of Python (latest stable version,
  as of December 2018):
```bash
$ pyenv install 3.7.1
Downloading Python-3.7.1.tar.xz...
-> https://www.python.org/ftp/python/3.7.1/Python-3.7.1.tar.xz
Installing Python-3.7.1...
Installed Python-3.7.1 to ~/.pyenv/versions/3.7.1
```

## Installation of `pipenv`

### Linux

#### Debian / Ubuntu
```bash
$ apt-get install python3-pip python3-all
$ pip3 install --user -U pipenv
```

#### CentOS
* As a standard user:
```bash
$ pip install --user -U pipenv
```

#### Fedora
```bash
$ dnf -y install pipenv
```

### MacOS
```bash
$ brew install pipenv
```

### Install specific versions in a given project
* Go to a project directory and install the required libraries.
  It will create a `Pipfile` file, if not already exising.
```bash
$ mkdir ~/dev/geo && cd ~/dev/geo
$ git clone https://github.com/opentraveldata/quality-assurance.git opentraveldata-qa
$ cd opentraveldata-qa
$ ./mkLocalDir.sh 
$ pipenv install
Creating a virtualenv for this project…
Pipfile: ~/dev/geo/opentraveldata-qa/Pipfile
Using ~/.pyenv/versions/3.7.1/bin/python3 (3.7.1) to create virtualenv…
⠋ Creating virtual environment...Using base prefix '~/.pyenv/versions/3.7.1'
New python executable in ~/.local/share/virtualenvs/opentraveldata-qa-JhZpfQQq/bin/python3
Also creating executable in ~/.local/share/virtualenvs/opentraveldata-qa-JhZpfQQq/bin/python
Installing setuptools, pip, wheel...done.
Running virtualenv with interpreter ~/.pyenv/versions/3.7.1/bin/python3

✔ Successfully created virtual environment! 
Virtualenv location: ~/.local/share/virtualenvs/opentraveldata-qa-JhZpfQQq
Installing dependencies from Pipfile.lock (a65489)…
  🐍   ▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉ 0/0 — 00:00:00
To activate this project's virtualenv, run pipenv shell.
Alternatively, run a command inside the virtualenv with pipenv run.
```

### Launch Python scripts with `pipenv`
* Check that the Python environment is ready
```bash
$ pipenv check
Checking PEP 508 requirements…
Passed!
Checking installed package safety…
All good!
```

* Just prefix the commands with `pipenv run`:
```bash
$ pipenv run checkers/check-por-cmp-optd-unlc.py
```

## `virtualenv`

### On CentOS
* If needed, enable the [EPEL](https://fedoraproject.org/wiki/EPEL) repository:
```bash
$ sudo yum -y install epel-release
```

* Install `python34` and `python-pip` packages
  (but not `virtualenv`):
```bash
$ sudo yum -y install python34 python34-devel python34-pip
```

* If needed, uninstall the CentOS-packaged `virtualenv`:
```bash
$ sudo yum remove python-virtualenv
```

* Update `pip` and install `virtualenv` with `pip`:
```bash
$ sudo pip3 install -U pip
$ sudo pip3 install virtualenv
```

* Create and activate a new Python 3 virtual environment:
```bash
$ mkdir -p ~/dev && cd ~/dev
$ PYTHON_VERSION=$(python3 --version 2>&1 | cut -d' ' -f2,2 | cut -d'.' -f1,2)
$ virtualenv -p python3 venv${PYTHON_VERSION}
$ ln -s venv${PYTHON_VERSION} venv3
```

* Optionally, install [Java 8](http://openjdk.java.net/projects/jdk8u),
  needed for instance by [Spark](https://spark.apache.org):
```bash
$ sudo yum -y install java-1.8.0-openjdk-devel java-1.8.0-openjdk-javadoc
```

### Fedora
* Install `python3` and `python3-pip` packages
  (but not `virtualenv`):
```bash
$ sudo dnf -y install python3 python3-devel python3-pip
```

* If needed, uninstall the Fedora-packaged `virtualenv`:
```bash
$ sudo dnf remove python3-virtualenv
```

* Update `pip` and install `virtualenv` with `pip`:
```bash
$ sudo pip install -U pip
$ sudo pip install virtualenv
```

* Create and activate a new Python 3 virtual environment:
```bash
$ mkdir -p ~/dev && cd ~/dev
$ PYTHON_VERSION=$(python3 --version 2>&1 | cut -d' ' -f2,2 | cut -d'.' -f1,2)
$ python3 -m venv venv${PYTHON_VERSION}
$ ln -s venv${PYTHON_VERSION} venv3
```

* Optionally, install [Java 8](http://openjdk.java.net/projects/jdk8u),
  needed for instance by [Spark](https://spark.apache.org):
```bash
$ sudo dnf -y install java-1.8.0-openjdk-devel java-1.8.0-openjdk-javadoc
```

### MacOS
* With your favorite MacOS package manager, for instance
  [Homebrew](https://brew.sh), install Python 3:
```bash
$ brew install python3
```

* Install the Python 3 virtual environment:
```bash
$ mkdir -p ~/dev && cd ~/dev
$ PYTHON_VERSION=$(python3 --version 2>&1 | cut -d' ' -f2,2 | cut -d'.' -f1,2)
$ python3 -m venv venv${PYTHON_VERSION}
$ ln -s venv${PYTHON_VERSION} venv3
```

* Add a Shell script function for graphical packages
  (eg, [Matplotlib](https://matplotlib.org)) in ``~/.bashrc``:
```bash
$ cat >> ~/.bashrc << _EOF

# Python - support for Matplotlib in virtual environment
# http://matplotlib.org/faq/osx_framework.html#osxframework-faq
function frameworkpython {
        PYVER=$(python --version | cut -d' ' -f2 | cut -d'.' -f1)
        PYTHON_EXEC=/usr/local/bin/python$PYVER
        if [[ ! -z "${VIRTUAL_ENV}" ]]
        then
                PYTHONHOME=${VIRTUAL_ENV} ${PYTHON_EXEC} "$@"
        else
                ${PYTHON_EXEC} "$@"
        fi
}

_EOF
```

* Any Matplotlib-based Python script can then be launched with:
```bash
$ frameworkpython myPyscript.py
```

### General - A few useful packages
An arbitrary selection of useful packages.

* Activate the Python virtual environment:
```bash
$ source ~/dev/venv3/bin/activate
(venv3.7) $ python --version
Python 3.7.0
```

* Upgrade ``pip`` if needed:
```bash
(venv3.7) $ pip install -U pip
```

#### Machine Learning (ML)
* [NumPy](http://www.numpy.org), [SciKit-Learn](http://scikit-learn.org/stable),
  [Pandas](http://pandas.pydata.org), [Jupyter Lab](https://jupyterlab.readthedocs.io/en/stable),
  [Dask](http://dask.org):
```bash
(venv3.7) $ pip install -U numpy scikit-learn pandas jupyterlab dask
```

* [Matplotlib](https://matplotlib.org), [Seaborn](https://seaborn.pydata.org):
```bash
(venv3.7) * pip install -U matplotlib seaborn
```

* [Featuretools](http://www.featuretools.com)(not available on CentOS 7):
```bash
(venv3.7) $ pip install -U featuretools
```

* [Altair for visualization](https://altair-viz.github.io):
```bash
(venv3.7) $ pip install -U altair vega_datasets gpdvega
```

* [PySpark](https://spark.apache.org/docs/2.3.0/api/python/pyspark.html):
```bash
(venv3.7) $ pip install -U pyspark
```

# Typical session

## ``pipenv``
* Prefix any Python command/script with ``pipenv run``:
```bash
$ pipenv run python --version
Python 3.7.0
```

## ``virtualenv``
* Activate the Python virtual environment:
```bash
$ source ~/dev/venv3/bin/activate
```

* Use Python:
```bash
(venv3.7) $ python --version
Python 3.7.0
```

* When done with the need for Python, deactivate the virtual environment:
```bash
(venv3.7) $ deactivate
```

# PySpark
* PySpark, run from the Python virtual environment, needs a standalone
  Java Virtual Machine (JVM) to run Spark. So, be sure to install Java 8,
  as explained in the above installation section.

* Launch a Spark Shell:
```bash
(venv3.7) $ spark-shell
[...]
Spark context Web UI available at http://localhost:4040
Spark context available as 'sc' (master = local[*], app id = local-12345).
Spark session available as 'spark'.
Welcome to
      ____              __
     / __/__  ___ _____/ /__
    _\ \/ _ \/ _ `/ __/  '_/
   /___/ .__/\_,_/_/ /_/\_\   version 2.3.2
      /_/
         
Using Scala version 2.11.8 (OpenJDK 64-Bit Server VM, Java 1.8.0_181)
Type in expressions to have them evaluated.
Type :help for more information.

scala> spark.version
res0: String = 2.3.2

scala> :quit
$ 
```


