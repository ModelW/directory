# Transforming an Existing Project

So you've got an existing project, and you need to transform it. Here are a few
key points to check.

## Repo structure

The first thing is to make sure that all the components are stored in the same
repo (as opposed to the legacy way of having several repos for several
components).

You should steal from the
[template](https://github.com/ModelW/project-maker/tree/develop/src/model_w/project_maker/template)
the different `.editorconfig`, `.formatignore`, `.gitignore` and `.prettierrc`
files.

## API

There is obviously no single way to do this correctly as pre-existing projects
are quite varied, however let's cover the most important topics.

### Poetry

We switch the dependency manager from `pip` to `poetry`. You can proceed as
follows:

-   Run `poetry init` to create the `pyproject.toml` file for the current
    project
-   Use the `requirements.in` or `requirements.txt` file of the existing project
    to fill up the dependencies in `pyproject.toml`. Please take into account
    the fact that Poetry supports semver dependency specification, so for each
    package don't hesitate to specify a version that suits you.
-   Overall, a lot of dependencies are already included by the preset, so the
    most important one to put there is the `modelw-preset-django`.
-   Make sure to have a valid `tool.poetry.packages` section, otherwise some
    things might break

### Settings

The settings are now 100% driven by environment variables. This used to be done
by calling directly `getenv()`, however now the presets and the env manager
provide an easy way to do this.

Basically you need to scrap away your existing `settings.py` file and re-write
it in a much more simple way using the
[Preset](https://modelw-django-preset.readthedocs.io/en/latest/).

In order to do this cleanly, you will need to remove most of the items from the
file in order to only keep those that are not already managed by the preset.
Read the
[Preset documentation](https://modelw-django-preset.readthedocs.io/en/latest/)
to know more about it.

### Dockerfiles

An important point of Model&#8239;W is to provide an easy way to make
Dockerfiles, which allows to easily deploy projects into containerized
environments.

First, copy your `.gitignore` into a `.dockerignore` file at the root of each
component.

Then, create a `Dockerfile` with the following content:

```dockerfile
FROM modelw/base:2024.04

# Use EITHER that for Django:
COPY --chown=user pyproject.toml poetry.lock ./
# OR that for Nuxt:
COPY --chown=user ./package.json ./package-lock.json ./

RUN modelw-docker install

COPY --chown=user . .

RUN modelw-docker build

CMD ["modelw-docker", "serve"]
```

If you build the image, it should work out of the box. If not, it's probably
that you need further steps of adaptation of the project.

In case you also have a Celery, you can configure different containers on the
same image with a different command, for example:

```dockerfile
# For Celery Worker
CMD ["modelw-docker", "serve", "celery"]

# For Celery Beat
CMD ["modelw-docker", "serve", "beat"]
```
