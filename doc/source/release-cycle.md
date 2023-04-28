# Release cycle

We'll discuss here how releases are made and what is the current choice of
software that is included in the distribution.

## Schedule

The release of Model W happens quarterly:

-   **1st Monday of January** (January 2, 2023)
-   **1st Monday of April** (April 3, 2023)
-   **1st Monday of July** (July 3, 2023)
-   **1st Monday of October** (October 2, 2023)

The cycle for each release will be like this:

-   **Development** (4 weeks) &mdash; In this phase the new release will be
    developed. Ideal versions of each software will be decided and all Model W
    packages and documentation will be updated and tested to reach this target.
-   **Pilot** (4 weeks) &mdash; A pilot project will be selected to test the
    upcoming release
-   **Roll-out** (3 months) &mdash; All projects must migrate to the new Model W
    release
-   **Support** (3 months) &mdash; After 3 month, when a new version comes out,
    the old version stays supported for 3 more months to give time to projects
    to make their roll-out
-   **LTS** (until 2 years after release) &mdash; Some versions will receive
    long-term support, as explained below

The above procedure is for long-lived projects. Some projects are considered
temporary if they meet all the following criterion:

-   They won't be online more than one year
-   The maintenance is not expected to be intensive
-   It is not expected that new features will be added

In that case, instead of using the latest Model W version, temporary projects
will use the latest LTS version.

> _Note_ &mdash; As Model W encompasses many dependencies, the 2 years goal for
> LTS releases will be kept afloat as long as possible, however the security
> coverage will have to depend on what is available upstream.

The LTS release will be made at the same time as the July release but might
contain different software versions to make sure that the underlying software is
also in LTS version. Otherwise, the normal release might receive a downgrade,
which is definitely not advised.

At a given point in time, there might be 4 releases supported:

-   Normal release &mdash; Current
-   Normal release &mdash; Previous
-   LTS &mdash; Current
-   LTS &mdash; Previous

## This repo

This repo contains the documentation. The `develop` branch matches the
development cycle of the release. Each release will then receive a PEP-440
version number in the format `<year>.<month>` which will be tagged. LTS releases
might receive their own branch.

## Versions

The latest release is `2023.03`. THe latest LTS release is `2023.03`.

The versions detailed below are the one for this release.

### Model W packages

All Model W packages follow the same release logic. For example, the January
2023 release will be versioned `2023.01`. The version number is used in all the
packages and they all are guaranteed to work together.

Which means that in order to switch from one version of Model W to another, you
mainly need to change the version number of those packages in your requirements.
Then you'll run into updating issues and so forth.

### Python

Versions are decided by checking at the time of entering development phase which
are the highest mutually compatible versions of Django, Numpy, SciPy, Pandas and
Python.

```{note}
We don't use Numpy and friends so much but since they are often picky about the
Python version it has been decided to include them.
```

-   [Python](https://endoflife.date/python) &mdash; Version `~3.10`
-   Web Stuff
    -   [Django](https://www.djangoproject.com/download/) &mdash; Version `~4.1`
    -   [Django REST Framework](https://www.django-rest-framework.org/community/release-notes/)
        &mdash; Version `~3.14`
    -   [Celery](https://github.com/celery/celery/releases) &mdash; Version
        `~5.2`
    -   [Wagtail](https://docs.wagtail.io/en/stable/releases/index.html) &mdash;
        Version `~4.1`
    -   [Channels](https://channels.readthedocs.io/en/stable/releases/index.html)
        &mdash; Version `~4.0`
    -   [Django Postgres Extra](https://django-postgres-extra.readthedocs.io/en/latest/major_releases.html)
        &mdash; Version `~2.0`
    -   [Wailer](https://github.com/WithAgency/Wailer/tags) &mdash; Version
        `~1.0`
-   Annoying compiled stuff
    -   [Numpy](https://numpy.org/news/) &mdash; Version `~1.23`
    -   [TensorFlow](https://github.com/tensorflow/tensorflow/releases) &mdash;
        Version `~2.11`
    -   [Pandas](https://pandas.pydata.org/docs/whatsnew/index.html) &mdash;
        Version `~1.4`

### JavaScript

-   [Node](https://nodejs.org/en/about/releases/) &mdash; Version `^18`
-   [Vue](https://endoflife.date/vue) &mdash; Version `~3.2`
-   [Nuxt](https://nuxtjs.org/releases) &mdash; Version `~3.4`

```{note}
Vlang is favored as a translation package for the front-end
as it provides a simple workflow to work with project managers and clients.
It's a bit rough technically but anyone is encouraged to contribute to improve
it.
```

### Databases

-   [PostgreSQL](https://www.postgresql.org/support/versioning/) &mdash; Version
    `^15`
-   [Redis](https://redis.io/topics/release-notes) &mdash; Version `^7`

## Adopting a new release

Switching to a new version of Model W is simple:

-   Update the first line of the `Dockerfile` under both `api` and `front`
-   Update the `modelw-preset-*` packages  inside `api/pyproject.toml` and inside `front/package.json`
-   Don't forget to run `poetry update` as well as `npm install`
-   `git push`
-   ???
-   Profit
