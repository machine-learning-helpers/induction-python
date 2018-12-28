# Overview
[That section](http://github.com/machine-learning-helpers/induction-python/tree/master/installation/virtual-env)
explains how to install and configure Python virtual environments.
It is part of the
[Python induction for Machine Learning (ML) project](http://github.com/machine-learning-helpers/induction-python),
but may be referenced by many other projects.

An alternative way to install Python virtual environments, and software pieces
such as Jupyter Lab, is to launch ready-to-use
[Docker images for Python Jupyter Lab notebooks](https://cloud.docker.com/u/artificialintelligence/repository/docker/artificialintelligence/python-jupyter).

## See also
* [Docker images with Jupyter Lab notebooks pre-installed](https://cloud.docker.com/u/artificialintelligence/repository/docker/artificialintelligence/python-jupyter)
* [Pyenv on GitHub](http://github.com/pyenv/pyenv)
* [How to install `Pyenv` in Linux](http://www.tecmint.com/pyenv-install-and-manage-multiple-python-versions-in-linux/)
* [Pipenv: Python Development Workflow for Humans](http://pypi.org/project/pipenv)
* [Basic Usage of Pipenv](http://pipenv.readthedocs.io/en/latest/basics/)
* [Pipenv and Virtual Environments](http://docs.python-guide.org/dev/virtualenvs/)
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

### Dependencies - CentOS 7
* (As `root`,) If needed, enable the [EPEL](https://fedoraproject.org/wiki/EPEL) repository:
```bash
$ sudo yum -y install epel-release
```

* (Still as `root`,) Install a few dependencies:
```bash
$ sudo yum -y install git gcc zlib-devel bzip2-devel readline-devel sqlite-devel openssl-devel libffi-devel
```

### Dependencies - Ubuntu / Debian
* (As `root`,) Install a few dependencies:
```bash
$ sudo aptitude install zlib1g-dev libbz2-dev libsqlite3-dev libreadline-dev libssl-dev libffi-dev
```

### All Linux distributions
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
* Thanks to [Homebrew](https://brew.sh), install `pyenv`:
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

## Java
Java is needed for at least a few big data related packages, for instance
Hive. The [OpenJDK 8](http://openjdk.java.net/projects/jdk8u) should be good
enough for [Spark](https://spark.apache.org) and
[PySpark](http://spark.apache.org/docs/latest/api/python).

### Fedora
```bash
$ sudo dnf -y install java-1.8.0-openjdk-devel java-1.8.0-openjdk-javadoc
```

## Support for graphical frameworks
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

## General - A few useful Python packages
An arbitrary selection of useful packages.

* [Cython, C-extensions for Python](http://cython.org)(may be needed to re-compile some extra Python modules):
```bash
$ pipenv install cython
```

* [NetworkX, software for complex networks](http://networkx.github.io):
```bash
$ pipenv install networkx
```

* [Graphviz](http://www.graphviz.org), graph visualization software:
```bash
$ pipenv install graphviz
```

* [Seaborn](http://seaborn.pydata.org), statistical data visualization:
```bash
$ pipenv install seaborn
```

* [imageio](http://imageio.github.io), Python library for reading
  and writing image data:
```bash
$ pipenv install imageio
```

* [Altair for visualization](https://altair-viz.github.io):
```bash
$ pipenv install altair vega_datasets gpdvega
```

* Graphical, maps and geographical packages:
  + [Matplotlib](https://matplotlib.org)
  + [Cartopy](https://scitools.org.uk/cartopy/docs/latest/)
  + [(deprecated) BaseMap, part of Matplotlib](http://github.com/matplotlib/basemap)
  + [NeoBase, GeoBase rebooted](http://neobase.readthedocs.io)
```bash
$ pipenv install matplotlib cartopy neobase
```

* [xlrd](http://www.python-excel.org), working with Excel Files in Python:
```bash
$ pipenv install xlrd
```

* Machine Learning (ML)
  + [NumPy](http://www.numpy.org)
  + [SciKit-Learn](http://scikit-learn.org/stable)
  + [Pandas](http://pandas.pydata.org)
  + [Dask](http://dask.org)
```bash
$ pipenv install numpy scikit-learn pandas dask
```

  + [ml-tools](https://github.com/kostasthebarbarian/mltools), a collection
    of ML tools for object detection and classification on Digital Globe (DG)
	imagery:
```bash
$ pipenv install ml-tools
```

  + [Tensorflow](http://www.tensorflow.org/api_docs/python/), an open source
    ML framework for everyone:
```bash
$ pipenv install tensorflow
```

  + [Keras](http://keras.io), the Python Deep Learning (DL) library:
```bash
$ pipenv install keras scikit-keras
```

  + [Theano](http://deeplearning.net/software/theano/):
```bash
$ pipenv install Theano
```

  + [gym](http://gym.openai.com), a toolkit for developing and comparing
    reinforcement learning (RL) algorithms:
```bash
$ pipenv install gym
```

  + [PyTorch](http://pytorch.org), an open source deep learning (DL) platform
    that provides a seamless path from research prototyping
	to production deployment:
```bash
$ pipenv install pytorch
```

  + [ONNXMLTools](http://github.com/onnx/onnxmltools), for the conversion
    of models to [ONNX](http://onnx.ai):
```bash
$ pipenv install onnxmltools
```

  + [sklearn-pmml-model](http://github.com/iamDecode/sklearn-pmml-model),
    library to parse [PMML](http://dmg.org/pmml/v4-3/GeneralStructure.html)
	models into Scikit-learn estimators:
```bash
$ pipenv install sklearn-pmml-model
```

  + [surprise](http://surpriselib.com), a Python
    [scikit](https://www.scipy.org/scikits.html) building and analyzing
	recommender systems:
```bash
$ pipenv install surprise
```

  + [parfit](http://github.com/jmcarpenter2/parfit), package for parallelizing
    the fit and flexibly scoring of Scikit-learn ML models,
	with visualization routines:
```bash
$ pipenv install parfit
```

  + [mcfly](http://github.com/NLeSC/mcfly), a deep learning (DL) tool
    for time series classification:
```bash
$ pipenv install mcfly
```

* [Featuretools](http://www.featuretools.com)(not available on CentOS 7):
```bash
$ pipenv install featuretools
```

* [PySpark](https://spark.apache.org/docs/2.3.0/api/python/pyspark.html):
```bash
$ pipenv install pyspark
```

* [OpenTracing](http://opentracing.io) for [ElasticSearch (ELK)](http://elastic.co):
```bash
$ pipenv install elasticsearch_opentracing
```

* Install latest versions (e.g., of `pyproj` and `basemap`):
```bash
$ pipenv install git+https://github.com/jswhit/pyproj.git#egg=pyproj \
         git+https://github.com/matplotlib/basemap.git#egg=basemap
```

* [Jupyter ecosystem](https://jupyter.org/documentation)
  + [Jupyter Lab](https://jupyterlab.readthedocs.io/en/stable):
```bash
$ pipenv install jupyterlab
```

  + Various Jupyter modules:
```bash
$ pipenv install jupyter-git jupyter-pip jupyter-beautifier jupyter-full-width jupyter-notebook-gist
$ pipenv install jupyter_dashboards jupyter_dashboards_bundlers jupyter-spark
$ pipenv install jupyter_utils jupyter-tools
```

  + Jupyter extensions:
```bash
$ pipenv install jupyter_contrib_nbextensions
$ jupyter contrib nbextension install --user
$ jupyter labextension install jupyterlab-drawio
```

  + [Jupyter kernels](https://github.com/jupyter/jupyter/wiki/Jupyter-kernels):
```bash
$ pipenv install bash_kernel ipykernel r2_kernel
```

# Typical session

## `pyenv`
* Check the installed versions of Python:
```bash
$ pyenv versions
* system (set by ~/.pyenv/version)
  3.7.1
```

## `pipenv`
* Prefix any Python command/script with ``pipenv run``:
```bash
$ mkdir -p /tmp/$USER && cd /tmp/$USER
$ pipenv install --python 3.7
Creating a virtualenv for this project…
Pipfile: /tmp/$USER/Pipfile
Using ~/.pyenv/versions/3.7.1/bin/python3.7 (3.7.1) to create virtualenv…
⠹Running virtualenv with interpreter ~/.pyenv/versions/3.7.1/bin/python3.7
Using base prefix '~/.pyenv/versions/3.7.1'
New python executable in ~/.local/share/virtualenvs/$USER-bV5bYO4h/bin/python3.7
Also creating executable in ~/.local/share/virtualenvs/$USER-bV5bYO4h/bin/python
Installing setuptools, pip, wheel...
done.

Virtualenv location: ~/.local/share/virtualenvs/$USER-bV5bYO4h
Creating a Pipfile for this project…
Pipfile.lock not found, creating…
Locking [dev-packages] dependencies…
Locking [packages] dependencies…
Updated Pipfile.lock (a65489)!
Installing dependencies from Pipfile.lock (a65489)…
  🐍   ▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉ 0/0 — 00:00:00
To activate this project's virtualenv, run pipenv shell.
Alternatively, run a command inside the virtualenv with pipenv run.
```

* Use Python without activating the virtual environment:
```bash
$ cd /tmp/$USER
$ pipenv run python --version
Python 3.7.1
```

* Use Python in an activated virtual environment:
```bash
$ cd /tmp/$USER
$ pipenv shell
($USER) $ python --version
Python 3.7.1
($USER) $ exit
```

# PySpark
* PySpark, run from the Python virtual environment, needs a standalone
  Java Virtual Machine (JVM) to run Spark. So, be sure to install Java 8,
  as explained in the above installation section.

* Launch a Spark Shell:
```bash
$ pipenv run spark-shell
[...]
Spark context Web UI available at http://localhost:4040
Spark context available as 'sc' (master = local[*], app id = local-12345).
Spark session available as 'spark'.
Welcome to
      ____              __
     / __/__  ___ _____/ /__
    _\ \/ _ \/ _ `/ __/  '_/
   /___/ .__/\_,_/_/ /_/\_\   version 2.4.0
      /_/
         
Using Scala version 2.11.12 (OpenJDK 64-Bit Server VM, Java 1.8.0_181)
Type in expressions to have them evaluated.
Type :help for more information.

scala> spark.version
res0: String = 2.4.0

scala> :quit
$ 
```


