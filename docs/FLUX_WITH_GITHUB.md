# Flux bootstrap for Github

- [Resource](https://fluxcd.io/flux/installation/bootstrap/github/)

1. Generate a GitHub PAT
2. Use our container to store the GITHUB_TOKEN

    ```sh
    export GITHUB_TOKEN=<gh-token>
    ```

3. Setup GitHub Personal Account

    NOTE: Insert the cluster after /fluxcd/clusters/ on which cluster you want to deploy

    ```sh
    flux bootstrap github \
        --token-auth \
        --owner=zinknotthemetal \
        --repository=intro-to-flux \
        --branch=main \
        --path=fluxcd/clusters/local-kind \
        --personal
    ```

4. Verify that flux is in place and working as expected

```sh
flux check

# flux tools installed by flux
kubectl -n flux-system get GitRepository
kubectl -n flux-system get Kustomization
```
