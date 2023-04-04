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
system. The following list is not exhaustive but it should give you a good idea
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
sudo bash -c 'echo "deb [signed-by=/etc/apt/trusted.gpg.d/apt.postgresql.org.gpg] http://apt.postgresql.org/pub/repos/apt $(lsb_release -cs)-pgdg main" > /etc/apt/sources.list.d/pgdg.list'
sudo apt-get update
sudo apt-get install -y postgresql-14 libpq-dev
```

If you've already got PostgreSQL installed, make sure to at least have
`libpq-dev`.

Finally you might want to install Redis. The one from the system is usually
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
pyenv install 3.10.5
```

And use it system-wide:

```bash
pyenv global 3.10.5
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
sudo bash -c 'echo "deb [signed-by=/etc/apt/trusted.gpg.d/nodesource.gpg] https://deb.nodesource.com/node_16.x $(lsb_release -cs) main" > /etc/apt/sources.list.d/pgdg.list'
```

```{note}
You can see there that we're installing version 16. When the Model W upgrade
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

If you always activate the right Python version in a `global` way with pyenv,
you should be fine. In doubt, Poetry can be configured to use a specific Python
version for a given project.

```bash
cd /my/project/dir
pyenv shell 3.10.5  # activates this python version just in the local shell
PYTHON_BIN=`pyenv which python`  # tells you where the binary is installed
poetry env use $PYTHON_BIN  # tells poetry to use this binary
```
