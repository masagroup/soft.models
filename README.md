<!--
sword:
  schema: 1
  name: soft.models
  family: ecore-esync
  kind: ecore-model
  generation: shared
  shipped: false # UNVERIFIED
  languages: [XML, Ecore]
  build: [none]
  ng: [ecore-model]
  apps: []
-->

# soft.models

> Ecore meta-models (`.ecore` XMI files) that the SOFT code generators consume to produce the `soft.cpp`, `soft.go` and `soft.ts` Ecore runtime libraries and their tests; data only, no executable code.

| | |
|---|---|
| **Family** | Ecore / esync |
| **Languages** | XML (Ecore/XMI), Eclipse launch XML. No Go, C++, TypeScript or Python source. |
| **Build systems** | None (no `build.xml`, Dockerfile, CMake, `go.mod`, Makefile or `package.json`) |

**[Architecture](ARCHITECTURE.md)** · [Contributing](CONTRIBUTING.md) · [known issues and open questions](https://github.com/masagroup/wiki/wiki/known-issues#soft.models) · [repository on GitHub](https://github.com/masagroup/soft.models)

## Overview

`soft.models` holds the input models of the SOFT generator chain: `ecore.ecore`, the SOFT port of the Eclipse EMF Ecore metamodel annotated with per-language generator hints, and the sample models `library`, `tournament` and `empty`. Generating from `ecore.ecore` produces the Ecore runtime itself in [soft.go](https://github.com/masagroup/soft.go), [soft.ts](https://github.com/masagroup/soft.ts) and [soft.cpp](https://github.com/masagroup/soft.cpp); the sample models generate their tests and examples. Data only, no executable code.

## Where to start

| You want to... | Read |
|---|---|
| generate code from these models | [soft.gen](https://github.com/masagroup/soft.gen) and [Use it](#use-it) below |
| understand how the models are consumed | [ARCHITECTURE.md](ARCHITECTURE.md) |
| contribute | [CONTRIBUTING.md](CONTRIBUTING.md) |

## Build

There is nothing to build: the other repositories read this one as a sibling folder `../models` (or as a git submodule of [soft](https://github.com/masagroup/soft)).

```
git clone git@github.com:masagroup/soft.models.git models
```

### Use it

Regenerate the runtimes from the models through their Makefiles, which mount `../models`:

```
cd ../soft.go && make generate   # Go runtime and tests
cd ../soft.ts && make generate   # TypeScript runtime and examples
```

Run the generator on a model directly with the soft.gen image:

```
docker run --rm -v "$PWD":/gen -w /gen masagroup/soft.gen go -m /gen/library.ecore -o /gen/out   # or: ts
```

The `generate.*.launch` files are Eclipse run configurations of the former Java generators (soft.gen v1); their arguments are in [ARCHITECTURE.md](ARCHITECTURE.md#interfaces). UNVERIFIED: whether they still run.

## Documentation and guides

- [Architecture](ARCHITECTURE.md): position in the ecosystem, repository layout, internal structure, how it works (diagrams), dependencies.
- [Contributing](CONTRIBUTING.md): development environment, Git and Jira workflow, conventions, CI/CD.
- [Known issues and open questions](https://github.com/masagroup/wiki/wiki/known-issues#soft.models): the known defects and open points of the repository, kept in the SWORD wiki.
- Related repositories: [soft](https://github.com/masagroup/soft), [soft.cpp](https://github.com/masagroup/soft.cpp), [soft.gen](https://github.com/masagroup/soft.gen), [soft.go](https://github.com/masagroup/soft.go), [soft.ts](https://github.com/masagroup/soft.ts).
- Transverse pages: [CI/CD pipelines](https://github.com/masagroup/wiki/wiki/cicd-pipelines), [Ecosystem today](https://github.com/masagroup/wiki/wiki/ecosystem-current), [Ecosystem next gen](https://github.com/masagroup/wiki/wiki/ecosystem-nextgen), [Glossary](https://github.com/masagroup/wiki/wiki/glossary).
- Repository on GitHub: [masagroup/soft.models](https://github.com/masagroup/soft.models).
- The same documentation in the SWORD wiki: [soft.models](https://github.com/masagroup/wiki/wiki/soft.models), [architecture](https://github.com/masagroup/wiki/wiki/soft.models-architecture), [contributing](https://github.com/masagroup/wiki/wiki/soft.models-contributing).
