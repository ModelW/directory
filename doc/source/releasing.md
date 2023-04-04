# Releasing

This part of the documentation is more destined for maintainers that will be
releasing Model W every quarter. We're describing, as a checklist, the steps to
follow in order to release a new major version of Model W.

## Presets

The simplest way to make sure that the dependencies can resolve is to upgrade
the dependencies of the presets.

```{note}
For now there is no Nuxt preset, the best substitute is to check the Project
Maker template for the front-end.
```

You'll find in there every single important dependency. You need to decide which
version to use.

1. Change the version to the target version
2. Run `poetry update` to make sure that the dependencies are resolved
3. Test the new preset by running the template project while installing your
   local preset instead of the published one

This is the simplified procedure. You might need to fight a bit. Once done, you
can finally make a beta release of the new revision.

## This repo

Start by checking the [release cycle](release-cycle.md) part of the document
and:

-   Update the part that says "The latest release is XXX" to match the name of
    the release you're about to do
-   Report version numbers that you've decided in the presets

When you're done, make a beta release of this repo.

## Project Maker

Go in the project maker and modify dependencies:

-   Change the version of the presets to the new beta version
-   Change the `pyproject.toml` and `package.json` to otherwise be updated in
    all the ways that need to be (non-preset dependencies, new content to put,
    etc)
-   Test the template projects to see if it makes sense
-   Generate different projects to see if the generation in itself works
-   Make sure that the templated Dockerfiles reference the right version in the
    FROM instruction

When all seems reasonable, make a beta release of the project maker.

## Docker

You need to reflect the changes in the way the Docker image is made.

-   Update the Dockerfile to use the right version of Python and Node
-   Also make sure to update the Dockerfile to get the modelw-docker package at
    the right major revision
-   Make sure that the `demo` folder matches the new output of the project
    maker.
-   Test it locally

When happy:

-   Make a beta release of the Docker image.
-   Start a support branch from this release.
-   Add the new major release in the matrix of the scheduled builds.

## Wrap up

When you've had people test your beta versions, go through all the steps again
and make a non-beta release.
