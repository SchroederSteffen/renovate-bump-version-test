# Renovate versioning bumping test

This repository demonstrates the [bumpVersion](https://docs.renovatebot.com/configuration-options/#bumpversion) behavior of [Renovate](https://docs.renovatebot.com/) when only the `package-lock.json` but not the `package.json` is touched.

Reproduction for https://github.com/renovatebot/renovate/issues/21996 / https://github.com/renovatebot/renovate/discussions/21972.

## Setup

This repository uses Renovate's `base` configuration, sets `bumpVersion: patch` and enables `lockFileMaintenance`.

The package requires `renovate@34` and has it locked in the `package-lock.json` to version `34.159.0` which is NOT the latest version matching the range `34`.

This lets Renovate create three PRs:

- <https://github.com/SchroederSteffen/renovate-bump-version-test/pull/4> to bump the -lock file to the latest v34 (`34.160.0`)
- <https://github.com/SchroederSteffen/renovate-bump-version-test/pull/5> to bump the package to the latest v35
- <https://github.com/SchroederSteffen/renovate-bump-version-test/pull/6> to maintain the lock file

## Observation

Unfortunately, only the PR for the major version (#5) also bumps the `version` in the `package.json`.

The other PRs (#4 & #6) don't bump the version.

## Expectation

We expect it to update the `version` in any case (for all PRs).
