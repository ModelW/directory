# Prerequisites

In order to be able to use Model W there is a given set of prerequisites that
you need to respect.

## Operating system

For now Model W is tested only on Linux. It will likely work on other UNIX
systems like macOS but if you want to work on Windows you're probably out of
luck.

Specifically, the instructions here are going to be given for Debian-based Linux
distributions.

If you're using anything else, feel free to contribute to this documentation and
make it more generic.

## Development tools

You need obviously to have a bunch of development tools installed on your
system. The following list is not exhaustive, but it should give you a good idea
of what you need:

```bash
sudo apt-get update

sudo apt-get install -y \
    git \
    gdal-bin \
    build-essential \
    libssl-dev \
    zlib1g-dev \
    libbz2-dev \
    libreadline-dev \
    libsqlite3-dev \
    curl \
    llvm \
    libncursesw5-dev \
    xz-utils \
    tk-dev \
    libxml2-dev \
    libxmlsec1-dev \
    libffi-dev \
    liblzma-dev
```

In addition, you might want to install PostgreSQL at its latest version:

```bash
sudo apt-get install -y curl ca-certificates gnupg
curl https://www.postgresql.org/media/keys/ACCC4CF8.asc | sudo gpg --dearmor --output /etc/apt/trusted.gpg.d/apt.postgresql.org.gpg
sudo bash -c 'echo "deb [signed-by=/etc/apt/trusted.gpg.d/apt.postgresql.org.gpg] https://apt.postgresql.org/pub/repos/apt $(lsb_release -cs)-pgdg main" > /etc/apt/sources.list.d/pgdg.list'
sudo apt-get update
sudo apt-get install -y postgresql-15 libpq-dev
```

If you've already got PostgreSQL installed, make sure to at least have
`libpq-dev`.

Finally, you might want to install Redis. The one from the system is usually
fine.

```bash
sudo apt-get install -y redis-server
```

## Language versions

A big point of Model W is to give the tempo for language version upgrades. This
means that you need to be in control of which version you're using at a given
point in time.

### Python

What we recommend for Python is to use [pyenv](https://github.com/pyenv/pyenv).

```bash
curl https://pyenv.run | bash
```

Once it's done, you can install the version of Python that you want to use:

```bash
pyenv install 3.11
```

And use it system-wide:

```bash
pyenv global 3.11
```

```{note}
Each new version of Model W will potentially impose a new version of Python. It
will be a good idea to install it at that time and to set it as the global
version.
```

### Node

For Node, while you could use NVM, the simplest is probably just to use the
packaged Node versions for Debian.

```bash
curl https://deb.nodesource.com/gpgkey/nodesource.gpg.key | sudo gpg --dearmor --output /etc/apt/trusted.gpg.d/nodesource.gpg
sudo bash -c 'echo "deb [signed-by=/etc/apt/trusted.gpg.d/nodesource.gpg] https://deb.nodesource.com/node_20.x $(lsb_release -cs) main" > /etc/apt/sources.list.d/pgdg.list'
```

```{note}
You can see there that we're installing version 18. When the Model W upgrade
happens you can switch the version in the sources and use the new one instead.
```

## Package management

The Node side is already covered by default, however for Python we'll diverge
from Pip, and we'll use Poetry.

The simplest to use Poetry is to install it with the default installer:

```bash
curl -sSL https://install.python-poetry.org | python3 -
```

### Poetry and Python version

Poetry itself has its own virtual environment and will run independently of the
Python version you're using. Now, it will detect which version of Python you
enabled when doing a `poetry install` and will use it to create the virtualenv
for your project.

To set up the environment for backend work properly the first thing we need to do is to create a
new environment with [poetry](https://python-poetry.org/docs/) and [pyenv](https://github.com/pyenv/pyenv).
You can also follow the steps described in the documentation of [ModelW](https://model-w.readthedocs.io/en/latest/prerequisites.html#development-tools)

By this way we can isolate the different dependencies from other projects.

To install the dependencies declared inside the file poetry.lock.
You have to follow the next steps:

Declare the python version by pyenv
```bash
pyenv local 3.10.9 # tells pyenv to configure a env with local coverage to use a specific version of python
```
Then we have to specify to poetry which env he has to use, it's done by
```bash
poetry env use <home of your pyenv>/versions/3.10.9/bin/python # tells to poetry what python it has to use
```
And with this specification we can follow to install all the dependencies from pyproject.toml by:
```bash
poetry install # installs the dependencies from pyproject
```

If you are using and IDE like Pycharm, you can configure the poetry env to be the one used by built commands

```bash
cd /my/project/dir
pyenv shell 3.10.10  # activates this python version just in the local shell
PYTHON_BIN=`pyenv which python`  # tells you where the binary is installed
poetry env use $PYTHON_BIN  # tells poetry to use this binary
```
