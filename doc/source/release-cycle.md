# Release cycle

We'll discuss here how releases are made and what is the current choice of
software that is included in the distribution.

## Schedule

The release of Model W happens quarterly:

-   **1st Monday of January** (January 2, 2023)
-   **1st Monday of April** (April 3, 2023)
-   **1st Monday of July** (July 3, 2023)
-   **1st Monday of October** (October 3, 2022)

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

### Python

Versions are decided by checking at the time of entering development phase which
are the highest mutually compatible versions of Django, Numpy, SciPy, Pandas and
Python.

We don't use Numpy and friends so much but since they are often picky about the
Python version it has been decided to include them.

-   [Python](https://endoflife.date/python) &mdash; Version `~3.10`
-   [Django](https://www.djangoproject.com/download/) &mdash; Version `~4.1`
-   [Numpy](https://numpy.org/news/) &mdash; Version `~1.23`
-   [Pandas](https://pandas.pydata.org/docs/whatsnew/index.html) &mdash; Version
    `~1.4`

-   Model W packages
    -   DRF pagination
-   Sentry
-   Sending emails ???
