# Build Resolution in Different Ecosystems

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

```mermaid
graph TD
;
    Project ~~~ |depth=0| Project;
    D4 ~~~ |depth=1| D4;
    Project --> D1;
    
    D1 --> D11
    D11 --> Dx1["Dx v1.0.0"]
    Project --> D2;
    D2 --> Dx2["Dx v1.2.0"]
    Project --> D3;
    D3 --> D31;
    D31 --> D311;
    D311 ~~~ |depth=3| D311
    D311 --> Dx3["Dx v1.3.0"]
    Dx3 ~~~ |depth=4| Dx3
    Project --> D4;
    Dx4 ~~~ |depth=2| Dx4
    D4 --> Dx4["Dx v1.5.0"]
```

First, we find out the minimum depth of `Dx`.
It is `2` in the branch of `D2` and `D4`.
So it has to be either `Dx v1.2.0` or `Dx v1.5.0`.

Then, we select the first sibling.
Based on this tree, it is `Dx v1.2.0` because it appears first in the tree
if we scan the tree left to right.
Thus, `Dx` is resolved to `v1.2.0`.

## Go

