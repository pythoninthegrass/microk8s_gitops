# microk8s_gitops

[![pre-commit](https://img.shields.io/badge/pre--commit-enabled-brightgreen?logo=pre-commit&logoColor=white&style=flat-square)](https://github.com/pre-commit/pre-commit)
[![update-flux](https://github.com/angelnu/k8s-gitops/workflows/update-flux/badge.svg)](https://github.com/angelnu/k8s-gitop/workflows/flux-update-schedule/actions)
<!-- ![renovate](https://img.shields.io/badge/Renovate?style=flat-square&link=https%3A%2F%2Fapp.renovatebot.com%2Fdashboard) -->

Leverage Flux to automate cluster state using code living in this repo.

## Repo structure

The Git repository contains the following directories under `cluster` and are ordered below by how Flux will apply them.

- **base**: directory is the entrypoint to Flux
- **crds**: directory contains custom resource definitions (CRDs) that need to exist globally in your cluster before anything else exists
- **core**: directory (depends on **crds**) are important infrastructure applications (grouped by namespace) that should never be pruned by Flux
- **apps**: directory (depends on **core**) is where your common applications (grouped by namespace) could be placed, Flux will prune resources here if they are not tracked by Git anymore

```
.
├── cluster
│   ├── apps
│   │   ├── default
│   │   └── networking
│   ├── base
│   │   └── flux-system
│   ├── core
│   │   ├── cert-manager
│   │   ├── kubed
│   │   ├── metallb-system
│   │   └── namespaces
│   └── crds
│       ├── cert-manager
│       └── metallb
├── docs
└── standalone
```

## Tools

| Tool                                                   | Purpose                                                    |
|--------------------------------------------------------|------------------------------------------------------------|
| [sops](https://github.com/mozilla/sops)                | Simple and flexible tool for managing secrets              |
| [pre-commit](https://github.com/pre-commit/pre-commit) | Ensure the YAML and shell script in my repo are consistent |
| [task](https://taskfile.dev/)                          | Task is a task runner / build tool|                        |

## Further Reading

[flux](https://github.com/fluxcd/flux2)

[awesome-home-kubernetes](https://github.com/k8s-at-home/awesome-home-kubernetes)
