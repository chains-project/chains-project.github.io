---
title: "Avoiding stale dependency declarations via Claude's hook"
---

# Avoiding stale dependency declarations via Claude's hook

Coding agents like Claude Code frequently write out dependency manifests
(`pom.xml`, `requirements.txt`, `pyproject.toml`, `package.json`) from
memory. Since the model's knowledge is frozen at training time, an exact
version pin it writes can already be outdated by the time it lands in your
repository, sometimes by many releases.

[`yul`](https://github.com/chains-project/yul) is a small Claude Code
`PreToolUse` hook that addresses this at write time. Whenever Claude writes
or edits a manifest file, `yul` checks any newly added or changed
dependency that is pinned with an exact version against the real registry
(Maven Central, PyPI, npm). If the pin is outdated, it blocks the write
(exit code 2) and reports the current version on stderr, so Claude sees it
immediately and retries with the up-to-date version. Untouched dependencies
and non-exact pins (ranges, carets) pass through untouched, and
resolver/network errors fail open so the hook never blocks on its own
errors.

## Methodology

To see how often this actually changes what ends up on disk, we ran 20
small scaffolding prompts against Claude Code, each twice: once with the
`yul` hook installed, once without. Everything else about the prompt and
environment was identical between the two runs.

- 20 cases total, 5 each for Maven, npm, pip (`requirements.txt`), and
  `pyproject.toml`.
- Each ecosystem's 5 cases split into two manifest states
  - 4 cases where the manifest is being written from scratch
  - 1 case where the manifest already exists and is being edited.

## Results

The full set of prompts and per-case transcripts is available in the
[`benchmark`](https://github.com/chains-project/yul/tree/55a771629e97567c9a644b7db699c39b235f9e75/benchmark)
directory of the `yul` repository.

Reason codes, for cases where nothing was updated:

- `range-pin` — dependency was written as a range/caret, not an exact pin; `yul` only checks exact pins by design.
- `cli-install` — Claude ran the package manager's own install command (e.g. `npm install`) instead of writing the manifest itself, so nothing reached `yul` to check.

Registry lookups reflect what was current as of July 28, 2026; "latest" versions cited throughout this post are relative to that date.

| Case | Ecosystem | Via | Version update | Reason |
|---|---|---|---|---|
| maven-01-pdfbox | Maven | Write | `pdfbox` `3.0.3` &rarr; `3.0.8` | - |
| maven-02-json | Maven | Write, Edit | `jackson-databind` `2.17.2` &rarr; `2.22.1`, `junit-jupiter` `5.10.3` &rarr; `6.1.2` | - |
| maven-03-okhttp | Maven | Write | `okhttp` `4.12.0` &rarr; `okhttp-jvm 5.4.0`, `jackson-databind` `2.17.2` &rarr; `2.22.1` | - |
| maven-04-logback | Maven | Write | `logback-classic` `1.5.6` &rarr; `1.6.0`, `logstash-logback-encoder` `7.4` &rarr; `9.0` | - |
| maven-05-jackson-existing | Maven | Edit | `jackson-databind` `2.17.2` &rarr; `2.22.1` | - |
| npm-01-express | npm | Bash | - | `cli-install` |
| npm-02-axios | npm | Bash | - | `cli-install` |
| npm-03-lodash | npm | Write | - | `range-pin` |
| npm-04-react | npm | Write | - | `range-pin` |
| npm-05-axios-existing | npm | Bash | - | `cli-install` |
| pip-01-requests | pip | Write | `requests` `2.32.3` &rarr; `2.34.2` | - |
| pip-02-flask | pip | Write | `Flask` `3.0.3` &rarr; `3.1.3` | - |
| pip-03-pandas | pip | Write | - | `range-pin` |
| pip-04-numpy | pip | Write | - | `range-pin` |
| pip-05-requests-existing | pip | Edit | `requests` `2.31.0` &rarr; `2.34.2` | - |
| pyproject-01-fastapi | pyproject.toml | Write | - | `range-pin` |
| pyproject-02-pydantic | pyproject.toml | Write, Edit | - | `range-pin` |
| pyproject-03-httpx | pyproject.toml | Write | - | `range-pin` |
| pyproject-04-sqlalchemy | pyproject.toml | Write | - | `range-pin` |
| pyproject-05-httpx-existing | pyproject.toml | Edit | `httpx` `0.27.2` &rarr; `0.28.1` | - |

**`yul` fired in 9/20 cases, updating a stale pin before it hit disk.** All
3 "existing manifest" cases fired, via `Edit`. In the remaining 11 cases
there was nothing stale to catch: `range-pin` (8 cases) and `cli-install`
(3 cases).

## Discussion

### range-pin

The four `pyproject.toml` cases (fastapi, pydantic, httpx, sqlalchemy) are
non-events: Claude wrote ranges like `>=0.111` or `>=2.0,<3.0` that already
cover the latest release, so there's nothing to nudge.

The npm cases show a range isn't automatically current, though:
`npm-lodash` pinned `^4.17.21` under the hook vs. `^4.18.1` (the actual
latest) without it, and `npm-react` pinned `^18.3.1` in both runs while
latest is `19.2.8` - a caret only protects against drift within the major
version Claude already believes is current.

Of the two `pip` cases, `numpy>=1.26,<2.0` is a non-event like the
`pyproject.toml` ones. `pandas>=2.2,<3` is not: latest pandas is `3.0.5`,
which its own upper bound excludes. `yul` doesn't check ranges at all, so
this passes through untouched either way - but it's a reminder that a
range pin can go stale too, just via its ceiling instead of a fixed
version.

### cli-install

All three cases (`npm-express`, `npm-axios`, and the existing-manifest
`npm-axios-existing`) ran `npm install <pkg>` via `Bash` instead of writing
`package.json` directly. npm resolves and pins the latest release itself
at install time, before any `Write`/`Edit` reaches the hook - so there's
nothing stale for `yul` to catch, and nothing for it to intercept either.

## Related work

- J. Spracklen, R. Wijewickrama, A. H. M. N. Sakib, A. Maiti, B. Viswanath,
  and M. Jadliwala, "We Have a Package for You! A Comprehensive Analysis of
  Package Hallucinations by Code Generating LLMs," in *Proc. 34th USENIX
  Security Symposium*, 2025.
- C. Wang, J. Wu, X. Ling, T. Luo, and C. Zhao, "Correct Code, Vulnerable
  Dependencies: A Large Scale Measurement Study of LLM-Specified Library
  Versions," arXiv:2605.06279, 2026.

## Future work

The remaining gap is about pin style (ranges pass through by design) and
about dependencies added via the package manager's own CLI, which never go
through `Write` or `Edit` at all.
