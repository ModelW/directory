# Releasing

This part of the documentation is more destined for maintainers that will be
releasing Model W every quarter. We're describing, as a checklist, the steps to
follow in order to release a new major version of Model W.

## Presets

The simplest way to make sure that the dependencies can resolve is to upgrade
the dependencies of the presets.

You'll find in there every single important dependency. You need to decide which
version to use.

1. Change the version to the target version
2. Run `poetry update`/`npm install` to make sure that the dependencies are
   resolved (don't hesitate to remove `node_modules` and `package-lock.json` in
   the Nuxt preset)
3. Test the new preset by running the template project while installing your
   local preset instead of the published one

This is the simplified procedure. You might need to fight a bit. Once done, you
can finally make a beta release of the new revision.

## Docker

You need to reflect the changes in the way the Docker image is made.

1. Update the Dockerfile to use the right version of Python and Node
2. Use the project maker to create a project called `Docker Demo`, picking all
   features save for Wagtail, and replace `demo` with this new project
3. Keep the Dockerfiles in `demo` as-is however, using `FROM modelw-base-test`
4. Test it locally using `make build_test_api build_test_front`

When happy:

1. Add the new major release in the matrix of the scheduled builds.
2. Make a beta release of the Docker image.

## Project Maker

Go in the project maker and modify dependencies:

1. Change the version of the presets to the new beta version
2. Change the `pyproject.toml` and `package.json` to otherwise be updated in all
   the ways that need to be (non-preset dependencies, new content to put, etc.)
3. Test the template projects to see if it makes sense
4. Generate different projects to see if the generation in itself works
5. Make sure that the templated Dockerfiles reference the right version in the
   `FROM` instruction

When all seems reasonable, make a beta release of the project maker.

## Directory (this repository)

Start by checking the [release cycle](release-cycle.md) part of the document
and:

1. Update the part that says "The latest release is XXXX.XX" to match the name
   of the release you're about to do
2. Report version numbers that you've decided in the presets

When you're done, make a beta release of this repo.

## Wrap up

For each repository, after making the beta release, you must start a new support
branch based on the newly created tag.

When you've had people test your beta versions, go through all the steps again
and make a non-beta release.
