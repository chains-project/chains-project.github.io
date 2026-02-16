---
title: CHAINS Software Supply Chain Checklist
---

This is a checklist for best practices in software supply chain security.

## Basic Security Requirements

| Rule | Check ✅|
|----------|----------|
| use dependency update bot (dependabot, renovate) |          |
| require code review before merging PRs |          |
| run security scanners in CI (CodeQL, Snyk, etc.) |          |
| use branch / tag protection rules |          |
| have 2FA enabled for all project members |          |

## Medium Security Requirements

| Rule | Check ✅|
|----------|----------|
| forbid transient dependencies in CI (no latest, SNAPSHOT, etc.) |          |
| forbid coarse-grain version (v45), force pinned, most specific, immutable version (v45.0.1)   |          |
| push lockfile in repo (maven-lockfile) |          |
| block bad dependencies in ci (dirty-waters) |          |
| automated creation of release tag |          |
| automated creation of SBOMs for releases |          |

## High Security Requirements

| Rule | Check ✅|
|----------|----------|
| forbid unsigned git commits (impossible to do on Github)|          |
| push build attestations for releases to a transparency logs (rekor) |          |
| have independent rebuilders (reproducible-central) |          |
| verify dependency crypto signatures from a trusted source |          |
| use a dynamic CI hardener [eg harden-runner](https://github.com/step-security/harden-runner) |          |
