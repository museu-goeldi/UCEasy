# UCEasy

UCEasy is a web application built on top of the [phyluce](https://phyluce.readthedocs.io/en/latest/) software package to serve as a graphical wrapper. Because the analyzes that can be done with [ultraconserved elements](https://www.ultraconserved.org/) (UCEs) are diverse, we provide a convenient tool to facilitate the execution of common tasks for all types of analyzes, these being [Quality Control](https://phyluce.readthedocs.io/en/latest/quality-control.html), [Assembly](https://phyluce.readthedocs.io/en/latest/assembly.html) and [UCE Processing](https://phyluce.readthedocs.io/en/latest/uce-processing.html).

<p align="center">
    <img src="doc/img/phyluce_diagram.png">
</p>


## Quick Start

Run the web application:

    make run

And open it in the browser at [http://127.0.0.1:5000/](http://127.0.0.1:5000/)


## Prerequisites

This is built to be used with Python 3. Update `Makefile` to switch to Python 2 if needed.

Some Flask dependencies are compiled during installation, so `gcc` and Python header files need to be present.
For example, on Ubuntu:

    apt install build-essential python3-dev


## Development environment and release process

 - create virtualenv with Flask and uceasy installed into it (latter is installed in
   [develop mode](http://setuptools.readthedocs.io/en/latest/setuptools.html#development-mode) which allows
   modifying source code directly without a need to re-install the app): `make venv`

 - run development server in debug mode: `make run`; Flask will restart if source code is modified

 - run tests: `make test` (see also: [Testing Flask Applications](http://flask.pocoo.org/docs/0.12/testing/))

 - create source distribution: `make sdist` (will run tests first)

 - to remove virtualenv and built distributions: `make clean`

 - to add more python dependencies: add to `install_requires` in `setup.py`

 - to modify configuration in development environment: edit file `settings.cfg`; this is a local configuration file
   and it is *ignored* by Git - make sure to put a proper configuration file to a production environment when
   deploying


## Deployment

If you are interested in an out-of-the-box deployment automation, check out accompanying
[`cookiecutter-flask-ansible`](https://github.com/candidtim/cookiecutter-flask-ansible).

Or, check out [Deploying with Fabric](http://flask.pocoo.org/docs/0.12/patterns/fabric/#fabric-deployment) on one of the
possible ways to automate the deployment.

In either case, generally the idea is to build a package (`make sdist`), deliver it to a server (`scp ...`),
install it (`pip install uceasy.tar.gz`), ensure that configuration file exists and
`UCEASY_SETTINGS` environment variable points to it, ensure that user has access to the
working directory to create and write log files in it, and finally run a
[WSGI container](http://flask.pocoo.org/docs/0.12/deploying/wsgi-standalone/) with the application.
And, most likely, it will also run behind a
[reverse proxy](http://flask.pocoo.org/docs/0.12/deploying/wsgi-standalone/#proxy-setups).
