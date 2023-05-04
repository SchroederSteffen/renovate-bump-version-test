# Renovate versioning bumping test

This repository demonstrates the [bumpVersion](https://docs.renovatebot.com/configuration-options/#bumpversion) behavior of [Renovate](https://docs.renovatebot.com/) when only the `package-lock.json` but not the `package.json` is touched.

## Setup

This repository uses Renovate's `base` configuration and sets `bumpVersion: patch`.

The package requires `renovate@34` and has it locked in the `package-lock.json` to version `34.159.0` which is NOT the latest version matching the range `34`.

This lets Renovate create two PRs:

- <https://github.com/SchroederSteffen/renovate-bump-version-test/pull/4> to bump the -lock file to the latest v34 (`34.160.0`)
- <https://github.com/SchroederSteffen/renovate-bump-version-test/pull/5> to bump the package to the latest v35

## Observation

Unfortunately, only the PR for the major version (#5) also bumps the `version` in the `package.json`.

The other PR (#4, only doing lock file maintenance), doesn't bump the version.

## Expectation

We (Renovate user) expect it to update the `version` in any case, but currently it only updates it if the `package.json` is touched.
