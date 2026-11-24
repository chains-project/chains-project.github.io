---
title: "A Look at Lean's Package Manager, Lake and Reservoir"
---

# A Look at Lean's Package Manager, Lake and Reservoir

[Lean 4](https://lean-lang.org/) is a programming language and theorem prover.
Four pieces are involved in getting and building its packages.

- The [Lean toolchain](https://github.com/leanprover/lean4/releases) is one release of Lean. It bundles the `lean` compiler, Lake and the core libraries, and is named by a GitHub repository and release tag, such as `leanprover/lean4:v4.36.0`.
- [Lake](https://github.com/leanprover/lean4/tree/master/src/lake) is the build tool and package manager that ships with every toolchain.
- [Reservoir](https://reservoir.lean-lang.org/) is the package registry.
- [elan](https://github.com/leanprover/elan) is the toolchain manager. It installs the compiler version named in a project's `lean-toolchain` file.

This post goes through the quirks we found in Lake and Reservoir and what they mean for supply chain security.

## TL;DR

- **The manifest is `lakefile.toml` and the lockfile is `lake-manifest.json`.** The manifest can be declarative because TOML is a declarative configuration language. It can also be imperative when written as a Lean program in `lakefile.lean`.
- **Source by default and binaries decided upstream.** Packages are Git repositories. Lake clones each one into `.lake/packages` and builds it locally. This is similar to `node_modules`. Some packages still arrive as prebuilt binaries. Their developer or Lake decides this and not the downstream user.
- **Conflicting versions.** A package can be referred to by its Git commit or by a Git reference such as a tag or branch. It can also be referred to by the `version` in its manifest. These can conflict.
- **Mutable references and locked commits.** The manifest allows branches and tags. The lockfile still pins every dependency to a commit SHA.
- **The commit SHA is the only integrity check.** Lake keeps no checksum of package contents.
- **The lockfile is compulsory.** `lake build` only reads the lockfile. A new dependency needs a `lake update` before it builds.
- **The lockfile is flat.** It says whether a dependency is direct or inherited. It does not say how deep it sits or who pulled it in.
- **Post-install hooks exist.** Every package in the workspace can run a `post_update` hook much like npm's `postinstall`.
- **The registry indexes source but hosts binaries.** Reservoir does not store source code. It indexes GitHub repositories and builds each one with its own toolchain and the latest Lean releases. It keeps those builds and serves them as prebuilt binaries.
- **No dependency conflict resolution.** Two dependencies can depend on different versions of the same package. Lake has no way to resolve a version that works for both. A conflict is only reported as a compile error when it breaks an API.

## The manifest is `lakefile.toml` and the lockfile is `lake-manifest.json`

The manifest comes in two forms.
The TOML form is declarative.

```toml
name = "hello"

[[require]]
name = "mathlib"
scope = "leanprover-community"
rev = "v4.36.0"
```

The Lean form is imperative, because it is a Lean program.

```lean
import Lake
open Lake DSL

package hello

require "leanprover-community" / "mathlib" @ git "v4.36.0"
```

Running `lake update` resolves either form into the lockfile.

## Source by default and binaries decided upstream

Every dependency source is cloned into `.lake/packages` inside the project and compiled from source.
However, building from source can take hours, so Lake also downloads prebuilt binaries in three cases.

- **Reservoir builds.** Since Lean v4.13.0, Lake downloads a prebuilt archive from Reservoir for every package in the `leanprover` and `leanprover-community` scopes, such as batteries. Nobody opts in. Reservoir lists a hash for each archive, but Lake does not check it before unpacking.
- **mathlib's cache.** `lake exe cache get` is mathlib's own tool. It downloads prebuilt `.olean` files for the locked mathlib commit. Mathlib runs it through its own `post_update` hook, so every project that depends on mathlib downloads these files on `lake update` by default.
- **GitHub releases.** `preferReleaseBuild := true` makes Lake download a package's build archive from its GitHub release, uploaded with `lake upload`. The package's developer sets this in their own manifest.

In every case the choice is made upstream, by Lake or by the package's developer, not by the downstream user.
The user can only opt out, with `lake build --no-cache` or `MATHLIB_NO_CACHE_ON_UPDATE=1`.

## Conflicting versions

There are two ways to declare a package's version.

### The `version` field in the manifest

```toml
# foo's manifest (lakefile.toml)
name = "foo"
version = "1.2.0"

# consumer's manifest (lakefile.toml)
[[require]]
name = "foo"
scope = "alice"
version = "1.2.0"
```

### A Git revision

```toml
# foo's GitHub repository
# release tagged v1.2.0

# consumer's manifest (lakefile.toml)
[[require]]
name = "foo"
scope = "alice"
rev = "v1.2.0"  # a tag, branch or commit
```

Nothing keeps the two in sync.
All 123 mathlib revisions indexed by Reservoir report version `0.0.0`, while their Git tags follow Lean releases (`v4.36.0`, `v4.37.0-rc1`).
This is probably done intentionally to ensure there is only one source of truth for the version.

## Mutable references and locked commits

Requirements may point at branches and tags, both of which can be moved or force-pushed.

```toml
[[require]]
name = "mathlib"
scope = "leanprover-community"
rev = "v4.36.0"
```

The lockfile stores that request (`inputRev`) next to the commit it resolved to (`rev`).
This keeps the version pinned even if the tag is moved.

```json
{"name": "mathlib",
 "scope": "leanprover-community",
 "url": "https://github.com/leanprover-community/mathlib4",
 "inputRev": "v4.36.0",
 "rev": "fc4f59e577feb1a4956671bc04ac18aaaf8cd842",
 "inherited": false}
```

## The commit SHA is the only integrity check

Lake stores no checksum of the fetched sources, and there is nothing like Go's checksum database.
This matters because references are mutable in the manifest.
A tag can be moved to a different commit (`v4.36.0` can be moved to a different commit).
If this commit is malicious, `lake update` will happily fetch it and record the new commit in the lockfile.
Thus, compromising the Lean project.

## The lockfile is compulsory

Lake has two commands that matter here.

- `lake update` resolves dependencies. It turns every Git reference in the manifest into a commit SHA and writes those pins to the lockfile.
- `lake build` compiles the project and all its dependencies. It uses the pinned commits and never resolves anything itself.

Here is what `lake build` does in each case.

1. **No lockfile yet.** This is the one exception. The first build runs an update and creates the lockfile.
2. **A new dependency.** The build stops and asks you to run `lake update`.
3. **A changed `rev`.** The build warns that the lockfile is out of date and keeps using the pinned commit.

Dependencies only move when you run `lake update`.

## The lockfile is flat

The lockfile lists every package in the workspace in one array.
Direct (the declared) dependencies are listed with `"inherited": false` while
transitive dependencies carry `"inherited": true`,

```json
{"name": "batteries",
 "inputRev": "main",
 "rev": "b4b25a3886a16daacaf6615c2eea7170a6e8f458",
 "inherited": true}
```

You cannot tell whether `batteries` sits at depth 2 or depth 5, or which dependency brought it in, and Lake has no `cargo tree` or `npm ls`.

## Post-install hooks exist

A manifest written in Lean is a program, so loading a dependency's manifest already runs its code.
Packages can also register `post_update` hooks.

```lean
post_update pkg do
  let child ← IO.Process.spawn {cmd := "sh", args := #["-c", "echo hello from a dependency"]}
  let _ ← child.wait
```

`lake update` runs the hooks of every package in the workspace, not only the root, and nothing is sandboxed.

## The registry indexes source but hosts binaries

Reservoir has no publish step and only indexes sources, but it runs a build farm and hosts the resulting binaries.

It crawls GitHub daily and lists every repository that meets its [inclusion criteria](https://reservoir.lean-lang.org/inclusion-criteria), which are a public non-fork repository, a lockfile at the repository root, an OSI-approved license and at least two stars.

It builds each package with the toolchain named in its own `lean-toolchain` file, and also with the latest stable and release-candidate Lean releases.
The package page then shows "builds on Lean v4.36.0" or "fails to build", a compatibility signal most registries lack.

## No dependency conflict resolution

Lake does no dependency conflict resolution.
It keeps one copy per package name, never compares two versions of the same package and never backtracks.
`lake update` works in three steps, described in a doc comment in [`Lake/Load/Resolve.lean`](https://github.com/leanprover/lean4/blob/611c117bfaf7b7ae1cfcf246ce6fba31e8f509e9/src/lake/Lake/Load/Resolve.lean#L446-L470).

1. Each `require` of the root is resolved to a commit and stored first, so the root's own pins always win.
2. The lockfile of each direct dependency is read, from the **last declared to the first**. Each entry is copied into the root's lockfile as `inherited`, unless a package with that name is already there.
3. Anything still missing is loaded breadth-first, siblings again in reverse order.

The source gives two reasons for the reverse order.
Later `require`s should shadow earlier ones, like later definitions in a file, and requirements written by the user should beat those inherited from dependencies.

Take the graph from our [earlier post](dependency-resolution/index.md).
The root requires `D1`, `D2`, `D3` and `D4` in that order, and each pulls in a different version of `Dx`.

![Lake reads D4 first, so the lockfile pins Dx v1.5.0](lean_reservoir_assets/lake-resolution.png)

Lake reads `D4`'s lockfile first, finds `Dx v1.5.0` there and copies it into the root lockfile.
The copies under `D3`, `D2` and `D1` are ignored.
Depth plays no role here, because each direct dependency's lockfile already lists its whole subtree, and Lake copies those lockfiles before the breadth-first walk starts.

| Ecosystem | Rule                                                              | `Dx`     |
|-----------|-------------------------------------------------------------------|----------|
| Maven     | Nearest to the root, then first declared                          | `v1.2.0` |
| Go        | Highest of the required minimums (MVS)                            | `v1.5.0` |
| Lake      | Root's own pin, then the lockfile of the last declared dependency | `v1.5.0` |

Because no versions are compared, conflicts are never reported during resolution.
If `D2` was tested against `Dx v1.2.0` and uses an API that `v1.5.0` removed, `lake update` succeeds and the error appears later as a compile error inside `D2`.
The dependencies check compatibility for themselves by compiling.
The fix is a direct `require` for `Dx` in the root, which always wins.

## Takeaway

Lake gets the basics right.
It has a mandatory lockfile, pins transitive dependencies to commits and makes builds reproducible.
Its resolution is deterministic but order sensitive and silent on conflicts, which works because the community lines up around mathlib and the Lean toolchain instead of version ranges.
The weaker side is everything around it.
Integrity rests on Git SHAs, dependencies run code on update, and prebuilt binaries arrive by default without Lake checking them.
Reservoir indexes source on GitHub rather than owning its packages, yet it serves its own builds.
As Lean is increasingly used to verify software, the supply chain that delivers those proofs deserves the same scrutiny as any other.
