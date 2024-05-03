# FluxCD demo

This repository stores the **desired state**[^1] of a system managed by [GitOps] using [FluxCD].

```bash
├── clusters
│   └── my-cluster                     # 2
│       ├── flux-system                # 1
│       │   ├── gotk-components.yaml
│       │   ├── gotk-sync.yaml         # 2a
│       │   └── kustomization.yaml
│       ├── podinfo-kustomization.yaml # 4
│       └── podinfo-source.yaml        # 3
└── README.md
```

1. Flux components **manifests**

   The prefix `gotk` stands for _GitOps Toolkit_

2. **Flux components** (the one deployed in Kubernetes Cluster) will track the path `/clusters/my-cluster/` in this repository

   a. Changes made to the **Kubernetes manifests** in the `main` branch at the path `/clusters/my-cluster/` of this repository are _reflected_ in Kubernetes **cluster**.

3. A `GitRepository` manifest pointing to `podinfo` repository’s `main` branch

   When the current `GitRepository` revision differs from the latest fetched revision, a new **Artifact** is archived.

4. A `Kustomization` that applies the `podinfo` deployment

> [!TIP]
> GitOps Toolkit is a set of
>
> - specialized tools and Flux Controllers
> - composable APIs
> - reusable Go packages for GitOps under the fluxcd GitHub organisation
>
> for building Continuous Delivery on top of Kubernetes.
>
> For more information, see [GitOps Toolkit components]

For more information, see [Get Started | FluxCD Docs]

[FluxCD]: https://fluxcd.io/
[GitOps]: https://github.com/open-gitops/documents/blob/v1.0.0/PRINCIPLES.md
[GitOps Toolkit components]: https://fluxcd.io/flux/components/
[Get Started | FluxCD Docs]: https://fluxcd.io/flux/get-started/

[^1]: <https://github.com/open-gitops/documents/blob/v1.0.0/GLOSSARY.md#desired-state>
