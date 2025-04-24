---
title: CHAINS Software Supply Chain Competition
---

This is a competition based on a checklist for best practices in software supply chain security.

Name: ______________  
Repo: ______________

| Rule | Check ✅|
|----------|----------|
| forbid unsigned git commits and tags (impossible to do on Github)|          |
| forbid transient dependencies in CI (no latest, SNAPSHOT, etc.) |          |
| forbid coarse-grain version (v45), force most specific, immutable version (v45.0.1)   |          |
| use dependency update bot (dependabot, renovate) |          |
| push lockfile in repo (maven-lockfile) |          |
| block bad dependencies in ci (dirty-waters) |          |
| require code review before merging PRs |          |
| run security scanners in CI (CodeQL, Snyk, etc.) |          |
| automated creation of release tag |          |
| automated creation of SBOMs for releases |          |
| push build attestations for releases (rekor) |          |
| have independent rebuilders (reproducible-central) |          |
| use branch / tag protection rules |          |
| verify dependency crypto signatures from a trusted source |          |
| have 2FA enabled for all project members |          |
| Total score  |          |
