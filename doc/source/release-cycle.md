# Release cycle

We'll discuss here how releases are made and what is the current choice of
software that is included in the distribution.

## Schedule

The release of Model W happens quarterly:

-   **1st Monday of January** (January 5, 2026)
-   **1st Monday of April** (April 6, 2026)
-   **1st Monday of July** (July 6, 2026)
-   **1st Monday of October** (October 5, 2026)

The cycle for each release will be like this:

-   **Development** (4 weeks) &mdash; In this phase the new release will be
    developed. Ideal versions of each software will be decided and all Model W
    packages and documentation will be updated and tested to reach this target.
-   **Pilot** (4 weeks) &mdash; A pilot project will be selected to test the
    upcoming release
-   **Roll-out** (3 months) &mdash; All projects must migrate to the new Model W
    release
-   **Support** (3 months) &mdash; After 3 month, when a new version comes out,
    the three previous versions stays supported for 3 more months to give time
    to projects to make their roll-out.

At any given point in time, there will be 4 releases supported. The latest
release and the three previous ones.

## This repo

This repo contains the documentation. The `develop` branch matches the
development cycle of the release. Each release will then receive a PEP-440
version number in the format `<year>.<month>` which will be tagged.

## Versions

The latest release is `2026.01`.

The versions detailed below are the one for this release.

### Model W packages

All Model W packages follow the same release logic. For example, the January
2023 release will be versioned `2023.01`. The version number is used in all the
packages, and they all are guaranteed to work together.

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

-   [Python](https://endoflife.date/python) &mdash; Version `~3.14`
-   Web Stuff
    -   [Django](https://www.djangoproject.com/download/) &mdash; Version `~6.0`
    -   [Django REST Framework](https://www.django-rest-framework.org/community/release-notes/)
        &mdash; Version `~3.16`
    -   [Procrastinate](https://github.com/procrastinate-org/procrastinate)
        &mdash; Version `~3.6`
    -   [Wagtail](https://docs.wagtail.io/en/stable/releases/index.html) &mdash;
        Version `~7.2`
    -   [Channels](https://channels.readthedocs.io/en/stable/releases/index.html)
        &mdash; Version `~4.3`
    -   [Django Postgres Extra](https://django-postgres-extra.readthedocs.io/en/latest/major_releases.html)
        &mdash; Version `~2.0`
    -   [Wailer](https://github.com/WithAgency/Wailer/tags) &mdash; Version
        `~1.0`
-   Annoying compiled stuff
    -   [Numpy](https://numpy.org/news/) &mdash; Version `~2.4`
    -   [Pandas](https://pandas.pydata.org/docs/whatsnew/index.html) &mdash;
        Version `~2.3`

### JavaScript

-   [Node](https://nodejs.org/en/about/releases/) &mdash; Version `^24`
-   [Svelte](https://www.npmjs.com/package/svelte) &mdash; Version `~5.46`
-   [SvelteKit](https://www.npmjs.com/package/@sveltejs/kit) &mdash; Version
    `~2.49`

### Databases

-   [PostgreSQL](https://www.postgresql.org/support/versioning/) &mdash; Version
    `^15`
-   [Redis](https://redis.io/topics/release-notes) &mdash; Version `^7`

## Adopting a new release

Switching to a new version of Model W is simple:

-   Update poetry and npm to their latest versions
-   Update the first line of the `Dockerfile` under both `api` and `front`
-   Update the `modelw-preset-*` packages inside `api/pyproject.toml` and inside
    `front/package.json`
-   Run `poetry update` as well as `npm update` to update all dependencies to their latest versions
-   Test the project locally
-   `git push`
-   Check the security tab in GitHub to make sure it's zero
-   Test the deployment
