# Why the directory structure

- [Flux documentation](https://fluxcd.io/flux/guides/repository-structure/)

## Delivery management 
In trunk-based development, the changes are made in small batches and are merged into the main branch often. Besides main, branches are short-lived, once a pull request is merged, the branch gets deleted.

New app release can be automatically delivered to staging using Flux’s image updates to Git. For production, you may choose to manually approve app version bumps by configuring Flux to push the changes to a new branch from which you can create a pull request. You can limit the impact of an issue that escaped staging testing by using Flagger’s canary releases.

Changes to infrastructure can be disruptive and could cause cluster-wide outages. These config changes can be made in steps, first you merge a change to staging, when the cluster is successfully reconciled, and the new cluster state passes conformance tests, you then promote the change to production. The promotion process is gated by PR reviews and end-to-end testing.