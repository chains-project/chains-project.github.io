# Dependency Resolution in Different Ecosystems

The post discusses how different package managers resolve dependencies while for building.

## Maven

[Maven](https://maven.apache.org/) is a build tool for building Java projects.
It defines dependencies in terms of three attributes - `groupId`,
`artifactId`, and `version`.
For
example, [`io.github.chains-project:collector-sahab:0.5.3`](https://mvnrepository.com/artifact/io.github.chains-project/collector-sahab/0.5.3),
is a maven dependency where `groupId` is `io.gihub.chains-project`,
`artifactId` is `collector-sahab`, and version is `0.5.3`.
So, when a project is built, Maven resolves the dependencies by looking for
these attributes.

However, if there are more than one dependency with same `groupId` and
`artifactId`, it keeps only one version of that dependency.
It decides the version to keep based on the following algorithm.

1. Choose dependency at the minimum depth in the dependency 
   tree with respect to the project.
2. If depth is same, the first sibling is selected.

Let's consider an example.
The following graph is dependency tree of a project, and we resolve
dependency `Dx` based on the above resolution algorithm.
Note that the tree is ordered.
`D1`, `D2`, `D3`, and `D4` are declared in an order and the tree reflects it
by showing it left to right.

<img src="dependency-graph.svg">

First, we find out the minimum depth of `Dx`.
It is `2` in the branch of `D2` and `D4`.
So it has to be either `Dx v1.2.0` or `Dx v1.5.0`.

Then, we select the first sibling.
Based on this tree, it is `Dx v1.2.0` because it appears first in the tree
if we scan the tree left to right.
Thus, `Dx` is resolved to `v1.2.0`.

## Go

To manage dependencies, Go uses _Modules_.
In Go, a module is identified by its _module path_ and a _version_.
A module used as a dependency is recorded in the `go.mod` file.
For instance `github.com/BurntSushi/toml v1.3.2`, where `github.com/BurntSushi/toml` is the module path, and `v1.3.2` is the version (semver).

To resolve the modules which are to be included in a build, it uses an algorithm called [Minimal Version Selection (MVS)](https://research.swtch.com/vgo-mvs) to generate a _build list_.
For dependency resolution, we only need to understand the first step in this algorithm i.e. - [Construct Build List](https://research.swtch.com/vgo-mvs#algorithm_1)

Consider the above dependency graph as an example.

To determine which modules make the build list, it looks into the `go.mod` files of both the main module and its dependencies, and traverses the graph of all reachable modules/versions.
During this traversal, a _rough list_ is created. The rough list will contain all reached modules. In our example: \[`D1`, `D11`, `Dx v1.0.0`, `D2`, `Dx 1.2.0` `D3`, `D31`, `D311`, `Dx v1.3.0`, `D4`, `Dx v1.5.0`\].

The rough list is then simplified, by keeping only the newest version of any listed module.
Hence, `Dx` which has the highest `semver` version is selected and that is `Dx v1.5.0`.

By following this algorithm, the build list is guaranteed to include the oldest module versions available that meet the requirements, thus achieving reproducible behavior.

## Node.js + npm

[npm](https://docs.npmjs.com/about-npm) is a package manager for [Node.js](https://nodejs.org/en), it facilitates the installation of dependencies for use by Node.js.
To understand what dependency is used at runtime, we need to understand how both npm and Node.js work.

Node.js resolves dependencies at runtime.
To do this it starts to look for a folder structure matching the dependency name inside a `node_modules/` directory in the directory of the file importing the dependency.
If it is not found it will repeat this process in the parent folder. This is repeated recursively until the root directory is reached ([ref](https://nodejs.org/docs/latest-v20.x/api/modules.html#loading-from-node_modules-folders)).
Importantly, this is also how transitive dependencies are resolved.

This means that for a file at `/home/example/projects/file.js` on a Unix-like system it will look for the dependency in order, returning the first instance it finds, in the following places:

```text
/home/example/projects/node_modules/
/home/example/node_modules/
/home/node_modules/
/node_modules/
```

And, if the [`--no-global-search-paths`](https://nodejs.org/docs/latest-v20.x/api/cli.html#--no-global-search-paths) option isn't used, it would also look in the following places:

```text
$NODE_PATH/node_modules
$HOME/.node_modules
```

As a package manager for Node.js, npm installs dependencies by downloading them from the internet (a package registry or source repository) and putting them in the `node_modules/` directory.
For re-used dependencies two things may happen.
If a common version is supported by multiple dependencies, npm will try to put the common version directly in the `node_modules/` directory of the root project, where it can be shared.
If a transitive version of a dependency is not supported by other dependencies according to [SemVer](https://semver.org/) rules, it will instead by installed in the `node_modules/` directory of the dependency that needs it, where it isn't shared.

npm's dependency version resolution algorithm is roughly as follows.
When installing a new dependency, npm will try to use the latest available version of each dependency such that it can be reused the most.
This may result in downgrading of a previously installed dependency or installing a dependency multiple times if no common version is available (e.g. two different major versions).
Further control over the resolution is possible through commands such as `npm upgrade` and `npm dedupe` which can upgrade dependencies on a specific path and try to reduce unnecessary dependency duplication respectively.

Consider the above dependency graph as an example.
If the version constraint of `Dx` for all parent dependencies is something like `^1.0.0` (i.e. any version at or above 1.0.0 but below 2.0.0) it will be installed only once, say as `1.6.0`, at `node_modules/Dx`.
If instead `D11` depends on exactly `1.0.0` and all others depend on `^1.0.0` it will still be installed only once at `node_modules/Dx` but as `1.0.0`.
If instead `D11` depends on exactly `1.0.0` and all other depends on `^1.2.0`, `Dx` will be installed twice: once as `1.6.0` at `node_modules/Dx` and once as `1.0.0` at `node_modules/D11/node_modules/Dx`.

If a lockfile is used by the parent project, the contents of the `node_modules/` directory are, and by extension Node.js' dependency resolution is, entirely reproducible (ignoring installation scripts).

## Python
### pip
pip is the package installer for Python and included with modern versions of Python, it is used to find, download, and install packages from [PyPI](https://pypi.org/) and other Python package indexes.

The process of package resolution in pip relies on three key pieces of information: `project name`, `release version` and `dependencies`. The first two pieces of information identify an individual “candidate” for installation, and the third one is used on “on demand” when backtracking algorithm starts to check that particular candidate.

When `pip install` is executed, pip first performs a dependency resolution process by analyzing all the dependencies of the requested packages to determine the most compatible version (starts from latest version that satisfies the given constraints). The resolution process might involve backtracking to find the best combination that satisfies all dependency constraints. Only one version of a dependency will get installed.

The resolution process is based on a separate package, [`resolvelib`](https://pypi.org/project/resolvelib/) which implements an abstract backtracking resolution algorithm. `resolvelib` implements  [backjumping technique](https://en.wikipedia.org/wiki/Backjumping) in [1.0.0]((https://github.com/sarugaku/resolvelib/blob/main/CHANGELOG.rst)) version which was [vendored](https://pip.pypa.io/en/stable/news/#v23-1) from `pip 23.1`, it can find a set of packages that meet requirements and whose requirements themselves don't conflict.

Now, consider the above dependency graph as an example. 

When
- `D11==1.0.0` depends on version `Dx==1.1.0`, 
- `D2==2.0.0` depends on version `Dx==1.2.0`, 
- `D311==3.0.0` depends on version `Dx==1.3.0`, 
- `D4==4.0.0` depends on version `Dx==1.5.0`, 

You will get a `ResolutionImpossible` [error](https://pip.pypa.io/en/stable/topics/dependency-resolution/#understanding-your-error-message) since all four dependents requires exact version and the conflict couldn't be resolved.

There are two ways to avoid `ResolutionImpossible` error.

**Dependency version specifier is flexible**
- `D11==1.0.0` depends on version `Dx>=1.1.0`, 
- `D2==2.0.0` depends on version `Dx>=1.2.0`, 
- `D311==3.0.0` depends on version `Dx>1.3.0`, 
- `D4==4.0.0` depends on version `Dx==1.5.0`, 

The resolved version for `Dx` will be `1.5.0`.

**Parent version specifier is flexible**

- `D11>=1.0.0` depends on version `Dx==1.1.0`, 
- `D2>=2.0.0` depends on version `Dx==1.2.0`, 
- `D311<=3.0.0` depends on version `Dx==1.3.0`, 
- `D4~=4.0.0` depends on version `Dx==1.5.0`, 

`pip` will automatically find a version for dependent that can fulfill all the requirements. For example, if `D11 v1.1.0`, `D2 v2.4.0`, `D311 v2.6.0`  and `D4 v4.0.3` are all dependent upon `Dx 1.3.0`, then the resolved version for `Dx` would be`1.3.0`.



