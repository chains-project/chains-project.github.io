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
- **Packages are Git repositories built from source.** There is no uploaded *compiled* archive. Lake clones each dependency's repository into `.lake/packages` and builds it locally. This is similar to `node_modules`. Prebuilt binaries are opt-in.
- **Conflicting versions.** A package can be referred to by its Git commit or by a Git reference such as a tag or branch. It can also be referred to by the `version` in its manifest. These can conflict.
- **Mutable references and locked commits.** The manifest allows branches and tags. The lockfile still pins every dependency to a commit SHA.
- **The lockfile is compulsory.** `lake build` only reads the lockfile. A new dependency needs a `lake update` before it builds.
- **The commit SHA is the only integrity check.** Lake keeps no checksum of package contents.
- **The lockfile is flat.** It says whether a dependency is direct or inherited. It does not say how deep it sits or who pulled it in.
- **Post-install hooks exist.** Every package in the workspace can run a `post_update` hook much like npm's `postinstall`.
- **The registry is an indexer.** Reservoir does not store packages. It indexes GitHub repositories and builds each one against recent Lean toolchains to report whether it compiles.
- **No dependency conflict resolution.** Two dependencies can depend on different versions of the same package. Lake has no way to resolve a version that works for both. A conflict is only reported as a compile error when it breaks an API.

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

## Mutable references, locked commits

Requirements may point at branches and tags, both of which can be moved or force-pushed.
Mathlib itself requires most of its own dependencies at `main` or `master`.
What keeps this safe is the lockfile.
Each entry in the lockfile stores the requested revision (`inputRev`) next to the commit it resolved to (`rev`).

```json
{"name": "mathlib",
 "scope": "leanprover-community",
 "url": "https://github.com/leanprover-community/mathlib4",
 "inputRev": "v4.36.0",
 "rev": "66ff77cf0c4c8987...",
 "inherited": false}
```

Watch the naming.
`rev` in the manifest is the request, while `rev` in the lockfile is the locked commit.

A moved tag changes nothing until someone runs `lake update`.
The commit SHA is also the only integrity check.
Lake stores no hash of the fetched sources, and there is nothing like Go's checksum database.
On GitHub those SHAs are SHA-1, hardened against known collision attacks but weaker than the SHA-256 and SHA-512 digests that Cargo and npm record.

## The lockfile is compulsory

`lake build` never resolves dependencies on its own.
It creates the lockfile on the very first build, and after that it only reads it.
Add a `require` and the build stops.

```
$ lake build
error: dependency 'foo' not in manifest; use `lake update foo` to add it
```

Change the `rev` of an existing dependency and Lake only warns that the lockfile is out of date, then keeps building the locked commit.
Only `lake update` moves pins, so builds are reproducible by default.

## A flat lockfile

The lockfile lists every package in the workspace in one array.
Transitive entries carry `"inherited": true`, and that is all the structure there is.

```json
{"name": "batteries",
 "inputRev": "main",
 "rev": "1804c8a02e64fdd55b24db6de5738ffa128d1ec1",
 "inherited": true}
```

You cannot tell whether `batteries` sits at depth 2 or depth 5, or which dependency brought it in, and Lake has no `cargo tree` or `npm ls`.
Reservoir's API does list the dependencies of each indexed revision, but only per package.

## Post-install hooks exist

A manifest written in Lean is a program, so loading a dependency's manifest already runs its code.
Packages can also register `post_update` hooks.

```lean
post_update pkg do
  let child ← IO.Process.spawn {cmd := "sh", args := #["-c", "echo hello from a dependency"]}
  let _ ← child.wait
```

`lake update` runs the hooks of every package in the workspace, not only the root, and nothing is sandboxed.
The Lean kernel checks your proofs, but not what a manifest, a hook or a native `extern_lib` build does on your machine.

## Source by default, binaries on request

Lake works like npm's `node_modules`.
Every dependency is cloned into `.lake/packages` inside the project and built from source.
Building mathlib from source takes hours, so there are two shortcuts.

- `lake exe cache get` is mathlib's own tool. It downloads prebuilt `.olean` files for the locked mathlib commit.
- `preferReleaseBuild := true` makes Lake download a package's build archive from its GitHub release, uploaded with `lake upload`.

Neither download carries a signature or build provenance.

## The registry is an indexer

