# NixCon 2022: A Brief Summary

[NixCon](https://2022.nixcon.org/), the yearly convention for all things Nix was
held in Paris this year. I attended as a member of the [Consistent Hardening and
Analysis of software supply chaINS (CHAINS)](https://chains.proj.kth.se/)
project. CHAINS is a team of researchers and engineers based in the KTH Royal
Institute of Technology in Stockholm, Sweden, working towards a more secure
software supply chain. The project is funded by the [Swedish Foundation for
Strategic Research](https://strategiska.se/).

## What Nix is

Nix is a package manager, first imagined by [Eelco
Dolstra](https://www.linkedin.com/in/edolstra/) in his soon-to-be twenty years
old doctoral dissertation [_The Purely Functional Software Deployment
Model_](https://edolstra.github.io/pubs/phd-thesis.pdf). It differs from other
package managers, such as Debian’s apt or Fedora’s yum, by its strong guarantees
of reproducibility; Nix lists all components and dependencies of a software
package, not just by name and version, but also with a cryptographic hash of
their source code and build environments. This allows consumers of a package to
reproduce not only the package’s binary, but also its entire runtime
environment. As a consequence, what works on my machine is as good as guaranteed
to work on yours.

Nix is not a one-trick pony. Besides being a package manager, it has a
Linux-based operating system called NixOS built on top of it. Nix also comes
with its own programming language, the Nix expression language. It is a far cry
from declarative configuration languages such as YAML. To my novice eyes, it
appears to be a mix of ML and JSON.

As an example, the following snippet will create a Python 3.9 environment with
the packages `numpy` and `pandas` installed:

```nix
{ pkgs ? import <nixpkgs> {} }:
pkgs.python3.withPackages (ps: with ps; [ numpy pandas ])
```

To run it, save it in a file called `shell.nix` and run `nix-shell`. This will
start a shell session with the requisite packages installed.

The high complexity of the Nix ecosystem can
make getting into Nix a daunting task. But Nix is growing, rapidly. As Eelco
Dolstra explained in his inaugural talk, half of the stars on Nix’s Github has
been accrued in the past year. For a nearly two decades old project, that is
impressive growth.

## NixCon 2022

The talks at the conference ranged from the highly technical and esoteric to the
very general and non-technical. There was no explicitly supply chain related
talks, but there was an awareness that the software supply chain is a topical
issue, together with sometimes rather bold claims about Nix's usefulness. Ron
Efroni, Nix board member and CEO of [Flox](https://floxdev.com/), were among the
most vocal regarding supply chains. He claimed that Nix “inherently solves”
[SLSA](http://slsa.dev/), the recently announced framework for supply chain
security, and that Nix replaces the entire DevOps ecosystem.

The talk that was most CHAINS-adjacent was [_Reproducibly building artifacts
that contain embedded
signatures_](https://talks.nixcon.org/nixcon-2022/talk/JHVF8N/), given by
[Martin
Schwaighofer](https://talks.nixcon.org/nixcon-2022/speaker/HMYGKG/twitter.com/mschwaig).
He tackled the problem of reproducibly building cryptographically signed
executables. Cryptographic signatures of executables are used for providing
trust in the source of a program. If the executable has been signed by a party
that you trust, you can run it with confidence. But this confidence is based on
the fact that only the trusted party has access to the signing keys. Since the
signature is embedded into the resulting artifact, it is not reproducible by
anyone but the signer, which defeats the main purpose of reproducible builds;
third parties need to be able to reproduce the build in order to attest to its
integrity. Martin approached this problem by creating two separate derivations
(a derivation is a build action in Nix), only one of which is signed, and
comparing the differences between the two. The reproducibility of the unsigned
derivation allows for verification of the signed one.

Reproducibility is not all about software security. [Markus
Kowalewski](https://www.su.se/profiles/mako5582-1.379187) of Stockholm
University gave [a talk](https://talks.nixcon.org/nixcon-2022/talk/MYHSKT/)
about how he uses Nix as a part of his research in computational chemistry. The
high performance computing software that underpins his research is often made in
house at the academic institutions that uses them. The programs tend to grow
organically over many years, as demands change. Often, however, maintainability
is not the primary concern of the programmers. They are chemists that need to
run an experiment, not software engineers. Since the code tends to be quite low
level, reproducibility quickly becomes a concern. The output may depend subtly
on the exact versions of libraries for scientific computations, and sometimes
even on the hardware on which it is executed. Prof. Kowalewski explained that
Nix allowed him to eliminate variable factors, which increased the
reproducibility and maintainability of his software. In other words, Nix helped
scientific experiments to be reproducible.

These were just a few highlights from the conference. A complete schedule with
all talks and speakers can be found
[here](https://talks.nixcon.org/nixcon-2022/schedule/).

## Final thoughts

There is a new focus among the Nixsters. Soft skills were a hot topic this year;
community management, onboarding of newcomers, and improved documentation was
discussed inbetween the highly technical and specialized talks. The Nix board
has recently been remade entirely to better serve these purposes. This is all a
reaction to the quick growth of the community, and more work is needed. Nix is
still confusing for beginners, but the onboarding experience is slowly
improving. The Nix community is a welcoming one, and I hope that it will
continue to grow and mature.

The lofty claims about Nix's role in the supply chain are perhaps not without
grounding. A lot of what is considered best practices now, such as building
software reproducibly on hermetic build servers, has been done by the Nix
community for a long time, in this case with their
[Hydra](https://hydra.nixos.org/build/196107287/download/1/hydra/) CI server. An
admittedly quite barebones demonstration of where Nix lines up with SLSA can be
seen [here](https://github.com/tomberek/slsa-demo). (Check out the Makefile to
see how different Nix commands can be used to fulfil SLSA requirements.)

But Nix is no panacea. There are many moving parts in every software supply chain, and package management forms only a part of it. Nix brings a lot of good ideas to the table, and I like the confidence of the community, but I am not sure that it is the silver bullet that some claim it to be. I am looking forward to seeing how the Nix community will continue to grow and mature.

## Key takeaways

- Nix is old, but it is suddenly growing rapidly.
- Nix enables reproducibility of software and its runtime environment.
- Nix provides hashes of all dependencies, which can be used to verify the integrity of a build.
- Nix is not a one-trick pony. It is a package manager, a Linux distribution, and a programming language.
- The Nix community is convinced that Nix will take over the world, but the onboarding experience must improve before it becomes mainstream.


-- Arvid Siberov
