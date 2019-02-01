# Overview
[This repository](http://github.com/machine-learning-helpers/induction-python)
features a set of various Python Jupyter notebooks, collected from books,
blogs, or originally designed and developed by the
[organization team](http://github.com/orgs/machine-learning-helpers/teams/contributors).
It provides guidance for end-to-end working examples of how to author
Python Jupyter notebooks in just a few minutes.

The source code is properly attributed in the corresponding directories. If you believe some attribution
is missing, please [submit a pull request](http://github.com/machine-learning-helpers/induction-python/pulls)
or [an issue](http://github.com/machine-learning-helpers/induction-python/issues).

That project makes use of [Jupyter Lab](http://jupyterlab.readthedocs.io/en/stable/)
and [Python virtual environments](https://docs.python.org/3/tutorial/venv.html),
which can either be:
* Installed locally on your laptop/workstation. More details are available
  in the corresponding sections of this project:
  + [Python virtual environments](http://github.com/machine-learning-helpers/induction-python/tree/master/installation/virtual-env)
  + [Jupyter Lab](http://github.com/machine-learning-helpers/induction-python/tree/master/installation/jupyter)
* Run from/within Docker. More details are available on
  the [Docker images for Python Jupyter Lab notebooks project](http://github.com/machine-learning-helpers/docker-python-jupyter)

* More integration with
  [Cookiecutter Data Science](https://drivendata.github.io/cookiecutter-data-science)
  may happen in the future. Those guidelines are nevertheless worth the read.
  As of February 2019, Cookiecutter Data Science works with explicit `virtualenv`
  and `requirements.txt` files, whereas we believe that Pyenv and `pipenv`
  are now the right choices to manage Python dependencies (as `pipenv`
  also uses `virtualenv`, but in a more seamless way for the developer).

## See also
* [NumPy](http://www.numpy.org)
* [SciKit-Learn](http://scikit-learn.org/stable)
* [Pandas](http://pandas.pydata.org)
  + [GeoPandas](http://geopandas.org)
* [Jupyter Lab](https://jupyterlab.readthedocs.io/en/stable)
* [Optimus, Agile Data Science Workflows made easy](http://www.hioptimus.com)
* [Featuretools](http://www.featuretools.com)
* [Dask](http://dask.org):
* [Matplotlib](https://matplotlib.org)
* [Seaborn](https://seaborn.pydata.org):
* [Altair for visualization](https://altair-viz.github.io/getting_started/installation.html)

# Dependencies
That projects makes use of [Jupyter Lab](http://jupyterlab.readthedocs.io/en/stable/)
and [Python virtual environments](https://docs.python.org/3/tutorial/venv.html).
More details are available in the corresponding sections:
* [Python virtual environments](http://github.com/machine-learning-helpers/induction-python/tree/master/installation/virtual-env)
* [Jupyter Lab](http://github.com/machine-learning-helpers/induction-python/tree/master/installation/jupyter)

# Cookiecutter Data Science
* A dependency on [Cookiecutter Data Science](https://drivendata.github.io/cookiecutter-data-science/)
  has been added to `pipenv`. Starting a new project is now as easy as issuing the following command:
```bash
$ mkdir -p ~/dev/ml
$ pipenv run cookiecutter https://github.com/drivendata/cookiecutter-data-science
$ cp .python-version Pipfile <resulting-project-directory-structure>/
$ mv <resulting-project-directory-structure> ~/dev/ml
$ pushd ~/dev/ml/<resulting-project-directory-structure>
$ pipenv install
$ pipenv run python ./test_environment.py
Loading .env environment variables…
>>> Development environment passes all tests!
$ git init .
$ git remote add origin https://<git-server>:/<your-preferred-repo>
$ git add .gitignore .python-version LICENSE Makefile Pipfile* README.md docs models notebooks references reports requirements.txt setup.py src test_environment.py tox.ini
$ git commit -m "Project creation"
$ git push --all
$ popd
```

* An example is provided in the
  [`ml_induction_python` project folder](http://github.com/machine-learning-helpers/induction-python/tree/master/ml_induction_python)