Reservoir has no publish step.
It crawls GitHub daily and lists every repository that meets its [inclusion criteria](https://reservoir.lean-lang.org/inclusion-criteria), which are a public non-fork repository, a lockfile at the repository root, an OSI-approved license and at least two stars.
Packages are named `@owner/name`, so the namespace and access control are GitHub's.
There is no trusted publishing because there is no publishing, and there is no advisory database or malware scanning.

What Reservoir does add is a build farm.
It builds each package against recent Lean toolchains and shows "builds on v4.36.0" or "fails to build" on the package page, a compatibility signal most registries lack.
Lake enforces the same contract locally.
`lake update` bumps the root `lean-toolchain` to the newest toolchain compatible with the direct dependencies and restarts itself through elan.

## Dependency resolution

Lake does no dependency conflict resolution.
It keeps one copy per package name, never compares two versions of the same package and never backtracks.
`lake update` works in three steps, described in a doc comment in [`Lake/Load/Resolve.lean`](https://github.com/leanprover/lean4/blob/master/src/lake/Lake/Load/Resolve.lean).

1. Each `require` of the root is resolved to a commit and stored first, so the root's own pins always win.
2. The lockfile of each direct dependency is read, from the **last declared to the first**. Each entry is copied into the root's lockfile as `inherited`, unless a package with that name is already there.
3. Anything still missing is loaded breadth-first, siblings again in reverse order.

The source gives two reasons for the reverse order.
Later `require`s should shadow earlier ones, like later definitions in a file, and requirements written by the user should beat those inherited from dependencies.

Take the graph from our [earlier post](dependency-resolution/index.md).
The root requires `D1`, `D2`, `D3` and `D4` in that order, and each pulls in a different version of `Dx`.

<pre class="mermaid">
flowchart TD
  R[Project]
  R -->|"read 4th"| D1
  R -->|"read 3rd"| D2
  R -->|"read 2nd"| D3
  R -->|"read 1st"| D4
  D1 --> D11 --> Dx1["Dx v1.0.0"]
  D2 --> Dx2["Dx v1.2.0"]
  D3 --> D31 --> D311 --> Dx3["Dx v1.3.0"]
  D4 --> Dx4["Dx v1.5.0"]
  Dx4 -.->|"first seen, copied"| M[("lockfile pins Dx v1.5.0")]
  classDef win fill:#d4edda,stroke:#2e7d32,stroke-width:2px
  class Dx4,M win
</pre>

<script type="module">
  import mermaid from "https://cdn.jsdelivr.net/npm/mermaid@11/dist/mermaid.esm.min.mjs";
  mermaid.initialize({ startOnLoad: true });
</script>

Lake reads `D4`'s lockfile first, finds `Dx v1.5.0` there and keeps it.
The copies under `D3`, `D2` and `D1` are ignored.
Depth plays no role, because every dependency's lockfile is already flat.

| Ecosystem | Rule                                                              | `Dx`     |
|-----------|-------------------------------------------------------------------|----------|
| Maven     | Nearest to the root, then first declared                          | `v1.2.0` |
| Go        | Highest of the required minimums (MVS)                            | `v1.5.0` |
| Lake      | Root's own pin, then the lockfile of the last declared dependency | `v1.5.0` |

Lake agrees with Go here, but for a different reason.
Go picks `v1.5.0` because it is the highest, Lake picks it because `D4` is declared last.
Move `D4` to the top of the `require` list and Lake reads `D3`'s lockfile first and picks `v1.3.0`, the deepest copy in the tree.

Because no versions are compared, conflicts are never reported during resolution.
If `D2` was tested against `Dx v1.2.0` and uses an API that `v1.5.0` removed, `lake update` succeeds and the error appears later as a compile error inside `D2`.
The dependencies check compatibility for themselves by compiling.
The fix is a direct `require` for `Dx` in the root, which always wins.

## Takeaway

Lake gets the basics right.
It has a mandatory lockfile, pins transitive dependencies to commits and makes builds reproducible.
Its resolution is deterministic but order sensitive and silent on conflicts, which works because the community lines up around mathlib and the Lean toolchain instead of version ranges.
The weaker side is everything around it.
Integrity rests on Git SHAs, dependencies run code on update, prebuilt binaries are unsigned, and Reservoir is an index over GitHub rather than a registry that owns its packages.
As Lean is increasingly used to verify software, the supply chain that delivers those proofs deserves the same scrutiny as any other.
